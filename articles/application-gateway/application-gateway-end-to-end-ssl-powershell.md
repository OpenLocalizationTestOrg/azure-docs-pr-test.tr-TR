---
title: "Azure uygulama ağ geçidi ile uçtan uca SSL'yi yapılandırma | Microsoft Docs"
description: "Bu makalede uçtan uca SSL uygulama ağ geçidi kullanarak Azure Resource Manager PowerShell ile nasıl yapılandırılacağı açıklanmaktadır"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 6d969d6a0c649c263e1d5bb99bdbceec484cb9a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-end-to-end-ssl-with-application-gateway-using-powershell"></a>Uygulama ağ geçidi PowerShell kullanarak ile uçtan uca SSL yapılandırma

## <a name="overview"></a>Genel Bakış

Uygulama ağ geçidi uçtan uca şifreleme trafiği destekler. Application Gateway bu işlemi uygulama ağ geçidindeki SSL bağlantısını sonlandırarak yapar. Ağ geçidi bundan sonra yönlendirme kurallarını trafiğe uygular, paketi yeniden şifreler ve tanımlanan yönlendirme kurallarına göre paketi uygun arka uca iletir. Web sunucusundan alınan herhangi bir yanıt, son kullanıcıya dönerken aynı süreci izler.

Başka bir özellik, bu uygulama ağ geçidi özel SSL seçenekleri tanımlama destekler. Uygulama ağ geçidi, aşağıdaki iletişim kuralı sürüm devre dışı bırakma destekler; **TLSv1.0**, **TLSv1.1**, ve **TLSv1.2** iyi tanımlayıcı olarak hangi şifre paketleri ve tercih sırasına göre.  Yapılandırılabilir SSL seçenekler hakkında daha fazla bilgi için [SSL ilkesine genel bakış](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 ve SSL 3.0 varsayılan olarak devre dışıdır ve etkinleştirilemez. Bunlar Güvensiz olarak kabul edilir ve uygulama ağ geçidi ile kullanılması mümkün değildir.

![Senaryo görüntüsü][scenario]

## <a name="scenario"></a>Senaryo

Bu senaryoda, PowerShell kullanarak uçtan uca SSL kullanan bir uygulama ağ geçidi oluşturmayı öğrenin.

Bu senaryo aşağıdakileri yapar:

* Adlı bir kaynak grubu oluşturmak **appgw-rg**
* Adlı bir sanal ağ oluşturma **appgwvnet** 10.0.0.0/16 bir adres alanı ile.
* Adlı iki alt ağ oluşturmak **appgwsubnet** ve **appsubnet**.
* Uçtan uca SSL şifrelemesini destekleyen bir küçük uygulama ağ geçidi, o sınırlar SSL protokolleri sürümlerini ve şifre paketleri oluşturun.

## <a name="before-you-begin"></a>Başlamadan önce

Bir uygulama ağ geçidi ile uçtan uca SSL'yi yapılandırmak için bir sertifika ağ geçidi için gereklidir ve sertifikaları arka uç sunucuları için gereklidir. Ağ geçidi sertifikası şifrelemek ve SSL ile gönderilen trafiğin şifresini çözmek için kullanılır. Ağ geçidi sertifikası kişisel bilgi değişimi (pfx) biçiminde olması gerekir. Bu dosya biçimi, uygulama ağ geçidi tarafından şifreleme ve şifre çözme trafik gerçekleştirmek için gereken özel anahtar verilebilsin sağlar.

Uçtan uca SSL şifrelemesi için arka uç uygulama ağ geçidi ile güvenilir listesinde olması gerekir. Bu uygulama ağ geçidi arka uçlarını ortak sertifikasını karşıya yükleyerek gerçekleştirilir. Bu uygulama ağ geçidi ile bilinen arka uç örnekleri yalnızca iletişim kurar sağlar. Bu ek uçtan uca iletişimin güvenliğini sağlar.

Bu işlem aşağıdaki adımlarda açıklanmaktadır:

## <a name="create-the-resource-group"></a>Kaynak grubu oluştur

Bu bölümde uygulama ağ geçidi içeren bir kaynak grubu oluşturmada size yol gösterir.

### <a name="step-1"></a>1. Adım

Azure hesabınızda oturum açın.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>2. Adım

Bu senaryo için kullanılacak aboneliği seçin.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>3. Adım

Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Uygulama ağ geçidi için bir sanal ağ ve bir alt ağ oluşturun

Aşağıdaki örnek, bir sanal ağ ve iki alt ağı oluşturur. Bir alt ağ, uygulama ağ geçidi tutmak için kullanılır. Diğer alt web uygulamasını barındıran arka uçlarını için kullanılır.

### <a name="step-1"></a>1. Adım

Alt ağ uygulama ağ geçidi için kendisini kullanılması için bir adres aralığı atayın.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Uygulama ağ geçidi için yapılandırılmış alt ağlar doğru boyutta olması. Bir uygulama ağ geçidi için en fazla 10 örneğini yapılandırılabilir. Her örneğin bir IP adresi alt ağdan alır. Çok küçük bir alt ağın, bir uygulama ağ geçidi ölçeklendirme olumsuz yönde etkileyebilir.
> 
> 

### <a name="step-2"></a>2. Adım

Arka uç adres havuzu için kullanılacak bir adres aralığı atayın.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>3. Adım

Önceki adımlarda tanımlanan alt ağları ile bir sanal ağ oluşturun.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>4. Adım

Aşağıdaki adımlarda kullanılacak alt ağ kaynaklarının ve sanal ağ kaynak Al:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Ön uç yapılandırma için genel bir IP adresi oluşturun

Uygulama ağ geçidi için kullanılacak genel bir IP kaynağı oluşturun. Bu genel IP adresi kullanılır aşağıdaki adımı.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Uygulama ağ geçidi, tanımlı bir etki alanı etiketi ile oluşturulan bir ortak IP adresi kullanımını desteklemiyor. Yalnızca bir ortak IP adresi dinamik olarak oluşturulan etki alanı etiketi ile desteklenir. Uygulama ağ geçidi için bir kolay dns adı gerekiyorsa, bir CNAME kaydı bir diğer ad olarak kullanmak için önerilir.

## <a name="create-an-application-gateway-configuration-object"></a>Uygulama ağ geçidi yapılandırma nesnesi oluşturun

Tüm yapılandırma öğeleri, uygulama ağ geçidi oluşturmadan önce ayarlanır. Aşağıdaki adımlar uygulama ağ geçidi kaynağı için gerekli yapılandırma öğelerini oluşturur.

### <a name="step-1"></a>1. Adım

Uygulama ağ geçidi IP yapılandırması oluşturun, bu ayarı, uygulama ağ geçidini kullanır hangi alt yapılandırır. Uygulama ağ geçidi başladığında, yapılandırılan alt ağdan bir IP adresi seçer ve arka uç IP havuzundaki IP adresleri için ağ trafiğini yönlendirir. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>2. Adım

Bir ön uç IP yapılandırmasını oluşturur, bu ayar, uygulama ağ geçidi ön ucu bir özel veya genel IP adresi eşler. Aşağıdaki adım önceki adımda genel IP adresi ön uç IP yapılandırmasını ilişkilendirir.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>3. Adım

Arka uç IP adresi havuzu ile arka uç web sunucularının IP adreslerini yapılandırın. Bu IP adresleri ön uç IP uç noktasından gelen ağ trafiğinin yönlendirildiği IP adresleridir. Kendi uygulama IP adresi uç noktalarını eklemek için aşağıdaki IP adreslerini değiştirin.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Bir tam etki alanı adı (FQDN) aynı zamanda arka uç sunucuları için bir IP adresi yerine geçerli bir değer - BackendFqdns anahtar kullanmaktır. 

### <a name="step-4"></a>4. Adım

Genel IP uç noktası için ön uç IP bağlantı noktası yapılandırın. Bu bağlantı noktası, son kullanıcılara bağlanan bağlantı noktasıdır.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>5. Adım

Uygulama ağ geçidi için sertifika yapılandırın. Bu sertifika, uygulama ağ geçidi trafiğinde yeniden şifrelemek ve şifresini çözmek için kullanılır.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Bu örnek, SSL bağlantısı için kullanılan sertifikayı yapılandırır. Sertifikanın .pfx formatında olması gerekir ve parola 4 ile 12 karakter arasında olmalıdır.

### <a name="step-6"></a>6. Adım

HTTP dinleyicisi için uygulama ağ geçidi oluşturun. Ön uç IP yapılandırması, bağlantı noktası ve kullanmak için SSL sertifikası atayın.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>7. Adım

SSL etkin arka uç havuzu kaynaklardaki kullanılan sertifikayı karşıya yükleyin.

> [!NOTE]
> Ortak anahtarı ile varsayılan araştırmasını alır **varsayılan** SSL bağlaması arka uç bilgisayarın IP adresi ve aldığı ortak anahtar değeri, ortak anahtar değeri sağlamak burada karşılaştırır. Alınan ortak anahtar hangi trafik akışları hedeflenen siteye mutlaka olmayabilir **varsa** ana bilgisayar üstbilgilerinin ve SNI uç kullanma. Emin değilseniz, hangi sertifika için kullanılan onaylamak için arka uç https://127.0.0.1/ ziyaret **varsayılan** SSL bağlaması. Bu bölümde bu istek ortak anahtarı kullanın. Ana bilgisayar üstbilgilerinin ve SNI HTTPS bağlantılarına kullanıyorsanız ve bir yanıt ve sertifika el ile tarayıcı isteğinden arka ucunda https://127.0.0.1/ için aldığınız olmayan bir varsayılan SSL bağlaması arka ucunda ayarlamanız gerekir. Bunu yaparsanız, araştırmalar başarısız ve arka uç izin verilenler listesinde değil.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> Bu adımda sağlanan sertifikanın arka uç mevcut pfx sertifika ortak anahtarı olması gerekir. Arka uç sunucuda yüklü sertifikayı (kök sertifikanın değil) verin. CER biçimlendirin ve bu adımda kullanın. Bu adım whitelists arka uç uygulama ağ geçidi ile.

### <a name="step-8"></a>8. Adım

Uygulama ağ geçidi arka uç http ayarları yapılandırın. Http ayarları için önceki adımda yüklediğiniz sertifikayı atayın.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>9. Adım

Yük Dengeleyici davranışını yapılandıran Yük Dengeleyiciyi yönlendirme kuralını oluşturun. Bu örnekte, bir temel hepsini bir kural oluşturulur.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>10. adım

Uygulama ağ geçidinin örnek boyutunu yapılandırın.  Kullanılabilir boyutları: **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**.  Kapasite için 1 ile 10 değerleri kullanılabilir.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Test amacıyla örnek sayısını 1 seçilebilir. Tüm örnek sayısı iki örneği altında SLA kapsamında değildir ve bu nedenle önerilmez bilmeniz önemlidir. Küçük ağ geçitleri geliştirme test ve üretim amaçları için kullanılacak olan.

### <a name="step-11"></a>11. adım

Uygulama ağ geçidinde kullanılacak SSL ilkesini yapılandırın. Uygulama ağ geçidi SSL protokol sürümleri için en düşük sürüm ayarlama özelliği destekler.

Aşağıdaki değerleri tanımlanabilir protokol sürümleri listesi verilmiştir.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

En düşük protokol sürümü ayarlar **TLSv1_2** ve sağlar **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_SHA256**, **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**ve  **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** yalnızca.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-the-application-gateway"></a>Uygulama ağ geçidi oluşturma

Yukarıdaki adımları kullanarak uygulama ağ geçidi oluşturun. Ağ geçidi oluşturma uzun süren bir işlemdir.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Mevcut bir uygulama ağ geçidi SSL protokolü sürümlerinde sınırla

Önceki adımlar, uçtan uca SSL ile uygulama oluşturma ve belirli SSL protokol sürümleri devre dışı bırakma uygulayın. Aşağıdaki örnekte belirli SSL ilkeleri var olan bir uygulama ağ geçidi üzerinde devre dışı bırakır.

### <a name="step-1"></a>1. Adım

Uygulama ağ geçidi güncelleştirilecek alın.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>2. Adım

SSL ilke tanımlayın. Aşağıdaki örnekte, TLSv1.0 ve TLSv1.1 devre dışı bırakıldı ve şifre paketleri olduğundan **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**, ve  **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** olan izin verilen yalnızca bu çalışanların.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>3. Adım

Son olarak, ağ geçidini güncelleştirin. Bu son adım uzun çalışan bir görev olduğunu dikkate almak önemlidir. Tamamlandığında, uçtan uca SSL uygulama ağ geçidinde yapılandırılır.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Uygulama ağ geçidi üzerinden Web uygulaması güvenlik duvarı ile web uygulamalarınızın güvenliğini ziyaret ederek artırma hakkında bilgi edinin [Web uygulaması güvenlik duvarı genel bakış](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
