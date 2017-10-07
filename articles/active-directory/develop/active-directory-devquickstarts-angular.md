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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>AngularJS tek sayfa uygulamaları Azure AD kullanarak korunmasına yardımcı olma

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) yapar, bunu, basit ve, tooadd oturum açma, oturum kapatma için kolay ve güvenli OAuth API tek sayfa uygulamaları tooyour çağırır.  Uygulamaları tooauthenticate Kullanıcılarınızla, Windows Server Active Directory hesaplarını sağlar ve tüm web Azure AD, Office 365 API'leri hello veya hello Azure API gibi korur API'si kullanabilir.

Bir tarayıcıda çalışan JavaScript uygulamaları için Azure AD hello sağlar. Active Directory Authentication Library (ADAL) ya da adal.js. Merhaba adal.js tek amacı toomake Bu, uygulama tooget erişim belirteçleri için kolay. toodemonstrate olduğu, ne kadar kolay burada size bir AngularJS tooDo listesi uygulaması, yapı:

* İşaretlerini hello kimlik sağlayıcısı Azure AD kullanarak toohello uygulamasında kullanıcı hello.

* Merhaba kullanıcı hakkındaki bazı bilgileri görüntüler.
* Güvenli bir şekilde Azure AD'den taşıyıcı belirteçlerini kullanarak uygulamanın tooDo listesi API çağrıları hello.
* İşaretlerini hello uygulama dışı kullanıcı hello.

toobuild hello eksiksiz, çalışan bir uygulama şunları yapmanız gerekir:

1. Uygulamanızı Azure AD ile kaydedin.
2. ADAL yükleyin ve hello tek sayfalı uygulama yapılandırın.
3. ADAL toohelp güvenli sayfaları hello tek sayfalı uygulama kullanma.

başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). Ayrıca kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir. Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>1. adım: Merhaba DirectorySearcher uygulamayı Kaydet
tooenable uygulama tooauthenticate kullanıcılar ve get belirteçleri, ilk gerek tooregister, Azure ad Kiracı:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Toomultiple dizinlerde kaydolduysanız hello doğru dizin görüntülemekte olduğunuz tooensure gerekebilir. toodo bu nedenle, hello üst çubuğunda tıklatın hesabınızı. Merhaba altında **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.
3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Merhaba komut istemlerini izleyin ve yeni web uygulaması ve/veya web API oluşturun:
  * **Ad** uygulama toousers açıklar.
  * **Yeniden yönlendirme URI'si** hello konumu toowhich Azure AD belirteçleri döndürecektir olduğu. Bu örnek Hello varsayılan konumu `https://localhost:44326/`.
6. Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği tooyour uygulama atar.  Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.
7. Adal.js Azure AD ile Merhaba OAuth örtük akış toocommunicate kullanır. Uygulamanız için hello örtük akış etkinleştirmeniz gerekir:
  1. Merhaba uygulaması tıklayın ve **bildirim** tooopen hello satır içi bildirim Düzenleyici.
  2. Merhaba bulun `oauth2AllowImplicitFlow` özelliği. Değerini çok ayarlama`true`.
  3. Tıklatın **kaydetmek** toosave hello bildirimi.
8. Uygulamanız için Kiracı arasında izinleri verin. Çok Git**ayarları** > **özellikleri** > **gerekli izinler**, hello tıklatıp **izinler**hello üst çubuğu düğmesini. Tıklatın **Evet** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>2. adım: Yükleme ADAL ve hello tek sayfalı uygulama yapılandırma
Azure AD'de bir uygulamanız varsa, adal.js yükleyin ve kimlikle ilgili kodunuzu yazın.

### <a name="configure-hello-javascript-client"></a>Merhaba JavaScript istemci yapılandırma
Merhaba Paket Yöneticisi konsolu kullanılarak adal.js toohello TodoSPA proje ekleyerek başlayın:
  1. Karşıdan [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) ve toohello ekleyin `App/Scripts/` proje dizini.
  2. Karşıdan [angular.js adal](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) ve toohello ekleyin `App/Scripts/` proje dizini.
  3. Her komut dosyası hello hello sonuna önce yük `</body>` içinde `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Merhaba arka uç sunucusu yapılandırın
Merhaba tarayıcısından Hello tek sayfalı uygulama arka uç tooDo listesi API tooaccept belirteçleri için hello arka uç hello uygulama kaydı hakkında yapılandırma bilgilerini gerekir. Merhaba TodoSPA projeyi açın `web.config`. Merhaba hello öğelerin Hello değerleri değiştirmek `<appSettings>` içinde kullanılan bölüm tooreflect hello değerleri hello Azure portalı. ADAL kullandığında kodunuzu bu değerleri başvurur.
  * `ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com Hello etki alanıdır.
  * `ida:Audience`Merhaba istemci uygulamanızın hello portalından kopyalandığından kimliğidir.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>3. adım: Kullanım ADAL toohelp güvenli sayfalarında hello tek sayfalı uygulama
Güvenli tek bir görünüm tek sayfalı uygulamanıza yardımcı olacak Adal.js AngularJS yolu ve HTTP sağlayıcıları ile tümleştirilir.

1. İçinde `App/Scripts/app.js`, hello adal.js modülünde getirin:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Initialize `adalProvider` hello yapılandırma değerlerini uygulama kaydınızı, da kullanarak `App/Scripts/app.js`:

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
3. Güvenli hello Yardım `TodoList` tek satırlık bir kod kullanarak hello uygulaması görünümünde: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Özet
Artık kullanıcılar oturum ve istekleri taşıyıcı belirteci korumalı tooits arka uç API'si sorun güvenli bir tek sayfalı uygulama vardır. Bir kullanıcı hello tıkladığında **TodoList** bağlantı adal.js otomatik olarak yeniden yönlendirme tooAzure için oturum açma gerekirse AD. Ayrıca, adal.js toohello uygulamanızın arka uç gönderilen Ajax istekleri bir erişim belirteci tooany otomatik olarak ekleyecek.  

Merhaba önceki hello tam minimum gerekli toobuild tek sayfalı uygulama adal.js kullanarak adımlardır. Ancak bazı özellikler tek sayfalı uygulama yararlıdır:

* tooexplicitly oturum açma ve oturum kapatma isteklerini vermek, adal.js çağırma denetleyicilerinizi içinde işlevler de tanımlayabilirsiniz.  İçinde `App/Scripts/homeCtrl.js`:

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
* Merhaba uygulamanın kullanıcı arabiriminde toopresent kullanıcı bilgilerini isteyebilirsiniz. Merhaba ADAL hizmet toohello zaten eklendi `userDataCtrl` hello erişebilmesi için denetleyici `userInfo` hello nesnesinde ilişkili Görünüm `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Veya hello kullanıcı oturum açmışsa, tooknow istediğiniz neden birçok senaryo vardır. Merhaba de kullanabilirsiniz `userInfo` bu bilgileri toogather nesne.  Örneğin, `index.html`, her iki hello gösterebilir **oturum açma** veya **oturum kapatma** düğmesi dayalı kimlik doğrulama durumu:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Azure AD ile tümleşik tek sayfalı uygulama kullanıcıların kimliğini doğrulamak, güvenli bir şekilde arka uç OAuth 2.0 kullanarak çağırmayı ve hello kullanıcı hakkındaki temel bilgileri alın. Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur. TooDo listesi tek sayfalı uygulamanızı çalıştırma ve kullanıcılarla biri ile oturum açın. Görevleri toohello kullanıcının yapılacaklar listesi ekleme, oturumu kapatın ve yeniden oturum açın.

Adal.js uygulamanıza kolayca tooincorporate ortak kimlik özelliklerinin kolaylaştırır. Bu, tüm hello dirty çalışmasına sizin için mvc'deki: önbellek yönetimi, belirteçlerin süresinin ve daha fazlasını yenilemeyi bir oturum açma kullanıcı Arabirimi ile hello kullanıcı sunan OAuth protokol desteği.

Başvuru için (yapılandırma değerleriniz olmadan) tamamlandı hello örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Sonraki adımlar
Şimdi tooadditional senaryoları taşıyabilirsiniz. Tootry isteyebilirsiniz: [tek sayfalı uygulamasından CORS web API'si çağırma](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
