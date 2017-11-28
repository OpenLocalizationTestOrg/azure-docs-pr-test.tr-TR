---
title: "aaaDiagnose ve sorunları çözme | Microsoft Docs"
description: "Bu öğretici kapsayan nasıl toodiagnose ve zaman serisi Öngörüler ortamınızdaki sorunları"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/24/2017
ms.author: venkatja
ms.openlocfilehash: 00893d4bec497f5f8bf7093be5b96f1844446d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-and-solve-problems-in-your-time-series-insights-environment"></a><span data-ttu-id="4421c-103">Zaman serisi Öngörüler ortamınızdaki sorunları tanılamada ve</span><span class="sxs-lookup"><span data-stu-id="4421c-103">Diagnose and solve problems in your Time Series Insights environment</span></span>

## <a name="i-dont-see-my-data"></a><span data-ttu-id="4421c-104">Verilerimi görmüyorum</span><span class="sxs-lookup"><span data-stu-id="4421c-104">I don't see my data</span></span>
<span data-ttu-id="4421c-105">Neden değil görebilirsiniz verilerinizi ortamınızdaki hello bazı nedenler şunlardır [Azure zaman serisi Insights portalında](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4421c-105">Here are some reasons why you might not see your data in your environment in hello [Azure Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-event-source-doesnt-have-data-in-json-format"></a><span data-ttu-id="4421c-106">Olay kaynağı JSON biçiminde veri yok</span><span class="sxs-lookup"><span data-stu-id="4421c-106">Your event source doesn't have data in JSON format</span></span>
<span data-ttu-id="4421c-107">Azure zaman serisi Öngörüler yalnızca JSON verilerini bugün destekler.</span><span class="sxs-lookup"><span data-stu-id="4421c-107">Azure Time Series Insights supports only JSON data today.</span></span> <span data-ttu-id="4421c-108">JSON örnekler için bkz: [desteklenen JSON şekiller](time-series-insights-send-events.md#supported-json-shapes).</span><span class="sxs-lookup"><span data-stu-id="4421c-108">For JSON samples, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

### <a name="when-you-registered-your-event-source-you-didnt-provide-hello-key-that-has-hello-required-permission"></a><span data-ttu-id="4421c-109">Olay kaynağı kaydolurken hello gerekli izne sahip hello anahtar sağlamadı</span><span class="sxs-lookup"><span data-stu-id="4421c-109">When you registered your event source, you didn't provide hello key that has hello required permission</span></span>
* <span data-ttu-id="4421c-110">Bir IOT hub için ihtiyacınız olan tooprovide hello anahtar **service bağlanma** izni.</span><span class="sxs-lookup"><span data-stu-id="4421c-110">For an IoT hub, you need tooprovide hello key that has **service connect** permission.</span></span>

   ![IOT hub hizmeti connect izni](media/diagnose-and-solve-problems/iothub-serviceconnect-permissions.png)

   <span data-ttu-id="4421c-112">Görüntü, önceki hello gösterildiği gibi hello ilkeleri birini **iothubowner** ve **hizmet** çalışır, her ikisi de olduğundan **hizmetine bağlanın** izni.</span><span class="sxs-lookup"><span data-stu-id="4421c-112">As shown in hello preceding image, either of hello policies **iothubowner** and **service** would work, because both have **service connect** permission.</span></span>
* <span data-ttu-id="4421c-113">Bir event hub için ihtiyacınız olan tooprovide hello anahtar **dinleme** izni.</span><span class="sxs-lookup"><span data-stu-id="4421c-113">For an event hub, you need tooprovide hello key that has **Listen** permission.</span></span>

   ![Olay hub'ı dinleme izni](media/diagnose-and-solve-problems/eventhub-listen-permissions.png)

   <span data-ttu-id="4421c-115">Görüntü, önceki hello gösterildiği gibi hello ilkeleri birini **okuma** ve **yönetmek** çalışır, her ikisi de olduğundan **dinleme** izni.</span><span class="sxs-lookup"><span data-stu-id="4421c-115">As shown in hello preceding image, either of hello policies **read** and **manage** would work, because both have **Listen** permission.</span></span>

### <a name="hello-provided-consumer-group-is-not-exclusive-tootime-series-insights"></a><span data-ttu-id="4421c-116">Merhaba tüketici grubu değil özel tooTime serisi Öngörüler sağlanır</span><span class="sxs-lookup"><span data-stu-id="4421c-116">hello provided consumer group is not exclusive tooTime Series Insights</span></span>
<span data-ttu-id="4421c-117">IOT hub'ı veya bir olay hub'ı için kayıt sırasında verilerinizi okumak için kullanılması gereken toospecify hello tüketici grubu isteriz.</span><span class="sxs-lookup"><span data-stu-id="4421c-117">For an IoT hub or an event hub, during registration we require you toospecify hello consumer group that should be used for reading your data.</span></span> <span data-ttu-id="4421c-118">Bu bir tüketici grubundaki paylaşılmayan gerekir.</span><span class="sxs-lookup"><span data-stu-id="4421c-118">This consumer group must not be shared.</span></span> <span data-ttu-id="4421c-119">Paylaşılıyorsa, hello temel olay hub'ı otomatik olarak hello okuyucular birini rastgele bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="4421c-119">If it's shared, hello underlying event hub automatically disconnects one of hello readers randomly.</span></span>

## <a name="i-see-my-data-but-theres-a-lag"></a><span data-ttu-id="4421c-120">Verilerimi bakın, ancak bir gecikme yok</span><span class="sxs-lookup"><span data-stu-id="4421c-120">I see my data, but there's a lag</span></span>
<span data-ttu-id="4421c-121">Neden görebilirsiniz kısmi veri ortamınızdaki hello nedenleri [zaman serisi Insights portalında](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4421c-121">Here are reasons why you might see partial data in your environment in hello [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span>

### <a name="your-environment-is-getting-throttled"></a><span data-ttu-id="4421c-122">Ortamınızı azaltıldı</span><span class="sxs-lookup"><span data-stu-id="4421c-122">Your environment is getting throttled</span></span>
<span data-ttu-id="4421c-123">Azaltma sınırından hello hello ortamı SKU türüne ve kapasite göre uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4421c-123">hello throttling limit is enforced based on hello environment's SKU type and capacity.</span></span> <span data-ttu-id="4421c-124">Tüm olay kaynakları hello ortamında bu kapasite paylaşır.</span><span class="sxs-lookup"><span data-stu-id="4421c-124">All event sources in hello environment share this capacity.</span></span> <span data-ttu-id="4421c-125">IOT hub'ını veya olay hub'ı için Hello olay kaynağı veri zorlanan hello sınırları ötesinde itmesi olursa, azaltma ve bir gecikme bakın.</span><span class="sxs-lookup"><span data-stu-id="4421c-125">If hello event source for your IoT hub or event hub is pushing data beyond hello enforced limits, you see throttling and a lag.</span></span>

<span data-ttu-id="4421c-126">Diyagram aşağıdaki Merhaba, SKU S1 ve 3 kapasiteye sahip bir zaman serisi Öngörüler ortamı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4421c-126">hello following diagram shows a Time Series Insights environment that has a SKU of S1 and a capacity of 3.</span></span> <span data-ttu-id="4421c-127">Gün başına giriş 3 milyon olayları dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4421c-127">It can ingress 3 million events per day.</span></span>

![Ortam SKU geçerli kapasitesi](media/diagnose-and-solve-problems/environment-sku-current-capacity.png)

<span data-ttu-id="4421c-129">Bu ortam diyagramı aşağıdaki hello gösterilen hello giriş oranı ile event hub'ındaki iletileri alma varsayın:</span><span class="sxs-lookup"><span data-stu-id="4421c-129">Assume that this environment is ingesting messages from an event hub with hello ingress rate shown in hello following diagram:</span></span>

![Bir olay hub'ına yönelik örnek giriş oranı](media/diagnose-and-solve-problems/eventhub-ingress-rate.png)

<span data-ttu-id="4421c-131">Merhaba diyagramda gösterildiği gibi hello günlük giriş ~ 67,000 iletileri hızıdır.</span><span class="sxs-lookup"><span data-stu-id="4421c-131">As shown in hello diagram, hello daily ingress rate is ~67,000 messages.</span></span> <span data-ttu-id="4421c-132">Bu oran too46 iletileri dakikada kabaca çevirir.</span><span class="sxs-lookup"><span data-stu-id="4421c-132">This rate translates roughly too46 messages every minute.</span></span> <span data-ttu-id="4421c-133">Her olay hub'ı ileti düzleştirilmiş tooa tek zaman serisi Öngörüler olay ise, bu ortam hiçbir azaltma görür.</span><span class="sxs-lookup"><span data-stu-id="4421c-133">If each event hub message is flattened tooa single Time Series Insights event, this environment sees no throttling.</span></span> <span data-ttu-id="4421c-134">Ardından her olay hub'ı ileti düzleştirilmiş too100 zaman serisi Öngörüler olayları ise, 4,600 olayları dakikada alınan.</span><span class="sxs-lookup"><span data-stu-id="4421c-134">If each event hub message is flattened too100 Time Series Insights events, then 4,600 events should be ingested every minute.</span></span> <span data-ttu-id="4421c-135">Dakikada 3 kapasiteye sahip bir S1 SKU ortam için giriş yalnızca 2,100 olayları (1 milyon olay günde 3 birimlerde dakikada 700 olayları = dakikada 2,100 olayları =).</span><span class="sxs-lookup"><span data-stu-id="4421c-135">An S1 SKU environment that has a capacity of 3 can ingress only 2,100 events every minute (1 million events per day = 700 events per minute at 3 units = 2,100 events per minute).</span></span> <span data-ttu-id="4421c-136">Bu nedenle, bir gecikme gördüğünüz son toothrottling.</span><span class="sxs-lookup"><span data-stu-id="4421c-136">Therefore you see a lag due toothrottling.</span></span> 

<span data-ttu-id="4421c-137">Mantığı düzleştirme nasıl çalıştığını üst düzey anlamak için bkz [desteklenen JSON şekiller](time-series-insights-send-events.md#supported-json-shapes).</span><span class="sxs-lookup"><span data-stu-id="4421c-137">For a high-level understanding of how flattening logic works, see [Supported JSON shapes](time-series-insights-send-events.md#supported-json-shapes).</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="4421c-138">Önerilen adımlar</span><span class="sxs-lookup"><span data-stu-id="4421c-138">Recommended steps</span></span>
<span data-ttu-id="4421c-139">toofix hello gecikme, artış hello ortamınızın SKU kapasitesi.</span><span class="sxs-lookup"><span data-stu-id="4421c-139">toofix hello lag, increase hello SKU capacity of your environment.</span></span> <span data-ttu-id="4421c-140">Daha fazla bilgi için bkz: [nasıl tooscale zaman serisi Öngörüler ortamınızı](time-series-insights-how-to-scale-your-environment.md).</span><span class="sxs-lookup"><span data-stu-id="4421c-140">For more information, see [How tooscale your Time Series Insights environment](time-series-insights-how-to-scale-your-environment.md).</span></span>

### <a name="youre-pushing-historical-data-and-causing-slow-ingress"></a><span data-ttu-id="4421c-141">Geçmiş verileri dağıtmaya ve yavaş giriş neden</span><span class="sxs-lookup"><span data-stu-id="4421c-141">You're pushing historical data and causing slow ingress</span></span>
<span data-ttu-id="4421c-142">Varolan bir olay kaynağına bağlanıyorsanız, IOT hub'ını veya olay hub'ı zaten verilerin içinde olduğunu olasıdır.</span><span class="sxs-lookup"><span data-stu-id="4421c-142">If you are connecting an existing event source, it's likely that your IoT hub or event hub already has data in it.</span></span> <span data-ttu-id="4421c-143">Bu nedenle hello ortamı hello olay kaynağının ileti saklama döneminin hello başından veri çekme başlatır.</span><span class="sxs-lookup"><span data-stu-id="4421c-143">So hello environment starts pulling data from hello beginning of hello event source's message retention period.</span></span> 

<span data-ttu-id="4421c-144">Bu davranış hello varsayılan davranıştır ve değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="4421c-144">This behavior is hello default behavior and cannot be overridden.</span></span> <span data-ttu-id="4421c-145">Azaltma gerçekleştirmesine ve biraz zaman alabilir geçmiş veri alma üzerinde toocatch ayarlama.</span><span class="sxs-lookup"><span data-stu-id="4421c-145">You can engage throttling, and it may take a while toocatch up on ingesting historical data.</span></span>

#### <a name="recommended-steps"></a><span data-ttu-id="4421c-146">Önerilen adımlar</span><span class="sxs-lookup"><span data-stu-id="4421c-146">Recommended steps</span></span>
<span data-ttu-id="4421c-147">toofix hello gecikme, aşağıdaki adımları gerçekleştirin hello:</span><span class="sxs-lookup"><span data-stu-id="4421c-147">toofix hello lag, take hello following steps:</span></span>
1. <span data-ttu-id="4421c-148">Merhaba SKU kapasitesi toohello maksimum izin verilen değer (Bu durumda 10) artırın.</span><span class="sxs-lookup"><span data-stu-id="4421c-148">Increase hello SKU capacity toohello maximum allowed value (10 in this case).</span></span> <span data-ttu-id="4421c-149">Merhaba kapasitesi artırılır sonra çok daha hızlı yakalama hello giriş işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="4421c-149">After hello capacity is increased, hello ingress process starts catching up much faster.</span></span> <span data-ttu-id="4421c-150">Ne kadar hızlı, hello kullanılabilirlik hello grafikte aracılığıyla yakalama görselleştirebilirsiniz [zaman serisi Insights portalında](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4421c-150">You can visualize how quickly you're catching up through hello availability chart in hello [Time Series Insights portal](https://insights.timeseries.azure.com).</span></span> <span data-ttu-id="4421c-151">Merhaba artan kapasite için sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="4421c-151">You are charged for hello increased capacity.</span></span>
2. <span data-ttu-id="4421c-152">Merhaba öteleme yakalanan sonra hello SKU kapasitesi geri tooyour normal giriş oranı azaltın.</span><span class="sxs-lookup"><span data-stu-id="4421c-152">After hello lag is caught up, decrease hello SKU capacity back tooyour normal ingress rate.</span></span>

## <a name="my-event-sources-timestamp-property-name-setting-doesnt-work"></a><span data-ttu-id="4421c-153">My olay kaynağının *zaman damgası özelliği adı* ayarı çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="4421c-153">My event source's *timestamp property name* setting doesn't work</span></span>
<span data-ttu-id="4421c-154">Merhaba ad ve değer toohello kurallara uygun emin olun:</span><span class="sxs-lookup"><span data-stu-id="4421c-154">Ensure that hello name and value conform toohello following rules:</span></span>
* <span data-ttu-id="4421c-155">Merhaba zaman damgası özelliği adı _büyük küçük harfe duyarlı_.</span><span class="sxs-lookup"><span data-stu-id="4421c-155">hello timestamp property name is _case-sensitive_.</span></span>
* <span data-ttu-id="4421c-156">Olay kaynağınız bir JSON dizesi olarak geldiği hello zaman damgası özelliği değeri hello biçimi olmalıdır _yyyy-MM-ddTHH. FFFFFFFK_.</span><span class="sxs-lookup"><span data-stu-id="4421c-156">hello timestamp property value that's coming from your event source, as a JSON string, should have hello format _yyyy-MM-ddTHH:mm:ss.FFFFFFFK_.</span></span> <span data-ttu-id="4421c-157">Bu tür bir dize örneğidir "2008-04-12T12:53Z".</span><span class="sxs-lookup"><span data-stu-id="4421c-157">An example of such a string is “2008-04-12T12:53Z”.</span></span>
