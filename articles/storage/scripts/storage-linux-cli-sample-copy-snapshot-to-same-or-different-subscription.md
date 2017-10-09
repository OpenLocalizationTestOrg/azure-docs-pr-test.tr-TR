---
title: "aaaAzure CLI komut dosyası örneği - yönetilen disk toosame veya CLI ile farklı bir abonelik kopya (Taşı) anlık | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yönetilen disk toosame veya CLI ile farklı bir abonelik kopya (Taşı) anlık"
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
ms.openlocfilehash: 4a21fd2435181a033b563100888aba0c5834496d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a>Yönetilen disk toosame veya farklı bir abonelik CLI ile anlık kopyalama

Bu komut, yönetilen disk toosame veya farklı bir abonelik anlık kopyalar. Bu komut dosyası toomove bir anlık görüntü toodifferent abonelik hello kullan hello üst anlık görüntü ile aynı bölgeye.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate aşağıdaki kullanır hello hedef abonelik kullanarak bir anlık görüntü hello hello kaynak anlık görüntü kimliği. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az anlık görüntü Göster](https://docs.microsoft.com/cli/azure/snapshot#show) | Tüm hello adını kullanarak bir anlık görüntü hello özelliklerini ve kaynak grubu özellikleri hello anlık görüntü alır. Kullanılan toocopy hello anlık görüntü toodifferent abonelik kimliği özelliğidir.  |
| [az anlık görüntü oluşturma](https://docs.microsoft.com/cli/azure/snapshot#create) | Farklı bir abonelik kullanarak bir anlık görüntü oluşturarak bir anlık görüntü hello kimliği ve adını kopya üst anlık görüntü hello.  |

## <a name="next-steps"></a>Sonraki adımlar

[Bir sanal makine bir anlık görüntüden oluşturun](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
