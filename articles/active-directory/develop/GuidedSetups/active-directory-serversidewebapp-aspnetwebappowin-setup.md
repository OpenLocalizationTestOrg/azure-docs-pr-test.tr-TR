---
title: aaaAzure AD v2 ASP.NET Web sunucusu Getting Started - Kurulumu | Microsoft Docs
description: "Microsoft oturum açma Openıd Connect standardını kullanan geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET çözümünü uygulama"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: eadc59666557e9cd294e6e99391001120579144c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Projenizin kurulumunu

Bu bölümde hello adımları tooinstall gösterir ve Openıd Connect kullanarak bir ASP.NET projede hello OWIN ara yazılımı üzerinden kimlik doğrulaması ardışık yapılandırın. 

> Toodownload, bunun yerine bu örnekte 's Visual Studio projesi tercih ediyorsunuz? [Bir proje indirme](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) ve toohello atla [yapılandırma adımı](#create-an-application-express) yürütmeden önce tooconfigure hello kod örneği.

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a>ASP.NET projesi oluşturma

> 1. Visual Studio'da:`File` > `New` > `Project`<br/>
> 2. Altında *Visual C# \Web*seçin `ASP.NET Web Application (.NET Framework)`.
> 3. Uygulamanızı adlandırın ve tıklayın *Tamam*
> 4. Seçin `Empty` ve select hello onay kutusunu tooadd `MVC` başvuruları
<!--end-collapse-->

## <a name="add-authentication-components"></a>Kimlik doğrulaması Bileşenleri Ekle

1. Visual Studio'da:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Ekleme *OWIN ara yazılımı NuGet paketlerini* hello Paket Yöneticisi konsolu penceresinde hello aşağıdakileri yazarak:

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a>Bu kitaplıklar hakkında

>Çoklu oturum tanımlama bilgisi tabanlı kimlik doğrulaması Openıd Connect kullanarak açma (SSO) Hello kitaplıkları yukarıdaki etkinleştirin. Kimlik doğrulama tamamlandıktan sonra hello kullanıcıyı temsil eden hello simge tooyour uygulama gönderilir, OWIN ara yazılımı bir oturum tanımlama bilgisi oluşturur. Merhaba kullanıcı tooretype gerekmez hello tarayıcı sonra bu tanımlama bilgisi sonraki isteklerde parolalarını kullanır, bu nedenle ve hiçbir ek doğrulama gereklidir.
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a>Merhaba kimlik doğrulaması ardışık düzenini yapılandırın
Merhaba aşağıdaki kullanılan toocreate bir OWIN ara yazılımı başlangıç sınıfı tooconfigure Openıd Connect kimlik doğrulamasını adımlardır. Bu sınıf, IIS işlemi başladığında otomatik olarak yürütülür.

> Projenizi yoksa, bir `Startup.cs` hello kök klasöründe dosyasında:<br/>
> 1. Merhaba projenin kök klasörü sağ tıklatın: >`Add` > `New Item...` > `OWIN Startup class`<br/>
> 2. Adlandırın`Startup.cs`

> OWIN başlangıç sınıfı ve değil bir standart C# sınıf hello sınıfı seçili olduğundan emin olun. Bu görürseniz denetleyerek doğrulayabilirsiniz `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` hello ad alanı üzerinde.


1. Ekleme *OWIN* ve *Microsoft.IdentityModel* çok başvuran`Startup.cs`:

```csharp
using Microsoft.Owin;
using Owin;
using Microsoft.IdentityModel.Protocols;
using Microsoft.Owin.Security;
using Microsoft.Owin.Security.Cookies;
using Microsoft.Owin.Security.OpenIdConnect;
using Microsoft.Owin.Security.Notifications;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Başlangıç sınıfı aşağıdaki hello kod ile değiştirin:
</li>
</ol>

```csharp
public class Startup
{        
    // hello Client ID is used by hello application toouniquely identify itself tooAzure AD.
    string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

    // RedirectUri is hello URL where hello user will be redirected tooafter they sign in.
    string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

    // Tenant is hello tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
    static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

    // Authority is hello URL for authority, composed by Azure Active Directory v2 endpoint and hello tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
    string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

    /// <summary>
    /// Configure OWIN toouse OpenIdConnect 
    /// </summary>
    /// <param name="app"></param>
    public void Configuration(IAppBuilder app)
    {
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Sets hello ClientId, authority, RedirectUri as obtained from web.config
                ClientId = clientId,
                Authority = authority,
                RedirectUri = redirectUri,
                // PostLogoutRedirectUri is hello page that users will be redirected tooafter sign-out. In this case, it is using hello home page
                PostLogoutRedirectUri = redirectUri,
                Scope = OpenIdConnectScopes.OpenIdProfile,
                // ResponseType is set toorequest hello id_token - which contains basic information about hello signed-in user
                ResponseType = OpenIdConnectResponseTypes.IdToken,
                // ValidateIssuer set toofalse tooallow personal and work accounts from any organization toosign in tooyour application
                // tooonly allow users from a single organizations, set ValidateIssuer tootrue and 'tenant' setting in web.config toohello tenant name
                // tooallow users from only a list of specific organizations, set ValidateIssuer tootrue and use ValidIssuers parameter 
                TokenValidationParameters = new System.IdentityModel.Tokens.TokenValidationParameters() { ValidateIssuer = false },
                // OpenIdConnectAuthenticationNotifications configures OWIN toosend notification of failed authentications tooOnAuthenticationFailed method
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    AuthenticationFailed = OnAuthenticationFailed
                }
            }
        );
    }

    /// <summary>
    /// Handle failed authentication requests by redirecting hello user toohello home page with an error in hello query string
    /// </summary>
    /// <param name="context"></param>
    /// <returns></returns>
    private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
    {
        context.HandleResponse();
        context.Response.Redirect("/?errormessage=" + context.Exception.Message);
        return Task.FromResult(0);
    }
}

```
<!--start-collapse-->
> ### <a name="more-information"></a>Daha Fazla Bilgi

> Merhaba, sağladığınız parametreler *OpenIDConnectAuthenticationOptions* hello uygulama toocommunicate Azure AD ile koordinatları olarak hizmet. Merhaba Openıd Connect Ara hello arka planda tanımlama bilgilerini kullandığından, ayrıca tanımlama bilgisi kimlik doğrulamasını oluşturan tooset gösterir yukarıdaki hello kodu olarak gerekir. Merhaba *Validateıssuer* değeri Openıdconnect söyler toonot erişim tooone belirli kuruluş kısıtlayın.
<!--end-collapse-->

