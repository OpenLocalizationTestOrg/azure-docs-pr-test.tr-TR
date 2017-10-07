---
title: "genelleştirilmiş bir Azure VM'de yönetilmeyen görüntüsü aaaCreate | Microsoft Docs"
description: "Genelleştirilmiş bir Windows VM toouse toocreate unmanged görüntüsünü Azure'da VM birden çok kopyasını oluşturun."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="ea87a-103">Nasıl toocreate yönetilmeyen VM görüntü bir Azure sanal makineden</span><span class="sxs-lookup"><span data-stu-id="ea87a-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="ea87a-104">Bu makalede, depolama hesapları kullanmayı ele alır.</span><span class="sxs-lookup"><span data-stu-id="ea87a-104">This article covers using storage accounts.</span></span> <span data-ttu-id="ea87a-105">Bir depolama hesabı yerine yönetilen diskleri ve yönetilen görüntüleri kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ea87a-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="ea87a-106">Daha fazla bilgi için bkz: [genelleştirilmiş VM Azure ile yönetilen bir görüntüsünü yakalama](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ea87a-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="ea87a-107">Bu makale size nasıl gösterir toouse Azure PowerShell toocreate bir depolama hesabı kullanılarak genelleştirilmiş bir Azure VM görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="ea87a-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="ea87a-108">Daha sonra başka bir VM hello görüntü toocreate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea87a-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="ea87a-109">Merhaba görüntü hello işletim sistemi diski ve ekli toohello sanal makine hello veri disklerinin içerir.</span><span class="sxs-lookup"><span data-stu-id="ea87a-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="ea87a-110">Merhaba görüntü hello sanal ağ kaynaklarına içermeyen, yeni VM, oluşturduğunuzda, bu kaynakları tooset gereken şekilde hello.</span><span class="sxs-lookup"><span data-stu-id="ea87a-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ea87a-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ea87a-111">Prerequisites</span></span>
<span data-ttu-id="ea87a-112">Toohave Azure PowerShell sürüm gereksinim 1.0.x ya da daha yeni yüklü.</span><span class="sxs-lookup"><span data-stu-id="ea87a-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="ea87a-113">PowerShell henüz yüklemediyseniz, okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) yükleme adımları için.</span><span class="sxs-lookup"><span data-stu-id="ea87a-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="ea87a-114">Merhaba VM generalize</span><span class="sxs-lookup"><span data-stu-id="ea87a-114">Generalize hello VM</span></span> 
<span data-ttu-id="ea87a-115">Bu bölümde, nasıl gösterilir toogeneralize Windows sanal makinenizi bir resim olarak kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="ea87a-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="ea87a-116">Bir VM genelleme tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar.</span><span class="sxs-lookup"><span data-stu-id="ea87a-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="ea87a-117">Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea87a-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="ea87a-118">Merhaba makine üzerinde çalışan hello sunucu rolleri Sysprep tarafından desteklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ea87a-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="ea87a-119">Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="ea87a-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea87a-120">Merhaba, VHD tooAzure ilk kez yüklüyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce.</span><span class="sxs-lookup"><span data-stu-id="ea87a-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="ea87a-121">Kullanarak bir Linux VM genelleştirmek `sudo waagent -deprovision+user` ve PowerShell toocapture hello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="ea87a-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="ea87a-122">Merhaba CLI toocapture VM kullanma hakkında daha fazla bilgi için bkz: [nasıl toogeneralize ve kullanarak bir Linux sanal makine yakalama Azure CLI hello ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="ea87a-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="ea87a-123">Windows sanal makine içinde toohello imzalayın.</span><span class="sxs-lookup"><span data-stu-id="ea87a-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="ea87a-124">Merhaba komut istemi penceresi bir yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="ea87a-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="ea87a-125">Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="ea87a-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="ea87a-126">Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**ve bu hello emin olun **Generalize** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="ea87a-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="ea87a-127">İçinde **kapatma seçenekleri**seçin **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="ea87a-128">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea87a-128">Click **OK**.</span></span>
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="ea87a-130">Sysprep tamamlandığında hello sanal makineyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="ea87a-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ea87a-131">Karşıya yükleme Bitti'yi hello VHD tooAzure veya VM hello bir görüntü oluşturma olana kadar hello VM yeniden başlatmayın.</span><span class="sxs-lookup"><span data-stu-id="ea87a-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="ea87a-132">Merhaba VM yanlışlıkla yeniden, Sysprep toogeneralize çalışır. yeniden.</span><span class="sxs-lookup"><span data-stu-id="ea87a-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="ea87a-133">TooAzure PowerShell oturumu</span><span class="sxs-lookup"><span data-stu-id="ea87a-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="ea87a-134">Azure PowerShell'i açın ve tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ea87a-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="ea87a-135">Açılır pencere, tooenter Azure hesabı kimlik bilgilerinizi açar.</span><span class="sxs-lookup"><span data-stu-id="ea87a-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="ea87a-136">Merhaba abonelik kimlikleri kullanılabilir aboneliklerinizi alın.</span><span class="sxs-lookup"><span data-stu-id="ea87a-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="ea87a-137">Merhaba doğru aboneliğin Hello abonelik kimliğini kullanarak ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ea87a-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="ea87a-138">Merhaba VM serbest bırakma ve hello durumu toogeneralized ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ea87a-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="ea87a-139">Merhaba VM kaynakları serbest bırakma.</span><span class="sxs-lookup"><span data-stu-id="ea87a-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="ea87a-140">Merhaba *durum* hello Azure VM hello için portal değişiklikleri **durduruldu** çok**durduruldu (serbest bırakıldı)**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="ea87a-141">Hello sanal makinenin başlangıç durumu çok Ayarla**Genelleştirmiş**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="ea87a-142">Merhaba VM Hello durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ea87a-142">Check hello status of hello VM.</span></span> <span data-ttu-id="ea87a-143">Merhaba **OSState ve genelleştirilmiş** hello VM hello olmalıdır için bölüm **DisplayStatus** çok ayarlamak**VM genelleştirilmiş**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="ea87a-144">Merhaba görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea87a-144">Create hello image</span></span>

<span data-ttu-id="ea87a-145">Bir yönetilmeyen sanal makine görüntüsü bu komutu kullanarak hello hedef depolama kapsayıcıda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea87a-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="ea87a-146">Merhaba görüntüsü hello aynı oluşturulur özgün sanal makine hello gibi depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="ea87a-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="ea87a-147">Merhaba `-Path` parametresi hello kaynak VM tooyour yerel bilgisayar için hello JSON şablonunun bir kopyasını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ea87a-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="ea87a-148">Merhaba `-DestinationContainerName` parametredir görüntülerinizi toohold istediğiniz hello kapsayıcısının hello adı.</span><span class="sxs-lookup"><span data-stu-id="ea87a-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="ea87a-149">Merhaba kapsayıcı yoksa, sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ea87a-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="ea87a-150">Görüntünüzün hello URL hello JSON dosyasını şablondan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea87a-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="ea87a-151">Toohello Git **kaynakları** > **storageProfile** > **osDisk** > **görüntü**  >  **URI** hello tam yol için bir bölüm görüntünüzün.</span><span class="sxs-lookup"><span data-stu-id="ea87a-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="ea87a-152">Merhaba görüntünün Hello URL'si arar gibi: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="ea87a-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="ea87a-153">Merhaba URI hello portalında da doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea87a-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="ea87a-154">Merhaba görüntüdür adlı kopyalanan tooa kapsayıcı **sistem** depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="ea87a-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="ea87a-155">Merhaba görüntüsünden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea87a-155">Create a VM from hello image</span></span>

<span data-ttu-id="ea87a-156">Artık hello yönetilmeyen görüntüsünden bir veya daha fazla sanal makine oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea87a-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="ea87a-157">Merhaba hello VHD URI'si ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ea87a-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="ea87a-158">Merhaba URI hello VHD toouse hello biçiminde olan: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="ea87a-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="ea87a-159">Bu örnekte adlı VHD hello **myVHD** hello depolama hesabında **mystorageaccount** hello kapsayıcısında **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="ea87a-160">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea87a-160">Create a virtual network</span></span>
<span data-ttu-id="ea87a-161">Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea87a-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="ea87a-162">Merhaba alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea87a-162">Create hello subnet.</span></span> <span data-ttu-id="ea87a-163">Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur **mySubnet** hello kaynak grubunda **myResourceGroup** hello adres öneki ile **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="ea87a-164">Merhaba sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea87a-164">Create hello virtual network.</span></span> <span data-ttu-id="ea87a-165">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur **myVnet** hello içinde **Batı ABD** hello adres öneki konumla **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="ea87a-166">Ortak IP adresi ve ağ arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea87a-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="ea87a-167">ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="ea87a-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="ea87a-168">Bir ortak IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea87a-168">Create a public IP address.</span></span> <span data-ttu-id="ea87a-169">Bu örnek adlı ortak IP adresi oluşturur **myPip**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="ea87a-170">Merhaba NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="ea87a-170">Create hello NIC.</span></span> <span data-ttu-id="ea87a-171">Bu örnek, adlandırılmış bir NIC oluşturur **myNic**.</span><span class="sxs-lookup"><span data-stu-id="ea87a-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="ea87a-172">Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea87a-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="ea87a-173">toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir güvenlik kuralı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea87a-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="ea87a-174">Bu örnekte adlı bir NSG oluşturulur **myNsg** adlı kuralı içeren **myRdpRule** 3389 numaralı bağlantı noktası RDP trafiğine izin veren.</span><span class="sxs-lookup"><span data-stu-id="ea87a-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="ea87a-175">Nsg'ler hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea87a-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="ea87a-176">Merhaba sanal ağ için bir değişken oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea87a-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="ea87a-177">Tamamlanan hello sanal ağ için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea87a-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="ea87a-178">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea87a-178">Create hello VM</span></span>
<span data-ttu-id="ea87a-179">Merhaba aşağıdaki PowerShell hello sanal makine yapılandırmaları tamamlandıktan ve yönetilmeyen görüntü hello kaynak olarak hello yeni yükleme için kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea87a-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

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

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="ea87a-180">VM oluşturulduğu bu hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ea87a-180">Verify that hello VM was created</span></span>
<span data-ttu-id="ea87a-181">Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:</span><span class="sxs-lookup"><span data-stu-id="ea87a-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="ea87a-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea87a-182">Next steps</span></span>
<span data-ttu-id="ea87a-183">Yeni sanal makinenizi Azure PowerShell ile toomanage bkz [Azure Resource Manager ve PowerShell kullanarak sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea87a-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


