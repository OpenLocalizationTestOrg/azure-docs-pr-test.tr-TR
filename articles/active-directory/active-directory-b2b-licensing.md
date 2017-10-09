---
title: "Kılavuzu lisans aaaAzure Active Directory B2B işbirliği | Microsoft Docs"
description: "Azure AD lisansları işbirliği gerektirmez Azure Active Directory B2B Ücretli ancak, aynı zamanda özellikleri B2B Konuk kullanıcılar için ücretli"
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
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: sasubram
ms.custom: it-pro
ms.openlocfilehash: 8e15d66209b090bff210674ecdacc88cd642dcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a>Azure Active Directory B2B işbirliği lisanslama kılavuzu

Azure AD B2B işbirliği özellikleri tooinvite Konuk kullanıcılar, Azure AD Kiracı tooallow bunları tooaccess Azure AD hizmetlerinde ve diğer kaynakları, kuruluşunuzda kullanabilirsiniz. B2B işbirliği Konuk kullanıcılar ile lisansına sahip olması gerekir tooprovide erişim toopaid Azure AD özellikler istiyorsanız, Azure AD lisansları uygun. 

Bu avantajlar şunlardır:
* Azure AD boş yetenekleri ek lisans olmadan Konuk kullanıcılar için kullanılabilir.
* Tooprovide erişim toopaid Azure AD özellikleri tooB2B kullanıcıları istiyorsanız bu B2B Konuk kullanıcılar yeterli lisans toosupport olması gerekir.
* Davet bir kiracı ile lisans Ücretli bir Azure AD B2B işbirliği kullanım hakları tooan ek beş B2B Konuk davet kullanıcılar toohello Kiracı vardır.
* Kiracı davet hello sahibi hello müşterinin Azure AD özellikleri Ücretli kaç B2B işbirliği kullanıcıların gereksinim hello bir toodetermine olması gerekir. Azure AD Ücretli hello bağlı olarak yeterince Azure AD olmalıdır, Konuk kullanıcılar için istediğiniz özelliklerini lisansları toocover B2B işbirliği kullanıcılar hello Ücretli aynı 5:1 oranında.

B2B işbirliği Konuk kullanıcı, iş ortağı şirkete veya değil, bir çalışan, kuruluşunuzun farklı bir iş, conglomerate içinde çalışan bir kullanıcı olarak eklenir. B2B Konuk kullanıcı dış kimlik bilgileri veya kuruluşunuz tarafından bu makalede açıklanan ait kimlik bilgilerinizle oturum açabilirsiniz. 

Diğer bir deyişle, B2B lisans hello kullanıcı kimliğini nasıl doğruladığını tarafından değil ancak yerine hello ilişki hello kullanıcı tooyour kuruluşun tarafından ayarlanır. Bu kullanıcılar iş ortakları emin değilseniz, farklı olarak, Lisans Koşulları'kabul edilir. Bunlar toobe B2B işbirliği kullanıcı kendi UserType "Konuk" olarak işaretlenmiş olsa bile amacıyla lisans için olarak kabul edilmez Bunlar normalde, bir lisansı kullanıcı başına lisansına sahip olması. Bu kullanıcılar şunları içerir:
* Çalışanlarınızın
* Dış kimlikler kullanarak oturum açmayı personel
* Bir çalışan, conglomerate içinde farklı bir iş


## <a name="licensing-examples"></a>Lisans örnekleri
- Bir müşteri tooinvite 100 B2B işbirliği kullanıcılar tooits Azure AD kiracısı istemektedir. erişim yönetimi ve tüm kullanıcılar için sağlama Hello müşteri atar ancak 50 kullanıcılar için de MFA ve koşullu erişim gerekir. Bu müşteri 10 Azure AD temel lisansları ve 10 Azure AD Premium P1 lisansları toocover bu B2B kullanıcılar doğru satın almanız gerekir. Merhaba müşteri B2B kullanıcılarla toouse kimlik koruması özellikleri planlıyorsa, Azure AD Premium P2 lisansları toocover davet hello kullanıcılar hello sahip olmaları aynı 5:1 oranında.
- Bir müşteri, Azure AD Premium P1 olan tüm lisanslı 10 çalışanlar sahiptir. Şimdi tüm çok faktörlü kimlik doğrulaması (MFA) gerektiren tooinvite 60 B2B kullanıcılar isterler. Hello 5:1 lisans kural altında hello müşteri tüm 60 B2B işbirliği kullanıcılar en az 12 Azure AD Premium P1 lisansları toocover olması gerekir. Zaten 10 Premium P1 lisansı 10 çalışanlar için sahip oldukları için MFA gibi Premium P1 özellikleri hakları tooinvite 50 B2B kullanıcı sahiptirler. Bu örnekte, daha sonra bunlar 2 ek Premium P1 lisanslar toocover hello kalan 10 B2B işbirliği kullanıcılar satın almanız gerekir.

> [!NOTE]
> Tooassign bu B2B işbirliği kullanıcı hakları doğrudan toohello B2B kullanıcılar tooenable lisansları henüz bir yolu yoktur.

Kiracı davet hello sahibi hello müşterinin Azure AD özellikleri Ücretli kaç B2B işbirliği kullanıcıların gereksinim hello bir toodetermine olması gerekir. Hangi Konuk kullanıcılar için istediğiniz Azure AD özelliklerini Ücretli bağlı olarak, lisansları toocover B2B işbirliği kullanıcılar hello 5:1 oranında Ücretli yeterince Azure AD olmalıdır. 

## <a name="additional-licensing-details"></a>Ek lisans ayrıntıları
- Tooactually Ata lisansları tooB2B kullanıcı hesaplarının gerek yoktur. Merhaba 5:1 oranında üzerinde bağlı olarak, lisans otomatik olarak hesaplanan bildirilen ve.
- Ücretli Hayır ise Azure AD lisans hello Kiracı, Azure AD serbest hello her davet edilen kullanıcı alır hello hakları var. edition sunar.
- Kendi kuruluştan işbirliği kullanıcı zaten Ücretli bir Azure AD B2B lisans varsa, bunlar hello B2B işbirliği lisanstan hello davet Kiracı kullanamayacaktır.

## <a name="advanced-discussion-what-are-hello-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a>Tartışma Gelişmiş: biz "üye Apı'lerinizi kullanarak" olarak kümeleme kuruluştan kullanıcılar eklediğinizde hello lisans değerlendirmeleri nelerdir?
B2B Konuk kullanıcı bir iş ortağı kuruluş toowork hello konak kuruluşla gelen davet biridir. Genellikle, herhangi bir durumu B2B bile, kullandığı B2B özellikleri uygun değil. Özellikle iki durumda bakalım:

1. Bir tüketici adresini kullanarak bir çalışan bir ana bilgisayar davet ederse
  * Bu senaryo bizim lisans ilkeleri ile uyumlu değildir ve önerilmez.

2. Bir ana bilgisayar kuruluş, başka bir kümeleme kuruluştan bir kullanıcı eklerse
  1. Bu durumda, B2B API'lerini kullanarak hello kullanıcı davet, ancak bu durumda geleneksel B2B değil. İdeal olarak, biz bu kuruluşların olmalıdır (bizim API sağlar,) üye olarak davet hello diğer düzenlemeler kullanıcılar. Bu durumda, toobe toothese üyeleri bunları kuruluş davet hello tooaccess kaynaklar için atanan lisanslara sahip.

  2. Bazı kuruluşlar tooadd hello ilke olarak "Konuk" olarak eklenen diğer kuruluş ait kullanıcılar toobe isteyebilirsiniz. Burada iki durum vardır:
      * Merhaba kümeleme kuruluş Azure AD kullanmakta olduğunu ve davet hello kullanıcıların hello lisansına sahip diğer kuruluşun: 1:5 formülü bu belgenin önceki bölümlerinde düzenlendiği davet edilen kullanıcılar tooneed toofollow hello bu durumda, bekliyoruz yok. 

      * Merhaba kümeleme kuruluş Azure AD kullanmayan veya yeterli lisans yok: Bu durumda, 1:5 formülü bu belgenin önceki bölümlerinde düzenlendiği hello izleyin.

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-admin-add-users.md)
* [Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-iw-add-users.md)
* [Merhaba B2B işbirliği davet e-posta Hello öğeleri](active-directory-b2b-invitation-email.md)
* [B2B işbirliği davet kullanım](active-directory-b2b-redemption-experience.md)
* [Azure Active Directory B2B işbirliği sorunlarını giderme](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B işbirliği API ve özelleştirme](active-directory-b2b-api.md)
* [B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması](active-directory-b2b-mfa-instructions.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
