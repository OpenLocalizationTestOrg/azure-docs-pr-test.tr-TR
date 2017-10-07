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
# <a name="group-by-options-in-sql-data-warehouse"></a>SQL veri ambarı seçeneklerinde göre gruplandırmak
Merhaba [GROUP BY] [ GROUP BY] yan tümcesinde kullanılan tooaggregate veri tooa Özet satır kümesi. Ayrıca, geçici doğrudan Azure SQL Data Warehouse tarafından desteklenmiyor gibi çalıştığını bu gereksinimi toobe cihazın işlevselliğini genişleten birkaç seçenek vardır.

Bu seçenekler

* GROUP BY ile dökümü
* GRUPLANDIRMA KÜMELERİ
* GROUP BY ile KÜPÜ

## <a name="rollup-and-grouping-sets-options"></a>Toplama ve gruplandırma kümeleri seçenekleri
Merhaba burada en basit seçenek olan toouse `UNION ALL` güvenmek yerine tooperform hello toplaması açık sözdizimi yerine hello. Merhaba sonucu olan tam olarak hello aynı

Aşağıda, bir grubu hello kullanarak deyimi tarafından örneğidir `ROLLUP` seçeneği:

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

Toplama kullanarak toplamalar aşağıdaki hello istediniz:

* Ülke ve bölgeye
* Ülke
* Genel toplam

tooreplace bu toouse gerekir `UNION ALL`; açıkça gerekli hello toplamalar belirtme tooreturn hello aynı sonuçları:

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

Tüm toodo ihtiyacımız olan benimsemeyi GROUPING SETS asıl aynı hello ancak yalnızca toplama düzeyleri hello için UNION ALL bölümler oluşturma toosee istiyoruz.

## <a name="cube-options"></a>Küp seçenekleri
Olası toocreate bir grup tarafından WITH CUBE olduğu hello UNION ALL yaklaşımı kullanarak. Merhaba hello kod sıkıcı ve yönetilmeleri hızlı bir şekilde olabilecek bir sorundur. toomitigate bu bu yaklaşımı daha gelişmiş kullanabilirsiniz.

Yukarıdaki örnekte hello kullanalım.

Merhaba ilk adımı toodefine hello 'toocreate istiyoruz toplama tüm hello düzeylerini tanımlar cube' dir. Önemli tootake Not hello hello iki türetilmiş tabloların çapraz birleşimi olan. Bu tüm hello düzeylerini bize oluşturur. Merhaba rest hello kod gerçekten biçimlendirme için yoktur.

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

Merhaba Hello sonuçlarını CTAS altında görülebilir:

![][1]

Hello ikinci adım, bir hedef tablo toostore geçici sonuçları toospecify şöyledir:

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

Merhaba üçüncü tooloop bizim hello toplama gerçekleştirme sütunları küp üzerinde bir adımdır. Merhaba sorgu hello #Cube geçici tablosunda her satır için bir kez çalıştır ve hello #Results geçici tablosunda hello sonuçları deposunu

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

Son olarak biz hello #Results geçici tablodaki okuyarak hello sonuçlar döndürebilir

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Merhaba kod bölümlere ayırma ve döngü yapısı hello oluşturma kodu daha yönetilebilir ve sürdürülebilir haline gelir.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
