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
# <a name="calling-a-web-api-from-a-net-web-app"></a><span data-ttu-id="9c130-103">Bir .NET web uygulamasından web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="9c130-103">Calling a web API from a .NET web app</span></span>
<span data-ttu-id="9c130-104">Hızlı bir şekilde Hello v2.0 uç noktası ile kimlik doğrulaması tooyour web uygulamaları ekleyin ve hem kişisel Microsoft hesapları için destek ve iş veya Okul hesaplarıyla API web.</span><span class="sxs-lookup"><span data-stu-id="9c130-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps and web APIs with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="9c130-105">Burada, biz Openıd Connect, Microsoft'un OWIN ara yazılımı için biraz Yardım ile kullanarak kullanıcılar oturum açtığında bir MVC web uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9c130-105">Here, we'll build an MVC web app that signs users in using OpenID Connect, with some help from Microsoft's OWIN middleware.</span></span>  <span data-ttu-id="9c130-106">Merhaba web uygulaması web API'si OAuth 2.0 tarafından sağlayan güvenli oluşturma için OAuth 2.0 erişim belirteçleri almak, okuma ve belirli kullanıcının "Yapılacaklar listesi üzerinde" silin.</span><span class="sxs-lookup"><span data-stu-id="9c130-106">hello web app will get OAuth 2.0 access tokens for a web api secured by OAuth 2.0 that allows create, read, and delete on a given user's "To-Do List".</span></span>

<span data-ttu-id="9c130-107">Bu öğretici odaklanmak öncelikle MSAL tooacquire kullanarak ve tam olarak tanımlanan bir web uygulamasında erişim belirteçleri kullanın [burada](active-directory-v2-flows.md#web-apps).</span><span class="sxs-lookup"><span data-stu-id="9c130-107">This tutorial will focus primarily on using MSAL tooacquire and use access tokens in a web app, described in full [here](active-directory-v2-flows.md#web-apps).</span></span>  <span data-ttu-id="9c130-108">Önkoşul olarak isteyebilirsiniz toofirst öğrenin nasıl çok[oturum açma temel tooa web uygulaması ekleme](active-directory-v2-devquickstarts-dotnet-web.md) veya nasıl çok[düzgün bir web API güvenliğini](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="9c130-108">As prerequisites, you may want toofirst learn how too[add basic sign-in tooa web app](active-directory-v2-devquickstarts-dotnet-web.md) or how too[properly secure a web API](active-directory-v2-devquickstarts-dotnet-api.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9c130-109">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c130-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="9c130-110">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9c130-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-sample-code"></a><span data-ttu-id="9c130-111">Örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="9c130-111">Download sample code</span></span>
<span data-ttu-id="9c130-112">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="9c130-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="9c130-113">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="9c130-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

<span data-ttu-id="9c130-114">Alternatif olarak, [tamamlandı hello uygulama .zip olarak karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) ya da kopyalama tamamlandı hello uygulama:</span><span class="sxs-lookup"><span data-stu-id="9c130-114">Alternatively, you can [download hello completed app as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip) or clone hello completed app:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet.git```

## <a name="register-an-app"></a><span data-ttu-id="9c130-115">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="9c130-115">Register an app</span></span>
<span data-ttu-id="9c130-116">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="9c130-116">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9c130-117">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="9c130-117">Make sure to:</span></span>

* <span data-ttu-id="9c130-118">Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="9c130-118">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="9c130-119">Oluşturma bir **uygulama gizli anahtarı** Merhaba, **parola** türü ve değeri için daha sonra kopyalayın</span><span class="sxs-lookup"><span data-stu-id="9c130-119">Create an **App Secret** of hello **Password** type, and copy down its value for later</span></span>
* <span data-ttu-id="9c130-120">Merhaba eklemek **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="9c130-120">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="9c130-121">Merhaba doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="9c130-121">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="9c130-122">Merhaba yeniden yönlendirme URI'si gösterir hello varsayılan Bu öğretici için burada kimlik doğrulama yanıtları yönlendirileceğini - tooAzure AD `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="9c130-122">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install-owin"></a><span data-ttu-id="9c130-123">OWIN yükleme</span><span class="sxs-lookup"><span data-stu-id="9c130-123">Install OWIN</span></span>
<span data-ttu-id="9c130-124">Merhaba OWIN ara yazılımı NuGet paketleri toohello ekleme `TodoList-WebApp` hello Paket Yöneticisi konsolu kullanarak projesi.</span><span class="sxs-lookup"><span data-stu-id="9c130-124">Add hello OWIN middleware NuGet packages toohello `TodoList-WebApp` project using hello Package Manager Console.</span></span>  <span data-ttu-id="9c130-125">Merhaba OWIN ara yazılımı kullanılan tooissue oturum açma ve oturum kapatma isteklerini olması, hello kullanıcının oturumunu yönetmek ve başka şeyler arasında hello kullanıcı hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="9c130-125">hello OWIN middleware will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Security.Cookies -ProjectName TodoList-WebApp
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoList-WebApp
```

## <a name="sign-hello-user-in"></a><span data-ttu-id="9c130-126">Merhaba kullanıcı olarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="9c130-126">Sign hello user in</span></span>
<span data-ttu-id="9c130-127">Şimdi hello OWIN ara yazılımı toouse hello yapılandırmak [Openıd Connect kimlik doğrulama protokolü](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="9c130-127">Now configure hello OWIN middleware toouse hello [OpenID Connect authentication protocol](active-directory-v2-protocols.md).</span></span>  

* <span data-ttu-id="9c130-128">Açık hello `web.config` hello hello kökündeki dosyasında `TodoList-WebApp` proje ve hello uygulamanızın yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c130-128">Open hello `web.config` file in hello root of hello `TodoList-WebApp` project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="9c130-129">Merhaba `ida:ClientId` hello olan **uygulama kimliği** tooyour uygulama hello kayıt Portalı'nda atanmış.</span><span class="sxs-lookup"><span data-stu-id="9c130-129">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="9c130-130">Merhaba `ida:ClientSecret` hello olan **uygulama gizli anahtarı** hello kayıt Portalı'nda oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="9c130-130">hello `ida:ClientSecret` is hello **App Secret** you created in hello registration portal.</span></span>
  * <span data-ttu-id="9c130-131">Merhaba `ida:RedirectUri` hello olan **yeniden yönlendirme URI'si** hello portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="9c130-131">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>
* <span data-ttu-id="9c130-132">Açık hello `web.config` hello hello kökündeki dosyasında `TodoList-Service` proje ve hello yerine `ida:Audience` ile aynı hello **uygulama kimliği** olarak yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="9c130-132">Open hello `web.config` file in hello root of hello `TodoList-Service` project, and replace hello `ida:Audience` with hello same **Application Id** as above.</span></span>
* <span data-ttu-id="9c130-133">Açık hello dosya `App_Start\Startup.Auth.cs` ve ekleme `using` deyimleri üstten hello kitaplıkları için.</span><span class="sxs-lookup"><span data-stu-id="9c130-133">Open hello file `App_Start\Startup.Auth.cs` and add `using` statements for hello libraries from above.</span></span>
* <span data-ttu-id="9c130-134">Buna Merhaba aynı dosya, hello uygulamak `ConfigureAuth(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9c130-134">In hello same file, implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="9c130-135">Merhaba, sağladığınız parametreler `OpenIDConnectAuthenticationOptions` , uygulama toocommunicate Azure AD ile koordinatları olarak hizmet verecektir.</span><span class="sxs-lookup"><span data-stu-id="9c130-135">hello parameters you provide in `OpenIDConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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

## <a name="use-msal-tooget-access-tokens"></a><span data-ttu-id="9c130-136">MSAL tooget erişim belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="9c130-136">Use MSAL tooget access tokens</span></span>
<span data-ttu-id="9c130-137">Merhaba, `AuthorizationCodeReceived` bildirim, toouse istiyoruz [Openıd Connect ile OAuth 2.0 art arda](active-directory-v2-protocols.md) tooredeem hello authorization_code bir erişim belirteci toohello Yapılacaklar listesi hizmeti için.</span><span class="sxs-lookup"><span data-stu-id="9c130-137">In hello `AuthorizationCodeReceived` notification, we want toouse [OAuth 2.0 in tandem with OpenID Connect](active-directory-v2-protocols.md) tooredeem hello authorization_code for an access token toohello To-Do List Service.</span></span>  <span data-ttu-id="9c130-138">MSAL bu işlemi sizin için kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="9c130-138">MSAL can make this process easy for you:</span></span>

* <span data-ttu-id="9c130-139">İlk olarak, MSAL hello önizleme sürümünü yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9c130-139">First, install hello preview version of MSAL:</span></span>

```PM> Install-Package Microsoft.Identity.Client -ProjectName TodoList-WebApp -IncludePrerelease```

* <span data-ttu-id="9c130-140">Ve başka bir tane eklemek `using` deyimi toohello `App_Start\Startup.Auth.cs` MSAL dosyası.</span><span class="sxs-lookup"><span data-stu-id="9c130-140">And add another `using` statement toohello `App_Start\Startup.Auth.cs` file for MSAL.</span></span>
* <span data-ttu-id="9c130-141">Şimdi yeni bir yöntemi, hello eklemek `OnAuthorizationCodeReceived` olay işleyicisi.</span><span class="sxs-lookup"><span data-stu-id="9c130-141">Now add a new method, hello `OnAuthorizationCodeReceived` event handler.</span></span>  <span data-ttu-id="9c130-142">Bu işleyici MSAL tooacquire bir erişim belirteci toohello Yapılacaklar listesi API kullanır ve hello belirteci MSAL'ın belirteci önbelleğinde daha sonrası için depolar:</span><span class="sxs-lookup"><span data-stu-id="9c130-142">This handler will use MSAL tooacquire an access token toohello To-Do List API, and will store hello token in MSAL's token cache for later:</span></span>

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

* <span data-ttu-id="9c130-143">Web uygulamalarında MSAL kullanılan toostore belirteçleri olabilecek genişletilebilir bir belirteç önbelleğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9c130-143">In web apps, MSAL has an extensible token cache that can be used toostore tokens.</span></span>  <span data-ttu-id="9c130-144">Bu örnek hello uygulayan `NaiveSessionCache` http oturumu depolama toocache belirteçlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9c130-144">This sample implements hello `NaiveSessionCache` which uses http session storage toocache tokens.</span></span>

<!-- TODO: Token Cache article -->


## <a name="call-hello-web-api"></a><span data-ttu-id="9c130-145">Merhaba Web API çağrısı</span><span class="sxs-lookup"><span data-stu-id="9c130-145">Call hello Web API</span></span>
<span data-ttu-id="9c130-146">Artık tooactually 3. adımda aldığınız hello access_token kullanışınızda durumdadır.</span><span class="sxs-lookup"><span data-stu-id="9c130-146">Now it's time tooactually use hello access_token you acquired in step 3.</span></span>  <span data-ttu-id="9c130-147">Açık hello web uygulamanızın `Controllers\TodoListController.cs` dosya, toohello Yapılacaklar listesi API istekleri, tüm hello CRUD yapar.</span><span class="sxs-lookup"><span data-stu-id="9c130-147">Open hello web app's `Controllers\TodoListController.cs` file, which makes all hello CRUD requests toohello To-Do List API.</span></span>

* <span data-ttu-id="9c130-148">MSAL kullanabileceğiniz yeniden toofetch access_tokens gelen MSAL önbellek burada hello.</span><span class="sxs-lookup"><span data-stu-id="9c130-148">You can use MSAL again here toofetch access_tokens from hello MSAL cache.</span></span>  <span data-ttu-id="9c130-149">İlk olarak, ekleyin bir `using` MSAL toothis dosya bildirimi.</span><span class="sxs-lookup"><span data-stu-id="9c130-149">First, add a `using` statement for MSAL toothis file.</span></span>
  
    `using Microsoft.Identity.Client;`
* <span data-ttu-id="9c130-150">Merhaba, `Index` eylemin, kullanım MSAL `AcquireTokenSilentAsync` yöntemi tooget hello Yapılacaklar listesi hizmet kullanılan tooread verilerden olabilir bir access_token:</span><span class="sxs-lookup"><span data-stu-id="9c130-150">In hello `Index` action, use MSAL's `AcquireTokenSilentAsync` method tooget an access_token that can be used tooread data from hello To-Do List service:</span></span>

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

* <span data-ttu-id="9c130-151">Merhaba örnek sonra sonuçta elde edilen belirteci toohello HTTP GET isteği hello hello ekler `Authorization` hangi hello Yapılacaklar listesi hizmetinin kullandığı tooauthenticate hello isteği üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="9c130-151">hello sample then adds hello resulting token toohello HTTP GET request as hello `Authorization` header, which hello To-Do List service uses tooauthenticate hello request.</span></span>
* <span data-ttu-id="9c130-152">Merhaba Yapılacaklar listesi hizmet döndürürse bir `401 Unauthorized` yanıtı hello access_tokens MSAL içinde geçersiz hale herhangi bir nedenden dolayı.</span><span class="sxs-lookup"><span data-stu-id="9c130-152">If hello To-Do List service returns a `401 Unauthorized` response, hello access_tokens in MSAL have become invalid for some reason.</span></span>  <span data-ttu-id="9c130-153">Bu durumda, tüm access_tokens MSAL önbellek hello bırakın ve yeniden hangi hello belirteç edinme akışı yeniden başlatılacak içinde toosign gerekebilir bir ileti hello kullanıcı Göster gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c130-153">In this case, you should drop any access_tokens from hello MSAL cache and show hello user a message that they may need toosign in again, which will restart hello token acquisition flow.</span></span>

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

* <span data-ttu-id="9c130-154">Benzer şekilde, MSAL herhangi bir nedenle yüklenemiyor tooreturn bir access_token ise, hello kullanıcı toosign yeniden istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c130-154">Similarly, if MSAL is unable tooreturn an access_token for any reason, you should instruct hello user toosign in again.</span></span>  <span data-ttu-id="9c130-155">Bu herhangi bir yakalama olarak kadar basittir `MSALException`:</span><span class="sxs-lookup"><span data-stu-id="9c130-155">This is as simple as catching any `MSALException`:</span></span>

```C#
// ...
catch (MsalException ee)
{
        // If MSAL could not get a token silently, show hello user an error indicating they might need toosign in again.
        return new RedirectResult("/Error?message=An Error Occurred Reading tooDo List: " + ee.Message + " You might need toolog out and log back in.");
}
// ...
```

* <span data-ttu-id="9c130-156">Merhaba tam aynı `AcquireTokenSilentAsync` çağrıdır hello implementd `Create` ve `Delete` eylemler.</span><span class="sxs-lookup"><span data-stu-id="9c130-156">hello exact same `AcquireTokenSilentAsync` call is implementd in hello `Create` and `Delete` actions.</span></span>  <span data-ttu-id="9c130-157">Web uygulamalarında uygulamanızda gerektiğinde bu MSAL yöntemi tooget access_tokens kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c130-157">In web apps, you can use this MSAL method tooget access_tokens whenever you need them in your app.</span></span>  <span data-ttu-id="9c130-158">MSAL alınırken, önbelleğe alma ve belirteçleri, yenileme ilgilenebilmek.</span><span class="sxs-lookup"><span data-stu-id="9c130-158">MSAL will take care of acquiring, caching, and refreshing tokens for you.</span></span>

<span data-ttu-id="9c130-159">Son olarak, yapı ve uygulamanızı çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="9c130-159">Finally, build and run your app!</span></span>  <span data-ttu-id="9c130-160">Microsoft Account veya bir Azure AD hesabının oturum açın ve hello kullanıcının kimliğini hello üst gezinti çubuğunda nasıl yansıtılır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9c130-160">Sign in with either a Microsoft Account or an Azure AD Account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="9c130-161">Ekleyin ve bazı öğeler hello kullanıcının Yapılacaklar listesinde OAuth 2.0 API güvenli toosee hello eylemini çağırır silin.</span><span class="sxs-lookup"><span data-stu-id="9c130-161">Add and delete some items from hello user's To-Do List toosee hello OAuth 2.0 secured API calls in action.</span></span>  <span data-ttu-id="9c130-162">Artık bir web uygulaması ve web API, hem kullanıcıların hem kişisel hem de iş/Okul hesaplarını ile doğrulanabilir endüstri standardı protokoller üzerine kullanılarak güvenlik altına sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c130-162">You now have a web app & web API, both secured using industry standard protocols, that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="9c130-163">Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9c130-163">For reference, hello completed sample (without your configuration values) [is provided here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-WebAPI-OpenIdConnect-DotNet/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9c130-164">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9c130-164">Next Steps</span></span>
<span data-ttu-id="9c130-165">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="9c130-165">For additional resources, check out:</span></span>

* [<span data-ttu-id="9c130-166">Merhaba v2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="9c130-166">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9c130-167">StackOverflow "azure-active-directory" etiketi >></span><span class="sxs-lookup"><span data-stu-id="9c130-167">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9c130-168">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="9c130-168">Get security updates for our products</span></span>
<span data-ttu-id="9c130-169">Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="9c130-169">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

