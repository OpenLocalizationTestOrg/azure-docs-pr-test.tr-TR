---
title: "Nasıl yükleneceğini azure'da Windows sanal makineler Bakiye | Microsoft Docs"
description: "Üç Windows sanal makineyi yüksek oranda kullanılabilir ve güvenli bir uygulama oluşturmak için Azure yük dengeleyici kullanmayı öğrenin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6738d88d5a0430abaf3855dbf97a618e4c83617f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="076d6-103">Nasıl yükleneceğini yüksek oranda kullanılabilir bir uygulama oluşturmak için azure'da Windows sanal makineler Bakiye</span><span class="sxs-lookup"><span data-stu-id="076d6-103">How to load balance Windows virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="076d6-104">Yük Dengeleme, birden çok sanal makine genelinde gelen istekleri yayarak daha yüksek düzeyde kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="076d6-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="076d6-105">Bu öğreticide, trafiği dağıtmak ve yüksek kullanılabilirlik sağlayan farklı bileşenleri, Azure yük dengeleyici hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="076d6-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="076d6-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="076d6-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="076d6-107">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="076d6-108">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="076d6-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="076d6-109">Yük Dengeleyici trafiği kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="076d6-110">Temel bir IIS sitesi oluşturmak için özel betik uzantısı kullanın</span><span class="sxs-lookup"><span data-stu-id="076d6-110">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="076d6-111">Sanal makineler oluşturun ve bir yük dengeleyiciye ekleyin</span><span class="sxs-lookup"><span data-stu-id="076d6-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="076d6-112">Bir yük dengeleyici eylemde görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="076d6-112">View a load balancer in action</span></span>
> * <span data-ttu-id="076d6-113">Ekleme ve sanal makineleri yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="076d6-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="076d6-114">Bu öğretici, Azure PowerShell modülü 3.6 veya sonraki bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="076d6-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="076d6-115">Sürümü bulmak için ` Get-Module -ListAvailable AzureRM` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="076d6-115">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="076d6-116">Yükseltme gerekiyorsa, bkz: [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="076d6-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="076d6-117">Azure yük dengeleyici genel bakış</span><span class="sxs-lookup"><span data-stu-id="076d6-117">Azure load balancer overview</span></span>
<span data-ttu-id="076d6-118">Bir Azure yük dengeleyici gelen trafiği sağlıklı VM'ler arasında dağıtarak yüksek kullanılabilirlik sağlayan bir katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="076d6-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="076d6-119">Bir yük dengeleyici durum araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafiği işletimsel bir VM dağıtır.</span><span class="sxs-lookup"><span data-stu-id="076d6-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="076d6-120">Bir veya daha fazla ortak IP adreslerini içeren bir ön uç IP yapılandırmasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="076d6-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="076d6-121">Bu ön uç IP yapılandırmasını yük dengeleyici ve uygulamaların Internet üzerinden erişilebilir olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="076d6-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="076d6-122">Sanal makineler kendi sanal ağ arabirim kartı (NIC) kullanarak bir yük dengeleyiciye bağlayın.</span><span class="sxs-lookup"><span data-stu-id="076d6-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="076d6-123">VM'ler trafiğini dağıtmak için bir arka uç adres havuzu IP içeren sanal (NIC'ler) adreslerini yük dengeleyiciye bağlı.</span><span class="sxs-lookup"><span data-stu-id="076d6-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="076d6-124">Trafik akışını denetlemek için belirli bağlantı noktalarını ve Vm'leriniz için eşleme protokolleri için yük dengeleyici kuralları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="076d6-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="076d6-125">Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-125">Create Azure load balancer</span></span>
<span data-ttu-id="076d6-126">Bu bölümde, nasıl oluşturma ve her bileşenin yük dengeleyicinin yapılandırma ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="076d6-126">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="076d6-127">Yük Dengeleyici oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="076d6-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="076d6-128">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroupLoadBalancer* içinde *EastUS* konumu:</span><span class="sxs-lookup"><span data-stu-id="076d6-128">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="076d6-129">Genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-129">Create a public IP address</span></span>
<span data-ttu-id="076d6-130">Uygulamanızı Internet'te erişmek için yük dengeleyici için bir ortak IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="076d6-130">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="076d6-131">Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="076d6-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="076d6-132">Aşağıdaki örnek adlı ortak IP adresi oluşturur *myPublicIP* içinde *myResourceGroupLoadBalancer* kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="076d6-132">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="076d6-133">Yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-133">Create a load balancer</span></span>
<span data-ttu-id="076d6-134">Bir ön uç IP adresiyle oluşturma [yeni AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="076d6-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="076d6-135">Aşağıdaki örnek, adlandırılmış bir ön uç IP adresi oluşturur *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="076d6-135">The following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="076d6-136">Olan bir arka uç adres havuzu oluşturma [yeni AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="076d6-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="076d6-137">Aşağıdaki örnek, adlandırılmış bir arka uç adres havuzu oluşturur *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="076d6-137">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="076d6-138">Şimdi, olan yük dengeleyici oluşturma [yeni AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="076d6-138">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="076d6-139">Aşağıdaki örnek, adlandırılmış bir yük dengeleyici oluşturur *myLoadBalancer* kullanarak *myPublicIP* adresi:</span><span class="sxs-lookup"><span data-stu-id="076d6-139">The following example creates a load balancer named *myLoadBalancer* using the *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="076d6-140">Bir sistem durumu araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="076d6-140">Create a health probe</span></span>
<span data-ttu-id="076d6-141">Uygulamanızın durumunu izlemek yük dengeleyici izin vermek için bir sistem durumu araştırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="076d6-141">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="076d6-142">Sistem durumu araştırma dinamik olarak ekler veya bunların yanıtını durumu denetimleri için temel yük dengeleyici döndürme VM'ler kaldırır.</span><span class="sxs-lookup"><span data-stu-id="076d6-142">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="076d6-143">Varsayılan olarak, bir VM yük dengeleyici dağıtımı 15 saniyelik aralıklarda iki ardışık hatadan sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="076d6-143">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="076d6-144">Bir protokol veya belirli bir sistem onay sayfasında uygulamanız için temel bir sistem durumu araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="076d6-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="076d6-145">Aşağıdaki örnekte bir TCP araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="076d6-145">The following example creates a TCP probe.</span></span> <span data-ttu-id="076d6-146">Daha fazla hassas sistem durumu denetimlerinin özel HTTP araştırmalara de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="076d6-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="076d6-147">Özel bir HTTP araştırma kullanırken, sistem durumu denetimi sayfası gibi oluşturmalısınız *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="076d6-147">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="076d6-148">Araştırma döndürmelidir bir **HTTP 200 Tamam** dönüş konak tutmak yük dengeleyici için yanıt.</span><span class="sxs-lookup"><span data-stu-id="076d6-148">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="076d6-149">TCP durumu araştırması oluşturmak için kullandığınız [Ekle AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="076d6-149">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="076d6-150">Aşağıdaki örnek adlı bir sistem durumu araştırması oluşturur *myHealthProbe* her VM izler:</span><span class="sxs-lookup"><span data-stu-id="076d6-150">The following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="076d6-151">Yük Dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="076d6-151">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="076d6-152">Yük Dengeleyici kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-152">Create a load balancer rule</span></span>
<span data-ttu-id="076d6-153">Yük Dengeleyici kuralı trafiğin Vm'lere nasıl dağıtıldığını tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="076d6-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="076d6-154">Gelen trafiği ve gerekli kaynak ve hedef bağlantı noktası ile birlikte trafiği almak için arka uç IP havuzu için ön uç IP yapılandırmasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="076d6-154">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="076d6-155">Yalnızca sağlıklı VM'ler trafiği aldığınızdan emin olmak için aynı zamanda kullanmak için sistem durumu araştırma tanımlar.</span><span class="sxs-lookup"><span data-stu-id="076d6-155">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="076d6-156">Yük Dengeleyici kuralı ile oluşturma [Ekle AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="076d6-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="076d6-157">Aşağıdaki örnek adlı yük dengeleyici kuralı oluşturur *myLoadBalancerRule* ve bağlantı noktası üzerinde trafiği dengeler *80*:</span><span class="sxs-lookup"><span data-stu-id="076d6-157">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="076d6-158">Yük Dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="076d6-158">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="076d6-159">Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="076d6-159">Configure virtual network</span></span>
<span data-ttu-id="076d6-160">Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce destekleyici sanal ağ kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="076d6-160">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="076d6-161">Sanal ağlar hakkında daha fazla bilgi için bkz: [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="076d6-161">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="076d6-162">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="076d6-162">Create network resources</span></span>
<span data-ttu-id="076d6-163">Bir sanal ağ ile oluşturma [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="076d6-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="076d6-164">Aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ile *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="076d6-164">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="076d6-165">Ağ güvenlik grubu kural oluştururken [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), bir ağ güvenlik grubu oluşturma [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="076d6-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="076d6-166">Alt ağ ile ağ güvenlik grubu eklemek [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) ve sanal ağ ile güncelleştirme [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="076d6-166">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="076d6-167">Aşağıdaki örnek adlı bir ağ güvenlik grubu kural oluşturur *myNetworkSecurityGroup* ve uygular *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="076d6-167">The following example creates a network security group rule named *myNetworkSecurityGroup* and applies it to *mySubnet*:</span></span>

```powershell
# Create security rule config
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

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="076d6-168">Sanal NIC ile oluşturulan [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="076d6-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="076d6-169">Aşağıdaki örnek, üç sanal NIC oluşturur.</span><span class="sxs-lookup"><span data-stu-id="076d6-169">The following example creates three virtual NICs.</span></span> <span data-ttu-id="076d6-170">(Her VM için bir sanal NIC için aşağıdaki adımları uygulamayı oluşturduğunuz).</span><span class="sxs-lookup"><span data-stu-id="076d6-170">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="076d6-171">Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturabilir ve bunları yük dengeleyiciye ekleyin:</span><span class="sxs-lookup"><span data-stu-id="076d6-171">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="076d6-172">Sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-172">Create virtual machines</span></span>
<span data-ttu-id="076d6-173">Uygulamanızı yüksek kullanılabilirliğini artırmak için bir kullanılabilirlik kümesine Vm'leriniz yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="076d6-173">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="076d6-174">Kullanılabilirlik kümesi oluştur [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="076d6-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="076d6-175">Aşağıdaki örnek, kullanılabilirlik adlandırılmış kümesi oluşturur *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="076d6-175">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="076d6-176">Yönetici olan VM'ler için kullanıcı adı ve parola ayarlayın [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="076d6-176">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="076d6-177">VM'lerin oluşturabileceğiniz artık [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="076d6-177">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="076d6-178">Aşağıdaki örnekte, üç VM'ler oluşturur:</span><span class="sxs-lookup"><span data-stu-id="076d6-178">The following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="076d6-179">Oluşturun ve tüm üç sanal makineleri yapılandırmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="076d6-179">It takes a few minutes to create and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="076d6-180">Özel betik uzantısı ile IIS yükleme</span><span class="sxs-lookup"><span data-stu-id="076d6-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="076d6-181">Önceki bir öğretici içinde [Windows sanal makine özelleştirmek nasıl](tutorial-automate-vm-deployment.md), Windows için özel betik uzantısı ile VM özelleştirme otomatikleştirmek öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="076d6-181">In a previous tutorial on [How to customize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with the Custom Script Extension for Windows.</span></span> <span data-ttu-id="076d6-182">Aynı yaklaşımı yükleyip Vm'leriniz IIS yapılandırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="076d6-182">You can use the same approach to install and configure IIS on your VMs.</span></span>

<span data-ttu-id="076d6-183">Kullanım [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) özel betik uzantısı yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="076d6-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="076d6-184">Uzantı çalışır `powershell Add-WindowsFeature Web-Server` IIS Web sunucusu ve ardından güncelleştirmeleri yüklemek için *Default.htm* sayfası ana bilgisayar VM adını göster:</span><span class="sxs-lookup"><span data-stu-id="076d6-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="076d6-185">Test yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="076d6-185">Test load balancer</span></span>
<span data-ttu-id="076d6-186">Yük Dengeleyici ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="076d6-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="076d6-187">Aşağıdaki örnek IP adresi alacağı *myPublicIP* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="076d6-187">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="076d6-188">Bir web tarayıcısı ortak IP adresi girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="076d6-188">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="076d6-189">Yük Dengeleyici trafiği için aşağıdaki örnekteki gibi dağıtılmış VM konak adı dahil olmak üzere Web sitesi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="076d6-189">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Çalışan IIS Web sitesi](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="076d6-191">Uygulamanızı çalıştıran tüm üç VM'ler arasında trafiği dağıtmak yük dengeleyici görmek için zorla-web tarayıcınızı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="076d6-191">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="076d6-192">Sanal makineleri ekleyip</span><span class="sxs-lookup"><span data-stu-id="076d6-192">Add and remove VMs</span></span>
<span data-ttu-id="076d6-193">İşletim sistemi güncelleştirmelerini yükleme gibi uygulamanızı çalıştıran VM'ler bakım yapmak gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="076d6-193">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="076d6-194">Uygulamanıza artan trafiği ile mücadele etmek için ek VM'ler eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="076d6-194">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="076d6-195">Bu bölümde kaldırın veya VM yük dengeleyiciden nasıl ekleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="076d6-195">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="076d6-196">VM yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="076d6-196">Remove a VM from the load balancer</span></span>
<span data-ttu-id="076d6-197">Ağ arabirimi kartı ile [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), ardından *LoadBalancerBackendAddressPools* sanal NIC'ye özelliğinin *$null*.</span><span class="sxs-lookup"><span data-stu-id="076d6-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set the *LoadBalancerBackendAddressPools* property of the virtual NIC to *$null*.</span></span> <span data-ttu-id="076d6-198">Son olarak, bir sanal NIC güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="076d6-198">Finally, update the virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="076d6-199">Uygulamanızı çalıştıran diğer iki VM arasında trafiği dağıtmak yük dengeleyici görmek için zorla-web tarayıcınızı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="076d6-199">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="076d6-200">İşletim sistemi güncelleştirmeleri yükleme veya VM yeniden başlatma gerçekleştirme gibi VM üzerinde bakım artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="076d6-200">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="076d6-201">VM yük dengeleyiciye ekleyin</span><span class="sxs-lookup"><span data-stu-id="076d6-201">Add a VM to the load balancer</span></span>
<span data-ttu-id="076d6-202">Sonra VM bakım yapmak veya kapasitesini genişletmek gerekiyorsa, ayarlayın *LoadBalancerBackendAddressPools* sanal NIC'ye özelliğinin *BackendAddressPool* gelen [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="076d6-202">After performing VM maintenance, or if you need to expand capacity, set the *LoadBalancerBackendAddressPools* property of the virtual NIC to the *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="076d6-203">Yük Dengeleyici alın:</span><span class="sxs-lookup"><span data-stu-id="076d6-203">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="076d6-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="076d6-204">Next steps</span></span>

<span data-ttu-id="076d6-205">Bu öğreticide, bir yük dengeleyici oluşturulur ve sanal makineleri bağlı.</span><span class="sxs-lookup"><span data-stu-id="076d6-205">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="076d6-206">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="076d6-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="076d6-207">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="076d6-208">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="076d6-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="076d6-209">Yük Dengeleyici trafiği kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="076d6-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="076d6-210">Temel bir IIS sitesi oluşturmak için özel betik uzantısı kullanın</span><span class="sxs-lookup"><span data-stu-id="076d6-210">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="076d6-211">Sanal makineler oluşturun ve bir yük dengeleyiciye ekleyin</span><span class="sxs-lookup"><span data-stu-id="076d6-211">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="076d6-212">Bir yük dengeleyici eylemde görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="076d6-212">View a load balancer in action</span></span>
> * <span data-ttu-id="076d6-213">Ekleme ve sanal makineleri yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="076d6-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="076d6-214">VM ağı yönetme konusunda bilgi almak için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="076d6-214">Advance to the next tutorial to learn how to manage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="076d6-215">VM’leri ve sanal ağları yönetme</span><span class="sxs-lookup"><span data-stu-id="076d6-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
