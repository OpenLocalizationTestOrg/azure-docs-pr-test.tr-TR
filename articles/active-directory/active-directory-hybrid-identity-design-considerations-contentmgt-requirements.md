---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - içerik yönetimi gereksinimlerini belirleme | Microsoft Docs"
description: "İçine nasıl toodetermine hello işinizin içerik yönetimi gereksinimleri hakkında bilgi sağlar. Genellikle bir kullanıcı kendi aygıt olduğunda kendisi de kullandığı according toohello uygulama değişen birden çok kimlik olabilir. Bu, önemli toodifferentiate hangi içerik hello Kurumsal kimlik bilgileri kullanılarak oluşturulan olanları karşı kişisel kimlik bilgileri kullanılarak oluşturulmuş olur. Kimlik çözümünüzün bir deneyim toohello son kullanıcı sırasında bulut Hizmetleri tooprovide ile mümkün toointeract olmalıdır kendi gizlilik sağlamak ve veri sızıntısına karşı koruma hello artırın."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a>Karma kimlik çözümü için içerik yönetimi gereksinimlerini belirleyin
İşinizi yönlendirebilir için hello içerik yönetimi gereksinimleri anlama kararınızı hangi karma kimlik çözümü toouse üzerindeki etkiler. İle birden çok aygıtların artışı ve kullanıcıların toobring hello yeteneğini kendi cihazlarını hello ([KCG](http://aka.ms/byodcg)), hello şirket kendi verilerini korumak gerekir, ancak bu ayrıca kullanıcının gizliliğini korumanız gerekir. Genellikle bir kullanıcı kendi aygıt olduğunda kendisi de kullandığı according toohello uygulama değişen birden çok kimlik olabilir. Bu, önemli toodifferentiate hangi içerik hello Kurumsal kimlik bilgileri kullanılarak oluşturulan olanları karşı kişisel kimlik bilgileri kullanılarak oluşturulmuş olur. Kimlik çözümünüzün bir deneyim toohello son kullanıcı sırasında bulut Hizmetleri tooprovide ile mümkün toointeract olmalıdır kendi gizlilik sağlamak ve veri sızıntısına karşı koruma hello artırın. 

Kimlik çözümünüzü farklı teknik denetimler sipariş tooprovide İçerik Yönetimi'nde hello aşağıdaki çizimde gösterildiği gibi işlevden:

![](./media/hybrid-id-design-considerations/securitycontrols.png)

**Kimlik yönetimi sistemi yararlanarak güvenlik denetimleri**

Genel olarak, içerik yönetimi gereksinimlerini Kimlik Yönetimi sisteminizde alanları aşağıdaki hello özelliğinden yararlanır:

* Gizlilik: bir kaynağın sahibi hello kullanıcı tanımlama ve hello uygun denetimleri toomaintain bütünlüğü uygulanıyor.
* Veri Sınıflandırması: hello kullanıcıyı veya grubu ve tooits sınıflandırma göre erişimi tooan nesnesi düzeyini belirleyin. 
* Veri sızıntısı koruma: güvenlik denetimleri veri tooavoid sızıntısı koruma sorumluluğunu hello kimlik sistemi toovalidate hello kullanıcı kimliği ile toointeract gerekir. Bu da izi amacı denetimi için önemlidir.

> [!NOTE]
> Okuma [bulut hazırlık için veri sınıflandırma](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) en iyi yöntemler ve veri sınıflandırması için yönergeleri hakkında daha fazla bilgi.
> 
> 

Karma kimlik çözümü planlama olun olduğunda aşağıdaki o hello tooyour kuruluşunuzun gereksinimlerine göre soruları yanıtlanır:

* Şirketinizin güvenlik denetimleri yer tooenforce veri gizlilik var mı?
  * Yanıt Evet ise, bu güvenlik denetimleri, devam eden tooadopt olduğunuzu hello karma kimlik çözümü ile mümkün toointegrate olacak?
* Şirketiniz veri sınıflandırması kullanıyor mu?
  * Yanıt Evet ise, hello geçerli çözüm mümkün toointegrate hello karma kimlik çözümü giderek tooadopt olduğunuz ile mi?
* Şirketiniz veri sızıntısı için herhangi bir çözümü şu anda var mı? 
  * Yanıt Evet ise, hello geçerli çözüm mümkün toointegrate hello karma kimlik çözümü giderek tooadopt olduğunuz ile mi?
* Şirketinizin tooaudit erişim tooresources gerekiyor mu?
  * Yanıt Evet ise, hangi kaynakları tür?
  * Yanıt Evet ise, hangi bilgilerin düzeyini gerekli mi?
  * Yanıt Evet ise, hello denetim günlüğü bulunduğu gerekir? Şirket içi veya hello bulutta?
* Şirketinizin hassas veriler (Ssn'ler, kredi kartı numaraları, vb.) içeren e-postaları tooencrypt gerekiyor mu?
* Şirketinizin tooencrypt dış iş ortaklarıyla paylaşılan tüm belgeler/içerik gerekiyor mu?
* Şirketinizin e-postalar belirli türdeki tooenforce şirket ilkeleri gerekiyor mu (tüm yanıt yapmak için iletme)?

> [!NOTE]
> Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun. [Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) hello seçenekleri ve her seçeneğin olumlu/olumsuz üzerinden geçer.  Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
[Erişim denetimi gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a>Ayrıca Bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

