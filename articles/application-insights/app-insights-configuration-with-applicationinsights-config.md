---
title: "aaaApplicationInsights.config başvuru - Azure | Microsoft Docs"
description: "Etkinleştirmek veya veri toplama modülleri devre dışı bırakın ve performans sayaçları ve diğer parametreleri ekleyin."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="191f0-103">Merhaba Application Insights SDK'sı Applicationınsights.config veya .xml yapılandırma</span><span class="sxs-lookup"><span data-stu-id="191f0-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="191f0-104">Merhaba Application Insights .NET SDK'sı bir NuGet paketlerini oluşur.</span><span class="sxs-lookup"><span data-stu-id="191f0-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="191f0-105">[Çekirdek paket](http://www.nuget.org/packages/Microsoft.ApplicationInsights) hello API hello Application Insights telemetri göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="191f0-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="191f0-106">[Ek paket](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) telemetri sağlamak *modülleri* ve *başlatıcıları* telemetri uygulamanız ve onun içeriği otomatik olarak izlemek için.</span><span class="sxs-lookup"><span data-stu-id="191f0-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="191f0-107">Hello yapılandırma dosyası ayarlayarak, etkinleştirmek veya telemetri modülleri ve başlatıcılar devre dışı bırakın ve bunların bazıları için parametreleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="191f0-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="191f0-108">Merhaba yapılandırma dosyası adlı `ApplicationInsights.config` veya `ApplicationInsights.xml`bağlı olarak, uygulamanızın hello türü.</span><span class="sxs-lookup"><span data-stu-id="191f0-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="191f0-109">Tooyour otomatik olarak eklenen ne zaman proje, [hello SDK çoğu sürümlerini yüklemek][start].</span><span class="sxs-lookup"><span data-stu-id="191f0-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="191f0-110">Tooa web uygulaması tarafından eklenir [Durum İzleyicisi bir IIS sunucusundaki][redfield], veya hello Appplication Öngörüler seçtiğinizde [bir Azure Web sitesine veya VM uzantısı](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="191f0-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="191f0-111">Bir eşdeğer dosya toocontrol hello hiç [SDK, bir web sayfasındaki][client].</span><span class="sxs-lookup"><span data-stu-id="191f0-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="191f0-112">Bu belgede, dosya, bunlar hello SDK ' hello bileşenlerinin nasıl kontrol ve bu bileşenleri hangi NuGet paketlerini yükleme hello yapılandırmasında bkz hello bölümleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="191f0-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="191f0-113">Telemetri modülleri (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="191f0-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="191f0-114">Her bir telemetri modülü, belirli bir veri türü toplar ve hello çekirdek API toosend hello veri kullanır.</span><span class="sxs-lookup"><span data-stu-id="191f0-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="191f0-115">Merhaba modülleri, ayrıca hello gerekli satırları toohello .config dosyası ekleyin farklı NuGet paketlerini tarafından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="191f0-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="191f0-116">Merhaba yapılandırma dosyasındaki her modül için bir düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="191f0-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="191f0-117">toodisable bir modül hello düğümü silin veya açıklama çıkarın.</span><span class="sxs-lookup"><span data-stu-id="191f0-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="191f0-118">Bağımlılık izleme</span><span class="sxs-lookup"><span data-stu-id="191f0-118">Dependency Tracking</span></span>
<span data-ttu-id="191f0-119">[Bağımlılık izleme](app-insights-asp-net-dependencies.md) uygulamanızı yapar toodatabases ve dış hizmetler ve veritabanları çağrıları hakkında telemetri toplar.</span><span class="sxs-lookup"><span data-stu-id="191f0-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="191f0-120">tooallow bu modülü toowork IIS Server çok ihtiyacınız[Durum İzleyicisi yükleme][redfield].</span><span class="sxs-lookup"><span data-stu-id="191f0-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="191f0-121">toouse bunu Azure web uygulamaları ya da sanal makineleri, [seçin hello Application Insights uzantısını](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="191f0-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="191f0-122">İzleme kodu hello kullanarak kendi bağımlılık de yazabilirsiniz [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="191f0-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="191f0-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="191f0-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="191f0-124">Performans Toplayıcı</span><span class="sxs-lookup"><span data-stu-id="191f0-124">Performance collector</span></span>
<span data-ttu-id="191f0-125">[Sistem performans sayaçlarını toplar](app-insights-performance-counters.md) gibi CPU, bellek ve ağ IIS yüklemelerinden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="191f0-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="191f0-126">Performans sayaçları, kendiniz ayarladığınız dahil olmak üzere hangi sayaçları toocollect belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="191f0-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="191f0-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="191f0-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="191f0-128">Application Insights tanılama Telemetrisi</span><span class="sxs-lookup"><span data-stu-id="191f0-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="191f0-129">Merhaba `DiagnosticsTelemetryModule` hello Application Insights araçları kod kendisini hataları bildirir.</span><span class="sxs-lookup"><span data-stu-id="191f0-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="191f0-130">Örneğin, performans sayaçları hello kod erişemiyorsanız veya bir `ITelemetryInitializer` bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="191f0-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="191f0-131">Bu modülü tarafından izlenen izleme telemetri görünür hello [tanılama arama][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="191f0-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="191f0-132">Tanılama veri toodc.services.vsallin.net gönderir.</span><span class="sxs-lookup"><span data-stu-id="191f0-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="191f0-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="191f0-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="191f0-134">Yalnızca bu paketi yüklerseniz, hello Applicationınsights.config dosyası otomatik olarak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="191f0-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="191f0-135">Geliştirici modu</span><span class="sxs-lookup"><span data-stu-id="191f0-135">Developer Mode</span></span>
<span data-ttu-id="191f0-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`zorlar hello Application Insights `TelemetryChannel` hemen toosend veri bir telemetri öğesi, her seferinde bir hata ayıklayıcısı olduğunda bağlı toohello uygulama işlemi.</span><span class="sxs-lookup"><span data-stu-id="191f0-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="191f0-137">Bu, uygulamanızın telemetri izler ve hello Application Insights portalında görüntülendiğinde hello şu anda arasındaki süre hello miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="191f0-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="191f0-138">Önemli yükünü CPU ve ağ bant genişliği neden olur.</span><span class="sxs-lookup"><span data-stu-id="191f0-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="191f0-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="191f0-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="191f0-140">Web isteği izleme</span><span class="sxs-lookup"><span data-stu-id="191f0-140">Web Request Tracking</span></span>
<span data-ttu-id="191f0-141">Raporları hello [yanıt süresi ve sonuç kodu](app-insights-asp-net.md) HTTP isteklerinin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="191f0-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="191f0-142">[Microsoft.applicationınsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="191f0-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="191f0-143">Özel durum izleme</span><span class="sxs-lookup"><span data-stu-id="191f0-143">Exception tracking</span></span>
<span data-ttu-id="191f0-144">`ExceptionTrackingTelemetryModule`parçaları işlenmeyen özel durumlar web uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="191f0-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="191f0-145">Bkz: [hataları ve özel durumları][exceptions].</span><span class="sxs-lookup"><span data-stu-id="191f0-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="191f0-146">[Microsoft.applicationınsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="191f0-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="191f0-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-parçaları [görev özel durumlarını unobserved](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="191f0-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="191f0-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-çalışan rolleri, windows Hizmetleri ve konsol uygulamaları için işlenmeyen özel durumları izler.</span><span class="sxs-lookup"><span data-stu-id="191f0-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="191f0-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="191f0-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="191f0-150">EventSource izleme</span><span class="sxs-lookup"><span data-stu-id="191f0-150">EventSource Tracking</span></span>
<span data-ttu-id="191f0-151">`EventSourceTelemetryModule`tooconfigure tooApplication Öngörüler izlemeleri gönderilen EventSource olaylarını toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="191f0-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="191f0-152">EventSource olaylarını izleme hakkında daha fazla bilgi için bkz: [kullanarak EventSource olaylarını](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="191f0-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="191f0-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="191f0-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="191f0-154">ETW olay izleme</span><span class="sxs-lookup"><span data-stu-id="191f0-154">ETW Event Tracking</span></span>
<span data-ttu-id="191f0-155">`EtwCollectorTelemetryModule`ETW sağlayıcılar toobe tooApplication Öngörüler izlemeleri gönderilen tooconfigure olayları sağlar.</span><span class="sxs-lookup"><span data-stu-id="191f0-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="191f0-156">ETW olayları izleme hakkında daha fazla bilgi için bkz: [kullanarak ETW olayları](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="191f0-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="191f0-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="191f0-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="191f0-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="191f0-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="191f0-159">Merhaba Microsoft.ApplicationInsights paket sağlar hello [API çekirdek](https://msdn.microsoft.com/library/mt420197.aspx) hello SDK.</span><span class="sxs-lookup"><span data-stu-id="191f0-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="191f0-160">Merhaba diğer telemetri modüller bunu kullanın ve ayrıca [toodefine kullanmak kendi telemetrinizi](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="191f0-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="191f0-161">Applicationınsights.config giriş yok.</span><span class="sxs-lookup"><span data-stu-id="191f0-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="191f0-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="191f0-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="191f0-163">Yalnızca bu NuGet yüklerseniz, hiçbir .config dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="191f0-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="191f0-164">Telemetri kanal</span><span class="sxs-lookup"><span data-stu-id="191f0-164">Telemetry Channel</span></span>
<span data-ttu-id="191f0-165">Merhaba telemetri kanal arabelleğe alma ve telemetri toohello Application Insights hizmeti aktarımını yönetir.</span><span class="sxs-lookup"><span data-stu-id="191f0-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="191f0-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`Hizmetler için Hello varsayılan kanalıdır.</span><span class="sxs-lookup"><span data-stu-id="191f0-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="191f0-167">Bu veri arabelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="191f0-167">It buffers data in memory.</span></span>
* <span data-ttu-id="191f0-168">`Microsoft.ApplicationInsights.PersistenceChannel`konsol uygulamaları için bir alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="191f0-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="191f0-169">Uygulamanızı kapatır ve hello uygulama yeniden başlatıldığında Gönder herhangi unflushed veri toopersistent depolama kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="191f0-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="191f0-170">Telemetri başlatıcıları (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="191f0-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="191f0-171">Telemetri başlatıcıları telemetrinin her öğesiyle birlikte gönderilir bağlam özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="191f0-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="191f0-172">Yapabilecekleriniz [kendi başlatıcıları yazma](app-insights-api-filtering-sampling.md#add-properties) tooset bağlam özellikleri.</span><span class="sxs-lookup"><span data-stu-id="191f0-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="191f0-173">Merhaba standart başlatıcıları tüm hello Web veya Windows Server NuGet paketleri tarafından ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="191f0-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="191f0-174">`AccountIdTelemetryInitializer`Merhaba AccountID özelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="191f0-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="191f0-175">`AuthenticatedUserIdTelemetryInitializer`Merhaba AuthenticatedUserId özelliği hello JavaScript SDK'sı tarafından kümesi olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="191f0-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="191f0-176">`AzureRoleEnvironmentTelemetryInitializer`güncelleştirmeleri hello `RoleName` ve `RoleInstance` hello özelliklerini `Device` hello Azure çalışma zamanı ortamından ayıklanan bilgilerle tüm telemetri öğeleri için bağlamı.</span><span class="sxs-lookup"><span data-stu-id="191f0-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="191f0-177">`BuildInfoConfigComponentVersionTelemetryInitializer`güncelleştirmeleri hello `Version` hello özelliğinin `Component` hello ayıklanan hello değere sahip tüm telemetri öğeleri bağlamının `BuildInfo.config` dosya MS Build tarafından üretilen.</span><span class="sxs-lookup"><span data-stu-id="191f0-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="191f0-178">`ClientIpHeaderTelemetryInitializer`güncelleştirmeleri `Ip` hello özelliğinin `Location` tüm telemetri öğeleri bağlamında dayalı hello üzerinde `X-Forwarded-For` hello isteğin HTTP üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="191f0-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="191f0-179">`DeviceTelemetryInitializer`Merhaba özelliklerini aşağıdaki güncelleştirmeleri hello `Device` tüm telemetri öğeleri için bağlamı.</span><span class="sxs-lookup"><span data-stu-id="191f0-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="191f0-180">`Type`çok Ayarla "PC"</span><span class="sxs-lookup"><span data-stu-id="191f0-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="191f0-181">`Id`Merhaba bilgisayarın etki alanı adını toohello Merhaba web uygulaması çalıştığı ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="191f0-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="191f0-182">`OemName`Hello ayıklanan toohello değerini ayarlayın `Win32_ComputerSystem.Manufacturer` WMI kullanarak alan.</span><span class="sxs-lookup"><span data-stu-id="191f0-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="191f0-183">`Model`Hello ayıklanan toohello değerini ayarlayın `Win32_ComputerSystem.Model` WMI kullanarak alan.</span><span class="sxs-lookup"><span data-stu-id="191f0-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="191f0-184">`NetworkType`Hello ayıklanan toohello değerini ayarlayın `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="191f0-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="191f0-185">`Language`Merhaba toohello adına ayarlanır `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="191f0-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="191f0-186">`DomainNameRoleInstanceTelemetryInitializer`güncelleştirmeleri hello `RoleInstance` hello özelliğinin `Device` hello etki alanı adına sahip tüm telemetri öğelerin hello bilgisayar Merhaba web uygulaması çalıştığı bağlam.</span><span class="sxs-lookup"><span data-stu-id="191f0-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="191f0-187">`OperationNameTelemetryInitializer`güncelleştirmeleri hello `Name` hello özelliğinin `RequestTelemetry` ve hello `Name` hello özelliğinin `Operation` tüm telemetri öğeleri bağlamında dayalı hello HTTP yöntemi, yanı sıra üzerinde ASP.NET MVC denetleyicisi ve eylem çağrılan tooprocess hello adları İstek.</span><span class="sxs-lookup"><span data-stu-id="191f0-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="191f0-188">`OperationIdTelemetryInitializer`veya `OperationCorrelationTelemetryInitializer` güncelleştirmeleri hello `Operation.Id` içerik özelliği tüm telemetri öğelerin izlenen hello ile otomatik olarak oluşturulan bir isteği işlerken `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="191f0-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="191f0-189">`SessionTelemetryInitializer`güncelleştirmeleri hello `Id` hello özelliğinin `Session` tüm telemetri öğeleri hello ayıklanan değerle bağlamının `ai_session` tanımlama bilgisi hello kullanıcının tarayıcısında çalışan Applicationınsights JavaScript araçları kodu hello tarafından oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="191f0-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="191f0-190">`SyntheticTelemetryInitializer`veya `SyntheticUserAgentTelemetryInitializer` güncelleştirmeleri hello `User`, `Session` ve `Operation` kullanılabilirlik test veya arama motoru bot gibi yapay bir kaynaktan bir isteği işlerken tüm telemetri öğelerinin bağlamları özellikleri izlenir.</span><span class="sxs-lookup"><span data-stu-id="191f0-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="191f0-191">Varsayılan olarak, [ölçüm Gezgini](app-insights-metrics-explorer.md) yapay telemetri görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="191f0-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="191f0-192">Merhaba `<Filters>` hello isteklerinin özelliklerini tanımlayan ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="191f0-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="191f0-193">`UserAgentTelemetryInitializer`güncelleştirmeleri hello `UserAgent` hello özelliğinin `User` tüm telemetri öğeleri bağlamında dayalı hello üzerinde `User-Agent` hello isteğin HTTP üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="191f0-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="191f0-194">`UserTelemetryInitializer`güncelleştirmeleri hello `Id` ve `AcquisitionDate` özelliklerini `User` hello ayıklanan değerlere sahip tüm telemetri öğeleri bağlamının `ai_user` hello çalışan hello uygulama Insights JavaScript araçları kodu tarafından oluşturulan tanımlama bilgisi Kullanıcının tarayıcısının.</span><span class="sxs-lookup"><span data-stu-id="191f0-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="191f0-195">`WebTestTelemetryInitializer`ayarlar, kullanıcı kimliği, oturum kimliği ve yapay kaynak özelliklerini bu geliyor HTTP istekleri için hello [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="191f0-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="191f0-196">Merhaba `<Filters>` hello isteklerinin özelliklerini tanımlayan ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="191f0-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="191f0-197">Service Fabric çalışan .NET uygulamaları için hello içerebilir `Microsoft.ApplicationInsights.ServiceFabric` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="191f0-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="191f0-198">Bu paketi içeren bir `FabricTelemetryInitializer`, Service Fabric özellikleri tootelemetry öğeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="191f0-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="191f0-199">Daha fazla bilgi için bkz: Merhaba [GitHub sayfası](https://go.microsoft.com/fwlink/?linkid=848457) bu NuGet paketi tarafından eklenen hello özellikleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="191f0-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="191f0-200">Telemetri işlemci (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="191f0-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="191f0-201">Telemetri işlemciler filtre ve hello SDK toohello portalından gönderilmeden önce her bir telemetri öğeyi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="191f0-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="191f0-202">Yapabilecekleriniz [kendi telemetri işlemciler yazma](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="191f0-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="191f0-203">Uyarlamalı örnekleme telemetri işlemcisine (2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="191f0-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="191f0-204">Bu, varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="191f0-204">This is enabled by default.</span></span> <span data-ttu-id="191f0-205">Uygulamanız çok sayıda telemetri gönderirse, bu işlemci bazıları da kaldırır.</span><span class="sxs-lookup"><span data-stu-id="191f0-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="191f0-206">Merhaba parametresi tooachieve algoritması hello hello hedef çalışır sağlar.</span><span class="sxs-lookup"><span data-stu-id="191f0-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="191f0-207">Sunucunuz birden fazla makine bir küme ise, telemetri gerçek hacmi hello uygun şekilde çarpılır şekilde hello her örneği SDK bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="191f0-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="191f0-208">[Örnekleme hakkında daha fazla bilgi](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="191f0-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="191f0-209">Sabit oran örnekleme telemetri işlemcisine (2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="191f0-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="191f0-210">Ayrıca bir standart olan [telemetri işlemci örnekleme](app-insights-api-filtering-sampling.md) (Başlangıç 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="191f0-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="191f0-211">Kanal parametreleri (Java)</span><span class="sxs-lookup"><span data-stu-id="191f0-211">Channel parameters (Java)</span></span>
<span data-ttu-id="191f0-212">Bu parametreler hello Java SDK'sı nasıl ve depolamak topladığı hello telemetri verilerini temizleme etkiler.</span><span class="sxs-lookup"><span data-stu-id="191f0-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="191f0-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="191f0-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="191f0-214">Merhaba hello SDK'ın bellek içi depolamada depolanan telemetri öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="191f0-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="191f0-215">Bu sayıya ulaşıldığında, hello telemetri arabellek Temizlenen - hello telemetri öğeleri toohello Application Insights sunucusunun diğer bir deyişle, gönderilir.</span><span class="sxs-lookup"><span data-stu-id="191f0-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="191f0-216">Min: 1</span><span class="sxs-lookup"><span data-stu-id="191f0-216">Min: 1</span></span>
* <span data-ttu-id="191f0-217">En fazla: 1000</span><span class="sxs-lookup"><span data-stu-id="191f0-217">Max: 1000</span></span>
* <span data-ttu-id="191f0-218">Varsayılan: 500</span><span class="sxs-lookup"><span data-stu-id="191f0-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="191f0-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="191f0-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="191f0-220">Ne sıklıkta hello hello bellek içi depolamada depolanan verileri temizlendi (gönderilen tooApplication Öngörüler) olmayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="191f0-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="191f0-221">Min: 1</span><span class="sxs-lookup"><span data-stu-id="191f0-221">Min: 1</span></span>
* <span data-ttu-id="191f0-222">En fazla: 300</span><span class="sxs-lookup"><span data-stu-id="191f0-222">Max: 300</span></span>
* <span data-ttu-id="191f0-223">Varsayılan: 5</span><span class="sxs-lookup"><span data-stu-id="191f0-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="191f0-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="191f0-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="191f0-225">Hello yerel diskteki toohello kalıcı depolama ayrılan MB cinsinden maksimum boyutu Hello belirler.</span><span class="sxs-lookup"><span data-stu-id="191f0-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="191f0-226">Bu depolama aktarılan toobe toohello Application Insights endpoint başarısız kalıcı telemetri öğeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="191f0-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="191f0-227">Merhaba depolama boyutu sağlandığında yeni telemetri öğeleri atılacak.</span><span class="sxs-lookup"><span data-stu-id="191f0-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="191f0-228">Min: 1</span><span class="sxs-lookup"><span data-stu-id="191f0-228">Min: 1</span></span>
* <span data-ttu-id="191f0-229">En fazla: 100</span><span class="sxs-lookup"><span data-stu-id="191f0-229">Max: 100</span></span>
* <span data-ttu-id="191f0-230">Varsayılan: 10</span><span class="sxs-lookup"><span data-stu-id="191f0-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="191f0-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="191f0-231">InstrumentationKey</span></span>
<span data-ttu-id="191f0-232">Bu, verilerinizi göründüğü hello Application Insights kaynağı belirler.</span><span class="sxs-lookup"><span data-stu-id="191f0-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="191f0-233">Genellikle, ayrı bir kaynak ayrı bir anahtarla her uygulamalarınız için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="191f0-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="191f0-234">Uygulama toodifferent kaynaklarınızdan - toosend sonuçları istiyorsanız tooset hello anahtar dinamik olarak - örneğin istiyorsanız hello anahtar hello yapılandırma dosyasından atlayın ve bunun yerine kodda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="191f0-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="191f0-235">tooset hello anahtarını TelemetryClient, standart telemetri modüller de dahil olmak üzere tüm örnekleri için başlangıç anahtarı TelemetryConfiguration.Active ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="191f0-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="191f0-236">Bu, bir ASP.NET hizmetinde global.aspx.cs gibi başlatma yöntemini yapın:</span><span class="sxs-lookup"><span data-stu-id="191f0-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="191f0-237">Toosend yalnızca istiyorsanız olayları tooa farklı kaynak belirli bir ayarla, belirli bir TelemetryClient için başlangıç anahtarı ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="191f0-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="191f0-238">Yeni bir anahtar tooget [hello Application Insights portalında yeni bir kaynak oluşturmak][new].</span><span class="sxs-lookup"><span data-stu-id="191f0-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="191f0-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="191f0-239">Next steps</span></span>
<span data-ttu-id="191f0-240">[Merhaba API'si hakkında daha fazla bilgi][api].</span><span class="sxs-lookup"><span data-stu-id="191f0-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
