---
title: "Bir Linux VM için bir veri diski ekleme | Microsoft Docs"
description: "Bir Linux VM Resource Manager dağıtım modelini kullanarak Azure portalında yeni veya var olan veri diski ekleme yapma."
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
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="fc2a0-103">Nasıl bir Linux VM Azure portalında bir veri diski ekleme</span><span class="sxs-lookup"><span data-stu-id="fc2a0-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="fc2a0-104">Bu makalede Azure portalı üzerinden Linux sanal makine için yeni ve mevcut diskleri ekleme gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="fc2a0-105">Ayrıca [bir Windows VM Azure portalında bir veri diski ekleme](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="fc2a0-106">Azure diskleri yönetilen veya yönetilmeyen diskler kullanmayı da tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="fc2a0-107">Yönetilen diskleri Azure platformu tarafından işlenir ve hazırlık veya konum depolamaya gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="fc2a0-108">Yönetilmeyen diskler bir depolama hesabı gerektirir ve bazı [kotalar ve uygulama sınırlar](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="fc2a0-109">Azure Yönetilen Diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Disklere genel bakış](../windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="fc2a0-110">VM'nize diskleri eklemeden önce bu ipuçlarını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="fc2a0-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="fc2a0-111">Sanal makinenin boyutunu, iliştirebilirsiniz kaç tane veri diskleri denetler.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="fc2a0-112">Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="fc2a0-113">Premium depolama kullanmak için DS serisi veya GS serisi bir sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="fc2a0-114">Bu sanal makinelerle Premium ve standart diskler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="fc2a0-115">Premium depolama belirli bölgelerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="fc2a0-116">Ayrıntılar için bkz [Premium Storage: Azure sanal makine iş yükleri için yüksek performanslı depolama](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="fc2a0-117">Sanal makinelere bağlı diskler Azure'da depolanan gerçekte .vhd dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="fc2a0-118">Ayrıntılar için bkz [diskler ve sanal makineler için VHD'ler hakkında](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="fc2a0-119">Sanal makine bulunamadı</span><span class="sxs-lookup"><span data-stu-id="fc2a0-119">Find the virtual machine</span></span>
1. <span data-ttu-id="fc2a0-120">[Azure Portal](https://portal.azure.com/) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fc2a0-121">Hub menüsünde, **Virtual Machines**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="fc2a0-122">Listeden sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="fc2a0-123">Sanal makineleri dikey penceresinde de **Essentials**, tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Disk Ayarları'nı açın](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="fc2a0-125">Ya da eklemek için aşağıdaki yönergeleri tarafından devam bir [yönetilen disk](#use-azure-managed-disks) veya [yönetilmeyen disk](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="fc2a0-126">Azure yönetilen diskleri kullanın</span><span class="sxs-lookup"><span data-stu-id="fc2a0-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="fc2a0-127">Yeni bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="fc2a0-127">Attach a new disk</span></span>

1. <span data-ttu-id="fc2a0-128">Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="fc2a0-129">Aşağı açılan menüsüne tıklayın **adı** seçip **oluşturma disk**:</span><span class="sxs-lookup"><span data-stu-id="fc2a0-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Azure oluşturmak yönetilen disk](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="fc2a0-131">Yönetilen disk için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="fc2a0-132">Varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="fc2a0-134">Tıklatın **kaydetmek** yönetilen disk oluşturmak ve VM yapılandırmasını güncelleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="fc2a0-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![Yeni Azure diski yönetilen Kaydet](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="fc2a0-136">Azure disk oluşturur ve sanal makineye iliştirir sonra yeni disk sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="fc2a0-137">Yönetilen diskleri en üst düzey bir kaynak olduğundan, diskin kaynak grubu kökünde görünür:</span><span class="sxs-lookup"><span data-stu-id="fc2a0-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![Kaynak grubundaki yönetilen Azure Disk](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="fc2a0-139">Var olan bir diski ekleme</span><span class="sxs-lookup"><span data-stu-id="fc2a0-139">Attach an existing disk</span></span>
1. <span data-ttu-id="fc2a0-140">Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="fc2a0-141">Aşağı açılan menüsüne tıklayın **adı** Azure aboneliğinize erişilebilir olan yönetilen disklerin listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="fc2a0-142">Yönetilen bir disk eklemek için seçin:</span><span class="sxs-lookup"><span data-stu-id="fc2a0-142">Select the managed disk to attach:</span></span>

   ![Yönetilen mevcut Azure diski ekleme](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="fc2a0-144">Tıklatın **kaydetmek** mevcut yönetilen diski ekleyin ve VM yapılandırmasını güncelleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="fc2a0-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Azure yönetilen diski güncelleştirmelerini kaydedin](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="fc2a0-146">Azure disk sanal makineye iliştirir sonra sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="fc2a0-147">Yönetilmeyen diskleri kullanın</span><span class="sxs-lookup"><span data-stu-id="fc2a0-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="fc2a0-148">Yeni bir diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="fc2a0-148">Attach a new disk</span></span>

1. <span data-ttu-id="fc2a0-149">Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="fc2a0-150">Varsayılan ayarları gözden geçirin, gerektiği gibi güncelleştirin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Disk ayarlarını gözden geçirin](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="fc2a0-152">Azure disk oluşturur ve sanal makineye iliştirir sonra yeni disk sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="fc2a0-153">Var olan bir diski ekleme</span><span class="sxs-lookup"><span data-stu-id="fc2a0-153">Attach an existing disk</span></span>
1. <span data-ttu-id="fc2a0-154">Üzerinde **diskleri** dikey penceresinde tıklatın **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="fc2a0-155">Altında **varolan bir diski İlişti**, tıklatın **VHD dosyasını**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Varolan bir diski kullanıma açın](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="fc2a0-157">Altında **depolama hesapları**, .vhd dosyası tutan kapsayıcı ve hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![VHD konumunu bulma](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="fc2a0-159">.Vhd dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="fc2a0-160">Altında **varolan bir diski İlişti**, seçtiğiniz dosya altında listelenen **VHD dosyasını**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="fc2a0-161">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-161">Click **OK**.</span></span>
6. <span data-ttu-id="fc2a0-162">Azure disk sanal makineye iliştirir sonra sanal makinenin disk ayarları altında listelenen **veri diskleri**.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fc2a0-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc2a0-163">Next steps</span></span>
<span data-ttu-id="fc2a0-164">Disk eklendikten sonra kullanım için hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc2a0-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="fc2a0-165">Daha fazla bilgi için bkz: [nasıl yapılır: Linux yeni bir veri diski başlatma](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fc2a0-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
