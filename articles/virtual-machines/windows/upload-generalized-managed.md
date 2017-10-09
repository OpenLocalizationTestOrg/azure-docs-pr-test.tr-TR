---
title: "yönetilen bir Azure VM genelleştirilmiş şirket içi VHD'den aaaCreate | Microsoft Docs"
description: "Genelleştirilmiş bir VHD tooAzure karşıya yükleme ve toocreate kullanmak hello Resource Manager dağıtım modelinde yeni VM'ler."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="9cea9-103">Genelleştirilmiş bir VHD yüklemek ve toocreate kullanmak azure'da yeni VM</span><span class="sxs-lookup"><span data-stu-id="9cea9-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="9cea9-104">Bu konu, PowerShell tooupload kullanılarak üzerinden genelleştirilmiş bir VM tooAzure VHD'sini açıklanmaktadır, VHD hello bir görüntü oluşturun ve bu görüntüden yeni bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="9cea9-105">Bir şirket içi sanallaştırma aracı ya da başka bir bulut dışa aktarılan bir VHD'yi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cea9-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="9cea9-106">Kullanarak [yönetilen diskleri](managed-disks-overview.md) hello yeni VM hello VM yönetimini basitleştirir ve bir kullanılabilirlik kümesine hello VM yerleştirildiğinde daha iyi kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="9cea9-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="9cea9-107">Toouse bir örnek komut dosyası istiyorsanız, bkz: [örnek komut dosyası tooupload VHD tooAzure ve yeni bir VM oluşturun](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="9cea9-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9cea9-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="9cea9-108">Before you begin</span></span>

- <span data-ttu-id="9cea9-109">Tüm VHD tooAzure karşıya yüklemeden önce uygulamanız gereken [Windows VHD veya VHDX tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9cea9-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="9cea9-110">Gözden geçirme [planlama hello geçiş için tooManaged diskleri](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) çok geçişinizi başlatmadan önce[yönetilen diskleri](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cea9-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="9cea9-111">Merhaba AzureRM.Compute PowerShell modülü hello en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="9cea9-112">Çalıştırma hello komut tooinstall onu.</span><span class="sxs-lookup"><span data-stu-id="9cea9-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="9cea9-113">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9cea9-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="9cea9-114">Generalize Sysprep kullanarak Windows VM hello</span><span class="sxs-lookup"><span data-stu-id="9cea9-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="9cea9-115">Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar.</span><span class="sxs-lookup"><span data-stu-id="9cea9-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="9cea9-116">Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="9cea9-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="9cea9-117">Merhaba makine üzerinde çalışan hello sunucu rolleri Sysprep tarafından desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="9cea9-118">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="9cea9-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cea9-119">Sysprep, VHD tooAzure hello için karşıya yüklemeden önce ilk kez çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce.</span><span class="sxs-lookup"><span data-stu-id="9cea9-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="9cea9-120">Windows sanal makine içinde toohello imzalayın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="9cea9-121">Merhaba komut istemi penceresi bir yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="9cea9-122">Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="9cea9-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="9cea9-123">Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**ve bu hello emin olun **Generalize** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="9cea9-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="9cea9-124">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="9cea9-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="9cea9-125">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-125">Click **OK**.</span></span>
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="9cea9-127">Sysprep tamamlandığında hello sanal makineyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="9cea9-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="9cea9-128">Merhaba VM yeniden başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="9cea9-129">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="9cea9-129">Log in tooAzure</span></span>
<span data-ttu-id="9cea9-130">PowerShell sürüm 1.4 zaten yoksa veya üstü yüklü okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9cea9-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="9cea9-131">Azure PowerShell'i açın ve tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="9cea9-132">Açılır pencere, tooenter Azure hesabı kimlik bilgilerinizi açar.</span><span class="sxs-lookup"><span data-stu-id="9cea9-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="9cea9-133">Merhaba abonelik kimlikleri kullanılabilir aboneliklerinizi alın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="9cea9-134">Merhaba doğru aboneliğin Hello abonelik kimliğini kullanarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="9cea9-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="9cea9-135">Değiştir  *<subscriptionID>*  hello hello Kimliğine sahip abonelik düzeltin.</span><span class="sxs-lookup"><span data-stu-id="9cea9-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="9cea9-136">Merhaba depolama hesabı edinin</span><span class="sxs-lookup"><span data-stu-id="9cea9-136">Get hello storage account</span></span>
<span data-ttu-id="9cea9-137">Azure toostore karşıya hello VM görüntüsündeki bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cea9-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="9cea9-138">Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="9cea9-139">Merhaba VHD toocreate yönetilen bir disk için bir VM kullanacaksa, hello depolama hesap konumu burada hello VM oluşturma aynı hello konumu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9cea9-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="9cea9-140">tooshow hello kullanılabilir depolama hesaplarını yazın:</span><span class="sxs-lookup"><span data-stu-id="9cea9-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="9cea9-141">Mevcut bir depolama hesabını toouse istiyorsanız, toohello devam [karşıya yükleme hello VM görüntüsü](#upload-the-vm-vhd-to-your-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9cea9-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="9cea9-142">Bir depolama hesabı toocreate gerekiyorsa, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="9cea9-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="9cea9-143">Merhaba hello depolama hesabı nerede oluşturulacağını hello kaynak grubunun adını gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cea9-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="9cea9-144">toofind, aboneliğinizdeki türü tüm hello kaynak gruplarını çıkışı:</span><span class="sxs-lookup"><span data-stu-id="9cea9-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="9cea9-145">bir kaynak grubu adında toocreate **myResourceGroup** hello içinde **Doğu ABD** bölge, türü:</span><span class="sxs-lookup"><span data-stu-id="9cea9-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="9cea9-146">Adlı depolama hesabı oluşturma **mystorageaccount** hello kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9cea9-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="9cea9-147">-SkuName için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9cea9-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="9cea9-148">**Standard_LRS** -yerel olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="9cea9-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="9cea9-149">**Standard_ZRS** -bölge olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="9cea9-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="9cea9-150">**Standard_GRS** -coğrafi olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="9cea9-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="9cea9-151">**Standard_RAGRS** -coğrafi olarak yedekli depolamaya okuma erişimi.</span><span class="sxs-lookup"><span data-stu-id="9cea9-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="9cea9-152">**Premium_LRS** -Premium yerel olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="9cea9-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="9cea9-153">Merhaba VHD tooyour depolama hesabı karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="9cea9-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="9cea9-154">Kullanım hello [Ekle AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) depolama hesabınızdaki cmdlet tooupload hello VHD tooa kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="9cea9-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="9cea9-155">Karşıya dosya hello Bu örnek *myVHD.vhd* gelen *"C:\Users\Public\Documents\Virtual sabit diskleri\"*  adlı tooa depolama hesabı *mystorageaccount*hello içinde *myResourceGroup* kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="9cea9-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="9cea9-156">Merhaba dosya adlı hello kapsayıcıya yerleştirilecek *mycontainer* ve hello yeni dosya adı olacaktır *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="9cea9-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="9cea9-157">Başarılı olursa, benzer toothis benzeyen bir yanıt alın:</span><span class="sxs-lookup"><span data-stu-id="9cea9-157">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="9cea9-158">Bu komut, ağ bağlantısı ve VHD dosyanızı hello boyutuna bağlı olarak biraz zaman alabilir toocomplete</span><span class="sxs-lookup"><span data-stu-id="9cea9-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="9cea9-159">Merhaba Kaydet **hedef URI** yolu toouse toocreate yönetilen bir disk kalacaklarını veya VHD hello kullanarak yeni bir VM karşıya sonraki.</span><span class="sxs-lookup"><span data-stu-id="9cea9-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="9cea9-160">Bir VHD karşıya yükleme için diğer seçenekleri</span><span class="sxs-lookup"><span data-stu-id="9cea9-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="9cea9-161">Bir VHD tooyour depolama hesabını hello aşağıdakilerden birini kullanarak da yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9cea9-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="9cea9-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="9cea9-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="9cea9-163">Azure depolama kopyalama Blob API</span><span class="sxs-lookup"><span data-stu-id="9cea9-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="9cea9-164">Azure Depolama Gezgini karşıya BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="9cea9-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="9cea9-165">Depolama içeri/dışarı aktarma hizmeti REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="9cea9-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="9cea9-166">İçeri/dışarı aktarma hizmeti 7 günden daha uzun süre karşıya tahmini varsa kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9cea9-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="9cea9-167">Kullanabileceğiniz [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) veri boyutu ve aktarım birimi tooestimate başlangıç saati.</span><span class="sxs-lookup"><span data-stu-id="9cea9-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="9cea9-168">İçeri/dışarı aktarma olabilir toocopy tooa standart depolama hesabı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9cea9-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="9cea9-169">AzCopy gibi bir araç kullanarak standart depolama toopremium depolama hesabından toocopy gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cea9-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="9cea9-170">Yönetilen oluşturmak hello görüntüden karşıya VHD</span><span class="sxs-lookup"><span data-stu-id="9cea9-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="9cea9-171">Genelleştirilmiş OS VHD kullanılarak yönetilen bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="9cea9-172">Merhaba değerleri kendi bilgileriyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9cea9-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="9cea9-173">İlk olarak, hello ortak parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9cea9-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="9cea9-174">Genelleştirilmiş OS VHD kullanarak hello görüntüsü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="9cea9-175">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cea9-175">Create a virtual network</span></span>
<span data-ttu-id="9cea9-176">Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cea9-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="9cea9-177">Merhaba alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-177">Create hello subnet.</span></span> <span data-ttu-id="9cea9-178">Bu örnek adlı bir alt ağı oluşturur *mySubnet* hello adres öneki ile *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="9cea9-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="9cea9-179">Merhaba sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-179">Create hello virtual network.</span></span> <span data-ttu-id="9cea9-180">Bu örnek adlı bir sanal ağ oluşturur *myVnet* hello adres öneki ile *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="9cea9-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="9cea9-181">Ortak IP adresi ve ağ arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cea9-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="9cea9-182">ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9cea9-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="9cea9-183">Bir ortak IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-183">Create a public IP address.</span></span> <span data-ttu-id="9cea9-184">Bu örnek adlı ortak IP adresi oluşturur *myPip*.</span><span class="sxs-lookup"><span data-stu-id="9cea9-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="9cea9-185">Merhaba NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="9cea9-185">Create hello NIC.</span></span> <span data-ttu-id="9cea9-186">Bu örnek, adlandırılmış bir NIC oluşturur **myNic**.</span><span class="sxs-lookup"><span data-stu-id="9cea9-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="9cea9-187">Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cea9-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="9cea9-188">toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir ağ güvenlik kuralı (NSG) gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cea9-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="9cea9-189">Bu örnekte adlı bir NSG oluşturulur *myNsg* adlı kuralı içeren *myRdpRule* 3389 numaralı bağlantı noktası RDP trafiğine izin veren.</span><span class="sxs-lookup"><span data-stu-id="9cea9-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="9cea9-190">Nsg'ler hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9cea9-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="9cea9-191">Merhaba sanal ağ için bir değişken oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cea9-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="9cea9-192">Tamamlanan hello sanal ağ için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cea9-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="9cea9-193">Merhaba VM Hello kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="9cea9-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="9cea9-194">Merhaba aşağıdaki cmdlet'i yeni bir kullanıcı adı ve parola toouse hello yerel yönetici hesabı olarak hello VM uzaktan erişmek için gireceğiniz bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="9cea9-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="9cea9-195">Merhaba VM adını ve boyutunu toohello VM yapılandırmasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9cea9-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="9cea9-196">Set hello VM görüntüsü hello için kaynak görüntüsü olarak yeni VM</span><span class="sxs-lookup"><span data-stu-id="9cea9-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="9cea9-197">Yönetilen hello VM görüntüsü Hello Kimliğini kullanarak hello kaynak görüntüsü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="9cea9-198">Merhaba işletim sistemi yapılandırması ayarlayın ve hello NIC ekleyin</span><span class="sxs-lookup"><span data-stu-id="9cea9-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="9cea9-199">Merhaba depolama türü (PremiumLRS veya StandardLRS) ve hello işletim sistemi diski hello boyutunu girin.</span><span class="sxs-lookup"><span data-stu-id="9cea9-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="9cea9-200">Bu örnek hello hesap türü çok ayarlar*PremiumLRS*, disk boyutu çok hello*128 GB* ve disk çok önbelleğe alma*ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="9cea9-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="9cea9-201">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cea9-201">Create hello VM</span></span>

<span data-ttu-id="9cea9-202">Merhaba Yapılandırması'nı kullanarak yeni VM depolanan hello hello oluşturma **$vm** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="9cea9-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="9cea9-203">VM oluşturulduğu bu hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="9cea9-203">Verify that hello VM was created</span></span>
<span data-ttu-id="9cea9-204">Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:</span><span class="sxs-lookup"><span data-stu-id="9cea9-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="9cea9-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9cea9-205">Next steps</span></span>

<span data-ttu-id="9cea9-206">tooyour yeni sanal makine, hello içinde Gözat toohello VM toosign [portal](https://portal.azure.com), tıklatın **Bağlan**ve açık hello Uzak Masaüstü RDP dosyası.</span><span class="sxs-lookup"><span data-stu-id="9cea9-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="9cea9-207">Özgün sanal makine toosign Hello hesabı kimlik bilgilerini tooyour yeni sanal makinede kullanın.</span><span class="sxs-lookup"><span data-stu-id="9cea9-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="9cea9-208">Daha fazla bilgi için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9cea9-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

