---
title: "Ağ kaynakları için Azure kaynak ilkelerini | Microsoft Docs"
description: "Ağ kaynakları dağıtımını yönetmek için Azure Resource Manager ilkelerini açıklar."
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
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="7693d-103">Kaynak ilkeleri, ağ kaynaklarına uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7693d-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="7693d-104">Bu makalede bir örnek gösterilmektedir [kaynak İlkesi](resource-manager-policy.md) Azure sanal ağ geçitlerine uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7693d-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="7693d-105">Bu ilke, kuruluşunuza dağıtmış ağ geçitleri için tutarlı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7693d-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="7693d-106">İzin verilen sanal ağ geçidi SKU'su tanımlayın</span><span class="sxs-lookup"><span data-stu-id="7693d-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="7693d-107">Aşağıdaki ilke hangi SKU'ları sanal ağ geçitleri için dağıtılabilir kısıtlar:</span><span class="sxs-lookup"><span data-stu-id="7693d-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7693d-108">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7693d-108">Next steps</span></span>
* <span data-ttu-id="7693d-109">(Yukarıdaki örneklerde gösterildiği gibi) bir ilke kuralı tanımladıktan sonra ilke tanımı oluşturun ve bir kapsama atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7693d-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="7693d-110">Kapsamı bir abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="7693d-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="7693d-111">Portal üzerinden ilkeler atamak için bkz: [atamak ve kaynak ilkelerini yönetmek için kullanım Azure portal](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7693d-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="7693d-112">REST API'si, PowerShell veya Azure CLI aracılığıyla ilkeleri atamak için bkz: [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="7693d-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="7693d-113">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="7693d-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

