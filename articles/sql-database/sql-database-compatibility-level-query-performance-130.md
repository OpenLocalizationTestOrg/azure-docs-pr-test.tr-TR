---
title: "aaaDatabase uyumluluk düzeyi 130 - Azure SQL veritabanı | Microsoft Docs"
description: "Bu makalede, Azure SQL veritabanı uyumluluk düzeyinde 130 çalıştıran ve hello yeni sorgu iyileştiricisi hello avantajlarından yararlanarak hello avantajlarını keşfedin ve işlemci özelliklerini sorgulayabilirsiniz. Biz de hello olası yan etkileri hello sorgu performansı hello mevcut SQL uygulamalar için adres."
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
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Azure SQL veritabanı uyumluluk düzeyi 130 ile sorgu performansı geliştirildi
Azure SQL veritabanı saydam yüz binlerce veritabanları birçok farklı uyumluluk düzeylerinde koruma ve kendi müşteriler için Microsoft SQL Server'ın hello geriye dönük uyumluluk toohello karşılık gelen sürüm güvence altına alır çalışıyor!

Bu makalede, Azure SQL veritabanı uyumluluk düzeyinde 130 çalıştıran ve hello yeni sorgu iyileştiricisi hello avantajlarından yararlanarak hello avantajlarını keşfedin ve işlemci özelliklerini sorgulayabilirsiniz. Biz de hello olası yan etkileri hello sorgu performansı hello mevcut SQL uygulamalar için adres.

Geçmiş hatırlatma SQL sürümleri toodefault Uyumluluk Düzeyleri hello hizalamasını aşağıdaki gibidir:

* 100: SQL Server 2008 ve Azure SQL veritabanı V11.
* 110: SQL Server 2012 ve Azure SQL veritabanı V11.
* 120: SQL Server 2014 ve Azure SQL veritabanı V12.
* 130: SQL Server 2016 ve Azure SQL veritabanı V12.

> [!IMPORTANT]
> İtibariyle **mid-Haziran 2016**, Azure SQL veritabanı'nda hello varsayılan uyumluluk düzeyi için 120 yerine 130 olacaktır **yeni oluşturulan** veritabanları.
> 
> Mid-Haziran 2016 öncesinde oluşturulan veritabanlarını olacak *değil* etkilenecek ve bunların geçerli uyumluluk düzeyini (100, 110 veya 120) barındırır. V11 tooV12 Azure SQL veritabanı sürümünden geçirilen veritabanları 100 veya 110 uyumluluk düzeyine sahip. 
> 

## <a name="about-compatibility-level-130"></a>130 uyumluluk düzeyi hakkında
Tooknow hello geçerli uyumluluk düzeyini veritabanınızı istiyorsanız, ilk olarak, Transact-SQL deyimi aşağıdaki hello yürütün.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Bu değişiklikten önce için toolevel 130 gerçekleşir **yeni** veritabanları oluşturuldu, şimdi bu değişiklik hakkında bazı temel sorgu örneklerle nedir gözden geçirin ve herkesin buradan nasıl yararlanabilir bakın.

İlişkisel veritabanları sorgu işleme çok karmaşık olabilir ve bilgisayar Bilim ve matematik toounderstand hello devralınmış tasarım seçenekleri ve davranışları toolots yol açabilir. Bu belgede, bazı minimum teknik arka plan kimseyle hello uyumluluk düzeyi değişiklik hello etkisini anlamak ve böylelikle uygulamalar nasıl yararlanabilir belirlemek bilerek Basitleştirilmiş tooensure hello içerik kaldırıldı.

Şimdi ne hello uyumluluk düzeyi 130 hello tablosu getirir en hızlı bir görünüme sahiptir.  Daha fazla bilgi bulabilirsiniz [ALTER veritabanı uyumluluk düzeyi (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), burada ancak kısa bir özeti:

* Hello INSERT select deyiminin ekleme işlemi çok iş parçacıklı olabilir veya bir paralel planınız bu işlem tek iş parçacıklı önce while.
* İyileştirilmiş tablosu ve Tablo değişkenleri sorguları şimdi olabilir paralel planları, bellek çalışırken bu işlem ayrıca tek iş parçacıklı önce.
* Bellek için iyileştirilmiş tablo İstatistikleri şimdi örneklenebilir ve otomatik olarak güncelleştirilir. Bkz: [Veritabanı Altyapısı'ndaki Yenilikler: bellek içi OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) daha fazla ayrıntı için.
* Toplu iş modu v/s satır modunu sütun deposu dizinleri ile değiştirir.
  * Bir sütun deposu dizini olan bir tabloda sıralar toplu iş modunda sunulmuştur.
  * Pencereleme toplamalar şimdi TSQL ÖTELEME/sağlama deyimleri gibi toplu iş modunda çalışır.
  * Birden çok distinct yan tümcelerinde sütun deposu tablolarla sorgulamaları toplu iş modunda çalışır.
  * DOP altında çalışmakta olan sorgulara = 1 veya seri bir plan ile aynı zamanda toplu iş modunda yürütün.
* Son olarak, kardinalite tahmin geliştirmeleri uyumluluk düzeyi 120 olan, ancak bu, düşük bir uyumluluk düzeyi çalıştıran (yani 100 veya 110) için gerçekten geliyor, hello taşıma toocompatibility düzeyi 130 de bu geliştirmeler getirecek ve bunlar da kullanabilirsiniz Merhaba sorgu uygulamalarınızın performansını yararlanır.

## <a name="practicing-compatibility-level-130"></a>Alıştırmasını uyumluluk düzeyi 130
İlk bu yeni özelliklerden bazıları şimdi bazı tablolar, dizinler ve oluşturulan rastgele veriler toopractice alın. Merhaba TSQL kod örnekleri, Azure SQL veritabanı altında veya SQL Server 2016, çalıştırılabilir. Ancak, bir Azure SQL veritabanı oluşturulurken bir P2 veritabanı, ihtiyacınız olduğu hello en az en az birkaç çekirdek tooallow çoklu iş parçacığı seçin ve bu nedenle bu özelliklerinden yararlanan emin olun.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

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


Şimdi, şimdi bir görünüm toosome 130 uyumluluk düzeyiyle gelen hello sorgu işleme özellikleri vardır.

## <a name="parallel-insert"></a>Paralel Ekle
Merhaba TSQL ifadeler çalıştırmasını hello sırasıyla çalıştırır tek iş parçacıklı model (120) ve çok iş parçacıklı model (130) hello ekleme işlemi, uyumluluk düzeyi 120 ve 130, altında ekleme işlemi yürütür.

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Merhaba gerçek hello sorgu planı, grafik gösterimi veya XML içeriğini arayan isteyerek yürütme sırasında işlevidir hangi kardinalite tahmin belirleyebilirsiniz. Şekil 1'üzerinde Hello planları yan yana bakarak açıkça o hello sütun deposu Ekle yürütme 120 tooparallel seri içinde 130 duruma geçtiğinde görebiliriz. Ayrıca, bu hello değişiklik hello yineleyici simgesinin iki paralel oklar, şimdi yineleyici yürütme hello hello olgu gösteren gerçekten paralel gösteren hello 130 planında unutmayın. Büyük ekleme işlemleri toocomplete varsa, hello Paralel yürütme, bağlantılı toohello, elden hello veritabanı için en sahip çekirdek sayısı daha iyi performans gösterir; 100 kat daha hızlı kendi koşullarınıza bağlı olarak tooa!

*Şekil 1: uyumluluk düzeyi 130 olan seri tooparallel işlemi değişiklikleri yerleştirin.*

![Şekil 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Seri toplu iş modu
Benzer şekilde, veri satırı işlerken toocompatibility düzeyi 130 taşıma toplu iş modu işleme sağlar. Sütun deposu dizini kullanıyor, ilk olarak, toplu iş modu işlemleri yalnızca kullanılabilir. İkinci olarak, bir toplu genellikle ~ 900 satırları temsil eder ve çok çekirdekli CPU, daha yüksek bellek verimliliği en iyi hale getirilmiş bir kod mantığını kullanır ve yararlanır hello mümkün olduğunca sütun deposu sıkıştırılmış verileri doğrudan hello. Bu koşullar altında SQL Server 2016 ~ 900 satır aynı anda 1 satır hello zamanında yerine işleyebilir ve sonuç olarak hello genel maliyeti hello işlemi şimdi hello genel satır maliyetini azaltma hello tüm toplu iş tarafından paylaşılır. Bu paylaşılan temelde hello sütun deposu sıkıştırması ile birlikte operations hello gecikme SELECT toplu iş modu işlemde yer alan azaltır. Merhaba sütun deposu hakkında daha fazla bilgi bulmak ve toplu iş modunda [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Görünür, hello sorgu planlarını yan yana Şekil 2 ' üzerindeki izlenerek hello işleme modunu hello uyumluluk düzeyiyle değişti ve sonuç olarak hello sorguları her iki uyumluluk düzeyi tamamen yürütürken, görebiliriz görebiliriz Çoğu hello işleme süresi, burada 2 toplu işlenen satır karşılaştırma modu (%86) toohello toplu iş modunda (%14) harcanır. Merhaba dataset artırın, hello avantajı artmasına neden olur.

*Şekil 2: uyumluluk düzeyi 130 seri toobatch moduyla işlemi değişiklikleri seçin.*

![Şekil 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Sıralama yürütme toplu iş modu
Satır (uyumluluk düzeyi 120) toobatch modu (uyumluluk düzeyi 130) benzer toohello yukarıdaki ancak uygulanan tooa sıralama işlemi hello geçiş hello hello için sıralama işlemi hello performansını artırır aynı nedenden dolayı.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Görünür yan yana Şekil 3'üzerinde satır modunda hello sıralama işlemi hello toplu iş modunda yalnızca hello maliyetinin (sırasıyla %81 ve hello sıralama kendisini %56) % 19 temsil ederken, maliyet hello %81 temsil ettiğini görebilirsiniz.

*Şekil 3: Uyumluluk düzeyi 130 olan satır toobatch modundan sıralama işlemi değiştirir.*

![Şekil 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Belli ki, bu örnekler yalnızca on binlerce satır, hiçbir şey çoğu SQL sunucuları kullanılabilir hello veri bugünlerde bakıldığında olduğu içerir. Yalnızca bu milyonlarca satır karşı yerine proje ve bu birkaç dakika bekleyen İş yükünüzün hello yapısını her gün kullanımdan yürütme çevirebilir.

## <a name="cardinality-estimation-ce-improvements"></a>Kardinalite tahmin (CE) geliştirmeleri
SQL Server 2014 ile sunulan, bir uyumluluk düzeyi 120 veya üstü çalıştıran herhangi bir veritabanı yapacak hello yeni kardinalite tahmin işlevselliğini kullanın. Esas olarak, kardinalite tahmin hello mantığı SQL server tahmini maliyetine bağlı bir sorgu nasıl yürütüleceği toodetermine kullanılır. Merhaba tahmin, sorguda kullanılan nesneleri ile ilişkili istatistikleri girişten kullanılarak hesaplanır. Pratikte, en üst düzey, kardinalite tahmin işlevleri tahminidir satır sayısı hello değerlerin ayrı değer sayıları hello dağıtımı hakkında bilgi ile birlikte ve yinelenen sayıları bulunan hello tablolar ve hello sorguda başvurulan nesneler. Bu tahminler yanlış alma tooinsufficient bellek verir (yani TempDB sıvı sıçraması) nedeniyle toounnecessary disk g/ç açabilir veya tooa seçimi paralel üzerinden bir seri planı yürütme birkaç yürütme, tooname planlayın. Sonuç, yanlış tahminleri tooan açabilir genel performans düşüşünü hello sorgu yürütme. Üzerindeki diğer tarafı, daha iyi tahminler, daha doğru tahminler, müşteri adayları toobetter sorgu yürütmeleri Merhaba!

Önceden belirtildiği gibi sorgu en iyi duruma getirme ve tahmin karmaşık sağlasa da, ancak toolearn sorgu planlarını ve kardinalite tahmin hakkında daha fazla bilgi istiyorsanız, toohello belge başvurabilir [hello SQL Server 2014 ile bilgisayarınızı sorgu planları en iyi duruma getirme Kardinalite tahmin](https://msdn.microsoft.com/library/dn673537.aspx) daha ayrıntılı bilgi edinmek için.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Hangi kardinalite tahmin, şu anda kullanıyor musunuz?
hangi kardinalite sorgularınızı çalıştıran tahmini altında yalnızca kullanım hello sorgu şimdi aşağıda örnekler toodetermine. Bu ilk örnek hello eski kardinalite tahmin işlevleri hello kullanımını olduğunu belirtmek uyumluluk düzeyi altında 110, çalışacağını unutmayın.

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


Yürütme tamamlandıktan sonra hello XML bağlantısına tıklayın ve aşağıda gösterildiği gibi hello ilk yineleyici hello özelliklerini bakın. Şu anda 70 üzerinde ayarlanmış CardinalityEstimationModelVersion adlı hello özellik adını not edin. Merhaba veritabanı uyumluluk düzeyi (bunu 110 deyimlerinde hello TSQL yukarıdaki görünür olarak ayarlanan) toohello SQL Server 7.0 sürümü ayarlanmış, ancak hello değeri 70 yalnızca hello eski kardinalite tahmin işlevselliği SQL itibaren kullanılabilir temsil eder gelmez (Bir uyumluluk düzeyinde 120 desteklemektedir) SQL Server 2014 kadar hiçbir önemli düzeltmeler vardı 7.0, sunucu.

*Şekil 4: uyumluluk düzeyi 110 veya aşağıda kullanırken too70 hello CardinalityEstimationModelVersion ayarlanır.*

![Şekil 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Alternatif olarak, hello uyumluluk düzeyi too130 değiştirebilir ve LEGACY_CARDINALITY_ESTIMATION ayarlama ile tooON hello kullanarak hello yeni kardinalite tahmin işlevi hello kullanımını devre dışı [ALTER veritabanı kapsamlı yapılandırma](https://msdn.microsoft.com/library/mt629158.aspx). Bu olması tam olarak hello hello son sorgu uyumluluk düzeyi işleme kullanırken 110 açısından bir kardinalite tahmin işlevi, aynı. Bunun yapılması, hello yeni sorgu işleme hello son uyumluluk düzeyinde (yani, toplu iş modu) gelen özelliklerini yararlı ancak hala gerekirse hello eski kardinalite tahmin işlevselliğini kullanır.

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


Yalnızca toohello uyumluluk düzeyi 120 veya 130 taşıma hello yeni kardinalite tahmin işlevsellik sağlar. Böyle bir durumda hello varsayılan CardinalityEstimationModelVersion uygun şekilde too120 veya 130 aşağıdaki görünür olarak ayarlanır.

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


*Şekil 5: Merhaba CardinalityEstimationModelVersion 130 uyumluluk düzeyini kullanırken too130 ayarlanır.*

![Şekil 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Witnessing hello kardinalite tahmin farklar
Şimdi, Şimdi Çalıştır biraz daha karmaşık bir INNER JOIN WHERE yan tümcesi ile bazı koşullar ile ilgili sorgu ve hello satır sayısı tahmini hello eski kardinalite tahmin işlevinden önce bakalım.

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


194,284 satırları Hello satır tahmini hello eski kardinalite tahmin işlevselliğe sahip iddia sırada etkili bir şekilde bu sorgu yürütülmeden 200.704 satırları döndürür. Belli ki, önce denirse gibi bu satır sayısı sonuçlarını da ne sıklıkta, hello önceki örnekleri, her çalıştırmayı tekrar tekrar adresindeki hello örnek tablolar doldurur çalıştırıldığı bağlıdır. Tabii ki sorgunuzu hello koşullarında hello gerçek tahmin hello tablo şekli, veri içeriği ve nasıl bu verilerin gerçekte bağıntısını birbiriyle yanı sıra üzerinde bir etkisi olacaktır.

*Şekil 6: hello satır sayısı tahmini 194,284 ya da 6,000 satır beklenen hello 200.704 satırlardan kapalıdır.*

![Şekil 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

Merhaba, aynı şekilde, şimdi şimdi hello hello yeni kardinalite tahmin işlevselliği ile aynı sorgu yürütün.

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


Başlangıç sırasında aşağıdaki baktığınızda, biz şimdi bu hello satır tahmini 202,877, ya da çok daha yakından ve eski kardinalite tahmin hello daha yüksek konusuna bakın.

*Şekil 7: hello satır sayısı tahmini 194,284 yerine 202,877 sunulmuştur.*

![Şekil 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

Gerçekte, hello sonuç 200.704 satır kümesidir (ancak tamamını bağlıdır ne sıklıkta hello hello sorgularını önceki örneklere karşılaştınız, ancak hello TSQL hello RAND() deyimi kullandığından daha da önemlisi, döndürülen hello gerçek değerler bir çalışma toohello sonraki farklı olabilir). Bu nedenle, bu örnekte hello yeni kardinalite tahmin 202,877 çok daha yakından too200, 704, 194,284 daha olduğundan satır hello sayısını tahmin etme sırasında daha iyi iş değil! WHERE yan tümcesi tooequality doğrulamaları hello değiştirirseniz, en son (yerine ">" örneği için), bu hello tahminleri hello eski ve yeni nicelik işlevi arasında daha farklı yapabilir, ne kadar eşleşme bağlı olarak, alabilirsiniz.

Belli ki, bu durumda, gerçek sayısını ~ 6000 satırları devre dışı bırakılıyor çok miktarda veri bazı durumlarda temsil etmiyor. Şimdi, bu toomillions satır birkaç tabloları ve daha karmaşık sorgular sırasını değiştir ve bazen hello tahmin kapalı milyonlarca satır tarafından olması ve bu nedenle, çekme yukarı hello yürütme planı veya yetersiz bellek isteme başında verir yanlış riskini hello tooTempDB sıvı sıçraması ve bu nedenle daha fazla g/ç, çok daha yüksek.

Merhaba fırsat varsa, bu karşılaştırma en tipik sorgular ve veri kümeleri ile uygulama ve kendiniz bazı yalnızca daha fazla devre dışı hello gerçekte veya bazı diğer yalnızca basit hale gelebilir sırada tarafından ne kadar hello eski ve yeni tahminleri bazıları, etkilenen görün yakın toohello gerçek satır gerçekte hello sonuç kümelerinde döndürülen sayar. Tüm bu sorgular, hello Azure SQL veritabanı özellikleri, hello yapısı ve veri kümelerini ve bunlarla ilgili kullanılabilir hello istatistikleri hello boyutu hello şeklinin bağlı olacaktır. Yeni oluşturduğunuz Azure SQL veritabanı örneğinde, hello sorgu iyileştiricisi toobuild olacaktır bildiğini en baştan yeniden kullanma istatistikleri hello önceki sorgunun yapılan yerine çalıştırır. Bu nedenle, çok bağlamsal ve neredeyse belirli tooevery sunucu ve uygulama durumu hello tahminlerdir. Önemli en boy tookeep aklınızda kadar!

## <a name="some-considerations-tootake-into-account"></a>Bazı konuları tootake göz önüne
Çoğu iş yükleri için üretim ortamınız için hello uyumluluk düzeyi'nu benimseme önce hello uyumluluk düzeyinin 130, yararlı olsa da, temel olarak 3 seçeneğiniz vardır:

1. Toocompatibility düzeyi 130 taşıyın ve nasıl şeyleri gerçekleştirmek bakın. Bazı gerileme fark durumunda, yalnızca yalnızca ayarlayın hello uyumluluk düzeyi geri tooits özgün düzeyi veya 130 tutmak ve yalnızca hello kardinalite tahmin geri toohello eski modu ters (yukarıda açıklandığı şekilde, bu tek başına hello soruna).
2. Mevcut uygulamalarınızı benzer üretim yük altında sınamanız ince ve devam eden tooproduction önce hello performansını doğrulama. Hataları durumunda aynı yukarıdaki her zaman toohello özgün uyumluluk düzeyi geri dönün veya için basitçe hello kardinalite tahmin geri toohello eski modu ters.
3. Bir son seçenek ve hello en son yolu tooaddress Bu sorular, tooleverage hello sorgu deposudur. Günümüzün önerilen seçenek olan! sorgularınızın uyumluluk altında tooassist hello analizini düzey 120 veya aşağıda 130 karşı yeterli toouse Query Store öneririz olamaz. Query Store hello en son sürümü Azure SQL Database V12 ile kullanılabilir ve tasarlanmıştır toohelp, sorgu performansı sorun giderme. Query Store Merhaba toplama ve tüm sorguları hakkında ayrıntılı geçmiş bilgileri sunan veritabanınız için uçuş veri Kaydedici olarak düşünün. Bu önemli ölçüde performans hukuk hello zaman toodiagnose azaltarak basitleştirir ve sorunları çözün. Daha fazla bilgi bulabilirsiniz [sorgu deposu: uçuş veri Kaydedici veritabanınız için](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

Merhaba zaten 120 uyumluluk düzeyinde veya altında çalışan bir veritabanları kümesi varsa ve toomove planlama üst düzey, adresindeki bazıları too130, veya İş yükünüzün otomatik olarak sağlamak için olacak yeni veritabanlarını hemen varsayılan too130 ayarlamak, lütfen göz önünde bulundurun Merhaba aşağıdakilere:

* Toohello yeni uyumluluk düzeyi üretimde değiştirmeden önce Query Store etkinleştirin. Çok başvurabilir[hello veritabanı uyumluluk modu ve kullanım hello sorgu deposu değişiklik](https://msdn.microsoft.com/library/bb895281.aspx) daha fazla bilgi için.
* Ardından, tüm kritik iş yükleri temsilcisi veri ve bir üretim benzeri bir ortam ve karşılaştırma hello performans karşılaştı ve sorgu deposu tarafından bildirilen olarak sorgularını kullanarak test edin. Bazı gerileme karşılaşırsanız, tanımlayabilirsiniz Query Store hello ile Merhaba gerileyen sorgular ve sorgu deposu seçeneği zorlama hello planını kullan (diğer adıyla sabitleme plan). Böyle bir durumda, tam olarak hello uyumluluk düzeyi 130 kalır ve hello eski sorgu planı hello Query Store tarafından önerilen olarak kullanın.
* Tooleverage yeni özellikler ve yetenekler (hangi SQL Server 2016 çalıştığı) Azure SQL veritabanı'nın istiyor, ancak son çare olarak hello uyumluluk düzeyi 130, tarafından duruma hassas toochanges olan geri hello uyumluluk düzeyi zorlama düşünebilirsiniz İş yükünüzün bir ALTER DATABASE deyimini kullanarak en çok uyan toohello düzeyi. Ancak önce bu hello Query Store planı seçeneği sabitleme 130 kullanmayan hello işlev düzeyinde eski bir SQL Server sürüm temelde kalıyor sizin için en iyi seçenek çünkü unutmayın.
* Birden çok veritabanı kapsayıcı çok müşterili uygulamalarınız varsa, tüm veritabanları arasında veritabanları tooensure tutarlı uyumluluk düzeyi mantığını sağlama gerekli tooupdate hello olabilir; eski ve yeni sağlanan olanlar. Uygulama iş yükü performansınızı bazı veritabanları farklı uyumluluk düzeylerinde çalıştıran hassas toohello olgu olabilir ve bu nedenle, üzerinde herhangi bir veritabanı uyumluluk düzeyinde tutarlılık gerekli olabilecek tooprovide hello aynı giriş sırası tooyour müşteriler tüm hello Panosu yaşar. Bir zorunluluğuna değil, gerçekten nasıl hello uyumluluk düzeyine göre uygulamanızın etkilenen bağlıdır dikkat edin.
* Son olarak, hello kardinalite tahmin ilgili olarak, üretim, devam etmeden önce hello uyumluluk düzeyinin değiştirilmesi gibi bu ise, uygulamanızın faydalanır Üretim İş yükünüzün hello yeni koşullar toodetermine altında tootest önerilen Merhaba kardinalite tahmin geliştirmeleri.

## <a name="conclusion"></a>Sonuç
Azure SQL veritabanı kullanarak toobenefit tüm SQL Server 2016 geliştirmeleri gelen sorgu yürütmeleri açıkça artırabilir. Gibi-değil! Elbette, herhangi bir yeni özelliği gibi doğru bir değerlendirme toodetermine hello tam koşullar altında veritabanının yükünüzü hello en iyi faaliyet yapılması gerekir. Deneyimi, çoğu iş yükü az saydam 130, uyumluluk düzeyi altında yeni sorgu işlevleri ve yeni kardinalite tahmin işleme yararlanarak sırasında çalıştırması beklenen tooat olduğunu gösterir. Olan gerçekçi olarak, her zaman bazı özel durumlar belirtti ve uygun son yapılması tespitlerini ne kadar avantajını bu iyileştirmeleriyle önemli değerlendirme toodetermine. Ve yeniden hello Query Store bu çalışarak harika Yardım olabilir!

SQL Azure geliştikçe hello bir uyumluluk düzeyi 140 gelecekteki bekleyebilirsiniz. Zaman uygun olduğunda, biz yalnızca biz kısaca burada uyumluluk seviyesi 130 bugün getiren anlatıldığı gibi ne bu ileriye dönük uyumluluk düzeyi 140 getirecek, Konuşmayı başlar.

Şimdilik, şimdi değil unutursanız, Haziran 2016'dan başlayarak, Azure SQL veritabanı hello varsayılan uyumluluk düzeyi yeni oluşturulan veritabanları için 120 too130 değiştirilecek. Dikkat!

## <a name="references"></a>Başvurular
* [Veritabanı Altyapısı'nda yenilikler nelerdir?](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blog: Sorgu deposu: Borko Novakovic, 8 Haziran 2016 tarafından veritabanınız için uçuş veri Kaydedicisi](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [ALTER veritabanı uyumluluk düzeyi (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER VERİTABANI KAPSAMLI YAPILANDIRMA](https://msdn.microsoft.com/library/mt629158.aspx)
* [Azure SQL Database V12 için uyumluluk düzeyi 130](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Bilgisayarınızı sorgu planları SQL Server 2014 kardinalite tahmin hello ile en iyi duruma getirme](https://msdn.microsoft.com/library/dn673537.aspx)
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
