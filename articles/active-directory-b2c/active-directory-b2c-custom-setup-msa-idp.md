---
title: "Azure Active Directory B2C: Microsoft hesabı (MSA) özel ilkelerini kullanarak bir kimlik sağlayıcısı ekleyin."
description: "Openıd Connect (OIDC) protokolünü kullanarak kimlik sağlayıcısı Microsoft kullanılarak örnek"
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
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: Microsoft hesabı (MSA) özel ilkelerini kullanarak bir kimlik sağlayıcısı ekleyin.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makale size nasıl tooenable oturum açmak için Microsoft hesabı (MSA) kullanıcılardan hello kullanımını gösterir [özel ilkeler](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Ön koşullar
Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.

Bu adımlar şunları içerir:

1.  Bir Microsoft hesabı uygulaması oluşturuluyor.
2.  Merhaba Microsoft hesabı uygulama anahtar tooAzure AD B2C ekleme
3.  Talep sağlayıcı tooa ilkesi ekleme
4.  Merhaba Microsoft Account talep sağlayıcısı tooa kullanıcı gezisine kaydetme
5.  Kiracı Hello İlkesi tooan Azure AD B2C karşıya yükleme ve test

## <a name="create-a-microsoft-account-application"></a>Bir Microsoft hesabı uygulaması oluşturma
toouse Microsoft hesabı kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde hello doğru parametrelerle tedarik ve toocreate bir Microsoft hesabı uygulaması gerekir. Bir Microsoft hesabı gerekir. Yoksa, ziyaret [https://www.live.com/](https://www.live.com/).

1.  Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ve Microsoft hesabı kimlik bilgilerinizle oturum açın.
2.  Tıklatın **bir uygulama ekleyin**.

    ![Microsoft hesabı - bir uygulama ekleyin](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  Sağlamak bir **adı** , uygulamanız için **kişi e-posta**, seçeneğinin işaretini kaldırın **başlamanıza yardım bize** tıklatıp **oluşturma**.

    ![Microsoft hesabı - uygulamanızı kaydetme](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  Merhaba değerini kopyalayın **uygulama kimliği**. Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız.

    ![Microsoft hesabı - kopyalama hello değeri uygulama kimliği](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  Tıklayın **Ekle platformu**

    ![Microsoft hesabı - platform ekleme](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  Merhaba platform listeden seçin **Web**.

    ![Microsoft hesabı - hello platform listeden Web seçin](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yeniden yönlendirme URI'ler** alan. Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).

    ![Microsoft hesabı - kümesi yeniden yönlendirme URL'leri](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  Tıklayın **yeni bir parola oluşturmak** hello altında **uygulama parolaları** bölümü. Ekranda görüntülenen hello yeni parolayı kopyalayın. Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız. Bu parolayı bir önemli güvenlik kimlik bilgisidir.

    ![Microsoft hesabı - yeni bir parola oluştur](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Microsoft hesabı - kopyalama hello yeni parola](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  Bildiren hello kutuyu **Live SDK'sı desteği** hello altında **Gelişmiş Seçenekler** bölümü. **Kaydet** düğmesine tıklayın.

    ![Microsoft hesabı - Live SDK'sı desteği](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a>Merhaba Microsoft hesabı uygulama anahtar tooAzure AD B2C ekleme
Microsoft hesapları ile Federasyon istemci parolasını hello uygulama adına Microsoft hesabı tootrust Azure AD B2C gerektirir. Azure AD B2C kiracısı içinde Microsoft hesabı uygulama secert toostore gerekir:   

1.  Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework**
2.  Seçin **İlkesi anahtarları** tooview hello anahtarları kiracınızda kullanılabilir.
3.  Tıklatın **+ Ekle**.
4.  İçin **seçenekleri**, kullanın **el ile**.
5.  İçin **adı**, kullanmak `MSASecret`.  
    Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.
6.  Merhaba, **gizli** kutusuna, https://apps.dev.microsoft.com Microsoft uygulama gizli anahtarı girin
7.  İçin **anahtar kullanımı**, kullanın **imza**.
8.  **Oluştur**'a tıklayın
9.  Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_MSASecret`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Bir talep sağlayıcı uzantısı ilkenizde ekleme
Kullanıcıların toosign Microsoft Account kullanarak isterseniz, bir talep sağlayıcısı olarak toodefine Microsoft Account gerekir. Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta toospecify gerekir. Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar.

Microsoft Account ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:

1.  Hello İlkesi uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın. Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.
2.  Hello bulur `<ClaimsProviders>` bölümü
3.  Aşağıdaki XML parçacığını hello altında ekleyin `ClaimsProviders` öğe:

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  Değiştir `client_id` Microsoft Account uygulama istemci kimliği değeri

5.  Merhaba dosyasını kaydedin.

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Merhaba Microsoft Account talep sağlayıcısı tooSign yukarı veya oturum açma kullanıcı gezisine kaydetme

Bu noktada, hello kimlik sağlayıcısı ayarlandı, ancak hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil. Tooadd hello Microsoft Account kimlik sağlayıcısı tooyour user gereksinim artık `SignUpOrSignIn` kullanıcı gezisine. toomake kullanılabilir, biz var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.  Daha sonra hello Microsoft Account kimlik sağlayıcısı ekleyin:

> [!NOTE]
>
>Daha önce hello kopyaladıysanız `<UserJourneys>` İlkesi toohello uzantısının temel dosyanın öğesinden `TrustFrameworkExtensions.xml`, toothis bölümü atlayabilirsiniz.

1.  Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.
2.  Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm içeriği `<UserJourneys>` düğümü.
3.  Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi. Merhaba öğe yoksa, ekleyin.
4.  Merhaba tüm içeriğini yapıştırın `<UserJournesy>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.

### <a name="display-hello-button"></a>Görüntü hello düğmesi
Merhaba `<ClaimsProviderSelections>` öğe, Talep sağlayıcı seçme seçenekleri hello listesi ve bunların sırası tanımlar.  `<ClaimsProviderSelection>`benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma sayfasında bir öğedir. Eklerseniz bir `<ClaimsProviderSelection>` öğesi Microsoft hesabı için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda. tooadd bu öğe:

1.  Hello bulur `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız hello kullanıcı gezisine içinde.
2.  Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`
3.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Bağlantı hello düğmesi tooan eylemi
Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem. Merhaba, bu durumda, Microsoft Account tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir. Merhaba düğmesi tooan eylemi, Microsoft Account talep sağlayıcısı hello teknik profili bağlayarak Bağla:

1.  Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.
2.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * Hello sağlamak `Id` hello aynı değeri aynı olan `TargetClaimsExchangeId` bölüm önceki hello içinde
>   * Olun `TechnicalProfileReferenceId` önceki (MSA-OIDC) oluşturulmuş toohello teknik profili kümesi kimliği.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hello İlkesi tooyour Kiracı karşıya yükle
1.  Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [bağlamı Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md)ve açık hello **Azure AD B2C** dikey.
2.  Seçin **kimlik deneyimi Framework**.
3.  Açık hello **tüm ilkeler** dikey.
4.  Seçin **karşıya İlkesi**.
5.  Denetleme **varsa hello ilkesi üzerine** kutusu.
6.  **Karşıya yükleme** TrustFrameworkExtensions.xml ve hello doğrulama başlayabildiğinden emin olun

## <a name="test-hello-custom-policy-by-using-run-now"></a>Şimdi Çalıştır kullanarak Hello özel ilkesini test

1.  Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.
> [!NOTE]
>
>**Şimdi Çalıştır** en az bir uygulama toobe preregistered hello Kiracı'gerektirir. tooregister uygulamaları nasıl görürüm toolearn hello Azure AD B2C [başlama](active-directory-b2c-get-started.md) makale veya hello [uygulama kaydı](active-directory-b2c-app-registration.md) makalesi.
2.  Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello. Seçin **Şimdi Çalıştır**.
3.  Microsoft hesabı kullanarak mümkün toosign olmalıdır.

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a>[İsteğe bağlı] Merhaba Microsoft Account talep sağlayıcısı tooProfile düzenleme kullanıcı gezisine kaydetme
Tooadd hello Microsoft Account kimlik sağlayıcısı tooyour kullanıcı da isteyebilir `ProfileEdit` kullanıcı gezisine. toomake, biz hello yineleyin kullanılabilir en son iki adımı:

### <a name="display-hello-button"></a>Görüntü hello düğmesi
1.  Merhaba uzantısının ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.
2.  Hello bulur `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız hello kullanıcı gezisine içinde.
3.  Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`
4.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Bağlantı hello düğmesi tooan eylemi
1.  Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.
2.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Şimdi Çalıştır kullanarak Hello özel profil Düzenleme İlkesi test
1.  Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.
2.  Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello. Seçin **Şimdi Çalıştır**.
3.  Microsoft hesabı kullanarak mümkün toosign olmalıdır.

## <a name="download-hello-complete-policy-files"></a>Merhaba tam ilke dosyaları indirme
İsteğe bağlı: Özel ilkeleri ile çalışmaya başlama size yol Bu örnek dosyalarını kullanmak yerine hello tamamladıktan sonra kendi özel ilke dosyaları kullanarak senaryonuz yapı öneririz.  [Başvuru için örnek ilke dosyaları](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
