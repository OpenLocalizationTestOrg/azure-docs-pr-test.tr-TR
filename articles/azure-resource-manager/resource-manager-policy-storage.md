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
# <a name="apply-resource-policies-toostorage-accounts"></a>Kaynak ilkeleri toostorage hesapları Uygula
Bu konu çeşitli gösterir [kaynak ilkeleri](resource-manager-policy.md) tooAzure depolama hesapları uygulayabilirsiniz. Bu ilkeler kuruluşunuza dağıtmış hello depolama hesapları için tutarlılık emin olun. 

## <a name="define-permitted-storage-account-types"></a>İzin verilen depolama hesabı türlerini tanımlayın

Merhaba aşağıdaki ilke hangi kısıtlayan [depolama hesabı türlerini](../storage/common/storage-redundancy.md) dağıtılabilir:

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

SKU'ları izin hello kabul etmek için bir parametre ile benzer bir ilke kuralı, bir yerleşik ilke tanımı kullanılabilir. Merhaba yerleşik ilkesine sahip hello kaynak Kimliğini `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>İzin verilen erişim katmanı tanımlayın

Merhaba aşağıdaki ilke hello türünü belirtir [erişim katmanı](../storage/blobs/storage-blob-storage-tiers.md) depolama hesapları için belirtilebilir:

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

## <a name="ensure-encryption-is-enabled"></a>Şifreleme etkin olduğundan emin olun

Merhaba aşağıdaki ilke gerektiren tüm depolama hesapları tooenable [depolama hizmeti şifrelemesi](../storage/common/storage-service-encryption.md):

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

Bu ilke kuralı olarak da hello kaynak kimliği olan yerleşik ilke tanımı kullanılabilir `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Sonraki adımlar
* (Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın. Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir. Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](resource-manager-policy-portal.md). REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](resource-manager-policy-create-assign.md). 
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).

