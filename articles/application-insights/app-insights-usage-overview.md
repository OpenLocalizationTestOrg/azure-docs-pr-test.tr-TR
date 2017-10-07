---
title: "Azure Application Insights ile web uygulamaları için aaaUsage çözümleme | Microsoft docs"
description: "Kullanıcılarınızın ve web uygulamanızı ile neler yaptığını anlayın."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a>Application Insights ile web uygulamaları için kullanım analizi

Web uygulamanızın hangi özellikleri en popüler var mı? Kullanıcılarınızın uygulamanızla hedeflerine ulaşması? Bunlar belirli zamanlarda bırakma ve döndürmeleri daha sonra?  [Azure Application Insights](app-insights-overview.md) , kişiler, web uygulamanızın kullanımını içine güçlü Öngörüler kazanmanıza yardımcı olur. Uygulamanızı güncelleştirme her zaman, kullanıcılar için ne kadar iyi çalıştığı değerlendirebilirsiniz. Bu bilgiyle, veri sonraki geliştirme döngüsü hakkında kararlar tabanlı yapabilirsiniz.

## <a name="send-telemetry-from-your-app"></a>Telemetriyi uygulamanızdan Gönder

Uygulama sunucusu kodunuzu hem de web sayfalarınıza Application Insights yükleyerek Hello en iyi deneyimi elde edilir. Merhaba istemci ve sunucu bileşenleri, uygulamanızın telemetri geri toohello analiz için Azure portalı gönderin.

1. **Sunucu kodu:** için yükleme hello uygun modülü, [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), veya [diğer](app-insights-platforms.md) uygulama.

    * *Tooinstall sunucu kodu istiyor mu? Yalnızca [Azure Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).*

2. **Web sayfası koduna:** açık hello [Azure portal](https://portal.azure.com), uygulamanız için hello Application Insights kaynağı açın ve ardından açın **Başlarken > İzleme ve tanılama istemci tarafı**. 

    ![Merhaba komut dosyası ana web sayfanızın hello head kopyalayın.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. **Telemetri alın:** projeniz için bir kaç dakika hata ayıklama modunda çalıştırılması ve hello genel bakış dikey penceresinde Application Insights sonuçlarında arayın.

    Uygulamanızın performansını uygulama toomonitor yayımlama ve uygulamanızla kullanıcıların ne yaptıklarını bulun.

## <a name="include-user-and-session-id-in-your-telemetry"></a>Kullanıcı ve oturum kimliği, telemetri dahil
zaman içinde tootrack kullanıcılar, Application Insights gerektirir yolu tooidentify bunları. bir kullanıcı kimliği veya bir oturum kimliği gerektirmez yalnızca kullanım aracı araçtır hello olayları hello

Bu kimlikleri göndermeye Başla [burada](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).

## <a name="explore-usage-demographics-and-statistics"></a>Kullanım demografisine ve istatistikleri keşfedin
Kişiler uygulamanızı kullandığınızda, bunlar en, kullanıcılarınızın bulunduğu ilgileniyor hangi sayfaların, hangi tarayıcılar ve işletim sistemleri bunlar kullandığını öğrenin. 

Merhaba kullanıcı ve oturum raporlar verilerinize sayfaları veya özel olaylar göre filtre uygulamak ve bunları konumu, ortam ve sayfa gibi özelliklere göre segmentlere ayırmak. Kendi filtreler de ekleyebilirsiniz.

![Kullanıcılar](./media/app-insights-usage-overview/users.png)  

Veri kümesi hello ilginç kalıpları çıkışı Öngörüler hello sağ üzerinde gelin.  

* Merhaba **kullanıcılar** rapor hello sayıda sayfalarınızı içinde seçilen zaman dönemleriniz erişim benzersiz kullanıcı sayısı. (Kullanıcılar tanımlama bilgilerini kullanarak sayılır. Birisi farklı tarayıcılar veya istemci makinelerle sitenize erişen veya kendi tanımlama bilgilerini temizler, ardından bunlar birden çok kez sayılacaktır.)
* Merhaba **oturumları** rapor sitenize erişen kullanıcı oturumlarını hello sayısını sayar. Bir süre etkinlik bir süre işlem yapılmadığında birden fazla yarım saat biri tarafından sonlandırıldı, bir kullanıcı tarafından oturumdur.

[Merhaba kullanıcıları, oturumlar ve olayları araçları hakkında daha fazla bilgi](app-insights-usage-segmentation.md)  

## <a name="page-views"></a>Sayfa görünümleri

Merhaba kullanım dikey penceresinden hello sayfa görünümleri döşeme tooget en popüler sayfalarınızı dökümünü tıklayın:

![Merhaba genel bakış dikey penceresinden hello sayfa görünümleri grafik tıklayın](./media/app-insights-usage-overview/05-games.png)

Yukarıdaki Hello örnek bir oyun web sitesinden ' dir. Merhaba grafikten biz hemen görebilirsiniz:

* Kullanım, geçen hafta hello geliştirilmiş kurmadı. Belki de arama motoru iyileştirme hakkında düşünüyoruz?
* Tenis hello en popüler oyun sayfasıdır. Şimdi daha fazla geliştirmeleri toothis sayfasında odaklanın.
* Ortalama, kullanıcıların hello tenis sayfasını yaklaşık üç kez haftalık ziyaret edin. (Yaklaşık üç kat daha fazla oturumları kullanıcıları daha vardır.)
* Kullanıcıların çoğunun hello ABD çalışma hafta sırasında ve çalışma saatleri içinde hello sitesini ziyaret edin. Belki de biz "hızlı gizle" düğmesini hello web sayfasında sağlamanız gerekir.
* Merhaba [ek açıklamaları](app-insights-annotations.md) hello Web sitesi yeni sürümlerini ne zaman dağıtılan hello grafikte göster. Merhaba son dağıtımlarda hiçbirinin kullanım belirgin bir etkisi vardı.

Ne tooinvestigate hello trafiği tooyour site, site, sayfa görünümü telemetrisi gönderir özel bir özellik tarafından bölme gibi daha ayrıntılı istediğiniz?

1. Açık hello **olayları** hello Application Insights kaynağı menüsünde aracı. Bu araç kaç sayfa görünümleri ve özel olaylar çeşitli süzme, cohorting ve kesimleme seçenekleri dayalı uygulamanızdan gönderilen analiz etmenize olanak sağlar.
2. "Any sayfa görünümü" Hello "Kimin kullanılan" açılır listesinde, seçin.
3. Merhaba "Tarafından bölme" açılır listede tarafından hangi toosplit sayfanızı görüntülemek telemetri özelliğini seçin.

## <a name="retention---how-many-users-come-back"></a>Bekletme - kaç kullanıcı döndürülmesini?

Bekletme ne sıklıkta kullanıcılarınızın toouse belirli bir zaman aralığı sırasında bazı iş eylemi gerçekleştiren kullanıcı cohorts göre kendi uygulama dönüş anlamanıza yardımcı olur. 

- Hangi belirli özellikleri diğerlerinden daha fazla toocome geri kullanıcıların neden anlama 
- Form varsayımlar gerçek kullanıcı verilerine dayalı 
- Bekletme ürününüz için bir sorun olup olmadığını 

![Bekletme](./media/app-insights-usage-overview/retention.png) 

Merhaba bekletme denetimleri üstte, toodefine belirli olayları ve zaman aralığı toocalculate bekletme izin verir. Merhaba hello Orta grafiğinde verir görsel bir hello belirtilen hello zaman aralığına göre genel saklama yüzdesi. Merhaba alt Hello grafikte saklama belirli bir dönemde temsil eder. Bu düzeyde ayrıntı kullanıcıların ne yaptıklarını toounderstand ve ne daha ayrıntılı ayrıntı düzeyi döndürmeyi kullanıcıları etkileyebilecek sağlar.  

[Merhaba bekletme aracı hakkında daha fazla bilgi](app-insights-usage-retention.md)

## <a name="custom-business-events"></a>Özel iş olayları

tooget hangi kullanıcıların NET bir anlayış yapmak, web uygulamanızı, yararlı tooinsert satırlık bir kod toolog özel olaylar. Bu olayların her şeyi belirli düğmelerini, satın alma veya oyun kazanma gibi toomore önemli iş olayları gibi ayrıntılı kullanıcı eylemlerine izleyebilirsiniz. 

Bazı durumlarda, sayfa görünümleri yararlı olaylar gösterebilir rağmen genel doğru değil. Bir kullanıcı hello ürün satın alma olmadan bir ürün sayfasını açabilir. 

Belirli iş olaylarla kullanıcılarınızın siteniz aracılığıyla kullanıcılarınızın ilerleme grafik. Farklı seçenekler için tercihlerini çıkışı bulabilir ve bunlar bırakma out veya sorunlar vardır. Bu bilgiyle, geliştirme kapsamınızı hello öncelikleri hakkında bilinçli kararlar yapabilirsiniz.

Olayları hello web sayfasında kaydedilebilir:

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

Veya sunucu tarafı hello web uygulaması hello:

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

Filtre ya da hello Portalı'nda incelediğinizde hello olayları bölme özellik değerleri toothese olayları ekleyebilirsiniz. Ayrıca, bir standart özellikler tootrace hello tek bir kullanıcı etkinliklerini bir dizi sağlar anonim kullanıcı kimliği gibi ekli tooeach olay kümesidir.

Daha fazla bilgi edinmek [özel olaylar](app-insights-api-custom-events-metrics.md#trackevent) ve [özellikleri](app-insights-api-custom-events-metrics.md#properties).

### <a name="slice-and-dice-events"></a>Dilimlediği olayları

Merhaba kullanıcıları, oturumlar ve olayları araçları dilim ve kullanıcı, olay adı ve özellikleri tarafından özel olaylar inin.
![Kullanıcılar](./media/app-insights-usage-overview/users.png)  
  
## <a name="design-hello-telemetry-with-hello-app"></a>Merhaba telemetri hello uygulama ile tasarlama

Her bir özellik, uygulamanızın tasarlarken nasıl toomeasure başarısını Kullanıcılarınızla adımıdır göz önünde bulundurun. Ne başlatma toorecord gerekir ve olaylar için çağrı uygulamanıza hello izleme hello kod iş olayları karar verin.

## <a name="a--b-testing"></a>A | B testi
Bir özelliğin hangi değişken daha başarılı olacaktır bilmiyorsanız, bunların her erişilebilir toodifferent kullanıcıların her ikisi de serbest bırakın. Her Hello başarısını ölçmenize ve tooa birleşik sürüm taşıyın.

Bu yöntem, her sürümü, uygulamanız tarafından gönderilen farklı özellik değerleri tooall hello telemetri ekleyin. Bunu hello özelliklerini tanımlayarak yapabilirsiniz etkin TelemetryContext. Bu varsayılan özellikleri uygulama hello tooevery telemetri iletisi gönderir - yalnızca, özel iletiler, ancak de standart telemetri hello eklenir.

Merhaba Application Insights portalında filtre ve hello özellik değerleri, verilerinizde toocompare hello farklı sürümlerini farklı şekilde bölebilirsiniz.

toodo bunu [telemetri Başlatıcı ayarlama](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

Merhaba web uygulama Başlatıcı Global.asax.cs gibi:

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

Tüm yeni TelemetryClients belirttiğiniz başlangıç özellik değeri otomatik olarak ekler. Telemetri olaylarını tek tek hello varsayılan değerleri geçersiz kılabilir.

## <a name="next-steps"></a>Sonraki adımlar
   - [Kullanıcılar, Oturumlar, Etkinlikler](app-insights-usage-segmentation.md)
   - [Huniler](usage-funnels.md)
   - [Bekletme](app-insights-usage-retention.md)
   - [Kullanıcı Akışları](app-insights-usage-flows.md)
   - [Çalışma kitapları](app-insights-usage-workbooks.md)
   - [Kullanıcı bağlamı Ekle](app-insights-usage-send-user-context.md)
