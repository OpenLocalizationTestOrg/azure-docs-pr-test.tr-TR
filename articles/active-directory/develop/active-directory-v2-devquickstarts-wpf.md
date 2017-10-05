---
title: Azure Active Directory v2.0 .NET yerel uygulama | Microsoft Docs
description: "Kullanıcıların hem kişisel Microsoft Account oturum ve iş veya Okul hesapları imzalar .NET yerel uygulama oluşturma."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="9c8e1-103">Bir Windows masaüstü uygulamasına oturum açma ekleme</span><span class="sxs-lookup"><span data-stu-id="9c8e1-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="9c8e1-104">İle v2.0 uç hızla Masaüstü uygulamalarınızı hem kişisel Microsoft hesapları için destek ile kimlik doğrulaması ve iş veya Okul hesapları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="9c8e1-105">Ayrıca, güvenli bir şekilde bir arka uç ile iletişim kurmak uygulamanızı sağlar web API'si, yanı [Microsoft Graph](https://graph.microsoft.io) ve bazılarını [Office 365 birleşik API'leri](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="9c8e1-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="9c8e1-106">Tüm Azure Active Directory (AD) senaryolarını ve özelliklerini v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="9c8e1-107">V2.0 uç kullanmanızın gerekli olup olmadığını belirlemek için okuyun [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9c8e1-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="9c8e1-108">İçin [bir cihazda çalıştırma .NET yerel uygulamalar](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD Microsoft Identity kimlik doğrulama kitaplığı veya MSAL sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="9c8e1-109">Hayatta MSAL'ın tek amacı, web hizmetleri çağırmak için belirteçleri almak, uygulamanız için kolay hale getirmektir.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="9c8e1-110">Ne kadar kolay olduğunu göstermek için burada size bir .NET WPF Yapılacaklar listesi uygulaması, yapı:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="9c8e1-111">Kullanıcı oturum açtığında & alır erişim belirteçleri kullanarak [OAuth 2.0 kimlik doğrulama protokolü](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="9c8e1-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="9c8e1-112">Arka uç OAuth 2.0 tarafından da güvenli Yapılacaklar listesi web hizmeti, güvenli bir şekilde çağırır.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="9c8e1-113">Kullanıcı oturumu kapattığında.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="9c8e1-114">Örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="9c8e1-114">Download sample code</span></span>
<span data-ttu-id="9c8e1-115">Bu öğretici için kod [GitHub'da](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet) korunur.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="9c8e1-116">İzlemek için [uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) veya çatıyı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="9c8e1-117">De Bu öğretici sonunda tamamlanmış uygulama sağlanır.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="9c8e1-118">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="9c8e1-118">Register an app</span></span>
<span data-ttu-id="9c8e1-119">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="9c8e1-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="9c8e1-120">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-120">Make sure to:</span></span>

* <span data-ttu-id="9c8e1-121">Aşağı kopyalama **uygulama kimliği** uygulamanıza atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="9c8e1-122">Ekleme **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="9c8e1-123">Yükleme & MSAL yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9c8e1-123">Install & Configure MSAL</span></span>
<span data-ttu-id="9c8e1-124">Microsoft ile kayıtlı bir uygulamaya sahip olduğunuza göre MSAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="9c8e1-125">V2.0 uç iletişim kurabilmesi MSAL uygulama kaydınızı hakkında bazı bilgiler ile sağlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="9c8e1-126">Paket Yöneticisi konsolu kullanılarak TodoListClient projeye MSAL ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="9c8e1-127">TodoListClient projeyi açın `app.config`.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="9c8e1-128">Öğeleri değerleri değiştirmek `<appSettings>` uygulama kayıt Portalı'na giriş değerleri yansıtacak şekilde bölümü.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="9c8e1-129">MSAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="9c8e1-130">`ida:ClientId` Olan **uygulama kimliği** portaldan kopyaladığınız, uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="9c8e1-131">TodoList hizmet projeyi açın `web.config` proje kökündeki.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="9c8e1-132">Değiştir `ida:Audience` aynı değerle **uygulama kimliği** portalından.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="9c8e1-133">Belirteçleri almak için MSAL kullanın</span><span class="sxs-lookup"><span data-stu-id="9c8e1-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="9c8e1-134">Temel MSAL arkasındaki bir erişim belirteci, uygulamanızı gereksinim duyduğunda, yalnızca çağrısı ilkesidir `app.AcquireToken(...)`, ve MSAL rest yapar.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="9c8e1-135">İçinde `TodoListClient` proje, açık `MainWindow.xaml.cs` ve bulun `OnInitialized(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="9c8e1-136">İlk adım, uygulamanızın başlatmaktır `PublicClientApplication` -yerel uygulamalar temsil eden MSAL'ın birincil sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="9c8e1-137">Burada, Azure AD ile iletişim kurmasını ve onu nasıl belirteçleri önbelleğe söyleyin gereken koordinatları MSAL geçirmek budur.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="9c8e1-138">Uygulama başlatıldığında denetleyin ve kullanıcı uygulamaya zaten imzalı değilse görmek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="9c8e1-139">Ancak, bir oturum açma kullanıcı Arabirimi henüz çağrılacak istemediğiniz - "işareti Bunu yapmak için" tıklatın kullanıcı hale getireceğiz.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="9c8e1-140">Ayrıca, `OnInitialized(...)` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="9c8e1-141">Kullanıcı oturum açmadı ve "Oturum Aç" düğmesini tıklatın, oturum açma kullanıcı Arabirimi çağırmak ve kimlik bilgilerini girin kullanıcının istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="9c8e1-142">Oturum açma düğmesi işleyicisi uygulayın:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="9c8e1-143">Kullanıcı başarıyla oturum açtığında, MSAL almak ve sizin için bir belirteç önbelleğe ve çağrı geçebilirsiniz `GetTodoList()` güvenle yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="9c8e1-144">Bir kullanıcının görevleri almak için sol şey uygulamak için `GetTodoList()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="9c8e1-145">Çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9c8e1-145">Run</span></span>
<span data-ttu-id="9c8e1-146">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="9c8e1-146">Congratulations!</span></span> <span data-ttu-id="9c8e1-147">Artık kullanıcıların kimliğini doğrulamak ve güvenli bir şekilde Web OAuth 2.0 kullanan API'leri çağırmak için gönderebilen bir çalışma .NET WPF uygulaması sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="9c8e1-148">Her iki projelerinizi çalıştırın ve kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="9c8e1-149">Görevler kullanıcının yapılacaklar listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="9c8e1-150">Oturumu kapatın ve başka bir kullanıcı olarak kendi yapılacaklar listesini görüntülemek için yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="9c8e1-151">Uygulamayı kapatın ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="9c8e1-152">Nasıl kullanıcının oturumunu değişmeden kalır - uygulama bir yerel dosya belirteçleri önbelleğe alır, çünkü dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="9c8e1-153">MSAL uygulamanıza, genel kimlik özellikleri içerecek şekilde hem kişisel hem de iş hesaplarını kullanarak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="9c8e1-154">Bu tüm dirty iş, - önbellek yönetimi, OAuth protokol desteği, kullanıcı bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme sunmak için mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="9c8e1-155">Gerçekten bilmeniz gereken tek şey tek bir API çağrısı `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="9c8e1-156">(Yapılandırma değerleriniz olmadan) tamamlanan örnek, başvuru için [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="9c8e1-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c8e1-157">Next steps</span></span>
<span data-ttu-id="9c8e1-158">Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="9c8e1-159">Denemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-159">You may want to try:</span></span>

* [<span data-ttu-id="9c8e1-160">V2.0 uç noktası ile TodoListService Web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="9c8e1-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="9c8e1-161">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="9c8e1-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="9c8e1-162">V2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="9c8e1-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="9c8e1-163">StackOverflow "msal" etiketi >></span><span class="sxs-lookup"><span data-stu-id="9c8e1-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="9c8e1-164">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="9c8e1-164">Get security updates for our products</span></span>
<span data-ttu-id="9c8e1-165">[Bu sayfayı](https://technet.microsoft.com/security/dd252948) ziyaret ederek ve Güvenlik Önerisi Uyarılarına abone olarak güvenlik olaylarının ne zaman ortaya çıkacağı hakkında bildirimleri almanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9c8e1-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

