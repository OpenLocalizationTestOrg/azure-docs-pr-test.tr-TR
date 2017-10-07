---
title: "Azure Application ınsights'ta aaaTelemetry örnekleme | Microsoft Docs"
description: "Nasıl tookeep telemetri denetimindeki hacmi hello."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a>Application Insights’ta örnekleme


Örnekleme bir özelliktir [Azure Application Insights](app-insights-overview.md). Bu uygulama verilerinin istatistiksel olarak doğru bir analiz korurken hello yolu tooreduce telemetri trafiği ve depolama, önerilen olur. Böylece, tanılama araştırmalar yaparken öğeleri arasında gezinebilirsiniz hello filtre ilgili öğeleri seçer.
Ölçüm sayıları hello Portalı'nda tooyou sunulduğunda renormalized örnekleme, herhangi bir efekt hello istatistiklerle toominimize hello tootake hesabı.

Örnekleme trafiği ve veri maliyetleri azaltır ve azaltma önlemenize yardımcı olur.

## <a name="in-brief"></a>Kısaca:
* Örnekleme korur 1'de  *n*  kaydeder ve hello rest atar. Örneğin, 1, 5 olayları, % 20 örnekleme oranını korumak. 
* Uygulamanız çok sayıda telemetri, ASP.NET web sunucusu uygulamalarında gönderirse örnekleme otomatik olarak gerçekleşir.
* El ile ya da hello örnekleme de ayarlayabilirsiniz fiyatlandırma sayfası; hello portalını ve hello hello .config dosyasına ASP.NET SDK, tooalso hello ağ trafiğini azaltabilir.
* Özel olayları günlüğe kaydedin ve toomake olayların kümesini korunur veya birlikte atılan emin emin istiyorsanız, bunlar sahip Merhaba, aynı Operationıd değeri emin olun.
* Merhaba örnekleme bölen  *n*  hello özelliğinde her bir kayıttaki bildirilen `itemCount`, arama göründüğü hello kolay adı "istek sayısı" veya "olay sayısı" altında. Örnekleme işlemi içinde olmadığında `itemCount==1`.
* Analitik sorguları yazma durumunda [örnekleme hesaba](app-insights-analytics-tour.md#counting-sampled-data). Özellikle, yalnızca kayıtları sayım yerine, kullanmanız gereken `summarize sum(itemCount)`.

## <a name="types-of-sampling"></a>Örnekleme türleri
Üç alternatif örnekleme yöntemi vardır:

* **Uyarlamalı örnekleme** hello telemetri ASP.NET uygulamanızı hello SDK gönderilen hacmi otomatik olarak ayarlar. SDK v 2.0.0-beta3 varsayılan. Şu anda, yalnızca ASP.NET sunucu tarafı telemetri için de kullanılabilir. 
* **Sabit oran örnekleme** ASP.NET sunucunuzdan hem ve kullanıcılarınızın tarayıcılarından gönderilen telemetri hello hacmini azaltır. Merhaba oranı ayarlayın. Merhaba istemci ve sunucu kendi örnekleme eşitleyecek böylece söz konusu, arama ilgili sayfa görünümleri ve istekler arasında gezinebilirsiniz.
* **Alım örnekleme** hello Azure portal çalışır. Belirlediğiniz bir hızda uygulamanızdan ulaşan hello telemetri bazıları atar. Telemetri trafiği azaltmaz ancak içinde aylık kota tutmanıza yardımcı olur. Alım örnekleme büyük avantajlarından Hello uygulamanızı yeniden dağıtmadan ayarlayabilirsiniz ve tüm sunucular ve istemciler için aynı şekilde çalışır ' dir. 

Bağdaşık veya sabit oranı örnekleme işlemi yoksa alım örnekleme devre dışı bırakılır.

## <a name="ingestion-sampling"></a>Alım örnekleme
Bu biçimi örnekleme, burada web sunucusu, tarayıcılar ve cihazlar hello telemetrisini hello Application Insights Hizmeti uç noktası ulaştığında hello noktada çalışır. Uygulamanızdan gönderilen hello telemetri trafiği azaltmaz ancak hello miktarını azaltmak işlenen ve korunur (ve için sizden ücret) Application Insights tarafından.

Bu tür örnekleme uygulamanızı genellikle aylık kotasına gider ve hello SDK tabanlı türleri örnekleme birini kullanarak hello seçeneği yoksa kullanın. 

Merhaba örnekleme hızını hello kotalar ve fiyatlandırma dikey ayarlayın:

![Merhaba uygulama genel bakış dikey penceresinden ayarları, kota, örnekleri, tıklatın ardından örnekleme hızını seçin ve Güncelleştir'i tıklatın.](./media/app-insights-sampling/04.png)

Örnekleme diğer türleri gibi ilgili telemetri öğeleri hello algoritması korur. Aramadaki hello telemetri incelerken, örneğin, size kullanabileceksiniz toofind hello isteği ilgili tooa belirli özel durum. Ölçüm isteği hızı gibi sayar ve özel durum oranı doğru korunur.

Örnekleme tarafından atılan veri noktaları kullanılamıyor herhangi bir Application Insights özellik gibi [sürekli verme](app-insights-export-telemetry.md).

SDK tabanlı uyarlamalı veya sabit oranı örnekleme çalışıyorken alım örnekleme çalışmaz. Merhaba SDK Hello örnekleme Oranı % 100'den az ise, ardından hello ayarladığınız alım örnekleme oranını göz ardı edilir.

> [!WARNING]
> Merhaba kutucuğu gösterilen hello değere alım örnekleme için ayarladığınız hello değeri gösterir. SDK örnekleme işlemiyse hello gerçek örnekleme oranını temsil etmez.
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a>Web sunucunuzdaki Uyarlamalı örnekleme
Uyarlamalı örnekleme hello Application Insights SDK'sı ASP.NET v 2.0.0-beta3 ve sonraki sürümleri için kullanılabilir ve varsayılan olarak etkindir. 

Uyarlamalı örnekleme, web sunucusu uygulama toohello Application Insights hizmeti gönderilen telemetri hello hacmi etkiler. Merhaba birimi otomatik olarak düzeltilir tookeep trafiğinin belirtilen maksimum oranını içinde.

Bu telemetrinin, düşük birimlerinin hata ayıklama, bir uygulama şekilde çalışmaz veya bir Web sitesi düşük kullanımı ile etkilenmeyecek.

tooachieve hello hedef birim, oluşturulan hello telemetri bazıları göz ardı edilir. Ancak, diğer örnekleme türleri gibi hello algoritması ilgili telemetri öğeleri korur. Aramadaki hello telemetri incelerken, örneğin, size kullanabileceksiniz toofind hello isteği ilgili tooa belirli özel durum. 

Böylece bunlar yaklaşık doğru değerlerin ölçüm Gezgininde Göster istek hızı ve özel durum oranı oranı, örnekleme hello için ayarlanan toocompensate gibi ölçüm sayar.

**Projenizin NuGet güncelleştirme** toohello son paketleri *yayın öncesi* Application Insights sürümü: hello Çözüm Gezgini'nde projeye sağ tıklayın, NuGet paketlerini Yönet seçin denetleyin **Ekle yayın öncesi** ve Microsoft.applicationınsights.Web arayın. 

İçinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), hello çeşitli parametreleri ayarlayabileceğiniz `AdaptiveSamplingTelemetryProcessor` düğümü. gösterilen hello rakamları hello varsayılan değerler şunlardır:

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    Merhaba Uyarlamalı algoritması hello hedef hızı için amaçlar **her sunucu ana bilgisayarda**. Web uygulamanızı pek çok ana bilgisayarda çalışıyorsa, bu değer, hedef hello Application Insights portalındaki trafiğinin oranını içinde tooremain olarak şekilde azaltın.
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    Merhaba aralığı sırasında hangi hello telemetri geçerli hızı yeniden değerlendirilir. Değerlendirme hareketli ortalama gerçekleştirilir. Telemetrinizi zararlardan toosudden WINS'e ise bu aralığı tooshorten isteyebilirsiniz.
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    Örnekleme yüzdesi değeri, ne zaman sonra değişir, biz toocapture veri daha az yüzdesi yeniden örnekleme toolower izin.
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    Örnekleme yüzdesi değeri, ne zaman sonra değişir, biz yüzdesi yeniden örnekleme tooincrease toocapture izin daha fazla veri.
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    Yüzde örnekleme değiştikçe hello en düşük değer nedir biz tooset izin verilir.
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    Yüzde örnekleme değiştikçe hello en büyük değer nedir biz tooset izin verilir.
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    Hareketli Ortalama hello Hello hesaplamadaki hello ağırlık toohello en son değer atanmış. 1'den küçük bir değere eşit tooor kullanın. Küçük değerler hello algoritması daha az reaktif toosudden değişiklikleri yapın.
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    Merhaba uygulama yalnızca başladığında atanan hello değer. Hatalarını ayıkladığınız sırada bu azaltma yok. 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    Noktalı virgülle ayrılmış örneklenen toobe istemediğiniz türleri listesi. Türler tanınan: bağımlılık, olay, özel durum, sayfa görünümü, istek, izleme. Merhaba tüm örneklerini türleri aktarılan belirtilen; belirtilmediği hello türleri örneklenen.

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    Örneklenen toobe istediğiniz türlerini noktalı virgülle ayrılmış listesi. Türler tanınan: bağımlılık, olay, özel durum, sayfa görünümü, istek, izleme. Merhaba türleri örneklenen belirtilen; tüm örnekleri Merhaba diğer türleri her zaman aktarılmaz.


**Kapalı tooswitch** Uyarlamalı örnekleme, Kaldır hello AdaptiveSamplingTelemetryProcessor applicationınsights-config düğümden.

### <a name="alternative-configure-adaptive-sampling-in-code"></a>Alternatif: Uyarlamalı örnekleme yapılandırma
Örnekleme hello .config dosyasına ayarlama yerine kodu kullanabilirsiniz. Bu, toospecify hello örnekleme hızını tekrar değerlendirilir olduğunda çağrılan bir geri çağırma işlevi sağlar. Bu kullanabilirsiniz, örneğin, hangi örnekleme hızını çıkışı toofind kullanılıyor.

Merhaba kaldırmak `AdaptiveSamplingTelemetryProcessor` hello .config dosyası düğümden.

*C#*

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Telemetri işlemciler hakkında daha fazla bilgi](app-insights-api-filtering-sampling.md#filtering).)

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a>JavaScript web sayfaları için örnekleme
Web sayfaları için herhangi bir sunucudan sabit oranı örnekleme yapılandırabilirsiniz. 

Olduğunda, [hello web sayfaları için Application Insights yapılandırma](app-insights-javascript.md), hello Application Insights portalından aldığınız hello parçacığını değiştirmek. (ASP.NET uygulamalarında hello parçacığı genellikle _Layout.cshtml içinde gider.)  Benzer bir satır ekleyin `samplingPercentage: 10,` hello izleme anahtarını önce:

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

Merhaba örnekleme yüzdesi Kapat too100/N N bir tamsayı olduğu bir yüzde seçin.  Şu anda örnekleme diğer değerleri desteklemiyor.

Sabit oran örnekleme hello sunucuda da etkinleştirirseniz, bu, içinde arama ilgili sayfa görünümleri ve istekler arasında gezinebilirsiniz şekilde hello istemciler ve sunucu eşitler.

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a>ASP.NET web siteleri için sabit oranı örnekleme
Sabit oranı örnekleme, web sunucunuz ve web tarayıcıları gönderilen hello trafiğini azaltır. Uyarlamalı örnekleme aksine, telemetri sizin tarafınızdan karar sabit bir oranda azaltır. İlgili öğeler - Örneğin, korunur, böylece arama sayfası görünümünde bakarsanız, ilgili isteğini bulabilmesi için aynı zamanda hello istemci ve sunucu örnekleme eşitler.

Merhaba örnekleme algoritması ilgili öğeler korur. Her HTTP isteği için olay, bu ve ilgili olaylar atılan aktarılan ya. 

Yaklaşık doğru; böylece ölçümleri Explorer'da faktörü toocompensate hello örnekleme hızı için istek ve özel durum sayısı gibi oranları çarpılır.

1. **Projenizin NuGet paketlerini güncelleştirmeyi** son toohello *yayın öncesi* Application Insights sürümü. Çözüm Gezgini'nde Hello projeye sağ tıklayın, NuGet paketlerini Yönet seçin denetleyin **dahil et** ve Microsoft.applicationınsights.Web arayın. 
2. **Uyarlamalı örnekleme devre dışı**: içinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), kaldırmak veya yorum hello `AdaptiveSamplingTelemetryProcessor` düğümü.
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. **Merhaba sabit oranı örnekleme modülü etkinleştirin.** Bu kod parçacığında çok eklemek[Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md):
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> Merhaba örnekleme yüzdesi Kapat too100/N N bir tamsayı olduğu bir yüzde seçin.  Şu anda örnekleme diğer değerleri desteklemiyor.
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a>Alternatif: sunucu kodunuzdaki sabit oranı örnekleme etkinleştir
Merhaba .config dosyasına Hello örnekleme parametre ayarı yerine kodu kullanabilirsiniz. 

*C#*

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

([Telemetri işlemciler hakkında daha fazla bilgi](app-insights-api-filtering-sampling.md#filtering).)

## <a name="when-toouse-sampling"></a>Zaman toouse örnekleme?
Uyarlamalı örnekleme hello ASP.NET SDK sürüm 2.0.0-beta3 kullanırsanız, otomatik olarak etkinleştirilmiş veya sonraki bir sürümü. Kullandığınız hangi SDK sürümü olsun alım örnekleme (bizim sunucuda) kullanabilirsiniz.

En küçük ve orta ölçekli uygulamalar için örnekleme gerekmez. Merhaba en yararlı tanı bilgilerini ve en doğru istatistikleri, tüm kullanıcı etkinliklerini veri toplayarak elde edilir. 

örnekleme Hello ana avantajları şunlardır:

* Uygulamanızı telemetri çok yüksek oranda kısa gönderdiğinde uygulama Öngörüler hizmeti düşme ("kısıtlamaları") veri noktaları aralığı zaman. 
* Merhaba içinde tookeep [kota](app-insights-pricing.md) fiyatlandırma katmanınızı veri noktaları. 
* telemetri hello koleksiyonundan tooreduce ağ trafiği. 

### <a name="which-type-of-sampling-should-i-use"></a>Hangi tür örnekleme kullanmalıyım?
**Alım varsa örnekleme kullanın:**

* Genellikle, telemetri aylık kota de gidin.
* Merhaba örnekleme - örneğin desteklemiyor SDK'sı, hello Java SDK'sı veya ASP.NET sürümleri sürümünü 2'den önceki kullanıyorsunuz.
* Çok sayıda telemetri kullanıcılarınızın web tarayıcılarından alıyorsunuz.

**Sabit oranı, örnekleme kullanın:**

* ASP.NET web Hizmetleri sürüm 2.0.0 hello Application Insights SDK kullanıyorsanız veya sonraki bir sürümü ve
* Olayların ne zaman çalışıyoruz böylece istemci ve sunucu arasında eşitlenen örnekleme istediğiniz [arama](app-insights-diagnostic-search.md), hello istemcide ilgili olaylar ve sayfa görünümleri ve http isteklerini gibi sunucu arasında gezinebilirsiniz.
* Uygulamanız için hello uygun örnekleme yüzdesi emin olduğunuz. Bunu yeterince tooget doğru ölçümler, ancak aşağıda fiyatlandırma kotayı aştığı oranı hello ve gerekir azaltma sınırları hello. 

**Uyarlamalı örnekleme kullanın:**

Aksi takdirde, Uyarlamalı örnekleme öneririz. Bu hello ASP.NET sunucusu SDK sürüm 2.0.0-beta3 varsayılan olarak etkin veya sonraki bir sürümü. Düşük kullanım site etkilememesi için trafiği bir belirli en düşük hızı kadar azaltmaz.

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a>Örnekleme işlemi olup olmadığını nasıl anlayabilirim?
Burada uygulandığından, olsun oranı örnekleme toodiscover hello gerçek kullanmak bir [Analytics sorgu](app-insights-analytics.md) bu gibi:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

Her kaydı tutulur `itemCount` temsil eder, özgün kayıt eşit too1 + hello kayıt sayısı, önceki atılan hello sayısını gösterir. 

## <a name="how-does-sampling-work"></a>Örnekleme nasıl çalışır?
Sabit oranı ve Uyarlamalı örnekleme hello SDK başlayarak 2.0.0 ASP.NET sürümlerden bir özelliğidir. Alım örnekleme hello Application Insights hizmeti, bir özelliğidir ve hello SDK örnekleme gerçekleştirmiyorsa işleminde olabilir. 

hangi telemetri öğeleri toodrop ve (Merhaba SDK veya hello Application Insights hizmeti olup) hangi olanları tookeep Hello örnekleme algoritmasını belirler. Merhaba örnekleme karar toopreserve tüm birbiriyle veri noktaları olduğu gibi bir işlem yapılabilir ve hatta sınırlı bir veri kümesi ile güvenilir Application Insights tanılama deneyimi koruma hedeflenir çeşitli kurallar temel alır. Başarısız bir istek için ek telemetri öğeleri (örneğin, özel durumu ve bu istekten oturum izlemeleri) uygulamanızı gönderirse, örneğin, örnekleme bu istek ve başka telemetriyle bölecek değil. Tutar ya da hepsini bir araya bırakır. Sonuç olarak, Application ınsights'ta hello İstek Ayrıntıları baktığınızda, her zaman hello istekle ilişkili telemetri öğelerinden birlikte görebilirsiniz. 

"Kullanıcı" tanımlamak uygulamalar için (diğer bir deyişle, en tipik web uygulamaları), hello örnekleme karar herhangi belirli bir kullanıcı için tüm telemetri korunur veya bırakılan anlamına gelir hello kullanıcı kimliği hello karmasını dayanır. Merhaba türleri (örneğin, web Hizmetleri) kullanıcıları tanımlamak olmayan uygulamalar için hello örnekleme karar üzerinde hello isteğin hello işlemi kimliği temel alır. Son olarak, tipleri (için örnek telemetri öğeleri http bağlam ile zaman uyumsuz iş parçacıklarından bildirilen) Ayarla kullanıcı veya işlem kimliğine sahip hello telemetri öğeleri için örnekleme yalnızca her tür telemetri öğeleri yüzdesini yakalar. 

Telemetri geri tooyou sunan, hello Application Insights hizmeti tarafından hello ölçümleri ayarlar hello zaman koleksiyonunun toocompensate veri noktaları eksik hello için kullanılan aynı örnekleme yüzdesini hello. Bu nedenle, Application ınsights'ta hello telemetri bakıldığında hello kullanıcılar için çok yakın toohello gerçek sayılar istatistiksel olarak doğru yakın görüyorsunuz.

Merhaba yaklaşık Hello doğruluğu büyük ölçüde yapılandırılmış hello örnekleme yüzdesi bağlıdır. Ayrıca, kullanıcıların çok sayıda genellikle benzer isteklerinden büyük miktarda işleyen uygulamalar için hello doğruluğu artırır. Üzerinde önemli bir yük ile çalışmıyor uygulamalar için diğer yandan Merhaba, bu uygulamalar genellikle kendi telemetri azaltma gelen veri kaybına neden olmadan hello kotanın kalsanız gönderebilirsiniz gibi örnekleme gerekli değildir. 

Application Insights telemetri türlerini, ölçümleri ve oturumlar itibaren bu türleri için örnek değil, hello duyarlık azalma yüksek oranda istenmeyen dikkat edin. 

### <a name="adaptive-sampling"></a>Uyarlamalı örnekleme
Uyarlamalı örnekleme hello SDK ' iletim izleyiciler hello geçerli hızı bir bileşen ekler ve hello örnekleme yüzde tootry toostay hello hedef en yüksek hızı içinde ayarlar. Merhaba ayarlama düzenli aralıklarla yeniden hesaplanır ve bir aktarım hızını giden hello hareketli ortalama üzerinde temel alır.

## <a name="sampling-and-hello-javascript-sdk"></a>Örnekleme ve hello JavaScript SDK'sı
Sabit oran örnekleme hello sunucu tarafı birlikte Hello istemci-tarafı (JavaScript) SDK katılan SDK. izlenmiş hello sayfaları yalnızca aynı kullanıcıların hangi hello için sunucu tarafı kendi kararı çok "içinde sample." Merhaba gelen istemci-tarafı telemetri gönderir Bu mantık, istemci - ve sunucu-tarafı boyunca kullanıcı oturumunun tasarlanmış toomaintain bütünlüğü içindir. Sonuç olarak, Application Insights herhangi belirli telemetri öğeden bu kullanıcıyı ya da oturumu için diğer tüm telemetri öğeleri bulabilirsiniz. 

*Yukarıda açıklanan şekilde my istemci ve sunucu tarafı telemetri Eşgüdümlü örnekleri gösterme.*

* Sabit oran örnekleme hem de sunucu ve istemci etkin olduğunu doğrulayın.
* Bu hello SDK sürüm 2.0 olduğundan emin olun veya üstü.
* Ayarladığınız onay hello aynı hello istemci ve sunucu yüzde örnekleme.

## <a name="frequently-asked-questions"></a>Sık Sorulan Sorular
*Bir basit "toplama her telemetri türü yüzdesi X" örnekleme değil neden?*

* Bu örnekleme yaklaşım ölçüm yaklaşık değerler, çok yüksek duyarlılık ile sağlayacak olsa da, kullanıcı, oturum ve tanılama için önemli olan istek başına özelliği toocorrelate Tanılama verileri bölün. Bu nedenle, works daha iyi "tüm telemetri öğeleri için yüzde X uygulama kullanıcılarının toplamak" veya "uygulama isteklerin yüzdesi X için tüm telemetri Topla" örnekleme mantığı. (Örneğin, arka plan zaman uyumsuz işleme) hello isteklerle ilişkili olmayan hello telemetri öğeleri için hello sonbaharda geri çok "toplama her telemetri türü için tüm öğeleri yüzdesi X." 

*Merhaba örnekleme yüzdesi zamanla değiştirebilir miyim?*

* Evet, Uyarlamalı örnekleme kademeli olarak hello örnekleme yüzde, şu anda hello telemetri hacmi gözlenen hello üzerinde tabanlı değiştirir.

*Sabit oran örnekleme kullanırsanız, nasıl anlarım hangi örnekleme yüzdesi çalışır hello Uygulamam için en iyi?*

* Uyarlamalı örnekleme ile toostart bir yoludur, üzerinde ne oranı çıkışı Bul kapatır (Merhaba soru yukarıda bakın), ve ardından anahtar toofixed hızında örnekleme hızı kullanma. 
  
    Aksi takdirde tooguess sahip. Geçerli telemetri kullanımınızı AI çözümlemek, herhangi diğer bir deyişle gerçekleşen ve hello toplanan telemetri hello hacmini tahmin azaltma inceleyin. Seçilen fiyatlandırma katmanınızı birlikte bu üç girişleri tooreduce hello hello toplanan telemetri hacmi ne kadar isteyebilirsiniz öneririz. Ancak, kullanıcılarınızın hello sayısı artan ya da diğer bazı shift telemetri hello birimindeki, tahmin geçersiz.

*Örnekleme yüzdesi çok düşük yapılandırırsanız ne olur?*

* Application Insights toocompensate hello görselleştirme hello veri birimi azaltılması için hello verilerin çalıştığında aşırı düşük örnekleme yüzdesi (over-aggressive örnekleme) hello yakın hello doğruluğunu azaltır. Ayrıca, tanılama deneyimi olumsuz, bazı sık başarısız hello etkilenebilir veya yavaş istekler çıkışı örneklenebilir.

*Örnekleme yüzdesi çok yüksek yapılandırırsanız ne olur?*

* Merhaba hello hacmi yetersiz bir düşüş yapılandırma çok yüksek örnekleme yüzdesi (değil agresif yeterince) sonuçlarında telemetri toplanır. Veri kaybı toothrottling ve Application Insights kullanma maliyetini Merhaba, toooverage ücretleri planlanan daha yüksek olabilir ilgili telemetri hala karşılaşabilirsiniz.

*Hangi platformlarda örnekleme kullanabilir miyim?*

* Merhaba SDK örnekleme gerçekleştirmiyor alım örnekleme otomatik olarak belirli bir birim üzerinde herhangi bir telemetri için ortaya çıkabilir. Bu, örneğin, uygulamanız Java sunucusu kullanıyorsa ya da hello ASP.NET SDK daha eski bir sürümü kullanıyorsanız çalışır.
* ASP.NET SDK sürüm 2.0.0 kullanıyorsanız ve üstünde (Azure veya kendi sunucusunda barındırılan), Uyarlamalı örnekleme varsayılan olarak alır ancak yukarıda açıklandığı gibi toofixed oranı geçiş yapabilirsiniz. Sabit oran örnekleme ile Merhaba tarayıcı SDK toosample otomatik olarak eşitleyen ilgili olaylar. 

*Her zaman toosee istiyorum nadir belirli olaylar vardır. Nasıl bunları hello örnekleme modülü alabilirim?*

* Yeni TelemetryConfiguration (Merhaba varsayılan etkin) ile TelemetryClient ayrı bir örneğini başlatır. Bu toosend nadir olaylarınızı kullanın.

## <a name="next-steps"></a>Sonraki adımlar
* [Filtreleme](app-insights-api-filtering-sampling.md) ne, SDK gönderir, daha katı denetim sağlayabilir.

