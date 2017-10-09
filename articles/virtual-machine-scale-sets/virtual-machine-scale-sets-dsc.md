---
title: "aaaUsing istenen durum yapılandırması ile sanal makine ölçek kümeleri | Microsoft Docs"
description: "Sanal makine ölçek kümeleri hello Azure DSC uzantısı ile kullanma"
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
ms.openlocfilehash: a35f1ca6700aa4889978032aa512882db50d6573
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a><span data-ttu-id="575ea-103">Sanal makine ölçek kümeleri hello Azure DSC uzantısı ile kullanma</span><span class="sxs-lookup"><span data-stu-id="575ea-103">Using Virtual Machine Scale Sets with hello Azure DSC Extension</span></span>
<span data-ttu-id="575ea-104">[Sanal makine ölçek kümeleri](virtual-machine-scale-sets-overview.md) ile Merhaba kullanılabilir [Azure istenen durum yapılandırması (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uzantısı işleyici.</span><span class="sxs-lookup"><span data-stu-id="575ea-104">[Virtual Machine Scale Sets](virtual-machine-scale-sets-overview.md) can be used with hello [Azure Desired State Configuration (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) extension handler.</span></span> <span data-ttu-id="575ea-105">Sanal makine ölçek kümeleri şekilde toodeploy sağlayın ve çok sayıda sanal makineleri yönetmek ve yanıt tooload özellikler esnek ve kapatma ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="575ea-105">Virtual machine scale sets provide a way toodeploy and manage large numbers of virtual machines, and can elastically scale in and out in response tooload.</span></span> <span data-ttu-id="575ea-106">DSC hello üretim yazılımı çalıştıran şekilde çevrimiçi geldikleri kullanılan tooconfigure hello VM'ler aynıdır.</span><span class="sxs-lookup"><span data-stu-id="575ea-106">DSC is used tooconfigure hello VMs as they come online so they are running hello production software.</span></span>

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a><span data-ttu-id="575ea-107">TooVirtual makineler ve sanal makine ölçek kümeleri dağıtma arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="575ea-107">Differences between deploying tooVirtual Machines and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="575ea-108">Merhaba temel şablon yapısı bir sanal makine ölçek kümesi için tek bir VM'den biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="575ea-108">hello underlying template structure for a virtual machine scale set is slightly different from a single VM.</span></span> <span data-ttu-id="575ea-109">Özellikle, tek bir VM uzantıları hello "virtualMachines" düğümünde dağıtır.</span><span class="sxs-lookup"><span data-stu-id="575ea-109">Specifically, a single VM deploys extensions under hello "virtualMachines" node.</span></span> <span data-ttu-id="575ea-110">DSC toohello şablonu burada eklenir "uzantılarla" türünde bir giriş olduğundan</span><span class="sxs-lookup"><span data-stu-id="575ea-110">There is an entry of type "extensions" where DSC is added toohello template</span></span>

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

<span data-ttu-id="575ea-111">Bir sanal makine ölçek kümesi düğüm hello "VirtualMachineProfile", "extensionProfile" özniteliği "Özellikler" bölümle sahiptir.</span><span class="sxs-lookup"><span data-stu-id="575ea-111">A virtual machine scale set node has a "properties" section with hello "VirtualMachineProfile", "extensionProfile" attribute.</span></span> <span data-ttu-id="575ea-112">DSC "Uzantılar altında" eklenir</span><span class="sxs-lookup"><span data-stu-id="575ea-112">DSC is added under "extensions"</span></span>

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a><span data-ttu-id="575ea-113">Bir sanal makine ölçek kümesi için davranış</span><span class="sxs-lookup"><span data-stu-id="575ea-113">Behavior for a Virtual Machine Scale Set</span></span>
<span data-ttu-id="575ea-114">bir sanal makine ölçek kümesi için Hello davranışı, tek bir VM için aynı toohello davranıştır.</span><span class="sxs-lookup"><span data-stu-id="575ea-114">hello behavior for a virtual machine scale set is identical toohello behavior for a single VM.</span></span> <span data-ttu-id="575ea-115">Yeni VM oluşturulduğunda, DSC uzantısı hello ile otomatik olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="575ea-115">When a new VM is created, it is automatically provisioned with hello DSC extension.</span></span> <span data-ttu-id="575ea-116">WMF hello uzantısı tarafından istenen hello daha yeni bir sürümü varsa, hello VM çevrimiçine girmeden önce yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="575ea-116">If a newer version of hello WMF is required by hello extension, hello VM reboots before coming online.</span></span> <span data-ttu-id="575ea-117">Çevrimiçi olduktan sonra hello DSC yapılandırma .zip indirir ve hello VM üzerinde sağlayın.</span><span class="sxs-lookup"><span data-stu-id="575ea-117">Once it is online, it downloads hello DSC configuration .zip and provision it on hello VM.</span></span> <span data-ttu-id="575ea-118">Daha fazla ayrıntı bulunabilir [Azure DSC uzantısı genel bakış hello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="575ea-118">More details can be found in [hello Azure DSC Extension Overview](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="575ea-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="575ea-119">Next steps</span></span>
<span data-ttu-id="575ea-120">Merhaba inceleyin [hello DSC uzantısı için Azure Resource Manager şablonu](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="575ea-120">Examine hello [Azure Resource Manager template for hello DSC extension](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="575ea-121">Bilgi nasıl hello [DSC uzantısı kimlik bilgileri güvenli bir şekilde işler](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="575ea-121">Learn how hello [DSC extension securely handles credentials](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="575ea-122">Hello Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="575ea-122">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="575ea-123">PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="575ea-123">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

