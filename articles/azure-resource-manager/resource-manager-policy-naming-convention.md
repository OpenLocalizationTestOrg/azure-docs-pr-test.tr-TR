---
title: "Adlandırma kuralları için Azure kaynak ilkeleri | Microsoft Docs"
description: "Kaynak adlandırma kuralları için Azure Resource Manager ilkelerini açıklar."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="95f66-103">Kaynak adları ve metin için geçerlidir</span><span class="sxs-lookup"><span data-stu-id="95f66-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="95f66-104">Bu konu çeşitli gösterir [kaynak ilkeleri](resource-manager-policy.md) adlandırma ve metin kuralları oluşturmak için geçerli olabilir.</span><span class="sxs-lookup"><span data-stu-id="95f66-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="95f66-105">Bu ilkeler kaynak adları ve etiket değerleri için tutarlılık emin olun.</span><span class="sxs-lookup"><span data-stu-id="95f66-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="95f66-106">Joker karakter ile adlandırma kuralı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="95f66-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="95f66-107">Aşağıdaki örnek tarafından desteklenen joker karakter kullanımı gösterilmiştir **gibi** koşulu.</span><span class="sxs-lookup"><span data-stu-id="95f66-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="95f66-108">Adı belirtilen desen eşleşirse bildiren koşul (namePrefix\*nameSuffix) isteği reddeder:</span><span class="sxs-lookup"><span data-stu-id="95f66-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="95f66-109">Desen ile adlandırma kuralı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="95f66-109">Set naming convention with pattern</span></span>

<span data-ttu-id="95f66-110">Kaynak adları bir desenle eşleşen belirtmek için eşleşme koşul kullanın.</span><span class="sxs-lookup"><span data-stu-id="95f66-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="95f66-111">Aşağıdaki örnek adları başlamak gerektirir `contoso` ve altı ek harf içermelidir:</span><span class="sxs-lookup"><span data-stu-id="95f66-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="95f66-112">Etiket değeri için tarih deseni ayarlayın</span><span class="sxs-lookup"><span data-stu-id="95f66-112">Set date pattern for tag value</span></span>

<span data-ttu-id="95f66-113">İki basamaklı, tire, üç harf, tire ve dört basamak kullanım tarihi düzeni istemek için:</span><span class="sxs-lookup"><span data-stu-id="95f66-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="95f66-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95f66-114">Next steps</span></span>
* <span data-ttu-id="95f66-115">(Yukarıdaki örneklerde gösterildiği gibi) bir ilke kuralı tanımladıktan sonra ilke tanımı oluşturun ve bir kapsama atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="95f66-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="95f66-116">Kapsamı bir abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="95f66-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="95f66-117">Portal üzerinden ilkeler atamak için bkz: [atamak ve kaynak ilkelerini yönetmek için kullanım Azure portal](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95f66-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="95f66-118">REST API'si, PowerShell veya Azure CLI aracılığıyla ilkeleri atamak için bkz: [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="95f66-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="95f66-119">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="95f66-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

