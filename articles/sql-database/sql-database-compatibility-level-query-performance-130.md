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
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="71607-104">Azure SQL veritabanı uyumluluk düzeyi 130 ile sorgu performansı geliştirildi</span><span class="sxs-lookup"><span data-stu-id="71607-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="71607-105">Azure SQL veritabanı saydam yüz binlerce veritabanları birçok farklı uyumluluk düzeylerinde koruma ve kendi müşteriler için Microsoft SQL Server'ın hello geriye dönük uyumluluk toohello karşılık gelen sürüm güvence altına alır çalışıyor!</span><span class="sxs-lookup"><span data-stu-id="71607-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="71607-106">Bu makalede, Azure SQL veritabanı uyumluluk düzeyinde 130 çalıştıran ve hello yeni sorgu iyileştiricisi hello avantajlarından yararlanarak hello avantajlarını keşfedin ve işlemci özelliklerini sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71607-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="71607-107">Biz de hello olası yan etkileri hello sorgu performansı hello mevcut SQL uygulamalar için adres.</span><span class="sxs-lookup"><span data-stu-id="71607-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="71607-108">Geçmiş hatırlatma SQL sürümleri toodefault Uyumluluk Düzeyleri hello hizalamasını aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="71607-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="71607-109">100: SQL Server 2008 ve Azure SQL veritabanı V11.</span><span class="sxs-lookup"><span data-stu-id="71607-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="71607-110">110: SQL Server 2012 ve Azure SQL veritabanı V11.</span><span class="sxs-lookup"><span data-stu-id="71607-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="71607-111">120: SQL Server 2014 ve Azure SQL veritabanı V12.</span><span class="sxs-lookup"><span data-stu-id="71607-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="71607-112">130: SQL Server 2016 ve Azure SQL veritabanı V12.</span><span class="sxs-lookup"><span data-stu-id="71607-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71607-113">İtibariyle **mid-Haziran 2016**, Azure SQL veritabanı'nda hello varsayılan uyumluluk düzeyi için 120 yerine 130 olacaktır **yeni oluşturulan** veritabanları.</span><span class="sxs-lookup"><span data-stu-id="71607-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="71607-114">Mid-Haziran 2016 öncesinde oluşturulan veritabanlarını olacak *değil* etkilenecek ve bunların geçerli uyumluluk düzeyini (100, 110 veya 120) barındırır.</span><span class="sxs-lookup"><span data-stu-id="71607-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="71607-115">V11 tooV12 Azure SQL veritabanı sürümünden geçirilen veritabanları 100 veya 110 uyumluluk düzeyine sahip.</span><span class="sxs-lookup"><span data-stu-id="71607-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="71607-116">130 uyumluluk düzeyi hakkında</span><span class="sxs-lookup"><span data-stu-id="71607-116">About compatibility level 130</span></span>
<span data-ttu-id="71607-117">Tooknow hello geçerli uyumluluk düzeyini veritabanınızı istiyorsanız, ilk olarak, Transact-SQL deyimi aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="71607-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="71607-118">Bu değişiklikten önce için toolevel 130 gerçekleşir **yeni** veritabanları oluşturuldu, şimdi bu değişiklik hakkında bazı temel sorgu örneklerle nedir gözden geçirin ve herkesin buradan nasıl yararlanabilir bakın.</span><span class="sxs-lookup"><span data-stu-id="71607-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="71607-119">İlişkisel veritabanları sorgu işleme çok karmaşık olabilir ve bilgisayar Bilim ve matematik toounderstand hello devralınmış tasarım seçenekleri ve davranışları toolots yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="71607-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="71607-120">Bu belgede, bazı minimum teknik arka plan kimseyle hello uyumluluk düzeyi değişiklik hello etkisini anlamak ve böylelikle uygulamalar nasıl yararlanabilir belirlemek bilerek Basitleştirilmiş tooensure hello içerik kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="71607-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="71607-121">Şimdi ne hello uyumluluk düzeyi 130 hello tablosu getirir en hızlı bir görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="71607-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="71607-122">Daha fazla bilgi bulabilirsiniz [ALTER veritabanı uyumluluk düzeyi (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), burada ancak kısa bir özeti:</span><span class="sxs-lookup"><span data-stu-id="71607-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="71607-123">Hello INSERT select deyiminin ekleme işlemi çok iş parçacıklı olabilir veya bir paralel planınız bu işlem tek iş parçacıklı önce while.</span><span class="sxs-lookup"><span data-stu-id="71607-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="71607-124">İyileştirilmiş tablosu ve Tablo değişkenleri sorguları şimdi olabilir paralel planları, bellek çalışırken bu işlem ayrıca tek iş parçacıklı önce.</span><span class="sxs-lookup"><span data-stu-id="71607-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="71607-125">Bellek için iyileştirilmiş tablo İstatistikleri şimdi örneklenebilir ve otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="71607-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="71607-126">Bkz: [Veritabanı Altyapısı'ndaki Yenilikler: bellek içi OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="71607-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="71607-127">Toplu iş modu v/s satır modunu sütun deposu dizinleri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="71607-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="71607-128">Bir sütun deposu dizini olan bir tabloda sıralar toplu iş modunda sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="71607-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="71607-129">Pencereleme toplamalar şimdi TSQL ÖTELEME/sağlama deyimleri gibi toplu iş modunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="71607-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="71607-130">Birden çok distinct yan tümcelerinde sütun deposu tablolarla sorgulamaları toplu iş modunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="71607-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="71607-131">DOP altında çalışmakta olan sorgulara = 1 veya seri bir plan ile aynı zamanda toplu iş modunda yürütün.</span><span class="sxs-lookup"><span data-stu-id="71607-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="71607-132">Son olarak, kardinalite tahmin geliştirmeleri uyumluluk düzeyi 120 olan, ancak bu, düşük bir uyumluluk düzeyi çalıştıran (yani 100 veya 110) için gerçekten geliyor, hello taşıma toocompatibility düzeyi 130 de bu geliştirmeler getirecek ve bunlar da kullanabilirsiniz Merhaba sorgu uygulamalarınızın performansını yararlanır.</span><span class="sxs-lookup"><span data-stu-id="71607-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="71607-133">Alıştırmasını uyumluluk düzeyi 130</span><span class="sxs-lookup"><span data-stu-id="71607-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="71607-134">İlk bu yeni özelliklerden bazıları şimdi bazı tablolar, dizinler ve oluşturulan rastgele veriler toopractice alın.</span><span class="sxs-lookup"><span data-stu-id="71607-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="71607-135">Merhaba TSQL kod örnekleri, Azure SQL veritabanı altında veya SQL Server 2016, çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="71607-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="71607-136">Ancak, bir Azure SQL veritabanı oluşturulurken bir P2 veritabanı, ihtiyacınız olduğu hello en az en az birkaç çekirdek tooallow çoklu iş parçacığı seçin ve bu nedenle bu özelliklerinden yararlanan emin olun.</span><span class="sxs-lookup"><span data-stu-id="71607-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

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


<span data-ttu-id="71607-137">Şimdi, şimdi bir görünüm toosome 130 uyumluluk düzeyiyle gelen hello sorgu işleme özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="71607-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="71607-138">Paralel Ekle</span><span class="sxs-lookup"><span data-stu-id="71607-138">Parallel INSERT</span></span>
<span data-ttu-id="71607-139">Merhaba TSQL ifadeler çalıştırmasını hello sırasıyla çalıştırır tek iş parçacıklı model (120) ve çok iş parçacıklı model (130) hello ekleme işlemi, uyumluluk düzeyi 120 ve 130, altında ekleme işlemi yürütür.</span><span class="sxs-lookup"><span data-stu-id="71607-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

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


<span data-ttu-id="71607-140">Merhaba gerçek hello sorgu planı, grafik gösterimi veya XML içeriğini arayan isteyerek yürütme sırasında işlevidir hangi kardinalite tahmin belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71607-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="71607-141">Şekil 1'üzerinde Hello planları yan yana bakarak açıkça o hello sütun deposu Ekle yürütme 120 tooparallel seri içinde 130 duruma geçtiğinde görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="71607-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="71607-142">Ayrıca, bu hello değişiklik hello yineleyici simgesinin iki paralel oklar, şimdi yineleyici yürütme hello hello olgu gösteren gerçekten paralel gösteren hello 130 planında unutmayın.</span><span class="sxs-lookup"><span data-stu-id="71607-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="71607-143">Büyük ekleme işlemleri toocomplete varsa, hello Paralel yürütme, bağlantılı toohello, elden hello veritabanı için en sahip çekirdek sayısı daha iyi performans gösterir; 100 kat daha hızlı kendi koşullarınıza bağlı olarak tooa!</span><span class="sxs-lookup"><span data-stu-id="71607-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="71607-144">*Şekil 1: uyumluluk düzeyi 130 olan seri tooparallel işlemi değişiklikleri yerleştirin.*</span><span class="sxs-lookup"><span data-stu-id="71607-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![Şekil 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="71607-146">Seri toplu iş modu</span><span class="sxs-lookup"><span data-stu-id="71607-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="71607-147">Benzer şekilde, veri satırı işlerken toocompatibility düzeyi 130 taşıma toplu iş modu işleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="71607-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="71607-148">Sütun deposu dizini kullanıyor, ilk olarak, toplu iş modu işlemleri yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="71607-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="71607-149">İkinci olarak, bir toplu genellikle ~ 900 satırları temsil eder ve çok çekirdekli CPU, daha yüksek bellek verimliliği en iyi hale getirilmiş bir kod mantığını kullanır ve yararlanır hello mümkün olduğunca sütun deposu sıkıştırılmış verileri doğrudan hello.</span><span class="sxs-lookup"><span data-stu-id="71607-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="71607-150">Bu koşullar altında SQL Server 2016 ~ 900 satır aynı anda 1 satır hello zamanında yerine işleyebilir ve sonuç olarak hello genel maliyeti hello işlemi şimdi hello genel satır maliyetini azaltma hello tüm toplu iş tarafından paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="71607-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="71607-151">Bu paylaşılan temelde hello sütun deposu sıkıştırması ile birlikte operations hello gecikme SELECT toplu iş modu işlemde yer alan azaltır.</span><span class="sxs-lookup"><span data-stu-id="71607-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="71607-152">Merhaba sütun deposu hakkında daha fazla bilgi bulmak ve toplu iş modunda [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="71607-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

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


<span data-ttu-id="71607-153">Görünür, hello sorgu planlarını yan yana Şekil 2 ' üzerindeki izlenerek hello işleme modunu hello uyumluluk düzeyiyle değişti ve sonuç olarak hello sorguları her iki uyumluluk düzeyi tamamen yürütürken, görebiliriz görebiliriz Çoğu hello işleme süresi, burada 2 toplu işlenen satır karşılaştırma modu (%86) toohello toplu iş modunda (%14) harcanır.</span><span class="sxs-lookup"><span data-stu-id="71607-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="71607-154">Merhaba dataset artırın, hello avantajı artmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="71607-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="71607-155">*Şekil 2: uyumluluk düzeyi 130 seri toobatch moduyla işlemi değişiklikleri seçin.*</span><span class="sxs-lookup"><span data-stu-id="71607-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Şekil 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="71607-157">Sıralama yürütme toplu iş modu</span><span class="sxs-lookup"><span data-stu-id="71607-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="71607-158">Satır (uyumluluk düzeyi 120) toobatch modu (uyumluluk düzeyi 130) benzer toohello yukarıdaki ancak uygulanan tooa sıralama işlemi hello geçiş hello hello için sıralama işlemi hello performansını artırır aynı nedenden dolayı.</span><span class="sxs-lookup"><span data-stu-id="71607-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

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


<span data-ttu-id="71607-159">Görünür yan yana Şekil 3'üzerinde satır modunda hello sıralama işlemi hello toplu iş modunda yalnızca hello maliyetinin (sırasıyla %81 ve hello sıralama kendisini %56) % 19 temsil ederken, maliyet hello %81 temsil ettiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71607-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="71607-160">*Şekil 3: Uyumluluk düzeyi 130 olan satır toobatch modundan sıralama işlemi değiştirir.*</span><span class="sxs-lookup"><span data-stu-id="71607-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Şekil 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="71607-162">Belli ki, bu örnekler yalnızca on binlerce satır, hiçbir şey çoğu SQL sunucuları kullanılabilir hello veri bugünlerde bakıldığında olduğu içerir.</span><span class="sxs-lookup"><span data-stu-id="71607-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="71607-163">Yalnızca bu milyonlarca satır karşı yerine proje ve bu birkaç dakika bekleyen İş yükünüzün hello yapısını her gün kullanımdan yürütme çevirebilir.</span><span class="sxs-lookup"><span data-stu-id="71607-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="71607-164">Kardinalite tahmin (CE) geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="71607-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="71607-165">SQL Server 2014 ile sunulan, bir uyumluluk düzeyi 120 veya üstü çalıştıran herhangi bir veritabanı yapacak hello yeni kardinalite tahmin işlevselliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="71607-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="71607-166">Esas olarak, kardinalite tahmin hello mantığı SQL server tahmini maliyetine bağlı bir sorgu nasıl yürütüleceği toodetermine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="71607-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="71607-167">Merhaba tahmin, sorguda kullanılan nesneleri ile ilişkili istatistikleri girişten kullanılarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="71607-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="71607-168">Pratikte, en üst düzey, kardinalite tahmin işlevleri tahminidir satır sayısı hello değerlerin ayrı değer sayıları hello dağıtımı hakkında bilgi ile birlikte ve yinelenen sayıları bulunan hello tablolar ve hello sorguda başvurulan nesneler.</span><span class="sxs-lookup"><span data-stu-id="71607-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="71607-169">Bu tahminler yanlış alma tooinsufficient bellek verir (yani TempDB sıvı sıçraması) nedeniyle toounnecessary disk g/ç açabilir veya tooa seçimi paralel üzerinden bir seri planı yürütme birkaç yürütme, tooname planlayın.</span><span class="sxs-lookup"><span data-stu-id="71607-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="71607-170">Sonuç, yanlış tahminleri tooan açabilir genel performans düşüşünü hello sorgu yürütme.</span><span class="sxs-lookup"><span data-stu-id="71607-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="71607-171">Üzerindeki diğer tarafı, daha iyi tahminler, daha doğru tahminler, müşteri adayları toobetter sorgu yürütmeleri Merhaba!</span><span class="sxs-lookup"><span data-stu-id="71607-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="71607-172">Önceden belirtildiği gibi sorgu en iyi duruma getirme ve tahmin karmaşık sağlasa da, ancak toolearn sorgu planlarını ve kardinalite tahmin hakkında daha fazla bilgi istiyorsanız, toohello belge başvurabilir [hello SQL Server 2014 ile bilgisayarınızı sorgu planları en iyi duruma getirme Kardinalite tahmin](https://msdn.microsoft.com/library/dn673537.aspx) daha ayrıntılı bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="71607-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="71607-173">Hangi kardinalite tahmin, şu anda kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="71607-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="71607-174">hangi kardinalite sorgularınızı çalıştıran tahmini altında yalnızca kullanım hello sorgu şimdi aşağıda örnekler toodetermine.</span><span class="sxs-lookup"><span data-stu-id="71607-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="71607-175">Bu ilk örnek hello eski kardinalite tahmin işlevleri hello kullanımını olduğunu belirtmek uyumluluk düzeyi altında 110, çalışacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="71607-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="71607-176">Yürütme tamamlandıktan sonra hello XML bağlantısına tıklayın ve aşağıda gösterildiği gibi hello ilk yineleyici hello özelliklerini bakın.</span><span class="sxs-lookup"><span data-stu-id="71607-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="71607-177">Şu anda 70 üzerinde ayarlanmış CardinalityEstimationModelVersion adlı hello özellik adını not edin.</span><span class="sxs-lookup"><span data-stu-id="71607-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="71607-178">Merhaba veritabanı uyumluluk düzeyi (bunu 110 deyimlerinde hello TSQL yukarıdaki görünür olarak ayarlanan) toohello SQL Server 7.0 sürümü ayarlanmış, ancak hello değeri 70 yalnızca hello eski kardinalite tahmin işlevselliği SQL itibaren kullanılabilir temsil eder gelmez (Bir uyumluluk düzeyinde 120 desteklemektedir) SQL Server 2014 kadar hiçbir önemli düzeltmeler vardı 7.0, sunucu.</span><span class="sxs-lookup"><span data-stu-id="71607-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="71607-179">*Şekil 4: uyumluluk düzeyi 110 veya aşağıda kullanırken too70 hello CardinalityEstimationModelVersion ayarlanır.*</span><span class="sxs-lookup"><span data-stu-id="71607-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Şekil 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="71607-181">Alternatif olarak, hello uyumluluk düzeyi too130 değiştirebilir ve LEGACY_CARDINALITY_ESTIMATION ayarlama ile tooON hello kullanarak hello yeni kardinalite tahmin işlevi hello kullanımını devre dışı [ALTER veritabanı kapsamlı yapılandırma](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="71607-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="71607-182">Bu olması tam olarak hello hello son sorgu uyumluluk düzeyi işleme kullanırken 110 açısından bir kardinalite tahmin işlevi, aynı.</span><span class="sxs-lookup"><span data-stu-id="71607-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="71607-183">Bunun yapılması, hello yeni sorgu işleme hello son uyumluluk düzeyinde (yani, toplu iş modu) gelen özelliklerini yararlı ancak hala gerekirse hello eski kardinalite tahmin işlevselliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="71607-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="71607-184">Yalnızca toohello uyumluluk düzeyi 120 veya 130 taşıma hello yeni kardinalite tahmin işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="71607-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="71607-185">Böyle bir durumda hello varsayılan CardinalityEstimationModelVersion uygun şekilde too120 veya 130 aşağıdaki görünür olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="71607-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

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


<span data-ttu-id="71607-186">*Şekil 5: Merhaba CardinalityEstimationModelVersion 130 uyumluluk düzeyini kullanırken too130 ayarlanır.*</span><span class="sxs-lookup"><span data-stu-id="71607-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![Şekil 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="71607-188">Witnessing hello kardinalite tahmin farklar</span><span class="sxs-lookup"><span data-stu-id="71607-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="71607-189">Şimdi, Şimdi Çalıştır biraz daha karmaşık bir INNER JOIN WHERE yan tümcesi ile bazı koşullar ile ilgili sorgu ve hello satır sayısı tahmini hello eski kardinalite tahmin işlevinden önce bakalım.</span><span class="sxs-lookup"><span data-stu-id="71607-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="71607-190">194,284 satırları Hello satır tahmini hello eski kardinalite tahmin işlevselliğe sahip iddia sırada etkili bir şekilde bu sorgu yürütülmeden 200.704 satırları döndürür.</span><span class="sxs-lookup"><span data-stu-id="71607-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="71607-191">Belli ki, önce denirse gibi bu satır sayısı sonuçlarını da ne sıklıkta, hello önceki örnekleri, her çalıştırmayı tekrar tekrar adresindeki hello örnek tablolar doldurur çalıştırıldığı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="71607-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="71607-192">Tabii ki sorgunuzu hello koşullarında hello gerçek tahmin hello tablo şekli, veri içeriği ve nasıl bu verilerin gerçekte bağıntısını birbiriyle yanı sıra üzerinde bir etkisi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="71607-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="71607-193">*Şekil 6: hello satır sayısı tahmini 194,284 ya da 6,000 satır beklenen hello 200.704 satırlardan kapalıdır.*</span><span class="sxs-lookup"><span data-stu-id="71607-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![Şekil 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="71607-195">Merhaba, aynı şekilde, şimdi şimdi hello hello yeni kardinalite tahmin işlevselliği ile aynı sorgu yürütün.</span><span class="sxs-lookup"><span data-stu-id="71607-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="71607-196">Başlangıç sırasında aşağıdaki baktığınızda, biz şimdi bu hello satır tahmini 202,877, ya da çok daha yakından ve eski kardinalite tahmin hello daha yüksek konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="71607-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="71607-197">*Şekil 7: hello satır sayısı tahmini 194,284 yerine 202,877 sunulmuştur.*</span><span class="sxs-lookup"><span data-stu-id="71607-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![Şekil 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="71607-199">Gerçekte, hello sonuç 200.704 satır kümesidir (ancak tamamını bağlıdır ne sıklıkta hello hello sorgularını önceki örneklere karşılaştınız, ancak hello TSQL hello RAND() deyimi kullandığından daha da önemlisi, döndürülen hello gerçek değerler bir çalışma toohello sonraki farklı olabilir).</span><span class="sxs-lookup"><span data-stu-id="71607-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="71607-200">Bu nedenle, bu örnekte hello yeni kardinalite tahmin 202,877 çok daha yakından too200, 704, 194,284 daha olduğundan satır hello sayısını tahmin etme sırasında daha iyi iş değil!</span><span class="sxs-lookup"><span data-stu-id="71607-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="71607-201">WHERE yan tümcesi tooequality doğrulamaları hello değiştirirseniz, en son (yerine ">" örneği için), bu hello tahminleri hello eski ve yeni nicelik işlevi arasında daha farklı yapabilir, ne kadar eşleşme bağlı olarak, alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71607-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="71607-202">Belli ki, bu durumda, gerçek sayısını ~ 6000 satırları devre dışı bırakılıyor çok miktarda veri bazı durumlarda temsil etmiyor.</span><span class="sxs-lookup"><span data-stu-id="71607-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="71607-203">Şimdi, bu toomillions satır birkaç tabloları ve daha karmaşık sorgular sırasını değiştir ve bazen hello tahmin kapalı milyonlarca satır tarafından olması ve bu nedenle, çekme yukarı hello yürütme planı veya yetersiz bellek isteme başında verir yanlış riskini hello tooTempDB sıvı sıçraması ve bu nedenle daha fazla g/ç, çok daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="71607-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="71607-204">Merhaba fırsat varsa, bu karşılaştırma en tipik sorgular ve veri kümeleri ile uygulama ve kendiniz bazı yalnızca daha fazla devre dışı hello gerçekte veya bazı diğer yalnızca basit hale gelebilir sırada tarafından ne kadar hello eski ve yeni tahminleri bazıları, etkilenen görün yakın toohello gerçek satır gerçekte hello sonuç kümelerinde döndürülen sayar.</span><span class="sxs-lookup"><span data-stu-id="71607-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="71607-205">Tüm bu sorgular, hello Azure SQL veritabanı özellikleri, hello yapısı ve veri kümelerini ve bunlarla ilgili kullanılabilir hello istatistikleri hello boyutu hello şeklinin bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="71607-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="71607-206">Yeni oluşturduğunuz Azure SQL veritabanı örneğinde, hello sorgu iyileştiricisi toobuild olacaktır bildiğini en baştan yeniden kullanma istatistikleri hello önceki sorgunun yapılan yerine çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="71607-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="71607-207">Bu nedenle, çok bağlamsal ve neredeyse belirli tooevery sunucu ve uygulama durumu hello tahminlerdir.</span><span class="sxs-lookup"><span data-stu-id="71607-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="71607-208">Önemli en boy tookeep aklınızda kadar!</span><span class="sxs-lookup"><span data-stu-id="71607-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="71607-209">Bazı konuları tootake göz önüne</span><span class="sxs-lookup"><span data-stu-id="71607-209">Some considerations tootake into account</span></span>
<span data-ttu-id="71607-210">Çoğu iş yükleri için üretim ortamınız için hello uyumluluk düzeyi'nu benimseme önce hello uyumluluk düzeyinin 130, yararlı olsa da, temel olarak 3 seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="71607-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="71607-211">Toocompatibility düzeyi 130 taşıyın ve nasıl şeyleri gerçekleştirmek bakın.</span><span class="sxs-lookup"><span data-stu-id="71607-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="71607-212">Bazı gerileme fark durumunda, yalnızca yalnızca ayarlayın hello uyumluluk düzeyi geri tooits özgün düzeyi veya 130 tutmak ve yalnızca hello kardinalite tahmin geri toohello eski modu ters (yukarıda açıklandığı şekilde, bu tek başına hello soruna).</span><span class="sxs-lookup"><span data-stu-id="71607-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="71607-213">Mevcut uygulamalarınızı benzer üretim yük altında sınamanız ince ve devam eden tooproduction önce hello performansını doğrulama.</span><span class="sxs-lookup"><span data-stu-id="71607-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="71607-214">Hataları durumunda aynı yukarıdaki her zaman toohello özgün uyumluluk düzeyi geri dönün veya için basitçe hello kardinalite tahmin geri toohello eski modu ters.</span><span class="sxs-lookup"><span data-stu-id="71607-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="71607-215">Bir son seçenek ve hello en son yolu tooaddress Bu sorular, tooleverage hello sorgu deposudur.</span><span class="sxs-lookup"><span data-stu-id="71607-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="71607-216">Günümüzün önerilen seçenek olan!</span><span class="sxs-lookup"><span data-stu-id="71607-216">That’s today’s recommended option!</span></span> <span data-ttu-id="71607-217">sorgularınızın uyumluluk altında tooassist hello analizini düzey 120 veya aşağıda 130 karşı yeterli toouse Query Store öneririz olamaz.</span><span class="sxs-lookup"><span data-stu-id="71607-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="71607-218">Query Store hello en son sürümü Azure SQL Database V12 ile kullanılabilir ve tasarlanmıştır toohelp, sorgu performansı sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="71607-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="71607-219">Query Store Merhaba toplama ve tüm sorguları hakkında ayrıntılı geçmiş bilgileri sunan veritabanınız için uçuş veri Kaydedici olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="71607-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="71607-220">Bu önemli ölçüde performans hukuk hello zaman toodiagnose azaltarak basitleştirir ve sorunları çözün.</span><span class="sxs-lookup"><span data-stu-id="71607-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="71607-221">Daha fazla bilgi bulabilirsiniz [sorgu deposu: uçuş veri Kaydedici veritabanınız için](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="71607-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="71607-222">Merhaba zaten 120 uyumluluk düzeyinde veya altında çalışan bir veritabanları kümesi varsa ve toomove planlama üst düzey, adresindeki bazıları too130, veya İş yükünüzün otomatik olarak sağlamak için olacak yeni veritabanlarını hemen varsayılan too130 ayarlamak, lütfen göz önünde bulundurun Merhaba aşağıdakilere:</span><span class="sxs-lookup"><span data-stu-id="71607-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="71607-223">Toohello yeni uyumluluk düzeyi üretimde değiştirmeden önce Query Store etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="71607-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="71607-224">Çok başvurabilir[hello veritabanı uyumluluk modu ve kullanım hello sorgu deposu değişiklik](https://msdn.microsoft.com/library/bb895281.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="71607-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="71607-225">Ardından, tüm kritik iş yükleri temsilcisi veri ve bir üretim benzeri bir ortam ve karşılaştırma hello performans karşılaştı ve sorgu deposu tarafından bildirilen olarak sorgularını kullanarak test edin.</span><span class="sxs-lookup"><span data-stu-id="71607-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="71607-226">Bazı gerileme karşılaşırsanız, tanımlayabilirsiniz Query Store hello ile Merhaba gerileyen sorgular ve sorgu deposu seçeneği zorlama hello planını kullan (diğer adıyla sabitleme plan).</span><span class="sxs-lookup"><span data-stu-id="71607-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="71607-227">Böyle bir durumda, tam olarak hello uyumluluk düzeyi 130 kalır ve hello eski sorgu planı hello Query Store tarafından önerilen olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="71607-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="71607-228">Tooleverage yeni özellikler ve yetenekler (hangi SQL Server 2016 çalıştığı) Azure SQL veritabanı'nın istiyor, ancak son çare olarak hello uyumluluk düzeyi 130, tarafından duruma hassas toochanges olan geri hello uyumluluk düzeyi zorlama düşünebilirsiniz İş yükünüzün bir ALTER DATABASE deyimini kullanarak en çok uyan toohello düzeyi.</span><span class="sxs-lookup"><span data-stu-id="71607-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="71607-229">Ancak önce bu hello Query Store planı seçeneği sabitleme 130 kullanmayan hello işlev düzeyinde eski bir SQL Server sürüm temelde kalıyor sizin için en iyi seçenek çünkü unutmayın.</span><span class="sxs-lookup"><span data-stu-id="71607-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="71607-230">Birden çok veritabanı kapsayıcı çok müşterili uygulamalarınız varsa, tüm veritabanları arasında veritabanları tooensure tutarlı uyumluluk düzeyi mantığını sağlama gerekli tooupdate hello olabilir; eski ve yeni sağlanan olanlar.</span><span class="sxs-lookup"><span data-stu-id="71607-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="71607-231">Uygulama iş yükü performansınızı bazı veritabanları farklı uyumluluk düzeylerinde çalıştıran hassas toohello olgu olabilir ve bu nedenle, üzerinde herhangi bir veritabanı uyumluluk düzeyinde tutarlılık gerekli olabilecek tooprovide hello aynı giriş sırası tooyour müşteriler tüm hello Panosu yaşar.</span><span class="sxs-lookup"><span data-stu-id="71607-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="71607-232">Bir zorunluluğuna değil, gerçekten nasıl hello uyumluluk düzeyine göre uygulamanızın etkilenen bağlıdır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="71607-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="71607-233">Son olarak, hello kardinalite tahmin ilgili olarak, üretim, devam etmeden önce hello uyumluluk düzeyinin değiştirilmesi gibi bu ise, uygulamanızın faydalanır Üretim İş yükünüzün hello yeni koşullar toodetermine altında tootest önerilen Merhaba kardinalite tahmin geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="71607-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="71607-234">Sonuç</span><span class="sxs-lookup"><span data-stu-id="71607-234">Conclusion</span></span>
<span data-ttu-id="71607-235">Azure SQL veritabanı kullanarak toobenefit tüm SQL Server 2016 geliştirmeleri gelen sorgu yürütmeleri açıkça artırabilir.</span><span class="sxs-lookup"><span data-stu-id="71607-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="71607-236">Gibi-değil!</span><span class="sxs-lookup"><span data-stu-id="71607-236">Just as-is!</span></span> <span data-ttu-id="71607-237">Elbette, herhangi bir yeni özelliği gibi doğru bir değerlendirme toodetermine hello tam koşullar altında veritabanının yükünüzü hello en iyi faaliyet yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="71607-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="71607-238">Deneyimi, çoğu iş yükü az saydam 130, uyumluluk düzeyi altında yeni sorgu işlevleri ve yeni kardinalite tahmin işleme yararlanarak sırasında çalıştırması beklenen tooat olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="71607-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="71607-239">Olan gerçekçi olarak, her zaman bazı özel durumlar belirtti ve uygun son yapılması tespitlerini ne kadar avantajını bu iyileştirmeleriyle önemli değerlendirme toodetermine.</span><span class="sxs-lookup"><span data-stu-id="71607-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="71607-240">Ve yeniden hello Query Store bu çalışarak harika Yardım olabilir!</span><span class="sxs-lookup"><span data-stu-id="71607-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="71607-241">SQL Azure geliştikçe hello bir uyumluluk düzeyi 140 gelecekteki bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71607-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="71607-242">Zaman uygun olduğunda, biz yalnızca biz kısaca burada uyumluluk seviyesi 130 bugün getiren anlatıldığı gibi ne bu ileriye dönük uyumluluk düzeyi 140 getirecek, Konuşmayı başlar.</span><span class="sxs-lookup"><span data-stu-id="71607-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="71607-243">Şimdilik, şimdi değil unutursanız, Haziran 2016'dan başlayarak, Azure SQL veritabanı hello varsayılan uyumluluk düzeyi yeni oluşturulan veritabanları için 120 too130 değiştirilecek.</span><span class="sxs-lookup"><span data-stu-id="71607-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="71607-244">Dikkat!</span><span class="sxs-lookup"><span data-stu-id="71607-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="71607-245">Başvurular</span><span class="sxs-lookup"><span data-stu-id="71607-245">References</span></span>
* [<span data-ttu-id="71607-246">Veritabanı Altyapısı'nda yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="71607-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="71607-247">Blog: Sorgu deposu: Borko Novakovic, 8 Haziran 2016 tarafından veritabanınız için uçuş veri Kaydedicisi</span><span class="sxs-lookup"><span data-stu-id="71607-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="71607-248">ALTER veritabanı uyumluluk düzeyi (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="71607-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="71607-249">ALTER VERİTABANI KAPSAMLI YAPILANDIRMA</span><span class="sxs-lookup"><span data-stu-id="71607-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="71607-250">Azure SQL Database V12 için uyumluluk düzeyi 130</span><span class="sxs-lookup"><span data-stu-id="71607-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="71607-251">Bilgisayarınızı sorgu planları SQL Server 2014 kardinalite tahmin hello ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="71607-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="71607-252">Columnstore dizinleri Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="71607-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="71607-253">Blog: İyileştirilmiş sorgu performansı Alain Lissoir tarafından uyumluluk düzeyi 130 Azure SQL veritabanında olan 6 Mayıs 2016</span><span class="sxs-lookup"><span data-stu-id="71607-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
