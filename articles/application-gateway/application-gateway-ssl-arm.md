---
title: "Azure uygulama ağ geçidi - PowerShell SSL boşaltma - yapılandırma | Microsoft Docs"
description: "Bu sayfada Azure Resource Manager kullanarak SSL yük boşaltımıyla uygulama ağ geçidi oluşturmak için yönergeler bulunmaktadır."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ededabc7c665d6bb05b91e4d21d01fb1379add32
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Azure Resource Manager kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Klasik PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway, web grubunda maliyetli SSL şifre çözme görevlerinin oluşmasından kaçınmak için Güvenli Yuva Katmanı (SSL) oturumunu sonlandırmak amacıyla yapılandırılabilir. SSL yük boşaltımı ön uç sunucusunun kurulumunu ve web uygulamasının yönetimini de basitleştirir.

## <a name="before-you-begin"></a>Başlamadan önce

1. Web Platformu Yükleyicisi’ni kullanarak Azure PowerShell cmdlet’lerin en son sürümünü yükleyin. **İndirmeler sayfası**’ndaki [Windows PowerShell](https://azure.microsoft.com/downloads/) bölümünden en son sürümü indirip yükleyebilirsiniz.
2. Uygulama ağ geçidi için bir sanal ağ ve bir alt ağ oluşturacaksınız. Hiçbir sanal makinenin veya bulut dağıtımlarının alt ağı kullanmadığından emin olun. Application Gateway tek başına bir sanal ağ alt ağında olmalıdır.
3. Uygulama ağ geçidi kullanırken yapılandırdığınız sunucular mevcut olmalıdır veya uç noktaları sanal ağda veya atanan genel bir IP/VIP’de oluşturulmuş olmalıdır.

## <a name="what-is-required-to-create-an-application-gateway"></a>Bir uygulama ağ geçidi oluşturmak için ne gereklidir?

* **Arka uç sunucusu havuzu:** Arka uç sunucularının IP adreslerinin listesi. Listede bulunan IP adresleri sanal ağ alt ağına veya genel IP/VIP’ye ait olmalıdır.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bir havuza bağlıdır ve havuzdaki tüm sunuculara uygulanır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik olursa arka uç sunuculardan birine yönlendirilir.
* **Dinleyici:** Dinleyicide bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu ayarlar büyük/küçük harfe duyarlıdır) ve SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa) vardır.
* **Kural:** Kural, dinleyiciyi ve arka uç sunucusu havuzunu bağlar ve belli bir dinleyicide trafik olduğunda trafiğin hangi arka uç sunucu havuzuna yönlendirileceğini belirler. Şu anda yalnızca *temel* kural desteklenmektedir. *Temel* kural hepsini bir kez deneme yöntemiyle yük dağıtımıdır.

**Ek yapılandırma notları**

SSL sertifikaları yapılandırmada **HttpListener**’daki protokol *Https* (küçük/büyük harf duyarlı) ile değiştirilmelidir. **SslCertificate** öğesi SSL sertifikası için yapılandırılmış değişken değerle **HttpListener**’a eklenir. Ön uç bağlantı noktası 443’e yükseltilmelidir.

**Tanımlama bilgisi temelli benzeşimi etkinleştirme:** Bir uygulama ağ geçidi, bir istemci oturumundan gelen isteğin web grubunda hep aynı VM’e yönlendirildiğinden emin olmak için yapılandırılabilir. Bu senaryo, ağ geçidinin trafiği uygun bir şekilde yönlendirmesini sağlayacak oturum tanımlama bilgisinin eklenmesiyle gerçekleştirilir. Tanımlama bilgisi temelli benzeşimi etkinleştirmek için, **CookieBasedAffinity**’yi *BackendHttpSetting* öğesindeki **Enabled**’a ayarlayın.

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

Azure Klasik dağıtım modeli ve Azure Resource Manager arasındaki fark, uygulama ağ geçidi oluştururken takip ettiğiniz sıra ve yapılandırılması gereken öğelerdir.

Resource Manager'da uygulama ağ geçidini oluşturan tüm öğeler ayrı ayrı yapılandırılır ve ardından bir uygulama ağ geçidi kaynağı oluşturmak üzere bir araya getirilir.

Bir uygulama ağ geçidi oluşturmak için takip etmeniz gereken adımlar şunlardır:

1. Resource Manager için kaynak grubu oluşturun
2. Uygulama ağ geçidi için sanal ağ, alt ağ ve genel IP oluşturun
3. Uygulama ağ geçidi yapılandırma nesnesi oluşturun
4. Bir uygulama ağ geçidi kaynağı oluşturma

## <a name="create-a-resource-group-for-resource-manager"></a>Resource Manager için kaynak grubu oluşturun

Azure Resource Manager cmdlet’lerini kullanmak için PowerShell modunu açtığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

### <a name="step-1"></a>1. Adım

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>2. Adım

Hesapla ilişkili abonelikleri kontrol edin.

```powershell
Get-AzureRmSubscription
```

Kimlik bilgilerinizle kimliğinizi doğrulamanız istenir.

### <a name="step-3"></a>3. Adım

Hangi Azure aboneliğinizin kullanılacağını seçin.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4. Adım

Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu ayar, kaynak grubundaki kaynaklar için varsayılan konum olarak kullanılır. Uygulama ağ geçidi oluşturmak için verilen komutların aynı kaynak grubunu kullandığından emin olun.

Yukarıdaki örnekte, **appgw-RG** adlı, **Batı ABD** konumlu bir kaynak grubu oluşturduk.

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Uygulama ağ geçidi için bir sanal ağ ve bir alt ağ oluşturun

Aşağıdaki örnek Resource Manager kullanarak nasıl sanal ağ oluşturulacağını gösterir:

### <a name="step-1"></a>1. Adım

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Bu örnek, 10.0.0.0/24 adres aralığını, sanal ağ oluşturmak için kullanılacak bir alt ağ değişkenine atar.

### <a name="step-2"></a>2. Adım

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

Bu örnek adlı bir sanal ağ oluşturur **appgwvnet** kaynak grubunda **appgw-rg** 10.0.0.0/24 alt ağıyla önek 10.0.0.0/16 kullanarak Batı ABD bölgesi için.

### <a name="step-3"></a>3. Adım

```powershell
$subnet = $vnet.Subnets[0]
```

Bu örnek, sonraki adımlar için alt ağ nesnesini bir $subnet değişkenine atar.

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Ön uç yapılandırma için genel bir IP adresi oluşturun

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Bu örnek bir genel IP kaynağı oluşturur **Publicıp01** kaynak grubunda **appgw-rg** Batı ABD bölgesi için.

## <a name="create-an-application-gateway-configuration-object"></a>Uygulama ağ geçidi yapılandırma nesnesi oluşturun

### <a name="step-1"></a>1. Adım

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Bu örnek adlı uygulama ağ geçidi IP yapılandırması oluşturur **Gatewayıp01**. Application Gateway başladığında, yapılandırılan alt ağdan bir IP adresi alır ve ağ trafiğini arka uç IP havuzundaki IP adreslerine yönlendirir. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

### <a name="step-2"></a>2. Adım

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Bu örnek adlı arka uç IP adresi havuzunu yapılandırır **pool01** IP adresleriyle **134.170.185.46**, **134.170.188.221**, **134.170.185.50**. Bu değerler, ön uç IP uç noktasından gelen ağ trafiğinin yönlendirildiği IP adresleridir. Önceki örnekte yazılan IP adreslerini, kendi web uygulaması uç noktalarınızla değiştirin.

### <a name="step-3"></a>3. Adım

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Bu örnek uygulama ağ geçidi ayarı yapılandırır **poolsetting01** arka uç havuzundaki yük dengeli ağ trafiği.

### <a name="step-4"></a>4. Adım

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Bu örnek adlı ön uç IP bağlantı noktasını yapılandırır **frontendport01** genel IP uç noktası için.

### <a name="step-5"></a>5. Adım

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Bu örnek, SSL bağlantısı için kullanılan sertifikayı yapılandırır. Sertifikanın .pfx formatında olması gerekir ve parola 4 ile 12 karakter arasında olmalıdır.

### <a name="step-6"></a>6. Adım

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

Bu örnek adlı ön uç IP yapılandırmasını oluşturur **fipconfig01** ve genel IP adresi ön uç IP yapılandırmasını ilişkilendirir.

### <a name="step-7"></a>7. Adım

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Bu örnek dinleyici adı oluşturur **listener01** ve ön uç bağlantı noktasıyla ön uç IP yapılandırmasını ve sertifikasını ilişkilendirir.

### <a name="step-8"></a>8. Adım

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Bu örnek adlı Yük Dengeleyiciyi yönlendirme kuralını oluşturur **rule01** yük dengeleyici davranışını yapılandırır.

### <a name="step-9"></a>9. Adım

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Bu örnek, uygulama ağ geçidinin örnek boyutunu yapılandırır.

> [!NOTE]
> *InstanceCount* için varsayılan değer 2 ile 10 arasıdır. *GatewaySize* için varsayılan değer Medium’dur. Aynı zamanda Standard_Small, Standard_Medium ve Standard_Large seçenekleri de bulunmaktadır.

### <a name="step-10"></a>10. adım

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Bu adım, uygulama ağ geçidinde kullanmak için SSL İlkesi tanımlar. Ziyaret [SSL yapılandırma İlkesi sürümlerini ve şifre paketleri uygulama ağ geçidi üzerinde](application-gateway-configure-ssl-policy-powershell.md) daha fazla bilgi için.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>New-AzureApplicationGateway kullanarak bir uygulama ağ geçidi oluşturma

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Bu örnek, önceki adımlarda geçen tüm yapılandırma öğeleri ile bir uygulama ağ geçidi oluşturur. Örnekte uygulama ağ geçidi olarak adlandırılır **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. Son kullanıcıların uygulama ağ geçidine ulaşmasını sağlamak için uygulama ağ geçidinin genel uç noktasını işaret edecek bir CNAME kaydı kullanılabilir. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). Bunu yapmak için uygulama ağ geçidinin ayrıntılarını ve onunla ilişkilendirilmiş olan IP/DNS adını uygulama ağ geçidine eklenmiş PublicIPAddress öğesini kullanarak alın. Uygulama ağ geçidinin DNS adı, iki web uygulamasını bu DNS adına götüren bir CNAME kaydı oluşturmak için kullanılmalıdır. Uygulama ağ geçidi yeniden başlatıldığında VIP değişebileceğinden A kaydı kullanımı önerilmez.


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

Bir uygulama ağ geçidini bir iç yük dengeleyici (ILB) ile kullanmak için yapılandırmak istiyorsanız, bkz. [İç yük dengeleyiciyle bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

