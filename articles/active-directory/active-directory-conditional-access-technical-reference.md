---
title: "Azure Active Directory koşullu erişim Teknik Başvurusu | Microsoft Docs"
description: "Koşullu erişim denetimi ile Azure Active Directory kullanıcı doğrulanırken ve uygulamaya erişimine izin vermeden önce çekme belirli koşullar denetler. Bu koşullar sağlandığında, kullanıcı kimlik doğrulaması ve uygulamaya erişim izni."
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Azure Active Directory koşullu erişim Teknik Başvurusu

## <a name="services-enabled-with-conditional-access"></a>Koşullu erişimle etkin hizmetleri

Koşullu erişim kuralları, çeşitli Azure AD uygulama türleri arasında desteklenir. Bu liste aşağıdakileri içerir:


* Azure uygulama ara sunucusu ile kaydedilmiş uygulamaları
* Azure RemoteApp
* İş ve Azure AD ile kayıtlı çok kiracılı uygulamalara geliştirilmiş kolu
* Dynamics CRM
* Azure AD uygulama galerisinde Federasyon uygulamalardan
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint (OneDrive iş içerir) çevrimiçi
* Microsoft Power BI 
* Azure AD uygulama galerisinde'ndan parola SSO uygulamalar
* Visual Studio Team Services
* Microsoft Teams









## <a name="enable-access-rules"></a>Erişim kurallarını etkinleştirin
Her kural etkinleştirilebilir veya devre dışı bir uygulama tabanları başına. Kuralları olduğunda **ON** bunlar etkinleştirilecek ve uygulamaya erişen kullanıcılar için uygulanmaz. Olduklarında **OFF** kullanılmayacak ve kullanıcıların oturum açma deneyimini etkilemez.

## <a name="applying-rules-to-specific-users"></a>Belirli kullanıcılara uygulama kuralları
Kurallar, belirli ayarlayarak güvenlik grubunu temel alan kullanıcı kümeleri için uygulanabilir **uygulamak için**. **Uygulanacak** ayarlanabilir **tüm kullanıcılar** veya **grupları**. Ayarlandığında **tüm kullanıcılar** kuralları uygulamaya erişimi olan herhangi bir kullanıcı için geçerli olacaktır. **Grupları** seçeneği, belirli güvenlik ve dağıtım grupları seçilmesine izin verir kuralları yalnızca zorunlu bu gruplara.

Bir kural dağıtırken, önce onu bir pilot gruplarının üyeleri olan kullanıcılar sınırlı kümesi uygulamak için yaygın bir sorundur. Tamamlandıktan sonra kural uygulanabilir **tüm kullanıcılar**. Bu kuralı kuruluştaki tüm kullanıcılar için zorlanacak neden olur.

Select ayrıca muaf tutulan gruplar İlkesi kullanarak **dışında** seçeneği. Dahil edilen grubunda göründükleri olsa bile bu grupların tüm üyelerinin muaf.

## <a name="at-work-networks"></a>"İşyerindeki" ağları
Bir "işyerindeki" ağı kullanmayı koşullu erişim kuralları, Azure AD içinde yapılandırılmış güvenilen IP adres aralıklarını Bel veya AD FS'den "içinde corpnet" talep kullanın. Söz konusu kurallar aşağıda belirtilmiştir:

* Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir
* İş olduğunda değil, erişimi engelle

Belirtmeyi seçeneklerini "işyerindeki" ağları

1. Güvenilen IP adres aralıklarını yapılandırma [çok faktörlü kimlik doğrulaması yapılandırma sayfası](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Koşullu erişim ilkesini yapılandırılmış aralıkları her kimlik doğrulama isteği ve belirteç verme kuralları değerlendirmek için kullanır. 
2. İç kullanımını yapılandır corpnet talep, bu seçenek, AD FS kullanarak Federasyon dizinleri ile kullanılabilir. İç hakkında daha fazla bilgi edinmek için corpnet talep bkz [Tusted IP'leri](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Uygulama duyarlılığına göre kuralları
Kuralları diğer hizmetlere erişimi etkilemeden korunması yüksek değerli hizmetleri izin vererek uygulama başına yapılandırılır. Koşullu erişim kuralları yapılandırılabilir **yapılandırma** uygulama sekmesinde. 

Şu anda sunulan kuralları:

* **Çok faktörlü kimlik doğrulaması gerektirir**
  
  * Bu ilkenin uygulandığı tüm kullanıcılar en az bir kez çok faktörlü kimlik doğrulaması kimlik doğrulaması için gerekli olacaktır.
* **Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir**
  
  * Bu ilke uygulandığında, tüm kullanıcılar İş dışı uzak bir konumdan hizmet erişirseniz en az bir kez çok faktörlü kimlik doğrulaması gerçekleştirmiş gerekli olacaktır. Bunlar bir işten uzak bir konuma taşırsanız, çok faktörlü kimlik doğrulama hizmeti erişirken gerçekleştirmek için gerekir.
* **İş olduğunda değil, erişimi engelle** 
  
  * Kullanıcılar uzak bir konuma işten taşıdığınızda, bunlar için "iş olduğunda değil, erişimi engelle" ilkesi uygulanırsa engellenir.  Bunlar erişimi olduğunda bir iş konumda yeniden izin verilir.

## <a name="related-topics"></a>İlgili konular
* [Azure Active Directory'ye bağlı Office 365 ve diğer uygulamalar için erişim güvenliğini sağlama](active-directory-conditional-access.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)

