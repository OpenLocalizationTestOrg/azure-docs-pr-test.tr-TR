---
title: bir Linux VM hello Azure CLI 2.0 ile aaaHow tooresize | Microsoft Docs
description: "Nasıl tooscale yukarı veya aşağı değiştirerek Linux sanal makine ölçek hello VM boyutu."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>CLI 2.0 kullanarak bir Linux sanal makine yeniden boyutlandırma

Bir sanal makine (VM) sağlama sonra hello VM yukarı veya aşağı hello değiştirerek ölçeklendirmek [VM boyutu][vm-sizes]. Bazı durumlarda, ilk hello VM ayırması gerekir. Merhaba boyutu hello VM barındırma hello donanım kümede kullanılabilir değil isterseniz toodeallocate hello VM gerekir. Bu makalede, nasıl bir Linux VM tooresize hello Azure CLI 2.0 ayrıntıları. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>VM’yi yeniden boyutlandırma
bir VM tooresize, gereksinim duyduğunuz hello son [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

1. Görünüm hello listesi kullanılabilir VM boyutları ile Merhaba VM barındırıldığı hello donanım kümede [az vm listesi-vm-yeniden boyutlandırma-seçenekleri](/cli/azure/vm#list-vm-resize-options). Merhaba aşağıdaki örnek listeler VM boyutları hello adlı VM için `myVM` hello kaynak grubunda `myResourceGroup` bölge:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. Merhaba VM boyutu listelendiğini isterseniz, yeniden boyutlandırma VM ile Merhaba [az VM'yi yeniden boyutlandırın](/cli/azure/vm#resize). Aşağıdaki örnek yeniden boyutlandırır hello hello adlı VM `myVM` toohello `Standard_DS3_v2` boyutu:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Bu işlem sırasında Hello VM yeniden başlatır. Merhaba yeniden başladıktan sonra var olan işletim sistemi ve veri diskleri eşleştirilir. Merhaba geçici diskteki herhangi bir şey kaybolur.

3. Merhaba VM boyutu listelenmeyen isterseniz, toofirst gereken ayırması VM ile Merhaba [az vm serbest bırakma](/cli/azure/vm#deallocate). Bu işlem, bölge destekler hello ve ardından başlatılan yeniden boyutlandırılan tooany boyutu kullanılabilir hello VM toothen sağlar. Merhaba aşağıdaki adımları serbest bırakma, yeniden boyutlandırma ve hello adlı VM Başlat `myVM` adlı hello kaynak grubunda `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Serbest bırakma hello VM toohello VM atanan dinamik IP adreslerini de serbest bırakır. Merhaba işletim sistemi ve veri diskleri etkilenmez.

## <a name="next-steps"></a>Sonraki adımlar
Ek ölçeklenebilirlik için birden çok VM örnekleri çalıştırın ve ölçeğini. Daha fazla bilgi için bkz: [otomatik olarak bir sanal makine ölçek kümesindeki Linux makineler ölçekleme][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
