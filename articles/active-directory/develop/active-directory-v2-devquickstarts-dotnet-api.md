---
title: "aaaAdd oturum açma tooa .NET MVC web API kullanarak Azure AD v2.0 uç hello | Microsoft Docs"
description: "Nasıl toobuild hem kişisel Microsoft Account gelen belirteçleri ve iş veya Okul hesapları kabul eden bir .NET MVC Web API."
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
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a><span data-ttu-id="3cd31-103">Bir MVC web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="3cd31-103">Secure an MVC web API</span></span>
<span data-ttu-id="3cd31-104">Azure Active Directory hello v2.0 uç ile Web API kullanarak koruyabilirsiniz [OAuth 2.0](active-directory-v2-protocols.md) erişim belirteçleri, hem kişisel Microsoft hesabı olan kullanıcılar ve iş veya Okul hesapları toosecurely Web API erişimi etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="3cd31-104">With Azure Active Directory hello v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts toosecurely access your Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="3cd31-105">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3cd31-105">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="3cd31-106">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="3cd31-106">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

<span data-ttu-id="3cd31-107">ASP.NET web API'da, bunu .NET Framework 4. 5 ' dahil Microsoft'un OWIN ara yazılımı kullanarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cd31-107">In ASP.NET web APIs, you can accomplish this using Microsoft’s OWIN middleware included in .NET Framework 4.5.</span></span>  <span data-ttu-id="3cd31-108">OWIN toobuild kullanıcının yapılacaklar listesi toocreate ve okuma görevlerden istemcilerinin veren "tooDo listesi" MVC Web API burada kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3cd31-108">Here we’ll use OWIN toobuild a "tooDo List" MVC Web API that allows clients toocreate and read tasks from a user's To-Do list.</span></span>  <span data-ttu-id="3cd31-109">Merhaba web API gelen istekleri geçerli erişim belirteci içeren ve doğrulama korumalı bir rotaya geçmeyin istekleri reddedecek doğrular.</span><span class="sxs-lookup"><span data-stu-id="3cd31-109">hello web API will validate that incoming requests contain a valid access token and reject any requests that do not pass validation on a protected route.</span></span>  <span data-ttu-id="3cd31-110">Bu örnek, Visual Studio 2015 kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3cd31-110">This sample was built using Visual Studio 2015.</span></span>

## <a name="download"></a><span data-ttu-id="3cd31-111">İndir</span><span class="sxs-lookup"><span data-stu-id="3cd31-111">Download</span></span>
<span data-ttu-id="3cd31-112">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span><span class="sxs-lookup"><span data-stu-id="3cd31-112">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).</span></span>  <span data-ttu-id="3cd31-113">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="3cd31-113">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

<span data-ttu-id="3cd31-114">Merhaba iskelet uygulama için basit bir API tüm hello Demirbaş kod içerir, ancak tüm hello kimlikle ilgili parçaları eksik.</span><span class="sxs-lookup"><span data-stu-id="3cd31-114">hello skeleton app includes all hello boilerplate code for a simple API, but is missing all of hello identity-related pieces.</span></span> <span data-ttu-id="3cd31-115">Toofollow boyunca istemiyorsanız, bunun yerine, kopyalayabilir veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3cd31-115">If you don't want toofollow along, you can instead clone or [download hello completed sample](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).</span></span>

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="3cd31-116">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="3cd31-116">Register an app</span></span>
<span data-ttu-id="3cd31-117">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="3cd31-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="3cd31-118">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="3cd31-118">Make sure to:</span></span>

* <span data-ttu-id="3cd31-119">Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="3cd31-119">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>

<span data-ttu-id="3cd31-120">Bu visual studio çözümü "basit bir WPF uygulaması olan bir TodoListClient", de içerir.</span><span class="sxs-lookup"><span data-stu-id="3cd31-120">This visual studio solution also contains a "TodoListClient", which is a simple WPF app.</span></span>  <span data-ttu-id="3cd31-121">Merhaba TodoListClient nasıl bir kullanıcı oturum açtığında kullanılan toodemonstrate olduğundan ve bir istemci nasıl verebilir tooyour Web API ister.</span><span class="sxs-lookup"><span data-stu-id="3cd31-121">hello TodoListClient is used toodemonstrate how a user signs-in and how a client can issue requests tooyour Web API.</span></span>  <span data-ttu-id="3cd31-122">Merhaba TodoListClient ve hello TodoListService hello tarafından bu durumda, gösterilen aynı uygulama.</span><span class="sxs-lookup"><span data-stu-id="3cd31-122">In this case, both hello TodoListClient and hello TodoListService are represented by hello same app.</span></span>  <span data-ttu-id="3cd31-123">tooconfigure TodoListClient Merhaba, ayrıca gerekir:</span><span class="sxs-lookup"><span data-stu-id="3cd31-123">tooconfigure hello TodoListClient, you should also:</span></span>

* <span data-ttu-id="3cd31-124">Merhaba eklemek **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="3cd31-124">Add hello **Mobile** platform for your app.</span></span>

## <a name="install-owin"></a><span data-ttu-id="3cd31-125">OWIN yükleme</span><span class="sxs-lookup"><span data-stu-id="3cd31-125">Install OWIN</span></span>
<span data-ttu-id="3cd31-126">Bir uygulama kaydınız, sipariş toovalidate gelen istekleri & belirteçleri hello v2.0 uç noktası ile uygulama toocommunicate yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cd31-126">Now that you’ve registered an app, you need tooset up your app toocommunicate with hello v2.0 endpoint in order toovalidate incoming requests & tokens.</span></span>

* <span data-ttu-id="3cd31-127">toobegin, hello çözümü açın ve hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello TodoListService proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3cd31-127">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a><span data-ttu-id="3cd31-128">OAuth kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3cd31-128">Configure OAuth authentication</span></span>
* <span data-ttu-id="3cd31-129">Adlı bir OWIN başlangıç sınıfı toohello TodoListService projesi eklemek `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="3cd31-129">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="3cd31-130">Merhaba projeyi sağ tıklayarak--> **Ekle** --> **yeni öğe** "OWIN" arayın.</span><span class="sxs-lookup"><span data-stu-id="3cd31-130">Right click on hello project --> **Add** --> **New Item** --> Search for “OWIN”.</span></span>  <span data-ttu-id="3cd31-131">Merhaba OWIN ara yazılımı hello çağırılır `Configuration(…)` uygulamanız başladığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3cd31-131">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>
* <span data-ttu-id="3cd31-132">Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup` -zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="3cd31-132">Change hello class declaration too`public partial class Startup` - we’ve already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="3cd31-133">Merhaba, `Configuration(…)` yöntemi çağrısı tooConfgureAuth(...) tooset web uygulamanız için kimlik doğrulaması kurma olun.</span><span class="sxs-lookup"><span data-stu-id="3cd31-133">In hello `Configuration(…)` method, make a call tooConfgureAuth(…) tooset up authentication for your web app.</span></span>

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* <span data-ttu-id="3cd31-134">Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(…)` hello Web API tooaccept belirteçleri hello v2.0 uç noktasından ayarlayacaktır yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3cd31-134">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method, which will set up hello Web API tooaccept tokens from hello v2.0 endpoint.</span></span>

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* <span data-ttu-id="3cd31-135">Kullanabileceğiniz artık `[Authorize]` denetleyicileri ve eylemleri OAuth 2.0 taşıyıcı kimlik doğrulaması ile tooprotect öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="3cd31-135">Now you can use `[Authorize]` attributes tooprotect your controllers and actions with OAuth 2.0 bearer authentication.</span></span>  <span data-ttu-id="3cd31-136">Merhaba tasarlamanız `Controllers\TodoListController.cs` bir authorize etiketiyle sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3cd31-136">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span>  <span data-ttu-id="3cd31-137">Bu sayfaya erişmeden önce bu hello kullanıcı toosign zorlar.</span><span class="sxs-lookup"><span data-stu-id="3cd31-137">This will force hello user toosign in before accessing that page.</span></span>

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* <span data-ttu-id="3cd31-138">Ne zaman bir yetkili çağıran başarıyla çağırır hello birini `TodoListController` API'leri, hello eylem erişim tooinformation hello çağıran hakkında.</span><span class="sxs-lookup"><span data-stu-id="3cd31-138">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span>  <span data-ttu-id="3cd31-139">OWIN sağlar erişim toohello talep hello taşıyıcı belirteci hello aracılığıyla içinde `ClaimsPrincpal` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3cd31-139">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* <span data-ttu-id="3cd31-140">Son olarak, hello açmak `web.config` hello TodoListService proje hello kökünde bulunan dosya ve hello yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="3cd31-140">Finally, open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="3cd31-141">`ida:Audience` Hello olan **uygulama kimliği** hello portalda girdiğiniz hello uygulamasının.</span><span class="sxs-lookup"><span data-stu-id="3cd31-141">Your `ida:Audience` is hello **Application Id** of hello app that you entered in hello portal.</span></span>

## <a name="configure-hello-client-app"></a><span data-ttu-id="3cd31-142">Merhaba istemci uygulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3cd31-142">Configure hello client app</span></span>
<span data-ttu-id="3cd31-143">Eylemin hello Yapılacaklar listesi hizmeti görebilmek hello v2.0 uç noktasından belirteç almak ve çağrıları toohello hizmeti hale tooconfigure hello Yapılacaklar listesi istemci gerekir.</span><span class="sxs-lookup"><span data-stu-id="3cd31-143">Before you can see hello Todo List Service in action, you need tooconfigure hello Todo List Client so it can get tokens from hello v2.0 endpoint and make calls toohello service.</span></span>

* <span data-ttu-id="3cd31-144">Merhaba TodoListClient projeyi açın `App.config` ve hello yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="3cd31-144">In hello TodoListClient project, open `App.config` and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="3cd31-145">`ida:ClientId` Uygulama hello portalından kopyaladığınız kimliği.</span><span class="sxs-lookup"><span data-stu-id="3cd31-145">Your `ida:ClientId` Application Id you copied from hello portal.</span></span>

<span data-ttu-id="3cd31-146">Son olarak, temiz, yapı ve her proje çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="3cd31-146">Finally, clean, build and run each project!</span></span>  <span data-ttu-id="3cd31-147">Artık hem kişisel Microsoft hesaplarını gelen belirteçleri ve iş veya Okul hesapları kabul eden bir .NET MVC Web API vardır.</span><span class="sxs-lookup"><span data-stu-id="3cd31-147">You now have a .NET MVC Web API that accepts tokens from both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="3cd31-148">Merhaba TodoListClient oturum ve arama, web API tooadd görevleri toohello kullanıcının yapılacaklar listesi.</span><span class="sxs-lookup"><span data-stu-id="3cd31-148">Sign into hello TodoListClient, and call your web api tooadd tasks toohello user's To-Do list.</span></span>

<span data-ttu-id="3cd31-149">Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3cd31-149">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="3cd31-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3cd31-150">Next steps</span></span>
<span data-ttu-id="3cd31-151">Artık ek konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cd31-151">You can now move onto additional topics.</span></span>  <span data-ttu-id="3cd31-152">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3cd31-152">You may want tootry:</span></span>

[<span data-ttu-id="3cd31-153">Bir Web uygulamasından Web API'si çağırma >></span><span class="sxs-lookup"><span data-stu-id="3cd31-153">Calling a Web API from a Web App >></span></span>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

<span data-ttu-id="3cd31-154">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="3cd31-154">For additional resources, check out:</span></span>

* [<span data-ttu-id="3cd31-155">Merhaba v2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="3cd31-155">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="3cd31-156">StackOverflow "azure-active-directory" etiketi >></span><span class="sxs-lookup"><span data-stu-id="3cd31-156">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="3cd31-157">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="3cd31-157">Get security updates for our products</span></span>
<span data-ttu-id="3cd31-158">Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="3cd31-158">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
