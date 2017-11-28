---
title: "SQL veri ambarı'nda (CTAS) seçip aaaCreate tablo | Microsoft Docs"
description: "Merhaba ile kodlamak için ipuçları çözümleri geliştirmek için Azure SQL Data Warehouse'da select (CTAS) deyimi gibi tablo oluşturun."
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
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="2db9b-103">SQL veri ambarı'nda create Table As Select (CTAS)</span><span class="sxs-lookup"><span data-stu-id="2db9b-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="2db9b-104">Tablo seçin olarak oluşturun veya `CTAS` hello en önemli T-SQL özelliklerini biridir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="2db9b-105">SELECT deyiminin hello çıktıya dayalı yeni bir tablo oluşturur tam olarak parallelized bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="2db9b-106">`CTAS`Merhaba basit ve hızlı yolu toocreate bir tablonun bir kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="2db9b-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="2db9b-107">Bu belge örnekleri ve en iyi yöntemleri sağlar `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2db9b-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="2db9b-108">SEÇİN... VS. CTAS</span><span class="sxs-lookup"><span data-stu-id="2db9b-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="2db9b-109">Göz önünde bulundurabilirsiniz `CTAS` Süper kartınızdan bir sürümü olarak `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="2db9b-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="2db9b-110">Basit bir örneği aşağıdadır `SELECT..INTO` deyimi:</span><span class="sxs-lookup"><span data-stu-id="2db9b-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="2db9b-111">Yukarıdaki hello örnekte `[dbo].[FactInternetSales_new]` hello tablo Varsayılanları Azure SQL Data warehouse'da bunlar gibi üzerindeki kümelenmiş COLUMNSTORE dizini olan ROUND_ROBIN dağıtılmış tablosu olarak oluşturulması.</span><span class="sxs-lookup"><span data-stu-id="2db9b-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="2db9b-112">`SELECT..INTO`Ancak, her iki hello dağıtım yöntemini veya hello dizinini yazın hello işleminin bir parçası toochange izin vermez.</span><span class="sxs-lookup"><span data-stu-id="2db9b-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="2db9b-113">Bu yerdir `CTAS` devreye girer.</span><span class="sxs-lookup"><span data-stu-id="2db9b-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="2db9b-114">çok hello yukarıda tooconvert`CTAS` oldukça düz-bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="2db9b-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

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

<span data-ttu-id="2db9b-115">İle `CTAS` mümkün toochange olduğunuz her ikisi de hello tablo türü yanı sıra hello tablo verisi dağıtımını hello.</span><span class="sxs-lookup"><span data-stu-id="2db9b-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="2db9b-116">Toochange hello dizinde yalnızca çalışıyorsanız, `CTAS` işlemi ve hello kaynak tablodur dağıtılmış karma sonra `CTAS` işlemi gerçekleştirecek, sahipseniz en iyi hello aynı dağıtım sütun ve veri türü.</span><span class="sxs-lookup"><span data-stu-id="2db9b-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="2db9b-117">Bu dağıtım veri taşıma daha etkili olan hello işlemi sırasında kaçının.</span><span class="sxs-lookup"><span data-stu-id="2db9b-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="2db9b-118">CTAS toocopy tablo kullanma</span><span class="sxs-lookup"><span data-stu-id="2db9b-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="2db9b-119">Belki de hello en yaygın birini kullanır `CTAS` hello DDL geçiş yapabilmeniz sağlayan bir tablonun kopyasını oluşturma.</span><span class="sxs-lookup"><span data-stu-id="2db9b-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="2db9b-120">Örneğin, tablo olarak başlangıçta oluşturduysanız `ROUND_ROBIN` ve değiştirmek istediğiniz şimdi onu tooa tablo dağıtılmış bir sütuna, `CTAS` nasıl hello dağıtım sütun değiştirme olduğu.</span><span class="sxs-lookup"><span data-stu-id="2db9b-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="2db9b-121">`CTAS`Ayrıca kullanılan toochange bölümlendirme, dizin oluşturma veya sütun türleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="2db9b-122">Bu tablo hello varsayılan dağıtım türünü kullanarak oluşturduğunuz düşünelim `ROUND_ROBIN` hiçbir dağıtım sütun hello belirtilmediğinden dağıtılmış `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="2db9b-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

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

<span data-ttu-id="2db9b-123">Şimdi kümelenmiş Columnstore tabloları hello performansını yararlanabilir böylece toocreate Bu tablo bir kümelenmiş Columnstore dizini ile yeni bir kopyasını istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="2db9b-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="2db9b-124">Bu sütunda birleştirmeler bekleme ve ProductKey üzerinde birleştirme sırasında tooavoid veri taşıma istiyorsanız bu yana ProductKey bu tabloda toodistribute da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db9b-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="2db9b-125">Son olarak, böylece eski bölümleri bırakarak, eski verileri hızlı bir şekilde silebilirsiniz tooadd OrderDateKey üzerinde bölümleme da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db9b-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="2db9b-126">Burada, eski tablonuz yeni bir tabloya kopyalarsınız hello CTAS deyimi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

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

<span data-ttu-id="2db9b-127">Son olarak, tablolar tooswap yeni tablonuzda yeniden adlandırın ve eski tablonuz bırakın.</span><span class="sxs-lookup"><span data-stu-id="2db9b-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="2db9b-128">Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="2db9b-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="2db9b-129">Sipariş tooget hello en iyi performansı sorgularınızı, istatistikleri hello ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda oluşturulması önemlidir veya hello verilerde önemli değişikliklerden.</span><span class="sxs-lookup"><span data-stu-id="2db9b-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="2db9b-130">Merhaba istatistikleri ayrıntılı bir açıklaması için bkz [istatistikleri] [ Statistics] konu hello geliştirme grubunu konuda.</span><span class="sxs-lookup"><span data-stu-id="2db9b-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="2db9b-131">Desteklenmeyen özellikler etrafında CTAS toowork kullanma</span><span class="sxs-lookup"><span data-stu-id="2db9b-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="2db9b-132">`CTAS`Aşağıda listelenen desteklenmeyen hello özelliklerini geçici kullanılan toowork de olabilir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="2db9b-133">Yalnızca kodunuzun uyumlu olur ancak bu genellikle daha hızlı SQL Data Warehouse yürütülmez bu genellikle bir win/win durum toobe kanıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db9b-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="2db9b-134">Tam olarak parallelized tasarımını sonucunda budur.</span><span class="sxs-lookup"><span data-stu-id="2db9b-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="2db9b-135">Geçici CTAS ile çalışılabilecek senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2db9b-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="2db9b-136">ANSI BİRLEŞTİRMELER güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="2db9b-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="2db9b-137">ANSI birleştirmeler üzerinde siler</span><span class="sxs-lookup"><span data-stu-id="2db9b-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="2db9b-138">MERGE deyimi</span><span class="sxs-lookup"><span data-stu-id="2db9b-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="2db9b-139">Toothink deneyin "CTAS ilk".</span><span class="sxs-lookup"><span data-stu-id="2db9b-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="2db9b-140">Kullanarak bir sorunu çözebilir düşünüyorsanız `CTAS` , genellikle hello en iyi şekilde tooapproach sonra onu - daha fazla veri sonuç olarak yazıyorsanız, hatta.</span><span class="sxs-lookup"><span data-stu-id="2db9b-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="2db9b-141">ANSI birleştirme değiştirme için güncelleştirme deyimleri</span><span class="sxs-lookup"><span data-stu-id="2db9b-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="2db9b-142">Sözdizimi tooperform hello birleştirme ANSI kullanılarak güncelleştirme veya silme ikiden fazla tabloyu birleştiren karmaşık bir güncelleştirmeye sahip bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db9b-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="2db9b-143">Bu tabloda tooupdate olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="2db9b-143">Imagine you had tooupdate this table:</span></span>

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

<span data-ttu-id="2db9b-144">Merhaba özgün sorgu şöyle bir şey attıktan:</span><span class="sxs-lookup"><span data-stu-id="2db9b-144">hello original query might have looked something like this:</span></span>

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

<span data-ttu-id="2db9b-145">SQL veri ambarı desteklemediği beri ANSI hello birleştirmeleri `FROM` yan tümcesinde bir `UPDATE` deyimi, biraz değiştirmeden üzerinden bu kodu kopyalayamıyor.</span><span class="sxs-lookup"><span data-stu-id="2db9b-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="2db9b-146">Bir bileşimini kullanabilirsiniz bir `CTAS` ve bir örtük bu kodu tooreplace Katıl:</span><span class="sxs-lookup"><span data-stu-id="2db9b-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

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

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="2db9b-147">ANSI birleştirme yerini silme deyimleri</span><span class="sxs-lookup"><span data-stu-id="2db9b-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="2db9b-148">Bazen veri silmek için hello en iyi toouse yaklaşımdır `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2db9b-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="2db9b-149">Merhaba verileri yalnızca silme yerine tookeep istediğiniz hello verileri seçin.</span><span class="sxs-lookup"><span data-stu-id="2db9b-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="2db9b-150">Bu özellikle true `DELETE` ANSI SQL veri ambarı hello ANSI birleştirmeler desteklemediğinden sözdizimi birleştirme kullan deyimleri `FROM` yan tümcesinde bir `DELETE` deyimi.</span><span class="sxs-lookup"><span data-stu-id="2db9b-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="2db9b-151">Dönüştürülen DELETE deyimi örneği aşağıda kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="2db9b-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="2db9b-152">Merge deyimlerinde değiştirin</span><span class="sxs-lookup"><span data-stu-id="2db9b-152">Replace merge statements</span></span>
<span data-ttu-id="2db9b-153">Merge deyimlerinde değiştirilebilir, en az bölümünde kullanarak `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="2db9b-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="2db9b-154">Merhaba birleştirebilir `INSERT` ve hello `UPDATE` tek bir deyimde içine.</span><span class="sxs-lookup"><span data-stu-id="2db9b-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="2db9b-155">Silinmiş kayıtları kapalı ikinci bir deyimde kapalı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="2db9b-156">Örnek olarak bir `UPSERT` aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2db9b-156">An example of an `UPSERT` is available below:</span></span>

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

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="2db9b-157">CTAS öneri: açıkça durumunda veri türü ve çıktı olabilirliği</span><span class="sxs-lookup"><span data-stu-id="2db9b-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="2db9b-158">Kod geçirirken bu tür bir kodlama düzeni çalıştırmak bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2db9b-158">When migrating code you might find you run across this type of coding pattern:</span></span>

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

<span data-ttu-id="2db9b-159">İnstinctively bu kodu tooa CTAS geçirmeniz gerekir ve doğru olacaktır düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db9b-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="2db9b-160">Ancak, burada gizli bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="2db9b-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="2db9b-161">Merhaba aşağıdaki kodu değil verim hello aynı sonucu:</span><span class="sxs-lookup"><span data-stu-id="2db9b-161">hello following code does NOT yield hello same result:</span></span>

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

<span data-ttu-id="2db9b-162">Merhaba sütun "sonuç" İleri hello ifadesinin hello veri türü ve null atanabilirlik değerleri taşıyan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2db9b-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="2db9b-163">Dikkatli değilseniz, bu değerleri toosubtle Varyanslar neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="2db9b-164">Örnek olarak Hello aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="2db9b-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="2db9b-165">sonuç için saklanan hello değeri farklıdır.</span><span class="sxs-lookup"><span data-stu-id="2db9b-165">hello value stored for result is different.</span></span> <span data-ttu-id="2db9b-166">Hello hello sonuç sütunu kalıcı değerinde diğer kullanıldıkça ifadeleri hello hata daha önemli hale gelir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="2db9b-167">Bu veri geçişler için özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="2db9b-168">Merhaba ikinci sorguyu tartışmaya açık bir şekilde daha doğru olsa bile bir sorun yoktur.</span><span class="sxs-lookup"><span data-stu-id="2db9b-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="2db9b-169">Hello veri farklı karşılaştırılan toohello kaynak sistemi olacaktır ve bütünlüğü tooquestions hello geçişte yol açar.</span><span class="sxs-lookup"><span data-stu-id="2db9b-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="2db9b-170">Bu, hello "yanlış" yanıt gerçekte hello sağa bir olduğu bu nadir durumlarda biridir!</span><span class="sxs-lookup"><span data-stu-id="2db9b-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="2db9b-171">Merhaba Biz bu farklılığa hello iki sonuçları arasında bkz tooimplicit nedeni atama yazın.</span><span class="sxs-lookup"><span data-stu-id="2db9b-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="2db9b-172">Hello ilk örnek Merhaba tablonun hello sütun tanımı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2db9b-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="2db9b-173">Merhaba satır eklendiğinde, bir örtük tür dönüştürme oluşur.</span><span class="sxs-lookup"><span data-stu-id="2db9b-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="2db9b-174">Merhaba ikinci örnekte yoktur örtük tür dönüştürme gibi hello ifade hello sütunun veri türünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2db9b-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="2db9b-175">Hello ilk örnekte, henüz ancak aynı zamanda hello ikinci örnek hello sütunda boş değer atanabilir sütun olarak tanımlanmış dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2db9b-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="2db9b-176">Merhaba tablo içinde oluşturulduğu sırada hello ilk örnek sütun null atanabilirlik açıkça tanımlandı.</span><span class="sxs-lookup"><span data-stu-id="2db9b-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="2db9b-177">Merhaba ikinci örnekte toohello ifade yalnızca bırakıldı ve varsayılan olarak bu NULL tanımında neden olur.</span><span class="sxs-lookup"><span data-stu-id="2db9b-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="2db9b-178">Bu sorunları tooresolve açıkça ayarlamalıdır hello tür dönüştürmeleri ve null atanabilirlik hello `SELECT` hello kısmı `CTAS` deyimi.</span><span class="sxs-lookup"><span data-stu-id="2db9b-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="2db9b-179">Bunlar ayarlanamıyor hello özelliklerinde tablo kısmen oluşturulamıyor.</span><span class="sxs-lookup"><span data-stu-id="2db9b-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="2db9b-180">Aşağıdaki Hello örnek nasıl toofix hello kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="2db9b-181">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2db9b-181">Note hello following:</span></span>

* <span data-ttu-id="2db9b-182">CAST veya CONVERT kullanılan</span><span class="sxs-lookup"><span data-stu-id="2db9b-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="2db9b-183">IsNull kullanılan tooforce null Atanabilirlik olmayan birleşim değil</span><span class="sxs-lookup"><span data-stu-id="2db9b-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="2db9b-184">IsNull hello en dıştaki işlevidir</span><span class="sxs-lookup"><span data-stu-id="2db9b-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="2db9b-185">Merhaba ikinci hello IsNull parçası olan bir sabit yani 0</span><span class="sxs-lookup"><span data-stu-id="2db9b-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="2db9b-186">Merhaba null atanabilirlik toobe doğru şekilde ayarlanması önemli toouse aranır `ISNULL` ve `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="2db9b-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="2db9b-187">`COALESCE`belirleyici bir işlev değil ve bu nedenle hello ifadenin hello sonucu null atanabilir her zaman olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2db9b-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="2db9b-188">`ISNULL`farklıdır.</span><span class="sxs-lookup"><span data-stu-id="2db9b-188">`ISNULL` is different.</span></span> <span data-ttu-id="2db9b-189">Belirleyici.</span><span class="sxs-lookup"><span data-stu-id="2db9b-189">It is deterministic.</span></span> <span data-ttu-id="2db9b-190">Bu nedenle zaman hello hello ikinci bölümü `ISNULL` işlevidir bir sabit ya da bir hazır değer sonra hello elde edilen değer NULL.</span><span class="sxs-lookup"><span data-stu-id="2db9b-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="2db9b-191">Bu ipucu, hesaplamalar hello bütünlüğünü sağlamak için yalnızca kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="2db9b-192">Bölüm tablo geçmek için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-192">It is also important for table partition switching.</span></span> <span data-ttu-id="2db9b-193">Bu tablo, olgu tanımlanan olduğunu düşünün:</span><span class="sxs-lookup"><span data-stu-id="2db9b-193">Imagine you have this table defined as your fact:</span></span>

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

<span data-ttu-id="2db9b-194">Ancak, hello değeri alanı hello kaynak veri parçası olmayan bir hesaplanan ifadesidir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="2db9b-195">toocreate isteyebileceğiniz toodo bu bölümlenmiş kümenizi:</span><span class="sxs-lookup"><span data-stu-id="2db9b-195">toocreate your partitioned dataset you might want toodo this:</span></span>

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

<span data-ttu-id="2db9b-196">Merhaba sorgu mükemmel iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="2db9b-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="2db9b-197">tooperform hello bölüm anahtarı çalıştığınızda hello sorun gelir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="2db9b-198">Merhaba tablo tanımları eşleşmiyor.</span><span class="sxs-lookup"><span data-stu-id="2db9b-198">hello table definitions do not match.</span></span> <span data-ttu-id="2db9b-199">toomake hello tablo tanımları değiştiren toobe CTAS gereken hello eşleşir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

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

<span data-ttu-id="2db9b-200">Bu nedenle, türü tutarlılık ve bir CTAS null atanabilirlik özellikleri koruma iyi bir mühendislik en iyi uygulama olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2db9b-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="2db9b-201">Toomaintain bütünlüğü, hesaplamalarda yardımcı olur ve ayrıca bölüm değiştirme mümkün olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2db9b-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="2db9b-202">Kullanma hakkında daha fazla bilgi için lütfen tooMSDN bakın [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="2db9b-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="2db9b-203">Azure SQL Data Warehouse en önemli deyimlerinde hello biridir.</span><span class="sxs-lookup"><span data-stu-id="2db9b-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2db9b-204">İyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2db9b-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2db9b-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2db9b-205">Next steps</span></span>
<span data-ttu-id="2db9b-206">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="2db9b-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
