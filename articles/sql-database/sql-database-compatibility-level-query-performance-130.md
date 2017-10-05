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
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="ecdb1-104">Azure SQL veritabanı uyumluluk düzeyi 130 ile sorgu performansı geliştirildi</span><span class="sxs-lookup"><span data-stu-id="ecdb1-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="ecdb1-105">Azure SQL veritabanı saydam yüz binlerce veritabanları birçok farklı uyumluluk düzeylerinde koruma ve onun tüm müşteriler için Microsoft SQL Server'ın ilgili sürümü için geriye dönük uyumluluk güvence altına alır çalışıyor!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing the backward compatibility to the corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="ecdb1-106">Bu makalede, Azure SQL veritabanı uyumluluk düzeyinde 130 çalıştıran ve avantajların yanı sıra yeni sorgu iyileştiricisi sorgu işlemci özelliklerini yararlanarak avantajlarını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-106">In this article, we explore the benefits of running your Azure SQL Databse at compatibility level 130, and leveraging the benefits of the new query optimizer and query processor features.</span></span> <span data-ttu-id="ecdb1-107">Biz de olası yan etkileri var olan SQL uygulamalar için sorgu performansına adres.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-107">We also address the possible side-effects on the query performance for the existing SQL applications.</span></span>

<span data-ttu-id="ecdb1-108">Geçmiş hatırlatma SQL sürümleri için varsayılan uyumluluk düzeyleri hizalamasını aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="ecdb1-108">As a reminder of history, the alignment of SQL versions to default compatibility levels are as follows:</span></span>

* <span data-ttu-id="ecdb1-109">100: SQL Server 2008 ve Azure SQL veritabanı V11.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="ecdb1-110">110: SQL Server 2012 ve Azure SQL veritabanı V11.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="ecdb1-111">120: SQL Server 2014 ve Azure SQL veritabanı V12.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="ecdb1-112">130: SQL Server 2016 ve Azure SQL veritabanı V12.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecdb1-113">İtibariyle **mid-Haziran 2016**, Azure SQL veritabanı'nda varsayılan uyumluluk düzeyi için 120 yerine 130 olacaktır **yeni oluşturulan** veritabanları.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-113">Starting in **mid-June 2016**, in Azure SQL Database, the default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="ecdb1-114">Mid-Haziran 2016 öncesinde oluşturulan veritabanlarını olacak *değil* etkilenecek ve bunların geçerli uyumluluk düzeyini (100, 110 veya 120) barındırır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="ecdb1-115">İçin V12 Azure SQL veritabanı V11 sürümünden geçirilen veritabanları 100 veya 110 uyumluluk düzeyine sahip.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-115">Databases that migrated from Azure SQL Database version V11 to V12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="ecdb1-116">130 uyumluluk düzeyi hakkında</span><span class="sxs-lookup"><span data-stu-id="ecdb1-116">About compatibility level 130</span></span>
<span data-ttu-id="ecdb1-117">Veritabanınızı geçerli uyumluluk düzeyini bilmek istiyorsanız, ilk olarak, aşağıdaki Transact-SQL deyimini yürütün.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-117">First, if you want to know the current compatibility level of your database, execute the following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="ecdb1-118">İçin düzeyine 130 bu değişiklik gerçekleşmeden önce **yeni** veritabanları oluşturuldu, şimdi bu değişiklik hakkında bazı temel sorgu örneklerle nedir gözden geçirin ve herkesin buradan nasıl yararlanabilir bakın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-118">Before this change to level 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="ecdb1-119">İlişkisel veritabanları sorgu işleme çok karmaşık olabilir ve için çok sayıda bilgisayar bilimi ve matematik devralınmış tasarım seçenekleri ve davranışlarını anlamak için yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-119">Query processing in relational databases can be very complex and can lead to lots of computer science and mathematics to understand the inherent design choices and behaviors.</span></span> <span data-ttu-id="ecdb1-120">Bu belgede, içerik bilerek minimum bazı teknik arka plan kimseyle uyumluluk düzeyi değişikliğin etkisini anlamak ve böylelikle uygulamalar nasıl yararlanabilir belirlemek emin olmak için basitleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-120">In this document, the content has been intentionally simplified to ensure that anyone with some minimum technical background can understand the impact of the compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="ecdb1-121">Şimdi ne uyumluluk düzeyi 130 tablosu getirir en hızlı bir görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-121">Let’s have a quick look at what the compatibility level 130 brings at the table.</span></span>  <span data-ttu-id="ecdb1-122">Daha fazla bilgi bulabilirsiniz [ALTER veritabanı uyumluluk düzeyi (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), burada ancak kısa bir özeti:</span><span class="sxs-lookup"><span data-stu-id="ecdb1-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="ecdb1-123">INSERT select deyiminin ekleme işlemi çok iş parçacıklı olabilir veya bir paralel planınız bu işlem tek iş parçacıklı önce while.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-123">The Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="ecdb1-124">İyileştirilmiş tablosu ve Tablo değişkenleri sorguları şimdi olabilir paralel planları, bellek çalışırken bu işlem ayrıca tek iş parçacıklı önce.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="ecdb1-125">Bellek için iyileştirilmiş tablo İstatistikleri şimdi örneklenebilir ve otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="ecdb1-126">Bkz: [Veritabanı Altyapısı'ndaki Yenilikler: bellek içi OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="ecdb1-127">Toplu iş modu v/s satır modunu sütun deposu dizinleri ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="ecdb1-128">Bir sütun deposu dizini olan bir tabloda sıralar toplu iş modunda sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="ecdb1-129">Pencereleme toplamalar şimdi TSQL ÖTELEME/sağlama deyimleri gibi toplu iş modunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="ecdb1-130">Birden çok distinct yan tümcelerinde sütun deposu tablolarla sorgulamaları toplu iş modunda çalışır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="ecdb1-131">DOP altında çalışmakta olan sorgulara = 1 veya seri bir plan ile aynı zamanda toplu iş modunda yürütün.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="ecdb1-132">Son olarak, kardinalite tahmin geliştirmeleri gerçekte 120, uyumluluk düzeyiyle geliyor ancak, düşük bir uyumluluk düzeyde (yani 100 veya 110), uyumluluk için taşıma çalıştıran içeriğiyle için düzeyi 130 Bu geliştirmeler ayrıca getirecek ve bu uygulamaların sorgu performansını da yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), the move to compatibility level 130 will also bring these improvements, and these can also benefit the query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="ecdb1-133">Alıştırmasını uyumluluk düzeyi 130</span><span class="sxs-lookup"><span data-stu-id="ecdb1-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="ecdb1-134">İlk şimdi bazı tablolar, dizinler ve bu yeni özelliklerden bazıları alıştırma yapmak için oluşturulmuş rastgele veri alın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-134">First let’s get some tables, indexes and random data created to practice some of these new capabilities.</span></span> <span data-ttu-id="ecdb1-135">TSQL kod örnekleri, Azure SQL veritabanı altında veya SQL Server 2016, çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-135">The TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="ecdb1-136">Ancak, bir Azure SQL veritabanı oluşturulurken en az birkaç çoklu iş parçacığı izin vermek ve bu nedenle bu özelliklerinden yararlanmak için çekirdek gerektiğinden P2 veritabanı en azından seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-136">However, when creating an Azure SQL database, make sure you choose at the minimum a P2 database because you need at least a couple of cores to allow multi-threading and therefore benefit from these features.</span></span>

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


<span data-ttu-id="ecdb1-137">Şimdi, şimdi bazı uyumluluk düzeyinde 130 gelen sorgu işleme özelliklerinin bir görünüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-137">Now, let’s have a look to some of the Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="ecdb1-138">Paralel Ekle</span><span class="sxs-lookup"><span data-stu-id="ecdb1-138">Parallel INSERT</span></span>
<span data-ttu-id="ecdb1-139">Aşağıdaki TSQL ifadeler çalıştırmasını sırasıyla çalıştırır tek iş parçacıklı model (120) ve çok iş parçacıklı model (130) ekleme işlemi, uyumluluk düzeyi 120 ve 130, altında ekleme işlemi yürütür.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-139">Executing the TSQL statements below executes the INSERT operation under compatibility level 120 and 130, which respectively executes the INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

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


<span data-ttu-id="ecdb1-140">Gerçek grafik gösterimi veya XML içeriğini arayan sorgu planı isteyerek yürütme sırasında işlevidir hangi kardinalite tahmin belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-140">By requesting the actual the query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="ecdb1-141">Şekil 1'üzerinde planları yan yana bakarak açıkça sütun deposu Ekle yürütme 120 seri paralel olarak 130 içinde duruma geçtiğinde, görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-141">Looking at the plans side-by-side on figure 1, we can clearly see that the Column Store INSERT execution goes from serial in 120 to parallel in 130.</span></span> <span data-ttu-id="ecdb1-142">Ayrıca, artık olgu gösteren iki paralel okları yineleyici yürütme gösteren 130 planında yineleyici simgesinin değişiklik gerçekten paralel olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-142">Also, note that the change of the iterator icon in the 130 plan showing two parallel arrows, illustrating the fact that now the iterator execution is indeed parallel.</span></span> <span data-ttu-id="ecdb1-143">Tamamlamak için büyük INSERT işlemlerine varsa, veritabanı için elden en sahip Çekirdek sayısına bağlı Paralel yürütme daha iyi performans gösterir; 100 kez daha hızlı kadar durumunuza bağlı olarak!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-143">If you have large INSERT operations to complete, the parallel execution, linked to the number of core you have at your disposal for the database, will perform better; up to a 100 times faster depending your situation!</span></span>

<span data-ttu-id="ecdb1-144">*Şekil 1: Ekleme işlemi seri paralel olarak değiştirir 130 ile uyumluluk düzeyi.*</span><span class="sxs-lookup"><span data-stu-id="ecdb1-144">*Figure 1: INSERT operation changes from serial to parallel with compatibility level 130.*</span></span>

![Şekil 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="ecdb1-146">Seri toplu iş modu</span><span class="sxs-lookup"><span data-stu-id="ecdb1-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="ecdb1-147">Benzer şekilde, veri satırı işlerken uyumluluk düzeyine 130 taşıma toplu iş modu işleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-147">Similarly, moving to compatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="ecdb1-148">Sütun deposu dizini kullanıyor, ilk olarak, toplu iş modu işlemleri yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="ecdb1-149">İkinci olarak, bir toplu genellikle ~ 900 satırları temsil eder ve çok çekirdekli CPU, daha yüksek bellek verimliliği en iyi hale getirilmiş bir kod mantığını kullanır ve mümkün olduğunca sütun deposu sıkıştırılmış verileri doğrudan yararlanır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages the compressed data of the Column Store whenever possible.</span></span> <span data-ttu-id="ecdb1-150">Bu koşullar altında SQL Server 2016 ~ 900 satır aynı anda 1 satır zaman yerine işleyebilir ve sonuç olarak, genel maliyeti işlemi şimdi satır maliyet genel azaltma tüm toplu işlem tarafından paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at the time, and as a consequence, the overall overhead cost of the operation is now shared by the entire batch, reducing the overall cost by row.</span></span> <span data-ttu-id="ecdb1-151">Sütun deposu sıkıştırmaya temelde birleştirilmiş işlemlerinin paylaşılan bu miktar seçin toplu iş modu işlemde yer alan gecikmesini azaltır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-151">This shared amount of operations combined with the column store compression basically reduces the latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="ecdb1-152">Sütun deposu hakkında daha fazla bilgi bulmak ve toplu iş modunda [Columnstore dizinleri Kılavuzu](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecdb1-152">You can find more details about the column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

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


<span data-ttu-id="ecdb1-153">Olarak aşağıda görünür, sorgu Şekil 2'üzerinde yan yana planları, parolanızı izlenerek işleme modunu uyumluluk düzeyiyle değişti ve sonuç olarak, sorguları her iki uyumluluk düzeyi tamamen yürütürken, işleme süresinin en görebiliriz görür toplu iş modunda (%14), burada 2 toplu işlenen karşılaştırıldığında row modunda (%86) harcanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-153">As visible below, by observing the query plans side-by-side on figure 2, we can see that the processing mode has changed with the compatibility level, and as a consequence, when executing the queries in both compatibility level altogether, we can see that most of the processing time is spent in row mode (86%) compared to the batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="ecdb1-154">Veri kümesi artırın, avantajı artmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-154">Increase the dataset, the benefit will increase.</span></span>

<span data-ttu-id="ecdb1-155">*Şekil 2: işlemi değişiklikleri seri toplu iş modunda 130 uyumluluk düzeyiyle seçin.*</span><span class="sxs-lookup"><span data-stu-id="ecdb1-155">*Figure 2: SELECT operation changes from serial to batch mode with compatibility level 130.*</span></span>

![Şekil 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="ecdb1-157">Sıralama yürütme toplu iş modu</span><span class="sxs-lookup"><span data-stu-id="ecdb1-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="ecdb1-158">Yukarıda, ancak sıralama işlemi uygulanan benzer toplu iş modunda (uyumluluk düzeyi 130) satır modu (uyumluluk düzeyi 120) geçiş aynı nedenden dolayı sıralama işlemi performansını artırır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-158">Similar to the above, but applied to a sort operation, the transition from row mode (compatibility level 120) to batch mode (compatibility level 130) improves the performance of the SORT operation for the same reasons.</span></span>

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


<span data-ttu-id="ecdb1-159">Toplu iş modunda yalnızca bir maliyetinin (sırasıyla %81 ve sıralama %56) % 19 temsil ederken, Satır modunda sıralama işlemi %81 maliyetinin temsil eden görünür yan yana Şekil 3'üzerinde görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-159">Visible side-by-side on figure 3, we can see that the sort operation in row mode represents 81% of the cost, while the batch mode only represents 19% of the cost (respectively 81% and 56% on the sort itself).</span></span>

<span data-ttu-id="ecdb1-160">*Şekil 3: Sıralama işlemi satırdan toplu iş modunda uyumluluk düzeyi 130 ile değiştirir.*</span><span class="sxs-lookup"><span data-stu-id="ecdb1-160">*Figure 3: SORT operation changes from row to batch mode with compatibility level 130.*</span></span>

![Şekil 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="ecdb1-162">Belli ki, bu örnekler yalnızca on binlerce satır, hiçbir şey çoğu SQL sunucuları kullanılabilir veri bugünlerde bakıldığında olduğu içerir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at the data available in most SQL Servers these days.</span></span> <span data-ttu-id="ecdb1-163">Yalnızca bu milyonlarca satır karşı yerine proje ve bu birkaç dakika bekleyen İş yükünüzün yapısını her gün kullanımdan yürütme çevirebilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending the nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="ecdb1-164">Kardinalite tahmin (CE) geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="ecdb1-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="ecdb1-165">SQL Server 2014 ile sunulan, bir uyumluluk düzeyi 120 veya üstü çalıştıran herhangi bir veritabanı yeni kardinalite tahmin kullanın yapar işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="ecdb1-166">Esas olarak, SQL server tahmini maliyetine bağlı bir sorgu nasıl yürütüleceği belirlemek için kullanılan mantığı kardinalite tahmin olur.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-166">Essentially, cardinality estimation is the logic used to determine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="ecdb1-167">Tahmin, sorguda kullanılan nesneleri ile ilişkili istatistikleri girişten kullanılarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-167">The estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="ecdb1-168">Pratikte, en üst düzey, kardinalite tahmin işlevleri tahminidir satır sayısı ayrı değer sayıları değerlerin dağıtımı hakkında bilgi ile birlikte ve yinelenen sayıları bulunan tabloları ve sorguda başvurulan nesneler.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about the distribution of the values, distinct value counts, and duplicate counts contained in the tables and objects referenced in the query.</span></span> <span data-ttu-id="ecdb1-169">Bu tahminler yanlış alınıyor, bellek yetersiz verir (yani TempDB sıvı sıçraması) nedeniyle gereksiz disk g/ç veya seri planı yürütme seçimi paralel plan yürütme birkaçıdır yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-169">Getting these estimates wrong, can lead to unnecessary disk I/O due to insufficient memory grants (i.e. TempDB spills), or to a selection of a serial plan execution over a parallel plan execution, to name a few.</span></span> <span data-ttu-id="ecdb1-170">Sonuç, yanlış tahminleri sorgu yürütme için bir genel performans düşüşüne neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-170">Conclusion, incorrect estimates can lead to an overall performance degradation of the query execution.</span></span> <span data-ttu-id="ecdb1-171">Diğer tarafta daha iyi tahminler, daha doğru tahminler daha iyi sorgu yürütmeleri müşteri adayları!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-171">On the other side, better estimates, more accurate estimates, leads to better query executions!</span></span>

<span data-ttu-id="ecdb1-172">Önceden belirtildiği gibi sorgu en iyi duruma getirme ve tahmin karmaşık sağlasa da, ancak sorgu planları ve kardinalite tahmin hakkında daha fazla bilgi edinmek istiyorsanız, belge başvurabilirsiniz [en iyi duruma getirme bilgisayarınızı sorgu planları ile SQL Server 2014 kardinalite tahmin](https://msdn.microsoft.com/library/dn673537.aspx) daha ayrıntılı bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want to learn more about query plans and cardinality estimator, you can refer to the document at [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="ecdb1-173">Hangi kardinalite tahmin, şu anda kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="ecdb1-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="ecdb1-174">Belirlemek için hangi kardinalite sorgularınızı çalıştığını tahmini altında yalnızca aşağıdaki sorgu örnekleri kullanalım.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-174">To determine under which Cardinality Estimation your queries are running, let’s just use the query samples below.</span></span> <span data-ttu-id="ecdb1-175">Bu ilk örnek eski kardinalite tahmin işlevleri kullanımını olduğunu belirtmek uyumluluk düzeyi altında 110, çalışacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-175">Note that this first example will run under compatibility level 110, implying the use of the old Cardinality Estimation functions.</span></span>

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


<span data-ttu-id="ecdb1-176">Yürütme tamamlandıktan sonra XML bağlantısına tıklayın ve aşağıda gösterildiği gibi ilk yineleyici özelliklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-176">Once execution is complete, click on the XML link, and look at the properties of the first iterator as shown below.</span></span> <span data-ttu-id="ecdb1-177">Şu anda 70 üzerinde ayarlanmış CardinalityEstimationModelVersion adlı özellik adını not edin.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-177">Note the property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="ecdb1-178">Veritabanı uyumluluk düzeyi (bunu 110 yukarıdaki TSQL deyimlerinde görünür olarak ayarlanan) SQL Server 7.0 sürümü için ayarlanmış, ancak 70 değeri yalnızca ana düzeltme yok (Uyumluluk düzeyinde 120 desteklemektedir) SQL Server 2014 kadar olan SQL Server 7.0 sürümünden itibaren kullanılabilir eski kardinalite tahmin işlevselliği temsil eder anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-178">It does not mean that the database compatibility level is set to the SQL Server 7.0 version (it is set on 110 as visible in the TSQL statements above), but the value 70 simply represents the legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="ecdb1-179">*Şekil 4: Uyumluluk düzeyi 110 veya aşağıda kullanırken CardinalityEstimationModelVersion 70 için ayarlanır.*</span><span class="sxs-lookup"><span data-stu-id="ecdb1-179">*Figure 4: The CardinalityEstimationModelVersion is set to 70 when using a compatibility level of 110 or below.*</span></span>

![Şekil 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="ecdb1-181">Alternatif olarak, uyumluluk düzeyi için 130 değiştirebilir ve on ile ayarlamak LEGACY_CARDINALITY_ESTIMATION kullanarak yeni kardinalite tahmin işlevi kullanımını devre dışı [ALTER veritabanı kapsamlı yapılandırma](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecdb1-181">Alternatively, you can change the compatibility level to 130, and disable the use of the new Cardinality Estimation function by using the LEGACY_CARDINALITY_ESTIMATION set to ON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="ecdb1-182">Bu tam olarak 110 açısından bir kardinalite tahmin işlevi, en son sorgu uyumluluk düzeyi işleme kullanırken aynı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-182">This will be exactly the same as using 110 from a Cardinality Estimation function point of view, while using the latest query processing compatibility level.</span></span> <span data-ttu-id="ecdb1-183">Bunun yapılması, yeni sorgu en son uyumluluk düzeyiyle (yani, toplu iş modu) gelen özellikleri işleme yararlı ancak hala gerekirse eski kardinalite tahmin işlevselliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-183">Doing so, you can benefit from the new query processing features coming with the latest compatibility level (i.e. batch mode), but still rely on the old Cardinality Estimation functionality if necessary.</span></span>

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


<span data-ttu-id="ecdb1-184">Yalnızca uyumluluk düzeyi 120 veya 130 taşıma yeni kardinalite tahmin işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-184">Simply moving to the compatibility level 120 or 130 enables the new Cardinality Estimation functionality.</span></span> <span data-ttu-id="ecdb1-185">Böyle bir durumda, varsayılan CardinalityEstimationModelVersion buna uygun olarak ayarlanacak 120 veya 130 altında görünür.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-185">In such a case, the default CardinalityEstimationModelVersion will be set accordingly to 120 or 130 as visible below.</span></span>

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


<span data-ttu-id="ecdb1-186">*Şekil 5: CardinalityEstimationModelVersion 130 uyumluluk düzeyini kullanırken 130 için ayarlanır.*</span><span class="sxs-lookup"><span data-stu-id="ecdb1-186">*Figure 5: The CardinalityEstimationModelVersion is set to 130 when using a compatibility level of 130.*</span></span>

![Şekil 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-the-cardinality-estimation-differences"></a><span data-ttu-id="ecdb1-188">Kardinalite tahmin farklar witnessing</span><span class="sxs-lookup"><span data-stu-id="ecdb1-188">Witnessing the Cardinality Estimation differences</span></span>
<span data-ttu-id="ecdb1-189">Şimdi, Şimdi Çalıştır biraz daha karmaşık bir INNER JOIN WHERE yan tümcesi ile bazı koşullar ile ilgili sorgu ve satır sayısı tahmini eski kardinalite tahmin işlevinden önce bakalım.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at the row count estimate from the old Cardinality Estimation function first.</span></span>

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


<span data-ttu-id="ecdb1-190">Eski kardinalite tahmin işlevsellikle satır tahmini 194,284 satırları talep ederken etkili bir şekilde bu sorgu yürütülmeden 200.704 satırları döndürür.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-190">Executing this query effectively returns 200,704 rows, while the row estimate with the old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="ecdb1-191">Belli ki, önce denirse gibi bu satır sayısı sonuçlarını da ne sıklıkta, önceki örnekleri, örnek tablolara her çalıştırmayı tekrar tekrar doldurur çalıştırıldığı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-191">Obviously, as said before, these row count results will also depend how often you ran the previous samples, which populates the sample tables over and over again at each run.</span></span> <span data-ttu-id="ecdb1-192">Tabii ki sorgunuzu koşullarında ayrıca veri içeriğini, tablo şekli yanı sıra gerçek tahmin üzerinde bir etkisi olacaktır ve nasıl bu verilerin gerçekte bağıntısını birbirleri ile.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-192">Obviously, the predicates in your query will also have an influence on the actual estimation aside from the table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="ecdb1-193">*Şekil 6: Satır sayısı tahmini 194,284 ya da 6,000 satır beklenen 200.704 satırların kapalıdır.*</span><span class="sxs-lookup"><span data-stu-id="ecdb1-193">*Figure 6: The row count estimate is 194,284 or 6,000 rows off from the 200,704 rows expected.*</span></span>

![Şekil 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="ecdb1-195">Aynı şekilde, şimdi artık aynı sorguyu yeni kardinalite tahmin işlevselliği ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-195">In the same way, let’s now execute the same query with the new Cardinality Estimation functionality.</span></span>

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


<span data-ttu-id="ecdb1-196">Bakarak Aşağıda, biz artık satır tahmini 202,877, veya çok daha yakından ve eski kardinalite tahmin daha yüksek olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-196">Looking at the below, we now see that the row estimate is 202,877, or much closer and higher than the old Cardinality Estimation.</span></span>

<span data-ttu-id="ecdb1-197">*Şekil 7: Satır sayısı tahmini 194,284 yerine 202,877 sunulmuştur.*</span><span class="sxs-lookup"><span data-stu-id="ecdb1-197">*Figure 7: The row count estimate is now 202,877, instead of 194,284.*</span></span>

![Şekil 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="ecdb1-199">Gerçekte, sonuç kümesi 200.704 satırları bağlıdır (ancak tamamını bağlıdır önceki örnek sorguları ne sıklıkta karşılaştınız, ancak TSQL RAND() deyimi kullandığından daha da önemlisi, döndürülen gerçek değerler bir çalışmadan diğerine sonraki farklı olabilir).</span><span class="sxs-lookup"><span data-stu-id="ecdb1-199">In reality, the result set is 200,704 rows (but all of it depends how often you did run the queries of the previous samples, but more importantly, because the TSQL uses the RAND() statement, the actual values returned can vary from one run to the next).</span></span> <span data-ttu-id="ecdb1-200">Bu nedenle, bu örnekte yeni kardinalite tahmin 202,877 194,284 200,704 için daha yakından olduğundan satır sayısını tahmin etme sırasında daha iyi iş değil!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-200">Therefore, in this particular example, the new Cardinality Estimation does a better job at estimating the number of rows because 202,877 is much closer to 200,704, than 194,284!</span></span> <span data-ttu-id="ecdb1-201">WHERE yan tümcesi eşitlik için doğrulamaları değiştirirseniz, en son (yerine ">" örneği için), bu eski arasında tahminleri yapabilir ve yeni nicelik işlevi kaç, eşleşen bağlı olarak daha da farklı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-201">Last, if you change the WHERE clause predicates to equality (rather than “>” for instance), this could make the estimates between the old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="ecdb1-202">Belli ki, bu durumda, gerçek sayısını ~ 6000 satırları devre dışı bırakılıyor çok miktarda veri bazı durumlarda temsil etmiyor.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="ecdb1-203">Şimdi, milyonlarca satır ve bu nedenle, çekme yukarı yanlış yürütme planı veya yetersiz bellek verir TempDB sıvı sıçraması ve bu nedenle daha fazla g/ç, yol isteyen riskini bu birden çok tablo ve daha karmaşık sorgular ve bazen tahmin satırlarda milyonlarca kapalı olabilir devrik çok daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-203">Now, transpose this to millions of rows across several tables and more complex queries, and at times the estimate can be off by millions of rows , and therefore, the risk of picking-up the wrong execution plan, or requesting insufficient memory grants leading to TempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="ecdb1-204">Alıştırma fırsat varsa en tipik sorgular ve veri kümeleri, bu karşılaştırma ve ne kadar eski ve yeni tahminleri bazıları etkilendiğini, bazı yalnızca daha fazla devre dışı gerçekte veya bazı başkalarına yalnızca yalnızca daha yakın gerçek satır hale gelebilir sırada sonuç kümelerinde gerçekte döndürülen sayıları kendiniz için bkz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-204">If you have the opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of the old and new estimates are affected, while some could just become more off from the reality, or some others just simply closer to the actual row counts actually returned in the result sets.</span></span> <span data-ttu-id="ecdb1-205">Tamamını sorgularınızı, Azure SQL veritabanı özellikleri, yapısı ve boyutunu, veri kümeleri ve bunlarla ilgili kullanılabilir istatistikleri şeklin bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-205">All of it will depend of the shape of your queries, the Azure SQL database characteristics, the nature and the size of your datasets, and the statistics available about them.</span></span> <span data-ttu-id="ecdb1-206">Azure SQL veritabanı örneğinde oluşturduysanız, sorgu iyileştiricisi bildiğini önceki sorgu çalışmalarını yapılan istatistikleri yeniden kullanmak yerine sıfırdan yapı gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-206">If you just created your Azure SQL Database instance, the query optimizer will have to build its knowledge from scratch instead of reusing statistics made of the previous query runs.</span></span> <span data-ttu-id="ecdb1-207">Bu nedenle, çok bağlamsal ve neredeyse her sunucu ve uygulama durumunuza özel tahmin eder.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-207">So, the estimates are very contextual and almost specific to every server and application situation.</span></span> <span data-ttu-id="ecdb1-208">Dikkate alınması gereken önemli bir durum değil!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-208">It is an important aspect to keep in mind!</span></span>

## <a name="some-considerations-to-take-into-account"></a><span data-ttu-id="ecdb1-209">Dikkate almanız gereken bazı noktalar</span><span class="sxs-lookup"><span data-stu-id="ecdb1-209">Some considerations to take into account</span></span>
<span data-ttu-id="ecdb1-210">Çoğu iş yükleri için üretim ortamınız için uyumluluk düzeyi'nu benimseme önce uyumluluk düzeyinin 130, yararlı olsa da, temel olarak 3 seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="ecdb1-210">Although most workloads would benefit from the compatibility level 130, before you adopting the compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="ecdb1-211">Uyumluluk düzeyi 130 taşıyın ve nasıl şeyleri gerçekleştirmek bakın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-211">You move to compatibility level 130, and see how things perform.</span></span> <span data-ttu-id="ecdb1-212">Bazı gerileme dikkat edin, yalnızca yalnızca özgün düzeyine uyumluluk düzeyi ayarlayın veya 130 Koru ve yalnızca geriye doğru kardinalite tahmin geri eski modu durumunda (yukarıda açıklandığı şekilde, bu tek başına soruna).</span><span class="sxs-lookup"><span data-stu-id="ecdb1-212">In case you notice some regressions, you just simply set the compatibility level back to its original level, or keep 130, and only reverse the Cardinality Estimation back to the legacy mode (As explained above, this alone could address the issue).</span></span>
2. <span data-ttu-id="ecdb1-213">Mevcut uygulamalarınızı benzer üretim yük altında sınamanız ince ve üretime geçmeden önce performansını doğrulama.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-213">You thoroughly test your existing applications under similar production load, fine tune, and validate the performance before going to production.</span></span> <span data-ttu-id="ecdb1-214">Hataları durumunda aynı yukarıdaki her zaman özgün uyumluluk düzeyine geri dönün veya için yalnızca eski moda kardinalite tahmin ters çevir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-214">In case of issues, same as above, you can always go back to the original compatibility level, or simply reverse the Cardinality Estimation back to the legacy mode.</span></span>
3. <span data-ttu-id="ecdb1-215">Son seçenek, bu soruları için en son yol, Query Store yararlanmak için ise.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-215">As a final option, and the most recent way to address these questions, is to leverage the Query Store.</span></span> <span data-ttu-id="ecdb1-216">Günümüzün önerilen seçenek olan!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-216">That’s today’s recommended option!</span></span> <span data-ttu-id="ecdb1-217">Sorgularınızı uyumluluk altında analizini yardımcı olmak için 120 düzeyinde veya altında 130 karşı yeterince sorgu deposu kullanmak için öneririz olamaz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-217">To assist the analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough to use Query Store.</span></span> <span data-ttu-id="ecdb1-218">Query Store Azure SQL Database V12 en son sürümü ile kullanılabilir ve sorgu performansı sorun giderme konusunda yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-218">Query Store is available with the latest version of Azure SQL Database V12, and it’s designed to help you with query performance troubleshooting.</span></span> <span data-ttu-id="ecdb1-219">Sorgu deposu veritabanınızın toplama ve tüm sorguları hakkında ayrıntılı geçmiş bilgileri sunan bir uçuş veri Kaydedici olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-219">Think of the Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="ecdb1-220">Bu önemli ölçüde performans hukuk tanılamak ve sorunları gidermek için zamanı azaltarak basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-220">This greatly simplifies performance forensics by reducing the time to diagnose and resolve issues.</span></span> <span data-ttu-id="ecdb1-221">Daha fazla bilgi bulabilirsiniz [sorgu deposu: uçuş veri Kaydedici veritabanınız için](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="ecdb1-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="ecdb1-222">En üst düzey, zaten 120 uyumluluk düzeyinde veya altında çalışan veritabanları kümesine sahiptir ve bunların bazıları için 130 taşımak veya İş yükünüzün otomatik olarak sağlamak için olacak yeni veritabanlarını hemen 130, varsayılan olarak ayarlanması düşünüyorsanız lütfen göz önünde bulundurun aşağıdakilere:</span><span class="sxs-lookup"><span data-stu-id="ecdb1-222">At the high-level, if you already have a set of databases running at compatibility level 120 or below, and plan to move some of them to 130, or because your workload automatically provision new databases that will be soon be set by default to 130, please consider the followings:</span></span>

* <span data-ttu-id="ecdb1-223">Yeni uyumluluk düzeyini üretimde değiştirmeden önce Query Store etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-223">Before changing to the new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="ecdb1-224">Başvurabilirsiniz [veritabanı Uyumluluk modunu değiştirme ve sorgu deposu kullanmanız](https://msdn.microsoft.com/library/bb895281.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-224">You can refer to [Change the Database Compatibility Mode and Use the Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="ecdb1-225">Ardından, tüm kritik iş yükleri temsilcisi veri ve bir üretim benzeri bir ortam ve karşılaştırma yaşadı performans ve sorgu deposu tarafından bildirilen olarak sorgularını kullanarak test edin.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare the performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="ecdb1-226">Bazı gerileme karşılaşırsanız, Query Store gerileyen sorgularıyla tanımlamak ve sorgu deposu seçeneği zorlama planını kullan (diğer adıyla sabitleme plan).</span><span class="sxs-lookup"><span data-stu-id="ecdb1-226">If you experience some regressions, you can identify the regressed queries with the Query Store and use the plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="ecdb1-227">Böyle bir durumda, tam olarak uyumluluk düzeyiyle 130 kalır ve eski sorgu planı Query Store tarafından önerilen olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-227">In such a case, you definitively stay with the compatibility level 130, and use the former query plan as suggested by the Query Store.</span></span>
* <span data-ttu-id="ecdb1-228">Yeni özellik ve yetenekler (hangi SQL Server 2016 çalıştığı) Azure SQL veritabanı'nın yararlanmak isteyen, ancak son çare olarak 130, uyumluluk düzeyine göre duruma değişikliklere duyarlıdır uyumluluk düzeyini tekrar İş yükünüzün bir ALTER DATABASE deyimini kullanarak en çok uyan düzeyine zorlama düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-228">If you want to leverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive to changes brought by the compatibility level 130, as a last resort, you could consider forcing the compatibility level back to the level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="ecdb1-229">Ancak, ilk olarak, 130 kullanmayan daha eski bir SQL Server sürümü işlev düzeyinde temelde kalıyor çünkü seçeneği sabitleme Query Store planı sizin için en iyi seçenek olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-229">But first, be aware that the Query Store plan pinning option is your best option because not using 130 is basically staying at the functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="ecdb1-230">Birden çok veritabanı kapsayıcı çok müşterili uygulamalarınız varsa, veritabanlarınızın tüm veritabanları arasında tutarlı uyumluluk düzeyini sağlamak için sağlama mantığı güncelleştirmek gerekli olabilir; eski ve yeni sağlanan olanlar.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-230">If you have multitenant applications spanning multiple databases, it may be necessary to update the provisioning logic of your databases to ensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="ecdb1-231">Uygulama iş yükü performansınızı bazı veritabanları farklı uyumluluk düzeylerinde çalıştıran olgu hassas olabilir ve bu nedenle, üzerinde herhangi bir veritabanı uyumluluk düzeyinde tutarlılık tüm Panosu müşterilerinize aynı deneyimi sağlamak için gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-231">Your application workload performance could be sensitive to the fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order to provide the same experience to your customers all across the board.</span></span> <span data-ttu-id="ecdb1-232">Bir zorunluluğuna değil, gerçekten nasıl uyumluluk düzeyine göre uygulamanızın etkilenen bağlıdır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-232">Note that it is not a mandate, it really depends on how your application is affected by the compatibility level.</span></span>
* <span data-ttu-id="ecdb1-233">Son olarak, kardinalite tahmin ilgili ve üretim, devam etmeden önce uyumluluk düzeyini değiştirme gibi üretim İş yükünüzün uygulamanızı kardinalite tahmin geliştirmelerden faydalanabilmeniz avantaj ise belirlemek için yeni koşullar altında test etmek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-233">Last, regarding the Cardinality Estimation, and just like changing the compatibility level, before proceeding in production, it is recommended to test your production workload under the new conditions to determine if your application benefits from the Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ecdb1-234">Sonuç</span><span class="sxs-lookup"><span data-stu-id="ecdb1-234">Conclusion</span></span>
<span data-ttu-id="ecdb1-235">Tüm SQL Server 2016 iyileştirmeleriyle yararlanmak için Azure SQL veritabanı kullanarak, sorgu yürütmeleri açıkça artırabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-235">Using Azure SQL Database to benefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="ecdb1-236">Gibi-değil!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-236">Just as-is!</span></span> <span data-ttu-id="ecdb1-237">Elbette, herhangi bir yeni özelliği gibi doğru bir değerlendirme altında veritabanının yükünüzü en iyi faaliyet tam koşullarını belirlemek için yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-237">Of course, like any new feature, a proper evaluation must be done to determine the exact conditions under which your database workload operates the best.</span></span> <span data-ttu-id="ecdb1-238">Çoğu iş yükü beklenen saydam 130, uyumluluk düzeyi altında yeni sorgu işlevleri ve yeni kardinalite tahmin işleme yararlanarak sırasında çalışması için en az deneyimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-238">Experience shows that most workload are expected to at least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="ecdb1-239">Olan gerçekçi olarak, her zaman bazı özel durumlar belirtti ve uygun son yapılması tespitlerini bu iyileştirmeleriyle ne kadar fayda belirlemek için önemli bir değerlendirme.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment to determine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="ecdb1-240">Ve yeniden, Query Store bu çalışarak harika Yardım olabilir!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-240">And again, the Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="ecdb1-241">SQL Azure geliştikçe uyumluluk düzeyi 140 gelecekte bekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-241">As SQL Azure evolves, you can expect a compatibility level 140 in the future.</span></span> <span data-ttu-id="ecdb1-242">Zaman uygun olduğunda, biz yalnızca biz kısaca burada uyumluluk seviyesi 130 bugün getiren anlatıldığı gibi ne bu ileriye dönük uyumluluk düzeyi 140 getirecek, Konuşmayı başlar.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="ecdb1-243">Şimdilik, şimdi değil unutursanız, Haziran 2016'dan başlayarak, Azure SQL veritabanı varsayılan uyumluluk düzeyi 120-yeni oluşturulan veritabanları için 130 değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ecdb1-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change the default compatibility level from 120 to 130 for newly created databases.</span></span> <span data-ttu-id="ecdb1-244">Dikkat!</span><span class="sxs-lookup"><span data-stu-id="ecdb1-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="ecdb1-245">Başvurular</span><span class="sxs-lookup"><span data-stu-id="ecdb1-245">References</span></span>
* [<span data-ttu-id="ecdb1-246">Veritabanı Altyapısı'nda yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="ecdb1-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="ecdb1-247">Blog: Sorgu deposu: Borko Novakovic, 8 Haziran 2016 tarafından veritabanınız için uçuş veri Kaydedicisi</span><span class="sxs-lookup"><span data-stu-id="ecdb1-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="ecdb1-248">ALTER veritabanı uyumluluk düzeyi (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="ecdb1-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="ecdb1-249">ALTER VERİTABANI KAPSAMLI YAPILANDIRMA</span><span class="sxs-lookup"><span data-stu-id="ecdb1-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="ecdb1-250">Azure SQL Database V12 için uyumluluk düzeyi 130</span><span class="sxs-lookup"><span data-stu-id="ecdb1-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="ecdb1-251">Sorgunuz en iyi duruma getirme ile SQL Server 2014 kardinalite tahmin planları</span><span class="sxs-lookup"><span data-stu-id="ecdb1-251">Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="ecdb1-252">Columnstore dizinleri Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="ecdb1-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="ecdb1-253">Blog: İyileştirilmiş sorgu performansı Alain Lissoir tarafından uyumluluk düzeyi 130 Azure SQL veritabanında olan 6 Mayıs 2016</span><span class="sxs-lookup"><span data-stu-id="ecdb1-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

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
