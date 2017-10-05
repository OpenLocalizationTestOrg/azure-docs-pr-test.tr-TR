---
title: Azure AD B2C | Microsoft Belgeleri
description: "Kimlik doğrulaması için OAuth 2.0 erişim belirteçleri ile güvenliği sağlanan Azure Active Directory B2C kullanarak .NET Web API'si oluşturma."
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
ms.openlocfilehash: 48749bfa2ab54a0e766a4aad4f39073cc4e90818
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a><span data-ttu-id="6fcbc-103">Azure Active Directory B2C: .NET web API'si oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fcbc-103">Azure Active Directory B2C: Build a .NET web API</span></span>

<span data-ttu-id="6fcbc-104">Azure Active Directory (Azure AD) B2C ile OAuth 2.0 erişim belirteçleri kullanarak web API'si güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="6fcbc-105">Bu belirteçler, istemci uygulamalarınızın API'ye ilişkin kimlik doğrulaması yapmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-105">These tokens allow your client apps to authenticate to the API.</span></span> <span data-ttu-id="6fcbc-106">Bu makalede istemci uygulamanızın kullanıcılarının CRUD görevlerini gerçekleştirmesine imkan tanıyan bir .NET MVC "yapılacaklar listesi" API’sini oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-106">This article shows you how to create a .NET MVC "to-do list" API that allows users of your client application to CRUD tasks.</span></span> <span data-ttu-id="6fcbc-107">Web API’sinin güvenliği Azure AD B2C kullanılarak sağlanır ve yapılacaklar listesini yalnızca kimliği doğrulanmış kullanıcıların yönetmesine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="6fcbc-108">Azure AD B2C dizini oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fcbc-108">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="6fcbc-109">Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="6fcbc-110">Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="6fcbc-111">Henüz yoksa devam etmeden önce bu kılavuzda [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6fcbc-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

> [!NOTE]
> <span data-ttu-id="6fcbc-112">İstemci uygulaması ve web API’si aynı Azure AD B2C dizinini kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-112">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="create-a-web-api"></a><span data-ttu-id="6fcbc-113">Web API’si oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fcbc-113">Create a web API</span></span>

<span data-ttu-id="6fcbc-114">Ardından B2C dizininizde bir web API uygulaması oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-114">Next, you need to create a web API app in your B2C directory.</span></span> <span data-ttu-id="6fcbc-115">Bu, uygulamanız ile güvenli şekilde iletişim kurması için gereken bilgileri Azure AD'ye verir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-115">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="6fcbc-116">Bir uygulama oluşturmak için [bu talimatları](active-directory-b2c-app-registration.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-116">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="6fcbc-117">Şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-117">Be sure to:</span></span>

* <span data-ttu-id="6fcbc-118">Uygulamaya bir **web uygulaması** veya **web API'si** ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-118">Include a **web app** or **web API** in the application.</span></span>
* <span data-ttu-id="6fcbc-119">Web uygulamasının **Yeniden Yönlendirme URI’sini** `https://localhost:44332/` kullanın.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-119">Use the **Redirect URI** `https://localhost:44332/` for the web app.</span></span> <span data-ttu-id="6fcbc-120">Bu konum bu kod örneği için web uygulaması sunucusunun varsayılan konumudur.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-120">This is the default location of the web app client for this code sample.</span></span>
* <span data-ttu-id="6fcbc-121">Uygulamanıza atanan **Uygulama Kimliği**'ni kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-121">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="6fcbc-122">Buna daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-122">You'll need it later.</span></span>
* <span data-ttu-id="6fcbc-123">**Uygulama Kimliği URI'si** alanına bir uygulama tanımlayıcısı girin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-123">Enter an app identifier into **App ID URI**.</span></span>
* <span data-ttu-id="6fcbc-124">**Yayımlanmış kapsamlar** menüsü üzerinden izinler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-124">Add permissions through the **Published scopes** menu.</span></span>

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="6fcbc-125">İlkelerinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fcbc-125">Create your policies</span></span>

<span data-ttu-id="6fcbc-126">Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-126">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6fcbc-127">Azure AD B2C ile iletişim kurmak için bir ilke oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-127">You will need to create a policy to communicate with Azure AD B2C.</span></span> <span data-ttu-id="6fcbc-128">[İlke başvurusu makalesinde](active-directory-b2c-reference-policies.md) açıklanan birleşik kaydolma/oturum açma ilkesinin kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-128">We recommend using the combined sign-up/sign-in policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6fcbc-129">İlkeyi oluştururken şunları yaptığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-129">When you create your policy, be sure to:</span></span>

* <span data-ttu-id="6fcbc-130">İlkenizde, **Görünen ad** ve diğer kaydolma özniteliklerini seçin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-130">Choose **Display name** and other sign-up attributes in your policy.</span></span>
* <span data-ttu-id="6fcbc-131">Her ilke için uygulamanın talep ettiği gibi **Görünen ad** ve **Nesne Kimliği** öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-131">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="6fcbc-132">Diğer talepleri de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-132">You can choose other claims as well.</span></span>
* <span data-ttu-id="6fcbc-133">Oluşturduktan sonra her ilkenin **Adını** kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-133">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="6fcbc-134">Bu ilke adına daha sonra ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-134">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="6fcbc-135">İlkeyi başarıyla oluşturduktan sonra uygulamanızı oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-135">After you have successfully created the policy, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="6fcbc-136">Kodu indirme</span><span class="sxs-lookup"><span data-stu-id="6fcbc-136">Download the code</span></span>

<span data-ttu-id="6fcbc-137">Bu öğretici için kod [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)'da korunur.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-137">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="6fcbc-138">Örneği kopyalamak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-138">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="6fcbc-139">Örnek kodu indirdikten sonra başlamak için Visual Studio .sln dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-139">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="6fcbc-140">Çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-140">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="6fcbc-141">`TaskWebApp`, kullanıcının etkileşime geçtiği bir MVC web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-141">`TaskWebApp` is an MVC web application that the user interacts with.</span></span> <span data-ttu-id="6fcbc-142">`TaskService`, uygulamanın, her kullanıcının yapılacaklar listesini depolayan arka uç web API'sidir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-142">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="6fcbc-143">Bu makalede yalnızca `TaskService` uygulaması ele alınacaktır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-143">This article will only discuss the `TaskService` application.</span></span> <span data-ttu-id="6fcbc-144">Azure AD B2C kullanarak bir `TaskWebApp` derlemeyi öğrenmek için bkz. [.NET web uygulaması öğreticisi](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="6fcbc-144">To learn how to build `TaskWebApp` using Azure AD B2C, see [our .NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="6fcbc-145">Azure AD B2C yapılandırmasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="6fcbc-145">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="6fcbc-146">Örneğimiz, tanıtım kiracımızın ilkelerini ve istemci kimliğini kullanacak şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-146">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="6fcbc-147">Kendi kiracınızı kullanmak istiyorsanız aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-147">If you would like to use your own tenant, you will need to do the following:</span></span>

1. <span data-ttu-id="6fcbc-148">`TaskService` projesinde `web.config` öğesini açın ve şu değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-148">Open `web.config` in the `TaskService` project and replace the values for</span></span>
    * <span data-ttu-id="6fcbc-149">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-149">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="6fcbc-150">Web API uygulamanızın kimliği ile `ida:ClientId`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-150">`ida:ClientId` with your web API application ID</span></span>
    * <span data-ttu-id="6fcbc-151">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-151">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="6fcbc-152">`TaskWebApp` projesinde `web.config` öğesini açın ve şu değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-152">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>
    * <span data-ttu-id="6fcbc-153">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-153">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="6fcbc-154">Web uygulamanızın kimliği ile `ida:ClientId`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-154">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="6fcbc-155">Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-155">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="6fcbc-156">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-156">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="6fcbc-157">"Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-157">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="6fcbc-158">"Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`</span><span class="sxs-lookup"><span data-stu-id="6fcbc-158">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>


## <a name="secure-the-api"></a><span data-ttu-id="6fcbc-159">API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="6fcbc-159">Secure the API</span></span>

<span data-ttu-id="6fcbc-160">API’nizi çağıran bir istemciniz olduğunda API’nizin (örn. `TaskService`) güvenliğini OAuth 2.0 taşıyıcı belirteçlerini kullanarak sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-160">When you have a client that calls your API, you can secure your API (e.g `TaskService`) by using OAuth 2.0 bearer tokens.</span></span> <span data-ttu-id="6fcbc-161">Bunun yapılması, API’nize gönderilen her isteğin yalnızca istekte bir taşıyıcı belirteç varsa geçerli olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-161">This ensures that each request to your API will only be valid if the request has a bearer token.</span></span> <span data-ttu-id="6fcbc-162">API'niz .NET (OWIN) kitaplığı için Microsoft'un Açık Web Arabirimi'ni kullanarak taşıyıcı belirteçleri kabul edebilir ve doğrulayabilir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-162">Your API can accept and validate bearer tokens by using Microsoft's Open Web Interface for .NET (OWIN) library.</span></span>

### <a name="install-owin"></a><span data-ttu-id="6fcbc-163">OWIN yükleme</span><span class="sxs-lookup"><span data-stu-id="6fcbc-163">Install OWIN</span></span>

<span data-ttu-id="6fcbc-164">İlk olarak Visual Studio Paket Yöneticisi Konsolu’nu kullanarak OWIN OAuth kimlik doğrulama işlem hattını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-164">Begin by installing the OWIN OAuth authentication pipeline by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

<span data-ttu-id="6fcbc-165">Bunun yapılması, taşıyıcı belirteçleri kabul edip doğrulayacak OWIN ara yazılımını yükler.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-165">This will install the OWIN middleware that will accept and validate bearer tokens.</span></span>

### <a name="add-an-owin-startup-class"></a><span data-ttu-id="6fcbc-166">OWIN başlangıç sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="6fcbc-166">Add an OWIN startup class</span></span>

<span data-ttu-id="6fcbc-167">`Startup.cs` adlı API’ye bir OWIN başlangıç sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-167">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="6fcbc-168">Projeye sağ tıklayın, **Ekle**'yi ve **Yeni Öğe**'yi seçin, ardından OWIN'i aratın.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-168">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="6fcbc-169">OWIN ara yazılımı, uygulamanız başlatıldığında `Configuration(…)` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-169">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="6fcbc-170">Örneğimizde, sınıf bildirimi `public partial class Startup` olarak değiştirilmiş ve sınıfın `App_Start\Startup.Auth.cs` içindeki diğer kısmı kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-170">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="6fcbc-171">`Configuration` yöntemine, `Startup.Auth.cs` içinde tanımlanan bir `ConfigureAuth` çağrısı eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-171">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="6fcbc-172">Değişikliklerden sonra `Startup.cs` aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-172">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a><span data-ttu-id="6fcbc-173">OAuth 2.0 kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6fcbc-173">Configure OAuth 2.0 authentication</span></span>

<span data-ttu-id="6fcbc-174">`App_Start\Startup.Auth.cs` dosyasını açın ve `ConfigureAuth(...)` yöntemini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-174">Open the file `App_Start\Startup.Auth.cs`, and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="6fcbc-175">Örneğin, aşağıdaki gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="6fcbc-175">For example, it could look like the following:</span></span>

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
         * Configure the authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where the audience of the token is equal to the client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches the Azure AD B2C metadata & signing keys from the OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-the-task-controller"></a><span data-ttu-id="6fcbc-176">Görev denetleyicisinin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="6fcbc-176">Secure the task controller</span></span>

<span data-ttu-id="6fcbc-177">Uygulama OAuth 2.0 kimlik doğrulaması kullanacak şekilde yapılandırıldıktan sonra görev denetleyicisine `[Authorize]` etiketi ekleyerek web API'nizin güvenliğini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-177">After the app is configured to use OAuth 2.0 authentication, you can secure your web API by adding an `[Authorize]` tag to the task controller.</span></span> <span data-ttu-id="6fcbc-178">Bu, tüm yapılacaklar listesi işlemelerinin yapıldığı denetleyicidir, yani tüm denetleyicinin sınıf düzeyinde güvenliğini sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-178">This is the controller where all to-do list manipulation takes place, so you should secure the entire controller at the class level.</span></span> <span data-ttu-id="6fcbc-179">Ayrıca daha ayrıntılı denetim için bireysel işlemlere `[Authorize]` etiketi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-179">You can also add the `[Authorize]` tag to individual actions for more fine-grained control.</span></span>

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-the-token"></a><span data-ttu-id="6fcbc-180">Belirteçten kullanıcı bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="6fcbc-180">Get user information from the token</span></span>

<span data-ttu-id="6fcbc-181">`TasksController`, görevleri, her görevin göreve "sahip olan" kullanıcı ile ilişkilendirildiği bir veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-181">`TasksController` stores tasks in a database where each task has an associated user who "owns" the task.</span></span> <span data-ttu-id="6fcbc-182">Sahip, kullanıcının **nesne kimliği** ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-182">The owner is identified by the user's **object ID**.</span></span> <span data-ttu-id="6fcbc-183">(Tüm ilkelerinize uygulama talebi olarak nesne kimliği eklemeniz gerekmesinin nedeni budur.)</span><span class="sxs-lookup"><span data-stu-id="6fcbc-183">(This is why you needed to add the object ID as an application claim in all of your policies.)</span></span>

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-the-permissions-in-the-token"></a><span data-ttu-id="6fcbc-184">Belirteçteki izinleri doğrulama</span><span class="sxs-lookup"><span data-stu-id="6fcbc-184">Validate the permissions in the token</span></span>

<span data-ttu-id="6fcbc-185">Web API’lerine yönelik genel bir gereksinim, belirteçteki mevcut "kapsamların" doğrulanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-185">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="6fcbc-186">Bunun yapılması, kullanıcının yapılacaklar listesi hizmetine erişmesi için gereken izinleri onaylamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-186">This ensures that the user has consented to the permissions required to access the to-do list service.</span></span>

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "The Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="6fcbc-187">Örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6fcbc-187">Run the sample app</span></span>

<span data-ttu-id="6fcbc-188">Son olarak hem `TaskWebApp` hem de `TaskService` öğesini oluşturup çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-188">Finally, build and run both `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="6fcbc-189">Kullanıcının yapılacaklar listesinde bazı görevler oluşturun ve istemciyi durdurmanız ve yeniden başlatmanız sonrasında bile API içinde nasıl kalıcı olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-189">Create some tasks on the user's to-do list and notice how they are persisted in the API even after you stop and restart the client.</span></span>

## <a name="edit-your-policies"></a><span data-ttu-id="6fcbc-190">İlkelerinizi düzenleme</span><span class="sxs-lookup"><span data-stu-id="6fcbc-190">Edit your policies</span></span>

<span data-ttu-id="6fcbc-191">Azure AD B2C kullanarak API güvenliğini sağladıktan sonra Kaydolma/Oturum Açma ilkelerinizi deneyebilir ve API üzerindeki etkileri (veya eksiklikleri) görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-191">After you have secured an API by using Azure AD B2C, you can experiment with your Sign-in/Sign-up policy and view the effects (or lack thereof) on the API.</span></span> <span data-ttu-id="6fcbc-192">Ayrıca ilkelerdeki uygulama talepleri denetleyebilir ve web API'sinde kullanılabilen kullanıcı bilgilerini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-192">You can manipulate the application claims in the policies and change the user information that is available in the web API.</span></span> <span data-ttu-id="6fcbc-193">Eklediğiniz tüm talepler bu makalede daha önce açıklandığı gibi `ClaimsPrincipal` nesnesindeki .NET MVC web API'nizde kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6fcbc-193">Any claims that you add will be available to your .NET MVC web API in the `ClaimsPrincipal` object, as described earlier in this article.</span></span>
