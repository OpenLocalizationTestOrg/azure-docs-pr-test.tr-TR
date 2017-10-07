---
title: "Azure SQL veritabanında aaaMonitoring veritabanı performansı | Microsoft Docs"
description: "Azure araçlarını ve dinamik yönetim görünümlerini kullanarak veritabanınızı izleme hello seçenekleri hakkında bilgi edinin."
keywords: "veritabanı izleme, bulut veritabanı performansı"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: a2e47475-c955-4a8d-a65c-cbef9a6d9b9f
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: b13771183d4ccf37f58e2fc518b9b14de38212dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-database-performance-in-azure-sql-database"></a>Azure SQL Database'de veritabanı performansını izleme
Azure SQL veritabanında Hello performansının izlenmesi hello kaynak kullanım göreli toohello düzeyi, seçtiğiniz veritabanı performans izleme ile başlar. İzleme yardımcı olur, veritabanınızın gerekenden fazla kapasiteye sahip veya çıkışı kaynak kullanımının çünkü zorlanıyor belirlemek ve ardından saat tooadjust hello performans düzeyi olup olmadığına karar vermek ve [hizmet katmanı](sql-database-service-tiers.md) veritabanınızın. Grafik araçları hello kullanarak veritabanını izleyebilirsiniz [Azure portal](https://portal.azure.com) veya SQL kullanarak [dinamik yönetim görünümlerini](https://msdn.microsoft.com/library/ms188754.aspx).

## <a name="monitor-databases-using-hello-azure-portal"></a>Hello Azure portalını kullanarak veritabanlarını izleme
Merhaba, [Azure portal](https://portal.azure.com/), tek veritabanlarının kullanımını veritabanınızı seçip hello tıklayarak izleyebilirsiniz **izleme** grafik. Bu işlem sonrasında bir **ölçüm** hello tıklatarak değiştirebilirsiniz penceresi **grafiği Düzenle** düğmesi. Ölçümleri aşağıdaki hello ekleyin:

* CPU yüzdesi
* DTU yüzdesi
* Veri G/Ç yüzdesi
* Veri boyutu yüzdesi

Bu ölçümleri ekledikten sonra tooview devam edebilirsiniz hello bunları **izleme** hello hakkında daha fazla ayrıntı içeren grafik **ölçüm** penceresi. Dört ölçümün tümü hello ortalama kullanım yüzdesi göreli toohello Göster **DTU** veritabanınızın. Merhaba bkz [hizmet katmanları](sql-database-service-tiers.md) makale Dtu'lar hakkında ayrıntılı bilgi için.

![Hizmet katmanına göre veritabanı performansını izleme.](./media/sql-database-service-tiers/sqldb_service_tier_monitoring.png)

Merhaba performans ölçümleri uyarıları da yapılandırabilirsiniz. Merhaba tıklatın **uyarı Ekle** hello düğmesini **ölçüm** penceresi. Merhaba Sihirbazı tooconfigure Uyarınız izleyin. Merhaba ölçümleri belirli bir eşiği aşması veya hello ölçüm belirli bir eşiğin altına düşerse hello seçeneği tooalert sahip.

Örneğin, hello iş yükü, veritabanı toogrow bekliyorsanız, tooconfigure bir e-posta uyarı seçebilirsiniz, veritabanınızı % 80'hello performans ölçümleri hiçbirinde eriştiğinde. Ne zaman tooswitch toohello sonraki daha yüksek performans düzeyine sahip olmayabilirsiniz çıkışı erken bir uyarı toofigure olarak kullanabilirsiniz.

Merhaba performans ölçümleri mümkün toodowngrade tooa daha düşük performans düzeyine olup olmadıklarını belirlemek de yardımcı olabilir. Standart S2 veritabanını kullandığınızı ve veritabanı ortalama hello tüm performans ölçümleri Göster % 10'dan daha fazla belirli bir zamanda kullanmaz varsayalım. Merhaba veritabanının standart S1'de iyi çalışır olasıdır. Ancak, ani değişiklik veya dalgalanma hello karar toomove tooa daha düşük performans düzeyine yapmadan önce iş yüklerini farkında olun.

## <a name="monitor-databases-using-dmvs"></a>DMV'leri kullanarak veritabanlarını izleme
Merhaba hello portalda kullanıma sunulan ölçümler aynı de sistem görünümleri aracılığıyla kullanılabilir: [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) hello mantıksal olarak **ana** veritabanı sunucunuzun ve [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) hello kullanıcı veritabanında. Kullanım **sys.resource_stats** daha uzun bir süre toomonitor daha az ayrıntılı veri gerekiyorsa. Kullanım **sys.dm_db_resource_stats** toomonitor ihtiyacınız varsa daha küçük bir zaman çerçevesi içinde daha ayrıntılı veri. Daha fazla bilgi için bkz. [Azure SQL Database Performans Rehberi](sql-database-single-database-monitor.md#monitor-resource-use).

> [!NOTE]
> **sys.dm_db_resource_stats**, Web ve İşletme sürümü veritabanlarında (bu sürümler kullanımdan kaldırılmıştır) kullanıldığında boş bir sonuç kümesi getirir.
>
>

### <a name="monitor-resource-use"></a>Kaynak kullanımını izleme

Kaynak kullanım kullanarak izleyebilirsiniz [SQL veritabanı sorgu performansı öngörüleri](sql-database-query-performance.md) ve [Query Store](https://msdn.microsoft.com/library/dn817826.aspx).

Bu iki görünüm kullanarak kullanımı da izleyebilirsiniz:

* [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx)
* [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx)

#### <a name="sysdmdbresourcestats"></a>sys.dm_db_resource_stats
Merhaba kullanabilirsiniz [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) her SQL veritabanını görünümünde. Merhaba **sys.dm_db_resource_stats** görünüm son kaynak kullanım verileri göreli toohello hizmet katmanı gösterir. Ortalama CPU, veri g/ç, günlük yazma ve bellek yüzdelerini 15 dakikada kaydedilir ve 1 saat boyunca saklanır.

Bu görünüm kaynak kullanımını daha ayrıntılı bir bakış sağladığından, kullanın **sys.dm_db_resource_stats** tüm geçerli durumu çözümleme için ilk ya da sorun giderme. Örneğin, bu sorgu hello ortalama ve en yüksek kaynak hello geçerli veritabanı için hello son bir saat gösterilmektedir:

    SELECT  
        AVG(avg_cpu_percent) AS 'Average CPU use in percent',
        MAX(avg_cpu_percent) AS 'Maximum CPU use in percent',
        AVG(avg_data_io_percent) AS 'Average data I/O in percent',
        MAX(avg_data_io_percent) AS 'Maximum data I/O in percent',
        AVG(avg_log_write_percent) AS 'Average log write use in percent',
        MAX(avg_log_write_percent) AS 'Maximum log write use in percent',
        AVG(avg_memory_usage_percent) AS 'Average memory use in percent',
        MAX(avg_memory_usage_percent) AS 'Maximum memory use in percent'
    FROM sys.dm_db_resource_stats;  

Diğer sorgular için hello örneklere bakın [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx).

#### <a name="sysresourcestats"></a>sys.resource_stats
Merhaba [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) hello görünümünde **ana** veritabanının bulunduğu SQL veritabanınızın belirli hizmet katmanını ve performans düzeyinde hello performansını izlemenize yardımcı olacak ek bilgiler . Merhaba veriler her 5 dakikada bir toplanan ve yaklaşık 35 gün boyunca tutulur. Bu görünüm, SQL veritabanınız kaynakları nasıl kullandığını, daha uzun vadeli bir geçmiş analize kullanışlıdır.

Merhaba aşağıdaki grafik Itanium tabanlı sistemler için hello CPU kaynak kullanımı hello P2 performans düzeyine sahip bir Premium veritabanı için her bir saat için bir hafta içinde gösterir. Bu grafik Pazartesi günü başlar, 5 iş günlerini gösterir ve hafta sonu gösterir, hello uygulaması üzerinde çok az olur.

![SQL veritabanı kaynak kullanımı](./media/sql-database-performance-guidance/sql_db_resource_utilization.png)

Merhaba verileri, bu veritabanı şu anda en yüksek CPU yükünü sahip yüzde 50'ten sadece CPU kullanımı göreli toohello P2 performans düzeyi (Öğle saati Salı günü). CPU hello uygulamanın kaynak profilinde hello baskın faktörü ise, P2 hello iş yükü her zaman hello performans düzeyi tooguarantee uygun doğru olduğunu karar verebilirsiniz. Zaman içinde bir uygulama toogrow bekliyorsanız, hello uygulama herhangi bir zamanda hello performans düzeyi sınırına ulaştığında değil iyi bir fikir toohave bir ek kaynak arabellek, böylelikle. Merhaba performans düzeyini artırmak için bir veritabanı yeterli güç tooprocess istekleri özellikle gecikme süresine duyarlı ortamlarında etkili bir şekilde sahip olmadığında ortaya çıkabilir müşteri görünür hataları önlemenize yardımcı olur. Örnek Web sayfalarını veritabanı çağrılarını hello sonuçlarına dayalı boyar uygulamanın destekleyen bir veritabanıdır.

Diğer uygulama türleriyle aynı farklı grafik hello yorumlayabilir. Örneğin, bir uygulama tooprocess bordro verileri her gün çalışır ve olan hello aynı grafik, "toplu" modelinin bu tür P1 performans düzeyi ince uygulayabilirsiniz. Merhaba P1 performans düzeyi 100 karşılaştırıldığında Dtu'lar too200 Dtu'lar P2 performans düzeyi hello sahiptir. Merhaba P1 performans düzeyi hello P2 performans düzeyi yarım hello performansını sağlar. Bu nedenle, yüzde 50 ' P2 CPU kullanımı yüzde 100 CPU P1 kullanımda eşittir. Merhaba uygulaması zaman aşımları yoksa, bir iş 2 saat veya 2.5 saat toofinish sürerse bugün bitti olup olmaması önemli değil. Bu kategorideki bir uygulama, büyük olasılıkla P1 performans düzeyi kullanabilirsiniz. Böylece tüm "büyük yoğun" Merhaba troughs birine daha sonra hello gün içinde sığdırmaya kaynak kullanımının düşük olduğunda hello gün sırasında süreler olduğunu hello olayının avantajından yararlanabilirsiniz. Merhaba işleri her gün saat bitirebilirsiniz sürece hello P1 performans düzeyi için bu türden uygulamasının (ve tasarruf) iyi olabilir.

Azure SQL veritabanı çıkarır tüketilen hello etkin her veritabanı için kaynak bilgileri **sys.resource_stats** hello görünümünü **ana** her sunucu veritabanında. Merhaba tablosunda Hello veri için 5 dakikalık aralıklarla toplanır. Bu verileri neredeyse gerçek zamanlı analiz yerine geçmiş çözümleme için daha yararlı olacak şekilde hello temel, standart ve Premium hizmet katmanları ile Merhaba verileri birden çok 5 dakika tooappear hello tabloda alabilir. Sorgu hello **sys.resource_stats** toosee hello bir veritabanı ve gerektiğinde istediğiniz hello performans teslim olup hello ayırma seçtiğiniz toovalidate yakın zamandaki geçmişini görüntüle.

> [!NOTE]
> Bağlı toohello olmalıdır **ana** , mantıksal SQL veritabanı sunucusu tooquery veritabanı **sys.resource_stats** örnek hello içinde.
> 
> 

Bu örnek nasıl hello verileri bu görünümde gösterilen gösterir:

    SELECT TOP 10 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Merhaba sys.resource_stats Katalog görünümü](./media/sql-database-performance-guidance/sys_resource_stats.png)

Merhaba sonraki örnek, hello kullanabileceğiniz farklı yolları gösterir **sys.resource_stats** katalog SQL veritabanınız kaynakları nasıl kullandığı hakkında tooget bilgileri görüntüle:

1. Geçen haftaki kaynak hello adresindeki toolook hello veritabanı userdb1 kullanın, bu sorguyu çalıştırabilirsiniz:
   
        SELECT *
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND
              start_time > DATEADD(day, -7, GETDATE())
        ORDER BY start_time DESC;
2. İş yükünüzün uygun hello performans düzeyine ne kadar iyi tooevaluate, gereksinim duyduğunuz toodrill aşağı hello kaynak ölçümleri her yönden: CPU, okuma, yazma, çalışan sayısı ve oturum sayısı. İşte bir düzeltilmiş kullanarak sorgu **sys.resource_stats** tooreport hello ortalama ve en yüksek değerleri bu kaynak ölçümleri:
   
        SELECT
            avg(avg_cpu_percent) AS 'Average CPU use in percent',
            max(avg_cpu_percent) AS 'Maximum CPU use in percent',
            avg(avg_data_io_percent) AS 'Average physical data I/O use in percent',
            max(avg_data_io_percent) AS 'Maximum physical data I/O use in percent',
            avg(avg_log_write_percent) AS 'Average log write use in percent',
            max(avg_log_write_percent) AS 'Maximum log write use in percent',
            avg(max_session_percent) AS 'Average % of sessions',
            max(max_session_percent) AS 'Maximum % of sessions',
            avg(max_worker_percent) AS 'Average % of workers',
            max(max_worker_percent) AS 'Maximum % of workers'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
3. Bu her kaynak ölçümü ile Merhaba ortalama ve en yüksek değerleri hakkında bilgi yükünüzü seçtiğiniz hello performans düzeyi ne kadar iyi uyduğunu değerlendirebilirsiniz. Genellikle, değerleri ortalama **sys.resource_stats** iyi temel toouse hello hedef boyutu karşı verin. Birincil ölçüm çubuğu olmalıdır. Bir örnek için hello standart hizmet katmanında S2 performans düzeyiyle kullanıyor olabilir. Merhaba ortalama CPU ve g/ç okuma yüzdeleri kullanın ve yazma 40 oranın altında olan, hello çalışanları 50 sayısıdır ve hello ortalama oturum sayısını 200. İş yükünüzün S1 performans düzeyine hello uygun. Veritabanınızı hello çalışan ve oturumu sınırlarını uygun olup olmadığını kolay toosee var. tooCPU, okuma ve yazma işlemleri, bir veritabanı içine daha düşük bir performans düzeyine olup olmadığını uygun tahminini toosee hello daha düşük performans düzeyine hello DTU sayısı, geçerli performans düzeyini DTU sayı hello tarafından bölmek ve ardından hello sonucu 100 ile çarpın:
   
    **S1 DTU / S2 DTU * 100 = 20 / 50 * 100 = 40**
   
    Merhaba, yüzde cinsinden hello iki performans düzeyleri arasında hello göreli performans farkı sonucudur. Kaynak kullanımınız bu miktar aşmadığından, iş yükünüzü hello daha düşük performans düzeyine uygun. Ancak, kaynak kullanım değerleri olan tüm aralıklarını adresindeki toolook gerekir ve yüzde olarak, veritabanının yükünüzü hello daha düşük performans düzeyine ne sıklıkta uyar belirler. Merhaba aşağıdaki sorguyu kaynak boyutu, 40 oranında Biz bu örnekte, hesaplanan hello eşik göre başına yüzde hello sığacak çıkarır:
   
        SELECT
            (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log Write Fit Percent'
            ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 40 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical Data IO Fit Percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Veritabanı Hizmet düzeyi hedefi (SLO) bağlı olarak, iş yükünüzü hello daha düşük performans düzeyine uygun olup olmadığını karar verebilirsiniz. Veritabanının yükünüzü SLO yüzde 99,9 ise ve hello önceki sorgu değerlerinin tüm üç kaynak boyutları için yüzde 99,9 büyük döndürür, büyük olasılıkla, iş yükü hello daha düşük performans düzeyine sığar.
   
    Ayrıca uygun hello yüzdesiyle arayan olup, SLO toohello sonraki daha yüksek performans düzeyi toomeet taşımalısınız içine Insight sağlar. Örneğin, geçen hafta CPU kullanımını hello için aşağıdaki hello userdb1 gösterir:
   
   | Ortalama CPU yüzdesi | En fazla CPU yüzdesi |
   | --- | --- |
   | 24.5 |100.00 |
   
    Merhaba sınırı iyi hello performans düzeyini hello veritabanı uyar hello performans düzeyinin çeyreği Hello ortalama CPU hakkındadır. Ancak bu hello veritabanı hello performans düzeyinin hello sınıra ulaşana hello en büyük değeri gösterir. Toomove toohello sonraki daha yüksek performans düzeyi gerekiyor mu? Ne birçok kez iş yükü ulaştığında yüzde 100 arayın ve ardından tooyour veritabanı iş yükü SLO karşılaştırın.
   
        SELECT
        (COUNT(database_name) - SUM(CASE WHEN avg_cpu_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'CPU fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_log_write_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Log write fit percent'
        ,(COUNT(database_name) - SUM(CASE WHEN avg_data_io_percent >= 100 THEN 1 ELSE 0 END) * 1.0) / COUNT(database_name) AS 'Physical data I/O fit percent'
        FROM sys.resource_stats
        WHERE database_name = 'userdb1' AND start_time > DATEADD(day, -7, GETDATE());
   
    Bu sorgu bir değer döndürürse yüzde 99,9'den az hello üç kaynak boyutlardan herhangi birinde için ya da taşıma toohello sonraki daha yüksek performans düzeyi göz önünde bulundurun veya uygulama ayarlamayı teknikleri tooreduce hello yük hello SQL database kullanın.
4. Bu alıştırmada ayrıca Merhaba, tahmini iş yükü artış gelecekteki göz önünde bulundurur.

Esnek havuzlar için bu bölümde açıklanan hello teknikleri ile Merhaba havuzdaki tek veritabanlarını izleyebilirsiniz. Ancak hello havuzu bir bütün olarak da izleyebilirsiniz. Bilgi için bkz. [Elastik havuz izleme ve yönetme](sql-database-elastic-pool-manage-portal.md).


### <a name="maximum-concurrent-requests"></a>Maksimum eşzamanlı istek
toosee hello eşzamanlı istek sayısı bu Transact-SQL sorgusu SQL veritabanınızda çalıştırın:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R

bir şirket içi SQL Server veritabanının tooanalyze hello iş yükü değiştirmek bu sorgu toofilter hello belirli veritabanında tooanalyze istiyor. Örneğin, Veritabanım adlı bir şirket içi veritabanınız varsa, bu Transact-SQL sorgusu bu veritabanında eşzamanlı istek Merhaba sayımını döndürür:

    SELECT COUNT(*) AS [Concurrent_Requests]
    FROM sys.dm_exec_requests R
    INNER JOIN sys.databases D ON D.database_id = R.database_id
    AND D.name = 'MyDatabase'

Bu, zaman içinde yalnızca tek bir noktada anlık görüntüsüdür. daha iyi, iş yükü ve eş zamanlı istek gereksinimleri anlamak tooget toocollect gerekir zaman içinde birçok örnekleri.

### <a name="maximum-concurrent-logins"></a>En fazla eşzamanlı oturum açma
Kullanıcı ve uygulama desenleri tooget oturumları hello sıklığını hakkında bir fikir analiz edebilirsiniz. Ayrıca, bir test ortamı toomake, bu veya bu makalede aşağıdakiler ele diğer sınırları basarsa değil olduğundan emin gerçek yükleri de çalıştırabilirsiniz. Tek bir sorgu veya dinamik yönetim görünümünü (DMV), eşzamanlı oturum açma sayar gösterebilir veya geçmişi yok.

Birden çok istemci kullanıyorsanız, aynı bağlantı dizesine hello hello hizmeti her oturum açma kimliğini doğrular. 10 kullanıcı aynı anda bağlanıyorsanız, aynı kullanıcı adı ve parola kullanarak tooa veritabanı Merhaba, 10 eşzamanlı oturum açma olacaktır. Bu sınır yalnızca toohello süresi hello oturum açma ve kimlik doğrulama geçerlidir. Merhaba aynı 10 kullanıcılar toohello veritabanı sırayla bağlanıyorsa, eşzamanlı oturum açma sayısı hello hiçbir zaman 1'den büyük olacaktır.

> [!NOTE]
> Şu anda, bu sınır esnek havuzlar toodatabases geçerli değildir.
> 
> 

### <a name="maximum-sessions"></a>En fazla oturum
toosee hello geçerli etkin oturum sayısı bu Transact-SQL sorgusu SQL veritabanınızda çalıştırın:

    SELECT COUNT(*) AS [Sessions]
    FROM sys.dm_exec_connections

Bir şirket içi SQL Server iş yükü analiz etme, belirli bir veritabanı üzerinde hello sorgu toofocus değiştirin. Bu sorgu, tooAzure SQL veritabanını taşımadan düşünüyorsanız hello veritabanı için olası oturum gereksinimlerini belirlemenize yardımcı olur.

    SELECT COUNT(*)  AS [Sessions]
    FROM sys.dm_exec_connections C
    INNER JOIN sys.dm_exec_sessions S ON (S.session_id = C.session_id)
    INNER JOIN sys.databases D ON (D.database_id = S.database_id)
    WHERE D.name = 'MyDatabase'

Yeniden, bu sorguları zaman içinde nokta sayısını döndürür. Zaman içinde birden fazla örnek toplarsanız hello en iyi anlama kullanın, oturumunuz sahip olacaksınız.

SQL veritabanı analize geçmiş istatistikleri oturumlarını hello sorgulayarak alabileceğiniz [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) Görünüm ve hello gözden geçirme **active_session_count** sütun. 
