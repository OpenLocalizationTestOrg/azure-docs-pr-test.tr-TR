---
title: "aaaQoS ExpressRoute için gereksinimleri | Microsoft Docs"
description: "Bu sayfada, ExpressRoute bağlantı hatları için hizmet kalitesini (QoS) yapılandırma ve yönetmeye yönelik ayrıntılı gereksinimler sağlanmıştır."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a>ExpressRoute QoS gereksinimleri
Skype Kurumsal’da farklı QoS davranışları gerektiren çeşitli iş yükleri vardır. ExpressRoute aracılığıyla ses Hizmetleri tooconsume planlıyorsanız, aşağıda açıklanan toohello gereksinimlere uymanız gerekir.

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> QoS gereksinimleri yalnızca Microsoft toohello eşlemesi geçerlidir. Azure ortak eşleme ve Azure özel eşleme alınan, ağ trafiğinin Hello DSCP değerlerini sıfırlama too0 olacaktır. 
> 
> 

Merhaba aşağıdaki tabloda işletmeler için Skype tarafından kullanılan DSCP işaretlerinin bir listesini sağlar. Çok başvuran[Skype Kurumsal için Qos'i yönetme](https://technet.microsoft.com/library/gg405409.aspx) daha fazla bilgi için.

| **Trafik Sınıfı** | **İşleme (DSCP İşaretleme)** | **Skype Kurumsal İş Yükleri** |
| --- | --- | --- |
| **Ses** |EF (46) |Skype / Lync ses |
| **Etkileşimli** |AF41 (34) |Video, VBSS |
| AF21 (18) |Uygulama paylaşımı | |
| **Varsayılan** |AF11 (10) |Dosya aktarımı |
| CS0 (0) |Diğer | |

* Merhaba iş yükleri sınıflandırmanız ve hello doğru DSCP değerlerini işaretlemeniz gerekir. Sağlanan hello yönergeleri izlemelidir [burada](https://technet.microsoft.com/library/gg405409.aspx) nasıl ağınızda DSCP işaretlerini tooset.
* Ağınızda çoklu QoS kuyruklarını yapılandırmanız ve desteklemeniz gerekir. Ses, tek başına bir sınıf olması ve ses için RFC 3246 içinde belirtilen hello EF işlemi uygulanmalıdır. 
* Mekanizması, sıkışma algılama İlkesi ve trafik sınıfı başına bant genişliği ayırma queuing hello karar verebilirsiniz. Ancak, hello DSCP Skype kurumsal iş yükleri için işaretleme korunmalıdır. Yukarıda listelenmeyen DSCP işaretlerini kullanıyorsanız AF31 (26) yeniden yazılması gerekir bu DSCP değeri too0 hello paket tooMicrosoft göndermeden önce. Microsoft, yalnızca hello hello yukarıdaki tabloda gösterilen DSCP değeri ile işaretlenen paketleri gönderir. 

## <a name="next-steps"></a>Sonraki adımlar
* Toohello gereksinimleri başvuran [yönlendirme](expressroute-routing.md) ve [NAT](expressroute-nat.md).
* ExpressRoute bağlantınızı tooconfigure Hello aşağıdaki bağlantılar bakın.
  
  * [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md)
  * [Yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md)
  * [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md)

