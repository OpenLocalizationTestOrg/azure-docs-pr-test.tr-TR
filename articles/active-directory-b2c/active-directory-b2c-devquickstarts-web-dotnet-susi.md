---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "Nasıl toobuild oturumu-up/oturum açma, sahip bir web uygulaması düzenleme ve parola sıfırlama ve Azure Active Directory B2C kullanarak profil."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a>Azure Active Directory B2C kaydolma, oturum açma profili düzenleme ve parola sıfırlama ile bir ASP.NET web uygulaması oluşturma

Bu öğretici şunların nasıl yapıldığını gösterir:

> [!div class="checklist"]
> * Azure AD B2C kimlik özellikleri tooyour web uygulaması Ekle
> * Azure AD B2C dizininizde web uygulamanızı kaydetme
> * Kullanıcı oturumu-up/oturum açma, profil düzenleme ve web uygulamanız için parola sıfırlama ilkesi oluşturma

## <a name="prerequisites"></a>Ön koşullar

- Azure hesabı, B2C Kiracı tooan bağlanmanız gerekir. Ücretsiz bir Azure hesabı oluşturabilirsiniz [burada](https://azure.microsoft.com/en-us/).
- Gereksinim duyduğunuz [Microsoft Visual Studio](https://www.visualstudio.com/) veya benzeri program tooview ve hello örnek kodu değiştirin.

## <a name="create-an-azure-ad-b2c-directory"></a>Azure AD B2C dizini oluşturma

Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir. Bir dizin, tüm kullanıcıların, uygulamaları, grupları ve daha fazlası için bir kapsayıcıdır. Zaten yoksa, bu kılavuza devam etmeden önce bir B2C dizini oluşturun.

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> Tooconnect hello B2C Kiracı tooyour Azure aboneliği gerekir. Seçtikten sonra **oluşturma**seçin hello **bağlantı var olan bir Azure AD B2C Kiracı toomy Azure aboneliği** seçeneğini ve ardından hello **Azure AD B2C Kiracısı** açılan, seçin Merhaba Kiracı tooassociate istiyor.

## <a name="create-and-register-an-application"></a>Oluşturma ve bir uygulamayı kaydetme

Ardından, toocreate gerekir ve B2C dizininizde hello uygulama kaydedin. Bu Azure AD B2C toosecurely gereken bilgileri sağlar uygulamanız ile iletişim kurması. 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

İşiniz bittiğinde, uygulamanızın ayarlarını bir API ve yerel bir uygulamaya gerekir.

## <a name="create-policies-on-your-b2c-tenant"></a>B2C kiracınızın ilkeleri oluşturma

Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır. Bu kod örneği üç kimlik deneyimi içerir: **kaydolma ve oturum açma**, **düzenleme profil**, ve **parola sıfırlama**.  Hello açıklandığı gibi her tür bir ilke toocreate gerek [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md). Her ilke için tooselect hello görünen adı özniteliği veya talep ve daha sonra kullanmak için hello ad ilkenizin aşağı toocopy emin olun.

### <a name="add-your-identity-providers"></a>Kimlik sağlayıcısı ekleyin

Ayarlarınızı seçin **kimlik sağlayıcıları** ve kullanıcı adı kayıt ya da e-posta'i seçin.

### <a name="create-a-sign-up-and-sign-in-policy"></a>Kaydolma ve oturum açma ilkesi oluşturma

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a>İlke düzenleme profil oluşturma

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a>Bir parola sıfırlama ilkesi oluşturma

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

İlkelerinizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.

## <a name="download-hello-sample-code"></a>Merhaba örnek kodu indirin

Bu öğretici için kod Hello korunduğu [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Çalıştırarak hello örnek kopyalayabilirsiniz:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı. Merhaba çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`. `TaskWebApp`Merhaba kullanıcı hello MVC web uygulaması ile etkileşime giren olur. `TaskService`her kullanıcının yapılacaklar listesini depolayan hello uygulamanızın arka uç web API'dır. Bu makalede yalnızca hello ele alınacaktır `TaskWebApp` uygulama. toolearn nasıl toobuild `TaskService` Azure AD B2C kullanarak bkz [.NET web API'si öğreticimizi](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="update-code-toouse-your-tenant-and-policies"></a>Kiracı ve ilkeleri kod toouse güncelleştir

Bizim örnek yapılandırılmış toouse hello ilkeleri ve istemci bizim demo Kiracı kimliğidir. tooconnect, tooyour kendi Kiracı tooopen gerek `web.config` hello içinde `TaskWebApp` proje ve değerleri aşağıdaki hello değiştirin:

* kiracı adınızla `ida:Tenant`
* Web uygulamanızın kimliği ile `ida:ClientId`
* Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`
* "Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`
* "Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`
* "Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`

## <a name="launch-hello-app"></a>Merhaba uygulamasını başlatın
Gelen Visual Studio içinde hello uygulamasını başlatın. Toohello Yapılacaklar listesi sekmesi ve URL Not hello gidin: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...

E-posta adresi veya kullanıcı adı kullanarak Hello uygulaması için kaydolun. Çıkışı, oturum daha sonra yeniden oturum açın ve hello profili düzenlemek veya hello parola sıfırlama. Oturumu kapatın ve farklı bir kullanıcı olarak oturum açın. 

## <a name="add-social-idps"></a>Sosyal IDPs Ekle

Şu anda kullanarak yalnızca kullanıcı kaydolma ve oturum açma'de hello uygulama'yı destekler **yerel hesaplar**; B2C dizininizde depolanan hesapları, bir kullanıcı adı ve parola kullanın. Azure AD B2C kullanarak diğer için destek ekleyebilmesi **kimlik sağlayıcıları** (IDPs) herhangi birini kodunuzu değiştirmeden.

tooadd sosyal IDPs tooyour uygulama, izleyerek başlamak hello ayrıntılı yönergeler bu makalelerde. Her IDP için toosupport istediğiniz, bu sistemde tooregister uygulamanın gerekir ve bir istemci kimliği alın

* [Facebook bir IDP ayarlayın](active-directory-b2c-setup-fb-app.md)
* [Google bir IDP ayarlayın](active-directory-b2c-setup-goog-app.md)
* [Amazon bir IDP ayarlayın](active-directory-b2c-setup-amzn-app.md)
* [LinkedIn bir IDP ayarlayın](active-directory-b2c-setup-li-app.md)

Eklediğiniz sonra hello kimlik sağlayıcıları tooyour B2C dizini, düzenlemesini her üç ilke tooinclude hello açıklandığı gibi yeni IDPs hello [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md). İlkelerinizi kaydettikten sonra hello uygulamayı yeniden çalıştırın.  Oturum açma ve kaydolma seçenekleri her kimlik deneyimlerinizi yeni IDPs eklenen hello görmeniz gerekir.

İlkelerinizle denemeler ve örnek uygulamanızı hello etkisi gözlemleyin. Ekleyebilir veya IDPs kaldırmak, uygulamanın talep değiştirmek veya kaydolma özniteliklerini değiştirebilirsiniz. İlkeleri ve kimlik doğrulama isteklerini OWIN nasıl birbirine bağlayan görene kadar deneyin.

## <a name="sample-code-walkthrough"></a>Örnek kod gözden geçirme
Aşağıdaki bölümlerde hello hello örnek uygulama kodu nasıl yapılandırıldığını gösterir. Bu kılavuz olarak gelecekte uygulama geliştirmede kullanabilir.

### <a name="add-authentication-support"></a>Kimlik doğrulama desteği ekleme

Artık, uygulama toouse Azure AD B2C yapılandırabilirsiniz. Uygulamanız, Openıd Connect kimlik doğrulama istekleri göndererek Azure AD B2C ile iletişim kurar. Merhaba istekleri dikte hello kullanıcı deneyimi hello İlkesi belirterek tooexecute uygulamanızı istemektedir. Bu istekleri Microsoft'un OWIN kitaplığı toosend kullanın, ilkeleri yürütmek, kullanıcı oturumları ve daha fazlasını yönetebilirsiniz.

#### <a name="install-owin"></a>OWIN yükleme

toobegin, hello Visual Studio Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello projesi ekleyin.

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a>OWIN başlangıç sınıfı ekleme

Bir OWIN başlangıç sınıfı toohello API adlı eklemek `Startup.cs`.  Merhaba projede, select sağ **Ekle** ve **yeni öğe**ve ardından OWIN'i aratın. Merhaba OWIN ara yazılımı hello çağırılır `Configuration(…)` uygulamanız başladığında yöntemi.

Örneğimizde, biz hello sınıf bildirimi çok değiştirilen`public partial class Startup` ve uygulanan diğer hello sınıfında parçası hello `App_Start\Startup.Auth.cs`. İç hello `Configuration` yöntemi, bir çağrı çok eklediğimiz`ConfigureAuth`, içinde tanımlanan `Startup.Auth.cs`. Merhaba değişiklikler sonra `Startup.cs` hello aşağıdaki gibi görünür:

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

#### <a name="configure-hello-authentication-middleware"></a>Merhaba kimlik doğrulaması ara yazılımını yapılandırma

Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(...)` yöntemi. Merhaba, sağladığınız parametreler `OpenIdConnectAuthenticationOptions` , uygulama toocommunicate Azure AD B2C ile koordinatları olarak hizmet. Belirli parametreleri belirtmezseniz hello varsayılan değeri kullanır. Örneğin, biz hello belirtmeyin `ResponseType` hello örneğinde, böylece varsayılan değer hello `code id_token` her giden istek tooAzure AD B2C kullanılacak.

Tanımlama bilgisi kimlik doğrulamasını oluşturan tooset de gerekir. Merhaba Openıd Connect ara yazılım tanımlama bilgilerini toomaintain kullanıcı oturumları, başka şeylerin kullanır.

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

İçinde `OpenIdConnectAuthenticationOptions` geri çağırma işlevleri hello ara yazılımı Openıd Connect tarafından alınan belirli bildirimleri için bir dizi yukarıdaki tanımlarız. Bu davranışların kullanarak tanımlanan bir `OpenIdConnectAuthenticationNotifications` nesne ve hello depolanmış `Notifications` değişkeni. Örneğimizde, biz hello olay bağlı olarak üç farklı geri aramalar tanımlayın.

### <a name="using-different-policies"></a>Farklı ilkelerini kullanma

Merhaba `RedirectToIdentityProvider` bildirim tooAzure AD B2C bir istek yapıldığında tetiklenir. Merhaba geri arama işlevinde `OnRedirectToIdentityProvider`, biz toouse istiyoruz, çağrı giden hello başka bir ilke kontrol edin. İlke hello varsayılan "Kaydolma veya oturum açma" ilke yerine Hello parola sıfırlama gibi bir parola sıfırlama veya bir profili düzenlemek sipariş toodo içinde toouse hello ilgili ilkeyi gerekir.

Bir kullanıcı tooreset hello parola istediği veya hello profili düzenlediğinizde Örneğimizde, biz biz toouse hello OWIN bağlamına tercih hello ilkesi ekleyin. Hello aşağıdakileri yaparak yapılabilir:

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

Ve hello geri çağırma işlevi uygulayabilirsiniz `OnRedirectToIdentityProvider` hello aşağıdakileri yaparak:

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a>Yetkilendirme kodları işleme

Merhaba `AuthorizationCodeReceived` bildirim bir yetkilendirme kodu alındığında tetiklenir. Merhaba Openıd Connect Ara değiş tokuşu kodları için erişim belirteçleri desteklemez. Bir geri çağırma işlevini hello belirteçte hello kodunu el ile değiştirebilir. Daha fazla bilgi için lütfen hello bakın [belgelerine](active-directory-b2c-devquickstarts-web-api-dotnet.md) , açıklar nasıl.

### <a name="handling-errors"></a>Hataları işleme

Merhaba `AuthenticationFailed` bildirim kimlik doğrulama başarısız olduğunda tetiklenir. İstediğiniz gibi kendi geri çağırma yönteminde hello hataları işleyebilir. Merhaba hata kodunu denetle ancak eklemelisiniz `AADB2C90118`. Merhaba "Kaydolma veya oturum açma" ilke Hello yürütülmesi sırasında hello kullanıcının hello fırsat tooselect sahip bir **parolanızı mı unuttunuz?** bağlantı. Bu durumda, uygulamanızı hello parolası sıfırlama ilkesini kullanmayı bir istek olmalısınız belirten bu hata kodu, uygulamanızı Azure AD B2C gönderir.

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a>Kimlik doğrulama isteklerini tooAzure AD Gönder

Uygulamanızı Azure AD B2C ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur. OWIN kimlik doğrulama iletileri hazırlayın, Azure AD B2C gelen belirteçleri doğrulamak ve kullanıcı oturumu koruyarak hello ayrıntılarını yönetir. Tüm bu kalır tooinitiate her kullanıcının akışıdır.

Bir kullanıcı seçtiğinde **oturum yukarı/oturum açma**, **Düzenle profili**, veya **parola sıfırlama** hello web uygulamasında hello ilişkili eylemin çağrılması `Controllers\AccountController.cs`:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

OWIN toosign hello kullanıcının hello uygulama çıkışı de kullanabilirsiniz. İçinde `Controllers\AccountController.cs` sunuyoruz:

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

Bir ilke çağırma toplama tooexplicitly kullanabileceğiniz bir `[Authorize]` hello kullanıcı imzalı değilse bir ilke yürütür etiketinde denetleyicilerinizi. Açık `Controllers\HomeController.cs` ve hello ekleyin `[Authorize]` etiketi toohello talep denetleyicisi.  OWIN seçer hello son ilke hello yapılandırılmış `[Authorize]` etiketi isabet.

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a>Kullanıcı bilgilerini görüntüleme

Openıd Connect kullanarak kullanıcıların kimlik doğrulaması sırasında Azure AD B2C içeren kimliği belirteci toohello uygulama döndürür **talep**. Bunlar, hello kullanıcı hakkında onaylamalardır. Uygulamanızı talep toopersonalize kullanabilirsiniz.

Açık hello `Controllers\HomeController.cs` dosya. Denetleyicilerinizi hello aracılığıyla, kullanıcı talepleri erişim `ClaimsPrincipal.Current` güvenlik sorumlusu nesnesi.

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

Uygulamanızı hello aynı aldığını talep erişebileceği şekilde.  Merhaba uygulama aldığı tüm hello talepler listesinin hello üzerinde sizin için kullanılabilir **talep** sayfası.
