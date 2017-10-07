---
title: "aaaCreating hello Azure Marketi için şirket içi sanal makine görüntü | Microsoft Docs"
description: "Anlama ve hello adımları toocreate bir şirket içi VM görüntüsü yürütün ve başkaları için toohello Azure Marketi dağıtmak toopurchase."
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
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="d9667-103">Hello Azure Marketi için şirket içi sanal makine görüntü geliştirin</span><span class="sxs-lookup"><span data-stu-id="d9667-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="d9667-104">Uzak Masaüstü Protokolü kullanarak, doğrudan hello bulutta Azure sanal sabit diskleri (VHD) geliştirmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="d9667-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="d9667-105">Ancak, gerekirse, olası toodownload bir VHD olduğunu ve şirket içi altyapısını kullanarak geliştirin.</span><span class="sxs-lookup"><span data-stu-id="d9667-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="d9667-106">Şirket içi geliştirme için hello işletim sistemi oluşturulan hello VHD indirmeniz gerekir VM.</span><span class="sxs-lookup"><span data-stu-id="d9667-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="d9667-107">Bu adımları adım 3.3, bir parçası olarak yukarıda gerçekleşmesi.</span><span class="sxs-lookup"><span data-stu-id="d9667-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="d9667-108">Bir VHD görüntüsü indirin</span><span class="sxs-lookup"><span data-stu-id="d9667-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="d9667-109">Bir blob URL'si bulun</span><span class="sxs-lookup"><span data-stu-id="d9667-109">Locate a blob URL</span></span>
<span data-ttu-id="d9667-110">Sipariş toodownload hello VHD, ilk hello blob URL'si hello işletim sistemi diski bulun.</span><span class="sxs-lookup"><span data-stu-id="d9667-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="d9667-111">Merhaba blob hello URL'den yeni bulun [Microsoft Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="d9667-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="d9667-112">Çok Git**Gözat** > **VM'ler**, ve ardından hello VM dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="d9667-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="d9667-113">Altında **yapılandırma**seçin hello **diskleri** döşeme, hangi hello diskleri dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d9667-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="d9667-115">Select hello **işletim sistemi diski**, disk özellikleri, hello VHD konumu dahil olmak üzere görüntüler başka bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="d9667-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="d9667-116">Bu blob URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d9667-116">Copy this blob URL.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="d9667-118">Şimdi, silmek hello dağıtılan VM hello yedekleme diskleri silmeden.</span><span class="sxs-lookup"><span data-stu-id="d9667-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="d9667-119">Merhaba VM silme yerine ayrıca durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9667-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="d9667-120">Merhaba VM çalıştırırken hello işletim sistemi VHD yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="d9667-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="d9667-122">VHD indirme</span><span class="sxs-lookup"><span data-stu-id="d9667-122">Download a VHD</span></span>
<span data-ttu-id="d9667-123">Merhaba blob URL'si öğrendikten sonra hello kullanarak hello VHD indirebilirsiniz [Azure portal](http://manage.windowsazure.com/) veya PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9667-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="d9667-124">Bu kılavuz oluşturma Hello sırasında hello işlevselliği toodownload VHD henüz hello yeni Microsoft Azure Portalı'nda mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="d9667-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="d9667-125">**Merhaba geçerli aracılığıyla Hello işletim sistemi VHD karşıdan [Azure portalı](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="d9667-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="d9667-126">Siz bunu zaten yapmadıysanız toohello Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="d9667-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="d9667-127">Merhaba tıklatın **depolama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d9667-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="d9667-128">VHD hangi hello içinde depolanan hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="d9667-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="d9667-130">Bu depolama hesabı özellikleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d9667-130">This displays storage account properties.</span></span> <span data-ttu-id="d9667-131">Select hello **kapsayıcıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d9667-131">Select hello **Containers** tab.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="d9667-133">Hangi hello VHD depolanan hello kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="d9667-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="d9667-134">Varsayılan olarak, hello Portalı'ndan oluşturduğunuzda hello VHD VHD'ler kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="d9667-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="d9667-136">Merhaba URL toohello bir kaydettiğiniz karşılaştırarak Hello doğru işletim sistemi VHD seçin.</span><span class="sxs-lookup"><span data-stu-id="d9667-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="d9667-137">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9667-137">Click **Download**.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="d9667-139">PowerShell kullanarak bir VHD'yi indirin</span><span class="sxs-lookup"><span data-stu-id="d9667-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="d9667-140">Ayrıca toousing Merhaba Azure portal, hello kullanabilirsiniz [Kaydet AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello işletim sistemi VHD.</span><span class="sxs-lookup"><span data-stu-id="d9667-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="d9667-141">Örneğin, kaydetme AzureVhd-kaynak "https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd" - LocalFilePath "C:\Users\Administrator\Desktop\baseimagevm.vhd" - depolama anahtarı<String></span><span class="sxs-lookup"><span data-stu-id="d9667-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="d9667-142">**Kaydet-AzureVhd** de sahip bir **NumberOfThreads** olabilir seçeneği tooincrease paralellik toomake hello en iyi kullanılabilir bant genişliği kullanımını hello indirme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d9667-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="d9667-143">VHD'ler tooan Azure depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d9667-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="d9667-144">VHD'ler şirket içi hazırlanmış, bunları bir depolama alanına Azure'da hesap tooupload gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9667-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="d9667-145">Bu adım, VHD oluşturma şirket içi sonra ancak VM görüntüsü için sertifika alma önce gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="d9667-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="d9667-146">Bir depolama hesabı ve kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9667-146">Create a storage account and container</span></span>
<span data-ttu-id="d9667-147">VHD'ler hello Amerika Birleşik Devletleri'nde bir bölgede depolama hesaba yüklenebilmesi öneririz.</span><span class="sxs-lookup"><span data-stu-id="d9667-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="d9667-148">Tüm VHD'leri tek bir SKU için tek bir depolama hesabına içindeki tek bir kapsayıcıda yerleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d9667-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="d9667-149">toocreate bir depolama hesabı, kullanabileceğiniz hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell veya hello Linux komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="d9667-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="d9667-150">**Merhaba Microsoft Azure Portalı'ndan bir depolama hesabı oluşturma**</span><span class="sxs-lookup"><span data-stu-id="d9667-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="d9667-151">**Yeni**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9667-151">Click **New**.</span></span>
2. <span data-ttu-id="d9667-152">Seçin **depolama**.</span><span class="sxs-lookup"><span data-stu-id="d9667-152">Select **Storage**.</span></span>
3. <span data-ttu-id="d9667-153">Merhaba depolama hesabı adı girin ve ardından bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="d9667-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="d9667-155">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d9667-155">Click **Create**.</span></span>
5. <span data-ttu-id="d9667-156">Depolama hesabı oluşturuldu hello Hello dikey penceresi açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9667-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="d9667-157">Aksi takdirde, seçin **Gözat** > **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="d9667-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="d9667-158">Dikey penceresinde Hello üzerinde depolama hesabı, oluşturulan hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="d9667-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="d9667-159">Seçin **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="d9667-159">Select **Containers**.</span></span>
   
   ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="d9667-161">Merhaba kapsayıcılara dikey penceresinde, seçin **Ekle**ve ardından bir kapsayıcı adı ve hello kapsayıcısı izinlerine girin.</span><span class="sxs-lookup"><span data-stu-id="d9667-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="d9667-162">Seçin **özel** kapsayıcı izinleri.</span><span class="sxs-lookup"><span data-stu-id="d9667-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="d9667-163">Bir kapsayıcı toopublish planlama SKU başına oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d9667-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![Çizim](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="d9667-165">PowerShell kullanarak bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9667-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="d9667-166">PowerShell kullanarak oluşturduğunuz bir depolama hesabı hello kullanarak [yeni AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d9667-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="d9667-167">Ardından hello kullanarak bu depolama hesabı içindeki bir kapsayıcı oluşturabilirsiniz [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d9667-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="d9667-168">Bu komutları o hello geçerli depolama hesabı bağlamını PowerShell'de ayarlamak varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d9667-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="d9667-169">Çok başvuran[Azure PowerShell ayarı](marketplace-publishing-powershell-setup.md) PowerShell kurulumu hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="d9667-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="d9667-170">Mac ve Linux için hello komut satırı aracını kullanarak bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9667-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="d9667-171">Gelen [Linux komut satırı aracı](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), aşağıdaki gibi bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9667-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="d9667-172">Şu şekilde bir kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9667-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="d9667-173">VHD’yi karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d9667-173">Upload a VHD</span></span>
<span data-ttu-id="d9667-174">Merhaba depolama hesabı ve kapsayıcı oluşturduktan sonra hazırlanan Vhd'lerinizi karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9667-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="d9667-175">PowerShell, hello Linux komut satırı aracını veya diğer Azure Depolama Yönetimi araçlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9667-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="d9667-176">Bir VHD PowerShell aracılığıyla karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d9667-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="d9667-177">Kullanım hello [Ekle AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="d9667-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="d9667-178">Mac ve Linux için hello komut satırı aracını kullanarak bir VHD'yi karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="d9667-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="d9667-179">Merhaba ile [Linux komut satırı aracı](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), hello aşağıdakileri kullanın: azure vm görüntüsü oluşturma <image name> --konum <Location of hello data center> --OS Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="d9667-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="d9667-180">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d9667-180">See also</span></span>
* [<span data-ttu-id="d9667-181">Merhaba Market için bir sanal makine görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="d9667-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="d9667-182">Azure PowerShell ayarlama</span><span class="sxs-lookup"><span data-stu-id="d9667-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

