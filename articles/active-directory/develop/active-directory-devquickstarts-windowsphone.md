---
title: "Azure AD Windows Phone Başlarken | Microsoft Docs"
description: "Oturum açmak için Azure AD ile tümleşir ve Azure AD çağıran bir Windows Phone uygulama oluşturmak nasıl OAuth kullanan API'ler korumalı."
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
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="be667-103">Azure AD ile Windows Phone Uygulama Tümleştirme</span><span class="sxs-lookup"><span data-stu-id="be667-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="be667-104">Windows Phone 8.1 ve önceki sürümlerde oluşturulmuş projeler Visual Studio 2017’de desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="be667-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="be667-105">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="be667-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="be667-106">Windows Phone 8.1 uygulama geliştiriyorsanız, Azure AD Basit ve kolay, kullanıcılarınız kendi Active Directory hesapları ile kimlik doğrulaması kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="be667-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="be667-107">Ayrıca, tüm web API Office 365 API'leri veya Azure API'sini gibi Azure AD tarafından korunan güvenli bir şekilde kullanmak uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="be667-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="be667-108">Bu kod örneği, ADAL v2.0 kullanır.</span><span class="sxs-lookup"><span data-stu-id="be667-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="be667-109">En son teknoloji için bunun yerine denemek isteyebilirsiniz bizim [ADAL v3.0 kullanarak Windows Evrensel Öğreticisine](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="be667-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="be667-110">Windows Phone 8.1 için gerçekten bir uygulama geliştiriyorsanız, bu en iyi yerdir.</span><span class="sxs-lookup"><span data-stu-id="be667-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="be667-111">ADAL v2.0 hala tam olarak desteklenir ve Windows Phone 8.1 uygulamaları agianst geliştirmenin önerilen yöntem Azure AD kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="be667-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="be667-112">Korunan kaynaklara erişim için gereken .NET yerel istemciler için Azure AD Active Directory kimlik doğrulama kitaplığı veya ADAL sağlar.</span><span class="sxs-lookup"><span data-stu-id="be667-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="be667-113">ADAL'ın tek amacı hayatta erişim belirteçleri almak uygulamanızı daha kolay hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="be667-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="be667-114">Ne kadar kolay olduğunu göstermek için burada size bir "Directory noktasıdır" Windows Phone 8.1 uygulama, yapı:</span><span class="sxs-lookup"><span data-stu-id="be667-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="be667-115">Alır erişim belirteçleri kullanarak Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="be667-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="be667-116">Verilen UPN olan kullanıcılar için bir dizin arar.</span><span class="sxs-lookup"><span data-stu-id="be667-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="be667-117">İşaretlerini kullanıcıları.</span><span class="sxs-lookup"><span data-stu-id="be667-117">Signs users out.</span></span>

<span data-ttu-id="be667-118">Tam çalışan uygulama oluşturmak için ihtiyacınız:</span><span class="sxs-lookup"><span data-stu-id="be667-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="be667-119">Uygulamanızı Azure AD ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="be667-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="be667-120">Yükleme & ADAL yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="be667-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="be667-121">ADAL, Azure AD'den belirteçleri almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="be667-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="be667-122">Başlamak için [bir çatı projesini indirin](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) veya [tamamlanan örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="be667-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="be667-123">Her bir Visual Studio 2013 çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="be667-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="be667-124">Ayrıca, kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.</span><span class="sxs-lookup"><span data-stu-id="be667-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="be667-125">Bir kiracı yoksa [edinebileceğinizi öğrenin](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="be667-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="be667-126">1. Dizin noktasıdır uygulamayı Kaydet</span><span class="sxs-lookup"><span data-stu-id="be667-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="be667-127">Belirteçleri almak uygulamanızı etkinleştirmek için ilk Azure AD kiracınızda kaydetmek ve Azure AD grafik API'sine erişim izni vermek gerekir:</span><span class="sxs-lookup"><span data-stu-id="be667-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="be667-128">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="be667-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="be667-129">Üst çubuğunda hesabınızda altında tıklatıp **Directory** listesinde, Active Directory Kiracı uygulamanızı kaydetmek için istediğiniz yeri seçin.</span><span class="sxs-lookup"><span data-stu-id="be667-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="be667-130">Tıklayın **daha Hizmetleri** sol taraftaki gezinti içinde ve **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="be667-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="be667-131">Tıklayın **uygulama kayıtlar** ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="be667-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="be667-132">Komut istemlerini izleyin ve yeni bir **yerel istemci uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="be667-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="be667-133">**Adı** uygulamayı son kullanıcılar uygulamanıza anlatmaktadır</span><span class="sxs-lookup"><span data-stu-id="be667-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="be667-134">**Yeniden yönlendirme URI'si** Azure AD belirteci yanıtları döndürmek için kullanacağı düzeni ve dize bir birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="be667-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="be667-135">Şimdilik, örneğin bir yer tutucu değerini girin `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="be667-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="be667-136">Biz bu değer daha sonra değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be667-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="be667-137">Kayıt tamamladıktan sonra AAD uygulamanızı benzersiz bir uygulama kimliği atar.</span><span class="sxs-lookup"><span data-stu-id="be667-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="be667-138">Bu değer gerekir sonraki bölümlerde, bu nedenle uygulama sekmesinden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="be667-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="be667-139">Gelen **ayarları** sayfasında, **gerekli izinler** ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="be667-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="be667-140">Seçin **Microsoft Graph** API olarak ve ekleme **dizin verilerini okuma** altında izni **izinlere temsilci**.</span><span class="sxs-lookup"><span data-stu-id="be667-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="be667-141">Bu kullanıcılar için grafik API'si sorgulamak için uygulamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="be667-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="be667-142">2. Yükleme & ADAL yapılandırın</span><span class="sxs-lookup"><span data-stu-id="be667-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="be667-143">Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="be667-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="be667-144">Azure AD ile iletişim kurabilmesi adal sırada uygulama kaydınızı hakkında bazı bilgiler ile sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be667-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="be667-145">Paket Yöneticisi konsolu kullanılarak DirectorySearcher projeye ADAL ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="be667-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="be667-146">DirectorySearcher projeyi açın `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="be667-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="be667-147">Değerleri değiştirin `Config Values` Azure Portalı'na giriş değerleri yansıtacak şekilde bölge.</span><span class="sxs-lookup"><span data-stu-id="be667-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="be667-148">ADAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="be667-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="be667-149">`tenant` Azure AD kiracınız, ör. contoso.onmicrosoft.com etki alanıdır</span><span class="sxs-lookup"><span data-stu-id="be667-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="be667-150">`clientId` Portaldan kopyaladığınız uygulamanızın istemci kimliği değil.</span><span class="sxs-lookup"><span data-stu-id="be667-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="be667-151">Artık Windows Phone uygulamanız için geri çağırma URI bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be667-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="be667-152">Bu satırında bir kesme noktası belirleyerek `MainPage` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="be667-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="be667-153">Uygulamayı çalıştırın ve kenara değerini kopyalayın `redirectUri` zaman kesme noktası isabet.</span><span class="sxs-lookup"><span data-stu-id="be667-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="be667-154">Aşağıdakine benzer görünmelidir</span><span class="sxs-lookup"><span data-stu-id="be667-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="be667-155">Geri **yapılandırma** sekmesi uygulamanızın Azure Yönetim Portalı'nda, değerini değiştirin **RedirectUri** bu değere sahip.</span><span class="sxs-lookup"><span data-stu-id="be667-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="be667-156">3. AAD belirteçleri almak için ADAL'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="be667-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="be667-157">Temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, onu yalnızca çağırdığı ilkesidir `authContext.AcquireToken(…)`, ve ADAL rest yapar.</span><span class="sxs-lookup"><span data-stu-id="be667-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="be667-158">İlk adım, uygulamanızın başlatmaktır `AuthenticationContext` -birincil sınıfı ADAL.</span><span class="sxs-lookup"><span data-stu-id="be667-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="be667-159">ADAL burada geçirdiğiniz budur gereken Azure AD ile iletişim kurmasını ve onu nasıl belirteçleri önbelleğe söyleyin koordinatları.</span><span class="sxs-lookup"><span data-stu-id="be667-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="be667-160">Şimdi bulun `Search(...)` uygulamanın kullanıcı Arabiriminde kullanıcı cliks "Ara" düğmesini olduğunda çağrılacak yöntem.</span><span class="sxs-lookup"><span data-stu-id="be667-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="be667-161">Bu yöntem, UPN verilen arama terimiyle kullanıcıları için Azure AD Graph API sorgu için bir GET isteği yapar.</span><span class="sxs-lookup"><span data-stu-id="be667-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="be667-162">Ancak bir access_token ile dahil etmeniz grafik API'si sorgulamak için `Authorization` üstbilgi ve istek - ADAL nereden geldiğini olan budur.</span><span class="sxs-lookup"><span data-stu-id="be667-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="be667-163">Etkileşimli kimlik doğrulaması gerekli olduğunda, ADAL Windows Phone ' ın Web kimlik doğrulama Aracısı (WAB) kullanır ve [devamlılık modeli](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) Azure AD oturum açma sayfasında görüntülenecek.</span><span class="sxs-lookup"><span data-stu-id="be667-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="be667-164">Kullanıcı oturum açtığında ADAL geçirmek uygulamanız gereken WAB etkileşim sonuçları.</span><span class="sxs-lookup"><span data-stu-id="be667-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="be667-165">Bu uygulama olarak kadar basittir `ContinueWebAuthentication` arabirimi:</span><span class="sxs-lookup"><span data-stu-id="be667-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="be667-166">Kullanın şimdi `AuthenticationResult` , uygulamanız için ADAL döndürdü.</span><span class="sxs-lookup"><span data-stu-id="be667-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="be667-167">İçinde `QueryGraph(...)` geri arama, yetkilendirme üst GET isteğini aldığınız access_token ekleme:</span><span class="sxs-lookup"><span data-stu-id="be667-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="be667-168">Aynı zamanda `AuthenticationResult` uygulamanızda kullanıcı hakkındaki bilgileri görüntülemek için nesne.</span><span class="sxs-lookup"><span data-stu-id="be667-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="be667-169">İçinde `QueryGraph(...)` yöntemi, kullanıcının kimliğini sayfada göstermek için sonuç kullanın:</span><span class="sxs-lookup"><span data-stu-id="be667-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="be667-170">Son olarak, kullanıcı uygulama da dışında imzalamak için ADAL kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be667-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="be667-171">Kullanıcı "Oturumu Kapat" düğmesini tıklattığında sonraki çağrısı emin olmak istiyoruz `AcquireTokenSilentAsync(...)` başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="be667-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="be667-172">ADAL ile bu belirteç önbelleği temizleme olarak kadar kolaydır:</span><span class="sxs-lookup"><span data-stu-id="be667-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="be667-173">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="be667-173">Congratulations!</span></span> <span data-ttu-id="be667-174">Artık çalışma kullanıcıların kimliğini doğrulamak için güvenli bir şekilde Web OAuth 2.0 kullanan API'leri çağırmak gönderebilen Windows Phone Uygulama sahip ve kullanıcı hakkındaki temel bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="be667-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="be667-175">Henüz yapmadıysanız, bazı kullanıcılar ile Kiracı doldurmak için zaman sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="be667-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="be667-176">DirectorySearcher uygulamanızı çalıştırın ve bu kullanıcıların biri oturum oturum.</span><span class="sxs-lookup"><span data-stu-id="be667-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="be667-177">Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.</span><span class="sxs-lookup"><span data-stu-id="be667-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="be667-178">Uygulamayı kapatın ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="be667-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="be667-179">Kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="be667-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="be667-180">Oturumu kapatın ve başka bir kullanıcı olarak yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="be667-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="be667-181">ADAL, bu ortak kimlik özelliklerin tümü, uygulamanıza eklemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="be667-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="be667-182">Bu tüm dirty iş, - önbellek yönetimi, OAuth protokol desteği, kullanıcı bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme sunmak için mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="be667-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="be667-183">Gerçekten bilmeniz gereken tek şey tek bir API çağrısı `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="be667-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="be667-184">Başvuru için tamamlanan örnek (yapılandırma değerleriniz olmadan) sağlanır [burada](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="be667-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="be667-185">Artık ek kimlik senaryolara geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be667-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="be667-186">Denemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="be667-186">You may want to try:</span></span>

[<span data-ttu-id="be667-187">.NET Web API'si Azure AD ile güvenli >></span><span class="sxs-lookup"><span data-stu-id="be667-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

