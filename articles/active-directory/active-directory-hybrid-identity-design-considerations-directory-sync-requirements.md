---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - dizin eşitleme gereksinimlerini belirleme | Microsoft Docs"
description: "Hangi gereksinimler tüm hello kullanıcılar arasında eşitlemek için gerekli olan tanımlamak şirket içi ve bulut hello kuruluş için on =."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>Dizin eşitleme gereksinimlerini belirleyin
Eşitleme, kullanıcıların kendi şirket içi kimliğine göre hello bulutta bir kimlik sağlama tüm hakkında olur. Kimlik doğrulaması veya şirket dışı kimlik doğrulaması için eşitlenmiş hesap kullanacakları olmadığını hello kullanıcılar yine toohave hello bulutta bir kimlik gerekir.  Bu kimlik korunur ve düzenli aralıklarla güncelleştirilen toobe gerekir.  Merhaba güncelleştirmeleri başlık değişiklikleri toopassword değişikliklerden birçok biçimde olabilir.  

Çözüm ve kullanıcı Hello kuruluşlar şirket içi kimlik gereksinimleri değerlendirerek başlatın. Bu değerlendirme nasıl kullanıcı kimlikleri oluşturulacak ve hello bulutta saklanır önemli toodefine hello teknik gereksinimleri ' dir.  Kuruluşların çoğunluğunun, şirket içi Active Directory verilir ve kullanıcılar tarafından olacak hello şirket içi dizin, ancak bazı durumlarda bu hello durumda olmayacaktır, eşitlenir.  

Aşağıdaki sorular emin tooanswer hello olun:

* Bir AD ormanında, birden çok veya hiçbiri var mı?
  
  * Kaç tane Azure AD dizinler için eşitleme?
    
    1. Filtreleme kullanıyor musunuz?
    2. Planlanan birden çok Azure AD Connect sunucuları var mı?
* Şu anda bir eşitleme elinizde aracı şirket içi?
  
  * Kullanıcıların kimliklerinin sanal bir dizin/tümleştirme varsa Evet ise, kullanıcılarınızın mu?
* Tüm diğer dizin toosynchronize (örn. LDAP dizini, ik veritabanını, vb.) istediğiniz şirket içi var mı?
  * Tüm GALSync yapılması toobe mısınız?
  * Merhaba geçerli durumunu UPN'ler kuruluşunuzdaki nedir? 
  * Kullanıcıların kimlik doğrulaması farklı bir dizin var mı?
  * Şirketiniz Microsoft Exchange kullanıyor mu?
    * Bunlar, karma bir exchange dağıtım sahip planlıyor musunuz?

Eşitleme gereksinimleri hakkında bir fikir sahip olduğunuza göre bu gereksinimleri hello doğru bir toomeet araçtır toodetermine gerekir.  Microsoft, çeşitli araçlar tooaccomplish dizin tümleştirme ve eşitleme sağlar.  Merhaba bkz [karma kimlik dizini tümleştirme araçları karşılaştırması tablo](active-directory-hybrid-identity-design-considerations-tools-comparison.md) daha fazla bilgi için. 

Eşitleme gereksinimlerini ve bu, şirketiniz için yapabiliriz hello aracı sahip olduğunuza göre bu dizin hizmetleri kullanan tooevaluate hello uygulamaları gerekir. Bu değerlendirme toodefine hello teknik gereksinimleri toointegrate bu uygulamaları toohello bulut önemlidir. Aşağıdaki sorular emin tooanswer hello olun:

* Bu uygulamalar taşınan toohello olur Bulut ve hello dizini kullanmak?
* Bu uygulamalar başarıyla kullanabilmeniz için eşitlenen toobe toohello bulut gereken özel öznitelikler var mı?
* Bu uygulamalar, bulut kimlik doğrulama tootake avantajlarından yeniden yazılmış toobe gerekiyor mu?
* Kullanıcıların erişmesine karşın bu uygulamaları içi toolive devam edecek hello bulut kimliği kullanarak?

Ayrıca toodetermine hello güvenlik gereksinimleri ve kısıtlamaları dizin eşitlemesi gerekir. Bu değerlendirme önemli tooget bir sipariş toocreate gerekli olacağını ve kullanıcının kimlikleri hello bulutta korumak hello gereksinimleri listesi olur. Aşağıdaki sorular emin tooanswer hello olun:

* Burada hello eşitleme sunucusu bulunur?
* Etki alanına katılmış olacak?
* Merhaba sunucu kısıtlanmış bir ağda DMZ gibi bir güvenlik duvarının arkasında bulunan?
  * Mümkün tooopen hello gerekli güvenlik duvarı bağlantı noktaları toosupport eşitleme olacak?
* Merhaba eşitleme sunucusu için bir olağanüstü durum kurtarma planı var mı?
* Merhaba toosynch ile istediğiniz tüm orman için doğru izinlere sahip bir hesap var mı?
  * Şirketiniz Bu soru için hello yanıt bilmiyor hello makale "Parola Eşitleme izinlerini" bölümünde hello inceleyin [yükleme hello Azure Active Directory eşitleme hizmeti](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) ve zaten olup olmadığını belirlemek bir Bu izinlere sahip olan hesabı veya bir toocreate ihtiyacınız varsa.
* Varsa belirleyebiliriz orman eşitleme hello eşitleme sunucusu mümkün tooget tooeach orman mı?

> [!NOTE]
> Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun. [Olay yanıtlama gereksinimlerini belirlemek](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) hello seçeneklerin geçilir. Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
[Çok faktörlü kimlik doğrulama gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>Ayrıca bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

