---
title: "aaaAzure bildirim hub'ları"
description: "Nasıl tooadd anında bildirim yetenekleri Azure Notification Hubs ile bilgi edinin."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a>Azure Notification Hubs
## <a name="overview"></a>Genel Bakış
Azure bildirim hub'ları, kullanımı kolay, çok platformlu, ölçeği itme altyapısı sağlar. Bir tek platformlar arası API çağrısı ile tüm Bulut veya şirket içi arka ucundan hedeflenen ve kişiselleştirilmiş anında iletme bildirimleri tooany mobil platformda kolayca gönderebilirsiniz.

Bildirim hub'ları hem kuruluş hem de tüketici senaryoları için harika çalışır. Müşteriler için Notification Hubs kullanma birkaç örnek aşağıda verilmiştir:

* En son haberleri bildirimleri toomillions düşük gecikme süresine sahip gönderin.
* Toointerested kullanıcı kesimlerini konum temelli kuponlar gönderin.
* Olay ilgili bildirimler toousers veya medya/Spor/Finans/oyun uygulamaları için grupları gönderin.
* Promosyon içeriği tooapps tooengage ve Pazar toocustomers iletin.
* Yeni iletiler gibi Kurumsal olaylar kullanıcıları bilgilendirin ve iş öğeleri.
* Çok faktörlü kimlik doğrulama kodları gönderin.

## <a name="what-are-push-notifications"></a>Anında İletme Bildirimleri nedir?
Anında iletme bildirimleri olan bir form uygulama kullanıcı iletişim nerede mobil uygulamaları kullanıcılarının belirli istenen bilgileri, genellikle bir açılır pencere veya iletişim kutusu size bildirilir. Kullanıcıları, genellikle tooview seçin veya hello iletiyi yok sayın ve hello eski seçme hello bildirim iletilen hello mobil uygulama açılacaktır.

Anında iletme bildirimleri güncel iş bilgilerini iletişim Kurumsal uygulamaları ve uygulamaya katılımı ve kullanımı artan tüketici uygulamaları için önemli. İlgili uygulamalar etkin olmasa da enerji tasarrufu sağlayan mobil cihazlar için hello bildirimleri Göndericiler için esnek ve kullanılabilir olduğundan hello en iyi uygulama kullanıcı iletişimini değildir.

Birkaç popüler platformlar için anında iletme bildirimleri hakkında daha fazla bilgi için:
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>Anında İletme Bildirimleri Nasıl Çalışır?
Anında iletme bildirimleri adlı platforma özgü altyapılar aracılığıyla teslim edilir *Platform bildirim sistemleri* (PNSes). Bunlar toodelivery ileti tooa aygıtla bir sağlanan işlemek ve ortak arabirim içermez barebone itme işlevler sunar. toosend bir bildirim tooall müşteriler hello iOS, Android ve Windows sürümlerinde, bir uygulamanın hello Geliştirici gerekir iş APNS (Apple Push Notification hizmeti), FCM (Firebase Cloud Messaging) ve WNS (Windows bildirim hizmeti), toplu işleme sırasında Merhaba gönderir.

Yüksek bir düzeyde İşte nasıl anında iletme çalışır:

1. Merhaba istemci uygulaması tooreceive, bu nedenle kişiler hello PNS tooretrieve karşılık gelen, benzersiz ve geçici gönderim tanıtıcısını iter istediği karar verir. Merhaba tanıtıcı türü (URI'ler örneğin WNS APNS belirteçleri sahipken sahiptir) "Merhaba sistemine bağlıdır.
2. Merhaba istemci uygulaması bu tanıtıcıyı hello uygulama arka ucu veya sağlayıcı depolar.
3. toosend bir anında iletme bildirimi, hello uygulama arka uç hello PNS hello tanıtıcı tootarget belirli istemci uygulaması kullanarak iletişim kurar.
4. Merhaba PNS hello tanıtıcı tarafından belirtilen hello bildirim toohello aygıt iletir.

![][0]

## <a name="hello-challenges-of-push-notifications"></a>Merhaba anında iletme bildirimleri zorlukları
Yayın veya anında iletme bildirimleri toosegmented kullanıcılara gönderme gibi sipariş tooimplement bile ortak anında iletme bildirimi senaryolarda PNSes güçlü olsa da, bunlar kadar iş toohello uygulama geliştiricisi bırakın.

Anında iletme biridir hello çalışma ilgisiz toohello uygulamanın ana iş mantığı olan karmaşık altyapılar gerektirdiğinden mobil bulut Hizmetleri özellikleri en istendi. Merhaba infrastructural zorluklarından bazıları şunlardır:

* **Platform bağımlılığı**: 

  * PNSes değil birleşik gibi hello arka uç toohave karmaşık ve sabit korumak platforma bağımlı mantığı toosend bildirimleri toodevices çeşitli platformlarda gerekir.
* **Ölçek**:

  * PNS yönergelerine göre her uygulama başlatmada cihaz belirteçleri yenilenmelidir. Bu çok miktarda trafiği hello arka uç ilgilenme ve veritabanına erişim yalnızca tookeep hello belirteçlerini güncel anlamına gelir. Cihaz Hello sayısını toohundreds ve milyonlarca binlerce büyürken oluşturma ve bu altyapısını sürdürme hello yoğun maliyetidir.
  * Çoğu PNSes yayın toomultiple cihazlar desteklemez. Bu basit bir yayın tooa bir milyon çağrıları toohello PNSes milyon aygıtları sonuçlarında anlamına gelir. Bu trafik miktarı en düşük gecikme süresi ile ölçeklendirme ölçeklendirebilmek kolay değildir.
* **Yönlendirme**:
  
  * Bir şekilde toosend iletileri toodevices PNSes sağlar ancak çoğu uygulamaları bildirimleri kullanıcılara veya ilgi alanı gruplarına hedeflenir. Bu, bir kayıt defteri tooassociate aygıtlarla ilgi alanı gruplarına, kullanıcılar, özellikler, vb. hello arka uç korumalıdır anlamına gelir. Bu ek yükü, bir uygulamanın toohello zaman toomarket ve bakım maliyetlerinin ekler.

## <a name="why-use-notification-hubs"></a>Neden Notification Hubs Kullanmalıyım?
Bildirim hub'ları ortadan kaldırır, etkinleştirme ile ilişkili tüm karmaşıklık push kendi. Kendi çok platformlu, ölçeği anında iletme bildirimi altyapısı itme ilgili kodları azaltır ve arka basitleştirir. Bildirim hub'larıyla aygıtları hello arka uç iletileri toousers veya ilgi alanı gruplarına hello aşağıdaki şekilde gösterildiği gibi gönderirken kendi PNS tanıtıcılarını bir hub ile kaydetmekten yalnızca sorumlu şunlardır:

![][1]

Bildirim hub'ları kullanıma hazır itme altyapınız avantajları aşağıdaki hello ile verilmiştir:

* **Platformlar arası**

  * İOS, Android, Windows ve Kindle ve Baidu dahil tüm büyük gönderme platformlar için destek.
  * Bir ortak arabirimi toopush tooall platformlarda hiçbir platforma özgü iş platforma özgü veya platformdan bağımsız biçimleri.
  * Aygıt Yönetimi tek bir yerde işleyin.
* **Arka uçlarını arası**
  
  * Bulut veya şirket içi
  * .NET, Node.js, Java, vs.
* **Zengin teslim düzeni kümesi**:

  * *Yayın tooone veya birden çok platform*: tek bir API çağrısı ile platformlarda cihazların toomillions anında yayınlayabilirsiniz.
  * *Toodevice anında*: bildirimleri tooindividual aygıtları hedefleyebilirsiniz.
  * *Toouser anında*: etiketleri ve şablonları özellikleri, bir kullanıcının tüm platformlar arası cihazlara ulaşmak yardımcı olur.
  * *İtme dinamik etiketlerle toosegment*: etiketler özelliği segmentlere aygıtları ve tooone segment veya bir ifade kesimleri (örneğin etkin ve yaşamlarını yeni kullanıcı Seattle değil) göndermek isteyip tooyour gereksinimlerine göre toothem anında yardımcı olur. Kısıtlı toopub-sub yerine herhangi bir yere aygıt etiketleri güncelleştirebilir ve zaman.
  * *Yerelleştirilmiş itme*: şablonları özelliği, arka uç kodunu etkilemeden yerelleştirme elde yardımcı olur.
  * *Sessiz anında*: sağlar hello gönderme çekme düzeni sessiz bildirimleri toodevices gönderme ve toocomplete tetikleme belirli çeken veya eylemler.
  * *Zamanlanmış itme*: toosend bildirimleri çıkışı dilediğiniz zaman zamanlayabilirsiniz.
  * *Doğrudan itme*: bizim hizmeti ve doğrudan toplu iş gönderme tooa cihaz tanıtıcılarını listesi ile kayıt cihazları atlayabilirsiniz.
  * *Kişiselleştirilmiş anında iletme*: cihaz bildirme değişkenleri aygıta özgü gönderdiğiniz yardımcı kişiselleştirilmiş anında iletme bildirimleri özelleştirilmiş anahtar-değer çiftleri ile.
* **Zengin telemetri**
  
  * Genel anında iletme, aygıt, hata ve işlem telemetri hello Azure portalında kullanılabilir ve program aracılığıyla.
  * İleti Telemetri parçaları her zorlama başarıyla hello toplu işleme, ilk isteği çağrısı tooour hizmetinden iter.
  * Platform bildirim sistemi geri bildirim Platform bildirim sistemleri tooassist hata ayıklama içindeki tüm görüşleri iletişim kurar.
* **Ölçeklenebilirlik** 
  
  * Hızlı ileti toomillions mimarisinin yeniden düzenlenmesinden veya aygıt parçalama olmadan aygıtların gönderin.
* **Güvenlik**

  * Paylaşılan erişim gizli anahtarı (SAS) veya Federasyon kimlik doğrulaması.

## <a name="integration-with-app-service-mobile-apps"></a>App Service Mobile Apps ile Tümleştirme
Azure Hizmetleri genelinde kesintisiz ve birleştirici bir deneyimi toofacilitate [App Service Mobile Apps] bildirim hub'ları kullanarak anında iletme bildirimleri için yerleşik desteğe sahiptir. [App Service Mobile Apps] Kurumsal geliştiriciler ve sistem zengin bir özellikler kümesi toomobile geliştiriciler tümleştiricileri için yüksek düzeyde ölçeklenebilir, genel olarak kullanılabilir bir mobil uygulama geliştirme platformu sunar.

Mobile Apps geliştiricileri Notification Hubs ile iş akışı aşağıdaki hello kullanabilir:

1. Cihaz PNS tanıtıcısını alma
2. Uygun Mobile Apps istemci SDK'sı kayıt API'si yoluyla Notification hubs'a cihazı kaydedin
   * Mobile Apps'in güvenlik amacıyla kayıtlardaki tüm etiketleri kaldırdığını unutmayın. Aygıtlarla tooassociate etiketler doğrudan arka ucunuzdan Notification Hubs ile çalışın.
3. Uygulama arka ucunuzdan Notification Hubs ile bildirimler gönderme

Bu tümleştirme ile toodevelopers bazı kolaylıklar şunlardır:

* **Mobile Apps istemci SDK'ları**: Bu çoklu platform SDK'ları kayıt için basit API'ler sağlar ve toohello bildirim hub'ı otomatik olarak bağlantılı hello mobil uygulama ile görüşün. Geliştiriciler değil Notification Hubs kimlik bilgilerini aracılığıyla toodig gerekir ve ek bir hizmet ile çalışabilirsiniz.

  * *Anında toouser*: hello SDK'ları otomatik olarak Mobile Apps kimliği doğrulanmış kullanıcı kimliği tooenable itme toouser senaryo aygıtla verilen hello etiketi.
  * *Toodevice anında*: hello SDK'ları otomatik olarak kullan hello Mobile Apps yükleme kimliği GUID tooregister geliştiricileri birden çok hizmet GUID'i saklama hello zahmetinden kurtarır Notification Hubs ile olarak.
* **Yükleme modeli**: tüm itme anında iletme bildirimi Hizmetleri ile hizalanan ve kolay toouse olan bir JSON yüklemesi bir aygıt ile ilişkili özellikleri Notification Hubs son itme modeli toorepresent Mobile Apps çalışır.
* **Esneklik**: geliştiriciler doğrudan Notification Hubs ile toowork hello tümleştirmesiyle bile her zaman yerinde seçebilirsiniz.
* **Tümleşik deneyim [Azure portal]**: bir özelliği mobil uygulamalarda görsel olarak temsil edilir ve geliştiriciler Mobile Apps aracılığıyla hello ilişkili bildirim hub'ı ile kolayca çalışabilir gibi anında.

## <a name="next-steps"></a>Sonraki Adımlar
Bu konu başlıklarında Notification Hubs hakkında daha fazla bilgi bulabilirsiniz:

* **[Müşteriler Notification Hubs'ı nasıl kullanıyor?]**
* **[Notification Hubs eğiticileri ve kılavuzları]**
* **Bildirim hub'ları başlama öğreticileri**: [iOS], [Android], [Windows Evrensel], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[Müşteriler Notification Hubs'ı nasıl kullanıyor?]: http://azure.microsoft.com/services/notification-hubs
[Notification Hubs eğiticileri ve kılavuzları]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[Windows Evrensel]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[App Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[Azure portal]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
