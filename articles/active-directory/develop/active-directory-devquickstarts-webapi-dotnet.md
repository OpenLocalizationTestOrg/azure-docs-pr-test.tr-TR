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
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="72287-103">Azure AD'den taşıyıcı belirteçlerini kullanarak bir web API korunmasına yardımcı olma</span><span class="sxs-lookup"><span data-stu-id="72287-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="72287-104">Tooprotected kaynaklara erişim sağlayan bir uygulama oluşturuyorsanız tooknow gereksinim nasıl tooprevent unwarranted toothose kaynaklarına erişim.</span><span class="sxs-lookup"><span data-stu-id="72287-104">If you’re building an application that provides access tooprotected resources, you need tooknow how tooprevent unwarranted access toothose resources.</span></span>
<span data-ttu-id="72287-105">Azure Active Directory (Azure AD), kolaylaştırır ve basit toohelp yalnızca birkaç kod satırıyla, OAuth 2.0 taşıyıcı erişim belirteçleri kullanarak web API'si koruyun.</span><span class="sxs-lookup"><span data-stu-id="72287-105">Azure Active Directory (Azure AD) makes it simple and straightforward toohelp protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="72287-106">ASP.NET web uygulamalarında hello Microsoft .NET Framework 4. 5 ' dahil hello topluluk odaklı OWIN ara yazılımı uyarlamasını kullanarak bu koruma gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72287-106">In ASP.NET web apps, you can accomplish this protection by using hello Microsoft implementation of hello community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="72287-107">OWIN toobuild "tooDo listesi" web API'sini burada kullanacağız:</span><span class="sxs-lookup"><span data-stu-id="72287-107">Here we’ll use OWIN toobuild a "tooDo List" web API that:</span></span>

* <span data-ttu-id="72287-108">API olan atayan korumalı.</span><span class="sxs-lookup"><span data-stu-id="72287-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="72287-109">Merhaba web API çağrıları geçerli erişim belirteci içeren doğrular.</span><span class="sxs-lookup"><span data-stu-id="72287-109">Validates that hello web API calls contain a valid access token.</span></span>

<span data-ttu-id="72287-110">toobuild hello tooDo listesi API, önce yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="72287-110">toobuild hello tooDo List API, you first need to:</span></span>

1. <span data-ttu-id="72287-111">Bir uygulamayı Azure AD'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72287-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="72287-112">Merhaba uygulama toouse hello OWIN kimlik doğrulaması ardışık ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="72287-112">Set up hello app toouse hello OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="72287-113">İstemci uygulama toocall hello web API'si yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="72287-113">Configure a client application toocall hello web API.</span></span>

<span data-ttu-id="72287-114">başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="72287-114">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="72287-115">Her bir Visual Studio 2013 çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="72287-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="72287-116">Ayrıca, uygulamanızın hangi tooregister içinde Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="72287-116">You also need an Azure AD tenant in which tooregister your application.</span></span> <span data-ttu-id="72287-117">Zaten yoksa, [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="72287-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="72287-118">1. adım: bir uygulamayı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72287-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="72287-119">toohelp güvenli uygulamanız, ilk kiracınızda toocreate uygulamanın gereksinim ve birkaç temel bilgiler ile Azure AD sağlayın.</span><span class="sxs-lookup"><span data-stu-id="72287-119">toohelp secure your application, you first need toocreate an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="72287-120">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72287-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="72287-121">Merhaba üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="72287-121">On hello top bar, click your account.</span></span> <span data-ttu-id="72287-122">Merhaba, **Directory** listesinde, uygulamanızın hello Azure AD Kiracı tooregister istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="72287-122">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>

3. <span data-ttu-id="72287-123">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="72287-123">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="72287-124">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="72287-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="72287-125">Merhaba komut istemlerini izleyin ve yeni bir **Web uygulaması ve/veya Web API**.</span><span class="sxs-lookup"><span data-stu-id="72287-125">Follow hello prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="72287-126">**Ad** uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="72287-126">**Name** describes your application toousers.</span></span> <span data-ttu-id="72287-127">Girin **tooDo listesi hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="72287-127">Enter **tooDo List Service**.</span></span>
  * <span data-ttu-id="72287-128">**Yeniden yönlendirme URI'si** herhangi belirteçler uygulamanızı istedi tooreturn Azure AD kullanır ve dize şeması bir birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="72287-128">**Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn any tokens that your app has requested.</span></span> <span data-ttu-id="72287-129">Girin `https://localhost:44321/` bu değer için.</span><span class="sxs-lookup"><span data-stu-id="72287-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="72287-130">Merhaba gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si hello güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="72287-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="72287-131">Kiracı özgü bir tanımlayıcı girin.</span><span class="sxs-lookup"><span data-stu-id="72287-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="72287-132">Örneğin, `https://contoso.onmicrosoft.com/TodoListService` girin.</span><span class="sxs-lookup"><span data-stu-id="72287-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="72287-133">Merhaba yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72287-133">Save hello configuration.</span></span> <span data-ttu-id="72287-134">Ayrıca tooregister istemci uygulamanızın kısa bir süre içinde gerekir çünkü hello portal kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="72287-134">Leave hello portal open, because you'll also need tooregister your client application shortly.</span></span>

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a><span data-ttu-id="72287-135">2. adım: hello uygulama toouse hello OWIN kimlik doğrulaması ardışık ayarlayın</span><span class="sxs-lookup"><span data-stu-id="72287-135">Step 2: Set up hello app toouse hello OWIN authentication pipeline</span></span>
<span data-ttu-id="72287-136">toovalidate gelen istekleri ve belirteçler, Azure AD ile uygulama toocommunicate yukarı tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="72287-136">toovalidate incoming requests and tokens, you need tooset up your application toocommunicate with Azure AD.</span></span>

1. <span data-ttu-id="72287-137">toobegin, hello çözüm açın ve hello Paket Yöneticisi konsolu kullanarak hello OWIN ara yazılımı NuGet paketleri toohello TodoListService projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72287-137">toobegin, open hello solution and add hello OWIN middleware NuGet packages toohello TodoListService project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="72287-138">Adlı bir OWIN başlangıç sınıfı toohello TodoListService projesi eklemek `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="72287-138">Add an OWIN Startup class toohello TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="72287-139">Sağ hello proje, select **Ekle** > **yeni öğe**, arayın ve sonra **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="72287-139">Right-click hello project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="72287-140">Merhaba OWIN ara yazılımı hello çağırılır `Configuration(…)` uygulamanız başladığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="72287-140">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="72287-141">Merhaba sınıf bildirimi çok değiştirmek`public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="72287-141">Change hello class declaration too`public partial class Startup`.</span></span> <span data-ttu-id="72287-142">Zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="72287-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="72287-143">Merhaba, `Configuration(…)` yöntemi, çok çağırmaya`ConfgureAuth(…)` tooset web uygulamanız için kimlik doğrulaması ayarlama.</span><span class="sxs-lookup"><span data-stu-id="72287-143">In hello `Configuration(…)` method, make a call too`ConfgureAuth(…)` tooset up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="72287-144">Açık hello dosya `App_Start\Startup.Auth.cs` ve hello uygulamak `ConfigureAuth(…)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="72287-144">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="72287-145">Merhaba sağladığınız parametreler `WindowsAzureActiveDirectoryBearerAuthenticationOptions` , uygulama toocommunicate Azure AD ile koordinatları olarak hizmet verecektir.</span><span class="sxs-lookup"><span data-stu-id="72287-145">hello parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app toocommunicate with Azure AD.</span></span>

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

5. <span data-ttu-id="72287-146">Kullanabileceğiniz artık `[Authorize]` öznitelikleri toohelp denetleyicileri ve eylemleri JSON Web Token (JWT) taşıyıcı kimlik doğrulaması ile koruyun.</span><span class="sxs-lookup"><span data-stu-id="72287-146">Now you can use `[Authorize]` attributes toohelp protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="72287-147">Merhaba tasarlamanız `Controllers\TodoListController.cs` bir authorize etiketiyle sınıfı.</span><span class="sxs-lookup"><span data-stu-id="72287-147">Decorate hello `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="72287-148">Bu sayfaya erişmeden önce bu hello kullanıcı toosign zorlar.</span><span class="sxs-lookup"><span data-stu-id="72287-148">This will force hello user toosign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="72287-149">Ne zaman bir yetkili çağıran başarıyla çağırır hello birini `TodoListController` API'leri, hello eylem erişim tooinformation hello çağıran hakkında.</span><span class="sxs-lookup"><span data-stu-id="72287-149">When an authorized caller successfully invokes one of hello `TodoListController` APIs, hello action might need access tooinformation about hello caller.</span></span> <span data-ttu-id="72287-150">OWIN sağlar erişim toohello talep hello taşıyıcı belirteci hello aracılığıyla içinde `ClaimsPrincpal` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="72287-150">OWIN provides access toohello claims inside hello bearer token via hello `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="72287-151">Web API'leri için ortak bir gereksinim toovalidate hello "kapsamlar" Merhaba belirtecinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="72287-151">A common requirement for web APIs is toovalidate hello "scopes" present in hello token.</span></span> <span data-ttu-id="72287-152">Bu, o hello kullanıcı toohello izinleri gerekli tooaccess hello tooDo listesi hizmet verdiği sağlar.</span><span class="sxs-lookup"><span data-stu-id="72287-152">This ensures that hello user has consented toohello permissions required tooaccess hello tooDo List Service.</span></span>

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

7. <span data-ttu-id="72287-153">Açık hello `web.config` hello TodoListService proje hello kökünde bulunan dosya ve hello yapılandırma değerlerini girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="72287-153">Open hello `web.config` file in hello root of hello TodoListService project, and enter your configuration values in hello `<appSettings>` section.</span></span>
  * <span data-ttu-id="72287-154">`ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="72287-154">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="72287-155">`ida:Audience`olan hello hello Azure portal girdiğiniz hello uygulamanın uygulama kimliği URI'si.</span><span class="sxs-lookup"><span data-stu-id="72287-155">`ida:Audience` is hello App ID URI of hello application that you entered in hello Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a><span data-ttu-id="72287-156">3. adım: bir istemci uygulamasını yapılandırma ve hello hizmeti çalıştırma</span><span class="sxs-lookup"><span data-stu-id="72287-156">Step 3: Configure a client application and run hello service</span></span>
<span data-ttu-id="72287-157">Eylem hello tooDo listesi hizmeti görebilirsiniz önce Azure AD'den belirteçleri almak ve çağrıları toohello hizmeti hale tooconfigure hello tooDo listesi istemci gerekir.</span><span class="sxs-lookup"><span data-stu-id="72287-157">Before you can see hello tooDo List Service in action, you need tooconfigure hello tooDo List client so it can get tokens from Azure AD and make calls toohello service.</span></span>

1. <span data-ttu-id="72287-158">Toohello dönün [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72287-158">Go back toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="72287-159">Azure AD kiracınızda yeni bir uygulama oluşturun ve seçin **yerel istemci uygulaması** hello elde edilen isteminde.</span><span class="sxs-lookup"><span data-stu-id="72287-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in hello resulting prompt.</span></span>
  * <span data-ttu-id="72287-160">**Ad** uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="72287-160">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="72287-161">Girin `http://TodoListClient/` hello için **yeniden yönlendirme URI'si** değeri.</span><span class="sxs-lookup"><span data-stu-id="72287-161">Enter `http://TodoListClient/` for hello **Redirect Uri** value.</span></span>

3. <span data-ttu-id="72287-162">Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği tooyour uygulama atar.</span><span class="sxs-lookup"><span data-stu-id="72287-162">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="72287-163">Bu değer gerekir hello sonraki adımlarda, böylece hello uygulama sayfadan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="72287-163">You’ll need this value in hello next steps, so copy it from hello application page.</span></span>

4. <span data-ttu-id="72287-164">Merhaba gelen **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="72287-164">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="72287-165">Bulun ve hello tooDo listesi hizmeti seçin, hello eklemeniz **erişim TodoListService** altında izni **izinlere temsilci**ve ardından **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="72287-165">Locate and select hello tooDo List Service, add hello **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="72287-166">Visual Studio'da açın `App.config` TodoListClient proje hello ve yapılandırma değerleriniz hello enter `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="72287-166">In Visual Studio, open `App.config` in hello TodoListClient project, and then enter your configuration values in hello `<appSettings>` section.</span></span>

  * <span data-ttu-id="72287-167">`ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com Hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="72287-167">`ida:Tenant` is hello name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="72287-168">`ida:ClientId`Azure portal hello kopyalanan hello uygulama kimliği değil.</span><span class="sxs-lookup"><span data-stu-id="72287-168">`ida:ClientId` is hello app ID that you copied from hello Azure portal.</span></span>
  * <span data-ttu-id="72287-169">`todo:TodoListResourceId`Merhaba hello tooDo hello Azure portal girdiğiniz listesi hizmet uygulaması, uygulama kimliği URI'si değil.</span><span class="sxs-lookup"><span data-stu-id="72287-169">`todo:TodoListResourceId` is hello App ID URI of hello tooDo List Service application that you entered in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72287-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72287-170">Next steps</span></span>
<span data-ttu-id="72287-171">Son olarak, temiz, yapı ve her proje çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72287-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="72287-172">Henüz yapmadıysanız, başlangıç saati toocreate yeni bir kullanıcı ile kiracınızda sunulmuştur bir *. onmicrosoft.com etki alanı.</span><span class="sxs-lookup"><span data-stu-id="72287-172">If you haven’t already, now is hello time toocreate a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="72287-173">Oturum açma kullanıcı toohello tooDo listesi istemci ve bazı görevler toohello kullanıcının yapılacaklar listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72287-173">Sign in toohello tooDo List client with that user, and add some tasks toohello user's to-do list.</span></span>

<span data-ttu-id="72287-174">Başvuru için (yapılandırma değerleriniz olmadan) tamamlandı hello örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="72287-174">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="72287-175">Şimdi toomore kimlik senaryoları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72287-175">You can now move on toomore identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
