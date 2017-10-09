---
title: "Özel olayları ve ölçümleri için Insights API'si aaaApplication | Microsoft Docs"
description: "Sorunlarını tanılamak ve birkaç satırlık bir kod, cihaz veya masaüstü uygulaması, Web sayfası veya service tootrack kullanımınızı ekleyin."
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
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="3e207-103">Özel olayları ve ölçümleri için Application Insights API'si</span><span class="sxs-lookup"><span data-stu-id="3e207-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="3e207-104">Birkaç satır kod ile kullanıcıların gerçekleştirdiği çıkışı, uygulama toofind eklemek veya toohelp sorunları tanılamak.</span><span class="sxs-lookup"><span data-stu-id="3e207-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="3e207-105">Aygıt ve Masaüstü uygulamaları, web istemcileri ve web sunucuları telemetri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="3e207-106">Kullanım hello [Azure Application Insights](app-insights-overview.md) çekirdek telemetri API'si toosend özel olayları ve ölçümleri ve standart telemetri kendi sürümleri.</span><span class="sxs-lookup"><span data-stu-id="3e207-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="3e207-107">Bu API aynı API Application Insights veri toplayıcıları kullanın Bu hello standart hello.</span><span class="sxs-lookup"><span data-stu-id="3e207-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="3e207-108">API özeti</span><span class="sxs-lookup"><span data-stu-id="3e207-108">API summary</span></span>
<span data-ttu-id="3e207-109">Merhaba API birkaç küçük Çeşitlemeler dışında tüm platformlar arasında Tekdüzen değil.</span><span class="sxs-lookup"><span data-stu-id="3e207-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="3e207-110">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3e207-110">Method</span></span> | <span data-ttu-id="3e207-111">İçin kullanılır</span><span class="sxs-lookup"><span data-stu-id="3e207-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="3e207-112">Sayfalar, ekranlar, dikey veya formlar.</span><span class="sxs-lookup"><span data-stu-id="3e207-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="3e207-113">Kullanıcı eylemleri ve diğer olaylar.</span><span class="sxs-lookup"><span data-stu-id="3e207-113">User actions and other events.</span></span> <span data-ttu-id="3e207-114">Tootrack kullanıcı davranışı veya toomonitor performans kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3e207-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="3e207-115">Performans ölçümleri sıra uzunlukları gibi toospecific olayları ilgili değildir.</span><span class="sxs-lookup"><span data-stu-id="3e207-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="3e207-116">Tanılama için günlük özel durumları.</span><span class="sxs-lookup"><span data-stu-id="3e207-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="3e207-117">İzleme burada bunlar ilişkisi tooother olaylar oluşur ve Yığın izlemeleri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="3e207-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="3e207-118">Merhaba sıklığı ve sunucu istek süresi performans analizi için günlüğe kaydetme.</span><span class="sxs-lookup"><span data-stu-id="3e207-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="3e207-119">Tanılama günlük iletileri.</span><span class="sxs-lookup"><span data-stu-id="3e207-119">Diagnostic log messages.</span></span> <span data-ttu-id="3e207-120">Üçüncü taraf günlükleri de yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="3e207-121">Günlüğe kaydetme hello süresi ve uygulamanızı bağlıdır çağrıları tooexternal bileşenleri sıklığı.</span><span class="sxs-lookup"><span data-stu-id="3e207-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="3e207-122">Yapabilecekleriniz [özellikleri ve ölçümleri attach](#properties) toomost bu telemetri çağrılarının.</span><span class="sxs-lookup"><span data-stu-id="3e207-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="3e207-123"><a name="prep"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3e207-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="3e207-124">Application Insights SDK'sı üzerinde bir başvuru henüz yoksa:</span><span class="sxs-lookup"><span data-stu-id="3e207-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="3e207-125">Merhaba Application Insights SDK'sı tooyour proje ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3e207-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="3e207-126">ASP.NET projesi</span><span class="sxs-lookup"><span data-stu-id="3e207-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="3e207-127">Java projesi</span><span class="sxs-lookup"><span data-stu-id="3e207-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="3e207-128">Her Web sayfasındaki JavaScript</span><span class="sxs-lookup"><span data-stu-id="3e207-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="3e207-129">Cihaz veya web sunucusu kodunuzda şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3e207-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="3e207-130">*C# ' TA:*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="3e207-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="3e207-131">*Visual Basic:*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="3e207-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="3e207-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="3e207-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="3e207-133">Bir TelemetryClient örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="3e207-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="3e207-134">Olgusu `TelemetryClient` (Web sayfalarındaki JavaScript'te hariç):</span><span class="sxs-lookup"><span data-stu-id="3e207-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="3e207-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="3e207-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="3e207-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="3e207-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="3e207-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="3e207-138">TelemetryClient iş parçacığı güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="3e207-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="3e207-139">Uygulamanızı her modül için TelemetryClient örneğini kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="3e207-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="3e207-140">Örneğin, web hizmeti tooreport gelen HTTP istekleri ve başka bir ara yazılım sınıf tooreport iş mantığı olayları bir TelemetryClient örneği olabilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="3e207-141">Özellikleri gibi ayarlayabilirsiniz `TelemetryClient.Context.User.Id` tootrack kullanıcılar ve oturumlar veya `TelemetryClient.Context.Device.Id` tooidentify hello makine.</span><span class="sxs-lookup"><span data-stu-id="3e207-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="3e207-142">Bu bilgiler örneği gönderir hello ekli tooall olayları olur.</span><span class="sxs-lookup"><span data-stu-id="3e207-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="3e207-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="3e207-143">TrackEvent</span></span>
<span data-ttu-id="3e207-144">Application ınsights'ta bir *özel olay* içinde görüntüleyebilirsiniz bir veri noktası [ölçüm Gezgini](app-insights-metrics-explorer.md) toplanan sayılara olarak ve buna [tanılama arama](app-insights-diagnostic-search.md) olarak tek tek yineleme.</span><span class="sxs-lookup"><span data-stu-id="3e207-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="3e207-145">(Bunu ilgili tooMVC veya diğer framework "olayları." değil)</span><span class="sxs-lookup"><span data-stu-id="3e207-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="3e207-146">INSERT `TrackEvent` çeşitli olayları, kod toocount çağırır.</span><span class="sxs-lookup"><span data-stu-id="3e207-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="3e207-147">Ne sıklıkla kullanıcıların belirli bir özellik, ne sıklıkta bunlar belirli hedeflere ulaşmak veya hatalar belirli tür belki ne sıklıkta yaptıkları seçin.</span><span class="sxs-lookup"><span data-stu-id="3e207-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="3e207-148">Örneğin, bir oyun uygulamada bir kullanıcı hello oyun WINS bir olay gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="3e207-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="3e207-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="3e207-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="3e207-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="3e207-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="3e207-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="3e207-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="3e207-153">Merhaba Microsoft Azure Portalı'nda, olayları görüntülemek</span><span class="sxs-lookup"><span data-stu-id="3e207-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="3e207-154">toosee, etkinliklerin sayısını açık bir [ölçüm Gezgini](app-insights-metrics-explorer.md) dikey penceresinde, yeni bir grafik ekleyin ve seçin **olayları**.</span><span class="sxs-lookup"><span data-stu-id="3e207-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Özel olaylar sayısını bakın](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="3e207-156">toocompare hello sayıları farklı olayların ayarlamak hello grafik türü çok**kılavuz**ve olay adı tarafından Grup:</span><span class="sxs-lookup"><span data-stu-id="3e207-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Merhaba grafik türü ve gruplandırma ayarlayın](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="3e207-158">Başlangıç Kılavuzu, bir olay adı toosee oluşumlarını olay ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3e207-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="3e207-159">toosee daha fazla ayrıntı - hello listesinde olayı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3e207-159">toosee more detail - click any occurrence in hello list.</span></span>

![Aracılığıyla Hello olaylarını incelemek](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="3e207-161">toofocus belirli olayları arama veya ölçüm Gezgini, ilgilendiğiniz kümesi hello dikey'nın filtre toohello olay adları:</span><span class="sxs-lookup"><span data-stu-id="3e207-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Filtreler açın, olay adı'nı genişletin ve bir veya daha fazla değerleri seçin](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="3e207-163">Analytics'te özel olaylar</span><span class="sxs-lookup"><span data-stu-id="3e207-163">Custom events in Analytics</span></span>

<span data-ttu-id="3e207-164">Merhaba telemetri hello kullanılabilir `customEvents` tablosundaki [uygulama Öngörüler Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="3e207-165">Her satır bir çağrı çok temsil eden`trackEvent(..)` uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="3e207-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="3e207-166">Varsa [örnekleme](app-insights-sampling.md) içinde hello ItemCount özelliği 1'den büyük bir değer gösterir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3e207-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="3e207-167">Örnek ItemCount == 10 çağrıları tootrackEvent() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3e207-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="3e207-168">özel olaylar doğru sayısını tooget, kullanmanız gereken bu nedenle kullanım kodu gibi `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="3e207-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="3e207-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="3e207-169">TrackMetric</span></span>

<span data-ttu-id="3e207-170">Application Insights ekli tooparticular olayları olmayan ölçümleri grafik.</span><span class="sxs-lookup"><span data-stu-id="3e207-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="3e207-171">Örneğin, bir kuyruk uzunluğu düzenli aralıklarla izlemek.</span><span class="sxs-lookup"><span data-stu-id="3e207-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="3e207-172">Ölçümler ile Merhaba Çeşitlemeler ve eğilimleri'den daha az ilgi hello tek tek ölçüler olan ve böylece istatistiksel grafikleri kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="3e207-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="3e207-173">Toosend ölçümleri tooApplication Öngörüler sipariş, hello kullanabilirsiniz `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="3e207-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="3e207-174">Ölçüm iki yolu toosend vardır:</span><span class="sxs-lookup"><span data-stu-id="3e207-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="3e207-175">Tek bir değer.</span><span class="sxs-lookup"><span data-stu-id="3e207-175">Single value.</span></span> <span data-ttu-id="3e207-176">Uygulamanızda bir ölçüm gerçekleştirdiğiniz her zaman tooApplication Öngörüler hello karşılık gelen değer gönderin.</span><span class="sxs-lookup"><span data-stu-id="3e207-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="3e207-177">Örneğin, bir kapsayıcı öğe hello sayısını açıklayan bir ölçüm olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="3e207-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="3e207-178">Belirli bir zaman diliminde ilk üç öğe hello kapsayıcıya yerleştirdiğiniz ve ardından iki öğeyi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3e207-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="3e207-179">Buna göre çağırırdı `TrackMetric` iki kez: hello değeri'ilk geçirme `3` ve değer hello `-2`.</span><span class="sxs-lookup"><span data-stu-id="3e207-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="3e207-180">Application Insights, sizin adınıza her iki değerin de depolar.</span><span class="sxs-lookup"><span data-stu-id="3e207-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="3e207-181">Toplama.</span><span class="sxs-lookup"><span data-stu-id="3e207-181">Aggregation.</span></span> <span data-ttu-id="3e207-182">Ölçümleri ile çalışırken, her tek nadiren ilgi ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="3e207-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="3e207-183">Bunun yerine belirli bir süre içinde ne Özet önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3e207-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="3e207-184">Bu tür bir özeti adlı _toplama_.</span><span class="sxs-lookup"><span data-stu-id="3e207-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="3e207-185">Yukarıdaki örnek Hello hello toplama ölçüm bu döneme ait toplamıdır `1` ve hello ölçüm değerleri hello sayısı `2`.</span><span class="sxs-lookup"><span data-stu-id="3e207-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="3e207-186">Merhaba toplama yaklaşım kullanırken, yalnızca çağırma `TrackMetric` zaman dönemi ve gönderme hello toplama değerlerini zorunda kalırsınız.</span><span class="sxs-lookup"><span data-stu-id="3e207-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="3e207-187">Merhaba maliyetini önemli ölçüde azaltabilir ve daha az veri göndererek yükü performans hala ilgili tüm bilgileri toplanırken tooApplication Öngörüler işaret olduğundan önerilen yaklaşımı hello budur.</span><span class="sxs-lookup"><span data-stu-id="3e207-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="3e207-188">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="3e207-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="3e207-189">Tek değer</span><span class="sxs-lookup"><span data-stu-id="3e207-189">Single values</span></span>

<span data-ttu-id="3e207-190">toosend tek bir ölçü değeri:</span><span class="sxs-lookup"><span data-stu-id="3e207-190">toosend a single metric value:</span></span>

<span data-ttu-id="3e207-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="3e207-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="3e207-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="3e207-193">Ölçümleri toplama</span><span class="sxs-lookup"><span data-stu-id="3e207-193">Aggregating metrics</span></span>

<span data-ttu-id="3e207-194">Uygulama, tooreduce bant genişliği, maliyet ve tooimprove performans kaynağı bunları göndermeden önce tooaggregate ölçümleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="3e207-195">Kod bir araya getirildiği bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3e207-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="3e207-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-196">*C#*</span></span>

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
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
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
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="3e207-197">Ölçümleri Explorer'da özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="3e207-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="3e207-198">toosee hello sonuçları ölçümleri Gezgini'ni açın ve yeni bir grafik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3e207-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="3e207-199">Merhaba grafik tooshow, ölçüm düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="3e207-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="3e207-200">Özel ölçüm birkaç dakika tooappear hello kullanılabilir ölçümler listesinde alabilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Yeni bir grafik ekleyin veya bir grafik seçin ve özel altında ölçüm seçin](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="3e207-202">Analytics'te özel ölçümleri</span><span class="sxs-lookup"><span data-stu-id="3e207-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="3e207-203">Merhaba telemetri hello kullanılabilir `customMetrics` tablosundaki [uygulama Öngörüler Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="3e207-204">Her satır bir çağrı çok temsil eden`trackMetric(..)` uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="3e207-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="3e207-205">`valueSum`-Bu hello hello ölçümleri toplamıdır.</span><span class="sxs-lookup"><span data-stu-id="3e207-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="3e207-206">tooget hello ortalama değer, sıfıra bölünme `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="3e207-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="3e207-207">`valueCount`-hello bu toplanan ölçümleri sayısı `trackMetric(..)` çağırın.</span><span class="sxs-lookup"><span data-stu-id="3e207-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="3e207-208">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="3e207-208">Page views</span></span>
<span data-ttu-id="3e207-209">Her ekranı veya sayfa yüklendiğinde, bir aygıt veya Web sayfası uygulamasında varsayılan olarak sayfa görünümü telemetrisi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="3e207-210">Ancak bu tootrack sayfa görünümleri ek veya farklı zamanlarda değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="3e207-211">Örneğin, sekmeler veya dikey pencereler görüntüler bir uygulamada Hello kullanıcı yeni bir dikey pencere açıldığında tootrack bir sayfa isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Genel Bakış dikey penceresinde kullanım Mercek](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="3e207-213">Sayfa görünümleri birlikte özellikleri şekilde hello gibi sayfa görünümü telemetrisi olduğunda Canlı gelen kullanıcı ve oturum grafik kullanıcı ve oturum verilerini gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="3e207-214">Özel sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="3e207-214">Custom page views</span></span>
<span data-ttu-id="3e207-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="3e207-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="3e207-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="3e207-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="3e207-218">Farklı HTML sayfaları içinde birden çok sekme varsa, hello URL çok belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3e207-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="3e207-219">Zamanlama sayfası görünümleri</span><span class="sxs-lookup"><span data-stu-id="3e207-219">Timing page views</span></span>
<span data-ttu-id="3e207-220">Varsayılan olarak, hello kez bildirildi **sayfa görünümü yükleme süresi** hello tarayıcının sayfası yük olayı çağrılıncaya kadar hello tarayıcı hello isteği gönderdiğinde gelen ölçülür.</span><span class="sxs-lookup"><span data-stu-id="3e207-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="3e207-221">Bunun yerine, şunlardan birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3e207-221">Instead, you can either:</span></span>

* <span data-ttu-id="3e207-222">Hello bir açık kalma süresini ayarlamak [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) çağırın: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="3e207-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="3e207-223">Merhaba sayfa görünümü zamanlama çağrıları kullanmak `startTrackPage` ve `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="3e207-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="3e207-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="3e207-225">...</span><span class="sxs-lookup"><span data-stu-id="3e207-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="3e207-226">Merhaba ilk parametre hello başlangıç ilişkilendirir gibi kullandığınız adı hello ve çağrıları durdurun.</span><span class="sxs-lookup"><span data-stu-id="3e207-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="3e207-227">Bu varsayılan toohello geçerli sayfa adı içerir.</span><span class="sxs-lookup"><span data-stu-id="3e207-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="3e207-228">Ölçümleri Gezgini'nde görüntülenen süreleri hello hello aralığını türetilir hello elde edilen sayfa yükleme başlatma ve durdurma çağrıları.</span><span class="sxs-lookup"><span data-stu-id="3e207-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="3e207-229">Bu tooyou gerçekten zaman hangi aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="3e207-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="3e207-230">Sayfa telemetri analizi</span><span class="sxs-lookup"><span data-stu-id="3e207-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="3e207-231">İçinde [Analytics](app-insights-analytics.md) iki tablo tarayıcı işlemleri verileri göster:</span><span class="sxs-lookup"><span data-stu-id="3e207-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="3e207-232">Merhaba `pageViews` tablo hello URL ve sayfa başlığını hakkındaki verileri içerir</span><span class="sxs-lookup"><span data-stu-id="3e207-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="3e207-233">Merhaba `browserTimings` tablo hello geçen süre tooprocess gelen veri hello gibi istemci performansı hakkında veri içerir</span><span class="sxs-lookup"><span data-stu-id="3e207-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="3e207-234">toofind hello tarayıcı tooprocess farklı sayfaları süreyi:</span><span class="sxs-lookup"><span data-stu-id="3e207-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="3e207-235">farklı tarayıcıların toodiscover hello popularities:</span><span class="sxs-lookup"><span data-stu-id="3e207-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="3e207-236">tooassociate sayfa görünümleri tooAJAX çağrıları, bağımlılıkları olan Katıl:</span><span class="sxs-lookup"><span data-stu-id="3e207-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="3e207-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="3e207-237">TrackRequest</span></span>
<span data-ttu-id="3e207-238">Merhaba sunucusu SDK TrackRequest toolog HTTP isteklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3e207-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="3e207-239">Bağlamda toosimulate istekleri istiyorsanız aynı zamanda kendiniz hello web hizmeti modülü çalışıyor burada yok çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="3e207-240">Ancak, hello yolu toosend isteği telemetri burada hello isteği görevi gören önerilir bir <a href="#operation-context">işlemi bağlam</a>.</span><span class="sxs-lookup"><span data-stu-id="3e207-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="3e207-241">İşlem bağlamı</span><span class="sxs-lookup"><span data-stu-id="3e207-241">Operation context</span></span>
<span data-ttu-id="3e207-242">Toothem ortak bir işlem kimliği ekleyerek telemetri öğelerini birlikte ilişkilendirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="3e207-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="3e207-243">Merhaba standart isteği izleme modülü, özel durumlar ve bir HTTP istek gerçekleştirilirken gönderilen diğer olayları için bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="3e207-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="3e207-244">İçinde [arama](app-insights-diagnostic-search.md) ve [Analytics](app-insights-analytics.md), hello istekle ilişkili olaylar hello kimliği tooeasily bulma kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="3e207-245">Merhaba en kolay yolu tooset hello kimliği, bu yöntemi kullanarak tooset bir işlem bağlamı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3e207-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="3e207-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="3e207-247">Bir işlemin bağlamını ayarlanması birlikte `StartOperation` belirttiğiniz hello türünde bir telemetri öğesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3e207-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="3e207-248">Merhaba işlemi çıkardığınızda veya açıkça çağırırsanız hello telemetri öğesi gönderir `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="3e207-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="3e207-249">Kullanırsanız `RequestTelemetry` hello telemetri türü olarak zaman aşımına toohello aralığını başlatma ve durdurma süresi ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3e207-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="3e207-250">İşlem bağlamı iç içe olamaz.</span><span class="sxs-lookup"><span data-stu-id="3e207-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="3e207-251">Bir işlem bağlamı zaten var. sonra Kimliğini ile oluşturulan hello öğesi de dahil olmak üzere tüm bulunan hello öğelerle ilişkili `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="3e207-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="3e207-252">Aramada, hello işlemi kullanılan toocreate hello bağlamdır **ilgili öğeler** listesi:</span><span class="sxs-lookup"><span data-stu-id="3e207-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![İlgili öğeler](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="3e207-254">[Uygulama-Öngörüler-özel-işlemleri-tracking.md] izleme özel işlemler hakkında daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="3e207-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="3e207-255">Analytics istekleri</span><span class="sxs-lookup"><span data-stu-id="3e207-255">Requests in Analytics</span></span> 

<span data-ttu-id="3e207-256">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), istekleri Göster yukarı hello `requests` tablo.</span><span class="sxs-lookup"><span data-stu-id="3e207-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="3e207-257">Varsa [örnekleme](app-insights-sampling.md) olduğundan, işlem hello ItemCount özelliği bir değer 1'den büyük gösterir.</span><span class="sxs-lookup"><span data-stu-id="3e207-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="3e207-258">Örnek ItemCount == 10 çağrıları tootrackRequest() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3e207-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="3e207-259">tooget istekleri ve ortalama süresi doğru sayısı isteği adlarıyla bölümlenmiş, kod gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="3e207-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="3e207-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="3e207-260">TrackException</span></span>
<span data-ttu-id="3e207-261">Özel durumlar tooApplication Öngörüler gönder:</span><span class="sxs-lookup"><span data-stu-id="3e207-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="3e207-262">çok[saymanız](app-insights-metrics-explorer.md), hello sıklığı bir sorunun belirtisi olarak.</span><span class="sxs-lookup"><span data-stu-id="3e207-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="3e207-263">çok[ayrı ayrı oluşumları inceleyin](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="3e207-264">Merhaba raporları hello Yığın izlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3e207-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="3e207-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="3e207-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="3e207-267">her zaman toocall TrackException açıkça aktarıp hello SDK'ları birçok özel durumlarını otomatik olarak yakalama.</span><span class="sxs-lookup"><span data-stu-id="3e207-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="3e207-268">ASP.NET: [toocatch özel durum kodu yazma](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="3e207-269">J2EE: [özel durumları yakalanan otomatik olarak](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="3e207-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="3e207-270">JavaScript: Özel durumları otomatik olarak yakalanır.</span><span class="sxs-lookup"><span data-stu-id="3e207-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="3e207-271">Toodisable otomatik olarak toplanmasını istiyorsanız, Web sayfalarındaki eklediğiniz bir satır toohello kod parçacığını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3e207-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="3e207-272">Analytics özel durumları</span><span class="sxs-lookup"><span data-stu-id="3e207-272">Exceptions in Analytics</span></span>

<span data-ttu-id="3e207-273">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), özel durumlar hello görünmesini `exceptions` tablo.</span><span class="sxs-lookup"><span data-stu-id="3e207-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="3e207-274">Varsa [örnekleme](app-insights-sampling.md) işleminde, hello olduğu `itemCount` özelliği değeri 1'den büyük gösterir.</span><span class="sxs-lookup"><span data-stu-id="3e207-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="3e207-275">Örnek ItemCount == 10 çağrıları tootrackException() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3e207-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="3e207-276">özel durum türüne göre özel durumlarının doğru bir sayısı tooget bölümlenmiş, kod gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="3e207-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="3e207-277">Merhaba yığın bilgileri ayrı değişkenlere zaten ayıklanan ancak birbirinden hello çekebilir önemli çoğu `details` yapısı tooget daha fazla.</span><span class="sxs-lookup"><span data-stu-id="3e207-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="3e207-278">Bu yapı dinamik olduğundan, beklediğiniz hello sonuç toohello türü atamalısınız.</span><span class="sxs-lookup"><span data-stu-id="3e207-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="3e207-279">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3e207-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="3e207-280">ilgili isteklerinde tooassociate istisnalar bir birleşim kullanın:</span><span class="sxs-lookup"><span data-stu-id="3e207-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="3e207-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="3e207-281">TrackTrace</span></span>
<span data-ttu-id="3e207-282">Kullanım TrackTrace toohelp Öngörüler "içerik haritası Kılavuzu" tooApplication göndererek sorunları tanılayın.</span><span class="sxs-lookup"><span data-stu-id="3e207-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="3e207-283">Tanılama veri öbekleri göndermek ve bunları inceleyin [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="3e207-284">[Oturum bağdaştırıcıları](app-insights-asp-net-trace-logs.md) bu API toosend üçüncü taraf günlükleri toohello portalı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e207-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="3e207-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="3e207-286">İleti içeriği arama yapabilirsiniz ancak (özellik değerlerini), üzerinde filtre uygulayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="3e207-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="3e207-287">Merhaba boyut sınırını `message` özellikleri hello sınırdan daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="3e207-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="3e207-288">TrackTrace avantajı hello iletisinde oldukça uzun veri koyabilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="3e207-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="3e207-289">Örneğin, POST verilerini şifreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="3e207-290">Ayrıca, bir önem düzeyi tooyour ileti ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="3e207-291">Ve diğer telemetri gibi filtre özellik değerleri toohelp veya izlemeleri farklı kümeleri için arama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="3e207-292">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3e207-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="3e207-293">İçinde [arama](app-insights-diagnostic-search.md), daha sonra kolayca tooa belirli veritabanı ile ilgili tüm hello iletilerini belirli önem düzeyine sahip bir filtre.</span><span class="sxs-lookup"><span data-stu-id="3e207-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="3e207-294">İçindeki analizi</span><span class="sxs-lookup"><span data-stu-id="3e207-294">Traces in Analytics</span></span>

<span data-ttu-id="3e207-295">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), çağıran tooTrackTrace Göster hello `traces` tablo.</span><span class="sxs-lookup"><span data-stu-id="3e207-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="3e207-296">Varsa [örnekleme](app-insights-sampling.md) içinde hello ItemCount özelliği 1'den büyük bir değer gösterir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3e207-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="3e207-297">Örnek ItemCount == 10 çok çağırır 10 anlamına gelir`trackTrace()`, hello örnekleme işlemi yalnızca aktarılan bunlardan biri.</span><span class="sxs-lookup"><span data-stu-id="3e207-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="3e207-298">tooget izleme çağrıları doğru sayısını, kullanmanız gereken bu nedenle kod gibi `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="3e207-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="3e207-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="3e207-299">TrackDependency</span></span>
<span data-ttu-id="3e207-300">Kullanım hello TrackDependency tootrack hello yanıt sürelerini ve başarı oranları çağrıları tooan dış kod parçası, çağırın.</span><span class="sxs-lookup"><span data-stu-id="3e207-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="3e207-301">Merhaba bağımlılık grafiklerinde hello portalında Hello sonuçları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3e207-301">hello results appear in hello dependency charts in hello portal.</span></span>

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

<span data-ttu-id="3e207-302">SDK'ları dahil hello sunucu unutmayın bir [bağımlılık Modülü](app-insights-asp-net-dependencies.md) bulur ve bazı bağımlılık çağrıları otomatik olarak--Örneğin, toodatabases ve REST API'leri izler.</span><span class="sxs-lookup"><span data-stu-id="3e207-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="3e207-303">İş tooinstall sunucu toomake hello modül bir aracı var.</span><span class="sxs-lookup"><span data-stu-id="3e207-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="3e207-304">Bu çağrı değil otomatik izleme hello tootrack çağrıları catch istiyorsanız veya tooinstall hello Aracısı istemiyorsanız kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e207-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="3e207-305">Merhaba standart bağımlılık izleme modül devre dışı tooturn Düzenle [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) ve hello başvuru çok silme`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="3e207-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="3e207-306">Analytics bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="3e207-306">Dependencies in Analytics</span></span>

<span data-ttu-id="3e207-307">İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), trackDependency çağrıları hello görünmesini `dependencies` tablo.</span><span class="sxs-lookup"><span data-stu-id="3e207-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="3e207-308">Varsa [örnekleme](app-insights-sampling.md) içinde hello ItemCount özelliği 1'den büyük bir değer gösterir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3e207-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="3e207-309">Örnek ItemCount == 10 çağrıları tootrackDependency() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3e207-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="3e207-310">tooget bağımlılıkları doğru sayısını hedef bileşen tarafından bölümlenmiş, kod gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="3e207-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="3e207-311">tooassociate bağımlılıkları ile ilgili isteklerinde bir birleşim kullanın:</span><span class="sxs-lookup"><span data-stu-id="3e207-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="3e207-312">Düzenleniyor veri</span><span class="sxs-lookup"><span data-stu-id="3e207-312">Flushing data</span></span>
<span data-ttu-id="3e207-313">Normalde, hello SDK bazen toominimize hello hello kullanıcı etkisini seçilen verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="3e207-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="3e207-314">Uygulamada kapandıktan hello SDK kullanıyorsanız, ancak bazı durumlarda, tooflush hello arabellek--Örneğin, isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="3e207-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="3e207-316">Merhaba işlevi hello için zaman uyumsuz olduğuna dikkat edin [server telemetri kanalı](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="3e207-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="3e207-317">Kimliği doğrulanmış kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="3e207-317">Authenticated users</span></span>
<span data-ttu-id="3e207-318">Bir web uygulaması, kullanıcıların (varsayılan) tanımlama bilgileri tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="3e207-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="3e207-319">Bir kullanıcı birden çok kez uygulamanız farklı makine ya da tarayıcı erişimi engelliyorsa veya tanımlama bilgilerini sildiğinizde sayılması.</span><span class="sxs-lookup"><span data-stu-id="3e207-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="3e207-320">Kullanıcıların tooyour uygulamada oturum açarsanız hello tarayıcı kodda hello kimliği doğrulanmış kullanıcı kimliği ayarlayarak daha doğru bir sayı elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3e207-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="3e207-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="3e207-322">Bir ASP.NET web örneğin MVC uygulaması:</span><span class="sxs-lookup"><span data-stu-id="3e207-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="3e207-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="3e207-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="3e207-324">Gerekli toouse hello kullanıcının gerçek oturum açma adı değil.</span><span class="sxs-lookup"><span data-stu-id="3e207-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="3e207-325">Yalnızca toobe benzersiz toothat kullanıcı Kimliğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="3e207-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="3e207-326">Boşluk veya hello karakterlerden herhangi birini içermemelidir `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="3e207-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="3e207-327">Merhaba kullanıcı kimliği ayrıca bir oturum tanımlama bilgisinde ayarlamak ve toohello sunucu gönderilen.</span><span class="sxs-lookup"><span data-stu-id="3e207-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="3e207-328">Merhaba server SDK'sı yüklü ise hello kimliği hello bağlam özellikleri hem istemci hem de sunucu telemetrinin bir parçası olarak gönderilen kullanıcı kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="3e207-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="3e207-329">Daha sonra filtre ve onu Search'te.</span><span class="sxs-lookup"><span data-stu-id="3e207-329">You can then filter and search on it.</span></span>

<span data-ttu-id="3e207-330">Uygulamanız kullanıcıların hesaplara gruplar, hello hesabı için bir tanımlayıcı da geçirebilirsiniz (Merhaba ile aynı, kısıtlamaları'karakter).</span><span class="sxs-lookup"><span data-stu-id="3e207-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="3e207-331">İçinde [ölçüm Gezgini](app-insights-metrics-explorer.md), sayar bir grafik oluşturabilirsiniz **kimliği doğrulanmış kullanıcılar,**, ve **kullanıcı hesaplarını**.</span><span class="sxs-lookup"><span data-stu-id="3e207-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="3e207-332">Ayrıca [arama](app-insights-diagnostic-search.md) belirli kullanıcı adları ve hesapları ile istemci veri noktaları için.</span><span class="sxs-lookup"><span data-stu-id="3e207-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="3e207-333"><a name="properties"></a>Filtreleme, aramayı ve özelliklerini kullanarak verilerinizi kesimlere</span><span class="sxs-lookup"><span data-stu-id="3e207-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="3e207-334">Özellikleri ve ölçülerini tooyour olayları (ve ayrıca toometrics, sayfa görünümleri, özel durumlar ve diğer telemetri verileri) ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="3e207-335">*Özellikler* dize değerleri toofilter hello kullanım raporlarında telemetrinizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="3e207-336">Örneğin, uygulamanızın birkaç oyunlar sağlıyorsa, hangi oyunlar daha popüler görebilmeniz için hello oyun tooeach olay hello adı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="3e207-337">8192 hello bir dize uzunluk sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="3e207-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="3e207-338">(Toosend büyük veri parçalarını istiyorsanız hello ileti parametresinin kullanın [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="3e207-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="3e207-339">*Ölçümleri* grafik sunulan sayısal değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="3e207-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="3e207-340">Örneğin, oyun severler elde hello puanları aşamalı bir artış ise toosee isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="3e207-341">Merhaba grafikleri hello olayla gönderilir ve böylece elde edebilirsiniz özelliklerini ayırmak hello tarafından kesimli veya farklı oyun grafikleri Yığılmış.</span><span class="sxs-lookup"><span data-stu-id="3e207-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="3e207-342">Doğru görüntülenen ölçüm değerleri toobe için bunlar too0 büyük veya ona eşit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3e207-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="3e207-343">Bazı vardır [hello sayısı özellikleri, özellik değerlerini ve ölçümleri sınırları](#limits) kullanabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="3e207-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-344">*JavaScript*</span></span>

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


<span data-ttu-id="3e207-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="3e207-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="3e207-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="3e207-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="3e207-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="3e207-348">Toolog kişisel bilgileri değil özelliklerinde ilgilenebilmek.</span><span class="sxs-lookup"><span data-stu-id="3e207-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="3e207-349">*Ölçümleri kullandıysanız*, ölçümleri Gezgini'ni açın ve hello hello ölçümü seçin **özel** Grup:</span><span class="sxs-lookup"><span data-stu-id="3e207-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Ölçüm Gezgini, select hello Grafiği'ni açın ve hello ölçümü seçin](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="3e207-351">Ölçüm görünmüyorsa veya hello **özel** başlığı Kapat hello seçimi dikey hiç ve daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="3e207-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="3e207-352">Ölçümleri bazen bir saatte zaman toobe hello ardışık düzen üzerinden toplanır.</span><span class="sxs-lookup"><span data-stu-id="3e207-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="3e207-353">*Özellikleri ve ölçümleri kullandıysanız*, hello ölçüm hello özelliği tarafından segmentlere:</span><span class="sxs-lookup"><span data-stu-id="3e207-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Gruplandırma ayarlayın ve ardından hello özelliği tarafından grubu altında seçin](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="3e207-355">*Tanılama arama*, hello özellikleri ve bir olay oluşumlarını ölçümlerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Bir örnek seçin ve ardından "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="3e207-357">Kullanım hello **arama** alan toosee olay belirli bir özellik değeri olan bir oluşumu.</span><span class="sxs-lookup"><span data-stu-id="3e207-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Arama terimi yazın](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="3e207-359">[Arama ifadeleri hakkında daha fazla bilgi](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="3e207-360">Alternatif yol tooset özellikleri ve ölçümleri</span><span class="sxs-lookup"><span data-stu-id="3e207-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="3e207-361">Daha kullanışlı ise, ayrı bir nesne olayda hello parametrelerinin toplayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3e207-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="3e207-362">Merhaba yeniden yok aynı telemetri öğesi örneği (`event` Bu örnekte) toocall Track*() birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="3e207-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="3e207-363">Bu yanlış yapılandırma ile gönderilen telemetri toobe neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="3e207-364">Özel ölçümleri ve analizi özellikleri</span><span class="sxs-lookup"><span data-stu-id="3e207-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="3e207-365">İçinde [Analytics](app-insights-analytics.md), özel Ölçümler ve özelliklerini göster hello `customMeasurements` ve `customDimensions` her telemetri kayıt öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="3e207-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="3e207-366">Örneğin, "Oyun" tooyour isteği telemetri adlı bir özellik eklediyseniz, bu sorgu farklı değerler "oyunun" Merhaba oluşumlarını sayar ve özel ölçüm "puan" Merhaba hello ortalaması göster:</span><span class="sxs-lookup"><span data-stu-id="3e207-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="3e207-367">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="3e207-367">Notice that:</span></span>

* <span data-ttu-id="3e207-368">Bir değer hello customDimensions veya customMeasurements JSON ayıkladığınızda, dinamik türüne sahip ve bu nedenle, gereken cast onu `tostring` veya `todouble`.</span><span class="sxs-lookup"><span data-stu-id="3e207-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="3e207-369">Merhaba olasılığını tootake hesabı [örnekleme](app-insights-sampling.md), kullanmanız gereken `sum(itemCount)`değil `count()`.</span><span class="sxs-lookup"><span data-stu-id="3e207-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="3e207-370"><a name="timed"></a>Zamanlama olayları</span><span class="sxs-lookup"><span data-stu-id="3e207-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="3e207-371">Bazen toochart tooperform eyleme geçen süreyi istersiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="3e207-372">Örneğin, tooknow isteyebilirsiniz ne kadar kullanıcılar bir oyunda tooconsider seçimler alın.</span><span class="sxs-lookup"><span data-stu-id="3e207-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="3e207-373">Bunun için hello ölçüm parametresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="3e207-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="3e207-375"><a name="defaults"></a>Özel telemetri için varsayılan özellikler</span><span class="sxs-lookup"><span data-stu-id="3e207-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="3e207-376">Bazı yazdığınız hello özel olaylar için tooset varsayılan özellik değerleri istiyorsanız, bunları TelemetryClient örneğinde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="3e207-377">Bu istemciden gönderilen ekli tooevery telemetri öğesi oldukları.</span><span class="sxs-lookup"><span data-stu-id="3e207-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="3e207-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="3e207-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="3e207-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="3e207-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="3e207-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="3e207-381">Tek tek telemetri çağrıları kendi özelliği sözlüklerindeki hello varsayılan değerleri geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="3e207-382">*JavaScript için web istemcileri*, [JavaScript telemetri başlatıcıları kullanmak](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="3e207-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="3e207-383">*tooadd özellikleri tooall telemetri*, standart toplama modüllerden hello veri dahil olmak üzere [uygulamak `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="3e207-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="3e207-384">Örnekleme, filtreleme ve telemetri işleniyor</span><span class="sxs-lookup"><span data-stu-id="3e207-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="3e207-385">SDK hello gönderilmeden önce telemetrinizi kod tooprocess yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="3e207-386">Merhaba işleme HTTP isteği koleksiyonu ve bağımlılık koleksiyonu gibi hello standart telemetri modüllerden gönderilen veriler içerir.</span><span class="sxs-lookup"><span data-stu-id="3e207-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="3e207-387">[Özellikler ekleme](app-insights-api-filtering-sampling.md#add-properties) uygulayarak tootelemetry `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="3e207-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="3e207-388">Örneğin, diğer özelliklerinden sürüm numaraları veya hesaplanan değerler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="3e207-389">[Filtreleme](app-insights-api-filtering-sampling.md#filtering) değiştirebilir veya SDK hello uygulayarak gönderilmeden önce telemetri atmak `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="3e207-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="3e207-390">Ne gönderildiğinde veya atılan denetlemek, ancak ölçümlerinizi hello etkisi tooaccount sahip.</span><span class="sxs-lookup"><span data-stu-id="3e207-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="3e207-391">Öğeler atılsın nasıl bağlı olarak, ilgili öğeler arasındaki hello özelliği toonavigate kaybedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="3e207-392">[Örnekleme](app-insights-api-filtering-sampling.md) paketlenmiş çözüm tooreduce hello uygulama toohello portalınızdan gönderilen verilerin birimdir.</span><span class="sxs-lookup"><span data-stu-id="3e207-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="3e207-393">Bunu görüntülenen hello ölçümleri etkilemeden yapar.</span><span class="sxs-lookup"><span data-stu-id="3e207-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="3e207-394">Ve bunu özel durumlar, istekleri ve sayfa görünümleri gibi ilgili öğeleri arasında giderek özelliği toodiagnose sorunlarınızı etkilemeden yapar.</span><span class="sxs-lookup"><span data-stu-id="3e207-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="3e207-395">[Daha fazla bilgi edinin](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="3e207-396">Telemetri devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="3e207-396">Disabling telemetry</span></span>
<span data-ttu-id="3e207-397">çok*dinamik olarak durdurmak ve başlatmak* hello toplama ve telemetri iletimini:</span><span class="sxs-lookup"><span data-stu-id="3e207-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="3e207-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="3e207-399">çok*seçili standart toplayıcıları devre dışı*--Örneğin, performans sayaçları, HTTP isteklerini veya bağımlılıkları--silin veya açıklama hello ilgili satırlarında çıkışı [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md). Örneğin, kendi TrackRequest veri toosend istiyorsanız bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="3e207-400"><a name="debug"></a>Geliştirici modu</span><span class="sxs-lookup"><span data-stu-id="3e207-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="3e207-401">Hata ayıklama sırasında yararlı toohave sonuçları hemen görebilmeniz için telemetrinizi hello ardışık düzen üzerinden öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="3e207-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="3e207-402">Size yardımcı ayrıca get ek ileti hello telemetri herhangi bir sorun izleme.</span><span class="sxs-lookup"><span data-stu-id="3e207-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="3e207-403">Uygulamanızı azaltabileceğinden, bir üretim ortamına kapatın.</span><span class="sxs-lookup"><span data-stu-id="3e207-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="3e207-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="3e207-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="3e207-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="3e207-406"><a name="ikey"></a>Seçili özel telemetri için Hello izleme anahtarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="3e207-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="3e207-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="3e207-408"><a name="dynamic-ikey"></a>Dinamik izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="3e207-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="3e207-409">geliştirme, test ve üretim ortamlarında, telemetri karıştırma tooavoid yapabilecekleriniz [ayrı Application Insights kaynakları oluşturmak](app-insights-create-new-resource.md) ve hello ortamına bağlı olarak kendi anahtarlarını değiştirme.</span><span class="sxs-lookup"><span data-stu-id="3e207-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="3e207-410">Merhaba yapılandırma dosyasından Hello izleme anahtarını almak yerine onu kodunuzda ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="3e207-411">Başlangıç anahtarı başlatma yöntemini, bir ASP.NET hizmetinde global.aspx.cs gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="3e207-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="3e207-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="3e207-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="3e207-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="3e207-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="3e207-414">Web sayfalarındaki, tooset isteyebilirsiniz, hello web sunucusunun durumu, yerine tam anlamıyla hello komut dosyasına kodlama.</span><span class="sxs-lookup"><span data-stu-id="3e207-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="3e207-415">Bir ASP.NET uygulamasında oluşturulan Örneğin, bir Web sayfasında:</span><span class="sxs-lookup"><span data-stu-id="3e207-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="3e207-416">*Razor JavaScript'te*</span><span class="sxs-lookup"><span data-stu-id="3e207-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="3e207-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="3e207-417">TelemetryContext</span></span>
<span data-ttu-id="3e207-418">TelemetryClient tüm telemetri verilerinin yanı sıra gönderilen değerleri içeren bir içerik özelliği vardır.</span><span class="sxs-lookup"><span data-stu-id="3e207-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="3e207-419">Normalde hello standart telemetri modülleri tarafından ayarlanmış, ancak Ayrıca bunları kendiniz ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="3e207-420">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="3e207-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="3e207-421">Bu değerleri kendiniz ayarlarsanız, hello ilgili satırından kaldırmayı düşünün [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), böylece değerleri ve hello standart değerleri kafası yok.</span><span class="sxs-lookup"><span data-stu-id="3e207-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="3e207-422">**Bileşen**: Merhaba uygulama ve onun sürümü.</span><span class="sxs-lookup"><span data-stu-id="3e207-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="3e207-423">**Aygıt**: hello uygulama çalıştığı hello cihaz hakkındaki verileri.</span><span class="sxs-lookup"><span data-stu-id="3e207-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="3e207-424">(Web uygulamalarında hello sunucu veya hello telemetri gönderilen istemci aygıt budur.)</span><span class="sxs-lookup"><span data-stu-id="3e207-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="3e207-425">**InstrumentationKey**: hello hello telemetri göründüğü Azure Application Insights kaynağı.</span><span class="sxs-lookup"><span data-stu-id="3e207-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="3e207-426">Bu genellikle Applicationınsights.config kayıt.</span><span class="sxs-lookup"><span data-stu-id="3e207-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="3e207-427">**Konum**: Merhaba hello cihazın coğrafi konumu.</span><span class="sxs-lookup"><span data-stu-id="3e207-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="3e207-428">**İşlem**: web uygulamalarında geçerli HTTP isteği Merhaba.</span><span class="sxs-lookup"><span data-stu-id="3e207-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="3e207-429">Diğer uygulama türleri bu toogroup olayları birlikte ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="3e207-430">**Kimliği**: öğeleri ilişkili herhangi bir olay tanılama arama incelediğinizde, bulabilmesi için farklı olayları, karşılık gelen oluşturulan bir değer.</span><span class="sxs-lookup"><span data-stu-id="3e207-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="3e207-431">**Ad**: bir tanımlayıcı, genellikle hello URL'sini hello HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="3e207-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="3e207-432">**SyntheticSource**: değil null veya boş, hello isteğinin hello kaynak belirten bir dize bir robot veya web testi belirlenmiştir durumunda.</span><span class="sxs-lookup"><span data-stu-id="3e207-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="3e207-433">Varsayılan olarak, ölçüm Gezgini hesaplamalarda gelen dışlanır.</span><span class="sxs-lookup"><span data-stu-id="3e207-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="3e207-434">**Özellikleri**: tüm telemetri verileri ile gönderilen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="3e207-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="3e207-435">Tek tek parça * çağrılarında geçersiz kılınabilir.</span><span class="sxs-lookup"><span data-stu-id="3e207-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="3e207-436">**Oturum**: hello kullanıcının oturumu.</span><span class="sxs-lookup"><span data-stu-id="3e207-436">**Session**: hello user's session.</span></span> <span data-ttu-id="3e207-437">Merhaba kimliği hello kullanıcı bir süredir etkin ayarlanmadı bağlandığınızda değiştirilir oluşturulan tooa değer ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3e207-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="3e207-438">**Kullanıcı**: kullanıcı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3e207-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="3e207-439">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="3e207-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="3e207-440">Merhaba veri hızı sınırı, kullanım basarsa tooavoid [örnekleme](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="3e207-441">long veri tutulur toodetermine bkz [veri saklama ve gizlilik](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="3e207-442">Başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="3e207-442">Reference docs</span></span>
* [<span data-ttu-id="3e207-443">ASP.NET başvurusu</span><span class="sxs-lookup"><span data-stu-id="3e207-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="3e207-444">Java başvurusu</span><span class="sxs-lookup"><span data-stu-id="3e207-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="3e207-445">JavaScript başvurusu</span><span class="sxs-lookup"><span data-stu-id="3e207-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="3e207-446">Android SDK</span><span class="sxs-lookup"><span data-stu-id="3e207-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="3e207-447">iOS SDK</span><span class="sxs-lookup"><span data-stu-id="3e207-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="3e207-448">SDK kod</span><span class="sxs-lookup"><span data-stu-id="3e207-448">SDK code</span></span>
* [<span data-ttu-id="3e207-449">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="3e207-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="3e207-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="3e207-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="3e207-451">Windows Server paketleri</span><span class="sxs-lookup"><span data-stu-id="3e207-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="3e207-452">Java SDK</span><span class="sxs-lookup"><span data-stu-id="3e207-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="3e207-453">JavaScript SDK'sı</span><span class="sxs-lookup"><span data-stu-id="3e207-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="3e207-454">Tüm platformlar</span><span class="sxs-lookup"><span data-stu-id="3e207-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="3e207-455">Sorular</span><span class="sxs-lookup"><span data-stu-id="3e207-455">Questions</span></span>
* <span data-ttu-id="3e207-456">*Hangi özel durumları Track_() çağrıları throw?*</span><span class="sxs-lookup"><span data-stu-id="3e207-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="3e207-457">yok.</span><span class="sxs-lookup"><span data-stu-id="3e207-457">None.</span></span> <span data-ttu-id="3e207-458">Toowrap gerekmeyen try-catch yan tümcelerinde bunları.</span><span class="sxs-lookup"><span data-stu-id="3e207-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="3e207-459">Ve Hello SDK sorunla karşılaşırsa hello hata ayıklama konsol çıkışı iletileri kaydedecek--tanılama Arama'da hello varsa--aracılığıyla iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e207-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="3e207-460">*REST API tooget veri hello portalından var mı?*</span><span class="sxs-lookup"><span data-stu-id="3e207-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="3e207-461">Evet, hello [veri erişim API](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="3e207-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="3e207-462">Diğer yolları tooextract verileri içerecek [verme Analytics tooPower BI](app-insights-export-power-bi.md) ve [sürekli verme](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="3e207-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="3e207-463"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e207-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="3e207-464">Arama olayları ve günlükleri</span><span class="sxs-lookup"><span data-stu-id="3e207-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="3e207-465">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3e207-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


