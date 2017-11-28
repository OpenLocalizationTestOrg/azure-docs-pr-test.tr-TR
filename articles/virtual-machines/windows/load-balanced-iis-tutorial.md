---
title: "aaaTutorial - yapı yüksek oranda kullanılabilir bir uygulamayı Azure vm'lerde | Microsoft Docs"
description: "Bilgi nasıl toocreate Azure yük dengeleyici ile üç Windows VM'ler arasında yüksek oranda kullanılabilir ve güvenli bir uygulama"
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
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="58b65-103">Bir yük dengeli, azure'da Windows sanal makinelerde yüksek oranda kullanılabilir uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="58b65-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="58b65-104">Bu öğreticide, esnek toomaintenance olayı yüksek oranda kullanılabilir bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="58b65-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="58b65-105">Merhaba uygulaması bir yük dengeleyici, bir kullanılabilirlik kümesi ve üç Windows sanal makineleri (VM'ler) kullanır.</span><span class="sxs-lookup"><span data-stu-id="58b65-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="58b65-106">Bu öğretici IIS yükler, kullanabilirsiniz ancak farklı uygulama framework kullanarak Bu öğretici toodeploy hello aynı yüksek kullanılabilirlik bileşenleri ve yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="58b65-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="58b65-107">1. adım - Azure önkoşulları</span><span class="sxs-lookup"><span data-stu-id="58b65-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="58b65-108">toocomplete Bu öğretici, hello son yüklediğinizden emin olun [Azure PowerShell](/powershell/azure/overview) modülü.</span><span class="sxs-lookup"><span data-stu-id="58b65-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="58b65-109">İlk olarak, tooyour hello Login-AzureRmAccount komutu Azure aboneliğiyle oturum ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="58b65-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="58b65-110">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="58b65-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="58b65-111">Diğer Azure kaynaklarına oluşturabilmeniz için önce bir kaynak grubu ile toocreate gerekir [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="58b65-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="58b65-112">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westeurope` bölge:</span><span class="sxs-lookup"><span data-stu-id="58b65-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="58b65-113">2. adım - kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="58b65-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="58b65-114">Sanal makineler arasında mantıksal hataya oluşturulabilir ve güncelleme etki alanları.</span><span class="sxs-lookup"><span data-stu-id="58b65-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="58b65-115">Her mantıksal bir etki alanı donanım hello temel Azure veri merkezinde bir bölümünü temsil eder.</span><span class="sxs-lookup"><span data-stu-id="58b65-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="58b65-116">İki veya daha fazla sanal makine oluşturduğunuzda, işlem ve depolama kaynaklarınızı bu etki alanları arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="58b65-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="58b65-117">Donanım bileşeni bakım gerekiyorsa bu dağıtım, uygulamanızın hello kullanılabilirlik tutar.</span><span class="sxs-lookup"><span data-stu-id="58b65-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="58b65-118">Kullanılabilirlik kümeleri, bu mantıksal arıza ve güncelleştirme etki alanları tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="58b65-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="58b65-119">Kullanılabilirlik kümesi oluştur [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="58b65-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="58b65-120">Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="58b65-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="58b65-121">3. adım - oluşturma yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="58b65-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="58b65-122">Bir Azure yük dengeleyici trafiği yük dengeleyici kuralları kullanarak tanımlanan VM'ler kümesi arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="58b65-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="58b65-123">Bir sistem durumu araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM.</span><span class="sxs-lookup"><span data-stu-id="58b65-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="58b65-124">Ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="58b65-124">Create public IP address</span></span>

<span data-ttu-id="58b65-125">tooaccess uygulamanızı hello Internet üzerinde bir ortak IP adresi toohello yük dengeleyici atayın.</span><span class="sxs-lookup"><span data-stu-id="58b65-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="58b65-126">Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="58b65-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="58b65-127">Merhaba aşağıdaki örnekte oluşturur adlı ortak IP adresi `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="58b65-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="58b65-128">Yük Dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="58b65-128">Create load balancer</span></span>

<span data-ttu-id="58b65-129">Bir ön uç IP adresiyle oluşturma [yeni AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="58b65-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="58b65-130">Merhaba aşağıdaki örnekte oluşturur adlı bir ön uç IP adresi `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="58b65-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="58b65-131">Olan bir arka uç adres havuzu oluşturma [yeni AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="58b65-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="58b65-132">Merhaba aşağıdaki örnekte oluşturur adlı arka uç adres havuzu `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="58b65-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="58b65-133">Şimdi, hello yük dengeleyici ile oluşturmak [yeni AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="58b65-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="58b65-134">Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur `myLoadBalancer` hello kullanarak `myPublicIP` adresi:</span><span class="sxs-lookup"><span data-stu-id="58b65-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="58b65-135">Sistem durumu araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="58b65-135">Create health probe</span></span>

<span data-ttu-id="58b65-136">tooallow hello yük dengeleyici toomonitor hello durumu, uygulamanızın bir sistem durumu araştırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="58b65-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="58b65-137">Merhaba durumu araştırması dinamik olarak ekler veya kendi yanıt toohealth denetimleri temel hello yük dengeleyici döndürme VM'ler kaldırır.</span><span class="sxs-lookup"><span data-stu-id="58b65-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="58b65-138">Varsayılan olarak, bir VM hello yük dengeleyici dağıtımı 15 saniyelik aralıklarda iki ardışık hatadan sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="58b65-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="58b65-139">Bir sistem durumu araştırması ile oluşturma [Ekle AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="58b65-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="58b65-140">Merhaba aşağıdaki örnek adlı bir sistem durumu araştırması oluşturur `myHealthProbe` her VM izler:</span><span class="sxs-lookup"><span data-stu-id="58b65-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="58b65-141">Yük Dengeleyici kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="58b65-141">Create load balancer rule</span></span>

<span data-ttu-id="58b65-142">Yük Dengeleyici kuralı kullanılan toodefine olduğu dağıtılmış toohello VM'ler nasıl trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="58b65-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="58b65-143">Yük Dengeleyici kuralı ile oluşturma [Ekle AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="58b65-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="58b65-144">Merhaba aşağıdaki örnek adlı bir yük dengeleyici kuralı oluşturur `myLoadBalancerRule` ve bağlantı noktası üzerinde trafiği dengeler `80`:</span><span class="sxs-lookup"><span data-stu-id="58b65-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="58b65-145">Merhaba yük dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="58b65-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="58b65-146">4. adım - ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="58b65-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="58b65-147">Her bir VM sanal ağ tooa bağlanan bir veya daha fazla sanal ağ arabirim kartları (NIC) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="58b65-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="58b65-148">Bu sanal ağ tanımlanmış erişim kurallarına göre toofilter trafiği güvenli hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="58b65-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="58b65-149">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="58b65-149">Create virtual network</span></span>

<span data-ttu-id="58b65-150">İlk olarak, bir alt ağ ile yapılandırma [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="58b65-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="58b65-151">Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="58b65-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="58b65-152">tooprovide ağ bağlantısı tooyour VM oluşturma bir sanal ağ ile [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="58b65-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="58b65-153">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur `myVnet` ile `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="58b65-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="58b65-154">Ağ güvenliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="58b65-154">Configure network security</span></span>

<span data-ttu-id="58b65-155">Bir Azure [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) (NSG) bir veya daha çok sanal makineler için gelen ve giden trafik denetler.</span><span class="sxs-lookup"><span data-stu-id="58b65-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="58b65-156">Ağ güvenlik grubu kurallarının izin verin veya belirli bir bağlantı noktası veya bağlantı noktası aralığı ağ trafiği engelle.</span><span class="sxs-lookup"><span data-stu-id="58b65-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="58b65-157">Önceden tanımlanmış bir kaynakta kaynaklanan trafiğin yalnızca bir sanal makineyle iletişim kurabilmesi için bu kurallar kaynak adres öneki de içerir.</span><span class="sxs-lookup"><span data-stu-id="58b65-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="58b65-158">tooallow trafiği tooreach uygulamanızı web, bir ağ güvenlik grubu kural oluştururken [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="58b65-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="58b65-159">Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu kural `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="58b65-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="58b65-160">Bir ağ güvenlik grubu oluşturma [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="58b65-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="58b65-161">Merhaba aşağıdaki örnekte oluşturur adlı bir NSG `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="58b65-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="58b65-162">Merhaba ağ güvenlik grubu toohello olan bir alt ağ Ekle [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="58b65-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="58b65-163">Güncelleştirme hello sanal ağ ile [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="58b65-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="58b65-164">Sanal ağ arabirim kartları oluşturma</span><span class="sxs-lookup"><span data-stu-id="58b65-164">Create virtual network interface cards</span></span>

<span data-ttu-id="58b65-165">Yük Dengeleyici işlevi hello sanal NIC kaynakla yerine gerçek VM hello.</span><span class="sxs-lookup"><span data-stu-id="58b65-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="58b65-166">Merhaba sanal NIC bağlı toohello yük dengeleyicinin ve tooa VM bağlı.</span><span class="sxs-lookup"><span data-stu-id="58b65-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="58b65-167">Bir sanal NIC ile oluşturma [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="58b65-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="58b65-168">Merhaba aşağıdaki örnek üç sanal NIC oluşturur.</span><span class="sxs-lookup"><span data-stu-id="58b65-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="58b65-169">(Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için):</span><span class="sxs-lookup"><span data-stu-id="58b65-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="58b65-170">5. adım - sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="58b65-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="58b65-171">Yerinde bileşenleri için temel alınan tüm hello ile uygulamanızı artık yüksek oranda kullanılabilir sanal makineleri toorun oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58b65-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="58b65-172">Merhaba kullanıcı adı ve parola ile Merhaba sanal makinede hello yönetici hesabı için gerekli alma [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="58b65-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="58b65-173">Merhaba VM'ler ile oluşturmak [yeni AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [kümesi AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [kümesi AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Ekleme AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), ve [AzureRmVM yeni](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="58b65-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="58b65-174">Aşağıdaki örnek hello üç VM'ler oluşturur:</span><span class="sxs-lookup"><span data-stu-id="58b65-174">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="58b65-175">Birkaç dakika toocreate alır ve tüm üç VM'ler yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="58b65-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="58b65-176">Merhaba uygulamayı her VM çalıştıran hello yük dengeleyici durum araştırması otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="58b65-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="58b65-177">Merhaba uygulama çalışmaya başladıktan sonra hello yük dengeleyici kuralı toodistribute trafiği başlatır.</span><span class="sxs-lookup"><span data-stu-id="58b65-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="58b65-178">Merhaba uygulamasını yükleyin</span><span class="sxs-lookup"><span data-stu-id="58b65-178">Install hello app</span></span> 

<span data-ttu-id="58b65-179">Azure sanal makinesi, uygulama yükleme ve yapılandırma hello işletim sistemi gibi kullanılan tooautomate sanal makine yapılandırma görevleri uzantılarıdır.</span><span class="sxs-lookup"><span data-stu-id="58b65-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="58b65-180">Merhaba [Windows için özel betik uzantısı](./../virtual-machines-windows-extensions-customscript.md) kullanılan toorun hello sanal makinede bir PowerShell betiğidir.</span><span class="sxs-lookup"><span data-stu-id="58b65-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="58b65-181">Merhaba komut dosyası Azure depolama alanında, erişilebilir tüm HTTP uç noktası depolanan veya hello özel betik uzantısı yapılandırmasında katıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="58b65-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="58b65-182">Merhaba özel betik uzantısı kullanırken hello Azure VM Aracısı hello betik yürütme yönetir.</span><span class="sxs-lookup"><span data-stu-id="58b65-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="58b65-183">Kullanım [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello özel betik uzantısı.</span><span class="sxs-lookup"><span data-stu-id="58b65-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="58b65-184">Merhaba uzantısı çalışır `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS Web sunucusu:</span><span class="sxs-lookup"><span data-stu-id="58b65-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="58b65-185">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="58b65-185">Test your app</span></span>

<span data-ttu-id="58b65-186">Merhaba, yük dengeleyici ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="58b65-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="58b65-187">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi `myPublicIP` daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="58b65-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="58b65-188">Tooa web tarayıcısında Hello genel IP adresi girin.</span><span class="sxs-lookup"><span data-stu-id="58b65-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="58b65-189">Yerinde Hello NSG kuralı ile Merhaba varsayılan IIS Web sitesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="58b65-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Varsayılan IIS sitesi](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="58b65-191">6. adım – yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="58b65-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="58b65-192">Merhaba işletim sistemi güncelleştirmelerini yükleme gibi uygulamanızı çalıştıran VM'ler tooperform bakım gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="58b65-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="58b65-193">toodeal trafiğinin artmasına tooyour uygulamayla ihtiyacınız olabilecek tooadd ilave VM'ler.</span><span class="sxs-lookup"><span data-stu-id="58b65-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="58b65-194">Bu bölümde, nasıl gösterilir tooremove veya VM hello yük dengeleyiciden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="58b65-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="58b65-195">Bir VM hello yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="58b65-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="58b65-196">Bir VM hello ağ arabirim kartı hello LoadBalancerBackendAddressPools özelliği sıfırlayarak hello arka uç adres havuzundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="58b65-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="58b65-197">Merhaba ağ arabirimi kartı ile [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="58b65-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="58b65-198">Merhaba ağ arabirim kartı Hello LoadBalancerBackendAddressPools özelliğini çok Ayarla $null:</span><span class="sxs-lookup"><span data-stu-id="58b65-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="58b65-199">Merhaba ağ arabirim kartı güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="58b65-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="58b65-200">Bir VM toohello yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="58b65-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="58b65-201">VM bakım yapmak veya tooexpand kapasitesine ihtiyacınız varsa, hello NIC VM toohello arka uç adres havuzu hello yük dengeleyici ekleme sonra.</span><span class="sxs-lookup"><span data-stu-id="58b65-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="58b65-202">Merhaba yük dengeleyici alın:</span><span class="sxs-lookup"><span data-stu-id="58b65-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="58b65-203">Merhaba yük dengeleyici toohello ağ arabirim kartı Hello arka uç adres havuzu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="58b65-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="58b65-204">Merhaba ağ arabirim kartı güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="58b65-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="58b65-205">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="58b65-205">Next Steps</span></span>

<span data-ttu-id="58b65-206">Örnekleri – [Azure sanal makine PowerShell örnek betikler](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="58b65-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
