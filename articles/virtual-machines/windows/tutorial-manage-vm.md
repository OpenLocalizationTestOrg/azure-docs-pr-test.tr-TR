---
title: "aaaCreate ve Windows sanal makineleri yönetme hello Azure PowerShell Modülü | Microsoft Docs"
description: "Öğretici - oluşturma ve yönetme Windows VM ile birlikte hello Azure PowerShell Modülü"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="e91db-103">Oluşturma ve yönetme Windows VM'ler ile Azure PowerShell modülü hello</span><span class="sxs-lookup"><span data-stu-id="e91db-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="e91db-104">Azure sanal makineler tam olarak yapılandırılabilir ve esnek bir bilgi işlem ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e91db-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="e91db-105">Bu öğretici, bir VM boyutu seçerek, bir VM görüntüsü seçme ve bir VM dağıtma gibi temel Azure sanal makine dağıtım öğeleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="e91db-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="e91db-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e91db-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e91db-107">Oluştur ve tooa VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="e91db-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="e91db-108">Seçin ve VM görüntüleri kullanmak</span><span class="sxs-lookup"><span data-stu-id="e91db-108">Select and use VM images</span></span>
> * <span data-ttu-id="e91db-109">Görüntüleme ve belirli VM boyutları kullanma</span><span class="sxs-lookup"><span data-stu-id="e91db-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="e91db-110">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="e91db-110">Resize a VM</span></span>
> * <span data-ttu-id="e91db-111">Görüntüleyin ve VM durumunu anlamak</span><span class="sxs-lookup"><span data-stu-id="e91db-111">View and understand VM state</span></span>

<span data-ttu-id="e91db-112">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="e91db-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e91db-113">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="e91db-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="e91db-114">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e91db-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="e91db-115">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e91db-115">Create resource group</span></span>

<span data-ttu-id="e91db-116">Bir kaynak grubu ile Merhaba oluşturmak [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) komutu.</span><span class="sxs-lookup"><span data-stu-id="e91db-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="e91db-117">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="e91db-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="e91db-118">Bir kaynak grubu bir sanal makine önce oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e91db-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="e91db-119">Bu örnekte, bir kaynak grubu adında *myResourceGroupVM* hello oluşturulan *EastUS* bölge.</span><span class="sxs-lookup"><span data-stu-id="e91db-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="e91db-120">Merhaba kaynak grubu oluştururken veya değiştirirken Bu öğretici görülebilir bir VM belirtilir.</span><span class="sxs-lookup"><span data-stu-id="e91db-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="e91db-121">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e91db-121">Create virtual machine</span></span>

<span data-ttu-id="e91db-122">Bir sanal makineye bağlı tooa sanal ağ olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e91db-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="e91db-123">Bir ağ arabirimi kartı bir ortak IP adresi kullanarak hello sanal makine ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="e91db-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="e91db-124">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="e91db-124">Create virtual network</span></span>

<span data-ttu-id="e91db-125">Bir alt ağ ile oluşturma [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="e91db-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="e91db-126">Bir sanal ağ ile oluşturma [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="e91db-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="e91db-127">Ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="e91db-127">Create public IP address</span></span>

<span data-ttu-id="e91db-128">Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="e91db-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="e91db-129">Ağ arabirimi kartı oluşturun</span><span class="sxs-lookup"><span data-stu-id="e91db-129">Create network interface card</span></span>

<span data-ttu-id="e91db-130">Bir ağ arabirimi kartı ile oluşturma [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="e91db-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="e91db-131">Ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="e91db-131">Create network security group</span></span>

<span data-ttu-id="e91db-132">Bir Azure [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) (NSG) bir veya daha çok sanal makineler için gelen ve giden trafik denetler.</span><span class="sxs-lookup"><span data-stu-id="e91db-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="e91db-133">Ağ güvenlik grubu kurallarının izin verin veya belirli bir bağlantı noktası veya bağlantı noktası aralığı ağ trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="e91db-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="e91db-134">Önceden tanımlanmış bir kaynakta kaynaklanan trafiğin yalnızca bir sanal makineyle iletişim kurabilmesi için bu kurallar kaynak adres öneki de içerir.</span><span class="sxs-lookup"><span data-stu-id="e91db-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="e91db-135">yüklemekte olduğunuz tooaccess hello IIS Web sunucusu, gelen bir NSG kuralı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e91db-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="e91db-136">toocreate gelen bir NSG kuralı kullanmak [Ekle AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="e91db-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="e91db-137">Merhaba aşağıdaki örnek adlı bir NSG kuralı oluşturur *myNSGRule* bağlantı noktası açar *3389* hello sanal makine için:</span><span class="sxs-lookup"><span data-stu-id="e91db-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="e91db-138">NSG Hello kullanarak oluşturduğunuz *myNSGRule* ile [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="e91db-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="e91db-139">Merhaba NSG toohello alt ağ ile Merhaba sanal ağındaki Ekle [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="e91db-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="e91db-140">Güncelleştirme hello sanal ağ ile [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="e91db-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="e91db-141">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="e91db-141">Create virtual machine</span></span>

<span data-ttu-id="e91db-142">Bir sanal makine oluştururken, işletim sistemi görüntüsü, disk boyutlandırma ve yönetici kimlik bilgileri gibi birkaç seçenek bulunur.</span><span class="sxs-lookup"><span data-stu-id="e91db-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="e91db-143">Bu örnekte, bir sanal makine adı ile oluşturulan *myVM* çalışan hello en son sürümünü Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="e91db-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="e91db-144">Merhaba kullanıcı adı ve parola ile Merhaba sanal makinede hello yönetici hesabı için gerekli ayarlama [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="e91db-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="e91db-145">Merhaba sanal makine için ilk yapılandırma Hello oluşturmak [yeni AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="e91db-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="e91db-146">Merhaba işletim sistemi bilgileri toohello sanal makine yapılandırmasıyla eklemek [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="e91db-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="e91db-147">Hello görüntü bilgileri toohello sanal makine yapılandırmasıyla eklemek [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="e91db-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="e91db-148">Merhaba işletim sistemi disk ayarları toohello sanal makine yapılandırmasıyla eklemek [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="e91db-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="e91db-149">Toohello sanal makine yapılandırmasıyla daha önce oluşturduğunuz Ekle hello ağ arabirim kartı [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="e91db-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="e91db-150">Merhaba sanal makineyle oluşturmak [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e91db-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="e91db-151">TooVM Bağlan</span><span class="sxs-lookup"><span data-stu-id="e91db-151">Connect tooVM</span></span>

<span data-ttu-id="e91db-152">Merhaba dağıtım tamamlandıktan sonra bir Uzak Masaüstü Bağlantısı ile Merhaba sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e91db-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="e91db-153">Aşağıdaki komutları tooreturn hello genel IP adresi hello sanal makinenin hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e91db-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="e91db-154">Tarayıcı tootest web bağlantınızı bir sonraki adımda ile tooit bağlanabilmesi için bu IP adresini not alın.</span><span class="sxs-lookup"><span data-stu-id="e91db-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="e91db-155">Kullanım hello aşağıdaki hello sanal makineyle Uzak Masaüstü oturumu toocreate komutu.</span><span class="sxs-lookup"><span data-stu-id="e91db-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="e91db-156">Başlangıç IP adresi ile hello yerine *Publicıpaddress* sanal makinenizin.</span><span class="sxs-lookup"><span data-stu-id="e91db-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="e91db-157">İstendiğinde, hello sanal makine oluşturulurken kullanılan hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="e91db-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="e91db-158">VM görüntüleri anlama</span><span class="sxs-lookup"><span data-stu-id="e91db-158">Understand VM images</span></span>

<span data-ttu-id="e91db-159">Hello Azure Market kullanılan toocreate yeni bir sanal makine olabilecek çok sayıda sanal makine görüntülerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e91db-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="e91db-160">Merhaba önceki adımlarda, bir sanal makine hello Windows Server 2016-Datacenter görüntüsü kullanılarak oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e91db-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="e91db-161">Bu adımda, ayrıca yeni VM'ler için temel olarak kullanabilirsiniz diğer Windows görüntüleri için kullanılan toosearch hello Market hello PowerShell modülüdür.</span><span class="sxs-lookup"><span data-stu-id="e91db-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="e91db-162">Bu işlem hello yayımcı, teklif ve hello görüntü adı (Sku) bulma oluşur.</span><span class="sxs-lookup"><span data-stu-id="e91db-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="e91db-163">Kullanım hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) komutu tooreturn görüntü yayımcıların listesini.</span><span class="sxs-lookup"><span data-stu-id="e91db-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="e91db-164">Kullanım hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn görüntü teklifleri listesi.</span><span class="sxs-lookup"><span data-stu-id="e91db-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="e91db-165">Bu komutla, liste hello belirtilen yayımcı üzerinde filtrelenmiş hello döndürdü.</span><span class="sxs-lookup"><span data-stu-id="e91db-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="e91db-166">Merhaba [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) komutu ardından filtre uygulayarak hello yayımcı ve teklif adı tooreturn üzerinde resim adları listesi.</span><span class="sxs-lookup"><span data-stu-id="e91db-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="e91db-167">Bu bilgiler kullanılan toodeploy belirli bir görüntü ile VM olabilir.</span><span class="sxs-lookup"><span data-stu-id="e91db-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="e91db-168">Bu örnek hello görüntü adı hello VM nesnesinde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e91db-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="e91db-169">Tam dağıtım adımları için bu öğreticideki toohello önceki örneklerde bakın.</span><span class="sxs-lookup"><span data-stu-id="e91db-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="e91db-170">VM boyutları anlama</span><span class="sxs-lookup"><span data-stu-id="e91db-170">Understand VM sizes</span></span>

<span data-ttu-id="e91db-171">Bir sanal makine boyutu, kullanılabilir toohello sanal makine yapılan işlem kaynaklarını CPU, GPU ve bellek gibi hello miktarını belirler.</span><span class="sxs-lookup"><span data-stu-id="e91db-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="e91db-172">Sanal makineler hello beklediğiniz için iş yükü boyutu ile uygun oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e91db-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="e91db-173">İş yükü artarsa, var olan bir sanal makine yeniden boyutlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e91db-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="e91db-174">VM boyutları</span><span class="sxs-lookup"><span data-stu-id="e91db-174">VM Sizes</span></span>

<span data-ttu-id="e91db-175">Aşağıdaki tablonun hello boyutları kullanım örneklerine kategorilere ayırır.</span><span class="sxs-lookup"><span data-stu-id="e91db-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="e91db-176">Tür</span><span class="sxs-lookup"><span data-stu-id="e91db-176">Type</span></span>                     | <span data-ttu-id="e91db-177">Boyutlar</span><span class="sxs-lookup"><span data-stu-id="e91db-177">Sizes</span></span>           |    <span data-ttu-id="e91db-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e91db-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e91db-179">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="e91db-179">General purpose</span></span>         |<span data-ttu-id="e91db-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="e91db-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="e91db-181">Dengeli CPU bellekten.</span><span class="sxs-lookup"><span data-stu-id="e91db-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="e91db-182">Geliştirme için ideal / test ve küçük toomedium uygulamaları ve verileri çözümler.</span><span class="sxs-lookup"><span data-stu-id="e91db-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="e91db-183">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="e91db-183">Compute optimized</span></span>      | <span data-ttu-id="e91db-184">FS, F</span><span class="sxs-lookup"><span data-stu-id="e91db-184">Fs, F</span></span>             | <span data-ttu-id="e91db-185">Yüksek CPU bellekten.</span><span class="sxs-lookup"><span data-stu-id="e91db-185">High CPU-to-memory.</span></span> <span data-ttu-id="e91db-186">Orta düzey trafik uygulamalar, ağ uygulamaları ve toplu işlemler için iyidir.</span><span class="sxs-lookup"><span data-stu-id="e91db-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="e91db-187">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="e91db-187">Memory optimized</span></span>       | <span data-ttu-id="e91db-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="e91db-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="e91db-189">Yüksek bellek için-çekirdek.</span><span class="sxs-lookup"><span data-stu-id="e91db-189">High memory-to-core.</span></span> <span data-ttu-id="e91db-190">İlişkisel veritabanları, Orta toolarge önbellekleri ve bellek içi analizi için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="e91db-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="e91db-191">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="e91db-191">Storage optimized</span></span>       | <span data-ttu-id="e91db-192">Ls</span><span class="sxs-lookup"><span data-stu-id="e91db-192">Ls</span></span>                | <span data-ttu-id="e91db-193">Yüksek disk aktarım hızı ve GÇ.</span><span class="sxs-lookup"><span data-stu-id="e91db-193">High disk throughput and IO.</span></span> <span data-ttu-id="e91db-194">Büyük Veri, SQL ve NoSQL veritabanları için ideal.</span><span class="sxs-lookup"><span data-stu-id="e91db-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="e91db-195">GPU</span><span class="sxs-lookup"><span data-stu-id="e91db-195">GPU</span></span>           | <span data-ttu-id="e91db-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="e91db-196">NV, NC</span></span>            | <span data-ttu-id="e91db-197">Yoğun Grafik işleme ve video düzenleme için hedeflenen özel VM'ler.</span><span class="sxs-lookup"><span data-stu-id="e91db-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="e91db-198">Yüksek performans</span><span class="sxs-lookup"><span data-stu-id="e91db-198">High performance</span></span> | <span data-ttu-id="e91db-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="e91db-199">H, A8-11</span></span>          | <span data-ttu-id="e91db-200">Bizim en güçlü CPU VM'ler isteğe bağlı yüksek verimlilik ağ arabirimlerine (RDMA) sahip.</span><span class="sxs-lookup"><span data-stu-id="e91db-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="e91db-201">Kullanılabilir VM boyutları Bul</span><span class="sxs-lookup"><span data-stu-id="e91db-201">Find available VM sizes</span></span>

<span data-ttu-id="e91db-202">toosee VM listesi boyutları kullanılabilen belirli bir bölgede, hello kullan [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) komutu.</span><span class="sxs-lookup"><span data-stu-id="e91db-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="e91db-203">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="e91db-203">Resize a VM</span></span>

<span data-ttu-id="e91db-204">Bir VM dağıtıldıktan sonra onu yeniden boyutlandırılan tooincrease olması veya kaynak ayırma azaltın.</span><span class="sxs-lookup"><span data-stu-id="e91db-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="e91db-205">Merhaba istenen boyuta hello geçerli VM kümede kullanılabilir durumdaysa bir VM'yi yeniden boyutlandırılırken önce denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e91db-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="e91db-206">Merhaba [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) komut boyutlarının listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e91db-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="e91db-207">Merhaba boyutu kullanılabilir isterseniz, hello işlemi sırasında yeniden başlatılıncaya kadar ancak hello VM bir gücü açma durumundan yeniden boyutlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e91db-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="e91db-208">Merhaba istenen boyut hello geçerli kümede hello VM hello yeniden boyutlandırma önce işlemi serbest toobe oluşabilir gereksinimlerini değildir.</span><span class="sxs-lookup"><span data-stu-id="e91db-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="e91db-209">, Hello VM geri açık olduğundan, hello geçici diskteki tüm verilerin kaldırılır ve hello genel IP adresi statik bir IP adresi kullanılmadığı sürece değiştirdiğinizde unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e91db-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="e91db-210">VM güç durumları</span><span class="sxs-lookup"><span data-stu-id="e91db-210">VM power states</span></span>

<span data-ttu-id="e91db-211">Bir Azure VM birçok güç durumlarını birine sahip.</span><span class="sxs-lookup"><span data-stu-id="e91db-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="e91db-212">Bu durum hello hiper yönetici hello açısından hello VM hello geçerli durumunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e91db-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="e91db-213">Güç durumları</span><span class="sxs-lookup"><span data-stu-id="e91db-213">Power states</span></span>

| <span data-ttu-id="e91db-214">Güç durumu</span><span class="sxs-lookup"><span data-stu-id="e91db-214">Power State</span></span> | <span data-ttu-id="e91db-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e91db-215">Description</span></span>
|----|----|
| <span data-ttu-id="e91db-216">Başlangıç</span><span class="sxs-lookup"><span data-stu-id="e91db-216">Starting</span></span> | <span data-ttu-id="e91db-217">Merhaba sanal makinenin başlatıldığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e91db-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="e91db-218">Çalışıyor</span><span class="sxs-lookup"><span data-stu-id="e91db-218">Running</span></span> | <span data-ttu-id="e91db-219">Merhaba sanal makinenin çalışmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e91db-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="e91db-220">Durduruluyor</span><span class="sxs-lookup"><span data-stu-id="e91db-220">Stopping</span></span> | <span data-ttu-id="e91db-221">Bu hello sanal makinenin durdurulması gösterir.</span><span class="sxs-lookup"><span data-stu-id="e91db-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="e91db-222">Durduruldu</span><span class="sxs-lookup"><span data-stu-id="e91db-222">Stopped</span></span> | <span data-ttu-id="e91db-223">Bu hello sanal makine durdurulduğunda gösterir.</span><span class="sxs-lookup"><span data-stu-id="e91db-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="e91db-224">Sanal makineleri hello durdurulmuş durumda hala bilgi işlem ücretleri olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e91db-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="e91db-225">Ayırmayı kaldırma</span><span class="sxs-lookup"><span data-stu-id="e91db-225">Deallocating</span></span> | <span data-ttu-id="e91db-226">Merhaba sanal makinenin serbest gösterir.</span><span class="sxs-lookup"><span data-stu-id="e91db-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="e91db-227">Serbest bırakıldı</span><span class="sxs-lookup"><span data-stu-id="e91db-227">Deallocated</span></span> | <span data-ttu-id="e91db-228">Merhaba sanal makinenin hello hiper yönetici hello denetim düzlemi hala kullanılabilir ancak tamamen kaldırılması gösterir.</span><span class="sxs-lookup"><span data-stu-id="e91db-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="e91db-229">Merhaba Deallocated durumu içindeki sanal makineler bilgi işlem ücretleri değil.</span><span class="sxs-lookup"><span data-stu-id="e91db-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="e91db-230">Merhaba güç hello sanal makinenin durumunu bilinmediğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e91db-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="e91db-231">Güç durumu Bul</span><span class="sxs-lookup"><span data-stu-id="e91db-231">Find power state</span></span>

<span data-ttu-id="e91db-232">belirli bir VM, kullanım hello tooretrieve hello durumu [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) komutu.</span><span class="sxs-lookup"><span data-stu-id="e91db-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="e91db-233">Emin toospecify bir sanal makine ve kaynak grubu için geçerli bir ad olabilir.</span><span class="sxs-lookup"><span data-stu-id="e91db-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="e91db-234">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="e91db-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="e91db-235">Yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="e91db-235">Management tasks</span></span>

<span data-ttu-id="e91db-236">Bir sanal makine Hello yaşam döngüsü sırasında başlatma, durdurma veya bir sanal makine silme gibi yönetim görevleri toorun isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e91db-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="e91db-237">Ayrıca, toocreate, komut dosyaları tooautomate yineleyen veya karmaşık görevleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e91db-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="e91db-238">Azure PowerShell kullanarak, birçok ortak yönetim görevlerinin hello komut satırından veya komut dosyalarında çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e91db-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="e91db-239">Sanal makineyi durdurma</span><span class="sxs-lookup"><span data-stu-id="e91db-239">Stop virtual machine</span></span>

<span data-ttu-id="e91db-240">Durdurun ve bir sanal makineyle ayırması [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="e91db-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="e91db-241">Sağlanan durumdaki tookeep hello sanal makine istiyorsanız hello - StayProvisioned parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e91db-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="e91db-242">Sanal makineyi Başlat</span><span class="sxs-lookup"><span data-stu-id="e91db-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="e91db-243">Kaynak grubunu silme</span><span class="sxs-lookup"><span data-stu-id="e91db-243">Delete resource group</span></span>

<span data-ttu-id="e91db-244">Bir kaynak grubunu silme içinde içerdiği tüm kaynaklar da siler.</span><span class="sxs-lookup"><span data-stu-id="e91db-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="e91db-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e91db-245">Next steps</span></span>

<span data-ttu-id="e91db-246">Bu öğreticide, temel VM oluşturmayı ve yönetmeyi nasıl gibi hakkında öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="e91db-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e91db-247">Oluştur ve tooa VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="e91db-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="e91db-248">Seçin ve VM görüntüleri kullanmak</span><span class="sxs-lookup"><span data-stu-id="e91db-248">Select and use VM images</span></span>
> * <span data-ttu-id="e91db-249">Görüntüleme ve belirli VM boyutları kullanma</span><span class="sxs-lookup"><span data-stu-id="e91db-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="e91db-250">VM’yi yeniden boyutlandırma</span><span class="sxs-lookup"><span data-stu-id="e91db-250">Resize a VM</span></span>
> * <span data-ttu-id="e91db-251">Görüntüleyin ve VM durumunu anlamak</span><span class="sxs-lookup"><span data-stu-id="e91db-251">View and understand VM state</span></span>

<span data-ttu-id="e91db-252">Toohello sonraki öğretici toolearn VM disklerle ilgili ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="e91db-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="e91db-253">Oluşturma ve yönetme VM diskleri</span><span class="sxs-lookup"><span data-stu-id="e91db-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
