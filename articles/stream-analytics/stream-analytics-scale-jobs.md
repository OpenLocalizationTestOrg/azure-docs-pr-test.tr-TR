---
title: "aaaScale Stream Analytics işleri tooincrease işleme | Microsoft Docs"
description: "Akış birimleri nasıl giriş bölümlerini yapılandırma, hello sorgu tanımı ayarlama ve ayarlayarak tooscale akış analizi işleri iş öğrenin."
keywords: "veri akış, veri işleme, akış analizi ayarlama"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="f00c5-104">Ölçek Azure akış analizi işleri tooincrease akış veri işleme işleme</span><span class="sxs-lookup"><span data-stu-id="f00c5-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="f00c5-105">Bu makalede nasıl tootune Stream Analytics sorgu tooincrease üretilen iş akış analizi işleri için gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="f00c5-106">Ayarlama hello analytics sorgu tanımı ve hesaplama ve ayarlama işi nasıl giriş bölümleri yapılandırarak tooscale Stream Analytics işleri öğrenin *akış birimleri* (SUs).</span><span class="sxs-lookup"><span data-stu-id="f00c5-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="f00c5-107">Akış analizi işi hello bölümlerini nelerdir?</span><span class="sxs-lookup"><span data-stu-id="f00c5-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="f00c5-108">Stream Analytics iş tanımı girişleri, sorgu ve çıktıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="f00c5-109">Burada hello iş hello veri akışından okuma girdileridir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="f00c5-110">Merhaba sorgu kullanılan tootransform hello veri giriş akışı ve hello çıktı hello işini hello iş sonuçları yere gönderir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="f00c5-111">Bir işi veri akış için en az bir giriş kaynağı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="f00c5-112">Merhaba veri akışı giriş kaynağı Azure event hub'ındaki veya Azure blob depolama alanındaki depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="f00c5-113">Daha fazla bilgi için bkz: [giriş tooAzure Stream Analytics](stream-analytics-introduction.md) ve [Azure Stream Analytics ile çalışmaya başlamak](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="f00c5-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="f00c5-114">Bölümler event hubs'a ve Azure depolama</span><span class="sxs-lookup"><span data-stu-id="f00c5-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="f00c5-115">Akış analizi işi ölçeklendirme bölümleri giriş veya çıkış hello yararlanır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="f00c5-116">Bir bölüm anahtarına göre alt kümeleri veri bölmek sağlar bölümleme.</span><span class="sxs-lookup"><span data-stu-id="f00c5-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="f00c5-117">Merhaba verileri (örneğin, bir akış analizi işine) kullanır bir işlem kullanabilir ve verimliliğini artırır paralel olarak farklı bölümleri yazma.</span><span class="sxs-lookup"><span data-stu-id="f00c5-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="f00c5-118">Akış Analizi ile çalışırken, olay hub'ları ve Blob Depolama bölümlendirme, yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f00c5-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="f00c5-119">Bölümleri hakkında daha fazla bilgi için aşağıdaki makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="f00c5-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="f00c5-120">Olay hub'ları özelliklere genel bakış</span><span class="sxs-lookup"><span data-stu-id="f00c5-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="f00c5-121">Veri bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="f00c5-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="f00c5-122">Akış birimleri (SUs)</span><span class="sxs-lookup"><span data-stu-id="f00c5-122">Streaming units (SUs)</span></span>
<span data-ttu-id="f00c5-123">Akış birimleri (SUs) temsil eder hello kaynakları ve gereken gücünün tooexecute bir Azure akış analizi işi sipariş.</span><span class="sxs-lookup"><span data-stu-id="f00c5-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="f00c5-124">SUs kapasite CPU, bellek, karışık bir ölçüyü temel bir şekilde toodescribe hello göreli olay işleme sağlamak ve okuma ve oranları yazma.</span><span class="sxs-lookup"><span data-stu-id="f00c5-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="f00c5-125">Her SU tooroughly karşılık gelen 1 MB/sn'ye saniye.</span><span class="sxs-lookup"><span data-stu-id="f00c5-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="f00c5-126">Kaç tane SUs seçme hello girişleri için hello bölüm yapılandırmasını ve hello sorgu hello iş için tanımlanan belirli bir işin bağlıdır için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="f00c5-127">SUs tooyour kota bir iş için yukarı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f00c5-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="f00c5-128">Varsayılan olarak, her Azure aboneliğinin kotası too50 SUs tüm hello analytics işleri yukarı belirli bir bölgede sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="f00c5-129">Bu kota, kişi ötesinde, abonelikler için SUs tooincrease [Microsoft Support](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f00c5-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="f00c5-130">İş başına SUs için geçerli değerler: 1, 3, 6 ve 6'ın artışlarla yukarı.</span><span class="sxs-lookup"><span data-stu-id="f00c5-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="f00c5-131">Utandırıcı derecede paralel işi</span><span class="sxs-lookup"><span data-stu-id="f00c5-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="f00c5-132">Bir *utandırıcı derecede paralel* iş hello en ölçeklenebilir senaryo Azure akış analizi sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f00c5-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="f00c5-133">Bir bölüm hello sorgu tooone bölümünün hello çıktı hello giriş tooone örneğinin bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="f00c5-134">Bu paralellik hello gereksinimlerine sahiptir:</span><span class="sxs-lookup"><span data-stu-id="f00c5-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="f00c5-135">Sorgu mantığınızı aynı anahtar işlenmekte olan hello üzerinde bağımlıysa hello tarafından aynı örnek sorgu, hello olayları toohello Git emin olmanız gerekir, giriş aynı bölüm.</span><span class="sxs-lookup"><span data-stu-id="f00c5-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="f00c5-136">Olay hub'ları için bu hello olay verilerini hello olmalıdır anlamına gelir **PartitionKey** değerinin ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="f00c5-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="f00c5-137">Alternatif olarak, bölümlenmiş Gönderenler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f00c5-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="f00c5-138">BLOB Depolama için bu hello olayları toohello gönderilir anlamına gelir aynı bölüm klasör.</span><span class="sxs-lookup"><span data-stu-id="f00c5-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="f00c5-139">Sorgu mantığınızı aynı işlenen toobe anahtarın hello gerektirmiyorsa hello tarafından aynı örnek sorgu, bu gereksinimin göz ardı edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f00c5-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="f00c5-140">Bu mantık örneği basit bir select proje filtresi sorgu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="f00c5-141">Merhaba veriler hello giriş tarafında düzenlendiğini sonra sorgunuzu bölümlenen emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="f00c5-142">Bu toouse gerektirir **bölüm tarafından** tüm hello adımlarda.</span><span class="sxs-lookup"><span data-stu-id="f00c5-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="f00c5-143">Birden çok adımı izin verilir, ancak hepsi tarafından hello bölümlenmiş gerekir aynı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="f00c5-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="f00c5-144">Şu anda, bölümlendirme anahtarı hello çok ayarlanmalıdır**PartitionID** hello iş toobe tam olarak paralel sırayla.</span><span class="sxs-lookup"><span data-stu-id="f00c5-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="f00c5-145">Şu anda yalnızca olay hub'ları ve blob depolama bölümlenmiş çıkış destekler.</span><span class="sxs-lookup"><span data-stu-id="f00c5-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="f00c5-146">Olay hub'ı çıkışı için hello bölüm anahtarı toobe yapılandırmalısınız **PartitionID**.</span><span class="sxs-lookup"><span data-stu-id="f00c5-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="f00c5-147">BLOB Depolama çıktı için toodo herhangi bir şey yok.</span><span class="sxs-lookup"><span data-stu-id="f00c5-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="f00c5-148">Giriş bölüm sayısı Hello hello çıkış bölüm sayısı eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="f00c5-149">BLOB Depolama çıkış bölümleri şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="f00c5-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="f00c5-150">Ancak hello Yukarı Akış sorgusunun bölümleme hello devralır Tamam, olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="f00c5-151">Örnek bir tam olarak paralel iş izin bölüm değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f00c5-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="f00c5-152">8 olay hub'ı giriş bölümleri ve 8 olay hub'ı bölümleri çıkış</span><span class="sxs-lookup"><span data-stu-id="f00c5-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="f00c5-153">8 olay hub'ı giriş bölümleri ve blob depolama çıktı</span><span class="sxs-lookup"><span data-stu-id="f00c5-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="f00c5-154">8 blob depolama giriş bölümleri ve blob depolama çıkış</span><span class="sxs-lookup"><span data-stu-id="f00c5-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="f00c5-155">Depolama giriş bölümleri ve 8 olay hub'ı çıkış bölümleri 8 blob</span><span class="sxs-lookup"><span data-stu-id="f00c5-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="f00c5-156">Merhaba aşağıdaki bölümlerde utandırıcı derecede paralel bazı örnek senaryolar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="f00c5-157">Basit Sorgu</span><span class="sxs-lookup"><span data-stu-id="f00c5-157">Simple query</span></span>

* <span data-ttu-id="f00c5-158">Giriş: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f00c5-159">Çıktı: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="f00c5-160">Sorgu:</span><span class="sxs-lookup"><span data-stu-id="f00c5-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="f00c5-161">Bu sorgu basit bir filtredir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-161">This query is a simple filter.</span></span> <span data-ttu-id="f00c5-162">Bu nedenle, event hub'ı toohello gönderilen hello giriş bölümleme hakkında tooworry gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f00c5-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="f00c5-163">Merhaba sorgulayan içerir dikkat edin **bölüm tarafından PartitionID**, gereksinimden #2 önceki yerine getirir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="f00c5-164">Merhaba çıktı için tooconfigure hello olay hub'ı çıkışı hello iş toohave hello bölümlendirmesini anahtar kümesi çok ihtiyacımız**PartitionID**.</span><span class="sxs-lookup"><span data-stu-id="f00c5-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="f00c5-165">Bir son denetimi toomake hello giriş bölüm sayısı eşit toohello çıkış bölüm sayısı olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="f00c5-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="f00c5-166">Gruplandırma anahtarı ile sorgulama</span><span class="sxs-lookup"><span data-stu-id="f00c5-166">Query with a grouping key</span></span>

* <span data-ttu-id="f00c5-167">Giriş: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f00c5-168">Çıktı: Blob storage'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-168">Output: Blob storage</span></span>

<span data-ttu-id="f00c5-169">Sorgu:</span><span class="sxs-lookup"><span data-stu-id="f00c5-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f00c5-170">Bu sorgu gruplandırma anahtarı yok.</span><span class="sxs-lookup"><span data-stu-id="f00c5-170">This query has a grouping key.</span></span> <span data-ttu-id="f00c5-171">Bu nedenle, aynı anahtar gereksinimlerini toobe aynı olayları toohello olay hub'ı bölümlenmiş bir şekilde gönderilmesi gerektiğini anlamına gelir örnek sorgu hello tarafından işlenen hello.</span><span class="sxs-lookup"><span data-stu-id="f00c5-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="f00c5-172">Ancak, hangi anahtar kullanılmalıdır?</span><span class="sxs-lookup"><span data-stu-id="f00c5-172">But which key should be used?</span></span> <span data-ttu-id="f00c5-173">**PartitionID** bir iş mantığı kavramdır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="f00c5-174">Biz gerçekte çok önem verdiğiniz hello anahtarı **TollBoothId**, bu nedenle hello **PartitionKey** hello olay verilerini değeri olmalıdır **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="f00c5-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="f00c5-175">Merhaba sorguda ayarlayarak bunu **bölüm tarafından** çok**PartitionID**.</span><span class="sxs-lookup"><span data-stu-id="f00c5-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="f00c5-176">Merhaba çıkış blob depolama olduğundan, gereksinim #4 göre bir bölüm anahtarı değerini yapılandırma hakkında daha fazla tooworry gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f00c5-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="f00c5-177">Çok adımlı sorgusu gruplandırma anahtarı ile</span><span class="sxs-lookup"><span data-stu-id="f00c5-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="f00c5-178">Giriş: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f00c5-179">Çıktı: 8 bölümlerle olay hub'ı örneği</span><span class="sxs-lookup"><span data-stu-id="f00c5-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="f00c5-180">Sorgu:</span><span class="sxs-lookup"><span data-stu-id="f00c5-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f00c5-181">Bu sorgu gruplandırma anahtara sahip; bu nedenle aynı anahtar gereksinimlerini toobe hello tarafından işlenen hello aynı sorgu örneği.</span><span class="sxs-lookup"><span data-stu-id="f00c5-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="f00c5-182">Biz kullanabilirsiniz hello hello önceki örnekte olduğu gibi aynı stratejisi.</span><span class="sxs-lookup"><span data-stu-id="f00c5-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="f00c5-183">Bu durumda, hello sorgu birden fazla adım vardır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="f00c5-184">Her adım sahip **bölüm tarafından PartitionID**?</span><span class="sxs-lookup"><span data-stu-id="f00c5-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="f00c5-185">Evet, şekilde Hello sorgu #3 gereksinimini yerine getirir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="f00c5-186">Merhaba çıktı için tooset hello bölüm anahtarı çok ihtiyacımız**PartitionID**, daha önce bahsedildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="f00c5-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="f00c5-187">Ayrıca hello olduğunu görebiliriz aynı sayıda hello giriş bölümler.</span><span class="sxs-lookup"><span data-stu-id="f00c5-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="f00c5-188">Örnek senaryoların *değil* utandırıcı derecede paralel</span><span class="sxs-lookup"><span data-stu-id="f00c5-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="f00c5-189">Merhaba önceki bölümde utandırıcı derecede paralel bazı senaryolar gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="f00c5-190">Bu bölümde, tüm başlangıç gereksinimlerini toobe utandırıcı derecede paralel uymayan senaryolar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="f00c5-191">Uyuşmayan bölüm sayısı</span><span class="sxs-lookup"><span data-stu-id="f00c5-191">Mismatched partition count</span></span>
* <span data-ttu-id="f00c5-192">Giriş: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f00c5-193">Çıkış: Olay hub'ı 32 bölümlerle</span><span class="sxs-lookup"><span data-stu-id="f00c5-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="f00c5-194">Bu durumda, önemli değildir hangi hello sorgudur.</span><span class="sxs-lookup"><span data-stu-id="f00c5-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="f00c5-195">Merhaba giriş bölüm sayısı hello çıkış bölüm sayısı eşleşmiyorsa, hello topoloji utandırıcı derecede paralel değil.</span><span class="sxs-lookup"><span data-stu-id="f00c5-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="f00c5-196">Olay hub'ları veya blob depolama çıkış olarak kullanan değil</span><span class="sxs-lookup"><span data-stu-id="f00c5-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="f00c5-197">Giriş: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f00c5-198">Çıkış: Powerbı</span><span class="sxs-lookup"><span data-stu-id="f00c5-198">Output: PowerBI</span></span>

<span data-ttu-id="f00c5-199">Powerbı çıkış bölümleme şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="f00c5-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="f00c5-200">Bu nedenle, bu senaryo utandırıcı derecede paralel değil.</span><span class="sxs-lookup"><span data-stu-id="f00c5-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="f00c5-201">Çok adımlı sorgu bölüm tarafından farklı değerlere sahip</span><span class="sxs-lookup"><span data-stu-id="f00c5-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="f00c5-202">Giriş: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="f00c5-203">Çıktı: 8 bölümlerle olay hub'ı</span><span class="sxs-lookup"><span data-stu-id="f00c5-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="f00c5-204">Sorgu:</span><span class="sxs-lookup"><span data-stu-id="f00c5-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="f00c5-205">Gördüğünüz gibi hello ikinci adımı kullanan **TollBoothId** bölümlendirme anahtarı hello olarak.</span><span class="sxs-lookup"><span data-stu-id="f00c5-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="f00c5-206">Bu adım olan değil hello aynı hello ilk adım olarak ve bu nedenle bize toodo bir karışık gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="f00c5-207">Önceki örneklerde utandırıcı derecede paralel bir topoloji çok uygun (veya yok) bazı Stream Analytics işleri hello.</span><span class="sxs-lookup"><span data-stu-id="f00c5-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="f00c5-208">Uygun değilse, bunlar en fazla ölçek hello potansiyeline sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="f00c5-209">Kılavuzu ölçeklendirme bu profillerinden birini uymayan işleri gelecekte kullanılabilecek yönelik güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="f00c5-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="f00c5-210">Şimdilik, hello genel rehberlik hello aşağıdaki bölümleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f00c5-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="f00c5-211">Merhaba maksimum akış birimleri, bir işin Hesapla</span><span class="sxs-lookup"><span data-stu-id="f00c5-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="f00c5-212">Hello toplam akış analizi işi tarafından kullanılan akış birim sayısını hello iş ve her adımı için bölüm hello sayısı için tanımlanan hello sorgusu adımlarda hello sayısına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="f00c5-213">Sorguda adımları</span><span class="sxs-lookup"><span data-stu-id="f00c5-213">Steps in a query</span></span>
<span data-ttu-id="f00c5-214">Sorguda bir veya daha fazla adım olabilir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-214">A query can have one or many steps.</span></span> <span data-ttu-id="f00c5-215">Her bir adımdır hello tarafından tanımlanan alt sorgu **ile** anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="f00c5-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="f00c5-216">Merhaba dışında hello sorgu **ile** anahtar sözcüğü (yalnızca bir sorgu) hello gibi bir adım olarak ayrıca sayılan **seçin** sorgu aşağıdaki hello deyiminde:</span><span class="sxs-lookup"><span data-stu-id="f00c5-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="f00c5-217">Bu sorgu iki adımı vardır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="f00c5-218">Bu sorgu hello makalenin sonraki bölümlerinde daha ayrıntılı ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="f00c5-219">Bir adımı bölüm</span><span class="sxs-lookup"><span data-stu-id="f00c5-219">Partition a step</span></span>
<span data-ttu-id="f00c5-220">Bir adımı bölümleme hello aşağıdaki koşulları gerektirir:</span><span class="sxs-lookup"><span data-stu-id="f00c5-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="f00c5-221">Merhaba giriş kaynağı bölümlenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="f00c5-222">Merhaba **seçin** hello sorgu deyimi bölümlenmiş bir giriş kaynağından okuma gerekir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="f00c5-223">Merhaba adım Hello sorguyla hello olmalıdır **bölüm tarafından** anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="f00c5-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="f00c5-224">Bir sorgu bölümlenmiş hello giriş işlenen ve toplu olarak ayrı bölüm grupları olaylardır ve çıkışları olayları hello gruplarının her biri için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f00c5-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="f00c5-225">Birleştirilmiş bir toplama istiyorsanız, ikinci bir adım bölümlenmemiş tooaggregate oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="f00c5-226">Akış birimleri işi için hello en fazla Hesapla</span><span class="sxs-lookup"><span data-stu-id="f00c5-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="f00c5-227">Tüm bölümlenmemiş adımları birlikte Yukarı Akış birimleri (SUs) Stream Analytics işi için toosix ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f00c5-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="f00c5-228">tooadd SUs, bir adım bölümlenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="f00c5-229">Her bölüm altı SUs olabilir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="f00c5-230">Sorgu</span><span class="sxs-lookup"><span data-stu-id="f00c5-230">Query</span></span></th><th><span data-ttu-id="f00c5-231">Merhaba işi için en çok SUs</span><span class="sxs-lookup"><span data-stu-id="f00c5-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="f00c5-232">Merhaba sorgu bir adım içerir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="f00c5-233">Merhaba adım bölümlenmiş değil.</span><span class="sxs-lookup"><span data-stu-id="f00c5-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f00c5-234">6</span><span class="sxs-lookup"><span data-stu-id="f00c5-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="f00c5-235">Merhaba giriş veri akışı 3 ile bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="f00c5-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="f00c5-236">Merhaba sorgu bir adım içerir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="f00c5-237">Merhaba adım bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="f00c5-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f00c5-238">18</span><span class="sxs-lookup"><span data-stu-id="f00c5-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="f00c5-239">Merhaba sorgu iki adımı içerir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="f00c5-240">Merhaba adımları hiçbiri bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="f00c5-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f00c5-241">6</span><span class="sxs-lookup"><span data-stu-id="f00c5-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="f00c5-242">Merhaba giriş veri akışı 3 ile bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="f00c5-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="f00c5-243">Merhaba sorgu iki adımı içerir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-243">hello query contains two steps.</span></span> <span data-ttu-id="f00c5-244">Merhaba giriş adım bölümlenmiş ve hello ikinci adım değildir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="f00c5-245">Merhaba <strong>seçin</strong> deyimi bölümlenmiş hello girişten okur.</span><span class="sxs-lookup"><span data-stu-id="f00c5-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="f00c5-246">24 (bölümlenmiş adımlar için 18) + bölümlenmemiş adımları için 6</span><span class="sxs-lookup"><span data-stu-id="f00c5-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="f00c5-247">Ölçeklendirme örnekleri</span><span class="sxs-lookup"><span data-stu-id="f00c5-247">Examples of scaling</span></span>

<span data-ttu-id="f00c5-248">Merhaba aşağıdaki sorguyu araba üç tollbooths sahip Ücretli istasyonu giderek üç dakikalık penceresinde hello sayısını hesaplar.</span><span class="sxs-lookup"><span data-stu-id="f00c5-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="f00c5-249">Bu sorgu SUs toosix genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f00c5-250">Daha fazla toouse SUs hello sorgu, her ikisi de giriş veri akışı hello ve hello sorgu bölümlenmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="f00c5-251">Merhaba veri akışı bölümü too3 ayarlandığından, hello aşağıdaki değiştirilmiş sorgu too18 SUs Genişletilebilir:</span><span class="sxs-lookup"><span data-stu-id="f00c5-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="f00c5-252">Bir sorgu bölümlenmiş, hello giriş olaylarını işlenir ve ayrı bölüm grupları bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="f00c5-253">Çıkış olayları da hello gruplarının her biri için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f00c5-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="f00c5-254">Bölümleme hello olduğunda bazı beklenmeyen sonuçlara neden olabilecek **GROUP BY** alan hello giriş veri akışında hello bölüm anahtarı değil.</span><span class="sxs-lookup"><span data-stu-id="f00c5-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="f00c5-255">Örneğin, hello **TollBoothId** hello önceki sorgu alanında hello bölüm anahtarı değil **Input1**.</span><span class="sxs-lookup"><span data-stu-id="f00c5-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="f00c5-256">Merhaba, gişe #1 verileri birden çok bölüm yayılabilir bu hello sonucudur.</span><span class="sxs-lookup"><span data-stu-id="f00c5-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="f00c5-257">Her hello **Input1** bölümleri işlenmeyecek ayrı olarak akış analizi tarafından.</span><span class="sxs-lookup"><span data-stu-id="f00c5-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="f00c5-258">Sonuç olarak, birden çok kayıt hello araba sayısı aynı atlayan pencere oluşturulacak hello içinde aynı gişe hello.</span><span class="sxs-lookup"><span data-stu-id="f00c5-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="f00c5-259">Merhaba giriş bölüm anahtarı değiştirilemez, bu sorun aşağıdaki örneğine hello gibi bir bölüm dışı adımı ekleyerek sabit:</span><span class="sxs-lookup"><span data-stu-id="f00c5-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="f00c5-260">Bu sorgu ölçeklendirilmiş too24 SUs olabilir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="f00c5-261">İki akışları birleştirilecekse toocreate hello birleştirmeler kullandığınız hello akışları tarafından hello sütunun hello bölüm anahtarı bölümlenir emin olun.</span><span class="sxs-lookup"><span data-stu-id="f00c5-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="f00c5-262">Ayrıca hello sahip olduğunuzdan emin olun hem akışları bölüm aynı sayısı.</span><span class="sxs-lookup"><span data-stu-id="f00c5-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="f00c5-263">Stream Analytics akış birimleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f00c5-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="f00c5-264">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f00c5-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f00c5-265">Kaynakları Hello listesinde tooscale istediğiniz ve açın hello Stream Analytics işi bulun.</span><span class="sxs-lookup"><span data-stu-id="f00c5-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="f00c5-266">Dikey penceresinde Hello altında iş **yapılandırma**, tıklatın **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="f00c5-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Azure portal Stream Analytics işi yapılandırma][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="f00c5-268">Merhaba kaydırıcı tooset hello SUs hello iş için kullanın.</span><span class="sxs-lookup"><span data-stu-id="f00c5-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="f00c5-269">Sınırlı toospecific SU ayarları olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f00c5-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="f00c5-270">İş performansını izleme</span><span class="sxs-lookup"><span data-stu-id="f00c5-270">Monitor job performance</span></span>
<span data-ttu-id="f00c5-271">Hello Azure portal kullanarak, bir işin hello verimlilik izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f00c5-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Azure Stream Analytics işleri izleme][img.stream.analytics.monitor.job]

<span data-ttu-id="f00c5-273">Merhaba iş yükünün beklenen hello verimliliği hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="f00c5-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="f00c5-274">Merhaba verimlilik beklenenden daha az ise, hello giriş bölümü ayarlamak, hello sorgu ayarlamak ve SUs tooyour iş ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f00c5-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="f00c5-275">Stream Analytics verimlilik ölçekte görselleştirmek: Merhaba Raspberry Pi'yi senaryosu</span><span class="sxs-lookup"><span data-stu-id="f00c5-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="f00c5-276">toohelp nasıl Stream Analytics işlerini ölçeklendirme anlamak, giriş Raspberry Pi'yi aygıttan dayalı bir denemeyi gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="f00c5-277">Bu deneme birden çok akış birimleri ile bölümleri verimini hello etkisini görmek bize.</span><span class="sxs-lookup"><span data-stu-id="f00c5-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="f00c5-278">Bu senaryoda, algılayıcı verileri (istemciler) tooan olay hub'ı hello aygıt gönderir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="f00c5-279">Analytics akış hello veri işler ve bir uyarı ya da istatistikleri çıktı tooanother olay hub ' gönderir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="f00c5-280">Merhaba istemci algılayıcı verileri JSON biçiminde gönderir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="f00c5-281">Merhaba veri çıkışı da JSON biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="f00c5-282">Merhaba veri şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f00c5-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="f00c5-283">bir açık kapalı olduğunda sorgu aşağıdaki hello kullanılan toosend bir uyarı değildir:</span><span class="sxs-lookup"><span data-stu-id="f00c5-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="f00c5-284">Ölçü işleme</span><span class="sxs-lookup"><span data-stu-id="f00c5-284">Measure throughput</span></span>

<span data-ttu-id="f00c5-285">Bu bağlamda verimlilik hello Sabit sürede akış analizi tarafından işlenen giriş veri miktarıdır.</span><span class="sxs-lookup"><span data-stu-id="f00c5-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="f00c5-286">(Biz 10 dakika cinsinden ölçülen.) tooachieve hello hello için en iyi işleme işleme giriş, giriş iki hello veri akışı ve hello sorgu bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="f00c5-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="f00c5-287">Biz dahil **COUNT()** hello sorgu toomeasure kaç tane giriş olaylarını işlendi.</span><span class="sxs-lookup"><span data-stu-id="f00c5-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="f00c5-288">toomake emin hello işi yalnızca giriş olaylarını toocome için beklediği değil, her bölüm hello giriş olay hub'ın yaklaşık 300 MB ile giriş verilerini önceden.</span><span class="sxs-lookup"><span data-stu-id="f00c5-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="f00c5-289">Merhaba aşağıdaki tabloda biz hello akış birim sayısını artar ve olay hub ' hello karşılık gelen bölüm sayar gördüğümüz hello sonuçları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f00c5-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="f00c5-290">Giriş bölümleri</span><span class="sxs-lookup"><span data-stu-id="f00c5-290">Input Partitions</span></span></th><th><span data-ttu-id="f00c5-291">Çıktı bölümleri</span><span class="sxs-lookup"><span data-stu-id="f00c5-291">Output Partitions</span></span></th><th><span data-ttu-id="f00c5-292">Akış Birimleri</span><span class="sxs-lookup"><span data-stu-id="f00c5-292">Streaming Units</span></span></th><th><span data-ttu-id="f00c5-293">Aralıksız üretilen</span><span class="sxs-lookup"><span data-stu-id="f00c5-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="f00c5-294">12</span><span class="sxs-lookup"><span data-stu-id="f00c5-294">12</span></span></td>
<td><span data-ttu-id="f00c5-295">12</span><span class="sxs-lookup"><span data-stu-id="f00c5-295">12</span></span></td>
<td><span data-ttu-id="f00c5-296">6</span><span class="sxs-lookup"><span data-stu-id="f00c5-296">6</span></span></td>
<td><span data-ttu-id="f00c5-297">4.06 MB/sn</span><span class="sxs-lookup"><span data-stu-id="f00c5-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f00c5-298">12</span><span class="sxs-lookup"><span data-stu-id="f00c5-298">12</span></span></td>
<td><span data-ttu-id="f00c5-299">12</span><span class="sxs-lookup"><span data-stu-id="f00c5-299">12</span></span></td>
<td><span data-ttu-id="f00c5-300">12</span><span class="sxs-lookup"><span data-stu-id="f00c5-300">12</span></span></td>
<td><span data-ttu-id="f00c5-301">8.06 MB/sn</span><span class="sxs-lookup"><span data-stu-id="f00c5-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f00c5-302">48</span><span class="sxs-lookup"><span data-stu-id="f00c5-302">48</span></span></td>
<td><span data-ttu-id="f00c5-303">48</span><span class="sxs-lookup"><span data-stu-id="f00c5-303">48</span></span></td>
<td><span data-ttu-id="f00c5-304">48</span><span class="sxs-lookup"><span data-stu-id="f00c5-304">48</span></span></td>
<td><span data-ttu-id="f00c5-305">38.32 MB/sn</span><span class="sxs-lookup"><span data-stu-id="f00c5-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f00c5-306">192</span><span class="sxs-lookup"><span data-stu-id="f00c5-306">192</span></span></td>
<td><span data-ttu-id="f00c5-307">192</span><span class="sxs-lookup"><span data-stu-id="f00c5-307">192</span></span></td>
<td><span data-ttu-id="f00c5-308">192</span><span class="sxs-lookup"><span data-stu-id="f00c5-308">192</span></span></td>
<td><span data-ttu-id="f00c5-309">172.67 MB/sn</span><span class="sxs-lookup"><span data-stu-id="f00c5-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f00c5-310">480</span><span class="sxs-lookup"><span data-stu-id="f00c5-310">480</span></span></td>
<td><span data-ttu-id="f00c5-311">480</span><span class="sxs-lookup"><span data-stu-id="f00c5-311">480</span></span></td>
<td><span data-ttu-id="f00c5-312">480</span><span class="sxs-lookup"><span data-stu-id="f00c5-312">480</span></span></td>
<td><span data-ttu-id="f00c5-313">454.27 MB/sn</span><span class="sxs-lookup"><span data-stu-id="f00c5-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="f00c5-314">720</span><span class="sxs-lookup"><span data-stu-id="f00c5-314">720</span></span></td>
<td><span data-ttu-id="f00c5-315">720</span><span class="sxs-lookup"><span data-stu-id="f00c5-315">720</span></span></td>
<td><span data-ttu-id="f00c5-316">720</span><span class="sxs-lookup"><span data-stu-id="f00c5-316">720</span></span></td>
<td><span data-ttu-id="f00c5-317">609.69 MB/sn</span><span class="sxs-lookup"><span data-stu-id="f00c5-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="f00c5-318">Ve hello aşağıdaki grafiği gösterir SUs ve işleme arasında hello ilişkinin bir görsel öğe.</span><span class="sxs-lookup"><span data-stu-id="f00c5-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.Stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="f00c5-320">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="f00c5-320">Get help</span></span>
<span data-ttu-id="f00c5-321">Daha fazla yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f00c5-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f00c5-322">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f00c5-322">Next steps</span></span>
* [<span data-ttu-id="f00c5-323">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="f00c5-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f00c5-324">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f00c5-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f00c5-325">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="f00c5-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f00c5-326">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="f00c5-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

