---
title: "Azure Application Insights izleme bağımlılık | Microsoft Docs"
description: "Application Insights ile şirket içi veya Microsoft Azure web uygulamanızın kullanımını, kullanılabilirliğini ve performansını analiz edin."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 6e0b67ba98af27017901608dde4401600eb9957f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="d1148-103">Application Insights'ı ayarlayın: bağımlılık izleme</span><span class="sxs-lookup"><span data-stu-id="d1148-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="d1148-104">A *bağımlılık* uygulamanız tarafından çağrılan bir dış bileşendir.</span><span class="sxs-lookup"><span data-stu-id="d1148-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="d1148-105">Bu genellikle HTTP veya bir veritabanı veya bir dosya sistemi kullanılarak adlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="d1148-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="d1148-106">[Application Insights](app-insights-overview.md) uygulamanız için bağımlılıkları ne kadar bekleyeceğini ve ne sıklıkta bir bağımlılık araması başarısız ölçer.</span><span class="sxs-lookup"><span data-stu-id="d1148-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="d1148-107">Belirli çağrıları araştırmak ve bunları istekler ve özel durumlar için ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1148-107">You can investigate specific calls, and relate them to requests and exceptions.</span></span>

![örnek grafikler](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="d1148-109">Giden kutusu bağımlılık İzleyicisi şu anda bu tür bağımlılıkların çağrıları raporları:</span><span class="sxs-lookup"><span data-stu-id="d1148-109">The out-of-the-box dependency monitor currently reports calls to these  types of dependencies:</span></span>

* <span data-ttu-id="d1148-110">Sunucu</span><span class="sxs-lookup"><span data-stu-id="d1148-110">Server</span></span>
  * <span data-ttu-id="d1148-111">SQL veritabanları</span><span class="sxs-lookup"><span data-stu-id="d1148-111">SQL databases</span></span>
  * <span data-ttu-id="d1148-112">ASP.NET web ve HTTP tabanlı bağlamalar kullanan WCF hizmetleri</span><span class="sxs-lookup"><span data-stu-id="d1148-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="d1148-113">Yerel veya uzak HTTP çağrıları</span><span class="sxs-lookup"><span data-stu-id="d1148-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="d1148-114">Azure Cosmos DB, tablo, blob depolama ve sırası</span><span class="sxs-lookup"><span data-stu-id="d1148-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="d1148-115">Web sayfaları</span><span class="sxs-lookup"><span data-stu-id="d1148-115">Web pages</span></span>
  * <span data-ttu-id="d1148-116">AJAX çağrıları</span><span class="sxs-lookup"><span data-stu-id="d1148-116">AJAX calls</span></span>

<span data-ttu-id="d1148-117">Kullanarak Works izleme [bayt kodu Araçları](https://msdn.microsoft.com/library/z9z62c29.aspx) seçili yöntemleri geçici.</span><span class="sxs-lookup"><span data-stu-id="d1148-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="d1148-118">Performansa düzeydedir.</span><span class="sxs-lookup"><span data-stu-id="d1148-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="d1148-119">Aynı zamanda, diğer bağımlılıkları, hem de istemci ve sunucu kodu izlemek için kendi SDK çağrıları yazabilirsiniz kullanarak [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="d1148-119">You can also write your own SDK calls to monitor other dependencies, both in the client and server code, using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="d1148-120">Bağımlılık izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="d1148-120">Set up dependency monitoring</span></span>
<span data-ttu-id="d1148-121">Kısmi bağımlılık bilgi tarafından otomatik olarak toplanan [Application Insights SDK'sı](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="d1148-121">Partial dependency information is collected automatically by the [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="d1148-122">Tam veri almak için ana bilgisayar sunucusu için uygun aracısını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d1148-122">To get complete data, install the appropriate agent for the host server.</span></span>

| <span data-ttu-id="d1148-123">Platform</span><span class="sxs-lookup"><span data-stu-id="d1148-123">Platform</span></span> | <span data-ttu-id="d1148-124">Yükleme</span><span class="sxs-lookup"><span data-stu-id="d1148-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="d1148-125">IIS sunucusu</span><span class="sxs-lookup"><span data-stu-id="d1148-125">IIS Server</span></span> |<span data-ttu-id="d1148-126">Her iki [sunucunuza Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md) veya [uygulamanız .NET Framework 4.6 veya sonrası yükseltme](http://go.microsoft.com/fwlink/?LinkId=528259) yükleyip [Application Insights SDK'sı](app-insights-asp-net.md) uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="d1148-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application to .NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install the [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="d1148-127">Azure Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="d1148-127">Azure Web App</span></span> |<span data-ttu-id="d1148-128">Web uygulama Denetim Masası'ndaki [, web uygulama Denetim Masası'nda Application Insights dikey penceresini açmak](app-insights-azure-web-apps.md) ve yükleme istenirse seçin.</span><span class="sxs-lookup"><span data-stu-id="d1148-128">In your web app control panel, [open the Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="d1148-129">Azure bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="d1148-129">Azure Cloud Service</span></span> |<span data-ttu-id="d1148-130">[Kullanım başlangıç görevi](app-insights-cloudservices.md) veya [yükleme .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="d1148-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-to-find-dependency-data"></a><span data-ttu-id="d1148-131">Bağımlılık verileri nerede bulacağını</span><span class="sxs-lookup"><span data-stu-id="d1148-131">Where to find dependency data</span></span>
* <span data-ttu-id="d1148-132">[Uygulama eşlemesi](#application-map) uygulama ve neighbouring bileşenleri arasındaki bağımlılıkları visualizes.</span><span class="sxs-lookup"><span data-stu-id="d1148-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="d1148-133">[Performans, tarayıcı ve hata dikey pencereleri](#performance-and-blades) sunucu bağımlılık verileri göster.</span><span class="sxs-lookup"><span data-stu-id="d1148-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="d1148-134">[Tarayıcılar dikey penceresinde](#ajax-calls) kullanıcılarınızın tarayıcılarından AJAX çağrıları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d1148-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="d1148-135">[Yavaş ya da başarısız isteklerinden tıklatın aracılığıyla](#diagnose-slow-requests) kendi bağımlılık denetlemek için çağırır.</span><span class="sxs-lookup"><span data-stu-id="d1148-135">[Click through from slow or failed requests](#diagnose-slow-requests) to check their dependency calls.</span></span>
* <span data-ttu-id="d1148-136">[Analytics](#analytics) sorgu bağımlılık verileri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d1148-136">[Analytics](#analytics) can be used to query dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="d1148-137">Uygulama Eşlemesi</span><span class="sxs-lookup"><span data-stu-id="d1148-137">Application Map</span></span>
<span data-ttu-id="d1148-138">Uygulama bileşenleri arasındaki bağımlılıkları keşfetmek için bir görsel Yardım uygulama eşlemesi görür.</span><span class="sxs-lookup"><span data-stu-id="d1148-138">Application Map acts as a visual aid to discovering dependencies between the components of your application.</span></span> <span data-ttu-id="d1148-139">Ayrıca, uygulamanızdan alınan telemetri gelen otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d1148-139">It is automatically generated from the telemetry from your app.</span></span> <span data-ttu-id="d1148-140">Bu örnek AJAX çağrılarını tarayıcı komut dosyaları ve sunucu uygulamasından REST çağrılarını iki dış hizmetler için gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1148-140">This example shows AJAX calls from the browser scripts and REST calls from the server app to two external services.</span></span>

![Uygulama Eşlemesi](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="d1148-142">**Kutularından gidin** ilgili bağımlılık ve diğer grafik.</span><span class="sxs-lookup"><span data-stu-id="d1148-142">**Navigate from the boxes** to relevant dependency and other charts.</span></span>
* <span data-ttu-id="d1148-143">**Harita PIN** için [Pano](app-insights-dashboards.md), burada bu tamamen işlevsel olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d1148-143">**Pin the map** to the [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="d1148-144">[Daha fazla bilgi edinin](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="d1148-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="d1148-145">Performans ve hata dikey pencereleri</span><span class="sxs-lookup"><span data-stu-id="d1148-145">Performance and failure blades</span></span>
<span data-ttu-id="d1148-146">Performans dikey penceresini sunucu uygulama tarafından oluşturulan bağımlılık çağrıları süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1148-146">The performance blade shows the duration of dependency calls made by the server app.</span></span> <span data-ttu-id="d1148-147">Bir Özet Grafik ve çağrısı tarafından bölümlenmiş bir tablo yok.</span><span class="sxs-lookup"><span data-stu-id="d1148-147">There's a summary chart and a table segmented by call.</span></span>

![Performans dikey bağımlılık grafikleri](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="d1148-149">Özet grafikleri veya bu çağrıları ham oluşumları aramak için Tablo öğelerini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d1148-149">Click through the summary charts or the table items to search raw occurrences of these calls.</span></span>

![Bağımlılık çağrısı örnekleri](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="d1148-151">**Hata sayısı** üzerinde gösterilen **hataları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d1148-151">**Failure counts** are shown on the **Failures** blade.</span></span> <span data-ttu-id="d1148-152">Aralık 200-399, veya bilinmeyen olmayan dönüş kodları hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="d1148-152">A failure is any return code that is not in the range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="d1148-153">**% 100 hataları?**</span><span class="sxs-lookup"><span data-stu-id="d1148-153">**100% failures?**</span></span> <span data-ttu-id="d1148-154">-Bu, büyük olasılıkla kısmi bağımlılık verileri yalnızca aldıklarından gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1148-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="d1148-155">Yapmanız [bağımlılık izleme işlevini platformunuz için uygun ayarlama](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="d1148-155">You need to [set up dependency monitoring appropriate to your platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="d1148-156">AJAX çağrıları</span><span class="sxs-lookup"><span data-stu-id="d1148-156">AJAX Calls</span></span>
<span data-ttu-id="d1148-157">Tarayıcılar dikey penceresinde AJAX çağrılarından süresi ve hata oranını gösterir [web sayfalarında JavaScript](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="d1148-157">The Browsers blade shows the duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="d1148-158">Bunlar bağımlılıklar olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d1148-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="d1148-159"><a name="diagnosis"></a>Yavaş istekler tanılama</span><span class="sxs-lookup"><span data-stu-id="d1148-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="d1148-160">Her istek olayı bağımlılık çağrıları, özel durumlar ve uygulamanızı isteği işlerken izlenen diğer olayları ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="d1148-160">Each request event is associated with the dependency calls, exceptions and other events that are tracked while your app is processing the request.</span></span> <span data-ttu-id="d1148-161">Bu nedenle bazı istekleri hatalı gerçekleştiriyorsanız, bir bağımlılık yavaş yanıt nedeniyle olup olmadığını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1148-161">So if some requests are performing badly, you can find out whether it's due to slow responses from a dependency.</span></span>

<span data-ttu-id="d1148-162">Şimdi örneği, yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1148-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-to-dependencies"></a><span data-ttu-id="d1148-163">Gelen istekleri için bağımlılıkları izleme</span><span class="sxs-lookup"><span data-stu-id="d1148-163">Tracing from requests to dependencies</span></span>
<span data-ttu-id="d1148-164">Performans dikey penceresini açın ve istekleri kılavuz bakın:</span><span class="sxs-lookup"><span data-stu-id="d1148-164">Open the Performance blade, and look at the grid of requests:</span></span>

![Ortalamalar ve sayıları istekleriyle listesi](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="d1148-166">Üst biri çok uzun sürüyor.</span><span class="sxs-lookup"><span data-stu-id="d1148-166">The top one is taking very long.</span></span> <span data-ttu-id="d1148-167">Biz zamanın nerede harcandığına çıkışı bulmak, görelim.</span><span class="sxs-lookup"><span data-stu-id="d1148-167">Let's see if we can find out where the time is spent.</span></span>

<span data-ttu-id="d1148-168">Satır ayrı istek olayları görmek için tıklatın:</span><span class="sxs-lookup"><span data-stu-id="d1148-168">Click that row to see individual request events:</span></span>

![İstek örnekleri listesi](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="d1148-170">Daha fazla incelemek ve bu istekle ilişkili uzak bağımlılık çağrıları aşağıya doğru kaydırmak için uzun süre çalışan örnek tıklatın:</span><span class="sxs-lookup"><span data-stu-id="d1148-170">Click any long-running instance to inspect it further, and scroll down to the remote dependency calls related to this request:</span></span>

![Uzak bağımlılıkları çağrıları bulmak, olağan dışı süre tanımla](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="d1148-172">Bu istek bir yerel hizmete çağrıda harcanan zaman bakım çoğu gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="d1148-172">It looks like most of the time servicing this request was spent in a call to a local service.</span></span>

<span data-ttu-id="d1148-173">Daha fazla bilgi için bu satırı seçin:</span><span class="sxs-lookup"><span data-stu-id="d1148-173">Select that row to get more information:</span></span>

![Sorunlu tanımlamak için bu uzak bağımlılık ' a tıklayın](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="d1148-175">Bu sorunu olduğu görülüyor.</span><span class="sxs-lookup"><span data-stu-id="d1148-175">Looks like this is where the problem is.</span></span> <span data-ttu-id="d1148-176">Biz sorun pinpointed, biz yalnızca artık bu nedenle neden bu çağrı çok uzun sürüyor bulmanız.</span><span class="sxs-lookup"><span data-stu-id="d1148-176">We've pinpointed the problem, so now we just need to find out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="d1148-177">İstek zaman çizelgesi</span><span class="sxs-lookup"><span data-stu-id="d1148-177">Request timeline</span></span>
<span data-ttu-id="d1148-178">Farklı bir durumda, özellikle uzun hiçbir bağımlılık çağrısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="d1148-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="d1148-179">Ancak Zaman Çizelgesi görünümüne geçerek, gecikme bizim iç işlem oluştuğu görebiliriz:</span><span class="sxs-lookup"><span data-stu-id="d1148-179">But by switching to the timeline view, we can see where the delay occurred in our internal processing:</span></span>

![Uzak bağımlılıkları çağrıları bulmak, olağan dışı süre tanımla](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="d1148-181">Olduğu anlaşılıyor ilk bağımlılık çağırdıktan sonra neden olan görmek için bizim kod gibi görünmelidir şekilde büyük bir boşluk olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1148-181">There seems to be a big gap after the first dependency call, so we should look at our code to see why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="d1148-182">Canlı sitenizi profil</span><span class="sxs-lookup"><span data-stu-id="d1148-182">Profile your live site</span></span>

<span data-ttu-id="d1148-183">Fikir olduğu zaman gider mi?</span><span class="sxs-lookup"><span data-stu-id="d1148-183">No idea where the time goes?</span></span> <span data-ttu-id="d1148-184">[Application Insights profil oluşturucu](app-insights-profiler.md) HTTP canlı sitenize çağırır ve hangi işlevleri kodunuzda gösterir izlemeleri en uzun zaman aldı.</span><span class="sxs-lookup"><span data-stu-id="d1148-184">The [Application Insights profiler](app-insights-profiler.md) traces HTTP calls to your live site and shows you which functions in your code took the longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="d1148-185">Başarısız istekler</span><span class="sxs-lookup"><span data-stu-id="d1148-185">Failed requests</span></span>
<span data-ttu-id="d1148-186">Başarısız olan istekler başarısız çağrılar bağımlılıkları ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="d1148-186">Failed requests might also be associated with failed calls to dependencies.</span></span> <span data-ttu-id="d1148-187">Yeniden, biz aracılığıyla problemi izlemek için tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1148-187">Again, we can click through to track down the problem.</span></span>

![Başarısız istekler grafiği tıklatın](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="d1148-189">Aracılığıyla başarısız bir istek bir örneğini tıklatın ve onun ilişkili olay bakın.</span><span class="sxs-lookup"><span data-stu-id="d1148-189">Click through to an occurrence of a failed request, and look at its associated events.</span></span>

![Bir istek türünü tıklatın, örnek aynı örneği farklı bir görünümünü almak için özel durum ayrıntıları almak için tıklatın.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="d1148-191">Analiz</span><span class="sxs-lookup"><span data-stu-id="d1148-191">Analytics</span></span>
<span data-ttu-id="d1148-192">Bağımlılıkları izleyebilirsiniz [günlük analizi sorgu dili](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="d1148-192">You can track dependencies in the [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="d1148-193">Bazı örnekler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d1148-193">Here are some examples.</span></span>

* <span data-ttu-id="d1148-194">Tüm başarısız bağımlılık çağrıları bulun:</span><span class="sxs-lookup"><span data-stu-id="d1148-194">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="d1148-195">AJAX çağrıları bulun:</span><span class="sxs-lookup"><span data-stu-id="d1148-195">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="d1148-196">İsteklerle ilişkili bağımlılık çağrıları bulun:</span><span class="sxs-lookup"><span data-stu-id="d1148-196">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="d1148-197">Sayfa görünümleri ile ilişkili Bul AJAX çağrıları:</span><span class="sxs-lookup"><span data-stu-id="d1148-197">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="d1148-198">Özel bağımlılık izleme</span><span class="sxs-lookup"><span data-stu-id="d1148-198">Custom dependency tracking</span></span>
<span data-ttu-id="d1148-199">Standart bağımlılık izleme modülü veritabanları ve REST API'leri gibi dış bağımlılıklar otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="d1148-199">The standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="d1148-200">Ancak, aynı şekilde kabul edilmesi için bazı ek bileşenleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1148-200">But you might want some additional components to be treated in the same way.</span></span>

<span data-ttu-id="d1148-201">Aynı kullanarak bağımlılık bilgi gönderir kod yazabilirsiniz [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) standart modülleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d1148-201">You can write code that sends dependency information, using the same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by the standard modules.</span></span>

<span data-ttu-id="d1148-202">Örneğin, kendiniz yazmak kaydetmedi ile bir derlemeyi kodunuzu yapılandırdıysanız, yanıt sürelerini kolaylaştırır hangi katkı öğrenmek için tüm çağrıları, zaman.</span><span class="sxs-lookup"><span data-stu-id="d1148-202">For example, if you build your code with an assembly that you didn't write yourself, you could time all the calls to it, to find out what contribution it makes to your response times.</span></span> <span data-ttu-id="d1148-203">Application Insights bağımlılık grafikte görüntülenen bu verileri olmasını kullanarak göndermek `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="d1148-203">To have this data displayed in the dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

```C#

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

<span data-ttu-id="d1148-204">Standart bağımlılık izleme modülünü devre dışı geçiş yapmak istiyorsanız, DependencyTrackingTelemetryModule içinde başvurusunu kaldırın [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="d1148-204">If you want to switch off the standard dependency tracking module, remove the reference to DependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d1148-205">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d1148-205">Troubleshooting</span></span>
<span data-ttu-id="d1148-206">*Bağımlılık başarı bayrağı her zaman true veya false gösterir.*</span><span class="sxs-lookup"><span data-stu-id="d1148-206">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="d1148-207">*SQL sorgu tam olarak gösterilmez.*</span><span class="sxs-lookup"><span data-stu-id="d1148-207">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="d1148-208">SDK'ın en son sürüme yükseltin.</span><span class="sxs-lookup"><span data-stu-id="d1148-208">Upgrade to the latest version of the SDK.</span></span> <span data-ttu-id="d1148-209">.NET sürüm 4.6'den az ise:</span><span class="sxs-lookup"><span data-stu-id="d1148-209">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="d1148-210">IIS ana: yükleme [Application Insights Aracısı](app-insights-monitor-performance-live-website-now.md) ana bilgisayar sunucuları üzerinde.</span><span class="sxs-lookup"><span data-stu-id="d1148-210">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on the host servers.</span></span>
  * <span data-ttu-id="d1148-211">Azure web uygulaması: açık Application Insights sekmesinde web uygulama Denetim Masası'nda ve Application Insights yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d1148-211">Azure web app: Open Application Insights tab in the web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="d1148-212">Video</span><span class="sxs-lookup"><span data-stu-id="d1148-212">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="d1148-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1148-213">Next steps</span></span>
* [<span data-ttu-id="d1148-214">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="d1148-214">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="d1148-215">Kullanıcı ve sayfa verileri</span><span class="sxs-lookup"><span data-stu-id="d1148-215">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="d1148-216">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="d1148-216">Availability</span></span>](app-insights-monitor-web-app-availability.md)
