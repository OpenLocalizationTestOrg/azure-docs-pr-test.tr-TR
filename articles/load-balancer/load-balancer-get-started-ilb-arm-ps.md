---
title: "aaaCreate Azure iç yük dengeleyici - PowerShell | Microsoft Docs"
description: "Toocreate bir iç yük dengeleyici Kaynak Yöneticisi'nde PowerShell kullanarak nasıl öğrenin"
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
ms.openlocfilehash: 4b9657c77aa32a142de49ff7871ed6a396b22223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-powershell"></a><span data-ttu-id="c4460-103">PowerShell kullanarak iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4460-103">Create an internal load balancer using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4460-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c4460-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="c4460-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4460-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="c4460-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c4460-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="c4460-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="c4460-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c4460-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c4460-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c4460-109">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c4460-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

<span data-ttu-id="c4460-110">Aşağıdaki adımları hello nasıl toocreate bir iç yük dengeleyici PowerShell ile Azure Resource Manager kullanarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c4460-110">hello following steps explain how toocreate an internal load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="c4460-111">Azure Resource Manager ile Merhaba öğeleri toocreate bir iç yük dengeleyici ayrı ayrı yapılandırılır ve toocreate bir yük dengeleyici bileşik.</span><span class="sxs-lookup"><span data-stu-id="c4460-111">With Azure Resource Manager, hello items toocreate a Internal load balancer are configured individually and then combined toocreate a load balancer.</span></span>

<span data-ttu-id="c4460-112">Nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmak ve toocreate gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4460-112">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="c4460-113">Ön uç IP yapılandırması - hello özel IP adresi gelen ağ trafiği için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c4460-113">Front end IP configuration - will configure hello private IP address for incoming network traffic</span></span>
* <span data-ttu-id="c4460-114">Arka uç adres havuzu - ön uç IP havuzundan gelen hello yükü dengelenmiş trafiği alacak hello ağ arabirimleri yapılandıracağınız</span><span class="sxs-lookup"><span data-stu-id="c4460-114">Backend address pool - will configure hello network interfaces which will receive hello load balanced traffic coming from front end IP pool</span></span>
* <span data-ttu-id="c4460-115">Yük Dengeleme kuralları - kaynak ve yerel bağlantı noktası yapılandırmasını hello için yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="c4460-115">Load balancing rules - source and local port configuration for hello load balancer.</span></span>
* <span data-ttu-id="c4460-116">Yoklamaları - hello sistem durum araştırması hello sanal makine örnekleri için yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="c4460-116">Probes - configures hello health status probe for hello Virtual Machine instances.</span></span>
* <span data-ttu-id="c4460-117">Gelen NAT kuralları - başlangıç bağlantı noktası kuralları toodirectly erişim hello sanal makine örneklerinden biri yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="c4460-117">Inbound NAT rules - configures hello port rules toodirectly access one of hello Virtual Machine instances.</span></span>

<span data-ttu-id="c4460-118">Azure Resource Manager içindeki yük dengeleyici bileşenleri hakkında daha fazla bilgi için bkz. [Azure Resource Manager yük dengeleyici desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="c4460-118">You can get more information about load balancer components with Azure resource manager at [Azure Resource Manager support for load balancer](load-balancer-arm.md).</span></span>

<span data-ttu-id="c4460-119">Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl tooconfigure iki sanal makineler arasında bir yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="c4460-119">hello following steps explain how tooconfigure a load balancer between two virtual machines.</span></span>

## <a name="setup-powershell-toouse-resource-manager"></a><span data-ttu-id="c4460-120">PowerShell toouse Resource Manager Kurulumu</span><span class="sxs-lookup"><span data-stu-id="c4460-120">Setup PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="c4460-121">Hello en son ürün sürümüne hello Azure modülü için PowerShell sahip ve doğru şekilde, Azure aboneliğinizin tooaccess Kurulum PowerShell sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c4460-121">Make sure you have hello latest production version of hello Azure module for PowerShell, and have PowerShell setup correctly tooaccess your Azure subscription.</span></span>

### <a name="step-1"></a><span data-ttu-id="c4460-122">1. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-122">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="c4460-123">2. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-123">Step 2</span></span>

<span data-ttu-id="c4460-124">Merhaba hesabının Hello abonelikleri kontrol edin</span><span class="sxs-lookup"><span data-stu-id="c4460-124">Check hello subscriptions for hello account</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="c4460-125">Kimlik bilgilerinizle istendiğinde tooAuthenticate olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4460-125">You will be prompted tooAuthenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="c4460-126">3. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-126">Step 3</span></span>

<span data-ttu-id="c4460-127">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="c4460-127">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="create-resource-group-for-load-balancer"></a><span data-ttu-id="c4460-128">Yük dengeleyici için Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4460-128">Create Resource Group for load balancer</span></span>

<span data-ttu-id="c4460-129">Yeni bir kaynak grubu oluşturma (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın)</span><span class="sxs-lookup"><span data-stu-id="c4460-129">Create a new resource group (skip this step if using an existing resource group)</span></span>

```powershell
New-AzureRmResourceGroup -Name NRP-RG -location "West US"
```

<span data-ttu-id="c4460-130">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c4460-130">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="c4460-131">Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4460-131">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="c4460-132">Bir yük dengeleyicinin kullanacağı toocreate aynı hello tüm komutları emin olun kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="c4460-132">Make sure all commands toocreate a load balancer will use hello same resource group.</span></span>

<span data-ttu-id="c4460-133">Hello biz Yukarıdaki örnek "NRP-RG adlı" "Batı ABD" konumlu bir kaynak grubu oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="c4460-133">In hello example above we created a resource group called "NRP-RG" and location "West US".</span></span>

## <a name="create-virtual-network-and-a-private-ip-address-for-front-end-ip-pool"></a><span data-ttu-id="c4460-134">Ön uç IP havuzu için Sanal Ağ ve özel IP adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4460-134">Create Virtual Network and a private IP address for front end IP pool</span></span>

<span data-ttu-id="c4460-135">Merhaba sanal ağ için bir alt ağ oluşturur ve toovariable $backendSubnet atar</span><span class="sxs-lookup"><span data-stu-id="c4460-135">Creates a subnet for hello virtual network and assigns toovariable $backendSubnet</span></span>

```powershell
$backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
```

<span data-ttu-id="c4460-136">Sanal ağ oluşturma:</span><span class="sxs-lookup"><span data-stu-id="c4460-136">Create a virtual network:</span></span>

```powershell
$vnet= New-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
```

<span data-ttu-id="c4460-137">Merhaba sanal ağ oluşturur ve hello alt lb alt olması toohello sanal ağ NRPVNet ekler ve toovariable $vnet atar</span><span class="sxs-lookup"><span data-stu-id="c4460-137">Creates hello virtual network and adds hello subnet lb-subnet-be toohello virtual network NRPVNet and assigns toovariable $vnet</span></span>

## <a name="create-front-end-ip-pool-and-backend-address-pool"></a><span data-ttu-id="c4460-138">Ön uç IP havuzu ve arka uç adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4460-138">Create Front end IP pool and backend address pool</span></span>

<span data-ttu-id="c4460-139">Merhaba gelen için bir ön uç IP havuzu ayarlama yük dengeleyici ağ trafiği ve arka uç adres havuzu tooreceive hello yükü dengelenmiş trafiği.</span><span class="sxs-lookup"><span data-stu-id="c4460-139">Setting up a front end IP pool for hello incoming load balancer network traffic and backend address pool tooreceive hello load balanced traffic.</span></span>

### <a name="step-1"></a><span data-ttu-id="c4460-140">1. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-140">Step 1</span></span>

<span data-ttu-id="c4460-141">Merhaba gelen ağ trafiğini uç olacağı hello alt 10.0.2.0/24 için Hello özel IP adresi 10.0.2.5 kullanarak bir ön uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4460-141">Create a front end IP pool using hello private IP address 10.0.2.5 for hello subnet 10.0.2.0/24 which will be hello incoming network traffic endpoint.</span></span>

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PrivateIpAddress 10.0.2.5 -SubnetId $vnet.subnets[0].Id
```

### <a name="step-2"></a><span data-ttu-id="c4460-142">2. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-142">Step 2</span></span>

<span data-ttu-id="c4460-143">Bir arka uç adres havuzu ayarlama tooreceive gelen trafiği ön uç IP havuzundan kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c4460-143">Set up a back end address pool used tooreceive incoming traffic from front end IP pool:</span></span>

```powershell
$beaddresspool= New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
```

## <a name="create-lb-rules-nat-rules-probe-and-load-balancer"></a><span data-ttu-id="c4460-144">LB kuralları, NAT kuralları, araştırma ve yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4460-144">Create LB rules, NAT rules, probe and load balancer</span></span>

<span data-ttu-id="c4460-145">Merhaba ön uç IP havuzu ve hello arka uç adres havuzu oluşturduktan sonra toohello yük dengeleyici kaynak ait toocreate hello kuralları gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4460-145">After creating hello front end IP pool and hello backend address pool, you will need toocreate hello rules which will belong toohello load balancer resource:</span></span>

### <a name="step-1"></a><span data-ttu-id="c4460-146">1. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-146">Step 1</span></span>

```powershell
$inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP1" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

$inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name "RDP2" -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389

$healthProbe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -RequestPath "HealthProbe.aspx" -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name "HTTP" -FrontendIpConfiguration $frontendIP -BackendAddressPool $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
```

<span data-ttu-id="c4460-147">Yukarıdaki Hello örnek öğeleri aşağıdaki hello oluşturuluyor:</span><span class="sxs-lookup"><span data-stu-id="c4460-147">hello example above is creating hello following items:</span></span>

* <span data-ttu-id="c4460-148">Tüm gelen tooport 3441 trafiği NAT kuralı tooport 3389 geçer.</span><span class="sxs-lookup"><span data-stu-id="c4460-148">NAT rule which all incoming traffic tooport 3441 will go tooport 3389.</span></span>
* <span data-ttu-id="c4460-149">tooport 3442 trafiği tüm gelen, ikinci bir NAT kuralı tooport 3389 geçer.</span><span class="sxs-lookup"><span data-stu-id="c4460-149">a second NAT rule which all incoming traffic tooport 3442 will go tooport 3389.</span></span>
* <span data-ttu-id="c4460-150">yükleyecek bir yük dengeleyici kuralı genel bağlantı noktası 80 toolocal 80 numaralı bağlantı noktasında hello arka uç adres havuzundaki tüm gelen trafiği dengeler.</span><span class="sxs-lookup"><span data-stu-id="c4460-150">a load balancer rule which will load balance all incoming traffic on public port 80 toolocal port 80 in hello back end address pool.</span></span>
* <span data-ttu-id="c4460-151">Araştırma kuralı, bir yolu "HealthProbe.aspx" Merhaba sistem durumunu denetler</span><span class="sxs-lookup"><span data-stu-id="c4460-151">a probe rule which will check hello health status for path "HealthProbe.aspx"</span></span>

### <a name="step-2"></a><span data-ttu-id="c4460-152">2. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-152">Step 2</span></span>

<span data-ttu-id="c4460-153">Merhaba yük dengeleyici (NAT kuralları, yük dengeleyici kuralları, araştırma yapılandırmaları) tüm nesnelerin araya ekleme oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c4460-153">Create hello load balancer adding all objects (NAT rules, Load balancer rules, probe configurations) together:</span></span>

```powershell
$NRPLB = New-AzureRmLoadBalancer -ResourceGroupName "NRP-RG" -Name "NRP-LB" -Location "West US" -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
```

## <a name="create-network-interfaces"></a><span data-ttu-id="c4460-154">Ağ arabirimlerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4460-154">Create network interfaces</span></span>

<span data-ttu-id="c4460-155">Merhaba iç yük dengeleyici oluşturduktan sonra hangi ağ arabirimleri hello gelen yük dengeli ağ trafiği NAT kuralları ve araştırma alacaksınız tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c4460-155">After creating hello internal load balancer, you need define which network interfaces will be receiving hello incoming load balanced network traffic, NAT rules and probe.</span></span> <span data-ttu-id="c4460-156">Hello ağ arabirimi, bu durumda tek tek yapılandırılır ve tooa sanal makineyi daha sonra atanabilir.</span><span class="sxs-lookup"><span data-stu-id="c4460-156">hello network interface in this case is configured individually and can be assigned tooa virtual machine later on.</span></span>

### <a name="step-1"></a><span data-ttu-id="c4460-157">1. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-157">Step 1</span></span>

<span data-ttu-id="c4460-158">Merhaba kaynak sanal ağ ve alt ağ toocreate ağ arabirimlerini Al:</span><span class="sxs-lookup"><span data-stu-id="c4460-158">Get hello resource virtual network and subnet toocreate network interfaces:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG

$backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
```

<span data-ttu-id="c4460-159">Bu adım toohello yük dengeleyici arka uç havuzuna ait ve bu ağ arabirimi için RDP hello ilk NAT kuralında ilişkilendirmek bir ağ arabirimi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c4460-159">This step creates a network interface which will belong toohello load balancer back end pool and associate hello first NAT rule for RDP for this network interface:</span></span>

```powershell
$backendnic1= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic1-be -Location "West US" -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
```

### <a name="step-2"></a><span data-ttu-id="c4460-160">2. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-160">Step 2</span></span>

<span data-ttu-id="c4460-161">LB-Nic2-BE adında ikinci bir ağ arabirimi oluşturma:</span><span class="sxs-lookup"><span data-stu-id="c4460-161">Create a second network interface called LB-Nic2-BE:</span></span>

<span data-ttu-id="c4460-162">Bu adımı ikinci bir ağ arabirimi oluşturur, geri aynı yük dengeleyici havuzu sonlandırmak ve hello ikinci NAT kuralı ilişkilendirme için RDP oluşturulan toohello atama:</span><span class="sxs-lookup"><span data-stu-id="c4460-162">This step creates a second network interface, assigning toohello same load balancer back end pool and associating hello second NAT rule created for RDP:</span></span>

```powershell
$backendnic2= New-AzureRmNetworkInterface -ResourceGroupName "NRP-RG" -Name lb-nic2-be -Location "West US" -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
```

<span data-ttu-id="c4460-163">Merhaba sonuç hello şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="c4460-163">hello end result will show hello following:</span></span>

    $backendnic1

<span data-ttu-id="c4460-164">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c4460-164">Expected output:</span></span>

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



### <a name="step-3"></a><span data-ttu-id="c4460-165">3. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-165">Step 3</span></span>

<span data-ttu-id="c4460-166">Merhaba komutu Ekle AzureRmVMNetworkInterface tooassign hello NIC tooa sanal makine kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4460-166">Use hello command Add-AzureRmVMNetworkInterface tooassign hello NIC tooa virtual Machine.</span></span>

<span data-ttu-id="c4460-167">Adım adım yönergeler toocreate bir sanal makine hello ve tooa NIC atayın bulabilir hello belgelerine aşağıdaki: [Azure PowerShell kullanarak bir VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4460-167">You can find hello step by step instructions toocreate a virtual machine and assign tooa NIC following hello documentation: [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-hello-network-interface"></a><span data-ttu-id="c4460-168">Merhaba ağ arabirimi ekleyin</span><span class="sxs-lookup"><span data-stu-id="c4460-168">Add hello network interface</span></span>

<span data-ttu-id="c4460-169">Oluşturulan bir sanal makine zaten varsa, aşağıdaki adımları hello ile Merhaba ağ arabirimi ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4460-169">If you already have a virtual machine created, you can add hello network interface with hello following steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="c4460-170">1. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-170">Step 1</span></span>

<span data-ttu-id="c4460-171">(Bunu, henüz yapmadıysanız) hello yük dengeleyici kaynak bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c4460-171">Load hello load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="c4460-172">kullanılan hello çağrılan $lb ve kullanım hello hello yük dengeleyici kaynak aynı adlarından yukarıda oluşturduğunuz değişkenidir.</span><span class="sxs-lookup"><span data-stu-id="c4460-172">hello variable used is called $lb and use hello same names from hello load balancer resource created above.</span></span>

```powershell
$lb = Get-AzureRmLoadBalancer –name NRP-LB -resourcegroupname NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="c4460-173">2. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-173">Step 2</span></span>

<span data-ttu-id="c4460-174">Yük hello arka uç yapılandırması tooa değişkeni.</span><span class="sxs-lookup"><span data-stu-id="c4460-174">Load hello backend configuration tooa variable.</span></span>

```powershell
$backend = Get-AzureRmLoadBalancerBackendAddressPoolConfig -name backendpool1 -LoadBalancer $lb
```

### <a name="step-3"></a><span data-ttu-id="c4460-175">3. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-175">Step 3</span></span>

<span data-ttu-id="c4460-176">Önceden oluşturulmuş hello ağ arabirimi bir değişkene yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c4460-176">Load hello already created network interface into a variable.</span></span> <span data-ttu-id="c4460-177">kullanılan hello değişken $NIC adıdır</span><span class="sxs-lookup"><span data-stu-id="c4460-177">hello variable name used is $nic.</span></span> <span data-ttu-id="c4460-178">kullanılan hello ağ arabirimi adı olduğu hello aynı örnek hello yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="c4460-178">hello network interface name used is hello same from hello example above.</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface –name lb-nic1-be -resourcegroupname NRP-RG
```

### <a name="step-4"></a><span data-ttu-id="c4460-179">4. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-179">Step 4</span></span>

<span data-ttu-id="c4460-180">Merhaba arka uç yapılandırması hello ağ arabiriminde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c4460-180">Change hello backend configuration on hello network interface.</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
```

### <a name="step-5"></a><span data-ttu-id="c4460-181">5. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-181">Step 5</span></span>

<span data-ttu-id="c4460-182">Merhaba ağ arabirimi nesnesi kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c4460-182">Save hello network interface object.</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="c4460-183">Bir ağ arabirimi toohello yük dengeleyici arka uç havuzuna eklendikten sonra ağ trafiğini hello Yük Dengeleme kuralları bu yük dengeleyici kaynak için temel almayı başlatır.</span><span class="sxs-lookup"><span data-stu-id="c4460-183">After a network interface is added toohello load balancer backend pool, it starts receiving network traffic based on hello load balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="c4460-184">Mevcut yük dengeleyiciyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c4460-184">Update an existing load balancer</span></span>

### <a name="step-1"></a><span data-ttu-id="c4460-185">1. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-185">Step 1</span></span>
<span data-ttu-id="c4460-186">Yukarıdaki hello örneğindeki Hello yük dengeleyicinin kullanılması, yük dengeleyici nesne toovariable Get-AzureRmLoadBalancer kullanarak $slb atayın</span><span class="sxs-lookup"><span data-stu-id="c4460-186">Using hello load balancer from hello example above, assign load balancer object toovariable $slb using Get-AzureRmLoadBalancer</span></span>

```powershell
$slb = Get-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

### <a name="step-2"></a><span data-ttu-id="c4460-187">2. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-187">Step 2</span></span>

<span data-ttu-id="c4460-188">Merhaba, aşağıdaki örneğine, hello ön uç bağlantı noktası 81'i kullanarak yeni bir gelen NAT kuralı ekleyeceksiniz ve hello geri için bağlantı noktası 8181 bitiş havuzu tooan varolan yük dengeleyicisi</span><span class="sxs-lookup"><span data-stu-id="c4460-188">In hello following example, you will add a new Inbound NAT rule using port 81 in hello front end and port 8181 for hello back end pool tooan existing load balancer</span></span>

```powershell
$slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol Tcp
```

### <a name="step-3"></a><span data-ttu-id="c4460-189">3. Adım</span><span class="sxs-lookup"><span data-stu-id="c4460-189">Step 3</span></span>

<span data-ttu-id="c4460-190">Set-AzureLoadBalancer kullanarak hello yeni yapılandırmayı kaydedin</span><span class="sxs-lookup"><span data-stu-id="c4460-190">Save hello new configuration using Set-AzureLoadBalancer</span></span>

```powershell
$slb | Set-AzureRmLoadBalancer
```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="c4460-191">Yük dengeleyici kaldırma</span><span class="sxs-lookup"><span data-stu-id="c4460-191">Remove a load balancer</span></span>

<span data-ttu-id="c4460-192">Merhaba komutu Kaldır AzureRmLoadBalancer toodelete "NRP-"NRP-RG"adlı LB" bir kaynak grubunda adlı önceden oluşturulmuş yük dengeleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="c4460-192">Use hello command Remove-AzureRmLoadBalancer toodelete a previously created load balancer named "NRP-LB"  in a resource group called "NRP-RG"</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRPLB -ResourceGroupName NRP-RG
```

> [!NOTE]
> <span data-ttu-id="c4460-193">İsteğe bağlı hello kullanabilirsiniz geçiş - Force tooavoid hello istemi silme işlemi için.</span><span class="sxs-lookup"><span data-stu-id="c4460-193">You can use hello optional switch -Force tooavoid hello prompt for deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4460-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4460-194">Next steps</span></span>

[<span data-ttu-id="c4460-195">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4460-195">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c4460-196">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4460-196">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
