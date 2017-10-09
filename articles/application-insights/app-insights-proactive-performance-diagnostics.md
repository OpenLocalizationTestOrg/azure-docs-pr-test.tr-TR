---
title: "aaaSmart algılama - performans anormalliklerini | Microsoft Docs"
description: "Application Insights, uygulama telemetri akıllı çözümleme yapar ve olası sorunları sizi uyarır. Bu özellik Kurulum gerekir."
services: application-insights
documentationcenter: windows
author: antonfrMSFT
manager: carmonm
ms.assetid: 6acd41b9-fbf0-45b8-b83b-117e19062dd2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: bwren
ms.openlocfilehash: 60f10612188920330030129f7464e2f398ef1f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection---performance-anomalies"></a>Akıllı algılama - performans Anormalliklerini

[Application Insights](app-insights-overview.md) otomatik olarak, web uygulamanızın hello performansını analiz eder ve olası sorunlar hakkında sizi uyarabilir. Bizim akıllı algılama bildirimlerini aldığından, bu okuma.

Bu özellik için Application Insights, uygulamanızın yapılandırma dışında hiçbir özel kurulum gerektirir (üzerinde [ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), veya [Node.js](app-insights-nodejs.md)hem de [web sayfası kod](app-insights-javascript.md)). Uygulamanızı yeterli telemetri oluşturduğunda etkin olur.

## <a name="when-would-i-get-a-smart-detection-notification"></a>Bir akıllı algılama bildirim ulaştıklarında?

Application Insights, uygulamanızın performansını hello şu yollardan biriyle düştü algıladı:

* **Yanıt süresi düşüşü** -uygulamanızı toorequests için kullanılan daha daha yavaş yanıt başlatıldı. Son dağıtımınız'teki bir gerileme olduğundan hello değişiklik Örneğin hızlı silinmiş olabilir. Veya, belki de bellek sızıntısı tarafından neden aşamalı, silinmiş olabilir. 
* **Bağımlılık süresi düşüşü** -tooa REST API çağrıları, veritabanı ya da diğer bağımlılık uygulamanızı sağlar. Merhaba bağımlılık için kullanılan daha daha yavaş yanıt vermiyor.
* **Yavaş performans düzeni** -uygulamanızı bir performans sorunu toohave yalnızca bazı istekleri etkileyen görüntülenir. Örneğin, sayfalar daha yavaş diğerlerinden tarayıcının bir türündeki yüklüyorsunuz; veya isteklerini belirli bir sunucudan daha yavaş hizmet vermeleri sağlanır. Şu anda bizim algoritmalar, sayfa yükleme sürelerinin, istek yanıt sürelerini ve bağımlılık yanıt sürelerini bakın.  

Akıllı algılama en az 8 gün sipariş tooestablish normal performansının taban çizgisini çalışılabilir birimde telemetrisini gerektirir. Bu nedenle, uygulamanızı belirli bir döneme ait çalıştıran sonra herhangi bir önemli sorun bir bildirim neden olur.


## <a name="does-my-app-definitely-have-a-problem"></a>Uygulamam kesinlikle bir sorun var mı?

Hayır, bir bildirim uygulamanızı kesinlikle bir sorun olduğu anlamına gelmez. Bu yalnızca bir şeyle adresindeki toolook daha yakından isteyebilirsiniz ilgili öneridir.

## <a name="how-do-i-fix-it"></a>Bunu nasıl düzeltirim?

Merhaba bildirimleri tanılama bilgileri içerir. Örnek aşağıda verilmiştir:


![Sunucu yanıt süresi düşüşü algılama bir örneği burada verilmiştir](./media/app-insights-proactive-diagnostics/server_response_time_degradation.png)

1. **Önceliklendirme**. Merhaba bildirimi kaç kullanıcı ya da kaç işlemleri etkilenir gösterir. Bu bir öncelik toohello sorun atamanıza yardımcı olabilir.
2. **Kapsam**. Tüm trafiği veya yalnızca bazı sayfaları Hello sorun etkilediğini? Kısıtlanmış BT tooparticular tarayıcılar veya konumları mi? Bu bilgiler hello bildirimden alınabilir.
3. **Tanılama**. Genellikle, hello tanı bilgilerini hello bildirim hello sorun hello yapısını önerir. Örneğin, istek oranı yüksek olduğunda yanıt süresi düşerse sunucunuz veya bağımlılıkları aşırı öneren. 

    Aksi takdirde, Application Insights'ta hello performans dikey penceresini açın. Burada, bulacaksınız [profil oluşturucu](app-insights-profiler.md) veri. Özel durumlar varsa, hello de deneyebilirsiniz [anlık görüntü hata ayıklayıcı](app-insights-snapshot-debugger.md).



## <a name="configure-email-notifications"></a>E-posta bildirimleri yapılandırma

Akıllı algılama bildirimleri varsayılan olarak etkindir ve sahip toothose gönderilen [sahipleri, Katkıda Bulunanlar ve okuyucular erişim toohello Application Insights kaynağı](app-insights-resources-roles-access-control.md). toochange bu i **yapılandırma** hello e-posta bildirimi veya Application Insights'ta akıllı algılama ayarları'nı açın. 
  
  ![Akıllı algılama ayarları](./media/app-insights-proactive-diagnostics/smart_detection_configuration.png)
  
  * Merhaba kullanabilirsiniz **aboneliği** hello e-posta bildirimleri alma hello akıllı algılama e-posta toostop bağlantıyı.

E-postaları akıllı algılamaların performans anormalliklerini hakkında sınırlı tooone e-posta Application Insights kaynağı başına günde ' dir. yalnızca o gün algılandı en az bir yeni sorun olduğunda hello e-posta gönderilir. Herhangi bir iletisi yineler alamazsınız. 

## <a name="faq"></a>SSS

* *Bu nedenle, yazarlar verilerimi göz önünde bulundurmanız?*
  * Hayır. Merhaba hizmet tamamen otomatik olarak yapılır. Yalnızca hello bildirimler alın. Verileriniz [özel](app-insights-data-retention-privacy.md).
* *Application Insights tarafından toplanan tüm hello verileri çözümlemek?*
  * Değil şu anda. Şu anda isteği yanıt süresi, bağımlılık yanıt süresi ve sayfa yükleme süresi çözümleyin. Ek ölçümler analizini ileriye doğru arama bizim biriktirme listesi üzerinde ' dir.

* Ne tür bir uygulama bu için çalışıyor mu?
  * Bu degradations hello uygun telemetri oluşturması herhangi bir uygulamada algılanır. Application Insights web uygulamanızda yüklediyseniz, ardından istekleri ve bağımlılıkları otomatik olarak izlenir. Ancak, arka uç Hizmetleri veya diğer uygulamalardan çağrıları çok eklediyseniz[TrackRequest()](app-insights-api-custom-events-metrics.md#trackrequest) veya [TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency), akıllı algılama hello aynı çalışır sonra yolu.

* *I kendi anomali algılama kuralları oluşturabilir veya mevcut kurallar özelleştirme?*

  * Henüz, ancak şunları yapabilirsiniz:
    * [Uyarıları ayarlamak](app-insights-alerts.md) , söyleyin, ne zaman bir ölçüm bir eşik kestiği.
    * [Telemetri verme](app-insights-export-telemetry.md) tooa [veritabanı](app-insights-code-sample-export-sql-stream-analytics.md) veya [tooPowerBI](app-insights-export-power-bi.md), burada, bunu kendiniz çözümleyebilirsiniz.
* *Ne sıklıkta hello çözümleme yapılır?*

  * Biz hello analiz günlük hello telemetriyi hello önceki gün (tam gün içinde UTC saat dilimi) çalıştırın.
* *Bu nedenle, bu Değiştir mu [ölçüm uyarıları](app-insights-alerts.md)?*
  * Hayır.  Biz, olağan dışı düşünebilirsiniz her davranışı toodetecting yürütün yok.


* *Bir anımsatıcı, yanıt tooa bildirim hiçbir şey yapmayın, alacak mıyım?*
  * Hayır, her sorun hakkında bir ileti yalnızca bir kez alın. Merhaba sorun devam ederse akıllı algılama dikey akış hello güncelleştirilir.
* *I hello e-posta kesildi. Merhaba Portalı'nda hello bildirimleri nereden bulabilirim?*
  * Merhaba Application Insights genel bakış, uygulamanızın, hello tıklatın **akıllı algılama** döşeme. Var. tüm bildirimleri too90 günlerini geri yükleyebilirsiniz toofind olacaktır.

## <a name="how-can-i-improve-performance"></a>Performansı artırmak ne?
Yavaş ve başarısız yanıtları kendi deneyimlerden bildiğiniz gibi web sitesi kullanıcı için en büyük frustrations hello biridir. Bu nedenle, sorunları tooaddress hello önemlidir.

### <a name="triage"></a>Değerlendirme
İlk olarak, önemli mu? Bir sayfa her zaman yavaş tooload, ancak yalnızca %1 sitenizin kullanıcılarının herhangi bir zamanda toolook adresinden sahip olabilir, daha önemli noktalar toothink hakkında varsa. Üzerinde %1 kullanıcı açmak yalnızca diğer yandan hello ancak araştırılması değerinde olabilecek her zaman özel durumları oluşturur.

Merhaba etkisi deyimi (etkilenen kullanıcılar veya trafiği %) genel bir kılavuz olarak kullanın, ancak hello Yazının tamamını değil unutmayın. Diğer kanıt tooconfirm toplayın.

Merhaba sorunu Hello parametrelerinin göz önünde bulundurun. Coğrafya bağımlı olması durumunda ayarlanan [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) bu bölge dahil: yalnızca ağ ilgili sorunlar olabilir, bu alanına.

### <a name="diagnose-slow-page-loads"></a>Yavaş sayfa yüklemeleri tanılama
Merhaba sorun nerede? Merhaba sunucu yavaş toorespond, hello sayfa çok uzun olduğundan, veya hello tarayıcı toodo çok sayıda iş toodisplay sahip onu?

Merhaba tarayıcılar ölçüm dikey penceresi açın. Merhaba tarayıcı sayfa yükleme süresi gösterir hello zaman nerede bulunacağını görüntüsünü bölümlenmiş. 

* Varsa **isteği gönderdiğinizde** olan yüksek hello sunuculardan yavaş yanıt ya da hello isteğidir bir posta çok miktarda veri ile. Ara hello [performans ölçümleri](app-insights-web-monitor-performance.md#metrics) tooinvestigate yanıt sürelerini.
* Ayarlanan [bağımlılık izleme](app-insights-asp-net-dependencies.md) toosee hello yavaşlığı tooexternal Hizmetleri veritabanınız olup.
* Varsa **alma yanıt** yaygındır, sayfanızın ve bağımlı bölümleri - JavaScript, CSS, vb. (ancak zaman uyumsuz olarak yüklenen veriler) görüntüleri uzun. Ayarlanmış bir [kullanılabilirlik test](app-insights-monitor-web-app-availability.md), ve hello seçeneği tooload bağımlı bölümleri emin tooset olabilir. Bazı sonuçları aldığınızda, açık bir sonuç hello ayrıntılarını ve toosee hello genişletin yük farklı dosyaların kez.
* Yüksek **istemci işleme süresi** betikleri yavaş çalışıyor önerir. Merhaba neden açık değilse, bazı zamanlama kod eklemeyi göz önünde bulundurun ve trackMetric çağrılarında hello kez gönderin.

### <a name="improve-slow-pages"></a>Yavaş sayfa geliştirmek
Biz toorepeat denemez şekilde sunucu yanıtlarını ve sayfa yükleme sürelerinin artırma önerileri, tam bir Web sitesi tüm buraya. İşte, yalnızca tooget bildiğiniz birkaç ipucu, düşünüyorum:

* Yavaş büyük dosyalar nedeniyle yükleniyor: hello betikleri ve diğer bölümleri zaman uyumsuz olarak yükler. Betik paketleme kullanın. Merhaba ana sayfa verilerine ayrı olarak yük pencere öğeleri sonu. Uzun tablolar için eski düz HTML gönderme: JSON veya diğer compact biçimi olarak bir komut dosyası toorequest hello veri kullanın, sonra hello tablo yerinde doldurun. Tüm Bu harika çerçeveler toohelp vardır. (Bunlar da büyük komut dosyaları, Elbette oluşturulmasını gerektirir.)
* Yavaş sunucu bağımlılıkları: hello bileşenleriniz coğrafi konumlarda göz önünde bulundurun. Azure kullanıyorsanız, örneğin, hello web sunucusu ve hello veritabanı hello olduğundan emin olun aynı bölgede. Sorguları ihtiyaç duydukları daha fazla bilgi almak? Önbelleğe alma veya Yardım toplu işleme musunuz?
* Kapasite sorunları: yanıt sürelerinin sunucu ölçümlere hello bakın ve istek sayısı. İstek sayısı genişliğindeki yükselmeleri ile yanıt sürelerini orantısız en yüksek, sunucularınızın uzatılır olasıdır.


## <a name="server-response-time-degradation"></a>Sunucu yanıt süresi düşüşü

Merhaba yanıt süresi düşüşü bildirimi size bildirir:

* Bu işlem için toonormal yanıt süresi Hello yanıt süresi karşılaştırılan.
* Kaç tane kullanıcılar etkilenir.
* Ortalama yanıt süresi ve hello algılama ve 7 gün önce hello gün üzerinde bu işlem için 90 yüzdebirlik yanıt süresi. 
* Merhaba günde hello algılama ve 7 gün önce bu işlemi isteği sayısı.
* Bu işlemde bozulması ve ilgili bağımlılıklar degradations arasında bağıntı. 
* Merhaba sorunu tanılamak toohelp bağlar.
  * Profil Oluşturucu görüntülemek işlemi zamanın nerede harcandığına toohelp izler (Merhaba bağlantı profil oluşturucu izleme örnekler hello algılama süre boyunca bu işlem için toplanan kullanılabilir). 
  * Performans raporları Gezgini'nde ölçüm burada dilim ve bu işlem için zaman aralığı/filtreleri inin.
  * Bu Ara tooview belirli çağrıları özellikleri çağırır.
  * Hata raporları - durumunda > 1 Bu anlamına tooperformance düşüşü katkıda bulunan bu işlemde hatalar oldu sayısı.

## <a name="dependency-duration-degradation"></a>Bağımlılık süresi düşüşü

Modern uygulamanın daha da fazla tooheavy güvenilirlik dış hizmetler hakkında müşteri adayları, çoğu durumda, mikro hizmetler tasarım yaklaşımı benimsemeye. Örneğin, uygulamanızın bazı veri platformda dayalıysa, kendi yapı olsa bile bot, hizmet veya bazı bilişsel Hizmetler Sağlayıcısı tooenable, aracılarını toointeract fazla insan şekillerde ve bazı verileri depolamak hizmeti bot toopull hello için büyük olasılıkla geçiş gelen yanıtlar.  

Örnek bağımlılık düşüşü bildirimi:

![Bağımlılık süresi düşüşü algılama bir örneği burada verilmiştir](./media/app-insights-proactive-diagnostics/dependency_duration_degradation.png)

Size bildirir dikkat edin:

* Bu işlem için toonormal yanıt süresi Hello süresi karşılaştırma
* Kaç kullanıcının etkilenen
* Ortalama süreye ve 90 yüzdebirlik süresince bu bağımlılığı hello algılama hello gününü ve 7 gün önce
* Merhaba algılama hello gününü ve 7 gün önce çağrı bağımlılık sayısı
* Merhaba sorunu tanılamak toohelp bağlar
  * Bu bağımlılığı ölçüm Explorer'da performans raporları
  * Bu bağımlılık Ara tooview çağrıları özellikleri çağırır.
  * Merhaba algılama başarısız bağımlılığı olan bu ortalama çağrı sırasında sayısı > 1, hata raporları - tooduration düşüşü katkıda bulunan süresi. 
  * Bu bağımlılık süresi ve sayısını hesaplamak sorgularıyla Analytics açın  

## <a name="smart-detection-of-slow-performing-patterns"></a>Yavaş gerçekleştirme desenleri akıllı algılama 

Application Insights, kullanıcılarınızın kısmı etkiler veya yalnızca bazı durumlarda kullanıcıları etkileyen performans sorunlarını bulur. Örneğin, sayfa yükleme hakkında tarayıcı diğer türler tarayıcıların, bir tür slowler bildirimidir veya istekleri daha yavaş belirli bir sunucudan hizmet alır. Belirli bir işletim sistemi kullanan istemciler için bir coğrafi alanda yavaş sayfa yükler gibi özellikleri bileşimleri ile ilgili sorunları da bulabilir.  

Bu gibi bozukluklar çok zor toodetect hello veri inceleyerek, ancak düşündüğünüzden daha yaygın. Çoğunlukla bunlar müşterilerinizin şikayetçi olduğunda yalnızca yüzey. O zamana dek çok geç: hello etkilenen kullanıcılar zaten tooyour rakiplere geçiş!

Şu anda bizim algoritmalar, sayfa yükleme sürelerinin, istek yanıt sürelerini hello sunucusunda ve bağımlılık yanıt sürelerini bakın.  

Eşikleri tooset sahip yok ya da kurallarını yapılandırın. Machine learning ve veri araştırma algoritmalarını kullanılan toodetect anormal desenleri alır.

![Merhaba bağlantı tooopen hello tanılama raporu azure'da Hello e-posta uyarıdan'ı tıklatın](./media/app-insights-proactive-performance-diagnostics/03.png)

* **Zaman** hello zaman hello sorunu algılandı gösterir.
* **Ne** açıklar:

  * algılandı hello sorunu;
  * Merhaba Hello özelliklerini hello sorunlu davranış görüntülenen bulduk olayların ayarlayın.
* Merhaba tablo hello gerçekleştirme hatalı kümesiyle hello ortalama tüm diğer olaylar davranışını karşılaştırır.

Hello bağlantılar tooopen ölçüm Gezgini ve arama ilgili raporları, başlangıç saati ve hello kümesi gerçekleştirme yavaş özelliklerini filtre'ı tıklatın.

Merhaba zaman aralığı ve filtreleri tooexplore hello telemetri değiştirin.

## <a name="next-steps"></a>Sonraki adımlar
Bu tanılama araçları hello telemetriyi uygulamanızdan incelemek yardımcı olur:

* [Profil Oluşturucu](app-insights-profiler.md) 
* [Anlık görüntü hata ayıklayıcı](app-insights-snapshot-debugger.md)
* [Analizler](app-insights-analytics-tour.md)
* [Analytics akıllı tanılama](app-insights-analytics-diagnostics.md)

Akıllı algılamaların tamamen otomatik olarak yapılır. Ancak, belki de daha fazla bazı uyarılar tooset ister misiniz?

* [El ile yapılandırılmış ölçüm uyarıları](app-insights-alerts.md)
* [Kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md)
