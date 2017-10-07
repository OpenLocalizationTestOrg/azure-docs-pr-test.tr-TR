---
title: "Windows sanal makineleri Azure üzerinde ilkeleriyle aaaEnforce güvenlik | Microsoft Docs"
description: "Nasıl tooapply İlkesi tooan Azure Resource Manager Windows sanal makine"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: b31c8a03ecf8eed6a929f97fe4146ea14364404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toowindows-vms-with-azure-resource-manager"></a><span data-ttu-id="ba60c-103">İlkeleri tooWindows VM'ler Azure Resource Manager ile uygulama</span><span class="sxs-lookup"><span data-stu-id="ba60c-103">Apply policies tooWindows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="ba60c-104">İlkeleri kullanarak, bir kuruluşun çeşitli kuralları ve kuralları hello kuruluş genelinde zorunlu kılabilir.</span><span class="sxs-lookup"><span data-stu-id="ba60c-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="ba60c-105">İstenen hello davranış zorlama hello kuruluş toohello başarısını katkıda bulunan sırasında risk azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ba60c-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="ba60c-106">Bu makalede, Azure Resource Manager ilkeleri toodefine istenen hello davranışı, kuruluşunuzun sanal makineler için nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="ba60c-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="ba60c-107">Bir giriş toopolicies için bkz: [kullanım ilkesi toomanage kaynakları ve erişimi denetleme](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ba60c-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="ba60c-108">İzin verilen sanal makineler</span><span class="sxs-lookup"><span data-stu-id="ba60c-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="ba60c-109">sanal makineler, kuruluşunuz için bir uygulama ile uyumlu olduğunu tooensure izin işletim sistemleri hello kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba60c-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="ba60c-110">Aşağıdaki ilke örneğine hello oluşturulan Windows Server 2012 R2 Datacenter sanal makineleri toobe izin ver:</span><span class="sxs-lookup"><span data-stu-id="ba60c-110">In hello following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines toobe created:</span></span>

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
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
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

<span data-ttu-id="ba60c-111">Herhangi bir Windows Server Datacenter görüntü İlkesi tooallow önceki bir joker karakter toomodify hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ba60c-111">Use a wild card toomodify hello preceding policy tooallow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="ba60c-112">Herhangi bir Windows Server 2012 R2 Datacenter veya daha yüksek görüntü İlkesi tooallow önceki herhangi toomodify hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ba60c-112">Use anyOf toomodify hello preceding policy tooallow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

<span data-ttu-id="ba60c-113">İlke alanlarını hakkında daha fazla bilgi için bkz: [İlkesi diğer adlar](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="ba60c-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="ba60c-114">Yönetilen diskler</span><span class="sxs-lookup"><span data-stu-id="ba60c-114">Managed disks</span></span>

<span data-ttu-id="ba60c-115">toorequire hello kullanımı yönetilen diskler, ilke aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="ba60c-115">toorequire hello use of managed disks, use hello following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="ba60c-116">Sanal makineler için görüntüleri</span><span class="sxs-lookup"><span data-stu-id="ba60c-116">Images for Virtual Machines</span></span>

<span data-ttu-id="ba60c-117">Güvenlik nedenleriyle, yalnızca onaylanan özel resimler ortamınızda dağıtılan gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="ba60c-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="ba60c-118">Onaylanan hello görüntüleri içeren hello kaynak grubu ya da hello belirli onayladığı yansımaları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba60c-118">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="ba60c-119">Aşağıdaki örnek hello onaylanan kaynak grubu görüntülerden gerektirir:</span><span class="sxs-lookup"><span data-stu-id="ba60c-119">hello following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="ba60c-120">Merhaba aşağıdaki örnek onaylanmış hello resim kimlikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="ba60c-120">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="ba60c-121">Sanal makine uzantıları</span><span class="sxs-lookup"><span data-stu-id="ba60c-121">Virtual Machine extensions</span></span>

<span data-ttu-id="ba60c-122">Belirli türde bir uzantıları kullanımını tooforbid isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba60c-122">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="ba60c-123">Örneğin, bir uzantı belirli özel bir sanal makine görüntüleri ile uyumlu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="ba60c-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="ba60c-124">örnekte gösterildiği nasıl aşağıdaki hello tooblock belirli bir uzantıya.</span><span class="sxs-lookup"><span data-stu-id="ba60c-124">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="ba60c-125">Yayımcı ve türüne toodetermine hangi uzantısı tooblock kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba60c-125">It uses publisher and type toodetermine which extension tooblock.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="ba60c-126">Azure karma kullanımı avantajı</span><span class="sxs-lookup"><span data-stu-id="ba60c-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="ba60c-127">Bir şirket içi lisansı olduğunda, sanal makinelere hello lisans ücret kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba60c-127">When you have an on-premise license, you can save hello license fee on your virtual machines.</span></span> <span data-ttu-id="ba60c-128">Merhaba lisansına sahip olmadığınız durumlarda hello seçeneği yasaklamaz.</span><span class="sxs-lookup"><span data-stu-id="ba60c-128">When you don't have hello license, you should forbid hello option.</span></span> <span data-ttu-id="ba60c-129">ilke aşağıdaki hello kullanım Azure karma kullanımı Avantajı (AHUB) engelliyor:</span><span class="sxs-lookup"><span data-stu-id="ba60c-129">hello following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="ba60c-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba60c-130">Next steps</span></span>
* <span data-ttu-id="ba60c-131">(Örnekler önceki hello gösterildiği gibi) bir ilke kuralı tanımlama sonra toocreate hello ilke tanımı gerekir ve tooa kapsamı atayın.</span><span class="sxs-lookup"><span data-stu-id="ba60c-131">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="ba60c-132">Merhaba kapsam abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="ba60c-132">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="ba60c-133">Merhaba portal aracılığıyla tooassign ilkeleri Bkz [kullanım Azure portal tooassign ve kaynak ilkelerini yönetme](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba60c-133">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="ba60c-134">REST API'si, PowerShell veya Azure CLI aracılığıyla tooassign ilkeleri Bkz [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="ba60c-134">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="ba60c-135">Bir giriş tooresource ilkeleri için bkz: [kaynak ilkesine genel bakış](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ba60c-135">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="ba60c-136">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ba60c-136">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
