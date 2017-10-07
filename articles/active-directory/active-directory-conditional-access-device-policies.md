---
title: "Office 365 Hizmetleri için aaaAzure Active Directory koşullu erişim cihaz ilkeleri | Microsoft Docs"
description: "Nasıl tooprovision koşullu erişim cihaz ilkeleri toohelp hale şirket kaynaklarına daha güvenli kullanıcı uyumluluk ve erişim tooservices korurken hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Office 365 Hizmetleri için Active Directory koşullu erişim cihaz ilkeleri

Koşullu erişim, birden çok parça toowork gerektirir. Çok faktörlü içerir kimliği doğrulanmış kullanıcı, kimliği doğrulanmış cihaz ve diğer etkenlere bağlı arasında uyumlu bir cihaz. Bu makalede, biz öncelikle aygıt tabanlı koşullara kuruluşunuz erişim tooOffice 365 Hizmetleri kontrol toohelp kullanabileceğiniz odaklanın. 

Şirket kullanıcıları Exchange ve SharePoint Online gibi Office 365 tooaccess Hizmetleri iş veya Okul, kişisel cihazlarından istiyor. Merhaba erişim toobe güvenli istiyor. Koşullu erişim cihaz ilkeleri toohelp yapma şirket kaynaklarına erişim tooservices uyumlu aygıtlarını kullanan kullanıcılar için verilirken daha güvenli sağlayabilirsiniz. Koşullu erişim ilkeleri tooOffice 365 hello Microsoft Intune koşullu erişim Portalı'nda ayarlayabilirsiniz.

Azure Active Directory (Azure AD) koşullu erişim ilkeleri toohelp güvenli erişim tooOffice 365 Hizmetleri zorlar. Bir Office 365 hizmeti erişmesini uyumsuz bir cihazı kullanan bir kullanıcı engelleyen bir koşullu erişim ilkesi oluşturabilirsiniz. erişim toohello hizmeti verilmeden önce hello kullanıcı toohello şirketin cihaz ilkelerini uygun olmalıdır. Alternatif olarak, kendi aygıtlarını toogain erişim tooan Office 365 hizmet kullanıcıları tooenroll gerektiren bir ilke oluşturabilirsiniz. İlkeleri, bir kuruluşta uygulanan tooall kullanıcılar olabilir veya birkaç hedef grupları tooa sınırlı. Zaman içinde daha fazla hedef gruplar tooa İlkesi ekleyebilirsiniz.

Cihaz ilkelerini zorlama kullanıcılar cihazlarını hello Azure AD cihaz kaydı hizmeti ile kaydetmelisiniz önkoşuldur. Hello Azure AD cihaz kaydı hizmeti ile kaydetme cihazlar için çok faktörlü kimlik doğrulaması tooturn tercih edebilirsiniz. Çok faktörlü kimlik doğrulaması hello Azure Active Directory cihaz kayıt hizmeti için önerilir. Çok faktörlü kimlik doğrulaması etkinken, kullanıcılar cihazlarını hello Azure AD cihaz kaydı hizmeti ile kaydetmek için ikinci faktör kimlik doğrulaması sayaçlara.

## <a name="how-does-a-conditional-access-policy-work"></a>Bir koşullu erişim ilkesi nasıl çalışır?

Bir kullanıcı desteklenen cihaz platformundan erişim tooan Office 365 hizmeti istediğinde, Azure AD hello kullanıcı ve hello cihaz kimliğini doğrular. Yalnızca hello kullanıcı toohello ilke hello hizmeti için kümesi uyuyorsa azure AD verir erişim toohello hizmeti. Kayıtlı olmayan cihazlardaki kullanıcılar hakkında yönergeler verilmiştir tooenroll ve uyumlu tooaccess şirket Office 365 Hizmetleri haline gelir. İOS ve Android cihazlarda kullanıcılar gerekli tooenroll kendi hello Intune Şirket portalı uygulamasını kullanarak aygıtlardır. Bir kullanıcı bir cihaz kaydediliyorsa hello cihaz Azure AD ile kaydedilir ve aygıt yönetimi ve uyumluluk için kayıtlı. Office 365 Hizmetleri için mobil cihaz yönetimi için Microsoft Intune hello Azure AD cihaz kaydı hizmeti kullanmanız gerekir. Cihaz ilkelerini uygulanmadığında cihaz kaydı kullanıcılar tooaccess Office 365 Hizmetleri için gereklidir.

Ne zaman bir kullanıcı başarıyla kaydettiği bir aygıt, hello cihaz güvenilir hale gelir. Azure AD kimlik doğrulaması hello kullanıcı oturum açma tek erişimi toocompany uygulamaları sağlar. Azure AD yalnızca hello ilk hello kullanıcı erişim istediğinde, ancak her zaman hello kullanıcı erişim için bir istek yeniler bir koşullu erişim ilkesi toogrant erişim tooa hizmeti zorlar. Merhaba kullanıcı oturum açma kimlik bilgileri değiştirilirken, hello cihaz kaybolur veya çalınırsa veya hello hello İlkesi yenileme isteğinin hello zamanında koşulları olmayan erişim tooservices reddedildi.

## <a name="deployment-considerations"></a>Dağıtma konuları

Hello Azure AD cihaz kaydı hizmeti tooregister cihazları kullanmanız gerekir.

Şirket içi kullanıcıların kimlik doğrulaması, toobe hakkında Active Directory Federasyon Hizmetleri (AD FS) olduğunda (sürüm 1.0 ve sonraki sürümler) gereklidir. Merhaba kimlik sağlayıcısı çok faktörlü kimlik doğrulaması özelliğine sahip olmadığında çalışma alanına katılma için çok faktörlü kimlik doğrulaması başarısız olur. Örneğin, AD FS 2.0 ile çok faktörlü kimlik doğrulamasını kullanamazsınız. Bu hello multi-Factor authentication ile AD FS çalışır ve multi-Factor Authentication'hello Azure AD cihaz kaydı hizmetini etkinleştirmeden önce geçerli çok faktörlü kimlik doğrulama yöntemini yerinde olduğundan içi emin olun. Örneğin, Windows Server 2012 R2 AD FS çok faktörlü kimlik doğrulama özellikleri içerir. Multi-Factor Authentication'hello Azure AD cihaz kaydı hizmetini etkinleştirmeden önce hello AD FS sunucusunda ek geçerli kimlik doğrulama (çok faktörlü kimlik doğrulaması) yöntemi de ayarlamanız gerekir. AD FS'de desteklenen çok faktörlü kimlik doğrulama yöntemleri hakkında daha fazla bilgi için bkz: [AD FS için ek kimlik doğrulama yöntemleri yapılandırma](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

## <a name="next-steps"></a>Sonraki adımlar

*   Yanıtlar toocommon soruları için bkz [Azure Active Directory koşullu erişim ile ilgili SSS](active-directory-conditional-faqs.md).
