---
title: "Azure AD v2.0 .NET web uygulaması arama API Başlarken | Microsoft Docs"
description: "Kişisel Microsoft hesapları ve iş kullanarak bu çağrıları web .NET MVC Web uygulaması oluşturma hizmetleri veya Okul hesapları için oturum açma."
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
ms.openlocfilehash: dc3162ae8e6ce622139125c2e78fa45d2e90d534
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="96f34-103">Bir .NET web uygulamasından web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="96f34-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="96f34-104">Hızlı bir şekilde v2.0 uç noktası ile kimlik doğrulaması web uygulamalarınıza eklemek ve hem kişisel Microsoft hesapları için destek ve iş veya Okul hesaplarıyla API web.</span><span class="sxs-lookup"><span data-stu-id="96f34-104">With the v2.0 endpoint, you can quickly add authentication to your web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="96f34-105">Burada, biz Openıd Connect, Microsoft'un OWIN ara yazılımı için biraz Yardım ile kullanarak kullanıcılar oturum açtığında bir MVC web uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="96f34-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="96f34-106">Web uygulaması web API'si OAuth 2.0 tarafından sağlayan güvenli oluşturma için OAuth 2.0 erişim belirteçleri almak, okuma ve belirli kullanıcının "Yapılacaklar listesi üzerinde" silin.</span><span class="sxs-lookup"><span data-stu-id="96f34-106">The web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="96f34-107">Bu öğretici edinmeli ve erişim belirteçleri tam olarak tanımlanan bir web uygulamasında kullanmak için öncelikle MSAL üzerinden odaklanacaktır [burada](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="96f34-107">This tutorial will focus primarily on using MSAL to acquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="96f34-108">Önkoşul olarak ilk bilgi edinmek isteyebilirsiniz nasıl [temel oturum açma için bir web uygulaması eklemek](active-directory-v2-devquickstarts-dotnet-web.md) veya nasıl [düzgün bir web API güvenliğini](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="96f34-108">As prerequisites, you may want to first learn how to [add basic sign-in to a web app](active-directory-v2-devquickstarts-dotnet-web.md) or how to [properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="96f34-109">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="96f34-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="96f34-110">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="96f34-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="96f34-111">Örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="96f34-111">Download sample code</span></span>
<span data-ttu-id="96f34-112">Bu öğretici için kod [GitHub'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet) korunur.</span><span class="sxs-lookup"><span data-stu-id="96f34-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="96f34-113">İzlemek için [uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="96f34-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="96f34-114">Alternatif olarak, [tamamlanmış uygulamayı .zip olarak karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) veya tamamlanan uygulama:</span><span class="sxs-lookup"><span data-stu-id="96f34-114">Alternatively, you can [download the completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone the completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="96f34-115">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="96f34-115">Register an app</span></span>
<span data-ttu-id="96f34-116">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="96f34-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="96f34-117">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="96f34-117">Make sure to:</span></span>

* <span data-ttu-id="96f34-118">Aşağı kopyalama **uygulama kimliği** uygulamanıza atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="96f34-118">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="96f34-119">Oluşturma bir **uygulama gizli anahtarı** , **parola** türü ve değeri için daha sonra kopyalayın</span><span class="sxs-lookup"><span data-stu-id="96f34-119">Create an **App Secret** of the **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="96f34-120">Ekleme **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="96f34-120">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="96f34-121">Doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="96f34-121">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="96f34-122">Bu öğretici için varsayılan burada kimlik doğrulama yanıtları yönlendirileceğini - Azure AD ile yeniden yönlendirme URI'si gösterir `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="96f34-122">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="96f34-123">OWIN yükleme</span><span class="sxs-lookup"><span data-stu-id="96f34-123">Install OWIN</span></span>
<span data-ttu-id="96f34-124">OWIN ara yazılımı NuGet paketleri ekleme `TodoList-WebApp` Paket Yöneticisi konsolu kullanılarak proje.</span><span class="sxs-lookup"><span data-stu-id="96f34-124">Add the OWIN middleware NuGet packages to the `TodoList-WebApp` project using the Package Manager Console.</span></span>  <span data-ttu-id="96f34-125">OWIN ara yazılımı, oturum açma ve oturum kapatma isteklerini yürütmek, kullanıcının oturumunu yönetmek ve başka şeyler arasında kullanıcı hakkında bilgi almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="96f34-125">The OWIN middleware will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-the-user-in"></a><span data-ttu-id="96f34-126">Kullanıcı oturum aç</span><span class="sxs-lookup"><span data-stu-id="96f34-126">Sign the user in</span></span>
<span data-ttu-id="96f34-127">Kullanılacak OWIN Ara yazılımının şimdi yapılandırmak [Openıd Connect kimlik doğrulama protokolü](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="96f34-127">Now configure the OWIN middleware to use the [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="96f34-128">Açık `web.config` kökündeki dosyasında `TodoList-WebApp` proje ve uygulamanızın yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="96f34-128">Open the `web.config` file in the root of the `TodoList-WebApp` project, and enter your app's configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="96f34-129">`ida:ClientId` Olan **uygulama kimliği** kayıt portalında uygulamanıza atanan.</span><span class="sxs-lookup"><span data-stu-id="96f34-129">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="96f34-130">`ida:ClientSecret` Olan **uygulama gizli anahtarı** kayıt Portalı'nda oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="96f34-130">The `ida:ClientSecret` is the **App Secret** you created in the registration portal.</span></span>
  * <span data-ttu-id="96f34-131">`ida:RedirectUri` Olan **yeniden yönlendirme URI'si** portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="96f34-131">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>
* <span data-ttu-id="96f34-132">Açık `web.config` kökündeki dosyasında `TodoList-Service` proje ve değiştirme `ida:Audience` aynı **uygulama kimliği** olarak yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="96f34-132">Open the `web.config` file in the root of the `TodoList-Service` project, and replace the `ida:Audience` with the same **Application Id** as above.</span></span>
* <span data-ttu-id="96f34-133">Dosyayı açmak `App_Start\Startup.Auth.cs` ve ekleme `using` deyimleri üstten kitaplıkları için.</span><span class="sxs-lookup"><span data-stu-id="96f34-133">Open the file `App_Start\Startup.Auth.cs` and add `using` statements for the libraries from above.</span></span>
* <span data-ttu-id="96f34-134">Aynı dosyada uygulamak `ConfigureAuth(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="96f34-134">In the same file, implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="96f34-135">Sağladığınız içinde parametreleri `OpenIDConnectAuthenticationOptions` uygulamanız için Azure AD ile iletişim kurmak için koordinatları olarak hizmet verecektir.</span><span class="sxs-lookup"><span data-stu-id="96f34-135">The parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
    app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

    app.UseCookieAuthentication(new CookieAuthenticationOptions());

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {

                    // The `Authority` represents the v2.0 endpoint - https://login.microsoftonline.com/common/v2.0
                    // The `Scope` describes the permissions that your app will need.  See https://azure.microsoft.com/documentation/articles/active-directory-v2-scopes/
                    // In a real application you could use issuer validation for additional checks, like making sure the user's organization has signed up for your app, for instance.

                    ClientId = clientId,
                    Authority = String.Format(CultureInfo.InvariantCulture, aadInstance, "common", "/v2.0 "),
                    Scope = "openid email profile offline_access",
                    RedirectUri = redirectUri,
                    PostLogoutRedirectUri = redirectUri,
                    TokenValidationParameters = new TokenValidationParameters
                    {
                        ValidateIssuer = false,
                    },

                    // The `AuthorizationCodeReceived` notification is used to capture and redeem the authorization_code that the v2.0 endpoint returns to your app.

                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed,
                        AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    }

        });
}
// ...
```

## <a name="use-msal-to-get-access-tokens"></a><span data-ttu-id="96f34-136">Erişim belirteci almak için MSAL kullanın</span><span class="sxs-lookup"><span data-stu-id="96f34-136">Use MSAL to get access tokens</span></span>
<span data-ttu-id="96f34-137">İçinde `AuthorizationCodeReceived` bildirim, biz kullanmak istediğiniz [Openıd Connect ile OAuth 2.0 art arda](active-directory-v2-protocols.md) Yapılacaklar listesi hizmeti için bir erişim belirteci authorization_code kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="96f34-137">In the `AuthorizationCodeReceived` notification, we want to use [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) to redeem the authorization_code for an access token to the To-Do List Service.</span></span>  <span data-ttu-id="96f34-138">MSAL bu işlemi sizin için kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="96f34-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="96f34-139">İlk olarak, MSAL önizleme sürümünü yükleyin:</span><span class="sxs-lookup"><span data-stu-id="96f34-139">First, install the preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="96f34-140">Ve başka bir tane eklemek `using` ifadesine `App_Start\Startup.Auth.cs` MSAL dosyası.</span><span class="sxs-lookup"><span data-stu-id="96f34-140">And add another `using` statement to the `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="96f34-141">Şimdi yeni bir yöntem ekleyin `OnAuthorizationCodeReceived` olay işleyicisi.</span><span class="sxs-lookup"><span data-stu-id="96f34-141">Now add a new method, the `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="96f34-142">Bu işleyici MSAL Yapılacaklar listesi API için bir erişim belirteci almak için kullanır ve belirteç MSAL'ın belirteci önbelleğinde daha sonrası için depolar:</span><span class="sxs-lookup"><span data-stu-id="96f34-142">This handler will use MSAL to acquire an access token to the To-Do List API, and will store the token in MSAL's token cache for later:</span></span>

```C#
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
        string userObjectId = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        string tenantID = notification.AuthenticationTicket.Identity.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
        string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenantID, string.Empty);
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        // Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
        app = new ConfidentialClientApplication(Startup.clientId, redirectUri, cred, new NaiveSessionCache(userObjectId, notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase)) {};
        var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { clientId }, notification.Code);
}
// ...
```

* <span data-ttu-id="96f34-143">Web uygulamalarında MSAL belirteçleri depolamak için kullanılan genişletilebilir bir belirteç önbelleğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="96f34-143">In web apps, MSAL has an extensible token cache that can be used to store tokens.</span></span>  <span data-ttu-id="96f34-144">Bu örnek uygulayan `NaiveSessionCache` önbellek belirteçleri için http oturum depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="96f34-144">This sample implements the `NaiveSessionCache` which uses http session storage to cache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-the-web-api"></a><span data-ttu-id="96f34-145">Web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="96f34-145">Call the Web API</span></span>
<span data-ttu-id="96f34-146">Şimdi 3. adımda aldığınız access_token gerçekten kullandığınız zamanı geldi.</span><span class="sxs-lookup"><span data-stu-id="96f34-146">Now it's time to actually use the access_token you acquired in step 3.</span></span>  <span data-ttu-id="96f34-147">Web uygulamanızın açmak `Controllers\TodoListController.cs` Yapılacaklar listesi API'sine tüm CRUD istek yaptığında dosya.</span><span class="sxs-lookup"><span data-stu-id="96f34-147">Open the web app's `Controllers\TodoListController.cs` file, which makes all the CRUD requests to the To-Do List API.</span></span>

* <span data-ttu-id="96f34-148">MSAL yeniden buraya access_tokens MSAL önbellekten getirileceği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96f34-148">You can use MSAL again here to fetch access_tokens from the MSAL cache.</span></span>  <span data-ttu-id="96f34-149">İlk olarak, ekleyin bir `using` bu dosyaya MSAL bildirimi.</span><span class="sxs-lookup"><span data-stu-id="96f34-149">First, add a `using` statement for MSAL to this file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="96f34-150">İçinde `Index` eylemin, kullanım MSAL `AcquireTokenSilentAsync` Yapılacaklar listesi hizmetinden veri okumak için kullanılan bir access_token almak için yöntemi:</span><span class="sxs-lookup"><span data-stu-id="96f34-150">In the `Index` action, use MSAL's `AcquireTokenSilentAsync` method to get an access_token that can be used to read data from the To-Do List service:</span></span>

```C#
// ...
string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
string tenantID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/tenantid").Value;
string authority = String.Format(CultureInfo.InvariantCulture, Startup.aadInstance, tenantID, string.Empty);
ClientCredential credential = new ClientCredential(Startup.clientId, Startup.clientSecret);

// Here you ask for a token using the web app's clientId as the scope, since the web app and service share the same clientId.
app = new ConfidentialClientApplication(Startup.clientId, redirectUri, credential, new NaiveSessionCache(userObjectID, this.HttpContext)){};
result = await app.AcquireTokenSilentAsync(new string[] { Startup.clientId });
// ...
```

* <span data-ttu-id="96f34-151">Örnek HTTP GET isteği elde edilen belirteç sonra ekler `Authorization` Yapılacaklar listesi hizmetinin istek kimliğini doğrulamak için kullandığı üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="96f34-151">The sample then adds the resulting token to the HTTP GET request as the `Authorization` header, which the To-Do List service uses to authenticate the request.</span></span>
* <span data-ttu-id="96f34-152">Yapılacaklar listesi hizmet döndürürse bir `401 Unauthorized` yanıtı access_tokens MSAL içinde geçersiz hale herhangi bir nedenden dolayı.</span><span class="sxs-lookup"><span data-stu-id="96f34-152">If the To-Do List service returns a `401 Unauthorized` response, the access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="96f34-153">Bu durumda, MSAL önbellekten herhangi access_tokens bırakın ve kullanıcı yeniden hangi belirteç edinme akışı yeniden içinde oturum gerekebilir görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="96f34-153">In this case, you should drop any access_tokens from the MSAL cache and show the user a message that they may need to sign in again, which will restart the token acquisition flow.</span></span>

```C#
// ...
// If the call failed with access denied, then drop the current access token from the cache,
// and show the user an error indicating they might need to sign-in again.
if (response.StatusCode == System.Net.HttpStatusCode.Unauthorized)
{
        app.AppTokenCache.Clear(Startup.clientId);

        return new RedirectResult("/Error?message=Error: " + response.ReasonPhrase + " You might need to sign in again.");
}
// ...
```

* <span data-ttu-id="96f34-154">Benzer şekilde, MSAL herhangi bir nedenle bir access_token döndüremedi ise, kullanıcı yeniden oturum açmak için istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="96f34-154">Similarly, if MSAL is unable to return an access_token for any reason, you should instruct the user to sign in again.</span></span>  <span data-ttu-id="96f34-155">Bu herhangi bir yakalama olarak kadar basittir `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="96f34-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show the user an error indicating they might need to sign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading To Do List: " + ee.Message + " You might need to log out and log back in.");
}
// ...
```

* <span data-ttu-id="96f34-156">Aynı tam `AcquireTokenSilentAsync` çağrıdır içinde implementd `Create` ve `Delete` eylemler.</span><span class="sxs-lookup"><span data-stu-id="96f34-156">The exact same `AcquireTokenSilentAsync` call is implementd in the `Create` and `Delete` actions.</span></span>  <span data-ttu-id="96f34-157">Web uygulamalarında uygulamanızda ihtiyaç duyduğunuzda access_tokens almak için bu MSAL yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96f34-157">In web apps, you can use this MSAL method to get access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="96f34-158">MSAL alınırken, önbelleğe alma ve belirteçleri, yenileme ilgilenebilmek.</span><span class="sxs-lookup"><span data-stu-id="96f34-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="96f34-159">Son olarak, yapı ve uygulamanızı çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="96f34-159">Finally, build and run your app!</span></span>  <span data-ttu-id="96f34-160">Microsoft Account veya bir Azure AD hesabının oturum açın ve kullanıcının kimliğini üst gezinti çubuğunda nasıl yansıtılır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="96f34-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="96f34-161">Ekleyin ve eylem API çağrılarında OAuth 2.0 güvenli görmek için kullanıcının Yapılacaklar listesinde bazı öğeleri silin.</span><span class="sxs-lookup"><span data-stu-id="96f34-161">Add and delete some items from the user's To-Do List to see the OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="96f34-162">Artık bir web uygulaması ve web API, hem kullanıcıların hem kişisel hem de iş/Okul hesaplarını ile doğrulanabilir endüstri standardı protokoller üzerine kullanılarak güvenlik altına sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="96f34-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="96f34-163">(Yapılandırma değerleriniz olmadan) tamamlanan örnek, başvuru için [burada sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="96f34-163">For reference, the completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="96f34-164">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="96f34-164">Next Steps</span></span>
<span data-ttu-id="96f34-165">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="96f34-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="96f34-166">V2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="96f34-166">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="96f34-167">StackOverflow "azure-active-directory" etiketi >></span><span class="sxs-lookup"><span data-stu-id="96f34-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="96f34-168">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="96f34-168">Get security updates for our products</span></span>
<span data-ttu-id="96f34-169">[Bu sayfayı](https://technet.microsoft.com/security/dd252948) ziyaret ederek ve Güvenlik Önerisi Uyarılarına abone olarak güvenlik olaylarının ne zaman ortaya çıkacağı hakkında bildirimleri almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="96f34-169">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

