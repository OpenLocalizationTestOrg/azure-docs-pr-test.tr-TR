---
title: "aaaCreate ve Azure uygulama ağ geçidi - PowerShell yönetme | Microsoft Docs"
description: "Bu sayfa toocreate, yapılandırmak, başlatmak ve Azure Resource Manager kullanarak bir Azure uygulama ağ geçidini silme yönergelerini sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a>Azure Resource Manager kullanarak bir uygulama ağ geçidi oluşturma, başlatma veya silme

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Klasik PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager şablonu](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Merhaba Bulut veya şirket içi olup, yük devretme ve performans yönlendirme HTTP isteklerini, farklı sunucular arasında sağlar. Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok uygulama teslim denetleyicisi (ADC) özelliği sunar. toofind desteklenen özelliklerin tam bir listesi ziyaret [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md).

Bu makalede hello adımları toocreate anlatılmaktadır, yapılandırmak, başlatmak ve bir uygulama ağ geçidini silin.

> [!IMPORTANT]
> Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Resource Manager ve klasik. Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun. Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz. Bu belge, Azure Resource Manager’ı kullanarak uygulama ağ geçidi oluşturmayı kapsar. toouse hello Klasik sürümü, çok Git[PowerShell kullanarak bir uygulama ağ geçidi Klasik dağıtımı oluşturma](application-gateway-create-gateway.md).

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
1. Varolan bir sanal ağınız varsa, mevcut bir boş alt seçin veya hello uygulama ağ geçidi tarafından varolan sanal ağınızda kullanmak için yalnızca bir alt ağ oluşturun. Merhaba uygulama ağ geçidi tooa farklı sanal ağı dağıtamazsınız hello uygulama ağ geçidi arkasında toodeploy düşündüğünüz daha hello kaynak.
1. toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Gerekli toocreate bir uygulama ağ geçidi nedir?

* **Arka uç sunucusu havuzu:** IP adresleri, FQDN'ler ya da NIC'ler hello arka uç sunucularının hello listesi. IP adresleri kullanılıyorsa, ya da toohello sanal ağ alt ait olması gerekir veya genel IP/VIP'ye olmalıdır.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Trafiği, bu bağlantı noktasında trafik ve yeniden yönlendirilen tooone hello arka uç sunucularının alır.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).
* **Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğini olmalıdır belirler.

## <a name="create-a-resource-group-for-resource-manager"></a>Resource Manager için kaynak grubu oluşturun

Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

1. İçinde tooAzure oturum ve kimlik bilgilerinizi girin.

  ```powershell
  Login-AzureRmAccount
  ```

2. Merhaba hesabının Hello abonelikleri kontrol edin.

  ```powershell
  Get-AzureRmSubscription
  ```

3. Azure abonelikleri toouse hangisinin seçin.

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Bir uygulama ağ geçidini kullanan tüm komutları toocreate Merhaba, aynı olduğundan emin olun kaynak grubu.

Adlı bir kaynak grubu oluşturduk Hello yukarıdaki örnekte, **ContosoRG** ve konum **Doğu ABD**.

> [!NOTE]
> Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekiyorsa, ziyaret edin: [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md). Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.


## <a name="create-hello-application-gateway-configuration-objects"></a>Merhaba uygulama ağ geçidi yapılandırma nesnesi oluşturun

Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanması gerekir. Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Tamamlandığında, DNS ve VIP hello uygulama ağ geçidi ayrıntılarını hello ortak IP kaynak ekli toohello uygulama ağ geçidi'nden alın.

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a>Merhaba uygulama ağ geçidini Sil

Merhaba aşağıdaki örnek hello uygulama ağ geçidini siler.

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> Merhaba **-force** anahtar kullanılan toosuppress hello kaldırma onayı iletisini olabilir.

Hizmet hello tooverify kaldırıldı, hello kullanabilirsiniz `Get-AzureRmApplicationGateway` cmdlet'i. Bu adım gerekli değildir.

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir. toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı. Bu Azure DNS veya diğer DNS sağlayıcıları tarafından toohello işaret eden bir CNAME kaydı oluşturma yapılabilir [genel IP adresi](../dns/dns-custom-domain.md#public-ip-address). Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.

> [!NOTE]
> Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a>Tüm kaynakları silme

Bu makalede, aşağıdaki tam hello oluşturulan tüm kaynakları adım toodelete:

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a>Sonraki adımlar

SSL boşaltma tooconfigure istiyorsanız, ziyaret edin: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).

Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, ziyaret edin: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)
