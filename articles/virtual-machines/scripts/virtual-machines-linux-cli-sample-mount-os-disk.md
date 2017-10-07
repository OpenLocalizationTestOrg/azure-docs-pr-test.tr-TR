---
title: "aaaAzure CLI komut dosyası örneği - bağlama işletim sistemi diski | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bağlama işletim sistemi diski"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a>Sanal makineleri işletim sistemi disk sorunlarını gider

Bu komut dosyası hello işletim sistemi diski başarısız veya sorunlu bir sanal makinenin veri diski tooa ikinci sanal makine olarak bağlar. Sorun giderme disk sorunları ya da veri kurtarma bu kullanışlı olabilir. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az vm Göster](https://docs.microsoft.com/cli/azure/vm#show) | Sanal makinelerin listesini döndürür. Bu durumda, hello sorgu kullanılan tooreturn hello sanal makine işletim sistemi diski seçenektir. Bu değer daha sonra tooa değişken adı 'uri' eklenir. |
| [az vm silme](https://docs.microsoft.com/cli/azure/vm#delete) | Bir sanal makineyi siler. |
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create) | Bir sanal makine oluşturur.  |
| [az vm diski kullanıma açın](https://docs.microsoft.com/cli/azure/vm/disk#attach) | Bir disk tooa sanal makineye iliştirir. |
| [az vm-IP-adresleri listesi](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Bir sanal makine IP adreslerini döndürür hello. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
