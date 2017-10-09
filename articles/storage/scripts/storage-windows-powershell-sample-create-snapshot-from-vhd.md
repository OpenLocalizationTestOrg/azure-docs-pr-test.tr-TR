---
title: "aaaAzure PowerShell komut dosyası örneği - oluşturma anlık bir VHD toocreate birden çok özdeş yönetilen diskler kısa sürede | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir anlık görüntü VHD toocreate birden çok özdeş yönetilen diskler küçük bir sürede oluşturun."
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
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Bir anlık görüntü VHD toocreate kısa sürede PowerShell ile birden çok özdeş yönetilen diskler oluşturma

Bu komut dosyası, aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından bir anlık görüntüsü oluşturur. Bu komut dosyası tooimport özel (değil genelleştirilmiş/Sysprep kullanılarak hazırlanmış) VHD tooa anlık görüntü ve ardından hello anlık görüntü toocreate kısa sürede birden çok özdeş yönetilen diskler kullanın. Ayrıca, tooimport veri VHD tooa anlık görüntü kullanın ve ardından hello anlık görüntü toocreate birden çok yönetilen diskleri kısa sürede kullanın. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını komutları toocreate farklı Abonelikteki bir VHD'den yönetilen bir diski kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [AzureRmDiskConfig yeni](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Disk oluşturmak için kullanılan disk yapılandırması oluşturur. Depolama türü, konum, kaynak kimliği hello depolama hesabının hello üst VHD depolandığı ve VHD URİ'si hello üst VHD içerir. |
| [AzureRmDisk yeni](/powershell/module/azurerm.compute/New-AzureRmDisk) | Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur. |

## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir disk anlık görüntüden oluşturma](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
