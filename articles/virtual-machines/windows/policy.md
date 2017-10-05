---
title: "Windows sanal makineleri Azure üzerinde ilkeleri ile güvenlik zorlama | Microsoft Docs"
description: "Bir Azure Kaynak Yöneticisi'ni Windows sanal makine için bir ilke uygulama"
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
ms.openlocfilehash: 246f5958478fd6d9afc9ba990413ab08429bd25d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-policies-to-windows-vms-with-azure-resource-manager"></a><span data-ttu-id="db0d1-103">Azure Resource Manager ile Windows sanal makineleri için geçerlidir</span><span class="sxs-lookup"><span data-stu-id="db0d1-103">Apply policies to Windows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="db0d1-104">İlkeleri kullanarak, bir kuruluşun çeşitli kuralları ve kuruluş genelinde kuralları zorunlu kılabilir.</span><span class="sxs-lookup"><span data-stu-id="db0d1-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="db0d1-105">İstenen davranışı zorlama kuruluşun başarısı için katkıda bulunan sırasında risk azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="db0d1-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="db0d1-106">Bu makalede, kuruluşunuzun sanal makineler için istenen davranışı tanımlamak için Azure Resource Manager ilkelerini nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="db0d1-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="db0d1-107">İlkeleri giriş için bkz: [kaynakları yönetmek ve erişimi denetlemek için ilke kullanma](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="db0d1-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="db0d1-108">İzin verilen sanal makineler</span><span class="sxs-lookup"><span data-stu-id="db0d1-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="db0d1-109">Sanal makineler, kuruluşunuz için bir uygulama ile uyumlu olduğundan emin olmak için izin verilen işletim sistemleri sınırlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0d1-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="db0d1-110">Aşağıdaki ilke örnekte, yalnızca Windows Server 2012 R2 Datacenter oluşturulması için sanal makineleri izin ver:</span><span class="sxs-lookup"><span data-stu-id="db0d1-110">In the following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created:</span></span>

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

<span data-ttu-id="db0d1-111">Herhangi bir Windows Server Datacenter görüntü izin vermek için önceki ilkeyi değiştirmek için joker kullanın:</span><span class="sxs-lookup"><span data-stu-id="db0d1-111">Use a wild card to modify the preceding policy to allow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="db0d1-112">Herhangi bir Windows Server 2012 R2 Datacenter veya daha yüksek görüntü izin vermek için önceki ilkeyi değiştirmek için herhangi kullanın:</span><span class="sxs-lookup"><span data-stu-id="db0d1-112">Use anyOf to modify the preceding policy to allow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

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

<span data-ttu-id="db0d1-113">İlke alanlarını hakkında daha fazla bilgi için bkz: [İlkesi diğer adlar](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="db0d1-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="db0d1-114">Yönetilen diskler</span><span class="sxs-lookup"><span data-stu-id="db0d1-114">Managed disks</span></span>

<span data-ttu-id="db0d1-115">Yönetilen disklerin gerektirmek için aşağıdaki ilke kullanın:</span><span class="sxs-lookup"><span data-stu-id="db0d1-115">To require the use of managed disks, use the following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="db0d1-116">Sanal makineler için görüntüleri</span><span class="sxs-lookup"><span data-stu-id="db0d1-116">Images for Virtual Machines</span></span>

<span data-ttu-id="db0d1-117">Güvenlik nedenleriyle, yalnızca onaylanan özel resimler ortamınızda dağıtılan gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="db0d1-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="db0d1-118">Özel resimler onaylanmış veya onaylanan görüntüleri içeren kaynak grubu ya da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0d1-118">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="db0d1-119">Aşağıdaki örnek, onaylanan kaynak grubu görüntülerden gerektirir:</span><span class="sxs-lookup"><span data-stu-id="db0d1-119">The following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="db0d1-120">Aşağıdaki örnek, onaylanan resim kimlikleri belirtir:</span><span class="sxs-lookup"><span data-stu-id="db0d1-120">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="db0d1-121">Sanal makine uzantıları</span><span class="sxs-lookup"><span data-stu-id="db0d1-121">Virtual Machine extensions</span></span>

<span data-ttu-id="db0d1-122">Belirli türde bir uzantıları kullanımını yasaklamaz isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0d1-122">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="db0d1-123">Örneğin, bir uzantı belirli özel bir sanal makine görüntüleri ile uyumlu olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="db0d1-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="db0d1-124">Aşağıdaki örnek, belirli bir uzantıya engelleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="db0d1-124">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="db0d1-125">Yayımcı ve türüne engellemek için hangi uzantısı belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="db0d1-125">It uses publisher and type to determine which extension to block.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="db0d1-126">Azure karma kullanımı avantajı</span><span class="sxs-lookup"><span data-stu-id="db0d1-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="db0d1-127">Bir şirket içi lisansı olduğunda, sanal makinelere lisans ücret kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db0d1-127">When you have an on-premise license, you can save the license fee on your virtual machines.</span></span> <span data-ttu-id="db0d1-128">Lisansına sahip olmadığınız durumlarda seçeneği yasaklamaz.</span><span class="sxs-lookup"><span data-stu-id="db0d1-128">When you don't have the license, you should forbid the option.</span></span> <span data-ttu-id="db0d1-129">Aşağıdaki ilke kullanım Azure karma kullanımı Avantajı (AHUB) engelliyor:</span><span class="sxs-lookup"><span data-stu-id="db0d1-129">The following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="db0d1-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db0d1-130">Next steps</span></span>
* <span data-ttu-id="db0d1-131">(Yukarıdaki örneklerde gösterildiği gibi) bir ilke kuralı tanımladıktan sonra ilke tanımı oluşturun ve bir kapsama atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db0d1-131">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="db0d1-132">Kapsamı bir abonelik, kaynak grubu veya kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="db0d1-132">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="db0d1-133">Portal üzerinden ilkeler atamak için bkz: [atamak ve kaynak ilkelerini yönetmek için kullanım Azure portal](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="db0d1-133">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="db0d1-134">REST API'si, PowerShell veya Azure CLI aracılığıyla ilkeleri atamak için bkz: [atayın ve komut dosyası aracılığıyla ilkelerini yönetme](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="db0d1-134">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="db0d1-135">Kaynak ilkelerini giriş için bkz: [kaynak ilkesine genel bakış](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="db0d1-135">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="db0d1-136">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="db0d1-136">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
