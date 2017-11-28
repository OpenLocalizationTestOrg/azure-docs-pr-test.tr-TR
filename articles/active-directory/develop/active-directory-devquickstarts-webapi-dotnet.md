---
title: "Azure AD .NET web API'si Başlarken | Microsoft Docs"
description: ".NET MVC web kimlik doğrulama ve yetkilendirme için Azure AD ile tümleşir API'si oluşturma."
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
ms.openlocfilehash: f44d75f45073a5d9aa9b1863ed227aba4efcf785
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a><span data-ttu-id="ebcb3-103">Azure AD'den taşıyıcı belirteçlerini kullanarak bir web API korunmasına yardımcı olma</span><span class="sxs-lookup"><span data-stu-id="ebcb3-103">Help protect a web API by using bearer tokens from Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ebcb3-104">Korunan kaynaklara erişim sağlayan bir uygulama oluşturuyorsanız, bu kaynakları unwarranted erişimi engellemek nasıl bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-104">If you’re building an application that provides access to protected resources, you need to know how to prevent unwarranted access to those resources.</span></span>
<span data-ttu-id="ebcb3-105">Basit ve basit bir web API OAuth 2.0 taşıyıcı erişimi kullanarak korunmasına yardımcı olmak yalnızca birkaç kod satırıyla belirteçler azure Active Directory (Azure AD) yapar.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-105">Azure Active Directory (Azure AD) makes it simple and straightforward to help protect a web API by using OAuth 2.0 bearer access tokens with only a few lines of code.</span></span>

<span data-ttu-id="ebcb3-106">ASP.NET web uygulamalarında .NET Framework 4. 5 ' bulunan topluluk odaklı OWIN ara yazılımı Microsoft uyarlamasını kullanarak bu koruma gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-106">In ASP.NET web apps, you can accomplish this protection by using the Microsoft implementation of the community-driven OWIN middleware included in .NET Framework 4.5.</span></span> <span data-ttu-id="ebcb3-107">OWIN için burada kullanacağız bir "Yapılacaklar listesi" web API'si oluşturma:</span><span class="sxs-lookup"><span data-stu-id="ebcb3-107">Here we’ll use OWIN to build a "To Do List" web API that:</span></span>

* <span data-ttu-id="ebcb3-108">API olan atayan korumalı.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-108">Designates which APIs are protected.</span></span>
* <span data-ttu-id="ebcb3-109">Web API çağrıları geçerli erişim belirteci içeren doğrular.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-109">Validates that the web API calls contain a valid access token.</span></span>

<span data-ttu-id="ebcb3-110">Yapmak listesi API'sine oluşturmak için önce gerekir:</span><span class="sxs-lookup"><span data-stu-id="ebcb3-110">To build the To Do List API, you first need to:</span></span>

1. <span data-ttu-id="ebcb3-111">Bir uygulamayı Azure AD'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-111">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="ebcb3-112">OWIN kimlik doğrulaması ardışık kullanmak için uygulama ayarlama.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-112">Set up the app to use the OWIN authentication pipeline.</span></span>
3. <span data-ttu-id="ebcb3-113">Web API'sini çağırmak için bir istemci uygulaması yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-113">Configure a client application to call the web API.</span></span>

<span data-ttu-id="ebcb3-114">Başlamak için [uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) veya [tamamlanan örnek indirme](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ebcb3-114">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ebcb3-115">Her bir Visual Studio 2013 çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-115">Each is a Visual Studio 2013 solution.</span></span> <span data-ttu-id="ebcb3-116">Ayrıca, uygulamanızın kaydedileceği Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-116">You also need an Azure AD tenant in which to register your application.</span></span> <span data-ttu-id="ebcb3-117">Zaten yoksa, [edinebileceğinizi öğrenin](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ebcb3-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="ebcb3-118">1. adım: bir uygulamayı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-118">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="ebcb3-119">Güvenliğini sağlamaya yardımcı olmak için uygulamanızın, önce kiracınızda bir uygulama oluşturun ve birkaç temel bilgiler ile Azure AD sağlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-119">To help secure your application, you first need to create an application in your tenant and provide Azure AD with a few key pieces of information.</span></span>

1. <span data-ttu-id="ebcb3-120">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ebcb3-121">Üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-121">On the top bar, click your account.</span></span> <span data-ttu-id="ebcb3-122">İçinde **Directory** listesinde, Azure AD Kiracı uygulamanızı kaydetmek istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-122">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>

3. <span data-ttu-id="ebcb3-123">Tıklatın **daha Hizmetleri** sol bölmesinde ve seçip **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-123">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="ebcb3-124">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-124">Click **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="ebcb3-125">Komut istemlerini izleyin ve yeni bir **Web uygulaması ve/veya Web API**.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-125">Follow the prompts and create a new **Web Application and/or Web API**.</span></span>
  * <span data-ttu-id="ebcb3-126">**Ad** kullanıcılar uygulamanıza açıklar.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-126">**Name** describes your application to users.</span></span> <span data-ttu-id="ebcb3-127">Girin **hizmet listelemek için**.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-127">Enter **To Do List Service**.</span></span>
  * <span data-ttu-id="ebcb3-128">**Yeniden yönlendirme URI'si** uygulamanızı istedi herhangi bir belirtece döndürmek için Azure AD kullanır ve dize şeması bir birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-128">**Redirect Uri** is a scheme and string combination that Azure AD uses to return any tokens that your app has requested.</span></span> <span data-ttu-id="ebcb3-129">Girin `https://localhost:44321/` bu değer için.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-129">Enter `https://localhost:44321/` for this value.</span></span>

6. <span data-ttu-id="ebcb3-130">Gelen **ayarları** -> **özellikleri** sayfasında uygulamanız için uygulama kimliği URI'si güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="ebcb3-131">Kiracı özgü bir tanımlayıcı girin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-131">Enter a tenant-specific identifier.</span></span> <span data-ttu-id="ebcb3-132">Örneğin, `https://contoso.onmicrosoft.com/TodoListService` girin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-132">For example, enter `https://contoso.onmicrosoft.com/TodoListService`.</span></span>

7. <span data-ttu-id="ebcb3-133">Yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-133">Save the configuration.</span></span> <span data-ttu-id="ebcb3-134">Ayrıca istemci uygulamanızın kısa bir süre sonra kaydetmeniz gerekir çünkü portal kapatmayın.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-134">Leave the portal open, because you'll also need to register your client application shortly.</span></span>

## <a name="step-2-set-up-the-app-to-use-the-owin-authentication-pipeline"></a><span data-ttu-id="ebcb3-135">2. adım: uygulama OWIN kimlik doğrulaması ardışık kullanmak için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-135">Step 2: Set up the app to use the OWIN authentication pipeline</span></span>
<span data-ttu-id="ebcb3-136">Gelen istekleri ve belirteçleri doğrulamak için uygulamanızı Azure AD ile iletişim kurmak için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-136">To validate incoming requests and tokens, you need to set up your application to communicate with Azure AD.</span></span>

1. <span data-ttu-id="ebcb3-137">Başlamak için çözümü açın ve OWIN ara yazılımı NuGet paketleri Paket Yöneticisi konsolu kullanılarak TodoListService projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-137">To begin, open the solution and add the OWIN middleware NuGet packages to the TodoListService project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. <span data-ttu-id="ebcb3-138">Adlı TodoListService projesine OWIN başlangıç sınıfı ekleyin `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-138">Add an OWIN Startup class to the TodoListService project called `Startup.cs`.</span></span>  <span data-ttu-id="ebcb3-139">Projeye sağ tıklayın, **Ekle** > **yeni öğe**, arayın ve sonra **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-139">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span> <span data-ttu-id="ebcb3-140">OWIN ara yazılımı, uygulamanız başlatıldığında `Configuration(…)` yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-140">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

3. <span data-ttu-id="ebcb3-141">Sınıf bildirimi değiştirme `public partial class Startup`.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-141">Change the class declaration to `public partial class Startup`.</span></span> <span data-ttu-id="ebcb3-142">Zaten bu sınıfın parçası sizin için başka bir dosyaya uyguladık.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-142">We’ve already implemented part of this class for you in another file.</span></span> <span data-ttu-id="ebcb3-143">İçinde `Configuration(…)` yöntemi çağrısına duruma `ConfgureAuth(…)` web uygulamanız için kimlik doğrulaması ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-143">In the `Configuration(…)` method, make a call to `ConfgureAuth(…)` to set up authentication for your web app.</span></span>

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. <span data-ttu-id="ebcb3-144">Dosyayı açmak `App_Start\Startup.Auth.cs` ve uygulamanıza `ConfigureAuth(…)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-144">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(…)` method.</span></span> <span data-ttu-id="ebcb3-145">Sağladığınız parametreler `WindowsAzureActiveDirectoryBearerAuthenticationOptions` uygulamanız için Azure AD ile iletişim kurmak için koordinatları olarak hizmet verecektir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-145">The parameters that you provide in `WindowsAzureActiveDirectoryBearerAuthenticationOptions` will serve as coordinates for your app to communicate with Azure AD.</span></span>

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

5. <span data-ttu-id="ebcb3-146">Kullanabileceğiniz artık `[Authorize]` denetleyicileri ve eylemleri JSON Web Token (JWT) taşıyıcı kimlik doğrulaması ile korumaya yardımcı olmak için öznitelikler.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-146">Now you can use `[Authorize]` attributes to help protect your controllers and actions with JSON Web Token (JWT) bearer authentication.</span></span> <span data-ttu-id="ebcb3-147">İşaretleme `Controllers\TodoListController.cs` bir authorize etiketiyle sınıfı.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-147">Decorate the `Controllers\TodoListController.cs` class with an authorize tag.</span></span> <span data-ttu-id="ebcb3-148">Bu sayfayı erişmeden önce oturum açmak için kullanıcının zorlar.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-148">This will force the user to sign in before accessing that page.</span></span>

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    <span data-ttu-id="ebcb3-149">Ne zaman bir yetkili çağıran başarıyla çağırır birini `TodoListController` API'leri, eylem çağıran hakkında bilgilere erişimi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-149">When an authorized caller successfully invokes one of the `TodoListController` APIs, the action might need access to information about the caller.</span></span> <span data-ttu-id="ebcb3-150">OWIN taşıyıcı belirteci içinde talep erişim sağlar `ClaimsPrincpal` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-150">OWIN provides access to the claims inside the bearer token via the `ClaimsPrincpal` object.</span></span>  

6. <span data-ttu-id="ebcb3-151">Web API’lerine yönelik genel bir gereksinim, belirteçteki mevcut "kapsamların" doğrulanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-151">A common requirement for web APIs is to validate the "scopes" present in the token.</span></span> <span data-ttu-id="ebcb3-152">Bu kullanıcı yapmak listesi hizmete erişmek için gerekli izinleri seçtiği sağlar.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-152">This ensures that the user has consented to the permissions required to access the To Do List Service.</span></span>

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is the default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "The Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. <span data-ttu-id="ebcb3-153">Açık `web.config` dosya TodoListService proje kök dizininde ve yapılandırma değerlerinizi girin `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-153">Open the `web.config` file in the root of the TodoListService project, and enter your configuration values in the `<appSettings>` section.</span></span>
  * <span data-ttu-id="ebcb3-154">`ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com adıdır.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-154">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="ebcb3-155">`ida:Audience`Azure portalında girdiğiniz uygulamanın uygulama kimliği URI'si değil.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-155">`ida:Audience` is the App ID URI of the application that you entered in the Azure portal.</span></span>

## <a name="step-3-configure-a-client-application-and-run-the-service"></a><span data-ttu-id="ebcb3-156">3. adım: bir istemci uygulamasını yapılandırma ve hizmet çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ebcb3-156">Step 3: Configure a client application and run the service</span></span>
<span data-ttu-id="ebcb3-157">İçin yapmak listesi hizmetinde eylem görebilmeniz için öncelikle Azure AD'den belirteçleri almak ve hizmet çağrı yapmak için yapılacaklar listesi istemci yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-157">Before you can see the To Do List Service in action, you need to configure the To Do List client so it can get tokens from Azure AD and make calls to the service.</span></span>

1. <span data-ttu-id="ebcb3-158">Geri dönerek [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ebcb3-158">Go back to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ebcb3-159">Azure AD kiracınızda yeni bir uygulama oluşturun ve seçin **yerel istemci uygulaması** elde edilen istemi.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-159">Create a new application in your Azure AD tenant, and select **Native Client Application** in the resulting prompt.</span></span>
  * <span data-ttu-id="ebcb3-160">**Ad** kullanıcılar uygulamanıza açıklar.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-160">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="ebcb3-161">Girin `http://TodoListClient/` için **yeniden yönlendirme URI'si** değeri.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-161">Enter `http://TodoListClient/` for the **Redirect Uri** value.</span></span>

3. <span data-ttu-id="ebcb3-162">Kayıt işlemini tamamladıktan sonra Azure AD benzersiz uygulama kimliği uygulamanıza atar.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-162">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="ebcb3-163">Bu değer gerekir sonraki adımlarda bu nedenle uygulama sayfasından kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-163">You’ll need this value in the next steps, so copy it from the application page.</span></span>

4. <span data-ttu-id="ebcb3-164">Gelen **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-164">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span> <span data-ttu-id="ebcb3-165">Bulun ve için yapmak listesi hizmeti seçin, eklemeniz **erişim TodoListService** altında izni **izinlere temsilci**ve ardından **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-165">Locate and select the To Do List Service, add the **Access TodoListService** permission under **Delegated Permissions**, and then click **Done**.</span></span>

5. <span data-ttu-id="ebcb3-166">Visual Studio'da açın `App.config` TodoListClient içinde proje ve yapılandırma değerleriniz enter `<appSettings>` bölümü.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-166">In Visual Studio, open `App.config` in the TodoListClient project, and then enter your configuration values in the `<appSettings>` section.</span></span>

  * <span data-ttu-id="ebcb3-167">`ida:Tenant`Azure AD kiracınıza--Örneğin, contoso.onmicrosoft.com adıdır.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-167">`ida:Tenant` is the name of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="ebcb3-168">`ida:ClientId`Azure portalından kopyalandığından uygulama kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-168">`ida:ClientId` is the app ID that you copied from the Azure portal.</span></span>
  * <span data-ttu-id="ebcb3-169">`todo:TodoListResourceId`Azure portalında girdiğiniz listesi hizmeti yapmak için uygulamanın uygulama kimliği URI'si değil.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-169">`todo:TodoListResourceId` is the App ID URI of the To Do List Service application that you entered in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebcb3-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ebcb3-170">Next steps</span></span>
<span data-ttu-id="ebcb3-171">Son olarak, temiz, yapı ve her proje çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-171">Finally, clean, build, and run each project.</span></span> <span data-ttu-id="ebcb3-172">Henüz yapmadıysanız, şimdi yeni bir kullanıcı ile kiracınızda oluşturma vakti bir *. onmicrosoft.com etki alanı.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-172">If you haven’t already, now is the time to create a new user in your tenant with a *.onmicrosoft.com domain.</span></span> <span data-ttu-id="ebcb3-173">Bu kullanıcının yapılacaklar listesi istemcisiyle oturum açın ve bazı görevler kullanıcının yapılacaklar listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-173">Sign in to the To Do List client with that user, and add some tasks to the user's to-do list.</span></span>

<span data-ttu-id="ebcb3-174">Başvuru için (yapılandırma değerleriniz olmadan) tamamlanan örnek kullanılabilir [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ebcb3-174">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ebcb3-175">Şimdi daha fazla kimlik senaryo da taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebcb3-175">You can now move on to more identity scenarios.</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
