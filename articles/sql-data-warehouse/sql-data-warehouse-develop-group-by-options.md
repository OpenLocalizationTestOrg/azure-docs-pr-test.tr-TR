---
title: "SQL veri ambarı seçeneklerinde tarafından aaaGroup | Microsoft Docs"
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
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="fec95-103">SQL veri ambarı seçeneklerinde göre gruplandırmak</span><span class="sxs-lookup"><span data-stu-id="fec95-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="fec95-104">Merhaba [GROUP BY] [ GROUP BY] yan tümcesinde kullanılan tooaggregate veri tooa Özet satır kümesi.</span><span class="sxs-lookup"><span data-stu-id="fec95-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="fec95-105">Ayrıca, geçici doğrudan Azure SQL Data Warehouse tarafından desteklenmiyor gibi çalıştığını bu gereksinimi toobe cihazın işlevselliğini genişleten birkaç seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="fec95-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="fec95-106">Bu seçenekler</span><span class="sxs-lookup"><span data-stu-id="fec95-106">These options are</span></span>

* <span data-ttu-id="fec95-107">GROUP BY ile dökümü</span><span class="sxs-lookup"><span data-stu-id="fec95-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="fec95-108">GRUPLANDIRMA KÜMELERİ</span><span class="sxs-lookup"><span data-stu-id="fec95-108">GROUPING SETS</span></span>
* <span data-ttu-id="fec95-109">GROUP BY ile KÜPÜ</span><span class="sxs-lookup"><span data-stu-id="fec95-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="fec95-110">Toplama ve gruplandırma kümeleri seçenekleri</span><span class="sxs-lookup"><span data-stu-id="fec95-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="fec95-111">Merhaba burada en basit seçenek olan toouse `UNION ALL` güvenmek yerine tooperform hello toplaması açık sözdizimi yerine hello.</span><span class="sxs-lookup"><span data-stu-id="fec95-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="fec95-112">Merhaba sonucu olan tam olarak hello aynı</span><span class="sxs-lookup"><span data-stu-id="fec95-112">hello result is exactly hello same</span></span>

<span data-ttu-id="fec95-113">Aşağıda, bir grubu hello kullanarak deyimi tarafından örneğidir `ROLLUP` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="fec95-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

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

<span data-ttu-id="fec95-114">Toplama kullanarak toplamalar aşağıdaki hello istediniz:</span><span class="sxs-lookup"><span data-stu-id="fec95-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="fec95-115">Ülke ve bölgeye</span><span class="sxs-lookup"><span data-stu-id="fec95-115">Country and Region</span></span>
* <span data-ttu-id="fec95-116">Ülke</span><span class="sxs-lookup"><span data-stu-id="fec95-116">Country</span></span>
* <span data-ttu-id="fec95-117">Genel toplam</span><span class="sxs-lookup"><span data-stu-id="fec95-117">Grand Total</span></span>

<span data-ttu-id="fec95-118">tooreplace bu toouse gerekir `UNION ALL`; açıkça gerekli hello toplamalar belirtme tooreturn hello aynı sonuçları:</span><span class="sxs-lookup"><span data-stu-id="fec95-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

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

<span data-ttu-id="fec95-119">Tüm toodo ihtiyacımız olan benimsemeyi GROUPING SETS asıl aynı hello ancak yalnızca toplama düzeyleri hello için UNION ALL bölümler oluşturma toosee istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fec95-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="fec95-120">Küp seçenekleri</span><span class="sxs-lookup"><span data-stu-id="fec95-120">Cube options</span></span>
<span data-ttu-id="fec95-121">Olası toocreate bir grup tarafından WITH CUBE olduğu hello UNION ALL yaklaşımı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="fec95-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="fec95-122">Merhaba hello kod sıkıcı ve yönetilmeleri hızlı bir şekilde olabilecek bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="fec95-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="fec95-123">toomitigate bu bu yaklaşımı daha gelişmiş kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fec95-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="fec95-124">Yukarıdaki örnekte hello kullanalım.</span><span class="sxs-lookup"><span data-stu-id="fec95-124">Let's use hello example above.</span></span>

<span data-ttu-id="fec95-125">Merhaba ilk adımı toodefine hello 'toocreate istiyoruz toplama tüm hello düzeylerini tanımlar cube' dir.</span><span class="sxs-lookup"><span data-stu-id="fec95-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="fec95-126">Önemli tootake Not hello hello iki türetilmiş tabloların çapraz birleşimi olan.</span><span class="sxs-lookup"><span data-stu-id="fec95-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="fec95-127">Bu tüm hello düzeylerini bize oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fec95-127">This generates all hello levels for us.</span></span> <span data-ttu-id="fec95-128">Merhaba rest hello kod gerçekten biçimlendirme için yoktur.</span><span class="sxs-lookup"><span data-stu-id="fec95-128">hello rest of hello code is really there for formatting.</span></span>

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

<span data-ttu-id="fec95-129">Merhaba Hello sonuçlarını CTAS altında görülebilir:</span><span class="sxs-lookup"><span data-stu-id="fec95-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="fec95-130">Hello ikinci adım, bir hedef tablo toostore geçici sonuçları toospecify şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fec95-130">hello second step is toospecify a target table toostore interim results:</span></span>

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

<span data-ttu-id="fec95-131">Merhaba üçüncü tooloop bizim hello toplama gerçekleştirme sütunları küp üzerinde bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="fec95-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="fec95-132">Merhaba sorgu hello #Cube geçici tablosunda her satır için bir kez çalıştır ve hello #Results geçici tablosunda hello sonuçları deposunu</span><span class="sxs-lookup"><span data-stu-id="fec95-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

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

<span data-ttu-id="fec95-133">Son olarak biz hello #Results geçici tablodaki okuyarak hello sonuçlar döndürebilir</span><span class="sxs-lookup"><span data-stu-id="fec95-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="fec95-134">Merhaba kod bölümlere ayırma ve döngü yapısı hello oluşturma kodu daha yönetilebilir ve sürdürülebilir haline gelir.</span><span class="sxs-lookup"><span data-stu-id="fec95-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fec95-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fec95-135">Next steps</span></span>
<span data-ttu-id="fec95-136">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="fec95-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
