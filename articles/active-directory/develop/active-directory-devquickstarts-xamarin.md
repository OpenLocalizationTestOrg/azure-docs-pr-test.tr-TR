---
title: "aaaAzure AD Başlarken Xamarin | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleştirilebilen ve OAuth kullanan Azure AD korumalı API'leri çağırmak Xamarin uygulamaları oluşturun."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Azure AD Xamarin uygulamaları ile tümleştirme
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Xamarin ile C# ' ta, iOS, Android ve Windows (mobil cihazları ve bilgisayarları) üzerinde çalışan mobil uygulamalar yazabilirsiniz. Azure Active Directory (Azure AD) Xamarin kullanarak bir uygulama oluşturuyorsanız, Azure AD hesaplarına sahip basit tooauthenticate kullanıcılar kolaylaştırır. Merhaba uygulama de güvenli bir şekilde hello Office 365 API'leri veya hello Azure API gibi Azure AD tarafından korunan tüm web API'si kullanabilir.

Korumalı tooaccess kaynaklara gereksinim Xamarin uygulamaları için Azure AD hello Active Directory Authentication Library (ADAL) sağlar. ADAL tek amacı Hello toomake bu uygulamaları tooget erişim belirteçleri için kolay. toodemonstrate olduğu, bu makalede gösterilmektedir ne kadar kolay nasıl toobuild DirectorySearcher uygulamalar:

* İOS, Android, Windows Masaüstü, Windows Phone ve Windows Mağazası'nı çalıştırın.
* Tek taşınabilir sınıf kitaplığı (PCL) tooauthenticate kullanıcıları ve belirteçleri hello Azure AD Graph API alın.
* Verilen UPN olan kullanıcılar için bir dizini arayın.

## <a name="before-you-get-started"></a>Başlamadan önce
* Merhaba karşıdan [çatı projesini](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), veya hello indirme [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Her yükleme Visual Studio 2013 çözümüdür.
* Ayrıca hangi toocreate kullanıcıları ve kayıt hello uygulama Azure AD kiracısı gerekir. Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

Hazır olduğunuzda İleri dört bölüm izleyin hello yordamlarda hello.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>1. adım: Xamarin geliştirme ortamınızı ayarlayın
Bu öğretici iOS, Android ve Windows için projeleri içerdiğinden, Visual Studio ve Xamarin gerekir. toocreate hello gerekli ortam, tam hello işleminde [ayarlamak ayarlama ve Visual Studio ve Xamarin yükleme](https://msdn.microsoft.com/library/mt613162.aspx) MSDN'de. Tamamlanan hello yüklemeleri toobe için beklerken toolearn Xamarin hakkında daha fazla gözden geçirebilirsiniz malzemesi Hello yönergeler içerir.

Merhaba kurulumu tamamladıktan sonra hello çözümü Visual Studio'da açın. Burada, altı projeleri bulacaksınız: beş platforma özel Proje ve bir PCL, tüm platformlarda paylaşılan DirectorySearcher.cs.

## <a name="step-2-register-hello-directorysearcher-app"></a>2. adım: Kayıt hello DirectorySearcher uygulama
tooenable hello uygulama tooget belirteçleri, ilk ihtiyacınız tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin. Bunu yapmak için:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst çubuğunda hesabınızı tıklatın. Ardından, hello altında **dizin** listesi, tooregister hello uygulama istediğiniz select hello Active Directory kiracısı.
3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Yeni bir toocreate **yerel istemci uygulaması**, hello istemleri izleyin.
  * **Ad** hello uygulama toousers açıklar.
  * **Yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanan bir şema ve dize birleşimidir. Bir değer (örneğin, http://DirectorySearcher) girin.
6. Kayıt tamamladıktan sonra Azure AD hello uygulama benzersiz uygulama kimliği atar. Hello Hello değerini kopyalayın **uygulama** sekmesinde, çünkü daha sonra ihtiyacınız olacak.
7. Merhaba üzerinde **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.
8. Seçin **Microsoft Graph** API hello gibi. Altında **izinlere temsilci**, hello eklemek **dizin verilerini okuma** izni.  
Bu eylem, kullanıcılar için hello uygulama tooquery hello grafik API'si sağlar.

## <a name="step-3-install-and-configure-adal"></a>3. adım: Yükleme ve ADAL yapılandırma
Azure AD'de bir uygulamaya sahip olduğunuza göre ADAL yükleyin ve kimlikle ilgili kodunuzu yazın. Azure AD ile tooenable ADAL toocommunicate hello uygulama kaydı hakkında bazı bilgiler verir.

1. Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher projesi ekleyin.

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    İki kitaplığı başvuru tooeach proje eklenen Not: hello PCL kısmı ADAL ve platforma özgü bölümü.
2. Merhaba DirectorySearcherLib projesinde DirectorySearcher.cs açın.
3. Merhaba sınıf üye değerlerinin hello Azure portal girdiğiniz hello değerlerle değiştirin. ADAL kullandığında kodunuzu toothese değerleri gösterir.

  * Merhaba *Kiracı* Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) hello etki alanıdır.
  * Merhaba *ClientID* hello portalından kopyalandığından hello uygulama hello istemci kimliği.
  * Merhaba *returnUri* hello yeniden yönlendirme (örneğin, http://DirectorySearcher) hello portalda girdiğiniz URI'si değil.

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>4. adım: Azure AD ADAL tooget belirteçlerinden kullanın
Neredeyse tüm hello uygulamanın kimlik doğrulaması mantığı arasındadır `DirectorySearcher.SearchByAlias(...)`. Merhaba platforma özgü projelerinde gerekli olan tek şey toopass bağlamsal parametresi toohello `DirectorySearcher` PCL.

1. DirectorySearcher.cs açın ve ardından yeni bir parametre toohello ekleyin `SearchByAlias(...)` yöntemi. `IPlatformParameters`ADAL gereksinimlerini tooperform hello kimlik doğrulamanın hello platforma özgü yalıtan hello bağlamsal parametre nesneleri olur.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Initialize `AuthenticationContext`, ADAL birincil sınıfının hello olduğu.  
Bu eylem geçiş ADAL hello Azure AD ile gereksinimlerini toocommunicate düzenler.
3. Çağrı `AcquireTokenAsync(...)`, hello kabul `IPlatformParameters` nesne ve gerekli tooreturn bir belirteç toohello uygulaması olan hello kimlik doğrulaması akışı çağırır.

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    `AcquireTokenAsync(...)`ilk deneme tooreturn hello için bir belirteç (aracılığıyla, önbelleğe alma veya eski belirteçleri yenileme) kimlik bilgilerini kullanıcılar tooenter sormadan istenen kaynak (Merhaba grafik API'si bu durumda). Gerekirse, bu kullanıcıların hello Azure AD oturum açma sayfası hello istenen belirtecini alma önce gösterir.
4. Merhaba erişim belirteci toohello grafik API'si hello istekte attach **yetkilendirme** üstbilgisi:

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

Tüm olan hello için `DirectorySearcher` PCL ve hello uygulamanın kimlikle ilgili kod. Kalan tek şey toocall hello `SearchByAlias(...)` yöntemi her platformun görünümlerinde ve gerektiğinde, doğru bir şekilde işlemek için tooadd kodu hello UI yaşam döngüsü.

### <a name="android"></a>Android
1. MainActivity.cs içinde çok bir çağrı ekleyin`SearchByAlias(...)` işleyici hello düğmesini tıklatın:

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Merhaba geçersiz kılma `OnActivityResult` yaşam döngüsü yöntemi tooforward geri toohello uygun yöntemi herhangi bir kimlik doğrulaması yönlendirir. ADAL yardımcı yöntem bu Android sağlar:

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Windows Masaüstü
MainWindow.xaml.cs içinde çok çağırmaya`SearchByAlias(...)` geçirerek bir `WindowInteropHelper` hello masaüstünün içinde `PlatformParameters` nesnesi:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
İOS DirSearchClient_iOSViewController.cs içinde hello `PlatformParameters` nesne başvurusu toohello View Controller alır:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Evrensel
Windows Evrensel MainPage.xaml.cs açın ve ardından hello uygulamak `Search` yöntemi. Bu yöntem gerektiği gibi paylaşılan bir proje tooupdate UI yardımcı bir yöntem kullanır.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>Sırada ne var?
Artık çalışan bir, kullanıcıların kimliğini doğrulamak ve güvenli bir şekilde beş farklı platformlarda OAuth 2.0 kullanarak web API çağırma Xamarin uygulaması sahipsiniz.

Kiracı kullanıcılarla zaten doldurulmuş yapmadıysanız, başlangıç saati toodo şekilde sunulmuştur.

1. DirectorySearcher uygulamanızı çalıştırın ve ardından hello kullanıcılardan birine oturum açın.
2. Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.

ADAL hello uygulamaya kolay tooincorporate ortak kimlik özelliklerinin kolaylaştırır. Bunu tüm hello dirty çalışmanın sizin için önbellek yönetimi gibi OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, hello kullanıcı sunan mvc'deki ve yenileme belirteçleri süresi. Tooknow yalnızca tek bir API çağrısı gereksinim `authContext.AcquireToken*(…)`.

Merhaba başvuru için karşıdan [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (yapılandırma değerleriniz olmadan).

Şimdi tooadditional kimlik senaryoları taşıyabilirsiniz. Örneğin, [Azure AD ile .NET Web API'si güvenli](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
