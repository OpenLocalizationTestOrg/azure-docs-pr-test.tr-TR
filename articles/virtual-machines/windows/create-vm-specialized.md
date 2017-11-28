---
title: "bir Windows VM Azure özelleştirilmiş bir VHD'den aaaCreate | Microsoft Docs"
description: "Yeni bir Windows VM hello Resource Manager dağıtım modeli kullanılarak hello işletim sistemi diski olarak özel bir yönetilen disk ekleyerek oluşturun."
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
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="f4183-103">Özelleştirilmiş bir diskten bir Windows VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4183-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="f4183-104">Powershell kullanarak hello işletim sistemi diski olarak özel bir yönetilen disk ekleyerek yeni bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4183-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="f4183-105">Özelleştirilmiş bir disk hello kullanıcı hesapları, uygulamaları ve diğer Durum verilerini orijinal VM tutar mevcut bir VM'yi sanal sabit disk (VHD) bir kopyasını arasındadır.</span><span class="sxs-lookup"><span data-stu-id="f4183-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="f4183-106">Özel bir VHD toocreate yeni bir VM kullandığınızda, yeni VM hello bilgisayar adını korur hello özgün VM hello.</span><span class="sxs-lookup"><span data-stu-id="f4183-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="f4183-107">Diğer bilgisayar özgü bilgiler de olması tutulur ve bazı durumlarda, bu yinelenen bilgiler sorunlara neden.</span><span class="sxs-lookup"><span data-stu-id="f4183-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="f4183-108">Ne tür bilgisayara özgü bilgileri uygulamalarınızı VM kopyalarken kullanır dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f4183-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="f4183-109">İki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="f4183-109">You have two options:</span></span>
* [<span data-ttu-id="f4183-110">Bir VHD’yi karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="f4183-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="f4183-111">Mevcut bir Azure VM'yi kopyalama</span><span class="sxs-lookup"><span data-stu-id="f4183-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="f4183-112">Bu konu toouse diskleri nasıl yönetileceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4183-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="f4183-113">Eski dağıtım varsa gerektiren bir depolama hesabı kullanarak, bkz: [depolama hesabındaki özelleştirilmiş bir VHD'den bir VM oluşturma](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="f4183-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f4183-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="f4183-114">Before you begin</span></span>
<span data-ttu-id="f4183-115">PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f4183-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="f4183-116">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4183-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="f4183-117">Seçenek 1: özel bir VHD yüklemek</span><span class="sxs-lookup"><span data-stu-id="f4183-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="f4183-118">Hyper-V ya da VM başka bir buluttan dışarı gibi bir şirket içi sanallaştırma aracı ile özel bir VM VHD'den oluşturulan hello karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4183-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="f4183-119">Merhaba VM hazırlama</span><span class="sxs-lookup"><span data-stu-id="f4183-119">Prepare hello VM</span></span>
<span data-ttu-id="f4183-120">Toouse düşünüyorsanız, VHD olarak hello-toocreate yeni bir VM olan aşağıdaki adımları hello tamamlanır emin olun.</span><span class="sxs-lookup"><span data-stu-id="f4183-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="f4183-121">[Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4183-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f4183-122">**Sağlamadığı** generalize Sysprep kullanarak VM hello.</span><span class="sxs-lookup"><span data-stu-id="f4183-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="f4183-123">Konuk sanallaştırma araçları ve hello VM (gibi VMware araçları) yüklenmiş aracıları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f4183-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="f4183-124">Merhaba VM olun yapılandırılmış toopull kendi IP adresini ve DNS ayarlarını DHCP yoluyla değil.</span><span class="sxs-lookup"><span data-stu-id="f4183-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="f4183-125">Bu başladığında hello sunucu hello VNet içindeki bir IP adresi alacağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f4183-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="f4183-126">Merhaba depolama hesabı edinin</span><span class="sxs-lookup"><span data-stu-id="f4183-126">Get hello storage account</span></span>
<span data-ttu-id="f4183-127">Bir depolama alanına ihtiyacınız Azure toostore hello hesabında karşıya VHD.</span><span class="sxs-lookup"><span data-stu-id="f4183-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="f4183-128">Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4183-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="f4183-129">tooshow hello kullanılabilir depolama hesaplarını yazın:</span><span class="sxs-lookup"><span data-stu-id="f4183-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="f4183-130">Mevcut bir depolama hesabını toouse istiyorsanız, toohello devam [karşıya yükleme hello VHD](#upload-the-vhd-to-your-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="f4183-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="f4183-131">Bir depolama hesabı toocreate gerekiyorsa, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f4183-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="f4183-132">Merhaba hello depolama hesabı nerede oluşturulacağını hello kaynak grubunun adını gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4183-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="f4183-133">toofind, aboneliğinizdeki türü tüm hello kaynak gruplarını çıkışı:</span><span class="sxs-lookup"><span data-stu-id="f4183-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="f4183-134">bir kaynak grubu adında toocreate *myResourceGroup* hello içinde *Batı ABD* bölge, türü:</span><span class="sxs-lookup"><span data-stu-id="f4183-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="f4183-135">Adlı depolama hesabı oluşturma *mystorageaccount* hello kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f4183-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="f4183-136">Merhaba VHD tooyour depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="f4183-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="f4183-137">Kullanım hello [Ekle AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) depolama hesabınızdaki cmdlet tooupload hello VHD tooa kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="f4183-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="f4183-138">Karşıya dosya hello Bu örnek *myVHD.vhd* gelen `"C:\Users\Public\Documents\Virtual hard disks\"` adlı tooa depolama hesabı *mystorageaccount* hello içinde *myResourceGroup* kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="f4183-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="f4183-139">Merhaba dosya adlı hello kapsayıcısında depolanır *mycontainer* ve hello yeni dosya adı olacaktır *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="f4183-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="f4183-140">Başarılı olursa, benzer toothis benzeyen bir yanıt alın:</span><span class="sxs-lookup"><span data-stu-id="f4183-140">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="f4183-141">Bu komut, ağ bağlantısı ve VHD dosyanızı hello boyutuna bağlı olarak biraz zaman alabilir toocomplete</span><span class="sxs-lookup"><span data-stu-id="f4183-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="f4183-142">VHD hello yönetilen bir disk oluşturun</span><span class="sxs-lookup"><span data-stu-id="f4183-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="f4183-143">Hello yönetilen bir disk oluşturma, depolama hesabı kullanarak VHD özelleştirilmiş [yeni AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="f4183-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="f4183-144">Bu örnekte **myOSDisk1** hello disk adı için disk yerleştirmelerin hello *StandardLRS* depolama ve kullandığı *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* hello kaynak VHD URI hello gibi.</span><span class="sxs-lookup"><span data-stu-id="f4183-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="f4183-145">Hello için yeni bir kaynak grubu oluşturma yeni VM.</span><span class="sxs-lookup"><span data-stu-id="f4183-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="f4183-146">Oluşturma hello yeni işletim sistemi diskinden hello karşıya VHD.</span><span class="sxs-lookup"><span data-stu-id="f4183-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="f4183-147">Seçenek 2: mevcut bir Azure VM'yi kopyalama</span><span class="sxs-lookup"><span data-stu-id="f4183-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="f4183-148">Bir hello VM anlık görüntüsü tarafından yönetilen disklerde kullanır ve ardından bu anlık görüntü toocreate kullanarak yeni bir disk ve yeni bir VM yönetilen VM bir kopyasını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4183-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="f4183-149">Merhaba işletim sistemi diski bir anlık görüntüsünü</span><span class="sxs-lookup"><span data-stu-id="f4183-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="f4183-150">(Tüm diskler dahil), anlık görüntü ve tüm VM alabilir veya yalnızca tek bir disk.</span><span class="sxs-lookup"><span data-stu-id="f4183-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="f4183-151">Merhaba aşağıdaki adımlar, nasıl tootake bir anlık görüntü yalnızca VM kullanmanın hello işletim sistemi diskinin hello gösterir [yeni AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="f4183-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="f4183-152">Bazı parametreler ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4183-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="f4183-153">Merhaba VM nesnesini alın.</span><span class="sxs-lookup"><span data-stu-id="f4183-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="f4183-154">Merhaba işletim sistemi disk adı alın.</span><span class="sxs-lookup"><span data-stu-id="f4183-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="f4183-155">Başlangıç anlık görüntü yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4183-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="f4183-156">Başlangıç anlık görüntü alın.</span><span class="sxs-lookup"><span data-stu-id="f4183-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="f4183-157">Toouse hello anlık görüntü toocreate toobe yüksek performanslı gereken VM planlıyorsanız, hello parametresini kullanın `-AccountType Premium_LRS` hello yeni AzureRmSnapshot komutu.</span><span class="sxs-lookup"><span data-stu-id="f4183-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="f4183-158">Merhaba parametre hello anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır.</span><span class="sxs-lookup"><span data-stu-id="f4183-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="f4183-159">Premium yönetilen diskleri standart daha pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="f4183-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="f4183-160">Bu nedenle, Premium hello parametre kullanmadan önce gerçekten emin olun.</span><span class="sxs-lookup"><span data-stu-id="f4183-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="f4183-161">Merhaba anlık görüntüden yeni bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4183-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="f4183-162">Yönetilen bir disk kullanarak anlık görüntü hello oluşturma [yeni AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="f4183-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="f4183-163">Bu örnekte *myOSDisk* hello disk adı.</span><span class="sxs-lookup"><span data-stu-id="f4183-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="f4183-164">Hello için yeni bir kaynak grubu oluşturma yeni VM.</span><span class="sxs-lookup"><span data-stu-id="f4183-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="f4183-165">Merhaba işletim sistemi disk adı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4183-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="f4183-166">Merhaba yönetilen diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4183-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="f4183-167">Oluşturma yeni VM hello</span><span class="sxs-lookup"><span data-stu-id="f4183-167">Create hello new VM</span></span> 

<span data-ttu-id="f4183-168">Ağ ve hello tarafından kullanılan diğer VM kaynakları toobe oluşturmak yeni VM.</span><span class="sxs-lookup"><span data-stu-id="f4183-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="f4183-169">Merhaba alt ağ ve sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4183-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="f4183-170">Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4183-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="f4183-171">Merhaba alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4183-171">Create hello subNet.</span></span> <span data-ttu-id="f4183-172">Bu örnek adlı bir alt ağı oluşturur **mySubNet**, hello kaynak grubunda **myDestinationResourceGroup**, ve ayarlar hello alt ağ adresi ön eki çok**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="f4183-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="f4183-173">Merhaba vNet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4183-173">Create hello vNet.</span></span> <span data-ttu-id="f4183-174">Ayarlar hello sanal ağ adı toobe Bu örnek **myVnetName**, konum çok hello**Batı ABD**, ve hello sanal ağ için adres ön eki çok hello**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="f4183-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="f4183-175">Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4183-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="f4183-176">toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir güvenlik kuralı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4183-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="f4183-177">Çünkü yeni VM, var olan bir özel sanal makineden oluşturulduğu hello için VHD Merhaba, RDP hello kaynak sanal makineden bir hesap kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4183-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="f4183-178">Bu örnek kümeleri hello NSG adı çok**myNsg** ve hello RDP kural adı çok**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="f4183-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="f4183-179">Uç noktaları ve NSG kuralları hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f4183-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="f4183-180">Bir ortak IP adresi ve NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="f4183-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="f4183-181">ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="f4183-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="f4183-182">Merhaba genel IP oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4183-182">Create hello public IP.</span></span> <span data-ttu-id="f4183-183">Bu örnekte hello ortak IP adresi adı çok ayarlanır**myIP**.</span><span class="sxs-lookup"><span data-stu-id="f4183-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="f4183-184">Merhaba NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="f4183-184">Create hello NIC.</span></span> <span data-ttu-id="f4183-185">Bu örnekte, hello NIC adı çok ayarlanır**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="f4183-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="f4183-186">Merhaba sanal makine adını ve boyutunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="f4183-186">Set hello VM name and size</span></span>

<span data-ttu-id="f4183-187">Bu örnek kümeleri hello VM adı çok*myVM* ve hello VM boyutu çok*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="f4183-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="f4183-188">Merhaba NIC ekleme</span><span class="sxs-lookup"><span data-stu-id="f4183-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="f4183-189">Merhaba işletim sistemi disk ekleme</span><span class="sxs-lookup"><span data-stu-id="f4183-189">Add hello OS disk</span></span> 

<span data-ttu-id="f4183-190">Merhaba işletim sistemi disk yapılandırması toohello kullanılarak eklemek [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="f4183-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="f4183-191">Bu örnek hello hello disk boyutunu çok ayarlar*128 GB* ekler hello yönetilen diski olarak ve bir *Windows* işletim sistemi diski.</span><span class="sxs-lookup"><span data-stu-id="f4183-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="f4183-192">Tam hello VM</span><span class="sxs-lookup"><span data-stu-id="f4183-192">Complete hello VM</span></span> 

<span data-ttu-id="f4183-193">VM Hello kullanarak oluşturduğunuz [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello yeni oluşturduğumuz yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="f4183-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="f4183-194">Bu komutun başarılı olduysa, benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="f4183-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="f4183-195">VM oluşturulduğu bu hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="f4183-195">Verify that hello VM was created</span></span>
<span data-ttu-id="f4183-196">Merhaba yeni oluşturulan VM ya da hello görmelisiniz [Azure portal](https://portal.azure.com)altında **Gözat** > **sanal makineleri**, veya PowerShell aşağıdaki hello kullanarak komutlar:</span><span class="sxs-lookup"><span data-stu-id="f4183-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="f4183-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f4183-197">Next steps</span></span>
<span data-ttu-id="f4183-198">tooyour yeni sanal makine, hello içinde Gözat toohello VM toosign [portal](https://portal.azure.com), tıklatın **Bağlan**ve açık hello Uzak Masaüstü RDP dosyası.</span><span class="sxs-lookup"><span data-stu-id="f4183-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="f4183-199">Özgün sanal makine toosign Hello hesabı kimlik bilgilerini tooyour yeni sanal makinede kullanın.</span><span class="sxs-lookup"><span data-stu-id="f4183-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="f4183-200">Daha fazla bilgi için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="f4183-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

