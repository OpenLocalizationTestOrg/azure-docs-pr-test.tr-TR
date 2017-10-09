---
title: "Azure AD B2C: Node.js kullanarak bir web API'sinin güvenliğini sağlama | Microsoft Belgeleri"
description: "Toobuild bir Node.js web nasıl API B2C kiracısından belirteç kabul eden"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a>Azure AD B2C: Node.js kullanarak bir web API'sinin güvenliğini sağlama
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

Azure Active Directory (Azure AD) B2C ile OAuth 2.0 erişim belirteçleri kullanarak web API'si güvenliğini sağlayabilirsiniz. Bu belirteçler Azure AD B2C tooauthenticate toohello API kullanan istemci uygulamalarınızın izin verir. Bu makalede nasıl toocreate bir "Yapılacaklar listesi" API kullanıcılar tooadd ve liste görevleri sağlayan gösterilmektedir. Merhaba web API'sini Azure AD B2C kullanarak güvenli ve kimliği doğrulanmış kullanıcılar toomanage kendi Yapılacaklar listesi yalnızca sağlar.

> [!NOTE]
> Bu örnek tooby bağlı toobe kullanılarak yazılmıştır bizim [iOS B2C örnek uygulamamızı](active-directory-b2c-devquickstarts-ios.md). Geçerli gözden geçirme ilk hello ve o örneği takip edin.
>
>

**Passport**, Node.js için kimlik doğrulama ara yazılımıdır. Esnek ve modüler özellikteki Passport, Express tabanlı veya Restify web uygulamasına sorunsuz bir şekilde yüklenebilir. Bir dizi kapsamlı strateji; bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler. Azure Active Directory (Azure AD) için bir strateji geliştirdik. Bu modülü yükleyin ve ardından hello Azure AD ekleyin `passport-azure-ad` eklentisi.

toodo Bu örnek, gerekir:

1. Bir uygulamayı Azure AD'ye kaydedin.
2. Uygulama toouse Passport's ayarlamak `azure-ad-passport` eklentisi.
3. İstemci uygulama toocall hello "Yapılacaklar listesi" web API'si yapılandırın.

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C dizini alma
Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.  Dizin; tüm kullanıcılar, uygulamalar, gruplar ve daha fazlası için bir kapsayıcıdır.  Henüz yoksa devam etmeden önce [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).

## <a name="create-an-application"></a>Uygulama oluşturma
Ardından B2C dizininizde Azure AD toosecurely gereken bazı bilgiler sağlayan bir uygulamanın iletişim toocreate uygulamanızla gerekir. Bu durumda, hem hello istemci uygulaması hem de web API'si tarafından tek bir temsil edilir **uygulama kimliği**, bir mantıksal uygulama içerdikleri için. Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md). Şunları yaptığınızdan emin olun:

* Dahil bir **web uygulaması/web API** hello uygulamada
* **Yanıt URL'si** olarak `http://localhost/TodoListService` adresini girin. Bu kod örneği için hello varsayılan URL değil.
* Uygulamanız için bir **Uygulama gizli anahtarı** oluşturun ve bunu kopyalayın. Bu veriler daha sonra gerekli olacaktır. Bu değer toobe gerektiğini Not [XML kaçışlı](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) kullanmadan önce.
* Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama. Bu veriler daha sonra gerekli olacaktır.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>İlkelerinizi oluşturma
Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır. Bu uygulama iki kimlik deneyimi içerir: kaydolma ve oturum açma. Bölümünde açıklandığı gibi her tür bir ilke toocreate gerek [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).  Üç ilkenizi oluştururken şunları yaptığınızdan emin olun:

* Merhaba seçin **görünen adı** ve diğer kaydolma özniteliklerini kaydolma ilkenizde.
* Merhaba seçin **görünen adı** ve **nesne kimliği** her ilkede uygulamanın talep.  Diğer talepleri de seçebilirsiniz.
* Merhaba basılı kopya **adı** oluşturduktan sonra her ilkenin. Merhaba önekine sahip olmalıdır `b2c_1_`.  Bu ilke adları daha sonra gerekli olacaktır.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Üç ilkenizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.

toolearn ile Merhaba ilkelerinin Azure AD B2C'de nasıl çalıştığı hakkında başlangıç [.NET web uygulamasıyla çalışmaya başlama Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="download-hello-code"></a>Merhaba kodu indirme
Bu öğretici için kod Hello [Github'da korunur](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS). toobuild hello örnek olarak, Git, yapabilecekleriniz [çatı projesini .zip dosyası olarak indirebilirsiniz](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip). Ayrıca hello çatıyı kopyalayabilirsiniz:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

Tamamlanan hello uygulamadır de [.zip dosyası olarak kullanılabilir](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) veya hello `complete` hello dalı aynı deposu.

## <a name="download-nodejs-for-your-platform"></a>Platformunuz için Node.js indirme
Bu örnek toosuccessfully kullanın, Node.js çalışan yüklemesine gerekir.

[nodejs.org](http://nodejs.org) adresinden Node.js'yi yükleyin.

## <a name="install-mongodb-for-your-platform"></a>Platformunuz için MongoDB yükleme
toosuccessfully kullanın Bu örnek, MongoDB çalışan yüklemesine gerekir. MongoDB toomake kalıcı, REST API'nizi sunucu örneklerinde kullanırız.

[mongodb.org](http://www.mongodb.org) adresinden MongoDB'yi yükleyin.

> [!NOTE]
> Bu kılavuz hello varsayılan yükleme ve sunucu uç noktaları olan bu yazma hello zamanında MongoDB kullanmak varsayar `mongodb://localhost`.
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a>Merhaba Restify modüllerini web API'nize yükleme
REST API'nizi Restify toobuild kullanırız. Restify, Express'ten türetilen minimal ve esnek bir Node.js uygulama çerçevesidir. Connect üstünde REST API'leri oluşturmaya yönelik bir dizi sağlam özelliğe sahiptir.

### <a name="install-restify"></a>Restify'ı yükleme
Merhaba komut satırından dizininizi çok değiştirin`azuread`. Merhaba, `azuread` dizin mevcut değil, oluşturun.

`cd azuread` veya `mkdir azuread;`

Merhaba aşağıdaki komutu girin:

`npm install restify`

Bu komut Restify'ı yükler.

#### <a name="did-you-get-an-error"></a>Hata mı aldınız?
Bazı işletim sistemlerindeki kullandığınızda, `npm`, hello hata iletisini alabilirsiniz `Error: EPERM, chmod '/usr/local/bin/..'` ve bir istek hello hesabı yönetici olarak çalıştırın. Bu sorun oluşursa, hello kullan `sudo` komutu toorun `npm` daha yüksek bir ayrıcalık düzeyinde.

#### <a name="did-you-get-a-dtrace-error"></a>Bir DTrace hatası mı aldınız?
Restify'ı yüklediğinizde şöyle bir metin görebilirsiniz:

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```

Restify, DTrace kullanarak REST çağrılarını izlemek için güçlü bir mekanizma sağlar. Ancak çoğu işletim sisteminde DTrace kullanılabilir değildir. Bu hataları güvenle yoksayabilirsiniz.

Merhaba hello komutunun çıkışını benzer toothis metin görünmelidir:

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)

## <a name="install-passport-in-your-web-api"></a>Passport'u web API'nize yükleme
Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa.

Passport komutu aşağıdaki hello kullanarak yükleyin:

`npm install passport`

Merhaba hello komutunun çıkışını benzer toothis metin olmalıdır:

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a>Passport-azuread'i tooyour web API ekleme
Ardından, kullanarak hello OAuth stratejisini ekleyin `passport-azuread`, Azure AD'yi Passport'a bağlayan stratejileri dizisi. Merhaba REST API'si örneğindeki taşıyıcı belirteçler için bu stratejiyi kullanın.

> [!NOTE]
> OAuth2, herhangi bir bilinen belirteç türünün verilebileceği bir altyapı sağlasa da yalnızca belirli belirteç türleri yaygın kullanım elde etmiştir. uç noktaları korumaya hello belirteçler, taşıyıcı belirteçlerdir. Bu belirteçler OAuth2 en yaygın olarak verilen hello türleridir. Birçok uygulama, taşıyıcı belirteçlerini hello tek belirteç türü olduğunu varsayar.
>
>

Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa.

Merhaba Passport yüklemek `passport-azure-ad` komutu aşağıdaki hello kullanarak Modülü:

`npm install passport-azure-ad`

Merhaba hello komutunun çıkışını benzer toothis metin olmalıdır:

``
passport-azure-ad@1.0.0 node_modules/passport-azure-ad
├── xtend@4.0.0
├── xmldom@0.1.19
├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
├── underscore@1.8.3
├── async@1.3.0
├── jsonwebtoken@5.0.2
├── xml-crypto@0.5.27 (xpath.js@1.0.6)
├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
└── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
``

## <a name="add-mongodb-modules-tooyour-web-api"></a>MongoDB modülleri tooyour web API ekleme
Bu örnekte MongoDB veri deponuz olarak kullanılır. Bunun için modelleri ve şemaları yönetmeye yönelik yaygın kullanılan bir eklenti olan Mongoose’u yükleyin.

* `npm install mongoose`

## <a name="install-additional-modules"></a>Ek modüller yükleme
Ardından, kalan gerekli modüllerini hello yükleyin.

Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:

`cd azuread`

Merhaba modüllerini yüklemek, `node_modules` dizini:

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a>Bağımlılıklarınız ile bir server.js dosyası oluşturma
Merhaba `server.js` dosyası, Web API sunucunuz için hello işlevselliği hello çoğunu sağlar.

Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:

`cd azuread`

Bir düzenleyicide `server.js` dosyası oluşturun. Aşağıdaki bilgilerle hello ekleyin:

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

Merhaba dosyasını kaydedin. Tooit daha sonra geri dönün.

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a>Azure AD ayarlarınızı bir config.js dosyası toostore oluşturma
Bu kod dosyası, Azure AD portalı toohello hello yapılandırma parametrelerini geçirir `Passport.js` dosya. Merhaba ilk hello gözden geçirme bölümünde hello web API toohello portal eklendiğinde bu yapılandırma değerlerini oluşturuldu. Merhaba kodu kopyaladıktan sonra biz hello değerleri bu parametre hangi tooput açıklanmaktadır.

Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:

`cd azuread`

Bir düzenleyicide `config.js` dosyası oluşturun. Aşağıdaki bilgilerle hello ekleyin:

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a>Gerekli değerler
`clientID`: Merhaba Web API uygulamanızın istemci kimliği.

`IdentityMetadata`: Bu yerdir `passport-azure-ad` hello kimlik sağlayıcısı için yapılandırma verilerinizi arar. Ayrıca, hello anahtarları toovalidate hello JSON web belirteçlerini için arar.

`audience`: Merhaba, çağıran uygulama tanımlayan hello portalından Tekdüzen Kaynak Tanımlayıcısı (URI).

`tenantName`: Kiracı adınız (örneğin, **contoso.onmicrosoft.com**).

`policyName`: Merhaba tooyour Server'da gelen toovalidate hello belirteçleri istediğiniz ilke. Bu ilke olmalıdır hello hello istemci uygulaması oturum açmak için kullandığınız aynı ilke.

> [!NOTE]
> Şimdilik, kullanım hello aynı istemci ve sunucu kurulumunda arasında ilkeleri. Zaten bir gözden geçirme tamamlandı ve bu ilkeleri oluşturduysanız, bu nedenle yeniden toodo gerekmez. Merhaba Kılavuzu tamamladığınız hello sitede istemci kılavuzlarına yönelik yeni ilkeleri tooset gerek döndürmemelidir.
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a>Yapılandırma tooyour server.js dosyası ekleme
Merhaba tooread hello değerleri `config.js` oluşturduğunuz dosya, hello eklemek `.config` dosya uygulamanızda gerekli bir kaynak olarak ve ardından hello hello genel değişkenler toothose `config.js` belge.

Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:

`cd azuread`

Açık hello `server.js` dosyasına bir düzenleyicide. Aşağıdaki bilgilerle hello ekleyin:

```Javascript
var config = require('./config');
```
Yeni bir bölüm çok eklemek`server.js` koddan hello içerir:

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

Ardından, arama bizim uygulamalardan aldığımız hello kullanıcılar için bazı yer tutucuları ekleyelim.

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

Devam edip günlükçümüzü de oluşturalım.

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>Mongoose kullanarak Hello MongoDB model ve şema bilgilerini ekleme
Bu üç dosyayı REST API hizmetinde araya getirdiğiniz hello erken hazırlık ödeyen devre dışı.

Bu kılavuz, MongoDB toostore daha önce bahsedildiği gibi görevlerinizin kullanın.

Merhaba, `config.js` dosyası, veritabanınızı adlı **tasklist**. Bu ayrıca hello hello sonuna eklediğiniz adlandırılmıştı `mongoose_auth_local` bağlantı URL'si. Bu veritabanında önceden MongoDB toocreate gerekmez. Merhaba veritabanı sizin için hello ilk sunucu uygulamanızı çalıştırılmasında oluşturur.

Hangi MongoDB veritabanı toouse hello sunucusuna bildirmek sonra toowrite bazı ek kod toocreate hello model ve şema sunucu görevleriniz için gerekir.

### <a name="expand-hello-model"></a>Merhaba modeli genişletme
Bu şema modeli basittir. Gerektiği şekilde genişletebilirsiniz.

`owner`: Göreve toohello görev atanır. Bu nesne bir **string**.  

`Text`: hello görevin kendisi. Bu nesne bir **string**.

`date`: Başlangıç tarihi bu hello son bir görevdir. Bu nesne bir **datetime**.

`completed`: Başlangıç görevi ise tamamlayın. Bu nesne bir **Boolean**.

### <a name="create-hello-schema-in-hello-code"></a>Merhaba kodda Hello şema oluşturun
Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:

`cd azuread`

Açık hello `server.js` dosyasına bir düzenleyicide. Hello aşağıdaki bilgilerle hello yapılandırma girdisi altına ekleyin:

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
İlk hello şema oluşturun ve ardından hello genelindeki verilerinizi tanımlarken kod toostore kullanan bir model nesnesi oluşturun, **yollar**.

## <a name="add-routes-for-your-rest-api-task-server"></a>REST API görev sunucunuz için yollar ekleme
Veritabanı modeli toowork ile sahip olduğunuza göre REST API sunucunuz için kullandığınız hello yolları ekleyin.

### <a name="about-routes-in-restify"></a>Restify'daki yollar hakkında
Yollar iş Restify'da hello aynı hello Express yığınını kullandıklarında çalıştıkları şekilde. Merhaba hello istemci uygulamaları toocall beklediğiniz URI kullanılarak yolları tanımlayın.

Bir Restify yolu için genel bir desen:

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

Restify ve Express, uygulama türlerini tanımlama ve farklı uç noktalar arasında karmaşık yönlendirme yapma gibi çok daha kapsamlı işlevsellik sağlayabilir. Bu öğreticinin Hello amaçları doğrultusunda, biz Bu yolları basit tutun.

#### <a name="add-default-routes-tooyour-server"></a>Varsayılan yollar tooyour sunucu ekleme
Şimdi hello temel CRUD yollarını ekleyin **oluşturma** ve **listesi** bizim REST API için. Diğer yollar hello bulunabilir `complete` hello örnek dalı.

Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:

`cd azuread`

Açık hello `server.js` dosyasına bir düzenleyicide. Merhaba veritabanı girişlerinin aşağıdaki bilgilerle hello yukarıdaki Ekle yaptığınız:

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Add one!");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}
```


#### <a name="add-error-handling-for-hello-routes"></a>Merhaba yollar için hata işleme ekleme
Anlayabileceği bir şekilde geri toohello istemci karşılaştığınız sorunları iletişim kurabilmesi için bazı hata işleme ekleyin.

Hello aşağıdaki kodu ekleyin:

```Javascript
///--- Errors for communicating something interesting back toohello client
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="create-your-server"></a>Sunucunuzu oluşturma
Artık veritabanınızı tanımladınız ve yollarınızı yerleştirdiniz. Merhaba son, toodo için çağrılarınızı yönetmediğinden tooadd hello sunucu örneği şeydir.

Restify ve Express REST API sunucunuz için kapsamlı özelleştirme sağlar ancak burada kullandığımız hello en temel kurulumu.

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a>Merhaba yollar toohello sunucu (kimlik doğrulaması olmadan) ekleme
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a>Kimlik doğrulama tooyour REST API sunucusu ekleme
Artık çalışan bir REST API sunucunuz olduğuna göre bunu Azure AD için faydalı hale getirebilirsiniz.

Merhaba komut satırından dizininizi çok değiştirin`azuread`, zaten yoksa:

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Merhaba passport-azure-ad ile dahil edilen Oıdcbearerstrategy'yi kullanma
> [!TIP]
> Ne zaman hello veri toosomething kullanıcı hello hello belirteçten benzersiz her zaman bağlanması gereken API ' ları yazma taklit edilemez. Merhaba sunucu Yapılacaklar öğelerini depoladığında hello böylece göre mu **OID** hangi hello "sahip" alanına hello kullanıcının hello belirteçteki (token.oid denir). Bu değer kendi ToDo öğesine yalnızca bu kullanıcının erişmesini sağlar. Olmadığından hiçbir Etkilenme hello "sahip" API bir dış kullanıcı kimlikleri doğrulanır olsa bile başkalarının Yapılacaklar öğelerini isteyebilir.
>
>

Ardından, birlikte hello taşıyıcı stratejisi kullanın `passport-azure-ad`.

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

Passport, tüm stratejileri hello aynı desen kullanır. Bu desene, parametre olarak `token` ve `done` öğelerini barındıran bir `function()` geçirirsiniz. tüm işlemlerini tamamladıktan sonra hello stratejisi tooyou gelir. Ardından hello kullanıcı depolamak ve gerekir hello belirteci kaydetmek için yeniden tooask gerekmez.

> [!IMPORTANT]
> Yukarıdaki Hello kod tooauthenticate tooyour server olur herhangi bir kullanıcı alır. Bu işlem otomatik kayıt olarak bilinir. Üretim sunucularında, bunları bir kayıt sürecinden geçerler gerekmeden tüm kullanıcılara erişim hello API izin vermeyin. Bu genellikle, Facebook kullanarak tooregister izin ver, ancak ardından ek bilgi toofill isteyin tüketici uygulamalarında görürsünüz hello düzeni işlemidir. Bu programın komut satırı programı olmasaydı, biz hello e-posta döndürülen ve ek bilgiler kullanıcıların toofill sorulan hello belirteç nesnesi ayıklanan. Bu bir örnek olduğundan, bunları tooan bellek içi veritabanına ekleriz.
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a>Sunucu uygulaması tooverify çalıştırmak, BT'nin sizi reddettiğini
Kullanabileceğiniz `curl` artık uç noktalarınızda OAuth2 koruması varsa toosee. Merhaba döndürülen üstbilgileri yeterli tootell olmalıdır hello doğru yolda olduğunu.

MongoDB örneğinizin çalıştığından emin olun:

    $sudo mongodb

Toohello dizin ve çalışma hello sunucu değiştirin:

    $ cd azuread
    $ node server.js

Yeni bir terminal penceresinde şunu çalıştırın: `curl`

Temel bir POST deneyin:

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

Merhaba yanıt istediğiniz bir 401 hatasıdır. Merhaba Passport katman tooredirect çalışıyor gösterir toohello kimlik doğrulama uç noktası.

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a>Artık OAuth2 kullanan bir REST API'niz var
Restify ve OAuth kullanarak bir REST API’si uyguladık! Böylece hizmetinizi toodevelop devam ve bu örneği temel yapı artık gerekli koda sahip. OAuth2 uyumlu bir istemci kullanmadan bu sunucu ile çalışabildiğiniz kadar çalıştınız. İlave bir kılavuz gibi bir sonraki adımda kullanmak bizim [tooa web API B2C ile iOS kullanarak bağlanmak](active-directory-b2c-devquickstarts-ios.md) gözden geçirme.

## <a name="next-steps"></a>Sonraki adımlar
Gelişmiş toomore konuları gibi geçebilirsiniz:

[Tooa web API B2C ile iOS kullanarak bağlanma](active-directory-b2c-devquickstarts-ios.md)
