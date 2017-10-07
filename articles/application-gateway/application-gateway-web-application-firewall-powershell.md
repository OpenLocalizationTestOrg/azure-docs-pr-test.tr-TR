---
title: "aaaConfigure web uygulaması güvenlik duvarı - Azure uygulama ağ geçidi | Microsoft Docs"
description: "Bu makalede, nasıl toostart kullanarak izin ver web uygulaması Güvenlik Duvarı'nı varolan veya yeni uygulama ağ geçidi hakkında yönergeleri sunar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi üzerinde yapılandırma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

Uygulama ağ geçidi mevcut web uygulaması güvenlik duvarı tooan ekleyin veya nasıl uygulama ağ geçidi toocreate bir web uygulaması Güvenlik Duvarı etkin öğrenin.

Hello web uygulaması Güvenlik Duvarı (WAF) Azure uygulama ağ geçidi, web uygulamaları, SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini korur.

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar. Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar. toofind desteklenen özelliklerin tam bir listesi ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).

Merhaba aşağıdaki makalede nasıl çok gösterilmektedir[uygulama ağ geçidi mevcut web uygulaması güvenlik duvarı tooan ekleme](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan uygulama ağ geçidi oluşturma](#create-an-application-gateway-with-web-application-firewall).

![Senaryo görüntüsü][scenario]

## <a name="waf-configuration-differences"></a>WAF yapılandırma farklılıkları

Okuma [PowerShell ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-arm.md), bir uygulama ağ geçidi oluştururken hello SKU ayarları tooconfigure anlayın. WAF ek ayarlar toodefine hello SKU üzerinde bir uygulama ağ geçidini yapılandırırken sağlar. Uygulama ağ geçidi kendisini hello üzerinde yaptığınız ek değişiklik yoktur.

| **Ayar** | **Ayrıntılar**
|---|---|
|**SKU** |WAF destekler olmadan normal bir uygulama ağ geçidi **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları. WAF Hello başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**. WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.|
|**Katmanı** | Merhaba kullanılabilir değerler **standart** veya **WAF**. Web uygulaması güvenlik duvarı, kullanırken **WAF** seçilmelidir.|
|**Modu** | Bu ayar, WAF, hello modudur. izin verilen değerler **algılama** ve **önleme**. WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır. Önleme modda olayları yine kaydedilir ancak hello saldırgan 403 yetkisiz yanıt hello uygulama ağ geçidi ' alır.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Uygulama ağ geçidi mevcut web uygulaması güvenlik duvarı tooan Ekle

Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

1. Tooyour Azure hesabı oturum açın.

    ```powershell
    Login-AzureRmAccount
    ```

2. Bu senaryo için Hello abonelik toouse seçin.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Web uygulaması Güvenlik Duvarı'na eklediğiniz hello ağ geçidi alın.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Merhaba web uygulaması güvenlik duvarı sku yapılandırın. Merhaba kullanılabilir boyutları: **WAF\_büyük** ve **WAF\_orta**. Web uygulaması güvenlik duvarı kullanıldığında hello katmanı olmalıdır **WAF**, hello kapasite gerekir onaylanıp hello sku ayarlarken.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Merhaba WAF ayarları aşağıdaki örneğine hello tanımlandığı şekilde yapılandırın:

   İçin **FirewallMode**, önleme ve algılama hello değerleri kullanılabilir.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Adım önceki hello tanımlanan hello ayarları ile Merhaba uygulama ağ geçidini güncelleştirin.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Bu komut hello uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir. Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) toounderstand tooview uygulama ağ geçidiniz için nasıl günlüğe kaydeder. Güvenlik yapısı toohello WAF, günlükleri gerek toobe toounderstand hello güvenlik yaklaşımı, web uygulamalarınızı, düzenli olarak gözden.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma

Merhaba aşağıdaki adımları hello tüm web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturmak için başlangıç tooend işleminden değerli.

Hello Azure PowerShell'in en son sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

1. İçinde tooAzure çalıştırarak oturum `Login-AzureRmAccount`, kimlik bilgilerinizle istendiğinde tooauthenticate olduğunuz.

1. Çalıştırarak hello hesabının Hello abonelikleri kontrol edin`Get-AzureRmSubscription`

1. Azure abonelikleri toouse hangisinin seçin.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Merhaba uygulama ağ geçidi için bir kaynak grubu oluşturun.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu konum, kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Bir uygulama ağ geçidi toocreate kullanan tüm komutları ile aynı kaynak grubunda hello emin olun.

Örnek önceki hello "Appgw-RG" ve konum "Batı ABD." adlı bir kaynak grubu oluşturduk

> [!NOTE]
> Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md). Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.

### <a name="configure-virtual-network"></a>Sanal ağ yapılandırma

Uygulama ağ geçidi alt ağı için kendi gerektirir. Bu adımda, bir sanal ağ adres alanı 10.0.0.0/16 ve iki alt ağ, hello uygulama ağ geçidi için bir tane ve arka uç havuzu üyeleri için bir tane oluşturun.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Genel IP adresi yapılandırın

Sipariş toohandle dış isteklerinde, uygulama ağ geçidi genel bir IP adresi gerektirir. Bu genel IP adresi değil olmalıdır bir `DomainNameLabel` hello uygulama ağ geçidi tarafından kullanılan toobe tanımlanmış.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Merhaba uygulama ağ geçidi yapılandırma

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Merhaba temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını Al

Merhaba ağ geçidi oluşturulduktan sonra hello sonraki tooconfigure hello ön uç iletişimi için adımdır. Genel IP kullanırken, uygulama ağ geçidi kolay olmayan dinamik olarak atanmış bir DNS adı gerektirir. Merhaba uygulama ağ geçidi isabet tooensure son kullanıcılar, bir CNAME kaydı kullanılan toopoint toohello ortak uç noktasını hello uygulama ağ geçidi olabilir. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure bir diğer ad ayrıntılarını hello uygulama ağ geçidi ve hello Publicıpaddress bağlı öğesi toohello uygulama ağ geçidi kullanarak ilişkili IP/DNS adını alır. Merhaba uygulama ağ geçidi'nin DNS adı kullanılan toocreate bir CNAME kaydı hangi noktaları hello iki web uygulamaları toothis DNS adı olmalıdır. Uygulama ağ geçidi başlatmada Hello VIP değişebileceği A kayıtlarını hello kullanımı önerilmez.

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

Bilgi nasıl tooconfigure tanılama günlük kaydını, algılanan veya web uygulaması güvenlik duvarı ile ziyaret ederek engelledi toolog hello olayları [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
