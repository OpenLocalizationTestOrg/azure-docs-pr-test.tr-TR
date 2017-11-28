---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme | Microsoft Docs"
description: "Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 11944dd38b1cc30106c0b76a108480c018ca39d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="6dbad-103">Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme</span><span class="sxs-lookup"><span data-stu-id="6dbad-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="6dbad-104">Bir Azure depolama hesabı, kapsayıcı ya da sanal sabit disk (VHD) silmeye çalıştığınızda, hatalar alabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6dbad-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6dbad-105">Bu makalede Azure Resource Manager dağıtımında sorunu gidermek için sorun giderme kılavuzu verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="6dbad-106">Bu makalede Azure sorununuzu adresi değil, üzerinde Azure forumları ziyaret [MSDN ve yığın taşması](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="6dbad-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="6dbad-107">Bu forumları veya çok sorununuzu nakledebilirsiniz @AzureSupport Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="6dbad-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="6dbad-108">Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="6dbad-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="6dbad-109">Belirtiler</span><span class="sxs-lookup"><span data-stu-id="6dbad-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="6dbad-110">Senaryo 1</span><span class="sxs-lookup"><span data-stu-id="6dbad-110">Scenario 1</span></span>
<span data-ttu-id="6dbad-111">Resource Manager dağıtım depolama hesabında bir VHD silmeye çalıştığınızda, aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6dbad-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="6dbad-112">**BLOB 'vhds/BlobName.vhd' silinemedi. Hata: Yoktur şu anda bir kira blob üzerindeki ve istekte hiçbir kiralama kimliği belirtildi.**</span><span class="sxs-lookup"><span data-stu-id="6dbad-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="6dbad-113">Bir sanal makine (VM), silmeyi denediğiniz VHD üzerinde bir kira olduğundan bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="6dbad-114">Senaryo 2</span><span class="sxs-lookup"><span data-stu-id="6dbad-114">Scenario 2</span></span>
<span data-ttu-id="6dbad-115">Resource Manager dağıtım depolama hesabında bir kapsayıcı silmeye çalıştığınızda, aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6dbad-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="6dbad-116">**Depolama kapsayıcısı 'VHD'ler' silinemedi. Hata: Yoktur şu anda bir kira kapsayıcısını ve istekte hiçbir kiralama kimliği belirtildi.**</span><span class="sxs-lookup"><span data-stu-id="6dbad-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="6dbad-117">Kapsayıcı kira durumda kilitli bir VHD olduğundan bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="6dbad-118">Senaryo 3</span><span class="sxs-lookup"><span data-stu-id="6dbad-118">Scenario 3</span></span>
<span data-ttu-id="6dbad-119">Resource Manager dağıtım bir depolama hesabını silmeye çalıştığınızda, aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="6dbad-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="6dbad-120">**Depolama hesabı 'StorageAccountName' silinemedi. Hata: Depolama hesabına ait yapıtlar kullanımda nedeniyle silinemiyor.**</span><span class="sxs-lookup"><span data-stu-id="6dbad-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="6dbad-121">Depolama hesabı kira durumuna sahip bir VHD içerdiğinden bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="6dbad-122">Çözüm</span><span class="sxs-lookup"><span data-stu-id="6dbad-122">Solution</span></span> 
<span data-ttu-id="6dbad-123">Bu sorunları gidermek için hataya neden olan VHD ve ilişkili VM tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="6dbad-124">Ardından, VM (için veri diskleri) VHD'den detach veya VHD (işletim sistemi diskler için) kullanarak VM silin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="6dbad-125">Bu kira VHD'den kaldırır ve silinmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="6dbad-126">Bunu yapmak için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="6dbad-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="6dbad-127">Yöntem 1 - kullanım Azure storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="6dbad-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="6dbad-128">Adım 1 depolama hesabı silinmesini engellemek VHD tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6dbad-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="6dbad-129">Depolama hesabı sildiğinizde, ileti iletişim kutusu aşağıdaki gibi alır:</span><span class="sxs-lookup"><span data-stu-id="6dbad-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![Depolama hesabını silme iletisi](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="6dbad-131">Denetleme **Disk URL** depolama belirlemek için hesap ve engelleyen VHD depolama hesabını silme.</span><span class="sxs-lookup"><span data-stu-id="6dbad-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="6dbad-132">Aşağıdaki örnekte, dize önce ". blob.core.windows.net" depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" VHD adı.</span><span class="sxs-lookup"><span data-stu-id="6dbad-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="6dbad-133">2. adım, Azure Storage Gezgini kullanarak VHD silme</span><span class="sxs-lookup"><span data-stu-id="6dbad-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="6dbad-134">En son sürümünü karşıdan yükleyip [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="6dbad-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="6dbad-135">Bu araç, Windows, macOS ve Linux Azure Storage ile kolayca çalışmanızı sağlayan Microsoft bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="6dbad-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="6dbad-136">Azure Depolama Gezgini'ni açın ve seçin</span><span class="sxs-lookup"><span data-stu-id="6dbad-136">Open Azure Storage Explorer, select</span></span> ![hesabı simgesi](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="6dbad-138">Sol çubuğunda, Azure ortamınıza seçin ve ardından oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6dbad-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="6dbad-139">Tüm abonelikleri veya silmek istediğiniz depolama hesabını içeren bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![Abonelik Ekle](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="6dbad-141">Biz disk URL'den daha önce edindiğiniz depolama hesabı gidin **Blob kapsayıcıları** > **VHD'ler** ve arama engelleyen VHD için depolama hesabı silin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="6dbad-142">VHD bulunursa, denetleme **VM adı** bu VHD kullanarak VM bulmak için sütun.</span><span class="sxs-lookup"><span data-stu-id="6dbad-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![VM denetleyin](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="6dbad-144">Kira VHD'den Azure portalını kullanarak kaldırın.</span><span class="sxs-lookup"><span data-stu-id="6dbad-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="6dbad-145">Daha fazla bilgi için bkz: [kira VHD'den kaldırmak](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="6dbad-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="6dbad-146">Azure depolama Gezgini'ne gidin, VHD'yi sağ tıklayın ve ardından Sil'i seçin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="6dbad-147">Depolama hesabını silin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="6dbad-148">Yöntem 2 - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="6dbad-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="6dbad-149">1. adım: depolama hesabı silinmesini engellemek VHD tanımlayın</span><span class="sxs-lookup"><span data-stu-id="6dbad-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="6dbad-150">Depolama hesabı sildiğinizde, ileti iletişim kutusu aşağıdaki gibi alır:</span><span class="sxs-lookup"><span data-stu-id="6dbad-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![Depolama hesabını silme iletisi](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="6dbad-152">Denetleme **Disk URL** depolama belirlemek için hesap ve engelleyen VHD depolama hesabını silme.</span><span class="sxs-lookup"><span data-stu-id="6dbad-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="6dbad-153">Aşağıdaki örnekte, dize önce ". blob.core.windows.net" depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" VHD adı.</span><span class="sxs-lookup"><span data-stu-id="6dbad-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="6dbad-154">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6dbad-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="6dbad-155">Hub menüsünde seçin **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="6dbad-156">Depolama hesabına gidin ve ardından **BLOB'lar** > **VHD'ler**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Depolama hesabı ve vurgulanmış "VHD" kapsayıcı portalı ekran görüntüsü](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="6dbad-158">Biz disk URL'den daha önce edindiğiniz VHD'yi bulun.</span><span class="sxs-lookup"><span data-stu-id="6dbad-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="6dbad-159">Ardından, VM kullanan belirlemek VHD.</span><span class="sxs-lookup"><span data-stu-id="6dbad-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="6dbad-160">Genellikle, VHD adını kontrol ederek VHD VM tutan belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6dbad-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="6dbad-161">Resource Manager geliştirme modelini VM</span><span class="sxs-lookup"><span data-stu-id="6dbad-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="6dbad-162">İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6dbad-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="6dbad-163">Veri diskleri genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6dbad-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="6dbad-164">VM Klasik geliştirme modeli</span><span class="sxs-lookup"><span data-stu-id="6dbad-164">VM in Classic development model</span></span>

   * <span data-ttu-id="6dbad-165">İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6dbad-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="6dbad-166">Veri diskleri genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="6dbad-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="6dbad-167">2. adım: kira VHD'den kaldırın.</span><span class="sxs-lookup"><span data-stu-id="6dbad-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="6dbad-168">[Kira VHD'den kaldırmak](#remove-the-lease-from-the-vhd)ve ardından depolama hesabını silin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="6dbad-169">Bir kira nedir?</span><span class="sxs-lookup"><span data-stu-id="6dbad-169">What is a lease?</span></span>
<span data-ttu-id="6dbad-170">Bir kira blob'u (örneğin, bir VHD) erişimi denetlemek için kullanılan bir kilit ' dir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="6dbad-171">Bir blob kiralanmış yalnızca kira sahipleri blob erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dbad-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="6dbad-172">Bir kira aşağıdaki nedenlerle önemlidir:</span><span class="sxs-lookup"><span data-stu-id="6dbad-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="6dbad-173">Aynı anda blob aynı bölümüne yazmak birden çok sahipleri denerseniz, veri bozulmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="6dbad-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="6dbad-174">Blob bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.</span><span class="sxs-lookup"><span data-stu-id="6dbad-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="6dbad-175">Depolama hesabı bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.</span><span class="sxs-lookup"><span data-stu-id="6dbad-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="6dbad-176">Kira VHD'den Kaldır</span><span class="sxs-lookup"><span data-stu-id="6dbad-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="6dbad-177">VHD bir işletim sistemi diski ise, kira kaldırmak için VM silmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="6dbad-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="6dbad-178">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6dbad-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6dbad-179">Üzerinde **Hub** menüsünde, select **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="6dbad-180">VHD bir kirayı tutan VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="6dbad-181">Hiçbir şey etkin olarak sanal makinenin kullandığından emin olun ve sanal makine artık gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="6dbad-182">Üstündeki **VM ayrıntıları** dikey penceresinde, select **silmek**ve ardından **Evet** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="6dbad-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="6dbad-183">VM silinmesi gerekir, ancak VHD korunabilir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="6dbad-184">Ancak, VHD'yi artık kira üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6dbad-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="6dbad-185">Yayımlanacak kira için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="6dbad-186">Kira serbest olduğunu doğrulamak için Git **tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >   **VHD'ler**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="6dbad-187">İçinde **Blob özellikleri** bölmesinde **kiralama durum** değeri olmalıdır **kilitli değil**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="6dbad-188">VHD bir veri diski varsa, kira kaldırmak için VM VHD'den bağlantısını kesin:</span><span class="sxs-lookup"><span data-stu-id="6dbad-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="6dbad-189">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6dbad-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6dbad-190">Üzerinde **Hub** menüsünde, select **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="6dbad-191">VHD bir kirayı tutan VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="6dbad-192">Seçin **diskleri** üzerinde **VM ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="6dbad-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="6dbad-193">VHD bir kirayı tutan veri diski seçin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="6dbad-194">VHD bağlı olduğu belirleyebilirsiniz VHD URL'sini denetleyerek disk.</span><span class="sxs-lookup"><span data-stu-id="6dbad-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="6dbad-195">Hiçbir şey veri diski etkin olarak kullandığını kesin olarak belirleyin.</span><span class="sxs-lookup"><span data-stu-id="6dbad-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="6dbad-196">Tıklatın **ayırma** üzerinde **Disk ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="6dbad-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="6dbad-197">Diski artık sanal makineden ayrılmış ve VHD artık kira üzerinde sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6dbad-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="6dbad-198">Yayımlanacak kira için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="6dbad-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="6dbad-199">Kiralamasının serbest bırakıldığını doğrulamak için Git **tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >  **VHD'ler**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="6dbad-200">İçinde **Blob özellikleri** bölmesinde **kiralama durum** değeri olmalıdır **kilitli değil**.</span><span class="sxs-lookup"><span data-stu-id="6dbad-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dbad-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6dbad-201">Next steps</span></span>
* [<span data-ttu-id="6dbad-202">Bir depolama hesabını silme</span><span class="sxs-lookup"><span data-stu-id="6dbad-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="6dbad-203">Microsoft Azure (PowerShell) kilitli kira blob storage'nın nasıl</span><span class="sxs-lookup"><span data-stu-id="6dbad-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
