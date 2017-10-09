---
title: "Azure bildirim hub'ları: Sık sorulan sorular (SSS) | Microsoft Docs"
description: "Bildirim hub'ları üzerinde çözümleri tasarlama/uygulama konusunda sık sorulan sorular"
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: "anında iletme bildirimi, anında iletme bildirimleri, iOS anında iletme bildirimleri, android anında iletme bildirimleri, ios anında iletme, android anında iletme"
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Anında iletme bildirimleri ile Azure Notification Hubs: sık sorulan sorular
## <a name="general"></a>Genel
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>Bildirim hub'larını hello kaynak yapısı nedir?

Azure bildirim hub'ları sahip iki kaynak düzey: hub'ları ve ad alanları. Bir hub'ı bir uygulama hello platformlar arası anında bilgileri içerebilen bir tek itme kaynaktır. Bir ad alanı, hub'ları bir bölgede koleksiyonudur.

Önerilen eşleme bir uygulama içeren bir ad ile eşleşir. Ad alanı içinde üretim uygulamanızın üzerinde çalıştığı bir üretim hub, sınama uygulama vb. ile çalışan test hub'ı sahip olabilir.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>Bildirim hub'ları için hello fiyat modeli nedir?
Merhaba son fiyatlandırma ayrıntıları hello üzerinde bulunabilir [bildirim hub'ları fiyatlandırması] sayfası. Bildirim hub'ları hello ad alanı düzeyinde faturalandırılır. (Bir ad alanı tanımını hello için bkz: "Merhaba kaynak yapısı bildirim hub'larını nedir?") Bildirim hub'ları üç sunar:

* **Ücretsiz**: Bu katmanı gönderme özellikleri keşfetmek için iyi bir başlangıç noktası olduğu. Üretim uygulamaları için önerilmez. 500 aygıtları alın ve hizmet düzeyi sözleşmesi (SLA) garanti ile 1 milyondan fazla ad alanı, ayda başına dahil edilen iter.
* **Temel**: Bu bağlayıcıya (veya hello standart katmanı) küçük üretim uygulamaları için önerilir. 200.000 aygıtları alın ve 10 milyon başına aylık başlangıç noktası olarak ad alanı dahil iter. Kota büyüme seçenekleri dahil edilir.
* **Standart**: Bu katmanı Orta toolarge üretim uygulamaları için önerilir. 10 milyon aygıtları alın ve 10 milyon başına aylık başlangıç noktası olarak ad alanı dahil iter. Kota artırma seçenekleri ve zengin telemetri yetenekleri dahil edilir.

Standart katman özellikleri:
* **Zengin telemetri**: ileti Telemetri başına bildirim hub'ları tootrack kullanabileceğiniz herhangi gönderme istekleri ve Platform bildirim sistemi geri bildirim hata ayıklama için.
* **Çoklu müşteri mimarisi**: bir ad alanı düzeyinde Platform bildirim sistem kimlik bilgileri ile çalışabilirsiniz. Bu seçenek, tooeasily kiracılar hello içinde hubs bölünmüş sağlar aynı ad.
* **Zamanlanmış itme**: dilediğiniz zaman gönderilen bildirimler toobe zamanlayabilirsiniz.

### <a name="what-is-hello-notification-hubs-sla"></a>Merhaba bildirim hub'ları SLA nedir?
Temel ve standart bildirim hub'ları katmanları için doğru yapılandırılmış uygulamaları anında iletme bildirimleri göndermek veya kayıt yönetimi en az hello süresinin yüzde 99,9 işlemleri. Merhaba SLA, Git toohello hakkında daha fazla toolearn [bildirim hub'ları SLA](https://azure.microsoft.com/support/legal/sla/notification-hubs/) sayfası.

> [!NOTE]
> Anında iletme bildirimleri üçüncü taraf Platform bildirim sistemleri (örneğin, Apple APNS ve Google FCM) bağımlı olduğundan, bu iletiler, hello teslimi için SLA garantisi yoktur. Bildirim hub'ları hello toplu tooPlatform bildirim sistemleri (garanti SLA) gönderir sonra (SLA garanti) hello Platform bildirim sistemleri toodeliver hello hello sorumluluğunda iter olur.

### <a name="which-customers-are-using-notification-hubs"></a>Hangi müşterilerin bildirim hub'ları kullanıyor musunuz?
Birçok müşteri bildirim hub'ları kullanın. Bazı önemli olanları aşağıda listelenmiştir:

* Sochi 2014: İlgi alanı gruplarına, 3 + milyon aygıtları ve iki hafta içinde gönderilen 150 + milyon bildirimler yüzlerce. [Örnek olay incelemesi: Sochi]
* Skanska: [örnek olay incelemesi: Skanska]
* Seattle süresi: [örnek olay incelemesi: Seattle saatleri]
* Mural.LY: [örnek olay incelemesi: Mural.ly]
* 7Digital: [örnek olay incelemesi: 7Digital]
* Bing uygulamalar: Cihazları milyonlarca günde 3 milyon bildirimleri gönderin.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>Nasıl yükseltme veya my hub veya ad alanı tooa farklı katmanı düşürmek?
Toohello Git  **[Azure portal]** > **bildirim hub'ları ad alanları** veya **bildirim hub'ları**. Tooupdate istediğiniz ve çok Git hello kaynağı seçin**fiyatlandırma katmanı**. Hello gereksinimleri aşağıdaki dikkat edin:

* Merhaba güncelleştirilmiş fiyatlandırma katmanı çok geçerlidir*tüm* hub'ları ile çalışırken hello ad.
* Cihaz sayısı için olana hello katmanının hello sınırını aşarsa, indirgeme önce toodelete aygıtları gerekir.


## <a name="design-and-development"></a>Tasarım ve geliştirme
### <a name="which-server-side-platforms-do-you-support"></a>Sunucu tarafı platformları destekliyor?
Sunucu SDK'ları, .NET, Java, Node.js, PHP ve Python için kullanılabilir. Farklı platformlarda kullanıyorsanız veya ek bağımlılık istemediğiniz doğrudan REST API'leri ile çalışabilmek için bildirim hub'ları API'leri, REST arabirimleri temel alır. Daha fazla bilgi için toohello Git [bildirim hub'ları REST API'leri] sayfası.

### <a name="which-client-platforms-do-you-support"></a>Hangi istemci platformlarını destekliyor?
Anında iletme bildirimleri için desteklenen [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [Windows Evrensel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [(aracılığıyla, Baidu) Android Çin](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) ve [Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome uygulamaları](notification-hubs-chrome-push-notifications-get-started.md), ve [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari). Daha fazla bilgi için toohello Git [bildirim hub'ları başlama öğreticileri] sayfası.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>SMS mesajı, e-posta veya web bildirimleri destekliyor musunuz?
Bildirim hub'ları öncelikle tasarlanmış toosend bildirimleri toomobile uygulamaları olur. İleti özellikleri e-posta veya metin sağlamaz. Ancak, bu yetenekleri sağlamak üçüncü taraf platformları ile bildirim hub'ları toosend yerel anında iletme bildirimleri kullanarak tümleştirilebilir [Mobile Apps].

Bildirim hub'ları da sağlamaz hello kutusu dışında bir tarayıcı içi anında bildirim teslim hizmeti. Müşteriler, desteklenen hello sunucu tarafı platformlar üzerinde SignalR kullanarak bu özelliği uygulayabilirsiniz. Merhaba toosend bildirimleri toobrowser hello Chrome sandbox uygulamalarında istiyorsanız bkz [Chrome uygulamaları Öğreticisi].

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>Mobile Apps ve Azure Notification Hubs'ın ilgili şeklini ve ne zaman bunları kullanabilirim?
Mobil varolan varsa geri uygulama sonlandırmak ve tooadd yalnızca hello yetenek toosend anında iletme bildirimleri istediğiniz, Azure bildirim hub'ları kullanabilirsiniz. Mobil uygulama arka ucu sıfırdan yukarı tooset istiyorsanız, Azure App Service'in hello Mobile Apps özelliğini kullanmayı düşünün. Böylece kolayca hello mobil uygulama arka uçtan anında iletme bildirimleri göndermek bir mobil uygulama otomatik olarak bir bildirim hub'ı sağlamasını yapar. Mobile Apps için fiyatlandırma hello temel ücretleri bir bildirim hub'ı içerir. Ne zaman dahil hello aşan iter yalnızca, ücret ödersiniz. Toohello maliyetleri hakkında daha fazla ayrıntı için Git [App Service fiyatlandırması] sayfası.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>Notification Hubs ile anında iletme bildirimleri göndermek istediğinizde kaç cihaz t destekler?
Toohello başvuran [bildirim hub'ları fiyatlandırması] hello desteklenen aygıtların sayısı hakkında ayrıntılı bilgi için sayfa.

10 milyondan fazla kayıtlı cihazlar için destek gerekiyorsa [Bize Ulaşın](https://azure.microsoft.com/overview/contact-us/) doğrudan çözümünüzü ölçek yardımcı.

### <a name="how-many-push-notifications-can-i-send-out"></a>Kaç tane anında iletme bildirimleri için gönderebilirim?
Merhaba seçili katmanına bağlı olarak, Azure Notification Hubs otomatik olarak hello sistemi üzerinden akan bildirim hello sayısı temel alınarak ölçek artırabilir.

> [!NOTE]
> Merhaba genel kullanım maliyeti sunulmasını anında iletme bildirimleri hello sayısına göre artırabilir. Merhaba katmanı sınırları üzerinde hello özetlenen haberdar olduğunuzdan emin olun [bildirim hub'ları fiyatlandırması] sayfası.
> 
> 

Müşterilerimizin bildirim hub'ları toosend milyonlarca anında iletme bildirimlerinin daily parametresini kullanın. Toodo herhangi bir şey özel tooscale hello Azure Notification Hubs kullandığınız sürece, anında iletme bildirimleri erişmek zorunda değildir.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>Ne kadar süreyle mu Al için gönderilen anında iletme bildirimleri tooreach cihazımı?
Burada hello gelen yük tutarlı ve hatta, Azure Notification Hubs en az işleyebilir normal kullanım senaryosunda, *1 milyon anında iletme bildirimi gönderir bir dakika*. Bu oran, etiket hello sayısı, hello yapısını hello gelen gönderir ve diğer dış faktörlere bağlı olarak değişebilir.

Tahmini hello teslimat zamanı sırasında hello hizmet hello hedefleri platformu başına hesaplar ve anında iletilen bildirim hizmeti (PNS) kayıtlı hello etiketleri veya etiket ifadeleri göre iletileri toohello yönlendirir. Bunu hello hello PNS toosend bildirimleri toohello aygıt sorumluluğundadır.

Merhaba PNS bildirimleri teslim etmek için tüm SLA garanti etmez. Bununla birlikte, çoğu anında iletme bildirimleri tootarget cihazlar (genellikle 10 dakika içinde) birkaç dakika içinde tooNotification hub gönderilmeden hello zamandan gönderilir. Birkaç bildirimleri daha fazla zaman alabilir.

> [!NOTE]
> Azure bildirim hub'ları bir ilke içinde yer toodrop toohello PNS 30 dakika içinde teslim olmayan herhangi bir anında bildirim sahiptir. Bu gecikme nedeniyle, bir dizi için oluşabilir, ancak hello PNS, uygulamanızın yaygın olarak azaltma çünkü çoğu.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>Herhangi bir gecikme garanti var mı?
Anında iletme bildirimleri (bir dış, platforma özgü PNS tarafından teslim edilir) Hello yapısı nedeniyle, gecikme garantisi yoktur. Genellikle, anında iletme bildirimleri hello çoğunluğu birkaç dakika içinde dağıtılır.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>Ne tooconsider ad alanları ve bildirim hub'ları ile bir çözüm tasarlarken gerekir?
#### <a name="mobile-appenvironment"></a>Mobil uygulama/ortamı
* Bir bildirim hub'ı ortamı başına mobil uygulama başına kullanın.
* Çok kiracılı bir senaryoda, her bir kiracı ayrı bir hub'ı olmalıdır.
* Hiçbir zaman paylaşımı aynı bildirim hub'ı üretim ve test ortamları için hello. Bu yöntem, bildirimleri gönderirken sorunlara neden olabilir. (Korumalı alan ve üretim gönderme uç noktalar, her biri ayrı kimlik bilgilerine sahip Apple sunar.)
* Varsayılan olarak, test bildirimleri tooyour kayıtlı cihazları hello Azure portal aracılığıyla göndermek ya da Visual Studio Azure tümleşik bileşen hello. Merhaba eşiği hello kayıt havuzundan rastgele seçilir too10 aygıtları ayarlanır.

> [!NOTE]
> Hub'ınızı başlangıçta bir Apple sandbox sertifikayla yapılandırılmış ve daha sonra yeniden yapılandırılan toouse bir Apple üretim sertifikası başarısız olursa hello özgün cihaz belirteçleri geçersizdir. Geçersiz belirteçleri iter toofail neden. Üretim ve test ortamlarınızı ayırmak ve farklı ortamlar için farklı hub'ları kullanın.
> 
> 

#### <a name="pns-credentials"></a>PNS kimlik bilgileri
Uygulama tanımlayıcısı ve güvenlik belirteçleri (örneğin, Apple veya Google) bir platformun Geliştirici Portalı ile mobil uygulama kaydedildikten sonra gönderilir. Böylece toodevices anında iletme bildirimleri gönderilebilir hello uygulama arka ucu bunlar belirteçleri toohello platformun PNS sağlar. Güvenlik belirteçleri hello sertifikaları (örneğin, Apple iOS veya Windows Phone) veya güvenlik anahtarları (örneğin, Google Android veya Windows) biçiminde olabilir. Bildirim hub'ları yapılandırılmalıdır. Yapılandırma genellikle hello bildirim hub'ı düzeyinde yapılır, ancak çok müşterili bir senaryoda hello ad alanı düzeyinde de yapılabilir.

#### <a name="namespaces"></a>ad alanları
Ad alanları dağıtım gruplandırma için kullanılabilir. Bunlar ayrıca tüm bildirim hub'ları tüm kiracılar için kullanılan toorepresent olabilir hello çok müşterili bir senaryoda aynı uygulama.

#### <a name="geo-distribution"></a>Coğrafi dağılımı
Coğrafi dağıtım her zaman anında iletme bildirimi senaryolarda önemli değildir. Anında iletme bildirimleri toodevices teslim çeşitli PNSes (örneğin, APNS veya GCM) dağılımla değil.

Genel olarak kullanılan bir uygulamanız varsa, farklı ad alanlarında hub Merhaba Dünya farklı Azure bölgelerinde hello bildirim hub'ları hizmetini kullanarak oluşturabilirsiniz.

> [!NOTE]
> Özellikle kayıtlar için Yönetim maliyetini artırır Biz bu düzenlenmesi önerilmez. Yalnızca açık bir gereksinimi varsa yapılmalıdır.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>Kayıtlar hello uygulama arka uçtan veya doğrudan istemci cihazları yapmalıyım?
Kayıtlar hello uygulama arka uçtan hello kayıt oluşturmadan önce tooauthenticate istemcileri olduğunda faydalıdır. Oluşturulan veya hello uygulama arka uç uygulama mantığına göre değiştiren etiketleri olduğunda da yararlı oldukları. Daha fazla bilgi için toohello Git [arka uç kaydı Kılavuzu] ve [arka uç kaydı Kılavuzu 2] sayfaları.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>Merhaba anında iletme bildirimi teslimi güvenlik modeli nedir?
Azure bildirim hub'ları kullanan bir [paylaşılan erişim imzası](../storage/common/storage-dotnet-shared-access-signature-part-1.md)-tabanlı güvenlik modeli. Merhaba kök ad alanı düzeyinde veya hello ayrıntılı bildirim hub düzeyindeki hello paylaşılan erişim imzası belirteçleri kullanabilirsiniz. Paylaşılan erişim imzası belirteçleri kümesi toofollow farklı yetkilendirme kuralları, örneğin, toosend ileti izinleri veya bildirim izinleri toolisten olabilir. Daha fazla bilgi için bkz: Merhaba [bildirim hub'ları güvenlik modeli] belge.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>Anında iletme bildirimleri hassas yükünde nasıl işleneceğini?
Tüm bildirimler tootarget cihazlar tarafından hello platformun PNS gönderilir. Bir bildirim tooAzure bildirim hub'ları gönderildiğinde, işlenir ve toohello geçirilen ilgili PNS.

Merhaba gönderen toohello Azure Notification Hubs toohello PNS, gelen tüm bağlantıları HTTPS kullanın.

> [!NOTE]
> Azure bildirim hub'ları hello yükü iletilerinin herhangi bir şekilde günlüğe kaydetmez.
> 
> 

toosend hassas yükü, bir güvenli itme desen kullanmanızı öneririz. Merhaba gönderen bir ping bildirim hello hassas yükü olmadan İleti tanımlayıcısı toohello aygıtıyla sunar. Merhaba cihaza Hello uygulamanın hello yükü aldığında, toofetch hello doğrudan ileti ayrıntılarını hello uygulama güvenli bir API çağırır. Toohello nasıl tooimplement Bu desen hakkında kılavuz için Git [güvenli bildirim hub'ları itme öğretici] sayfası.

## <a name="operations"></a>İşlemler
### <a name="what-support-is-provided-for-disaster-recovery"></a>Olağanüstü durum kurtarma için hangi destek sağlanır?
Bizden (Merhaba bildirim hub'ları adı, hello bağlantı dizesi ve diğer kritik bilgileri) meta veri olağanüstü durum kurtarma kapsamı sunuyoruz. Bir olağanüstü durum kurtarma senaryosunda tetiklendiğinde kayıt hello verilerdir *yalnızca segmentlere* kaybolur hello bildirim hub'ları altyapısının. Bu veriler, yeni hub kurtarma sonrası tooimplement bir çözüm toorepopulate gerekir:

1. Bir ikincil bildirimler hub'ı farklı bir veri merkezinde oluşturun. Merhaba başına tooshield birinden oluşturmanızı öneririz, yönetim özelliklerinizi etkileyebilecek bir olağanüstü durum kurtarma olayı. Merhaba olağanüstü durum kurtarma olayı hello birer de oluşturabilirsiniz.

2. Merhaba ikincil bildirim hub'ı birincil bildirim hub'ınızı hello kayıtları ile doldurun. Biz yoksa, her iki hub toomaintain kayıtları denemenizi öneririz ve kayıtlar geldikçe gibi bunları eşitlenmiş tut. Bu yöntem de hello devralınmış işlemciler kayıtlar tooexpire nedeniyle PNS yan hello üzerinde çalışmıyor. Bildirim hub'ları temizler bunları süresi dolmuş veya geçersiz kayıtlar hakkında PNS geri bildirim aldığı gibi.  

Uygulama arka uçları için iki önerileri sunuyoruz:

* Kayıtlar kendi uçta belirli bir dizi tutan bir uygulama arka uç kullanın. Merhaba ikincil bildirim hub'ına toplu ekleme daha sonra gerçekleştirebilirsiniz.

* Yedek olarak hello birincil bildirim hub'ı kayıtlar normal bir dökümünü alır bir uygulama arka ucu kullanın. Merhaba ikincil bildirim hub'ına toplu ekleme daha sonra gerçekleştirebilirsiniz.

> [!NOTE]
> Kayıtlar içeri/dışarı aktarma işlevleri hello standart katmanında kullanılabilen hello açıklanan [kayıtlar dışa aktarma/içe aktarma] belge.
> 
> 

Hedef cihazlarda Hello uygulama başlatıldığında bir arka uç yoksa, hello ikincil bildirim hub ' yeni bir kayıt gerçekleştirin. Sonunda hello ikincil bildirim hub'ı kayıtlı tüm hello etkin aygıtlar sahip olur.

Açılmamış uygulamalar içeren cihazları bildirimleri zaman almazsınız bir zaman dilimi olacaktır.

### <a name="is-there-audit-log-capability"></a>Denetim günlüğü özelliği var mı?
Hello gösterilen toooperation günlükleri, tüm bildirim hub'ları yönetim işlemlerinin Git [Klasik Azure portalı].

## <a name="monitoring-and-troubleshooting"></a>İzleme ve sorun giderme
### <a name="what-troubleshooting-capabilities-are-available"></a>Sorun giderme hangi özellikler sağlanıyor?
Azure bildirim hub'ları, özellikle hello en yaygın senaryo bırakılan bildirimler için sorun giderme için birçok özellik sağlar. Merhaba Ayrıntılar için bkz [bildirim hub'ları sorun giderme] teknik incelemesi.

### <a name="what-telemetry-features-are-available"></a>Hangi telemetri özellikler sağlanıyor?
Azure Notification Hubs etkinleştirir hello telemetri verilerini görüntüleme [Klasik Azure portalı]. Merhaba ölçümleri ayrıntılarını hello üzerinde kullanılabilir [bildirim hub'ları ölçümleri] sayfası.

> [!NOTE]
> Toohello anında iletme bildirimleri teslim anlamına başarılı bildirimler yalnızca ortalama dış PNS (örneğin, APNS için Apple) veya GCM için Google. Bunu hello hello PNS toodeliver hello bildirimleri tootarget aygıtları sorumluluğundadır. Genellikle, hello PNS teslim ölçümleri toothird tarafların kullanıma sunmuyor.  
> 
> 

Merhaba yetenek tooexport hello telemetri verileri programlı olarak (Merhaba standart katman) de sunuyoruz. Merhaba Ayrıntılar için bkz [bildirim hub'ları ölçümleri örnek].

[Klasik Azure portalı]: https://manage.windowsazure.com
[bildirim hub'ları fiyatlandırması]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[Örnek olay incelemesi: Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[Örnek olay incelemesi: Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[Örnek olay incelemesi: Seattle saatleri]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[Örnek olay incelemesi: Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[Örnek olay incelemesi: 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[bildirim hub'ları REST API'leri]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[bildirim hub'ları başlama öğreticileri]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Chrome uygulamaları Öğreticisi]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[arka uç kaydı Kılavuzu]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[arka uç kaydı Kılavuzu 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[bildirim hub'ları güvenlik modeli]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[güvenli bildirim hub'ları itme öğretici]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[bildirim hub'ları sorun giderme]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[bildirim hub'ları ölçümleri]: https://msdn.microsoft.com/library/dn458822.aspx
[bildirim hub'ları ölçümleri örnek]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[kayıtlar dışa aktarma/içe aktarma]: https://msdn.microsoft.com/library/dn790624.aspx
[Azure portal]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[Mobile Apps]: https://azure.microsoft.com/services/app-service/mobile/
[App Service fiyatlandırması]: https://azure.microsoft.com/pricing/details/app-service/
