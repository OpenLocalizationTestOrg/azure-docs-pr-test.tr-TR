---
title: "Azure Application Insights DevOps için aaaOverview | Microsoft Docs"
description: "Bilgi nasıl toouse Application Insights geliştirme Ops ortamında."
author: CFreemanwa
services: application-insights
documentationcenter: 
manager: carmonm
ms.assetid: 6ccab5d4-34c4-4303-9d3b-a0f1b11e6651
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: bwren
ms.openlocfilehash: 42139f4645e815f26378726f4716a9bfbdc78551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-insights-for-devops"></a>DevOps için Application Insights genel bakış

İle [Application Insights](app-insights-overview.md), uygulamanızı nasıl gerçekleştiriyor hızlıca bulabilir ve canlı olduğunda kullanılıyor. Bir sorun varsa, bunu, hello etkisini değerlendirmenize yardımcı olur ve hello neden saptamanıza yardımcı olur hakkında bilmenizi sağlar.

Web uygulamaları geliştirir ekibinden bir hesap şöyledir:

* *"Birkaç gün önce bir 'ikincil' düzeltme dağıttığımız. Biz geniş test geçişi çalıştırılmadı, ancak bazı beklenmeyen değişiklik hello ön ve arka uç arasındaki uyumsuzluk neden hello yükü içine ne yazık ki birleştirilmiş. Hemen sunucu özel durumları, surged bizim uyarı tetiklenir ve biz hello durumdan haberdar. Birkaç tıklama hello Application Insights portalındaki hemen özel durum callstacks toonarrow hello sorun aşağı gelen yeterli bilgi aldı. Biz geri hemen ve hello hasar sınırlıdır. Application Insights yaptı döngüsü bu kısmı hello devops çok kolay ve işlem yapılabilir."*

Bu makalede biz hello geliştirir Fabrikam banka bir ekipte izleyin çevrimiçi bankacılık nasıl kullandıkları sistem (RÇY) toosee Application Insights tooquickly toocustomers yanıt ve güncelleştirmeler yapabilir.  

Merhaba takım hello aşağıdaki çizimde gösterilen bir DevOps döngüde çalışır:

![DevOps döngüsü](./media/app-insights-detect-triage-diagnose/00-devcycle.png)

Gereksinimleri geliştirme biriktirme (görev listesi) akış. Bunlar genellikle çalışma - geliştirmeleri ve uzantıları var olan uygulamanın toohello hello formunda genellikle yazılımlara sprint kısa çalışır. Hello dinamik uygulama sık sık yeni özelliklerle güncelleştirilmiştir. Canlı olsa da, hello takım performans ve hello Yardımı Application Insights ile kullanım için izler. Bu APM veri kendi geliştirme biriktirme akışları.

Merhaba takım yakından için Application Insights toomonitor hello canlı web uygulaması kullanır:

* Performans. Nasıl yanıt süreleri olan istek sayısı değişir toounderstand istedikleri; ne kadar CPU, ağ, disk ve diğer kaynakları kullanılıyor; ve hello performans sorunlarını olduğu.
* Hataları. Özel durumlar varsa veya başarısız istekleri ya da bir performans sayacı kendi rahat aralığın dışında kalırsa, böylece işlemleri gerçekleştirebilir takım gereksinimlerini tooknow hızlı bir şekilde hello.
* Kullanımı. Yeni bir özellik yayımlandığında hello takım istediğiniz tooknow toowhat ölçüde kullanılır ve kullanıcıların bir güçlükle onunla olup olmadığına.

Şimdi hello geri bildirim hello döngüsünün parçası üzerinde odaklanır:

![Algılama-önceliklendirme-tanılama](./media/app-insights-detect-triage-diagnose/01-pipe1.png)

## <a name="detect-poor-availability"></a>Zayıf kullanılabilirlik Algıla
Marcela Markova hello RÇY ekipteki Kıdemli bir geliştiricinin ve çevrimiçi performansını izleme hello sağlama alır. Aynen birkaç ayarlar [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md):

* Merhaba ana giriş sayfası hello uygulama için tek URL test http://fabrikambank.com/onlinebanking/. Aynen 'Hoş Geldiniz!' HTTP kodu 200 ve metin ölçütüne göre ayarlar. Bu test başarısız olursa, hello ağ veya hello sunucuları veya belki de bir dağıtım sorunu ciddi yanlış bir şey yoktur. (Veya birisi hello Hoş Geldiniz değiştirildi! ileti kendi bilinen izin vererek olmadan hello sayfasında.)
* Her oturum açtığında ve geçerli listeleme, birkaç önemli ayrıntıları her sayfada denetimi hesap alır daha derin çok adımlı bir test. Bu test hello bağlantı toohello hesapları veritabanının çalıştığını doğrular. Aynen kurgusal Müşteri Kimliği kullanır: test amaçları için birkaç tanesi tutulur.

Bu testler ayarlama, Marcela bu hello takım herhangi kesinti hakkında hızlı bir şekilde bilir emin olur.  

Merhaba web testi grafik kırmızı nokta olarak hataları görünecektir:

![Görüntü noktadan önceki hello çalıştıran web testleri](./media/app-insights-detect-triage-diagnose/04-webtests.png)

Ancak daha da önemlisi, herhangi bir hata hakkında uyarı toohello geliştirme ekibi e-posta ile. Neredeyse tüm müşterilerin hello önce bu şekilde, bunlar bildirin.

## <a name="monitor-performance"></a>Performansı İzle
Application ınsights'ta Hello genel bakış sayfasında bulunan çeşitli gösteren bir grafik olduğundan [anahtar ölçümleri](app-insights-web-monitor-performance.md).

![Çeşitli ölçümleri](./media/app-insights-detect-triage-diagnose/05-perfMetrics.png)

Tarayıcı sayfa yükleme süresi doğrudan web sayfalarından gönderilen telemetri türetilir. Sunucu yanıt süresi, sunucu istek sayısı ve başarısız istek sayısı tüm hello web sunucusunda ölçülen ve buradan tooApplication Öngörüler gönderilen.

Marcela hello sunucu yanıt grafiğini ile biraz ilgilenen ' dir. Bu grafik zaman hello sunucu kullanıcının tarayıcıdan bir HTTP isteğini alır ve hello yanıt döndüğünde arasındaki ortalama süre hello gösterir. Merhaba sistem bilgisayardaki yük değiştikçe olağan dışı toosee Bu grafikteki bir değişim değil. Ancak bu durumda olduğu anlaşılıyor toobe küçük miktarı artar hello sayısı isteklerinin ve büyük arasında bir bağıntı hello yanıt süresi miktarı artar. Yalnızca kendi sınırlarına işletim hello sistemi belirtebilir.

Aynen hello sunucuları grafikleri açar:

![Çeşitli ölçümleri](./media/app-insights-detect-triage-diagnose/06.png)

Olduğu anlaşılıyor toobe kaynak sınırlaması, hiçbir belirtisi olabilir hello darbe hello sunucu yanıt grafiklerde yalnızca bir rastlantı şekilde.

## <a name="set-alerts-toomeet-goals"></a>Uyarıları toomeet hedeflerini ayarlama
Bununla birlikte, aynen hello yanıt süreleri tookeep bir göz ister. Çok yüksek gidin, ilgili tooknow hemen istediği.

Aynen ayarlar için bir [uyarı](app-insights-metrics-explorer.md), yanıt zamanları tipik bir eşik değerinden yüksek. Bu yanıt süreleri yavaşsa, kendisi hakkında anlarsınız kendi güven verir.

![Uyarı dikey ekleme](./media/app-insights-detect-triage-diagnose/07-alerts.png)

Uyarılar, çok çeşitli diğer ölçümleri üzerinde ayarlanabilir. Örneğin, e-postaları hello özel durum sayısı yüksek olur ya da hello kullanılabilir bellek düşük gider veya istemci isteklerini bir en yüksek ise alabilir.

## <a name="stay-informed-with-smart-detection-alerts"></a>Akıllı algılama Uyarıları hakkında bilgi sahibi olmak
Ertesi gün, bir uyarı e-posta Application Insights ulaşır. Ancak kendisi açıldığında, aynen aynen ayarlamak hello yanıt süresi uyarı değil bulur. Bunun yerine, her başarısız isteklerin - diğer bir deyişle, 500 veya daha fazla hata kodları döndürmüş istekleri ani bir artışa olmamıştı söyler.

Kullanıcılar genellikle hello kodda oluşturulan bir özel aşağıdaki hata - burada gördünüz başarısız isteklerdir. "Üzgünüz ayrıntılarınızı şu an güncelleştiremedik." söyleyen bir ileti görürler olabilir Veya mutlak utanç en kötü yığın dökümü hello web sunucusu'nın hello kullanıcının ekran görüntülenir.

Bu uyarı bir beklenmedik biçimde çünkü Hello aynen olduğundan, hello Aranan son zamanı sayısı encouragingly düşük isteği başarısız oldu. Bir küçük hataları meşgul Server'da beklenen toobe sayısıdır.

Ayrıca edildi beklenmedik biçimde her için biraz aynen tooconfigure bu uyarı kaydetmedi olduğundan. Application Insights akıllı algılama içerir. Tooyour uygulamanın normal hata düzeni ve belirli bir sayfada ya da yüksek yük ya da bağlantılı tooother ölçümleri altında "için kullanılan" hataları otomatik olarak ayarlar. Yalnızca bir neden varsa hello alarm oluşturur BT'nin tooexpect gelir.

![Öngörülü tanılama e-posta](./media/app-insights-detect-triage-diagnose/21.png)

Bu çok kullanışlı bir e-postadır. Yalnızca bir alarm yükseltmek değil. Çok sayıda hello önceliklendirme ve tanılama iş çok yapar.

Etkilenen kaç müşteriler ve hangi web sayfaları veya işlemleri gösterir. Marcela tooget hello tüm ekip bu yangın ayrıntıya çalışma gerek duyduğu aynen veya olup haftaya kadar yoksayılabilir karar verebilirsiniz.

Merhaba e-posta Ayrıca belirli bir özel durum oluştu ve - daha ilginç - o hello hatası başarısız çağrılar tooa belirli veritabanıyla ilişkili olduğunu gösterir. Bu Marcela'nın takım yakın zamanda herhangi bir güncelleştirme dağıtılmamış olsa bile neden hello hataya aniden görünen açıklanmaktadır.

Marcella bu e-postaya göre hello veritabanı takım hello lideri ping atar. Aynen bir düzeltmenin hello içinde son yarım saat yayımlanmış öğrenir; ve hata, belki de bulunmamış olabilir ikincil şema değişikliği...

Bu nedenle hello sorun sabit günlükleri araştırma önce bile ve bunu doğan 15 dakika içinde hello yolu toobeing açıktır. Ancak, Marcela hello bağlantı tooopen Application Insights tıklatır. Düz başarısız bir istek açar ve kârlılığı hello ilişkili bağımlılık çağrıları listesinde çağrısı başarısız veritabanı görebilir.

![başarısız istek](./media/app-insights-detect-triage-diagnose/23.png)

## <a name="detect-exceptions"></a>Özel durumlar Algıla
Kurulum, biraz ile [özel durumlar](app-insights-asp-net-exceptions.md) bildirilen tooApplication Öngörüler otomatik olarak olursunuz. Bunlar aynı zamanda açıkça çağrıları çok ekleyerek yakalanabilir[TrackException()](app-insights-api-custom-events-metrics.md#trackexception) hello koda:  

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }


belirgin bir kurtarma olmadıkça hello Fabrikam banka takım hello uygulama olarak her zaman bir özel durum telemetri göndermesini gelişmiştir.  

Aslında, bunların daha da geniş stratejidir: hello müşteri olduğu yerde ne engellenen her durumda telemetri gönderdikleri veya tooan özel durum hello kodda karşılık olup olmadığını toodo, istedikleri. Hello dış arası banka aktarım sistemi işletimsel bir nedenden dolayı (hata hello müşterinin) "Bu işlem tamamlanamıyor" iletisi döndürürse, örneğin, ardından bunlar olay izler.

    var successCode = AttemptTransfer(transferAmount, ...);
    if (successCode < 0)
    {
       var properties = new Dictionary <string, string>
            {{ "Code", returnCode, ... }};
       var measurements = new Dictionary <string, double>
         {{"Value", transferAmount}};
       telemetry.TrackEvent("transfer failed", properties, measurements);
    }

TrackException kullanılan tooreport özel durumların nedeni hello yığını bir kopyasını gönderir. TrackEvent kullanılan tooreport diğer olayları değil. Tanılama aşamasında yararlı olabilecek herhangi bir özellik ekleyebilirsiniz.

Özel durumlar ve olayları görünmesini hello [tanılama arama](app-insights-diagnostic-search.md) dikey. Bunlara toosee hello ek özellikler incelemek ve yığın izleme.

![Tanılama Arama'da filtreleri tooshow belirli veri türlerini kullanma](./media/app-insights-detect-triage-diagnose/appinsights-333facets.png)


## <a name="monitor-proactively"></a>Proaktif izleme
Marcela, yalnızca uyarılar için beklerken kalmaya devam etmez. Yeniden her dağıtım hemen sonra aynen bir inceler [yanıt sürelerini](app-insights-web-monitor-performance.md) - hem de genel şekil hello ve özel durum yanı sıra, en yavaş istekler Merhaba tablonun sayar.  

![Yanıt süresi grafiği ve sunucu yanıt sürelerinin kılavuz.](./media/app-insights-detect-triage-diagnose/09-dependencies.png)

Genellikle her hafta hello ile son karşılaştırma aynen her dağıtım hello performans etkisini değerlendirebilirsiniz. Varsa ani worsening, kârlılığı, hello ilgili geliştiricilere başlatır.

## <a name="triage-issues"></a>Önceliklendirme sorunları
-Hello önem ve bir sorun kapsamını değerlendirmesinde - önceliklendirme hello ilk algılama sonra adımdır. Merhaba takım gece yarısı diyoruz? Veya sonraki uygun boşluk hello biriktirme listesi hello kadar bırakılabilir? Değerlendirme içinde anahtar bazı sorular verilmiştir.

Ne sıklıkta gerçekleştiriliyor? Merhaba genel bakış dikey penceresinde Hello grafiklerde perspektif tooa sorun verin. Örneğin, Fabrikam uygulama hello bir gece dört web test uyarılar oluşturulur. Hala hello testleri çoğu yeşil oturuyormuş hello grafiği hello sabah baktığınızda, hello takım gerçekten bazı kırmızı nokta olduğunu görebilir. Merhaba kullanılabilirlik şemasına ayrıntılara, tüm bu zaman zaman ortaya çıkan sorunları bir test konumdan olduğunu açıktı. Bu açıkça yalnızca bir rota etkileyen bir ağ sorunu oluştu ve büyük olasılıkla kendisini temizler.  

Bunun aksine, özel durum sayısı veya yanıt süreleri hello grafiği çarpıcı ve kararlı bir artışa açıkça şeydir toopanic hakkında.

Yararlı önceliklendirme Taktik bunun deneyin, kendiniz ' dir. Merhaba çalıştırırsanız aynı sorun bildiğiniz gerçek olduğu.

Kullanıcıların hangi kesir etkilendiğini? tooobtain kaba yanıt hello oturum sayısı tarafından hello hata oranı bölün.

![Başarısız istekler ve oturumlarının grafikleri](./media/app-insights-detect-triage-diagnose/10-failureRate.png)

Yavaş yanıtlar olduğunda en yavaş yanıt istekleri Merhaba tablonun her sayfanın hello kullanım sıklığı ile karşılaştırın.

Engellenen hello senaryo ne kadar önemli mi? Belirli bir kullanıcı hikayesinin engelleme işlevsel bir sorun varsa, çok önemli midir? Müşteriler, faturalar ödeme edilemez, bu ciddi olur; Ekran rengi tercihlerini değiştiremezsiniz, belki de bekleyebilir. Merhaba olay ya da özel durum ayrıntısı veya hello yavaş sayfa hello kimliğini Merhaba, müşterilerin burada yaşıyorsanız söyler.

## <a name="diagnose-issues"></a>Sorunları tanılama
Tanılama değil oldukça hello hata ayıklama aynıdır. Merhaba kodlarda İzleme başlamadan önce neden, kaba fikrini olmalıdır hello sorun nerede ve ne zaman oluştuğunu.

**Ne zaman böyle bir durum?**  hello Geçmiş görünümünü hello olay ve ölçüm grafikleri tarafından sağlanan kolay toocorrelate efektleri ile olası nedenleri sağlar. Yanıt süresi veya özel durum hızları aralıklı yükselme olup, hello istek sayısına ulaştığı arayın: aynı hello tarafı, saat sonra kaynak sorunu gibi görünüyor. Daha fazla CPU veya bellek tooassign gerekiyor mu? Yoksa hello yük yönetemez bir bağımlılık mı?

**Bu bize?**  Olasılığı daha sonra - Örneğin ne zaman hello müşterinin hesap özetine istediği - isteğinin belirli bir türdeki performans ani açılan varsa, web uygulamanızın yerine bir dış alt olabilir. Ölçüm Gezgini hello bağımlılık hata oranı ve bağımlılık süresi ücretlerin seçin ve birkaç saat veya gün, algılanan hello sorunla geçmiş hello üzerinden kendi geçmişlerini karşılaştırın. Değişiklikler var. ilişkilendirerek, bir dış alt tooblame olabilir.  

![Bağımlılık hatası çağrıları toodependencies süresini ve grafikler](./media/app-insights-detect-triage-diagnose/11-dependencies.png)

Coğrafi konuma sorunları bazı yavaş bağımlılık sorunlardır. Fabrikam banka Azure sanal makineleri kullanır ve bunlar yanlışlıkla hesap sunucusu ve web sunucusu farklı bir ülkede bulunan olduğunu buldu. Çarpıcı geliştirme geçirerek olana bunlardan biri.

**Biz ne?** Hello sorunu toobe bir bağımlılık olarak görünüp görünmediğini ve her zaman vardır durumda değilse, büyük olasılıkla tarafından son zamanlarda bir değişiklik neden oldu. Merhaba hello ölçüm ve olay grafikleri tarafından sağlanan geçmiş perspektif kolay toocorrelate kolaylaştırır ani değişiklikler dağıtımlar ile. Merhaba arama hello sorun için aşağı, daraltır.

**Ne var ne yok?** Bazı sorunlar nadiren oluşur ve zor tootrack aşağı test ederek çevrimdışı olabilir. Tüm yapabiliriz olduğunda tootry toocapture hello hata Canlı oluşur. Özel durum raporlarında hello yığın dökümleri inceleyebilirsiniz. Ayrıca, sık kullandığınız günlük ile veya TrackTrace() ya da TrackEvent() ile izleme çağrıları yazabilirsiniz.  

Fabrikam ile arası hesap aktarımları, ancak yalnızca hesap türleri için belirli zaman zaman ortaya çıkan bir sorun var. toounderstand daha iyi olanlar, hello kod içinde bir özellik tooeach çağrı hello hesap türü ekleme, anahtar noktalarda TrackTrace() çağrıları eklenir. Yalnızca bu izlemeler çıkışı kolay toofilter tanılama Arama'da yapılan. Bunlar, ayrıca parametre değerleri özellikleri ve ölçüleri toohello izleme çağrıları iliştirilmiş.

## <a name="respond-toodiscovered-issues"></a>Yanıt toodiscovered sorunları
Merhaba sorunu tanı koydu sonra planı toofix yapabilir. Belki de geri son zamanlarda bir değişiklik veya belki de yalnızca bir tane Düzelt tooroll gerekir. Merhaba düzeltme yaptıktan sonra Application Insights başarılı olup olmadığını bildirir.  

Fabrikam Bank'ın geliştirme ekibi Application Insights kullanılan toobefore halinden daha fazla yapılandırılmış bir yaklaşım tooperformance ölçüm alın.

* Bunlar belirli ölçümleri açısından performans hedefleri hello Application Insights genel bakış sayfasında ayarlayın.
* Bunlar performans ölçümleri 'funnels.' kullanıcı ilerlemeyi ölçmek hello ölçümleri gibi hello başından Merhaba uygulaması tasarlama  


## <a name="monitor-user-activity"></a>Kullanıcı etkinliğini izleme
Yanıt süresi sürekli olarak iyi ve birkaç özel durum olduğunda hello geliştirme ekibi üzerinde toousability taşıyabilirsiniz. Tooimprove hello kullanıcı deneyimini nasıl ve ne tooencourage daha fazla kullanıcı tooachieve hello istenen hakkında düşünebilirsiniz hedefler.

Application Insights Ayrıca hangi kullanıcıların bir uygulamayla yerine kullanılan toolearn olabilir. Sorunsuz çalışır duruma geldiğinde hello takım hangi kullanıcıların veya gibi zorluk ile ve ne sıklıkta geri dönmeden hello en yaygın özelliklerdir tooknow ister. Bunları yaklaşan işlerini önceliklendirmek yardımcı olur. Ve her bir özelliğin toomeasure hello başarısını hello geliştirme döngüsü bir parçası olarak planlayabilirsiniz. 

Örneğin, tipik kullanıcı gezisine hello web sitesi aracılığıyla bir Temizle "Huni." sahip Birçok müşteri kredi farklı türlerde hello oranlarda arayın. Daha küçük bir sayı hello tırnak formunda toofill geçin. Olanların bir teklif almak, birkaç bir tane hello kredisi alın.

![Sayfa görünümü sayar](./media/app-insights-detect-triage-diagnose/12-funnel.png)

Müşteriler büyük sayıda hello burada bırakma dikkate alarak, hello iş tooget hello toohello alt aracılığıyla daha fazla kullanıcı Huni nasıl dışarı çalışabilir. Bazı durumlarda, bir kullanıcı deneyimi (UX) hatası olabilir - örneğin, sabit toofind hello 'İleri' düğmesine olduğu veya hello yönergeleri açık değil. Büyük olasılıkla, açılan aşımı ayarlarına daha önemli iş nedenleri vardır: hello kredisi oranları çok yüksek olabilir.

Ne olursa olsun hello nedeniyle, kullanıcıların ne yaptıklarını iş hello takım hello veriler yardımcı olur. Daha fazla izleme çağrıları olabilir ayrıntılı toowork eklenir. Tüm kullanıcı eylemlerden hello ince ayrıntılarını TrackEvent() kullanılan toocount olabilir tek tek düğmesini tıklattığında, bir kredi ödeme gibi toosignificant başarılar.

Merhaba takım kullanılan toohaving kullanıcı etkinliği hakkında bilgi alma. Günümüzde, yeni bir özellik tasarım olduğunda, kullanım hakkında geri bildirim nasıl elde çalışırlar. Bunlar hello başlangıç hello özelliğinden izleme çağrıları tasarlayın. Her geliştirme döngüsü hello görüşleri tooimprove hello özelliği kullanırlar.

[Kullanımı izleme hakkında daha fazla okuma](app-insights-usage-overview.md).

## <a name="apply-hello-devops-cycle"></a>Merhaba DevOps döngüsü Uygula
Bu nedenle nasıl bir takım kullanım Application Insights yalnızca toofix tek veren, tooimprove geliştirme yaşam döngüleri olmasıdır. I bunu nasıl Application Insights ile uygulama performans yönetimi, kendi uygulamalarında yardımcı olabileceği hakkında fikir edinmek verdiği umuyoruz.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Sonraki adımlar
Uygulamanızın hello özelliklere bağlı olarak çeşitli şekillerde başlayabiliriz. En iyi uyan seçin:

* [ASP.NET web uygulaması](app-insights-asp-net.md)
* [Java web uygulaması](app-insights-java-get-started.md)
* [Node.js web uygulaması](app-insights-nodejs.md)
* Üzerinde barındırılan uygulamalar, dağıtılmış [IIS](app-insights-monitor-web-app-availability.md), [J2EE](app-insights-java-live.md), veya [Azure](app-insights-azure.md).
* [Web sayfaları](app-insights-javascript.md) -tek sayfa uygulaması veya normal web sayfası - kullanın Bu kendi başına veya toplama tooany hello sunucu seçenekleri.
* [Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) tootest uygulamanızdan hello genel internet.
