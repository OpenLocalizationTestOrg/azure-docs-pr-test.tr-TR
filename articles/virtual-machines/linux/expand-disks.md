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
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="165aa-103">Bir Linux VM üzerindeki sanal sabit disklere tooexpand Azure CLI nasıl hello</span><span class="sxs-lookup"><span data-stu-id="165aa-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="165aa-104">Merhaba varsayılan sanal sabit disk boyutu hello işletim sistemi (OS) için azure'da bir Linux sanal makine (VM) genellikle 30 GB açıktır.</span><span class="sxs-lookup"><span data-stu-id="165aa-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="165aa-105">Yapabilecekleriniz [veri diski Ekle](add-disk.md) tooprovide ek depolama alanı, ancak ayrıca istediğiniz tooexpand varolan bir veri diski.</span><span class="sxs-lookup"><span data-stu-id="165aa-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="165aa-106">Bu makalede nasıl tooexpand için bir Linux VM hello Azure CLI 2.0 ile yönetilen disklerde ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="165aa-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="165aa-107">Yönetilmeyen hello işletim sistemi diski hello ile genişletebilirsiniz [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="165aa-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="165aa-108">Her zaman, disk gerçekleştirmeden önce verileri yedekleyin operations yeniden boyutlandırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="165aa-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="165aa-109">Daha fazla bilgi için bkz: [Linux VM'ler için Azure'da yedekleme](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="165aa-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="165aa-110">Disk genişletme</span><span class="sxs-lookup"><span data-stu-id="165aa-110">Expand disk</span></span>
<span data-ttu-id="165aa-111">Merhaba son olduğundan emin olun [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="165aa-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="165aa-112">Bu makalede Azure mevcut bir VM'yi sahip bağlı ve hazırlanan en az bir veri diski gerektirir.</span><span class="sxs-lookup"><span data-stu-id="165aa-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="165aa-113">Kullanabileceğiniz VM zaten yoksa bkz [oluşturma ve veri diskleri içeren bir VM hazırlama](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="165aa-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="165aa-114">Hello aşağıdaki örnekleri, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="165aa-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="165aa-115">Örnek parametre adlarında *myResourceGroup* ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="165aa-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="165aa-116">Sanal sabit diskler üzerinde işlemler hello VM ile gerçekleştirilemiyor çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="165aa-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="165aa-117">VM ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="165aa-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="165aa-118">Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="165aa-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="165aa-119">`az vm stop`Merhaba işlem kaynaklarını serbest değil.</span><span class="sxs-lookup"><span data-stu-id="165aa-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="165aa-120">toorelease işlem kaynaklarını, kullanın `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="165aa-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="165aa-121">Merhaba VM tooexpand hello sanal sabit disk ayırması gerekir.</span><span class="sxs-lookup"><span data-stu-id="165aa-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="165aa-122">Bir kaynak grubu ile yönetilen disklerin listesini görüntülemek [az disk listesi](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="165aa-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="165aa-123">Merhaba aşağıdaki örnek yönetilen disklerin listesini adlı hello kaynak grubunda görüntüler *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="165aa-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="165aa-124">Merhaba gerekli diskle genişletin [az disk güncelleştirme](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="165aa-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="165aa-125">Merhaba aşağıdaki örnek genişletir adlı hello yönetilen disk *myDataDisk* toobe *200*Gb boyutunda:</span><span class="sxs-lookup"><span data-stu-id="165aa-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="165aa-126">Yönetilen bir disk genişlettiğinizde, güncelleştirilmiş hello en yakın yönetilen disk boyutu eşlenen toohello boyutudur.</span><span class="sxs-lookup"><span data-stu-id="165aa-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="165aa-127">Merhaba kullanılabilir yönetilen disk boyutları ve katmanları tablosu için bkz: [Azure yönetilen diskleri fiyatlandırma ve faturalama genel bakış -](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="165aa-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="165aa-128">VM ile başlangıç [az vm başlangıç](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="165aa-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="165aa-129">Örnek başlatır aşağıdaki hello hello adlı VM *myVM* adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="165aa-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="165aa-130">SSH tooyour VM hello uygun kimlik bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="165aa-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="165aa-131">Merhaba, VM ile genel IP adresi elde edebilirsiniz [az vm Göster](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="165aa-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="165aa-132">disk toouse hello genişletilmiş, tooexpand hello altındaki bölüm ve dosya sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="165aa-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="165aa-133">a.</span><span class="sxs-lookup"><span data-stu-id="165aa-133">a.</span></span> <span data-ttu-id="165aa-134">Takılı, hello disk çıkarın:</span><span class="sxs-lookup"><span data-stu-id="165aa-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="165aa-135">b.</span><span class="sxs-lookup"><span data-stu-id="165aa-135">b.</span></span> <span data-ttu-id="165aa-136">Kullanım `parted` tooview disk bilgileri ve hello bölümü yeniden boyutlandırma:</span><span class="sxs-lookup"><span data-stu-id="165aa-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="165aa-137">Merhaba var olan bir bölüm düzeni ile hakkındaki bilgileri görüntüleyin `print`.</span><span class="sxs-lookup"><span data-stu-id="165aa-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="165aa-138">Merhaba, benzer toohello hello temel disk 215 Gb boyutunda gösterilir örnek aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="165aa-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

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

    <span data-ttu-id="165aa-139">c.</span><span class="sxs-lookup"><span data-stu-id="165aa-139">c.</span></span> <span data-ttu-id="165aa-140">Merhaba bölümüyle genişletin `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="165aa-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="165aa-141">Merhaba bölüm numarası girin *1*ve hello yeni bölüm için bir boyut:</span><span class="sxs-lookup"><span data-stu-id="165aa-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="165aa-142">d.</span><span class="sxs-lookup"><span data-stu-id="165aa-142">d.</span></span> <span data-ttu-id="165aa-143">tooexit, girin`quit`</span><span class="sxs-lookup"><span data-stu-id="165aa-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="165aa-144">Yeniden boyutlandırılabilir hello bölümüyle hello bölüm tutarlılığı doğrulamak `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="165aa-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="165aa-145">Şimdi hello dosya sistemi ile yeniden boyutlandırın `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="165aa-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="165aa-146">Bağlama hello bölüm toohello istenen konuma gibi `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="165aa-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="165aa-147">tooverify hello işletim sistemi diski yeniden, kullanın `df -h`.</span><span class="sxs-lookup"><span data-stu-id="165aa-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="165aa-148">örnek çıktı aşağıdaki hello gösterir hello veri sürücüsü */dev/sdc1*, 200 GB sunulmuştur:</span><span class="sxs-lookup"><span data-stu-id="165aa-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="165aa-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="165aa-149">Next steps</span></span>
<span data-ttu-id="165aa-150">Ek depolama alanı, gerekirse, ayrıca [veri diskleri tooa Linux VM eklemek](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="165aa-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="165aa-151">Disk şifrelemesi hakkında daha fazla bilgi için bkz: [kullanarak bir Linux VM şifrele disklerde hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="165aa-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
