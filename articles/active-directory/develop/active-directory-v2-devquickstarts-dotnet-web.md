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
# <a name="add-sign-in-tooan-net-mvc-web-app"></a><span data-ttu-id="23b68-103">Oturum açma tooan .NET MVC web uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="23b68-103">Add sign-in tooan .NET MVC web app</span></span>
<span data-ttu-id="23b68-104">Merhaba v2.0 uç noktası ile kimlik doğrulaması tooyour web uygulamaları hem kişisel Microsoft hesapları için destek ve iş veya Okul hesapları ile kolayca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23b68-104">With hello v2.0 endpoint, you can quickly add authentication tooyour web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="23b68-105">ASP.NET web uygulamalarında bunu .NET Framework 4. 5 ' dahil Microsoft'un OWIN ara yazılımı kullanarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23b68-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="23b68-106">Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="23b68-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="23b68-107">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="23b68-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="23b68-108">Burada biz OWIN toosign hello kullanıcı, görüntü kullanan bir web uygulaması hello kullanıcı hakkında bazı bilgiler oluşturma ve hello uygulama dışı kullanıcı oturum hello.</span><span class="sxs-lookup"><span data-stu-id="23b68-108">Here we'll build an web app that uses OWIN toosign hello user in, display some information about hello user, and sign hello user out of hello app.</span></span>

## <a name="download"></a><span data-ttu-id="23b68-109">İndir</span><span class="sxs-lookup"><span data-stu-id="23b68-109">Download</span></span>
<span data-ttu-id="23b68-110">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span><span class="sxs-lookup"><span data-stu-id="23b68-110">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="23b68-111">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="23b68-111">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="23b68-112">Tamamlanan hello uygulama hello de bu öğreticinin sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="23b68-112">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="23b68-113">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="23b68-113">Register an app</span></span>
<span data-ttu-id="23b68-114">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="23b68-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="23b68-115">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="23b68-115">Make sure to:</span></span>

* <span data-ttu-id="23b68-116">Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="23b68-116">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="23b68-117">Merhaba eklemek **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="23b68-117">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="23b68-118">Merhaba doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="23b68-118">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="23b68-119">Merhaba yeniden yönlendirme URI'si gösterir hello varsayılan Bu öğretici için burada kimlik doğrulama yanıtları yönlendirileceğini - tooAzure AD `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="23b68-119">hello redirect uri indicates tooAzure AD where authentication responses should be directed - hello default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="23b68-120">Yükleme & OWIN kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="23b68-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="23b68-121">Burada, biz hello OWIN ara yazılımı toouse hello Openıd Connect kimlik doğrulama protokolünü yapılandıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="23b68-121">Here, we'll configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="23b68-122">OWIN kullanılan tooissue oturum açma ve oturum kapatma isteklerini olması, hello kullanıcının oturumunu yönetmek ve başka şeyler arasında hello kullanıcı hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="23b68-122">OWIN will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

1. <span data-ttu-id="23b68-123">toobegin, açık hello `web.config` hello proje hello kökünde bulunan dosya ve hello uygulamanızın yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="23b68-123">toobegin, open hello `web.config` file in hello root of hello project, and enter your app's configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="23b68-124">Merhaba `ida:ClientId` hello olan **uygulama kimliği** tooyour uygulama hello kayıt Portalı'nda atanmış.</span><span class="sxs-lookup"><span data-stu-id="23b68-124">hello `ida:ClientId` is hello **Application Id** assigned tooyour app in hello registration portal.</span></span>
  * <span data-ttu-id="23b68-125">Merhaba `ida:RedirectUri` hello olan **yeniden yönlendirme URI'si** hello portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="23b68-125">hello `ida:RedirectUri` is hello **Redirect Uri** you entered in hello portal.</span></span>

2. <span data-ttu-id="23b68-126">Ardından, hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="23b68-126">Next, add hello OWIN middleware NuGet packages toohello project using hello Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="23b68-127">"OWIN başlangıç sınıfı" toohello projesinde adlı Ekle `Startup.cs` sağ tıklatın hello projede--> **Ekle** --> **yeni öğe** "OWIN" arayın.</span><span class="sxs-lookup"><span data-stu-id="23b68-127">Add an "OWIN Startup Class" toohello project called `Startup.cs`  Right click on hello project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="23b68-128">Merhaba OWIN ara yazılımı hello çağırılır `Configuration(...)` uygulamanız başladığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="23b68-128">hello OWIN middleware will invoke hello `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="23b68-129">Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup` -zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="23b68-129">Change hello class declaration too`public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="23b68-130">Merhaba, `Configuration(...)` yöntemi çağrısı tooConfigureAuth(...) tooset web uygulamanız için kimlik doğrulaması kurma olun</span><span class="sxs-lookup"><span data-stu-id="23b68-130">In hello `Configuration(...)` method, make a call tooConfigureAuth(...) tooset up authentication for your web app</span></span>  

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

5. <span data-ttu-id="23b68-131">Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="23b68-131">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="23b68-132">Merhaba, sağladığınız parametreler `OpenIdConnectAuthenticationOptions` , uygulama toocommunicate Azure AD ile koordinatları olarak hizmet verecektir.</span><span class="sxs-lookup"><span data-stu-id="23b68-132">hello parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>  <span data-ttu-id="23b68-133">Tanımlama bilgisi kimlik doğrulamasını oluşturan tooset ayrıca gerekir - hello Openıd Connect Ara hello kapsar altında tanımlama bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="23b68-133">You'll also need tooset up Cookie Authentication - hello OpenID Connect middleware uses cookies underneath hello covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="23b68-134">Kimlik doğrulama isteklerini gönderme</span><span class="sxs-lookup"><span data-stu-id="23b68-134">Send authentication requests</span></span>
<span data-ttu-id="23b68-135">Uygulamanızı hello Openıd Connect kimlik doğrulama protokolünü kullanarak hello v2.0 uç noktası ile düzgün şekilde yapılandırılmış toocommunicate sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="23b68-135">Your app is now properly configured toocommunicate with hello v2.0 endpoint using hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="23b68-136">OWIN geçen tüm kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumu koruyarak hello çirkin ayrıntılarını verdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="23b68-136">OWIN has taken care of all of hello ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="23b68-137">Tüm bu kalır, kullanıcılarınızın toogive olan bir şekilde toosign ve oturum kapatma.</span><span class="sxs-lookup"><span data-stu-id="23b68-137">All that remains is toogive your users a way toosign in and sign out.</span></span>

- <span data-ttu-id="23b68-138">Kullanabileceğiniz etiketleri yetkilendirmek, denetleyicileri toorequire, belirli bir sayfaya erişmeden önce oturum açtığında.</span><span class="sxs-lookup"><span data-stu-id="23b68-138">You can use authorize tags in your controllers toorequire that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="23b68-139">Açık `Controllers\HomeController.cs`ve hello ekleyin `[Authorize]` Denetleyicisi hakkında toohello etiketi.</span><span class="sxs-lookup"><span data-stu-id="23b68-139">Open `Controllers\HomeController.cs`, and add hello `[Authorize]` tag toohello About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="23b68-140">OWIN toodirectly sorunu kimlik doğrulama isteklerini kodunuzu içinde de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23b68-140">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span>  <span data-ttu-id="23b68-141">Açık `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="23b68-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="23b68-142">Merhaba SignIn() ve SignOut() Eylemler, Openıd Connect sınama ve oturum kapatma isteklerini sırasıyla gönderin.</span><span class="sxs-lookup"><span data-stu-id="23b68-142">In hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

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

- <span data-ttu-id="23b68-143">Şimdi, açmak `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="23b68-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="23b68-144">Bu, hello kullanıcı uygulamanızın oturum açma ve oturum kapatma bağlantıları göstermek ve bir görünümünde hello kullanıcının adını yazdırmak yerdir.</span><span class="sxs-lookup"><span data-stu-id="23b68-144">This is where you'll show hello user your app's sign-in and sign-out links, and print out hello user's name in a view.</span></span>

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

## <a name="display-user-information"></a><span data-ttu-id="23b68-145">Kullanıcı bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="23b68-145">Display user information</span></span>
<span data-ttu-id="23b68-146">Openıd Connect ile kullanıcıların kimlik doğrulamasını yaparken, hello v2.0 uç talep veya onaylar hello kullanıcı hakkında içeren id_token toohello uygulama döndürür.</span><span class="sxs-lookup"><span data-stu-id="23b68-146">When authenticating users with OpenID Connect, hello v2.0 endpoint returns an id_token toohello app that contains claims, or assertions about hello user.</span></span>  <span data-ttu-id="23b68-147">Bu talep toopersonalize uygulamanızı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="23b68-147">You can use these claims toopersonalize your app:</span></span>

- <span data-ttu-id="23b68-148">Açık hello `Controllers\HomeController.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="23b68-148">Open hello `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="23b68-149">Denetleyicilerinizi hello aracılığıyla hello kullanıcının talepleri erişebilmeniz için `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.</span><span class="sxs-lookup"><span data-stu-id="23b68-149">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

## <a name="run"></a><span data-ttu-id="23b68-150">Çalıştırın</span><span class="sxs-lookup"><span data-stu-id="23b68-150">Run</span></span>
<span data-ttu-id="23b68-151">Son olarak, yapı ve uygulamanızı çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="23b68-151">Finally, build and run your app!</span></span>   <span data-ttu-id="23b68-152">Kişisel bir Microsoft Account veya bir iş veya Okul hesabınızla oturum açın ve hello kullanıcının kimliğini hello üst gezinti çubuğunda nasıl yansıtılır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="23b68-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how hello user's identity is reflected in hello top navigation bar.</span></span>  <span data-ttu-id="23b68-153">Artık, hem kişisel hem de iş/Okul hesaplarını ile kullanıcıların kimliklerini doğrulayabilir endüstri standardı protokoller kullanılarak güvenli bir web uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="23b68-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="23b68-154">Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="23b68-154">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="23b68-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23b68-155">Next steps</span></span>
<span data-ttu-id="23b68-156">Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23b68-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="23b68-157">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="23b68-157">You may want tootry:</span></span>

[<span data-ttu-id="23b68-158">Merhaba hello v2.0 uç noktası ile bir Web API'SİNİN güvenliğini >></span><span class="sxs-lookup"><span data-stu-id="23b68-158">Secure a Web API with hello hello v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="23b68-159">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="23b68-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="23b68-160">Merhaba v2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="23b68-160">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="23b68-161">StackOverflow "azure-active-directory" etiketi >></span><span class="sxs-lookup"><span data-stu-id="23b68-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="23b68-162">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="23b68-162">Get security updates for our products</span></span>
<span data-ttu-id="23b68-163">Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="23b68-163">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>
