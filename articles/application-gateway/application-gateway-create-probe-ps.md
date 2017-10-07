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
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a>Azure Resource Manager PowerShell kullanarak Azure uygulama ağ geçidi için özel bir araştırma oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Klasik PowerShell](application-gateway-create-probe-classic-ps.md)

Bu makalede, bir özel araştırma tooan varolan uygulama ağ geçidi PowerShell ile ekleyin. Özel araştırmalara başarılı bir yanıt hello varsayılan web uygulaması üzerinde sağlamaz, uygulamaları veya belirli bir sağlık denetimi sayfası uygulamaları için kullanışlıdır.

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](application-gateway-create-probe-classic-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a>Bir uygulama ağ geçidi ile özel bir araştırma oluşturma

### <a name="sign-in-and-create-resource-group"></a>Oturum açın ve kaynak grubu oluştur

1. Kullanım `Login-AzureRmAccount` tooauthenticate.

  ```powershell
  Login-AzureRmAccount
  ```

1. Merhaba hesap Hello abonelikler alın.

  ```powershell
  Get-AzureRmSubscription
  ```

1. Azure abonelikleri toouse hangisinin seçin.

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. Bir kaynak grubu oluşturun. Varolan bir kaynak grubunuz varsa, bu adımı atlayabilirsiniz.

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.

Adlı bir kaynak grubu oluşturduk örnek önceki hello **appgw-RG** konumda **Batı ABD**.

### <a name="create-a-virtual-network-and-a-subnet"></a>Sanal ağ ve alt ağ oluşturma

Merhaba aşağıdaki örnek bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturur. Uygulama ağ geçidi, kendi alt ağ için kullanılmasını gerektirir. Bu nedenle, hello uygulama ağ geçidi için oluşturulan hello alt ağ için oluşturulan ve kullanılan diğer alt ağları toobe hello VNET tooallow hello adres alanı değerinden küçük olmalıdır.

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Merhaba ön uç yapılandırma için genel bir IP adresi oluştur

Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için. Bu örnek hello ön uç IP adresi hello uygulama ağ geçidi için bir ortak IP adresini kullanır.  Uygulama ağ geçidi gerektiren dinamik olarak oluşturulmuş bir DNS adı bu nedenle hello hello ortak IP adresi toohave `-DomainNameLabel` hello genel IP adresi hello oluşturma sırasında belirtilemez.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

Tüm yapılandırma öğelerini hello uygulama ağ geçidi oluşturmadan önce ayarlayın. Merhaba aşağıdaki örnek hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturur.

| **Bileşen** | **Açıklama** |
|---|---|
| **Ağ geçidi IP yapılandırması** | Bir uygulama ağ geçidi için IP yapılandırma.|
| **Arka uç havuzu** | IP adresleri, FQDN'ın veya Merhaba web uygulaması konağı toohello uygulama sunucuları NIC havuzu|
| **Sistem durumu araştırması** | Özel bir araştırma toomonitor hello durumu hello arka uç havuzu üyelerinin kullanılan|
| **HTTP ayarları** | Ayarlar dahil olmak üzere, bağlantı noktası, protokol, tanımlama bilgisi temelli benzeşimi, araştırma ve zaman aşımı koleksiyonu.  Bu ayarların nasıl trafiği yönlendirilmiş toohello arka uç havuzu üyeleri belirlemek|
| **Ön uç bağlantı noktası** | Uygulama ağ geçidi hello hello bağlantı noktası üzerinde trafiği için dinler|
| **Dinleyici** | Protokol, ön uç IP yapılandırması ve ön uç bağlantı noktası birleşimi. Ne gelen istekleri dinlediği budur.
|**Kural**| HTTP ayarlarınızı temel alan trafiği toohello uygun arka uç yolları hello.|

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

## <a name="add-a-probe-tooan-existing-application-gateway"></a>Bir araştırma tooan varolan uygulama ağ geçidi Ekle

Merhaba aşağıdaki kod parçacığını bir araştırma tooan varolan uygulama ağ geçidi ekler.

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

## <a name="remove-a-probe-from-an-existing-application-gateway"></a>Var olan bir uygulama ağ geçidi'nden bir araştırma Kaldır

Aşağıdaki kod parçacığını hello var olan bir uygulama ağ geçidi'nden bir araştırma kaldırır.

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

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. tooensure son kullanıcılar bir CNAME kaydı kullanılabilir hello uygulama ağ geçidi isabet toopoint hello uygulama ağ geçidi toohello ortak uç nokta. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı. Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır. Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.

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

## <a name="next-steps"></a>Sonraki adımlar

Tooconfigure ziyaret ederek SSL boşaltma öğrenin: [SSL boşaltma yapılandırın](application-gateway-ssl-arm.md)

