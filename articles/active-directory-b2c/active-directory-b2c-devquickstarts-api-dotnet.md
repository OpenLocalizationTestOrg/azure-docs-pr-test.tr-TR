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
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: .NET web API'si oluşturma

Azure Active Directory (Azure AD) B2C ile OAuth 2.0 erişim belirteçleri kullanarak web API'si güvenliğini sağlayabilirsiniz. Bu belirteçler istemci uygulamaları tooauthenticate toohello API izin verin. Bu makalede nasıl toocreate .NET MVC "Yapılacaklar listesi" API İstemci kullanıcılarının uygulama tooCRUD görevleri sağlayan gösterilmektedir. Merhaba web API'sini Azure AD B2C kullanarak güvenli ve kimliği doğrulanmış kullanıcılar toomanage kendi Yapılacaklar listesi yalnızca sağlar.

## <a name="create-an-azure-ad-b2c-directory"></a>Azure AD B2C dizini oluşturma

Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir. Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır. Henüz yoksa devam etmeden önce bu kılavuzda [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).

> [!NOTE]
> Merhaba istemci uygulaması ve web API hello aynı Azure AD B2C dizini kullanmanız gerekir.
>

## <a name="create-a-web-api"></a>Web API’si oluşturma

Ardından B2C dizininizde toocreate bir web API uygulaması gerekir. Bu ihtiyaçlarını uygulamanızla toosecurely, iletişim bilgileri Azure AD'ye verir. Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md). Şunları yaptığınızdan emin olun:

* Dahil bir **web uygulaması** veya **web API'si** hello uygulamada.
* Kullanım hello **yeniden yönlendirme URI'si** `https://localhost:44332/` hello web uygulaması için. Bu kod örneği için başlangıç web uygulaması istemci hello varsayılan konumu budur.
* Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama. Buna daha sonra ihtiyacınız olacak.
* **Uygulama Kimliği URI'si** alanına bir uygulama tanımlayıcısı girin.
* İzinleri hello aracılığıyla eklemek **kapsamları yayımlanan** menüsü.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>İlkelerinizi oluşturma

Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır. Azure AD B2C ile bir ilke toocommunicate toocreate gerekir. Merhaba kullanılarak birleştirilen oturumu-up/oturum açma ilkesi hello açıklandığı şekilde öneririz [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md). İlkeyi oluştururken şunları yaptığınızdan emin olun:

* İlkenizde, **Görünen ad** ve diğer kaydolma özniteliklerini seçin.
* Her ilke için uygulamanın talep ettiği gibi **Görünen ad** ve **Nesne Kimliği** öğelerini seçin. Diğer talepleri de seçebilirsiniz.
* Kopya hello **adı** oluşturduktan sonra her ilkenin. Hello ilkesi adı daha sonra ihtiyacınız olacak.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Hazır toobuild olduğunuz hello ilkesi başarıyla oluşturduktan sonra uygulamanızı.

## <a name="download-hello-code"></a>Merhaba kodu indirme

Bu öğretici için kod Hello korunduğu [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Çalıştırarak hello örnek kopyalayabilirsiniz:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı. Merhaba çözüm dosyası iki proje içerir: `TaskWebApp` ve `TaskService`. `TaskWebApp`Kullanıcı hello bir MVC web uygulaması ile etkileşime giren olur. `TaskService`her kullanıcının yapılacaklar listesini depolayan hello uygulamanızın arka uç web API'dır. Bu makalede yalnızca hello ele alınacaktır `TaskService` uygulama. toolearn nasıl toobuild `TaskWebApp` Azure AD B2C kullanarak bkz [bizim .NET web uygulaması Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Hello Azure AD B2C yapılandırmasını güncelleştir

Bizim örnek yapılandırılmış toouse hello ilkeleri ve istemci bizim demo Kiracı kimliğidir. Toouse isterseniz kendi Kiracı aşağıdaki toodo hello gerekir:

1. Açık `web.config` hello içinde `TaskService` proje ve hello değerlerini değiştirme
    * kiracı adınızla `ida:Tenant`
    * Web API uygulamanızın kimliği ile `ida:ClientId`
    * "Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`

2. Açık `web.config` hello içinde `TaskWebApp` proje ve hello değerlerini değiştirme
    * kiracı adınızla `ida:Tenant`
    * Web uygulamanızın kimliği ile `ida:ClientId`
    * Web uygulamanızın gizli anahtarı ile `ida:ClientSecret`
    * "Kaydolma veya Oturum açma" ilkenizin adıyla `ida:SignUpSignInPolicyId`
    * "Profil Düzenleme" ilkenizin adıyla `ida:EditProfilePolicyId`
    * "Parola Sıfırlama" ilkenizin adıyla `ida:ResetPasswordPolicyId`


## <a name="secure-hello-api"></a>Merhaba API güvenli

API’nizi çağıran bir istemciniz olduğunda API’nizin (örn. `TaskService`) güvenliğini OAuth 2.0 taşıyıcı belirteçlerini kullanarak sağlayabilirsiniz. Bu her isteği tooyour API yalnızca bir taşıyıcı belirteci hello isteği varsa, geçerli olmasını sağlar. API'niz .NET (OWIN) kitaplığı için Microsoft'un Açık Web Arabirimi'ni kullanarak taşıyıcı belirteçleri kabul edebilir ve doğrulayabilir.

### <a name="install-owin"></a>OWIN yükleme

Merhaba Visual Studio Paket Yöneticisi konsolu kullanılarak Hello OWIN OAuth kimlik doğrulaması işlem hattı yükleyerek çalışmaya başlayın.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Bu kabul etmek ve taşıyıcı belirteçleri doğrulamak hello OWIN ara yazılımı yükler.

### <a name="add-an-owin-startup-class"></a>OWIN başlangıç sınıfı ekleme

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

### <a name="configure-oauth-20-authentication"></a>OAuth 2.0 kimlik doğrulamasını yapılandırma

Açık hello dosya `App_Start\Startup.Auth.cs`ve hello uygulamak `ConfigureAuth(...)` yöntemi. Örneğin, hello şu şekilde görünebilir:

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

### <a name="secure-hello-task-controller"></a>Merhaba görev denetleyicisinin güvenliğini sağlama

Merhaba uygulama yapılandırılmış toouse OAuth 2.0 kimlik doğrulaması getirildikten sonra ekleyerek web API güvenliğini sağlayabilirsiniz bir `[Authorize]` etiketi toohello görev denetleyicisi. Bu hello tüm denetleyicinin hello sınıf düzeyinde güvenliğini sağlamanız gerekir böylece tüm yapılacaklar listesi işlemelerinin, gerçekleştiği hello denetleyicisidir. Merhaba de ekleyebilirsiniz `[Authorize]` tooindividual Eylemler daha ayrıntılı denetim için etiket.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Kullanıcı bilgilerini hello belirteci alma

`TasksController`görevleri her görev sahibi "Merhaba görev" bir ilişkili kullanıcının sahip olduğu bir veritabanında depolar. Merhaba sahibi hello kullanıcı tarafından tanımlanan **nesne kimliği**. (Bir uygulama olarak tooadd hello nesne kimliği gerekli bu yüzden talep ilkelerinizi tümünde.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Merhaba belirteci Hello izinleri doğrula

Web API'leri için ortak bir gereksinim toovalidate hello "kapsamlar" Merhaba belirtecinde ' dir. Bu, o hello kullanıcı toohello izinleri gerekli tooaccess hello Yapılacaklar listesi hizmet verdiği sağlar.

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

## <a name="run-hello-sample-app"></a>Merhaba örnek uygulamayı çalıştırma

Son olarak hem `TaskWebApp` hem de `TaskService` öğesini oluşturup çalıştırın. Merhaba kullanıcının Yapılacaklar listesinde bazı görevler oluşturun ve hatta durdurmak ve hello istemci yeniden başlattıktan sonra nasıl bunlar hello API kalıcı olduğuna dikkat edin.

## <a name="edit-your-policies"></a>İlkelerinizi düzenleme

Azure AD B2C kullanarak API güvenliğini sağladıktan sonra oturum-açma/kaydolma ilke ve görünüm hello etkileri (veya bunların olmaması) hello API ile deneyebilirsiniz. Merhaba uygulama talepleri hello ilkelerinde işlemek ve hello web API'SİNDE kullanılabilen hello kullanıcı bilgilerini değiştirin. Eklediğiniz herhangi bir talep kullanılabilir tooyour .NET MVC web API'si hello olacaktır `ClaimsPrincipal` , bu makalenin önceki bölümlerinde açıklandığı gibi nesne.
