---
title: "Azure AD v2.0 NodeJS AngularJS tek sayfa uygulaması Başlarken | Microsoft Docs"
description: "Hem kişisel Microsoft hesabı olan kullanıcılar oturum açtığında bir Açısal JS tek sayfa uygulaması oluşturma ve iş veya Okul hesapları."
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
ms.openlocfilehash: 0e90171afd9c4c782fbb18375ab2d147497ef442
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="a27b5-103">Oturum açma bir AngularJS tek sayfalı uygulama için - NodeJS ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a27b5-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="a27b5-104">Bu makalede bir AngularJS uygulamasına Azure Active Directory v2.0 uç kullanarak oturum açın. desteklenen Microsoft hesapları ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="a27b5-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="a27b5-105">v2.0 uç noktası hem kişisel hem de iş/Okul hesapları olan kullanıcıların kimliğini doğrulamak ve uygulamanızda tek tümleştirme gerçekleştirmek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="a27b5-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="a27b5-106">Bu örnek arka uç REST NodeJS içinde yazılmış ve Azure AD'den OAuth taşıyıcı belirteçlerini kullanarak güvenliği API görevleri depolayan basit bir Yapılacaklar listesi tek sayfa uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a27b5-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="a27b5-107">AngularJS uygulama bizim açık kaynak JavaScript kimlik doğrulama kitaplığı kullanır [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) tüm oturum açma işlemine işlemek ve REST API çağırma belirteçleri almak için.</span><span class="sxs-lookup"><span data-stu-id="a27b5-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="a27b5-108">Aynı desende diğer REST API'leri gibi kimlik doğrulaması için uygulanabilir [Microsoft Graph](https://graph.microsoft.com) veya Azure Resource Manager API'leri.</span><span class="sxs-lookup"><span data-stu-id="a27b5-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="a27b5-109">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a27b5-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="a27b5-110">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a27b5-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="a27b5-111">İndir</span><span class="sxs-lookup"><span data-stu-id="a27b5-111">Download</span></span>
<span data-ttu-id="a27b5-112">Başlamak için indirme ve yükleme gerekir [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a27b5-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="a27b5-113">Sonra kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) iskelet uygulama:</span><span class="sxs-lookup"><span data-stu-id="a27b5-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="a27b5-114">İskelet uygulama basit bir AngularJS uygulama için tüm Demirbaş kod içerir, ancak kimlikle ilgili şey eksik.</span><span class="sxs-lookup"><span data-stu-id="a27b5-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="a27b5-115">Takip istemiyorsanız, bunun yerine, kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) tamamlanan örnek.</span><span class="sxs-lookup"><span data-stu-id="a27b5-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="a27b5-116">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="a27b5-116">Register an app</span></span>
<span data-ttu-id="a27b5-117">İlk olarak, bir uygulama oluşturun [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a27b5-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a27b5-118">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="a27b5-118">Make sure to:</span></span>

* <span data-ttu-id="a27b5-119">Ekleme **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="a27b5-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="a27b5-120">Doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="a27b5-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="a27b5-121">Bu örnek için varsayılan değer `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="a27b5-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="a27b5-122">Bırakın **izin örtük akış** Etkin onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="a27b5-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="a27b5-123">Aşağı kopyalama **uygulama kimliği** uygulamanıza atanan, kısa süre içinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="a27b5-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="a27b5-124">Adal.js yükleyin</span><span class="sxs-lookup"><span data-stu-id="a27b5-124">Install adal.js</span></span>
<span data-ttu-id="a27b5-125">Başlatmak için indirilen proje gidin ve adal.js yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a27b5-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="a27b5-126">Varsa [bower](http://bower.io/) yüklüyse, bu komutu yalnızca çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a27b5-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="a27b5-127">Hiçbir bağımlılık sürümü uyuşmazlığı için yalnızca daha yüksek sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="a27b5-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="a27b5-128">Alternatif olarak, el ile yükleyebileceğiniz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) ve [angular.js adal](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="a27b5-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="a27b5-129">Her iki dosyalarına ekleme `app/lib/adal-angular-experimental/dist` dizin.</span><span class="sxs-lookup"><span data-stu-id="a27b5-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="a27b5-130">Artık sık kullandığınız metin düzenleyicinizde projesini açın ve sayfa gövdesi sonunda adal.js yükleyin:</span><span class="sxs-lookup"><span data-stu-id="a27b5-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="a27b5-131">REST API ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a27b5-131">Set up the REST API</span></span>
<span data-ttu-id="a27b5-132">Ayarlamaları olsa da, arka uç REST API çalışabileceğiniz olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a27b5-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="a27b5-133">Bir komut istemi çalıştırarak tüm gerekli paketleri yüklemek (Proje en üst düzey dizininde olduğunuzdan emin olun):</span><span class="sxs-lookup"><span data-stu-id="a27b5-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="a27b5-134">Şimdi açmak `config.js` ve değiştirme `audience` değeri:</span><span class="sxs-lookup"><span data-stu-id="a27b5-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="a27b5-135">REST API AJAX isteği Açısal uygulamadan aldığı belirteçleri doğrulamak için bu değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="a27b5-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="a27b5-136">Bu basit REST API'si veri bellek içi - böylece her depolar Not sunucusunu durdurmak için saat, önceden oluşturulmuş tüm görevler kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="a27b5-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="a27b5-137">REST API nasıl çalıştığını ele harcamanız oluşturacağız her zaman olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a27b5-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="a27b5-138">Kodda karıştırın geçici bir çözüm, ancak Azure AD ile API'leri web güvenliğini sağlama hakkında daha fazla bilgi edinmek istiyorsanız kullanıma çekinmeyin [bu makalede](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="a27b5-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="a27b5-139">Kullanıcıların oturumunu açma</span><span class="sxs-lookup"><span data-stu-id="a27b5-139">Sign users in</span></span>
<span data-ttu-id="a27b5-140">Bazı kimlik kod yazma süresi.</span><span class="sxs-lookup"><span data-stu-id="a27b5-140">Time to write some identity code.</span></span>  <span data-ttu-id="a27b5-141">Zaten sorunsuz şekilde Açısal yönlendirme yöntemleriyle oynadığı bir AngularJS sağlayıcısı bu adal.js içeren fark etmiş olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a27b5-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="a27b5-142">Uygulama adal modülü ekleyerek başlayın:</span><span class="sxs-lookup"><span data-stu-id="a27b5-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="a27b5-143">Şimdi başlatabilir `adalProvider` uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="a27b5-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="a27b5-144">Harika, artık adal.js uygulamanızı güvenli ve kullanıcılar oturum açmak için gerekli tüm bilgilere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a27b5-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="a27b5-145">Uygulamasında belirli bir rota için oturum açma zorlamak için gereken tek şey bir kod satırı:</span><span class="sxs-lookup"><span data-stu-id="a27b5-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="a27b5-146">Şimdi bir kullanıcı tıkladığında `TodoList` bağlantı adal.js otomatik olarak yeniden yönlendirme oturum açma için Azure ad gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="a27b5-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="a27b5-147">Oturum açma ve oturum kapatma isteklerini denetleyicilerinizi adal.js çağırarak açıkça gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a27b5-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="a27b5-148">Kullanıcı bilgilerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="a27b5-148">Display user info</span></span>
<span data-ttu-id="a27b5-149">Kullanıcının oturum açtığı, uygulamanızda oturum açmış kullanıcının kimlik doğrulaması veri erişim gerekecek.</span><span class="sxs-lookup"><span data-stu-id="a27b5-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="a27b5-150">Adal.js gösterir bu bilgileri `userInfo` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a27b5-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="a27b5-151">Bu nesne bir görünümde erişmek için ilk adal.js karşılık gelen denetleyicisi kök kapsamını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a27b5-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="a27b5-152">Doğrudan ele alabileceği sonra `userInfo` görünümünüzü nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="a27b5-152">Then you can directly address the `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="a27b5-153">Aynı zamanda `userInfo` kullanıcı veya oturum varsa belirlemek için nesne.</span><span class="sxs-lookup"><span data-stu-id="a27b5-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

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

## <a name="call-the-rest-api"></a><span data-ttu-id="a27b5-154">REST API çağrısı</span><span class="sxs-lookup"><span data-stu-id="a27b5-154">Call the REST API</span></span>
<span data-ttu-id="a27b5-155">Son olarak, bazı belirteçleri almak ve oluşturma, okuma, güncelleştirme için REST API çağrısı ve görevleri silme zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="a27b5-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="a27b5-156">İyi ne tahmin?</span><span class="sxs-lookup"><span data-stu-id="a27b5-156">Well guess what?</span></span>  <span data-ttu-id="a27b5-157">Yapmanıza gerek yoktur *bir şey*.</span><span class="sxs-lookup"><span data-stu-id="a27b5-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="a27b5-158">Adal.js otomatik olarak ele alma, önbellekleme ve yenileme belirteçleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a27b5-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="a27b5-159">Bu ayrıca REST API'sine gönderdiğiniz giden AJAX istekleri için bu simgeleri ekleme dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="a27b5-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="a27b5-160">Bu tam olarak nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="a27b5-160">How exactly does this work?</span></span> <span data-ttu-id="a27b5-161">Sihirli sayesinde tümü olduğu [AngularJS dinleyiciler](https://docs.angularjs.org/api/ng/service/$http), giden ve gelen http iletileri dönüştürmek adal.js izin verir.</span><span class="sxs-lookup"><span data-stu-id="a27b5-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="a27b5-162">Ayrıca, adal.js penceresi AngularJS uygulama aynı uygulama Kimliğine yönelik belirteçleri kullanması gereken gibi tüm istekler aynı etki alanına göndermek varsayar.</span><span class="sxs-lookup"><span data-stu-id="a27b5-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="a27b5-163">Aynı uygulama kimliği hem Açısal uygulama ve NodeJS REST API kullandık nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="a27b5-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="a27b5-164">Elbette, bu davranışı geçersiz kılabilir ve diğer REST API'leri için gerekirse - belirteçleri almak için adal.js söyleyin ancak basit bu senaryo için varsayılanları yapar.</span><span class="sxs-lookup"><span data-stu-id="a27b5-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="a27b5-165">Azure AD'den taşıyıcı belirteçlerini istekleri göndermek için ne kadar kolay olduğunu gösteren bir parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a27b5-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="a27b5-166">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a27b5-166">Congratulations!</span></span>  <span data-ttu-id="a27b5-167">Azure AD tümleşik tek sayfa uygulaması tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a27b5-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="a27b5-168">Şimdi, bir paketi alın.</span><span class="sxs-lookup"><span data-stu-id="a27b5-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="a27b5-169">Kullanıcıların kimliğini doğrulamak, güvenli bir şekilde arka uç Openıd Connect kullanarak REST API çağrısı ve kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="a27b5-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="a27b5-170">Kutudan çıktığında, kişisel bir Microsoft Account veya Azure AD'den bir iş/Okul hesabı olan herhangi bir kullanıcı destekler.</span><span class="sxs-lookup"><span data-stu-id="a27b5-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="a27b5-171">Uygulama, çalıştırarak bir deneyin:</span><span class="sxs-lookup"><span data-stu-id="a27b5-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="a27b5-172">Bir tarayıcıda gidin `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="a27b5-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="a27b5-173">Kişisel bir Microsoft hesabı veya iş/Okul hesabı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a27b5-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="a27b5-174">Görevler kullanıcının yapılacaklar listesine ekleyin ve oturumu kapatın.</span><span class="sxs-lookup"><span data-stu-id="a27b5-174">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="a27b5-175">Hesap diğer bir tür oturum açmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="a27b5-175">Try signing in with the other type of account.</span></span> <span data-ttu-id="a27b5-176">İş/Okul kullanıcıları oluşturmak için Azure AD kiracısı gerekiyorsa [edinebileceğinizi öğrenin burada](active-directory-howto-tenant.md) (boş).</span><span class="sxs-lookup"><span data-stu-id="a27b5-176">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="a27b5-177">Hakkında bilgi almaya devam etmek için geri baş v2.0 uç bizim [v2.0 Geliştirici Kılavuzu](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a27b5-177">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="a27b5-178">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="a27b5-178">For additional resources, check out:</span></span>

* [<span data-ttu-id="a27b5-179">Azure-Samples github'da >></span><span class="sxs-lookup"><span data-stu-id="a27b5-179">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="a27b5-180">Yığın taşması üzerinde Azure AD >></span><span class="sxs-lookup"><span data-stu-id="a27b5-180">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="a27b5-181">Azure AD belgelerinde bulunan [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="a27b5-181">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a27b5-182">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="a27b5-182">Get security updates for our products</span></span>
<span data-ttu-id="a27b5-183">[Bu sayfayı](https://technet.microsoft.com/security/dd252948) ziyaret ederek ve Güvenlik Önerisi Uyarılarına abone olarak güvenlik olaylarının ne zaman ortaya çıkacağı hakkında bildirimleri almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a27b5-183">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

