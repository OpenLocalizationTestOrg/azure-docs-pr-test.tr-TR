---
title: "Azure Active Directory B2C: SSO ve belirteç özelleştirme özel ilkeler ile yönetme | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/02/2017
ms.author: sama
ms.openlocfilehash: 8f5703d15766f221517cd89352d41685652d32d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="59deb-102">Azure Active Directory B2C: SSO ve belirteç özelleştirme özel ilkeler ile yönetme</span><span class="sxs-lookup"><span data-stu-id="59deb-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="59deb-103">Özel ilkelerini kullanma belirteci, oturum ve çoklu oturum açma (SSO) yapılandırmaları üzerinden aynı denetimi gibi yerleşik ilkeleri aracılığıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="59deb-103">Using custom policies provides you the same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="59deb-104">Her ayar yaptıklarını öğrenmek için lütfen belgelere bakın [burada](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="59deb-104">To learn what each setting does, please see the documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="59deb-105">Belirteç yaşam süresi ve talep yapılandırma</span><span class="sxs-lookup"><span data-stu-id="59deb-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="59deb-106">Üzerinde belirteci, yaşam süresi ayarları değiştirmek için eklemeniz gerekir bir `<ClaimsProviders>` etkisi istediğiniz ilkeyi bağlı olan taraf dosyasındaki öğesi.</span><span class="sxs-lookup"><span data-stu-id="59deb-106">To change the settings on your token lifetimes, you need to add a `<ClaimsProviders>` element in the relying party file of the policy you want to impact.</span></span>  <span data-ttu-id="59deb-107">`<ClaimsProviders>` Bir alt öğedir `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="59deb-107">The `<ClaimsProviders>` element is a child of the `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="59deb-108">İçinde belirteç yaşam süreleri etkiler bilgileri koymak gerekir.</span><span class="sxs-lookup"><span data-stu-id="59deb-108">Inside you'll need to put the information that affects your token lifetimes.</span></span>  <span data-ttu-id="59deb-109">XML şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="59deb-109">The XML looks like this:</span></span>

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

<span data-ttu-id="59deb-110">**Erişim belirteci yaşam süreleri** erişim belirteç ömrü içindeki değeri değiştirerek değiştirilebilir `<Item>` anahtarla "token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="59deb-110">**Access token lifetimes** The access token lifetime can be changed by modifying the value inside the `<Item>` with the Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="59deb-111">Varsayılan yerleşik 3600 saniye (60 dakika) değerdir.</span><span class="sxs-lookup"><span data-stu-id="59deb-111">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="59deb-112">**Kimliği belirteç ömrü** kimliği belirteç ömrü içindeki değeri değiştirerek değiştirilebilir `<Item>` anahtarla "id_token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="59deb-112">**ID token lifetime** The ID token lifetime can be changed by modifying the value inside the `<Item>` with the Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="59deb-113">Varsayılan yerleşik 3600 saniye (60 dakika) değerdir.</span><span class="sxs-lookup"><span data-stu-id="59deb-113">The default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="59deb-114">**Belirteç ömrü yenileme** yenileme belirteç ömrü içindeki değeri değiştirerek değiştirilebilir `<Item>` anahtarla "refresh_token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="59deb-114">**Refresh token lifetime** The refresh token lifetime can be changed by modifying the value inside the `<Item>` with the Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="59deb-115">Yerleşik varsayılan değeri 1209600 (14 gün) saniyedir.</span><span class="sxs-lookup"><span data-stu-id="59deb-115">The default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="59deb-116">**Belirteç kayan pencere ömrü yenileme** yenileme belirtecinizi kayan bir pencere ömrü ayarlamak istiyorsanız içindeki değeri değiştirmek `<Item>` anahtarla "rolling_refresh_token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="59deb-116">**Refresh token sliding window lifetime** If you would like to set a sliding window lifetime to your refresh token, modify the value inside `<Item>` with the Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="59deb-117">7776000 (90 gün) içinde yerleşik varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="59deb-117">The default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="59deb-118">Bir kayan için enfore istemiyorsanız, Pencere Ömrü bu satırla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="59deb-118">If you don't want to enfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="59deb-119">**Veren (ISS) talep** içindeki değeri veren (ISS) talep değiştirmek isterseniz, değiştirmek `<Item>` anahtarıyla = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="59deb-119">**Issuer (iss) claim** If you want to change the Issuer (iss) claim, modify the value inside the `<Item>` with the Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="59deb-120">Geçerli değerler `AuthorityAndTenantGuid` ve `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="59deb-120">The applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="59deb-121">**Ayar talep İlkesi Kimliğini temsil eden** bu değeri ayarlamak için Seçenekler şunlardır: TFP (güven framework ilke) ve ACR (kimlik doğrulaması bağlamı başvuru).</span><span class="sxs-lookup"><span data-stu-id="59deb-121">**Setting claim representing policy ID** The options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="59deb-122">Bu TFP için ayarı öneririz, bunu yapmak için olun `<Item>` ile anahtar = "AuthenticationContextReferenceClaimPattern" var ve değer `None`.</span><span class="sxs-lookup"><span data-stu-id="59deb-122">We recommend setting this to TFP, to do this, ensure the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern" exists and the value is `None`.</span></span>
<span data-ttu-id="59deb-123">İçinde `<OutputClaims>` öğesi, bu öğe ekleyin:</span><span class="sxs-lookup"><span data-stu-id="59deb-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="59deb-124">ACR için kaldırma `<Item>` anahtarıyla = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="59deb-124">For ACR, remove the `<Item>` with the Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="59deb-125">**Konu (alt) talep** için geçiş yapmak istiyorsanız bu seçeneği objectID için alınır `Not Supported`, aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="59deb-125">**Subject (sub) claim** This option is defaulted to ObjectID, if you would like to switch this to `Not Supported`, do the following:</span></span>

<span data-ttu-id="59deb-126">Bu satırı değiştirin</span><span class="sxs-lookup"><span data-stu-id="59deb-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="59deb-127">Bu satırla:</span><span class="sxs-lookup"><span data-stu-id="59deb-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="59deb-128">Oturum davranışını ve SSO</span><span class="sxs-lookup"><span data-stu-id="59deb-128">Session behavior and SSO</span></span>
<span data-ttu-id="59deb-129">Oturum davranışını ve SSO yapılandırmaları değiştirmek için eklemeniz gerekir bir `<UserJourneyBehaviors>` öğesinin içine `<RelyingParty>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="59deb-129">To change your session behavior and SSO configurations, you need to add a `<UserJourneyBehaviors>` element inside of the `<RelyingParty>` element.</span></span>  <span data-ttu-id="59deb-130">`<UserJourneyBehaviors>` Öğesi hemen uymalıdır `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="59deb-130">The `<UserJourneyBehaviors>` element must immediately follow the `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="59deb-131">İçini, `<UserJourneyBehavors>` öğesi aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="59deb-131">The inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="59deb-132">**Çoklu oturum açma (SSO) yapılandırma** değerini değiştirmenize gerek tek oturum açma yapılandırmasını değiştirmek için `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="59deb-132">**Single sign-on (SSO) configuration** To change the single sign-on configuration, you need to modify the value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="59deb-133">Geçerli değerler `Tenant`, `Application`, `Policy` ve `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="59deb-133">The applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="59deb-134">**Web uygulaması oturum yaşam süresi (dakika)** değiştirmek için web uygulaması oturum yaşam değerini değiştirmek ihtiyacınız `<SessionExpiryInSeconds>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="59deb-134">**Web app session lifetime (minutes)** To change the the web app session lifetime, you need to modify value of the `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="59deb-135">Varsayılan değer yerleşik ilkelerinde 86400 (1440 dakika) saniyedir.</span><span class="sxs-lookup"><span data-stu-id="59deb-135">The default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="59deb-136">**Web uygulaması oturum zaman aşımı** değerini değiştirmenize gerek web uygulaması oturum zaman aşımı süresini değiştirmek için `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="59deb-136">**Web app session timeout** To change the web app session timeout, you need to modify the value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="59deb-137">Geçerli değerler `Absolute` ve `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="59deb-137">The applicable values are `Absolute` and `Rolling`.</span></span>
