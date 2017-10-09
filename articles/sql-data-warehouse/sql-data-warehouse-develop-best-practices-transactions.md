---
title: "SQL veri ambarı için aaaOptimizing işlemler | Microsoft Docs"
description: "Azure SQL Data Warehouse'da verimli işlem güncelleştirmeleri yazma en iyi uygulama kılavuzunu"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a>İşlemleri SQL Data Warehouse için en iyi duruma getirme
Bu makalede nasıl toooptimize hello uzun düzeyine riskini en aza indirme sırasında işlem kodunuzu performansını açıklanmaktadır.

## <a name="transactions-and-logging"></a>İşlemler ve günlüğe kaydetme
İşlemler, ilişkisel veritabanı altyapısını önemli bileşenidir. SQL veri ambarı işlemleri sırasında veri değişikliği kullanır. Bu işlemler, açık veya örtülü olabilir. Tek `INSERT`, `UPDATE` ve `DELETE` deyimleri örtülü işlemler tüm örnekler verilmiştir. Açık işlemleri açıkça kullanarak bir geliştirici tarafından yazılan `BEGIN TRAN`, `COMMIT TRAN` veya `ROLLBACK TRAN` ve birden çok değişikliği deyimleri birlikte tek bir atomik biriminde bağlı toobe gerektiğinde tipik olarak kullanılır. 

Azure SQL Data Warehouse değişiklikleri toohello veritabanı işlem günlüklerinin kullanarak kaydeder. Her dağıtım kendi işlem günlüğü vardır. İşlem günlüğü yazma otomatik olarak yapılır. Gerekli yapılandırma yoktur. Ancak, bu işlem hello yazma garanti adımında, bir ek yük hello sistemde tanıtır. İşlemsel olarak verimli kodlar yazarak bu etkiyi en aza indirebilirsiniz. İşlemsel olarak verimli kod kapsamlı iki kategoride yer alır.

* Mümkün olduğunda en az günlük yapılardan yararlanın
* Uzun süre çalışan işlemleri kapsamlı toplu tooavoid tekil kullanarak verileri işlemek
* Bir bölüm düzeni büyük değişiklikler tooa verilen bölüm için değiştirme benimsemeyi

## <a name="minimal-vs-full-logging"></a>En az tam günlük kaydı karşılaştırması
Merhaba işlem günlüğü tookeep her satır değişiklik izini kullanacağınız tam olarak günlüğe kaydedilmiş işlemlerin en düşük düzeyde günlüğe kaydedilmiş işlemlerin kapsam ayırma ve yalnızca meta veri değişiklikleri takip edin. Bu nedenle, yalnızca gerekli toorollback hello işlemde hello olay bir hata veya açık bir istekte hello bilgilerini günlüğe kaydetme en az günlük içerir (`ROLLBACK TRAN`). En düşük düzeyde günlüğe kaydedilmiş bir işlemin benzer şekilde boyutlandırılmış tam olarak günlüğe kaydedilmiş bir işlemin daha iyi bilgi hello işlem günlüğünde daha az izlenen olarak gerçekleştirir. Ayrıca, daha az yazma hello işlem günlüğü gitmek için günlük verileri kadar daha az miktarda oluşturulur ve bu nedenle daha fazla g/ç etkilidir.

Merhaba işlem güvenlik sınırları yalnızca oturum açmış toofully operations uygulayın.

> [!NOTE]
> En düşük düzeyde günlüğe kaydedilmiş işlemlerin açık işlemlerde yer alabilir. İzlenen ayırma yapılarında tüm değişiklikler, olası tooroll geri en düşük düzeyde olur işlemleri günlüğe. "En düşük düzeyde" olarak hello değişikliktir toounderstand oturum önemlidir beklemediğiniz oturum değil.
> 
> 

## <a name="minimally-logged-operations"></a>En düşük düzeyde günlüğe kaydedilmiş işlemlerin
Merhaba aşağıdaki işlemleri en düşük düzeyde günlüğe kaydedilmesini yeteneğine sahiptir:

* TABLE AS SELECT OLUŞTURUN ([CTAS][CTAS])
* EKLE... SEÇİN
* DİZİN OLUŞTURMA
* ALTER INDEX YENİDEN OLUŞTURMA
* DROP INDEX
* TRUNCATE TABLE
* TABLO BIRAKMA
* ALTER TABLE SWITCH PARTITION

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> İç veri taşıma işlemleri (gibi `BROADCAST` ve `SHUFFLE`) hello işlem güvenlik sınırı tarafından etkilenmez.
> 
> 

## <a name="minimal-logging-with-bulk-load"></a>Toplu yükleme ile en az günlüğe kaydetme
`CTAS`ve `INSERT...SELECT` olan hem de toplu yükleme işlemleri. Bununla birlikte, her ikisi de hello hedef tablo tanımı tarafından etkilenir ve hello yük senaryoya bağlıdır. Toplu işlemi tam olarak veya en düşük düzeyde oturum varsa açıklayan bir tablo aşağıdadır:  

| Birincil dizin | Yükleme senaryosu | Oturum açma modu |
| --- | --- | --- |
| Yığın |Herhangi biri |**En az** |
| Kümelenmiş dizini |Boş hedef tablo |**En az** |
| Kümelenmiş dizini |Yüklenen satırları hedef var olan sayfaları ile çakışmaması |**En az** |
| Kümelenmiş dizini |Hedef varolan sayfalarında yüklenen satırları çakışıyor |Tam |
| Kümelenmiş Columnstore dizini |Yığın boyutu > hizalı bölüm dağıtım başına 102,400 = |**En az** |
| Kümelenmiş Columnstore dizini |Toplu iş boyutu < 102,400 hizalı bölüm dağıtım başına |Tam |

Bu tooupdate ikincil veya kümelenmemiş dizinleri her zaman tam olarak olacak yazma işlemlerini günlüğe önemlidir.

> [!IMPORTANT]
> SQL veri ambarı 60 dağıtımları sahiptir. Bu nedenle, tüm satırları eşit olarak dağıtılır ve tek bir bölüm giriş, toplu toocontain 6,144,000 satır veya daha büyük toobe en düşük düzeyde gerekir varsayılarak tooa kümelenmiş Columnstore dizini yazılırken günlüğe. Ardından Merhaba tablonun bölümlenme şekli ve bölüm sınırları eklenmekte hello satırları span bile veri dağıtım varsayılarak bölüm sınır başına 6,144,000 satır gerekir. Her bölümde her dağıtım bağımsız olarak en düşük düzeyde hello dağıtım oturum hello INSERT toobe hello 102,400 satır eşiği aşması gerekir.
> 
> 

Kümelenmiş bir dizin ile bir boş olmayan tabloya veri yükleme genellikle tam olarak günlüğe kaydedilen ve en düşük düzeyde oturum satır bir karışımını içerebilir. Kümelenmiş bir dizin sayfalarını dengeli ağacının (b-ağacı) ' dir. Merhaba sayfa tooalready başka bir işlem satırları içeren yazılmakta varsa, bu yazma tam olarak kaydedilir. Merhaba sayfa boşsa, ancak ardından hello yazma toothat sayfa en düşük düzeyde günlüğe kaydedilir.

## <a name="optimizing-deletes"></a>Siler en iyi duruma getirme
`DELETE`tam olarak günlüğe kaydedilen bir işlemdir.  Toodelete büyük miktarda veri bir tablo ya da bir bölüme ihtiyacınız varsa, genellikle daha fazla çok mantıklıdır`SELECT` hello veri en düşük düzeyde günlüğe kaydedilmiş bir işlemin çalıştırılabilir tookeep istiyor.  tooaccomplish Bu, yeni bir tablo ile oluşturmak [CTAS][CTAS].  Oluşturduktan sonra kullanmak [yeniden adlandırma] [ RENAME] tooswap eski tablonuz yeni oluşturulan hello tablosuyla çıkışı.

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a>Güncelleştirmeleri en iyi duruma getirme
`UPDATE`tam olarak günlüğe kaydedilen bir işlemdir.  Çok sayıda tablodaki satırları tooupdate gerekir ya da bir bölüm, genellikle daha verimli toouse gibi en düşük düzeyde günlüğe kaydedilmiş bir işlemin olabilir [CTAS] [ CTAS] toodo şekilde.

Hello dönüştürülmüş tooa tam tablosu güncelleştirmesi aşağıdaki örnekte bırakıldı `CTAS` en az günlük mümkün olmasını sağlayın.

Bu durumda retrospectively indirim tutarı toohello satış hello tabloda ekliyoruz:

```sql
--Step 01. Create a new table containing hello "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> Büyük tabloları yeniden oluşturma, SQL veri ambarı iş yükü yönetimi özelliklerini kullanarak yararlı olabilir. Daha fazla ayrıntı Lütfen toohello iş yükü yönetimi hello bölümünde başvurun [eşzamanlılık] [ concurrency] makalesi.
> 
> 

## <a name="optimizing-with-partition-switching"></a>Bölüm geçiş ile en iyi duruma getirme
Büyük ölçekli değişiklikleri içinde ile karşılaştığı olduğunda bir [tablo bölüm][table partition], sonra da bir bölüm düzeni değiştirme algılama çok yapar. Merhaba, veri değişikliği önemlidir ve aynı sonucu birden çok bölüm, yalnızca hello bölümler yineleme başarır yayılma hello.

Merhaba adımları tooperform bir bölüm anahtarı aşağıdaki gibidir:

1. Boş bir bölüm çıkışı oluşturma
2. Merhaba 'güncelleştirme' CTAS gerçekleştirme
3. Hello mevcut veri toohello tablo dışarı giden geçiş
4. Merhaba yeni verileri geçiş
5. Merhaba verilerini temizle

Ancak, toohelp ilk toobuild bir hello gibi bir yardımcı yordam aşağıdaki ihtiyacımız hello bölümleri tooswitch tanımlayın. 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

Bu yordam, kodu yeniden kullanma en üst düzeye çıkarır ve hello bölüm örnek daha küçük değiştirme tutar.

Aşağıdaki Hello kodu hello beş adımı tam bir bölüm yordamı değiştirme tooachieve bahsedilen gösterir.

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a>Küçük toplu günlüğüyle simge durumuna küçült
Büyük veri değiştirme işlemleri için Itanium tabanlı sistemler için anlamlı toodivide hello işlemi tooscope hello birime öbekleri veya toplu iş duruma getirebilir.

Çalışan bir örnek aşağıda verilmiştir. Merhaba toplu iş boyutu tooa Önemsiz numara toohighlight hello teknik ayarlandı. Gerçekte hello toplu iş boyutu önemli ölçüde daha büyük olabilir. 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a>Duraklatma ve ölçeklendirme Kılavuzu
Azure SQL Data Warehouse, duraklatma, sürdürme ve veri ambarınız isteğe bağlı ölçeği olanak tanır. Duraklatmak veya SQL Data Warehouse ölçeklendirebilir yüklediğinizde yürütülen işlemler hemen sonlandırılır önemli toounderstand olur; Tüm açık hareketleri toobe neden geri alındı. İş yükünüzün uzun süre çalışan ve tamamlanmamış veri değişikliği önceki verilen toohello duraklatma veya ölçeklendirme işlemi, sonra da bu iş geri toobe gerekir. Bu toopause hello süresi etkisi veya Azure SQL Data Warehouse veritabanınızın ölçeğini olabilir. 

> [!IMPORTANT]
> Her ikisi de `UPDATE` ve `DELETE` tam olarak günlüğe kaydedilen işlemleri ve bunlar geri alma/yineleme için işlemleri eşdeğer en düşük düzeyde işlemleri günlüğe daha önemli ölçüde uzun sürebilir. 
> 
> 

Merhaba en iyi senaryo, uçuş veri değiştirme işlemleri tam önceki toopausing veya ölçeklendirme SQL Data Warehouse toolet bulunur. Ancak, bu her zaman pratik olmayabilir. uzun bir geri alma toomitigate hello riskini seçenekleri aşağıdaki hello birini dikkate alın:

* Uzun süre çalışan işlemleri kullanarak yeniden yazma [CTAS][CTAS]
* Merhaba işlemi parçalara bölmek; bir alt hello satır kümesi üzerinde çalışan

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [SQL Data Warehouse işlemlerinde] [ Transactions in SQL Data Warehouse] toolearn yalıtım düzeyleri ve işlem sınırları hakkında daha fazla bilgi.  Diğer en iyi yöntemler genel bakış için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

