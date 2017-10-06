---
title: "Azure Active Directory B2B işbirliği aaaLimitations | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği geçerli sınırlamalar"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Azure AD B2B işbirliği sınırlamaları
Azure Active Directory (Azure AD) B2B işbirliği şu anda bu makalede açıklanan konu toohello sınırlamalar olur.

## <a name="possible-double-multi-factor-authentication"></a>Olası çift çok faktörlü kimlik doğrulaması
Azure AD B2B ile Merhaba kaynak kuruluştaki (kuruluş davet hello) çok faktörlü kimlik doğrulamasını zorunlu kılabilir. Bu yaklaşım Hello nedenlerle ayrıntılı olarak [B2B işbirliği kullanıcılar için koşullu erişim](active-directory-b2b-mfa-instructions.md). Bir iş ortağı ayarlama ve zorlanan çok faktörlü kimlik doğrulaması zaten varsa, bunların kullanıcıları tooperform hello kimlik doğrulaması kez giriş kuruluşlarında olabilir ve ardından yeniden size ait.

## <a name="instant-on"></a>Anında açık
Merhaba B2B işbirliği akışlar, biz kullanıcıların toohello dizin ekleyin ve davet kullanım, uygulama atama ve benzeri sırasında dinamik olarak güncelleştir. Merhaba güncelleştirmeleri ve yazma işlemleri genellikle bir dizin örneğinde gerçekleşir ve tüm örneklerde çoğaltılması gerekir. Tüm örnekleri güncelleştirilir sonra çoğaltma tamamlandı. Bazen zaman hello nesne yazıldığı veya bir örneğinde güncelleştirildi ve hello çağırın tooretrieve bu nesne tooanother çoğaltma gecikmeleri oluşabilir örneğidir. Bu durumda, yenileme veya toohelp yeniden deneyin. Bizim API, ardından yeniden deneme bazı kullanarak bir uygulama yazıyorsanız, geri alma iyi, savunma yöntem tooalleviate bu sorunudur.

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B işbirliği kullanıcı özellikleri](active-directory-b2b-user-properties.md)
* [B2B işbirliği kullanıcı tooa rolü ekleme](active-directory-b2b-add-guest-to-role.md)
* [B2bB işbirliği davetleri temsilci seçme](active-directory-b2b-delegate-invitations.md)
* [Dinamik gruplar ve B2B işbirliği](active-directory-b2b-dynamic-groups.md)
* [B2B işbirliği kodu ve PowerShell örnekleri](active-directory-b2b-code-samples.md)
* [SaaS uygulamaları B2B işbirliği için yapılandırma](active-directory-b2b-configure-saas-apps.md)
* [B2B işbirliği kullanıcı belirteçleri](active-directory-b2b-user-token.md)
* [B2B işbirliği kullanıcı taleplerini eşleme](active-directory-b2b-claims-mapping.md)
* [Office 365 dış paylaşım](active-directory-b2b-o365-external-user.md)
