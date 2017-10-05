---
title: "İşlemleri SQL Data Warehouse için en iyi duruma getirme | Microsoft Docs"
description: "Azure SQL Data Warehouse'da verimli işlem güncelleştirmeleri yazma en iyi uygulama kılavuzunu"
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 6f326f26-8a54-49df-a482-9c96a58db371
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: f9f19d75a37351b3562ce8c2f3629df14c5437c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="5ffe6-103">İşlemleri SQL Data Warehouse için en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="5ffe6-104">Bu makalede, uzun düzeyine riskini en aza indirme sırasında işlem kodunuzu performansını en iyi duruma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-104">This article explains how to optimize the performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="5ffe6-105">İşlemler ve günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-105">Transactions and logging</span></span>
<span data-ttu-id="5ffe6-106">İşlemler, ilişkisel veritabanı altyapısını önemli bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="5ffe6-107">SQL veri ambarı işlemleri sırasında veri değişikliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="5ffe6-108">Bu işlemler, açık veya örtülü olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="5ffe6-109">Tek `INSERT`, `UPDATE` ve `DELETE` deyimleri örtülü işlemler tüm örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="5ffe6-110">Açık işlemleri açıkça kullanarak bir geliştirici tarafından yazılan `BEGIN TRAN`, `COMMIT TRAN` veya `ROLLBACK TRAN` ve birden çok değişikliği deyimleri tek bir atomik biriminde birlikte bağlanması gerektiğinde tipik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need to be tied together in a single atomic unit.</span></span> 

<span data-ttu-id="5ffe6-111">Azure SQL Data Warehouse, işlem günlükleri kullanarak veritabanı değişiklikleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-111">Azure SQL Data Warehouse commits changes to the database using transaction logs.</span></span> <span data-ttu-id="5ffe6-112">Her dağıtım kendi işlem günlüğü vardır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="5ffe6-113">İşlem günlüğü yazma otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="5ffe6-114">Gerekli yapılandırma yoktur.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-114">There is no configuration required.</span></span> <span data-ttu-id="5ffe6-115">Ancak, bu işlem yazma garanti adımında, bir ek yük sistemde tanıtır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-115">However, whilst this process guarantees the write it does introduce an overhead in the system.</span></span> <span data-ttu-id="5ffe6-116">İşlemsel olarak verimli kodlar yazarak bu etkiyi en aza indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="5ffe6-117">İşlemsel olarak verimli kod kapsamlı iki kategoride yer alır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="5ffe6-118">Mümkün olduğunda en az günlük yapılardan yararlanın</span><span class="sxs-lookup"><span data-stu-id="5ffe6-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="5ffe6-119">Tekil uzun süre çalışan işlemleri önlemek için kapsamlı toplu işlemleri kullanarak verileri işlemek</span><span class="sxs-lookup"><span data-stu-id="5ffe6-119">Process data using scoped batches to avoid singular long running transactions</span></span>
* <span data-ttu-id="5ffe6-120">Bir bölüm düzeni büyük değişiklikler belli bir bölüm için değiştirme benimsemeyi</span><span class="sxs-lookup"><span data-stu-id="5ffe6-120">Adopt a partition switching pattern for large modifications to a given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="5ffe6-121">En az tam günlük kaydı karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="5ffe6-121">Minimal vs. full logging</span></span>
<span data-ttu-id="5ffe6-122">Her satır değişiklik izlemek için işlem günlüğü kullanın, tam olarak günlüğe kaydedilmiş işlemlerin en düşük düzeyde günlüğe kaydedilmiş işlemlerin kapsam ayırma ve yalnızca meta veri değişiklikleri takip edin.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-122">Unlike fully logged operations, which use the transaction log to keep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="5ffe6-123">Bu nedenle, en az günlük kaydı geri alma işlemi bir hata veya açık bir istekte durumunda için gerekli olan bilgiler günlüğü içerir (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="5ffe6-123">Therefore, minimal logging involves logging only the information that is required to rollback the transaction in the event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="5ffe6-124">Bilgi işlem günlüğünde daha az izlenen gibi en düşük düzeyde günlüğe kaydedilmiş bir işlemin benzer şekilde boyutlandırılmış tam olarak günlüğe kaydedilmiş bir işlemin daha iyi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-124">As much less information is tracked in the transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="5ffe6-125">Ayrıca, daha az yazma işlem günlüğü gitmek için günlük verileri kadar daha az miktarda oluşturulur ve bu nedenle daha fazla g/ç etkilidir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-125">Furthermore, because fewer writes go the transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="5ffe6-126">İşlem güvenliği sınırları yalnızca tam olarak günlüğe kaydedilen işlemleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-126">The transaction safety limits only apply to fully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="5ffe6-127">En düşük düzeyde günlüğe kaydedilmiş işlemlerin açık işlemlerde yer alabilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="5ffe6-128">Ayırma yapılarında tüm değişiklikleri izlenen gibi en düşük düzeyde günlüğe kaydedilmiş işlemlerin geri mümkündür.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-128">As all changes in allocation structures are tracked, it is possible to roll back minimally logged operations.</span></span> <span data-ttu-id="5ffe6-129">Değişiklik "en düşük düzeyde" kaydedilir anlamak önemlidir beklemediğiniz oturum değil.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-129">It is important to understand that the change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="5ffe6-130">En düşük düzeyde günlüğe kaydedilmiş işlemlerin</span><span class="sxs-lookup"><span data-stu-id="5ffe6-130">Minimally logged operations</span></span>
<span data-ttu-id="5ffe6-131">Aşağıdaki işlemleri en düşük düzeyde günlüğe kaydedilmesini yeteneğine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="5ffe6-131">The following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="5ffe6-132">TABLE AS SELECT OLUŞTURUN ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="5ffe6-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="5ffe6-133">EKLE... SEÇİN</span><span class="sxs-lookup"><span data-stu-id="5ffe6-133">INSERT..SELECT</span></span>
* <span data-ttu-id="5ffe6-134">DİZİN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="5ffe6-134">CREATE INDEX</span></span>
* <span data-ttu-id="5ffe6-135">ALTER INDEX YENİDEN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="5ffe6-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="5ffe6-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="5ffe6-136">DROP INDEX</span></span>
* <span data-ttu-id="5ffe6-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="5ffe6-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="5ffe6-138">TABLO BIRAKMA</span><span class="sxs-lookup"><span data-stu-id="5ffe6-138">DROP TABLE</span></span>
* <span data-ttu-id="5ffe6-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="5ffe6-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="5ffe6-140">İç veri taşıma işlemleri (gibi `BROADCAST` ve `SHUFFLE`) göre hareket güvenlik sınırı etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by the transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="5ffe6-141">Toplu yükleme ile en az günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="5ffe6-142">`CTAS`ve `INSERT...SELECT` olan hem de toplu yükleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="5ffe6-143">Ancak, hem de hedef tablo tanımı tarafından etkilenir ve yük senaryoya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-143">However, both are influenced by the target table definition and depend on the load scenario.</span></span> <span data-ttu-id="5ffe6-144">Toplu işlemi tam olarak veya en düşük düzeyde oturum varsa açıklayan bir tablo aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="5ffe6-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="5ffe6-145">Birincil dizin</span><span class="sxs-lookup"><span data-stu-id="5ffe6-145">Primary Index</span></span> | <span data-ttu-id="5ffe6-146">Yükleme senaryosu</span><span class="sxs-lookup"><span data-stu-id="5ffe6-146">Load Scenario</span></span> | <span data-ttu-id="5ffe6-147">Oturum açma modu</span><span class="sxs-lookup"><span data-stu-id="5ffe6-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5ffe6-148">Yığın</span><span class="sxs-lookup"><span data-stu-id="5ffe6-148">Heap</span></span> |<span data-ttu-id="5ffe6-149">Herhangi biri</span><span class="sxs-lookup"><span data-stu-id="5ffe6-149">Any</span></span> |<span data-ttu-id="5ffe6-150">**En az**</span><span class="sxs-lookup"><span data-stu-id="5ffe6-150">**Minimal**</span></span> |
| <span data-ttu-id="5ffe6-151">Kümelenmiş dizini</span><span class="sxs-lookup"><span data-stu-id="5ffe6-151">Clustered Index</span></span> |<span data-ttu-id="5ffe6-152">Boş hedef tablo</span><span class="sxs-lookup"><span data-stu-id="5ffe6-152">Empty target table</span></span> |<span data-ttu-id="5ffe6-153">**En az**</span><span class="sxs-lookup"><span data-stu-id="5ffe6-153">**Minimal**</span></span> |
| <span data-ttu-id="5ffe6-154">Kümelenmiş dizini</span><span class="sxs-lookup"><span data-stu-id="5ffe6-154">Clustered Index</span></span> |<span data-ttu-id="5ffe6-155">Yüklenen satırları hedef var olan sayfaları ile çakışmaması</span><span class="sxs-lookup"><span data-stu-id="5ffe6-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="5ffe6-156">**En az**</span><span class="sxs-lookup"><span data-stu-id="5ffe6-156">**Minimal**</span></span> |
| <span data-ttu-id="5ffe6-157">Kümelenmiş dizini</span><span class="sxs-lookup"><span data-stu-id="5ffe6-157">Clustered Index</span></span> |<span data-ttu-id="5ffe6-158">Hedef varolan sayfalarında yüklenen satırları çakışıyor</span><span class="sxs-lookup"><span data-stu-id="5ffe6-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="5ffe6-159">Tam</span><span class="sxs-lookup"><span data-stu-id="5ffe6-159">Full</span></span> |
| <span data-ttu-id="5ffe6-160">Kümelenmiş Columnstore dizini</span><span class="sxs-lookup"><span data-stu-id="5ffe6-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="5ffe6-161">Yığın boyutu > hizalı bölüm dağıtım başına 102,400 =</span><span class="sxs-lookup"><span data-stu-id="5ffe6-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="5ffe6-162">**En az**</span><span class="sxs-lookup"><span data-stu-id="5ffe6-162">**Minimal**</span></span> |
| <span data-ttu-id="5ffe6-163">Kümelenmiş Columnstore dizini</span><span class="sxs-lookup"><span data-stu-id="5ffe6-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="5ffe6-164">Toplu iş boyutu < 102,400 hizalı bölüm dağıtım başına</span><span class="sxs-lookup"><span data-stu-id="5ffe6-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="5ffe6-165">Tam</span><span class="sxs-lookup"><span data-stu-id="5ffe6-165">Full</span></span> |

<span data-ttu-id="5ffe6-166">Bu, ikincil veya kümelenmemiş dizinler güncelleştirilecek tüm yazma tam olarak günlüğe kaydedilmiş işlemlerin her zaman olacağını dikkate değerdir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-166">It is worth noting that any writes to update secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ffe6-167">SQL veri ambarı 60 dağıtımları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="5ffe6-168">Bu nedenle, tüm satırları eşit olarak dağıtılır ve tek bir bölüm giriş, toplu 6,144,000 satır içermesi gerekir varsayılarak veya en düşük düzeyde bir kümelenmiş Columnstore dizini yazılırken günlüğe kaydedilecek daha büyük.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need to contain 6,144,000 rows or larger to be minimally logged when writing to a Clustered Columnstore Index.</span></span> <span data-ttu-id="5ffe6-169">Ardından tablonun bölümlenme şekli ve bölüm sınırları eklenen satır span bile veri dağıtım varsayılarak bölüm sınır başına 6,144,000 satır gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-169">If the table is partitioned and the rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="5ffe6-170">Her bölümde her dağıtım bağımsız olarak dağıtım en düşük düzeyde tutulacak INSERT 102,400 satır eşiği aşması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-170">Each partition in each distribution must independently exceed the 102,400 row threshold for the insert to be minimally logged into the distribution.</span></span>
> 
> 

<span data-ttu-id="5ffe6-171">Kümelenmiş bir dizin ile bir boş olmayan tabloya veri yükleme genellikle tam olarak günlüğe kaydedilen ve en düşük düzeyde oturum satır bir karışımını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="5ffe6-172">Kümelenmiş bir dizin sayfalarını dengeli ağacının (b-ağacı) ' dir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="5ffe6-173">Sayfa için zaten var. başka bir işlem satırları yazılmakta varsa, bu yazma tam olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-173">If the page being written to already contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="5ffe6-174">Sayfa boş ise, ancak daha sonra bu sayfayı yazma en düşük düzeyde günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-174">However, if the page is empty then the write to that page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="5ffe6-175">Siler en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-175">Optimizing deletes</span></span>
<span data-ttu-id="5ffe6-176">`DELETE`tam olarak günlüğe kaydedilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="5ffe6-177">Büyük miktarda veri bir tablo veya bir bölümü silmek gerekiyorsa, genellikle daha fazla için mantıklıdır `SELECT` korumak istediğiniz veri en düşük düzeyde günlüğe kaydedilen bir işlem olarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-177">If you need to delete a large amount of data in a table or a partition, it often makes more sense to `SELECT` the data you wish to keep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="5ffe6-178">Bunu gerçekleştirmek için yeni bir tablo oluşturma [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="5ffe6-178">To accomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="5ffe6-179">Oluşturduktan sonra kullanmak [yeniden adlandırma] [ RENAME] eski tablonuz yeni oluşturulan tabloyla takas etmek.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-179">Once created, use [RENAME][RENAME] to swap out your old table with the newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only the records we want to kep (PromotionKey 2)
CREATE TABLE [dbo].[FactInternetSales_d]
WITH
(    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
)
AS
SELECT     *
FROM     [dbo].[FactInternetSales]
WHERE    [PromotionKey] = 2
OPTION (LABEL = 'CTAS : Delete')
;

--Step 02. Rename the Tables to replace the 
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] TO [FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="5ffe6-180">Güncelleştirmeleri en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-180">Optimizing updates</span></span>
<span data-ttu-id="5ffe6-181">`UPDATE`tam olarak günlüğe kaydedilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="5ffe6-182">Bir bölüm, genellikle en düşük düzeyde günlüğe kaydedilmiş bir işlemin gibi kullanmak için daha etkili olabilir ya da çok sayıda tablodaki satırları güncelleştirmek gereken [CTAS] [ CTAS] Bunu yapmak için.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-182">If you need to update a large number of rows in a table or a partition it can often be far more efficient to use a minimally logged operation such as [CTAS][CTAS] to do so.</span></span>

<span data-ttu-id="5ffe6-183">Tam bir tablo aşağıdaki örnekte güncelleştirme dönüştürülen bir `CTAS` en az günlük mümkün olmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-183">In the example below a full table update has been converted to a `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="5ffe6-184">Bu durumda retrospectively bir indirim tutarı tablosundaki Satış ekliyoruz:</span><span class="sxs-lookup"><span data-stu-id="5ffe6-184">In this case we are retrospectively adding a discount amount to the sales in the table:</span></span>

```sql
--Step 01. Create a new table containing the "Update". 
CREATE TABLE [dbo].[FactInternetSales_u]
WITH
(    CLUSTERED INDEX
,    DISTRIBUTION = HASH([ProductKey])
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20000101, 20010101, 20020101, 20030101, 20040101, 20050101
                                                ,    20060101, 20070101, 20080101, 20090101, 20100101, 20110101
                                                ,    20120101, 20130101, 20140101, 20150101, 20160101, 20170101
                                                ,    20180101, 20190101, 20200101, 20210101, 20220101, 20230101
                                                ,    20240101, 20250101, 20260101, 20270101, 20280101, 20290101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
OPTION (LABEL = 'CTAS : Update')
;

--Step 02. Rename the tables
RENAME OBJECT [dbo].[FactInternetSales]   TO [FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] TO [FactInternetSales];

--Step 03. Drop the old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="5ffe6-185">Büyük tabloları yeniden oluşturma, SQL veri ambarı iş yükü yönetimi özelliklerini kullanarak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="5ffe6-186">Daha fazla ayrıntı iş yükü Yönetim bölümünde Lütfen başvurmak için [eşzamanlılık] [ concurrency] makalesi.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-186">For more details please refer to the workload management section in the [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="5ffe6-187">Bölüm geçiş ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-187">Optimizing with partition switching</span></span>
<span data-ttu-id="5ffe6-188">Büyük ölçekli değişiklikleri içinde ile karşılaştığı olduğunda bir [tablo bölüm][table partition], sonra da bir bölüm düzeni değiştirme algılama çok yapar.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="5ffe6-189">Veri değişikliği önemlidir ve birden çok bölüm yayılan, basitçe bölümlerden yineleme aynı sonucu veren.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-189">If the data modification is significant and spans multiple partitions, then simply iterating over the partitions achieves the same result.</span></span>

<span data-ttu-id="5ffe6-190">Bir bölüm anahtarı gerçekleştirme adımları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5ffe6-190">The steps to perform a partition switch are as follows:</span></span>

1. <span data-ttu-id="5ffe6-191">Boş bir bölüm çıkışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ffe6-191">Create an empty out partition</span></span>
2. <span data-ttu-id="5ffe6-192">'Güncelleştirme' CTAS gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-192">Perform the 'update' as a CTAS</span></span>
3. <span data-ttu-id="5ffe6-193">Var olan verilerini out tabloya geç</span><span class="sxs-lookup"><span data-stu-id="5ffe6-193">Switch out the existing data to the out table</span></span>
4. <span data-ttu-id="5ffe6-194">Yeni verileri geçiş</span><span class="sxs-lookup"><span data-stu-id="5ffe6-194">Switch in the new data</span></span>
5. <span data-ttu-id="5ffe6-195">Verileri temizleme</span><span class="sxs-lookup"><span data-stu-id="5ffe6-195">Clean up the data</span></span>

<span data-ttu-id="5ffe6-196">Ancak, geçiş yapmak için bölümleri belirlemenize yardımcı olması için öncelikle aşağıdaki gibi bir yardımcı yordamı oluşturmamız gereken.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-196">However, to help identify the partitions to switch we will first need to build a helper procedure such as the one below.</span></span> 

```sql
CREATE PROCEDURE dbo.partition_data_get
    @schema_name           NVARCHAR(128)
,    @table_name               NVARCHAR(128)
,    @boundary_value           INT
AS
IF OBJECT_ID('tempdb..#ptn_data') IS NOT NULL
BEGIN
    DROP TABLE #ptn_data
END
CREATE TABLE #ptn_data
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
WITH CTE
AS
(
SELECT     s.name                            AS [schema_name]
,        t.name                            AS [table_name]
,         p.partition_number                AS [ptn_nmbr]
,        p.[rows]                        AS [ptn_rows]
,        CAST(r.[value] AS INT)            AS [boundary_value]
FROM        sys.schemas                    AS s
JOIN        sys.tables                    AS t    ON  s.[schema_id]        = t.[schema_id]
JOIN        sys.indexes                    AS i    ON     t.[object_id]        = i.[object_id]
JOIN        sys.partitions                AS p    ON     i.[object_id]        = p.[object_id] 
                                                AND i.[index_id]        = p.[index_id] 
JOIN        sys.partition_schemes        AS h    ON     i.[data_space_id]    = h.[data_space_id]
JOIN        sys.partition_functions        AS f    ON     h.[function_id]        = f.[function_id]
LEFT JOIN    sys.partition_range_values    AS r     ON     f.[function_id]        = r.[function_id] 
                                                AND r.[boundary_id]        = p.[partition_number]
WHERE i.[index_id] <= 1
)
SELECT    *
FROM    CTE
WHERE    [schema_name]        = @schema_name
AND        [table_name]        = @table_name
AND        [boundary_value]    = @boundary_value
OPTION (LABEL = 'dbo.partition_data_get : CTAS : #ptn_data')
;
GO
```

<span data-ttu-id="5ffe6-197">Bu yordam, kodu yeniden kullanma en üst düzeye çıkarır ve bölüm örnek daha küçük değiştirme tutar.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-197">This procedure maximizes code re-use and keeps the partition switching example more compact.</span></span>

<span data-ttu-id="5ffe6-198">Aşağıdaki kodu tam bir bölüm yordamı değiştirme elde etmek için yukarıdaki beş adımı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-198">The code below demonstrates the five steps mentioned above to achieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table to switch out the data 
IF OBJECT_ID('[dbo].[FactInternetSales_out]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_out]
END

CREATE TABLE [dbo].[FactInternetSales_out]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS
SELECT *
FROM    [dbo].[FactInternetSales]
WHERE 1=2
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Create a partitioned aligned table and update the data in the select portion of the CTAS
IF OBJECT_ID('[dbo].[FactInternetSales_in]') IS NOT NULL
BEGIN
    DROP TABLE [dbo].[FactInternetSales_in]
END

CREATE TABLE [dbo].[FactInternetSales_in]
WITH
(    DISTRIBUTION = HASH([ProductKey])
,    CLUSTERED COLUMNSTORE INDEX
,     PARTITION     (    [OrderDateKey] RANGE RIGHT 
                                    FOR VALUES    (    20020101, 20030101
                                                )
                )
)
AS 
SELECT
    [ProductKey]  
,    [OrderDateKey] 
,    [DueDateKey]  
,    [ShipDateKey] 
,    [CustomerKey] 
,    [PromotionKey] 
,    [CurrencyKey] 
,    [SalesTerritoryKey]
,    [SalesOrderNumber]
,    [SalesOrderLineNumber]
,    [RevisionNumber]
,    [OrderQuantity]
,    [UnitPrice]
,    [ExtendedAmount]
,    [UnitPriceDiscountPct]
,    ISNULL(CAST(5 as float),0) AS [DiscountAmount]
,    [ProductStandardCost]
,    [TotalProductCost]
,    ISNULL(CAST(CASE WHEN [SalesAmount] <=5 THEN 0
         ELSE [SalesAmount] - 5
         END AS MONEY),0) AS [SalesAmount]
,    [TaxAmt]
,    [Freight]
,    [CarrierTrackingNumber] 
,    [CustomerPONumber]
FROM    [dbo].[FactInternetSales]
WHERE    OrderDateKey BETWEEN 20020101 AND 20021231
OPTION (LABEL = 'CTAS : Partition Switch IN : UPDATE')
;

--Use the helper procedure to identify the partitions
--The source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--The "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--The "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch the partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' TO [dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' TO [dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform the clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="5ffe6-199">Küçük toplu günlüğüyle simge durumuna küçült</span><span class="sxs-lookup"><span data-stu-id="5ffe6-199">Minimize logging with small batches</span></span>
<span data-ttu-id="5ffe6-200">Büyük veri değiştirme işlemleri için bu işlemi öbekleri veya toplu iş birimini kapsam içine bölmek için mantıklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-200">For large data modification operations, it may make sense to divide the operation into chunks or batches to scope the unit of work.</span></span>

<span data-ttu-id="5ffe6-201">Çalışan bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-201">A working example is provided below.</span></span> <span data-ttu-id="5ffe6-202">Toplu iş boyutu Önemsiz birkaç teknik vurgulamak için ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-202">The batch size has been set to a trivial number to highlight the technique.</span></span> <span data-ttu-id="5ffe6-203">Gerçekte toplu iş boyutu önemli ölçüde daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-203">In reality the batch size would be significantly larger.</span></span> 

```sql
SET NO_COUNT ON;
IF OBJECT_ID('tempdb..#t') IS NOT NULL
BEGIN
    DROP TABLE #t;
    PRINT '#t dropped';
END

CREATE TABLE #t
WITH    (    DISTRIBUTION = ROUND_ROBIN
        ,    HEAP
        )
AS
SELECT    ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS seq_nmbr
,        SalesOrderNumber
,        SalesOrderLineNumber
FROM    dbo.FactInternetSales
WHERE    [OrderDateKey] BETWEEN 20010101 and 20011231
;

DECLARE    @seq_start        INT = 1
,        @batch_iterator    INT = 1
,        @batch_size        INT = 50
,        @max_seq_nmbr    INT = (SELECT MAX(seq_nmbr) FROM dbo.#t)
;

DECLARE    @batch_count    INT = (SELECT CEILING((@max_seq_nmbr*1.0)/@batch_size))
,        @seq_end        INT = @batch_size
;

SELECT COUNT(*)
FROM    dbo.FactInternetSales f

PRINT 'MAX_seq_nmbr '+CAST(@max_seq_nmbr AS VARCHAR(20))
PRINT 'MAX_Batch_count '+CAST(@batch_count AS VARCHAR(20))

WHILE    @batch_iterator <= @batch_count
BEGIN
    DELETE
    FROM    dbo.FactInternetSales
    WHERE EXISTS
    (
            SELECT    1
            FROM    #t t
            WHERE    seq_nmbr BETWEEN  @seq_start AND @seq_end
            AND        FactInternetSales.SalesOrderNumber        = t.SalesOrderNumber
            AND        FactInternetSales.SalesOrderLineNumber    = t.SalesOrderLineNumber
    )
    ;

    SET @seq_start = @seq_end
    SET @seq_end = (@seq_start+@batch_size);
    SET @batch_iterator +=1;
END
```

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="5ffe6-204">Duraklatma ve ölçeklendirme Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="5ffe6-204">Pause and scaling guidance</span></span>
<span data-ttu-id="5ffe6-205">Azure SQL Data Warehouse, duraklatma, sürdürme ve veri ambarınız isteğe bağlı ölçeği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="5ffe6-206">Duraklattığınızda veya SQL Data Warehouse ölçeklendirebilir yürütülen işlemler hemen sonlandırılır anlamak önemlidir; geri alınması açık işlemler neden oluyor.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-206">When you pause or scale your SQL Data Warehouse it is important to understand that any in-flight transactions are terminated immediately; causing any open transactions to be rolled back.</span></span> <span data-ttu-id="5ffe6-207">İş yükünüzün uzun çalışan ve tamamlanmamış veri değişikliği duraklama veya ölçek işlemi öncesinde yayımlanan değilse, bu iş geri gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-207">If your workload had issued a long running and incomplete data modification prior to the pause or scale operation, then this work will need to be undone.</span></span> <span data-ttu-id="5ffe6-208">Bu, duraklatmak veya Azure SQL Data Warehouse veritabanınızı ölçeklendirmek için gereken süreyi etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-208">This may impact the time it takes to pause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5ffe6-209">Her ikisi de `UPDATE` ve `DELETE` tam olarak günlüğe kaydedilen işlemleri ve bunlar geri alma/yineleme için işlemleri eşdeğer en düşük düzeyde işlemleri günlüğe daha önemli ölçüde uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="5ffe6-210">En iyi senaryo uçuş veri değişikliği işlemlerin duraklatma veya SQL Data Warehouse ölçeklendirme önce tam kurmanızı sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-210">The best scenario is to let in flight data modification transactions complete prior to pausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="5ffe6-211">Ancak, bu her zaman pratik olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-211">However, this may not always be practical.</span></span> <span data-ttu-id="5ffe6-212">Uzun bir geri alma riskini azaltmak için aşağıdaki seçeneklerden birini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="5ffe6-212">To mitigate the risk of a long rollback, consider one of the following options:</span></span>

* <span data-ttu-id="5ffe6-213">Uzun süre çalışan işlemleri kullanarak yeniden yazma [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="5ffe6-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="5ffe6-214">İşlemi parçalara bölmek; Alt satır kümesi üzerinde çalışan</span><span class="sxs-lookup"><span data-stu-id="5ffe6-214">Break the operation down into chunks; operating on a subset of the rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ffe6-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ffe6-215">Next steps</span></span>
<span data-ttu-id="5ffe6-216">Bkz: [SQL Data Warehouse işlemlerinde] [ Transactions in SQL Data Warehouse] yalıtım düzeylerinde ve işlem sınırları hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="5ffe6-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] to learn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="5ffe6-217">Diğer en iyi yöntemler genel bakış için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="5ffe6-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Transactions in SQL Data Warehouse]: ./sql-data-warehouse-develop-transactions.md
[table partition]: ./sql-data-warehouse-tables-partition.md
[Concurrency]: ./sql-data-warehouse-develop-concurrency.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->
[alter index]:https://msdn.microsoft.com/library/ms188388.aspx
[RENAME]: https://msdn.microsoft.com/library/mt631611.aspx

<!-- Other web references -->

