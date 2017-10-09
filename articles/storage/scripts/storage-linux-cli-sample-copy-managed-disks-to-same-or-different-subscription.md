---
title: "aaaAzure CLI komut dosyası örneği - kopyalama (Taşı) yönetilen diskleri toosame veya farklı bir abonelik | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - yönetilen kopyalama (Taşı) diskleri toosame veya farklı bir abonelik"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a>Yönetilen diskleri toosame veya farklı bir abonelik CLI ile kopyalama

Bu komut dosyasını bir yönetilen disk toosame veya farklı bir abonelik kopyalar ancak içinde aynı hello bölgesi. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Aşağıdaki komutları toocreate kullanır hello hedef abonelik kullanarak yeni bir yönetilen disk hello hello kaynak kimliğini bu komut dosyası disk yönetilen. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az disk Göster](https://docs.microsoft.com/cli/azure/disk#show) | Merhaba yönetilen disk hello ad ve kaynak grubu özellikleri kullanılarak yönetilen bir disk tüm hello özelliklerini alır. Kullanılan toocopy yönetilen hello disk toodifferent abonelik kimliği özelliğidir.  |
| [az disketi oluşturma](https://docs.microsoft.com/cli/azure/disk#create) | Yönetilen bir disk kimliği ve adını kullanarak farklı abonelikte yeni bir yönetilen disk oluşturarak kopyalar hello üst disk yönetilen.  |

## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir diskten bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
