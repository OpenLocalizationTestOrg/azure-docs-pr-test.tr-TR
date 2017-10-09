---
title: "Application Insights'ta aaaExplore .NET izleme günlükleri"
description: "İzleme, NLog veya Log4Net ile oluşturulan günlükleri arayın."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="ab6dd-103">.NET izleme günlükleri Application ınsights'ta keşfedin</span><span class="sxs-lookup"><span data-stu-id="ab6dd-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="ab6dd-104">NLog, log4Net veya System.Diagnostics.Trace, ASP.NET uygulamanızda Tanılama izleme için kullanırsanız, çok gönderilen günlüklerinizi olabilir[Azure Application Insights][start], burada keşfedin aramak ve bunları.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="ab6dd-105">Günlüklerinizi hello ile diğer birleştirilecek tanımlayabilirsiniz böylece, uygulamadan gelen telemetri hello her kullanıcı isteği hizmeti ile ilişkilendirilmiş izlemeleri ve diğer olayları ve özel durum raporları ile ilişkilendirilmesi.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="ab6dd-106">Merhaba günlük yakalama modülü gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="ab6dd-106">Do you need hello log capture module?</span></span> <span data-ttu-id="ab6dd-107">3. taraf günlükçüleri için yararlı bir bağdaştırıcı olduğundan, ancak NLog kullanmıyorsanız, log4Net veya System.Diagnostics.Trace, göz önünde bulundurun yalnızca arama [uygulama Öngörüler TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) doğrudan.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="ab6dd-108">Uygulamanıza oturum yükleyin</span><span class="sxs-lookup"><span data-stu-id="ab6dd-108">Install logging on your app</span></span>
<span data-ttu-id="ab6dd-109">Seçilen günlük framework projenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="ab6dd-110">Bu app.config veya web.config bir girişe neden.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="ab6dd-111">System.Diagnostics.Trace kullanıyorsanız, tooadd bir giriş tooweb.config gerekir:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="ab6dd-112">Application Insights toocollect günlüklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ab6dd-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="ab6dd-113">**[Application Insights tooyour projesi eklemek](app-insights-asp-net.md)**  bunu, henüz yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="ab6dd-114">Bir seçenek tooinclude hello günlük Toplayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="ab6dd-115">Veya **yapılandırma Application Insights** Çözüm Gezgini'nde projenize sağ tarafından.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="ab6dd-116">Çok olarak Hello seçeneğini**izleme koleksiyonu yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="ab6dd-117">*Application Insights menüsü veya günlük Toplayıcı seçeneği yok?*</span><span class="sxs-lookup"><span data-stu-id="ab6dd-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="ab6dd-118">Deneyin [sorun giderme](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ab6dd-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="ab6dd-119">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="ab6dd-119">Manual installation</span></span>
<span data-ttu-id="ab6dd-120">Proje türü hello Application Insights Yükleyici (örneğin Windows Masaüstü projesi) tarafından desteklenmiyor, bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="ab6dd-121">Toouse log4Net veya NLog düşünüyorsanız, projenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="ab6dd-122">Çözüm Gezgini'nde, projenize sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="ab6dd-123">"Application Insights" araması yapın</span><span class="sxs-lookup"><span data-stu-id="ab6dd-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="ab6dd-124">Merhaba uygun paket - aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="ab6dd-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace çağrı)</span><span class="sxs-lookup"><span data-stu-id="ab6dd-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="ab6dd-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource olaylarını)</span><span class="sxs-lookup"><span data-stu-id="ab6dd-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="ab6dd-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW olayları)</span><span class="sxs-lookup"><span data-stu-id="ab6dd-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="ab6dd-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="ab6dd-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="ab6dd-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="ab6dd-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="ab6dd-130">Merhaba NuGet paketi hello gerekli derlemeleri yükler ve ayrıca web.config veya app.config değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="ab6dd-131">Tanılama günlük çağrıları Ekle</span><span class="sxs-lookup"><span data-stu-id="ab6dd-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="ab6dd-132">System.Diagnostics.Trace kullanırsanız, tipik bir çağrı olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="ab6dd-133">Log4net veya NLog isterseniz:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="ab6dd-134">EventSource olaylarını kullanma</span><span class="sxs-lookup"><span data-stu-id="ab6dd-134">Using EventSource events</span></span>
<span data-ttu-id="ab6dd-135">Yapılandırabileceğiniz [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) olayları gönderilen toobe tooApplication Öngörüler izlemeleri olarak.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="ab6dd-136">İlk olarak, hello yükleyin `Microsoft.ApplicationInsights.EventSourceListener` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="ab6dd-137">Daha sonra Düzenle `TelemetryModules` hello bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="ab6dd-138">Her bir kaynağı için şu parametreler hello ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="ab6dd-139">`Name`Merhaba EventSource toocollect Hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="ab6dd-140">`Level`günlüğe kaydetme düzeyi toocollect hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="ab6dd-141">Aşağıdakilerden biri olabilir `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="ab6dd-142">`Keywords`(İsteğe bağlı) anahtar sözcükleri birleşimleri toouse hello tamsayı değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="ab6dd-143">DiagnosticSource olaylarını kullanma</span><span class="sxs-lookup"><span data-stu-id="ab6dd-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="ab6dd-144">Yapılandırabileceğiniz [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) olayları gönderilen toobe tooApplication Öngörüler izlemeleri olarak.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="ab6dd-145">İlk olarak, hello yükleyin [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="ab6dd-146">Merhaba Düzenle `TelemetryModules` hello bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="ab6dd-147">Tootrace, istediğiniz her DiagnosticSource için hello olan bir giriş eklemek `Name` özniteliği, DiagnosticSource toohello adını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="ab6dd-148">ETW olayları kullanma</span><span class="sxs-lookup"><span data-stu-id="ab6dd-148">Using ETW events</span></span>
<span data-ttu-id="ab6dd-149">ETW olayları toobe tooApplication Öngörüler izlemeleri gönderilen yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="ab6dd-150">İlk olarak, hello yükleyin `Microsoft.ApplicationInsights.EtwCollector` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="ab6dd-151">Daha sonra Düzenle `TelemetryModules` hello bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="ab6dd-152">Merhaba işlem barındırma hello SDK'sı, "Performans günlüğü kullanıcıları" veya yöneticileri üyesi olan bir kimlik altında çalışıyorsa, ETW olayları yalnızca toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="ab6dd-153">Her bir kaynağı için şu parametreler hello ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="ab6dd-154">`ProviderName`Merhaba ETW sağlayıcı toocollect Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="ab6dd-155">`ProviderGuid`Merhaba hello ETW sağlayıcı toocollect GUİD'si belirtir yerine kullanılabilir `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="ab6dd-156">`Level`günlüğe kaydetme düzeyi toocollect hello ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="ab6dd-157">Aşağıdakilerden biri olabilir `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="ab6dd-158">`Keywords`(İsteğe bağlı) kümeleri anahtar sözcüğü birleşimleri toouse tamsayı değerini hello.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="ab6dd-159">Merhaba izleme API kullanarak doğrudan</span><span class="sxs-lookup"><span data-stu-id="ab6dd-159">Using hello Trace API directly</span></span>
<span data-ttu-id="ab6dd-160">Merhaba Application Insights izleme API doğrudan çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="ab6dd-161">Merhaba günlük bağdaştırıcıları bu API'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="ab6dd-162">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="ab6dd-163">TrackTrace avantajı hello iletisinde oldukça uzun veri koyabilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="ab6dd-164">Örneğin, gönderme verisi kodlayın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="ab6dd-165">Ayrıca, bir önem düzeyi tooyour ileti ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="ab6dd-166">Ve diğer telemetri gibi toohelp filtre veya arama izlemeleri farklı kümeleri için kullanabileceğiniz özellik değerlerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="ab6dd-167">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="ab6dd-168">Bu, içinde sağlayacağı [arama][diagnostic], tooeasily filtre tooa belirli veritabanı ile ilgili belirli bir önemde tüm hello iletilerinin çıkışı.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="ab6dd-169">Günlüklerinizi keşfedin</span><span class="sxs-lookup"><span data-stu-id="ab6dd-169">Explore your logs</span></span>
<span data-ttu-id="ab6dd-170">Uygulamanızı, ya da hata ayıklama modunda çalıştırmak veya dinamik dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="ab6dd-171">Uygulamanızın genel bakış dikey penceresinde de [hello Application Insights portalındaki][portal], seçin [arama][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="ab6dd-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Application Insights'ta arama seçin](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Arama](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="ab6dd-174">Örneğin yapabilecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="ab6dd-174">You can, for example:</span></span>

* <span data-ttu-id="ab6dd-175">Günlük izlemelerini veya belirli özelliklere sahip öğeleri Filtrele</span><span class="sxs-lookup"><span data-stu-id="ab6dd-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="ab6dd-176">Belirli bir öğeyi ayrıntılı inceleyin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="ab6dd-177">Toohello ilgili diğer telemetriyi Bul aynı kullanıcı isteği (diğer bir deyişle, ile aynı hello Operationıd)</span><span class="sxs-lookup"><span data-stu-id="ab6dd-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="ab6dd-178">Bu sayfanın Hello yapılandırma sık kullanılan olarak Kaydet</span><span class="sxs-lookup"><span data-stu-id="ab6dd-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="ab6dd-179">**Örnekleme.**</span><span class="sxs-lookup"><span data-stu-id="ab6dd-179">**Sampling.**</span></span> <span data-ttu-id="ab6dd-180">Uygulamanız çok miktarda veri gönderir ve hello Application Insights SDK'sı ASP.NET sürüm 2.0.0-beta3 veya üzeri kullanıyorsanız, hello Uyarlamalı örnekleme özelliği çalışır ve yalnızca telemetrinizi yüzdesi gönderin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="ab6dd-181">Örnekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="ab6dd-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab6dd-182">Next steps</span></span>
<span data-ttu-id="ab6dd-183">[Hataları ve ASP.NET özel durumları tanılama][exceptions]</span><span class="sxs-lookup"><span data-stu-id="ab6dd-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="ab6dd-184">[Arama hakkında daha fazla bilgi][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="ab6dd-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ab6dd-185">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ab6dd-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="ab6dd-186">Bunu nasıl yapabilirim Java için?</span><span class="sxs-lookup"><span data-stu-id="ab6dd-186">How do I do this for Java?</span></span>
<span data-ttu-id="ab6dd-187">Kullanım hello [Java günlük bağdaştırıcıları](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ab6dd-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="ab6dd-188">Merhaba proje bağlam menüsünde Application Insights seçeneği yoktur</span><span class="sxs-lookup"><span data-stu-id="ab6dd-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="ab6dd-189">Application Insights araçları bu geliştirme makinede yüklü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="ab6dd-190">Visual Studio menü Araçlar, uzantılar ve güncelleştirmeler, için Application Insights araçları arayın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="ab6dd-191">Merhaba yüklü sekmesinde değilse, çevrimiçi hello sekmesini açın ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="ab6dd-192">Bu proje Application Insights araçları tarafından desteklenmeyen bir türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="ab6dd-193">Kullanım [el ile yükleme](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="ab6dd-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="ab6dd-194">Merhaba Yapılandırma aracında günlük bağdaştırıcısı seçeneği</span><span class="sxs-lookup"><span data-stu-id="ab6dd-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="ab6dd-195">Tooinstall hello günlük önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="ab6dd-196">System.Diagnostics.Trace kullanıyorsanız, emin [içinde yapılandırılmış `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab6dd-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="ab6dd-197">Application Insights en son sürümünü hello var mı?</span><span class="sxs-lookup"><span data-stu-id="ab6dd-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="ab6dd-198">Visual Studio'da **Araçları** menüsünde seçin **Uzantılar ve güncelleştirmeler**ve açık hello **güncelleştirmeleri** sekmesi. Geliştirici analiz araçları vardır, tooupdate'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="ab6dd-199"><a name="emptykey"></a>"İzleme anahtarını boş olamaz" hata alıyorum</span><span class="sxs-lookup"><span data-stu-id="ab6dd-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="ab6dd-200">Application Insights yüklemeden bağdaştırıcısı Nuget paketi günlüğü hello yüklü gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="ab6dd-201">Çözüm Gezgini'nde sağ `ApplicationInsights.config` ve **güncelleştirme Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="ab6dd-202">Toosign, başvurulmasını bir iletişim kutusu içinde tooAzure elde edersiniz ve ya da bir Application Insights kaynağı oluşturun veya var olan bir yeniden kullanın.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="ab6dd-203">Bu sorununu çözer.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="ab6dd-204">I tanılama arama içindeki görebilir, ancak diğer olayları hello değil</span><span class="sxs-lookup"><span data-stu-id="ab6dd-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="ab6dd-205">Bu, bazen hello ardışık düzeninden tüm hello olayları ve istekleri tooget için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="ab6dd-206"><a name="limits"></a>Ne kadar veri tutulur?</span><span class="sxs-lookup"><span data-stu-id="ab6dd-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="ab6dd-207">Pek çok etken hello korunur veri miktarını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="ab6dd-208">Merhaba bkz [sınırları](app-insights-api-custom-events-metrics.md#limits) sayfasının bölümünde hello müşteri olay ölçümleri daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="ab6dd-209">Bazı t beklediğiniz hello günlük girdileri görüyorum değil</span><span class="sxs-lookup"><span data-stu-id="ab6dd-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="ab6dd-210">Uygulamanız çok miktarda veri gönderir ve hello Application Insights SDK'sı ASP.NET sürüm 2.0.0-beta3 veya üzeri kullanıyorsanız, hello Uyarlamalı örnekleme özelliği çalışır ve yalnızca telemetrinizi yüzdesi gönderin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="ab6dd-211">Örnekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ab6dd-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="ab6dd-212"><a name="add"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab6dd-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="ab6dd-213">[Kullanılabilirlik ve yanıt hızını testleri ayarlama][availability]</span><span class="sxs-lookup"><span data-stu-id="ab6dd-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="ab6dd-214">[Sorun giderme][qna]</span><span class="sxs-lookup"><span data-stu-id="ab6dd-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
