---
title: "PowerShell komut dosyası örneği - farklı bir bölgeye VHD tooa depolama hesabı olarak verme/kopyalama anlık görüntü aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - VHD tooa depolama hesabıyla aynı farklı bölgede dışa aktarma/kopyalama anlık görüntü"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Dışa aktarma/yönetilen anlık görüntüler VHD tooa farklı bir bölgeye PowerShell ile depolama hesabı olarak kopyalama

Bu komut dosyasını farklı bir bölgeye yönetilen anlık görüntü tooa depolama hesabında dışa aktarır. İlk hello hello anlık görüntü SAS URI'sini oluşturur ve toocopy kullanır, farklı bölgede tooa depolama hesabı. Bu komut dosyası toomaintain yedekleme yönetilen disklerinizi olağanüstü durum kurtarma için farklı bir bölge kullanın.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toogenerate aşağıdaki kullanır, SAS URI'sini kullanarak tooa depolama hesabı yönetilen anlık görüntülere veya kopyalara hello SAS URI'sini anlık görüntüsünü alın. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [GRANT-AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Kullanılan toocopy bir anlık görüntüyü için SAS URI'sini oluşturur, tooa depolama hesabı. |
| [AzureStorageContext yeni](/powershell/module/azure.storage/New-AzureStorageContext) | Merhaba hesap adı ve anahtarı kullanarak bir depolama hesabı bağlamını oluşturur. Bu bağlamda kullanılan tooperform okuma/yazma işlemleri hello depolama hesabı üzerinde olabilir. |
| [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Kopya bir anlık görüntü tooa depolama hesabının temel VHD hello |

## <a name="next-steps"></a>Sonraki adımlar

[Bir VHD'den yönetilen bir disk oluştur](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Yönetilen bir diskten bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
