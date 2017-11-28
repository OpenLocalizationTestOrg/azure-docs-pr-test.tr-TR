---
title: "adlandırma kuralları için aaaAzure kaynak ilkeleri | Microsoft Docs"
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
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="e5925-103">Kaynak adları ve metin için geçerlidir</span><span class="sxs-lookup"><span data-stu-id="e5925-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="e5925-104">Bu konu çeşitli gösterir [kaynak ilkeleri](resource-manager-policy.md) tooestablish adlandırma ve metin kuralları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5925-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="e5925-105">Bu ilkeler kaynak adları ve etiket değerleri için tutarlılık emin olun.</span><span class="sxs-lookup"><span data-stu-id="e5925-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="e5925-106">Joker karakter ile adlandırma kuralı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="e5925-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="e5925-107">Merhaba aşağıdaki örnek gösterir hello tarafından desteklenen joker hello kullanımını **gibi** koşulu.</span><span class="sxs-lookup"><span data-stu-id="e5925-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="e5925-108">Merhaba koşul hello varsa ad hello belirtilen desenle eşleşen belirtir (namePrefix\*nameSuffix) hello isteği reddedecek:</span><span class="sxs-lookup"><span data-stu-id="e5925-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="e5925-109">Desen ile adlandırma kuralı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="e5925-109">Set naming convention with pattern</span></span>

<span data-ttu-id="e5925-110">kaynak adları kullanım hello bir desen eşleşmesini toospecify koşul eşleşir.</span><span class="sxs-lookup"><span data-stu-id="e5925-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="e5925-111">Merhaba aşağıdaki örnek gerektirir adları toostart ile `contoso` ve altı ek harf içermelidir:</span><span class="sxs-lookup"><span data-stu-id="e5925-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="e5925-112">Etiket değeri için tarih deseni ayarlayın</span><span class="sxs-lookup"><span data-stu-id="e5925-112">Set date pattern for tag value</span></span>

<span data-ttu-id="e5925-113">toorequire tarih düzeni iki basamak, tire, üç harf, tire ve dört basamak kullanımı:</span><span class="sxs-lookup"><span data-stu-id="e5925-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e5925-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5925-114">Next steps</span></span>
* <span data-ttu-id="e5925-115">(Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="e5925-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="e5925-116">Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="e5925-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="e5925-117">Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5925-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="e5925-118">REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="e5925-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="e5925-119">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e5925-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

