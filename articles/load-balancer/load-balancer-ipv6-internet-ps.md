---
title: "IPv6 - PowerShell ile aaaCreate bir Azure Internet'e yönelik Yük Dengeleyici | Microsoft Docs"
description: "Nasıl toocreate bir İnternete yük dengeleyici kaynak yöneticisi için PowerShell kullanarak IPv6 ile bilgi edinin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, azure yük dengeleyici, çift yığın, genel IP, yerel IPv6, mobil, IOT"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="9e42a-104">Internet'e yönelik Yük Dengeleyici kaynak yöneticisi için PowerShell kullanarak IPv6 oluşturmaya başlamak</span><span class="sxs-lookup"><span data-stu-id="9e42a-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e42a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e42a-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="9e42a-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9e42a-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="9e42a-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="9e42a-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="9e42a-108">Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="9e42a-109">Merhaba yük dengeleyici, gelen trafiği bulut Hizmetleri sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e42a-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="9e42a-110">Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="9e42a-111">Örnek dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="9e42a-111">Example deployment scenario</span></span>

<span data-ttu-id="9e42a-112">Merhaba Aşağıdaki diyagramda hello yük dengeleme çözümü bu makalede dağıtılan gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![Yük dengeleyici senaryosu](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="9e42a-114">Bu senaryoda aşağıdaki Azure kaynakları hello oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="9e42a-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="9e42a-115">bir IPv4 ve IPv6 genel IP adresi olan bir Internet'e yönelik Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="9e42a-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="9e42a-116">iki Yük Dengeleme kuralları toomap hello ortak VIP'ler toohello özel uç noktaları</span><span class="sxs-lookup"><span data-stu-id="9e42a-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="9e42a-117">Merhaba iki sanal makineleri bir kullanılabilirlik kümesi toothat içerir</span><span class="sxs-lookup"><span data-stu-id="9e42a-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="9e42a-118">iki sanal makine (VM)</span><span class="sxs-lookup"><span data-stu-id="9e42a-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="9e42a-119">atanan IPv4 ve IPv6 adreslerinin her VM için bir sanal ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="9e42a-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="9e42a-120">Hello Azure PowerShell kullanarak hello çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="9e42a-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="9e42a-121">Aşağıdaki adımları hello nasıl toocreate Internet'e yönelik Yük Dengeleyici PowerShell ile Azure Resource Manager kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="9e42a-122">Azure Resource Manager ile her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır, ardından birlikte toocreate kaynak alın.</span><span class="sxs-lookup"><span data-stu-id="9e42a-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="9e42a-123">oluşturma ve nesneleri aşağıdaki hello yapılandırma toodeploy bir yük dengeleyici:</span><span class="sxs-lookup"><span data-stu-id="9e42a-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="9e42a-124">Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="9e42a-125">Arka uç adres havuzu - hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="9e42a-126">Yük Dengeleme kuralları - hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="9e42a-127">Gelen NAT kuralları - noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="9e42a-128">Yoklamaları - sistem durumu kullanılan araştırmalar toocheck kullanılabilirliği hello arka uç adres havuzundaki sanal makineler örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="9e42a-129">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9e42a-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="9e42a-130">Resource Manager PowerShell toouse ayarlayın</span><span class="sxs-lookup"><span data-stu-id="9e42a-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="9e42a-131">Merhaba son üretim hello Azure Resource Manager modülü sürümü için PowerShell olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="9e42a-132">Oturum Azure açın</span><span class="sxs-lookup"><span data-stu-id="9e42a-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="9e42a-133">İstendiğinde kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="9e42a-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="9e42a-134">Merhaba hesabının Hello abonelikleri kontrol edin</span><span class="sxs-lookup"><span data-stu-id="9e42a-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="9e42a-135">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="9e42a-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="9e42a-136">Bir kaynak grubu (var olan bir kaynak grubu kullanıyorsanız bu adımı atla) oluşturun</span><span class="sxs-lookup"><span data-stu-id="9e42a-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="9e42a-137">Bir sanal ağ ve hello ön uç IP havuzu için bir ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="9e42a-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="9e42a-138">Bir sanal ağ alt ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="9e42a-139">Azure genel IP adresi (PIP) kaynakları için hello ön uç IP adresi havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="9e42a-140">Merhaba yük dengeleyicisi hello etki alanı etiketi hello ortak IP FQDN'sini için önek olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e42a-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="9e42a-141">Bu örnekte, hello FQDN'ler olan *lbnrpipv4.westus.cloudapp.azure.com* ve *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="9e42a-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="9e42a-142">Bir ön uç IP yapılandırmaları ve arka uç adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e42a-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="9e42a-143">Oluşturduğunuz hello ortak IP adresleri kullanan ön uç adresi yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="9e42a-144">Arka uç adres havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="9e42a-145">LB kuralları, NAT kuralları, bir araştırma ve bir yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e42a-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="9e42a-146">Bu örnekte aşağıdaki öğelerindeki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="9e42a-146">This example creates hello following items:</span></span>

* <span data-ttu-id="9e42a-147">NAT kuralı tootranslate 443 numaralı bağlantı noktasını tooport 4443 tüm gelen trafiği</span><span class="sxs-lookup"><span data-stu-id="9e42a-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="9e42a-148">bir yük dengeleyici kuralı toobalance hello arka uç havuzundaki tüm gelen trafiği hello üzerinde bağlantı noktası 80 tooport 80 giderir.</span><span class="sxs-lookup"><span data-stu-id="9e42a-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="9e42a-149">bir yük dengeleyici kuralı tooallow RDP bağlantı toohello 3389 numaralı bağlantı noktasını Vm'lerinde.</span><span class="sxs-lookup"><span data-stu-id="9e42a-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="9e42a-150">bir araştırma kural toocheck hello sistem durumu adlı bir sayfada *HealthProbe.aspx* veya bir hizmet bağlantı noktası 8080</span><span class="sxs-lookup"><span data-stu-id="9e42a-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="9e42a-151">Bu nesneler kullanan bir yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="9e42a-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="9e42a-152">Merhaba NAT kuralları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="9e42a-153">Durum araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-153">Create a health probe.</span></span> <span data-ttu-id="9e42a-154">Bir araştırma iki yolu tooconfigure vardır:</span><span class="sxs-lookup"><span data-stu-id="9e42a-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="9e42a-155">HTTP araştırma</span><span class="sxs-lookup"><span data-stu-id="9e42a-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="9e42a-156">veya TCP araştırması</span><span class="sxs-lookup"><span data-stu-id="9e42a-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="9e42a-157">Bu örnekte, biz TCP yoklamaları toouse hello adımıdır.</span><span class="sxs-lookup"><span data-stu-id="9e42a-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="9e42a-158">Yük dengeleyici kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="9e42a-159">Daha önce oluşturduğunuz hello nesneleri kullanarak hello yük dengeleyicisi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="9e42a-160">NIC hello için arka uç VM'ler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="9e42a-161">Sanal ağ Hello almak ve sanal ağ alt, oluşturulan toobe hello NIC'ler gereken yeri.</span><span class="sxs-lookup"><span data-stu-id="9e42a-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="9e42a-162">IP yapılandırmaları ve NIC hello VM'ler için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e42a-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="9e42a-163">Sanal makineler oluşturun ve yeni oluşturulan NIC'ler hello atayın</span><span class="sxs-lookup"><span data-stu-id="9e42a-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="9e42a-164">Bir VM oluşturma hakkında daha fazla bilgi için bkz: [oluşturma ve Resource Manager ve Azure PowerShell ile Windows sanal makine önceden yapılandırın](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="9e42a-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="9e42a-165">Bir kullanılabilirlik kümesi ve depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e42a-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="9e42a-166">Her bir VM oluşturun ve hello önceki oluşturulan NIC'ler atayın</span><span class="sxs-lookup"><span data-stu-id="9e42a-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="9e42a-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e42a-167">Next steps</span></span>

[<span data-ttu-id="9e42a-168">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="9e42a-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="9e42a-169">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e42a-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9e42a-170">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e42a-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
