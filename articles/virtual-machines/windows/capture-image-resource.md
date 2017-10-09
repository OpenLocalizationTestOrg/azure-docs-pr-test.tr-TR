---
title: "Azure yönetilen görüntüde aaaCreate | Microsoft Docs"
description: "Genelleştirilmiş bir VM veya VHD yönetilen bir görüntüsünü oluşturma. Görüntüleri kullanılan toocreate yönetilen diskler kullanan birden çok VM olabilir."
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
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="794af-104">Yönetilen bir genelleştirilmiş bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="794af-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="794af-105">Yönetilen görüntü kaynağı olarak yönetilen bir disk veya yönetilmeyen bir disk depolama hesabında depolanan genelleştirilmiş bir VM oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="794af-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="794af-106">Görüntü can hello sonra birden çok VM kullanılan toocreate olabilir.</span><span class="sxs-lookup"><span data-stu-id="794af-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="794af-107">Generalize Sysprep kullanarak Windows VM hello</span><span class="sxs-lookup"><span data-stu-id="794af-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="794af-108">Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar.</span><span class="sxs-lookup"><span data-stu-id="794af-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="794af-109">Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="794af-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="794af-110">Merhaba makine üzerinde çalışan hello sunucu rolleri Sysprep tarafından desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="794af-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="794af-111">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="794af-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="794af-112">Sysprep, VHD tooAzure hello için karşıya yüklemeden önce ilk kez çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce.</span><span class="sxs-lookup"><span data-stu-id="794af-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="794af-113">Windows sanal makine içinde toohello imzalayın.</span><span class="sxs-lookup"><span data-stu-id="794af-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="794af-114">Merhaba komut istemi penceresi bir yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="794af-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="794af-115">Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="794af-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="794af-116">Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**ve bu hello emin olun **Generalize** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="794af-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="794af-117">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="794af-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="794af-118">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="794af-118">Click **OK**.</span></span>
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="794af-120">Sysprep tamamlandığında hello sanal makineyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="794af-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="794af-121">Merhaba VM yeniden başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="794af-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="794af-122">Merhaba Portalı'nda yönetilen bir görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="794af-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="794af-123">Açık hello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="794af-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="794af-124">Yeni bir kaynak artı toocreate hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="794af-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="794af-125">Merhaba filtre ara yazın **görüntü**.</span><span class="sxs-lookup"><span data-stu-id="794af-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="794af-126">Seçin **görüntü** hello sonuçlarından.</span><span class="sxs-lookup"><span data-stu-id="794af-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="794af-127">Merhaba, **görüntü** dikey penceresinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="794af-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="794af-128">İçinde **adı**, hello görüntü için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="794af-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="794af-129">Birden fazla aboneliğiniz varsa, select hello doğru bir hello **abonelik** açılır.</span><span class="sxs-lookup"><span data-stu-id="794af-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="794af-130">İçinde **kaynak grubu** ya da seçin **Yeni Oluştur** ve bir ad yazın veya seçin **varolan** ve kaynak grubu toouse hello aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="794af-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="794af-131">İçinde **konumu**, kaynak grubunuz hello konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="794af-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="794af-132">İçinde **işletim sistemi türü** işletim sistemi, Windows veya Linux hello türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="794af-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="794af-133">İçinde **depolama blobu**, tıklatın **Gözat** toolook Azure depolama alanınızı hello VHD için.</span><span class="sxs-lookup"><span data-stu-id="794af-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="794af-134">İçinde **hesap türü** Standard_LRS veya Premium_LRS seçin.</span><span class="sxs-lookup"><span data-stu-id="794af-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="794af-135">Standart sabit disk sürücüleri ve Premium katı hal sürücüleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="794af-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="794af-136">Hem yerel olarak yedekli depolama kullanın.</span><span class="sxs-lookup"><span data-stu-id="794af-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="794af-137">İçinde **Disk önbelleği** hello önbelleğe uygun diski seçin.</span><span class="sxs-lookup"><span data-stu-id="794af-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="794af-138">Başlangıç Seçenekleri **hiçbiri**, **salt okunur** ve **sürücüsünde**.</span><span class="sxs-lookup"><span data-stu-id="794af-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="794af-139">İsteğe bağlı: Da var olan bir veri diski toohello görüntüsünü tıklayarak ekleyebilirsiniz **+ Ekle veri diski**.</span><span class="sxs-lookup"><span data-stu-id="794af-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="794af-140">İşiniz bittiğinde seçimlerinizi yaptıktan tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="794af-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="794af-141">Merhaba görüntü oluşturulduktan sonra bunu olarak görür bir **görüntü** kaynak hello Seçtiğiniz hello kaynak grubundaki kaynaklar listesinde.</span><span class="sxs-lookup"><span data-stu-id="794af-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="794af-142">Yönetilen bir Powershell kullanarak bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="794af-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="794af-143">Doğrudan VM, hello görüntü sağlar hello bir görüntü oluşturmayı hello hello işletim sistemi diski ve veri diskleri gibi VM ile ilişkili hello disklerin tümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="794af-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="794af-144">Başlamadan önce hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="794af-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="794af-145">Çalıştırma hello komut tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="794af-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="794af-146">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="794af-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="794af-147">Bazı değişkenler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="794af-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="794af-148">VM serbest emin hello olun.</span><span class="sxs-lookup"><span data-stu-id="794af-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="794af-149">Hello sanal makinenin başlangıç durumu çok Ayarla**Genelleştirmiş**.</span><span class="sxs-lookup"><span data-stu-id="794af-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="794af-150">Merhaba sanal makine alın.</span><span class="sxs-lookup"><span data-stu-id="794af-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="794af-151">Merhaba görüntü yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="794af-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="794af-152">Merhaba görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="794af-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="794af-153">PowerShell'de yönetilen bir VHD görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="794af-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="794af-154">Genelleştirilmiş OS VHD kullanılarak yönetilen bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="794af-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="794af-155">İlk olarak, hello ortak parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="794af-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="794af-156">Step\deallocate hello VM.</span><span class="sxs-lookup"><span data-stu-id="794af-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="794af-157">Merhaba VM genelleştirilmiş olarak işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="794af-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="794af-158">Genelleştirilmiş OS VHD kullanarak hello görüntüsü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="794af-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="794af-159">Powershell kullanarak bir anlık görüntüden yönetilen bir görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="794af-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="794af-160">Bir anlık görüntüsünü hello genelleştirilmiş VM VHD'den yönetilen resim de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="794af-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="794af-161">Bazı değişkenler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="794af-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="794af-162">Başlangıç anlık görüntü alın.</span><span class="sxs-lookup"><span data-stu-id="794af-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="794af-163">Merhaba görüntü yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="794af-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="794af-164">Merhaba görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="794af-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="794af-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="794af-165">Next steps</span></span>
- <span data-ttu-id="794af-166">Artık [genelleştirilmiş hello yönetilen görüntüsünden bir VM oluşturma](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="794af-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

