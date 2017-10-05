---
title: "Bir şirket içi sanal makine görüntüsü için Azure Marketi oluşturma | Microsoft Docs"
description: "Anlama ve şirket içi VM görüntü oluşturma ve Azure satın almak için Marketinde başkalarının dağıtma adımları yürütün."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: 8f6b9a9293dc149586e6e5fd55028170ea825b07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="eec89-103">Bir şirket içi sanal makine görüntüsü için Azure Marketi geliştirin</span><span class="sxs-lookup"><span data-stu-id="eec89-103">Develop an on-premises virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="eec89-104">Uzak Masaüstü Protokolü kullanarak Azure sanal sabit diskleri (VHD) doğrudan bulutta geliştirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="eec89-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in the cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="eec89-105">Ancak, gerekirse, bir VHD karşıdan yüklemek ve şirket içi altyapıyı kullanarak geliştirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="eec89-105">However, if you must, it is possible to download a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="eec89-106">Şirket içi geliştirme için işletim sistemi oluşturulan VM VHD indirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eec89-106">For on-premises development, you must download the operating system VHD of the created VM.</span></span> <span data-ttu-id="eec89-107">Bu adımları adım 3.3, bir parçası olarak yukarıda gerçekleşmesi.</span><span class="sxs-lookup"><span data-stu-id="eec89-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="eec89-108">Bir VHD görüntüsü indirin</span><span class="sxs-lookup"><span data-stu-id="eec89-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="eec89-109">Bir blob URL'si bulun</span><span class="sxs-lookup"><span data-stu-id="eec89-109">Locate a blob URL</span></span>
<span data-ttu-id="eec89-110">VHD indirmek için önce işletim sistemi diski blob URL'si bulun.</span><span class="sxs-lookup"><span data-stu-id="eec89-110">In order to download the VHD, first locate the blob URL for the operating system disk.</span></span>

<span data-ttu-id="eec89-111">Yeni blob URL'den bulun [Microsoft Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="eec89-111">Locate the blob URL from the new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="eec89-112">Git **Gözat** > **VM'ler**ve ardından dağıtılan VM seçin.</span><span class="sxs-lookup"><span data-stu-id="eec89-112">Go to **Browse** > **VMs**, and then select the deployed VM.</span></span>
2. <span data-ttu-id="eec89-113">Altında **yapılandırma**seçin **diskleri** döşeme, hangi diskleri bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="eec89-113">Under **Configure**, select the **Disks** tile, which opens the Disks blade.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="eec89-115">Seçin **işletim sistemi diski**, disk özellikleri, VHD konumu dahil olmak üzere görüntüler başka bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="eec89-115">Select the **OS Disk**, which opens another blade that displays disk properties, including the VHD location.</span></span>
4. <span data-ttu-id="eec89-116">Bu blob URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="eec89-116">Copy this blob URL.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="eec89-118">Şimdi, dağıtılan VM yedekleme diskleri silmeden silin.</span><span class="sxs-lookup"><span data-stu-id="eec89-118">Now, delete the deployed VM without deleting the backing disks.</span></span> <span data-ttu-id="eec89-119">Ayrıca silmeden yerine VM durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eec89-119">You can also stop the VM instead of deleting it.</span></span> <span data-ttu-id="eec89-120">VM çalışırken işletim sistemi VHD yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="eec89-120">Do not download the operating system VHD when the VM is running.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="eec89-122">VHD indirme</span><span class="sxs-lookup"><span data-stu-id="eec89-122">Download a VHD</span></span>
<span data-ttu-id="eec89-123">Blob URL'si öğrendikten sonra kullanarak VHD indirebilirsiniz [Azure portal](http://manage.windowsazure.com/) veya PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eec89-123">After you know the blob URL, you can download the VHD by using the [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="eec89-124">Bu kılavuz oluşturma sırasında bir VHD yüklemek için işlevsellik henüz yeni Microsoft Azure Portalı'nda mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="eec89-124">At the time of this guide’s creation, the functionality to download a VHD is not yet present in the new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="eec89-125">**Bir işletim sistemi geçerli aracılığıyla karşıdan [Azure portalı](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="eec89-125">**Download the operating system VHD via the current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="eec89-126">Siz bunu zaten yapmadıysanız, Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eec89-126">Sign in to the Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="eec89-127">Tıklatın **depolama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eec89-127">Click the **Storage** tab.</span></span>
3. <span data-ttu-id="eec89-128">VHD depolandığı depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="eec89-128">Select the storage account within which the VHD is stored.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="eec89-130">Bu depolama hesabı özellikleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eec89-130">This displays storage account properties.</span></span> <span data-ttu-id="eec89-131">Seçin **kapsayıcıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eec89-131">Select the **Containers** tab.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="eec89-133">VHD depolandığı kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="eec89-133">Select the container in which the VHD is stored.</span></span> <span data-ttu-id="eec89-134">Varsayılan olarak, portalından oluşturulması sırasında VHD'yi bir VHD kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="eec89-134">By default, when created from the portal, the VHD is stored in a vhds container.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="eec89-136">Kaydedilen bir URL karşılaştırarak doğru işletim sistemi VHD seçin.</span><span class="sxs-lookup"><span data-stu-id="eec89-136">Select the correct operating system VHD by comparing the URL to the one you saved.</span></span>
7. <span data-ttu-id="eec89-137">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eec89-137">Click **Download**.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="eec89-139">PowerShell kullanarak bir VHD'yi indirin</span><span class="sxs-lookup"><span data-stu-id="eec89-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="eec89-140">Azure Portalı'nı kullanarak ek olarak, kullanabileceğiniz [Kaydet AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) VHD işletim sistemi yüklemek için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="eec89-140">In addition to using the Azure portal, you can use the [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet to download the operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="eec89-141">Örneğin, kaydetme AzureVhd-kaynak "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath "C:\Users\Administrator\Desktop\baseimagevm.vhd" - depolama anahtarı<String></span><span class="sxs-lookup"><span data-stu-id="eec89-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="eec89-142">**Kaydet-AzureVhd** de sahip bir **NumberOfThreads** indirme için kullanılabilir bant genişliğini en iyi kullanılmasını sağlamak üzere paralelliği artırmak için kullanılan seçeneği.</span><span class="sxs-lookup"><span data-stu-id="eec89-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used to increase parallelism to make the best use of available bandwidth for the download.</span></span>
> 
> 

## <a name="upload-vhds-to-an-azure-storage-account"></a><span data-ttu-id="eec89-143">VHD bir Azure storage hesabına yükleme</span><span class="sxs-lookup"><span data-stu-id="eec89-143">Upload VHDs to an Azure storage account</span></span>
<span data-ttu-id="eec89-144">VHD'ler şirket içi hazırlanmış, Azure depolama hesabında içine karşıya yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eec89-144">If you prepared your VHDs on-premises, you need to upload them into a storage account in Azure.</span></span> <span data-ttu-id="eec89-145">Bu adım, VHD oluşturma şirket içi sonra ancak VM görüntüsü için sertifika alma önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="eec89-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="eec89-146">Bir depolama hesabı ve kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eec89-146">Create a storage account and container</span></span>
<span data-ttu-id="eec89-147">VHD'ler Amerika Birleşik Devletleri'nde bir bölgede depolama hesaba yüklenebilmesi öneririz.</span><span class="sxs-lookup"><span data-stu-id="eec89-147">We recommend that VHDs be uploaded into a storage account in a region in the United States.</span></span> <span data-ttu-id="eec89-148">Tüm VHD'leri tek bir SKU için tek bir depolama hesabına içindeki tek bir kapsayıcıda yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="eec89-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="eec89-149">Bir depolama hesabı oluşturmak için kullanabileceğiniz [Microsoft Azure portal](https://portal.azure.com/), PowerShell veya Linux komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="eec89-149">To create a storage account, you can use the [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or the Linux command-line tool.</span></span>  

<span data-ttu-id="eec89-150">**Microsoft Azure Portalı'ndan bir depolama hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="eec89-150">**Create a storage account from the Microsoft Azure portal**</span></span>

1. <span data-ttu-id="eec89-151">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eec89-151">Click **New**.</span></span>
2. <span data-ttu-id="eec89-152">Seçin **depolama**.</span><span class="sxs-lookup"><span data-stu-id="eec89-152">Select **Storage**.</span></span>
3. <span data-ttu-id="eec89-153">Depolama hesabı adı girin ve ardından bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="eec89-153">Fill in the storage account name, and then select a location.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="eec89-155">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eec89-155">Click **Create**.</span></span>
5. <span data-ttu-id="eec89-156">Oluşturulan depolama hesabı için dikey penceresi açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eec89-156">The blade for the created storage account should be open.</span></span> <span data-ttu-id="eec89-157">Aksi takdirde, seçin **Gözat** > **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="eec89-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="eec89-158">Depolama hesabı dikey penceresinde, oluşturduğunuz depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="eec89-158">On the Storage account blade, select the storage account created.</span></span>
6. <span data-ttu-id="eec89-159">Seçin **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="eec89-159">Select **Containers**.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="eec89-161">Kapsayıcıları dikey penceresinde, seçin **Ekle**ve ardından bir kapsayıcı adı hem kapsayıcı izinleri girin.</span><span class="sxs-lookup"><span data-stu-id="eec89-161">On the Containers blade, select **Add**, and then enter a container name and the container permissions.</span></span> <span data-ttu-id="eec89-162">Seçin **özel** kapsayıcı izinleri.</span><span class="sxs-lookup"><span data-stu-id="eec89-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="eec89-163">Bir kapsayıcıya yayımlamak için planlama SKU başına oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="eec89-163">We recommend that you create one container per SKU that you are planning to publish.</span></span>
> 
> 

  ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="eec89-165">PowerShell kullanarak bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eec89-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="eec89-166">PowerShell kullanarak oluşturduğunuz bir depolama hesabı kullanarak [yeni AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="eec89-166">Using PowerShell, create a storage account by using the [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="eec89-167">Ardından kullanarak bu depolama hesabı içindeki bir kapsayıcı oluşturabilirsiniz [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="eec89-167">Then you can create a container within that storage account by using the [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="eec89-168">Bu komutlar, geçerli depolama hesabı bağlamını PowerShell'de zaten ayarlanmış varsayalım.</span><span class="sxs-lookup"><span data-stu-id="eec89-168">Those commands assume that the current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="eec89-169">Başvurmak [Azure PowerShell ayarı](marketplace-publishing-powershell-setup.md) PowerShell kurulumu hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="eec89-169">Refer to [Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="eec89-170">Mac ve Linux için komut satırı aracını kullanarak bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eec89-170">Create a storage account by using the command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="eec89-171">Gelen [Linux komut satırı aracı](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aşağıdaki gibi bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eec89-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="eec89-172">Şu şekilde bir kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eec89-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="eec89-173">VHD’yi karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="eec89-173">Upload a VHD</span></span>
<span data-ttu-id="eec89-174">Depolama hesabı ve kapsayıcı oluşturduktan sonra hazırlanan Vhd'lerinizi karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eec89-174">After the storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="eec89-175">PowerShell, Linux komut satırı aracını veya diğer Azure Depolama Yönetimi araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eec89-175">You can use PowerShell, the Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="eec89-176">Bir VHD PowerShell aracılığıyla karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="eec89-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="eec89-177">Kullanım [Ekle AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="eec89-177">Use the [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-the-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="eec89-178">Mac ve Linux için komut satırı aracını kullanarak bir VHD'yi karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="eec89-178">Upload a VHD by using the command-line tool for Mac and Linux</span></span>
<span data-ttu-id="eec89-179">İle [Linux komut satırı aracı](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), aşağıdakileri kullanın: azure vm görüntüsü oluşturma <image name> --konum <Location of the data center> --OS Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="eec89-179">With the [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use the following: azure vm image create <image name> --location <Location of the data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="eec89-180">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="eec89-180">See also</span></span>
* [<span data-ttu-id="eec89-181">Market bir sanal makine görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="eec89-181">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="eec89-182">Azure PowerShell ayarlama</span><span class="sxs-lookup"><span data-stu-id="eec89-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

