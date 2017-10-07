---
title: "aaaAzure AD v2.0 .NET web uygulaması oturum Başlarken | Microsoft Docs"
description: "Nasıl toobuild .NET MVC Web uygulaması, kullanıcıların hem kişisel Microsoft Account oturum açtığında ve iş veya Okul hesapları."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c8b97ac6-0a06-4367-81b6-7d1d98152b14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 241e9c90bd752fbecc3696ce4f1bed3f9772189d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-net-mvc-web-app"></a>Oturum açma tooan .NET MVC web uygulaması Ekle
Merhaba v2.0 uç noktası ile kimlik doğrulaması tooyour web uygulamaları hem kişisel Microsoft hesapları için destek ve iş veya Okul hesapları ile kolayca ekleyebilirsiniz.  ASP.NET web uygulamalarında bunu .NET Framework 4. 5 ' dahil Microsoft'un OWIN ara yazılımı kullanarak gerçekleştirebilirsiniz.

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>
>

 Burada biz OWIN toosign hello kullanıcı, görüntü kullanan bir web uygulaması hello kullanıcı hakkında bazı bilgiler oluşturma ve hello uygulama dışı kullanıcı oturum hello.

## <a name="download"></a>İndir
Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).  yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

Tamamlanan hello uygulama hello de bu öğreticinin sonunda sağlanır.

## <a name="register-an-app"></a>Bir uygulamayı kaydetme
En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).  Emin olun:

* Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.
* Merhaba eklemek **Web** uygulamanız için platform.
* Merhaba doğru girin **yeniden yönlendirme URI'si**. Merhaba yeniden yönlendirme URI'si gösterir hello varsayılan Bu öğretici için burada kimlik doğrulama yanıtları yönlendirileceğini - tooAzure AD `https://localhost:44326/`.

## <a name="install--configure-owin-authentication"></a>Yükleme & OWIN kimlik doğrulamasını yapılandırma
Burada, biz hello OWIN ara yazılımı toouse hello Openıd Connect kimlik doğrulama protokolünü yapılandıracaksınız.  OWIN kullanılan tooissue oturum açma ve oturum kapatma isteklerini olması, hello kullanıcının oturumunu yönetmek ve başka şeyler arasında hello kullanıcı hakkında bilgi alın.

1. toobegin, açık hello `web.config` hello proje hello kökünde bulunan dosya ve hello uygulamanızın yapılandırma değerlerini girin `<appSettings>` bölümü.

  * Merhaba `ida:ClientId` hello olan **uygulama kimliği** tooyour uygulama hello kayıt Portalı'nda atanmış.
  * Merhaba `ida:RedirectUri` hello olan **yeniden yönlendirme URI'si** hello portalda girdiğiniz.

2. Ardından, hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello proje ekleyin.

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. "OWIN başlangıç sınıfı" toohello projesinde adlı Ekle `Startup.cs` sağ tıklatın hello projede--> **Ekle** --> **yeni öğe** "OWIN" arayın.  Merhaba OWIN ara yazılımı hello çağırılır `Configuration(...)` uygulamanız başladığında yöntemi.
4. Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup` -zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.  Merhaba, `Configuration(...)` yöntemi çağrısı tooConfigureAuth(...) tooset web uygulamanız için kimlik doğrulaması kurma olun  

        ```C#
        [assembly: OwinStartup(typeof(Startup))]
        
        namespace TodoList_WebApp
        {
            public partial class Startup
            {
                public void Configuration(IAppBuilder app)
                {
                    ConfigureAuth(app);
                }
            }
        }
        ```

5. Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(...)` yöntemi.  Merhaba, sağladığınız parametreler `OpenIdConnectAuthenticationOptions` , uygulama toocommunicate Azure AD ile koordinatları olarak hizmet verecektir.  Tanımlama bilgisi kimlik doğrulamasını oluşturan tooset ayrıca gerekir - hello Openıd Connect Ara hello kapsar altında tanımlama bilgilerini kullanır.

        ```C#
        public void ConfigureAuth(IAppBuilder app)
                     {
                             app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);
        
                             app.UseCookieAuthentication(new CookieAuthenticationOptions());
        
                             app.UseOpenIdConnectAuthentication(
                                     new OpenIdConnectAuthenticationOptions
                                     {
                                             // hello `Authority` represents hello v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                                             // hello `Scope` describes hello permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                                             // In a real application you could use issuer validation for additional checks, like making sure hello user's organization has signed up for your app, for instance.
        
                                             ClientId = clientId,
                                             Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0"),
                                             RedirectUri = redirectUri,
                                             Scope = "openid email profile",
                                             ResponseType = "id_token",
                                             PostLogoutRedirectUri = redirectUri,
                                             TokenValidationParameters = new TokenValidationParameters
                                             {
                                                     ValidateIssuer = false,
                                             },
                                             Notifications = new OpenIdConnectAuthenticationNotifications
                                             {
                                                     AuthenticationFailed = OnAuthenticationFailed,
                                             }
                                     });
                     }
        ```

## <a name="send-authentication-requests"></a>Kimlik doğrulama isteklerini gönderme
Uygulamanızı hello Openıd Connect kimlik doğrulama protokolünü kullanarak hello v2.0 uç noktası ile düzgün şekilde yapılandırılmış toocommunicate sunulmuştur.  OWIN geçen tüm kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumu koruyarak hello çirkin ayrıntılarını verdiğiniz.  Tüm bu kalır, kullanıcılarınızın toogive olan bir şekilde toosign ve oturum kapatma.

- Kullanabileceğiniz etiketleri yetkilendirmek, denetleyicileri toorequire, belirli bir sayfaya erişmeden önce oturum açtığında.  Açık `Controllers\HomeController.cs`ve hello ekleyin `[Authorize]` Denetleyicisi hakkında toohello etiketi.
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- OWIN toodirectly sorunu kimlik doğrulama isteklerini kodunuzu içinde de kullanabilirsiniz.  Açık `Controllers\AccountController.cs`.  Merhaba SignIn() ve SignOut() Eylemler, Openıd Connect sınama ve oturum kapatma isteklerini sırasıyla gönderin.

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with hello v2.0 endpoint is not yet supported.  Here, we just end hello session with hello web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- Şimdi, açmak `Views\Shared\_LoginPartial.cshtml`.  Bu, hello kullanıcı uygulamanızın oturum açma ve oturum kapatma bağlantıları göstermek ve bir görünümünde hello kullanıcının adını yazdırmak yerdir.

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves.*@
        
                        Hello, @(System.Security.Claims.ClaimsPrincipal.Current.FindFirst("preferred_username").Value)!
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

## <a name="display-user-information"></a>Kullanıcı bilgilerini görüntüleme
Openıd Connect ile kullanıcıların kimlik doğrulamasını yaparken, hello v2.0 uç talep veya onaylar hello kullanıcı hakkında içeren id_token toohello uygulama döndürür.  Bu talep toopersonalize uygulamanızı kullanabilirsiniz:

- Açık hello `Controllers\HomeController.cs` dosya.  Denetleyicilerinizi hello aracılığıyla hello kullanıcının talepleri erişebilmeniz için `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // hello object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // hello 'preferred_username' claim can be used for showing hello user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // hello subject or nameidentifier claim can be used toouniquely identify hello user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a>Çalıştırın
Son olarak, yapı ve uygulamanızı çalıştırın!   Kişisel bir Microsoft Account veya bir iş veya Okul hesabınızla oturum açın ve hello kullanıcının kimliğini hello üst gezinti çubuğunda nasıl yansıtılır dikkat edin.  Artık, hem kişisel hem de iş/Okul hesaplarını ile kullanıcıların kimliklerini doğrulayabilir endüstri standardı protokoller kullanılarak güvenli bir web uygulaması sahipsiniz.

Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a>Sonraki adımlar
Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.  Tootry isteyebilirsiniz:

[Merhaba hello v2.0 uç noktası ile bir Web API'SİNİN güvenliğini >>](active-directory-devquickstarts-webapi-dotnet.md)

Ek kaynaklar için gözden geçirin:

* [Merhaba v2.0 Geliştirici Kılavuzu >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" etiketi >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Ürünlerimiz için güvenlik güncelleştirmelerini alma
Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.
