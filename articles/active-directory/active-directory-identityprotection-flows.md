---
title: "Azure AD Identity Protection deneyimleriyle aaaSign bileşenini | Microsoft Docs"
description: "Kimlik koruması azaltıldığından veya bir kullanıcı veya çok faktörlü kimlik doğrulama İlkesi tarafından ne zaman gerekli düzeltilen hello kullanıcı deneyimi genel bir bakış sağlar."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Oturum açma deneyimlerini Azure AD kimlik koruması
Azure Active Directory kimlik koruması ile şunları yapabilirsiniz:

* Kullanıcıların tooregister çok faktörlü kimlik doğrulamasını gerektirir
* riskli oturum açma işlemleri ve güvenliği aşılan kullanıcılar işleme

yalnızca doğrudan imzalama bir kullanıcı adı ve parola sağlayarak bileşenini artık mümkün olmayacaktır çünkü hello sistem toothese sorunları hello yanıtın bir kullanıcının oturum açma deneyimi üzerinde bir etkisi yoktur. Bir kullanıcı güvenli biçimde yedeklemeniz işletme gerekli tooget ek adımlardır.

Bu konu, oluşabilecek tüm durumlarda bir kullanıcının oturum açma deneyimini genel bir bakış sağlar.

**Multi-Factor Authentication**

* Çok faktörlü kimlik doğrulaması kayıt

**Risk altında oturum aç**

* Oturum açma riskli kurtarma
* Riskli oturum engellenen açma
* Çok faktörlü kimlik doğrulaması kayıt sırasında bir riskli oturum açma

**Risk kullanıcı**

* Gizliliği tehlikeye giren hesap kurtarma
* Engellenen gizliliği tehlikeye giren hesap

## <a name="multi-factor-authentication-registration"></a>Çok faktörlü kimlik doğrulaması kayıt
her ikisi için de en iyi kullanıcı deneyimini Merhaba, gizliliği tehlikeye giren hesap kurtarma akışı hello ve oturum açma riskli akış Merhaba, hello kullanıcı kendi kendine kurtarabilirsiniz durumdur. Kullanıcılar için multi-Factor authentication kaydettiyseniz, zaten kullanılan toopass güvenlik tehditlerine olabilir, hesabıyla ilişkili bir telefon numarası sahiptirler. Yardım masasına veya yöneticinize katılımı hesabı güvenliğinin aşılmasına gelen gerekli toorecover ' dir. Bu nedenle, tooget kullanıcılarınızın tavsiye çok faktörlü kimlik doğrulaması için kayıtlı. 

Yöneticiler şunları yapabilir:

* Kullanıcıların tooset kendi hesaplarını ek güvenlik doğrulaması gerektiren bir ilke ayarlayın. 
* çok faktörlü kimlik doğrulaması kayıt too30 günlerini atlanıyor toogive kullanıcıların istedikleri durumunda izin kaydetmeden önce bir yetkisiz kullanım süresi.

**Merhaba çok faktörlü kimlik doğrulaması kayıt üç adım vardır:**

1. Merhaba ilk adımda hello kullanıcı hello gereksinim tooset hello hesabı çok faktörlü kimlik doğrulama kaydınızı hakkında bir bildirim alır. 
   
    ![Düzeltme](./media/active-directory-identityprotection-flows/140.png "düzeltme")
2. tooset çok faktörlü kimlik doğrulamasını kurma toolet hello sistem ihtiyacınız temas toobe istediğiniz bildirin.
   
    ![Düzeltme](./media/active-directory-identityprotection-flows/141.png "düzeltme")
3. bir challenge tooyou Hello sistem gönderir ve toorespond gerekir.
   
    ![Düzeltme](./media/active-directory-identityprotection-flows/142.png "düzeltme")

## <a name="risky-sign-in-recovery"></a>Oturum açma riskli kurtarma
Yönetici oturum açma riskler için bir ilke şekilde yapılandırdığında toosign içinde çalıştıklarında hello etkilenen kullanıcılara bildirilir. 

**oturum açma Hello riskli akışı iki adımı vardır:** 

1. olağan dışı bir şey hakkında kendi oturum yeni konumu, cihaz veya uygulama oturum açma gibi algılandı Hello kullanıcı bilgilendirilir. 
   
    ![Düzeltme](./media/active-directory-identityprotection-flows/120.png "düzeltme")
2. Merhaba kullanıcı gerekli tooprove kendi güvenlik sınaması çözme tarafından kimliğidir. Merhaba kullanıcı çok faktörlü kimlik doğrulaması için kayıtlı değilse tooround seyahat bir güvenlik kodu tootheir telefon numarası ihtiyaç duyar. Bu yalnızca bir olduğundan riskli bir oturum açma ve güvenliği aşılmış bir hesabı değil, hello kullanıcı bu akışında toochange hello parola sahip olmaz. 
   
    ![Düzeltme](./media/active-directory-identityprotection-flows/121.png "düzeltme")

## <a name="risky-sign-in-blocked"></a>Riskli oturum engellenen açma
Yöneticiler, bir oturum açma riski İlkesi tooblock kullanıcılar oturum açma hello risk düzeyi bağlı olarak bağlı tooset de seçebilirsiniz. engeli kaldırılmış tooget, son kullanıcıların yöneticinize veya yardım masasına başvurun veya tanıdık konumu ya da cihaz açmayı deneyin. Çok faktörlü kimlik doğrulaması çözme tarafından otomatik olarak kurtarma seçeneği bu durumda değil.

![Düzeltme](./media/active-directory-identityprotection-flows/200.png "düzeltme")

## <a name="compromised-account-recovery"></a>Gizliliği tehlikeye giren hesap kurtarma
Bir kullanıcı risk Güvenlik İlkesi yapılandırıldığında hello kullanıcı karşılayan kullanıcılar risk düzeyi hello İlkesi'nde belirtilen (ve bu nedenle varsayılır tehlikeye), oturum açma önce hello kullanıcı güvenliğinin aşılmasına kurtarma aktığı gitmeniz gerekir. 

**Merhaba kullanıcı güvenliğinin aşılmasına kurtarma akışı üç adım vardır:**

1. Merhaba kullanıcı, kendi hesabı güvenlik riski nedeniyle şüpheli etkinlik olduğu veya kimlik bilgilerini sızmasını bilgilendirilir.
   
    ![Düzeltme](./media/active-directory-identityprotection-flows/101.png "düzeltme")
2. Merhaba kullanıcı gerekli tooprove kendi güvenlik sınaması çözme tarafından kimliğidir. Merhaba kullanıcı çok faktörlü kimlik doğrulaması için kayıtlı değilse, güvenliğinin bozulması riskini Self kurtarabilirsiniz. Bunlar tooround seyahat bir güvenlik kodu tootheir telefon numarası gerekir. 
   
   ![Düzeltme](./media/active-directory-identityprotection-flows/110.png "düzeltme")
3. Son olarak, kullanıcı hello zorlanmış toochange parolalarını olduğu başka birisi erişim tootheir hesabı olmuş olabilir. 
   Aşağıda bu deneyim ekran görüntüleri verilmiştir.
   
   ![Düzeltme](./media/active-directory-identityprotection-flows/111.png "düzeltme")

## <a name="compromised-account-blocked"></a>Engellenen gizliliği tehlikeye giren hesap
tooget engeli kaldırılmış bir kullanıcı risk güvenlik ilkesi tarafından engellenen bir kullanıcı, hello kullanıcı bir yönetici veya yardım masasına başvurmanız gerekir. Çok faktörlü kimlik doğrulaması çözme tarafından otomatik olarak kurtarma seçeneği bu durumda değil.

![Düzeltme](./media/active-directory-identityprotection-flows/104.png "düzeltme")

## <a name="reset-password"></a>Parola sıfırlama
Güvenliği aşılmış kullanıcıların açmasını engellenirse yönetici kendileri için geçici bir parola oluşturun. Merhaba kullanıcılar toochange, bir sonraki oturum açma sırasında parolalarını sahip olacaktır.

![Düzeltme](./media/active-directory-identityprotection-flows/160.png "düzeltme")

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) 

