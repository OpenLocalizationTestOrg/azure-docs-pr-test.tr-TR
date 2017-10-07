---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - belirlemek erişim denetimi gereksinimlerine | Microsoft Docs"
description: "Kapak kimlik ve karma bir ortamda kullanıcıları için kaynaklar tanımlayıcı erişim gereksinimlerini ayaklar hello."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a>Karma kimlik çözümü için erişim denetimi gereksinimleri belirleme
Bir kuruluş tasarlarken toomake planladığınıza gereksinimleri hello kaynaklar için erişim de kullanabilecekleri bu fırsatı tooreview kendi karma kimlik çözümü, kullanıcılar için kullanılabilir. Merhaba veri erişimi olan tüm dört ayaklar kimliğini, çapraz:

* Yönetim
* Kimlik Doğrulaması
* Yetkilendirme
* Denetim

izleyen hello bölümleri kimlik doğrulama ve yetkilendirme daha ayrıntılı ele alınacaktır, yönetim ve denetimi hello karma kimlik yaşam döngüsü parçasıdır. Okuma [karma kimlik yönetimi görevleri belirlemek](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) bu özellikleri hakkında daha fazla bilgi için.

> [!NOTE]
> Okuma [hello dört ayaklar kimliği - hello karma BT yaş Identity Management](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) bu dayanaklarından her biri hakkında daha fazla bilgi.
> 
> 

## <a name="authentication-and-authorization"></a>Kimlik doğrulama ve yetkilendirme
Kimlik doğrulama ve yetkilendirme için farklı senaryolar vardır, bu senaryoların hello karma kimlik çözümü tarafından hello şirket giderek tooadopt olduğunu yerine getirilmesi gereken belirli gereksinimleri vardır. Merhaba kuruluş tarafından kullanılan kimlik doğrulama ve yetkilendirme yöntemi hello iş ortaklarıyla iletişim kurabilir tooensure gerekir bu yana iş tooBusiness (B2B) içeren senaryoları iletişimi için BT yöneticileri bir ek sınama ekleyebilirsiniz. Kimlik doğrulama ve yetkilendirme gereksinimlerine yönelik işlemini tasarlama hello sırasında aşağıdaki soruları bu hello yanıtlanır emin olun:

* Kuruluşunuzun kimlik doğrulaması ve kimlik yönetimi sistemlerine bulunan kullanıcıları yetkilendirmek?
  * B2B senaryolarını için herhangi bir plan var mı?
  * Yanıt Evet ise, zaten hangi protokollerin (SAML, OAuth, Kerberos, belirteçleri veya Sertifikalar) olacak bilebilirsiniz hem işletmeler kullanılan tooconnect olabilir?
* Merhaba karma kimlik çözümü tooadopt kalacaklarını protokollerin destekliyor mu?

Başka bir önemli nokta tooconsider burada kullanıcılar ve iş ortakları tarafından kullanılacak hello kimlik doğrulama deposu bulunur ve kullanılan hello yönetim modeli toobe ' dir. Aşağıdaki iki çekirdek seçenekleri şu hello göz önünde bulundurun:

* Merkezi: Bu modeli hello kullanıcının kimlik bilgilerini, ilkeleri ve Yönetim Merkezi şirket içi olabilir veya hello bulutta.
* Karma: Bu modeli hello kullanıcının kimlik bilgilerini, ilkeleri ve Yönetim Merkezi şirket içi ve çoğaltılan hello bulutta olacaktır.

Kuruluşunuz benimseyeceği hangi model according tootheir iş gereksinimleri farklılık gösterir, burada hello kimlik yönetimi sistem bulunan ve Yönetici modu toouse hello soruları tooidentify aşağıdaki tooanswer hello istiyor:

* Kuruluşunuz şu anda bir kimlik yönetimi sahip şirket içi?
  * Yanıt Evet ise, tookeep planlıyor musunuz?
  * Kuruluşunuz bu belirtir hello kimlik yönetimi sistemi bulunduğu izlemelisiniz düzenleme veya uyumluluk gereksinimleri var mı?
* Kuruluşunuz çoklu oturum açma bulunan uygulamalar şirket içi veya hello bulutta kullanıyor mu?
  * Yanıt Evet ise, bir karma kimlik modelin hello benimseme bu işlem etkiliyor mu?

## <a name="access-control"></a>Access Control
Kimlik doğrulama ve yetkilendirme çekirdek öğeleri tooenable erişim toocorporate verilerine kullanıcının doğrulama olsa da, bu da önemli toocontrol hello bu kullanıcıların ve erişim yöneticileri hello düzeyini hello olacak bir erişim düzeyidir yönetmekte olduğunuz kaynaklar. Karma kimlik çözümü mümkün tooprovide ayrıntılı erişim tooresources, temsilci seçme ve rol tabanlı erişim denetimini olması gerekir. Soru aşağıdaki o Merhaba, erişim denetimi ile ilgili yanıtlanır emin olun:

* Şirketiniz yükseltilmiş ayrıcalık toomanage ile birden fazla kullanıcı, kimlik sistemi var mı?
  * Evet, her kullanıcı hello mu gerekiyorsa aynı erişim düzeyi?
* Şirket gerek toodelegate erişim toousers toomanage belirli kaynaklarınıza musunuz?
  * Yanıt Evet ise, bu ne sıklıkta olur?
* Şirket içi ve bulut arasında toointegrate erişim denetimi özelliklerinden gerekir kaynakları?
* Şirketiniz toosome koşullara göre toolimit erişim tooresources gerekiyor mu?
* Şirketiniz özel denetim toosome kaynaklarına erişim gerektiren herhangi bir uygulama bulunur?
  * Yanıt Evet ise, burada uygulamalarla bulunur (şirket içi veya hello bulutta)?
  * Yanıtınız evet ise, burada olan bu hedef kaynaklara (şirket içi veya hello bulutta)?

> [!NOTE]
> Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun. [Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) hello seçenekleri ve her seçeneğin olumlu/olumsuz üzerinden geçer.  Bu soruyu yanıtlayarak, iş gereksinimlerinize en iyi hangi seçeneği en seçersiniz.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
[Olay yanıtlama gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a>Ayrıca Bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

