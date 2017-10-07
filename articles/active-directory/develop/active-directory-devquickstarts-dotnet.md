---
title: "aaaAzure AD .NET Başlarken | Microsoft Docs"
description: "Nasıl toobuild oturum açmak için Azure AD ile tümleştirilen ve Azure AD çağıran bir .NET Windows masaüstü uygulaması OAuth kullanan API'ler korumalı."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="ac19d-103">Azure AD bir Windows Masaüstü WPF uygulamanıza tümleştirmek</span><span class="sxs-lookup"><span data-stu-id="ac19d-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ac19d-104">Bir masaüstü uygulaması geliştiriyorsanız, Azure AD Basit ve kolay, tooauthenticate için Active Directory hesaplarını Kullanıcılarınızla kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ac19d-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="ac19d-105">Ayrıca, uygulama toosecurely sağlar Office 365 API'leri hello veya Azure API hello gibi tüm web Azure AD tarafından korunan API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ac19d-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="ac19d-106">Korumalı tooaccess kaynakları gereken .NET yerel istemciler için Azure AD hello Active Directory kimlik doğrulama kitaplığı ya da ADAL sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac19d-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="ac19d-107">ADAL'ın tek amacı hayatta toomake olduğu için uygulama tooget erişim belirteçleri kolay.</span><span class="sxs-lookup"><span data-stu-id="ac19d-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="ac19d-108">toodemonstrate olduğu, ne kadar kolay burada size bir .NET WPF Yapılacaklar listesi uygulaması, yapı:</span><span class="sxs-lookup"><span data-stu-id="ac19d-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="ac19d-109">Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac19d-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="ac19d-110">Belirtilen diğer ada sahip kullanıcılar için bir dizin arar.</span><span class="sxs-lookup"><span data-stu-id="ac19d-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="ac19d-111">İşaretlerini kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="ac19d-111">Signs users out.</span></span>

<span data-ttu-id="ac19d-112">toobuild hello tam çalışan bir uygulama ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="ac19d-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="ac19d-113">Uygulamanızı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ac19d-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="ac19d-114">Yükleme & ADAL yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="ac19d-115">Azure AD'den ADAL tooget belirteçleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="ac19d-116">başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ac19d-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="ac19d-117">Ayrıca, kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac19d-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="ac19d-118">Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ac19d-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="ac19d-119">1. Merhaba DirectorySearcher uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="ac19d-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="ac19d-120">tooenable önce gerekir, uygulama tooget belirteçleri tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin:</span><span class="sxs-lookup"><span data-stu-id="ac19d-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="ac19d-121">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac19d-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ac19d-122">Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.</span><span class="sxs-lookup"><span data-stu-id="ac19d-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="ac19d-123">Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ac19d-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ac19d-124">Tıklayın **uygulama kayıtlar** ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ac19d-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="ac19d-125">Merhaba komut istemlerini izleyin ve yeni bir **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="ac19d-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="ac19d-126">Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın anlatmaktadır</span><span class="sxs-lookup"><span data-stu-id="ac19d-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="ac19d-127">Merhaba **yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanacağını düzeni ve dize birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="ac19d-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="ac19d-128">Örneğin bir değer belirli tooyour uygulama girin `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="ac19d-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="ac19d-129">Kayıt tamamladıktan sonra AAD uygulamanızı benzersiz bir uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="ac19d-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="ac19d-130">Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sayfadan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="ac19d-131">Merhaba gelen **ayarları** sayfasında, **gerekli izinler** ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ac19d-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="ac19d-132">Select hello **Microsoft Graph** olarak API hello ve hello ekleyin **dizin verilerini okuma** altında izni **izinlere temsilci**.</span><span class="sxs-lookup"><span data-stu-id="ac19d-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="ac19d-133">Bu, kullanıcılar için uygulama tooquery hello grafik API'si olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ac19d-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="ac19d-134">2. Yükleme & ADAL yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ac19d-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="ac19d-135">Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="ac19d-136">Azure AD ile mümkün toocommunicate ADAL toobe için sırayla tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.</span><span class="sxs-lookup"><span data-stu-id="ac19d-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="ac19d-137">Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher proje ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="ac19d-138">Merhaba DirectorySearcher projeyi açın `app.config`.</span><span class="sxs-lookup"><span data-stu-id="ac19d-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="ac19d-139">Merhaba hello öğelerin Hello değerleri değiştirmek `<appSettings>` bölüm tooreflect hello hello Azure Portal giriş değerleri.</span><span class="sxs-lookup"><span data-stu-id="ac19d-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="ac19d-140">ADAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="ac19d-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="ac19d-141">Merhaba `ida:Tenant` Azure AD kiracınız, ör. contoso.onmicrosoft.com hello etki alanıdır</span><span class="sxs-lookup"><span data-stu-id="ac19d-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="ac19d-142">Merhaba `ida:ClientId` hello ClientID hello portalından kopyaladığınız uygulamanızın olduğu.</span><span class="sxs-lookup"><span data-stu-id="ac19d-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="ac19d-143">Merhaba `ida:RedirectUri` hello olan yeniden yönlendirme URL'si hello Portalı'nda kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="ac19d-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="ac19d-144">3.    AAD gelen ADAL tooGet belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ac19d-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="ac19d-145">Merhaba temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, onu yalnızca çağırdığı ilkesidir `authContext.AcquireTokenAsync(...)`, ve ADAL rest hello.</span><span class="sxs-lookup"><span data-stu-id="ac19d-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="ac19d-146">Merhaba, `DirectorySearcher` proje, açık `MainWindow.xaml.cs` ve hello bulun `MainWindow()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ac19d-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="ac19d-147">Merhaba ilk adım, uygulamanızın tooinitialize olan `AuthenticationContext` -birincil sınıfı ADAL.</span><span class="sxs-lookup"><span data-stu-id="ac19d-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="ac19d-148">ADAL burada geçirdiğiniz budur hello Azure AD ile toocommunicate gereken koordinatları ve nasıl söyleyin toocache belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="ac19d-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="ac19d-149">Şimdi hello bulun `Search(...)` hello kullanıcı cliks "Ara" düğmesini hello uygulamanın kullanıcı arabiriminde hello olduğunda çağrılacak yöntem.</span><span class="sxs-lookup"><span data-stu-id="ac19d-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="ac19d-150">Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir GET isteği toohello Azure AD Graph API tooquery sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac19d-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="ac19d-151">Ancak sipariş tooquery hello grafik API'si, tooinclude bir access_token ile Merhaba gerekir `Authorization` hello üstbilgisinin isteği - ADAL nereden geldiğini budur.</span><span class="sxs-lookup"><span data-stu-id="ac19d-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="ac19d-152">Uygulamanızı isteğinde bulunduğunda bir belirteç çağırarak `AcquireTokenAsync(...)`, ADAL hello kullanıcı kimlik bilgilerinin sorulmasına olmadan tooreturn bir belirteç deneyecek.</span><span class="sxs-lookup"><span data-stu-id="ac19d-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="ac19d-153">ADAL tooget bir belirteç toosign hello kullanıcı gerektiğini belirlerse, bir oturum açma iletişim kutusu görüntüler, hello kullanıcının kimlik bilgilerini toplamak ve başarılı bir kimlik doğrulaması sırasında bir simge döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac19d-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="ac19d-154">ADAL herhangi bir nedenle yüklenemiyor tooreturn bir belirteç ise, throw bir `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="ac19d-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="ac19d-155">Bu hello fark `AuthenticationResult` nesnesini içeren bir `UserInfo` uygulamanız gerekebilir kullanılan toocollect bilgi olabilir nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ac19d-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="ac19d-156">Merhaba DirectorySearcher, içinde `UserInfo` kullanılan toocustomize hello uygulamanın UI hello kullanıcının kimliği.</span><span class="sxs-lookup"><span data-stu-id="ac19d-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="ac19d-157">Merhaba kullanıcı hello "Oturumu Kapat" düğmesini tıklattığında, sonraki çağrı çok hello tooensure istiyoruz`AcquireTokenAsync(...)` hello kullanıcı toosign sorar.</span><span class="sxs-lookup"><span data-stu-id="ac19d-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="ac19d-158">ADAL ile bu hello belirteç önbelleği temizleme olarak kadar kolaydır:</span><span class="sxs-lookup"><span data-stu-id="ac19d-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="ac19d-159">Ancak, Hello kullanıcı hello "Oturumu Kapat" düğmesini tıklatın değil, bunlar hello DirectorySearcher sonraki çalıştırmanızda toomaintain hello kullanıcının oturumunu hello için isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ac19d-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="ac19d-160">Merhaba uygulama başlattığında, varolan bir belirteci için ADAL'ın belirteç önbelleği denetleyin ve hello kullanıcı Arabirimi gerektiği gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ac19d-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="ac19d-161">Merhaba, `CheckForCachedToken()` yöntemi, başka bir çok çağırmaya`AcquireTokenAsync(...)`, bu kez hello geçirme `PromptBehavior.Never` parametresi.</span><span class="sxs-lookup"><span data-stu-id="ac19d-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="ac19d-162">`PromptBehavior.Never`ADAL hello kullanıcı oturum açma için sorulması değil ve oluşturamıyor tooreturn ise ADAL bunun yerine bir özel durum bir belirteç oluşturması gerekir söyler.</span><span class="sxs-lookup"><span data-stu-id="ac19d-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="ac19d-163">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="ac19d-163">Congratulations!</span></span> <span data-ttu-id="ac19d-164">Artık çalışan bir hello özelliği tooauthenticate kullanıcılara .NET WPF uygulaması sahip, güvenli bir şekilde OAuth 2.0 kullanan Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="ac19d-165">Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="ac19d-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="ac19d-166">DirectorySearcher uygulamanızı çalıştırın ve bu kullanıcıların biri oturum oturum.</span><span class="sxs-lookup"><span data-stu-id="ac19d-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="ac19d-167">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="ac19d-168">Merhaba uygulamasını kapatın ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="ac19d-169">Merhaba kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ac19d-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="ac19d-170">Oturumu kapatın ve başka bir kullanıcı olarak yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ac19d-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="ac19d-171">ADAL kolay tooincorporate kılar uygulamanıza bu ortak kimlik özelliklerin tümü.</span><span class="sxs-lookup"><span data-stu-id="ac19d-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="ac19d-172">Bu tüm hello dirty iş, - önbellek yönetimi, OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme hello kullanıcı sunmak için mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="ac19d-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="ac19d-173">Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="ac19d-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="ac19d-174">Başvuru için tamamlandı hello örnek (yapılandırma değerleriniz olmadan) sağlanır [burada](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ac19d-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="ac19d-175">Şimdi tooadditional senaryoları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac19d-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="ac19d-176">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ac19d-176">You may want tootry:</span></span>

[<span data-ttu-id="ac19d-177">.NET Web API'si Azure AD ile güvenli >></span><span class="sxs-lookup"><span data-stu-id="ac19d-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

