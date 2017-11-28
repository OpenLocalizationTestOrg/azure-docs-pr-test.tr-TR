---
title: "hello Azure PowerShell ile özel VM görüntüleri aaaCreate | Microsoft Docs"
description: "Öğretici - hello Azure PowerShell kullanarak özel bir VM görüntüsü oluşturun."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="57e66-103">Özel bir Azure PowerShell kullanarak bir VM görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="57e66-104">Özel resimler gibi Market görüntülerini olsa da, bunları kendiniz oluşturmanız.</span><span class="sxs-lookup"><span data-stu-id="57e66-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="57e66-105">Özel resimler gibi uygulamalar, uygulama yapılandırmaları ve diğer işletim sistemi yapılandırmalarını önceden kullanılan toobootstrap yapılandırmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="57e66-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="57e66-106">Bu öğreticide, kendi özel görüntünüzü bir Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="57e66-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="57e66-107">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="57e66-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57e66-108">Sysprep ve VM'ler generalize</span><span class="sxs-lookup"><span data-stu-id="57e66-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="57e66-109">Özel görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-109">Create a custom image</span></span>
> * <span data-ttu-id="57e66-110">Özel bir görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="57e66-111">Aboneliğinizdeki tüm hello görüntüler liste</span><span class="sxs-lookup"><span data-stu-id="57e66-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="57e66-112">Bir görüntü Sil</span><span class="sxs-lookup"><span data-stu-id="57e66-112">Delete an image</span></span>

<span data-ttu-id="57e66-113">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="57e66-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="57e66-114">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="57e66-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="57e66-115">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="57e66-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="57e66-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="57e66-116">Before you begin</span></span>

<span data-ttu-id="57e66-117">Merhaba adımları tootake mevcut bir VM'yi ve onu yeniden kullanılabilir özel bir görüntü, etkinleştirin toocreate yeni VM örnekleri nasıl kullanabileceğinizi ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="57e66-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="57e66-118">Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="57e66-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="57e66-119">Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57e66-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="57e66-120">Çalışma hello öğretici aracılığıyla değiştirdiğinizde hello kaynak grubu VM adları ve gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="57e66-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="57e66-121">VM hazırlama</span><span class="sxs-lookup"><span data-stu-id="57e66-121">Prepare VM</span></span>

<span data-ttu-id="57e66-122">bir sanal makine görüntüsü toocreate genelleme hello ayırmasını kaldırma ve Azure'da genelleştirilmiş gibi VM hello kaynak işaretleme VM tarafından tooprepare hello VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="57e66-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="57e66-123">Generalize Sysprep kullanarak Windows VM hello</span><span class="sxs-lookup"><span data-stu-id="57e66-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="57e66-124">Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar.</span><span class="sxs-lookup"><span data-stu-id="57e66-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="57e66-125">Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="57e66-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="57e66-126">Toohello sanal makineye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="57e66-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="57e66-127">Merhaba komut istemi penceresi bir yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="57e66-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="57e66-128">Merhaba dizini çok değiştirmek*%windir%\system32\sysprep*ve ardından çalıştırın *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="57e66-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="57e66-129">Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda *girin sistem Out-of-Box deneyimi (OOBE)*ve bu hello emin olun *Generalize* onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="57e66-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="57e66-130">İçinde **kapatma seçenekleri**seçin *kapatma* ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="57e66-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="57e66-131">Sysprep tamamlandığında hello sanal makineyi kapatır.</span><span class="sxs-lookup"><span data-stu-id="57e66-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="57e66-132">**Merhaba VM yeniden başlatma**.</span><span class="sxs-lookup"><span data-stu-id="57e66-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="57e66-133">Deallocate ve hello VM genelleştirilmiş olarak işaretleyin</span><span class="sxs-lookup"><span data-stu-id="57e66-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="57e66-134">görüntüyü toocreate hello VM serbest ve Azure'da genelleştirilmiş olarak işaretlenen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="57e66-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="57e66-135">VM deallocated hello kullanarak [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="57e66-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="57e66-136">Hello sanal makinenin başlangıç durumu çok Ayarla`-Generalized` kullanarak [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="57e66-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="57e66-137">Merhaba görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-137">Create hello image</span></span>

<span data-ttu-id="57e66-138">Merhaba VM görüntüsünü kullanarak oluşturabileceğiniz artık [yeni AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) ve [yeni AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="57e66-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="57e66-139">Merhaba aşağıdaki örnekte oluşturur adlı bir resim *myImage* adlı bir VM'den *myVM*.</span><span class="sxs-lookup"><span data-stu-id="57e66-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="57e66-140">Merhaba sanal makine alın.</span><span class="sxs-lookup"><span data-stu-id="57e66-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="57e66-141">Merhaba görüntü yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="57e66-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="57e66-142">Merhaba görüntü oluşturma.</span><span class="sxs-lookup"><span data-stu-id="57e66-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="57e66-143">Sanal makineleri hello görüntüden oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-143">Create VMs from hello image</span></span>

<span data-ttu-id="57e66-144">Bir görüntü sahip olduğunuza göre bir veya daha fazla yeni VM'ler hello görüntüsünü oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57e66-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="57e66-145">Özel bir görüntüden bir VM oluşturma çok benzer toocreating bir Market görüntüsü kullanarak bir VM'i bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="57e66-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="57e66-146">Market görüntüsünü kullandığınızda, tooinformation hello görüntü, görüntü sağlayıcısı, teklif, SKU ve sürümü hakkında sahip.</span><span class="sxs-lookup"><span data-stu-id="57e66-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="57e66-147">Özel bir görüntü ile tooprovide hello hello özel görüntü kaynak Kimliğini yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="57e66-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="57e66-148">Bir değişken oluşturuyoruz komut dosyası izleyen hello *$image* hello özel görüntü kullanma hakkında bilgi toostore [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) ve ardından kullanırız [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)ve hello kullanarak hello kimliği belirtin *$image* değişken yeni oluşturduğumuz.</span><span class="sxs-lookup"><span data-stu-id="57e66-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="57e66-149">Merhaba betiği oluşturur adlı bir VM'den *myVMfromImage* bizim Özel görüntüden yeni bir kaynak grubu adında *myResourceGroupFromImage* hello içinde *Batı ABD* konumu.</span><span class="sxs-lookup"><span data-stu-id="57e66-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="57e66-150">Görüntü Yönetimi</span><span class="sxs-lookup"><span data-stu-id="57e66-150">Image management</span></span> 

<span data-ttu-id="57e66-151">İşte bazı örnekler ortak yönetim görüntü görevlerinin nasıl ve ne toocomplete bunları PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="57e66-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="57e66-152">Tüm görüntüleri ada göre listeler.</span><span class="sxs-lookup"><span data-stu-id="57e66-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="57e66-153">Görüntüyü silin.</span><span class="sxs-lookup"><span data-stu-id="57e66-153">Delete an image.</span></span> <span data-ttu-id="57e66-154">Bu örnek siler hello adlı görüntü *myOldImage* hello gelen *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="57e66-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="57e66-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57e66-155">Next steps</span></span>

<span data-ttu-id="57e66-156">Bu öğreticide, özel bir VM görüntüsü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="57e66-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="57e66-157">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="57e66-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57e66-158">Sysprep ve VM'ler generalize</span><span class="sxs-lookup"><span data-stu-id="57e66-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="57e66-159">Özel görüntü oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-159">Create a custom image</span></span>
> * <span data-ttu-id="57e66-160">Özel bir görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="57e66-161">Aboneliğinizdeki tüm hello görüntüler liste</span><span class="sxs-lookup"><span data-stu-id="57e66-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="57e66-162">Bir görüntü Sil</span><span class="sxs-lookup"><span data-stu-id="57e66-162">Delete an image</span></span>

<span data-ttu-id="57e66-163">Toohello sonraki öğretici toolearn nasıl yüksek oranda kullanılabilir sanal makineler hakkında ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="57e66-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57e66-164">Yüksek oranda kullanılabilir VM’ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e66-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



