---
title: "ExpressRoute bağlantı modelleri: tooMicrosoft Azure ağ hizmet sağlayıcılarının, alışverişleri ve Ethernet sağlayıcıları bağlanma | Microsoft Docs"
description: "Bu makalede hello Müşteri'nin ağ ve Microsoft Azure, Office 365 ve Dynamics 365 hizmetleri arasında bağlantı hello farklı modları açıklanır. Müşteriler MPLS sağlayıcılarını, bulut değişimlerini ve Ethernet sağlayıcılarını kullanabilir."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: cherylmc
ms.openlocfilehash: 2682e6e45b2892869068f132bedb4bb08e3f89a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-connectivity-models"></a>ExpressRoute bağlantı modelleri
Bağlantı şirket içi ağınız ve hello Microsoft Bulutu arasında üç farklı yolla oluşturabilirsiniz [CloudExchange birlikte bulundurma](#CloudExchange), [noktadan noktaya Ethernet bağlantısı](#Ethernet)ve [Herhangi herhangi bir (IPVPN) bağlantı](#IPVPN). Bağlantı sağlayıcıları bir veya daha fazla bağlantı modeli sunabilir. En uygun bağlantı sağlayıcısı toopick hello modelde çalışabilirsiniz.
<br><br>

![ExpressRoute bağlantı modeli diyagramı](./media/expressroute-connectivity-models/expressroute-connectivity-models-diagram.png)

## <a name="CloudExchange"></a>Bulut değişiminde ortak yerleşim
Bir bulut değişimine sahip bir tesiste ortak yerleşime sahipseniz, Microsoft bulut hello ortak yerleşim sağlayıcının Ethernet değişimi üzerinden sanal çapraz bağlantıları toohello sıralayabilirsiniz. Ortak yerleşim sağlayıcıları, Katman 2 çapraz bağlantıları veya yönetilen Katman 3 çapraz bağlantılarını altyapınızda hello ortak yerleşim tesisi ve hello Microsoft Bulutu arasında sunabilir.

## <a name="Ethernet"></a>Noktadan noktaya Ethernet bağlantıları
Noktadan noktaya Ethernet bağlantıları şirket içi veri merkezleri/ofisleri toohello Microsoft Bulut'a bağlanabilirsiniz. Noktadan noktaya Ethernet sağlayıcıları Katman 2 bağlantıları sağlayabilir veya site hello Microsoft cloud arasındaki Katman 3 bağlantılarını yönetiliyor.

## <a name="IPVPN"></a>Herhangi bir ağdan herhangi bir (IPVPN) ağa
WAN'ınız hello Microsoft Bulutu ile tümleştirebilirsiniz. IPVPN sağlayıcıları (genellikle MPLS VPN) şubeleriniz ve veri merkezleriniz arasında herhangi bir yerden herhangi bir yere bağlantı sunabilir. Hello Microsoft bulut Ara yalnızca birbirine tooyour WAN toomake olabilir, diğer bir şube ofisi ister. WAN sağlayıcıları genel olarak yönetilen Katman 3 bağlantısı sağlar. ExpressRoute yetenekleri ve özellikleri tüm bağlantı modelleri yukarıda hello aynıdır. 

## <a name="next-steps"></a>Sonraki adımlar
* ExpressRoute bağlantıları ve yönlendirme etki alanları hakkında bilgi edinin. Bkz. [ExpressRoute bağlantı hatları ve etki alanlarını yönlendirme](expressroute-circuit-peerings.md).
* ExpressRoute özellikleri hakkında bilgi alın. Merhaba bkz [ExpressRoute teknik genel bakış](expressroute-introduction.md)
* Bir hizmet sağlayıcı bulun. Bkz. [ExpressRoute ortakları ve eşleme konumları](expressroute-locations.md).
* Tüm önkoşulların sağlandığından emin olun. Bkz. [ExpressRoute önkoşulları](expressroute-prerequisites.md).
* Toohello gereksinimleri başvuran [yönlendirme](expressroute-routing.md), [NAT](expressroute-nat.md), ve [QoS](expressroute-qos.md).
* ExpressRoute bağlantınızı yapılandırın.
  * [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md)
  * [Yönlendirmeyi yapılandırma](expressroute-howto-routing-portal-resource-manager.md)
  * [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-portal-resource-manager.md)
