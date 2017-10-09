---
title: "aaaConfigure son tooend SSL Azure uygulama ağ geçidi ile | Microsoft Docs"
description: "Bu makalede nasıl tooconfigure sona tooend SSL Azure Resource Manager PowerShell kullanarak uygulama ağ geçidi ile açıklanır"
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
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Uygulama ağ geçidi PowerShell kullanarak ile son tooend SSL yapılandırma

## <a name="overview"></a>Genel Bakış

Uygulama ağ geçidi destekler tooend şifreleme trafik sonlandırın. Uygulama ağ geçidi bunu hello uygulama ağ geçidi hello SSL bağlantısını sonlandırarak yapar. Hello ağ geçidi sonra toohello trafiği hello paket yeniden şifreler ve tanımlanan hello yönlendirme kurallarına göre hello paket toohello uygun arka uç iletir hello yönlendirme kuralları uygular. Merhaba web sunucusundan herhangi bir yanıt hello gider aynı işlemi geri toohello son kullanıcı.

Başka bir özellik, bu uygulama ağ geçidi özel SSL seçenekleri tanımlama destekler. Uygulama Ağ Geçidi Protokolü sürüm aşağıdaki devre dışı bırakma hello destekler; **TLSv1.0**, **TLSv1.1**, ve **TLSv1.2** de şifre paketleri toouse ve hello tercih sırasına göre hello tanımlama.  yapılandırılabilir SSL seçenekleri hakkında daha fazla toolearn ziyaret [SSL ilkesine genel bakış](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 ve SSL 3.0 varsayılan olarak devre dışıdır ve etkinleştirilemez. Bunlar Güvensiz olarak kabul edilir ve uygulama ağ geçidi ile kullanılan mümkün toobe değildir.

![Senaryo görüntüsü][scenario]

## <a name="scenario"></a>Senaryo

Bu senaryoda, nasıl kullanarak bir uygulama ağ geçidi toocreate sona tooend SSL öğrenin PowerShell kullanarak.

Bu senaryo aşağıdakileri yapar:

* Adlı bir kaynak grubu oluşturmak **appgw-rg**
* Adlı bir sanal ağ oluşturma **appgwvnet** 10.0.0.0/16 bir adres alanı ile.
* Adlı iki alt ağ oluşturmak **appgwsubnet** ve **appsubnet**.
* Bir küçük uygulama ağ geçidi destek bitiş tooend SSL şifrelemesi bu sınırları SSL protokolleri sürümlerini ve şifre paketleri oluşturun.

## <a name="before-you-begin"></a>Başlamadan önce

bir uygulama ağ geçidi ile tooconfigure son tooend SSL, bir sertifika hello ağ geçidi için gereklidir ve sertifikaları hello arka uç sunucuları için gereklidir. SSL ile kullanılan tooencrypt ve şifre çözme hello gönderilen trafiğin tooit Hello ağ geçidi sertifikasıdır. Merhaba ağ geçidi sertifikası kişisel bilgi değişimi (pfx) biçiminde toobe gerekir. Bu dosya biçimi, hangi hello uygulama ağ geçidi tooperform hello şifreleme ve şifre çözme trafik tarafından gerekli anahtar toobe dışarı Merhaba özel sağlar.

End tooend SSL şifreleme hello arka uç uygulama ağ geçidi ile Güvenilenler listesine olması gerekir. Bu, hello arka uçlarını toohello uygulama ağ geçidi hello ortak sertifikasını karşıya yükleyerek gerçekleştirilir. Bu, o hello uygulama ağ geçidi yalnızca bilinen arka uç örnekleri ile iletişim kurar sağlar. Bu daha fazla hello son tooend iletişimin güvenliğini sağlar.

Bu işlem aşağıdaki adımları hello açıklanmıştır:

## <a name="create-hello-resource-group"></a>Merhaba kaynak grubu oluştur

Bu bölümde hello uygulama ağ geçidi içeren bir kaynak grubu oluşturmada size yol gösterir.

### <a name="step-1"></a>1. Adım

Tooyour Azure hesabı oturum açın.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>2. Adım

Bu senaryo için Hello abonelik toouse seçin.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>3. Adım

Bir kaynak grubu oluşturun (mevcut bir kaynak grubu kullanıyorsanız bu adımı atlayın).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Bir sanal ağ ve hello uygulama ağ geçidi için bir alt ağ oluşturma

Merhaba aşağıdaki örnek bir sanal ağ ve iki alt ağı oluşturur. Bir alt ağda kullanılan toohold hello uygulama ağ geçidi ' dir. Merhaba diğer alt hello arka uçlarını barındırma hello web uygulaması için kullanılır.

### <a name="step-1"></a>1. Adım

Merhaba alt hello uygulama ağ geçidi kendisi için kullanılması için bir adres aralığı atayın.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Uygulama ağ geçidi için yapılandırılmış alt ağlar doğru boyutta olması. Bir uygulama ağ geçidi too10 örneği için yapılandırılabilir. Her bir örnek hello alt ağdan bir IP adresi alır. Çok küçük bir alt ağın, bir uygulama ağ geçidi ölçeklendirme olumsuz yönde etkileyebilir.
> 
> 

### <a name="step-2"></a>2. Adım

Merhaba arka uç adres havuzu için kullanılan bir adres aralığı toobe atayın.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>3. Adım

Önceki adımları hello tanımlanan hello alt ağlar ile bir sanal ağ oluşturun.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>4. Adım

Aşağıdaki adımları hello kullanılan hello sanal ağ kaynak ve alt ağ kaynakları toobe Al:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Merhaba ön uç yapılandırma için genel bir IP adresi oluştur

Merhaba uygulama ağ geçidi için kullanılan bir ortak IP kaynak toobe oluşturun. Bu genel IP adresi kullanılır aşağıdaki adımı.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Uygulama ağ geçidi hello tanımlı bir etki alanı etiketi ile oluşturulan bir ortak IP adresi kullanımını desteklemez. Yalnızca bir ortak IP adresi dinamik olarak oluşturulan etki alanı etiketi ile desteklenir. Merhaba uygulama ağ geçidi için bir kolay dns adı gerekiyorsa, önerilen toouse bir CNAME kaydı bir diğer ad olarak.

## <a name="create-an-application-gateway-configuration-object"></a>Uygulama ağ geçidi yapılandırma nesnesi oluşturun

Tüm yapılandırma öğeleri hello uygulama ağ geçidi oluşturmadan önce ayarlanır. Merhaba aşağıdaki adımları hello uygulama ağ geçidi kaynağı için gerekli olan yapılandırma öğeleri oluşturun.

### <a name="step-1"></a>1. Adım

Uygulama ağ geçidi IP yapılandırması oluşturun, bu ayarı, hangi alt hello uygulama ağ geçidi kullanan yapılandırır. Application gateway başladığında, yapılandırılan hello alt ağdan bir IP adresi seçer ve ağ trafiğini toohello IP adreslerini hello arka uç IP havuzundaki yönlendirir. Her örneğin bir IP adresi aldığını göz önünde bulundurun.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>2. Adım

Bu ayar hello uygulama ağ geçidi bir özel veya genel IP adresi toohello ön ucu eşlemeleri, ön uç IP yapılandırmasını oluşturun. adımı aşağıdaki hello hello ön uç IP yapılandırmasını adımıyla önceki hello hello genel IP adresi ilişkilendirir.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>3. Adım

Merhaba arka uç IP adresi havuzu ile Merhaba arka uç web sunucularının hello IP adreslerini yapılandırın. Bu IP adreslerine hello ön uç IP uç noktasından gelen ağ trafiğini hello aldığınız hello IP adresleridir. Kendi uygulama IP adresi bitiş IP adreslerini tooadd aşağıdaki hello değiştirin.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Bir tam etki alanı adı (FQDN) da geçerli bir değer hello arka uç sunucuları için bir IP adresi yerine hello - BackendFqdns anahtar kullanmaktır. 

### <a name="step-4"></a>4. Adım

Merhaba ön uç IP bağlantı noktası hello genel IP uç noktası için yapılandırın. Bu bağlantı noktası, son kullanıcılara bağlanan hello bağlantı noktasıdır.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>5. Adım

Merhaba hello uygulama ağ geçidi için yapılandırın. Bu sertifika kullanılan toodecrypt ve hello uygulama ağ geçidi üzerinde hello trafiğini yeniden şifreleyin.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Bu örnek, SSL bağlantısı için kullanılan hello sertifika yapılandırır. Merhaba sertifikanın .pfx biçiminde toobe gerekir ve hello parola 4 too12 karakter arasında olmalıdır.

### <a name="step-6"></a>6. Adım

Merhaba HTTP dinleyicisi hello uygulama ağ geçidi için oluşturun. Merhaba ön uç IP yapılandırması, bağlantı noktası ve SSL sertifika toouse atayın.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>7. Adım

Arka uç havuzu kaynaklarına SSL Hello üzerinde kullanılan toobe etkin hello sertifikasını yükleyin.

> [!NOTE]
> Merhaba varsayılan araştırmasını alır hello ortak anahtar hello **varsayılan** SSL bağlaması hello arka uç bilgisayarın IP adresi ve toohello ortak anahtar değeri burada aldığı karşılaştırır hello ortak anahtar değeri. Merhaba alınan ortak anahtar mutlaka hedeflenen hello site toowhich trafik akışına olabilir **varsa** ana bilgisayar üstbilgilerinin ve SNI hello arka uçta kullanma. Emin değilseniz, hangi sertifikanın hello için kullanılan hello arka uçları tooconfirm https://127.0.0.1/ ziyaret **varsayılan** SSL bağlaması. Bu bölümde bu istek Hello ortak anahtar kullanın. Ana bilgisayar üstbilgilerinin ve SNI HTTPS bağlantılarına kullanıyorsanız ve, yanıt ve sertifikayı el ile tarayıcı istek toohttps://127.0.0.1/ hello arka ucunda alırsınız olmayan bir varsayılan SSL bağlaması hello arka ucunda ayarlamanız gerekir. Bunu yaparsanız, araştırmalar başarısız ve hello arka uç izin verilenler listesinde değil.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> Bu adımda sağlanan hello sertifika hello ortak anahtarı hello pfx sertifika hello arka uç üzerinde mevcut olmalıdır. Merhaba arka uç sunucusunda yüklü hello sertifika (Merhaba kök sertifikanın değil) verin. CER biçimlendirin ve bu adımda kullanın. Bu adım whitelists hello uygulama ağ geçidi ile arka uç hello.

### <a name="step-8"></a>8. Adım

Merhaba uygulama ağ geçidi arka uç http ayarları yapılandırın. Adım toohello http ayarları önceki hello karşıya hello sertifika atayın.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>9. Adım

Merhaba yük dengeleyici davranışını yapılandıran Yük Dengeleyiciyi yönlendirme kuralını oluşturun. Bu örnekte, bir temel hepsini bir kural oluşturulur.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>10. adım

Merhaba uygulama ağ geçidi Hello örnek boyutunu yapılandırın.  Merhaba kullanılabilir boyutları: **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**.  Kapasite için 1 ile 10 hello değerleri kullanılabilir.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Test amacıyla örnek sayısını 1 seçilebilir. Herhangi bir örneğine altında iki örnek sayısı tooknow hello tarafından SLA kapsamında değildir ve bu nedenle önerilmez önemlidir. Küçük ağ geçitleri geliştirme test ve üretim amaçları için kullanılan toobe ' dir.

### <a name="step-11"></a>11. adım

Uygulama ağ geçidi Hello üzerinde kullanılan hello SSL İlkesi toobe yapılandırın. Uygulama ağ geçidi hello özelliği tooset en düşük sürüm SSL protokol sürümleri için destekler.

Merhaba aşağıdaki değerleri tanımlanabilir protokol sürümleri listesi verilmiştir.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Ayarlar hello en düşük protokol sürümü çok**TLSv1_2** ve sağlar **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**ve **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** yalnızca.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Merhaba uygulama ağ geçidi oluşturma

Adımları önceki tüm hello kullanarak hello uygulama ağ geçidi oluşturun. Merhaba ağ geçidi Hello oluşturulmasını uzun süren bir işlemdir.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Mevcut bir uygulama ağ geçidi SSL protokolü sürümlerinde sınırla

Merhaba önceki son tooend SSL ile uygulama oluşturma ve belirli SSL protokol sürümleri devre dışı bırakma adımlar. Merhaba aşağıdaki örnekte belirli SSL ilkeleri var olan bir uygulama ağ geçidi üzerinde devre dışı bırakır.

### <a name="step-1"></a>1. Adım

Merhaba uygulama ağ geçidi tooupdate alın.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>2. Adım

SSL ilke tanımlayın. Merhaba, aşağıdaki örneğine TLSv1.0 ve TLSv1.1 devre dışı bırakılır ve şifre paketleri hello **TLS\_ECDHE\_ECDSA\_ile\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_ile\_AES\_256\_GCM\_SHA384**, ve  **TLS\_RSA\_ile\_AES\_128\_GCM\_SHA256** hello izin yalnızca olanlardır.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>3. Adım

Son olarak, hello ağ geçidini güncelleştirin. Önemli toonote bu son adım uzun çalışan bir görev olduğundan emin olur. Tamamlandığında, son tooend SSL hello uygulama ağ geçidinde yapılandırılır.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Web uygulamalarınızın uygulama ağ geçidi üzerinden Web uygulaması güvenlik duvarı ile Merhaba güvenlik ziyaret ederek artırma hakkında bilgi edinin [Web uygulaması güvenlik duvarı genel bakış](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
