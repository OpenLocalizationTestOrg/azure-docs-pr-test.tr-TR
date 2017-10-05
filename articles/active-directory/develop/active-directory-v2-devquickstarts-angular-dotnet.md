---
title: "Başlarken azure AD v2.0 .NET AngularJS tek sayfa uygulaması | Microsoft Docs"
description: "Hem kişisel Microsoft hesabı olan kullanıcılar oturum açtığında bir Açısal JS tek sayfa uygulaması oluşturma ve iş veya Okul hesapları."
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
ms.openlocfilehash: c68180c0ecabf5c0732f0db77ef1f3cc93be965b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---net"></a><span data-ttu-id="611f0-103">Oturum açma bir AngularJS tek sayfalı uygulama için - .NET ekleyin</span><span class="sxs-lookup"><span data-stu-id="611f0-103">Add sign-in to an AngularJS single page app - .NET</span></span>
<span data-ttu-id="611f0-104">Bu makalede bir AngularJS uygulamasına Azure Active Directory v2.0 uç kullanarak oturum açın. desteklenen Microsoft hesapları ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="611f0-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="611f0-105">V2.0 uç noktası, uygulamanızda tek tümleştirme gerçekleştirmek ve hem kişisel hem de iş/Okul hesapları olan kullanıcıların kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="611f0-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="611f0-106">Bu örnek görevleri arka uç REST API'si, .NET 4.5 MVC framework kullanılarak yazılmış ve Azure AD'den OAuth taşıyıcı belirteçlerini kullanarak güvenliği depolayan basit bir Yapılacaklar listesi tek sayfa uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="611f0-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="611f0-107">AngularJS uygulama bizim açık kaynak JavaScript kimlik doğrulama kitaplığı kullanır [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) tüm oturum açma işlemine işlemek ve REST API çağırma belirteçleri almak için.</span><span class="sxs-lookup"><span data-stu-id="611f0-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="611f0-108">Aynı desende diğer REST API'leri gibi kimlik doğrulaması için uygulanabilir [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="611f0-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="611f0-109">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="611f0-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="611f0-110">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="611f0-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="611f0-111">İndir</span><span class="sxs-lookup"><span data-stu-id="611f0-111">Download</span></span>
<span data-ttu-id="611f0-112">Başlamak için indir ve Visual Studio yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="611f0-112">To get started, you'll need to download & install Visual Studio.</span></span>  <span data-ttu-id="611f0-113">Sonra kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) iskelet uygulama:</span><span class="sxs-lookup"><span data-stu-id="611f0-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="611f0-114">İskelet uygulama basit bir AngularJS uygulama için tüm Demirbaş kod içerir, ancak kimlikle ilgili şey eksik.</span><span class="sxs-lookup"><span data-stu-id="611f0-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="611f0-115">Takip istemiyorsanız, bunun yerine, kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) tamamlanan örnek.</span><span class="sxs-lookup"><span data-stu-id="611f0-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="611f0-116">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="611f0-116">Register an app</span></span>
<span data-ttu-id="611f0-117">İlk olarak, bir uygulama oluşturun [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="611f0-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="611f0-118">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="611f0-118">Make sure to:</span></span>

* <span data-ttu-id="611f0-119">Ekleme **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="611f0-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="611f0-120">Doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="611f0-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="611f0-121">Bu örnek için varsayılan değer `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="611f0-121">The default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="611f0-122">Bırakın **izin örtük akış** Etkin onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="611f0-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="611f0-123">Aşağı kopyalama **uygulama kimliği** uygulamanıza atanan, kısa süre içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="611f0-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="611f0-124">Adal.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="611f0-124">Install adal.js</span></span>
<span data-ttu-id="611f0-125">Başlatmak için indirilen proje gidin ve adal.js yükleyin.</span><span class="sxs-lookup"><span data-stu-id="611f0-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="611f0-126">Varsa [bower](http://bower.io/) yüklüyse, bu komutu yalnızca çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="611f0-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="611f0-127">Hiçbir bağımlılık sürümü uyuşmazlığı için yalnızca daha yüksek sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="611f0-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="611f0-128">Alternatif olarak, el ile yükleyebileceğiniz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) ve [angular.js adal](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="611f0-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="611f0-129">Her iki dosyalarına ekleme `app/lib/adal-angular-experimental/dist` dizininde `TodoSPA` projesi.</span><span class="sxs-lookup"><span data-stu-id="611f0-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span></span>

<span data-ttu-id="611f0-130">Şimdi projesini Visual Studio'da açın ve ana sayfa gövdesi sonunda adal.js yükleyin:</span><span class="sxs-lookup"><span data-stu-id="611f0-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="611f0-131">REST API ayarlayın</span><span class="sxs-lookup"><span data-stu-id="611f0-131">Set up the REST API</span></span>
<span data-ttu-id="611f0-132">Şimdi ayarlamaları olsa da, arka uç REST API çalışma alın.</span><span class="sxs-lookup"><span data-stu-id="611f0-132">While we're setting things up, let's get the backend REST API working.</span></span>  <span data-ttu-id="611f0-133">Proje kök dizininde açın `web.config` ve değiştirme `audience` değeri.</span><span class="sxs-lookup"><span data-stu-id="611f0-133">In the root of the project, open `web.config` and replace the `audience` value.</span></span>  <span data-ttu-id="611f0-134">REST API AJAX isteği Açısal uygulamadan aldığı belirteçleri doğrulamak için bu değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="611f0-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="611f0-135">REST API nasıl çalıştığını ele harcamanız oluşturacağız her zaman olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="611f0-135">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="611f0-136">Kodda karıştırın geçici bir çözüm, ancak Azure AD ile API'leri web güvenliğini sağlama hakkında daha fazla bilgi edinmek istiyorsanız kullanıma çekinmeyin [bu makalede](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="611f0-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="611f0-137">Kullanıcıların oturumunu açma</span><span class="sxs-lookup"><span data-stu-id="611f0-137">Sign users in</span></span>
<span data-ttu-id="611f0-138">Bazı kimlik kod yazma süresi.</span><span class="sxs-lookup"><span data-stu-id="611f0-138">Time to write some identity code.</span></span>  <span data-ttu-id="611f0-139">Zaten sorunsuz şekilde Açısal yönlendirme yöntemleriyle oynadığı bir AngularJS sağlayıcısı bu adal.js içeren fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="611f0-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="611f0-140">Uygulama adal modülü ekleyerek başlayın:</span><span class="sxs-lookup"><span data-stu-id="611f0-140">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="611f0-141">Şimdi başlatabilir `adalProvider` uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="611f0-141">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="611f0-142">Harika, artık adal.js uygulamanızı güvenli ve kullanıcılar oturum açmak için gerekli tüm bilgilere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="611f0-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="611f0-143">Uygulamasında belirli bir rota için oturum açma zorlamak için gereken tek şey bir kod satırı:</span><span class="sxs-lookup"><span data-stu-id="611f0-143">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="611f0-144">Şimdi bir kullanıcı tıkladığında `TodoList` bağlantı adal.js otomatik olarak yeniden yönlendirme oturum açma için Azure ad gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="611f0-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="611f0-145">Oturum açma ve oturum kapatma isteklerini denetleyicilerinizi adal.js çağırarak açıkça gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="611f0-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="611f0-146">Kullanıcı bilgilerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="611f0-146">Display user info</span></span>
<span data-ttu-id="611f0-147">Kullanıcının oturum açtığı, uygulamanızda oturum açmış kullanıcının kimlik doğrulaması veri erişim gerekecek.</span><span class="sxs-lookup"><span data-stu-id="611f0-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="611f0-148">Adal.js gösterir bu bilgileri `userInfo` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="611f0-148">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="611f0-149">Bu nesne bir görünümde erişmek için ilk adal.js karşılık gelen denetleyicisi kök kapsamını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="611f0-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="611f0-150">Doğrudan ele alabileceği sonra `userInfo` görünümünüzü nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="611f0-150">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="611f0-151">Aynı zamanda `userInfo` kullanıcı veya oturum varsa belirlemek için nesne.</span><span class="sxs-lookup"><span data-stu-id="611f0-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="611f0-152">REST API çağrısı</span><span class="sxs-lookup"><span data-stu-id="611f0-152">Call the REST API</span></span>
<span data-ttu-id="611f0-153">Son olarak, bazı belirteçleri almak ve oluşturma, okuma, güncelleştirme için REST API çağrısı ve görevleri silme zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="611f0-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="611f0-154">İyi ne tahmin?</span><span class="sxs-lookup"><span data-stu-id="611f0-154">Well guess what?</span></span>  <span data-ttu-id="611f0-155">Yapmanıza gerek yoktur *bir şey*.</span><span class="sxs-lookup"><span data-stu-id="611f0-155">You don't have to do *a thing*.</span></span>  <span data-ttu-id="611f0-156">Adal.js otomatik olarak ele alma, önbellekleme ve yenileme belirteçleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="611f0-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="611f0-157">Bu ayrıca REST API'sine gönderdiğiniz giden AJAX istekleri için bu simgeleri ekleme dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="611f0-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="611f0-158">Bu tam olarak nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="611f0-158">How exactly does this work?</span></span> <span data-ttu-id="611f0-159">Sihirli sayesinde tümü olduğu [AngularJS dinleyiciler](https://docs.angularjs.org/api/ng/service/$http), giden ve gelen http iletileri dönüştürmek adal.js izin verir.</span><span class="sxs-lookup"><span data-stu-id="611f0-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="611f0-160">Ayrıca, adal.js penceresi AngularJS uygulama aynı uygulama Kimliğine yönelik belirteçleri kullanması gereken gibi tüm istekler aynı etki alanına göndermek varsayar.</span><span class="sxs-lookup"><span data-stu-id="611f0-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="611f0-161">Aynı uygulama kimliği hem Açısal uygulama ve NodeJS REST API kullandık nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="611f0-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="611f0-162">Elbette, bu davranışı geçersiz kılabilir ve diğer REST API'leri için gerekirse - belirteçleri almak için adal.js söyleyin ancak basit bu senaryo için varsayılanları yapar.</span><span class="sxs-lookup"><span data-stu-id="611f0-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="611f0-163">Azure AD'den taşıyıcı belirteçlerini istekleri göndermek için ne kadar kolay olduğunu gösteren bir parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="611f0-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="611f0-164">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="611f0-164">Congratulations!</span></span>  <span data-ttu-id="611f0-165">Azure AD tümleşik tek sayfa uygulaması tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="611f0-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="611f0-166">Şimdi, bir paketi alın.</span><span class="sxs-lookup"><span data-stu-id="611f0-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="611f0-167">Kullanıcıların kimliğini doğrulamak, güvenli bir şekilde arka uç Openıd Connect kullanarak REST API çağrısı ve kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="611f0-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="611f0-168">Kutudan çıktığında, kişisel bir Microsoft Account veya Azure AD'den bir iş/Okul hesabı olan herhangi bir kullanıcı destekler.</span><span class="sxs-lookup"><span data-stu-id="611f0-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="611f0-169">Uygulamayı çalıştırın ve bir tarayıcıda gidin `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="611f0-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span></span>  <span data-ttu-id="611f0-170">Kişisel bir Microsoft hesabı veya iş/Okul hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="611f0-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="611f0-171">Görevler kullanıcının yapılacaklar listesine ekleyin ve oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="611f0-171">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="611f0-172">Hesap diğer bir tür oturum açmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="611f0-172">Try signing in with the other type of account.</span></span> <span data-ttu-id="611f0-173">İş/Okul kullanıcıları oluşturmak için Azure AD kiracısı gerekiyorsa [edinebileceğinizi öğrenin burada](active-directory-howto-tenant.md) (boş).</span><span class="sxs-lookup"><span data-stu-id="611f0-173">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="611f0-174">V2.0 uç noktası hakkında bilgi almaya devam etmek için head dön bizim [v2.0 Geliştirici Kılavuzu](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="611f0-174">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="611f0-175">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="611f0-175">For additional resources, check out:</span></span>

* [<span data-ttu-id="611f0-176">Azure-Samples github'da >></span><span class="sxs-lookup"><span data-stu-id="611f0-176">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="611f0-177">Yığın taşması üzerinde Azure AD >></span><span class="sxs-lookup"><span data-stu-id="611f0-177">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="611f0-178">Azure AD belgelerinde bulunan [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="611f0-178">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="611f0-179">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="611f0-179">Get security updates for our products</span></span>
<span data-ttu-id="611f0-180">[Bu sayfayı](https://technet.microsoft.com/security/dd252948) ziyaret ederek ve Güvenlik Önerisi Uyarılarına abone olarak güvenlik olaylarının ne zaman ortaya çıkacağı hakkında bildirimleri almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="611f0-180">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

