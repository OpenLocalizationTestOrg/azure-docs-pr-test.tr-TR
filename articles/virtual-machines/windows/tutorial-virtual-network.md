---
title: "Azure sanal ağlar ve Windows sanal makineleri | Microsoft Docs"
description: "Öğretici - Azure sanal ağlar ve Azure PowerShell ile Windows sanal makineleri yönetme"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="2ee34-103">Azure sanal ağlar ve Azure PowerShell ile Windows sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="2ee34-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="2ee34-104">Azure sanal makineler, iç ve dış ağ iletişimi için Azure ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ee34-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="2ee34-105">Bu öğreticide, bir sanal ağda birden çok sanal makine (VM) oluşturabilir ve bunları arasında ağ bağlantısı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ee34-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="2ee34-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2ee34-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2ee34-107">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee34-107">Create a virtual network</span></span>
> * <span data-ttu-id="2ee34-108">Sanal ağ alt ağları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee34-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="2ee34-109">Ağ güvenlik gruplarıyla ağ trafiğini denetleme</span><span class="sxs-lookup"><span data-stu-id="2ee34-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="2ee34-110">Eylem trafik kurallarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="2ee34-110">View traffic rules in action</span></span>

<span data-ttu-id="2ee34-111">Bu öğretici, Azure PowerShell modülü 3.6 veya sonraki bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2ee34-112">Sürümü bulmak için ` Get-Module -ListAvailable AzureRM` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2ee34-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="2ee34-113">Yükseltme gerekiyorsa, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2ee34-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="2ee34-114">VNet oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee34-114">Create VNet</span></span>

<span data-ttu-id="2ee34-115">Bir VNet kendi ağ bulutta gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="2ee34-116">Bir VNet Azure bulutunun aboneliğinize adanmış mantıksal bir yalıtım ' dir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="2ee34-117">Bir sanal ağ içinde alt ağlar, bu alt ağlar ve bağlantıları VM'ler alt ağlara bağlantısı kurallarını bulun.</span><span class="sxs-lookup"><span data-stu-id="2ee34-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="2ee34-118">Diğer Azure kaynaklarına oluşturabilmeniz için önce bir kaynak grubu ile oluşturmanıza gerek [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="2ee34-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="2ee34-119">Aşağıdaki örnek, bir kaynak grubu oluşturur *myRGNetwork* içinde *EastUS* konumu:</span><span class="sxs-lookup"><span data-stu-id="2ee34-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="2ee34-120">Bir alt ağ alt bir vnet'in kaynaktır ve adres alanları IP adresi öneklerini kullanarak bir CIDR bloğu içinde kesimleri yardımcı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2ee34-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="2ee34-121">NIC alt ağlara eklendi ve çeşitli iş yükleri için bağlantı sağlama VM'ler bağlı.</span><span class="sxs-lookup"><span data-stu-id="2ee34-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="2ee34-122">Bir alt ağ ile oluşturma [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="2ee34-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="2ee34-123">Adlı VNET oluşturma *myVNet* kullanarak *myFrontendSubnet* ile [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="2ee34-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="2ee34-124">Ön uç VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee34-124">Create front-end VM</span></span>

<span data-ttu-id="2ee34-125">Bir VM sanal ağ içinde iletişim kurmak bir sanal ağ arabirimi (NIC) gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="2ee34-126">*MyFrontendVM* internet'ten erişilir, böylece bir ortak IP adresini de gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="2ee34-127">Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="2ee34-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="2ee34-128">Bir NIC ile oluşturma [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="2ee34-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="2ee34-129">Kullanıcı adı ayarlayabilir ve parola için yönetici hesabı ile VM üzerinde [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="2ee34-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="2ee34-130">VM'lerin oluşturma [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig), [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [ekleme AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), ve [AzureRmVM yeni](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2ee34-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="2ee34-131">Web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="2ee34-131">Install web server</span></span>

<span data-ttu-id="2ee34-132">IIS yükleyebilirsiniz *myFrontendVM* Uzak Masaüstü oturumu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2ee34-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="2ee34-133">Genel IP adresi erişmek için VM'nin edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="2ee34-134">Genel IP adresi elde edebilirsiniz *myFrontendVM* ile [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="2ee34-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="2ee34-135">Aşağıdaki örnek IP adresi alacağı *myPublicIPAddress* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="2ee34-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="2ee34-136">Sonraki adımlarda kullanabilmesi için bu IP adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="2ee34-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="2ee34-137">İle Uzak Masaüstü oturumu oluşturmak için aşağıdaki komutu kullanın *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="2ee34-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="2ee34-138">Değiştir  *<publicIPAddress>*  daha önce kaydettiğiniz adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="2ee34-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="2ee34-139">İstendiğinde VM oluşturduğunuz sırada kullanılan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="2ee34-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="2ee34-140">Oturum olduğunuza *myFrontendVM*, IIS yüklemek ve web trafiğine izin vermek yerel güvenlik duvarı kuralı etkinleştirmek için tek satırlık bir PowerShell kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ee34-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="2ee34-141">Bir PowerShell istemi açın ve şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2ee34-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="2ee34-142">Kullanım [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) IIS Web sunucusu yükler özel betik uzantısı çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="2ee34-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="2ee34-143">Şimdi IIS sitesi görmek için VM göz atmak için genel IP adresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ee34-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![Varsayılan IIS sitesi](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="2ee34-145">İç trafiği yönetmek</span><span class="sxs-lookup"><span data-stu-id="2ee34-145">Manage internal traffic</span></span>

<span data-ttu-id="2ee34-146">Bir ağ güvenlik grubu (NSG) izin veren veya reddeden bir sanal ağa bağlı kaynaklar için ağ trafiği güvenlik kurallarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="2ee34-147">Nsg'ler alt ağları veya VM'ler için bağlı tekil NIC'lerle ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="2ee34-148">Açma veya kapatma Vm'lere erişim bağlantı noktaları üzerinden yapılır NSG kurallarını kullanma.</span><span class="sxs-lookup"><span data-stu-id="2ee34-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="2ee34-149">Oluşturduğunuzda *myFrontendVM*, gelen bağlantı noktası 3389 RDP bağlantı için otomatik olarak açılmışsa.</span><span class="sxs-lookup"><span data-stu-id="2ee34-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="2ee34-150">İç iletişim VM'lerin bir NSG kullanarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="2ee34-151">Bu bölümde, ağdaki ek bir alt ağ oluşturun ve bir NSG bir bağlantıdan izin verecek şekilde atamak öğrenin *myFrontendVM* için *myBackendVM* 1433 numaralı bağlantı noktasında.</span><span class="sxs-lookup"><span data-stu-id="2ee34-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="2ee34-152">Alt ağ VM oluşturulduktan sonra atanır.</span><span class="sxs-lookup"><span data-stu-id="2ee34-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="2ee34-153">İç trafiği sınırlayabilirsiniz *myBackendVM* yalnızca gelen *myFrontendVM* arka uç alt ağı için bir NSG oluşturarak.</span><span class="sxs-lookup"><span data-stu-id="2ee34-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="2ee34-154">Aşağıdaki örnek, adlandırılmış bir NSG kuralı oluşturur *myBackendNSGRule* ile [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="2ee34-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="2ee34-155">Adlı ağ güvenlik grubu Ekle *myBackendNSG* ile [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="2ee34-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="2ee34-156">Arka uç alt ağ Ekle</span><span class="sxs-lookup"><span data-stu-id="2ee34-156">Add back-end subnet</span></span>

<span data-ttu-id="2ee34-157">Ekle *myBackEndSubnet* için *myVNet* ile [Ekle AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="2ee34-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="2ee34-158">Arka uç VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee34-158">Create back-end VM</span></span>

<span data-ttu-id="2ee34-159">Arka uç VM oluşturmak için en kolay yolu, bir SQL Server görüntüsü kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="2ee34-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="2ee34-160">Bu öğretici yalnızca VM veritabanı sunucusuyla oluşturur, ancak veritabanı erişme hakkında bilgi sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="2ee34-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="2ee34-161">Oluşturma *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="2ee34-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="2ee34-162">Kullanıcı adı ve parola Get-Credential ile VM üzerinde yönetici hesabı için gerekli ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2ee34-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="2ee34-163">Oluşturma *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="2ee34-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="2ee34-164">Kullanılan görüntü SQL Server'ın yüklü, ancak bu öğreticide kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="2ee34-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="2ee34-165">Web trafiğini işlemek için bir VM ve veritabanı yönetimi işlemek için bir VM nasıl yapılandırabileceğiniz göstermek için dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="2ee34-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ee34-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ee34-166">Next steps</span></span>

<span data-ttu-id="2ee34-167">Bu öğreticide oluşturduğunuz ve Azure ağları sanal makinelerle ilgili olarak güvenli.</span><span class="sxs-lookup"><span data-stu-id="2ee34-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2ee34-168">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee34-168">Create a virtual network</span></span>
> * <span data-ttu-id="2ee34-169">Sanal ağ alt ağları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ee34-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="2ee34-170">Ağ güvenlik gruplarıyla ağ trafiğini denetleme</span><span class="sxs-lookup"><span data-stu-id="2ee34-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="2ee34-171">Eylem trafik kurallarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="2ee34-171">View traffic rules in action</span></span>

<span data-ttu-id="2ee34-172">Azure Yedekleme'yi kullanarak sanal makinelerde güvenli hale getirme verileri izleme hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="2ee34-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="2ee34-173">.</span><span class="sxs-lookup"><span data-stu-id="2ee34-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2ee34-174">Azure'da Windows sanal makineleri yedekleyin</span><span class="sxs-lookup"><span data-stu-id="2ee34-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
