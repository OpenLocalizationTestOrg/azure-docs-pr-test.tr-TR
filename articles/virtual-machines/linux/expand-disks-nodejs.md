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
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="fb258-103">Azure CLI 1.0 hello ile hello Azure CLI kullanarak bir Linux VM üzerindeki işletim sistemi diski genişletin</span><span class="sxs-lookup"><span data-stu-id="fb258-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="fb258-104">Merhaba varsayılan sanal sabit disk boyutu hello işletim sistemi (OS) için azure'da bir Linux sanal makine (VM) genellikle 30 GB açıktır.</span><span class="sxs-lookup"><span data-stu-id="fb258-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="fb258-105">Yapabilecekleriniz [veri diski Ekle](add-disk.md) tooprovide ek depolama alanı, ancak tooexpand hello işletim sistemi diski de istiyor.</span><span class="sxs-lookup"><span data-stu-id="fb258-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="fb258-106">Bu makalede nasıl tooexpand hello işletim sistemi disk hello Azure CLI 1.0 ile yönetilmeyen diskleri kullanarak bir Linux VM için ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fb258-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="fb258-107">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="fb258-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="fb258-108">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="fb258-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="fb258-109">[Azure CLI 1.0](#prerequisites) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="fb258-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fb258-110">[Azure CLI 2.0](expand-disks.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="fb258-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb258-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fb258-111">Prerequisites</span></span>
<span data-ttu-id="fb258-112">Merhaba gereksinim [en son Azure CLI 1.0](../../cli-install-nodejs.md) yüklü ve tooan içinde günlüğe [Azure hesabı](https://azure.microsoft.com/pricing/free-trial/) hello Resource Manager modunu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="fb258-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="fb258-113">Hello aşağıdaki örnekleri, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fb258-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fb258-114">Örnek parametre adlarında *myResourceGroup* ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fb258-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="fb258-115">İşletim sistemi diskini genişletme</span><span class="sxs-lookup"><span data-stu-id="fb258-115">Expand OS disk</span></span>

1. <span data-ttu-id="fb258-116">Sanal sabit diskler üzerinde işlemler hello VM ile gerçekleştirilemiyor çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="fb258-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="fb258-117">Merhaba aşağıdaki örnek durdurur ve hello adlı VM kaldırır *myVM* adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fb258-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="fb258-118">`azure vm stop`Merhaba işlem kaynaklarını serbest değil.</span><span class="sxs-lookup"><span data-stu-id="fb258-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="fb258-119">toorelease işlem kaynaklarını, kullanın `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="fb258-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="fb258-120">Merhaba VM tooexpand hello sanal sabit disk ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb258-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="fb258-121">Yönetilmeyen hello işletim sistemi diski hello kullanarak Hello boyutunu güncelleştirme `azure vm set` komutu.</span><span class="sxs-lookup"><span data-stu-id="fb258-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="fb258-122">Şu örnek güncelleştirmeleri hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup* toobe *50* GB:</span><span class="sxs-lookup"><span data-stu-id="fb258-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="fb258-123">VM şu şekilde başlatın:</span><span class="sxs-lookup"><span data-stu-id="fb258-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="fb258-124">SSH tooyour VM hello uygun kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="fb258-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="fb258-125">tooverify hello işletim sistemi diski yeniden, kullanın `df -h`.</span><span class="sxs-lookup"><span data-stu-id="fb258-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="fb258-126">örnek çıktı aşağıdaki hello hello birincil bölüm gösterir (*/dev/sda1*) 50 GB sunulmuştur:</span><span class="sxs-lookup"><span data-stu-id="fb258-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="fb258-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb258-127">Next steps</span></span>
<span data-ttu-id="fb258-128">Ek depolama alanı, gerekirse, ayrıca [veri diskleri tooa Linux VM eklemek](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fb258-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="fb258-129">Disk şifrelemesi hakkında daha fazla bilgi için bkz: [kullanarak bir Linux VM şifrele disklerde hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="fb258-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
