---
title: ".NET izleme günlükleri Application ınsights'ta keşfedin"
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
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="19dc0-103">.NET izleme günlükleri Application ınsights'ta keşfedin</span><span class="sxs-lookup"><span data-stu-id="19dc0-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="19dc0-104">NLog, log4Net veya System.Diagnostics.Trace, ASP.NET uygulamanızda Tanılama izleme için kullanıyorsanız günlüklerinizi gönderilmesini sağlayabilirsiniz [Azure Application Insights][start], burada keşfedin aramak ve bunları.</span><span class="sxs-lookup"><span data-stu-id="19dc0-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="19dc0-105">Günlüklerinizi, böylece her kullanıcı isteği hizmeti ile ilişkilendirilmiş izlemeleri belirlemek ve diğer olayları ve özel durum raporları ile ilişkilendirmek, uygulamadan gelen telemetri ile birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="19dc0-106">Günlük yakalama modülü gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="19dc0-106">Do you need the log capture module?</span></span> <span data-ttu-id="19dc0-107">3. taraf günlükçüleri için yararlı bir bağdaştırıcı olduğundan, ancak NLog kullanmıyorsanız, log4Net veya System.Diagnostics.Trace, göz önünde bulundurun yalnızca arama [uygulama Öngörüler TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) doğrudan.</span><span class="sxs-lookup"><span data-stu-id="19dc0-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="19dc0-108">Uygulamanıza oturum yükleyin</span><span class="sxs-lookup"><span data-stu-id="19dc0-108">Install logging on your app</span></span>
<span data-ttu-id="19dc0-109">Seçilen günlük framework projenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="19dc0-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="19dc0-110">Bu app.config veya web.config bir girişe neden.</span><span class="sxs-lookup"><span data-stu-id="19dc0-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="19dc0-111">System.Diagnostics.Trace kullanıyorsanız, web.config dosyasına bir giriş eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="19dc0-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

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
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="19dc0-112">Application Insights'ın günlükleri toplamak için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="19dc0-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="19dc0-113">**[Application Insights projenize eklemek](app-insights-asp-net.md)**  bunu, henüz yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="19dc0-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="19dc0-114">Günlük Toplayıcı dahil etmek için bir seçenek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="19dc0-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="19dc0-115">Veya **yapılandırma Application Insights** Çözüm Gezgini'nde projenize sağ tarafından.</span><span class="sxs-lookup"><span data-stu-id="19dc0-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="19dc0-116">Seçeneğini **izleme koleksiyonu yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="19dc0-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="19dc0-117">*Application Insights menüsü veya günlük Toplayıcı seçeneği yok?*</span><span class="sxs-lookup"><span data-stu-id="19dc0-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="19dc0-118">Deneyin [sorun giderme](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="19dc0-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="19dc0-119">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="19dc0-119">Manual installation</span></span>
<span data-ttu-id="19dc0-120">Proje türü (örneğin Windows Masaüstü projesi) Application Insights yükleyici tarafından desteklenmiyor, bu yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="19dc0-121">Log4Net veya NLog kullanmayı planlıyorsanız, projenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="19dc0-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="19dc0-122">Çözüm Gezgini'nde, projenize sağ tıklayın ve seçin **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="19dc0-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="19dc0-123">"Application Insights" araması yapın</span><span class="sxs-lookup"><span data-stu-id="19dc0-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="19dc0-124">Uygun paket - aşağıdakilerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="19dc0-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="19dc0-125">Microsoft.ApplicationInsights.TraceListener (System.Diagnostics.Trace çağrıları yakalamak için)</span><span class="sxs-lookup"><span data-stu-id="19dc0-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="19dc0-126">Microsoft.ApplicationInsights.EventSourceListener (EventSource olaylarını yakalamak için)</span><span class="sxs-lookup"><span data-stu-id="19dc0-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="19dc0-127">Microsoft.ApplicationInsights.EtwListener (ETW olaylarını yakalamak için)</span><span class="sxs-lookup"><span data-stu-id="19dc0-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="19dc0-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="19dc0-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="19dc0-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="19dc0-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="19dc0-130">NuGet paketi gerekli derlemeleri yükler ve ayrıca web.config veya app.config değiştirir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="19dc0-131">Tanılama günlük çağrıları Ekle</span><span class="sxs-lookup"><span data-stu-id="19dc0-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="19dc0-132">System.Diagnostics.Trace kullanırsanız, tipik bir çağrı olacaktır:</span><span class="sxs-lookup"><span data-stu-id="19dc0-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="19dc0-133">Log4net veya NLog isterseniz:</span><span class="sxs-lookup"><span data-stu-id="19dc0-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="19dc0-134">EventSource olaylarını kullanma</span><span class="sxs-lookup"><span data-stu-id="19dc0-134">Using EventSource events</span></span>
<span data-ttu-id="19dc0-135">Yapılandırabileceğiniz [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) Application Insights izlemeleri olarak gönderilmesini olaylar.</span><span class="sxs-lookup"><span data-stu-id="19dc0-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="19dc0-136">İlk olarak, yükleme `Microsoft.ApplicationInsights.EventSourceListener` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="19dc0-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="19dc0-137">Daha sonra Düzenle `TelemetryModules` bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.</span><span class="sxs-lookup"><span data-stu-id="19dc0-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="19dc0-138">Her bir kaynağı için şu parametreleri ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="19dc0-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="19dc0-139">`Name`Toplanacak EventSource adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="19dc0-140">`Level`Toplanacak günlüğe kaydetme düzeyini belirtir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="19dc0-141">Aşağıdakilerden biri olabilir `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="19dc0-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="19dc0-142">`Keywords`(İsteğe bağlı) kullanmak için anahtar sözcükler birleşimleri tamsayı değerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="19dc0-143">DiagnosticSource olaylarını kullanma</span><span class="sxs-lookup"><span data-stu-id="19dc0-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="19dc0-144">Yapılandırabileceğiniz [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) Application Insights izlemeleri olarak gönderilmesini olaylar.</span><span class="sxs-lookup"><span data-stu-id="19dc0-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="19dc0-145">İlk olarak, yükleme [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="19dc0-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="19dc0-146">Daha sonra Düzenle `TelemetryModules` bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.</span><span class="sxs-lookup"><span data-stu-id="19dc0-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="19dc0-147">İzlemek istediğiniz her DiagnosticSource için olan bir giriş eklemek `Name` özniteliği, DiagnosticSource adına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="19dc0-148">ETW olayları kullanma</span><span class="sxs-lookup"><span data-stu-id="19dc0-148">Using ETW events</span></span>
<span data-ttu-id="19dc0-149">Application Insights izlemeleri olarak gönderilmesini ETW olayları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19dc0-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="19dc0-150">İlk olarak, yükleme `Microsoft.ApplicationInsights.EtwCollector` NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="19dc0-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="19dc0-151">Daha sonra Düzenle `TelemetryModules` bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.</span><span class="sxs-lookup"><span data-stu-id="19dc0-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="19dc0-152">SDK barındırma işlemi, "Performans günlüğü kullanıcıları" veya yöneticileri üyesi olan bir kimlik altında çalışıyorsa, ETW olayları yalnızca toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="19dc0-153">Her bir kaynağı için şu parametreleri ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="19dc0-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="19dc0-154">`ProviderName`Toplanacak ETW sağlayıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="19dc0-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="19dc0-155">`ProviderGuid`Toplama ETW sağlayıcı GUID belirtir yerine kullanılabilir `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="19dc0-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="19dc0-156">`Level`Toplanacak günlüğe kaydetme düzeyi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="19dc0-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="19dc0-157">Aşağıdakilerden biri olabilir `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span><span class="sxs-lookup"><span data-stu-id="19dc0-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="19dc0-158">`Keywords`(İsteğe bağlı) kullanmak için anahtar sözcüğü birleşimleri tamsayı değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="19dc0-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="19dc0-159">Kullanarak doğrudan API izleme</span><span class="sxs-lookup"><span data-stu-id="19dc0-159">Using the Trace API directly</span></span>
<span data-ttu-id="19dc0-160">Application Insights izleme API doğrudan çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="19dc0-161">Günlüğe kaydetme bağdaştırıcıları bu API'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-161">The logging adapters use this API.</span></span>

<span data-ttu-id="19dc0-162">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="19dc0-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="19dc0-163">TrackTrace avantajı, iletide oldukça uzun veri koyabilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="19dc0-164">Örneğin, gönderme verisi kodlayın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="19dc0-165">Ayrıca, bir önem düzeyi iletinize ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19dc0-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="19dc0-166">Ve diğer telemetri gibi filtre veya arama izlemeleri farklı kümeleri için yardımcı olmak için kullanabileceğiniz özellik değerlerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19dc0-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="19dc0-167">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="19dc0-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="19dc0-168">Bu, içinde sağlayacağı [arama][diagnostic], belirli bir veritabanı ile ilgili belirli bir önemde tüm iletileri kolayca filtrelemek için.</span><span class="sxs-lookup"><span data-stu-id="19dc0-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="19dc0-169">Günlüklerinizi keşfedin</span><span class="sxs-lookup"><span data-stu-id="19dc0-169">Explore your logs</span></span>
<span data-ttu-id="19dc0-170">Uygulamanızı, ya da hata ayıklama modunda çalıştırmak veya dinamik dağıtın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="19dc0-171">Uygulamanızın genel bakış dikey penceresinde de [Application Insights portalındaki][portal], seçin [arama][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="19dc0-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![Application Insights'ta arama seçin](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Arama](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="19dc0-174">Örneğin yapabilecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="19dc0-174">You can, for example:</span></span>

* <span data-ttu-id="19dc0-175">Günlük izlemelerini veya belirli özelliklere sahip öğeleri Filtrele</span><span class="sxs-lookup"><span data-stu-id="19dc0-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="19dc0-176">Belirli bir öğeyi ayrıntılı inceleyin.</span><span class="sxs-lookup"><span data-stu-id="19dc0-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="19dc0-177">Aynı kullanıcı istekle ilgili diğer telemetriyi Bul (diğer bir deyişle, aynı Operationıd ile)</span><span class="sxs-lookup"><span data-stu-id="19dc0-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="19dc0-178">Bu sayfa yapılandırmasını sık kullanılan olarak Kaydet</span><span class="sxs-lookup"><span data-stu-id="19dc0-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="19dc0-179">**Örnekleme.**</span><span class="sxs-lookup"><span data-stu-id="19dc0-179">**Sampling.**</span></span> <span data-ttu-id="19dc0-180">Uygulamanız çok miktarda veri gönderiyorsa ve ASP.NET sürüm 2.0.0-beta3 veya daha sonraki uygulamalar için Application Insights SDK kullanıyorsanız, uyarlamalı örnekleme özelliği telemetrenizin yalnızca yüzdesini çalıştırır ve gönderir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="19dc0-181">Örnekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="19dc0-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="19dc0-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19dc0-182">Next steps</span></span>
<span data-ttu-id="19dc0-183">[Hataları ve ASP.NET özel durumları tanılama][exceptions]</span><span class="sxs-lookup"><span data-stu-id="19dc0-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="19dc0-184">[Arama hakkında daha fazla bilgi][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="19dc0-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="19dc0-185">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="19dc0-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="19dc0-186">Bunu nasıl yapabilirim Java için?</span><span class="sxs-lookup"><span data-stu-id="19dc0-186">How do I do this for Java?</span></span>
<span data-ttu-id="19dc0-187">Kullanım [Java günlük bağdaştırıcıları](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="19dc0-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="19dc0-188">Proje bağlam menüsünde Application Insights seçeneği yoktur</span><span class="sxs-lookup"><span data-stu-id="19dc0-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="19dc0-189">Application Insights araçları bu geliştirme makinede yüklü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="19dc0-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="19dc0-190">Visual Studio menü Araçlar, uzantılar ve güncelleştirmeler, için Application Insights araçları arayın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="19dc0-191">Yüklü sekmesinde değilse, çevrimiçi sekmesini açın ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="19dc0-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="19dc0-192">Bu proje Application Insights araçları tarafından desteklenmeyen bir türde olabilir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="19dc0-193">Kullanım [el ile yükleme](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="19dc0-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="19dc0-194">Hiçbir yapılandırma aracı günlük bağdaştırıcısı seçeneğinde</span><span class="sxs-lookup"><span data-stu-id="19dc0-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="19dc0-195">Günlüğe kaydetme framework yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="19dc0-196">System.Diagnostics.Trace kullanıyorsanız, emin [içinde yapılandırılmış `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="19dc0-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="19dc0-197">Application Insights'ın en son sürümünü var mı?</span><span class="sxs-lookup"><span data-stu-id="19dc0-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="19dc0-198">Visual Studio'da **Araçları** menüsünde seçin **Uzantılar ve güncelleştirmeler**, açarak **güncelleştirmeleri** sekmesi. Geliştirici analiz araçları vardır, güncelleştirmek için'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="19dc0-199"><a name="emptykey"></a>"İzleme anahtarını boş olamaz" hata alıyorum</span><span class="sxs-lookup"><span data-stu-id="19dc0-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="19dc0-200">Application Insights yüklemeden günlük bağdaştırıcısı Nuget paketi yüklü gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="19dc0-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="19dc0-201">Çözüm Gezgini'nde sağ `ApplicationInsights.config` ve **güncelleştirme Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="19dc0-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="19dc0-202">Azure'da oturum açmanız başvurulmasını bir iletişim kutusu elde edersiniz ve ya da bir Application Insights kaynağı oluşturun veya var olan bir yeniden kullanın.</span><span class="sxs-lookup"><span data-stu-id="19dc0-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="19dc0-203">Bu sorununu çözer.</span><span class="sxs-lookup"><span data-stu-id="19dc0-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="19dc0-204">Tanılama arama, ancak olmayan diğer olayları izlemelerini görmek için</span><span class="sxs-lookup"><span data-stu-id="19dc0-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="19dc0-205">Bu, bazen tüm olayları ve istek ardışık düzenine ulaşması biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="19dc0-206"><a name="limits"></a>Ne kadar veri tutulur?</span><span class="sxs-lookup"><span data-stu-id="19dc0-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="19dc0-207">Pek çok etken korunur veri miktarını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="19dc0-208">Bkz: [sınırları](app-insights-api-custom-events-metrics.md#limits) daha fazla bilgi için müşteri olay ölçümleri sayfasının bölümünde.</span><span class="sxs-lookup"><span data-stu-id="19dc0-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="19dc0-209">Bazı t beklediğiniz günlük girdileri görüyorum değil</span><span class="sxs-lookup"><span data-stu-id="19dc0-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="19dc0-210">Uygulamanız çok miktarda veri gönderiyorsa ve ASP.NET sürüm 2.0.0-beta3 veya daha sonraki uygulamalar için Application Insights SDK kullanıyorsanız, uyarlamalı örnekleme özelliği telemetrenizin yalnızca yüzdesini çalıştırır ve gönderir.</span><span class="sxs-lookup"><span data-stu-id="19dc0-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="19dc0-211">Örnekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="19dc0-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="19dc0-212"><a name="add"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19dc0-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="19dc0-213">[Kullanılabilirlik ve yanıt hızını testleri ayarlama][availability]</span><span class="sxs-lookup"><span data-stu-id="19dc0-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="19dc0-214">[Sorun giderme][qna]</span><span class="sxs-lookup"><span data-stu-id="19dc0-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
