---
title: "aaaAzure CLI komut dosyası örneği - yönetilen bir disk anlık görüntüden oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir anlık görüntüden yönetilen bir disk oluşturma"
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
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a>Anlık görüntü CLI ile yönetilen bir disk oluşturun

Bu komut dosyasını bir anlık görüntüden yönetilen bir disk oluşturur. İşletim sistemi ve veri disklerin anlık görüntüleri sanal makineden toorestore kullanın. İşletim sistemi oluşturun ve veri diskleri ilgili anlık görüntülerden yönetilen ve ardından yönetilen diskleri ekleyerek yeni bir sanal makine oluşturun. Anlık görüntülerden oluşturulan veri diskleri ekleyerek, mevcut bir VM'yi veri diskleri geri yükleyebilirsiniz.


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını komutları toocreate bir anlık görüntü yönetilen bir diskten kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az anlık görüntü Göster](https://docs.microsoft.com/cli/azure/snapshot#show) | Tüm hello adını kullanarak bir anlık görüntü hello özelliklerini ve kaynak grubu özellikleri hello anlık görüntü alır. ID özelliği kullanılan toocreate yönetilen disktir.  |
| [az disketi oluşturma](https://docs.microsoft.com/cli/azure/disk#create) | Yönetilen oluşturur diski kullanarak, yönetilen bir anlık görüntü kimliğini anlık görüntüsünü alın |

## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
