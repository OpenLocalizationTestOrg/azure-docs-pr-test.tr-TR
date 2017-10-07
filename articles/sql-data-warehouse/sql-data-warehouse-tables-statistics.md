---
title: "SQL veri ambarı tablolarda aaaManaging istatistikleri | Microsoft Docs"
description: "Azure SQL Data Warehouse tablolarda istatistiklerle ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>SQL veri ambarı tablolarda istatistiklerle yönetme
> [!div class="op_single_selector"]
> * [Genel bakış][Overview]
> * [Veri türleri][Data Types]
> * [Dağıt][Distribute]
> * [Dizin][Index]
> * [Bölüm][Partition]
> * [İstatistikleri][Statistics]
> * [Geçici][Temporary]
> 
> 

Merhaba daha fazla SQL Data Warehouse bilir verilerinizle ilgili hello daha hızlı onu verilerinizi sorguları çalıştırabilirsiniz.  SQL Data Warehouse verilerinizi hakkında söyleyen hello yoludur verilerinizle ilgili istatistikleri toplama tarafından.  Verilerinize ilişkin istatistikler sahip bir olduğundan hello en önemli nokta sorgularınızı toooptimize yapabilirsiniz.  İstatistikleri SQL Data Warehouse hello sorgularınızı için en iyi planı oluşturmanıza yardımcı olur.  İyileştirici hello SQL Data Warehouse sorgu iyileştiricisi maliyetidir dayalı olmasıdır.  Diğer bir deyişle, çeşitli sorgu planlarını hello maliyetini karşılaştırır ve ayrıca hello hızlı yürütecek hello planı olmalıdır hello en düşük maliyeti hello planla seçer.

İstatistikleri, birden çok sütun tek bir sütun veya tablo dizini oluşturulabilir.  İstatistikleri hello aralığı ve değerlerin seçiciliği yakalar çubuk grafik içinde depolanır.  İlginizi çeken budur Hello iyileştirici ihtiyacı olduğunda tooevaluate birleşimler, GROUP BY, HAVING ve WHERE sorgu yan tümcelerinde.  Hello iyileştirici tahminleri hello tarih sorgunuzda filtrelemeyi 1 satır döndürür, çok farklı planlama varsa daha da tercih edebilirsiniz örneğin, tarih, tahmin seçmiş 1 milyon satırları döndürür.  İstatistik oluşturma oldukça önemli olmakla birlikte, eşit oranda önemli olan bu istatistikleri *doğru şekilde* Merhaba tablonun hello geçerli durumunu yansıtır.  Güncel istatistikleri olması iyi bir plan hello iyileştiricisi tarafından seçilir sağlar.  Merhaba iyileştiricisi tarafından oluşturulan hello planlar yalnızca verilerinizi hello istatistik kadar iyi olur.

oluşturma ve istatistikleri güncelleştirmeyi hello işlemi şu anda el ile ancak çok basit toodo gelir.  Bu, otomatik olarak oluşturur ve tek sütunları ve dizinleri istatistiklerle güncelleştiren SQL sunucusu benzemez.  Aşağıdaki Hello bilgileri kullanarak, verilerinizi hello istatistikleri hello yönetimini büyük ölçüde otomatikleştirebilirsiniz. 

## <a name="getting-started-with-statistics"></a>İstatistikleri ile çalışmaya başlama
 Her sütunda örneklenen istatistikleri oluşturma kolay bir yolu tooget istatistikleri ile başlatıldı.  Eşit oranda önemli tookeep istatistikleri güncel olduğuna göre koruyucu bir yaklaşım olabilir tooupdate, istatistikleri günlük eşit veya ondan sonra her yük. Dengelemeler performans ve hello maliyet toocreate ve güncelleştirme istatistiklerini arasındaki her zaman vardır.  Tüm, istatistik uzun toomaintain sürüyor bulursanız, hangi sütunların istatistiklerine sahip veya hangi sütunların hakkında daha fazla seçmeli tootry toobe sık sık güncelleştirilmesi gerekmeyen isteyebilirsiniz.  Örneğin, günlük, yeni değerleri eklenebilir gibi yerine her yük sonra tooupdate tarih sütunlarının isteyebilirsiniz. Yeniden, hello çoğu avantajı sütunlarda söz konusu birleşimler, GROUP BY, HAVING istatistikleri sağlayarak elde edersiniz ve WHERE yan tümcelerini.  Çok sayıda içeren bir tablo varsa, yan tümcesi yalnızca hello kullanılan sütunları seçin, bu sütunlar istatistik yardımcı ve biraz daha fazla çaba tooidentify harcama burada istatistikleri yardımcı olur, hello sütunları azaltabilir hello zaman toomaintain, istatistikleri .

## <a name="multi-column-statistics"></a>Birden çok sütun istatistikleri
Ayrıca toocreating istatistikleri tek sütunlarda sorgularınızı çok sütunlu İstatistikler faydalanırsınız bulabilirsiniz.  Çok sütunlu İstatistikler sütun listesini oluşturulan istatistikleri ' dir.  Merhaba listesinde tek sütun istatistikleri hello ilk sütunda içerirler artı bazı arası sütun bağıntı bilgileri densities çağrılır.  Örneğin, iki sütun tooanother katıldığı bir tablo varsa, iki sütun arasında ilişki hello bilirse SQL Data Warehouse daha iyi hello planı iyileştirebilirsiniz bulabilirsiniz.   Çok sütunlu İstatistikler bileşik birleştirmeler ve Grupla gibi bazı işlemleri için sorgu performansını iyileştirebilir.

## <a name="updating-statistics"></a>İstatistikleri güncelleştirme
İstatistikleri güncelleştirmeyi, veritabanı yönetim alışkanlık önemli bir parçasıdır.  Merhaba dağıtım hello veritabanında veri değiştiğinde istatistikleri güncelleştirilmiş toobe gerekir.  Güncel olmayan İstatistikler toosub en iyi sorgu performansını götürür.

Yeni tarihleri eklendikçe bir en iyi tarih sütunlarının tooupdate istatistik günde bir uygulamadır.  Her zaman yeni satırlar hello veri ambarına yüklenir, yeni yükleme veya işlem tarihleri eklenir. Bunlar hello veri dağıtım değiştirin ve hello istatistikleri güncel olun. Buna karşılık, değerlerin Hello dağıtım genellikle değişmez gibi bir müşteri tablosundaki Ülke sütunu istatistiklerle hiçbir zaman güncelleştirilmiş, toobe gerekebilir. Merhaba dağıtım müşterileri arasında sabit olduğunu varsayarak, yeni satır toohello tablosu değişimi ekleme toochange hello veri dağıtım adımıdır değil. Ancak, veri Ambarınızı yalnızca bir ülkede varsa ve yeni bir ülkeden veri Getir depolanmakta, birden fazla ülkede verilerden sonuçta sonra kesinlikle hello Ülke sütunu tooupdate istatistik gerekir.

Bir sorgu sorun giderme olduğunda hello ilk soruları tooask "biri hello istatistikleri güncel?"

Bu soru hello veri hello yaşa göre yanıtlanması biri değil. Yukarı toodate istatistikleri nesneyi veri arka plandaki hiçbir malzeme değişiklik toohello yapıldıysa çok eski olabilir. Merhaba satır sayısını önemli ölçüde değişti veya belirtilen sütun için değerlerin hello dağıtımındaki maddi bir değişiklik olduğunda *sonra* süresi tooupdate istatistikleri değil.  

Başvuru için **SQL Server** (SQL Data Warehouse değil) otomatik olarak bu gibi durumlarda istatistiklerini güncelleştirir:

* Satır eklediğinizde hello tablosunda sıfır satır varsa, bir otomatik güncelleştirme istatistik alacaksınız
* 500'den az satırlarla başlangıç 500'den fazla satır tooa tablo eklediğinizde (örn. başlangıçta 499 sahip ve 500 satır tooa toplam 999 satır ekleme), bir otomatik güncelleştirme alırsınız 
* 500'den fazla satır olduğunuzda hello istatistikleri üzerinde bir otomatik güncelleştirme görürsünüz önce tooadd 500 ek satırlar + Merhaba tablonun hello boyutunun % 20 gerekir

Hiçbir DMV toodetermine olduğundan hello tablo içindeki veri hello son süresi istatistikleri güncelleştirildi oluşturulmasından sonra değiştirilmişse, istatistik hello yaş bilerek, hello resim parçası olan sağlayabilirsiniz.  Toodetermine hello son zamanı, istatistikleri sorgu aşağıdaki hello kullanabileceğiniz her bir tabloda güncelleştirilmiş burada.  

> [!NOTE]
> Verili bir sütunun değerlerini hello dağıtımını maddi bir değişiklik varsa, bunlar güncelleştirildiği son zaman istatistikleri hello bağımsız olarak güncelleştirmeniz gerekir unutmayın.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

Örneğin, bir veri ambarında tarih sütunlarının genellikle istatistikleri güncelleştirmeleri sık. Her zaman yeni satırlar hello veri ambarına yüklenir, yeni yükleme veya işlem tarihleri eklenir. Bunlar hello veri dağıtım değiştirin ve hello istatistikleri güncel olun.  Buna karşılık, bir müşteri tabloda cinsiyetiniz sütun istatistiklerle güncelleştirilmiş toobe hiçbir zaman gerekebilir. Merhaba dağıtım müşterileri arasında sabit olduğunu varsayarak, yeni satır toohello tablosu değişimi ekleme toochange hello veri dağıtım adımıdır değil. Veri ambarınız bir cinsiyeti ve birden çok genders yeni gereksinimi sonuçlarında yalnızca içeriyorsa ancak ardından kesinlikle hello cinsiyetiniz sütun tooupdate istatistik gerekir.

Daha fazla açıklama için bkz: [istatistikleri] [ Statistics] konusuna bakın.

## <a name="implementing-statistics-management"></a>İstatistikleri yönetimini uygulama
İyi bir fikir tooextend görülür adresindeki İstatistikler güncelleştirilir işlem tooensure yüklenirken verilerinizi hello hello yük sonuna. tabloları boyutlarına ve/veya bunların değerleri dağıtımını en sık değiştirdiğinizde hello veri yükü var. Bu nedenle, bu mantıksal yer tooimplement olan bazı yönetim işlemleri.

Bazı temel ilkeler hello yükleme işlemi sırasında İstatistikleri güncelleştirmek için aşağıda verilmiştir:

* Yüklenen her tablo güncelleştirilmiş en az bir istatistik nesnesi olduğundan emin olun. Bu güncelleştirmeleri hello hello istatistikleri güncelleştirme parçası olarak boyutu (satır sayısı ve sayfa sayısı) bilgilerini tablolarını.
* BİRLEŞTİRME, GROUP BY, ORDER BY ve DISTINCT yan tümcelerinde katılan sütunları odaklanmak
* Bu değerleri hello istatistikleri Histogramı dahil edilmeyen daha sık tarihleri "anahtar artan" sütunlarını işlem gibi güncelleştirme göz önünde bulundurun.
* Statik dağıtım sütunları daha az sıklıkla güncelleştirmeyi deneyin.
* Her istatistik nesne serisinde güncelleştirilir unutmayın. Yalnızca uygulama `UPDATE STATISTICS <TABLE_NAME>` - özellikle istatistikleri nesnelerin çok geniş tablolar için uygun olmayabilir.

> [!NOTE]
> [Anahtar artan] hakkında daha fazla ayrıntı için lütfen toohello SQL Server 2014 kardinalite tahmin modeli teknik incelemesine bakın.
> 
> 

Daha fazla açıklama için bkz: [kardinalite tahmin] [ Cardinality Estimation] konusuna bakın.

## <a name="examples-create-statistics"></a>Örnekler: istatistikler oluşturma
Bu örnekler nasıl toouse istatistikleri oluşturmak için çeşitli seçenekler. her sütun için kullandığınız hello seçenekleri verilerinizi hello özelliklerini ve hello sütunu sorguda nasıl kullanılacağını bağlıdır.

### <a name="a-create-single-column-statistics-with-default-options"></a>A. Varsayılan seçeneklerle tek sütunlu istatistikler oluşturma
bir sütunda toocreate istatistikleri, hello istatistikleri nesnesi için ad ve hello sütunun hello adı yalnızca sağlar.

Bu sözdiziminin tüm hello varsayılan seçenekleri kullanır. İstatistikleri oluşturduğunda, varsayılan olarak, SQL Data Warehouse Merhaba tablonun yüzde 20 örnekleri.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

Örneğin:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Her satır inceleyerek tek sütunlu istatistikler oluşturma
Merhaba varsayılan örnekleme oranını yüzde 20 oranında çoğu durumlar için yeterli olur. Bununla birlikte, hello örnekleme hızını ayarlayabilirsiniz.

toosample hello tam tablo, bu söz dizimini kullanın:

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

Örneğin:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Tek sütunlu İstatistikler hello örnek boyutunu belirterek oluşturun.
Alternatif olarak, bir yüzde olarak hello örnek boyutu belirtebilirsiniz:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Tek sütunlu İstatistikler yalnızca bazı hello satırları oluşturma
Başka bir seçenek tablonuzda hello satır bir kısmı istatistikleri oluşturabilirsiniz. Bu filtrelenmiş istatistiği çağrılır.

Örneğin, tooquery büyük bölümlenmiş bir tablodaki belirli bir bölüm planlarken filtrelenmiş istatistik kullanabilirsiniz. İstatistikler yalnızca hello üzerinde bölüm değerleri oluşturmayı tarafından hello istatistikleri hello doğruluğunu artırmak ve bu nedenle sorgu performansını artırmak.

Bu örnek değerleri çeşitli İstatistikler oluşturur. Merhaba değerleri kolayca olabilir değerleri toomatch hello aralığı bir bölümünde tanımlanmış.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Sorgu iyileştiricisi tooconsider hello dağıtılmış sorgu planı seçtiğinde filtrelenmiş istatistik kullanarak hello için hello sorgu hello istatistikleri nesnesinin hello tanımı içinde sığması gerekir. Merhaba önceki örnekte, burada yan tümcesi 2000101 ve 20001231 arasındaki toospecify col1 değerleri gereken hello sorgunun kullanma.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Tüm hello seçeneklerle tek sütunlu istatistikler oluşturma
Elbette, başlangıç seçenekleri birlikte birleştirebilirsiniz. Aşağıdaki Hello örnek filtrelenmiş istatistik nesnesi bir özel örnek boyutu ile oluşturur:

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Merhaba tam başvuru için bkz: [CREATE STATISTICS] [ CREATE STATISTICS] konusuna bakın.

### <a name="f-create-multi-column-statistics"></a>F Çok sütunlu istatistikler oluşturma
toocreate çok sütunlu İstatistikler yalnızca hello önceki örneklerde kullanır, ancak daha fazla sütun belirtin.

> [!NOTE]
> kullanılan hello histogram tooestimate hello sorgu sonucu, satır sayısıdır yalnızca hello istatistikleri nesne tanımı'nda listelenen hello ilk sütun için kullanılabilir.
> 
> 

Bu örnekte, hello histogram açıktır *ürün\_kategori*. Çapraz sütunlu İstatistikler hesaplanır *ürün\_kategori* ve *ürün\_sub_c\ategory*:

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Arasında bir ilişki olduğundan *ürün\_kategori* ve *ürün\_alt\_kategori*, birden çok sütun stat bu sütunları erişilen faydalı olabilir Merhaba, aynı anda.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. Bir tablodaki tüm hello sütunlarda istatistikler oluşturma
Tek yönlü toocreate istatistikleri hello tablosu oluşturduktan sonra tooissues CREATE STATISTICS komutları olur.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. Saklı yordam toocreate istatistikleri veritabanındaki tüm sütunları kullanın
SQL veri ambarı sistem saklı yordam eşdeğer çok yok SQL Server'daki [sp_create_stats] []. Bu saklı yordam istatistikleri zaten yok hello veritabanı her sütunun bir tek sütun istatistikleri nesnesi oluşturur.

Bu, veritabanı tasarımınız ile çalışmaya başlamanıza yardımcı olur. Ücretsiz tooadapt düşünüyorsanız, tooyour gerekir.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

Bu yordam ile Merhaba tablodaki tüm sütunları toocreate istatistik yalnızca hello yordamını çağırın.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Örnekler: istatistikleri güncelleştir
tooupdate istatistikleri, şunları yapabilirsiniz:

1. Bir istatistik Nesne güncelleştirilemiyor. İstatistikleri tooupdate istediğiniz nesne hello Hello adını belirtin.
2. Bir tablodaki tüm istatistikleri nesneleri güncelleştirin. Bir özel istatistikleri nesne yerine Merhaba tablonun Hello adı belirtin.

### <a name="a-update-one-specific-statistics-object"></a>A. Güncelleştirme belirli bir istatistik nesnesi
Sözdizimi tooupdate belirli istatistikleri nesne aşağıdaki hello kullan:

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

Örneğin:

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

Belirli istatistikleri nesneleri güncelleştirerek hello zaman ve kaynak gerekli toomanage istatistikleri en aza indirebilirsiniz. Bu, bazı, yine de toochoose hello en iyi istatistiklerini nesneleri tooupdate zorlayıcı gerektirir.

### <a name="b-update-all-statistics-on-a-table"></a>B. Bir tablodaki tüm istatistikleri güncelleştir
Bu tabloda tüm hello istatistikleri nesnelerini güncelleştirme için basit bir yöntemi gösterir.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

Örneğin:

```sql
UPDATE STATISTICS dbo.table1;
```

Kolay toouse ifadesidir. Yalnızca bu hello tablosundaki tüm istatistiklerini güncelleştirir ve bu nedenle gerekli olandan daha fazla iş gerçekleştirebileceğiniz unutmayın. Merhaba performans sorunu değilse, bu kesinlikle tooguarantee istatistikleri güncel hello en kolay ve eksiksiz yoludur.

> [!NOTE]
> Bir tablodaki tüm istatistikleri güncelleştirirken SQL Data Warehouse bir tarama toosample hello tablo her istatistik desteklemiyor. Merhaba tablonun büyük ise fazla sayıda sütun ve birçok istatistikleri sahipse, gerekli olduğunda bağlı olarak daha verimli tooupdate tek tek istatistikleri olabilir.
> 
> 

Bir uygulama için bir `UPDATE STATISTICS` yordamı Lütfen hello bakın [geçici tablolar] [ Temporary] makalesi. Merhaba uygulama yöntemidir biraz farklı toohello `CREATE STATISTICS` yukarıdaki yordamı hello sonuç ancak aynı hello olduğu.

Merhaba tam sözdizimi için bkz: [Update STATISTICS] [ Update Statistics] konusuna bakın.

## <a name="statistics-metadata"></a>İstatistikleri meta verileri
Çeşitli sistem görünümü ve toofind istatistikleri hakkında bilgi kullanabileceğiniz işlevleri vardır. Örneğin, bir istatistik nesnesi istatistikleri en son oluşturulan veya güncelleştirilen hello istatistikleri tarih işlevi toosee kullanarak güncel olmayabilir, görebilirsiniz.

### <a name="catalog-views-for-statistics"></a>Katalog görünümleri istatistikleri
Bu sistem görünümleri İstatistikler hakkında bilgi sağlar:

| Katalog görünümü | Açıklama |
|:--- |:--- |
| [sys.Columns][sys.columns] |Her sütun için bir satır. |
| [sys.Objects][sys.objects] |Merhaba veritabanında her nesne için bir satır. |
| [sys.schemas][sys.schemas] |Merhaba veritabanındaki her şema için bir satır. |
| [sys.stats][sys.stats] |Her bir istatistik nesne için bir satır. |
| [sys.stats_columns][sys.stats_columns] |Merhaba istatistikleri nesnesindeki her sütun için bir satır. Bağlantılar toosys.columns yedekleyin. |
| [sys.Tables][sys.tables] |(Dış tablolara içerir) her tablo için bir satır. |
| [sys.table_types][sys.table_types] |Her bir veri türü için bir satır. |

### <a name="system-functions-for-statistics"></a>Sistem işlevleri için istatistikleri
Bu sistem işlevler istatistikleri ile çalışmak için yararlıdır:

| Sistem işlevi | Açıklama |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Tarih hello istatistikleri nesnesi son güncelleştirildi. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Merhaba istatistikleri nesnesi tarafından anlaşılan değerlerin hello dağıtımı hakkında özet düzeyi ve ayrıntılı bilgi sağlar. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Bir görünüme istatistikleri sütunları ve işlevlerini birleştirme
Bu görünüm toostatistics ve sonuçları hello [STATS_DATE()] [] işlevinden birlikte ilgili sütunları getirir.

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>DBCC SHOW_STATISTICS() örnekleri
DBCC SHOW_STATISTICS() istatistikleri nesnesi içinde tutulan hello verileri gösterir. Bu veriler üç bölümlerinde gelir.

1. Üstbilgi
2. Yoğunluğu vektör
3. Çubuk grafik

Merhaba istatistiklerde Hello üstbilgi meta veriler. Merhaba histogram hello dağıtım değerlerin hello ilk anahtar sütununa hello istatistikleri nesnesinin görüntüler. Merhaba yoğunluğu vektör arası sütun bağıntı ölçer. SQLDW kardinalite tahminlerde hello istatistikleri nesnesindeki hello verilerin hesaplar.

### <a name="show-header-density-and-histogram"></a>Üstbilgi, yoğunluğu ve histogram Göster
Bu basit bir örnek istatistikleri nesnesinin tüm üç bölümlerini gösterir.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Örneğin:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>DBCC SHOW_STATISTICS() bir veya daha fazla bölümlerini gösterme;
Yalnızca belirli bölümlerini görüntüleme ilgileniyorsanız, hello kullan `WITH` yan tümcesi ve hangi bölümleri belirtin toosee istiyor:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

Örneğin:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>DBCC SHOW_STATISTICS() farklar
DBCC SHOW_STATISTICS() daha kesinlikle SQL Data Warehouse karşılaştırıldığında tooSQL sunucu uygulanır.

1. Belgelenmemiş özellikler desteklenmez
2. Stats_stream kullanamazsınız
3. İstatistik verileri belirli alt kümeleri için sonuçlarını örneğin katılamıyor (STAT_HEADER birleştirme DENSITY_VECTOR)
4. NO_INFOMSGS ileti gizleme için ayarlanamaz
5. İstatistikleri adları köşeli ayraç kullanılamaz
6. Sütun adları tooidentify istatistikleri nesneleri kullanamazsınız
7. Özel hata 2767 desteklenmiyor

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla ayrıntı için bkz: [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] konusuna bakın.  toolearn daha hello makalelere bakın üzerinde [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Tablo dizin][Index], [bir tablo bölümleme] [ Partition] ve [ Geçici tablolara][Temporary].  En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->  
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
