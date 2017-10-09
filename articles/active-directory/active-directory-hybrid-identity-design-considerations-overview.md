---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - genel bakış | Microsoft Docs"
description: "Genel bakış ve içerik haritasını karma kimlik tasarımı hakkında dikkat edilecek noktalar Kılavuzu"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Azure Active Directory Karma Kimlik Tasarımı ile İlgili Dikkat Edilmesi Gerekenler
Tüketici tabanlı cihazlar şirket Merhaba Dünya proliferating ve bulut tabanlı hizmet olarak yazılım (SaaS) kolay tooadopt uygulamalardır. Sonuç olarak, bir iç veri merkezleri ile bulut platformlarda kullanıcıların uygulama erişim denetimini korumada görevdir.  

Microsoft'un kimlik çözümleri şirket içi ve bulut tabanlı özellikleri, tek bir kullanıcı kimliği kimlik doğrulama ve yetkilendirme için konum bağımsız olarak tooall kaynakları oluşturma span. Bu karma kimlik diyoruz. Farklı tasarım ve yapılandırma seçenekleri için Microsoft Çözüm kullanarak karma kimlik vardır ve bazı durumda hangi birleşimin hello kuruluşunuzun ihtiyaçlarını en iyi şekilde karşılayacağını zor toodetermine olması olabilir. 

Bu karma kimlik tasarımı hakkında dikkat edilecek noktalar Kılavuzu toounderstand nasıl toodesign hello iş ve teknoloji en uygun karma kimlik çözümü kuruluşunuzun gereksinimlerine yardımcı olur.  Bu kılavuzda, bir dizi adım ve görevleri, kuruluşunuzun özel gereksinimleri karşılayan bir karma kimlik çözümü tasarlama toohelp izleyebilirsiniz ayrıntıları verilmektedir. Merhaba adımlar ve görevler boyunca hello Kılavuzu hello ilgili teknolojiler ve özellik seçenekleri kullanılabilir tooorganizations toomeet işlev ve hizmet kalitesi (kullanılabilirlik, ölçeklenebilirlik, performans, yönetilebilirlik ve güvenlik gibi) sunacaktır düzeyi gereksinimleri. 

Özellikle, aşağıdaki soruları tooanswer hello hello karma kimlik tasarımı hakkında dikkat edilecek noktalar Kılavuzu hedefleri şunlardır: 

* Sorular ne tooask gerekir ve toodrive en iyi my gereksinimlerini karşıladığını bir karma kimlik özgü tasarım teknoloji veya sorun alanı için yanıt?
* Hangi etkinlikler dizisini gereken toodesign hello teknoloji veya sorun alanı için bir karma kimlik çözümü tamamlamak? 
* Hangi karma kimlik teknolojisi ve yapılandırma seçenekleri kullanılabilir toohelp bana gereksinimlerimi karşılayacak misiniz? İşimi için hello en iyi seçenek seçebilmeniz hello dengelemeler Bu seçenekler arasında nelerdir?

## <a name="who-is-this-guide-intended-for"></a>Bu kılavuz için Kime yöneliktir?
 CIO, CITO, baş kimlik mimarları, Kurumsal mimarlar ve orta veya büyük ölçekli kuruluşlarda karma kimlik çözümü tasarlamaktan sorumlu BT mimarları.

## <a name="how-can-this-guide-help-you"></a>Bu kılavuz size nasıl yardımcı olabilir?
Bu kılavuzu toounderstand kullanabileceğiniz nasıl toodesign mümkün toointegrate Bulutu olan karma kimlik çözümü kimlik yönetimi sistemi geçerli ile temel şirket içi kimlik çözümü. 

hello grafiği aşağıdaki örnek, geçerli Windows Server Active Directory bulunan çözüm ile şirket içi Microsoft Azure Active Directory tooenable kullanıcılar toouse tek BT yöneticilerine toomanage toointegrate sağlayan karma kimlik çözümü gösterir. Oturum açma (SSO) hello Bulut ve şirket içi bulunan uygulamalar arasında.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

Yukarıdaki çizimde Hello olduğu bulut yararlanan bir karma kimlik çözümü örneği Hizmetleri toointegrate sipariş tooprovide şirket içi özelliklerle tek deneyimi toohello son kullanıcı kimlik doğrulama işlemi ve toofacilitate BT yönetme Bu kaynaklar. Bu çok yaygın bir senaryo olsa da, her kuruluşun karma kimlik tasarımı büyük olasılıkla toobe toodifferent gereksinimler Şekil 1'de gösterilen hello örnek farklı ' dir. 

Bu kılavuz, bir dizi adım ve görevleri toodesign kuruluşunuzun özel gereksinimleri karşılayan bir karma kimlik çözümü izleyebilirsiniz sağlar. Merhaba aşağıdaki adımlar ve görevler, hello Kılavuzu sunar hello ilgili teknolojiler ve özellik kullanılabilir tooyou toomeet işlev ve hizmet kalite düzeyi gereksinimlerini kuruluşunuz seçenekleri.

**Varsayımlar**: Windows Server, Active Directory etki alanı Hizmetleri ve Azure Active Directory ile biraz deneyim sahibi. Bu belgede, bu çözümlerin kendi başına veya tümleşik bir çözüm içinde iş gereksinimlerinizi nasıl karşılayabileceğini görmek istediğinizi varsayarız.

## <a name="design-considerations-overview"></a>Tasarım konularına genel bakış
Bu belge, bir dizi adım ve görevin toodesign gereksinimlerinize en uygun karma kimlik çözümü izleyebilirsiniz sağlar. Merhaba adımlar sıralı halde verilmiştir. Sonraki adımlarda öğreneceğiniz tasarım konuları, önceki adımlarda, ancak tooconflicting tasarım seçenekleri toochange kararlara gerektirebilir. Tooalert her girişimde, hello belge boyunca toopotential tasarım çakışıyor. 

En iyi yalnızca adımları hello gerekli tooincorporate sayıda uygulama işlemini, gereksinimlerinize uygun hello tasarım ulaşır tüm hello belge hello konuları. 

| Karma kimlik aşaması | Konu listesi |
| --- | --- |
| Kimlik gereksinimleri belirleme |[İş gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [Dizin eşitleme gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Çok faktörlü kimlik doğrulama gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [Bir karma kimlik benimseme stratejinizi tanımlayın](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| Güçlü kimlik çözümü ile veri güvenliği iyileştirmeyi planlama |[Veri koruma gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [İçerik Yönetimi gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [Erişim denetimi gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [Olay yanıtlama gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| Karma kimlik yaşam döngüsü planlaması |[Karma kimlik yönetimi görevleri belirleme](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [Eşitleme Yönetimi](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [Karma kimlik yönetimini benimseme stratejinizi belirleme](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>Bu Kılavuzu'nu indirin
Hello hello karma kimlik tasarımı hakkında dikkat edilecek noktalar Kılavuzu bir pdf sürümünü indirebilirsiniz [Technet Galerisi](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288). 

