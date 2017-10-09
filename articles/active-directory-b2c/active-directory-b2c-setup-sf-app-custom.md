---
title: "Azure Active Directory B2C: özel ilkeler kullanılarak Salesforce SAML sağlayıcı ekleme | Microsoft Docs"
description: "Hakkında bilgi edinin toocreate ve Azure Active Directory B2C özel ilkelerini yönetin."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a>Azure Active Directory B2C: SAML aracılığıyla Salesforce hesaplarını kullanarak oturum açın

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makale size nasıl gösterir toouse [özel ilkeler](active-directory-b2c-overview-custom.md) tooset oturum açma belirli Salesforce kuruluştan kullanıcılar için ayarlama.

## <a name="prerequisites"></a>Ön koşullar

### <a name="azure-ad-b2c-setup"></a>Azure AD B2C Kurulumu

Tüm nasıl çok Göster hello adımları tamamladığınızdan emin olun[özel ilkelerini kullanmaya başlama](active-directory-b2c-get-started-custom.md) Azure Active Directory B2C içinde (Azure AD B2C).

Bunlar:

* Azure AD B2C kiracısı oluşturun.
* Bir Azure AD B2C uygulaması oluşturun.
* İki ilke altyapısı uygulama kaydedin.
* Anahtarları ayarlayın.
* Merhaba başlangıç paketi ayarlayın.

### <a name="salesforce-setup"></a>Salesforce Kurulum

Bu makalede, zaten hello aşağıdakileri yaptığınızdan varsayın:

* İmzalanmış Salesforce hesabınız için. Oturum açabileceğiniz bir [ücretsiz bir geliştirici sürümü hesap](https://developer.salesforce.com/signup).
* [My etki alanını ayarlama](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) Salesforce kuruluşunuz için.

## <a name="set-up-salesforce-so-users-can-federate"></a>Kullanıcıların devredebilir Salesforce ayarlandı

toohelp Azure AD B2C Salesforce ile iletişim kurmak, tooget hello Salesforce meta veri URL'sini gerekir.

### <a name="set-up-salesforce-as-an-identity-provider"></a>Salesforce kimlik sağlayıcısı olarak ayarlayın

> [!NOTE]
> Bu makalede, kullanmakta olan varsayıyoruz [Salesforce Şimşek deneyimi](https://developer.salesforce.com/page/Lightning_Experience_FAQ).

1. [İçinde tooSalesforce oturum](https://login.salesforce.com/). 
2. Merhaba üzerinde menüsünde altında sol **ayarları**, genişletin **kimlik**ve ardından **kimlik sağlayıcısı**.
3. Tıklatın **etkinleştirme kimlik sağlayıcısı**.
4. Altında **Select hello sertifika**seçin Salesforce toouse toocommunicate Azure AD B2C ile istediğiniz hello sertifika. (Merhaba varsayılan sertifika kullanabilirsiniz.) **Kaydet** düğmesine tıklayın. 

### <a name="create-a-connected-app-in-salesforce"></a>Salesforce'ta bağlı bir uygulama oluşturma

1. Merhaba üzerinde **kimlik sağlayıcısı** sayfasında, çok Git**hizmet sağlayıcıları**.
2. Tıklatın **hizmet sağlayıcıları bağlı uygulamalar şimdi oluşturulur. Burayı tıklatın.**
3. Altında **temel bilgileri**, bağlı uygulamanız için hello gerekli değerleri girin.
4. Altında **Web uygulaması ayarları**seçin hello **etkinleştirmek SAML** onay kutusu.
5. Merhaba, **varlık kimliği** alanında, URL aşağıdaki hello girin. Merhaba değeri yerini olmak `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. Merhaba, **ACS URL** alanında, URL aşağıdaki hello girin. Merhaba değeri yerini olmak `tenantName`.
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. Merhaba tüm diğer ayarlar için varsayılan değerleri bırakın.
8. Merhaba listesinin toohello altına'e gidin ve ardından **kaydetmek**.

### <a name="get-hello-metadata-url"></a>Merhaba meta veri URL'sini alma

1. Merhaba genel bakış sayfasında, bağlı uygulamanızın tıklayın **Yönet**.
2. Merhaba değerini kopyalayın **meta veri bulma uç noktası**ve kaydedin. Bu makalenin sonraki bölümlerinde kullanacaksınız.

### <a name="set-up-salesforce-users-toofederate"></a>Salesforce kullanıcılar toofederate ayarlayın

1. Merhaba üzerinde **Yönet** sayfa bağlı uygulamanızı çok Git**profilleri**.
2. Tıklatın **profillerini yönetmek**.
3. Hello profilleri (veya kullanıcı grupları) seçin, Azure AD B2C ile toofederate istediğiniz. Bir sistem yöneticisi olarak hello seçin **Sistem Yöneticisi** Salesforce hesabınıza kullanarak birleştirmek için onay kutusunu.

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a>Azure AD B2C için imzalama sertifikası oluştur

Azure AD B2C tarafından imzalanmış tooSalesforce gerek toobe gönderdiği istekleri. toogenerate bir imzalama sertifikası Azure PowerShell'i açın ve ardından hello aşağıdaki komutları çalıştırın.

> [!NOTE]
> Merhaba Kiracı adı ve parola hello üst iki satırlardaki güncelleştirdiğinizden emin olun.

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a>Merhaba SAML imzalama sertifikası tooAzure AD B2C ekleme

Sertifika tooyour Azure AD B2C Kiracı imzalama hello karşıya yükle: 

1. Tooyour Azure AD B2C Kiracı gidin. Tıklatın **ayarları** > **kimlik deneyimi Framework** > **İlkesi anahtarları**.
2. Tıklatın **+ Ekle**ve ardından:
    1. Tıklatın **seçenekleri** > **karşıya**.
    2. Girin bir **adı** (örneğin, SAMLSigningCert). Merhaba önek *B2C_1A_* anahtarınızı toohello adını otomatik olarak eklenir.
    3. tooselect, sertifikanızı seçin **dosya denetimi karşıya**. 
    4. Merhaba PowerShell komut dosyasında ayarlanan hello sertifikanın parolasını girin.
3. **Oluştur**'a tıklayın.
4. Bir anahtar (örneğin, B2C_1A_SAMLSigningCert) oluşturduğunuzdan emin olun. Merhaba tam adı not edin (de dahil olmak üzere *B2C_1A_*). Daha sonra hello İlkesi toothis anahtar başvurur.

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a>Temel ilkenizde Hello Salesforce SAML Talep sağlayıcı oluşturma

Kullanıcıların Salesforce kullanarak oturum açabilmeniz için bir talep sağlayıcısı olarak toodefine Salesforce gerekir. Diğer bir deyişle, Azure AD B2C ile iletişim kuracak toospecify hello uç noktası gerekir. Merhaba uç nokta olacak *sağlamak* bir dizi *talep* Azure AD B2C belirli bir kullanıcı doğrulaması tooverify kullanır. toodo bunu eklemek bir `<ClaimsProvider>` ilkenizin hello uzantısı dosyasında Salesforce için:

1. Çalışma dizininizi hello uzantısının (TrustFrameworkExtensions.xml) açın.
2. Hello bulur `<ClaimsProviders>` bölümü. Yoksa, hello kök düğümü altında oluşturun.
3. Yeni bir ekleme `<ClaimsProvider>`:

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
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

Merhaba altında `<ClaimsProvider>` düğümü:

1. Değiştirmek için hello değer `<Domain>` ayırt eden benzersiz bir değer tooa `<ClaimsProvider>` diğer kimlik sağlayıcılardan gelen.
2. Merhaba değeri güncelleştirme `<DisplayName>` hello tooa görünen adı talep sağlayıcısı. Şu anda, bu değer kullanılmıyor.

### <a name="update-hello-technical-profile"></a>Merhaba teknik profilini güncelleştir

tooget Salesforce, bir SAML belirtecinden Azure AD B2C, Azure Active Directory (Azure AD) ile toocommunicate kullanacağını hello protokolleri tanımlayın. Hello bunu `<TechnicalProfile>` öğesinin `<ClaimsProvider>`:

1. Merhaba Hello Kimliğini güncelleştirme `<TechnicalProfile>` düğümü. Bu kimliği kullanılan toorefer toothis hello İlkesi diğer kısımlarından teknik profilidir.
2. Merhaba değeri güncelleştirme `<DisplayName>`. Bu değer düğmesinde hello oturum açma, oturum açma sayfasında görüntülenir.
3. Merhaba değeri güncelleştirme `<Description>`.
4. Salesforce hello SAML 2.0 protokolünü kullanır. Bu hello değeri olun `<Protocol>` olan **SAML2**.

Güncelleştirme hello `<Metadata>` hello belirli Salesforce hesabınızın XML tooreflect hello ayarlarını önceki bölümünde. Hello XML, hello meta veri değerlerini güncelleştirin:

1. Merhaba değerini güncelleştirmek `<Item Key="PartnerEntity">` daha önce kopyaladığınız hello Salesforce meta veri URL'sine sahip. Biçim aşağıdaki hello sahiptir: 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. Merhaba, `<CryptographicKeys>` bölümünde, her iki örnekleri için güncelleştirme hello değeri `StorageReferenceId` hello anahtarının imzalama sertifikanızın (örneğin, B2C_1A_SAMLSigningCert) toohello adı.

### <a name="upload-hello-extension-file-for-verification"></a>Doğrulama Hello uzantısı dosyasını karşıya yükleme

Böylece Azure AD B2C bilir ilkeniz yapılandırılmıştır nasıl toocommunicate Salesforce ile. Merhaba uzantısının olmadığından sorunları kadar tooverify ilkenizin karşıya yüklemeyi deneyin. tooupload hello uzantısının ilkenizin:

1. Azure AD B2C kiracınızda toohello Git **tüm ilkeler** dikey.
2. Select hello **varsa hello ilkesi üzerine** onay kutusu.
3. Merhaba uzantısının (TrustFrameworkExtensions.xml) karşıya yükleyin. Doğrulama başarısız olmayan emin olun.

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a>Merhaba Salesforce SAML talep sağlayıcısı tooa kullanıcı gezisine kaydetme

Ardından, hello Salesforce SAML kimlik sağlayıcısı tooone kullanıcı Yolculuklar olarak ekleyin. Bu noktada, hello kimlik sağlayıcısı ayarlandı, ancak herhangi bir hello kullanıcı kaydolma veya oturum açma sayfası üzerinde kullanılabilir değil. tooadd hello kimlik sağlayıcısı tooa oturum açma sayfası, ilk olarak, var olan bir şablonu kullanıcı gezisine bir kopyasını oluşturun. Ardından, ayrıca hello Azure AD kimlik sağlayıcısı sahip olması hello şablonu değiştirin.

1. Merhaba temel dosyanın ilkenizin (örneğin, TrustFrameworkBase.xml) açın.
2. Hello bulur `<UserJourneys>` öğesi ve kopyalama hello tüm `<UserJourney>` değeri, "SignUpOrSignIn" kimliğine dahil olmak üzere.
3. Merhaba uzantısının (örneğin, TrustFrameworkExtensions.xml) açın. Hello bulur `<UserJourneys>` öğesi. Merhaba öğe yoksa, bir tane oluşturun.
4. Tüm kopyalanan Yapıştır hello `<UserJourney>` hello alt olarak `<UserJourneys>` öğesi.
5. Merhaba yeni Hello Kimliğini yeniden adlandırma `<UserJourney>` (örneğin, SignUpOrSignUsingContoso).

### <a name="display-hello-identity-provider-button"></a>Görüntü hello kimlik sağlayıcısı düğmesi

Merhaba `<ClaimsProviderSelection>` benzer tooan kimlik sağlayıcısı düğmesi kaydolma veya oturum açma sayfasında bir öğedir. Ekleyerek bir `<ClaimsProviderSelection>` öğesi Salesforce için yeni bir düğme görüntülenir kullanıcı toothis sayfası çıktığında. toodisplay hello kimlik sağlayıcısı düğmesi:

1. Merhaba, `<UserJourney>` oluşturduğunuz, hello Bul `<OrchestrationStep>` ile `Order="1"`.
2. XML aşağıdaki hello ekleyin:

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. Ayarlama `TargetClaimsExchangeId` tooa mantıksal bir değer. Aşağıdaki hello aynı öneririz kuralı başkalarının olarak (örneğin,  *\[ClaimProviderName\]Exchange*).

### <a name="link-hello-identity-provider-button-tooan-action"></a>Bağlantı hello kimlik sağlayıcısı düğmesi tooan eylemi

Bir kimlik sağlayıcısı düğmesi yerinde sahip olduğunuza göre tooan eylem bağlantı kurun. Bu durumda, Azure AD B2C toocommunicate Salesforce tooreceive SAML belirteci ile Merhaba eylem içindir. Merhaba teknik profil için Salesforce SAML bağlayarak Talep sağlayıcı bunu yapabilirsiniz:

1. Merhaba, `<UserJourney>` düğümü, Bul hello `<OrchestrationStep>` ile `Order="2"`.
2. XML aşağıdaki hello ekleyin:

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. Güncelleştirme `Id` toohello aynı değer, sizin için daha önce kullanılan `TargetClaimsExchangeId`.
4. Güncelleştirme `TechnicalProfileReferenceId` toohello `Id` hello teknik daha önce oluşturduğunuz (örneğin, ContosoProfile) profil.

### <a name="upload-hello-updated-extension-file"></a>Merhaba güncelleştirilmiş uzantısı dosyasını karşıya yükle

Değiştirme hello uzantısının yapılır. Kaydet ve bu dosyayı karşıya yükleyin. Tüm Doğrulamalar başarıyla emin olun.

### <a name="update-hello-relying-party-file"></a>Merhaba bağlı olan taraf dosyasını güncelleştirme

Ardından, oluşturduğunuz hello kullanıcı gezisine başlatan hello bağlı olan taraf (RP) dosyasını güncelleştirin:

1. Çalışma dizininizi SignUpOrSignIn.xml kopyası. Sonra (örneğin, SignUpOrSignInWithAAD.xml) yeniden adlandırın.
2. Açık hello yeni dosya ve güncelleştirme hello `PolicyId` için öznitelik `<TrustFrameworkPolicy>` benzersiz bir değere sahip. Bu hello ilkeniz (örneğin, SignUpOrSignInWithAAD) adıdır.
3. Merhaba değiştirme `ReferenceId` özniteliğini `<DefaultUserJourney>` toomatch hello `Id` (örneğin, SignUpOrSignUsingContoso) oluşturduğunuz hello yeni kullanıcı gezisine biri.
4. Yaptığınız değişiklikleri kaydedin ve hello dosyasını karşıya yükleyin.

## <a name="test-and-troubleshoot"></a>Test etme ve sorun giderme

yalnızca, hello Azure portal, karşıya yüklediğiniz tootest hello özel ilke toohello İlkesi dikey penceresine gidin ve ardından **Şimdi Çalıştır**. Başarısız olursa bkz [özel ilke sorunlarını giderme](active-directory-b2c-troubleshoot-custom.md).

## <a name="next-steps"></a>Sonraki adımlar

Çok görüş[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).
