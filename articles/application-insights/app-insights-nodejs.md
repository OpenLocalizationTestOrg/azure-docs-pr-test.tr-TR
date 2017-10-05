---
title: Node.js hizmetlerini Azure Application Insights ile izleme | Microsoft Docs
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
ms.openlocfilehash: ee65207e546c7050cc7bf35c36624fc49ad9eec4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a><span data-ttu-id="bd0bc-103">Application Insights ile Node.js hizmetlerinizi ve uygulamalarınızı izleme</span><span class="sxs-lookup"><span data-stu-id="bd0bc-103">Monitor your Node.js services and apps with Application Insights</span></span>

<span data-ttu-id="bd0bc-104">[Azure Application Insights](app-insights-overview.md), [performans ve diğer sorunları keşfetmeye ve hızlıca tanılamaya](app-insights-detect-triage-diagnose.md) yardımcı olmak üzere, arka uç hizmetlerinizi ve bileşenlerinizi dağıtmanızdan sonra izler.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-104">[Azure Application Insights](app-insights-overview.md) monitors your backend services and components after you deploy them to help you [discover and rapidly diagnose performance and other issues](app-insights-detect-triage-diagnose.md).</span></span> <span data-ttu-id="bd0bc-105">Veri merkeziniz, Azure VM’leri, Web Apps ve hatta diğer genel bulutlar dahil herhangi bir yerde barındırılan Node.js hizmetleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-105">Use it for Node.js services hosted anywhere: your datacenter, Azure VMs and Web Apps, and even other public clouds.</span></span>

<span data-ttu-id="bd0bc-106">İzleme verilerinizi almak, depolamak ve araştırmak için kodunuza aracı ekleme ve Azure’da karşılık gelen Application Insights kaynağını ayarlamaya yönelik aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-106">To receive, store, and explore your monitoring data, follow the following instructions to include an agent in your code and set up a corresponding Application Insights resource in Azure.</span></span> <span data-ttu-id="bd0bc-107">Aracı daha fazla analiz ve araştırma için verileri bu kaynağa gönderir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-107">The agent sends data to that resource for further analysis and exploration.</span></span>

<span data-ttu-id="bd0bc-108">Node.js aracısı gelen ve giden HTTP isteklerini, birçok sistem ölçümünü ve özel durumları otomatik olarak izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-108">The Node.js agent can automatically monitor incoming and outgoing HTTP requests, several system metrics, and exceptions.</span></span> <span data-ttu-id="bd0bc-109">Sürüm 0.20 sonrası sürümlerde, `mongodb`, `mysql` ve `redis` gibi bazı yaygın üçüncü taraf paketlerini de izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-109">Beginning in v0.20, it can also monitor some common third-party packages such as `mongodb`, `mysql`, and `redis`.</span></span> <span data-ttu-id="bd0bc-110">Gelen bir HTTP isteği ile ilgili tüm olaylar, daha hızlı sorun giderme için birbiriyle ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-110">All events related to an incoming HTTP request are correlated for faster troubleshooting.</span></span>

<span data-ttu-id="bd0bc-111">Daha sonra açıklanacak olan aracı API’si ile el ile izleyerek, uygulama ve sisteminizin daha fazla yönünü izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-111">You can monitor more aspects of your app and system by manually instrumenting them using the agent API described later.</span></span>

![Örnek performans izleme grafikleri](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a><span data-ttu-id="bd0bc-113">Başlarken</span><span class="sxs-lookup"><span data-stu-id="bd0bc-113">Getting Started</span></span>

<span data-ttu-id="bd0bc-114">Şimdi, bir uygulama veya hizmet için izlemeyi ayarlama adımlarına bakalım.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-114">Let's step through setting up monitoring for an app or service.</span></span>

### <span data-ttu-id="bd0bc-115"><a name="resource"></a> App Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd0bc-115"><a name="resource"></a> Set up an App Insights resource</span></span>

<span data-ttu-id="bd0bc-116">**Başlamadan önce**, bir Azure aboneliğine sahip olduğunuzdan emin olun veya [ücretsiz olarak yeni bir tane edinin][azure-free-offer].</span><span class="sxs-lookup"><span data-stu-id="bd0bc-116">**Before you start**, make sure you have an Azure subscription or [get a new one for free][azure-free-offer].</span></span> <span data-ttu-id="bd0bc-117">Kuruluşunuzun bir Azure aboneliğini zaten varsa, yöneticiniz [bu yönergeleri][add-aad-user] izleyerek sizi aboneliğe ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-117">If your organization already has an Azure subscription, an administrator can follow [these instructions][add-aad-user] to add you to it.</span></span>

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

<span data-ttu-id="bd0bc-118">Şimdi [Azure portalında][portal] oturum açın ve aşağıda gösterilen şekilde bir Application Insights kaynağı oluşturun - "Yeni" > "Geliştirici araçları" > "Application Insights" öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-118">Now log in to the [Azure portal][portal] and create an Application Insights resource as illustrated in the following - click "New" > "Developer tools" > "Application Insights".</span></span> <span data-ttu-id="bd0bc-119">Kaynak; telemetri verilerini, bu veriler için depolamayı, kayıtlı rapor ve panoları, kural ve uyarı yapılandırmasını almak ve diğer işlemlere yönelik bir uç nokta içerir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-119">The resource includes an endpoint for receiving telemetry data, storage for this data, saved reports and dashboards, rule and alert configuration, and more.</span></span>

![App Insights kaynağı oluşturma](./media/app-insights-nodejs/03-new_appinsights_resource.png)

<span data-ttu-id="bd0bc-121">Kaynak oluşturma sayfasındaki uygulama türü açılır listesinden "Node.js Uygulaması" öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-121">On the resource creation page, choose "Node.js Application" from the application type drop-down.</span></span> <span data-ttu-id="bd0bc-122">Uygulama türü, sizin için oluşturulan varsayılan pano ve rapor kümesini belirler.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-122">The app type determines the default set of dashboards and reports created for you.</span></span> <span data-ttu-id="bd0bc-123">Ancak endişelenmeyin, herhangi bir Application Insights kaynağı herhangi bir dil ve platformdan veri toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-123">Don't worry though, any App Insights resource can in fact collect data from any language and platform.</span></span>

![Yeni App Insights kaynağı formu](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <span data-ttu-id="bd0bc-125"><a name="agent"></a> Node.js aracısını ayarlama</span><span class="sxs-lookup"><span data-stu-id="bd0bc-125"><a name="agent"></a> Set up the Node.js agent</span></span>

<span data-ttu-id="bd0bc-126">Şimdi aracıyı veri toplayabilmesi için uygulamanıza eklemeniz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-126">Now it's time to include the agent in your app so it can gather data.</span></span>
<span data-ttu-id="bd0bc-127">İlk olarak, aşağıda gösterildiği gibi kaynağınızın İzleme Anahtarını (bundan böyle `ikey`‘iniz olarak ifade edilecektir) portaldan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-127">Start by copying your resource's Instrumentation Key (hereinafter referred to as your `ikey`) from the portal as shown below.</span></span> <span data-ttu-id="bd0bc-128">App Insights sistemi, verileri Azure kaynağınıza eşlemek için bu anahtarı kullanır; bu nedenle, bu anahtarı aracının kullanabilmesi için bir ortam değişkeninde ya da kodunuzda belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-128">The App Insights system uses this key to map data to your Azure resource so you need to specify it in an environment variable or your code for the agent to use.</span></span>  

![İzleme anahtarını kopyalama](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

<span data-ttu-id="bd0bc-130">Ardından, Node.js aracı kitaplığını package.json aracılığıyla uygulamanızın bağımlılıklarına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-130">Next, add the Node.js agent library to your app's dependencies via package.json.</span></span> <span data-ttu-id="bd0bc-131">Uygulamanızın kök klasöründen şunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="bd0bc-131">From the root folder of your app, run:</span></span>

```bash
npm install applicationinsights --save
```

<span data-ttu-id="bd0bc-132">Şimdi kitaplığı kodunuza açıkça yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-132">Now you need to explicitly load the library in your code.</span></span> <span data-ttu-id="bd0bc-133">Aracı diğer birçok kitaplığa izleme eklediği için, aracıyı diğer `require` deyimlerinden de önce olmak üzere mümkün olduğunca erken yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-133">Because the agent injects instrumentation into many other libraries, you should load it as early as possible, even before other `require` statements.</span></span> <span data-ttu-id="bd0bc-134">Başlamak için ilk .js dosyanızın üstüne şunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bd0bc-134">To get started, at the top of your first .js file add:</span></span>

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

<span data-ttu-id="bd0bc-135">`setup` yöntemi, izleme anahtarını (ve bu nedenle Azure kaynağını) izlenen tüm öğeler için varsayılan olarak kullanılacak şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-135">The `setup` method configures the instrumentation key (and thus Azure resource) to be used by default for all tracked items.</span></span> <span data-ttu-id="bd0bc-136">Telemetri verilerini toplayıp göndermeye başlamak için yapılandırma tamamlandıktan sonra `start` öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-136">Call `start` after configuration is finished to begin gathering and sending telemetry data.</span></span>

<span data-ttu-id="bd0bc-137">Ayrıca `setup()` veya `getClient()` konumuna el ile geçirmek yerine APPINSIGHTS\_INSTRUMENTATIONKEY ortam değişkeni aracılığıyla bir ikey sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-137">You can also provide an ikey via the environment variable APPINSIGHTS\_INSTRUMENTATIONKEY instead of passing it manually to  `setup()` or `getClient()`.</span></span> <span data-ttu-id="bd0bc-138">Bu uygulama, ikey’leri yürütülen kaynak kodunun dışında tutmanıza ve farklı ortamlar için farklı ikey’ler belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-138">This practice lets you keep ikeys out of committed source code and to specify different ikeys for different environments.</span></span>

<span data-ttu-id="bd0bc-139">Ek yapılandırma seçenekleri aşağıda belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-139">Additional configuration options are documented below.</span></span>

<span data-ttu-id="bd0bc-140">İzleme anahtarını boş olmayan bir dizeye ayarlayarak, aracıyı telemetri göndermeden deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-140">You can try the agent without sending telemetry by setting the instrumentation key to any non-empty string.</span></span>

### <span data-ttu-id="bd0bc-141"><a name="monitor"></a> Uygulamanızı izleme</span><span class="sxs-lookup"><span data-stu-id="bd0bc-141"><a name="monitor"></a> Monitor your app</span></span>

<span data-ttu-id="bd0bc-142">Aracı, Node.js çalışma zamanı ve bazı yaygın üçüncü taraf modülleriyle ilgili telemetriyi otomatik olarak toplar.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-142">The agent automatically gathers telemetry about the Node.js runtime and some common third-party modules.</span></span> <span data-ttu-id="bd0bc-143">Şimdi uygulamanızı kullanarak bu verilerin bazılarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-143">Use your application now to generate some of this data.</span></span>

<span data-ttu-id="bd0bc-144">Ardından, [Azure portalında][portal] daha önce oluşturduğunuz Application Insights kaynağına göz atın ve aşağıdaki görüntüde gösterildiği gibi Genel Bakış zaman çizelgesinde ilk birkaç veri noktanızı arayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-144">Then, in the [Azure portal][portal] browse to the Application Insights resource you created earlier and look for your first few data points in the Overview timeline, as in the following image.</span></span> <span data-ttu-id="bd0bc-145">Daha fazla ayrıntı için grafiklere tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-145">Click through the charts for more details.</span></span>

![İlk veri noktaları](./media/app-insights-nodejs/12-first-perf.png)

<span data-ttu-id="bd0bc-147">Aşağıdaki görüntüde gösterildiği gibi, uygulamanız için bulunan topolojiyi görüntülemek için Uygulama eşlemesi düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-147">Click the Application map button to view the topology discovered for your app, as in the following image.</span></span> <span data-ttu-id="bd0bc-148">Daha fazla bilgi için eşlemedeki bileşenlere tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-148">Click through components in the map for more details.</span></span>

![Basit uygulama eşlemesi](./media/app-insights-nodejs/06-appinsights_appmap.png)

<span data-ttu-id="bd0bc-150">Uygulamanız hakkında daha fazla bilgi almak ve sorunları gidermek için "Araştır" bölümü altında mevcut olan diğer görünümleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-150">Learn more about your app and troubleshoot problems using the other views available under the "Investigate" section.</span></span>

![Araştır bölümü](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a><span data-ttu-id="bd0bc-152">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="bd0bc-152">No data?</span></span>

<span data-ttu-id="bd0bc-153">Aracı gönderilecek verileri toplu hale getirdiği için, öğelerin portalde gösterilmesi biraz gecikebilir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-153">Because the agent batches data for submission there may be a delay before items are displayed in the portal.</span></span> <span data-ttu-id="bd0bc-154">Verileri kaynağınızda görmüyorsanız, aşağıdaki düzeltmelerden bazılarını deneyin:</span><span class="sxs-lookup"><span data-stu-id="bd0bc-154">If you don't see data in your resource try some of the following fixes:</span></span>

* <span data-ttu-id="bd0bc-155">Uygulamayı biraz daha kullanın; daha fazla telemetri oluşturmak için daha fazla eylem gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-155">Use the application some more; take more actions to generate more telemetry.</span></span>
* <span data-ttu-id="bd0bc-156">Portal kaynak görünümünde **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-156">Click **Refresh** in the portal resource view.</span></span> <span data-ttu-id="bd0bc-157">Grafikler kendilerini düzenli aralıklarla otomatik olarak yeniler, ancak yenileme işlemi bunu hemen gerçekleşmeye zorlar.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-157">Charts automatically refresh themselves periodically but refreshing forces this to happen immediately.</span></span>
* <span data-ttu-id="bd0bc-158">[Gerekli giden bağlantı noktalarının](app-insights-ip-addresses.md) açık olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-158">Verify that [needed outgoing ports](app-insights-ip-addresses.md) are open.</span></span>
* <span data-ttu-id="bd0bc-159">[Ara](app-insights-diagnostic-search.md) kutucuğunu açın ve olayları tek tek arayın.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-159">Open the [Search](app-insights-diagnostic-search.md) tile and look for individual events.</span></span>
* <span data-ttu-id="bd0bc-160">[SSS][] sayfasını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-160">Check the [FAQ][].</span></span>


## <a name="agent-configuration"></a><span data-ttu-id="bd0bc-161">Aracı Yapılandırması</span><span class="sxs-lookup"><span data-stu-id="bd0bc-161">Agent Configuration</span></span>

<span data-ttu-id="bd0bc-162">Aracının yapılandırma yöntemleri ve varsayılan değerleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-162">Following are the agent's configuration methods and their default values.</span></span>

<span data-ttu-id="bd0bc-163">Bir hizmetteki olayları tam olarak ilişkilendirmek için `.setAutoDependencyCorrelation(true)` ayarını yaptığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-163">To fully correlate events in a service, be sure to set `.setAutoDependencyCorrelation(true)`.</span></span> <span data-ttu-id="bd0bc-164">Bunun yapılması, aracının Node.js içindeki zaman uyumsuz geri çağırmalar arasında içeriği izlemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-164">This allows the agent to track context across asynchronous callbacks in Node.js.</span></span>

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

## <a name="agent-api"></a><span data-ttu-id="bd0bc-165">Aracı API'si</span><span class="sxs-lookup"><span data-stu-id="bd0bc-165">Agent API</span></span>

<!-- TODO: Fully document agent API. -->

<span data-ttu-id="bd0bc-166">.NET aracı API’si [burada](app-insights-api-custom-events-metrics.md) eksiksiz olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-166">The .NET agent API is fully described [here](app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="bd0bc-167">Application Insights Node.js istemcisini kullanarak herhangi bir istek, olay, ölçüm veya özel durumu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-167">You can track any request, event, metric, or exception using the Application Insights Node.js client.</span></span> <span data-ttu-id="bd0bc-168">Aşağıdaki örnek, kullanılabilir API'lerden bazılarını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="bd0bc-168">The following example demonstrates some of the available APIs.</span></span>

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
  client.trackRequest(req, res); // Place at the beginning of your request handler
});
```

### <a name="track-your-dependencies"></a><span data-ttu-id="bd0bc-169">Bağımlılıklarınızı izleme</span><span class="sxs-lookup"><span data-stu-id="bd0bc-169">Track your dependencies</span></span>

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

### <a name="add-a-custom-property-to-all-events"></a><span data-ttu-id="bd0bc-170">Tüm olaylara özel bir özellik ekleme</span><span class="sxs-lookup"><span data-stu-id="bd0bc-170">Add a custom property to all events</span></span>

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a><span data-ttu-id="bd0bc-171">HTTP GET isteklerini izleme</span><span class="sxs-lookup"><span data-stu-id="bd0bc-171">Track HTTP GET requests</span></span>

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a><span data-ttu-id="bd0bc-172">Sunucu başlangıç saatini izleme</span><span class="sxs-lookup"><span data-stu-id="bd0bc-172">Track server startup time</span></span>

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a><span data-ttu-id="bd0bc-173">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bd0bc-173">More resources</span></span>

* [<span data-ttu-id="bd0bc-174">Portalda telemetrinizi izleme</span><span class="sxs-lookup"><span data-stu-id="bd0bc-174">Monitor your telemetry in the portal</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="bd0bc-175">Telemetriniz üzerinden Analiz sorguları yazma</span><span class="sxs-lookup"><span data-stu-id="bd0bc-175">Write Analytics queries over your telemetry</span></span>](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
<span data-ttu-id="bd0bc-176">[SSS]: app-insights-troubleshoot-faq.md</span><span class="sxs-lookup"><span data-stu-id="bd0bc-176">[FAQ]: app-insights-troubleshoot-faq.md</span></span>
