---
title: "aaaAzure Active Directory koşullu erişim Teknik Başvurusu | Microsoft Docs"
description: "Koşullu erişim denetimi ile Azure Active Directory hello belirli koşullar hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin vermeden önce çekme denetler. Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Azure Active Directory koşullu erişim Teknik Başvurusu

## <a name="services-enabled-with-conditional-access"></a>Koşullu erişimle etkin hizmetleri

Koşullu erişim kuralları, çeşitli Azure AD uygulama türleri arasında desteklenir. Bu liste aşağıdakileri içerir:


* Azure uygulama proxy'si Hello ile kaydedilmiş uygulamaları
* Azure RemoteApp
* İş ve Azure AD ile kayıtlı çok kiracılı uygulamalara geliştirilmiş kolu
* Dynamics CRM
* Hello Azure AD uygulama galerisinde Federasyon uygulamalardan
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint (OneDrive iş içerir) çevrimiçi
* Microsoft Power BI 
* Parola SSO uygulamalardan hello Azure AD uygulama Galerisi
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Erişim kurallarını etkinleştirin
Her kural etkinleştirilebilir veya devre dışı bir uygulama tabanları başına. Kuralları olduğunda **ON** bunlar etkinleştirilecek ve hello uygulamaya erişen kullanıcılar için uygulanmaz. Olduklarında **OFF** değil kullanılır ve etkisi hello kullanıcı deneyimi imzalar.

## <a name="applying-rules-toospecific-users"></a>Kuralları toospecific kullanıcıların uygulama
Kuralları ayarlayarak güvenlik grubunu temel alan kullanıcı uygulanan toospecific kümeleri olabilir **uygulamak için**. **Uygulanacak** çok ayarlanabilir**tüm kullanıcılar** veya **grupları**. Ayarlandığında çok**tüm kullanıcılar** hello kuralları tooany kullanıcı erişimi toohello uygulamayla geçerlidir. Merhaba **grupları** seçeneği sağlayan belirli güvenlik ve dağıtım grupları toobe seçili, kuralları yalnızca zorunlu bu gruplara.

Bir kural dağıtırken yaygındır toofirst, pilot gruplarının üyeleri olan kullanıcılar, sınırlı sayıda uygulayın. Tam hello kural çok uygulanabilir sonra**tüm kullanıcılar**. Bu toobe hello kuruluşunuzdaki tüm kullanıcılar için zorlanan hello kural neden olur.

Select ayrıca muaf tutulan gruplar hello kullanarak ilkesinden **dışında** seçeneği. Dahil edilen grubunda göründükleri olsa bile bu grupların tüm üyelerinin muaf.

## <a name="at-work-networks"></a>"İşyerindeki" ağları
Bir "işyerindeki" ağı kullanmayı koşullu erişim kuralları, Azure AD içinde yapılandırılmış güvenilen IP adres aralıklarını Bel veya hello "içinde corpnet" AD FS talep kullanımını. Söz konusu kurallar aşağıda belirtilmiştir:

* Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir
* İş olduğunda değil, erişimi engelle

Belirtmeyi seçeneklerini "işyerindeki" ağları

1. Hello güvenilen IP adres aralıklarını yapılandırma [çok faktörlü kimlik doğrulaması yapılandırma sayfası](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Koşullu erişim ilkesini her kimlik doğrulama isteği ve belirteç verme tooevaluate kurallarında yapılandırılmış hello aralıklarını kullanır. 
2. Corpnet talep içinde hello kullanımını yapılandırmak, bu seçenek, AD FS kullanarak Federasyon dizinleri ile kullanılabilir. corpnet talepleri içinde hello hakkında daha fazla toolearn bkz [Tusted IP'leri](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Uygulama duyarlılığına göre kuralları
Kuralları, erişim tooother Hizmetleri etkilemeden güvenli hello yüksek değerli hizmetleri toobe izin vererek uygulama başına yapılandırılır. Koşullu erişim kuralları hello üzerinde yapılandırılabilir **yapılandırma** hello uygulama sekmesinde. 

Şu anda sunulan kuralları:

* **Çok faktörlü kimlik doğrulaması gerektirir**
  
  * Bu ilke uygulanan toowill olan tüm kullanıcıların en az bir kez çok faktörlü kimlik doğrulaması aracılığıyla gerekli tooauthenticate olabilir.
* **Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir**
  
  * Bu ilkenin geçerli olduğu iş dışı uzak bir konumdan hello hizmet eriştiklerinde ise tüm kullanıcıların bu gerçekleştirilen gerekli toohave çok faktörlü kimlik doğrulaması en az bir kez olacaktır. Bir iş tooremote konumundan taşırsanız, bunlar gerekli tooperform çok faktörlü kimlik doğrulama hello hizmet erişirken olacaktır.
* **İş olduğunda değil, erişimi engelle** 
  
  * Kullanıcılar iş tooa uzak bir konumdan taşıdığınızda, bunlar hello "iş olduğunda değil, erişimi engelle" ilke uygulanan toothem ise engellenir.  Bunlar erişimi olduğunda bir iş konumda yeniden izin verilir.

## <a name="related-topics"></a>İlgili konular
* [Active Directory tooAzure bağlı erişim tooOffice 365 ve diğer uygulamaların güvenliğini sağlama](active-directory-conditional-access.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

