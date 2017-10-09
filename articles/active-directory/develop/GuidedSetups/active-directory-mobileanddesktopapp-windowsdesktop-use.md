---
title: "aaaAzure AD v2 Windows Masaüstü Getting Started - kullanım | Microsoft Docs"
description: "Windows Masaüstü .NET (XAML) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: bb258fe5f523ec727ca02716fd823d853d3349b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a><span data-ttu-id="ee359-103">Merhaba Microsoft Graph API Hello Microsoft kimlik doğrulama kitaplığı (MSAL) tooget bir belirteci kullanın</span><span class="sxs-lookup"><span data-stu-id="ee359-103">Use hello Microsoft Authentication Library (MSAL) tooget a token for hello Microsoft Graph API</span></span>

<span data-ttu-id="ee359-104">Bu bölümde, nasıl toouse MSAL tooget bir belirteç hello Microsoft Graph API gösterir.</span><span class="sxs-lookup"><span data-stu-id="ee359-104">This section shows how toouse MSAL tooget a token hello Microsoft Graph API.</span></span>

1.  <span data-ttu-id="ee359-105">İçinde `MainWindow.xaml.cs`, MSAL kitaplığı toohello sınıfı hello başvurusunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ee359-105">In `MainWindow.xaml.cs`, add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="ee359-106">Değiştir <code>MainWindow</code> sınıf koduyla:</span><span class="sxs-lookup"><span data-stu-id="ee359-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set hello API Endpoint tooGraph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set hello scope for API call toouser.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - tooacquire a token requiring user toosign-in
    /// </summary>
    private async void CallGraphButton_Click(object sender, RoutedEventArgs e)
    {
        AuthenticationResult authResult = null;

        try
        {
            authResult = await App.PublicClientApp.AcquireTokenSilentAsync(_scopes, App.PublicClientApp.Users.FirstOrDefault());
        }
        catch (MsalUiRequiredException ex)
        {
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need toocall AcquireTokenAsync tooacquire a token
            System.Diagnostics.Debug.WriteLine($"MsalUiRequiredException: {ex.Message}");

            try
            {
                authResult = await App.PublicClientApp.AcquireTokenAsync(_scopes);
            }
            catch (MsalException msalex)
            {
                ResultText.Text = $"Error Acquiring Token:{System.Environment.NewLine}{msalex}";
            }
        }
        catch (Exception ex)
        {
            ResultText.Text = $"Error Acquiring Token Silently:{System.Environment.NewLine}{ex}";
            return;
        }

        if (authResult != null)
        {
            ResultText.Text = await GetHttpContentWithToken(_graphAPIEndpoint, authResult.AccessToken);
            DisplayBasicTokenInfo(authResult);
            this.SignOutButton.Visibility = Visibility.Visible;
        }
    }
}
```

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="ee359-107">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="ee359-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="ee359-108">Etkileşimli bir kullanıcı belirteci alma</span><span class="sxs-lookup"><span data-stu-id="ee359-108">Getting a user token interactive</span></span>
<span data-ttu-id="ee359-109">Arama hello `AcquireTokenAsync` isteyen bir pencere yöntemi sonuçları hello kullanıcı toosign.</span><span class="sxs-lookup"><span data-stu-id="ee359-109">Calling hello `AcquireTokenAsync` method results in a window prompting hello user toosign in.</span></span> <span data-ttu-id="ee359-110">Uygulamalar genellikle zorunlu kullanıcı toosign etkileşimli olarak hello içinde tooaccess ihtiyaç duydukları ilk kez korunan bir kaynağa veya Sessiz işlemi tooacquire bir belirteç başarısız oluyor (örneğin hello kullanıcının parolasının süresi).</span><span class="sxs-lookup"><span data-stu-id="ee359-110">Applications usually require a user toosign in interactively hello first time they need tooaccess a protected resource, or when a silent operation tooacquire a token fails (e.g. hello user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="ee359-111">Bir kullanıcı sessizce belirteci alma</span><span class="sxs-lookup"><span data-stu-id="ee359-111">Getting a user token silently</span></span>
<span data-ttu-id="ee359-112">`AcquireTokenSilentAsync`belirteç satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler.</span><span class="sxs-lookup"><span data-stu-id="ee359-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="ee359-113">Sonra `AcquireTokenAsync` hello için ilk kez yürütüldüğünde `AcquireTokenSilentAsync` hello kullanılan her zamanki yöntemi tooobtain kullanılan belirteçleri tooaccess sonraki çağrılar için-kaynaklar çağrıları toorequest korumalı veya belirteçleri yenileme sessiz bir şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="ee359-113">After `AcquireTokenAsync` is executed for hello first time, `AcquireTokenSilentAsync` is hello usual method used tooobtain tokens used tooaccess protected resources for subsequent calls - as calls toorequest or renew tokens are made silently.</span></span>
<span data-ttu-id="ee359-114">Sonuç olarak, `AcquireTokenSilentAsync` başarısız olur – örneğin hello kullanıcı oturumunuz veya başka bir aygıtta parolalarını değişti.</span><span class="sxs-lookup"><span data-stu-id="ee359-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. hello user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="ee359-115">MSAL hello sorun çözümlenir etkileşimli bir eylem kılarak, harekete algıladığında bir `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="ee359-115">When MSAL detects that hello issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="ee359-116">Uygulamanız bu özel durumun iki yolla işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="ee359-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="ee359-117">Karşı çağırmaya `AcquireTokenAsync` hemen hangi sonuçları toosign bileşenini hello kullanıcıdan içinde.</span><span class="sxs-lookup"><span data-stu-id="ee359-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting hello user toosign-in.</span></span> <span data-ttu-id="ee359-118">Bu deseni genelde çevrimiçi uygulamalarda kullanılır söz konusu olduğunda çevrimdışı içerik hello uygulamada hello kullanıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ee359-118">This pattern is usually used in online applications where there is no offline content in hello application available for hello user.</span></span> <span data-ttu-id="ee359-119">Merhaba destekli bu kurulum tarafından oluşturulan örnek bu desen kullanır: hello örnek yürütme ilk kez eylemin hello görebilirsiniz: hiçbir kullanıcı herhangi bir zamanda Merhaba uygulaması kullanıldığından `PublicClientApp.Users.FirstOrDefault()` bir null değer içerir ve bir `MsalUiRequiredException` özel durum.</span><span class="sxs-lookup"><span data-stu-id="ee359-119">hello sample generated by this guided setup uses this pattern: you can see it in action hello first time you execute hello sample: because no user ever used hello application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="ee359-120">çağırarak özel durum işleyici hello sonra hello örnek kodda Hello `AcquireTokenAsync` toosign bileşenini hello kullanıcıdan içinde sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ee359-120">hello code in hello sample then handles hello exception by calling `AcquireTokenAsync` resulting in prompting hello user toosign-in.</span></span>

2.  <span data-ttu-id="ee359-121">Uygulamalar ayrıca bir etkileşimli oturum açma hello kullanıcı hello doğru zamanı toosign seçebilir ya da hello başvurusunda gerekli olan bir görsel gösterimi toohello kullanıcı olun `AcquireTokenSilentAsync` daha sonra.</span><span class="sxs-lookup"><span data-stu-id="ee359-121">Applications can also make a visual indication toohello user that an interactive sign-in is required, so hello user can select hello right time toosign in, or hello application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="ee359-122">Bu genellikle kullanılan hello kullanıcı kesintiye olmadan hello uygulama diğer işlevlerini kullanabilirsiniz - örneğin, çevrimdışı içeriği hello uygulamada kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="ee359-122">This is usually used when hello user can use other functionality of hello application without being disrupted - for example, there is offline content available in hello application.</span></span> <span data-ttu-id="ee359-123">Bu durumda, hello kullanıcı ne zaman toosign tooaccess korumalı hello kaynak istedikleri toorefresh hello eski bilgi veya uygulamanızın tooretry karar verebilirsiniz karar verebilir `AcquireTokenSilentAsync` ağ zaman geri geçici olarak kullanılamıyor kaldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="ee359-123">In this case, hello user can decide when they want toosign in tooaccess hello protected resource, or toorefresh hello outdated information, or your application can decide tooretry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a><span data-ttu-id="ee359-124">Yalnızca aldığınız hello belirteci kullanarak hello Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="ee359-124">Call hello Microsoft Graph API using hello token you just obtained</span></span>

1. <span data-ttu-id="ee359-125">Merhaba yeni yöntemi tooyour aşağıda eklemek `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="ee359-125">Add hello new method below tooyour `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="ee359-126">Merhaba kullanılan toomake yöntemdir bir `GET` bir Authorize üstbilgisi kullanarak grafik API'sine isteği:</span><span class="sxs-lookup"><span data-stu-id="ee359-126">hello method is used toomake a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request tooa URL using an HTTP Authorization header
/// </summary>
/// <param name="url">hello URL</param>
/// <param name="token">hello token</param>
/// <returns>String containing hello results of hello GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add hello token in Authorization header
        request.Headers.Authorization = new System.Net.Http.Headers.AuthenticationHeaderValue("Bearer", token);
        response = await httpClient.SendAsync(request);
        var content = await response.Content.ReadAsStringAsync();
        return content;
    }
    catch (Exception ex)
    {
        return ex.ToString();
    }
}
```
<!--start-collapse-->
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="ee359-127">Karşı korumalı bir API REST çağrısı yapma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="ee359-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="ee359-128">Bu örnek uygulamasında hello `GetHttpContentWithToken` yöntemdir kullanılan toomake bir HTTP `GET` belirteci ve ardından dönüş hello içerik toohello çağıran gerektirir korunan bir kaynağa karşı istek.</span><span class="sxs-lookup"><span data-stu-id="ee359-128">In this sample application, hello `GetHttpContentWithToken` method is used toomake an HTTP `GET` request against a protected resource that requires a token and then return hello content toohello caller.</span></span> <span data-ttu-id="ee359-129">Bu yöntem hello edinilen belirteci hello ekler *HTTP Authorization Üstbilgisi*.</span><span class="sxs-lookup"><span data-stu-id="ee359-129">This method adds hello acquired token in hello *HTTP Authorization header*.</span></span> <span data-ttu-id="ee359-130">Merhaba Microsoft Graph API Bu örnek için hello kaynaktır *bana* endpoint – hello kullanıcının profil bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ee359-130">For this sample, hello resource is hello Microsoft Graph API *me* endpoint – which displays hello user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a><span data-ttu-id="ee359-131">Merhaba kullanıcı çıkışı yöntemi toosign Ekle</span><span class="sxs-lookup"><span data-stu-id="ee359-131">Add a method toosign out hello user</span></span>

1. <span data-ttu-id="ee359-132">Yöntem tooyour aşağıdaki hello eklemek `MainWindow.xaml.cs` toosign hello kullanıcı çıkışı:</span><span class="sxs-lookup"><span data-stu-id="ee359-132">Add hello following method tooyour `MainWindow.xaml.cs` toosign out hello user:</span></span>

```csharp
/// <summary>
/// Sign out hello current user
/// </summary>
private void SignOutButton_Click(object sender, RoutedEventArgs e)
{
    if (App.PublicClientApp.Users.Any())
    {
        try
        {
            App.PublicClientApp.Remove(App.PublicClientApp.Users.FirstOrDefault());
            this.ResultText.Text = "User has signed-out";
            this.CallGraphButton.Visibility = Visibility.Visible;
            this.SignOutButton.Visibility = Visibility.Collapsed;
        }
        catch (MsalException ex)
        {
            ResultText.Text = $"Error signing-out user: {ex.Message}";
        }
    }
}
```
<!--start-collapse-->
### <a name="more-info-on-sign-out"></a><span data-ttu-id="ee359-133">Oturum kapatma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="ee359-133">More info on Sign-Out</span></span>

<span data-ttu-id="ee359-134">`SignOutButton_Click`Kullanıcı MSAL kullanıcı önbelleğinden kaldırır hello – toobe etkileşimli yapılırsa, gelecekteki isteği tooacquire bir belirteç yalnızca başarılı şekilde bu MSAL tooforget hello geçerli kullanıcının etkin bir şekilde söyler.</span><span class="sxs-lookup"><span data-stu-id="ee359-134">`SignOutButton_Click` removes hello user from MSAL user cache – this will effectively tell MSAL tooforget hello current user so a future request tooacquire a token will only succeed if it is made toobe interactive.</span></span>
<span data-ttu-id="ee359-135">Tek bir kullanıcı bu örnekte Merhaba uygulaması desteklemesine rağmen MSAL burada birden çok hesabı olabilir açan hello senaryolarını destekler. aynı anda – örneğidir bir e-posta uygulamasının bir kullanıcı birden fazla hesap sahip olduğu.</span><span class="sxs-lookup"><span data-stu-id="ee359-135">Although hello application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at hello same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="ee359-136">Temel belirteci bilgilerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="ee359-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="ee359-137">Yöntem tootooyour aşağıdaki hello eklemek `MainWindow.xaml.cs` toodisplay hello belirteci ile ilgili temel bilgileri:</span><span class="sxs-lookup"><span data-stu-id="ee359-137">Add hello following method tootooyour `MainWindow.xaml.cs` toodisplay basic information about hello token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in hello token
/// </summary>
private void DisplayBasicTokenInfo(AuthenticationResult authResult)
{
    TokenInfoText.Text = "";
    if (authResult != null)
    {
        TokenInfoText.Text += $"Name: {authResult.User.Name}" + Environment.NewLine;
        TokenInfoText.Text += $"Username: {authResult.User.DisplayableId}" + Environment.NewLine;
        TokenInfoText.Text += $"Token Expires: {authResult.ExpiresOn.ToLocalTime()}" + Environment.NewLine;
        TokenInfoText.Text += $"Access Token: {authResult.AccessToken}" + Environment.NewLine;
    }
}
```
<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="ee359-138">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="ee359-138">More Information</span></span>

<span data-ttu-id="ee359-139">Belirteçleri edinilen aracılığıyla *Openıd Connect* küçük bir alt bilgi ilgili toohello kullanıcının de içerir.</span><span class="sxs-lookup"><span data-stu-id="ee359-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent toohello user.</span></span> <span data-ttu-id="ee359-140">`DisplayBasicTokenInfo`Merhaba belirtecinde yer alan temel bilgileri görüntüler: Örneğin, hello kullanıcının adı ve kimliği görüntülemek yanı sıra hello hello erişim belirteci kendisini temsil eden belirteci süre sonu tarihi ve hello dize.</span><span class="sxs-lookup"><span data-stu-id="ee359-140">`DisplayBasicTokenInfo` displays basic information contained in hello token: for example, hello user's display name and ID, as well as hello token expiration date and hello string representing hello access token itself.</span></span> <span data-ttu-id="ee359-141">Bu bilgiler, toosee görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ee359-141">This information is displayed for you toosee.</span></span> <span data-ttu-id="ee359-142">Merhaba isabet *Microsoft Graph API çağrısı* birden çok kez düğmesine tıklayın ve aynı belirtecin sonraki istekleri için yeniden bu hello bakın.</span><span class="sxs-lookup"><span data-stu-id="ee359-142">You can hit hello *Call Microsoft Graph API* button multiple times and see that hello same token was reused for subsequent requests.</span></span> <span data-ttu-id="ee359-143">MSAL zaman toorenew hello belirteci olduğuna karar genişletilen hello sona erme tarihini de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee359-143">You can also see hello expiration date being extended when MSAL decides it is time toorenew hello token.</span></span>
<!--end-collapse-->

