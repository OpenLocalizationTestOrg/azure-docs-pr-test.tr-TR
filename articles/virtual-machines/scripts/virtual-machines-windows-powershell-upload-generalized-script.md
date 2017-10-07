---
title: "genelleştirilmiş bir VHD tooAzure PowerShell komut dosyası örneği aaaUpload | Microsoft Docs"
description: "PowerShell komut dosyası tooupload genelleştirilmiş bir VHD tooAzure örnek ve hello resource manager dağıtım modeli ve yönetilen diskleri kullanarak yeni bir VM oluşturun."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="e1f63-103">Örnek bir VHD tooAzure tooupload komut dosyasını hazırlamak ve yeni bir VM oluşturun</span><span class="sxs-lookup"><span data-stu-id="e1f63-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="e1f63-104">Bu komut dosyasını bir yerel .vhd dosyası genelleştirilmiş bir sanal makineden alır ve tooAzure yükler, yönetilen Disk görüntüsü oluşturur ve hello toocreate yeni bir VM kullanır.</span><span class="sxs-lookup"><span data-stu-id="e1f63-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e1f63-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e1f63-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="e1f63-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="e1f63-106">Clean up deployment</span></span> 

<span data-ttu-id="e1f63-107">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="e1f63-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e1f63-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e1f63-108">Script explanation</span></span>

<span data-ttu-id="e1f63-109">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="e1f63-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="e1f63-110">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="e1f63-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e1f63-111">Komut</span><span class="sxs-lookup"><span data-stu-id="e1f63-111">Command</span></span>                                                                                                             | <span data-ttu-id="e1f63-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="e1f63-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="e1f63-113">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e1f63-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="e1f63-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="e1f63-115">Yeni-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="e1f63-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="e1f63-116">Bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="e1f63-117">Ekleme AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="e1f63-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="e1f63-118">Bir sanal sabit diskten bir şirket içi sanal makine tooa blob Azure bulut depolama hesabında karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="e1f63-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="e1f63-119">AzureRmImageConfig yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="e1f63-120">Yapılandırılabilir Resim nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="e1f63-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="e1f63-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="e1f63-122">Merhaba işletim sistemi görüntüsü nesne üzerinde disk özelliklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e1f63-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="e1f63-123">AzureRmImage yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="e1f63-124">Yeni bir görüntü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="e1f63-125">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e1f63-126">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-126">Creates a subnet configuration.</span></span> <span data-ttu-id="e1f63-127">Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1f63-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="e1f63-128">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e1f63-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="e1f63-129">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="e1f63-130">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="e1f63-131">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="e1f63-132">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="e1f63-133">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="e1f63-134">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="e1f63-135">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="e1f63-136">Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="e1f63-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="e1f63-137">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="e1f63-138">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="e1f63-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e1f63-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="e1f63-140">Bir sanal ağ, bir kaynak grubunda alır.</span><span class="sxs-lookup"><span data-stu-id="e1f63-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="e1f63-141">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="e1f63-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="e1f63-142">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e1f63-142">Creates a VM configuration.</span></span> <span data-ttu-id="e1f63-143">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="e1f63-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e1f63-144">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e1f63-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e1f63-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="e1f63-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="e1f63-146">Bir sanal makine için bir görüntü belirtir.</span><span class="sxs-lookup"><span data-stu-id="e1f63-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="e1f63-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="e1f63-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="e1f63-148">Merhaba işletim sistemi, bir sanal makineye disk özelliklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e1f63-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="e1f63-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="e1f63-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="e1f63-150">Merhaba işletim sistemi, bir sanal makineye disk özelliklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e1f63-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="e1f63-151">Ekleme AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e1f63-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="e1f63-152">Bir ağ arabirimi tooa sanal makineye ekler.</span><span class="sxs-lookup"><span data-stu-id="e1f63-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="e1f63-153">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e1f63-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="e1f63-154">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e1f63-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="e1f63-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e1f63-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="e1f63-156">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e1f63-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="e1f63-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1f63-157">Next steps</span></span>

<span data-ttu-id="e1f63-158">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e1f63-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e1f63-159">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e1f63-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
