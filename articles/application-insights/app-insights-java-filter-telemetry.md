---
title: "Azure Application Insights telemetri Java web uygulamanıza filtre | Microsoft Docs"
description: "Telemetri trafiğini izlemek için gerekmeyen olaylarını filtreleyerek azaltmak."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbullwin
ms.openlocfilehash: f9e061c010667bc18ac54e6546cc25339e9c0e3e
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/01/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a>Java web uygulamanızda telemetri filtreleme

Filtreleri telemetri seçmek için bir yol sağlar, [Java web uygulaması Application Insights'a gönderir](app-insights-java-get-started.md). Kullanabileceğiniz bazı Giden kutusu filtreler vardır ve kendi özel filtreler de yazabilirsiniz.

Giden kutusu filtreler aşağıdakileri içerir:

* İzleme önem düzeyi
* Belirli URL'leri, anahtar sözcükleri veya yanıt kodları
* Hızlı yanıtlar - diğer bir deyişle, istekleri için uygulamanızı hızlı bir şekilde yanıt verdi.
* Belirli olay adları

> [!NOTE]
> Filtreler, uygulamanızın ölçümleri eğme. Örneğin, yavaş yanıtlar tanılamak için hızlı yanıt süreleri atmak için bir filtre ayarlar, karar verebilirsiniz. Ancak Application Insights tarafından bildirilen ortalama yanıt sürelerini sonra doğru hızından daha yavaş olacaktır ve isteği sayısı gerçek sayısından küçük olmalıdır.
> İlgili bir sorun varsa kullanmak [örnekleme](app-insights-sampling.md) yerine.

## <a name="setting-filters"></a>Filtre ayarlama

Applicationınsights.XML içinde eklemek bir `TelemetryProcessors` bölüm bu örnek gibi:


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
                  <!-- Names of events we don't want to see -->
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




[Yerleşik işlemciler kümesini İnceleme](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Yerleşik filtreleri

### <a name="metric-telemetry-filter"></a>Ölçüm Telemetri filtresi

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded`-Özel ölçüm adları virgülle ayrılmış listesi.


### <a name="page-view-telemetry-filter"></a>Sayfa görünümü Telemetrisi filtresi

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`-Süre sayfa yüklenmesi için geçen süre anlamına gelmektedir. Bu ayarlanırsa, bu süre daha hızlı yüklenen sayfaları raporlanmaz.
* `NotNeededNames`-Sayfa adları virgülle ayrılmış listesi.
* `NotNeededUrls`-URL virgülle ayrılmış listesini parça. Örneğin, `"home"` "home" URL'de bulunan tüm sayfaları çıkışı filtreler.


### <a name="request-telemetry-filter"></a>İstek Telemetri filtresi


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Yapay Kaynak Filtresi

SyntheticSource özelliğinde değerlere sahip tüm telemetri çıkışı filtreler. Bunlar bot, örümcekler ve kullanılabilirlik testleri gelen istekleri içerir.

Telemetri tüm yapay istekleri filtrelemenize:


```XML

           <Processor type="SyntheticSourceFilter" />
```

Belirli yapay kaynakları için telemetri filtrelemenize:


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded`-Yapay kaynak adları virgülle ayrılmış listesi.

### <a name="telemetry-event-filter"></a>Telemetri olay filtresi

Özel olaylar filtreler (kullanarak oturum [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames`-Olay adları virgülle ayrılmış listesi.


### <a name="trace-telemetry-filter"></a>İzleme Telemetri filtresi

Filtreler oturum izlemeleri (kullanarak oturum [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) veya [günlüğü framework Toplayıcı](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* `FromSeverityLevel`Geçerli değerler şunlardır:
 *  Kapalı - tüm izlemeleri filtre
 *  İzleme - filtre yok. İzleme düzeyi eşittir
 *  BİLGİ - filtre izleme düzeyi çıkışı
 *  UYAR - filtre izleme ve bilgileri
 *  HATA - filtre UYAR, bilgi, izleme çıkışı
 *  Kritik - kritik dışındaki tüm giden filtresi


## <a name="custom-filters"></a>Özel Filtreler

### <a name="1-code-your-filter"></a>1. Filtre kod

Kodunuzda, uygulayan bir sınıf oluşturun `TelemetryProcessor`:

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
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


### <a name="2-invoke-your-filter-in-the-configuration-file"></a>2. Yapılandırma dosyasında filtre çağırma

Applicationınsights.XML içinde:

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

## <a name="troubleshooting"></a>Sorun giderme

*My filtresi çalışmıyor.*

* Geçerli parametre değerleri sağladığınız denetleyin. Örneğin, süreleri tamsayı olmalıdır. Geçersiz değerler yok sayılacak filtre neden olur. Özel filtre Oluşturucusu veya set yöntemi bir özel durum oluşturursa, göz ardı edilir.

## <a name="next-steps"></a>Sonraki adımlar

* [Örnekleme](app-insights-sampling.md) -örnekleme ölçümlerinizi eğme olmayan alternatif olarak göz önünde bulundurun.
