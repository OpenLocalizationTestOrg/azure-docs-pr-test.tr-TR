---
title: "Tasarım çoğaltılmış tablolar - Azure SQL Data Warehouse için Kılavuzu | Microsoft Docs"
description: "Çoğaltılmış tablolar, Azure SQL Data Warehouse şemasında tasarlama için öneriler."
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 07/14/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 437a4f628a343312984d1fa2981df7fa01459e26
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="2576c-103">Azure SQL Data Warehouse'da çoğaltılmış tablolar kullanmaya yönelik kılavuz tasarım</span><span class="sxs-lookup"><span data-stu-id="2576c-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="2576c-104">Bu makalede SQL Data Warehouse şemanızı çoğaltılmış tablolarda tasarlamak için öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="2576c-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="2576c-105">Veri taşıma ve sorgu karmaşıklık azaltarak sorgu performansını artırmak için bu önerileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="2576c-105">Use these recommendations to improve query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="2576c-106">Çoğaltılmış tablo özelliği şu anda genel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="2576c-106">The replicated table feature is currently in public preview.</span></span> <span data-ttu-id="2576c-107">Bazı davranışları farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-107">Some behaviors are subject to change.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="2576c-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2576c-108">Prerequisites</span></span>
<span data-ttu-id="2576c-109">Bu makalede, veri dağıtımı ve SQL Data Warehouse veri taşıma kavramlarına alışık olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="2576c-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="2576c-110">Daha fazla bilgi için bkz: [Dağıtılmış veri](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="2576c-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="2576c-111">Tablo Tasarımı bir parçası olarak, verilerinizi ve verilerin nasıl sorgulanır hakkında mümkün olduğunca anlayın.</span><span class="sxs-lookup"><span data-stu-id="2576c-111">As part of table design, understand as much as possible about your data and how the data is queried.</span></span>  <span data-ttu-id="2576c-112">Örneğin, aşağıdaki soruları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="2576c-112">For example, consider these questions:</span></span>

- <span data-ttu-id="2576c-113">Tablo büyüklüğü nedir?</span><span class="sxs-lookup"><span data-stu-id="2576c-113">How large is the table?</span></span>   
- <span data-ttu-id="2576c-114">Tablo ne sıklıkla yenileniyor?</span><span class="sxs-lookup"><span data-stu-id="2576c-114">How often is the table refreshed?</span></span>   
- <span data-ttu-id="2576c-115">Bir veri ambarı olgu ve boyut tabloları var mı?</span><span class="sxs-lookup"><span data-stu-id="2576c-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="2576c-116">Çoğaltılmış tablosu nedir?</span><span class="sxs-lookup"><span data-stu-id="2576c-116">What is a replicated table?</span></span>
<span data-ttu-id="2576c-117">Yinelenen tablo her işlem düğümü üzerinde erişilebilir tablo tam bir kopyasını sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2576c-117">A replicated table has a full copy of the table accessible on each Compute node.</span></span> <span data-ttu-id="2576c-118">Tablo çoğaltma JOIN veya toplama önce işlem düğümleri arasında veri aktarmak için gereksinimini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="2576c-118">Replicating a table removes the need to transfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="2576c-119">Tablosunda birden çok kopya bulunduğundan tablo boyutunu sıkıştırılmış 2 GB'tan daha az olduğunda çoğaltılmış tablolarda en iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="2576c-119">Since the table has multiple copies, replicated tables work best when the table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="2576c-120">Aşağıdaki diyagram, her işlem düğümü üzerinde erişilebilir olan bir çoğaltılmış tablo gösterir.</span><span class="sxs-lookup"><span data-stu-id="2576c-120">The following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="2576c-121">SQL veri ambarı'nda çoğaltılmış tablo her işlem düğümü üzerinde bir dağıtım veritabanı tam olarak kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="2576c-121">In SQL Data Warehouse, the replicated table is fully copied to a distribution database on each Compute node.</span></span> 

<span data-ttu-id="2576c-122">![Yinelenmiş tablo](media/guidance-for-using-replicated-tables/replicated-table.png "yinelenmiş tablosu")</span><span class="sxs-lookup"><span data-stu-id="2576c-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="2576c-123">İyi bir yıldız şemasının küçük boyut tabloları için tabloları iş çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="2576c-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="2576c-124">Boyut tabloları genellikle depolamak ve birden çok kopyasını korumak için uygun yapan bir boyutu var.</span><span class="sxs-lookup"><span data-stu-id="2576c-124">Dimension tables are usually of a size that makes it feasible to store and maintain multiple copies.</span></span> <span data-ttu-id="2576c-125">Boyutların müşteri adı ve adres ve ürün ayrıntıları gibi yavaş değişir açıklayıcı verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="2576c-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="2576c-126">Verileri yavaş değişen yapısı daha az çoğaltılmış tablo yeniden için yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="2576c-126">The slowly changing nature of the data leads to fewer rebuilds of the replicated table.</span></span> 

<span data-ttu-id="2576c-127">Çoğaltılan kullanmayı tablosundan:</span><span class="sxs-lookup"><span data-stu-id="2576c-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="2576c-128">2 GB'den az, satır sayısından bağımsız olarak disk üzerindeki tablo boyutudur.</span><span class="sxs-lookup"><span data-stu-id="2576c-128">The table size on disk is less than 2 GB, regardless of the number of rows.</span></span> <span data-ttu-id="2576c-129">Bir tablonun boyutunu bulmak için kullanabileceğiniz [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) komutu: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="2576c-129">To find the size of a table, you can use the [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="2576c-130">Tablo, aksi halde veri taşıma gerektirecek birleştirme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2576c-130">The table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="2576c-131">Örneğin, birleşme sütunları aynı dağıtım sütun olmadığında bir birleştirme karma dağıtılmış tablolarda veri taşıma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2576c-131">For example, a join on hash-distributed tables requires data movement when the joining columns are not the same distribution column.</span></span> <span data-ttu-id="2576c-132">Karma dağıtılmış tablolardan birini küçükse, çoğaltılmış bir tablo göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="2576c-132">If one of the hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="2576c-133">Bir birleştirme hepsini tabloda veri taşıma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2576c-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="2576c-134">Çoğu durumda hepsini tablolar yerine çoğaltılmış tablolar kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="2576c-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="2576c-135">Varolan bir dönüştürme dağıtılmış bir çoğaltılmış tabloya göz önünde bulundurun tablosundan:</span><span class="sxs-lookup"><span data-stu-id="2576c-135">Consider converting an existing distributed table to a replicated table when:</span></span>

- <span data-ttu-id="2576c-136">Sorgu, veri tüm işlem düğümlerine yayını kullanımı veri taşıma işlemleri planlar.</span><span class="sxs-lookup"><span data-stu-id="2576c-136">Query plans use data movement operations that broadcast the data to all the Compute nodes.</span></span> <span data-ttu-id="2576c-137">BroadcastMoveOperation pahalıdır ve sorgu performansı yavaşlatır.</span><span class="sxs-lookup"><span data-stu-id="2576c-137">The BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="2576c-138">Sorgu planında veri taşıma işlemleri görüntülemek için kullanın [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="2576c-138">To view data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="2576c-139">Çoğaltılmış tablolarda en iyi sorgu performansını değil verim zaman:</span><span class="sxs-lookup"><span data-stu-id="2576c-139">Replicated tables may not yield the best query performance when:</span></span>

- <span data-ttu-id="2576c-140">Tablo sık ekleme, güncelleştirme ve silme işlemleri vardır.</span><span class="sxs-lookup"><span data-stu-id="2576c-140">The table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="2576c-141">Bu veri işleme dili (DML) işlemleri yeniden çoğaltılmış tablo oluşturulmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2576c-141">These data manipulation language (DML) operations require a rebuild of the replicated table.</span></span> <span data-ttu-id="2576c-142">Yeniden derleme sık performans neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="2576c-143">Veri ambarı sık ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-143">The data warehouse is scaled frequently.</span></span> <span data-ttu-id="2576c-144">Veri ambarı ölçeklendirme yeniden oluşturur, işlem düğümleri sayısını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="2576c-144">Scaling a data warehouse changes the number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="2576c-145">Tablo için çok sayıda sütun olsa da, veri işlemleri genellikle az sayıda sütun erişim.</span><span class="sxs-lookup"><span data-stu-id="2576c-145">The table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="2576c-146">Tüm tabloyu çoğaltmak yerine bu senaryoda, karma değerini daha fazla etkili tablo dağıtın ve ardından sık erişilen sütunlarda dizin oluşturma olabilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-146">In this scenario, instead of replicating the entire table, it might be more effective to hash distribute the table, and then create an index on the frequently accessed columns.</span></span> <span data-ttu-id="2576c-147">Bir sorgu veri taşıma gerektirdiğinde, SQL Data Warehouse istenen sütunlarda yalnızca verileri taşır.</span><span class="sxs-lookup"><span data-stu-id="2576c-147">When a query requires data movement, SQL Data Warehouse only moves data in the requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="2576c-148">Çoğaltılmış tablolar ile basit sorgu koşulları kullanın</span><span class="sxs-lookup"><span data-stu-id="2576c-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="2576c-149">Dağıtmak veya bir tablo çoğaltmak seçmeden önce tabloda çalıştırmayı planladığınız sorgu türleri düşünün.</span><span class="sxs-lookup"><span data-stu-id="2576c-149">Before you choose to distribute or replicate a table, think about the types of queries you plan to run against the table.</span></span> <span data-ttu-id="2576c-150">Mümkün olduğunda,</span><span class="sxs-lookup"><span data-stu-id="2576c-150">Whenever possible,</span></span>

- <span data-ttu-id="2576c-151">Eşitlik veya eşitsizlik gibi basit sorgu koşulları içeren sorgular için çoğaltılmış tablolarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="2576c-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="2576c-152">DEĞİL gibi veya benzer gibi karmaşık bir sorgu koşulları içeren sorgular için Dağıtılmış tabloları kullanın.</span><span class="sxs-lookup"><span data-stu-id="2576c-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="2576c-153">CPU-yoğun sorguları en iyi iş tüm işlem düğümleri arasında dağıtıldığında gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2576c-153">CPU-intensive queries perform best when the work is distributed across all of the Compute nodes.</span></span> <span data-ttu-id="2576c-154">Örneğin, tablonun her satırında hesaplamaları çalıştırmak sorguları dağıtılmış tablolarda çoğaltılmış tablolar daha iyi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2576c-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="2576c-155">Çoğaltılmış bir tabloda, her işlem düğümü üzerinde tam kaydedildiği, çoğaltılmış bir tabloda bir CPU-yoğun sorgu karşı tüm tablo her işlem düğümünde çalışır.</span><span class="sxs-lookup"><span data-stu-id="2576c-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against the entire table on every Compute node.</span></span> <span data-ttu-id="2576c-156">Ek hesaplama sorgu performansı düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-156">The extra computation can slow query performance.</span></span>

<span data-ttu-id="2576c-157">Örneğin, bu sorgu, bir karmaşık koşuluna sahip.</span><span class="sxs-lookup"><span data-stu-id="2576c-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="2576c-158">Sağlayıcı bir çoğaltılmış tablo yerine dağıtılmış bir tablo olduğunda daha hızlı çalışır.</span><span class="sxs-lookup"><span data-stu-id="2576c-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="2576c-159">Bu örnekte, hepsini dağıtılmış veya tedarikçi karma dağıtılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-to-replicated-tables"></a><span data-ttu-id="2576c-160">Çoğaltılmış tablolar için varolan hepsini tabloları Dönüştür</span><span class="sxs-lookup"><span data-stu-id="2576c-160">Convert existing round-robin tables to replicated tables</span></span>
<span data-ttu-id="2576c-161">Hepsini tablolar zaten varsa, bu makalede açıklanan ölçütlerle karşılıyorsa bunları çoğaltılmış tablolar dönüştürme öneririz.</span><span class="sxs-lookup"><span data-stu-id="2576c-161">If you already have round-robin tables, we recommend converting them to replicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="2576c-162">Veri taşıma gereksinimini ortadan kaldırdığı çoğaltılmış tablolar hepsini tablolar üzerindeki performansı.</span><span class="sxs-lookup"><span data-stu-id="2576c-162">Replicated tables improve performance over round-robin tables because they eliminate the need for data movement.</span></span>  <span data-ttu-id="2576c-163">Hepsini tablo, veri taşıma birleştirmeler için her zaman gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2576c-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="2576c-164">Bu örnekte [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) DimSalesTerritory tablo çoğaltılmış bir tabloya değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="2576c-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) to change the DimSalesTerritory table to a replicated table.</span></span> <span data-ttu-id="2576c-165">Bu örnek DimSalesTerritory karma dağıtılmış veya hepsini bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="2576c-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

```sql
CREATE TABLE [dbo].[DimSalesTerritory_REPLICATE]   
WITH   
  (   
    CLUSTERED COLUMNSTORE INDEX,  
    DISTRIBUTION = REPLICATE  
  )  
AS SELECT * FROM [dbo].[DimSalesTerritory]
OPTION  (LABEL  = 'CTAS : DimSalesTerritory_REPLICATE') 

--Create statistics on new table
CREATE STATISTICS [SalesTerritoryKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryKey]);
CREATE STATISTICS [SalesTerritoryAlternateKey] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryAlternateKey]);
CREATE STATISTICS [SalesTerritoryRegion] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryRegion]);
CREATE STATISTICS [SalesTerritoryCountry] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryCountry]);
CREATE STATISTICS [SalesTerritoryGroup] ON [DimSalesTerritory_REPLICATE] ([SalesTerritoryGroup]);

-- Switch table names
RENAME OBJECT [dbo].[DimSalesTerritory] to [DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] TO [DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="2576c-166">Sorgu performansı hepsini karşı örneğin çoğaltılan</span><span class="sxs-lookup"><span data-stu-id="2576c-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="2576c-167">Tüm tablo her işlem düğümü üzerinde zaten varolduğundan çoğaltılmış tablo birleşimler için tüm veri hareketlerini gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="2576c-167">A replicated table does not require any data movement for joins because the entire table is already present on each Compute node.</span></span> <span data-ttu-id="2576c-168">Boyut tabloları dağıtılmış hepsini varsa, bir birleştirme her işlem düğümü tam olarak Boyut tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="2576c-168">If the dimension tables are round-robin distributed, a join copies the dimension table in full to each Compute node.</span></span> <span data-ttu-id="2576c-169">Verileri taşımak için sorgu planı BroadcastMoveOperation adlı bir işlem içerir.</span><span class="sxs-lookup"><span data-stu-id="2576c-169">To move the data, the query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="2576c-170">Bu tür veri taşıma işlemi sorgu performansını yavaşlatır ve çoğaltılmış tablolar kullanarak ortadan kalkar.</span><span class="sxs-lookup"><span data-stu-id="2576c-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="2576c-171">Sorgu planı adımları görüntülemek için kullanın [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) sistem Katalog görünümü.</span><span class="sxs-lookup"><span data-stu-id="2576c-171">To view query plan steps, use the [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="2576c-172">Örneğin, sorgudaki aşağıdaki AdventureWorks şemayla ` FactInternetSales` tablo karma dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="2576c-172">For example, in following query against the AdventureWorks schema, the ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="2576c-173">`DimDate` Ve `DimSalesTerritory` tablolardır daha küçük boyut tabloları.</span><span class="sxs-lookup"><span data-stu-id="2576c-173">The `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="2576c-174">Bu sorgu, Kuzey Amerika'da mali yılın 2004 toplam satış döndürür:</span><span class="sxs-lookup"><span data-stu-id="2576c-174">This query returns the total sales in North America for fiscal year 2004:</span></span>
 
```sql
SELECT [TotalSalesAmount] = SUM(SalesAmount)
FROM dbo.FactInternetSales s
INNER JOIN dbo.DimDate d
  ON d.DateKey = s.OrderDateKey
INNER JOIN dbo.DimSalesTerritory t
  ON t.SalesTerritoryKey = s.SalesTerritoryKey
WHERE d.FiscalYear = 2004
  AND t.SalesTerritoryGroup = 'North America'
```
<span data-ttu-id="2576c-175">Yeniden oluşturduğumuz `DimDate` ve `DimSalesTerritory` hepsini tabloları olarak.</span><span class="sxs-lookup"><span data-stu-id="2576c-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="2576c-176">Sonuç olarak, sorguyu taşıma işlemlerini birden fazla yayını olan aşağıdaki sorgu planı gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2576c-176">As a result, the query showed the following query plan, which has multiple broadcast move operations:</span></span> 
 
![Hepsini sorgu planı](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="2576c-178">Yeniden oluşturduğumuz `DimDate` ve `DimSalesTerritory` olarak çoğaltılmış tablolar ve sorguyu tekrar çalıştırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="2576c-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran the query again.</span></span> <span data-ttu-id="2576c-179">Sonuçta elde edilen sorgu planı daha kısadır ve mu değil sahip herhangi yayını taşır.</span><span class="sxs-lookup"><span data-stu-id="2576c-179">The resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Sorgu planı çoğaltılan](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="2576c-181">Çoğaltılmış tabloları değiştirmek için başarım düşünceleri</span><span class="sxs-lookup"><span data-stu-id="2576c-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="2576c-182">SQL veri ambarı ana sürüm tablosunun tutarak çoğaltılmış tablo uygular.</span><span class="sxs-lookup"><span data-stu-id="2576c-182">SQL Data Warehouse implements a replicated table by maintaining a master version of the table.</span></span> <span data-ttu-id="2576c-183">Her işlem düğümü üzerinde bir dağıtım veritabanı için ana sürüm kopyalar.</span><span class="sxs-lookup"><span data-stu-id="2576c-183">It copies the master version to one distribution database on each Compute node.</span></span> <span data-ttu-id="2576c-184">Bir değişiklik olduğunda, SQL Data Warehouse ilk ana tablo güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="2576c-184">When there is a change, SQL Data Warehouse first updates the master table.</span></span> <span data-ttu-id="2576c-185">Ardından her işlem düğümünde tabloların yeniden gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2576c-185">Then it requires a rebuild of the tables on each Compute node.</span></span> <span data-ttu-id="2576c-186">Bir yeniden oluşturma çoğaltılmış bir tablonun her işlem düğümü Tablo kopyalama ve dizinleri yeniden oluşturma içerir.</span><span class="sxs-lookup"><span data-stu-id="2576c-186">A rebuild of a replicated table includes copying the table to each Compute node and then rebuilding the indexes.</span></span>

<span data-ttu-id="2576c-187">Sonra yeniden gereklidir:</span><span class="sxs-lookup"><span data-stu-id="2576c-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="2576c-188">Veri yüklenen ya da değiştirilmiş</span><span class="sxs-lookup"><span data-stu-id="2576c-188">Data is loaded or modified</span></span>
- <span data-ttu-id="2576c-189">Veri ambarı farklı bir DWU ayarlarına ölçeklendirilir</span><span class="sxs-lookup"><span data-stu-id="2576c-189">The data warehouse is scaled to a different DWU setting</span></span>
- <span data-ttu-id="2576c-190">Tablo tanımı güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="2576c-190">Table definition is updated</span></span>

<span data-ttu-id="2576c-191">Yeniden sonra gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="2576c-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="2576c-192">Duraklatma işlemi</span><span class="sxs-lookup"><span data-stu-id="2576c-192">Pause operation</span></span>
- <span data-ttu-id="2576c-193">Sürdürme işlemi</span><span class="sxs-lookup"><span data-stu-id="2576c-193">Resume operation</span></span>

<span data-ttu-id="2576c-194">Veri hemen değiştirildikten sonra yeniden gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="2576c-194">The rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="2576c-195">Bunun yerine, yeniden tablodan bir sorgu seçer ilk kez tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="2576c-195">Instead, the rebuild is triggered the first time a query selects from the table.</span></span>  <span data-ttu-id="2576c-196">Tablodaki ilk select deyimi içinde çoğaltılmış tablosunu yeniden adımlardır.</span><span class="sxs-lookup"><span data-stu-id="2576c-196">Within the initial select statement from the table are steps to rebuild the replicated table.</span></span>  <span data-ttu-id="2576c-197">Yeniden oluşturma sorgu içinde yapıldığından, ilk select deyiminde etkisini tablo boyutuna bağlı olarak önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-197">Because the rebuild is done within the query, the impact to the initial select statement could be significant depending on the size of the table.</span></span>  <span data-ttu-id="2576c-198">Birden çok çoğaltılmış tablolar yeniden gereken söz konusuysa, her kopya seri olarak deyimi içindeki adımları olarak yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2576c-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within the statement.</span></span>  <span data-ttu-id="2576c-199">Verileri korumak için özel bir kilit çoğaltılmış tablo yeniden sırasında tutarlılık tabloda alınır.</span><span class="sxs-lookup"><span data-stu-id="2576c-199">To maintain data consistency during the rebuild of the replicated table an exclusive lock is taken on the table.</span></span>  <span data-ttu-id="2576c-200">Kilit yeniden süresince tabloya tüm erişimi engeller.</span><span class="sxs-lookup"><span data-stu-id="2576c-200">The lock prevents all access to the table for the duration of the rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="2576c-201">Dizinleri ölçülü kullanın</span><span class="sxs-lookup"><span data-stu-id="2576c-201">Use indexes conservatively</span></span>
<span data-ttu-id="2576c-202">Standart dizin oluşturma yöntemleri çoğaltılmış tablolar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2576c-202">Standard indexing practices apply to replicated tables.</span></span> <span data-ttu-id="2576c-203">SQL veri ambarı her çoğaltılmış tablosu dizini yeniden oluşturma bir parçası olarak yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2576c-203">SQL Data Warehouse rebuilds each replicated table index as part of the rebuild.</span></span> <span data-ttu-id="2576c-204">Performans kazancı dizinleri yeniden oluşturma, maliyetinden ağır yalnızca dizinler kullanın.</span><span class="sxs-lookup"><span data-stu-id="2576c-204">Only use indexes when the performance gain outweighs the cost of rebuilding the indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="2576c-205">Toplu veri yükler</span><span class="sxs-lookup"><span data-stu-id="2576c-205">Batch data loads</span></span>
<span data-ttu-id="2576c-206">Verileri çoğaltılmış tablolara yüklenirken yükleri birlikte toplu işleme tarafından yeniden küçültmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-206">When loading data into replicated tables, try to minimize rebuilds by batching loads together.</span></span> <span data-ttu-id="2576c-207">Select deyimi çalıştırmadan önce tüm toplu iş yükleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2576c-207">Perform all the batched loads before running select statements.</span></span>

<span data-ttu-id="2576c-208">Örneğin, bu yük düzeni dört kaynaktan verileri yükler ve dört yeniden çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="2576c-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="2576c-209">1 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-209">Load from source 1.</span></span>
- <span data-ttu-id="2576c-210">SELECT deyimi Tetikleyicileri 1 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2576c-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="2576c-211">2 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-211">Load from source 2.</span></span>
- <span data-ttu-id="2576c-212">SELECT deyimi Tetikleyicileri 2 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2576c-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="2576c-213">3 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-213">Load from source 3.</span></span>
- <span data-ttu-id="2576c-214">SELECT deyimi Tetikleyicileri 3 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2576c-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="2576c-215">4 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-215">Load from source 4.</span></span>
- <span data-ttu-id="2576c-216">SELECT deyimi Tetikleyicileri 4 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2576c-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="2576c-217">Örneğin, bu yük düzeni dört kaynaktan verileri yükler, ancak yalnızca bir yeniden çağırır.</span><span class="sxs-lookup"><span data-stu-id="2576c-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="2576c-218">1 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-218">Load from source 1.</span></span>
- <span data-ttu-id="2576c-219">2 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-219">Load from source 2.</span></span>
- <span data-ttu-id="2576c-220">3 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-220">Load from source 3.</span></span>
- <span data-ttu-id="2576c-221">4 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2576c-221">Load from source 4.</span></span>
- <span data-ttu-id="2576c-222">SELECT deyimi Tetikleyicileri yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2576c-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="2576c-223">Toplu yükleme sonrasında çoğaltılmış tablo yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="2576c-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="2576c-224">Tutarlı bir sorgu yürütme süreleri sağlamak için toplu yükleme sonrasında çoğaltılmış tablolar yenilenmesini zorlama öneririz.</span><span class="sxs-lookup"><span data-stu-id="2576c-224">To ensure consistent query execution times, we recommend forcing a refresh of the replicated tables after a batch load.</span></span> <span data-ttu-id="2576c-225">Aksi durumda, ilk sorgu tabloları yenilemek, dizinleri yeniden oluşturma içeren beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2576c-225">Otherwise, the first query must wait for the tables to refresh, which includes rebuilding the indexes.</span></span> <span data-ttu-id="2576c-226">Boyut ve etkilenen çoğaltılmış tablolar sayısına bağlı olarak, performans etkisi önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="2576c-226">Depending on the size and number of replicated tables affected, the performance impact can be significant.</span></span>  

<span data-ttu-id="2576c-227">Bu sorgu kullanan [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV değiştirildi, ancak değil yeniden çoğaltılmış tablolarda listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="2576c-227">This query uses the [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV to list the replicated tables that have been modified, but not rebuilt.</span></span>

```sql 
SELECT [ReplicatedTable] = t.[name]
  FROM sys.tables t  
  JOIN sys.pdw_replicated_table_cache_state c  
    ON c.object_id = t.object_id 
  JOIN sys.pdw_table_distribution_properties p 
    ON p.object_id = t.object_id 
  WHERE c.[state] = 'NotReady'
    AND p.[distribution_policy_desc] = 'REPLICATE'
```
 
<span data-ttu-id="2576c-228">Bir yeniden oluşturma zorlamak için her bir tabloda yukarıdaki çıktıda aşağıdaki deyimini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2576c-228">To force a rebuild, run the following statement on each table in the preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="2576c-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2576c-229">Next steps</span></span> 
<span data-ttu-id="2576c-230">Çoğaltılmış bir tablo oluşturmak için bu deyimleri birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="2576c-230">To create a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="2576c-231">TABLOSU (Azure SQL Data Warehouse) oluşturma</span><span class="sxs-lookup"><span data-stu-id="2576c-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="2576c-232">TABLE AS SELECT (Azure SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="2576c-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="2576c-233">Dağıtılmış tabloları genel bakış için bkz: [dağıtılmış tabloları](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="2576c-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



