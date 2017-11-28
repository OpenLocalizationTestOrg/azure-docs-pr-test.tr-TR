---
title: "Ayrıca Azure akış analizi veri güdümlü hello iş diyagramı kullanarak hata ayıklama | Microsoft Docs"
description: "Stream Analytics işiniz hello iş diyagramı ve ölçümleri kullanarak sorun giderin."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="92c9c-103">Veri temelli hello iş diyagramı kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="92c9c-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="92c9c-104">Merhaba iş hello diyagramda **izleme** dikey penceresinde hello Azure portal iş hattınızı görselleştirmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="92c9c-105">Giriş, çıkış ve sorgu adımları gösterir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="92c9c-106">Toomore sorunları giderirken bir sorunun hello kaynağını hızlı bir şekilde ayırmak, her adımı için hello iş diyagramı tooexamine hello ölçümleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c9c-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="92c9c-107">Merhaba iş diyagramı kullanma</span><span class="sxs-lookup"><span data-stu-id="92c9c-107">Using hello job diagram</span></span>

<span data-ttu-id="92c9c-108">Hello Azure portal'ın altında bir Stream Analytics işinde while **destek + sorun giderme**seçin **iş diyagramı**:</span><span class="sxs-lookup"><span data-stu-id="92c9c-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Ölçümleri - konumu ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="92c9c-110">Her sorgu adım toosee hello karşılık gelen bölüm bölmesinde düzenleme sorguda seçin.</span><span class="sxs-lookup"><span data-stu-id="92c9c-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="92c9c-111">Merhaba adım için bir ölçüm grafik hello sayfasında alt bölmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Ölçümleri - temel iş ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="92c9c-113">hello Azure Event Hubs'a giriş toosee hello bölümleri seçin **...**</span><span class="sxs-lookup"><span data-stu-id="92c9c-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="92c9c-114">Bir bağlam menüsü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-114">A context menu appears.</span></span> <span data-ttu-id="92c9c-115">Merhaba giriş birleşme de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c9c-115">You also can see hello input merger.</span></span>

![Diyagram ölçümlerle iş - bölümü genişletin](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="92c9c-117">yalnızca tek bir bölüm, select hello bölümü düğümü için toosee hello ölçüm grafik.</span><span class="sxs-lookup"><span data-stu-id="92c9c-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="92c9c-118">Merhaba ölçümleri hello sayfasının hello altında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Ölçümleri - daha fazla ölçümleri ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="92c9c-120">bir birleşme select hello birleşme düğümü için toosee hello ölçümleri grafik.</span><span class="sxs-lookup"><span data-stu-id="92c9c-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="92c9c-121">Grafik aşağıdaki hello hiçbir olay bırakılan veya ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![İş diyagramı - ölçümlerle kılavuz](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="92c9c-123">Merhaba ölçüm değer ve zaman noktası toohello grafik toosee hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="92c9c-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Diyagram ölçümlerle iş - getirin](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="92c9c-125">Ölçümleri kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="92c9c-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="92c9c-126">Merhaba **QueryLastProcessedTime** ölçüm, belirli bir adıma veri alındığında gösterir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="92c9c-127">Merhaba topoloji bakarak hello çıkış işlemci toosee hangi adımın veri almıyor geriye doğru çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="92c9c-128">Bir adımı veri alamıyorsanız, toohello sorgu adımı hemen önce gidin.</span><span class="sxs-lookup"><span data-stu-id="92c9c-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="92c9c-129">Merhaba önceki sorgu adımı bir zaman penceresi olup olmadığını ve bunun için yeterli süre geçtiyse denetleyin toooutput veri.</span><span class="sxs-lookup"><span data-stu-id="92c9c-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="92c9c-130">(Windows açıldı toohello saat olan Not bundan.)</span><span class="sxs-lookup"><span data-stu-id="92c9c-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="92c9c-131">Merhaba önceki sorgu adımı bir giriş işlemci ise, hedeflenen sorular aşağıdaki hello giriş ölçümleri toohelp yanıt hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="92c9c-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="92c9c-132">Bunlar, bir iş giriş kaynaklardan veri alma olup olmadığını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="92c9c-133">Merhaba sorgu bölümlenmiş varsa her bölüm inceleyin.</span><span class="sxs-lookup"><span data-stu-id="92c9c-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="92c9c-134">Ne kadar veri okunan?</span><span class="sxs-lookup"><span data-stu-id="92c9c-134">How much data is being read?</span></span>

*   <span data-ttu-id="92c9c-135">**InputEventsSourcesTotal** okuma veri birimleri hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="92c9c-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="92c9c-136">Örneğin, BLOB sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="92c9c-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="92c9c-137">**InputEventsTotal** okuma olay hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="92c9c-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="92c9c-138">Bu ölçüm her bölüm için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="92c9c-139">**InputEventsInBytesTotal** hello okunan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="92c9c-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="92c9c-140">**InputEventsLastArrivalTime** alınan her olayın sıraya alınan saatiyle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="92c9c-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="92c9c-141">Zaman ilerleyen?</span><span class="sxs-lookup"><span data-stu-id="92c9c-141">Is time moving forward?</span></span> <span data-ttu-id="92c9c-142">Gerçek olayları okuyorsanız noktalama verilen değil.</span><span class="sxs-lookup"><span data-stu-id="92c9c-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="92c9c-143">**InputEventsLastPunctuationTime** tookeep zaman taşıma bir noktalama zaman verilmiş gösterir ilet.</span><span class="sxs-lookup"><span data-stu-id="92c9c-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="92c9c-144">Noktalama işaretleri verilmemiş, veri akışı engellenen.</span><span class="sxs-lookup"><span data-stu-id="92c9c-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="92c9c-145">Merhaba girişinde hataları var mı?</span><span class="sxs-lookup"><span data-stu-id="92c9c-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="92c9c-146">**InputEventsEventDataNullTotal** null veri olayları sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="92c9c-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="92c9c-147">**InputEventsSerializerErrorsTotal** doğru serisi kaldırılamadı olayların sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="92c9c-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="92c9c-148">**InputEventsDegradedTotal** seri durumdan çıkarma dışında bir sorunla olayların sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="92c9c-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="92c9c-149">Olayları bırakılan veya ayarlanmış misiniz?</span><span class="sxs-lookup"><span data-stu-id="92c9c-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="92c9c-150">**InputEventsEarlyTotal** hello yüksek Filigran önce bir uygulama zaman damgası olan olayları hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="92c9c-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="92c9c-151">**InputEventsLateTotal** hello yüksek Filigran sonra bir uygulama zaman damgası olan olayları hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="92c9c-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="92c9c-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** hello sayı olayı hello iş başlangıç saatinden önce bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="92c9c-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="92c9c-153">Biz veri okuma dönmeden?</span><span class="sxs-lookup"><span data-stu-id="92c9c-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="92c9c-154">**InputEventsSourcesBackloggedTotal** toobe kaç tane daha fazla ileti gereksinim söyler olay hub'ları ve Azure IOT Hub girdileri okuyun.</span><span class="sxs-lookup"><span data-stu-id="92c9c-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="92c9c-155">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="92c9c-155">Get help</span></span>
<span data-ttu-id="92c9c-156">Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="92c9c-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="92c9c-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92c9c-157">Next steps</span></span>
* [<span data-ttu-id="92c9c-158">Giriş tooStream analizi</span><span class="sxs-lookup"><span data-stu-id="92c9c-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="92c9c-159">Stream Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="92c9c-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="92c9c-160">Stream Analytics işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="92c9c-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="92c9c-161">Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="92c9c-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="92c9c-162">Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="92c9c-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
