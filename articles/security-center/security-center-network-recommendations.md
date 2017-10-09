---
title: "aaaProtecting Azure Güvenlik Merkezi, ağınızda | Microsoft Docs"
description: "Yardımcı olacak öneriler Azure Güvenlik Merkezi'nde Azure ağınızı korumak ve güvenlik ilkeleriyle uyumlu olmak bu belge adresleri."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Azure Güvenlik Merkezi, ağınızda koruma
Azure Güvenlik Merkezi hello Azure kaynaklarınızın güvenlik durumunu çözümler. Güvenlik Merkezi olası güvenlik açıklarını belirlediğinde, gerekli hello denetimlerini yapılandırma hello işleminde size kılavuzluk öneriler oluşturur.  Önerileri tooAzure kaynak türleri geçerlidir: sanal ağ, SQL ve uygulamaları makineleri (VM'ler).

Bu makalede tooyour ağ uygulamak önerileri giderir.  Ağ önerileri merkezi İleri nesil güvenlik duvarları, ağ güvenlik grupları, yapılandırma gelen trafiği kuralları ve daha fazla etrafında.  Bir başvuru toohelp olarak kullanımı hello tablo aşağıda hello kullanılabilir ağ önerileri ve onu uygularsanız her birini ne yaptığını anlayın.

## <a name="available-network-recommendations"></a>Kullanılabilir ağ önerileri
| Öneri | Açıklama |
| --- | --- |
| [Yeni Nesil Güvenlik Duvarı ekleme](security-center-add-next-generation-firewall.md) |Güvenlik korumaları bir Microsoft iş ortağı tooincrease İleri nesil Güvenlik Duvarı (NGFW) eklemek önerir. |
| [Trafiği yalnızca NGFW aracılığıyla yönlendirme](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Gelen trafik tooyour, NGFW aracılığıyla VM zorla ağ güvenlik grubu (NSG) kurallarını yapılandırmak önerir. |
| [Ağ güvenlik grupları alt ağları veya sanal makinelerde etkinleştir](security-center-enable-network-security-groups.md) |Nsg'ler alt ağları veya VM'ler etkinleştirmenizi önerir. |
| [Uç nokta Internet'e aracılığıyla erişimi kısıtlama](security-center-restrict-access-through-internet-facing-endpoints.md) |İçin Nsg'ler gelen trafik kurallarını yapılandırmak önerir. |

## <a name="see-also"></a>Ayrıca bkz.
toolearn tooother Azure kaynak türleri bkz hello aşağıdaki öneriler hakkında daha fazla bilgi:

* [Azure Güvenlik Merkezi'nde, sanal makineleri koruma](security-center-virtual-machine-recommendations.md)
* [Uygulamalarınızı Azure Güvenlik Merkezi'nde koruma](security-center-application-recommendations.md)
* [Azure SQL hizmetinizi Azure Güvenlik Merkezi'nde koruma](security-center-sql-service-recommendations.md)

Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
