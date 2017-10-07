---
title: "Azure Active Directory B2B işbirliği aaaWhat mi? | Microsoft Belgeleri"
description: "Azure Active Directory B2B işbirliği, şirket uygulamalarınızı iş ortakları tooselectively erişim sağlayarak, şirketler arası ilişkilerinizi destekler."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: 359989b66f3d012c306e8748a607662fffacb919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a>Azure AD B2B işbirliği nedir?

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

Azure AD iş işletmeden işletmeye (B2B) işbirliği özelliklerinden herhangi diğer kuruluştan, küçük veya büyük kullanıcılarla güvenle ve güvenli bir şekilde Azure AD toowork kullanan herhangi bir kuruluş etkinleştirin. Bu kuruluşlardan Azure AD ile veya olmadan, hatta bir BT kuruluşu ile veya olmadan olabilir. 

Azure AD kullanarak kuruluşlar kendi şirket verileri üzerinde tam denetimi korurken toodocuments, kaynaklar ve uygulamalar tootheir ortakları, erişim sağlayabilir. Geliştiriciler, iki kuruluş birlikte daha güvenli bir şekilde Getir hello Azure AD iş iş API'leri toowrite uygulamaları kullanabilir. Ayrıca, son kullanıcıların toonavigate için oldukça kolaydır.

Azure AD B2B işbirliği çok önemli toothem olduğundan, müşterilerimizin %97 olmamızı istiyordu.

![Pasta grafik](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

Erken Nisan 2017 itibariyle zaten Azure AD B2B işbirliği özelliklerini kullanarak yaklaşık 3 milyon kullanıcı vardı. Ve birden fazla %23 10'dan fazla kullanıcınız Azure AD kuruluşların zaten bu özelliklerini benefiting.

## <a name="hello-key-benefits-of-azure-ad-b2b-collaboration-tooyour-organization"></a>Azure AD B2B işbirliği tooyour kuruluş Hello kilit yararları

### <a name="work-with-any-user-from-any-partner"></a>Herhangi bir ortaktan herhangi bir kullanıcı ile çalışma

* İş ortakları kendi kimlik bilgilerini kullan

* İş ortakları toouse Azure AD için bir gereksinimi

* Hiçbir dış dizinleri veya karmaşık Kurulum gerekli

### <a name="simple-and-secure-collaboration"></a>Basit ve güvenli işbirliği

* Gelişmiş, Azure AD destekli Yetkilendirme İlkeleri uygulanırken Access tooany şirket uygulaması veya verileri sağlar

* Kullanıcılar için kolay

* Uygulamalar ve veriler için kurumsal düzeyde güvenlik

### <a name="no-management-overhead"></a>Yönetim yükü

* Dış bir hesap veya parola yönetimi

* Hiçbir eşitleme veya el ile hesap yaşam döngüsü yönetimi

* Hiçbir dış yönetim yükü

## <a name="you-can-easily-add-b2b-collaboration-users-tooyour-organization"></a>B2B işbirliği kullanıcılar tooyour kuruluş kolayca ekleyebilirsiniz.

Yöneticileri hello B2B işbirliği (konuk) kullanıcılar ekleyebilirsiniz [Azure portal](https://portal.azure.com).

![Konuk kullanıcı ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-toobring-their-own-identity"></a>Ortak Çalışanlar toobring kendi kimliğini etkinleştir

B2B Ortak Çalışanlar kendi seçtikleri kimlik bilgilerinizle oturum açabilirsiniz. Merhaba kullanıcının bir Microsoft hesabı veya bir Azure AD hesabı – yoksa, bunlar için sorunsuz bir şekilde hello anda teklif kullanım için oluşturulur.

![oturum açma kimlik seçimi](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-tooapplication-and-group-owners"></a>Temsilci tooapplication ve grubu sahipleri 
Uygulama ve Grup sahipleri B2B kullanıcılar ekleyebilir, bir Microsoft uygulaması olsun veya olmasın, ilgilendiğiniz doğrudan tooany uygulama. Yöneticileri izin tooadd B2B kullanıcılar toonon-yöneticileri atayabilirsiniz. Olmayan yöneticilere hello kullanabileceğiniz [Azure AD uygulama erişim Paneli'ne](https://myapps.microsoft.com) tooadd B2B işbirliği kullanıcılar tooapplications veya gruplar.

![erişim paneli](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![üye ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a>Yetkilendirme İlkeleri, şirket içeriğini koruyun

Koşullu erişim ilkeleri, çok faktörlü kimlik doğrulaması gibi uygulanabilir:
- Merhaba Kiracı düzeyinde
- Merhaba uygulama düzeyinde
- Belirli kullanıcıları tooprotect şirket uygulamaları ve verileri için

![üye ekleme](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-tooeasily-build-applications-tooonboard"></a>Bizim API'leri kullanan ve örnek kod tooeasily uygulamaları tooonboard derleme
Dış ortaklarınız karttaki yolları özelleştirilmiş tooyour kuruluşunuzun gereksinimlerini duruma getirin.

Hello kullanarak [B2B İşbirliği davetini API'leri](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), Self Servis kaydolma portalları oluşturma dahil olmak üzere onboarding deneyimlerinizi özelleştirebilirsiniz. Bir Self Servis portalı için örnek kod sağladığımız [github'da](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

![Kayıt portalı](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

Azure AD B2B işbirliği ile Azure AD tooprotect hello gücünü son kullanıcıların kolay ve sezgisel bulabileceğiniz bir şekilde, iş ortağı ilişkileri alabilirsiniz. Bu nedenle, Azure AD B2B kendi dış işbirliği için zaten kullanıyorsanız kuruluşların birleştirme hello binlerce devam!

## <a name="next-steps"></a>Sonraki adımlar

* Yönetici deneyimleri hello bulunduğunda [Azure portal](https://portal.azure.com).

* Bilgi çalışanı deneyimleri hello kullanılabilir [erişim paneli](https://myapps.microsoft.com).

* Ve her zaman olduğu gibi tüm geri bildirim, tartışmalara ve üzerinden öneriler için hello ürün ekibi bağlamak bizim [Microsoft teknik topluluk](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-admin-add-users.md)
* [Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-iw-add-users.md)
* [Merhaba B2B işbirliği davet e-posta Hello öğeleri](active-directory-b2b-invitation-email.md)
* [B2B işbirliği davet kullanım](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B işbirliği lisanslama](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B işbirliği sorunlarını giderme](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B işbirliği API ve özelleştirme](active-directory-b2b-api.md)
* [B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması](active-directory-b2b-mfa-instructions.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [B2B işbirliği kullanıcı Denetim ve Raporlama](active-directory-b2b-auditing-and-reporting.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
