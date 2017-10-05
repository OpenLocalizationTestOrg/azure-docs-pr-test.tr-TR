---
title: "İşleme olayı sırası ve Azure akış Analizi ile lateness | Microsoft Docs"
description: "Stream Analytics veri akışında düzen dışı ya da geç olaylarla işleyişi hakkında bilgi edinin."
keywords: "bozuk, geç, olayları"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: a48e48c5fc65d0ffbb7c23f426a4b06dcd568821
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a><span data-ttu-id="84552-104">Azure Stream Analytics olay sipariş işleme</span><span class="sxs-lookup"><span data-stu-id="84552-104">Azure Stream Analytics event order handling</span></span>

<span data-ttu-id="84552-105">Olayları bir zamana bağlı veri akışında olayı alındığında süresiyle her olay kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="84552-105">In a temporal data stream of events, each event is recorded with the time that the event is received.</span></span> <span data-ttu-id="84552-106">Bazı koşullar, bazı olaylar bazen gönderildikleri farklı bir sırada almaya olay akışları neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="84552-106">Some conditions might cause event streams to occasionally receive some events in a different order than which they were sent.</span></span> <span data-ttu-id="84552-107">Bunun gerçekleşmesi için basit bir TCP yeniden aktarım ya da bile bir saat gönderen aygıtı ve alıcı olay hub'ı arasında kaymasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="84552-107">A simple TCP retransmit, or even a clock skew between the sending device and the receiving event hub might cause this to occur.</span></span> <span data-ttu-id="84552-108">"Noktalama" olayları olay varış yokluğu zamanında ilerletmek için alınan olay akışlar için de eklenir.</span><span class="sxs-lookup"><span data-stu-id="84552-108">“Punctuation” events also are added to received event streams, to advance the time in the absence of event arrivals.</span></span> <span data-ttu-id="84552-109">Bunlar "bildirim 3 dakika bana oturum yok olduğunda oluşur." gibi senaryolarda gerekli</span><span class="sxs-lookup"><span data-stu-id="84552-109">These are needed in scenarios like “Notify me when no logins occur for 3 minutes."</span></span>

<span data-ttu-id="84552-110">Sırayla olmayan giriş akışları ya da şunlardır:</span><span class="sxs-lookup"><span data-stu-id="84552-110">Input streams that are not in order are either:</span></span>
* <span data-ttu-id="84552-111">Sıralanmış (ve bu nedenle **Gecikmeli**).</span><span class="sxs-lookup"><span data-stu-id="84552-111">Sorted (and therefore **delayed**).</span></span>
* <span data-ttu-id="84552-112">Sistem tarafından bir kullanıcı tarafından belirtilen ilkesine göre ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="84552-112">Adjusted by the system, according to a user-specified policy.</span></span>


## <a name="lateness-tolerance"></a><span data-ttu-id="84552-113">Lateness dayanıklılık</span><span class="sxs-lookup"><span data-stu-id="84552-113">Lateness tolerance</span></span>
<span data-ttu-id="84552-114">Akış analizi, bu senaryo türlerini göstereceği.</span><span class="sxs-lookup"><span data-stu-id="84552-114">Stream Analytics tolerates these types of scenarios.</span></span> <span data-ttu-id="84552-115">Akış analizi "çıkış sıra" ve "geç" olayları için sahiptir.</span><span class="sxs-lookup"><span data-stu-id="84552-115">Stream Analytics has handling for "out-of-order" and "late" events.</span></span> <span data-ttu-id="84552-116">Bu olaylar aşağıdaki yollarla işlediği:</span><span class="sxs-lookup"><span data-stu-id="84552-116">It handles these events in the following ways:</span></span>

* <span data-ttu-id="84552-117">Sıranın dışında ancak kümesi tolerans dahilinde gelmesini olaylar **zaman damgası tarafından kaldırılmasında**.</span><span class="sxs-lookup"><span data-stu-id="84552-117">Events that arrive out of order but within the set tolerance are **reordered by timestamp**.</span></span>
* <span data-ttu-id="84552-118">Dayanıklılık daha sonra gelen olaylar **bırakılan veya ayarlanmış**.</span><span class="sxs-lookup"><span data-stu-id="84552-118">Events that arrive later than tolerance are **dropped or adjusted**.</span></span>
    * <span data-ttu-id="84552-119">**Ayarlanmış**: kabul edilebilir en son zaman gelmedi görünecek şekilde ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="84552-119">**Adjusted**: Adjusted to appear to have arrived at the latest acceptable time.</span></span>
    * <span data-ttu-id="84552-120">**Bırakılan**: atılır.</span><span class="sxs-lookup"><span data-stu-id="84552-120">**Dropped**: Discarded.</span></span>

![Stream Analytics olay işleme](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-the-number-of-out-of-order-events"></a><span data-ttu-id="84552-122">Düzen dışı olayların sayısını azaltın</span><span class="sxs-lookup"><span data-stu-id="84552-122">Reduce the number of out-of-order events</span></span>

<span data-ttu-id="84552-123">Stream Analytics (örneğin, pencerelenmiş toplamlar veya zamana bağlı birleştirmeler) gelen olayları işlerken zamana bağlı bir dönüşüm uygulandığından, Stream Analytics gelen olayları zaman damgası sırasına göre sıralar.</span><span class="sxs-lookup"><span data-stu-id="84552-123">Because Stream Analytics applies a temporal transformation when it processes incoming events (for example, for windowed aggregates or temporal joins), Stream Analytics sorts incoming events by timestamp order.</span></span>

<span data-ttu-id="84552-124">"Zaman damgası tarafından" anahtar sözcüğü olduğunda **değil** kullanıldığında, Azure Event Hubs olay sıraya alma süresi varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84552-124">When the “timestamp by” keyword is **not** used, the Azure Event Hubs event enqueue time is used by default.</span></span> <span data-ttu-id="84552-125">Olay hub'ları olay hub'ın her bölüm zaman damgasını monotonicity güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="84552-125">Event Hubs guarantees monotonicity of the timestamp on each partition of the event hub.</span></span> <span data-ttu-id="84552-126">Ayrıca, tüm bölümleri olaylarından zaman damgası sırayla birleştirilecek garanti eder.</span><span class="sxs-lookup"><span data-stu-id="84552-126">It also guarantees that events from all partitions will be merged in timestamp order.</span></span> <span data-ttu-id="84552-127">Bu iki olay hub'ları garantiler hiçbir sipariş olayları emin olun.</span><span class="sxs-lookup"><span data-stu-id="84552-127">These two Event Hubs guarantees ensure no out-of-order events.</span></span>

<span data-ttu-id="84552-128">Bazı durumlarda, gönderenin zaman damgası kullanabilmeniz için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="84552-128">Sometimes, it’s important for you to use the sender’s timestamp.</span></span> <span data-ttu-id="84552-129">Bu durumda, bir zaman damgası olay yükü gelen "zaman damgası tarafından." kullanarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="84552-129">In that case, a timestamp from the event payload is chosen by using “timestamp by.”</span></span> <span data-ttu-id="84552-130">Bu senaryolarda, bir veya daha fazla olay misorder kaynakları sunulan:</span><span class="sxs-lookup"><span data-stu-id="84552-130">In these scenarios, one or more sources of event misorder might be introduced:</span></span>

* <span data-ttu-id="84552-131">Olay üreticileri saati eğriltir vardır.</span><span class="sxs-lookup"><span data-stu-id="84552-131">Event producers have clock skews.</span></span> <span data-ttu-id="84552-132">Üreticileri, farklı bilgisayarlardan olduğunda farklı saatler sahip oldukları için bu yaygındır.</span><span class="sxs-lookup"><span data-stu-id="84552-132">This is common when producers are from different computers, so they have different clocks.</span></span>
* <span data-ttu-id="84552-133">Hedef olay hub'ına olayların kaynağından bir ağ gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="84552-133">There's a network delay from the source of the events to the destination event hub.</span></span>
* <span data-ttu-id="84552-134">Saat eğriltir olay hub'ı bölümler arasında mevcut.</span><span class="sxs-lookup"><span data-stu-id="84552-134">Clock skews exist between event hub partitions.</span></span> <span data-ttu-id="84552-135">Akış analizi, ilk olay enqueue zamanına göre tüm olay hub'ı bölümleri olaylarından sıralar.</span><span class="sxs-lookup"><span data-stu-id="84552-135">Stream Analytics first sorts events from all event hub partitions by event enqueue time.</span></span> <span data-ttu-id="84552-136">Ardından, hatalı sıralanmış olayları için veri akışı inceler.</span><span class="sxs-lookup"><span data-stu-id="84552-136">Then, it examines the data stream for misordered events.</span></span>

<span data-ttu-id="84552-137">Yapılandırma sekmesinde, aşağıdaki varsayılanlar bakın:</span><span class="sxs-lookup"><span data-stu-id="84552-137">On the configuration tab, you see the following defaults:</span></span>

![Stream Analytics sipariş işleme](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

<span data-ttu-id="84552-139">0 saniye düzen dışı tolerans penceresi kullanırsanız, tüm olayları her zaman sırada olduğundan ettiği taraf olduğunu.</span><span class="sxs-lookup"><span data-stu-id="84552-139">If you use 0 seconds as the out-of-order tolerance window, you are asserting that all events are in order all the time.</span></span> <span data-ttu-id="84552-140">Hatalı sıralanmış olay üç kaynağını göz önüne alındığında, bu durum geçerlidir düşüktür.</span><span class="sxs-lookup"><span data-stu-id="84552-140">Given the three sources of misordered events, it’s unlikely that this is true.</span></span> 

<span data-ttu-id="84552-141">Bir olay misorder düzeltmek Stream Analytics izin vermek için sıfır olmayan düzen dışı tolerans penceresi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84552-141">To allow Stream Analytics to correct an event misorder, you can specify a non-zero out-of-order tolerance window.</span></span> <span data-ttu-id="84552-142">Akış analizi kadar bu pencere olaylarını arabelleğe alır ve ardından bunları seçtiğiniz zaman damgası kullanarak yeniden sıralar.</span><span class="sxs-lookup"><span data-stu-id="84552-142">Stream Analytics buffers events up to that window, and then reorders them by using the timestamp you chose.</span></span> <span data-ttu-id="84552-143">Ardından, zamana bağlı dönüşümünü uygular.</span><span class="sxs-lookup"><span data-stu-id="84552-143">It then applies the temporal transformation.</span></span> <span data-ttu-id="84552-144">Bir 3 saniyelik penceresi başlatın ve saatine göre olay sayısını azaltmak için değer ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="84552-144">You can start with a 3-second window, and tune the value to reduce the number of events that are time-adjusted.</span></span> 

<span data-ttu-id="84552-145">Ara belleğe almanın bir yan etkisi çıkış olmasıdır **saat tutarında Gecikmeli**.</span><span class="sxs-lookup"><span data-stu-id="84552-145">A side effect of the buffering is that the output is **delayed by the same amount of time**.</span></span> <span data-ttu-id="84552-146">Düzen dışı olayların sayısını azaltmak için değer ayarlamak ve iş gecikme düşük tutun.</span><span class="sxs-lookup"><span data-stu-id="84552-146">You can tune the value to reduce the number of out-of-order events, and keep the job latency low.</span></span>

## <a name="get-help"></a><span data-ttu-id="84552-147">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="84552-147">Get help</span></span>
<span data-ttu-id="84552-148">Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="84552-148">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="84552-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84552-149">Next steps</span></span>
* [<span data-ttu-id="84552-150">Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="84552-150">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="84552-151">Stream Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84552-151">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="84552-152">Stream Analytics işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="84552-152">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="84552-153">Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="84552-153">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="84552-154">Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="84552-154">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)