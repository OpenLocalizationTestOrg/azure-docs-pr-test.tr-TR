---
title: "URL yönlendirme kullanarak bir uygulama ağ geçidi kuralları aaaCreate | Microsoft Docs"
description: "Bu sayfa yönergeleri toocreate sağlar, URL yönlendirme kurallarını kullanarak bir Azure uygulama ağ geçidi yapılandırma"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Yol tabanlı yönlendirme kullanarak bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

URL yolu tabanlı yönlendirme hello URL yola bir Http isteğinin göre tooassociate yollar sağlar. Bu uygulama ağ geçidi hello sunulan hello URL için yapılandırılmış bir rota tooa arka uç havuzu olup olmadığını denetler. Ardından, arka uç havuzu hello ağ trafiği toohello tanımlanan gönderir. Farklı içerik türlerini toodifferent arka uç sunucu havuzu tooload bakiye istekleri URL tabanlı yönlendirme için ortak bir kullanılır.

URL tabanlı yönlendirme yeni bir kural türü tooapplication ağ geçidi sunar. Uygulama ağ geçidi sahip iki kural türleri: temel ve PathBasedRouting. Temel kural türü hello arka uç için hepsini hizmeti tooround bir kez deneme dağıtımı sırasında PathBasedRouting ayrıca havuzları, ayrıca hello arka uç havuzu seçerken hello istek URL'sinin yol deseni dikkate alır sağlar.

## <a name="scenario"></a>Senaryo

Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com için uygulama ağ geçidi hizmet: video sunucu havuzu ve görüntü sunucu havuzu.

Http://contoso.com/image * yönlendirilir tooimage sunucu havuzuna (pool1) ve http://contoso.com/video * yönlendirilir isteğinin toovideo sunucu havuzuna (pool2). Merhaba yolu desenleri hiçbiri eşleşirse, varsayılan sunucu havuzuna (pool1) seçilidir.

![URL rota](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Uygulama ağ geçidi için bir sanal ağ ve alt ağ oluşturun. Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun. Merhaba uygulama ağ geçidi tek başına bir sanal ağ alt ağında olmalıdır.
3. Merhaba sunucuları toohello arka uç havuzu toouse hello uygulama ağ geçidi mevcut olmalıdır veya uç noktaları hello sanal ağda veya atanan genel IP/VIP'ye ile oluşturduğunuz eklendi.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Gerekli toocreate bir uygulama ağ geçidi nedir?

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi. listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).
* **Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

Azure Klasik ve Azure Resource Manager kullanma arasındaki fark hello hello uygulama ağ geçidi ve yapılandırılmış toobe gereksinim hello öğelerini oluşturmak hello sırasıdır.

Resource Manager ile uygulama ağ geçidini oluşturan öğeler ayrı ayrı yapılandırılır ve toocreate hello uygulama ağ geçidi kaynağı bir araya getirin.

Gerekli toocreate bir uygulama ağ geçidi hello adımlar şunlardır:

1. Resource Manager için kaynak grubu oluşturun.
2. Bir sanal ağ, alt ağ ve hello uygulama ağ geçidi için genel IP oluşturun.
3. Uygulama ağ geçidi yapılandırma nesnesi oluşturun.
4. Uygulama ağ geçidi kaynağı oluşturun.

## <a name="create-a-resource-group-for-resource-manager"></a>Resource Manager için kaynak grubu oluşturun

Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

### <a name="step-1"></a>1. Adım

İçinde tooAzure oturum

```powershell
Login-AzureRmAccount
```

Kimlik bilgilerinizle istendiğinde tooauthenticate var.<BR>

### <a name="step-2"></a>2. Adım

Merhaba hesabının Hello abonelikleri kontrol edin.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>3. Adım

Azure abonelikleri toouse hangisinin seçin. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4. Adım

Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

Alternatif olarak, uygulama ağ geçidi için bir kaynak grubu için etiketler de oluşturabilirsiniz:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu kaynak grubu, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.

Merhaba yukarıdaki örnekte, "appgw-RG adlı" "Batı ABD" konumlu bir kaynak grubu oluşturduk.

> [!NOTE]
> Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md). Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma

örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ. Bu örnek hello uygulama ağ geçidi için bir sanal ağ oluşturur. Uygulama ağ geçidi hello uygulama ağ geçidi için oluşturulan hello alt VNET adres alanı hello küçük olan bu nedenle, kendi alt gerektirir. Bu da dahil olmak üzere için diğer kaynaklar sağlar ancak bunlarla sınırlı tooweb sunucuları toobe yapılandırılmış hello aynı sanal ağ.

### <a name="step-1"></a>1. Adım

Başlangıç adresi aralığı 10.0.0.0/24 toohello alt kullanılan değişken toobe toocreate bir sanal ağ atayın.  Bu uygulama ağ geçidi hello sonraki örnekte kullanılan hello için hello alt ağ yapılandırma nesnesi oluşturur.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>2. Adım

Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **appgw-rg** 10.0.0.0/24 alt ağıyla hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için. Bu hello VNET hello uygulama ağ geçidi tooreside için tek bir alt ağ ile Merhaba yapılandırmasını tamamlar.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>3. Adım

Sonraki adımlar hello için Hello alt ağ değişkeni atayın, bu toohello geçirilen `New-AzureRMApplicationGateway` bir sonraki adımda cmdlet'i.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Merhaba ön uç yapılandırma için genel bir IP adresi oluştur

Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için. Uygulama ağ geçidi genel bir IP adresi, iç IP adresi veya hem tooreceive istekleri Yük Dengeleme için kullanabilirsiniz.  Bu örnekte yalnızca genel IP adresi kullanılmaktadır. Aşağıdaki örnek hello, DNS adı yok hello genel IP adresi oluşturmak için yapılandırılır.  Application Gateway, genel IP adreslerinde özel DNS adlarını desteklemez.  Merhaba ortak uç nokta için özel bir adı gerekiyorsa, toopoint otomatik olarak oluşturulan toohello DNS adı hello ortak IP adresi için bir CNAME kaydı oluşturulmalıdır.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.

## <a name="create-application-gateway-configuration"></a>Uygulama ağ geçidi yapılandırmasını oluşturma

Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanması gerekir. Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.

### <a name="step-1"></a>1. Adım

**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun. Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>2. Adım

Adlı hello arka uç IP adresi havuzunu yapılandırmak **pool01** ve **pool2** için IP adresleriyle **pool1** ve **pool2**. Merhaba IP adreslerini hello uygulama ağ geçidi tarafından korunan hello web uygulama toobe barındırma hello kaynakların bu IP adresleridir. Temel araştırmalar veya özel araştırmalara olup bu arka uç havuzu tarafından araştırmalar sağlıklı tüm doğrulanmış toobe üyeleridir.  Trafik sonra yönlendirilir istekleri hello uygulama ağ geçidine geldiğinizde toothem. Arka uç havuzları, aynı hello üzerinde bulunan birden çok web uygulamaları için bir arka uç havuzu kullanılabilirdi anlamı hello uygulama ağ geçidi içinde birden çok kurallar tarafından kullanılabilir ana bilgisayar.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

Bu örnekte, iki arka uç havuzları tooroute ağ trafiğini hello URL yola göre vardır. Bir havuz "/video" URL yolundan trafiği alırken, diğer havuz "/image" yolundan trafiği alır. Kendi uygulama IP adresi bitiş IP adreslerini tooadd önceki hello değiştirin. 

### <a name="step-3"></a>3. Adım

Uygulama ağ geçidi ayarlarını yapılandırmanız **poolsetting01** ve **poolsetting02** hello yük dengeli ağ trafiği hello arka uç havuzundaki. Bu örnekte, hello arka uç havuzları farklı arka uç havuzu ayarlarını yapılandırın. Her bir arka uç havuzu kendi arka uç havuzu ayarlarına sahip olabilir.  Arka uç HTTP ayarları kuralları tooroute trafiği toohello doğru arka uç havuzu üyeleri tarafından kullanılır. Bu, hello protokolü ve trafik toohello arka uç havuzu üyeleri gönderirken kullanılan bağlantı noktası belirler. Tanımlama bilgisi tabanlı oturum de hello arka uç HTTP ayarları tarafından belirlenir.  Etkinleştirilirse, tanımlama bilgisi tabanlı oturum benzeşimi trafiği toohello gönderir aynı arka uç her paket için önceki istekleri olarak.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>4. Adım

Merhaba ön uç IP ile genel IP uç noktasını yapılandırın. Merhaba ön uç IP yapılandırma nesnesi tarafından dinleyici toorelate hello dışa doğru hello dinleyici IP adresiyle karşılıklı kullanılır.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>5. Adım

Merhaba, bir uygulama ağ geçidi için ön uç bağlantı noktasını yapılandırın. Merhaba ön uç bağlantı noktası yapılandırma nesnesi tarafından dinleyici toodefine ne hello dinleyicisi trafiğini hello uygulama ağ geçidi dinlediği bağlantı noktası kullanılır.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>6. Adım

Merhaba dinleyicisini yapılandırın. Bu adım hello dinleyici hello genel IP adresi için yapılandırır ve bağlantı noktası tooreceive gelen ağ trafiğini kullanılır. Aşağıdaki örneğine hello önceden yapılandırılmış hello ön uç IP yapılandırmasını, ön uç bağlantı noktası yapılandırması ve bir protokol (http veya https) alır ve hello dinleyicisi yapılandırır. Bu örnekte, hello dinleyici tooHTTP trafiği daha önce oluşturulan hello genel IP adresi üzerinde bağlantı noktası 80 üzerinde dinler.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>7. Adım

URL kuralı yolları hello arka uç havuzları için yapılandırın. Bu adım, uygulama ağ geçidi tarafından kullanılan hello göreli yolu yapılandırır ve hello URL yolu ile toohandle hello gelen trafiği atanan hello arka uç havuzu arasında hello eşleme tanımlar.

> [!IMPORTANT]
> Her bir yol ile başlamalıdır / ve hello yalnızca Yerleştir bir "\*" izin verilir, hello sonunda olur. Geçerli örnekler /xyz, /xyz* veya/xyz / *. Merhaba toohello yolu Eşleştirici sat dize herhangi bir metin hello sonra ilk içermiyor "?" veya "#" ve bu karakterleri izin verilmez. 

Merhaba aşağıdaki örnekte iki kural oluşturur: biri "/ Görüntü /" yol yönlendirme trafiği tooback uç "pool1" ve başka bir yönlendirme trafiği tooback uç "pool2." "/ video /" yolu için Bu kurallar, trafiği URL'leri her kümesi yönlendirilmiş toohello arka uç olduğundan emin olun. Örneğin, http://contoso.com/image/figure1.jpg toopool1 gider ve http://contoso.com/video/example.mp4 toopool2 geçer.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Merhaba yolu hello önceden tanımlanmış bir yol kurallardan herhangi birinin eşleşmiyorsa, hello kuralı yol haritası yapılandırmasını varsayılan arka uç adres havuzu da yapılandırır. Örneğin, hello eşleşmeyen trafiği için varsayılan havuzu olarak tanımlanan http://contoso.com/shoppingcart/test.html toopool1 gider.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>8. Adım

Bir kural ayarı oluşturun. Bu adım, hello uygulama ağ geçidi toouse URL yolu tabanlı yönlendirme yapılandırır. Merhaba `$urlPathMap` tanımlanan değişken hello önceki adımda şimdi kullanılan toocreate hello yol tabanlı kuralıdır. Bu adımda, biz hello kuralı bir dinleyici ve daha önce oluşturduğunuz hello url yolu eşlemesi ile ilişkilendirin.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>9. Adım

Merhaba sayısı örnekleri ve boyutu hello uygulama ağ geçidi için yapılandırın.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Uygulama ağ geçidi oluşturma

Merhaba adımları önceki tüm yapılandırma nesnelerden ile bir uygulama ağ geçidi oluşturun.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını alma

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken uygulama ağ geçidi için dinamik olarak atanan DNS adı gerekir ve bu durum çok kullanışlı değildir. hello uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello genel bir uç nokta hello uygulama ağ geçidi olabilir. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure hello ön uç IP CNAME kaydı ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress öğesi ekli toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır. kullanılan toocreate bir CNAME kaydı Hello uygulama ağ geçidi DNS adı olmalıdır. Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.

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

Güvenli Yuva Katmanı (SSL) yük boşaltma toolearn istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl-arm.md).

