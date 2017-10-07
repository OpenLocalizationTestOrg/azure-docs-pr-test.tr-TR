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
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Azure AD bir Windows Masaüstü WPF uygulamanıza tümleştirmek
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Bir masaüstü uygulaması geliştiriyorsanız, Azure AD Basit ve kolay, tooauthenticate için Active Directory hesaplarını Kullanıcılarınızla kolaylaştırır.  Ayrıca, uygulama toosecurely sağlar Office 365 API'leri hello veya Azure API hello gibi tüm web Azure AD tarafından korunan API'si kullanabilir.

Korumalı tooaccess kaynakları gereken .NET yerel istemciler için Azure AD hello Active Directory kimlik doğrulama kitaplığı ya da ADAL sağlar.  ADAL'ın tek amacı hayatta toomake olduğu için uygulama tooget erişim belirteçleri kolay.  toodemonstrate olduğu, ne kadar kolay burada size bir .NET WPF Yapılacaklar listesi uygulaması, yapı:

* Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Belirtilen diğer ada sahip kullanıcılar için bir dizin arar.
* İşaretlerini kullanıcıları.

toobuild hello tam çalışan bir uygulama ihtiyacınız vardır:

1. Uygulamanızı Azure AD ile kaydedin.
2. Yükleme & ADAL yapılandırın.
3. Azure AD'den ADAL tooget belirteçleri kullanın.

başlatıldı, tooget [hello uygulama çatıyı indirmeniz](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Ayrıca, kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.  Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Merhaba DirectorySearcher uygulamayı Kaydet
tooenable önce gerekir, uygulama tooget belirteçleri tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.
3. Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.
4. Tıklayın **uygulama kayıtlar** ve **Ekle**.
5. Merhaba komut istemlerini izleyin ve yeni bir **yerel istemci uygulaması**.
  * Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın anlatmaktadır
  * Merhaba **yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanacağını düzeni ve dize birleşimidir.  Örneğin bir değer belirli tooyour uygulama girin `http://DirectorySearcher`.
6. Kayıt tamamladıktan sonra AAD uygulamanızı benzersiz bir uygulama kimliği atar.  Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sayfadan kopyalayın.
7. Merhaba gelen **ayarları** sayfasında, **gerekli izinler** ve **Ekle**. Select hello **Microsoft Graph** olarak API hello ve hello ekleyin **dizin verilerini okuma** altında izni **izinlere temsilci**.  Bu, kullanıcılar için uygulama tooquery hello grafik API'si olanak tanır.

## <a name="2-install--configure-adal"></a>2. Yükleme & ADAL yapılandırın
Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.  Azure AD ile mümkün toocommunicate ADAL toobe için sırayla tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.

* Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher proje ekleyerek başlayın.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Merhaba DirectorySearcher projeyi açın `app.config`.  Merhaba hello öğelerin Hello değerleri değiştirmek `<appSettings>` bölüm tooreflect hello hello Azure Portal giriş değerleri.  ADAL kullandığında kodunuzu bu değerleri başvurur.
  * Merhaba `ida:Tenant` Azure AD kiracınız, ör. contoso.onmicrosoft.com hello etki alanıdır
  * Merhaba `ida:ClientId` hello ClientID hello portalından kopyaladığınız uygulamanızın olduğu.
  * Merhaba `ida:RedirectUri` hello olan yeniden yönlendirme URL'si hello Portalı'nda kayıtlı.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    AAD gelen ADAL tooGet belirteçleri kullanın
Merhaba temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, onu yalnızca çağırdığı ilkesidir `authContext.AcquireTokenAsync(...)`, ve ADAL rest hello.  

* Merhaba, `DirectorySearcher` proje, açık `MainWindow.xaml.cs` ve hello bulun `MainWindow()` yöntemi.  Merhaba ilk adım, uygulamanızın tooinitialize olan `AuthenticationContext` -birincil sınıfı ADAL.  ADAL burada geçirdiğiniz budur hello Azure AD ile toocommunicate gereken koordinatları ve nasıl söyleyin toocache belirteçleri.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Şimdi hello bulun `Search(...)` hello kullanıcı cliks "Ara" düğmesini hello uygulamanın kullanıcı arabiriminde hello olduğunda çağrılacak yöntem.  Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir GET isteği toohello Azure AD Graph API tooquery sağlar.  Ancak sipariş tooquery hello grafik API'si, tooinclude bir access_token ile Merhaba gerekir `Authorization` hello üstbilgisinin isteği - ADAL nereden geldiğini budur.

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
* Uygulamanızı isteğinde bulunduğunda bir belirteç çağırarak `AcquireTokenAsync(...)`, ADAL hello kullanıcı kimlik bilgilerinin sorulmasına olmadan tooreturn bir belirteç deneyecek.  ADAL tooget bir belirteç toosign hello kullanıcı gerektiğini belirlerse, bir oturum açma iletişim kutusu görüntüler, hello kullanıcının kimlik bilgilerini toplamak ve başarılı bir kimlik doğrulaması sırasında bir simge döndürür.  ADAL herhangi bir nedenle yüklenemiyor tooreturn bir belirteç ise, throw bir `AdalException`.
* Bu hello fark `AuthenticationResult` nesnesini içeren bir `UserInfo` uygulamanız gerekebilir kullanılan toocollect bilgi olabilir nesnesi.  Merhaba DirectorySearcher, içinde `UserInfo` kullanılan toocustomize hello uygulamanın UI hello kullanıcının kimliği.
* Merhaba kullanıcı hello "Oturumu Kapat" düğmesini tıklattığında, sonraki çağrı çok hello tooensure istiyoruz`AcquireTokenAsync(...)` hello kullanıcı toosign sorar.  ADAL ile bu hello belirteç önbelleği temizleme olarak kadar kolaydır:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* Ancak, Hello kullanıcı hello "Oturumu Kapat" düğmesini tıklatın değil, bunlar hello DirectorySearcher sonraki çalıştırmanızda toomaintain hello kullanıcının oturumunu hello için isteyeceksiniz.  Merhaba uygulama başlattığında, varolan bir belirteci için ADAL'ın belirteç önbelleği denetleyin ve hello kullanıcı Arabirimi gerektiği gibi güncelleştirin.  Merhaba, `CheckForCachedToken()` yöntemi, başka bir çok çağırmaya`AcquireTokenAsync(...)`, bu kez hello geçirme `PromptBehavior.Never` parametresi.  `PromptBehavior.Never`ADAL hello kullanıcı oturum açma için sorulması değil ve oluşturamıyor tooreturn ise ADAL bunun yerine bir özel durum bir belirteç oluşturması gerekir söyler.

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

Tebrikler! Artık çalışan bir hello özelliği tooauthenticate kullanıcılara .NET WPF uygulaması sahip, güvenli bir şekilde OAuth 2.0 kullanan Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri alın.  Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.  DirectorySearcher uygulamanızı çalıştırın ve bu kullanıcıların biri oturum oturum.  Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.  Merhaba uygulamasını kapatın ve yeniden çalıştırın.  Merhaba kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.  Oturumu kapatın ve başka bir kullanıcı olarak yeniden oturum açın.

ADAL kolay tooincorporate kılar uygulamanıza bu ortak kimlik özelliklerin tümü.  Bu tüm hello dirty iş, - önbellek yönetimi, OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme hello kullanıcı sunmak için mvc'deki.  Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `authContext.AcquireTokenAsync(...)`.

Başvuru için tamamlandı hello örnek (yapılandırma değerleriniz olmadan) sağlanır [burada](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Şimdi tooadditional senaryoları taşıyabilirsiniz.  Tootry isteyebilirsiniz:

[.NET Web API'si Azure AD ile güvenli >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

