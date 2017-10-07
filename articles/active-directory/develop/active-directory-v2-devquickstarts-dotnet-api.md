---
title: "aaaAdd oturum açma tooa .NET MVC web API kullanarak Azure AD v2.0 uç hello | Microsoft Docs"
description: "Nasıl toobuild hem kişisel Microsoft Account gelen belirteçleri ve iş veya Okul hesapları kabul eden bir .NET MVC Web API."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Bir MVC web API güvenliğini sağlama
Azure Active Directory hello v2.0 uç ile Web API kullanarak koruyabilirsiniz [OAuth 2.0](active-directory-v2-protocols.md) erişim belirteçleri, hem kişisel Microsoft hesabı olan kullanıcılar ve iş veya Okul hesapları toosecurely Web API erişimi etkinleştirme.

> [!NOTE]
> Tüm Azure Active Directory senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
>
>

ASP.NET web API'da, bunu .NET Framework 4. 5 ' dahil Microsoft'un OWIN ara yazılımı kullanarak gerçekleştirebilirsiniz.  OWIN toobuild kullanıcının yapılacaklar listesi toocreate ve okuma görevlerden istemcilerinin veren "tooDo listesi" MVC Web API burada kullanacağız.  Merhaba web API gelen istekleri geçerli erişim belirteci içeren ve doğrulama korumalı bir rotaya geçmeyin istekleri reddedecek doğrular.  Bu örnek, Visual Studio 2015 kullanılarak oluşturuldu.

## <a name="download"></a>İndir
Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

Merhaba iskelet uygulama için basit bir API tüm hello Demirbaş kod içerir, ancak tüm hello kimlikle ilgili parçaları eksik. Toofollow boyunca istemiyorsanız, bunun yerine, kopyalayabilir veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>Bir uygulamayı kaydetme
En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).  Emin olun:

* Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.

Bu visual studio çözümü "basit bir WPF uygulaması olan bir TodoListClient", de içerir.  Merhaba TodoListClient nasıl bir kullanıcı oturum açtığında kullanılan toodemonstrate olduğundan ve bir istemci nasıl verebilir tooyour Web API ister.  Merhaba TodoListClient ve hello TodoListService hello tarafından bu durumda, gösterilen aynı uygulama.  tooconfigure TodoListClient Merhaba, ayrıca gerekir:

* Merhaba eklemek **mobil** uygulamanız için platform.

## <a name="install-owin"></a>OWIN yükleme
Bir uygulama kaydınız, sipariş toovalidate gelen istekleri & belirteçleri hello v2.0 uç noktası ile uygulama toocommunicate yukarı tooset gerekir.

* toobegin, hello çözümü açın ve hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello TodoListService proje ekleyin.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>OAuth kimlik doğrulamasını yapılandırma
* Adlı bir OWIN başlangıç sınıfı toohello TodoListService projesi eklemek `Startup.cs`.  Merhaba projeyi sağ tıklayarak--> **Ekle** --> **yeni öğe** "OWIN" arayın.  Merhaba OWIN ara yazılımı hello çağırılır `Configuration(…)` uygulamanız başladığında yöntemi.
* Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup` -zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.  Merhaba, `Configuration(…)` yöntemi çağrısı tooConfgureAuth(...) tooset web uygulamanız için kimlik doğrulaması kurma olun.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(…)` hello Web API tooaccept belirteçleri hello v2.0 uç noktasından ayarlayacaktır yöntemi.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* Kullanabileceğiniz artık `[Authorize]` denetleyicileri ve eylemleri OAuth 2.0 taşıyıcı kimlik doğrulaması ile tooprotect öznitelikleri.  Merhaba tasarlamanız `Controllers\TodoListController.cs` bir authorize etiketiyle sınıfı.  Bu sayfaya erişmeden önce bu hello kullanıcı toosign zorlar.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Ne zaman bir yetkili çağıran başarıyla çağırır hello birini `TodoListController` API'leri, hello eylem erişim tooinformation hello çağıran hakkında.  OWIN sağlar erişim toohello talep hello taşıyıcı belirteci hello aracılığıyla içinde `ClaimsPrincpal` nesnesi.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Son olarak, hello açmak `web.config` hello TodoListService proje hello kökünde bulunan dosya ve hello yapılandırma değerlerini girin `<appSettings>` bölümü.
  * `ida:Audience` Hello olan **uygulama kimliği** hello portalda girdiğiniz hello uygulamasının.

## <a name="configure-hello-client-app"></a>Merhaba istemci uygulamasını yapılandırma
Eylemin hello Yapılacaklar listesi hizmeti görebilmek hello v2.0 uç noktasından belirteç almak ve çağrıları toohello hizmeti hale tooconfigure hello Yapılacaklar listesi istemci gerekir.

* Merhaba TodoListClient projeyi açın `App.config` ve hello yapılandırma değerlerini girin `<appSettings>` bölümü.
  * `ida:ClientId` Uygulama hello portalından kopyaladığınız kimliği.

Son olarak, temiz, yapı ve her proje çalıştırın!  Artık hem kişisel Microsoft hesaplarını gelen belirteçleri ve iş veya Okul hesapları kabul eden bir .NET MVC Web API vardır.  Merhaba TodoListClient oturum ve arama, web API tooadd görevleri toohello kullanıcının yapılacaklar listesi.

Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Sonraki adımlar
Artık ek konu başlıklarına geçebilirsiniz.  Tootry isteyebilirsiniz:

[Bir Web uygulamasından Web API'si çağırma >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Ek kaynaklar için gözden geçirin:

* [Merhaba v2.0 Geliştirici Kılavuzu >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "azure-active-directory" etiketi >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Ürünlerimiz için güvenlik güncelleştirmelerini alma
Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.
