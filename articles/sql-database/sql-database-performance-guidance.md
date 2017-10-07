---
title: "aaaAzure SQL veritabanı performans Kılavuzu ayarlama | Microsoft Docs"
description: "Bu makalede, uygulamanız için hangi hizmet katmanı toochoose belirlemenize yardımcı olabilir. Ayrıca, uygulama tooget hello Azure SQL veritabanından en yolları tootune önerir."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Azure SQL veritabanında performans ayarlama

Azure SQL veritabanı sağlar [önerileri](sql-database-advisor.md) veritabanınızın tooimprove performansını kullanabilir veya Azure SQL veritabanı sağlayabilirsiniz [tooyour uygulama otomatik olarak uyum](sql-database-automatic-tuning.md) ve değişiklikleri uygulayın Bu, İş yükünüzün performansını artırır.

Size herhangi bir geçerli önerimiz yok ve performans sorunlarını çözümlenmedi, yöntemleri tooimprove performanslarını aşağıdaki hello kullanabilirsiniz:
1. Artırmak [hizmet katmanları](sql-database-service-tiers.md) ve daha fazla kaynak tooyour veritabanı sağlayın.
2. Uygulamanızı ayarlama ve performansı artırabilir bazı en iyi uygulamalar uygulayın. 
3. Dizinler ve toomore verimli bir şekilde verilerle çalışma sorgular değiştirerek Hello veritabanı ayarlayın.

El ile uygulanan yöntemleri toodecide gerekenleri çünkü bunlar [hizmet katmanları](sql-database-service-tiers.md) seçmeniz veya toorewrite uygulama veya veritabanı kod gerekir ve hello değişiklikleri deply.

## <a name="increasing-performance-tier-of-your-database"></a>Veritabanınızın artan performans katmanı

Azure SQL veritabanı sunan dört [hizmet katmanları](sql-database-service-tiers.md) , arasından seçim yapabilirsiniz: temel, standart, Premium ve Premium RS (performans veritabanı işleme birimleri içinde ölçülen veya [Dtu'lar](sql-database-what-is-a-dtu.md). Her hizmet katmanında kesinlikle SQL veritabanınız kullanabilirsiniz ve bu hizmet düzeyi için tahmin edilebilir performans garanti hello kaynakları yalıtır. Bu makalede, uygulamanız için hello hizmet katmanı seçmenize yardımcı olacak yönergeler sağlıyoruz. Ayrıca, uygulama tooget hello Azure SQL veritabanından en ince ayar yolları aşağıdakiler ele.

> [!NOTE]
> Bu makalede tek veritabanları Azure SQL Database performans rehberi odaklanır. Performans rehberi için bkz: ilgili tooelastic havuzlarını [esnek havuzlar için fiyat ve performans konuları](sql-database-elastic-pool-guidance.md). Ancak, bu makale toodatabases esnek havuzdaki önerileri ayarlama hello çoğunu uygulamak ve benzer performans avantajlarından yararlanabilmek unutmayın.
> 

* **Temel**: hello temel hizmet katmanı teklifleri iyi bir performans öngörülebilirlik her veritabanı için saat üzerinden saat. Temel bir veritabanında yeterli kaynakları birden çok eşzamanlı istek yok küçük bir veritabanında iyi bir performans desteklemez. Temel Hizmet katmanını kullandığınızda tipik kullanım örnekleri şunlardır:
  * **Yalnızca Azure SQL veritabanı ile çalışmaya Başlarken**. Genellikle geliştirme olan uygulamalar, yüksek performans düzeyleri gerek yoktur. Veritabanı geliştirme veya sınama, düşük fiyat noktada için ideal bir ortam temel veritabanlarıdır.
  * **Tek bir kullanıcıyla bir veritabanına sahip**. Tek bir kullanıcı genellikle bir veritabanıyla ilişkilendirin uygulamaları yüksek tutarlılık ve performans gereksinimlerini yok. Bu uygulamalar hello temel hizmet katmanı için bir aday değildir.
* **Standart**: hello standart hizmet katmanı performansı öngörülebilirlik sunar ve çalışma grubu ve web uygulamaları gibi birden çok eş zamanlı istekleri veritabanları için iyi bir performans sağlar. Bir standart hizmet katmanı veritabanı seçtiğinizde, veritabanı uygulamanızı tahmin edilebilir performans üzerinde boyutlandırabilirsiniz dakika üzerinden dakika.
  * **Birden çok eşzamanlı istek veritabanınızı sahip**. Genellikle aynı anda birden fazla kullanıcı hizmet uygulamaları, daha yüksek performans düzeyleri gerekir. Örneğin, birden çok eşzamanlı sorguyu destekler düşük toomedium g/ç trafiği gereksinimlerin çalışma grubu veya web uygulamaları hello standart hizmet katmanı için iyi bir aday değildir.
* **Premium**: hello Premium Hizmet katmanını tahmin edilebilir performans sunar ikinci olarak, her Premium veritabanı için üzerinden ikinci. Merhaba Premium Hizmet katmanını seçtiğinizde, bu veritabanı için hello yoğun yük temel veritabanı uygulamanızı boyutlandırabilirsiniz. Merhaba planı performans farkı küçük sorguları tootake gecikme süresine duyarlı işlemleri beklenenden uzun neden olabilir durumlarda kaldırır. Bu model hello geliştirme ve ürün doğrulama döngüleri toomake güçlü deyimleri en yüksek kaynak gereksinimleri, performans farkı veya sorgu gecikmesi hakkında gereken uygulamalar için büyük ölçüde basitleştirebilir. Çoğu Premium Hizmet katmanını kullanım örnekleri, bir veya daha fazla şu özelliklere sahiptir:
  * **Yüksek yoğun yük**. Önemli ölçüde CPU, bellek veya giriş/çıkış (g/ç) toocomplete gerektiren bir uygulama işlemlerini ayrılmış, yüksek performans düzeyi gerektirir. Örneğin, tooconsume bilinen bir veritabanı uzun bir süre için birkaç CPU çekirdekleri işlemdir hello Premium Hizmet katmanını aday.
  * **Çok sayıda eşzamanlı istek**. Bir Web sitesi, hizmet veren bir yüksek trafik hacmi olduğunda bazı veritabanı çok sayıda eşzamanlı istek, örneğin, hizmet uygulamaları. Temel ve standart hizmet katmanları hello veritabanı başına eşzamanlı istek sayısını sınırlayın. Daha fazla bağlantı gerektiren uygulamalar toochoose bir uygun ayırma boyutu toohandle hello istekleri sayısı üst sınırını gerekli gerekir.
  * **Düşük gecikme süresi**. Bazı uygulamalar tooguarantee hello veritabanından yanıt en az sürede gerekir. Belirli bir saklı yordam daha geniş bir müşteri işleminin bir parçası çağrılırsa, en fazla 20 milisaniye cinsinden hello süresinin yüzde 99'return bu çağrısından gereksinim toohave sahip olabilir. Bu tür bir uygulama avantajları hello Premium hizmet katmanından, toomake gücünün bu hello gerekli emin kullanılabilir.
* **Premium RS**: Premium RS katmanı hello gerektirmez g/ç açısından yoğun iş yükleri yüksek kullanılabilirlik garantilerinden hello için tasarlanmıştır. Örnekler, yüksek performanslı iş yükleri veya hello veritabanı kaydının hello sistem olduğu analitik bir iş yükü test edilmesini içerir.

SQL veritabanınız için gereksinim duyduğunuz hello hizmet düzeyi her kaynak boyutu için hello yoğun yük gereksinimlerine bağlıdır. Bazı uygulamaları tek bir kaynak Önemsiz miktarını kullanır, ancak diğer kaynaklar için önemli gereksinimleri vardır.

### <a name="service-tier-capabilities-and-limits"></a>Hizmet katmanı özellikleri ve sınırları

Her bir hizmet katmanına hello esneklik toopay yalnızca gereksinim duyduğunuz hello kapasitesi alacak şekilde hello performans düzeyi ayarlayın. Yapabilecekleriniz [kapasite ayarlamak](sql-database-service-tiers.md), yukarı veya aşağı, iş yükü değişiklikleri olarak. Örneğin, veritabanının yükünüzü hello geri Okul alışveriş sezonu sırasında yüksekse, Temmuz Eylül aracılığıyla belirlenen bir süre için hello veritabanı için hello performans düzeyi artırabilir. Yoğun sezonu sona erdiğinde azaltabilir. İşinizin, bulut ortamı toohello mevsimselliğin en iyi duruma getirme tarafından ödeme en aza indirebilirsiniz. Bu model de iyi yazılım ürün yayın döngüsü boyunca çalışır. Test çalışmasını ve test bitirdiğinizde kapasiteyi yayın sırasında test takımı kapasite ayırabilir. Gereksinim ve nadiren kullanabilecek ayrılmış kaynakları harcama kaçının bir kapasite isteği modelde kapasiteyi ücret ödersiniz.

### <a name="why-service-tiers"></a>Neden katmanları hizmet?
Her veritabanı iş yükü değişebilir hizmet katmanları hello amacı tooprovide performans öngörülebilirlik çeşitli performans düzeyleri olsa da. Büyük ölçekli veritabanı kaynak gereksinimleri müşterilerle daha ayrılmış bir bilgisayar ortamda çalışabilir.

## <a name="tune-your-application"></a>Uygulamanızı ayarlama
Geleneksel şirket içi SQL Server ' ilk kapasite planlaması hello işlemi genellikle uygulama üretimde çalışan hello işleminden ayrılır. Donanım ve Ürün lisans ilk satın ve performans ayarlama daha sonra yapılır. Azure SQL veritabanı kullandığınızda, bu uygulamayı çalıştıran ve bu ayar bir fikir toointerweave hello işlemidir. İsteğe bağlı kapasite için ödeme hello modeli ile bir uygulama için hangi sıklıkta yanlış Gelecekteki büyümeyi planları tahmin üzerinde temel donanımda işleminin yerine şimdi, gerekli uygulama toouse hello minimum kaynaklarınızı ayarlayabilirsiniz. Bazı müşteriler değil tootune bir uygulama seçin ve bunun yerine toooverprovision donanım kaynakları seçin. Toochange meşgul bir süre içinde önemli uygulama istemiyorsanız, bu yaklaşım iyi bir fikir olabilir. Ancak, Azure SQL veritabanı'nda hello hizmet katmanları kullandığınızda, bir uygulama ayarı kaynak gereksinimlerini ve daha düşük aylık faturaları en aza indirebilirsiniz.

### <a name="application-characteristics"></a>Uygulama özellikleri
Azure SQL Database hizmet katmanları tasarlanmış tooimprove performans kararlılık ve öngörülebilirlik için bir uygulama olsa da, bazı en iyi uygulamalar, uygulama toobetter faydalanan bir performans düzeyinde hello kaynakları ince ayar yardımcı olabilir. Birçok uygulama yalnızca göre önemli performans artışları sahip olsa da tooa geçiş daha yüksek performans düzeyi veya hizmet katmanı, bazı uygulamalar gerek toobenefit hizmetinin daha yüksek bir düzeyinden ayarlama ek. Performansı artırmak için bu özelliklere sahip uygulamalar için ek uygulama ayarlamayı göz önünde bulundurun:

* **Yavaş performansı nedeniyle "chatty" davranışı uygulamaları**. Chatty uygulamaları hassas toonetwork gecikme aşırı veri erişim işlemleri yapın. Bu tür uygulamalar tooreduce hello veri erişim işlemleri toohello SQL veritabanı sayısı toomodify gerekebilir. Örneğin, geçici sorguları toplu işleme veya toostored yordamları hello sorgular taşıma gibi teknikler kullanılarak uygulama performansını iyileştirebilir. Daha fazla bilgi için bkz: [Toplu sorguları](#batch-queries).
* **Tüm tek makine tarafından desteklenen yoğun bir iş yükü veritabanlarıyla**. Hello kaynakları hello yüksek Premium performans düzeyinin aşan veritabanları hello iş yükünü ölçeklendirme yararlı. Daha fazla bilgi için bkz: [veritabanları arası parçalama](#cross-database-sharding) ve [işlevsel bölümleme](#functional-partitioning).
* **Yetersiz sorguları uygulamaları**. Uygulamalar, özellikle de sorguları kötü düzenlediniz hello veri erişim katmanı, daha yüksek bir performans düzeyinden yararlanabilir değil. Bu, WHERE yan tümcesi eksik, dizinleri eksik olan veya istatistikleri eski sorguları içerir. Bu uygulamalar standart sorgu teknikleri performans ayarlama yarar. Daha fazla bilgi için bkz: [eksik dizinler](#identifying-and-adding-missing-indexes) ve [ayarlama ve ipucu sorgu](#query-tuning-and-hinting).
* **Yetersiz veri uygulamaları erişim tasarım**. Devralınan veri erişim eşzamanlılık sorunları, örneğin kilitlenmenin, uygulamaları daha yüksek bir performans düzeyinden yararlı değildir. Gidiş dönüş hello Azure SQL veritabanı hello istemci tarafında önbelleğe alma verileri tarafından hello Azure önbellek hizmeti ile karşı veya başka bir önbelleğe alma teknolojisi azaltmayı deneyin. Bkz: [uygulama katmanı önbelleğe alma](#application-tier-caching).

## <a name="tune-your-database"></a>Veritabanınızı ayarlama
Bu bölümde, uygulamanız için tootune Azure SQL veritabanı toogain hello en iyi performansı kullanın ve en düşük olası performans düzeyinde hello çalıştırmak bazı teknikleri ele. Başkalarının belirli tooAzure SQL veritabanı olan ancak bu teknikler bazıları geleneksel SQL Server en iyi yöntemler ayarlama eşleşmesi. Bazı durumlarda, bir veritabanı toofind alanları toofurther ayarlama için tüketilen hello kaynakları inceleyin ve Azure SQL veritabanında geleneksel SQL Server teknikleri toowork genişletir.

### <a name="identify-performance-issues-using-azure-portal"></a>Azure portalını kullanarak performans sorunlarını belirle
Araçları hello Azure Portalı'nda aşağıdaki hello çözümlemek ve SQL veritabanı ile performans sorunlarını gidermenize yardımcı olabilir:

* [Sorgu Performansı Öngörüleri](sql-database-query-performance.md)
* [SQL Veritabanı Danışmanı](sql-database-advisor.md)

Hello Azure portal sahip hem de bu araçları hakkında daha fazla bilgi ve nasıl toouse bunları. tooefficiently tanılamak ve doğru sorunları hello araçları hello Azure Portalı'nda ilk deneyin önerilir. Eksik dizinler ve özel durumlarda sorgu ayarlama için ardından, aşağıdakiler ele yaklaşımlar ayarlama hello el ile kullanmanızı öneririz.

Üzerinde Azure SQL veritabanı sorunlarını tanımlama hakkında daha fazla bilgi bulmak [performans izleme](sql-database-single-database-monitor.md) makalesi.

### <a name="identifying-and-adding-missing-indexes"></a>Tanımlama ve eksik dizinler ekleme
Ortak bir OLTP veritabanı performans sorunu toohello fiziksel veritabanı tasarım ilişkilendirir. Genellikle, veritabanı şemalarını tasarlanır ve ölçekli (ya da yükleme veya veri birimi) sınamadan geliyordu. Ne yazık ki, bir sorgu planı hello performansını bir küçük ölçekte kabul edilebilir ancak üretim düzeyinde veri birimlerini önemli ölçüde düşürebilir. Merhaba en yaygın bu sorunu hello eksikliği uygun dizinleri toosatisfy filtre ya da başka kısıtlamalar sorguda kaynağıdır. Dizin arama yeterli genellikle, bir tablo olarak eksik dizinler bildirimleri taramasını.

Bir arama yeterli, bu örnekte, bir tarama hello seçili sorgu planı kullanır:

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Eksik dizinler içeren bir sorgu planı](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Azure SQL veritabanı Bul ve koşullar dizin düzeltme ortak eksik yardımcı olabilir. Azure SQL veritabanına yerleşik Dmv'leri içinde bir dizin önemli ölçüde hello tahmini maliyet toorun bir sorgu azaltabilir sorgu derlemelerinin arayın. Sorgu yürütme sırasında her sorgu planı ne sıklıkta yürütülen SQL veritabanı izler ve burada bu dizin mevcut olan bir sorgu planı ve hello yürütme hello arasındaki boşluğu tasarlandı parçaları hello tahmini. Genel iş yükü maliyet veritabanı ve onun gerçek iş yükü için hangi değişikliklerin tooyour fiziksel veritabanı tasarım iyileştirebilir bu Dmv'leri tooquickly tahmin kullanabilirsiniz.

Bu sorgu tooevaluate olası dizinleri eksik kullanabilirsiniz:

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

Bu örnekte, bu önerisine hello sorgu sonuçlandı:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Oluşturulduktan sonra aynı SELECT deyimi bir tarama yerine bir arama kullanan ve hello planı daha verimli bir şekilde yürütür farklı bir plan seçer:

![Düzeltilmiş dizinleri içeren bir sorgu planı](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

Merhaba anahtar Insight bu hello paylaşılan g/ç kapasitesi, ticari sistem daha kısıtlı bir adanmış sunucu makine,. Gereksiz g/ç tootake en büyük avantajlarından hello DTU hello sistemdeki her hello Azure SQL Database hizmet katmanlarına yönelik performans düzeyinin en aza üzerinde bir premium yoktur. Önemli ölçüde uygun fiziksel veritabanı tasarım seçenekleri tek tek sorgular için hello gecikme süresini artırmak, Ölçek birimi işlenen eş zamanlı isteklerin hello verimini artırmak ve hello maliyetleri gerekli toosatisfy hello sorgu en aza. Dizin Dmv'leri eksik hello hakkında daha fazla bilgi için bkz: [sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Sorgu ayarlama ve ipuçları
Azure SQL veritabanında Hello sorgu iyileştiricisi benzer toohello geleneksel SQL Server sorgu iyileştiricisi ' dir. Sorgular ve hello sorgu iyileştiricisi modeli sınırlamalar da akıl anlama hello ayarlama hello en iyi yöntemler çoğunu tooAzure SQL veritabanı uygulayın. Azure SQL Database sorguları ayarlamak, birleşik kaynak taleplerini azaltma hello ek bir avantaja alabilirsiniz. Daha düşük bir performans düzeyinde çalışabildiğinden uygulamanızı karıncalı gösteren eşdeğer bir daha düşük bir maliyetle mümkün toorun olabilir.

SQL Server'da ortak ve tooAzure SQL veritabanı da geçerli nasıl hello sorgu iyileştiricisi "sızar" parametreleri örneğidir. Derleme sırasında daha uygun bir sorgu planı oluşturabilir olmadığını hello sorgu iyileştiricisi hello geçerli bir parametre toodetermine değerini değerlendirir. Bu stratejinin önemli ölçüde daha hızlı bir şekilde bilinen parametre değerlerini derlenmiş bir planı tooa sorgu planı genellikle açabilir ancak şu anda imperfectly her ikisi de çalıştığını SQL Server ve Azure SQL veritabanı. Bazen hello parametresi sniffed değil ve bazen hello parametresi sniffed ancak hello oluşturulan plan hello tam bir iş yükü parametre değerleri kümesi için yetersiz. Microsoft hedefi daha bilinçli olarak belirtin ve parametre algılaması hello varsayılan davranışı geçersiz kılma sorgulama ipuçlarını (yönergeleri) içerir. Genellikle, ipuçlarını kullanırsanız, belirli bir müşteri iş yükü için kusurlu hello varsayılan SQL Server veya Azure SQL veritabanı davranış olduğu durumlar düzeltebilirsiniz.

hello Sorgu işlemcisi hem performans ve kaynak gereksinimleri için uygun olmayan bir planı nasıl oluşturacağınız Hello sonraki örnek gösterilmektedir. Bu örnek bir sorgu ipucu kullanırsanız, SQL veritabanınız için sorgu çalıştırma zaman ve kaynak gereksinimlerini azaltmak de gösterir:

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

Merhaba Kurulum kodu, veri dağıtımı eğri bir tablo oluşturur. Merhaba en iyi sorgu planı farklı hangi parametresini seçili temel. Ne yazık ki, önbelleğe alma davranışı hello planı her zaman hello sorgu hello en yaygın parametre değerine göre yeniden derleyin değil. Bu nedenle, önbelleğe alınan ve hatta farklı bir plan daha iyi bir plan seçim ortalama olabilir birden fazla değer için kullanılan bir yetersiz planı toobe için mümkündür. Daha sonra özel sorgu ipucu varsa ancak bu, aynı olan iki saklı yordamlar hello sorgu planı oluşturur.

**Örneğin, bölüm 1**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Örneğin, bölüm 2**

(Merhaba sonuçları telemetri verilerini kaynaklanan hello ayrı; böylece hello örnek 2 parçası başlamadan önce en az 10 dakika bekleyin öneririz.)

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Bu örnekte her bir parçasını toorun parametreli INSERT deyiminin 1.000 kez çalışır (toogenerate yeterli yük toouse sınama veri kümesi olarak). Saklı yordamlar yürütüldüğünde, hello Sorgu işlemcisi toohello yordamı (parametre "algılaması"), ilk derleme sırasında geçirilen hello parametre değeri inceler. Merhaba işlemci hello elde edilen planı önbelleğe alır ve hello parametre değeri farklı olsa bile sonraki etkinleştirmeleri için kullanır. tüm durumlarda Hello en iyi planı kullanılmayabilir. Bazen tooguide hello iyileştirici toopick zaman hello sorgu önce derlenen gelen hello belirli talebi yerine hello ortalama çalışması için daha iyi bir plan gerekir. Bu örnekte, tüm satırları toofind hello parametreyle eşleşen her değeri okuyan bir "tarama" planı hello ilk planı oluşturur:

![Bir tarama planı kullanarak ayarlama sorgulama](./media/sql-database-performance-guidance/query_tuning_1.png)

Biz hello değeri 1 kullanılarak hello yordamı yürütülen çünkü hello elde edilen planı başlangıç değeri 1'için en iyi ancak hello tablosundaki diğer tüm değerler için yetersiz. Her plan rastgele hello planda daha yavaş çalışır ve daha fazla kaynak kullandığı için toopick olsaydı istiyor Hello sonuç olası değil.

Merhaba test ile çalıştırırsanız `SET STATISTICS IO` çok ayarlamak`ON`, bu örnekte hello mantıksal tarama iş hello arka planda gerçekleştirilir. 1,148 okuma (Merhaba ortalama tooreturn yalnızca bir satır durumda verimsiz) hello plan tarafından yapılan olduğunu görebilirsiniz:

![Mantıksal bir tarama kullanarak ayarlama sorgulama](./media/sql-database-performance-guidance/query_tuning_2.png)

Merhaba örneği Hello ikinci bölümü hello derleme işlemi sırasında bir sorgu ipucu tootell hello iyileştirici toouse belirli bir değeri kullanır. Bu durumda, hello parametre olarak geçirilen hello Sorgu işlemcisi tooignore hello değeri zorlar ve bunun yerine tooassume `UNKNOWN`. Bu hello ortalama sıklığını (Eğme yoksayar) hello tablosunda yok tooa değeri ifade eder. Merhaba elde edilen planı daha hızlıdır ve bölüm bu örnek 1 ortalama olarak hello planı'den daha az kaynak kullanan bir arama tabanlı planı şöyledir:

![Bir sorgu ipucunu kullanarak sorguyu ayarlamayı](./media/sql-database-performance-guidance/query_tuning_3.png)

Merhaba hello aslında görebilirsiniz **sys.resource_stats** tablosu (Merhaba test ve ne zaman hello veri hello tablo doldurur yürütme hello zamandan bir gecikme olur). Bu örnek, hello 22:25:00 zaman penceresi sırasında yürütülen bölüm 1 ve 2. Bölüm 22:35: 00'dan yürütüldü. Merhaba önceki zaman penceresi daha fazla kaynak (nedeniyle plan Verimlilik geliştirmeleri) sonraki bir hello daha konusu zaman penceresi kullanılır.

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Sorgu ayarlama örneği sonuçları](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Bu örnekte Hello birim özellikle küçük olsa da, yetersiz parametreleri hello etkisini özellikle büyük veritabanları üzerinde önemli olabilir. aşırı durumlarda Hello fark hızlı durumlarda saniye ile yavaş durumlarda saat arasında olabilir.
> 
> 

İnceleyebilirsiniz **sys.resource_stats** toodetermine olup hello kaynak testi için başka bir test daha az veya daha fazla kaynak kullanır. Veri karşılaştırdığınızda, böylece hello olmadıkları hello zamanlama testleri ayrı hello aynı 5 dakikalık penceresinde **sys.resource_stats** görünümü. Merhaba hello alıştırma toominimize hello toplam miktarı, kullanılan kaynakların ve toominimize hello yoğun kaynakları değil hedefidir. Genellikle, bir gecikme için kod parçasını iyileştirme Ayrıca kaynak tüketimini azaltır. Tooan uygulama hello değişiklikler gereklidir ve hello değişiklikler sorgulama ipuçlarını hello uygulamada kullanabilecek birinin hello müşteri deneyimini olumsuz etkilemez emin olun.

Bir iş yükü sorgularını yineleme kümesi varsa, genellikle bu algılama toocapture yapar ve hello en düşük kaynak boyutu birimi gerekli toohost hello veritabanı sürücüleri olduğundan planı seçenekleriniz, hello en iyi hale getirme doğrulayın. Bazen, doğrulama sonra bunlar değil düşürülmüş olduğundan emin olun toohelp hello planları yeniden gözden geçirin. Hakkında daha fazla bilgiyi [sorgulama ipuçlarını (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Veritabanları arası parçalama
Azure SQL veritabanı ticari donanım üzerinde çalıştığından, tek bir veritabanı için kapasite limitlerini hello geleneksel şirket içi SQL Server yüklemesi için daha düşük. Merhaba işlemlerini tek bir Azure SQL veritabanı veritabanında hello sınırları içinde uygun olmayan bazı müşteriler birden fazla veritabanı parçalama teknikleri toospread veritabanı işlemleri kullanın. Azure SQL veritabanı'nda parçalama teknikleri kullanan çoğu müşteri verilerini tek bir boyuttaki birden çok veritabanı arasında bölün. Bu yaklaşım, OLTP uygulamalar genellikle tooonly bir satır veya tooa küçük grup hello şema satır uygulamak işlemleri gerçekleştirmek toounderstand gerekir.

> [!NOTE]
> SQL veritabanı artık bir kitaplık tooassist parçalama ile sağlar. Daha fazla bilgi için bkz: [esnek veritabanı istemci kitaplığına genel bakış](sql-database-elastic-database-client-library.md).
> 
> 

Bir veritabanında müşteri adı, sipariş ve (SQL Server ile birlikte gelen geleneksel örnek Northwind veritabanı hello gibi) sipariş ayrıntılarını varsa, örneğin, size bu verileri birden çok veritabanlarına hello müşteriyle gruplandırarak bölebilir ilgili sipariş ve Sipariş Ayrıntısı bilgi. Merhaba müşterinin verileri tek bir veritabanında kalır garanti edebilir. Merhaba uygulaması hello yük birden çok veritabanı arasında etkili bir şekilde yayılmak veritabanları arasında farklı müşterilere ayırırsınız. Parçalama ile müşteriler yalnızca hello en fazla veritabanı boyut sınırına önleyebilirsiniz ancak Azure SQL veritabanı da işlenebilecek içine tek tek her veritabanı uygun sürece hello farklı performans düzeylerini hello sınırlardan önemli ölçüde daha büyük iş yüklerini kendi DTU.

Veritabanı parçalama bir çözüm için hello birleşik kaynak kapasitesini azaltmaz ancak birden fazla veritabanı yayılır çok büyük çözümlerde destekleyen en son derece etkili olur. Her veritabanı bir farklı performans düzeyi toosupport çok büyük, yüksek kaynak gereksinimleri "etkin" veritabanları adresindeki çalıştırabilirsiniz.

### <a name="functional-partitioning"></a>İşlev bölümlendirme
SQL Server kullanıcıları genellikle tek bir veritabanında birçok işlevini birleştirin. Örneğin, bir uygulama bir mağaza için mantığı toomanage Envanter varsa, bu veritabanı izleme satınalma siparişi, saklı yordamları ve ayın son bildirdikleri yönetmek dizinlenmiş veya gerçekleştirilmiş görünümler stok ile ilişkili mantığı sahip olabilir. Bu teknik daha kolay tooadminister hello veritabanı yedekleme gibi işlemleri için kolaylaştırır, ancak aynı zamanda bir uygulamanın tüm işlevlerinin, toosize hello donanım toohandle hello yoğun yük gerektirir.

Azure SQL veritabanı genişleme mimarisinde kullanmak iyi bir fikir toosplit farklı işlevler farklı veritabanlarına bir uygulama olur. Bu yöntemi kullanarak, her uygulama bağımsız olarak ölçekler. Hello Yöneticisi uygulama yoğun olur (ve hello veritabanını artış üzerindeki yükü hello gibi), her işlevin bağımsız performans düzeyleri hello uygulamada seçebilirsiniz. Bu mimari ile Merhaba sınırı, bir uygulama birden fazla makine arasında hello yük yayıldığı için tek Emtia makine işleyebileceğinden daha büyük olamaz.

### <a name="batch-queries"></a>Toplu sorguları
Yüksek hacimli kullanarak veri erişim uygulamalar için sık, geçici sorgulama, yanıt süresini önemli miktarda hello uygulama katmanı ve hello Azure SQL veritabanı katmanı arasındaki ağ iletişimi harcanmaktadır. Bile her ikisi de hello zaman aynı veri merkezinde, hello ağ gecikmesi hello iki arasında çok sayıda veri erişim işlemleri tarafından büyütülmüş hello uygulama ve Azure SQL veritabanı arasındadır. tooreduce hello ağ gidiş dönüşleri hello veri erişim işlemleri, hello seçeneği tooeither toplu hello geçici sorgular veya toocompile kullanmayı bunları saklı yordamlar. Merhaba geçici sorguları toplu, tek seyahat tooAzure SQL veritabanı bir büyük toplu olarak birden çok sorgu gönderebilirsiniz. Saklı yordamdaki geçici sorgular derleme varsa bunları toplu olarak aynı neden hello elde. Saklı yordam ayrıca hello kullanabilmeniz için Azure SQL veritabanında hello sorgu planları önbelleğe alma hello olasılığını artırmak yararı hello verir kullanarak yeniden saklı yordamı.

Bazı uygulamalar yazma yoğunluklu. Bazen toobatch birlikte yazılma dikkate alarak bir veritabanı hello toplam g/ç yükünü azaltabilir. Genellikle, bu saklı yordamları ve geçici toplu otomatik tamamlama işlemlerini yerine açık işlemleri kullanmanız yeterlidir. Kullanabileceğiniz farklı teknikleri değerlendirme için bkz: [teknikleri Azure SQL veritabanı uygulamaları için toplu işleme](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Toplu işleme için kendi iş yükü toofind hello sağ modeli deneme. Bir model olabilir emin toounderstand olması biraz farklı işlem tutarlılığı garanti altına alır. Kaynak kullanımını en aza indiren hello sağ iş yükü bulma tutarlılık ve performans dengelemeler doğru bileşimini hello bulma gerektirir.

### <a name="application-tier-caching"></a>Uygulama katmanı önbelleğe alma
Bazı veritabanı uygulamaları okuma yoğun iş yükleri vardır. Katmanlar önbelleğe alma hello veritabanında hello yük ve potansiyel olarak hello performans düzeyi gerekli toosupport bir veritabanını Azure SQL veritabanı kullanarak azaltmak. İle [Azure Redis önbelleği](https://azure.microsoft.com/services/cache/), okuma ağır iş yükü varsa, bir kez hello veri okuma (ya da belki nasıl yapılandırıldığına bağlı olarak bir kez uygulama katmanı makine başına,), SQL veritabanınızın dışındaki verileri depolamak ve. Bu şekilde tooreduce veritabanı Yükü (CPU ve okuma g/ç), ancak işlem tutarlılığı üzerinde bir etkisi hello önbellekten okunan hello verileri eşitlenmemiş hello veritabanındaki hello verilerle olabileceğinden. Birçok uygulamada belirli bir düzeyde tutarsızlık kabul edilebilir olmasına rağmen tüm iş yükleri için geçerli değildir. Bir uygulama katmanı önbelleğe alma stratejisi uygulamadan önce herhangi bir uygulama gereksinimi tam olarak anlamanız gerekir.

## <a name="next-steps"></a>Sonraki adımlar
* Hizmet katmanları hakkında daha fazla bilgi için bkz: [SQL Database seçenekleri ve performansı](sql-database-service-tiers.md)
* Esnek havuzları hakkında daha fazla bilgi için bkz: [Azure bir esnek havuz nedir?](sql-database-elastic-pool.md)
* Performans ve esnek havuzları hakkında daha fazla bilgi için bkz: [zaman tooconsider bir esnek havuz](sql-database-elastic-pool-guidance.md)

