---
title: "aaaAzure AD Windows Phone Başlarken | Microsoft Docs"
description: "Nasıl toobuild oturum açmak için Azure AD ile tümleştirilen ve Azure AD çağıran bir Windows Phone Uygulama OAuth kullanan API'ler korumalı."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="09f7f-103">Azure AD ile Windows Phone Uygulama Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="09f7f-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="09f7f-104">Windows Phone 8.1 ve önceki sürümlerde oluşturulmuş projeler Visual Studio 2017’de desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="09f7f-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="09f7f-105">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="09f7f-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="09f7f-106">Windows Phone 8.1 uygulama geliştiriyorsanız, Azure AD Basit ve kolay, tooauthenticate için Active Directory hesaplarını Kullanıcılarınızla kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="09f7f-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="09f7f-107">Ayrıca, uygulama toosecurely sağlar Office 365 API'leri hello veya Azure API hello gibi tüm web Azure AD tarafından korunan API'si kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="09f7f-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="09f7f-108">Bu kod örneği, ADAL v2.0 kullanır.</span><span class="sxs-lookup"><span data-stu-id="09f7f-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="09f7f-109">Merhaba son teknoloji tooinstead deneyin isteyebilirsiniz bizim [ADAL v3.0 kullanarak Windows Evrensel Öğreticisine](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="09f7f-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="09f7f-110">Windows Phone 8.1 için gerçekten bir uygulama geliştiriyorsanız, hello doğru yerde budur.</span><span class="sxs-lookup"><span data-stu-id="09f7f-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="09f7f-111">ADAL v2.0 hala tam olarak desteklenir ve hello önerilen yol geliştirme uygulamaları agianst Windows Phone 8.1, Azure AD kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="09f7f-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="09f7f-112">Korumalı tooaccess kaynakları gereken .NET yerel istemciler için Azure AD hello Active Directory kimlik doğrulama kitaplığı ya da ADAL sağlar.</span><span class="sxs-lookup"><span data-stu-id="09f7f-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="09f7f-113">ADAL'ın tek amacı hayatta toomake olduğu için uygulama tooget erişim belirteçleri kolay.</span><span class="sxs-lookup"><span data-stu-id="09f7f-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="09f7f-114">toodemonstrate olduğu, ne kadar kolay burada size bir "Directory noktasıdır" Windows Phone 8.1 uygulama, yapı:</span><span class="sxs-lookup"><span data-stu-id="09f7f-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="09f7f-115">Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="09f7f-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="09f7f-116">Verilen UPN olan kullanıcılar için bir dizin arar.</span><span class="sxs-lookup"><span data-stu-id="09f7f-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="09f7f-117">İşaretlerini kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="09f7f-117">Signs users out.</span></span>

<span data-ttu-id="09f7f-118">toobuild hello tam çalışan bir uygulama ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="09f7f-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="09f7f-119">Uygulamanızı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="09f7f-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="09f7f-120">Yükleme & ADAL yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="09f7f-121">Azure AD'den ADAL tooget belirteçleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="09f7f-122">başlatıldı, tooget [bir çatı projesini indirin](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="09f7f-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="09f7f-123">Her bir Visual Studio 2013 çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="09f7f-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="09f7f-124">Ayrıca, kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="09f7f-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="09f7f-125">Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="09f7f-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="09f7f-126">1. YAZMAÇ hello Directory noktasıdır uygulama</span><span class="sxs-lookup"><span data-stu-id="09f7f-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="09f7f-127">tooenable önce gerekir, uygulama tooget belirteçleri tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin:</span><span class="sxs-lookup"><span data-stu-id="09f7f-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="09f7f-128">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="09f7f-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="09f7f-129">Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.</span><span class="sxs-lookup"><span data-stu-id="09f7f-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="09f7f-130">Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="09f7f-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="09f7f-131">Tıklayın **uygulama kayıtlar** ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="09f7f-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="09f7f-132">Merhaba komut istemlerini izleyin ve yeni bir **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="09f7f-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="09f7f-133">Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın anlatmaktadır</span><span class="sxs-lookup"><span data-stu-id="09f7f-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="09f7f-134">Merhaba **yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanacağını düzeni ve dize birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="09f7f-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="09f7f-135">Şimdilik, örneğin bir yer tutucu değerini girin `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="09f7f-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="09f7f-136">Biz bu değer daha sonra değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09f7f-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="09f7f-137">Kayıt tamamladıktan sonra AAD uygulamanızı benzersiz bir uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="09f7f-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="09f7f-138">Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="09f7f-139">Merhaba gelen **ayarları** sayfasında, **gerekli izinler** ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="09f7f-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="09f7f-140">Select hello **Microsoft Graph** olarak API hello ve hello ekleyin **dizin verilerini okuma** altında izni **izinlere temsilci**.</span><span class="sxs-lookup"><span data-stu-id="09f7f-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="09f7f-141">Bu, kullanıcılar için uygulama tooquery hello grafik API'si olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="09f7f-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="09f7f-142">2. Yükleme & ADAL yapılandırın</span><span class="sxs-lookup"><span data-stu-id="09f7f-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="09f7f-143">Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="09f7f-144">Azure AD ile mümkün toocommunicate ADAL toobe için sırayla tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.</span><span class="sxs-lookup"><span data-stu-id="09f7f-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="09f7f-145">Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher proje ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="09f7f-146">Merhaba DirectorySearcher projeyi açın `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="09f7f-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="09f7f-147">Hello başlangıç değerleri değiştirin `Config Values` bölge tooreflect hello hello Azure Portal giriş değerleri.</span><span class="sxs-lookup"><span data-stu-id="09f7f-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="09f7f-148">ADAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="09f7f-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="09f7f-149">Merhaba `tenant` Azure AD kiracınız, ör. contoso.onmicrosoft.com hello etki alanıdır</span><span class="sxs-lookup"><span data-stu-id="09f7f-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="09f7f-150">Merhaba `clientId` hello ClientID hello portalından kopyaladığınız uygulamanızın olduğu.</span><span class="sxs-lookup"><span data-stu-id="09f7f-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="09f7f-151">Artık Windows Phone uygulamanız için toodiscover hello geri çağırma URI gerekir.</span><span class="sxs-lookup"><span data-stu-id="09f7f-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="09f7f-152">Merhaba bu satırında bir kesme noktası belirleyerek `MainPage` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="09f7f-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="09f7f-153">Merhaba uygulamayı çalıştırın ve kenara hello değerini kopyalayın `redirectUri` zaman hello kesme noktası isabet.</span><span class="sxs-lookup"><span data-stu-id="09f7f-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="09f7f-154">Aşağıdakine benzer görünmelidir</span><span class="sxs-lookup"><span data-stu-id="09f7f-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="09f7f-155">Merhaba üzerinde geri **yapılandırma** hello Azure Yönetim Portalı, uygulamanızda sekmesinde hello hello değerini değiştirin **RedirectUri** bu değere sahip.</span><span class="sxs-lookup"><span data-stu-id="09f7f-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="09f7f-156">3. AAD gelen ADAL tooGet belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="09f7f-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="09f7f-157">Merhaba temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, onu yalnızca çağırdığı ilkesidir `authContext.AcquireToken(…)`, ve ADAL rest hello.</span><span class="sxs-lookup"><span data-stu-id="09f7f-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="09f7f-158">Merhaba ilk adım, uygulamanızın tooinitialize olan `AuthenticationContext` -birincil sınıfı ADAL.</span><span class="sxs-lookup"><span data-stu-id="09f7f-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="09f7f-159">ADAL burada geçirdiğiniz budur hello Azure AD ile toocommunicate gereken koordinatları ve nasıl söyleyin toocache belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="09f7f-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="09f7f-160">Şimdi hello bulun `Search(...)` hello kullanıcı cliks "Ara" düğmesini hello uygulamanın kullanıcı arabiriminde hello olduğunda çağrılacak yöntem.</span><span class="sxs-lookup"><span data-stu-id="09f7f-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="09f7f-161">Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir GET isteği toohello Azure AD Graph API tooquery sağlar.</span><span class="sxs-lookup"><span data-stu-id="09f7f-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="09f7f-162">Ancak sipariş tooquery hello grafik API'si, tooinclude bir access_token ile Merhaba gerekir `Authorization` hello üstbilgisinin isteği - ADAL nereden geldiğini budur.</span><span class="sxs-lookup"><span data-stu-id="09f7f-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="09f7f-163">Etkileşimli kimlik doğrulaması gerekli olduğunda, ADAL Windows Phone ' ın Web kimlik doğrulama Aracısı (WAB) kullanır ve [devamlılık modeli](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sayfasında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="09f7f-164">Merhaba kullanıcı oturum açtığında uygulamanızın toopass ADAL hello hello WAB etkileşim sonuçlarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="09f7f-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="09f7f-165">Bu hello uygulama olarak kadar basittir `ContinueWebAuthentication` arabirimi:</span><span class="sxs-lookup"><span data-stu-id="09f7f-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="09f7f-166">Zaman toouse hello şimdi `AuthenticationResult` bu ADAL tooyour uygulama döndürdü.</span><span class="sxs-lookup"><span data-stu-id="09f7f-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="09f7f-167">Merhaba, `QueryGraph(...)` geri toohello GET isteğini hello yetkilendirme üst bilgisinde aldığınız hello access_token ekleyin:</span><span class="sxs-lookup"><span data-stu-id="09f7f-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="09f7f-168">Merhaba de kullanabilirsiniz `AuthenticationResult` nesne uygulamanızda hello kullanıcı hakkında toodisplay bilgi.</span><span class="sxs-lookup"><span data-stu-id="09f7f-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="09f7f-169">Merhaba, `QueryGraph(...)` yöntemi, kullanım hello sonuç tooshow hello kullanıcının kimliğini hello sayfasında:</span><span class="sxs-lookup"><span data-stu-id="09f7f-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="09f7f-170">Son olarak, ADAL toosign hello kullanıcı dışında uygulama da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09f7f-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="09f7f-171">Merhaba kullanıcı hello "Oturumu Kapat" düğmesini tıklattığında, sonraki çağrı çok hello tooensure istiyoruz`AcquireTokenSilentAsync(...)` başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="09f7f-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="09f7f-172">ADAL ile bu hello belirteç önbelleği temizleme olarak kadar kolaydır:</span><span class="sxs-lookup"><span data-stu-id="09f7f-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="09f7f-173">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="09f7f-173">Congratulations!</span></span> <span data-ttu-id="09f7f-174">Artık çalışan bir hello özelliği tooauthenticate kullanıcılar Windows Phone Uygulama sahip, güvenli bir şekilde OAuth 2.0 kullanan Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="09f7f-175">Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="09f7f-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="09f7f-176">DirectorySearcher uygulamanızı çalıştırın ve bu kullanıcıların biri oturum oturum.</span><span class="sxs-lookup"><span data-stu-id="09f7f-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="09f7f-177">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="09f7f-178">Merhaba uygulamasını kapatın ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="09f7f-179">Merhaba kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="09f7f-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="09f7f-180">Oturumu kapatın ve başka bir kullanıcı olarak yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="09f7f-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="09f7f-181">ADAL kolay tooincorporate kılar uygulamanıza bu ortak kimlik özelliklerin tümü.</span><span class="sxs-lookup"><span data-stu-id="09f7f-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="09f7f-182">Bu tüm hello dirty iş, - önbellek yönetimi, OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme hello kullanıcı sunmak için mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="09f7f-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="09f7f-183">Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="09f7f-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="09f7f-184">Başvuru için tamamlandı hello örnek (yapılandırma değerleriniz olmadan) sağlanır [burada](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="09f7f-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="09f7f-185">Şimdi tooadditional kimlik senaryoları taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09f7f-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="09f7f-186">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09f7f-186">You may want tootry:</span></span>

[<span data-ttu-id="09f7f-187">.NET Web API'si Azure AD ile güvenli >></span><span class="sxs-lookup"><span data-stu-id="09f7f-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

