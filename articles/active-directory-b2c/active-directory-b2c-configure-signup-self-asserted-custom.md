---
title: "Azure Active Directory B2C: oturum özel ilkelerinde değiştirmek ve kendini sağlayıcısı uygulanan yapılandırın"
description: "Ekleme bir kılavuz yukarı toosign talepleri ve hello kullanıcı girişi yapılandırın"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: tbd
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/29/2017
ms.author: joroja
ms.openlocfilehash: c31d737263fef3e771bdf451b809b0ca522c8fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a>Azure Active Directory B2C: tooadd yeni talep kaydolma değiştirin ve kullanıcı girişi yapılandırın.

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

Bu makalede, yeni bir kullanıcı tarafından sağlanan girdi (talep) tooyour kaydolma kullanıcı gezisine ekleyeceksiniz.  Merhaba girişi bir açılır liste yapılandırma yapar ve gerekli olduğunda tanımlayın.

Sipi tootrigger test iletimi tarafından düzenlenebilir.

## <a name="prerequisites"></a>Ön koşullar

* Tam hello hello makaledeki adımları [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md).  Merhaba kaydolma/oturum açma kullanıcı gezisine toosignup devam etmeden önce yeni bir yerel hesap sınayın.


İlk veri toplama, kullanıcılardan kaydolma/signın elde edilir.  Ek talepleri daha sonra Profil düzenleme kullanıcı Yolculuklar toplanabilir. Azure AD B2C doğrudan hello kullanıcıdan etkileşimli olarak toplayacağını zaman hello kimlik deneyimi Framework kullanan, `selfasserted provider`. Bu sağlayıcı kullanılan herhangi bir zamanda hello adımları uygulayın.


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a>Merhaba talep, görünen ad ve hello kullanıcı girişi türünü tanımlayın
Kendi şehrini Hello kullanıcıya sor olanak sağlar.  Öğe toohello aşağıdaki hello eklemek `<ClaimsSchema>` hello TrustFrameWorkExtensions ilke dosyası öğesinde:

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
Talep toocustomize hello burada yapabileceğiniz ek seçenekler vardır.  İçin tam bir şema, toohello başvuran **kimlik deneyimi Framework Teknik Başvuru Kılavuzu**.  Bu kılavuz, hello başvuru bölümünde yakında yayımlanacaktır.

* `<DisplayName>`Merhaba kullanıcı dönük tanımlayan bir dize *etiketi*

* `<UserHelpText>`gerekenden hello anlamasına yardımcı olur

* `<UserInputType>`Merhaba aşağıdaki dört seçenekten aşağıda vurgulanan:
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * `RadioSingleSelectduration`-Tek seçim zorlar.
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>RadioSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

    * `DropdownSingleSelect`-Yalnızca geçerli değer hello seçilmesine izin verir.

![Aşağı açılan seçeneği ekran görüntüsü](./media/active-directory-b2c-configure-signup-self-asserted-custom/dropdown-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserInputType>DropdownSingleSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```


* `CheckboxMultiSelect`İçin bir veya daha fazla değer Hello seçilmesine izin verir.

![Çoklu seçeneğinin ekran görüntüsü](./media/active-directory-b2c-configure-signup-self-asserted-custom/multiselect-menu-example.png)


```xml
<ClaimType Id="city">
  <DisplayName>Receive updates from which cities?</DisplayName>
  <DataType>string</DataType>
  <UserInputType>CheckboxMultiSelect</UserInputType>
  <Restriction>
    <Enumeration Text="Bellevue" Value="bellevue" SelectByDefault="false" />
    <Enumeration Text="Redmond" Value="redmond" SelectByDefault="false" />
    <Enumeration Text="Kirkland" Value="kirkland" SelectByDefault="false" />
  </Restriction>
</ClaimType>
```

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a>Merhaba talep toohello oturum yukarı/kullanıcı gezisine ekleme

1. Merhaba talep olarak ekleme bir `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (Merhaba TrustFrameworkBase ilke dosyasında bulunur).  Bu TechnicalProfile hello SelfAssertedAttributeProvider kullandığına dikkat edin.

  ```xml
  <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
    <DisplayName>Email signup</DisplayName>
    <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
    <Metadata>
      <Item Key="IpAddressClaimReferenceId">IpAddress</Item>
      <Item Key="ContentDefinitionReferenceId">api.localaccountsignup</Item>
      <Item Key="language.button_continue">Create</Item>
    </Metadata>
    <CryptographicKeys>
      <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
    </CryptographicKeys>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" />
    </InputClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
      <OutputClaim ClaimTypeReferenceId="newPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="reenterPassword" Required="true" />
      <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" />
      <OutputClaim ClaimTypeReferenceId="newUser" />
      <!-- Optional claims, toobe collected from hello user -->
      <OutputClaim ClaimTypeReferenceId="givenName" />
      <OutputClaim ClaimTypeReferenceId="surName" />
      <OutputClaim ClaimTypeReferenceId="city"/>
    </OutputClaims>
    <ValidationTechnicalProfiles>
      <ValidationTechnicalProfile ReferenceId="AAD-UserWriteUsingLogonEmail" />
    </ValidationTechnicalProfiles>
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

2. Merhaba talep toohello AAD UserWriteUsingLogonEmail olarak ekleme bir `<PersistedClaim ClaimTypeReferenceId="city" />` hello kullanıcıdan topladıktan sonra toowrite hello talep toohello bir AAD dizini. Değil toopersist hello talep hello dizininde ileride kullanılmak üzere tercih ederseniz, bu adımı atlayabilirsiniz.

  ```xml
  <!-- Technical profiles for local accounts -->
  <TechnicalProfile Id="AAD-UserWriteUsingLogonEmail">
    <Metadata>
      <Item Key="Operation">Write</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">true</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" Required="true" />
    </InputClaims>
    <PersistedClaims>
      <!-- Required claims -->
      <PersistedClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames.emailAddress" />
      <PersistedClaim ClaimTypeReferenceId="newPassword" PartnerClaimType="password" />
      <PersistedClaim ClaimTypeReferenceId="displayName" DefaultValue="unknown" />
      <PersistedClaim ClaimTypeReferenceId="passwordPolicies" DefaultValue="DisablePasswordExpiration" />
      <!-- Optional claims. -->
      <PersistedClaim ClaimTypeReferenceId="givenName" />
      <PersistedClaim ClaimTypeReferenceId="surname" />
      <PersistedClaim ClaimTypeReferenceId="city" />
    </PersistedClaims>
    <OutputClaims>
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="newUser" PartnerClaimType="newClaimsPrincipalCreated" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
    <UseTechnicalProfileForSessionManagement ReferenceId="SM-AAD" />
  </TechnicalProfile>
  ```

3. Merhaba talep toohello hello dizininden olarak bir kullanıcı oturum açtığında okuyan TechnicalProfile eklemek bir`<OutputClaim ClaimTypeReferenceId="city" />`

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for hello provided user ID.</Item>
    </Metadata>
    <IncludeInSso>false</IncludeInSso>
    <InputClaims>
      <InputClaim ClaimTypeReferenceId="email" PartnerClaimType="signInNames" Required="true" />
    </InputClaims>
    <OutputClaims>
      <!-- Required claims -->
      <OutputClaim ClaimTypeReferenceId="objectId" />
      <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="localAccountAuthentication" />
      <!-- Optional claims -->
      <OutputClaim ClaimTypeReferenceId="userPrincipalName" />
      <OutputClaim ClaimTypeReferenceId="displayName" />
      <OutputClaim ClaimTypeReferenceId="otherMails" />
      <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
      <OutputClaim ClaimTypeReferenceId="city" />
    </OutputClaims>
    <IncludeTechnicalProfile ReferenceId="AAD-Common" />
  </TechnicalProfile>
  ```

4. Merhaba eklemek `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP ilke dosyası bu talep başarılı kullanıcı gezisine sonra hello belirteçte toohello uygulama gönderilen şekilde SignUporSignIn.xml.

  ```xml
  <RelyingParty>
    <DefaultUserJourney ReferenceId="SignUpOrSignIn" />
    <TechnicalProfile Id="PolicyProfile">
      <DisplayName>PolicyProfile</DisplayName>
      <Protocol Name="OpenIdConnect" />
      <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="displayName" />
        <OutputClaim ClaimTypeReferenceId="givenName" />
        <OutputClaim ClaimTypeReferenceId="surname" />
        <OutputClaim ClaimTypeReferenceId="email" />
        <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" />
        <OutputClaim ClaimTypeReferenceId="city" />
      </OutputClaims>
      <SubjectNamingInfo ClaimType="sub" />
    </TechnicalProfile>
  </RelyingParty>
  ```

## <a name="test-hello-custom-policy-using-run-now"></a>"Şimdi Çalıştır" kullanarak test hello özel İlkesi

1. Açık hello **Azure AD B2C dikey** ve çok gidin**kimlik deneyimi Framework > özel ilkeleri**.
2. Karşıya yüklediğiniz hello özel ilkesini seçin ve hello tıklayın **Şimdi Çalıştır** düğmesi.
3. Bir e-posta adresi kullanarak yukarı mümkün toosign olmalıdır.

test modunda Hello kaydolma ekran benzer toothis görünmelidir:

![Değiştirilen kayıt seçeneğinin ekran görüntüsü](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  Merhaba belirteci geri tooyour uygulama artık hello içerecektir `city` aşağıda gösterildiği gibi talep
```json
{
  "exp": 1493596822,
  "nbf": 1493593222,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "9c2a3a9e-ac65-4e46-a12d-9557b63033a9",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustf_signup_signin",
  "nonce": "defaultNonce",
  "iat": 1493593222,
  "auth_time": 1493593222,
  "email": "joe@outlook.com",
  "given_name": "Joe",
  "family_name": "Ras",
  "city": "Bellevue",
  "name": "unknown"
}
```

## <a name="optional-remove-email-verification-from-signup-journey"></a>İsteğe bağlı: Kaydolma gezisine gelen Kaldır e-posta doğrulama

tooskip e-posta doğrulama hello İlkesi Yazar tooremove seçebilirsiniz `PartnerClaimType="Verified.Email"`. Merhaba e-posta adresi gerekli ancak, "Gerekli olmadıkça" doğrulanmadı = true kaldırılır.  Bu seçenek, kullanım durumları için uygun olup olmadığını dikkatlice!

E-posta hello varsayılan olarak etkindir doğrulandı `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` hello TrustFrameworkBase ilke dosyasında hello başlangıç paketi:
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a>Sonraki adımlar

Merhaba yeni talep toohello akışları sosyal hesap oturum açma TechnicalProfiles aşağıda listelenen hello değiştirerek ekleyin. Bunlar sosyal ve Federasyon hesap oturumu açma toowrite tarafından kullanılan ve Bulucu hello gibi hello alternativeSecurityId kullanılarak hello kullanıcı verilerini okuyun.
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
