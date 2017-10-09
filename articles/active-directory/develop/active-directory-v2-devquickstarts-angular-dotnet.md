---
title: "aaaAzure AD v2.0 .NET AngularJS tek sayfa uygulaması Başlarken | Microsoft Docs"
description: "Nasıl toobuild hem kişisel Microsoft ile kullanıcılar oturum açtığında bir Açısal JS tek sayfa uygulaması hesapları ve iş veya Okul hesapları."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a><span data-ttu-id="f8da9-103">Oturum açma tooan AngularJS tek sayfalı uygulama - .NET Ekle</span><span class="sxs-lookup"><span data-stu-id="f8da9-103">Add sign-in tooan AngularJS single page app - .NET</span></span>
<span data-ttu-id="f8da9-104">Bu makalede gücü Microsoft hesapları tooan AngularJS uygulaması hello Azure Active Directory v2.0 uç kullanarak oturum ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="f8da9-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="f8da9-105">Merhaba v2.0 uç tooperform uygulamanızda tek bir tümleştirme sağlar ve hem kişisel hem de iş/Okul hesapları olan kullanıcıların kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="f8da9-105">hello v2.0 endpoint enables you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="f8da9-106">Bu örnek arka uç REST hello .NET 4.5 MVC framework kullanılarak yazılmış ve Azure AD'den OAuth taşıyıcı belirteçlerini kullanarak güvenliği API görevleri depolayan basit bir Yapılacaklar listesi tek sayfa uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="f8da9-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using hello .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="f8da9-107">Merhaba AngularJS uygulama bizim açık kaynak JavaScript kimlik doğrulama kitaplığı kullanır [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle tüm oturum açma işlemine hello ve arama hello REST API için belirteçleri almak.</span><span class="sxs-lookup"><span data-stu-id="f8da9-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="f8da9-108">Merhaba aynı düzeni hello gibi uygulanan tooauthenticate tooother REST API'leri olabilir [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f8da9-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="f8da9-109">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f8da9-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="f8da9-110">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f8da9-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="f8da9-111">İndir</span><span class="sxs-lookup"><span data-stu-id="f8da9-111">Download</span></span>
<span data-ttu-id="f8da9-112">başlatıldı, tooget toodownload gereken & Visual Studio yüklemeniz.</span><span class="sxs-lookup"><span data-stu-id="f8da9-112">tooget started, you'll need toodownload & install Visual Studio.</span></span>  <span data-ttu-id="f8da9-113">Sonra kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) iskelet uygulama:</span><span class="sxs-lookup"><span data-stu-id="f8da9-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="f8da9-114">Merhaba iskelet uygulama basit bir AngularJS uygulama için tüm hello Demirbaş kod içerir, ancak tüm hello kimlikle ilgili parçaları eksik.</span><span class="sxs-lookup"><span data-stu-id="f8da9-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="f8da9-115">Toofollow boyunca istemiyorsanız, bunun yerine, kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) tamamlandı hello örnek.</span><span class="sxs-lookup"><span data-stu-id="f8da9-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="f8da9-116">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="f8da9-116">Register an app</span></span>
<span data-ttu-id="f8da9-117">İlk olarak, bir uygulama hello oluşturmak [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f8da9-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f8da9-118">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="f8da9-118">Make sure to:</span></span>

* <span data-ttu-id="f8da9-119">Merhaba eklemek **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="f8da9-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="f8da9-120">Merhaba doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="f8da9-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="f8da9-121">Bu örnek için Hello varsayılan değer `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="f8da9-121">hello default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="f8da9-122">Merhaba bırakın **izin örtük akış** Etkin onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="f8da9-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="f8da9-123">Merhaba basılı kopya **uygulama kimliği** , atanan tooyour uygulama, kısa süre içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8da9-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="f8da9-124">Adal.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="f8da9-124">Install adal.js</span></span>
<span data-ttu-id="f8da9-125">toostart, indirdiğiniz tooproject gidin ve adal.js yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f8da9-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="f8da9-126">Varsa [bower](http://bower.io/) yüklüyse, bu komutu yalnızca çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8da9-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="f8da9-127">Hiçbir bağımlılık sürümü uyuşmazlığı için yalnızca hello daha yüksek bir sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="f8da9-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="f8da9-128">Alternatif olarak, el ile yükleyebileceğiniz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) ve [angular.js adal](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="f8da9-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="f8da9-129">Her iki dosyaları toohello ekleme `app/lib/adal-angular-experimental/dist` hello dizininde `TodoSPA` projesi.</span><span class="sxs-lookup"><span data-stu-id="f8da9-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory of hello `TodoSPA` project.</span></span>

<span data-ttu-id="f8da9-130">Şimdi hello projesini Visual Studio'da açın ve hello ana sayfanın gövdesi hello sonunda adal.js yükleyin:</span><span class="sxs-lookup"><span data-stu-id="f8da9-130">Now open hello project in Visual Studio, and load adal.js at hello end of hello main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="f8da9-131">REST API Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f8da9-131">Set up hello REST API</span></span>
<span data-ttu-id="f8da9-132">Ayarlamaları olsa da, şimdi hello arka uç REST API çalışma alın.</span><span class="sxs-lookup"><span data-stu-id="f8da9-132">While we're setting things up, let's get hello backend REST API working.</span></span>  <span data-ttu-id="f8da9-133">Merhaba proje Hello kökte açmak `web.config` ve hello yerine `audience` değeri.</span><span class="sxs-lookup"><span data-stu-id="f8da9-133">In hello root of hello project, open `web.config` and replace hello `audience` value.</span></span>  <span data-ttu-id="f8da9-134">Merhaba REST API hello Açısal uygulamasından AJAX isteği aldığında bu değer toovalidate belirteçlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="f8da9-134">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="f8da9-135">Tüm olan hello REST API nasıl çalıştığını ele toospend yapmamız hello zaman.</span><span class="sxs-lookup"><span data-stu-id="f8da9-135">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="f8da9-136">Ücretsiz toopoke hello kodda eşitleyerek ancak toolearn web API'leri Azure AD ile güvenli hale getirme hakkında daha fazla bilgi istiyorsanız, kullanıma [bu makalede](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="f8da9-136">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="f8da9-137">Kullanıcıların oturumunu açma</span><span class="sxs-lookup"><span data-stu-id="f8da9-137">Sign users in</span></span>
<span data-ttu-id="f8da9-138">Bazı kimlik kodu toowrite zaman.</span><span class="sxs-lookup"><span data-stu-id="f8da9-138">Time toowrite some identity code.</span></span>  <span data-ttu-id="f8da9-139">Zaten sorunsuz şekilde Açısal yönlendirme yöntemleriyle oynadığı bir AngularJS sağlayıcısı bu adal.js içeren fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8da9-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="f8da9-140">Merhaba adal modülü toohello uygulama ekleyerek başlayın:</span><span class="sxs-lookup"><span data-stu-id="f8da9-140">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="f8da9-141">Merhaba şimdi başlatabilir `adalProvider` uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="f8da9-141">You can now initialize hello `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="f8da9-142">Harika adal.js tüm hello bilgileri artık bunu toosecure, uygulama ve oturum kullanıcılarınızın gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8da9-142">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="f8da9-143">Tüm sürdüğünü hello uygulamasında belirli bir rota için tooforce oturum açma bir kod satırı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f8da9-143">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

<span data-ttu-id="f8da9-144">Şimdi bir kullanıcı tıkladığında hello `TodoList` bağlantı adal.js otomatik olarak yeniden yönlendirme tooAzure için oturum açma gerekirse AD.</span><span class="sxs-lookup"><span data-stu-id="f8da9-144">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="f8da9-145">Oturum açma ve oturum kapatma isteklerini denetleyicilerinizi adal.js çağırarak açıkça gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8da9-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="f8da9-146">Kullanıcı bilgilerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="f8da9-146">Display user info</span></span>
<span data-ttu-id="f8da9-147">Merhaba kullanıcı oturumu açık, büyük olasılıkla, uygulamanızda tooaccess hello oturum açmış kullanıcının kimlik doğrulama verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8da9-147">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="f8da9-148">Adal.js hello sizin için bu bilgileri sunan `userInfo` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f8da9-148">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="f8da9-149">tooaccess görünümünde, bu nesnenin ilk adal.js toohello kök hello karşılık gelen denetleyicisi kapsamını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f8da9-149">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="f8da9-150">Merhaba doğrudan ele alabileceği sonra `userInfo` görünümünüzü nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="f8da9-150">Then you can directly address hello `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="f8da9-151">Merhaba de kullanabilirsiniz `userInfo` veya hello kullanıcı oturum açmışsa, toodetermine nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f8da9-151">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a><span data-ttu-id="f8da9-152">Merhaba REST API çağrısı</span><span class="sxs-lookup"><span data-stu-id="f8da9-152">Call hello REST API</span></span>
<span data-ttu-id="f8da9-153">Son olarak, bazı belirteçleri çağrısı REST API toocreate Merhaba, okuma, güncelleştirme ve görevleri silme zamanı tooget olur.</span><span class="sxs-lookup"><span data-stu-id="f8da9-153">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="f8da9-154">İyi ne tahmin?</span><span class="sxs-lookup"><span data-stu-id="f8da9-154">Well guess what?</span></span>  <span data-ttu-id="f8da9-155">Toodo yok *bir şey*.</span><span class="sxs-lookup"><span data-stu-id="f8da9-155">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="f8da9-156">Adal.js otomatik olarak ele alma, önbellekleme ve yenileme belirteçleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f8da9-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="f8da9-157">Bu ayrıca toooutgoing AJAX toohello REST API gönderdiğiniz istekleri konusu belirteçleri ekleme dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="f8da9-157">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="f8da9-158">Bu tam olarak nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="f8da9-158">How exactly does this work?</span></span> <span data-ttu-id="f8da9-159">Tüm teşekkürler toohello Sihirli biri olan [AngularJS dinleyiciler](https://docs.angularjs.org/api/ng/service/$http), giden ve gelen http iletileri adal.js tootransform sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8da9-159">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="f8da9-160">Ayrıca, tüm istekleri toohello göndermek adal.js varsayar aynı etki alanında hello penceresi yönelik belirteçleri kullanması gereken şekilde hello aynı uygulama kimliği AngularJS uygulama hello gibi.</span><span class="sxs-lookup"><span data-stu-id="f8da9-160">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="f8da9-161">Merhaba kullandık bu yüzden aynı uygulama kimliği hem hello Açısal uygulama ve hello NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="f8da9-161">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="f8da9-162">Doğal olarak, bu davranışı geçersiz kılabilir ve adal.js tooget belirteçleri diğer REST API'leri için gerekirse - söyleyin. ancak bu basit senaryoyu hello için varsayılanları yapar.</span><span class="sxs-lookup"><span data-stu-id="f8da9-162">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="f8da9-163">Ne kadar kolay taşıyıcı belirteçlerini Azure AD'den toosend istekleriyle olduğunu gösteren bir parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f8da9-163">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="f8da9-164">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="f8da9-164">Congratulations!</span></span>  <span data-ttu-id="f8da9-165">Azure AD tümleşik tek sayfa uygulaması tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f8da9-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="f8da9-166">Şimdi, bir paketi alın.</span><span class="sxs-lookup"><span data-stu-id="f8da9-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="f8da9-167">Kullanıcıların kimliğini doğrulamak, güvenli bir şekilde arka uç Openıd Connect kullanarak REST API çağrısı ve hello kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="f8da9-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="f8da9-168">Merhaba kutudan çıktığında, kişisel bir Microsoft Account veya Azure AD'den bir iş/Okul hesabı olan herhangi bir kullanıcı destekler.</span><span class="sxs-lookup"><span data-stu-id="f8da9-168">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="f8da9-169">Merhaba uygulamayı çalıştırın ve bir tarayıcıda çok gidin`https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="f8da9-169">Run hello app, and in a browser navigate too`https://localhost:44326/`.</span></span>  <span data-ttu-id="f8da9-170">Kişisel bir Microsoft hesabı veya iş/Okul hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f8da9-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="f8da9-171">Görevleri toohello kullanıcının yapılacaklar listesi ekleyin ve oturumu kapatın.  Try ile imzalama hello diğer hesap türü.</span><span class="sxs-lookup"><span data-stu-id="f8da9-171">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="f8da9-172">Bir Azure AD Kiracı toocreate iş/Okul kullanıcıları gerekiyorsa [öğrenin nasıl tooget bir burada](active-directory-howto-tenant.md) (boş).</span><span class="sxs-lookup"><span data-stu-id="f8da9-172">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="f8da9-173">Merhaba v2.0 uç, head geri tooour hakkında öğrenme toocontinue [v2.0 Geliştirici Kılavuzu](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8da9-173">toocontinue learning about hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="f8da9-174">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="f8da9-174">For additional resources, check out:</span></span>

* [<span data-ttu-id="f8da9-175">Azure-Samples github'da >></span><span class="sxs-lookup"><span data-stu-id="f8da9-175">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="f8da9-176">Yığın taşması üzerinde Azure AD >></span><span class="sxs-lookup"><span data-stu-id="f8da9-176">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="f8da9-177">Azure AD belgelerinde bulunan [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="f8da9-177">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="f8da9-178">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="f8da9-178">Get security updates for our products</span></span>
<span data-ttu-id="f8da9-179">Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="f8da9-179">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

