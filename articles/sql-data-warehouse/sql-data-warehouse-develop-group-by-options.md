---
title: "SQL veri ambarı seçeneklerinde grupla | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse seçeneklerinde tarafından Grup uygulamak için ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: da71cb834c13da5d0f5690f471efc6c696163f30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="036d8-103">SQL veri ambarı seçeneklerinde göre gruplandırmak</span><span class="sxs-lookup"><span data-stu-id="036d8-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="036d8-104">[GROUP BY] [ GROUP BY] yan tümcesi Özet bir satır kümesi için veri toplama için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="036d8-104">The [GROUP BY][GROUP BY] clause is used to aggregate data to a summary set of rows.</span></span> <span data-ttu-id="036d8-105">Ayrıca, geçici doğrudan Azure SQL Data Warehouse tarafından desteklenmiyor olarak çalışması için gereken kendi işlevselliğini genişleten birkaç seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="036d8-105">It also has a few options that extend it's functionality that need to be worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="036d8-106">Bu seçenekler</span><span class="sxs-lookup"><span data-stu-id="036d8-106">These options are</span></span>

* <span data-ttu-id="036d8-107">GROUP BY ile dökümü</span><span class="sxs-lookup"><span data-stu-id="036d8-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="036d8-108">GRUPLANDIRMA KÜMELERİ</span><span class="sxs-lookup"><span data-stu-id="036d8-108">GROUPING SETS</span></span>
* <span data-ttu-id="036d8-109">GROUP BY ile KÜPÜ</span><span class="sxs-lookup"><span data-stu-id="036d8-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="036d8-110">Toplama ve gruplandırma kümeleri seçenekleri</span><span class="sxs-lookup"><span data-stu-id="036d8-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="036d8-111">Burada en basit seçenek kullanmaktır `UNION ALL` yerine toplama gerçekleştirmek için açık sözdizimi, bağlı olan yerine.</span><span class="sxs-lookup"><span data-stu-id="036d8-111">The simplest option here is to use `UNION ALL` instead to perform the rollup rather than relying on the explicit syntax.</span></span> <span data-ttu-id="036d8-112">Tam olarak aynı sonucudur</span><span class="sxs-lookup"><span data-stu-id="036d8-112">The result is exactly the same</span></span>

<span data-ttu-id="036d8-113">Aşağıda, bir gruba deyimi kullanılarak örneğidir `ROLLUP` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="036d8-113">Below is an example of a group by statement using the `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="036d8-114">Toplama kullanarak aşağıdaki toplamalar istediniz:</span><span class="sxs-lookup"><span data-stu-id="036d8-114">By using ROLLUP we have requested the following aggregations:</span></span>

* <span data-ttu-id="036d8-115">Ülke ve bölgeye</span><span class="sxs-lookup"><span data-stu-id="036d8-115">Country and Region</span></span>
* <span data-ttu-id="036d8-116">Ülke</span><span class="sxs-lookup"><span data-stu-id="036d8-116">Country</span></span>
* <span data-ttu-id="036d8-117">Genel toplam</span><span class="sxs-lookup"><span data-stu-id="036d8-117">Grand Total</span></span>

<span data-ttu-id="036d8-118">Bu kullanması gerekecektir değiştirmek için `UNION ALL`; aynı sonuçları döndürmek için açıkça gerekli toplamalar belirtme:</span><span class="sxs-lookup"><span data-stu-id="036d8-118">To replace this you will need to use `UNION ALL`; specifying the aggregations required explicitly to return the same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="036d8-119">GRUPLANDIRMA yapmamız gereken ayarlar tüm için aynı asıl adı benimsemeyi ancak yalnızca görmeyi istiyoruz toplama düzeyleri için UNION ALL bölümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="036d8-119">For GROUPING SETS all we need to do is adopt the same principal but only create UNION ALL sections for the aggregation levels we want to see</span></span>

## <a name="cube-options"></a><span data-ttu-id="036d8-120">Küp seçenekleri</span><span class="sxs-lookup"><span data-stu-id="036d8-120">Cube options</span></span>
<span data-ttu-id="036d8-121">Bir grup tarafından ile UNION ALL yaklaşımı kullanarak KÜPÜ oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="036d8-121">It is possible to create a GROUP BY WITH CUBE using the UNION ALL approach.</span></span> <span data-ttu-id="036d8-122">Kod sıkıcı ve yönetilmeleri hızlı bir şekilde olabilecek sorunudur.</span><span class="sxs-lookup"><span data-stu-id="036d8-122">The problem is that the code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="036d8-123">Bunu azaltmak için bu yaklaşım daha gelişmiş kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="036d8-123">To mitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="036d8-124">Yukarıdaki örnekte kullanalım.</span><span class="sxs-lookup"><span data-stu-id="036d8-124">Let's use the example above.</span></span>

<span data-ttu-id="036d8-125">İlk adım, 'biz oluşturmak istediğiniz bir toplama tüm düzeylerini tanımlar cube' tanımlamaktır.</span><span class="sxs-lookup"><span data-stu-id="036d8-125">The first step is to define the 'cube' that defines all the levels of aggregation that we want to create.</span></span> <span data-ttu-id="036d8-126">CROSS JOIN iki türetilmiş tabloların not almanız önemlidir.</span><span class="sxs-lookup"><span data-stu-id="036d8-126">It is important to take note of the CROSS JOIN of the two derived tables.</span></span> <span data-ttu-id="036d8-127">Bu tüm düzeyleri bize oluşturur.</span><span class="sxs-lookup"><span data-stu-id="036d8-127">This generates all the levels for us.</span></span> <span data-ttu-id="036d8-128">Kod kalan gerçekten biçimlendirme için yoktur.</span><span class="sxs-lookup"><span data-stu-id="036d8-128">The rest of the code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="036d8-129">CTAS sonuçlarını aşağıda görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="036d8-129">The results of the CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="036d8-130">Ara Sonuçların depolanacağı bir hedef tablo belirtmek için ikinci adım şöyledir:</span><span class="sxs-lookup"><span data-stu-id="036d8-130">The second step is to specify a target table to store interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="036d8-131">Üçüncü adım bizim toplama gerçekleştirme sütunları küp üzerinde döngü oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="036d8-131">The third step is to loop over our cube of columns performing the aggregation.</span></span> <span data-ttu-id="036d8-132">Sorgu #Cube geçici tablodaki her satır için bir kez çalıştır ve #Results geçici tablosunda Sonuçların depolanacağı</span><span class="sxs-lookup"><span data-stu-id="036d8-132">The query will run once for every row in the #Cube temporary table and store the results in the #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="036d8-133">Son olarak biz #Results geçici tablosundan okuyarak sonuçlar döndürebilir</span><span class="sxs-lookup"><span data-stu-id="036d8-133">Lastly we can return the results by simply reading from the #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="036d8-134">Kod bölümlere ayırma ve döngü yapısı oluşturma kodu daha yönetilebilir ve sürdürülebilir haline gelir.</span><span class="sxs-lookup"><span data-stu-id="036d8-134">By breaking the code up into sections and generating a looping construct the code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="036d8-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="036d8-135">Next steps</span></span>
<span data-ttu-id="036d8-136">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="036d8-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
