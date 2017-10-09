---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "Nasıl toobuild .NET Web uygulaması ve web çağırma Azure Active Directory B2C ve OAuth 2.0 erişim belirteçleri kullanarak API."
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
ms.openlocfilehash: 9b248e3bf18968e12aae73c07083fa8278befb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a><span data-ttu-id="163e0-103">Azure AD B2C: bir .NET web uygulamasından .NET web API'si çağırma</span><span class="sxs-lookup"><span data-stu-id="163e0-103">Azure AD B2C: Call a .NET web API from a .NET web app</span></span>

<span data-ttu-id="163e0-104">Azure AD B2C kullanarak güçlü kimlik yönetimi özelliklerini tooyour web uygulamaları ve web API'leri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="163e0-104">By using Azure AD B2C, you can add powerful identity management features tooyour web apps and web APIs.</span></span> <span data-ttu-id="163e0-105">Bu makalede nasıl toorequest erişim belirteçleri ve .NET "Yapılacaklar listesi" çağrılarından olun ele web uygulama tooa .NET web API'si.</span><span class="sxs-lookup"><span data-stu-id="163e0-105">This article discusses how toorequest access tokens and make calls from a .NET "to-do list" web app tooa .NET web api.</span></span>

<span data-ttu-id="163e0-106">Bu makalede nasıl tooimplement oturum açma kapsamaz, kaydolma ve profil Yönetimi Azure AD B2C ile.</span><span class="sxs-lookup"><span data-stu-id="163e0-106">This article does not cover how tooimplement sign-in, sign-up and profile management with Azure AD B2C.</span></span> <span data-ttu-id="163e0-107">Merhaba kullanıcının kimliği zaten doğrulanmış sonra web API'leri çağırmaya odaklanır.</span><span class="sxs-lookup"><span data-stu-id="163e0-107">It focuses on calling web APIs after hello user is already authenticated.</span></span> <span data-ttu-id="163e0-108">Henüz yapmadıysanız, aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="163e0-108">If you haven't already, you should:</span></span>

* <span data-ttu-id="163e0-109">Kullanmaya başlama bir [.NET web uygulaması](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span><span class="sxs-lookup"><span data-stu-id="163e0-109">Get started with a [.NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md)</span></span>
* <span data-ttu-id="163e0-110">Kullanmaya başlama bir [.NET web API'si](active-directory-b2c-devquickstarts-api-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="163e0-110">Get started with a [.NET web api](active-directory-b2c-devquickstarts-api-dotnet.md)</span></span>

## <a name="prerequisite"></a><span data-ttu-id="163e0-111">Önkoşul</span><span class="sxs-lookup"><span data-stu-id="163e0-111">Prerequisite</span></span>

<span data-ttu-id="163e0-112">toobuild web çağıran bir web uygulaması API, gerekir:</span><span class="sxs-lookup"><span data-stu-id="163e0-112">toobuild a web application that calls a web api, you need to:</span></span>

1. <span data-ttu-id="163e0-113">[Bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="163e0-113">[Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>
2. <span data-ttu-id="163e0-114">[Bir web kayıt API](active-directory-b2c-app-registration.md#register-a-web-api).</span><span class="sxs-lookup"><span data-stu-id="163e0-114">[Register a web api](active-directory-b2c-app-registration.md#register-a-web-api).</span></span>
3. <span data-ttu-id="163e0-115">[Bir web uygulaması kaydetmek](active-directory-b2c-app-registration.md#register-a-web-app).</span><span class="sxs-lookup"><span data-stu-id="163e0-115">[Register a web app](active-directory-b2c-app-registration.md#register-a-web-app).</span></span>
4. <span data-ttu-id="163e0-116">[İlkeleri Ayarla](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="163e0-116">[Set up policies](active-directory-b2c-reference-policies.md).</span></span>
5. <span data-ttu-id="163e0-117">[GRANT hello web uygulama izinleri toouse hello web API'si](active-directory-b2c-access-tokens.md#publishing-permissions).</span><span class="sxs-lookup"><span data-stu-id="163e0-117">[Grant hello web app permissions toouse hello web api](active-directory-b2c-access-tokens.md#publishing-permissions).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="163e0-118">Merhaba istemci uygulaması ve web API hello aynı Azure AD B2C dizini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="163e0-118">hello client application and web API must use hello same Azure AD B2C directory.</span></span>
>

## <a name="download-hello-code"></a><span data-ttu-id="163e0-119">Merhaba kodu indirme</span><span class="sxs-lookup"><span data-stu-id="163e0-119">Download hello code</span></span>

<span data-ttu-id="163e0-120">Bu öğretici için kod Hello korunduğu [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="163e0-120">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="163e0-121">Çalıştırarak hello örnek kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="163e0-121">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="163e0-122">Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="163e0-122">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="163e0-123">Merhaba çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="163e0-123">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="163e0-124">`TaskWebApp`Kullanıcı hello bir MVC web uygulaması ile etkileşime giren olur.</span><span class="sxs-lookup"><span data-stu-id="163e0-124">`TaskWebApp` is a MVC web application that hello user interacts with.</span></span> <span data-ttu-id="163e0-125">`TaskService`her kullanıcının yapılacaklar listesini depolayan hello uygulamanızın arka uç web API'dır.</span><span class="sxs-lookup"><span data-stu-id="163e0-125">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="163e0-126">Bu makalede yapı hello kapsamaz `TaskWebApp` web uygulaması veya hello `TaskService` web API'si.</span><span class="sxs-lookup"><span data-stu-id="163e0-126">This article does not cover building hello `TaskWebApp` web app or hello `TaskService` web api.</span></span> <span data-ttu-id="163e0-127">toolearn toobuild hello .NET web uygulamasını Azure AD B2C kullanarak bkz bizim [.NET web uygulaması Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="163e0-127">toolearn how toobuild hello .NET web app using Azure AD B2C, see our [.NET web app tutorial](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span> <span data-ttu-id="163e0-128">nasıl toobuild hello .NET web API kullanarak Azure AD B2C, güvenliği toolearn bkz bizim [.NET web API'si Öğreticisi](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="163e0-128">toolearn how toobuild hello .NET web API secured using Azure AD B2C, see our [.NET web API tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

### <a name="update-hello-azure-ad-b2c-configuration"></a><span data-ttu-id="163e0-129">Hello Azure AD B2C yapılandırmasını güncelleştir</span><span class="sxs-lookup"><span data-stu-id="163e0-129">Update hello Azure AD B2C configuration</span></span>

<span data-ttu-id="163e0-130">Bizim örnek yapılandırılmış toouse hello ilkeleri ve istemci bizim demo Kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="163e0-130">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="163e0-131">Toouse isterseniz kendi Kiracı:</span><span class="sxs-lookup"><span data-stu-id="163e0-131">If you would like toouse your own tenant:</span></span>

1. <span data-ttu-id="163e0-132">Açık `web.config` hello içinde `TaskService` proje ve hello değerlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="163e0-132">Open `web.config` in hello `TaskService` project and replace hello values for</span></span>

    * <span data-ttu-id="163e0-133">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="163e0-133">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="163e0-134">`ida:ClientId`web API uygulama Kimliğinizle</span><span class="sxs-lookup"><span data-stu-id="163e0-134">`ida:ClientId` with your web api application ID</span></span>
    * <span data-ttu-id="163e0-135">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="163e0-135">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>

2. <span data-ttu-id="163e0-136">Açık `web.config` hello içinde `TaskWebApp` proje ve hello değerlerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="163e0-136">Open `web.config` in hello `TaskWebApp` project and replace hello values for</span></span>

    * <span data-ttu-id="163e0-137">kiracı adınızla `ida:Tenant`</span><span class="sxs-lookup"><span data-stu-id="163e0-137">`ida:Tenant` with your tenant name</span></span>
    * <span data-ttu-id="163e0-138">Web uygulamanızın kimliği ile `ida:ClientId`</span><span class="sxs-lookup"><span data-stu-id="163e0-138">`ida:ClientId` with your web app application ID</span></span>
    * <span data-ttu-id="163e0-139">Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`</span><span class="sxs-lookup"><span data-stu-id="163e0-139">`ida:ClientSecret` with your web app secret key</span></span>
    * <span data-ttu-id="163e0-140">"Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`</span><span class="sxs-lookup"><span data-stu-id="163e0-140">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
    * <span data-ttu-id="163e0-141">"Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`</span><span class="sxs-lookup"><span data-stu-id="163e0-141">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
    * <span data-ttu-id="163e0-142">"Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`</span><span class="sxs-lookup"><span data-stu-id="163e0-142">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>



## <a name="requesting-and-saving-an-access-token"></a><span data-ttu-id="163e0-143">İsteme ve bir erişim belirteci kaydetme</span><span class="sxs-lookup"><span data-stu-id="163e0-143">Requesting and saving an access token</span></span>

### <a name="specify-hello-permissions"></a><span data-ttu-id="163e0-144">Merhaba izinleri belirtin</span><span class="sxs-lookup"><span data-stu-id="163e0-144">Specify hello permissions</span></span>

<span data-ttu-id="163e0-145">Sipariş toomake hello çağrısı toohello web API'de, tooauthenticate hello kullanıcı (oturumu-up/oturum açma ilkeniz kullanılarak) gerekir ve [bir erişim belirteci almak](active-directory-b2c-access-tokens.md) Azure AD B2C'ndan.</span><span class="sxs-lookup"><span data-stu-id="163e0-145">In order toomake hello call toohello web API, you need tooauthenticate hello user (using your sign-up/sign-in policy) and [receive an access token](active-directory-b2c-access-tokens.md) from Azure AD B2C.</span></span> <span data-ttu-id="163e0-146">Sipariş tooreceive bir erişim belirteci'da, ilk hello erişim belirteci toogrant istediğiniz hello izinleri belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="163e0-146">In order tooreceive an access token, you first must specify hello permissions you would like hello access token toogrant.</span></span> <span data-ttu-id="163e0-147">Merhaba izinleri hello belirtilen `scope` hello isteği toohello yaptığınızda parametresi `/authorize` uç noktası.</span><span class="sxs-lookup"><span data-stu-id="163e0-147">hello permissions are specified in hello `scope` parameter when you make hello request toohello `/authorize` endpoint.</span></span> <span data-ttu-id="163e0-148">Örneğin, bir erişim belirteci ile Merhaba "Okuma" olan izni toohello kaynak uygulama tooacquire hello uygulama kimliği URI'sini `https://contoso.onmicrosoft.com/tasks`, hello kapsam olacaktır `https://contoso.onmicrosoft.com/tasks/read`.</span><span class="sxs-lookup"><span data-stu-id="163e0-148">For example, tooacquire an access token with hello “read” permission toohello resource application that has hello App ID URI of `https://contoso.onmicrosoft.com/tasks`, hello scope would be `https://contoso.onmicrosoft.com/tasks/read`.</span></span>

<span data-ttu-id="163e0-149">Bizim örnek, açık hello dosya toospecify hello kapsamda `App_Start\Startup.Auth.cs` ve hello tanımlamak `Scope` OpenIdConnectAuthenticationOptions değişkeni.</span><span class="sxs-lookup"><span data-stu-id="163e0-149">toospecify hello scope in our sample, open hello file `App_Start\Startup.Auth.cs` and define hello `Scope` variable in OpenIdConnectAuthenticationOptions.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

    app.UseOpenIdConnectAuthentication(
        new OpenIdConnectAuthenticationOptions
        {
            ...

            // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
            Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
        }
    );
}
```

### <a name="exchange-hello-authorization-code-for-an-access-token"></a><span data-ttu-id="163e0-150">Bir erişim belirteci için Exchange hello yetkilendirme kodu</span><span class="sxs-lookup"><span data-stu-id="163e0-150">Exchange hello authorization code for an access token</span></span>

<span data-ttu-id="163e0-151">Bir kullanıcı hello kaydolma veya oturum açma deneyimi tamamlandıktan sonra uygulamanızı Azure AD B2C ' bir yetkilendirme kodu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="163e0-151">After an user completes hello sign-up or sign-in experience, your app will receive an authorization code from Azure AD B2C.</span></span> <span data-ttu-id="163e0-152">Merhaba OWIN Openıd Connect Ara hello kodunu depolar, ancak bir erişim belirteci için exchange değil.</span><span class="sxs-lookup"><span data-stu-id="163e0-152">hello OWIN OpenID Connect middleware will store hello code, but will not exchange it for an access token.</span></span> <span data-ttu-id="163e0-153">Merhaba kullanabilirsiniz [MSAL Kitaplığı](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span><span class="sxs-lookup"><span data-stu-id="163e0-153">You can use hello [MSAL library](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange.</span></span> <span data-ttu-id="163e0-154">Bir yetkilendirme kodu alındığında Örneğimizde, biz bildirimi geri araması hello ara yazılım Openıd Connect yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="163e0-154">In our sample, we configured a notification callback into hello OpenID Connect middleware whenever an authorization code is received.</span></span> <span data-ttu-id="163e0-155">Merhaba geri arama, biz MSAL tooexchange hello kodu için bir belirteç kullanın ve hello belirteci hello önbelleğe kaydedin.</span><span class="sxs-lookup"><span data-stu-id="163e0-155">In hello callback, we use MSAL tooexchange hello code for a token and save hello token into hello cache.</span></span>

```CSharp
/*
* Callback function when an authorization code is received
*/
private async Task OnAuthorizationCodeReceived(AuthorizationCodeReceivedNotification notification)
{
    // Extract hello code from hello response notification
    var code = notification.Code;

    var userObjectId = notification.AuthenticationTicket.Identity.FindFirst(ObjectIdElement).Value;
    var authority = String.Format(AadInstance, Tenant, DefaultPolicy);
    var httpContext = notification.OwinContext.Environment["System.Web.HttpContextBase"] as HttpContextBase;

    // Exchange hello code for a token. Make sure toospecify hello necessary scopes
    ClientCredential cred = new ClientCredential(ClientSecret);
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                            RedirectUri, cred, new NaiveSessionCache(userObjectId, httpContext));
    var authResult = await app.AcquireTokenByAuthorizationCodeAsync(new string[] { ReadTasksScope, WriteTasksScope }, code, DefaultPolicy);
}
```

## <a name="calling-hello-web-api"></a><span data-ttu-id="163e0-156">Merhaba web API çağırma</span><span class="sxs-lookup"><span data-stu-id="163e0-156">Calling hello web API</span></span>

<span data-ttu-id="163e0-157">Bu bölümde, nasıl sırasında toouse hello belirteci alınan anlatılmaktadır oturumu-up/oturum açma Azure AD B2C ile sırayla web API tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="163e0-157">This section discusses how toouse hello token received during sign-up/sign-in with Azure AD B2C in order tooaccess hello web API.</span></span>

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a><span data-ttu-id="163e0-158">Merhaba denetleyicileri kaydedilmiş hello belirteci alma</span><span class="sxs-lookup"><span data-stu-id="163e0-158">Retrieve hello saved token in hello controllers</span></span>

<span data-ttu-id="163e0-159">Merhaba `TasksController` hello web API ile iletişim kurmak için sorumludur ve HTTP isteklerini toohello API tooread göndermek için oluşturmak ve görevleri silin.</span><span class="sxs-lookup"><span data-stu-id="163e0-159">hello `TasksController` is responsible for communicating with hello web API and for sending HTTP requests toohello API tooread, create, and delete tasks.</span></span> <span data-ttu-id="163e0-160">Merhaba API Azure AD B2C tarafından korumalı olduğundan, yukarıdaki adımı hello kaydettiğiniz toofirst alma hello belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="163e0-160">Because hello API is secured by Azure AD B2C, you need toofirst retrieve hello token you saved in hello above step.</span></span>

```CSharp
// Controllers\TasksController.cs

/*
* Uses MSAL tooretrieve hello token from hello cache
*/
private async void acquireToken(String[] scope)
{
    string userObjectID = ClaimsPrincipal.Current.FindFirst(Startup.ObjectIdElement).Value;
    string authority = String.Format(Startup.AadInstance, Startup.Tenant, Startup.DefaultPolicy);

    ClientCredential credential = new ClientCredential(Startup.ClientSecret);

    // Retrieve hello token using hello provided scopes
    ConfidentialClientApplication app = new ConfidentialClientApplication(authority, Startup.ClientId,
                                        Startup.RedirectUri, credential,
                                        new NaiveSessionCache(userObjectID, this.HttpContext));
    AuthenticationResult result = await app.AcquireTokenSilentAsync(scope);

    accessToken = result.Token;
}
```

### <a name="read-tasks-from-hello-web-api"></a><span data-ttu-id="163e0-161">Merhaba web API görevlerini okuma</span><span class="sxs-lookup"><span data-stu-id="163e0-161">Read tasks from hello web API</span></span>

<span data-ttu-id="163e0-162">Bir belirteç olduğunda toohello HTTP iliştirebilirsiniz `GET` hello istekte `Authorization` üstbilgi toosecurely çağrısı `TaskService`:</span><span class="sxs-lookup"><span data-stu-id="163e0-162">When you have a token, you can attach it toohello HTTP `GET` request in hello `Authorization` header toosecurely call `TaskService`:</span></span>

```CSharp
// Controllers\TasksController.cs

public async Task<ActionResult> Index()
{
    try {

        // Retrieve hello token with hello specified scopes
        acquireToken(new string[] { Startup.ReadTasksScope });

        HttpClient client = new HttpClient();
        HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, apiEndpoint);

        // Add token toohello Authorization header and make hello request
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = await client.SendAsync(request);

        // Handle response ...
}

```

### <a name="create-and-delete-tasks-on-hello-web-api"></a><span data-ttu-id="163e0-163">Oluşturma ve hello web API görevleri silme</span><span class="sxs-lookup"><span data-stu-id="163e0-163">Create and delete tasks on hello web API</span></span>

<span data-ttu-id="163e0-164">Aynı deseni, gönderdiğinizde izleyin hello `POST` ve `DELETE` MSAL tooretrieve hello erişim belirteci hello önbellekten kullanarak toohello web API, ister.</span><span class="sxs-lookup"><span data-stu-id="163e0-164">Follow hello same pattern when you send `POST` and `DELETE` requests toohello web API, using MSAL tooretrieve hello access token from hello cache.</span></span>

## <a name="run-hello-sample-app"></a><span data-ttu-id="163e0-165">Merhaba örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="163e0-165">Run hello sample app</span></span>

<span data-ttu-id="163e0-166">Son olarak, yapı ve her iki hello uygulamaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="163e0-166">Finally, build and run both hello apps.</span></span> <span data-ttu-id="163e0-167">Kaydolma ve oturum açın ve hello oturum açmış kullanıcı için Görevler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="163e0-167">Sign up and sign in, and create tasks for hello signed-in user.</span></span> <span data-ttu-id="163e0-168">Oturumu kapatın ve farklı bir kullanıcı olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="163e0-168">Sign out and sign in as a different user.</span></span> <span data-ttu-id="163e0-169">Bu kullanıcı için Görevler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="163e0-169">Create tasks for that user.</span></span> <span data-ttu-id="163e0-170">Merhaba API, aldığı hello belirtecinden hello kullanıcının kimliğini ayıkladığı için nasıl hello görevleri kullanıcı başına hello API, üzerinde olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="163e0-170">Notice how hello tasks are stored per-user on hello API, because hello API extracts hello user's identity from hello token it receives.</span></span> <span data-ttu-id="163e0-171">Ayrıca hello kapsamlarla yürütmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="163e0-171">Also try playing with hello scopes.</span></span> <span data-ttu-id="163e0-172">Merhaba iznini kaldırın çok "yazma" ve bir görev eklemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="163e0-172">Remove hello permission too"write" and then try adding a task.</span></span> <span data-ttu-id="163e0-173">Yalnızca hello kapsamını değiştirmek her zaman kullanıma emin toosign yapın.</span><span class="sxs-lookup"><span data-stu-id="163e0-173">Just make sure toosign out each time you change hello scope.</span></span>

