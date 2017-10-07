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
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Oturum açma tooa Windows Masaüstü uygulama Ekle
Merhaba hello v2.0 uç ile kimlik doğrulaması tooyour Masaüstü uygulamaları hem kişisel Microsoft hesapları için destek ve iş veya Okul hesapları ile kolayca ekleyebilirsiniz.  Bu ayrıca, uygulama toosecurely arka ucuyla iletişim etkinleştirir web API'si, yanı [Microsoft Graph hello](https://graph.microsoft.io) ve hello bazılarını [Office 365 birleşik API'leri](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> Tüm Azure Active Directory (AD) senaryolarını ve özelliklerini hello v2.0 uç noktası tarafından desteklenir.  Merhaba v2.0 uç noktası, kullanmanız gereken varsa toodetermine okuyun hakkında [v2.0 sınırlamaları](active-directory-v2-limitations.md).
> 
> 

İçin [bir cihazda çalıştırma .NET yerel uygulamalar](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD hello Microsoft Identity kimlik doğrulama kitaplığı ya da MSAL sağlar.  Hayatta MSAL'ın tek amacı, uygulama tooget için kolay, web hizmetleri çağırmak için belirteçler toomake ' dir.  toodemonstrate olduğu, ne kadar kolay burada size bir .NET WPF Yapılacaklar listesi uygulaması, yapı:

* İşaretlerini hello kullanıcı & alır erişim belirteçleri hello kullanarak [OAuth 2.0 kimlik doğrulama protokolü](active-directory-v2-protocols.md).
* Arka uç OAuth 2.0 tarafından da güvenli Yapılacaklar listesi web hizmeti, güvenli bir şekilde çağırır.
* İşaretlerini hello kullanıcı çıkışı.

## <a name="download-sample-code"></a>Örnek kodu indirin
Bu öğretici için kod Hello korunduğu [github'da](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip karşıdan](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) veya kopya hello çatıyı:

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

Tamamlanan hello uygulama hello de bu öğreticinin sonunda sağlanır.

## <a name="register-an-app"></a>Bir uygulamayı kaydetme
En yeni bir uygulama oluşturma [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), veya adımları izleyin: [ayrıntılı adımları](active-directory-v2-app-registration.md).  Emin olun:

* Merhaba basılı kopya **uygulama kimliği** tooyour uygulama atanan, bunu en kısa sürede ihtiyacınız vardır.
* Merhaba eklemek **mobil** uygulamanız için platform.

## <a name="install--configure-msal"></a>Yükleme & MSAL yapılandırın
Microsoft ile kayıtlı bir uygulamaya sahip olduğunuza göre MSAL yükleyin ve kimlikle ilgili kodunuzu yazın.  MSAL toobe mümkün toocommunicate hello v2.0 uç noktası için sırayla tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.

* Merhaba Paket Yöneticisi konsolu kullanarak MSAL toohello TodoListClient proje ekleyerek başlayın.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* Merhaba TodoListClient projeyi açın `app.config`.  Merhaba hello öğelerin Hello değerleri değiştirmek `<appSettings>` bölüm tooreflect hello hello uygulama kayıt portalı giriş değerleri.  MSAL kullandığında kodunuzu bu değerleri başvurur.
  
  * Merhaba `ida:ClientId` hello olan **uygulama kimliği** hello portalından kopyaladığınız, uygulamanızın.
* Merhaba TodoList hizmet projeyi açın `web.config` hello projesinin hello kök.  
  
  * Hello yerine `ida:Audience` hello ile aynı değer **uygulama kimliği** hello portalından.

## <a name="use-msal-tooget-tokens"></a>MSAL tooget belirteçleri kullanın
Merhaba temel MSAL arkasındaki bir erişim belirteci, uygulamanızı gereksinim duyduğunda, yalnızca çağrısı ilkesidir `app.AcquireToken(...)`, ve MSAL rest hello.  

* Merhaba, `TodoListClient` proje, açık `MainWindow.xaml.cs` ve hello bulun `OnInitialized(...)` yöntemi.  Merhaba ilk adım, uygulamanızın tooinitialize olan `PublicClientApplication` -yerel uygulamalar temsil eden MSAL'ın birincil sınıfı.  MSAL burada geçirdiğiniz budur hello Azure AD ile toocommunicate gereken koordinatları ve nasıl söyleyin toocache belirteçleri.

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* Merhaba uygulama başladığında biz toocheck istediğiniz ve hello kullanıcı hello uygulamaya zaten oturum açmışsa, bkz.  Ancak, bir oturum açma kullanıcı Arabirimi tooinvoke henüz istediğiniz yok - "Oturum Aç" toodo şekilde tıklatın hello kullanıcı hale getireceğiz.  Merhaba, ayrıca `OnInitialized(...)` yöntemi:

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

* Merhaba kullanıcı oturum açmadı ve hello "Oturum Aç" düğmesini tıklatın, biz tooinvoke oturum açma kullanıcı Arabirimi istediğiniz ve hello kullanıcı kimlik bilgilerini girin.  Oturum açma Hello düğme işleyicisi uygulayın:

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

* Merhaba kullanıcı başarıyla oturum açtığında, MSAL almak ve sizin için bir belirteç önbelleğe ve toocall hello geçebilmeniz `GetTodoList()` güvenle yöntemi.  Bir kullanıcının görevlerin tooget ayrıldı şey tooimplement hello `GetTodoList()` yöntemi.

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

## <a name="run"></a>Çalıştırın
Tebrikler! Artık çalışan bir hello özelliği tooauthenticate kullanıcılara .NET WPF uygulaması sahip & güvenli bir şekilde Web OAuth 2.0 kullanan API'leri çağırmak.  Her iki projelerinizi çalıştırın ve kişisel bir Microsoft hesabı veya bir iş veya Okul hesabınızla oturum açın.  Görevleri toothat kullanıcının yapılacaklar listesi ekleyin.  Oturumu kapatın ve başka bir kullanıcı tooview kendi Yapılacaklar listesi yeniden oturum açın.  Merhaba uygulamasını kapatın ve yeniden çalıştırın.  Nasıl hello kullanıcının oturumunu değişmeden kalır - hello uygulama yerel bir dosya belirteçleri önbelleğe alır, çünkü dikkat edin.

MSAL kolay tooincorporate ortak kimlik özelliklerinin uygulamanıza, hem kişisel hem de iş hesaplarını kullanarak kolaylaştırır.  Bu tüm hello dirty iş, - önbellek yönetimi, OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme hello kullanıcı sunmak için mvc'deki.  Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `app.AcquireTokenAsync(...)`.

Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [burada bir .zip sağlanan](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), veya Github'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Sonraki adımlar
Şimdi daha gelişmiş konu başlıklarına geçebilirsiniz.  Tootry isteyebilirsiniz:

* [Merhaba v2.0 uç noktası ile Merhaba TodoListService Web API güvenliğini sağlama](active-directory-v2-devquickstarts-dotnet-api.md)

Ek kaynaklar için gözden geçirin:  

* [Merhaba v2.0 Geliştirici Kılavuzu >>](active-directory-appmodel-v2-overview.md)
* [StackOverflow "msal" etiketi >>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Ürünlerimiz için güvenlik güncelleştirmelerini alma
Güvenlik olayları ziyaret ederek ortaya çıktığında, tooget bildirimleri öneririz [bu sayfayı](https://technet.microsoft.com/security/dd252948) ve tooSecurity önerisi uyarılarına abone olma.

