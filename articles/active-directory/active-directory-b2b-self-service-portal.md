---
title: "Azure Active Directory B2B işbirliği aaaSelf hizmet kayıt portalı | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği Kurumsal uygulamalarınıza iş ortakları tooselectively erişim sağlayarak, şirketler arası ilişkilerinizi destekler."
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Azure AD B2B işbirliği kayıt için Self Servis portalı

Müşteriler yapabilir çok bizim BT yöneticisi sunulan hello yerleşik özellikleri ile [Azure portal](https://portal.azure.com) ve bizim [uygulama erişim Paneli'ne](https://myapps.microsoft.com) son kullanıcılar için. Ancak biz de işletmeler toocustomize hello ekleme iş akışı B2B kullanıcılar toofit için kuruluşun gereksinimlerini gerektiğini fark. İle yapabileceklerini [API'mize](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

Müşterilerimizin ile tartışmalara bir ortak yukarıdaki tüm diğer hesapları yükselmeye bakın. Kuruluş davet hello hello zaman öncesinde tootheir kaynaklarına erişebilecek tek tek dış ortak olan bilemeyebilirsiniz. İş ortağı şirketlerden kullanıcılar çok kendilerini ilkeleri kümesiyle kuruluş denetimleri davet bu hello kaydolmak için bir yol istedikleri. Biz bunu vermedi Github projede yayımlanan şekilde bu senaryo bizim API'leri aracılığıyla mümkündür: [örnek Github proje](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Github Projemizin nasıl kuruluşlar bizim API'leri ve kullanabileceğiniz erişebilecekleri hello uygulamaları belirleyen kuralları ile güvenilir ortakları için bir ilke tabanlı, Self Servis kaydolma yeteneği sağlamak gösterir. İş ortağı kullanıcılar, erişimi tooresources alabilirsiniz, bunları güvenli bir şekilde, yerleşik kuruluş toomanually davet hello gerek kalmadan istedikleri zaman bunları. Tercih ettiğiniz bir Azure aboneliğinize hello proje kolayca dağıtabilirsiniz.

## <a name="as-is-code"></a>Olarak-kodu.

Bu kod hello Azure Active Directory B2B davet API örnek toodemonstrate kullanımını kullanılabilir hale getirileceğini unutmayın. Geliştirme ekibiniz veya bir iş ortağı tarafından özelleştirilmelidir ve bir üretim senaryosunda dağıtılmadan önce gözden geçirilmesi gerekir.

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:
* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-admin-add-users.md)
* [Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-iw-add-users.md)
* [Merhaba B2B işbirliği davet e-posta Hello öğeleri](active-directory-b2b-invitation-email.md)
* [B2B işbirliği davet kullanım](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B işbirliği lisanslama](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B işbirliği sorunlarını giderme](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)](active-directory-b2b-faq.md)
* [B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması](active-directory-b2b-mfa-instructions.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)