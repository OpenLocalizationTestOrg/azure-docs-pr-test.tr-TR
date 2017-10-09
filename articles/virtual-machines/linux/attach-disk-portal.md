---
title: bir veri diski tooa Linux VM aaaAttach | Microsoft Docs
description: "Nasıl tooattach yeni veya var olan veri diski tooa Linux VM Azure portal kullanarak hello Resource Manager dağıtım modeli hello."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="3b06c-103">Nasıl tooattach bir veri diski hello Azure portal'ın tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="3b06c-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="3b06c-104">Bu makalede nasıl tooattach hem yeni hem de mevcut hello Azure portal aracılığıyla tooa Linux sanal makine disklerini gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3b06c-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="3b06c-105">Ayrıca [hello Azure portal'ın bir veri diski tooa Windows VM ekleme](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b06c-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3b06c-106">Toouse yönetilen ya da Azure diskleri seçin veya yönetilmeyen diskler.</span><span class="sxs-lookup"><span data-stu-id="3b06c-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="3b06c-107">Yönetilen diskleri hello Azure platformu tarafından işlenir ve hazırlık veya konumu toostore gerektirmeyen bunları.</span><span class="sxs-lookup"><span data-stu-id="3b06c-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="3b06c-108">Yönetilmeyen diskler bir depolama hesabı gerektirir ve bazı [kotalar ve uygulama sınırlar](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="3b06c-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="3b06c-109">Azure Yönetilen Diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b06c-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="3b06c-110">Diskleri tooyour VM eklemeden önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="3b06c-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="3b06c-111">Merhaba boyutunu hello sanal makine, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="3b06c-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="3b06c-112">Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b06c-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="3b06c-113">Premium depolama toouse, DS serisi veya GS serisi bir sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="3b06c-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="3b06c-114">Bu sanal makinelerle Premium ve standart diskler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b06c-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="3b06c-115">Premium depolama belirli bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3b06c-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="3b06c-116">Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b06c-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="3b06c-117">Diskleri ekli toovirtual makineleri Azure'da depolanan gerçekte .vhd dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="3b06c-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="3b06c-118">Ayrıntılar için bkz [diskler ve sanal makineler için VHD'ler hakkında](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b06c-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="3b06c-119">Merhaba sanal makine bulunamadı</span><span class="sxs-lookup"><span data-stu-id="3b06c-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="3b06c-120">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3b06c-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3b06c-121">Merhaba Hub menüsünde **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="3b06c-122">Merhaba sanal makine hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="3b06c-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="3b06c-123">toohello sanal makineleri dikey penceresinde de **Essentials**, tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Disk Ayarları'nı açın](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="3b06c-125">Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yönetilen disk](#use-azure-managed-disks) veya [yönetilmeyen disk](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="3b06c-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="3b06c-126">Azure yönetilen diskleri kullanın</span><span class="sxs-lookup"><span data-stu-id="3b06c-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="3b06c-127">Yeni bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="3b06c-127">Attach a new disk</span></span>

1. <span data-ttu-id="3b06c-128">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="3b06c-129">Merhaba açılan menüsüne tıklayın **adı** seçip **oluşturma disk**:</span><span class="sxs-lookup"><span data-stu-id="3b06c-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Azure oluşturmak yönetilen disk](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="3b06c-131">Yönetilen disk için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="3b06c-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="3b06c-132">Merhaba varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="3b06c-134">Tıklatın **kaydetmek** toocreate hello yönetilen disk ve güncelleştirme hello VM yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="3b06c-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Yeni Azure diski yönetilen Kaydet](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="3b06c-136">Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="3b06c-137">Yönetilen diskleri en üst düzey bir kaynak olduğundan, hello disk hello hello kaynak grubu kökünde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="3b06c-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Kaynak grubundaki yönetilen Azure Disk](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="3b06c-139">Var olan bir diski ekleme</span><span class="sxs-lookup"><span data-stu-id="3b06c-139">Attach an existing disk</span></span>
1. <span data-ttu-id="3b06c-140">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="3b06c-141">Merhaba açılan menüsüne tıklayın **adı** tooview varolan listesini yönetilen diskleri erişilebilir tooyour Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="3b06c-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="3b06c-142">Select hello disk tooattach yönetilen:</span><span class="sxs-lookup"><span data-stu-id="3b06c-142">Select hello managed disk tooattach:</span></span>

   ![Yönetilen mevcut Azure diski ekleme](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="3b06c-144">Tıklatın **kaydetmek** tooattach hello varolan yönetilen disk ve güncelleştirme hello VM yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="3b06c-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Azure yönetilen diski güncelleştirmelerini kaydedin](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="3b06c-146">Disk toohello sanal makine Azure ekler hello sonra hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="3b06c-147">Yönetilmeyen diskleri kullanın</span><span class="sxs-lookup"><span data-stu-id="3b06c-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="3b06c-148">Yeni bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="3b06c-148">Attach a new disk</span></span>

1. <span data-ttu-id="3b06c-149">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="3b06c-150">Merhaba varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="3b06c-152">Azure hello disk oluşturur ve toohello sanal makineye iliştirir sonra hello yeni disk hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="3b06c-153">Var olan bir diski ekleme</span><span class="sxs-lookup"><span data-stu-id="3b06c-153">Attach an existing disk</span></span>
1. <span data-ttu-id="3b06c-154">Merhaba üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="3b06c-155">Altında **varolan bir diski İlişti**, tıklatın **VHD dosyasını**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Varolan bir diski kullanıma açın](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="3b06c-157">Altında **depolama hesapları**, hello hesabınızı ve hello .vhd dosyası tutan kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="3b06c-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![VHD konumunu bulma](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="3b06c-159">Merhaba .vhd dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="3b06c-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="3b06c-160">Altında **varolan bir diski İlişti**, seçtiğiniz hello dosya altında listelenen **VHD dosyasını**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="3b06c-161">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3b06c-161">Click **OK**.</span></span>
6. <span data-ttu-id="3b06c-162">Disk toohello sanal makine Azure ekler hello sonra hello sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="3b06c-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3b06c-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3b06c-163">Next steps</span></span>
<span data-ttu-id="3b06c-164">Merhaba disk eklendikten sonra tooprepare gereksinim için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b06c-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="3b06c-165">Daha fazla bilgi için bkz: [nasıl yapılır: Linux yeni bir veri diski başlatma](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="3b06c-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
