---
title: "bir çok kiracılı SaaS uygulamasında birçok Azure SQL veritabanı performansını aaaMonitor | Microsoft Docs"
description: "İzleme ve veritabanları ve hello Azure SQL veritabanı Wingtip SaaS uygulama havuzlarında performansını yönetme"
keywords: "sql veritabanı öğreticisi"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Merhaba Wingtip SaaS uygulama performansını izleme

Bu öğretici kapsamında, SaaS uygulamalarında kullanılan birkaç önemli performans yönetim senaryolarını ele alınan dizelerle. Tüm Kiracı veritabanları arasında bir yük Oluşturucu toosimulate etkinlik kullanıldığında hello yerleşik izleme ve uyarma özelliklerini SQL veritabanı ve esnek havuzlar gösterilmiştir.

Merhaba Wingtip SaaS uygulaması her salonundan (Kiracı) kendi veritabanına sahip olduğu bir kiracı tek veri modeli kullanır. Birçok SaaS uygulamaları gibi öngörülemeyen ve kullanımın Kiracı İş yükü düzeni hello beklenen. Diğer bir deyişle, bilet satışı herhangi bir zamanda gerçekleşebilir. tootake bu modelinin avantajı, tipik veritabanı kullanım, Kiracı veritabanları esnek veritabanı havuzları halinde dağıtılır. Esnek havuzlar kaynakları birçok veritabanı arasında paylaşarak bir çözüm hello maliyetini en iyi duruma getirme. Bu tür deseni önemli toomonitor veritabanıdır ve yükler havuzu kaynak kullanım tooensure makul havuzlardaki dengeli. Tek veritabanlarını yeterli kaynaklara sahip olduğunuzdan ve havuzları değil basarsa tooensure etmeniz kendi [eDTU](sql-database-what-is-a-dtu.md) sınırlar. Bu öğretici yolları toomonitor inceler ve veritabanları ve havuzları, yönetmek ve nasıl yanıt toovariations iş yükü de tootake düzeltme eylemi.

Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]

> * Sağlanan yük Oluşturucu çalıştırarak hello Kiracı veritabanı kullanımı benzetimi
> * Yük toohello artış yanıt olarak İzleyicisi Merhaba Kiracı veritabanları
> * Merhaba yanıt toohello artan veritabanı yük esnek havuzda ölçeklendirme
> * İkinci bir esnek havuz tooload Bakiye veritabanı etkinliklerini sağlama


Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:

* Merhaba Wingtip SaaS uygulaması dağıtılır. beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)
* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toosaas-performance-management-patterns"></a>Giriş tooSaaS performans yönetim desenleri

Veritabanı performansı yönetme derleme ve performans verilerini çözümleme ve ardından uygulamanız için bir kabul edilebilir yanıt süresi parametreleri toomaintain ayarlayarak toothis veri tepki oluşur. Birden çok kiracıya barındırdığında, esnek veritabanı havuzları uygun maliyetli şekilde tooprovide olan ve öngörülemeyen iş yükleri ile grubu için kaynaklar yönetin. Bazı iş yükü düzenlerinde iki S3 veritabanı bile tek bir havuzda yönetilebilir.

![medya](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

Havuzları ve havuzları hello veritabanlarında performansı kabul edilebilir aralık içinde kalırlar izlenen tooensure olması gerekir. Merhaba havuzu yapılandırma toomeet hello gereksinimlerini hello hello havuz Edtu hello için uygun olduğundan emin olduktan tüm veritabanlarının toplam iş yükü ince ayar genel iş yükü. Hello veritabanı başına min ve veritabanı başına maksimum eDTU değerleri tooappropriate değerleri, belirli bir uygulama gereksinimleri ayarlayın.

### <a name="performance-management-strategies"></a>Uygulama performansı stratejileri

* toomanually performansı izleyebilir, sahip tooavoid çok en etkili**veritabanları veya havuzları dışında normal aralıkları parazit durumlarda tetikleyen uyarıları ayarlama**.
* bir havuzu hello performans düzeyini toorespond tooshort terim dalgalanmalara hello **havuz eDTU düzeyi ölçeklendirilmiş yukarı veya aşağı**. Bu dalgalanmayı normal veya öngörülebilir bir temelinde oluşursa **hello havuzu ölçeklendirme olabilir zamanlanmış toooccur otomatik olarak**. Örneğin, iş yükünüzün hafif olduğunu bildiğiniz gece veya hafta sonları gibi zamanlarda ölçeği azaltabilirsiniz.
* toorespond toolonger terim dalgalanmaları veya değişiklikler hello veritabanları, sayısı **tek veritabanlarını diğer havuzlara taşınabilir**.
* toorespond tooshort terim artırır *tek tek* veritabanı yük **tek veritabanlarını dışında bir havuzu alınır ve bir bireysel performans düzeyi atanan**. Merhaba yükü daha azdır sonra hello veritabanı sonra toohello havuzu döndürülebilir. Bu önceden bilindiğinde veritabanları pre-emptively tooensure hello veritabanı her zaman gerekli hello kaynakları ve tooavoid etkisi hello havuzunda diğer veritabanlarında sahip taşınabilir. Bu gereksinim tahmin edilebilir, popüler bir olay için bilet satış sağladığından yaşayan salonundan gibi ise, bu yönetim davranış hello uygulamasına tümleştirilebilir.

Merhaba [Azure portal](https://portal.azure.com) yerleşik izleme ve çoğu kaynaklardaki uyarı sağlar. SQL Veritabanı için veritabanı ve havuzlarda izleme ve uyarı özellikleri kullanılabilir. Küçük sayıda kaynağı için uygun toouse, ancak birçok kaynaklarla çalışırken çok uygun değil izleme ve uyarma bu yerleşik kaynak özgü olduğundan.

Burada çalıştığınız birçok reources ile yüksek hacimli senaryolar için [günlük analizi (OMS)](sql-database-saas-tutorial-log-analytics.md) kullanılabilir. Verilmiş tanılama günlüklerini ve günlük analizi çalışma alanındaki toplanan telemetri üzerinden analytics sağlayan ayrı bir Azure hizmet budur. Günlük analizi birçok Hizmetleri'nden telemetri toplamak ve kullanılan tooquery olması ve Uyarıları ayarlayın.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Merhaba Wingtip uygulama kaynak koduna ve komut dosyaları alma

Merhaba Wingtip SaaS komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. [Adımları toodownload hello Wingtip SaaS betikleri](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Ek kiracılar sağlama

Havuzlar yalnızca iki S3 veritabanları ile düşük maliyetli olabilirler, ancak etkili ortalaması hello hale hello havuzu hello daha düşük maliyetli olan daha fazla veritabanlarını hello. Performans izleme ve yönetiminin ölçeklenerek nasıl çalıştığını anlamak için bu öğreticide en az 20 veritabanınızın dağıtılmış olması gerekir.

Önceki bir öğreticide kiracılar toplu zaten sağlanan varsa, toohello atlayın [tüm Kiracı veritabanları benzetim kullanımı](#simulate-usage-on-all-tenant-databases) bölümü.

1. Aç... \\Öğrenme modülleri\\performans izleme ve Yönetim\\*Demo PerformanceMonitoringAndManagement.ps1* hello içinde *PowerShell ISE*. Bu öğretici sırasında birkaç senaryo çalıştıracağından bu betiği açık tutun.
1. **$DemoScenario** = **1**, **Kiracı grubu sağlama** değerini ayarlayın
1. Tuşuna **F5** toorun hello komut dosyası.

Merhaba betik 17 kiracılar beş dakikadan daha kısa bir süre içinde dağıtır.

Merhaba *yeni TenantBatch* komut dosyası kullanan bir iç içe ya da bağlantılı dizi [Resource Manager](../azure-resource-manager/index.md) hello veritabanını kopyalar, varsayılan kiracılar, toplu oluşturmak şablonlar **basetenantdb** hello katalog sunucusu toocreate hello yeni Kiracı veritabanlarını, ardından bu hello kataloğunda kaydeder ve son olarak bunları hello Kiracı adı ve salonundan türü ile başlatır. Bu, yeni bir kiracı hello uygulama hazırlar hello işlemleriyle tutarlıdır. Çok yapılan değişiklikler*basetenantdb* uygulanan tooany yeni kiracılar bundan sonra sağlanmış olan. Merhaba bkz [şema yönetimi öğretici](sql-database-saas-tutorial-schema-management.md) toomake şema nasıl değiştiğini çok toosee*varolan* Kiracı veritabanları (Merhaba dahil olmak üzere *basetenantdb* veritabanı).

## <a name="simulate-usage-on-all-tenant-databases"></a>Tüm kiracı veritabanlarındaki kullanımın benzetimini gerçekleştirme

Merhaba *Demo PerformanceMonitoringAndManagement.ps1* tüm Kiracı veritabanları karşı çalışan bir iş yükünü benzetim sağlanan komut dosyasıdır. Merhaba yük hello kullanılabilir yük senaryolardan biri, kullanılarak oluşturulur:

| Tanıtım | Senaryo |
|:--|:--|
| 2 | Normal yoğunlukta yük (yaklaşık 40 DTU) oluşturma |
| 3 | Veritabanı başına daha uzun ve daha sık artışla yük oluşturma|
| 4 | Veritabanı başına daha yüksek DTU veri bloğu (yaklaşık 80 DTU) ile yük oluşturma|
| 5 | Tek bir kiracı üzerinde normal yük ve yoğun yük oluşturma (yaklaşık 95 DTU)|
| 6 | Birden çok havuzda dengesiz yük oluşturma|

Merhaba yük Oluşturucu geçerlidir bir *yapay* yalnızca CPU yükü tooevery Kiracı veritabanı. Merhaba Oluşturucu hello yük oluşturan bir saklı yordam düzenli aralıklarla çağrıları her Kiracı veritabanı için bir iş başlatılır. Merhaba yük düzeyleri (Edtu'lar), süre ve aralıklarını öngörülemeyen Kiracı etkinlik benzetimi tüm veritabanları arasında farklılık gösterir.

1. Aç... \\Öğrenme modülleri\\performans izleme ve Yönetim\\*Demo PerformanceMonitoringAndManagement.ps1* hello içinde *PowerShell ISE*. Bu öğretici sırasında birkaç senaryo çalıştıracağından bu betiği açık tutun.
1. Ayarlama **$DemoScenario** = **2**, *Generate normal yoğunluğu yük*.
1. Tuşuna **F5** tooapply yük tooall Kiracı veritabanlarınızda.

Wingtip bir SaaS uygulaması ve bir SaaS uygulaması hello gerçek yükünü genellikle durumlarıyla ve tahmin edilemez. toosimulate bu rastgele yük dağıtılmış tüm kiracılar arasında hello yük üreteci oluşturur. Birkaç dakika hello yük düzeni tooemerge, böylece bölümleri aşağıdaki hello toomonitor hello yük denemeden önce 3-5 dakika hello yük oluşturucuyu çalıştırmak için gereklidir.

> [!IMPORTANT]
> Merhaba yük Oluşturucu yerel PowerShell oturumunuzda işleri bir dizi olarak çalışıyor. Merhaba tutmak *Demo PerformanceMonitoringAndManagement.ps1* sekmesi açık! Merhaba sekmesini kapatın veya makinenizi askıya alma, hello yük Oluşturucu durdurur. Merhaba yük Oluşturucu kaldığı bir *iş çağırma* ürettiği burada hello Oluşturucu başlatıldıktan sonra sağlanan yeni kiracılar yük durumu. Kullanım *Ctrl-C* toostop yeni işler ve çıkış hello betik çağırma. Merhaba yük Oluşturucu toorun, ancak yalnızca var olan kiracılar devam eder.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Hello Azure portal kullanarak kaynak kullanımını izleme

Merhaba sonuçlarından uygulanmakta, yük toomonitor hello kaynak kullanımı hello Kiracı veritabanları içeren hello portal toohello havuzu açın:

1. Açık hello [Azure portal](https://portal.azure.com) ve toohello Gözat *tenants1 -&lt;kullanıcı&gt;*  sunucu.
1. Aşağı kaydırıp elastik havuzları bulun ve **Pool1**’e tıklayın. Bu havuz şu ana kadar oluşturulan tüm hello Kiracı veritabanlarını içerir.

Merhaba gözlemlemek **esnek Havuz izleme** ve **esnek veritabanı izleme** grafik.

Merhaba havuzunun kaynak kullanımı hello toplama veritabanı kullanımı hello havuzdaki tüm veritabanları için ' dir. Merhaba veritabanı grafik hello beş yeni veritabanları gösterir:

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Merhaba havuzunda ek veritabanları olduğundan üst beş Merhaba, hello havuzu kullanımı hello üst beş veritabanları grafikte yansıtılmaz etkinliğini gösterir. Ek ayrıntılar için tıklatın **veritabanı kaynak kullanımını**:

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Merhaba havuzunda performans uyarıları ayarlayın

Bir uyarı üzerinde tetikler hello havuzu Ayarla \>şekilde % 75 kullanımı:

1. Açık *Pool1* (Merhaba üzerinde *tenants1 -\<kullanıcı\>*  sunucu) hello içinde [Azure portal](https://portal.azure.com).
1. **Uyarı Kuralları**ve ardından **+ Uyarı ekle**’ye tıklayın:

   ![uyarı ekle](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. **Yüksek DTU** gibi bir ad belirtin,
1. Hello aşağıdaki değerleri ayarlayın:
   * **Ölçüm = eDTU yüzdesi**
   * **Koşul = büyüktür**.
   * **Eşik = 75**.
   * **Son 30 dakika hello dönem =**.
1. Bir e-posta adresi toohello ekleme *ek yönetici email(s)* kutusuna ve tıklatın **Tamam**.

   ![uyarı ayarlama](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Meşgul bir havuzun ölçeğini artırma

Merhaba toplama yük düzeyi hello havuzu maxes ve % 100 eDTU kullanımı ulaştığında bir havuzu toohello noktasında artarsa, potansiyel olarak yavaşlamasını sorgusu yanıt sürelerini hello havuzdaki tüm veritabanları için tek tek veritabanı performansı etkilenir.

**Kısa vadeli**, hello havuzu tooprovide ek kaynakları ölçekleme veya veritabanlarını hello havuzundan kaldırılıyor göz önünde bulundurun (tooother havuzları taşıma veya hello havuzu tooa tek başına hizmet katmanı dışında).

**Uzun vadeli**, sorguları en iyi duruma getirme göz önünde bulundurun veya dizin kullanım tooimprove veritabanı performansı. % 100 eDTU kullanımı erişmeden önce hello bağlı olarak, en iyi yöntem tooscale uygulamanın duyarlılık tooperformance havuzu oluşturmak verir. Bir uyarı toowarn kullanın, önceden.

Merhaba Oluşturucu tarafından üretilen artan hello yük tarafından meşgul havuzu benzetimini yapabilirsiniz. Merhaba veritabanları tooburst daha sık ve uzun, artan hello toplama yük hello havuzunda hello gereksinimleri veritabanlarını tek tek hello değiştirmeden neden oluyor. Merhaba kuyruğunu ölçeklendirme hello portal veya PowerShell kolayca yapılır. Bu alıştırmada hello portal kullanır.

1. Ayarlama *$DemoScenario* = **3**, _Generate yük uzun ve daha sık WINS'e veritabanı başına ile_ tooincrease hello hello toplama yükünü yoğunluğunu Her veritabanı tarafından istenen hello yoğun yük değiştirmeden hello havuzu.
1. Tuşuna **F5** tooapply yük tooall Kiracı veritabanlarınızda.

1. Çok Git**Pool1** hello Azure Portalı'nda.

İzleyici hello havuz eDTU kullanımı hello üst grafik artar. Merhaba yeni yüksek yük tookick, birkaç dakika sürer ancak toohit max kullanımı Başlat hello havuzu hızlı bir şekilde görmeniz gerekir ve hello yeni modele hello yük steadies gibi hızlı bir şekilde hello havuzu overloads.

1. Merhaba havuzu yukarı tooscale tıklatın **havuzu yapılandırma** hello hello üstündeki **Pool1** sayfası.
1. Merhaba ayarlamak **havuz eDTU** çok ayarı**100**. Merhaba havuz eDTU değiştirme (olan hala veritabanı başına maksimum 50 eDTU) hello veritabanı başına ayarlarını değiştirmez. Merhaba sağ tarafında hello hello veritabanı başına ayarlarını görebilir **havuzu yapılandırma** sayfası.
1. Tıklatın **kaydetmek** toosubmit hello isteği tooscale hello havuzu.

Çok dön**Pool1** > **genel bakış** izleme grafikleri tooview hello. (Süre için çalıştırana kadar birkaç veritabanları ve rastgele bir yük, her zaman kolay toosee conclusively olmasa da) ile daha fazla kaynak hello havuzu sağlama hello etkisini izleyin. Hello grafikleri ayı göz önünde % 100 hello üst bakarken artık grafik 100 Edtu'lar temsil eder, hello üzerinde daha düşük grafik % 100 hala 50 Edtu'lar hello olarak en fazla veritabanı başına olsa da yine 50 Edtu'lar.

Veritabanları çevrimiçi ve tam olarak hello işlemi boyunca kullanılabilir olmaya devam eder. Her veritabanı hazır toobe hello yeni havuz eDTU ile etkin olarak hello en son şu anda tüm etkin bağlantılar kesilir. Uygulama kodu bırakılan tooretry bağlantıları, her zaman yazılması ve hello ölçeği artırılmış havuzunda toohello veritabanı yeniden bağlanır.

## <a name="load-balance-between-pools"></a>Havuzları arasında Yük Dengelemesi

Bir alternatif tooscaling hello havuzu yukarı ikinci bir havuzu oluşturun ve içine veritabanlarını taşımak gibi toobalance hello iki havuzları arasında hello yükleyin. Merhaba hello aynı sunucuya ilk toodo bu hello yeni havuz üzerinde oluşturulması gerekir.

1. Merhaba, [Azure portal](https://portal.azure.com)açın hello **tenants1 -&lt;kullanıcı&gt;**  sunucu.
1. Tıklatın **+ yeni havuz** toocreate hello geçerli sunucudaki bir havuzu.
1. Merhaba üzerinde **esnek veritabanı havuzu** şablonu:

    1. Ayarlama **adı** çok*Pool2*.
    1. Fiyatlandırma katmanı olarak hello bırakın **standart havuz**.
    1. **Havuzu yapılandır**'a tıklayın,
    1. Ayarlama **havuz eDTU** çok*50 eDTU*.
    1. Tıklatın **eklemek veritabanları** toosee çok eklenebilir hello sunucuda veritabanlarının listesini*Pool2*.
    1. Tüm 10 veritabanları toomove bu toohello yeni havuzu seçin ve ardından **seçin**. Merhaba yük Oluşturucu çalışır durumda, hello hizmeti performans profilinizi hello varsayılan 50 eDTU boyutundan daha büyük bir havuzu gerektirir ve bir 100 eDTU ayarı ile başlayan önerir zaten bilir.

    ![Öneri](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. Bu öğretici için hello varsayılan 50 Edtu bırakın ve tıklatın **seçin** yeniden.
    1. Seçin **Tamam** toocreate hello yeni havuz ve toomove hello seçili veritabanları içine.

Merhaba havuzu oluşturma ve hello veritabanlarını taşıma birkaç dakika sürer. Veritabanları, hello kadar çok son şu anda çevrimiçi ve tam olarak erişilebilir kalırlar taşınırken, bu noktada açık olan bağlantıları kapanır. Bazı yeniden deneme mantığı sahip olduğu sürece, istemciler daha sonra hello yeni havuz toohello veritabanına bağlanır.

Çok Gözat**Pool2** (Merhaba üzerinde *tenants1* sunucu) tooopen hello havuzu ve kendi performansını izleyebilir. Göremiyorsanız, hello yeni havuz toocomplete sağlama için bekleyin.

Artık kaynak kullanımının gördüğünüz *Pool1* bıraktı ve *Pool2* şimdi benzer şekilde yüklenir.

## <a name="manage-performance-of-a-single-database"></a>Tek bir veritabanının performansını yönetme

Bir havuzdaki tek veritabanı hello havuzu yapılandırmasına bağlı olarak uzun süreli yüksek yük karşılaşırsa toodominate hello kaynakları hello havuzunda eğilimindedir ve diğer veritabanlarına etkileyebilir. Merhaba etkinlik süre için büyük olasılıkla toocontinue ise, hello veritabanı geçici olarak hello havuzu dışında taşınabilir. Bu hello veritabanı toohave hello gerekir ve diğer veritabanlarına hello yalıtır ek kaynakları sağlar.

Bu alıştırmada, Contoso birlikte bilet satış popüler birlikte için olduğunuzda yüksek yük yaşayan Hall hello etkisini taklit eder.

1. Açık hello... \\ *Demo PerformanceMonitoringAndManagement.ps1* komut dosyası.
1. **$DemoScenario = 5, Tek bir kiracı üzerinde normal yük ve yoğun yük oluşturma (yaklaşık 95 DTU)** ayarını yapın.
1. **$SingleTenantDatabaseName = contosoconcerthall** değerini ayarlayın
1. Merhaba komut dosyasını kullanarak yürütme **F5**.


1. Merhaba, [Azure portal](https://portal.azure.com) açmak **Pool1**.
1. Merhaba incelemek **esnek Havuz izleme** grafik ve artan hello havuz eDTU kullanımı için bakın. Veya iki dakika sonra hello daha yüksek yük içinde tookick başlamanız gerekir ve hızlı bir şekilde hello havuzu kullanımı % 100 isabetler görmeniz gerekir.
1. Merhaba incelemek **esnek veritabanı izleme** hello yeni veritabanları hello son bir saat gösteren görüntü. Merhaba *contosoconcerthall* veritabanı yakında görünmelidir hello beş yeni veritabanları biri olarak.
1. **Merhaba esnek veritabanı izleme'yi tıklatın** **grafik** ve hello açar **veritabanı kaynak kullanımını** burada izleyebilirsiniz hello veritabanları hiçbirini sayfası. Bu hello hello görüntü ayırmanıza olanak tanır *contosoconcerthall* veritabanı.
1. Veritabanları Hello listeden tıklatın **contosoconcerthall**.
1. Tıklatın **fiyatlandırma Katmanı (Ölçek Dtu'lar)** tooopen hello **performansını yapılandırın** hello veritabanı için bir tek başına performans düzeyi ayarlayabileceğiniz sayfa.
1. Tıklatın hello üzerinde **standart** sekmesinde hello standart katmanındaki tooopen hello ölçeklendirme seçeneği.
1. Merhaba slayt **DTU kaydırıcı** tooright tooselect **100** Dtu'lar. Bu toohello hizmet hedefi, karşılık gelen Not **S3**.
1. Tıklatın **Uygula** toomove hello hello havuzu veritabanından ve onu bir *standart S3* veritabanı.
1. Ölçeklendirme sonra tamamlayın, hello contosoconcerthall veritabanı İzleyicisi Merhaba etkisi ve Pool1 hello esnek havuzu ve veritabanı dikey pencereleri üzerinde.

Merhaba yüksek yük hello contosoconcerthall veritabanında subsides sonra kısa süre içinde bu toohello havuzu tooreduce döndürmelidir, maliyeti. Belirsiz ise, ayarladığınız uyarı hello veritabanında, ne zaman olacağını tetiklemek DTU kullanımını hello veritabanı başına düştüğünde hello havuzunda maks. Veritabanını havuza taşıma işlemi 5. alıştırmada açıklanmıştır.

## <a name="other-performance-management-patterns"></a>Diğer Performans Yönetimi Düzenleri

**Önleyici ölçeklendirme** alıştırmada burada incelediniz nasıl tooscale yalıtılmış bir veritabanı, sizin için hangi veritabanı toolook biliyorduk hello yukarıdaki. Contoso birlikte Hall Hello yönetimini hello yaklaşan bilet satış Wingtips haberdar, hello veritabanı dışında hello havuzu pre-emptively taşınmış. Aksi takdirde, bu büyük olasılıkla bir uyarı hello havuzu veya hello veritabanı toospot neler için şunlar gerekir. Bu konuda toolearn hello gelen hello havuzu düşürülmüş performansını şikayetçi içindeki diğer kiracılar istemezsiniz. Ve hello Kiracı ne kadar süreyle hello havuzu bir Azure Otomasyonu runbook toomove hello veritabanından ayarlayın ve ardından içinde tanımlanmış bir zamanlamaya göre yeniden ek kaynaklar gerekir tahmin edebilirsiniz.

**Kiracı Self Servis ölçeklendirme** ölçeklendirme hello yönetim API'si kolayca adında bir görev olduğundan, kolayca hello özelliği Kiracı kullanıma yönelik uygulamanız tooscale Kiracı veritabanı oluşturmak ve SaaS hizmetiniz bir özellik olarak sunar. Örneğin, belki de doğrudan bağlı yukarı ve aşağı Ölçeklendirmesi self-administer kiracılar izin tootheir faturalama!

**Bir havuz üzerinde zamanlama toomatch kullanım desenlerini yukarı ve aşağı ölçeklendirme**

Toplam Kiracı kullanım tahmin edilebilir kullanım desenlerini aşağıdaki durumlarda, bir zamanlamaya göre yukarı ve aşağı olarak Azure Otomasyonu tooscale bir havuz kullanabilirsiniz. Örneğin, kaynak gereksinimlerinde düşüş olduğunu bildiğiniz hafta içi günlerinde havuz ölçeğini akşam 6’dan sonra azaltıp sabah 6’dan önce yeniden artırabilirsiniz.



## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Sağlanan yük Oluşturucu çalıştırarak hello Kiracı veritabanı kullanımı benzetimi
> * Yük toohello artış yanıt olarak İzleyicisi Merhaba Kiracı veritabanları
> * Merhaba yanıt toohello artan veritabanı yük esnek havuzda ölçeklendirme
> * İkinci bir esnek havuz tooload Bakiye hello veritabanı etkinliklerini sağlama

[Tek bir kiracıyı geri yükleme öğreticisi](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Ek kaynaklar

* Ek [hello Wingtip SaaS uygulama dağıtımı sırasında yapı öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [SQL Elastik havuzları](sql-database-elastic-pool.md)
* [Azure otomasyonu](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) - Log Analytics ayarlama ve kullanma öğreticisi
