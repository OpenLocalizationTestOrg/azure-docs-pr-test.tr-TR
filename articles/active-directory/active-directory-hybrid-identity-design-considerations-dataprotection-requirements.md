---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - veri koruma gereksinimlerini belirleme | Microsoft Docs"
description: "Karma kimlik çözümünüzü planlarken tanımladığınızda, işletmeniz için hello veri koruma gereksinimlerini ve hangi seçeneklerin kullanılabilir toobest olduğunu bu gereksinimleri karşılamak."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Güçlü kimlik çözümü ile veri güvenliği iyileştirmeyi planlama
Merhaba ilk adım tooprotect hello bu verilere kimlerin erişebileceğini belirlemek ve bu işlemin bir parçası olarak için bir kimlik çözümü, sistem tooprovide kimlik doğrulama ve yetkilendirme özellikleriyle tümleşen toohave gerekiyor verilerdir. Kimlik doğrulama ve Yetkilendirme genellikle birbiriyle yanıltıcı olmaktadır ve rollerine yanlış. Gerçekte hello aşağıdaki çizimde gösterildiği gibi oldukça farklı bunlar:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Mobil cihaz Yönetimi yaşam döngüsünün aşamaları**

Karma kimlik çözümü planlarken hello veri koruma gereksinimlerini ve hangi seçeneklerin kullanılabilir toobest olduğunu işinizin bu gereksinimleri karşılamak anlamanız gerekir.

> [!NOTE]
> Veri güvenliği için planlama tamamladıktan sonra gözden [çok faktörlü kimlik doğrulama gereksinimlerini belirlemek](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) seçimlerinizi çok faktörlü kimlik doğrulama gereksinimleri ile ilgili hello kararları tarafından etkilenmeyen tooensure Bu bölümde yapılan.
> 
> 

## <a name="determine-data-protection-requirements"></a>Veri koruma gereksinimlerini belirleme
Mobility Hello geçerlilik süresi içinde çoğu şirketin ortak bir hedefe sahip: herhangi bir yere sipariş tooincrease üretkenliği açısından mobil cihazlarını şirket içi veya uzaktan üretken gelen kendi kullanıcılar toobe etkinleştirin. Bu ortak bir hedefe olabilir ancak bu tür gereksinim şirketler de güvenli sipariş tookeep şirketin verilerini azaltılması gereken ve kullanıcı gizliliğini tehditler hello miktarı ile ilgili sorun. Her şirketin farklı gereksinimleri bu bağlamda olabilir; according toowhich endüstri hello şirket değişir farklı uyumluluk kuralları hareket toodifferent tasarım kararlarına yol açar. 

Ancak, hello sonraki bölümde açıklanacak, hello sektörden bağımsız doğrulandı ve incelediniz bazı güvenlik konuları vardır.

## <a name="data-protection-paths"></a>Veri koruma yolları
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Veri koruma yolları**

Yukarıdaki diyagramda Hello hello kimliği bileşenini hello veri erişmeden önce doğrulandı ilk toobe olacaktır. Ancak, bu veriler farklı durumlarda erişilmiş olan hello sırada olabilir. Bu diyagramdaki her sayı, veri zamanında bir noktada bulunabilir yolu temsil eder. Bu sayı, aşağıda açıklanmıştır:

1. Merhaba cihaz düzeyinde veri koruma.
2. Aktarım sırasında veri koruması.
3. Rest şirket içi karşın, veri koruma.
4. Veri koruma beklerken hello bulutta.

Bu aşamalar her biri BT tooprotect hello verilerin kendisini etkinleştirecek hello teknik denetimler hello karma kimlik çözümü tarafından doğrudan sunulmayan rağmen hello karma kimlik çözümü her iki şirket içi yararlanarak kapasitesine sahip olduğunu gerekli ve bulut Kimlik Yönetimi kaynakları tooidentify hello kullanıcı grant erişim toohello veri önce. Karma kimlik çözümü planlama olun olduğunda aşağıdaki o hello tooyour kuruluşunuzun gereksinimlerine göre soruları yanıtlanır:

## <a name="data-protection-at-rest"></a>Bekleyen verilerin korunması konusunda
Merhaba veri bekleyen (cihaz, Bulut veya şirket içi) nerede olduğuna bakılmaksızın, tooperform değerlendirme toounderstand hello kuruluşun bu bağlamda gerekli önemlidir. Bu alan için aşağıdaki soruları bu hello istendi emin olun:

* Şirketinizin rest tooprotect verileri gerekiyor mu?
  * Yanıtınız evet ise, hello karma kimlik çözümü mümkün toointegrate geçerli şirket içi altyapınıza mı?
  * Yanıt Evet ise, hello buluttaki, iş yükleri ile Merhaba karma kimlik çözümü mümkün toointegrate mi?
* Merhaba bulut Kimlik Yönetimi mümkün tooprotect hello kullanıcının kimlik bilgilerini ve diğer verileri hello bulutta depolanan nedir?

## <a name="data-protection-in-transit"></a>Aktarımdaki verileri koruma
Aktarım veya hello aygıt ile Merhaba bulut hello cihaz ve hello veri merkezi arasında verileri korunması gerekir. Ancak, aktarım sırasında olan mutlaka bulut hizmetiniz dışında bir bileşen olan bir iletişim işlem gelmez; Ayrıca, dahili olarak, taşır iki sanal ağ arasında gibi. Bu alan için aşağıdaki soruları bu hello istendi emin olun:

* Şirketinizin aktarım tooprotect verileri gerekiyor mu?
  * Yanıt Evet ise, SSL/TLS gibi güvenli denetimleriyle hello karma kimlik çözümü mümkün toointegrate mi?
* Merhaba bulut Kimlik Yönetimi hello trafiği tooand imzalı hello dizin (içinde ve veri merkezleri arasında) içinde saklama mu?

## <a name="compliance"></a>Uyumluluk
Şirket ait according toohello endüstri düzenlemeleri, yasa ve yönetmeliklere uygunluğu gereksinimleri farklılık gösterir. Yüksek düzenlenen sektörlerde şirketlerde kimlik yönetimi sorunları ilgili toocompliance konuları incelemeniz gerekir. Sarbanes-Oxley (SOX), hello Sağlık Sigortası Taşınabilirlik ve Sorumluluk Yasası (HIPAA), gibi düzenlemeleri hello Gramm Leach Bliley Act (GLBA) ve kimlik ve erişim ile ilgili hello ödeme kartı sektör veri güvenliği standardı (PCI DSS) çok sıkı. bir veya daha fazla bu yönetmelikler hello gereksinimlerini karşılar hello çekirdek özellikler, şirketin benimseyeceği hello karma kimlik çözümü olması gerekir. Bu alan için aşağıdaki soruları bu hello istendi emin olun:

* Merhaba karma kimlik çözümü işletmeniz için hello yasal gereksinimleriyle uyumlu mu?
* Mu hello karma kimlik çözümü, şirket toobe uyumlu yasal gereksinimlerinizi sağlayacak özellikleri yerleşik olan? 

> [!NOTE]
> Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun. [Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) hello seçenekleri ve her seçeneğin olumlu/olumsuz üzerinden geçer.  Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
 [İçerik Yönetimi gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Ayrıca Bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

