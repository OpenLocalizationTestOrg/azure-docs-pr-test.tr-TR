---
title: "çok kiracılı uygulama aaaManage Azure SQL veritabanı şemasında | Microsoft Docs"
description: "Azure SQL Veritabanı’nı kullanan çok kiracılı bir uygulamada birden fazla kiracı için Şemayı yönetme"
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
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>Merhaba Wingtip SaaS uygulama içinde birden çok Kiracı için şema yönetme

Merhaba [ilk Wingtip SaaS öğretici](sql-database-saas-tutorial.md) nasıl hello uygulama bir kiracı veritabanı sağlamak ve hello kataloğunda kaydetmek gösterir. Herhangi bir uygulama gibi Wingtip SaaS uygulama zamanla ve bazen gelişmesi hello değişiklikleri toohello veritabanı gerektirir. Değişiklikler, yeni veya değiştirilmiş şema, yeni veya değiştirilmiş başvuru verileri ve rutin veritabanı bakım görevleri tooensure en iyi uygulama performansını içerebilir. Bir SaaS uygulaması ile bu değişikliklerin Kiracı veritabanları arasında bir olası yoğun Donanma koordineli bir şekilde dağıtılan toobe gerekir. Bu değişiklikleri toobe için gelecekte veritabanlarını Kiracı, sağlama işlemi hello dahil toobe gerekir.

Bu öğretici iki senaryo - tüm kiracılar için başvuru veri güncelleştirmelerini dağıtma inceler ve hello dizin retuning hello başvuru verileri içeren tablo. Merhaba [esnek iş](sql-database-elastic-jobs-overview.md) özelliği kullanılan tooexecute bu işlemleri tüm kiracılar, hello arasında ise *altın* yeni veritabanları için şablon olarak kullanılan Kiracı veritabanı.

Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]

> * Bir iş hesabı oluşturun
> * Birden çok Kiracı arasında sorgu
> * Tüm kiracı veritabanlarında verileri güncelleştirme
> * Tüm kiracı veritabanlarında bir tabloda dizin oluşturma


Bu öğretici, Önkoşullar aşağıdaki yapma emin hello karşılanmadığı toocomplete:

* Merhaba Wingtip SaaS uygulaması dağıtılır. beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)
* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* Merhaba SQL Server Management Studio (SSMS) en son sürümü yüklü. [SSMS’yi İndirin ve Yükleyin](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*Bu öğretici bir sınırlı (esnek veritabanı iş) önizlemede hello SQL veritabanı hizmetinin özelliklerini kullanır. Bu öğretici toodo isterseniz, abonelik kimliğinizi sağlamak tooSaaSFeedback@microsoft.com esnek işleri Önizleme konuyla =. Aboneliğinizi etkinleştirildiğini onay aldıktan sonra [hello en son sürüm öncesi işleri cmdlet'leri yükleyip](https://github.com/jaredmoo/azure-powershell/releases). Bu önizleme sınırlıdır, bu nedenle başvurun SaaSFeedback@microsoft.com ile ilgili sorular veya destek.*


## <a name="introduction-toosaas-schema-management-patterns"></a>Giriş tooSaaS şema yönetimi desenleri

Hello veritabanı başına tek bir kiracı SaaS sonuçları hello veri yalıtımı gelen birçok yolla avantajları desen, ancak hello aynı anda Bakımı ve yönetiminin birçok veritabanı yönetme hello karmaşıklık tanıtır. [Esnek iş](sql-database-elastic-jobs-overview.md) hello SQL veri katmanı yönetim kolaylaştırır. İşlerini toosecurely etkinleştirin ve güvenilir bir şekilde, görevler (T-SQL komut dosyaları) kullanıcı etkileşimi ve girişinden, bağımsız veritabanları grubu karşı çalıştırın. Bu yöntem, uygulamadaki tüm kiracılar arasında kullanılan toodeploy şema ve ortak başvuru veri değişikliklerini olabilir. Esnek iş kullanılan toomaintain de olabilir bir *altın* hello veritabanının kopyasını hello en son şema ve başvuru verileri her zaman sahip olduktan toocreate yeni kiracılar kullanılır.

![ekran](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>Esnek İşler sınırlı önizlemesi

Esnek İşler’in artık Azure SQL Veritabanı’nın (ek hizmet veya bileşen gerektirmeyen) tümleşik bir özelliği olan yeni bir sürümü vardır. Esnek İşler’in bu yeni sürümü, şu anda sınırlı önizlemeyle sunulmaktadır. Bu sınırlı Önizleme şu anda PowerShell toocreate iş hesapları ve T-SQL toocreate destekler ve işleri yönetir.

> [!NOTE]
> *Bu öğretici bir sınırlı (esnek veritabanı iş) önizlemede hello SQL veritabanı hizmetinin özelliklerini kullanır. Bu öğretici toodo isterseniz, abonelik kimliğinizi sağlamak tooSaaSFeedback@microsoft.com esnek işleri Önizleme konuyla =. Aboneliğinizi etkinleştirildiğini onay aldıktan sonra [hello en son sürüm öncesi işleri cmdlet'leri yükleyip](https://github.com/jaredmoo/azure-powershell/releases). Bu önizleme sınırlıdır, bu nedenle başvurun SaaSFeedback@microsoft.com ile ilgili sorular veya destek.*

## <a name="get-hello-wingtip-application-scripts"></a>Merhaba Wingtip uygulama komut dosyaları alma

Merhaba Wingtip SaaS komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. [Adımları toodownload hello Wingtip SaaS betikleri](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-a-job-account-database-and-new-job-account"></a>İş hesabı veritabanı ve yeni bir iş hesabı oluşturma

Bu öğreticide PowerShell toocreate hello iş veritabanı ve iş hesabı kullanmak gerektirir. MSDB ve SQL aracısı gibi esnek işler bir Azure SQL toostore iş tanımları, iş durumunu ve geçmişini veritabanı kullanır. Merhaba iş hesabı oluşturulduktan sonra oluşturma ve işleri hemen izleyin.

1. Aç... \\Öğrenme modülleri\\Şema Yönetimi\\*Demo SchemaManagement.ps1* hello içinde **PowerShell ISE**.
1. Tuşuna **F5** toorun hello komut dosyası.

Merhaba *Demo SchemaManagement.ps1* betik çağrıları hello *dağıtma SchemaManagement.ps1* toocreate komut dosyası bir *S2* adlı veritabanı **jobaccount** hello katalog sunucusunda. Daha sonra bir parametre toohello iş hesabı oluşturma çağrı hello jobaccount veritabanı geçirme hello iş hesabı oluşturur.

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>Bir işi toodeploy yeni başvuru veri tooall kiracılar oluşturma

Her Kiracı veritabanı salonundan barındırılan olayları hello türünü tanımlayın salonundan türleri kümesi içerir. Bu alıştırmada, bir güncelleştirme tooall hello Kiracı veritabanları tooadd iki ek salonundan türlerini dağıtmanıza: *Motosikletinizin yarış* ve *yüzme kulübü*. Bu salonundan türleri hello Kiracı olayları uygulamasında gördüğünüz toohello arka plan görüntüsü karşılık gelir.

Merhaba Salonundan türü açılır menüsünü tıklatın ve yalnızca 10 salonundan türü seçenekleri kullanılabilir ve özellikle, 'Motosikletinizin yarış' ve 'Yüzme kulübü' hello listesinde bulunmayan doğrulayın.

Şimdi bir iş tooupdate hello oluşturalım *VenueTypes* tablo tüm hello Kiracı veritabanları ve hello yeni salonundan türlerini ekleyin.

Yeni bir iş toocreate kullanırız işleri bir dizi sistem saklı yordamlar hello iş hesabı oluşturduğunuzda hello jobaccount veritabanında oluşturulmuş.

1. SSMS açın ve toohello katalog sunucusuna bağlanma: Katalog -\<kullanıcı\>. database.windows.net sunucu
1. Ayrıca toohello Kiracı sunucuya: tenants1 -\<kullanıcı\>. database.windows.net
1. Toohello Gözat *contosoconcerthall* hello veritabanında *tenants1* sunucusunda ve sorgu hello *VenueTypes* tablo tooconfirm, *Motosikletinizin yarış*  ve *yüzme kulübü* **değil** hello sonuçları listesinde.
1. Açık hello dosyası... \\Modülleri öğrenme\\Şema Yönetimi\\DeployReferenceData.sql
1. Merhaba deyimi değiştirin: AYARLAMAK @wtpUser = &lt;kullanıcı&gt; ve hello Wingtip uygulama dağıtıldığında kullanılan hello kullanıcı değerini değiştirin
1. Bağlı toohello jobaccount veritabanı ve tuşuna olduğundan emin olun **F5** hello komut dosyasını çalıştırmak için

* **SP\_ekleme\_hedef\_grup** tooadd hedef üyeleri ihtiyacımız artık hello hedef grup adı DemoServerGroup, oluşturur.
* **SP\_ekleme\_hedef\_grup\_üye** ekler bir *server* hedef sunucu (Bu hello tenants1-Notiçindekitümveritabanlarıuymakaçısındangerekliolduğunuüyetürü&lt; Kullanıcı&gt; hello Kiracı veritabanları içeren sunucu) işi aynı anda yürütme hello işinde hello ikinci ekleme eklenmesi gereken bir *veritabanı* hedef üye türü, 'Altın' veritabanına ('özellikle hello basetenantdb) bulunan katalog - üzerinde&lt;kullanıcı&gt; sunucusu ve son olarak başka bir *veritabanı* bir sonraki öğreticide kullanılan hedef grubu üye türü tooinclude hello adhocanalytics veritabanı.
* **sp\_add\_job**, “Başvuru Verileri Dağıtımı” adında bir iş oluşturur
* **SP\_ekleme\_iş** T-SQL komut metni tooupdate hello başvuru tablosu, VenueTypes içeren hello işi adımı oluşturur
* Merhaba kalan görünümleri hello komut hello varlığını hello nesneleri ve izleme iş yürütme görüntüler. Bu sorguları tooreview hello durum değeri hello kullan **yaşam döngüsü** hello işi başarıyla tüm Kiracı veritabanları ve hello iki ek veritabanları hello başvuru tablosu içeren tamamlandığında sütun toodetermine.

1. SSMS, toohello Gözat *contosoconcerthall* hello veritabanında *tenants1* sunucusunda ve sorgu hello *VenueTypes* tablo tooconfirm, *Motosikletinizin Yarış* ve *yüzme kulübü* **olan** hello sonuçları listesinde şimdi.


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>Bir iş toomanage hello başvuru tablosu dizini oluşturma

Benzer toohello önceki alıştırmada, bu alıştırmada bir iş toorebuild hello dizin hello başvuru tablosunda birincil anahtar oluşturur, tipik veritabanı yönetim işlemi yönetici büyük veri yükleme sonrası bir tabloya gerçekleştirebilir.

Aynı işleri 'system' Hello kullanarak işi oluşturmak saklı yordamlar.

1. SSMS açmak ve toohello katalog -&lt;kullanıcı&gt;. database.windows.net sunucu
1. Açık hello dosyası... \\Modülleri öğrenme\\Şema Yönetimi\\OnlineReindex.sql
1. Sağ tıklayın, bağlantıyı seçin ve toohello katalog - bağlanmak&lt;kullanıcı&gt;. database.windows.net sunucusu zaten bağlıysa,
1. Bağlı toohello jobaccount veritabanı olduğundan ve F5 toorun hello betik basın emin olun

* sp\_add\_job, “Online Reindex PK\_\_VenueTyp\_\_265E44FD7FD4C885” adlı yeni bir iş oluşturur
* SP\_ekleme\_iş T-SQL komut metni tooupdate hello dizini içeren hello işi adımı oluşturur




## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]

> * Bir iş hesabı tooquery arasında birden çok Kiracı oluşturma
> * Tüm kiracı veritabanlarında verileri güncelleştirme
> * Tüm kiracı veritabanlarında bir tabloda dizin oluşturma

[Geçici analizler öğreticisi](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>Ek kaynaklar

* [Merhaba Wingtip SaaS uygulama dağıtımı sırasında yapı ek öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Ölçeği artırılmış bulut veritabanlarını yönetme](sql-database-elastic-jobs-overview.md)
* [Ölçeği artırılmış bulut veritabanları oluşturma ve yönetme](sql-database-elastic-jobs-create-and-manage.md)
