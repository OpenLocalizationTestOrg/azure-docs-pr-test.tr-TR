---
title: "İç yük dengeleyici - PowerShell ile Azure uygulama ağ geçidi aaaUsing | Microsoft Docs"
description: "Bu sayfa toocreate, yapılandırmak, başlatmak ve Azure Resource Manager için iç yük dengeleyiciye (ILB) sahip bir Azure uygulama ağ geçidi silme yönergelerini sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Azure Resource Manager kullanarak iç yük dengeleyiciye (ILB) sahip bir uygulama ağ geçidi oluşturma

> [!div class="op_single_selector"]
> * [Azure Klasik PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

Azure uygulama ağ geçidi, bir Internet'e yönelik VIP veya gösterilen toohello Internet, olarak da bilinen bir iç yük dengeleyiciye (ILB) uç noktası olmayan iç uç nokta ile yapılandırılabilir. Yapılandırma hello ağ geçidini bir ILB ile sunulan toohello Internet olmayan iç iş kolu satır uygulamaları için kullanışlıdır. Ayrıca Hizmetleri için faydalı olur ve dağıtım, oturum sürekliliği veya Güvenli Yuva Katmanı (SSL) sonlandırma gösterilen toohello Internet olmayan bir güvenlik sınırı içinde sunulmamış ancak hala hepsini gerektiren çok katmanlı bir uygulama içinde katmanları yükleyin.

Bu makalede, hello adımları tooconfigure bir uygulama ağ geçidini bir ILB ile adım adım anlatılmaktadır.

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Application Gateway için bir sanal ağ ve bir alt ağ oluşturacaksınız. Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun. Application Gateway tek başına bir sanal ağ alt ağında olmalıdır.
3. toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Gerekli toocreate bir uygulama ağ geçidi nedir?

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi. Merhaba listede IP adresleri ya da toohello sanal ağ ait olması gerekir, ancak hello uygulama ağ geçidi için farklı bir alt ağ veya genel IP/VIP'ye olmalıdır.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bunlar büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).
* **Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler. Şu anda yalnızca hello *temel* kural desteklenmektedir. Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

Azure Klasik ve Azure Resource Manager kullanma arasındaki fark hello hello uygulama ağ geçidi ve yapılandırılmış toobe gereksinim hello öğelerini oluşturmak hello sırasıdır.
Resource Manager ile uygulama ağ geçidini oluşturan öğeler ayrı ayrı yapılandırılır ve toocreate hello uygulama ağ geçidi kaynağı bir araya getirin.

Gerekli toocreate bir uygulama ağ geçidi hello adımlar şunlardır:

1. Resource Manager için kaynak grubu oluşturun
2. Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma
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

Yeni bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Bir uygulama ağ geçidini kullanan tüm komutları toocreate Merhaba, aynı olduğundan emin olun kaynak grubu.

Örnek önceki hello "Appgw-rg" ve konum "Batı ABD" konumlu bir kaynak grubu oluşturduk.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma

örnekte gösterildiği nasıl aşağıdaki hello toocreate Kaynak Yöneticisi'ni kullanarak bir sanal ağ:

### <a name="step-1"></a>1. Adım

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Bu adım, bir sanal ağ başlangıç adresi aralığı 10.0.0.0/24 tooa alt kullanılan değişken toobe toocreate atar.

### <a name="step-2"></a>2. Adım

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Bu adım, "appgw-rg" kaynak grubunda 10.0.0.0/24 alt ağıyla hello önek 10.0.0.0/16 kullanarak hello Batı ABD bölgesi için "appgwvnet" adlı bir sanal ağ oluşturur.

### <a name="step-3"></a>3. Adım

```powershell
$subnet = $vnet.subnets[0]
```

Bu adım hello sonraki adımlar için hello alt ağ nesnesini toovariable $subnet atar.

## <a name="create-an-application-gateway-configuration-object"></a>Uygulama ağ geçidi yapılandırma nesnesi oluşturun

### <a name="step-1"></a>1. Adım

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Bu adım, "Gatewayıp01" adlı uygulama ağ geçidi IP yapılandırması oluşturur. Application Gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki rota. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

### <a name="step-2"></a>2. Adım

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Bu adım adlı hello arka uç IP adresi havuzunu yapılandırır "pool01" IP adresleri "10.1.1.8, 10.1.1.9, 10.1.1.10". Bu hello ön uç IP uç noktasından gelen ağ trafiğini hello aldığınız hello IP adresleridir. Kendi uygulama IP adresi bitiş IP adreslerini tooadd önceki hello değiştirin.

### <a name="step-3"></a>3. Adım

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Bu adım, uygulama "dengeli poolsetting01" ağ geçidi hello yük için ağ trafiğini hello arka uç havuzundaki yapılandırır.

### <a name="step-4"></a>4. Adım

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Bu adım hello ILB için "frontendport01" adlı hello ön uç IP bağlantı noktasını yapılandırır.

### <a name="step-5"></a>5. Adım

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Bu adım hello "fipconfig01" adlı ön uç IP yapılandırmasını oluşturur ve hello geçerli sanal ağ alt ağından özel IP ile ilişkilendirir.

### <a name="step-6"></a>6. Adım

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Bu adım, "listener01" adlı hello dinleyiciyi oluşturur ve hello ön uç bağlantı noktası toohello ön uç IP yapılandırmasını ilişkilendirir.

### <a name="step-7"></a>7. Adım

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Bu adım hello Yük Dengeleyiciyi yönlendirme kuralını hello yük dengeleyici davranışını yapılandıran "rule01" adlı oluşturur.

### <a name="step-8"></a>8. Adım

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Bu adım hello uygulama ağ geçidi hello örnek boyutunu yapılandırır.

> [!NOTE]
> Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir. Merhaba için varsayılan değer *GatewaySize* Orta'dır. Aynı zamanda Standard_Small, Standard_Medium ve Standard_Large seçenekleri de bulunmaktadır.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>New-AzureApplicationGateway kullanarak bir uygulama ağ geçidi oluşturma

Merhaba adımları önceki tüm yapılandırma öğelerinden bir uygulama ağ geçidi oluşturur. Bu örnekte, hello uygulama ağ geçidi "appgwtest" olarak adlandırılmıştır.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Bu adım, önceki adımları hello tüm yapılandırma öğelerinden bir uygulama ağ geçidi oluşturur. Merhaba örnekte hello uygulama ağ geçidi "appgwtest" olarak adlandırılmıştır.

## <a name="delete-an-application-gateway"></a>Uygulama ağ geçidini silme

bir uygulama ağ geçidi toodelete, aşağıdaki adımları sırayla toodo hello gerekir:

1. Kullanım hello `Stop-AzureRmApplicationGateway` cmdlet toostop hello ağ geçidi.
2. Kullanım hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello ağ geçidi.
3. Bu hello ağ geçidi hello kullanarak kaldırıldı doğrulayın `Get-AzureApplicationGateway` cmdlet'i.

### <a name="step-1"></a>1. Adım

Merhaba uygulama ağ geçidi nesnesini alın ve tooa değişkeni "$getgw" ilişkilendirebilirsiniz.

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>2. Adım

Kullanım `Stop-AzureRmApplicationGateway` toostop hello uygulama ağ geçidi. Bu örnek hello gösterir `Stop-AzureRmApplicationGateway` cmdlet hello ilk satırdaki ardından tarafından hello çıktı.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Merhaba uygulama ağ geçidi durdurulmuş durumda olduğunda, hello kullan `Remove-AzureRmApplicationGateway` cmdlet tooremove hello hizmet.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Merhaba **-force** anahtar kullanılan toosuppress hello kaldırma onayı iletisini olabilir.

Hizmet hello tooverify kaldırıldı, hello kullanabilirsiniz `Get-AzureRmApplicationGateway` cmdlet'i. Bu adım gerekli değildir.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Sonraki adımlar

SSL boşaltma tooconfigure istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).

Bir uygulama ağ geçidi toouse bir ILB ile tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

