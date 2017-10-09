---
title: "Azure Active Directory B2C: Özel ilkelerini kullanma OAuth2 kimlik sağlayıcısı Google + Ekle"
description: "Örnek Google + OAuth2 protokolünü kullanarak kimlik sağlayıcısı kullanma"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Özel ilkelerini kullanma OAuth2 kimlik sağlayıcısı Google + Ekle

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu kılavuz size nasıl tooenable oturum açma için Google + hello kullanımını hesabıyla kullanıcılardan gösterir [özel ilkeler](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Ön koşullar

Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.

Bu adımlar şunları içerir:

1.  Google + hesabı uygulaması oluşturuluyor.
2.  Merhaba Google + hesap uygulama anahtar tooAzure AD B2C ekleme
3.  Talep sağlayıcı tooa ilkesi ekleme
4.  Merhaba Google + hesap talep sağlayıcısı tooa kullanıcı gezisine kaydetme
5.  Kiracı Hello İlkesi tooan Azure AD B2C karşıya yükleme ve test

## <a name="create-a-google-account-application"></a>Google + hesabı uygulaması oluşturma
toouse Google + Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Google + uygulama gerekir ve hello doğru parametrelerle sağlayın. Bir Google + uygulama burada kaydedebilirsiniz: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)

1.  Toohello Git [Google geliştiriciler konsol](https://console.developers.google.com/) ve Google + hesabı kimlik bilgilerinizle oturum açın.
2.  Tıklatın **proje oluştur**, girin bir **proje adı**ve ardından **oluşturma**.

3.  Tıklatın hello üzerinde **projeleri menü**.

    ![Google + hesabı - proje'yi seçin](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  Tıklatın hello üzerinde  **+**  düğmesi.

    ![Google + hesap - yeni proje oluşturma](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  Girin bir **proje adı**ve ardından **oluşturma**.

    ![Google + hesabı - yeni proje](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  Hello proje hazır olana kadar bekleyin ve hello üzerinde tıklatın **projeleri menü**.

    ![Google + hesabı - yeni proje hazır toouse olana kadar bekleyin](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  Proje adına tıklayın.

    ![Google + hesabı - Select hello yeni proje](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  Tıklatın **API Yöneticisi** ve ardından **kimlik bilgileri** sol gezinti hello içinde.
9.  Merhaba tıklatın **OAuth izni ekran** sekmesini hello üstünde.

    ![Google + hesabı - ayarlamak OAuth onay ekranı](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  Seçin veya geçerli bir belirtin **e-posta adresi**, sağlayan bir **ürün adı**, tıklatıp **kaydetmek**.

    ![Google + - uygulama kimlik bilgileri](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  Tıklatın **yeni kimlik bilgileri** ve ardından **OAuth istemci kimliği**.

    ![Google + - yeni uygulama kimlik bilgileri oluşturun](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  Altında **uygulama türü**seçin **Web uygulaması**.

    ![Google + - uygulama türünü seçme](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  Sağlamak bir **adı** , uygulamanız için girin `https://login.microsoftonline.com` hello içinde **yetkili JavaScript çıkış** alan, ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yetkili URI'leryenidenyönlendirme**alan. Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com). Merhaba **{tenant}** duyarlıdır. **Oluştur**'a tıklayın.

    ![Google + - yetkili JavaScript çıkış sağlayın ve URI'ler yeniden yönlendirme](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  Merhaba değerlerini kopyalamayı **istemci kimliği** ve **gizli**. Her iki tooconfigure Google + kimlik sağlayıcısı olarak kiracınızda gerekir. **İstemci parolası** önemli güvenlik kimlik bilgileri.

    ![Google + - istemci kimliği ve istemci gizli kopya hello değerleri](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a>Merhaba Google + hesap uygulama anahtar tooAzure AD B2C ekleme
Google + hesaplarıyla Federasyon istemci parolasını Google + hesap tootrust için Azure AD B2C hello uygulama adına gerektirir. Azure AD B2C kiracısı içinde Google + uygulama gizli toostore gerekir:  

1.  Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework**
2.  Seçin **İlkesi anahtarları** tooview hello anahtarları kiracınızda kullanılabilir.
3.  Tıklatın **+ Ekle**.
4.  İçin **seçenekleri**, kullanın **el ile**.
5.  İçin **adı**, kullanmak `GoogleSecret`.  
    Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.
6.  Merhaba, **gizli** kutusuna, https://apps.dev.microsoft.com Microsoft uygulama gizli anahtarı girin
7.  İçin **anahtar kullanımı**, kullanın **imza**.
8.  **Oluştur**'a tıklayın
9.  Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_GoogleSecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Bir talep sağlayıcı uzantısı ilkenizde ekleme

Kullanıcıların toosign Google + hesabı kullanarak isterseniz, bir talep sağlayıcısı olarak toodefine Google + hesabınızın olması gerekir. Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta toospecify gerekir. Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar.

Google + hesabı ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:

1.  Hello İlkesi uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın. Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.
2.  Hello bulur `<ClaimsProviders>` bölümü
3.  Aşağıdaki XML parçacığını hello altında hello eklemek `ClaimsProviders` öğesi ve Değiştir `client_id` hello dosyayı kaydetmeden önce Google + hesabı uygulama istemci kimliği değeri.  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Yukarı Hello Google + hesap talep sağlayıcısı tooSign kaydetmek veya kullanıcı gezisine oturum

Merhaba kimlik sağlayıcısı ayarlandığına.  Ancak, hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil. Merhaba Google + hesabı kimlik sağlayıcısı tooyour kullanıcı ekleme `SignUpOrSignIn` kullanıcı gezisine. toomake kullanılabilir, biz var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.  Daha sonra hello Google + hesabı kimlik sağlayıcısı ekleyin:

>[!NOTE]
>
>Merhaba kopyaladıysanız `<UserJourneys>` öğesi ilke toohello uzantısı dosyanız (TrustFrameworkExtensions.xml) temel dosyasından toothis bölümü atlayabilirsiniz.

1.  Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.
2.  Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm içeriği `<UserJourneys>` düğümü.
3.  Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi. Merhaba öğe yoksa, ekleyin.
4.  Merhaba tüm içeriğini yapıştırın `<UserJournesy>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.

### <a name="display-hello-button"></a>Görüntü hello düğmesi
Merhaba `<ClaimsProviderSelections>` öğe, Talep sağlayıcı seçme seçenekleri hello listesi ve bunların sırası tanımlar.  `<ClaimsProviderSelection>`benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma sayfasında bir öğedir. Eklerseniz bir `<ClaimsProviderSelection>` öğesi Google + hesap için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda. tooadd bu öğe:

1.  Hello bulur `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız hello kullanıcı gezisine içinde.
2.  Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`
3.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Bağlantı hello düğmesi tooan eylemi
Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem. Merhaba, bu durumda, Google + hesap tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir.

1.  Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.
2.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * Hello sağlamak `Id` hello aynı değeri aynı olan `TargetClaimsExchangeId` bölüm önceki hello içinde
> * Olun `TechnicalProfileReferenceId` önceki (Google-OAUTH) oluşturulmuş toohello teknik profili kümesi kimliği.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hello İlkesi tooyour Kiracı karşıya yükle
1.  Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [bağlamı Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md)ve açık hello **Azure AD B2C** dikey.
2.  Seçin **kimlik deneyimi Framework**.
3.  Açık hello **tüm ilkeler** dikey.
4.  Seçin **karşıya İlkesi**.
5.  Denetleme **varsa hello ilkesi üzerine** kutusu.
6.  **Karşıya yükleme** TrustFrameworkExtensions.xml ve hello doğrulama başlayabildiğinden emin olun

## <a name="test-hello-custom-policy-by-using-run-now"></a>Şimdi Çalıştır kullanarak Hello özel ilkesini test
1.  Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.

    >[!NOTE]
    >
    >    **Şimdi Çalıştır** en az bir uygulama toobe preregistered hello Kiracı'gerektirir. 
    >    tooregister uygulamaları nasıl görürüm toolearn hello Azure AD B2C [başlama](active-directory-b2c-get-started.md) makale veya hello [uygulama kaydı](active-directory-b2c-app-registration.md) makalesi.


2.  Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello. Seçin **Şimdi Çalıştır**.
3.  Google + hesabı kullanarak mümkün toosign olmalıdır.

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a>[İsteğe bağlı] Merhaba Google + hesap talep sağlayıcısı tooProfile düzenleme kullanıcı gezisine kaydetme
Tooadd hello Google + hesabı kimlik sağlayıcısı tooyour kullanıcı da isteyebilir `ProfileEdit` kullanıcı gezisine. toomake, biz hello yineleyin kullanılabilir en son iki adımı:

### <a name="display-hello-button"></a>Görüntü hello düğmesi
1.  Merhaba uzantısının ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.
2.  Hello bulur `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız hello kullanıcı gezisine içinde.
3.  Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`
4.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Bağlantı hello düğmesi tooan eylemi
1.  Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.
2.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Şimdi Çalıştır kullanarak Hello özel profil Düzenleme İlkesi test

1.  Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.
2.  Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello. Seçin **Şimdi Çalıştır**.
3.  Google + hesabı kullanarak mümkün toosign olmalıdır.

## <a name="download-hello-complete-policy-files"></a>Merhaba tam ilke dosyaları indirme
İsteğe bağlı: Özel ilkeleri ile çalışmaya başlama size yol Bu örnek dosyalarını kullanmak yerine hello tamamladıktan sonra kendi özel ilke dosyaları kullanarak senaryonuz yapı öneririz.  [Başvuru için örnek ilke dosyaları](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
