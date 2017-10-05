---
title: "Yönetilen bir görüntü oluşturma | Microsoft Docs"
description: "Genelleştirilmiş bir VM veya VHD yönetilen bir görüntüsünü oluşturma. Görüntüleri yönetilen diskler kullanan birden çok VM oluşturmak için kullanılabilir."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="20906-104">Yönetilen bir genelleştirilmiş bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="20906-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="20906-105">Yönetilen görüntü kaynağı olarak yönetilen bir disk veya yönetilmeyen bir disk depolama hesabında depolanan genelleştirilmiş bir VM oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="20906-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="20906-106">Görüntü sonra birden çok VM oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="20906-106">The image can then be used to create multiple VMs.</span></span> 


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="20906-107">Sysprep kullanarak Windows VM generalize</span><span class="sxs-lookup"><span data-stu-id="20906-107">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="20906-108">Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılacak makine hazırlar.</span><span class="sxs-lookup"><span data-stu-id="20906-108">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="20906-109">Sysprep hakkında daha fazla ayrıntı için bkz: [kullanım Sysprep nasıl: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="20906-109">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="20906-110">Makinede çalışan sunucu rollerini Sysprep tarafından desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="20906-110">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="20906-111">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="20906-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20906-112">Sysprep, VHD Azure'a ilk kez karşıya yüklemeden önce çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce.</span><span class="sxs-lookup"><span data-stu-id="20906-112">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="20906-113">Windows sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="20906-113">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="20906-114">Bir yönetici olarak komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="20906-114">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="20906-115">Dizinine değiştirin **%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="20906-115">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="20906-116">İçinde **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**, emin olun **Generalize** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="20906-116">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="20906-117">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="20906-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="20906-118">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20906-118">Click **OK**.</span></span>
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="20906-120">Sysprep tamamlandığında, sanal makineyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="20906-120">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="20906-121">VM yeniden başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="20906-121">Do not restart the VM.</span></span>


## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="20906-122">Portalda yönetilen bir görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="20906-122">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="20906-123">Açık [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20906-123">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="20906-124">Yeni bir kaynak oluşturmak için artı işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="20906-124">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="20906-125">Filtre Ara yazın **görüntü**.</span><span class="sxs-lookup"><span data-stu-id="20906-125">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="20906-126">Seçin **görüntü** sonuçlarından.</span><span class="sxs-lookup"><span data-stu-id="20906-126">Select **Image** from the results.</span></span>
5. <span data-ttu-id="20906-127">İçinde **görüntü** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20906-127">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="20906-128">İçinde **adı**, görüntü için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="20906-128">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="20906-129">Birden fazla aboneliğiniz varsa doğru makineden seçin **abonelik** açılır.</span><span class="sxs-lookup"><span data-stu-id="20906-129">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="20906-130">İçinde **kaynak grubu** ya da seçin **Yeni Oluştur** ve bir ad yazın veya seçin **varolan** ve aşağı açılan listeden kullanmak için bir kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="20906-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="20906-131">İçinde **konumu**, kaynak grubu konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="20906-131">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="20906-132">İçinde **işletim sistemi türü** Windows ya da Linux işletim sistemi türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="20906-132">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="20906-133">İçinde **depolama blobu**, tıklatın **Gözat** Azure depolama alanınızı VHD aramak için.</span><span class="sxs-lookup"><span data-stu-id="20906-133">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="20906-134">İçinde **hesap türü** Standard_LRS veya Premium_LRS seçin.</span><span class="sxs-lookup"><span data-stu-id="20906-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="20906-135">Standart sabit disk sürücüleri ve Premium katı hal sürücüleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="20906-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="20906-136">Hem yerel olarak yedekli depolama kullanın.</span><span class="sxs-lookup"><span data-stu-id="20906-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="20906-137">İçinde **Disk önbelleği** seçeneği önbelleğe alma için uygun diski seçin.</span><span class="sxs-lookup"><span data-stu-id="20906-137">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="20906-138">Seçenekler şunlardır: **hiçbiri**, **salt okunur** ve **sürücüsünde**.</span><span class="sxs-lookup"><span data-stu-id="20906-138">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="20906-139">İsteğe bağlı: Da varolan bir veri diski görüntüye tıklayarak ekleyebilirsiniz **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="20906-139">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="20906-140">İşiniz bittiğinde seçimlerinizi yaptıktan tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20906-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="20906-141">Görüntü oluşturulduktan sonra bunu olarak görür bir **görüntü** kaynak seçtiğiniz kaynak grubundaki kaynaklar listesinde.</span><span class="sxs-lookup"><span data-stu-id="20906-141">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="20906-142">Yönetilen bir Powershell kullanarak bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="20906-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="20906-143">Doğrudan sanal makineden bir görüntü oluşturma görüntünün işletim sistemi diski ve veri diskleri gibi VM ile ilişkili tüm diskleri içeren sağlar.</span><span class="sxs-lookup"><span data-stu-id="20906-143">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="20906-144">Başlamadan önce AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="20906-144">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="20906-145">Yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="20906-145">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="20906-146">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20906-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="20906-147">Bazı değişkenler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20906-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="20906-148">VM serbest emin olun.</span><span class="sxs-lookup"><span data-stu-id="20906-148">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="20906-149">Sanal makine durumunu ayarlamak **Genelleştirmiş**.</span><span class="sxs-lookup"><span data-stu-id="20906-149">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="20906-150">Sanal makine Al.</span><span class="sxs-lookup"><span data-stu-id="20906-150">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="20906-151">Görüntü yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20906-151">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="20906-152">Görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="20906-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="20906-153">PowerShell'de yönetilen bir VHD görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="20906-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="20906-154">Genelleştirilmiş OS VHD kullanılarak yönetilen bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20906-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="20906-155">İlk olarak, ortak parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="20906-155">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="20906-156">Step\deallocate VM.</span><span class="sxs-lookup"><span data-stu-id="20906-156">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="20906-157">VM genelleştirilmiş olarak işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="20906-157">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="20906-158">Genelleştirilmiş OS VHD kullanarak görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="20906-158">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="20906-159">Powershell kullanarak bir anlık görüntüden yönetilen bir görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="20906-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="20906-160">Genelleştirilmiş bir VM VHD'den görüntüsünü yönetilen resim de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20906-160">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="20906-161">Bazı değişkenler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20906-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="20906-162">Anlık görüntü alın.</span><span class="sxs-lookup"><span data-stu-id="20906-162">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="20906-163">Görüntü yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20906-163">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="20906-164">Görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="20906-164">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="20906-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20906-165">Next steps</span></span>
- <span data-ttu-id="20906-166">Artık [bir VM genelleştirilmiş yönetilen görüntüden oluşturma](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20906-166">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

