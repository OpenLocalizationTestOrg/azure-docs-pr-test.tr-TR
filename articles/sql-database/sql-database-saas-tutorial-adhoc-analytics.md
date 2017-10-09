---
title: "birden çok Azure SQL veritabanları arasında aaaRun geçici analitik sorguları | Microsoft Docs"
description: "Merhaba Wingtip SaaS çok kiracılı uygulama içinde birden çok SQL veritabanları arasında geçici analitik sorguları çalıştırın."
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
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>Geçici tüm Wingtip SaaS kiracılar arasında analitik sorguları çalıştırma

Bu öğreticide, dağıtılmış sorgular tooenable geçici analytics hello kümesinin tamamını Kiracı veritabanları üzerinde çalıştırın. Esnek sorgu gerektiren bir ek analiz veritabanı dağıtıldığı kullanılan tooenable dağıtılmış sorgular olan (toohello katalog sunucusu). Bu sorguları hello günlük işletimsel verileri hello Wingtip SaaS uygulamasının kaçınma Öngörüler ayıklayabilirsiniz.


Bu öğreticide şunları öğrenirsiniz:

> [!div class="checklist"]

> * Merhaba genel görünümler hakkında her veritabanında, kiracılar arasında verimli sorgulama etkinleştirin.
> * Nasıl toodeploy geçici Analizi veritabanı
> * Toorun sorguları tüm Kiracı veritabanları arasında nasıl dağıtılmış



Bu öğretici, Önkoşullar aşağıdaki yapma emin hello tamamlanır toocomplete:

* Merhaba Wingtip SaaS uygulaması dağıtılır. beş dakikadan kısa toodeploy bakın [dağıtma ve Merhaba Wingtip SaaS uygulaması keşfedin.](sql-database-saas-tutorial.md)
* Azure PowerShell’in yüklendiğinden. Ayrıntılar için bkz. [Azure PowerShell’i kullanmaya başlama](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* SQL Server Management Studio (SSMS) yüklenir. bkz: toodownload ve yükleme SSMS, [karşıdan SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


## <a name="ad-hoc-analytics-pattern"></a>Geçici analytics düzeni

SaaS uygulamaları ile Merhaba harika fırsatları toouse hello çok büyük miktarda Kiracı verilerini merkezi olarak hello bulutta depolanan biridir. Bu veri toogain fikir hello işlemi ve uygulamanız, kiracılarınıza, kendi kullanıcılar, tercihleri, davranışlar vb. kullanımını kullanın. Bu Öngörüler özelliği development, kullanılabilirlik yenilikleri ve diğer uygulamalar ve hizmetler yatırım yönlendirebilir.

Bu verilere tek bir çok kiracılı veritabanında erişim kolaydır, ancak binlerce veritabanına ölçekli olarak dağıtıldığında çok kolay değildir. Bir yaklaşım ise toouse [esnek sorgu](sql-database-elastic-query-overview.md), sağlayan veritabanları ortak bir şema ile dağıtılmış bir dizi arasında sorgulama. Esnek sorgusu kullanan tek bir *head* , dış tablolara tanımlanır (Kiracı) veritabanı yansıtma tabloları ve görünümleri hello dağıtılmış veritabanı. Sorguları gönderilen toothis head Veritabanı derlenmiş tooproduce gerektiği gibi toohello Kiracı veritabanları gönderilen hello sorgu bölümünü içeren bir dağıtılmış sorgu planı şunlardır. Esnek sorgu hello parça eşleme hello Katalog veritabanı tooprovide hello konumundaki hello Kiracı veritabanlarını kullanır. Kurulum ve sorgu standardını kullanarak basit [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)ve Power BI ve Excel gibi Araçları'ndan geçici sorgulama destekler.

Sorguları hello Kiracı veritabanları arasında dağıtarak, esnek sorgu Canlı üretim verileri daha iyi sağlar. Ancak, esnek sorgu potansiyel olarak birçok veritabanı veri çeker gibi gecikme süresi bazen eşdeğer sorgular için daha yüksek olabilir sorgu tooa tek çok Kiracı veritabanı gönderildi. Tasarlama döndürülen toominimize hello veri sorguladığında dikkatli olunmalıdır. Esnek sorgu genellikle en sık kullanılan karşılıklı toobuilding veya karmaşık analitik sorguları veya rapor küçük miktarda gerçek zamanlı veri sorgulama için uygundur. Sorguları da gerçekleştirme hello arayın [yürütme planı](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan) hello sorgu hangi kısmının gönderilen toohello Uzak veritabanı ve ne kadar veri döndürülmüyor aşağı toosee. Karmaşık analitik işleme daha iyi gerektiren sorguları bazı durumlarda bir adanmış veritabanı veya veri ambarı analitik sorguları için en iyi duruma getirilmiş içine Kiracı verileri çıkartarak sundu. Bu desen hello anlatılmıştır [Kiracı analytics Öğreticisi](sql-database-saas-tutorial-tenant-analytics.md). 

## <a name="get-hello-wingtip-application-scripts"></a>Merhaba Wingtip uygulama komut dosyaları alma

Merhaba Wingtip SaaS komut dosyaları ve uygulama kaynak koduna hello kullanılabilir [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github depo. [Adımları toodownload hello Wingtip SaaS betikleri](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="create-ticket-sales-data"></a>Bilet satış verileri oluşturma

toorun karşı daha ilginç bir veri kümesi, sorgular bilet satış verileri hello bilet-Oluşturucu çalıştırarak oluşturun.

1. Merhaba, *PowerShell ISE*açın hello... \\Öğrenme modülleri\\işletimsel Analytics\\geçici Analytics\\*Demo AdhocAnalytics.ps1* komut dosyası ve değerleri aşağıdaki hello ayarlayın:
   * **$DemoScenario** = 1, **satın tüm görebildikleri etkinliklerine biletlerini**.
2. Tuşuna **F5** hello komut dosyasını çalıştırın ve bilet satış oluşturmak için. Merhaba komut dosyası çalıştırılırken, bu öğreticide hello adımlara devam edin. Merhaba bilet verileri hello sorgulanan *dağıtılmış geçici sorguları çalıştırmak* bölümünde, toothat alıştırma aldığınızda hala çalışıyorsa, bu nedenle hello bilet Oluşturucu toocomplete için bekleyin.

## <a name="explore-hello-global-views"></a>Merhaba genel görünümler keşfedin

Merhaba Wingtip SaaS uygulamasına hello Kiracı veritabanı şeması tek Kiracı açısından tanımlanan şekilde bir kiracı başına veritabanı modeli kullanılarak oluşturulmuştur. Kiracı özgü bilgiler mevcut bir tabloda *Salonundan*, her zaman tek bir satır var ve birincil anahtarı olmayan bir yığın olarak uygulanır. Merhaba şema diğer tablolarla ilişkili toobe gerekmeyen toohello *Salonundan* normal kullanımda hiçbir zaman olduğundan Kiracı hello veri ait olduğu için şüpheli tablo.

Ancak, tüm veritabanları arasında sorgularken, tek bir mantıksal veritabanı parçalı Kiracı tarafından parçası ise gibi esnek sorgu hello veri davranabilirsiniz önemlidir. tooachieve Bu, bir dizi 'global' görünümleri olan bir kiracı kimliği her genel sorgulanır hello tabloları proje eklenen toohello Kiracı veritabanı. Örneğin, hello *VenueEvents* görünüm ekler bir hesaplanan *VenueId* toohello sütunları öngörülen hello *olayları* tablo. Üzerinden hello dış hello merkez veritabanı tablosunda tanımlayarak *VenueEvents* (Merhaba temel yerine *olayları* tablo), esnek sorgudur göre birleştirmeler aşağı mümkün toopush *VenueId* paralel her bir uzak veritabanına (yerine hello merkez veritabanı) yürütülebilecek şekilde. Bu çok sayıda sorgu performansını önemli bir artış sonuçlanır döndürülecek veri miktarı hello önemli ölçüde azaltır. Bu genel görünümler tüm Kiracı veritabanları önceden oluşturulmuştur (ve *basetenantdb*).

1. SSMS açın ve [toohello tenants1 - bağlanmak&lt;kullanıcı&gt; server](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms).
2. Genişletme **veritabanları**, sağ **contosoconcerthall**seçip **yeni sorgu**.
3. Sorguları tooexplore hello birbirinden hello tek Kiracı tablolar ve hello genel görünümler aşağıdaki hello çalıştırın:

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

Bu görünümlerde hello *VenueId* hello Salonundan adı, ancak herhangi bir yaklaşım karmasını kullanılan toointroduce benzersiz bir değer olabilir olarak hesaplanır. Bu yaklaşım hello Kiracı anahtarı hello katalog kullanmak için hesaplanan benzer toohello yoludur.

Merhaba tooexamine hello tanımı *görebildikleri* görünümü:

1. İçinde **Object Explorer**, genişletin **contosoconcethall** > **görünümleri**:

   ![Görünümler](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. Sağ **dbo. Görebildikleri**.
3. Seçin **komut görünüm olarak** > **için oluşturun** > **yeni sorgu Düzenleyicisi penceresini**

Herhangi bir hello diğer komut dosyası *Salonundan* toosee görünümleri hello nasıl ekledikleri *VenueId*.

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>Dağıtılmış geçici sorgular için kullanılan hello veritabanı dağıtma

Bu alıştırmada hello dağıtır *adhocanalytics* veritabanı. Bu tüm Kiracı veritabanları arasında sorgulamak için kullanılan hello şema içerecek hello baş veritabanıdır. Merhaba, dağıtılan toohello hello sunucu hello örnek uygulama yönetimiyle ilgili tüm veritabanları için kullanılan katalog sunucusu varolan veritabanıdır.

1. Aç... \\Öğrenme modülleri\\işletimsel Analytics\\geçici Analytics\\*Demo AdhocAnalytics.ps1* hello içinde *PowerShell ISE* ve kümesi hello Aşağıdaki değerler:
   * **$DemoScenario** = 2, **Geçici analiz veritabanı dağıtma**.

2. Tuşuna **F5** toorun hello komut dosyası ve hello oluşturma *adhocanalytics* veritabanı.

Kullanılan toorun dağıtılmış sorgular olabilir hello sonraki bölümde, şema toohello veritabanını ekleyin.

## <a name="configure-hello-database-for-running-distributed-queries"></a>Dağıtılmış sorgular çalıştırmak için hello veritabanını Yapılandır

Bu alıştırmada, tüm Kiracı veritabanları arasında sorgulama sağlar (Merhaba dış veri kaynağına ve dış tablo tanımları) şema toohello geçici Analizi veritabanı ekler.

1. SQL Server Management Studio'yu açın ve toohello hello önceki adımda oluşturduğunuz geçici Analizi veritabanı bağlanın. Merhaba veritabanının Hello adı adhocanalytics olacaktır.
2. Açık ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql* SSMS içinde.
3. Merhaba SQL komut dosyasını gözden geçirin ve hello aşağıdakileri göz önünde bulundurun:

   Bir veritabanı kapsamlı bir kimlik bilgisi tooaccess her hello Kiracı veritabanlarının esnek sorgusu kullanır. Bu kimlik bilgisi toobe tüm hello veritabanlarında kullanılabilir gerekir ve normal olarak bu geçici sorgular tooenable hello en düşük hakları gerekli verilmelidir.

    ![kimlik bilgisi oluşturma](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   Merhaba, dış veri kaynağına toouse hello Kiracı parça eşleme hello katalog veritabanında tanımlı. Bu hello dış veri kaynağı olarak kullanarak, sorguları hello sorgu çalıştığında hello kataloğa kayıtlı dağıtılmış tooall veritabanlarıdır. Sunucu adları için her bir dağıtım farklı olduğundan, bu başlatma betiği hello Katalog veritabanı hello konumunu hello geçerli sunucu alarak alır (@@servername) hello betik yürütüldüğü.

    ![Dış veri kaynağı oluşturun](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   ile tanımlanan ve hello önceki bölümde açıklanan hello genel görünümlere başvuru dış tablolara hello **dağıtım SHARDED(VenueId) =**. Çünkü her *VenueId* tooa tek veritabanı eşlemeleri bu hello sonraki bölümde gösterildiği gibi birçok senaryo için performansı geliştirir.

    ![Dış tabloları oluşturma](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   Merhaba yerel tablo *VenueTypes* oluşturulur ve doldurulur. Bu başvuru veri tablosu tüm Kiracı veritabanları ortak olduğundan burada yerel tablo olarak ve hello ortak verilerle doldurulan gösterilebilir. Bu hello azaltmak bazı sorgular için veri miktarını taşınmış hello hello Kiracı veritabanları arasında *adhocanalytics* veritabanı.

    ![Tablo oluşturma](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   Bu şekilde başvuru tabloları eklerseniz, hello Kiracı veritabanları güncelleştirdiğinizde emin tooupdate hello tablo şemasını ve verileri olabilir.

4. Tuşuna **F5** toorun hello komut dosyası ve hello başlatma *adhocanalytics* veritabanı. 

Şimdi dağıtılmış sorgular çalıştırın ve tüm kiracılar arasında görüşleri toplamak!

## <a name="run-ad-hoc-distributed-queries"></a>Dağıtılmış geçici sorguları çalıştırma

Şimdi bu hello *adhocanalytics* veritabanı ayarlama, devam edin ve bazı dağıtılmış sorgular çalıştırın. Daha iyi hello sorgu işleme nerede gerçekleştiği anlamak için hello yürütme planı içerir. 

Merhaba yürütme planı incelerken, Ayrıntılar için hello planı simgeler üzerine gelerek. 

Önemli toonote olduğundan, ayar **dağıtım SHARDED(VenueId) =** biz hello dış veri kaynağına tanımlandığında, çok sayıda senaryoları için performansı geliştirir. Çünkü her *VenueId* tooa eşlemeleri tek veritabanı kolayca Bitti'yi uzaktan, döndürmeyi yalnızca hello veri ihtiyacımız olan filtreleme.

1. SSMS’te ...\\Öğrenme Modülleri\\İşlem Analizi\\Geçici Analiz\\*Demo-AdhocAnalyticsQueries.sql* dosyasını açın.
2. Bağlı toohello olduğundan emin olun **adhocanalytics** veritabanı.
3. Select hello **sorgu** menüsüne ve ardından **gerçek Execution Plan Ekle**
4. Merhaba vurgulayın *hangi görebildikleri şu anda kayıtlı olan?* sorgu ve tuşuna **F5**.

   Merhaba sorgu nasıl hızlı gösteren hello tüm salonundan listesini döndürür ve onu tooquery tüm kiracılar ve her bir kiracı dönüş verileri arasında kolaydır.

   Merhaba planı inceleyebilir ve sadece giderek tooeach Kiracı veritabanı ve hello salonundan bilgi seçme ki çünkü hello tüm maliyetini hello uzak sorgu olduğunu görürsünüz.

   ![SEÇİN * dbo gelen. Görebildikleri](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. Select hello sonraki sorgu ve tuşuna **F5**.

   Bu sorgu hello Kiracı veritabanları ve hello yerel verileri birleştirir *VenueTypes* tablosu (Merhaba tabloda olarak yerel *adhocanalytics* veritabanı).

   Merhaba planı inceleyebilir ve o hello bkz maliyet çoğunluğu olduğundan hello uzak sorgu biz her bir kiracının salonundan bilgisi (dbo. sorgu Görebildikleri), ve ardından Hızlı yerel bir birleşme hello yerel yapın *VenueTypes* tablo toodisplay hello kolay adı.

   ![Uzak ve yerel verileri birleştirme](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. Şimdi hello seçin *satılan çoğu biletleri hello hangi gününde olan?* sorgu ve tuşuna **F5**.

   Bu sorgu, biraz daha karmaşık birleştirme ve toplama işlemlerini gerçekleştirir. Önemli toonote nedir hello işleme çoğunu uzaktan yapılır ve yine de geri getirmek biz yalnızca hello satır, her salonundan 's toplama bilet satış sayısı her gün için yalnızca tek bir satır döndürme ihtiyacımız var.

   ![sorgu](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:

> [!div class="checklist"]

> * Tüm kiracı veritabanlarında dağıtılmış sorguları çalıştırma
> * Bir geçici analytics veritabanı dağıtmak ve şema tooit dağıtılmış toorun sorguları ekleyin.


Şimdi hello deneyin [Kiracı Analytics öğretici](sql-database-saas-tutorial-tenant-analytics.md) tooexplore daha karmaşık analitik işleme için veri tooa ayrı analytics veritabanı ayıklanıyor...

## <a name="additional-resources"></a>Ek kaynaklar

* Ek [hello Wingtip SaaS uygulamasına yapı öğreticileri](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Esnek Sorgu](sql-database-elastic-query-overview.md)
