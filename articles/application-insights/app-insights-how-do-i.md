---
title: aaaHow yedeklerim... Azure Application Insights'ta | Microsoft Docs
description: "Application ınsights'ta SSS."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a>Application Insights’ta nasıl ... yapabilirim?
## <a name="get-an-email-when-"></a>Bir e-posta almak zaman...
### <a name="email-if-my-site-goes-down"></a>Sitem devre dışı kalırsa e-posta
Ayarlanmış bir [kullanılabilirlik web testi](app-insights-monitor-web-app-availability.md).

### <a name="email-if-my-site-is-overloaded"></a>Sitem aşırı yüklüyse e-posta
Ayarlanmış bir [uyarı](app-insights-alerts.md) üzerinde **sunucu yanıt süresi**. 1 ve 2 saniye arasında bir eşik çalışması gerekir.

![](./media/app-insights-how-do-i/030-server.png)

Uygulamanızı hata kodları döndürme yükü belirtileri da gösterebilir. Bir uyarı ayarlamak **başarısız istekler**.

Tooset bir uyarı istiyorsanız **sunucu özel durumları**, toodo olabilir [bazı ek kurulum](app-insights-asp-net-exceptions.md) sipariş toosee veri.

### <a name="email-on-exceptions"></a>Özel durumları e-posta
1. [Özel durum izleme işlevini ayarlama](app-insights-asp-net-exceptions.md)
2. [Bir uyarı ayarlamak](app-insights-alerts.md) ölçüm hello üzerinde özel durum sayısı

### <a name="email-on-an-event-in-my-app"></a>Uygulamam olayda e-posta
Şimdi belirli bir olay gerçekleştiğinde tooget bir e-posta istediğiniz varsayalım. Application Insights sunmaz bu tesis doğrudan, ancak bunu [bir eşik ölçüm kestiği olduğunda bir uyarı gönder](app-insights-alerts.md).

Uyarılar, üzerinde ayarlanabilir [özel ölçümleri](app-insights-api-custom-events-metrics.md#trackmetric)olmayan özel olaylar ancak. Merhaba olay gerçekleştiğinde bazı kod tooincrease ölçüm yazma:

    telemetry.TrackMetric("Alarm", 10);

Ya da:

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

İki durumlu uyarıları sahip olduğundan, toohave sona erdi hello uyarı göz önüne aldığınızda düşük bir değere toosend vardır:

    telemetry.TrackMetric("Alarm", 0.5);

Grafik oluşturma [ölçüm Gezgini](app-insights-metrics-explorer.md) toosee, uyarısı:

![](./media/app-insights-how-do-i/010-alarm.png)

Şimdi Hello ölçüm kısa bir süre için orta değer geçtiğinde bir uyarı toofire ayarlayın:

![](./media/app-insights-how-do-i/020-threshold.png)

Dönem toohello minimum ortalaması hello ayarlayın.

E-postaları hello ölçüm yukarıda gittiğinde hem hello eşiğin altına elde edersiniz.

Bazı noktaları tooconsider:

* Bir uyarı iki durumlu ("uyarı" ve "sağlıklı") sahiptir. yalnızca bir ölçü alındığında hello durumu değerlendirilir.
* Yalnızca hello durumu değiştiğinde bir e-posta gönderilir. Toosend sahip olmanızın nedeni budur yüksek ve düşük değer ölçümleri.
* tooevaluate hello uyarı, hello ortalama süre önceki hello alınan hello değerlerini alınır. Ölçüm alınan her zaman, e-postaları ayarladığınız hello süresinden daha sık gönderilmesini şekilde gerçekleşir.
* Hem "uyarı" ve "sağlıklı" e-postaları gönderilen olduğundan, tek adımda olayınızın iki durumlu koşul olarak yeniden düşünüyorum tooconsider isteyebilirsiniz. Örneğin, "işi tamamlandı" olay yerine hello başlangıç ve bitiş bir işin e-postaları nereden bir "devam eden işi" koşula sahipsiniz.

### <a name="set-up-alerts-automatically"></a>Uyarıları otomatik olarak ayarla
[PowerShell toocreate yeni uyarıları kullanın](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a>PowerShell tooManage Application Insights kullanın
* [Yeni kaynaklar oluşturma](app-insights-powershell-script-create-resource.md)
* [Yeni uyarılar oluştur](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a>Farklı sürümlerdeki ayrı telemetri

* Bir uygulama içinde birden çok rol: tek bir Application Insights kaynağı kullanın ve filtre cloud_Rolename üzerinde. [Daha fazla bilgi](app-insights-monitor-multi-role-apps.md)
* Geliştirme, test ve yayın sürümleri ayırma: farklı Application Insights kaynakları kullanın. Web.config hello araçları anahtarları seçin. [Daha fazla bilgi](app-insights-separate-resources.md)
* Sürümleri derleme raporlama: telemetri Başlatıcı kullanarak özellik ekleme. [Daha fazla bilgi](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a>Arka uç sunucularının ve Masaüstü uygulamaları izleme
[Kullanım hello Windows Server SDK Modülü](app-insights-windows-desktop.md).

## <a name="visualize-data"></a>Verileri görselleştirin
#### <a name="dashboard-with-metrics-from-multiple-apps"></a>Birden çok uygulamalardan ölçümlerle Panosu
* İçinde [ölçüm Gezgini](app-insights-metrics-explorer.md), grafiğinizi özelleştirmek ve sık kullanılan olarak Kaydet. Toohello Azure Pano sabitleyin.

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a>Diğer kaynaklardan ve Application Insights verilerle Panosu
* [Telemetri tooPower BI verme](app-insights-export-power-bi.md).

Veya

* SharePoint web bölümleri verileri görüntüleme panonuz olarak SharePoint kullanın. [Sürekli dışarı aktarma ve akış analizi tooexport tooSQL kullanmak](app-insights-code-sample-export-sql-stream-analytics.md).  PowerView tooexamine hello veritabanını kullanın ve bir SharePoint web bölümü için PowerView oluşturun.

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a>Anonim veya kimliği doğrulanmış kullanıcıları Filtrele
Kullanıcılarınız oturum açarsa, hello ayarlayabilirsiniz [kullanıcı kimliği kimlik doğrulaması](app-insights-api-custom-events-metrics.md#authenticated-users). (Bunu otomatik olarak gerçekleşmez.)

Sonra şunları yapabilirsiniz:

* Belirli bir kullanıcı kimliklerine göre ara

![](./media/app-insights-how-do-i/110-search.png)

* Ölçümleri tooeither anonim veya kimliği doğrulanmış kullanıcıları Filtrele

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a>Özellik adlarını ve değerleri değiştirme
Oluşturma bir [filtre](app-insights-api-filtering-sampling.md#filtering). Bu, değiştirmek veya uygulama tooApplication Öngörüler gönderilmeden önce telemetri filtre sağlar.

## <a name="list-specific-users-and-their-usage"></a>Liste belirli kullanıcılar ve kullanımı
Yalnızca çok istiyorsanız[belirli kullanıcılar için arama](#search-specific-users), hello ayarlayabilirsiniz [kullanıcı kimliği kimlik doğrulaması](app-insights-api-custom-events-metrics.md#authenticated-users).

Hangi sayfaların gibi verileri sahip kullanıcıların listesini istiyorsanız, bunlar bakmak veya ne sıklıkta oturum, iki seçeneğiniz vardır:

* [Kümesi kimliği doğrulanmış kullanıcı kimliği](app-insights-api-custom-events-metrics.md#authenticated-users), [tooa veritabanı dışarı](app-insights-code-sample-export-sql-stream-analytics.md) ve araçları tooanalyze kullanın uygun kullanıcı verilerinizi vardır.
* Az sayıda kullanıcılar varsa, özel olaylar veya ölçümleri, ölçüm değeri veya olay adı ve ayarı hello kullanıcı kimliği özelliği olarak hello gibi hello verileri kullanarak gönderir. tooanalyze sayfa görünümleri hello standart JavaScript trackPageView çağrısı değiştirin. tooanalyze sunucu tarafı telemetri, bir telemetri Başlatıcı tooadd hello kullanıcı kimliği tooall sunucu telemetri kullanın. Bundan sonra filtre ve segment ölçümleri ve hello kullanıcı kimliği arama yapabilirsiniz.

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a>My uygulama tooApplication Öngörüler trafiğini azaltır
* İçinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), gerek yoktur, herhangi bir modül gibi hello performans sayacı Toplayıcı devre dışı bırakın.
* Kullanım [örnekleme ve filtre](app-insights-api-filtering-sampling.md) hello SDK adresindeki.
* Web sayfalarınızda Ajax çağrıları her sayfa görünümü için bildirilen hello sayısını sınırlayın. Sonra hello kod parçacığında bulunan `instrumentationKey:...` , Ekle: `,maxAjaxCallsPerView:3` (veya uygun rakam).
* Kullanıyorsanız, [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), ölçüm değerleri toplu hello toplamını hello sonuç göndermeden önce işlem. Bir aşırı yüklemesini için sağlayan TrackMetric() yoktur.

Daha fazla bilgi edinmek [fiyatlandırma ve kotaları](app-insights-pricing.md).

## <a name="disable-telemetry"></a>Telemetri devre dışı bırak
çok**dinamik olarak durdurmak ve başlatmak** hello toplama ve hello sunucusundan telemetri iletimini:

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



çok**seçili standart toplayıcıları devre dışı** - örnek, performans sayaçları, HTTP isteklerini veya bağımlılıkları - silin veya açıklama hello ilgili satırlarında çıkışı [Applicationınsights.config](app-insights-api-custom-events-metrics.md). Örneğin, kendi TrackRequest veri toosend istiyorsanız bunu.

## <a name="view-system-performance-counters"></a>Görünüm sistem performans sayaçları
Merhaba arasında ölçümleri Gezgini'nde Göster ölçümleri sistem performans sayaçları kümesidir. Başlıklı önceden tanımlanmış bir dikey pencere yok **sunucuları** birkaç görüntüler.

![Application Insights kaynağınıza açın ve sunucuları'nı tıklatın](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a>Hiçbir performans sayacı verilerini görürseniz
* **IIS server** kendi makine veya bir VM üzerinde. [Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md).
* **Azure web sitesi** -performans sayaçları henüz desteklemiyoruz. Hello Azure web sitesi Denetim Masası standart bir parçası olarak alabilirsiniz çeşitli ölçümleri vardır.
* **UNIX sunucusu** - [collectd yükleyin](app-insights-java-collectd.md)

### <a name="toodisplay-more-performance-counters"></a>toodisplay daha fazla performans sayaçları
* İlk olarak, [yeni bir grafik ekleyin](app-insights-metrics-explorer.md) ve hello sayaç hello temel, sunduğumuz ayarlanmış olup olmadığını görebilirsiniz.
* Aksi durumda, [eklemek hello performans sayacı modülü tarafından toplanan hello sayaç toohello kümesi](app-insights-performance-counters.md).
