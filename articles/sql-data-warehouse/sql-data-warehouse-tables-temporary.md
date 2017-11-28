---
title: "SQL veri ambarı geçici tablolarda | Microsoft Docs"
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
ms.openlocfilehash: fd8c31a727dae3b011aa8294a81f005bad72a278
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="60ca3-103">SQL veri ambarı geçici tabloları</span><span class="sxs-lookup"><span data-stu-id="60ca3-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="60ca3-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="60ca3-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="60ca3-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="60ca3-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="60ca3-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="60ca3-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="60ca3-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="60ca3-107">[Index][Index]</span></span>
> * <span data-ttu-id="60ca3-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="60ca3-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="60ca3-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="60ca3-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="60ca3-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="60ca3-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="60ca3-111">Geçici tablolara verileri - özellikle Ara sonuçların geçici nerede dönüştürme sırasında işlerken çok yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="60ca3-111">Temporary tables are very useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="60ca3-112">SQL veri ambarı'nda geçici tablolara oturum düzeyindedir.</span><span class="sxs-lookup"><span data-stu-id="60ca3-112">In SQL Data Warehouse temporary tables exist at the session level.</span></span>  <span data-ttu-id="60ca3-113">Bunlar yalnızca, bunlar oluşturuldu ve bu oturumu kapattığında otomatik olarak bırakılan oturum görünür olur.</span><span class="sxs-lookup"><span data-stu-id="60ca3-113">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="60ca3-114">Uzaktaki Depolama birimi yerine yerel sonuçları yazıldığından geçici tablolara performans avantajı sunar.</span><span class="sxs-lookup"><span data-stu-id="60ca3-114">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="60ca3-115">Bunlar her yerden ve saklı yordam haricindeki dahil olmak üzere oturumu içinde erişilebilir olarak geçici tabloları Azure SQL veritabanından Azure SQL Data Warehouse'da biraz farklı.</span><span class="sxs-lookup"><span data-stu-id="60ca3-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="60ca3-116">Bu makalede geçici tabloları kullanmak için temel kılavuz içerir ve oturum düzeyi geçici tablolara ilkeleri vurgular.</span><span class="sxs-lookup"><span data-stu-id="60ca3-116">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="60ca3-117">Bu makaledeki bilgileri kullanarak yeniden kullanılırlığı ve kodunuzun bakım kolaylığı artırma kodunuzu modülarize etmek yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="60ca3-117">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="60ca3-118">Geçici bir tablo oluştur</span><span class="sxs-lookup"><span data-stu-id="60ca3-118">Create a temporary table</span></span>
<span data-ttu-id="60ca3-119">Geçici tablolara tablo adıyla ekleyerek oluşturulur bir `#`.</span><span class="sxs-lookup"><span data-stu-id="60ca3-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="60ca3-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="60ca3-120">For example:</span></span>

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

<span data-ttu-id="60ca3-121">Geçici tablolara de oluşturulabilir ile bir `CTAS` tam olarak aynı yaklaşımı kullanarak:</span><span class="sxs-lookup"><span data-stu-id="60ca3-121">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

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
> <span data-ttu-id="60ca3-122">`CTAS`çok güçlü bir komut ve işlem günlüğü alanının kullanımını çok verimli olma ek avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="60ca3-122">`CTAS` is a very powerful command and has the added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="60ca3-123">Geçici tablolara bırakılıyor</span><span class="sxs-lookup"><span data-stu-id="60ca3-123">Dropping temporary tables</span></span>
<span data-ttu-id="60ca3-124">Yeni bir oturum oluşturulduğunda, hiçbir geçici tablolar var olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="60ca3-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="60ca3-125">Ancak, emin olmak için aynı ada sahip bir geçici oluşturur aynı saklı yordamı çağırma varsa, `CREATE TABLE` deyimleri başarılı basit bir ön varlığı denetimi ile bir `DROP` olarak kullanılan örnek aşağıda:</span><span class="sxs-lookup"><span data-stu-id="60ca3-125">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="60ca3-126">Tutarlılık kodlama için tablo ve geçici tablolar için bu deseni kullanmak için iyi bir uygulama olur.</span><span class="sxs-lookup"><span data-stu-id="60ca3-126">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="60ca3-127">Bu aynı zamanda kullanmak için iyi bir fikirdir `DROP TABLE` bunlarla kodunuzda tamamladığınızda geçici tabloları kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="60ca3-127">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="60ca3-128">Saklı yordam, drop komutu bu nesneler emin olmak için bir yordam sonunda birlikte gruplanır görmek için oldukça yaygındır geliştirme temizlendi.</span><span class="sxs-lookup"><span data-stu-id="60ca3-128">In stored procedure development it is quite common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="60ca3-129">Modularizing kodu</span><span class="sxs-lookup"><span data-stu-id="60ca3-129">Modularizing code</span></span>
<span data-ttu-id="60ca3-130">Geçici tablolara herhangi bir kullanıcı oturum görülebilir olduğundan, bu uygulama kodunuz modülarize etmek amacıyla yararlanılabilir.</span><span class="sxs-lookup"><span data-stu-id="60ca3-130">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="60ca3-131">Örneğin, aşağıdaki saklı yordamı bir araya önerilen uygulamaları yukarıda veritabanındaki tüm istatistikleri istatistiği adıyla güncelleştirecektir DDL oluşturmak için getirir.</span><span class="sxs-lookup"><span data-stu-id="60ca3-131">For example, the stored procedure below brings together the recommended practices from above to generate DDL which will update all statistics in the database by statistic name.</span></span>

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

<span data-ttu-id="60ca3-132">Yalnızca olacak bir saklı yordam oluşturulmasını oluştu yalnızca eylem ise bu aşamada, geçici bir tablo DDL deyimleri ile #stats_ddl oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="60ca3-132">At this stage the only action that has occurred is the creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="60ca3-133">Oturum içindeki birden çok kez çalıştırırsanız başlayabildiğinden emin olmak için zaten varsa bu saklı yordam #stats_ddl bırakın.</span><span class="sxs-lookup"><span data-stu-id="60ca3-133">This stored procedure will drop #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="60ca3-134">Ancak, olduğundan hiçbir `DROP TABLE` saklı yordam tamamlandığında, böylece dışında saklı yordam okunabilir saklı yordamın sonunda, oluşturulmuş bir tabloyu bırakır.</span><span class="sxs-lookup"><span data-stu-id="60ca3-134">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it will leave the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="60ca3-135">SQL veri ambarı'nda diğer SQL Server veritabanlarını geçici tablo oluşturulduğu yordamı dışında kullanmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="60ca3-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="60ca3-136">SQL veri ambarı geçici tablolar kullanılabilir **herhangi bir yere** oturumu içinde.</span><span class="sxs-lookup"><span data-stu-id="60ca3-136">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="60ca3-137">Daha fazla modüler ve yönetilebilir kodu olarak neden olabilir örnek aşağıda:</span><span class="sxs-lookup"><span data-stu-id="60ca3-137">This can lead to more modular and manageable code as in the below example:</span></span>

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

## <a name="temporary-table-limitations"></a><span data-ttu-id="60ca3-138">Geçici Tablo sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="60ca3-138">Temporary table limitations</span></span>
<span data-ttu-id="60ca3-139">SQL veri ambarı birkaç sınırlama geçici tablolara uygularken zorunlu tuttukları.</span><span class="sxs-lookup"><span data-stu-id="60ca3-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="60ca3-140">Şu anda yalnızca oturum kapsamlı geçici tablolar desteklenir.</span><span class="sxs-lookup"><span data-stu-id="60ca3-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="60ca3-141">Genel geçici tablolar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="60ca3-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="60ca3-142">Ayrıca, geçici tablolarda görünümlere oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="60ca3-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60ca3-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60ca3-143">Next steps</span></span>
<span data-ttu-id="60ca3-144">Daha fazla bilgi edinmek için üzerinde makalelerine bakın [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tablodağıtma] [ Distribute], [Tablo dizin][Index], [bir tablo bölümleme] [ Partition] ve [Tablo istatistikleri koruma][Statistics].</span><span class="sxs-lookup"><span data-stu-id="60ca3-144">To learn more, see the articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="60ca3-145">En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="60ca3-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
