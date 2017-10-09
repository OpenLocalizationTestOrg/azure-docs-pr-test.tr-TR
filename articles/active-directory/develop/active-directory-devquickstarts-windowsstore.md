---
title: "aaaAzure AD Windows Mağazası'ı kullanmaya başlama | Microsoft Docs"
description: "Oturum açma için Azure AD ile tümleştirme, Azure AD çağıran derleme Windows mağazası uygulamaları API'leri OAuth kullanan korumalı."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Azure AD Windows mağazası uygulamaları ile tümleştirme
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Windows mağazası 8.1 ve önceki sürümü projeleri Visual Studio 2017 desteklenmez.  Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

Merhaba Windows mağazası için uygulama geliştiriyorsanız, Azure Active Directory (Azure AD), basit ve kolay tooauthenticate kolaylaştırır, Active Directory hesaplarını Kullanıcılarınızla. Bir uygulama, Azure AD ile tümleştirerek, güvenli bir şekilde tüm web hello Office 365 API'leri veya hello Azure API gibi Azure AD tarafından korunan API'si kullanabilir.

Korumalı tooaccess kaynakları gereken Windows mağazası Masaüstü uygulamaları için Azure AD hello Active Directory Authentication Library (ADAL) sağlar. Merhaba tek amacı, ADAL olan toomake hello uygulama tooget erişim belirteçleri için kolay. toodemonstrate olduğu, bu makalede gösterilmektedir nasıl toobuild bir DirectorySearcher Windows mağazası ne kadar kolay uygulama:

* Alır erişim belirteçleri hello kullanarak hello Azure AD Graph API çağırma [OAuth 2.0 kimlik doğrulama protokolü](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Sağlanan kullanıcı asıl adı (UPN) sahip kullanıcılar için bir dizin arar.
* İşaretlerini kullanıcıları.

## <a name="before-you-get-started"></a>Başlamadan önce
* Merhaba karşıdan [çatı projesini](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), veya hello indirme [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Her yükleme Visual Studio 2015 çözümüdür.
* Ayrıca hangi toocreate kullanıcıları ve kayıt hello uygulama Azure AD kiracısı gerekir. Bir kiracı yoksa [öğrenin nasıl tooget bir](active-directory-howto-tenant.md).

Hazır olduğunuzda izleyin hello yordamlarda sonraki üç bölümde hello.

## <a name="step-1-register-hello-directorysearcher-app"></a>1. adım: Kayıt hello DirectorySearcher uygulama
tooenable hello uygulama tooget belirteçleri, ilk ihtiyacınız tooregister bunu Azure ad Kiracı ve izni tooaccess hello Azure AD Graph API verin. Bunu yapmak için:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Merhaba üst çubuğunda hesabınızı tıklatın. Ardından, hello altında **dizin** listesi, tooregister hello uygulama istediğiniz select hello Active Directory kiracısı.
3. Tıklatın **daha Hizmetleri** hello sol bölmesinde ve ardından **Azure Active Directory**.
4. Tıklatın **uygulama kayıtlar**ve ardından **Ekle**.
5. Merhaba istemleri toocreate izleyin bir **yerel istemci uygulaması**.
  * **Ad** hello uygulama toousers açıklar.
  * **Yeniden yönlendirme URI'si** Azure AD tooreturn belirteci yanıtları kullanan bir şema ve dize birleşimidir. Şu an için bir yer tutucu değerini girin (örneğin, **http://DirectorySearcher**). Merhaba değer daha sonra değiştirirsiniz.
6. Merhaba kaydı tamamladıktan sonra Azure AD hello uygulama benzersiz uygulama kimliği atar. Merhaba Hello değerini kopyalayın **uygulama** sekmesinde, çünkü daha sonra ihtiyacınız olacak.
7. Merhaba üzerinde **ayarları** sayfasında, **gerekli izinler**ve ardından **Ekle**.
8. Hello için **Azure Active Directory** uygulama, select **Microsoft Graph** API hello gibi.
9. Altında **izinlere temsilci**, hello eklemek **erişim hello dizini hello oturum açmış kullanıcı olarak** izni. Bunun yapılması, kullanıcılar için hello uygulama tooquery hello grafik API'si sağlar.

## <a name="step-2-install-and-configure-adal"></a>2. adım: Yükleme ve ADAL yapılandırma
Azure AD'de bir uygulamaya sahip olduğunuza göre ADAL yükleyin ve kimlikle ilgili kodunuzu yazın. Azure AD ile tooenable ADAL toocommunicate hello uygulama kaydı hakkında bazı bilgiler verir.

1. Merhaba Paket Yöneticisi konsolu kullanarak ADAL toohello DirectorySearcher projesi ekleyin.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. Merhaba DirectorySearcher projesinde MainPage.xaml.cs açın.
3. Hello başlangıç değerleri değiştirin **yapılandırma değerleri** bölge hello Azure portal girdiğiniz hello değerlere sahip. ADAL kullandığında kodunuzu toothese değerleri gösterir.
  * Merhaba *Kiracı* Azure AD kiracınız (örneğin, contoso.onmicrosoft.com) hello etki alanıdır.
  * Merhaba *ClientID* hello portalından kopyalandığından hello uygulama hello istemci kimliği.
4. Artık Windows mağazası uygulamanız için toodiscover hello geri çağırma URI gerekir. Merhaba bu satırında bir kesme noktası belirleyerek `MainPage` yöntemi:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Tüm başvuruları paket emin yapı hello çözüm geri yüklenir. Herhangi bir paket eksikse hello NuGet Paket Yöneticisi'ni açın ve bunları geri yükleyin.
6. Merhaba uygulamayı çalıştırın ve kopyalama hello değerini `redirectUri` zaman hello kesme noktası isabet. Merhaba değeri hello aşağıdaki gibi görünmelidir:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. Merhaba üzerinde geri **ayarları** hello Azure portal hello uygulamada sekme ekleme bir **RedirectUri** değeri önceki hello ile.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>3. adım: Azure AD ADAL tooget belirteçlerinden kullanın
Merhaba temel ADAL arkasında hello uygulamanın bir erişim belirteci ihtiyacı olduğunda, onu yalnızca çağırdığı ilkesidir `authContext.AcquireToken(…)`, ve ADAL rest hello.  

1. Merhaba uygulamanın başlatma `AuthenticationContext`, ADAL birincil sınıfının hello olduğu. Bu eylem Azure AD ile toocommunicate gerekir ve nasıl söyleyin ADAL hello koordinatları geçirir toocache belirteçleri.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Merhaba bulun `Search(...)` hello kullanıcılar'ı tıklattığınızda, çağrılan yöntemi **arama** hello uygulamanın UI düğmesinde. Bu yöntem, UPN arama terimi verilen hello kullanıcıları bir get isteği toohello Azure AD Graph API tooquery sağlar. tooquery hello grafik API'si içeren bir erişim belirteci hello isteğin içinde **yetkilendirme** üstbilgi. ADAL nereden geldiğini budur.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    Merhaba uygulama isteğinde bulunduğunda bir belirteç çağırarak `AcquireTokenAsync(...)`, ADAL tooreturn bir belirteç hello kullanıcı kimlik bilgilerinin sorulmasına olmadan çalışır. ADAL tooget bir belirteç toosign hello kullanıcı gerektiğini belirlerse, bir oturum açma iletişim kutusu görüntüler, hello kullanıcının kimlik bilgilerini toplar ve kimlik doğrulaması başarılı olduktan sonra bir belirteç döndürür. ADAL herhangi bir nedenle yüklenemiyor tooreturn bir belirteç ise, hello *yazılımdan AuthenticationResult* bir hata durumudur.
3. Bu zaman toouse hello erişim belirteci almış sunulmuştur. Merhaba, ayrıca `Search(...)` yöntemi, grafik API'si get isteği hello hello belirteci toohello ekleme **yetkilendirme** üstbilgisi:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. Merhaba kullanabilirsiniz `AuthenticationResult` nesne hello kullanıcının kimliği gibi hello uygulama hello kullanıcı hakkında toodisplay bilgi:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. ADAL toosign kullanıcılar hello uygulama dışında de kullanabilirsiniz. Merhaba kullanıcı hello tıkladığında **oturum kapatma** düğmesini tıklatın, bu hello sonraki çağrı çok olun`AcquireTokenAsync(...)` bir oturum açma görünümü gösterir. ADAL ile bu eylemin hello belirteç önbelleği temizleme olarak kadar kolaydır:

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>Sırada ne var?
Artık çalışan bir kullanıcıların kimlik doğrulaması, güvenli bir şekilde web OAuth 2.0 kullanan API'leri çağırmak ve hello kullanıcı hakkındaki temel bilgileri elde Windows mağazası uygulaması sahipsiniz.

Kiracı kullanıcılarla zaten doldurulmuş yapmadıysanız, başlangıç saati toodo şekilde sunulmuştur.
1. DirectorySearcher uygulamanızı çalıştırın ve ardından hello kullanıcılardan birine oturum açın.
2. Diğer kullanıcıların UPN Değerlerinin üzerinde göre arayın.
3. Merhaba uygulamasını kapatın ve onu yeniden çalıştırın. Merhaba kullanıcının oturumunu nasıl olduğu gibi kalır dikkat edin.
4. Toodisplay hello alt çubuğu sağ tıklayarak oturumu kapatın ve ardından başka bir kullanıcı olarak yeniden oturum açın.

ADAL kolay tooincorporate kılar tüm bu ortak kimlik özellikler hello uygulamada. Bunu tüm hello dirty çalışmanın sizin için önbellek yönetimi gibi OAuth protokol desteği, bir oturum açma kullanıcı Arabirimi, hello kullanıcı sunan mvc'deki ve yenileme belirteçleri süresi. Tooknow yalnızca tek bir API çağrısı gereksinim `authContext.AcquireToken*(…)`.

Merhaba başvuru için karşıdan [tamamlanan örnek](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (yapılandırma değerleriniz olmadan).

Şimdi tooadditional kimlik senaryoları taşıyabilirsiniz. Örneğin, [Azure AD ile .NET Web API'si güvenli](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
