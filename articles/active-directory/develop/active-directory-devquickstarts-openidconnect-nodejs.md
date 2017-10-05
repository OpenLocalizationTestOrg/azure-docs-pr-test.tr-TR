---
title: "Azure AD ile oturum açma ve oturum kapatma Node.js kullanarak Başlarken | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleşen bir Node.js Express MVC web uygulaması oluşturmayı öğrenin."
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
ms.openlocfilehash: 13317b016f9ff3955f376b858645c42668b0de42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="dbf34-103">Node.js web uygulamasına oturum açma ve Azure AD ile oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="dbf34-103">Node.js web app sign-in and sign-out with Azure AD</span></span>
<span data-ttu-id="dbf34-104">Burada Passport kullanın:</span><span class="sxs-lookup"><span data-stu-id="dbf34-104">Here we use Passport to:</span></span>

* <span data-ttu-id="dbf34-105">Kullanıcı uygulamayı Azure Active Directory (Azure AD) ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="dbf34-106">Kullanıcı hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dbf34-106">Display information about the user.</span></span>
* <span data-ttu-id="dbf34-107">Uygulama dışında kullanıcı oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="dbf34-107">Sign the user out of the app.</span></span>

<span data-ttu-id="dbf34-108">Passport Node.js için kimlik doğrulama Ara yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="dbf34-109">Esnek ve modüler, Passport sorunsuz bir şekilde her Express tabanlı bırakılabilir veya restify web uygulamasına.</span><span class="sxs-lookup"><span data-stu-id="dbf34-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="dbf34-110">Bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlasını kullanan kimlik doğrulama stratejileri kapsamlı bir kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="dbf34-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="dbf34-111">Microsoft Azure Active Directory için bir strateji geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="dbf34-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="dbf34-112">Bu modülü yükleyin ve ardından Microsoft Azure Active Directory ekleyin `passport-azure-ad` eklentisi.</span><span class="sxs-lookup"><span data-stu-id="dbf34-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="dbf34-113">Bunu yapmak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="dbf34-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="dbf34-114">Bir uygulamayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="dbf34-114">Register an app.</span></span>
2. <span data-ttu-id="dbf34-115">Kullanmak için uygulamanızı ayarlayın `passport-azure-ad` stratejisi.</span><span class="sxs-lookup"><span data-stu-id="dbf34-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="dbf34-116">Azure AD'ye yönelik oturum açma ve oturum kapatma isteklerini yürütmek için Passport kullanın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="dbf34-117">Kullanıcı hakkındaki verileri yazdırın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-117">Print data about the user.</span></span>

<span data-ttu-id="dbf34-118">Bu öğretici için kod [GitHub'da](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS) korunur.</span><span class="sxs-lookup"><span data-stu-id="dbf34-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span>  <span data-ttu-id="dbf34-119">İzlemek için [uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="dbf34-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="dbf34-120">De Bu öğretici sonunda tamamlanmış uygulama sağlanır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="dbf34-121">1. adım: uygulama kaydetmeyi</span><span class="sxs-lookup"><span data-stu-id="dbf34-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="dbf34-122">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="dbf34-123">Sayfanın en üstündeki menüde hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="dbf34-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="dbf34-124">Altında **Directory** listesinde, Active Directory Kiracı uygulamanızı kaydetmek istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="dbf34-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="dbf34-125">Seçin **daha Hizmetleri** ekran ve ardından sol tarafındaki menüde **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dbf34-125">Select **More Services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="dbf34-126">Seçin **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="dbf34-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="dbf34-127">Oluşturmak için istemleri izleyerek bir **Web uygulaması** ve/veya **Webapı**.</span><span class="sxs-lookup"><span data-stu-id="dbf34-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="dbf34-128">**Adı** kullanıcılar uygulamanıza uygulamayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="dbf34-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="dbf34-129">**Oturum açma URL'si** , uygulamanızın temel URL.</span><span class="sxs-lookup"><span data-stu-id="dbf34-129">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="dbf34-130">Çatıyı 's varsayılandır ' http://localhost: 3000/auth/openıd/return ''.</span><span class="sxs-lookup"><span data-stu-id="dbf34-130">The skeleton's default is `http://localhost:3000/auth/openid/return`\`.</span></span>

6. <span data-ttu-id="dbf34-131">Azure AD kaydettikten sonra uygulamanızı bir benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="dbf34-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="dbf34-132">Bu değer gereken aşağıdaki bölümlerde, bu nedenle uygulama sayfasından kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="dbf34-133">Gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="dbf34-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="dbf34-134">**Uygulama kimliği URI'si** uygulamanız için benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="dbf34-135">Kuralı biçim kullanmaktır `https://<tenant-domain>/<app-name>`, örneğin: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="dbf34-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="dbf34-136">2. adım: dizininize Önkoşullar ekleme</span><span class="sxs-lookup"><span data-stu-id="dbf34-136">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="dbf34-137">Komut satırından, zaten orada değilseniz kök klasörünüze yönelik dizinleri değiştirin ve ardından aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="dbf34-137">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="dbf34-138">Ayrıca, gereksinim duyduğunuz `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="dbf34-138">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="dbf34-139">Bu kitaplıklar yükler, `passport-azure-ad` bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-139">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="dbf34-140">3. adım: passport düğümü js stratejisi kullanmak için uygulamanızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-140">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="dbf34-141">Burada, Openıd Connect kimlik doğrulama protokolünü kullanmak için Express yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-141">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="dbf34-142">Passport, sorunu oturum açma ve oturum kapatma istekleri dahil olmak üzere çeşitli işlemler yapmak, kullanıcının oturumunu yönetmek ve kullanıcı hakkında bilgi almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-142">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="dbf34-143">Başlamak için açın `config.js` dosya projenin kökünde ve uygulamanızın yapılandırma değerlerini girin `exports.creds` bölümü.</span><span class="sxs-lookup"><span data-stu-id="dbf34-143">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="dbf34-144">`clientID` Olan **uygulama kimliği** kayıt portalında uygulamanıza atanan.</span><span class="sxs-lookup"><span data-stu-id="dbf34-144">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="dbf34-145">`returnURL` Olan **yeniden yönlendirme URI'si** portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="dbf34-145">The `returnURL` is the **Redirect Uri** that you entered in the portal.</span></span>

  * <span data-ttu-id="dbf34-146">`clientSecret` Portalda oluşturulan parolası.</span><span class="sxs-lookup"><span data-stu-id="dbf34-146">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="dbf34-147">Ardından, açık `app.js` proje kökündeki dosyasında.</span><span class="sxs-lookup"><span data-stu-id="dbf34-147">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="dbf34-148">Çağrılacak aşağıdaki çağrıyı ekleyin `OIDCStrategy` birlikte stratejisi `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="dbf34-148">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="dbf34-149">Bundan sonra biz bizim oturum açma isteklerini işlemek için az önce başvurduğunuz stratejiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-149">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
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
<span data-ttu-id="dbf34-150">Passport, strateji yazarlarının hepsinin bağlı tüm kendi stratejileri (Twitter, Facebook vb.) için benzer bir desen kullanır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-150">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="dbf34-151">Stratejisi baktığınızda, biz bir belirteç ve yapılan bir parametre olarak olan bir işlev geçirdiğinizi bakın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-151">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="dbf34-152">Kendi iş yaptıktan sonra strateji bize gelir.</span><span class="sxs-lookup"><span data-stu-id="dbf34-152">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="dbf34-153">Ardından kullanıcıyı depolayın ve böylece biz bunları yeniden istemeniz gerekmez belirteci kaydedin; istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="dbf34-153">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="dbf34-154">Önceki kod olur bizim sunucusuna kimlik doğrulaması için herhangi bir kullanıcı alır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-154">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="dbf34-155">Bu otomatik kaydı bilinir.</span><span class="sxs-lookup"><span data-stu-id="dbf34-155">This is known as auto-registration.</span></span> <span data-ttu-id="dbf34-156">Herhangi bir üretim sunucusuna bunları karar bir işlem aracılığıyla kaydetme gerekmeden kimlik doğrulaması çok izin vermeyin öneririz.</span><span class="sxs-lookup"><span data-stu-id="dbf34-156">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="dbf34-157">Genellikle, Facebook ile kaydedebilirsiniz ancak ek bilgileri vermeniz istenir olanak tanıyan tüketici uygulamalarında görürsünüz düzeni budur.</span><span class="sxs-lookup"><span data-stu-id="dbf34-157">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="dbf34-158">Bu örnek bir uygulama doğru değilse, biz kullanıcının e-posta adresi döndürdü ve ek bilgileri doldurmasını kullanıcıya sorulan belirteç nesnesi ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="dbf34-158">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="dbf34-159">Bu bir test sunucusu olduğundan, bunları bellek içi veritabanına ekleriz.</span><span class="sxs-lookup"><span data-stu-id="dbf34-159">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="dbf34-160">Ardından, bize Passport gerektirdiği gibi oturum açmış kullanıcıların izlemenizi sağlayan yöntemler ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="dbf34-160">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="dbf34-161">Bu yöntemler, seri hale getirme ve seri durumdan kullanıcının bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="dbf34-161">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript

            // Passport session setup. (Section 2)

            //   To support persistent sign-in sessions, Passport needs to be able to
            //   serialize users into the session and deserialize them out of the session. Typically,
            //   this is done simply by storing the user ID when serializing and finding
            //   the user by ID when deserializing.
            passport.serializeUser(function(user, done) {
            done(null, user.email);
            });

            passport.deserializeUser(function(id, done) {
            findByEmail(id, function (err, user) {
                done(err, user);
            });
            });

            // array to hold signed-in users
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

5.  <span data-ttu-id="dbf34-162">Ardından, Express altyapısını yüklemek için kod ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="dbf34-162">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="dbf34-163">Varsayılan /views burada kullandığımız ve Express /routes desen sağlar.</span><span class="sxs-lookup"><span data-stu-id="dbf34-163">Here we use the default /views and /routes pattern that Express provides.</span></span>

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
          // Initialize Passport!  Also use passport.session() middleware, to support
          // persistent login sessions (recommended).
          app.use(passport.initialize());
          app.use(passport.session());
          app.use(app.router);
          app.use(express.static(__dirname + '/../../public'));
        });

    ```

6. <span data-ttu-id="dbf34-164">Son olarak, gerçek oturum açma istekleri için kapalı el rotaları ekleyelim `passport-azure-ad` altyapısı:</span><span class="sxs-lookup"><span data-stu-id="dbf34-164">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>


       ```JavaScript

        // Our Auth routes (section 3)

        // GET /auth/openid
        //   Use passport.authenticate() as route middleware to authenticate the
        //   request. The first step in OpenID authentication involves redirecting
        //   the user to their OpenID provider. After authenticating, the OpenID
        //   provider redirects the user back to this application at
        //   /auth/openid/return.
        app.get('/auth/openid',
        passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
        function(req, res) {
            log.info('Authentication was called in the Sample');
            res.redirect('/');
        });

            // GET /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.get('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });

            // POST /auth/openid/return
            //   Use passport.authenticate() as route middleware to authenticate the
            //   request. If authentication fails, the user is redirected back to the
            //   sign-in page. Otherwise, the primary route function is called,
            //   which, in this example, redirects the user to the home page.
            app.post('/auth/openid/return',
              passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
              function(req, res) {
                log.info('We received a return from AzureAD.');
                res.redirect('/');
              });
       ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="dbf34-165">4. adım: Azure AD ile oturum açma ve oturum kapatma isteklerini yürütmek için Passport kullan</span><span class="sxs-lookup"><span data-stu-id="dbf34-165">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="dbf34-166">Uygulamanız artık Openıd Connect kimlik doğrulama protokolü kullanarak uç noktasıyla iletişim kurmak için düzgün şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-166">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="dbf34-167">`passport-azure-ad`alınan kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumlarını koruma tüm ayrıntılarını verdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="dbf34-167">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="dbf34-168">Kalan tüm kullanıcılarınızın bir şekilde oturum açabilir ve oturumu vermiş ve oturum açmış kullanıcılar hakkında ek bilgi toplanıyor.</span><span class="sxs-lookup"><span data-stu-id="dbf34-168">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="dbf34-169">İlk olarak, varsayılan, oturum açma, hesap ve oturum kapatma yöntemlerini ekleyelim bizim `app.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="dbf34-169">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

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
            log.info('Login was called in the Sample');
            res.redirect('/');
        });

        app.get('/logout', function(req, res){
          req.logout();
          res.redirect('/');
        });

    ```

2.  <span data-ttu-id="dbf34-170">Şimdi bunlara ayrıntılı gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="dbf34-170">Let's review these in detail:</span></span>

  * <span data-ttu-id="dbf34-171">`/`Rota (varsa) kullanıcı istekte geçirme index.ejs görünümüne yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="dbf34-171">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="dbf34-172">`/account` İlk yol *biz doğrulaması sağlar* (biz uygulamak, aşağıdaki örnekte) ve böylece kullanıcı hakkında ek bilgi elde edebilirsiniz kullanıcı istekte geçirir.</span><span class="sxs-lookup"><span data-stu-id="dbf34-172">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="dbf34-173">`/login` Yol çağırır bizim azuread'i openıdconnect doğrulayıcıdan `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="dbf34-173">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="dbf34-174">Değil başarılı olursa, kullanıcı geri /login yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="dbf34-174">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="dbf34-175">`/logout` Tanımlama bilgilerini temizler ve ardından kullanıcı geri index.ejs döndüren yalnızca çağrıların logout.ejs (ve rota).</span><span class="sxs-lookup"><span data-stu-id="dbf34-175">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="dbf34-176">Son bölümü için `app.js`, ekleyelim **EnsureAuthenticated** kullanılır yöntemi `/account`, daha önce gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="dbf34-176">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript

        // Simple route middleware to ensure user is authenticated. (section 4)

        //   Use this route middleware on any resource that needs to be protected. If
        //   the request is authenticated (typically via a persistent sign-in session),
        //   the request proceeds. Otherwise, the user is redirected to the
        //   sign-in page.
        function ensureAuthenticated(req, res, next) {
          if (req.isAuthenticated()) { return next(); }
          res.redirect('/login')
        }
    ```

4. <span data-ttu-id="dbf34-177">Son olarak, sunucunun kendisini oluşturalım içinde `app.js`:</span><span class="sxs-lookup"><span data-stu-id="dbf34-177">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript

        app.listen(3000);

```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="dbf34-178">5. adım: kullanıcı Web sitesi görüntülemek için görünümler ve yollar Express'te oluşturun</span><span class="sxs-lookup"><span data-stu-id="dbf34-178">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="dbf34-179">Şimdi `app.js` tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="dbf34-179">Now `app.js` is complete.</span></span> <span data-ttu-id="dbf34-180">Yalnızca yolları ve biz kullanıcıya alma yanı sıra işlemek bilgilerini göster görünümleri eklemek ihtiyacımız `/logout` ve `/login` oluşturduğumuz yollar.</span><span class="sxs-lookup"><span data-stu-id="dbf34-180">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="dbf34-181">Kök dizin kısmında `/routes/index.js` yolunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbf34-181">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
                /*
                 * GET home page.
                 */

                exports.index = function(req, res){
                  res.render('index', { title: 'Express' });
                };
    ```

2. <span data-ttu-id="dbf34-182">Kök dizin kısmında `/routes/user.js` yolunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbf34-182">Create the `/routes/user.js` route under the root directory.</span></span>

                ```JavaScript
                /*
                 * GET users listing.
                 */

                exports.list = function(req, res){
                  res.send("respond with a resource");
                };
                ```

 <span data-ttu-id="dbf34-183">Bu istek varsa kullanıcının de dahil olmak üzere bizim, geçer.</span><span class="sxs-lookup"><span data-stu-id="dbf34-183">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="dbf34-184">Kök dizin kısmında `/views/index.ejs` görünümünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbf34-184">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="dbf34-185">Bu bizim oturum açma ve oturum kapatma yöntemlerini çağırır ve hesap bilgilerini alın kurmamızı sağlayan basit bir sayfadır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-185">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="dbf34-186">Koşullu kullanabilirsiniz bildirimi `if (!user)` aracılığıyla istekte geçirilen oturum açmış bir kullanıcı sahibiz kanıt kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="dbf34-186">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

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

4. <span data-ttu-id="dbf34-187">Oluşturma `/views/account.ejs` biz ek bilgileri görüntüleyebilmek için kök dizin kısmında görüntülemek, `passport-azuread` kullanıcı isteğine getirdi.</span><span class="sxs-lookup"><span data-stu-id="dbf34-187">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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

5. <span data-ttu-id="dbf34-188">Bu görünüm iyi bir düzen ekleyerek olalım.</span><span class="sxs-lookup"><span data-stu-id="dbf34-188">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="dbf34-189">Oluştur ' / views/layout.ejs görünüm kök dizininin altında.</span><span class="sxs-lookup"><span data-stu-id="dbf34-189">Create the '/views/layout.ejs' view under the root directory.</span></span>

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

##<a name="next-steps"></a><span data-ttu-id="dbf34-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dbf34-190">Next steps</span></span>
<span data-ttu-id="dbf34-191">Son olarak, yapı ve uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dbf34-191">Finally, build and run your app.</span></span> <span data-ttu-id="dbf34-192">Çalıştırma `node app.js`ve ardından `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="dbf34-192">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="dbf34-193">Kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın ve kullanıcının kimliğini ApplicationTier/account listesinde nasıl yansıtılır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="dbf34-193">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="dbf34-194">Artık, hem kişisel hem de iş/Okul hesaplarını ile kullanıcıların kimliklerini doğrulayabilir endüstri standardı protokoller ile güvenli bir web uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbf34-194">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="dbf34-195">Tamamlanan örnek, başvuru için (yapılandırma değerleriniz olmadan) [.zip dosyası olarak sağlanır](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="dbf34-195">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="dbf34-196">Alternatif olarak, bu Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dbf34-196">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="dbf34-197">Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbf34-197">You can now move onto more advanced topics.</span></span> <span data-ttu-id="dbf34-198">Denemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dbf34-198">You might want to try:</span></span>

[<span data-ttu-id="dbf34-199">Bir Web API Azure AD ile güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="dbf34-199">Secure a Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
