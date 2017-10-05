---
title: "Yönetilen bir Azure VM genelleştirilmiş şirket içi VHD'den oluştur | Microsoft Docs"
description: "Genelleştirilmiş bir VHD Azure'a yükleyin ve yeni VM'ler, Resource Manager dağıtım modelinde oluşturmak için kullanın."
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
ms.openlocfilehash: d802ba16ecb4e32e2adb7be3a8e99c72a1625841
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-to-create-new-vms-in-azure"></a><span data-ttu-id="c0ef9-103">Genelleştirilmiş bir VHD yüklemek ve yeni sanal makineleri oluşturmak için kullanın</span><span class="sxs-lookup"><span data-stu-id="c0ef9-103">Upload a generalized VHD and use it to create new VMs in Azure</span></span>

<span data-ttu-id="c0ef9-104">Bu konuda, bir VHD genelleştirilmiş bir VM'nin Azure'a yükleyin, VHD'den görüntü oluştur ve bu görüntüden yeni bir VM oluşturmak için PowerShell kullanılarak üzerinden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-104">This topic walks you through using PowerShell to upload a VHD of a generalized VM to Azure, create an image from the VHD and create a new VM from that image.</span></span> <span data-ttu-id="c0ef9-105">Bir şirket içi sanallaştırma aracı ya da başka bir bulut dışa aktarılan bir VHD'yi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="c0ef9-106">Kullanarak [yönetilen diskleri](managed-disks-overview.md) yeni VM VM yönetimini basitleştirir ve VM bir kullanılabilirlik kümesine yerleştirildiğinde daha iyi kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-106">Using [Managed Disks](managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> 

<span data-ttu-id="c0ef9-107">Bir örnek komut dosyası kullanmak istiyorsanız, bkz: [örnek bir VHD Azure'a yükleyin ve yeni bir VM oluşturmak için komut dosyası](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="c0ef9-107">If you want to use a sample script, see [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c0ef9-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="c0ef9-108">Before you begin</span></span>

- <span data-ttu-id="c0ef9-109">Herhangi bir VHD'yi Azure'a karşıya yüklemeden önce uygulamanız gereken [Windows VHD veya VHDX Azure'a karşıya yüklemek için hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c0ef9-109">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="c0ef9-110">Gözden geçirme [Plan yönetilen disklerin geçiş için](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) geçişinizi başlatmadan önce [yönetilen diskleri](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0ef9-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="c0ef9-111">AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="c0ef9-112">Yüklemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-112">Run the following command to install it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="c0ef9-113">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0ef9-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="c0ef9-114">Sysprep kullanarak Windows VM generalize</span><span class="sxs-lookup"><span data-stu-id="c0ef9-114">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="c0ef9-115">Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılacak makine hazırlar.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-115">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="c0ef9-116">Sysprep hakkında daha fazla ayrıntı için bkz: [kullanım Sysprep nasıl: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0ef9-116">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="c0ef9-117">Makinede çalışan sunucu rollerini Sysprep tarafından desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-117">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="c0ef9-118">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="c0ef9-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0ef9-119">Sysprep, VHD Azure'a ilk kez karşıya yüklemeden önce çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-119">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="c0ef9-120">Windows sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-120">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="c0ef9-121">Bir yönetici olarak komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-121">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="c0ef9-122">Dizinine değiştirin **%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-122">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="c0ef9-123">İçinde **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**, emin olun **Generalize** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-123">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="c0ef9-124">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="c0ef9-125">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-125">Click **OK**.</span></span>
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="c0ef9-127">Sysprep tamamlandığında, sanal makineyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-127">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="c0ef9-128">VM yeniden başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-128">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="c0ef9-129">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="c0ef9-129">Log in to Azure</span></span>
<span data-ttu-id="c0ef9-130">PowerShell sürüm 1.4 zaten yoksa veya üstü yüklü okuma [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0ef9-130">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="c0ef9-131">Azure PowerShell'i açın ve Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-131">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="c0ef9-132">Azure hesabı kimlik bilgilerinizi girmeniz için bir açılır pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-132">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="c0ef9-133">Abonelik kimlikleri kullanılabilir aboneliklerinizi alın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-133">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="c0ef9-134">Abonelik kimliğini kullanarak doğru aboneliğin ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c0ef9-134">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="c0ef9-135">Değiştir  *<subscriptionID>*  doğru abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-135">Replace *<subscriptionID>* with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="c0ef9-136">Depolama hesabı edinin</span><span class="sxs-lookup"><span data-stu-id="c0ef9-136">Get the storage account</span></span>
<span data-ttu-id="c0ef9-137">Karşıya yüklenen VM görüntüsü depolamak için Azure depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-137">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="c0ef9-138">Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="c0ef9-139">VHD için bir VM yönetilen bir disk oluşturmak için kullanıyorsanız, depolama hesabı konumu aynı olmalıdır nerede oluşturmakta VM konumu.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-139">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="c0ef9-140">Kullanılabilir depolama hesaplarını görüntülemek için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-140">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="c0ef9-141">Varolan bir depolama hesabı kullanmak istiyorsanız, devam [VM görüntüsü karşıya](#upload-the-vm-vhd-to-your-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-141">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="c0ef9-142">Bir depolama hesabı oluşturmanız gerekiyorsa, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-142">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="c0ef9-143">Depolama hesabı nerede oluşturulacağını kaynak grubunun adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-143">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="c0ef9-144">Aboneliğinizde olan tüm kaynak grupları bulmak için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-144">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="c0ef9-145">Adlı bir kaynak grubu oluşturmak için **myResourceGroup** içinde **Doğu ABD** bölge, türü:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-145">To create a resource group named **myResourceGroup** in the **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="c0ef9-146">Adlı depolama hesabı oluşturma **mystorageaccount** kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-146">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="c0ef9-147">-SkuName için geçerli değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="c0ef9-148">**Standard_LRS** -yerel olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="c0ef9-149">**Standard_ZRS** -bölge olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="c0ef9-150">**Standard_GRS** -coğrafi olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="c0ef9-151">**Standard_RAGRS** -coğrafi olarak yedekli depolamaya okuma erişimi.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="c0ef9-152">**Premium_LRS** -Premium yerel olarak yedekli depolama.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="c0ef9-153">Depolama hesabınız VHD karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="c0ef9-153">Upload the VHD to your storage account</span></span>

<span data-ttu-id="c0ef9-154">Kullanım [Ekle AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) depolama hesabınızdaki bir kapsayıcıya VHD yüklemek için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-154">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="c0ef9-155">Bu örnek dosya karşıya yükleme *myVHD.vhd* gelen *"C:\Users\Public\Documents\Virtual sabit diskleri\"*  bir depolama hesabına adlı *mystorageaccount* içinde *myResourceGroup* kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-155">This example uploads the file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="c0ef9-156">Dosya adında kapsayıcısının içine yerleştirilecek *mycontainer* ve yeni dosya adı *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-156">The file will be placed into the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="c0ef9-157">Başarılı olursa, şuna benzer bir yanıt alın:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-157">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="c0ef9-158">Ağ bağlantısı ve VHD dosyasının boyutuna bağlı olarak, bu komutun tamamlanması biraz zaman alabilir</span><span class="sxs-lookup"><span data-stu-id="c0ef9-158">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="c0ef9-159">Kaydet **hedef URI** yönetilen bir disk veya karşıya yüklenen VHD kullanarak yeni bir VM oluşturmak için kullanacaksanız daha sonra kullanmak üzere yolu.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-159">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="c0ef9-160">Bir VHD karşıya yükleme için diğer seçenekleri</span><span class="sxs-lookup"><span data-stu-id="c0ef9-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="c0ef9-161">Bir VHD depolama hesabınıza aşağıdakilerden birini kullanarak da yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-161">You can also upload a VHD to your storage account using one of the following:</span></span>

- [<span data-ttu-id="c0ef9-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="c0ef9-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="c0ef9-163">Azure depolama kopyalama Blob API</span><span class="sxs-lookup"><span data-stu-id="c0ef9-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="c0ef9-164">Azure Depolama Gezgini karşıya BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="c0ef9-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="c0ef9-165">Depolama içeri/dışarı aktarma hizmeti REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="c0ef9-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="c0ef9-166">İçeri/dışarı aktarma hizmeti 7 günden daha uzun süre karşıya tahmini varsa kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="c0ef9-167">Kullanabileceğiniz [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) veri boyutu ve aktarım birimi saati tahmin etmek için.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 
    <span data-ttu-id="c0ef9-168">İçeri/dışarı aktarma, bir standart depolama hesabına kopyalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-168">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="c0ef9-169">Premium depolama hesabı AzCopy gibi bir araç kullanarak standart depolama biriminden kopyalamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-169">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="c0ef9-170">Karşıya yüklenen VHD'den yönetilen bir görüntü oluştur</span><span class="sxs-lookup"><span data-stu-id="c0ef9-170">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="c0ef9-171">Genelleştirilmiş OS VHD kullanılarak yönetilen bir görüntü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="c0ef9-172">Değerleri kendi bilgileriyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-172">Replace the values with your own information.</span></span>


1.  <span data-ttu-id="c0ef9-173">İlk olarak, ortak parametreleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-173">First, set the common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="c0ef9-174">Genelleştirilmiş OS VHD kullanarak görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="c0ef9-175">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0ef9-175">Create a virtual network</span></span>
<span data-ttu-id="c0ef9-176">VNet ve alt ağı oluşturmak [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0ef9-176">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="c0ef9-177">Alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-177">Create the subnet.</span></span> <span data-ttu-id="c0ef9-178">Bu örnek adlı bir alt ağı oluşturur *mySubnet* adres öneki ile *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-178">This example creates a subnet named *mySubnet* with the address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="c0ef9-179">Sanal ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-179">Create the virtual network.</span></span> <span data-ttu-id="c0ef9-180">Bu örnek adlı bir sanal ağ oluşturur *myVnet* adres öneki ile *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-180">This example creates a virtual network named *myVnet* with the address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="c0ef9-181">Ortak IP adresi ve ağ arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0ef9-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="c0ef9-182">Sanal makinenin sanal ağda iletişimini etkinleştirmeniz için, [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-182">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="c0ef9-183">Bir ortak IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-183">Create a public IP address.</span></span> <span data-ttu-id="c0ef9-184">Bu örnek adlı ortak IP adresi oluşturur *myPip*.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="c0ef9-185">NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="c0ef9-185">Create the NIC.</span></span> <span data-ttu-id="c0ef9-186">Bu örnek, adlandırılmış bir NIC oluşturur **myNic**.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="c0ef9-187">Ağ güvenlik grubu ve bir RDP kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0ef9-187">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="c0ef9-188">RDP kullanarak VM'nizi oturum açmak bağlantı noktası 3389 üzerinde RDP erişimine izin veren bir ağ güvenlik kuralı (NSG) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-188">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="c0ef9-189">Bu örnekte adlı bir NSG oluşturulur *myNsg* adlı kuralı içeren *myRdpRule* 3389 numaralı bağlantı noktası RDP trafiğine izin veren.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="c0ef9-190">Nsg'ler hakkında daha fazla bilgi için bkz: [PowerShell kullanarak Azure'da bir VM için bağlantı noktaları açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0ef9-190">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="c0ef9-191">Sanal ağ için bir değişken oluşturun</span><span class="sxs-lookup"><span data-stu-id="c0ef9-191">Create a variable for the virtual network</span></span>

<span data-ttu-id="c0ef9-192">Tamamlanan sanal ağ için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-192">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="c0ef9-193">VM için kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="c0ef9-193">Get the credentials for the VM</span></span>

<span data-ttu-id="c0ef9-194">Aşağıdaki cmdlet'i yeni bir kullanıcı adı ve parola VM uzaktan erişmek için yerel yönetici hesabı olarak kullanılacak gireceğiniz bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-194">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-the-vm-name-and-size-to-the-vm-configuration"></a><span data-ttu-id="c0ef9-195">Sanal makine adını ve boyutunu VM yapılandırmasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-195">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="c0ef9-196">VM görüntüsü yeni VM için kaynak görüntü olarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c0ef9-196">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="c0ef9-197">Yönetilen VM görüntüsü Kimliğini kullanarak kaynak görüntüsü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-197">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="c0ef9-198">İşletim sistemi yapılandırması ayarlayın ve NIC ekleyin</span><span class="sxs-lookup"><span data-stu-id="c0ef9-198">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="c0ef9-199">Depolama türü (PremiumLRS veya StandardLRS) ve işletim sistemi disk boyutu girin.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-199">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="c0ef9-200">Bu örnekte hesap türünü ayarlar *PremiumLRS*, disk boyutu *128 GB* ve disk önbelleğe alma *ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-200">This example sets the account type to *PremiumLRS*, the disk size to *128 GB* and disk caching to *ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="c0ef9-201">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0ef9-201">Create the VM</span></span>

<span data-ttu-id="c0ef9-202">İçinde depolanan yapılandırmayı kullanarak yeni VM oluşturma **$vm** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-202">Create the new VM using the configuration stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="c0ef9-203">VM oluşturulduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c0ef9-203">Verify that the VM was created</span></span>
<span data-ttu-id="c0ef9-204">Tamamlandığında, yeni oluşturulan VM görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya aşağıdaki PowerShell komutlarını kullanarak:</span><span class="sxs-lookup"><span data-stu-id="c0ef9-204">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="c0ef9-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0ef9-205">Next steps</span></span>

<span data-ttu-id="c0ef9-206">Yeni sanal makinede oturum açmak için Gözat VM [portal](https://portal.azure.com), tıklatın **Bağlan**ve Uzak Masaüstü RDP dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-206">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="c0ef9-207">Yeni sanal makinede oturum açmak için özgün sanal makine hesabı kimlik bilgilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c0ef9-207">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="c0ef9-208">Daha fazla bilgi için bkz: [bağlanmayı ve Windows çalıştıran Azure sanal makinesi için oturum](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0ef9-208">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

