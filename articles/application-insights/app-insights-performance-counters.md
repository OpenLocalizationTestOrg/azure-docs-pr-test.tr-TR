---
title: "Application Insights aaaPerformance sayaçları | Microsoft Docs"
description: "Sistem ve Application Insights özel .NET performans sayaçları izleyin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a><span data-ttu-id="a4244-103">Application Insights sistem performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="a4244-103">System performance counters in Application Insights</span></span>
<span data-ttu-id="a4244-104">Windows, çok çeşitli sağlar [performans sayaçları](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) CPU doluluğu, bellek, disk ve ağ kullanımı gibi.</span><span class="sxs-lookup"><span data-stu-id="a4244-104">Windows provides a wide variety of [performance counters](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) such as CPU occupancy, memory, disk, and network usage.</span></span> <span data-ttu-id="a4244-105">Ayrıca kendi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4244-105">You can also define your own.</span></span> <span data-ttu-id="a4244-106">[Application Insights](app-insights-overview.md) uygulamanız IIS altında bir şirket içi ana bilgisayar veya sanal makine toowhich, çalışıyorsa, bu performans sayaçlarını yönetimsel erişime sahip gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="a4244-106">[Application Insights](app-insights-overview.md) can show these performance counters if your application is running under IIS on an on-premises host or virtual machine toowhich you have administrative access.</span></span> <span data-ttu-id="a4244-107">Merhaba grafikleri hello kaynakları kullanılabilir tooyour dinamik uygulama belirtmek ve sunucu örnekleri arasında tooidentify dengesiz yük yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a4244-107">hello charts indicate hello resources available tooyour live application, and can help tooidentify unbalanced load between server instances.</span></span>

<span data-ttu-id="a4244-108">Performans sayaçları, bu kesimleri sunucu örneği tarafından bir tablo içeren hello sunucuları dikey penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="a4244-108">Performance counters appear in hello Servers blade, which includes a table that segments by server instance.</span></span>

![Application Insights'ta bildirilen performans sayaçları](./media/app-insights-performance-counters/counters-by-server-instance.png)

<span data-ttu-id="a4244-110">(Performans sayaçlarını Azure Web uygulamaları için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="a4244-110">(Performance counters aren't available for Azure Web Apps.</span></span> <span data-ttu-id="a4244-111">Ancak [Azure tanılama tooApplication Öngörüler Gönder](app-insights-azure-diagnostics.md).)</span><span class="sxs-lookup"><span data-stu-id="a4244-111">But you can [send Azure Diagnostics tooApplication Insights](app-insights-azure-diagnostics.md).)</span></span>

## <a name="view-counters"></a><span data-ttu-id="a4244-112">Sayaçları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="a4244-112">View counters</span></span>
<span data-ttu-id="a4244-113">Merhaba sunucuları dikey varsayılan bir performans sayaçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4244-113">hello Servers blade shows a default set of performance counters.</span></span> 

<span data-ttu-id="a4244-114">toosee diğer sayaçları hello sunucuları dikey penceresinde hello grafikleri düzenleyebilir veya yeni bir [ölçüm Gezgini](app-insights-metrics-explorer.md) dikey ve yeni grafikler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4244-114">toosee other counters, either edit hello charts on hello Servers blade, or open a new [Metrics Explorer](app-insights-metrics-explorer.md) blade and add new charts.</span></span> 

<span data-ttu-id="a4244-115">bir grafiği düzenlediğinizde hello kullanılabilir sayaçlar ölçümleri listelenir.</span><span class="sxs-lookup"><span data-stu-id="a4244-115">hello available counters are listed as metrics when you edit a chart.</span></span>

![Application Insights'ta bildirilen performans sayaçları](./media/app-insights-performance-counters/choose-performance-counters.png)

<span data-ttu-id="a4244-117">tek bir yerde tüm en yararlı grafikler toosee oluşturma bir [Pano](app-insights-dashboards.md) ve tooit sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="a4244-117">toosee all your most useful charts in one place, create a [dashboard](app-insights-dashboards.md) and pin them tooit.</span></span>

## <a name="add-counters"></a><span data-ttu-id="a4244-118">Sayaç ekleme</span><span class="sxs-lookup"><span data-stu-id="a4244-118">Add counters</span></span>
<span data-ttu-id="a4244-119">İstediğiniz hello performans sayacı hello ölçümleri listesinde gösterilen değil, hello Application Insights SDK'sı web sunucunuz toplama değil çünkü olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a4244-119">If hello performance counter you want isn't shown in hello list of metrics, that's because hello Application Insights SDK isn't collecting it in your web server.</span></span> <span data-ttu-id="a4244-120">Toodo şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4244-120">You can configure it toodo so.</span></span>

1. <span data-ttu-id="a4244-121">Hangi sayaçları hello sunucuda bu PowerShell komutunu kullanarak sunucunuzun kullanılabilir olduğunu bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4244-121">Find out what counters are available in your server by using this PowerShell command at hello server:</span></span>
   
    `Get-Counter -ListSet *`
   
    <span data-ttu-id="a4244-122">(Bkz [ `Get-Counter` ](https://technet.microsoft.com/library/hh849685.aspx).)</span><span class="sxs-lookup"><span data-stu-id="a4244-122">(See [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)</span></span>
2. <span data-ttu-id="a4244-123">Applicationınsights.config açın.</span><span class="sxs-lookup"><span data-stu-id="a4244-123">Open ApplicationInsights.config.</span></span>
   
   * <span data-ttu-id="a4244-124">Application Insights tooyour uygulama geliştirme sırasında eklediyseniz, projenizde Applicationınsights.config düzenleyin ve yeniden dağıtın tooyour sunucuları.</span><span class="sxs-lookup"><span data-stu-id="a4244-124">If you added Application Insights tooyour app during development, edit ApplicationInsights.config in your project, and then re-deploy it tooyour servers.</span></span>
   * <span data-ttu-id="a4244-125">Çalışma zamanında Durum İzleyicisi tooinstrument bir web uygulaması kullandıysanız, IIS'de hello uygulamasının hello kök dizininde Applicationınsights.config bulun.</span><span class="sxs-lookup"><span data-stu-id="a4244-125">If you used Status Monitor tooinstrument a web app at runtime, find ApplicationInsights.config in hello root directory of hello app in IIS.</span></span> <span data-ttu-id="a4244-126">Var. her sunucu örneğinde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a4244-126">Update it there in each server instance.</span></span>
3. <span data-ttu-id="a4244-127">Merhaba performans Toplayıcı yönergesi düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="a4244-127">Edit hello performance collector directive:</span></span>
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

<span data-ttu-id="a4244-128">Standart sayaçları hem olanlar kendiniz uyguladık yakalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4244-128">You can capture both standard counters and those you have implemented yourself.</span></span> <span data-ttu-id="a4244-129">`\Objects\Processes`Standart bir sayaç örneği tüm Windows sistemlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a4244-129">`\Objects\Processes` is an example of a standard counter, available on all Windows systems.</span></span> <span data-ttu-id="a4244-130">`\Sales(photo)\# Items Sold`bir web hizmeti uygulanan özel bir sayaç örneğidir.</span><span class="sxs-lookup"><span data-stu-id="a4244-130">`\Sales(photo)\# Items Sold` is an example of a custom counter that might be implemented in a web service.</span></span> 

<span data-ttu-id="a4244-131">Merhaba biçimi `\Category(instance)\Counter"`, veya örnekleri yok kategoriler, sadece `\Category\Counter`.</span><span class="sxs-lookup"><span data-stu-id="a4244-131">hello format is `\Category(instance)\Counter"`, or for categories that don't have instances, just `\Category\Counter`.</span></span>

<span data-ttu-id="a4244-132">`ReportAs`Eşleşmeyen sayaç adları için gerekli olan `[a-zA-Z()/-_ \.]+` -diğer bir deyişle, ayarlar aşağıdaki hello karakterler içerir: harfler, köşeli ayraçlar, eğik çizgi, tire, alt çizgi, boşluk, yuvarlak nokta.</span><span class="sxs-lookup"><span data-stu-id="a4244-132">`ReportAs` is required for counter names that do not match `[a-zA-Z()/-_ \.]+` - that is, they contain characters that are not in hello following sets: letters, round brackets, forward slash, hyphen, underscore, space, dot.</span></span>

<span data-ttu-id="a4244-133">Bir örnek belirtirseniz, bir boyut "CounterInstanceName" hello, ölçüm raporlanan toplanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a4244-133">If you specify an instance, it will be collected as a dimension "CounterInstanceName" of hello reported metric.</span></span>

### <a name="collecting-performance-counters-in-code"></a><span data-ttu-id="a4244-134">Kodda performans sayaçlarını toplama</span><span class="sxs-lookup"><span data-stu-id="a4244-134">Collecting performance counters in code</span></span>
<span data-ttu-id="a4244-135">toocollect sistem performans sayaçları ve tooApplication Öngörüler göndermek, aşağıdaki hello parçacığı uyum sağlayabilir:</span><span class="sxs-lookup"><span data-stu-id="a4244-135">toocollect system performance counters and send them tooApplication Insights, you can adapt hello snippet below:</span></span>


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

<span data-ttu-id="a4244-136">Veya yapabileceğiniz Merhaba, oluşturduğunuz özel ölçümleri ile aynı anlama:</span><span class="sxs-lookup"><span data-stu-id="a4244-136">Or you can do hello same thing with custom metrics you created:</span></span>

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a><span data-ttu-id="a4244-137">Analytics performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="a4244-137">Performance counters in Analytics</span></span>
<span data-ttu-id="a4244-138">Arama ve performans sayacı raporlarda görüntüleme [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="a4244-138">You can search and display performance counter reports in [Analytics](app-insights-analytics.md).</span></span>

<span data-ttu-id="a4244-139">Merhaba **performanceCounters** şeması sunan hello `category`, `counter` adı ve `instance` her performans sayacı adı.</span><span class="sxs-lookup"><span data-stu-id="a4244-139">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span>  <span data-ttu-id="a4244-140">Telemetri Hello her uygulama için yalnızca bu uygulama için hello sayaçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a4244-140">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="a4244-141">Örneğin, toosee hangi sayaçları kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="a4244-141">For example, toosee what counters are available:</span></span> 

![Application Insights analytics performans sayaçları](./media/app-insights-performance-counters/analytics-performance-counters.png)

<span data-ttu-id="a4244-143">('Instance' burada toohello performans sayacı örneği başvuruyor, rol veya sunucu makine örneğini hello değil.</span><span class="sxs-lookup"><span data-stu-id="a4244-143">('Instance' here refers toohello performance counter instance,  not hello role or server machine instance.</span></span> <span data-ttu-id="a4244-144">Merhaba performans sayacı örneği adı genellikle sayaçları işlemci zamanı gibi hello işlem veya uygulama tarafından hello adı kesim.)</span><span class="sxs-lookup"><span data-stu-id="a4244-144">hello performance counter instance name typically segments counters such as processor time by hello name of hello process or application.)</span></span>

<span data-ttu-id="a4244-145">bir grafik hello son dönemde üzerinden kullanılabilir belleğin tooget:</span><span class="sxs-lookup"><span data-stu-id="a4244-145">tooget a chart of available memory over hello recent period:</span></span> 

![Application Insights analytics'te bellek timechart](./media/app-insights-performance-counters/analytics-available-memory.png)

<span data-ttu-id="a4244-147">Gibi diğer telemetri **performanceCounters** de bir sütuna sahip `cloud_RoleInstance` uygulamanızı çalıştıran hello ana bilgisayar sunucu örneğinin hello kimliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4244-147">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host server instance on which your app is running.</span></span> <span data-ttu-id="a4244-148">Örneğin, toocompare hello uygulamanızın performansı ile Merhaba farklı makinelerde:</span><span class="sxs-lookup"><span data-stu-id="a4244-148">For example, toocompare hello performance of your app on hello different machines:</span></span> 

![Performans rol örneğinde Application Insights tarafından analiz bölümlenmiş.](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a><span data-ttu-id="a4244-150">ASP.NET ve Application Insights sayılar</span><span class="sxs-lookup"><span data-stu-id="a4244-150">ASP.NET and Application Insights counts</span></span>
<span data-ttu-id="a4244-151">*Hello hello özel durum oranı ve özel durumları ölçümleri arasındaki fark nedir?*</span><span class="sxs-lookup"><span data-stu-id="a4244-151">*What's hello difference between hello Exception rate and Exceptions metrics?*</span></span>

* <span data-ttu-id="a4244-152">*Özel durum oranı* bir sistem performans sayacı.</span><span class="sxs-lookup"><span data-stu-id="a4244-152">*Exception rate* is a system performance counter.</span></span> <span data-ttu-id="a4244-153">Merhaba CLR tüm işlenmiş hello ve oluşturulan ve hello toplam bir örnekleme aralığı içinde hello aralığı hello uzunluğu ile böler işlenmeyen özel durumları sayar.</span><span class="sxs-lookup"><span data-stu-id="a4244-153">hello CLR counts all hello handled and unhandled exceptions that are thrown, and divides hello total in a sampling interval by hello length of hello interval.</span></span> <span data-ttu-id="a4244-154">Merhaba Application Insights SDK'sı bu sonucu toplar ve toohello portal gönderir.</span><span class="sxs-lookup"><span data-stu-id="a4244-154">hello Application Insights SDK collects this result and sends it toohello portal.</span></span>
* <span data-ttu-id="a4244-155">*Özel durumlar* hello hello portal hello grafik hello örnekleme aralığı içinde tarafından alınan TrackException raporları sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="a4244-155">*Exceptions* is a count of hello TrackException reports received by hello portal in hello sampling interval of hello chart.</span></span> <span data-ttu-id="a4244-156">Burada TrackException kodunuzda çağırır ve tüm içermeyen yazmıştır özel durumlar Hello işlenmiş yalnızca içerir [işlenmeyen özel durumlar](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="a4244-156">It includes only hello handled exceptions where you have written TrackException calls in your code, and doesn't include all [unhandled exceptions](app-insights-asp-net-exceptions.md).</span></span> 

## <a name="alerts"></a><span data-ttu-id="a4244-157">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="a4244-157">Alerts</span></span>
<span data-ttu-id="a4244-158">Diğer ölçümleri gibi yapabilecekleriniz [bir uyarı ayarlamak](app-insights-alerts.md) bir performans sayacı, bir sınır dışında kalırsa belirttiğiniz toowarn.</span><span class="sxs-lookup"><span data-stu-id="a4244-158">Like other metrics, you can [set an alert](app-insights-alerts.md) toowarn you if a performance counter goes outside a limit you specify.</span></span> <span data-ttu-id="a4244-159">Merhaba uyarıları dikey penceresini açın ve eklemek uyarı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a4244-159">Open hello Alerts blade and click Add Alert.</span></span>

## <span data-ttu-id="a4244-160"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4244-160"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="a4244-161">Bağımlılık izleme</span><span class="sxs-lookup"><span data-stu-id="a4244-161">Dependency tracking</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="a4244-162">Özel durum izleme</span><span class="sxs-lookup"><span data-stu-id="a4244-162">Exception tracking</span></span>](app-insights-asp-net-exceptions.md)

