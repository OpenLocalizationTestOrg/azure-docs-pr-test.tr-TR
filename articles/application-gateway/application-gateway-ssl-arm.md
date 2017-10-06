---
title: "aaaConfigure SSL boşaltma - Azure uygulama ağ geçidi - PowerShell | Microsoft Docs"
description: "Bu sayfa bir uygulama ağ geçidi ile SSL boşaltma Azure Kaynak Yöneticisi'ni kullanarak yönergeleri toocreate sağlar"
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
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Azure Resource Manager kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Klasik PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure uygulama ağ geçidi yapılandırılmış tooterminate hello Güvenli Yuva Katmanı (SSL) hello ağ geçidi tooavoid maliyetli SSL şifre çözme görevleri toohappen hello web grubu adresindeki oturumunda olabilir. SSL boşaltma ayrıca hello ön uç sunucusunun kurulumunu ve hello web uygulamasının yönetimini basitleştirir.

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturun. Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun. Application Gateway tek başına bir sanal ağ alt ağında olmalıdır.
3. toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya uç noktaları hello sanal ağda veya atanan genel IP/VIP'ye ile oluşturdunuz.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Gerekli toocreate bir uygulama ağ geçidi nedir?

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi. listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu ayarları büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).
* **Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler. Şu anda yalnızca hello *temel* kural desteklenmektedir. Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.

**Ek yapılandırma notları**

SSL sertifikaları yapılandırma, protokolünde hello **HttpListener** çok değiştirmelisiniz*Https* (büyük küçük harf duyarlı). Merhaba **SslCertificate** öğesi çok eklenen**HttpListener** hello SSL sertifikası için yapılandırılmış hello değişken değeri. Merhaba ön uç bağlantı noktası güncelleştirilmiş too443 olmalıdır.

**tooenable tanımlama bilgisi temelli benzeşimi**: bir uygulama ağ geçidi isteği bir istemci oturumundan her zaman yönlendirilmiş toohello olduğunu yapılandırılmış tooensure olabilir hello web grubundaki aynı VM. Bu senaryo, uygun şekilde hello ağ geçidi toodirect trafiğe izin veren bir oturum tanımlama bilgisi ekleme işlemi tarafından yapılır. tanımlama bilgisi temelli benzeşimi tooenable ayarlamak **CookieBasedAffinity** çok*etkin* hello içinde **BackendHttpSettings** öğesi.

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

hello Azure Klasik dağıtım modeli ve Azure Resource Manager kullanarak arasındaki farkı hello yapılandırılmış toobe gereken bir uygulama ağ geçidi ve hello öğeleri oluşturduğunuz hello sırasıdır.

Resource Manager ile uygulama ağ geçidi'nın tüm bileşenleri ayrı ayrı yapılandırılır ve sonra birlikte toocreate uygulama ağ geçidi kaynağı.

Bir uygulama ağ geçidi hello adımlar toocreate şunlardır:

1. Resource Manager için kaynak grubu oluşturun
2. Sanal ağ, alt ağ ve hello uygulama ağ geçidi için genel IP oluşturun
3. Uygulama ağ geçidi yapılandırma nesnesi oluşturun
4. Bir uygulama ağ geçidi kaynağı oluşturma

## <a name="create-a-resource-group-for-resource-manager"></a>Resource Manager için kaynak grubu oluşturun

PowerShell modu toouse hello Azure Resource Manager cmdlet'lerini geçtiğinizden emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

### <a name="step-1"></a>1. Adım

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>2. Adım

Merhaba hesabının Hello abonelikleri kontrol edin.

```powershell
Get-AzureRmSubscription
```

Kimlik bilgilerinizle istendiğinde tooauthenticate var.

### <a name="step-3"></a>3. Adım

Azure abonelikleri toouse hangisinin seçin.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4. Adım

Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu ayar, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Bir uygulama ağ geçidini kullanan tüm komutları toocreate Merhaba, aynı olduğundan emin olun kaynak grubu.

Adlı bir kaynak grubu oluşturduk Hello yukarıdaki örnekte, **appgw-RG** ve konum **Batı ABD**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma

örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ:

### <a name="step-1"></a>1. Adım

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Bu örnek, bir sanal ağ başlangıç adresi aralığı 10.0.0.0/24 tooa alt kullanılan değişken toobe toocreate atar.

### <a name="step-2"></a>2. Adım

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

Bu örnek adlı bir sanal ağ oluşturur **appgwvnet** kaynak grubunda **appgw-rg** 10.0.0.0/24 alt ağıyla hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için.

### <a name="step-3"></a>3. Adım

```powershell
$subnet = $vnet.Subnets[0]
```

Bu örnek hello sonraki adımlar için hello alt ağ nesnesini toovariable $subnet atar.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Merhaba ön uç yapılandırma için genel bir IP adresi oluştur

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Bu örnek bir genel IP kaynağı oluşturur **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için.

## <a name="create-an-application-gateway-configuration-object"></a>Uygulama ağ geçidi yapılandırma nesnesi oluşturun

### <a name="step-1"></a>1. Adım

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Bu örnek adlı uygulama ağ geçidi IP yapılandırması oluşturur **Gatewayıp01**. Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

### <a name="step-2"></a>2. Adım

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Bu örnek adlı hello arka uç IP adresi havuzunu yapılandırır **pool01** IP adresleriyle **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Bu değerleri hello ön uç IP uç noktasından gelen ağ trafiğini hello aldığınız hello IP adresleridir. Kendi web uygulama uç hello IP adresleriyle örneği önceki hello Hello IP adreslerini değiştirin.

### <a name="step-3"></a>3. Adım

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

Bu örnek uygulama ağ geçidi ayarı yapılandırır **poolsetting01** hello arka uç havuzundaki tooload dengeli ağ trafiği.

### <a name="step-4"></a>4. Adım

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Bu örnek adlı hello ön uç IP bağlantı noktasını yapılandırır **frontendport01** hello genel IP uç noktası için.

### <a name="step-5"></a>5. Adım

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Bu örnek, SSL bağlantısı için kullanılan hello sertifika yapılandırır. Merhaba sertifikanın .pfx biçiminde toobe gerekir ve hello parola 4 too12 karakter arasında olmalıdır.

### <a name="step-6"></a>6. Adım

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

Bu örnek hello adlı ön uç IP yapılandırmasını oluşturur **fipconfig01** ve ortak IP adresi hello ön uç IP yapılandırması ile ilişkilendirilmiş bir hello.

### <a name="step-7"></a>7. Adım

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Bu örnek hello dinleyici adı oluşturur **listener01** ve hello ön uç bağlantı noktası toohello ön uç IP yapılandırmasını ve sertifikasını ilişkilendirir.

### <a name="step-8"></a>8. Adım

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Bu örnek adlı hello Yük Dengeleyiciyi yönlendirme kuralını oluşturur **rule01** hello yük dengeleyici davranışını yapılandırır.

### <a name="step-9"></a>9. Adım

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Bu örnek hello uygulama ağ geçidi hello örnek boyutunu yapılandırır.

> [!NOTE]
> Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir. Merhaba için varsayılan değer *GatewaySize* Orta'dır. Aynı zamanda Standard_Small, Standard_Medium ve Standard_Large seçenekleri de bulunmaktadır.

### <a name="step-10"></a>10. adım

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Bu adım hello SSL İlkesi toouse hello uygulama ağ geçidinde tanımlar. Ziyaret [SSL yapılandırma İlkesi sürümlerini ve şifre paketleri uygulama ağ geçidi üzerinde](application-gateway-configure-ssl-policy-powershell.md) toolearn daha fazla.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>New-AzureApplicationGateway kullanarak bir uygulama ağ geçidi oluşturma

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Bu örnek hello adımları önceki tüm yapılandırma öğelerinden bir uygulama ağ geçidi oluşturur. Merhaba örnekte hello uygulama ağ geçidi olarak adlandırılır **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo Bu, alma ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adı. Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır. Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.


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

Bir iç yük dengeleyiciye (ILB) sahip bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

