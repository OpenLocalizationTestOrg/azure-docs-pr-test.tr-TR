---
title: "aaaAzure CLI komut dosyası örneği - VHD ile bir VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir sanal sabit disk kullanan bir VM oluşturma."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a>Bir sanal sabit disk ile bir VM oluşturma

Bu örnek, bir VHD'yi kullanarak bir sanal makine oluşturur.
Bir kaynak grubu, bir depolama hesabı ve kapsayıcı oluşturur, ardından hello VHD toohello kapsayıcı karşıya yükleyerek bir VM oluşturur.
Merhaba ssh ortak yerini böylece erişim toohello VM sahip anahtar ortak anahtarınızla değiştirin.

Önyüklenebilir bir VHD gerekir.
Https://azclisamples.blob.core.windows.net/vhds/sample.vhd hello kullandık VHD indirin veya kendi VHD kullanın. Merhaba komut dosyası arar `~/sample.vhd`.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az depolama hesabı listesi](https://docs.microsoft.com/cli/azure/storage/account#list) | Listeleri depolama hesapları |
| [az depolama hesabı onay-adı](https://docs.microsoft.com/cli/azure/storage/account#check-name) | Depolama hesabı adı geçerli olduğunu ve önceden var olmayan denetler |
| [az depolama hesabı anahtarları listesi](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | Merhaba depolama hesapları için anahtarları listeler |
| [az depolama blob var.](https://docs.microsoft.com/cli/azure/storage/blob#exists) | Merhaba blob mevcut olup olmadığını denetler |
| [az depolama kapsayıcısı oluşturma](https://docs.microsoft.com/cli/azure/storage/container#create) | Bir depolama hesabında bir kapsayıcı oluşturur. |
| [az depolama blob karşıya yükleme](https://docs.microsoft.com/cli/azure/storage/blob#upload) | Bir blob karşıya yükleme hello VHD tarafından hello kapsayıcıda oluşturur. |
| [az vm listesi](https://docs.microsoft.com/cli/azure/vm#list) | İle kullanılan `--query` hello VM adı kullanımda olup olmadığını denetleyin. | 
| [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Merhaba sanal makineler oluşturur. |
| [az vm kümesi linux kullanıcıya erişim](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | Merhaba SSH anahtar toogive hello geçerli kullanıcı erişim toohello VM sıfırlar. |
| [az vm-IP-adresleri listesi](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | Merhaba oluşturulan VM Hello IP adresini alır. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
