---
title: "aaaAzure AD Başlarken Xamarin | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleştirilebilen ve OAuth kullanan Azure AD korumalı API'leri çağırmak Xamarin uygulamaları oluşturun."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="143c0-103">Azure AD Xamarin uygulamaları ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="143c0-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="143c0-104">Xamarin ile C# ' ta, iOS, Android ve Windows (mobil cihazları ve bilgisayarları) üzerinde çalışan mobil uygulamalar yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="143c0-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="143c0-105">Azure Active Directory (Azure AD) Xamarin kullanarak bir uygulama oluşturuyorsanız, Azure AD hesaplarına sahip basit tooauthenticate kullanıcılar kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="143c0-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="143c0-106">Merhaba uygulama de güvenli bir şekilde hello Office 365 API'leri veya hello Azure API gibi Azure AD tarafından korunan tüm web API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="143c0-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="143c0-107">Korumalı tooaccess kaynaklara gereksinim Xamarin uygulamaları için Azure AD hello Active Directory Authentication Library (ADAL) sağlar.</span><span class="sxs-lookup"><span data-stu-id="143c0-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="143c0-108">ADAL tek amacı Hello toomake bu uygulamaları tooget erişim belirteçleri için kolay.</span><span class="sxs-lookup"><span data-stu-id="143c0-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="143c0-109">toodemonstrate olduğu, bu makalede gösterilmektedir ne kadar kolay nasıl toobuild DirectorySearcher uygulamalar:</span><span class="sxs-lookup"><span data-stu-id="143c0-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="143c0-110">İOS, Android, Windows Masaüstü, Windows Phone ve Windows Mağazası'nı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="143c0-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="143c0-111">Tek taşınabilir sınıf kitaplığı (PCL) tooauthenticate kullanıcıları ve belirteçleri hello Azure AD Graph API alın.</span><span class="sxs-lookup"><span data-stu-id="143c0-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="143c0-112">Verilen UPN olan kullanıcılar için bir dizini arayın.</span><span class="sxs-lookup"><span data-stu-id="143c0-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="143c0-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="143c0-113">Before you get started</span></span>
* <span data-ttu-id="143c0-114">Merhaba karşıdan [çatı projesini](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), veya hello indirme [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="143c0-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="143c0-115">Her yükleme Visual Studio 2013 çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="143c0-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="143c0-116">Ayrıca hangi toocreate kullanıcıları ve kayıt hello uygulama Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="143c0-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="143c0-117">Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="143c0-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="143c0-118">Hazır olduğunuzda İleri dört bölüm izleyin hello yordamlarda hello.</span><span class="sxs-lookup"><span data-stu-id="143c0-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="143c0-119">1. adım: Xamarin geliştirme ortamınızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="143c0-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="143c0-120">Bu öğretici iOS, Android ve Windows için projeleri içerdiğinden, Visual Studio ve Xamarin gerekir.</span><span class="sxs-lookup"><span data-stu-id="143c0-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="143c0-121">toocreate hello gerekli ortam, tam hello işleminde [ayarlamak ayarlama ve Visual Studio ve Xamarin yükleme](https://msdn.microsoft.com/library/mt613162.aspx) MSDN'de.</span><span class="sxs-lookup"><span data-stu-id="143c0-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="143c0-122">Tamamlanan hello yüklemeleri toobe için beklerken toolearn Xamarin hakkında daha fazla gözden geçirebilirsiniz malzemesi Hello yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="143c0-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="143c0-123">Merhaba kurulumu tamamladıktan sonra hello çözümü Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="143c0-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="143c0-124">Burada, altı projeleri bulacaksınız: beş platforma özel Proje ve bir PCL, tüm platformlarda paylaşılan DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="143c0-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="143c0-125">2. adım: Kayıt hello DirectorySearcher uygulama</span><span class="sxs-lookup"><span data-stu-id="143c0-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="143c0-126">tooenable hello uygulama tooget belirteçleri, ilk ihtiyacınız tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin.</span><span class="sxs-lookup"><span data-stu-id="143c0-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="143c0-127">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="143c0-127">Here's how:</span></span>

1. <span data-ttu-id="143c0-128">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="143c0-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="143c0-129">Merhaba üst çubuğunda hesabınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="143c0-129">On hello top bar, click your account.</span></span> <span data-ttu-id="143c0-130">Ardından, hello altında **dizin** listesi, tooregister hello uygulama istediğiniz select hello Active Directory kiracısı.</span><span class="sxs-lookup"><span data-stu-id="143c0-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="143c0-131">Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="143c0-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="143c0-132">Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="143c0-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="143c0-133">Yeni bir toocreate **yerel istemci uygulaması**, hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="143c0-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="143c0-134">**Ad** hello uygulama toousers açıklar.</span><span class="sxs-lookup"><span data-stu-id="143c0-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="143c0-135">**Yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanan bir şema ve dize birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="143c0-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="143c0-136">Bir değer (örneğin, http://DirectorySearcher) girin.</span><span class="sxs-lookup"><span data-stu-id="143c0-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="143c0-137">Kayıt tamamladıktan sonra Azure AD hello uygulama benzersiz uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="143c0-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="143c0-138">Hello Hello değerini kopyalayın **uygulama** sekmesinde, çünkü daha sonra ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="143c0-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="143c0-139">Merhaba üzerinde **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="143c0-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="143c0-140">Seçin **Microsoft Graph** API hello gibi.</span><span class="sxs-lookup"><span data-stu-id="143c0-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="143c0-141">Altında **izinlere temsilci**, hello eklemek **dizin verilerini okuma** izni.</span><span class="sxs-lookup"><span data-stu-id="143c0-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="143c0-142">Bu eylem, kullanıcılar için hello uygulama tooquery hello grafik API'si sağlar.</span><span class="sxs-lookup"><span data-stu-id="143c0-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="143c0-143">3. adım: Yükleme ve ADAL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="143c0-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="143c0-144">Azure AD'de bir uygulamaya sahip olduğunuza göre ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="143c0-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="143c0-145">Azure AD ile tooenable ADAL toocommunicate hello uygulama kaydı hakkında bazı bilgiler verir.</span><span class="sxs-lookup"><span data-stu-id="143c0-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="143c0-146">Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="143c0-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="143c0-147">İki kitaplığı başvuru tooeach proje eklenen Not: hello PCL kısmı ADAL ve platforma özgü bölümü.</span><span class="sxs-lookup"><span data-stu-id="143c0-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="143c0-148">Merhaba DirectorySearcherLib projesinde DirectorySearcher.cs açın.</span><span class="sxs-lookup"><span data-stu-id="143c0-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="143c0-149">Merhaba sınıf üye değerlerinin hello Azure portal girdiğiniz hello değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="143c0-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="143c0-150">ADAL kullandığında kodunuzu toothese değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="143c0-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="143c0-151">Merhaba *Kiracı* Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) hello etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="143c0-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="143c0-152">Merhaba *ClientID* hello portalından kopyalandığından hello uygulama hello istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="143c0-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="143c0-153">Merhaba *returnUri* hello yeniden yönlendirme (örneğin, http://DirectorySearcher) hello portalda girdiğiniz URI'si değil.</span><span class="sxs-lookup"><span data-stu-id="143c0-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="143c0-154">4. adım: Azure AD ADAL tooget belirteçlerinden kullanın</span><span class="sxs-lookup"><span data-stu-id="143c0-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="143c0-155">Neredeyse tüm hello uygulamanın kimlik doğrulaması mantığı arasındadır `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="143c0-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="143c0-156">Merhaba platforma özgü projelerinde gerekli olan tek şey toopass bağlamsal parametresi toohello `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="143c0-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="143c0-157">DirectorySearcher.cs açın ve ardından yeni bir parametre toohello ekleyin `SearchByAlias(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="143c0-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="143c0-158">`IPlatformParameters`ADAL gereksinimlerini tooperform hello kimlik doğrulamanın hello platforma özgü yalıtan hello bağlamsal parametre nesneleri olur.</span><span class="sxs-lookup"><span data-stu-id="143c0-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="143c0-159">Initialize `AuthenticationContext`, ADAL birincil sınıfının hello olduğu.</span><span class="sxs-lookup"><span data-stu-id="143c0-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="143c0-160">Bu eylem geçiş ADAL hello Azure AD ile gereksinimlerini toocommunicate düzenler.</span><span class="sxs-lookup"><span data-stu-id="143c0-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="143c0-161">Çağrı `AcquireTokenAsync(...)`, hello kabul `IPlatformParameters` nesne ve gerekli tooreturn bir belirteç toohello uygulaması olan hello kimlik doğrulaması akışı çağırır.</span><span class="sxs-lookup"><span data-stu-id="143c0-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="143c0-162">`AcquireTokenAsync(...)`ilk deneme tooreturn hello için bir belirteç (aracılığıyla, önbelleğe alma veya eski belirteçleri yenileme) kimlik bilgilerini kullanıcılar tooenter sormadan istenen kaynak (Merhaba grafik API'si bu durumda).</span><span class="sxs-lookup"><span data-stu-id="143c0-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="143c0-163">Gerekirse, bu kullanıcıların hello Azure AD oturum açma sayfası hello istenen belirtecini alma önce gösterir.</span><span class="sxs-lookup"><span data-stu-id="143c0-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="143c0-164">Merhaba erişim belirteci toohello grafik API'si hello istekte attach **yetkilendirme** üstbilgisi:</span><span class="sxs-lookup"><span data-stu-id="143c0-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="143c0-165">Tüm olan hello için `DirectorySearcher` PCL ve hello uygulamanın kimlikle ilgili kod.</span><span class="sxs-lookup"><span data-stu-id="143c0-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="143c0-166">Kalan tek şey toocall hello `SearchByAlias(...)` yöntemi her platformun görünümlerinde ve gerektiğinde, doğru bir şekilde işlemek için tooadd kodu hello UI yaşam döngüsü.</span><span class="sxs-lookup"><span data-stu-id="143c0-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="143c0-167">Android</span><span class="sxs-lookup"><span data-stu-id="143c0-167">Android</span></span>
1. <span data-ttu-id="143c0-168">MainActivity.cs içinde çok bir çağrı ekleyin`SearchByAlias(...)` işleyici hello düğmesini tıklatın:</span><span class="sxs-lookup"><span data-stu-id="143c0-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="143c0-169">Merhaba geçersiz kılma `OnActivityResult` yaşam döngüsü yöntemi tooforward geri toohello uygun yöntemi herhangi bir kimlik doğrulaması yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="143c0-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="143c0-170">ADAL yardımcı yöntem bu Android sağlar:</span><span class="sxs-lookup"><span data-stu-id="143c0-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="143c0-171">Windows Masaüstü</span><span class="sxs-lookup"><span data-stu-id="143c0-171">Windows Desktop</span></span>
<span data-ttu-id="143c0-172">MainWindow.xaml.cs içinde çok çağırmaya`SearchByAlias(...)` geçirerek bir `WindowInteropHelper` hello masaüstünün içinde `PlatformParameters` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="143c0-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="143c0-173">iOS</span><span class="sxs-lookup"><span data-stu-id="143c0-173">iOS</span></span>
<span data-ttu-id="143c0-174">İOS DirSearchClient_iOSViewController.cs içinde hello `PlatformParameters` nesne başvurusu toohello View Controller alır:</span><span class="sxs-lookup"><span data-stu-id="143c0-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="143c0-175">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="143c0-175">Windows Universal</span></span>
<span data-ttu-id="143c0-176">Windows Evrensel MainPage.xaml.cs açın ve ardından hello uygulamak `Search` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="143c0-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="143c0-177">Bu yöntem gerektiği gibi paylaşılan bir proje tooupdate UI yardımcı bir yöntem kullanır.</span><span class="sxs-lookup"><span data-stu-id="143c0-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="143c0-178">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="143c0-178">What's next</span></span>
<span data-ttu-id="143c0-179">Artık çalışan bir, kullanıcıların kimliğini doğrulamak ve güvenli bir şekilde beş farklı platformlarda OAuth 2.0 kullanarak web API çağırma Xamarin uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="143c0-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="143c0-180">Kiracı kullanıcılarla zaten doldurulmuş yapmadıysanız, başlangıç saati toodo şekilde sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="143c0-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="143c0-181">DirectorySearcher uygulamanızı çalıştırın ve ardından hello kullanıcılardan birine oturum açın.</span><span class="sxs-lookup"><span data-stu-id="143c0-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="143c0-182">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="143c0-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="143c0-183">ADAL hello uygulamaya kolay tooincorporate ortak kimlik özelliklerinin kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="143c0-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="143c0-184">Bunu tüm hello dirty çalışmanın sizin için önbellek yönetimi gibi OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, hello kullanıcı sunan mvc'deki ve yenileme belirteçleri süresi.</span><span class="sxs-lookup"><span data-stu-id="143c0-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="143c0-185">Tooknow yalnızca tek bir API çağrısı gereksinim `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="143c0-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="143c0-186">Merhaba başvuru için karşıdan [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (yapılandırma değerleriniz olmadan).</span><span class="sxs-lookup"><span data-stu-id="143c0-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="143c0-187">Şimdi tooadditional kimlik senaryoları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="143c0-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="143c0-188">Örneğin, [Azure AD ile .NET Web API'si güvenli](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="143c0-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
