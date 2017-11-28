---
title: "Azure Application Insights .NET uygulamaları için hata ayıklayıcı anlık görüntü | Microsoft Docs"
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
ms.openlocfilehash: 56eba2ff7af228b3c44354ad43b384288b4e1972
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="f43f9-103">Anlık görüntü özel durumları .NET uygulamalarında hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f43f9-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="f43f9-104">Özel durum oluştuğunda, hata ayıklama anlık görüntü canlı web uygulamanızı otomatik olarak toplayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f43f9-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="f43f9-105">Anlık görüntü özel durumu şu anda kaynak kodu ve değişkenleri durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="f43f9-106">Anlık görüntü ayıklayıcıda (Önizleme) [Azure Application Insights](app-insights-overview.md) özel durum, web uygulamanızın telemetrisinden izler.</span><span class="sxs-lookup"><span data-stu-id="f43f9-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="f43f9-107">Böylece üretim sorunları tanılamak için gereken bilgileri sahip anlık görüntüleri, üst atma özel durumlarını toplar.</span><span class="sxs-lookup"><span data-stu-id="f43f9-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="f43f9-108">Dahil [anlık görüntü Toplayıcı NuGet paketi](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanızda ve isteğe bağlı olarak koleksiyon parametrelerinde yapılandırma [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md). Anlık görüntüler görünmez [özel durumları](app-insights-asp-net-exceptions.md) Application Insights portalında.</span><span class="sxs-lookup"><span data-stu-id="f43f9-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="f43f9-109">Yığın ve her çağrı yığını çerçevesi en değişkenlerle incelemek çağrı görmek için Portalı'nda hata ayıklama anlık görüntüleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f43f9-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="f43f9-110">Kaynak kodu ile daha güçlü bir hata ayıklama deneyimini almak için anlık görüntüleri olan açık Visual Studio 2017 kuruluş tarafından [Visual Studio için anlık görüntü hata ayıklayıcısı uzantısı yükleme](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="f43f9-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

<span data-ttu-id="f43f9-111">Anlık görüntü koleksiyonu için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="f43f9-111">Snapshot collection is available for:</span></span>
* <span data-ttu-id="f43f9-112">.NET framework ve ASP.NET uygulamaları .NET Framework 4.5 veya sonraki sürümlerini çalıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="f43f9-112">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="f43f9-113">Windows üzerinde çalışan .NET core 2.0 ve ASP.NET Core 2.0 uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="f43f9-113">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="f43f9-114">ASP.NET uygulamaları için anlık görüntü koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f43f9-114">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="f43f9-115">[Application Insights web uygulamanızda etkinleştirmek](app-insights-asp-net.md), henüz yapmadınız.</span><span class="sxs-lookup"><span data-stu-id="f43f9-115">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="f43f9-116">Dahil [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="f43f9-116">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span> 

3. <span data-ttu-id="f43f9-117">Pakete eklenen varsayılan seçenekleri gözden [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="f43f9-117">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="f43f9-118">Anlık görüntüler için Application Insights bildirilen özel durum toplanır.</span><span class="sxs-lookup"><span data-stu-id="f43f9-118">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="f43f9-119">Bazı durumlarda (örneğin, daha eski sürümlerini .NET platformu) için gereksinim duyabileceğiniz [özel durum koleksiyonunu yapılandırma](app-insights-asp-net-exceptions.md#exceptions) portalında anlık görüntüler içeren özel durumları görmek için.</span><span class="sxs-lookup"><span data-stu-id="f43f9-119">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="f43f9-120">ASP.NET Core 2.0 uygulamaları için anlık görüntü koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f43f9-120">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="f43f9-121">[Application Insights ASP.NET Core web uygulamanızda etkinleştirmek](app-insights-asp-net-core.md), henüz yapmadınız.</span><span class="sxs-lookup"><span data-stu-id="f43f9-121">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="f43f9-122">Dahil [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="f43f9-122">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="f43f9-123">Değiştirme `ConfigureServices` uygulamanızın yönteminde `Startup` sınıfı anlık görüntü toplayıcının telemetri işlemci ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f43f9-123">Modify the `ConfigureServices` method in your application's `Startup` class to add the Snapshot Collector's telemetry processor.</span></span> <span data-ttu-id="f43f9-124">Eklemeniz gereken kod Microsoft.ApplicationInsights.ASPNETCore NuGet paketi başvurulan sürümüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f43f9-124">The code you should add depends on the referenced version of the Microsoft.ApplicationInsights.ASPNETCore NuGet package.</span></span>

   <span data-ttu-id="f43f9-125">Microsoft.ApplicationInsights.AspNetCore 2.1.0 ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f43f9-125">For Microsoft.ApplicationInsights.AspNetCore 2.1.0 add:</span></span>
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   <span data-ttu-id="f43f9-126">Microsoft.ApplicationInsights.AspNetCore 2.1.1 ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f43f9-126">For Microsoft.ApplicationInsights.AspNetCore 2.1.1 add:</span></span>
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

       // This method is called by the runtime. Use it to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="f43f9-127">Diğer .NET uygulamaları için anlık görüntü koleksiyonunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f43f9-127">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="f43f9-128">Uygulamanızı Application Insights ile zaten izlenmemektedir, başlayın [Application Insights etkinleştirme ve izleme anahtarı ayarını](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="f43f9-128">If your application is not already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="f43f9-129">Ekleme [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) uygulamanıza NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="f43f9-129">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="f43f9-130">Anlık görüntüler için Application Insights bildirilen özel durum toplanır.</span><span class="sxs-lookup"><span data-stu-id="f43f9-130">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="f43f9-131">Bunları raporlamak için kodunuzu değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-131">You may need to modify your code to report them.</span></span> <span data-ttu-id="f43f9-132">Özel durum işleme kodunu yapısını uygulamanızın bağlıdır, ancak bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f43f9-132">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a><span data-ttu-id="f43f9-133">İzinleri</span><span class="sxs-lookup"><span data-stu-id="f43f9-133">Grant permissions</span></span>

<span data-ttu-id="f43f9-134">Azure abonelik sahipleri anlık görüntüleri inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f43f9-134">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="f43f9-135">Diğer kullanıcıların bir sahibi tarafından izin verilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-135">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="f43f9-136">İzin vermek için Ata `Application Insights Snapshot Debugger` anlık görüntüleri araştırmasını kullanıcılara rol.</span><span class="sxs-lookup"><span data-stu-id="f43f9-136">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="f43f9-137">Bu rolü, bireysel kullanıcılar veya gruplar için Application Insights kaynağı hedef abonelik sahipleri tarafından veya kendi kaynak grubuna veya aboneliğe atanabilir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-137">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="f43f9-138">Erişim denetimi (IAM) dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-138">Open the Access Control (IAM) blade.</span></span>
1. <span data-ttu-id="f43f9-139">Tıklatın + Ekle düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f43f9-139">Click the +Add button.</span></span>
1. <span data-ttu-id="f43f9-140">Uygulama Öngörüler anlık görüntü hata ayıklayıcı rolleri aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="f43f9-140">Select Application Insights Snapshot Debugger from the Roles drop-down list.</span></span>
1. <span data-ttu-id="f43f9-141">Arayın ve eklemek kullanıcı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f43f9-141">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="f43f9-142">Kullanıcı rolüne eklemek için Kaydet düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-142">Click the Save button to add the user to the role.</span></span>


[!IMPORTANT]
    <span data-ttu-id="f43f9-143">Anlık görüntüler olası değişken ve parametre değerlerini kişisel ve diğer hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-143">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="f43f9-144">Application Insights portalında anlık görüntüleri hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f43f9-144">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="f43f9-145">Belirli bir özel durum ya da bir sorun kimliği için bir anlık görüntü kullanılabiliyorsa, bir **açık hata ayıklama anlık görüntü** düğmesi görünür [özel durum](app-insights-asp-net-exceptions.md) Application Insights portalında.</span><span class="sxs-lookup"><span data-stu-id="f43f9-145">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![Özel durum açık hata ayıklama anlık görüntü düğmesine](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="f43f9-147">Anlık görüntü hata ayıklama Görünümü'nde, çağrı yığını ve değişkenleri bölmesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f43f9-147">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="f43f9-148">Çağrı yığını çerçeveler çağrı yığını Bölmesi'nde seçtiğinizde, yerel değişkenleri görüntüleyebilir ve bu işlev parametrelerini değişkenleri bölmesinde çağırın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-148">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![Hata ayıklama görünümü anlık portalında](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="f43f9-150">Varsayılan olarak görüntülenebilir olmadıkları ve anlık görüntüleri hassas bilgiler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-150">Snapshots might contain sensitive information, and by default they are not viewable.</span></span> <span data-ttu-id="f43f9-151">Anlık görüntüler görüntülemek için bilmeniz gereken `Application Insights Snapshot Debugger` rolü size atanmış.</span><span class="sxs-lookup"><span data-stu-id="f43f9-151">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="f43f9-152">Visual Studio 2017 Enterprise sahip anlık görüntüleri hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f43f9-152">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="f43f9-153">Tıklatın **karşıdan anlık görüntü** karşıdan yüklemek için düğmeyi bir `.diagsession` Visual Studio 2017 kuruluş tarafından açılabilir dosya.</span><span class="sxs-lookup"><span data-stu-id="f43f9-153">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span> 

2. <span data-ttu-id="f43f9-154">Açmak için `.diagsession` dosya, şunları yapmalısınız ilk [anlık görüntü hata ayıklayıcısı uzantısı için Visual Studio yükleyip](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="f43f9-154">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="f43f9-155">Anlık görüntü dosyayı açtıktan sonra Visual Studio'da mini döküm hata ayıklama sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-155">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="f43f9-156">Tıklatın **yönetilen kod hata ayıklama** anlık görüntü hata ayıklama başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="f43f9-156">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="f43f9-157">Anlık görüntü işlemi geçerli durumunu ayıklayabilirsiniz böylece burada özel durum oluştu kod satırına açar.</span><span class="sxs-lookup"><span data-stu-id="f43f9-157">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![Visual Studio'da hata ayıklama anlık görünümü](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="f43f9-159">İndirilen anlık görüntü web uygulaması sunucunuzda bulunan tüm simge dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-159">The downloaded snapshot contains any symbol files that were found on your web application server.</span></span> <span data-ttu-id="f43f9-160">Bu simge dosyaları, anlık görüntü verileri kaynak kodu ile ilişkilendirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-160">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="f43f9-161">Uygulama hizmeti uygulamalarınız için web uygulamaları yayımlarken simgesi dağıtım etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f43f9-161">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="f43f9-162">Anlık görüntüler nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="f43f9-162">How snapshots work</span></span>

<span data-ttu-id="f43f9-163">Uygulamanız başladığında, ayrı anlık görüntü yükleyici işlemi, uygulamanız için anlık görüntü istekleri izleyen oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f43f9-163">When your application starts, a separate snapshot uploader process is created that monitors your application for snapshot requests.</span></span> <span data-ttu-id="f43f9-164">Bir anlık görüntü istendiğinde, bir çalışan işlemi gölge kopyasını yaklaşık 10 ila 20 dakika içinde yapılır.</span><span class="sxs-lookup"><span data-stu-id="f43f9-164">When a snapshot is requested, a shadow copy of the running process is made in about 10 to 20 minutes.</span></span> <span data-ttu-id="f43f9-165">Gölge işleminin ardından analiz ve çalıştırmanız ve kullanıcılar için trafiği hizmet ana işlem devam ederken bir anlık görüntüsü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f43f9-165">The shadow process is then analyzed, and a snapshot is created while the main process continues to run and serve traffic to users.</span></span> <span data-ttu-id="f43f9-166">Anlık görüntü, ardından Application Insights'a anlık görüntüyü görüntülemek için gereken ilgili simge (.pdb) dosyalarla birlikte yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-166">The snapshot is then uploaded to Application Insights along with any relevant symbol (.pdb) files that are needed to view the snapshot.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="f43f9-167">Geçerli sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="f43f9-167">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="f43f9-168">Simgeler yayımlama</span><span class="sxs-lookup"><span data-stu-id="f43f9-168">Publish symbols</span></span>
<span data-ttu-id="f43f9-169">Anlık görüntü hata ayıklayıcı değişkenleri kod çözme ve Visual Studio'da hata ayıklama deneyimini sağlamak üzere üretim sunucusunda simge dosyaları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-169">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span> <span data-ttu-id="f43f9-170">Uygulama hizmeti yayımladığında Visual Studio 2017 15.2 sürümü yayın derlemeleri simgelerini varsayılan olarak yayımlar.</span><span class="sxs-lookup"><span data-stu-id="f43f9-170">The 15.2 release of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="f43f9-171">Önceki sürümlerde, aşağıdaki satırı yayımlama profilinizi eklemenize gerek `.pubxml` simgeleri yayın modunda yayımlanan dosyasını:</span><span class="sxs-lookup"><span data-stu-id="f43f9-171">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="f43f9-172">Azure işlem ve diğer türleri için simge dosyaları ana uygulama .dll aynı klasörde olduğundan emin olun (genellikle `wwwroot/bin`) ya da geçerli yolda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-172">For Azure Compute and other types, ensure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="f43f9-173">En iyi duruma getirilmiş derlemeleri</span><span class="sxs-lookup"><span data-stu-id="f43f9-173">Optimized builds</span></span>
<span data-ttu-id="f43f9-174">Bazı durumlarda, yerel değişkenleri oluşturma işlemi sırasında uygulanan en iyi duruma getirme nedeniyle yayın derlemelerde görüntülenemiyor.</span><span class="sxs-lookup"><span data-stu-id="f43f9-174">In some cases, local variables cannot be viewed in release builds because of optimizations that are applied during the build process.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f43f9-175">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f43f9-175">Troubleshooting</span></span>

<span data-ttu-id="f43f9-176">Bu ipuçları anlık görüntü hata ayıklayıcısı ile sorunları gidermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f43f9-176">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="f43f9-177">İzleme anahtarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f43f9-177">Verify the instrumentation key</span></span>

<span data-ttu-id="f43f9-178">Yayımlanan uygulamanızda doğru izleme anahtarını kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f43f9-178">Make sure that you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="f43f9-179">Genellikle, Application Insights izleme anahtarı Applicationınsights.config dosyasını okur.</span><span class="sxs-lookup"><span data-stu-id="f43f9-179">Usually, Application Insights reads the instrumentation key from the ApplicationInsights.config file.</span></span> <span data-ttu-id="f43f9-180">Değer Portalı'nda bkz Application Insights kaynağı izleme anahtarı ile aynı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-180">Verify that the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="f43f9-181">Yükleyici günlüklerini kontrol edin</span><span class="sxs-lookup"><span data-stu-id="f43f9-181">Check the uploader logs</span></span>

<span data-ttu-id="f43f9-182">Bir anlık görüntü oluşturulduktan sonra bir mini döküm dosyası (.dmp) disk üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f43f9-182">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="f43f9-183">Ayrı yükleyici işlem, mini döküm dosyası alır ve bunu uygulama Öngörüler anlık görüntü hata ayıklayıcı depolama ilişkili tüm pdb birlikte yükler.</span><span class="sxs-lookup"><span data-stu-id="f43f9-183">A separate uploader process takes that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="f43f9-184">Mini döküm başarıyla yükledi sonra diskten silinir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-184">After the minidump has uploaded successfully, it is deleted from disk.</span></span> <span data-ttu-id="f43f9-185">Mini döküm Yükleyici günlük dosyaları diskte korunur.</span><span class="sxs-lookup"><span data-stu-id="f43f9-185">The log files for the minidump uploader are retained on disk.</span></span> <span data-ttu-id="f43f9-186">Bir uygulama hizmeti ortamı'nda, bu günlükler bulabilirsiniz `D:\Home\LogFiles\Uploader_*.log`.</span><span class="sxs-lookup"><span data-stu-id="f43f9-186">In an App Service environment, you can find these logs in `D:\Home\LogFiles\Uploader_*.log`.</span></span> <span data-ttu-id="f43f9-187">Bu günlük dosyaları bulmak için uygulama hizmeti Kudu yönetim sitesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-187">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="f43f9-188">Uygulama hizmeti uygulamanızı Azure Portal'da açın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-188">Open your App Service application in the Azure portal.</span></span>

2. <span data-ttu-id="f43f9-189">Seçin **Gelişmiş Araçlar** dikey veya arama **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="f43f9-189">Select the **Advanced Tools** blade, or search for **Kudu**.</span></span>
3. <span data-ttu-id="f43f9-190">tıklatın **Git**.</span><span class="sxs-lookup"><span data-stu-id="f43f9-190">Click **Go**.</span></span>
4. <span data-ttu-id="f43f9-191">İçinde **hata ayıklama konsoluna** aşağı açılan liste kutusunda **CMD**.</span><span class="sxs-lookup"><span data-stu-id="f43f9-191">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="f43f9-192">Tıklatın **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="f43f9-192">Click **LogFiles**.</span></span>

<span data-ttu-id="f43f9-193">İle başlayan bir ada sahip en az bir dosya görmelisiniz `Uploader_` ve `.log` uzantısı.</span><span class="sxs-lookup"><span data-stu-id="f43f9-193">You should see at least one file with a name that begins with `Uploader_` and a `.log` extension.</span></span> <span data-ttu-id="f43f9-194">Tüm günlük dosyalarını indirin veya bir tarayıcıda açmak için uygun simgeye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-194">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="f43f9-195">Dosya adı makine adını içerir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-195">The file name includes the machine name.</span></span> <span data-ttu-id="f43f9-196">Uygulama hizmeti örneğinizi birden fazla makine üzerinde barındırılıyorsa, her makine için farklı günlük dosyaları vardır.</span><span class="sxs-lookup"><span data-stu-id="f43f9-196">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="f43f9-197">Yeni bir mini döküm dosyası karşıya yükleyen algıladığında, günlük dosyasına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-197">When the uploader detects a new minidump file, it is recorded in the log file.</span></span> <span data-ttu-id="f43f9-198">Başarılı bir karşıya yükleme bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f43f9-198">Here's an example of a successful upload:</span></span>

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

<span data-ttu-id="f43f9-199">İzleme anahtarını önceki örnekte olduğu `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="f43f9-199">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="f43f9-200">Bu değer, uygulamanız için izleme anahtarını eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-200">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="f43f9-201">Mini döküm Kimliğine sahip bir anlık görüntüsü ile ilişkili `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="f43f9-201">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="f43f9-202">Daha sonra uygulama Öngörüler analizleri ilişkili özel durum telemetrisi bulmak için bu kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f43f9-202">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="f43f9-203">Karşıya yükleyen her 15 dakikada hakkında yeni pdb tarar.</span><span class="sxs-lookup"><span data-stu-id="f43f9-203">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="f43f9-204">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f43f9-204">Here's an example:</span></span>

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

<span data-ttu-id="f43f9-205">Uygulamalar için _değil_ App Service içinde barındırılan, yükleyici Mini dökümler ile aynı klasörde günlüklerin: `%TEMP%\Dumps\<ikey>` (burada `<ikey>` araçları anahtarınız).</span><span class="sxs-lookup"><span data-stu-id="f43f9-205">For applications that are _not_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="f43f9-206">Anlık görüntüler istisnalar bulmak için Application Insights arama kullanın</span><span class="sxs-lookup"><span data-stu-id="f43f9-206">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="f43f9-207">Bir anlık görüntü oluşturulduğunda oluşturma özel durum ile bir anlık görüntü kimliği etiketli</span><span class="sxs-lookup"><span data-stu-id="f43f9-207">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="f43f9-208">Ne zaman özel durum telemetrisi Application Insights için anlık görüntü kimliği bir özel özellik olarak dahil olduğunu bildirdi.</span><span class="sxs-lookup"><span data-stu-id="f43f9-208">When the exception telemetry is reported to Application Insights, that snapshot ID is included as a custom property.</span></span> <span data-ttu-id="f43f9-209">Arama dikey Application Insights'ta kullanarak, tüm telemetri ile bulabilirsiniz `ai.snapshot.id` özel özellik.</span><span class="sxs-lookup"><span data-stu-id="f43f9-209">Using the Search blade in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="f43f9-210">Azure portalında Application Insights kaynağınıza göz atın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-210">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="f43f9-211">Tıklatın **arama**.</span><span class="sxs-lookup"><span data-stu-id="f43f9-211">Click **Search**.</span></span>
3. <span data-ttu-id="f43f9-212">Tür `ai.snapshot.id` arama metin kutusuna ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-212">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![Bir anlık görüntü kimliği portalındaki telemetriyle arayın](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="f43f9-214">Bu arama sonuç döndürürse, hiç anlık görüntü seçili zaman aralığı içinde uygulamanız için Application Insights bildirildi.</span><span class="sxs-lookup"><span data-stu-id="f43f9-214">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="f43f9-215">Yükleyici günlüklerini belirli bir anlık görüntüye Kimliğinden aramak için arama kutusunu bu kimliği yazın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-215">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="f43f9-216">Karşıya yüklenen bildiğiniz bir anlık görüntü için telemetri bulamazsanız, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f43f9-216">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="f43f9-217">İzleme anahtarını doğrulayarak sağ Application Insights kaynağı arıyorsanız denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f43f9-217">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="f43f9-218">Zaman damgası yükleyici günlüğündeki kullanarak, bu zaman aralığı karşılamak üzere arama zaman aralığı filtre ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f43f9-218">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="f43f9-219">Bu anlık görüntü Kimliğine sahip bir özel durum hala göremiyorsanız, özel durum telemetrisi Application Insights'a bildirilen değildi.</span><span class="sxs-lookup"><span data-stu-id="f43f9-219">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="f43f9-220">Bu durum, anlık görüntü sürdü sonra uygulamanızın kilitlendi, ancak özel durum telemetrisi bildirilen önce gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="f43f9-220">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="f43f9-221">Bu durumda, altında uygulama hizmeti günlüklerini kontrol `Diagnose and solve problems` beklenmeyen yeniden başlatmalar olup olmadığını görmek için veya işlenmeyen özel durum.</span><span class="sxs-lookup"><span data-stu-id="f43f9-221">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f43f9-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f43f9-222">Next steps</span></span>

* <span data-ttu-id="f43f9-223">[Kodunuzda snappoints ayarlamak](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) için bir özel durum beklemeden anlık görüntüleri alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="f43f9-223">[Set snappoints in your code](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="f43f9-224">[Özel durumlar, web uygulamalarında tanılama](app-insights-asp-net-exceptions.md) daha fazla özel durumlar Application Insights tarafından görülebilmesi için açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f43f9-224">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span> 
* <span data-ttu-id="f43f9-225">[Akıllı algılama](app-insights-proactive-diagnostics.md) performans anormalliklerini otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="f43f9-225">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
