---
title: "aaaConvert yönetilmeyenden Linux sanal makine azure'da diskler toomanaged diskler - Azure yönetilen disk | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde Azure CLI 2.0 kullanarak tooconvert yönetilmeyen diskleri toomanaged Linux VM'den nasıl diskler"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Linux sanal makine yönetilmeyen diskleri toomanaged disklerden Dönüştür

Yönetilmeyen diskleri kullanan bir varolan Linux sanal makineleri (VM'ler) varsa, hello aracılığıyla hello VM'ler yönetilen toouse diskler dönüştürülebilir [Azure yönetilen diskleri](../windows/managed-disks-overview.md) hizmet. Bu işlem hello işletim sistemi disk ve tüm eklenen veri disklerini dönüştürür.

Bu makalede, Azure CLI kullanarak sanal makineleri tooconvert hello nasıl gösterir. Yükseltmek veya tooinstall gerekir, bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Başlamadan önce

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Tek Örnekli VM'ler Dönüştür
Bu bölüm, nasıl tooconvert Tek Örnekli yönetilmeyenden Azure VM'ler toomanaged diskleri kapsar. (Bir kullanılabilirlik kümesine Vm'leriniz varsa hello sonraki bölüme bakın.) Bu işlem tooconvert hello yönetilmeyen VM'ler yönetilmeyen premium (SSD) diskleri yönetilen toopremium diskleri veya standart (HDD) diskleri yönetilen toostandard diskleri kullanabilirsiniz.

1. Kullanarak Hello VM serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate). Merhaba aşağıdaki örnek kaldırır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Merhaba VM toomanaged diskleri kullanarak dönüştürme [az vm dönüştürme](/cli/azure/vm#convert). işlem dönüştürür aşağıdaki hello hello adlı VM `myVM`hello işletim sistemi diski ve veri diskleri dahil olmak üzere:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Merhaba VM hello dönüştürme toomanaged diskleri sonra başlamayı [az vm başlangıç](/cli/azure/vm#start). Örnek başlatır aşağıdaki hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Sanal makineleri bir kullanılabilirlik kümesine Dönüştür

Tooconvert toomanaged disklerdir bir kullanılabilirlik kümesinde istediğiniz hello VM'ler, ilk tooconvert hello kullanılabilirlik kümesi tooa yönetilen ihtiyacınız varsa kullanılabilirlik kümesi.

Merhaba kullanılabilirlik kümesi dönüştürmeden önce hello kullanılabilirlik kümesindeki tüm VM'ler serbest gerekir. Tüm sanal makineleri toomanaged diskleri hello kullanılabilirlik sonra kendisini ayarlamak planı tooconvert yönetilen dönüştürülmüş tooa kullanılabilirlik kümesi olmuştur. Ardından, tüm hello VM'ler başlatın ve normal olarak çalışmaya devam.

1. Kullanılabilirlik kümesi kullanarak tüm sanal makineleri listesinde [az vm kullanılabilirlik kümesi listesi](/cli/azure/vm/availability-set#list). Merhaba aşağıdaki örnekte tüm VM'ler hello kullanılabilirlik adlandırılmış kümesi içinde listelenmiştir `myAvailabilitySet` adlı hello kaynak grubunda `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Kullanarak tüm hello VM'ler ayırması [az vm serbest bırakma](/cli/azure/vm#deallocate). Merhaba aşağıdaki örnek kaldırır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Merhaba kullanılabilirlik kullanarak kümesi Dönüştür [az vm kullanılabilirlik kümesi dönüştürme](/cli/azure/vm/availability-set#convert). Merhaba aşağıdaki örnek dönüştürür hello kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet` adlı hello kaynak grubunda `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Kullanarak tüm hello VM'ler toomanaged diskleri dönüştürme [az vm dönüştürme](/cli/azure/vm#convert). işlem dönüştürür aşağıdaki hello hello adlı VM `myVM`hello işletim sistemi diski ve veri diskleri dahil olmak üzere:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Tüm hello VM'ler hello dönüştürme toomanaged diskleri sonra başlamayı [az vm başlangıç](/cli/azure/vm#start). Örnek başlatır aşağıdaki hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Sonraki adımlar
Depolama seçenekleri hakkında daha fazla bilgi için bkz: [Azure yönetilen diskleri genel bakış](../windows/managed-disks-overview.md).
