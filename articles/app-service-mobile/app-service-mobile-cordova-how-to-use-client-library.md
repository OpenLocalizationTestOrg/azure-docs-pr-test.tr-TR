---
title: "aaaHow tooUse Azure Mobile Apps için Apache Cordova eklentisi"
description: "Nasıl tooUse Azure Mobile Apps için Apache Cordova eklentisi"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>Nasıl Azure Mobile Apps için toouse Apache Cordova istemci kitaplığı
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Bu kılavuz hello son kullanarak tooperform genel senaryolar öğretilmektedir [Azure Mobile Apps için Apache Cordova eklentisi]. Yeni tooAzure mobil uygulamalar varsa, ilk tamamlamak [Azure Mobile Apps Hızlı Başlangıç] toocreate bir arka uç bir tablo oluşturun ve önceden oluşturulmuş bir Apache Cordova projenizi indirin. Bu kılavuzda, biz hello istemci tarafında odaklanmak Apache Cordova eklentisi.

## <a name="supported-platforms"></a>Desteklenen platformlar
Apache Cordova v6.0.0 ve daha sonra iOS, Android ve Windows bu SDK destekleyen cihazlar.  Merhaba platform desteği aşağıdaki gibidir:

* Android API 19-24 (KitKat Nougat aracılığıyla).
* iOS 8.0 ve sonraki sürümleri.
* Windows Phone 8.1.
* Evrensel Windows platformu.

## <a name="Setup"></a>Kurulum ve Önkoşullar
Bu kılavuz, bir tablo ile bir arka uç oluşturduğunuzu varsayar. Bu kılavuz o hello tablolu hello varsayar bu öğreticiler hello tablolarla aynı şema. Bu kılavuz, ayrıca hello Apache Cordova eklentisi tooyour kodu eklemiştir varsayar.  Bunu yapmadıysanız hello komut satırında hello Apache Cordova eklentisi tooyour proje ekleyebilirsiniz:

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Oluşturma hakkında daha fazla bilgi için [ilk Apache Cordova uygulamanızı], kendi belgelerine bakın.

## <a name="ionic"></a>Ionic v2 uygulama ayarlama

tooproperly Ionic v2 projesinde yapılandırmak, ilk temel bir uygulama oluşturun ve hello Cordova eklentisi ekleyin:

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Çok satırlardan hello eklemek`app.component.ts` toocreate hello istemci nesnesi:

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

Şimdi, yapı ve başlangıç projesi hello tarayıcıda çalıştırın:

```
ionic platform add browser
ionic run browser
```

Hello Azure Mobile Apps Cordova eklentisi her iki Ionic v1 ve v2 uygulamaları destekler.  Merhaba Ionic v2 uygulamaları ek bildirimi Merhaba gerekir. yalnızca `WindowsAzure` nesnesi.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Nasıl yapılır: kullanıcıların kimlik doğrulaması
Azure uygulama hizmeti, kimlik doğrulaması ve çeşitli dış kimlik sağlayıcılarını kullanarak uygulama kullanıcıları yetkilendirmek destekler: Facebook, Google, Microsoft Account ve Twitter. Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz. Sunucu komut dosyalarında kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz. Daha fazla bilgi için bkz: Merhaba [kimlik doğrulamayı kullanmaya başlama] Öğreticisi.

Kimlik doğrulaması bir Apache Cordova uygulaması kullanırken, Cordova eklenti aşağıdaki hello kullanılabilir olması gerekir:

* [cordova-plugin-device]
* [cordova eklentisi inappbrowser]

İki kimlik doğrulama akışı desteklenir: sunucu akışı ve bir istemci akışı.  Merhaba sağlayıcının web kimlik doğrulaması arabirimde alacağından hello sunucu akış hello Basit kimlik doğrulama deneyimi sağlar. Merhaba istemci akışı aygıta özgü özellikleri ile daha derin tümleştirme gibi izin verir çoklu oturum açma sağlayıcıya özgü aygıta özgü SDK'ları üzerinde alacağından.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Nasıl yapılır: Mobil uygulama hizmetiniz için dış yönlendirme URL'lerini yapılandırın.
Apache Cordova uygulamaları çeşitli OAuth UI akar geri döngü yetenek toohandle kullanın.  Localhost üzerinde OAuth UI akışları hello kimlik doğrulama hizmeti yalnızca bilir beri sorunlara neden nasıl tooutilize varsayılan olarak, hizmet.  Sorunlu OAuth UI akışları örnekleri şunlardır:

* Merhaba Ripple öykünücüsü.
* Yeniden Ionic ile canlı.
* Merhaba mobil arka uç yerel olarak çalıştırma
* Merhaba mobil arka uç hello bir sağlayan kimlik doğrulama'den farklı bir Azure uygulama hizmeti çalışıyor.

Bu yönergeler tooadd yerel ayarları toohello yapılandırmanızı izleyin:

1. İçinde toohello oturum [Azure portalı]
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın hello adını tıklatın.
3. Tıklatın **araçları**
4. Tıklatın **kaynak Gezgini** hello GÖZLEMLE menüde, ardından **Git**.  Yeni bir pencere veya sekmesinde açar.
5. Merhaba genişletin **config**, **authsettings** hello sol gezinti sitenizdeki düğümlerin.
6. Tıklatın **Düzenle**
7. Merhaba "allowedExternalRedirectUrls" öğesini arayın.  Toonull veya bir dizi değere ayarlanabilir.  Aşağıdaki değeri hello değeri toohello değiştirin:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Merhaba URL'leri hizmetinizi hello URL'ler ile değiştirin.  Örnekler (Merhaba Node.js örnek hizmeti için) "http://localhost: 3000" veya "http://localhost:4400" (Merhaba Ripple hizmeti) içerir.  Ancak, bu URL'ler örnekler - hello örneklerde, belirtilen hello Hizmetleri dahil olmak üzere durumunuz farklı değildir.
8. Merhaba tıklatın **okuma/yazma** Merhaba ekranında sağ üst köşesindeki hello düğmesi.
9. Merhaba yeşil tıklatın **PUT** düğmesi.

Bu noktada kaydedilmiş Hello ayarları.  Hello ayarları bitinceye kadar hello tarayıcı penceresini kapatmayın kaydediliyor.
Ayrıca uygulama hizmetiniz için bu geri döngü URL'leri toohello CORS ayarları ekleyin:

1. İçinde toohello oturum [Azure portalı]
2. Seçin **tüm kaynakları** veya **uygulama hizmetleri** mobil uygulamanızın hello adını tıklatın.
3. Merhaba ayarlar dikey penceresi otomatik olarak açılır.  ' I içermiyorsa tıklatırsanız **tüm ayarları**.
4. Tıklatın **CORS** hello API menüsü altında.
5. Sağlanan hello kutusunda tooadd istediğiniz hello URL'sini girin ve Enter tuşuna basın.
6. Gerektiğinde ek URL'leri girin.
7. Tıklatın **kaydetmek** toosave hello ayarları.

Merhaba yeni ayarları tootake etkisi yaklaşık olarak 10-15 saniye sürer.

## <a name="register-for-push"></a>Nasıl yapılır: anında iletme bildirimleri için
Merhaba yüklemek [phonegap eklentiyi itme] toohandle anında iletme bildirimleri.  Bu eklenti kullanarak kolayca eklenebilen `cordova plugin add` hello komut satırında veya Visual Studio içinde hello Git eklentisi yükleyici aracılığıyla komutu.  Apache Cordova uygulamanızı aşağıdaki kodda Cihazınızı anında iletme bildirimleri için kaydeder:

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

Merhaba Notification Hubs SDK'sı toosend anında iletme bildirimleri hello sunucusundan kullanın.  Hiçbir zaman doğrudan istemcilerden anında iletme bildirimleri gönderme. Bunu yapmak nedenle oluşturulamadı kullanılan tootrigger bir hizmet reddi saldırısına karşı bildirim hub'ları olması veya PNS hello.  Merhaba PNS trafiğinizi bu tür saldırıları sonucunda bSunucu.

## <a name="more-information"></a>Daha fazla bilgi

Ayrıntılı API ayrıntılarda bulabilirsiniz bizim [API belgelerine](http://azure.github.io/azure-mobile-apps-js-client/).

<!-- URLs. -->
[Azure portalı]: https://portal.azure.com
[Azure Mobile Apps Hızlı Başlangıç]: app-service-mobile-cordova-get-started.md
[kimlik doğrulamayı kullanmaya başlama]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure Mobile Apps için Apache Cordova eklentisi]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[ilk Apache Cordova uygulamanızı]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap eklentiyi itme]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova eklentisi inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
