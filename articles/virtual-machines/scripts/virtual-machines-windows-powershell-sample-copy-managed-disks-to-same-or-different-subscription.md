---
title: "aaaAzure PowerShell komut dosyası örneği - kopyalama (Taşı) yönetilen diskleri toosame veya farklı bir abonelik | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yönetilen kopyalama (Taşı) diskleri toosame veya farklı bir abonelik"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 22e19a47228cbf628bebebd73012b8aa7baf073c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a>Yönetilen kopyalama diskler hello aynı abonelik veya PowerShell ile farklı bir abonelik

Bu komut dosyasını varolan bir yönetilen diski kopyasını hello oluşturur. aynı abonelik veya farklı bir abonelik. Merhaba yeni diski hello aynı oluşturulur hello üst bölgede yönetilen disk.   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Aşağıdaki komutları toocreate kullanır hello hedef abonelik kullanarak yeni bir yönetilen disk hello hello kaynak kimliğini bu komut dosyası disk yönetilen. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [AzureRmDiskConfig yeni](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Disk oluşturmak için kullanılan disk yapılandırması oluşturur. Merhaba kaynak kimliği hello üst disk ve üst diski hello konumu olarak aynı konuma içerir.  |
| [AzureRmDisk yeni](/powershell/module/azurerm.compute/New-AzureRmDisk) | Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur. |


## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir diskten bir sanal makine oluşturun](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
