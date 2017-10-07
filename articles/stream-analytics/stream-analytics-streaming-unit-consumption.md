---
title: "Azure Stream Analytics: akış birimleri, iş toouse verimli bir şekilde en iyi duruma getirme | Microsoft Docs"
description: "Ölçekleme ve performans Azure akış analizi için en iyi uygulamaları sorgulayın."
keywords: "Birim, sorgu performansı akış"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="63c31-104">Akış birimleri, iş toouse verimli bir şekilde en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="63c31-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="63c31-105">Azure Stream Analytics iş akış birimleri (SUs) çalışan ağırlığı"" Merhaba performans toplar.</span><span class="sxs-lookup"><span data-stu-id="63c31-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="63c31-106">SUs tüketilen tooexecute bir işi hello bilgi işlem kaynaklarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="63c31-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="63c31-107">SUs kapasite CPU, bellek, karışık bir ölçüyü temel bir şekilde toodescribe hello göreli olay işleme sağlamak ve okuma ve oranları yazma.</span><span class="sxs-lookup"><span data-stu-id="63c31-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="63c31-108">Merhaba sorgu mantığı ve sizden tooknow depolama katmanı performans konuları ihtiyaç duyan işiniz için el ile bellek ayırabilir ve hello CPU gerekli core-sayısı toorun işinizi zamanında yaklaşık kaldırır odaklanmak bu kapasite sağlar.</span><span class="sxs-lookup"><span data-stu-id="63c31-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="63c31-109">Kaç tane SUs bir iş için gerekli?</span><span class="sxs-lookup"><span data-stu-id="63c31-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="63c31-110">Belirli bir proje için gerekli SUs Hello sayısını seçmeye hello bölüm yapılandırmasını hello girişleri ve hello iş içinde tanımlanan hello sorgu bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="63c31-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="63c31-111">Merhaba **ölçek** dikey verir tooset hello SUs sağ sayısı.</span><span class="sxs-lookup"><span data-stu-id="63c31-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="63c31-112">Bu, en iyi uygulamadır tooallocate gerekli olandan daha fazla SUs olur.</span><span class="sxs-lookup"><span data-stu-id="63c31-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="63c31-113">Merhaba Stream Analytics işleme altyapısı gecikme süresi ve ek bellek ayırma, hello maliyet verimliliği için en iyi duruma getirir.</span><span class="sxs-lookup"><span data-stu-id="63c31-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="63c31-114">Genel olarak, toostart kullanmayan sorgular için 6 SUs ile Merhaba en iyi uygulamalardan biridir *bölüm tarafından*.</span><span class="sxs-lookup"><span data-stu-id="63c31-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="63c31-115">Ardından hello Lezzetli nokta temsili miktarda veriyi geçirmek ve hello SU % kullanım ölçüm inceleyin sonra SUs hello sayısı değişiklik bir deneme yanılma yöntemi kullanarak belirler.</span><span class="sxs-lookup"><span data-stu-id="63c31-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="63c31-116">Azure Stream Analytics herhangi bir işlem başlatmadan önce hello "sipariş arabelleği" adlı bir pencerede olayları tutar.</span><span class="sxs-lookup"><span data-stu-id="63c31-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="63c31-117">Olayları hello sipariş pencereye zamanına göre sıralanır ve sonraki işlemleri geçici olarak sıralanmış hello olaylarına gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="63c31-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="63c31-118">Olayları zamanına göre yeniden sıralama sağlar hello işleç sahip tüm görünürlük hello hello olayda belirlenen zaman çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="63c31-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="63c31-119">Ayrıca hello gerekli işleme gerçekleştirmek ve bir çıktı oluşturmak hello işleci olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="63c31-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="63c31-120">Bu mekanizma yan etkisi, işleme hello sipariş penceresinde hello süreye göre gecikti ' dir.</span><span class="sxs-lookup"><span data-stu-id="63c31-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="63c31-121">Merhaba bellek alanını (, SU tüketim etkileyen) hello işin Bu sipariş penceresini açın ve hello içerdiği olayların sayısı hello boyutunun bir işlevdir.</span><span class="sxs-lookup"><span data-stu-id="63c31-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="63c31-122">Okuyucu Hello sayısını iş yükseltmeler sırasında değiştiğinde geçici uyarıları tooaudit günlüklerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="63c31-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="63c31-123">Akış analizi işleri, bu geçici sorunları otomatik olarak kurtarın.</span><span class="sxs-lookup"><span data-stu-id="63c31-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="63c31-124">İşlerini çalıştırmak için yüksek SU kullanımı yaygın yüksek bellek nedenleri</span><span class="sxs-lookup"><span data-stu-id="63c31-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="63c31-125">GROUP BY için yüksek kardinalite</span><span class="sxs-lookup"><span data-stu-id="63c31-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="63c31-126">gelen olayları Hello önemi hello işi için bellek kullanımını belirler.</span><span class="sxs-lookup"><span data-stu-id="63c31-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="63c31-127">Örneğin, `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello ilişkili numarası **kümelenmiş** hello nicelik hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="63c31-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="63c31-128">yüksek kardinalite tarafından neden toomitigate sorunları kullanan bölümler artırarak hello sorguyu dışarıya ölçeklendirme **bölüm tarafından**.</span><span class="sxs-lookup"><span data-stu-id="63c31-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="63c31-129">Merhaba sayısı *kümelenmiş* burada hello nicelik, GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="63c31-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="63c31-130">Merhaba sorgu bölümlenmiş sonra birden çok düğümleri üzerinde dağılmış.</span><span class="sxs-lookup"><span data-stu-id="63c31-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="63c31-131">Sonuç olarak, hangi sırayla hello hello sipariş arabellek boyutunu azaltır hello her düğümüne gelen olayların sayısı azalır.</span><span class="sxs-lookup"><span data-stu-id="63c31-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="63c31-132">Ayrıca PartitionID tarafından olay hub'ı bölümler bölüm.</span><span class="sxs-lookup"><span data-stu-id="63c31-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="63c31-133">BİRLEŞTİRME için yüksek eşleşmeyen olay sayısı</span><span class="sxs-lookup"><span data-stu-id="63c31-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="63c31-134">Merhaba birleştirme eşleşmeyen olayların sayısını hello sorgu hello bellek kullanımını etkiler.</span><span class="sxs-lookup"><span data-stu-id="63c31-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="63c31-135">Örneğin, tıklama oluşturan toofind hello ad izlenim sayısı arayan bir sorgu gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="63c31-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="63c31-136">Bu senaryoda, birçok ads gösterilir ve birkaç tıklatmayla oluşturulan mümkündür.</span><span class="sxs-lookup"><span data-stu-id="63c31-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="63c31-137">Böyle bir sonuç hello iş tookeep hello zaman penceresi içindeki tüm hello olayları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="63c31-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="63c31-138">Merhaba kullanılan bellek miktarına orantılı toohello pencere boyutu ve olay hızıdır.</span><span class="sxs-lookup"><span data-stu-id="63c31-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="63c31-139">toomitigate bölüm tarafından kullanarak bu durumda, artırarak hello sorgu genişletme bölümler.</span><span class="sxs-lookup"><span data-stu-id="63c31-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="63c31-140">Merhaba sorgu bölümlenmiş sonra birden çok işlem düğümleri üzerinde dağılmış.</span><span class="sxs-lookup"><span data-stu-id="63c31-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="63c31-141">Sonuç olarak, hangi sırayla hello hello sipariş arabellek boyutunu azaltır hello her düğümüne gelen olayların sayısı azalır.</span><span class="sxs-lookup"><span data-stu-id="63c31-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="63c31-142">Çok fazla sayıda bozuk olayı</span><span class="sxs-lookup"><span data-stu-id="63c31-142">Large number of out of order events</span></span> 

<span data-ttu-id="63c31-143">Çok sayıda bozuk olay büyük zaman penceresi içinde hello "arabellek yeniden sıralamak" toobe büyük hello boyutunu neden olur.</span><span class="sxs-lookup"><span data-stu-id="63c31-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="63c31-144">toomitigate bölüm tarafından kullanarak bu durumda, Ölçek hello sorgu artırarak bölümler.</span><span class="sxs-lookup"><span data-stu-id="63c31-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="63c31-145">Merhaba sorgu bölümlenmiş sonra birden çok düğümleri üzerinde dağılmış.</span><span class="sxs-lookup"><span data-stu-id="63c31-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="63c31-146">Sonuç olarak, hangi sırayla hello hello sipariş arabellek boyutunu azaltır hello her düğümüne gelen olayların sayısı azalır.</span><span class="sxs-lookup"><span data-stu-id="63c31-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="63c31-147">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="63c31-147">Get help</span></span>
<span data-ttu-id="63c31-148">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="63c31-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63c31-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63c31-149">Next steps</span></span>
* [<span data-ttu-id="63c31-150">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="63c31-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="63c31-151">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="63c31-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="63c31-152">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="63c31-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="63c31-153">Azure Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="63c31-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="63c31-154">Azure Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="63c31-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
