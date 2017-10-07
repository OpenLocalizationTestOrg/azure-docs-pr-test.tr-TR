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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>SQL veri ambarı'nda create Table As Select (CTAS)
Tablo seçin olarak oluşturun veya `CTAS` hello en önemli T-SQL özelliklerini biridir. SELECT deyiminin hello çıktıya dayalı yeni bir tablo oluşturur tam olarak parallelized bir işlemdir. `CTAS`Merhaba basit ve hızlı yolu toocreate bir tablonun bir kopyasıdır. Bu belge örnekleri ve en iyi yöntemleri sağlar `CTAS`.

## <a name="selectinto-vs-ctas"></a>SEÇİN... VS. CTAS
Göz önünde bulundurabilirsiniz `CTAS` Süper kartınızdan bir sürümü olarak `SELECT..INTO`.

Basit bir örneği aşağıdadır `SELECT..INTO` deyimi:

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

Yukarıdaki hello örnekte `[dbo].[FactInternetSales_new]` hello tablo Varsayılanları Azure SQL Data warehouse'da bunlar gibi üzerindeki kümelenmiş COLUMNSTORE dizini olan ROUND_ROBIN dağıtılmış tablosu olarak oluşturulması.

`SELECT..INTO`Ancak, her iki hello dağıtım yöntemini veya hello dizinini yazın hello işleminin bir parçası toochange izin vermez. Bu yerdir `CTAS` devreye girer.

çok hello yukarıda tooconvert`CTAS` oldukça düz-bir işlemdir:

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

İle `CTAS` mümkün toochange olduğunuz her ikisi de hello tablo türü yanı sıra hello tablo verisi dağıtımını hello. 

> [!NOTE]
> Toochange hello dizinde yalnızca çalışıyorsanız, `CTAS` işlemi ve hello kaynak tablodur dağıtılmış karma sonra `CTAS` işlemi gerçekleştirecek, sahipseniz en iyi hello aynı dağıtım sütun ve veri türü. Bu dağıtım veri taşıma daha etkili olan hello işlemi sırasında kaçının.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>CTAS toocopy tablo kullanma
Belki de hello en yaygın birini kullanır `CTAS` hello DDL geçiş yapabilmeniz sağlayan bir tablonun kopyasını oluşturma. Örneğin, tablo olarak başlangıçta oluşturduysanız `ROUND_ROBIN` ve değiştirmek istediğiniz şimdi onu tooa tablo dağıtılmış bir sütuna, `CTAS` nasıl hello dağıtım sütun değiştirme olduğu. `CTAS`Ayrıca kullanılan toochange bölümlendirme, dizin oluşturma veya sütun türleri olabilir.

Bu tablo hello varsayılan dağıtım türünü kullanarak oluşturduğunuz düşünelim `ROUND_ROBIN` hiçbir dağıtım sütun hello belirtilmediğinden dağıtılmış `CREATE TABLE`.

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

Şimdi kümelenmiş Columnstore tabloları hello performansını yararlanabilir böylece toocreate Bu tablo bir kümelenmiş Columnstore dizini ile yeni bir kopyasını istiyorsunuz. Bu sütunda birleştirmeler bekleme ve ProductKey üzerinde birleştirme sırasında tooavoid veri taşıma istiyorsanız bu yana ProductKey bu tabloda toodistribute da isteyebilirsiniz. Son olarak, böylece eski bölümleri bırakarak, eski verileri hızlı bir şekilde silebilirsiniz tooadd OrderDateKey üzerinde bölümleme da isteyebilirsiniz. Burada, eski tablonuz yeni bir tabloya kopyalarsınız hello CTAS deyimi verilmiştir.

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

Son olarak, tablolar tooswap yeni tablonuzda yeniden adlandırın ve eski tablonuz bırakın.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.  Sipariş tooget hello en iyi performansı sorgularınızı, istatistikleri hello ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda oluşturulması önemlidir veya hello verilerde önemli değişikliklerden.  Merhaba istatistikleri ayrıntılı bir açıklaması için bkz [istatistikleri] [ Statistics] konu hello geliştirme grubunu konuda.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>Desteklenmeyen özellikler etrafında CTAS toowork kullanma
`CTAS`Aşağıda listelenen desteklenmeyen hello özelliklerini geçici kullanılan toowork de olabilir. Yalnızca kodunuzun uyumlu olur ancak bu genellikle daha hızlı SQL Data Warehouse yürütülmez bu genellikle bir win/win durum toobe kanıtlayabilirsiniz. Tam olarak parallelized tasarımını sonucunda budur. Geçici CTAS ile çalışılabilecek senaryolar şunlardır:

* ANSI BİRLEŞTİRMELER güncelleştirmeleri
* ANSI birleştirmeler üzerinde siler
* MERGE deyimi

> [!NOTE]
> Toothink deneyin "CTAS ilk". Kullanarak bir sorunu çözebilir düşünüyorsanız `CTAS` , genellikle hello en iyi şekilde tooapproach sonra onu - daha fazla veri sonuç olarak yazıyorsanız, hatta.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>ANSI birleştirme değiştirme için güncelleştirme deyimleri
Sözdizimi tooperform hello birleştirme ANSI kullanılarak güncelleştirme veya silme ikiden fazla tabloyu birleştiren karmaşık bir güncelleştirmeye sahip bulabilirsiniz.

Bu tabloda tooupdate olduğunu varsayalım:

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

Merhaba özgün sorgu şöyle bir şey attıktan:

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

SQL veri ambarı desteklemediği beri ANSI hello birleştirmeleri `FROM` yan tümcesinde bir `UPDATE` deyimi, biraz değiştirmeden üzerinden bu kodu kopyalayamıyor.

Bir bileşimini kullanabilirsiniz bir `CTAS` ve bir örtük bu kodu tooreplace Katıl:

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

## <a name="ansi-join-replacement-for-delete-statements"></a>ANSI birleştirme yerini silme deyimleri
Bazen veri silmek için hello en iyi toouse yaklaşımdır `CTAS`. Merhaba verileri yalnızca silme yerine tookeep istediğiniz hello verileri seçin. Bu özellikle true `DELETE` ANSI SQL veri ambarı hello ANSI birleştirmeler desteklemediğinden sözdizimi birleştirme kullan deyimleri `FROM` yan tümcesinde bir `DELETE` deyimi.

Dönüştürülen DELETE deyimi örneği aşağıda kullanılabilir:

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

## <a name="replace-merge-statements"></a>Merge deyimlerinde değiştirin
Merge deyimlerinde değiştirilebilir, en az bölümünde kullanarak `CTAS`. Merhaba birleştirebilir `INSERT` ve hello `UPDATE` tek bir deyimde içine. Silinmiş kayıtları kapalı ikinci bir deyimde kapalı toobe gerekir.

Örnek olarak bir `UPSERT` aşağıda verilmiştir:

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>CTAS öneri: açıkça durumunda veri türü ve çıktı olabilirliği
Kod geçirirken bu tür bir kodlama düzeni çalıştırmak bulabilirsiniz:

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

İnstinctively bu kodu tooa CTAS geçirmeniz gerekir ve doğru olacaktır düşünebilirsiniz. Ancak, burada gizli bir sorun yoktur.

Merhaba aşağıdaki kodu değil verim hello aynı sonucu:

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

Merhaba sütun "sonuç" İleri hello ifadesinin hello veri türü ve null atanabilirlik değerleri taşıyan dikkat edin. Dikkatli değilseniz, bu değerleri toosubtle Varyanslar neden olabilir.

Örnek olarak Hello aşağıdakileri deneyin:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

sonuç için saklanan hello değeri farklıdır. Hello hello sonuç sütunu kalıcı değerinde diğer kullanıldıkça ifadeleri hello hata daha önemli hale gelir.

![][1]

Bu veri geçişler için özellikle önemlidir. Merhaba ikinci sorguyu tartışmaya açık bir şekilde daha doğru olsa bile bir sorun yoktur. Hello veri farklı karşılaştırılan toohello kaynak sistemi olacaktır ve bütünlüğü tooquestions hello geçişte yol açar. Bu, hello "yanlış" yanıt gerçekte hello sağa bir olduğu bu nadir durumlarda biridir!

Merhaba Biz bu farklılığa hello iki sonuçları arasında bkz tooimplicit nedeni atama yazın. Hello ilk örnek Merhaba tablonun hello sütun tanımı tanımlar. Merhaba satır eklendiğinde, bir örtük tür dönüştürme oluşur. Merhaba ikinci örnekte yoktur örtük tür dönüştürme gibi hello ifade hello sütunun veri türünü tanımlar. Hello ilk örnekte, henüz ancak aynı zamanda hello ikinci örnek hello sütunda boş değer atanabilir sütun olarak tanımlanmış dikkat edin. Merhaba tablo içinde oluşturulduğu sırada hello ilk örnek sütun null atanabilirlik açıkça tanımlandı. Merhaba ikinci örnekte toohello ifade yalnızca bırakıldı ve varsayılan olarak bu NULL tanımında neden olur.  

Bu sorunları tooresolve açıkça ayarlamalıdır hello tür dönüştürmeleri ve null atanabilirlik hello `SELECT` hello kısmı `CTAS` deyimi. Bunlar ayarlanamıyor hello özelliklerinde tablo kısmen oluşturulamıyor.

Aşağıdaki Hello örnek nasıl toofix hello kodu gösterir.

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Merhaba aşağıdakileri göz önünde bulundurun:

* CAST veya CONVERT kullanılan
* IsNull kullanılan tooforce null Atanabilirlik olmayan birleşim değil
* IsNull hello en dıştaki işlevidir
* Merhaba ikinci hello IsNull parçası olan bir sabit yani 0

> [!NOTE]
> Merhaba null atanabilirlik toobe doğru şekilde ayarlanması önemli toouse aranır `ISNULL` ve `COALESCE`. `COALESCE`belirleyici bir işlev değil ve bu nedenle hello ifadenin hello sonucu null atanabilir her zaman olacaktır. `ISNULL`farklıdır. Belirleyici. Bu nedenle zaman hello hello ikinci bölümü `ISNULL` işlevidir bir sabit ya da bir hazır değer sonra hello elde edilen değer NULL.
> 
> 

Bu ipucu, hesaplamalar hello bütünlüğünü sağlamak için yalnızca kullanışlı değildir. Bölüm tablo geçmek için önemlidir. Bu tablo, olgu tanımlanan olduğunu düşünün:

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

Ancak, hello değeri alanı hello kaynak veri parçası olmayan bir hesaplanan ifadesidir.

toocreate isteyebileceğiniz toodo bu bölümlenmiş kümenizi:

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

Merhaba sorgu mükemmel iyi çalışır. tooperform hello bölüm anahtarı çalıştığınızda hello sorun gelir. Merhaba tablo tanımları eşleşmiyor. toomake hello tablo tanımları değiştiren toobe CTAS gereken hello eşleşir.

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

Bu nedenle, türü tutarlılık ve bir CTAS null atanabilirlik özellikleri koruma iyi bir mühendislik en iyi uygulama olduğunu görebilirsiniz. Toomaintain bütünlüğü, hesaplamalarda yardımcı olur ve ayrıca bölüm değiştirme mümkün olmasını sağlar.

Kullanma hakkında daha fazla bilgi için lütfen tooMSDN bakın [CTAS][CTAS]. Azure SQL Data Warehouse en önemli deyimlerinde hello biridir. İyice anladığınızdan emin olun.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
