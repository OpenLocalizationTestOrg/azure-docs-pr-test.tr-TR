---
title: "aaaUnderstanding Stream Analytics işi izleme | Microsoft Docs"
description: "Akış analizi işi izleme anlama"
keywords: Sorgu izlemesi
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="a29ad-104">Akış analizi işi izleme anlamak ve nasıl toomonitor sorguları</span><span class="sxs-lookup"><span data-stu-id="a29ad-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="a29ad-105">Giriş: hello izleme sayfası</span><span class="sxs-lookup"><span data-stu-id="a29ad-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="a29ad-106">Merhaba kullanılan toomonitor ve sorgu ve iş performans sorunlarını giderme temel performans ölçümlerini yüzey hem de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a29ad-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="a29ad-107">toosee bu ölçümleri gözatmak için ölçümleri ve görünüm hello görmeniz ilginizi toohello Stream Analytics işi **izleme** hello genel bakış sayfasında bölüm.</span><span class="sxs-lookup"><span data-stu-id="a29ad-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Bağlantı izleme](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="a29ad-109">Merhaba penceresinde gösterildiği gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="a29ad-109">hello window will appear as shown:</span></span>

![İzleme işi Panosu](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="a29ad-111">Akış analizi için kullanılabilir ölçümleri</span><span class="sxs-lookup"><span data-stu-id="a29ad-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="a29ad-112">Ölçüm</span><span class="sxs-lookup"><span data-stu-id="a29ad-112">Metric</span></span>                 | <span data-ttu-id="a29ad-113">Tanım</span><span class="sxs-lookup"><span data-stu-id="a29ad-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="a29ad-114">SU % kullanımı</span><span class="sxs-lookup"><span data-stu-id="a29ad-114">SU % Utilization</span></span>       | <span data-ttu-id="a29ad-115">Merhaba Hello kullanımı akış birimi hello ölçek sekmesinden hello işin tooa iş atanır.</span><span class="sxs-lookup"><span data-stu-id="a29ad-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="a29ad-116">Bu gösterge % 80 ulaşmalıdır ya da yukarıdaki mevcut olay işleme gecikebilir veya ilerleme durduruldu yüksek olasılık.</span><span class="sxs-lookup"><span data-stu-id="a29ad-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="a29ad-117">Giriş olayları</span><span class="sxs-lookup"><span data-stu-id="a29ad-117">Input Events</span></span>           | <span data-ttu-id="a29ad-118">Olayların sayısını de hello Stream Analytics işinde tarafından alınan veri miktarı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="a29ad-119">Bu olaylar toohello giriş kaynağı gönderilme kullanılan toovalidate olabilir.</span><span class="sxs-lookup"><span data-stu-id="a29ad-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="a29ad-120">Çıkış olayları</span><span class="sxs-lookup"><span data-stu-id="a29ad-120">Output Events</span></span>          | <span data-ttu-id="a29ad-121">Merhaba Stream Analytics işi toohello çıkış hedef olayların sayısı tarafından gönderilen veri miktarı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="a29ad-122">Düzen dışı olayları</span><span class="sxs-lookup"><span data-stu-id="a29ad-122">Out-of-Order Events</span></span>    | <span data-ttu-id="a29ad-123">Bırakılan veya olay sıralama İlkesi hello üzerinde temel ayarlanmış bir zaman damgası, verilen sıra dışında alınan olayların sayısı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="a29ad-124">Bu hello sırası tolerans penceresi ayarı hello yapılandırması tarafından etkilenebilir.</span><span class="sxs-lookup"><span data-stu-id="a29ad-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="a29ad-125">Veri dönüştürme hataları</span><span class="sxs-lookup"><span data-stu-id="a29ad-125">Data Conversion Errors</span></span> | <span data-ttu-id="a29ad-126">Akış analizi işi tarafından oluşturulan veri dönüştürme hatası sayısı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="a29ad-127">Çalışma zamanı hataları</span><span class="sxs-lookup"><span data-stu-id="a29ad-127">Runtime Errors</span></span>         | <span data-ttu-id="a29ad-128">Akış analizi işi yürütme sırasında gerçekleşecek hatalarının toplam sayısını Hello.</span><span class="sxs-lookup"><span data-stu-id="a29ad-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="a29ad-129">Geç giriş olayları</span><span class="sxs-lookup"><span data-stu-id="a29ad-129">Late Input Events</span></span>      | <span data-ttu-id="a29ad-130">Merhaba olay sıralama İlkesi yapılandırmasına göre hello geç gerçekleşme tolerans penceresi ayarı ya da bırakılan hello kaynak ya da kendi zaman damgası geç gelen olayların sayısının ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="a29ad-131">İşlev istekleri</span><span class="sxs-lookup"><span data-stu-id="a29ad-131">Function Requests</span></span>      | <span data-ttu-id="a29ad-132">Çağrıları toohello Azure Machine Learning işlevi (varsa) sayısı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="a29ad-133">Başarısız işleve istekleri</span><span class="sxs-lookup"><span data-stu-id="a29ad-133">Failed Function Requests</span></span> | <span data-ttu-id="a29ad-134">Başarısız Azure Machine Learning işlev çağrıları (varsa) sayısı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="a29ad-135">İşlev olayları</span><span class="sxs-lookup"><span data-stu-id="a29ad-135">Function Events</span></span>        | <span data-ttu-id="a29ad-136">Olay sayısı, (varsa) toohello Azure Machine Learning işlevi gönderdi.</span><span class="sxs-lookup"><span data-stu-id="a29ad-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="a29ad-137">Giriş olayı bayt</span><span class="sxs-lookup"><span data-stu-id="a29ad-137">Input Event Bytes</span></span>      | <span data-ttu-id="a29ad-138">Bayt cinsinden hello akış analizi işi tarafından alınan veri miktarı.</span><span class="sxs-lookup"><span data-stu-id="a29ad-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="a29ad-139">Bu olaylar toohello giriş kaynağı gönderilme kullanılan toovalidate olabilir.</span><span class="sxs-lookup"><span data-stu-id="a29ad-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="a29ad-140">İzleme hello Azure portalını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a29ad-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="a29ad-141">Grafik, gösterilen ölçümleri hello türünü ayarlayın ve hello grafiği Düzenle ayarları aralığında saat.</span><span class="sxs-lookup"><span data-stu-id="a29ad-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="a29ad-142">Ayrıntılar için bkz [nasıl tooCustomize izleme](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="a29ad-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Sorgu izleme saati grafiği](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="a29ad-144">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="a29ad-144">Get help</span></span>
<span data-ttu-id="a29ad-145">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="a29ad-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a29ad-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a29ad-146">Next steps</span></span>
* [<span data-ttu-id="a29ad-147">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="a29ad-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a29ad-148">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a29ad-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a29ad-149">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="a29ad-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a29ad-150">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a29ad-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a29ad-151">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a29ad-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

