---
title: "Azure AD Connect eşitleme: teknik kavramlar | Microsoft Docs"
description: "Azure AD Connect eşitleme Hello teknik kavramlarını açıklar."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Azure AD Connect Eşitleme: Teknik Kavramlar
Bu makalede hello konu özetidir [anlama mimarisi](active-directory-aadconnectsync-technical-concepts.md).

Azure AD Connect eşitleme bir düz meta dizin eşitleme platformu oluşturur.
Aşağıdaki bölümlerde hello meta dizin eşitleme hello kavramlarını tanıtır.
MIIS, ILM ve FIM temel oluşturma, hello Azure Active Directory Eşitleme Hizmetleri hello sonraki platformu bağlanan toodata kaynakları için sağlama ve kimlikler etkinleştirmektir hello yanı sıra veri kaynakları arasında veri eşitlenirken sağlar.

![Teknik Kavramlar](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Aşağıdaki bölümlerde hello hello FIM eşitleme hizmeti yönlerini aşağıdaki hello hakkında daha fazla ayrıntı sağlar:

* Bağlayıcı
* Öznitelik akışı
* Bağlayıcı alanı
* Meta veri deposu
* Sağlama

## <a name="connector"></a>Bağlayıcı
bağlı bir dizin ile kullanılan toocommunicate olan hello kod modülleri bağlayıcılar (önceki adıyla (MAs) yönetim aracıları olarak da bilinen) adı verilir.

Bu Azure AD Connect eşitleme çalıştıran hello bilgisayara yüklenir. Merhaba bağlayıcıları özelleştirilmiş aracıları hello dağıtımını güvenmek yerine uzak sistem protokolleri kullanılarak hello aracısız özelliği tooconverse sağlar. Bunun anlamı azalmasına risk ve dağıtım zamanlarını, özellikle Kritik uygulamalar ve sistemler ile ilgilenirken.

Resim hello yukarıdaki hello bağlayıcı hello bağlayıcı alanı ile çalışır ancak hello dış sistem ile tüm iletişim kapsar.

Tüm alma ve verme işlevselliği toohello sistem ve toounderstand nasıl gerek gelen geliştiriciler boşaltır için hello bağlayıcı sorumludur yerel bildirim temelli hazırlama toocustomize veri dönüşümleri kullanırken tooconnect tooeach sistem.

İçeri ve dışarı aktarmalar yalnızca zamanlanmış yalıtımı değişiklikleri otomatik olarak toohello bağlı veri kaynağı değil yayıldığından hello sistem içinde gerçekleşen değişikliklere karşı daha fazla izin vermeyi oluşur. Ayrıca, geliştiricilerin toovirtually herhangi bir veri kaynağını bağlamak için kendi bağlayıcılarını oluşturabilir.

## <a name="attribute-flow"></a>Öznitelik akışı
Merhaba meta veri deposu, bağlayıcı alanları komşu gelen tüm birleştirilmiş kimlikleri, birleştirilmiş hello görünümüdür. Merhaba Yukarıdaki şekilde, hem gelen hem de giden akış için ok uçları satırıyla tarafından öznitelik akışı belirtilmiştir. Öznitelik akışı kopyalama veya bir sistem tooanother verileri dönüştürme hello işlemidir ve tüm akışlar (gelen veya giden) öznitelik.

Eşitleme (tam veya delta) zamanlanmış toorun işlemlerdir öznitelik akışı hello meta veri deposu hello bağlayıcı alanı arasında çift yönlü oluşur.

Öznitelik akışı yalnızca bu eşitlemeler çalıştırdığınızda oluşur. Öznitelik akışları eşitleme kurallarında tanımlanır. Bunlar, gelen (yukarıdaki hello resimdeki ISR) veya giden (yukarıdaki hello resimdeki OSR) olabilir.

## <a name="connected-system"></a>Bağlı sistem
Bağlantılı sistem (diğer adıyla bağlı dizin) toohello uzak sistem Azure başvuran AD Connect eşitleme bağlı tooand okuma ve gelen kimlik veri tooand yazma.

## <a name="connector-space"></a>Bağlayıcı alanı
Her bağlı veri kaynağı hello nesneler ve özniteliklerin hello bağlayıcı alana filtre uygulanmış bir alt olarak temsil edilir.
Bu hello eşitleme hizmeti toooperate hello gerek toocontact hello uzak sistem olmadan yerel olarak hello nesneleri eşitlerken verir ve etkileşim tooimports sınırlar ve yalnızca dışa aktarır.

Ardından Hello veri kaynağı ve hello bağlayıcı hello özelliği tooprovide değişikliklerin (delta içeri aktarma) listesini varsa, yalnızca hello son yoklama sonrasındaki değişiklikler döngüsü gibi hello işletimsel verimliliğini artırır önemli ölçüde değiştirilir. Merhaba bağlayıcı alanı hello bağlı veri kaynağı bu hello bağlayıcı zamanlama alır isteyen ve dışarı aktarma tarafından otomatik olarak yayılıyor değişikliklere karşı korunmasını sağlar. Bu eklenen sigorta sınama, Önizleme veya hello sonraki güncelleştirme onaylama sırasında içiniz rahat verir.

## <a name="metaverse"></a>Meta veri deposu
Merhaba meta veri deposu, bağlayıcı alanları komşu gelen tüm birleştirilmiş kimlikleri, birleştirilmiş hello görünümüdür.

Kimlikleri birbirine bağlı ve yetkilisi alma akışı eşlemeleri aracılığıyla çeşitli öznitelikler için atanan hello merkezi meta veri deposu nesnesine birden çok sistemlerden tooaggregate bilgi başlar. Bu nesne öznitelik akışı eşlemeleri bilgi toooutbound sistemleri uygulayın.

Yetkili bir sistem bunları hello meta veri deposuna projeleri nesneleri oluşturulur. Tüm bağlantılar kaldırılır hemen hello meta veri deposu Nesne silindi.

Merhaba meta veri deposu nesneleri doğrudan düzenlenemez. Merhaba nesnesindeki tüm verilerin öznitelik akışı katkıda bulunan gerekir. Merhaba meta veri deposu her bağlayıcı alanı ile kalıcı bağlayıcılar tutar. Bu bağlayıcıların yeniden değerlendirme çalıştırmak için her eşitleme gerektirmez. Başka bir deyişle, Azure AD Connect eşitleme her zaman toolocate hello eşleşen uzak nesne yok. Bu normalde hello nesneleri ilişkilendirme için sorumlu olacaktır maliyetli aracıları tooprevent değişiklikleri tooattributes hello gereksinimini önler.

Ne zaman toobe yönetilen, Azure AD Connect eşitleme kullanır gereken önceden var olan nesneleri bir işlem olabilir yeni veri kaynaklarını bulma birleşim bir kural tooevaluate olası adaylar hangi tooestablish ile bir bağlantı denir.
Merhaba bağlantı kurulduktan sonra bu değerlendirmeyi yeniden değil ve normal öznitelik akışı hello uzaktan bağlı veri kaynağı ve hello meta veri deposu gerçekleştirilebilir.

## <a name="provisioning"></a>Sağlama
Bir yetkili kaynağı projeleri zaman hello meta veri deposu yeni bir bağlayıcı alanı nesne yeni bir nesneye bir aşağı akış bağlı veri kaynağı temsil eden başka bir bağlayıcı oluşturulabilir.

Bu kendiliğinden bir bağlantı kurar ve öznitelik akışı çift yönlü devam edebilirsiniz.

Bir kural, yeni bir bağlayıcı alanı nesne oluşturulan toobe gerektiğini belirler her sağlama denir. Bu işlem daha yalnızca hello bağlayıcı alanı içinde yer aldığından verme gerçekleştirilene kadar ancak onu hello bağlı veri kaynağına taşımaz.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Azure AD Connect eşitleme: Eşitleme seçeneklerini özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
