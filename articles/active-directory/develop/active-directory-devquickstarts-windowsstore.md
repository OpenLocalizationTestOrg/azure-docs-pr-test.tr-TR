---
title: "aaaAzure AD Windows Mağazası'ı kullanmaya başlama | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleştirme, Azure AD çağıran derleme Windows mağazası uygulamaları API'leri OAuth kullanan korumalı."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="1d4e1-103">Azure AD Windows mağazası uygulamaları ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1d4e1-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="1d4e1-104">Windows mağazası 8.1 ve önceki sürümü projeleri Visual Studio 2017 desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="1d4e1-105">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="1d4e1-106">Merhaba Windows mağazası için uygulama geliştiriyorsanız, Azure Active Directory (Azure AD), basit ve kolay tooauthenticate kolaylaştırır, Active Directory hesaplarını Kullanıcılarınızla.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="1d4e1-107">Bir uygulama, Azure AD ile tümleştirerek, güvenli bir şekilde tüm web hello Office 365 API'leri veya hello Azure API gibi Azure AD tarafından korunan API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="1d4e1-108">Korumalı tooaccess kaynakları gereken Windows mağazası Masaüstü uygulamaları için Azure AD hello Active Directory Authentication Library (ADAL) sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="1d4e1-109">Merhaba tek amacı, ADAL olan toomake hello uygulama tooget erişim belirteçleri için kolay.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="1d4e1-110">toodemonstrate olduğu, bu makalede gösterilmektedir nasıl toobuild bir DirectorySearcher Windows mağazası ne kadar kolay uygulama:</span><span class="sxs-lookup"><span data-stu-id="1d4e1-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="1d4e1-111">Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="1d4e1-112">Sağlanan kullanıcı asıl adı (UPN) sahip kullanıcılar için bir dizin arar.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="1d4e1-113">İşaretlerini kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="1d4e1-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1d4e1-114">Before you get started</span></span>
* <span data-ttu-id="1d4e1-115">Merhaba karşıdan [çatı projesini](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), veya hello indirme [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="1d4e1-116">Her yükleme Visual Studio 2015 çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="1d4e1-117">Ayrıca hangi toocreate kullanıcıları ve kayıt hello uygulama Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="1d4e1-118">Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="1d4e1-119">Hazır olduğunuzda izleyin hello yordamlarda sonraki üç bölümde hello.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="1d4e1-120">1. adım: Kayıt hello DirectorySearcher uygulama</span><span class="sxs-lookup"><span data-stu-id="1d4e1-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="1d4e1-121">tooenable hello uygulama tooget belirteçleri, ilk ihtiyacınız tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="1d4e1-122">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="1d4e1-122">Here's how:</span></span>

1. <span data-ttu-id="1d4e1-123">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1d4e1-124">Merhaba üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-124">On hello top bar, click your account.</span></span> <span data-ttu-id="1d4e1-125">Ardından, hello altında **dizin** listesi, tooregister hello uygulama istediğiniz select hello Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="1d4e1-126">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="1d4e1-127">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="1d4e1-128">Merhaba istemleri toocreate izleyin bir **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="1d4e1-129">**Ad** hello uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="1d4e1-130">**Yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanan bir şema ve dize birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="1d4e1-131">Şu an için bir yer tutucu değerini girin (örneğin, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="1d4e1-132">Merhaba değer daha sonra değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="1d4e1-133">Merhaba kaydı tamamladıktan sonra Azure AD hello uygulama benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="1d4e1-134">Merhaba Hello değerini kopyalayın **uygulama** sekmesinde, çünkü daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="1d4e1-135">Merhaba üzerinde **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="1d4e1-136">Hello için **Azure Active Directory** uygulama, select **Microsoft Graph** API hello gibi.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="1d4e1-137">Altında **izinlere temsilci**, hello eklemek **erişim hello dizini hello oturum açmış kullanıcı olarak** izni.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="1d4e1-138">Bunun yapılması, kullanıcılar için hello uygulama tooquery hello grafik API'si sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="1d4e1-139">2. adım: Yükleme ve ADAL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1d4e1-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="1d4e1-140">Azure AD'de bir uygulamaya sahip olduğunuza göre ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="1d4e1-141">Azure AD ile tooenable ADAL toocommunicate hello uygulama kaydı hakkında bazı bilgiler verir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="1d4e1-142">Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="1d4e1-143">Merhaba DirectorySearcher projesinde MainPage.xaml.cs açın.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="1d4e1-144">Hello başlangıç değerleri değiştirin **yapılandırma değerleri** bölge hello Azure portal girdiğiniz hello değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="1d4e1-145">ADAL kullandığında kodunuzu toothese değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="1d4e1-146">Merhaba *Kiracı* Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) hello etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="1d4e1-147">Merhaba *ClientID* hello portalından kopyalandığından hello uygulama hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="1d4e1-148">Artık Windows mağazası uygulamanız için toodiscover hello geri çağırma URI gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="1d4e1-149">Merhaba bu satırında bir kesme noktası belirleyerek `MainPage` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1d4e1-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="1d4e1-150">Tüm başvuruları paket emin yapı hello çözüm geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="1d4e1-151">Herhangi bir paket eksikse hello NuGet Paket Yöneticisi'ni açın ve bunları geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="1d4e1-152">Merhaba uygulamayı çalıştırın ve kopyalama hello değerini `redirectUri` zaman hello kesme noktası isabet.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="1d4e1-153">Merhaba değeri hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="1d4e1-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="1d4e1-154">Merhaba üzerinde geri **ayarları** hello Azure portal hello uygulamada sekme ekleme bir **RedirectUri** değeri önceki hello ile.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="1d4e1-155">3. adım: Azure AD ADAL tooget belirteçlerinden kullanın</span><span class="sxs-lookup"><span data-stu-id="1d4e1-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="1d4e1-156">Merhaba temel ADAL arkasında hello uygulamanın bir erişim belirteci ihtiyacı olduğunda, onu yalnızca çağırdığı ilkesidir `authContext.AcquireToken(…)`, ve ADAL rest hello.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="1d4e1-157">Merhaba uygulamanın başlatma `AuthenticationContext`, ADAL birincil sınıfının hello olduğu.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="1d4e1-158">Bu eylem Azure AD ile toocommunicate gerekir ve nasıl söyleyin ADAL hello koordinatları geçirir toocache belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="1d4e1-159">Merhaba bulun `Search(...)` hello kullanıcılar'ı tıklattığınızda, çağrılan yöntemi **arama** hello uygulamanın UI düğmesinde.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="1d4e1-160">Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir get isteği toohello Azure AD Graph API tooquery sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="1d4e1-161">tooquery hello grafik API'si içeren bir erişim belirteci hello isteğin içinde **yetkilendirme** üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="1d4e1-162">ADAL nereden geldiğini budur.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="1d4e1-163">Merhaba uygulama isteğinde bulunduğunda bir belirteç çağırarak `AcquireTokenAsync(...)`, ADAL tooreturn bir belirteç hello kullanıcı kimlik bilgilerinin sorulmasına olmadan çalışır.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="1d4e1-164">ADAL tooget bir belirteç toosign hello kullanıcı gerektiğini belirlerse, bir oturum açma iletişim kutusu görüntüler, hello kullanıcının kimlik bilgilerini toplar ve kimlik doğrulaması başarılı olduktan sonra bir belirteç döndürür.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="1d4e1-165">ADAL herhangi bir nedenle yüklenemiyor tooreturn bir belirteç ise, hello *yazılımdan AuthenticationResult* bir hata durumudur.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="1d4e1-166">Bu zaman toouse hello erişim belirteci almış sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="1d4e1-167">Merhaba, ayrıca `Search(...)` yöntemi, grafik API'si get isteği hello hello belirteci toohello ekleme **yetkilendirme** üstbilgisi:</span><span class="sxs-lookup"><span data-stu-id="1d4e1-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="1d4e1-168">Merhaba kullanabilirsiniz `AuthenticationResult` nesne hello kullanıcının kimliği gibi hello uygulama hello kullanıcı hakkında toodisplay bilgi:</span><span class="sxs-lookup"><span data-stu-id="1d4e1-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="1d4e1-169">ADAL toosign kullanıcılar hello uygulama dışında de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="1d4e1-170">Merhaba kullanıcı hello tıkladığında **oturum kapatma** düğmesini tıklatın, bu hello sonraki çağrı çok olun`AcquireTokenAsync(...)` bir oturum açma görünümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="1d4e1-171">ADAL ile bu eylemin hello belirteç önbelleği temizleme olarak kadar kolaydır:</span><span class="sxs-lookup"><span data-stu-id="1d4e1-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="1d4e1-172">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="1d4e1-172">What's next</span></span>
<span data-ttu-id="1d4e1-173">Artık çalışan bir kullanıcıların kimlik doğrulaması, güvenli bir şekilde web OAuth 2.0 kullanan API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri elde Windows mağazası uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="1d4e1-174">Kiracı kullanıcılarla zaten doldurulmuş yapmadıysanız, başlangıç saati toodo şekilde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="1d4e1-175">DirectorySearcher uygulamanızı çalıştırın ve ardından hello kullanıcılardan birine oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="1d4e1-176">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="1d4e1-177">Merhaba uygulamasını kapatın ve onu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="1d4e1-178">Merhaba kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="1d4e1-179">Toodisplay hello alt çubuğu sağ tıklayarak oturumu kapatın ve ardından başka bir kullanıcı olarak yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="1d4e1-180">ADAL kolay tooincorporate kılar tüm bu ortak kimlik özellikler hello uygulamada.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="1d4e1-181">Bunu tüm hello dirty çalışmanın sizin için önbellek yönetimi gibi OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, hello kullanıcı sunan mvc'deki ve yenileme belirteçleri süresi.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="1d4e1-182">Tooknow yalnızca tek bir API çağrısı gereksinim `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="1d4e1-183">Merhaba başvuru için karşıdan [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (yapılandırma değerleriniz olmadan).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="1d4e1-184">Şimdi tooadditional kimlik senaryoları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4e1-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="1d4e1-185">Örneğin, [Azure AD ile .NET Web API'si güvenli](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1d4e1-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
