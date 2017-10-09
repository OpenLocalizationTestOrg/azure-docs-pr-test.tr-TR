---
title: aaaDependency Azure Application Insights izleme | Microsoft Docs
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
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a><span data-ttu-id="a5b5b-103">Application Insights'ı ayarlayın: bağımlılık izleme</span><span class="sxs-lookup"><span data-stu-id="a5b5b-103">Set up Application Insights: Dependency tracking</span></span>
<span data-ttu-id="a5b5b-104">A *bağımlılık* uygulamanız tarafından çağrılan bir dış bileşendir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-104">A *dependency* is an external component that is called by your app.</span></span> <span data-ttu-id="a5b5b-105">Bu genellikle HTTP veya bir veritabanı veya bir dosya sistemi kullanılarak adlı bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-105">It's typically a service called using HTTP, or a database, or a file system.</span></span> <span data-ttu-id="a5b5b-106">[Application Insights](app-insights-overview.md) uygulamanız için bağımlılıkları ne kadar bekleyeceğini ve ne sıklıkta bir bağımlılık araması başarısız ölçer.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-106">[Application Insights](app-insights-overview.md) measures how long your application waits for dependencies and how often a dependency call fails.</span></span> <span data-ttu-id="a5b5b-107">Belirli çağrıları araştırmak ve bunları toorequests ve özel durumları ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-107">You can investigate specific calls, and relate them toorequests and exceptions.</span></span>

![örnek grafikler](./media/app-insights-asp-net-dependencies/10-intro.png)

<span data-ttu-id="a5b5b-109">Merhaba Giden kutusu bağımlılık İzleyicisi şu anda çağrıları toothese tür bağımlılığı raporları:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-109">hello out-of-the-box dependency monitor currently reports calls toothese  types of dependencies:</span></span>

* <span data-ttu-id="a5b5b-110">Sunucu</span><span class="sxs-lookup"><span data-stu-id="a5b5b-110">Server</span></span>
  * <span data-ttu-id="a5b5b-111">SQL veritabanları</span><span class="sxs-lookup"><span data-stu-id="a5b5b-111">SQL databases</span></span>
  * <span data-ttu-id="a5b5b-112">ASP.NET web ve HTTP tabanlı bağlamalar kullanan WCF hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a5b5b-112">ASP.NET web and WCF services that use HTTP-based bindings</span></span>
  * <span data-ttu-id="a5b5b-113">Yerel veya uzak HTTP çağrıları</span><span class="sxs-lookup"><span data-stu-id="a5b5b-113">Local or remote HTTP calls</span></span>
  * <span data-ttu-id="a5b5b-114">Azure Cosmos DB, tablo, blob depolama ve sırası</span><span class="sxs-lookup"><span data-stu-id="a5b5b-114">Azure Cosmos DB, table, blob storage, and queue</span></span>
* <span data-ttu-id="a5b5b-115">Web sayfaları</span><span class="sxs-lookup"><span data-stu-id="a5b5b-115">Web pages</span></span>
  * <span data-ttu-id="a5b5b-116">AJAX çağrıları</span><span class="sxs-lookup"><span data-stu-id="a5b5b-116">AJAX calls</span></span>

<span data-ttu-id="a5b5b-117">Kullanarak Works izleme [bayt kodu Araçları](https://msdn.microsoft.com/library/z9z62c29.aspx) seçili yöntemleri geçici.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-117">Monitoring works by using [byte code instrumentation](https://msdn.microsoft.com/library/z9z62c29.aspx) around selected methods.</span></span> <span data-ttu-id="a5b5b-118">Performansa düzeydedir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-118">Performance overhead is minimal.</span></span>

<span data-ttu-id="a5b5b-119">Kendi SDK çağrıları toomonitor diğer bağımlılıkları, hem de hello istemci ve sunucu kodu hello kullanarak da yazabilirsiniz [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="a5b5b-119">You can also write your own SDK calls toomonitor other dependencies, both in hello client and server code, using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

## <a name="set-up-dependency-monitoring"></a><span data-ttu-id="a5b5b-120">Bağımlılık izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="a5b5b-120">Set up dependency monitoring</span></span>
<span data-ttu-id="a5b5b-121">Kısmi bağımlılık bilgi hello tarafından otomatik olarak toplanır [Application Insights SDK'sı](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="a5b5b-121">Partial dependency information is collected automatically by hello [Application Insights SDK](app-insights-asp-net.md).</span></span> <span data-ttu-id="a5b5b-122">tooget tam veri hello hello ana bilgisayarı sunucusu için uygun aracısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-122">tooget complete data, install hello appropriate agent for hello host server.</span></span>

| <span data-ttu-id="a5b5b-123">Platform</span><span class="sxs-lookup"><span data-stu-id="a5b5b-123">Platform</span></span> | <span data-ttu-id="a5b5b-124">Yükleme</span><span class="sxs-lookup"><span data-stu-id="a5b5b-124">Install</span></span> |
| --- | --- |
| <span data-ttu-id="a5b5b-125">IIS sunucusu</span><span class="sxs-lookup"><span data-stu-id="a5b5b-125">IIS Server</span></span> |<span data-ttu-id="a5b5b-126">Her iki [sunucunuza Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md) veya [, uygulama too.NET framework 4.6 veya sonrası yükseltme](http://go.microsoft.com/fwlink/?LinkId=528259) hello yükleyip [Application Insights SDK'sı](app-insights-asp-net.md) uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-126">Either [install Status Monitor on your server](app-insights-monitor-performance-live-website-now.md) or [Upgrade your application too.NET framework 4.6 or later](http://go.microsoft.com/fwlink/?LinkId=528259) and install hello [Application Insights SDK](app-insights-asp-net.md)  in your app.</span></span> |
| <span data-ttu-id="a5b5b-127">Azure Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="a5b5b-127">Azure Web App</span></span> |<span data-ttu-id="a5b5b-128">Web uygulama Denetim Masası'ndaki [açık hello Application Insights dikey penceresinde, web uygulama Denetim Masası'ndaki](app-insights-azure-web-apps.md) ve yükleme istenirse seçin.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-128">In your web app control panel, [open hello Application Insights blade in your web app control panel](app-insights-azure-web-apps.md) and choose Install if prompted.</span></span> |
| <span data-ttu-id="a5b5b-129">Azure bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="a5b5b-129">Azure Cloud Service</span></span> |<span data-ttu-id="a5b5b-130">[Kullanım başlangıç görevi](app-insights-cloudservices.md) veya [yükleme .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="a5b5b-130">[Use startup task](app-insights-cloudservices.md) or [Install .NET framework 4.6+](../cloud-services/cloud-services-dotnet-install-dotnet.md)</span></span> |

## <a name="where-toofind-dependency-data"></a><span data-ttu-id="a5b5b-131">Burada toofind bağımlılık verileri</span><span class="sxs-lookup"><span data-stu-id="a5b5b-131">Where toofind dependency data</span></span>
* <span data-ttu-id="a5b5b-132">[Uygulama eşlemesi](#application-map) uygulama ve neighbouring bileşenleri arasındaki bağımlılıkları visualizes.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-132">[Application Map](#application-map) visualizes dependencies between your app and neighbouring components.</span></span>
* <span data-ttu-id="a5b5b-133">[Performans, tarayıcı ve hata dikey pencereleri](#performance-and-blades) sunucu bağımlılık verileri göster.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-133">[Performance, browser, and failure blades](#performance-and-blades) show server dependency data.</span></span>
* <span data-ttu-id="a5b5b-134">[Tarayıcılar dikey penceresinde](#ajax-calls) kullanıcılarınızın tarayıcılarından AJAX çağrıları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-134">[Browsers blade](#ajax-calls) shows AJAX calls from your users' browsers.</span></span>
* <span data-ttu-id="a5b5b-135">[Yavaş ya da başarısız isteklerinden tıklatın aracılığıyla](#diagnose-slow-requests) kendi bağımlılık toocheck çağırır.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-135">[Click through from slow or failed requests](#diagnose-slow-requests) toocheck their dependency calls.</span></span>
* <span data-ttu-id="a5b5b-136">[Analytics](#analytics) kullanılan tooquery bağımlılık verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-136">[Analytics](#analytics) can be used tooquery dependency data.</span></span>

## <a name="application-map"></a><span data-ttu-id="a5b5b-137">Uygulama Eşlemesi</span><span class="sxs-lookup"><span data-stu-id="a5b5b-137">Application Map</span></span>
<span data-ttu-id="a5b5b-138">Uygulama eşlemesi, uygulamanızın hello bileşenler arasındaki bir görsel Yardım toodiscovering bağımlılıklar olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-138">Application Map acts as a visual aid toodiscovering dependencies between hello components of your application.</span></span> <span data-ttu-id="a5b5b-139">Merhaba, uygulamanızın telemetrisinden gelen otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-139">It is automatically generated from hello telemetry from your app.</span></span> <span data-ttu-id="a5b5b-140">Bu örnek uygulama tootwo dış hizmetler hello tarayıcı komut dosyalarından AJAX çağrılarını ve REST çağrılarını hello sunucusundan gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-140">This example shows AJAX calls from hello browser scripts and REST calls from hello server app tootwo external services.</span></span>

![Uygulama Eşlemesi](./media/app-insights-asp-net-dependencies/08.png)

* <span data-ttu-id="a5b5b-142">**Merhaba kutularından gidin** toorelevant bağımlılık ve diğer grafik.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-142">**Navigate from hello boxes** toorelevant dependency and other charts.</span></span>
* <span data-ttu-id="a5b5b-143">**PIN hello harita** toohello [Pano](app-insights-dashboards.md), burada bu tamamen işlevsel olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-143">**Pin hello map** toohello [dashboard](app-insights-dashboards.md), where it will be fully functional.</span></span>

<span data-ttu-id="a5b5b-144">[Daha fazla bilgi edinin](app-insights-app-map.md).</span><span class="sxs-lookup"><span data-stu-id="a5b5b-144">[Learn more](app-insights-app-map.md).</span></span>

## <a name="performance-and-failure-blades"></a><span data-ttu-id="a5b5b-145">Performans ve hata dikey pencereleri</span><span class="sxs-lookup"><span data-stu-id="a5b5b-145">Performance and failure blades</span></span>
<span data-ttu-id="a5b5b-146">Merhaba performans dikey penceresinde hello sunucu uygulama tarafından oluşturulan bağımlılık çağrıları hello süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-146">hello performance blade shows hello duration of dependency calls made by hello server app.</span></span> <span data-ttu-id="a5b5b-147">Bir Özet Grafik ve çağrısı tarafından bölümlenmiş bir tablo yok.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-147">There's a summary chart and a table segmented by call.</span></span>

![Performans dikey bağımlılık grafikleri](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

<span data-ttu-id="a5b5b-149">Merhaba Özet grafikleri veya hello Tablo öğeleri toosearch ham oluşumları bu çağrıları tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-149">Click through hello summary charts or hello table items toosearch raw occurrences of these calls.</span></span>

![Bağımlılık çağrısı örnekleri](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

<span data-ttu-id="a5b5b-151">**Hata sayısı** hello üzerinde gösterilen **hataları** dikey.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-151">**Failure counts** are shown on hello **Failures** blade.</span></span> <span data-ttu-id="a5b5b-152">Merhaba aralığı 200-399, veya bilinmeyen olmayan dönüş kodları hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-152">A failure is any return code that is not in hello range 200-399, or unknown.</span></span>

> [!NOTE]
> <span data-ttu-id="a5b5b-153">**% 100 hataları?**</span><span class="sxs-lookup"><span data-stu-id="a5b5b-153">**100% failures?**</span></span> <span data-ttu-id="a5b5b-154">-Bu, büyük olasılıkla kısmi bağımlılık verileri yalnızca aldıklarından gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-154">- This probably indicates that you are only getting partial dependency data.</span></span> <span data-ttu-id="a5b5b-155">Çok ihtiyacınız[uygun tooyour platform izleme bağımlılık ayarlamak](#set-up-dependency-monitoring).</span><span class="sxs-lookup"><span data-stu-id="a5b5b-155">You need too[set up dependency monitoring appropriate tooyour platform](#set-up-dependency-monitoring).</span></span>
>
>

## <a name="ajax-calls"></a><span data-ttu-id="a5b5b-156">AJAX çağrıları</span><span class="sxs-lookup"><span data-stu-id="a5b5b-156">AJAX Calls</span></span>
<span data-ttu-id="a5b5b-157">Merhaba tarayıcılar dikey penceresinde hello süresi gösterir ve hata oranı AJAX çağrıları [web sayfalarında JavaScript](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a5b5b-157">hello Browsers blade shows hello duration and failure rate of AJAX calls from [JavaScript in your web pages](app-insights-javascript.md).</span></span> <span data-ttu-id="a5b5b-158">Bunlar bağımlılıklar olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-158">They are shown as Dependencies.</span></span>

## <span data-ttu-id="a5b5b-159"><a name="diagnosis"></a>Yavaş istekler tanılama</span><span class="sxs-lookup"><span data-stu-id="a5b5b-159"><a name="diagnosis"></a> Diagnose slow requests</span></span>
<span data-ttu-id="a5b5b-160">Her isteği olayı hello bağımlılık çağrıları ile ilişkili olduğundan, özel durumlar ve uygulamanızı işlerken izlenen diğer olayları isteği Merhaba.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-160">Each request event is associated with hello dependency calls, exceptions and other events that are tracked while your app is processing hello request.</span></span> <span data-ttu-id="a5b5b-161">Bu nedenle bazı istekleri hatalı gerçekleştiriyorsanız, bir bağımlılık tooslow yanıtlarının son olup olmadığını bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-161">So if some requests are performing badly, you can find out whether it's due tooslow responses from a dependency.</span></span>

<span data-ttu-id="a5b5b-162">Şimdi örneği, yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-162">Let's walk through an example of that.</span></span>

### <a name="tracing-from-requests-toodependencies"></a><span data-ttu-id="a5b5b-163">İstekleri toodependencies izleme</span><span class="sxs-lookup"><span data-stu-id="a5b5b-163">Tracing from requests toodependencies</span></span>
<span data-ttu-id="a5b5b-164">Merhaba performans dikey penceresini açın ve istekleri hello kılavuz bakın:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-164">Open hello Performance blade, and look at hello grid of requests:</span></span>

![Ortalamalar ve sayıları istekleriyle listesi](./media/app-insights-asp-net-dependencies/02-reqs.png)

<span data-ttu-id="a5b5b-166">Merhaba üst biri çok uzun sürüyor.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-166">hello top one is taking very long.</span></span> <span data-ttu-id="a5b5b-167">Biz hello zamanın nerede harcandığına çıkışı bulmak, görelim.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-167">Let's see if we can find out where hello time is spent.</span></span>

<span data-ttu-id="a5b5b-168">Bu satır toosee ayrı istek olayları tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-168">Click that row toosee individual request events:</span></span>

![İstek örnekleri listesi](./media/app-insights-asp-net-dependencies/03-instances.png)

<span data-ttu-id="a5b5b-170">Daha fazla ve toohello uzak bağımlılık çağrıları ilgili toothis isteği kaydırarak herhangi uzun süre çalışan örnek tooinspect tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-170">Click any long-running instance tooinspect it further, and scroll down toohello remote dependency calls related toothis request:</span></span>

![Çağrıları tooRemote bağımlılıkları bulun, olağan dışı süre tanımla](./media/app-insights-asp-net-dependencies/04-dependencies.png)

<span data-ttu-id="a5b5b-172">Bu istek bir çağrı tooa yerel hizmetinde harcanan zamanı hello bakım çoğu gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-172">It looks like most of hello time servicing this request was spent in a call tooa local service.</span></span>

<span data-ttu-id="a5b5b-173">Bu satır tooget daha fazla bilgi seçin:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-173">Select that row tooget more information:</span></span>

![Bu uzak bağımlılık tooidentify hello sorunlu tıklatın](./media/app-insights-asp-net-dependencies/05-detail.png)

<span data-ttu-id="a5b5b-175">Bu hello sorunu olduğu görülüyor.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-175">Looks like this is where hello problem is.</span></span> <span data-ttu-id="a5b5b-176">Biz hello sorun pinpointed, biz yalnızca artık neden bu çağrı çok uzun sürüyor çıkışı toofind şekilde gerekir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-176">We've pinpointed hello problem, so now we just need toofind out why that call is taking so long.</span></span>

### <a name="request-timeline"></a><span data-ttu-id="a5b5b-177">İstek zaman çizelgesi</span><span class="sxs-lookup"><span data-stu-id="a5b5b-177">Request timeline</span></span>
<span data-ttu-id="a5b5b-178">Farklı bir durumda, özellikle uzun hiçbir bağımlılık çağrısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-178">In a different case, there is no dependency call that is particularly long.</span></span> <span data-ttu-id="a5b5b-179">Ancak toohello Zaman Çizelgesi görünümüne geçiş yaparak hello gecikme bizim iç işlem oluştuğu görebiliriz:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-179">But by switching toohello timeline view, we can see where hello delay occurred in our internal processing:</span></span>

![Çağrıları tooRemote bağımlılıkları bulun, olağan dışı süre tanımla](./media/app-insights-asp-net-dependencies/04-1.png)

<span data-ttu-id="a5b5b-181">Olduğu anlaşılıyor toobe büyük bir boşluk hello ilk bağımlılık çağrısından sonra diğer bir deyişle neden biz bizim kod toosee görünmelidir şekilde.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-181">There seems toobe a big gap after hello first dependency call, so we should look at our code toosee why that is.</span></span>

### <a name="profile-your-live-site"></a><span data-ttu-id="a5b5b-182">Canlı sitenizi profil</span><span class="sxs-lookup"><span data-stu-id="a5b5b-182">Profile your live site</span></span>

<span data-ttu-id="a5b5b-183">Fikir burada hello zaman gider mi? Merhaba [Application Insights profil oluşturucu](app-insights-profiler.md) HTTP tooyour Canlı site çağırır ve hangi işlevleri kodunuzda gösterir izlemeleri hello en uzun zaman aldı.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-183">No idea where hello time goes? hello [Application Insights profiler](app-insights-profiler.md) traces HTTP calls tooyour live site and shows you which functions in your code took hello longest time.</span></span>

## <a name="failed-requests"></a><span data-ttu-id="a5b5b-184">Başarısız istekler</span><span class="sxs-lookup"><span data-stu-id="a5b5b-184">Failed requests</span></span>
<span data-ttu-id="a5b5b-185">Başarısız olan istekler başarısız çağrılar toodependencies ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-185">Failed requests might also be associated with failed calls toodependencies.</span></span> <span data-ttu-id="a5b5b-186">Yeniden, biz hello sorun aşağı tootrack aracılığıyla tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-186">Again, we can click through tootrack down hello problem.</span></span>

![Merhaba başarısız isteklerin grafiği tıklatın](./media/app-insights-asp-net-dependencies/06-fail.png)

<span data-ttu-id="a5b5b-188">Başarısız bir istek tooan geçişi tıklatın ve onun ilişkili olay arayın.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-188">Click through tooan occurrence of a failed request, and look at its associated events.</span></span>

![Bir istek türünü tıklatın, hello örnek tooget tooa farklı görünümünü Merhaba aynı örneği, tooget özel durum ayrıntıları tıklatın.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a><span data-ttu-id="a5b5b-190">Analiz</span><span class="sxs-lookup"><span data-stu-id="a5b5b-190">Analytics</span></span>
<span data-ttu-id="a5b5b-191">Merhaba bağımlılıkları izleyebilirsiniz [günlük analizi sorgu dili](https://docs.loganalytics.io/).</span><span class="sxs-lookup"><span data-stu-id="a5b5b-191">You can track dependencies in hello [Log Analytics query language](https://docs.loganalytics.io/).</span></span> <span data-ttu-id="a5b5b-192">Bazı örnekler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-192">Here are some examples.</span></span>

* <span data-ttu-id="a5b5b-193">Tüm başarısız bağımlılık çağrıları bulun:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-193">Find any failed dependency calls:</span></span>

```

    dependencies | where success != "True" | take 10
```

* <span data-ttu-id="a5b5b-194">AJAX çağrıları bulun:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-194">Find AJAX calls:</span></span>

```

    dependencies | where client_Type == "Browser" | take 10
```

* <span data-ttu-id="a5b5b-195">İsteklerle ilişkili bağımlılık çağrıları bulun:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-195">Find dependency calls associated with requests:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* <span data-ttu-id="a5b5b-196">Sayfa görünümleri ile ilişkili Bul AJAX çağrıları:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-196">Find AJAX calls associated with page views:</span></span>

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a><span data-ttu-id="a5b5b-197">Özel bağımlılık izleme</span><span class="sxs-lookup"><span data-stu-id="a5b5b-197">Custom dependency tracking</span></span>
<span data-ttu-id="a5b5b-198">Merhaba standart bağımlılık izleme modülü veritabanları ve REST API'leri gibi dış bağımlılıklar otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-198">hello standard dependency-tracking module automatically discovers external dependencies such as databases and REST APIs.</span></span> <span data-ttu-id="a5b5b-199">Ancak, bazı ek bileşenleri toobe kabul hello aynı isteyebilirsiniz yolu.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-199">But you might want some additional components toobe treated in hello same way.</span></span>

<span data-ttu-id="a5b5b-200">Bağımlılık bilgi gönderir kod yazabilirsiniz kullanarak, hello aynı [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) hello standart modülleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-200">You can write code that sends dependency information, using hello same [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) that is used by hello standard modules.</span></span>

<span data-ttu-id="a5b5b-201">Örneğin, bir derleme kodunuzu yapı, kendiniz yazmak alamadık, size tüm hello çağrıları tooit zaman hangi katkı kolaylaştırır tooyour yanıt çıkışı toofind zaman.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-201">For example, if you build your code with an assembly that you didn't write yourself, you could time all hello calls tooit, toofind out what contribution it makes tooyour response times.</span></span> <span data-ttu-id="a5b5b-202">toohave hello bağımlılık Application Insights, grafiklerde görüntülenen bu verileri gönder kullanarak `TrackDependency`.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-202">toohave this data displayed in hello dependency charts in Application Insights, send it using `TrackDependency`.</span></span>

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

<span data-ttu-id="a5b5b-203">Tooswitch hello standart bağımlılık izleme modülü kapatmak isterseniz, hello başvuru tooDependencyTrackingTelemetryModule kaldırmak [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="a5b5b-203">If you want tooswitch off hello standard dependency tracking module, remove hello reference tooDependencyTrackingTelemetryModule in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a5b5b-204">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="a5b5b-204">Troubleshooting</span></span>
<span data-ttu-id="a5b5b-205">*Bağımlılık başarı bayrağı her zaman true veya false gösterir.*</span><span class="sxs-lookup"><span data-stu-id="a5b5b-205">*Dependency success flag always shows either true or false.*</span></span>

<span data-ttu-id="a5b5b-206">*SQL sorgu tam olarak gösterilmez.*</span><span class="sxs-lookup"><span data-stu-id="a5b5b-206">*SQL query not shown in full.*</span></span>

* <span data-ttu-id="a5b5b-207">Merhaba SDK toohello en son sürümüne yükseltme.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-207">Upgrade toohello latest version of hello SDK.</span></span> <span data-ttu-id="a5b5b-208">.NET sürüm 4.6'den az ise:</span><span class="sxs-lookup"><span data-stu-id="a5b5b-208">If your .NET version is less than 4.6:</span></span>
  * <span data-ttu-id="a5b5b-209">IIS ana: yükleme [Application Insights Aracısı](app-insights-monitor-performance-live-website-now.md) hello ana bilgisayar sunucuları üzerinde.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-209">IIS host: Install [Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on hello host servers.</span></span>
  * <span data-ttu-id="a5b5b-210">Azure web uygulaması: açık Application Insights sekmesinde hello web uygulama Denetim Masası'nda ve Application Insights yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a5b5b-210">Azure web app: Open Application Insights tab in hello web app control panel, and install Application Insights.</span></span>

## <a name="video"></a><span data-ttu-id="a5b5b-211">Video</span><span class="sxs-lookup"><span data-stu-id="a5b5b-211">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="a5b5b-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a5b5b-212">Next steps</span></span>
* [<span data-ttu-id="a5b5b-213">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="a5b5b-213">Exceptions</span></span>](app-insights-asp-net-exceptions.md)
* [<span data-ttu-id="a5b5b-214">Kullanıcı ve sayfa verileri</span><span class="sxs-lookup"><span data-stu-id="a5b5b-214">User & page data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="a5b5b-215">Kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="a5b5b-215">Availability</span></span>](app-insights-monitor-web-app-availability.md)
