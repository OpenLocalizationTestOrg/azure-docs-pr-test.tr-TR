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
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Azure AD ile Windows Phone Uygulama Tümleştirme
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Windows Phone 8.1 ve önceki sürümlerde oluşturulmuş projeler Visual Studio 2017’de desteklenmez.  Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Windows Phone 8.1 uygulama geliştiriyorsanız, Azure AD Basit ve kolay, tooauthenticate için Active Directory hesaplarını Kullanıcılarınızla kolaylaştırır.  Ayrıca, uygulama toosecurely sağlar Office 365 API'leri hello veya Azure API hello gibi tüm web Azure AD tarafından korunan API'si kullanabilir.

> [!NOTE]
> Bu kod örneği, ADAL v2.0 kullanır.  Merhaba son teknoloji tooinstead deneyin isteyebilirsiniz bizim [ADAL v3.0 kullanarak Windows Evrensel Öğreticisine](active-directory-devquickstarts-windowsstore.md).  Windows Phone 8.1 için gerçekten bir uygulama geliştiriyorsanız, hello doğru yerde budur.  ADAL v2.0 hala tam olarak desteklenir ve hello önerilen yol geliştirme uygulamaları agianst Windows Phone 8.1, Azure AD kullanıyor.
> 
> 

Korumalı tooaccess kaynakları gereken .NET yerel istemciler için Azure AD hello Active Directory kimlik doğrulama kitaplığı ya da ADAL sağlar.  ADAL'ın tek amacı hayatta toomake olduğu için uygulama tooget erişim belirteçleri kolay.  toodemonstrate olduğu, ne kadar kolay burada size bir "Directory noktasıdır" Windows Phone 8.1 uygulama, yapı:

* Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Verilen UPN olan kullanıcılar için bir dizin arar.
* İşaretlerini kullanıcıları.

toobuild hello tam çalışan bir uygulama ihtiyacınız vardır:

1. Uygulamanızı Azure AD ile kaydedin.
2. Yükleme & ADAL yapılandırın.
3. Azure AD'den ADAL tooget belirteçleri kullanın.

başlatıldı, tooget [bir çatı projesini indirin](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) veya [tamamlandı hello örnek indirme](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Her bir Visual Studio 2013 çözümüdür.  Ayrıca, kullanıcı oluşturma ve bir uygulamayı kaydetme Azure AD kiracısı gerekir.  Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. YAZMAÇ hello Directory noktasıdır uygulama
tooenable önce gerekir, uygulama tooget belirteçleri tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Hesabınızda ve hello altında Hello üst çubuğunda tıklatın **Directory** listesinde, burada istediğiniz tooregister uygulamanızı hello Active Directory Kiracı seçin.
3. Tıklayın **daha Hizmetleri** sol taraftaki gezinti hello ve seçin **Azure Active Directory**.
4. Tıklayın **uygulama kayıtlar** ve **Ekle**.
5. Merhaba komut istemlerini izleyin ve yeni bir **yerel istemci uygulaması**.
  * Merhaba **adı** Merhaba uygulama, uygulama tooend kullanıcılarınızın anlatmaktadır
  * Merhaba **yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanacağını düzeni ve dize birleşimidir.  Şimdilik, örneğin bir yer tutucu değerini girin `http://DirectorySearcher`.  Biz bu değer daha sonra değiştirirsiniz.
6. Kayıt tamamladıktan sonra AAD uygulamanızı benzersiz bir uygulama kimliği atar.  Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sekmesinden kopyalayın.
7. Merhaba gelen **ayarları** sayfasında, **gerekli izinler** ve **Ekle**. Select hello **Microsoft Graph** olarak API hello ve hello ekleyin **dizin verilerini okuma** altında izni **izinlere temsilci**.  Bu, kullanıcılar için uygulama tooquery hello grafik API'si olanak tanır.

## <a name="2-install--configure-adal"></a>2. Yükleme & ADAL yapılandırın
Azure AD'de bir uygulamanız varsa, ADAL yükleyin ve kimlikle ilgili kodunuzu yazın.  Azure AD ile mümkün toocommunicate ADAL toobe için sırayla tooprovide gereken uygulama kaydınızı hakkında bazı bilgiler ile.

* Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher proje ekleyerek başlayın.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* Merhaba DirectorySearcher projeyi açın `MainPage.xaml.cs`.  Hello başlangıç değerleri değiştirin `Config Values` bölge tooreflect hello hello Azure Portal giriş değerleri.  ADAL kullandığında kodunuzu bu değerleri başvurur.
  * Merhaba `tenant` Azure AD kiracınız, ör. contoso.onmicrosoft.com hello etki alanıdır
  * Merhaba `clientId` hello ClientID hello portalından kopyaladığınız uygulamanızın olduğu.
* Artık Windows Phone uygulamanız için toodiscover hello geri çağırma URI gerekir.  Merhaba bu satırında bir kesme noktası belirleyerek `MainPage` yöntemi:

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Merhaba uygulamayı çalıştırın ve kenara hello değerini kopyalayın `redirectUri` zaman hello kesme noktası isabet.  Aşağıdakine benzer görünmelidir

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* Merhaba üzerinde geri **yapılandırma** hello Azure Yönetim Portalı, uygulamanızda sekmesinde hello hello değerini değiştirin **RedirectUri** bu değere sahip.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. AAD gelen ADAL tooGet belirteçleri kullanın
Merhaba temel ADAL arkasında uygulamanızı bir erişim belirteci her gerektiğinde, onu yalnızca çağırdığı ilkesidir `authContext.AcquireToken(…)`, ve ADAL rest hello.  

* Merhaba ilk adım, uygulamanızın tooinitialize olan `AuthenticationContext` -birincil sınıfı ADAL.  ADAL burada geçirdiğiniz budur hello Azure AD ile toocommunicate gereken koordinatları ve nasıl söyleyin toocache belirteçleri.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Şimdi hello bulun `Search(...)` hello kullanıcı cliks "Ara" düğmesini hello uygulamanın kullanıcı arabiriminde hello olduğunda çağrılacak yöntem.  Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir GET isteği toohello Azure AD Graph API tooquery sağlar.  Ancak sipariş tooquery hello grafik API'si, tooinclude bir access_token ile Merhaba gerekir `Authorization` hello üstbilgisinin isteği - ADAL nereden geldiğini budur.

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
* Etkileşimli kimlik doğrulaması gerekli olduğunda, ADAL Windows Phone ' ın Web kimlik doğrulama Aracısı (WAB) kullanır ve [devamlılık modeli](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sayfasında oturum açın.  Merhaba kullanıcı oturum açtığında uygulamanızın toopass ADAL hello hello WAB etkileşim sonuçlarını gerekir.  Bu hello uygulama olarak kadar basittir `ContinueWebAuthentication` arabirimi:

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

* Zaman toouse hello şimdi `AuthenticationResult` bu ADAL tooyour uygulama döndürdü.  Merhaba, `QueryGraph(...)` geri toohello GET isteğini hello yetkilendirme üst bilgisinde aldığınız hello access_token ekleyin:

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
* Merhaba de kullanabilirsiniz `AuthenticationResult` nesne uygulamanızda hello kullanıcı hakkında toodisplay bilgi. Merhaba, `QueryGraph(...)` yöntemi, kullanım hello sonuç tooshow hello kullanıcının kimliğini hello sayfasında:

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Son olarak, ADAL toosign hello kullanıcı dışında uygulama da kullanabilirsiniz.  Merhaba kullanıcı hello "Oturumu Kapat" düğmesini tıklattığında, sonraki çağrı çok hello tooensure istiyoruz`AcquireTokenSilentAsync(...)` başarısız olur.  ADAL ile bu hello belirteç önbelleği temizleme olarak kadar kolaydır:

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Tebrikler! Artık çalışan bir hello özelliği tooauthenticate kullanıcılar Windows Phone Uygulama sahip, güvenli bir şekilde OAuth 2.0 kullanan Web API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri alın.  Henüz yapmadıysanız, başlangıç saati toopopulate kiracınız bazı kullanıcılar ile sunulmuştur.  DirectorySearcher uygulamanızı çalıştırın ve bu kullanıcıların biri oturum oturum.  Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.  Merhaba uygulamasını kapatın ve yeniden çalıştırın.  Merhaba kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.  Oturumu kapatın ve başka bir kullanıcı olarak yeniden oturum açın.

ADAL kolay tooincorporate kılar uygulamanıza bu ortak kimlik özelliklerin tümü.  Bu tüm hello dirty iş, - önbellek yönetimi, OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, belirteçlerin süresinin ve daha fazlasını yenileme hello kullanıcı sunmak için mvc'deki.  Tüm tooknow gerçekten ihtiyacınız olan tek bir API çağrısı `authContext.AcquireToken*(…)`.

Başvuru için tamamlandı hello örnek (yapılandırma değerleriniz olmadan) sağlanır [burada](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Şimdi tooadditional kimlik senaryoları taşıyabilirsiniz.  Tootry isteyebilirsiniz:

[.NET Web API'si Azure AD ile güvenli >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

