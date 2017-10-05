---
title: "Azure PowerShell Betiği örnek - yönetilen bir disk anlık görüntüden oluşturun. | Microsoft Docs"
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
ms.openlocfilehash: 9105d9dc06eea33b3a4e1eeea7fd793919166c9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a>Anlık görüntü PowerShell ile yönetilen bir disk oluşturun

Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturur. Bir sanal makine işletim sistemi ve veri diskleri anlık görüntülerden geri yüklemek için kullanın. İşletim sistemi oluşturun ve veri diskleri ilgili anlık görüntülerden yönetilen ve ardından yönetilen diskleri ekleyerek yeni bir sanal makine oluşturun. Anlık görüntülerden oluşturulan veri diskleri ekleyerek, mevcut bir VM'yi veri diskleri geri yükleyebilirsiniz.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[Ana](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "yönetilen diskten anlık görüntü oluşturma")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturmak için komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [Get-AzureRmSnapshot](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | Anlık görüntü özelliklerini alır.  |
| [AzureRmDiskConfig yeni](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Disk oluşturmak için kullanılan disk yapılandırması oluşturur. Kaynak Kimliği üst anlık görüntü ve depolama türü konumu olarak aynı konuma üst anlık görüntü içerir.  |
| [AzureRmDisk yeni](/powershell/module/azurerm.compute/New-AzureRmDisk) | Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur. |


## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir diskten bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).