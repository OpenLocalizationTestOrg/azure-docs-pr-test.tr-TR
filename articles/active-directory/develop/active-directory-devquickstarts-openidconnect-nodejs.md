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
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="c0d73-103">Node.js web uygulamasına oturum açma ve Azure AD ile oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="c0d73-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="c0d73-104">Burada Passport kullanın:</span><span class="sxs-lookup"><span data-stu-id="c0d73-104">Here we use Passport to:</span></span>

* <span data-ttu-id="c0d73-105">Oturum toohello uygulama Azure Active Directory'ye (Azure AD) kullanıcı hello.</span><span class="sxs-lookup"><span data-stu-id="c0d73-105">Sign hello user in toohello app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="c0d73-106">Merhaba kullanıcı hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c0d73-106">Display information about hello user.</span></span>
* <span data-ttu-id="c0d73-107">Oturum, kullanıcı hello uygulama dışında hello.</span><span class="sxs-lookup"><span data-stu-id="c0d73-107">Sign hello user out of hello app.</span></span>

<span data-ttu-id="c0d73-108">Passport Node.js için kimlik doğrulama Ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="c0d73-109">Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan tooany Express tabanlı veya restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="c0d73-109">Flexible and modular, Passport can be unobtrusively dropped in tooany Express-based or restify web application.</span></span> <span data-ttu-id="c0d73-110">Bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlasını kullanan kimlik doğrulama stratejileri kapsamlı bir kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="c0d73-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="c0d73-111">Microsoft Azure Active Directory için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="c0d73-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="c0d73-112">Bu modülü yükleyin ve ardından hello Microsoft Azure Active Directory ekleyin `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="c0d73-112">We install this module and then add hello Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="c0d73-113">toodo adımları izleyerek bu, Al hello:</span><span class="sxs-lookup"><span data-stu-id="c0d73-113">toodo this, take hello following steps:</span></span>

1. <span data-ttu-id="c0d73-114">Bir uygulamayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c0d73-114">Register an app.</span></span>
2. <span data-ttu-id="c0d73-115">Uygulama toouse hello ayarlamak `passport-azure-ad` stratejisi.</span><span class="sxs-lookup"><span data-stu-id="c0d73-115">Set up your app toouse hello `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="c0d73-116">Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-116">Use Passport tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="c0d73-117">Merhaba kullanıcı hakkındaki verileri yazdırın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-117">Print data about hello user.</span></span>

<span data-ttu-id="c0d73-118">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="c0d73-118">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="c0d73-119">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="c0d73-119">toofollow along, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="c0d73-120">Tamamlanan Merhaba uygulaması hello de bu öğreticinin sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-120">hello completed application is provided at hello end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="c0d73-121">1. adım: uygulama kaydetmeyi</span><span class="sxs-lookup"><span data-stu-id="c0d73-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="c0d73-122">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c0d73-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c0d73-123">Merhaba sayfanın üst kısmındaki hello Hello menüde hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="c0d73-123">In hello menu at hello top of hello page, select your account.</span></span> <span data-ttu-id="c0d73-124">Merhaba altında **Directory** listesinde, uygulamanızın hello Active Directory Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="c0d73-124">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="c0d73-125">Seçin **daha Hizmetleri** hello hello menüsünde sol Merhaba ekranında tarafında ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0d73-125">Select **More Services** in hello menu on hello left side of hello screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="c0d73-126">Seçin **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c0d73-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="c0d73-127">Merhaba istemleri toocreate izleyin bir **Web uygulaması** ve/veya **Webapı**.</span><span class="sxs-lookup"><span data-stu-id="c0d73-127">Follow hello prompts toocreate a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="c0d73-128">Merhaba **adı** Merhaba uygulama, uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="c0d73-128">hello **name** of hello application describes your application toousers.</span></span>

  * <span data-ttu-id="c0d73-129">Merhaba **oturum açma URL'si** , uygulamanızın hello temel URL'dir.</span><span class="sxs-lookup"><span data-stu-id="c0d73-129">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="c0d73-130">Merhaba çatıyı'nın varsayılan değer ' http://localhost: 3000/auth/openıd/return ''.</span><span class="sxs-lookup"><span data-stu-id="c0d73-130">hello skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="c0d73-131">Azure AD kaydettikten sonra uygulamanızı bir benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="c0d73-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="c0d73-132">Bu değer hello aşağıdaki gereksinim duyduğunuz bölümleri, böylece hello uygulama sayfasından onu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-132">You need this value in hello following sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="c0d73-133">Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c0d73-133">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="c0d73-134">Merhaba **uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-134">hello **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="c0d73-135">Merhaba kuraldır toouse hello biçimi `https://<tenant-domain>/<app-name>`, örneğin: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="c0d73-135">hello convention is toouse hello format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-tooyour-directory"></a><span data-ttu-id="c0d73-136">2. adım: Önkoşullar tooyour Dizin Ekle</span><span class="sxs-lookup"><span data-stu-id="c0d73-136">Step 2: Add prerequisites tooyour directory</span></span>
1. <span data-ttu-id="c0d73-137">Zaten orada değilseniz hello komut satırında, dizinleri tooyour kök klasörü değiştirin ve sonra çalışma hello aşağıdaki komutlar:</span><span class="sxs-lookup"><span data-stu-id="c0d73-137">From hello command line, change directories tooyour root folder if you're not already there, and then run hello following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="c0d73-138">Ayrıca, gereksinim duyduğunuz `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="c0d73-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="c0d73-139">Bu hello kitaplıkları yükler, `passport-azure-ad` bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-139">This installs hello libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="c0d73-140">3. adım: Uygulama toouse hello passport düğümü js stratejinizi ayarlama</span><span class="sxs-lookup"><span data-stu-id="c0d73-140">Step 3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="c0d73-141">Burada, Express toouse hello Openıd Connect kimlik doğrulama protokolünü yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-141">Here, we configure Express toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="c0d73-142">Passport kullanılan toodo olduğu sorunu oturum açma ve oturum kapatma isteklerini dahil olmak üzere çeşitli şeyler hello kullanıcının oturumunu yönetmek ve hello kullanıcı hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-142">Passport is used toodo various things, including issue sign-in and sign-out requests, manage hello user's session, and get information about hello user.</span></span>

1. <span data-ttu-id="c0d73-143">toobegin, açık hello `config.js` dosya hello hello proje kökündeki ve uygulamanızın yapılandırma değerlerini hello enter `exports.creds` bölümü.</span><span class="sxs-lookup"><span data-stu-id="c0d73-143">toobegin, open hello `config.js` file at hello root of hello project, and then enter your app's configuration values in hello `exports.creds` section.</span></span>

  * <span data-ttu-id="c0d73-144">Merhaba `clientID` hello olan **uygulama kimliği** atanan tooyour uygulama hello kayıt Portalı'nda olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-144">hello `clientID` is hello **Application Id** that's assigned tooyour app in hello registration portal.</span></span>

  * <span data-ttu-id="c0d73-145">Merhaba `returnURL` hello olan **yeniden yönlendirme URI'si** hello portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d73-145">hello `returnURL` is hello **Redirect Uri** that you entered in hello portal.</span></span>

  * <span data-ttu-id="c0d73-146">Merhaba `clientSecret` hello Portalı'nda oluşturulan hello parolası.</span><span class="sxs-lookup"><span data-stu-id="c0d73-146">hello `clientSecret` is hello secret that you generated in hello portal.</span></span>

2. <span data-ttu-id="c0d73-147">Ardından, hello'ı açmak `app.js` hello hello proje kökündeki dosyasında.</span><span class="sxs-lookup"><span data-stu-id="c0d73-147">Next, open hello `app.js` file in hello root of hello project.</span></span> <span data-ttu-id="c0d73-148">Çağrı tooinvoke hello aşağıdaki hello eklemek `OIDCStrategy` birlikte stratejisi `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="c0d73-148">Then add hello following call tooinvoke hello `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="c0d73-149">Bundan sonra biz yalnızca toohandle bizim oturum açma isteklerini başvurulan hello stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-149">After that, use hello strategy we just referenced toohandle our sign-in requests.</span></span>

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
<span data-ttu-id="c0d73-150">Passport, strateji yazarlarının hepsinin bağlı tüm kendi stratejileri (Twitter, Facebook vb.) için benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="c0d73-151">Merhaba stratejisi baktığınızda, biz ve bir yapılan bir belirtece sahip bir işlevi olarak hello parametreler geçirdiğinizi bakın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-151">Looking at hello strategy, you see that we pass it a function that has a token and a done as hello parameters.</span></span> <span data-ttu-id="c0d73-152">kendi iş yaptıktan sonra hello stratejisi geri toous gelir.</span><span class="sxs-lookup"><span data-stu-id="c0d73-152">hello strategy comes back toous after it does its work.</span></span> <span data-ttu-id="c0d73-153">Bunun için yeniden tooask gerekmez şekilde sonra toostore hello kullanıcı ve hazırlama hello belirteci istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="c0d73-153">Then we want toostore hello user and stash hello token so we don't need tooask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="c0d73-154">Merhaba önceki kod tooauthenticate tooour server olur herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-154">hello previous code takes any user that happens tooauthenticate tooour server.</span></span> <span data-ttu-id="c0d73-155">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="c0d73-155">This is known as auto-registration.</span></span> <span data-ttu-id="c0d73-156">Herkes bunları karar bir işlem aracılığıyla kaydetme gerekmeden tooa üretim sunucusunun kimlik doğrulaması çok izin vermeyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="c0d73-156">We    recommend that you don't let anyone authenticate tooa production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="c0d73-157">Genellikle, Facebook ile tooregister izin ancak ardından ek bilgi tooprovide isteyin tüketici uygulamalarında görürsünüz hello düzeni budur.</span><span class="sxs-lookup"><span data-stu-id="c0d73-157">This is usually hello pattern you see in consumer apps, which allow you tooregister with Facebook but then ask you tooprovide additional information.</span></span> <span data-ttu-id="c0d73-158">Bu örnek bir uygulama doğru değilse, biz hello kullanıcının e-posta adresi döndürdü ve ek bilgiler hello kullanıcı toofill sorulan hello belirteç nesnesi ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="c0d73-158">If this weren't a sample application, we could have extracted hello user's email address from hello token object that is returned and then asked hello user toofill out additional information.</span></span> <span data-ttu-id="c0d73-159">Bu bir test sunucusu olduğundan, bunları toohello bellek içi veritabanına ekleriz.</span><span class="sxs-lookup"><span data-stu-id="c0d73-159">Because this is a test server, we add them toohello in-memory database.</span></span>


4. <span data-ttu-id="c0d73-160">Ardından, bize tootrack hello kullanıcıların Passport gerektirdiği gibi oturum açmış sağlayan hello yöntemler ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="c0d73-160">Next, let's add hello methods that enable us tootrack hello signed-in users as required by Passport.</span></span> <span data-ttu-id="c0d73-161">Bu yöntemleri seri hale getirme ve seri durumdan hello kullanıcının bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="c0d73-161">These methods include serializing and deserializing hello user's information.</span></span>

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

5.  <span data-ttu-id="c0d73-162">Ardından, hello kod tooload hello Express altyapısını ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="c0d73-162">Next, let's add hello code tooload hello Express engine.</span></span> <span data-ttu-id="c0d73-163">Merhaba varsayılan /views burada kullandığımız ve Express /routes desen sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0d73-163">Here we use hello default /views and /routes pattern that Express provides.</span></span>

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

6. <span data-ttu-id="c0d73-164">Son olarak, hello yönlendirir o elde hello gerçek oturum açma isteklerini toohello kapalı ekleyelim `passport-azure-ad` altyapısı:</span><span class="sxs-lookup"><span data-stu-id="c0d73-164">Finally, let's add hello routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>


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


## <a name="step-4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="c0d73-165">4. adım: Kullanım Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="c0d73-165">Step 4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="c0d73-166">Uygulamanızı hello uç noktası ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="c0d73-166">Your app is now properly configured toocommunicate with hello endpoint by using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="c0d73-167">`passport-azure-ad`alınan kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumlarını koruma hello ayrıntılarını verdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d73-167">`passport-azure-ad` has taken care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="c0d73-168">Tüm bu kalır, kullanıcılarınızın bir şekilde toosign ve oturum kapatma vermiş ve hello oturum açmış kullanıcılar hakkında ek bilgi toplanıyor.</span><span class="sxs-lookup"><span data-stu-id="c0d73-168">All that remains is giving your users a way toosign in and sign out, and gathering additional information about hello signed-in users.</span></span>

1. <span data-ttu-id="c0d73-169">İlk olarak, hello varsayılan, oturum açma, hesap ve oturum kapatma yöntemlerini tooour ekleyelim `app.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="c0d73-169">First, let's add hello default, sign-in, account, and sign-out methods tooour `app.js` file:</span></span>

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

2.  <span data-ttu-id="c0d73-170">Şimdi bunlara ayrıntılı gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="c0d73-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="c0d73-171">Merhaba `/`rota (varsa) hello kullanıcı hello istekte geçirme toohello index.ejs görünümü yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="c0d73-171">hello `/`route redirects toohello index.ejs view, passing hello user in hello request (if it exists).</span></span>
  * <span data-ttu-id="c0d73-172">Merhaba `/account` ilk yol *biz doğrulaması sağlar* (biz uygulamak, aşağıdaki örneğine hello), ve böylece biz hello kullanıcı hakkında ek bilgi alabilir geçişleri hello istekteki kullanıcı hello.</span><span class="sxs-lookup"><span data-stu-id="c0d73-172">hello `/account` route first *ensures we are authenticated* (we implement that in hello following example), and then passes hello user in hello request so that we can get additional information about hello user.</span></span>
  * <span data-ttu-id="c0d73-173">Merhaba `/login` yol çağırır bizim azuread'i openıdconnect doğrulayıcıdan `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="c0d73-173">hello `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="c0d73-174">Başarılı değil, hello kullanıcı geri çok/oturum açma yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="c0d73-174">If that doesn't succeed, it redirects hello user back too/login.</span></span>
  * <span data-ttu-id="c0d73-175">Merhaba `/logout` rota yalnızca hello logout.ejs (ve rota), hangi tanımlama bilgilerini temizler ve ardından döndürür hello kullanıcı geri tooindex.ejs çağırır.</span><span class="sxs-lookup"><span data-stu-id="c0d73-175">hello `/logout` route simply calls hello logout.ejs (and route), which clears cookies and then returns hello user back tooindex.ejs.</span></span>

3. <span data-ttu-id="c0d73-176">Merhaba son kısmı için `app.js`, hello ekleyelim **EnsureAuthenticated** kullanılır yöntemi `/account`, daha önce gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="c0d73-176">For hello last part of `app.js`, let's add hello **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

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

4. <span data-ttu-id="c0d73-177">Son olarak, hello sunucusunun kendisi oluşturalım içinde `app.js`:</span><span class="sxs-lookup"><span data-stu-id="c0d73-177">Finally, let's create hello server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-toodisplay-our-user-in-hello-website-create-hello-views-and-routes-in-express"></a><span data-ttu-id="c0d73-178">5. adım: toodisplay bizim kullanıcı hello Web oluşturmak hello görünümleri ve yollar Express</span><span class="sxs-lookup"><span data-stu-id="c0d73-178">Step 5: toodisplay our user in hello website, create hello views and routes in Express</span></span>
<span data-ttu-id="c0d73-179">Şimdi `app.js` tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="c0d73-179">Now `app.js` is complete.</span></span> <span data-ttu-id="c0d73-180">Biz yalnızca tooadd hello yollar gerekir ve biz toohello kullanıcı yanı sıra işlemek hello bu Göster hello bilgileri görünümleri `/logout` ve `/login` oluşturduğumuz yollar.</span><span class="sxs-lookup"><span data-stu-id="c0d73-180">We simply need tooadd hello routes and views that show hello information we get toohello user, as well as handle hello `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="c0d73-181">Merhaba oluşturmak `/routes/index.js` hello kök dizininin altındaki yol.</span><span class="sxs-lookup"><span data-stu-id="c0d73-181">Create hello `/routes/index.js` route under hello root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="c0d73-182">Merhaba oluşturmak `/routes/user.js` hello kök dizininin altındaki yol.</span><span class="sxs-lookup"><span data-stu-id="c0d73-182">Create hello `/routes/user.js` route under hello root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="c0d73-183">Bu istek tooour görünümler varsa hello kullanıcı de dahil olmak üzere hello geçirin.</span><span class="sxs-lookup"><span data-stu-id="c0d73-183">These pass along hello request tooour views, including hello user if present.</span></span>

3. <span data-ttu-id="c0d73-184">Merhaba oluşturmak `/views/index.ejs` hello kök dizininin altında görünümü.</span><span class="sxs-lookup"><span data-stu-id="c0d73-184">Create hello `/views/index.ejs` view under hello root directory.</span></span> <span data-ttu-id="c0d73-185">Bu bizim oturum açma ve oturum kapatma yöntemlerini çağıran basit bir sayfadır ve bize toograb hesap bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0d73-185">This is a simple page that calls our login and logout methods and enables us toograb account information.</span></span> <span data-ttu-id="c0d73-186">Biz kullanabilirsiniz bildirimi hello koşullu `if (!user)` aracılığıyla hello istekte geçirilen hello kullanıcı oturum açmış bir kullanıcı sahibiz kanıt olarak.</span><span class="sxs-lookup"><span data-stu-id="c0d73-186">Notice that we can use hello conditional `if (!user)` as hello user being passed through in hello request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="c0d73-187">Merhaba oluşturma `/views/account.ejs` biz ek bilgileri görüntüleyebilmek hello kök dizininin altındaki görüntülemek, `passport-azuread` hello kullanıcı isteğine koyulan.</span><span class="sxs-lookup"><span data-stu-id="c0d73-187">Create hello `/views/account.ejs` view under hello root directory so that we can view additional information that `passport-azuread` has put in hello user request.</span></span>

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

5. <span data-ttu-id="c0d73-188">Bu görünüm iyi bir düzen ekleyerek olalım.</span><span class="sxs-lookup"><span data-stu-id="c0d73-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="c0d73-189">Merhaba oluşturmak ' / views/layout.ejs görünüm hello altında kök dizini.</span><span class="sxs-lookup"><span data-stu-id="c0d73-189">Create hello '/views/layout.ejs' view under hello root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="c0d73-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0d73-190">Next steps</span></span>
<span data-ttu-id="c0d73-191">Son olarak, yapı ve uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c0d73-191">Finally, build and run your app.</span></span> <span data-ttu-id="c0d73-192">Çalıştırma `node app.js`ve çok Git`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="c0d73-192">Run `node app.js`, and then go too`http://localhost:3000`.</span></span>

<span data-ttu-id="c0d73-193">Kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın ve hello kullanıcının kimliğini hello ApplicationTier/account listesinde nasıl yansıtılır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c0d73-193">Sign in with either a personal Microsoft account or a work or school account, and notice how hello user's identity is reflected in hello /account list.</span></span> <span data-ttu-id="c0d73-194">Artık, hem kişisel hem de iş/Okul hesaplarını ile kullanıcıların kimliklerini doğrulayabilir endüstri standardı protokoller ile güvenli bir web uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d73-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="c0d73-195">Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [bir .zip dosyası olarak sağlanan](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="c0d73-195">For reference, hello completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="c0d73-196">Alternatif olarak, bu Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0d73-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="c0d73-197">Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0d73-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="c0d73-198">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0d73-198">You might want tootry:</span></span>

[<span data-ttu-id="c0d73-199">Bir Web API Azure AD ile güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="c0d73-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
