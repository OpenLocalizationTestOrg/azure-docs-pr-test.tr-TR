---
title: "Depolama hesapları için aaaAzure kaynak ilkeleri | Microsoft Docs"
description: "Depolama hesapları hello dağıtımını yönetmek için Azure Resource Manager ilkelerini açıklar."
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
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="c051d-103">Kaynak ilkeleri toostorage hesapları Uygula</span><span class="sxs-lookup"><span data-stu-id="c051d-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="c051d-104">Bu konu çeşitli gösterir [kaynak ilkeleri](resource-manager-policy.md) tooAzure depolama hesapları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c051d-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="c051d-105">Bu ilkeler kuruluşunuza dağıtmış hello depolama hesapları için tutarlılık emin olun.</span><span class="sxs-lookup"><span data-stu-id="c051d-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="c051d-106">İzin verilen depolama hesabı türlerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="c051d-106">Define permitted storage account types</span></span>

<span data-ttu-id="c051d-107">Merhaba aşağıdaki ilke hangi kısıtlayan [depolama hesabı türlerini](../storage/common/storage-redundancy.md) dağıtılabilir:</span><span class="sxs-lookup"><span data-stu-id="c051d-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="c051d-108">SKU'ları izin hello kabul etmek için bir parametre ile benzer bir ilke kuralı, bir yerleşik ilke tanımı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c051d-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="c051d-109">Merhaba yerleşik ilkesine sahip hello kaynak Kimliğini `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span><span class="sxs-lookup"><span data-stu-id="c051d-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="c051d-110">İzin verilen erişim katmanı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="c051d-110">Define permitted access tier</span></span>

<span data-ttu-id="c051d-111">Merhaba aşağıdaki ilke hello türünü belirtir [erişim katmanı](../storage/blobs/storage-blob-storage-tiers.md) depolama hesapları için belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="c051d-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="c051d-112">Şifreleme etkin olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="c051d-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="c051d-113">Merhaba aşağıdaki ilke gerektiren tüm depolama hesapları tooenable [depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="c051d-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="c051d-114">Bu ilke kuralı olarak da hello kaynak kimliği olan yerleşik ilke tanımı kullanılabilir `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span><span class="sxs-lookup"><span data-stu-id="c051d-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c051d-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c051d-115">Next steps</span></span>
* <span data-ttu-id="c051d-116">(Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="c051d-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="c051d-117">Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="c051d-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="c051d-118">Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c051d-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="c051d-119">REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="c051d-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="c051d-120">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c051d-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

