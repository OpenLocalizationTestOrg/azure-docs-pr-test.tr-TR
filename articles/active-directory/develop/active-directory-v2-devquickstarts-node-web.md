---
title: "Azure Active Directory v2.0 Node.js web uygulaması oturum açma | Microsoft Docs"
description: "Kişisel bir Microsoft hesabı ve bir iş veya Okul hesabı kullanarak bir kullanıcı oturum açtığında bir Node.js web uygulaması oluşturmayı öğrenin."
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
ms.openlocfilehash: 6d49c742f72440e22830915c90de009d9188db2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="d1e9d-103">Oturum açma bir Node.js web uygulamasına ekleme</span><span class="sxs-lookup"><span data-stu-id="d1e9d-103">Add sign-in to a Node.js web app</span></span>

> [!NOTE]
> <span data-ttu-id="d1e9d-104">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-104">Not all Azure Active Directory scenarios and features work with the v2.0 endpoint.</span></span> <span data-ttu-id="d1e9d-105">V2.0 uç noktası veya v1.0 uç nokta kullanması gerekip gerekmediğini belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="d1e9d-105">To determine whether you should use the v2.0 endpoint or the v1.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 

<span data-ttu-id="d1e9d-106">Bu öğreticide, aşağıdaki görevleri gerçekleştirmek için Passport kullanın:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-106">In this tutorial, we use Passport to do the following tasks:</span></span>

* <span data-ttu-id="d1e9d-107">Bir web uygulaması, Azure Active Directory (Azure AD) ve v2.0 uç noktası kullanarak kullanıcı oturum.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-107">In a web app, sign in the user by using Azure Active Directory (Azure AD) and the v2.0 endpoint.</span></span>
* <span data-ttu-id="d1e9d-108">Kullanıcı hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-108">Display information about the user.</span></span>
* <span data-ttu-id="d1e9d-109">Uygulama dışında kullanıcı oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-109">Sign the user out of the app.</span></span>

<span data-ttu-id="d1e9d-110">**Passport**, Node.js için kimlik doğrulama ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="d1e9d-111">Esnek ve modüler, Passport sorunsuz bir şekilde bırakılan hiçbir Express tabanlı veya restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-111">Flexible and modular, Passport can be unobtrusively dropped into any Express-based or restify web application.</span></span> <span data-ttu-id="d1e9d-112">Passport, bir dizi kapsamlı strateji kimlik doğrulamasını bir kullanıcı adı ve parola, Facebook, Twitter veya diğer seçenekleri kullanarak destekler.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-112">In Passport, a comprehensive set of strategies support authentication by using a username and password, Facebook, Twitter, or other options.</span></span> <span data-ttu-id="d1e9d-113">Azure AD için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-113">We have developed a strategy for Azure AD.</span></span> <span data-ttu-id="d1e9d-114">Bu makalede, modülünü yüklemek ve Azure AD eklemek nasıl gösteriyoruz `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-114">In this article, we show you how to install the module, and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="d1e9d-115">İndir</span><span class="sxs-lookup"><span data-stu-id="d1e9d-115">Download</span></span>
<span data-ttu-id="d1e9d-116">Bu öğretici için kod [GitHub'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs) korunur.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span> <span data-ttu-id="d1e9d-117">Öğreticiyi izlemek için şunları yapabilirsiniz [uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-117">To follow the tutorial, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="d1e9d-118">Bu öğretici sonunda tamamlanmış uygulama da alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-118">You also can get the completed application at the end of this tutorial.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="d1e9d-119">1: bir uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="d1e9d-119">1: Register an app</span></span>
<span data-ttu-id="d1e9d-120">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya izleyin [bu adımları ayrıntılı](active-directory-v2-app-registration.md) uygulama kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow [these detailed steps](active-directory-v2-app-registration.md) to register an app.</span></span> <span data-ttu-id="d1e9d-121">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-121">Make sure you:</span></span>

* <span data-ttu-id="d1e9d-122">Kopya **uygulama kimliği** uygulamanıza atanmış.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-122">Copy the **Application Id** assigned to your app.</span></span> <span data-ttu-id="d1e9d-123">Bu öğretici için ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-123">You need it for this tutorial.</span></span>
* <span data-ttu-id="d1e9d-124">Ekleme **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-124">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="d1e9d-125">Kopya **yeniden yönlendirme URI'si** portalından.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-125">Copy the **Redirect URI** from the portal.</span></span> <span data-ttu-id="d1e9d-126">Varsayılan URI değeri kullanmalısınız `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-126">You must use the default URI value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-add-prerequisities-to-your-directory"></a><span data-ttu-id="d1e9d-127">2: ön koşullar dizininize eklemek</span><span class="sxs-lookup"><span data-stu-id="d1e9d-127">2: Add prerequisities to your directory</span></span>
<span data-ttu-id="d1e9d-128">Zaten orada değilseniz kök klasörünüze gitmek için dizinleri bir komut isteminde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-128">At a command prompt, change directories to go to your root folder, if you are not already there.</span></span> <span data-ttu-id="d1e9d-129">Aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-129">Run the following commands:</span></span>

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

<span data-ttu-id="d1e9d-130">Ayrıca, kullandığımız `passport-azure-ad` hızlı başlangıç çatısında önizlememiz:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-130">In addition, we use `passport-azure-ad` in the skeleton of the quickstart:</span></span>

* `npm install passport-azure-ad`

<span data-ttu-id="d1e9d-131">Bu kitaplıklar yükler, `passport-azure-ad` kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-131">This installs the libraries that `passport-azure-ad` uses.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="d1e9d-132">3: passport düğümü js stratejisi kullanmak için uygulamanızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="d1e9d-132">3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="d1e9d-133">Openıd Connect kimlik doğrulama protokolünü kullanmak için Express ara yazılımını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-133">Set up the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d1e9d-134">Passport, oturum açma ve oturum kapatma isteklerini yürütmek, kullanıcının oturumunu yönetmek ve kullanıcı, başka şeylerin hakkında bilgi almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-134">You use Passport to issue sign-in and sign-out requests, manage the user's session, and get information about the user, among other things.</span></span>

1.  <span data-ttu-id="d1e9d-135">Proje kök dizininde Config.js dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-135">In the root of the project, open the Config.js file.</span></span> <span data-ttu-id="d1e9d-136">İçinde `exports.creds` bölümünde, uygulamanızın yapılandırma değerlerini girin.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-136">In the `exports.creds` section, enter your app's configuration values.</span></span>
  
  * <span data-ttu-id="d1e9d-137">`clientID`**Uygulama kimliği** Azure portalında uygulamanıza atanan.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-137">`clientID`: The **Application Id** that's assigned to your app in the Azure portal.</span></span>
  * <span data-ttu-id="d1e9d-138">`returnURL`**Yeniden yönlendirme URI'si** portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-138">`returnURL`: The **Redirect URI** that you entered in the portal.</span></span>
  * <span data-ttu-id="d1e9d-139">`clientSecret`: Portalda oluşturulan gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-139">`clientSecret`: The secret that you generated in the portal.</span></span>

2.  <span data-ttu-id="d1e9d-140">Proje kök dizininde App.js dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-140">In the root of the project, open the App.js file.</span></span> <span data-ttu-id="d1e9d-141">İle birlikte OIDCStrategy stratey çağrılacak `passport-azure-ad`, aşağıdaki çağrıyı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-141">To invoke the OIDCStrategy stratey, which comes with `passport-azure-ad`, add the following call:</span></span>

  ```JavaScript
  var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

  // Add some logging
  var log = bunyan.createLogger({
      name: 'Microsoft OIDC Example Web Application'
  });
  ```

3.  <span data-ttu-id="d1e9d-142">Oturum açma isteklerini işlemek için az önce başvurduğunuz stratejiyi kullanın:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-142">To handle your sign-in requests, use the strategy you just referenced:</span></span>

  ```JavaScript
  // Use the OIDCStrategy within Passport (section 2)
  //
  //   Strategies in Passport require a `validate` function. The function accepts
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

<span data-ttu-id="d1e9d-143">Passport, tüm kendi stratejileri (Twitter, Facebook vb.) benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-143">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on).</span></span> <span data-ttu-id="d1e9d-144">Tüm strateji yazıcıları desene bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-144">All strategy writers adhere to the pattern.</span></span> <span data-ttu-id="d1e9d-145">Stratejisi geçirmek bir `function()` bir belirteç kullanan ve `done` parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-145">Pass the strategy a `function()` that uses a token and `done` as parameters.</span></span> <span data-ttu-id="d1e9d-146">Tüm iş yaptıktan sonra strateji döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-146">The strategy is returned after it does all its work.</span></span> <span data-ttu-id="d1e9d-147">Kullanıcıyı depolayın ve böylece bunları yeniden istemeniz gerekmez belirteci kaydedin;.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-147">Store the user and stash the token so you don’t need to ask for it again.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d1e9d-148">Önceki kod sunucunuza doğrulanabilir herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-148">The preceding code takes any user that can authenticate to your server.</span></span> <span data-ttu-id="d1e9d-149">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-149">This is known as auto-registration.</span></span> <span data-ttu-id="d1e9d-150">Bir üretim sunucusunda herkes bunları seçtiğiniz bir kayıt sürecinden geçerler gerekmeden let istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-150">On a production server, you wouldn’t want to let anyone in without first having them go through a registration process that you choose.</span></span> <span data-ttu-id="d1e9d-151">Bu genellikle tüketici uygulamalarında görürsünüz düzeni olur.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-151">This is usually the pattern that you see in consumer apps.</span></span> <span data-ttu-id="d1e9d-152">Uygulama, Facebook ile kaydetmenize olanak sağlayabilir, ancak ek bilgileri girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-152">The app might allow you to register with Facebook, but then it asks you to enter additional information.</span></span> <span data-ttu-id="d1e9d-153">Bu öğretici için bir komut satırı programı doğru kullanıyorsanız, döndürülen belirteç nesnesinden e-posta ayıklanamıyor.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-153">If you weren't using a command-line program for this tutorial, you could extract the email from the token object that is returned.</span></span> <span data-ttu-id="d1e9d-154">Sonra ek bilgilerini girmesini isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-154">Then, you might ask the user to enter additional information.</span></span> <span data-ttu-id="d1e9d-155">Bu bir test sunucusu olduğundan, bellek içi veritabanına doğrudan kullanıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-155">Because this is a test server, you add the user directly to the in-memory database.</span></span>
  > 
  > 

4.  <span data-ttu-id="d1e9d-156">Oturum açtığınız kullanıcılar izlemek için kullandığınız yöntemleri ekleyin Passport'un gerektirdiği gibi.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-156">Add the methods that you use to keep track of users who are signed in, as required by Passport.</span></span> <span data-ttu-id="d1e9d-157">Bu seri hale getirme ve seri durumdan kullanıcının bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-157">This includes serializing and deserializing the user's information:</span></span>

  ```JavaScript

  // Passport session setup (section 2)

  //   To support persistent login sessions, Passport needs to be able to
  //   serialize users into, and deserialize users out of, the session. Typically,
  //   this is as simple as storing the user ID when serializing, and finding
  //   the user by ID when deserializing.
  passport.serializeUser(function(user, done) {
    done(null, user.email);
  });

  passport.deserializeUser(function(id, done) {
    findByEmail(id, function (err, user) {
      done(err, user);
    });
  });

  // Array to hold signed-in users
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

5.  <span data-ttu-id="d1e9d-158">Express altyapısını yükler kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-158">Add the code that loads the Express engine.</span></span> <span data-ttu-id="d1e9d-159">Varsayılan /views kullanın ve Express /routes desen sağlar:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-159">You use the default /views and /routes pattern that Express provides:</span></span>

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
    // Initialize Passport!  Also use passport.session() middleware, to support
    // persistent login sessions (recommended).
    app.use(passport.initialize());
    app.use(passport.session());
    app.use(app.router);
    app.use(express.static(__dirname + '/../../public'));
  });

  ```

6.  <span data-ttu-id="d1e9d-160">POST yönlendirir o elde gerçek oturum açma istekleri için devre dışı eklemek `passport-azure-ad` altyapısı:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-160">Add the POST routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

  ```JavaScript

  // Auth routes (section 3)

  // GET /auth/openid
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. The first step in OpenID authentication involves redirecting
  //   the user to the user's OpenID provider. After authenticating, the OpenID
  //   provider redirects the user back to this application at
  //   /auth/openid/return.

  app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
      log.info('Authentication was called in the sample');
      res.redirect('/');
    });

  // GET /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called.
  //   In this example, it redirects the user to the home page.
  app.get('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });

  // POST /auth/openid/return
  //   Use passport.authenticate() as route middleware to authenticate the
  //   request. If authentication fails, the user is redirected back to the
  //   sign-in page. Otherwise, the primary route function is called. 
  //   In this example, it redirects the user to the home page.

  app.post('/auth/openid/return',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {

      res.redirect('/');
    });
  ```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="d1e9d-161">4: Azure AD ile oturum açma ve oturum kapatma isteklerini yürütmek için Passport kullan</span><span class="sxs-lookup"><span data-stu-id="d1e9d-161">4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="d1e9d-162">Uygulamanız artık Openıd Connect kimlik doğrulama protokolü kullanarak v2.0 uç noktası ile iletişim kurmak için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-162">Your app is now set up to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d1e9d-163">`passport-azure-ad` Stratejisi, kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumunu sürdürme tüm ayrıntılarını mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-163">The `passport-azure-ad` strategy takes care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining the user session.</span></span> <span data-ttu-id="d1e9d-164">Tüm yapmak için sol etmektir kullanıcılarınız oturum açın ve oturumu kapatın ve oturum kullanıcının hakkında daha fazla bilgi toplamak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-164">All that is left to do is to give your users a way to sign in and sign out, and to gather more information about the user who is signed in.</span></span>

1.  <span data-ttu-id="d1e9d-165">Ekleme **varsayılan**, **oturum açma**, **hesap**, ve **oturum kapatma** App.js dosyanıza yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-165">Add the **default**, **login**, **account**, and **logout** methods to your App.js file:</span></span>

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
      log.info('Login was called in the sample');
      res.redirect('/');
  });

  app.get('/logout', function(req, res){
    req.logout();
    res.redirect('/');
  });

  ```

  <span data-ttu-id="d1e9d-166">Ayrıntıları aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-166">Here are the details:</span></span>
    
    * <span data-ttu-id="d1e9d-167">`/` Rota index.ejs görünümüne yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-167">The `/` route redirects to the index.ejs view.</span></span> <span data-ttu-id="d1e9d-168">(Varsa) istek kullanıcı geçirir.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-168">It passes the user in the request (if it exists).</span></span>
    * <span data-ttu-id="d1e9d-169">`/account` İlk yol *, kimlik doğrulaması yapmasını sağlar* (Bu aşağıdaki kodda uygulamanız).</span><span class="sxs-lookup"><span data-stu-id="d1e9d-169">The `/account` route first *ensures that you are authenticated* (you implement that in the following code).</span></span> <span data-ttu-id="d1e9d-170">Ardından, kullanıcı istekte geçirir.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-170">Then, it passes the user in the request.</span></span> <span data-ttu-id="d1e9d-171">Böylece kullanıcı hakkında daha fazla bilgi elde edebilirsiniz budur.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-171">This is so you can get more information about the user.</span></span>
    * <span data-ttu-id="d1e9d-172">`/login` Rota çağrıları, `azuread-openidconnect` doğrulayıcıdan `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-172">The `/login` route calls your `azuread-openidconnect` authenticator from `passport-azuread`.</span></span> <span data-ttu-id="d1e9d-173">Değil başarılı olursa, kullanıcının yeniden geri `/login`.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-173">If that doesn't succeed, it redirects the user back to `/login`.</span></span>
    * <span data-ttu-id="d1e9d-174">`/logout` Logout.ejs görüntüleyin (ve rota) yol çağırır.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-174">The `/logout` route calls the logout.ejs view (and route).</span></span> <span data-ttu-id="d1e9d-175">Bu tanımlama bilgilerini temizler ve ardından kullanıcıyı geri index.ejs döndürür.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-175">This clears cookies, and then returns the user back to index.ejs.</span></span>

2.  <span data-ttu-id="d1e9d-176">Ekleme **EnsureAuthenticated** daha önce kullanılan yöntem `/account`:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-176">Add the **EnsureAuthenticated** method that you used earlier in `/account`:</span></span>

  ```JavaScript

  // Route middleware to ensure the user is authenticated (section 4)

  //   Use this route middleware on any resource that needs to be protected. If
  //   the request is authenticated (typically via a persistent login session),
  //   the request proceeds. Otherwise, the user is redirected to the
  //   sign-in page.
  function ensureAuthenticated(req, res, next) {
    if (req.isAuthenticated()) { return next(); }
    res.redirect('/login')
  }

  ```

3.  <span data-ttu-id="d1e9d-177">App.js içinde sunucu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-177">In App.js, create the server:</span></span>

  ```JavaScript

  app.listen(3000);

  ```


## <a name="5-create-the-views-and-routes-in-express-that-you-show-your-user-on-the-website"></a><span data-ttu-id="d1e9d-178">5: kullanıcı Web sitesinde Göster Express'te yolları ve görünümleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1e9d-178">5: Create the views and routes in Express that you show your user on the website</span></span>
<span data-ttu-id="d1e9d-179">Yollar ve kullanıcı bilgilerini göster görünümleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-179">Add the routes and views that show information to the user.</span></span> <span data-ttu-id="d1e9d-180">Yolları ve görünümleri de işlemek `/logout` ve `/login` oluşturduğunuz yollar.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-180">The routes and views also handle the `/logout` and `/login` routes that you created.</span></span>

1. <span data-ttu-id="d1e9d-181">Kök dizininde oluşturmak `/routes/index.js` rota.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-181">In the root directory, create the `/routes/index.js` route.</span></span>

  ```JavaScript

  /*
  * GET home page.
  */

  exports.index = function(req, res){
    res.render('index', { title: 'Express' });
  };
  ```

2.  <span data-ttu-id="d1e9d-182">Kök dizininde oluşturmak `/routes/user.js` rota.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-182">In the root directory, create the `/routes/user.js` route.</span></span>

  ```JavaScript

  /*
  * GET users listing.
  */

  exports.list = function(req, res){
    res.send("respond with a resource");
  };
  ```

  <span data-ttu-id="d1e9d-183">`/routes/index.js`ve `/routes/user.js` isteği varsa kullanıcı da dahil olmak üzere, geçer basit yollar.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-183">`/routes/index.js` and `/routes/user.js` are simple routes that pass along the request to your views, including the user, if present.</span></span>

3.  <span data-ttu-id="d1e9d-184">Kök dizininde oluşturmak `/views/index.ejs` görünümü.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-184">In the root directory, create the `/views/index.ejs` view.</span></span> <span data-ttu-id="d1e9d-185">Bu sayfa çağrıları, **oturum açma** ve **oturum kapatma** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-185">This page calls your **login** and **logout** methods.</span></span> <span data-ttu-id="d1e9d-186">Aynı zamanda `/views/index.ejs` hesap bilgileri yakalamak için görünümü.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-186">You also use the `/views/index.ejs` view to capture account information.</span></span> <span data-ttu-id="d1e9d-187">Koşullu kullanabilirsiniz `if (!user)` aracılığıyla istekte geçirilen kullanıcı olarak.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-187">You can use the conditional `if (!user)` as the user being passed through in the request.</span></span> <span data-ttu-id="d1e9d-188">Bu bulgu açtığınız kullanıcı sahip olur.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-188">It is evidence that you have a user signed in.</span></span>

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

4.  <span data-ttu-id="d1e9d-189">Kök dizininde oluşturmak `/views/account.ejs` görünümü.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-189">In the root directory, create the `/views/account.ejs` view.</span></span> <span data-ttu-id="d1e9d-190">`/views/account.ejs` Görünümü sağlar, ek bilgileri görüntülemek, `passport-azuread` kullanıcı isteğine koyar.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-190">The `/views/account.ejs` view allows you to view additional information that `passport-azuread` puts in the user request.</span></span>

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

5.  <span data-ttu-id="d1e9d-191">Bir düzen ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-191">Add a layout.</span></span> <span data-ttu-id="d1e9d-192">Kök dizininde oluşturmak `/views/layout.ejs` görünümü.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-192">In the root directory, create the `/views/layout.ejs` view.</span></span>

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

6.  <span data-ttu-id="d1e9d-193">Derleme ve uygulamanızı çalıştırmak için Çalıştır `node app.js`.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-193">To build and run your app, run `node app.js`.</span></span> <span data-ttu-id="d1e9d-194">Ardından, Git `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-194">Then, go to `http://localhost:3000`.</span></span>

7.  <span data-ttu-id="d1e9d-195">Kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-195">Sign in with either a personal Microsoft account or a work or school account.</span></span> <span data-ttu-id="d1e9d-196">Kullanıcının kimliğini ApplicationTier/account listesinde yansıtılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-196">Note that the user's identity is reflected in the /account list.</span></span> 

<span data-ttu-id="d1e9d-197">Endüstri standardı protokoller kullanılarak güvenli bir web uygulaması şimdi sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-197">You now have a web app that is secured by using industry standard protocols.</span></span> <span data-ttu-id="d1e9d-198">Kişisel ve iş veya Okul hesaplarını kullanarak uygulamanızı kullanıcıların kimliklerini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-198">You can authenticate users in your app by using their personal and work or school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1e9d-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1e9d-199">Next steps</span></span>
<span data-ttu-id="d1e9d-200">Başvuru için tamamlanan örnek (yapılandırma değerleriniz olmadan) olarak sağlanan [bir .zip dosyası](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d1e9d-200">For reference, the completed sample (without your configuration values) is provided as [a .zip file](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip).</span></span> <span data-ttu-id="d1e9d-201">Aynı zamanda Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-201">You also can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="d1e9d-202">Ardından, size daha ileri seviyeli konulara geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-202">Next, you can move on to more advanced topics.</span></span> <span data-ttu-id="d1e9d-203">Denemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-203">You might want to try:</span></span>

[<span data-ttu-id="d1e9d-204">Node.js web API'si v2.0 uç noktası kullanarak güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="d1e9d-204">Secure a Node.js web API by using the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="d1e9d-205">Bazı ek kaynaklar aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d1e9d-205">Here are some additional resources:</span></span>

* [<span data-ttu-id="d1e9d-206">Azure AD v2.0 Geliştirici Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d1e9d-206">Azure AD v2.0 developer guide</span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="d1e9d-207">Yığın taşması "azure-active-directory" etiketi</span><span class="sxs-lookup"><span data-stu-id="d1e9d-207">Stack Overflow "azure-active-directory" tag</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

### <a name="get-security-updates-for-our-products"></a><span data-ttu-id="d1e9d-208">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="d1e9d-208">Get security updates for our products</span></span>
<span data-ttu-id="d1e9d-209">Güvenlik olayları oluştuğunda bildirim almak için kaydolun öneririz.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-209">We encourage you to sign up to be notified when security incidents occur.</span></span> <span data-ttu-id="d1e9d-210">Üzerinde [Microsoft Teknik Güvenlik bildirimleri](https://technet.microsoft.com/security/dd252948) sayfasında, güvenlik danışma uyarılara abone.</span><span class="sxs-lookup"><span data-stu-id="d1e9d-210">On the [Microsoft Technical Security Notifications](https://technet.microsoft.com/security/dd252948) page, subscribe to Security Advisories Alerts.</span></span>

