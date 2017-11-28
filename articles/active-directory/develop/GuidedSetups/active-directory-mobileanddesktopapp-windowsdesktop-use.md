---
title: "Azure AD v2 Windows Masaüstü başlamak - kullanın | Microsoft Docs"
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
ms.openlocfilehash: 826ba0a00b26993d4f37f0a8ce587d7bb77e7eb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="use-the-microsoft-authentication-library-msal-to-get-a-token-for-the-microsoft-graph-api"></a><span data-ttu-id="45141-103">Microsoft Graph API için bir belirteç almak üzere Microsoft kimlik doğrulama kitaplığı (MSAL) kullanın</span><span class="sxs-lookup"><span data-stu-id="45141-103">Use the Microsoft Authentication Library (MSAL) to get a token for the Microsoft Graph API</span></span>

<span data-ttu-id="45141-104">Bu bölümde MSAL Microsoft Graph API'si bir belirteç almak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="45141-104">This section shows how to use MSAL to get a token the Microsoft Graph API.</span></span>

1.  <span data-ttu-id="45141-105">İçinde `MainWindow.xaml.cs`, MSAL Kitaplığı Başvurusu sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="45141-105">In `MainWindow.xaml.cs`, add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="45141-106">Değiştir <code>MainWindow</code> sınıf koduyla:</span><span class="sxs-lookup"><span data-stu-id="45141-106">Replace <code>MainWindow</code> class code with:</span></span>
</li>
</ol>

```csharp
public partial class MainWindow : Window
{
    //Set the API Endpoint to Graph 'me' endpoint
    string _graphAPIEndpoint = "https://graph.microsoft.com/v1.0/me";

    //Set the scope for API call to user.read
    string[] _scopes = new string[] { "user.read" };


    public MainWindow()
    {
        InitializeComponent();
    }

    /// <summary>
    /// Call AcquireTokenAsync - to acquire a token requiring user to sign-in
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
            // A MsalUiRequiredException happened on AcquireTokenSilentAsync. This indicates you need to call AcquireTokenAsync to acquire a token
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
### <a name="more-information"></a><span data-ttu-id="45141-107">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="45141-107">More Information</span></span>
#### <a name="getting-a-user-token-interactive"></a><span data-ttu-id="45141-108">Etkileşimli bir kullanıcı belirteci alma</span><span class="sxs-lookup"><span data-stu-id="45141-108">Getting a user token interactive</span></span>
<span data-ttu-id="45141-109">Çağırma `AcquireTokenAsync` yöntemi, oturum açmak için kullanıcıdan bir pencere sonuçlanıyor.</span><span class="sxs-lookup"><span data-stu-id="45141-109">Calling the `AcquireTokenAsync` method results in a window prompting the user to sign in.</span></span> <span data-ttu-id="45141-110">Uygulamalar genellikle gerektirir etkileşimli olarak korunan bir kaynağa erişmek için ihtiyaç duydukları ilk kez oturum açmak bir kullanıcı ya da (örneğin kullanıcının parolasının süresi) belirteci başarısız edinmeye sessiz bir işlem.</span><span class="sxs-lookup"><span data-stu-id="45141-110">Applications usually require a user to sign in interactively the first time they need to access a protected resource, or when a silent operation to acquire a token fails (e.g. the user’s password expired).</span></span>

#### <a name="getting-a-user-token-silently"></a><span data-ttu-id="45141-111">Bir kullanıcı sessizce belirteci alma</span><span class="sxs-lookup"><span data-stu-id="45141-111">Getting a user token silently</span></span>
<span data-ttu-id="45141-112">`AcquireTokenSilentAsync`belirteç satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler.</span><span class="sxs-lookup"><span data-stu-id="45141-112">`AcquireTokenSilentAsync` handles token acquisitions and renewal without any user interaction.</span></span> <span data-ttu-id="45141-113">Sonra `AcquireTokenAsync` ilk kez yürütüldüğünde `AcquireTokenSilentAsync` veya belirteçleri yenileme isteği için çağrıları sessizce gerçekleştirilmediğinden sonraki çağrılar için-korumalı kaynaklara erişmek için kullanılan belirteçleri elde etmek için kullanılan normal yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="45141-113">After `AcquireTokenAsync` is executed for the first time, `AcquireTokenSilentAsync` is the usual method used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.</span></span>
<span data-ttu-id="45141-114">Sonuç olarak, `AcquireTokenSilentAsync` başarısız olur – örneğin kullanıcı oturumunuz veya başka bir aygıtta parolalarını değişti.</span><span class="sxs-lookup"><span data-stu-id="45141-114">Eventually, `AcquireTokenSilentAsync` will fail – e.g. the user has signed out, or has changed their password on another device.</span></span> <span data-ttu-id="45141-115">MSAL algıladığında, etkileşimli bir eylem gerektirmeyen tarafından sorunu çözmek için harekete bir `MsalUiRequiredException`.</span><span class="sxs-lookup"><span data-stu-id="45141-115">When MSAL detects that the issue can be resolved by requiring an interactive action, it fires an `MsalUiRequiredException`.</span></span> <span data-ttu-id="45141-116">Uygulamanız bu özel durumun iki yolla işleyebilir:</span><span class="sxs-lookup"><span data-stu-id="45141-116">Your application can handle this exception in two ways:</span></span>

1.  <span data-ttu-id="45141-117">Karşı çağırmaya `AcquireTokenAsync` hemen hangi sonuçları oturum açma kullanıcıdan içinde.</span><span class="sxs-lookup"><span data-stu-id="45141-117">Make a call against `AcquireTokenAsync` immediately, which results in prompting the user to sign-in.</span></span> <span data-ttu-id="45141-118">Bu deseni genelde çevrimiçi uygulamalarda kullanılır söz konusu olduğunda çevrimdışı içerik uygulamada kullanıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="45141-118">This pattern is usually used in online applications where there is no offline content in the application available for the user.</span></span> <span data-ttu-id="45141-119">Destekli Bu kurulum tarafından oluşturulan örnek bu deseni kullanır: örnek yürütme eylemi ilk zamanında görebilirsiniz: hiçbir kullanıcı, uygulamayı her zamankinden kullanıldığından `PublicClientApp.Users.FirstOrDefault()` bir null değer içerir ve bir `MsalUiRequiredException` özel durum.</span><span class="sxs-lookup"><span data-stu-id="45141-119">The sample generated by this guided setup uses this pattern: you can see it in action the first time you execute the sample: because no user ever used the application, `PublicClientApp.Users.FirstOrDefault()` will contain a null value, and an `MsalUiRequiredException` exception will be thrown.</span></span> <span data-ttu-id="45141-120">Ardından örnek kodda çağırarak özel durumu işler `AcquireTokenAsync` oturum açma kullanıcıdan içinde sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="45141-120">The code in the sample then handles the exception by calling `AcquireTokenAsync` resulting in prompting the user to sign-in.</span></span>

2.  <span data-ttu-id="45141-121">Uygulamalar bir etkileşimli oturum açma kullanıcı oturum açmak için doğru zamanı seçebilir ya da uygulama deneyebilirsiniz gerekli olan kullanıcı için görsel bir gösterge de yapabilirsiniz `AcquireTokenSilentAsync` daha sonra.</span><span class="sxs-lookup"><span data-stu-id="45141-121">Applications can also make a visual indication to the user that an interactive sign-in is required, so the user can select the right time to sign in, or the application can retry `AcquireTokenSilentAsync` at a later time.</span></span> <span data-ttu-id="45141-122">Bu genellikle kullanılan kullanıcı kesintiye olmadan diğer uygulamanın işlevselliğini kullanabilir - Örneğin, çevrimdışı içeriği uygulamada kullanılabilir olduğunda.</span><span class="sxs-lookup"><span data-stu-id="45141-122">This is usually used when the user can use other functionality of the application without being disrupted - for example, there is offline content available in the application.</span></span> <span data-ttu-id="45141-123">Bu durumda, kullanıcı ne zaman korumalı kaynağa erişmek için ya da eski bilgileri yenilemek için oturum açmak istedikleri veya uygulamanızın denemeye karar verebilirsiniz karar verebilir `AcquireTokenSilentAsync` ağ zaman geri geçici olarak kullanılamıyor kaldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="45141-123">In this case, the user can decide when they want to sign in to access the protected resource, or to refresh the outdated information, or your application can decide to retry `AcquireTokenSilentAsync` when network is restored after being unavailable temporarily.</span></span>
<!--end-collapse-->

## <a name="call-the-microsoft-graph-api-using-the-token-you-just-obtained"></a><span data-ttu-id="45141-124">Yalnızca edinilen belirteçle kullanarak Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="45141-124">Call the Microsoft Graph API using the token you just obtained</span></span>

1. <span data-ttu-id="45141-125">Aşağıda yeni yöntemine ekleyin, `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="45141-125">Add the new method below to your `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="45141-126">Yöntem yapmak için kullanılan bir `GET` bir Authorize üstbilgisi kullanarak grafik API'sine isteği:</span><span class="sxs-lookup"><span data-stu-id="45141-126">The method is used to make a `GET` request against Graph API using an Authorize header:</span></span>

```csharp
/// <summary>
/// Perform an HTTP GET request to a URL using an HTTP Authorization header
/// </summary>
/// <param name="url">The URL</param>
/// <param name="token">The token</param>
/// <returns>String containing the results of the GET operation</returns>
public async Task<string> GetHttpContentWithToken(string url, string token)
{
    var httpClient = new System.Net.Http.HttpClient();
    System.Net.Http.HttpResponseMessage response;
    try
    {
        var request = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, url);
        //Add the token in Authorization header
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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a><span data-ttu-id="45141-127">Karşı korumalı bir API REST çağrısı yapma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="45141-127">More information on making a REST call against a protected API</span></span>

<span data-ttu-id="45141-128">Bu örnek uygulamasında `GetHttpContentWithToken` yöntemi bir HTTP yapmak için kullanılan `GET` isteği için bir belirteç gerekiyor korunan bir kaynağa karşı ve ardından içeriği çağırana dönün.</span><span class="sxs-lookup"><span data-stu-id="45141-128">In this sample application, the `GetHttpContentWithToken` method is used to make an HTTP `GET` request against a protected resource that requires a token and then return the content to the caller.</span></span> <span data-ttu-id="45141-129">Bu yöntem alınan belirteç ekler *HTTP Authorization Üstbilgisi*.</span><span class="sxs-lookup"><span data-stu-id="45141-129">This method adds the acquired token in the *HTTP Authorization header*.</span></span> <span data-ttu-id="45141-130">Bu örnek için Microsoft Graph API kaynaktır *bana* endpoint – kullanıcı profili bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="45141-130">For this sample, the resource is the Microsoft Graph API *me* endpoint – which displays the user's profile information.</span></span>
<!--end-collapse-->

## <a name="add-a-method-to-sign-out-the-user"></a><span data-ttu-id="45141-131">Kullanıcı imzalamak için bir yöntem ekleyin</span><span class="sxs-lookup"><span data-stu-id="45141-131">Add a method to sign out the user</span></span>

1. <span data-ttu-id="45141-132">Aşağıdaki yöntemi ekleyin, `MainWindow.xaml.cs` kullanıcı imzalamak için:</span><span class="sxs-lookup"><span data-stu-id="45141-132">Add the following method to your `MainWindow.xaml.cs` to sign out the user:</span></span>

```csharp
/// <summary>
/// Sign out the current user
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
### <a name="more-info-on-sign-out"></a><span data-ttu-id="45141-133">Oturum kapatma hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="45141-133">More info on Sign-Out</span></span>

<span data-ttu-id="45141-134">`SignOutButton_Click`Kullanıcı etkileşimli olarak yapılırsa bir belirteç almak için gelecekteki bir isteği yalnızca başarılı şekilde geçerli kullanıcının unuttunuz için bu MSAL etkili bir şekilde söyler MSAL kullanıcı önbellekten – kaldırır.</span><span class="sxs-lookup"><span data-stu-id="45141-134">`SignOutButton_Click` removes the user from MSAL user cache – this will effectively tell MSAL to forget the current user so a future request to acquire a token will only succeed if it is made to be interactive.</span></span>
<span data-ttu-id="45141-135">Bu örnek uygulamasında tek bir kullanıcı desteklese de MSAL nerede birden fazla hesap oturum açmış aynı anda – bir e-posta uygulamasının bir kullanıcı birden fazla hesap sahip olduğu örneğidir senaryolarını destekler.</span><span class="sxs-lookup"><span data-stu-id="45141-135">Although the application in this sample supports a single user, MSAL supports scenarios where multiple accounts can be signed-in at the same time – an example is an email application where a user has multiple accounts.</span></span>
<!--end-collapse-->

## <a name="display-basic-token-information"></a><span data-ttu-id="45141-136">Temel belirteci bilgilerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="45141-136">Display Basic Token Information</span></span>

1. <span data-ttu-id="45141-137">İçin aşağıdaki yöntemi ekleyin, `MainWindow.xaml.cs` belirteci ile ilgili temel bilgileri görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="45141-137">Add the following method to to your `MainWindow.xaml.cs` to display basic information about the token:</span></span>

```csharp
/// <summary>
/// Display basic information contained in the token
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
### <a name="more-information"></a><span data-ttu-id="45141-138">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="45141-138">More Information</span></span>

<span data-ttu-id="45141-139">Belirteçleri edinilen aracılığıyla *Openıd Connect* küçük bir alt kullanıcıya ilgili bilgileri de içerir.</span><span class="sxs-lookup"><span data-stu-id="45141-139">Tokens acquired via *OpenID Connect* also contain a small subset of information pertinent to the user.</span></span> <span data-ttu-id="45141-140">`DisplayBasicTokenInfo`belirtecinde yer alan temel bilgileri görüntüler: Örneğin, kullanıcının görünen adı ve kimliği için belirteç süre sonu tarihi ve erişim temsil eden dize yanı sıra kendi simge.</span><span class="sxs-lookup"><span data-stu-id="45141-140">`DisplayBasicTokenInfo` displays basic information contained in the token: for example, the user's display name and ID, as well as the token expiration date and the string representing the access token itself.</span></span> <span data-ttu-id="45141-141">Bu bilgileri görmek için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45141-141">This information is displayed for you to see.</span></span> <span data-ttu-id="45141-142">İsabet *Microsoft Graph API çağrısı* birden çok kez düğmesine tıklayın ve aynı belirtecin sonraki istekleri için yeniden kullanılmış bakın.</span><span class="sxs-lookup"><span data-stu-id="45141-142">You can hit the *Call Microsoft Graph API* button multiple times and see that the same token was reused for subsequent requests.</span></span> <span data-ttu-id="45141-143">MSAL onu kapılarını açtığında genişletilen belirteci yenileme süresi sona erme tarihi de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45141-143">You can also see the expiration date being extended when MSAL decides it is time to renew the token.</span></span>
<!--end-collapse-->

