---
title: "aaaAzure PowerShell komut dosyası örneği - aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturma"
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>PowerShell ile aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturma

Bu komut dosyası, aynı veya farklı Abonelikteki depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturur. Bu komut dosyası tooimport bir özel (değil genelleştirilmiş/Sysprep kullanılarak hazırlanmış) VHD toomanaged işletim sistemi disk toocreate bir sanal makine kullanın. Ayrıca, bir veri VHD toomanaged veri diski tooimport kullanın. 

Birden çok özdeş yönetilen diskler bir VHD dosyasından kısa sürede oluşturmayın. bir vhd dosyasından toocreate yönetilen disklerde, blob anlık görüntü hello vhd dosyasının oluşturulur ve yönetilen kullanılan toocreate diskler ise. Yalnızca bir blob anlık görüntü disk oluşturma hataları neden olan bir dakika içinde oluşturulabilir son toothrottling. tooavoid bu kısıtlama, oluşturma bir [yönetilen anlık görüntüden hello vhd dosyasını](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) ve kullanım hello anlık görüntü toocreate birden çok yönetilen diskleri kısa sürede sonra yönetilir. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını komutları toocreate farklı Abonelikteki bir VHD'den yönetilen bir diski kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [AzureRmDiskConfig yeni](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Disk oluşturmak için kullanılan disk yapılandırması oluşturur. Depolama türü, konum, kaynak hello üst VHD depolandığı hello depolama hesabını VHD URİ'si hello üst VHD kimliğini içerir. |
| [AzureRmDisk yeni](/powershell/module/azurerm.compute/New-AzureRmDisk) | Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur. |

## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
