---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme aaaTroubleshoot | Microsoft Docs"
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
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="65895-103">Azure depolama hesapları, kapsayıcıları veya VHD'leri klasik bir dağıtımda silme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="65895-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="65895-104">Hello toodelete hello Azure depolama hesabı, kapsayıcısı veya VHD çalıştığınızda hata alabilirsiniz [Azure portal](https://portal.azure.com/) veya hello [Klasik Azure portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="65895-104">You might receive errors when you try toodelete hello Azure storage account, container, or VHD in hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="65895-105">Merhaba sorunları koşullar aşağıdaki hello tarafından kaynaklanabilir:</span><span class="sxs-lookup"><span data-stu-id="65895-105">hello issues can be caused by hello following circumstances:</span></span>

* <span data-ttu-id="65895-106">Bir VM sildiğinizde, hello disk ve VHD otomatik olarak silinmez.</span><span class="sxs-lookup"><span data-stu-id="65895-106">When you delete a VM, hello disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="65895-107">Bu depolama hesabı silme hatası hello neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="65895-107">That might be hello reason for failure on storage account deletion.</span></span> <span data-ttu-id="65895-108">Başka bir VM hello disk toomount kullanabilmesi biz hello disk silmeyin.</span><span class="sxs-lookup"><span data-stu-id="65895-108">We don't delete hello disk so that you can use hello disk toomount another VM.</span></span>
* <span data-ttu-id="65895-109">Olduğundan hala bir kira hello diskle ilişkili bir disk veya hello blob.</span><span class="sxs-lookup"><span data-stu-id="65895-109">There is still a lease on a disk or hello blob that's associated with hello disk.</span></span>
* <span data-ttu-id="65895-110">Hala bir blob, kapsayıcısı veya depolama hesabı kullanarak bir VM görüntüsü yok.</span><span class="sxs-lookup"><span data-stu-id="65895-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="65895-111">Bu makalede Azure sorunu ele alınmamışsa ziyaret üzerinde Azure forumları hello [MSDN ve yığın taşması hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="65895-111">If your Azure issue is not addressed in this article, visit hello Azure forums on [MSDN and hello Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="65895-112">Bu forumlar sorununuzu nakledebilirsiniz veya too@AzureSupport Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="65895-112">You can post your issue on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="65895-113">Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="65895-113">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="65895-114">Belirtiler</span><span class="sxs-lookup"><span data-stu-id="65895-114">Symptoms</span></span>
<span data-ttu-id="65895-115">bölümden hello toodelete hello Azure depolama hesapları, kapsayıcıları veya VHD'leri çalıştığınızda alabileceğiniz yaygın hataları listeler.</span><span class="sxs-lookup"><span data-stu-id="65895-115">hello following section lists common errors that you might receive when you try toodelete hello Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-toodelete-a-storage-account"></a><span data-ttu-id="65895-116">Senaryo 1: Oluşturulamıyor toodelete bir depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="65895-116">Scenario 1: Unable toodelete a storage account</span></span>
<span data-ttu-id="65895-117">Merhaba toohello Klasik depolama hesabında gidin zaman [Azure portal](https://portal.azure.com/) seçip **silmek**, hello depolama hesabı silinmesini engelliyor nesnelerin bir listesini sunulan:</span><span class="sxs-lookup"><span data-stu-id="65895-117">When you navigate toohello classic storage account in hello [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of hello storage account:</span></span>

  ![Hata görüntüsü zaman hello depolama hesabını silme](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="65895-119">Merhaba toohello depolama hesabında gidin zaman [Klasik Azure portalı](https://manage.windowsazure.com/) seçip **silmek**, aşağıdaki hatalar hello birini görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65895-119">When you navigate toohello storage account in hello [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of hello following errors:</span></span>

- <span data-ttu-id="65895-120">*Depolama hesabı StorageAccountName VM görüntüleri içeriyor. Bu depolama hesabını silmeden önce bu VM görüntülerinin kaldırıldığından emin olun.*</span><span class="sxs-lookup"><span data-stu-id="65895-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="65895-121">*Toodelete depolama hesabı < vm-storage-account-name > başarısız oldu. %S toodelete depolama hesabı < vm-storage-hesap-adı >: ' < vm-storage-account-name > depolama hesabı bazı etkin görüntülere ve/veya disklerin sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.'.*</span><span class="sxs-lookup"><span data-stu-id="65895-121">*Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="65895-122">*Depolama hesabı < vm-storage-account-name > bazı etkin görüntülere ve/veya disklerin, örneğin xxxxxxxxx-xxxxxxxxx-O-209490240936090599 sahiptir. Bu görüntülerin ve/veya diskleri bu depolama hesabını silmeden önce kaldırıldığından emin olun.*</span><span class="sxs-lookup"><span data-stu-id="65895-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="65895-123">*Depolama hesabı < vm-storage-account-name > etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından sahiptir. Bu depolama hesabını silmeden önce bu yapıların hello görüntü deposundan kaldırıldığından emin olmak*.</span><span class="sxs-lookup"><span data-stu-id="65895-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="65895-124">*Etkin bir görüntü ve/veya disk yapıları olan 1 kaldırıldığından başarısız depolama hesabının < vm-storage-account-name > sahip gönderin. Bu depolama hesabını silmeden önce yapıların hello görüntü deposundan kaldırıldığından emin olun. Toodelete bir depolama hesabı dener ve onunla ilişkili hala etkin disk olduğunda silinmiş toobe gereken etkin disk söyleyen bir ileti görürsünüz*.</span><span class="sxs-lookup"><span data-stu-id="65895-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from hello image repository before deleting this storage account. When you attempt toodelete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need toobe deleted*.</span></span>

### <a name="scenario-2-unable-toodelete-a-container"></a><span data-ttu-id="65895-125">Senaryo 2: Oluşturulamıyor toodelete bir kapsayıcı</span><span class="sxs-lookup"><span data-stu-id="65895-125">Scenario 2: Unable toodelete a container</span></span>
<span data-ttu-id="65895-126">Toodelete hello depolama kapsayıcısı denediğinizde aşağıdaki hata hello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65895-126">When you try toodelete hello storage container, you might see hello following error:</span></span>

<span data-ttu-id="65895-127">*Başarısız toodelete depolama kapsayıcısı <container name>. Hata: ' hello kapsayıcısı üzerinde şu anda bir kira yoktur ve hiçbir kiralama kimliği hello istekte belirtilen*.</span><span class="sxs-lookup"><span data-stu-id="65895-127">*Failed toodelete storage container <container name>. Error: 'There is currently a lease on hello container and no lease ID was specified in hello request*.</span></span>

<span data-ttu-id="65895-128">Veya</span><span class="sxs-lookup"><span data-stu-id="65895-128">Or</span></span>

<span data-ttu-id="65895-129">*sanal makine disklerini aşağıdaki hello hello kapsayıcı silinemez bu kapsayıcıdaki blobları kullanın: VirtualMachineDiskName1, VirtualMachineDiskName2,...*</span><span class="sxs-lookup"><span data-stu-id="65895-129">*hello following virtual machine disks use blobs in this container, so hello container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-toodelete-a-vhd"></a><span data-ttu-id="65895-130">Senaryo 3: Oluşturulamıyor toodelete VHD</span><span class="sxs-lookup"><span data-stu-id="65895-130">Scenario 3: Unable toodelete a VHD</span></span>
<span data-ttu-id="65895-131">Bir VM silin ve ardından VHD try toodelete hello BLOB'lar hello için ilişkilendirilmiş sonra iletiden hello alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65895-131">After you delete a VM and then try toodelete hello blobs for hello associated VHDs, you might receive hello following message:</span></span>

<span data-ttu-id="65895-132">*Başarısız toodelete blob ' yolu/XXXXXX-XXXXXX-os-1447379084699.vhd'. Hata: ' hello blob üzerinde şu anda bir kira yoktur ve hiçbir kiralama kimliği hello istekte belirtildi.*</span><span class="sxs-lookup"><span data-stu-id="65895-132">*Failed toodelete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on hello blob and no lease ID was specified in hello request.*</span></span>

<span data-ttu-id="65895-133">Veya</span><span class="sxs-lookup"><span data-stu-id="65895-133">Or</span></span>

<span data-ttu-id="65895-134">*Merhaba blob silinemez blob 'BlobName.vhd' sanal makine diski 'VirtualMachineDiskName' olarak kullanılıyor.*</span><span class="sxs-lookup"><span data-stu-id="65895-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so hello blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="65895-135">Çözüm</span><span class="sxs-lookup"><span data-stu-id="65895-135">Solution</span></span>
<span data-ttu-id="65895-136">tooresolve hello en sık karşılaşılan sorunları, yöntem aşağıdaki hello deneyin:</span><span class="sxs-lookup"><span data-stu-id="65895-136">tooresolve hello most common issues, try hello following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a><span data-ttu-id="65895-137">1. adım: hello depolama hesabı, kapsayıcısı veya VHD silinmesini engelliyor diskler Sil</span><span class="sxs-lookup"><span data-stu-id="65895-137">Step 1: Delete any disks that are preventing deletion of hello storage account, container, or VHD</span></span>
1. <span data-ttu-id="65895-138">Geçiş toohello [Klasik Azure portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="65895-138">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="65895-139">Seçin **sanal makine** > **DİSKLERİ**.</span><span class="sxs-lookup"><span data-stu-id="65895-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Klasik Azure portalı sanal makinelerde disklerde görüntüsü.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="65895-141">Merhaba depolama hesabı, kapsayıcısı veya toodelete istediğiniz VHD ile ilişkilendirilmiş hello diskleri bulun.</span><span class="sxs-lookup"><span data-stu-id="65895-141">Locate hello disks that are associated with hello storage account, container, or VHD that you want toodelete.</span></span> <span data-ttu-id="65895-142">Merhaba disk hello konumunu işaretlediğinizde, depolama hesabı, kapsayıcısı veya VHD hello ilişkili bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="65895-142">When you check hello location of hello disk, you will find hello associated storage account, container, or VHD.</span></span>

    ![Konum bilgileri diskler için Azure Klasik portalında gösteren resim](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="65895-144">Merhaba diskleri yöntemler aşağıdaki hello birini kullanarak silin:</span><span class="sxs-lookup"><span data-stu-id="65895-144">Delete hello disks by using one of hello following methods:</span></span>

  - <span data-ttu-id="65895-145">Varsa hiçbir VM üzerinde hello listelenen **bağlı** alan hello disk, hello disk doğrudan silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65895-145">If  there is no VM listed on hello **Attached To** field of hello disk, you can delete hello disk directly.</span></span>

  - <span data-ttu-id="65895-146">Başlangıç diski bir veri diski ise, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="65895-146">If hello disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="65895-147">Disk hello VM iliştirildiği hello Hello adını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="65895-147">Check hello name of hello VM that hello disk is attached to.</span></span>
    2. <span data-ttu-id="65895-148">Çok Git**sanal makineleri** > **örnekleri**ve hello VM bulun.</span><span class="sxs-lookup"><span data-stu-id="65895-148">Go too**Virtual Machines** > **Instances**, and then locate hello VM.</span></span>
    3. <span data-ttu-id="65895-149">Hiçbir şey etkin şekilde hello disk kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="65895-149">Make sure that nothing is actively using hello disk.</span></span>
    4. <span data-ttu-id="65895-150">Seçin **diski Ayır** hello portal toodetach hello disk hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="65895-150">Select **Detach Disk** at hello bottom of hello portal toodetach hello disk.</span></span>
    5. <span data-ttu-id="65895-151">Çok Git**sanal makineleri** > **diskleri**ve Merhaba bekleyin **bağlı** alan tooturn boş.</span><span class="sxs-lookup"><span data-stu-id="65895-151">Go too**Virtual Machines** > **Disks**, and wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="65895-152">Bu hello disk hello VM ' başarıyla ayrıldı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="65895-152">This indicates hello disk has successfully detached from hello VM.</span></span>
    6. <span data-ttu-id="65895-153">Seçin **silmek** hello altındaki **sanal makineleri** > **diskleri** toodelete hello disk.</span><span class="sxs-lookup"><span data-stu-id="65895-153">Select **Delete** at hello bottom of **Virtual Machines** > **Disks** toodelete hello disk.</span></span>

  - <span data-ttu-id="65895-154">Merhaba disk işletim sistemi diski ise (Merhaba **içeren işletim sistemi** alanı, Windows gibi bir değer içeriyor) ve ekli tooa VM, şu adımları izleyin toodelete hello VM.</span><span class="sxs-lookup"><span data-stu-id="65895-154">If hello disk is an OS disk (hello **Contains OS** field has a value like Windows) and attached tooa VM, follow these steps toodelete hello VM.</span></span> <span data-ttu-id="65895-155">toodelete hello VM toorelease hello kira sahibiz şekilde hello işletim sistemi diski ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="65895-155">hello OS disk cannot be detached, so we have toodelete hello VM toorelease hello lease.</span></span>

    1. <span data-ttu-id="65895-156">Veri diski bağlı hello sanal makine hello Hello adını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="65895-156">Check hello name of hello Virtual Machine hello Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="65895-157">Çok Git**sanal makineleri** > **örnekleri**, ve ardından select hello disk hello VM bağlı.</span><span class="sxs-lookup"><span data-stu-id="65895-157">Go too**Virtual Machines** > **Instances**, and then select hello VM that hello disk is attached to.</span></span>
    3. <span data-ttu-id="65895-158">Hiçbir şey etkin şekilde hello sanal makine ve sanal makine artık hello kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="65895-158">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
    4. <span data-ttu-id="65895-159">Select hello VM hello disk eklendiği, ardından **silmek** > **Delete hello bağlı diskler**.</span><span class="sxs-lookup"><span data-stu-id="65895-159">Select hello VM hello disk is attached to, then select **Delete** > **Delete hello attached disks**.</span></span>
    5. <span data-ttu-id="65895-160">Çok Git**sanal makineleri** > **diskleri**ve hello disk toodisappear için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="65895-160">Go too**Virtual Machines** > **Disks**, and wait for hello disk toodisappear.</span></span>  <span data-ttu-id="65895-161">Bu toooccur birkaç dakika sürebilir ve toorefresh hello sayfa gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="65895-161">It may take a few minutes for this toooccur, and you may need toorefresh hello page.</span></span>
    6. <span data-ttu-id="65895-162">Merhaba disk kayboluyor değil, hello için bekleyin. **bağlı** alan tooturn boş.</span><span class="sxs-lookup"><span data-stu-id="65895-162">If hello disk does not disappear, wait for hello **Attached To** field tooturn blank.</span></span> <span data-ttu-id="65895-163">Bu hello disk tam olarak VM hello ayrıldı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="65895-163">This indicates hello disk has fully detached from hello VM.</span></span>  <span data-ttu-id="65895-164">Sonra hello disk seçin ve Seç **silmek** hello sayfa toodelete hello disk hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="65895-164">Then, select hello disk, and select **Delete** at hello bottom of hello page toodelete hello disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="65895-165">Bir disk ekli tooa VM ise mümkün toodelete olmaz.</span><span class="sxs-lookup"><span data-stu-id="65895-165">If a disk is attached tooa VM, you will not be able toodelete it.</span></span> <span data-ttu-id="65895-166">Diskleri silinmiş bir VM'den zaman uyumsuz olarak ayrılır.</span><span class="sxs-lookup"><span data-stu-id="65895-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="65895-167">Bu alan tooclear için hello VM silindikten sonra birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="65895-167">It might take a few minutes after hello VM is deleted for this field tooclear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a><span data-ttu-id="65895-168">2. adım: hello depolama hesabı veya kapsayıcı silinmesine engelleyen tüm VM görüntüleri silin</span><span class="sxs-lookup"><span data-stu-id="65895-168">Step 2: Delete any VM Images that are preventing deletion of hello storage account or container</span></span>
1. <span data-ttu-id="65895-169">Geçiş toohello [Klasik Azure portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="65895-169">Switch toohello [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="65895-170">Seçin **sanal makine** > **GÖRÜNTÜLERİ**ve ardından hello depolama hesabı, kapsayıcısı veya VHD ile ilişkilendirilmiş hello görüntüleri silin.</span><span class="sxs-lookup"><span data-stu-id="65895-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete hello images that are associated with hello storage account, container, or VHD.</span></span>

    <span data-ttu-id="65895-171">Bundan sonra toodelete hello depolama hesabı, kapsayıcısı veya VHD yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="65895-171">After that, try toodelete hello storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="65895-172">Merhaba hesabı silmeden önce emin tooback herhangi bir şey olması toosave istiyor.</span><span class="sxs-lookup"><span data-stu-id="65895-172">Be sure tooback up anything you want toosave before you delete hello account.</span></span> <span data-ttu-id="65895-173">VHD, blob, tablo, kuyruk veya dosya sildiğinizde, kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="65895-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="65895-174">Merhaba kaynak kullanımda olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="65895-174">Ensure that hello resource is not in use.</span></span>
>
>

## <a name="about-hello-stopped-deallocated-status"></a><span data-ttu-id="65895-175">Merhaba durduruldu (serbest bırakıldı) durumu hakkında</span><span class="sxs-lookup"><span data-stu-id="65895-175">About hello Stopped (deallocated) status</span></span>
<span data-ttu-id="65895-176">Merhaba Klasik dağıtım modelinde oluşturulmuş ve, korundu VM'ler hello olacaktır **durduruldu (serbest bırakıldı)** ya da hello durumuna [Azure portal](https://portal.azure.com/) veya [Klasik Azure portalı ](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="65895-176">VMs that were created in hello classic deployment model and that have been retained will have hello **Stopped (deallocated)** status on either hello [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="65895-177">**Klasik Azure portalı**:</span><span class="sxs-lookup"><span data-stu-id="65895-177">**Azure classic portal**:</span></span>

![(Deallocated) durum VM'ler için Azure Portal'da durduruldu.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="65895-179">**Azure portal**:</span><span class="sxs-lookup"><span data-stu-id="65895-179">**Azure portal**:</span></span>

![Durduruldu (serbest bırakıldığında) durum VM'ler için Klasik Azure portalı.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="65895-181">"Durduruldu (serbest bırakıldı)" durumu hello CPU, bellek ve ağ gibi hello bilgisayar kaynakları serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="65895-181">A "Stopped (deallocated)" status releases hello computer resources, such as hello CPU, memory, and network.</span></span> <span data-ttu-id="65895-182">Böylece, hızlı bir şekilde hello VM gerekirse yeniden oluşturabilirsiniz hello diskler, ancak hala korunur.</span><span class="sxs-lookup"><span data-stu-id="65895-182">hello disks, however, are still retained so that you can quickly re-create hello VM if necessary.</span></span> <span data-ttu-id="65895-183">Bu diskleri Azure Depolama tarafından yedeklenen VHD'ler üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="65895-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="65895-184">Merhaba depolama hesabı bu VHD ve hello diskleri kiraları bu VHD'lerde sahip.</span><span class="sxs-lookup"><span data-stu-id="65895-184">hello storage account has these VHDs, and hello disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65895-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65895-185">Next steps</span></span>
* [<span data-ttu-id="65895-186">Bir depolama hesabını silme</span><span class="sxs-lookup"><span data-stu-id="65895-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
