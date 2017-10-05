---
title: "Applicationınsights.config başvuru - Azure | Microsoft Docs"
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
ms.openlocfilehash: 7737f47d4181b5e920434f3a5372991efb58f63e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="45838-103">ApplicationInsights.config veya .xml ile Application Insights SDK yapılandırma</span><span class="sxs-lookup"><span data-stu-id="45838-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="45838-104">Application Insights .NET SDK'sı bir NuGet paketlerini oluşur.</span><span class="sxs-lookup"><span data-stu-id="45838-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="45838-105">[Çekirdek paket](http://www.nuget.org/packages/Microsoft.ApplicationInsights) Application Insights telemetri göndermek için API sağlar.</span><span class="sxs-lookup"><span data-stu-id="45838-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="45838-106">[Ek paket](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) telemetri sağlamak *modülleri* ve *başlatıcıları* telemetri uygulamanız ve onun içeriği otomatik olarak izlemek için.</span><span class="sxs-lookup"><span data-stu-id="45838-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="45838-107">Yapılandırma dosyası ayarlayarak, etkinleştirmek veya telemetri modülleri ve başlatıcılar devre dışı bırakın ve bazıları için parametreleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="45838-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="45838-108">Yapılandırma dosyası adlı `ApplicationInsights.config` veya `ApplicationInsights.xml`, uygulamanın türüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="45838-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="45838-109">Projenize otomatik olarak eklenen olduğunda, [SDK çoğu sürümlerini yüklemek][start].</span><span class="sxs-lookup"><span data-stu-id="45838-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="45838-110">Ayrıca bir web uygulamasına tarafından eklenir [Durum İzleyicisi bir IIS sunucusundaki][redfield], veya Appplication Öngörüler seçtiğinizde [bir Azure Web sitesine veya VM uzantısı](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="45838-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="45838-111">Denetim eşdeğer bir dosyaya hiç [SDK, bir web sayfasındaki][client].</span><span class="sxs-lookup"><span data-stu-id="45838-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="45838-112">Bu belgede, dosya, bunlar bileşenleri SDK ' nın nasıl kontrol ve bu bileşenleri hangi NuGet paketlerini yükleme yapılandırmada bkz bölümlerde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="45838-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="45838-113">Telemetri modülleri (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="45838-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="45838-114">Her bir telemetri modülü, belirli bir veri türü toplar ve veri göndermek için çekirdek API kullanır.</span><span class="sxs-lookup"><span data-stu-id="45838-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="45838-115">Modüller, ayrıca gerekli satırları .config dosyasına ekleyin farklı NuGet paketleri tarafından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="45838-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="45838-116">Yapılandırma dosyasındaki her modül için bir düğüm yok.</span><span class="sxs-lookup"><span data-stu-id="45838-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="45838-117">Bir modül devre dışı bırakmak için düğüm silin veya açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="45838-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="45838-118">Bağımlılık izleme</span><span class="sxs-lookup"><span data-stu-id="45838-118">Dependency Tracking</span></span>
<span data-ttu-id="45838-119">[Bağımlılık izleme](app-insights-asp-net-dependencies.md) uygulamanızı yapar veritabanları ve dış hizmetler ve veritabanları için çağrıları hakkında telemetri toplar.</span><span class="sxs-lookup"><span data-stu-id="45838-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="45838-120">Bir IIS Server'da çalışmak için bu modülü izin vermek için gereken [Durum İzleyicisi yükleme][redfield].</span><span class="sxs-lookup"><span data-stu-id="45838-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="45838-121">Azure web uygulamaları veya sanal makineleri, kullanılacak [Application Insights uzantısını seçin](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="45838-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="45838-122">Kod kullanarak izleme kendi bağımlılık de yazabilirsiniz [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="45838-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="45838-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="45838-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="45838-124">Performans Toplayıcı</span><span class="sxs-lookup"><span data-stu-id="45838-124">Performance collector</span></span>
<span data-ttu-id="45838-125">[Sistem performans sayaçlarını toplar](app-insights-performance-counters.md) gibi CPU, bellek ve ağ IIS yüklemelerinden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="45838-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="45838-126">Performans sayaçları, kendiniz ayarladığınız dahil olmak üzere toplamak için hangi sayaçları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45838-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="45838-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="45838-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="45838-128">Application Insights tanılama Telemetrisi</span><span class="sxs-lookup"><span data-stu-id="45838-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="45838-129">`DiagnosticsTelemetryModule` Application Insights araçları kod kendisini hataları bildirir.</span><span class="sxs-lookup"><span data-stu-id="45838-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="45838-130">Örneğin, kod performans sayaçları erişemiyorsanız veya bir `ITelemetryInitializer` bir özel durum oluşturur.</span><span class="sxs-lookup"><span data-stu-id="45838-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="45838-131">Bu modülü tarafından izlenen izleme telemetri görünür [tanılama arama][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="45838-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="45838-132">Tanılama verileri için dc.services.vsallin.net gönderir.</span><span class="sxs-lookup"><span data-stu-id="45838-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="45838-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="45838-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="45838-134">Yalnızca bu paketi yüklerseniz, Applicationınsights.config dosyası otomatik olarak oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="45838-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="45838-135">Geliştirici modu</span><span class="sxs-lookup"><span data-stu-id="45838-135">Developer Mode</span></span>
<span data-ttu-id="45838-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`Application Insights zorlar `TelemetryChannel` veri hemen bir hata ayıklayıcı uygulama işlemi için bağlı olduğunda, bir seferde bir telemetri öğesi göndermek için.</span><span class="sxs-lookup"><span data-stu-id="45838-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="45838-137">Uygulamanızı telemetri izler ve Application Insights portalında görüntülendiğinde bu anda arasındaki süreyi azaltır.</span><span class="sxs-lookup"><span data-stu-id="45838-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="45838-138">Önemli yükünü CPU ve ağ bant genişliği neden olur.</span><span class="sxs-lookup"><span data-stu-id="45838-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="45838-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="45838-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="45838-140">Web isteği izleme</span><span class="sxs-lookup"><span data-stu-id="45838-140">Web Request Tracking</span></span>
<span data-ttu-id="45838-141">Raporları [yanıt süresi ve sonuç kodu](app-insights-asp-net.md) HTTP isteklerinin sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="45838-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="45838-142">[Microsoft.applicationınsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="45838-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="45838-143">Özel durum izleme</span><span class="sxs-lookup"><span data-stu-id="45838-143">Exception tracking</span></span>
<span data-ttu-id="45838-144">`ExceptionTrackingTelemetryModule`parçaları işlenmeyen özel durumlar web uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="45838-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="45838-145">Bkz: [hataları ve özel durumları][exceptions].</span><span class="sxs-lookup"><span data-stu-id="45838-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="45838-146">[Microsoft.applicationınsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet paketi</span><span class="sxs-lookup"><span data-stu-id="45838-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="45838-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-parçaları [görev özel durumlarını unobserved](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="45838-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="45838-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-çalışan rolleri, windows Hizmetleri ve konsol uygulamaları için işlenmeyen özel durumları izler.</span><span class="sxs-lookup"><span data-stu-id="45838-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="45838-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="45838-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="45838-150">EventSource izleme</span><span class="sxs-lookup"><span data-stu-id="45838-150">EventSource Tracking</span></span>
<span data-ttu-id="45838-151">`EventSourceTelemetryModule`EventSource olaylarını Application Insights izlemeleri olarak gönderilmesini yapılandırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="45838-151">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="45838-152">EventSource olaylarını izleme hakkında daha fazla bilgi için bkz: [kullanarak EventSource olaylarını](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="45838-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="45838-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="45838-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="45838-154">ETW olay izleme</span><span class="sxs-lookup"><span data-stu-id="45838-154">ETW Event Tracking</span></span>
<span data-ttu-id="45838-155">`EtwCollectorTelemetryModule`Application Insights izlemeleri olarak gönderilmesini ETW sağlayıcılar olaylarından yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="45838-155">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="45838-156">ETW olayları izleme hakkında daha fazla bilgi için bkz: [kullanarak ETW olayları](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="45838-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="45838-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="45838-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="45838-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="45838-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="45838-159">Microsoft.ApplicationInsights paket sağlar [API çekirdek](https://msdn.microsoft.com/library/mt420197.aspx) SDK'sının.</span><span class="sxs-lookup"><span data-stu-id="45838-159">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="45838-160">Bu diğer telemetri modüllerini kullanmanız ve ayrıca [kendi telemetrinizi tanımlamak için kullanmak](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="45838-160">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="45838-161">Applicationınsights.config giriş yok.</span><span class="sxs-lookup"><span data-stu-id="45838-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="45838-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="45838-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="45838-163">Yalnızca bu NuGet yüklerseniz, hiçbir .config dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="45838-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="45838-164">Telemetri kanal</span><span class="sxs-lookup"><span data-stu-id="45838-164">Telemetry Channel</span></span>
<span data-ttu-id="45838-165">Telemetri kanal arabelleğe alma ve telemetri Application Insights hizmetine aktarımını yönetir.</span><span class="sxs-lookup"><span data-stu-id="45838-165">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="45838-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`Hizmetler için varsayılan kanalıdır.</span><span class="sxs-lookup"><span data-stu-id="45838-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="45838-167">Bu veri arabelleğe alır.</span><span class="sxs-lookup"><span data-stu-id="45838-167">It buffers data in memory.</span></span>
* <span data-ttu-id="45838-168">`Microsoft.ApplicationInsights.PersistenceChannel`konsol uygulamaları için bir alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="45838-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="45838-169">Uygulamanızı kapatır ve uygulama yeniden başlatıldığında Gönder unflushed tüm verileri kalıcı depolama birimine kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45838-169">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="45838-170">Telemetri başlatıcıları (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="45838-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="45838-171">Telemetri başlatıcıları telemetrinin her öğesiyle birlikte gönderilir bağlam özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="45838-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="45838-172">Yapabilecekleriniz [kendi başlatıcıları yazma](app-insights-api-filtering-sampling.md#add-properties) bağlamı özelliklerini ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="45838-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="45838-173">Standart başlatıcıları tüm Web veya Windows Server NuGet paketleri tarafından ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="45838-173">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="45838-174">`AccountIdTelemetryInitializer`Hesap Kimliği özelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="45838-174">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="45838-175">`AuthenticatedUserIdTelemetryInitializer`JavaScript SDK'sı tarafından belirlenen AuthenticatedUserId özelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="45838-175">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="45838-176">`AzureRoleEnvironmentTelemetryInitializer`güncelleştirmeleri `RoleName` ve `RoleInstance` özelliklerini `Device` Azure çalışma zamanı ortamından ayıklanan bilgilerle tüm telemetri öğeleri için bağlamı.</span><span class="sxs-lookup"><span data-stu-id="45838-176">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="45838-177">`BuildInfoConfigComponentVersionTelemetryInitializer`güncelleştirmeleri `Version` özelliği `Component` tüm telemetri öğeleri ayıklanan değerle bağlamının `BuildInfo.config` dosya MS Build tarafından üretilen.</span><span class="sxs-lookup"><span data-stu-id="45838-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="45838-178">`ClientIpHeaderTelemetryInitializer`güncelleştirmeleri `Ip` özelliği `Location` tüm telemetri öğeleri bağlamında temel alarak `X-Forwarded-For` isteğin HTTP üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="45838-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="45838-179">`DeviceTelemetryInitializer`Aşağıdaki özellikleri güncelleştirmeleri `Device` tüm telemetri öğeleri için bağlamı.</span><span class="sxs-lookup"><span data-stu-id="45838-179">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="45838-180">`Type`"Bilgisayar" ayarlayın</span><span class="sxs-lookup"><span data-stu-id="45838-180">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="45838-181">`Id`web uygulamasının çalıştığı bilgisayarın etki alanı adına ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="45838-181">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="45838-182">`OemName`Ayıklanan değerine ayarlanır `Win32_ComputerSystem.Manufacturer` WMI kullanarak alan.</span><span class="sxs-lookup"><span data-stu-id="45838-182">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="45838-183">`Model`Ayıklanan değerine ayarlanır `Win32_ComputerSystem.Model` WMI kullanarak alan.</span><span class="sxs-lookup"><span data-stu-id="45838-183">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="45838-184">`NetworkType`Ayıklanan değerine ayarlanır `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="45838-184">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="45838-185">`Language`adına ayarlayın `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="45838-185">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="45838-186">`DomainNameRoleInstanceTelemetryInitializer`güncelleştirmeleri `RoleInstance` özelliği `Device` web uygulamasının çalıştığı bilgisayarın etki alanı adı ile tüm telemetri öğelerini bağlamı.</span><span class="sxs-lookup"><span data-stu-id="45838-186">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="45838-187">`OperationNameTelemetryInitializer`güncelleştirmeleri `Name` özelliği `RequestTelemetry` ve `Name` özelliği `Operation` tüm telemetri öğeleri bağlamında temel HTTP yöntemini yanı sıra üzerinde adlarını, ASP.NET MVC denetleyicisi ve eylem isteği işlemek üzere çağrılır.</span><span class="sxs-lookup"><span data-stu-id="45838-187">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="45838-188">`OperationIdTelemetryInitializer`veya `OperationCorrelationTelemetryInitializer` güncelleştirmeleri `Operation.Id` içerik özelliği tüm telemetri öğelerin izlenen otomatik olarak oluşturulan bir isteği işlerken `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="45838-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="45838-189">`SessionTelemetryInitializer`güncelleştirmeleri `Id` özelliği `Session` tüm telemetri öğeleri ayıklanan değerle bağlamının `ai_session` kullanıcının tarayıcısında çalışan Applicationınsights JavaScript araçları kodu tarafından oluşturulan tanımlama bilgisi.</span><span class="sxs-lookup"><span data-stu-id="45838-189">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="45838-190">`SyntheticTelemetryInitializer`veya `SyntheticUserAgentTelemetryInitializer` güncelleştirmeleri `User`, `Session` ve `Operation` kullanılabilirlik test veya arama motoru bot gibi yapay bir kaynaktan bir isteği işlerken tüm telemetri öğelerinin bağlamları özellikleri izlenir.</span><span class="sxs-lookup"><span data-stu-id="45838-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="45838-191">Varsayılan olarak, [ölçüm Gezgini](app-insights-metrics-explorer.md) yapay telemetri görüntülemez.</span><span class="sxs-lookup"><span data-stu-id="45838-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="45838-192">`<Filters>` İsteklerinin özelliklerini tanımlayan ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="45838-192">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="45838-193">`UserAgentTelemetryInitializer`güncelleştirmeleri `UserAgent` özelliği `User` tüm telemetri öğeleri bağlamında temel alarak `User-Agent` isteğin HTTP üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="45838-193">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="45838-194">`UserTelemetryInitializer`güncelleştirmeleri `Id` ve `AcquisitionDate` özelliklerini `User` ayıklanan değerlere sahip tüm telemetri öğeleri bağlamının `ai_user` tanımlama bilgisi kullanıcının içinde çalışan uygulama Insights JavaScript araçları kodu tarafından oluşturulan Tarayıcı.</span><span class="sxs-lookup"><span data-stu-id="45838-194">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="45838-195">`WebTestTelemetryInitializer`Bu geliyor HTTP istekleri için kullanıcı kimliği ve oturum kimliği yapay kaynağı özellikleri ayarlar [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="45838-195">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="45838-196">`<Filters>` İsteklerinin özelliklerini tanımlayan ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="45838-196">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="45838-197">Service Fabric çalışan .NET uygulamaları için eklediğiniz `Microsoft.ApplicationInsights.ServiceFabric` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="45838-197">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="45838-198">Bu paketi içeren bir `FabricTelemetryInitializer`, telemetri öğelerine Service Fabric özellikler ekler.</span><span class="sxs-lookup"><span data-stu-id="45838-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="45838-199">Daha fazla bilgi için bkz: [GitHub sayfası](https://go.microsoft.com/fwlink/?linkid=848457) bu NuGet paketi tarafından eklenen özellikler hakkında.</span><span class="sxs-lookup"><span data-stu-id="45838-199">For more information, see the [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="45838-200">Telemetri işlemci (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="45838-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="45838-201">Telemetri işlemciler filtre ve yalnızca SDK portala göndermeden önce her bir telemetri öğeyi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="45838-201">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="45838-202">Yapabilecekleriniz [kendi telemetri işlemciler yazma](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="45838-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="45838-203">Uyarlamalı örnekleme telemetri işlemcisine (2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="45838-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="45838-204">Bu, varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="45838-204">This is enabled by default.</span></span> <span data-ttu-id="45838-205">Uygulamanız çok sayıda telemetri gönderirse, bu işlemci bazıları da kaldırır.</span><span class="sxs-lookup"><span data-stu-id="45838-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="45838-206">Parametre elde etmek için algoritma çalışır hedef sağlar.</span><span class="sxs-lookup"><span data-stu-id="45838-206">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="45838-207">Sunucunuz birden fazla makine bir küme ise, telemetri gerçek hacmi uygun şekilde çarpılır şekilde SDK her örneği bağımsız olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="45838-207">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="45838-208">[Örnekleme hakkında daha fazla bilgi](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="45838-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="45838-209">Sabit oran örnekleme telemetri işlemcisine (2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="45838-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="45838-210">Ayrıca bir standart olan [telemetri işlemci örnekleme](app-insights-api-filtering-sampling.md) (Başlangıç 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="45838-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="45838-211">Kanal parametreleri (Java)</span><span class="sxs-lookup"><span data-stu-id="45838-211">Channel parameters (Java)</span></span>
<span data-ttu-id="45838-212">Bu parametreler Java SDK'sı nasıl ve depolamak topladığı telemetri verilerini temizleme etkiler.</span><span class="sxs-lookup"><span data-stu-id="45838-212">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="45838-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="45838-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="45838-214">SDK'ın bellek içi depolamada depolanan telemetri öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="45838-214">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="45838-215">Bu sayıya ulaşıldığında, telemetri arabellek Temizlenen - diğer bir deyişle, telemetri öğeleri Application Insights sunucusuna gönderilir.</span><span class="sxs-lookup"><span data-stu-id="45838-215">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="45838-216">Min: 1</span><span class="sxs-lookup"><span data-stu-id="45838-216">Min: 1</span></span>
* <span data-ttu-id="45838-217">En fazla: 1000</span><span class="sxs-lookup"><span data-stu-id="45838-217">Max: 1000</span></span>
* <span data-ttu-id="45838-218">Varsayılan: 500</span><span class="sxs-lookup"><span data-stu-id="45838-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="45838-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="45838-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="45838-220">Ne sıklıkla bellekte depolamada depolanan veri (Application Insights gönderilen) kopyalanması belirler.</span><span class="sxs-lookup"><span data-stu-id="45838-220">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="45838-221">Min: 1</span><span class="sxs-lookup"><span data-stu-id="45838-221">Min: 1</span></span>
* <span data-ttu-id="45838-222">En fazla: 300</span><span class="sxs-lookup"><span data-stu-id="45838-222">Max: 300</span></span>
* <span data-ttu-id="45838-223">Varsayılan: 5</span><span class="sxs-lookup"><span data-stu-id="45838-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="45838-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="45838-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="45838-225">Yerel diskteki kalıcı depolama birimine ayrılan MB cinsinden maksimum boyutu belirler.</span><span class="sxs-lookup"><span data-stu-id="45838-225">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="45838-226">Bu depolama Application Insights uç noktasına aktarılacak başarısız kalıcı telemetri öğeleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="45838-226">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="45838-227">Depolama boyutu sağlandığında yeni telemetri öğeleri atılacak.</span><span class="sxs-lookup"><span data-stu-id="45838-227">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="45838-228">Min: 1</span><span class="sxs-lookup"><span data-stu-id="45838-228">Min: 1</span></span>
* <span data-ttu-id="45838-229">En fazla: 100</span><span class="sxs-lookup"><span data-stu-id="45838-229">Max: 100</span></span>
* <span data-ttu-id="45838-230">Varsayılan: 10</span><span class="sxs-lookup"><span data-stu-id="45838-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="45838-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="45838-231">InstrumentationKey</span></span>
<span data-ttu-id="45838-232">Bu, verilerinizi göründüğü Application Insights kaynağı belirler.</span><span class="sxs-lookup"><span data-stu-id="45838-232">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="45838-233">Genellikle, ayrı bir kaynak ayrı bir anahtarla her uygulamalarınız için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45838-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="45838-234">Farklı kaynaklara - uygulamanızdan sonuçları göndermek istiyorsanız, dinamik olarak - örneğin anahtar ayarlamak istiyorsanız, yapılandırma dosyasından anahtarı atlayın ve bunun yerine kodda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="45838-234">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="45838-235">Anahtar TelemetryClient tüm örnekler için ayarlamak için standart telemetri modüller de dahil olmak üzere ayarlayın anahtar TelemetryConfiguration.Active içinde.</span><span class="sxs-lookup"><span data-stu-id="45838-235">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="45838-236">Bu, bir ASP.NET hizmetinde global.aspx.cs gibi başlatma yöntemini yapın:</span><span class="sxs-lookup"><span data-stu-id="45838-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="45838-237">Yalnızca olayları belirli bir dizi farklı bir kaynağa göndermek istiyorsanız, bu anahtar için belirli bir TelemetryClient ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45838-237">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="45838-238">Yeni bir anahtar almak için [Application Insights portalında yeni bir kaynak oluşturmak][new].</span><span class="sxs-lookup"><span data-stu-id="45838-238">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="45838-239">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45838-239">Next steps</span></span>
<span data-ttu-id="45838-240">[API hakkında daha fazla bilgi][api].</span><span class="sxs-lookup"><span data-stu-id="45838-240">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
