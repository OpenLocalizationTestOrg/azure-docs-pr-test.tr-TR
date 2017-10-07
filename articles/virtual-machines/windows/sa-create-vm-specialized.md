---
title: "Azure özel bir diskten VM aaaCreate | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde bir özelleştirilmiş yönetilmeyen disk ekleyerek yeni bir VM oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="5879d-103">Bir depolama hesabında özelleştirilmiş bir VHD'den bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="5879d-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="5879d-104">Powershell kullanarak hello işletim sistemi diski olarak özel bir yönetilmeyen disk ekleyerek yeni bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5879d-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="5879d-105">Özelleştirilmiş bir disk hello kullanıcı hesapları, uygulamaları ve diğer Durum verilerini orijinal VM tutar mevcut bir VM'yi VHD'den kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="5879d-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="5879d-106">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="5879d-106">You have two options:</span></span>
* [<span data-ttu-id="5879d-107">Bir VHD’yi karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="5879d-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="5879d-108">Merhaba mevcut bir Azure VM'i VHD kopyalayın</span><span class="sxs-lookup"><span data-stu-id="5879d-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="5879d-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5879d-109">Before you begin</span></span>
<span data-ttu-id="5879d-110">PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5879d-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5879d-111">Çalıştırma hello komut tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="5879d-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="5879d-112">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5879d-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="5879d-113">Seçenek 1: özel bir VHD yüklemek</span><span class="sxs-lookup"><span data-stu-id="5879d-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="5879d-114">Hyper-V ya da VM başka bir buluttan dışarı gibi bir şirket içi sanallaştırma aracı ile özel bir VM VHD'den oluşturulan hello karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="5879d-115">Merhaba VM hazırlama</span><span class="sxs-lookup"><span data-stu-id="5879d-115">Prepare hello VM</span></span>
<span data-ttu-id="5879d-116">Bir şirket içi VM veya başka bir buluttan dışa aktarılan bir VHD kullanılarak oluşturulmuş özel bir VHD karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="5879d-117">Özel bir VHD hello kullanıcı hesapları, uygulamaları ve diğer Durum verilerini orijinal VM tutar.</span><span class="sxs-lookup"><span data-stu-id="5879d-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="5879d-118">Toouse düşünüyorsanız, VHD olarak hello-toocreate yeni bir VM olan aşağıdaki adımları hello tamamlanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="5879d-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="5879d-119">[Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5879d-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5879d-120">**Sağlamadığı** generalize Sysprep kullanarak VM hello.</span><span class="sxs-lookup"><span data-stu-id="5879d-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="5879d-121">Konuk sanallaştırma araçları ve hello VM (yani VMware araçları) üzerinde yüklü aracıları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5879d-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="5879d-122">Merhaba VM olun yapılandırılmış toopull kendi IP adresini ve DNS ayarlarını DHCP yoluyla değil.</span><span class="sxs-lookup"><span data-stu-id="5879d-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="5879d-123">Bu başladığında hello sunucu hello VNet içindeki bir IP adresi alacağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5879d-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="5879d-124">Merhaba depolama hesabı edinin</span><span class="sxs-lookup"><span data-stu-id="5879d-124">Get hello storage account</span></span>
<span data-ttu-id="5879d-125">Azure toostore karşıya hello VM görüntüsündeki bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5879d-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="5879d-126">Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5879d-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="5879d-127">tooshow hello kullanılabilir depolama hesaplarını yazın:</span><span class="sxs-lookup"><span data-stu-id="5879d-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="5879d-128">Mevcut bir depolama hesabını toouse istiyorsanız, toohello devam [karşıya yükleme hello VM görüntüsü](#upload-the-vm-vhd-to-your-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5879d-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="5879d-129">Bir depolama hesabı toocreate gerekiyorsa, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5879d-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="5879d-130">Merhaba hello depolama hesabı nerede oluşturulacağını hello kaynak grubunun adını gerekir.</span><span class="sxs-lookup"><span data-stu-id="5879d-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="5879d-131">toofind, aboneliğinizdeki türü tüm hello kaynak gruplarını çıkışı:</span><span class="sxs-lookup"><span data-stu-id="5879d-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="5879d-132">bir kaynak grubu adında toocreate **myResourceGroup** hello içinde **Batı ABD** bölge, türü:</span><span class="sxs-lookup"><span data-stu-id="5879d-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="5879d-133">Adlı depolama hesabı oluşturma **mystorageaccount** hello kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5879d-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="5879d-134">Merhaba VHD tooyour depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="5879d-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="5879d-135">Kullanım hello [Ekle AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) depolama hesabınızdaki cmdlet tooupload hello görüntü tooa kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="5879d-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="5879d-136">Karşıya dosya hello Bu örnek **myVHD.vhd** gelen `"C:\Users\Public\Documents\Virtual hard disks\"` adlı tooa depolama hesabı **mystorageaccount** hello içinde **myResourceGroup** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="5879d-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="5879d-137">Merhaba dosya adlı hello kapsayıcıya yerleştirilecek **mycontainer** ve hello yeni dosya adı olacaktır **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="5879d-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="5879d-138">Başarılı olursa, benzer toothis benzeyen bir yanıt alın:</span><span class="sxs-lookup"><span data-stu-id="5879d-138">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="5879d-139">Bu komut, ağ bağlantısı ve VHD dosyanızı hello boyutuna bağlı olarak biraz zaman alabilir toocomplete.</span><span class="sxs-lookup"><span data-stu-id="5879d-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="5879d-140">Seçenek 2: Kopyalama hello mevcut bir Azure VM'i VHD'den</span><span class="sxs-lookup"><span data-stu-id="5879d-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="5879d-141">Yeni, yinelenen bir VM oluştururken, bir VHD tooanother depolama hesabı toouse kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="5879d-142">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5879d-142">Before you begin</span></span>
<span data-ttu-id="5879d-143">Olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="5879d-143">Make sure that you:</span></span>

* <span data-ttu-id="5879d-144">Merhaba ilgili bilgiler **kaynak ve hedef depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="5879d-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="5879d-145">Merhaba kaynak VM toohave hello depolama hesabı ve kapsayıcı adları olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5879d-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="5879d-146">Genellikle, hello kapsayıcı adı olacaktır **VHD'ler**.</span><span class="sxs-lookup"><span data-stu-id="5879d-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="5879d-147">Ayrıca toohave bir hedef depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5879d-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="5879d-148">Zaten yoksa, her iki hello portalı kullanarak bir tane oluşturabilirsiniz (**daha Hizmetleri** > depolama hesapları > Ekle) veya hello kullanarak [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5879d-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="5879d-149">İndirilen ve hello yüklenmiş [AzCopy aracı](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5879d-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="5879d-150">Merhaba VM serbest bırakma</span><span class="sxs-lookup"><span data-stu-id="5879d-150">Deallocate hello VM</span></span>
<span data-ttu-id="5879d-151">Merhaba kopyalanan hello VHD toobe boşaltır VM serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="5879d-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="5879d-152">**Portal**: tıklatın **sanal makineleri** > **myVM** > Durdur</span><span class="sxs-lookup"><span data-stu-id="5879d-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="5879d-153">**PowerShell**: kullanım [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) adlı VM hello **myVM** kaynak grubunda **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5879d-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="5879d-154">Merhaba **durum** hello Azure VM hello için portal değişiklikleri **durduruldu** çok**durduruldu (serbest bırakıldı)**.</span><span class="sxs-lookup"><span data-stu-id="5879d-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="5879d-155">Merhaba depolama hesabı URL'lerini alma</span><span class="sxs-lookup"><span data-stu-id="5879d-155">Get hello storage account URLs</span></span>
<span data-ttu-id="5879d-156">Merhaba kaynak ve hedef depolama hesapları hello URL'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="5879d-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="5879d-157">Merhaba URL'leri neye benzediğini gösteren: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="5879d-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="5879d-158">Merhaba depolama hesabı ve kapsayıcı adını biliyorsanız, hello köşeli toocreate arasında hello bilgi URL'nizi yalnızca değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="5879d-159">Hello Azure portalında veya Azure Powershell tooget hello URL kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5879d-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="5879d-160">**Portal**: tıklatın hello  **>**  için **daha fazla hizmet** > **depolama hesapları**  >   *Depolama hesabı* > **BLOB'lar** ve kaynak VHD dosyası büyük olasılıkla hello **VHD'ler** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="5879d-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="5879d-161">Tıklatın **özellikleri** hello kapsayıcı ve etiketli hello metin Kopyala **URL**.</span><span class="sxs-lookup"><span data-stu-id="5879d-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="5879d-162">Her iki hello kaynak ve hedef kapsayıcılarını hello URL'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="5879d-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="5879d-163">**PowerShell**: kullanım [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello bilgi adlı VM için **myVM** hello kaynak grubunda **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5879d-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="5879d-164">Merhaba sonuçlarında hello Ara **depolama profili** hello bölümüne **Vhd Uri'si**.</span><span class="sxs-lookup"><span data-stu-id="5879d-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="5879d-165">Merhaba ilk hello URI hello URL toohello kapsayıcı bir parçasıdır ve hello son hello hello VM için işletim sistemi VHD ad parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="5879d-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="5879d-166">Merhaba depolama erişim anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="5879d-166">Get hello storage access keys</span></span>
<span data-ttu-id="5879d-167">Merhaba erişim tuşları hello için kaynak ve hedef depolama hesapları bulun.</span><span class="sxs-lookup"><span data-stu-id="5879d-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="5879d-168">Erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure storage hesapları hakkında](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5879d-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="5879d-169">**Portal**: tıklatın **daha fazla hizmet** > **depolama hesapları** > *depolama hesabı*  >  **Erişim anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="5879d-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="5879d-170">Kopya hello anahtar etiketli olarak **key1**.</span><span class="sxs-lookup"><span data-stu-id="5879d-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="5879d-171">**PowerShell**: kullanım [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello depolama anahtarı hello depolama hesabı için **mystorageaccount** hello kaynak grubunda  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="5879d-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="5879d-172">Etiketli kopyalama hello anahtar **key1**.</span><span class="sxs-lookup"><span data-stu-id="5879d-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="5879d-173">Merhaba VHD kopyalayın</span><span class="sxs-lookup"><span data-stu-id="5879d-173">Copy hello VHD</span></span>
<span data-ttu-id="5879d-174">AzCopy kullanarak depolama hesapları arasında dosya kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="5879d-175">Merhaba belirtilen kapsayıcı mevcut değilse hello hedef kapsayıcı için sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5879d-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="5879d-176">toouse AzCopy, yerel makinenizde bir komut istemi açın ve AzCopy yüklendiği toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="5879d-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="5879d-177">Bu çok benzer olacaktır*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="5879d-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="5879d-178">Tüm hello dosyaları bir kapsayıcıda toocopy kullandığınız hello **/S** geçin.</span><span class="sxs-lookup"><span data-stu-id="5879d-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="5879d-179">Bu kullanılan toocopy hello OS VHD olabilir ve kullanılıyorlarsa hello veri disklerin tümü aynı kapsayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="5879d-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="5879d-180">Bu örnekte gösterilir nasıl tüm hello dosyaları hello kapsayıcısında toocopy **mysourcecontainer** depolama hesabındaki **mysourcestorageaccount** toohello kapsayıcı **mydestinationcontainer**  hello içinde **mydestinationstorageaccount** depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="5879d-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="5879d-181">Merhaba depolama hesapları ve kapsayıcıları Hello adlarını kendi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5879d-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="5879d-182">Değiştir `<sourceStorageAccountKey1>` ve `<destinationStorageAccountKey1>` kendi anahtarlara sahip.</span><span class="sxs-lookup"><span data-stu-id="5879d-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="5879d-183">Toocopy belirli bir VHD'yi bir kapsayıcıda yalnızca sahip birden çok dosya istiyorsanız, ayrıca hello /Pattern anahtar kullanılarak hello dosya adını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="5879d-184">Bu örnekte, yalnızca adlı dosya hello **myFileName.vhd** kopyalanacak.</span><span class="sxs-lookup"><span data-stu-id="5879d-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="5879d-185">Tamamlandığında, aşağıdakine benzer bir ileti alırsınız:</span><span class="sxs-lookup"><span data-stu-id="5879d-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="5879d-186">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5879d-186">Troubleshooting</span></span>
* <span data-ttu-id="5879d-187">Merhaba hatası görürseniz, AZCopy, "Sunucu tooauthenticate hello isteği başarısız oldu" kullandığınızda hello Authorization Üstbilgisi hello değeri doğru hello imza dahil olmak üzere biçimlendirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5879d-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="5879d-188">Anahtar 2 veya hello ikincil depolama anahtarı kullanıyorsanız, hello birincil ya da 1 depolama anahtarı kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5879d-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="5879d-189">Oluşturma yeni VM hello</span><span class="sxs-lookup"><span data-stu-id="5879d-189">Create hello new VM</span></span> 

<span data-ttu-id="5879d-190">Toocreate ağ ve hello tarafından kullanılan diğer VM kaynakları toobe gereken yeni VM.</span><span class="sxs-lookup"><span data-stu-id="5879d-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="5879d-191">Merhaba alt ağ ve sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="5879d-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="5879d-192">Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5879d-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="5879d-193">Merhaba alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5879d-193">Create hello subNet.</span></span> <span data-ttu-id="5879d-194">Bu örnek adlı bir alt ağı oluşturur **mySubNet**, hello kaynak grubunda **myResourceGroup**, ve ayarlar hello alt ağ adresi ön eki çok**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="5879d-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="5879d-195">Merhaba vNet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5879d-195">Create hello vNet.</span></span> <span data-ttu-id="5879d-196">Ayarlar hello sanal ağ adı toobe Bu örnek **myVnetName**, konum çok hello**Batı ABD**, ve hello sanal ağ için adres ön eki çok hello**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="5879d-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="5879d-197">Bir ortak IP adresi ve NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="5879d-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="5879d-198">ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="5879d-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="5879d-199">Merhaba genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5879d-199">Create hello public IP.</span></span> <span data-ttu-id="5879d-200">Bu örnekte hello ortak IP adresi adı çok ayarlanır**myIP**.</span><span class="sxs-lookup"><span data-stu-id="5879d-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="5879d-201">Merhaba NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="5879d-201">Create hello NIC.</span></span> <span data-ttu-id="5879d-202">Bu örnekte, hello NIC adı çok ayarlanır**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="5879d-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="5879d-203">Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5879d-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="5879d-204">toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir güvenlik kuralı gerekir.</span><span class="sxs-lookup"><span data-stu-id="5879d-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="5879d-205">Yeni VM mevcut bir oluşturulduğu hello Merhaba VHD özelleştirilmiş çünkü hello VM, oluşturulduktan sonra VM hello kaynak sanal makineden RDP kullanma izni toolog sahip var olan bir hesap kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="5879d-206">Bu örnek kümeleri hello NSG adı çok**myNsg** ve hello RDP kural adı çok**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="5879d-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="5879d-207">Uç noktaları ve NSG kuralları hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5879d-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="5879d-208">Merhaba sanal makine adını ve boyutunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="5879d-208">Set hello VM name and size</span></span>

<span data-ttu-id="5879d-209">Ayarlar hello VM adını bu örnek çok "myVM" ve hello VM çok boyutu "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="5879d-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="5879d-210">Merhaba NIC ekleme</span><span class="sxs-lookup"><span data-stu-id="5879d-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="5879d-211">Merhaba işletim sistemi diski yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5879d-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="5879d-212">Merhaba URI hello karşıya veya kopyalanan VHD için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5879d-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="5879d-213">Bu örnekte, VHD dosyası adlı hello **myOsDisk.vhd** adlı bir depolama hesabında tutulur **myStorageAccount** adlı bir kapsayıcıda **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="5879d-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="5879d-214">Merhaba işletim sistemi diski ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5879d-214">Add hello OS disk.</span></span> <span data-ttu-id="5879d-215">Hello işletim sistemi diski oluşturulduğunda bu örnekte, appened toohello VM toocreate hello işletim sistemi disk adı hello terimi "osDisk" şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="5879d-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="5879d-216">Bu örnek ayrıca bu Windows tabanlı VHD ekli toohello hello işletim sistemi diski olarak VM olması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5879d-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="5879d-217">İsteğe bağlı: veri diski varsa, bu gereksinimi toobe toohello VM ekli veri VHD'ler hello URL'leri kullanarak hello veri diski ekleyin ve uygun mantıksal birim numarası (Lun) hello.</span><span class="sxs-lookup"><span data-stu-id="5879d-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="5879d-218">Bir depolama hesabı kullanılırken hello veri ve işletim sistemi disk URL'leri aşağıdaki gibi görünmelidir: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="5879d-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="5879d-219">Bu hello portalında toohello hedef depolama kapsayıcısı hello işletim sistemi veya veri kopyalanan VHD tıklatarak, tarama ve hello URL Merhaba içeriğine kopyalama bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5879d-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="5879d-220">Tam hello VM</span><span class="sxs-lookup"><span data-stu-id="5879d-220">Complete hello VM</span></span> 

<span data-ttu-id="5879d-221">Oluşturma yeni oluşturduğumuz hello yapılandırmaları kullanarak VM hello.</span><span class="sxs-lookup"><span data-stu-id="5879d-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="5879d-222">Bu komutun başarılı olduysa, benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="5879d-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="5879d-223">VM oluşturulduğu bu hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="5879d-223">Verify that hello VM was created</span></span>
<span data-ttu-id="5879d-224">Merhaba yeni oluşturulan VM ya da hello görmelisiniz [Azure portal](https://portal.azure.com)altında **Gözat** > **sanal makineleri**, veya PowerShell aşağıdaki hello kullanarak komutlar:</span><span class="sxs-lookup"><span data-stu-id="5879d-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="5879d-225">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5879d-225">Next steps</span></span>
<span data-ttu-id="5879d-226">tooyour yeni sanal makine, hello içinde Gözat toohello VM toosign [portal](https://portal.azure.com), tıklatın **Bağlan**ve açık hello Uzak Masaüstü RDP dosyası.</span><span class="sxs-lookup"><span data-stu-id="5879d-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="5879d-227">Özgün sanal makine toosign Hello hesabı kimlik bilgilerini tooyour yeni sanal makinede kullanın.</span><span class="sxs-lookup"><span data-stu-id="5879d-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="5879d-228">Daha fazla bilgi için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="5879d-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

