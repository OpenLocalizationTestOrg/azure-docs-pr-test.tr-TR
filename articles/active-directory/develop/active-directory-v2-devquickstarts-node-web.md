---
title: "Node.js web uygulaması oturum açma aaaAzure Active Directory v2.0 | Microsoft Docs"
description: "Nasıl toobuild bir Node.js web kişisel bir Microsoft hesabı ve bir iş veya Okul hesabı kullanarak bir kullanıcı oturum açtığında uygulama hakkında bilgi edinin."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 05/13/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f8ce6e2b841c215cb14e82bcf444fe849634cc88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-nodejs-web-app"></a>Oturum açma tooa Node.js web uygulaması Ekle

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası ile çalışır. mı hello v2.0 uç noktası veya hello v1.0 uç noktası, kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 

Bu öğreticide, görevleri aşağıdaki Passport toodo hello kullanın:

* Bir web uygulamasında hello kullanıcının Azure Active Directory (Azure AD) kullanarak oturum açın ve v2.0 uç hello.
* Merhaba kullanıcı hakkındaki bilgileri görüntüler.
* Oturum, kullanıcı hello uygulama dışında hello.

**Passport**, Node.js için kimlik doğrulama ara yazılımıdır. Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan hiçbir Express tabanlı veya restify web uygulamasına. Passport, bir dizi kapsamlı strateji kimlik doğrulamasını bir kullanıcı adı ve parola, Facebook, Twitter veya diğer seçenekleri kullanarak destekler. Azure AD için bir strateji geliştirdik. Bu makalede, nasıl tooinstall hello modülü ve ardından hello Azure AD ekleyin gösteriyoruz `passport-azure-ad` eklentisi.

## <a name="download"></a>İndir
Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs). yapabilecekleriniz toofollow hello öğretici, [hello uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) veya kopya hello çatıyı:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Bu öğretici hello sonunda tamamlanmış Merhaba uygulaması da alabilirsiniz.

## <a name="1-register-an-app"></a>1: bir uygulamayı Kaydet
En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya izleyin [bu adımları ayrıntılı](active-directory-v2-app-registration.md) tooregister bir uygulama. Emin olun:

* Kopya hello **uygulama kimliği** tooyour uygulama atanmış. Bu öğretici için ihtiyacınız.
* Merhaba eklemek **Web** uygulamanız için platform.
* Kopya hello **yeniden yönlendirme URI'si** hello portalından. Merhaba varsayılan URI değeri kullanmalısınız `urn:ietf:wg:oauth:2.0:oob`.

## <a name="2-add-prerequisities-tooyour-directory"></a>2: ön koşullar tooyour Dizin Ekle
Zaten yoksa bir komut isteminde dizinleri toogo tooyour kök klasörü değiştirin. Merhaba aşağıdaki komutları çalıştırın:

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`

Ayrıca, kullandığımız `passport-azure-ad` hello hızlı başlangıç çatısında önizlememiz hello içinde:

* `npm install passport-azure-ad`

Bu hello kitaplıkları yükler, `passport-azure-ad` kullanır.

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3: uygulama toouse hello passport düğümü js stratejinizi ayarlayın
Merhaba Express ara yazılım toouse hello Openıd Connect kimlik doğrulama protokolü olarak ayarlayın. Passport tooissue oturum açma ve oturum kapatma isteklerini kullanın, hello kullanıcının oturumunu yönetmek ve başka şeylerin hello kullanıcı hakkında bilgi alın.

1.  Merhaba proje Hello kökte hello Config.js dosyasını açın. Merhaba, `exports.creds` bölümünde, uygulamanızın yapılandırma değerlerini girin.
  
  * `clientID`: Merhaba **uygulama kimliği** hello Azure portal atanan tooyour uygulamada olmasıdır.
  * `returnURL`: Merhaba **yeniden yönlendirme URI'si** hello portalda girdiğiniz.
  * `clientSecret`: hello Portalı'nda oluşturulan hello gizli anahtarı.

2.  Merhaba proje Hello kökte hello App.js dosyasını açın. ile birlikte tooinvoke hello OIDCStrategy stratey `passport-azure-ad`, çağrı aşağıdaki hello ekleyin:

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  toohandle, oturum açma istekleri, yalnızca başvurulan hello stratejisi kullanın:

  ```JavaScript
  // Use hello OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. hello function accepts
  //   credentials (in this case, an OpenID identifier), and invokes a callback
  //   with a user object.
  passport.use( new OIDCStrategy({
      callbackURL: config.creds.returnURL,
      realm: config.creds.realm,
      clientID: config.creds.clientID,
      clientSecret: config.creds.clientSecret,
      oidcIssuer: config.creds.issuer,
      identityMetadata: config.creds.identityMetadata,
      responseType: config.creds.responseType,
      responseMode: config.creds.responseMode,
      skipUserProfile: config.creds.skipUserProfile
      scope: config.creds.scope
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
      log.info('Example: Email address we received was: ', profile.email);
      // Asynchronous verification, for effect...
      process.nextTick(function () {
        findByEmail(profile.email, function(err, user) {
          if (err) {
            return done(err);
          }
          if (!user) {
            // "Auto-registration"
            users.push(profile);
            return done(null, profile);
          }
          return done(null, user);
        });
      });
    }
  ));
  ```

Passport, tüm kendi stratejileri (Twitter, Facebook vb.) benzer bir desen kullanır. Tüm strateji yazıcıları toohello düzeni uyması. Merhaba stratejisi geçirmek bir `function()` bir belirteç kullanan ve `done` parametre olarak. tüm iş yaptıktan sonra hello stratejisi döndürülür. İçin yeniden tooask gerekmeyen şekilde hello kullanıcı ve hazırlama hello belirtecini depolar.

  > [!IMPORTANT]
  > Merhaba önceki kod tooyour sunucu kimliğini doğrulayabilir herhangi bir kullanıcı alır. Bu otomatik kaydı bilinir. Bir üretim sunucusunda toolet herkes bunları seçtiğiniz bir kayıt sürecinden geçerler gerekmeden istediğiniz olmayacaktır. Bu genellikle tüketici uygulamalarında görürsünüz hello düzeni olur. Merhaba uygulama Facebook ile tooregister sağlayabilir, ancak tooenter ek bilgiler, ister. Bu öğretici için bir komut satırı programı doğru kullanıyorsanız, döndürülen hello belirteç nesnesinden hello e-posta ayıklanamıyor. Ardından, hello kullanıcı tooenter ek bilgileri isteyebilir. Bu bir test sunucusu olduğundan, hello kullanıcı ekleme doğrudan toohello bellek içi veritabanı.
  > 
  > 

4.  Oturum açtığınız kullanıcı tookeep izleme kullanmak hello yöntemleri ekleyin Passport'un gerektirdiği gibi. Bu seri hale getirme ve seri durumdan hello kullanıcının bilgileri içerir:

  ```JavaScript

  // Passport session setup (section 2)

  //   toosupport persistent login sessions, Passport needs toobe able to
  //   serialize users into, and deserialize users out of, hello session. Typically,
  //   this is as simple as storing hello user ID when serializing, and finding
  //   hello user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array toohold signed-in users
  var users = [];

  var findByEmail = function(email, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
      var user = users[i];
      log.info('we are using user: ', user);
      if (user.email === email) {
        return fn(null, user);
      }
    }
    return fn(null, null);
  };
  ```

5.  Merhaba Express altyapısını yükler hello kodu ekleyin. Merhaba varsayılan /views kullanın ve Express /routes desen sağlar:

  ```JavaScript

  // Set up Express (section 2)

  var app = express();

  app.configure(function() {
    app.set('views', __dirname + '/views');
    app.set('view engine', 'ejs');
    app.use(express.logger());
    app.use(express.methodOverride());
    app.use(cookieParser());
    app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
    app.use(bodyParser.urlencoded({ extended : true }));
    // Initialize Passport!  Also use passport.session() middleware, toosupport
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  Merhaba POST yönlendirir o elde hello gerçek oturum açma isteklerini toohello kapalı eklemek `passport-azure-ad` altyapısı:

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. hello first step in OpenID authentication involves redirecting
  //   hello user toohello user's OpenID provider. After authenticating, hello OpenID
  //   provider redirects hello user back toothis application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in hello sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called.
  //   In this example, it redirects hello user toohello home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware tooauthenticate the
  //   request. If authentication fails, hello user is redirected back toothe
  //   sign-in page. Otherwise, hello primary route function is called. 
  //   In this example, it redirects hello user toohello home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4: kullanım Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD
Uygulamanızı şimdi hello v2.0 uç noktası ile toocommunicate yukarı hello Openıd Connect kimlik doğrulama protokolü kullanarak ayarlanır. Merhaba `passport-azure-ad` stratejisi, kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve hello kullanıcı oturumunu sürdürme hello ayrıntılarını mvc'deki. Toodo sol tüm kullanıcılarınız toogive olan bir şekilde toosign ve oturum out ve toogather açık olan hello kullanıcı hakkında daha fazla bilgi.

1.  Merhaba eklemek **varsayılan**, **oturum açma**, **hesap**, ve **oturum kapatma** yöntemleri tooyour App.js dosyası:

  ```JavaScript

  //Routes (section 4)

  app.get('/', function(req, res){
    res.render('index', { user: req.user });
  });

  app.get('/account', ensureAuthenticated, function(req, res){
    res.render('account', { user: req.user });
  });

  app.get('/login',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Login was called in hello sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  Merhaba ayrıntıları aşağıdadır:
    
    * Merhaba `/` rota toohello index.ejs görünümü yeniden yönlendirir. (Varsa) hello istekte hello kullanıcı geçirir.
    * Merhaba `/account` ilk yol *, kimlik doğrulaması yapmasını sağlar* (Bu koddan hello uygulamanız). Ardından, hello istekte hello kullanıcı geçirir. Merhaba kullanıcı hakkında daha fazla bilgi sınıflandırıp budur.
    * Merhaba `/login` rota çağrıları, `azuread-openidconnect` doğrulayıcıdan `passport-azuread`. Başarılı değil, hello kullanıcı geri çok yeniden`/login`.
    * Merhaba `/logout` hello logout.ejs görüntüleyin (ve rota) yol çağırır. Bu tanımlama bilgilerini temizler ve ardından kullanıcı geri tooindex.ejs döndürür hello.

2.  Merhaba eklemek **EnsureAuthenticated** daha önce kullanılan yöntem `/account`:

  ```JavaScript

  // Route middleware tooensure hello user is authenticated (section 4)

  //   Use this route middleware on any resource that needs toobe protected. If
  //   hello request is authenticated (typically via a persistent login session),
  //   hello request proceeds. Otherwise, hello user is redirected toothe
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  App.js içinde hello sunucusu oluştur:

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a>5: hello Web sitesinde kullanıcı Göster Express'te hello görünümleri ve yollar oluşturma
Merhaba yollar ve bilgi toohello kullanıcı Göster görünümleri ekleyin. Merhaba yolları ve görünümleri de hello işlemek `/logout` ve `/login` oluşturduğunuz yollar.

1. Merhaba Hello kök dizininde oluşturmak `/routes/index.js` rota.

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  Merhaba Hello kök dizininde oluşturmak `/routes/user.js` rota.

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  `/routes/index.js`ve `/routes/user.js` isteği tooyour görünümlerini hello kullanıcı gibi hello geçirmek basit yollar.

3.  Merhaba Hello kök dizininde oluşturmak `/views/index.ejs` görünümü. Bu sayfa çağrıları, **oturum açma** ve **oturum kapatma** yöntemleri. Merhaba de `/views/index.ejs` toocapture hesap bilgileri görüntüleyin. Merhaba koşullu kullanabilirsiniz `if (!user)` aracılığıyla hello istekte geçirilen hello kullanıcı olarak. Bu bulgu açtığınız kullanıcı sahip olur.

  ```JavaScript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
      <h2>Hello, <%= user.displayName %>.</h2>
      <a href="/account">Account info</a></br>
      <a href="/logout">Sign out</a>
  <% } %>
  ```

4.  Merhaba Hello kök dizininde oluşturmak `/views/account.ejs` görünümü. Merhaba `/views/account.ejs` görünümü tooview ek bilgiler sağlar, `passport-azuread` hello kullanıcı istekte koyar.

  ```Javascript
  <% if (!user) { %>
      <h2>Welcome! Please sign in.</h2>
      <a href="/login">Sign in</a>
  <% } else { %>
  <p>displayName: <%= user.displayName %></p>
  <p>givenName: <%= user.name.givenName %></p>
  <p>familyName: <%= user.name.familyName %></p>
  <p>UPN: <%= user._json.upn %></p>
  <p>Profile ID: <%= user.id %></p>
  <p>Full Claimes</p>
  <%- JSON.stringify(user) %>
  <p></p>
  <a href="/logout">Sign out</a>
  <% } %>
  ```

5.  Bir düzen ekleyin. Merhaba Hello kök dizininde oluşturmak `/views/layout.ejs` görünümü.

  ```HTML

  <!DOCTYPE html>
  <html>
      <head>
          <title>Passport-OpenID Example</title>
      </head>
      <body>
          <% if (!user) { %>
              <p>
              <a href="/">Home</a> |
              <a href="/login">Sign in</a>
              </p>
          <% } else { %>
              <p>
              <a href="/">Home</a> |
              <a href="/account">Account</a> |
              <a href="/logout">Sign out</a>
              </p>
          <% } %>
          <%- body %>
      </body>
  </html>
  ```

6.  toobuild, uygulamanızı ve çalıştırma Çalıştır `node app.js`. Ardından, çok Git`http://localhost:3000`.

7.  Kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın. Merhaba kullanıcının kimliğini hello ApplicationTier/account listesinde yansıtılır unutmayın. 

Endüstri standardı protokoller kullanılarak güvenli bir web uygulaması şimdi sahipsiniz. Kişisel ve iş veya Okul hesaplarını kullanarak uygulamanızı kullanıcıların kimliklerini doğrulayabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Başvuru için tamamlandı hello örnek (yapılandırma değerleriniz olmadan) olarak sağlanan [bir .zip dosyası](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip). Aynı zamanda Github'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

Ardından, Gelişmiş konular toomore üzerinde taşıyabilirsiniz. Tootry isteyebilirsiniz:

[Node.js web API'si hello v2.0 uç kullanarak güvenli hale getirme](active-directory-v2-devquickstarts-node-api.md)

Bazı ek kaynaklar aşağıda verilmiştir:

* [Azure AD v2.0 Geliştirici Kılavuzu](active-directory-appmodel-v2-overview.md)
* [Yığın taşması "azure-active-directory" etiketi](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a>Ürünlerimiz için güvenlik güncelleştirmelerini alma
Güvenlik olayları olduğunda bildirim toobe yukarı toosign öneririz. Merhaba üzerinde [Microsoft Teknik Güvenlik bildirimleri](https://technet.microsoft.com/security/dd252948) sayfasında, tooSecurity danışma uyarıları abone olun.

