---
title: "SQL veri ambarı aaaDistributing tablolarda | Microsoft Docs"
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
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="b8a7c-103">SQL veri ambarı tablolarda dağıtma</span><span class="sxs-lookup"><span data-stu-id="b8a7c-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="b8a7c-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="b8a7c-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="b8a7c-105">[Veri türleri][Data Types]</span><span class="sxs-lookup"><span data-stu-id="b8a7c-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="b8a7c-106">[Dağıt][Distribute]</span><span class="sxs-lookup"><span data-stu-id="b8a7c-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="b8a7c-107">[Dizin][Index]</span><span class="sxs-lookup"><span data-stu-id="b8a7c-107">[Index][Index]</span></span>
> * <span data-ttu-id="b8a7c-108">[Bölüm][Partition]</span><span class="sxs-lookup"><span data-stu-id="b8a7c-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="b8a7c-109">[İstatistikleri][Statistics]</span><span class="sxs-lookup"><span data-stu-id="b8a7c-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="b8a7c-110">[Geçici][Temporary]</span><span class="sxs-lookup"><span data-stu-id="b8a7c-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="b8a7c-111">SQL Veri Ambarı, yüksek düzeyde paralel işleme (MPP) ile dağıtılmış bir veritabanı sistemidir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="b8a7c-112">Birden fazla düğümde verileri ve işleme özelliğini bölerek, SQL Veri Ambarı tek bir sistemin sağlayabileceğinden çok büyük ölçeklenebilirlik sunabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="b8a7c-113">Toodistribute verilerinizi SQL veri ambarı içinde ne olduğuna karar vermeyle hello en önemli birini Etkenler tooachieving en iyi performans.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="b8a7c-114">Veri taşıma Hello anahtar toooptimal performans en aza indirerek ve hello anahtar toominimizing veri taşıma hello doğru Dağıtım stratejisi sırayla seçme.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="b8a7c-115">Veri taşıma anlama</span><span class="sxs-lookup"><span data-stu-id="b8a7c-115">Understanding data movement</span></span>
<span data-ttu-id="b8a7c-116">Bir MPP sisteminde hello veriler her tablodan birkaç temel veritabanları arasında bölünür.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="b8a7c-117">en iyileştirilmiş hello sorguları bir MPP sistemde yalnızca geçirilebilir tooexecute üzerinde hello etkileşimi olmadan tek tek dağıtılan veritabanları arasında diğer veritabanlarına hello.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="b8a7c-118">Örneğin, iki tablo, satış ve müşteriler içeren satış verilerini içeren bir veritabanına sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="b8a7c-119">Satış tooyour müşteri tablo toojoin gerektiren bir sorgu varsa ve hem satış hem de müşteri tabloları müşteri numarası tarafından ayrı bir veritabanında her müşteri koyma bölme, satış ve müşteri birleştiren herhangi bir sorgu her içinde çözülebilir hiçbir bilgisine sahip veritabanı diğer veritabanlarından hello.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="b8a7c-120">Sipariş numarası ve müşteri verilerinizi müşteri numarasına göre satış verilerinizi bölünmüş, buna karşılık, ardından tüm verilen veritabanı hello karşılık gelen verilerin her müşteri için sahip olmaz ve bu nedenle, satış verileri tooyour müşteri verilerinizi toojoin istediyseniz, gerekir tooget hello veri hello gelen her bir müşteri için diğer veritabanları.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="b8a7c-121">Böylece Hello iki tabloları katılabilir bu ikinci örnekte toooccur toomove hello müşteri veri toohello satış verileri, veri taşıma gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="b8a7c-122">Veri taşıma her zaman hatalı bir şey değilse, bazen gerekli toosolve bir sorgu olabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="b8a7c-123">Ancak bu ek adım önlenebilir doğal olarak sorgunuzu daha hızlı çalışır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="b8a7c-124">Veri taşıma en yaygın olarak tablolar birleştirilir veya toplamalar gerçekleştirilen ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="b8a7c-125">Genellikle mümkün olabilir ancak bir birleştirme, siz hala gibi bir senaryoya ihtiyaç için veri taşıma toohelp için çözmek toooptimize hello için bir toplama gibi diğer senaryo toodo ikisini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="b8a7c-126">Merhaba eli daha az iş olduğu çıkışı çıkarılıyor.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="b8a7c-127">Çoğu durumda, büyük olgu tabloları genellikle birleştirilmiş bir sütunda dağıtma olduğu hello hello azaltma en etkili yöntemi çoğu veri taşıma.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="b8a7c-128">Verileri birleştirme sütunlarda dağıtma veri bir toplama söz konusu sütunlarda dağıtma daha bir çok daha yaygın yöntemi tooreduce veri hareketi olur.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="b8a7c-129">Dağıtım yöntemini seçin</span><span class="sxs-lookup"><span data-stu-id="b8a7c-129">Select distribution method</span></span>
<span data-ttu-id="b8a7c-130">Merhaba arka planda, SQL Data Warehouse verilerinizi 60 veritabanlarına böler.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="b8a7c-131">Başvurulan tooas tek tek her veritabanı olan bir **dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="b8a7c-132">Veri her tabloya yüklendiğinde, SQL Data Warehouse tooknow nasıl sahip toodivide verilerinizi 60 bu dağıtımlar arasında.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="b8a7c-133">Merhaba dağıtım yöntemini hello tablo düzeyinde tanımlanır ve şu anda iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="b8a7c-134">**Hepsini bir kez** eşit ancak rastgele veri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="b8a7c-135">**Dağıtılmış karma** tek bir sütun değerlerinden karma göre verileri dağıtır</span><span class="sxs-lookup"><span data-stu-id="b8a7c-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="b8a7c-136">Bir veri dağıtım yöntemi olmayan tanımlarken varsayılan olarak, tablonuz hello kullanarak dağıtılacak **hepsini** dağıtım yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="b8a7c-137">Uygulamanızda daha karmaşık hale geldikçe ancak tooconsider kullanarak istediğiniz **dağıtılmış karma** tabloları sırayla sorgu performansı en iyi duruma getirir, toominimize veri taşıma.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="b8a7c-138">Hepsini bir kez tabloları</span><span class="sxs-lookup"><span data-stu-id="b8a7c-138">Round Robin Tables</span></span>
<span data-ttu-id="b8a7c-139">Merhaba veri dağıtmanın hepsini bir kez yöntemi kullanarak çok nasıl, göründüğü değildir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="b8a7c-140">Verilerinizi yüklenen gibi her satır yalnızca toohello sonraki dağıtım gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="b8a7c-141">Merhaba veri dağıtmanın bu yöntem her zaman rastgele hello veri çok eşit tüm hello dağıtımlar arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="b8a7c-142">Diğer bir deyişle, var. sıralama Bitti'yi verilerinizi koyan bir kez deneme işlemi round hello sırasında</span><span class="sxs-lookup"><span data-stu-id="b8a7c-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="b8a7c-143">Hepsini bir kez dağıtım, bu nedenle rastgele bir karma bazen denir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="b8a7c-144">Hepsini dağıtılmış tabloyla gerek toounderstand hello verisi yok.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="b8a7c-145">Bu nedenle, hepsini tabloları genellikle iyi yükleme hedefleri olun.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="b8a7c-146">Hiçbir dağıtım yöntemi seçilirse, varsayılan olarak, hello hepsini dağıtım yöntemi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="b8a7c-147">Ancak, veri rastgele hello sistem hangi dağıtım garanti edemez anlamına gelir hello sistem dağıtıldığı hepsini bir kez tabloları kolay toouse durumdayken her satırın'dır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="b8a7c-148">Sonuç, bazen hello sistem tooinvoke veri taşıma işlemi toobetter gerektiği bir sorgu çözebilmek için önce verilerinizi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="b8a7c-149">Bu ek adım sorgularınızı yavaşlatabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="b8a7c-150">Hepsini bir kez dağıtım senaryoları aşağıdaki hello tablonuzda için kullanmayı dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="b8a7c-151">Basit bir başlangıç noktası olarak çalışmaya</span><span class="sxs-lookup"><span data-stu-id="b8a7c-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="b8a7c-152">Hiçbir belirgin katılma anahtarı ise</span><span class="sxs-lookup"><span data-stu-id="b8a7c-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="b8a7c-153">Karma hello tablo dağıtmak için iyi bir adaydır sütun değilse</span><span class="sxs-lookup"><span data-stu-id="b8a7c-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="b8a7c-154">Merhaba, tablo ortak bir birleşim anahtar diğer tablolarla paylaşmaz</span><span class="sxs-lookup"><span data-stu-id="b8a7c-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="b8a7c-155">Merhaba birleştirme hello sorgu diğer birleşimlerde'den daha az önemli ise</span><span class="sxs-lookup"><span data-stu-id="b8a7c-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="b8a7c-156">Merhaba tablo geçici bir hazırlama tablosunda olduğunda</span><span class="sxs-lookup"><span data-stu-id="b8a7c-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="b8a7c-157">Bu örneklerin her ikisi de hepsini bir kez tablo oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="b8a7c-158">Hepsini bir kez olsa hello varsayılan tablo türü, DDL'de açık olan bir tablo düzeni hello amaçları Temizle tooothers; böylece en iyi yöntem olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="b8a7c-159">Dağıtılmış tabloları karma</span><span class="sxs-lookup"><span data-stu-id="b8a7c-159">Hash Distributed Tables</span></span>
<span data-ttu-id="b8a7c-160">Kullanarak bir **dağıtılmış karma** algoritması toodistribute tablolarınızı birçok senaryoları için sorgu zamanında veri taşıma azaltarak performansı artırabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="b8a7c-161">Dağıtılmış tablolar arasında hello bölünen tablolardır karma seçtiğiniz tek bir sütun üzerinde bir karma algoritması kullanarak veritabanlarını dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="b8a7c-162">Merhaba dağıtım ne hello veriler dağıtılan veritabanları arasında nasıl bölünür belirler bir sütundur.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="b8a7c-163">Merhaba karma işlevi hello dağıtım sütun tooassign satırları toodistributions kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="b8a7c-164">karma algoritma hello ve sonuçta elde edilen dağıtım belirleyici.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="b8a7c-165">Diğer bir deyişle hello aynı veri türünde olacak her zaman hello ile aynı değere sahip toohello aynı dağıtım.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="b8a7c-166">Bu örnek kimliği, dağıtılmış bir tablo oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="b8a7c-167">Dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="b8a7c-167">Select distribution column</span></span>
<span data-ttu-id="b8a7c-168">Çok seçtiğinizde**karma dağıtmak** bir tablo tooselect tek dağıtım sütun gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="b8a7c-169">Bir dağıtım sütun seçerken, üç ana Etkenler tooconsider vardır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="b8a7c-170">Olur, tek bir sütun seçin:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-170">Select a single column which will:</span></span>

1. <span data-ttu-id="b8a7c-171">Güncelleştirilmemiş</span><span class="sxs-lookup"><span data-stu-id="b8a7c-171">Not be updated</span></span>
2. <span data-ttu-id="b8a7c-172">Veri eşit, veri eğme önleme Dağıt</span><span class="sxs-lookup"><span data-stu-id="b8a7c-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="b8a7c-173">Veri taşıma simge durumuna küçült</span><span class="sxs-lookup"><span data-stu-id="b8a7c-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="b8a7c-174">Güncelleştirilmez dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="b8a7c-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="b8a7c-175">Dağıtım sütunları bu nedenle güncelleştirilebilir, değildir, statik değerleri içeren bir sütun seçin.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="b8a7c-176">Bir sütun güncelleştirilmiş toobe gerekecekse, genellikle iyi dağıtım aday değil.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="b8a7c-177">Bir dağıtım sütun güncelleştirme söz konusu ise, bu ilk hello satırın silinmesi ve yeni satır ekleme yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="b8a7c-178">Veri eşit olarak dağıtmanızı dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="b8a7c-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="b8a7c-179">Dağıtılmış bir sistemde yalnızca olabildiğince hızlı şekilde kendi yavaş dağıtım gerçekleştirir olduğundan, bu önemli toodivide hello iş eşit sipariş dengeli tooachieve yürütmesinde hello dağıtımlar arasında hello arasında sistemidir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="b8a7c-180">Hello iş dağıtılmış bir sistemde ayrılmıştır hello yolu, her dağıtım için hello veri nerede yaşıyor temel alır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="b8a7c-181">Bu, böylece her dağıtım eşit iş sahiptir ve Al aynı zaman toocomplete hello iş kendi kısmı hello hello veri dağıtmak için çok önemli tooselect hello doğru dağıtım sütun kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="b8a7c-182">İş iyi hello sistem ayrıldığında, hello veri hello dağıtımlar arasında dengelenir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="b8a7c-183">Veri eşit dengeli değil, bu diyoruz **veri eğme**.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="b8a7c-184">toodivide veri eşit ve veri eğme kaçınmak için dağıtım sütun seçerken hello aşağıdakileri dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="b8a7c-185">Çok sayıda farklı değerleri içeren bir sütun seçin.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="b8a7c-186">Veri birkaç farklı değerleri olan sütunlarda dağıtma kaçının.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="b8a7c-187">Null değerlere yüksek sıklığını sahip sütunlarda veri dağıtma kaçının.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="b8a7c-188">Veri tarih sütunlarda dağıtma kaçının.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="b8a7c-189">Tooachieve bile dağıtım her değer 60 dağıtımları, karma too1 olduğundan, yüksek oranda benzersiz olan ve birden fazla 60 benzersiz değerler içeren bir sütun tooselect isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="b8a7c-190">tooillustrate, bir sütun yalnızca sahip olduğu 40 benzersiz değerler bir durum düşünün.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="b8a7c-191">Bu sütun hello dağıtım anahtarı olarak seçtiyseniz, bu tablo için hello veri üzerinde 40 dağıtımları en fazla 20 dağıtımları hiçbir veri ve hiçbir işlem toodo bırakarak güden.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="b8a7c-192">Buna karşılık, hello diğer 40 dağıtımları hello varsa veri eşit 60 dağıtımları yayılan, daha fazla iş toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="b8a7c-193">Bu senaryoda, veri eğme örneğidir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="b8a7c-194">MPP sistemdeki her sorgu adım için tüm dağıtımların toocomplete kendi paylaşımı hello iş bekler.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="b8a7c-195">Bir dağıtım başkalarının hello daha fazla çalışma yapılması olduğu sonra hello kaynak hello diğer dağıtımlar temelde yalnızca hello meşgul dağıtım noktasında bekleme küçülttüğü iyi bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="b8a7c-196">İş eşit tüm dağıtımlar arasında yayılır değil, bu diyoruz **işleme eğme**.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="b8a7c-197">İşleme eğme sorguları toorun hello iş yükü hello dağıtımlar arasında eşit olarak yayılabilen varsa daha yavaş neden olur.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="b8a7c-198">Veri eğme tooprocessing eğme götürür.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="b8a7c-199">Merhaba null değerler tüm hello üzerinde aynı gideceksiniz gibi yüksek oranda boş değer atanabilir sütun dağıtmaktan kaçınmak dağıtım.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="b8a7c-200">Bir tarih sütunu dağıtma de neden olabilir işleme eğme belirli bir tarih için tüm veriler üzerinde hello aynı gideceksiniz çünkü dağıtım.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="b8a7c-201">Birkaç kullanıcı sorguları tüm filtreleme hello üzerinde çalıştırıyorsanız belirli bir tarih yalnızca bir dağıtım noktasında olacağından yalnızca 1'hello 60 dağıtımları, tüm hello iş istediğimizi sonra aynı, tarih.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="b8a7c-202">Bu senaryoda, hello sorguları büyük olasılıkla 60 kez hello veri eşit tüm hello dağıtımları yayılan, daha yavaş çalışır.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="b8a7c-203">İyi bir adaydır sütun mevcut olduğunda hello dağıtım yöntemi olarak hepsini kullanarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="b8a7c-204">Veri taşıma en aza indirecek dağıtım sütun seçin</span><span class="sxs-lookup"><span data-stu-id="b8a7c-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="b8a7c-205">Veri taşıma hello doğru dağıtım sütun seçerek en aza SQL veri ambarı performansını iyileştirmek için en önemli stratejileri hello biridir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="b8a7c-206">Veri taşıma en yaygın olarak tablolar birleştirilir veya toplamalar gerçekleştirilen ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="b8a7c-207">Kullanılan sütunlar `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` ve `HAVING` tüm hale getirmek için yan tümceleri **iyi** dağıtım adayları karma.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="b8a7c-208">Üzerinde diğer yandan, hello sütunlarında hello `WHERE` yan tümcesi **değil** hangi dağıtımları işleme neden hello sorguda katılmak sınırlamak için iyi bir karma sütun adayları eğme olun.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="b8a7c-209">İyi tempting toodistribute olabilir, ancak bu işleme eğme genellikle neden olabilir bir sütunun bir tarih sütunu bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="b8a7c-210">Bir birleştirme sık söz konusu iki büyük olgu tabloları varsa, genel olarak bakıldığında, hello çoğu performans hello birleştirme sütunları her iki tablolarda dağıtarak elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="b8a7c-211">Hiçbir zaman birleştirilmiş tooanother büyük Olgu Tablosu olan bir tablo varsa, sık hello olan toocolumns Ara `GROUP BY` yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="b8a7c-212">Ölç tooavoid veri taşıma sırasında bir birleştirme olması gereken birkaç anahtar ölçütleri vardır:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="b8a7c-213">Merhaba hello birleştirme söz konusu tablolar üzerinde dağıtılmış karma olmalıdır **bir** hello birleştirme katılan hello sütunların.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="b8a7c-214">Merhaba birleştirme sütunların veri türlerini Hello her iki tablo arasında eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="b8a7c-215">Merhaba sütunları olan bir eşittir işleci katılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="b8a7c-216">Merhaba birleşim türü olamaz bir `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="b8a7c-217">Veri eğme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="b8a7c-217">Troubleshooting data skew</span></span>
<span data-ttu-id="b8a7c-218">Tablo verisi yok hello karma dağıtım yöntemini kullanarak dağıtıldığında bazı dağıtımları olacak şansı toohave diğerlerinden orantısız daha fazla veri eğri.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="b8a7c-219">Dağıtılmış bir sorguyla Hello sonucunu hello uzun çalışan dağıtım toofinish için beklemeniz gerekir çünkü aşırı miktarda verinin eğme sorgu performansını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="b8a7c-220">Merhaba veri tooaddress gerekebilecek eğme Hello derecesini, bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="b8a7c-221">Eğme tanımlama</span><span class="sxs-lookup"><span data-stu-id="b8a7c-221">Identifying skew</span></span>
<span data-ttu-id="b8a7c-222">Toouse basit yol tooidentify eğri gibi bir tablo olduğundan `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="b8a7c-223">Çok hızlı ve basit bir yol toosee budur hello her hello 60 dağıtımları veritabanınızın depolanır tablosu satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="b8a7c-224">En dengeli hello performans için Dağıtılmış tablonuz hello satır eşit tüm hello dağıtımlar arasında yayılan olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="b8a7c-225">Ancak, hello Azure SQL Data Warehouse dinamik yönetim görünümlerini (DMV) sorgu varsa daha ayrıntılı bir analiz gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="b8a7c-226">toostart, hello görünümü oluşturma [dbo.vTableSizes] [ dbo.vTableSizes] kullanarak görüntülemek SQL'den hello [tablo genel bakışı] [ Overview] makalesi.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="b8a7c-227">Merhaba görünüm oluşturulduktan sonra hangi tabloları % 10 veri eğme birden fazla sahip bu sorgu tooidentify çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="b8a7c-228">Veri eğme çözme</span><span class="sxs-lookup"><span data-stu-id="b8a7c-228">Resolving data skew</span></span>
<span data-ttu-id="b8a7c-229">Tüm eğme yeterli toowarrant bir düzeltme bulunur.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="b8a7c-230">Bazı durumlarda, bazı sorgular tabloda hello performansını hello zarar eğme verilerin daha ağır basar.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="b8a7c-231">Veri çözümlenmelidir varsa toodecide eğme bir tabloda, hello veri birimleri ve sorguları hakkında mümkün olduğunca, iş yükü anlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="b8a7c-232">Tek yönlü toolook eğme hello etkisini en olduğu toouse hello hello adımlarda [sorgu izleme] [ Query Monitoring] makale toomonitor hello etkisini sorgu performansı eğme ve özellikle etkisi toohow uzun sorguları hello toocomplete hello tek tek dağıtımları üzerinde gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="b8a7c-233">Veri dağıtma veri eğme en aza indirerek ve veri taşıma en aza arasında doğru dengeyi hello bulma bir konudur.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="b8a7c-234">Bu hedefleri karşıt ve bazen tookeep veri sırası tooreduce veri taşıma eğme isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="b8a7c-235">Merhaba dağıtım sütun sık birleşimler ve toplamalar paylaşılan sütununda hello olduğunda, örneğin, veri taşıma en aza indirme.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="b8a7c-236">Merhaba bir eğme verilere sahip olmak hello etkisi en hello en düşük düzeyde veri taşıma sahip olmanın avantajı üstün olabilir.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="b8a7c-237">Merhaba normal şekilde tooresolve veri eğme olan toore-farklı dağıtım sütunla hello tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="b8a7c-238">Olduğundan toochange hello dağıtım sütun üzerinde var olan tablo, hello yolu toochange hello dağıtımı bir tablonun hiçbir şekilde bunu toorecreate [CTAS] [] ile.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="b8a7c-239">İşte nasıl iki örnek veri eğme çözün:</span><span class="sxs-lookup"><span data-stu-id="b8a7c-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="b8a7c-240">Örnek 1: yeni bir dağıtım sütun ile Merhaba tabloyu yeniden oluşturun</span><span class="sxs-lookup"><span data-stu-id="b8a7c-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="b8a7c-241">Bu örnek [CTAS] [] toore kullanır-farklı bir karma dağıtım sütun bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="b8a7c-242">Örnek 2: hello tabloyu hepsini dağıtım kullanarak yeniden oluşturun</span><span class="sxs-lookup"><span data-stu-id="b8a7c-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="b8a7c-243">Bu örnek [CTAS] [] toore kullanır-hepsini bir karma dağıtım yerine bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="b8a7c-244">Bu değişiklik, hatta veri dağıtımını hello maliyetle artan veri taşıma oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a><span data-ttu-id="b8a7c-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b8a7c-245">Next steps</span></span>
<span data-ttu-id="b8a7c-246">Tablo tasarımı hakkında daha fazla toolearn bkz hello [Dağıt][Distribute], [dizin][Index], [bölüm] [ Partition], [Veri türleri][Data Types], [istatistikleri] [ Statistics] ve [geçici tablolar] [ Temporary] makaleleri.</span><span class="sxs-lookup"><span data-stu-id="b8a7c-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="b8a7c-247">En iyi yöntemler genel bakış için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="b8a7c-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
