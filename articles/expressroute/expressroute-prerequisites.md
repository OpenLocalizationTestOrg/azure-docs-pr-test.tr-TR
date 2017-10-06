---
title: "Azure ExpressRoute benimseme için aaaPrerequisites | Microsoft Docs"
description: "Bu sayfa bir Azure expressroute bağlantı hattı sipariş etmeden önce karşılanır gereksinimleri toobe listesini sağlar."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>ExpressRoute önkoşulları ve denetim listesi
ExpressRoute kullanarak hizmetlerini hello aşağıdaki bölümlerde listelenen gereksinimleri aşağıdaki o hello tooverify gerek tooconnect tooMicrosoft bulut karşılandığından.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Azure hesabı
* Geçerli ve etkin bir Microsoft Azure hesabı. Merhaba expressroute bağlantı hattı kurmak gerekli tooset hesabıdır. ExpressRoute bağlantı hatları Azure aboneliklerinin içindeki kaynaklardır. Bağlantı sınırlı toonon Azure gibi Microsoft bulut Hizmetleri, Office 365 hizmetlerinizi ve Dynamics 365 olsa bile bir Azure aboneliği bir gereksinimdir.
* Etkin bir Office 365 aboneliği (Office 365 hizmetlerini kullanıyorsanız) Daha fazla bilgi için bkz: Merhaba [Office 365 için belli gereksinimler](#office-365-specific-requirements) bu makalenin.

## <a name="connectivity-provider"></a>Bağlantı sağlayıcısı

* Çalışabileceğiniz bir [ExpressRoute bağlantı ortağı](expressroute-locations.md#partners) tooconnect toohello Microsoft bulut. Şirket içi ağınız ve Microsoft arasında bağlantıyı [üç şekilde](expressroute-introduction.md) kurabilirsiniz.
* Sağlayıcınız ExpressRoute bağlantı ortağı değilse, toohello Microsoft bulut üzerinden hala bağlanabilir bir [bulut değişim sağlayıcısı](expressroute-locations.md#connectivity-through-exchange-providers).

## <a name="network-requirements"></a>Ağ gereksinimleri
* **Yedekli bağlantı**: Siz ve sağlayıcınız arasında fiziksel bağlantıda yedekleme gereksinimi yoktur. Microsoft, yalnızca olsa bile Microsoft'un yönlendiriciler ve hello eşleme yönlendiricileri arasında ayarlanmış yedekli BGP oturumlarının toobe gerektiren [bir fiziksel ağ bağlantısı tooa bulut değişimine](expressroute-faqs.md#onep2plink).
* **Yönlendirme**: toohello Microsoft Cloud connect nasıl bağlı olarak siz veya sağlayıcınız yukarı tooset gerekir ve hello BGP oturumlarının yönetmek [Yönlendirme etki alanları](expressroute-circuit-peerings.md). Bazı Ethernet bağlantı sunucuları veya bulut değişim sunucuları değer ekleme hizmeti olarak BGP yönetimi sunabilir.
* **NAT**: Microsoft genel IP adreslerini sadece Microsoft eşleme yoluyla kabul eder. Şirket içi ağınızda özel IP adresleri kullanıyorsanız, siz veya sağlayıcı gerek tootranslate hello özel IP toohello ortak IP adreslerine [hello NAT kullanarak](expressroute-nat.md).
* **QoS**: Skype Kurumsal’da farklı QoS davranışları gerektiren çeşitli hizmetler (ör. ses, video, mesaj) vardır. Siz ve sağlayıcınız hello izlemeniz gereken [QoS gereksinimleri](expressroute-qos.md).
* **Ağ güvenliği**: göz önünde bulundurun [ağ güvenliği](../best-practices-network-security.md) toohello ExpressRoute aracılığıyla Microsoft Cloud bağlanırken.

## <a name="office-365"></a>Office 365
Expressroute bağlantı hattı üzerinde tooenable Office 365 planlıyorsanız, belgeleri Office 365 gereksinimleri hakkında daha fazla bilgi için aşağıdaki hello gözden geçirin.

* [Office 365 için ExpressRoute’a Genel Bakış](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Office 365 için ExpressRoute ile Yönlendirme](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Office 365 URL’leri ve IP adresi aralıkları](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Office 365 için ağ planlama ve performans ayarı](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [Ağ bant genişliği hesaplayıcıları ve araçları](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [Office 365’i şirket içi ortamlarla tümleştirme](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Office 365'te ExpressRoute ileri düzey eğitim videoları](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
Expressroute bağlantı hattı üzerinde tooenable Dynamics 365 planlıyorsanız, belgeler Dynamics 365 hakkında daha fazla bilgi için aşağıdaki hello gözden geçirin

* [Dynamics 365 ve ExpressRoute teknik incelemesi](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [Dynamics 365 URL'leri](https://support.microsoft.com/kb/2655102) ve [IP adresi aralıkları](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>Sonraki adımlar
* ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).
* ExpressRoute bağlantı sağlayıcısı bulun. Bkz. [ExpressRoute ortakları ve eşleme konumları](expressroute-locations.md).
* Başvurmak için toorequirements [yönlendirme](expressroute-routing.md), [NAT](expressroute-nat.md), ve [QoS](expressroute-qos.md).
* ExpressRoute bağlantınızı yapılandırın.
  * [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md)
  * [Yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md)
  * [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md)
