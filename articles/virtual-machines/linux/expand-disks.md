---
title: "azure'da bir Linux VM üzerindeki sanal sabit disklere aaaExpand | Microsoft Docs"
description: "Bir Linux VM üzerindeki sanal sabit disklere tooexpand Azure CLI 2.0 nasıl hello öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Bir Linux VM üzerindeki sanal sabit disklere tooexpand Azure CLI nasıl hello
Merhaba varsayılan sanal sabit disk boyutu hello işletim sistemi (OS) için azure'da bir Linux sanal makine (VM) genellikle 30 GB açıktır. Yapabilecekleriniz [veri diski Ekle](add-disk.md) tooprovide ek depolama alanı, ancak ayrıca istediğiniz tooexpand varolan bir veri diski. Bu makalede nasıl tooexpand için bir Linux VM hello Azure CLI 2.0 ile yönetilen disklerde ayrıntıları verilmektedir. Yönetilmeyen hello işletim sistemi diski hello ile genişletebilirsiniz [Azure CLI 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Her zaman, disk gerçekleştirmeden önce verileri yedekleyin operations yeniden boyutlandırma emin olun. Daha fazla bilgi için bkz: [Linux VM'ler için Azure'da yedekleme](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Disk genişletme
Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

Bu makalede Azure mevcut bir VM'yi sahip bağlı ve hazırlanan en az bir veri diski gerektirir. Kullanabileceğiniz VM zaten yoksa bkz [oluşturma ve veri diskleri içeren bir VM hazırlama](tutorial-manage-disks.md#create-and-attach-disks).

Hello aşağıdaki örnekleri, örnek parametre adları kendi değerlerinizle değiştirin. Örnek parametre adlarında *myResourceGroup* ve *myVM*.

1. Sanal sabit diskler üzerinde işlemler hello VM ile gerçekleştirilemiyor çalışıyor. VM ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate). Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`Merhaba işlem kaynaklarını serbest değil. toorelease işlem kaynaklarını, kullanın `az vm deallocate`. Merhaba VM tooexpand hello sanal sabit disk ayırması gerekir.

2. Bir kaynak grubu ile yönetilen disklerin listesini görüntülemek [az disk listesi](/cli/azure/disk#list). Merhaba aşağıdaki örnek yönetilen disklerin listesini adlı hello kaynak grubunda görüntüler *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Merhaba gerekli diskle genişletin [az disk güncelleştirme](/cli/azure/disk#update). Merhaba aşağıdaki örnek genişletir adlı hello yönetilen disk *myDataDisk* toobe *200*Gb boyutunda:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Yönetilen bir disk genişlettiğinizde, güncelleştirilmiş hello en yakın yönetilen disk boyutu eşlenen toohello boyutudur. Merhaba kullanılabilir yönetilen disk boyutları ve katmanları tablosu için bkz: [Azure yönetilen diskleri fiyatlandırma ve faturalama genel bakış -](../windows/managed-disks-overview.md#pricing-and-billing).

3. VM ile başlangıç [az vm başlangıç](/cli/azure/vm#start). Örnek başlatır aşağıdaki hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM hello uygun kimlik bilgilerine sahip. Merhaba, VM ile genel IP adresi elde edebilirsiniz [az vm Göster](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. disk toouse hello genişletilmiş, tooexpand hello altındaki bölüm ve dosya sistemi gerekir.

    a. Takılı, hello disk çıkarın:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Kullanım `parted` tooview disk bilgileri ve hello bölümü yeniden boyutlandırma:

    ```bash
    sudo parted /dev/sdc
    ```

    Merhaba var olan bir bölüm düzeni ile hakkındaki bilgileri görüntüleyin `print`. Merhaba, benzer toohello hello temel disk 215 Gb boyutunda gösterilir örnek aşağıdaki çıktı:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Merhaba bölümüyle genişletin `resizepart`. Merhaba bölüm numarası girin *1*ve hello yeni bölüm için bir boyut:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, girin`quit`

5. Yeniden boyutlandırılabilir hello bölümüyle hello bölüm tutarlılığı doğrulamak `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Şimdi hello dosya sistemi ile yeniden boyutlandırın `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Bağlama hello bölüm toohello istenen konuma gibi `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. tooverify hello işletim sistemi diski yeniden, kullanın `df -h`. örnek çıktı aşağıdaki hello gösterir hello veri sürücüsü */dev/sdc1*, 200 GB sunulmuştur:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Sonraki adımlar
Ek depolama alanı, gerekirse, ayrıca [veri diskleri tooa Linux VM eklemek](add-disk.md). Disk şifrelemesi hakkında daha fazla bilgi için bkz: [kullanarak bir Linux VM şifrele disklerde hello Azure CLI](encrypt-disks.md).
