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
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="e3eeb-103">Kaynak ilkeleri toonetwork kaynakları Uygula</span><span class="sxs-lookup"><span data-stu-id="e3eeb-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="e3eeb-104">Bu makalede bir örnek gösterilmektedir [kaynak İlkesi](resource-manager-policy.md) tooAzure sanal ağ geçitlerini uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3eeb-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="e3eeb-105">Bu ilke, kuruluşunuza dağıtmış ağ geçitleri için tutarlı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3eeb-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="e3eeb-106">İzin verilen sanal ağ geçidi SKU'su tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e3eeb-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="e3eeb-107">sanal ağ geçitleri için hangi SKU'ları dağıtılabilir ilke aşağıdaki hello kısıtlar:</span><span class="sxs-lookup"><span data-stu-id="e3eeb-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e3eeb-108">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3eeb-108">Next steps</span></span>
* <span data-ttu-id="e3eeb-109">(Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="e3eeb-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="e3eeb-110">Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3eeb-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="e3eeb-111">Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e3eeb-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="e3eeb-112">REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="e3eeb-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="e3eeb-113">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e3eeb-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

