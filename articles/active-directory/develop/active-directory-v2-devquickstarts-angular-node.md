---
title: "aaaAzure AD v2.0 NodeJS AngularJS tek sayfa uygulaması Başlarken | Microsoft Docs"
description: "Nasıl toobuild hem kişisel Microsoft ile kullanıcılar oturum açtığında bir Açısal JS tek sayfa uygulaması hesapları ve iş veya Okul hesapları."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="59266-103">Oturum açma tooan AngularJS tek sayfalı uygulama - NodeJS Ekle</span><span class="sxs-lookup"><span data-stu-id="59266-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="59266-104">Bu makalede gücü Microsoft hesapları tooan AngularJS uygulaması hello Azure Active Directory v2.0 uç kullanarak oturum ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="59266-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="59266-105">Merhaba v2.0 uç tooperform uygulamanızda tek bir tümleştirme etkinleştirin ve hem kişisel hem de iş/Okul hesapları olan kullanıcıların kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="59266-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="59266-106">Bu örnek arka uç REST NodeJS içinde yazılmış ve Azure AD'den OAuth taşıyıcı belirteçlerini kullanarak güvenliği API görevleri depolayan basit bir Yapılacaklar listesi tek sayfa uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="59266-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="59266-107">Merhaba AngularJS uygulama bizim açık kaynak JavaScript kimlik doğrulama kitaplığı kullanır [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle tüm oturum açma işlemine hello ve arama hello REST API için belirteçleri almak.</span><span class="sxs-lookup"><span data-stu-id="59266-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="59266-108">Merhaba aynı düzeni hello gibi uygulanan tooauthenticate tooother REST API'leri olabilir [Microsoft Graph](https://graph.microsoft.com) veya Azure Resource Manager API'leri hello.</span><span class="sxs-lookup"><span data-stu-id="59266-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="59266-109">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="59266-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="59266-110">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="59266-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="59266-111">İndir</span><span class="sxs-lookup"><span data-stu-id="59266-111">Download</span></span>
<span data-ttu-id="59266-112">başlatılan tooget gerekir toodownload & yükleme [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="59266-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="59266-113">Sonra kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) iskelet uygulama:</span><span class="sxs-lookup"><span data-stu-id="59266-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="59266-114">Merhaba iskelet uygulama basit bir AngularJS uygulama için tüm hello Demirbaş kod içerir, ancak tüm hello kimlikle ilgili parçaları eksik.</span><span class="sxs-lookup"><span data-stu-id="59266-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="59266-115">Toofollow boyunca istemiyorsanız, bunun yerine, kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) tamamlandı hello örnek.</span><span class="sxs-lookup"><span data-stu-id="59266-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="59266-116">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="59266-116">Register an app</span></span>
<span data-ttu-id="59266-117">İlk olarak, bir uygulama hello oluşturmak [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="59266-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="59266-118">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="59266-118">Make sure to:</span></span>

* <span data-ttu-id="59266-119">Merhaba eklemek **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="59266-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="59266-120">Merhaba doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="59266-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="59266-121">Bu örnek için Hello varsayılan değer `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="59266-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="59266-122">Merhaba bırakın **izin örtük akış** Etkin onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="59266-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="59266-123">Merhaba basılı kopya **uygulama kimliği** , atanan tooyour uygulama, kısa süre içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="59266-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="59266-124">Adal.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="59266-124">Install adal.js</span></span>
<span data-ttu-id="59266-125">toostart, indirdiğiniz tooproject gidin ve adal.js yükleyin.</span><span class="sxs-lookup"><span data-stu-id="59266-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="59266-126">Varsa [bower](http://bower.io/) yüklüyse, bu komutu yalnızca çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59266-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="59266-127">Hiçbir bağımlılık sürümü uyuşmazlığı için yalnızca hello daha yüksek bir sürümü seçin.</span><span class="sxs-lookup"><span data-stu-id="59266-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="59266-128">Alternatif olarak, el ile yükleyebileceğiniz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) ve [angular.js adal](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="59266-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="59266-129">Her iki dosyaları toohello ekleme `app/lib/adal-angular-experimental/dist` dizin.</span><span class="sxs-lookup"><span data-stu-id="59266-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="59266-130">Artık sık kullandığınız metin düzenleyicinizde Merhaba projeyi açın ve adal.js hello sayfa gövdesi hello sonunda yük:</span><span class="sxs-lookup"><span data-stu-id="59266-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="59266-131">REST API Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="59266-131">Set up hello REST API</span></span>
<span data-ttu-id="59266-132">Ayarlamaları olsa da, get hello arka uç REST API çalışma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="59266-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="59266-133">Bir komut istemi çalıştırarak tüm hello gerekli paketleri yüklemek (Merhaba en üst düzey hello proje dizininde olduğunuzdan emin olun):</span><span class="sxs-lookup"><span data-stu-id="59266-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="59266-134">Şimdi açmak `config.js` ve hello yerine `audience` değeri:</span><span class="sxs-lookup"><span data-stu-id="59266-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="59266-135">Merhaba REST API hello Açısal uygulamasından AJAX isteği aldığında bu değer toovalidate belirteçlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="59266-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="59266-136">Bu basit REST API'si veri bellek içi - böylece her zaman toostop hello sunucu depolar, önceden oluşturulmuş tüm görevler kaybedersiniz dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="59266-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="59266-137">Tüm olan hello REST API nasıl çalıştığını ele toospend yapmamız hello zaman.</span><span class="sxs-lookup"><span data-stu-id="59266-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="59266-138">Ücretsiz toopoke hello kodda eşitleyerek ancak toolearn web API'leri Azure AD ile güvenli hale getirme hakkında daha fazla bilgi istiyorsanız, kullanıma [bu makalede](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="59266-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="59266-139">Kullanıcıların oturumunu açma</span><span class="sxs-lookup"><span data-stu-id="59266-139">Sign users in</span></span>
<span data-ttu-id="59266-140">Bazı kimlik kodu toowrite zaman.</span><span class="sxs-lookup"><span data-stu-id="59266-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="59266-141">Zaten sorunsuz şekilde Açısal yönlendirme yöntemleriyle oynadığı bir AngularJS sağlayıcısı bu adal.js içeren fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59266-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="59266-142">Merhaba adal modülü toohello uygulama ekleyerek başlayın:</span><span class="sxs-lookup"><span data-stu-id="59266-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="59266-143">Merhaba şimdi başlatabilir `adalProvider` uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="59266-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="59266-144">Harika adal.js tüm hello bilgileri artık bunu toosecure, uygulama ve oturum kullanıcılarınızın gerekir.</span><span class="sxs-lookup"><span data-stu-id="59266-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="59266-145">Tüm sürdüğünü hello uygulamasında belirli bir rota için tooforce oturum açma bir kod satırı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="59266-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="59266-146">Şimdi bir kullanıcı tıkladığında hello `TodoList` bağlantı adal.js otomatik olarak yeniden yönlendirme tooAzure için oturum açma gerekirse AD.</span><span class="sxs-lookup"><span data-stu-id="59266-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="59266-147">Oturum açma ve oturum kapatma isteklerini denetleyicilerinizi adal.js çağırarak açıkça gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="59266-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="59266-148">Kullanıcı bilgilerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="59266-148">Display user info</span></span>
<span data-ttu-id="59266-149">Merhaba kullanıcı oturumu açık, büyük olasılıkla, uygulamanızda tooaccess hello oturum açmış kullanıcının kimlik doğrulama verileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="59266-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="59266-150">Adal.js hello sizin için bu bilgileri sunan `userInfo` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="59266-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="59266-151">tooaccess görünümünde, bu nesnenin ilk adal.js toohello kök hello karşılık gelen denetleyicisi kapsamını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="59266-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="59266-152">Merhaba doğrudan ele alabileceği sonra `userInfo` görünümünüzü nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="59266-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="59266-153">Merhaba de kullanabilirsiniz `userInfo` veya hello kullanıcı oturum açmışsa, toodetermine nesnesi.</span><span class="sxs-lookup"><span data-stu-id="59266-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

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

## <a name="call-hello-rest-api"></a><span data-ttu-id="59266-154">Merhaba REST API çağrısı</span><span class="sxs-lookup"><span data-stu-id="59266-154">Call hello REST API</span></span>
<span data-ttu-id="59266-155">Son olarak, bazı belirteçleri çağrısı REST API toocreate Merhaba, okuma, güncelleştirme ve görevleri silme zamanı tooget olur.</span><span class="sxs-lookup"><span data-stu-id="59266-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="59266-156">İyi ne tahmin?</span><span class="sxs-lookup"><span data-stu-id="59266-156">Well guess what?</span></span>  <span data-ttu-id="59266-157">Toodo yok *bir şey*.</span><span class="sxs-lookup"><span data-stu-id="59266-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="59266-158">Adal.js otomatik olarak ele alma, önbellekleme ve yenileme belirteçleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="59266-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="59266-159">Bu ayrıca toooutgoing AJAX toohello REST API gönderdiğiniz istekleri konusu belirteçleri ekleme dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="59266-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="59266-160">Bu tam olarak nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="59266-160">How exactly does this work?</span></span> <span data-ttu-id="59266-161">Tüm teşekkürler toohello Sihirli biri olan [AngularJS dinleyiciler](https://docs.angularjs.org/api/ng/service/$http), giden ve gelen http iletileri adal.js tootransform sağlar.</span><span class="sxs-lookup"><span data-stu-id="59266-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="59266-162">Ayrıca, tüm istekleri toohello göndermek adal.js varsayar aynı etki alanında hello penceresi yönelik belirteçleri kullanması gereken şekilde hello aynı uygulama kimliği AngularJS uygulama hello gibi.</span><span class="sxs-lookup"><span data-stu-id="59266-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="59266-163">Merhaba kullandık bu yüzden aynı uygulama kimliği hem hello Açısal uygulama ve hello NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="59266-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="59266-164">Doğal olarak, bu davranışı geçersiz kılabilir ve adal.js tooget belirteçleri diğer REST API'leri için gerekirse - söyleyin. ancak bu basit senaryoyu hello için varsayılanları yapar.</span><span class="sxs-lookup"><span data-stu-id="59266-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="59266-165">Ne kadar kolay taşıyıcı belirteçlerini Azure AD'den toosend istekleriyle olduğunu gösteren bir parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="59266-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="59266-166">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="59266-166">Congratulations!</span></span>  <span data-ttu-id="59266-167">Azure AD tümleşik tek sayfa uygulaması tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="59266-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="59266-168">Şimdi, bir paketi alın.</span><span class="sxs-lookup"><span data-stu-id="59266-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="59266-169">Kullanıcıların kimliğini doğrulamak, güvenli bir şekilde arka uç Openıd Connect kullanarak REST API çağrısı ve hello kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="59266-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="59266-170">Merhaba kutudan çıktığında, kişisel bir Microsoft Account veya Azure AD'den bir iş/Okul hesabı olan herhangi bir kullanıcı destekler.</span><span class="sxs-lookup"><span data-stu-id="59266-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="59266-171">Merhaba uygulama, çalıştırarak bir deneyin:</span><span class="sxs-lookup"><span data-stu-id="59266-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="59266-172">Bir tarayıcıda çok gidin`http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="59266-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="59266-173">Kişisel bir Microsoft hesabı veya iş/Okul hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="59266-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="59266-174">Görevleri toohello kullanıcının yapılacaklar listesi ekleyin ve oturumu kapatın.  Try ile imzalama hello diğer hesap türü.</span><span class="sxs-lookup"><span data-stu-id="59266-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="59266-175">Bir Azure AD Kiracı toocreate iş/Okul kullanıcıları gerekiyorsa [öğrenin nasıl tooget bir burada](active-directory-howto-tenant.md) (boş).</span><span class="sxs-lookup"><span data-stu-id="59266-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="59266-176">Merhaba hakkında öğrenme toocontinue v2.0 uç Merhaba, head geri tooour [v2.0 Geliştirici Kılavuzu](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="59266-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="59266-177">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="59266-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="59266-178">Azure-Samples github'da >></span><span class="sxs-lookup"><span data-stu-id="59266-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="59266-179">Yığın taşması üzerinde Azure AD >></span><span class="sxs-lookup"><span data-stu-id="59266-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="59266-180">Azure AD belgelerinde bulunan [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="59266-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="59266-181">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="59266-181">Get security updates for our products</span></span>
<span data-ttu-id="59266-182">Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="59266-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

