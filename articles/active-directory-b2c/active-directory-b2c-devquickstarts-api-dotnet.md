---
title: aaaAzure AD B2C | Microsoft Docs
description: "Azure Active Directory B2C kullanarak .NET Web API'si toobuild güvenliği nasıl kimlik doğrulaması için OAuth 2.0 erişim belirteçleri kullanarak."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="05735-103">Azure Active Directory B2C: .NET web API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="05735-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="05735-104">Azure Active Directory (Azure AD) B2C ile OAuth 2.0 erişim belirteçleri kullanarak web API'si güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05735-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="05735-105">Bu belirteçler istemci uygulamaları tooauthenticate toohello API izin verin.</span><span class="sxs-lookup"><span data-stu-id="05735-105">These tokens allow your client apps tooauthenticate toohello API.</span></span> <span data-ttu-id="05735-106">Bu makalede nasıl toocreate .NET MVC "Yapılacaklar listesi" API İstemci kullanıcılarının uygulama tooCRUD görevleri sağlayan gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="05735-106">This article shows you how toocreate a .NET MVC "to-do list" API that allows users of your client application tooCRUD tasks.</span></span> <span data-ttu-id="05735-107">Merhaba web API'sini Azure AD B2C kullanarak güvenli ve kimliği doğrulanmış kullanıcılar toomanage kendi Yapılacaklar listesi yalnızca sağlar.</span><span class="sxs-lookup"><span data-stu-id="05735-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="05735-108">Azure AD B2C dizini oluşturma</span><span class="sxs-lookup"><span data-stu-id="05735-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="05735-109">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05735-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="05735-110">Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="05735-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="05735-111">Henüz yoksa devam etmeden önce bu kılavuzda [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="05735-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="05735-112">Merhaba istemci uygulaması ve web API hello aynı Azure AD B2C dizini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05735-112">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="05735-113">Web API’si oluşturma</span><span class="sxs-lookup"><span data-stu-id="05735-113">Create a web API</span></span>

<span data-ttu-id="05735-114">Ardından B2C dizininizde toocreate bir web API uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="05735-114">Next, you need toocreate a web API app in your B2C directory.</span></span> <span data-ttu-id="05735-115">Bu ihtiyaçlarını uygulamanızla toosecurely, iletişim bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="05735-115">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="05735-116">Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="05735-116">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="05735-117">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="05735-117">Be sure to:</span></span>

* <span data-ttu-id="05735-118">Dahil bir **web uygulaması** veya **web API'si** hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="05735-118">Include a **web app** or **web API** in hello application.</span></span>
* <span data-ttu-id="05735-119">Kullanım hello **yeniden yönlendirme URI'si** `https://localhost:44332/` hello web uygulaması için.</span><span class="sxs-lookup"><span data-stu-id="05735-119">Use hello **Redirect URI** `https://localhost:44332/` for hello web app.</span></span> <span data-ttu-id="05735-120">Bu kod örneği için başlangıç web uygulaması istemci hello varsayılan konumu budur.</span><span class="sxs-lookup"><span data-stu-id="05735-120">This is hello default location of hello web app client for this code sample.</span></span>
* <span data-ttu-id="05735-121">Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="05735-121">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="05735-122">Buna daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="05735-122">You'll need it later.</span></span>
* <span data-ttu-id="05735-123">**Uygulama Kimliği URI'si** alanına bir uygulama tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="05735-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="05735-124">İzinleri hello aracılığıyla eklemek **kapsamları yayımlanan** menüsü.</span><span class="sxs-lookup"><span data-stu-id="05735-124">Add permissions through hello **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="05735-125">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="05735-125">Create your policies</span></span>

<span data-ttu-id="05735-126">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="05735-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="05735-127">Azure AD B2C ile bir ilke toocommunicate toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="05735-127">You will need toocreate a policy toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="05735-128">Merhaba kullanılarak birleştirilen oturumu-up/oturum açma ilkesi hello açıklandığı şekilde öneririz [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="05735-128">We recommend using hello combined sign-up/sign-in policy, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="05735-129">İlkeyi oluştururken şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="05735-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="05735-130">İlkenizde, **Görünen ad** ve diğer kaydolma özniteliklerini seçin.</span><span class="sxs-lookup"><span data-stu-id="05735-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="05735-131">Her ilke için uygulamanın talep ettiği gibi **Görünen ad** ve **Nesne Kimliği** öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="05735-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="05735-132">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05735-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="05735-133">Kopya hello **adı** oluşturduktan sonra her ilkenin.</span><span class="sxs-lookup"><span data-stu-id="05735-133">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="05735-134">Hello ilkesi adı daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="05735-134">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="05735-135">Hazır toobuild olduğunuz hello ilkesi başarıyla oluşturduktan sonra uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="05735-135">After you have successfully created hello policy, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="05735-136">Merhaba kodu indirme</span><span class="sxs-lookup"><span data-stu-id="05735-136">Download hello code</span></span>

<span data-ttu-id="05735-137">Bu öğretici için kod Hello korunduğu [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="05735-137">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="05735-138">Çalıştırarak hello örnek kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="05735-138">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="05735-139">Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="05735-139">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="05735-140">Merhaba çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="05735-140">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="05735-141">`TaskWebApp`Kullanıcı hello bir MVC web uygulaması ile etkileşime giren olur.</span><span class="sxs-lookup"><span data-stu-id="05735-141">`TaskWebApp` is an MVC web application that hello user interacts with.</span></span> <span data-ttu-id="05735-142">`TaskService`her kullanıcının yapılacaklar listesini depolayan hello uygulamanızın arka uç web API'dır.</span><span class="sxs-lookup"><span data-stu-id="05735-142">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="05735-143">Bu makalede yalnızca hello ele alınacaktır `TaskService` uygulama.</span><span class="sxs-lookup"><span data-stu-id="05735-143">This article will only discuss hello `TaskService` application.</span></span> <span data-ttu-id="05735-144">toolearn nasıl toobuild `TaskWebApp` Azure AD B2C kullanarak bkz [bizim .NET web uygulaması Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="05735-144">toolearn how toobuild `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="05735-145">Hello Azure AD B2C yapılandırmasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="05735-145">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="05735-146">Bizim örnek yapılandırılmış toouse hello ilkeleri ve istemci bizim demo Kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="05735-146">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="05735-147">Toouse isterseniz kendi Kiracı aşağıdaki toodo hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="05735-147">If you would like toouse your own tenant, you will need toodo hello following:</span></span>

1. <span data-ttu-id="05735-148">Açık `web.config` hello içinde `TaskService` proje ve hello değerlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="05735-148">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>
    * <span data-ttu-id="05735-149">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="05735-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="05735-150">Web API uygulamanızın kimliği ile `ida:ClientId`</span><span class="sxs-lookup"><span data-stu-id="05735-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="05735-151">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="05735-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="05735-152">Açık `web.config` hello içinde `TaskWebApp` proje ve hello değerlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="05735-152">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>
    * <span data-ttu-id="05735-153">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="05735-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="05735-154">Web uygulamanızın kimliği ile `ida:ClientId`</span><span class="sxs-lookup"><span data-stu-id="05735-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="05735-155">Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`</span><span class="sxs-lookup"><span data-stu-id="05735-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="05735-156">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="05735-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="05735-157">"Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`</span><span class="sxs-lookup"><span data-stu-id="05735-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="05735-158">"Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`</span><span class="sxs-lookup"><span data-stu-id="05735-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-hello-api"></a><span data-ttu-id="05735-159">Merhaba API güvenli</span><span class="sxs-lookup"><span data-stu-id="05735-159">Secure hello API</span></span>

<span data-ttu-id="05735-160">API’nizi çağıran bir istemciniz olduğunda API’nizin (örn. `TaskService`) güvenliğini OAuth 2.0 taşıyıcı belirteçlerini kullanarak sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05735-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="05735-161">Bu her isteği tooyour API yalnızca bir taşıyıcı belirteci hello isteği varsa, geçerli olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="05735-161">This ensures that each request tooyour API will only be valid if hello request has a bearer token.</span></span> <span data-ttu-id="05735-162">API'niz .NET (OWIN) kitaplığı için Microsoft'un Açık Web Arabirimi'ni kullanarak taşıyıcı belirteçleri kabul edebilir ve doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="05735-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="05735-163">OWIN yükleme</span><span class="sxs-lookup"><span data-stu-id="05735-163">Install OWIN</span></span>

<span data-ttu-id="05735-164">Merhaba Visual Studio Paket Yöneticisi konsolu kullanılarak Hello OWIN OAuth kimlik doğrulaması işlem hattı yükleyerek çalışmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="05735-164">Begin by installing hello OWIN OAuth authentication pipeline by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="05735-165">Bu kabul etmek ve taşıyıcı belirteçleri doğrulamak hello OWIN ara yazılımı yükler.</span><span class="sxs-lookup"><span data-stu-id="05735-165">This will install hello OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="05735-166">OWIN başlangıç sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="05735-166">Add an OWIN startup class</span></span>

<span data-ttu-id="05735-167">Bir OWIN başlangıç sınıfı toohello API adlı eklemek `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="05735-167">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="05735-168">Merhaba projede, select sağ **Ekle** ve **yeni öğe**ve ardından OWIN'i aratın.</span><span class="sxs-lookup"><span data-stu-id="05735-168">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="05735-169">Merhaba OWIN ara yazılımı hello çağırılır `Configuration(…)` uygulamanız başladığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="05735-169">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="05735-170">Örneğimizde, biz hello sınıf bildirimi çok değiştirilen`public partial class Startup` ve uygulanan diğer hello sınıfında parçası hello `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="05735-170">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="05735-171">İç hello `Configuration` yöntemi, bir çağrı çok eklediğimiz`ConfigureAuth`, içinde tanımlanan `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="05735-171">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="05735-172">Merhaba değişiklikler sonra `Startup.cs` hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="05735-172">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="05735-173">OAuth 2.0 kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="05735-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="05735-174">Açık hello dosya `App_Start\Startup.Auth.cs`ve hello uygulamak `ConfigureAuth(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="05735-174">Open hello file `App_Start\Startup.Auth.cs`, and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="05735-175">Örneğin, hello şu şekilde görünebilir:</span><span class="sxs-lookup"><span data-stu-id="05735-175">For example, it could look like hello following:</span></span>

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a><span data-ttu-id="05735-176">Merhaba görev denetleyicisinin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="05735-176">Secure hello task controller</span></span>

<span data-ttu-id="05735-177">Merhaba uygulama yapılandırılmış toouse OAuth 2.0 kimlik doğrulaması getirildikten sonra ekleyerek web API güvenliğini sağlayabilirsiniz bir `[Authorize]` etiketi toohello görev denetleyicisi.</span><span class="sxs-lookup"><span data-stu-id="05735-177">After hello app is configured toouse OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag toohello task controller.</span></span> <span data-ttu-id="05735-178">Bu hello tüm denetleyicinin hello sınıf düzeyinde güvenliğini sağlamanız gerekir böylece tüm yapılacaklar listesi işlemelerinin, gerçekleştiği hello denetleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="05735-178">This is hello controller where all to-do list manipulation takes place, so you should secure hello entire controller at hello class level.</span></span> <span data-ttu-id="05735-179">Merhaba de ekleyebilirsiniz `[Authorize]` tooindividual Eylemler daha ayrıntılı denetim için etiket.</span><span class="sxs-lookup"><span data-stu-id="05735-179">You can also add hello `[Authorize]` tag tooindividual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a><span data-ttu-id="05735-180">Kullanıcı bilgilerini hello belirteci alma</span><span class="sxs-lookup"><span data-stu-id="05735-180">Get user information from hello token</span></span>

<span data-ttu-id="05735-181">`TasksController`görevleri her görev sahibi "Merhaba görev" bir ilişkili kullanıcının sahip olduğu bir veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="05735-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" hello task.</span></span> <span data-ttu-id="05735-182">Merhaba sahibi hello kullanıcı tarafından tanımlanan **nesne kimliği**.</span><span class="sxs-lookup"><span data-stu-id="05735-182">hello owner is identified by hello user's **object ID**.</span></span> <span data-ttu-id="05735-183">(Bir uygulama olarak tooadd hello nesne kimliği gerekli bu yüzden talep ilkelerinizi tümünde.)</span><span class="sxs-lookup"><span data-stu-id="05735-183">(This is why you needed tooadd hello object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a><span data-ttu-id="05735-184">Merhaba belirteci Hello izinleri doğrula</span><span class="sxs-lookup"><span data-stu-id="05735-184">Validate hello permissions in hello token</span></span>

<span data-ttu-id="05735-185">Web API'leri için ortak bir gereksinim toovalidate hello "kapsamlar" Merhaba belirtecinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="05735-185">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="05735-186">Bu, o hello kullanıcı toohello izinleri gerekli tooaccess hello Yapılacaklar listesi hizmet verdiği sağlar.</span><span class="sxs-lookup"><span data-stu-id="05735-186">This ensures that hello user has consented toohello permissions required tooaccess hello to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="05735-187">Merhaba örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="05735-187">Run hello sample app</span></span>

<span data-ttu-id="05735-188">Son olarak hem `TaskWebApp` hem de `TaskService` öğesini oluşturup çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="05735-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="05735-189">Merhaba kullanıcının Yapılacaklar listesinde bazı görevler oluşturun ve hatta durdurmak ve hello istemci yeniden başlattıktan sonra nasıl bunlar hello API kalıcı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="05735-189">Create some tasks on hello user's to-do list and notice how they are persisted in hello API even after you stop and restart hello client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="05735-190">İlkelerinizi düzenleme</span><span class="sxs-lookup"><span data-stu-id="05735-190">Edit your policies</span></span>

<span data-ttu-id="05735-191">Azure AD B2C kullanarak API güvenliğini sağladıktan sonra oturum-açma/kaydolma ilke ve görünüm hello etkileri (veya bunların olmaması) hello API ile deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05735-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view hello effects (or lack thereof) on hello API.</span></span> <span data-ttu-id="05735-192">Merhaba uygulama talepleri hello ilkelerinde işlemek ve hello web API'SİNDE kullanılabilen hello kullanıcı bilgilerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="05735-192">You can manipulate hello application claims in hello policies and change hello user information that is available in hello web API.</span></span> <span data-ttu-id="05735-193">Eklediğiniz herhangi bir talep kullanılabilir tooyour .NET MVC web API'si hello olacaktır `ClaimsPrincipal` , bu makalenin önceki bölümlerinde açıklandığı gibi nesne.</span><span class="sxs-lookup"><span data-stu-id="05735-193">Any claims that you add will be available tooyour .NET MVC web API in hello `ClaimsPrincipal` object, as described earlier in this article.</span></span>
