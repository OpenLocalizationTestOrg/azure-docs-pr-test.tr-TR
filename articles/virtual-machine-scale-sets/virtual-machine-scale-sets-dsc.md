---
title: "İstenen durum yapılandırması ile sanal makine ölçekleme kümeleri kullanarak | Microsoft Docs"
description: "Sanal makine ölçek kullanarak Azure DSC uzantısı ile ayarlar"
services: virtual-machine-scale-sets
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: c8f047b5-0e6c-4ef3-8a47-f1b284d32942
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 04/05/2017
ms.author: zachal
ms.openlocfilehash: b61b0acf3072569ab733a13defb465c921d26187
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-virtual-machine-scale-sets-with-the-azure-dsc-extension"></a><span data-ttu-id="c2813-103">Sanal makine ölçek kullanarak Azure DSC uzantısı ile ayarlar</span><span class="sxs-lookup"><span data-stu-id="c2813-103">Using Virtual Machine Scale Sets with the Azure DSC Extension</span></span>
<span data-ttu-id="c2813-104">[Sanal makine ölçek kümeleri](virtual-machine-scale-sets-overview.md) ile kullanılan [Azure istenen durum yapılandırması (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uzantısı işleyici.</span><span class="sxs-lookup"><span data-stu-id="c2813-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with the [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="c2813-105">Sanal makine ölçek kümeleri dağıtmak ve çok sayıda sanal makineleri yönetmek için bir yol sağlayın ve Özellikler esnek yük yanıtta ölçeğini.</span><span class="sxs-lookup"><span data-stu-id="c2813-105">Virtual machine scale sets provide a way to deploy and manage large numbers of virtual machines, and can elastically scale in and out in response to load.</span></span> <span data-ttu-id="c2813-106">DSC Vm'leri üretim yazılımı çalıştıran şekilde çevrimiçine bunlar yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2813-106">DSC is used to configure the VMs as they come online so they are running the production software.</span></span>

## <a name="differences-between-deploying-to-virtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="c2813-107">Sanal makineler ve sanal makine ölçek kümeleri dağıtma arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="c2813-107">Differences between deploying to Virtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="c2813-108">Şablon yapılarını bir sanal makine ölçek kümesi için tek bir VM'den biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="c2813-108">The underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="c2813-109">Özellikle, tek bir VM uzantıları "virtualMachines" düğümünde dağıtır.</span><span class="sxs-lookup"><span data-stu-id="c2813-109">Specifically, a single VM deploys extensions under the "virtualMachines" node.</span></span> <span data-ttu-id="c2813-110">DSC şablona burada eklenir "uzantılarla" türünde bir giriş olduğundan</span><span class="sxs-lookup"><span data-stu-id="c2813-110">There is an entry of type "extensions" where DSC is added to the template</span></span>

```
"resources": [
          {
              "name": "Microsoft.Powershell.DSC",
              "type": "extensions",
              "location": "[resourceGroup().location]",
              "apiVersion": "2015-06-15",
              "dependsOn": [
                  "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
              ],
              "tags": {
                  "displayName": "dscExtension"
              },
              "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.20",
                  "autoUpgradeMinorVersion": false,
                  "forceUpdateTag": "[parameters('dscExtensionUpdateTagVersion')]",
                  "settings": {
                      "configuration": {
                          "url": "[concat(parameters('_artifactsLocation'), '/', variables('dscExtensionArchiveFolder'), '/', variables('dscExtensionArchiveFileName'))]",
                          "script": "DscExtension.ps1",
                          "function": "Main"
                      },
                      "configurationArguments": {
                          "nodeName": "[variables('vmName')]"
                      }
                  },
                  "protectedSettings": {
                      "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                  }
              }
          }
      ]
```

<span data-ttu-id="c2813-111">Bir sanal makine ölçek kümesi düğümü "VirtualMachineProfile", "extensionProfile" özniteliği "Özellikler" bölümle sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c2813-111">A virtual machine scale set node has a "properties" section with the "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="c2813-112">DSC "Uzantılar altında" eklenir</span><span class="sxs-lookup"><span data-stu-id="c2813-112">DSC is added under "extensions"</span></span>

```
"extensionProfile": {
            "extensions": [
                {
                    "name": "Microsoft.Powershell.DSC",
                    "properties": {
                        "publisher": "Microsoft.Powershell",
                        "type": "DSC",
                        "typeHandlerVersion": "2.20",
                        "autoUpgradeMinorVersion": false,
                        "forceUpdateTag": "[parameters('DscExtensionUpdateTagVersion')]",
                        "settings": {
                            "configuration": {
                                "url": "[concat(parameters('_artifactsLocation'), '/', variables('DscExtensionArchiveFolder'), '/', variables('DscExtensionArchiveFileName'))]",
                                "script": "DscExtension.ps1",
                                "function": "Main"
                            },
                            "configurationArguments": {
                                "nodeName": "localhost"
                            }
                        },
                        "protectedSettings": {
                            "configurationUrlSasToken": "[parameters('_artifactsLocationSasToken')]"
                        }
                    }
                }
            ]
```

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="c2813-113">Bir sanal makine ölçek kümesi için davranış</span><span class="sxs-lookup"><span data-stu-id="c2813-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="c2813-114">Bir sanal makine ölçek kümesi için davranış davranışı, tek bir VM için aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c2813-114">The behavior for a virtual machine scale set is identical to the behavior for a single VM.</span></span> <span data-ttu-id="c2813-115">Yeni VM oluşturulduğunda, DSC uzantısı ile otomatik olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="c2813-115">When a new VM is created, it is automatically provisioned with the DSC extension.</span></span> <span data-ttu-id="c2813-116">WMF daha yeni bir sürümü uzantısı tarafından gerekirse, VM çevrimiçine girmeden önce yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="c2813-116">If a newer version of the WMF is required by the extension, the VM reboots before coming online.</span></span> <span data-ttu-id="c2813-117">Çevrimiçi olduktan sonra DSC yapılandırma .zip indirir ve VM sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c2813-117">Once it is online, it downloads the DSC configuration .zip and provision it on the VM.</span></span> <span data-ttu-id="c2813-118">Daha fazla ayrıntı bulunabilir [Azure DSC uzantısı genel bakış](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2813-118">More details can be found in [the Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2813-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c2813-119">Next steps</span></span>
<span data-ttu-id="c2813-120">İncelemek [DSC uzantısı için Azure Resource Manager şablonu](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2813-120">Examine the [Azure Resource Manager template for the DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c2813-121">Bilgi nasıl [DSC uzantısı kimlik bilgileri güvenli bir şekilde işler](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2813-121">Learn how the [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c2813-122">Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı işleyici giriş](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2813-122">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c2813-123">PowerShell DSC hakkında daha fazla bilgi için [PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="c2813-123">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

