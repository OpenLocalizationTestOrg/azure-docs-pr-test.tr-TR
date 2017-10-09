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
# <a name="azure-ad-b2c-call-a-net-web-api-from-a-net-web-app"></a>Azure AD B2C: bir .NET web uygulamasından .NET web API'si çağırma

Azure AD B2C kullanarak güçlü kimlik yönetimi özelliklerini tooyour web uygulamaları ve web API'leri ekleyebilirsiniz. Bu makalede nasıl toorequest erişim belirteçleri ve .NET "Yapılacaklar listesi" çağrılarından olun ele web uygulama tooa .NET web API'si.

Bu makalede nasıl tooimplement oturum açma kapsamaz, kaydolma ve profil Yönetimi Azure AD B2C ile. Merhaba kullanıcının kimliği zaten doğrulanmış sonra web API'leri çağırmaya odaklanır. Henüz yapmadıysanız, aşağıdakileri yapmalısınız:

* Kullanmaya başlama bir [.NET web uygulaması](active-directory-b2c-devquickstarts-web-dotnet-susi.md)
* Kullanmaya başlama bir [.NET web API'si](active-directory-b2c-devquickstarts-api-dotnet.md)

## <a name="prerequisite"></a>Önkoşul

toobuild web çağıran bir web uygulaması API, gerekir:

1. [Bir Azure AD B2C kiracısı oluşturma](active-directory-b2c-get-started.md).
2. [Bir web kayıt API](active-directory-b2c-app-registration.md#register-a-web-api).
3. [Bir web uygulaması kaydetmek](active-directory-b2c-app-registration.md#register-a-web-app).
4. [İlkeleri Ayarla](active-directory-b2c-reference-policies.md).
5. [GRANT hello web uygulama izinleri toouse hello web API'si](active-directory-b2c-access-tokens.md#publishing-permissions).

> [!IMPORTANT]
> Merhaba istemci uygulaması ve web API hello aynı Azure AD B2C dizini kullanmanız gerekir.
>

## <a name="download-hello-code"></a>Merhaba kodu indirme

Bu öğretici için kod Hello korunduğu [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Çalıştırarak hello örnek kopyalayabilirsiniz:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı. Merhaba çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`. `TaskWebApp`Kullanıcı hello bir MVC web uygulaması ile etkileşime giren olur. `TaskService`her kullanıcının yapılacaklar listesini depolayan hello uygulamanızın arka uç web API'dır. Bu makalede yapı hello kapsamaz `TaskWebApp` web uygulaması veya hello `TaskService` web API'si. toolearn toobuild hello .NET web uygulamasını Azure AD B2C kullanarak bkz bizim [.NET web uygulaması Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet-susi.md). nasıl toobuild hello .NET web API kullanarak Azure AD B2C, güvenliği toolearn bkz bizim [.NET web API'si Öğreticisi](active-directory-b2c-devquickstarts-api-dotnet.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Hello Azure AD B2C yapılandırmasını güncelleştir

Bizim örnek yapılandırılmış toouse hello ilkeleri ve istemci bizim demo Kiracı kimliğidir. Toouse isterseniz kendi Kiracı:

1. Açık `web.config` hello içinde `TaskService` proje ve hello değerlerini değiştirme

    * kiracı adınızla `ida:Tenant`
    * `ida:ClientId`web API uygulama Kimliğinizle
    * "Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`

2. Açık `web.config` hello içinde `TaskWebApp` proje ve hello değerlerini değiştirme

    * kiracı adınızla `ida:Tenant`
    * Web uygulamanızın kimliği ile `ida:ClientId`
    * Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`
    * "Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`
    * "Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`
    * "Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`



## <a name="requesting-and-saving-an-access-token"></a>İsteme ve bir erişim belirteci kaydetme

### <a name="specify-hello-permissions"></a>Merhaba izinleri belirtin

Sipariş toomake hello çağrısı toohello web API'de, tooauthenticate hello kullanıcı (oturumu-up/oturum açma ilkeniz kullanılarak) gerekir ve [bir erişim belirteci almak](active-directory-b2c-access-tokens.md) Azure AD B2C'ndan. Sipariş tooreceive bir erişim belirteci'da, ilk hello erişim belirteci toogrant istediğiniz hello izinleri belirtmeniz gerekir. Merhaba izinleri hello belirtilen `scope` hello isteği toohello yaptığınızda parametresi `/authorize` uç noktası. Örneğin, bir erişim belirteci ile Merhaba "Okuma" olan izni toohello kaynak uygulama tooacquire hello uygulama kimliği URI'sini `https://contoso.onmicrosoft.com/tasks`, hello kapsam olacaktır `https://contoso.onmicrosoft.com/tasks/read`.

Bizim örnek, açık hello dosya toospecify hello kapsamda `App_Start\Startup.Auth.cs` ve hello tanımlamak `Scope` OpenIdConnectAuthenticationOptions değişkeni.

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

### <a name="exchange-hello-authorization-code-for-an-access-token"></a>Bir erişim belirteci için Exchange hello yetkilendirme kodu

Bir kullanıcı hello kaydolma veya oturum açma deneyimi tamamlandıktan sonra uygulamanızı Azure AD B2C ' bir yetkilendirme kodu alırsınız. Merhaba OWIN Openıd Connect Ara hello kodunu depolar, ancak bir erişim belirteci için exchange değil. Merhaba kullanabilirsiniz [MSAL Kitaplığı](https://github.com/AzureAD/microsoft-authentication-library-for-dotnet) toomake hello exchange. Bir yetkilendirme kodu alındığında Örneğimizde, biz bildirimi geri araması hello ara yazılım Openıd Connect yapılandırılmış. Merhaba geri arama, biz MSAL tooexchange hello kodu için bir belirteç kullanın ve hello belirteci hello önbelleğe kaydedin.

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

## <a name="calling-hello-web-api"></a>Merhaba web API çağırma

Bu bölümde, nasıl sırasında toouse hello belirteci alınan anlatılmaktadır oturumu-up/oturum açma Azure AD B2C ile sırayla web API tooaccess hello.

### <a name="retrieve-hello-saved-token-in-hello-controllers"></a>Merhaba denetleyicileri kaydedilmiş hello belirteci alma

Merhaba `TasksController` hello web API ile iletişim kurmak için sorumludur ve HTTP isteklerini toohello API tooread göndermek için oluşturmak ve görevleri silin. Merhaba API Azure AD B2C tarafından korumalı olduğundan, yukarıdaki adımı hello kaydettiğiniz toofirst alma hello belirteci gerekir.

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

### <a name="read-tasks-from-hello-web-api"></a>Merhaba web API görevlerini okuma

Bir belirteç olduğunda toohello HTTP iliştirebilirsiniz `GET` hello istekte `Authorization` üstbilgi toosecurely çağrısı `TaskService`:

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

### <a name="create-and-delete-tasks-on-hello-web-api"></a>Oluşturma ve hello web API görevleri silme

Aynı deseni, gönderdiğinizde izleyin hello `POST` ve `DELETE` MSAL tooretrieve hello erişim belirteci hello önbellekten kullanarak toohello web API, ister.

## <a name="run-hello-sample-app"></a>Merhaba örnek uygulamayı çalıştırma

Son olarak, yapı ve her iki hello uygulamaları çalıştırın. Kaydolma ve oturum açın ve hello oturum açmış kullanıcı için Görevler oluşturun. Oturumu kapatın ve farklı bir kullanıcı olarak oturum açın. Bu kullanıcı için Görevler oluşturun. Merhaba API, aldığı hello belirtecinden hello kullanıcının kimliğini ayıkladığı için nasıl hello görevleri kullanıcı başına hello API, üzerinde olduğuna dikkat edin. Ayrıca hello kapsamlarla yürütmeyi deneyin. Merhaba iznini kaldırın çok "yazma" ve bir görev eklemeyi deneyin. Yalnızca hello kapsamını değiştirmek her zaman kullanıma emin toosign yapın.

