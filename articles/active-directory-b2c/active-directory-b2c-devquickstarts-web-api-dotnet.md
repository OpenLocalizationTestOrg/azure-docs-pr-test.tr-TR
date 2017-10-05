---
title: Azure Active Directory B2C | Microsoft Docs
description: ".NET Web uygulaması oluşturma ve bir web çağırmak nasıl Azure Active Directory B2C ve OAuth 2.0 erişim belirteçleri kullanarak API."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: d3888556-2647-4a42-b068-027f9374aa61
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 48452eb68f826d1c7aa61d5e5531f941ac1422b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="92043-103">Azure AD B2C: bir .NET web uygulamasından .NET web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="92043-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="92043-104">Azure AD B2C kullanarak web uygulamaları ve web API'leri için güçlü kimlik yönetimi özellikleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92043-104">By using Azure AD B2C, you can add powerful identity management features to your web apps and web APIs.</span></span> <span data-ttu-id="92043-105">Bu makalede erişim belirteçleri ve bir .NET yapma çağrıları .NET "Yapılacaklar listesi" web uygulamasından web API'si istemek nasıl anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="92043-105">This article discusses how to request access tokens and make calls from a .NET "to-do list" web app to a .NET web api.</span></span>

<span data-ttu-id="92043-106">Bu makalede, oturum açma, kaydolma nasıl uygulanacağını ve profil Yönetimi Azure AD B2C ile kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="92043-106">This article does not cover how to implement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="92043-107">Kullanıcının kimliği zaten doğrulanmış sonra web API'leri çağırmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="92043-107">It focuses on calling web APIs after the user is already authenticated.</span></span> <span data-ttu-id="92043-108">Henüz yapmadıysanız, aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="92043-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="92043-109">Kullanmaya başlama bir [.NET web uygulaması](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="92043-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="92043-110">Kullanmaya başlama bir [.NET web API'si](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="92043-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="92043-111">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="92043-111">Prerequisite</span></span>

<span data-ttu-id="92043-112">Bir web çağıran bir web uygulaması oluşturmak için API, gerekir:</span><span class="sxs-lookup"><span data-stu-id="92043-112">To build a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="92043-113">[Bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="92043-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="92043-114">[Bir web kayıt API](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="92043-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="92043-115">[Bir web uygulaması kaydetmek](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="92043-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="92043-116">[İlkeleri Ayarla](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="92043-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="92043-117">[Web uygulaması web kullanma izni vermek API](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="92043-117">[Grant the web app permissions to use the web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92043-118">İstemci uygulaması ve web API’si aynı Azure AD B2C dizinini kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="92043-118">The client application and web API must use the same Azure AD B2C directory.</span></span>
>

## <a name="download-the-code"></a><span data-ttu-id="92043-119">Kodu indirme</span><span class="sxs-lookup"><span data-stu-id="92043-119">Download the code</span></span>

<span data-ttu-id="92043-120">Bu öğretici için kod [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)'da korunur.</span><span class="sxs-lookup"><span data-stu-id="92043-120">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="92043-121">Örneği kopyalamak için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="92043-121">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="92043-122">Örnek kodu indirdikten sonra başlamak için Visual Studio .sln dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="92043-122">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="92043-123">Çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="92043-123">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="92043-124">`TaskWebApp`kullanıcı ile etkileşime giren bir MVC bir web uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="92043-124">`TaskWebApp` is a MVC web application that the user interacts with.</span></span> <span data-ttu-id="92043-125">`TaskService`, uygulamanın, her kullanıcının yapılacaklar listesini depolayan arka uç web API'sidir.</span><span class="sxs-lookup"><span data-stu-id="92043-125">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="92043-126">Bu makalede yapı kapsamaz `TaskWebApp` web uygulaması veya `TaskService` web API'si.</span><span class="sxs-lookup"><span data-stu-id="92043-126">This article does not cover building the `TaskWebApp` web app or the `TaskService` web api.</span></span> <span data-ttu-id="92043-127">Azure AD B2C kullanarak .NET web uygulaması oluşturmayı öğrenmek için bkz: bizim [.NET web uygulaması Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="92043-127">To learn how to build the .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="92043-128">.NET web API'si Azure AD B2C kullanarak güvenliği oluşturma konusunda bilgi almak için bkz: bizim [.NET web API'si Öğreticisi](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="92043-128">To learn how to build the .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-the-azure-ad-b2c-configuration"></a><span data-ttu-id="92043-129">Azure AD B2C yapılandırmasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="92043-129">Update the Azure AD B2C configuration</span></span>

<span data-ttu-id="92043-130">Örneğimiz, tanıtım kiracımızın ilkelerini ve istemci kimliğini kullanacak şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="92043-130">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="92043-131">Kendi Kiracı kullanmak istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="92043-131">If you would like to use your own tenant:</span></span>

1. <span data-ttu-id="92043-132">`TaskService` projesinde `web.config` öğesini açın ve şu değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="92043-132">Open `web.config` in the `TaskService` project and replace the values for</span></span>

    * <span data-ttu-id="92043-133">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="92043-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="92043-134">`ida:ClientId`web API uygulama Kimliğinizle</span><span class="sxs-lookup"><span data-stu-id="92043-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="92043-135">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="92043-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="92043-136">`TaskWebApp` projesinde `web.config` öğesini açın ve şu değerleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="92043-136">Open `web.config` in the `TaskWebApp` project and replace the values for</span></span>

    * <span data-ttu-id="92043-137">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="92043-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="92043-138">Web uygulamanızın kimliği ile `ida:ClientId`</span><span class="sxs-lookup"><span data-stu-id="92043-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="92043-139">Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`</span><span class="sxs-lookup"><span data-stu-id="92043-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="92043-140">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="92043-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="92043-141">"Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`</span><span class="sxs-lookup"><span data-stu-id="92043-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="92043-142">"Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`</span><span class="sxs-lookup"><span data-stu-id="92043-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="92043-143">İsteme ve bir erişim belirteci kaydetme</span><span class="sxs-lookup"><span data-stu-id="92043-143">Requesting and saving an access token</span></span>

### <a name="specify-the-permissions"></a><span data-ttu-id="92043-144">İzinleri belirtin</span><span class="sxs-lookup"><span data-stu-id="92043-144">Specify the permissions</span></span>

<span data-ttu-id="92043-145">Web API çağrısı yapmak için (oturumu-up/oturum açma ilkeniz kullanarak) kullanıcı kimlik doğrulaması gerekir ve [bir erişim belirteci almak](active-directory-b2c-access-tokens.md) Azure AD B2C'ndan.</span><span class="sxs-lookup"><span data-stu-id="92043-145">In order to make the call to the web API, you need to authenticate the user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="92043-146">Bir erişim belirteci almak için erişim belirteci vermek istediğiniz izinleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="92043-146">In order to receive an access token, you first must specify the permissions you would like the access token to grant.</span></span> <span data-ttu-id="92043-147">İzinleri belirtilen `scope` isteği yaptığınızda parametresi `/authorize` uç noktası.</span><span class="sxs-lookup"><span data-stu-id="92043-147">The permissions are specified in the `scope` parameter when you make the request to the `/authorize` endpoint.</span></span> <span data-ttu-id="92043-148">Örneğin, uygulama kimliği URI'si kaynak uygulamanın "Okuma" izni olan bir erişim belirteci alması için `https://contoso.onmicrosoft.com/tasks`, kapsam olacaktır `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="92043-148">For example, to acquire an access token with the “read” permission to the resource application that has the App ID URI of `https://contoso.onmicrosoft.com/tasks`, the scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="92043-149">Bizim örnek kapsamını belirtmek için dosyayı açmak `App_Start\Startup.Auth.cs` ve tanımlayın `Scope` OpenIdConnectAuthenticationOptions değişkeni.</span><span class="sxs-lookup"><span data-stu-id="92043-149">To specify the scope in our sample, open the file `App_Start\Startup.Auth.cs` and define the `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-the-authorization-code-for-an-access-token"></a><span data-ttu-id="92043-150">Bir erişim belirteci yetkilendirme kodu değişimi</span><span class="sxs-lookup"><span data-stu-id="92043-150">Exchange the authorization code for an access token</span></span>

<span data-ttu-id="92043-151">Bir kullanıcı kaydı veya oturum açma deneyimi tamamlandıktan sonra uygulamanızı Azure AD B2C ' bir yetkilendirme kodu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="92043-151">After an user completes the sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="92043-152">OWIN Openıd Connect Ara kodunu depolar, ancak bir erişim belirteci için exchange değil.</span><span class="sxs-lookup"><span data-stu-id="92043-152">The OWIN OpenID Connect middleware will store the code, but will not exchange it for an access token.</span></span> <span data-ttu-id="92043-153">Kullanabileceğiniz [MSAL Kitaplığı](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) değişikliği yapmak için.</span><span class="sxs-lookup"><span data-stu-id="92043-153">You can use the [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) to make the exchange.</span></span> <span data-ttu-id="92043-154">Bir yetkilendirme kodu alındığında Örneğimizde, biz bildirimi geri araması Openıd Connect Ara yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="92043-154">In our sample, we configured a notification callback into the OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="92043-155">Geri arama, bir belirteç kodunu exchange ve belirteç önbelleğe kaydetmek için MSAL kullanın.</span><span class="sxs-lookup"><span data-stu-id="92043-155">In the callback, we use MSAL to exchange the code for a token and save the token into the cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract the code from the response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange the code for a token. Make sure to specify the necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-the-web-api"></a><span data-ttu-id="92043-156">Web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="92043-156">Calling the web API</span></span>

<span data-ttu-id="92043-157">Bu bölümde sırasında alınan simgesinin nasıl kullanılacağına ilişkin anlatılmaktadır oturumu-up/oturum açma web API'si erişmek için Azure AD B2C ile.</span><span class="sxs-lookup"><span data-stu-id="92043-157">This section discusses how to use the token received during sign-up/sign-in with Azure AD B2C in order to access the web API.</span></span>

### <a name="retrieve-the-saved-token-in-the-controllers"></a><span data-ttu-id="92043-158">Denetleyicileri kaydedilmiş belirteçte alma</span><span class="sxs-lookup"><span data-stu-id="92043-158">Retrieve the saved token in the controllers</span></span>

<span data-ttu-id="92043-159">`TasksController` Web API ile iletişim kurmasını ve okuma, oluşturun ve görevleri silme API'sine HTTP istekleri göndermek için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="92043-159">The `TasksController` is responsible for communicating with the web API and for sending HTTP requests to the API to read, create, and delete tasks.</span></span> <span data-ttu-id="92043-160">API Azure AD B2C tarafından korumalı olduğundan, ilk ve Yukarıdaki adımda kaydettiğiniz belirtecini almak gerekir.</span><span class="sxs-lookup"><span data-stu-id="92043-160">Because the API is secured by Azure AD B2C, you need to first retrieve the token you saved in the above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL to retrieve the token from the cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve the token using the provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-the-web-api"></a><span data-ttu-id="92043-161">Web API görevlerini okuma</span><span class="sxs-lookup"><span data-stu-id="92043-161">Read tasks from the web API</span></span>

<span data-ttu-id="92043-162">Bir belirteç sahip olduğunuzda, HTTP iliştirebilirsiniz `GET` içindeki istek `Authorization` güvenli bir şekilde çağırmak için üstbilgi `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="92043-162">When you have a token, you can attach it to the HTTP `GET` request in the `Authorization` header to securely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve the token with the specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token to the Authorization header and make the request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-the-web-api"></a><span data-ttu-id="92043-163">Oluşturma ve web API görevleri silme</span><span class="sxs-lookup"><span data-stu-id="92043-163">Create and delete tasks on the web API</span></span>

<span data-ttu-id="92043-164">Gönderdiğiniz aynı düzeni uygular `POST` ve `DELETE` önbellekten erişim belirteci almak için MSAL kullanarak API, web istekleri.</span><span class="sxs-lookup"><span data-stu-id="92043-164">Follow the same pattern when you send `POST` and `DELETE` requests to the web API, using MSAL to retrieve the access token from the cache.</span></span>

## <a name="run-the-sample-app"></a><span data-ttu-id="92043-165">Örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="92043-165">Run the sample app</span></span>

<span data-ttu-id="92043-166">Son olarak, yapı ve her iki uygulamaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="92043-166">Finally, build and run both the apps.</span></span> <span data-ttu-id="92043-167">Kaydolma ve oturum açın ve oturum açmış kullanıcı için Görevler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="92043-167">Sign up and sign in, and create tasks for the signed-in user.</span></span> <span data-ttu-id="92043-168">Oturumu kapatın ve farklı bir kullanıcı olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="92043-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="92043-169">Bu kullanıcı için Görevler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="92043-169">Create tasks for that user.</span></span> <span data-ttu-id="92043-170">API, aldığı belirtecinden kullanıcının kimliğini ayıkladığı için görevlerin kullanıcı başına API üzerinde nasıl olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="92043-170">Notice how the tasks are stored per-user on the API, because the API extracts the user's identity from the token it receives.</span></span> <span data-ttu-id="92043-171">Ayrıca kapsamlarla yürütmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="92043-171">Also try playing with the scopes.</span></span> <span data-ttu-id="92043-172">"Yazma" ve bir görev eklemeyi deneyin iznini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="92043-172">Remove the permission to "write" and then try adding a task.</span></span> <span data-ttu-id="92043-173">Yeni kapsam değiştirme her zaman aşımına uğrar imzalamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="92043-173">Just make sure to sign out each time you change the scope.</span></span>

