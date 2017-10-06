---
title: "Java web uygulamanıza Azure Application Insights telemetri aaaFilter | Microsoft Docs"
description: "Telemetri trafiğini azaltmak hello olaylarını filtreleyerek toomonitor gerekmez."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="5ceb4-103">Java web uygulamanızda telemetri filtreleme</span><span class="sxs-lookup"><span data-stu-id="5ceb4-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="5ceb4-104">Filtreleri, bir şekilde tooselect hello telemetri sağlar, [Java web uygulaması gönderir tooApplication Öngörüler](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="5ceb4-105">Kullanabileceğiniz bazı Giden kutusu filtreler vardır ve kendi özel filtreler de yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="5ceb4-106">Merhaba Giden kutusu filtreler aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="5ceb4-107">İzleme önem düzeyi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-107">Trace severity level</span></span>
* <span data-ttu-id="5ceb4-108">Belirli URL'leri, anahtar sözcükleri veya yanıt kodları</span><span class="sxs-lookup"><span data-stu-id="5ceb4-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="5ceb4-109">Hızlı yanıtlar - diğer bir deyişle, istekleri toowhich uygulamanızı yanıt tooquickly</span><span class="sxs-lookup"><span data-stu-id="5ceb4-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="5ceb4-110">Belirli olay adları</span><span class="sxs-lookup"><span data-stu-id="5ceb4-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="5ceb4-111">Filtreler, uygulamanızın hello ölçümleri eğme.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="5ceb4-112">Örneğin, sipariş toodiagnose yavaş yanıtları, bir filtre toodiscard hızlı yanıt süreleri ayarlayın, karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="5ceb4-113">Ancak Application Insights tarafından bildirilen hello ortalama yanıt sürelerini sonra hello true hızından daha yavaş olacaktır ve isteği hello sayısı hello gerçek sayısından küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="5ceb4-114">İlgili bir sorun varsa kullanmak [örnekleme](app-insights-sampling.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="5ceb4-115">Filtre ayarlama</span><span class="sxs-lookup"><span data-stu-id="5ceb4-115">Setting filters</span></span>

<span data-ttu-id="5ceb4-116">Applicationınsights.XML içinde eklemek bir `TelemetryProcessors` bölüm bu örnek gibi:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want toosee -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="5ceb4-117">[Yerleşik işlemciler Hello kümesini İnceleme](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="5ceb4-118">Yerleşik filtreleri</span><span class="sxs-lookup"><span data-stu-id="5ceb4-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="5ceb4-119">Ölçüm Telemetri filtresi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="5ceb4-120">`NotNeeded`-Özel ölçüm adları virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="5ceb4-121">Sayfa görünümü Telemetrisi filtresi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="5ceb4-122">`DurationThresholdInMS`-Süre tooload hello sayfa geçen toohello süre anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="5ceb4-123">Bu ayarlanırsa, bu süre daha hızlı yüklenen sayfaları raporlanmaz.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="5ceb4-124">`NotNeededNames`-Sayfa adları virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="5ceb4-125">`NotNeededUrls`-URL virgülle ayrılmış listesini parça.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="5ceb4-126">Örneğin, `"home"` "home" Merhaba URL'de bulunan tüm sayfaları çıkışı filtreler.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="5ceb4-127">İstek Telemetri filtresi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="5ceb4-128">Yapay Kaynak Filtresi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-128">Synthetic Source filter</span></span>

<span data-ttu-id="5ceb4-129">Merhaba SyntheticSource özellik değerlerine sahip tüm telemetri çıkışı filtreler.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="5ceb4-130">Bunlar bot, örümcekler ve kullanılabilirlik testleri gelen istekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="5ceb4-131">Telemetri tüm yapay istekleri filtrelemenize:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="5ceb4-132">Belirli yapay kaynakları için telemetri filtrelemenize:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="5ceb4-133">`NotNeeded`-Yapay kaynak adları virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="5ceb4-134">Telemetri olay filtresi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-134">Telemetry Event filter</span></span>

<span data-ttu-id="5ceb4-135">Özel olaylar filtreler (kullanarak oturum [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="5ceb4-136">`NotNeededNames`-Olay adları virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="5ceb4-137">İzleme Telemetri filtresi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-137">Trace Telemetry filter</span></span>

<span data-ttu-id="5ceb4-138">Filtreler oturum izlemeleri (kullanarak oturum [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) veya [günlüğü framework Toplayıcı](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="5ceb4-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="5ceb4-139">`FromSeverityLevel`Geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="5ceb4-140">Kapalı - tüm izlemeleri filtre</span><span class="sxs-lookup"><span data-stu-id="5ceb4-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="5ceb4-141">İzleme - filtre yok.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-141">TRACE           - No filtering.</span></span> <span data-ttu-id="5ceb4-142">tooTrace düzeyine eşit</span><span class="sxs-lookup"><span data-stu-id="5ceb4-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="5ceb4-143">BİLGİ - filtre izleme düzeyi çıkışı</span><span class="sxs-lookup"><span data-stu-id="5ceb4-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="5ceb4-144">UYAR - filtre izleme ve bilgileri</span><span class="sxs-lookup"><span data-stu-id="5ceb4-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="5ceb4-145">HATA - filtre UYAR, bilgi, izleme çıkışı</span><span class="sxs-lookup"><span data-stu-id="5ceb4-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="5ceb4-146">Kritik - kritik dışındaki tüm giden filtresi</span><span class="sxs-lookup"><span data-stu-id="5ceb4-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="5ceb4-147">Özel Filtreler</span><span class="sxs-lookup"><span data-stu-id="5ceb4-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="5ceb4-148">1. Filtre kod</span><span class="sxs-lookup"><span data-stu-id="5ceb4-148">1. Code your filter</span></span>

<span data-ttu-id="5ceb4-149">Kodunuzda, uygulayan bir sınıf oluşturun `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="5ceb4-150">2. Filtreniz hello yapılandırma dosyasında çağırma</span><span class="sxs-lookup"><span data-stu-id="5ceb4-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="5ceb4-151">Applicationınsights.XML içinde:</span><span class="sxs-lookup"><span data-stu-id="5ceb4-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="5ceb4-152">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5ceb4-152">Troubleshooting</span></span>

<span data-ttu-id="5ceb4-153">*My filtresi çalışmıyor.*</span><span class="sxs-lookup"><span data-stu-id="5ceb4-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="5ceb4-154">Geçerli parametre değerleri sağladığınız denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="5ceb4-155">Örneğin, süreleri tamsayı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-155">For example, durations should be integers.</span></span> <span data-ttu-id="5ceb4-156">Geçersiz değerler göz ardı hello filtre toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="5ceb4-157">Özel filtre Oluşturucusu veya set yöntemi bir özel durum oluşturursa, göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ceb4-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ceb4-158">Next steps</span></span>

* <span data-ttu-id="5ceb4-159">[Örnekleme](app-insights-sampling.md) -örnekleme ölçümlerinizi eğme olmayan alternatif olarak göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5ceb4-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
