---
title: "Oturum açma bir .NET MVC web API kullanarak Azure AD v2.0 uç ekleme | Microsoft Docs"
description: "Hem kişisel Microsoft Account belirteçleri kabul eder .NET MVC Web API'si oluşturma ve iş veya Okul hesapları."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: b2d7bbfcd9218698f71e9dfdb1ad5d9ff8740f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="7e155-103">Bir MVC web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="7e155-103">Secure an MVC web API</span></span>
<span data-ttu-id="7e155-104">Azure Active Directory ile v2.0 uç noktası, bir Web API kullanarak koruyabilirsiniz [OAuth 2.0](active-directory-v2-protocols.md) erişim belirteçleri, kullanıcıların hem kişisel Microsoft hesabı ile etkinleştirme ve iş veya Okul güvenli erişim sağlamak, Web API hesaplar.</span><span class="sxs-lookup"><span data-stu-id="7e155-104">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="7e155-105">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7e155-105">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="7e155-106">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="7e155-106">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="7e155-107">ASP.NET web API'da, bunu .NET Framework 4. 5 ' dahil Microsoft'un OWIN ara yazılımı kullanarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e155-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="7e155-108">OWIN oluşturmak ve bir kullanıcının yapılacaklar listesinden görevleri okumak istemcilerin bir "Yapılacaklar listesi" MVC Web API oluşturmak için buraya kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="7e155-108">Here we’ll use OWIN to build a "To Do List" MVC Web API that allows clients to create and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="7e155-109">Web API gelen istekleri geçerli erişim belirteci içeren ve doğrulama korumalı bir rotaya geçmeyin istekleri reddedecek doğrular.</span><span class="sxs-lookup"><span data-stu-id="7e155-109">The web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="7e155-110">Bu örnek, Visual Studio 2015 kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7e155-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="7e155-111">İndir</span><span class="sxs-lookup"><span data-stu-id="7e155-111">Download</span></span>
<span data-ttu-id="7e155-112">Bu öğretici için kod [GitHub'da](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet) korunur.</span><span class="sxs-lookup"><span data-stu-id="7e155-112">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="7e155-113">İzlemek için [uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="7e155-113">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="7e155-114">İskelet uygulama için basit bir API tüm Demirbaş kod içerir, ancak kimlikle ilgili şey eksik.</span><span class="sxs-lookup"><span data-stu-id="7e155-114">The skeleton app includes all the boilerplate code for a simple API, but is missing all of the identity-related pieces.</span></span> <span data-ttu-id="7e155-115">Takip istemiyorsanız, bunun yerine, kopyalayabilir veya [tamamlanan örnek indirme](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7e155-115">If you don't want to follow along, you can instead clone or [download the completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="7e155-116">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="7e155-116">Register an app</span></span>
<span data-ttu-id="7e155-117">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="7e155-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="7e155-118">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="7e155-118">Make sure to:</span></span>

* <span data-ttu-id="7e155-119">Aşağı kopyalama **uygulama kimliği** uygulamanıza atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="7e155-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>

<span data-ttu-id="7e155-120">Bu visual studio çözümü "basit bir WPF uygulaması olan bir TodoListClient", de içerir.</span><span class="sxs-lookup"><span data-stu-id="7e155-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="7e155-121">TodoListClient nasıl bir kullanıcı oturum açtığında ve bir istemci isteklerini Web API'nizi nasıl verebilir göstermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7e155-121">The TodoListClient is used to demonstrate how a user signs-in and how a client can issue requests to your Web API.</span></span>  <span data-ttu-id="7e155-122">Bu durumda, TodoListClient ve TodoListService aynı uygulama tarafından temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="7e155-122">In this case, both the TodoListClient and the TodoListService are represented by the same app.</span></span>  <span data-ttu-id="7e155-123">TodoListClient yapılandırmak için de yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="7e155-123">To configure the TodoListClient, you should also:</span></span>

* <span data-ttu-id="7e155-124">Ekleme **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="7e155-124">Add the **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="7e155-125">OWIN yükleme</span><span class="sxs-lookup"><span data-stu-id="7e155-125">Install OWIN</span></span>
<span data-ttu-id="7e155-126">Bir uygulama kaydınız, gelen istekleri & belirteçleri doğrulamak için v2.0 uç noktası ile iletişim kurmak için uygulamanızı ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e155-126">Now that you’ve registered an app, you need to set up your app to communicate with the v2.0 endpoint in order to validate incoming requests & tokens.</span></span>

* <span data-ttu-id="7e155-127">Başlamak için çözümü açın ve OWIN ara yazılımı NuGet paketleri Paket Yöneticisi konsolu kullanılarak TodoListService projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7e155-127">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="7e155-128">OAuth kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7e155-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="7e155-129">Adlı TodoListService projesine OWIN başlangıç sınıfı ekleyin `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="7e155-129">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="7e155-130">Projeye sağ tıklatma--> **Ekle** --> **yeni öğe** "OWIN" arayın.</span><span class="sxs-lookup"><span data-stu-id="7e155-130">Right click on the project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="7e155-131">OWIN ara yazılımı, uygulamanız başlatıldığında `Configuration(…)` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="7e155-131">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="7e155-132">Sınıf bildirimi değiştirme `public partial class Startup` -zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="7e155-132">Change the class declaration to `public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="7e155-133">İçinde `Configuration(…)` yöntemi, bir web uygulamanız için kimlik doğrulaması ayarlamak için ConfgureAuth(...) çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="7e155-133">In the `Configuration(…)` method, make a call to ConfgureAuth(…) to set up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="7e155-134">Dosyayı açmak `App_Start\Startup.Auth.cs` ve uygulamanıza `ConfigureAuth(…)` Web API v2.0 uç noktasından belirteçleri kabul ayarlar yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7e155-134">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method, which will set up the Web API to accept tokens from the v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, the TodoListClient and TodoListService
                // are represented using the same Application Id - we use
                // the Application Id to represent the audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that the user's organization (if applicable) has
                // signed up for the app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up the OWIN pipeline to use OAuth 2.0 Bearer authentication.
        // The options provided here tell the middleware about the type of tokens
        // that will be recieved, which are JWTs for the v2.0 endpoint.

        // NOTE: The usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by the v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used to fetch & use the OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="7e155-135">Kullanabileceğiniz artık `[Authorize]` denetleyicileri ve eylemleri OAuth 2.0 taşıyıcı kimlik doğrulaması ile korumak için öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="7e155-135">Now you can use `[Authorize]` attributes to protect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="7e155-136">İşaretleme `Controllers\TodoListController.cs` bir authorize etiketiyle sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7e155-136">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="7e155-137">Bu sayfayı erişmeden önce oturum açmak için kullanıcının zorlar.</span><span class="sxs-lookup"><span data-stu-id="7e155-137">This will force the user to sign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="7e155-138">Ne zaman bir yetkili çağıran başarıyla çağırır birini `TodoListController` API'leri, eylem çağıran hakkında bilgilere erişimi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="7e155-138">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span>  <span data-ttu-id="7e155-139">OWIN taşıyıcı belirteci içinde talep erişim sağlar `ClaimsPrincpal` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7e155-139">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use the ClaimsPrincipal to access information about the
    // user making the call.  In this case, we use the 'sub' or
    // NameIdentifier claim to serve as a key for the tasks in the data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="7e155-140">Son olarak, açık `web.config` dosya TodoListService proje kök dizininde ve yapılandırma değerlerinizi girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="7e155-140">Finally, open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="7e155-141">`ida:Audience` Olan **uygulama kimliği** portalda girdiğiniz uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="7e155-141">Your `ida:Audience` is the **Application Id** of the app that you entered in the portal.</span></span>

## <a name="configure-the-client-app"></a><span data-ttu-id="7e155-142">İstemci uygulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7e155-142">Configure the client app</span></span>
<span data-ttu-id="7e155-143">Eylem Yapılacaklar listesi hizmetinde görebilmek v2.0 uç noktasından belirteç almak ve hizmet çağrı yapmak için yapılacaklar listesi istemci yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7e155-143">Before you can see the Todo List Service in action, you need to configure the Todo List Client so it can get tokens from the v2.0 endpoint and make calls to the service.</span></span>

* <span data-ttu-id="7e155-144">TodoListClient projeyi açın `App.config` ve yapılandırma değerlerinizi girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="7e155-144">In the TodoListClient project, open `App.config` and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="7e155-145">`ida:ClientId` Uygulama portaldan kopyaladığınız kimliği.</span><span class="sxs-lookup"><span data-stu-id="7e155-145">Your `ida:ClientId` Application Id you copied from the portal.</span></span>

<span data-ttu-id="7e155-146">Son olarak, temiz, yapı ve her proje çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="7e155-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="7e155-147">Artık hem kişisel Microsoft hesaplarını gelen belirteçleri ve iş veya Okul hesapları kabul eden bir .NET MVC Web API vardır.</span><span class="sxs-lookup"><span data-stu-id="7e155-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="7e155-148">Oturum TodoListClient ve web çağrı görevler kullanıcının yapılacaklar listesine eklemek için API.</span><span class="sxs-lookup"><span data-stu-id="7e155-148">Sign into the TodoListClient, and call your web api to add tasks to the user's To-Do list.</span></span>

<span data-ttu-id="7e155-149">(Yapılandırma değerleriniz olmadan) tamamlanan örnek, başvuru için [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e155-149">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="7e155-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7e155-150">Next steps</span></span>
<span data-ttu-id="7e155-151">Artık ek konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e155-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="7e155-152">Denemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e155-152">You may want to try:</span></span>

[<span data-ttu-id="7e155-153">Bir Web uygulamasından Web API'si çağırma >></span><span class="sxs-lookup"><span data-stu-id="7e155-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="7e155-154">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="7e155-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="7e155-155">V2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="7e155-155">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="7e155-156">StackOverflow "azure-active-directory" etiketi >></span><span class="sxs-lookup"><span data-stu-id="7e155-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="7e155-157">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="7e155-157">Get security updates for our products</span></span>
<span data-ttu-id="7e155-158">[Bu sayfayı](https://technet.microsoft.com/security/dd252948) ziyaret ederek ve Güvenlik Önerisi Uyarılarına abone olarak güvenlik olaylarının ne zaman ortaya çıkacağı hakkında bildirimleri almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="7e155-158">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
