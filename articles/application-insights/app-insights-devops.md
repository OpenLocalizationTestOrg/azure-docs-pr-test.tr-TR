---
title: "aaaWeb uygulama performansı izleme - Azure Application Insights | Microsoft Docs"
description: "Application Insights hello devOps döngüsü nasıl uyduğunu"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Application Insights ile ayrıntılı web uygulaması ve hizmet tanılama
## <a name="why-do-i-need-application-insights"></a>Application Insights neden gerekiyor mu?
Application Insights çalışan web uygulamanızı izler. Hataları ve performans sorunları hakkında bildirir ve müşteriler, uygulamanızın kullanımını analiz etmenize yardımcı olur. Birçok platformda (ASP.NET, J2EE, Node.js,...) üzerinde çalışan uygulamalar için çalışır ve hello Bulut veya şirket içi barındırılır. 

![Web uygulamaları teslim hello karmaşıklığını yönleri](./media/app-insights-devops/010.png)

Çalışırken temel toomonitor modern uygulama var. En önemlisi, müşterilerinizin çoğunu önce toodetect hataları istiyor. Ayrıca toodiscover istediğiniz ve, değil yıkıcı olsa da, belki de sistemi yavaşlatır veya bazı rahatsızlıktan tooyour kullanıcıların neden performans sorunları düzeltin. Ve hello sistem tooyour memnuniyet gerçekleştirirken, hangi hello kullanıcılar ile gittiğini tooknow istiyorsanız: Bunlar hello son özelliğini kullanarak misiniz? Bunlar ile başarılı oluyor?

Modern web uygulamaları kesintisiz teslim döngüsünde geliştirilen: yeni bir özellik ya da geliştirme; sürüm Merhaba kullanıcılar için ne kadar iyi çalıştığı inceleyin; Bu bilgilere dayanan geliştirme Hello sonraki artışı planlayın. Bu döngü önemli bir parçası hello gözlem aşamasıdır. Application Insights, performans ve kullanım için bir web uygulaması hello araçları toomonitor sağlar.

Merhaba en önemli bu işlem tanılama ve tanılama yönüdür. Merhaba uygulama başarısız olursa, sonra iş kaybolmasına. Hello prime rol izleme framework'ün bu nedenle toodetect hataları güvenle, toodiagnose hello sorun hello bilgilerle gereksinim, hemen ve toopresent bildir. Bu, tam olarak Application Insights ne olur.

### <a name="where-do-bugs-come-from"></a>Hatalar alınacağı yeri?
Web sistemlerinde hataları, genellikle yapılandırma sorunları veya birçok bileşenleri arasındaki hatalı etkileşimler ortaya çıkar. Canlı site olay tackling zaman hello ilk görevdir bu nedenle tooidentify hello locus hello sorununun: hangi bileşen veya ilişki hello nedeni?

Bazı gri artı olanlar bize, bilgisayar programı bir bilgisayarda çalıştırıldığı daha basit bir dönem anımsamasını sağlayabilirsiniz. Merhaba geliştiriciler göndermeden önce baştan sona test; ve, gönderilen nadiren bakın veya bu konuda yeniden düşünün. Merhaba kullanıcılar tooput hello fazlalık hatalarla yıllardır gerekir. 

Şimdi bu nedenle çok farklı noktalardır. Farklı cihaz toorun sayısız uygulamanızı açmıştır ve zor tooguarantee hello tam aynı davranışı her birinde olabilir. Hello bulut uygulamalarında barındırma hızlı hataların düzeltilmesi, ancak de sürekli rekabet ve hello beklentisi yeni özellikler sık aralıklarla anlamına gelir. 

Bu koşullar, hello hello hata sayısı üzerinde kesin bir denetim yolu tookeep birim testi otomatik. İmkansız toomanually yeniden test her teslim her şeyi kısa. Merhaba sıradan bir parçası yapı artık işlem birim testi olur. Merhaba Xamarin Test Cloud gibi araçları birden çok tarayıcı sürümlerinde test otomatikleştirilmiş UI sağlayarak yardımcı olur. Bunlar regimes sınama bize toohope izin içinde uygulama bulunan hataların hello hızı tooa minimum tutulabilir.

Normal web uygulamaları birçok Canlı bileşeni vardır. Toplama toohello istemci (tarayıcı veya aygıt uygulama) ve hello web sunucusu, büyük olasılıkla toobe önemli arka uç işleme yoktur. Belki de hello arka uç bileşenlerinin bir ardışık düzen veya iş parça ok koleksiyonu ' dir. Ve bunların kaç, denetiminde olmayacaktır - dış hizmetler, bağımlı oldukları.

Bu gibi yapılandırmalarında, onu, zor ve uneconomical tootest olması veya öngörüyor, her olası hata modu, dışında hello sisteminin kendisi Canlı. 

### <a name="questions-"></a>Soru...
Biz web sistemi geliştirirken size bazı sorular sorun:

* Uygulamam kilitlenen? 
* Tam olarak ne oldu? -Bir istek başarısız olursa nasıl var. var tooknow istiyor. Bir izleme olaylarının ihtiyacımız...
* Uygulamam yeterince hızlı mı? Toorespond tootypical istekleri ne kadar sürer?
* Merhaba sunucu tanıtıcısı hello yüklenmesi miyim? İstekleri Hello oranını miktarı artar, hello yanıt süresi sürekli içeriyor mu?
* My - hello REST API'leri, veritabanları ve Uygulamam çağıran bileşenlerle nasıl yanıt vereceğini bağımlılıklardır. Özellikle, hello sistem yavaşsa, my bileşenidir veya yavaş yanıt birisinden alıyorum?
* Uygulamam yukarı veya aşağı mi? Bu gelen Merhaba Dünya görülebilir mi? Durdurur, bilmeniz izin ver...
* Merhaba kök nedeni nedir? My bileşeni ya da bir bağımlılık Hello hatası oldu mu? Bir iletişim sorunu mu?
* Kaç kullanıcının etkilenen? Birden fazla sorunu tootackle hello en önemli olduğu sahipsem?

## <a name="what-is-application-insights"></a>Application Insights nedir?
![Application Insights temel iş akışı](./media/app-insights-devops/020.png)

1. Application Insights uygulamanızı Instruments ve hello uygulama çalışırken ilgili telemetri gönderir. Merhaba uygulamaya hello Application Insights SDK'sı oluşturabilir ya da çalışma zamanında izleme uygulayabilirsiniz. kendi telemetri toohello normal modüller ekleyebilirsiniz gibi hello eski yöntemi daha esnektir.
2. Merhaba telemetri toohello Application Insights portalı, burada, depolanan işlenen ve gönderilir. (Application Insights Microsoft Azure üzerinde barındırılan olsa da, tüm web uygulamaları - yalnızca Azure uygulamalarını izleyebilirsiniz.)
3. Merhaba telemetri tooyou grafik hello formlarını ve olayların tablolarındaki sunulur.

Telemetri iki ana türü vardır: toplanan ve raw örnekleri. 

* Örnek veri Örneğin, web uygulamanız tarafından alınan bir isteğin bir rapor içerir. İçin bulun ve hello Application Insights portalında hello arama aracını kullanarak bir isteğin hello ayrıntılarını inceleyin. Merhaba örneği uygulamanızı toorespond toohello isteği ne kadar sürdü gibi verileri içerecek yanı istenen URL, hello istemci yaklaşık konumunu ve diğer verileri hello.
* Böylece hello yanıt sürelerini istekleriyle hello oranını karşılaştırabilirsiniz birim saat başına olay sayısı toplanan verileri içerir. Ayrıca, ortalama istek yanıt süreleri gibi ölçümleri içerir.

Veri Hello ana kategoriler şunlardır:

* URL, yanıt süresi ve başarı veya başarısızlık verileriyle istekleri tooyour uygulama (genellikle HTTP istekleri).
* Bağımlılıklar - URI, yanıt sürelerini ve başarı ile de uygulamanız tarafından oluşturulan REST ve SQL çağrıları
* Yığın izlemeleri dahil olmak üzere özel durumlar.
* Merhaba kullanıcılarınızın tarayıcılarından gelen sayfası görünüm verileri.
* Ölçüm ölçümleri yanı sıra, performans sayaçları gibi kendiniz yazın. 
* Özel olaylar tootrack iş olayları kullanabilirsiniz
* Günlük izlemelerini hata ayıklama için kullanılır.

## <a name="case-study-real-madrid-fc"></a>Örnek olay incelemesi: Gerçek Madrid F.C.
Merhaba, web hizmeti [gerçek Madrid futbol kulübü](http://www.realmadrid.com/) hakkında 450 milyon fanlar Merhaba Dünya işlevi görür. Fan her iki web tarayıcısı erişim ve kulübü'nın mobil uygulamaları hello. Fan yalnızca biletleri kitap, ancak sonuçları, oynatıcıları ve yaklaşan oyunlar bilgileri ve video klip de erişim. Hedefleri sayıda belirtmek gibi filtrelerle arama yapabilirsiniz. Bağlantılar toosocial medya vardır. Hello kullanıcı deneyimi, yüksek oranda kişiselleştirilmiş ve iki yönlü iletişim tooengage fanlar tasarlanmıştır.

Merhaba çözüm [hizmetler ve uygulamalar Microsoft azure'da oluşan bir sistemdir](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx). Ölçeklenebilirlik anahtar bir gereksinimdir: trafiği değişkendir ve çok yüksek birimleri sırasında ve eşleşmeleri geçici ulaşabilirsiniz.

İçin gerçek Madrid, bu önemli toomonitor hello sistem performansını olur. Azure Application Insights, bir güvenilir ve yüksek düzeyde hizmet sağlama hello sistem kapsamlı bir görünüm sağlar. 

Merhaba kulübü Ayrıca kendi fanların ayrıntılı anlama alır: oldukları (% 3'yalnızca olan İspanya '), hangi ilgi sahip oldukları oynatıcılar, geçmiş sonuçları ve yaklaşan oyunları ve toomatch sonuçlar vereceği.

Bu telemetri verilerini çoğunu hello çözüm Basitleştirilmiş ve azaltılmış işletim karmaşıklığını hiçbir eklenen kodu ile otomatik olarak toplanır.  İçin gerçek Madrid, Application Insights, her ay 3.8 milyar telemetri noktaları ile ilgilidir.

Gerçek Madrid hello Power BI modülü tooview kendi telemetri kullanır.

![Application Insights telemetri Power BI görünümü](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>Akıllı algılama
[Öngörülü tanılama](app-insights-proactive-diagnostics.md) yeni bir özelliktir. Herhangi bir özel yapılandırma sizin tarafınızdan olmadan Application Insights otomatik olarak algılar ve olağan dışı miktarı artar, uygulamanızda başarısızlık oranları içinde hakkında sizi uyarır. Yeterli akıllı tooignore bir arka plan zaman hatalar olduğunu ve ayrıca olan miktarı artar yalnızca istekleri tooa artışa ile orantılı. Sonra e-postası Ara hemen hakkında anlarsınız dolayısıyla Örneğin, bağımlı hello Hizmetleri birinde bir hata olduğunda ya da henüz dağıtılan hello yeni oluşturma kadar iyi çalışmıyor. (Ve Web kancalarını diğer uygulamalar tetiklersiniz.)

Bu özellik bir diğer unsuru sabit toodiscover olan olağan dışı desenlerini performans için arayan telemetrinize günlük ayrıntılı bir analizini gerçekleştirir. Örneğin, belirli bir coğrafi bölge ile veya belirli bir tarayıcı sürümü ile ilişkili yavaş performans bulabilirsiniz.

Her iki durumda da uyarı hello değil yalnızca söyler bulunan Belirtiler Merhaba, ancak Ayrıca, gereksinim duyduğunuz toohelp veri tanılama verir ilgili özel durum raporları gibi sorun hello.

![Öngörülü tanılama e-posta](./media/app-insights-devops/030.png)

Müşteri Samtec belirtilmektedir: "son özelliğini sırasında cutover altında ölçeklendirilmiş kaynak sınırlarına basarsa ve zaman aşımlarına neden olan bir veritabanı bulduk. Öngörülü algılama Uyarıları gelen tam anlamıyla biz tanıtılan gibi çok yakın gerçek zamanlı hello sorunu önceliklendirmek gibi. Bu uyarı Hello Azure platformu uyarılarla eşleşmiş bize neredeyse anında hello sorunu düzeltin olunmasına yardımcı oldu. Toplam kapalı kalma süresi < 10 dakika."

## <a name="live-metrics-stream"></a>Canlı ölçümleri akış
Merhaba son yapı dağıtma harcad bir deneyim olabilir. Herhangi bir sorun varsa, böylece, gerekirse yedekleyebilirsiniz hemen, bunlarla ilgili tooknow istediğiniz. Ölçümler bir canlı akışı hakkında bir saniye gecikmeyle anahtar ölçümleri sağlar.

![Canlı ölçümleri](./media/app-insights-devops/040.png)

Ve hemen bir örnek herhangi bir hata veya özel durumları inceleyin olanak tanır.

![Canlı hata olayları](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>Uygulama Eşlemesi
Uygulama eşlemesi hello performans bilgileri, performans sorunlarını ve sorunlu akışları dağıtılmış ortamınız arasında kolayca toolet üstünde yerleştirmede uygulama topolojinizi otomatik olarak bulur. Toodiscover Uygulama bağımlılıklarını Azure hizmetlerini sağlar. Kod ilgili ise anlama ya da ilgili bağımlılık tarafından hello sorun önceliklendirme ve ilgili tanılama tek konumdan ayrıntıya gelen deneyimi. Örneğin, uygulamanızın SQL katmanı tooperformance bozulma nedeniyle başarısız. Uygulama eşlemesi ile hemen görmek ve hello SQL dizin Danışmanı'nı veya sorgu öngörüleri deneyimi ayrıntıya gidin.

![Uygulama Eşlemesi](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Uygulama Öngörüler analizi
İle [Analytics](app-insights-analytics.md), rasgele sorgular güçlü SQL benzeri bir dil yazabilirsiniz.  Merhaba tüm uygulama yığınını arasında tanılama çeşitli yönlerden bağlanın ve hello doğru soruları toocorrelate iş ölçümleri ve müşteri deneyimi ile hizmet performansı sorabilirsiniz kolay olur. 

Tüm telemetri örneği ve hello Portalı'nda depolanan ölçüm ham verileri sorgulayabilirsiniz. Merhaba dili filtre, birleştirme, toplama ve diğer işlemleri içerir. Alanlarını hesaplamak ve istatistiksel çözümleme gerçekleştirin. Tablo ve grafik görselleştirmeleri vardır.

![Analytics sorgu ve sonuçları grafiği](./media/app-insights-devops/025.png)

Örneğin, kolay olduğundan:

* Performans verileri müşteri tarafından toounderstand deneyimlerini katmanlarını uygulamanızın isteği kesiminde.
* Belirli hata kodları veya özel olay adları sırasında dinamik site araştırmalar arayın.
* Merhaba uygulama kullanımını belirli müşterilere toounderstand özellikleri nasıl edinilen ve benimsenen detaya.
* Oturumlar ve belirli kullanıcılar tooenable ve işlemleri takımlar tooprovide anında müşteri desteği için yanıt sürelerini izleyen.
* Sık kullanılan uygulama özellikleri tooanswer özelliği öncelik sorular belirler.

Müşteri DNN belirtilmektedir: "Application Insights sağlanan bize mümkün toocombine, sıralama, sorgu ve gerektiğinde filtre veri olması için hello eşitlik parçası eksik hello ile. Bizim takım toouse kendi resimleri ve deneyimi toofind izin vererek güçlü sorgu dili verileri bize toofind Öngörüler izin ve bile biz vardı biliyoruz kaydetmedi sorunları. Merhaba sorular ile başlayan gelen çok ilginç yanıtların *' ı şimdi çok daha güzel If...'.*"

## <a name="development-tools-integration"></a>Geliştirme araçları tümleştirme
### <a name="configuring-application-insights"></a>Application Insights yapılandırma
Visual Studio ve Eclipse araçları tooconfigure hello doğru SDK paketleri, geliştirmekte olduğunuz hello projesi için sahiptir. Menü komutu tooadd Application Insights yoktur.

İzleme günlüğü framework Log4N, NLog veya System.Diagnostics.Trace gibi kullanarak toobe görülüyorsa, böylece istekleriyle hello izlemeleri kolayca ilişkilendirebilirsiniz sonra hello birlikte hello seçeneği toosend hello günlükleri tooApplication Öngörüler diğer telemetri elde , bağımlılık çağrıları ve özel durumları.

### <a name="search-telemetry-in-visual-studio"></a>Visual Studio'da arama telemetri
Geliştirme ve bir özellik hatalarını ayıklarken, arama ve görüntüleyebilirsiniz hello doğrudan Visual Studio'da aynı tesislerde hello web Portalı'nda arama hello kullanarak, telemetri.

Ve Application Insights bir özel durum kapattığında, Visual Studio'da hello veri noktası görüntülemek ve düz toohello ilgili kod atlama.

![Visual Studio arama](./media/app-insights-devops/060.png)

Hata ayıklama sırasında hello seçeneği tookeep hello telemetri geliştirme makinenizde Visual Studio'da ancak toohello portal göndermeden görüntüleme vardır. Bu yerel seçeneği üretim telemetri ile hata ayıklama karıştırma önler.

### <a name="build-annotations"></a>Ek açıklamaları oluşturma
Visual Studio Team Services toobuild kullanın ve uygulamanızı dağıtırsanız, dağıtım ek açıklamaları grafiklerde hello Portalı'nda görünür. En son sürüm hello ölçümleri herhangi bir etkisi olsaydı, belirgin olur.

![Ek açıklamaları oluşturma](./media/app-insights-devops/070.png)

### <a name="work-items"></a>İş öğeleri
Bir uyarı oluştuğunda, Application Insights, otomatik olarak bir iş öğesi izleme sistemi çalışmanızı oluşturabilirsiniz.

## <a name="but-what-about"></a>Ancak ne...?
* [Gizlilik ve depolama](app-insights-data-retention-privacy.md) -telemetrinizi Azure güvenli sunucularda tutulur.
* Performans - hello etkisi çok düşüktür. Telemetri toplu hale.
* [Fiyatlandırma](app-insights-pricing.md) -, ücretsiz kullanmaya başlayabilir ve düşük biriminde iken sürdürür.


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>Sonraki adımlar
Application Insights ile Başlarken kolaydır. Merhaba ana Seçenekler şunlardır:

* Zaten çalışan web uygulaması izleme. Bu, tüm hello yerleşik performans telemetrisini sağlar. İçin kullanılabilir [Java](app-insights-java-live.md) ve [IIS sunucuları](app-insights-monitor-performance-live-website-now.md), için ve ayrıca [Azure web uygulamaları](app-insights-azure.md).
* Projenizi geliştirme sırasında izleme. Bunu yapabilmeniz [ASP.NET](app-insights-asp-net.md) veya [Java](app-insights-java-get-started.md) uygulamaları yanı [Node.js](app-insights-nodejs.md) ve ana bilgisayar [diğer türleri](app-insights-platforms.md). 
* Aracı [herhangi bir web sayfasında](app-insights-javascript.md) kısa kod parçacığını ekleyerek düzenleyin.

