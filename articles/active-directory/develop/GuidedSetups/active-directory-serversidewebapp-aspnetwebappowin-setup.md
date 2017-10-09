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
## <a name="set-up-your-project"></a><span data-ttu-id="1dbca-103">Projenizin kurulumunu</span><span class="sxs-lookup"><span data-stu-id="1dbca-103">Set up your project</span></span>

<span data-ttu-id="1dbca-104">Bu bölümde hello adımları tooinstall gösterir ve Openıd Connect kullanarak bir ASP.NET projede hello OWIN ara yazılımı üzerinden kimlik doğrulaması ardışık yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1dbca-104">This section shows hello steps tooinstall and configure hello authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="1dbca-105">Toodownload, bunun yerine bu örnekte 's Visual Studio projesi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="1dbca-105">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="1dbca-106">[Bir proje indirme](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) ve toohello atla [yapılandırma adımı](#create-an-application-express) yürütmeden önce tooconfigure hello kod örneği.</span><span class="sxs-lookup"><span data-stu-id="1dbca-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>

<!--start-collapse-->
> ### <a name="create-your-aspnet-project"></a><span data-ttu-id="1dbca-107">ASP.NET projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1dbca-107">Create your ASP.NET project</span></span>

> 1. <span data-ttu-id="1dbca-108">Visual Studio'da:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="1dbca-108">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
> 2. <span data-ttu-id="1dbca-109">Altında *Visual C# \Web*seçin `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="1dbca-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
> 3. <span data-ttu-id="1dbca-110">Uygulamanızı adlandırın ve tıklayın *Tamam*</span><span class="sxs-lookup"><span data-stu-id="1dbca-110">Name your application and click *OK*</span></span>
> 4. <span data-ttu-id="1dbca-111">Seçin `Empty` ve select hello onay kutusunu tooadd `MVC` başvuruları</span><span class="sxs-lookup"><span data-stu-id="1dbca-111">Select `Empty` and select hello checkbox tooadd `MVC` references</span></span>
<!--end-collapse-->

## <a name="add-authentication-components"></a><span data-ttu-id="1dbca-112">Kimlik doğrulaması Bileşenleri Ekle</span><span class="sxs-lookup"><span data-stu-id="1dbca-112">Add authentication components</span></span>

1. <span data-ttu-id="1dbca-113">Visual Studio'da:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="1dbca-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="1dbca-114">Ekleme *OWIN ara yazılımı NuGet paketlerini* hello Paket Yöneticisi konsolu penceresinde hello aşağıdakileri yazarak:</span><span class="sxs-lookup"><span data-stu-id="1dbca-114">Add *OWIN middleware NuGet packages* by typing hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Owin.Security.OpenIdConnect
Install-Package Microsoft.Owin.Security.Cookies
Install-Package Microsoft.Owin.Host.SystemWeb
```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="1dbca-115">Bu kitaplıklar hakkında</span><span class="sxs-lookup"><span data-stu-id="1dbca-115">About these libraries</span></span>

><span data-ttu-id="1dbca-116">Çoklu oturum tanımlama bilgisi tabanlı kimlik doğrulaması Openıd Connect kullanarak açma (SSO) Hello kitaplıkları yukarıdaki etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1dbca-116">hello libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="1dbca-117">Kimlik doğrulama tamamlandıktan sonra hello kullanıcıyı temsil eden hello simge tooyour uygulama gönderilir, OWIN ara yazılımı bir oturum tanımlama bilgisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1dbca-117">After authentication is completed and hello token representing hello user is sent tooyour application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="1dbca-118">Merhaba kullanıcı tooretype gerekmez hello tarayıcı sonra bu tanımlama bilgisi sonraki isteklerde parolalarını kullanır, bu nedenle ve hiçbir ek doğrulama gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1dbca-118">hello browser then uses this cookie on subsequent requests so hello user doesn't need tooretype their password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-hello-authentication-pipeline"></a><span data-ttu-id="1dbca-119">Merhaba kimlik doğrulaması ardışık düzenini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1dbca-119">Configure hello authentication pipeline</span></span>
<span data-ttu-id="1dbca-120">Merhaba aşağıdaki kullanılan toocreate bir OWIN ara yazılımı başlangıç sınıfı tooconfigure Openıd Connect kimlik doğrulamasını adımlardır.</span><span class="sxs-lookup"><span data-stu-id="1dbca-120">hello steps below are used toocreate an OWIN middleware Startup Class tooconfigure OpenID Connect authentication.</span></span> <span data-ttu-id="1dbca-121">Bu sınıf, IIS işlemi başladığında otomatik olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="1dbca-121">This class will be executed automatically when your IIS process starts.</span></span>

> <span data-ttu-id="1dbca-122">Projenizi yoksa, bir `Startup.cs` hello kök klasöründe dosyasında:</span><span class="sxs-lookup"><span data-stu-id="1dbca-122">If your project doesn't have a `Startup.cs` file in hello root folder:</span></span><br/>
> 1. <span data-ttu-id="1dbca-123">Merhaba projenin kök klasörü sağ tıklatın: >`Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="1dbca-123">Right click on hello project's root folder: >  `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="1dbca-124">Adlandırın`Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="1dbca-124">Name it `Startup.cs`</span></span>

> <span data-ttu-id="1dbca-125">OWIN başlangıç sınıfı ve değil bir standart C# sınıf hello sınıfı seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1dbca-125">Make sure hello class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="1dbca-126">Bu görürseniz denetleyerek doğrulayabilirsiniz `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` hello ad alanı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="1dbca-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above hello namespace.</span></span>


1. <span data-ttu-id="1dbca-127">Ekleme *OWIN* ve *Microsoft.IdentityModel* çok başvuran`Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="1dbca-127">Add *OWIN* and *Microsoft.IdentityModel* references too`Startup.cs`:</span></span>

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
<span data-ttu-id="1dbca-128">Başlangıç sınıfı aşağıdaki hello kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1dbca-128">Replace Startup class with hello code below:</span></span>
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
> ### <a name="more-information"></a><span data-ttu-id="1dbca-129">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="1dbca-129">More Information</span></span>

> <span data-ttu-id="1dbca-130">Merhaba, sağladığınız parametreler *OpenIDConnectAuthenticationOptions* hello uygulama toocommunicate Azure AD ile koordinatları olarak hizmet.</span><span class="sxs-lookup"><span data-stu-id="1dbca-130">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello application toocommunicate with Azure AD.</span></span> <span data-ttu-id="1dbca-131">Merhaba Openıd Connect Ara hello arka planda tanımlama bilgilerini kullandığından, ayrıca tanımlama bilgisi kimlik doğrulamasını oluşturan tooset gösterir yukarıdaki hello kodu olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="1dbca-131">Because hello OpenID Connect middleware uses cookies in hello background, you also need tooset up cookie authentication as hello code above shows.</span></span> <span data-ttu-id="1dbca-132">Merhaba *Validateıssuer* değeri Openıdconnect söyler toonot erişim tooone belirli kuruluş kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="1dbca-132">hello *ValidateIssuer* value tells OpenIdConnect toonot restrict access tooone specific organization.</span></span>
<!--end-collapse-->

