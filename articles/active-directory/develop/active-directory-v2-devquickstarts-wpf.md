---
title: aaaAzure Active Directory v2.0 .NET yerel uygulama | Microsoft Docs
description: "Nasıl toobuild .NET yerel uygulaması, kullanıcıların hem kişisel Microsoft Account oturum açtığında ve iş veya Okul hesapları."
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
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="bc2de-103">Oturum açma tooa Windows Masaüstü uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="bc2de-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="bc2de-104">Merhaba hello v2.0 uç ile kimlik doğrulaması tooyour Masaüstü uygulamaları hem kişisel Microsoft hesapları için destek ve iş veya Okul hesapları ile kolayca ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2de-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="bc2de-105">Bu ayrıca, uygulama toosecurely arka ucuyla iletişim etkinleştirir web API'si, yanı [Microsoft Graph hello](https://graph.microsoft.io) ve hello bazılarını [Office 365 birleşik API'leri](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="bc2de-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="bc2de-106">Tüm Azure Active Directory (AD) senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="bc2de-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="bc2de-107">Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="bc2de-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="bc2de-108">İçin [bir cihazda çalıştırma .NET yerel uygulamalar](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD hello Microsoft Identity kimlik doğrulama kitaplığı ya da MSAL sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc2de-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="bc2de-109">Hayatta MSAL'ın tek amacı, uygulama tooget için kolay, web hizmetleri çağırmak için belirteçler toomake ' dir.</span><span class="sxs-lookup"><span data-stu-id="bc2de-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="bc2de-110">toodemonstrate olduğu, ne kadar kolay burada size bir .NET WPF Yapılacaklar listesi uygulaması, yapı:</span><span class="sxs-lookup"><span data-stu-id="bc2de-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="bc2de-111">İşaretlerini hello kullanıcı & alır erişim belirteçleri hello kullanarak [OAuth 2.0 kimlik doğrulama protokolü](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="bc2de-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="bc2de-112">Arka uç OAuth 2.0 tarafından da güvenli Yapılacaklar listesi web hizmeti, güvenli bir şekilde çağırır.</span><span class="sxs-lookup"><span data-stu-id="bc2de-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="bc2de-113">İşaretlerini hello kullanıcı çıkışı.</span><span class="sxs-lookup"><span data-stu-id="bc2de-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="bc2de-114">Örnek kodu indirin</span><span class="sxs-lookup"><span data-stu-id="bc2de-114">Download sample code</span></span>
<span data-ttu-id="bc2de-115">Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="bc2de-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="bc2de-116">yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:</span><span class="sxs-lookup"><span data-stu-id="bc2de-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="bc2de-117">Tamamlanan hello uygulama hello de bu öğreticinin sonunda sağlanır.</span><span class="sxs-lookup"><span data-stu-id="bc2de-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="bc2de-118">Bir uygulamayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="bc2de-118">Register an app</span></span>
<span data-ttu-id="bc2de-119">En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="bc2de-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="bc2de-120">Emin olun:</span><span class="sxs-lookup"><span data-stu-id="bc2de-120">Make sure to:</span></span>

* <span data-ttu-id="bc2de-121">Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="bc2de-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="bc2de-122">Merhaba eklemek **mobil** uygulamanız için platform.</span><span class="sxs-lookup"><span data-stu-id="bc2de-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="bc2de-123">Yükleme & MSAL yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bc2de-123">Install & Configure MSAL</span></span>
<span data-ttu-id="bc2de-124">Microsoft ile kayıtlı bir uygulamaya sahip olduğunuza göre MSAL yükleyin ve kimlikle ilgili kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="bc2de-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="bc2de-125">MSAL toobe mümkün toocommunicate hello v2.0 uç noktası için sırayla tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.</span><span class="sxs-lookup"><span data-stu-id="bc2de-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="bc2de-126">Merhaba Paket Yöneticisi konsolu kullanarak MSAL toohello TodoListClient proje ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="bc2de-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="bc2de-127">Merhaba TodoListClient projeyi açın `app.config`.</span><span class="sxs-lookup"><span data-stu-id="bc2de-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="bc2de-128">Merhaba hello öğelerin Hello değerleri değiştirmek `<appSettings>` bölüm tooreflect hello hello uygulama kayıt portalı giriş değerleri.</span><span class="sxs-lookup"><span data-stu-id="bc2de-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="bc2de-129">MSAL kullandığında kodunuzu bu değerleri başvurur.</span><span class="sxs-lookup"><span data-stu-id="bc2de-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="bc2de-130">Merhaba `ida:ClientId` hello olan **uygulama kimliği** hello portalından kopyaladığınız, uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="bc2de-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="bc2de-131">Merhaba TodoList hizmet projeyi açın `web.config` hello projesinin hello kök.</span><span class="sxs-lookup"><span data-stu-id="bc2de-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="bc2de-132">Hello yerine `ida:Audience` hello ile aynı değer **uygulama kimliği** hello portalından.</span><span class="sxs-lookup"><span data-stu-id="bc2de-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="bc2de-133">MSAL tooget belirteçleri kullanın</span><span class="sxs-lookup"><span data-stu-id="bc2de-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="bc2de-134">Merhaba temel MSAL arkasındaki bir erişim belirteci, uygulamanızı gereksinim duyduğunda, yalnızca çağrısı ilkesidir `app.AcquireToken(...)`, ve MSAL rest hello.</span><span class="sxs-lookup"><span data-stu-id="bc2de-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="bc2de-135">Merhaba, `TodoListClient` proje, açık `MainWindow.xaml.cs` ve hello bulun `OnInitialized(...)` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bc2de-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="bc2de-136">Merhaba ilk adım, uygulamanızın tooinitialize olan `PublicClientApplication` -yerel uygulamalar temsil eden MSAL'ın birincil sınıfı.</span><span class="sxs-lookup"><span data-stu-id="bc2de-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="bc2de-137">MSAL burada geçirdiğiniz budur hello Azure AD ile toocommunicate gereken koordinatları ve nasıl söyleyin toocache belirteçleri.</span><span class="sxs-lookup"><span data-stu-id="bc2de-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="bc2de-138">Merhaba uygulama başladığında biz toocheck istediğiniz ve hello kullanıcı hello uygulamaya zaten oturum açmışsa, bkz.</span><span class="sxs-lookup"><span data-stu-id="bc2de-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="bc2de-139">Ancak, bir oturum açma kullanıcı Arabirimi tooinvoke henüz istediğiniz yok - "Oturum Aç" toodo şekilde tıklatın hello kullanıcı hale getireceğiz.</span><span class="sxs-lookup"><span data-stu-id="bc2de-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="bc2de-140">Merhaba, ayrıca `OnInitialized(...)` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="bc2de-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
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

* <span data-ttu-id="bc2de-141">Merhaba kullanıcı oturum açmadı ve hello "Oturum Aç" düğmesini tıklatın, biz tooinvoke oturum açma kullanıcı Arabirimi istediğiniz ve hello kullanıcı kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="bc2de-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="bc2de-142">Oturum açma Hello düğme işleyicisi uygulayın:</span><span class="sxs-lookup"><span data-stu-id="bc2de-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

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
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
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

* <span data-ttu-id="bc2de-143">Merhaba kullanıcı başarıyla oturum açtığında, MSAL almak ve sizin için bir belirteç önbelleğe ve toocall hello geçebilmeniz `GetTodoList()` güvenle yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bc2de-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="bc2de-144">Bir kullanıcının görevlerin tooget ayrıldı şey tooimplement hello `GetTodoList()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bc2de-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

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

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

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

## <a name="run"></a><span data-ttu-id="bc2de-145">Çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bc2de-145">Run</span></span>
<span data-ttu-id="bc2de-146">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="bc2de-146">Congratulations!</span></span> <span data-ttu-id="bc2de-147">Artık çalışan bir hello özelliği tooauthenticate kullanıcılara .NET WPF uygulaması sahip & güvenli bir şekilde Web OAuth 2.0 kullanan API'leri çağırmak.</span><span class="sxs-lookup"><span data-stu-id="bc2de-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="bc2de-148">Her iki projelerinizi çalıştırın ve kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bc2de-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="bc2de-149">Görevleri toothat kullanıcının yapılacaklar listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bc2de-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="bc2de-150">Oturumu kapatın ve başka bir kullanıcı tooview kendi Yapılacaklar listesi yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="bc2de-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="bc2de-151">Merhaba uygulamasını kapatın ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc2de-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="bc2de-152">Nasıl hello kullanıcının oturumunu değişmeden kalır - hello uygulama yerel bir dosya belirteçleri önbelleğe alır, çünkü dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bc2de-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="bc2de-153">MSAL kolay tooincorporate ortak kimlik özelliklerinin uygulamanıza, hem kişisel hem de iş hesaplarını kullanarak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="bc2de-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="bc2de-154">Bu tüm hello dirty iş, - önbellek yönetimi, OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme hello kullanıcı sunmak için mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="bc2de-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="bc2de-155">Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="bc2de-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="bc2de-156">Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc2de-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="bc2de-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc2de-157">Next steps</span></span>
<span data-ttu-id="bc2de-158">Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc2de-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="bc2de-159">Tootry isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc2de-159">You may want tootry:</span></span>

* [<span data-ttu-id="bc2de-160">Merhaba v2.0 uç noktası ile Merhaba TodoListService Web API güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="bc2de-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="bc2de-161">Ek kaynaklar için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="bc2de-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="bc2de-162">Merhaba v2.0 Geliştirici Kılavuzu >></span><span class="sxs-lookup"><span data-stu-id="bc2de-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="bc2de-163">StackOverflow "msal" etiketi >></span><span class="sxs-lookup"><span data-stu-id="bc2de-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="bc2de-164">Ürünlerimiz için güvenlik güncelleştirmelerini alma</span><span class="sxs-lookup"><span data-stu-id="bc2de-164">Get security updates for our products</span></span>
<span data-ttu-id="bc2de-165">Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="bc2de-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

