---
title: "aaaAzure AD v2.0 .NET web uygulaması arama API Başlarken | Microsoft Docs"
description: "Nasıl toobuild çağıran bir .NET MVC Web uygulaması web hizmetlerini kullanarak kişisel Microsoft hesapları ve iş veya Okul hesapları için oturum açma."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 56be906e-71de-469d-9a5c-9fc08aae4223
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 1a70791418bc2a7d1fdfbafb9b5126a033a32292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a>Bir .NET web uygulamasından web API'si çağırma
Hızlı bir şekilde Hello v2.0 uç noktası ile kimlik doğrulaması tooyour web uygulamaları ekleyin ve hem kişisel Microsoft hesapları için destek ve iş veya Okul hesaplarıyla API web.  Burada, biz Openıd Connect, Microsoft'un OWIN ara yazılımı için biraz Yardım ile kullanarak kullanıcılar oturum açtığında bir MVC web uygulaması oluşturma.  Merhaba web uygulaması web API'si OAuth 2.0 tarafından sağlayan güvenli oluşturma için OAuth 2.0 erişim belirteçleri almak, okuma ve belirli kullanıcının "Yapılacaklar listesi üzerinde" silin.

Bu öğretici odaklanmak öncelikle MSAL tooacquire kullanarak ve tam olarak tanımlanan bir web uygulamasında erişim belirteçleri kullanın [burada](active-directory-v2-flows.md#web-apps).  Önkoşul olarak isteyebilirsiniz toofirst öğrenin nasıl çok[oturum açma temel tooa web uygulaması ekleme](active-directory-v2-devquickstarts-dotnet-web.md) veya nasıl çok[düzgün bir web API güvenliğini](active-directory-v2-devquickstarts-dotnet-api.md).

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

## <a name="download-sample-code"></a>Örnek kodu indirin
Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).  yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

Alternatif olarak, [tamamlandı hello uygulama .zip olarak karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ya da kopyalama tamamlandı hello uygulama:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a>Bir uygulamayı kaydetme
En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).  Emin olun:

* Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.
* Oluşturma bir **uygulama gizli anahtarı** Merhaba, **parola** türü ve değeri için daha sonra kopyalayın
* Merhaba eklemek **Web** uygulamanız için platform.
* Merhaba doğru girin **yeniden yönlendirme URI'si**. Merhaba yeniden yönlendirme URI'si gösterir hello varsayılan Bu öğretici için burada kimlik doğrulama yanıtları yönlendirileceğini - tooAzure AD `https://localhost:44326/`.

## <a name="install-owin"></a>OWIN yükleme
Merhaba OWIN ara yazılımı NuGet paketleri toohello ekleme `TodoList-WebApp` hello Paket Yöneticisi konsolu kullanarak projesi.  Merhaba OWIN ara yazılımı kullanılan tooissue oturum açma ve oturum kapatma isteklerini olması, hello kullanıcının oturumunu yönetmek ve başka şeyler arasında hello kullanıcı hakkında bilgi alın.

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a>Merhaba kullanıcı olarak oturum açın
Şimdi hello OWIN ara yazılımı toouse hello yapılandırmak [Openıd Connect kimlik doğrulama protokolü](active-directory-v2-protocols.md).  

* Açık hello `web.config` hello hello kökündeki dosyasında `TodoList-WebApp` proje ve hello uygulamanızın yapılandırma değerlerini girin `<appSettings>` bölümü.
  * Merhaba `ida:ClientId` hello olan **uygulama kimliği** tooyour uygulama hello kayıt Portalı'nda atanmış.
  * Merhaba `ida:ClientSecret` hello olan **uygulama gizli anahtarı** hello kayıt Portalı'nda oluşturulan.
  * Merhaba `ida:RedirectUri` hello olan **yeniden yönlendirme URI'si** hello portalda girdiğiniz.
* Açık hello `web.config` hello hello kökündeki dosyasında `TodoList-Service` proje ve hello yerine `ida:Audience` ile aynı hello **uygulama kimliği** olarak yukarıdaki.
* Açık hello dosya `App_Start\Startup.Auth.cs` ve ekleme `using` deyimleri üstten hello kitaplıkları için.
* Buna Merhaba aynı dosya, hello uygulamak `ConfigureAuth(...)` yöntemi.  Merhaba, sağladığınız parametreler `OpenIDConnectAuthenticationOptions` , uygulama toocommunicate Azure AD ile koordinatları olarak hizmet verecektir.

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
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // hello `AuthorizationCodeReceived` notification is used toocapture and redeem hello authorization_code that hello v2.0 endpoint returns tooyour app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-tooget-access-tokens"></a>MSAL tooget erişim belirteçleri kullanın
Merhaba, `AuthorizationCodeReceived` bildirim, toouse istiyoruz [Openıd Connect ile OAuth 2.0 art arda](active-directory-v2-protocols.md) tooredeem hello authorization_code bir erişim belirteci toohello Yapılacaklar listesi hizmeti için.  MSAL bu işlemi sizin için kolaylaştırır:

* İlk olarak, MSAL hello önizleme sürümünü yükleyin:

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* Ve başka bir tane eklemek `using` deyimi toohello `App_Start\Startup.Auth.cs` MSAL dosyası.
* Şimdi yeni bir yöntemi, hello eklemek `OnAuthorizationCodeReceived` olay işleyicisi.  Bu işleyici MSAL tooacquire bir erişim belirteci toohello Yapılacaklar listesi API kullanır ve hello belirteci MSAL'ın belirteci önbelleğinde daha sonrası için depolar:

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* Web uygulamalarında MSAL kullanılan toostore belirteçleri olabilecek genişletilebilir bir belirteç önbelleğe sahiptir.  Bu örnek hello uygulayan `NaiveSessionCache` http oturumu depolama toocache belirteçlerini kullanır.

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a>Merhaba Web API çağrısı
Artık tooactually 3. adımda aldığınız hello access_token kullanışınızda durumdadır.  Açık hello web uygulamanızın `Controllers\TodoListController.cs` dosya, toohello Yapılacaklar listesi API istekleri, tüm hello CRUD yapar.

* MSAL kullanabileceğiniz yeniden toofetch access_tokens gelen MSAL önbellek burada hello.  İlk olarak, ekleyin bir `using` MSAL toothis dosya bildirimi.
  
    `using Microsoft.Identity.Client;`
* Merhaba, `Index` eylemin, kullanım MSAL `AcquireTokenSilentAsync` yöntemi tooget hello Yapılacaklar listesi hizmet kullanılan tooread verilerden olabilir bir access_token:

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using hello web app's clientId as hello scope, since hello web app and service share hello same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* Merhaba örnek sonra sonuçta elde edilen belirteci toohello HTTP GET isteği hello hello ekler `Authorization` hangi hello Yapılacaklar listesi hizmetinin kullandığı tooauthenticate hello isteği üstbilgisi.
* Merhaba Yapılacaklar listesi hizmet döndürürse bir `401 Unauthorized` yanıtı hello access_tokens MSAL içinde geçersiz hale herhangi bir nedenden dolayı.  Bu durumda, tüm access_tokens MSAL önbellek hello bırakın ve yeniden hangi hello belirteç edinme akışı yeniden başlatılacak içinde toosign gerekebilir bir ileti hello kullanıcı Göster gerekir.

```C#
// ...
// If hello call failed with access denied, then drop hello current access token from hello cache,
// and show hello user an error indicating they might need toosign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need toosign in again.");
}
// ...
```

* Benzer şekilde, MSAL herhangi bir nedenle yüklenemiyor tooreturn bir access_token ise, hello kullanıcı toosign yeniden istemeniz gerekir.  Bu herhangi bir yakalama olarak kadar basittir `MSALException`:

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* Merhaba tam aynı `AcquireTokenSilentAsync` çağrıdır hello implementd `Create` ve `Delete` eylemler.  Web uygulamalarında uygulamanızda gerektiğinde bu MSAL yöntemi tooget access_tokens kullanabilirsiniz.  MSAL alınırken, önbelleğe alma ve belirteçleri, yenileme ilgilenebilmek.

Son olarak, yapı ve uygulamanızı çalıştırın!  Microsoft Account veya bir Azure AD hesabının oturum açın ve hello kullanıcının kimliğini hello üst gezinti çubuğunda nasıl yansıtılır dikkat edin.  Ekleyin ve bazı öğeler hello kullanıcının Yapılacaklar listesinde OAuth 2.0 API güvenli toosee hello eylemini çağırır silin.  Artık bir web uygulaması ve web API, hem kullanıcıların hem kişisel hem de iş/Okul hesaplarını ile doğrulanabilir endüstri standardı protokoller üzerine kullanılarak güvenlik altına sahipsiniz.

Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).  

## <a name="next-steps"></a>Sonraki Adımlar
Ek kaynaklar için gözden geçirin:

* [Merhaba v2.0 Geliştirici Kılavuzu >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" etiketi >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Ürünlerimiz için güvenlik güncelleştirmelerini alma
Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.

