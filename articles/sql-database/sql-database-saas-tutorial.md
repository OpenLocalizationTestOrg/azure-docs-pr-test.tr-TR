---
title: "aaaDeploy ve Azure SQL veritabanı kullanan Merhaba çok kiracılı Wingtip SaaS uygulaması keşfetme | Microsoft Docs"
description: "Dağıtma ve Azure SQL veritabanı kullanarak SaaS desenleri gösteren hello Wingtip SaaS çok kiracılı uygulama keşfedin."
keywords: "sql veritabanı öğreticisi"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
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
ms.openlocfilehash: 7c528ee19472d3b8c7a285b2f86013945e8f4bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-explore-a-multi-tenant-application-that-uses-azure-sql-database---wingtip-saas"></a>Dağıtma ve Azure SQL veritabanı - Wingtip SaaS kullanan çok kiracılı uygulama keşfedin

Bu öğreticide dağıtın ve Merhaba Wingtip SaaS uygulaması keşfedin. Merhaba uygulaması birden çok Kiracı veritabanı-başına-Kiracı, SaaS uygulama düzeni tooservice kullanır. Merhaba, etkinleştirme SaaS senaryoları basitleştiren tasarlanmış tooshowcase özelliklerini Azure SQL veritabanı uygulamasıdır.

' I tıklattıktan sonra beş dakika hello *tooAzure dağıtmak* düğmeye ise, bir çok kiracılı SaaS uygulamasının SQL Database, en fazla kullanarak ve hello bulutta çalışan sahip. Merhaba uygulaması, her bir SQL esnek havuza tüm dağıtılan kendi veritabanına sahip üç örnek kiracıları ile dağıtılır. Merhaba, dağıtılan tooyour tam erişim tooexplore ve hello tek tek uygulama bileşenleri ile çalışma vermiş Azure aboneliği uygulamasıdır. Merhaba, uygulama kaynak kodu ve yönetim komut dosyaları hello WingtipSaaS GitHub deposuna kullanılabilir.


Bu öğreticide şunları öğrenirsiniz:

> [!div class="checklist"]

> * Nasıl toodeploy hello Wingtip SaaS uygulaması
> * Burada tooget hello uygulama kaynak koduna ve yönetim komut dosyaları
> * Merhaba sunucuları, havuzları ve hello uygulaması veritabanlarını hakkında
> * Nasıl kiracılar hello tootheir verilerle eşlendi *Kataloğu*
> * Nasıl yeni bir kiracı tooprovision
> * Nasıl toomonitor Kiracı hello uygulama etkinlik

tooexplore çeşitli SaaS tasarım ve yönetim desenlerini, bir [ilgili eğitim serileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials) kullanılabilir bu ilk dağıtım sırasında oluşturun. Hello öğreticileri giderek sırasında sağlanan başlangıç komut dosyalarına daha yakından inceleyin ve hello farklı SaaS desenleri nasıl uygulandığını inceleyin. Merhaba komut dosyalarında nasıl tooimplement hello birçok SQL veritabanı özelliklere daha derin bir anlayış basitleştirmek SaaS uygulamaları geliştirme Öğreticisi her toogain adım adım.

## <a name="prerequisites"></a>Ön koşullar

Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:

* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="deploy-hello-wingtip-saas-application"></a>Merhaba Wingtip SaaS uygulaması dağıtma

Merhaba Wingtip SaaS uygulaması dağıtın:

1. Tıklatmak hello **tooAzure dağıtmak** düğme hello Azure portal toohello Wingtip SaaS dağıtım şablonu açar. Merhaba şablonu iki parametre değerlerini gerektirir; Yeni bir kaynak grubu için bir ad ve bu dağıtım hello Wingtip SaaS uygulamasının diğer dağıtımlardan ayıran bir kullanıcı adı. Merhaba sonraki adım, bu değerleri ayarlamak için Ayrıntılar sağlar.

   Daha sonra bunları bir yapılandırma dosyası tooenter gerekeceğinden, kullandığınız emin toonote hello değerleri tam olun.

   <a href="http://aka.ms/deploywtpapp" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

1. Merhaba dağıtımı için gerekli parametre değerleri girin:

    > [!IMPORTANT]
    > Gösterim amaçları doğrultusunda bazı kimlik doğrulama işlemlerinin ve sunucu güvenlik duvarlarının güvenliği kasıtlı olarak kaldırılmıştır. **Yeni bir kaynak grubu oluşturma**ve mevcut kaynak grupları, sunucular veya havuzları kullanmayın. Bu uygulama ya da oluşturur, herhangi bir kaynağa üretim için kullanmayın. Bu kaynağı silme hello uygulama toostop ile işiniz bittiğinde Grup faturalama ilgili.

    * **Kaynak grubu** - seçin **Yeni Oluştur** ve sağlayan bir **adı** hello kaynak grubu için. Seçin bir **konumu** hello aşağı açılan listeden.
    * **Kullanıcı** -bazı kaynaklar genel benzersiz adlar gerektirir. tooensure benzersizlik hello uygulama dağıttığınız her zaman toodifferentiate kaynakları oluşturduğunuz hello Wingtip uygulama herhangi başka bir dağıtım tarafından oluşturulan kaynaklardan bir değer sağlayın. Kısa bir toouse önermiştir **kullanıcı** adınızın baş harflerini artı bir sayı gibi ad (örneğin, *bg1*) ve ardından hello kaynak grubu adı kullanan (örneğin, *wingtip bg1*). **Kullanıcı** parametresi yalnızca harf, rakam ve kısa çizgi (boşluksuz) içerebilir. Merhaba ilk ve son karakter bir harf ya da (tüm küçük önerilir) bir sayı olmalıdır.


1. **Merhaba uygulaması dağıtma**.

    * Tooagree toohello hüküm ve koşullar'ı tıklatın.
    * **Satın al**’a tıklayın.

1. Dağıtım durumunu izlemek tıklayarak **bildirimleri** (Merhaba zil simgesine hello arama kutusunun sağında). Dağıtma hello Wingtip SaaS uygulaması yaklaşık beş dakika sürer.

   ![dağıtım başarılı](media/sql-database-saas-tutorial/succeeded.png)

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Karşıdan yükleme ve hello Wingtip SaaS betikleri Engellemeyi Kaldır

Merhaba uygulama dağıtımı sırasında hello kaynak kodu ve yönetim komut dosyaları indirin.

> [!IMPORTANT]
> ZIP dosyaları bir dış kaynaktan yüklediğiniz ve açtığınız zaman yürütülebilir içeriği (komut dosyaları, DLL'ler) Windows tarafından engellenmiş olabilir. Merhaba komut dosyaları zip dosyasından çıkarılırken, ayıklama önce toounblock hello .zip dosyası hello adımları izleyin. Bu, hello betikleri toorun izin verilen sağlar.

1. Çok Gözat[hello Wingtip SaaS github deposuna](https://github.com/Microsoft/WingtipSaaS).
1. Tıklatın **Kopyala veya indir**.
1. Tıklatın **ZIP'i indir** ve hello dosyasını kaydedin.
1. Sağ hello **WingtipSaaS-master.zip** dosyasını bulun ve seçin **özellikleri**.
1. Merhaba üzerinde **genel** sekmesine **Engellemeyi Kaldır**, tıklatıp **Uygula**.
1. **Tamam** düğmesine tıklayın.
1. Merhaba dosyaları ayıklayın.

Komut dosyaları hello bulunan *... \\WingtipSaaS ana\\öğrenme modülleri* klasör.

## <a name="update-hello-configuration-file-for-this-deployment"></a>Bu dağıtım için Hello yapılandırma dosyasını güncelleştir

Herhangi bir betiği çalıştırmadan önce hello ayarlayın *kaynak grubu* ve *kullanıcı* değerler **UserConfig.psm1**. Bu değişkenler dağıtımı sırasında ayarladığınız toohello değerlerini ayarlayın.

1. Aç... \\Öğrenme modülleri\\*UserConfig.psm1* hello içinde *PowerShell ISE*
1. Güncelleştirme *ResourceGroupName* ve *adı* (10 ve 11 yalnızca satırlarındaki) dağıtımınız için hello belirli değerleri içeren.
1. Merhaba değişiklikleri kaydedin!

Bu ayarı burada basitçe, tooupdate bu dağıtım özgü değerleri her komut dosyasında engelleyen.

## <a name="run-hello-application"></a>Merhaba uygulamayı çalıştırın

birlikte salonları, jazz Sinek Spor olayları barındıran Sinek gibi hello uygulama görebildikleri, gösterir. Görebildikleri müşterinin (veya) için bir kolay bir yolu toolist olayları hello Wingtip platform olarak kaydettirmek ve bilet satabilir. Her salonundan kişiselleştirilmiş web uygulama toomanage alır ve bunların olaylarını listeler ve bağımsız ve diğer kiracıdan yalıtılmış bilet satabilir. Merhaba perde arkasında her Kiracı SQL esnek havuza dağıtılan bir SQL veritabanı alır.

Merkezi bir **olay hub'ı** URL'leri belirli tooyour dağıtım Kiracı listesini sağlar.

1. Açık hello _olay hub'ı_ web tarayıcınızda: http://events.wtp.&lt; Kullanıcı&gt;. trafficmanager.net (dağıtımınızın kullanıcı adıyla değiştirin):

    ![olay hub’ı](media/sql-database-saas-tutorial/events-hub.png)

1. *Olay Hub’ında* **Fabrikam Caz Kulübü**’ne tıklayın.

   ![Olaylar](./media/sql-database-saas-tutorial/fabrikam.png)


gelen istekler, hello uygulama kullandığı toocontrol hello dağıtım [ *Azure Traffic Manager*](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview). Kiracı özgü, hello olayları sayfaları, Kiracı adları hello URL'lerinde içerdiği gerektirir. Tüm Kiracı hello URL'leri özel *kullanıcı* değeri ve bu biçim izleyin: http://events.wtp.&lt; Kullanıcı&gt;.trafficmanager.net/*fabrikamjazzclub*. Merhaba olayları uygulama hello Kiracı adı hello URL'den ayrıştırır ve toocreate Kataloğu'nu kullanarak bir anahtar tooaccess kullanır [ *parça eşleme Yönetim*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-scale-shard-map-management). Katalog eşlemeleri hello anahtar toohello kiracının veritabanı konumu hello. Merhaba **olay hub'ı** her veritabanı tooprovide hello URL'lerin listesi ile ilişkili hello katalog tooretrieve hello kiracının adında genişletilmiş meta verilerini kullanır.

Bir üretim ortamında genellikle bir CNAME DNS kaydı oluşturacak [ *bir şirketin internet etki alanını işaret* ](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-point-internet-domain) hello trafik Yöneticisi profili için.

## <a name="start-generating-load-on-hello-tenant-databases"></a>Merhaba Kiracı veritabanları üzerindeki yükü oluşturma Başlat

Şimdi Hello uygulamanın dağıtıldığı, toowork put! Merhaba *Demo LoadGenerator* PowerShell komut dosyasını tüm Kiracı veritabanları karşı çalışan bir iş yükünü başlatır. birçok SaaS uygulamalarını Hello gerçek Yük genellikle durumlarıyla ve tahmin edilemez. toosimulate yük, hello Oluşturucu bu tür tüm kiracılar, rastgele aralıklarla gerçekleşen her bir kiracı üzerinde rastgele WINS'e ile dağıtılmış bir yük oluşturur. Bu nedenle hello yük düzeni tooemerge birkaç dakika sürer veya dört hello izleme önce dakika yük böylece en iyi toolet hello Oluşturucu için en az üç farklı çalıştır yapılır.

1. Merhaba, *PowerShell ISE*açın hello... \\Öğrenme modülleri\\yardımcı programları\\*Demo LoadGenerator.ps1* komut dosyası.
1. Tuşuna **F5** hello komut dosyasını çalıştırın ve hello yük Oluşturucu (bırakın hello için varsayılan parametre değerleri şimdi) başlatın.

> [!IMPORTANT]
> toorun diğer komut dosyaları, yeni bir PowerShell ISE penceresi açın. Merhaba yük Oluşturucu yerel PowerShell oturumunuzda işleri bir dizi olarak çalışıyor. Merhaba *Demo LoadGenerator.ps1* betik devreye bir ön plan görev artı arka plan yük oluşturma işleri bir dizi olarak çalışan hello gerçek yük Oluşturucu betik kapalı. Bir yük Oluşturucu işi hello kataloğa kayıtlı her veritabanı için çağrılır. tüm işleri durdurur Hello PowerShell oturumu kapatma şekilde hello işleri yerel PowerShell oturumunuzda çalışır. Makinenizi askıya alırsanız yük oluşturma duraklatıldı ve, makineyi uyandırmak devam edecek.

Her bir kiracı için yük oluşturma işleri Hello yük oluşturucuyu çağırır sonra hello ön plan görev, sonradan sağlanan yeni kiracılar için ek arka plan işleri başladığı bir işi çağırma durumda kalır. Kullanabileceğiniz *Ctrl-C* veya tuşuna hello *durdurmak* düğmesini toostop hello ön plan görev, ancak varolan arka plan işleri her veritabanı oluşturma devam edecek. Toomonitor gerekir ve kontrol hello arka plan işlerinin kullanın *Get-Job*, *Receive-Job* ve *işini durdurmayı*. Merhaba ön plan görev, çalışırken kullanım başka betikleri aynı PowerShell oturumu tooexecute hello olamaz. toorun diğer komut dosyaları, yeni bir PowerShell ISE penceresi açın.

Toorestart hello yük Oluşturucu oturumu isterseniz, örneğin farklı parametrelerle hello ön plan görev ve yeniden çalıştırın hello durdurabilirsiniz *Demo LoadGenerator.ps1* komut dosyası. Yeniden çalıştırmayı *Demo LoadGenerator.ps1* ilk herhangi işler ve işleri hello geçerli parametrelerini kullanarak yeni bir dizi devreye yeniden başlatmalar hello Oluşturucu çalışmakta durdurur.

Şimdilik, iş çağırma hello durumda çalışan hello yük Oluşturucu bırakın.


## <a name="provision-a-new-tenant"></a>Yeni bir kiracı sağlama

Merhaba ilk dağıtım üç örnek kiracılar oluşturur, ancak başka bir kiracı toosee oluşturalım nasıl bu dağıtılan hello uygulama etkiler. Merhaba Wingtip SaaS sağlama kiracılar iş akışı hello ayrıntılı [sağlamak ve kataloğu Öğreticisi](sql-database-saas-tutorial-provision-and-catalog.md). Bu adımda, yeni bir kiracı hızla oluşturun.

1. Aç... \\Öğrenme Modules\Provision ve Katalog\\*Demo ProvisionAndCatalog.ps1* hello içinde *PowerShell ISE*.
1. Tuşuna **F5** hello betiğini (Merhaba varsayılan değerler şimdilik bırakın) çalıştırmak için.

   > [!NOTE]
   > Birçok Wingtip SaaS komut *$PSScriptRoot* klasörleri toocall başka betikleri işlevlerde gezinme tooallow. Tuşlarına basarak Hello betik çalıştırıldığında bu değişken yalnızca hesaplanan **F5**.  Vurgulama ve bir seçim çalıştıran (**F8**) neden hataları, bu nedenle basın **F5** betikleri çalışırken.

Merhaba yeni Kiracı veritabanı bir SQL esnek havuzu oluşturulur, başlatılmış ve hello kataloğa kayıtlı. Merhaba yeni Kiracı bilet satış başarılı sağladıktan sonra *olayları* sitesi tarayıcınızda görüntülenir:

![Yeni kiracı](./media/sql-database-saas-tutorial/red-maple-racing.png)

Merhaba yenileme *olay hub'ı* ve hello yeni Kiracı hello listesinde görünür.


## <a name="explore-hello-servers-pools-and-tenant-databases"></a>Merhaba sunucuları, havuzlar, araştırın ve Kiracı veritabanları

Bir yük kiracılar hello koleksiyonunu karşı çalışan başladıktan, dağıtılan hello kaynakların bazıları bakalım:

1. İçinde [Azure portal](http://portal.azure.com)tooyour SQL sunucularının listesini göz atın ve Aç **katalog -&lt;kullanıcı&gt;**  sunucu. Merhaba katalog sunucusu iki veritabanı içerir. Merhaba **tenantcatalog**ve hello **basetenantdb** (boş bir *altın* veya olan şablon veritabanı kopyalanan toocreate yeni kiracılar).

   ![veritabanları](./media/sql-database-saas-tutorial/databases.png)

1. SQL sunucularının listesini tooyour geri gidin ve açmak hello **tenants1 -&lt;kullanıcı&gt;**  hello Kiracı veritabanlarını barındıran sunucu. Her Kiracı veritabanı bir _esnek standart_ 50 eDTU standart havuzdaki veritabanı. Ayrıca fark bir _kırmızı Akçaağaç yarış_ veritabanı, daha önce sağlanan hello Kiracı veritabanı.

   ![sunucu](./media/sql-database-saas-tutorial/server.png)

## <a name="monitor-hello-pool"></a>İzleyici hello havuzu

Merhaba yük Oluşturucu için birkaç dakika çalışır, yeterli veri bazı izleme kapasiteleri havuzları ve veritabanları yerleşik hello bakarak kullanılabilir toostart olmalıdır.

1. Toohello sunucu Gözat **tenants1 -&lt;kullanıcı&gt;**, tıklatıp **Pool1** hello havuz için kaynak kullanımını görüntülemek için (Merhaba yük oluşturucuyu çalışan grafikleri aşağıdaki hello bir saat için) :

   ![havuzu izleme](./media/sql-database-saas-tutorial/monitor-pool.png)

Bu iki grafik, elastik havuzların ve SQL Veritabanı’nın SaaS uygulaması iş yükleri için ne kadar uygun olduğunu gösterir. 50 eDTU havuzu içinde 40 edtu'ları kolayca desteklenen kadar her tooas emniyeti dört veritabanları. Tek başına veritabanı olarak sağlanan varsa, her gerek toobe bir S2 yaptıkları (50 DTU) toosupport hello WINS'e. Merhaba maliyeti 4 tek başına S2 veritabanlarının yaklaşık 3 kez hello fiyat hello havuzunun olur ve hello havuzunun hala yeterli boş alan çok daha fazla veritabanı için vardır. Gerçek dünya durumlarda, SQL veritabanı müşteriler too500 veritabanlarını 200 eDTU havuzlarında şu anda çalışıyor. Daha fazla bilgi için bkz: Merhaba [performans öğretici izleme](sql-database-saas-tutorial-performance-monitoring.md).


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları öğrendiniz:

> [!div class="checklist"]

> * Nasıl toodeploy hello Wingtip SaaS uygulaması
> * Merhaba sunucuları, havuzları ve hello uygulaması veritabanlarını hakkında
> * Kiracılar olan hello eşlenen tootheir verilerle *Kataloğu*
> * Nasıl tooprovision yeni kiracılar
> * Nasıl tooview havuzu kullanımı toomonitor Kiracı etkinliği
> * Toodelete örnek kaynaklar toostop faturalama ilişkisini

Şimdi hello deneyin [sağlamak ve kataloğu Öğreticisi](sql-database-saas-tutorial-provision-and-catalog.md)



## <a name="additional-resources"></a>Ek kaynaklar

* Ek [oluşturmanıza öğreticileri hello Wingtip SaaS uygulaması](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* Esnek havuzları hakkında toolearn bkz [ *bir Azure SQL esnek havuzu nedir*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool)
* toolearn esnek işler hakkında bkz [ *yönetme ölçeklendirilmiş bulut veritabanları*](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-jobs-overview)
* toolearn çok kiracılı SaaS uygulamaları hakkında bkz [ *tasarım desenleri çok kiracılı SaaS uygulamaları için*](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)
