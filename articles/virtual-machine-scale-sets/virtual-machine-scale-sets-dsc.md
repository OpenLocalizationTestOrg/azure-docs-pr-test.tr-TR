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
# <a name="using-virtual-machine-scale-sets-with-hello-azure-dsc-extension"></a>Sanal makine ölçek kümeleri hello Azure DSC uzantısı ile kullanma
[Sanal makine ölçek kümeleri](virtual-machine-scale-sets-overview.md) ile Merhaba kullanılabilir [Azure istenen durum yapılandırması (DSC)](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) uzantısı işleyici. Sanal makine ölçek kümeleri şekilde toodeploy sağlayın ve çok sayıda sanal makineleri yönetmek ve yanıt tooload özellikler esnek ve kapatma ölçeklendirebilirsiniz. DSC hello üretim yazılımı çalıştıran şekilde çevrimiçi geldikleri kullanılan tooconfigure hello VM'ler aynıdır.

## <a name="differences-between-deploying-toovirtual-machines-and-virtual-machine-scale-sets"></a>TooVirtual makineler ve sanal makine ölçek kümeleri dağıtma arasındaki farklar
Merhaba temel şablon yapısı bir sanal makine ölçek kümesi için tek bir VM'den biraz farklıdır. Özellikle, tek bir VM uzantıları hello "virtualMachines" düğümünde dağıtır. DSC toohello şablonu burada eklenir "uzantılarla" türünde bir giriş olduğundan

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

Bir sanal makine ölçek kümesi düğüm hello "VirtualMachineProfile", "extensionProfile" özniteliği "Özellikler" bölümle sahiptir. DSC "Uzantılar altında" eklenir

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

## <a name="behavior-for-a-virtual-machine-scale-set"></a>Bir sanal makine ölçek kümesi için davranış
bir sanal makine ölçek kümesi için Hello davranışı, tek bir VM için aynı toohello davranıştır. Yeni VM oluşturulduğunda, DSC uzantısı hello ile otomatik olarak sağlanır. WMF hello uzantısı tarafından istenen hello daha yeni bir sürümü varsa, hello VM çevrimiçine girmeden önce yeniden başlatır. Çevrimiçi olduktan sonra hello DSC yapılandırma .zip indirir ve hello VM üzerinde sağlayın. Daha fazla ayrıntı bulunabilir [Azure DSC uzantısı genel bakış hello](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Sonraki adımlar
Merhaba inceleyin [hello DSC uzantısı için Azure Resource Manager şablonu](../virtual-machines/windows/extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Bilgi nasıl hello [DSC uzantısı kimlik bilgileri güvenli bir şekilde işler](../virtual-machines/windows/extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hello Azure DSC uzantısı işleyici hakkında daha fazla bilgi için bkz: [giriş toohello Azure istenen durum yapılandırması uzantısı işleyici](../virtual-machines/windows/extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

PowerShell DSC hakkında daha fazla bilgi için [hello PowerShell Belge Merkezi ziyaret](https://msdn.microsoft.com/powershell/dsc/overview). 

