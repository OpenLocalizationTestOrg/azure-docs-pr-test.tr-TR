---
title: "Özel olayları ve ölçümleri için Application Insights API'si | Microsoft Docs"
description: "Birkaç satır kod, cihaz veya masaüstü uygulaması, Web sayfası veya kullanımı izlemek ve sorunlarını tanılamak için hizmetinizi ekleyin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="b8756-103">Özel olayları ve ölçümleri için Application Insights API'si</span><span class="sxs-lookup"><span data-stu-id="b8756-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="b8756-104">Birkaç satır kod uygulamanızda kullanıcıların ne ile yaptıklarını bulmak için veya sorunları tanılamak için ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b8756-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="b8756-105">Aygıt ve Masaüstü uygulamaları, web istemcileri ve web sunucuları telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="b8756-106">Kullanım [Azure Application Insights](app-insights-overview.md) çekirdek özel olayları ve ölçümleri ve kendi sürümleri standart telemetri göndermeyi telemetri API'si.</span><span class="sxs-lookup"><span data-stu-id="b8756-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="b8756-107">Bu API standart Application Insights veri toplayıcıları kullanan aynı API'dir.</span><span class="sxs-lookup"><span data-stu-id="b8756-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="b8756-108">API özeti</span><span class="sxs-lookup"><span data-stu-id="b8756-108">API summary</span></span>
<span data-ttu-id="b8756-109">Birkaç küçük Çeşitlemeler dışında tüm platformlar genelinde Tekdüzen API'dir.</span><span class="sxs-lookup"><span data-stu-id="b8756-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="b8756-110">Yöntem</span><span class="sxs-lookup"><span data-stu-id="b8756-110">Method</span></span> | <span data-ttu-id="b8756-111">İçin kullanılır</span><span class="sxs-lookup"><span data-stu-id="b8756-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="b8756-112">Sayfalar, ekranlar, dikey veya formlar.</span><span class="sxs-lookup"><span data-stu-id="b8756-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="b8756-113">Kullanıcı eylemleri ve diğer olaylar.</span><span class="sxs-lookup"><span data-stu-id="b8756-113">User actions and other events.</span></span> <span data-ttu-id="b8756-114">Kullanıcı davranışı izlemek veya performansını izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b8756-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="b8756-115">Performans ölçümleri gibi sıra uzunlukları belirli olayları ile ilgili değildir.</span><span class="sxs-lookup"><span data-stu-id="b8756-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="b8756-116">Tanılama için günlük özel durumları.</span><span class="sxs-lookup"><span data-stu-id="b8756-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="b8756-117">İzleme burada bunlar ile ilgili diğer olaylar oluşur ve Yığın izlemeleri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b8756-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="b8756-118">Sunucu istek süresi Performans Analizi ve sıklığı günlüğü.</span><span class="sxs-lookup"><span data-stu-id="b8756-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="b8756-119">Tanılama günlük iletileri.</span><span class="sxs-lookup"><span data-stu-id="b8756-119">Diagnostic log messages.</span></span> <span data-ttu-id="b8756-120">Üçüncü taraf günlükleri de yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="b8756-121">Uygulamanızı bağlıdır dış bileşenlere çağrılar sıklığı ve süresi günlüğü.</span><span class="sxs-lookup"><span data-stu-id="b8756-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="b8756-122">Yapabilecekleriniz [özellikleri ve ölçümleri ekleme](#properties) bu telemetri çağrılardan bir çoğuna.</span><span class="sxs-lookup"><span data-stu-id="b8756-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="b8756-123"><a name="prep"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b8756-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="b8756-124">Application Insights SDK'sı üzerinde bir başvuru henüz yoksa:</span><span class="sxs-lookup"><span data-stu-id="b8756-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="b8756-125">Application Insights SDK'sı projenize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b8756-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="b8756-126">ASP.NET projesi</span><span class="sxs-lookup"><span data-stu-id="b8756-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="b8756-127">Java projesi</span><span class="sxs-lookup"><span data-stu-id="b8756-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="b8756-128">Her Web sayfasındaki JavaScript</span><span class="sxs-lookup"><span data-stu-id="b8756-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="b8756-129">Cihaz veya web sunucusu kodunuzda şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="b8756-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="b8756-130">*C# ' TA:*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="b8756-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="b8756-131">*Visual Basic:*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="b8756-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="b8756-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="b8756-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="b8756-133">Bir TelemetryClient örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="b8756-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="b8756-134">Olgusu `TelemetryClient` (Web sayfalarındaki JavaScript'te hariç):</span><span class="sxs-lookup"><span data-stu-id="b8756-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="b8756-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="b8756-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b8756-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="b8756-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="b8756-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="b8756-138">TelemetryClient iş parçacığı güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="b8756-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="b8756-139">Uygulamanızı her modül için TelemetryClient örneğini kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="b8756-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="b8756-140">Örneğin, gelen HTTP isteklerini ve başka bir ara yazılım sınıfında rapor iş mantığı olaylarını bildirmek için web hizmetiniz bir TelemetryClient örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="b8756-141">Özellikleri gibi ayarlayabilirsiniz `TelemetryClient.Context.User.Id` kullanıcılar ve oturumları izlemek için veya `TelemetryClient.Context.Device.Id` makine tanımlamak için.</span><span class="sxs-lookup"><span data-stu-id="b8756-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="b8756-142">Bu bilgiler örneği gönderdiği tüm olayları eklenir.</span><span class="sxs-lookup"><span data-stu-id="b8756-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="b8756-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="b8756-143">TrackEvent</span></span>
<span data-ttu-id="b8756-144">Application ınsights'ta bir *özel olay* içinde görüntüleyebilirsiniz bir veri noktası [ölçüm Gezgini](app-insights-metrics-explorer.md) toplanan sayılara olarak ve buna [tanılama arama](app-insights-diagnostic-search.md) olarak tek tek yineleme.</span><span class="sxs-lookup"><span data-stu-id="b8756-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="b8756-145">(Bu MVC veya diğer framework "olayları." ile ilişkili değil)</span><span class="sxs-lookup"><span data-stu-id="b8756-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="b8756-146">INSERT `TrackEvent` çeşitli olaylarının sayılacağı kodunuzda çağırır.</span><span class="sxs-lookup"><span data-stu-id="b8756-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="b8756-147">Ne sıklıkla kullanıcıların belirli bir özellik, ne sıklıkta bunlar belirli hedeflere ulaşmak veya hatalar belirli tür belki ne sıklıkta yaptıkları seçin.</span><span class="sxs-lookup"><span data-stu-id="b8756-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="b8756-148">Örneğin, bir oyun uygulamada bir kullanıcı oyun WINS bir olay gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="b8756-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="b8756-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="b8756-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="b8756-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b8756-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="b8756-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="b8756-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="b8756-153">Microsoft Azure Portalı'nda, olayları görüntülemek</span><span class="sxs-lookup"><span data-stu-id="b8756-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="b8756-154">Olaylarınızı sayısını görmek için açık bir [ölçüm Gezgini](app-insights-metrics-explorer.md) dikey penceresinde, yeni bir grafik ekleyin ve seçin **olayları**.</span><span class="sxs-lookup"><span data-stu-id="b8756-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Özel olaylar sayısını bakın](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="b8756-156">Farklı olayları sayısı karşılaştırmak için grafik türünü ayarlamak **kılavuz**ve olay adı tarafından Grup:</span><span class="sxs-lookup"><span data-stu-id="b8756-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![Gruplandırma ve grafik türünü ayarlayın](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="b8756-158">Kılavuzda, bu olay oluşumlarını görmek için bir olay adı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b8756-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="b8756-159">Daha fazla ayrıntı - listedeki olayı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b8756-159">To see more detail - click any occurrence in the list.</span></span>

![Aracılığıyla olaylarını incelemek](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="b8756-161">Arama veya ölçüm Gezgini belirli olayları odaklanmak için dikey 's filtresi ilgilendiğiniz olay adları ayarla:</span><span class="sxs-lookup"><span data-stu-id="b8756-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![Filtreler açın, olay adı'nı genişletin ve bir veya daha fazla değerleri seçin](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="b8756-163">Analytics'te özel olaylar</span><span class="sxs-lookup"><span data-stu-id="b8756-163">Custom events in Analytics</span></span>

<span data-ttu-id="b8756-164">Telemetriyi kullanılabilir `customEvents` tablosundaki [uygulama Öngörüler Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="b8756-165">Her satır için bir çağrı temsil eden `trackEvent(..)` uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="b8756-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="b8756-166">Varsa [örnekleme](app-insights-sampling.md) içinde ItemCount özelliği 1'den büyük bir değer gösterir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b8756-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b8756-167">Örnek ItemCount == trackEvent() için 10 çağrıları, örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b8756-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b8756-168">Özel olaylar doğru sayısını almak için bu nedenle kullanım kodu gibi kullanmalısınız `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="b8756-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="b8756-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="b8756-169">TrackMetric</span></span>

<span data-ttu-id="b8756-170">Application Insights belirli olaylara bağlı olmayan ölçümleri grafik.</span><span class="sxs-lookup"><span data-stu-id="b8756-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="b8756-171">Örneğin, bir kuyruk uzunluğu düzenli aralıklarla izlemek.</span><span class="sxs-lookup"><span data-stu-id="b8756-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="b8756-172">Ölçümleri, bağımsız değişkenleri ve eğilimleri daha az ilgi ölçümlerdir ve böylece istatistiksel grafikler kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b8756-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="b8756-173">Ölçümleri Application Insights'a gönderme için kullanabileceğiniz `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="b8756-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="b8756-174">Ölçüm göndermek için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="b8756-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="b8756-175">Tek bir değer.</span><span class="sxs-lookup"><span data-stu-id="b8756-175">Single value.</span></span> <span data-ttu-id="b8756-176">Uygulamanızda bir ölçüm gerçekleştirdiğiniz her zaman, karşılık gelen değerle Application Insights'a gönderme.</span><span class="sxs-lookup"><span data-stu-id="b8756-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="b8756-177">Örneğin, bir kapsayıcı öğe sayısını açıklayan bir ölçüm olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b8756-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="b8756-178">Belirli bir zaman diliminde ilk üç öğeleri kapsayıcıya yerleştirdiğiniz ve ardından iki öğeyi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b8756-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="b8756-179">Buna göre çağırırdı `TrackMetric` iki kez: ilk değer geçirme `3` ve ardından değeri `-2`.</span><span class="sxs-lookup"><span data-stu-id="b8756-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="b8756-180">Application Insights, sizin adınıza her iki değerin de depolar.</span><span class="sxs-lookup"><span data-stu-id="b8756-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="b8756-181">Toplama.</span><span class="sxs-lookup"><span data-stu-id="b8756-181">Aggregation.</span></span> <span data-ttu-id="b8756-182">Ölçümleri ile çalışırken, her tek nadiren ilgi ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="b8756-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="b8756-183">Bunun yerine belirli bir süre içinde ne Özet önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b8756-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="b8756-184">Bu tür bir özeti adlı _toplama_.</span><span class="sxs-lookup"><span data-stu-id="b8756-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="b8756-185">Yukarıdaki örnekte, toplama ölçüm bu döneme ait toplamıdır `1` ve ölçüm değerlerin sayısını `2`.</span><span class="sxs-lookup"><span data-stu-id="b8756-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="b8756-186">Toplama yaklaşım kullanırken, yalnızca çağırma `TrackMetric` zaman süresi başına bir kez ve toplam değerler gönderin.</span><span class="sxs-lookup"><span data-stu-id="b8756-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="b8756-187">Bu önemli ölçüde performans ve maliyet ek yükü daha az veri noktası Application Insights'a hala ilgili tüm bilgileri toplanırken göndererek küçültebilirsiniz beri önerilen yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="b8756-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="b8756-188">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="b8756-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="b8756-189">Tek değer</span><span class="sxs-lookup"><span data-stu-id="b8756-189">Single values</span></span>

<span data-ttu-id="b8756-190">Tek bir ölçü değeri göndermek için:</span><span class="sxs-lookup"><span data-stu-id="b8756-190">To send a single metric value:</span></span>

<span data-ttu-id="b8756-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="b8756-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="b8756-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="b8756-193">Ölçümleri toplama</span><span class="sxs-lookup"><span data-stu-id="b8756-193">Aggregating metrics</span></span>

<span data-ttu-id="b8756-194">Birleşik ölçümleri uygulamanızdan göndermeden önce önerilir, bant genişliğini azaltmak için maliyet ve performansı artırmak için.</span><span class="sxs-lookup"><span data-stu-id="b8756-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="b8756-195">Kod bir araya getirildiği bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b8756-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="b8756-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="b8756-197">Ölçümleri Explorer'da özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="b8756-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="b8756-198">Sonuçları görmek için ölçümleri Gezgini'ni açın ve yeni bir grafik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b8756-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="b8756-199">Ölçüm göstermek için grafik düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="b8756-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="b8756-200">Özel ölçüm, kullanılabilir ölçümlere listesinde görünmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![Yeni bir grafik ekleyin veya bir grafik seçin ve özel altında ölçüm seçin](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="b8756-202">Analytics'te özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="b8756-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="b8756-203">Telemetriyi kullanılabilir `customMetrics` tablosundaki [uygulama Öngörüler Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="b8756-204">Her satır için bir çağrı temsil eden `trackMetric(..)` uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="b8756-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="b8756-205">`valueSum`-Bu ölçümler toplamıdır.</span><span class="sxs-lookup"><span data-stu-id="b8756-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="b8756-206">Ortalama değer almak için bölün `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="b8756-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="b8756-207">`valueCount`-Bu toplanan ölçümleri sayısını `trackMetric(..)` çağırın.</span><span class="sxs-lookup"><span data-stu-id="b8756-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="b8756-208">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="b8756-208">Page views</span></span>
<span data-ttu-id="b8756-209">Her ekranı veya sayfa yüklendiğinde, bir aygıt veya Web sayfası uygulamasında varsayılan olarak sayfa görünümü telemetrisi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="b8756-210">Ancak, sayfa görünümleri ek veya farklı zamanlarda izlemek için değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="b8756-211">Örneğin, sekmeler veya dikey pencereler görüntüleyen bir uygulama, kullanıcının yeni bir dikey pencere açıldığında bir sayfayı izlemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![Genel Bakış dikey penceresinde kullanım Mercek](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="b8756-213">Sayfa görünümü telemetrisi olduğunda kullanıcı ve oturum grafikleri Canlı gelmesi için kullanıcı ve oturum verilerini sayfa görünümleri birlikte özellikleri olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="b8756-214">Özel sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="b8756-214">Custom page views</span></span>
<span data-ttu-id="b8756-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="b8756-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="b8756-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b8756-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="b8756-218">Farklı HTML sayfaları içinde birden çok sekme varsa, URL çok belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b8756-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="b8756-219">Zamanlama sayfası görünümleri</span><span class="sxs-lookup"><span data-stu-id="b8756-219">Timing page views</span></span>
<span data-ttu-id="b8756-220">Varsayılan olarak, kez bildirildi **sayfa görünümü yükleme süresi** tarayıcı isteği gönderdiğinde tarayıcının sayfası yük olayı çağrılıncaya kadar gelen ölçülür.</span><span class="sxs-lookup"><span data-stu-id="b8756-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="b8756-221">Bunun yerine, şunlardan birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b8756-221">Instead, you can either:</span></span>

* <span data-ttu-id="b8756-222">Açık bir süre kümesinde [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) çağırın: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="b8756-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="b8756-223">Çağrıları zamanlama sayfası görünümü kullanmak `startTrackPage` ve `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="b8756-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="b8756-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="b8756-225">...</span><span class="sxs-lookup"><span data-stu-id="b8756-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="b8756-226">İlk parametre olarak kullandığınız adı başlatma ve durdurma çağrıları ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="b8756-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="b8756-227">Geçerli sayfa adı varsayar.</span><span class="sxs-lookup"><span data-stu-id="b8756-227">It defaults to the current page name.</span></span>

<span data-ttu-id="b8756-228">Ölçümleri Gezgini'nde görüntülenen sonuç sayfa yükleme süreleri başlatma ve durdurma çağrıları arasındaki aralığı türetilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="b8756-229">Bu size gerçekten zaman hangi aralığı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b8756-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="b8756-230">Sayfa telemetri analizi</span><span class="sxs-lookup"><span data-stu-id="b8756-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="b8756-231">İçinde [Analytics](app-insights-analytics.md) iki tablo tarayıcı işlemleri verileri göster:</span><span class="sxs-lookup"><span data-stu-id="b8756-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="b8756-232">`pageViews` Tablosu URL ve sayfa başlığını hakkındaki verileri içerir</span><span class="sxs-lookup"><span data-stu-id="b8756-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="b8756-233">`browserTimings` Tablosu gelen verileri işlemek için geçen süre gibi istemci performansı hakkında veri içerir</span><span class="sxs-lookup"><span data-stu-id="b8756-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="b8756-234">Tarayıcı farklı sayfaları işlemek için gereken süreyi bulmak için:</span><span class="sxs-lookup"><span data-stu-id="b8756-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="b8756-235">Farklı tarayıcılar popularities bulmak için:</span><span class="sxs-lookup"><span data-stu-id="b8756-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="b8756-236">Sayfa görünümleri AJAX çağrıları ilişkilendirilecek bağımlılıklarla Katıl:</span><span class="sxs-lookup"><span data-stu-id="b8756-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="b8756-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="b8756-237">TrackRequest</span></span>
<span data-ttu-id="b8756-238">SDK sunucusu, HTTP isteklerini günlüğe kaydetmek için TrackRequest kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8756-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="b8756-239">İstekleri bir bağlamda benzetimini yapmak istiyorsanız, ayrıca kendiniz çalışan web hizmeti modülü burada yok çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="b8756-240">Ancak, istek telemetri göndermek için önerilen burada isteği görevi gören yoludur bir <a href="#operation-context">işlemi bağlam</a>.</span><span class="sxs-lookup"><span data-stu-id="b8756-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="b8756-241">İşlem bağlamı</span><span class="sxs-lookup"><span data-stu-id="b8756-241">Operation context</span></span>
<span data-ttu-id="b8756-242">Ortak bir işlem kimliği ekleyerek bunları telemetri öğelerini birlikte ilişkilendirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="b8756-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="b8756-243">Standart isteği izleme modülü, özel durumlar ve bir HTTP istek gerçekleştirilirken gönderilen diğer olayları için bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="b8756-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="b8756-244">İçinde [arama](app-insights-diagnostic-search.md) ve [Analytics](app-insights-analytics.md), kimliği istekle ilişkili tüm olayları kolayca bulmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="b8756-245">En kolay yolu Kimliğini ayarlamak için bu yöntemi kullanarak bir işlem bağlamı ayarlamaktır:</span><span class="sxs-lookup"><span data-stu-id="b8756-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="b8756-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="b8756-247">Bir işlemin bağlamını ayarlanması birlikte `StartOperation` telemetri öğesi, belirttiğiniz türü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b8756-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="b8756-248">İşlemi çıkardığınızda veya açıkça çağırırsanız telemetri öğesi gönderir `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="b8756-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="b8756-249">Kullanırsanız `RequestTelemetry` telemetri türü olarak başlatma ve durdurma arasında zaman aralıklarında süresinin ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b8756-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="b8756-250">İşlem bağlamı iç içe olamaz.</span><span class="sxs-lookup"><span data-stu-id="b8756-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="b8756-251">Bir işlem bağlamı zaten var. sonra Kimliğini ile oluşturulan öğesi de dahil olmak üzere içerilen tüm öğelerin ilişkilendirildiği `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="b8756-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="b8756-252">Aramada, işlem bağlamı oluşturmak için kullanılan **ilgili öğeler** listesi:</span><span class="sxs-lookup"><span data-stu-id="b8756-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![İlgili öğeler](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="b8756-254">[Uygulama-Öngörüler-özel-işlemleri-tracking.md] izleme özel işlemler hakkında daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="b8756-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="b8756-255">Analytics istekleri</span><span class="sxs-lookup"><span data-stu-id="b8756-255">Requests in Analytics</span></span> 

<span data-ttu-id="b8756-256">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), içinde Göster istekleri `requests` tablo.</span><span class="sxs-lookup"><span data-stu-id="b8756-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="b8756-257">Varsa [örnekleme](app-insights-sampling.md) olduğundan, işlem ItemCount özelliği bir değer 1'den büyük gösterir.</span><span class="sxs-lookup"><span data-stu-id="b8756-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="b8756-258">Örnek ItemCount == trackRequest() için 10 çağrıları, örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b8756-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b8756-259">İstek ve istek adlarıyla kesimli ortalama süresi doğru sayısı almak için kodu gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="b8756-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="b8756-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="b8756-260">TrackException</span></span>
<span data-ttu-id="b8756-261">Özel durumlar Application Insights'a gönderme:</span><span class="sxs-lookup"><span data-stu-id="b8756-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="b8756-262">İçin [saymanız](app-insights-metrics-explorer.md), bir sorun sıklığını belirtisi olarak.</span><span class="sxs-lookup"><span data-stu-id="b8756-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="b8756-263">İçin [ayrı ayrı oluşumları inceleyin](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b8756-264">Raporları Yığın izlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b8756-264">The reports include the stack traces.</span></span>

<span data-ttu-id="b8756-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="b8756-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="b8756-267">Her zaman TrackException açıkça çağırın zorunda kalmamak için SDK'ları birçok özel durumlarını otomatik olarak yakalama.</span><span class="sxs-lookup"><span data-stu-id="b8756-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="b8756-268">ASP.NET: [özel durumları yakalamak için kod yazma](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="b8756-269">J2EE: [özel durumları yakalanan otomatik olarak](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="b8756-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="b8756-270">JavaScript: Özel durumları otomatik olarak yakalanır.</span><span class="sxs-lookup"><span data-stu-id="b8756-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="b8756-271">Otomatik olarak toplanmasını devre dışı bırakmak istiyorsanız, bir satırı, Web sayfalarındaki Ekle kod parçacığını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b8756-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="b8756-272">Analytics özel durumları</span><span class="sxs-lookup"><span data-stu-id="b8756-272">Exceptions in Analytics</span></span>

<span data-ttu-id="b8756-273">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), özel durumlar gösterilmiyor `exceptions` tablo.</span><span class="sxs-lookup"><span data-stu-id="b8756-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="b8756-274">Varsa [örnekleme](app-insights-sampling.md) işlem içinde `itemCount` özelliği değeri 1'den büyük gösterir.</span><span class="sxs-lookup"><span data-stu-id="b8756-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="b8756-275">Örnek ItemCount == 10 trackException() çağrıları ekleme, örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b8756-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b8756-276">Özel durum türüne göre kesimli özel durumlarının doğru bir sayıyı almak için kodu gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="b8756-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="b8756-277">Önemli yığın bilgilerin çoğunu ayrı değişkenlere zaten ayıklanan ancak birbirinden çekme `details` daha fazlasına yapısı.</span><span class="sxs-lookup"><span data-stu-id="b8756-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="b8756-278">Bu yapı dinamik olduğundan, beklediğiniz türü sonucu atamalısınız.</span><span class="sxs-lookup"><span data-stu-id="b8756-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="b8756-279">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b8756-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="b8756-280">Özel durumlar ilgili isteklerinde ile ilişkilendirilecek bir birleşim kullanın:</span><span class="sxs-lookup"><span data-stu-id="b8756-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="b8756-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="b8756-281">TrackTrace</span></span>
<span data-ttu-id="b8756-282">Application Insights "içerik haritası Kılavuzu" göndererek sorunların tanılanmasına yardımcı olmak için TrackTrace kullanın.</span><span class="sxs-lookup"><span data-stu-id="b8756-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="b8756-283">Tanılama veri öbekleri göndermek ve bunları inceleyin [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b8756-284">[Oturum bağdaştırıcıları](app-insights-asp-net-trace-logs.md) portalına üçüncü taraf günlükleri göndermek için bu API'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="b8756-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="b8756-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="b8756-286">İleti içeriği arama yapabilirsiniz ancak (özellik değerlerini), üzerinde filtre uygulayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b8756-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="b8756-287">Boyut sınırını `message` özellikleri sınırından daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="b8756-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="b8756-288">TrackTrace avantajı, iletide oldukça uzun veri koyabilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="b8756-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="b8756-289">Örneğin, POST verilerini şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="b8756-290">Ayrıca, bir önem düzeyi iletinize ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="b8756-291">Ve diğer telemetri gibi filtre veya arama izlemeleri farklı kümeleri için yardımcı olmak için özellik değerlerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="b8756-292">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b8756-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="b8756-293">İçinde [arama](app-insights-diagnostic-search.md), daha sonra kolayca belirli bir veritabanı ile ilgili tüm iletileri belirli önem düzeyine sahip bir filtre.</span><span class="sxs-lookup"><span data-stu-id="b8756-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="b8756-294">İçindeki analizi</span><span class="sxs-lookup"><span data-stu-id="b8756-294">Traces in Analytics</span></span>

<span data-ttu-id="b8756-295">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), TrackTrace çağrıları gösterilmiyor `traces` tablo.</span><span class="sxs-lookup"><span data-stu-id="b8756-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="b8756-296">Varsa [örnekleme](app-insights-sampling.md) içinde ItemCount özelliği 1'den büyük bir değer gösterir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b8756-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b8756-297">Örnek ItemCount == 10, 10 çağrı anlamına gelir `trackTrace()`, örnekleme işlemi yalnızca bunlardan birinin aktarılan.</span><span class="sxs-lookup"><span data-stu-id="b8756-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b8756-298">İzleme çağrıları doğru sayısını almak için bu nedenle kod gibi kullanmalısınız `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="b8756-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="b8756-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="b8756-299">TrackDependency</span></span>
<span data-ttu-id="b8756-300">TrackDependency çağrısı bir dış kod parçası, yapılan çağrıların başarı oranları ve yanıt sürelerini izlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b8756-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="b8756-301">Sonuçlar portalında bağımlılık grafiklerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b8756-301">The results appear in the dependency charts in the portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="b8756-302">Sunucu SDK'ları içerdiğini unutmayın bir [bağımlılık Modülü](app-insights-asp-net-dependencies.md) bulur ve bazı bağımlılık çağrıları otomatik olarak--Örneğin, veritabanları ve REST API'leri izler.</span><span class="sxs-lookup"><span data-stu-id="b8756-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="b8756-303">İş modülü yapmak için sunucunuzda bir aracı yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8756-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="b8756-304">Bu çağrı otomatik izleme catch değil çağrılarını izlemek istiyorsanız veya aracıyı yüklemek istemiyorsanız kullanın.</span><span class="sxs-lookup"><span data-stu-id="b8756-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="b8756-305">Standart bağımlılık izleme modülünü devre dışı bırakmak için düzenleme [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) ve başvuru silme `DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="b8756-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="b8756-306">Analytics bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="b8756-306">Dependencies in Analytics</span></span>

<span data-ttu-id="b8756-307">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), trackDependency çağrıları Göster `dependencies` tablo.</span><span class="sxs-lookup"><span data-stu-id="b8756-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="b8756-308">Varsa [örnekleme](app-insights-sampling.md) içinde ItemCount özelliği 1'den büyük bir değer gösterir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b8756-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b8756-309">Örnek ItemCount == trackDependency() için 10 çağrıları, örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b8756-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b8756-310">Hedef bileşen tarafından kesimli bağımlılıkların doğru bir sayıyı almak için kodu gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="b8756-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="b8756-311">Bağımlılıkları ile ilgili isteklerinde ilişkilendirilecek bir birleşim kullanın:</span><span class="sxs-lookup"><span data-stu-id="b8756-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="b8756-312">Düzenleniyor veri</span><span class="sxs-lookup"><span data-stu-id="b8756-312">Flushing data</span></span>
<span data-ttu-id="b8756-313">Normalde, SDK zamanlarda kullanıcı üzerindeki etkiyi en aza indirmek için seçilen verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="b8756-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="b8756-314">Uygulamada kapandıktan SDK kullanıyorsanız, ancak, bazı durumlarda, arabellek--Örneğin, temizlemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="b8756-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="b8756-316">İşlevi için zaman uyumsuz olduğuna dikkat edin [server telemetri kanalı](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="b8756-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="b8756-317">Kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="b8756-317">Authenticated users</span></span>
<span data-ttu-id="b8756-318">Bir web uygulaması, kullanıcıların (varsayılan) tanımlama bilgileri tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="b8756-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="b8756-319">Bir kullanıcı birden çok kez uygulamanız farklı makine ya da tarayıcı erişimi engelliyorsa veya tanımlama bilgilerini sildiğinizde sayılması.</span><span class="sxs-lookup"><span data-stu-id="b8756-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="b8756-320">Kullanıcılar uygulamanıza oturum açarsa, tarayıcı kodda kimliği doğrulanmış kullanıcı kimliği ayarlayarak daha doğru bir sayı elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b8756-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="b8756-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="b8756-322">Bir ASP.NET web örneğin MVC uygulaması:</span><span class="sxs-lookup"><span data-stu-id="b8756-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="b8756-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="b8756-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="b8756-324">Oturum açma kullanıcı asıl adını kullanmak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="b8756-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="b8756-325">Yalnızca o kullanıcı için benzersiz bir kimliği olmak zorundadır.</span><span class="sxs-lookup"><span data-stu-id="b8756-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="b8756-326">Boşluk veya karakterlerden herhangi birini içermemelidir `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="b8756-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="b8756-327">Kullanıcı Kimliği ayrıca bir oturum tanımlama bilgisinde ayarlamak ve sunucuya gönderilen.</span><span class="sxs-lookup"><span data-stu-id="b8756-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="b8756-328">SDK sunucusu yüklediyseniz, kimliği doğrulanmış kullanıcı kimliği hem istemci hem de sunucu telemetri bağlamı özelliklerini bir parçası olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="b8756-329">Daha sonra filtre ve onu Search'te.</span><span class="sxs-lookup"><span data-stu-id="b8756-329">You can then filter and search on it.</span></span>

<span data-ttu-id="b8756-330">Uygulamanız kullanıcıların hesaplara grupları varsa, (aynı karakter kısıtlamalarla birlikte) hesabı için bir tanıtıcı geçiş yapabilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="b8756-331">İçinde [ölçüm Gezgini](app-insights-metrics-explorer.md), sayar bir grafik oluşturabilirsiniz **kimliği doğrulanmış kullanıcılar,**, ve **kullanıcı hesaplarını**.</span><span class="sxs-lookup"><span data-stu-id="b8756-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="b8756-332">Ayrıca [arama](app-insights-diagnostic-search.md) belirli kullanıcı adları ve hesapları ile istemci veri noktaları için.</span><span class="sxs-lookup"><span data-stu-id="b8756-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="b8756-333"><a name="properties"></a>Filtreleme, aramayı ve özelliklerini kullanarak verilerinizi kesimlere</span><span class="sxs-lookup"><span data-stu-id="b8756-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="b8756-334">Özellikleri ve ölçülerini, olaylar ekleme (ve ayrıca ölçümlere görünümleri, özel durumlar ve diğer telemetri verilerini sayfasında).</span><span class="sxs-lookup"><span data-stu-id="b8756-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="b8756-335">*Özellikler* kullanım raporlarında telemetrinizi filtrelemek için kullanabileceğiniz dize değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="b8756-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="b8756-336">Örneğin, uygulamanızı birkaç oyunlar sağlıyorsa, oyunun adından da her olay için ekleyebilirsiniz, böylece hangi oyunlar daha popüler görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="b8756-337">8192 bir dize uzunluk sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="b8756-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="b8756-338">(Büyük veri parçalarını göndermek istiyorsanız, ileti parametresini kullanmak [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="b8756-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="b8756-339">*Ölçümleri* grafik sunulan sayısal değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="b8756-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="b8756-340">Örneğin, aşamalı bir artış, oyun severler elde puanları içinde olup olmadığını görmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="b8756-341">Böylece ayrı alabilir grafikleri olay ile gönderilen özelliklerine göre kesimlere ayrılmıştır veya yığın grafik farklı oyunlar için.</span><span class="sxs-lookup"><span data-stu-id="b8756-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="b8756-342">Ölçüm değerleri doğru görüntülenebilmesi için bunlar büyük veya 0 değerine eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b8756-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="b8756-343">Bazı vardır [özellikleri, özellik değerlerini ve ölçümleri sayısı sınırları](#limits) kullanabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="b8756-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="b8756-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="b8756-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b8756-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="b8756-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="b8756-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="b8756-348">Kişisel bilgi özelliklerinde oturum değil dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="b8756-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="b8756-349">*Ölçümleri kullandıysanız*, ölçümleri Gezgini'ni açın ve gelen ölçümü seçin **özel** Grup:</span><span class="sxs-lookup"><span data-stu-id="b8756-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![Ölçümleri Gezgini'ni açın, grafiği seçin ve ölçümü seçin](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="b8756-351">Ölçüm görünmüyorsa veya **özel** başlık değil vardır, seçimi dikey penceresini kapatın ve daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="b8756-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="b8756-352">Ölçümleri bazen ardışık düzen üzerinden toplanacak bir saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="b8756-353">*Özellikleri ve ölçümleri kullandıysanız*, ölçüm özelliği tarafından segmentlere:</span><span class="sxs-lookup"><span data-stu-id="b8756-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![Gruplandırma ayarlayın ve ardından grupla altında özellik seçin](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="b8756-355">*Tanılama arama*, özellikleri ve bir olay oluşumlarını ölçümlerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![Bir örnek seçin ve ardından "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="b8756-357">Kullanım **arama** belirli bir özellik değeri olan olay örnekleri görmek için alanı.</span><span class="sxs-lookup"><span data-stu-id="b8756-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![Arama terimi yazın](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="b8756-359">[Arama ifadeleri hakkında daha fazla bilgi](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="b8756-360">Özellikler ve ölçümleri ayarlamak için alternatif yol</span><span class="sxs-lookup"><span data-stu-id="b8756-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="b8756-361">Daha kullanışlı ise, ayrı bir nesne olayda parametrelerinin toplayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b8756-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="b8756-362">Aynı telemetriyi öğesi örneği yeniden yok (`event` Bu örnekte) Track*() birden çok kez çağrılması.</span><span class="sxs-lookup"><span data-stu-id="b8756-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="b8756-363">Bu yanlış yapılandırma ile gönderilecek telemetri neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="b8756-364">Özel ölçümleri ve analizi özellikleri</span><span class="sxs-lookup"><span data-stu-id="b8756-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="b8756-365">İçinde [Analytics](app-insights-analytics.md), özel Ölçümler ve özelliklerini göster `customMeasurements` ve `customDimensions` her telemetri kayıt öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="b8756-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="b8756-366">Örneğin, istek telemetrinizi "oyuna" adlı bir özellik eklediyseniz, bu sorgu "oyunun" farklı değerler oluşumlarını sayar ve özel ölçüm "puan" ortalama göster:</span><span class="sxs-lookup"><span data-stu-id="b8756-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="b8756-367">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="b8756-367">Notice that:</span></span>

* <span data-ttu-id="b8756-368">Bir değer customDimensions ya da customMeasurements JSON ayıkladığınızda, dinamik türüne sahip ve bu nedenle, gereken cast onu `tostring` veya `todouble`.</span><span class="sxs-lookup"><span data-stu-id="b8756-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="b8756-369">Hesaba olasılığı için [örnekleme](app-insights-sampling.md), kullanmanız gereken `sum(itemCount)`değil `count()`.</span><span class="sxs-lookup"><span data-stu-id="b8756-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="b8756-370"><a name="timed"></a>Zamanlama olayları</span><span class="sxs-lookup"><span data-stu-id="b8756-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="b8756-371">Bazen bir eylemi gerçekleştirmek için gereken süreyi grafik istersiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="b8756-372">Örneğin, ne kadar kullanıcılar bilmek isteyebilirsiniz oyun seçimlerini göz önüne alın.</span><span class="sxs-lookup"><span data-stu-id="b8756-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="b8756-373">Bu ölçüm parametresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="b8756-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="b8756-375"><a name="defaults"></a>Özel telemetri için varsayılan özellikler</span><span class="sxs-lookup"><span data-stu-id="b8756-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="b8756-376">Varsayılan özellik değerleri bazı yazdığınız özel olaylar için ayarlamak istiyorsanız, bunları TelemetryClient örneğinde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="b8756-377">Bu istemciden gönderilen her telemetri öğesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="b8756-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="b8756-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="b8756-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b8756-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="b8756-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="b8756-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="b8756-381">Tek tek telemetri çağrıları kendi özelliği sözlükler varsayılan değerleri geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="b8756-382">*JavaScript için web istemcileri*, [JavaScript telemetri başlatıcıları kullanmak](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="b8756-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="b8756-383">*Tüm telemetri özellikleri eklemek için*, standart toplama modüllerden verileri dahil olmak üzere [uygulamak `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="b8756-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="b8756-384">Örnekleme, filtreleme ve telemetri işleniyor</span><span class="sxs-lookup"><span data-stu-id="b8756-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="b8756-385">SDK'dan gelen gönderilmeden önce telemetri işlemek üzere kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="b8756-386">İşleme HTTP isteği koleksiyonu ve bağımlılık koleksiyonu gibi standart telemetri modüllerden gönderilen veriler içerir.</span><span class="sxs-lookup"><span data-stu-id="b8756-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="b8756-387">[Özellikler ekleme](app-insights-api-filtering-sampling.md#add-properties) uygulayarak telemetri için `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="b8756-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="b8756-388">Örneğin, diğer özelliklerinden sürüm numaraları veya hesaplanan değerler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="b8756-389">[Filtreleme](app-insights-api-filtering-sampling.md#filtering) değiştirebilir veya SDK'dan gelen uygulayarak gönderilmeden önce telemetri atmak `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="b8756-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="b8756-390">Ne gönderildiğinde veya atılan denetlemek, ancak ölçümlerinizi etkisi hesaba sahip.</span><span class="sxs-lookup"><span data-stu-id="b8756-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="b8756-391">Öğeler atılsın nasıl bağlı olarak, ilgili öğeleri arasında gezinme becerisini kaybedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="b8756-392">[Örnekleme](app-insights-api-filtering-sampling.md) uygulamanızdan portala gönderilen verilerin hacmi azaltmak için paketlenmiş bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="b8756-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="b8756-393">Bunu görüntülenen ölçümlerin etkilemeden yapar.</span><span class="sxs-lookup"><span data-stu-id="b8756-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="b8756-394">Ve bunu özel durumlar, istekleri ve sayfa görünümleri gibi ilgili öğeleri arasında gezinme tarafından sorunları tanılama yeteneğinizi etkilemeden yapar.</span><span class="sxs-lookup"><span data-stu-id="b8756-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="b8756-395">[Daha fazla bilgi edinin](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="b8756-396">Telemetri devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="b8756-396">Disabling telemetry</span></span>
<span data-ttu-id="b8756-397">İçin *dinamik olarak durdurmak ve başlatmak* telemetri iletimini ve koleksiyon:</span><span class="sxs-lookup"><span data-stu-id="b8756-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="b8756-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="b8756-399">İçin *seçili standart toplayıcıları devre dışı*--Örneğin, performans sayaçları, HTTP isteklerini veya bağımlılıkları--silin veya açıklama ilgili satırları çıkışı [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md). Örneğin, kendi TrackRequest veri göndermek istiyorsanız, bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="b8756-400"><a name="debug"></a>Geliştirici modu</span><span class="sxs-lookup"><span data-stu-id="b8756-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="b8756-401">Hata ayıklama sırasında sonuçları hemen görebilmeniz için ardışık düzen üzerinden öncelikli telemetrinizi sağlamak kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b8756-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="b8756-402">Size yardımcı ayrıca get ek ileti telemetri herhangi bir sorun izleme.</span><span class="sxs-lookup"><span data-stu-id="b8756-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="b8756-403">Uygulamanızı azaltabileceğinden, bir üretim ortamına kapatın.</span><span class="sxs-lookup"><span data-stu-id="b8756-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="b8756-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="b8756-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b8756-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="b8756-406"><a name="ikey"></a>Seçili özel telemetri izleme anahtarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="b8756-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="b8756-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="b8756-408"><a name="dynamic-ikey"></a>Dinamik izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="b8756-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="b8756-409">Geliştirme, test ve üretim ortamlarını telemetri karıştırma önlemek için şunları yapabilirsiniz [ayrı Application Insights kaynakları oluşturmak](app-insights-create-new-resource.md) ve kendi anahtarları ortamına bağlı olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b8756-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="b8756-410">Yapılandırma dosyasından izleme anahtarını almak yerine onu kodunuzda ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="b8756-411">Anahtar başlatma yöntemini, bir ASP.NET hizmetinde global.aspx.cs gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="b8756-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="b8756-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="b8756-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="b8756-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b8756-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="b8756-414">Web sayfalarındaki, web sunucusunun durumu, yerine tam anlamıyla betiğe kodlama ayarlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="b8756-415">Bir ASP.NET uygulamasında oluşturulan Örneğin, bir Web sayfasında:</span><span class="sxs-lookup"><span data-stu-id="b8756-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="b8756-416">*Razor JavaScript'te*</span><span class="sxs-lookup"><span data-stu-id="b8756-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="b8756-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="b8756-417">TelemetryContext</span></span>
<span data-ttu-id="b8756-418">TelemetryClient tüm telemetri verilerinin yanı sıra gönderilen değerleri içeren bir içerik özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="b8756-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="b8756-419">Normalde standart telemetri modülleri tarafından ayarlanmış, ancak Ayrıca bunları kendiniz ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="b8756-420">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b8756-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="b8756-421">Bu değerleri kendiniz ayarlarsanız, ilgili satırından kaldırmayı düşünün [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), böylece bilgilerinizi ve standart değerlerini kafası yok.</span><span class="sxs-lookup"><span data-stu-id="b8756-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="b8756-422">**Bileşen**: uygulama ve onun sürümü.</span><span class="sxs-lookup"><span data-stu-id="b8756-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="b8756-423">**Aygıt**: uygulamanın çalıştığı cihaz hakkındaki verileri.</span><span class="sxs-lookup"><span data-stu-id="b8756-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="b8756-424">(Web uygulamalarında sunucu veya telemetri gönderilen istemci aygıt budur.)</span><span class="sxs-lookup"><span data-stu-id="b8756-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="b8756-425">**InstrumentationKey**: Application Insights kaynağı telemetri göründüğü azure'da.</span><span class="sxs-lookup"><span data-stu-id="b8756-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="b8756-426">Bu genellikle Applicationınsights.config kayıt.</span><span class="sxs-lookup"><span data-stu-id="b8756-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="b8756-427">**Konum**: cihazın coğrafi konumunu.</span><span class="sxs-lookup"><span data-stu-id="b8756-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="b8756-428">**İşlem**: web uygulamalarında, geçerli HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="b8756-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="b8756-429">Diğer uygulama türleri, bu Grup olaylarına birlikte ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8756-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="b8756-430">**Kimliği**: öğeleri ilişkili herhangi bir olay tanılama arama incelediğinizde, bulabilmesi için farklı olayları, karşılık gelen oluşturulan bir değer.</span><span class="sxs-lookup"><span data-stu-id="b8756-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="b8756-431">**Ad**: bir tanımlayıcı, genellikle HTTP istek URL'si.</span><span class="sxs-lookup"><span data-stu-id="b8756-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="b8756-432">**SyntheticSource**: değilse null veya boş, isteğin kaynak robot veya web testine belirlenmiştir gösteren bir dize.</span><span class="sxs-lookup"><span data-stu-id="b8756-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="b8756-433">Varsayılan olarak, ölçüm Gezgini hesaplamalarda gelen dışlanır.</span><span class="sxs-lookup"><span data-stu-id="b8756-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="b8756-434">**Özellikleri**: tüm telemetri verileri ile gönderilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="b8756-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="b8756-435">Tek tek parça * çağrılarında geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="b8756-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="b8756-436">**Oturum**: kullanıcı oturumu.</span><span class="sxs-lookup"><span data-stu-id="b8756-436">**Session**: The user's session.</span></span> <span data-ttu-id="b8756-437">Kimliği, kullanıcı bir süredir etkin ayarlanmadı bağlandığınızda değiştirilir oluşturulan bir değere ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b8756-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="b8756-438">**Kullanıcı**: kullanıcı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b8756-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="b8756-439">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="b8756-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="b8756-440">Veri hızı sınırı basarsa önlemek için [örnekleme](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="b8756-441">Verileri Tutuluyor ne kadar süreyle belirlemek için bkz: [veri saklama ve gizlilik](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="b8756-442">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="b8756-442">Reference docs</span></span>
* [<span data-ttu-id="b8756-443">ASP.NET başvurusu</span><span class="sxs-lookup"><span data-stu-id="b8756-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="b8756-444">Java başvurusu</span><span class="sxs-lookup"><span data-stu-id="b8756-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="b8756-445">JavaScript başvurusu</span><span class="sxs-lookup"><span data-stu-id="b8756-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="b8756-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="b8756-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="b8756-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="b8756-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="b8756-448">SDK kod</span><span class="sxs-lookup"><span data-stu-id="b8756-448">SDK code</span></span>
* [<span data-ttu-id="b8756-449">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="b8756-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="b8756-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="b8756-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="b8756-451">Windows Server paketleri</span><span class="sxs-lookup"><span data-stu-id="b8756-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="b8756-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="b8756-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="b8756-453">JavaScript SDK'sı</span><span class="sxs-lookup"><span data-stu-id="b8756-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="b8756-454">Tüm platformlar</span><span class="sxs-lookup"><span data-stu-id="b8756-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="b8756-455">Sorular</span><span class="sxs-lookup"><span data-stu-id="b8756-455">Questions</span></span>
* <span data-ttu-id="b8756-456">*Hangi özel durumları Track_() çağrıları throw?*</span><span class="sxs-lookup"><span data-stu-id="b8756-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="b8756-457">yok.</span><span class="sxs-lookup"><span data-stu-id="b8756-457">None.</span></span> <span data-ttu-id="b8756-458">Try-catch yan tümcelerinde kaydırma gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="b8756-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="b8756-459">SDK sorunla karşılaşırsa, hata ayıklama konsol çıktısı iletileri kaydedecek ve--tanılama Arama'da iletileri üzerinden--alırsanız.</span><span class="sxs-lookup"><span data-stu-id="b8756-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="b8756-460">*Portaldan veri almak için bir REST API var mı?*</span><span class="sxs-lookup"><span data-stu-id="b8756-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="b8756-461">Evet, [veri erişim API](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="b8756-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="b8756-462">Veri ayıklamak için diğer yolları dahil [Analytics'ten Power BI verme](app-insights-export-power-bi.md) ve [sürekli verme](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="b8756-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="b8756-463"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b8756-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="b8756-464">Arama olayları ve günlükleri</span><span class="sxs-lookup"><span data-stu-id="b8756-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="b8756-465">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="b8756-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


