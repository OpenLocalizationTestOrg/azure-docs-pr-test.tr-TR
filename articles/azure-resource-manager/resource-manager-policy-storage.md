---
title: "Depolama hesapları için Azure kaynak ilkeleri | Microsoft Docs"
description: "Depolama hesapları dağıtımını yönetmek için Azure Resource Manager ilkelerini açıklar."
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
ms.openlocfilehash: 6612ee61f5c50e743241b92030660cea7ae7094d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-to-storage-accounts"></a><span data-ttu-id="717a9-103">Depolama hesapları için kaynak ilkelerini uygula</span><span class="sxs-lookup"><span data-stu-id="717a9-103">Apply resource policies to storage accounts</span></span>
<span data-ttu-id="717a9-104">Bu konu çeşitli gösterir [kaynak ilkeleri](resource-manager-policy.md) Azure depolama hesapları için geçerli olabilir.</span><span class="sxs-lookup"><span data-stu-id="717a9-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to Azure storage accounts.</span></span> <span data-ttu-id="717a9-105">Bu ilkeler kuruluşunuza dağıtmış depolama hesapları için tutarlılık emin olun.</span><span class="sxs-lookup"><span data-stu-id="717a9-105">These policies ensure consistency for the storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="717a9-106">İzin verilen depolama hesabı türlerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="717a9-106">Define permitted storage account types</span></span>

<span data-ttu-id="717a9-107">Aşağıdaki ilke hangi kısıtlayan [depolama hesabı türlerini](../storage/common/storage-redundancy.md) dağıtılabilir:</span><span class="sxs-lookup"><span data-stu-id="717a9-107">The following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
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

<span data-ttu-id="717a9-108">İzin verilen SKU'lar kabul etmek için bir parametre ile benzer bir ilke kuralı, bir yerleşik ilke tanımı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="717a9-108">A similar policy rule with a parameter for accepting the allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="717a9-109">Kaynak Kimliği yerleşik ilkesine sahip `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="717a9-109">The built-in policy has the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="717a9-110">İzin verilen erişim katmanı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="717a9-110">Define permitted access tier</span></span>

<span data-ttu-id="717a9-111">Aşağıdaki ilke türünü belirtir. [erişim katmanı](../storage/blobs/storage-blob-storage-tiers.md) depolama hesapları için belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="717a9-111">The following policy specifies the type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="717a9-112">Şifreleme etkin olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="717a9-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="717a9-113">Tüm depolama hesaplarını etkinleştirmek için aşağıdaki ilke gerektiriyorsa [depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="717a9-113">The following policy requires all storage accounts to enable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="717a9-114">Bu ilke kuralı olarak da kaynak kimliği yerleşik ilke tanımı kullanılabilir `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="717a9-114">This policy rule is also available as a built-in policy definition with the resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="717a9-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="717a9-115">Next steps</span></span>
* <span data-ttu-id="717a9-116">(Yukarıdaki örneklerde gösterildiği gibi) bir ilke kuralı tanımladıktan sonra ilke tanımı oluşturun ve bir kapsama atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="717a9-116">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="717a9-117">Kapsamı bir abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="717a9-117">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="717a9-118">Portal üzerinden ilkeler atamak için bkz: [atamak ve kaynak ilkelerini yönetmek için kullanım Azure portal](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="717a9-118">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="717a9-119">REST API'si, PowerShell veya Azure CLI aracılığıyla ilkeleri atamak için bkz: [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="717a9-119">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="717a9-120">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="717a9-120">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

