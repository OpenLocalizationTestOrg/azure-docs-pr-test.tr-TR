---
title: "aaaAzure Windows sanal makineler ve sanal ağları | Microsoft Docs"
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="2015f-103">Azure sanal ağlar ve Azure PowerShell ile Windows sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="2015f-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="2015f-104">Azure sanal makineler, iç ve dış ağ iletişimi için Azure ağ kullanın.</span><span class="sxs-lookup"><span data-stu-id="2015f-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="2015f-105">Bu öğreticide, bir sanal ağda birden çok sanal makine (VM) oluşturabilir ve bunları arasında ağ bağlantısı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2015f-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="2015f-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2015f-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2015f-107">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2015f-107">Create a virtual network</span></span>
> * <span data-ttu-id="2015f-108">Sanal ağ alt ağları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2015f-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="2015f-109">Ağ güvenlik gruplarıyla ağ trafiğini denetleme</span><span class="sxs-lookup"><span data-stu-id="2015f-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="2015f-110">Eylem trafik kurallarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="2015f-110">View traffic rules in action</span></span>

<span data-ttu-id="2015f-111">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="2015f-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2015f-112">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="2015f-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="2015f-113">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2015f-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="2015f-114">VNet oluşturma</span><span class="sxs-lookup"><span data-stu-id="2015f-114">Create VNet</span></span>

<span data-ttu-id="2015f-115">Bir VNet kendi ağ hello bulutta gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="2015f-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="2015f-116">Bir VNet hello ayrılmış Azure bulut tooyour abonelik mantıksal yalıtımının ' dir.</span><span class="sxs-lookup"><span data-stu-id="2015f-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="2015f-117">Bir sanal ağ içinde alt ağlar, bağlantı toothose alt ağları ve hello VM'ler toohello alt bağlantılarından kurallarını bulun.</span><span class="sxs-lookup"><span data-stu-id="2015f-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="2015f-118">Diğer Azure kaynaklarına oluşturabilmeniz için önce bir kaynak grubu ile toocreate gerekir [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="2015f-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="2015f-119">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myRGNetwork* hello içinde *EastUS* konumu:</span><span class="sxs-lookup"><span data-stu-id="2015f-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="2015f-120">Bir alt ağ alt bir vnet'in kaynaktır ve adres alanları IP adresi öneklerini kullanarak bir CIDR bloğu içinde kesimleri yardımcı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2015f-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="2015f-121">NIC toosubnets ve çeşitli iş yükleri için bağlantı sağlama bağlı tooVMs eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2015f-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="2015f-122">Bir alt ağ ile oluşturma [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="2015f-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="2015f-123">Adlı VNET oluşturma *myVNet* kullanarak *myFrontendSubnet* ile [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="2015f-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="2015f-124">Ön uç VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2015f-124">Create front-end VM</span></span>

<span data-ttu-id="2015f-125">Bir sanal ağda VM toocommunicate için bir sanal ağ arabirimi (NIC) gerekir.</span><span class="sxs-lookup"><span data-stu-id="2015f-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="2015f-126">Merhaba *myFrontendVM* hello erişilen Internet nedenle da genel bir IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2015f-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="2015f-127">Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="2015f-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="2015f-128">Bir NIC ile oluşturma [AzureRmNetworkInterface yeni](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="2015f-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="2015f-129">Merhaba kullanıcı adı ve parola hello VM hello yönetici hesabı için gerekli olan [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="2015f-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="2015f-130">Merhaba VM'ler ile oluşturmak [yeni AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Ekleme AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), ve [AzureRmVM yeni](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2015f-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="2015f-131">Web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="2015f-131">Install web server</span></span>

<span data-ttu-id="2015f-132">IIS yükleyebilirsiniz *myFrontendVM* Uzak Masaüstü oturumu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2015f-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="2015f-133">Merhaba VM tooaccess tooget hello genel IP adresi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="2015f-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="2015f-134">Merhaba genel IP adresi elde edebilirsiniz *myFrontendVM* ile [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="2015f-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="2015f-135">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIPAddress* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="2015f-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="2015f-136">Sonraki adımlarda kullanabilmesi için bu IP adresini not edin.</span><span class="sxs-lookup"><span data-stu-id="2015f-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="2015f-137">Kullanım hello aşağıdaki komut ile Uzak Masaüstü oturumu toocreate *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="2015f-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="2015f-138">Değiştir  *<publicIPAddress>*  daha önce kaydettiğiniz hello adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="2015f-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="2015f-139">İstendiğinde, hello VM oluştururken kullanılan hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="2015f-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="2015f-140">Çok günlüğe olduğunuza*myFrontendVM*, tek satırlık bir PowerShell tooinstall IIS kullanın ve hello yerel güvenlik duvarı kuralı tooallow web trafiği etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2015f-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="2015f-141">PowerShell komut istemini açın ve hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2015f-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="2015f-142">Kullanım [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) hello IIS Web sunucusu yükler toorun hello özel betik uzantısı:</span><span class="sxs-lookup"><span data-stu-id="2015f-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="2015f-143">Artık hello ortak IP adresi toobrowse toohello VM toosee hello IIS sitesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2015f-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Varsayılan IIS sitesi](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="2015f-145">İç trafiği yönetmek</span><span class="sxs-lookup"><span data-stu-id="2015f-145">Manage internal traffic</span></span>

<span data-ttu-id="2015f-146">Bir ağ güvenlik grubu (NSG) izin veren veya reddeden ağ trafiğine bağlı tooresources tooa VNet güvenlik kurallarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="2015f-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="2015f-147">Nsg'ler ilişkili toosubnets olabilir veya tek tek NIC tooVMs bağlı.</span><span class="sxs-lookup"><span data-stu-id="2015f-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="2015f-148">Açma veya kapatma erişim tooVMs bağlantı noktaları üzerinden yapılır NSG kurallarını kullanma.</span><span class="sxs-lookup"><span data-stu-id="2015f-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="2015f-149">Oluşturduğunuzda *myFrontendVM*, gelen bağlantı noktası 3389 RDP bağlantı için otomatik olarak açılmışsa.</span><span class="sxs-lookup"><span data-stu-id="2015f-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="2015f-150">İç iletişim VM'lerin bir NSG kullanarak yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2015f-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="2015f-151">Bu bölümde, bilgi nasıl toocreate hello ek bir alt ağ ve bir NSG tooit tooallow bir bağlantıdan atayın *myFrontendVM* çok*myBackendVM* 1433 numaralı bağlantı noktasında.</span><span class="sxs-lookup"><span data-stu-id="2015f-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="2015f-152">Merhaba alt toohello VM oluşturulduktan sonra atanır.</span><span class="sxs-lookup"><span data-stu-id="2015f-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="2015f-153">Çok iç trafiğini sınırlandırmak*myBackendVM* yalnızca gelen *myFrontendVM* hello arka uç alt ağı için bir NSG oluşturarak.</span><span class="sxs-lookup"><span data-stu-id="2015f-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="2015f-154">Merhaba aşağıdaki örnek adlı bir NSG kuralı oluşturur *myBackendNSGRule* ile [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="2015f-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="2015f-155">Adlı ağ güvenlik grubu Ekle *myBackendNSG* ile [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="2015f-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="2015f-156">Arka uç alt ağ Ekle</span><span class="sxs-lookup"><span data-stu-id="2015f-156">Add back-end subnet</span></span>

<span data-ttu-id="2015f-157">Ekle *myBackEndSubnet* çok*myVNet* ile [Ekle AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="2015f-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="2015f-158">Arka uç VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2015f-158">Create back-end VM</span></span>

<span data-ttu-id="2015f-159">bir SQL Server görüntüsü kullanarak arka uç VM Hello en kolay yolu toocreate hello var.</span><span class="sxs-lookup"><span data-stu-id="2015f-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="2015f-160">Bu öğretici yalnızca hello VM hello veritabanı sunucusuyla oluşturur, ancak hello veritabanına erişme hakkında bilgi sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="2015f-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="2015f-161">Oluşturma *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="2015f-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="2015f-162">Merhaba kullanıcı adı ve parola hello VM Get-Credential ile Merhaba yönetici hesabı için gerekli ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="2015f-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="2015f-163">Oluşturma *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="2015f-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="2015f-164">kullanılan hello görüntü SQL Server'ın yüklü, ancak bu öğreticide kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="2015f-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="2015f-165">Dahil edilen tooshow olduğu, nasıl bir VM toohandle web trafiği ve toohandle veritabanı yönetimi VM yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2015f-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2015f-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2015f-166">Next steps</span></span>

<span data-ttu-id="2015f-167">Bu öğreticide oluşturduğunuz ve Azure ağları ilgili toovirtual makineler olarak güvenli.</span><span class="sxs-lookup"><span data-stu-id="2015f-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2015f-168">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2015f-168">Create a virtual network</span></span>
> * <span data-ttu-id="2015f-169">Sanal ağ alt ağları oluşturma</span><span class="sxs-lookup"><span data-stu-id="2015f-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="2015f-170">Ağ güvenlik gruplarıyla ağ trafiğini denetleme</span><span class="sxs-lookup"><span data-stu-id="2015f-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="2015f-171">Eylem trafik kurallarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="2015f-171">View traffic rules in action</span></span>

<span data-ttu-id="2015f-172">Azure Yedekleme'yi kullanarak sanal makinelerde güvenli hale getirme verileri izleme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="2015f-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="2015f-173">.</span><span class="sxs-lookup"><span data-stu-id="2015f-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2015f-174">Azure'da Windows sanal makineleri yedekleyin</span><span class="sxs-lookup"><span data-stu-id="2015f-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
