---
title: "aaaAzure CLI komut dosyası örneği - farklı bir bölgeye VHD tooa depolama hesabı olarak verme/kopyalama anlık görüntü | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - VHD tooa depolama hesabıyla aynı veya farklı Abonelikteki dışa aktarma/kopyalama anlık görüntü"
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
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a>Dışa aktarma/yönetilen anlık görüntüler CLI ile farklı bir bölgeye VHD tooa depolama hesabı olarak kopyalama

Bu komut dosyasını farklı bir bölgeye yönetilen anlık görüntü tooa depolama hesabında dışa aktarır. İlk hello hello anlık görüntü SAS URI'sini oluşturur ve toocopy kullanır, farklı bölgede tooa depolama hesabı. Bu komut dosyası toomaintain yedekleme yönetilen disklerinizi olağanüstü durum kurtarma için farklı bir bölge kullanın. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toogenerate aşağıdaki kullanır, SAS URI'sini kullanarak tooa depolama hesabı yönetilen anlık görüntülere veya kopyalara hello SAS URI'sini anlık görüntüsünü alın. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [erişim izni ver az anlık görüntüsünü alın](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | VHD dosyası tooa depolama hesabını temel kullanılan toocopy veya karşıdan salt okunur SAS tooon içi oluşturur  |
| [az depolama blob kopyalama Başlat](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | Bir blobu bir depolama hesabı tooanother zaman uyumsuz olarak kopyalar. |

## <a name="next-steps"></a>Sonraki adımlar

[Bir VHD'den yönetilen bir disk oluştur](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[Yönetilen bir diskten bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
