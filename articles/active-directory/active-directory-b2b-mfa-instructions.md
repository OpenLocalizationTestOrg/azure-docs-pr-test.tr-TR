---
title: "Azure Active Directory B2B işbirliği kullanıcılar aaaConditional erişimi | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği seçmeli erişim tooyour kurumsal uygulamalar için çok faktörlü kimlik doğrulaması (MFA) destekler"
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
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>B2B işbirliği kullanıcılar için koşullu erişim

## <a name="multi-factor-authentication-for-b2b-users"></a>B2B kullanıcılar için çok faktörlü kimlik doğrulaması
Azure AD B2B işbirliği ile kuruluşlar B2B kullanıcılar için çok faktörlü kimlik doğrulaması (MFA) ilkeleri uygulayabilirsiniz. Bu ilkeler hello Kiracı, uygulama veya bireysel kullanıcı düzeyinde hello zorunlu tutulabilir aynı şekilde tam zamanlı çalışanlar ve hello kuruluş üyeleri için etkinleştirilir. MFA ilkeleri hello kaynak kuruluştan uygulanır.

Örnek:
1. Yönetici veya bilgi çalışanı şirketindeki başvurulmasını Şirket B tooan uygulama kullanıcıdan *Foo* A. şirketteki
2. Uygulama *Foo* şirkette yapılandırılmış toorequire MFA erişimine açık.
3. Şirket B hello kullanıcıdan tooaccess uygulama çalıştığında *Foo* oldukları hello şirket Kiracı'da, MFA testini toocomplete istedi.
4. Merhaba kullanıcı kendi MFA Şirket A ile ayarlayabilirsiniz ve bunların MFA seçeneğini seçer.
5. Bu senaryo için herhangi bir kimlik çalışır (Azure AD veya örneğin, kullanıcıların şirket b sosyal kimliği kullanarak kimlik doğrulaması MSA)
6. Şirket A MFA desteği yeterli Azure AD Premium lisansı olması gerekir. Bu lisans A. şirketten Hello kullanıcı B şirketten kullanır

Merhaba ortağı kuruluşu MFA yetenekleri olsa bile hello davet kiralama her zaman MFA için kullanıcıların hello iş ortağı kuruluştan sorumludur.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>B2B işbirliği kullanıcılar için MFA'yı ayarlama
B2B işbirliği kullanıcılar için MFA yukarı tooset olduğu ne kadar kolay toodiscover bkz nasıl içinde hello video:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>Kullanım B2B kullanıcılar için MFA deneyimi sunar
Animasyon toosee hello kullanım deneyimi aşağıdaki hello denetleyin:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>MFA B2B işbirliği kullanıcılar için Sıfırla
Şu anda hello Yöneticisi B2B işbirliği kullanıcılar tooproof yukarı yeniden gerektirebilir PowerShell cmdlet'lerini aşağıdaki hello kullanarak yalnızca:

1. TooAzure AD connect

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Tüm kullanıcılara sağlama yöntemleri ile Al

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Örnek aşağıda verilmiştir:

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Merhaba MFA yöntemi bir özel kullanıcı toorequire hello B2B işbirliği kullanıcı tooset güçlü yöntemleri için yeniden Sıfırla. Örnek:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Neden biz hello kaynak kiralama MFA gerçekleştiriyorsunuz?

Merhaba geçerli sürümde, MFA öngörülebilirlik nedenlerle hello kaynak kiralama her zaman kullanılıyor. Örneğin, Contoso kullanıcı (değiştirmemesi) davet edilen tooFabrikam ve Fabrikam B2B kullanıcılar için MFA etkinleştirilmiş varsayalım.

Contoso etkin App1 ancak değil App2 için MFA ilkesi varsa, biz hello Contoso MFA talep hello belirtecindeki bakarsanız sonra biz sorunu aşağıdaki hello görebilirsiniz:

* 1. güne: Bir kullanıcının Contoso ağında MFA varsa ve App1 sonra hiçbir ek MFA erişme istemi Fabrikam ' gösterilir.

* Günde 2: hello kullanıcı, Fabrikam erişirken artık Contoso, uygulama 2 eriştiğini, var. MFA için kaydolması gerekir.

Bu işlem kafa karıştırıcı olabilir ve oturum açma tamamlamalar içinde toodrop neden olabilir.

Contoso MFA yeteneği olsa bile, ayrıca, her zaman hello servis talebi hello Fabrikam hello Contoso MFA İlkesi güven değildir.

Son olarak, kaynak Kiracı MFA ayarladığınız MFA olmayan iş ortağı kuruluşu ve Msa'lar ve sosyal kimlikleri için çalışır.

Bu nedenle, hello mfa B2B kullanıcılar için tooalways Kiracı davet hello MFA gerektirecek önerilir. Bu gereksinim toodouble MFA bazı durumlarda neden olabilir, ancak hello davet Kiracı erişen her hello son kullanıcıların deneyimini tahmin edilebilir: değiştirmemesi MFA için hello davet Kiracı ile kaydetmeniz gerekir.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>B2B kullanıcılar için cihaz, konum ve risk tabanlı koşullu erişim

Contoso şirket verilerini için cihaz temelli koşullu erişim ilkeleri etkinleştirdiğinde, Contoso ve hello Contoso cihaz ilkeleriyle uyumlu olmayan yönetilmeyen cihazlar üzerinden erişimi engelledi.

Hello B2B kullanıcının cihaz Contoso tarafından yönetilmiyor, bu ilkeleri zorunlu ne olursa olsun bağlamda hello iş ortağı kuruluşlardan B2B kullanıcıların erişim engellendi. Ancak, Contoso belirli iş ortağı kullanıcıların tooexclude içeren liste onlardan cihaz temelli koşullu erişim ilkesi hello dışlama oluşturabilirsiniz.

#### <a name="location-based-conditional-access-for-b2b"></a>Konum temelli B2B için koşullu erişim

Merhaba davet kuruluş mümkün toocreate kendi ortak kuruluşlar tanımlayan güvenilir bir IP adresi aralığı ise B2B kullanıcılar için konum temelli koşullu erişim ilkeleri uygulanabilir.

#### <a name="risk-based-conditional-access-for-b2b"></a>Risk tabanlı B2B için koşullu erişim

Şu anda Hello risk değerlendirme hello B2B kullanıcının ev kuruluştan yapıldığından risk tabanlı oturum açma ilkeleri uygulanan tooB2B kullanıcılar olamaz.

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
* [Azure Active Directory B2B işbirliği API ve özelleştirme](active-directory-b2b-api.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
