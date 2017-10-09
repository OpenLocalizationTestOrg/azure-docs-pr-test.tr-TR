---
title: "Özel olayları ve ölçümleri için Insights API'si aaaApplication | Microsoft Docs"
description: "Sorunlarını tanılamak ve birkaç satırlık bir kod, cihaz veya masaüstü uygulaması, Web sayfası veya service tootrack kullanımınızı ekleyin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>Özel olayları ve ölçümleri için Application Insights API'si

Birkaç satır kod ile kullanıcıların gerçekleştirdiği çıkışı, uygulama toofind eklemek veya toohelp sorunları tanılamak. Aygıt ve Masaüstü uygulamaları, web istemcileri ve web sunucuları telemetri gönderebilir. Kullanım hello [Azure Application Insights](app-insights-overview.md) çekirdek telemetri API'si toosend özel olayları ve ölçümleri ve standart telemetri kendi sürümleri. Bu API aynı API Application Insights veri toplayıcıları kullanın Bu hello standart hello.

## <a name="api-summary"></a>API özeti
Merhaba API birkaç küçük Çeşitlemeler dışında tüm platformlar arasında Tekdüzen değil.

| Yöntem | İçin kullanılır |
| --- | --- |
| [`TrackPageView`](#page-views) |Sayfalar, ekranlar, dikey veya formlar. |
| [`TrackEvent`](#trackevent) |Kullanıcı eylemleri ve diğer olaylar. Tootrack kullanıcı davranışı veya toomonitor performans kullanılır. |
| [`TrackMetric`](#trackmetric) |Performans ölçümleri sıra uzunlukları gibi toospecific olayları ilgili değildir. |
| [`TrackException`](#trackexception) |Tanılama için günlük özel durumları. İzleme burada bunlar ilişkisi tooother olaylar oluşur ve Yığın izlemeleri inceleyin. |
| [`TrackRequest`](#trackrequest) |Merhaba sıklığı ve sunucu istek süresi performans analizi için günlüğe kaydetme. |
| [`TrackTrace`](#tracktrace) |Tanılama günlük iletileri. Üçüncü taraf günlükleri de yakalayabilirsiniz. |
| [`TrackDependency`](#trackdependency) |Günlüğe kaydetme hello süresi ve uygulamanızı bağlıdır çağrıları tooexternal bileşenleri sıklığı. |

Yapabilecekleriniz [özellikleri ve ölçümleri attach](#properties) toomost bu telemetri çağrılarının.

## <a name="prep"></a>Başlamadan önce
Application Insights SDK'sı üzerinde bir başvuru henüz yoksa:

* Merhaba Application Insights SDK'sı tooyour proje ekleyin:

  * [ASP.NET projesi](app-insights-asp-net.md)
  * [Java projesi](app-insights-java-get-started.md)
  * [Her Web sayfasındaki JavaScript](app-insights-javascript.md) 
* Cihaz veya web sunucusu kodunuzda şunları içerir:

    *C# ' TA:*`using Microsoft.ApplicationInsights;`

    *Visual Basic:*`Imports Microsoft.ApplicationInsights`

    *Java:*`import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Bir TelemetryClient örneği oluşturma
Olgusu `TelemetryClient` (Web sayfalarındaki JavaScript'te hariç):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient iş parçacığı güvenlidir.

Uygulamanızı her modül için TelemetryClient örneğini kullanmanızı öneririz. Örneğin, web hizmeti tooreport gelen HTTP istekleri ve başka bir ara yazılım sınıf tooreport iş mantığı olayları bir TelemetryClient örneği olabilir. Özellikleri gibi ayarlayabilirsiniz `TelemetryClient.Context.User.Id` tootrack kullanıcılar ve oturumlar veya `TelemetryClient.Context.Device.Id` tooidentify hello makine. Bu bilgiler örneği gönderir hello ekli tooall olayları olur.

## <a name="trackevent"></a>TrackEvent
Application ınsights'ta bir *özel olay* içinde görüntüleyebilirsiniz bir veri noktası [ölçüm Gezgini](app-insights-metrics-explorer.md) toplanan sayılara olarak ve buna [tanılama arama](app-insights-diagnostic-search.md) olarak tek tek yineleme. (Bunu ilgili tooMVC veya diğer framework "olayları." değil)

INSERT `TrackEvent` çeşitli olayları, kod toocount çağırır. Ne sıklıkla kullanıcıların belirli bir özellik, ne sıklıkta bunlar belirli hedeflere ulaşmak veya hatalar belirli tür belki ne sıklıkta yaptıkları seçin.

Örneğin, bir oyun uygulamada bir kullanıcı hello oyun WINS bir olay gönderebilir:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Merhaba Microsoft Azure Portalı'nda, olayları görüntülemek
toosee, etkinliklerin sayısını açık bir [ölçüm Gezgini](app-insights-metrics-explorer.md) dikey penceresinde, yeni bir grafik ekleyin ve seçin **olayları**.  

![Özel olaylar sayısını bakın](./media/app-insights-api-custom-events-metrics/01-custom.png)

toocompare hello sayıları farklı olayların ayarlamak hello grafik türü çok**kılavuz**ve olay adı tarafından Grup:

![Merhaba grafik türü ve gruplandırma ayarlayın](./media/app-insights-api-custom-events-metrics/07-grid.png)

Başlangıç Kılavuzu, bir olay adı toosee oluşumlarını olay ' ı tıklatın. toosee daha fazla ayrıntı - hello listesinde olayı tıklatın.

![Aracılığıyla Hello olaylarını incelemek](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus belirli olayları arama veya ölçüm Gezgini, ilgilendiğiniz kümesi hello dikey'nın filtre toohello olay adları:

![Filtreler açın, olay adı'nı genişletin ve bir veya daha fazla değerleri seçin](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Analytics'te özel olaylar

Merhaba telemetri hello kullanılabilir `customEvents` tablosundaki [uygulama Öngörüler Analytics](app-insights-analytics.md). Her satır bir çağrı çok temsil eden`trackEvent(..)` uygulamanızda. 

Varsa [örnekleme](app-insights-sampling.md) içinde hello ItemCount özelliği 1'den büyük bir değer gösterir işlemdir. Örnek ItemCount == 10 çağrıları tootrackEvent() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir. özel olaylar doğru sayısını tooget, kullanmanız gereken bu nedenle kullanım kodu gibi `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights ekli tooparticular olayları olmayan ölçümleri grafik. Örneğin, bir kuyruk uzunluğu düzenli aralıklarla izlemek. Ölçümler ile Merhaba Çeşitlemeler ve eğilimleri'den daha az ilgi hello tek tek ölçüler olan ve böylece istatistiksel grafikleri kullanışlıdır.

Toosend ölçümleri tooApplication Öngörüler sipariş, hello kullanabilirsiniz `TrackMetric(..)` API. Ölçüm iki yolu toosend vardır: 

* Tek bir değer. Uygulamanızda bir ölçüm gerçekleştirdiğiniz her zaman tooApplication Öngörüler hello karşılık gelen değer gönderin. Örneğin, bir kapsayıcı öğe hello sayısını açıklayan bir ölçüm olduğunu varsayalım. Belirli bir zaman diliminde ilk üç öğe hello kapsayıcıya yerleştirdiğiniz ve ardından iki öğeyi kaldırın. Buna göre çağırırdı `TrackMetric` iki kez: hello değeri'ilk geçirme `3` ve değer hello `-2`. Application Insights, sizin adınıza her iki değerin de depolar. 

* Toplama. Ölçümleri ile çalışırken, her tek nadiren ilgi ölçüsüdür. Bunun yerine belirli bir süre içinde ne Özet önemlidir. Bu tür bir özeti adlı _toplama_. Yukarıdaki örnek Hello hello toplama ölçüm bu döneme ait toplamıdır `1` ve hello ölçüm değerleri hello sayısı `2`. Merhaba toplama yaklaşım kullanırken, yalnızca çağırma `TrackMetric` zaman dönemi ve gönderme hello toplama değerlerini zorunda kalırsınız. Merhaba maliyetini önemli ölçüde azaltabilir ve daha az veri göndererek yükü performans hala ilgili tüm bilgileri toplanırken tooApplication Öngörüler işaret olduğundan önerilen yaklaşımı hello budur.

### <a name="examples"></a>Örnekler:

#### <a name="single-values"></a>Tek değer

toosend tek bir ölçü değeri:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Ölçümleri toplama

Uygulama, tooreduce bant genişliği, maliyet ve tooimprove performans kaynağı bunları göndermeden önce tooaggregate ölçümleri önerilir.
Kod bir araya getirildiği bir örneği burada verilmiştir:

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Ölçümleri Explorer'da özel ölçümleri

toosee hello sonuçları ölçümleri Gezgini'ni açın ve yeni bir grafik ekleyin. Merhaba grafik tooshow, ölçüm düzenleyin.

> [!NOTE]
> Özel ölçüm birkaç dakika tooappear hello kullanılabilir ölçümler listesinde alabilir.
>

![Yeni bir grafik ekleyin veya bir grafik seçin ve özel altında ölçüm seçin](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Analytics'te özel ölçümleri

Merhaba telemetri hello kullanılabilir `customMetrics` tablosundaki [uygulama Öngörüler Analytics](app-insights-analytics.md). Her satır bir çağrı çok temsil eden`trackMetric(..)` uygulamanızda.
* `valueSum`-Bu hello hello ölçümleri toplamıdır. tooget hello ortalama değer, sıfıra bölünme `valueCount`.
* `valueCount`-hello bu toplanan ölçümleri sayısı `trackMetric(..)` çağırın.

## <a name="page-views"></a>Sayfa görünümleri
Her ekranı veya sayfa yüklendiğinde, bir aygıt veya Web sayfası uygulamasında varsayılan olarak sayfa görünümü telemetrisi gönderilir. Ancak bu tootrack sayfa görünümleri ek veya farklı zamanlarda değiştirebilirsiniz. Örneğin, sekmeler veya dikey pencereler görüntüler bir uygulamada Hello kullanıcı yeni bir dikey pencere açıldığında tootrack bir sayfa isteyebilirsiniz.

![Genel Bakış dikey penceresinde kullanım Mercek](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Sayfa görünümleri birlikte özellikleri şekilde hello gibi sayfa görünümü telemetrisi olduğunda Canlı gelen kullanıcı ve oturum grafik kullanıcı ve oturum verilerini gönderilir.

### <a name="custom-page-views"></a>Özel sayfa görünümleri
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Farklı HTML sayfaları içinde birden çok sekme varsa, hello URL çok belirtebilirsiniz:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Zamanlama sayfası görünümleri
Varsayılan olarak, hello kez bildirildi **sayfa görünümü yükleme süresi** hello tarayıcının sayfası yük olayı çağrılıncaya kadar hello tarayıcı hello isteği gönderdiğinde gelen ölçülür.

Bunun yerine, şunlardan birini yapabilirsiniz:

* Hello bir açık kalma süresini ayarlamak [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) çağırın: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Merhaba sayfa görünümü zamanlama çağrıları kullanmak `startTrackPage` ve `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Merhaba ilk parametre hello başlangıç ilişkilendirir gibi kullandığınız adı hello ve çağrıları durdurun. Bu varsayılan toohello geçerli sayfa adı içerir.

Ölçümleri Gezgini'nde görüntülenen süreleri hello hello aralığını türetilir hello elde edilen sayfa yükleme başlatma ve durdurma çağrıları. Bu tooyou gerçekten zaman hangi aralığıdır.

### <a name="page-telemetry-in-analytics"></a>Sayfa telemetri analizi

İçinde [Analytics](app-insights-analytics.md) iki tablo tarayıcı işlemleri verileri göster:

* Merhaba `pageViews` tablo hello URL ve sayfa başlığını hakkındaki verileri içerir
* Merhaba `browserTimings` tablo hello geçen süre tooprocess gelen veri hello gibi istemci performansı hakkında veri içerir

toofind hello tarayıcı tooprocess farklı sayfaları süreyi:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

farklı tarayıcıların toodiscover hello popularities:

```
pageViews | summarize count() by client_Browser
```

tooassociate sayfa görünümleri tooAJAX çağrıları, bağımlılıkları olan Katıl:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
Merhaba sunucusu SDK TrackRequest toolog HTTP isteklerini kullanır.

Bağlamda toosimulate istekleri istiyorsanız aynı zamanda kendiniz hello web hizmeti modülü çalışıyor burada yok çağırabilirsiniz.

Ancak, hello yolu toosend isteği telemetri burada hello isteği görevi gören önerilir bir <a href="#operation-context">işlemi bağlam</a>.

## <a name="operation-context"></a>İşlem bağlamı
Toothem ortak bir işlem kimliği ekleyerek telemetri öğelerini birlikte ilişkilendirebilirsiniz Merhaba standart isteği izleme modülü, özel durumlar ve bir HTTP istek gerçekleştirilirken gönderilen diğer olayları için bunu yapar. İçinde [arama](app-insights-diagnostic-search.md) ve [Analytics](app-insights-analytics.md), hello istekle ilişkili olaylar hello kimliği tooeasily bulma kullanabilirsiniz.

Merhaba en kolay yolu tooset hello kimliği, bu yöntemi kullanarak tooset bir işlem bağlamı şöyledir:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Bir işlemin bağlamını ayarlanması birlikte `StartOperation` belirttiğiniz hello türünde bir telemetri öğesi oluşturur. Merhaba işlemi çıkardığınızda veya açıkça çağırırsanız hello telemetri öğesi gönderir `StopOperation`. Kullanırsanız `RequestTelemetry` hello telemetri türü olarak zaman aşımına toohello aralığını başlatma ve durdurma süresi ayarlanır.

İşlem bağlamı iç içe olamaz. Bir işlem bağlamı zaten var. sonra Kimliğini ile oluşturulan hello öğesi de dahil olmak üzere tüm bulunan hello öğelerle ilişkili `StartOperation`.

Aramada, hello işlemi kullanılan toocreate hello bağlamdır **ilgili öğeler** listesi:

![İlgili öğeler](./media/app-insights-api-custom-events-metrics/21.png)

[Uygulama-Öngörüler-özel-işlemleri-tracking.md] izleme özel işlemler hakkında daha fazla bilgi için bkz.

### <a name="requests-in-analytics"></a>Analytics istekleri 

İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), istekleri Göster yukarı hello `requests` tablo.

Varsa [örnekleme](app-insights-sampling.md) olduğundan, işlem hello ItemCount özelliği bir değer 1'den büyük gösterir. Örnek ItemCount == 10 çağrıları tootrackRequest() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir. tooget istekleri ve ortalama süresi doğru sayısı isteği adlarıyla bölümlenmiş, kod gibi kullanın:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Özel durumlar tooApplication Öngörüler gönder:

* çok[saymanız](app-insights-metrics-explorer.md), hello sıklığı bir sorunun belirtisi olarak.
* çok[ayrı ayrı oluşumları inceleyin](app-insights-diagnostic-search.md).

Merhaba raporları hello Yığın izlemeleri içerir.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

her zaman toocall TrackException açıkça aktarıp hello SDK'ları birçok özel durumlarını otomatik olarak yakalama.

* ASP.NET: [toocatch özel durum kodu yazma](app-insights-asp-net-exceptions.md).
* J2EE: [özel durumları yakalanan otomatik olarak](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: Özel durumları otomatik olarak yakalanır. Toodisable otomatik olarak toplanmasını istiyorsanız, Web sayfalarındaki eklediğiniz bir satır toohello kod parçacığını ekleyin:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Analytics özel durumları

İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), özel durumlar hello görünmesini `exceptions` tablo.

Varsa [örnekleme](app-insights-sampling.md) işleminde, hello olduğu `itemCount` özelliği değeri 1'den büyük gösterir. Örnek ItemCount == 10 çağrıları tootrackException() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir. özel durum türüne göre özel durumlarının doğru bir sayısı tooget bölümlenmiş, kod gibi kullanın:

```
exceptions | summarize sum(itemCount) by type
```

Merhaba yığın bilgileri ayrı değişkenlere zaten ayıklanan ancak birbirinden hello çekebilir önemli çoğu `details` yapısı tooget daha fazla. Bu yapı dinamik olduğundan, beklediğiniz hello sonuç toohello türü atamalısınız. Örneğin:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

ilgili isteklerinde tooassociate istisnalar bir birleşim kullanın:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Kullanım TrackTrace toohelp Öngörüler "içerik haritası Kılavuzu" tooApplication göndererek sorunları tanılayın. Tanılama veri öbekleri göndermek ve bunları inceleyin [tanılama arama](app-insights-diagnostic-search.md).

[Oturum bağdaştırıcıları](app-insights-asp-net-trace-logs.md) bu API toosend üçüncü taraf günlükleri toohello portalı kullanın.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


İleti içeriği arama yapabilirsiniz ancak (özellik değerlerini), üzerinde filtre uygulayamazsınız.

Merhaba boyut sınırını `message` özellikleri hello sınırdan daha yüksektir.
TrackTrace avantajı hello iletisinde oldukça uzun veri koyabilirsiniz ' dir. Örneğin, POST verilerini şifreleyebilirsiniz.  

Ayrıca, bir önem düzeyi tooyour ileti ekleyebilirsiniz. Ve diğer telemetri gibi filtre özellik değerleri toohelp veya izlemeleri farklı kümeleri için arama ekleyebilirsiniz. Örneğin:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

İçinde [arama](app-insights-diagnostic-search.md), daha sonra kolayca tooa belirli veritabanı ile ilgili tüm hello iletilerini belirli önem düzeyine sahip bir filtre.


### <a name="traces-in-analytics"></a>İçindeki analizi

İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), çağıran tooTrackTrace Göster hello `traces` tablo.

Varsa [örnekleme](app-insights-sampling.md) içinde hello ItemCount özelliği 1'den büyük bir değer gösterir işlemdir. Örnek ItemCount == 10 çok çağırır 10 anlamına gelir`trackTrace()`, hello örnekleme işlemi yalnızca aktarılan bunlardan biri. tooget izleme çağrıları doğru sayısını, kullanmanız gereken bu nedenle kod gibi `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Kullanım hello TrackDependency tootrack hello yanıt sürelerini ve başarı oranları çağrıları tooan dış kod parçası, çağırın. Merhaba bağımlılık grafiklerinde hello portalında Hello sonuçları görüntülenir.

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

SDK'ları dahil hello sunucu unutmayın bir [bağımlılık Modülü](app-insights-asp-net-dependencies.md) bulur ve bazı bağımlılık çağrıları otomatik olarak--Örneğin, toodatabases ve REST API'leri izler. İş tooinstall sunucu toomake hello modül bir aracı var. Bu çağrı değil otomatik izleme hello tootrack çağrıları catch istiyorsanız veya tooinstall hello Aracısı istemiyorsanız kullanın.

Merhaba standart bağımlılık izleme modül devre dışı tooturn Düzenle [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) ve hello başvuru çok silme`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Analytics bağımlılıkları

İçinde [uygulama Öngörüler Analytics](app-insights-analytics.md), trackDependency çağrıları hello görünmesini `dependencies` tablo.

Varsa [örnekleme](app-insights-sampling.md) içinde hello ItemCount özelliği 1'den büyük bir değer gösterir işlemdir. Örnek ItemCount == 10 çağrıları tootrackDependency() hello örnekleme işlemi yalnızca bunlardan birinin aktarılan 10 anlamına gelir. tooget bağımlılıkları doğru sayısını hedef bileşen tarafından bölümlenmiş, kod gibi kullanın:

```
dependencies | summarize sum(itemCount) by target
```

tooassociate bağımlılıkları ile ilgili isteklerinde bir birleşim kullanın:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Düzenleniyor veri
Normalde, hello SDK bazen toominimize hello hello kullanıcı etkisini seçilen verileri gönderir. Uygulamada kapandıktan hello SDK kullanıyorsanız, ancak bazı durumlarda, tooflush hello arabellek--Örneğin, isteyebilirsiniz.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Merhaba işlevi hello için zaman uyumsuz olduğuna dikkat edin [server telemetri kanalı](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>Kimliği doğrulanmış kullanıcılar
Bir web uygulaması, kullanıcıların (varsayılan) tanımlama bilgileri tarafından tanımlanır. Bir kullanıcı birden çok kez uygulamanız farklı makine ya da tarayıcı erişimi engelliyorsa veya tanımlama bilgilerini sildiğinizde sayılması.

Kullanıcıların tooyour uygulamada oturum açarsanız hello tarayıcı kodda hello kimliği doğrulanmış kullanıcı kimliği ayarlayarak daha doğru bir sayı elde edebilirsiniz:

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

Bir ASP.NET web örneğin MVC uygulaması:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Gerekli toouse hello kullanıcının gerçek oturum açma adı değil. Yalnızca toobe benzersiz toothat kullanıcı Kimliğiniz vardır. Boşluk veya hello karakterlerden herhangi birini içermemelidir `,;=|`.

Merhaba kullanıcı kimliği ayrıca bir oturum tanımlama bilgisinde ayarlamak ve toohello sunucu gönderilen. Merhaba server SDK'sı yüklü ise hello kimliği hello bağlam özellikleri hem istemci hem de sunucu telemetrinin bir parçası olarak gönderilen kullanıcı kimlik doğrulaması. Daha sonra filtre ve onu Search'te.

Uygulamanız kullanıcıların hesaplara gruplar, hello hesabı için bir tanımlayıcı da geçirebilirsiniz (Merhaba ile aynı, kısıtlamaları'karakter).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

İçinde [ölçüm Gezgini](app-insights-metrics-explorer.md), sayar bir grafik oluşturabilirsiniz **kimliği doğrulanmış kullanıcılar,**, ve **kullanıcı hesaplarını**.

Ayrıca [arama](app-insights-diagnostic-search.md) belirli kullanıcı adları ve hesapları ile istemci veri noktaları için.

## <a name="properties"></a>Filtreleme, aramayı ve özelliklerini kullanarak verilerinizi kesimlere
Özellikleri ve ölçülerini tooyour olayları (ve ayrıca toometrics, sayfa görünümleri, özel durumlar ve diğer telemetri verileri) ekleyebilirsiniz.

*Özellikler* dize değerleri toofilter hello kullanım raporlarında telemetrinizi kullanabilirsiniz. Örneğin, uygulamanızın birkaç oyunlar sağlıyorsa, hangi oyunlar daha popüler görebilmeniz için hello oyun tooeach olay hello adı ekleyebilirsiniz.

8192 hello bir dize uzunluk sınırı yoktur. (Toosend büyük veri parçalarını istiyorsanız hello ileti parametresinin kullanın [TrackTrace](#track-trace).)

*Ölçümleri* grafik sunulan sayısal değerlerdir. Örneğin, oyun severler elde hello puanları aşamalı bir artış ise toosee isteyebilirsiniz. Merhaba grafikleri hello olayla gönderilir ve böylece elde edebilirsiniz özelliklerini ayırmak hello tarafından kesimli veya farklı oyun grafikleri Yığılmış.

Doğru görüntülenen ölçüm değerleri toobe için bunlar too0 büyük veya ona eşit olmalıdır.

Bazı vardır [hello sayısı özellikleri, özellik değerlerini ve ölçümleri sınırları](#limits) kullanabileceğiniz.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Toolog kişisel bilgileri değil özelliklerinde ilgilenebilmek.
>
>

*Ölçümleri kullandıysanız*, ölçümleri Gezgini'ni açın ve hello hello ölçümü seçin **özel** Grup:

![Ölçüm Gezgini, select hello Grafiği'ni açın ve hello ölçümü seçin](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Ölçüm görünmüyorsa veya hello **özel** başlığı Kapat hello seçimi dikey hiç ve daha sonra yeniden deneyin. Ölçümleri bazen bir saatte zaman toobe hello ardışık düzen üzerinden toplanır.

*Özellikleri ve ölçümleri kullandıysanız*, hello ölçüm hello özelliği tarafından segmentlere:

![Gruplandırma ayarlayın ve ardından hello özelliği tarafından grubu altında seçin](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*Tanılama arama*, hello özellikleri ve bir olay oluşumlarını ölçümlerini görüntüleyebilirsiniz.

![Bir örnek seçin ve ardından "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Kullanım hello **arama** alan toosee olay belirli bir özellik değeri olan bir oluşumu.

![Arama terimi yazın](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Arama ifadeleri hakkında daha fazla bilgi](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Alternatif yol tooset özellikleri ve ölçümleri
Daha kullanışlı ise, ayrı bir nesne olayda hello parametrelerinin toplayabilirsiniz:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Merhaba yeniden yok aynı telemetri öğesi örneği (`event` Bu örnekte) toocall Track*() birden çok kez. Bu yanlış yapılandırma ile gönderilen telemetri toobe neden olabilir.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Özel ölçümleri ve analizi özellikleri

İçinde [Analytics](app-insights-analytics.md), özel Ölçümler ve özelliklerini göster hello `customMeasurements` ve `customDimensions` her telemetri kayıt öznitelikleri.

Örneğin, "Oyun" tooyour isteği telemetri adlı bir özellik eklediyseniz, bu sorgu farklı değerler "oyunun" Merhaba oluşumlarını sayar ve özel ölçüm "puan" Merhaba hello ortalaması göster:

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Şunlara dikkat edin:

* Bir değer hello customDimensions veya customMeasurements JSON ayıkladığınızda, dinamik türüne sahip ve bu nedenle, gereken cast onu `tostring` veya `todouble`.
* Merhaba olasılığını tootake hesabı [örnekleme](app-insights-sampling.md), kullanmanız gereken `sum(itemCount)`değil `count()`.



## <a name="timed"></a>Zamanlama olayları
Bazen toochart tooperform eyleme geçen süreyi istersiniz. Örneğin, tooknow isteyebilirsiniz ne kadar kullanıcılar bir oyunda tooconsider seçimler alın. Bunun için hello ölçüm parametresini kullanabilirsiniz.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Özel telemetri için varsayılan özellikler
Bazı yazdığınız hello özel olaylar için tooset varsayılan özellik değerleri istiyorsanız, bunları TelemetryClient örneğinde ayarlayabilirsiniz. Bu istemciden gönderilen ekli tooevery telemetri öğesi oldukları.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Tek tek telemetri çağrıları kendi özelliği sözlüklerindeki hello varsayılan değerleri geçersiz kılabilirsiniz.

*JavaScript için web istemcileri*, [JavaScript telemetri başlatıcıları kullanmak](#js-initializer).

*tooadd özellikleri tooall telemetri*, standart toplama modüllerden hello veri dahil olmak üzere [uygulamak `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Örnekleme, filtreleme ve telemetri işleniyor
SDK hello gönderilmeden önce telemetrinizi kod tooprocess yazabilirsiniz. Merhaba işleme HTTP isteği koleksiyonu ve bağımlılık koleksiyonu gibi hello standart telemetri modüllerden gönderilen veriler içerir.

[Özellikler ekleme](app-insights-api-filtering-sampling.md#add-properties) uygulayarak tootelemetry `ITelemetryInitializer`. Örneğin, diğer özelliklerinden sürüm numaraları veya hesaplanan değerler ekleyebilirsiniz.

[Filtreleme](app-insights-api-filtering-sampling.md#filtering) değiştirebilir veya SDK hello uygulayarak gönderilmeden önce telemetri atmak `ITelemetryProcesor`. Ne gönderildiğinde veya atılan denetlemek, ancak ölçümlerinizi hello etkisi tooaccount sahip. Öğeler atılsın nasıl bağlı olarak, ilgili öğeler arasındaki hello özelliği toonavigate kaybedebilirsiniz.

[Örnekleme](app-insights-api-filtering-sampling.md) paketlenmiş çözüm tooreduce hello uygulama toohello portalınızdan gönderilen verilerin birimdir. Bunu görüntülenen hello ölçümleri etkilemeden yapar. Ve bunu özel durumlar, istekleri ve sayfa görünümleri gibi ilgili öğeleri arasında giderek özelliği toodiagnose sorunlarınızı etkilemeden yapar.

[Daha fazla bilgi edinin](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Telemetri devre dışı bırakma
çok*dinamik olarak durdurmak ve başlatmak* hello toplama ve telemetri iletimini:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

çok*seçili standart toplayıcıları devre dışı*--Örneğin, performans sayaçları, HTTP isteklerini veya bağımlılıkları--silin veya açıklama hello ilgili satırlarında çıkışı [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md). Örneğin, kendi TrackRequest veri toosend istiyorsanız bunu yapabilirsiniz.

## <a name="debug"></a>Geliştirici modu
Hata ayıklama sırasında yararlı toohave sonuçları hemen görebilmeniz için telemetrinizi hello ardışık düzen üzerinden öncelikli olur. Size yardımcı ayrıca get ek ileti hello telemetri herhangi bir sorun izleme. Uygulamanızı azaltabileceğinden, bir üretim ortamına kapatın.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>Seçili özel telemetri için Hello izleme anahtarı ayarlama
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a>Dinamik izleme anahtarı
geliştirme, test ve üretim ortamlarında, telemetri karıştırma tooavoid yapabilecekleriniz [ayrı Application Insights kaynakları oluşturmak](app-insights-create-new-resource.md) ve hello ortamına bağlı olarak kendi anahtarlarını değiştirme.

Merhaba yapılandırma dosyasından Hello izleme anahtarını almak yerine onu kodunuzda ayarlayabilirsiniz. Başlangıç anahtarı başlatma yöntemini, bir ASP.NET hizmetinde global.aspx.cs gibi ayarlayın:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



Web sayfalarındaki, tooset isteyebilirsiniz, hello web sunucusunun durumu, yerine tam anlamıyla hello komut dosyasına kodlama. Bir ASP.NET uygulamasında oluşturulan Örneğin, bir Web sayfasında:

*Razor JavaScript'te*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient tüm telemetri verilerinin yanı sıra gönderilen değerleri içeren bir içerik özelliği vardır. Normalde hello standart telemetri modülleri tarafından ayarlanmış, ancak Ayrıca bunları kendiniz ayarlayabilirsiniz. Örneğin:

    telemetry.Context.Operation.Name = "MyOperationName";

Bu değerleri kendiniz ayarlarsanız, hello ilgili satırından kaldırmayı düşünün [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), böylece değerleri ve hello standart değerleri kafası yok.

* **Bileşen**: Merhaba uygulama ve onun sürümü.
* **Aygıt**: hello uygulama çalıştığı hello cihaz hakkındaki verileri. (Web uygulamalarında hello sunucu veya hello telemetri gönderilen istemci aygıt budur.)
* **InstrumentationKey**: hello hello telemetri göründüğü Azure Application Insights kaynağı. Bu genellikle Applicationınsights.config kayıt.
* **Konum**: Merhaba hello cihazın coğrafi konumu.
* **İşlem**: web uygulamalarında geçerli HTTP isteği Merhaba. Diğer uygulama türleri bu toogroup olayları birlikte ayarlayabilirsiniz.
  * **Kimliği**: öğeleri ilişkili herhangi bir olay tanılama arama incelediğinizde, bulabilmesi için farklı olayları, karşılık gelen oluşturulan bir değer.
  * **Ad**: bir tanımlayıcı, genellikle hello URL'sini hello HTTP isteği.
  * **SyntheticSource**: değil null veya boş, hello isteğinin hello kaynak belirten bir dize bir robot veya web testi belirlenmiştir durumunda. Varsayılan olarak, ölçüm Gezgini hesaplamalarda gelen dışlanır.
* **Özellikleri**: tüm telemetri verileri ile gönderilen özellikleri. Tek tek parça * çağrılarında geçersiz kılınabilir.
* **Oturum**: hello kullanıcının oturumu. Merhaba kimliği hello kullanıcı bir süredir etkin ayarlanmadı bağlandığınızda değiştirilir oluşturulan tooa değer ayarlanır.
* **Kullanıcı**: kullanıcı bilgileri.

## <a name="limits"></a>Sınırlar
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

Merhaba veri hızı sınırı, kullanım basarsa tooavoid [örnekleme](app-insights-sampling.md).

long veri tutulur toodetermine bkz [veri saklama ve gizlilik](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Başvuru belgeleri
* [ASP.NET başvurusu](https://msdn.microsoft.com/library/dn817570.aspx)
* [Java başvurusu](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [JavaScript başvurusu](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [Android SDK](https://github.com/Microsoft/ApplicationInsights-Android)
* [iOS SDK](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>SDK kod
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Windows Server paketleri](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [Java SDK](https://github.com/Microsoft/ApplicationInsights-Java)
* [JavaScript SDK'sı](https://github.com/Microsoft/ApplicationInsights-JS)
* [Tüm platformlar](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Sorular
* *Hangi özel durumları Track_() çağrıları throw?*

    yok. Toowrap gerekmeyen try-catch yan tümcelerinde bunları. Ve Hello SDK sorunla karşılaşırsa hello hata ayıklama konsol çıkışı iletileri kaydedecek--tanılama Arama'da hello varsa--aracılığıyla iletileri alabilirsiniz.
* *REST API tooget veri hello portalından var mı?*

    Evet, hello [veri erişim API](https://dev.applicationinsights.io/). Diğer yolları tooextract verileri içerecek [verme Analytics tooPower BI](app-insights-export-power-bi.md) ve [sürekli verme](app-insights-export-telemetry.md).

## <a name="next"></a>Sonraki adımlar
* [Arama olayları ve günlükleri](app-insights-diagnostic-search.md)

* [Sorun giderme](app-insights-troubleshoot-faq.md)


