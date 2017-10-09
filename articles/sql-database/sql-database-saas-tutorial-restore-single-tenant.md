---
title: "çok kiracılı uygulama Azure SQL veritabanında aaaRestore | Microsoft Docs"
description: "Nasıl toorestore tek bir SQL Kiracı öğrenin yanlışlıkla veri sildikten sonra veritabanı"
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
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Wingtip SaaS kiracılar SQL veritabanını geri yükle

Merhaba Wingtip SaaS uygulama, her bir kiracı kendi veritabanına sahip olduğu bir kiracı başına veritabanı modeli kullanılarak oluşturulur. Bu modelin hello avantajlarından biri olduğundan, BT'nin kolay toorestore tek bir kiracının başka kiracılar etkileyen olmadan yalıtım verisinde.

Bu öğreticide iki veri kurtarma desenleri öğrenin:

> [!div class="checklist"]

> * Paralel veritabanına (yan yana) bir veritabanını geri yükleyin
> * Yerinde bir veritabanını geri yükle


|||
|:--|:--|
| **Kiracı tooa önceki noktası, zaman içindeki paralel bir veritabanına geri yükleme** | Bu desen hello Kiracı tarafından kullanılan gözden geçirme denetimi, uyumluluk için vb. hello özgün veritabanı çevrimiçi ve değişmeden kalır. |
| **Yerinde Kiracı geri yükleme** | Bu deseni genelde kullanılan toorecover bir kiracı tooa önceki noktası Kiracı yanlışlıkla veri sildikten sonra saattir. Merhaba özgün veritabanını çevrimdışına ve hello geri yüklenen veritabanı ile değiştirilir. |
|||

Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:

* Merhaba Wingtip SaaS uygulaması dağıtılır. beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)
* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>Giriş toohello SaaS Kiracı geri yükleme düzeni

Merhaba Kiracı için desen geri yüklemek için tek bir kiracının verileri geri yüklemek için iki basit modeli vardır. Kiracı veritabanları birbirinden yalıtılmış olduğundan, bir kiracı geri herhangi diğer kiracının veri üzerinde etkisi yoktur.

Merhaba ilk desende verileri yeni bir veritabanına geri yüklenir. Merhaba Kiracı sonra üretim verilerini yanında toothis veritabanına verilir. Bu desen bir kiracı yönetici tooreview geri hello veri sağlar ve potansiyel olarak kullanmak tooselectively üzerine geçerli verileri değerleri. Bu, veri kurtarma seçenekleri olmalıdır toohello SaaS Uygulama Tasarımcısı toodetermine ne kadar karmaşık hello olur. Yalnızca belirli bir anda zamanında durumla hello durum mümkün tooreview verileri olan bazı senaryolarda gerekli olabilir. Merhaba veritabanı kullanıyorsa, [coğrafi çoğaltma](sql-database-geo-replication-overview.md), hello özgün veritabanına geri hello kopyadan gerekli hello veri kopyalama öneririz. Merhaba özgün veritabanına geri hello veritabanıyla değiştirirseniz, tooreconfigure gerekir ve coğrafi çoğaltma yeniden eşitleyin.

Merhaba Kiracı başlayamıyorsa kaybı veya veri bozulması varsayan hello ikinci modelinde hello kiracının üretim veritabanı geri tooa önceki bir noktaya. Merhaba veritabanı geri ve tekrar çevrimiçi durumdayken hello geri yükleme yeri düzeninde, hello Kiracı kısa bir süre için çevrimdışı hale getirilir. Merhaba özgün veritabanı silinir, ancak toogo geri tooan gerekiyorsa hala geri yüklenebileceği daha önceki bir noktaya. Hiçbir ek avantajı veri güvenliği açısından yeniden adlandırma hello veritabanı sunmasına karşın bu deseni çeşitlemesi silmeden yerine hello veritabanı yeniden adlandırabilirsiniz.

## <a name="get-hello-wingtip-application-scripts"></a>Merhaba Wingtip uygulama komut dosyaları alma

Merhaba Wingtip SaaS komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. [Adımları toodownload hello Wingtip SaaS betikleri](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>Yanlışlıkla veri silme Kiracı benzetimi

toodemonstrate bu kurtarma senaryoları çok ihtiyacımız*yanlışlıkla* bazı veriler hello Kiracı veritabanlarından birini silin. Herhangi bir kayıt silebilirsiniz olsa da, hello demo toonot hello sonraki adım ayarlar başvuru bütünlüğü ihlali tarafından engellenen! Ayrıca daha sonra hello kullanabileceğiniz bazı bilet satın alma verileri ekler *Wingtip SaaS Analytics öğreticileri*.

Merhaba bilet üreteci komut dosyasını çalıştırın ve ek veri oluşturun. Merhaba bilet Oluşturucu her kiracılar son olay biletlerini kasıtlı olarak satın değil.

1. Aç... \\Öğrenme modülleri\\yardımcı programları\\*Demo TicketGenerator.ps1* hello içinde *PowerShell ISE*
1. Tuşuna **F5** toorun hello betik müşteriler üretmek ve bilet satış verileri.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Açık hello olayları uygulama tooreview hello geçerli olaylar

1. Açık hello *olay hub'ı* (http://events.wtp.&lt; Kullanıcı&gt;. trafficmanager.net) tıklatıp **Contoso birlikte Hall**:

   ![olay hub’ı](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Merhaba olayların listesini kaydırın ve hello listesinde hello son olay not edin:

   ![Son olay](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Merhaba demo senaryo tooaccidentally delete hello son olay çalıştırın

1. Aç... \\Öğrenme modülleri\\iş sürekliliği ve olağanüstü durum kurtarma\\RestoreTenant\\*Demo RestoreTenant.ps1* hello içinde *PowerShell ISE*, kümesi hello izleyerek değeri:
   * **$DemoScenario** = **1**çok ayarlayın**1** -Sil bilet satış olmayan olaylar.
1. Tuşuna **F5** toorun hello komut dosyası ve hello son olay silin. Bir onay iletisi benzer toohello aşağıdaki görmeniz gerekir:

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. Merhaba Contoso olayları sayfası açılır. Aşağı kaydırın ve hello olay kayboluyor doğrulayın. Merhaba Olay hala hello listesinde ise Yenile'yi tıklatın ve kayboldu olduğunu doğrulayın.

   ![Son olay](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Bir kiracı veritabanı hello üretim veritabanı ile paralel geri yükleme

Bu alıştırmada hello Contoso birlikte Hall veritabanı tooa noktası hello olay silinmiş önce geçen süre içinde geri yükler. Merhaba olay hello önceki adımlarda silindikten sonra toorecover istediğiniz ve Silinen hello veri bakın. Silinen hello kaydıyla üretim veritabanınız toorestore gerekli değildir, ancak diğer iş nedenleri toorecover hello eski veritabanı tooaccess hello eski verileri gerekir.

 Merhaba *geri yükleme TenantInParallel.ps1* betik, veritabanı ve adlı paralel katalog girişini hem paralel bir kiracı oluşturur *ContosoConcertHall\_eski*. Bu tür bir geri yükleme veya uyumluluk ve kurtarma senaryolarına denetim ikincil veri kaybına karşı kurtarmak için uygundur. Aynı zamanda, kullanırken önerilen yaklaşımı hello olan [coğrafi çoğaltma](sql-database-geo-replication-overview.md).

1. Tam hello [yanlışlıkla veri silme kullanıcı benzetimini](#simulate-a-tenant-accidentally-deleting-data) bölümü.
1. Aç... \\Öğrenme modülleri\\iş sürekliliği ve olağanüstü durum kurtarma\\RestoreTenant\\_Demo RestoreTenant.ps1_ hello içinde *PowerShell ISE*.
1. Ayarlama **$DemoScenario** = **2**, bu çok ayarlamak**2** çok*paralel geri yükleme Kiracı*.
1. Tuşuna **F5** toorun hello komut dosyası.

Merhaba betik hello Kiracı veritabanı (tooa paralel veritabanı) tooa noktası hello önceki bölümdeki hello olay silmeden önce zaman içinde geri yükler. İkinci bir veritabanı oluşturur, bu veritabanında var ve hello veritabanı toohello katalog hello altında ekler varolan katalog meta verileri kaldırır *ContosoConcertHall\_eski* girişi.

Merhaba tanıtım betiği tarayıcınızda hello olayları sayfası açılır. Merhaba URL'den Not: ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` bu geri hello veritabanındaki verileri gösteren nerede *_old* toohello adı eklenir.

Merhaba önceki bölümde silinmiş olay hello hello tarayıcı tooconfirm içinde listelenen kaydırma hello olayları geri yüklendi.

Bir ek Kiracı kendi olayları uygulama toobrowse biletleri ile Kiracı erişim toorestored veri ancak görevi görür tooeasily hello geri yükleme düzeni göstermek nasıl sağlamak olası toobe olduğu gibi sunan geri hello Kiracı unutmayın.

Gerçekte, büyük olasılıkla yaptığınız tanımlanan bir süre için yalnızca bu geri yüklenen veritabanı korur. Arama hello tarafından sona erdikten sonra geri hello Kiracı girişi silebilirsiniz *Kaldır RestoredTenant.ps1* komut dosyası.

1. Ayarlama **$DemoScenario** çok**4** tooselect hello *geri Kaldır Kiracı* senaryo.
1. **Yürütme** **kullanarak** **F5**
1. Merhaba *ContosoConcertHall\_eski* girişi hello Kataloğu'ndan artık silinir. Bir tane tarayıcınızda bu Kiracı için hello olayları sayfasını kapatın.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>Merhaba varolan Kiracı veritabanı değiştirme Kiracı varken, geri yükleme

Bu alıştırmada hello Contoso birlikte Hall Kiracı tooa noktası hello olay silinmiş önce geçen süre içinde geri yükler. Merhaba *geri yükleme TenantInPlace* komut dosyası tooa önceki noktası zamanında işaret eden hello geçerli Kiracı veritabanı tooa yeni veritabanını geri yükler ve siler hello özgün veritabanı. Kiracı hello önemli veri kaybı olabileceğinden ciddi veri bozulmasını kurtarmak tooaccommodate olurdu için bu deseni geri yükleme daha uygundur.

1. Açık **Demo RestoreTenant.ps1** PowerShell ISE dosyasında
1. Ayarlama **$DemoScenario** çok**5** tooselect hello *yer senaryoda Kiracı geri*.
1. Kullanılarak yürütülmesi **F5**.

Merhaba betik hello Kiracı veritabanı tooa noktası beş dakika hello olay silinmiş önce geri yükler. İlk bunu yapar hello Contoso birlikte Hall alma çevrimdışı vardır; bu nedenle daha fazla Kiracı toohello verileri güncelleştirir. Ardından, paralel bir veritabanı hello geri yükleme noktasından geri yükleyerek oluşturulur ve adlı bir zaman damgası ile tooensure hello veritabanı adı hello varolan Kiracı veritabanı adı ile çakışmaması. Ardından, hello eski Kiracı veritabanı silinir ve hello geri yüklenen veritabanı yeniden adlandırılmış toohello özgün veritabanı adıdır. Son olarak, Contoso birlikte Hall çevrimiçi tooallow hello uygulama erişim geri toohello veritabanı duruma getirilir.

Merhaba olay silinmeden önce zamanında hello veritabanı tooa noktası başarıyla geri. Olayları sayfası açılır Merhaba, bu nedenle onaylayın hello son olay geri yüklendi.


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]

> * Paralel veritabanına (yan yana) bir veritabanını geri yükleyin
> * Yerinde bir veritabanını geri yükle

[Kiracı veritabanı şeması yönetme](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>Ek kaynaklar

* Ek [hello Wingtip SaaS uygulamasına yapı öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure SQL Database iş sürekliliğine genel bakış](sql-database-business-continuity.md)
* [SQL veritabanı yedeklemeleri hakkında bilgi edinin](sql-database-automated-backups.md)
