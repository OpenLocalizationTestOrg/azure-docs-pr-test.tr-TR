---
title: "Azure Application Insights aramasında aaaUsing | Microsoft Docs"
description: "Web uygulamanız tarafından gönderilen arama ve filtreleme ham telemetri."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Application Insights'ta aramayı kullanma
Arama özelliğidir [Application Insights](app-insights-overview.md) toofind kullanıyorsanız ve sayfa görünümleri, özel durumlar gibi tek tek telemetri öğeleri keşfedin veya web istekleri olduğunu. Ve günlük izlemelerini ve kodlanmış olayları görüntüleyebilirsiniz.

(Verilerinizi üzerinden daha karmaşık sorgular için kullanın [Analytics](app-insights-analytics-tour.md).)

## <a name="where-do-you-see-search"></a>Burada arama görüyor musunuz?
### <a name="in-hello-azure-portal"></a>Hello Azure portalı
Tanılama arama, uygulamanızın hello uygulama Öngörüler genel bakış dikey penceresinden açıkça açabilirsiniz:

![Tanılama arama Aç](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

Bazı grafikler ve kılavuz öğeleri tıklattığınızda da açılır. Bu durumda, kendi filtrelerini toofocus seçtiğiniz öğesi hello türünü önceden ayarlanır. 

Örneğin, hello genel bakış dikey penceresinde bir çubuk grafiği, yanıt süresine göre sınıflandırılmış isteklerinin yoktur. Yanıt süresi aralığı, bir performans aralığı toosee tek tek isteklerin listesini tıklatın:

![İsteği Performans'ı tıklatın](./media/app-insights-diagnostic-search/07-open-from-filters.png)

Tanılama arama ana gövdesini Hello listesidir telemetri öğelerinin - sunucu istekleri, sayfa görünümleri, kodlanmış özel olaylar ve benzeri. Merhaba hello listenin olayları sayıları zamanla gösteren bir Özet Grafiği ' dir.

Yenileme tooget yeni olaylar'ı tıklatın.

### <a name="in-visual-studio"></a>Visual Studio’da

Visual Studio'da, ayrıca bir uygulama Insights arama penceresi yok. Hatalarını ayıkladığınız hello uygulama tarafından oluşturulan telemetri olayları görüntülemek için en kullanışlıdır. Ancak hello Azure portal, yayımlanan uygulamanızdan toplanan hello olayları gösterebilir.

Visual Studio'da Hello arama penceresini açın:

![Visual Studio Application Insights arama açın](./media/app-insights-diagnostic-search/32.png)

Merhaba arama penceresinin özellikleri benzer toohello web portalı vardır:

![Visual Studio Application Insights arama penceresi](./media/app-insights-diagnostic-search/34.png)

bir isteğin ya da bir sayfa görünümü açtığınızda hello izleme işlemi sekmesi kullanılabilir. Bir'işlemi ' tooa tek istek veya sayfa görünümü ile ilişkili olayları dizisidir. Örneğin, bağımlılık çağrıları, özel durumlar, izleme günlükleri ve özel olaylar tek bir işlemin parçası olabilir. Merhaba izleme işlemi sekmesini gösterir zamanlaması ve süresi ilişkisi toohello istek veya sayfası görünümünde bu olayların grafiksel hello. 

## <a name="inspect-individual-items"></a>Bireysel öğeleri inceleyin.
Tüm telemetri öğesi toosee anahtar alanları ve ilişkili öğeleri seçin. Toosee hello kümesini alanları isterseniz tıklayın "...". 

![Yeni iş öğesini, hello alanları düzenleyin ve Tamam'ı tıklatın.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>Filtre olay türleri
Merhaba filtre dikey penceresini açın ve hello olay türleri seçin toosee istiyor. (Daha sonra hello dikey penceresi açılır toorestore hello filtreleri istiyorsanız, Sıfırla'yı tıklatın.)

![Filtre seçin ve telemetri türlerini seçin](./media/app-insights-diagnostic-search/02-filter-req.png)

Merhaba olay türleri şunlardır:

* **İzleme** - [tanılama günlükleri](app-insights-asp-net-trace-logs.md) TrackTrace, log4Net, NLog ve System.Diagnostic.Trace çağrıları dahil.
* **İstek** -sayfaları, komut dosyaları, görüntüler, Stil dosyaları ve verileri de dahil olmak üzere sunucu uygulamanız tarafından alınan HTTP isteği. Bu olaylar kullanılan toocreate hello istek ve yanıt genel bakış grafiklerinde verilmiştir.
* **Sayfa görünümü** - [Telemetri hello web istemcisi tarafından gönderilen](app-insights-javascript.md), toocreate sayfa görünümü raporları kullanılır. 
* **Özel olay** - çağrıları tooTrackEvent() sırada çok eklediğiniz[izlemek kullanım](app-insights-api-custom-events-metrics.md), burada bulabilirsiniz.
* **Özel durum** - yakalanmayan [hello sunucu özel durumları](app-insights-asp-net-exceptions.md)ve TrackException() kullanarak oturum açın.
* **Bağımlılık** - [sunucu uygulamanızı gelen çağrıları](app-insights-asp-net-dependencies.md) tooother Hizmetleri REST API'leri veya veritabanları gibi ve AJAX çağrıları, [istemci kodu](app-insights-javascript.md).
* **Kullanılabilirlik** -sonuçlarını [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Özellik değerleri üzerinde filtreleme
Olayları özelliklerini hello değerleri filtreleyebilirsiniz. Merhaba kullanılabilir özellikler seçtiğiniz hello olay türlerine bağlıdır. 

Örneğin, belirli yanıt kodu istekleriyle çıkışı seçin. 

![Bir özelliği'ni genişletin ve bir değer seçin](./media/app-insights-diagnostic-search/03-response500.png)

Belirli bir özellik yok değerleri seçme aynı tüm değerleri seçme olarak efekt hello sahiptir. Bu, söz konusu özellik üzerinde filtreleme kapalı geçer.

### <a name="narrow-your-search"></a>Aramanızı daraltın
Bu hello toohello sağında hello filtre değerleri sayar bildirim göster var. kaç yineleme hello geçerli filtrelenmiş kümesinde yer alan. 

Bu örnekte '500' hello hataların çoğu bu hello ' Rpt/çalışanlar' istek sonuçları açıktır:

![Bir özelliği'ni genişletin ve bir değer seçin](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Merhaba olaylarla Bul aynı özelliği
Tüm hello Bul öğelerini hello ile aynı özellik değeri:

![Bir özellik sağ tıklayın](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Arama hello veri

> [!NOTE]
> toowrite daha karmaşık sorgular, açık [ **Analytics** ](app-insights-analytics-tour.md) hello arama dikey hello üstten.
> 

Koşullar herhangi bir hello özellik değerleri için arama yapabilirsiniz. Bu, yazdıysanız özellikle yararlıdır [özel olaylar](app-insights-api-custom-events-metrics.md) özellik değerlerine sahip. 

Bir zaman aralığı olarak aramaları daha kısa bir aralık içinde olan daha hızlı tooset isteyebilirsiniz. 

![Tanılama arama Aç](./media/app-insights-diagnostic-search/appinsights-311search.png)

Tam sözcük, değil alt dizeler arayın. Tırnak işaretleri tooenclose özel karakterler kullanın.

| Dize | olan *değil* tarafından bulunamadı | Ancak bu Bul |
| --- | --- | --- |
| HomeController.About |Giriş<br/>Denetleyici<br/>Çıkışı | homecontroller<br/>hakkında<br/>"homecontroller.about"|
|Amerika Birleşik Devletleri|UNI<br/>düzenlenmiş|Birleşik<br/>durumları<br/>VE Birleşik Devletleri<br/>"ABD"

Kullanabileceğiniz hello arama ifadeleri şunlardır:

| Örnek sorgu | Etki |
| --- | --- |
| `apple` |Tüm olayları, alanlar hello word "apple" Merhaba zaman aralığında Bul |
| `apple AND banana` |Her iki sözcüklerini olayları bulun. Capital "ve", değil kullan "ve". |
| `apple OR banana`<br/>`apple banana` |Her iki word içeren olayları bulun. "", Kullanıp "veya".<br/>Kısa formu. |
| `apple NOT banana` |Bir sözcük ancak değil hello diğer içeren olayları bulun. |



## <a name="sampling"></a>Örnekleme
Uygulamanız çok sayıda telemetri oluşturuyorsa (ve ASP.NET SDK sürüm 2.0.0-beta3 hello kullanıyorsanız veya sonrası), hello Uyarlamalı örnekleme modülü olayların yalnızca bir temsilci fraksiyonunu göndererek toohello portal gönderilen hello birimi otomatik olarak azaltır. Ancak, böylece ilgili olaylar arasında gezinebilirsiniz olayları, ilgili toohello aynı istekte seçilen veya bir grup olarak işaretli değildir. 

[Örnekleme hakkında bilgi edinin](app-insights-sampling.md).



## <a name="create-work-item"></a>İş öğesi oluşturma
Tüm telemetri öğesinden hello ayrıntılarla GitHub veya Visual Studio Team Services içinde bir hata oluşturabilirsiniz. 

![Yeni iş öğesini, hello alanları düzenleyin ve Tamam'ı tıklatın.](./media/app-insights-diagnostic-search/42.png)

Merhaba tooconfigure sorulur bunu ilk kez bir bağlantı tooyour Team Services hesabı ve proje.

![Merhaba URL'sini Team Services sunucunuzun ve hello proje adı doldurun ve Yetkilendir'i tıklatın](./media/app-insights-diagnostic-search/41.png)

(De hello bağlantı hello iş öğeleri dikey penceresinde yapılandırabilirsiniz.)

## <a name="save-your-search"></a>Aramayı kaydetme
İstediğiniz tüm hello filtreleri belirledikten sonra hello aramayı sık kullanılan olarak kaydedebilirsiniz. Bir kurumsal hesap çalışıyorsanız, seçebileceğiniz olup olmadığını tooshare diğer takım üyeleri ile.

![Sık Kullanılanlar'a tıklayın, hello adını ayarlayın ve Kaydet](./media/app-insights-diagnostic-search/08-favorite-save.png)

yeniden toosee hello arama **gidin toohello genel bakış dikey** ve Sık Kullanılanlar açın:

![Sık Kullanılanlar döşeme](./media/app-insights-diagnostic-search/09-favorite-get.png)

Göreli zaman aralığı ile kaydettiyseniz hello yeniden açılan dikey penceresinde hello en son verileri içeriyor. Mutlak zaman aralığıyla kaydettiyseniz hello bkz aynı verileri her zaman. (Toosave sık kullanılan istediğinizde 'Göreli' yoksa, hello başlığında zaman aralığı'nı tıklatın ve özel bir aralık olmadığından bir zaman aralığı ayarlayın.)

## <a name="send-more-telemetry-tooapplication-insights"></a>Daha fazla telemetri tooApplication Öngörüler Gönder
Toohello Giden kutusu telemetri Application Insights SDK'sı tarafından gönderilen ek şunları yapabilirsiniz:

* İçinde sık kullandığınız günlük çerçeveden günlük izlemelerini yakalama [.NET](app-insights-asp-net-trace-logs.md) veya [Java](app-insights-java-trace-logs.md). , Günlük izlemelerini arayın ve sayfa görünümleri, özel durumlar ve diğer olaylarla ilişkilendirmek anlamına gelir. 
* [Kod yazma](app-insights-api-custom-events-metrics.md) toosend özel olaylar, sayfa görünümleri ve özel durumları. 

[Nasıl toosend ve özel telemetri tooApplication Öngörüler öğrenin](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>SORU- CEVAP
### <a name="limits"></a>Ne kadar veri tutulur?

Merhaba bkz [sınırları Özet](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>My server istekleri gönderme verisi nasıl görebilirim?
Merhaba POST verilerini otomatik olarak oturum yoktur, ancak kullanabileceğiniz [TrackTrace ya da günlük çağrıları](app-insights-asp-net-trace-logs.md). Merhaba gönderme verisi hello ileti parametresinde yerleştirin. Merhaba hello iletisinde aynı filtre olamaz özellikleri şekilde filtre uygulayabilirsiniz, ancak hello boyut sınırı daha uzun.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Sonraki adımlar
* [Karmaşık sorgular analizleri yazma](app-insights-analytics-tour.md)
* [Günlükleri ve özel telemetri tooApplication Öngörüler Gönder](app-insights-asp-net-trace-logs.md)
* [Kullanılabilirlik ve yanıt hızını testleri ayarlama](app-insights-monitor-web-app-availability.md)
* [Sorun giderme](app-insights-troubleshoot-faq.md)
