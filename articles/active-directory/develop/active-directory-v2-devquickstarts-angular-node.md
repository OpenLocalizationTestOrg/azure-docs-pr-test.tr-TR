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
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a>Oturum açma tooan AngularJS tek sayfalı uygulama - NodeJS Ekle
Bu makalede gücü Microsoft hesapları tooan AngularJS uygulaması hello Azure Active Directory v2.0 uç kullanarak oturum ekleyeceğiz. Merhaba v2.0 uç tooperform uygulamanızda tek bir tümleştirme etkinleştirin ve hem kişisel hem de iş/Okul hesapları olan kullanıcıların kimlik doğrulaması.

Bu örnek arka uç REST NodeJS içinde yazılmış ve Azure AD'den OAuth taşıyıcı belirteçlerini kullanarak güvenliği API görevleri depolayan basit bir Yapılacaklar listesi tek sayfa uygulamasıdır.  Merhaba AngularJS uygulama bizim açık kaynak JavaScript kimlik doğrulama kitaplığı kullanır [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle tüm oturum açma işlemine hello ve arama hello REST API için belirteçleri almak.  Merhaba aynı düzeni hello gibi uygulanan tooauthenticate tooother REST API'leri olabilir [Microsoft Graph](https://graph.microsoft.com) veya Azure Resource Manager API'leri hello.

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>İndir
başlatılan tooget gerekir toodownload & yükleme [node.js](https://nodejs.org).  Sonra kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) iskelet uygulama:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

Merhaba iskelet uygulama basit bir AngularJS uygulama için tüm hello Demirbaş kod içerir, ancak tüm hello kimlikle ilgili parçaları eksik.  Toofollow boyunca istemiyorsanız, bunun yerine, kopyalayabilir veya [karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) tamamlandı hello örnek.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a>Bir uygulamayı kaydetme
İlk olarak, bir uygulama hello oluşturmak [uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).  Emin olun:

* Merhaba eklemek **Web** uygulamanız için platform.
* Merhaba doğru girin **yeniden yönlendirme URI'si**. Bu örnek için Hello varsayılan değer `http://localhost:8080`.
* Merhaba bırakın **izin örtük akış** Etkin onay kutusu. 

Merhaba basılı kopya **uygulama kimliği** , atanan tooyour uygulama, kısa süre içinde gerekir. 

## <a name="install-adaljs"></a>Adal.js yükleyin
toostart, indirdiğiniz tooproject gidin ve adal.js yükleyin.  Varsa [bower](http://bower.io/) yüklüyse, bu komutu yalnızca çalıştırabilirsiniz.  Hiçbir bağımlılık sürümü uyuşmazlığı için yalnızca hello daha yüksek bir sürümü seçin.

```
bower install adal-angular#experimental
```

Alternatif olarak, el ile yükleyebileceğiniz [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) ve [angular.js adal](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Her iki dosyaları toohello ekleme `app/lib/adal-angular-experimental/dist` dizin.

Artık sık kullandığınız metin düzenleyicinizde Merhaba projeyi açın ve adal.js hello sayfa gövdesi hello sonunda yük:

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>REST API Hello ayarlayın
Ayarlamaları olsa da, get hello arka uç REST API çalışma olanak sağlar.  Bir komut istemi çalıştırarak tüm hello gerekli paketleri yüklemek (Merhaba en üst düzey hello proje dizininde olduğunuzdan emin olun):

```
npm install
```

Şimdi açmak `config.js` ve hello yerine `audience` değeri:

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

Merhaba REST API hello Açısal uygulamasından AJAX isteği aldığında bu değer toovalidate belirteçlerini kullanır.  Bu basit REST API'si veri bellek içi - böylece her zaman toostop hello sunucu depolar, önceden oluşturulmuş tüm görevler kaybedersiniz dikkat edin.

Tüm olan hello REST API nasıl çalıştığını ele toospend yapmamız hello zaman.  Ücretsiz toopoke hello kodda eşitleyerek ancak toolearn web API'leri Azure AD ile güvenli hale getirme hakkında daha fazla bilgi istiyorsanız, kullanıma [bu makalede](active-directory-v2-devquickstarts-node-api.md). 

## <a name="sign-users-in"></a>Kullanıcıların oturumunu açma
Bazı kimlik kodu toowrite zaman.  Zaten sorunsuz şekilde Açısal yönlendirme yöntemleriyle oynadığı bir AngularJS sağlayıcısı bu adal.js içeren fark etmiş olabilirsiniz.  Merhaba adal modülü toohello uygulama ekleyerek başlayın:

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

Merhaba şimdi başlatabilir `adalProvider` uygulama kimliği:

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

Harika adal.js tüm hello bilgileri artık bunu toosecure, uygulama ve oturum kullanıcılarınızın gerekir.  Tüm sürdüğünü hello uygulamasında belirli bir rota için tooforce oturum açma bir kod satırı şöyledir:

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

Şimdi bir kullanıcı tıkladığında hello `TodoList` bağlantı adal.js otomatik olarak yeniden yönlendirme tooAzure için oturum açma gerekirse AD.  Oturum açma ve oturum kapatma isteklerini denetleyicilerinizi adal.js çağırarak açıkça gönderebilirsiniz:

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

## <a name="display-user-info"></a>Kullanıcı bilgilerini görüntüle
Merhaba kullanıcı oturumu açık, büyük olasılıkla, uygulamanızda tooaccess hello oturum açmış kullanıcının kimlik doğrulama verileri gerekir.  Adal.js hello sizin için bu bilgileri sunan `userInfo` nesnesi.  tooaccess görünümünde, bu nesnenin ilk adal.js toohello kök hello karşılık gelen denetleyicisi kapsamını ekleyin:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Merhaba doğrudan ele alabileceği sonra `userInfo` görünümünüzü nesnesinde: 

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

Merhaba de kullanabilirsiniz `userInfo` veya hello kullanıcı oturum açmışsa, toodetermine nesnesi.

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

## <a name="call-hello-rest-api"></a>Merhaba REST API çağrısı
Son olarak, bazı belirteçleri çağrısı REST API toocreate Merhaba, okuma, güncelleştirme ve görevleri silme zamanı tooget olur.  İyi ne tahmin?  Toodo yok *bir şey*.  Adal.js otomatik olarak ele alma, önbellekleme ve yenileme belirteçleri gerçekleştirir.  Bu ayrıca toooutgoing AJAX toohello REST API gönderdiğiniz istekleri konusu belirteçleri ekleme dikkatli olun.  

Bu tam olarak nasıl çalışır? Tüm teşekkürler toohello Sihirli biri olan [AngularJS dinleyiciler](https://docs.angularjs.org/api/ng/service/$http), giden ve gelen http iletileri adal.js tootransform sağlar.  Ayrıca, tüm istekleri toohello göndermek adal.js varsayar aynı etki alanında hello penceresi yönelik belirteçleri kullanması gereken şekilde hello aynı uygulama kimliği AngularJS uygulama hello gibi.  Merhaba kullandık bu yüzden aynı uygulama kimliği hem hello Açısal uygulama ve hello NodeJS REST API.  Doğal olarak, bu davranışı geçersiz kılabilir ve adal.js tooget belirteçleri diğer REST API'leri için gerekirse - söyleyin. ancak bu basit senaryoyu hello için varsayılanları yapar.

Ne kadar kolay taşıyıcı belirteçlerini Azure AD'den toosend istekleriyle olduğunu gösteren bir parçacığı aşağıda verilmiştir:

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

Tebrikler!  Azure AD tümleşik tek sayfa uygulaması tamamlanmıştır.  Şimdi, bir paketi alın.  Kullanıcıların kimliğini doğrulamak, güvenli bir şekilde arka uç Openıd Connect kullanarak REST API çağrısı ve hello kullanıcı hakkındaki temel bilgileri alın.  Merhaba kutudan çıktığında, kişisel bir Microsoft Account veya Azure AD'den bir iş/Okul hesabı olan herhangi bir kullanıcı destekler.  Merhaba uygulama, çalıştırarak bir deneyin:

```
node server.js
```

Bir tarayıcıda çok gidin`http://localhost:8080`.  Kişisel bir Microsoft hesabı veya iş/Okul hesabı kullanarak oturum açın.  Görevleri toohello kullanıcının yapılacaklar listesi ekleyin ve oturumu kapatın.  Try ile imzalama hello diğer hesap türü. Bir Azure AD Kiracı toocreate iş/Okul kullanıcıları gerekiyorsa [öğrenin nasıl tooget bir burada](active-directory-howto-tenant.md) (boş).

Merhaba hakkında öğrenme toocontinue v2.0 uç Merhaba, head geri tooour [v2.0 Geliştirici Kılavuzu](active-directory-appmodel-v2-overview.md).  Ek kaynaklar için gözden geçirin:

* [Azure-Samples github'da >>](https://github.com/Azure-Samples)
* [Yığın taşması üzerinde Azure AD >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Azure AD belgelerinde bulunan [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Ürünlerimiz için güvenlik güncelleştirmelerini alma
Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.

