---
title: "birden çok Azure SQL veritabanı aaaRun analytics sorguları | Microsoft Docs"
description: "Analytics veritabanına çevrimdışı analiz için Kiracı veritabanlarından veri ayıklamak"
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
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>Analytics veritabanına çevrimdışı analiz için Kiracı veritabanlarından veri ayıklamak

Bu öğreticide, her bir kiracı veritabanını bir esnek iş toorun sorguları kullanın. Merhaba iş bilet satış verileri ayıklar ve çözümleme için bir analytics veritabanı (veya veri ambarı) yükler. Merhaba Analizi veritabanı ise tüm kiracılar, bu günlük işletimsel verilerden tooextract Öngörüler sorgulanan.


Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Merhaba Kiracı analytics veritabanı oluşturma
> * Zamanlanmış iş tooretrieve veri oluşturun ve hello analytics veritabanını doldurma

Bu öğretici, Önkoşullar aşağıdaki yapma emin hello karşılanmadığı toocomplete:

* Merhaba Wingtip SaaS uygulaması dağıtılır. beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)
* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* Merhaba SQL Server Management Studio (SSMS) en son sürümü yüklü. [SSMS’yi İndirin ve Yükleyin](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>Kiracı İşlem Analizi düzeni

SaaS uygulamaları ile Merhaba harika fırsatları hello bulutta depolanan toouse hello zengin Kiracı veri biridir. Bu veri toogain fikir hello işlemi ve uygulamanızı ve kiracılarınızın kullanımı için kullanın. Bu veriler özelliği development, kullanılabilirlik yenilikleri ve diğer hello uygulama ve platform yatırım yönlendirebilir. Tek bir çok kiracılı veritabanında olduğunda bu verilere erişmek kolaydır, ancak binlerce veritabanında büyük ölçekli olarak dağıtıldığında çok kolay değildir. Bir yaklaşım tooaccessing Bu, sorgu sonuçlarından sonucu döndürerek bir çıktı veritabanı ve tablo yakalanan iş yürütme toobe etkinleştirmek toouse esnek iş verilerdir.

## <a name="get-hello-wingtip-application-scripts"></a>Merhaba Wingtip uygulama komut dosyaları alma

Merhaba Wingtip SaaS komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. [Adımları toodownload hello Wingtip SaaS betikleri](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="deploy-a-database-for-tenant-analytics-results"></a>Kiracı analiz sonuçları için bir veritabanı dağıtma

Bu öğretici bir veritabanı dağıtılan toocapture hello sonuçları döndüren sorgular içeren komut dosyası iş yürütme sonuçları toohave gerektirir. Bu amaçla tenantanalytics adlı bir veritabanı oluşturalım.

1. Aç... \\Öğrenme modülleri\\işletimsel Analytics\\Kiracı Analytics\\*Demo TenantAnalyticsDB.ps1* hello içinde *PowerShell ISE* ve ayarlayın Aşağıdaki değeri hello:
   * **$DemoScenario** = **2** *İşlem analizi veritabanını dağıtma*
1. Tuşuna **F5** toorun hello tanıtım betiği (Bu çağrıları hello *dağıtma TenantAnalyticsDB.ps1* komut dosyası) hello Kiracı analytics veritabanı oluşturur.

## <a name="create-some-data-for-hello-demo"></a>Merhaba gösteri için bazı veriler oluşturun

1. Aç... \\Öğrenme modülleri\\işletimsel Analytics\\Kiracı Analytics\\*Demo TenantAnalyticsDB.ps1* hello içinde *PowerShell ISE* ve ayarlayın Aşağıdaki değeri hello:
   * **$DemoScenario** = **1** *Tüm mekanlardaki etkinlikler için bilet satın alma*
1. Tuşuna **F5** toorun hello komut dosyası ve geçmiş satın bileti oluşturun.


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>Zamanlanmış iş tooretrieve Kiracı analytics bilet satın alma işlemleri hakkında oluşturma

Bu komut dosyası iş tooretrieve bilet satın alma bilgileri tüm kiracılardan oluşturur. Tek bir tabloya toplanan sonra bilet desenleri hello kiracılar arasında satın alma hakkında zengin ayrıntılı ölçümler elde edebilirsiniz.

1. SSMS açmak ve toohello katalog -&lt;kullanıcı&gt;. database.windows.net sunucu
1. ...\\Öğrenme Modülleri\\İşlem Analizi\\Kiracı Analizleri\\*TicketPurchasesfromAllTenants.sql*’i açın
1. Değiştirme &lt;kullanıcı&gt;, hello kullanıcı adını kullan hello betik hello üstündeki hello Wingtip SaaS uygulama dağıtıldığında kullanılan **sp\_ekleme\_hedef\_grup\_üye** ve **sp\_ekleme\_iş**
1. Sağ tıklayın, seçin **bağlantı**ve toohello katalog - bağlanmak&lt;kullanıcı&gt;. database.windows.net sunucusu zaten bağlıysa,
1. Bağlı toohello olduğundan emin olun **jobaccount** veritabanı ve tuşuna **F5** hello komut dosyasını çalıştırmak için

* **SP\_ekleme\_hedef\_grup** hello hedef grup adı oluşturur *TenantGroup*, tooadd hedef üyeleri ihtiyacımız artık.
* **SP\_ekleme\_hedef\_grup\_üye** ekler bir *server* hedef sunucu (Bu hello customer1 - Not içindeki tüm veritabanları uymak açısından gerekli olduğunu üye türü &lt;Kullanıcı&gt; hello Kiracı veritabanları içeren sunucu) hello işinde işi aynı anda yürütme bulunması gerekir.
* **sp\_add\_job**, “Tüm Kiracıların Bilet Satın Alma İşlemleri” adında yeni bir haftalık olarak zamanlanmış iş oluşturur
* **SP\_ekleme\_iş** hello işi adımı T-SQL komut metni tooretrieve içeren tüm hello bilet satın alma bilgileri tüm kiracılar ve sonuç olarak adlandırılan bir tabloya kümesini döndüren kopyalama hello oluşturur  *AllTicketsPurchasesfromAllTenants*
* Merhaba kalan görünümleri hello komut hello varlığını hello nesneleri ve izleme iş yürütme görüntüler. Gözden hello durum hello değerinden **yaşam döngüsü** sütun toomonitor hello durumu. Bir kez, başarılı, hello işi tüm Kiracı veritabanları başarıyla tamamlandı ve hello hello içeren iki ek veritabanları başvuru tablosu.

Başarılı bir şekilde hello betiğini çalıştırmaya benzer sonuçlarında neden olur:

![sonuçlar](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>Bilet Özet sayısını tüm kiracılardan satın alma işi tooretrieve oluşturma

Bu komut tüm bilet satın alma işi tooretrieve toplamı tüm kiracılardan oluşturur.

1. SSMS açmak ve toohello *katalog -&lt;kullanıcı&gt;. database.windows.net* sunucu
1. Açık hello dosyası... \\Modülleri öğrenme\\sağlamak ve Katalog\\işletimsel Analytics\\Kiracı Analytics\\*sonuçları TicketPurchasesfromAllTenants.sql*
1. Değiştirme &lt;kullanıcı&gt;, hello kullanıcı adını kullan hello kodda hello hello Wingtip SaaS uygulama dağıtıldığında kullanılan **sp\_ekleme\_iş** saklı yordamı
1. Sağ tıklayın, seçin **bağlantı**ve toohello katalog - bağlanmak&lt;kullanıcı&gt;. database.windows.net sunucusu zaten bağlıysa,
1. Bağlı toohello olduğundan emin olun **tenantanalytics** veritabanı ve tuşuna **F5** hello komut dosyasını çalıştırmak için

Başarılı bir şekilde hello betiğini çalıştırmaya benzer sonuçlarında neden olur:

![sonuçlar](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job**, “ResultsTicketsOrders” adında yeni bir haftalık zamanlanmış iş oluşturur

* **SP\_ekleme\_iş** hello işi adımı T-SQL komut metni tooretrieve içeren tüm kiracılar ve CountofTicketOrders adlı bir tabloya ayarlamak sonucu döndürerek kopyalama hello tüm hello bilet satın alma bilgileri oluşturur.

* Merhaba kalan görünümleri hello komut hello varlığını hello nesneleri ve izleme iş yürütme görüntüler. Gözden hello durum hello değerinden **yaşam döngüsü** sütun toomonitor hello durumu. Bir kez, başarılı, hello işi tüm Kiracı veritabanları başarıyla tamamlandı ve hello hello içeren iki ek veritabanları başvuru tablosu.


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunları öğrendiniz:

> [!div class="checklist"]
> * Kiracı analiz veritabanını dağıtma
> * Zamanlanmış iş tooretrieve analitik veri kiracılar arasında oluşturma

Tebrikler!

## <a name="additional-resources"></a>Ek kaynaklar

* Ek [hello Wingtip SaaS uygulamasına yapı öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Esnek İşler](sql-database-elastic-jobs-overview.md)
