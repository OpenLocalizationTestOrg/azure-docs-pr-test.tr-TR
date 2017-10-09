---
title: "PowerShell komut dosyası örneği - yönetilen disk toosame veya farklı bir abonelik kopya (Taşı) anlık aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yönetilen disk toosame veya farklı bir abonelik kopya (Taşı) anlık"
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a>Aynı abonelik ya da farklı bir abonelik PowerShell ile yönetilen bir disk görüntüsünü Kopyala

Bu komut dosyasının bir kopyasını bir anlık görüntü hello oluşturur aynı aynı abonelik veya farklı bir abonelik. Bu komut dosyası toomove bir anlık görüntü toodifferent abonelik veri saklama için kullanın. Farklı Abonelikteki depolama anlık görüntüler, anlık görüntü ana aboneliğinizde yanlışlıkla silinmeye karşı koruyun. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate aşağıdaki kullanır hello hedef abonelik kullanarak bir anlık görüntü hello hello kaynak anlık görüntü kimliği. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [AzureRmSnapshotConfig yeni](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | Anlık görüntü oluşturmak için kullanılan anlık görüntü yapılandırması oluşturur. Merhaba kaynak hello üst anlık görüntü ve hello üst anlık görüntü olarak aynı konuma kimliğini içerir.  |
| [AzureRmSnapshot yeni](/powershell/module/azurerm.compute/New-AzureRmDisk) | Anlık görüntü yapılandırması, anlık görüntü adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir anlık görüntüsü oluşturur. |


## <a name="next-steps"></a>Sonraki adımlar

[Bir sanal makine bir anlık görüntüden oluşturun](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
