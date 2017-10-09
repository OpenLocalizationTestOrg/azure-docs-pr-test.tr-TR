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
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="05844-103">SQL veri ambarı geçici tabloları</span><span class="sxs-lookup"><span data-stu-id="05844-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="05844-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="05844-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="05844-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="05844-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="05844-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="05844-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="05844-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="05844-107">[Index][Index]</span></span>
> * <span data-ttu-id="05844-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="05844-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="05844-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="05844-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="05844-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="05844-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="05844-111">Geçici tablolara verileri - özellikle hello Ara sonuçların geçici nerede dönüştürme sırasında işlerken çok yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="05844-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="05844-112">SQL veri ambarı'nda geçici tablolara hello oturum düzeyindedir.</span><span class="sxs-lookup"><span data-stu-id="05844-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="05844-113">Bunlar, bunlar oluşturuldu ve bu oturumu kapattığında otomatik olarak bırakılan yalnızca görünür toohello oturumu var.</span><span class="sxs-lookup"><span data-stu-id="05844-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="05844-114">Uzaktaki Depolama birimi yerine toolocal sonuçları yazıldığından geçici tablolara performans avantajı sunar.</span><span class="sxs-lookup"><span data-stu-id="05844-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="05844-115">Bunlar her yerden ve saklı yordam haricindeki dahil olmak üzere hello oturumu içinde erişilebilir olarak geçici tabloları Azure SQL veritabanından Azure SQL Data Warehouse'da biraz farklı.</span><span class="sxs-lookup"><span data-stu-id="05844-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="05844-116">Bu makalede, geçici tablolar kullanmak için temel kılavuz içerir ve oturum düzeyi geçici tablolara hello ilkeleri vurgular.</span><span class="sxs-lookup"><span data-stu-id="05844-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="05844-117">Bu makalede Hello bilgileri kullanarak yeniden kullanılırlığı ve kodunuzun bakım kolaylığı artırma kodunuzu modülarize etmek yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="05844-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="05844-118">Geçici bir tablo oluştur</span><span class="sxs-lookup"><span data-stu-id="05844-118">Create a temporary table</span></span>
<span data-ttu-id="05844-119">Geçici tablolara tablo adıyla ekleyerek oluşturulur bir `#`.</span><span class="sxs-lookup"><span data-stu-id="05844-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="05844-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="05844-120">For example:</span></span>

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

<span data-ttu-id="05844-121">Geçici tablolara de oluşturulabilir ile bir `CTAS` kullanarak tam olarak aynı yaklaşımı hello:</span><span class="sxs-lookup"><span data-stu-id="05844-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

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
> <span data-ttu-id="05844-122">`CTAS`çok güçlü bir komut ve hello kullanımını işlem günlüğü alanının çok verimli olmanın avantajı ekledi.</span><span class="sxs-lookup"><span data-stu-id="05844-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="05844-123">Geçici tablolara bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="05844-123">Dropping temporary tables</span></span>
<span data-ttu-id="05844-124">Yeni bir oturum oluşturulduğunda, hiçbir geçici tablolar var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="05844-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="05844-125">Ancak, aynı Merhaba, arıyorsanız, saklı geçici bir hello ile oluşturur yordamı aynı adı, tooensure, `CREATE TABLE` deyimleri başarılı basit bir ön varlığı denetimi ile bir `DROP` hello örnek aşağıda olduğu gibi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="05844-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="05844-126">Tutarlılık kodlama için bu iyi bir uygulamadır toouse tablolar ve geçici tablolar için bu deseni olur.</span><span class="sxs-lookup"><span data-stu-id="05844-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="05844-127">Aynı zamanda bir fikir toouse olan `DROP TABLE` bunlarla kodunuzda tamamladığınızda tooremove geçici tablolar.</span><span class="sxs-lookup"><span data-stu-id="05844-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="05844-128">Saklı yordam geliştirme, bu nesnelerin Temizlenen hello yordamı tooensure sonunda birlikte gruplanır oldukça yaygın toosee hello açılan komuttur.</span><span class="sxs-lookup"><span data-stu-id="05844-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="05844-129">Modularizing kodu</span><span class="sxs-lookup"><span data-stu-id="05844-129">Modularizing code</span></span>
<span data-ttu-id="05844-130">Geçici tablolara herhangi bir kullanıcı oturum görülebilir olduğundan, bu uygulama kodunuz modülarize etmek kötü amaçla kullanılan toohelp olabilir.</span><span class="sxs-lookup"><span data-stu-id="05844-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="05844-131">Örneğin, hello aşağıdaki saklı yordamı bir araya istatistiği ada göre önerilen uygulamalar toogenerate hello veritabanındaki tüm istatistiklerini güncelleştirir DDL yukarıdaki hello getirir.</span><span class="sxs-lookup"><span data-stu-id="05844-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

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

<span data-ttu-id="05844-132">Bu aşamada oluştu hello yalnızca hello oluşturma olacak bir saklı yordam yalnızca geçici bir tablo DDL deyimleri ile #stats_ddl oluşturulan eylemdir.</span><span class="sxs-lookup"><span data-stu-id="05844-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="05844-133">Zaten bir oturumu içinde birden çok kez çalıştırırsanız başlayabildiğinden tooensure varsa bu saklı yordam #stats_ddl bırakın.</span><span class="sxs-lookup"><span data-stu-id="05844-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="05844-134">Ancak, olduğundan hiçbir `DROP TABLE` hello saklı yordam tamamlandığında, hello saklı yordamı dışında okuyabilmesini hello saklı yordamı hello sonunda, oluşturulan hello tablo bırakır.</span><span class="sxs-lookup"><span data-stu-id="05844-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="05844-135">SQL veri ambarı'nda diğer SQL Server veritabanları, olası toouse hello oluşturulduğu hello yordamı dışında geçici bir tablo değil.</span><span class="sxs-lookup"><span data-stu-id="05844-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="05844-136">SQL veri ambarı geçici tablolar kullanılabilir **herhangi bir yere** hello oturumu içinde.</span><span class="sxs-lookup"><span data-stu-id="05844-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="05844-137">Bu örnek aşağıda hello olduğu gibi toomore modüler ve yönetilebilir kodu neden olabilir:</span><span class="sxs-lookup"><span data-stu-id="05844-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="05844-138">Geçici Tablo sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="05844-138">Temporary table limitations</span></span>
<span data-ttu-id="05844-139">SQL veri ambarı birkaç sınırlama geçici tablolara uygularken zorunlu tuttukları.</span><span class="sxs-lookup"><span data-stu-id="05844-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="05844-140">Şu anda yalnızca oturum kapsamlı geçici tablolar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="05844-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="05844-141">Genel geçici tablolar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="05844-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="05844-142">Ayrıca, geçici tablolarda görünümlere oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="05844-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05844-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05844-143">Next steps</span></span>
<span data-ttu-id="05844-144">toolearn daha hello makalelere bakın üzerinde [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Tablo dizin][Index], [bir tablo bölümleme] [ Partition] ve [ Tablo istatistikleri koruma][Statistics].</span><span class="sxs-lookup"><span data-stu-id="05844-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="05844-145">En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="05844-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
