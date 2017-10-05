---
title: "Azur İç yük dengeleyicisi oluşturma - PowerShell | Microsoft Docs"
description: "Resource Manager’da PowerShell kullanarak iç yük dengeleyici oluşturmayı öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c6c98981-df9d-4dd7-a94b-cc7d1dc99369
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7bd31ab8f52ec5e81f6966000554be46eaa59396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="faa18-103">PowerShell kullanarak iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="faa18-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="faa18-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="faa18-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="faa18-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="faa18-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="faa18-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="faa18-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="faa18-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="faa18-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="faa18-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="faa18-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="faa18-109">Bu makale, Microsoft’un çoğu yeni dağıtım için [klasik dağıtım modeli](load-balancer-get-started-ilb-classic-ps.md) yerine önerdiği Resource Manager dağıtım modelini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="faa18-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="faa18-110">Aşağıdaki adımlarda, Azure Resource Manager ve PowerShell kullanarak iç yük dengeleyici oluşturma işlemleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="faa18-110">The following steps explain how to create an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="faa18-111">Azure Resource Manager ile iç yük dengeleyici oluşturmak için gerekli olan adımları ayrı ayrı tamamlamanız, ardından bunları birleştirerek yük dengeleyici oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="faa18-111">With Azure Resource Manager, the items to create a Internal load balancer are configured individually and then combined to create a load balancer.</span></span>

<span data-ttu-id="faa18-112">Yük dengeleyici dağıtmak için aşağıdaki nesneleri oluşturmanız ve yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="faa18-112">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="faa18-113">Ön uç IP yapılandırması: Gelen ağ trafiği için özel IP adresinin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="faa18-113">Front end IP configuration - will configure the private IP address for incoming network traffic</span></span>
* <span data-ttu-id="faa18-114">Arka uç adres havuzu: Ön uç IP havuzundan gelen yük dengeli trafiği alacak ağ arabirimlerinin yapılandırılması</span><span class="sxs-lookup"><span data-stu-id="faa18-114">Backend address pool - will configure the network interfaces which will receive the load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="faa18-115">Yük dengeleme kuralları: Yük dengeleyici için kaynak ve yerel bağlantı noktası yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="faa18-115">Load balancing rules - source and local port configuration for the load balancer.</span></span>
* <span data-ttu-id="faa18-116">Araştırmalar: Sanal Makine örnekleri için durum araştırması yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="faa18-116">Probes - configures the health status probe for the Virtual Machine instances.</span></span>
* <span data-ttu-id="faa18-117">Gelen NAT kuralları: Sanal Makine örneklerinden birine doğrudan erişmek için bağlantı noktası kurallarının yapılandırılması.</span><span class="sxs-lookup"><span data-stu-id="faa18-117">Inbound NAT rules - configures the port rules to directly access one of the Virtual Machine instances.</span></span>

<span data-ttu-id="faa18-118">Azure Resource Manager içindeki yük dengeleyici bileşenleri hakkında daha fazla bilgi için bkz. [Azure Resource Manager yük dengeleyici desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="faa18-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="faa18-119">Aşağıdaki adımlarda iki sanal makine arasında yük dengeleyici yapılandırma işlemleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="faa18-119">The following steps explain how to configure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-to-use-resource-manager"></a><span data-ttu-id="faa18-120">PowerShell’i Resource Manager’ı kullanacak şekilde ayarlama</span><span class="sxs-lookup"><span data-stu-id="faa18-120">Setup PowerShell to use Resource Manager</span></span>

<span data-ttu-id="faa18-121">PowerShell Azure modülünün son üretim sürümüne sahip olduğunuzdan ve PowerShell ayarlarının Azure aboneliğinize doğrudan erişecek şekilde yapıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="faa18-121">Make sure you have the latest production version of the Azure module for PowerShell, and have PowerShell setup correctly to access your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="faa18-122">1. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="faa18-123">2. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-123">Step 2</span></span>

<span data-ttu-id="faa18-124">Hesapla ilişkili abonelikleri kontrol etme</span><span class="sxs-lookup"><span data-stu-id="faa18-124">Check the subscriptions for the account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="faa18-125">Kimlik bilgilerinizle kimliğinizi doğrulamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="faa18-125">You will be prompted to Authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="faa18-126">3. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-126">Step 3</span></span>

<span data-ttu-id="faa18-127">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="faa18-127">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="faa18-128">Yük dengeleyici için Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="faa18-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="faa18-129">Yeni bir kaynak grubu oluşturma (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın)</span><span class="sxs-lookup"><span data-stu-id="faa18-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="faa18-130">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="faa18-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="faa18-131">Bu, kaynak grubunda kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="faa18-131">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="faa18-132">Tüm yük dengeleyici oluşturma komutlarının aynı kaynak grubunu kullanacağından emin olun.</span><span class="sxs-lookup"><span data-stu-id="faa18-132">Make sure all commands to create a load balancer will use the same resource group.</span></span>

<span data-ttu-id="faa18-133">Yukarıdaki örnekte, "NRP-RG" adlı "Batı ABD" konumlu bir kaynak grubu oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="faa18-133">In the example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="faa18-134">Ön uç IP havuzu için Sanal Ağ ve özel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="faa18-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="faa18-135">Sanal ağ için bir alt ağ oluşturur ve $backendSubnet değişkenine atar</span><span class="sxs-lookup"><span data-stu-id="faa18-135">Creates a subnet for the virtual network and assigns to variable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="faa18-136">Sanal ağ oluşturma:</span><span class="sxs-lookup"><span data-stu-id="faa18-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="faa18-137">Sanal ağı oluşturur ve lb-subnet-be alt ağını NRPVNet sanal ağına ekler ve $vnet değişkenine atar</span><span class="sxs-lookup"><span data-stu-id="faa18-137">Creates the virtual network and adds the subnet lb-subnet-be to the virtual network NRPVNet and assigns to variable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="faa18-138">Ön uç IP havuzu ve arka uç adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="faa18-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="faa18-139">Gelen yük dengeleyici ağı trafiği için ön uç IP havuzu ve yük dengeli trafiği almak için arka uç adres havuzu kurma.</span><span class="sxs-lookup"><span data-stu-id="faa18-139">Setting up a front end IP pool for the incoming load balancer network traffic and backend address pool to receive the load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="faa18-140">1. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-140">Step 1</span></span>

<span data-ttu-id="faa18-141">Gelen ağ trafiği uç noktası olacak 10.0.2.0/24 alt ağı için 10.0.2.5 özel IP adresini kullanan ön uç IP havuzu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="faa18-141">Create a front end IP pool using the private IP address 10.0.2.5 for the subnet 10.0.2.0/24 which will be the incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="faa18-142">2. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-142">Step 2</span></span>

<span data-ttu-id="faa18-143">Ön uç IP havuzundan gelen trafiği almak için kullanılacak arka uç adres havuzu kurma:</span><span class="sxs-lookup"><span data-stu-id="faa18-143">Set up a back end address pool used to receive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="faa18-144">LB kuralları, NAT kuralları, araştırma ve yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="faa18-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="faa18-145">Ön uç IP havuzunu ve arka uç adres havuzunu oluşturduktan sonra yük dengeleyici kaynağına ait olacak kuralları oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="faa18-145">After creating the front end IP pool and the backend address pool, you will need to create the rules which will belong to the load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="faa18-146">1. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="faa18-147">Yukarıdaki örnek aşağıdaki öğeleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="faa18-147">The example above is creating the following items:</span></span>

* <span data-ttu-id="faa18-148">3441 numaralı bağlantı noktasına gelen tüm trafiği 3389 numaralı bağlantı noktasına yönlendirecek NAT kuralı.</span><span class="sxs-lookup"><span data-stu-id="faa18-148">NAT rule which all incoming traffic to port 3441 will go to port 3389.</span></span>
* <span data-ttu-id="faa18-149">3442 numaralı bağlantı noktasına gelen tüm trafiği 3389 numaralı bağlantı noktasına yönlendirecek ikinci NAT kuralı.</span><span class="sxs-lookup"><span data-stu-id="faa18-149">a second NAT rule which all incoming traffic to port 3442 will go to port 3389.</span></span>
* <span data-ttu-id="faa18-150">80 numaralı genel bağlantı noktasına gelen tüm trafik için arka uç adres havuzundaki 80 numaralı yerel bağlantı noktasında yük dengeleme gerçekleştirecek yük dengeleyici kuralı.</span><span class="sxs-lookup"><span data-stu-id="faa18-150">a load balancer rule which will load balance all incoming traffic on public port 80 to local port 80 in the back end address pool.</span></span>
* <span data-ttu-id="faa18-151">"HealthProbe.aspx" yolu için sistem durumunu kontrol edecek bir araştırma kuralı</span><span class="sxs-lookup"><span data-stu-id="faa18-151">a probe rule which will check the health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="faa18-152">2. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-152">Step 2</span></span>

<span data-ttu-id="faa18-153">Tüm nesneleri (NAT kuralları, Yük dengeleyici kuralları, araştırma yapılandırmaları) ekleyerek yük dengeleyiciyi oluşturma:</span><span class="sxs-lookup"><span data-stu-id="faa18-153">Create the load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="faa18-154">Ağ arabirimlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="faa18-154">Create network interfaces</span></span>

<span data-ttu-id="faa18-155">İç yük dengeleyiciyi oluşturduktan sonra gelen yük dengeli ağ trafiğini alacak olan ağ arabirimlerini, NAT kurallarını ve araştırmayı tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="faa18-155">After creating the internal load balancer, you need define which network interfaces will be receiving the incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="faa18-156">Bu durumda ağ arabirimi ayrı olarak yapılandırılabilir ve daha sonra bir sanal makineye atanabilir.</span><span class="sxs-lookup"><span data-stu-id="faa18-156">The network interface in this case is configured individually and can be assigned to a virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="faa18-157">1. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-157">Step 1</span></span>

<span data-ttu-id="faa18-158">Ağ arabirimlerini oluşturmak için kaynak sanal ağını ve alt ağını edinme:</span><span class="sxs-lookup"><span data-stu-id="faa18-158">Get the resource virtual network and subnet to create network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="faa18-159">Bu adımda yük dengeleyici arka uç havuzuna ait olacak ağ birimi oluşturulur ve bu ağ arabirimi için ilk RDP NAT kuralıyla ilişkilendirilir:</span><span class="sxs-lookup"><span data-stu-id="faa18-159">This step creates a network interface which will belong to the load balancer back end pool and associate the first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="faa18-160">2. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-160">Step 2</span></span>

<span data-ttu-id="faa18-161">LB-Nic2-BE adında ikinci bir ağ arabirimi oluşturma:</span><span class="sxs-lookup"><span data-stu-id="faa18-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="faa18-162">Bu adımda ikinci bir ağ arabirimi oluşturulur, aynı yük dengeleyici arka uç havuzuna atanır ve RDP için oluşturulan ikinci NAT kuralıyla ilişkilendirilir:</span><span class="sxs-lookup"><span data-stu-id="faa18-162">This step creates a second network interface, assigning to the same load balancer back end pool and associating the second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="faa18-163">Sonuç şunu verecektir:</span><span class="sxs-lookup"><span data-stu-id="faa18-163">The end result will show the following:</span></span>

    $backendnic1

<span data-ttu-id="faa18-164">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="faa18-164">Expected output:</span></span>

    Name                 : lb-nic1-be
    ResourceGroupName    : NRP-RG
    Location             : westus
    Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
    Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
    ProvisioningState    : Succeeded
    Tags                 :
    VirtualMachine       : null
    IpConfigurations     : [
                         {
                           "PrivateIpAddress": "10.0.2.6",
                           "PrivateIpAllocationMethod": "Static",
                           "Subnet": {
                             "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                           },
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
                           "ProvisioningState": "Succeeded",
                           "Name": "ipconfig1",
                           "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                           "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1"
                         }
                       ]
    DnsSettings          : {
                         "DnsServers": [],
                         "AppliedDnsServers": []
                       }
    AppliedDnsSettings   :
    NetworkSecurityGroup : null
    Primary              : False



### <a name="step-3"></a><span data-ttu-id="faa18-165">3. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-165">Step 3</span></span>

<span data-ttu-id="faa18-166">NIC’i bir sanal makineye atamak için Add-AzureRmVMNetworkInterface komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="faa18-166">Use the command Add-AzureRmVMNetworkInterface to assign the NIC to a virtual Machine.</span></span>

<span data-ttu-id="faa18-167">Sanal makine oluşturma ve bir NIC’e atama ile ilgili adım adım talimatları şu belgede bulabilirsiniz: [PowerShell kullanarak Azure VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="faa18-167">You can find the step by step instructions to create a virtual machine and assign to a NIC following the documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface"></a><span data-ttu-id="faa18-168">Ağ arabirimini ekleme</span><span class="sxs-lookup"><span data-stu-id="faa18-168">Add the network interface</span></span>

<span data-ttu-id="faa18-169">Önceden oluşturulan bir sanal makineniz varsa aşağıdaki adımları uygulayarak ağ arabirimini etkileyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="faa18-169">If you already have a virtual machine created, you can add the network interface with the following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="faa18-170">1. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-170">Step 1</span></span>

<span data-ttu-id="faa18-171">Yük dengeleyici kaynağını bir değişkene yükleyin (henüz yapmadıysanız).</span><span class="sxs-lookup"><span data-stu-id="faa18-171">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="faa18-172">Kullanılan değişken $lb olarak adlandırılır ve yukarıda oluşturulan yük dengeleyici kaynağıyla aynı adları kullanır.</span><span class="sxs-lookup"><span data-stu-id="faa18-172">The variable used is called $lb and use the same names from the load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="faa18-173">2. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-173">Step 2</span></span>

<span data-ttu-id="faa18-174">Arka uç yapılandırmasını bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="faa18-174">Load the backend configuration to a variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="faa18-175">3. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-175">Step 3</span></span>

<span data-ttu-id="faa18-176">Önceden oluşturulan ağ arabirimini bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="faa18-176">Load the already created network interface into a variable.</span></span> <span data-ttu-id="faa18-177">$nic değişken adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="faa18-177">the variable name used is $nic.</span></span> <span data-ttu-id="faa18-178">Kullanılan ağ arabirimi adı yukarıdaki örnekle aynıdır.</span><span class="sxs-lookup"><span data-stu-id="faa18-178">The network interface name used is the same from the example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="faa18-179">4. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-179">Step 4</span></span>

<span data-ttu-id="faa18-180">Ağ arabiriminde arka uç yapılandırmasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="faa18-180">Change the backend configuration on the network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="faa18-181">5. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-181">Step 5</span></span>

<span data-ttu-id="faa18-182">Ağ arabirimi nesnesini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="faa18-182">Save the network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="faa18-183">Yük dengeleyici arka uç havuzuna bir ağ arabirimi eklendikten sonra ilgili yük dengeleyici kaynağı için yük dengeleme kurallarına göre ağ trafiğini almaya başlar.</span><span class="sxs-lookup"><span data-stu-id="faa18-183">After a network interface is added to the load balancer backend pool, it starts receiving network traffic based on the load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="faa18-184">Mevcut yük dengeleyiciyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="faa18-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="faa18-185">1. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-185">Step 1</span></span>
<span data-ttu-id="faa18-186">Yukarıdaki örnekte verilen yük dengeleyiciyi kullanarak yük dengeleyici nesnesini $slb değişkenine Get-AzureRmLoadBalancer ile atayın</span><span class="sxs-lookup"><span data-stu-id="faa18-186">Using the load balancer from the example above, assign load balancer object to variable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="faa18-187">2. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-187">Step 2</span></span>

<span data-ttu-id="faa18-188">Aşağıdaki örnekte mevcut bir yük dengeleyiciye ön uç için 81 numaralı bağlantı noktasını, arka uç havuzu için ise 8181 numaralı arka uç bağlantı noktasını kullanarak yeni bir Gelen NAT kuralı ekleyeceksiniz</span><span class="sxs-lookup"><span data-stu-id="faa18-188">In the following example, you will add a new Inbound NAT rule using port 81 in the front end and port 8181 for the back end pool to an existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="faa18-189">3. Adım</span><span class="sxs-lookup"><span data-stu-id="faa18-189">Step 3</span></span>

<span data-ttu-id="faa18-190">Yeni yapılandırmayı Set-AzureLoadBalancer kullanarak kaydedin</span><span class="sxs-lookup"><span data-stu-id="faa18-190">Save the new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="faa18-191">Yük dengeleyici kaldırma</span><span class="sxs-lookup"><span data-stu-id="faa18-191">Remove a load balancer</span></span>

<span data-ttu-id="faa18-192">“NRP-RG” adlı kaynak grubunda yer alan “NRP-LB” adlı önceden oluşturulmuş yük dengeleyiciyi silmek için Remove-AzureRmLoadBalancer komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="faa18-192">Use the command Remove-AzureRmLoadBalancer to delete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="faa18-193">Silme istemini atlamak için isteğe bağlı -Force anahtarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faa18-193">You can use the optional switch -Force to avoid the prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="faa18-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="faa18-194">Next steps</span></span>

[<span data-ttu-id="faa18-195">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="faa18-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="faa18-196">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="faa18-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
