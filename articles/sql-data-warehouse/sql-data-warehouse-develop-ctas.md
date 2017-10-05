---
title: "(CTAS) SQL veri ambarı'nda seçerken tablo oluşturma | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse select (CTAS) deyiminde olarak oluşturma tabloyla kodlamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: cb08313726e8135feaa9b413937c2197ea397f4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="72eae-103">SQL veri ambarı'nda create Table As Select (CTAS)</span><span class="sxs-lookup"><span data-stu-id="72eae-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="72eae-104">Tablo seçin olarak oluşturun veya `CTAS` en önemli T-SQL özellikler kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="72eae-104">Create table as select or `CTAS` is one of the most important T-SQL features available.</span></span> <span data-ttu-id="72eae-105">Bir SELECT deyimi çıktıya dayalı yeni bir tablo oluşturur tam olarak parallelized bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="72eae-105">It is a fully parallelized operation that creates a new table based on the output of a SELECT statement.</span></span> <span data-ttu-id="72eae-106">`CTAS`bir tablonun kopyasını oluşturmak için basit ve hızlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="72eae-106">`CTAS` is the simplest and fastest way to create a copy of a table.</span></span> <span data-ttu-id="72eae-107">Bu belge örnekleri ve en iyi yöntemleri sağlar `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="72eae-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="72eae-108">SEÇİN... VS. CTAS</span><span class="sxs-lookup"><span data-stu-id="72eae-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="72eae-109">Göz önünde bulundurabilirsiniz `CTAS` Süper kartınızdan bir sürümü olarak `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="72eae-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="72eae-110">Basit bir örneği aşağıdadır `SELECT..INTO` deyimi:</span><span class="sxs-lookup"><span data-stu-id="72eae-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="72eae-111">Yukarıdaki örnekte `[dbo].[FactInternetSales_new]` Azure SQL Data warehouse'da tablo Varsayılanları bunlar gibi üzerindeki kümelenmiş COLUMNSTORE dizini olan ROUND_ROBIN dağıtılmış tablosu olarak oluşturulması.</span><span class="sxs-lookup"><span data-stu-id="72eae-111">In the example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are the table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="72eae-112">`SELECT..INTO`ancak dağıtım yöntemini veya dizin türü işleminin bir parçası değiştirmenize izin vermez.</span><span class="sxs-lookup"><span data-stu-id="72eae-112">`SELECT..INTO` however does not allow you to change either the distribution method or the index type as part of the operation.</span></span> <span data-ttu-id="72eae-113">Bu yerdir `CTAS` devreye girer.</span><span class="sxs-lookup"><span data-stu-id="72eae-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="72eae-114">Yukarıdaki dönüştürmek için `CTAS` oldukça düz-bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="72eae-114">To convert the above to `CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="72eae-115">İle `CTAS` dağıtım, tablo türü yanı sıra tablo verileri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eae-115">With `CTAS` you are able to change both the distribution of the table data as well as the table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="72eae-116">Yalnızca dizinde değiştirmeye çalışıyorsanız, `CTAS` işlemi ve kaynak tablosu olduğu dağıtılmış karma sonra `CTAS` işlemi aynı dağıtım sütun ve veri türü sahipseniz en iyi şekilde gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="72eae-116">If you are only trying to change the index in your `CTAS` operation and the source table is hash distributed then your `CTAS` operation will perform best if you maintain the same distribution column and data type.</span></span> <span data-ttu-id="72eae-117">Bu dağıtım veri taşıma daha etkilidir işlemi sırasında kaçının.</span><span class="sxs-lookup"><span data-stu-id="72eae-117">This will avoid cross distribution data movement during the operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-to-copy-a-table"></a><span data-ttu-id="72eae-118">CTAS bir tabloyu kopyalama için kullanma</span><span class="sxs-lookup"><span data-stu-id="72eae-118">Using CTAS to copy a table</span></span>
<span data-ttu-id="72eae-119">Belki de en yaygın birini kullanır `CTAS` DDL geçiş yapabilmeniz sağlayan bir tablonun kopyasını oluşturma.</span><span class="sxs-lookup"><span data-stu-id="72eae-119">Perhaps one of the most common uses of `CTAS` is creating a copy of a table so that you can change the DDL.</span></span> <span data-ttu-id="72eae-120">Örneğin, tablo olarak başlangıçta oluşturduysanız `ROUND_ROBIN` ve değiştirmek istediğiniz artık, dağıtılmış bir sütuna, tabloya `CTAS` nasıl dağıtım sütun değiştirme olduğu.</span><span class="sxs-lookup"><span data-stu-id="72eae-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it to a table distributed on a column, `CTAS` is how you would change the distribution column.</span></span> <span data-ttu-id="72eae-121">`CTAS`Ayrıca bölümlendirme, dizin oluşturma veya sütun türlerini değiştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="72eae-121">`CTAS` can also be used to change partitioning, indexing, or column types.</span></span>

<span data-ttu-id="72eae-122">Bu tablonun varsayılan dağıtım türünü kullanarak oluşturduğunuz düşünelim `ROUND_ROBIN` hiçbir dağıtım sütun belirtilmediğinden dağıtılmış `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="72eae-122">Let's say you created this table using the default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in the `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="72eae-123">Şimdi bu tabloda yeni bir kopyasını, ile kümelenmiş Columnstore dizini oluşturun, böylece kümelenmiş Columnstore tabloları performansını yararlanabilir istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="72eae-123">Now you want to create a new copy of this table with a Clustered Columnstore Index so that you can take advantage of the performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="72eae-124">Ayrıca bu sütunda birleştirmeler bekleme beri bu tabloda ProductKey dağıtmak istediğiniz ve ProductKey üzerinde birleştirme sırasında veri taşıma önlemek istiyor.</span><span class="sxs-lookup"><span data-stu-id="72eae-124">You also want to distribute this table on ProductKey since you are anticipating joins on this column and want to avoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="72eae-125">Son olarak da eski bölümleri bırakarak, eski verileri hızlı bir şekilde silebilirsiniz böylece OrderDateKey üzerinde bölümleme eklemek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="72eae-125">Lastly you also want to add partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="72eae-126">Burada, eski tablonuz yeni bir tabloya kopyalarsınız CTAS deyimi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="72eae-126">Here is the CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="72eae-127">Son olarak, yeni tablonuzda değiştirme ve eski tablonuz bırakma için tablolarınız adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eae-127">Finally you can rename your tables to swap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales TO FactInternetSales_old;
RENAME OBJECT FactInternetSales_new TO FactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="72eae-128">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="72eae-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="72eae-129">Sorgularınızdan en iyi performansı elde edebilmeniz için ilk yüklemeden veya verilerdeki önemli değişikliklerden sonra her tablonun her sütununa ilişkin istatistiklerin oluşturulması önemlidir.</span><span class="sxs-lookup"><span data-stu-id="72eae-129">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="72eae-130">İstatistikler hakkında ayrıntılı bir açıklama için Geliştirme ile ilgili konu başlığı grubunda yer alan [İstatistikler][Statistics] bölümüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="72eae-130">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-to-work-around-unsupported-features"></a><span data-ttu-id="72eae-131">Desteklenmeyen özellikler etrafında çalışmak için CTAS kullanma</span><span class="sxs-lookup"><span data-stu-id="72eae-131">Using CTAS to work around unsupported features</span></span>
<span data-ttu-id="72eae-132">`CTAS`Ayrıca aşağıda listelenen desteklenmeyen özellikler çeşitli geçici olarak çözmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="72eae-132">`CTAS` can also be used to work around a number of the unsupported features listed below.</span></span> <span data-ttu-id="72eae-133">Bu genellikle yalnızca kodunuzu uyumlu olacaktır, ancak bunu genellikle daha hızlı SQL Data Warehouse yürütecek win/win durum olması için kanıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eae-133">This can often prove to be a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="72eae-134">Tam olarak parallelized tasarımını sonucunda budur.</span><span class="sxs-lookup"><span data-stu-id="72eae-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="72eae-135">Geçici CTAS ile çalışılabilecek senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="72eae-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="72eae-136">ANSI BİRLEŞTİRMELER güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="72eae-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="72eae-137">ANSI birleştirmeler üzerinde siler</span><span class="sxs-lookup"><span data-stu-id="72eae-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="72eae-138">MERGE deyimi</span><span class="sxs-lookup"><span data-stu-id="72eae-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="72eae-139">Düşünmek deneyin "CTAS ilk".</span><span class="sxs-lookup"><span data-stu-id="72eae-139">Try to think "CTAS first".</span></span> <span data-ttu-id="72eae-140">Kullanarak bir sorunu çözebilir düşünüyorsanız `CTAS` , ise genellikle en iyi yolu, - yaklaşımını daha fazla veri sonuç olarak yazıyorsanız bile.</span><span class="sxs-lookup"><span data-stu-id="72eae-140">If you think you can solve a problem using `CTAS` then that is generally the best way to approach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="72eae-141">ANSI birleştirme değiştirme için güncelleştirme deyimleri</span><span class="sxs-lookup"><span data-stu-id="72eae-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="72eae-142">Birlikte sözdizimi birleştirme ANSI UPDATE veya DELETE kullanarak gerçekleştirmek için ikiden fazla tabloyu birleştiren karmaşık bir güncelleştirmeye sahip bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eae-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax to perform the UPDATE or DELETE.</span></span>

<span data-ttu-id="72eae-143">Bu tablo güncelleştirmeniz gerekiyordu düşünün:</span><span class="sxs-lookup"><span data-stu-id="72eae-143">Imagine you had to update this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="72eae-144">Özgün sorgu şöyle bir şey attıktan:</span><span class="sxs-lookup"><span data-stu-id="72eae-144">The original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="72eae-145">ANSI SQL veri ambarı desteklemediği bu yana birleştirmeleri `FROM` yan tümcesinde bir `UPDATE` deyimi, biraz değiştirmeden üzerinden bu kodu kopyalayamıyor.</span><span class="sxs-lookup"><span data-stu-id="72eae-145">Since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="72eae-146">Bir bileşimini kullanabilirsiniz bir `CTAS` ve bu kodu değiştirmek için örtük bir birleşim:</span><span class="sxs-lookup"><span data-stu-id="72eae-146">You can use a combination of a `CTAS` and an implicit join to replace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="72eae-147">ANSI birleştirme yerini silme deyimleri</span><span class="sxs-lookup"><span data-stu-id="72eae-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="72eae-148">Bazen veri silmek için en iyi yaklaşımı kullanmaktır `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="72eae-148">Sometimes the best approach for deleting data is to use `CTAS`.</span></span> <span data-ttu-id="72eae-149">Verileri yalnızca silme yerine korumak istediğiniz verileri seçin.</span><span class="sxs-lookup"><span data-stu-id="72eae-149">Rather than deleting the data simply select the data you want to keep.</span></span> <span data-ttu-id="72eae-150">Bu özellikle true `DELETE` ANSI SQL veri ambarı ANSI desteklemediğinden katılma sözdizimi birleştirir kullan deyimleri `FROM` yan tümcesinde bir `DELETE` deyimi.</span><span class="sxs-lookup"><span data-stu-id="72eae-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in the `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="72eae-151">Dönüştürülen DELETE deyimi örneği aşağıda kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="72eae-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish to keep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        TO DimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert TO DimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="72eae-152">Merge deyimlerinde değiştirin</span><span class="sxs-lookup"><span data-stu-id="72eae-152">Replace merge statements</span></span>
<span data-ttu-id="72eae-153">Merge deyimlerinde değiştirilebilir, en az bölümünde kullanarak `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="72eae-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="72eae-154">Birleştirebilir `INSERT` ve `UPDATE` tek bir deyimde içine.</span><span class="sxs-lookup"><span data-stu-id="72eae-154">You can consolidate the `INSERT` and the `UPDATE` into a single statement.</span></span> <span data-ttu-id="72eae-155">Silinmiş kayıtları Kapat'ı ikinci bir deyimde kapatılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="72eae-155">Any deleted records would need to be closed off in a second statement.</span></span>

<span data-ttu-id="72eae-156">Örnek olarak bir `UPSERT` aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="72eae-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          TO [DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  TO [DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="72eae-157">CTAS öneri: açıkça durumunda veri türü ve çıktı olabilirliği</span><span class="sxs-lookup"><span data-stu-id="72eae-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="72eae-158">Kod geçirirken bu tür bir kodlama düzeni çalıştırmak bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="72eae-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="72eae-159">İnstinctively CTAS için bu kodu geçirmeniz gerekir ve doğru olacaktır düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eae-159">Instinctively you might think you should migrate this code to a CTAS and you would be correct.</span></span> <span data-ttu-id="72eae-160">Ancak, burada gizli bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="72eae-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="72eae-161">Aşağıdaki kod, aynı sonucu vermez:</span><span class="sxs-lookup"><span data-stu-id="72eae-161">The following code does NOT yield the same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="72eae-162">"Sonuç" sütun İleri ifade veri türü ve null atanabilirlik değerleri taşıyan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="72eae-162">Notice that the column "result" carries forward the data type and nullability values of the expression.</span></span> <span data-ttu-id="72eae-163">Dikkatli değilseniz, bu değerleri Zarif Varyanslar neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="72eae-163">This can lead to subtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="72eae-164">Örnek olarak aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="72eae-164">Try the following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="72eae-165">Sonuç için saklanan değer farklıdır.</span><span class="sxs-lookup"><span data-stu-id="72eae-165">The value stored for result is different.</span></span> <span data-ttu-id="72eae-166">Sonuç sütunu kalıcı değerinde diğer ifadelerinde kullanıldıkça hata daha önemli hale gelir.</span><span class="sxs-lookup"><span data-stu-id="72eae-166">As the persisted value in the result column is used in other expressions the error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="72eae-167">Bu veri geçişler için özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="72eae-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="72eae-168">İkinci sorguyu tartışmaya açık bir şekilde daha doğru olsa bile bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="72eae-168">Even though the second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="72eae-169">Veri kaynağı sisteme karşılaştırıldığında farklı olacaktır ve bütünlüğü geçiş sorular, yol açar.</span><span class="sxs-lookup"><span data-stu-id="72eae-169">The data would be different compared to the source system and that leads to questions of integrity in the migration.</span></span> <span data-ttu-id="72eae-170">Bu, "yanlış" yanıt gerçekten doğru olanı olduğu bu nadir durumlarda biridir!</span><span class="sxs-lookup"><span data-stu-id="72eae-170">This is one of those rare cases where the "wrong" answer is actually the right one!</span></span>

<span data-ttu-id="72eae-171">Biz bu farklılığa arasında iki sonuçları görmek için örtük tür atama nedenidir.</span><span class="sxs-lookup"><span data-stu-id="72eae-171">The reason we see this disparity between the two results is down to implicit type casting.</span></span> <span data-ttu-id="72eae-172">İlk örnekte tablonun sütun tanımı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="72eae-172">In the first example the table defines the column definition.</span></span> <span data-ttu-id="72eae-173">Satır eklendiğinde, bir örtük tür dönüştürme oluşur.</span><span class="sxs-lookup"><span data-stu-id="72eae-173">When the row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="72eae-174">İkinci örnekte yoktur örtük tür dönüştürme gibi ifade sütunun veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="72eae-174">In the second example there is no implicit type conversion as the expression defines data type of the column.</span></span> <span data-ttu-id="72eae-175">Ayrıca ilk örnekte, henüz ancak ikinci örnek sütununda bir boş değer atanabilir sütun olarak tanımlanmış dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="72eae-175">Notice also that the column in the second example has been defined as a NULLable column whereas in the first example it has not.</span></span> <span data-ttu-id="72eae-176">Tablonun ilk örnek sütun null atanabilirlik içinde oluşturulduğu açıkça tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="72eae-176">When the table was created in the first example column nullability was explicitly defined.</span></span> <span data-ttu-id="72eae-177">İkinci örneği, yalnızca bir ifadeye ve varsayılan olarak bu bırakıldı NULL tanımında neden olur.</span><span class="sxs-lookup"><span data-stu-id="72eae-177">In the second example it was just left to the expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="72eae-178">Bu sorunları gidermek için açıkça içinde null atanabilirlik ve tür dönüştürmeleri ayarlanmalıdır `SELECT` kısmı `CTAS` deyimi.</span><span class="sxs-lookup"><span data-stu-id="72eae-178">To resolve these issues you must explicitly set the type conversion and nullability in the `SELECT` portion of the `CTAS` statement.</span></span> <span data-ttu-id="72eae-179">Create table bölümünde bu özellikleri ayarlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="72eae-179">You cannot set these properties in the create table part.</span></span>

<span data-ttu-id="72eae-180">Aşağıdaki örnek kod gidermeye yönelik gösterir.</span><span class="sxs-lookup"><span data-stu-id="72eae-180">The example below demonstrates how to fix the code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="72eae-181">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="72eae-181">Note the following:</span></span>

* <span data-ttu-id="72eae-182">CAST veya CONVERT kullanılan</span><span class="sxs-lookup"><span data-stu-id="72eae-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="72eae-183">IsNull null Atanabilirlik olmayan birleşim zorlamak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="72eae-183">ISNULL is used to force NULLability not COALESCE</span></span>
* <span data-ttu-id="72eae-184">IsNull en dıştaki işlevidir</span><span class="sxs-lookup"><span data-stu-id="72eae-184">ISNULL is the outermost function</span></span>
* <span data-ttu-id="72eae-185">Bir sabit IsNull ikinci parçası olan yani 0</span><span class="sxs-lookup"><span data-stu-id="72eae-185">The second part of the ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="72eae-186">Olabilirliği doğru şekilde ayarlanması kullanılacak önemli `ISNULL` ve `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="72eae-186">For the nullability to be correctly set it is vital to use `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="72eae-187">`COALESCE`belirleyici bir işlev değil ve bu nedenle ifade sonucu null atanabilir her zaman olacaktır.</span><span class="sxs-lookup"><span data-stu-id="72eae-187">`COALESCE` is not a deterministic function and so the result of the expression will always be NULLable.</span></span> <span data-ttu-id="72eae-188">`ISNULL`farklıdır.</span><span class="sxs-lookup"><span data-stu-id="72eae-188">`ISNULL` is different.</span></span> <span data-ttu-id="72eae-189">Belirleyici.</span><span class="sxs-lookup"><span data-stu-id="72eae-189">It is deterministic.</span></span> <span data-ttu-id="72eae-190">Bu nedenle, ikinci bölümü `ISNULL` işlevidir bir sabit ya da bir hazır değer sonra sonuçta elde edilen değer olacaktır NOT NULL.</span><span class="sxs-lookup"><span data-stu-id="72eae-190">Therefore when the second part of the `ISNULL` function is a constant or a literal then the resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="72eae-191">Bu ipucu, hesaplamalar bütünlüğünü sağlamak için yalnızca kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="72eae-191">This tip is not just useful for ensuring the integrity of your calculations.</span></span> <span data-ttu-id="72eae-192">Bölüm tablo geçmek için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="72eae-192">It is also important for table partition switching.</span></span> <span data-ttu-id="72eae-193">Bu tablo, olgu tanımlanan olduğunu düşünün:</span><span class="sxs-lookup"><span data-stu-id="72eae-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="72eae-194">Ancak, değer alanına veri kaynağını parçası olmayan bir hesaplanan ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="72eae-194">However, the value field is a calculated expression it is not part of the source data.</span></span>

<span data-ttu-id="72eae-195">Bölümlenmiş kümenizi oluşturmak için bunu yapmak isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="72eae-195">To create your partitioned dataset you might want to do this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="72eae-196">Sorgu mükemmel iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="72eae-196">The query would run perfectly fine.</span></span> <span data-ttu-id="72eae-197">Bölüm anahtarı gerçekleştirmeye çalıştığında sorun gelir.</span><span class="sxs-lookup"><span data-stu-id="72eae-197">The problem comes when you try to perform the partition switch.</span></span> <span data-ttu-id="72eae-198">Tablo tanımları eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="72eae-198">The table definitions do not match.</span></span> <span data-ttu-id="72eae-199">CTAS eşleşen tablo tanımları yapmak için değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="72eae-199">To make the table definitions match the CTAS needs to be modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="72eae-200">Bu nedenle, türü tutarlılık ve bir CTAS null atanabilirlik özellikleri koruma iyi bir mühendislik en iyi uygulama olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72eae-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="72eae-201">Bu, hesaplamalarda bütünlüğünü sağlamaya yardımcı olur ve ayrıca bölüm değiştirme mümkün olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="72eae-201">It helps to maintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="72eae-202">Lütfen kullanma hakkında daha fazla bilgi için MSDN başvurun [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="72eae-202">Please refer to MSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="72eae-203">Azure SQL Data Warehouse en önemli deyimlerinde biridir.</span><span class="sxs-lookup"><span data-stu-id="72eae-203">It is one of the most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="72eae-204">İyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="72eae-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72eae-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72eae-205">Next steps</span></span>
<span data-ttu-id="72eae-206">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="72eae-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
