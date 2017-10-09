---
title: "ağ kaynakları için aaaAzure kaynak ilkeleri | Microsoft Docs"
description: "Ağ kaynakları hello dağıtımını yönetmek için Azure Resource Manager ilkelerini açıklar."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a>Kaynak ilkeleri toonetwork kaynakları Uygula
Bu makalede bir örnek gösterilmektedir [kaynak İlkesi](resource-manager-policy.md) tooAzure sanal ağ geçitlerini uygulayabilirsiniz. Bu ilke, kuruluşunuza dağıtmış ağ geçitleri için tutarlı olmasını sağlar. 

## <a name="define-permitted-virtual-network-gateway-sku"></a>İzin verilen sanal ağ geçidi SKU'su tanımlayın

sanal ağ geçitleri için hangi SKU'ları dağıtılabilir ilke aşağıdaki hello kısıtlar:

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Sonraki adımlar
* (Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın. Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir. Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md). REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md). 
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

