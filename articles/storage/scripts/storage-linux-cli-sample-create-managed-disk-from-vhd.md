---
title: "aaaAzure CLI komut dosyası örneği - hello depolama hesabında bir VHD dosyasından yönetilen bir disk oluşturmak aynı abonelik | Microsoft Docs"
description: "Azure CLI betik örnek - hello depolama hesabında bir VHD dosyasından yönetilen bir disk oluşturma aynı abonelik"
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
ms.openlocfilehash: 1e792fdbb7daea92bf6a6589a5d8aab5b9b5a670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a>Bir VHD dosyasının hello depolama hesabında yönetilen bir disk oluşturmak CLI ile aynı abonelik

Bu komut dosyasını bir VHD dosyasının hello depolama hesabında yönetilen bir disk oluşturur aynı abonelik. Bu komut dosyası tooimport bir özel (değil genelleştirilmiş/Sysprep kullanılarak hazırlanmış) VHD toomanaged işletim sistemi disk toocreate bir sanal makine kullanın. Veya tooimport veri VHD toomanaged veri diski kullanın. 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını komutları toocreate VHD yönetilen bir diskten kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az disketi oluşturma](https://docs.microsoft.com/cli/azure/disk#create) | Merhaba depolama hesabında VHD URI kullanılarak yönetilen bir disk oluşturur aynı abonelik |

## <a name="next-steps"></a>Sonraki adımlar

[Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
