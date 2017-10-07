---
title: "aaaAnalyze kullanıcı Gezinti desenlerle kullanıcı akar Azure Application ınsights'ta | Microsoft docs"
description: "Kullanıcılarınızın hello sayfaları ve web uygulamanızın özellikleri arasında nasıl gezindiğini analiz edin."
services: application-insights
documentationcenter: 
author: numberbycolors
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 08/02/2017
ms.author: cfreeman
ms.openlocfilehash: d3f35dc78e9874e4b7974604bf91c40a5e5b78eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-user-navigation-patterns-with-user-flows-in-application-insights"></a>Kullanıcı Gezinti desenlerle kullanıcı akar Application ınsights'ta Çözümle

![Uygulama kullanıcı Öngörüler akar aracı](./media/app-insights-usage-flows/flows.png)

Merhaba kullanıcı akar aracı kullanıcılarınızın hello sayfaları ve sitenizin özellikleri arasında nasıl gezindiğini visualizes. Gibi sorulara yanıt verilmesi için mükemmeldir:
* Nasıl kullanıcıların, sitenizde bir sayfa başka bir sayfaya geçemezsiniz?
* Sitenizin sayfasında hangi kullanıcıların tıklayın?
* Merhaba nerede kullanıcılar siteniz en karmaşıklığı yerleştirir?
* Burada kullanıcıları yineleme aynı eylemi tekrar tekrar hello yerler var mı?

Merhaba kullanıcı akar aracını bir ilk sayfa görünümü ya da belirttiğiniz bir olay başlatır. Bu sayfa görünümü veya özel olay, kullanıcı akar verilen gösterir, sayfa görünümleri ve daha sonra bir oturumu sırasında iki adımları hemen ardından, vb. kullanıcılara gönderilen özel olayları hello. Değişen kalınlığı satırlarını her yol kullanıcılar tarafından izlenen kaç kez gösterir. Özel "Oturumu sona erdi" düğümleri kaç kullanıcının hiçbir sayfa görünümleri veya özel olaylar düğümü, önceki hello sonra burada kullanıcıların sitenize büyük olasılıkla sol vurgulama gönderilen gösterir.



> [!NOTE]
> Application Insights kaynağınıza, sayfa görünümleri veya özel olaylar toouse hello kullanıcı akar aracı içermesi gerekir. [Uygulama toocollect sayfasını tooset hello Application Insights JavaScript SDK'sı ile otomatik olarak nasıl görünümleri öğrenin](app-insights-javascript.md).
> 
> 

## <a name="start-by-choosing-an-initial-page-view-or-custom-event"></a>İlk sayfa görünümü veya özel olay seçerek başlatın

![Kullanıcı akışlar için ilk bir olay seçin](./media/app-insights-usage-flows/flows-initial-event.png)

Merhaba kullanıcı akar aracıyla sorulara yanıt verilmesi başlatılan tooget seçin bir ilk sayfa görünümü veya özel olay tooserve hello hello görselleştirme için başlangıç noktası olarak:
1. Merhaba Hello bağlantıya tıklayın "kullanıcıların sonra ne yapacaksınız...?" Başlık veya hello Düzenle düğmesini tıklatın. 
2. Bir sayfa görünümü veya özel olay hello "İlk olay" açılan listeden seçin.
3. "Grafik oluştur" seçeneğini tıklatın.

Merhaba "1. adım" Merhaba görselleştirme sütunun ne kullanıcıların en sık üst alt çoğu tooleast sık kısmından sıralı yalnızca hello ilk olay sonra yaptığını gösterir. "2. adım" Merhaba ve sonraki sütunları göster hangi kullanıcılar bundan sonra tüm hello şekilde kullanıcıların bir resim oluşturma vermedi kullanıcılarınızın siteniz aracılığıyla gittiğiniz.

Varsayılan olarak, hello kullanıcı akar aracı, yalnızca hello rastgele son 24 saat sayfa görünümleri ve sitenizin özel olay örnekleri. Merhaba zaman aralığını artırın ve hello bakiyesi performans ve doğruluğu için rastgele örnekleme hello Düzenle menüsünde değiştirin.

Bazı hello sayfa görünümleri ve özel olaylar ilgili tooyou değilseniz, "X" Merhaba tıklatın hello düğümlerinde toohide istiyor. Toohide istediğiniz hello düğümlerinin seçtikten sonra hello görselleştirme aşağıda hello "Create grafik" düğmesini tıklatın. toosee tüm hello düğümleri gizlenmiş hello Düzenle düğmesini tıklatın, sonra hello "olayları dışlanan" kısmına bakın.

Sayfa görünümleri veya özel olaylar eksik ise hello görselleştirme toosee beklediğiniz:
* Merhaba Düzen menüsü Hello "olayları dışlanan" bölümüne bakın.
* Merhaba "Ayrıntı düzeyi" Denetim hello Düzen menüsü tooinclude daha az sıklıkta olayları hello görselleştirme kullanın.
* Merhaba sayfa görünümü veya özel olay beklediğiniz kullanıcılar tarafından seyrek gönderilirse hello görselleştirme hello Düzenle menüsünde artan hello zaman aralığını deneyin.
* Emin hello sayfa görünümü veya özel olay sitenizin hello kaynak kodunda hello Application Insights SDK'sı tarafından toplanan toobe ayarlama beklediğiniz yapın. [Özel olaylar toplama hakkında daha fazla bilgi edinin.](app-insights-api-custom-events-metrics.md)

İstiyorsanız, daha fazla adımları hello görselleştirme, kullanım hello "Adımları sayısı" kaydırıcı hello içinde toosee menü düzenleyin.

## <a name="after-visiting-a-page-or-feature-where-do-users-go-and-what-do-they-click"></a>Bir sayfa veya özellik ziyaret ettikten sonra kullanıcıların gittikleri ve ne bunlar tıklatın?

![Burada kullanıcılar'ı tıklatın kullanıcı akar toounderstand kullanın](./media/app-insights-usage-flows/flows-one-step.png)

İlk olay sayfa görünümü hello ilk sütunu ("Adım 1") hello görselleştirme hello sayfasını ziyaret hemen sonra kullanıcıların vermedi hızlı şekilde toounderstand ise. Siteniz bir pencere sonraki toohello kullanıcı akar görselleştirme içinde açmayı deneyin. Kullanıcıların hello sayfa toohello listesi hello "1. adım" sütununda olayların nasıl etkileşim, beklentilerinizi karşılaştırın. Genellikle, bir kullanıcı Arabirimi öğesi Önemsiz tooyour takım görünüyor hello sayfasında hello hello sayfasında en sık kullanılan arasında olabilir. Tasarım geliştirmeleri tooyour sitesi için harika bir başlangıç noktası olabilir.

İlk olay özel bir olay ise, hello ilk sütun bu eylemi gerçekleştirdikten sonra kullanıcıların ne yaptığını gösterir. Sayfa görünümleri gibi ile Merhaba kullanıcılarınızın davranışını ekibinizin hedefleri ve beklentileri eşleşen gözlenen varsa göz önünde bulundurun. Örneğin, seçili ilk olay "Sepeti eklenen öğesi tooShopping" ise, toosee görünmesini "Git tooCheckout" ve "Kısa süre içinde bundan sonra hello görselleştirme içinde görünür satınalma tamamlandı". Kullanıcı davranışlarını beklentilerinizi çok farklıysa nasıl kullanıcılar "sitenizin geçerli tasarım gereği yakalanır" Merhaba görselleştirme toounderstand kullanın.

## <a name="where-are-hello-places-that-users-churn-most-from-your-site"></a>Merhaba nerede kullanıcılar siteniz en karmaşıklığı yerleştirir?

Gözcü yüksek yukarı görünmesini "Oturumu sona erdi" düğümler için özellikle başlarında bir akış hello görselleştirme sütununda. Bu, çok sayıda kullanıcı sayfaları ve kullanıcı Arabirimi etkileşimleri önceki yol aşağıdaki hello sonra büyük olasılıkla sitenizden churned anlamına gelir. Bazen karmaşası - Örneğin, bir e-ticaret sitesinde bir satın alma tamamladığınızda - bekleniyordu, ancak genellikle karmaşası bir tasarım sorunları, düşük performans veya diğer sorunlar sitenizle geliştirilebilir işaretidir.

Bu "oturum düğümleri yalnızca bu Application Insights kaynağı tarafından toplanan telemetri dayanır sona" göz önünde bulundurun. Application Insights telemetri belirli kullanıcı etkileşimleri almazsa hello oturumu sona erdi hello kullanıcı akar aracı diyor sonra kullanıcılar hala bu yolla sitenizle kurduğunda.

## <a name="are-there-places-where-users-repeat-hello-same-action-over-and-over"></a>Burada kullanıcıları yineleme aynı eylemi tekrar tekrar hello yerler var mı?

Sayfa görünümü veya birden çok kullanıcı tarafından hello görselleştirme sonraki adımlarda arasında yinelenen özel olay arayın. Bu, genellikle kullanıcıların, sitenizde yinelenen Eylemler performans gösterdiğini anlamına gelir. Yineleme bulursanız, yeni işlevsellik tooreduce yineleme ekleme veya hello tasarım sitenizin değiştirme hakkında düşünün. Örneğin, her bir tablo öğesi satırındaki yinelenen eylemler gerçekleştirme kullanıcılar bulursanız Toplu Düzenle işlevselliği ekleme.

## <a name="common-questions"></a>Sık sorulan sorular

### <a name="why-do-steps-appear-disconnected"></a>Adımları neden bağlantısı kesilmiş görünüyor?

![Bağlantısı kesilmiş adımlara kullanıcı akışlar](./media/app-insights-usage-flows/flows-disconnected.png)

Kullanıcı akar görselleştirme (sütunları) adımlarda bağlantısı kesilirse, hello adımlar arasındaki kullanıcılar tarafından gerçekleştirilen hello yolları hiçbiri gösterilen yetecek kadar sık toobe edildiği anlamına gelir. Merhaba görselleştirme sık olaylarına daha az tooshow hello adımları bağlı görünecek şekilde hello "Ayrıntı düzeyi" kaydırıcı hello Düzenle menüsünde ayarlayın.

### <a name="does-hello-initial-event-represent-hello-first-time-hello-event-appears-in-a-session-or-any-time-it-appears-in-a-session"></a>Mu hello ilk temsil hello ilk zaman hello olay görünür bir oturumda veya isteğe bağlı olarak her zaman bir oturumda görünür?

Merhaba ilk olay hello görselleştirme üzerinde yalnızca bir kullanıcı bu sayfa görünümü veya özel olay bir oturum sırasında gönderilen ilk kez hello temsil eder. Kullanıcılar, birden çok kez oturumda hello ilk olay gönderebilir sonra hello "1. adım" sütun yalnızca gösterir hello sonra kullanıcıların nasıl davranacağını *ilk* ilk olay örneği, tüm örnekleri.

## <a name="next-steps"></a>Sonraki adımlar

* [Kullanıma genel bakış](app-insights-usage-overview.md)
* [Kullanıcıları, oturumlar ve olaylar](app-insights-usage-segmentation.md)
* [Bekletme](app-insights-usage-retention.md)
* [Özel olaylar tooyour uygulama ekleme](app-insights-api-custom-events-metrics.md)
