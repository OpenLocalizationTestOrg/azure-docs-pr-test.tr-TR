---
title: "aaaCreate özel bir araştırma - Azure uygulama ağ geçidi - PowerShell | Microsoft Docs"
description: "Nasıl toocreate özel bir araştırma uygulama ağ geçidi için Kaynak Yöneticisi'nde PowerShell kullanarak bilgi edinin"
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
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="2cef3-103">Azure Resource Manager PowerShell kullanarak Azure uygulama ağ geçidi için özel bir araştırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cef3-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2cef3-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2cef3-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="2cef3-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cef3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="2cef3-106">Azure Klasik PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cef3-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="2cef3-107">Bu makalede, bir özel araştırma tooan varolan uygulama ağ geçidi PowerShell ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2cef3-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="2cef3-108">Özel araştırmalara başarılı bir yanıt hello varsayılan web uygulaması üzerinde sağlamaz, uygulamaları veya belirli bir sağlık denetimi sayfası uygulamaları için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="2cef3-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="2cef3-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2cef3-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="2cef3-110">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2cef3-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="2cef3-111">Bir uygulama ağ geçidi ile özel bir araştırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cef3-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="2cef3-112">Oturum açın ve kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="2cef3-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="2cef3-113">Kullanım `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="2cef3-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="2cef3-114">Merhaba hesap Hello abonelikler alın.</span><span class="sxs-lookup"><span data-stu-id="2cef3-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="2cef3-115">Azure abonelikleri toouse hangisinin seçin.</span><span class="sxs-lookup"><span data-stu-id="2cef3-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="2cef3-116">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2cef3-116">Create a resource group.</span></span> <span data-ttu-id="2cef3-117">Varolan bir kaynak grubunuz varsa, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cef3-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="2cef3-118">Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2cef3-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="2cef3-119">Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2cef3-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="2cef3-120">Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="2cef3-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="2cef3-121">Adlı bir kaynak grubu oluşturduk örnek önceki hello **appgw-RG** konumda **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="2cef3-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="2cef3-122">Sanal ağ ve alt ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cef3-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="2cef3-123">Merhaba aşağıdaki örnek bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2cef3-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="2cef3-124">Uygulama ağ geçidi, kendi alt ağ için kullanılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2cef3-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="2cef3-125">Bu nedenle, hello uygulama ağ geçidi için oluşturulan hello alt ağ için oluşturulan ve kullanılan diğer alt ağları toobe hello VNET tooallow hello adres alanı değerinden küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2cef3-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="2cef3-126">Merhaba ön uç yapılandırma için genel bir IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="2cef3-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="2cef3-127">Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="2cef3-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="2cef3-128">Bu örnek hello ön uç IP adresi hello uygulama ağ geçidi için bir ortak IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2cef3-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="2cef3-129">Uygulama ağ geçidi gerektiren dinamik olarak oluşturulmuş bir DNS adı bu nedenle hello hello ortak IP adresi toohave `-DomainNameLabel` hello genel IP adresi hello oluşturma sırasında belirtilemez.</span><span class="sxs-lookup"><span data-stu-id="2cef3-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="2cef3-130">Uygulama ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cef3-130">Create an application gateway</span></span>

<span data-ttu-id="2cef3-131">Tüm yapılandırma öğelerini hello uygulama ağ geçidi oluşturmadan önce ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2cef3-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="2cef3-132">Merhaba aşağıdaki örnek hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2cef3-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="2cef3-133">**Bileşen**</span><span class="sxs-lookup"><span data-stu-id="2cef3-133">**Component**</span></span> | <span data-ttu-id="2cef3-134">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="2cef3-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="2cef3-135">**Ağ geçidi IP yapılandırması**</span><span class="sxs-lookup"><span data-stu-id="2cef3-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="2cef3-136">Bir uygulama ağ geçidi için IP yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="2cef3-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="2cef3-137">**Arka uç havuzu**</span><span class="sxs-lookup"><span data-stu-id="2cef3-137">**Backend pool**</span></span> | <span data-ttu-id="2cef3-138">IP adresleri, FQDN'ın veya Merhaba web uygulaması konağı toohello uygulama sunucuları NIC havuzu</span><span class="sxs-lookup"><span data-stu-id="2cef3-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="2cef3-139">**Sistem durumu araştırması**</span><span class="sxs-lookup"><span data-stu-id="2cef3-139">**Health probe**</span></span> | <span data-ttu-id="2cef3-140">Özel bir araştırma toomonitor hello durumu hello arka uç havuzu üyelerinin kullanılan</span><span class="sxs-lookup"><span data-stu-id="2cef3-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="2cef3-141">**HTTP ayarları**</span><span class="sxs-lookup"><span data-stu-id="2cef3-141">**HTTP settings**</span></span> | <span data-ttu-id="2cef3-142">Ayarlar dahil olmak üzere, bağlantı noktası, protokol, tanımlama bilgisi temelli benzeşimi, araştırma ve zaman aşımı koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="2cef3-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="2cef3-143">Bu ayarların nasıl trafiği yönlendirilmiş toohello arka uç havuzu üyeleri belirlemek</span><span class="sxs-lookup"><span data-stu-id="2cef3-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="2cef3-144">**Ön uç bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="2cef3-144">**Frontend port**</span></span> | <span data-ttu-id="2cef3-145">Uygulama ağ geçidi hello hello bağlantı noktası üzerinde trafiği için dinler</span><span class="sxs-lookup"><span data-stu-id="2cef3-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="2cef3-146">**Dinleyici**</span><span class="sxs-lookup"><span data-stu-id="2cef3-146">**Listener**</span></span> | <span data-ttu-id="2cef3-147">Protokol, ön uç IP yapılandırması ve ön uç bağlantı noktası birleşimi.</span><span class="sxs-lookup"><span data-stu-id="2cef3-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="2cef3-148">Ne gelen istekleri dinlediği budur.</span><span class="sxs-lookup"><span data-stu-id="2cef3-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="2cef3-149">**Kural**</span><span class="sxs-lookup"><span data-stu-id="2cef3-149">**Rule**</span></span>| <span data-ttu-id="2cef3-150">HTTP ayarlarınızı temel alan trafiği toohello uygun arka uç yolları hello.</span><span class="sxs-lookup"><span data-stu-id="2cef3-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="2cef3-151">Bir araştırma tooan varolan uygulama ağ geçidi Ekle</span><span class="sxs-lookup"><span data-stu-id="2cef3-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="2cef3-152">Merhaba aşağıdaki kod parçacığını bir araştırma tooan varolan uygulama ağ geçidi ekler.</span><span class="sxs-lookup"><span data-stu-id="2cef3-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="2cef3-153">Var olan bir uygulama ağ geçidi'nden bir araştırma Kaldır</span><span class="sxs-lookup"><span data-stu-id="2cef3-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="2cef3-154">Aşağıdaki kod parçacığını hello var olan bir uygulama ağ geçidi'nden bir araştırma kaldırır.</span><span class="sxs-lookup"><span data-stu-id="2cef3-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="2cef3-155">Uygulama ağ geçidi DNS adını alma</span><span class="sxs-lookup"><span data-stu-id="2cef3-155">Get application gateway DNS name</span></span>

<span data-ttu-id="2cef3-156">Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır.</span><span class="sxs-lookup"><span data-stu-id="2cef3-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="2cef3-157">Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir.</span><span class="sxs-lookup"><span data-stu-id="2cef3-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="2cef3-158">tooensure son kullanıcılar bir CNAME kaydı kullanılabilir hello uygulama ağ geçidi isabet toopoint hello uygulama ağ geçidi toohello ortak uç nokta.</span><span class="sxs-lookup"><span data-stu-id="2cef3-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="2cef3-159">[Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2cef3-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="2cef3-160">toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı.</span><span class="sxs-lookup"><span data-stu-id="2cef3-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="2cef3-161">Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2cef3-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="2cef3-162">Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.</span><span class="sxs-lookup"><span data-stu-id="2cef3-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2cef3-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2cef3-163">Next steps</span></span>

<span data-ttu-id="2cef3-164">Tooconfigure ziyaret ederek SSL boşaltma öğrenin: [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="2cef3-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

