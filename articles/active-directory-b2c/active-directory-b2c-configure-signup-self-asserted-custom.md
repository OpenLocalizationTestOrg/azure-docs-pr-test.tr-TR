---
title: "Azure Active Directory B2C: oturum özel ilkelerinde değiştirmek ve kendini sağlayıcısı uygulanan yapılandırın"
description: "Kaydolun ve kullanıcı girişini yapılandırmak bir kılavuz ekleme talepleri"
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
ms.openlocfilehash: 64b9d904d7d070052e125b479f4719d208c9ff85
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2017
---
# <a name="azure-active-directory-b2c-modify-sign-up-to-add-new-claims-and-configure-user-input"></a><span data-ttu-id="f9c93-103">Azure Active Directory B2C: yeni talep eklemek ve kullanıcı girişi yapılandırmak için yukarı oturum değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f9c93-103">Azure Active Directory B2C: Modify sign up to add new claims and configure user input.</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="f9c93-104">Bu makalede, yeni bir kullanıcı tarafından sağlanan giriş (talep) kaydolma kullanıcı Yolculuğunuzun ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c93-104">In this article, you will add a new user provided entry (a claim) to your signup user journey.</span></span>  <span data-ttu-id="f9c93-105">Giriş bir açılır liste yapılandırma yapar ve gerekli olduğunda tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f9c93-105">You will configure the entry as a dropdown, and define if it is required.</span></span>

<span data-ttu-id="f9c93-106">Test iletimi tetiklemek için Sipi tarafından düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="f9c93-106">Edited by Sipi to trigger test handoff.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9c93-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f9c93-107">Prerequisites</span></span>

* <span data-ttu-id="f9c93-108">Makalesindeki adımları [özel ilkeleri ile çalışmaya başlama](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f9c93-108">Complete the steps in the article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>  <span data-ttu-id="f9c93-109">Kaydolma devam etmeden önce yeni bir yerel hesap için kaydolma/oturum açma kullanıcı gezisine test edin.</span><span class="sxs-lookup"><span data-stu-id="f9c93-109">Test the signup/signin user journey to signup a new local account before proceeding.</span></span>


<span data-ttu-id="f9c93-110">İlk veri toplama, kullanıcılardan kaydolma/signın elde edilir.</span><span class="sxs-lookup"><span data-stu-id="f9c93-110">Gathering initial data from your users is achieved via signup/signin.</span></span>  <span data-ttu-id="f9c93-111">Ek talepleri daha sonra Profil düzenleme kullanıcı Yolculuklar toplanabilir.</span><span class="sxs-lookup"><span data-stu-id="f9c93-111">Additional claims can be gathered later via profile edit user journeys.</span></span> <span data-ttu-id="f9c93-112">Azure AD B2C doğrudan kullanıcıdan etkileşimli olarak toplayacağını zaman kimlik deneyimi çerçevesi kullanır, `selfasserted provider`.</span><span class="sxs-lookup"><span data-stu-id="f9c93-112">Anytime Azure AD B2C gathers information directly from the user interactively, the Identity Experience Framework uses its `selfasserted provider`.</span></span> <span data-ttu-id="f9c93-113">Bu sağlayıcı kullanılan herhangi bir zamanda aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f9c93-113">The steps below apply anytime this provider is used.</span></span>


## <a name="define-the-claim-its-display-name-and-the-user-input-type"></a><span data-ttu-id="f9c93-114">Talep, görünen adını ve kullanıcı giriş türünü tanımlayın</span><span class="sxs-lookup"><span data-stu-id="f9c93-114">Define the claim, its display name and the user input type</span></span>
<span data-ttu-id="f9c93-115">Kendi şehrini kaldırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9c93-115">Lets ask the user for their city.</span></span>  <span data-ttu-id="f9c93-116">Aşağıdaki öğeyi ekleyin `<ClaimsSchema>` TrustFrameWorkExtensions ilke dosyası öğesinde:</span><span class="sxs-lookup"><span data-stu-id="f9c93-116">Add the following element to the `<ClaimsSchema>` element in the TrustFrameWorkExtensions policy file:</span></span>

```xml
<ClaimType Id="city">
  <DisplayName>city</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```
<span data-ttu-id="f9c93-117">Burada talep özelleştirmek için yapabileceğiniz ek seçenekler vardır.</span><span class="sxs-lookup"><span data-stu-id="f9c93-117">There are additional choices you can make here to customize the claim.</span></span>  <span data-ttu-id="f9c93-118">İçin tam bir şema, başvurmak **kimlik deneyimi Framework Teknik Başvuru Kılavuzu**.</span><span class="sxs-lookup"><span data-stu-id="f9c93-118">For a full schema, refer to the **Identity Experience Framework Technical Reference Guide**.</span></span>  <span data-ttu-id="f9c93-119">Bu kılavuz başvuru bölümünde yakında yayımlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="f9c93-119">This guide will be published soon in the reference section.</span></span>

* <span data-ttu-id="f9c93-120">`<DisplayName>`Kullanıcı dönük tanımlayan bir dize *etiketi*</span><span class="sxs-lookup"><span data-stu-id="f9c93-120">`<DisplayName>` is a string that defines the user-facing *label*</span></span>

* <span data-ttu-id="f9c93-121">`<UserHelpText>`gerekenden anlamasına yardımcı olur</span><span class="sxs-lookup"><span data-stu-id="f9c93-121">`<UserHelpText>` helps the user understand what is required</span></span>

* <span data-ttu-id="f9c93-122">`<UserInputType>`Aşağıdaki dört seçenekten aşağıda vurgulanan:</span><span class="sxs-lookup"><span data-stu-id="f9c93-122">`<UserInputType>` has the following four options highlighted below:</span></span>
    * `TextBox`
```xml
<ClaimType Id="city">
  <DisplayName>city where you work</DisplayName>
  <DataType>string</DataType>
  <UserHelpText>Your city</UserHelpText>
  <UserInputType>TextBox</UserInputType>
</ClaimType>
```

    * <span data-ttu-id="f9c93-123">`RadioSingleSelectduration`-Tek seçim zorlar.</span><span class="sxs-lookup"><span data-stu-id="f9c93-123">`RadioSingleSelectduration` - Enforces a single selection.</span></span>
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

    * <span data-ttu-id="f9c93-124">`DropdownSingleSelect`-Yalnızca geçerli değer seçimine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f9c93-124">`DropdownSingleSelect` - Allows the selection of only valid value.</span></span>

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


* <span data-ttu-id="f9c93-126">`CheckboxMultiSelect`İçin bir veya daha fazla değer seçimine izin verir.</span><span class="sxs-lookup"><span data-stu-id="f9c93-126">`CheckboxMultiSelect` Allows for the selection of one or more values.</span></span>

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

## <a name="add-the-claim-to-the-sign-upsign-in-user-journey"></a><span data-ttu-id="f9c93-128">Oturum açma için talep ekleme yukarı/kullanıcı gezisine oturum</span><span class="sxs-lookup"><span data-stu-id="f9c93-128">Add the claim to the sign up/sign in user journey</span></span>

1. <span data-ttu-id="f9c93-129">Talep olarak ekleme bir `<OutputClaim ClaimTypeReferenceId="city"/>` TechnicalProfile için `LocalAccountSignUpWithLogonEmail` (TrustFrameworkBase ilke dosyasında bulunur).</span><span class="sxs-lookup"><span data-stu-id="f9c93-129">Add the claim as an `<OutputClaim ClaimTypeReferenceId="city"/>` to the TechnicalProfile `LocalAccountSignUpWithLogonEmail` (found in the TrustFrameworkBase policy file).</span></span>  <span data-ttu-id="f9c93-130">Bu TechnicalProfile SelfAssertedAttributeProvider kullandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f9c93-130">Note this TechnicalProfile uses the SelfAssertedAttributeProvider.</span></span>

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
      <!-- Optional claims, to be collected from the user -->
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

2. <span data-ttu-id="f9c93-131">Talep AAD UserWriteUsingLogonEmail için ekleme bir `<PersistedClaim ClaimTypeReferenceId="city" />` kullanıcıdan topladıktan sonra talep AAD dizinine yazılacak.</span><span class="sxs-lookup"><span data-stu-id="f9c93-131">Add the claim to the AAD-UserWriteUsingLogonEmail as a `<PersistedClaim ClaimTypeReferenceId="city" />` to write the claim to the AAD directory after collecting it from the user.</span></span> <span data-ttu-id="f9c93-132">Dizinde talep gelecekte kullanım için kalıcı olmayan tercih ediyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9c93-132">You may skip this step if you prefer not to persist the claim in the directory for future use.</span></span>

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

3. <span data-ttu-id="f9c93-133">Farklı bir kullanıcı oturum açtığında, dizinden okuma TechnicalProfile için talep ekleme bir`<OutputClaim ClaimTypeReferenceId="city" />`</span><span class="sxs-lookup"><span data-stu-id="f9c93-133">Add the claim to the TechnicalProfile that reads from the directory when a user logs in as an `<OutputClaim ClaimTypeReferenceId="city" />`</span></span>

  ```xml
  <TechnicalProfile Id="AAD-UserReadUsingEmailAddress">
    <Metadata>
      <Item Key="Operation">Read</Item>
      <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
      <Item Key="UserMessageIfClaimsPrincipalDoesNotExist">An account could not be found for the provided user ID.</Item>
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

4. <span data-ttu-id="f9c93-134">Ekleme `<OutputClaim ClaimTypeReferenceId="city" />` bu talep belirteci başarılı kullanıcı gezisine sonra uygulama gönderilir şekilde RP ilkeyi SignUporSignIn.xml dosya.</span><span class="sxs-lookup"><span data-stu-id="f9c93-134">Add the `<OutputClaim ClaimTypeReferenceId="city" />` to the RP policy file SignUporSignIn.xml so this claim is sent to the application in the token after a successful user journey.</span></span>

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

## <a name="test-the-custom-policy-using-run-now"></a><span data-ttu-id="f9c93-135">"Şimdi Çalıştır" kullanarak özel ilkeyi test etme</span><span class="sxs-lookup"><span data-stu-id="f9c93-135">Test the custom policy using "Run Now"</span></span>

1. <span data-ttu-id="f9c93-136">Açık **Azure AD B2C dikey** gidin **kimlik deneyimi Framework > özel ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="f9c93-136">Open the **Azure AD B2C Blade** and navigate to **Identity Experience Framework > Custom policies**.</span></span>
2. <span data-ttu-id="f9c93-137">Karşıya yüklenen ve'ı tıklatın özel ilkeyi seçin **Şimdi Çalıştır** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="f9c93-137">Select the custom policy that you uploaded, and click the **Run now** button.</span></span>
3. <span data-ttu-id="f9c93-138">Bir e-posta adresi kullanarak kaydolabilirsiniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9c93-138">You should be able to sign up using an email address.</span></span>

<span data-ttu-id="f9c93-139">Test modunda kaydolma ekran şuna benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="f9c93-139">The signup screen in test mode should look similar to this:</span></span>

![Değiştirilen kayıt seçeneğinin ekran görüntüsü](./media/active-directory-b2c-configure-signup-self-asserted-custom/signup-with-city-claim-dropdown-example.png)

  <span data-ttu-id="f9c93-141">Belirtece uygulamanız şimdi içerecektir `city` aşağıda gösterildiği gibi talep</span><span class="sxs-lookup"><span data-stu-id="f9c93-141">The token back to your application will now include the `city` claim as shown below</span></span>
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

## <a name="optional-remove-email-verification-from-signup-journey"></a><span data-ttu-id="f9c93-142">İsteğe bağlı: Kaydolma gezisine gelen Kaldır e-posta doğrulama</span><span class="sxs-lookup"><span data-stu-id="f9c93-142">Optional: Remove email verification from signup journey</span></span>

<span data-ttu-id="f9c93-143">E-posta doğrulama atlamak için ilke Yazar kaldırmayı seçebilirsiniz `PartnerClaimType="Verified.Email"`.</span><span class="sxs-lookup"><span data-stu-id="f9c93-143">To skip email verification, the policy author can choose to remove `PartnerClaimType="Verified.Email"`.</span></span> <span data-ttu-id="f9c93-144">E-posta adresi gerekli ancak, "Gerekli olmadıkça" doğrulanmadı = true kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="f9c93-144">The email address will be required but not verified, unless “Required” = true is removed.</span></span>  <span data-ttu-id="f9c93-145">Bu seçenek, kullanım durumları için uygun olup olmadığını dikkatlice!</span><span class="sxs-lookup"><span data-stu-id="f9c93-145">Carefully consider if this option is right for your use cases!</span></span>

<span data-ttu-id="f9c93-146">E-posta, varsayılan olarak etkindir doğrulandı `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` başlangıç paketi TrustFrameworkBase ilke dosyasında:</span><span class="sxs-lookup"><span data-stu-id="f9c93-146">Verified email is enabled by default in the `<TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">` in the TrustFrameworkBase policy file in the starter pack:</span></span>
```xml
<OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="Verified.Email" Required="true" />
```

## <a name="next-steps"></a><span data-ttu-id="f9c93-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9c93-147">Next steps</span></span>

<span data-ttu-id="f9c93-148">Akışlar için yeni talep sosyal hesap oturum açma, aşağıda listelenen TechnicalProfiles değiştirerek ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f9c93-148">Add the new claim to the flows for social account logins by changing the TechnicalProfiles listed below.</span></span> <span data-ttu-id="f9c93-149">Kullanıcı verileri Bulucu alternativeSecurityId kullanarak okuyup yazmak için bunlar sosyal ve Federasyon hesap oturumu açma tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f9c93-149">These are used by social/federated account logins to write and read the user data using the alternativeSecurityId as the locator.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">
<TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```
