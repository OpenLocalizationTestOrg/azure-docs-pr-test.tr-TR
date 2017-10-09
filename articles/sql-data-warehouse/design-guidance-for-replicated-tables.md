---
title: "aaaDesign yönergeler için çoğaltılmış tablolarda - Azure SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: 5d405b8c404c65177b387ba959126839c1cf8799
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-guidance-for-using-replicated-tables-in-azure-sql-data-warehouse"></a><span data-ttu-id="d2503-103">Azure SQL Data Warehouse'da çoğaltılmış tablolar kullanmaya yönelik kılavuz tasarım</span><span class="sxs-lookup"><span data-stu-id="d2503-103">Design guidance for using replicated tables in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d2503-104">Bu makalede SQL Data Warehouse şemanızı çoğaltılmış tablolarda tasarlamak için öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2503-104">This article gives recommendations for designing replicated tables in your SQL Data Warehouse schema.</span></span> <span data-ttu-id="d2503-105">Bu öneriler tooimprove sorgu performansı veri hareketlerini ve sorgu karmaşıklık azaltarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2503-105">Use these recommendations tooimprove query performance by reducing data movement and query complexity.</span></span>

> [!NOTE]
> <span data-ttu-id="d2503-106">Merhaba çoğaltılmış tablo şu anda genel önizlemede özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d2503-106">hello replicated table feature is currently in public preview.</span></span> <span data-ttu-id="d2503-107">Bazı davranışları konu toochange ' dir.</span><span class="sxs-lookup"><span data-stu-id="d2503-107">Some behaviors are subject toochange.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="d2503-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d2503-108">Prerequisites</span></span>
<span data-ttu-id="d2503-109">Bu makalede, veri dağıtımı ve SQL Data Warehouse veri taşıma kavramlarına alışık olduğunuz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="d2503-109">This article assumes you are familiar with data distribution and data movement concepts in SQL Data Warehouse.</span></span>  <span data-ttu-id="d2503-110">Daha fazla bilgi için bkz: [Dağıtılmış veri](sql-data-warehouse-distributed-data.md).</span><span class="sxs-lookup"><span data-stu-id="d2503-110">For more information, see [Distributed data](sql-data-warehouse-distributed-data.md).</span></span> 

<span data-ttu-id="d2503-111">Tablo Tasarımı bir parçası olarak, verilerinizi ve hello verileri nasıl sorgulanır hakkında mümkün olduğunca anlayın.</span><span class="sxs-lookup"><span data-stu-id="d2503-111">As part of table design, understand as much as possible about your data and how hello data is queried.</span></span>  <span data-ttu-id="d2503-112">Örneğin, aşağıdaki soruları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="d2503-112">For example, consider these questions:</span></span>

- <span data-ttu-id="d2503-113">Merhaba tablo büyüklüğü nedir?</span><span class="sxs-lookup"><span data-stu-id="d2503-113">How large is hello table?</span></span>   
- <span data-ttu-id="d2503-114">Merhaba tablo ne sıklıkla yenileniyor?</span><span class="sxs-lookup"><span data-stu-id="d2503-114">How often is hello table refreshed?</span></span>   
- <span data-ttu-id="d2503-115">Bir veri ambarı olgu ve boyut tabloları var mı?</span><span class="sxs-lookup"><span data-stu-id="d2503-115">Do I have fact and dimension tables in a data warehouse?</span></span>   

## <a name="what-is-a-replicated-table"></a><span data-ttu-id="d2503-116">Çoğaltılmış tablosu nedir?</span><span class="sxs-lookup"><span data-stu-id="d2503-116">What is a replicated table?</span></span>
<span data-ttu-id="d2503-117">Yinelenen Tablo Merhaba tablonun erişilebilir tam bir kopyasını her işlem düğümünde sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d2503-117">A replicated table has a full copy of hello table accessible on each Compute node.</span></span> <span data-ttu-id="d2503-118">Tablo çoğaltma JOIN veya toplama önce işlem düğümleri arasında hello gerek tootransfer verileri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d2503-118">Replicating a table removes hello need tootransfer data among Compute nodes before a join or aggregation.</span></span> <span data-ttu-id="d2503-119">Merhaba tablosunda birden çok kopya bulunduğundan hello tablo boyutunu sıkıştırılmış 2 GB'tan daha az olduğunda çoğaltılmış tablolarda en iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="d2503-119">Since hello table has multiple copies, replicated tables work best when hello table size is less than 2 GB compressed.</span></span>

<span data-ttu-id="d2503-120">Merhaba Aşağıdaki diyagramda her işlem düğümü üzerinde erişilebilir olan bir çoğaltılmış tablo gösterir.</span><span class="sxs-lookup"><span data-stu-id="d2503-120">hello following diagram shows a replicated table that is accessible on each Compute node.</span></span> <span data-ttu-id="d2503-121">SQL veri ambarı'nda hello çoğaltılmış tablo tam kopyalanan tooa dağıtım her işlem düğümünde veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="d2503-121">In SQL Data Warehouse, hello replicated table is fully copied tooa distribution database on each Compute node.</span></span> 

<span data-ttu-id="d2503-122">![Yinelenmiş tablo](media/guidance-for-using-replicated-tables/replicated-table.png "yinelenmiş tablosu")</span><span class="sxs-lookup"><span data-stu-id="d2503-122">![Replicated table](media/guidance-for-using-replicated-tables/replicated-table.png "Replicated table")</span></span>  

<span data-ttu-id="d2503-123">İyi bir yıldız şemasının küçük boyut tabloları için tabloları iş çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="d2503-123">Replicated tables work well for small dimension tables in a star schema.</span></span> <span data-ttu-id="d2503-124">Boyut tabloları genellikle uygun toostore kolaylaştıran bir boyutta olduğundan ve birden çok kopyasını sürdürün.</span><span class="sxs-lookup"><span data-stu-id="d2503-124">Dimension tables are usually of a size that makes it feasible toostore and maintain multiple copies.</span></span> <span data-ttu-id="d2503-125">Boyutların müşteri adı ve adres ve ürün ayrıntıları gibi yavaş değişir açıklayıcı verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="d2503-125">Dimensions store descriptive data that changes slowly, such as customer name and address, and product details.</span></span> <span data-ttu-id="d2503-126">yavaş hello veri yapısını değiştirme hello toofewer yeniden hello çoğaltılmış tablosunun yol açar.</span><span class="sxs-lookup"><span data-stu-id="d2503-126">hello slowly changing nature of hello data leads toofewer rebuilds of hello replicated table.</span></span> 

<span data-ttu-id="d2503-127">Çoğaltılan kullanmayı tablosundan:</span><span class="sxs-lookup"><span data-stu-id="d2503-127">Consider using a replicated table when:</span></span>

- <span data-ttu-id="d2503-128">Merhaba tablo diskteki 2 GB'den az, satır sayısı hello bağımsız olarak boyutudur.</span><span class="sxs-lookup"><span data-stu-id="d2503-128">hello table size on disk is less than 2 GB, regardless of hello number of rows.</span></span> <span data-ttu-id="d2503-129">bir tablonun toofind hello boyutunu, hello kullanabilir [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) komutu: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span><span class="sxs-lookup"><span data-stu-id="d2503-129">toofind hello size of a table, you can use hello [DBCC PDW_SHOWSPACEUSED](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql) command: `DBCC PDW_SHOWSPACEUSED('ReplTableCandidate')`.</span></span> 
- <span data-ttu-id="d2503-130">Merhaba tablo, aksi halde veri taşıma gerektirecek birleştirme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2503-130">hello table is used in joins that would otherwise require data movement.</span></span> <span data-ttu-id="d2503-131">Örneğin, Hello katılma sütunları hello değil, aynı dağıtım sütun tablolarda karma dağıtılmış bir birleştirme veri taşıma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-131">For example, a join on hash-distributed tables requires data movement when hello joining columns are not hello same distribution column.</span></span> <span data-ttu-id="d2503-132">Merhaba karma dağıtılmış tablolardan biri küçükse, çoğaltılmış bir tablo göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="d2503-132">If one of hello hash-distributed tables is small, consider a replicated table.</span></span> <span data-ttu-id="d2503-133">Bir birleştirme hepsini tabloda veri taşıma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-133">A join on a round-robin table requires data movement.</span></span> <span data-ttu-id="d2503-134">Çoğu durumda hepsini tablolar yerine çoğaltılmış tablolar kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d2503-134">We recommend using replicated tables instead of round-robin tables in most cases.</span></span> 


<span data-ttu-id="d2503-135">Varolan bir dönüştürme dağıtılmış çoğaltılmış tablo tooa göz önünde bulundurun tablosundan:</span><span class="sxs-lookup"><span data-stu-id="d2503-135">Consider converting an existing distributed table tooa replicated table when:</span></span>

- <span data-ttu-id="d2503-136">Sorgu hello veri tooall hello işlem düğümleri yayını kullanımı veri taşıma işlemleri planlar.</span><span class="sxs-lookup"><span data-stu-id="d2503-136">Query plans use data movement operations that broadcast hello data tooall hello Compute nodes.</span></span> <span data-ttu-id="d2503-137">Merhaba BroadcastMoveOperation pahalıdır ve sorgu performansı yavaşlatır.</span><span class="sxs-lookup"><span data-stu-id="d2503-137">hello BroadcastMoveOperation is expensive and slows query performance.</span></span> <span data-ttu-id="d2503-138">Sorgu planlarda tooview veri taşıma işlemleri kullanmak [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="d2503-138">tooview data movement operations in query plans, use [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql).</span></span>
 
<span data-ttu-id="d2503-139">Çoğaltılmış tablolar hello en iyi sorgu performansını değil verim zaman:</span><span class="sxs-lookup"><span data-stu-id="d2503-139">Replicated tables may not yield hello best query performance when:</span></span>

- <span data-ttu-id="d2503-140">Merhaba tablosu sık ekleme, güncelleştirme ve silme işlemleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d2503-140">hello table has frequent insert, update, and delete operations.</span></span> <span data-ttu-id="d2503-141">Bu veri işleme dili (DML) işlemleri yeniden çoğaltılan Merhaba tablonun gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-141">These data manipulation language (DML) operations require a rebuild of hello replicated table.</span></span> <span data-ttu-id="d2503-142">Yeniden derleme sık performans neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2503-142">Rebuilding frequently can cause slower performance.</span></span>
- <span data-ttu-id="d2503-143">Merhaba veri ambarı sık ölçeklendirilir.</span><span class="sxs-lookup"><span data-stu-id="d2503-143">hello data warehouse is scaled frequently.</span></span> <span data-ttu-id="d2503-144">Veri ambarı ölçeklendirme hello yeniden oluşturur, işlem düğümleri sayısı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-144">Scaling a data warehouse changes hello number of Compute nodes, which incurs a rebuild.</span></span>
- <span data-ttu-id="d2503-145">Merhaba tablosunda çok sayıda sütun var, ancak veri işlemleri genellikle az sayıda sütun erişim.</span><span class="sxs-lookup"><span data-stu-id="d2503-145">hello table has a large number of columns, but data operations typically access only a small number of columns.</span></span> <span data-ttu-id="d2503-146">Merhaba tüm tablo çoğaltmak yerine bu senaryoda, daha etkili toohash olabilir hello tablo dağıtın ve ardından sık erişilen hello sütunlarda bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2503-146">In this scenario, instead of replicating hello entire table, it might be more effective toohash distribute hello table, and then create an index on hello frequently accessed columns.</span></span> <span data-ttu-id="d2503-147">Ne zaman hello taşır verilerde sütunları istenen yalnızca bir sorgu veri taşıma, SQL Data Warehouse gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-147">When a query requires data movement, SQL Data Warehouse only moves data in hello requested columns.</span></span> 



## <a name="use-replicated-tables-with-simple-query-predicates"></a><span data-ttu-id="d2503-148">Çoğaltılmış tablolar ile basit sorgu koşulları kullanın</span><span class="sxs-lookup"><span data-stu-id="d2503-148">Use replicated tables with simple query predicates</span></span>
<span data-ttu-id="d2503-149">Toodistribute seçin veya bir tablo çoğaltmak önce toorun hello tabloda plan sorgu hello türleri düşünün.</span><span class="sxs-lookup"><span data-stu-id="d2503-149">Before you choose toodistribute or replicate a table, think about hello types of queries you plan toorun against hello table.</span></span> <span data-ttu-id="d2503-150">Mümkün olduğunda,</span><span class="sxs-lookup"><span data-stu-id="d2503-150">Whenever possible,</span></span>

- <span data-ttu-id="d2503-151">Eşitlik veya eşitsizlik gibi basit sorgu koşulları içeren sorgular için çoğaltılmış tablolarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2503-151">Use replicated tables for queries with simple query predicates, such as equality or inequality.</span></span>
- <span data-ttu-id="d2503-152">DEĞİL gibi veya benzer gibi karmaşık bir sorgu koşulları içeren sorgular için Dağıtılmış tabloları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2503-152">Use distributed tables for queries with complex query predicates, such as LIKE or NOT LIKE.</span></span>

<span data-ttu-id="d2503-153">CPU-yoğun sorguları en iyi şekilde Hello iş tüm hello işlem düğümleri arasında dağıtıldığında gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d2503-153">CPU-intensive queries perform best when hello work is distributed across all of hello Compute nodes.</span></span> <span data-ttu-id="d2503-154">Örneğin, tablonun her satırında hesaplamaları çalıştırmak sorguları dağıtılmış tablolarda çoğaltılmış tablolar daha iyi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d2503-154">For example, queries that run computations on each row of a table perform better on distributed tables than replicated tables.</span></span> <span data-ttu-id="d2503-155">Çoğaltılmış tablo her işlem düğümü üzerinde tam kaydedildiği çoğaltılmış bir tabloda bir CPU-yoğun sorgu karşı hello tüm tablo her işlem düğümünde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d2503-155">Since a replicated table is stored in full on each Compute node, a CPU-intensive query against a replicated table runs against hello entire table on every Compute node.</span></span> <span data-ttu-id="d2503-156">Merhaba ek hesaplama sorgu performansı düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="d2503-156">hello extra computation can slow query performance.</span></span>

<span data-ttu-id="d2503-157">Örneğin, bu sorgu, bir karmaşık koşuluna sahip.</span><span class="sxs-lookup"><span data-stu-id="d2503-157">For example, this query has a complex predicate.</span></span>  <span data-ttu-id="d2503-158">Sağlayıcı bir çoğaltılmış tablo yerine dağıtılmış bir tablo olduğunda daha hızlı çalışır.</span><span class="sxs-lookup"><span data-stu-id="d2503-158">It runs faster when supplier is a distributed table instead of a replicated table.</span></span> <span data-ttu-id="d2503-159">Bu örnekte, hepsini dağıtılmış veya tedarikçi karma dağıtılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2503-159">In this example, supplier can be hash-distributed or round-robin distributed.</span></span>

```sql

SELECT EnglishProductName 
FROM DimProduct 
WHERE EnglishDescription LIKE '%frame%comfortable%'

```

## <a name="convert-existing-round-robin-tables-tooreplicated-tables"></a><span data-ttu-id="d2503-160">Varolan hepsini tabloları tooreplicated tabloları Dönüştür</span><span class="sxs-lookup"><span data-stu-id="d2503-160">Convert existing round-robin tables tooreplicated tables</span></span>
<span data-ttu-id="d2503-161">Hepsini tablolar zaten varsa, bu makalede açıklanan ölçütlerle karşılıyorsa bunları dönüştürme tooreplicated tabloları öneririz.</span><span class="sxs-lookup"><span data-stu-id="d2503-161">If you already have round-robin tables, we recommend converting them tooreplicated tables if they meet with criteria outlined in this article.</span></span> <span data-ttu-id="d2503-162">Veri taşıma hello gereksinimini ortadan kaldırdığı çoğaltılmış tablolar hepsini tablolar üzerindeki performansı.</span><span class="sxs-lookup"><span data-stu-id="d2503-162">Replicated tables improve performance over round-robin tables because they eliminate hello need for data movement.</span></span>  <span data-ttu-id="d2503-163">Hepsini tablo, veri taşıma birleştirmeler için her zaman gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-163">A round-robin table always requires data movement for joins.</span></span> 

<span data-ttu-id="d2503-164">Bu örnekte [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory tablo tooa çoğaltılmış tablo.</span><span class="sxs-lookup"><span data-stu-id="d2503-164">This example uses [CTAS](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse) toochange hello DimSalesTerritory table tooa replicated table.</span></span> <span data-ttu-id="d2503-165">Bu örnek DimSalesTerritory karma dağıtılmış veya hepsini bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="d2503-165">This example works regardless of whether DimSalesTerritory is hash-distributed or round-robin.</span></span>

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
RENAME OBJECT [dbo].[DimSalesTerritory] too[DimSalesTerritory_old];
RENAME OBJECT [dbo].[DimSalesTerritory_REPLICATE] too[DimSalesTerritory];

DROP TABLE [dbo].[DimSalesTerritory_old];
```  

### <a name="query-performance-example-for-round-robin-versus-replicated"></a><span data-ttu-id="d2503-166">Sorgu performansı hepsini karşı örneğin çoğaltılan</span><span class="sxs-lookup"><span data-stu-id="d2503-166">Query performance example for round-robin versus replicated</span></span> 

<span data-ttu-id="d2503-167">Merhaba tüm tablo her işlem düğümü üzerinde zaten varolduğundan çoğaltılmış tablo birleşimler için tüm veri hareketlerini gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="d2503-167">A replicated table does not require any data movement for joins because hello entire table is already present on each Compute node.</span></span> <span data-ttu-id="d2503-168">Merhaba boyut tabloları dağıtılmış hepsini varsa, bir birleştirme tam tooeach işlem düğümünde hello Boyut tablosuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d2503-168">If hello dimension tables are round-robin distributed, a join copies hello dimension table in full tooeach Compute node.</span></span> <span data-ttu-id="d2503-169">toomove hello veri hello sorgu planı BroadcastMoveOperation adlı bir işlem içerir.</span><span class="sxs-lookup"><span data-stu-id="d2503-169">toomove hello data, hello query plan contains an operation called BroadcastMoveOperation.</span></span> <span data-ttu-id="d2503-170">Bu tür veri taşıma işlemi sorgu performansını yavaşlatır ve çoğaltılmış tablolar kullanarak ortadan kalkar.</span><span class="sxs-lookup"><span data-stu-id="d2503-170">This type of data movement operation slows query performance and is eliminated by using replicated tables.</span></span> <span data-ttu-id="d2503-171">tooview sorgu planı adımları, kullanmak hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) sistem Katalog görünümü.</span><span class="sxs-lookup"><span data-stu-id="d2503-171">tooview query plan steps, use hello [sys.dm_pdw_request_steps](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql) system catalog view.</span></span> 

<span data-ttu-id="d2503-172">Örneğin, hello AdventureWorks şemayla aşağıdaki sorguda hello ` FactInternetSales` tablo karma dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="d2503-172">For example, in following query against hello AdventureWorks schema, hello ` FactInternetSales` table is hash-distributed.</span></span> <span data-ttu-id="d2503-173">Merhaba `DimDate` ve `DimSalesTerritory` tablolardır daha küçük boyut tabloları.</span><span class="sxs-lookup"><span data-stu-id="d2503-173">hello `DimDate` and `DimSalesTerritory` tables are smaller dimension tables.</span></span> <span data-ttu-id="d2503-174">Bu sorgu, Kuzey Amerika'da mali yılın 2004 hello toplam satış döndürür:</span><span class="sxs-lookup"><span data-stu-id="d2503-174">This query returns hello total sales in North America for fiscal year 2004:</span></span>
 
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
<span data-ttu-id="d2503-175">Yeniden oluşturduğumuz `DimDate` ve `DimSalesTerritory` hepsini tabloları olarak.</span><span class="sxs-lookup"><span data-stu-id="d2503-175">We re-created `DimDate` and `DimSalesTerritory` as round-robin tables.</span></span> <span data-ttu-id="d2503-176">Sonuç olarak, hello sorgu işlemleri taşıdığınız çoklu yayın sahip sorgu planı aşağıdaki hello gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d2503-176">As a result, hello query showed hello following query plan, which has multiple broadcast move operations:</span></span> 
 
![Hepsini sorgu planı](media/design-guidance-for-replicated-tables/round-robin-tables-query-plan.jpg) 

<span data-ttu-id="d2503-178">Yeniden oluşturduğumuz `DimDate` ve `DimSalesTerritory` olarak çoğaltılmış tablolar ve hello sorgu tekrar çalıştırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d2503-178">We re-created `DimDate` and `DimSalesTerritory` as replicated tables, and ran hello query again.</span></span> <span data-ttu-id="d2503-179">Hello elde edilen sorgu planı daha kısadır ve mu değil sahip herhangi yayını taşır.</span><span class="sxs-lookup"><span data-stu-id="d2503-179">hello resulting query plan is much shorter and does not have any broadcast moves.</span></span>

![Sorgu planı çoğaltılan](media/design-guidance-for-replicated-tables/replicated-tables-query-plan.jpg) 


## <a name="performance-considerations-for-modifying-replicated-tables"></a><span data-ttu-id="d2503-181">Çoğaltılmış tabloları değiştirmek için başarım düşünceleri</span><span class="sxs-lookup"><span data-stu-id="d2503-181">Performance considerations for modifying replicated tables</span></span>
<span data-ttu-id="d2503-182">SQL veri ambarı ana sürüm Merhaba tablonun tutarak çoğaltılmış tablo uygular.</span><span class="sxs-lookup"><span data-stu-id="d2503-182">SQL Data Warehouse implements a replicated table by maintaining a master version of hello table.</span></span> <span data-ttu-id="d2503-183">Merhaba ana sürüm tooone dağıtım veritabanı her işlem düğümü üzerinde kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d2503-183">It copies hello master version tooone distribution database on each Compute node.</span></span> <span data-ttu-id="d2503-184">Bir değişiklik olduğunda, SQL Data Warehouse hello ana tablo ilk güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-184">When there is a change, SQL Data Warehouse first updates hello master table.</span></span> <span data-ttu-id="d2503-185">Ardından her işlem düğümünde Merhaba tablonun yeniden gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d2503-185">Then it requires a rebuild of hello tables on each Compute node.</span></span> <span data-ttu-id="d2503-186">Çoğaltılmış bir tablonun yeniden hello tablo tooeach işlem düğümü kopyalama ve hello dizinleri yeniden oluşturma içerir.</span><span class="sxs-lookup"><span data-stu-id="d2503-186">A rebuild of a replicated table includes copying hello table tooeach Compute node and then rebuilding hello indexes.</span></span>

<span data-ttu-id="d2503-187">Sonra yeniden gereklidir:</span><span class="sxs-lookup"><span data-stu-id="d2503-187">Rebuilds are required after:</span></span>
- <span data-ttu-id="d2503-188">Veri yüklenen ya da değiştirilmiş</span><span class="sxs-lookup"><span data-stu-id="d2503-188">Data is loaded or modified</span></span>
- <span data-ttu-id="d2503-189">ölçeklendirilmiş tooa farklı DWU ayarını Hello veri ambarıdır.</span><span class="sxs-lookup"><span data-stu-id="d2503-189">hello data warehouse is scaled tooa different DWU setting</span></span>
- <span data-ttu-id="d2503-190">Tablo tanımı güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="d2503-190">Table definition is updated</span></span>

<span data-ttu-id="d2503-191">Yeniden sonra gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="d2503-191">Rebuilds are not required after:</span></span>
- <span data-ttu-id="d2503-192">Duraklatma işlemi</span><span class="sxs-lookup"><span data-stu-id="d2503-192">Pause operation</span></span>
- <span data-ttu-id="d2503-193">Sürdürme işlemi</span><span class="sxs-lookup"><span data-stu-id="d2503-193">Resume operation</span></span>

<span data-ttu-id="d2503-194">Veri hemen değiştirildikten sonra hello yeniden gerçekleşmez.</span><span class="sxs-lookup"><span data-stu-id="d2503-194">hello rebuild does not happen immediately after data is modified.</span></span> <span data-ttu-id="d2503-195">Bunun yerine, hello yeniden tetiklenir hello ilk kez bir sorgu hello tablosundan seçer.</span><span class="sxs-lookup"><span data-stu-id="d2503-195">Instead, hello rebuild is triggered hello first time a query selects from hello table.</span></span>  <span data-ttu-id="d2503-196">Merhaba ilk select deyimi hello tablosundan adımları toorebuild hello çoğaltılmış tablo ağdadır.</span><span class="sxs-lookup"><span data-stu-id="d2503-196">Within hello initial select statement from hello table are steps toorebuild hello replicated table.</span></span>  <span data-ttu-id="d2503-197">Merhaba yeniden hello sorguyla yapıldığından hello etkisi toohello ilk select deyiminde hello tablo hello boyutuna bağlı olarak önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2503-197">Because hello rebuild is done within hello query, hello impact toohello initial select statement could be significant depending on hello size of hello table.</span></span>  <span data-ttu-id="d2503-198">Birden çok çoğaltılmış tablolar yeniden gereken söz konusuysa, her kopya seri olarak hello deyimi içindeki adımları olarak yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d2503-198">If multiple replicated tables are involved that need a rebuild, each copy is rebuilt serially as steps within hello statement.</span></span>  <span data-ttu-id="d2503-199">toomaintain veri tutarlılığını hello hello yeniden sırasında özel bir kilit hello tablo üzerinde gerçekleştirilecek tablo çoğaltılan.</span><span class="sxs-lookup"><span data-stu-id="d2503-199">toomaintain data consistency during hello rebuild of hello replicated table an exclusive lock is taken on hello table.</span></span>  <span data-ttu-id="d2503-200">Merhaba kilit tüm erişim toohello tablo hello yeniden hello süresince engeller.</span><span class="sxs-lookup"><span data-stu-id="d2503-200">hello lock prevents all access toohello table for hello duration of hello rebuild.</span></span> 

### <a name="use-indexes-conservatively"></a><span data-ttu-id="d2503-201">Dizinleri ölçülü kullanın</span><span class="sxs-lookup"><span data-stu-id="d2503-201">Use indexes conservatively</span></span>
<span data-ttu-id="d2503-202">Standart dizin oluşturma yöntemleri tooreplicated tabloları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d2503-202">Standard indexing practices apply tooreplicated tables.</span></span> <span data-ttu-id="d2503-203">SQL veri ambarı her çoğaltılmış tablo dizin hello yeniden parçası olarak yeniden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d2503-203">SQL Data Warehouse rebuilds each replicated table index as part of hello rebuild.</span></span> <span data-ttu-id="d2503-204">Merhaba performans kazancı hello dizinleri yeniden oluşturma, hello maliyetinden ağır yalnızca dizinler kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2503-204">Only use indexes when hello performance gain outweighs hello cost of rebuilding hello indexes.</span></span>  
 
### <a name="batch-data-loads"></a><span data-ttu-id="d2503-205">Toplu veri yükler</span><span class="sxs-lookup"><span data-stu-id="d2503-205">Batch data loads</span></span>
<span data-ttu-id="d2503-206">Verileri çoğaltılmış tablolara yüklenirken yükleri birlikte toplu işleme tarafından toominimize yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-206">When loading data into replicated tables, try toominimize rebuilds by batching loads together.</span></span> <span data-ttu-id="d2503-207">Select deyimi çalıştırmadan önce tüm toplu hale hello yükleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d2503-207">Perform all hello batched loads before running select statements.</span></span>

<span data-ttu-id="d2503-208">Örneğin, bu yük düzeni dört kaynaktan verileri yükler ve dört yeniden çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d2503-208">For example, this load pattern loads data from four sources and invokes four rebuilds.</span></span> 

- <span data-ttu-id="d2503-209">1 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-209">Load from source 1.</span></span>
- <span data-ttu-id="d2503-210">SELECT deyimi Tetikleyicileri 1 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2503-210">Select statement triggers rebuild 1.</span></span>
- <span data-ttu-id="d2503-211">2 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-211">Load from source 2.</span></span>
- <span data-ttu-id="d2503-212">SELECT deyimi Tetikleyicileri 2 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2503-212">Select statement triggers rebuild 2.</span></span>
- <span data-ttu-id="d2503-213">3 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-213">Load from source 3.</span></span>
- <span data-ttu-id="d2503-214">SELECT deyimi Tetikleyicileri 3 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2503-214">Select statement triggers rebuild 3.</span></span>
- <span data-ttu-id="d2503-215">4 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-215">Load from source 4.</span></span>
- <span data-ttu-id="d2503-216">SELECT deyimi Tetikleyicileri 4 yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2503-216">Select statement triggers rebuild 4.</span></span>

<span data-ttu-id="d2503-217">Örneğin, bu yük düzeni dört kaynaktan verileri yükler, ancak yalnızca bir yeniden çağırır.</span><span class="sxs-lookup"><span data-stu-id="d2503-217">For example, this load pattern loads data from four sources, but only invokes one rebuild.</span></span>

- <span data-ttu-id="d2503-218">1 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-218">Load from source 1.</span></span>
- <span data-ttu-id="d2503-219">2 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-219">Load from source 2.</span></span>
- <span data-ttu-id="d2503-220">3 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-220">Load from source 3.</span></span>
- <span data-ttu-id="d2503-221">4 kaynağından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d2503-221">Load from source 4.</span></span>
- <span data-ttu-id="d2503-222">SELECT deyimi Tetikleyicileri yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2503-222">Select statement triggers rebuild.</span></span>


### <a name="rebuild-a-replicated-table-after-a-batch-load"></a><span data-ttu-id="d2503-223">Toplu yükleme sonrasında çoğaltılmış tablo yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2503-223">Rebuild a replicated table after a batch load</span></span>
<span data-ttu-id="d2503-224">tooensure tutarlı bir sorgu yürütme sürelerinin toplu yükleme sonrasında hello çoğaltılmış tablolar yenilenmesini zorlama öneririz.</span><span class="sxs-lookup"><span data-stu-id="d2503-224">tooensure consistent query execution times, we recommend forcing a refresh of hello replicated tables after a batch load.</span></span> <span data-ttu-id="d2503-225">Aksi takdirde hello ilk sorgu hello dizinleri yeniden oluşturma içerir hello tabloları toorefresh için beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2503-225">Otherwise, hello first query must wait for hello tables toorefresh, which includes rebuilding hello indexes.</span></span> <span data-ttu-id="d2503-226">Merhaba boyut ve etkilenen çoğaltılmış tablolar sayısına bağlı olarak hello performans etkisi önemli olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2503-226">Depending on hello size and number of replicated tables affected, hello performance impact can be significant.</span></span>  

<span data-ttu-id="d2503-227">Bu sorgu hello kullanan [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello çoğaltılan değiştirildi, ancak değil yeniden tablolar.</span><span class="sxs-lookup"><span data-stu-id="d2503-227">This query uses hello [sys.pdw_replicated_table_cache_state](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-pdw-replicated-table-cache-state-transact-sql) DMV toolist hello replicated tables that have been modified, but not rebuilt.</span></span>

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
 
<span data-ttu-id="d2503-228">Çıktı önceki hello her tablosunda deyiminden hello çalıştırmak tooforce bir yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d2503-228">tooforce a rebuild, run hello following statement on each table in hello preceding output.</span></span> 

```sql
SELECT TOP 1 * FROM [ReplicatedTable]
``` 
 
## <a name="next-steps"></a><span data-ttu-id="d2503-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2503-229">Next steps</span></span> 
<span data-ttu-id="d2503-230">toocreate çoğaltılmış tablo, bu deyimleri birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="d2503-230">toocreate a replicated table, use one of these statements:</span></span>

- [<span data-ttu-id="d2503-231">TABLOSU (Azure SQL Data Warehouse) oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2503-231">CREATE TABLE (Azure SQL Data Warehouse)</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-azure-sql-data-warehouse)
- [<span data-ttu-id="d2503-232">TABLE AS SELECT (Azure SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2503-232">CREATE TABLE AS SELECT (Azure SQL Data Warehouse</span></span>](https://docs.microsoft.com/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse)

<span data-ttu-id="d2503-233">Dağıtılmış tabloları genel bakış için bkz: [dağıtılmış tabloları](sql-data-warehouse-tables-distribute.md).</span><span class="sxs-lookup"><span data-stu-id="d2503-233">For an overview of distributed tables, see [distributed tables](sql-data-warehouse-tables-distribute.md).</span></span>



