---
title: "aaaHandling olayı sırası ve Azure akış Analizi ile lateness | Microsoft Docs"
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
ms.openlocfilehash: 87c028662fbafbf4f72f57f215d017f65bb649f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-event-order-handling"></a><span data-ttu-id="e3749-104">Azure Stream Analytics olay sipariş işleme</span><span class="sxs-lookup"><span data-stu-id="e3749-104">Azure Stream Analytics event order handling</span></span>

<span data-ttu-id="e3749-105">Olayları bir zamana bağlı veri akışında her olay kaydedilir hello süresiyle bu hello olayı aldı.</span><span class="sxs-lookup"><span data-stu-id="e3749-105">In a temporal data stream of events, each event is recorded with hello time that hello event is received.</span></span> <span data-ttu-id="e3749-106">Bazı koşullar toooccasionally alma olay akışları bazı olaylar gönderildikleri farklı bir sırada neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3749-106">Some conditions might cause event streams toooccasionally receive some events in a different order than which they were sent.</span></span> <span data-ttu-id="e3749-107">Basit bir TCP'nin veya bile bir saat eğriltme cihaz ve olay hub'ı alma hello gönderme hello arasındaki bu toooccur neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3749-107">A simple TCP retransmit, or even a clock skew between hello sending device and hello receiving event hub might cause this toooccur.</span></span> <span data-ttu-id="e3749-108">"Noktalama" olaylar ayrıca eklenir tooreceived olay akışları, olay varış hello yokluğu tooadvance hello süre.</span><span class="sxs-lookup"><span data-stu-id="e3749-108">“Punctuation” events also are added tooreceived event streams, tooadvance hello time in hello absence of event arrivals.</span></span> <span data-ttu-id="e3749-109">Bunlar "bildirim 3 dakika bana oturum yok olduğunda oluşur." gibi senaryolarda gerekli</span><span class="sxs-lookup"><span data-stu-id="e3749-109">These are needed in scenarios like “Notify me when no logins occur for 3 minutes."</span></span>

<span data-ttu-id="e3749-110">Sırayla olmayan giriş akışları ya da şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e3749-110">Input streams that are not in order are either:</span></span>
* <span data-ttu-id="e3749-111">Sıralanmış (ve bu nedenle **Gecikmeli**).</span><span class="sxs-lookup"><span data-stu-id="e3749-111">Sorted (and therefore **delayed**).</span></span>
* <span data-ttu-id="e3749-112">Tooa kullanıcı tarafından belirtilen ilke göre hello sistem tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e3749-112">Adjusted by hello system, according tooa user-specified policy.</span></span>


## <a name="lateness-tolerance"></a><span data-ttu-id="e3749-113">Lateness dayanıklılık</span><span class="sxs-lookup"><span data-stu-id="e3749-113">Lateness tolerance</span></span>
<span data-ttu-id="e3749-114">Akış analizi, bu senaryo türlerini göstereceği.</span><span class="sxs-lookup"><span data-stu-id="e3749-114">Stream Analytics tolerates these types of scenarios.</span></span> <span data-ttu-id="e3749-115">Akış analizi "çıkış sıra" ve "geç" olayları için sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e3749-115">Stream Analytics has handling for "out-of-order" and "late" events.</span></span> <span data-ttu-id="e3749-116">Bu yolu izleyerek hello olayları işler:</span><span class="sxs-lookup"><span data-stu-id="e3749-116">It handles these events in hello following ways:</span></span>

* <span data-ttu-id="e3749-117">Sıralama dışında ulaşır ancak içinde hello toleransını ayarlayın olaylar **zaman damgası tarafından kaldırılmasında**.</span><span class="sxs-lookup"><span data-stu-id="e3749-117">Events that arrive out of order but within hello set tolerance are **reordered by timestamp**.</span></span>
* <span data-ttu-id="e3749-118">Dayanıklılık daha sonra gelen olaylar **bırakılan veya ayarlanmış**.</span><span class="sxs-lookup"><span data-stu-id="e3749-118">Events that arrive later than tolerance are **dropped or adjusted**.</span></span>
    * <span data-ttu-id="e3749-119">**Ayarlanmış**: ayarlanmış tooappear toohave hello son kabul edilebilir zaman gelmedi.</span><span class="sxs-lookup"><span data-stu-id="e3749-119">**Adjusted**: Adjusted tooappear toohave arrived at hello latest acceptable time.</span></span>
    * <span data-ttu-id="e3749-120">**Bırakılan**: atılır.</span><span class="sxs-lookup"><span data-stu-id="e3749-120">**Dropped**: Discarded.</span></span>

![Stream Analytics olay işleme](media/stream-analytics-event-handling/stream-analytics-event-handling.png)

## <a name="reduce-hello-number-of-out-of-order-events"></a><span data-ttu-id="e3749-122">Düzen dışı olayları Hello sayısını azaltın</span><span class="sxs-lookup"><span data-stu-id="e3749-122">Reduce hello number of out-of-order events</span></span>

<span data-ttu-id="e3749-123">Stream Analytics (örneğin, pencerelenmiş toplamlar veya zamana bağlı birleştirmeler) gelen olayları işlerken zamana bağlı bir dönüşüm uygulandığından, Stream Analytics gelen olayları zaman damgası sırasına göre sıralar.</span><span class="sxs-lookup"><span data-stu-id="e3749-123">Because Stream Analytics applies a temporal transformation when it processes incoming events (for example, for windowed aggregates or temporal joins), Stream Analytics sorts incoming events by timestamp order.</span></span>

<span data-ttu-id="e3749-124">Merhaba "zaman damgası tarafından" anahtar sözcüğü olduğunda **değil** kullanıldığında, hello Azure Event Hubs olay sıraya alma süresi varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e3749-124">When hello “timestamp by” keyword is **not** used, hello Azure Event Hubs event enqueue time is used by default.</span></span> <span data-ttu-id="e3749-125">Olay hub'ları hello zaman damgası hello olay hub'ın her bir bölüm monotonicity güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="e3749-125">Event Hubs guarantees monotonicity of hello timestamp on each partition of hello event hub.</span></span> <span data-ttu-id="e3749-126">Ayrıca, tüm bölümleri olaylarından zaman damgası sırayla birleştirilecek garanti eder.</span><span class="sxs-lookup"><span data-stu-id="e3749-126">It also guarantees that events from all partitions will be merged in timestamp order.</span></span> <span data-ttu-id="e3749-127">Bu iki olay hub'ları garantiler hiçbir sipariş olayları emin olun.</span><span class="sxs-lookup"><span data-stu-id="e3749-127">These two Event Hubs guarantees ensure no out-of-order events.</span></span>

<span data-ttu-id="e3749-128">Bazı durumlarda, toouse hello gönderenin zaman damgası için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="e3749-128">Sometimes, it’s important for you toouse hello sender’s timestamp.</span></span> <span data-ttu-id="e3749-129">Bu durumda, bir zaman damgası hello olay yükü öğesinden "zaman damgası tarafından." kullanarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="e3749-129">In that case, a timestamp from hello event payload is chosen by using “timestamp by.”</span></span> <span data-ttu-id="e3749-130">Bu senaryolarda, bir veya daha fazla olay misorder kaynakları sunulan:</span><span class="sxs-lookup"><span data-stu-id="e3749-130">In these scenarios, one or more sources of event misorder might be introduced:</span></span>

* <span data-ttu-id="e3749-131">Olay üreticileri saati eğriltir vardır.</span><span class="sxs-lookup"><span data-stu-id="e3749-131">Event producers have clock skews.</span></span> <span data-ttu-id="e3749-132">Üreticileri, farklı bilgisayarlardan olduğunda farklı saatler sahip oldukları için bu yaygındır.</span><span class="sxs-lookup"><span data-stu-id="e3749-132">This is common when producers are from different computers, so they have different clocks.</span></span>
* <span data-ttu-id="e3749-133">Ağ gecikmesi hello olayları toohello hedef olay hub'ının hello kaynağından yoktur.</span><span class="sxs-lookup"><span data-stu-id="e3749-133">There's a network delay from hello source of hello events toohello destination event hub.</span></span>
* <span data-ttu-id="e3749-134">Saat eğriltir olay hub'ı bölümler arasında mevcut.</span><span class="sxs-lookup"><span data-stu-id="e3749-134">Clock skews exist between event hub partitions.</span></span> <span data-ttu-id="e3749-135">Akış analizi, ilk olay enqueue zamanına göre tüm olay hub'ı bölümleri olaylarından sıralar.</span><span class="sxs-lookup"><span data-stu-id="e3749-135">Stream Analytics first sorts events from all event hub partitions by event enqueue time.</span></span> <span data-ttu-id="e3749-136">Ardından, hatalı sıralanmış olayları için hello veri akışı inceler.</span><span class="sxs-lookup"><span data-stu-id="e3749-136">Then, it examines hello data stream for misordered events.</span></span>

<span data-ttu-id="e3749-137">Merhaba yapılandırma sekmesinde Varsayılanları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e3749-137">On hello configuration tab, you see hello following defaults:</span></span>

![Stream Analytics sipariş işleme](media/stream-analytics-event-handling/stream-analytics-out-of-order-handling.png)

<span data-ttu-id="e3749-139">0 saniye hello düzen dışı tolerans penceresi kullanırsanız, tüm olayları hello zaman sırada olduğundan ettiği taraf olduğunu.</span><span class="sxs-lookup"><span data-stu-id="e3749-139">If you use 0 seconds as hello out-of-order tolerance window, you are asserting that all events are in order all hello time.</span></span> <span data-ttu-id="e3749-140">Hatalı sıralanmış olay Hello üç kaynağını göz önüne alındığında, bu durum geçerlidir düşüktür.</span><span class="sxs-lookup"><span data-stu-id="e3749-140">Given hello three sources of misordered events, it’s unlikely that this is true.</span></span> 

<span data-ttu-id="e3749-141">tooallow Stream Analytics toocorrect bir olay misorder, sıfır olmayan düzen dışı tolerans penceresi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3749-141">tooallow Stream Analytics toocorrect an event misorder, you can specify a non-zero out-of-order tolerance window.</span></span> <span data-ttu-id="e3749-142">Stream Analytics toothat penceresi ve bunları kullanarak seçtiğiniz zaman damgası hello yeniden verilen siparişler olaylarını arabelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="e3749-142">Stream Analytics buffers events up toothat window, and then reorders them by using hello timestamp you chose.</span></span> <span data-ttu-id="e3749-143">Ardından, hello zamana bağlı dönüştürme uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e3749-143">It then applies hello temporal transformation.</span></span> <span data-ttu-id="e3749-144">Bir 3 saniyelik penceresi başlatın ve hello değeri tooreduce hello saatine göre olayların sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e3749-144">You can start with a 3-second window, and tune hello value tooreduce hello number of events that are time-adjusted.</span></span> 

<span data-ttu-id="e3749-145">Merhaba ara belleğe almanın bir yan etkisi hello çıkış olmasıdır **tarafından hello aynı Gecikmeli süreyi**.</span><span class="sxs-lookup"><span data-stu-id="e3749-145">A side effect of hello buffering is that hello output is **delayed by hello same amount of time**.</span></span> <span data-ttu-id="e3749-146">Merhaba değeri tooreduce hello düzen dışı olayların sayısını ayarlamak ve hello iş gecikme düşük tutun.</span><span class="sxs-lookup"><span data-stu-id="e3749-146">You can tune hello value tooreduce hello number of out-of-order events, and keep hello job latency low.</span></span>

## <a name="get-help"></a><span data-ttu-id="e3749-147">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="e3749-147">Get help</span></span>
<span data-ttu-id="e3749-148">Ek Yardım için deneyin bizim [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="e3749-148">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3749-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3749-149">Next steps</span></span>
* [<span data-ttu-id="e3749-150">Giriş tooStream analizi</span><span class="sxs-lookup"><span data-stu-id="e3749-150">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e3749-151">Stream Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e3749-151">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e3749-152">Stream Analytics işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e3749-152">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="e3749-153">Stream Analytics sorgu dili başvurusu</span><span class="sxs-lookup"><span data-stu-id="e3749-153">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e3749-154">Stream Analytics Yönetimi REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="e3749-154">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)