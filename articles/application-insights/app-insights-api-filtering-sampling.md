---
title: "aaaFiltering ve içinde ön işleme hello Azure Application Insights SDK'sı | Microsoft Docs"
description: "Telemetri işlemciler ve Telemetri başlatıcıları hello SDK toofilter için yazma veya hello telemetri toohello Application Insights portalındaki gönderilmeden önce özellikleri toohello veri ekleyin."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Filtreleme ve hello Application Insights SDK'sı telemetri ön işleme


Yazma ve eklentiler nasıl telemetri yakalanan ve toohello Application Insights hizmeti gönderilmeden önce işlenen hello Application Insights SDK'sı toocustomize için yapılandırın.

* [Örnekleme](app-insights-sampling.md) , istatistikleri etkilemeden telemetri hello hacmini azaltır. Birlikte tutar ilgili veri noktaları aralarında bir sorunu tanılamada gidebilirsiniz. Merhaba Portalı'nda hello örnekleme için çarpılan toocompensate hello toplam sayı olan.
* Telemetri işlemcilerle filtreleme [ASP.NET](#filtering) veya [Java](app-insights-java-filter-telemetry.md) seçin veya toohello sunucu gönderilmeden önce hello SDK telemetri değiştirme olanak sağlar. Örneğin, robots istekleri hariç tutarak telemetri hello hacmi azaltabilir. Ancak filtreleme örnekleme daha fazla temel bir yaklaşım tooreducing trafiği. Ne iletilen üzerinde daha fazla denetim sağlar, ancak tüm başarılı istek filtresi toobe Bu, istatistikleri - Örneğin, etkiler farkında olması.
* [Telemetri başlatıcıları Özellikler ekleme](#add-properties) telemetri hello standart modüllerden dahil uygulamanızın gönderilen tooany telemetri. Örneğin, hesaplanan değerler ekleyebilirsiniz; veya toofilter hello veri hello Portalı'nda sürüm numaralarıyla.
* [Merhaba SDK API'si](app-insights-api-custom-events-metrics.md) kullanılan toosend özel olayları ve ölçümleri.

Başlamadan önce:

* Merhaba Application Insights yükleme [ASP.NET SDK](app-insights-asp-net.md) veya [Java için SDK](app-insights-java-get-started.md) uygulamanızda.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Filtreleme: ITelemetryProcessor
Bu teknik ne dahil ya da hello telemetri akışına dışlanan üzerinden daha doğrudan denetim olanağı verir. Örnekleme ile birlikte kullanın ya da ayrı olarak.

telemetri işlemci yazma ve hello SDK ile kaydetmek toofilter telemetri. Tüm telemetri işlemcinizin gider ve toodrop seçebilirsiniz hello ondan akışla aktarmak veya özellikleri ekleyin. Bu, telemetri hello HTTP isteği Toplayıcı ve hello bağımlılık Toplayıcı gibi hello standart modüllerden yanı sıra, kendiniz yazmıştır telemetri içerir. Örneğin, robots ya da başarılı bağımlılık çağrıları isteklerini hakkında telemetriyi filtre olabilir.

> [!WARNING]
> SDK Hello gönderilen hello telemetri filtreleme işlemcileri kullanan eğme hello portalında görebilir ve zor toofollow olun hello istatistikleri ilgili öğeleri.
>
> Bunun yerine, kullanmayı [örnekleme](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Bir telemetri işlemci (C#) oluşturma
1. Projenizi bu hello Application Insights SDK'sı sürüm 2.0.0 olduğunu doğrulayın veya daha sonra. Visual Studio Çözüm Gezgini'nde projenize sağ tıklayın ve NuGet paketlerini Yönet'i seçin. NuGet Paket Yöneticisi'nde Microsoft.applicationınsights.Web denetleyin.
2. toocreate bir filtre ITelemetryProcessor uygulayın. Telemetri modülü, telemetri başlatıcı ve telemetri kanal gibi başka bir genişletilebilirlik noktası budur.

    Telemetri işlemciler işleme zinciri oluşturmak dikkat edin. Telemetri işlemcisi örneği olduğunda, bir bağlantı toohello sonraki işlemci hello zincirinde geçir. Telemetri veri noktası toohello işlem yöntemi geçirildiğinde çalışmasını yapar ve sonra çağrıları hello zincirinde sonraki Telemetri işlemci hello.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. Bu Applicationınsights.Config'de ekleyin:

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Merhaba budur başlatma burada örnekleme filtre aynı bölüm.)

Sınıfınızda ortak adlandırılmış özellikleri sağlayarak hello .config dosyasından dize değerlerini geçirebilirsiniz.

> [!WARNING]
> Toomatch hello türü adını herhangi hello .config dosyası toohello sınıfı özellik adlarını ve özellik adları hello kodda dikkatli olun. Merhaba .config dosyası mevcut olmayan türe veya özelliğe başvuruyorsa, hello SDK sessizce toosend tüm telemetri başarısız olabilir.
>
>

**Alternatif olarak,** hello filtre kodda başlatabilirsiniz. Uygun başlatma sınıfında - örneğin AppStart Global.asax.cs içinde - hello zincirine işlemci ekleyin:

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

Bu noktadan sonra oluşturulan TelemetryClients, işlemci kullanır.

### <a name="example-filters"></a>Örnek filtreleri
#### <a name="synthetic-requests"></a>Yapay istekleri
Bot ve web testi filtreleyin. Ölçüm Gezgini sağlamakla birlikte seçeneği toofilter yapay kaynakları çıkışı Merhaba, bu seçenek SDK hello filtreleyerek trafiğini azaltır.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Başarısız kimlik doğrulaması
"401" yanıt istekleri filtreler.

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Hızlı uzak bağımlılık çağrıları filtre
Yavaş toodiagnose çağrıları yalnızca istiyorsanız hello hızlı olanları filtreleyin.

> [!NOTE]
> Bu hello portalında gördüğünüz hello istatistikleri eğme. Merhaba bağımlılık çağrıları tüm hataları varsa gibi hello bağımlılık grafik arar.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Bağımlılık sorunlarını tanılama
[Bu blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) otomatik olarak normal ping toodependencies göndererek proje toodiagnose bağımlılık sorunları açıklar.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Özellikleri ekleyin: ITelemetryInitializer
Gönderilen telemetri başlatıcıları toodefine genel özellikleri ile tüm telemetri kullanın; ve hello standart telemetri modülleri davranışını toooverride seçtiniz.

Örneğin, Web Paketi için Application Insights hello HTTP istekleriyle ilgili telemetri toplar. Varsayılan olarak, bu yanıt kodu ile herhangi bir istek başarısız olarak işaretler > = 400. Ancak, başarı olarak tootreat 400 istiyorsanız, hello başarı özelliğini ayarlayan bir telemetri Başlatıcı sağlayabilir.

Bir telemetri Başlatıcı sağlarsanız, herhangi bir Track*() hello olduğunda çağrılır yöntemleri çağrılır. Bu hello standart telemetri modülleri tarafından adlı yöntemler içerir. Kurala göre bu modülleri başlatıcısı tarafından zaten ayarlanmış herhangi bir özelliği ayarlı değil.

**Başlatıcı tanımlayın**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**Başlatıcı yükleme**

Applicationınsights.Config'de:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*Alternatif olarak,* kodda, örneğin Global.aspx.cs hello Başlatıcı örneği:

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Bu örnek daha fazla bilgi bakın.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>JavaScript telemetri başlatıcıları
*JavaScript*

Merhaba portalından aldığınız hemen hello başlatma koddan sonra bir telemetri başlatıcı ekleyin:

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Merhaba özel olmayan özellikleri hello telemetryItem üzerinde kullanılabilir özeti için bkz: [uygulama Öngörüler dışarı veri modeli](app-insights-export-data-model.md).

İstediğiniz sayıda başlatıcıları ekleyebilirsiniz.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor ve ITelemetryInitializer
Merhaba telemetri işlemciler ve telemetri başlatıcıları arasındaki fark nedir?

* Bazı üst üste geliyor bunlarla yapabileceklerinizi içinde vardır: her ikisi de kullanılan tooadd özellikleri tootelemetry olabilir.
* TelemetryInitializers TelemetryProcessors önce her zaman çalışır.
* TelemetryProcessors toocompletely Değiştir izin ver veya bir telemetri öğesini atın.
* TelemetryProcessors performans sayacı telemetri işlem yok.


## <a name="reference-docs"></a>Başvuru belgeleri
* [API’ye Genel Bakış](app-insights-api-custom-events-metrics.md)
* [ASP.NET başvurusu](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>SDK kod
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [JavaScript SDK'sı](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Sonraki adımlar
* [Arama olayları ve günlükleri](app-insights-diagnostic-search.md)
* [Örnekleme](app-insights-sampling.md)
* [Sorun giderme](app-insights-troubleshoot-faq.md)
