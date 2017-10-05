---
title: "Veritabanı uyumluluk düzeyi 130 - Azure SQL veritabanı | Microsoft Docs"
description: "Bu makalede, Azure SQL veritabanı uyumluluk düzeyinde 130 çalıştıran ve avantajların yanı sıra yeni sorgu iyileştiricisi sorgu işlemci özelliklerini yararlanarak avantajlarını keşfedin. Biz de olası yan etkileri var olan SQL uygulamalar için sorgu performansına adres."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: c08c0690df4f389416e4ed2e2df2dbb72d6fd567
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Azure SQL veritabanı uyumluluk düzeyi 130 ile sorgu performansı geliştirildi
Azure SQL veritabanı saydam yüz binlerce veritabanları birçok farklı uyumluluk düzeylerinde koruma ve onun tüm müşteriler için Microsoft SQL Server'ın ilgili sürümü için geriye dönük uyumluluk güvence altına alır çalışıyor!

Bu makalede, Azure SQL veritabanı uyumluluk düzeyinde 130 çalıştıran ve avantajların yanı sıra yeni sorgu iyileştiricisi sorgu işlemci özelliklerini yararlanarak avantajlarını keşfedin. Biz de olası yan etkileri var olan SQL uygulamalar için sorgu performansına adres.

Geçmiş hatırlatma SQL sürümleri için varsayılan uyumluluk düzeyleri hizalamasını aşağıdaki gibidir:

* 100: SQL Server 2008 ve Azure SQL veritabanı V11.
* 110: SQL Server 2012 ve Azure SQL veritabanı V11.
* 120: SQL Server 2014 ve Azure SQL veritabanı V12.
* 130: SQL Server 2016 ve Azure SQL veritabanı V12.

> [!IMPORTANT]
> İtibariyle **mid-Haziran 2016**, Azure SQL veritabanı'nda varsayılan uyumluluk düzeyi için 120 yerine 130 olacaktır **yeni oluşturulan** veritabanları.
> 
> Mid-Haziran 2016 öncesinde oluşturulan veritabanlarını olacak *değil* etkilenecek ve bunların geçerli uyumluluk düzeyini (100, 110 veya 120) barındırır. İçin V12 Azure SQL veritabanı V11 sürümünden geçirilen veritabanları 100 veya 110 uyumluluk düzeyine sahip. 
> 

## <a name="about-compatibility-level-130"></a>130 uyumluluk düzeyi hakkında
Veritabanınızı geçerli uyumluluk düzeyini bilmek istiyorsanız, ilk olarak, aşağıdaki Transact-SQL deyimini yürütün.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


İçin düzeyine 130 bu değişiklik gerçekleşmeden önce **yeni** veritabanları oluşturuldu, şimdi bu değişiklik hakkında bazı temel sorgu örneklerle nedir gözden geçirin ve herkesin buradan nasıl yararlanabilir bakın.

İlişkisel veritabanları sorgu işleme çok karmaşık olabilir ve için çok sayıda bilgisayar bilimi ve matematik devralınmış tasarım seçenekleri ve davranışlarını anlamak için yol açabilir. Bu belgede, içerik bilerek minimum bazı teknik arka plan kimseyle uyumluluk düzeyi değişikliğin etkisini anlamak ve böylelikle uygulamalar nasıl yararlanabilir belirlemek emin olmak için basitleştirilmiştir.

Şimdi ne uyumluluk düzeyi 130 tablosu getirir en hızlı bir görünüme sahiptir.  Daha fazla bilgi bulabilirsiniz [ALTER veritabanı uyumluluk düzeyi (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), burada ancak kısa bir özeti:

* INSERT select deyiminin ekleme işlemi çok iş parçacıklı olabilir veya bir paralel planınız bu işlem tek iş parçacıklı önce while.
* İyileştirilmiş tablosu ve Tablo değişkenleri sorguları şimdi olabilir paralel planları, bellek çalışırken bu işlem ayrıca tek iş parçacıklı önce.
* Bellek için iyileştirilmiş tablo İstatistikleri şimdi örneklenebilir ve otomatik olarak güncelleştirilir. Bkz: [Veritabanı Altyapısı'ndaki Yenilikler: bellek içi OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) daha fazla ayrıntı için.
* Toplu iş modu v/s satır modunu sütun deposu dizinleri ile değiştirir.
  * Bir sütun deposu dizini olan bir tabloda sıralar toplu iş modunda sunulmuştur.
  * Pencereleme toplamalar şimdi TSQL ÖTELEME/sağlama deyimleri gibi toplu iş modunda çalışır.
  * Birden çok distinct yan tümcelerinde sütun deposu tablolarla sorgulamaları toplu iş modunda çalışır.
  * DOP altında çalışmakta olan sorgulara = 1 veya seri bir plan ile aynı zamanda toplu iş modunda yürütün.
* Son olarak, kardinalite tahmin geliştirmeleri gerçekte 120, uyumluluk düzeyiyle geliyor ancak, düşük bir uyumluluk düzeyde (yani 100 veya 110), uyumluluk için taşıma çalıştıran içeriğiyle için düzeyi 130 Bu geliştirmeler ayrıca getirecek ve bu uygulamaların sorgu performansını da yararlı olabilir.

## <a name="practicing-compatibility-level-130"></a>Alıştırmasını uyumluluk düzeyi 130
İlk şimdi bazı tablolar, dizinler ve bu yeni özelliklerden bazıları alıştırma yapmak için oluşturulmuş rastgele veri alın. TSQL kod örnekleri, Azure SQL veritabanı altında veya SQL Server 2016, çalıştırılabilir. Ancak, bir Azure SQL veritabanı oluşturulurken en az birkaç çoklu iş parçacığı izin vermek ve bu nedenle bu özelliklerinden yararlanmak için çekirdek gerektiğinden P2 veritabanı en azından seçtiğinizden emin olun.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- the second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


Şimdi, şimdi bazı uyumluluk düzeyinde 130 gelen sorgu işleme özelliklerinin bir görünüme sahiptir.

## <a name="parallel-insert"></a>Paralel Ekle
Aşağıdaki TSQL ifadeler çalıştırmasını sırasıyla çalıştırır tek iş parçacıklı model (120) ve çok iş parçacıklı model (130) ekleme işlemi, uyumluluk düzeyi 120 ve 130, altında ekleme işlemi yürütür.

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- The INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- The INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Gerçek grafik gösterimi veya XML içeriğini arayan sorgu planı isteyerek yürütme sırasında işlevidir hangi kardinalite tahmin belirleyebilirsiniz. Şekil 1'üzerinde planları yan yana bakarak açıkça sütun deposu Ekle yürütme 120 seri paralel olarak 130 içinde duruma geçtiğinde, görebiliriz. Ayrıca, artık olgu gösteren iki paralel okları yineleyici yürütme gösteren 130 planında yineleyici simgesinin değişiklik gerçekten paralel olduğuna dikkat edin. Tamamlamak için büyük INSERT işlemlerine varsa, veritabanı için elden en sahip Çekirdek sayısına bağlı Paralel yürütme daha iyi performans gösterir; 100 kez daha hızlı kadar durumunuza bağlı olarak!

*Şekil 1: Ekleme işlemi seri paralel olarak değiştirir 130 ile uyumluluk düzeyi.*

![Şekil 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Seri toplu iş modu
Benzer şekilde, veri satırı işlerken uyumluluk düzeyine 130 taşıma toplu iş modu işleme sağlar. Sütun deposu dizini kullanıyor, ilk olarak, toplu iş modu işlemleri yalnızca kullanılabilir. İkinci olarak, bir toplu genellikle ~ 900 satırları temsil eder ve çok çekirdekli CPU, daha yüksek bellek verimliliği en iyi hale getirilmiş bir kod mantığını kullanır ve mümkün olduğunca sütun deposu sıkıştırılmış verileri doğrudan yararlanır. Bu koşullar altında SQL Server 2016 ~ 900 satır aynı anda 1 satır zaman yerine işleyebilir ve sonuç olarak, genel maliyeti işlemi şimdi satır maliyet genel azaltma tüm toplu işlem tarafından paylaşılır. Sütun deposu sıkıştırmaya temelde birleştirilmiş işlemlerinin paylaşılan bu miktar seçin toplu iş modu işlemde yer alan gecikmesini azaltır. Sütun deposu hakkında daha fazla bilgi bulmak ve toplu iş modunda [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Olarak aşağıda görünür, sorgu Şekil 2'üzerinde yan yana planları, parolanızı izlenerek işleme modunu uyumluluk düzeyiyle değişti ve sonuç olarak, sorguları her iki uyumluluk düzeyi tamamen yürütürken, işleme süresinin en görebiliriz görür toplu iş modunda (%14), burada 2 toplu işlenen karşılaştırıldığında row modunda (%86) harcanmaktadır. Veri kümesi artırın, avantajı artmasına neden olur.

*Şekil 2: işlemi değişiklikleri seri toplu iş modunda 130 uyumluluk düzeyiyle seçin.*

![Şekil 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Sıralama yürütme toplu iş modu
Yukarıda, ancak sıralama işlemi uygulanan benzer toplu iş modunda (uyumluluk düzeyi 130) satır modu (uyumluluk düzeyi 120) geçiş aynı nedenden dolayı sıralama işlemi performansını artırır.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- The scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- The scan and aggregate are in batch mode,
-- and force MAXDOP to 1 to show that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Toplu iş modunda yalnızca bir maliyetinin (sırasıyla %81 ve sıralama %56) % 19 temsil ederken, Satır modunda sıralama işlemi %81 maliyetinin temsil eden görünür yan yana Şekil 3'üzerinde görebiliriz.

*Şekil 3: Sıralama işlemi satırdan toplu iş modunda uyumluluk düzeyi 130 ile değiştirir.*

![Şekil 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Belli ki, bu örnekler yalnızca on binlerce satır, hiçbir şey çoğu SQL sunucuları kullanılabilir veri bugünlerde bakıldığında olduğu içerir. Yalnızca bu milyonlarca satır karşı yerine proje ve bu birkaç dakika bekleyen İş yükünüzün yapısını her gün kullanımdan yürütme çevirebilir.

## <a name="cardinality-estimation-ce-improvements"></a>Kardinalite tahmin (CE) geliştirmeleri
SQL Server 2014 ile sunulan, bir uyumluluk düzeyi 120 veya üstü çalıştıran herhangi bir veritabanı yeni kardinalite tahmin kullanın yapar işlevselliği. Esas olarak, SQL server tahmini maliyetine bağlı bir sorgu nasıl yürütüleceği belirlemek için kullanılan mantığı kardinalite tahmin olur. Tahmin, sorguda kullanılan nesneleri ile ilişkili istatistikleri girişten kullanılarak hesaplanır. Pratikte, en üst düzey, kardinalite tahmin işlevleri tahminidir satır sayısı ayrı değer sayıları değerlerin dağıtımı hakkında bilgi ile birlikte ve yinelenen sayıları bulunan tabloları ve sorguda başvurulan nesneler. Bu tahminler yanlış alınıyor, bellek yetersiz verir (yani TempDB sıvı sıçraması) nedeniyle gereksiz disk g/ç veya seri planı yürütme seçimi paralel plan yürütme birkaçıdır yol açabilir. Sonuç, yanlış tahminleri sorgu yürütme için bir genel performans düşüşüne neden olabilir. Diğer tarafta daha iyi tahminler, daha doğru tahminler daha iyi sorgu yürütmeleri müşteri adayları!

Önceden belirtildiği gibi sorgu en iyi duruma getirme ve tahmin karmaşık sağlasa da, ancak sorgu planları ve kardinalite tahmin hakkında daha fazla bilgi edinmek istiyorsanız, belge başvurabilirsiniz [en iyi duruma getirme bilgisayarınızı sorgu planları ile SQL Server 2014 kardinalite tahmin](https://msdn.microsoft.com/library/dn673537.aspx) daha ayrıntılı bilgi edinmek için.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Hangi kardinalite tahmin, şu anda kullanıyor musunuz?
Belirlemek için hangi kardinalite sorgularınızı çalıştığını tahmini altında yalnızca aşağıdaki sorgu örnekleri kullanalım. Bu ilk örnek eski kardinalite tahmin işlevleri kullanımını olduğunu belirtmek uyumluluk düzeyi altında 110, çalışacağını unutmayın.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Yürütme tamamlandıktan sonra XML bağlantısına tıklayın ve aşağıda gösterildiği gibi ilk yineleyici özelliklerine bakın. Şu anda 70 üzerinde ayarlanmış CardinalityEstimationModelVersion adlı özellik adını not edin. Veritabanı uyumluluk düzeyi (bunu 110 yukarıdaki TSQL deyimlerinde görünür olarak ayarlanan) SQL Server 7.0 sürümü için ayarlanmış, ancak 70 değeri yalnızca ana düzeltme yok (Uyumluluk düzeyinde 120 desteklemektedir) SQL Server 2014 kadar olan SQL Server 7.0 sürümünden itibaren kullanılabilir eski kardinalite tahmin işlevselliği temsil eder anlamına gelmez.

*Şekil 4: Uyumluluk düzeyi 110 veya aşağıda kullanırken CardinalityEstimationModelVersion 70 için ayarlanır.*

![Şekil 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Alternatif olarak, uyumluluk düzeyi için 130 değiştirebilir ve on ile ayarlamak LEGACY_CARDINALITY_ESTIMATION kullanarak yeni kardinalite tahmin işlevi kullanımını devre dışı [ALTER veritabanı kapsamlı yapılandırma](https://msdn.microsoft.com/library/mt629158.aspx). Bu tam olarak 110 açısından bir kardinalite tahmin işlevi, en son sorgu uyumluluk düzeyi işleme kullanırken aynı olacaktır. Bunun yapılması, yeni sorgu en son uyumluluk düzeyiyle (yani, toplu iş modu) gelen özellikleri işleme yararlı ancak hala gerekirse eski kardinalite tahmin işlevselliğini kullanır.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Yalnızca uyumluluk düzeyi 120 veya 130 taşıma yeni kardinalite tahmin işlevsellik sağlar. Böyle bir durumda, varsayılan CardinalityEstimationModelVersion buna uygun olarak ayarlanacak 120 veya 130 altında görünür.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Şekil 5: CardinalityEstimationModelVersion 130 uyumluluk düzeyini kullanırken 130 için ayarlanır.*

![Şekil 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a>Kardinalite tahmin farklar witnessing
Şimdi, Şimdi Çalıştır biraz daha karmaşık bir INNER JOIN WHERE yan tümcesi ile bazı koşullar ile ilgili sorgu ve satır sayısı tahmini eski kardinalite tahmin işlevinden önce bakalım.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Eski kardinalite tahmin işlevsellikle satır tahmini 194,284 satırları talep ederken etkili bir şekilde bu sorgu yürütülmeden 200.704 satırları döndürür. Belli ki, önce denirse gibi bu satır sayısı sonuçlarını da ne sıklıkta, önceki örnekleri, örnek tablolara her çalıştırmayı tekrar tekrar doldurur çalıştırıldığı bağlıdır. Tabii ki sorgunuzu koşullarında ayrıca veri içeriğini, tablo şekli yanı sıra gerçek tahmin üzerinde bir etkisi olacaktır ve nasıl bu verilerin gerçekte bağıntısını birbirleri ile.

*Şekil 6: Satır sayısı tahmini 194,284 ya da 6,000 satır beklenen 200.704 satırların kapalıdır.*

![Şekil 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

Aynı şekilde, şimdi artık aynı sorguyu yeni kardinalite tahmin işlevselliği ile çalıştırın.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Bakarak Aşağıda, biz artık satır tahmini 202,877, veya çok daha yakından ve eski kardinalite tahmin daha yüksek olduğunu görebilirsiniz.

*Şekil 7: Satır sayısı tahmini 194,284 yerine 202,877 sunulmuştur.*

![Şekil 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

Gerçekte, sonuç kümesi 200.704 satırları bağlıdır (ancak tamamını bağlıdır önceki örnek sorguları ne sıklıkta karşılaştınız, ancak TSQL RAND() deyimi kullandığından daha da önemlisi, döndürülen gerçek değerler bir çalışmadan diğerine sonraki farklı olabilir). Bu nedenle, bu örnekte yeni kardinalite tahmin 202,877 194,284 200,704 için daha yakından olduğundan satır sayısını tahmin etme sırasında daha iyi iş değil! WHERE yan tümcesi eşitlik için doğrulamaları değiştirirseniz, en son (yerine ">" örneği için), bu eski arasında tahminleri yapabilir ve yeni nicelik işlevi kaç, eşleşen bağlı olarak daha da farklı alabilirsiniz.

Belli ki, bu durumda, gerçek sayısını ~ 6000 satırları devre dışı bırakılıyor çok miktarda veri bazı durumlarda temsil etmiyor. Şimdi, milyonlarca satır ve bu nedenle, çekme yukarı yanlış yürütme planı veya yetersiz bellek verir TempDB sıvı sıçraması ve bu nedenle daha fazla g/ç, yol isteyen riskini bu birden çok tablo ve daha karmaşık sorgular ve bazen tahmin satırlarda milyonlarca kapalı olabilir devrik çok daha yüksek.

Alıştırma fırsat varsa en tipik sorgular ve veri kümeleri, bu karşılaştırma ve ne kadar eski ve yeni tahminleri bazıları etkilendiğini, bazı yalnızca daha fazla devre dışı gerçekte veya bazı başkalarına yalnızca yalnızca daha yakın gerçek satır hale gelebilir sırada sonuç kümelerinde gerçekte döndürülen sayıları kendiniz için bkz. Tamamını sorgularınızı, Azure SQL veritabanı özellikleri, yapısı ve boyutunu, veri kümeleri ve bunlarla ilgili kullanılabilir istatistikleri şeklin bağlı olacaktır. Azure SQL veritabanı örneğinde oluşturduysanız, sorgu iyileştiricisi bildiğini önceki sorgu çalışmalarını yapılan istatistikleri yeniden kullanmak yerine sıfırdan yapı gerekecektir. Bu nedenle, çok bağlamsal ve neredeyse her sunucu ve uygulama durumunuza özel tahmin eder. Dikkate alınması gereken önemli bir durum değil!

## <a name="some-considerations-to-take-into-account"></a>Dikkate almanız gereken bazı noktalar
Çoğu iş yükleri için üretim ortamınız için uyumluluk düzeyi'nu benimseme önce uyumluluk düzeyinin 130, yararlı olsa da, temel olarak 3 seçeneğiniz vardır:

1. Uyumluluk düzeyi 130 taşıyın ve nasıl şeyleri gerçekleştirmek bakın. Bazı gerileme dikkat edin, yalnızca yalnızca özgün düzeyine uyumluluk düzeyi ayarlayın veya 130 Koru ve yalnızca geriye doğru kardinalite tahmin geri eski modu durumunda (yukarıda açıklandığı şekilde, bu tek başına soruna).
2. Mevcut uygulamalarınızı benzer üretim yük altında sınamanız ince ve üretime geçmeden önce performansını doğrulama. Hataları durumunda aynı yukarıdaki her zaman özgün uyumluluk düzeyine geri dönün veya için yalnızca eski moda kardinalite tahmin ters çevir.
3. Son seçenek, bu soruları için en son yol, Query Store yararlanmak için ise. Günümüzün önerilen seçenek olan! Sorgularınızı uyumluluk altında analizini yardımcı olmak için 120 düzeyinde veya altında 130 karşı yeterince sorgu deposu kullanmak için öneririz olamaz. Query Store Azure SQL Database V12 en son sürümü ile kullanılabilir ve sorgu performansı sorun giderme konusunda yardımcı olmak için tasarlanmıştır. Sorgu deposu veritabanınızın toplama ve tüm sorguları hakkında ayrıntılı geçmiş bilgileri sunan bir uçuş veri Kaydedici olarak düşünün. Bu önemli ölçüde performans hukuk tanılamak ve sorunları gidermek için zamanı azaltarak basitleştirir. Daha fazla bilgi bulabilirsiniz [sorgu deposu: uçuş veri Kaydedici veritabanınız için](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

En üst düzey, zaten 120 uyumluluk düzeyinde veya altında çalışan veritabanları kümesine sahiptir ve bunların bazıları için 130 taşımak veya İş yükünüzün otomatik olarak sağlamak için olacak yeni veritabanlarını hemen 130, varsayılan olarak ayarlanması düşünüyorsanız lütfen göz önünde bulundurun aşağıdakilere:

* Yeni uyumluluk düzeyini üretimde değiştirmeden önce Query Store etkinleştirin. Başvurabilirsiniz [veritabanı Uyumluluk modunu değiştirme ve sorgu deposu kullanmanız](https://msdn.microsoft.com/library/bb895281.aspx) daha fazla bilgi için.
* Ardından, tüm kritik iş yükleri temsilcisi veri ve bir üretim benzeri bir ortam ve karşılaştırma yaşadı performans ve sorgu deposu tarafından bildirilen olarak sorgularını kullanarak test edin. Bazı gerileme karşılaşırsanız, Query Store gerileyen sorgularıyla tanımlamak ve sorgu deposu seçeneği zorlama planını kullan (diğer adıyla sabitleme plan). Böyle bir durumda, tam olarak uyumluluk düzeyiyle 130 kalır ve eski sorgu planı Query Store tarafından önerilen olarak kullanın.
* Yeni özellik ve yetenekler (hangi SQL Server 2016 çalıştığı) Azure SQL veritabanı'nın yararlanmak isteyen, ancak son çare olarak 130, uyumluluk düzeyine göre duruma değişikliklere duyarlıdır uyumluluk düzeyini tekrar İş yükünüzün bir ALTER DATABASE deyimini kullanarak en çok uyan düzeyine zorlama düşünebilirsiniz. Ancak, ilk olarak, 130 kullanmayan daha eski bir SQL Server sürümü işlev düzeyinde temelde kalıyor çünkü seçeneği sabitleme Query Store planı sizin için en iyi seçenek olduğunu unutmayın.
* Birden çok veritabanı kapsayıcı çok müşterili uygulamalarınız varsa, veritabanlarınızın tüm veritabanları arasında tutarlı uyumluluk düzeyini sağlamak için sağlama mantığı güncelleştirmek gerekli olabilir; eski ve yeni sağlanan olanlar. Uygulama iş yükü performansınızı bazı veritabanları farklı uyumluluk düzeylerinde çalıştıran olgu hassas olabilir ve bu nedenle, üzerinde herhangi bir veritabanı uyumluluk düzeyinde tutarlılık tüm Panosu müşterilerinize aynı deneyimi sağlamak için gerekli olabilir. Bir zorunluluğuna değil, gerçekten nasıl uyumluluk düzeyine göre uygulamanızın etkilenen bağlıdır dikkat edin.
* Son olarak, kardinalite tahmin ilgili ve üretim, devam etmeden önce uyumluluk düzeyini değiştirme gibi üretim İş yükünüzün uygulamanızı kardinalite tahmin geliştirmelerden faydalanabilmeniz avantaj ise belirlemek için yeni koşullar altında test etmek için önerilir.

## <a name="conclusion"></a>Sonuç
Tüm SQL Server 2016 iyileştirmeleriyle yararlanmak için Azure SQL veritabanı kullanarak, sorgu yürütmeleri açıkça artırabilir. Gibi-değil! Elbette, herhangi bir yeni özelliği gibi doğru bir değerlendirme altında veritabanının yükünüzü en iyi faaliyet tam koşullarını belirlemek için yapılması gerekir. Çoğu iş yükü beklenen saydam 130, uyumluluk düzeyi altında yeni sorgu işlevleri ve yeni kardinalite tahmin işleme yararlanarak sırasında çalışması için en az deneyimi gösterir. Olan gerçekçi olarak, her zaman bazı özel durumlar belirtti ve uygun son yapılması tespitlerini bu iyileştirmeleriyle ne kadar fayda belirlemek için önemli bir değerlendirme. Ve yeniden, Query Store bu çalışarak harika Yardım olabilir!

SQL Azure geliştikçe uyumluluk düzeyi 140 gelecekte bekleyebilirsiniz. Zaman uygun olduğunda, biz yalnızca biz kısaca burada uyumluluk seviyesi 130 bugün getiren anlatıldığı gibi ne bu ileriye dönük uyumluluk düzeyi 140 getirecek, Konuşmayı başlar.

Şimdilik, şimdi değil unutursanız, Haziran 2016'dan başlayarak, Azure SQL veritabanı varsayılan uyumluluk düzeyi 120-yeni oluşturulan veritabanları için 130 değiştirir. Dikkat!

## <a name="references"></a>Başvurular
* [Veritabanı Altyapısı'nda yenilikler nelerdir?](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blog: Sorgu deposu: Borko Novakovic, 8 Haziran 2016 tarafından veritabanınız için uçuş veri Kaydedicisi](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [ALTER veritabanı uyumluluk düzeyi (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER VERİTABANI KAPSAMLI YAPILANDIRMA](https://msdn.microsoft.com/library/mt629158.aspx)
* [Azure SQL Database V12 için uyumluluk düzeyi 130](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Sorgunuz en iyi duruma getirme ile SQL Server 2014 kardinalite tahmin planları](https://msdn.microsoft.com/library/dn673537.aspx)
* [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx)
* [Blog: İyileştirilmiş sorgu performansı Alain Lissoir tarafından uyumluluk düzeyi 130 Azure SQL veritabanında olan 6 Mayıs 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
