---
title: "aaaUpload generalize VHD toocreate Azure birden çok VM | Microsoft Docs"
description: "Bir genelleştirilmiş VHD tooan Azure depolama hesabı toocreate hello Resource Manager dağıtım modeli içeren bir Windows VM toouse karşıya yükleyin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="0274b-103">Genelleştirilmiş bir VHD tooAzure toocreate yeni bir VM karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="0274b-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="0274b-104">Bu konu, bir genelleştirilmiş yönetilmeyen disk tooa depolama hesabı karşıya yükleme ve karşıya hello diski kullanarak yeni bir VM oluşturma kapsar.</span><span class="sxs-lookup"><span data-stu-id="0274b-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="0274b-105">Genelleştirilmiş bir VHD görüntüsü tüm kişisel hesap bilgilerinizi Sysprep kullanılarak kaldırılıncaya oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="0274b-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="0274b-106">Toocreate özel bir VHD depolama hesabındaki bir VM'den istiyorsanız, bkz: [özelleştirilmiş bir VHD'den bir VM oluşturma](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="0274b-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="0274b-107">Depolama hesaplarını kullanarak bu konu şunları içerir, ancak bunun yerine müşteriler toousing yönetilen diskleri taşırken öneririz.</span><span class="sxs-lookup"><span data-stu-id="0274b-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="0274b-108">Yönetilen disklerde nasıl tooprepare, karşıya yükleme ve kullanarak yeni bir VM oluşturmak eksiksiz bir kılavuz için bkz: [oluşturma yönetilen diskleri kullanılarak genelleştirilmiş bir VHD karşıya tooAzure yeni VM'den](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="0274b-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="0274b-109">Merhaba VM hazırlama</span><span class="sxs-lookup"><span data-stu-id="0274b-109">Prepare hello VM</span></span>

<span data-ttu-id="0274b-110">Genelleştirilmiş bir VHD tüm kişisel hesap bilgilerinizi Sysprep kullanılarak kaldırılıncaya oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="0274b-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="0274b-111">Toouse hello VHD görüntüsü toocreate olarak amaçlıyorsanız, yeni VM'lerin, aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="0274b-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="0274b-112">[Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="0274b-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="0274b-113">Sysprep kullanarak Hello sanal makine generalize</span><span class="sxs-lookup"><span data-stu-id="0274b-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="0274b-114">Sysprep kullanarak bir Windows sanal makine generalize</span><span class="sxs-lookup"><span data-stu-id="0274b-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="0274b-115">Bu bölümde, nasıl gösterilir toogeneralize Windows sanal makinenizi bir resim olarak kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="0274b-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="0274b-116">Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar.</span><span class="sxs-lookup"><span data-stu-id="0274b-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="0274b-117">Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="0274b-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="0274b-118">Merhaba makine üzerinde çalışan hello sunucu rolleri Sysprep tarafından desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0274b-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="0274b-119">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="0274b-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0274b-120">Sysprep, VHD tooAzure hello için karşıya yüklemeden önce ilk kez çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce.</span><span class="sxs-lookup"><span data-stu-id="0274b-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="0274b-121">Windows sanal makine içinde toohello imzalayın.</span><span class="sxs-lookup"><span data-stu-id="0274b-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="0274b-122">Merhaba komut istemi penceresi bir yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="0274b-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="0274b-123">Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="0274b-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="0274b-124">Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**ve bu hello emin olun **Generalize** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="0274b-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="0274b-125">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="0274b-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="0274b-126">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0274b-126">Click **OK**.</span></span>
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="0274b-128">Sysprep tamamlandığında hello sanal makineyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="0274b-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0274b-129">Karşıya yükleme Bitti'yi hello VHD tooAzure veya VM hello bir görüntü oluşturma olana kadar hello VM yeniden başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="0274b-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="0274b-130">Merhaba VM yanlışlıkla yeniden, Sysprep toogeneralize çalışır. yeniden.</span><span class="sxs-lookup"><span data-stu-id="0274b-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="0274b-131">Merhaba VHD karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="0274b-131">Upload hello VHD</span></span>

<span data-ttu-id="0274b-132">Merhaba VHD tooan Azure depolama hesabı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0274b-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="0274b-133">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="0274b-133">Log in tooAzure</span></span>
<span data-ttu-id="0274b-134">PowerShell sürüm 1.4 zaten yoksa veya üstü yüklü okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0274b-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="0274b-135">Azure PowerShell'i açın ve tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0274b-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="0274b-136">Açılır pencere, tooenter Azure hesabı kimlik bilgilerinizi açar.</span><span class="sxs-lookup"><span data-stu-id="0274b-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="0274b-137">Merhaba abonelik kimlikleri kullanılabilir aboneliklerinizi alın.</span><span class="sxs-lookup"><span data-stu-id="0274b-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="0274b-138">Merhaba doğru aboneliğin Hello abonelik kimliğini kullanarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0274b-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="0274b-139">Değiştir `<subscriptionID>` hello hello Kimliğine sahip abonelik düzeltin.</span><span class="sxs-lookup"><span data-stu-id="0274b-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="0274b-140">Merhaba depolama hesabı edinin</span><span class="sxs-lookup"><span data-stu-id="0274b-140">Get hello storage account</span></span>
<span data-ttu-id="0274b-141">Azure toostore karşıya hello VM görüntüsündeki bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="0274b-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="0274b-142">Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0274b-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="0274b-143">tooshow hello kullanılabilir depolama hesaplarını yazın:</span><span class="sxs-lookup"><span data-stu-id="0274b-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="0274b-144">Mevcut bir depolama hesabını toouse istiyorsanız, toohello devam [karşıya yükleme hello VM görüntüsü](#upload-the-vm-vhd-to-your-storage-account) bölümü.</span><span class="sxs-lookup"><span data-stu-id="0274b-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="0274b-145">Bir depolama hesabı toocreate gerekiyorsa, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="0274b-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="0274b-146">Merhaba hello depolama hesabı nerede oluşturulacağını hello kaynak grubunun adını gerekir.</span><span class="sxs-lookup"><span data-stu-id="0274b-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="0274b-147">toofind, aboneliğinizdeki türü tüm hello kaynak gruplarını çıkışı:</span><span class="sxs-lookup"><span data-stu-id="0274b-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="0274b-148">bir kaynak grubu adında toocreate **myResourceGroup** hello içinde **Batı ABD** bölge, türü:</span><span class="sxs-lookup"><span data-stu-id="0274b-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="0274b-149">Adlı depolama hesabı oluşturma **mystorageaccount** hello kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="0274b-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="0274b-150">Başlangıç hello karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="0274b-150">Start hello upload</span></span> 

<span data-ttu-id="0274b-151">Kullanım hello [Ekle AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) depolama hesabınızdaki cmdlet tooupload hello görüntü tooa kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="0274b-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="0274b-152">Karşıya dosya hello Bu örnek **myVHD.vhd** gelen `"C:\Users\Public\Documents\Virtual hard disks\"` adlı tooa depolama hesabı **mystorageaccount** hello içinde **myResourceGroup** kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="0274b-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="0274b-153">Merhaba dosya adlı hello kapsayıcıya yerleştirilecek **mycontainer** ve hello yeni dosya adı olacaktır **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="0274b-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="0274b-154">Başarılı olursa, benzer toothis benzeyen bir yanıt alın:</span><span class="sxs-lookup"><span data-stu-id="0274b-154">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="0274b-155">Bu komut, ağ bağlantısı ve VHD dosyanızı hello boyutuna bağlı olarak biraz zaman alabilir toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0274b-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="0274b-156">Yeni bir VM oluşturun</span><span class="sxs-lookup"><span data-stu-id="0274b-156">Create a new VM</span></span> 

<span data-ttu-id="0274b-157">VHD toocreate yeni bir VM kullanım hello karşıya artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0274b-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="0274b-158">Merhaba hello VHD URI'si ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0274b-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="0274b-159">Merhaba URI hello VHD toouse hello biçiminde olan: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="0274b-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="0274b-160">Bu örnekte adlı VHD hello **myVHD** hello depolama hesabında **mystorageaccount** hello kapsayıcısında **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="0274b-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="0274b-161">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="0274b-161">Create a virtual network</span></span>
<span data-ttu-id="0274b-162">Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0274b-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="0274b-163">Merhaba alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0274b-163">Create hello subnet.</span></span> <span data-ttu-id="0274b-164">Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur **mySubnet** hello kaynak grubunda **myResourceGroup** hello adres öneki ile **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="0274b-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="0274b-165">Merhaba sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0274b-165">Create hello virtual network.</span></span> <span data-ttu-id="0274b-166">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur **myVnet** hello içinde **Batı ABD** hello adres öneki konumla **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="0274b-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="0274b-167">Ortak IP adresi ve ağ arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0274b-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="0274b-168">ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="0274b-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="0274b-169">Bir ortak IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0274b-169">Create a public IP address.</span></span> <span data-ttu-id="0274b-170">Bu örnek adlı ortak IP adresi oluşturur **myPip**.</span><span class="sxs-lookup"><span data-stu-id="0274b-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="0274b-171">Merhaba NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="0274b-171">Create hello NIC.</span></span> <span data-ttu-id="0274b-172">Bu örnek, adlandırılmış bir NIC oluşturur **myNic**.</span><span class="sxs-lookup"><span data-stu-id="0274b-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="0274b-173">Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0274b-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="0274b-174">toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir güvenlik kuralı gerekir.</span><span class="sxs-lookup"><span data-stu-id="0274b-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="0274b-175">Bu örnekte adlı bir NSG oluşturulur **myNsg** adlı kuralı içeren **myRdpRule** 3389 numaralı bağlantı noktası RDP trafiğine izin veren.</span><span class="sxs-lookup"><span data-stu-id="0274b-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="0274b-176">Nsg'ler hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0274b-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="0274b-177">Merhaba sanal ağ için bir değişken oluşturma</span><span class="sxs-lookup"><span data-stu-id="0274b-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="0274b-178">Tamamlanan hello sanal ağ için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0274b-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="0274b-179">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0274b-179">Create hello VM</span></span>
<span data-ttu-id="0274b-180">Merhaba aşağıdaki PowerShell betiğini nasıl hello yeni yükleme için hello kaynak olarak VM görüntüsü tooset hello sanal makine yapılandırmaları ve kullanım hello karşıya gösterir.</span><span class="sxs-lookup"><span data-stu-id="0274b-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="0274b-181">VM oluşturulduğu bu hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="0274b-181">Verify that hello VM was created</span></span>
<span data-ttu-id="0274b-182">Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:</span><span class="sxs-lookup"><span data-stu-id="0274b-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="0274b-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0274b-183">Next steps</span></span>
<span data-ttu-id="0274b-184">Yeni sanal makinenizi Azure PowerShell ile toomanage bkz [Azure Resource Manager ve PowerShell kullanarak sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0274b-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


