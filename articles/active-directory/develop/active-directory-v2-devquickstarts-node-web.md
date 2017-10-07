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
# <a name="add-sign-in-tooa-nodejs-web-app"></a><span data-ttu-id="8657d-103">Oturum açma tooa Node.js web uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="8657d-103">Add sign-in tooa Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="8657d-104">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="8657d-104">Not all Azure Active Directory scenarios and features work with hello v2.0 endpoint.</span></span> <span data-ttu-id="8657d-105">mı hello v2.0 uç noktası veya hello v1.0 uç noktası, kullanılacağını toodetermine okuma hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="8657d-105">toodetermine whether you should use hello v2.0 endpoint or hello v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="8657d-106">Bu öğreticide, görevleri aşağıdaki Passport toodo hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="8657d-106">In this tutorial, we use Passport toodo hello following tasks:</span></span>

* <span data-ttu-id="8657d-107">Bir web uygulamasında hello kullanıcının Azure Active Directory (Azure AD) kullanarak oturum açın ve v2.0 uç hello.</span><span class="sxs-lookup"><span data-stu-id="8657d-107">In a web app, sign in hello user by using Azure Active Directory (Azure AD) and hello v2.0 endpoint.</span></span>
* <span data-ttu-id="8657d-108">Merhaba kullanıcı hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8657d-108">Display information about hello user.</span></span>
* <span data-ttu-id="8657d-109">Oturum, kullanıcı hello uygulama dışında hello.</span><span class="sxs-lookup"><span data-stu-id="8657d-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="8657d-110">**Passport**, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="8657d-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="8657d-111">Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan hiçbir Express tabanlı veya restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="8657d-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="8657d-112">Passport, bir dizi kapsamlı strateji kimlik doğrulamasını bir kullanıcı adı ve parola, Facebook, Twitter veya diğer seçenekleri kullanarak destekler.</span><span class="sxs-lookup"><span data-stu-id="8657d-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="8657d-113">Azure AD için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="8657d-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="8657d-114">Bu makalede, nasıl tooinstall hello modülü ve ardından hello Azure AD ekleyin gösteriyoruz `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="8657d-114">In this article, we show you how tooinstall hello module, and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="8657d-115">İndir</span><span class="sxs-lookup"><span data-stu-id="8657d-115">Download</span></span>
<span data-ttu-id="8657d-116">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="8657d-116">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="8657d-117">yapabilecekleriniz toofollow hello öğretici, [hello uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="8657d-117">toofollow hello tutorial, you can [download hello app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="8657d-118">Bu öğretici hello sonunda tamamlanmış Merhaba uygulaması da alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8657d-118">You also can get hello completed application at hello end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="8657d-119">1: bir uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="8657d-119">1: Register an app</span></span>
<span data-ttu-id="8657d-120">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya izleyin [bu adımları ayrıntılı](active-directory-v2-app-registration.md) tooregister bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="8657d-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) tooregister an app.</span></span> <span data-ttu-id="8657d-121">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="8657d-121">Make sure you:</span></span>

* <span data-ttu-id="8657d-122">Kopya hello **uygulama kimliği** tooyour uygulama atanmış.</span><span class="sxs-lookup"><span data-stu-id="8657d-122">Copy hello **Application Id** assigned tooyour app.</span></span> <span data-ttu-id="8657d-123">Bu öğretici için ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="8657d-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="8657d-124">Merhaba eklemek **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="8657d-124">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="8657d-125">Kopya hello **yeniden yönlendirme URI'si** hello portalından.</span><span class="sxs-lookup"><span data-stu-id="8657d-125">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="8657d-126">Merhaba varsayılan URI değeri kullanmalısınız `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="8657d-126">You must use hello default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-tooyour-directory"></a><span data-ttu-id="8657d-127">2: ön koşullar tooyour Dizin Ekle</span><span class="sxs-lookup"><span data-stu-id="8657d-127">2: Add prerequisities tooyour directory</span></span>
<span data-ttu-id="8657d-128">Zaten yoksa bir komut isteminde dizinleri toogo tooyour kök klasörü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8657d-128">At a command prompt, change directories toogo tooyour root folder, if you are not already there.</span></span> <span data-ttu-id="8657d-129">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8657d-129">Run hello following commands:</span></span>

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

<span data-ttu-id="8657d-130">Ayrıca, kullandığımız `passport-azure-ad` hello hızlı başlangıç çatısında önizlememiz hello içinde:</span><span class="sxs-lookup"><span data-stu-id="8657d-130">In addition, we use `passport-azure-ad` in hello skeleton of hello quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="8657d-131">Bu hello kitaplıkları yükler, `passport-azure-ad` kullanır.</span><span class="sxs-lookup"><span data-stu-id="8657d-131">This installs hello libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-toouse-hello-passport-node-js-strategy"></a><span data-ttu-id="8657d-132">3: uygulama toouse hello passport düğümü js stratejinizi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="8657d-132">3: Set up your app toouse hello passport-node-js strategy</span></span>
<span data-ttu-id="8657d-133">Merhaba Express ara yazılım toouse hello Openıd Connect kimlik doğrulama protokolü olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8657d-133">Set up hello Express middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="8657d-134">Passport tooissue oturum açma ve oturum kapatma isteklerini kullanın, hello kullanıcının oturumunu yönetmek ve başka şeylerin hello kullanıcı hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="8657d-134">You use Passport tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, among other things.</span></span>

1.  <span data-ttu-id="8657d-135">Merhaba proje Hello kökte hello Config.js dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8657d-135">In hello root of hello project, open hello Config.js file.</span></span> <span data-ttu-id="8657d-136">Merhaba, `exports.creds` bölümünde, uygulamanızın yapılandırma değerlerini girin.</span><span class="sxs-lookup"><span data-stu-id="8657d-136">In hello `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="8657d-137">`clientID`: Merhaba **uygulama kimliği** hello Azure portal atanan tooyour uygulamada olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="8657d-137">`clientID`: hello **Application Id** that's assigned tooyour app in hello Azure portal.</span></span>
  * <span data-ttu-id="8657d-138">`returnURL`: Merhaba **yeniden yönlendirme URI'si** hello portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="8657d-138">`returnURL`: hello **Redirect URI** that you entered in hello portal.</span></span>
  * <span data-ttu-id="8657d-139">`clientSecret`: hello Portalı'nda oluşturulan hello gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="8657d-139">`clientSecret`: hello secret that you generated in hello portal.</span></span>

2.  <span data-ttu-id="8657d-140">Merhaba proje Hello kökte hello App.js dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8657d-140">In hello root of hello project, open hello App.js file.</span></span> <span data-ttu-id="8657d-141">ile birlikte tooinvoke hello OIDCStrategy stratey `passport-azure-ad`, çağrı aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8657d-141">tooinvoke hello OIDCStrategy stratey, which comes with `passport-azure-ad`, add hello following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="8657d-142">toohandle, oturum açma istekleri, yalnızca başvurulan hello stratejisi kullanın:</span><span class="sxs-lookup"><span data-stu-id="8657d-142">toohandle your sign-in requests, use hello strategy you just referenced:</span></span>

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

<span data-ttu-id="8657d-143">Passport, tüm kendi stratejileri (Twitter, Facebook vb.) benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="8657d-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="8657d-144">Tüm strateji yazıcıları toohello düzeni uyması.</span><span class="sxs-lookup"><span data-stu-id="8657d-144">All strategy writers adhere toohello pattern.</span></span> <span data-ttu-id="8657d-145">Merhaba stratejisi geçirmek bir `function()` bir belirteç kullanan ve `done` parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="8657d-145">Pass hello strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="8657d-146">tüm iş yaptıktan sonra hello stratejisi döndürülür.</span><span class="sxs-lookup"><span data-stu-id="8657d-146">hello strategy is returned after it does all its work.</span></span> <span data-ttu-id="8657d-147">İçin yeniden tooask gerekmeyen şekilde hello kullanıcı ve hazırlama hello belirtecini depolar.</span><span class="sxs-lookup"><span data-stu-id="8657d-147">Store hello user and stash hello token so you don’t need tooask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8657d-148">Merhaba önceki kod tooyour sunucu kimliğini doğrulayabilir herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="8657d-148">hello preceding code takes any user that can authenticate tooyour server.</span></span> <span data-ttu-id="8657d-149">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="8657d-149">This is known as auto-registration.</span></span> <span data-ttu-id="8657d-150">Bir üretim sunucusunda toolet herkes bunları seçtiğiniz bir kayıt sürecinden geçerler gerekmeden istediğiniz olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="8657d-150">On a production server, you wouldn’t want toolet anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="8657d-151">Bu genellikle tüketici uygulamalarında görürsünüz hello düzeni olur.</span><span class="sxs-lookup"><span data-stu-id="8657d-151">This is usually hello pattern that you see in consumer apps.</span></span> <span data-ttu-id="8657d-152">Merhaba uygulama Facebook ile tooregister sağlayabilir, ancak tooenter ek bilgiler, ister.</span><span class="sxs-lookup"><span data-stu-id="8657d-152">hello app might allow you tooregister with Facebook, but then it asks you tooenter additional information.</span></span> <span data-ttu-id="8657d-153">Bu öğretici için bir komut satırı programı doğru kullanıyorsanız, döndürülen hello belirteç nesnesinden hello e-posta ayıklanamıyor.</span><span class="sxs-lookup"><span data-stu-id="8657d-153">If you weren't using a command-line program for this tutorial, you could extract hello email from hello token object that is returned.</span></span> <span data-ttu-id="8657d-154">Ardından, hello kullanıcı tooenter ek bilgileri isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="8657d-154">Then, you might ask hello user tooenter additional information.</span></span> <span data-ttu-id="8657d-155">Bu bir test sunucusu olduğundan, hello kullanıcı ekleme doğrudan toohello bellek içi veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8657d-155">Because this is a test server, you add hello user directly toohello in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="8657d-156">Oturum açtığınız kullanıcı tookeep izleme kullanmak hello yöntemleri ekleyin Passport'un gerektirdiği gibi.</span><span class="sxs-lookup"><span data-stu-id="8657d-156">Add hello methods that you use tookeep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="8657d-157">Bu seri hale getirme ve seri durumdan hello kullanıcının bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="8657d-157">This includes serializing and deserializing hello user's information:</span></span>

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

5.  <span data-ttu-id="8657d-158">Merhaba Express altyapısını yükler hello kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8657d-158">Add hello code that loads hello Express engine.</span></span> <span data-ttu-id="8657d-159">Merhaba varsayılan /views kullanın ve Express /routes desen sağlar:</span><span class="sxs-lookup"><span data-stu-id="8657d-159">You use hello default /views and /routes pattern that Express provides:</span></span>

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

6.  <span data-ttu-id="8657d-160">Merhaba POST yönlendirir o elde hello gerçek oturum açma isteklerini toohello kapalı eklemek `passport-azure-ad` altyapısı:</span><span class="sxs-lookup"><span data-stu-id="8657d-160">Add hello POST routes that hand off hello actual sign-in requests toohello `passport-azure-ad` engine:</span></span>

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

## <a name="4-use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="8657d-161">4: kullanım Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="8657d-161">4: Use Passport tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="8657d-162">Uygulamanızı şimdi hello v2.0 uç noktası ile toocommunicate yukarı hello Openıd Connect kimlik doğrulama protokolü kullanarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8657d-162">Your app is now set up toocommunicate with hello v2.0 endpoint by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="8657d-163">Merhaba `passport-azure-ad` stratejisi, kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve hello kullanıcı oturumunu sürdürme hello ayrıntılarını mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="8657d-163">hello `passport-azure-ad` strategy takes care of all hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining hello user session.</span></span> <span data-ttu-id="8657d-164">Toodo sol tüm kullanıcılarınız toogive olan bir şekilde toosign ve oturum out ve toogather açık olan hello kullanıcı hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="8657d-164">All that is left toodo is toogive your users a way toosign in and sign out, and toogather more information about hello user who is signed in.</span></span>

1.  <span data-ttu-id="8657d-165">Merhaba eklemek **varsayılan**, **oturum açma**, **hesap**, ve **oturum kapatma** yöntemleri tooyour App.js dosyası:</span><span class="sxs-lookup"><span data-stu-id="8657d-165">Add hello **default**, **login**, **account**, and **logout** methods tooyour App.js file:</span></span>

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

  <span data-ttu-id="8657d-166">Merhaba ayrıntıları aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="8657d-166">Here are hello details:</span></span>
    
    * <span data-ttu-id="8657d-167">Merhaba `/` rota toohello index.ejs görünümü yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="8657d-167">hello `/` route redirects toohello index.ejs view.</span></span> <span data-ttu-id="8657d-168">(Varsa) hello istekte hello kullanıcı geçirir.</span><span class="sxs-lookup"><span data-stu-id="8657d-168">It passes hello user in hello request (if it exists).</span></span>
    * <span data-ttu-id="8657d-169">Merhaba `/account` ilk yol *, kimlik doğrulaması yapmasını sağlar* (Bu koddan hello uygulamanız).</span><span class="sxs-lookup"><span data-stu-id="8657d-169">hello `/account` route first *ensures that you are authenticated* (you implement that in hello following code).</span></span> <span data-ttu-id="8657d-170">Ardından, hello istekte hello kullanıcı geçirir.</span><span class="sxs-lookup"><span data-stu-id="8657d-170">Then, it passes hello user in hello request.</span></span> <span data-ttu-id="8657d-171">Merhaba kullanıcı hakkında daha fazla bilgi sınıflandırıp budur.</span><span class="sxs-lookup"><span data-stu-id="8657d-171">This is so you can get more information about hello user.</span></span>
    * <span data-ttu-id="8657d-172">Merhaba `/login` rota çağrıları, `azuread-openidconnect` doğrulayıcıdan `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="8657d-172">hello `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="8657d-173">Başarılı değil, hello kullanıcı geri çok yeniden`/login`.</span><span class="sxs-lookup"><span data-stu-id="8657d-173">If that doesn't succeed, it redirects hello user back too`/login`.</span></span>
    * <span data-ttu-id="8657d-174">Merhaba `/logout` hello logout.ejs görüntüleyin (ve rota) yol çağırır.</span><span class="sxs-lookup"><span data-stu-id="8657d-174">hello `/logout` route calls hello logout.ejs view (and route).</span></span> <span data-ttu-id="8657d-175">Bu tanımlama bilgilerini temizler ve ardından kullanıcı geri tooindex.ejs döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="8657d-175">This clears cookies, and then returns hello user back tooindex.ejs.</span></span>

2.  <span data-ttu-id="8657d-176">Merhaba eklemek **EnsureAuthenticated** daha önce kullanılan yöntem `/account`:</span><span class="sxs-lookup"><span data-stu-id="8657d-176">Add hello **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

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

3.  <span data-ttu-id="8657d-177">App.js içinde hello sunucusu oluştur:</span><span class="sxs-lookup"><span data-stu-id="8657d-177">In App.js, create hello server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-hello-views-and-routes-in-express-that-you-show-your-user-on-hello-website"></a><span data-ttu-id="8657d-178">5: hello Web sitesinde kullanıcı Göster Express'te hello görünümleri ve yollar oluşturma</span><span class="sxs-lookup"><span data-stu-id="8657d-178">5: Create hello views and routes in Express that you show your user on hello website</span></span>
<span data-ttu-id="8657d-179">Merhaba yollar ve bilgi toohello kullanıcı Göster görünümleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8657d-179">Add hello routes and views that show information toohello user.</span></span> <span data-ttu-id="8657d-180">Merhaba yolları ve görünümleri de hello işlemek `/logout` ve `/login` oluşturduğunuz yollar.</span><span class="sxs-lookup"><span data-stu-id="8657d-180">hello routes and views also handle hello `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="8657d-181">Merhaba Hello kök dizininde oluşturmak `/routes/index.js` rota.</span><span class="sxs-lookup"><span data-stu-id="8657d-181">In hello root directory, create hello `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="8657d-182">Merhaba Hello kök dizininde oluşturmak `/routes/user.js` rota.</span><span class="sxs-lookup"><span data-stu-id="8657d-182">In hello root directory, create hello `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="8657d-183">`/routes/index.js`ve `/routes/user.js` isteği tooyour görünümlerini hello kullanıcı gibi hello geçirmek basit yollar.</span><span class="sxs-lookup"><span data-stu-id="8657d-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along hello request tooyour views, including hello user, if present.</span></span>

3.  <span data-ttu-id="8657d-184">Merhaba Hello kök dizininde oluşturmak `/views/index.ejs` görünümü.</span><span class="sxs-lookup"><span data-stu-id="8657d-184">In hello root directory, create hello `/views/index.ejs` view.</span></span> <span data-ttu-id="8657d-185">Bu sayfa çağrıları, **oturum açma** ve **oturum kapatma** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="8657d-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="8657d-186">Merhaba de `/views/index.ejs` toocapture hesap bilgileri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="8657d-186">You also use hello `/views/index.ejs` view toocapture account information.</span></span> <span data-ttu-id="8657d-187">Merhaba koşullu kullanabilirsiniz `if (!user)` aracılığıyla hello istekte geçirilen hello kullanıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="8657d-187">You can use hello conditional `if (!user)` as hello user being passed through in hello request.</span></span> <span data-ttu-id="8657d-188">Bu bulgu açtığınız kullanıcı sahip olur.</span><span class="sxs-lookup"><span data-stu-id="8657d-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="8657d-189">Merhaba Hello kök dizininde oluşturmak `/views/account.ejs` görünümü.</span><span class="sxs-lookup"><span data-stu-id="8657d-189">In hello root directory, create hello `/views/account.ejs` view.</span></span> <span data-ttu-id="8657d-190">Merhaba `/views/account.ejs` görünümü tooview ek bilgiler sağlar, `passport-azuread` hello kullanıcı istekte koyar.</span><span class="sxs-lookup"><span data-stu-id="8657d-190">hello `/views/account.ejs` view allows you tooview additional information that `passport-azuread` puts in hello user request.</span></span>

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

5.  <span data-ttu-id="8657d-191">Bir düzen ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8657d-191">Add a layout.</span></span> <span data-ttu-id="8657d-192">Merhaba Hello kök dizininde oluşturmak `/views/layout.ejs` görünümü.</span><span class="sxs-lookup"><span data-stu-id="8657d-192">In hello root directory, create hello `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="8657d-193">toobuild, uygulamanızı ve çalıştırma Çalıştır `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="8657d-193">toobuild and run your app, run `node app.js`.</span></span> <span data-ttu-id="8657d-194">Ardından, çok Git`http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="8657d-194">Then, go too`http://localhost:3000`.</span></span>

7.  <span data-ttu-id="8657d-195">Kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8657d-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="8657d-196">Merhaba kullanıcının kimliğini hello ApplicationTier/account listesinde yansıtılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8657d-196">Note that hello user's identity is reflected in hello /account list.</span></span> 

<span data-ttu-id="8657d-197">Endüstri standardı protokoller kullanılarak güvenli bir web uygulaması şimdi sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="8657d-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="8657d-198">Kişisel ve iş veya Okul hesaplarını kullanarak uygulamanızı kullanıcıların kimliklerini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8657d-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8657d-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8657d-199">Next steps</span></span>
<span data-ttu-id="8657d-200">Başvuru için tamamlandı hello örnek (yapılandırma değerleriniz olmadan) olarak sağlanan [bir .zip dosyası](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="8657d-200">For reference, hello completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="8657d-201">Aynı zamanda Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8657d-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="8657d-202">Ardından, Gelişmiş konular toomore üzerinde taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8657d-202">Next, you can move on toomore advanced topics.</span></span> <span data-ttu-id="8657d-203">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8657d-203">You might want tootry:</span></span>

[<span data-ttu-id="8657d-204">Node.js web API'si hello v2.0 uç kullanarak güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="8657d-204">Secure a Node.js web API by using hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="8657d-205">Bazı ek kaynaklar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8657d-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="8657d-206">Azure AD v2.0 Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="8657d-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="8657d-207">Yığın taşması "azure-active-directory" etiketi</span><span class="sxs-lookup"><span data-stu-id="8657d-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="8657d-208">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="8657d-208">Get security updates for our products</span></span>
<span data-ttu-id="8657d-209">Güvenlik olayları olduğunda bildirim toobe yukarı toosign öneririz.</span><span class="sxs-lookup"><span data-stu-id="8657d-209">We encourage you toosign up toobe notified when security incidents occur.</span></span> <span data-ttu-id="8657d-210">Merhaba üzerinde [Microsoft Teknik Güvenlik bildirimleri](https://technet.microsoft.com/security/dd252948) sayfasında, tooSecurity danışma uyarıları abone olun.</span><span class="sxs-lookup"><span data-stu-id="8657d-210">On hello [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe tooSecurity Advisories Alerts.</span></span>

