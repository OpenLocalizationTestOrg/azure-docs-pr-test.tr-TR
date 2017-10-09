---
title: bir Linux VM hello Azure CLI 1.0 ile aaaHow tooresize | Microsoft Docs
description: "Nasıl tooscale yukarı veya aşağı değiştirerek Linux sanal makine ölçek hello VM boyutu."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Bir Linux VM Azure CLI 1.0 ile yeniden boyutlandırın

## <a name="overview"></a>Genel Bakış

Bir sanal makine (VM) sağlama sonra hello VM yukarı veya aşağı hello değiştirerek ölçeklendirmek [VM boyutu][vm-sizes]. Bazı durumlarda, ilk hello VM ayırması gerekir. Merhaba yeni boyutunu hello VM barındırma hello donanım kümede kullanılabilir değilse, bu durum oluşabilir.

Bu makalede gösterilmektedir nasıl hello kullanarak Linux VM bir tooresize [Azure CLI][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](#resize-a-linux-vm) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="resize-a-linux-vm"></a>Bir Linux VM yeniden boyutlandırma
bir VM tooresize hello aşağıdaki adımları gerçekleştirin.

1. CLI komutu aşağıdaki hello çalıştırın. Bu komut hello VM barındırıldığı hello donanım kümede kullanılabilir hello VM boyutları listeler.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. Merhaba boyutu listelenen isterseniz, aşağıdaki komut tooresize hello VM hello çalıştırın.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    Bu işlem sırasında Hello VM yeniden başlatılır. Merhaba yeniden başladıktan sonra var olan işletim sistemi ve veri diskleri yeniden eşlenirken. Merhaba geçici diskteki herhangi bir şey kaybolur.
   
    Kullanım hello `--enable-boot-diagnostics` seçeneği belirlendiğinde [önyükleme tanılama][boot-diagnostics], toolog tüm hataları ilgili toostartup.
3. Hello boyutu listelenmeyen isterseniz, aksi takdirde toodeallocate VM Merhaba, yeniden boyutlandırabilir ve hello VM yeniden başlatma komutlarını aşağıdaki hello çalıştırın.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Serbest bırakma hello VM toohello VM atanan dinamik IP adreslerini de serbest bırakır. Merhaba işletim sistemi ve veri diskleri etkilenmez.
   > 
   > 

## <a name="next-steps"></a>Sonraki adımlar
Ek ölçeklenebilirlik için birden çok VM örnekleri çalıştırın ve ölçeğini. Daha fazla bilgi için bkz: [otomatik olarak bir sanal makine ölçek kümesindeki Linux makineler ölçekleme][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
