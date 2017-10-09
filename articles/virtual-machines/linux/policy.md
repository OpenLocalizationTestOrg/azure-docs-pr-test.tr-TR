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
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a><span data-ttu-id="99fec-103">İlkeleri tooLinux VM'ler Azure Resource Manager ile uygulama</span><span class="sxs-lookup"><span data-stu-id="99fec-103">Apply policies tooLinux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="99fec-104">İlkeleri kullanarak, bir kuruluşun çeşitli kuralları ve kuralları hello kuruluş genelinde zorunlu kılabilir.</span><span class="sxs-lookup"><span data-stu-id="99fec-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="99fec-105">İstenen hello davranış zorlama hello kuruluş toohello başarısını katkıda bulunan sırasında risk azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="99fec-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="99fec-106">Bu makalede, Azure Resource Manager ilkeleri toodefine istenen hello davranışı, kuruluşunuzun sanal makineler için nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="99fec-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="99fec-107">Bir giriş toopolicies için bkz: [kullanım ilkesi toomanage kaynakları ve erişimi denetleme](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="99fec-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="99fec-108">İzin verilen sanal makineler</span><span class="sxs-lookup"><span data-stu-id="99fec-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="99fec-109">sanal makineler, kuruluşunuz için bir uygulama ile uyumlu olduğunu tooensure izin işletim sistemleri hello kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99fec-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="99fec-110">Aşağıdaki ilke örneğine hello yalnızca Ubuntu 14.04.2-LTS sanal makineler izin toobe oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="99fec-110">In hello following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines toobe created.</span></span>

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

<span data-ttu-id="99fec-111">Herhangi bir Ubuntu LTS görüntü İlkesi tooallow önceki bir joker karakter toomodify hello kullan:</span><span class="sxs-lookup"><span data-stu-id="99fec-111">Use a wild card toomodify hello preceding policy tooallow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="99fec-112">İlke alanlarını hakkında daha fazla bilgi için bkz: [İlkesi diğer adlar](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="99fec-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="99fec-113">Yönetilen diskler</span><span class="sxs-lookup"><span data-stu-id="99fec-113">Managed disks</span></span>

<span data-ttu-id="99fec-114">toorequire hello kullanımı yönetilen diskler, ilke aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="99fec-114">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="99fec-115">Sanal makineler için görüntüleri</span><span class="sxs-lookup"><span data-stu-id="99fec-115">Images for Virtual Machines</span></span>

<span data-ttu-id="99fec-116">Güvenlik nedenleriyle, yalnızca onaylanan özel resimler ortamınızda dağıtılan gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="99fec-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="99fec-117">Onaylanan hello görüntüleri içeren hello kaynak grubu ya da hello belirli onayladığı yansımaları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99fec-117">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="99fec-118">Aşağıdaki örnek hello onaylanan kaynak grubu görüntülerden gerektirir:</span><span class="sxs-lookup"><span data-stu-id="99fec-118">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="99fec-119">Merhaba aşağıdaki örnek onaylanmış hello resim kimlikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="99fec-119">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="99fec-120">Sanal makine uzantıları</span><span class="sxs-lookup"><span data-stu-id="99fec-120">Virtual Machine extensions</span></span>

<span data-ttu-id="99fec-121">Belirli türde bir uzantıları kullanımını tooforbid isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99fec-121">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="99fec-122">Örneğin, bir uzantı belirli özel bir sanal makine görüntüleri ile uyumlu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="99fec-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="99fec-123">örnekte gösterildiği nasıl aşağıdaki hello tooblock belirli bir uzantıya.</span><span class="sxs-lookup"><span data-stu-id="99fec-123">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="99fec-124">Yayımcı ve türüne toodetermine hangi uzantısı tooblock kullanır.</span><span class="sxs-lookup"><span data-stu-id="99fec-124">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="99fec-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99fec-125">Next steps</span></span>
* <span data-ttu-id="99fec-126">(Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="99fec-126">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="99fec-127">Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="99fec-127">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="99fec-128">Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="99fec-128">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="99fec-129">REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="99fec-129">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="99fec-130">Bir giriş tooresource ilkeleri için bkz: [kaynak ilkesine genel bakış](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="99fec-130">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="99fec-131">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="99fec-131">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
