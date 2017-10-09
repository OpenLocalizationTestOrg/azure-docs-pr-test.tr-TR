---
title: Linux VM aaaExpand OS diskte hello Azure CLI 1.0 ile | Microsoft Docs
description: "Nasıl tooexpand hello hello Azure CLI 1.0 ve hello Resource Manager dağıtım modeli kullanarak bir Linux VM üzerindeki işletim sistemi (OS) sanal diski öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Azure CLI 1.0 hello ile hello Azure CLI kullanarak bir Linux VM üzerindeki işletim sistemi diski genişletin
Merhaba varsayılan sanal sabit disk boyutu hello işletim sistemi (OS) için azure'da bir Linux sanal makine (VM) genellikle 30 GB açıktır. Yapabilecekleriniz [veri diski Ekle](add-disk.md) tooprovide ek depolama alanı, ancak tooexpand hello işletim sistemi diski de istiyor. Bu makalede nasıl tooexpand hello işletim sistemi disk hello Azure CLI 1.0 ile yönetilmeyen diskleri kullanarak bir Linux VM için ayrıntıları verilmektedir.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#prerequisites) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](expand-disks.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için

## <a name="prerequisites"></a>Ön koşullar
Merhaba gereksinim [en son Azure CLI 1.0](../../cli-install-nodejs.md) yüklü ve tooan içinde günlüğe [Azure hesabı](https://azure.microsoft.com/pricing/free-trial/) hello Resource Manager modunu kullanarak:

```azurecli
azure config mode arm
```

Hello aşağıdaki örnekleri, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup* ve *myVM*.

## <a name="expand-os-disk"></a>İşletim sistemi diskini genişletme

1. Sanal sabit diskler üzerinde işlemler hello VM ile gerçekleştirilemiyor çalışıyor. Merhaba aşağıdaki örnek durdurur ve hello adlı VM kaldırır *myVM* adlı hello kaynak grubunda *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`Merhaba işlem kaynaklarını serbest değil. toorelease işlem kaynaklarını, kullanın `azure vm deallocate`. Merhaba VM tooexpand hello sanal sabit disk ayırması gerekir.

2. Yönetilmeyen hello işletim sistemi diski hello kullanarak Hello boyutunu güncelleştirme `azure vm set` komutu. Şu örnek güncelleştirmeleri hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup* toobe *50* GB:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. VM şu şekilde başlatın:

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM hello uygun kimlik bilgilerine sahip. tooverify hello işletim sistemi diski yeniden, kullanın `df -h`. örnek çıktı aşağıdaki hello hello birincil bölüm gösterir (*/dev/sda1*) 50 GB sunulmuştur:

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Sonraki adımlar
Ek depolama alanı, gerekirse, ayrıca [veri diskleri tooa Linux VM eklemek](add-disk.md). Disk şifrelemesi hakkında daha fazla bilgi için bkz: [kullanarak bir Linux VM şifrele disklerde hello Azure CLI](encrypt-disks.md).
