---
title: "birden çok sitesi barındırmak için bir uygulama ağ geçidi aaaCreate | Microsoft Docs"
description: "Bu sayfa yönergeleri toocreate sağlar, hello birden çok web uygulamalarını barındırmak için bir Azure uygulama ağ geçidi aynı ağ geçidi."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Birden çok web uygulamalarını barındırmak için bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Birden çok siteyi barındıran bir web uygulaması'birden fazla toodeploy üzerinde hello sağlar aynı uygulama ağ geçidi. Ana bilgisayar üst bilgisi hello gelen HTTP isteği, hangi dinleyicisi trafiği alacağı toodetermine kullanır. Merhaba dinleyicisi sonra hello kuralları tanımı hello ağ geçidi içinde yapılandırıldığı gibi trafik tooappropriate arka uç havuzu yönlendirir. SSL etkin web uygulamaları, uygulama ağ geçidi hello sunucu adı göstergesi (SNI) uzantısı toochoose hello doğru dinleyicisi hello web trafiği için kullanır. Tooload bakiye istekleri farklı web etki alanları toodifferent arka uç sunucu havuzu için birden çok sitesi barındırmak için ortak bir kullanılır. Benzer şekilde aynı kök etki alanı üzerinde de barındırılabilecek hello birden çok alt etki alanları aynı uygulama ağ geçidi hello.

## <a name="scenario"></a>Senaryo

Aşağıdaki örneğine hello iki arka uç sunucu havuzu ile trafiği contoso.com ve fabrikam.com için uygulama ağ geçidi hizmet: contoso sunucu havuzu ve fabrikam sunucu havuzu. Benzer Kurulum app.contoso.com ve blog.contoso.com gibi kullanılan toohost alt etki alanları olabilir.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Merhaba sunucuları toohello arka uç havuzu toouse hello uygulama ağ geçidi mevcut olmalıdır veya uç noktaları da hello sanal ağda ayrı bir alt ağ veya atanan genel IP/VIP'ye oluşturduysanız eklendi.

## <a name="requirements"></a>Gereksinimler

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi. listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır. FQDN de kullanılabilir.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa). Çok siteli kullanan bir uygulama ağ geçitleri için ana bilgisayar adı ve SNI göstergeleri de eklenir.
* **Kural:** hello kural hello dinleyicisi, hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler. Kuralları listelendikleri hello sırada işlenir ve trafik belirginliğe bağımsız olarak eşleşen ilk kural hello aracılığıyla yönlendirilir. Temel bir dinleyici kullanan bir kural ve çok siteli dinleyicisi hem aynı bağlantı noktası, hello kuralla hello kullanarak bir kuralı varsa, örneğin, hello çok siteli dinleyicisi önce hello kural hello çok siteli kural toofunction sırayla hello temel dinleyicisiyle listelenmiş olması gerekir bekleniyordu.

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

Merhaba hello adımları toocreate bir uygulama ağ geçidi gerekli şunlardır:

1. Resource Manager için kaynak grubu oluşturun.
2. Bir sanal ağ, alt ağlar ve hello uygulama ağ geçidi için genel IP oluşturun.
3. Uygulama ağ geçidi yapılandırma nesnesi oluşturun.
4. Uygulama ağ geçidi kaynağı oluşturun.

## <a name="create-a-resource-group-for-resource-manager"></a>Resource Manager için kaynak grubu oluşturun

Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz. [Resource Manager ile Windows PowerShell kullanarak](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>1. Adım

İçinde tooAzure oturum

```powershell
Login-AzureRmAccount
```
Kimlik bilgilerinizle istendiğinde tooauthenticate var.

### <a name="step-2"></a>2. Adım

Merhaba hesabının Hello abonelikleri kontrol edin.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>3. Adım

Azure abonelikleri toouse hangisinin seçin.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>4. Adım

Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

Alternatif olarak, uygulama ağ geçidi için bir kaynak grubu için etiketler de oluşturabilirsiniz:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Tüm komutlar, toocreate bir uygulama ağ geçidi kullanım hello emin olun aynı kaynak grubu.

Adlı bir kaynak grubu oluşturduk Hello yukarıdaki örnekte, **appgw-RG** konumunu ile **Batı ABD**.

> [!NOTE]
> Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md). Ziyaret [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) daha fazla bilgi için.

## <a name="create-a-virtual-network-and-subnets"></a>Bir sanal ağ ve alt ağlar oluşturun

örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ. Bu adımda iki alt ağ oluşturulur. Merhaba ilk alt hello uygulama ağ geçidi için kendisini değil. Uygulama ağ geçidi, kendi alt toohold örneklerini gerektirir. Bu alt ağda yalnızca başka uygulama ağ geçitleri dağıtılabilir. Merhaba ikinci alt kullanılan toohold hello uygulama arka uç sunucuları değil.

### <a name="step-1"></a>1. Adım

Başlangıç adresi aralığı 10.0.0.0/24 toohello alt değişken toobe kullanılan toohold hello uygulama ağ geçidi atayın.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>2. Adım

Başlangıç adresi aralığı 10.0.1.0/24 toohello Altağ2 değişken toobe Hello arka uç havuzları için kullanılan atayın.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>3. Adım

Adlı bir sanal ağ oluşturma **appgwvnet** kaynak grubunda **appgw-rg** hello önek 10.0.0.0/16 10.0.0.0/24 alt ağıyla hello Batı ABD bölgesi için kullanarak ve 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>4. Adım

Bir uygulama ağ geçidi oluşturur hello sonraki adımlar için bir alt ağ değişkeni atayın.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Merhaba ön uç yapılandırma için genel bir IP adresi oluştur

Genel IP kaynağı oluşturun **Publicıp01** kaynak grubunda **appgw-rg** hello Batı ABD bölgesi için.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Merhaba hizmeti başladığında toohello uygulama ağ geçidi bir IP adresi atanır.

## <a name="create-application-gateway-configuration"></a>Uygulama ağ geçidi yapılandırmasını oluşturma

Merhaba uygulama ağ geçidi oluşturmadan önce tüm yapılandırma öğeleri yukarı tooset sahip. Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.

### <a name="step-1"></a>1. Adım

**gatewayIP01** adlı bir uygulama ağ geçidi IP yapılandırması oluşturun. Application gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>2. Adım

Adlı hello arka uç IP adresi havuzunu yapılandırmak **pool01** ve **pool2** IP adresleriyle **134.170.185.46**, **134.170.188.221**, **134.170.185.50** için **pool1** ve **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  için **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

Bu örnekte, iki arka uç havuzları tooroute ağ trafiğini hello istenen sitesinde dayalı vardır. Bir havuz "contoso.com" sitesinden trafiği alır ve diğer havuzu "fabrikam.com" sitesinden trafiği alır. Kendi uygulama IP adresi bitiş IP adreslerini tooadd önceki tooreplace hello var. İç IP adresleri yerine, arka uç örnekleri için genel IP adresleri, FQDN veya bir sanal makinenin NIC de kullanabilirsiniz. PowerShell kullanımda toospecify FQDN'ler IP'leri yerine "-BackendFQDNs" parametresi.

### <a name="step-3"></a>3. Adım

Uygulama ağ geçidi ayarlarını yapılandırmanız **poolsetting01** ve **poolsetting02** hello yük dengeli ağ trafiği hello arka uç havuzundaki. Bu örnekte, hello arka uç havuzları farklı arka uç havuzu ayarlarını yapılandırın. Her bir arka uç havuzu kendi arka uç havuzu ayarlarına sahip olabilir.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>4. Adım

Merhaba ön uç IP ile genel IP uç noktasını yapılandırın.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>5. Adım

Merhaba, bir uygulama ağ geçidi için ön uç bağlantı noktasını yapılandırın.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>6. Adım

İki SSL sertifikalarını yapılandırmak için hello iki Web siteleri Biz bu örnekte toosupport adımıdır. Bir sertifika contoso.com trafiği için ve diğer hello fabrikam.com trafiği için. Bu sertifikalar, Web siteleri için sertifikalar bir sertifika yetkilisi olması gerekir. Otomatik olarak imzalanan sertifikalar desteklenir, ancak üretim trafiği için önerilmez.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>7. Adım

Bu örnekte, iki dinleyicileri hello iki web sitesi için yapılandırın. Ortak IP adresi, bağlantı noktası ve ana bilgisayar tooreceive gelen trafiği kullanılan için bu adımı hello dinleyicileri yapılandırır. Ana bilgisayar adı parametresi, çoklu site desteği için gereklidir ve hangi Merhaba trafiğinin alınıp kümesi toohello uygun Web sitesi olmalıdır. Requireservernameındication parametresi birden çok ana senaryo için SSL desteklenmesi gereken Web siteleri için tootrue ayarlanmalıdır. SSL desteği gerekiyorsa, toospecify hello SSL ayrıca gereken sertifika, web uygulaması için kullanılan toosecure trafiği. Frontendıpconfiguration, FrontendPort ve ana bilgisayar adı Hello birleşimi benzersiz tooa dinleyicisi olmalıdır. Her dinleyicisi bir sertifikayı destekleyebilir.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>8. Adım

Bu örnekte, iki web uygulamaları için Hello ayarlama iki kural oluşturun. Bir kural dinleyicileri, arka uç havuzları ve http ayarları birbirine bağlar. Bu adım hello uygulama ağ geçidi toouse temel yönlendirme kuralı, her Web sitesi için bir tane yapılandırır. Trafiği tooeach Web sitesi, yapılandırılmış bir dinleyici tarafından alınır ve ardından tooits hello BackendHttpSettings belirtilen hello özelliklerini kullanarak arka uç havuzu yapılandırılmış yönlendirilir.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>9. Adım

Merhaba sayısı örnekleri ve boyutu hello uygulama ağ geçidi için yapılandırın.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Uygulama ağ geçidi oluşturma

Merhaba adımları önceki tüm yapılandırma nesnelerden ile bir uygulama ağ geçidi oluşturun.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Uygulama ağ geçidi sağlama, uzun süreli bir işlemdir ve bazı zaman toocomplete sürebilir.
> 
> 

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

Bilgi nasıl tooprotect ile Web siteleri [uygulama ağ geçidi - Web uygulaması güvenlik duvarı](application-gateway-webapplicationfirewall-overview.md)

