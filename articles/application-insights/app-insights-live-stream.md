---
title: "Ölçümleri akışı özel ölçümleri ve Tanılama, Azure Application Insights ile canlı | Microsoft Docs"
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
ms.openlocfilehash: 1eb2e0c467d4fb4cb263047caf58d36231578d9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="2ffd0-103">Canlı ölçümleri akış: 1 saniye gecikme süresi ile Tanıla & zle</span><span class="sxs-lookup"><span data-stu-id="2ffd0-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="2ffd0-104">Canlı ölçümleri akıştan kullanarak canlı, üretim web uygulamanızın göndermeyi Kalp araştırma [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ffd0-104">Probe the beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="2ffd0-105">Seçin ve tüm rahatsızlık hizmetinize olmadan gerçek zamanlı olarak izlemek için ölçümleri ve performans sayaçlarını filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-105">Select and filter metrics and performance counters to watch in real time, without any disturbance to your service.</span></span> <span data-ttu-id="2ffd0-106">Yığın izlemeleri örnek başarısız istekler ve özel durumları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="2ffd0-107">İle birlikte [profil oluşturucu](app-insights-profiler.md), [anlık görüntü hata ayıklayıcı](app-insights-snapshot-debugger.md), ve [performans testi](app-insights-monitor-web-app-availability.md#performance-tests), Canlı ölçümleri akış için canlı web güçlü ve bozucu bir tanılama aracı sağlar Site.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="2ffd0-108">Canlı ölçümleri akış ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2ffd0-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="2ffd0-109">Serbest olsa da, bir düzeltme doğrulamak performans ve hata sayısını izlerken tarafından.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="2ffd0-110">Sorunlarını tanılamak ve test yükleri etkisini izleme Canlı.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-110">Watch the effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="2ffd0-111">Belirli test oturumlarını odaklanmak veya seçerek ve izlemek istediğiniz ölçümleri filtreleme bilinen sorunlar filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-111">Focus on particular test sessions or filter out known issues, by selecting and filtering the metrics you want to watch.</span></span>
* <span data-ttu-id="2ffd0-112">Özel durum izlemeleri olduğu alın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="2ffd0-113">En uygun KPI'ları Bul filtrelerle denemeler yapın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-113">Experiment with filters to find the most relevant KPIs.</span></span>
* <span data-ttu-id="2ffd0-114">Performans sayacı Canlı herhangi bir Windows izleyin.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="2ffd0-115">Kolayca sorunlar ve bu sunucuya yalnızca tüm KPI/canlı akış filtre sahip bir sunucu tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-115">Easily identify a server that is having issues, and filter all the KPI/live feed to just that server.</span></span>

<span data-ttu-id="2ffd0-116">[![Canlı ölçümleri akış video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="2ffd0-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="2ffd0-117">Ölçümler bir canlı akışı ASP.NET uygulamalarını çalıştıran şirket içi veya bulutta şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in the Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="2ffd0-118">başlarken</span><span class="sxs-lookup"><span data-stu-id="2ffd0-118">Get started</span></span>

1. <span data-ttu-id="2ffd0-119">Henüz yapmadıysanız [Application Insights yüklü](app-insights-asp-net.md) , ASP.NET web uygulamanızda veya [Windows server uygulaması](app-insights-windows-services.md), bunu şimdi yapın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="2ffd0-120">**En son sürüme güncelleştirin** Application Insights paketi.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-120">**Update to the latest version** of the Application Insights package.</span></span> <span data-ttu-id="2ffd0-121">Visual Studio'da, projenize sağ tıklayın ve seçin **Manage Nuget paketleri**.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="2ffd0-122">Açık **güncelleştirmeleri** sekmesi, onay **dahil et**ve tüm Microsoft.ApplicationInsights.* paketleri seçin.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-122">Open the **Updates** tab, check **Include prerelease**, and select all the Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="2ffd0-123">Uygulamanızı yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-123">Redeploy your app.</span></span>

3. <span data-ttu-id="2ffd0-124">İçinde [Azure portal](https://portal.azure.com), uygulamanız için Application Insights kaynağı açın ve ardından canlı akış'ı açın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-124">In the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="2ffd0-125">[Denetim kanalı güvenli](#secure-the-control-channel) müşteri adları gibi hassas verileri, filtrelerinizi kullandığınız.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-125">[Secure the control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![Genel Bakış dikey penceresinde, canlı akış'a tıklayın.](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="2ffd0-127">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="2ffd0-127">No data?</span></span> <span data-ttu-id="2ffd0-128">Sunucu güvenlik duvarının denetleyin</span><span class="sxs-lookup"><span data-stu-id="2ffd0-128">Check your server firewall</span></span>

<span data-ttu-id="2ffd0-129">Denetleme [bağlantı noktaları için Canlı ölçümleri akış giden](app-insights-ip-addresses.md#outgoing-ports) sunucularınızın Güvenlik Duvarı'nda açıktır.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-129">Check the [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in the firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="2ffd0-130">Ölçümler bir canlı akışı nasıl ölçüm Gezgini ve analizi farkı nedir?</span><span class="sxs-lookup"><span data-stu-id="2ffd0-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="2ffd0-131">Canlı akış</span><span class="sxs-lookup"><span data-stu-id="2ffd0-131">Live Stream</span></span> | <span data-ttu-id="2ffd0-132">Ölçüm Gezgini ve analizi</span><span class="sxs-lookup"><span data-stu-id="2ffd0-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="2ffd0-133">Gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="2ffd0-133">Latency</span></span>|<span data-ttu-id="2ffd0-134">Bir saniye içinde görüntülenen verileri</span><span class="sxs-lookup"><span data-stu-id="2ffd0-134">Data displayed within one second</span></span>|<span data-ttu-id="2ffd0-135">Dakika boyunca bir araya getirilir</span><span class="sxs-lookup"><span data-stu-id="2ffd0-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="2ffd0-136">Hiçbir bekletme</span><span class="sxs-lookup"><span data-stu-id="2ffd0-136">No retention</span></span>|<span data-ttu-id="2ffd0-137">Grafikte olduğu ve sonra atılır verileri devam eder.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-137">Data persists while it's on the chart, and is then discarded</span></span>|[<span data-ttu-id="2ffd0-138">90 gün boyunca tutulur veri</span><span class="sxs-lookup"><span data-stu-id="2ffd0-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="2ffd0-139">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="2ffd0-139">On demand</span></span>|<span data-ttu-id="2ffd0-140">Canlı ölçümleri açarken veri akışı</span><span class="sxs-lookup"><span data-stu-id="2ffd0-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="2ffd0-141">SDK'ın yüklü ve etkin olduğunda veriler gönderilir</span><span class="sxs-lookup"><span data-stu-id="2ffd0-141">Data is sent whenever the SDK is installed and enabled</span></span>|
|<span data-ttu-id="2ffd0-142">Ücretsiz</span><span class="sxs-lookup"><span data-stu-id="2ffd0-142">Free</span></span>|<span data-ttu-id="2ffd0-143">Canlı akış verileri için herhangi bir ücret alınmaz</span><span class="sxs-lookup"><span data-stu-id="2ffd0-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="2ffd0-144">Konusu [fiyatlandırma](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="2ffd0-144">Subject to [pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="2ffd0-145">Örnekleme</span><span class="sxs-lookup"><span data-stu-id="2ffd0-145">Sampling</span></span>|<span data-ttu-id="2ffd0-146">Seçilen tüm ölçümler ve sayaçlar aktarılır.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="2ffd0-147">Hataları ve Yığın izlemeleri örneklenen.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="2ffd0-148">TelemetryProcessors uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="2ffd0-149">Olayları olabilir [örneklenen](app-insights-api-filtering-sampling.md)</span><span class="sxs-lookup"><span data-stu-id="2ffd0-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="2ffd0-150">Denetim kanalı</span><span class="sxs-lookup"><span data-stu-id="2ffd0-150">Control channel</span></span>|<span data-ttu-id="2ffd0-151">Filtre denetimi sinyalleri SDK gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-151">Filter control signals are sent to the SDK.</span></span> <span data-ttu-id="2ffd0-152">Öneririz [bu kanal güvenli](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="2ffd0-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="2ffd0-153">Portala tek yönlü iletişim</span><span class="sxs-lookup"><span data-stu-id="2ffd0-153">Communication is one-way, to the portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="2ffd0-154">Seçin ve ölçümlerinizi filtre</span><span class="sxs-lookup"><span data-stu-id="2ffd0-154">Select and filter your metrics</span></span>

<span data-ttu-id="2ffd0-155">(Klasik ASP.NET uygulamalarını son SDK'sı ile kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="2ffd0-155">(Available on classic ASP.NET apps with the latest SDK.)</span></span>

<span data-ttu-id="2ffd0-156">Portaldan herhangi Application Insights telemetriyi rasgele filtreleri uygulayarak özel KPI dinamik izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from the portal.</span></span> <span data-ttu-id="2ffd0-157">Ne zaman, fare aşağıdakilerden grafikleri üzerinde gösteren filtre denetimi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-157">Click the filter control that shows when you mouse-over any of the charts.</span></span> <span data-ttu-id="2ffd0-158">Aşağıdaki grafikte URL ve süre öznitelikleri filtreleri ile özel bir istek sayısı KPI Çizdirmek.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-158">The following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="2ffd0-159">Bir canlı akış zamanında herhangi bir noktada belirtilen ölçütlerle eşleşen telemetri gösteren akış Önizleme bölümüyle filtrelerinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-159">Validate your filters with the Stream Preview section that shows a live feed of telemetry that matches the criteria you have specified at any point in time.</span></span> 

![Özel istek KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="2ffd0-161">Sayısını başka bir değer izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="2ffd0-162">Seçenekler herhangi Application Insights telemetri olabilir akış türüne bağlıdır: istekleri, bağımlılıkları, özel durumlar, izlemeleri, olayları veya ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-162">The options depend on the type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="2ffd0-163">Bu, kendi olabilir [özel ölçüm](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="2ffd0-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Değer seçenekleri](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="2ffd0-165">Application Insights telemetri yanı sıra akış seçeneklerden birini seçerek ve performans sayacının adını sağlayan tüm Windows performans sayacı da izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-165">In addition to Application Insights telemetry, you can also monitor any Windows performance counter by selecting that from the stream options, and providing the name of the performance counter.</span></span>

<span data-ttu-id="2ffd0-166">Canlı ölçümleri iki noktalarda toplanır: her sunucuda yerel olarak ve tüm sunucular genelinde.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="2ffd0-167">Varsayılan değer olarak ilgili aşağı açılan listeler diğer seçenekleri belirleyerek ya da değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-167">You can change the default at either by selecting other options in the respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="2ffd0-168">Örnek Telemetri: Özel Canlı Tanılama Olayları</span><span class="sxs-lookup"><span data-stu-id="2ffd0-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="2ffd0-169">Varsayılan olarak, olayların canlı akış başarısız isteklerin ve bağımlılık çağrıları, özel durumlar, olayları ve izlemeleri örnekleri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-169">By default, the live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="2ffd0-170">Zamanında uygulanan ölçütlerini herhangi bir noktada görmek için filtre simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-170">Click the filter icon to see the applied criteria at any point in time.</span></span> 

![Varsayılan Canlı akış](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="2ffd0-172">Olarak ölçümleri ile Application Insights telemetri türlerinden herhangi birini için herhangi bir rastgele ölçüt belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-172">As with metrics, you can specify any arbitrary criteria to any of the Application Insights telemetry types.</span></span> <span data-ttu-id="2ffd0-173">Bu örnekte, biz belirli bir istek hataları, izlemeler ve olaylar seçmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="2ffd0-174">Biz de tüm özel durumlar ve bağımlılık hataları seçmiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-174">We are also selecting all exceptions and dependency failures.</span></span>

![Özel canlı akış](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="2ffd0-176">Not: Özel durum iletisi tabanlı ölçütü için şu anda en dıştaki özel durum iletisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-176">Note: Currently, for Exception message-based criteria, use the outermost exception message.</span></span> <span data-ttu-id="2ffd0-177">İç özel durum iletisi zararsız durumla filtrelemek için önceki örnekte (aşağıdaki "<--" sınırlayıcı) "istemci bağlantısı kesildi."</span><span class="sxs-lookup"><span data-stu-id="2ffd0-177">In the preceding example, to filter out the benign exception with inner exception message (follows the "<--" delimiter) "The client disconnected."</span></span> <span data-ttu-id="2ffd0-178">Kullanım bir ileti değil-"İstek içeriği okunurken hata oluştu" ölçütler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="2ffd0-179">Bir öğenin Canlı akıştaki ayrıntılarını tıklayarak bakın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-179">See the details of an item in the live feed by clicking it.</span></span> <span data-ttu-id="2ffd0-180">Akış tıklayarak ya da duraklatabilir **duraklatma** yalnızca aşağı kaydırma veya bir öğeyi tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-180">You can pause the feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="2ffd0-181">Başa dön veya durdurulduğundan sırasında toplanan öğeleri sayaç tıklayarak kaydırma sonra canlı akış devam eder.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-181">Live feed will resume after you scroll back to the top, or by clicking the counter of items collected while it was paused.</span></span>

![Örneklenen Canlı hataları](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="2ffd0-183">Sunucu örneği tarafından filtre</span><span class="sxs-lookup"><span data-stu-id="2ffd0-183">Filter by server instance</span></span>

<span data-ttu-id="2ffd0-184">Belirli bir sunucu rolü örneği izlemek istiyorsanız, sunucu tarafından filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-184">If you want to monitor a particular server role instance, you can filter by server.</span></span>

![Örneklenen Canlı hataları](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="2ffd0-186">SDK gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="2ffd0-186">SDK Requirements</span></span>
<span data-ttu-id="2ffd0-187">Özel Canlı ölçümleri akış sürüm 2.4.0-beta2 bulunan ya da daha yeni olan [Application Insights SDK Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="2ffd0-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="2ffd0-188">NuGet Paket Yöneticisi'nden "Yayın öncesi Ekle" seçeneğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-188">Remember to select "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-the-control-channel"></a><span data-ttu-id="2ffd0-189">Denetim kanalının güvenliğini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-189">Secure the control channel</span></span>
<span data-ttu-id="2ffd0-190">Belirttiğiniz özel filtreler ölçütlere geri Application Insights SDK'sı Canlı ölçümleri bileşeni gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-190">The custom filters criteria you specify are sent back to the Live Metrics component in the Application Insights SDK.</span></span> <span data-ttu-id="2ffd0-191">Filtreler olası customerIDs gibi hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-191">The filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="2ffd0-192">Kanal güvenli izleme anahtarını ek olarak gizli bir API anahtarı ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-192">You can make the channel secure with a secret API key in addition to the instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="2ffd0-193">API anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ffd0-193">Create an API Key</span></span>

![API anahtarı oluşturma](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-to-configuration"></a><span data-ttu-id="2ffd0-195">API anahtarı yapılandırmasına ekleyin</span><span class="sxs-lookup"><span data-stu-id="2ffd0-195">Add API key to Configuration</span></span>
<span data-ttu-id="2ffd0-196">Applicationınsights.config dosyasında AuthenticationApiKey QuickPulseTelemetryModule ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2ffd0-196">In the applicationinsights.config file, add the AuthenticationApiKey to the QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="2ffd0-197">Veya isteğe bağlı olarak kod içinde üzerinde QuickPulseTelemetryModule ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2ffd0-197">Or in code, set it on the QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="2ffd0-198">Ancak, algılar ve tüm bağlı sunucular güveniyorsanız, kimliği doğrulanmış kanal olmadan özel filtreler deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-198">However, if you recognize and trust all the connected servers, you can try the custom filters without the authenticated channel.</span></span> <span data-ttu-id="2ffd0-199">Bu seçenek altı ay için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-199">This option is available for six months.</span></span> <span data-ttu-id="2ffd0-200">Bu geçersiz kılma kez her yeni bir oturum gereklidir veya ne zaman yeni bir sunucu gelir çevrimiçi.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-200">This override is required once every new session, or when a new server comes online.</span></span>

![Canlı ölçümleri kimlik doğrulama seçenekleri](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="2ffd0-202">Kimliği doğrulanmış kanalının filtre ölçütünü CustomerID gibi olası hassas bilgileri girmeden önce ayarlamak öneririz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-202">We strongly recommend that you set up the authenticated channel before entering potentially sensitive information like CustomerID in the filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="2ffd0-203">Performans testi yükleme oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ffd0-203">Generating a performance test load</span></span>

<span data-ttu-id="2ffd0-204">Bir yük artışı etkisini izlemek isterseniz, performansı Test dikey penceresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-204">If you want to watch the effect of a load increase, use the Performance Test blade.</span></span> <span data-ttu-id="2ffd0-205">Bu, eşzamanlı kullanıcıların sayısı gelen istekleri benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="2ffd0-206">Ya da "el ile testleri" çalıştırabilirsiniz (ping testleri) tek bir URL veya çalıştırabilirsiniz bir [çok adımlı web performans testi](app-insights-monitor-web-app-availability.md#multi-step-web-tests) (ile bir kullanılabilirlik test aynı şekilde) karşıya.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in the same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="2ffd0-207">Performans testi oluşturduktan sonra ayrı windows test ve canlı akış dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-207">After you create the performance test, open the test and the Live Stream blade in separate windows.</span></span> <span data-ttu-id="2ffd0-208">Sıraya alınan performans testi başladığında ve izleme canlı akış aynı anda görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-208">You can see when the queued performance test starts, and watch live stream at the same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="2ffd0-209">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="2ffd0-209">Troubleshooting</span></span>

<span data-ttu-id="2ffd0-210">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="2ffd0-210">No data?</span></span> <span data-ttu-id="2ffd0-211">Uygulamanızı korunan bir ağda ise: Canlı ölçümleri akış diğer Application Insights telemetri daha farklı bir IP adreslerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="2ffd0-212">Emin olun [bu IP adreslerinden](app-insights-ip-addresses.md) duvarınızda açıktır.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="2ffd0-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ffd0-213">Next steps</span></span>
* [<span data-ttu-id="2ffd0-214">Application Insights ile kullanım izleme</span><span class="sxs-lookup"><span data-stu-id="2ffd0-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="2ffd0-215">Tanılama aramayı kullanma</span><span class="sxs-lookup"><span data-stu-id="2ffd0-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="2ffd0-216">Profil Oluşturucu</span><span class="sxs-lookup"><span data-stu-id="2ffd0-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="2ffd0-217">Anlık görüntü hata ayıklayıcı</span><span class="sxs-lookup"><span data-stu-id="2ffd0-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
