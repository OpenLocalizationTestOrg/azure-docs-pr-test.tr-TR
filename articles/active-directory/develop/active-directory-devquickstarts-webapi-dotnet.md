---
title: "aaaAzure AD .NET web API'si Başlarken | Microsoft Docs"
description: "Nasıl toobuild .NET MVC web API, kimlik doğrulama ve yetkilendirme için Azure AD ile tümleşir."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Azure AD'den taşıyıcı belirteçlerini kullanarak bir web API korunmasına yardımcı olma
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Tooprotected kaynaklara erişim sağlayan bir uygulama oluşturuyorsanız tooknow gereksinim nasıl tooprevent unwarranted toothose kaynaklarına erişim.
Azure Active Directory (Azure AD), kolaylaştırır ve basit toohelp yalnızca birkaç kod satırıyla, OAuth 2.0 taşıyıcı erişim belirteçleri kullanarak web API'si koruyun.

ASP.NET web uygulamalarında hello Microsoft .NET Framework 4. 5 ' dahil hello topluluk odaklı OWIN ara yazılımı uyarlamasını kullanarak bu koruma gerçekleştirebilirsiniz. OWIN toobuild "tooDo listesi" web API'sini burada kullanacağız:

* API olan atayan korumalı.
* Merhaba web API çağrıları geçerli erişim belirteci içeren doğrular.

toobuild hello tooDo listesi API, önce yapmanız gerekir:

1. Bir uygulamayı Azure AD'ye kaydedin.
2. Merhaba uygulama toouse hello OWIN kimlik doğrulaması ardışık ayarlayın.
3. İstemci uygulama toocall hello web API'si yapılandırın.

başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Her bir Visual Studio 2013 çözümüdür. Ayrıca, uygulamanızın hangi tooregister içinde Azure AD kiracısı gerekir. Zaten yoksa, [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>1. adım: bir uygulamayı Azure AD ile kaydedin.
toohelp güvenli uygulamanız, ilk kiracınızda toocreate uygulamanın gereksinim ve birkaç temel bilgiler ile Azure AD sağlayın.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).

2. Merhaba üst çubuğunda hesabınızı tıklatın. Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.

3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.

4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.

5. Merhaba komut istemlerini izleyin ve yeni bir **Web uygulaması ve/veya Web API**.
  * **Ad** uygulama toousers açıklar. Girin **tooDo listesi hizmeti**.
  * **Yeniden yönlendirme URI'si** herhangi belirteçler uygulamanızı istedi tooreturn Azure AD kullanır ve dize şeması bir birleşimidir. Girin `https://localhost:44321/` bu değer için.

6. Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin. Kiracı özgü bir tanımlayıcı girin. Örneğin, `https://contoso.onmicrosoft.com/TodoListService` girin.

7. Merhaba yapılandırmayı kaydedin. Ayrıca tooregister istemci uygulamanızın kısa bir süre içinde gerekir çünkü hello portal kapatmayın.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>2. adım: hello uygulama toouse hello OWIN kimlik doğrulaması ardışık ayarlayın
toovalidate gelen istekleri ve belirteçler, Azure AD ile uygulama toocommunicate yukarı tooset gerekir.

1. toobegin, hello çözüm açın ve hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello TodoListService projesi ekleyin.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Adlı bir OWIN başlangıç sınıfı toohello TodoListService projesi eklemek `Startup.cs`.  Sağ hello proje, select **Ekle** > **yeni öğe**, arayın ve sonra **OWIN**. Merhaba OWIN ara yazılımı hello çağırılır `Configuration(…)` uygulamanız başladığında yöntemi.

3. Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup`. Zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık. Merhaba, `Configuration(…)` yöntemi, çok çağırmaya`ConfgureAuth(…)` tooset web uygulamanız için kimlik doğrulaması ayarlama.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(…)` yöntemi. Merhaba sağladığınız parametreler `WindowsAzureActiveDirectoryBearerAuthenticationOptions` , uygulama toocommunicate Azure AD ile koordinatları olarak hizmet verecektir.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. Kullanabileceğiniz artık `[Authorize]` öznitelikleri toohelp denetleyicileri ve eylemleri JSON Web Token (JWT) taşıyıcı kimlik doğrulaması ile koruyun. Merhaba tasarlamanız `Controllers\TodoListController.cs` bir authorize etiketiyle sınıfı. Bu sayfaya erişmeden önce bu hello kullanıcı toosign zorlar.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Ne zaman bir yetkili çağıran başarıyla çağırır hello birini `TodoListController` API'leri, hello eylem erişim tooinformation hello çağıran hakkında. OWIN sağlar erişim toohello talep hello taşıyıcı belirteci hello aracılığıyla içinde `ClaimsPrincpal` nesnesi.  

6. Web API'leri için ortak bir gereksinim toovalidate hello "kapsamlar" Merhaba belirtecinde ' dir. Bu, o hello kullanıcı toohello izinleri gerekli tooaccess hello tooDo listesi hizmet verdiği sağlar.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Açık hello `web.config` hello TodoListService proje hello kökünde bulunan dosya ve hello yapılandırma değerlerini girin `<appSettings>` bölümü.
  * `ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com Hello adıdır.
  * `ida:Audience`olan hello hello Azure portal girdiğiniz hello uygulamanın uygulama kimliği URI'si.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>3. adım: bir istemci uygulamasını yapılandırma ve hello hizmeti çalıştırma
Eylem hello tooDo listesi hizmeti görebilirsiniz önce Azure AD'den belirteçleri almak ve çağrıları toohello hizmeti hale tooconfigure hello tooDo listesi istemci gerekir.

1. Toohello dönün [Azure portal](https://portal.azure.com).

2. Azure AD kiracınızda yeni bir uygulama oluşturun ve seçin **yerel istemci uygulaması** hello elde edilen isteminde.
  * **Ad** uygulama toousers açıklar.
  * Girin `http://TodoListClient/` hello için **yeniden yönlendirme URI'si** değeri.

3. Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği tooyour uygulama atar. Bu değer gerekir hello sonraki adımlarda, böylece hello uygulama sayfadan kopyalayın.

4. Merhaba gelen **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**. Bulun ve hello tooDo listesi hizmeti seçin, hello eklemeniz **erişim TodoListService** altında izni **izinlere temsilci**ve ardından **Bitti**.

5. Visual Studio'da açın `App.config` TodoListClient proje hello ve yapılandırma değerleriniz hello enter `<appSettings>` bölümü.

  * `ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com Hello adıdır.
  * `ida:ClientId`Azure portal hello kopyalanan hello uygulama kimliği değil.
  * `todo:TodoListResourceId`Merhaba hello tooDo hello Azure portal girdiğiniz listesi hizmet uygulaması, uygulama kimliği URI'si değil.

## <a name="next-steps"></a>Sonraki adımlar
Son olarak, temiz, yapı ve her proje çalıştırın. Henüz yapmadıysanız, başlangıç saati toocreate yeni bir kullanıcı ile kiracınızda sunulmuştur bir *. onmicrosoft.com etki alanı. Oturum açma kullanıcı toohello tooDo listesi istemci ve bazı görevler toohello kullanıcının yapılacaklar listesi ekleyin.

Başvuru için (yapılandırma değerleriniz olmadan) tamamlandı hello örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Şimdi toomore kimlik senaryoları taşıyabilirsiniz.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
