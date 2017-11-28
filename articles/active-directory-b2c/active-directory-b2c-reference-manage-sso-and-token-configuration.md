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
ms.openlocfilehash: b65271a22c77ea41eeec2126e4a3ad24364edd17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a><span data-ttu-id="cc88a-102">Azure Active Directory B2C: SSO ve belirteç özelleştirme özel ilkeler ile yönetme</span><span class="sxs-lookup"><span data-stu-id="cc88a-102">Azure Active Directory B2C: Manage SSO and token customization with custom policies</span></span>
<span data-ttu-id="cc88a-103">Özel ilkelerini kullanma gibi yerleşik ilkeleri aracılığıyla belirteci, oturum ve çoklu oturum açma (SSO) yapılandırmaları aynı denetime hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc88a-103">Using custom policies provides you hello same control over your token, session and single sign-on (SSO) configurations as through built-in policies.</span></span>  <span data-ttu-id="cc88a-104">Her ayarın yapar, toolearn hello belgelerine bakın [burada](#active-directory-b2c-token-session-sso).</span><span class="sxs-lookup"><span data-stu-id="cc88a-104">toolearn what each setting does, please see hello documentation [here](#active-directory-b2c-token-session-sso).</span></span>

## <a name="token-lifetimes-and-claims-configuration"></a><span data-ttu-id="cc88a-105">Belirteç yaşam süresi ve talep yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc88a-105">Token lifetimes and claims configuration</span></span>
<span data-ttu-id="cc88a-106">belirteç, yaşam süresi toochange hello ayarlarını, gereksinim duyduğunuz tooadd bir `<ClaimsProviders>` öğesi hello bağlı olan taraf hello İlkesi tooimpact istediğiniz dosyada.</span><span class="sxs-lookup"><span data-stu-id="cc88a-106">toochange hello settings on your token lifetimes, you need tooadd a `<ClaimsProviders>` element in hello relying party file of hello policy you want tooimpact.</span></span>  <span data-ttu-id="cc88a-107">Merhaba `<ClaimsProviders>` öğesidir hello alt `<TrustFrameworkPolicy>`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-107">hello `<ClaimsProviders>` element is a child of hello `<TrustFrameworkPolicy>`.</span></span>  <span data-ttu-id="cc88a-108">İçinde belirteç yaşam süreleri etkiler tooput hello bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc88a-108">Inside you'll need tooput hello information that affects your token lifetimes.</span></span>  <span data-ttu-id="cc88a-109">Merhaba XML şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="cc88a-109">hello XML looks like this:</span></span>

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

<span data-ttu-id="cc88a-110">**Erişim belirteci yaşam süreleri** hello belirteç ömrü hello içindeki hello değeri değiştirerek değiştirilebilir erişim `<Item>` hello anahtarı ile "token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="cc88a-110">**Access token lifetimes** hello access token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="cc88a-111">Merhaba varsayılan yerleşik 3600 saniye (60 dakika) değerdir.</span><span class="sxs-lookup"><span data-stu-id="cc88a-111">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="cc88a-112">**Kimliği belirteç ömrü** hello kimliği belirteç ömrü hello içindeki hello değeri değiştirerek değiştirilebilir `<Item>` hello anahtarı ile "id_token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="cc88a-112">**ID token lifetime** hello ID token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="id_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="cc88a-113">Merhaba varsayılan yerleşik 3600 saniye (60 dakika) değerdir.</span><span class="sxs-lookup"><span data-stu-id="cc88a-113">hello default value in built-in is 3600 seconds (60 minutes).</span></span>

<span data-ttu-id="cc88a-114">**Belirteç ömrü yenileme** hello yenileme belirteç ömrü hello içindeki hello değeri değiştirerek değiştirilebilir `<Item>` hello anahtarı ile "refresh_token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="cc88a-114">**Refresh token lifetime** hello refresh token lifetime can be changed by modifying hello value inside hello `<Item>` with hello Key="refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="cc88a-115">Yerleşik Hello varsayılan değer 1209600 (14 gün) saniyedir.</span><span class="sxs-lookup"><span data-stu-id="cc88a-115">hello default value in built-in is 1209600 seconds (14 days).</span></span>

<span data-ttu-id="cc88a-116">**Belirteç kayan pencere ömrü yenileme** tooset bir kayan pencere ömrü tooyour yenileme belirteci isterseniz içindeki hello değeri değiştirmek `<Item>` hello anahtarı ile "rolling_refresh_token_lifetime_secs" = saniye içinde.</span><span class="sxs-lookup"><span data-stu-id="cc88a-116">**Refresh token sliding window lifetime** If you would like tooset a sliding window lifetime tooyour refresh token, modify hello value inside `<Item>` with hello Key="rolling_refresh_token_lifetime_secs" in seconds.</span></span>  <span data-ttu-id="cc88a-117">Merhaba varsayılan yerleşik 7776000 (90 gün) değerdir.</span><span class="sxs-lookup"><span data-stu-id="cc88a-117">hello default value in built-in is 7776000 (90 days).</span></span>  <span data-ttu-id="cc88a-118">Tooenfore istemiyorsanız, bir kayan pencere ömrü bu satırla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="cc88a-118">If you don't want tooenfore a sliding window lifetime, replace this line with:</span></span>
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

<span data-ttu-id="cc88a-119">**Veren (ISS) talep** toochange hello veren (ISS) talep istiyorsanız, hello içindeki hello değeri değiştirin `<Item>` hello anahtarı ile = "IssuanceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="cc88a-119">**Issuer (iss) claim** If you want toochange hello Issuer (iss) claim, modify hello value inside hello `<Item>` with hello Key="IssuanceClaimPattern".</span></span>  <span data-ttu-id="cc88a-120">Merhaba geçerli değerler `AuthorityAndTenantGuid` ve `AuthorityWithTfp`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-120">hello applicable values are `AuthorityAndTenantGuid` and `AuthorityWithTfp`.</span></span>

<span data-ttu-id="cc88a-121">**Ayar talep İlkesi Kimliğini temsil eden** bu değeri ayarlamak için hello seçeneklerdir TFP (güven framework ilke) ve ACR (kimlik doğrulaması bağlamı başvuru).</span><span class="sxs-lookup"><span data-stu-id="cc88a-121">**Setting claim representing policy ID** hello options for setting this value are TFP (trust framework policy) and ACR (authentication context reference).</span></span>  
<span data-ttu-id="cc88a-122">Bu tooTFP toodo bu ayarlamanız önerilir, hello olun `<Item>` hello anahtarı ile = "AuthenticationContextReferenceClaimPattern" var ve hello değer `None`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-122">We recommend setting this tooTFP, toodo this, ensure hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern" exists and hello value is `None`.</span></span>
<span data-ttu-id="cc88a-123">İçinde `<OutputClaims>` öğesi, bu öğe ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cc88a-123">In your `<OutputClaims>` item, add this element:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
<span data-ttu-id="cc88a-124">Merhaba ACR için kaldırma `<Item>` hello anahtarı ile = "AuthenticationContextReferenceClaimPattern".</span><span class="sxs-lookup"><span data-stu-id="cc88a-124">For ACR, remove hello `<Item>` with hello Key="AuthenticationContextReferenceClaimPattern".</span></span>

<span data-ttu-id="cc88a-125">**Konu (alt) talep** bu seçenek tooswitch isterseniz tooObjectID, bu çok varsayılan`Not Supported`, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="cc88a-125">**Subject (sub) claim** This option is defaulted tooObjectID, if you would like tooswitch this too`Not Supported`, do hello following:</span></span>

<span data-ttu-id="cc88a-126">Bu satırı değiştirin</span><span class="sxs-lookup"><span data-stu-id="cc88a-126">Replace this line</span></span> 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
<span data-ttu-id="cc88a-127">Bu satırla:</span><span class="sxs-lookup"><span data-stu-id="cc88a-127">with this line:</span></span>
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a><span data-ttu-id="cc88a-128">Oturum davranışını ve SSO</span><span class="sxs-lookup"><span data-stu-id="cc88a-128">Session behavior and SSO</span></span>
<span data-ttu-id="cc88a-129">toochange oturum davranışını ve SSO yapılandırmaları tooadd gereken bir `<UserJourneyBehaviors>` öğesinin hello içindeki `<RelyingParty>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="cc88a-129">toochange your session behavior and SSO configurations, you need tooadd a `<UserJourneyBehaviors>` element inside of hello `<RelyingParty>` element.</span></span>  <span data-ttu-id="cc88a-130">Merhaba `<UserJourneyBehaviors>` öğesi hello hemen uymalıdır `<DefaultUserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-130">hello `<UserJourneyBehaviors>` element must immediately follow hello `<DefaultUserJourney>`.</span></span>  <span data-ttu-id="cc88a-131">içinde Merhaba, `<UserJourneyBehavors>` öğesi aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="cc88a-131">hello inside of your `<UserJourneyBehavors>` element should look like this:</span></span>

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
<span data-ttu-id="cc88a-132">**Çoklu oturum açma (SSO) yapılandırma** toochange hello tek oturum açma yapılandırması, gereksinim duyduğunuz toomodify hello değerini `<SingleSignOn>`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-132">**Single sign-on (SSO) configuration** toochange hello single sign-on configuration, you need toomodify hello value of `<SingleSignOn>`.</span></span>  <span data-ttu-id="cc88a-133">Merhaba geçerli değerler `Tenant`, `Application`, `Policy` ve `Disabled`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-133">hello applicable values are `Tenant`, `Application`, `Policy` and `Disabled`.</span></span> 

<span data-ttu-id="cc88a-134">**Web uygulaması oturum yaşam süresi (dakika)** toochange hello hello web uygulaması oturum yaşam hello toomodify değerini gereksinim `<SessionExpiryInSeconds>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="cc88a-134">**Web app session lifetime (minutes)** toochange hello hello web app session lifetime, you need toomodify value of hello `<SessionExpiryInSeconds>` element.</span></span>  <span data-ttu-id="cc88a-135">Merhaba varsayılan yerleşik ilkeleri 86400 saniyedir (1440 dakika) değerdir.</span><span class="sxs-lookup"><span data-stu-id="cc88a-135">hello default value in built-in policies is 86400 seconds (1440 minutes).</span></span>

<span data-ttu-id="cc88a-136">**Web uygulaması oturum zaman aşımı** toochange hello web uygulaması oturum zaman aşımı, gereksinim duyduğunuz toomodify hello değerini `<SessionExpiryType>`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-136">**Web app session timeout** toochange hello web app session timeout, you need toomodify hello value of `<SessionExpiryType>`.</span></span>  <span data-ttu-id="cc88a-137">Merhaba geçerli değerler `Absolute` ve `Rolling`.</span><span class="sxs-lookup"><span data-stu-id="cc88a-137">hello applicable values are `Absolute` and `Rolling`.</span></span>
