---
title: "Linux sanal makineleri Azure üzerinde ilkeleriyle aaaEnforce güvenlik | Microsoft Docs"
description: "Nasıl tooapply İlkesi tooan Azure Resource Manager Linux sanal makine"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a>İlkeleri tooLinux VM'ler Azure Resource Manager ile uygulama
İlkeleri kullanarak, bir kuruluşun çeşitli kuralları ve kuralları hello kuruluş genelinde zorunlu kılabilir. İstenen hello davranış zorlama hello kuruluş toohello başarısını katkıda bulunan sırasında risk azaltılmasına yardımcı olur. Bu makalede, Azure Resource Manager ilkeleri toodefine istenen hello davranışı, kuruluşunuzun sanal makineler için nasıl kullanabileceğiniz açıklanır.

Bir giriş toopolicies için bkz: [kullanım ilkesi toomanage kaynakları ve erişimi denetleme](../../azure-resource-manager/resource-manager-policy.md).

## <a name="permitted-virtual-machines"></a>İzin verilen sanal makineler
sanal makineler, kuruluşunuz için bir uygulama ile uyumlu olduğunu tooensure izin işletim sistemleri hello kısıtlayabilirsiniz. Aşağıdaki ilke örneğine hello yalnızca Ubuntu 14.04.2-LTS sanal makineler izin toobe oluşturuldu.

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
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

Herhangi bir Ubuntu LTS görüntü İlkesi tooallow önceki bir joker karakter toomodify hello kullan: 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

İlke alanlarını hakkında daha fazla bilgi için bkz: [İlkesi diğer adlar](../../azure-resource-manager/resource-manager-policy.md#aliases).

## <a name="managed-disks"></a>Yönetilen diskler

toorequire hello kullanımı yönetilen diskler, ilke aşağıdaki kullanım hello:

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a>Sanal makineler için görüntüleri

Güvenlik nedenleriyle, yalnızca onaylanan özel resimler ortamınızda dağıtılan gerektirebilir. Onaylanan hello görüntüleri içeren hello kaynak grubu ya da hello belirli onayladığı yansımaları belirtebilirsiniz.

Aşağıdaki örnek hello onaylanan kaynak grubu görüntülerden gerektirir:

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

Merhaba aşağıdaki örnek onaylanmış hello resim kimlikleri belirtir:

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a>Sanal makine uzantıları

Belirli türde bir uzantıları kullanımını tooforbid isteyebilirsiniz. Örneğin, bir uzantı belirli özel bir sanal makine görüntüleri ile uyumlu olmayabilir. örnekte gösterildiği nasıl aşağıdaki hello tooblock belirli bir uzantıya. Yayımcı ve türüne toodetermine hangi uzantısı tooblock kullanır.

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a>Sonraki adımlar
* (Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın. Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir. Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](../../azure-resource-manager/resource-manager-policy-portal.md). REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](../../azure-resource-manager/resource-manager-policy-create-assign.md).
* Bir giriş tooresource ilkeleri için bkz: [kaynak ilkesine genel bakış](../../azure-resource-manager/resource-manager-policy.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](../../azure-resource-manager/resource-manager-subscription-governance.md).
