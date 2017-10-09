---
title: aaaHow tooload dengelemek azure'da Windows sanal makineler | Microsoft Docs
description: "Nasıl toouse hello Azure yük dengeleyici toocreate yüksek oranda kullanılabilir ve güvenli bir uygulama üç Windows VM'ler üzerindeki bilgi edinin"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="51cc7-103">Nasıl tooload Bakiye Azure toocreate Windows sanal makinesi yüksek oranda kullanılabilir bir uygulama</span><span class="sxs-lookup"><span data-stu-id="51cc7-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="51cc7-104">Yük Dengeleme, birden çok sanal makine genelinde gelen istekleri yayarak daha yüksek düzeyde kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="51cc7-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="51cc7-105">Bu öğreticide, trafiği dağıtmak ve yüksek kullanılabilirlik sağlamak hello farklı bileşenler hello Azure yük dengeleyici hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="51cc7-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="51cc7-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="51cc7-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51cc7-107">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="51cc7-108">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="51cc7-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="51cc7-109">Yük Dengeleyici trafiği kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="51cc7-110">Merhaba özel betik uzantısının toocreate temel IIS site kullanın</span><span class="sxs-lookup"><span data-stu-id="51cc7-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="51cc7-111">Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="51cc7-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="51cc7-112">Bir yük dengeleyici eylemde görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="51cc7-112">View a load balancer in action</span></span>
> * <span data-ttu-id="51cc7-113">Ekleme ve sanal makineleri yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="51cc7-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="51cc7-114">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="51cc7-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="51cc7-115">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="51cc7-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="51cc7-116">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="51cc7-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="51cc7-117">Azure yük dengeleyici genel bakış</span><span class="sxs-lookup"><span data-stu-id="51cc7-117">Azure load balancer overview</span></span>
<span data-ttu-id="51cc7-118">Bir Azure yük dengeleyici gelen trafiği sağlıklı VM'ler arasında dağıtarak yüksek kullanılabilirlik sağlayan bir katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="51cc7-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="51cc7-119">Bir yük dengeleyici durum araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM.</span><span class="sxs-lookup"><span data-stu-id="51cc7-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="51cc7-120">Bir veya daha fazla ortak IP adreslerini içeren bir ön uç IP yapılandırmasını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="51cc7-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="51cc7-121">Bu ön uç IP yapılandırmasını yük dengeleyici ve uygulamaları toobe hello Internet erişilebilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="51cc7-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="51cc7-122">Sanal makineler tooa yük dengeleyici, sanal ağ arabirim kartı (NIC) kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="51cc7-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="51cc7-123">toodistribute trafiği toohello VM'ler, bir arka uç adres havuzu hello sanal (NIC) bağlı toohello yük dengeleyici hello IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="51cc7-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="51cc7-124">toocontrol hello akış trafiği belirli bağlantı noktalarını ve tooyour VM'ler eşleme protokolleri için yük dengeleyici kuralları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="51cc7-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="51cc7-125">Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-125">Create Azure load balancer</span></span>
<span data-ttu-id="51cc7-126">Bu bölümde, nasıl oluşturma ve her bileşenin hello yük dengeleyicinin yapılandırma ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="51cc7-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="51cc7-127">Yük Dengeleyici oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="51cc7-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="51cc7-128">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupLoadBalancer* hello içinde *EastUS* konumu:</span><span class="sxs-lookup"><span data-stu-id="51cc7-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="51cc7-129">Genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-129">Create a public IP address</span></span>
<span data-ttu-id="51cc7-130">tooaccess uygulamanıza Internet Merhaba, hello yük dengeleyici için bir ortak IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="51cc7-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="51cc7-131">Bir ortak IP adresiyle oluşturma [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="51cc7-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="51cc7-132">Merhaba aşağıdaki örnekte oluşturur adlı ortak IP adresi *myPublicIP* hello içinde *myResourceGroupLoadBalancer* kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="51cc7-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="51cc7-133">Yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-133">Create a load balancer</span></span>
<span data-ttu-id="51cc7-134">Bir ön uç IP adresiyle oluşturma [yeni AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="51cc7-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="51cc7-135">Merhaba aşağıdaki örnekte oluşturur adlı bir ön uç IP adresi *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="51cc7-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="51cc7-136">Olan bir arka uç adres havuzu oluşturma [yeni AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="51cc7-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="51cc7-137">Merhaba aşağıdaki örnekte oluşturur adlı arka uç adres havuzu *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="51cc7-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="51cc7-138">Şimdi, hello yük dengeleyici ile oluşturmak [yeni AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="51cc7-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="51cc7-139">Merhaba aşağıdaki örnek adlı bir yük dengeleyici oluşturur *myLoadBalancer* hello kullanarak *myPublicIP* adresi:</span><span class="sxs-lookup"><span data-stu-id="51cc7-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="51cc7-140">Bir sistem durumu araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="51cc7-140">Create a health probe</span></span>
<span data-ttu-id="51cc7-141">tooallow hello yük dengeleyici toomonitor hello durumu, uygulamanızın bir sistem durumu araştırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="51cc7-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="51cc7-142">Merhaba durumu araştırması dinamik olarak ekler veya kendi yanıt toohealth denetimleri temel hello yük dengeleyici döndürme VM'ler kaldırır.</span><span class="sxs-lookup"><span data-stu-id="51cc7-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="51cc7-143">Varsayılan olarak, bir VM hello yük dengeleyici dağıtımı 15 saniyelik aralıklarda iki ardışık hatadan sonra kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="51cc7-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="51cc7-144">Bir protokol veya belirli bir sistem onay sayfasında uygulamanız için temel bir sistem durumu araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="51cc7-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="51cc7-145">Aşağıdaki örnek hello bir TCP araştırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="51cc7-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="51cc7-146">Daha fazla hassas sistem durumu denetimlerinin özel HTTP araştırmalara de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51cc7-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="51cc7-147">Özel bir HTTP araştırma kullanırken, hello sistem durumu onay sayfasında, aşağıdaki gibi oluşturmalısınız *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="51cc7-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="51cc7-148">Merhaba araştırma döndürmelidir bir **HTTP 200 Tamam** hello yük dengeleyici tookeep hello ana döndürme yanıtı.</span><span class="sxs-lookup"><span data-stu-id="51cc7-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="51cc7-149">toocreate TCP durumu araştırması, kullandığınız [Ekle AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="51cc7-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="51cc7-150">Merhaba aşağıdaki örnek adlı bir sistem durumu araştırması oluşturur *myHealthProbe* her VM izler:</span><span class="sxs-lookup"><span data-stu-id="51cc7-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="51cc7-151">Merhaba yük dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="51cc7-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="51cc7-152">Yük Dengeleyici kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-152">Create a load balancer rule</span></span>
<span data-ttu-id="51cc7-153">Yük Dengeleyici kuralı kullanılan toodefine olduğu dağıtılmış toohello VM'ler nasıl trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="51cc7-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="51cc7-154">Merhaba ön uç IP yapılandırmasını hello gelen trafiği ve hello arka uç IP havuzu tooreceive hello trafiği için hello gerekli kaynak ve hedef bağlantı noktası ile birlikte tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="51cc7-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="51cc7-155">toomake trafiği yalnızca sağlıklı VM'ler aldığınızdan emin, aynı zamanda hello sistem durumu araştırma toouse tanımlar.</span><span class="sxs-lookup"><span data-stu-id="51cc7-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="51cc7-156">Yük Dengeleyici kuralı ile oluşturma [Ekle AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="51cc7-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="51cc7-157">Merhaba aşağıdaki örnek adlı bir yük dengeleyici kuralı oluşturur *myLoadBalancerRule* ve bağlantı noktası üzerinde trafiği dengeler *80*:</span><span class="sxs-lookup"><span data-stu-id="51cc7-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="51cc7-158">Merhaba yük dengeleyici ile güncelleştirme [kümesi AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="51cc7-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="51cc7-159">Sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="51cc7-159">Configure virtual network</span></span>
<span data-ttu-id="51cc7-160">Bazı sanal makineleri dağıtmak ve, dengeleyici sınayabilirsiniz önce sanal ağ kaynaklarına destekleme hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="51cc7-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="51cc7-161">Sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Sanal Ağları Yönet](tutorial-virtual-network.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="51cc7-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="51cc7-162">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="51cc7-162">Create network resources</span></span>
<span data-ttu-id="51cc7-163">Bir sanal ağ ile oluşturma [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="51cc7-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="51cc7-164">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ile *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="51cc7-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="51cc7-165">Ağ güvenlik grubu kural oluştururken [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), bir ağ güvenlik grubu oluşturma [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="51cc7-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="51cc7-166">Merhaba ağ güvenlik grubu toohello olan bir alt ağ Ekle [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) ve hello sanal ağ ile güncelleştirme [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="51cc7-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="51cc7-167">Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu kural *myNetworkSecurityGroup* ve çok geçerlidir*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="51cc7-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="51cc7-168">Sanal NIC ile oluşturulan [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="51cc7-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="51cc7-169">Merhaba aşağıdaki örnek üç sanal NIC oluşturur.</span><span class="sxs-lookup"><span data-stu-id="51cc7-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="51cc7-170">(Bir sanal NIC aşağıdaki hello uygulamanızda adımları için oluşturduğunuz her VM için).</span><span class="sxs-lookup"><span data-stu-id="51cc7-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="51cc7-171">Ek sanal NIC ve sanal makineleri herhangi bir zamanda oluşturmak ve bunları toohello yük dengeleyici Ekle:</span><span class="sxs-lookup"><span data-stu-id="51cc7-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="51cc7-172">Sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-172">Create virtual machines</span></span>
<span data-ttu-id="51cc7-173">tooimprove hello yüksek kullanılabilirlik, uygulamanızın bir kullanılabilirlik kümesine Vm'leriniz yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="51cc7-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="51cc7-174">Kullanılabilirlik kümesi oluştur [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="51cc7-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="51cc7-175">Merhaba aşağıdaki örnekte oluşturur kullanılabilirlik adlandırılmış kümesi *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="51cc7-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="51cc7-176">Yönetici olan hello VM'ler için kullanıcı adı ve parola ayarlayın [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="51cc7-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="51cc7-177">Merhaba VM'ler ile oluşturduğunuz artık [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="51cc7-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="51cc7-178">Aşağıdaki örnek hello üç VM'ler oluşturur:</span><span class="sxs-lookup"><span data-stu-id="51cc7-178">hello following example creates three VMs:</span></span>

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

<span data-ttu-id="51cc7-179">Birkaç dakika toocreate alır ve tüm üç VM'ler yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="51cc7-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="51cc7-180">Özel betik uzantısı ile IIS yükleme</span><span class="sxs-lookup"><span data-stu-id="51cc7-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="51cc7-181">Önceki bir öğretici içinde [nasıl toocustomize Windows sanal makine](tutorial-automate-vm-deployment.md), nasıl özel betik uzantısı için Windows hello tooautomate VM özelleştirmesiyle öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="51cc7-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="51cc7-182">Merhaba kullanabilirsiniz aynı tooinstall yaklaşmak ve IIS Vm'leriniz yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="51cc7-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="51cc7-183">Kullanım [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello özel betik uzantısı.</span><span class="sxs-lookup"><span data-stu-id="51cc7-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="51cc7-184">Merhaba uzantısı çalışır `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS Web sunucusu ve ardından güncelleştirmeleri hello *Default.htm* sayfa tooshow hello hello VM konak adı:</span><span class="sxs-lookup"><span data-stu-id="51cc7-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="51cc7-185">Test yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="51cc7-185">Test load balancer</span></span>
<span data-ttu-id="51cc7-186">Merhaba, yük dengeleyici ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="51cc7-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="51cc7-187">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="51cc7-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="51cc7-188">Ardından tooa web tarayıcısında hello genel IP adresi girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51cc7-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="51cc7-189">Merhaba Web sitesi gösterilir, hello VM hello hostname dahil olmak üzere bu hello yük dengeleyici trafiği tooas aşağıdaki örneğine hello içinde dağıtılmış:</span><span class="sxs-lookup"><span data-stu-id="51cc7-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Çalışan IIS Web sitesi](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="51cc7-191">toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm üç VM'ler arasında trafiği dağıtmak, zorla web tarayıcınızı yenileme.</span><span class="sxs-lookup"><span data-stu-id="51cc7-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="51cc7-192">Sanal makineleri ekleyip</span><span class="sxs-lookup"><span data-stu-id="51cc7-192">Add and remove VMs</span></span>
<span data-ttu-id="51cc7-193">Merhaba işletim sistemi güncelleştirmelerini yükleme gibi uygulamanızı çalıştıran VM'ler tooperform bakım gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="51cc7-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="51cc7-194">toodeal trafiğinin artmasına tooyour uygulamayla ihtiyacınız olabilecek tooadd ilave VM'ler.</span><span class="sxs-lookup"><span data-stu-id="51cc7-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="51cc7-195">Bu bölümde, nasıl gösterilir tooremove veya VM hello yük dengeleyiciden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="51cc7-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="51cc7-196">Bir VM hello yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="51cc7-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="51cc7-197">Merhaba ağ arabirimi kartı ile [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), ardından kümesi hello *LoadBalancerBackendAddressPools* özelliği hello sanal NIC çok*$null*.</span><span class="sxs-lookup"><span data-stu-id="51cc7-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="51cc7-198">Son olarak, sanal NIC hello güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="51cc7-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="51cc7-199">toosee hello yük dengeleyici iki kalan hello arasında trafiği dağıtmak uygulamanızı çalıştıran VM'ler, zorla web tarayıcınızı yenileme.</span><span class="sxs-lookup"><span data-stu-id="51cc7-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="51cc7-200">Merhaba işletim sistemi güncelleştirmeleri yükleme veya VM yeniden başlatma gerçekleştirme gibi VM üzerinde bakım artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51cc7-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="51cc7-201">Bir VM toohello yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="51cc7-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="51cc7-202">Sonra VM bakım yapmak veya tooexpand kapasitesine ihtiyacınız varsa, hello ayarlayın *LoadBalancerBackendAddressPools* hello sanal NIC toohello özelliğinin *BackendAddressPool* gelen [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="51cc7-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="51cc7-203">Merhaba yük dengeleyici alın:</span><span class="sxs-lookup"><span data-stu-id="51cc7-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="51cc7-204">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51cc7-204">Next steps</span></span>

<span data-ttu-id="51cc7-205">Bu öğreticide, bir yük dengeleyici oluşturulur ve sanal makineleri tooit bağlı.</span><span class="sxs-lookup"><span data-stu-id="51cc7-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="51cc7-206">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="51cc7-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51cc7-207">Bir Azure yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="51cc7-208">Bir yük dengeleyici durum araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="51cc7-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="51cc7-209">Yük Dengeleyici trafiği kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="51cc7-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="51cc7-210">Merhaba özel betik uzantısının toocreate temel IIS site kullanın</span><span class="sxs-lookup"><span data-stu-id="51cc7-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="51cc7-211">Sanal makineler oluşturmak ve tooa yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="51cc7-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="51cc7-212">Bir yük dengeleyici eylemde görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="51cc7-212">View a load balancer in action</span></span>
> * <span data-ttu-id="51cc7-213">Ekleme ve sanal makineleri yük dengeleyiciden kaldırın</span><span class="sxs-lookup"><span data-stu-id="51cc7-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="51cc7-214">Toohello sonraki öğretici toolearn nasıl ilerlemek toomanage VM ağı.</span><span class="sxs-lookup"><span data-stu-id="51cc7-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51cc7-215">VM’leri ve sanal ağları yönetme</span><span class="sxs-lookup"><span data-stu-id="51cc7-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
