---
title: "aaaAzure AD Node.js Başlarken | Microsoft Docs"
description: "Nasıl toobuild bir Node.js REST web API'si, kimlik doğrulaması için Azure AD ile tümleşir."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 512ae6de9acfde8b58c0447ab4a6b573fb6407c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a>Node.js için Web API ile çalışmaya başlama
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

*Passport*, Node.js için kimlik doğrulama ara yazılımıdır. Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan tooany Express tabanlı veya Restify web uygulamasına. Bir dizi kapsamlı strateji bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler. Microsoft Azure Active Directory için (Azure AD) bir strateji geliştirdik. Bu modülü yükleyin ve ardından hello Microsoft Azure Active Directory ekleyin `passport-azure-ad` eklentisi.

toodo bunu yapmanız:

1. Bir uygulamayı Azure AD'ye kaydedin.
2. Uygulama toouse Passport's ayarlamak `passport-azure-ad` eklentisi.
3. Bir istemci uygulama toocall hello tooDo listesi web API yapılandırın.

Bu öğretici için kod Hello korunduğu [github'da](https://github.com/Azure-Samples/active-directory-node-webapi).

> [!NOTE]
> Bu makalede nasıl tooimplement oturum açma kapsamıyordur, kaydolma, veya profil Yönetimi Azure AD B2C ile. Merhaba kullanıcının kimliği zaten doğrulanmış sonra web API'leri çağırmaya odaklanır.  İle başlamanızı öneririz [nasıl toointegrate Azure Active Directory belgeyle](active-directory-how-to-integrate.md) toolearn Azure Active Directory hello temelleri hakkında.
>
>

Tüm hello kaynak kodu github'da çalışan bu örneğin bir MIT lisansı altında yayımladık şekilde eşitleyerek ücretsiz tooclone (veya hatta daha iyi çatalı) ve geri bildirim sağlamak ve çekme istekleri.

## <a name="about-nodejs-modules"></a>Node.js modüllerini hakkında
Bu kılavuzda Node.js modüllerini kullanırız. Modüller, uygulamanız için belirli işlevler sağlayan yüklenebilir JavaScript paketlerdir. Modüller genellikle hello NPM yükleme dizininde hello Node.js NPM komut satırı aracını kullanarak yükleyin. Ancak, hello HTTP modülü gibi bazı modüller hello çekirdek Node.js paketinde dahil edilir.

Yüklü modülleri hello kaydedilir **node_modules** hello kökündeki Node.js yükleme dizininin dizin. Merhaba her modülünde **node_modules** directory tutar kendi **node_modules** bağımlı herhangi bir modül içeren dizini. Ayrıca, her gerekli modülüne sahip bir **node_modules** dizini. Bu özyinelemeli dizin yapısını hello bağımlılık zinciri temsil eder.

Bu bağımlılık zinciri yapı daha büyük bir uygulama yer sonuçlanır. Ancak, ayrıca tüm bağımlılıkları karşılanırsa ve geliştirme kullanılan hello sürümünün hello modüllerin de üretimde kullanılan güvence altına alır. Bu hello üretim uygulamanızın davranışını daha tahmin edilebilir hale getirir ve kullanıcıları etkileyebilecek sürüm oluşturma sorunları önler.

## <a name="step-1-register-an-azure-ad-tenant"></a>1. adım: Azure AD kiracısı kaydetme
toouse Bu örnek, Azure Active Directory kiracısı gerekir. Emin değilseniz, hangi bir kiracı veya nasıl tooget, bkz. [nasıl tooget bir Azure AD Kiracı](active-directory-howto-tenant.md).

## <a name="step-2-create-an-application"></a>2. adım: uygulama oluşturma
Sonraki toosecurely ihtiyaç duyduğu verir Azure AD bilgilerini uygulamanız ile iletişim kurması dizininizde bir uygulama oluşturun.  Merhaba istemci uygulaması ve web API tarafından tek bir temsil **uygulama kimliği** bu durumda, bir mantıksal uygulama içerdikleri için.  Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-how-applications-are-added.md). Bir satır iş kolu uygulaması geliştiriyorsanız [bu ek yönergeler yararlı olabilecek](../active-directory-applications-guiding-developers-for-lob-applications.md).

bir uygulama toocreate:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba üst menüsünde hesabınızı seçin. Ardından, hello altında **Directory** listesinde, uygulamanızın hello Active Directory Kiracı tooregister istediğiniz yeri seçin.

3. Merhaba soldaki Hello menüde seçin **daha Hizmetleri**ve ardından **Azure Active Directory**.

4. Seçin **uygulama kayıtlar**ve ardından **Ekle**.

5. Merhaba istemleri toocreate izleyin bir **Web uygulaması ve/veya Webapı**.

      * Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın açıklar.

      * Merhaba **oturum açma URL'si** , uygulamanızın hello temel URL'dir.  Merhaba hello örnek kod URL'sidir varsayılan `https://localhost:8080`.

6. Kaydettikten sonra Azure AD, uygulamanızın benzersiz bir uygulama kimliği atar Bu değer ihtiyacınız hello sonraki bölümlerde, bu nedenle hello uygulama sayfadan kopyalayın.

7. Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin. Merhaba **uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır. Merhaba kuraldır toouse `https://<tenant-domain>/<app-name>`, örneğin: `https://contoso.onmicrosoft.com/my-first-aad-app`.

8. Oluşturma bir **anahtar** hello uygulamanızdan için **ayarları** sayfasında ve bir yere kopyalayın. Kısa süre içinde gerekir.

## <a name="step-3-download-nodejs-for-your-platform"></a>3. adım: Platformunuz için Node.js indirme
Bu örnek toosuccessfully kullanın, Node.js çalışan yüklemesine sahip olmalıdır.

Adresinden node.js'yi yükleyin [http://nodejs.org](http://nodejs.org).

## <a name="step-4-install-mongodb-on-your-platform"></a>4. adım: Yükleme MongoDB, platformda
toosuccessfully kullanın Bu örnek, MongoDB çalışan yüklemesine sahip olmalıdır. Sunucu örneklerinde kalıcı REST API MongoDB toomake hello kullanın.

Adresinden [http://mongodb.org](http://www.mongodb.org).

> [!NOTE]
> Bu kılavuzda mongodb://localhost hello zaman bu yazma olduğu hello varsayılan yükleme ve sunucu uç noktalarını MongoDB için kullandığını kabul eder.
>
>

## <a name="step-5-install-hello-restify-modules-in-your-web-api"></a>5. adım: Merhaba Restify modüllerini web API'nize yükleme
Bizim REST API Restify toobuild kullanıyoruz. Restify, Express'ten türetilen minimal ve esnek Node.js uygulama çerçevesi. Connect üstünde REST API'leri oluşturmaya yönelik bir dizi sağlam özelliğe sahiptir.

### <a name="install-restify"></a>Restify'ı yükleme
1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** dizini. Merhaba, **azuread'i** directory olmayabilir, oluşturun.

        `cd azuread - or- mkdir azuread; cd azuread`

2. Merhaba aşağıdaki komutu yazın:

    `npm install restify`

    Bu komut Restify'ı yükler.

#### <a name="did-you-get-an-error"></a>Hata mı aldınız?
Bazı işletim sistemlerinde NPM kullandığınızda bildiren bir hata alabilirsiniz **hata: EPERM, chmod ' / usr/yerel/bin /..'** ve öneride çalışan hello hesabı yönetici olarak deneyin. Bu durum oluşursa, daha yüksek bir ayrıcalık düzeyinde hello sudo komutu toorun NPM kullanın.

#### <a name="did-you-get-an-error-regarding-dtrace"></a>DTRACE ilgili bir hata mı aldınız?
Restify'ı yüklerken şuna benzer bir hata görebilirsiniz:

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
Restify, DTrace kullanarak REST çağrılarını izlemek için güçlü bir mekanizma sağlar. Bununla birlikte, birçok işletim sistemi DTrace gerekmez. Bu hataları güvenle yoksayabilirsiniz.

Bu komutun çıktısı Hello benzer toohello çıktı aşağıdaki gibi görünmelidir:

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


## <a name="step-6-install-passportjs-in-your-web-api"></a>6. adım: Yükleme Passport.js, Web API
[Passport](http://passportjs.org/), Node.js için kimlik doğrulama ara yazılımıdır. Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan tooany Express tabanlı veya Restify web uygulamasına. Bir dizi kapsamlı strateji bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.

Azure Active Directory için bir strateji geliştirdik. Biz bu modülü yükleyin ve ardından hello Azure Active Directory stratejisi eklentisini ekleyin.

1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** dizini.

2. tooinstall passport.js hello aşağıdaki komutu girin:

    `npm install passport`

    Merhaba hello komutunun çıkışını benzer toohello aşağıdaki gibi görünmelidir:

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-tooyour-web-api"></a>7. adım: Passport Azure AD tooyour web API ekleme
Sonraki hello OAuth stratejisini kullanarak eklediğimiz `passport-azure-ad`, Azure Active Directory tooPassport bağlanmak stratejileri dizisi. Bu REST API'si örneğindeki taşıyıcı belirteçler için bu stratejiyi kullanın.

> [!NOTE]
> OAuth2 herhangi bir bilinen belirteç türünün verilebilir bir altyapı sağlasa da yalnızca belirli belirteç türleri yaygın olarak kullanılır. Taşıyıcı belirteçleri uç noktaları korumak için en yaygın olarak kullanılan hello belirteçleridir. Bunlar en yaygın olarak verilen hello OAuth2 belirteci türüdür. Birçok uygulama, taşıyıcı belirteçlerini hello türündeki tek düzenlenen belirteçlerin olduğunu varsayar.
>
>

Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** dizini.

Türü hello şu komutu tooinstall hello Passport.js `passport-azure-ad module`:

`npm install passport-azure-ad`

Merhaba hello komutunun çıkışını benzer toohello çıktı aşağıdaki gibi görünmelidir:


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



## <a name="step-8-add-mongodb-modules-tooyour-web-api"></a>8. adım: MongoDB modülleri tooyour web API ekleme
Bizim veri deposu olarak MongoDB kullanırız. Bu nedenle, tooinstall ihtiyacımız hello yaygın olarak kullanılan eklenti çağrılan Mongoose toomanage model ve şemaları. Ayrıca tooinstall hello veritabanı sürücüsünü (hangi MongoDB olarak da adlandırılır) MongoDB için ihtiyacımız var.

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a>9. adım: ek modülleri yükleme
Sonraki hello kalan gerekli modüllerini yükleyin.

1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.

    `cd azuread`

2. Bu modüllerdeki komutlar tooinstall aşağıdaki hello girin, **node_modules** dizini:

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a>10. adım: bağımlılıklarınız ile bir server.js oluşturma
Merhaba server.js dosyası hello işlevselliğinin bizim web API sunucunuz için sağlar. Bizim kod toothis dosyasını çoğunu ekleriz. Üretim amaçları doğrultusunda hello işlevselliği, ayrı yollar ve denetleyiciler gibi daha küçük dosyalar halinde yeniden düzenlemeniz öneririz. Bu gösteride, biz bu işlevsellik için server.js kullanın.

1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.

    `cd azuread`

2. Oluşturma bir `server.js` dosya, en sık kullandığınız düzenleyicide ve ardından aşağıdaki bilgilerle hello ekleyin:

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. Merhaba dosyasını kaydedin. Kısa süre içinde tooit getireceğiz.

## <a name="step-11-create-a-config-file-toostore-your-azure-ad-settings"></a>11. adım: Azure AD ayarlarınızı bir yapılandırma dosyası toostore oluşturma
Bu kod dosyası, Azure Active Directory portal tooPassport.js hello yapılandırma parametrelerini geçirir. Merhaba kılavuzun hello ilk bölümü hello web API toohello portal eklendiğinde bu yapılandırma değerlerini oluşturuldu. Merhaba kodu kopyaladıktan sonra biz hello değerleri bu parametre hangi tooput açıklanmaktadır.

1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.

    `cd azuread`

2. Oluşturma bir `config.js` dosya, en sık kullandığınız düzenleyicide ve ardından aşağıdaki bilgilerle hello ekleyin:

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in tooyour server unless you use hello common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in tooyour server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes toostderr in Unix.

         };
    ```
3. Merhaba dosyasını kaydedin.

## <a name="step-12-add-configuration-values-tooyour-serverjs-file"></a>12. adım: yapılandırma değerleri tooyour server.js dosyası ekleme
Tooread oluşturduğunuz hello .config dosyası bu değerleri arasında uygulamamız ihtiyacımız var. toodo bunu hello .config dosyası gerekli bir kaynak olarak bizim uygulamada ekleriz. Ardından hello genel değişkenler toomatch hello değişkenleri hello config.js belgede ayarlarız.

1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.

    `cd azuread`

2. Açık, `server.js` dosya, en sık kullandığınız düzenleyicide ve ardından aşağıdaki bilgilerle hello ekleyin:

    ```Javascript
    var config = require('./config');
    ```
3. Yeni bir bölüm çok eklemek`server.js` koddan hello ile:

    ```Javascript
    var options = {
        // hello URL of hello metadata document for your app. We will put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array toohold logged in users and hello current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If hello logging level is specified, switch tooit.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. Merhaba dosyasını kaydedin.

## <a name="step-13-add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a>13. adım: Mongoose kullanarak MongoDB Model ve şema bilgilerini hello Ekle
Şimdi bu hazırlık Biz bu üç dosyayı REST API hizmetinde birleştirmek gibi ödeme toostart geçiyor.

Bu kılavuz için 4. adımda açıklandığı gibi görevler MongoDB toostore kullanırız.

Merhaba, `config.js` dosya adım 11 oluşturduğumuz, biz Veritabanımıza adlı `tasklist`, biz hello sonuna eklediğiniz olduğu için bizim **mogoose_auth_local** bağlantı URL'si. Bu veritabanında önceden MongoDB toocreate gerekmez. Bunun yerine, MongoDB bu bize hello üzerinde ilk (Merhaba veritabanı önceden var olmayan varsayılarak) sunucu uygulamamız çalışma oluşturur.

Biz hello sunucu hangi MongoDB veritabanını söylediyse göre toouse isteriz, toowrite bazı ek kod toocreate hello model ve şema bizim sunucunun görevler için ihtiyacımız.

### <a name="discussion-of-hello-model"></a>Merhaba modelinin tartışma
Bizim şema modeli basit bir işlemdir. Size gereken şekilde genişletin.

ADI: toohello göreve atanan hello kişi hello adı. A **dize**.

: Hello görevi kendisi. A **dize**.

Tarihi: hello hello görev bitiş tarihidir. A **DATETIME**.

TAMAMLANAN: hello görev varsa veya tamamlanmış. A **BOOLEAN**.

### <a name="creating-hello-schema-in-hello-code"></a>Merhaba kodda Hello şema oluşturma
1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.

    `cd azuread`

2. Açık, `server.js` en sık kullandığınız düzenleyicide dosya ve bilgileri hello yapılandırma girdisi altına aşağıdaki hello ekleyin:

    ```Javascript
    // Connect tooMongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema toostore our tasks and users. It's a fairly simple schema for now.
    var TaskSchema = new Schema({
        owner: String,
        task: String,
        completed: Boolean,
        date: Date
    });

    // Use hello schema tooregister a model.
    mongoose.model('Task', TaskSchema);
    var Task = mongoose.model('Task');
    ```
Merhaba koddan anlayabilirsiniz gibi bizim şema ilk oluşturuyoruz. Biz verilerimizi hello boyunca biz tanımlarken kod toostore kullandığımız bir model nesnesi oluşturup bizim **yollar**.

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a>14. adım: bizim görev REST API sunucunuz için bizim yollar ekleme
Veritabanı modeli toowork ile sahibiz, bizim REST API sunucunuz için devam eden kullanım duyuyoruz hello yollar ekleyelim.

### <a name="about-routes-in-restify"></a>Restify'daki yollar hakkında
Yollar iş Restify hello aynı bunlar hello Express yığın yolu. Merhaba hello istemci uygulamaları toocall beklediğiniz URI kullanılarak yolları tanımlayın. Genellikle, yollarınızı ayrı bir dosyaya tanımlayın. Bizim amacıyla, biz hello server.js dosyasında bizim yollar yerleştirin. Üretim kullanımı için kendi dosyasına bu yollar faktörü öneririz.

Bir Restify yolu için genel bir desen aşağıdaki gibidir:

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep hello server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


Merhaba düzeni, en temel düzeyde budur. Restify (ve hızlı) uygulama türlerini tanımlama ve farklı uç noktalar arasında karmaşık yönlendirme sağlama gibi çok daha kapsamlı işlevsellik sağlar. Bizim amacıyla, biz Bu yolları basit tutuyor musunuz.

### <a name="add-default-routes-tooour-server"></a>Varsayılan yollar tooour sunucu ekleme
Biz şimdi hello temel CRUD yollarını oluşturma, alma, güncelleştirme, ekleme ve silme.

1. Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasörü:

    `cd azuread`

2. Açık hello `server.js` en sık kullandığınız düzenleyicide dosya ve bilgileri yaptığınız hello önceki veritabanı girişlerinin altına aşağıdaki hello ekleyin:

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it tooMongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.task = req.params.task;
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


// Delete a task by name.

function removeTask(req, res, next) {

    Task.remove({
        task: req.params.task,
        owner: owner
    }, function(err) {
        if (err) {
            req.log.warn(err,
                'removeTask: unable toodelete %s',
                req.params.task);
            next(err);
        } else {
            log.info('Deleted task:', req.params.task);
            res.send(204);
            next();
        }
    });
}

// Delete all tasks.

function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
}


// Get a specific task based on name.

function getTask(req, res, next) {

    log.info('getTask was called for: ', owner);
    Task.find({
        owner: owner
    }, function(err, data) {
        if (err) {
            req.log.warn(err, 'get: unable tooread %s', owner);
            next(err);
            return;
        }

        res.json(data);
    });

    return next();
}

/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you tooset default headers.
    // These headers comply with CORS and allow us toomongodbServer our response tooany origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in hello database. Did you initialize hello database as stated in hello README?");
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

### <a name="add-error-handling-in-our-apis"></a>Hata işleme bizim API'leri ekleme
```

///--- Errors for communicating something interesting back toohello client.

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


## <a name="step-15-create-your-server"></a>15. adım: sunucunuzu oluşturma
Veritabanımıza tanımlamış olduğunuz ve bizim yollar yerdir. Merhaba son şey toodo bizim çağrıları yönetir hello sunucuyu ekleyin.

Restify'ı (ve hızlı) çok sayıda REST API sunucunuz için özelleştirme yapabilirsiniz ancak biz bizim amacıyla toouse hello en temel kurulumu tekrar kalacaklarını.

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst too10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping tooREST.
```

## <a name="step-16-add-hello-routes-toohello-server-without-authentication-for-now"></a>16. adım: hello yollar toohello sunucu (olmadan kimlik doğrulaması için şimdi) Ekle
```Javascript
/// Now hello real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In hello pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need toomaintain session state. You can experiment with removing API protection
/* by removing hello passport.authenticate() method as follows:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler.
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser too%s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-hello-server-before-adding-oauth-support"></a>17. adım: (OAuth desteğini eklemeden önce) hello sunucu çalıştırma
Biz kimlik doğrulaması eklemeden önce sunucunuzu sınayın.

Merhaba en kolay yolu tootest, komut satırında curl kullanarak, sunucusudur. Bunu önce bize tooparse çıktıyı JSON olarak sağlayan bir yardımcı gerekiyor.

1. JSON aracını (örnek tüm Merhaba, bu aracı kullanmak) aşağıdaki hello yükleyin:

    `$npm install -g jsontool`

    Bu hello JSON aracını Global olarak yükler. Şimdi biz elde, hello sunucusuyla Yürüt:

2. Öncelikle, mongoDB örneğinizin çalıştığından emin olun:

    `$sudo mongod`

3. Ardından, toohello dizini değiştirin ve curling başlatın:

    `$ cd azuread` `$ node server.js`

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4. Ardından, biz bu şekilde bir görev ekleyebilirsiniz:

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    Merhaba yanıt şu şekilde olmalıdır:

        ```Shell
        HTTP/1.1 201 Created
        Connection: close
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Headers: X-Requested-With
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 5
        Date: Tue, 04 Feb 2014 01:02:26 GMT
        Hello
        ```
    Ve şu görevleri bu şekilde Brandon için listeleyebilirsiniz:

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

Tüm bu çalışırsa, hazır tooadd OAuth toohello REST API sunucusuna çalışıyoruz.

Bir REST API MongoDB sunucusuyla var!

## <a name="step-18-add-authentication-tooour-rest-api-server"></a>18. adım: kimlik doğrulaması tooour REST API sunucusuna ekleme
Çalışan bir REST API sahibiz, Azure AD ile yararlı hale getirme başlayalım.

Merhaba komut satırında, dizinleri toohello değiştirme **azuread'i** , zaten orada değilseniz klasör.

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a>Merhaba passport-azure-ad ile dahil edilen Oıdcbearerstrategy'yi kullanma
Şu ana kadar herhangi türde bir yetkilendirme olmadan genel bir REST TODO sunucusu oluşturduğumuz. Burada, bir araya getirilmesi Başlat budur.

1. İlk olarak, toouse Passport istiyoruz tooindicate gerekir. Bu hak, diğer sunucu yapılandırmanızın sonra koyun:

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > Ne zaman hello veri toosomething kullanıcı hello hello belirteçten benzersiz her zaman bağlantı öneririz API ' ları yazma taklit edilemez. Bu sunucu, Yapılacaklar öğelerini depoladığında, bunları hello nesne kimliği, biz hello "sahip" alanına yerleştirin hello kullanıcının hello belirteçteki (token.oid denir) göre depolar. Bu, yalnızca bu kullanıcının kendi TODOs erişebilmesini sağlar. Olmadığından hiçbir Etkilenme hello "sahip" API kimlikleri doğrulanır olsa bile bir dış kullanıcı hello diğer TODOs isteyebilir.                    

2. Sonraki birlikte hello taşıyıcı stratejisi kullanalım `passport-azure-ad`. Şu an için Hello koda bakın ve hello rest kısa süre içinde açıklayacağız. Bu, ne yukarıda yapıştırdığınız sonra koyun:

```Javascript
    /**
    /*
    /* Calling hello OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides hello need toomanage users and info tokens
    /* with a FindorCreate() method that must be provided by hello implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want toodo something smarter.
    **/

    var findById = function(id, fn) {
        for (var i = 0, len = users.length; i < len; i++) {
            var user = users[i];
            if (user.sub === id) {
                log.info('Found user: ', user);
                return fn(null, user);
            }
        }
        return fn(null, null);
    };


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying hello user');
            log.info(token, 'was hello token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

Passport, strateji yazarlarının hepsinin bağlı tüm kendi stratejileri (Twitter, Facebook vb.) için benzer bir desen kullanır. Merhaba stratejisi baktığınızda, biz bir belirteç ve bir Bitti'yi olan bir işlev hello parametreler olarak geçirin bakın. kendi iş yaptıktan sonra hello stratejisi geri toous gelir. Bunu yaptıktan sonra biz tooask için yeniden gerekmez şekilde hello kullanıcı ve hazırlama hello belirteci depolarız.

> [!IMPORTANT]
> Merhaba önceki kod tooauthenticate tooour server olur herhangi bir kullanıcı alır. Bu otomatik kaydı bilinir. Üretim sunucularında, herkesin bunları gerekmeden izin verme olduğunu öneririz karar kayıt işlemiyle gidin. Genellikle, Facebook ile tooregister ver, ancak ardından ek bilgi toofill isteyin tüketici uygulamalarında görürsünüz hello düzeni budur. Bu komut satırı programı olmasaydı, biz hello e-posta döndürülen ve ek bilgiler hello kullanıcı toofill sorulan hello belirteç nesnesi ayıklanan. Bu bir test sunucusu olduğundan, biz bunları toohello bellek içi veritabanına eklemeniz yeterlidir.
>
>

### <a name="protect-some-endpoints"></a>Bazı uç noktaları koruma
Merhaba belirterek uç noktaları koruma `passport.authenticate()` toouse istediğiniz çağrısı hello protokolü ile.

Bizim sunucu kodu yapmak bir şey daha fazla ilginç, toomake hello rota düzenlemenize olanak tanır.

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a>19. adım: sunucu uygulamanızı yeniden çalıştırın ve sizi reddettiğini olun
Kullanalım `curl` yeniden biz artık OAuth2 koruma bizim uç noktalarına karşı varsa toosee. Biz, herhangi bir istemci SDK Bu uç noktaya karşı çalıştırmadan önce bu test yapabilirsiniz. Merhaba döndürülen üstbilgileri yeterli tootell olmalıdır bize doğru yolu hello yapacağız durumunda.

1. Öncelikle, mongoDB örneğinizin çalıştığından emin olun:

    `$sudo mongod`

2. Ardından, toohello dizini değiştirin ve curling başlatın.

      `$ cd azuread` `$ node server.js`

3. Temel bir POST deneyin.

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

Bir 401 burada aradığınız hello yanıt ' dir. Bu yanıt hello Passport katman tooredirect toohello yetkili uç noktası, tam olarak ne olduğu çalışıyor gösterir.

## <a name="next-steps"></a>Sonraki adımlar
OAuth2 uyumlu bir istemci kullanmadan bu sunucu ile kadar gitti. Ek bir gözden geçirme aracılığıyla toogo gerekir.

Bir REST API kullanarak nasıl tooimplement Restify artık öğrendiğinize ve OAuth2. Ayrıca, hizmeti geliştirmek ve öğrenme birden fazla yeterli kod tookeep sahip nasıl toobuild Bu örnek üzerinde.

ADAL Yolculuğunuzun hello sonraki adımlarda ilgileniyorsanız, desteklenen bazı ADAL istemcileri ile çalışmaya devam öneririz aşağıda verilmiştir.

Tooyour Geliştirici makineyi kopyalama ve hello kılavuzda açıklandığı gibi yapılandırın.

[İOS için ADAL](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[Android için ADAL](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
