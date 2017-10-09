---
title: "SQL veri ambarı için aaaOptimizing işlemler | Microsoft Docs"
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
ms.openlocfilehash: 1a821161711db9460b7e10d3cf7ba498d711448b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-transactions-for-sql-data-warehouse"></a><span data-ttu-id="2e30b-103">İşlemleri SQL Data Warehouse için en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="2e30b-103">Optimizing transactions for SQL Data Warehouse</span></span>
<span data-ttu-id="2e30b-104">Bu makalede nasıl toooptimize hello uzun düzeyine riskini en aza indirme sırasında işlem kodunuzu performansını açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-104">This article explains how toooptimize hello performance of your transactional code while minimizing risk for long rollbacks.</span></span>

## <a name="transactions-and-logging"></a><span data-ttu-id="2e30b-105">İşlemler ve günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="2e30b-105">Transactions and logging</span></span>
<span data-ttu-id="2e30b-106">İşlemler, ilişkisel veritabanı altyapısını önemli bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-106">Transactions are an important component of a relational database engine.</span></span> <span data-ttu-id="2e30b-107">SQL veri ambarı işlemleri sırasında veri değişikliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-107">SQL Data Warehouse uses transactions during data modification.</span></span> <span data-ttu-id="2e30b-108">Bu işlemler, açık veya örtülü olabilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-108">These transactions can be explicit or implicit.</span></span> <span data-ttu-id="2e30b-109">Tek `INSERT`, `UPDATE` ve `DELETE` deyimleri örtülü işlemler tüm örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-109">Single `INSERT`, `UPDATE` and `DELETE` statements are all examples of implicit transactions.</span></span> <span data-ttu-id="2e30b-110">Açık işlemleri açıkça kullanarak bir geliştirici tarafından yazılan `BEGIN TRAN`, `COMMIT TRAN` veya `ROLLBACK TRAN` ve birden çok değişikliği deyimleri birlikte tek bir atomik biriminde bağlı toobe gerektiğinde tipik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-110">Explicit transactions are written explicitly by a developer using `BEGIN TRAN`, `COMMIT TRAN` or `ROLLBACK TRAN` and are typically used when multiple modification statements need toobe tied together in a single atomic unit.</span></span> 

<span data-ttu-id="2e30b-111">Azure SQL Data Warehouse değişiklikleri toohello veritabanı işlem günlüklerinin kullanarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="2e30b-111">Azure SQL Data Warehouse commits changes toohello database using transaction logs.</span></span> <span data-ttu-id="2e30b-112">Her dağıtım kendi işlem günlüğü vardır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-112">Each distribution has its own transaction log.</span></span> <span data-ttu-id="2e30b-113">İşlem günlüğü yazma otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-113">Transaction log writes are automatic.</span></span> <span data-ttu-id="2e30b-114">Gerekli yapılandırma yoktur.</span><span class="sxs-lookup"><span data-stu-id="2e30b-114">There is no configuration required.</span></span> <span data-ttu-id="2e30b-115">Ancak, bu işlem hello yazma garanti adımında, bir ek yük hello sistemde tanıtır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-115">However, whilst this process guarantees hello write it does introduce an overhead in hello system.</span></span> <span data-ttu-id="2e30b-116">İşlemsel olarak verimli kodlar yazarak bu etkiyi en aza indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e30b-116">You can minimize this impact by writing transactionally efficient code.</span></span> <span data-ttu-id="2e30b-117">İşlemsel olarak verimli kod kapsamlı iki kategoride yer alır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-117">Transactionally efficient code broadly falls into two categories.</span></span>

* <span data-ttu-id="2e30b-118">Mümkün olduğunda en az günlük yapılardan yararlanın</span><span class="sxs-lookup"><span data-stu-id="2e30b-118">Leverage minimal logging constructs where possible</span></span>
* <span data-ttu-id="2e30b-119">Uzun süre çalışan işlemleri kapsamlı toplu tooavoid tekil kullanarak verileri işlemek</span><span class="sxs-lookup"><span data-stu-id="2e30b-119">Process data using scoped batches tooavoid singular long running transactions</span></span>
* <span data-ttu-id="2e30b-120">Bir bölüm düzeni büyük değişiklikler tooa verilen bölüm için değiştirme benimsemeyi</span><span class="sxs-lookup"><span data-stu-id="2e30b-120">Adopt a partition switching pattern for large modifications tooa given partition</span></span>

## <a name="minimal-vs-full-logging"></a><span data-ttu-id="2e30b-121">En az tam günlük kaydı karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="2e30b-121">Minimal vs. full logging</span></span>
<span data-ttu-id="2e30b-122">Merhaba işlem günlüğü tookeep her satır değişiklik izini kullanacağınız tam olarak günlüğe kaydedilmiş işlemlerin en düşük düzeyde günlüğe kaydedilmiş işlemlerin kapsam ayırma ve yalnızca meta veri değişiklikleri takip edin.</span><span class="sxs-lookup"><span data-stu-id="2e30b-122">Unlike fully logged operations, which use hello transaction log tookeep track of every row change, minimally logged operations keep track of extent allocations and meta-data changes only.</span></span> <span data-ttu-id="2e30b-123">Bu nedenle, yalnızca gerekli toorollback hello işlemde hello olay bir hata veya açık bir istekte hello bilgilerini günlüğe kaydetme en az günlük içerir (`ROLLBACK TRAN`).</span><span class="sxs-lookup"><span data-stu-id="2e30b-123">Therefore, minimal logging involves logging only hello information that is required toorollback hello transaction in hello event of a failure or an explicit request (`ROLLBACK TRAN`).</span></span> <span data-ttu-id="2e30b-124">En düşük düzeyde günlüğe kaydedilmiş bir işlemin benzer şekilde boyutlandırılmış tam olarak günlüğe kaydedilmiş bir işlemin daha iyi bilgi hello işlem günlüğünde daha az izlenen olarak gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-124">As much less information is tracked in hello transaction log, a minimally logged operation performs better than a similarly sized fully logged operation.</span></span> <span data-ttu-id="2e30b-125">Ayrıca, daha az yazma hello işlem günlüğü gitmek için günlük verileri kadar daha az miktarda oluşturulur ve bu nedenle daha fazla g/ç etkilidir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-125">Furthermore, because fewer writes go hello transaction log, a much smaller amount of log data is generated and so is more I/O efficient.</span></span>

<span data-ttu-id="2e30b-126">Merhaba işlem güvenlik sınırları yalnızca oturum açmış toofully operations uygulayın.</span><span class="sxs-lookup"><span data-stu-id="2e30b-126">hello transaction safety limits only apply toofully logged operations.</span></span>

> [!NOTE]
> <span data-ttu-id="2e30b-127">En düşük düzeyde günlüğe kaydedilmiş işlemlerin açık işlemlerde yer alabilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-127">Minimally logged operations can participate in explicit transactions.</span></span> <span data-ttu-id="2e30b-128">İzlenen ayırma yapılarında tüm değişiklikler, olası tooroll geri en düşük düzeyde olur işlemleri günlüğe.</span><span class="sxs-lookup"><span data-stu-id="2e30b-128">As all changes in allocation structures are tracked, it is possible tooroll back minimally logged operations.</span></span> <span data-ttu-id="2e30b-129">"En düşük düzeyde" olarak hello değişikliktir toounderstand oturum önemlidir beklemediğiniz oturum değil.</span><span class="sxs-lookup"><span data-stu-id="2e30b-129">It is important toounderstand that hello change is "minimally" logged it is not un-logged.</span></span>
> 
> 

## <a name="minimally-logged-operations"></a><span data-ttu-id="2e30b-130">En düşük düzeyde günlüğe kaydedilmiş işlemlerin</span><span class="sxs-lookup"><span data-stu-id="2e30b-130">Minimally logged operations</span></span>
<span data-ttu-id="2e30b-131">Merhaba aşağıdaki işlemleri en düşük düzeyde günlüğe kaydedilmesini yeteneğine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="2e30b-131">hello following operations are capable of being minimally logged:</span></span>

* <span data-ttu-id="2e30b-132">TABLE AS SELECT OLUŞTURUN ([CTAS][CTAS])</span><span class="sxs-lookup"><span data-stu-id="2e30b-132">CREATE TABLE AS SELECT ([CTAS][CTAS])</span></span>
* <span data-ttu-id="2e30b-133">EKLE... SEÇİN</span><span class="sxs-lookup"><span data-stu-id="2e30b-133">INSERT..SELECT</span></span>
* <span data-ttu-id="2e30b-134">DİZİN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="2e30b-134">CREATE INDEX</span></span>
* <span data-ttu-id="2e30b-135">ALTER INDEX YENİDEN OLUŞTURMA</span><span class="sxs-lookup"><span data-stu-id="2e30b-135">ALTER INDEX REBUILD</span></span>
* <span data-ttu-id="2e30b-136">DROP INDEX</span><span class="sxs-lookup"><span data-stu-id="2e30b-136">DROP INDEX</span></span>
* <span data-ttu-id="2e30b-137">TRUNCATE TABLE</span><span class="sxs-lookup"><span data-stu-id="2e30b-137">TRUNCATE TABLE</span></span>
* <span data-ttu-id="2e30b-138">TABLO BIRAKMA</span><span class="sxs-lookup"><span data-stu-id="2e30b-138">DROP TABLE</span></span>
* <span data-ttu-id="2e30b-139">ALTER TABLE SWITCH PARTITION</span><span class="sxs-lookup"><span data-stu-id="2e30b-139">ALTER TABLE SWITCH PARTITION</span></span>

<!--
- MERGE
- UPDATE on LOB Types .WRITE
- SELECT..INTO
-->

> [!NOTE]
> <span data-ttu-id="2e30b-140">İç veri taşıma işlemleri (gibi `BROADCAST` ve `SHUFFLE`) hello işlem güvenlik sınırı tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="2e30b-140">Internal data movement operations (such as `BROADCAST` and `SHUFFLE`) are not affected by hello transaction safety limit.</span></span>
> 
> 

## <a name="minimal-logging-with-bulk-load"></a><span data-ttu-id="2e30b-141">Toplu yükleme ile en az günlüğe kaydetme</span><span class="sxs-lookup"><span data-stu-id="2e30b-141">Minimal logging with bulk load</span></span>
<span data-ttu-id="2e30b-142">`CTAS`ve `INSERT...SELECT` olan hem de toplu yükleme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="2e30b-142">`CTAS` and `INSERT...SELECT` are both bulk load operations.</span></span> <span data-ttu-id="2e30b-143">Bununla birlikte, her ikisi de hello hedef tablo tanımı tarafından etkilenir ve hello yük senaryoya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-143">However, both are influenced by hello target table definition and depend on hello load scenario.</span></span> <span data-ttu-id="2e30b-144">Toplu işlemi tam olarak veya en düşük düzeyde oturum varsa açıklayan bir tablo aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="2e30b-144">Below is a table that explains if your bulk operation will be fully or minimally logged:</span></span>  

| <span data-ttu-id="2e30b-145">Birincil dizin</span><span class="sxs-lookup"><span data-stu-id="2e30b-145">Primary Index</span></span> | <span data-ttu-id="2e30b-146">Yükleme senaryosu</span><span class="sxs-lookup"><span data-stu-id="2e30b-146">Load Scenario</span></span> | <span data-ttu-id="2e30b-147">Oturum açma modu</span><span class="sxs-lookup"><span data-stu-id="2e30b-147">Logging Mode</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e30b-148">Yığın</span><span class="sxs-lookup"><span data-stu-id="2e30b-148">Heap</span></span> |<span data-ttu-id="2e30b-149">Herhangi biri</span><span class="sxs-lookup"><span data-stu-id="2e30b-149">Any</span></span> |<span data-ttu-id="2e30b-150">**En az**</span><span class="sxs-lookup"><span data-stu-id="2e30b-150">**Minimal**</span></span> |
| <span data-ttu-id="2e30b-151">Kümelenmiş dizini</span><span class="sxs-lookup"><span data-stu-id="2e30b-151">Clustered Index</span></span> |<span data-ttu-id="2e30b-152">Boş hedef tablo</span><span class="sxs-lookup"><span data-stu-id="2e30b-152">Empty target table</span></span> |<span data-ttu-id="2e30b-153">**En az**</span><span class="sxs-lookup"><span data-stu-id="2e30b-153">**Minimal**</span></span> |
| <span data-ttu-id="2e30b-154">Kümelenmiş dizini</span><span class="sxs-lookup"><span data-stu-id="2e30b-154">Clustered Index</span></span> |<span data-ttu-id="2e30b-155">Yüklenen satırları hedef var olan sayfaları ile çakışmaması</span><span class="sxs-lookup"><span data-stu-id="2e30b-155">Loaded rows do not overlap with existing pages in target</span></span> |<span data-ttu-id="2e30b-156">**En az**</span><span class="sxs-lookup"><span data-stu-id="2e30b-156">**Minimal**</span></span> |
| <span data-ttu-id="2e30b-157">Kümelenmiş dizini</span><span class="sxs-lookup"><span data-stu-id="2e30b-157">Clustered Index</span></span> |<span data-ttu-id="2e30b-158">Hedef varolan sayfalarında yüklenen satırları çakışıyor</span><span class="sxs-lookup"><span data-stu-id="2e30b-158">Loaded rows overlap with existing pages in target</span></span> |<span data-ttu-id="2e30b-159">Tam</span><span class="sxs-lookup"><span data-stu-id="2e30b-159">Full</span></span> |
| <span data-ttu-id="2e30b-160">Kümelenmiş Columnstore dizini</span><span class="sxs-lookup"><span data-stu-id="2e30b-160">Clustered Columnstore Index</span></span> |<span data-ttu-id="2e30b-161">Yığın boyutu > hizalı bölüm dağıtım başına 102,400 =</span><span class="sxs-lookup"><span data-stu-id="2e30b-161">Batch size >= 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="2e30b-162">**En az**</span><span class="sxs-lookup"><span data-stu-id="2e30b-162">**Minimal**</span></span> |
| <span data-ttu-id="2e30b-163">Kümelenmiş Columnstore dizini</span><span class="sxs-lookup"><span data-stu-id="2e30b-163">Clustered Columnstore Index</span></span> |<span data-ttu-id="2e30b-164">Toplu iş boyutu < 102,400 hizalı bölüm dağıtım başına</span><span class="sxs-lookup"><span data-stu-id="2e30b-164">Batch size < 102,400 per partition aligned distribution</span></span> |<span data-ttu-id="2e30b-165">Tam</span><span class="sxs-lookup"><span data-stu-id="2e30b-165">Full</span></span> |

<span data-ttu-id="2e30b-166">Bu tooupdate ikincil veya kümelenmemiş dizinleri her zaman tam olarak olacak yazma işlemlerini günlüğe önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-166">It is worth noting that any writes tooupdate secondary or non-clustered indexes will always be fully logged operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e30b-167">SQL veri ambarı 60 dağıtımları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-167">SQL Data Warehouse has 60 distributions.</span></span> <span data-ttu-id="2e30b-168">Bu nedenle, tüm satırları eşit olarak dağıtılır ve tek bir bölüm giriş, toplu toocontain 6,144,000 satır veya daha büyük toobe en düşük düzeyde gerekir varsayılarak tooa kümelenmiş Columnstore dizini yazılırken günlüğe.</span><span class="sxs-lookup"><span data-stu-id="2e30b-168">Therefore, assuming all rows are evenly distributed and landing in a single partition, your batch will need toocontain 6,144,000 rows or larger toobe minimally logged when writing tooa Clustered Columnstore Index.</span></span> <span data-ttu-id="2e30b-169">Ardından Merhaba tablonun bölümlenme şekli ve bölüm sınırları eklenmekte hello satırları span bile veri dağıtım varsayılarak bölüm sınır başına 6,144,000 satır gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-169">If hello table is partitioned and hello rows being inserted span partition boundaries, then you will need 6,144,000 rows per partition boundary assuming even data distribution.</span></span> <span data-ttu-id="2e30b-170">Her bölümde her dağıtım bağımsız olarak en düşük düzeyde hello dağıtım oturum hello INSERT toobe hello 102,400 satır eşiği aşması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-170">Each partition in each distribution must independently exceed hello 102,400 row threshold for hello insert toobe minimally logged into hello distribution.</span></span>
> 
> 

<span data-ttu-id="2e30b-171">Kümelenmiş bir dizin ile bir boş olmayan tabloya veri yükleme genellikle tam olarak günlüğe kaydedilen ve en düşük düzeyde oturum satır bir karışımını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-171">Loading data into a non-empty table with a clustered index can often contain a mixture of fully logged and minimally logged rows.</span></span> <span data-ttu-id="2e30b-172">Kümelenmiş bir dizin sayfalarını dengeli ağacının (b-ağacı) ' dir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-172">A clustered index is a balanced tree (b-tree) of pages.</span></span> <span data-ttu-id="2e30b-173">Merhaba sayfa tooalready başka bir işlem satırları içeren yazılmakta varsa, bu yazma tam olarak kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-173">If hello page being written tooalready contains rows from another transaction, then these writes will be fully logged.</span></span> <span data-ttu-id="2e30b-174">Merhaba sayfa boşsa, ancak ardından hello yazma toothat sayfa en düşük düzeyde günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-174">However, if hello page is empty then hello write toothat page will be minimally logged.</span></span>

## <a name="optimizing-deletes"></a><span data-ttu-id="2e30b-175">Siler en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="2e30b-175">Optimizing deletes</span></span>
<span data-ttu-id="2e30b-176">`DELETE`tam olarak günlüğe kaydedilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-176">`DELETE` is a fully logged operation.</span></span>  <span data-ttu-id="2e30b-177">Toodelete büyük miktarda veri bir tablo ya da bir bölüme ihtiyacınız varsa, genellikle daha fazla çok mantıklıdır`SELECT` hello veri en düşük düzeyde günlüğe kaydedilmiş bir işlemin çalıştırılabilir tookeep istiyor.</span><span class="sxs-lookup"><span data-stu-id="2e30b-177">If you need toodelete a large amount of data in a table or a partition, it often makes more sense too`SELECT` hello data you wish tookeep, which can be run as a minimally logged operation.</span></span>  <span data-ttu-id="2e30b-178">tooaccomplish Bu, yeni bir tablo ile oluşturmak [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="2e30b-178">tooaccomplish this, create a new table with [CTAS][CTAS].</span></span>  <span data-ttu-id="2e30b-179">Oluşturduktan sonra kullanmak [yeniden adlandırma] [ RENAME] tooswap eski tablonuz yeni oluşturulan hello tablosuyla çıkışı.</span><span class="sxs-lookup"><span data-stu-id="2e30b-179">Once created, use [RENAME][RENAME] tooswap out your old table with hello newly created table.</span></span>

```sql
-- Delete all sales transactions for Promotions except PromotionKey 2.

--Step 01. Create a new table select only hello records we want tookep (PromotionKey 2)
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

--Step 02. Rename hello Tables tooreplace hello 
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_d] too[FactInternetSales];
```

## <a name="optimizing-updates"></a><span data-ttu-id="2e30b-180">Güncelleştirmeleri en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="2e30b-180">Optimizing updates</span></span>
<span data-ttu-id="2e30b-181">`UPDATE`tam olarak günlüğe kaydedilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-181">`UPDATE` is a fully logged operation.</span></span>  <span data-ttu-id="2e30b-182">Çok sayıda tablodaki satırları tooupdate gerekir ya da bir bölüm, genellikle daha verimli toouse gibi en düşük düzeyde günlüğe kaydedilmiş bir işlemin olabilir [CTAS] [ CTAS] toodo şekilde.</span><span class="sxs-lookup"><span data-stu-id="2e30b-182">If you need tooupdate a large number of rows in a table or a partition it can often be far more efficient toouse a minimally logged operation such as [CTAS][CTAS] toodo so.</span></span>

<span data-ttu-id="2e30b-183">Hello dönüştürülmüş tooa tam tablosu güncelleştirmesi aşağıdaki örnekte bırakıldı `CTAS` en az günlük mümkün olmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2e30b-183">In hello example below a full table update has been converted tooa `CTAS` so that minimal logging is possible.</span></span>

<span data-ttu-id="2e30b-184">Bu durumda retrospectively indirim tutarı toohello satış hello tabloda ekliyoruz:</span><span class="sxs-lookup"><span data-stu-id="2e30b-184">In this case we are retrospectively adding a discount amount toohello sales in hello table:</span></span>

```sql
--Step 01. Create a new table containing hello "Update". 
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

--Step 02. Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales]   too[FactInternetSales_old];
RENAME OBJECT [dbo].[FactInternetSales_u] too[FactInternetSales];

--Step 03. Drop hello old table
DROP TABLE [dbo].[FactInternetSales_old]
```

> [!NOTE]
> <span data-ttu-id="2e30b-185">Büyük tabloları yeniden oluşturma, SQL veri ambarı iş yükü yönetimi özelliklerini kullanarak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-185">Re-creating large tables can benefit from using SQL Data Warehouse workload management features.</span></span> <span data-ttu-id="2e30b-186">Daha fazla ayrıntı Lütfen toohello iş yükü yönetimi hello bölümünde başvurun [eşzamanlılık] [ concurrency] makalesi.</span><span class="sxs-lookup"><span data-stu-id="2e30b-186">For more details please refer toohello workload management section in hello [concurrency][concurrency] article.</span></span>
> 
> 

## <a name="optimizing-with-partition-switching"></a><span data-ttu-id="2e30b-187">Bölüm geçiş ile en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="2e30b-187">Optimizing with partition switching</span></span>
<span data-ttu-id="2e30b-188">Büyük ölçekli değişiklikleri içinde ile karşılaştığı olduğunda bir [tablo bölüm][table partition], sonra da bir bölüm düzeni değiştirme algılama çok yapar.</span><span class="sxs-lookup"><span data-stu-id="2e30b-188">When faced with large scale modifications inside a [table partition][table partition], then a partition switching pattern makes a lot of sense.</span></span> <span data-ttu-id="2e30b-189">Merhaba, veri değişikliği önemlidir ve aynı sonucu birden çok bölüm, yalnızca hello bölümler yineleme başarır yayılma hello.</span><span class="sxs-lookup"><span data-stu-id="2e30b-189">If hello data modification is significant and spans multiple partitions, then simply iterating over hello partitions achieves hello same result.</span></span>

<span data-ttu-id="2e30b-190">Merhaba adımları tooperform bir bölüm anahtarı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="2e30b-190">hello steps tooperform a partition switch are as follows:</span></span>

1. <span data-ttu-id="2e30b-191">Boş bir bölüm çıkışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e30b-191">Create an empty out partition</span></span>
2. <span data-ttu-id="2e30b-192">Merhaba 'güncelleştirme' CTAS gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="2e30b-192">Perform hello 'update' as a CTAS</span></span>
3. <span data-ttu-id="2e30b-193">Hello mevcut veri toohello tablo dışarı giden geçiş</span><span class="sxs-lookup"><span data-stu-id="2e30b-193">Switch out hello existing data toohello out table</span></span>
4. <span data-ttu-id="2e30b-194">Merhaba yeni verileri geçiş</span><span class="sxs-lookup"><span data-stu-id="2e30b-194">Switch in hello new data</span></span>
5. <span data-ttu-id="2e30b-195">Merhaba verilerini temizle</span><span class="sxs-lookup"><span data-stu-id="2e30b-195">Clean up hello data</span></span>

<span data-ttu-id="2e30b-196">Ancak, toohelp ilk toobuild bir hello gibi bir yardımcı yordam aşağıdaki ihtiyacımız hello bölümleri tooswitch tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2e30b-196">However, toohelp identify hello partitions tooswitch we will first need toobuild a helper procedure such as hello one below.</span></span> 

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

<span data-ttu-id="2e30b-197">Bu yordam, kodu yeniden kullanma en üst düzeye çıkarır ve hello bölüm örnek daha küçük değiştirme tutar.</span><span class="sxs-lookup"><span data-stu-id="2e30b-197">This procedure maximizes code re-use and keeps hello partition switching example more compact.</span></span>

<span data-ttu-id="2e30b-198">Aşağıdaki Hello kodu hello beş adımı tam bir bölüm yordamı değiştirme tooachieve bahsedilen gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-198">hello code below demonstrates hello five steps mentioned above tooachieve a full partition switching routine.</span></span>

```sql
--Create a partitioned aligned empty table tooswitch out hello data 
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

--Create a partitioned aligned table and update hello data in hello select portion of hello CTAS
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

--Use hello helper procedure tooidentify hello partitions
--hello source table
EXEC dbo.partition_data_get 'dbo','FactInternetSales',20030101
DECLARE @ptn_nmbr_src INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_src

--hello "in" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_in',20030101
DECLARE @ptn_nmbr_in INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_in

--hello "out" table
EXEC dbo.partition_data_get 'dbo','FactInternetSales_out',20030101
DECLARE @ptn_nmbr_out INT = (SELECT ptn_nmbr FROM #ptn_data)
SELECT @ptn_nmbr_out

--Switch hello partitions over
DECLARE @SQL NVARCHAR(4000) = '
ALTER TABLE [dbo].[FactInternetSales]    SWITCH PARTITION '+CAST(@ptn_nmbr_src AS VARCHAR(20))    +' too[dbo].[FactInternetSales_out] PARTITION '    +CAST(@ptn_nmbr_out AS VARCHAR(20))+';
ALTER TABLE [dbo].[FactInternetSales_in] SWITCH PARTITION '+CAST(@ptn_nmbr_in AS VARCHAR(20))    +' too[dbo].[FactInternetSales] PARTITION '        +CAST(@ptn_nmbr_src AS VARCHAR(20))+';'
EXEC sp_executesql @SQL

--Perform hello clean-up
TRUNCATE TABLE dbo.FactInternetSales_out;
TRUNCATE TABLE dbo.FactInternetSales_in;

DROP TABLE dbo.FactInternetSales_out
DROP TABLE dbo.FactInternetSales_in
DROP TABLE #ptn_data
```

## <a name="minimize-logging-with-small-batches"></a><span data-ttu-id="2e30b-199">Küçük toplu günlüğüyle simge durumuna küçült</span><span class="sxs-lookup"><span data-stu-id="2e30b-199">Minimize logging with small batches</span></span>
<span data-ttu-id="2e30b-200">Büyük veri değiştirme işlemleri için Itanium tabanlı sistemler için anlamlı toodivide hello işlemi tooscope hello birime öbekleri veya toplu iş duruma getirebilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-200">For large data modification operations, it may make sense toodivide hello operation into chunks or batches tooscope hello unit of work.</span></span>

<span data-ttu-id="2e30b-201">Çalışan bir örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-201">A working example is provided below.</span></span> <span data-ttu-id="2e30b-202">Merhaba toplu iş boyutu tooa Önemsiz numara toohighlight hello teknik ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="2e30b-202">hello batch size has been set tooa trivial number toohighlight hello technique.</span></span> <span data-ttu-id="2e30b-203">Gerçekte hello toplu iş boyutu önemli ölçüde daha büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-203">In reality hello batch size would be significantly larger.</span></span> 

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

## <a name="pause-and-scaling-guidance"></a><span data-ttu-id="2e30b-204">Duraklatma ve ölçeklendirme Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="2e30b-204">Pause and scaling guidance</span></span>
<span data-ttu-id="2e30b-205">Azure SQL Data Warehouse, duraklatma, sürdürme ve veri ambarınız isteğe bağlı ölçeği olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="2e30b-205">Azure SQL Data Warehouse lets you pause, resume and scale your data warehouse on demand.</span></span> <span data-ttu-id="2e30b-206">Duraklatmak veya SQL Data Warehouse ölçeklendirebilir yüklediğinizde yürütülen işlemler hemen sonlandırılır önemli toounderstand olur; Tüm açık hareketleri toobe neden geri alındı.</span><span class="sxs-lookup"><span data-stu-id="2e30b-206">When you pause or scale your SQL Data Warehouse it is important toounderstand that any in-flight transactions are terminated immediately; causing any open transactions toobe rolled back.</span></span> <span data-ttu-id="2e30b-207">İş yükünüzün uzun süre çalışan ve tamamlanmamış veri değişikliği önceki verilen toohello duraklatma veya ölçeklendirme işlemi, sonra da bu iş geri toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-207">If your workload had issued a long running and incomplete data modification prior toohello pause or scale operation, then this work will need toobe undone.</span></span> <span data-ttu-id="2e30b-208">Bu toopause hello süresi etkisi veya Azure SQL Data Warehouse veritabanınızın ölçeğini olabilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-208">This may impact hello time it takes toopause or scale your Azure SQL Data Warehouse database.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2e30b-209">Her ikisi de `UPDATE` ve `DELETE` tam olarak günlüğe kaydedilen işlemleri ve bunlar geri alma/yineleme için işlemleri eşdeğer en düşük düzeyde işlemleri günlüğe daha önemli ölçüde uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-209">Both `UPDATE` and `DELETE` are fully logged operations and so these undo/redo operations can take significantly longer than equivalent minimally logged operations.</span></span> 
> 
> 

<span data-ttu-id="2e30b-210">Merhaba en iyi senaryo, uçuş veri değiştirme işlemleri tam önceki toopausing veya ölçeklendirme SQL Data Warehouse toolet bulunur.</span><span class="sxs-lookup"><span data-stu-id="2e30b-210">hello best scenario is toolet in flight data modification transactions complete prior toopausing or scaling SQL Data Warehouse.</span></span> <span data-ttu-id="2e30b-211">Ancak, bu her zaman pratik olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="2e30b-211">However, this may not always be practical.</span></span> <span data-ttu-id="2e30b-212">uzun bir geri alma toomitigate hello riskini seçenekleri aşağıdaki hello birini dikkate alın:</span><span class="sxs-lookup"><span data-stu-id="2e30b-212">toomitigate hello risk of a long rollback, consider one of hello following options:</span></span>

* <span data-ttu-id="2e30b-213">Uzun süre çalışan işlemleri kullanarak yeniden yazma [CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="2e30b-213">Re-write long running operations using [CTAS][CTAS]</span></span>
* <span data-ttu-id="2e30b-214">Merhaba işlemi parçalara bölmek; bir alt hello satır kümesi üzerinde çalışan</span><span class="sxs-lookup"><span data-stu-id="2e30b-214">Break hello operation down into chunks; operating on a subset of hello rows</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e30b-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2e30b-215">Next steps</span></span>
<span data-ttu-id="2e30b-216">Bkz: [SQL Data Warehouse işlemlerinde] [ Transactions in SQL Data Warehouse] toolearn yalıtım düzeyleri ve işlem sınırları hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="2e30b-216">See [Transactions in SQL Data Warehouse][Transactions in SQL Data Warehouse] toolearn more about isolation levels and transactional limits.</span></span>  <span data-ttu-id="2e30b-217">Diğer en iyi yöntemler genel bakış için bkz: [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="2e30b-217">For an overview of other Best Practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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

