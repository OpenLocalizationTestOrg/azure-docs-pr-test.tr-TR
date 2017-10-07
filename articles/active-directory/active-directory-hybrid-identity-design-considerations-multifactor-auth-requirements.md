---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - çok faktörlü kimlik doğrulama gereksinimlerini belirleme"
description: "Koşullu erişim denetimi ile Azure Active Directory hello belirli koşullar hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin vermeden önce çekme denetler. Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>Karma kimlik çözümü çok faktörlü kimlik doğrulama gereksinimlerini belirleme
Veri ve uygulamaları hello bulutta ve herhangi bir CİHAZDAN erişen kullanıcılar ile yeteneği bu dünyasında bu bilgileri güvenlik altına almanın en önemli haline gelmiştir.  Her gün yeni bir başlık güvenlik ihlali hakkında yoktur.  Çok faktörlü kimlik doğrulaması, olmasına karşın, bu tür ihlallerine karşı garanti, ek bir katman sağlar güvenliğini toohelp önlemek bu ihlallerini.
Çok faktörlü kimlik doğrulaması için Hello kuruluşların gereksinimleri değerlendirerek başlatın. Diğer bir deyişle, hello kuruluş çalışırken toosecure nedir.  Bu değerlendirme önemli toodefine hello teknik gereksinimlerine ayarlama ve çok faktörlü kimlik doğrulaması için hello kuruluşların kullanıcıları etkinleştirme olur.

> [!NOTE]
> MFA ile ne yaptığını bilmiyorsanız, hello makalesini okuyun önerilir [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md) bu bölümü okumadan önce toocontinue.
> 
> 

Emin tooanswer hello aşağıdakileri yapın:

* Şirketiniz toosecure Microsoft uygulamaları çalışıyor? 
* Bu uygulamaları nasıl yayımlanacak?
* Şirketiniz uzaktan erişim tooallow çalışanlar tooaccess şirket içi uygulamalar sağlar?

Yanıt Evet ise, hangi uzaktan erişimi tür? Ayrıca bu uygulamalara erişen hello kullanıcılar nerede yer alacağı tooevaluate gerekir. Bu değerlendirme başka bir önemli adım toodefine hello uygun çok faktörlü kimlik doğrulama stratejisi ' dir. Aşağıdaki sorular emin tooanswer hello olun:

* Toobe giderek hello kullanıcıların bulunduğu?
* Bunlar herhangi bir yerde bulunan olabilir mi?
* Şirketiniz toohello kullanıcının konumuna göre tooestablish kısıtlamaları istiyor mu?

Bu gereksinimleri anladığınızda, tooalso değerlendirmek için çok faktörlü kimlik doğrulaması hello kullanıcının gereksinimleri önemlidir. Bu değerlendirme önemlidir, çünkü çok faktörlü kimlik doğrulaması çalışırken hello gereksinimleri tanımlayacaksınız. Aşağıdaki sorular emin tooanswer hello olun:

* Merhaba kullanıcıların çok faktörlü kimlik doğrulaması ile bilinen misiniz?
* Bazı kullanımlarını gerekli tooprovide ek kimlik doğrulama olacak?  
  * Yanıt Evet ise, tüm Merhaba, dış ağlara ya da erişimi belirli uygulamalar veya diğer koşullar altında çıkarken zaman?
* Merhaba kullanıcıların nasıl eğitim gerektirir toosetup ve uygulama çok faktörlü kimlik doğrulaması?
* Şirket kullanıcılarının tooenable çok faktörlü kimlik doğrulamasını istediği hello temel senaryolar nelerdir?

Merhaba önceki sorulara yanıt verilmesi sonra çok faktörlü kimlik doğrulaması zaten uygulanmış şirket içi varsa mümkün toounderstand olacaktır. Bu değerlendirme önemli toodefine hello teknik gereksinimlerine ayarlama ve çok faktörlü kimlik doğrulaması için hello kuruluşların kullanıcıları etkinleştirme olur. Aşağıdaki sorular emin tooanswer hello olun:

* Şirketinizin tooprotect ayrıcalıklı hesapları MFA ile gerekiyor mu?
* Şirketinizin tooenable MFA belirli uygulama uyumluluk nedenleriyle gerekiyor mu?
* Şirketiniz, bu uygulama ya da yalnızca Yöneticiler tüm uygun kullanıcılar için tooenable MFA gerekiyor mu?
* Her zaman etkin MFA veya yalnızca zaman hello kullanıcılar şirket ağının dışından oturum olmak zorunda?

## <a name="next-steps"></a>Sonraki adımlar
[Bir karma kimlik benimseme stratejinizi tanımlayın](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>Ayrıca bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

