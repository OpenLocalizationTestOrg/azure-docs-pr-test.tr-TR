---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - belirlemek olay rResponse gereksinimleri | Microsoft Docs"
description: "BT tootake Eylemler tooidentify tarafından yararlanılabilir ve olası tehdit risklerini azaltmanıza hello karma kimlik çözümü için izleme ve raporlama özelliklerini belirleme"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Karma kimlik çözümü için olay yanıtlama gereksinimlerini belirleyin
Büyük veya orta ölçekli kuruluşlarda büyük olasılıkla sahip olacak bir [güvenlik olay yanıtlama](https://technet.microsoft.com/library/cc700825.aspx) yer toohelp BT buna göre eylemleri olay toohello düzeyi. Merhaba hedefe karşı belirli bir eylemi gerçekleştiren kişiye tanımlayan kullanılan toohelp olabileceğinden hello kimlik yönetimi sistemi hello olay yanıtlama işlemindeki önemli bir bileşendir. Merhaba karma kimlik çözümü izleme ve raporlama, BT tootake Eylemler tooidentify tarafından yararlanılabilir ve olası tehdidi azaltmak özellikleri mümkün tooprovide olması gerekir. Bir genel olay yanıtlama planında aşamaları hello planının bir parçası aşağıdaki hello olacaktır:

1. İlk değerlendirmesi.
2. Olay iletişim.
3. Hasar denetim ve risk azaltma.
4. Ne tanımlaması güvenliğinin aşılması ve önem derecesi oluştu.
5. Kanıt koruma.
6. Bildirim tooappropriate tarafların.
7. Sistem Kurtarma.
8. Belgeler.
9. Hasar ve maliyet değerlendirmesi.
10. İşlem ve planı gözden geçirme.

BT'nin Hello tanımlaması sırasında güvenliğinin aşılması ve önem derecesi aşaması, aşılmış, gerekli tooidentify hello sistemleri erişilen ve bu dosyaların hello duyarlılık belirlemek dosyalar olacaktır. Karma kimlik sistemi mümkün toofulfill bu gereksinimleri tooassist olmalıdır, bu değişiklikler hello kullanıcı tanımlama. 

## <a name="monitoring-and-reporting"></a>İzleme ve Raporlama
Çoğunlukla hello sistem denetim ve raporlama özellikleri içinde yerleşik olan birçok kez hello kimlik sistemi ayrıca ilk değerlendirme aşamasında yardımcı olabilir. Merhaba ilk değerlendirme sırasında BT yöneticisi mümkün tooidentify kuşkulu bir etkinlik olmalıdır veya hello sistem otomatik olarak önceden yapılandırılmış bir görev tabanlı mümkün tootrigger olmalıdır. Diğer durumlarda, hatalı yapılandırılmış bir sistem tooa sayıda hatalı pozitif sonuç bir yetkisiz erişim algılama sisteminde neden olabilir ancak birçok etkinlik olası bir saldırı olduğunu gösteriyor olabilir. 

Merhaba kimlik yönetimi sistemi, BT yöneticileri tooidentify yardımcı olmak ve bu kuşkulu etkinlikleri rapor gerekir. Genellikle bu teknik gereksinimleri tüm sistemler izleme ve olası tehditler vurgulamak bir raporlama özelliği sahip uyması gereken. Merhaba soruları kullanın, karma kimlik çözümü göz önünde bulundurarak olay yanıtlama gereksinimlerini alırken çalışırken Tasarım toohelp:

* Mu şirketinizin sahip bir güvenlik olay yanıtı yerinde?
  * Yanıt Evet ise, hello geçerli kimlik yönetimi sistemi hello işleminin bir parçası kullanılır?
* Şirketinizin farklı cihazlarda kullanıcılardan tooidentify şüpheli oturum açma denemelerinin gerekiyor mu?
* Şirketinizin toodetect olası güvenliği aşılmış kullanıcının kimlik bilgileri gerekiyor mu?
* Şirketinizin tooaudit kullanıcının erişim ve eylem gerekiyor mu?
* Bir kullanıcı parolasını sıfırladığınızda şirket tooknow gerekiyor mu?

## <a name="policy-enforcement"></a>İlke zorlama
Hasar denetim ve risk azaltma-aşaması sırasında tooquickly azaltmak saldırının hello gerçek ve olası etkileri önemlidir. Sizi yönlendirir o eylemi bu noktada bir küçük ve büyük bir hello farkı yapabilirsiniz. Merhaba tam yanıtı kuruluşunuz ve karşılaştığınız hello saldırı hello doğasına bağlı olacaktır. Bir hesap aşılmış Hello ilk değerlendirme sonuçları, bu hesap tooenforce İlkesi tooblock gerekir. Hello kimlik yönetimi sistemi işlevden burada yalnızca bir örnektir. İlkeleri nasıl olacaktır göz önünde bulundurarak tooreact tooan devam eden olay zorlanan sırada karma kimlik çözümü tasarlama toohelp aşağıda Hello soruları kullanın:

* Şirket ilkeleri yer tooblock kullanıcıların erişim hello ağdan gerekirse var mı?
  * Yanıt Evet ise, hello geçerli çözüme giderek tooadopt olduğunuz hello karma kimlik yönetimi sistemi ile tümleşik çalışıyor mu?
* Şirketinizin Karantinada bulunan kullanıcılar için tooenforce koşullu erişim gerekiyor mu? 

> [!NOTE]
> Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun. [Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) hello seçenekleri ve her seçeneğin olumlu/olumsuz üzerinden geçer.  Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
[Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Ayrıca Bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

