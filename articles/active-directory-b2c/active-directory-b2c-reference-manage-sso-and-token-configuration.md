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
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C: SSO ve belirteç özelleştirme özel ilkeler ile yönetme
Özel ilkelerini kullanma gibi yerleşik ilkeleri aracılığıyla belirteci, oturum ve çoklu oturum açma (SSO) yapılandırmaları aynı denetime hello sağlar.  Her ayarın yapar, toolearn hello belgelerine bakın [burada](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Belirteç yaşam süresi ve talep yapılandırma
belirteç, yaşam süresi toochange hello ayarlarını, gereksinim duyduğunuz tooadd bir `<ClaimsProviders>` öğesi hello bağlı olan taraf hello İlkesi tooimpact istediğiniz dosyada.  Merhaba `<ClaimsProviders>` öğesidir hello alt `<TrustFrameworkPolicy>`.  İçinde belirteç yaşam süreleri etkiler tooput hello bilgi gerekir.  Merhaba XML şöyle görünür:

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

**Erişim belirteci yaşam süreleri** hello belirteç ömrü hello içindeki hello değeri değiştirerek değiştirilebilir erişim `<Item>` hello anahtarı ile "token_lifetime_secs" = saniye içinde.  Merhaba varsayılan yerleşik 3600 saniye (60 dakika) değerdir.

**Kimliği belirteç ömrü** hello kimliği belirteç ömrü hello içindeki hello değeri değiştirerek değiştirilebilir `<Item>` hello anahtarı ile "id_token_lifetime_secs" = saniye içinde.  Merhaba varsayılan yerleşik 3600 saniye (60 dakika) değerdir.

**Belirteç ömrü yenileme** hello yenileme belirteç ömrü hello içindeki hello değeri değiştirerek değiştirilebilir `<Item>` hello anahtarı ile "refresh_token_lifetime_secs" = saniye içinde.  Yerleşik Hello varsayılan değer 1209600 (14 gün) saniyedir.

**Belirteç kayan pencere ömrü yenileme** tooset bir kayan pencere ömrü tooyour yenileme belirteci isterseniz içindeki hello değeri değiştirmek `<Item>` hello anahtarı ile "rolling_refresh_token_lifetime_secs" = saniye içinde.  Merhaba varsayılan yerleşik 7776000 (90 gün) değerdir.  Tooenfore istemiyorsanız, bir kayan pencere ömrü bu satırla değiştirin:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Veren (ISS) talep** toochange hello veren (ISS) talep istiyorsanız, hello içindeki hello değeri değiştirin `<Item>` hello anahtarı ile = "IssuanceClaimPattern".  Merhaba geçerli değerler `AuthorityAndTenantGuid` ve `AuthorityWithTfp`.

**Ayar talep İlkesi Kimliğini temsil eden** bu değeri ayarlamak için hello seçeneklerdir TFP (güven framework ilke) ve ACR (kimlik doğrulaması bağlamı başvuru).  
Bu tooTFP toodo bu ayarlamanız önerilir, hello olun `<Item>` hello anahtarı ile = "AuthenticationContextReferenceClaimPattern" var ve hello değer `None`.
İçinde `<OutputClaims>` öğesi, bu öğe ekleyin:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Merhaba ACR için kaldırma `<Item>` hello anahtarı ile = "AuthenticationContextReferenceClaimPattern".

**Konu (alt) talep** bu seçenek tooswitch isterseniz tooObjectID, bu çok varsayılan`Not Supported`, aşağıdaki hello:

Bu satırı değiştirin 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
Bu satırla:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Oturum davranışını ve SSO
toochange oturum davranışını ve SSO yapılandırmaları tooadd gereken bir `<UserJourneyBehaviors>` öğesinin hello içindeki `<RelyingParty>` öğesi.  Merhaba `<UserJourneyBehaviors>` öğesi hello hemen uymalıdır `<DefaultUserJourney>`.  içinde Merhaba, `<UserJourneyBehavors>` öğesi aşağıdaki gibi görünmelidir:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Çoklu oturum açma (SSO) yapılandırma** toochange hello tek oturum açma yapılandırması, gereksinim duyduğunuz toomodify hello değerini `<SingleSignOn>`.  Merhaba geçerli değerler `Tenant`, `Application`, `Policy` ve `Disabled`. 

**Web uygulaması oturum yaşam süresi (dakika)** toochange hello hello web uygulaması oturum yaşam hello toomodify değerini gereksinim `<SessionExpiryInSeconds>` öğesi.  Merhaba varsayılan yerleşik ilkeleri 86400 saniyedir (1440 dakika) değerdir.

**Web uygulaması oturum zaman aşımı** toochange hello web uygulaması oturum zaman aşımı, gereksinim duyduğunuz toomodify hello değerini `<SessionExpiryType>`.  Merhaba geçerli değerler `Absolute` ve `Rolling`.
