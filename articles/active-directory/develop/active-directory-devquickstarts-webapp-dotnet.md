---
title: "Başlarken aaaAzure AD .NET web uygulaması | Microsoft Docs"
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
ms.openlocfilehash: 6d3098c9e3d7e1916ccb110c703f501ae52e788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-web-app-sign-in-and-sign-out-with-azure-ad"></a><span data-ttu-id="1ea31-103">ASP.NET web uygulaması oturum açma ve Azure AD ile oturum kapatma</span><span class="sxs-lookup"><span data-stu-id="1ea31-103">ASP.NET web app sign-in and sign-out with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="1ea31-104">Yalnızca birkaç kod satırıyla, tek bir oturum açma ve oturum kapatma sağlayarak, Azure Active Directory (Azure AD), toooutsource web uygulaması için kimlik yönetimi basit kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1ea31-104">By providing a single sign-in and sign-out with only a few lines of code, Azure Active Directory (Azure AD) makes it simple for you toooutsource web-app identity management.</span></span> <span data-ttu-id="1ea31-105">ASP.NET web uygulamaları ve kullanıcıların .NET (OWIN) ara yazılımı için açık Web arabirimi Microsoft uyarlamasını hello kullanarak oturum.</span><span class="sxs-lookup"><span data-stu-id="1ea31-105">You can sign users in and out of ASP.NET web apps by using hello Microsoft implementation of Open Web Interface for .NET (OWIN) middleware.</span></span> <span data-ttu-id="1ea31-106">OWIN ara yazılımı topluluk odaklı .NET Framework 4. 5 ' bulunur.</span><span class="sxs-lookup"><span data-stu-id="1ea31-106">Community-driven OWIN middleware is included in .NET Framework 4.5.</span></span> <span data-ttu-id="1ea31-107">Bu makalede gösterilmektedir nasıl toouse OWIN için:</span><span class="sxs-lookup"><span data-stu-id="1ea31-107">This article shows how toouse OWIN to:</span></span>

* <span data-ttu-id="1ea31-108">Kullanıcıların tooweb uygulamalarda hello kimlik sağlayıcısı Azure AD kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-108">Sign users in tooweb apps by using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="1ea31-109">Bazı kullanıcı bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1ea31-109">Display some user information.</span></span>
* <span data-ttu-id="1ea31-110">Merhaba uygulamaları dışında kullanıcılar oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-110">Sign users out of hello apps.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="1ea31-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1ea31-111">Before you get started</span></span>
* <span data-ttu-id="1ea31-112">Merhaba karşıdan [uygulama çatıyı](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) veya hello indirme [tamamlanan örnek](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1ea31-112">Download hello [app skeleton](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/skeleton.zip) or download hello [completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip).</span></span>
* <span data-ttu-id="1ea31-113">Ayrıca hangi tooregister hello uygulamasında Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ea31-113">You also need an Azure AD tenant in which tooregister hello app.</span></span> <span data-ttu-id="1ea31-114">Azure AD kiracısı, zaten yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="1ea31-114">If you don't already have an Azure AD tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="1ea31-115">Hazır olduğunuzda İleri dört bölüm izleyin hello yordamlarda hello.</span><span class="sxs-lookup"><span data-stu-id="1ea31-115">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-register-hello-new-app-with-azure-ad"></a><span data-ttu-id="1ea31-116">1. adım: Azure AD ile Merhaba yeni uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="1ea31-116">Step 1: Register hello new app with Azure AD</span></span>
<span data-ttu-id="1ea31-117">Merhaba uygulama tooauthenticate kullanıcıları tooset ilk kaydedin, kiracınızda hello aşağıdakileri yaparak:</span><span class="sxs-lookup"><span data-stu-id="1ea31-117">tooset up hello app tooauthenticate users, first register it in your tenant by doing hello following:</span></span>

1. <span data-ttu-id="1ea31-118">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ea31-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1ea31-119">Merhaba üst çubuğunda hesabınızın adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-119">On hello top bar, click your account name.</span></span> <span data-ttu-id="1ea31-120">Merhaba altında **Directory** listesi, tooregister hello uygulama istediğiniz select hello Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="1ea31-120">Under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="1ea31-121">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ea31-121">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="1ea31-122">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1ea31-122">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="1ea31-123">İzleyin hello ister yeni bir toocreate **Web uygulaması ve/veya Webapı**.</span><span class="sxs-lookup"><span data-stu-id="1ea31-123">Follow hello prompts toocreate a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="1ea31-124">**Ad** hello uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="1ea31-124">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="1ea31-125">**Oturum açma URL'si** hello hello uygulamasının temel URL'si.</span><span class="sxs-lookup"><span data-stu-id="1ea31-125">**Sign-On URL** is hello base URL of hello app.</span></span> <span data-ttu-id="1ea31-126">Merhaba çatıyı'nın varsayılan URL'dir https://localhost:44320 /.</span><span class="sxs-lookup"><span data-stu-id="1ea31-126">hello skeleton's default URL is https://localhost:44320/.</span></span>
6. <span data-ttu-id="1ea31-127">Merhaba kaydı tamamladıktan sonra Azure AD hello uygulama benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="1ea31-127">After you've completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="1ea31-128">Merhaba uygulama sayfası toouse hello sonraki bölümlerde Hello değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-128">Copy hello value from hello app page toouse in hello next sections.</span></span>
7. <span data-ttu-id="1ea31-129">Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1ea31-129">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="1ea31-130">Merhaba **uygulama kimliği URI'si** hello uygulama için benzersiz bir tanımlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="1ea31-130">hello **App ID URI** is a unique identifier for hello app.</span></span> <span data-ttu-id="1ea31-131">Merhaba adlandırma kuralı olan `https://<tenant-domain>/<app-name>` (örneğin, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span><span class="sxs-lookup"><span data-stu-id="1ea31-131">hello naming convention is `https://<tenant-domain>/<app-name>` (for example, `https://contoso.onmicrosoft.com/my-first-aad-app`).</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="1ea31-132">2. adım: hello uygulama toouse hello OWIN kimlik doğrulaması ardışık ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1ea31-132">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="1ea31-133">Bu adımda, hello OWIN ara yazılımı toouse hello Openıd Connect kimlik doğrulama protokolü yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-133">In this step, you configure hello OWIN middleware toouse hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="1ea31-134">OWIN tooissue oturum açma ve oturum kapatma isteklerini kullanın, kullanıcı oturumlarını yönetmek, kullanıcı bilgilerini almak ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="1ea31-134">You use OWIN tooissue sign-in and sign-out requests, manage user sessions, get user information, and so forth.</span></span>

1. <span data-ttu-id="1ea31-135">toobegin, hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1ea31-135">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Package Manager Console.</span></span>

     ```
     PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
     PM> Install-Package Microsoft.Owin.Security.Cookies
     PM> Install-Package Microsoft.Owin.Host.SystemWeb
     ```

2. <span data-ttu-id="1ea31-136">OWIN başlangıç sınıfı toohello projesinde adlı tooadd `Startup.cs`, hello projesine sağ tıklayın, seçin **Ekle**seçin **yeni öğe**, arayın ve sonra **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="1ea31-136">tooadd an OWIN Startup class toohello project called `Startup.cs`, right-click hello project, select **Add**, select **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="1ea31-137">Merhaba OWIN ara yazılımı çağırır hello **Configuration(...)**  hello uygulama başlatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ea31-137">hello OWIN middleware invokes hello **Configuration(...)** method when hello app starts.</span></span>
3. <span data-ttu-id="1ea31-138">Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="1ea31-138">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="1ea31-139">Zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="1ea31-139">We've already implemented part of this class for you in another file.</span></span> <span data-ttu-id="1ea31-140">Merhaba, **Configuration(...)**  yöntemi, çok çağırmaya**ConfgureAuth(...)**  tooset hello uygulaması için kimlik doğrulama ayarlama.</span><span class="sxs-lookup"><span data-stu-id="1ea31-140">In hello **Configuration(...)** method, make a call too**ConfgureAuth(...)** tooset up authentication for hello app.</span></span>  

     ```C#
     public partial class Startup
     {
         public void Configuration(IAppBuilder app)
         {
             ConfigureAuth(app);
         }
     }
     ```

4. <span data-ttu-id="1ea31-141">Merhaba App_Start\Startup.Auth.cs dosyasını açın ve ardından hello uygulamak **ConfigureAuth(...)**  yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1ea31-141">Open hello App_Start\Startup.Auth.cs file, and then implement hello **ConfigureAuth(...)** method.</span></span> <span data-ttu-id="1ea31-142">Merhaba, sağladığınız parametreler *OpenIDConnectAuthenticationOptions* hello uygulama toocommunicate Azure AD ile koordinatları olarak hizmet.</span><span class="sxs-lookup"><span data-stu-id="1ea31-142">hello parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for hello app toocommunicate with Azure AD.</span></span> <span data-ttu-id="1ea31-143">Merhaba Openıd Connect Ara hello arka planda tanımlama bilgileri kullandığından tooset tanımlama bilgisi kimlik doğrulamasını ayarlamak da gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ea31-143">You also need tooset up cookie authentication, because hello OpenID Connect middleware uses cookies in hello background.</span></span>

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

5. <span data-ttu-id="1ea31-144">Merhaba hello proje kök dizininde hello web.config dosyasını açın ve ardından hello hello yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="1ea31-144">Open hello web.config file in hello root of hello project, and then enter hello configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="1ea31-145">`ida:ClientId`: hello Azure portalında hello kopyalanan GUID "1. adım: kayıt hello Azure AD ile yeni bir uygulaması."</span><span class="sxs-lookup"><span data-stu-id="1ea31-145">`ida:ClientId`: hello GUID you copied from hello Azure portal in "Step 1: Register hello new app with Azure AD."</span></span>
  * <span data-ttu-id="1ea31-146">`ida:Tenant`: Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) hello adı.</span><span class="sxs-lookup"><span data-stu-id="1ea31-146">`ida:Tenant`: hello name of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="1ea31-147">`ida:PostLogoutRedirectUri`: bir kullanıcı oturum kapatma isteği başarıyla tamamlandıktan sonra burada yönlendirilmesi gereken Azure AD söyler hello göstergesi.</span><span class="sxs-lookup"><span data-stu-id="1ea31-147">`ida:PostLogoutRedirectUri`: hello indicator that tells Azure AD where a user should be redirected after a sign-out request is successfully completed.</span></span>

## <a name="step-3-use-owin-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a><span data-ttu-id="1ea31-148">3. adım: Kullanma OWIN tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="1ea31-148">Step 3: Use OWIN tooissue sign-in and sign-out requests tooAzure AD</span></span>
<span data-ttu-id="1ea31-149">Merhaba uygulama Azure AD ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1ea31-149">hello app is now properly configured toocommunicate with Azure AD by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="1ea31-150">OWIN tüm kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumlarını koruma hello ayrıntıları ele.</span><span class="sxs-lookup"><span data-stu-id="1ea31-150">OWIN has handled all of hello details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="1ea31-151">Tüm bu kalır, kullanıcılarınızın toogive olan bir şekilde toosign ve oturum kapatma.</span><span class="sxs-lookup"><span data-stu-id="1ea31-151">All that remains is toogive your users a way toosign in and sign out.</span></span>

1. <span data-ttu-id="1ea31-152">Kullanabileceğiniz belirli sayfalarını erişmeden önce denetleyicileri toorequire kullanıcılar toosign içinde etiketlerinde yetkilendirin.</span><span class="sxs-lookup"><span data-stu-id="1ea31-152">You can use authorize tags in your controllers toorequire users toosign in before they access certain pages.</span></span> <span data-ttu-id="1ea31-153">toodo, Controllers\HomeController.cs açın ve ardından hello ekleyin `[Authorize]` Denetleyicisi hakkında toohello etiketi.</span><span class="sxs-lookup"><span data-stu-id="1ea31-153">toodo so, open Controllers\HomeController.cs, and then add hello `[Authorize]` tag toohello About controller.</span></span>

     ```C#
     [Authorize]
     public ActionResult About()
     {
       ...
     ```

2. <span data-ttu-id="1ea31-154">OWIN toodirectly sorunu kimlik doğrulama isteklerini kodunuzu içinde de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ea31-154">You can also use OWIN toodirectly issue authentication requests from within your code.</span></span> <span data-ttu-id="1ea31-155">toodo, bu nedenle, Controllers\AccountController.cs açın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-155">toodo so, open Controllers\AccountController.cs.</span></span> <span data-ttu-id="1ea31-156">Ardından, Openıd Connect sınama ve oturum kapatma isteklerini hello SignIn() ve SignOut() Eylemler gönderin.</span><span class="sxs-lookup"><span data-stu-id="1ea31-156">Then, in hello SignIn() and SignOut() actions, issue OpenID Connect challenge and sign-out requests.</span></span>

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

3. <span data-ttu-id="1ea31-157">Görünümler/paylaşılan açmak\_LoginPartial.cshtml tooshow hello kullanıcı hello uygulama oturum açma ve oturum kapatma bağlantılar ve tooprint hello kullanıcının adını görünümünde çıkışı.</span><span class="sxs-lookup"><span data-stu-id="1ea31-157">Open Views\Shared\_LoginPartial.cshtml tooshow hello user hello app sign-in and sign-out links, and tooprint out hello user's name in a view.</span></span>

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

## <a name="step-4-display-user-information"></a><span data-ttu-id="1ea31-158">4. adım: kullanıcı bilgilerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="1ea31-158">Step 4: Display user information</span></span>
<span data-ttu-id="1ea31-159">Openıd Connect ile kullanıcıların kimliğini doğrular, Azure AD "talep" ya da hello kullanıcı hakkında onaylar içeren id_token toohello uygulama döndürür.</span><span class="sxs-lookup"><span data-stu-id="1ea31-159">When it authenticates users with OpenID Connect, Azure AD returns an id_token toohello app that contains "claims," or assertions about hello user.</span></span> <span data-ttu-id="1ea31-160">Merhaba aşağıdakileri yaparak bu talepler toopersonalize hello uygulamasını kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1ea31-160">You can use these claims toopersonalize hello app by doing hello following:</span></span>

1. <span data-ttu-id="1ea31-161">Merhaba Controllers\HomeController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-161">Open hello Controllers\HomeController.cs file.</span></span> <span data-ttu-id="1ea31-162">Denetleyicilerinizi hello aracılığıyla hello kullanıcının talepleri erişebilmeniz için `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1ea31-162">You can access hello user's claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

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

2. <span data-ttu-id="1ea31-163">Derleme ve hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-163">Build and run hello app.</span></span> <span data-ttu-id="1ea31-164">Kiracınızda onmicrosoft.com etki alanı ile yeni bir kullanıcı zaten oluşturmadıysanız hello zaman toodo şekilde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1ea31-164">If you haven't already created a new user in your tenant with an onmicrosoft.com domain, now is hello time toodo so.</span></span> <span data-ttu-id="1ea31-165">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="1ea31-165">Here's how:</span></span>

  <span data-ttu-id="1ea31-166">a.</span><span class="sxs-lookup"><span data-stu-id="1ea31-166">a.</span></span> <span data-ttu-id="1ea31-167">Oturum, kullanıcı oturum açabilir ve hello kullanıcının kimliğini hello üst çubuğunda nasıl yansıtılır not edin.</span><span class="sxs-lookup"><span data-stu-id="1ea31-167">Sign in with that user, and note how hello user's identity is reflected on hello top bar.</span></span>

  <span data-ttu-id="1ea31-168">b.</span><span class="sxs-lookup"><span data-stu-id="1ea31-168">b.</span></span> <span data-ttu-id="1ea31-169">Oturumu kapatın ve kiracınızda başka bir kullanıcı olarak yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1ea31-169">Sign out, and then sign back in as another user in your tenant.</span></span>

  <span data-ttu-id="1ea31-170">c.</span><span class="sxs-lookup"><span data-stu-id="1ea31-170">c.</span></span> <span data-ttu-id="1ea31-171">Özellikle hırslı hissediyorsanız kaydetmek ve bu uygulamayla (kendi ClientID) başka bir örneğini çalıştıran ve çoklu oturum açma eylem izleyin.</span><span class="sxs-lookup"><span data-stu-id="1ea31-171">If you're feeling particularly ambitious, register and run another instance of this app (with its own clientId), and watch single sign-in in action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ea31-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ea31-172">Next steps</span></span>
<span data-ttu-id="1ea31-173">Başvuru için bkz: [tamamlandı hello örnek](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (yapılandırma değerleriniz olmadan).</span><span class="sxs-lookup"><span data-stu-id="1ea31-173">For reference, see [hello completed sample](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="1ea31-174">Gelişmiş konular toomore üzerinde şimdi taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ea31-174">You can now move on toomore advanced topics.</span></span> <span data-ttu-id="1ea31-175">Örneğin, [Azure AD ile Web API güvenliğini](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1ea31-175">For example, try [Secure a Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
