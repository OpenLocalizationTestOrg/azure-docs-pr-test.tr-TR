---
title: "aaaCompare B2B işbirliği ve Azure Active Directory B2C | Microsoft Docs"
description: "Hello Azure Active Directory B2B işbirliği ve Azure AD B2C arasındaki fark nedir?"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>B2B işbirliği ve Azure Active Directory B2C ile karşılaştırın

Azure Active Directory (Azure AD) B2B işbirliği ve Azure AD B2C Azure AD'de dış kullanıcılarla toowork izin verin. Ancak nasıl karşılaştırmak?


B2B işbirliği özellikleri |     Azure AD B2C tek başına teklifi
-------- | --------
Yönelik: toobe mümkün tooauthenticate kullanıcılarının kimlik sağlayıcısı bağımsız olarak bir iş ortağı kuruluştan isteyen kuruluşların. | Yönelik: Mobil müşterileri ve web uygulamaları olup davet kişiler, Kurumsal veya Kurumsal müşteriler, Azure AD'ye.
Desteklenen kimlikleri: iş, okul hesapları, iş veya Okul hesapları iş ortaklarıyla veya herhangi bir e-posta adresi olan çalışanlar. En kısa sürede toosupport doğrudan Federasyon.  | Desteklenen kimlikleri: tüketici kullanıcılarla yerel uygulama hesapları (tüm e-posta adresi veya kullanıcı adı) veya herhangi bir desteklenen doğrudan Federasyon ile sosyal kimliği.
Directory hello iş ortağı kullanıcıları olan: hello dış kuruluştan kullanıcılar yönetilen ortak çalışanlar, Açıklamalı ancak aynı dizinde özel hello. Bunlar yönetilebilir hello aynı şekilde çalışanlar, olarak eklenen toohello aynı grupları olması vb.  | Dizin hello müşteri kullanıcı varlıkları olan: hello uygulama dizinindeki. Ayrı olarak yönetilen hello kuruluşunuzun çalışan ve iş ortağı dizininden (eğer varsa.
Çoklu oturum açma (SSO) tooall Azure AD bağlı uygulamalar desteklenir. Örneğin, erişim tooOffice 365 veya şirket içi uygulamalar ve tooother SaaS uygulamaları Salesforce veya Workday gibi sağlayabilir.  |  SSO toocustomer sahip olduğu uygulamalar hello Azure AD B2C kiracıları içinde desteklenir. SSO tooOffice 365 veya tooother Microsoft ve Microsoft olmayan SaaS uygulamaları desteklenmez.
İş ortağı yaşam döngüsü: kuruluş konak/davet hello tarafından yönetilir.  | Müşteri döngüsü: Self Servis veya Merhaba uygulaması tarafından yönetilir.
Güvenlik ilke ve uyumluluk: kuruluş konak/davet hello tarafından yönetilir.  | Güvenlik ilke ve uyumluluk: hello uygulama tarafından yönetilir.
Marka: Ana bilgisayar ve davet kuruluşunuzun markası kullanılır.  |    Marka: uygulama tarafından yönetiliyor. Genellikle hello kuruluş Soluklaşan hello arka plan içine markalı toobe ürün eğilimlidir.
Daha fazla bilgi: [Blog Gönderisi](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [belgeleri](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Daha fazla bilgi: [ürün sayfası](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [belgeleri](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B işbirliği kullanıcı özellikleri](active-directory-b2b-user-properties.md)
* [B2B işbirliği kullanıcı tooa rolü ekleme](active-directory-b2b-add-guest-to-role.md)
* [B2B işbirliği davetleri temsilci seçme](active-directory-b2b-delegate-invitations.md)
* [Dinamik gruplar ve B2B işbirliği](active-directory-b2b-dynamic-groups.md)
* [SaaS uygulamaları B2B işbirliği için yapılandırma](active-directory-b2b-configure-saas-apps.md)
* [B2B işbirliği kullanıcı belirteçleri](active-directory-b2b-user-token.md)
* [B2B işbirliği kullanıcı taleplerini eşleme](active-directory-b2b-claims-mapping.md)
* [Office 365 dış paylaşım](active-directory-b2b-o365-external-user.md)
* [B2B işbirliği geçerli sınırlamalar](active-directory-b2b-current-limitations.md)
* [B2B işbirliği için destek alma](active-directory-b2b-support.md)
