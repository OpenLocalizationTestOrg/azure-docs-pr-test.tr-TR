---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme | Microsoft Docs"
description: "Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="79a69-103">Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="79a69-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="79a69-104">Azure depolama hesabı, kapsayıcı ya da VHD silmeye çalıştığınızda hata alabilirsiniz [Azure portal](https://portal.azure.com/) veya [Klasik Azure portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="79a69-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="79a69-105">Bu sorunlar aşağıdaki durumlarda oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="79a69-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="79a69-106">Bir VM’yi sildiğinizde disk ve VHD otomatik olarak silinmez.</span><span class="sxs-lookup"><span data-stu-id="79a69-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="79a69-107">Depolama hesabını silmede başarısızlık bundan kaynaklanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="79a69-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="79a69-108">Başka bir VM bağlamak için disk kullanabilmeleri biz disk silmeyin.</span><span class="sxs-lookup"><span data-stu-id="79a69-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="79a69-109">Disk veya diskle ilişkili blob üzerinde kiralama hala devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="79a69-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="79a69-110">Hala bir blob, kapsayıcısı veya depolama hesabı kullanarak bir VM görüntüsü yok.</span><span class="sxs-lookup"><span data-stu-id="79a69-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="79a69-111">Bu makalede Azure sorunu ele alınmamışsa Azure forumları ziyaret [MSDN ve yığın taşması](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="79a69-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="79a69-112">Bu forumları veya çok sorununuzu nakledebilirsiniz @AzureSupport Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="79a69-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="79a69-113">Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="79a69-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="79a69-114">Belirtiler</span><span class="sxs-lookup"><span data-stu-id="79a69-114">Symptoms</span></span>
<span data-ttu-id="79a69-115">Aşağıdaki bölümde Azure depolama hesapları, kapsayıcıları veya VHD'leri silmeye çalıştığınızda alabileceğiniz yaygın hataları listeler.</span><span class="sxs-lookup"><span data-stu-id="79a69-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="79a69-116">Senaryo 1: Depolama hesabı silinemedi</span><span class="sxs-lookup"><span data-stu-id="79a69-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="79a69-117">Klasik depolama hesabına gidin zaman [Azure portal](https://portal.azure.com/) seçip **silmek**, depolama hesabı silinmesini engelliyor nesnelerin bir listesini sunulan:</span><span class="sxs-lookup"><span data-stu-id="79a69-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Hata görüntüsü zaman depolama hesabını silme](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="79a69-119">Depolama hesabına gidin zaman [Klasik Azure portalı](https://manage.windowsazure.com/) seçip **silmek**, aşağıdaki hatalardan birini görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="79a69-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="79a69-120">*Depolama hesabı StorageAccountName VM görüntüleri içeriyor. Bu depolama hesabını silmeden önce bu VM görüntülerinin kaldırıldığından emin olun.*</span><span class="sxs-lookup"><span data-stu-id="79a69-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="79a69-121">*Depolama hesabı < vm-storage-account-name > silinemedi. Depolama hesabı < vm-storage-account-name > silinemiyor: ' < vm-storage-account-name > depolama hesabı bazı etkin görüntülere ve/veya disklerin sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.'.*</span><span class="sxs-lookup"><span data-stu-id="79a69-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="79a69-122">*Depolama hesabı < vm-storage-account-name > bazı etkin görüntülere ve/veya disklerin, örneğin xxxxxxxxx-xxxxxxxxx-O-209490240936090599 sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.*</span><span class="sxs-lookup"><span data-stu-id="79a69-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="79a69-123">*Depolama hesabı < vm-storage-account-name > etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından sahiptir. Bu depolama hesabını silmeden önce bu yapıların görüntü deposundan kaldırıldığından emin olmak*.</span><span class="sxs-lookup"><span data-stu-id="79a69-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="79a69-124">*Etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından başarısız depolama hesabının < vm-storage-account-name > sahip gönderin. Bu depolama hesabını silmeden önce bu yapıların görüntü deposundan kaldırıldığından emin olun. Bir depolama hesabı silme girişimi ve onunla ilişkili hala etkin disk olduğunda silinmesi gereken etkin disk söyleyen bir ileti görürsünüz*.</span><span class="sxs-lookup"><span data-stu-id="79a69-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="79a69-125">2. Senaryo: Bir kapsayıcı silinemedi</span><span class="sxs-lookup"><span data-stu-id="79a69-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="79a69-126">Depolama kapsayıcısı silmeye çalıştığınızda, aşağıdaki hatayı görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="79a69-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="79a69-127">*Depolama kapsayıcısı silinemedi <container name>. Hata: ' kapsayıcısı üzerinde şu anda bir kira yoktur ve hiçbir kiralama kimliği istekte belirtilen*.</span><span class="sxs-lookup"><span data-stu-id="79a69-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="79a69-128">Veya</span><span class="sxs-lookup"><span data-stu-id="79a69-128">Or</span></span>

<span data-ttu-id="79a69-129">*Kapsayıcı silinemez aşağıdaki sanal makine disklerini BLOB'ları bu kapsayıcıda kullanın: VirtualMachineDiskName1, VirtualMachineDiskName2,...*</span><span class="sxs-lookup"><span data-stu-id="79a69-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="79a69-130">Senaryo 3: Bir VHD silinemiyor</span><span class="sxs-lookup"><span data-stu-id="79a69-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="79a69-131">Bir VM silin ve ardından BLOB'lar için ilişkili VHD'leri silmeyi deneyin sonra aşağıdaki iletiyi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="79a69-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="79a69-132">*BLOB silinemedi ' yolu/XXXXXX-XXXXXX-os-1447379084699.vhd'. Hata: ' blob üzerindeki şu anda bir kira yoktur ve istekte hiçbir kiralama kimliği belirtildi.*</span><span class="sxs-lookup"><span data-stu-id="79a69-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="79a69-133">Veya</span><span class="sxs-lookup"><span data-stu-id="79a69-133">Or</span></span>

<span data-ttu-id="79a69-134">*Blob silinemez blob 'BlobName.vhd' sanal makine diski 'VirtualMachineDiskName' olarak kullanılıyor.*</span><span class="sxs-lookup"><span data-stu-id="79a69-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="79a69-135">Çözüm</span><span class="sxs-lookup"><span data-stu-id="79a69-135">Solution</span></span>
<span data-ttu-id="79a69-136">En sık karşılaşılan sorunları gidermek için aşağıdaki yöntemi deneyin:</span><span class="sxs-lookup"><span data-stu-id="79a69-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="79a69-137">1. adım: depolama hesabı, kapsayıcısı veya VHD silinmesini engelliyor diskler Sil</span><span class="sxs-lookup"><span data-stu-id="79a69-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="79a69-138">Geçiş [Klasik Azure portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="79a69-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="79a69-139">Seçin **sanal makine** > **DİSKLERİ**.</span><span class="sxs-lookup"><span data-stu-id="79a69-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Klasik Azure portalı sanal makinelerde disklerde görüntüsü.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="79a69-141">Silmek istediğiniz depolama hesabı, kapsayıcı ya da VHD ile ilişkilendirilmiş diskleri bulun.</span><span class="sxs-lookup"><span data-stu-id="79a69-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="79a69-142">Disklerin konumunu denetlediğinizde, ilişkili olduğu depolama hesabı, kapsayıcı veya VHD’yi bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="79a69-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Konum bilgileri diskler için Azure Klasik portalında gösteren resim](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="79a69-144">Aşağıdaki yöntemlerden birini kullanarak diskleri silin:</span><span class="sxs-lookup"><span data-stu-id="79a69-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="79a69-145">Hiçbir VM varsa listelenen **bağlı** alan diskin, disk doğrudan silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79a69-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="79a69-146">Disk bir veri diski ise, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="79a69-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="79a69-147">Diski bağlı VM adını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="79a69-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="79a69-148">Git **sanal makineleri** > **örnekleri**ve ardından VM bulun.</span><span class="sxs-lookup"><span data-stu-id="79a69-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="79a69-149">Hiçbir şey etkin olarak disk kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="79a69-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="79a69-150">Seçin **diski Ayır** diski kullanımdan çıkarmak için portalın altındaki.</span><span class="sxs-lookup"><span data-stu-id="79a69-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="79a69-151">Git **sanal makineleri** > **diskleri**ve bekleyin **bağlı** boş açmak için alan.</span><span class="sxs-lookup"><span data-stu-id="79a69-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="79a69-152">Bu diski sanal makineden başarıyla ayrıldı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="79a69-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="79a69-153">Seçin **silmek** alt kısmındaki **sanal makineleri** > **diskleri** disk silmek için.</span><span class="sxs-lookup"><span data-stu-id="79a69-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="79a69-154">Disk bir işletim sistemi diski ise ( **içeren işletim sistemi** alanı, Windows gibi bir değer içeriyor) ve bir VM'ye bağlı, VM silmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="79a69-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="79a69-155">İşletim sistemi diski ayrılamıyor, bu nedenle biz kira serbest bırakmak için VM silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="79a69-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="79a69-156">Veri diski bağlı sanal makine adını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="79a69-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="79a69-157">Git **sanal makineleri** > **örnekleri**ve ardından diski bağlı VM seçin.</span><span class="sxs-lookup"><span data-stu-id="79a69-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="79a69-158">Hiçbir şey etkin olarak sanal makinenin kullandığından emin olun ve sanal makine artık gerekir.</span><span class="sxs-lookup"><span data-stu-id="79a69-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="79a69-159">Disk VM eklendiği, ardından seçin **silmek** > **ekli disklerini silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="79a69-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="79a69-160">Git **sanal makineleri** > **diskleri**ve disk kayboluyor bekleyin.</span><span class="sxs-lookup"><span data-stu-id="79a69-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="79a69-161">Bunun gerçekleşmesi birkaç dakika sürebilir ve sayfayı yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="79a69-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="79a69-162">Disk kayboluyor değil, bekleyin **bağlı** boş açmak için alan.</span><span class="sxs-lookup"><span data-stu-id="79a69-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="79a69-163">Bu diski sanal makineden tam olarak ayrılmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="79a69-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="79a69-164">Sonra disk seçin ve Seç **silmek** disk silmek için sayfanın altındaki.</span><span class="sxs-lookup"><span data-stu-id="79a69-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="79a69-165">Bir VM'ye bir disk bağlıysa silmek mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="79a69-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="79a69-166">Diskleri silinmiş bir VM'den zaman uyumsuz olarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="79a69-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="79a69-167">VM temizlemek Bu alan için silindikten sonra birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="79a69-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="79a69-168">2. adım: depolama hesabı veya kapsayıcı silinmesine engelleyen tüm VM görüntüleri silin</span><span class="sxs-lookup"><span data-stu-id="79a69-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="79a69-169">Geçiş [Klasik Azure portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="79a69-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="79a69-170">Seçin **sanal makine** > **GÖRÜNTÜLERİ**ve ardından depolama hesabı, kapsayıcısı veya VHD ile ilişkilendirilmiş görüntüleri silin.</span><span class="sxs-lookup"><span data-stu-id="79a69-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="79a69-171">Bundan sonra depolama hesabı, kapsayıcısı veya VHD silmeyi tekrar deneyin.</span><span class="sxs-lookup"><span data-stu-id="79a69-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="79a69-172">Hesabı silmeden önce kaydetmek istediğiniz şeyleri yedeklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="79a69-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="79a69-173">VHD, blob, tablo, kuyruk veya dosya sildiğinizde, kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="79a69-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="79a69-174">Kaynak kullanımda olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="79a69-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="79a69-175">Durduruldu (serbest bırakıldı) durumu hakkında</span><span class="sxs-lookup"><span data-stu-id="79a69-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="79a69-176">Klasik dağıtım modelinde oluşturulmuş ve, korundu VM'ler olacaktır **durduruldu (serbest bırakıldı)** ya da durum [Azure portal](https://portal.azure.com/) veya [Klasik Azure portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="79a69-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="79a69-177">**Klasik Azure portalı**:</span><span class="sxs-lookup"><span data-stu-id="79a69-177">**Azure classic portal**:</span></span>

![(Deallocated) durum VM'ler için Azure Portal'da durduruldu.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="79a69-179">**Azure portal**:</span><span class="sxs-lookup"><span data-stu-id="79a69-179">**Azure portal**:</span></span>

![Durduruldu (serbest bırakıldığında) durum VM'ler için Klasik Azure portalı.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="79a69-181">"Durduruldu (serbest bırakıldı)" durumu CPU, bellek ve ağ gibi bilgisayar kaynaklarını serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="79a69-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="79a69-182">Böylece, hızlı bir şekilde VM gerekirse yeniden oluşturabilirsiniz diskleri ancak hala korunur.</span><span class="sxs-lookup"><span data-stu-id="79a69-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="79a69-183">Bu diskleri Azure Depolama tarafından yedeklenen VHD'ler üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="79a69-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="79a69-184">Depolama hesabı bu VHD ve diskleri kiraları bu VHD'lerde sahip.</span><span class="sxs-lookup"><span data-stu-id="79a69-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79a69-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="79a69-185">Next steps</span></span>
* [<span data-ttu-id="79a69-186">Bir depolama hesabını silme</span><span class="sxs-lookup"><span data-stu-id="79a69-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
