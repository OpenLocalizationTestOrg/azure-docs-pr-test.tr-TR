---
title: "aaaLive özel ölçümleri ve tanılama Azure Application Insights'olan ölçümleri akış | Microsoft Docs"
description: "Özel ölçümleri ile gerçek zamanlı web uygulamanızı izlemek ve canlı akış hataları, izlemeleri ve olayları ile ilgili sorunları tanılamak."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a>Canlı ölçümleri akış: 1 saniye gecikme süresi ile Tanıla & zle 

Merhaba göndermeyi Kalp canlı, üretim web uygulamanızın Canlı ölçümleri akıştan kullanarak araştırma [Application Insights](app-insights-overview.md). Seçin ve herhangi bir rahatsızlık tooyour hizmeti olmadan gerçek zamanlı ölçümleri ve performans sayaçları toowatch filtreleyebilirsiniz. Yığın izlemeleri örnek başarısız istekler ve özel durumları inceleyin. İle birlikte [profil oluşturucu](app-insights-profiler.md), [anlık görüntü hata ayıklayıcı](app-insights-snapshot-debugger.md), ve [performans testi](app-insights-monitor-web-app-availability.md#performance-tests), Canlı ölçümleri akış için canlı web güçlü ve bozucu bir tanılama aracı sağlar Site.

Canlı ölçümleri akış ile şunları yapabilirsiniz:

* Serbest olsa da, bir düzeltme doğrulamak performans ve hata sayısını izlerken tarafından.
* Sorunlarını tanılamak ve test yükleri hello etkisini izleme Canlı. 
* Belirli test oturumlarını odaklanmak veya seçerek ve toowatch istediğiniz hello ölçümleri filtreleme bilinen sorunlar filtreleyebilirsiniz.
* Özel durum izlemeleri olduğu alın.
* Filtrelerle deneme toofind hello en uygun KPI'ları.
* Performans sayacı Canlı herhangi bir Windows izleyin.
* Kolayca sorunları sahip bir sunucu tanımlayın ve bu sunucu tüm hello KPI ve canlı akış toojust filtre.

[![Canlı ölçümleri akış video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)

Ölçümler bir canlı akışı hello Bulut veya şirket içi çalıştıran ASP.NET uygulamaları üzerinde şu anda kullanılabilir değil. 

## <a name="get-started"></a>başlarken

1. Henüz yapmadıysanız [Application Insights yüklü](app-insights-asp-net.md) , ASP.NET web uygulamanızda veya [Windows server uygulaması](app-insights-windows-services.md), bunu şimdi yapın. 
2. **Güncelleştirme toohello en son sürümü** hello Application Insights paketi. Visual Studio'da, projenize sağ tıklayın ve seçin **Manage Nuget paketleri**. Açık hello **güncelleştirmeleri** sekmesi, onay **dahil et**ve tüm hello Microsoft.ApplicationInsights.* paketlerini seçin.

    Uygulamanızı yeniden dağıtın.

3. Merhaba, [Azure portal](https://portal.azure.com), uygulamanız için hello Application Insights kaynağı ve ardından canlı akış açın.

4. [Güvenli hello denetim kanalı](#secure-the-control-channel) müşteri adları gibi hassas verileri, filtrelerinizi kullandığınız.


![Merhaba genel bakış dikey penceresinde, canlı akış'a tıklayın.](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a>Veri yok mu? Sunucu güvenlik duvarının denetleyin

Merhaba denetleyin [bağlantı noktaları için Canlı ölçümleri akış giden](app-insights-ip-addresses.md#outgoing-ports) sunucularınızı hello Güvenlik Duvarı'nda açıktır. 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a>Ölçümler bir canlı akışı nasıl ölçüm Gezgini ve analizi farkı nedir?

| |Canlı akış | Ölçüm Gezgini ve analizi |
|---|---|---|
|Gecikme süresi|Bir saniye içinde görüntülenen verileri|Dakika boyunca bir araya getirilir|
|Hiçbir bekletme|Merhaba grafiğidir ve sonra atılır verileri devam eder.|[90 gün boyunca tutulur veri](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|İsteğe bağlı|Canlı ölçümleri açarken veri akışı|Merhaba SDK yüklü ve etkin olduğunda veriler gönderilir|
|Ücretsiz|Canlı akış verileri için herhangi bir ücret alınmaz|Çok konu[fiyatlandırma](app-insights-pricing.md)
|Örnekleme|Seçilen tüm ölçümler ve sayaçlar aktarılır. Hataları ve Yığın izlemeleri örneklenen. TelemetryProcessors uygulanmaz.|Olayları olabilir [örneklenen](app-insights-api-filtering-sampling.md)|
|Denetim kanalı|Filtre denetimi sinyalleri toohello SDK gönderilir. Öneririz [bu kanal güvenli](#secure-channel).|Tek yönlü iletişim toohello portalı|


## <a name="select-and-filter-your-metrics"></a>Seçin ve ölçümlerinizi filtre

(Klasik kullanılabilir ASP.NET uygulamaları ile en son SDK hello.)

Merhaba Portalı'ndan herhangi Application Insights telemetriyi rasgele filtreleri uygulayarak özel KPI dinamik izleyebilirsiniz. Ne zaman, fare hello grafikleri hiçbirini üzerinde gösterir hello filtre denetimi'ı tıklatın. Grafik aşağıdaki hello URL ve süre öznitelikleri filtreleri ile özel bir istek sayısı KPI Çizdirmek. Filtrelerinizi hello bir canlı akış zamanında herhangi bir noktada belirtilen hello ölçütlerle eşleşen telemetri gösteren akış Önizleme bölümü ile doğrulayın. 

![Özel istek KPI](./media/app-insights-live-stream/live-stream-filteredMetric.png)

Sayısını başka bir değer izleyebilirsiniz. Merhaba seçenekler hello herhangi Application Insights telemetri olabilir akış türüne bağlıdır: istekleri, bağımlılıkları, özel durumlar, izlemeleri, olayları veya ölçümleri. Bu, kendi olabilir [özel ölçüm](app-insights-api-custom-events-metrics.md#properties):

![Değer seçenekleri](./media/app-insights-live-stream/live-stream-valueoptions.png)

Ayrıca tooApplication Insights telemetri, da herhangi bir Windows performans sayacı hello akış seçeneklerden birini seçerek ve sağlayan hello performans sayacı hello adı izleyebilirsiniz.

Canlı ölçümleri iki noktalarda toplanır: her sunucuda yerel olarak ve tüm sunucular genelinde. Merhaba varsayılan hello ilgili aşağı açılan listeler diğer seçenekler seçerek ya da değiştirebilirsiniz.

## <a name="sample-telemetry-custom-live-diagnostic-events"></a>Örnek Telemetri: Özel Canlı Tanılama Olayları
Varsayılan olarak, başarısız olan istekler ve bağımlılık çağrıları, özel durumlar, olayları ve izlemeleri örnekleri hello canlı akış olayların gösterir. Merhaba filtre simgesini toosee uygulanan hello ölçütlerini herhangi bir noktada zamanında'ı tıklatın. 

![Varsayılan Canlı akış](./media/app-insights-live-stream/live-stream-eventsdefault.png)

Olarak ölçümleri ile tüm rasgele ölçütleri tooany hello Application Insights telemetri türlerinin belirtebilirsiniz. Bu örnekte, biz belirli bir istek hataları, izlemeler ve olaylar seçmiş olursunuz. Biz de tüm özel durumlar ve bağımlılık hataları seçmiş olursunuz.

![Özel canlı akış](./media/app-insights-live-stream/live-stream-events.png)

Not: Özel durum iletisi tabanlı ölçütü için şu anda hello en dıştaki özel durum iletisi kullanın. Örnek, önceki hello içinde hello zararsız iç özel durum iletisi durumla çıkışı toofilter (aşağıdaki hello "<--" sınırlayıcı) "Merhaba istemci bağlantısı kesildi." Kullanım bir ileti değil-"İstek içeriği okunurken hata oluştu" ölçütler içeriyor.

Merhaba ayrıntılarını tıklayarak akış canlı bir öğeyi hello bakın. Tıklayarak ya da akış hello duraklatabilirsiniz **duraklatma** yalnızca aşağı kaydırma veya bir öğeyi tıklatarak. Canlı akış geri toohello üst kaydırma sonra devam eder veya öğelerin hello sayaç tıklayarak durdurulduğundan sırasında toplanan.

![Örneklenen Canlı hataları](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a>Sunucu örneği tarafından filtre

Belirli bir sunucu rolü örneği toomonitor istiyorsanız, sunucu tarafından filtre uygulayabilirsiniz.

![Örneklenen Canlı hataları](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a>SDK gereksinimleri
Özel Canlı ölçümleri akış sürüm 2.4.0-beta2 bulunan ya da daha yeni olan [Application Insights SDK Web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/). NuGet Paket Yöneticisi'nden tooselect "Yayın öncesi Ekle" seçeneğini unutmayın.

## <a name="secure-hello-control-channel"></a>Merhaba denetim kanalının güvenliğini sağlayın.
Merhaba özel filtreler ölçütlere geri toohello Canlı ölçümleri bileşen hello Application Insights SDK'sı gönderilir. Hello filtreleri olası customerIDs gibi hassas bilgiler içerebilir. Merhaba kanal gizli bir API anahtarı ile ayrıca toohello izleme anahtarını güvenli hale getirebilirsiniz.
### <a name="create-an-api-key"></a>API anahtarı oluşturma

![API anahtarı oluşturma](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a>API anahtar tooConfiguration Ekle
Merhaba applicationınsights.config dosyasında hello AuthenticationApiKey toohello QuickPulseTelemetryModule ekleyin:
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
Veya isteğe bağlı olarak kod içinde QuickPulseTelemetryModule hello üzerinde ayarlayın:

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

Ancak, algılar ve tüm bağlı sunucular hello güveniyorsanız hello özel filtreler kimliği doğrulanmış hello kanal olmadan deneyebilirsiniz. Bu seçenek altı ay için kullanılabilir. Bu geçersiz kılma kez her yeni bir oturum gereklidir veya ne zaman yeni bir sunucu gelir çevrimiçi.

![Canlı ölçümleri kimlik doğrulama seçenekleri](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
>Hello filtre ölçütlerini CustomerID gibi olası hassas bilgileri girmeden önce kimlik doğrulaması hello kanalı ayarlamanız önerilir.
>

## <a name="generating-a-performance-test-load"></a>Performans testi yükleme oluşturma

İsterseniz toowatch hello etkisini bir iş yükünün artırmak, kullanım hello performans testi dikey. Bu, eşzamanlı kullanıcıların sayısı gelen istekleri benzetimini yapar. Ya da "el ile testleri" çalıştırabilirsiniz (ping testleri) tek bir URL veya çalıştırabilirsiniz bir [çok adımlı web performans testi](app-insights-monitor-web-app-availability.md#multi-step-web-tests) (aynı kullanılabilirlik olarak şekilde test hello) karşıya yükleyin.

> [!TIP]
> Merhaba performans testi oluşturduktan sonra hello test açın ve canlı akış dikey penceresinde ayrı windows hello. Performans testi başlatır ve izleme canlı akış hello hello zaman sıraya görebilirsiniz aynı anda.
>


## <a name="troubleshooting"></a>Sorun giderme

Veri yok mu? Uygulamanızı korunan bir ağda ise: Canlı ölçümleri akış diğer Application Insights telemetri daha farklı bir IP adreslerini kullanır. Emin olun [bu IP adreslerinden](app-insights-ip-addresses.md) duvarınızda açıktır.



## <a name="next-steps"></a>Sonraki adımlar
* [Application Insights ile kullanım izleme](app-insights-web-track-usage.md)
* [Tanılama aramayı kullanma](app-insights-diagnostic-search.md)
* [Profil Oluşturucu](app-insights-profiler.md)
* [Anlık görüntü hata ayıklayıcı](app-insights-snapshot-debugger.md)
