---
title: "Başlarken aaaAzure AD .NET web uygulaması | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleşen bir .NET MVC web uygulaması oluşturun."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a>ASP.NET web uygulaması oturum açma ve Azure AD ile oturum kapatma
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Yalnızca birkaç kod satırıyla, tek bir oturum açma ve oturum kapatma sağlayarak, Azure Active Directory (Azure AD), toooutsource web uygulaması için kimlik yönetimi basit kolaylaştırır. ASP.NET web uygulamaları ve kullanıcıların .NET (OWIN) ara yazılımı için açık Web arabirimi Microsoft uyarlamasını hello kullanarak oturum. OWIN ara yazılımı topluluk odaklı .NET Framework 4. 5 ' bulunur. Bu makalede gösterilmektedir nasıl toouse OWIN için:

* Kullanıcıların tooweb uygulamalarda hello kimlik sağlayıcısı Azure AD kullanarak oturum açın.
* Bazı kullanıcı bilgileri görüntüler.
* Merhaba uygulamaları dışında kullanıcılar oturum açın.

## <a name="before-you-get-started"></a>Başlamadan önce
* Merhaba karşıdan [uygulama çatıyı](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) veya hello indirme [tamamlanan örnek](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).
* Ayrıca hangi tooregister hello uygulamasında Azure AD kiracısı gerekir. Azure AD kiracısı, zaten yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

Hazır olduğunuzda İleri dört bölüm izleyin hello yordamlarda hello.

## <a name="step-1-register-hello-new-app-with-azure-ad"></a>1. adım: Azure AD ile Merhaba yeni uygulamayı Kaydet
Merhaba uygulama tooauthenticate kullanıcıları tooset ilk kaydedin, kiracınızda hello aşağıdakileri yaparak:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst çubuğunda hesabınızın adını tıklatın. Merhaba altında **Directory** listesi, tooregister hello uygulama istediğiniz select hello Active Directory kiracısı.
3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. İzleyin hello ister yeni bir toocreate **Web uygulaması ve/veya Webapı**.
  * **Ad** hello uygulama toousers açıklar.
  * **Oturum açma URL'si** hello hello uygulamasının temel URL'si. Merhaba çatıyı'nın varsayılan URL'dir https://localhost:44320 /.
6. Merhaba kaydı tamamladıktan sonra Azure AD hello uygulama benzersiz uygulama kimliği atar. Merhaba uygulama sayfası toouse hello sonraki bölümlerde Hello değerini kopyalayın.
7. Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin. Merhaba **uygulama kimliği URI'si** hello uygulama için benzersiz bir tanımlayıcıdır. Merhaba adlandırma kuralı olan `https://<tenant-domain>/<app-name>` (örneğin, `https://contoso.onmicrosoft.com/my-first-aad-app`).

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>2. adım: hello uygulama toouse hello OWIN kimlik doğrulaması ardışık ayarlayın
Bu adımda, hello OWIN ara yazılımı toouse hello Openıd Connect kimlik doğrulama protokolü yapılandırın. OWIN tooissue oturum açma ve oturum kapatma isteklerini kullanın, kullanıcı oturumlarını yönetmek, kullanıcı bilgilerini almak ve benzeri.

1. toobegin, hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello projesi ekleyin.

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. OWIN başlangıç sınıfı toohello projesinde adlı tooadd `Startup.cs`, hello projesine sağ tıklayın, seçin **Ekle**seçin **yeni öğe**, arayın ve sonra **OWIN**. Merhaba OWIN ara yazılımı çağırır hello **Configuration(...)**  hello uygulama başlatıldığında yöntemi.
3. Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup`. Zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık. Merhaba, **Configuration(...)**  yöntemi, çok çağırmaya**ConfgureAuth(...)**  tooset hello uygulaması için kimlik doğrulama ayarlama.  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. Merhaba App_Start\Startup.Auth.cs dosyasını açın ve ardından hello uygulamak **ConfigureAuth(...)**  yöntemi. Merhaba, sağladığınız parametreler *OpenIDConnectAuthenticationOptions* hello uygulama toocommunicate Azure AD ile koordinatları olarak hizmet. Merhaba Openıd Connect Ara hello arka planda tanımlama bilgileri kullandığından tooset tanımlama bilgisi kimlik doğrulamasını ayarlamak da gerekir.

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. Merhaba hello proje kök dizininde hello web.config dosyasını açın ve ardından hello hello yapılandırma değerlerini girin `<appSettings>` bölümü.
  * `ida:ClientId`: hello Azure portalında hello kopyalanan GUID "1. adım: kayıt hello Azure AD ile yeni bir uygulaması."
  * `ida:Tenant`: Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) hello adı.
  * `ida:PostLogoutRedirectUri`: bir kullanıcı oturum kapatma isteği başarıyla tamamlandıktan sonra burada yönlendirilmesi gereken Azure AD söyler hello göstergesi.

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>3. adım: Kullanma OWIN tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD
Merhaba uygulama Azure AD ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur. OWIN tüm kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumlarını koruma hello ayrıntıları ele. Tüm bu kalır, kullanıcılarınızın toogive olan bir şekilde toosign ve oturum kapatma.

1. Kullanabileceğiniz belirli sayfalarını erişmeden önce denetleyicileri toorequire kullanıcılar toosign içinde etiketlerinde yetkilendirin. toodo, Controllers\HomeController.cs açın ve ardından hello ekleyin `[Authorize]` Denetleyicisi hakkında toohello etiketi.

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. OWIN toodirectly sorunu kimlik doğrulama isteklerini kodunuzu içinde de kullanabilirsiniz. toodo, bu nedenle, Controllers\AccountController.cs açın. Ardından, Openıd Connect sınama ve oturum kapatma isteklerini hello SignIn() ve SignOut() Eylemler gönderin.

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. Görünümler/paylaşılan açmak\_LoginPartial.cshtml tooshow hello kullanıcı hello uygulama oturum açma ve oturum kapatma bağlantılar ve tooprint hello kullanıcının adını görünümünde çıkışı.

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
             </li>
             <li>
                 @Html.ActionLink("Sign out", "SignOut", "Account")
             </li>
         </ul>
     </text>
    }
    else
    {
     <ul class="nav navbar-nav navbar-right">
         <li>@Html.ActionLink("Sign in", "SignIn", "Account", routeValues: null, htmlAttributes: new { id = "loginLink" })</li>
     </ul>
    }
    ```

## <a name="step-4-display-user-information"></a>4. adım: kullanıcı bilgilerini görüntüleme
Openıd Connect ile kullanıcıların kimliğini doğrular, Azure AD "talep" ya da hello kullanıcı hakkında onaylar içeren id_token toohello uygulama döndürür. Merhaba aşağıdakileri yaparak bu talepler toopersonalize hello uygulamasını kullanarak şunları yapabilirsiniz:

1. Merhaba Controllers\HomeController.cs dosyasını açın. Denetleyicilerinizi hello aracılığıyla hello kullanıcının talepleri erişebilmeniz için `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. Derleme ve hello uygulamayı çalıştırın. Kiracınızda onmicrosoft.com etki alanı ile yeni bir kullanıcı zaten oluşturmadıysanız hello zaman toodo şekilde sunulmuştur. Bunu yapmak için:

  a. Oturum, kullanıcı oturum açabilir ve hello kullanıcının kimliğini hello üst çubuğunda nasıl yansıtılır not edin.

  b. Oturumu kapatın ve kiracınızda başka bir kullanıcı olarak yeniden oturum açın.

  c. Özellikle hırslı hissediyorsanız kaydetmek ve bu uygulamayla (kendi ClientID) başka bir örneğini çalıştıran ve çoklu oturum açma eylem izleyin.

## <a name="next-steps"></a>Sonraki adımlar
Başvuru için bkz: [tamamlandı hello örnek](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (yapılandırma değerleriniz olmadan).

Gelişmiş konular toomore üzerinde şimdi taşıyabilirsiniz. Örneğin, [Azure AD ile Web API güvenliğini](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
