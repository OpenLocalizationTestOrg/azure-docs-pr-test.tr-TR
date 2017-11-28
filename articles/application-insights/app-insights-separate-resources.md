---
title: "aaaSeparating telemetri geliştirme, test ve yayın Azure Application Insights'ta | Microsoft Docs"
description: "Geliştirme, test ve üretim Damgalar için doğrudan telemetri toodifferent kaynaklar."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="40ce7-103">Geliştirme, Test ve üretim telemetri ayırma</span><span class="sxs-lookup"><span data-stu-id="40ce7-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="40ce7-104">Bir web uygulaması sonraki sürümü hello geliştirirken hello yukarı toomix istemediğiniz [Application Insights](app-insights-overview.md) hello yeni sürümü ve hello önceden yayımlanan sürümü telemetrisinden.</span><span class="sxs-lookup"><span data-stu-id="40ce7-104">When you are developing hello next version of a web application, you don't want toomix up hello [Application Insights](app-insights-overview.md) telemetry from hello new version and hello already released version.</span></span> <span data-ttu-id="40ce7-105">tooavoid Karışıklığı önlemek için farklı geliştirme gönderme hello telemetrisinden tooseparate Application Insights kaynakları ayrı izleme anahtarı (ikeys) ile aşamaları.</span><span class="sxs-lookup"><span data-stu-id="40ce7-105">tooavoid confusion, send hello telemetry from different development stages tooseparate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="40ce7-106">toomake, bir sürüm olarak daha kolay toochange hello izleme anahtarını yararlı tooset hello ikey hello yapılandırma dosyasında yerine kodda olması bir aşamada tooanother taşır.</span><span class="sxs-lookup"><span data-stu-id="40ce7-106">toomake it easier toochange hello instrumentation key as a version moves from one stage tooanother, it can be useful tooset hello ikey in code instead of in hello configuration file.</span></span> 

<span data-ttu-id="40ce7-107">(Sisteminiz bir Azure bulut hizmeti ise var. [ayrı ikeys ayarlama başka bir yöntem](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="40ce7-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="40ce7-108">Kaynaklar ve izleme anahtarı hakkında</span><span class="sxs-lookup"><span data-stu-id="40ce7-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="40ce7-109">Web uygulamanız için Application Insights izleme işlevini ayarlama Application Insights oluşturduğunuzda *kaynak* Microsoft azure'da.</span><span class="sxs-lookup"><span data-stu-id="40ce7-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="40ce7-110">Bu kaynak hello sipariş toosee Azure portalında açın ve hello telemetriyi uygulamanızdan toplanan analiz.</span><span class="sxs-lookup"><span data-stu-id="40ce7-110">You open this resource in hello Azure portal in order toosee and analyze hello telemetry collected from your app.</span></span> <span data-ttu-id="40ce7-111">Merhaba kaynak tarafından tanımlanan bir *izleme anahtarını* (ikey).</span><span class="sxs-lookup"><span data-stu-id="40ce7-111">hello resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="40ce7-112">Merhaba yüklediğinizde Application Insights toomonitor uygulamanızı paketleme, burada toosend hello telemetri bilir şekilde, hello izleme anahtarı ile yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40ce7-112">When you install hello Application Insights package toomonitor your app, you configure it with hello instrumentation key, so that it knows where toosend hello telemetry.</span></span>

<span data-ttu-id="40ce7-113">Genellikle toouse ayrı kaynaklar ya da tek bir paylaşılan kaynağa farklı senaryolarda seçin:</span><span class="sxs-lookup"><span data-stu-id="40ce7-113">You typically choose toouse separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="40ce7-114">Farklı, bağımsız uygulamalar - her uygulama için ayrı kaynak ve ikey kullanın.</span><span class="sxs-lookup"><span data-stu-id="40ce7-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="40ce7-115">Birden çok bileşenleri ya da bir iş uygulaması - rolleri kullanmak bir [tek bir paylaşılan kaynak](app-insights-monitor-multi-role-apps.md) tüm bileşen uygulamaları hello için.</span><span class="sxs-lookup"><span data-stu-id="40ce7-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all hello component apps.</span></span> <span data-ttu-id="40ce7-116">Telemetri filtre veya hello cloud_RoleName özelliği tarafından ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="40ce7-116">Telemetry can be filtered or segmented by hello cloud_RoleName property.</span></span>
* <span data-ttu-id="40ce7-117">Geliştirme, Test ve yayın - ayrı kaynak ve ikey sürümlerini 'damga' ın hello veya üretim aşaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="40ce7-117">Development, Test, and Release - Use a separate resource and ikey for versions of hello system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="40ce7-118">A | B testi - tek bir kaynak kullanın.</span><span class="sxs-lookup"><span data-stu-id="40ce7-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="40ce7-119">TelemetryInitializer tooadd hello çeşitleri tanımlayan bir özellik toohello telemetri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="40ce7-119">Create a TelemetryInitializer tooadd a property toohello telemetry that identifies hello variants.</span></span>


## <span data-ttu-id="40ce7-120"><a name="dynamic-ikey"></a>Dinamik izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="40ce7-120"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>

<span data-ttu-id="40ce7-121">toomake kolaylaştırır toochange hello ikey hello kod olarak üretim aşamaları arasında taşır yerine kodda hello yapılandırma dosyasında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="40ce7-121">toomake it easier toochange hello ikey as hello code moves between stages of production, set it in code instead of in hello configuration file.</span></span>

<span data-ttu-id="40ce7-122">Başlangıç anahtarı başlatma yöntemini, bir ASP.NET hizmetinde global.aspx.cs gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40ce7-122">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="40ce7-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="40ce7-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="40ce7-124">Bu örnekte, hello web yapılandırma dosyası farklı sürümlerini hello ikeys hello farklı kaynaklar yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="40ce7-124">In this example, hello ikeys for hello different resources are placed in different versions of hello web configuration file.</span></span> <span data-ttu-id="40ce7-125">-Hello yayın komut dosyasının bir parçası yapabileceğiniz - takası hello web yapılandırma dosyasını hello hedef kaynak değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="40ce7-125">Swapping hello web configuration file - which you can do as part of hello release script - will swap hello target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="40ce7-126">Web sayfaları</span><span class="sxs-lookup"><span data-stu-id="40ce7-126">Web pages</span></span>
<span data-ttu-id="40ce7-127">Merhaba, uygulamanızın web sayfalarında de Hello iKey kullanıldığında [hello hızlı başlangıç dikey penceresinden aldığınız betik](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="40ce7-127">hello iKey is also used in your app's web pages, in hello [script that you got from hello quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="40ce7-128">Harfi harfine hello komut dosyasına kodlama yerine, hello sunucu durumundan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="40ce7-128">Instead of coding it literally into hello script, generate it from hello server state.</span></span> <span data-ttu-id="40ce7-129">Örneğin, bir ASP.NET uygulamasında:</span><span class="sxs-lookup"><span data-stu-id="40ce7-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="40ce7-130">*Razor JavaScript'te*</span><span class="sxs-lookup"><span data-stu-id="40ce7-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="40ce7-131">Ek Application Insights kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="40ce7-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="40ce7-132">tooseparate telemetri farklı Damgalar (dev/test/üretim) hello ya da farklı uygulama bileşenleri için aynı bileşen toocreate yeni bir Application Insights kaynağı sahip.</span><span class="sxs-lookup"><span data-stu-id="40ce7-132">tooseparate telemetry for different application components, or for different stamps (dev/test/production) of hello same component, then you'll have toocreate a new Application Insights resource.</span></span>

<span data-ttu-id="40ce7-133">Merhaba, [portal.azure.com](https://portal.azure.com), Application Insights kaynağı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40ce7-133">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="40ce7-135">**Uygulama türü** hello genel bakış dikey penceresinde ve hello özellikler kullanılabilir Görünenleri etkiler [ölçüm Gezgini](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="40ce7-135">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="40ce7-136">Uygulama, türünü görmüyorsanız, web sayfaları için hello web türlerinden birini seçin.</span><span class="sxs-lookup"><span data-stu-id="40ce7-136">If you don't see your type of app, choose one of hello web types for web pages.</span></span>
* <span data-ttu-id="40ce7-137">**Kaynak grubu** gibi özellikleri yönetmek için kullanışlı olan [erişim denetimi](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="40ce7-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="40ce7-138">Ayrı kaynak grupları, geliştirme, test ve üretim için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40ce7-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="40ce7-139">**Abonelik** ödeme hesabınız azure'da.</span><span class="sxs-lookup"><span data-stu-id="40ce7-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="40ce7-140">**Konum** burada biz verilerinizi tutmak olduğu.</span><span class="sxs-lookup"><span data-stu-id="40ce7-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="40ce7-141">Şu anda değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="40ce7-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="40ce7-142">**Toodashboard ekleme** kaynağınız için hızlı erişim kutucuğu, Azure giriş sayfasında koyar.</span><span class="sxs-lookup"><span data-stu-id="40ce7-142">**Add toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="40ce7-143">Merhaba kaynak oluşturma birkaç saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="40ce7-143">Creating hello resource takes a few seconds.</span></span> <span data-ttu-id="40ce7-144">Bu yapıldığında, bir uyarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="40ce7-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="40ce7-145">(Yazabileceğiniz bir [PowerShell Betiği](app-insights-powershell-script-create-resource.md) toocreate kaynak otomatik olarak.)</span><span class="sxs-lookup"><span data-stu-id="40ce7-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) toocreate a resource automatically.)</span></span>

### <a name="getting-hello-instrumentation-key"></a><span data-ttu-id="40ce7-146">Merhaba izleme anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="40ce7-146">Getting hello instrumentation key</span></span>
<span data-ttu-id="40ce7-147">Merhaba izleme anahtarı oluşturduğunuz hello kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="40ce7-147">hello instrumentation key identifies hello resource that you created.</span></span> 

![Essentials'ı tıklatın, hello izleme anahtarı, CTRL + C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="40ce7-149">Merhaba izleme anahtarı ihtiyacınız tüm hello kaynakları toowhich uygulamanızı verileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="40ce7-149">You need hello instrumentation keys of all hello resources toowhich your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="40ce7-150">Yapı numarası filtre</span><span class="sxs-lookup"><span data-stu-id="40ce7-150">Filter on build number</span></span>
<span data-ttu-id="40ce7-151">Uygulamanızı yeni bir sürümü yayımladığınızda, toobe mümkün tooseparate hello telemetri farklı yapılandırmalardan isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="40ce7-151">When you publish a new version of your app, you'll want toobe able tooseparate hello telemetry from different builds.</span></span>

<span data-ttu-id="40ce7-152">Filtre uygulayabilirsiniz şekilde hello uygulama Version özelliği ayarlayabilirsiniz [arama](app-insights-diagnostic-search.md) ve [ölçüm Gezgini](app-insights-metrics-explorer.md) sonuçları.</span><span class="sxs-lookup"><span data-stu-id="40ce7-152">You can set hello Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Bir özellik filtreleme](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="40ce7-154">Merhaba uygulama Version özelliği ayarlama birkaç farklı yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="40ce7-154">There are several different methods of setting hello Application Version property.</span></span>

* <span data-ttu-id="40ce7-155">Doğrudan ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="40ce7-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="40ce7-156">Bu satırda sarmalamak bir [telemetri Başlatıcı](app-insights-api-custom-events-metrics.md#defaults) TelemetryClient hepsinin tutarlı bir şekilde ayarlanan tooensure.</span><span class="sxs-lookup"><span data-stu-id="40ce7-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) tooensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="40ce7-157">[ASP.NET] Set hello sürümünde `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="40ce7-157">[ASP.NET] Set hello version in `BuildInfo.config`.</span></span> <span data-ttu-id="40ce7-158">Merhaba web modülü hello sürüm hello BuildLabel düğümünden yukarı seçer.</span><span class="sxs-lookup"><span data-stu-id="40ce7-158">hello web module will pick up hello version from hello BuildLabel node.</span></span> <span data-ttu-id="40ce7-159">Bu dosyayı projenize eklemek ve tooset hello her zaman Kopyala özelliği Çözüm Gezgini'nde unutmayın.</span><span class="sxs-lookup"><span data-stu-id="40ce7-159">Include this file in your project and remember tooset hello Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="40ce7-160">[ASP.NET] BuildInfo.config Msbuild'de otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="40ce7-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="40ce7-161">toodo Bu, birkaç satırları tooyour ekleme `.csproj` dosyası:</span><span class="sxs-lookup"><span data-stu-id="40ce7-161">toodo this, add a few lines tooyour `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="40ce7-162">Bu adlı bir dosya oluşturur *yourProjectName*. BuildInfo.config. hello yayımlama işlemi tooBuildInfo.config yeniden adlandırır.</span><span class="sxs-lookup"><span data-stu-id="40ce7-162">This generates a file called *yourProjectName*.BuildInfo.config. hello Publish process renames it tooBuildInfo.config.</span></span>

    <span data-ttu-id="40ce7-163">Visual Studio ile derlerken hello yapı etiketi yer tutucu (AutoGen_...) içerir.</span><span class="sxs-lookup"><span data-stu-id="40ce7-163">hello build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="40ce7-164">Ancak MSBuild ile yapılandırıldığında hello doğru sürüm numarasıyla doldurulur.</span><span class="sxs-lookup"><span data-stu-id="40ce7-164">But when built with MSBuild, it is populated with hello correct version number.</span></span>

    <span data-ttu-id="40ce7-165">kümesi hello sürümünü tooallow MSBuild toogenerate sürüm numaralarını, ister `1.0.*` AssemblyReference.cs içinde</span><span class="sxs-lookup"><span data-stu-id="40ce7-165">tooallow MSBuild toogenerate version numbers, set hello version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="40ce7-166">Sürüm ve sürüm izleme</span><span class="sxs-lookup"><span data-stu-id="40ce7-166">Version and release tracking</span></span>
<span data-ttu-id="40ce7-167">tootrack hello uygulama sürümü, emin olun `buildinfo.config` Microsoft Build Engine işlem tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="40ce7-167">tootrack hello application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="40ce7-168">.csproj dosyanızda şunları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40ce7-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="40ce7-169">Merhaba yapı bilgisi mevcut olduğunda hello Application Insights web modülü otomatik olarak ekler **uygulama sürümü** telemetri özellik tooevery öğesi olarak.</span><span class="sxs-lookup"><span data-stu-id="40ce7-169">When it has hello build info, hello Application Insights web module automatically adds **Application version** as a property tooevery item of telemetry.</span></span> <span data-ttu-id="40ce7-170">Böylece toofilter sürümü tarafından gerçekleştirdiğinizde [tanılama aramaları](app-insights-diagnostic-search.md), veya ne zaman, [ölçümleri keşfedin](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="40ce7-170">That allows you toofilter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="40ce7-171">Ancak, yalnızca Microsoft Build Engine, hello geliştirici tarafından değil, Visual Studio'da derleme hello hello derleme sürüm numarası oluşturan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="40ce7-171">However, notice that hello build version number is generated only by hello Microsoft Build Engine, not by hello developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="40ce7-172">Sürüm ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="40ce7-172">Release annotations</span></span>
<span data-ttu-id="40ce7-173">Visual Studio Team Services kullanıyorsanız, şunları yapabilirsiniz [bir ek açıklama işaretçisi almak](app-insights-annotations.md) yeni bir sürüm yayın her tooyour grafikler eklendi.</span><span class="sxs-lookup"><span data-stu-id="40ce7-173">If you use Visual Studio Team Services, you can [get an annotation marker](app-insights-annotations.md) added tooyour charts whenever you release a new version.</span></span> <span data-ttu-id="40ce7-174">Görüntü aşağıdaki Merhaba, bu işaret nasıl göründüğünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="40ce7-174">hello following image shows how this marker appears.</span></span>

![Bir grafikteki örnek sürüm ek açıklamasının ekran görüntüsü](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="40ce7-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40ce7-176">Next steps</span></span>

* [<span data-ttu-id="40ce7-177">Birden çok rol için paylaşılan kaynakları</span><span class="sxs-lookup"><span data-stu-id="40ce7-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="40ce7-178">Telemetri Başlatıcı toodistinguish A oluşturun | B çeşitleri</span><span class="sxs-lookup"><span data-stu-id="40ce7-178">Create a Telemetry Initializer toodistinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
