---
title: "SQL veri ambarı aaaPartitioning tablolarda | Microsoft Docs"
description: "Azure SQL Data Warehouse'da tablo bölümleme ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a>SQL veri ambarı tablolarda bölümlendirme
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

Bölümleme tüm SQL veri ambarı tablo türlerinde desteklenir; Kümelenmiş columnstore, kümelenmiş dizin ve yığın dahil.  Bölümlendirme, karma veya dağıtılmış hepsini dahil olmak üzere tüm dağıtım türlerinde de desteklenir.  Bölümleme bölümleme daha küçük gruplar veri ve çoğu durumda, verilerinizi bir tarih sütunu yapılır toodivide sağlar.

## <a name="benefits-of-partitioning"></a>Bölümleme avantajları
Bölümleme veri Bakım ve sorgu performansını yararlı olabilir.  Olup hem veya yalnızca bir avantaj verilerin nasıl yüklendiği ve bölümleme yalnızca bir sütun üzerinde yapılabilir beri hello aynı sütuna iki amaçlar için kullanılıp kullanılamayacağını bağımlıdır.

### <a name="benefits-tooloads"></a>Avantajları tooloads
SQL veri ambarı'nda bölümleme hello birincil yararı olduğu hello verimliliği ve bölüm silme işlemini kullanarak verileri yüklenirken, değiştirme ve birleştirme performansını artırır.  Çoğu durumda bir tarihte verileri bölümlenen toohello sırası hello veri yüklenen toohello veritabanı yakından sütuna bağlıdır.  İşlem günlüğü kaçınma hello bölümleri toomaintain veri kullanımının hello en büyük avantajlarından biri.  Yalnızca ekleme, güncelleştirme veya verileri silme küçük bir düşünce ve çaba, hello en kolay yaklaşım olabileceği yükleme işlemi sırasında bölümleme kullanılarak önemli ölçüde performansı artırabilir.

Bölüm geçiş kullanılan tooquickly Kaldır yüklenebilir veya bir tablonun bölümünü değiştirmek.  Örneğin, satış olgu tablosunun son 36 ay hello için yalnızca verileri içerebilir.  Her ayın Hello sonunda hello satış verileri eski ayın hello tablosundan silindi.  Bu veriler, en eski ay Merhaba bir delete deyimi toodelete hello verileri kullanarak silinemedi.  Ancak, büyük miktarda veri-satır delete deyimi ile silme çok uzun zaman yanı bir sorun yaşanırsa, uzun süre toorollback ele geçirebilir büyük işlemleri hello riskini oluşturun.  Daha iyi yaklaşımı toosimply açılan hello en eski veri bölümdür.  Burada, hello tek tek satırları silme saat ele geçirebilir bölümünün tamamını silme saniye sürebilir.

### <a name="benefits-tooqueries"></a>Avantajları tooqueries
Bölümleme kullanılan tooimprove sorgu performansını da olabilir.  Bir sorgu bölümlenmiş bir sütunda bir filtre geçerliyse, bu bir çok daha küçük veri alt kümesini tam tablo taraması önleme hello olabilen bölümleri niteleme hello tarama tooonly hello sınırlayabilirsiniz.  Merhaba giriş kümelenmiş columnstore dizinleri hello koşul eleme performans avantajı daha az faydalı bağlıdır, ancak bazı durumlarda olabilir avantajı tooqueries.  Merhaba satış Olgu Tablosu 36 hello satış tarihi alanını kullanarak ay bölümlenmiş, örneğin, ardından hello satış tarihte filtre sorguları hello filtre eşleşmeyen bölümlerinde arama atlayabilirsiniz.

## <a name="partition-sizing-guidance"></a>Bölüm boyutlandırma kılavuzluğu
Bölümleme sırasında kullanılan tooimprove performans içeren bir tablo oluşturma bazı senaryolar olabilir **çok fazla** bölümleri bazı koşullarda performans ölçeklenme.  Bu sorunları için kümelenmiş columnstore tabloları özellikle doğrudur.  Toobe yararlı bölümleme için önemli toounderstand olduğu zaman toouse bölümlendirme ve hello sayısı bölümleri toocreate.  Var. toohow olarak sabit bir hızlı kural yok birçok bölüm çok fazla, verilerinizde bağlıdır ve kaç tane bölümler toosimultaneously yüklüyorsunuz.  Ancak genel altın kural, 10'luk ekleme düşündüğünüz bölümlerinin değil 1000'lik too100s.

Üzerinde bölümleme oluştururken **kümelenmiş columnstore** tablolar, satır sayısını her bölüm güden önemli tooconsider değil.  Dağıtım ve bölüm başına 1 milyon satır en az, en iyi sıkıştırma ve kümelenmiş columnstore tabloları performansını için gereklidir.  Bölümler oluşturulmadan önce SQL veri ambarı her tablo 60 dağıtılmış veritabanlarına zaten böler.  Herhangi bir bölümleme eklenen tooa Tablo ayrıca hello arka planda oluşturulan toohello dağıtımları olur.  Bu örnekte, Hello satış Olgu Tablosu 36 aylık bölümleri içeriyordu ve SQL Data Warehouse 60 dağıtımları sahip o aylar yerleştirildiğinde tablo 60 milyon satır aylık veya 2.1 milyon satır içermelidir satış olgu hello kullanıyor.  Bir tablo hello önerilen minimum bölüm başına satır sayısı çok önemli ölçüde daha az satır içeriyorsa, daha az bölümleri sipariş toomake artış hello bölüm başına satır sayısı kullanmayı düşünün.  Ayrıca bkz. hello [dizin] [ Index] Itanium tabanlı sistemler için SQL Data Warehouse tooassess hello kalitesi küme columnstore dizinleri, üzerinde çalışan sorguları içerir makale.

## <a name="syntax-difference-from-sql-server"></a>SQL Server sözdizimi farkı
SQL veri ambarı SQL Server'dan biraz farklıdır basitleştirilmiş bir bölüm tanımı tanıtır.  SQL Server'da olduğu gibi SQL veri ambarı'nda bölümleme işlevleri ve şeması kullanılmaz.  Bunun yerine, tüm toodo gereken budur bölümlenmiş sütun ve hello sınır noktaları tanımlar.  Bölümleme hello sözdizimi SQL Server'dan biraz farklı olabilir, ancak hello temel kavramları şunlardır hello aynı.  SQL Server ve SQL Data Warehouse aralıklı bölüm olabilir tablo başına bir bölüm sütunu destekler.  Bölümlendirme, hakkında daha fazla toolearn bkz [bölümlenmiş tablolar ve dizinler][Partitioned Tables and Indexes].

bölümlenmiş bir SQL veri ambarı örneği aşağıda Hello [CREATE TABLE] [ CREATE TABLE] deyimi, bölümler hello OrderDateKey sütun hello Factınternetsales tablosunda:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a>SQL Server'dan bölümleme geçirme
toomigrate SQL Server veri ambarı tanımları tooSQL yalnızca bölüm:

* SQL Server Hello ortadan [bölüm düzeni][partition scheme].
* Merhaba eklemek [bölümleme işlevi] [ partition function] tanımı tooyour tablo oluştur.

Bölümlenmiş bir tablodaki bir SQL Server örneği hello SQL aşağıda geçiş durumunda toointerrogate hello her bölüm satır sayısı yardımcı olabilir.  Merhaba aynı bölümleme ayrıntı SQL Data Warehouse kullanılırsa, bölüm başına satır sayısı hello 60 faktörüyle düşürür aklınızda bulundurun.  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a>İş yükü yönetimi
Bir son parçası göz önünde bulundurarak toofactor toohello tablo bölüm karar içinde olduğu [iş yükü Yönetim][workload management].  SQL veri ambarı iş yükü yönetiminde öncelikle hello bellek ve eşzamanlılık yönetimidir.  SQL veri ambarı hello tooeach dağıtım sorgu yürütme sırasında ayrılan en fazla bellek yönetilen kaynak sınıfları ' dir.  İdeal olarak, bölümler hello bellek gereksinimlerini kümelenmiş columnstore dizinleri oluşturma gibi diğer faktörlere söz konusu boyutta.  Daha fazla bellek ayırırken columnstore dizinleri avantajı büyük ölçüde kümelenmiş.  Bu nedenle, bir bölüm dizini yeniden tooensure bellek gerek duyuldu değil isteyeceksiniz. Merhaba kullanılabilir tooyour sorgu elde edilebilir hello varsayılan rol, smallrc, tooone, geçiş tarafından bellek miktarını artırmayı hello largerc gibi diğer rolleri.

Dağıtım başına bellek hello ayrılması hakkında bilgi hello kaynak İdarecisi dinamik yönetim görünümlerini sorgulayarak kullanılabilir. Gerçekte, bellek ataması hello resimde daha az olur. Ancak, bu veri yönetimi işlemleri için iyi bir bölüm boyutlandırma olduğunda kullanabileceğiniz kılavuzu düzeyi sağlar.  Merhaba bellek ataması hello çok büyük kaynak sınıfı tarafından sağlanan dışında bir bölüm boyutlandırma tooavoid deneyin. Bu şekil, bölümler büyümesine hangi sırayla tooless en iyi sıkıştırma müşteri adayları bellek baskısı hello riskini çalıştırın.

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a>Bölüm değiştirme
SQL veri ambarı geçiş bölme ve birleştirme bölüm destekler. Bu işlevlerin her biri hello kullanarak excuted olan [ALTER TABLE] [ ALTER TABLE] deyimi.

tooswitch bölümleri iki tablo arasında hello bölümleri ilgili sınırlarının hizalama ve hello tablo tanımları eşleştiğinden emin olmalısınız. Denetim kısıtlamalarında kullanılabilir olmadığından bir tablo hello kaynak tablodaki değerleri tooenforce hello aralığı hello içermelidir hello hedef tablo olarak aynı bölüm sınırlar. Merhaba durum bu değilse, hello bölüm meta verileri eşitlenmemiş hello bölüm anahtarı başarısız olur.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Nasıl toosplit verileri içeren bir bölüm
Merhaba en verimli yöntemi toosplit zaten verileri içeren bir bölüm olduğundan toouse bir `CTAS` deyimi. Merhaba bölümlenmiş tabloda kümelenmiş columnstore ise, bölünebilir önce sonra hello tablo bölüm boş olması gerekir.

Her bölümde bir satır içeren bir örnek bölümlenmiş columnstore tablo aşağıdadır:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> Oluşturma hello istatistiği nesnesiyle Biz bu tablo meta veri daha doğru olduğundan emin olun. Biz istatistikleri oluşturma atlarsanız, SQL veri ambarı varsayılan değerleri kullanır. Lütfen istatistikleri ayrıntıları gözden geçirme için [istatistikleri][statistics].
> 
> 

Biz sonra hello satır sayısı için hello kullanarak sorgulama yapabilirsiniz `sys.partitions` Katalog görünümü:

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

Toosplit Bu tablo çalışırsanız şu hata iletisini alırsınız:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Msg 35346, düzey 15, State 1, ALTER PARTITION deyiminin yan tümcesi 44 Satırı Böl Hello bölüm boş olmadığından başarısız oldu.  Merhaba tabloda bir columnstore dizini mevcut olduğunda, yalnızca boş bölümler bölünebilir. Merhaba ALTER PARTITION deyimini yürütmeden, ardından ALTER PARTITION tamamlandıktan sonra hello columnstore dizinini yeniden oluşturmayı önce hello columnstore dizinini devre dışı bırakın.

Ancak, biz kullanabilirsiniz `CTAS` toocreate yeni bir tablo toohold verilerimizi.

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

Merhaba bölüm sınırları hizalı gibi bir anahtar izin verilir. Biz sonradan bölebilirsiniz boş bir bölüm ile bu hello kaynak tablosu bırakır.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Toodo kalan tek şey bizim veri toohello yeni bölüm kullanarak sınırları tooalign `CTAS` ve verilerimizi toohello ana tabloda geçiş

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

Merhaba veri hello hareketini tamamladıktan sonra bir fikir toorefresh hello istatistikleri olduğu hello hedef tablo tooensure üzerinde bunlar doğru bir şekilde hello yeni dağıtım ilgili bölümlerinin hello veri yansıtmak:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Kaynak denetimi bölümleme tablosu
tooavoid tablosu tanımınızı **paslanma** kaynak denetim sisteminiz yaklaşımı izleyerek tooconsider hello isteyebilirsiniz:

1. Bölümlenmiş bir tablodaki olarak ancak hiç bölüm değerlerle Hello tablosu oluşturma

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. `SPLIT`Merhaba tablo hello dağıtım işleminin bir parçası olarak:

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

Bu yaklaşım hello ile kaynak denetimi kodu statik kalır ve hello bölümleme sınır değerleri toobe dinamik izin verilir; Merhaba ambarıyla zamanla gelişen.

## <a name="next-steps"></a>Sonraki adımlar
toolearn daha hello makalelere bakın üzerinde [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Tablo dizin][Index], [tablo istatistikleri koruma] [ Statistics] ve [ Geçici tablolara][Temporary].  En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
