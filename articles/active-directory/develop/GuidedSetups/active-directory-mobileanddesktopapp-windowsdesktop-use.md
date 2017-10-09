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
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Merhaba Microsoft Graph API Hello Microsoft kimlik doğrulama kitaplığı (MSAL) tooget bir belirteci kullanın

Bu bölümde, nasıl toouse MSAL tooget bir belirteç hello Microsoft Graph API gösterir.

1.  İçinde `MainWindow.xaml.cs`, MSAL kitaplığı toohello sınıfı hello başvurusunu ekleyin:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Değiştir <code>MainWindow</code> sınıf koduyla:
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
### <a name="more-information"></a>Daha Fazla Bilgi
#### <a name="getting-a-user-token-interactive"></a>Etkileşimli bir kullanıcı belirteci alma
Arama hello `AcquireTokenAsync` isteyen bir pencere yöntemi sonuçları hello kullanıcı toosign. Uygulamalar genellikle zorunlu kullanıcı toosign etkileşimli olarak hello içinde tooaccess ihtiyaç duydukları ilk kez korunan bir kaynağa veya Sessiz işlemi tooacquire bir belirteç başarısız oluyor (örneğin hello kullanıcının parolasının süresi).

#### <a name="getting-a-user-token-silently"></a>Bir kullanıcı sessizce belirteci alma
`AcquireTokenSilentAsync`belirteç satın almalar ve herhangi bir kullanıcı etkileşimi olmadan yenileme işler. Sonra `AcquireTokenAsync` hello için ilk kez yürütüldüğünde `AcquireTokenSilentAsync` hello kullanılan her zamanki yöntemi tooobtain kullanılan belirteçleri tooaccess sonraki çağrılar için-kaynaklar çağrıları toorequest korumalı veya belirteçleri yenileme sessiz bir şekilde yapılır.
Sonuç olarak, `AcquireTokenSilentAsync` başarısız olur – örneğin hello kullanıcı oturumunuz veya başka bir aygıtta parolalarını değişti. MSAL hello sorun çözümlenir etkileşimli bir eylem kılarak, harekete algıladığında bir `MsalUiRequiredException`. Uygulamanız bu özel durumun iki yolla işleyebilir:

1.  Karşı çağırmaya `AcquireTokenAsync` hemen hangi sonuçları toosign bileşenini hello kullanıcıdan içinde. Bu deseni genelde çevrimiçi uygulamalarda kullanılır söz konusu olduğunda çevrimdışı içerik hello uygulamada hello kullanıcı için kullanılabilir. Merhaba destekli bu kurulum tarafından oluşturulan örnek bu desen kullanır: hello örnek yürütme ilk kez eylemin hello görebilirsiniz: hiçbir kullanıcı herhangi bir zamanda Merhaba uygulaması kullanıldığından `PublicClientApp.Users.FirstOrDefault()` bir null değer içerir ve bir `MsalUiRequiredException` özel durum. çağırarak özel durum işleyici hello sonra hello örnek kodda Hello `AcquireTokenAsync` toosign bileşenini hello kullanıcıdan içinde sonuçlanır.

2.  Uygulamalar ayrıca bir etkileşimli oturum açma hello kullanıcı hello doğru zamanı toosign seçebilir ya da hello başvurusunda gerekli olan bir görsel gösterimi toohello kullanıcı olun `AcquireTokenSilentAsync` daha sonra. Bu genellikle kullanılan hello kullanıcı kesintiye olmadan hello uygulama diğer işlevlerini kullanabilirsiniz - örneğin, çevrimdışı içeriği hello uygulamada kullanılabilir olduğunda. Bu durumda, hello kullanıcı ne zaman toosign tooaccess korumalı hello kaynak istedikleri toorefresh hello eski bilgi veya uygulamanızın tooretry karar verebilirsiniz karar verebilir `AcquireTokenSilentAsync` ağ zaman geri geçici olarak kullanılamıyor kaldıktan sonra.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Yalnızca aldığınız hello belirteci kullanarak hello Microsoft Graph API çağrısı

1. Merhaba yeni yöntemi tooyour aşağıda eklemek `MainWindow.xaml.cs`. Merhaba kullanılan toomake yöntemdir bir `GET` bir Authorize üstbilgisi kullanarak grafik API'sine isteği:

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
### <a name="more-information-on-making-a-rest-call-against-a-protected-api"></a>Karşı korumalı bir API REST çağrısı yapma hakkında daha fazla bilgi

Bu örnek uygulamasında hello `GetHttpContentWithToken` yöntemdir kullanılan toomake bir HTTP `GET` belirteci ve ardından dönüş hello içerik toohello çağıran gerektirir korunan bir kaynağa karşı istek. Bu yöntem hello edinilen belirteci hello ekler *HTTP Authorization Üstbilgisi*. Merhaba Microsoft Graph API Bu örnek için hello kaynaktır *bana* endpoint – hello kullanıcının profil bilgilerini görüntüler.
<!--end-collapse-->

## <a name="add-a-method-toosign-out-hello-user"></a>Merhaba kullanıcı çıkışı yöntemi toosign Ekle

1. Yöntem tooyour aşağıdaki hello eklemek `MainWindow.xaml.cs` toosign hello kullanıcı çıkışı:

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
### <a name="more-info-on-sign-out"></a>Oturum kapatma hakkında daha fazla bilgi

`SignOutButton_Click`Kullanıcı MSAL kullanıcı önbelleğinden kaldırır hello – toobe etkileşimli yapılırsa, gelecekteki isteği tooacquire bir belirteç yalnızca başarılı şekilde bu MSAL tooforget hello geçerli kullanıcının etkin bir şekilde söyler.
Tek bir kullanıcı bu örnekte Merhaba uygulaması desteklemesine rağmen MSAL burada birden çok hesabı olabilir açan hello senaryolarını destekler. aynı anda – örneğidir bir e-posta uygulamasının bir kullanıcı birden fazla hesap sahip olduğu.
<!--end-collapse-->

## <a name="display-basic-token-information"></a>Temel belirteci bilgilerini görüntüle

1. Yöntem tootooyour aşağıdaki hello eklemek `MainWindow.xaml.cs` toodisplay hello belirteci ile ilgili temel bilgileri:

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
### <a name="more-information"></a>Daha Fazla Bilgi

Belirteçleri edinilen aracılığıyla *Openıd Connect* küçük bir alt bilgi ilgili toohello kullanıcının de içerir. `DisplayBasicTokenInfo`Merhaba belirtecinde yer alan temel bilgileri görüntüler: Örneğin, hello kullanıcının adı ve kimliği görüntülemek yanı sıra hello hello erişim belirteci kendisini temsil eden belirteci süre sonu tarihi ve hello dize. Bu bilgiler, toosee görüntülenir. Merhaba isabet *Microsoft Graph API çağrısı* birden çok kez düğmesine tıklayın ve aynı belirtecin sonraki istekleri için yeniden bu hello bakın. MSAL zaman toorenew hello belirteci olduğuna karar genişletilen hello sona erme tarihini de görebilirsiniz.
<!--end-collapse-->

