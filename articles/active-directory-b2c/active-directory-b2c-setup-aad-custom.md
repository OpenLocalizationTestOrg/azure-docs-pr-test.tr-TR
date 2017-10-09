---
title: "Azure Active Directory B2C: özel ilkeler kullanarak bir Azure AD Sağlayıcısı Ekle | Microsoft Docs"
description: "Azure Active Directory B2C özel ilkeleri hakkında bilgi edinin"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 31f0dfe5-1ad0-4a25-a53b-8acc71bcea72
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: 9b0c32086cebc171d91da2e7bfb48136723ccd4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-azure-ad-accounts"></a>Azure Active Directory B2C: Azure AD hesapları kullanarak oturum açın

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makalede nasıl tooenable oturum açmak için kullanıcılar hello kullanımı aracılığıyla belirli bir Azure Active Directory (Azure AD) kuruluştan gösterilmektedir [özel ilkeler](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Ön koşullar

Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.

Bu adımlar şunları içerir:

1. Bir Azure Active Directory B2C oluşturma (Azure AD B2C) Kiracı.
2. Bir Azure AD B2C uygulaması oluşturuluyor.
3. İki ilke altyapısı uygulama kaydediliyor.
4. Anahtarları ayarlama.
5. Merhaba başlangıç paketi ayarlama.

## <a name="create-an-azure-ad-app"></a>Bir Azure AD uygulaması oluştur

tooenable oturum açma belirli kullanıcılar için Azure AD kuruluş tooregister hello kuruluş Azure AD Kiracı içinde bir uygulama gerekiyor.

>[!NOTE]
> "Contoso.com" Merhaba kuruluş Azure AD Kiracı ve "fabrikamb2c.onmicrosoft.com" için yönergeleri izleyerek hello hello Azure AD B2C Kiracı olarak kullanırız.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
1. Merhaba üst çubuğunda hesabınızı seçin. Merhaba gelen **Directory** listesinde, uygulamanız (contoso.com) hello kuruluş Azure AD Kiracı tooregister istediğiniz yeri seçin.
1. Seçin **daha fazla hizmet** hello sol bölmesinde ve "Uygulama kayıtlar" için arama
1. Seçin **yeni uygulama kaydı**.
1. Uygulamanız için bir ad girin (örneğin, `Azure AD B2C App`).
1. Seçin **Web uygulaması / API** hello uygulama türü için.
1. İçin **oturum açma URL'si**, URL, aşağıdaki hello girin nerede `yourtenant` hello Azure AD B2C kiracınızın adıyla değiştirilen (`fabrikamb2c.onmicrosoft.com`):

    ```
    https://login.microsoftonline.com/te/yourtenant.onmicrosoft.com/oauth2/authresp
    ```

1. Kaydet Hello uygulama kimliği.
1. Yeni oluşturulan hello uygulaması'nı seçin.
1. Merhaba altında **ayarları** dikey penceresinde, select **anahtarları**.
1. Yeni bir anahtar oluşturun ve kaydedin. Merhaba sonraki bölümde hello adımlarda kullanır.

## <a name="add-hello-azure-ad-key-tooazure-ad-b2c"></a>Hello Azure AD anahtar tooAzure AD B2C ekleme

Azure AD B2C kiracınızda toostore hello contoso.com uygulama anahtarı gerekir. toodo bu:
1. Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework** > **İlkesi anahtarları**.
1. Seçin **+ Ekle**.
1. Bu seçenekler girin veya seçin:
   * Seçin **el ile**.
   * İçin **adı**, Azure AD Kiracı adı ile eşleşen bir ad seçin (örneğin, `ContosoAppSecret`).  Merhaba önek `B2C_1A_` anahtarınızı toohello adını otomatik olarak eklenir.
   * Uygulama anahtarınızı hello Yapıştır **gizli** kutusu.
   * Seçin **imza**.
1. **Oluştur**’u seçin.
1. Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_ContosoAppSecret`.


## <a name="add-a-claims-provider-in-your-base-policy"></a>Bir talep sağlayıcı temel ilkenizde ekleme

Kullanıcıların toosign Azure AD kullanarak istiyorsanız, Talep sağlayıcı olarak Azure AD toodefine gerekir. Diğer bir deyişle, Azure AD B2C ile iletişim kuracak bir uç nokta toospecify gerekir. Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar. 

Azure AD toohello ekleyerek bir talep sağlayıcısı olarak Azure AD tanımlayabilirsiniz `<ClaimsProvider>` ilkenizin hello uzantısı dosyasında düğümü:

1. Merhaba uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın.
1. Hello bulur `<ClaimsProviders>` bölümü. Yoksa, hello kök düğümü ekleyin.
1. Yeni bir ekleme `<ClaimsProvider>` şekilde düğümü:

    ```XML
    <ClaimsProvider>
        <Domain>Contoso</Domain>
        <DisplayName>Login using Contoso</DisplayName>
        <TechnicalProfiles>
            <TechnicalProfile Id="ContosoProfile">
                <DisplayName>Contoso Employee</DisplayName>
                <Description>Login with your Contoso account</Description>
                <Protocol Name="OpenIdConnect"/>
                <OutputTokenFormat>JWT</OutputTokenFormat>
                <Metadata>
                    <Item Key="METADATA">https://login.windows.net/contoso.com/.well-known/openid-configuration</Item>
                    <Item Key="ProviderName">https://sts.windows.net/00000000-0000-0000-0000-000000000000/</Item>
                    <Item Key="client_id">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="IdTokenAudience">00000000-0000-0000-0000-000000000000</Item>
                    <Item Key="response_types">id_token</Item>
                    <Item Key="UsePolicyInRedirectUri">false</Item>
                </Metadata>
                <CryptographicKeys>
                    <Key Id="client_secret" StorageReferenceId="B2C_1A_ContosoAppSecret"/>
                </CryptographicKeys>
                <OutputClaims>
                    <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="oid"/>
                    <OutputClaim ClaimTypeReferenceId="tenantId" PartnerClaimType="tid"/>
                    <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
                    <OutputClaim ClaimTypeReferenceId="surName" PartnerClaimType="family_name" />
                    <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
                    <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="contosoAuthentication" />
                    <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="AzureADContoso" />
                </OutputClaims>
                <OutputClaimsTransformations>
                    <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
                    <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
                    <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
                    <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
                </OutputClaimsTransformations>
                <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
            </TechnicalProfile>
        </TechnicalProfiles>
    </ClaimsProvider>
    ```

1. Merhaba altında `<ClaimsProvider>` düğümü, güncelleştirme hello değeri `<Domain>` kullanılan toodistinguish olabilir benzersiz bir değer tooa bu diğer kimlik sağlayıcılardan gelen.
1. Merhaba altında `<ClaimsProvider>` düğümü, güncelleştirme hello değeri `<DisplayName>` hello için kolay ad tooa talep sağlayıcısı. Bu değer şu anda kullanılmıyor.

### <a name="update-hello-technical-profile"></a>Merhaba teknik profilini güncelleştir

tooget hello Azure AD uç noktasından bir belirteç, toodefine hello protokolleri Azure AD B2C Azure AD ile toocommunicate kullanmanız gerekir. Bu hello içinde yapılır `<TechnicalProfile>` öğesinin `<ClaimsProvider>`.
1. Merhaba Hello Kimliğini güncelleştirme `<TechnicalProfile>` düğümü. Bu kimliği kullanılan toorefer toothis hello İlkesi diğer kısımlarından teknik profilidir.
1. Merhaba değeri güncelleştirme `<DisplayName>`. Bu değer, oturum açma hello düğmesine oturum açma ekranında görüntülenir.
1. Merhaba değeri güncelleştirme `<Description>`.
1. Azure AD hello Openıd Connect protokolünü kullanır, böylece bu hello değeri sağlamak `<Protocol>` olan `"OpenIdConnect"`.

Tooupdate hello gereksinim `<Metadata>` hello XML dosyasındaki bölümünde başvurulan tooearlier tooreflect hello yapılandırma ayarları için özel Azure AD kiracısı. Merhaba XML dosyasında hello meta veri değerleri şu şekilde güncelleştirin:

1. Ayarlama `<Item Key="METADATA">` çok`https://login.windows.net/yourAzureADtenant/.well-known/openid-configuration`, burada `yourAzureADtenant` Azure AD Kiracı adınız (contoso.com).
1. Tarayıcı ve Git toohello açmak `METADATA` güncelleştirdiğiniz URL.
1. Merhaba tarayıcıda hello 'dağıtımcı' nesnesi için konum ve değerini kopyalayın. Merhaba aşağıdaki gibi görünmelidir: `https://sts.windows.net/{tenantId}/`.
1. Yapıştırmak için hello değer `<Item Key="ProviderName">` hello XML dosyasında.
1. Ayarlama `<Item Key="client_id">` hello uygulama kaydı toohello uygulama kimliği.
1. Ayarlama `<Item Key="IdTokenAudience">` hello uygulama kaydı toohello uygulama kimliği.
1. Emin `<Item Key="response_types">` çok ayarlanır`id_token`.
1. Emin `<Item Key="UsePolicyInRedirectUri">` çok ayarlanır`false`.

Ayrıca, Azure AD B2C Kiracı toohello Azure AD kayıtlı toolink hello Azure AD parola gerekir `<ClaimsProvider>` bilgi:

* Merhaba, `<CryptographicKeys>` hello XML dosyası önceki bölümünde, güncelleştirmek için hello değer `StorageReferenceId` tanımladığınız hello gizli toohello başvuru kimliği (örneğin, `ContosoAppSecret`).

### <a name="upload-hello-extension-file-for-verification"></a>Doğrulama Hello uzantısı dosyasını karşıya yükleme

Artık, böylece Azure AD B2C bilir ilkeniz yapılandırmış olduğunuz nasıl toocommunicate Azure AD dizininizi ile. Bu sorunları kadar sahip olmadığı için ilke yalnızca tooconfirm Hello uzantısı dosyasını karşıya yüklemeyi deneyin. toodo için:

1. Açık hello **tüm ilkeler** dikey penceresinde, Azure AD B2C kiracısı.
1. Merhaba denetleyin **varsa hello ilkesi üzerine** kutusu.
1. Merhaba uzantısının (TrustFrameworkExtensions.xml) karşıya yükleyin ve hello doğrulama başlayabildiğinden emin olun.

## <a name="register-hello-azure-ad-claims-provider-tooa-user-journey"></a>Hello Azure AD talep sağlayıcısı tooa kullanıcı gezisine kaydetme

Şimdi tooadd hello Azure AD kimlik sağlayıcısı tooone kullanıcı Yolculuklar biri gerekir. Bu noktada, hello kimlik sağlayıcısı ayarlandı, ancak hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil. toomake, kullanılabilir var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturur ve ardından değiştirin hello Azure AD kimlik sağlayıcısı de vardır:

1. Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.
1. Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"`.
1. Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi. Merhaba öğe yoksa, ekleyin.
1. Yapıştır hello tüm `<UserJourney>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.
1. Merhaba yeni kullanıcı gezisine Hello Kimliğini yeniden adlandırın (örneğin, olarak yeniden adlandırın `SignUpOrSignUsingContoso`).

### <a name="display-hello-button"></a>Görüntü hello "button"

Merhaba `<ClaimsProviderSelection>` benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma ekranında bir öğedir. Eklerseniz bir `<ClaimsProviderSelection>` öğesi Azure AD için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda. tooadd bu öğe:

1. Hello bulur `<OrchestrationStep>` içeren düğüm `Order="1"` oluşturduğunuz hello kullanıcı gezisine içinde.
1. Merhaba aşağıdakileri ekleyin:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

1. Ayarlama `TargetClaimsExchangeId` tooan uygun değeri. Aşağıdaki hello aynı öneririz başkalarının olarak kuralı:  *\[ClaimProviderName\]Exchange*.

### <a name="link-hello-button-tooan-action"></a>Bağlantı hello düğmesi tooan eylemi

Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem. Merhaba, bu durumda, Azure AD tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir. Merhaba düğmesi tooan eylemi, Azure AD talep sağlayıcısı hello teknik profili bağlayarak Bağla:

1. Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.
1. Merhaba aşağıdakileri ekleyin:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

1. Güncelleştirme `Id` aynı değer aynı toohello `TargetClaimsExchangeId` bölüm önceki hello içinde.
1. Güncelleştirme `TechnicalProfileReferenceId` hello teknik toohello Kimliğini profil daha önce oluşturduğunuz (ContosoProfile).

### <a name="upload-hello-updated-extension-file"></a>Merhaba güncelleştirilmiş uzantısı dosyasını karşıya yükle

Değiştirme hello uzantısının yapılır. Dosyayı kaydedin. Merhaba dosyasını karşıya yükleyin ve tüm doğrulamaları başarılı olduğunu doğrulayın.

### <a name="update-hello-rp-file"></a>Merhaba RP dosyasını güncelleştirme

Şimdi yeni oluşturduğunuz hello kullanıcı gezisine başlatacaktır tooupdate hello bağlı olan taraf (RP) dosya gerekir:

1. Çalışma dizininizi SignUpOrSignIn.xml bir kopyasını oluşturun ve yeniden adlandırın (örneğin, tooSignUpOrSignInWithAAD.xml yeniden adlandırmadan).
1. Açık hello yeni dosya ve güncelleştirme hello `PolicyId` için öznitelik `<TrustFrameworkPolicy>` benzersiz bir değerle (örneğin, SignUpOrSignInWithAAD). <br> Bu ilkenizin hello ad olacaktır (örneğin, B2C\_1A\_SignUpOrSignInWithAAD).
1. Merhaba değiştirme `ReferenceId` özniteliğini `<DefaultUserJourney>` hello (SignUpOrSignUsingContoso) oluşturulan yeni kullanıcı gezisine toomatch hello kimliği.
1. Yaptığınız değişiklikleri kaydedin ve hello dosyasını karşıya yükleyin.

## <a name="troubleshooting"></a>Sorun giderme

Test yalnızca kendi dikey penceresini açıp tıklatarak karşıya hello özel ilke **Şimdi Çalıştır**. Okuma toodiagnose sorunları hakkında [sorun giderme](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Sonraki adımlar

Çok görüş[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
