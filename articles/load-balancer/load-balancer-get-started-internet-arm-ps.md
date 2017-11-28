---
title: "Azure İnternet’e yönelik yük dengeleyicisi oluşturma - PowerShell | Microsoft Docs"
description: "PowerShell kullanarak Resource Manager’da İnternet’e yönelik yük dengeleyici oluşturmayı öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: f610afbdfac7b5dd9a1a5eb6812c86d8ce0d63e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="b1ca9-103"><a name="get-started"></a>PowerShell kullanarak Resource Manager’da İnternet’e yönelik yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1ca9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b1ca9-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="b1ca9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1ca9-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="b1ca9-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b1ca9-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="b1ca9-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="b1ca9-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b1ca9-108">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="b1ca9-109">[Klasik dağıtım modelini kullanarak İnternet’e yönelik yük dengeleyici oluşturma](load-balancer-get-started-internet-classic-cli.md) sayfasını da inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-by-using-azure-powershell"></a><span data-ttu-id="b1ca9-110">Çözümü Azure PowerShell kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-110">Deploying the solution by using Azure PowerShell</span></span>

<span data-ttu-id="b1ca9-111">Aşağıdaki yordamlarda, Azure Resource Manager ve PowerShell kullanarak İnternet’e yönelik yük dengeleyici oluşturma işlemleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="b1ca9-112">Azure Resource Manager ile her bir kaynak ayrı ayrı oluşturulup yapılandırıldıktan sonra yük dengeleyici oluşturmak için bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span></span>

<span data-ttu-id="b1ca9-113">Yük dengeleyici dağıtmak için aşağıdaki nesneleri oluşturmanız ve yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b1ca9-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="b1ca9-114">Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP (PIP) adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="b1ca9-115">Arka uç adres havuzu: Sanal makinelerin yük dengeleyiciden ağ trafiği alması için ağ arabirimlerini (NIC’ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="b1ca9-116">Yük dengeleme kuralları: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki bağlantı noktasına eşleyen kuralları içerir.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="b1ca9-117">Gelen NAT kuralları: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki belirli bir sanal makineye ait bağlantı noktasına eşleyen kuralları içerir.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="b1ca9-118">Araştırmalar: Arka uç adres havuzundaki sanal makine örneklerinin kullanılabilirliğini kontrol etmek için kullanılan durum araştırmalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span></span>

<span data-ttu-id="b1ca9-119">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b1ca9-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="b1ca9-120">PowerShell’i Resource Manager’ı kullanacak şekilde ayarlama</span><span class="sxs-lookup"><span data-stu-id="b1ca9-120">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="b1ca9-121">PowerShell için Azure Resource Manager’ın en güncel üretim sürümüne sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="b1ca9-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="b1ca9-122">Azure'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-122">Sign in to Azure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="b1ca9-123">İstendiğinde kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="b1ca9-124">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-124">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="b1ca9-125">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-125">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="b1ca9-126">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-126">Create a resource group.</span></span> <span data-ttu-id="b1ca9-127">(Mevcut bir kaynak grubunu kullanıyorsanız bu adımı atlayın.)</span><span class="sxs-lookup"><span data-stu-id="b1ca9-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="b1ca9-128">Ön uç IP havuzu için sanal ağ ve genel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-128">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="b1ca9-129">Alt ağ ve sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="b1ca9-130">**loadbalancernrp.westus.cloudapp.azure.com** DNS adına sahip ön uç IP havuzu tarafından kullanılacak **PublicIP** adlı bir Azure genel IP adresi kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="b1ca9-131">Aşağıdaki komutta statik ayırma türü kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-131">The following command uses the static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="b1ca9-132">Yük dengeleyici, FQDN ön eki olarak genel IP’nin etki alanı etiketini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-132">The load balancer uses the domain label of the public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="b1ca9-133">Bu, yük dengeleyici FQDN değeri olarak bulut hizmeti kullanan klasik dağıtım modelinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-133">This is different from the classic deployment model, which uses the cloud service as the load balancer FQDN.</span></span>
   > <span data-ttu-id="b1ca9-134">Bu örnekte FQDN: **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-134">In this example, the FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="b1ca9-135">Ön uç IP havuzu ve arka uç adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-135">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="b1ca9-136">**PublicIp** kaynağını kullanan **LB-Frontend** adlı bir ön uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="b1ca9-137">**LB-backend** adlı bir arka uç adres havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-137">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="b1ca9-138">NAT kuralları, yük dengeleyici kuralı, araştırma ve yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="b1ca9-139">Bu örnek aşağıdaki nesneleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="b1ca9-139">This example creates the following items:</span></span>

* <span data-ttu-id="b1ca9-140">3441 numaralı bağlantı noktasına gelen tüm trafiği 3389 numaralı bağlantı noktasına yönlendiren NAT kuralı</span><span class="sxs-lookup"><span data-stu-id="b1ca9-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span></span>
* <span data-ttu-id="b1ca9-141">3442 numaralı bağlantı noktasına gelen tüm trafiği 3389 numaralı bağlantı noktasına yönlendiren NAT kuralı</span><span class="sxs-lookup"><span data-stu-id="b1ca9-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span></span>
* <span data-ttu-id="b1ca9-142">**HealthProbe.aspx** adlı sayfanın durumunu denetleyen araştırma kuralı</span><span class="sxs-lookup"><span data-stu-id="b1ca9-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="b1ca9-143">80 numaralı bağlantı noktasına gelen tüm trafiği arka uç havuzundaki adreslerin 80 numaralı bağlantı noktasıyla dengeleyen yük dengeleyici kuralı</span><span class="sxs-lookup"><span data-stu-id="b1ca9-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span></span>
* <span data-ttu-id="b1ca9-144">Tüm bu nesneleri kullanan yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="b1ca9-144">A load balancer that uses all these objects</span></span>

<span data-ttu-id="b1ca9-145">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="b1ca9-145">Use these steps:</span></span>

1. <span data-ttu-id="b1ca9-146">NAT kurallarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-146">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="b1ca9-147">Durum araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-147">Create a health probe.</span></span> <span data-ttu-id="b1ca9-148">Araştırmaları iki şekilde yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b1ca9-148">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="b1ca9-149">HTTP araştırma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-149">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="b1ca9-150">TCP araştırma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-150">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="b1ca9-151">Yük dengeleyici kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-151">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="b1ca9-152">Önceden oluşturulan nesneleri kullanarak yük dengeleyiciyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-152">Create the load balancer by using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="b1ca9-153">NIC’leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-153">Create NICs</span></span>

<span data-ttu-id="b1ca9-154">Ağ arabirimleri oluşturun (veya var olanları düzenleyin) ve bunları NAT kuralları, yük dengeleyici kuralları ve araştırmalarla ilişkilendirin:</span><span class="sxs-lookup"><span data-stu-id="b1ca9-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="b1ca9-155">NIC’lerin oluşturulacağı sanal ağı ve sanal ağ alt ağını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="b1ca9-156">**lb-nic1-be** adlı bir NIC oluşturup ilk NAT kuralı ve ilk (ve tek) arka uç adres havuzuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="b1ca9-157">**lb-nic2-be** adlı bir NIC oluşturup ikinci NAT kuralı ve ilk (ve tek) arka uç adres havuzuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="b1ca9-158">NIC’leri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-158">Check the NICs.</span></span>

        $backendnic1

    <span data-ttu-id="b1ca9-159">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="b1ca9-159">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="b1ca9-160">NIC’leri farklı VM’lere atamak için `Add-AzureRmVMNetworkInterface` cmdlet’ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="b1ca9-161">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-161">Create a virtual machine</span></span>

<span data-ttu-id="b1ca9-162">Sanal makine oluşturma ve NIC atama talimatları için bkz. [PowerShell kullanarak Azure VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1ca9-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface-to-the-load-balancer"></a><span data-ttu-id="b1ca9-163">Ağ arabirimini yük dengeleyiciye ekleme</span><span class="sxs-lookup"><span data-stu-id="b1ca9-163">Add the network interface to the load balancer</span></span>

1. <span data-ttu-id="b1ca9-164">Yük dengeleyiciyi Azure’dan alın.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-164">Retrieve the load balancer from Azure.</span></span>

    <span data-ttu-id="b1ca9-165">Yük dengeleyici kaynağını bir değişkene yükleyin (henüz yapmadıysanız).</span><span class="sxs-lookup"><span data-stu-id="b1ca9-165">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="b1ca9-166">Değişken adı: **$lb**. Daha önce oluşturduğunuz yük dengeleyici kaynağındaki adları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="b1ca9-167">Arka uç yapılandırmasını bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-167">Load the back-end configuration to a variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="b1ca9-168">Önceden oluşturulan ağ arabirimini bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-168">Load the already created network interface into a variable.</span></span> <span data-ttu-id="b1ca9-169">Değişken adı: **$nic**.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-169">The variable name is **$nic**.</span></span> <span data-ttu-id="b1ca9-170">Ağ arabirimi adı önceki örnekle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-170">The network interface name is the same one from the earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="b1ca9-171">Ağ arabiriminde arka uç yapılandırmasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-171">Change the back-end configuration on the network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="b1ca9-172">Ağ arabirimi nesnesini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-172">Save the network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="b1ca9-173">Yük dengeleyici arka uç havuzuna bir ağ arabirimi eklendikten sonra ilgili yük dengeleyici kaynağı için yük dengeleme kurallarına göre ağ trafiğini almaya başlar.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="b1ca9-174">Mevcut yük dengeleyiciyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="b1ca9-174">Update an existing load balancer</span></span>

1. <span data-ttu-id="b1ca9-175">Önceki örnekte verilen yük dengeleyiciyi kullanarak **$slb** değişkenine `Get-AzureLoadBalancer` aracılığıyla yük dengeleyici nesnesi atayın.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="b1ca9-176">Aşağıdaki örnekte mevcut bir yük dengeleyiciye ön uç için 81 numaralı bağlantı noktasını, arka uç havuzu için ise 8181 numaralı arka uç bağlantı noktasını kullanarak yeni bir Gelen NAT kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="b1ca9-177">`Set-AzureLoadBalancer` kullanarak yeni yapılandırmayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="b1ca9-178">Yük dengeleyici kaldırma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-178">Remove a load balancer</span></span>

<span data-ttu-id="b1ca9-179">**NRP-RG** adlı kaynak grubunda yer alan **NRP-LB** adlı önceden oluşturulmuş yük dengeleyiciyi silmek için `Remove-AzureLoadBalancer` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="b1ca9-180">Silme istemini atlamak için isteğe bağlı **-Force** anahtarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b1ca9-180">You can use the optional switch **-Force** to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1ca9-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b1ca9-181">Next steps</span></span>

[<span data-ttu-id="b1ca9-182">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="b1ca9-182">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="b1ca9-183">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-183">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="b1ca9-184">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b1ca9-184">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
