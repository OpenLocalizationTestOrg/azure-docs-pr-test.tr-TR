---
title: "aaaHow tooconfigure güvenlik uyarıları | Microsoft Docs"
description: "Azure Privileged Identity Management uzantısı için nasıl tooconfigure güvenlik uyarıları hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management nasıl tooconfigure güvenlik uyarıları
## <a name="security-alerts"></a>Güvenlik uyarıları
Azure Privileged Identity Management (PIM) ortamınızda kuşkulu veya güvenli olmayan etkinliği olduğunda uyarı verir. Bir uyarı tetiklendiğinde hello PIM Panoda görüntülersiniz. Merhaba uyarı toosee listeleri kullanıcılar ya da hello uyarının roller hello bir rapor seçin.

![PIM Pano güvenlik uyarıları - ekran görüntüsü][1]

| Uyarı | Tetikleyici | Öneri |
| --- | --- | --- |
| **Roller PIM dışında atanmış durumda** |Yönetici kalıcı olarak hello PIM arabirimi dışında tooa rolü atandı. |Merhaba yeni rol ataması gözden geçirin. Diğer hizmetler yalnızca kalıcı Yöneticiler atayabilirsiniz olduğundan, gerekirse tooan uygun atama değiştirin. |
| **Roller çok sık etkinleştirilmekte** |Hello süre içinde aynı rol hello Ayarları'nda izin verilen Merhaba, çok fazla yeniden etkinleştirmeleri vardı. |Bunlar çok fazla kez hello rol neden etkinleştirdikten hello kullanıcı toosee başvurun. Sınır kendileri için çok kısa belki hello zaman görevlerini veya belki de bunlar kullanmakta olduğunuz toocomplete tooautomatically komutlar bir rolünü etkinleştirin. |
| **Rol etkinleştirmesi için çok faktörlü kimlik doğrulaması gerektirmeyen** |Merhaba ayarlarında etkinleştirilmiş MFA olmadan rolü vardır. |Biz hello en yüksek ayrıcalıklı rolleri için MFA gerekir, ancak tüm rolleri etkinleştirme için MFA etkinleştirin kesinlikle öneririz. |
| **Yöneticiler ayrıcalıklı rollerini kullanmadığınız** |Rollerine son etkinleştirmediyseniz uygun Yöneticiler vardır. |Erişim artık ihtiyacınız bir erişim gözden geçirme toodetermine hello kullanıcıları başlatın. |
| **Çok sayıda genel Yöneticiler vardır** |Önerilen daha fazla genel Yöneticiler vardır. |Çok sayıda genel Yöneticiler varsa, kullanıcıların ihtiyaç duyduklarından fazla izinler aldıklarından olasıdır. Taşıma kullanıcılar tooless ayrıcalıklı rolleri ya da bunlardan bazıları kalıcı olarak atanan yerine hello rolü için uygun hale getirmek. |

## <a name="configure-security-alert-settings"></a>Güvenlik uyarı ayarlarını yapılandırma
PIM toowork ortamı ve güvenlik hedeflerinizle hello güvenlik uyarıları bazıları özelleştirebilirsiniz. Bu adımları tooreach hello ayarları dikey izleyin:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve select hello **Azure AD Privileged Identity Management** döşeme hello panodan.
2. Seçin **yönetilen ayrıcalıklı rolleri** > **ayarları** > **uyarıları ayarları**.
   
    ![Toosecurity uyarı ayarlarını gidin][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>"Rolleri çok sık etkinleştirilmekte" Uyarısı
Bir kullanıcı etkinleştirir, Tetikleyicileri birden çok kez belirli bir süre içinde aynı ayrıcalıklı rolün hello bu uyarı. Her iki hello zaman dönemi ve hello etkinleştirme sayısını yapılandırabilirsiniz.

* **Etkinleştirme yenileme zaman çerçevesi**: gün, saat, dakika belirtin ve ikinci hello zaman dönemi toouse tootrack şüpheli yenilemeleri istiyorsanız.
* **Etkinleştirme yenilemesi sayısı**: seçtiğiniz hello zaman çerçevesi içinde uyarı worthy dikkate 2 too100 gelen etkinleştirme hello sayısını belirtin. Bu ayar taşıma hello kaydırıcı tarafından veya bir sayı hello metin kutusuna yazarak değiştirebilirsiniz.

### <a name="there-are-too-many-global-administrators-alert"></a>"Çok sayıda genel Yöneticiler bulunur" Uyarısı
PIM bu uyarı, iki farklı ölçütler karşılanıyorsa ve bunların her ikisi de yapılandırabilirsiniz tetikler. İlk olarak, tooreach genel yöneticiler belirli bir eşiği gerekir. İkinci olarak, belirli bir yüzdesi toplam rol atamalarınızı genel yönetici olması gerekir. Yalnızca bu ölçümleri birini karşılamıyorsa, hello uyarısı görünmez.  

* **Genel yöneticiler en az sayıda**: Genel yöneticileri, bir güvenli miktarını göz önünde bulundurun 2 too100 hello sayısını belirtin.
* **Genel yönetici oranı**: % 0'dan genel Yöneticiler yöneticilerine hello yüzdesini belirtin, ortamınızda güvenli değildir too100%.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>"Yöneticiler ayrıcalıklı rollerini kullanmadığınız" Uyarısı
Bir kullanıcı bir rolünü etkinleştirmeden belirli bir süre kalırsa bu uyarı tetikler.

* **Gün sayısı**: Merhaba, bir kullanıcı bir rolünü etkinleştirmeden gidebilirsiniz 0 too100 itibaren gün sayısını belirtin.

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
