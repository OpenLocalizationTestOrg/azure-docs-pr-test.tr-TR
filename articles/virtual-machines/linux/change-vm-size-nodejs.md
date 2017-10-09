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
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="20d1e-103">Bir Linux VM Azure CLI 1.0 ile yeniden boyutlandırın</span><span class="sxs-lookup"><span data-stu-id="20d1e-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="20d1e-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="20d1e-104">Overview</span></span>

<span data-ttu-id="20d1e-105">Bir sanal makine (VM) sağlama sonra hello VM yukarı veya aşağı hello değiştirerek ölçeklendirmek [VM boyutu][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="20d1e-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="20d1e-106">Bazı durumlarda, ilk hello VM ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20d1e-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="20d1e-107">Merhaba yeni boyutunu hello VM barındırma hello donanım kümede kullanılabilir değilse, bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="20d1e-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="20d1e-108">Bu makalede gösterilmektedir nasıl hello kullanarak Linux VM bir tooresize [Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="20d1e-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="20d1e-109">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="20d1e-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="20d1e-110">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="20d1e-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="20d1e-111">[Azure CLI 1.0](#resize-a-linux-vm) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="20d1e-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="20d1e-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="20d1e-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="20d1e-113">Bir Linux VM yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="20d1e-113">Resize a Linux VM</span></span>
<span data-ttu-id="20d1e-114">bir VM tooresize hello aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="20d1e-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="20d1e-115">CLI komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20d1e-115">Run hello following CLI command.</span></span> <span data-ttu-id="20d1e-116">Bu komut hello VM barındırıldığı hello donanım kümede kullanılabilir hello VM boyutları listeler.</span><span class="sxs-lookup"><span data-stu-id="20d1e-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="20d1e-117">Merhaba boyutu listelenen isterseniz, aşağıdaki komut tooresize hello VM hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20d1e-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="20d1e-118">Bu işlem sırasında Hello VM yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="20d1e-118">hello VM will restart during this process.</span></span> <span data-ttu-id="20d1e-119">Merhaba yeniden başladıktan sonra var olan işletim sistemi ve veri diskleri yeniden eşlenirken.</span><span class="sxs-lookup"><span data-stu-id="20d1e-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="20d1e-120">Merhaba geçici diskteki herhangi bir şey kaybolur.</span><span class="sxs-lookup"><span data-stu-id="20d1e-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="20d1e-121">Kullanım hello `--enable-boot-diagnostics` seçeneği belirlendiğinde [önyükleme tanılama][boot-diagnostics], toolog tüm hataları ilgili toostartup.</span><span class="sxs-lookup"><span data-stu-id="20d1e-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="20d1e-122">Hello boyutu listelenmeyen isterseniz, aksi takdirde toodeallocate VM Merhaba, yeniden boyutlandırabilir ve hello VM yeniden başlatma komutlarını aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20d1e-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="20d1e-123">Serbest bırakma hello VM toohello VM atanan dinamik IP adreslerini de serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="20d1e-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="20d1e-124">Merhaba işletim sistemi ve veri diskleri etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="20d1e-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="20d1e-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20d1e-125">Next steps</span></span>
<span data-ttu-id="20d1e-126">Ek ölçeklenebilirlik için birden çok VM örnekleri çalıştırın ve ölçeğini. Daha fazla bilgi için bkz: [otomatik olarak bir sanal makine ölçek kümesindeki Linux makineler ölçekleme][scale-set].</span><span class="sxs-lookup"><span data-stu-id="20d1e-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
