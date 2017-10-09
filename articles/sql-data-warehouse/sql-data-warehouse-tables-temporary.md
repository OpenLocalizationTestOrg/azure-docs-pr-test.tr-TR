---
title: "SQL veri ambarı aaaTemporary tablolarda | Microsoft Docs"
description: "Geçici tablolarda Azure SQL Data Warehouse ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a>SQL veri ambarı geçici tabloları
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

Geçici tablolara verileri - özellikle hello Ara sonuçların geçici nerede dönüştürme sırasında işlerken çok yararlı olur. SQL veri ambarı'nda geçici tablolara hello oturum düzeyindedir.  Bunlar, bunlar oluşturuldu ve bu oturumu kapattığında otomatik olarak bırakılan yalnızca görünür toohello oturumu var.  Uzaktaki Depolama birimi yerine toolocal sonuçları yazıldığından geçici tablolara performans avantajı sunar.  Bunlar her yerden ve saklı yordam haricindeki dahil olmak üzere hello oturumu içinde erişilebilir olarak geçici tabloları Azure SQL veritabanından Azure SQL Data Warehouse'da biraz farklı.

Bu makalede, geçici tablolar kullanmak için temel kılavuz içerir ve oturum düzeyi geçici tablolara hello ilkeleri vurgular. Bu makalede Hello bilgileri kullanarak yeniden kullanılırlığı ve kodunuzun bakım kolaylığı artırma kodunuzu modülarize etmek yardımcı olabilir.

## <a name="create-a-temporary-table"></a>Geçici bir tablo oluştur
Geçici tablolara tablo adıyla ekleyerek oluşturulur bir `#`.  Örneğin:

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

Geçici tablolara de oluşturulabilir ile bir `CTAS` kullanarak tam olarak aynı yaklaşımı hello:

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> `CTAS`çok güçlü bir komut ve hello kullanımını işlem günlüğü alanının çok verimli olmanın avantajı ekledi. 
> 
> 

## <a name="dropping-temporary-tables"></a>Geçici tablolara bırakılıyor
Yeni bir oturum oluşturulduğunda, hiçbir geçici tablolar var olmalıdır.  Ancak, aynı Merhaba, arıyorsanız, saklı geçici bir hello ile oluşturur yordamı aynı adı, tooensure, `CREATE TABLE` deyimleri başarılı basit bir ön varlığı denetimi ile bir `DROP` hello örnek aşağıda olduğu gibi kullanılabilir:

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

Tutarlılık kodlama için bu iyi bir uygulamadır toouse tablolar ve geçici tablolar için bu deseni olur.  Aynı zamanda bir fikir toouse olan `DROP TABLE` bunlarla kodunuzda tamamladığınızda tooremove geçici tablolar.  Saklı yordam geliştirme, bu nesnelerin Temizlenen hello yordamı tooensure sonunda birlikte gruplanır oldukça yaygın toosee hello açılan komuttur.

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a>Modularizing kodu
Geçici tablolara herhangi bir kullanıcı oturum görülebilir olduğundan, bu uygulama kodunuz modülarize etmek kötü amaçla kullanılan toohelp olabilir.  Örneğin, hello aşağıdaki saklı yordamı bir araya istatistiği ada göre önerilen uygulamalar toogenerate hello veritabanındaki tüm istatistiklerini güncelleştirir DDL yukarıdaki hello getirir.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

Bu aşamada oluştu hello yalnızca hello oluşturma olacak bir saklı yordam yalnızca geçici bir tablo DDL deyimleri ile #stats_ddl oluşturulan eylemdir.  Zaten bir oturumu içinde birden çok kez çalıştırırsanız başlayabildiğinden tooensure varsa bu saklı yordam #stats_ddl bırakın.  Ancak, olduğundan hiçbir `DROP TABLE` hello saklı yordam tamamlandığında, hello saklı yordamı dışında okuyabilmesini hello saklı yordamı hello sonunda, oluşturulan hello tablo bırakır.  SQL veri ambarı'nda diğer SQL Server veritabanları, olası toouse hello oluşturulduğu hello yordamı dışında geçici bir tablo değil.  SQL veri ambarı geçici tablolar kullanılabilir **herhangi bir yere** hello oturumu içinde. Bu örnek aşağıda hello olduğu gibi toomore modüler ve yönetilebilir kodu neden olabilir:

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a>Geçici Tablo sınırlamaları
SQL veri ambarı birkaç sınırlama geçici tablolara uygularken zorunlu tuttukları.  Şu anda yalnızca oturum kapsamlı geçici tablolar desteklenir.  Genel geçici tablolar desteklenmez.  Ayrıca, geçici tablolarda görünümlere oluşturulamıyor.

## <a name="next-steps"></a>Sonraki adımlar
toolearn daha hello makalelere bakın üzerinde [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Tablo dizin][Index], [bir tablo bölümleme] [ Partition] ve [ Tablo istatistikleri koruma][Statistics].  En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].

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

<!--Other Web references-->
