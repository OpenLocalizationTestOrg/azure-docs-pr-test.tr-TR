---
title: "Azure CLI komut dosyası örneği - kopyalama (Taşı) yönetilen aynı veya farklı bir abonelik disklere | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - kopyalama (Taşı) yönetilen aynı veya farklı bir abonelik disklere"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 784ad81db2c83da14665fa926425928f12a15c27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a>CLI ile aynı veya farklı aboneliğe yönetilen diskleri kopyalama

Bu komut dosyası, aynı veya farklı bir abonelik ancak aynı bölgede yönetilen bir diske kopyalar. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[Ana](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "kopya disk yönetilen")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını yeni bir yönetilen disk kaynağı yönetilen disk kimliğini kullanarak hedef abonelikte oluşturmak için komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az disk Göster](https://docs.microsoft.com/cli/azure/disk#show) | Tüm adını kullanarak yönetilen bir diskin özelliklerini ve kaynak grubu yönetilen diskin özelliklerini alır. ID özelliği, yönetilen disk farklı aboneliğe kopyalamak için kullanılır.  |
| [az disketi oluşturma](https://docs.microsoft.com/cli/azure/disk#create) | Kopya yeni oluşturma tarafından yönetilen bir disk disk kimliğini kullanarak farklı Abonelikteki yönetilen ve üst yönetilen disk adlandırın.  |

## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir diskten bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
