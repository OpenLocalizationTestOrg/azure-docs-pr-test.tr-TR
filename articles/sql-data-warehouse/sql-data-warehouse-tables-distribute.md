---
title: "SQL veri ambarı tablolarda dağıtma | Microsoft Docs"
description: "Azure SQL Data Warehouse tablolarda dağıtma ile çalışmaya başlama."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: d0e12bf821a81826a20b8db84e76c48fa60ad9b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="85445-103">SQL veri ambarı tablolarda dağıtma</span><span class="sxs-lookup"><span data-stu-id="85445-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="85445-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="85445-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="85445-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="85445-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="85445-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="85445-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="85445-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="85445-107">[Index][Index]</span></span>
> * <span data-ttu-id="85445-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="85445-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="85445-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="85445-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="85445-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="85445-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="85445-111">SQL Veri Ambarı, yüksek düzeyde paralel işleme (MPP) ile dağıtılmış bir veritabanı sistemidir.</span><span class="sxs-lookup"><span data-stu-id="85445-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="85445-112">Birden fazla düğümde verileri ve işleme özelliğini bölerek, SQL Veri Ambarı tek bir sistemin sağlayabileceğinden çok büyük ölçeklenebilirlik sunabilir.</span><span class="sxs-lookup"><span data-stu-id="85445-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="85445-113">SQL veri ambarı içindeki verilerinizi dağıtmak nasıl karar verme en iyi performans elde için en önemli faktörler biridir.</span><span class="sxs-lookup"><span data-stu-id="85445-113">Deciding how to distribute your data within your SQL Data Warehouse is one of the most important factors to achieving optimal performance.</span></span>   <span data-ttu-id="85445-114">En iyi performans anahtarına veri taşıma en aza indirerek ve veri taşıma en aza indirmek için anahtarı doğru Dağıtım stratejisi sırayla seçme.</span><span class="sxs-lookup"><span data-stu-id="85445-114">The key to optimal performance is minimizing data movement and in turn the key to minimizing data movement is selecting the right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="85445-115">Veri taşıma anlama</span><span class="sxs-lookup"><span data-stu-id="85445-115">Understanding data movement</span></span>
<span data-ttu-id="85445-116">MPP sistemde, her tablodan veri birkaç temel veritabanları arasında bölünür.</span><span class="sxs-lookup"><span data-stu-id="85445-116">In an MPP system, the data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="85445-117">MPP sistemde en iyileştirilmiş sorgular yalnızca üzerinden diğer veritabanları arasındaki etkileşimi olmadan dağıtılmış veritabanlarını yürütmek için geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="85445-117">The most optimized queries on an MPP system can simply be passed through to execute on the individual distributed databases with no interaction between the other databases.</span></span>  <span data-ttu-id="85445-118">Örneğin, iki tablo, satış ve müşteriler içeren satış verilerini içeren bir veritabanına sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="85445-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="85445-119">Ayrı bir veritabanında, her bir müşteri koyma, satış ve müşteri katılma herhangi bir sorgu içinde her müşteri tablonuz satış tablonuz katılmak için gereken bir sorgu varsa ve müşteri sayıya hem satış hem de müşteri tabloları bölme çözülebilir Veritabanı diğer veritabanlarından olanağıyla ile.</span><span class="sxs-lookup"><span data-stu-id="85445-119">If you have a query that needs to join your sales table to your customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of the other databases.</span></span>  <span data-ttu-id="85445-120">Sipariş numarası ve müşteri verilerinizi müşteri numarasına göre satış verilerinizi bölünmüş, buna karşılık, ardından tüm verilen veritabanı karşılık gelen verilerin her müşteri için sahip olmaz ve bu nedenle, müşteri verileri için satış verilerinizi katılmak istiyorsanız, t yapılandırtmanız gerekir Müşterinizle diğer veritabanlarındaki her bir müşteri için verileri.</span><span class="sxs-lookup"><span data-stu-id="85445-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have the corresponding data for each customer and thus if you wanted to join your sales data to your customer data, you would need to get the data for each customer from the other databases.</span></span>  <span data-ttu-id="85445-121">Bu ikinci örnekte, iki tablo katılabilir satış verileri için müşteri verileri taşımak için gerçekleşmesini veri taşıma gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-121">In this second example, data movement would need to occur to move the customer data to the sales data, so that the two tables can be joined.</span></span>  

<span data-ttu-id="85445-122">Veri taşıma her zaman hatalı bir şey değilse, bazen bir sorgu çözmek gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="85445-122">Data movement isn't always a bad thing, sometimes it's necessary to solve a query.</span></span>  <span data-ttu-id="85445-123">Ancak bu ek adım önlenebilir doğal olarak sorgunuzu daha hızlı çalışır.</span><span class="sxs-lookup"><span data-stu-id="85445-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="85445-124">Veri taşıma en yaygın olarak tablolar birleştirilir veya toplamalar gerçekleştirilen ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="85445-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="85445-125">Her ikisi de, gerçekleştirmeniz gereken genellikle bir birleştirme gibi bir senaryo için en iyi duruma olabilir ancak bir toplama gibi diğer senaryo için çözmenize yardımcı olmak için veri taşıma hala gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-125">Often you need to do both, so while you may be able to optimize for one scenario, like a join, you still need data movement to help you solve for the other scenario, like an aggregation.</span></span>  <span data-ttu-id="85445-126">Eli daha az iş olduğu çıkışı çıkarılıyor.</span><span class="sxs-lookup"><span data-stu-id="85445-126">The trick is figuring out which is less work.</span></span>  <span data-ttu-id="85445-127">Çoğu durumda, büyük olgu tabloları genellikle birleştirilmiş bir sütunda dağıtma çoğu veri taşıma azaltma en etkili yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="85445-127">In most cases, distributing large fact tables on a commonly joined column is the most effective method for reducing the most data movement.</span></span>  <span data-ttu-id="85445-128">Veri birleştirme sütunlarda dağıtma, bir toplama söz konusu sütunlarda veri dağıtma daha veri taşıma azaltmak için daha yaygın bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="85445-128">Distributing data on join columns is a much more common method to reduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="85445-129">Dağıtım yöntemini seçin</span><span class="sxs-lookup"><span data-stu-id="85445-129">Select distribution method</span></span>
<span data-ttu-id="85445-130">Arka planda, SQL Data Warehouse verilerinizi 60 veritabanlarına böler.</span><span class="sxs-lookup"><span data-stu-id="85445-130">Behind the scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="85445-131">Her bağımsız veritabanı olarak adlandırılır bir **dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="85445-131">Each individual database is referred to as a **distribution**.</span></span>  <span data-ttu-id="85445-132">Veri her tabloya yüklendiğinde, SQL Data Warehouse verilerinizi 60 bu dağıtımlar arasında bölmek nasıl bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-132">When data is loaded into each table, SQL Data Warehouse has to know how to divide your data across these 60 distributions.</span></span>  

<span data-ttu-id="85445-133">Dağıtım yöntemi tablo düzeyinde tanımlanır ve şu anda iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="85445-133">The distribution method is defined at the table level and currently there are two choices:</span></span>

1. <span data-ttu-id="85445-134">**Hepsini bir kez** eşit ancak rastgele veri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="85445-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="85445-135">**Dağıtılmış karma** tek bir sütun değerlerinden karma göre verileri dağıtır</span><span class="sxs-lookup"><span data-stu-id="85445-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="85445-136">Bir veri dağıtım yöntemi olmayan tanımlarken varsayılan olarak, tablonuz kullanarak dağıtılacak **hepsini** dağıtım yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85445-136">By default, when you do not define a data distribution method, your table will be distributed using the **round robin** distribution method.</span></span>  <span data-ttu-id="85445-137">Bununla birlikte, uygulamanızda daha karmaşık hale geldikçe kullanarak düşünmek isteyebilirsiniz **dağıtılmış karma** hangi sırayla iyileştirir veri taşıma en aza indirmek için tabloları sorgu performansı.</span><span class="sxs-lookup"><span data-stu-id="85445-137">However, as you become more sophisticated in your implementation, you will want to consider using **hash distributed** tables to minimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="85445-138">Hepsini bir kez tabloları</span><span class="sxs-lookup"><span data-stu-id="85445-138">Round Robin Tables</span></span>
<span data-ttu-id="85445-139">Veri dağıtmanın hepsini bir kez yöntemi kullanarak çok nasıl, göründüğü değildir.</span><span class="sxs-lookup"><span data-stu-id="85445-139">Using the Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="85445-140">Verilerinizi yüklenen gibi her satır yalnızca ileri dağıtım noktasına gönderilir.</span><span class="sxs-lookup"><span data-stu-id="85445-140">As your data is loaded, each row is simply sent to the next distribution.</span></span>  <span data-ttu-id="85445-141">Veri dağıtmanın bu yöntem her zaman rastgele veriler çok eşit tüm dağıtımlar arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="85445-141">This method of distributing the data will always randomly distribute the data very evenly across all of the distributions.</span></span>  <span data-ttu-id="85445-142">Diğer bir deyişle, var. verilerinizi yerleştirir hepsini bir kez işlemi sırasında yapılan sıralama</span><span class="sxs-lookup"><span data-stu-id="85445-142">That is, there is no sorting done during the round robin process which places your data.</span></span>  <span data-ttu-id="85445-143">Hepsini bir kez dağıtım, bu nedenle rastgele bir karma bazen denir.</span><span class="sxs-lookup"><span data-stu-id="85445-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="85445-144">Hepsini dağıtılmış tablo ile veri anlamak için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="85445-144">With a round-robin distributed table there is no need to understand the data.</span></span>  <span data-ttu-id="85445-145">Bu nedenle, hepsini tabloları genellikle iyi yükleme hedefleri olun.</span><span class="sxs-lookup"><span data-stu-id="85445-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="85445-146">Hiçbir dağıtım yöntemi seçilirse, varsayılan olarak, hepsini bir kez dağıtım yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85445-146">By default, if no distribution method is chosen, the round robin distribution method will be used.</span></span>  <span data-ttu-id="85445-147">Ancak, sistem hangi dağıtım garanti edemez anlamına gelir sistem veri rastgele dağıtıldığından hepsini bir kez tablolar kullanmayı, durumdayken her satırın'dır.</span><span class="sxs-lookup"><span data-stu-id="85445-147">However, while round robin tables are easy to use, because data is randomly distributed across the system it means that the system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="85445-148">Sonuç olarak, sistem, bir sorgu çözebilmek için önce verilerinizi daha iyi düzenlemek için bir veri taşıma işlemini çağırmak bazen gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-148">As a result, the system sometimes needs to invoke a data movement operation to better organize your data before it can resolve a query.</span></span>  <span data-ttu-id="85445-149">Bu ek adım sorgularınızı yavaşlatabilir.</span><span class="sxs-lookup"><span data-stu-id="85445-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="85445-150">Aşağıdaki senaryolarda tablonuzun hepsini dağıtım kullanmayı dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="85445-150">Consider using Round Robin distribution for your table in the following scenarios:</span></span>

* <span data-ttu-id="85445-151">Basit bir başlangıç noktası olarak çalışmaya</span><span class="sxs-lookup"><span data-stu-id="85445-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="85445-152">Hiçbir belirgin katılma anahtarı ise</span><span class="sxs-lookup"><span data-stu-id="85445-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="85445-153">Karma tablo dağıtmak için iyi bir adaydır sütun değilse</span><span class="sxs-lookup"><span data-stu-id="85445-153">If there is not good candidate column for hash distributing the table</span></span>
* <span data-ttu-id="85445-154">Tablo diğer tablolarla ortak bir birleşim anahtar paylaşmaz varsa</span><span class="sxs-lookup"><span data-stu-id="85445-154">If the table does not share a common join key with other tables</span></span>
* <span data-ttu-id="85445-155">Join sorgu diğer birleşimlerde'den daha az önemli ise</span><span class="sxs-lookup"><span data-stu-id="85445-155">If the join is less significant than other joins in the query</span></span>
* <span data-ttu-id="85445-156">Tablo geçici bir hazırlama tablosunda olduğunda</span><span class="sxs-lookup"><span data-stu-id="85445-156">When the table is a temporary staging table</span></span>

<span data-ttu-id="85445-157">Bu örneklerin her ikisi de hepsini bir kez tablo oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="85445-157">Both of these examples will create a Round Robin Table:</span></span>

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> <span data-ttu-id="85445-158">Hepsini bir kez olsa da, DDL'de açık olan varsayılan tablo türü bir tablo düzeni amaçları başkalarına açık olmasını sağlamak en iyi yöntem olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="85445-158">While round robin is the default table type being explicit in your DDL is considered a best practice so that the intentions of your table layout are clear to others.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="85445-159">Dağıtılmış tabloları karma</span><span class="sxs-lookup"><span data-stu-id="85445-159">Hash Distributed Tables</span></span>
<span data-ttu-id="85445-160">Kullanarak bir **dağıtılmış karma** tablolarınızı dağıtmak için algoritma sorgu zamanında veri taşıma azaltarak pek çok senaryoyla performansı geliştirebilir.</span><span class="sxs-lookup"><span data-stu-id="85445-160">Using a **Hash distributed** algorithm to distribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="85445-161">Dağıtılmış karma, seçtiğiniz tek bir sütun üzerinde bir karma algoritması kullanılarak dağıtılan veritabanları arasında bölünmüş tabloların tablolardır.</span><span class="sxs-lookup"><span data-stu-id="85445-161">Hash distributed tables are tables which are divided between the distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="85445-162">Dağıtım ne veriler dağıtılan veritabanları arasında nasıl bölünür belirler bir sütundur.</span><span class="sxs-lookup"><span data-stu-id="85445-162">The distribution column is what determines how the data is divided across your distributed databases.</span></span>  <span data-ttu-id="85445-163">Karma işlevi dağıtım sütun dağıtımları için satır atamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="85445-163">The hash function uses the distribution column to assign rows to distributions.</span></span>  <span data-ttu-id="85445-164">Karma algoritması ve sonuçta elde edilen dağıtım belirleyici.</span><span class="sxs-lookup"><span data-stu-id="85445-164">The hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="85445-165">Aynı veri türüne sahip aynı değer her zaman aynı dağıtım noktasına sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="85445-165">That is the same value with the same data type will always has to the same distribution.</span></span>    

<span data-ttu-id="85445-166">Bu örnek kimliği, dağıtılmış bir tablo oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="85445-166">This example will create a table distributed on id:</span></span>

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a><span data-ttu-id="85445-167">Dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="85445-167">Select distribution column</span></span>
<span data-ttu-id="85445-168">Seçtiğinizde **karma dağıtmak** bir tablo tek dağıtım sütun seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-168">When you choose to **hash distribute** a table, you will need to select a single distribution column.</span></span>  <span data-ttu-id="85445-169">Bir dağıtım sütun seçerken, dikkate alınması gereken üç temel Etkenler vardır.</span><span class="sxs-lookup"><span data-stu-id="85445-169">When selecting a distribution column, there are three major factors to consider.</span></span>  

<span data-ttu-id="85445-170">Olur, tek bir sütun seçin:</span><span class="sxs-lookup"><span data-stu-id="85445-170">Select a single column which will:</span></span>

1. <span data-ttu-id="85445-171">Güncelleştirilmemiş</span><span class="sxs-lookup"><span data-stu-id="85445-171">Not be updated</span></span>
2. <span data-ttu-id="85445-172">Veri eşit, veri eğme önleme Dağıt</span><span class="sxs-lookup"><span data-stu-id="85445-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="85445-173">Veri taşıma simge durumuna küçült</span><span class="sxs-lookup"><span data-stu-id="85445-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="85445-174">Güncelleştirilmez dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="85445-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="85445-175">Dağıtım sütunları bu nedenle güncelleştirilebilir, değildir, statik değerleri içeren bir sütun seçin.</span><span class="sxs-lookup"><span data-stu-id="85445-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="85445-176">Bir sütun güncelleştirilmesi gerekiyorsa, genelde iyi dağıtım aday değildir.</span><span class="sxs-lookup"><span data-stu-id="85445-176">If a column will need to be updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="85445-177">Bir dağıtım sütun güncelleştirme söz konusu ise, bu ilk satırın silinmesi ve yeni satır ekleme yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="85445-177">If there is a case where you must update a distribution column, this can be done by first deleting the row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="85445-178">Veri eşit olarak dağıtmanızı dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="85445-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="85445-179">Dağıtılmış bir sistemde yalnızca olabildiğince hızlı şekilde kendi yavaş dağıtım gerçekleştirir, iş dengeli yürütme sistem üzerindeki elde etmek için dağıtımlar arasında eşit olarak bölmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="85445-179">Since a distributed system performs only as fast as its slowest distribution, it is important to divide the work evenly across the distributions in order to achieve balanced execution across the system.</span></span>  <span data-ttu-id="85445-180">Dağıtılmış bir sistemde iş bölünmüş şekilde, burada her dağıtım için veri yaşamaktadır temel alır.</span><span class="sxs-lookup"><span data-stu-id="85445-180">The way the work is divided on a distributed system is based on where the data for each distribution lives.</span></span>  <span data-ttu-id="85445-181">Bu, böylece her dağıtım eşit bir iş ve kendi iş kısmını tamamlamak için aynı anda sürer verileri dağıtmak için doğru dağıtım sütun seçmek çok önemli kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="85445-181">This makes it very important to select the right distribution column for distributing the data so that each distribution has equal work and will take the same time to complete its portion of the work.</span></span>  <span data-ttu-id="85445-182">İş iyi sistem üzerindeki ayrıldığında, verileri dağıtımlar arasında dengelenir.</span><span class="sxs-lookup"><span data-stu-id="85445-182">When work is well divided across the system, the data is balanced across the distributions.</span></span>  <span data-ttu-id="85445-183">Veri eşit dengeli değil, bu diyoruz **veri eğme**.</span><span class="sxs-lookup"><span data-stu-id="85445-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="85445-184">Veri eşit ayırın ve verileri eğme önlemek için dağıtım sütun seçerken aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="85445-184">To divide data evenly and avoid data skew, consider the following when selecting your distribution column:</span></span>

1. <span data-ttu-id="85445-185">Çok sayıda farklı değerleri içeren bir sütun seçin.</span><span class="sxs-lookup"><span data-stu-id="85445-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="85445-186">Veri birkaç farklı değerleri olan sütunlarda dağıtma kaçının.</span><span class="sxs-lookup"><span data-stu-id="85445-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="85445-187">Null değerlere yüksek sıklığını sahip sütunlarda veri dağıtma kaçının.</span><span class="sxs-lookup"><span data-stu-id="85445-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="85445-188">Veri tarih sütunlarda dağıtma kaçının.</span><span class="sxs-lookup"><span data-stu-id="85445-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="85445-189">Her değer 60 dağıtımları 1 için karma olduğundan, hatta dağıtım elde etmek için yüksek oranda benzersiz olan ve birden fazla 60 benzersiz değerler içeren bir sütun seçmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="85445-189">Since each value is hashed to 1 of 60 distributions, to achieve even distribution you will want to select a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="85445-190">Göstermek için bir sütun yalnızca 40 benzersiz değerlere sahip olduğu bir durumu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="85445-190">To illustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="85445-191">Bu sütun dağıtım anahtarı olarak seçtiyseniz, bu tablo için veri üzerinde 40 dağıtımları en fazla 20 dağıtımları hiçbir veri ve hiçbir işlem yapmak için bırakarak güden.</span><span class="sxs-lookup"><span data-stu-id="85445-191">If this column was selected as the distribution key, the data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing to do.</span></span>  <span data-ttu-id="85445-192">Buna karşılık, diğer 40 dağıtımları verileri, eşit 60 dağıtımları yayılan, bunu yapmak için daha fazla iş gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-192">Conversely, the other 40 distributions would have more work to do that if the data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="85445-193">Bu senaryoda, veri eğme örneğidir.</span><span class="sxs-lookup"><span data-stu-id="85445-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="85445-194">MPP sistemdeki her sorgu adım için tüm dağıtımları kendi paylaşımı iş tamamlamak bekler.</span><span class="sxs-lookup"><span data-stu-id="85445-194">In MPP system, each query step waits for all distributions to complete their share of the work.</span></span>  <span data-ttu-id="85445-195">Bir dağıtım diğerlerinden daha fazla iş yapıyor, ardından diğer dağıtımlar kaynak temelde küçülttüğü iyi bir şekilde yalnızca meşgul dağıtım bekleniyor.</span><span class="sxs-lookup"><span data-stu-id="85445-195">If one distribution is doing more work than the others, then the resource of the other distributions are essentially wasted just waiting on the busy distribution.</span></span>  <span data-ttu-id="85445-196">İş eşit tüm dağıtımlar arasında yayılır değil, bu diyoruz **işleme eğme**.</span><span class="sxs-lookup"><span data-stu-id="85445-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="85445-197">İşleme eğme sorgu iş yükü dağıtımlar arasında eşit olarak yayılabilen varsa daha yavaş çalışmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="85445-197">Processing skew will cause queries to run slower than if the workload can be evenly spread across the distributions.</span></span>  <span data-ttu-id="85445-198">Veri eğme işleme eğme götürür.</span><span class="sxs-lookup"><span data-stu-id="85445-198">Data skew will lead to processing skew.</span></span>

<span data-ttu-id="85445-199">Null değerler tüm aynı dağıtım gideceksiniz gibi yüksek oranda boş değer atanabilir sütun dağıtma kaçının.</span><span class="sxs-lookup"><span data-stu-id="85445-199">Avoid distributing on highly nullable column as the null values will all land on the same distribution.</span></span> <span data-ttu-id="85445-200">Tüm veriler belirli bir tarih için aynı dağıtım gideceksiniz çünkü bir tarih sütunu dağıtma işleme eğme da neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="85445-200">Distributing on a date column can also cause processing skew because all data for a given date will land on the same distribution.</span></span> <span data-ttu-id="85445-201">Birkaç kullanıcı sorguları yürütme tüm filtreleme aynı tarihte 60 dağıtımları yalnızca 1 tüm belirli bir tarihten bu yana iş istediğimizi sonra yalnızca bir dağıtım noktasında olur.</span><span class="sxs-lookup"><span data-stu-id="85445-201">If several users are executing queries all filtering on the same date, then only 1 of the 60 distributions will be doing all of the work since a given date will only be on one distribution.</span></span> <span data-ttu-id="85445-202">Bu senaryoda, sorguları büyük olasılıkla 60 kez veri eşit tüm dağıtımları yayılan, daha yavaş çalışır.</span><span class="sxs-lookup"><span data-stu-id="85445-202">In this scenario, the queries will likely run 60 times slower than if the data were equally spread over all of the distributions.</span></span>

<span data-ttu-id="85445-203">İyi bir adaydır sütun mevcut olduğunda dağıtım yöntemi olarak hepsini kullanarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="85445-203">When no good candidate columns exist, then consider using round robin as the distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="85445-204">Veri taşıma en aza indirecek dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="85445-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="85445-205">Veri taşıma doğru dağıtım sütun seçerek en aza SQL veri ambarı performansını iyileştirmek için en önemli stratejileri biridir.</span><span class="sxs-lookup"><span data-stu-id="85445-205">Minimizing data movement by selecting the right distribution column is one of the most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="85445-206">Veri taşıma en yaygın olarak tablolar birleştirilir veya toplamalar gerçekleştirilen ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="85445-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="85445-207">Kullanılan sütunlar `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` ve `HAVING` tüm hale getirmek için yan tümceleri **iyi** dağıtım adayları karma.</span><span class="sxs-lookup"><span data-stu-id="85445-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="85445-208">Diğer yandan, sütunlarında `WHERE` yan tümcesi **değil** hangi dağıtımları işleme neden sorguda katılmak sınırlamak için iyi bir karma sütun adayları eğme olun.</span><span class="sxs-lookup"><span data-stu-id="85445-208">On the other hand, columns in the `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in the query, causing processing skew.</span></span>  <span data-ttu-id="85445-209">İyi üzerinde dağıtmak için tempting olabilir, ancak bu işleme eğme genellikle neden olabilir bir sütunun bir tarih sütunu bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="85445-209">A good example of a column which might be tempting to distribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="85445-210">Genel olarak bakıldığında, bir birleştirme sık söz konusu iki büyük olgu tabloları varsa, her iki tabloyu birleştirme sütunları birinde dağıtarak çoğu performans elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="85445-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain the most performance by distributing both tables on one of the join columns.</span></span>  <span data-ttu-id="85445-211">Hiçbir zaman başka bir büyük olgu tablosu için birleştirilmiş bir tablo varsa, sık içinde sütunları Ara `GROUP BY` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="85445-211">If you have a table that is never joined to another large fact table, then look to columns that are frequently in the `GROUP BY` clause.</span></span>

<span data-ttu-id="85445-212">Veri taşıma sırasında bir birleştirme önlemek için karşılanması gereken birkaç anahtar ölçütleri vardır:</span><span class="sxs-lookup"><span data-stu-id="85445-212">There are a few key criteria which must be met to avoid data movement during a join:</span></span>

1. <span data-ttu-id="85445-213">Birleştirme söz konusu tablolar üzerinde dağıtılmış karma olmalıdır **bir** birleşimde yer alan sütun.</span><span class="sxs-lookup"><span data-stu-id="85445-213">The tables involved in the join must be hash distributed on **one** of the columns participating in the join.</span></span>
2. <span data-ttu-id="85445-214">Birleşim sütunların veri türlerini iki tablo arasında eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="85445-214">The data types of the join columns must match between both tables.</span></span>
3. <span data-ttu-id="85445-215">Sütunları olan bir eşittir işleci katılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-215">The columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="85445-216">Birleşim türü olamaz bir `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="85445-216">The join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="85445-217">Veri eğme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="85445-217">Troubleshooting data skew</span></span>
<span data-ttu-id="85445-218">Tablo verisi karma dağıtım yöntemi kullanılarak dağıtıldığında diğerlerinden orantısız daha fazla veri sağlamak için bazı dağıtımları eğri şansı yoktur.</span><span class="sxs-lookup"><span data-stu-id="85445-218">When table data is distributed using the hash distribution method there is a chance that some distributions will be skewed to have disproportionately more data than others.</span></span> <span data-ttu-id="85445-219">Bir dağıtılmış sorgu sonucunu uzun süre çalışan dağıtım için beklemeniz gerekir çünkü aşırı miktarda verinin eğme sorgu performansını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="85445-219">Excessive data skew can impact query performance because the final result of a distributed query must wait for the longest running distribution to finish.</span></span> <span data-ttu-id="85445-220">Veri eğme derecesini bağlı olarak ele gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="85445-220">Depending on the degree of the data skew you might need to address it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="85445-221">Eğme tanımlama</span><span class="sxs-lookup"><span data-stu-id="85445-221">Identifying skew</span></span>
<span data-ttu-id="85445-222">Eğri bir tablo tanımlamak için basit bir yol kullanmaktır `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="85445-222">A simple way to identify a table as skewed is to use `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="85445-223">Her 60 dağıtımları veritabanınızın depolanan tablo satır sayısını görmek için çok hızlı ve kolay bir yolu budur.</span><span class="sxs-lookup"><span data-stu-id="85445-223">This is a very quick and simple way to see the number of table rows that are stored in each of the 60 distributions of your database.</span></span>  <span data-ttu-id="85445-224">En dengeli performans için unutmayın, dağıtılmış, tablosundaki satırları tüm dağıtımları eşit yayılan.</span><span class="sxs-lookup"><span data-stu-id="85445-224">Remember that for the most balanced performance, the rows in your distributed table should be spread evenly across all the distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="85445-225">Ancak, Azure SQL Data Warehouse dinamik yönetim görünümlerini (DMV) sorgu varsa daha ayrıntılı bir analiz gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="85445-225">However, if you query the Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="85445-226">Başlatmak için Görünüm oluşturma [dbo.vTableSizes] [ dbo.vTableSizes] SQL kullanarak görüntülemek [tablo genel bakışı] [ Overview] makalesi.</span><span class="sxs-lookup"><span data-stu-id="85445-226">To start, create the view [dbo.vTableSizes][dbo.vTableSizes] view using the SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="85445-227">Görünüm oluşturulduğunda, en fazla % 10 veri eğme hangi tabloları tanımlamak için bu sorguyu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="85445-227">Once the view is created, run this query to identify which tables have more than 10% data skew.</span></span>

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a><span data-ttu-id="85445-228">Veri eğme çözme</span><span class="sxs-lookup"><span data-stu-id="85445-228">Resolving data skew</span></span>
<span data-ttu-id="85445-229">Bir düzeltme garanti etmeye yetecek tüm eğme değil.</span><span class="sxs-lookup"><span data-stu-id="85445-229">Not all skew is enough to warrant a fix.</span></span>  <span data-ttu-id="85445-230">Bazı durumlarda, bazı sorgular tabloda performans verileri eğme zarar daha ağır basar.</span><span class="sxs-lookup"><span data-stu-id="85445-230">In some cases, the performance of a table in some queries can outweigh the harm of data skew.</span></span>  <span data-ttu-id="85445-231">Veri çözümlenmelidir varsa karar vermek için bir tabloda eğme, sorgular ve veri birimleri hakkında mümkün olduğunca, iş yükü anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="85445-231">To decide if you should resolve data skew in a table, you should understand as much as possible about the data volumes and queries in your workload.</span></span>   <span data-ttu-id="85445-232">Eğme etkisini bakmak için bir yoldur adımlarda kullanmak üzere [sorgu izleme] [ Query Monitoring] eğme sorgu performansı üzerindeki etkisini ve özellikle nasıl etkisini uzun izlemek için makale sorgular tamamlanması Al tek tek dağıtımları.</span><span class="sxs-lookup"><span data-stu-id="85445-232">One way to look at the impact of skew is to use the steps in the [Query Monitoring][Query Monitoring] article to monitor the impact of skew on query performance and specifically the impact to how long queries take to complete on the individual distributions.</span></span>

<span data-ttu-id="85445-233">Veri dağıtma veri eğme en aza indirerek ve veri taşıma en aza arasında doğru dengeyi bulma bir konudur.</span><span class="sxs-lookup"><span data-stu-id="85445-233">Distributing data is a matter of finding the right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="85445-234">Bu hedefleri karşıt ve bazen veri veri taşıma azaltmak için eğme tutmak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="85445-234">These can be opposing goals, and sometimes you will want to keep data skew in order to reduce data movement.</span></span> <span data-ttu-id="85445-235">Dağıtım sütun sık birleşimler ve toplamalar paylaşılan sütunu olduğunda, örneğin, veri taşıma en aza indirme.</span><span class="sxs-lookup"><span data-stu-id="85445-235">For example, when the distribution column is frequently the shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="85445-236">En düşük düzeyde veri hareketini sahip yararı eğme verilere sahip olmak etkisini üstün olabilir.</span><span class="sxs-lookup"><span data-stu-id="85445-236">The benefit of having the minimal data movement might outweigh the impact of having data skew.</span></span>

<span data-ttu-id="85445-237">Veri eğme çözümlemek için tipik tablonun farklı dağıtım sütunu yeniden oluşturmanız yoludur.</span><span class="sxs-lookup"><span data-stu-id="85445-237">The typical way to resolve data skew is to re-create the table with a different distribution column.</span></span> <span data-ttu-id="85445-238">Varolan bir tabloda, bir tablo dağıtımını değiştirmek için yol dağıtım sütunu değiştirmek mümkün olduğundan yeniden oluşturmak için [CTAS] [] ile.</span><span class="sxs-lookup"><span data-stu-id="85445-238">Since there is no way to change the distribution column on an existing table, the way to change the distribution of a table it to recreate it with a [CTAS][].</span></span>  <span data-ttu-id="85445-239">İşte nasıl iki örnek veri eğme çözün:</span><span class="sxs-lookup"><span data-stu-id="85445-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-the-table-with-a-new-distribution-column"></a><span data-ttu-id="85445-240">Örnek 1: yeni bir dağıtım sütun içeren tabloyu yeniden oluşturun</span><span class="sxs-lookup"><span data-stu-id="85445-240">Example 1: Re-create the table with a new distribution column</span></span>
<span data-ttu-id="85445-241">Bu örnekte, farklı bir karma dağıtım sütunlu bir tablo yeniden oluşturmak için [CTAS] [] kullanır.</span><span class="sxs-lookup"><span data-stu-id="85445-241">This example uses [CTAS][] to re-create a table with a different hash distribution column.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] TO [FactInternetSales];
```

### <a name="example-2-re-create-the-table-using-round-robin-distribution"></a><span data-ttu-id="85445-242">Örnek 2: hepsini dağıtım kullanarak tabloyu yeniden oluşturun</span><span class="sxs-lookup"><span data-stu-id="85445-242">Example 2: Re-create the table using round robin distribution</span></span>
<span data-ttu-id="85445-243">Bu örnek [CTAS] [] hepsini bir karma dağıtım yerine içeren bir tablo yeniden oluşturmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="85445-243">This example uses [CTAS][] to re-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="85445-244">Bu değişiklik bile artan veri taşıma, veri dağıtımı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85445-244">This change will produce even data distribution at the cost of increased data movement.</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename the tables
RENAME OBJECT [dbo].[FactInternetSales] TO [FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] TO [FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="85445-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85445-245">Next steps</span></span>
<span data-ttu-id="85445-246">Tablo tasarımı hakkında daha fazla bilgi için bkz: [Dağıt][Distribute], [dizin][Index], [bölüm] [ Partition], [Veri türleri][Data Types], [istatistikleri] [ Statistics] ve [geçici tablolar] [ Temporary] makaleleri.</span><span class="sxs-lookup"><span data-stu-id="85445-246">To learn more about table design, see the [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="85445-247">En iyi yöntemler genel bakış için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="85445-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
