---
title: "aaaAzure PowerShell komut dosyası örneği - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a>PowerShell ile varolan yönetilen bir işletim sistemi diski kullanarak bir sanal makine oluşturun

Bu komut dosyasını varolan yönetilen disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturur. Senaryolar önceki içinde bu komut dosyasını kullanın:
* Yönetilen bir diskten farklı Abonelikteki kopyalanan var olan bir diskten yönetilen işletim sistemi bir VM oluşturma
* Özel bir VHD dosyasından oluşturulmuş var olan bir diskten yönetilen bir VM oluşturma 
* Bir anlık görüntüden oluşturulmuş var olan bir diskten yönetilen işletim sistemi bir VM oluşturma 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları yönetilen tooget disk özelliklere hello kullanıyorsa, yönetilen disk tooa ekleme yeni VM ve VM oluşturun. Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Get-AzureRmDisk](/powershell/module/azurerm.compute/Get-AzureRmDisk) | Merhaba adı ve hello kaynak grubu bir disk temel alınarak disk nesnesini alır. Merhaba kimliği özelliği döndürülür disk nesnesi kullanılan tooattach hello disk tooa yeni VM |
| [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig) | Bir VM yapılandırması oluşturur. Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir. Merhaba yapılandırma VM oluşturma sırasında kullanılır. |
| [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) | İşletim sistemi disk tooa yeni sanal makine hello disk Hello kimliği özelliğini kullanarak yönetilen bir disk ekler |
| [AzureRmPublicIpAddress yeni](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Bir ortak IP adresi oluşturur. |
| [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Bir ağ arabirimi oluşturur. |
| [Yeni-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Bir sanal makine oluşturun. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
