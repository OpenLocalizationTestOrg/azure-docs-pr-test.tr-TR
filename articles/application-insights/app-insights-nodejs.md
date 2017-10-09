---
title: Azure Application Insights ile aaaMonitor Node.js Hizmetleri | Microsoft Docs
description: "Application Insights ile Node.js hizmetlerindeki performansı izleyin ve sorunları tanılayın."
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="b304c-103">Application Insights ile Node.js hizmetlerinizi ve uygulamalarınızı izleme</span><span class="sxs-lookup"><span data-stu-id="b304c-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="b304c-104">[Azure Application Insights](app-insights-overview.md) toohelp dağıttıktan sonra arka uç Hizmetleri ve bileşenleri izler, [bulmak ve hızlı bir şekilde performans ve diğer sorunları tanılamak](app-insights-detect-triage-diagnose.md).</span><span class="sxs-lookup"><span data-stu-id="b304c-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them toohelp you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="b304c-105">Veri merkeziniz, Azure VM’leri, Web Apps ve hatta diğer genel bulutlar dahil herhangi bir yerde barındırılan Node.js hizmetleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b304c-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="b304c-106">tooreceive, depolayıp, izleme verilerinizi keşfedin, yönergeleri tooinclude kodunuzda bir aracı aşağıdaki hello izleyin ve azure'da karşılık gelen bir Application Insights kaynağı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b304c-106">tooreceive, store, and explore your monitoring data, follow hello following instructions tooinclude an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="b304c-107">Merhaba aracı veri toothat kaynak daha detaylı analiz ve araştırması için gönderir.</span><span class="sxs-lookup"><span data-stu-id="b304c-107">hello agent sends data toothat resource for further analysis and exploration.</span></span>

<span data-ttu-id="b304c-108">Merhaba Node.js Aracısı, gelen ve giden HTTP isteklerini, birkaç sistem ölçümleri ve özel durumları otomatik olarak izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b304c-108">hello Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="b304c-109">Sürüm 0.20 sonrası sürümlerde, `mongodb`, `mysql` ve `redis` gibi bazı yaygın üçüncü taraf paketlerini de izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="b304c-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="b304c-110">Tüm olayları tooan gelen HTTP istek bağıntılı daha hızlı sorun giderme için ilgili.</span><span class="sxs-lookup"><span data-stu-id="b304c-110">All events related tooan incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="b304c-111">Uygulamanızı daha fazla yönlerini izleyebilirsiniz ve bunları el ile düzenleme tarafından sistem kullanarak hello Aracısı API'si aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b304c-111">You can monitor more aspects of your app and system by manually instrumenting them using hello agent API described later.</span></span>

![Örnek performans izleme grafikleri](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="b304c-113">Başlarken</span><span class="sxs-lookup"><span data-stu-id="b304c-113">Getting Started</span></span>

<span data-ttu-id="b304c-114">Şimdi, bir uygulama veya hizmet için izlemeyi ayarlama adımlarına bakalım.</span><span class="sxs-lookup"><span data-stu-id="b304c-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="b304c-115"><a name="resource"></a> App Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b304c-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="b304c-116">**Başlamadan önce**, bir Azure aboneliğine sahip olduğunuzdan emin olun veya [ücretsiz olarak yeni bir tane edinin][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="b304c-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="b304c-117">Kuruluşunuzun zaten bir Azure aboneliğiniz varsa, bir yönetici izleyebilirsiniz [bu yönergeleri] [ add-aad-user] tooadd, tooit.</span><span class="sxs-lookup"><span data-stu-id="b304c-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] tooadd you tooit.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="b304c-118">Şimdi toohello oturum [Azure portal] [ portal] ve hello aşağıda gösterildiği gibi bir Application Insights kaynağı oluşturma - "Yeni"'a tıklayın > "Geliştirici Araçları" > "Application Insights".</span><span class="sxs-lookup"><span data-stu-id="b304c-118">Now log in toohello [Azure portal][portal] and create an Application Insights resource as illustrated in hello following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="b304c-119">Merhaba kaynak telemetri verileri, raporlar ve panolar, kural ve uyarı yapılandırma ve daha fazla kaydedilen bu veriler için depolama alanı almak için bir uç nokta içerir.</span><span class="sxs-lookup"><span data-stu-id="b304c-119">hello resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![App Insights kaynağı oluşturma](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="b304c-121">Merhaba kaynak oluşturma sayfasında "Node.js uygulaması" Merhaba uygulama türü açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="b304c-121">On hello resource creation page, choose "Node.js Application" from hello application type drop-down.</span></span> <span data-ttu-id="b304c-122">Merhaba uygulama türü hello varsayılan panolar ve raporlar için oluşturduğunuz belirler.</span><span class="sxs-lookup"><span data-stu-id="b304c-122">hello app type determines hello default set of dashboards and reports created for you.</span></span> <span data-ttu-id="b304c-123">Ancak endişelenmeyin, herhangi bir Application Insights kaynağı herhangi bir dil ve platformdan veri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="b304c-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Yeni App Insights kaynağı formu](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="b304c-125"><a name="agent"></a>Merhaba Node.js aracısını ayarlama</span><span class="sxs-lookup"><span data-stu-id="b304c-125"><a name="agent"></a> Set up hello Node.js agent</span></span>

<span data-ttu-id="b304c-126">Bu verileri toplamak için zaman tooinclude hello aracı, uygulamanızda sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b304c-126">Now it's time tooinclude hello agent in your app so it can gather data.</span></span>
<span data-ttu-id="b304c-127">Başlat, kaynağın izleme anahtarını kopyalayarak (Bundan sonra tooas başvurulan, `ikey`) aşağıda gösterildiği gibi hello portalından.</span><span class="sxs-lookup"><span data-stu-id="b304c-127">Start by copying your resource's Instrumentation Key (hereinafter referred tooas your `ikey`) from hello portal as shown below.</span></span> <span data-ttu-id="b304c-128">Merhaba App Insights sistem toospecify gerekir böylece bu anahtar toomap veri tooyour Azure kaynak kullanır, bir ortam değişkeni veya kodunuz hello Aracısı toouse için.</span><span class="sxs-lookup"><span data-stu-id="b304c-128">hello App Insights system uses this key toomap data tooyour Azure resource so you need toospecify it in an environment variable or your code for hello agent toouse.</span></span>  

![İzleme anahtarını kopyalama](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="b304c-130">Ardından, package.json aracılığıyla hello Node.js Aracısı kitaplığı tooyour uygulamanın bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b304c-130">Next, add hello Node.js agent library tooyour app's dependencies via package.json.</span></span> <span data-ttu-id="b304c-131">Merhaba kök klasörden, uygulamanızın, çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="b304c-131">From hello root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="b304c-132">Şimdi, kodunuzda tooexplicitly yük hello kitaplığı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b304c-132">Now you need tooexplicitly load hello library in your code.</span></span> <span data-ttu-id="b304c-133">Merhaba Aracısı Araçları diğer birçok kitaplıkları içine yerleştirir olduğundan, hatta diğer önce olabildiğince erken yükleyeceğini `require` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="b304c-133">Because hello agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="b304c-134">tooget başlatıldı, ilk .js dosyanızı hello üstüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b304c-134">tooget started, at hello top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="b304c-135">Merhaba `setup` yöntemi yapılandırır hello izleme anahtarını (ve bu nedenle Azure kaynak) toobe varsayılan olarak tüm izlenen öğeler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b304c-135">hello `setup` method configures hello instrumentation key (and thus Azure resource) toobe used by default for all tracked items.</span></span> <span data-ttu-id="b304c-136">Çağrı `start` yapılandırma tamamlanmış toobegin toplamak ve telemetri verileri göndermeye sonra.</span><span class="sxs-lookup"><span data-stu-id="b304c-136">Call `start` after configuration is finished toobegin gathering and sending telemetry data.</span></span>

<span data-ttu-id="b304c-137">Ayrıca bir ikey hello ortam değişkeni APPINSİGHTS'dan aracılığıyla sağlayabilir\_çok el ile geçirme yerine INSTRUMENTATIONKEY `setup()` veya `getClient()`.</span><span class="sxs-lookup"><span data-stu-id="b304c-137">You can also provide an ikey via hello environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually too `setup()` or `getClient()`.</span></span> <span data-ttu-id="b304c-138">Bu yöntem kaydedilmiş kaynak kodu dışında ikeys ve farklı ortamlar için farklı ikeys toospecify tutmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b304c-138">This practice lets you keep ikeys out of committed source code and toospecify different ikeys for different environments.</span></span>

<span data-ttu-id="b304c-139">Ek yapılandırma seçenekleri aşağıda belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b304c-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="b304c-140">Merhaba Aracısı hello araçları anahtar tooany boş dize ayarlayarak telemetri verilerini göndermeden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b304c-140">You can try hello agent without sending telemetry by setting hello instrumentation key tooany non-empty string.</span></span>

### <span data-ttu-id="b304c-141"><a name="monitor"></a> Uygulamanızı izleme</span><span class="sxs-lookup"><span data-stu-id="b304c-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="b304c-142">Hello Aracısı hello Node.js çalışma zamanı hakkında telemetriyi ve ortak bazı üçüncü taraf modüllerin otomatik olarak toplar.</span><span class="sxs-lookup"><span data-stu-id="b304c-142">hello agent automatically gathers telemetry about hello Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="b304c-143">Uygulamayı şimdi toogenerate kullanın Bu verilerin bazıları.</span><span class="sxs-lookup"><span data-stu-id="b304c-143">Use your application now toogenerate some of this data.</span></span>

<span data-ttu-id="b304c-144">Ardından hello [Azure portal] [ portal] daha önce oluşturduğunuz toohello Application Insights kaynağı göz atın ve birkaç veri noktası için ilk, görüntü aşağıdaki hello olduğu gibi hello genel bakış zaman çizelgesi bakın.</span><span class="sxs-lookup"><span data-stu-id="b304c-144">Then, in hello [Azure portal][portal] browse toohello Application Insights resource you created earlier and look for your first few data points in hello Overview timeline, as in hello following image.</span></span> <span data-ttu-id="b304c-145">Daha fazla ayrıntı için hello grafikler aracılığıyla'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b304c-145">Click through hello charts for more details.</span></span>

![İlk veri noktaları](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="b304c-147">Merhaba uygulama harita düğmesini tooview hello topolojisi görüntüsü aşağıdaki hello olduğu gibi uygulamanız için bulunan'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b304c-147">Click hello Application map button tooview hello topology discovered for your app, as in hello following image.</span></span> <span data-ttu-id="b304c-148">Daha fazla ayrıntı için hello eşlemesindeki bileşenleri üzerinden'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b304c-148">Click through components in hello map for more details.</span></span>

![Basit uygulama eşlemesi](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="b304c-150">Uygulamanız hakkında daha fazla bilgi ve diğer görünümlere hello "Araştır" bölümü altında kullanılabilir hello kullanarak sorunlarını giderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b304c-150">Learn more about your app and troubleshoot problems using hello other views available under hello "Investigate" section.</span></span>

![Araştır bölümü](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="b304c-152">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="b304c-152">No data?</span></span>

<span data-ttu-id="b304c-153">Merhaba aracısı veri gönderimi için toplu işlemleri nedeniyle hello Portalı'nda görüntülenen öğelerin önce bir gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="b304c-153">Because hello agent batches data for submission there may be a delay before items are displayed in hello portal.</span></span> <span data-ttu-id="b304c-154">Görmüyorsanız, veri kaynağınızın düzeltmeleri aşağıdaki hello bazılarını deneyin:</span><span class="sxs-lookup"><span data-stu-id="b304c-154">If you don't see data in your resource try some of hello following fixes:</span></span>

* <span data-ttu-id="b304c-155">Merhaba uygulaması bazı daha kullanın; Daha fazla Eylemler toogenerate daha fazla telemetri alın.</span><span class="sxs-lookup"><span data-stu-id="b304c-155">Use hello application some more; take more actions toogenerate more telemetry.</span></span>
* <span data-ttu-id="b304c-156">Tıklatın **yenileme** hello portal kaynak görünümünde.</span><span class="sxs-lookup"><span data-stu-id="b304c-156">Click **Refresh** in hello portal resource view.</span></span> <span data-ttu-id="b304c-157">Grafikler otomatik olarak kendilerini düzenli olarak yeniler, ancak bu toohappen yenilemeyi hemen zorlar.</span><span class="sxs-lookup"><span data-stu-id="b304c-157">Charts automatically refresh themselves periodically but refreshing forces this toohappen immediately.</span></span>
* <span data-ttu-id="b304c-158">[Gerekli giden bağlantı noktalarının](app-insights-ip-addresses.md) açık olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b304c-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="b304c-159">Açık hello [arama](app-insights-diagnostic-search.md) parçasında ve tek tek olaylarını arayın.</span><span class="sxs-lookup"><span data-stu-id="b304c-159">Open hello [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="b304c-160">Merhaba denetleyin [SSS][].</span><span class="sxs-lookup"><span data-stu-id="b304c-160">Check hello [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="b304c-161">Aracı Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="b304c-161">Agent Configuration</span></span>

<span data-ttu-id="b304c-162">Merhaba aracısının yapılandırma yöntemleri ve varsayılan değerlerine aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b304c-162">Following are hello agent's configuration methods and their default values.</span></span>

<span data-ttu-id="b304c-163">bir hizmette toofully correlate olayları olarak emin tooset `.setAutoDependencyCorrelation(true)`.</span><span class="sxs-lookup"><span data-stu-id="b304c-163">toofully correlate events in a service, be sure tooset `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="b304c-164">Bu hello Aracısı tootrack bağlamı Node.js içinde zaman uyumsuz geri aramalar arasında sağlar.</span><span class="sxs-lookup"><span data-stu-id="b304c-164">This allows hello agent tootrack context across asynchronous callbacks in Node.js.</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a><span data-ttu-id="b304c-165">Aracı API'si</span><span class="sxs-lookup"><span data-stu-id="b304c-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="b304c-166">Merhaba .NET Aracısı API tam olarak açıklanan [burada](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="b304c-166">hello .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="b304c-167">İstek, olay, ölçüm veya hello uygulama Öngörüler Node.js istemcisini kullanarak özel durum izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b304c-167">You can track any request, event, metric, or exception using hello Application Insights Node.js client.</span></span> <span data-ttu-id="b304c-168">Merhaba aşağıdaki örnek bazılarını hello göstermektedir kullanılabilir API'ler.</span><span class="sxs-lookup"><span data-stu-id="b304c-168">hello following example demonstrates some of hello available APIs.</span></span>

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="b304c-169">Bağımlılıklarınızı izleme</span><span class="sxs-lookup"><span data-stu-id="b304c-169">Track your dependencies</span></span>

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a><span data-ttu-id="b304c-170">Bir özel özellik tooall olaylar ekleme</span><span class="sxs-lookup"><span data-stu-id="b304c-170">Add a custom property tooall events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="b304c-171">HTTP GET isteklerini izleme</span><span class="sxs-lookup"><span data-stu-id="b304c-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="b304c-172">Sunucu başlangıç saatini izleme</span><span class="sxs-lookup"><span data-stu-id="b304c-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="b304c-173">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b304c-173">More resources</span></span>

* [<span data-ttu-id="b304c-174">Merhaba portalında telemetrinizi izleme</span><span class="sxs-lookup"><span data-stu-id="b304c-174">Monitor your telemetry in hello portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="b304c-175">Telemetriniz üzerinden Analiz sorguları yazma</span><span class="sxs-lookup"><span data-stu-id="b304c-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[SSS]: app-insights-troubleshoot-faq.md
