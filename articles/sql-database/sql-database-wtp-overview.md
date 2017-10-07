---
title: "aaaIntro Wingtip SaaS - Azure SQL veritabanı çok kiracılı uygulama | Microsoft Docs"
description: "Azure SQL Database, hello Wingtip SaaS uygulama kullanan örnek bir çok kiracılı uygulama kullanarak bilgi edinin"
keywords: "sql veritabanı öğreticisi"
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Giriş toohello Wingtip SaaS uygulaması

Merhaba *Wingtip SaaS* hello benzersiz SQL veritabanı avantajları gösteren örnek bir çok kiracılı uygulama, bir uygulamadır. Merhaba uygulama birden çok Kiracı veritabanı-başına-Kiracı, SaaS uygulama düzeni tooservice kullanır. Merhaba, SaaS senaryoları, birçok SaaS tasarım ve yönetim desenleri de dahil olmak üzere Azure SQL veritabanı'nın tasarlanmış tooshowcase özellikleri uygulamasıdır. tooquickly hale getirmek ve çalışan, hello Wingtip SaaS uygulamayı beş dakikadan daha kısa bir süre içinde dağıtır!

Uygulama kaynak kodu ve yönetim komut dosyaları hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. toorun hello komut dosyaları, [indirme hello öğrenme modülleri klasörü](#download-and-unblock-the-wingtip-saas-scripts) tooyour yerel bilgisayar.

## <a name="sql-database-wingtip-saas-tutorials"></a>SQL veritabanı Wingtip SaaS öğreticileri

Merhaba uygulama dağıttıktan sonra hello ilk dağıtım sırasında yapı öğreticileri aşağıdaki hello keşfedin. SQL veritabanı, SQL veri ambarı ve diğer Azure hizmetleriyle yerleşik özelliklerden yararlanmak ortak SaaS desenler bu öğreticileri keşfedin. Uygulama hello uygulamalarınızda aynı SaaS Yönetimi desenleri ve öğreticiler anlama, büyük ölçüde kolaylaştırma ayrıntılı açıklamalar, PowerShell komut dosyaları içerir.


| Öğretici | Açıklama |
|:--|:--|
|[Dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin](sql-database-saas-tutorial.md)| **BURADAN BAŞLAYIN!** Dağıtma ve hello Wingtip SaaS uygulama tooyour Azure aboneliği keşfedin. |
|[Sağlama ve Katalog kiracılar](sql-database-saas-tutorial-provision-and-catalog.md)| Kiracı tootheir veri hello katalog nasıl eşlendiğini ve hello uygulama Kataloğu veritabanı kullanarak tootenants nasıl bağlandığını öğrenin. |
|[İzleme ve performansı yönetme](sql-database-saas-tutorial-performance-monitoring.md)| Nasıl toouse İzleme özelliklerini öğrenin SQL veritabanı ve nasıl tooset ne zaman uyaracağını performans eşikleri aşıldığında. |
|[Günlük analizi (OMS) ile izleme](sql-database-saas-tutorial-log-analytics.md) | Kullanma hakkında bilgi edinin [günlük analizi](../log-analytics/log-analytics-overview.md) toomonitor büyük miktarlarda birden çok havuz arasında kaynağı. |
|[Tek bir kiracı geri yükleme](sql-database-saas-tutorial-restore-single-tenant.md)| Nasıl toorestore Kiracı veritabanı tooa önceki bir nokta öğrenin. Adımları toorestore tooa paralel veritabanı, bırakma hello varolan Kiracı veritabanı çevrimiçi de dahildir. |
|[Kiracı şema yönetme](sql-database-saas-tutorial-schema-management.md)| Nasıl tooupdate şema ve güncelleştirme tüm Wingtip SaaS kiracılar arasında veri başvuru öğrenin. |
|[Geçici analizler çalıştırır](sql-database-saas-tutorial-adhoc-analytics.md) | Bir geçici analytics veritabanı oluşturun ve tüm kiracılar arasında gerçek zamanlı dağıtılmış sorgular çalıştırın.  |
|[Kiracı analizler çalıştırır](sql-database-saas-tutorial-tenant-analytics.md) | Kiracı veri ambarında çevrimdışı analitik sorguları çalıştırmak için bir analytics veritabanı veya veri ayıklayın. |



## <a name="application-architecture"></a>Uygulama mimarisi

Merhaba Wingtip SaaS uygulama hello Kiracı başına veritabanı modeli kullanır ve SQL esnek havuzu toomaximize verimliliği kullanır. Katalog veritabanına sağlama ve kiracılar tootheir verileri eşleştirmesi için kullanılır. Merhaba çekirdek Wingtip SaaS uygulama havuzu üç örnek kiracılar artı hello Katalog veritabanı ile kullanır. Wingtip SaaS öğreticileri eklentileri toohello ilk dağıtımda neden hello çoğunu Tamamlanıyor, analitik veritabanları sunarak veritabanları arası şema yönetimi, vb..


![Wingtip SaaS mimarisi](media/sql-database-wtp-overview/app-architecture.png)


Toohello veri katmanı ilişkili oldukları gibi hello öğreticileri giderek ve hello uygulamayla çalışma sırasında önemli toofocus hello SaaS modeli sağlanır. Diğer bir deyişle, hello veri katmanını odaklanmanıza ve hello uygulamanın kendi üzerindeki analiz yok. Bu SaaS desenleri Hello uyarlamasını anlama anahtar tooimplementing bu desenleri, uygulamalarınızda belirli iş gereksinimlerinizi için gerekli tüm değişiklikleri ınızın olan.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Karşıdan yükleme ve hello Wingtip SaaS betikleri Engellemeyi Kaldır

ZIP dosyaları bir dış kaynaktan yüklediğiniz ve açtığınız zaman yürütülebilir içeriği (komut dosyaları, DLL'ler) Windows tarafından engellenmiş olabilir. Merhaba komut dosyaları zip dosyasından çıkarılırken ***ayıklanıyor önce toounblock hello .zip dosyası hello adımları izleyin***. Bu, hello betikleri toorun izin verilen sağlar.

1. Çok Gözat[hello Wingtip SaaS github deposuna](https://github.com/Microsoft/WingtipSaaS).
1. Tıklatın **Kopyala veya indir**.
1. Tıklatın **ZIP'i indir** ve hello dosyasını kaydedin.
1. Sağ hello **WingtipSaaS-master.zip** dosyasını bulun ve seçin **özellikleri**.
1. Merhaba üzerinde **genel** sekmesine **Engellemeyi Kaldır**.
1. **Tamam** düğmesine tıklayın.
1. Merhaba dosyaları ayıklayın.

Komut dosyaları hello bulunan *... \\WingtipSaaS ana\\öğrenme modülleri* klasör.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Merhaba Wingtip SaaS PowerShell komut dosyaları ile çalışma

tooget hello en hello örnek dışında toodive sağlanan hello komut dosyalarına gerekir. Merhaba farklı SaaS desenleri nasıl uygulandığını hello ayrıntılarını inceleyerek hello komut dosyalarıyla adım ve kesme noktaları kullanın. sağlanan hello komut dosyaları ve modüller için en iyi anlama, hello kullanmanızı öneririz hello aracılığıyla tooeasily adım [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Dağıtımınız için Hello yapılandırma dosyasını güncelleştir

Merhaba Düzenle **UserConfig.psm1** değeri ile dosyasını dağıtımı sırasında ayarlanan hello kaynak grubu ve kullanıcı:

1. Açık hello *PowerShell ISE* ve yükle... \\Modülleri öğrenme\\*UserConfig.psm1* 
1. Güncelleştirme *ResourceGroupName* ve *adı* (10 ve 11 yalnızca satırlarındaki) dağıtımınız için hello belirli değerleri içeren.
1. Merhaba değişiklikleri kaydedin!

Bu değerleri ayarı burada basitçe, tooupdate bu dağıtım özgü değerleri her komut dosyasında engelleyen.

### <a name="execute-scripts-by-pressing-f5"></a>F5’e basarak Betikleri çalıştırma

Birkaç komut *$PSScriptRoot* toonavigate klasörleri ve *$PSScriptRoot* tuşuna basarak komut yürütüldüğünde yalnızca değerlendirilir **F5**.  Vurgulama ve bir seçim çalıştıran (**F8**) neden hataları, bu nedenle basın **F5** betikleri çalışırken.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Merhaba betikleri tooexamine hello uygulaması aracılığıyla adım

Merhaba en iyi şekilde toounderstand hello betikleri olduğu aralarında adımla toosee ne yaptıklarını. Dahil hello denetleyin **Demo -** kolay toofollow üst düzey iş akışı sunmak komut dosyaları. Merhaba **Demo -** betikleri hello adımları gerekli tooaccomplish her görev Göster kesme noktaları olacak şekilde ayarlamanız ve ayrıntıya daha derin hello tek farklı SaaS desenleri Merhaba toosee uygulama ayrıntılarını çağırır.

Keşfetmek ve PowerShell komut dosyalarıyla Adımlama ipuçları:

* Açık **Demo -** hello PowerShell ISE komut.
* Execute veya devam **F5** (kullanarak **F8** çünkü önerilmez *$PSScriptRoot* seçimleri komut dosyası çalıştırılırken değerlendirilmez).
* Bir çizgiye tıklayarak veya çizgiyi seçerek ve **F9**’a basarak kesme noktaları yerleştirin.
* **F10**’u kullanarak bir işlev veya betiği atlayın.
* **F11**’i kullanarak bir işlev veya betiğe gidin.
* Adım hello geçerli işlevi dışında veya çağrı kullanarak betiği **SHIFT + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Veritabanı şemasını keşfetme ve SSMS kullanarak SQL sorguları yürütme

Kullanım [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect ve göz atma hello uygulama sunucular ve veritabanları.

Merhaba dağıtım başlangıçta sahip iki SQL veritabanı sunucularının tooconnect çok-hello *tenants1 -&lt;kullanıcı&gt;*  sunucusu ve hello *katalog -&lt;kullanıcı&gt;* sunucu. Her iki sunucuyu tooensure başarılı demo bağlantı, sahip bir [güvenlik duvarı kuralı](sql-database-firewall-configure.md) aracılığıyla tüm IP'ler izin verme.


1. Açık *SSMS* ve toohello bağlanmak *tenants1 -&lt;kullanıcı&gt;. database.windows.net* sunucu.
1. **Bağlan** > **Veritabanı Altyapısı...**:

   ![katalog sunucusu seçeneğine tıklayın](media/sql-database-wtp-overview/connect.png)

1. Tanıtım kimlik bilgileri: Kullanıcı adı = *developer*, Parola = *P@ssword1*

   ![bağlantı](media\sql-database-wtp-overview\tenants1-connect.png)

1. 2-3 arasındaki adımları yineleyin ve toohello bağlanmak *katalog -&lt;kullanıcı&gt;. database.windows.net* sunucu.

Başarıyla bağlandıktan sonra her iki sunucuyu da görmeniz gerekir. Veritabanlarının listesini sağlanan hello kiracılar bağlı olarak farklı olabilir:

![nesne gezgini](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Sonraki adımlar

[Merhaba Wingtip SaaS uygulaması dağıtma](sql-database-saas-tutorial.md)
