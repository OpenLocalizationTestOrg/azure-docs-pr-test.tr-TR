---
title: "Azure AD oturum açma ile başlatılan ve oturum kapatma Node.js kullanarak aaaGetting | Microsoft Docs"
description: "Nasıl toobuild bir Node.js Express MVC web oturum açma için Azure AD ile tümleşen uygulama hakkında bilgi edinin."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 26481899c74741743b947bd891b65ff24ffc43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a>Node.js web uygulamasına oturum açma ve Azure AD ile oturum kapatma
Burada Passport kullanın:

* Oturum toohello uygulama Azure Active Directory'ye (Azure AD) kullanıcı hello.
* Merhaba kullanıcı hakkındaki bilgileri görüntüler.
* Oturum, kullanıcı hello uygulama dışında hello.

Passport Node.js için kimlik doğrulama Ara yazılımıdır. Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan tooany Express tabanlı veya restify web uygulamasına. Bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlasını kullanan kimlik doğrulama stratejileri kapsamlı bir kümesini destekler. Microsoft Azure Active Directory için bir strateji geliştirdik. Bu modülü yükleyin ve ardından hello Microsoft Azure Active Directory ekleyin `passport-azure-ad` eklentisi.

toodo adımları izleyerek bu, Al hello:

1. Bir uygulamayı kaydedin.
2. Uygulama toouse hello ayarlamak `passport-azure-ad` stratejisi.
3. Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın.
4. Merhaba kullanıcı hakkındaki verileri yazdırın.

Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).  yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) veya kopya hello çatıyı:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Tamamlanan Merhaba uygulaması hello de bu öğreticinin sonunda sağlanır.

## <a name="step-1-register-an-app"></a>1. adım: uygulama kaydetmeyi
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba sayfanın üst kısmındaki hello Hello menüde hesabınızı seçin. Merhaba altında **Directory** listesinde, uygulamanızın hello Active Directory Kiracı tooregister istediğiniz yeri seçin.

3. Seçin **daha Hizmetleri** hello hello menüsünde sol Merhaba ekranında tarafında ve ardından **Azure Active Directory**.

4. Seçin **uygulama kayıtlar**ve ardından **Ekle**.

5. Merhaba istemleri toocreate izleyin bir **Web uygulaması** ve/veya **Webapı**.
  * Merhaba **adı** Merhaba uygulama, uygulama toousers açıklar.

  * Merhaba **oturum açma URL'si** , uygulamanızın hello temel URL'dir.  Merhaba çatıyı'nın varsayılan değer ' http://localhost: 3000/auth/openıd/return ''.

6. Azure AD kaydettikten sonra uygulamanızı bir benzersiz uygulama kimliği atar. Bu değer hello aşağıdaki gereksinim duyduğunuz bölümleri, böylece hello uygulama sayfasından onu kopyalayın.
7. Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin. Merhaba **uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır. Merhaba kuraldır toouse hello biçimi `https://<tenant-domain>/<app-name>`, örneğin: `https://contoso.onmicrosoft.com/my-first-aad-app`.

## <a name="step-2-add-prerequisites-tooyour-directory"></a>2. adım: Önkoşullar tooyour Dizin Ekle
1. Zaten orada değilseniz hello komut satırında, dizinleri tooyour kök klasörü değiştirin ve sonra çalışma hello aşağıdaki komutlar:

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. Ayrıca, gereksinim duyduğunuz `passport-azure-ad`:
    * `npm install passport-azure-ad`

Bu hello kitaplıkları yükler, `passport-azure-ad` bağlıdır.

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a>3. adım: Uygulama toouse hello passport düğümü js stratejinizi ayarlama
Burada, Express toouse hello Openıd Connect kimlik doğrulama protokolünü yapılandırın.  Passport kullanılan toodo olduğu sorunu oturum açma ve oturum kapatma isteklerini dahil olmak üzere çeşitli şeyler hello kullanıcının oturumunu yönetmek ve hello kullanıcı hakkında bilgi alın.

1. toobegin, açık hello `config.js` dosya hello hello proje kökündeki ve uygulamanızın yapılandırma değerlerini hello enter `exports.creds` bölümü.

  * Merhaba `clientID` hello olan **uygulama kimliği** atanan tooyour uygulama hello kayıt Portalı'nda olmasıdır.

  * Merhaba `returnURL` hello olan **yeniden yönlendirme URI'si** hello portalda girdiğiniz.

  * Merhaba `clientSecret` hello Portalı'nda oluşturulan hello parolası.

2. Ardından, hello'ı açmak `app.js` hello hello proje kökündeki dosyasında. Çağrı tooinvoke hello aşağıdaki hello eklemek `OIDCStrategy` birlikte stratejisi `passport-azure-ad`.

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. Bundan sonra biz yalnızca toohandle bizim oturum açma isteklerini başvurulan hello stratejiyi kullanın.

    ```JavaScript
    // Use hello OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
        // asynchronous verification, for effect...
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
Passport, strateji yazarlarının hepsinin bağlı tüm kendi stratejileri (Twitter, Facebook vb.) için benzer bir desen kullanır. Merhaba stratejisi baktığınızda, biz ve bir yapılan bir belirtece sahip bir işlevi olarak hello parametreler geçirdiğinizi bakın. kendi iş yaptıktan sonra hello stratejisi geri toous gelir. Bunun için yeniden tooask gerekmez şekilde sonra toostore hello kullanıcı ve hazırlama hello belirteci istiyoruz.

> [!IMPORTANT]
Merhaba önceki kod tooauthenticate tooour server olur herhangi bir kullanıcı alır. Bu otomatik kaydı bilinir. Herkes bunları karar bir işlem aracılığıyla kaydetme gerekmeden tooa üretim sunucusunun kimlik doğrulaması çok izin vermeyin öneririz. Genellikle, Facebook ile tooregister izin ancak ardından ek bilgi tooprovide isteyin tüketici uygulamalarında görürsünüz hello düzeni budur. Bu örnek bir uygulama doğru değilse, biz hello kullanıcının e-posta adresi döndürdü ve ek bilgiler hello kullanıcı toofill sorulan hello belirteç nesnesi ayıklanan. Bu bir test sunucusu olduğundan, bunları toohello bellek içi veritabanına ekleriz.


4. Ardından, bize tootrack hello kullanıcıların Passport gerektirdiği gibi oturum açmış sağlayan hello yöntemler ekleyelim. Bu yöntemleri seri hale getirme ve seri durumdan hello kullanıcının bilgileri içerir.

    ```JavaScript

            // Passport session setup. (Section 2)

            //   toosupport persistent sign-in sessions, Passport needs toobe able to
            //   serialize users into hello session and deserialize them out of hello session. Typically,
            //   this is done simply by storing hello user ID when serializing and finding
            //   hello user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array toohold signed-in users
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

5.  Ardından, hello kod tooload hello Express altyapısını ekleyelim. Merhaba varsayılan /views burada kullandığımız ve Express /routes desen sağlar.

    ```JavaScript

        // configure Express (section 2)

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

6. Son olarak, hello yönlendirir o elde hello gerçek oturum açma isteklerini toohello kapalı ekleyelim `passport-azure-ad` altyapısı:


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware tooauthenticate the
        //   request. hello first step in OpenID authentication involves redirecting
        //   hello user tootheir OpenID provider. After authenticating, hello OpenID
        //   provider redirects hello user back toothis application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in hello Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware tooauthenticate the
            //   request. If authentication fails, hello user is redirected back toothe
            //   sign-in page. Otherwise, hello primary route function is called,
            //   which, in this example, redirects hello user toohello home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>4. adım: Kullanım Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD
Uygulamanızı hello uç noktası ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur.  `passport-azure-ad`alınan kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumlarını koruma hello ayrıntılarını verdiğiniz. Tüm bu kalır, kullanıcılarınızın bir şekilde toosign ve oturum kapatma vermiş ve hello oturum açmış kullanıcılar hakkında ek bilgi toplanıyor.

1. İlk olarak, hello varsayılan, oturum açma, hesap ve oturum kapatma yöntemlerini tooour ekleyelim `app.js` dosyası:

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
            log.info('Login was called in hello Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  Şimdi bunlara ayrıntılı gözden geçirin:

  * Merhaba `/`rota (varsa) hello kullanıcı hello istekte geçirme toohello index.ejs görünümü yeniden yönlendirir.
  * Merhaba `/account` ilk yol *biz doğrulaması sağlar* (biz uygulamak, aşağıdaki örneğine hello), ve böylece biz hello kullanıcı hakkında ek bilgi alabilir geçişleri hello istekteki kullanıcı hello.
  * Merhaba `/login` yol çağırır bizim azuread'i openıdconnect doğrulayıcıdan `passport-azuread`. Başarılı değil, hello kullanıcı geri çok/oturum açma yönlendirir.
  * Merhaba `/logout` rota yalnızca hello logout.ejs (ve rota), hangi tanımlama bilgilerini temizler ve ardından döndürür hello kullanıcı geri tooindex.ejs çağırır.

3. Merhaba son kısmı için `app.js`, hello ekleyelim **EnsureAuthenticated** kullanılır yöntemi `/account`, daha önce gösterildiği gibi.

    ```JavaScript

        // Simple route middleware tooensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs toobe protected. If
        //   hello request is authenticated (typically via a persistent sign-in session),
        //   hello request proceeds. Otherwise, hello user is redirected toothe
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. Son olarak, hello sunucusunun kendisi oluşturalım içinde `app.js`:

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a>5. adım: toodisplay bizim kullanıcı hello Web oluşturmak hello görünümleri ve yollar Express
Şimdi `app.js` tamamlandı. Biz yalnızca tooadd hello yollar gerekir ve biz toohello kullanıcı yanı sıra işlemek hello bu Göster hello bilgileri görünümleri `/logout` ve `/login` oluşturduğumuz yollar.

1. Merhaba oluşturmak `/routes/index.js` hello kök dizininin altındaki yol.

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. Merhaba oluşturmak `/routes/user.js` hello kök dizininin altındaki yol.

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 Bu istek tooour görünümler varsa hello kullanıcı de dahil olmak üzere hello geçirin.

3. Merhaba oluşturmak `/views/index.ejs` hello kök dizininin altında görünümü. Bu bizim oturum açma ve oturum kapatma yöntemlerini çağıran basit bir sayfadır ve bize toograb hesap bilgileri sağlar. Biz kullanabilirsiniz bildirimi hello koşullu `if (!user)` aracılığıyla hello istekte geçirilen hello kullanıcı oturum açmış bir kullanıcı sahibiz kanıt olarak.

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. Merhaba oluşturma `/views/account.ejs` biz ek bilgileri görüntüleyebilmek hello kök dizininin altındaki görüntülemek, `passport-azuread` hello kullanıcı isteğine koyulan.

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. Bu görünüm iyi bir düzen ekleyerek olalım. Merhaba oluşturmak ' / views/layout.ejs görünüm hello altında kök dizini.

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
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

##<a name="next-steps"></a>Sonraki adımlar
Son olarak, yapı ve uygulamanızı çalıştırın. Çalıştırma `node app.js`ve çok Git`http://localhost:3000`.

Kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın ve hello kullanıcının kimliğini hello ApplicationTier/account listesinde nasıl yansıtılır dikkat edin. Artık, hem kişisel hem de iş/Okul hesaplarını ile kullanıcıların kimliklerini doğrulayabilir endüstri standardı protokoller ile güvenli bir web uygulaması sahipsiniz.

Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [bir .zip dosyası olarak sağlanan](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Alternatif olarak, bu Github'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz. Tootry isteyebilirsiniz:

[Bir Web API Azure AD ile güvenliğini sağlama](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
