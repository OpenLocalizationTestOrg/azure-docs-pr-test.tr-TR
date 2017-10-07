---
title: "Azure Active Directory B2C: ADFS özel ilkelerini kullanma SAML kimlik sağlayıcısı ekleyin."
description: "ADFS SAML protokolü ve özel ilkeler kullanılarak 2016 ayarlama bir nasıl tooarticle"
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
ms.openlocfilehash: 30fb7700e7834e3d91fab1fc1b169b761584b204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a>Azure Active Directory B2C: ADFS özel ilkelerini kullanma SAML kimlik sağlayıcısı ekleyin.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makalede nasıl tooenable oturum açma için ADFS hesabı hello kullanımını üzerinden kullanıcılardan gösterilmektedir [özel ilkeler](active-directory-b2c-overview-custom.md).

## <a name="prerequisites"></a>Ön koşullar

Tam hello adımları hello [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md) makalesi.

Bu adımlar şunları içerir:

1.  Bağlı olan taraf güveni ADFS oluşturuluyor.
2.  Merhaba ADFS bağlı olan taraf güveni sertifika tooAzure AD B2C ekleniyor.
3.  Talep sağlayıcı tooa ilke ekleniyor.
4.  Kayıt hello ADFS hesap sağlayıcısı tooa kullanıcı gezisine talepleri.
5.  Hello İlkesi tooan Azure AD B2C karşıya yükleme, Kiracı ve test.

## <a name="toocreate-a-claims-aware-relying-party-trust"></a>toocreate talep kullanan bir bağlı taraf güveni

toouse ADFS kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde toocreate bir ADFS bağlı olan taraf güveni gerekir ve hello doğru parametrelerle sağlayın.

Yeni bir bağlı olan taraf hello AD FS Yönetimi ek bileşenini kullanarak güven ve hello ayarları elle yapılandır tooadd hello bir federasyon sunucusu üzerinde aşağıdaki yordamı gerçekleştirin.

Üyelik **Yöneticiler**, veya eşdeğer bir gruba, hello yerel bilgisayarda hello minimum gerekli toocomplete bu yordamı. Merhaba uygun hesapları kullanmayla ilgili ayrıntıları gözden geçirin ve grup üyeliklerini [yerel ve etki alanı varsayılan grupları](http://go.microsoft.com/fwlink/?LinkId=83477)

1.  Sunucu Yöneticisi'nde **Araçları**ve ardından **ADFS Yönetim**.

2.  Tıklayın **bağlı olan taraf güveni ekleme**.
    ![Bağlı olan taraf güveni ekleme](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)

3.  Merhaba üzerinde **Hoş Geldiniz** sayfasında, **talep kullanan** tıklatıp **Başlat**.
    ![Merhaba Hoş Geldiniz sayfasında, talep kullanan seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)
4.  Merhaba üzerinde **veri kaynağı Seç** sayfasında, **hello bağlı olan taraf verilerini elle girin**ve ardından **sonraki**.
    ![Merhaba bağlı olan taraf verilerini girin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)

5.  Merhaba üzerinde **görünen adı belirt** sayfasında, bir ad yazın **görünen adı**altında **notları** bu bağlı olan taraf güveni için bir açıklama yazın ve ardından **sonraki** .
    ![Görünen ad ve notlar belirtin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)
6.  İsteğe bağlı. Bir isteğe bağlı belirteç şifreleme sertifikası sonra hello üzerinde varsa **sertifika Yapılandır** sayfasında, **Gözat** toolocate sertifika dosyasını ve ardından **sonraki** .
    ![Sertifika yapılandırma](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)
7.  Merhaba üzerinde **URL Yapılandır** sayfası, select hello **hello SAML 2.0 WebSSO protokolü için desteği etkinleştir** onay kutusu. Altında **bağlı olan taraf SAML 2.0 SSO hizmet URL'si**, bu bağlı olan taraf güveni hello güvenlik onaylama işlemi biçimlendirme dili (SAML) Hizmeti uç nokta URL'sini yazın ve ardından **sonraki**.  Hello için **bağlı olan taraf SAML 2.0 SSO hizmet URL'si**, hello Yapıştır `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`. {Tenant} (örneğin, contosob2c.onmicrosoft.com), kiracının adıyla değiştirin ve hello {İlkesi} uzantıları ilke adı (örneğin, B2C_1A_TrustFrameworkExtensions) ile değiştirin.
    > [!IMPORTANT]
    >Hello İlkesi adıdır signup_or_signin İlkesi, çünkü bu durumda devralan hello bir: `B2C_1A_TrustFrameworkExtensions`.
    >Örneğin hello URL olabilir: https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.

    ![Bağlı olan taraf SAML 2.0 SSO hizmet URL'si](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. Merhaba üzerinde **tanımlayıcıları yapılandırma** sayfasında, hello belirtin hello önceki adımla aynı URL'yi tıklatın **Ekle** tooadd bunları toohello listeleyin ve ardından **sonraki**.
    ![Bağlı olan taraf güveni tanımlayıcıları](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)
9.  Merhaba üzerinde **erişim denetimi ilkesini seçin** bir ilke seçin ve tıklatın **sonraki**.
    ![Erişim denetimi ilkesini seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)
10.  Merhaba üzerinde **tooAdd güven hazır** sayfasında, hello ayarlarını gözden geçirin ve ardından **sonraki** toosave bağlı olan taraf güven bilgilerinizi.
    ![Bağlı olan taraf güven bilgilerinizi Kaydet](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)
11.  Merhaba üzerinde **son** sayfasında, **Kapat**, bu eylem otomatik olarak hello görüntüler **talep kurallarını Düzenle** iletişim kutusu.
    ![Talep kurallarını Düzenle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)
12. Tıklatın **Kuralı Ekle**.  
      ![Yeni Kural Ekle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)
13.  İçinde **talep kuralı şablonu**seçin **Gönder LDAP özniteliklerini talep olarak**.
    ![Gönderme LDAP özniteliklerini talep şablonu kural olarak seçin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)
14.  Sağlamak **talep kuralı adı**. Hello için **öznitelik deposu** seçin **seçin Active Directory** talepler aşağıdaki hello ekleyin ve ardından **son** ve **Tamam**.
    ![Kural özelliklerini ayarlama](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)
15.  Sunucu Yöneticisi'nde seçin **bağlı olan taraf güvenleri** ardından oluşturduğunuz hello bağlı olan taraf güveni tıklatıp **özellikleri**.
    ![Bağlı olan taraf Özellikleri Düzenle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)
16.  Bir bağlı olan taraf güveni (B2C Demo) Özellikleri penceresinde hello **imza** sekmesinde **Ekle**.  
    ![Set imza](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)
17.  İmza sertifikanızı (özel anahtarı olmayan .cert dosyası) ekleyin.  
    ![İmza sertifikası ekleme](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  Merhaba bağlı olan taraf güveni (B2C Demo) Özellikleri penceresinde tıklatın **Gelişmiş** sekmesinde ve hello değiştirin **güvenli karma algoritması** çok**SHA-1**, tıklatın **Tamam**.  
    ![Güvenli Karma algoritması tooSHA-1 ayarlayın](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)

## <a name="add-hello-adfs-account-application-key-tooazure-ad-b2c"></a>Merhaba ADFS hesap uygulama anahtar tooAzure AD B2C ekleme
ADFS hesaplarıyla Federasyon istemci parolasını ADFS hesap tootrust Azure AD B2C hello uygulama adına gerektirir. Azure AD B2C kiracınızda ADFS sertifikanızı toostore gerekir. 

1.  Tooyour Azure AD B2C Kiracı gidip seçin **B2C ayarlarını** > **kimlik deneyimi Framework**
2.  Seçin **İlkesi anahtarları** tooview hello anahtarları kiracınızda kullanılabilir.
3.  Tıklatın **+ Ekle**.
4.  İçin **seçenekleri**, kullanın **karşıya**.
5.  İçin **adı**, kullanmak `ADFSSamlCert`.  
    Merhaba önek `B2C_1A_` otomatik olarak eklenebilir.
6.  Merhaba dosya karşıya yükleme içinde ** özel anahtarla sertifika .pfx dosyasını seçin. Not: Bu sertifikayla (Merhaba özel anahtarı) hello verilen ve hello ADFS bağlı olan taraf için kullanılan aynı olmalıdır.
![İlke anahtarını karşıya yükleyin](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)
7.  **Oluştur**'a tıklayın
8.  Başlangıç anahtarı oluşturduğunuz onaylayın `B2C_1A_ADFSSamlCert`.

## <a name="add-a-claims-provider-in-your-extension-policy"></a>Bir talep sağlayıcı uzantısı ilkenizde ekleme
Kullanıcıların toosign ADFS hesabı kullanarak isterseniz, bir talep sağlayıcısı olarak toodefine ADFS hesabınızın olması gerekir. Diğer bir deyişle, Azure AD B2C ile iletişim kuran bir uç nokta toospecify gerekir. Merhaba endpoint belirli bir kullanıcı doğrulaması Azure AD B2C tooverify tarafından kullanılan talepler kümesi sağlar.

ADFS ekleyerek bir talep sağlayıcısı olarak tanımlamak `<ClaimsProvider>` İlkesi uzantısının düğümünde:

1. Hello İlkesi uzantısının (TrustFrameworkExtensions.xml) çalışma dizininizi açın. Bir XML Düzenleyici, gerekirse [Visual Studio Code deneyin](https://code.visualstudio.com/download), basit bir platformlar arası Düzenleyici.
2. Hello bulur `<ClaimsProviders>` bölümü
3. Aşağıdaki XML parçacığını hello altında hello eklemek `ClaimsProviders` öğesi ve Değiştir `identityProvider` DNS sunucunuzun (etki alanınızdaki gösterir rastgele değer) ile Merhaba dosyasını kaydedin. 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
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

## <a name="register-hello-adfs-account-claims-provider-toosign-up-or-sign-in-user-journey"></a>Yukarı Hello ADFS hesap talep sağlayıcısı tooSign kaydetmek veya kullanıcı gezisine oturum
Bu noktada, hello kimlik sağlayıcısı ayarlandığına.  Ancak, hello oturumu-up/oturum açma ekranları hiçbirinde kullanılabilir değil. Tooadd hello ADFS hesabı kimlik sağlayıcısı tooyour kullanıcı gerek artık `SignUpOrSignIn` kullanıcı gezisine. toomake kullanılabilir, biz var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun.  Merhaba ADFS kimlik sağlayıcısı içerecek şekilde sonra biz değiştirebilirsiniz:
    >[!NOTE]
    >If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.
2.  Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm içeriği `<UserJourneys>` düğümü.
3.  Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın ve hello bulur `<UserJourneys>` öğesi. Merhaba öğe yoksa, ekleyin.
4.  Merhaba tüm içeriğini yapıştırın `<UserJournesy>` hello alt sitesi olarak kopyaladığınız düğümü `<UserJourneys>` öğesi.

### <a name="display-hello-button"></a>Görüntü hello düğmesi
Merhaba `<ClaimsProviderSelections>` öğe, Talep sağlayıcı seçme seçenekleri hello listesi ve bunların sırası tanımlar.  `<ClaimsProviderSelection>`benzer tooan kimlik sağlayıcısı düğmesi oturumu-up/oturum açma sayfasında bir öğedir. Eklerseniz bir `<ClaimsProviderSelection>` öğesi ADFS hesap için yeni bir düğme görüntülenir hello sayfasında bir kullanıcı adlandırıldığını olduğunda. tooadd bu öğe:

1.  Hello bulur `<UserJourney>` içeren düğüm `Id="SignUpOrSignIn"` kopyaladığınız hello kullanıcı gezisine içinde.
2.  Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`
3.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-hello-button-tooan-action"></a>Bağlantı hello düğmesi tooan eylemi

Yerinde bir düğmeye sahip olduğunuza göre toolink gerekir, tooan eylem. Merhaba, bu durumda, ADFS hesap tooreceive ile Azure AD B2C toocommunicate için bir belirteç eylemdir. Merhaba düğmesi tooan eylemi, ADFS hesap talep sağlayıcısı hello teknik profili bağlayarak Bağla:

1.  Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.
2.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * Hello sağlamak `Id` hello aynı değeri aynı olan `TargetClaimsExchangeId` bölüm önceki hello içinde.
> * Olun `TechnicalProfileReferenceId` önceki (Contoso-SAML2) oluşturulmuş toohello teknik profili ayarlayın.

## <a name="upload-hello-policy-tooyour-tenant"></a>Hello İlkesi tooyour Kiracı karşıya yükle
1.  Merhaba, [Azure portal](https://portal.azure.com), geçiş hello [bağlamı Azure AD B2C kiracınızın](active-directory-b2c-navigate-to-b2c-context.md)ve açık hello **Azure AD B2C** dikey.
2.  Seçin **kimlik deneyimi Framework**.
3.  Açık hello **tüm ilkeler** dikey.
4.  Seçin **karşıya İlkesi**.
5.  Denetleme **varsa hello ilkesi üzerine** kutusu.
6.  **Karşıya yükleme** TrustFrameworkExtensions.xml ve hello doğrulama başlayabildiğinden emin olun

## <a name="test-hello-custom-policy-by-using-run-now"></a>Şimdi Çalıştır kullanarak Hello özel ilkesini test
1.  Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.
2.  Açık **B2C_1A_signup_signin**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello. Seçin **Şimdi Çalıştır**.
3.  ADFS hesabı kullanarak mümkün toosign olmalıdır.

## <a name="optional-register-hello-adfs-account-claims-provider-tooprofile-edit-user-journey"></a>[İsteğe bağlı] Merhaba ADFS hesap talep sağlayıcısı tooProfile düzenleme kullanıcı gezisine kaydetme
Tooadd hello ADFS hesabı kimlik sağlayıcısı tooyour kullanıcı da isteyebilir `ProfileEdit` kullanıcı gezisine. toomake, biz hello yineleyin kullanılabilir en son iki adımı:

### <a name="display-hello-button"></a>Görüntü hello düğmesi
1.  Merhaba uzantısının ilkenizin (örneğin, TrustFrameworkExtensions.xml) açın.
2.  Hello bulur `<UserJourney>` içeren düğüm `Id="ProfileEdit"` kopyaladığınız hello kullanıcı gezisine içinde.
3.  Merhaba bulun `<OrchestrationStep>` içeren düğümü`Order="1"`
4.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsProviderSelections>` düğümü:

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-hello-button-tooan-action"></a>Bağlantı hello düğmesi tooan eylemi
1.  Hello bulur `<OrchestrationStep>` içeren `Order="2"` hello içinde `<UserJourney>` düğümü.
2.  Aşağıdaki XML parçacığını altında ekleyin `<ClaimsExchanges>` düğümü:

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a>Şimdi Çalıştır kullanarak Hello özel profil Düzenleme İlkesi test
1.  Açık **Azure AD B2C ayarlarını** ve çok Git**kimlik deneyimi Framework**.
2.  Açık **B2C_1A_ProfileEdit**, karşıya yüklediğiniz bağlı olan taraf (RP) özel ilke hello. Seçin **Şimdi Çalıştır**.
3.  ADFS hesabı kullanarak mümkün toosign olmalıdır.

## <a name="download-hello-complete-policy-files"></a>Merhaba tam ilke dosyaları indirme
İsteğe bağlı: Size özel ilkeleri ile çalışmaya başlama yol hello tamamladıktan sonra kendi özel ilke dosyaları kullanarak senaryonuz yapı öneririz. [İlke örnek dosyaları yalnızca başvuru için](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
