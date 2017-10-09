---
title: aaaDependency Azure Application Insights izleme | Microsoft Docs
description: "Application Insights ile şirket içi veya Microsoft Azure web uygulamanızın kullanımını, kullanılabilirliğini ve performansını analiz edin."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d15c4ca8-4c1a-47ab-a03d-c322b4bb2a9e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: e72f5465462ae8e64363cbbaa62911aff636c504
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-dependency-tracking"></a>Application Insights'ı ayarlayın: bağımlılık izleme
A *bağımlılık* uygulamanız tarafından çağrılan bir dış bileşendir. Bu genellikle HTTP veya bir veritabanı veya bir dosya sistemi kullanılarak adlı bir hizmettir. [Application Insights](app-insights-overview.md) uygulamanız için bağımlılıkları ne kadar bekleyeceğini ve ne sıklıkta bir bağımlılık araması başarısız ölçer. Belirli çağrıları araştırmak ve bunları toorequests ve özel durumları ilişkilendirebilirsiniz.

![örnek grafikler](./media/app-insights-asp-net-dependencies/10-intro.png)

Merhaba Giden kutusu bağımlılık İzleyicisi şu anda çağrıları toothese tür bağımlılığı raporları:

* Sunucu
  * SQL veritabanları
  * ASP.NET web ve HTTP tabanlı bağlamalar kullanan WCF hizmetleri
  * Yerel veya uzak HTTP çağrıları
  * Azure Cosmos DB, tablo, blob depolama ve sırası
* Web sayfaları
  * AJAX çağrıları

Kullanarak Works izleme [bayt kodu Araçları](https://msdn.microsoft.com/library/z9z62c29.aspx) seçili yöntemleri geçici. Performansa düzeydedir.

Kendi SDK çağrıları toomonitor diğer bağımlılıkları, hem de hello istemci ve sunucu kodu hello kullanarak da yazabilirsiniz [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

## <a name="set-up-dependency-monitoring"></a>Bağımlılık izleme işlevini ayarlama
Kısmi bağımlılık bilgi hello tarafından otomatik olarak toplanır [Application Insights SDK'sı](app-insights-asp-net.md). tooget tam veri hello hello ana bilgisayarı sunucusu için uygun aracısı yükleyin.

| Platform | Yükleme |
| --- | --- |
| IIS sunucusu |Her iki [sunucunuza Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md) veya [, uygulama too.NET framework 4.6 veya sonrası yükseltme](http://go.microsoft.com/fwlink/?LinkId=528259) hello yükleyip [Application Insights SDK'sı](app-insights-asp-net.md) uygulamanızda. |
| Azure Web Uygulaması |Web uygulama Denetim Masası'ndaki [açık hello Application Insights dikey penceresinde, web uygulama Denetim Masası'ndaki](app-insights-azure-web-apps.md) ve yükleme istenirse seçin. |
| Azure bulut hizmeti |[Kullanım başlangıç görevi](app-insights-cloudservices.md) veya [yükleme .NET framework 4.6 +](../cloud-services/cloud-services-dotnet-install-dotnet.md) |

## <a name="where-toofind-dependency-data"></a>Burada toofind bağımlılık verileri
* [Uygulama eşlemesi](#application-map) uygulama ve neighbouring bileşenleri arasındaki bağımlılıkları visualizes.
* [Performans, tarayıcı ve hata dikey pencereleri](#performance-and-blades) sunucu bağımlılık verileri göster.
* [Tarayıcılar dikey penceresinde](#ajax-calls) kullanıcılarınızın tarayıcılarından AJAX çağrıları gösterilir.
* [Yavaş ya da başarısız isteklerinden tıklatın aracılığıyla](#diagnose-slow-requests) kendi bağımlılık toocheck çağırır.
* [Analytics](#analytics) kullanılan tooquery bağımlılık verileri olabilir.

## <a name="application-map"></a>Uygulama Eşlemesi
Uygulama eşlemesi, uygulamanızın hello bileşenler arasındaki bir görsel Yardım toodiscovering bağımlılıklar olarak görev yapar. Merhaba, uygulamanızın telemetrisinden gelen otomatik olarak oluşturulur. Bu örnek uygulama tootwo dış hizmetler hello tarayıcı komut dosyalarından AJAX çağrılarını ve REST çağrılarını hello sunucusundan gösterir.

![Uygulama Eşlemesi](./media/app-insights-asp-net-dependencies/08.png)

* **Merhaba kutularından gidin** toorelevant bağımlılık ve diğer grafik.
* **PIN hello harita** toohello [Pano](app-insights-dashboards.md), burada bu tamamen işlevsel olacaktır.

[Daha fazla bilgi edinin](app-insights-app-map.md).

## <a name="performance-and-failure-blades"></a>Performans ve hata dikey pencereleri
Merhaba performans dikey penceresinde hello sunucu uygulama tarafından oluşturulan bağımlılık çağrıları hello süresini gösterir. Bir Özet Grafik ve çağrısı tarafından bölümlenmiş bir tablo yok.

![Performans dikey bağımlılık grafikleri](./media/app-insights-asp-net-dependencies/dependencies-in-performance-blade.png)

Merhaba Özet grafikleri veya hello Tablo öğeleri toosearch ham oluşumları bu çağrıları tıklayın.

![Bağımlılık çağrısı örnekleri](./media/app-insights-asp-net-dependencies/dependency-call-instance.png)

**Hata sayısı** hello üzerinde gösterilen **hataları** dikey. Merhaba aralığı 200-399, veya bilinmeyen olmayan dönüş kodları hatasıdır.

> [!NOTE]
> **% 100 hataları?** -Bu, büyük olasılıkla kısmi bağımlılık verileri yalnızca aldıklarından gösterir. Çok ihtiyacınız[uygun tooyour platform izleme bağımlılık ayarlamak](#set-up-dependency-monitoring).
>
>

## <a name="ajax-calls"></a>AJAX çağrıları
Merhaba tarayıcılar dikey penceresinde hello süresi gösterir ve hata oranı AJAX çağrıları [web sayfalarında JavaScript](app-insights-javascript.md). Bunlar bağımlılıklar olarak gösterilir.

## <a name="diagnosis"></a>Yavaş istekler tanılama
Her isteği olayı hello bağımlılık çağrıları ile ilişkili olduğundan, özel durumlar ve uygulamanızı işlerken izlenen diğer olayları isteği Merhaba. Bu nedenle bazı istekleri hatalı gerçekleştiriyorsanız, bir bağımlılık tooslow yanıtlarının son olup olmadığını bulabilirsiniz.

Şimdi örneği, yol gösterir.

### <a name="tracing-from-requests-toodependencies"></a>İstekleri toodependencies izleme
Merhaba performans dikey penceresini açın ve istekleri hello kılavuz bakın:

![Ortalamalar ve sayıları istekleriyle listesi](./media/app-insights-asp-net-dependencies/02-reqs.png)

Merhaba üst biri çok uzun sürüyor. Biz hello zamanın nerede harcandığına çıkışı bulmak, görelim.

Bu satır toosee ayrı istek olayları tıklatın:

![İstek örnekleri listesi](./media/app-insights-asp-net-dependencies/03-instances.png)

Daha fazla ve toohello uzak bağımlılık çağrıları ilgili toothis isteği kaydırarak herhangi uzun süre çalışan örnek tooinspect tıklatın:

![Çağrıları tooRemote bağımlılıkları bulun, olağan dışı süre tanımla](./media/app-insights-asp-net-dependencies/04-dependencies.png)

Bu istek bir çağrı tooa yerel hizmetinde harcanan zamanı hello bakım çoğu gibi görünüyor.

Bu satır tooget daha fazla bilgi seçin:

![Bu uzak bağımlılık tooidentify hello sorunlu tıklatın](./media/app-insights-asp-net-dependencies/05-detail.png)

Bu hello sorunu olduğu görülüyor. Biz hello sorun pinpointed, biz yalnızca artık neden bu çağrı çok uzun sürüyor çıkışı toofind şekilde gerekir.

### <a name="request-timeline"></a>İstek zaman çizelgesi
Farklı bir durumda, özellikle uzun hiçbir bağımlılık çağrısı yoktur. Ancak toohello Zaman Çizelgesi görünümüne geçiş yaparak hello gecikme bizim iç işlem oluştuğu görebiliriz:

![Çağrıları tooRemote bağımlılıkları bulun, olağan dışı süre tanımla](./media/app-insights-asp-net-dependencies/04-1.png)

Olduğu anlaşılıyor toobe büyük bir boşluk hello ilk bağımlılık çağrısından sonra diğer bir deyişle neden biz bizim kod toosee görünmelidir şekilde.

### <a name="profile-your-live-site"></a>Canlı sitenizi profil

Fikir burada hello zaman gider mi? Merhaba [Application Insights profil oluşturucu](app-insights-profiler.md) HTTP tooyour Canlı site çağırır ve hangi işlevleri kodunuzda gösterir izlemeleri hello en uzun zaman aldı.

## <a name="failed-requests"></a>Başarısız istekler
Başarısız olan istekler başarısız çağrılar toodependencies ile ilişkili olabilir. Yeniden, biz hello sorun aşağı tootrack aracılığıyla tıklatabilirsiniz.

![Merhaba başarısız isteklerin grafiği tıklatın](./media/app-insights-asp-net-dependencies/06-fail.png)

Başarısız bir istek tooan geçişi tıklatın ve onun ilişkili olay arayın.

![Bir istek türünü tıklatın, hello örnek tooget tooa farklı görünümünü Merhaba aynı örneği, tooget özel durum ayrıntıları tıklatın.](./media/app-insights-asp-net-dependencies/07-faildetail.png)

## <a name="analytics"></a>Analiz
Merhaba bağımlılıkları izleyebilirsiniz [günlük analizi sorgu dili](https://docs.loganalytics.io/). Bazı örnekler aşağıda verilmiştir.

* Tüm başarısız bağımlılık çağrıları bulun:

```

    dependencies | where success != "True" | take 10
```

* AJAX çağrıları bulun:

```

    dependencies | where client_Type == "Browser" | take 10
```

* İsteklerle ilişkili bağımlılık çağrıları bulun:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type != "Browser"
    | join (requests | where timestamp > ago(1d))
      on operation_Id  
```


* Sayfa görünümleri ile ilişkili Bul AJAX çağrıları:

```

    dependencies
    | where timestamp > ago(1d) and  client_Type == "Browser"
    | join (browserTimings | where timestamp > ago(1d))
      on operation_Id
```



## <a name="custom-dependency-tracking"></a>Özel bağımlılık izleme
Merhaba standart bağımlılık izleme modülü veritabanları ve REST API'leri gibi dış bağımlılıklar otomatik olarak bulur. Ancak, bazı ek bileşenleri toobe kabul hello aynı isteyebilirsiniz yolu.

Bağımlılık bilgi gönderir kod yazabilirsiniz kullanarak, hello aynı [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency) hello standart modülleri tarafından kullanılır.

Örneğin, bir derleme kodunuzu yapı, kendiniz yazmak alamadık, size tüm hello çağrıları tooit zaman hangi katkı kolaylaştırır tooyour yanıt çıkışı toofind zaman. toohave hello bağımlılık Application Insights, grafiklerde görüntülenen bu verileri gönder kullanarak `TrackDependency`.

```C#

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

Tooswitch hello standart bağımlılık izleme modülü kapatmak isterseniz, hello başvuru tooDependencyTrackingTelemetryModule kaldırmak [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md).

## <a name="troubleshooting"></a>Sorun giderme
*Bağımlılık başarı bayrağı her zaman true veya false gösterir.*

*SQL sorgu tam olarak gösterilmez.*

* Merhaba SDK toohello en son sürümüne yükseltme. .NET sürüm 4.6'den az ise:
  * IIS ana: yükleme [Application Insights Aracısı](app-insights-monitor-performance-live-website-now.md) hello ana bilgisayar sunucuları üzerinde.
  * Azure web uygulaması: açık Application Insights sekmesinde hello web uygulama Denetim Masası'nda ve Application Insights yükleyin.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Sonraki adımlar
* [Özel durumlar](app-insights-asp-net-exceptions.md)
* [Kullanıcı ve sayfa verileri](app-insights-javascript.md)
* [Kullanılabilirlik](app-insights-monitor-web-app-availability.md)
