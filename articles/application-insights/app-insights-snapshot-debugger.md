---
title: ".NET uygulamaları için uygulama Öngörüler anlık görüntü hata ayıklayıcı aaaAzure | Microsoft Docs"
description: "Hata ayıklama anlık görüntüleri otomatik olarak üretim .NET uygulamaları özel durumlar, toplanan"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="91562-103">Anlık görüntü özel durumları .NET uygulamalarında hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="91562-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="91562-104">Özel durum oluştuğunda, hata ayıklama anlık görüntü canlı web uygulamanızı otomatik olarak toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91562-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="91562-105">değişkenleri hello şu anda hello özel durum sırasında oluşturuldu ve Hello anlık görüntü kaynak kodu hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="91562-105">hello snapshot shows hello state of source code and variables at hello moment hello exception was thrown.</span></span> <span data-ttu-id="91562-106">Başlangıç anlık görüntü hata ayıklayıcısı (Önizleme) içinde [Azure Application Insights](app-insights-overview.md) özel durum, web uygulamanızın telemetrisinden izler.</span><span class="sxs-lookup"><span data-stu-id="91562-106">hello Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="91562-107">Böylece toodiagnose sorunları üretimde gereksinim hello bilgileri sahip anlık görüntüleri, üst atma özel durumlar toplar.</span><span class="sxs-lookup"><span data-stu-id="91562-107">It collects snapshots on your top-throwing exceptions so that you have hello information you need toodiagnose issues in production.</span></span> <span data-ttu-id="91562-108">Merhaba dahil [anlık görüntü Toplayıcı NuGet paketi](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanızda ve isteğe bağlı olarak koleksiyon parametrelerinde yapılandırma [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md). Anlık görüntüler görünmez [özel durumları](app-insights-asp-net-exceptions.md) hello Application Insights portalında.</span><span class="sxs-lookup"><span data-stu-id="91562-108">Include hello [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

<span data-ttu-id="91562-109">Hata ayıklama anlık görüntüleri hello portal toosee hello çağrı yığınında görüntüleyebilir ve her çağrı yığını çerçevesi en değişkenlerle inceleyin.</span><span class="sxs-lookup"><span data-stu-id="91562-109">You can view debug snapshots in hello portal toosee hello call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="91562-110">Kaynak kodu, Visual Studio 2017 kuruluş tarafından sahip açık anlık görüntüleri ile daha güçlü bir hata ayıklama deneyimini tooget [Visual Studio için başlangıç anlık görüntü hata ayıklayıcısı uzantısı yükleme](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="91562-110">tooget a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="91562-111">Anlık görüntü koleksiyonu için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="91562-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="91562-112">.NET framework ve ASP.NET uygulamaları .NET Framework 4.5 veya sonraki sürümlerini çalıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="91562-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="91562-113">Windows üzerinde çalışan .NET core 2.0 ve ASP.NET Core 2.0 uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="91562-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="91562-114">ASP.NET uygulamaları için anlık görüntü koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91562-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="91562-115">[Application Insights web uygulamanızda etkinleştirmek](app-insights-asp-net.md), henüz yapmadınız.</span><span class="sxs-lookup"><span data-stu-id="91562-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="91562-116">Merhaba dahil [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="91562-116">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="91562-117">Paket çok eklenen hello hello varsayılan seçenekleri gözden geçir[Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="91562-117">Review hello default options that hello package added too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="91562-118">Anlık görüntüler, bildirilen tooApplication Öngörüler yalnızca özel durumları toplanır.</span><span class="sxs-lookup"><span data-stu-id="91562-118">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="91562-119">Bazı durumlarda (örneğin, daha eski sürümleri hello .NET platformu), çok gerekebilir[özel durum koleksiyonunu yapılandırma](app-insights-asp-net-exceptions.md#exceptions) toosee istisnalar hello portalında anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91562-119">In some cases (for example, older versions of hello .NET platform), you might need too[configure exception collection](app-insights-asp-net-exceptions.md#exceptions) toosee exceptions with snapshots in hello portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="91562-120">ASP.NET Core 2.0 uygulamaları için anlık görüntü koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91562-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="91562-121">[Application Insights ASP.NET Core web uygulamanızda etkinleştirmek](app-insights-asp-net-core.md), henüz yapmadınız.</span><span class="sxs-lookup"><span data-stu-id="91562-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="91562-122">Merhaba dahil [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="91562-122">Include hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="91562-123">Merhaba değiştirme `ConfigureServices` uygulamanızın yönteminde `Startup` tooadd hello anlık görüntü toplayıcının telemetri işlemci sınıfı.</span><span class="sxs-lookup"><span data-stu-id="91562-123">Modify hello `ConfigureServices` method in your application's `Startup` class tooadd hello Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="91562-124">Merhaba kodu eklemeniz gerekir hello başvurulan hello Microsoft.ApplicationInsights.ASPNETCore NuGet paketi sürümüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="91562-124">hello code you should add depends on hello referenced version of hello Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="91562-125">Microsoft.ApplicationInsights.AspNetCore 2.1.0 ekleyin:</span><span class="sxs-lookup"><span data-stu-id="91562-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="91562-126">Microsoft.ApplicationInsights.AspNetCore 2.1.1 ekleyin:</span><span class="sxs-lookup"><span data-stu-id="91562-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="91562-127">Diğer .NET uygulamaları için anlık görüntü koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="91562-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="91562-128">Uygulamanızı Application Insights ile zaten izlenmemektedir, başlayın [Application Insights ve ayar hello izleme anahtarını etkinleştirme](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="91562-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting hello instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="91562-129">Merhaba eklemek [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="91562-129">Add hello [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="91562-130">Anlık görüntüler, bildirilen tooApplication Öngörüler yalnızca özel durumları toplanır.</span><span class="sxs-lookup"><span data-stu-id="91562-130">Snapshots are collected only on exceptions that are reported tooApplication Insights.</span></span> <span data-ttu-id="91562-131">Kod tooreport toomodify gerekebilir bunları.</span><span class="sxs-lookup"><span data-stu-id="91562-131">You may need toomodify your code tooreport them.</span></span> <span data-ttu-id="91562-132">Uygulamanızı hello yapısını hello özel durum kodu işleme bağlıdır, ancak bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="91562-132">hello exception handling code depends on hello structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="91562-133">İzinleri</span><span class="sxs-lookup"><span data-stu-id="91562-133">Grant permissions</span></span>

<span data-ttu-id="91562-134">Hello Azure abonelik sahipleri anlık görüntüleri inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91562-134">Owners of hello Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="91562-135">Diğer kullanıcıların bir sahibi tarafından izin verilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="91562-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="91562-136">toogrant izni, Ata hello `Application Insights Snapshot Debugger` anlık görüntüleri araştırmasını rol toousers.</span><span class="sxs-lookup"><span data-stu-id="91562-136">toogrant permission, assign hello `Application Insights Snapshot Debugger` role toousers who will inspect snapshots.</span></span> <span data-ttu-id="91562-137">Bu rol, tooindividual kullanıcıları veya grupları hello hedef Application Insights kaynağı için abonelik sahipleri tarafından veya kaynak grubu ya da abonelik atanabilir.</span><span class="sxs-lookup"><span data-stu-id="91562-137">This role can be assigned tooindividual users or groups by subscription owners for hello target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="91562-138">Merhaba erişim denetimi (IAM) dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="91562-138">Open hello Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="91562-139">Merhaba + Ekle düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="91562-139">Click hello +Add button.</span></span>
1. <span data-ttu-id="91562-140">Uygulama Öngörüler anlık görüntü hata ayıklayıcı hello rolleri aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="91562-140">Select Application Insights Snapshot Debugger from hello Roles drop-down list.</span></span>
1. <span data-ttu-id="91562-141">Arayın ve hello kullanıcı tooadd için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="91562-141">Search for and enter a name for hello user tooadd.</span></span>
1. <span data-ttu-id="91562-142">Merhaba Kaydet düğmesine tooadd hello kullanıcı toohello rolüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="91562-142">Click hello Save button tooadd hello user toohello role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="91562-143">Anlık görüntüler olası değişken ve parametre değerlerini kişisel ve diğer hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="91562-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-hello-application-insights-portal"></a><span data-ttu-id="91562-144">Anlık görüntüler hello Application Insights portalında hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="91562-144">Debug snapshots in hello Application Insights portal</span></span>

<span data-ttu-id="91562-145">Belirli bir özel durum ya da bir sorun kimliği için bir anlık görüntü kullanılabiliyorsa, bir **açık hata ayıklama anlık görüntü** düğmesinin üzerinde hello [özel durum](app-insights-asp-net-exceptions.md) hello Application Insights portalında.</span><span class="sxs-lookup"><span data-stu-id="91562-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on hello [exception](app-insights-asp-net-exceptions.md) in hello Application Insights portal.</span></span>

![Özel durum açık hata ayıklama anlık görüntü düğmesine](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="91562-147">Hello hata ayıklama anlık Görünüm'de, çağrı yığını ve değişkenleri bölmesine bakın.</span><span class="sxs-lookup"><span data-stu-id="91562-147">In hello Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="91562-148">Seçtiğinizde hello çağrı yığını Bölmesi'nde hello çağrının çerçeveler yığın, yerel değişkenleri görüntüleyebilir ve bu işlev parametrelerini hello değişkenleri bölmesinde çağırın.</span><span class="sxs-lookup"><span data-stu-id="91562-148">When you select frames of hello call stack in hello call stack pane, you can view local variables and parameters for that function call in hello variables pane.</span></span>

![Görünüm hata ayıklama anlık hello portalı](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="91562-150">Varsayılan olarak görüntülenebilir olmadıkları ve anlık görüntüleri hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="91562-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="91562-151">tooview anlık görüntüler, hello olmalıdır `Application Insights Snapshot Debugger` atanan rolü tooyou.</span><span class="sxs-lookup"><span data-stu-id="91562-151">tooview snapshots, you must have hello `Application Insights Snapshot Debugger` role assigned tooyou.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="91562-152">Visual Studio 2017 Enterprise sahip anlık görüntüleri hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="91562-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="91562-153">Merhaba tıklatın **karşıdan anlık görüntü** düğmesini toodownload bir `.diagsession` Visual Studio 2017 kuruluş tarafından açılabilir dosya.</span><span class="sxs-lookup"><span data-stu-id="91562-153">Click hello **Download Snapshot** button toodownload a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="91562-154">tooopen hello `.diagsession` dosya, şunları yapmalısınız ilk [hello anlık görüntü hata ayıklayıcısı uzantısı için Visual Studio yükleyip](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="91562-154">tooopen hello `.diagsession` file, you must first [download and install hello Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="91562-155">Başlangıç anlık görüntü dosyasını açın sonra Visual Studio'da hello mini döküm hata ayıklama sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="91562-155">After you open hello snapshot file, hello Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="91562-156">Tıklatın **yönetilen kod hata ayıklama** hello anlık görüntü hata ayıklama toostart.</span><span class="sxs-lookup"><span data-stu-id="91562-156">Click **Debug Managed Code** toostart debugging hello snapshot.</span></span> <span data-ttu-id="91562-157">Başlangıç anlık görüntü toohello kod satırı, böylece hello işleminin geçerli durumunu hello ayıklayabilirsiniz burada hello özel durum oluştu açar.</span><span class="sxs-lookup"><span data-stu-id="91562-157">hello snapshot opens toohello line of code where hello exception was thrown so that you can debug hello current state of hello process.</span></span>

    ![Visual Studio'da hata ayıklama anlık görünümü](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="91562-159">Merhaba indirilen anlık görüntü web uygulaması sunucunuzda bulundu herhangi sembol dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="91562-159">hello downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="91562-160">Kaynak kodu ile gerekli tooassociate anlık görüntü verilerini bu simge dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="91562-160">These symbol files are required tooassociate snapshot data with source code.</span></span> <span data-ttu-id="91562-161">Web uygulamalarınızı yayımladığınızda, uygulama hizmeti uygulamalarınız için emin tooenable simgesi dağıtımı yapın.</span><span class="sxs-lookup"><span data-stu-id="91562-161">For App Service apps, make sure tooenable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="91562-162">Anlık görüntüler nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="91562-162">How snapshots work</span></span>

<span data-ttu-id="91562-163">Uygulamanız başladığında, ayrı anlık görüntü yükleyici işlemi, uygulamanız için anlık görüntü istekleri izleyen oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="91562-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="91562-164">Bir anlık görüntü istendiğinde işlem çalışan hello bir gölge kopyasını yaklaşık 10 too20 dakika içinde yapılır.</span><span class="sxs-lookup"><span data-stu-id="91562-164">When a snapshot is requested, a shadow copy of hello running process is made in about 10 too20 minutes.</span></span> <span data-ttu-id="91562-165">Merhaba gölge işleminin ardından analiz ve bir anlık görüntü toorun hello ana işlem devam ederken oluşturulur ve trafik toousers hizmet.</span><span class="sxs-lookup"><span data-stu-id="91562-165">hello shadow process is then analyzed, and a snapshot is created while hello main process continues toorun and serve traffic toousers.</span></span> <span data-ttu-id="91562-166">tüm ilgili simge (.pdb) dosyalar ile birlikte yüklenen tooApplication Öngörüler tooview gerekirse hello anlık görüntüsüdür hello anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="91562-166">hello snapshot is then uploaded tooApplication Insights along with any relevant symbol (.pdb) files that are needed tooview hello snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="91562-167">Geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="91562-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="91562-168">Simgeler yayımlama</span><span class="sxs-lookup"><span data-stu-id="91562-168">Publish symbols</span></span>
<span data-ttu-id="91562-169">Başlangıç anlık görüntü hata ayıklayıcı simge dosyaları hello üretim sunucusu toodecode değişkenleri ve tooprovide Visual Studio'da hata ayıklama deneyimini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="91562-169">hello Snapshot Debugger requires symbol files on hello production server toodecode variables and tooprovide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="91562-170">tooApp hizmet yayımladığında hello 15.2 sürümü Visual Studio 2017, sürüm derlemeleri simgelerini varsayılan olarak yayımlar.</span><span class="sxs-lookup"><span data-stu-id="91562-170">hello 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes tooApp Service.</span></span> <span data-ttu-id="91562-171">Önceki sürümlerde, tooadd hello aşağıdakiler satır tooyour yayımlama profili `.pubxml` simgeleri yayın modunda yayımlanan dosyasını:</span><span class="sxs-lookup"><span data-stu-id="91562-171">In prior versions, you need tooadd hello following line tooyour publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="91562-172">Azure işlem ve diğer türleri için hello simge dosyaları hello olduğundan emin olun hello ana uygulama .dll aynı klasörü (genellikle `wwwroot/bin`) veya hello geçerli yolda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="91562-172">For Azure Compute and other types, ensure that hello symbol files are in hello same folder of hello main application .dll (typically, `wwwroot/bin`) or are available on hello current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="91562-173">En iyi duruma getirilmiş derlemeleri</span><span class="sxs-lookup"><span data-stu-id="91562-173">Optimized builds</span></span>
<span data-ttu-id="91562-174">Bazı durumlarda, yerel değişkenleri hello oluşturma işlemi sırasında uygulanan en iyi duruma getirme nedeniyle yayın derlemelerde görüntülenemiyor.</span><span class="sxs-lookup"><span data-stu-id="91562-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during hello build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="91562-175">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="91562-175">Troubleshooting</span></span>

<span data-ttu-id="91562-176">Bu ipuçları hello anlık görüntü hata ayıklayıcı sorunlarını gidermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="91562-176">These tips help you troubleshoot problems with hello Snapshot Debugger.</span></span>

### <a name="verify-hello-instrumentation-key"></a><span data-ttu-id="91562-177">Merhaba izleme anahtarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="91562-177">Verify hello instrumentation key</span></span>

<span data-ttu-id="91562-178">Yayımlanan uygulamanızda hello doğru izleme anahtarını kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="91562-178">Make sure that you're using hello correct instrumentation key in your published application.</span></span> <span data-ttu-id="91562-179">Genellikle, Application Insights hello izleme anahtarını hello Applicationınsights.config dosyasını okur.</span><span class="sxs-lookup"><span data-stu-id="91562-179">Usually, Application Insights reads hello instrumentation key from hello ApplicationInsights.config file.</span></span> <span data-ttu-id="91562-180">Hello değeri olan Merhaba, aynı hello Portalı'nda bkz hello Application Insights kaynağı için hello araçları anahtar olarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="91562-180">Verify that hello value is hello same as hello instrumentation key for hello Application Insights resource that you see in hello portal.</span></span>

### <a name="check-hello-uploader-logs"></a><span data-ttu-id="91562-181">Merhaba yükleyici günlüklerini kontrol edin</span><span class="sxs-lookup"><span data-stu-id="91562-181">Check hello uploader logs</span></span>

<span data-ttu-id="91562-182">Bir anlık görüntü oluşturulduktan sonra bir mini döküm dosyası (.dmp) disk üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="91562-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="91562-183">Ayrı yükleyici işlem, mini döküm dosyası alır ve bunu, tooApplication Öngörüler anlık görüntü hata ayıklayıcı depolama gibi ilişkili tüm pdb birlikte yükler.</span><span class="sxs-lookup"><span data-stu-id="91562-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, tooApplication Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="91562-184">Merhaba mini döküm başarıyla yükledi sonra diskten silinir.</span><span class="sxs-lookup"><span data-stu-id="91562-184">After hello minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="91562-185">Merhaba mini döküm yükleyici için Hello günlük dosyaları diskte korunur.</span><span class="sxs-lookup"><span data-stu-id="91562-185">hello log files for hello minidump uploader are retained on disk.</span></span> <span data-ttu-id="91562-186">Bir uygulama hizmeti ortamı'nda, bu günlükler bulabilirsiniz `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="91562-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="91562-187">Kullanım hello Kudu yönetim sitesi için uygulama hizmeti toofind bu günlük dosyaları.</span><span class="sxs-lookup"><span data-stu-id="91562-187">Use hello Kudu management site for App Service toofind these log files.</span></span>

1. <span data-ttu-id="91562-188">Uygulama hizmeti uygulamanızı hello Azure portalını açın.</span><span class="sxs-lookup"><span data-stu-id="91562-188">Open your App Service application in hello Azure portal.</span></span>

2. <span data-ttu-id="91562-189">Select hello **Gelişmiş Araçlar** dikey veya arama **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="91562-189">Select hello **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="91562-190">tıklatın **Git**.</span><span class="sxs-lookup"><span data-stu-id="91562-190">Click **Go**.</span></span>
4. <span data-ttu-id="91562-191">Merhaba, **hata ayıklama konsoluna** aşağı açılan liste kutusunda **CMD**.</span><span class="sxs-lookup"><span data-stu-id="91562-191">In hello **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="91562-192">Tıklatın **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="91562-192">Click **LogFiles**.</span></span>

<span data-ttu-id="91562-193">İle başlayan bir ada sahip en az bir dosya görmelisiniz `Uploader_` ve `.log` uzantısı.</span><span class="sxs-lookup"><span data-stu-id="91562-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="91562-194">Tüm günlük dosyalarını Hello uygun simgeye toodownload tıklatın veya bir tarayıcıda açın.</span><span class="sxs-lookup"><span data-stu-id="91562-194">Click hello appropriate icon toodownload any log files or open them in a browser.</span></span>
<span data-ttu-id="91562-195">Merhaba dosya adı hello makine adını içerir.</span><span class="sxs-lookup"><span data-stu-id="91562-195">hello file name includes hello machine name.</span></span> <span data-ttu-id="91562-196">Uygulama hizmeti örneğinizi birden fazla makine üzerinde barındırılıyorsa, her makine için farklı günlük dosyaları vardır.</span><span class="sxs-lookup"><span data-stu-id="91562-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="91562-197">Merhaba yükleyici yeni bir mini döküm dosyası algıladığında hello günlük dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="91562-197">When hello uploader detects a new minidump file, it is recorded in hello log file.</span></span> <span data-ttu-id="91562-198">Başarılı bir karşıya yükleme bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="91562-198">Here's an example of a successful upload:</span></span>

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

<span data-ttu-id="91562-199">Merhaba izleme anahtarını Hello önceki örnekte olduğu `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="91562-199">In hello previous example, hello instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="91562-200">Bu değer, uygulamanız için hello izleme anahtarını eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="91562-200">This value should match hello instrumentation key for your application.</span></span>
<span data-ttu-id="91562-201">Merhaba mini döküm hello Kimliğine sahip bir anlık görüntüsü ile ilişkili `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="91562-201">hello minidump is associated with a snapshot with hello ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="91562-202">Bu kimliği kullanabilirsiniz sonraki toolocate hello ilişkili uygulama Öngörüler analytics'te özel durum telemetrisi.</span><span class="sxs-lookup"><span data-stu-id="91562-202">You can use this ID later toolocate hello associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="91562-203">Merhaba Yükleyici her 15 dakikada hakkında yeni pdb tarar.</span><span class="sxs-lookup"><span data-stu-id="91562-203">hello uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="91562-204">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="91562-204">Here's an example:</span></span>

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

<span data-ttu-id="91562-205">Uygulamalar için _değil_ App Service içinde barındırılan, hello yükleyici hello günlüklerin hello Mini dökümler aynı klasöre: `%TEMP%\Dumps\<ikey>` (burada `<ikey>` araçları anahtarınız).</span><span class="sxs-lookup"><span data-stu-id="91562-205">For applications that are _not_ hosted in App Service, hello uploader logs are in hello same folder as hello minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a><span data-ttu-id="91562-206">Anlık görüntü toofind istisnalar kullanım Application Insights arama</span><span class="sxs-lookup"><span data-stu-id="91562-206">Use Application Insights search toofind exceptions with snapshots</span></span>

<span data-ttu-id="91562-207">Bir anlık görüntü oluşturulduğunda, özel durum atma hello bir anlık görüntü kimliği ile etiketlenir</span><span class="sxs-lookup"><span data-stu-id="91562-207">When a snapshot is created, hello throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="91562-208">Merhaba özel durum telemetrisi bildirilen tooApplication Öngörüler olduğunda, bu anlık görüntü kimliği bir özel özellik olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="91562-208">When hello exception telemetry is reported tooApplication Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="91562-209">Merhaba Ara dikey Application Insights'ta kullanarak, tüm telemetri hello ile bulabilirsiniz `ai.snapshot.id` özel özellik.</span><span class="sxs-lookup"><span data-stu-id="91562-209">Using hello Search blade in Application Insights, you can find all telemetry with hello `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="91562-210">Tooyour Application Insights kaynağını hello Azure portalına göz atın.</span><span class="sxs-lookup"><span data-stu-id="91562-210">Browse tooyour Application Insights resource in hello Azure portal.</span></span>
2. <span data-ttu-id="91562-211">Tıklatın **arama**.</span><span class="sxs-lookup"><span data-stu-id="91562-211">Click **Search**.</span></span>
3. <span data-ttu-id="91562-212">Tür `ai.snapshot.id` arama metin kutusuna hello ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="91562-212">Type `ai.snapshot.id` in hello Search text box and press Enter.</span></span>

![Bir anlık görüntü kimliği hello portalındaki telemetriyle arayın](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="91562-214">Bu arama sonuç döndürürse, hiç anlık görüntü uygulamanıza hello seçili zaman aralığı için raporlanan tooApplication Insights yoktu.</span><span class="sxs-lookup"><span data-stu-id="91562-214">If this search returns no results, then no snapshots were reported tooApplication Insights for your application in hello selected time range.</span></span>

<span data-ttu-id="91562-215">Merhaba yükleyici günlükleri, belirli bir anlık görüntüye Kimliğinden toosearch bu kimliği hello arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="91562-215">toosearch for a specific snapshot ID from hello Uploader logs, type that ID in hello Search box.</span></span> <span data-ttu-id="91562-216">Karşıya yüklenen bildiğiniz bir anlık görüntü için telemetri bulamazsanız, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="91562-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="91562-217">Merhaba sağ Application Insights kaynağı hello izleme anahtarını doğrulayarak arıyorsanız denetleyin.</span><span class="sxs-lookup"><span data-stu-id="91562-217">Double-check that you're looking at hello right Application Insights resource by verifying hello instrumentation key.</span></span>

2. <span data-ttu-id="91562-218">Merhaba zaman damgası hello yükleyici günlüğündeki kullanarak, bu zaman aralığı hello arama toocover hello zaman aralığı filtresi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="91562-218">Using hello timestamp from hello Uploader log, adjust hello Time Range filter of hello search toocover that time range.</span></span>

<span data-ttu-id="91562-219">Bu anlık görüntü Kimliğine sahip bir özel durum hala göremiyorsanız hello özel durum telemetrisi bildirilen tooApplication Öngörüler değildi.</span><span class="sxs-lookup"><span data-stu-id="91562-219">If you still don't see an exception with that snapshot ID, then hello exception telemetry wasn't reported tooApplication Insights.</span></span> <span data-ttu-id="91562-220">Bu durum, hello anlık görüntü sürdü sonra uygulamanızın kilitlendi, ancak hello özel durum telemetrisi bildirilen önce gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="91562-220">This situation can happen if your application crashed after it took hello snapshot but before it reported hello exception telemetry.</span></span> <span data-ttu-id="91562-221">Bu durumda, uygulama hizmeti günlüklerini altında hello denetleyin `Diagnose and solve problems` olsaydı beklenmeyen toosee yeniden başlatır veya işlenmeyen özel durum.</span><span class="sxs-lookup"><span data-stu-id="91562-221">In this case, check hello App Service logs under `Diagnose and solve problems` toosee if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91562-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91562-222">Next steps</span></span>

* <span data-ttu-id="91562-223">[Kodunuzda snappoints ayarlamak](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) için bir özel durum bekleniyor olmadan tooget anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="91562-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="91562-224">[Özel durumlar, web uygulamalarında tanılama](app-insights-asp-net-exceptions.md) açıklar nasıl toomake daha fazla özel durumları görünür tooApplication Öngörüler.</span><span class="sxs-lookup"><span data-stu-id="91562-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how toomake more exceptions visible tooApplication Insights.</span></span> 
* <span data-ttu-id="91562-225">[Akıllı algılama](app-insights-proactive-diagnostics.md) performans anormalliklerini otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="91562-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
