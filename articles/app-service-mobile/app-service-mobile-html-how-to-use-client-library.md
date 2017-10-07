---
title: "aaaHow tooUse hello Azure Mobile Apps için JavaScript SDK'sı"
description: "Nasıl Azure Mobile Apps için tooUse v"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Nasıl tooUse hello JavaScript istemci kitaplığı Azure Mobile Apps için
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Bu kılavuz hello son kullanarak tooperform genel senaryolar öğretilmektedir [JavaScript SDK'sı Azure Mobile Apps için]. Yeni tooAzure mobil uygulamalar varsa, ilk tamamlamak [Azure Mobile Apps Hızlı Başlangıç] toocreate bir arka uç ve bir tablo oluşturun. Bu kılavuzda, HTML/JavaScript Web uygulamaları kullanarak hello mobil arka uç odaklanın.

## <a name="supported-platforms"></a>Desteklenen platformlar
Tarayıcı desteği toohello geçerli sınırlamak ve önde gelen tarayıcılar hello sürümleri son: Google Chrome, Microsoft Edge, Microsoft Internet Explorer ve Mozilla Firefox.  Görece modern bir tarayıcı ile Merhaba SDK toofunction bekliyoruz.

Merhaba paket Evrensel JavaScript modülü olarak CommonJS biçimleri ve genel öğeleri, AMD, destekler şekilde dağıtılır.

## <a name="Setup"></a>Kurulum ve Önkoşullar
Bu kılavuz, bir tablo ile bir arka uç oluşturduğunuzu varsayar. Bu kılavuz o hello tablolu hello varsayar bu öğreticiler hello tablolarla aynı şema.

Hello Azure Mobile Apps JavaScript SDK'sı yükleme hello yapılabilir `npm` komutu:

```
npm install azure-mobile-apps-client --save
```

Merhaba kitaplığı CommonJS ortamlarda AMD kitaplığı olarak ve Browserify ve Webpack gibi bir ES2015 modül olarak da kullanılabilir.  Örneğin:

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

Doğrudan sunduğumuz CDN yükleyerek hello SDK önceden oluşturulmuş bir sürümünü de kullanabilirsiniz:

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Nasıl yapılır: kullanıcıların kimlik doğrulaması
Azure uygulama hizmeti, kimlik doğrulaması ve çeşitli dış kimlik sağlayıcılarını kullanarak uygulama kullanıcıları yetkilendirmek destekler: Facebook, Google, Microsoft Account ve Twitter. Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz. Sunucu komut dosyalarında kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz. Daha fazla bilgi için bkz: Merhaba [kimlik doğrulamayı kullanmaya başlama] Öğreticisi.

İki kimlik doğrulama akışı desteklenir: sunucu akışı ve bir istemci akışı.  Merhaba sağlayıcının web kimlik doğrulaması arabirimde alacağından hello sunucu akış hello Basit kimlik doğrulama deneyimi sağlar. Merhaba istemci akışı aygıta özgü özellikleri ile daha derin tümleştirme gibi izin verir çoklu oturum açma sağlayıcıya özgü SDK'ları üzerinde alacağından.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Nasıl yapılır: Mobil uygulama hizmetiniz için dış yönlendirme URL'lerini yapılandırın.
JavaScript uygulamaları çeşitli OAuth UI akar geri döngü yetenek toohandle kullanın.  Bu özellikler şunları içerir:

* Hizmetinizi yerel olarak çalıştırma
* Dinamik yeniden hello Ionic Framework ile kullanma
* TooApp hizmet kimlik doğrulaması için yönlendirme.

Varsayılan olarak, uygulama hizmet kimlik doğrulaması yalnızca olduğundan, mobil uygulamanızın arka ucuna tooallow erişimden yapılandırılmış olduğundan, yerel olarak çalışan sorunlara neden olabilir. Adımları toochange hello App Service ayarlarını tooenable kimlik doğrulaması hello sunucu yerel olarak çalıştırırken aşağıdaki hello kullan:

1. İçinde toohello oturum [Azure portalı]
2. Tooyour mobil uygulama arka ucu gidin.
3. Seçin **kaynak Gezgini** hello içinde **geliştirme araçları** menüsü.
4. Tıklatın **Git** tooopen hello kaynak Gezgini, mobil uygulamanızın arka ucuna yeni sekmesinde veya penceresinde için.
5. Merhaba genişletin **config** > **authsettings** düğümü, uygulamanız için.
6. Merhaba tıklatın **Düzenle** düğmesini tooenable hello kaynak düzenleme.
7. Hello bulur **allowedExternalRedirectUrls** öğesi null olmalıdır. URL'nizde bir dizide ekleyin:

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Merhaba URL'leri hello dizisinde olan bu örnekte hizmetinizi hello URL'ler ile Değiştir `http://localhost:3000` hello yerel Node.js örnek hizmetinin. De kullanabilirsiniz `http://localhost:4400` hello Ripple hizmet veya uygulamanızı nasıl yapılandırıldığına bağlı olarak bazı diğer URL.
8. Merhaba hello sayfanın en üstünde, tıklatın **okuma/yazma**, ardından **PUT** toosave yaptığınız güncelleştirmeler.

Tooadd etmeniz aynı geri döngü URL'leri toohello CORS beyaz liste ayarları hello:

1. Geri toohello gidin [Azure portalı].
2. Tooyour mobil uygulama arka ucu gidin.
3. Tıklatın **CORS** hello içinde **API** menüsü.
4. Merhaba boş her URL girin **izin verilen çıkış noktası** metin kutusu.  Yeni bir metin kutusu oluşturulur.
5. Tıklatın **Kaydet**

Merhaba arka uç güncelleştirildikten sonra uygulamanızda mümkün toouse hello yeni geri döngü URL'ler olacaktır.

<!-- URLs. -->
[Azure Mobile Apps Hızlı Başlangıç]: app-service-mobile-cordova-get-started.md
[kimlik doğrulamayı kullanmaya başlama]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[Azure portalı]: https://portal.azure.com/
[JavaScript SDK'sı Azure Mobile Apps için]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
