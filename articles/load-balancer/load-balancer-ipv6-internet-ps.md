---
title: "IPv6 - PowerShell ile bir Azure Internet'e yönelik Yük Dengeleyici oluşturma | Microsoft Docs"
description: "Internet'e yönelik Yük Dengeleyici kaynak yöneticisi için PowerShell kullanarak IPv6 oluşturmayı öğrenin"
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
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="c9229-104">Internet'e yönelik Yük Dengeleyici kaynak yöneticisi için PowerShell kullanarak IPv6 oluşturmaya başlamak</span><span class="sxs-lookup"><span data-stu-id="c9229-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9229-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9229-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="c9229-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c9229-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="c9229-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="c9229-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="c9229-108">Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="c9229-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="c9229-109">Yük dengeleyici, gelen trafiği bulut hizmetlerindeki sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9229-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="c9229-110">Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="c9229-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="c9229-111">Örnek dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="c9229-111">Example deployment scenario</span></span>

<span data-ttu-id="c9229-112">Aşağıdaki diyagram, bu makaledeki dağıtılan çözümü dengelemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c9229-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![Yük dengeleyici senaryosu](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="c9229-114">Bu senaryoda aşağıdaki Azure kaynakları oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="c9229-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="c9229-115">bir IPv4 ve IPv6 genel IP adresi olan bir Internet'e yönelik Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="c9229-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="c9229-116">iki Yük Dengeleme kuralları özel uç noktaları için ortak VIP'ler eşlemek için</span><span class="sxs-lookup"><span data-stu-id="c9229-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="c9229-117">bir kullanılabilirlik kümesi, iki VM içerir</span><span class="sxs-lookup"><span data-stu-id="c9229-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="c9229-118">iki sanal makine (VM)</span><span class="sxs-lookup"><span data-stu-id="c9229-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="c9229-119">atanan IPv4 ve IPv6 adreslerinin her VM için bir sanal ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="c9229-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="c9229-120">Azure PowerShell kullanarak çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="c9229-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="c9229-121">Aşağıdaki adımlar, Internet'e yönelik Yük Dengeleyici PowerShell ile Azure Resource Manager kullanarak nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c9229-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="c9229-122">Azure Resource Manager ile her bir kaynak oluşturulur ve birlikte bir kaynak oluşturmak için ENTER koy ayrı ayrı yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c9229-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="c9229-123">Bir yük dengeleyici dağıtmayı oluşturun ve aşağıdaki nesneleri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="c9229-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="c9229-124">Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c9229-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="c9229-125">Arka uç adres havuzu: Sanal makinelerin yük dengeleyiciden ağ trafiği alması için ağ arabirimlerini (NIC’ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="c9229-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="c9229-126">Yük dengeleme kuralları: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki bağlantı noktasına eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="c9229-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="c9229-127">Gelen NAT kuralları: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki belirli bir sanal makineye ait bağlantı noktasına eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="c9229-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="c9229-128">Araştırmalar: Arka uç adres havuzundaki sanal makine örneklerinin kullanılabilirliğini kontrol etmek için kullanılan durum araştırmalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="c9229-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="c9229-129">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c9229-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="c9229-130">PowerShell’i Resource Manager’ı kullanacak şekilde ayarlama</span><span class="sxs-lookup"><span data-stu-id="c9229-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="c9229-131">PowerShell için Azure Resource Manager modülüyle en son ürün sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c9229-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="c9229-132">Oturum Azure açın</span><span class="sxs-lookup"><span data-stu-id="c9229-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="c9229-133">İstendiğinde kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="c9229-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="c9229-134">Hesapla ilişkili abonelikleri kontrol etme</span><span class="sxs-lookup"><span data-stu-id="c9229-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="c9229-135">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="c9229-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="c9229-136">Bir kaynak grubu (var olan bir kaynak grubu kullanıyorsanız bu adımı atla) oluşturun</span><span class="sxs-lookup"><span data-stu-id="c9229-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="c9229-137">Ön uç IP havuzu için sanal ağ ve genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9229-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="c9229-138">Bir sanal ağ alt ağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="c9229-139">Azure genel IP adresi (PIP) kaynakları için ön uç IP adresi havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="c9229-140">Yük Dengeleyici genel IP etki alanı etiketini FQDN'sini için önek olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="c9229-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="c9229-141">Bu örnekte, FQDN'ler olan *lbnrpipv4.westus.cloudapp.azure.com* ve *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="c9229-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="c9229-142">Bir ön uç IP yapılandırmaları ve arka uç adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9229-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="c9229-143">Oluşturduğunuz ortak IP adresleri kullanan ön uç adresi yapılandırmasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="c9229-144">Arka uç adres havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="c9229-145">LB kuralları, NAT kuralları, bir araştırma ve bir yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9229-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="c9229-146">Bu örnek aşağıdaki nesneleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c9229-146">This example creates the following items:</span></span>

* <span data-ttu-id="c9229-147">bağlantı noktası 443 numaralı bağlantı noktasına 4443 tüm gelen trafiği çevirmek için NAT kuralı</span><span class="sxs-lookup"><span data-stu-id="c9229-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="c9229-148">80 numaralı bağlantı noktasına gelen tüm trafiği arka uç havuzundaki adreslerin 80 numaralı bağlantı noktasıyla dengeleyen yük dengeleyici kuralı.</span><span class="sxs-lookup"><span data-stu-id="c9229-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="c9229-149">bağlantı noktası 3389 sanal makinelerin RDP bağlantılarına izin vermek için bir yük dengeleyici kuralı.</span><span class="sxs-lookup"><span data-stu-id="c9229-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="c9229-150">adlı bir sayfada sistem durumunu denetlemek için bir araştırma kuralı *HealthProbe.aspx* veya bir hizmet bağlantı noktası 8080</span><span class="sxs-lookup"><span data-stu-id="c9229-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="c9229-151">Bu nesneler kullanan bir yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="c9229-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="c9229-152">NAT kurallarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="c9229-153">Durum araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-153">Create a health probe.</span></span> <span data-ttu-id="c9229-154">Araştırmaları iki şekilde yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c9229-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="c9229-155">HTTP araştırma</span><span class="sxs-lookup"><span data-stu-id="c9229-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="c9229-156">veya TCP araştırması</span><span class="sxs-lookup"><span data-stu-id="c9229-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="c9229-157">Bu örnekte, biz TCP araştırmalar kullanacaksanız.</span><span class="sxs-lookup"><span data-stu-id="c9229-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="c9229-158">Yük dengeleyici kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="c9229-159">Yük Dengeleyici daha önce oluşturulan nesneleri kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="c9229-160">Arka uç VM'ler için NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="c9229-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="c9229-161">Sanal ağ ve sanal ağ alt, burada NIC'ler oluşturulması gerektiğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c9229-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="c9229-162">IP yapılandırmaları ve NIC'ler, VM'ler için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9229-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="c9229-163">Sanal makineler oluşturun ve yeni oluşturulan NIC'ler atayın</span><span class="sxs-lookup"><span data-stu-id="c9229-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="c9229-164">Bir VM oluşturma hakkında daha fazla bilgi için bkz: [oluşturma ve Resource Manager ve Azure PowerShell ile Windows sanal makine önceden yapılandırın](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c9229-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="c9229-165">Bir kullanılabilirlik kümesi ve depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c9229-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="c9229-166">Her bir VM oluşturun ve önceki NIC'ler oluşturulan atayın</span><span class="sxs-lookup"><span data-stu-id="c9229-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

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

## <a name="next-steps"></a><span data-ttu-id="c9229-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9229-167">Next steps</span></span>

[<span data-ttu-id="c9229-168">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="c9229-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="c9229-169">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c9229-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c9229-170">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c9229-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
