---
title: "Sanal ağ uygulama ağ geçidi ile Azure API Management'te aaaHow toouse | Microsoft Docs"
description: "Bilgi nasıl toosetup ve iç sanal ağ ile uygulama ağ geçidi (WAF) ön uç olarak Azure API Management yapılandırın"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Bir iç sanal ağ API Management'te uygulama ağ geçidi ile tümleştirme 

##<a name="overview"></a> Genel bakış
 
Merhaba API Management hizmeti, bir sanal ağdaki hello sanal ağ içinde yalnızca erişilebilir kılan iç modunda yapılandırılabilir. Azure uygulama ağ geçidi bir katman 7 yük dengeleyici sağlayan bir PAAS hizmetidir. Ters proxy hizmeti davranır ve onun bir Web uygulaması Güvenlik Duvarı (WAF) sunan arasında sağlar.

API Management hello uygulama ağ geçidi ön uç ile dahili bir VNET içinde sağlanan birleştirme senaryoları aşağıdaki hello sağlar:

* Kullanım hello aynı API Management kaynak tüketimi hem iç tüketiciler hem de dış tüketiciler tarafından.
* Bir alt kümesini API'leri dış Tüketiciler için kullanılabilir API Management tanımladığınız ve tek bir API Management kaynağı kullanın.
* Bir anahtar teslim yolu tooswitch erişim tooAPI yönetim hello gelen sağlayan genel Internet'ı kapatabilirsiniz. 

##<a name="scenario"></a> Senaryosu
Bu makalede nasıl toouse tek bir API Management hizmet için hem iç hem de dış tüketicileri kapsar ve her iki şirket içi için tek bir ön uç görevi görür ve bulut API'leri yapın. Ayrıca görürsünüz nasıl tooexpose Apı'lerinizi (örnekte yeşil vurgulanmış bunlar hello) yalnızca bir kısmı dış uygulama ağ geçidi mevcut hello PathBasedRouting işlevselliğini kullanarak tüketimi için.

Merhaba ilk kurulum örnekte tüm API'leri yalnızca sanal ağınızın içinde yönetilir. İç tüketicileri (vurgulanmış turuncu) tüm iç ve dış API'leri erişebilir. Trafik, yüksek performanslı teslim tooInternet Expressroute bağlantı hatları hiçbir zaman gider.

![URL rota](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a> Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Bir sanal ağ oluşturma ve API Management ve uygulama ağ geçidi için ayrı alt ağlar oluşturun. 
3. Toocreate hello sanal ağ için özel bir DNS sunucusu düşünüyorsanız, hello dağıtıma başlamadan önce bunu. Hello sanal ağ içinde yeni bir alt ağ içinde oluşturulmuş bir sanal makinenin sağlayarak çalıştığını kontrol edin, çözümlemek ve tüm Azure hizmet uç noktalarına erişebilirsiniz.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>Gerekli toocreate API Management ile uygulama ağ geçidi arasında bir tümleştirme nedir?

* **Arka uç sunucusu havuzu:** hello iç sanal IP adresini hello API Management hizmeti budur.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar, hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** bu hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bunu basarsa trafiği yeniden yönlendirilen tooone Merhaba, arka uç sunucuları alır.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).
* **Kural:** hello kuralı bir dinleyici tooa arka uç sunucusu havuzunu bağlar.
* **Özel durum araştırması:** uygulama ağ geçidi, varsayılan olarak, hangi sunucuların hello içinde kullanıma BackendAddressPool etkin IP adreslerini göre araştırmalar toofigure kullanır. Merhaba API Management hizmeti yalnızca hello doğru ana bilgisayar üstbilgisi olan toorequests yanıtlar, bu nedenle hello varsayılan araştırmalar başarısız. Bir özel durum araştırması tanımlanan toobe gereken toohelp uygulama ağ geçidi hello hizmetidir canlı ve isteklerini iletmek belirler.
* **Özel etki alanı sertifikası:** tooaccess API Management hello gelen Internet toocreate CNAME eşlemesi kendi ana bilgisayar adı toohello uygulama ağ geçidi ön uç DNS adı gerekiyor. Bu hello ana bilgisayar üstbilgisi ve gönderilen sertifikayı tooApplication tooAPI iletilen ağ geçidi yönetim bir APIM geçerli olarak tanıyabilmesi olmasını sağlar.

## <a name="overview-steps"></a> API Management ve uygulama ağ geçidi tümleştirmek için gerekli adımları 

1. Resource Manager için kaynak grubu oluşturun.
2. Bir sanal ağ, alt ağ ve hello uygulama ağ geçidi için genel IP oluşturun. API yönetimi için başka bir alt ağ oluşturun.
3. Yukarıda oluşturduğunuz hello sanal alt içinde bir API Management hizmeti oluşturma ve hello iç modu kullandığınızdan emin olun.
4. Merhaba API Management hizmeti Hello özel etki alanı adı ayarlayın.
5. Bir uygulama ağ geçidi yapılandırma nesnesi oluşturun.
6. Bir uygulama ağ geçidi kaynağı oluşturun.
7. Merhaba Genel DNS adından hello uygulama ağ geçidi toohello API Management proxy ana bilgisayar adı bir CNAME oluşturun.

## <a name="create-a-resource-group-for-resource-manager"></a>Resource Manager için kaynak grubu oluşturun

Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

### <a name="step-1"></a>1. Adım

İçinde tooAzure oturum

```powershell
Login-AzureRmAccount
```

Kimlik bilgilerinizle kimlik doğrulaması.<BR>

### <a name="step-2"></a>2. Adım

Merhaba hesabının Hello abonelikleri kontrol edin ve seçin.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>3. Adım

Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma

Aşağıdaki örnek hello Kaynak Yöneticisi'ni kullanarak bir sanal ağ toocreate hello nasıl gösterir.

### <a name="step-1"></a>1. Adım

Başlangıç adresi aralığı 10.0.0.0/24 toohello alt değişken toobe uygulama ağ geçidi için bir sanal ağ oluşturulurken kullanılan atayın.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>2. Adım

Başlangıç adresi aralığı 10.0.1.0/24 toohello alt değişken toobe API yönetimi için bir sanal ağ oluşturulurken kullanılan atayın.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>3. Adım

Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **apim-appGw-RG** hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için 10.0.0.0/24 alt ağları ve 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>4. Adım

Merhaba sonraki adımlar için bir alt ağ değişkeni atayın

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>İç modunda yapılandırılmış bir sanal ağ içinde bir API Management hizmeti oluşturma

Merhaba aşağıdaki örnekte toocreate bir VNET içindeki bir API Management hizmeti yalnızca iç erişim için nasıl yapılandırılacağı gösterilmektedir.

### <a name="step-1"></a>1. Adım
Merhaba alt yukarıda oluşturduğunuz $apimsubnetdata kullanarak bir API Yönetim sanal ağ nesnesi oluşturun.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>2. Adım
Merhaba sanal ağ içinde bir API Management hizmeti oluşturun.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Merhaba komutu yukarıda başarılı olduktan sonra çok başvurmak[DNS yapılandırma gerekli tooaccess iç VNET API Management hizmeti](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess onu.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Kurulum API Management'te özel etki alanı adı

### <a name="step-1"></a>1. Adım
Merhaba etki alanı için özel anahtara sahip Hello sertifikasını yükleyin. Bu örnek için olacak `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>2. Adım
Merhaba sertifika yüklendikten sonra bir ana bilgisayar adını ile Merhaba proxy için bir ana bilgisayar yapılandırma nesnesi oluşturun `api.contoso.net`hello örnek sertifika yetkilisi Merhaba sağlar gibi `*.contoso.net` etki alanı. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Merhaba ön uç yapılandırma için genel bir IP adresi oluştur

Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **apim-appGw-RG** hello Batı ABD bölgesi için.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.

## <a name="create-application-gateway-configuration"></a>Uygulama ağ geçidi yapılandırmasını oluşturma

Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanması gerekir. Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.

### <a name="step-1"></a>1. Adım

**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun. Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>2. Adım

Merhaba ön uç IP bağlantı noktası hello genel IP uç noktası için yapılandırın. Bu bağlantı noktası, son kullanıcılara bağlanan hello bağlantı noktasıdır.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>3. Adım

Merhaba ön uç IP ile genel IP uç noktasını yapılandırın.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>4. Adım

Merhaba uygulama ağ geçidi, kullanılan için toodecrypt hello sertifikası yapılandırın ve komut zincirinden geçen hello trafiğini yeniden şifreleyin.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>5. Adım

Merhaba HTTP dinleyicisi hello uygulama ağ geçidi için oluşturun. Merhaba ön uç IP yapılandırmasını, bağlantı noktası ve ssl sertifika tooit atayın.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>6. Adım

Özel araştırma toohello API Management hizmeti oluşturma `ContosoApi` proxy etki alanı uç noktası. Merhaba yolu `/status-0123456789abcdef` olan tüm hello API Management services üzerinde barındırılan bir varsayılan durumu uç noktası. Ayarlama `api.contoso.net` özel araştırma hostname toosecure olarak SSL sertifikası ile.

> [!NOTE]
> ana bilgisayar adı hello `contosoapi.azure-api.net` adlı bir hizmetin hello varsayılan proxy ana bilgisayar adı yapılandırılır `contosoapi` ortak Azure içinde oluşturulur. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>7. Adım

Merhaba SSL etkin arka uç havuzu kaynaklardaki toobe kullanılan hello sertifikasını yükleyin. Merhaba budur yukarıdaki adım 4'te sağlanan aynı sertifika.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>8. Adım

Merhaba uygulama ağ geçidi için HTTP arka uç ayarlarını yapılandırın. Bu, daha sonra iptal arka uç istek için zaman aşımı sınırı ayarı içerir. Bu değer hello yoklama zaman aşımı farklıdır.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>9. Adım

Adlı bir arka uç IP adresi havuzu yapılandırmak **apimbackend** hello iç sanal IP'ye sahip yukarıda hello API Management hizmeti, bir adres oluşturdu.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>10. adım

Bir kukla (mevcut olmayan) arka uç ayarlarını oluşturun. İstek tooAPI yollarını biz tooexpose API Management uygulama ağ geçidi aracılığıyla istemiyorsanız bu arka uç isabet ve 404 döndürür.

Merhaba kukla arka uç HTTP ayarları yapılandırın.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Sahte bir arka uç yapılandırma **dummyBackendPool**, tooa FQDN adresi işaret **dummybackend.com**. Bu FQDN adresi hello sanal ağında yok.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Uygulama ağ geçidi toohello mevcut olmayan arka uç noktaları varsayılan olarak kullanacağı bu hello ayarını bir kural oluşturmak **dummybackend.com** hello sanal ağ içinde.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>11. adım

URL kuralı yolları hello arka uç havuzları için yapılandırın. Bu, bazı olması için API Management API'lerinin hello toohello genel kullanıma sunulan yalnızca seçerek sağlar. Örneğin, varsa `Echo API` (/ Yankı /) `Calculator API` (/calc/) vb. yapma yalnızca `Echo API` Internet'ten erişilebilir). 

Merhaba aşağıdaki örnek hello "/ Yankı /" yol yönlendirme trafiği toohello arka uç "apimProxyBackendPool" için basit bir kural oluşturur.

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

API Management, yol haritası yapılandırması da adlı bir varsayılan arka uç adres havuzu yapılandırır hello kural tooenable istiyoruz hello yolu Hello yolu eşleşmiyorsa kuralları **dummyBackendPool**. Örneğin, çok http://api.contoso.net/calc/ * gider**dummyBackendPool** beklemediğiniz eşleşen trafiği için varsayılan havuzu hello olarak tanımlanan.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Yukarıdaki adımı Hello sağlar hello yolu yalnızca istekleri "/ echo" Merhaba uygulama ağ geçidi izin verilir. API Management API'leri yapılandırılmış istekleri tooother 404 hataları uygulama Internet hello erişildiğinde ağ geçidi durum oluşturur. 

### <a name="step-12"></a>12. adımı

Merhaba uygulama ağ geçidi toouse URL yolu tabanlı yönlendirme kuralı ayarı oluşturun.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>13. adım

Merhaba sayısı örnekleri ve boyutu hello uygulama ağ geçidi için yapılandırın. Merhaba burada kullanıyoruz [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) hello API Management kaynak güvenliği artırmak için.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>14. adım

WAF toobe "Önleme" modunda yapılandırın.
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Uygulama ağ geçidi oluşturma

Merhaba yapılandırma adımları önceki hello alt nesnelerden ile bir uygulama ağ geçidi oluşturun.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME hello API Management proxy ana bilgisayar adı toohello Genel DNS adını hello uygulama ağ geçidi kaynağı

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken, uygulama ağ geçidi kolay toouse olmayabilir dinamik olarak atanmış bir DNS adı gerektirir. 

Merhaba uygulama ağ geçidi DNS adı kullanılan toocreate hello APIM proxy ana bilgisayar adını gösteren bir CNAME kaydı olmalıdır (ör `api.contoso.net` yukarıdaki hello örneklerde) toothis DNS adı. tooconfigure hello ön uç IP CNAME kaydı hello uygulama ağ geçidi hello ayrıntılarını ve hello Publicıpaddress öğesi kullanarak ilişkili IP/DNS adını alır. ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a> Özeti
Azure API Management sanal ağ içinde yapılandırılmış bir tek ağ geçidi arabirimi barındırılan şirket içi olup olmadıklarını hello bulutta tüm yapılandırılmış API'ler sağlar. Uygulama ağ geçidi API Management ile tümleştirme sağlayan bir Web uygulaması güvenlik duvarı bir ön uç tooyour API Management örneği olarak yanı sıra belirli API'leri toobe hello Internet üzerinde erişilebilir seçmeli olarak etkinleştirme hello esnekliğini sağlar.

##<a name="next-steps"></a> Sonraki adımlar
* Azure uygulama ağ geçidi hakkında daha fazla bilgi edinin
  * [Uygulama ağ geçidi'ne genel bakış](../application-gateway/application-gateway-introduction.md)
  * [Uygulama ağ geçidi Web uygulaması güvenlik duvarı](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Yol tabanlı yönlendirme kullanarak uygulama ağ geçidi](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* API Management ve sanal ağlar hakkında daha fazla bilgi edinin
  * [API Management hello içinde yalnızca VNET kullanılabilir kullanma](api-management-using-with-internal-vnet.md)
  * [VNET içinde API Management kullanma](api-management-using-with-vnet.md)
