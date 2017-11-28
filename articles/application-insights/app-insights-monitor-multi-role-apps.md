---
title: "aaaAzure Application Insights birden çok bileşenleri, mikro ve kapsayıcıları için desteği | Microsoft Docs"
description: "Birden çok bileşenleri veya performans ve kullanım için rolleri oluşur uygulamaları izleme."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="939fb-103">Application Insights (Önizleme) ile birden çok bileşen uygulamaları izleme</span><span class="sxs-lookup"><span data-stu-id="939fb-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="939fb-104">Birden çok sunucu bileşenlerini, roller veya hizmetlerle oluşur uygulamaları izleyebilirsiniz [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="939fb-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="939fb-105">Merhaba durumunu hello bileşenler ve aralarındaki ilişkilerin hello tek bir uygulama harita üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="939fb-105">hello health of hello components and hello relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="939fb-106">Tek tek işlemleri otomatik HTTP bağıntı ile birden çok bileşeni aracılığıyla izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="939fb-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="939fb-107">Kapsayıcı tanılama tümleşiktir ve uygulama telemetri ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="939fb-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="939fb-108">Tek bir Application Insights kaynağı hello bileşenlerinin tümünü uygulamanız için kullanın.</span><span class="sxs-lookup"><span data-stu-id="939fb-108">Use a single Application Insights resource for all hello components of your application.</span></span> 

![Birden çok bileşen uygulama eşlemesi](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="939fb-110">'Bileşeni' kullanırız burada toomean büyük bir uygulama, herhangi bir işlevsel parçası.</span><span class="sxs-lookup"><span data-stu-id="939fb-110">We use 'component' here toomean any functioning part of a large application.</span></span> <span data-ttu-id="939fb-111">Örneğin, tipik iş uygulaması tooone Konuşmayı web tarayıcısında çalışan istemci kodunun oluşabilir veya hizmetleri sırayla geri kullanan daha fazla web uygulama hizmetleri bitemez.</span><span class="sxs-lookup"><span data-stu-id="939fb-111">For example, a typical business application may consist of client code running in web browsers, talking tooone or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="939fb-112">Sunucu bileşenleri barındırılan şirket içi hello bulutta üzerinde olabilir ya da Azure web ve çalışan rolleri olabilir veya kapsayıcılarında Docker veya Service Fabric gibi çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="939fb-112">Server components may be hosted on-premises on in hello cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="939fb-113">Tek bir Application Insights kaynağı paylaşma</span><span class="sxs-lookup"><span data-stu-id="939fb-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="939fb-114">Merhaba burada anahtar tekniği olan, uygulama toohello her bileşenin toosend telemetrisinden aynı Application Insights kaynağı ancak kullanım hello `cloud_RoleName` özelliği toodistinguish bileşenleri gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="939fb-114">hello key technique here is toosend telemetry from every component in your application toohello same Application Insights resource, but use hello `cloud_RoleName` property toodistinguish components when necessary.</span></span> <span data-ttu-id="939fb-115">Merhaba Application Insights SDK'sı ekler hello `cloud_RoleName` özelliği toohello telemetri bileşenleri yayma.</span><span class="sxs-lookup"><span data-stu-id="939fb-115">hello Application Insights SDK adds hello `cloud_RoleName` property toohello telemetry components emit.</span></span> <span data-ttu-id="939fb-116">Örneğin, hello SDK web sitesi adı ya da hizmet rol adı toohello ekleyeceksiniz `cloud_RoleName` özelliği.</span><span class="sxs-lookup"><span data-stu-id="939fb-116">For example, hello SDK will add a web site name, or service role name toohello `cloud_RoleName` property.</span></span> <span data-ttu-id="939fb-117">Bu değer bir telemetryinitializer ile geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="939fb-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="939fb-118">Merhaba uygulama eşlemesi kullanan hello `cloud_RoleName` özelliği tooidentify hello bileşenleri hello haritaya.</span><span class="sxs-lookup"><span data-stu-id="939fb-118">hello Application Map uses hello `cloud_RoleName` property tooidentify hello components on hello map.</span></span>

<span data-ttu-id="939fb-119">Hakkında daha fazla bilgi için hello geçersiz kılma `cloud_RoleName` özelliği bakın [özellikleri ekleyin: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="939fb-119">For more information about how do override hello `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="939fb-120">Bazı durumlarda, bu uygun olmayabilir ve toouse ayrı kaynaklar bileşenleri farklı kullanıcı grupları için tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="939fb-120">In some cases, this may not be appropriate, and you may prefer toouse separate resources for different groups of components.</span></span> <span data-ttu-id="939fb-121">Örneğin, yönetim veya faturalandırma için toouse farklı kaynaklar gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="939fb-121">For example, you might need toouse different resources for management or billing purposes.</span></span> <span data-ttu-id="939fb-122">Ayrı kaynaklarını kullanan tüm hello bileşenleri tek bir uygulama haritada görüntülenmelerini görmüyorum anlamına gelir; ve bileşenler arasında sorgulanamıyor [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="939fb-122">Using separate resources means that you don't see all hello components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="939fb-123">Tooset hello ayrı kaynakları da vardır.</span><span class="sxs-lookup"><span data-stu-id="939fb-123">You also have tooset up hello separate resources.</span></span>

<span data-ttu-id="939fb-124">Bu uyarısıyla birlikte, bu belgenin hello kalan birden çok bileşenleri tooone Application Insights kaynağı toosend verileri istediğiniz varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="939fb-124">With that caveat, we'll assume in hello rest of this document that you want toosend data from multiple components tooone Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="939fb-125">Birden çok bileşen uygulamaları yapılandır</span><span class="sxs-lookup"><span data-stu-id="939fb-125">Configure multi-component applications</span></span>

<span data-ttu-id="939fb-126">birden çok bileşen uygulama tooget eşleme, bu hedefleri tooachieve gerekir:</span><span class="sxs-lookup"><span data-stu-id="939fb-126">tooget a multi-component application map, you need tooachieve these goals:</span></span>

* <span data-ttu-id="939fb-127">**Merhaba en son sürüm öncesi yüklemek** her bileşenin hello uygulamasının Application Insights paketinde.</span><span class="sxs-lookup"><span data-stu-id="939fb-127">**Install hello latest pre-release** Application Insights package in each component of hello application.</span></span> 
* <span data-ttu-id="939fb-128">**Tek bir Application Insights kaynağı paylaşma** tüm uygulama bileşenleri hello için.</span><span class="sxs-lookup"><span data-stu-id="939fb-128">**Share a single Application Insights resource** for all hello components of your application.</span></span>
* <span data-ttu-id="939fb-129">**Birden çok rol uygulama eşlemesi etkinleştirmek** hello önizlemeleri dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="939fb-129">**Enable Multi-role Application Map** in hello Previews blade.</span></span>

<span data-ttu-id="939fb-130">Her bileşen türü için hello uygun yöntemi kullanarak, uygulamanızın yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="939fb-130">Configure each component of your application using hello appropriate method for its type.</span></span> <span data-ttu-id="939fb-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="939fb-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-hello-latest-pre-release-package"></a><span data-ttu-id="939fb-132">1. Merhaba en son sürüm öncesi paketini yükle</span><span class="sxs-lookup"><span data-stu-id="939fb-132">1. Install hello latest pre-release package</span></span>

<span data-ttu-id="939fb-133">Güncelleştirme veya hello projesinde her sunucu bileşeni için hello kullanılıyor Öngörüler paketlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="939fb-133">Update or install hello Appication Insights packages in hello project for each server component.</span></span> <span data-ttu-id="939fb-134">Visual Studio kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="939fb-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="939fb-135">Bir projeye sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="939fb-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="939fb-136">Seçin **dahil et**.</span><span class="sxs-lookup"><span data-stu-id="939fb-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="939fb-137">Application Insights paketleri güncelleştirmelerinde görünmüyorsa, bunları seçin.</span><span class="sxs-lookup"><span data-stu-id="939fb-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="939fb-138">Aksi takdirde, göz atın ve hello uygun paket yükleyin:</span><span class="sxs-lookup"><span data-stu-id="939fb-138">Otherwise, browse for and install hello appropriate package:</span></span>
    
    * <span data-ttu-id="939fb-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="939fb-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="939fb-140">Microsoft.ApplicationInsights.ServiceFabric - Konuk yürütülebilir dosyalar ve Docker kapsayıcıları içinde bir Service Fabric uygulaması çalıştıran çalışan bileşenleri için</span><span class="sxs-lookup"><span data-stu-id="939fb-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="939fb-141">Microsoft.ApplicationInsights.ServiceFabric.Native - ServiceFabric uygulamaları güvenilir hizmetler için</span><span class="sxs-lookup"><span data-stu-id="939fb-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="939fb-142">Docker içinde Kubernetes üzerinde çalışan bileşenleri için Microsoft.ApplicationInsights.Kubernetes</span><span class="sxs-lookup"><span data-stu-id="939fb-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="939fb-143">2. Tek bir Application Insights kaynağı paylaşma</span><span class="sxs-lookup"><span data-stu-id="939fb-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="939fb-144">Visual Studio'da bir projeye sağ tıklayın ve seçin **yapılandırma Application Insights**, veya **Application Insights > yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="939fb-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="939fb-145">Merhaba ilk projeniz için hello Sihirbazı toocreate Application Insights kaynağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="939fb-145">For hello first project, use hello wizard toocreate an Application Insights resource.</span></span> <span data-ttu-id="939fb-146">Sonraki projeleri için aynı kaynak Seç hello.</span><span class="sxs-lookup"><span data-stu-id="939fb-146">For subsequent projects, select hello same resource.</span></span>
* <span data-ttu-id="939fb-147">Application Insights menü ise, el ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="939fb-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="939fb-148">İçinde [Azure portal](https://portal,azure.com), başka bir bileşen için önceden oluşturulmuş hello Application Insights kaynağı açın.</span><span class="sxs-lookup"><span data-stu-id="939fb-148">In [Azure portal](https://portal,azure.com), open hello Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="939fb-149">Merhaba genel bakış dikey penceresinde, açık hello Essentials açılan sekmesi ve kopyalama hello **izleme anahtarı.**</span><span class="sxs-lookup"><span data-stu-id="939fb-149">In hello Overview blade, open hello Essentials drop-down tab, and copy hello **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="939fb-150">Projenizdeki Applicationınsights.config açın ve Ekle:`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="939fb-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Merhaba araçları anahtar toohello .config dosyasını kopyalayın](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="939fb-152">3. Birden çok rol uygulama eşlemesi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="939fb-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="939fb-153">Hello Azure portal, uygulamanız için hello kaynak açın.</span><span class="sxs-lookup"><span data-stu-id="939fb-153">In hello Azure portal, open hello resource for your application.</span></span> <span data-ttu-id="939fb-154">Merhaba önizlemeleri dikey penceresinde, etkinleştirme *birden çok rol uygulama eşlemesi*.</span><span class="sxs-lookup"><span data-stu-id="939fb-154">In hello Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="939fb-155">4. Docker ölçümleri (isteğe bağlı) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="939fb-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="939fb-156">Bir bileşen bir Azure Windows VM üzerinde barındırılan bir Docker çalıştırıyorsa, ek ölçümler hello kapsayıcıdan toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="939fb-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from hello container.</span></span> <span data-ttu-id="939fb-157">Bu konuda eklemek, [Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics.md) yapılandırma dosyası:</span><span class="sxs-lookup"><span data-stu-id="939fb-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a><span data-ttu-id="939fb-158">Cloud_RoleName tooseparate bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="939fb-158">Use cloud_RoleName tooseparate components</span></span>

<span data-ttu-id="939fb-159">Merhaba `cloud_RoleName` ekli tooall telemetri bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="939fb-159">hello `cloud_RoleName` property is attached tooall telemetry.</span></span> <span data-ttu-id="939fb-160">Merhaba telemetri kaynaklanan hello bileşen - hello rol veya hizmete - tanımlar.</span><span class="sxs-lookup"><span data-stu-id="939fb-160">It identifies hello component - hello role or service - that originates hello telemetry.</span></span> <span data-ttu-id="939fb-161">(Bu, aynı paralel olarak birden çok sunucu işlemlerini veya makinelerde çalışan aynı roller ayıran cloud_RoleInstance olarak hello yok olur.)</span><span class="sxs-lookup"><span data-stu-id="939fb-161">(It is not hello same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="939fb-162">Merhaba Portalı'nda, filtre ya da bu özelliği kullanan telemetrinizi segmentlere.</span><span class="sxs-lookup"><span data-stu-id="939fb-162">In hello portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="939fb-163">Bu örnekte, hello hataları dikey penceresinde hello CRM API arka uç hatalarından çıkışı filtreleme hello ön uç web hizmetinden, filtrelenmiş tooshow yalnızca bilgiler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="939fb-163">In this example, hello Failures blade is filtered tooshow just information from hello front-end web service, filtering out failures from hello CRM API backend:</span></span>

![Bulut rolü adıyla kesimli ölçüm grafik](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="939fb-165">Bileşenleri arasında izleme işlemleri</span><span class="sxs-lookup"><span data-stu-id="939fb-165">Trace operations between components</span></span>

<span data-ttu-id="939fb-166">Bir bileşen tooanother, tek bir işlem işlenirken yapılan hello çağrıları alanından izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="939fb-166">You can trace from one component tooanother, hello calls made while processing an individual operation.</span></span>


![İşlem için telemetri Göster](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="939fb-168">Bu işlem için telemetri tooa bağıntılı listesi kullanılarak hello ön uç web sunucusunu ve hello arka uç API'si üzerinden tıklatın:</span><span class="sxs-lookup"><span data-stu-id="939fb-168">Click through tooa correlated list of telemetry for this operation across hello front-end web server and hello back-end API:</span></span>

![Bileşenler genelinde arama](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="939fb-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="939fb-170">Next steps</span></span>

* [<span data-ttu-id="939fb-171">Geliştirme, Test ve üretim ayrı telemetri</span><span class="sxs-lookup"><span data-stu-id="939fb-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
