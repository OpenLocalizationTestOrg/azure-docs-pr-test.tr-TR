---
title: "Azure uygulama ağ geçidi - PowerShell özel bir araştırma - oluşturma | Microsoft Docs"
description: "Kaynak Yöneticisi'nde PowerShell kullanarak uygulama ağ geçidi için özel bir araştırma oluşturmayı öğrenin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="3ebe6-103">Azure Resource Manager PowerShell kullanarak Azure uygulama ağ geçidi için özel bir araştırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ebe6-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ebe6-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3ebe6-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="3ebe6-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ebe6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="3ebe6-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ebe6-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="3ebe6-107">Bu makalede, PowerShell ile var olan bir uygulama ağ geçidi için özel bir araştırma ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="3ebe6-108">Özel araştırmalara başarılı yanıt varsayılan web uygulaması üzerinde sağlamaz, uygulamaları veya belirli bir sağlık denetimi sayfası uygulamaları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="3ebe6-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3ebe6-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="3ebe6-110">Bu makale, Microsoft’un çoğu yeni dağıtım için [klasik dağıtım modeli](application-gateway-create-probe-classic-ps.md) yerine önerdiği Resource Manager dağıtım modelini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="3ebe6-111">Bir uygulama ağ geçidi ile özel bir araştırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ebe6-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="3ebe6-112">Oturum açın ve kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="3ebe6-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="3ebe6-113">Kullanım `Login-AzureRmAccount` kimliğini doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="3ebe6-114">Hesap için abonelikler alın.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="3ebe6-115">Hangi Azure aboneliğinizin kullanılacağını seçin.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="3ebe6-116">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-116">Create a resource group.</span></span> <span data-ttu-id="3ebe6-117">Varolan bir kaynak grubunuz varsa, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="3ebe6-118">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="3ebe6-119">Bu konum, kaynak grubundaki kaynaklar için varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="3ebe6-120">Bir uygulama ağ geçidi oluşturmak için verilecek komutların aynı kaynak grubunda kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="3ebe6-121">Önceki örnekte adlı bir kaynak grubu oluşturduk **appgw-RG** konumda **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="3ebe6-122">Sanal ağ ve alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ebe6-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="3ebe6-123">Aşağıdaki örnek, bir sanal ağ ve uygulama ağ geçidi için bir alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="3ebe6-124">Uygulama ağ geçidi, kendi alt ağ için kullanılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="3ebe6-125">Bu nedenle, uygulama ağ geçidi için oluşturulan alt diğer alt oluşturulan ve kullanılabilmesi izin vermek için sanal ağ adres alanının değerinden küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="3ebe6-126">Ön uç yapılandırma için genel bir IP adresi oluşturun</span><span class="sxs-lookup"><span data-stu-id="3ebe6-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="3ebe6-127">Batı ABD bölgesi için **appgw-rg** kaynak grubunda **publicIP01** genel bir IP kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="3ebe6-128">Bu örnek uygulama ağ geçidi ön uç IP adresi için bir ortak IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="3ebe6-129">Uygulama ağ geçidi gerektiren dinamik olarak oluşturulmuş bir DNS adı bu nedenle olması için ortak IP adresi `-DomainNameLabel` genel IP adresi oluşturma sırasında belirtilemez.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="3ebe6-130">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3ebe6-130">Create an application gateway</span></span>

<span data-ttu-id="3ebe6-131">Uygulama ağ geçidi oluşturmadan önce tüm yapılandırma öğelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="3ebe6-132">Aşağıdaki örnek, bir uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğelerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="3ebe6-133">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-133">**Component**</span></span> | <span data-ttu-id="3ebe6-134">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="3ebe6-135">**Ağ geçidi IP yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="3ebe6-136">Bir uygulama ağ geçidi için IP yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="3ebe6-137">**Arka uç havuzu**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-137">**Backend pool**</span></span> | <span data-ttu-id="3ebe6-138">IP adresleri, FQDN'ın veya web uygulamasını barındırmak uygulama sunucularını NIC havuzu</span><span class="sxs-lookup"><span data-stu-id="3ebe6-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="3ebe6-139">**Sistem durumu araştırması**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-139">**Health probe**</span></span> | <span data-ttu-id="3ebe6-140">Arka uç havuzu üyeleri sağlığını izlemek için kullanılan özel bir araştırma</span><span class="sxs-lookup"><span data-stu-id="3ebe6-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="3ebe6-141">**HTTP ayarları**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-141">**HTTP settings**</span></span> | <span data-ttu-id="3ebe6-142">Ayarlar dahil olmak üzere, bağlantı noktası, protokol, tanımlama bilgisi temelli benzeşimi, araştırma ve zaman aşımı koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="3ebe6-143">Bu ayarlar, trafiği arka uç havuzu üyelerine nasıl yönlendirildiğini belirler.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="3ebe6-144">**Ön uç bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-144">**Frontend port**</span></span> | <span data-ttu-id="3ebe6-145">Uygulama ağ geçidi için trafiğini dinlediği bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="3ebe6-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="3ebe6-146">**Dinleyici**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-146">**Listener**</span></span> | <span data-ttu-id="3ebe6-147">Protokol, ön uç IP yapılandırması ve ön uç bağlantı noktası birleşimi.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="3ebe6-148">Ne gelen istekleri dinlediği budur.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="3ebe6-149">**Kural**</span><span class="sxs-lookup"><span data-stu-id="3ebe6-149">**Rule**</span></span>| <span data-ttu-id="3ebe6-150">Yollar uygun arka uç trafiği HTTP ayarlarınızı temel alan.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="3ebe6-151">Bir araştırma eklemek için var olan bir uygulama ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="3ebe6-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="3ebe6-152">Aşağıdaki kod parçacığını bir araştırma için var olan bir uygulama ağ geçidi ekler.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="3ebe6-153">Var olan bir uygulama ağ geçidi'nden bir araştırma Kaldır</span><span class="sxs-lookup"><span data-stu-id="3ebe6-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="3ebe6-154">Aşağıdaki kod parçacığını bir araştırma var olan bir uygulama ağ geçidi'nden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="3ebe6-155">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="3ebe6-155">Get application gateway DNS name</span></span>

<span data-ttu-id="3ebe6-156">Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="3ebe6-157">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="3ebe6-158">Son kullanıcıların uygulama ağ geçidine ulaşmasını sağlamak için uygulama ağ geçidinin genel uç noktasını işaret edecek bir CNAME kaydı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="3ebe6-159">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3ebe6-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="3ebe6-160">Bunu yapmak için uygulama ağ geçidinin ayrıntılarını ve onunla ilişkilendirilmiş olan IP/DNS adını uygulama ağ geçidine eklenmiş PublicIPAddress öğesini kullanarak alın.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="3ebe6-161">Uygulama ağ geçidinin DNS adı, iki web uygulamasını bu DNS adına götüren bir CNAME kaydı oluşturmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="3ebe6-162">Uygulama ağ geçidi yeniden başlatıldığında VIP değişebileceğinden A kaydı kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="3ebe6-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="3ebe6-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ebe6-163">Next steps</span></span>

<span data-ttu-id="3ebe6-164">Ziyaret ederek SSL boşaltma yapılandırmayı öğrenin: [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="3ebe6-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

