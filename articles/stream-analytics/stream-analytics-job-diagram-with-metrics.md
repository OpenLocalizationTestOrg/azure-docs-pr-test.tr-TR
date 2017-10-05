---
title: "Azure akış veri temelli iş diyagramı kullanarak hata ayıklama analizi | Microsoft Docs"
description: "Stream Analytics işiniz iş diyagramı ve ölçümleri kullanarak sorun giderin."
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
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="aef80-103">Veri temelli iş diyagramı kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="aef80-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="aef80-104">İş diyagramı **izleme** dikey Azure portalında iş hattınızı görselleştirmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="aef80-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="aef80-105">Giriş, çıkış ve sorgu adımları gösterir.</span><span class="sxs-lookup"><span data-stu-id="aef80-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="aef80-106">Her adım sorunları giderirken daha hızlı bir sorunun kaynağını yalıtmak için ölçümleri incelemek için iş diyagramı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aef80-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="aef80-107">İş diyagramı kullanma</span><span class="sxs-lookup"><span data-stu-id="aef80-107">Using the job diagram</span></span>

<span data-ttu-id="aef80-108">Azure portalında altında bir Stream Analytics işinde while **destek + sorun giderme**seçin **iş diyagramı**:</span><span class="sxs-lookup"><span data-stu-id="aef80-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Ölçümleri - konumu ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="aef80-110">Her sorgu adım bölmesinde düzenleme sorgu karşılık gelen bölümünde görmek için seçin.</span><span class="sxs-lookup"><span data-stu-id="aef80-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="aef80-111">Adım için bir ölçüm grafik sayfasında alt bölmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aef80-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![Ölçümleri - temel iş ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="aef80-113">Azure Event Hubs'a giriş bölümlerini görmek için seçin **...**</span><span class="sxs-lookup"><span data-stu-id="aef80-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="aef80-114">Bir bağlam menüsü görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aef80-114">A context menu appears.</span></span> <span data-ttu-id="aef80-115">Giriş birleşme de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aef80-115">You also can see the input merger.</span></span>

![Diyagram ölçümlerle iş - bölümü genişletin](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="aef80-117">Yalnızca tek bir bölüm için ölçüm grafik görmek için bölüm düğümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="aef80-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="aef80-118">Ölçümleri sayfasının en altında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="aef80-118">The metrics are shown at the bottom of the page.</span></span>

![Ölçümleri - daha fazla ölçümleri ile iş diyagramı](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="aef80-120">Bir birleşme ölçümleri grafik görmek için birleşme düğümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="aef80-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="aef80-121">Aşağıdaki grafikte hiçbir olay bırakılan veya ayarlanmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="aef80-121">The following chart shows that no events were dropped or adjusted.</span></span>

![İş diyagramı - ölçümlerle kılavuz](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="aef80-123">Saat ve ölçüm değeri ayrıntılarını görmek için grafik üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="aef80-123">To see the details of the metric value and time, point to the chart.</span></span>

![Diyagram ölçümlerle iş - getirin](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="aef80-125">Ölçümleri kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="aef80-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="aef80-126">**QueryLastProcessedTime** ölçüm, belirli bir adıma veri alındığında gösterir.</span><span class="sxs-lookup"><span data-stu-id="aef80-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="aef80-127">Topoloji bakarak, hangi adımın veri almıyor görmek için çıkış işlemcisine geriye doğru çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="aef80-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="aef80-128">Bir adım veri alamıyorsanız, hemen önce sorgu adıma gidin.</span><span class="sxs-lookup"><span data-stu-id="aef80-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="aef80-129">Önceki sorgu adımı bir zaman penceresi sahip olup olmadığını belirler ve yeterli bir süre için çıktı verilerini geçti olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="aef80-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="aef80-130">(Windows saate tutturulur Not bundan.)</span><span class="sxs-lookup"><span data-stu-id="aef80-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="aef80-131">Önceki sorgu adımı Giriş bir işlemci ise, giriş ölçümleri yanıt yardımcı olması için aşağıdaki hedeflenen soruları kullanın.</span><span class="sxs-lookup"><span data-stu-id="aef80-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="aef80-132">Bunlar, bir iş giriş kaynaklardan veri alma olup olmadığını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="aef80-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="aef80-133">Sorgu bölümlendirilmişse her bir bölümü inceleyin.</span><span class="sxs-lookup"><span data-stu-id="aef80-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="aef80-134">Ne kadar veri okunan?</span><span class="sxs-lookup"><span data-stu-id="aef80-134">How much data is being read?</span></span>

*   <span data-ttu-id="aef80-135">**InputEventsSourcesTotal** okuma veri birimleri sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="aef80-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="aef80-136">Örneğin, BLOB sayısı.</span><span class="sxs-lookup"><span data-stu-id="aef80-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="aef80-137">**InputEventsTotal** okuma olay sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="aef80-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="aef80-138">Bu ölçüm her bölüm için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aef80-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="aef80-139">**InputEventsInBytesTotal** okunan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="aef80-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="aef80-140">**InputEventsLastArrivalTime** alınan her olayın sıraya alınan saatiyle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="aef80-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="aef80-141">Zaman ilerleyen?</span><span class="sxs-lookup"><span data-stu-id="aef80-141">Is time moving forward?</span></span> <span data-ttu-id="aef80-142">Gerçek olayları okuyorsanız noktalama verilen değil.</span><span class="sxs-lookup"><span data-stu-id="aef80-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="aef80-143">**InputEventsLastPunctuationTime**, zamanın ilerlemesini sağlamak için bir noktalama işaretinin ne zaman verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="aef80-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="aef80-144">Noktalama işaretleri verilmemiş, veri akışı engellenen.</span><span class="sxs-lookup"><span data-stu-id="aef80-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="aef80-145">Girdide hataları var mı?</span><span class="sxs-lookup"><span data-stu-id="aef80-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="aef80-146">**InputEventsEventDataNullTotal** null veri olayları sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="aef80-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="aef80-147">**InputEventsSerializerErrorsTotal** doğru serisi kaldırılamadı olayların sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="aef80-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="aef80-148">**InputEventsDegradedTotal** seri durumdan çıkarma dışında bir sorunla olayların sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="aef80-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="aef80-149">Olayları bırakılan veya ayarlanmış misiniz?</span><span class="sxs-lookup"><span data-stu-id="aef80-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="aef80-150">**InputEventsEarlyTotal** yüksek Filigran önce bir uygulama zaman damgası olan olayları sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="aef80-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="aef80-151">**InputEventsLateTotal** yüksek Filigran sonra bir uygulama zaman damgası olan olayları sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="aef80-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="aef80-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** iş başlangıç saatinden önce bırakılan sayı olayı.</span><span class="sxs-lookup"><span data-stu-id="aef80-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="aef80-153">Biz veri okuma dönmeden?</span><span class="sxs-lookup"><span data-stu-id="aef80-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="aef80-154">**InputEventsSourcesBackloggedTotal** olay hub'ları ve Azure IOT Hub girdileri okumak kaç tane daha fazla ileti gereksinim söyler.</span><span class="sxs-lookup"><span data-stu-id="aef80-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="aef80-155">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="aef80-155">Get help</span></span>
<span data-ttu-id="aef80-156">Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="aef80-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aef80-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aef80-157">Next steps</span></span>
* [<span data-ttu-id="aef80-158">Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="aef80-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="aef80-159">Stream Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="aef80-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="aef80-160">Stream Analytics işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="aef80-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="aef80-161">Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="aef80-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="aef80-162">Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="aef80-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
