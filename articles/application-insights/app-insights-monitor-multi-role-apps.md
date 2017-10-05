---
title: "Azure Application Insights, birden çok bileşenleri, mikro ve kapsayıcıları için desteği | Microsoft Docs"
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
ms.openlocfilehash: ca1bb8ee886c4b4e69be9dd653d6a52b874e1f5a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="ecdfe-103">Application Insights (Önizleme) ile birden çok bileşen uygulamaları izleme</span><span class="sxs-lookup"><span data-stu-id="ecdfe-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="ecdfe-104">Birden çok sunucu bileşenlerini, roller veya hizmetlerle oluşur uygulamaları izleyebilirsiniz [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecdfe-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="ecdfe-105">Bileşenler ve aralarındaki ilişkilerin durumunu tek bir uygulama harita üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="ecdfe-106">Tek tek işlemleri otomatik HTTP bağıntı ile birden çok bileşeni aracılığıyla izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="ecdfe-107">Kapsayıcı tanılama tümleşiktir ve uygulama telemetri ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="ecdfe-108">Tek bir Application Insights kaynağı, uygulamanızın tüm bileşenler için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![Birden çok bileşen uygulama eşlemesi](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="ecdfe-110">'Bileşen' burada büyük bir uygulamanın düzgün herhangi bir kısmını anlamına için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="ecdfe-111">Örneğin, tipik iş uygulaması bir konuşma web tarayıcılarında çalışan istemci kodunun oluşabilir veya hizmetleri sırayla geri kullanan daha fazla web uygulama hizmetleri bitemez.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="ecdfe-112">Sunucu bileşenleri içi barındırılan buluta üzerinde olabilir ya da Azure web ve çalışan rolleri olabilir veya kapsayıcılarında Docker veya Service Fabric gibi çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="ecdfe-113">Tek bir Application Insights kaynağı paylaşma</span><span class="sxs-lookup"><span data-stu-id="ecdfe-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="ecdfe-114">Anahtar burada her bileşen aynı Application Insights kaynağı için uygulamanızda telemetri gönderen, ancak kullanmak için bir tekniktir `cloud_RoleName` bileşenleri gerektiğinde ayırt etmek için özellik.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="ecdfe-115">Application Insights SDK'sı ekler `cloud_RoleName` telemetri bileşenleri özelliğine yayma.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="ecdfe-116">Örneğin, SDK'yı bir web sitesi adı ya da hizmet rol adı için ekleyecek `cloud_RoleName` özelliği.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="ecdfe-117">Bu değer bir telemetryinitializer ile geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="ecdfe-118">Uygulama eşlemesi kullanan `cloud_RoleName` harita üzerinde bileşenleri tanımlamak için özellik.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="ecdfe-119">Hakkında daha fazla bilgi için geçersiz kılma `cloud_RoleName` özelliği bakın [özellikleri ekleyin: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="ecdfe-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="ecdfe-120">Bazı durumlarda, bu uygun olmayabilir ve farklı bileşenleri grupları için ayrı kaynakları kullanmayı tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="ecdfe-121">Örneğin, farklı kaynaklarının yönetim veya faturalandırma amaçları için kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="ecdfe-122">Ayrı kaynakları kullanarak tek bir uygulama haritada görüntülenmelerini tüm bileşenleri görmüyorum anlamına gelir; ve bileşenler arasında sorgulanamıyor [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="ecdfe-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="ecdfe-123">Ayrıca ayrı kaynakları ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="ecdfe-124">Bu uyarı ile bir Application Insights kaynağı için birden çok bileşenlerinden veri göndermek istediğiniz bu belgenin geri kalanında varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="ecdfe-125">Birden çok bileşen uygulamaları yapılandır</span><span class="sxs-lookup"><span data-stu-id="ecdfe-125">Configure multi-component applications</span></span>

<span data-ttu-id="ecdfe-126">Birden çok bileşen uygulama eşlemesi almak için bu hedefleri başarmanın gerekir:</span><span class="sxs-lookup"><span data-stu-id="ecdfe-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="ecdfe-127">**En son ön sürümü yüklemek** her bileşen uygulamanın Application Insights paketinde.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="ecdfe-128">**Tek bir Application Insights kaynağı paylaşma** uygulamanızın tüm bileşenler için.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="ecdfe-129">**Birden çok rol uygulama eşlemesi etkinleştirmek** önizlemeleri dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-129">**Enable Multi-role Application Map** in the Previews blade.</span></span>

<span data-ttu-id="ecdfe-130">Her bileşen türü için uygun yöntemi kullanarak, uygulamanızın yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="ecdfe-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="ecdfe-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="ecdfe-132">1. En son sürüm öncesi paketini yükle</span><span class="sxs-lookup"><span data-stu-id="ecdfe-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="ecdfe-133">Güncelleştirme veya her sunucu bileşeni için projedeki kullanılıyor Öngörüler paketlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-133">Update or install the Appication Insights packages in the project for each server component.</span></span> <span data-ttu-id="ecdfe-134">Visual Studio kullanıyorsanız:</span><span class="sxs-lookup"><span data-stu-id="ecdfe-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="ecdfe-135">Bir projeye sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="ecdfe-136">Seçin **dahil et**.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="ecdfe-137">Application Insights paketleri güncelleştirmelerinde görünmüyorsa, bunları seçin.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="ecdfe-138">Aksi takdirde, göz atın ve uygun paketi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ecdfe-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="ecdfe-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="ecdfe-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="ecdfe-140">Microsoft.ApplicationInsights.ServiceFabric - Konuk yürütülebilir dosyalar ve Docker kapsayıcıları içinde bir Service Fabric uygulaması çalıştıran çalışan bileşenleri için</span><span class="sxs-lookup"><span data-stu-id="ecdfe-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="ecdfe-141">Microsoft.ApplicationInsights.ServiceFabric.Native - ServiceFabric uygulamaları güvenilir hizmetler için</span><span class="sxs-lookup"><span data-stu-id="ecdfe-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="ecdfe-142">Docker içinde Kubernetes üzerinde çalışan bileşenleri için Microsoft.ApplicationInsights.Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ecdfe-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="ecdfe-143">2. Tek bir Application Insights kaynağı paylaşma</span><span class="sxs-lookup"><span data-stu-id="ecdfe-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="ecdfe-144">Visual Studio'da bir projeye sağ tıklayın ve seçin **yapılandırma Application Insights**, veya **Application Insights > yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="ecdfe-145">İlk projeniz için Application Insights kaynağı oluşturmak için sihirbazı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="ecdfe-146">Sonraki projeleri için aynı kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="ecdfe-147">Application Insights menü ise, el ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="ecdfe-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="ecdfe-148">İçinde [Azure portal](https://portal,azure.com), başka bir bileşen için önceden oluşturulmuş Application Insights kaynağı açın.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="ecdfe-149">Genel Bakış dikey penceresinde, açık Essentials açılan sekmesi ve kopyalama **izleme anahtarı.**</span><span class="sxs-lookup"><span data-stu-id="ecdfe-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="ecdfe-150">Projenizdeki Applicationınsights.config açın ve Ekle:`<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="ecdfe-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![.Config dosyasına izleme anahtarını kopyalama](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a><span data-ttu-id="ecdfe-152">3. Birden çok rol uygulama eşlemesi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ecdfe-152">3. Enable multi-role Application Map</span></span>

<span data-ttu-id="ecdfe-153">Azure Portal'da, uygulamanız için kaynak açın.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="ecdfe-154">Önizlemeler dikey penceresinde, etkinleştirme *birden çok rol uygulama eşlemesi*.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-154">In the Previews blade, enable *Multi-role Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="ecdfe-155">4. Docker ölçümleri (isteğe bağlı) etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ecdfe-155">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="ecdfe-156">Bir bileşen bir Azure Windows VM üzerinde barındırılan bir Docker çalıştırıyorsa, kapsayıcıdan ek ölçümler toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-156">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="ecdfe-157">Bu konuda eklemek, [Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics.md) yapılandırma dosyası:</span><span class="sxs-lookup"><span data-stu-id="ecdfe-157">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

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

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="ecdfe-158">Bileşenleri ayırmak için cloud_RoleName kullanın</span><span class="sxs-lookup"><span data-stu-id="ecdfe-158">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="ecdfe-159">`cloud_RoleName` Özelliği tüm telemetri eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-159">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="ecdfe-160">Telemetri kaynaklanan bileşen - rol veya hizmete - tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-160">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="ecdfe-161">(Bunu paralel olarak birden çok sunucu işlemlerini veya makinelerde çalışan aynı roller ayıran cloud_RoleInstance ile aynı değildir.)</span><span class="sxs-lookup"><span data-stu-id="ecdfe-161">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="ecdfe-162">Portalda, filtre ya da bu özelliği kullanan telemetrinizi segmentlere.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-162">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="ecdfe-163">Bu örnekte, hataları dikey CRM API arka uç hatalarından çıkışı filtreleme ön uç web hizmetinden sadece bilgi göstermek için filtrelenir:</span><span class="sxs-lookup"><span data-stu-id="ecdfe-163">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![Bulut rolü adıyla kesimli ölçüm grafik](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="ecdfe-165">Bileşenleri arasında izleme işlemleri</span><span class="sxs-lookup"><span data-stu-id="ecdfe-165">Trace operations between components</span></span>

<span data-ttu-id="ecdfe-166">Başka bir tek bir işlem işlenirken yapılan çağrılar bir bileşenden izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecdfe-166">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![İşlem için telemetri Göster](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="ecdfe-168">Aracılığıyla bu işlem için telemetri bağıntılı listesine ön uç web sunucusu ve arka uç API'si üzerinden tıklatın:</span><span class="sxs-lookup"><span data-stu-id="ecdfe-168">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![Bileşenler genelinde arama](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="ecdfe-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ecdfe-170">Next steps</span></span>

* [<span data-ttu-id="ecdfe-171">Geliştirme, Test ve üretim ayrı telemetri</span><span class="sxs-lookup"><span data-stu-id="ecdfe-171">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
