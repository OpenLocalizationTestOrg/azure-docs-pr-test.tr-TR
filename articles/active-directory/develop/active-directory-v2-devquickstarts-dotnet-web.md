---
title: "Azure AD v2.0 .NET web uygulaması oturum Başlarken | Microsoft Docs"
description: "Kullanıcıların hem kişisel Microsoft Account oturum ve iş veya Okul hesapları imzalar .NET MVC Web uygulaması oluşturma."
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
ms.openlocfilehash: ba5bdf7daba6086b70aec54ebe25d4445fa708c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-net-mvc-web-app"></a><span data-ttu-id="a05d1-103">Oturum açma bir .NET MVC web uygulaması'na ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a05d1-103">Add sign-in to an .NET MVC web app</span></span>
<span data-ttu-id="a05d1-104">V2.0 uç noktası ile kolayca web uygulamalarınızı hem kişisel Microsoft hesapları için destek ile kimlik doğrulaması ve iş veya Okul hesapları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-104">With the v2.0 endpoint, you can quickly add authentication to your web apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="a05d1-105">ASP.NET web uygulamalarında bunu .NET Framework 4. 5 ' dahil Microsoft'un OWIN ara yazılımı kullanarak gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-105">In ASP.NET web apps, you can accomplish this using Microsoft's OWIN middleware included in .NET Framework 4.5.</span></span>

> [!NOTE]
> <span data-ttu-id="a05d1-106">Tüm Azure Active Directory senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a05d1-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="a05d1-107">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="a05d1-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

 <span data-ttu-id="a05d1-108">Burada size kullanıcı oturum açma, kullanıcı hakkındaki bazı bilgileri görüntülemek ve uygulama dışı kullanıcı oturum OWIN kullanan bir web uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a05d1-108">Here we'll build an web app that uses OWIN to sign the user in, display some information about the user, and sign the user out of the app.</span></span>

## <a name="download"></a><span data-ttu-id="a05d1-109">İndir</span><span class="sxs-lookup"><span data-stu-id="a05d1-109">Download</span></span>
<span data-ttu-id="a05d1-110">Bu öğretici için kod [GitHub'da](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet) korunur.</span><span class="sxs-lookup"><span data-stu-id="a05d1-110">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet).</span></span>  <span data-ttu-id="a05d1-111">İzlemek için [uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="a05d1-111">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

<span data-ttu-id="a05d1-112">De Bu öğretici sonunda tamamlanmış uygulama sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a05d1-112">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="a05d1-113">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="a05d1-113">Register an app</span></span>
<span data-ttu-id="a05d1-114">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a05d1-114">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="a05d1-115">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="a05d1-115">Make sure to:</span></span>

* <span data-ttu-id="a05d1-116">Aşağı kopyalama **uygulama kimliği** uygulamanıza atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="a05d1-116">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="a05d1-117">Ekleme **Web** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="a05d1-117">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="a05d1-118">Doğru girin **yeniden yönlendirme URI'si**.</span><span class="sxs-lookup"><span data-stu-id="a05d1-118">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="a05d1-119">Bu öğretici için varsayılan burada kimlik doğrulama yanıtları yönlendirileceğini - Azure AD ile yeniden yönlendirme URI'si gösterir `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a05d1-119">The redirect uri indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `https://localhost:44326/`.</span></span>

## <a name="install--configure-owin-authentication"></a><span data-ttu-id="a05d1-120">Yükleme & OWIN kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a05d1-120">Install & configure OWIN authentication</span></span>
<span data-ttu-id="a05d1-121">Burada, Openıd Connect kimlik doğrulama protokolünü kullanmak için OWIN ara yazılımı yapılandıracağız.</span><span class="sxs-lookup"><span data-stu-id="a05d1-121">Here, we'll configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="a05d1-122">OWIN oturum açma ve oturum kapatma isteklerini yürütmek, kullanıcının oturumunu yönetmek ve başka şeyler arasında kullanıcı hakkında bilgi almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a05d1-122">OWIN will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

1. <span data-ttu-id="a05d1-123">Başlamak için açın `web.config` dosya proje kök dizininde ve uygulamanızın yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="a05d1-123">To begin, open the `web.config` file in the root of the project, and enter your app's configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="a05d1-124">`ida:ClientId` Olan **uygulama kimliği** kayıt portalında uygulamanıza atanan.</span><span class="sxs-lookup"><span data-stu-id="a05d1-124">The `ida:ClientId` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="a05d1-125">`ida:RedirectUri` Olan **yeniden yönlendirme URI'si** portalda girdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-125">The `ida:RedirectUri` is the **Redirect Uri** you entered in the portal.</span></span>

2. <span data-ttu-id="a05d1-126">Ardından, OWIN ara yazılımı NuGet paketleri Paket Yöneticisi konsolu kullanılarak projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a05d1-126">Next, add the OWIN middleware NuGet packages to the project using the Package Manager Console.</span></span>

        ```
        PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
        PM> Install-Package Microsoft.Owin.Security.Cookies
        PM> Install-Package Microsoft.Owin.Host.SystemWeb
        ```  

3. <span data-ttu-id="a05d1-127">"OWIN başlangıç adlı sınıfı" projeye eklemek `Startup.cs` sağ tıklatın projeye--> **Ekle** --> **yeni öğe** "OWIN" arayın.</span><span class="sxs-lookup"><span data-stu-id="a05d1-127">Add an "OWIN Startup Class" to the project called `Startup.cs`  Right click on the project --> **Add** --> **New Item** --> Search for "OWIN".</span></span>  <span data-ttu-id="a05d1-128">OWIN ara yazılımı, uygulamanız başlatıldığında `Configuration(...)` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="a05d1-128">The OWIN middleware will invoke the `Configuration(...)` method when your app starts.</span></span>
4. <span data-ttu-id="a05d1-129">Sınıf bildirimi değiştirme `public partial class Startup` -zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="a05d1-129">Change the class declaration to `public partial class Startup` - we've already implemented part of this class for you in another file.</span></span>  <span data-ttu-id="a05d1-130">İçinde `Configuration(...)` yöntemi, bir web uygulamanız için kimlik doğrulaması ayarlamak için ConfigureAuth(...) çağrı yapma</span><span class="sxs-lookup"><span data-stu-id="a05d1-130">In the `Configuration(...)` method, make a call to ConfigureAuth(...) to set up authentication for your web app</span></span>  

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

5. <span data-ttu-id="a05d1-131">Dosyayı açmak `App_Start\Startup.Auth.cs` ve uygulamanıza `ConfigureAuth(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a05d1-131">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span>  <span data-ttu-id="a05d1-132">Sağladığınız içinde parametreleri `OpenIdConnectAuthenticationOptions` uygulamanız için Azure AD ile iletişim kurmak için koordinatları olarak hizmet verecektir.</span><span class="sxs-lookup"><span data-stu-id="a05d1-132">The parameters you provide in `OpenIdConnectAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>  <span data-ttu-id="a05d1-133">Tanımlama bilgisi kimlik doğrulamasını kurmanız gerekir - Openıd Connect Ara kapsar altında tanımlama bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a05d1-133">You'll also need to set up Cookie Authentication - the OpenID Connect middleware uses cookies underneath the covers.</span></span>

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

## <a name="send-authentication-requests"></a><span data-ttu-id="a05d1-134">Kimlik doğrulama isteklerini gönderme</span><span class="sxs-lookup"><span data-stu-id="a05d1-134">Send authentication requests</span></span>
<span data-ttu-id="a05d1-135">Uygulamanız artık Openıd Connect kimlik doğrulama protokolü kullanarak v2.0 uç noktası ile iletişim kurmak için düzgün şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a05d1-135">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="a05d1-136">OWIN geçen tüm kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumu koruyarak çirkin ayrıntılarını verdiğiniz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-136">OWIN has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="a05d1-137">Kalan tek şey, kullanıcılarınızın bir şekilde oturum açabilir ve oturumu vermek için.</span><span class="sxs-lookup"><span data-stu-id="a05d1-137">All that remains is to give your users a way to sign in and sign out.</span></span>

- <span data-ttu-id="a05d1-138">Kullanabilirsiniz, kullanıcı oturum açtığında belirli bir sayfaya erişmeden önce gerektirecek şekilde denetleyicilerinizi etiketlerinde yetkilendirmek.</span><span class="sxs-lookup"><span data-stu-id="a05d1-138">You can use authorize tags in your controllers to require that user signs in before accessing a certain page.</span></span>  <span data-ttu-id="a05d1-139">Açık `Controllers\HomeController.cs`ve ekleme `[Authorize]` hakkında denetleyicisine etiketi.</span><span class="sxs-lookup"><span data-stu-id="a05d1-139">Open `Controllers\HomeController.cs`, and add the `[Authorize]` tag to the About controller.</span></span>
        
        ```C#
        [Authorize]
        public ActionResult About()
        {
          ...
        ```

- <span data-ttu-id="a05d1-140">OWIN, doğrudan kimlik doğrulama isteklerini kodunuzu içinde vermek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-140">You can also use OWIN to directly issue authentication requests from within your code.</span></span>  <span data-ttu-id="a05d1-141">Açık `Controllers\AccountController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a05d1-141">Open `Controllers\AccountController.cs`.</span></span>  <span data-ttu-id="a05d1-142">SignIn() ve SignOut() Eylemler, Openıd Connect sınama ve oturum kapatma isteklerini sırasıyla gönderin.</span><span class="sxs-lookup"><span data-stu-id="a05d1-142">In the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests, respectively.</span></span>

        ```C#
        public void SignIn()
        {
            // Send an OpenID Connect sign-in request.
            if (!Request.IsAuthenticated)
            {
                HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
            }
        }
        
        // BUGBUG: Ending a session with the v2.0 endpoint is not yet supported.  Here, we just end the session with the web app.  
        public void SignOut()
        {
            // Send an OpenID Connect sign-out request.
            HttpContext.GetOwinContext().Authentication.SignOut(CookieAuthenticationDefaults.AuthenticationType);
            Response.Redirect("/");
        }
        ```

- <span data-ttu-id="a05d1-143">Şimdi, açmak `Views\Shared\_LoginPartial.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a05d1-143">Now, open `Views\Shared\_LoginPartial.cshtml`.</span></span>  <span data-ttu-id="a05d1-144">Bu, kullanıcı uygulamanızın oturum açma ve oturum kapatma bağlantıları göstermek ve kullanıcının adını görünümünde yazdırmak yerdir.</span><span class="sxs-lookup"><span data-stu-id="a05d1-144">This is where you'll show the user your app's sign-in and sign-out links, and print out the user's name in a view.</span></span>

        ```HTML
        @if (Request.IsAuthenticated)
        {
            <text>
                <ul class="nav navbar-nav navbar-right">
                    <li class="navbar-text">
        
                        @*The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves.*@
        
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

## <a name="display-user-information"></a><span data-ttu-id="a05d1-145">Kullanıcı bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a05d1-145">Display user information</span></span>
<span data-ttu-id="a05d1-146">Openıd Connect ile kullanıcıların kimlik doğrulamasını yaparken, v2.0 uç noktası bir id_token talep ya da kullanıcı hakkında onaylar içeren bir uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="a05d1-146">When authenticating users with OpenID Connect, the v2.0 endpoint returns an id_token to the app that contains claims, or assertions about the user.</span></span>  <span data-ttu-id="a05d1-147">Uygulamanızı kişiselleştirmek için bu talepler kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a05d1-147">You can use these claims to personalize your app:</span></span>

- <span data-ttu-id="a05d1-148">`Controllers\HomeController.cs` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="a05d1-148">Open the `Controllers\HomeController.cs` file.</span></span>  <span data-ttu-id="a05d1-149">Denetleyicilerinizi kullanıcının talepleri erişebilmeniz için `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a05d1-149">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

        ```C#
        [Authorize]
        public ActionResult About()
        {
            ViewBag.Name = ClaimsPrincipal.Current.FindFirst("name").Value;
        
            // The object ID claim will only be emitted for work or school accounts at this time.
            Claim oid = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier");
            ViewBag.ObjectId = oid == null ? string.Empty : oid.Value;
        
            // The 'preferred_username' claim can be used for showing the user's primary way of identifying themselves
            ViewBag.Username = ClaimsPrincipal.Current.FindFirst("preferred_username").Value;
        
            // The subject or nameidentifier claim can be used to uniquely identify the user
            ViewBag.Subject = ClaimsPrincipal.Current.FindFirst("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier").Value;
        
            return View();
        }
        ```

## <a name="run"></a><span data-ttu-id="a05d1-150">Çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a05d1-150">Run</span></span>
<span data-ttu-id="a05d1-151">Son olarak, yapı ve uygulamanızı çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="a05d1-151">Finally, build and run your app!</span></span>   <span data-ttu-id="a05d1-152">Kişisel bir Microsoft Account veya bir iş veya Okul hesabınızla oturum açın ve kullanıcının kimliğini üst gezinti çubuğunda nasıl yansıtılır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a05d1-152">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the top navigation bar.</span></span>  <span data-ttu-id="a05d1-153">Artık, hem kişisel hem de iş/Okul hesaplarını ile kullanıcıların kimliklerini doğrulayabilir endüstri standardı protokoller kullanılarak güvenli bir web uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-153">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="a05d1-154">(Yapılandırma değerleriniz olmadan) tamamlanan örnek, başvuru için [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a05d1-154">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIdConnect-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="a05d1-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a05d1-155">Next steps</span></span>
<span data-ttu-id="a05d1-156">Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-156">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="a05d1-157">Denemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a05d1-157">You may want to try:</span></span>

[<span data-ttu-id="a05d1-158">Bir Web API ile güvenli v2.0 uç noktası >></span><span class="sxs-lookup"><span data-stu-id="a05d1-158">Secure a Web API with the the v2.0 endpoint >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

<span data-ttu-id="a05d1-159">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="a05d1-159">For additional resources, check out:</span></span>

* [<span data-ttu-id="a05d1-160">V2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="a05d1-160">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="a05d1-161">StackOverflow "azure-active-directory" etiketi >></span><span class="sxs-lookup"><span data-stu-id="a05d1-161">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="a05d1-162">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="a05d1-162">Get security updates for our products</span></span>
<span data-ttu-id="a05d1-163">[Bu sayfayı](https://technet.microsoft.com/security/dd252948) ziyaret ederek ve Güvenlik Önerisi Uyarılarına abone olarak güvenlik olaylarının ne zaman ortaya çıkacağı hakkında bildirimleri almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a05d1-163">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>
