---
title: "JavaScript için aaaAzure Application Insights web uygulamaları | Microsoft Docs"
description: "Sayfa görünümü ve oturum sayısını, web istemci verilerini alın ve kullanım desenlerini izleyin. JavaScript web sayfalarında özel durumları ve performans sorunlarını yakalayın."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Web sayfaları için Application Insights
Merhaba performans ve web sayfası veya uygulama kullanımı hakkında bilgi edinin. Eklerseniz [Application Insights](app-insights-overview.md) tooyour sayfa komut dosyası, sayfa yükler ve AJAX çağrıları, sayıları ve tarayıcı özel durumlar ve AJAX hataları yanı sıra kullanıcıları ve oturum sayıları ayrıntılarını zamanlamaları alın. Bunların tümü sayfaya, istemci işletim sistemi ve tarayıcı sürümüne, coğrafi konuma ve başka boyutlara göre kesimlere ayrılmıştır. Hata sayısı veya yavaş sayfa yüklemesi hakkında uyarı ayarlayabilirsiniz. Ve JavaScript kodunuzda izleme çağrıları ekleyerek hello farklı özellikler, web sayfası uygulamanızın nasıl kullanıldığını izleyebilirsiniz.

Application Insights tüm web sayfalarıyla kullanılabilir; kısa bir JavaScript eklemeniz yeterlidir. Web hizmetinizin [Java](app-insights-java-get-started.md) veya [ASP.NET](app-insights-asp-net.md) olması halinde, sunucunuzdan ve istemcilerinizden telemetri tümleştirebilirsiniz.

![portal.azure.com adresinde uygulamanızın kaynağını açıp Tarayıcı’ya tıklayın](./media/app-insights-javascript/03.png)

Bir abonelik gerekiyor[Microsoft Azure](https://azure.com). Takımınızın kurumsal bir aboneliği varsa, Microsoft Account tooit hello sahibi tooadd isteyin. Geliştirme ve küçük ölçekli kullanımın herhangi bir maliyeti olmayacaktır.

## <a name="set-up-application-insights-for-your-web-page"></a>Web sayfalarınız için Application Insights’ı ayarlama
Hello yükleyicisi kod parçacığını tooyour web sayfaları, aşağıdaki şekilde ekleyin.

### <a name="open-or-create-application-insights-resource"></a>Application Insights kaynağı açma veya oluşturma
sayfanızın performansı ve kullanımı hakkında verilerin görüntülendiği Hello Application Insights kaynağı değil. 

[Azure portalda](https://portal.azure.com) oturum açın.

Uygulamanızın hello sunucu tarafı için izlemeyi zaten ayarladıysanız zaten bir kaynağa sahip:

![Gözat, Geliştirici Hizmetleri, Application Insights’ı seçin.](./media/app-insights-javascript/01-find.png)

Yoksa, bir tane oluşturun:

![Yeni, Geliştirici Hizmetleri, Application Insights’ı seçin.](./media/app-insights-javascript/01-create.png)

*Hala sorularınız mı var?* [Kaynak oluşturma hakkında daha fazla bilgi](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Merhaba SDK komut dosyası tooyour uygulama ya da web sayfalarına ekleme
Hızlı Başlangıç'ta web sayfaları için hello betik alın:

![Uygulama genel bakış dikey pencerenizde, Hızlı Başlat'ı seçin, web sayfalarımı kod toomonitor alın. Merhaba betiği kopyalayın.](./media/app-insights-javascript/02-monitor-web-page.png)

Merhaba hemen önce Hello komut dosyası Ekle `</head>` etiketi her sayfada tootrack istiyor. Web sitenizi bir ana sayfa varsa, hello betiği buraya koyabilirsiniz. Örneğin:

* ASP.NET MVC projesinde `View\Shared\_Layout.cshtml` içine koyabilirsiniz
* Bir SharePoint sitesinde hello Denetim Masası'nda açmak [Site Ayarları / ana sayfa](app-insights-sharepoint.md).

Hello betik hello veri tooyour Application Insights kaynağı yönlendirir hello izleme anahtarını içerir. 

([Hello betik daha ayrıntılı açıklaması. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(İyi bilinen web sayfası altyapısı kullanıyorsanız, Application Insights bağdaştırıcılarını araştırın. Örneğin, [AngularJS modülü](http://ngmodules.org/modules/angular-appinsights) var.)*

## <a name="detailed-configuration"></a>Ayrıntılı yapılandırma
Çoğunlukla gerekmese de, ayarlayabileceğiniz birkaç [parametre](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) vardır. Örneğin, devre dışı bırakın ya da (tooreduce trafiği) sayfa görünümü rapor edilen Ajax çağrılarını hello sayısını sınırlayın. Veya toplu hale olmadan hata ayıklama modu toohave telemetri taşıma hello ardışık düzeninden hızlı bir şekilde ayarlayabilirsiniz.

tooset Bu parametreler hello kod parçacığında bu satırı arayın ve sonra virgülle ayrılmış daha fazla öğe ekleyin:

    })({
      instrumentationKey: "..."
      // Insert here
    });

Merhaba [kullanılabilir parametrelerin](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) içerir:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Uygulamanızı çalıştırma
Web uygulamanızı çalıştırmak ve kullanacağını bir toogenerate telemetri ve bir birkaç saniye bekleyin. Her iki çalışma hello kullanarak şunları yapabilirsiniz **F5** anahtar geliştirme makinenizde yayımlayabilir ve kullanıcıların bunu yürütmesine olanak tanır.

Bir web uygulaması tooApplication Öngörüler gönderiyor toocheck hello telemetri istiyorsanız, tarayıcınızın hata ayıklama araçlarını kullanın (**F12** birçok tarayıcılarda). Veri toodc.services.visualstudio.com gönderilir.

## <a name="explore-your-browser-performance-data"></a>Tarayıcı performans verilerinizi araştırma
Açık hello tarayıcı dikey tooshow kullanıcılarınızın tarayıcılarından performans verilerini bir araya getirilir.

![portal.azure.com adresinde uygulamanızın kaynağını açıp Ayarlar, Tarayıcı’ya tıklama](./media/app-insights-javascript/03.png)

*Henüz veri yok mu? Tıklatın **yenileme** hello sayfanın üst kısmındaki hello. Hala hiçbir şey yok mu? Bkz. [Sorun giderme](app-insights-troubleshoot-faq.md).*

Merhaba tarayıcı dikey penceresi bir [ölçüm Gezgini dikey](app-insights-metrics-explorer.md) hazır filtrelerin ve grafik seçimlerinin ile. Ve hello sonucu sık kullanılan olarak kaydetmek istiyorsanız hello zaman aralığını, filtreleri ve grafik yapılandırmasını düzenleyebilir. Tıklatın **Varsayılanları Geri Yükle** tooget geri toohello asıl dikey pencere yapılandırmasına.

## <a name="page-load-performance"></a>Sayfa yükleme performansı
Merhaba üst kısım sayfa yükleme sürelerinin bölümlenmiş bir grafik bulunur. Merhaba grafiğin toplam yüksekliği Hello kullanıcılarınızın tarayıcılarda uygulamanızdan hello ortalama süre tooload ve görüntü sayfaları temsil eder. Merhaba tarayıcı olayları, Düzen ve çalışan komut dosyaları da dahil olmak üzere işlenen tüm zaman uyumlu yük kadar hello ilk HTTP isteği gönderdiğinde hello zamandan ölçülür. AJAX çağrılarından web bölümleri yükleme gibi zaman uyumsuz görevleri içermez.

Merhaba grafik kesim hello toplam sayfa yükleme süresi hello [W3C tarafından tanımlanan standart zamanlamalara](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Bu hello Not *ağa bağlanma* zaman nedeni genellikle beklenenden daha düşük hello tarayıcı toohello sunucusundan gelen tüm istekleri üzerinden ortalama bir değer. Zaten bir etkin bağlantı toohello sunucusu olduğundan tek tek isteklerin bağlantı süresi 0 ' var.

### <a name="slow-loading"></a>Yavaş mı yükleniyor?
Yavaş sayfa yüklenmesi kullanım memnuniyetsizliğinin başlıca kaynaklarından biridir. Merhaba grafik yavaş sayfa yüklemeleri gösteriyorsa, kolay toodo olan bazı tanılama araştırmalarını.

Merhaba grafik uygulamanızda hello tüm sayfa yüklerinin ortalamasını gösterir. Merhaba sorun toosee tooparticular sayfaları, daha fazla hello dikey penceresini aşağı görünüm sınırlı, tarafından bölümlenmiş kılavuzun bulunduğu sayfası URL'si:

![](./media/app-insights-javascript/09-page-perf.png)

Merhaba sayfa görünümü sayısına ve standart sapmaya dikkat edin. Ardından Hello sayfa sayısı çok azsa hello sorun kullanıcıları çok etkilemez. Yüksek bir standart sapma (karşılaştırılabilir toohello ortalama kendisini) çok sayıda tek tek ölçüler arasında farklılık gösterir.

**Tek URL’yi ve tek sayfa görünümünü yakınlaştırma.** Tüm sayfa adı toosee tarayıcı grafikleri filtrelenmez yalnızca toothat URL dikey tıklayın; ve daha sonra bir sayfa görünümü örneği üzerinde.

![](./media/app-insights-javascript/35.png)

Tıklatın `...` bu olay için özelliklerin tam listesi için veya hello Ajax çağrılarını ve bağlantılı etkinlikleri inceleyin. Yavaş Ajax çağrıları etkileyen hello genel sayfa yükleme süresi zaman uyumlu olmaları durumunda. İlgili olaylar hello için sunucu isteklerini içerir (web sunucunuza Application Insights'ı ayarladıysanız) aynı URL.

**Zaman içerisinde performans sayfası.** Belirli zamanlarda yükselme olup geri hello tarayıcılar dikey penceresine, hello sayfa görünümü yükleme süresi kılavuzunu çizgi grafiği toosee değiştirin:

![Merhaba head hello kılavuzunun tıklayın ve yeni bir grafik türü seçin](./media/app-insights-javascript/10-page-perf-area.png)

**Diğer boyutlara göre bölme.** Belki de sayfalarınızın yavaş tooload üzerinde belirli bir tarayıcı, istemci işletim sistemi veya kullanıcı yer misiniz? Yeni bir grafik ekleyin ve hello ile denemeler **Group by** boyut.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>AJAX Performansı
Web sayfalarınızda AJAX çağrılarının iyi iş çıkardığından emin olun. Bunlar genellikle kullanılan toofill sayfanızı zaman uyumsuz olarak bölümlerdir. Merhaba genel sayfa hemen yüklenebilse de, kullanıcılarınızın boş web bölümlerine bakıp burada veri tooappear bunlara bekleniyor kırıklığına uğrayabilirler.

Web sayfasından oluşturulan AJAX çağrıları hello tarayıcılar dikey penceresinde bağımlılıklar olarak gösterilir.

Merhaba dikey pencerenin üst kısmındaki hello Özet grafikleri vardır:

![](./media/app-insights-javascript/31.png)

daha aşağıda da ayrıntılı kılavuzlar:

![](./media/app-insights-javascript/33.png)

Belirli ayrıntılar için herhangi bir satıra tıklayın.

> [!NOTE]
> Merhaba dikey penceresinde hello tarayıcılar filtresini silerseniz, bu grafiklere hem sunucu hem de AJAX bağımlılıkları eklenir. Tooreconfigure hello filtre Varsayılanları Geri Yükle'yi tıklatın.
> 
> 

**başarısız Ajax çağrılarını içine toodrill** toohello bağımlılık hataları kılavuzuna kaydırın ve satır toosee belirli örnekleri'ye tıklayın.

![](./media/app-insights-javascript/37.png)


Tıklatın `...` hello tam telemetri için bir Ajax çağrısı için.

### <a name="no-ajax-calls-reported"></a>Hiç Ajax çağrısı bildirilmedi mi?
Web sayfanızın hello betikten yapılan tüm HTTP/HTTPS çağrıları AJAX çağrılarını içerir. Bunların bildirildiğini görmüyorsanız, bu hello kod parçacığını hello ayarlanmış değil denetlemek `disableAjaxTracking` veya `maxAjaxCallsPerView` [parametreleri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Tarayıcı özel durumları
Merhaba tarayıcılar dikey penceresinde, bir özel durum Özet grafiği ve özel durum türleri daha fazla hello dikey penceresini aşağı oluşan bir kılavuz yoktur.

![](./media/app-insights-javascript/39.png)

Tarayıcı özel durumlarının bildirildiğini görmüyorsanız, bu hello kod parçacığını hello ayarlanmış değil denetlemek `disableExceptionTracking` [parametresi](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>Tek tek sayfa görünümü etkinliklerini inceleme

Sayfa görünümü telemetrisi çoğunlukla Application Insights tarafından analiz edilir; yalnızca birikmeli raporları, tüm kullanıcıların ortalamasını görürsünüz. Ancak, hata ayıklama amacıyla tek tek sayfa görünümü etkinliklerine de bakabilirsiniz.

Merhaba tanılama Ara dikey penceresinde filtreleri tooPage görünümü ayarlayın.

![](./media/app-insights-javascript/12-search-pages.png)

Tüm olay toosee daha fazla ayrıntı seçin. Merhaba Ayrıntılar sayfasında "..." toosee daha fazla ayrıntı tıklayın.

> [!NOTE]
> Kullanırsanız [arama](app-insights-diagnostic-search.md), toomatch tam sözcükleri özen gösterin: "Abou" ve "bout girişleri" eşleşmiyor "About".
> 
> 

Ayrıca hello güçlü kullanabilirsiniz [günlük analizi sorgu dili](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch sayfa görünümleri.

### <a name="page-view-properties"></a>Sayfa görünümü özellikleri
* **Sayfa görünümü süresi** 
  
  * Varsayılan olarak, hello alır tooload hello sayfa zaman, (yardımcı dosyalar ancak Ajax çağrıları gibi hariç zaman uyumsuz görevleri dahil) istemci isteği toofull yükleyin. 
  * Ayarlarsanız `overridePageViewDuration` hello içinde [sayfa Yapılandırması](#detailed-configuration), istemci isteği tooexecution Merhaba, aralığını ilk hello `trackPageView`. Merhaba betik hello başlatma sonra normal konumundan trackPageView taşındıysa, farklı bir değer yansıtır.
  * Varsa `overridePageViewDuration` ayarlanır ve bağımsız değişkeni hello sağlanan süre `trackPageView()` çağrısı hello bağımsız değişken değeri yerine kullanılır. 

## <a name="custom-page-counts"></a>Özel sayfa sayıları
Varsayılan olarak, yeni bir sayfa hello istemci tarayıcısına her yüklenişinde bir sayfa sayısı oluşur.  Ancak toocount ek sayfa görünümlerini isteyebilirsiniz. Örneğin, bir sayfa içeriğini sekmelerde görüntüleyebilir ve hello kullanıcı sekmeler arasında geçiş yaptığında toocount bir sayfa istiyor. Veya JavaScript kodu hello sayfasındaki hello tarayıcının URL'sini değiştirmeden yeni içerik yükleyebilir.

İstemci kodunuzda hello uygun noktada gibi JavaScript çağrısı ekleyin:

    appInsights.trackPageView(myPageName);

Merhaba sayfa adı, URL olarak ancak "#" sonra hepsi aynı karakterleri hello içerebilir veya "?" göz ardı edilir.

## <a name="usage-tracking"></a>Kullanımı izleme
Uygulamanızla kullanıcılarınızın neler çıkışı toofind istiyorsunuz?

* [Kullanımı izleme hakkında bilgi edinin](app-insights-web-track-usage.md)
* [Özel etkinlikler ve ölçüm API’si hakkında bilgi edinin](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Video


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Sonraki adımlar
* [Kullanımı izleme](app-insights-web-track-usage.md)
* [Özel etkinlikler ve ölçümler](app-insights-api-custom-events-metrics.md)
* [Build-measure-learn](app-insights-web-track-usage.md)

