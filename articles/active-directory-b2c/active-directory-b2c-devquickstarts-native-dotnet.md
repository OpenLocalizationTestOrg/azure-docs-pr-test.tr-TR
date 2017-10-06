---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "Nasıl toobuild bir Windows masaüstü uygulaması, oturum açma, kaydolma içerir ve Azure Active Directory B2C kullanarak yönetim profili."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a>Azure AD B2C: bir Windows masaüstü uygulaması oluşturma
Azure Active Directory (Azure AD) B2C kullanarak kısa birkaç adımda güçlü Self Servis kimlik yönetimi özelliklerini tooyour masaüstü uygulaması ekleyebilirsiniz. Bu makale size nasıl gösterir toocreate kullanıcı kaydolma, oturum açma ve profil yönetimini kapsayan .NET Windows Presentation Foundation (WPF) "Yapılacaklar listesi" uygulama. Merhaba uygulama bir kullanıcı adı veya e-posta kullanarak kaydolma ve oturum açma için destek içerir. Facebook ve Google gibi sosyal hesaplarını kullanarak, kaydolma ve oturum açma için destek yer alacaktır.

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C dizini alma
Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.  Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır. Henüz yoksa devam etmeden önce bu kılavuzda [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).

## <a name="create-an-application"></a>Uygulama oluşturma
Ardından B2C dizininizde uygulama toocreate gerekir. Bu ihtiyaçlarını uygulamanızla toosecurely, iletişim bilgileri Azure AD'ye verir. Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md).  Şunları yaptığınızdan emin olun:

* Dahil bir **yerel istemci** hello uygulamada.
* Kopya hello **yeniden yönlendirme URI'si** `urn:ietf:wg:oauth:2.0:oob`. Bu kod örneği için hello varsayılan URL değil.
* Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama. Buna daha sonra ihtiyacınız olacak.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>İlkelerinizi oluşturma
Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır. Bu kod örneği üç kimlik deneyimi içerir: kaydolma, oturum açın ve profil düzenleme. Toocreate bir ilke açıklandığı gibi her tür için gereken [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Merhaba üç ilke oluşturduğunuzda, emin olun:

* Ya da seçin **kullanıcı kimliği kaydolma** veya **kayıt e-posta** hello kimlik sağlayıcılar dikey penceresinde.
* Kaydolma ilkenizde, **Görünen ad** ve diğer kaydolma özniteliklerini seçin.
* Her ilke için uygulamanın talep ettiği gibi **Görünen ad** ve **Nesne Kimliği** öğelerini seçin. Diğer talepleri de seçebilirsiniz.
* Kopya hello **adı** oluşturduktan sonra her ilkenin. Merhaba önekine sahip olmalıdır `b2c_1_`.  Bu ilke adlarına daha sonra ihtiyacınız olacak.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Üç ilke hello başarıyla oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.

## <a name="download-hello-code"></a>Merhaba kodu indirme
Bu öğretici için kod Hello [Github'da korunur](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet). toobuild hello örnek olarak, Git, yapabilecekleriniz [çatı projesini .zip dosyası olarak indirebilirsiniz](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip). Ayrıca hello çatıyı kopyalayabilirsiniz:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

Tamamlanan hello uygulamadır de [.zip dosyası olarak kullanılabilir](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) veya hello `complete` hello dalı aynı deposu.

Merhaba örnek kodu indirdikten sonra açık hello Visual Studio .sln dosyasını tooget başlatıldı. Merhaba `TaskClient` projedir hello kullanıcı hello WPF masaüstü uygulaması ile etkileşim kurar. Bu öğreticinin Hello amaçları doğrultusunda, arka uç görev web API'si, her kullanıcının yapılacaklar listesini depolayan Azure üzerinde barındırılan çağırır.  Toobuild hello web API gerekmez, biz zaten çalışıyor olması.

güvenli bir şekilde web API'si Azure AD B2C kullanarak istekleri doğrular nasıl toolearn kullanıma [web API Başlarken makale](active-directory-b2c-devquickstarts-api-dotnet.md).

## <a name="execute-policies"></a>İlkeleri yürütme
Uygulamanızı hello HTTP isteğinin bir parçası olarak tooexecute istedikleri hello İlkesi belirtin kimlik doğrulama iletileri göndererek Azure AD B2C ile iletişim kurar. Merhaba kullanabileceğiniz .NET Masaüstü uygulamaları için Microsoft kimlik doğrulama kitaplığı (MSAL) toosend OAuth 2.0 kimlik doğrulama iletileri önizleme, ilkeleri yürütün ve bu çağrı web API'leri belirteçleri almak.

### <a name="install-msal"></a>MSAL yükleyin
MSAL toohello ekleme `TaskClient` hello Visual Studio Paket Yöneticisi konsolu kullanarak proje.

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a>B2C bilgilerinizi girme
Açık hello dosya `Globals.cs` ve her hello özellik değerleri kendinizinkilerle değiştirin. Bu sınıf genelinde kullanılan `TaskClient` tooreference yaygın olarak kullanılan değerler.

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-hello-publicclientapplication"></a>Merhaba PublicClientApplication oluşturma
Merhaba birincil sınıf MSAL `PublicClientApplication`. Bu sınıf, uygulamanızın hello Azure AD B2C sistemde temsil eder. Merhaba uygulama initalizes oluşturduğunuzda örneği `PublicClientApplication` içinde `MainWindow.xaml.cs`. Bu hello penceresi kullanılabilir.

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a>Kaydolma akışı başlatma
Bir kullanıcı yukarı toosigns seçtiğinde tooinitiate oluşturduğunuz hello kaydolma ilkeyi kullanan bir kaydolma akışı istiyorsunuz. MSAL kullanarak, yalnızca çağırmanız `pca.AcquireTokenAsync(...)`. Merhaba çok geçirdiğiniz parametreler`AcquireTokenAsync(...)` hangi belirteci, aldığınız hello kimlik doğrulama isteği ve daha fazlasını kullanılan hello ilkesi belirleyin.

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a>Oturum açma akışını başlatmak
Merhaba bir oturum açma akışını başlatabilirsiniz aynı şekilde kaydolma akış başlatmak. Bir kullanıcı oturum açtığında aynı hello olun tooMSAL, arama, oturum açma ilkesini kullanarak bu saati:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a>Bir profili Düzenle akışı başlatma
Yeniden hello profili Düzenle İlkesi yürütebilir aynı şekilde:

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

Bu durumların tümünde, MSAL bir belirteç içine ya da döndürür `AuthenticationResult` veya bir özel durum oluşturur. MSAL belirteci Al her zaman hello kullanabilirsiniz `AuthenticationResult.User` tooupdate hello kullanıcı verilerini hello UI gibi hello uygulama nesnesi. ADAL de önbellekleri hello uygulama diğer bölümleri kullanmak için belirteç hello.

### <a name="check-for-tokens-on-app-start"></a>Uygulama başlangıç belirteçleri denetleyin
Merhaba kullanıcının oturum açma durumu MSAL tookeep izleme de kullanabilirsiniz.  Bu uygulamada hello kullanıcı tooremain bile bunlar hello uygulamasını kapatın ve yeniden açın sonra oturum istiyoruz.  Merhaba içinde geri `OnInitialized` geçersiz kılma, MSAL'ın kullanmak `AcquireTokenSilent` yöntemi toocheck önbelleğe alınmış belirteçler için:

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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
```

## <a name="call-hello-task-api"></a>Merhaba görev API çağrısı
Şimdi MSAL tooexecute ilkeleri kullanmış ve belirteçleri almak.  Toouse biri bu belirteçleri toocall hello görev API istediğinizde MSAL'ın yeniden kullanabilirsiniz `AcquireTokenSilent` yöntemi toocheck önbelleğe alınmış belirteçler için:

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

Ne zaman hello çağrısı çok`AcquireTokenSilentAsync(...)` başarılı olur ve bir belirteç bulundu hello Önbelleği'nde hello belirteci toohello ekleyebilirsiniz `Authorization` hello HTTP isteği üstbilgisi. Merhaba görev web API bu başlığı tooauthenticate hello isteği tooread hello kullanıcının yapılacaklar listesi kullanır:

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a>Out hello kullanıcı oturum açın
Son olarak, MSAL kullanabilirsiniz bir kullanıcının oturumunu hello kullanıcı seçtiğinde hello uygulamayla tooend **oturumu**.  MSAL kullanırken, bu tüm hello belirteç önbelleği hello belirteçlerinden temizleyerek gerçekleştirilir:

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a>Merhaba örnek uygulamayı çalıştırma
Son olarak, yapı ve hello örnek çalıştırın.  Bir e-posta adresi veya kullanıcı adı kullanarak Hello uygulaması için kaydolun. Oturumu kapatın ve tekrar oturum içinde hello aynı kullanıcı. Bu kullanıcının profilini düzenleyin. Oturumu kapatın ve farklı bir kullanıcı kullanarak kaydolun.

## <a name="add-social-idps"></a>Sosyal IDPs Ekle
Şu anda hello uygulama yalnızca kullanıcı kaydolma ve oturum kullanan açma destekler **yerel hesaplar**. Bunlar, bir kullanıcı adı ve parola kullanan B2C dizininizde depolanan hesaplarıdır. Azure AD B2C kullanarak kodunuzu değiştirmeden diğer kimlik sağlayıcılardan (IDPs) için destek ekleyebilirsiniz.

tooadd sosyal IDPs tooyour uygulama, izleyerek başlamak hello ayrıntılı yönergeler bu makalelerde. Her IDP için toosupport istediğiniz, bu sistemde tooregister uygulamanın gerekir ve bir istemci kimliği alın

* [Facebook bir IDP ayarlayın](active-directory-b2c-setup-fb-app.md)
* [Google bir IDP ayarlayın](active-directory-b2c-setup-goog-app.md)
* [Amazon bir IDP ayarlayın](active-directory-b2c-setup-amzn-app.md)
* [LinkedIn bir IDP ayarlayın](active-directory-b2c-setup-li-app.md)

Merhaba kimlik sağlayıcıları tooyour B2C dizini ekledikten sonra her üç ilkenizi tooinclude olarak yeni IDPs hello açıklanan hello tooedit gerek [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md). İlkelerinizi kaydettikten sonra hello uygulamayı yeniden çalıştırın. Oturum açma ve kaydolma seçenekleri her kimlik deneyimlerinizi yeni IDPs eklenen hello görmeniz gerekir.

İlkelerinizle denemeler ve örnek uygulamanızı hello etkileri gözlemleyin. Ekleyebilir veya IDPs kaldırmak, uygulamanın talep değiştirmek veya kaydolma özniteliklerini değiştirebilirsiniz. İlkeleri, kimlik doğrulama isteklerini ve MSAL nasıl birbirine bağlayan görene kadar deneyin.

Başvuru için hello tamamlandı örnek [bir .zip dosyası olarak sağlanan](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip). Aynı zamanda GitHub'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
