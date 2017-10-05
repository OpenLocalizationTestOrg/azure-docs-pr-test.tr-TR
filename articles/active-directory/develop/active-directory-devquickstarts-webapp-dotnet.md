---
title: "Azure AD .NET web uygulaması Başlarken | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleşen bir .NET MVC web uygulaması oluşturun."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e15a41a4-dc5d-4c90-b3fe-5dc33b9a1e96
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 7ac5d3e5cc28ead993e159d003244e6451acb0cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="3afa1-103">ASP.NET web uygulaması oturum açma ve Azure AD ile oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="3afa1-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="3afa1-104">Yalnızca birkaç kod satırıyla, tek bir oturum açma ve oturum kapatma sağlayarak, Azure Active Directory (Azure AD), web uygulaması kimlik yönetimi dış için kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="3afa1-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you to outsource web-app identity management.</span></span> <span data-ttu-id="3afa1-105">.NET (OWIN) ara yazılımı için açık Web arabirimi Microsoft uyarlamasını kullanarak ASP.NET web uygulamaları ve kullanıcıların imzalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3afa1-105">You can sign users in and out of ASP.NET web apps by using the Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="3afa1-106">OWIN ara yazılımı topluluk odaklı .NET Framework 4. 5 ' bulunur.</span><span class="sxs-lookup"><span data-stu-id="3afa1-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="3afa1-107">Bu makale için OWIN kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="3afa1-107">This article shows how to use OWIN to:</span></span>

* <span data-ttu-id="3afa1-108">Kullanıcıların kimlik sağlayıcısı olarak Azure AD kullanarak web uygulamaları için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-108">Sign users in to web apps by using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="3afa1-109">Bazı kullanıcı bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3afa1-109">Display some user information.</span></span>
* <span data-ttu-id="3afa1-110">Kullanıcıların uygulamaları dışında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-110">Sign users out of the apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="3afa1-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="3afa1-111">Before you get started</span></span>
* <span data-ttu-id="3afa1-112">Karşıdan [uygulama çatıyı](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) veya karşıdan [tamamlanan örnek](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="3afa1-112">Download the [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download the [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="3afa1-113">Ayrıca uygulamanın kaydedileceği Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3afa1-113">You also need an Azure AD tenant in which to register the app.</span></span> <span data-ttu-id="3afa1-114">Azure AD kiracısı, zaten yoksa [edinebileceğinizi öğrenin](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="3afa1-114">If you don't already have an Azure AD tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="3afa1-115">Hazır olduğunuzda İleri dört bölümlerdeki yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-115">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-register-the-new-app-with-azure-ad"></a><span data-ttu-id="3afa1-116">1. adım: Azure AD ile yeni uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="3afa1-116">Step 1: Register the new app with Azure AD</span></span>
<span data-ttu-id="3afa1-117">Kullanıcıların kimliğini doğrulamak için önce aşağıdakileri yaparak kiracınızda kaydetmeniz uygulama ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="3afa1-117">To set up the app to authenticate users, first register it in your tenant by doing the following:</span></span>

1. <span data-ttu-id="3afa1-118">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-118">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3afa1-119">Üst çubuğunda hesabınızın adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-119">On the top bar, click your account name.</span></span> <span data-ttu-id="3afa1-120">Altında **Directory** listesinde, uygulama kaydetmek istediğiniz Active Directory Kiracı seçin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-120">Under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="3afa1-121">Tıklatın **daha Hizmetleri** sol bölmesinde ve seçip **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3afa1-121">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="3afa1-122">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3afa1-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="3afa1-123">Yeni bir oluşturmak için istemleri izleyin **Web uygulaması ve/veya Webapı**.</span><span class="sxs-lookup"><span data-stu-id="3afa1-123">Follow the prompts to create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="3afa1-124">**Ad** kullanıcılara uygulamasının açıklar.</span><span class="sxs-lookup"><span data-stu-id="3afa1-124">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="3afa1-125">**Oturum açma URL'si** uygulamasının temel URL'si.</span><span class="sxs-lookup"><span data-stu-id="3afa1-125">**Sign-On URL** is the base URL of the app.</span></span> <span data-ttu-id="3afa1-126">Çatıyı ait varsayılan URL'dir https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="3afa1-126">The skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="3afa1-127">Kayıt tamamladıktan sonra Azure AD uygulama benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="3afa1-127">After you've completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="3afa1-128">Sonraki bölümlerde kullanmak için uygulama sayfasında değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-128">Copy the value from the app page to use in the next sections.</span></span>
7. <span data-ttu-id="3afa1-129">Gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-129">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="3afa1-130">**Uygulama kimliği URI'si** uygulama için benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="3afa1-130">The **App ID URI** is a unique identifier for the app.</span></span> <span data-ttu-id="3afa1-131">Adlandırma kuralı `https://<tenant-domain>/<app-name>` (örneğin, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="3afa1-131">The naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="3afa1-132">2. adım: uygulama OWIN kimlik doğrulaması ardışık kullanmak için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="3afa1-132">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="3afa1-133">Bu adımda, Openıd Connect kimlik doğrulama protokolünü kullanmak için OWIN ara yazılımını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-133">In this step, you configure the OWIN middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="3afa1-134">Oturum açma ve oturum kapatma isteklerini yürütmek, kullanıcı oturumlarını yönetmek, kullanıcı bilgilerini almak ve benzeri için OWIN kullanın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-134">You use OWIN to issue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="3afa1-135">Başlamak için Paket Yöneticisi konsolu kullanılarak OWIN ara yazılımı NuGet paketlerini projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-135">To begin, add the OWIN middleware NuGet packages to the project by using the Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="3afa1-136">Bir OWIN başlangıç sınıfı adlı projeye eklemek için `Startup.cs`, projeye sağ tıklayın, seçin **Ekle**seçin **yeni öğe**, arayın ve sonra **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="3afa1-136">To add an OWIN Startup class to the project called `Startup.cs`, right-click the project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="3afa1-137">OWIN ara yazılımı çağırır **Configuration(...)**  uygulama başlatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3afa1-137">The OWIN middleware invokes the **Configuration(...)** method when the app starts.</span></span>
3. <span data-ttu-id="3afa1-138">Sınıf bildirimi değiştirme `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="3afa1-138">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="3afa1-139">Zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="3afa1-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="3afa1-140">İçinde **Configuration(...)**  yöntemi çağrısına duruma **ConfgureAuth(...)**  uygulaması için kimlik doğrulamasını ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="3afa1-140">In the **Configuration(...)** method, make a call to **ConfgureAuth(...)** to set up authentication for the app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="3afa1-141">App_Start\Startup.Auth.cs dosyasını açın ve ardından uygulama **ConfigureAuth(...)**  yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3afa1-141">Open the App_Start\Startup.Auth.cs file, and then implement the **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="3afa1-142">Sağladığınız içinde parametreleri *OpenIDConnectAuthenticationOptions* Azure AD ile iletişim kurmak için uygulama koordinatları olarak hizmet.</span><span class="sxs-lookup"><span data-stu-id="3afa1-142">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the app to communicate with Azure AD.</span></span> <span data-ttu-id="3afa1-143">Openıd Connect ara yazılımı arka planda tanımlama bilgileri kullandığından ayrıca tanımlama bilgisi kimlik doğrulamasını kurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3afa1-143">You also need to set up cookie authentication, because the OpenID Connect middleware uses cookies in the background.</span></span>

     ```C#
     public void ConfigureAuth(IAppBuilder app)
     {
         app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

         app.UseCookieAuthentication(new CookieAuthenticationOptions());

         app.UseOpenIdConnectAuthentication(
             new OpenIdConnectAuthenticationOptions
             {
                 ClientId = clientId,
                 Authority = authority,
                 PostLogoutRedirectUri = postLogoutRedirectUri,
                 Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = context =>
                        {
                            context.HandleResponse();
                            context.Response.Redirect("/Error?message=" + context.Exception.Message);
                            return Task.FromResult(0);
                        }
                    }
             });
     }
     ```

5. <span data-ttu-id="3afa1-144">Proje kök dizininde web.config dosyasını açın ve ardından yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="3afa1-144">Open the web.config file in the root of the project, and then enter the configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="3afa1-145">`ida:ClientId`: Azure portalında kendisinden kopyaladığınız GUID "1. adım: Azure AD ile yeni uygulamayı kaydedin."</span><span class="sxs-lookup"><span data-stu-id="3afa1-145">`ida:ClientId`: The GUID you copied from the Azure portal in "Step 1: Register the new app with Azure AD."</span></span>
  * <span data-ttu-id="3afa1-146">`ida:Tenant`: Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) adı.</span><span class="sxs-lookup"><span data-stu-id="3afa1-146">`ida:Tenant`: The name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="3afa1-147">`ida:PostLogoutRedirectUri`: Bir kullanıcı oturum kapatma isteği başarıyla tamamlandıktan sonra burada yönlendirilmesi gereken Azure AD bildirir göstergesi.</span><span class="sxs-lookup"><span data-stu-id="3afa1-147">`ida:PostLogoutRedirectUri`: The indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="3afa1-148">3. adım: Kullanım için Azure AD oturum açma ve oturum kapatma isteklerini yürütmek için OWIN</span><span class="sxs-lookup"><span data-stu-id="3afa1-148">Step 3: Use OWIN to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="3afa1-149">Uygulama artık Openıd Connect kimlik doğrulama protokolü kullanarak Azure AD ile iletişim kurmak için düzgün şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="3afa1-149">The app is now properly configured to communicate with Azure AD by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="3afa1-150">OWIN tüm kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumlarını Bakım Ayrıntıları ele.</span><span class="sxs-lookup"><span data-stu-id="3afa1-150">OWIN has handled all of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="3afa1-151">Kalan tek şey, kullanıcılarınızın bir şekilde oturum açabilir ve oturumu vermek için.</span><span class="sxs-lookup"><span data-stu-id="3afa1-151">All that remains is to give your users a way to sign in and sign out.</span></span>

1. <span data-ttu-id="3afa1-152">Kullanabileceğiniz belirli sayfalarını erişmeden önce oturum açmalarını gerektirecek şekilde denetleyicilerinizi etiketlerinde yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-152">You can use authorize tags in your controllers to require users to sign in before they access certain pages.</span></span> <span data-ttu-id="3afa1-153">Bunu yapmak için Controllers\HomeController.cs açın ve ardından ekleyin `[Authorize]` hakkında denetleyicisine etiketi.</span><span class="sxs-lookup"><span data-stu-id="3afa1-153">To do so, open Controllers\HomeController.cs, and then add the `[Authorize]` tag to the About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="3afa1-154">OWIN, doğrudan kimlik doğrulama isteklerini kodunuzu içinde vermek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3afa1-154">You can also use OWIN to directly issue authentication requests from within your code.</span></span> <span data-ttu-id="3afa1-155">Bunu yapmak için Controllers\AccountController.cs açın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-155">To do so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="3afa1-156">Ardından, SignIn() ve SignOut() Eylemler, Openıd Connect sınama ve oturum kapatma isteklerini gönderin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-156">Then, in the SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

     ```C#
     public void SignIn()
     {
         // Send an OpenID Connect sign-in request.
         if (!Request.IsAuthenticated)
         {
             HttpContext.GetOwinContext().Authentication.Challenge(new AuthenticationProperties { RedirectUri = "/" }, OpenIdConnectAuthenticationDefaults.AuthenticationType);
         }
     }
     public void SignOut()
     {
         // Send an OpenID Connect sign-out request.
         HttpContext.GetOwinContext().Authentication.SignOut(
              OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType);
     }
     ```

3. <span data-ttu-id="3afa1-157">Görünümler/paylaşılan açmak\_LoginPartial.cshtml kullanıcı uygulama oturum açma ve oturum kapatma bağlantıları göstermek için ve kullanıcının adını görünümünde yazdırmak için.</span><span class="sxs-lookup"><span data-stu-id="3afa1-157">Open Views\Shared\_LoginPartial.cshtml to show the user the app sign-in and sign-out links, and to print out the user's name in a view.</span></span>

    ```HTML
    @if (Request.IsAuthenticated)
    {
     <text>
         <ul class="nav navbar-nav navbar-right">
             <li class="navbar-text">
                 Hello, @User.Identity.Name!
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

## <a name="step-4-display-user-information"></a><span data-ttu-id="3afa1-158">4. adım: kullanıcı bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="3afa1-158">Step 4: Display user information</span></span>
<span data-ttu-id="3afa1-159">Openıd Connect ile kullanıcıların kimliğini doğrular, Azure AD bir id_token "talep" ya da kullanıcı hakkında onaylar içeren bir uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="3afa1-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token to the app that contains "claims," or assertions about the user.</span></span> <span data-ttu-id="3afa1-160">Aşağıdakileri yaparak app kişiselleştirmek için bu talepler kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3afa1-160">You can use these claims to personalize the app by doing the following:</span></span>

1. <span data-ttu-id="3afa1-161">Controllers\HomeController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-161">Open the Controllers\HomeController.cs file.</span></span> <span data-ttu-id="3afa1-162">Denetleyicilerinizi kullanıcının talepleri erişebilmeniz için `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3afa1-162">You can access the user's claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

 ```C#
 public ActionResult About()
 {
     ViewBag.Name = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Name).Value;
     ViewBag.ObjectId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
     ViewBag.GivenName = ClaimsPrincipal.Current.FindFirst(ClaimTypes.GivenName).Value;
     ViewBag.Surname = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Surname).Value;
     ViewBag.UPN = ClaimsPrincipal.Current.FindFirst(ClaimTypes.Upn).Value;

     return View();
 }
 ```

2. <span data-ttu-id="3afa1-163">Derleme ve uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-163">Build and run the app.</span></span> <span data-ttu-id="3afa1-164">Onmicrosoft.com etki alanı ile kiracınızda zaten yeni bir kullanıcı oluşturmadıysanız, bunu yapmak için gereken süre sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="3afa1-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is the time to do so.</span></span> <span data-ttu-id="3afa1-165">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="3afa1-165">Here's how:</span></span>

  <span data-ttu-id="3afa1-166">a.</span><span class="sxs-lookup"><span data-stu-id="3afa1-166">a.</span></span> <span data-ttu-id="3afa1-167">Oturum, kullanıcı oturum açabilir ve kullanıcının kimliğini üst çubuğunda nasıl yansıtılır not edin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-167">Sign in with that user, and note how the user's identity is reflected on the top bar.</span></span>

  <span data-ttu-id="3afa1-168">b.</span><span class="sxs-lookup"><span data-stu-id="3afa1-168">b.</span></span> <span data-ttu-id="3afa1-169">Oturumu kapatın ve kiracınızda başka bir kullanıcı olarak yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3afa1-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="3afa1-170">c.</span><span class="sxs-lookup"><span data-stu-id="3afa1-170">c.</span></span> <span data-ttu-id="3afa1-171">Özellikle hırslı hissediyorsanız kaydetmek ve bu uygulamayla (kendi ClientID) başka bir örneğini çalıştıran ve çoklu oturum açma eylem izleyin.</span><span class="sxs-lookup"><span data-stu-id="3afa1-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3afa1-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3afa1-172">Next steps</span></span>
<span data-ttu-id="3afa1-173">Başvuru için bkz: [tamamlanan örnek](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (yapılandırma değerleriniz olmadan).</span><span class="sxs-lookup"><span data-stu-id="3afa1-173">For reference, see [the completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="3afa1-174">Artık daha ileri seviyeli konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3afa1-174">You can now move on to more advanced topics.</span></span> <span data-ttu-id="3afa1-175">Örneğin, [Azure AD ile Web API güvenliğini](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3afa1-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
