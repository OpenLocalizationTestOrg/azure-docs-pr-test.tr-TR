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
# <a name="azure-active-directory-b2c-modify-sign-up-tooadd-new-claims-and-configure-user-input"></a><span data-ttu-id="c6fdf-103">Azure Active Directory B2C: tooadd yeni talep kaydolma değiştirin ve kullanıcı girişi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-103">Azure Active Directory B2C: Modify sign up tooadd new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="c6fdf-104">Bu makalede, yeni bir kullanıcı tarafından sağlanan girdi (talep) tooyour kaydolma kullanıcı gezisine ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-104">In this article, you will add a new user provided entry (a claim) tooyour signup user journey.</span></span>  <span data-ttu-id="c6fdf-105">Merhaba girişi bir açılır liste yapılandırma yapar ve gerekli olduğunda tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-105">You will configure hello entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="c6fdf-106">Sipi tootrigger test iletimi tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-106">Edited by Sipi tootrigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6fdf-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c6fdf-107">Prerequisites</span></span>

* <span data-ttu-id="c6fdf-108">Tam hello hello makaledeki adımları [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="c6fdf-108">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="c6fdf-109">Merhaba kaydolma/oturum açma kullanıcı gezisine toosignup devam etmeden önce yeni bir yerel hesap sınayın.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-109">Test hello signup/signin user journey toosignup a new local account before proceeding.</span></span>


<span data-ttu-id="c6fdf-110">İlk veri toplama, kullanıcılardan kaydolma/signın elde edilir.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="c6fdf-111">Ek talepleri daha sonra Profil düzenleme kullanıcı Yolculuklar toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="c6fdf-112">Azure AD B2C doğrudan hello kullanıcıdan etkileşimli olarak toplayacağını zaman hello kimlik deneyimi Framework kullanan, `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-112">Anytime Azure AD B2C gathers information directly from hello user interactively, hello Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="c6fdf-113">Bu sağlayıcı kullanılan herhangi bir zamanda hello adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-113">hello steps below apply anytime this provider is used.</span></span>


## <a name="define-hello-claim-its-display-name-and-hello-user-input-type"></a><span data-ttu-id="c6fdf-114">Merhaba talep, görünen ad ve hello kullanıcı girişi türünü tanımlayın</span><span class="sxs-lookup"><span data-stu-id="c6fdf-114">Define hello claim, its display name and hello user input type</span></span>
<span data-ttu-id="c6fdf-115">Kendi şehrini Hello kullanıcıya sor olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-115">Lets ask hello user for their city.</span></span>  <span data-ttu-id="c6fdf-116">Öğe toohello aşağıdaki hello eklemek `<ClaimsSchema>` hello TrustFrameWorkExtensions ilke dosyası öğesinde:</span><span class="sxs-lookup"><span data-stu-id="c6fdf-116">Add hello following element toohello `<ClaimsSchema>` element in hello TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="c6fdf-117">Talep toocustomize hello burada yapabileceğiniz ek seçenekler vardır.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-117">There are additional choices you can make here toocustomize hello claim.</span></span>  <span data-ttu-id="c6fdf-118">İçin tam bir şema, toohello başvuran **kimlik deneyimi Framework Teknik Başvuru Kılavuzu**.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-118">For a full schema, refer toohello **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="c6fdf-119">Bu kılavuz, hello başvuru bölümünde yakında yayımlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-119">This guide will be published soon in hello reference section.</span></span>

* <span data-ttu-id="c6fdf-120">`<DisplayName>`Merhaba kullanıcı dönük tanımlayan bir dize *etiketi*</span><span class="sxs-lookup"><span data-stu-id="c6fdf-120">`<DisplayName>` is a string that defines hello user-facing *label*</span></span>

* <span data-ttu-id="c6fdf-121">`<UserHelpText>`gerekenden hello anlamasına yardımcı olur</span><span class="sxs-lookup"><span data-stu-id="c6fdf-121">`<UserHelpText>` helps hello user understand what is required</span></span>

* <span data-ttu-id="c6fdf-122">`<UserInputType>`Merhaba aşağıdaki dört seçenekten aşağıda vurgulanan:</span><span class="sxs-lookup"><span data-stu-id="c6fdf-122">`<UserInputType>` has hello following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="c6fdf-123">`RadioSingleSelectduration`-Tek seçim zorlar.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="c6fdf-124">`DropdownSingleSelect`-Yalnızca geçerli değer hello seçilmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-124">`DropdownSingleSelect` - Allows hello selection of only valid value.</span></span>

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


* <span data-ttu-id="c6fdf-126">`CheckboxMultiSelect`İçin bir veya daha fazla değer Hello seçilmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-126">`CheckboxMultiSelect` Allows for hello selection of one or more values.</span></span>

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

## <a name="add-hello-claim-toohello-sign-upsign-in-user-journey"></a><span data-ttu-id="c6fdf-128">Merhaba talep toohello oturum yukarı/kullanıcı gezisine ekleme</span><span class="sxs-lookup"><span data-stu-id="c6fdf-128">Add hello claim toohello sign up/sign in user journey</span></span>

1. <span data-ttu-id="c6fdf-129">Merhaba talep olarak ekleme bir `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (Merhaba TrustFrameworkBase ilke dosyasında bulunur).</span><span class="sxs-lookup"><span data-stu-id="c6fdf-129">Add hello claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` toohello TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in hello TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="c6fdf-130">Bu TechnicalProfile hello SelfAssertedAttributeProvider kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-130">Note this TechnicalProfile uses hello SelfAssertedAttributeProvider.</span></span>

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

2. <span data-ttu-id="c6fdf-131">Merhaba talep toohello AAD UserWriteUsingLogonEmail olarak ekleme bir `<PersistedClaim ClaimTypeReferenceId="city" />` hello kullanıcıdan topladıktan sonra toowrite hello talep toohello bir AAD dizini.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-131">Add hello claim toohello AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` toowrite hello claim toohello AAD directory after collecting it from hello user.</span></span> <span data-ttu-id="c6fdf-132">Değil toopersist hello talep hello dizininde ileride kullanılmak üzere tercih ederseniz, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-132">You may skip this step if you prefer not toopersist hello claim in hello directory for future use.</span></span>

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

3. <span data-ttu-id="c6fdf-133">Merhaba talep toohello hello dizininden olarak bir kullanıcı oturum açtığında okuyan TechnicalProfile eklemek bir`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="c6fdf-133">Add hello claim toohello TechnicalProfile that reads from hello directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

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

4. <span data-ttu-id="c6fdf-134">Merhaba eklemek `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP ilke dosyası bu talep başarılı kullanıcı gezisine sonra hello belirteçte toohello uygulama gönderilen şekilde SignUporSignIn.xml.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-134">Add hello `<OutputClaim ClaimTypeReferenceId="city" />` toohello RP policy file SignUporSignIn.xml so this claim is sent toohello application in hello token after a successful user journey.</span></span>

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

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="c6fdf-135">"Şimdi Çalıştır" kullanarak test hello özel İlkesi</span><span class="sxs-lookup"><span data-stu-id="c6fdf-135">Test hello custom policy using "Run Now"</span></span>

1. <span data-ttu-id="c6fdf-136">Açık hello **Azure AD B2C dikey** ve çok gidin**kimlik deneyimi Framework > özel ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-136">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="c6fdf-137">Karşıya yüklediğiniz hello özel ilkesini seçin ve hello tıklayın **Şimdi Çalıştır** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-137">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
3. <span data-ttu-id="c6fdf-138">Bir e-posta adresi kullanarak yukarı mümkün toosign olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-138">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="c6fdf-139">test modunda Hello kaydolma ekran benzer toothis görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c6fdf-139">hello signup screen in test mode should look similar toothis:</span></span>

![Değiştirilen kayıt seçeneğinin ekran görüntüsü](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="c6fdf-141">Merhaba belirteci geri tooyour uygulama artık hello içerecektir `city` aşağıda gösterildiği gibi talep</span><span class="sxs-lookup"><span data-stu-id="c6fdf-141">hello token back tooyour application will now include hello `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="c6fdf-142">İsteğe bağlı: Kaydolma gezisine gelen Kaldır e-posta doğrulama</span><span class="sxs-lookup"><span data-stu-id="c6fdf-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="c6fdf-143">tooskip e-posta doğrulama hello İlkesi Yazar tooremove seçebilirsiniz `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-143">tooskip email verification, hello policy author can choose tooremove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="c6fdf-144">Merhaba e-posta adresi gerekli ancak, "Gerekli olmadıkça" doğrulanmadı = true kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-144">hello email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="c6fdf-145">Bu seçenek, kullanım durumları için uygun olup olmadığını dikkatlice!</span><span class="sxs-lookup"><span data-stu-id="c6fdf-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="c6fdf-146">E-posta hello varsayılan olarak etkindir doğrulandı `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` hello TrustFrameworkBase ilke dosyasında hello başlangıç paketi:</span><span class="sxs-lookup"><span data-stu-id="c6fdf-146">Verified email is enabled by default in hello `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in hello TrustFrameworkBase policy file in hello starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="c6fdf-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6fdf-147">Next steps</span></span>

<span data-ttu-id="c6fdf-148">Merhaba yeni talep toohello akışları sosyal hesap oturum açma TechnicalProfiles aşağıda listelenen hello değiştirerek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-148">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed below.</span></span> <span data-ttu-id="c6fdf-149">Bunlar sosyal ve Federasyon hesap oturumu açma toowrite tarafından kullanılan ve Bulucu hello gibi hello alternativeSecurityId kullanılarak hello kullanıcı verilerini okuyun.</span><span class="sxs-lookup"><span data-stu-id="c6fdf-149">These are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
