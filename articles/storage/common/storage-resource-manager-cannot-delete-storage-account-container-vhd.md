---
title: "Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde aaaTroubleshoot hataları | Microsoft Docs"
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
ms.openlocfilehash: 33261562a2dd2614b35bc1118924513f8c624d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="120f0-103">Azure depolama hesapları, kapsayıcıları veya VHD'leri sildiğinizde hatalarında sorun giderme</span><span class="sxs-lookup"><span data-stu-id="120f0-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="120f0-104">Bir Azure depolama hesabı, kapsayıcı ya da sanal sabit disk (VHD) toodelete çalıştığınızda hello hataları alabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="120f0-104">You might receive errors when you try toodelete an Azure storage account, container, or virtual hard disk (VHD) in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="120f0-105">Bu makale bir Azure Resource Manager dağıtım kılavuzu toohelp Çöz hello sorun giderme sağlar.</span><span class="sxs-lookup"><span data-stu-id="120f0-105">This article provides troubleshooting guidance toohelp resolve hello problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="120f0-106">Bu makalede Azure sorununuzu adresi değil, ziyaret üzerinde Azure forumları hello [MSDN ve yığın taşması](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="120f0-106">If this article doesn't address your Azure problem, visit hello Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="120f0-107">Bu forumlar sorununuzu nakledebilirsiniz veya too@AzureSupport Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="120f0-107">You can post your problem on these forums or too@AzureSupport on Twitter.</span></span> <span data-ttu-id="120f0-108">Ayrıca, size bir Azure destek isteği seçerek dosya **alma desteği** hello üzerinde [Azure Destek](https://azure.microsoft.com/support/options/) site.</span><span class="sxs-lookup"><span data-stu-id="120f0-108">Also, you can file an Azure support request by selecting **Get support** on hello [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="120f0-109">Belirtiler</span><span class="sxs-lookup"><span data-stu-id="120f0-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="120f0-110">Senaryo 1</span><span class="sxs-lookup"><span data-stu-id="120f0-110">Scenario 1</span></span>
<span data-ttu-id="120f0-111">Toodelete bir Resource Manager dağıtım depolama hesabında bir VHD çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="120f0-111">When you try toodelete a VHD in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="120f0-112">**Toodelete blob 'vhds/BlobName.vhd' başarısız oldu. Hata: Yoktur şu anda bir kira hello blob üzerindeki ve hiçbir kiralama kimliği hello istekte belirtildi.**</span><span class="sxs-lookup"><span data-stu-id="120f0-112">**Failed toodelete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on hello blob and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="120f0-113">Bir sanal makine (VM) toodelete çalıştığınız VHD hello üzerinde bir kira olduğundan bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="120f0-113">This problem can occur because a virtual machine (VM) has a lease on hello VHD that you are trying toodelete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="120f0-114">Senaryo 2</span><span class="sxs-lookup"><span data-stu-id="120f0-114">Scenario 2</span></span>
<span data-ttu-id="120f0-115">Toodelete bir Resource Manager dağıtım depolama hesabında bir kapsayıcı çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="120f0-115">When you try toodelete a container in a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="120f0-116">**Toodelete depolama kapsayıcısı 'VHD'ler' başarısız oldu. Hata: Yoktur şu anda bir kira hello kapsayıcısını ve hiçbir kiralama kimliği hello istekte belirtildi.**</span><span class="sxs-lookup"><span data-stu-id="120f0-116">**Failed toodelete storage container 'vhds'. Error: There is currently a lease on hello container and no lease ID was specified in hello request.**</span></span>

<span data-ttu-id="120f0-117">Merhaba kapsayıcı hello kira durumda kilitli bir VHD olduğundan bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="120f0-117">This problem can occur because hello container has a VHD that is locked in hello lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="120f0-118">Senaryo 3</span><span class="sxs-lookup"><span data-stu-id="120f0-118">Scenario 3</span></span>
<span data-ttu-id="120f0-119">Toodelete bir Resource Manager dağıtım depolama hesabında çalıştığınızda hello aşağıdaki hata iletisini alıyorsunuz:</span><span class="sxs-lookup"><span data-stu-id="120f0-119">When you try toodelete a storage account in a Resource Manager deployment, you receive hello following error message:</span></span>

<span data-ttu-id="120f0-120">**Toodelete depolama hesabı 'StorageAccountName' başarısız oldu. Hata: hello depolama hesabı kullanımda tooits yapıları nedeniyle silinemiyor.**</span><span class="sxs-lookup"><span data-stu-id="120f0-120">**Failed toodelete storage account 'StorageAccountName'. Error: hello storage account cannot be deleted due tooits artifacts being in use.**</span></span>

<span data-ttu-id="120f0-121">Merhaba depolama hesabı hello kira durumda bir VHD içerdiğinden bu sorun oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="120f0-121">This problem can occur because hello storage account contains a VHD that is in hello lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="120f0-122">Çözüm</span><span class="sxs-lookup"><span data-stu-id="120f0-122">Solution</span></span> 
<span data-ttu-id="120f0-123">tooresolve hello ilişkili VM ve bu sorunları hello hello hataya neden olan VHD tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="120f0-123">tooresolve these problems, you must identify hello VHD that is causing hello error and hello associated VM.</span></span> <span data-ttu-id="120f0-124">Ardından, hello VHD Merhaba VM (veri diskleri) gelen detach veya hello hello VHD (işletim sistemi diskler için) kullanarak VM silin.</span><span class="sxs-lookup"><span data-stu-id="120f0-124">Then, detach hello VHD from hello VM (for data disks) or delete hello VM that is using hello VHD (for OS disks).</span></span> <span data-ttu-id="120f0-125">Bu VHD hello hello kira kaldırır ve Silinen toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="120f0-125">This removes hello lease from hello VHD and allows it toobe deleted.</span></span> 

<span data-ttu-id="120f0-126">toodo Bu, kullanımı bir yöntem aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="120f0-126">toodo this, use one of hello following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="120f0-127">Yöntem 1 - kullanım Azure storage Gezgini</span><span class="sxs-lookup"><span data-stu-id="120f0-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="120f0-128">1. adım tanımla hello hello depolama hesabı silinmesini engellemek VHD</span><span class="sxs-lookup"><span data-stu-id="120f0-128">Step 1 Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="120f0-129">Merhaba depolama hesabını sildiğinizde, ileti iletişim kutusu hello aşağıdaki gibi alır:</span><span class="sxs-lookup"><span data-stu-id="120f0-129">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![Merhaba depolama hesabını silme iletisi](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="120f0-131">Merhaba denetleyin **Disk URL** tooidentify hello depolama hesabı ve hello engelleyen VHD hello depolama hesabı silin.</span><span class="sxs-lookup"><span data-stu-id="120f0-131">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="120f0-132">Dize önce aşağıdaki örneğine hello hello ". blob.core.windows.net" Merhaba depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" Merhaba VHD adı.</span><span class="sxs-lookup"><span data-stu-id="120f0-132">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="120f0-133">2. adım Delete hello VHD Azure Storage Gezgini kullanarak</span><span class="sxs-lookup"><span data-stu-id="120f0-133">Step 2 Delete hello VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="120f0-134">İndirme ve yükleme hello en son sürümünü [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="120f0-134">Download and Install hello latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="120f0-135">Bu araç, Windows, macOS ve Linux Azure Storage verilerle tooeasily çalışma sağlayan Microsoft bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="120f0-135">This tool is a standalone app from Microsoft that allows you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="120f0-136">Azure Depolama Gezgini'ni açın ve seçin</span><span class="sxs-lookup"><span data-stu-id="120f0-136">Open Azure Storage Explorer, select</span></span> ![hesabı simgesi](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="120f0-138">Merhaba sol çubuğunda Azure ortamınızı seçin ve ardından oturum açın.</span><span class="sxs-lookup"><span data-stu-id="120f0-138">on hello left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="120f0-139">Tüm abonelikleri veya toodelete istediğiniz hello depolama hesabını içeren hello abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="120f0-139">Select all subscriptions or hello subscription that contains hello storage account you want toodelete.</span></span>

    ![Abonelik Ekle](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="120f0-141">Biz hello disk URL daha önce hello alınan toohello depolama hesabı Git **Blob kapsayıcıları** > **VHD'ler** ve delete hello depolama hesabı Merhaba engelleyen VHD arayın.</span><span class="sxs-lookup"><span data-stu-id="120f0-141">Go toohello storage account that we obtained from hello disk URL earlier, select hello **Blob Containers** > **vhds** and search for hello VHD that prevents you delete hello storage account.</span></span>
5. <span data-ttu-id="120f0-142">Merhaba VHD bulunursa, hello denetleyin **VM adı** sütun toofind hello bu VHD kullanarak VM.</span><span class="sxs-lookup"><span data-stu-id="120f0-142">If hello VHD is found,  check hello **VM Name** column toofind hello VM that is using this VHD.</span></span>

    ![VM denetleyin](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="120f0-144">Merhaba kira Azure portalını kullanarak VHD hello kaldırın.</span><span class="sxs-lookup"><span data-stu-id="120f0-144">Remove hello lease from hello VHD by using Azure portal.</span></span> <span data-ttu-id="120f0-145">Daha fazla bilgi için bkz: [hello VHD öğesinden Kaldır hello kira](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="120f0-145">For more information, see [Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="120f0-146">Toohello Azure Storage Gezgini gidin, hello VHD sağ tıklayın ve ardından Sil'i seçin.</span><span class="sxs-lookup"><span data-stu-id="120f0-146">Go toohello Azure Storage Explorer, right-click hello VHD and then select delete.</span></span>

8. <span data-ttu-id="120f0-147">Merhaba depolama hesabı silin.</span><span class="sxs-lookup"><span data-stu-id="120f0-147">Delete hello storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="120f0-148">Yöntem 2 - Azure portalı</span><span class="sxs-lookup"><span data-stu-id="120f0-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a><span data-ttu-id="120f0-149">1. adım: hello hello depolama hesabı silinmesini engellemek VHD tanımlayın</span><span class="sxs-lookup"><span data-stu-id="120f0-149">Step 1: Identify hello VHD that prevent deletion of hello storage account</span></span>

1. <span data-ttu-id="120f0-150">Merhaba depolama hesabını sildiğinizde, ileti iletişim kutusu hello aşağıdaki gibi alır:</span><span class="sxs-lookup"><span data-stu-id="120f0-150">When you delete hello storage account, you will receive a message dialog such as hello following:</span></span> 

    ![Merhaba depolama hesabını silme iletisi](././media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="120f0-152">Merhaba denetleyin **Disk URL** tooidentify hello depolama hesabı ve hello engelleyen VHD hello depolama hesabı silin.</span><span class="sxs-lookup"><span data-stu-id="120f0-152">Check hello **Disk URL** tooidentify hello storage account and hello VHD that prevents you delete hello storage account.</span></span> <span data-ttu-id="120f0-153">Dize önce aşağıdaki örneğine hello hello ". blob.core.windows.net" Merhaba depolama hesabı adı ve "SCCM2012-2015-08-28.vhd" Merhaba VHD adı.</span><span class="sxs-lookup"><span data-stu-id="120f0-153">In hello following example, hello string before “.blob.core.windows.net “ is hello storage account name, and "SCCM2012-2015-08-28.vhd" is hello VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="120f0-154">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="120f0-154">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="120f0-155">Merhaba Hub menüsünde seçin **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="120f0-155">On hello Hub menu, select **All resources**.</span></span> <span data-ttu-id="120f0-156">Toohello depolama hesabına gidin ve ardından **BLOB'lar** > **VHD'ler**.</span><span class="sxs-lookup"><span data-stu-id="120f0-156">Go toohello storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Merhaba depolama hesabı ve vurgulanmış hello "VHD" kapsayıcı hello portalı ekran görüntüsü](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="120f0-158">Merhaba, biz hello disk URL'den daha önce elde edilen VHD bulun.</span><span class="sxs-lookup"><span data-stu-id="120f0-158">Locate hello VHD that we obtained from hello disk URL earlier.</span></span> <span data-ttu-id="120f0-159">Ardından, VM kullanan belirlemek VHD hello.</span><span class="sxs-lookup"><span data-stu-id="120f0-159">Then, determine which VM is using hello VHD.</span></span> <span data-ttu-id="120f0-160">Genellikle, olan VM hello VHD hello VHD adını kontrol ederek belirleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="120f0-160">Usually, you can determine which VM holds hello VHD by checking name of hello VHD:</span></span>

<span data-ttu-id="120f0-161">Resource Manager geliştirme modelini VM</span><span class="sxs-lookup"><span data-stu-id="120f0-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="120f0-162">İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="120f0-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="120f0-163">Veri diskleri genellikle bu adlandırma kuralını izleyin: VMName-YYYY-AA-GG-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="120f0-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="120f0-164">VM Klasik geliştirme modeli</span><span class="sxs-lookup"><span data-stu-id="120f0-164">VM in Classic development model</span></span>

   * <span data-ttu-id="120f0-165">İşletim sistemi disk genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="120f0-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="120f0-166">Veri diskleri genellikle bu adlandırma kuralını izleyin: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="120f0-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="120f0-167">2. adım: hello kira hello VHD ' kaldırın.</span><span class="sxs-lookup"><span data-stu-id="120f0-167">Step 2: Remove hello lease from hello VHD</span></span>

<span data-ttu-id="120f0-168">[Merhaba kira VHD hello Kaldır](#remove-the-lease-from-the-vhd)ve hello depolama hesabı silin.</span><span class="sxs-lookup"><span data-stu-id="120f0-168">[Remove hello lease from hello VHD](#remove-the-lease-from-the-vhd), and then delete hello storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="120f0-169">Bir kira nedir?</span><span class="sxs-lookup"><span data-stu-id="120f0-169">What is a lease?</span></span>
<span data-ttu-id="120f0-170">Bir kira kullanılan toocontrol erişim tooa blob (örneğin, bir VHD) olabilecek kilit ' dir.</span><span class="sxs-lookup"><span data-stu-id="120f0-170">A lease is a lock that can be used toocontrol access tooa blob (for example, a VHD).</span></span> <span data-ttu-id="120f0-171">Bir blob kiralanmış olduğunda yalnızca hello kira hello sahipleri hello blob erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="120f0-171">When a blob is leased, only hello owners of hello lease can access hello blob.</span></span> <span data-ttu-id="120f0-172">Bir kira nedenleri aşağıdaki hello için önemlidir:</span><span class="sxs-lookup"><span data-stu-id="120f0-172">A lease is important for hello following reasons:</span></span>

* <span data-ttu-id="120f0-173">Birden çok sahipleri toowrite toohello çalışırsanız veri bozulmasını engeller hello blob hello adresindeki aynı bölümünü aynı anda.</span><span class="sxs-lookup"><span data-stu-id="120f0-173">It prevents data corruption if multiple owners try toowrite toohello same portion of hello blob at hello same time.</span></span>
* <span data-ttu-id="120f0-174">Merhaba blob bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.</span><span class="sxs-lookup"><span data-stu-id="120f0-174">It prevents hello blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="120f0-175">Merhaba depolama hesabı bir şey etkin olarak da (örneğin, bir VM) kullanıyorsa, silinen engeller.</span><span class="sxs-lookup"><span data-stu-id="120f0-175">It prevents hello storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-hello-lease-from-hello-vhd"></a><span data-ttu-id="120f0-176">Merhaba kira VHD hello Kaldır</span><span class="sxs-lookup"><span data-stu-id="120f0-176">Remove hello lease from hello VHD</span></span>
<span data-ttu-id="120f0-177">Merhaba VHD bir işletim sistemi diski ise, hello VM tooremove hello kira silmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="120f0-177">If hello VHD is an OS disk, you must delete hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="120f0-178">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="120f0-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="120f0-179">Merhaba üzerinde **Hub** menüsünde, select **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="120f0-179">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="120f0-180">Merhaba VHD hello üzerinde bir kirayı tutan VM seçin.</span><span class="sxs-lookup"><span data-stu-id="120f0-180">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="120f0-181">Hiçbir şey etkin şekilde hello sanal makine ve sanal makine artık hello kullandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="120f0-181">Make sure that nothing is actively using hello virtual machine, and that you no longer need hello virtual machine.</span></span>
5. <span data-ttu-id="120f0-182">Merhaba hello üstündeki **VM ayrıntıları** dikey penceresinde, select **silmek**ve ardından **Evet** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="120f0-182">At hello top of hello **VM details** blade, select **Delete**, and then click **Yes** tooconfirm.</span></span>
6. <span data-ttu-id="120f0-183">Merhaba VM silinmesi gerekir, ancak hello VHD korunabilir.</span><span class="sxs-lookup"><span data-stu-id="120f0-183">hello VM should be deleted, but hello VHD can be retained.</span></span> <span data-ttu-id="120f0-184">Ancak, hello VHD artık kira üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="120f0-184">However, hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="120f0-185">Yayımlanan hello kira toobe birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="120f0-185">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="120f0-186">kira hello tooverify yayımlanır, çok Git**tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >  **VHD'ler**.</span><span class="sxs-lookup"><span data-stu-id="120f0-186">tooverify that hello lease is released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="120f0-187">Merhaba, **Blob özellikleri** bölmesi, hello **kiralama durum** değeri olmalıdır **kilitli değil**.</span><span class="sxs-lookup"><span data-stu-id="120f0-187">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="120f0-188">Merhaba VHD bir veri diski varsa, hello VHD hello VM tooremove hello kira gelen bağlantısını kesin:</span><span class="sxs-lookup"><span data-stu-id="120f0-188">If hello VHD is a data disk, detach hello VHD from hello VM tooremove hello lease:</span></span>

1. <span data-ttu-id="120f0-189">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="120f0-189">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="120f0-190">Merhaba üzerinde **Hub** menüsünde, select **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="120f0-190">On hello **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="120f0-191">Merhaba VHD hello üzerinde bir kirayı tutan VM seçin.</span><span class="sxs-lookup"><span data-stu-id="120f0-191">Select hello VM that holds a lease on hello VHD.</span></span>
4. <span data-ttu-id="120f0-192">Seçin **diskleri** hello üzerinde **VM ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="120f0-192">Select **Disks** on hello **VM details** blade.</span></span>
5. <span data-ttu-id="120f0-193">VHD hello üzerinde bir kirayı tutan hello veri diski seçin.</span><span class="sxs-lookup"><span data-stu-id="120f0-193">Select hello data disk that holds a lease on hello VHD.</span></span> <span data-ttu-id="120f0-194">VHD bağlı olduğu belirleyebilirsiniz hello VHD hello URL'sini denetleyerek hello disk.</span><span class="sxs-lookup"><span data-stu-id="120f0-194">You can determine which VHD is attached in hello disk by checking hello URL of hello VHD.</span></span>
6. <span data-ttu-id="120f0-195">Hiçbir şey hello veri diski etkin olarak kullandığını kesin olarak belirleyin.</span><span class="sxs-lookup"><span data-stu-id="120f0-195">Determine with certainty that nothing is actively using hello data disk.</span></span>
7. <span data-ttu-id="120f0-196">Tıklatın **ayırma** hello üzerinde **Disk ayrıntıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="120f0-196">Click **Detach** on hello **Disk details** blade.</span></span>
8. <span data-ttu-id="120f0-197">Hello disk şimdi VM hello ayrılmış ve hello VHD artık kira üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="120f0-197">hello disk should now be detached from hello VM, and hello VHD should no longer have a lease on it.</span></span> <span data-ttu-id="120f0-198">Yayımlanan hello kira toobe birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="120f0-198">It may take a few minutes for hello lease toobe released.</span></span> <span data-ttu-id="120f0-199">kira hello tooverify yayımlanan, çok Git**tüm kaynakları** > **depolama hesabı adı** > **BLOB'lar**  >  **VHD'ler**.</span><span class="sxs-lookup"><span data-stu-id="120f0-199">tooverify that hello lease has been released, go too**All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="120f0-200">Merhaba, **Blob özellikleri** bölmesi, hello **kiralama durum** değeri olmalıdır **kilitli değil**.</span><span class="sxs-lookup"><span data-stu-id="120f0-200">In hello **Blob properties** pane, hello **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="120f0-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="120f0-201">Next steps</span></span>
* [<span data-ttu-id="120f0-202">Bir depolama hesabını silme</span><span class="sxs-lookup"><span data-stu-id="120f0-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="120f0-203">Toobreak hello kira blob storage'nın Microsoft Azure (PowerShell) nasıl kilitli</span><span class="sxs-lookup"><span data-stu-id="120f0-203">How toobreak hello locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
