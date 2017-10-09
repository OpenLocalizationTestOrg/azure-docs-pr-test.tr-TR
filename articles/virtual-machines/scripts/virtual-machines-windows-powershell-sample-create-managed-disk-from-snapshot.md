---
title: "aaaAzure PowerShell komut dosyası örneği - yönetilen bir disk anlık görüntüden oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir anlık görüntüden yönetilen bir disk oluşturma"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: b99413b4c3e9a662a5fef74b7e4aeb5ecbb26af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a>Anlık görüntü PowerShell ile yönetilen bir disk oluşturun

Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturur. İşletim sistemi ve veri disklerin anlık görüntüleri sanal makineden toorestore kullanın. İşletim sistemi oluşturun ve veri diskleri ilgili anlık görüntülerden yönetilen ve ardından yönetilen diskleri ekleyerek yeni bir sanal makine oluşturun. Anlık görüntülerden oluşturulan veri diskleri ekleyerek, mevcut bir VM'yi veri diskleri geri yükleyebilirsiniz.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını komutları toocreate bir anlık görüntü yönetilen bir diskten kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Get-AzureRmSnapshot](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | Anlık görüntü özelliklerini alır.  |
| [AzureRmDiskConfig yeni](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Disk oluşturmak için kullanılan disk yapılandırması oluşturur. Merhaba kaynak hello üst anlık görüntü, üst anlık görüntü ve hello depolama türü hello konumu olarak aynı konuma kimliğini içerir.  |
| [AzureRmDisk yeni](/powershell/module/azurerm.compute/New-AzureRmDisk) | Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur. |


## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir diskten bir sanal makine oluşturun](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
