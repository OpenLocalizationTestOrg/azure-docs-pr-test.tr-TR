---
title: "aaaAzure AD Başlarken AngularJS | Microsoft Docs"
description: "Nasıl toobuild bir AngularJS tek sayfalı uygulama oturum açma için Azure AD ile tümleşir ve OAuth kullanarak Azure AD korumalı API'lerini çağırır."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="ac571-103">AngularJS tek sayfa uygulamaları Azure AD kullanarak korunmasına yardımcı olma</span><span class="sxs-lookup"><span data-stu-id="ac571-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ac571-104">Azure Active Directory (Azure AD) yapar, bunu, basit ve, tooadd oturum açma, oturum kapatma için kolay ve güvenli OAuth API tek sayfa uygulamaları tooyour çağırır.</span><span class="sxs-lookup"><span data-stu-id="ac571-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="ac571-105">Uygulamaları tooauthenticate Kullanıcılarınızla, Windows Server Active Directory hesaplarını sağlar ve tüm web Azure AD, Office 365 API'leri hello veya hello Azure API gibi korur API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ac571-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="ac571-106">Bir tarayıcıda çalışan JavaScript uygulamaları için Azure AD hello sağlar. Active Directory Authentication Library (ADAL) ya da adal.js.</span><span class="sxs-lookup"><span data-stu-id="ac571-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="ac571-107">Merhaba adal.js tek amacı toomake Bu, uygulama tooget erişim belirteçleri için kolay.</span><span class="sxs-lookup"><span data-stu-id="ac571-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="ac571-108">toodemonstrate olduğu, ne kadar kolay burada size bir AngularJS tooDo listesi uygulaması, yapı:</span><span class="sxs-lookup"><span data-stu-id="ac571-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="ac571-109">İşaretlerini hello kimlik sağlayıcısı Azure AD kullanarak toohello uygulamasında kullanıcı hello.</span><span class="sxs-lookup"><span data-stu-id="ac571-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="ac571-110">Merhaba kullanıcı hakkındaki bazı bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ac571-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="ac571-111">Güvenli bir şekilde Azure AD'den taşıyıcı belirteçlerini kullanarak uygulamanın tooDo listesi API çağrıları hello.</span><span class="sxs-lookup"><span data-stu-id="ac571-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="ac571-112">İşaretlerini hello uygulama dışı kullanıcı hello.</span><span class="sxs-lookup"><span data-stu-id="ac571-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="ac571-113">toobuild hello eksiksiz, çalışan bir uygulama şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac571-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="ac571-114">Uygulamanızı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ac571-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="ac571-115">ADAL yükleyin ve hello tek sayfalı uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ac571-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="ac571-116">ADAL toohelp güvenli sayfaları hello tek sayfalı uygulama kullanma.</span><span class="sxs-lookup"><span data-stu-id="ac571-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="ac571-117">başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ac571-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ac571-118">Ayrıca kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac571-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="ac571-119">Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ac571-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="ac571-120">1. adım: Merhaba DirectorySearcher uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="ac571-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="ac571-121">tooenable uygulama tooauthenticate kullanıcılar ve get belirteçleri, ilk gerek tooregister, Azure ad Kiracı:</span><span class="sxs-lookup"><span data-stu-id="ac571-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="ac571-122">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac571-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ac571-123">Toomultiple dizinlerde kaydolduysanız hello doğru dizin görüntülemekte olduğunuz tooensure gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ac571-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="ac571-124">toodo bu nedenle, hello üst çubuğunda tıklatın hesabınızı.</span><span class="sxs-lookup"><span data-stu-id="ac571-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="ac571-125">Merhaba altında **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="ac571-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="ac571-126">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac571-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ac571-127">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ac571-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ac571-128">Merhaba komut istemlerini izleyin ve yeni web uygulaması ve/veya web API oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ac571-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="ac571-129">**Ad** uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="ac571-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="ac571-130">**Yeniden yönlendirme URI'si** hello konumu toowhich Azure AD belirteçleri döndürecektir olduğu.</span><span class="sxs-lookup"><span data-stu-id="ac571-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="ac571-131">Bu örnek Hello varsayılan konumu `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="ac571-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="ac571-132">Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği tooyour uygulama atar.</span><span class="sxs-lookup"><span data-stu-id="ac571-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="ac571-133">Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ac571-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="ac571-134">Adal.js Azure AD ile Merhaba OAuth örtük akış toocommunicate kullanır.</span><span class="sxs-lookup"><span data-stu-id="ac571-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="ac571-135">Uygulamanız için hello örtük akış etkinleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ac571-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="ac571-136">Merhaba uygulaması tıklayın ve **bildirim** tooopen hello satır içi bildirim Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="ac571-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="ac571-137">Merhaba bulun `oauth2AllowImplicitFlow` özelliği.</span><span class="sxs-lookup"><span data-stu-id="ac571-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="ac571-138">Değerini çok ayarlama`true`.</span><span class="sxs-lookup"><span data-stu-id="ac571-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="ac571-139">Tıklatın **kaydetmek** toosave hello bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ac571-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="ac571-140">Uygulamanız için Kiracı arasında izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="ac571-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="ac571-141">Çok Git**ayarları** > **özellikleri** > **gerekli izinler**, hello tıklatıp **izinler**hello üst çubuğu düğmesini.</span><span class="sxs-lookup"><span data-stu-id="ac571-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="ac571-142">Tıklatın **Evet** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="ac571-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="ac571-143">2. adım: Yükleme ADAL ve hello tek sayfalı uygulama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac571-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="ac571-144">Azure AD'de bir uygulamanız varsa, adal.js yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="ac571-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="ac571-145">Merhaba JavaScript istemci yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ac571-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="ac571-146">Merhaba Paket Yöneticisi konsolu kullanılarak adal.js toohello TodoSPA proje ekleyerek başlayın:</span><span class="sxs-lookup"><span data-stu-id="ac571-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="ac571-147">Karşıdan [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) ve toohello ekleyin `App/Scripts/` proje dizini.</span><span class="sxs-lookup"><span data-stu-id="ac571-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="ac571-148">Karşıdan [angular.js adal](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) ve toohello ekleyin `App/Scripts/` proje dizini.</span><span class="sxs-lookup"><span data-stu-id="ac571-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="ac571-149">Her komut dosyası hello hello sonuna önce yük `</body>` içinde `index.html`:</span><span class="sxs-lookup"><span data-stu-id="ac571-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="ac571-150">Merhaba arka uç sunucusu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ac571-150">Configure hello back end server</span></span>
<span data-ttu-id="ac571-151">Merhaba tarayıcısından Hello tek sayfalı uygulama arka uç tooDo listesi API tooaccept belirteçleri için hello arka uç hello uygulama kaydı hakkında yapılandırma bilgilerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac571-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="ac571-152">Merhaba TodoSPA projeyi açın `web.config`.</span><span class="sxs-lookup"><span data-stu-id="ac571-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="ac571-153">Merhaba hello öğelerin Hello değerleri değiştirmek `<appSettings>` içinde kullanılan bölüm tooreflect hello değerleri hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="ac571-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="ac571-154">ADAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="ac571-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="ac571-155">`ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com Hello etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="ac571-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="ac571-156">`ida:Audience`Merhaba istemci uygulamanızın hello portalından kopyalandığından kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="ac571-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="ac571-157">3. adım: Kullanım ADAL toohelp güvenli sayfalarında hello tek sayfalı uygulama</span><span class="sxs-lookup"><span data-stu-id="ac571-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="ac571-158">Güvenli tek bir görünüm tek sayfalı uygulamanıza yardımcı olacak Adal.js AngularJS yolu ve HTTP sağlayıcıları ile tümleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ac571-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="ac571-159">İçinde `App/Scripts/app.js`, hello adal.js modülünde getirin:</span><span class="sxs-lookup"><span data-stu-id="ac571-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="ac571-160">Initialize `adalProvider` hello yapılandırma değerlerini uygulama kaydınızı, da kullanarak `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="ac571-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. <span data-ttu-id="ac571-161">Güvenli hello Yardım `TodoList` tek satırlık bir kod kullanarak hello uygulaması görünümünde: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="ac571-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="ac571-162">Özet</span><span class="sxs-lookup"><span data-stu-id="ac571-162">Summary</span></span>
<span data-ttu-id="ac571-163">Artık kullanıcılar oturum ve istekleri taşıyıcı belirteci korumalı tooits arka uç API'si sorun güvenli bir tek sayfalı uygulama vardır.</span><span class="sxs-lookup"><span data-stu-id="ac571-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="ac571-164">Bir kullanıcı hello tıkladığında **TodoList** bağlantı adal.js otomatik olarak yeniden yönlendirme tooAzure için oturum açma gerekirse AD.</span><span class="sxs-lookup"><span data-stu-id="ac571-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="ac571-165">Ayrıca, adal.js toohello uygulamanızın arka uç gönderilen Ajax istekleri bir erişim belirteci tooany otomatik olarak ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="ac571-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="ac571-166">Merhaba önceki hello tam minimum gerekli toobuild tek sayfalı uygulama adal.js kullanarak adımlardır.</span><span class="sxs-lookup"><span data-stu-id="ac571-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="ac571-167">Ancak bazı özellikler tek sayfalı uygulama yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="ac571-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="ac571-168">tooexplicitly oturum açma ve oturum kapatma isteklerini vermek, adal.js çağırma denetleyicilerinizi içinde işlevler de tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac571-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="ac571-169">İçinde `App/Scripts/homeCtrl.js`:</span><span class="sxs-lookup"><span data-stu-id="ac571-169">In `App/Scripts/homeCtrl.js`:</span></span>

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* <span data-ttu-id="ac571-170">Merhaba uygulamanın kullanıcı arabiriminde toopresent kullanıcı bilgilerini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac571-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="ac571-171">Merhaba ADAL hizmet toohello zaten eklendi `userDataCtrl` hello erişebilmesi için denetleyici `userInfo` hello nesnesinde ilişkili Görünüm `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="ac571-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="ac571-172">Veya hello kullanıcı oturum açmışsa, tooknow istediğiniz neden birçok senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="ac571-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="ac571-173">Merhaba de kullanabilirsiniz `userInfo` bu bilgileri toogather nesne.</span><span class="sxs-lookup"><span data-stu-id="ac571-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="ac571-174">Örneğin, `index.html`, her iki hello gösterebilir **oturum açma** veya **oturum kapatma** düğmesi dayalı kimlik doğrulama durumu:</span><span class="sxs-lookup"><span data-stu-id="ac571-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="ac571-175">Azure AD ile tümleşik tek sayfalı uygulama kullanıcıların kimliğini doğrulamak, güvenli bir şekilde arka uç OAuth 2.0 kullanarak çağırmayı ve hello kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="ac571-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="ac571-176">Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ac571-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="ac571-177">TooDo listesi tek sayfalı uygulamanızı çalıştırma ve kullanıcılarla biri ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ac571-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="ac571-178">Görevleri toohello kullanıcının yapılacaklar listesi ekleme, oturumu kapatın ve yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ac571-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="ac571-179">Adal.js uygulamanıza kolayca tooincorporate ortak kimlik özelliklerinin kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ac571-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="ac571-180">Bu, tüm hello dirty çalışmasına sizin için mvc'deki: önbellek yönetimi, belirteçlerin süresinin ve daha fazlasını yenilemeyi bir oturum açma kullanıcı Arabirimi ile hello kullanıcı sunan OAuth protokol desteği.</span><span class="sxs-lookup"><span data-stu-id="ac571-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="ac571-181">Başvuru için (yapılandırma değerleriniz olmadan) tamamlandı hello örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ac571-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac571-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac571-182">Next steps</span></span>
<span data-ttu-id="ac571-183">Şimdi tooadditional senaryoları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac571-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="ac571-184">Tootry isteyebilirsiniz: [tek sayfalı uygulamasından CORS web API'si çağırma](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="ac571-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
