---
title: "aaaCreate bir Azure Internet'e yönelik Yük Dengeleyici - PowerShell | Microsoft Docs"
description: "Nasıl toocreate bir Internet'e yönelik Yük Dengeleyici Kaynak Yöneticisi'nde PowerShell kullanarak bilgi edinin"
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
ms.openlocfilehash: e4e0e5271bc83c23fc62c0910e784c57d2b30065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="6c2fb-103"><a name="get-started"></a>PowerShell kullanarak Resource Manager’da İnternet’e yönelik yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-103"><a name="get-started"></a>Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c2fb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6c2fb-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="6c2fb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c2fb-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="6c2fb-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6c2fb-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="6c2fb-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="6c2fb-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="6c2fb-108">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="6c2fb-109">Ayrıca [nasıl toocreate bir Internet'e yönelik Yük Dengeleyici hello Klasik dağıtım modelini kullanarak bilgi](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6c2fb-109">You can also [learn how toocreate an Internet-facing load balancer by using hello classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-by-using-azure-powershell"></a><span data-ttu-id="6c2fb-110">Azure PowerShell kullanarak Hello çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-110">Deploying hello solution by using Azure PowerShell</span></span>

<span data-ttu-id="6c2fb-111">yordamları izleyerek hello nasıl toocreate bir Internet'e yönelik Yük Dengeleyici PowerShell ile Azure Kaynak Yöneticisi'ni kullanarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-111">hello following procedures explain how toocreate an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="6c2fb-112">Azure Resource Manager ile her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır ve toocreate bir yük dengeleyici bir araya getirin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a load balancer.</span></span>

<span data-ttu-id="6c2fb-113">Oluşturma ve nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c2fb-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="6c2fb-114">Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP (PIP) adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="6c2fb-115">Arka uç adres havuzu: hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-115">Back-end address pool: contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="6c2fb-116">Yük Dengeleme kuralları: hello arka uç adres havuzu hello yük dengeleyici tooa bağlantı noktası üzerinde genel bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-116">Load-balancing rules: contains rules that map a public port on hello load balancer tooa port in hello back-end address pool.</span></span>
* <span data-ttu-id="6c2fb-117">Gelen NAT kuralları: bağlantı noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-117">Inbound NAT rules: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="6c2fb-118">Sonda: sistem durumu kullanılan araştırmalar toocheck hello arka uç adres havuzu sanal makine örneklerinin kullanılabilirliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-118">Probes: contains health probes used toocheck availability of virtual machine instances in hello back-end address pool.</span></span>

<span data-ttu-id="6c2fb-119">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6c2fb-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="6c2fb-120">Resource Manager PowerShell toouse ayarlayın</span><span class="sxs-lookup"><span data-stu-id="6c2fb-120">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="6c2fb-121">Merhaba son üretim hello Azure Resource Manager modülü sürümü için PowerShell bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="6c2fb-121">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="6c2fb-122">TooAzure oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-122">Sign in tooAzure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="6c2fb-123">İstendiğinde kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="6c2fb-124">Merhaba hesabının Hello abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-124">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="6c2fb-125">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-125">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="6c2fb-126">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-126">Create a resource group.</span></span> <span data-ttu-id="6c2fb-127">(Mevcut bir kaynak grubunu kullanıyorsanız bu adımı atlayın.)</span><span class="sxs-lookup"><span data-stu-id="6c2fb-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="6c2fb-128">Bir sanal ağ ve hello ön uç IP havuzu için bir ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="6c2fb-128">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="6c2fb-129">Alt ağ ve sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="6c2fb-130">Adlı bir Azure ortak IP adresi kaynağı oluşturma **Publicıp**, hello DNS adına sahip bir ön uç IP havuzu tarafından kullanılan toobe **loadbalancernrp.westus.cloudapp.azure.com**. komutu aşağıdaki hello hello kullanır statik ayırma türü.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-130">Create an Azure public IP address resource, named **PublicIP**, toobe used by a front-end IP pool with hello DNS name **loadbalancernrp.westus.cloudapp.azure.com**. hello following command uses hello static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="6c2fb-131">Merhaba yük dengeleyicisi hello etki alanı etiketi hello ortak IP FQDN'sini için önek olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-131">hello load balancer uses hello domain label of hello public IP as a prefix for its FQDN.</span></span> <span data-ttu-id="6c2fb-132">Bu yük dengeleyici FQDN hello gibi hello bulut hizmeti kullanan hello Klasik dağıtım modelinden, farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-132">This is different from hello classic deployment model, which uses hello cloud service as hello load balancer FQDN.</span></span>
   > <span data-ttu-id="6c2fb-133">Bu örnekte, hello FQDN'sidir **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-133">In this example, hello FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.</span></span>

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="6c2fb-134">Ön uç IP havuzu ve arka uç adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-134">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="6c2fb-135">Adlı bir ön uç IP havuzu oluşturma **LB ön uç** hello kullanan **Publicıp** kaynak.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-135">Create a front-end IP pool named **LB-Frontend** that uses hello **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="6c2fb-136">**LB-backend** adlı bir arka uç adres havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-136">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="6c2fb-137">NAT kuralları, yük dengeleyici kuralı, araştırma ve yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-137">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="6c2fb-138">Bu örnekte aşağıdaki öğelerindeki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="6c2fb-138">This example creates hello following items:</span></span>

* <span data-ttu-id="6c2fb-139">Tüm gelen trafiği üzerinde bağlantı noktası 3441 tooport 3389 NAT kuralı tootranslate</span><span class="sxs-lookup"><span data-stu-id="6c2fb-139">A NAT rule tootranslate all incoming traffic on port 3441 tooport 3389</span></span>
* <span data-ttu-id="6c2fb-140">Tüm gelen trafiği üzerinde bağlantı noktası 3442 tooport 3389 NAT kuralı tootranslate</span><span class="sxs-lookup"><span data-stu-id="6c2fb-140">A NAT rule tootranslate all incoming traffic on port 3442 tooport 3389</span></span>
* <span data-ttu-id="6c2fb-141">Bir araştırma kural toocheck hello sistem durumu adlı bir sayfada **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="6c2fb-141">A probe rule toocheck hello health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="6c2fb-142">Bir yük dengeleyici kuralı toobalance hello üzerinde bağlantı noktası 80 tooport 80 tüm gelen trafiği hello arka uç havuzundaki adresleri</span><span class="sxs-lookup"><span data-stu-id="6c2fb-142">A load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool</span></span>
* <span data-ttu-id="6c2fb-143">Tüm bu nesneleri kullanan yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="6c2fb-143">A load balancer that uses all these objects</span></span>

<span data-ttu-id="6c2fb-144">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="6c2fb-144">Use these steps:</span></span>

1. <span data-ttu-id="6c2fb-145">Merhaba NAT kuralları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-145">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="6c2fb-146">Durum araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-146">Create a health probe.</span></span> <span data-ttu-id="6c2fb-147">Bir araştırma iki yolu tooconfigure vardır:</span><span class="sxs-lookup"><span data-stu-id="6c2fb-147">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="6c2fb-148">HTTP araştırma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-148">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="6c2fb-149">TCP araştırma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-149">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="6c2fb-150">Yük dengeleyici kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-150">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="6c2fb-151">Merhaba yük dengeleyici hello daha önce oluşturduğunuz nesneleri kullanarak oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-151">Create hello load balancer by using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="6c2fb-152">NIC’leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-152">Create NICs</span></span>

<span data-ttu-id="6c2fb-153">Ağ arabirimleri oluşturun (veya var olanları değiştirme) ve ardından bunları tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirin:</span><span class="sxs-lookup"><span data-stu-id="6c2fb-153">Create network interfaces (or modify existing ones) and then associate them tooNAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="6c2fb-154">Merhaba sanal ağ ve bir sanal ağ alt hello NIC'ler oluşturulan toobe gereken yeri alın.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-154">Get hello virtual network and a virtual network subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="6c2fb-155">Adlı bir NIC oluşturun **lb nıc1 olması**ve hello ilk NAT kuralında ve hello ilk (ve yalnızca) arka uç adres havuzu ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-155">Create a NIC named **lb-nic1-be**, and associate it with hello first NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="6c2fb-156">Adlı bir NIC oluşturun **lb nic2 olması**ve hello ikinci NAT kuralı ve hello ilk (ve yalnızca) arka uç adres havuzu ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-156">Create a NIC named **lb-nic2-be**, and associate it with hello second NAT rule and hello first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="6c2fb-157">Merhaba NIC'ler denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-157">Check hello NICs.</span></span>

        $backendnic1

    <span data-ttu-id="6c2fb-158">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="6c2fb-158">Expected output:</span></span>

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

5. <span data-ttu-id="6c2fb-159">Kullanım hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NIC'ler toodifferent VM'ler.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-159">Use hello `Add-AzureRmVMNetworkInterface` cmdlet tooassign hello NICs toodifferent VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="6c2fb-160">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-160">Create a virtual machine</span></span>

<span data-ttu-id="6c2fb-161">Sanal makine oluşturma ve NIC atama talimatları için bkz. [PowerShell kullanarak Azure VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c2fb-161">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface-toohello-load-balancer"></a><span data-ttu-id="6c2fb-162">Merhaba ağ arabirimi toohello yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="6c2fb-162">Add hello network interface toohello load balancer</span></span>

1. <span data-ttu-id="6c2fb-163">Merhaba yük dengeleyici Azure'dan alın.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-163">Retrieve hello load balancer from Azure.</span></span>

    <span data-ttu-id="6c2fb-164">(Bunu, henüz yapmadıysanız) hello yük dengeleyici kaynak bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-164">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="6c2fb-165">Merhaba değişkeni çağrılır **$lb**. Merhaba aynı daha önce oluşturduğunuz hello yük dengeleyici kaynaktan adları kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-165">hello variable is called **$lb**. Use hello same names from hello load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="6c2fb-166">Yük hello arka uç yapılandırması tooa değişkeni.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-166">Load hello back-end configuration tooa variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="6c2fb-167">Önceden oluşturulmuş hello ağ arabirimi bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-167">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="6c2fb-168">Merhaba değişken adı **$nic**.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-168">hello variable name is **$nic**.</span></span> <span data-ttu-id="6c2fb-169">Merhaba ağ arabirimi adı olduğu hello aynı hello önceki örnek.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-169">hello network interface name is hello same one from hello earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="6c2fb-170">Merhaba arka uç yapılandırması hello ağ arabiriminde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-170">Change hello back-end configuration on hello network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="6c2fb-171">Merhaba ağ arabirimi nesnesi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-171">Save hello network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="6c2fb-172">Bir ağ arabirimi toohello yük dengeleyici arka uç havuzuna eklendikten sonra ağ trafiğini hello Yük Dengeleme kuralları bu yük dengeleyici kaynak için temel almayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-172">After a network interface is added toohello load balancer back-end pool, it starts receiving network traffic based on hello load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="6c2fb-173">Mevcut yük dengeleyiciyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="6c2fb-173">Update an existing load balancer</span></span>

1. <span data-ttu-id="6c2fb-174">Yük Dengeleyici gelen Hello kullanarak hello önceki örnekte, bir yük dengeleyici nesne toohello değişkeni Ata **$slb** kullanarak `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-174">By using hello load balancer from hello earlier example, assign a load balancer object toohello variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="6c2fb-175">Aşağıdaki örnek hello, bağlantı noktası 81 hello ön uç havuzunda ve bağlantı noktası 8181 hello arka uç havuzu--tooan varolan yük dengeleyicisi kullanarak gelen NAT kuralı--ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-175">In hello following example, you add an inbound NAT rule--by using port 81 in hello front-end pool and port 8181 for hello back-end pool--tooan existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="6c2fb-176">Kullanarak Hello yeni yapılandırmayı kaydedin `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-176">Save hello new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="6c2fb-177">Yük dengeleyici kaldırma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-177">Remove a load balancer</span></span>

<span data-ttu-id="6c2fb-178">Hello komutunu `Remove-AzureLoadBalancer` toodelete adlı önceden oluşturulmuş yük dengeleyici **NRP LB** bir kaynak grubunda **NRP RG**.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-178">Use hello command `Remove-AzureLoadBalancer` toodelete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="6c2fb-179">Merhaba isteğe bağlı bir anahtar kullandığınız **-Force** tooavoid hello istemi silme işlemi için.</span><span class="sxs-lookup"><span data-stu-id="6c2fb-179">You can use hello optional switch **-Force** tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c2fb-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6c2fb-180">Next steps</span></span>

[<span data-ttu-id="6c2fb-181">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="6c2fb-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="6c2fb-182">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="6c2fb-183">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6c2fb-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
