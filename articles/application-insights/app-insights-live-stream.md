---
title: "aaaLive özel ölçümleri ve tanılama Azure Application Insights'olan ölçümleri akış | Microsoft Docs"
description: "Özel ölçümleri ile gerçek zamanlı web uygulamanızı izlemek ve canlı akış hataları, izlemeleri ve olayları ile ilgili sorunları tanılamak."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="0e48c-103">Canlı ölçümleri akış: 1 saniye gecikme süresi ile Tanıla & zle</span><span class="sxs-lookup"><span data-stu-id="0e48c-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="0e48c-104">Merhaba göndermeyi Kalp canlı, üretim web uygulamanızın Canlı ölçümleri akıştan kullanarak araştırma [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e48c-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="0e48c-105">Seçin ve herhangi bir rahatsızlık tooyour hizmeti olmadan gerçek zamanlı ölçümleri ve performans sayaçları toowatch filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="0e48c-106">Yığın izlemeleri örnek başarısız istekler ve özel durumları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="0e48c-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="0e48c-107">İle birlikte [profil oluşturucu](app-insights-profiler.md), [anlık görüntü hata ayıklayıcı](app-insights-snapshot-debugger.md), ve [performans testi](app-insights-monitor-web-app-availability.md#performance-tests), Canlı ölçümleri akış için canlı web güçlü ve bozucu bir tanılama aracı sağlar Site.</span><span class="sxs-lookup"><span data-stu-id="0e48c-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="0e48c-108">Canlı ölçümleri akış ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0e48c-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="0e48c-109">Serbest olsa da, bir düzeltme doğrulamak performans ve hata sayısını izlerken tarafından.</span><span class="sxs-lookup"><span data-stu-id="0e48c-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="0e48c-110">Sorunlarını tanılamak ve test yükleri hello etkisini izleme Canlı.</span><span class="sxs-lookup"><span data-stu-id="0e48c-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="0e48c-111">Belirli test oturumlarını odaklanmak veya seçerek ve toowatch istediğiniz hello ölçümleri filtreleme bilinen sorunlar filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="0e48c-112">Özel durum izlemeleri olduğu alın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="0e48c-113">Filtrelerle deneme toofind hello en uygun KPI'ları.</span><span class="sxs-lookup"><span data-stu-id="0e48c-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="0e48c-114">Performans sayacı Canlı herhangi bir Windows izleyin.</span><span class="sxs-lookup"><span data-stu-id="0e48c-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="0e48c-115">Kolayca sorunları sahip bir sunucu tanımlayın ve bu sunucu tüm hello KPI ve canlı akış toojust filtre.</span><span class="sxs-lookup"><span data-stu-id="0e48c-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="0e48c-116">[![Canlı ölçümleri akış video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="0e48c-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="0e48c-117">Ölçümler bir canlı akışı hello Bulut veya şirket içi çalıştıran ASP.NET uygulamaları üzerinde şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="0e48c-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="0e48c-118">başlarken</span><span class="sxs-lookup"><span data-stu-id="0e48c-118">Get started</span></span>

1. <span data-ttu-id="0e48c-119">Henüz yapmadıysanız [Application Insights yüklü](app-insights-asp-net.md) , ASP.NET web uygulamanızda veya [Windows server uygulaması](app-insights-windows-services.md), bunu şimdi yapın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="0e48c-120">**Güncelleştirme toohello en son sürümü** hello Application Insights paketi.</span><span class="sxs-lookup"><span data-stu-id="0e48c-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="0e48c-121">Visual Studio'da, projenize sağ tıklayın ve seçin **Manage Nuget paketleri**.</span><span class="sxs-lookup"><span data-stu-id="0e48c-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="0e48c-122">Açık hello **güncelleştirmeleri** sekmesi, onay **dahil et**ve tüm hello Microsoft.ApplicationInsights.* paketlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="0e48c-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="0e48c-123">Uygulamanızı yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-123">Redeploy your app.</span></span>

3. <span data-ttu-id="0e48c-124">Merhaba, [Azure portal](https://portal.azure.com), uygulamanız için hello Application Insights kaynağı ve ardından canlı akış açın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="0e48c-125">[Güvenli hello denetim kanalı](#secure-the-control-channel) müşteri adları gibi hassas verileri, filtrelerinizi kullandığınız.</span><span class="sxs-lookup"><span data-stu-id="0e48c-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Merhaba genel bakış dikey penceresinde, canlı akış'a tıklayın.](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="0e48c-127">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="0e48c-127">No data?</span></span> <span data-ttu-id="0e48c-128">Sunucu güvenlik duvarının denetleyin</span><span class="sxs-lookup"><span data-stu-id="0e48c-128">Check your server firewall</span></span>

<span data-ttu-id="0e48c-129">Merhaba denetleyin [bağlantı noktaları için Canlı ölçümleri akış giden](app-insights-ip-addresses.md#outgoing-ports) sunucularınızı hello Güvenlik Duvarı'nda açıktır.</span><span class="sxs-lookup"><span data-stu-id="0e48c-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="0e48c-130">Ölçümler bir canlı akışı nasıl ölçüm Gezgini ve analizi farkı nedir?</span><span class="sxs-lookup"><span data-stu-id="0e48c-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="0e48c-131">Canlı akış</span><span class="sxs-lookup"><span data-stu-id="0e48c-131">Live Stream</span></span> | <span data-ttu-id="0e48c-132">Ölçüm Gezgini ve analizi</span><span class="sxs-lookup"><span data-stu-id="0e48c-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="0e48c-133">Gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="0e48c-133">Latency</span></span>|<span data-ttu-id="0e48c-134">Bir saniye içinde görüntülenen verileri</span><span class="sxs-lookup"><span data-stu-id="0e48c-134">Data displayed within one second</span></span>|<span data-ttu-id="0e48c-135">Dakika boyunca bir araya getirilir</span><span class="sxs-lookup"><span data-stu-id="0e48c-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="0e48c-136">Hiçbir bekletme</span><span class="sxs-lookup"><span data-stu-id="0e48c-136">No retention</span></span>|<span data-ttu-id="0e48c-137">Merhaba grafiğidir ve sonra atılır verileri devam eder.</span><span class="sxs-lookup"><span data-stu-id="0e48c-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="0e48c-138">90 gün boyunca tutulur veri</span><span class="sxs-lookup"><span data-stu-id="0e48c-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="0e48c-139">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="0e48c-139">On demand</span></span>|<span data-ttu-id="0e48c-140">Canlı ölçümleri açarken veri akışı</span><span class="sxs-lookup"><span data-stu-id="0e48c-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="0e48c-141">Merhaba SDK yüklü ve etkin olduğunda veriler gönderilir</span><span class="sxs-lookup"><span data-stu-id="0e48c-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="0e48c-142">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="0e48c-142">Free</span></span>|<span data-ttu-id="0e48c-143">Canlı akış verileri için herhangi bir ücret alınmaz</span><span class="sxs-lookup"><span data-stu-id="0e48c-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="0e48c-144">Çok konu[fiyatlandırma](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="0e48c-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="0e48c-145">Örnekleme</span><span class="sxs-lookup"><span data-stu-id="0e48c-145">Sampling</span></span>|<span data-ttu-id="0e48c-146">Seçilen tüm ölçümler ve sayaçlar aktarılır.</span><span class="sxs-lookup"><span data-stu-id="0e48c-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="0e48c-147">Hataları ve Yığın izlemeleri örneklenen.</span><span class="sxs-lookup"><span data-stu-id="0e48c-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="0e48c-148">TelemetryProcessors uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="0e48c-149">Olayları olabilir [örneklenen](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="0e48c-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="0e48c-150">Denetim kanalı</span><span class="sxs-lookup"><span data-stu-id="0e48c-150">Control channel</span></span>|<span data-ttu-id="0e48c-151">Filtre denetimi sinyalleri toohello SDK gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0e48c-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="0e48c-152">Öneririz [bu kanal güvenli](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="0e48c-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="0e48c-153">Tek yönlü iletişim toohello portalı</span><span class="sxs-lookup"><span data-stu-id="0e48c-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="0e48c-154">Seçin ve ölçümlerinizi filtre</span><span class="sxs-lookup"><span data-stu-id="0e48c-154">Select and filter your metrics</span></span>

<span data-ttu-id="0e48c-155">(Klasik kullanılabilir ASP.NET uygulamaları ile en son SDK hello.)</span><span class="sxs-lookup"><span data-stu-id="0e48c-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="0e48c-156">Merhaba Portalı'ndan herhangi Application Insights telemetriyi rasgele filtreleri uygulayarak özel KPI dinamik izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="0e48c-157">Ne zaman, fare hello grafikleri hiçbirini üzerinde gösterir hello filtre denetimi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="0e48c-158">Grafik aşağıdaki hello URL ve süre öznitelikleri filtreleri ile özel bir istek sayısı KPI Çizdirmek.</span><span class="sxs-lookup"><span data-stu-id="0e48c-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="0e48c-159">Filtrelerinizi hello bir canlı akış zamanında herhangi bir noktada belirtilen hello ölçütlerle eşleşen telemetri gösteren akış Önizleme bölümü ile doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![Özel istek KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="0e48c-161">Sayısını başka bir değer izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="0e48c-162">Merhaba seçenekler hello herhangi Application Insights telemetri olabilir akış türüne bağlıdır: istekleri, bağımlılıkları, özel durumlar, izlemeleri, olayları veya ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="0e48c-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="0e48c-163">Bu, kendi olabilir [özel ölçüm](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="0e48c-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Değer seçenekleri](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="0e48c-165">Ayrıca tooApplication Insights telemetri, da herhangi bir Windows performans sayacı hello akış seçeneklerden birini seçerek ve sağlayan hello performans sayacı hello adı izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="0e48c-166">Canlı ölçümleri iki noktalarda toplanır: her sunucuda yerel olarak ve tüm sunucular genelinde.</span><span class="sxs-lookup"><span data-stu-id="0e48c-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="0e48c-167">Merhaba varsayılan hello ilgili aşağı açılan listeler diğer seçenekler seçerek ya da değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="0e48c-168">Örnek Telemetri: Özel Canlı Tanılama Olayları</span><span class="sxs-lookup"><span data-stu-id="0e48c-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="0e48c-169">Varsayılan olarak, başarısız olan istekler ve bağımlılık çağrıları, özel durumlar, olayları ve izlemeleri örnekleri hello canlı akış olayların gösterir.</span><span class="sxs-lookup"><span data-stu-id="0e48c-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="0e48c-170">Merhaba filtre simgesini toosee uygulanan hello ölçütlerini herhangi bir noktada zamanında'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![Varsayılan Canlı akış](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="0e48c-172">Olarak ölçümleri ile tüm rasgele ölçütleri tooany hello Application Insights telemetri türlerinin belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="0e48c-173">Bu örnekte, biz belirli bir istek hataları, izlemeler ve olaylar seçmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="0e48c-174">Biz de tüm özel durumlar ve bağımlılık hataları seçmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-174">We are also selecting all exceptions and dependency failures.</span></span>

![Özel canlı akış](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="0e48c-176">Not: Özel durum iletisi tabanlı ölçütü için şu anda hello en dıştaki özel durum iletisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="0e48c-177">Örnek, önceki hello içinde hello zararsız iç özel durum iletisi durumla çıkışı toofilter (aşağıdaki hello "<--" sınırlayıcı) "Merhaba istemci bağlantısı kesildi."</span><span class="sxs-lookup"><span data-stu-id="0e48c-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="0e48c-178">Kullanım bir ileti değil-"İstek içeriği okunurken hata oluştu" ölçütler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="0e48c-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="0e48c-179">Merhaba ayrıntılarını tıklayarak akış canlı bir öğeyi hello bakın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="0e48c-180">Tıklayarak ya da akış hello duraklatabilirsiniz **duraklatma** yalnızca aşağı kaydırma veya bir öğeyi tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="0e48c-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="0e48c-181">Canlı akış geri toohello üst kaydırma sonra devam eder veya öğelerin hello sayaç tıklayarak durdurulduğundan sırasında toplanan.</span><span class="sxs-lookup"><span data-stu-id="0e48c-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![Örneklenen Canlı hataları](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="0e48c-183">Sunucu örneği tarafından filtre</span><span class="sxs-lookup"><span data-stu-id="0e48c-183">Filter by server instance</span></span>

<span data-ttu-id="0e48c-184">Belirli bir sunucu rolü örneği toomonitor istiyorsanız, sunucu tarafından filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![Örneklenen Canlı hataları](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="0e48c-186">SDK gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="0e48c-186">SDK Requirements</span></span>
<span data-ttu-id="0e48c-187">Özel Canlı ölçümleri akış sürüm 2.4.0-beta2 bulunan ya da daha yeni olan [Application Insights SDK Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="0e48c-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="0e48c-188">NuGet Paket Yöneticisi'nden tooselect "Yayın öncesi Ekle" seçeneğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="0e48c-189">Merhaba denetim kanalının güvenliğini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0e48c-189">Secure hello control channel</span></span>
<span data-ttu-id="0e48c-190">Merhaba özel filtreler ölçütlere geri toohello Canlı ölçümleri bileşen hello Application Insights SDK'sı gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0e48c-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="0e48c-191">Hello filtreleri olası customerIDs gibi hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0e48c-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="0e48c-192">Merhaba kanal gizli bir API anahtarı ile ayrıca toohello izleme anahtarını güvenli hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="0e48c-193">API anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e48c-193">Create an API Key</span></span>

![API anahtarı oluşturma](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="0e48c-195">API anahtar tooConfiguration Ekle</span><span class="sxs-lookup"><span data-stu-id="0e48c-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="0e48c-196">Merhaba applicationınsights.config dosyasında hello AuthenticationApiKey toohello QuickPulseTelemetryModule ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0e48c-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="0e48c-197">Veya isteğe bağlı olarak kod içinde QuickPulseTelemetryModule hello üzerinde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="0e48c-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="0e48c-198">Ancak, algılar ve tüm bağlı sunucular hello güveniyorsanız hello özel filtreler kimliği doğrulanmış hello kanal olmadan deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e48c-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="0e48c-199">Bu seçenek altı ay için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0e48c-199">This option is available for six months.</span></span> <span data-ttu-id="0e48c-200">Bu geçersiz kılma kez her yeni bir oturum gereklidir veya ne zaman yeni bir sunucu gelir çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="0e48c-200">This override is required once every new session, or when a new server comes online.</span></span>

![Canlı ölçümleri kimlik doğrulama seçenekleri](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="0e48c-202">Hello filtre ölçütlerini CustomerID gibi olası hassas bilgileri girmeden önce kimlik doğrulaması hello kanalı ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="0e48c-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="0e48c-203">Performans testi yükleme oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e48c-203">Generating a performance test load</span></span>

<span data-ttu-id="0e48c-204">İsterseniz toowatch hello etkisini bir iş yükünün artırmak, kullanım hello performans testi dikey.</span><span class="sxs-lookup"><span data-stu-id="0e48c-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="0e48c-205">Bu, eşzamanlı kullanıcıların sayısı gelen istekleri benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="0e48c-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="0e48c-206">Ya da "el ile testleri" çalıştırabilirsiniz (ping testleri) tek bir URL veya çalıştırabilirsiniz bir [çok adımlı web performans testi](app-insights-monitor-web-app-availability.md#multi-step-web-tests) (aynı kullanılabilirlik olarak şekilde test hello) karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e48c-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="0e48c-207">Merhaba performans testi oluşturduktan sonra hello test açın ve canlı akış dikey penceresinde ayrı windows hello.</span><span class="sxs-lookup"><span data-stu-id="0e48c-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="0e48c-208">Performans testi başlatır ve izleme canlı akış hello hello zaman sıraya görebilirsiniz aynı anda.</span><span class="sxs-lookup"><span data-stu-id="0e48c-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="0e48c-209">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0e48c-209">Troubleshooting</span></span>

<span data-ttu-id="0e48c-210">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="0e48c-210">No data?</span></span> <span data-ttu-id="0e48c-211">Uygulamanızı korunan bir ağda ise: Canlı ölçümleri akış diğer Application Insights telemetri daha farklı bir IP adreslerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0e48c-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="0e48c-212">Emin olun [bu IP adreslerinden](app-insights-ip-addresses.md) duvarınızda açıktır.</span><span class="sxs-lookup"><span data-stu-id="0e48c-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0e48c-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e48c-213">Next steps</span></span>
* [<span data-ttu-id="0e48c-214">Application Insights ile kullanım izleme</span><span class="sxs-lookup"><span data-stu-id="0e48c-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="0e48c-215">Tanılama aramayı kullanma</span><span class="sxs-lookup"><span data-stu-id="0e48c-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="0e48c-216">Profil Oluşturucu</span><span class="sxs-lookup"><span data-stu-id="0e48c-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="0e48c-217">Anlık görüntü hata ayıklayıcı</span><span class="sxs-lookup"><span data-stu-id="0e48c-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
