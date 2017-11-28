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
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="37438-103">Linux sanal makine yönetilmeyen diskleri toomanaged disklerden Dönüştür</span><span class="sxs-lookup"><span data-stu-id="37438-103">Convert a Linux virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="37438-104">Yönetilmeyen diskleri kullanan bir varolan Linux sanal makineleri (VM'ler) varsa, hello aracılığıyla hello VM'ler yönetilen toouse diskler dönüştürülebilir [Azure yönetilen diskleri](../windows/managed-disks-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="37438-104">If you have existing Linux virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](../windows/managed-disks-overview.md) service.</span></span> <span data-ttu-id="37438-105">Bu işlem hello işletim sistemi disk ve tüm eklenen veri disklerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="37438-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="37438-106">Bu makalede, Azure CLI kullanarak sanal makineleri tooconvert hello nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="37438-106">This article shows you how tooconvert VMs by using hello Azure CLI.</span></span> <span data-ttu-id="37438-107">Yükseltmek veya tooinstall gerekir, bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="37438-107">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="37438-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="37438-108">Before you begin</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a><span data-ttu-id="37438-109">Tek Örnekli VM'ler Dönüştür</span><span class="sxs-lookup"><span data-stu-id="37438-109">Convert single-instance VMs</span></span>
<span data-ttu-id="37438-110">Bu bölüm, nasıl tooconvert Tek Örnekli yönetilmeyenden Azure VM'ler toomanaged diskleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="37438-110">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="37438-111">(Bir kullanılabilirlik kümesine Vm'leriniz varsa hello sonraki bölüme bakın.) Bu işlem tooconvert hello yönetilmeyen VM'ler yönetilmeyen premium (SSD) diskleri yönetilen toopremium diskleri veya standart (HDD) diskleri yönetilen toostandard diskleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="37438-111">(If your VMs are in an availability set, see hello next section.) You can use this process tooconvert hello VMs from premium (SSD) unmanaged disks toopremium managed disks, or from standard (HDD) unmanaged disks toostandard managed disks.</span></span>

1. <span data-ttu-id="37438-112">Kullanarak Hello VM serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="37438-112">Deallocate hello VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="37438-113">Merhaba aşağıdaki örnek kaldırır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37438-113">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. <span data-ttu-id="37438-114">Merhaba VM toomanaged diskleri kullanarak dönüştürme [az vm dönüştürme](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="37438-114">Convert hello VM toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="37438-115">işlem dönüştürür aşağıdaki hello hello adlı VM `myVM`hello işletim sistemi diski ve veri diskleri dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="37438-115">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="37438-116">Merhaba VM hello dönüştürme toomanaged diskleri sonra başlamayı [az vm başlangıç](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="37438-116">Start hello VM after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="37438-117">Örnek başlatır aşağıdaki hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="37438-117">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="37438-118">Sanal makineleri bir kullanılabilirlik kümesine Dönüştür</span><span class="sxs-lookup"><span data-stu-id="37438-118">Convert VMs in an availability set</span></span>

<span data-ttu-id="37438-119">Tooconvert toomanaged disklerdir bir kullanılabilirlik kümesinde istediğiniz hello VM'ler, ilk tooconvert hello kullanılabilirlik kümesi tooa yönetilen ihtiyacınız varsa kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="37438-119">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

<span data-ttu-id="37438-120">Merhaba kullanılabilirlik kümesi dönüştürmeden önce hello kullanılabilirlik kümesindeki tüm VM'ler serbest gerekir.</span><span class="sxs-lookup"><span data-stu-id="37438-120">All VMs in hello availability set must be deallocated before you convert hello availability set.</span></span> <span data-ttu-id="37438-121">Tüm sanal makineleri toomanaged diskleri hello kullanılabilirlik sonra kendisini ayarlamak planı tooconvert yönetilen dönüştürülmüş tooa kullanılabilirlik kümesi olmuştur.</span><span class="sxs-lookup"><span data-stu-id="37438-121">Plan tooconvert all VMs toomanaged disks after hello availability set itself has been converted tooa managed availability set.</span></span> <span data-ttu-id="37438-122">Ardından, tüm hello VM'ler başlatın ve normal olarak çalışmaya devam.</span><span class="sxs-lookup"><span data-stu-id="37438-122">Then, start all hello VMs and continue operating as normal.</span></span>

1. <span data-ttu-id="37438-123">Kullanılabilirlik kümesi kullanarak tüm sanal makineleri listesinde [az vm kullanılabilirlik kümesi listesi](/cli/azure/vm/availability-set#list).</span><span class="sxs-lookup"><span data-stu-id="37438-123">List all VMs in an availability set by using [az vm availability-set list](/cli/azure/vm/availability-set#list).</span></span> <span data-ttu-id="37438-124">Merhaba aşağıdaki örnekte tüm VM'ler hello kullanılabilirlik adlandırılmış kümesi içinde listelenmiştir `myAvailabilitySet` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37438-124">hello following example lists all VMs in hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. <span data-ttu-id="37438-125">Kullanarak tüm hello VM'ler ayırması [az vm serbest bırakma](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="37438-125">Deallocate all hello VMs by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="37438-126">Merhaba aşağıdaki örnek kaldırır hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37438-126">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. <span data-ttu-id="37438-127">Merhaba kullanılabilirlik kullanarak kümesi Dönüştür [az vm kullanılabilirlik kümesi dönüştürme](/cli/azure/vm/availability-set#convert).</span><span class="sxs-lookup"><span data-stu-id="37438-127">Convert hello availability set by using [az vm availability-set convert](/cli/azure/vm/availability-set#convert).</span></span> <span data-ttu-id="37438-128">Merhaba aşağıdaki örnek dönüştürür hello kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37438-128">hello following example converts hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. <span data-ttu-id="37438-129">Kullanarak tüm hello VM'ler toomanaged diskleri dönüştürme [az vm dönüştürme](/cli/azure/vm#convert).</span><span class="sxs-lookup"><span data-stu-id="37438-129">Convert all hello VMs toomanaged disks by using [az vm convert](/cli/azure/vm#convert).</span></span> <span data-ttu-id="37438-130">işlem dönüştürür aşağıdaki hello hello adlı VM `myVM`hello işletim sistemi diski ve veri diskleri dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="37438-130">hello following process converts hello VM named `myVM`, including hello OS disk and any data disks:</span></span>

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. <span data-ttu-id="37438-131">Tüm hello VM'ler hello dönüştürme toomanaged diskleri sonra başlamayı [az vm başlangıç](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="37438-131">Start all hello VMs after hello conversion toomanaged disks by using [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="37438-132">Örnek başlatır aşağıdaki hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="37438-132">hello following example starts hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="37438-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37438-133">Next steps</span></span>
<span data-ttu-id="37438-134">Depolama seçenekleri hakkında daha fazla bilgi için bkz: [Azure yönetilen diskleri genel bakış](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37438-134">For more information about storage options, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>
