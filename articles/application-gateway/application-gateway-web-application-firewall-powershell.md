---
title: "Web uygulaması güvenlik duvarı - Azure uygulama ağ geçidi yapılandırma | Microsoft Docs"
description: "Bu makalede bir mevcut veya yeni uygulama ağ geçidi üzerinde web uygulaması Güvenlik Duvarı'nı kullanmaya başlamak hakkında yönergeler açıklanmaktadır."
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Web uygulaması güvenlik duvarı bir yeni veya var olan uygulama ağ geçidi üzerinde yapılandırma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

Bir web uygulaması oluşturmayı öğrenin Güvenlik Duvarı etkin uygulama ağ geçidi veya var olan bir uygulama ağ geçidi için web uygulaması güvenlik duvarı ekleyin.

Azure uygulama ağ geçidi, web uygulaması Güvenlik Duvarı (WAF), SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini web uygulamaları korur.

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Bulutta veya şirket içinde olmalarından bağımsız olarak, farklı sunucular arasında yük devretme ile HTTP istekleri için performans amaçlı yönlendirme sağlar. Uygulama ağ geçidi HTTP dahil olmak üzere pek çok uygulama teslim denetleyici (ADC) özelliklerini Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) yük boşaltma, özel sistem durumu araştırmalarının, çoklu site desteği ve diğer birçok sağlar. Desteklenen özelliklerin tam listesi için ziyaret edin: [genel bakış, uygulama ağ geçidi](application-gateway-introduction.md).

Aşağıdaki makale gösterir nasıl [var olan bir uygulama ağ geçidi için web uygulaması güvenlik duvarı ekleme](#add-web-application-firewall-to-an-existing-application-gateway) ve [web uygulaması Güvenlik Duvarı'nı kullanan uygulama ağ geçidi oluşturma](#create-an-application-gateway-with-web-application-firewall).

![Senaryo görüntüsü][scenario]

## <a name="waf-configuration-differences"></a>WAF yapılandırma farklılıkları

Okuma [PowerShell ile bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-arm.md), bir uygulama ağ geçidi oluştururken yapılandırmak için SKU ayarları anlayın. WAF SKU üzerinde bir uygulama ağ geçidini yapılandırırken tanımlamak için ek ayarlar sağlar. Uygulama ağ geçidinde kendisini oluşturan ek değişiklik yoktur.

| **Ayar** | **Ayrıntılar**
|---|---|
|**SKU** |WAF destekler olmadan normal bir uygulama ağ geçidi **standart\_küçük**, **standart\_orta**, ve **standart\_büyük**boyutları. WAF başlanmasıyla, iki ek SKU vardır **WAF\_orta** ve **WAF\_büyük**. WAF küçük uygulama ağ geçitleri üzerinde desteklenmiyor.|
|**Katmanı** | Kullanılabilir değerler **standart** veya **WAF**. Web uygulaması güvenlik duvarı, kullanırken **WAF** seçilmelidir.|
|**Modu** | Bu ayar WAF modudur. izin verilen değerler **algılama** ve **önleme**. WAF algılama modunda ayarlandığında, tüm tehditler bir günlük dosyasında depolanır. Önleme modda olayları yine kaydedilir ancak saldırgan 403 yetkisiz yanıt uygulama ağ geçidi'nden alır.|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web uygulaması güvenlik duvarı için var olan bir uygulama ağ geçidi Ekle

Azure PowerShell’in en yeni sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

1. Azure hesabınızda oturum açın.

    ```powershell
    Login-AzureRmAccount
    ```

2. Bu senaryo için kullanılacak aboneliği seçin.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Web uygulaması Güvenlik Duvarı'nda eklemekte olduğunuz ağ geçidi alın.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Web uygulaması güvenlik duvarı sku yapılandırın. Kullanılabilir boyutları: **WAF\_büyük** ve **WAF\_orta**. Web uygulaması güvenlik duvarı kullanıldığında katmanı olmalıdır **WAF**, kapasite sku ayarlarken onaylanması gerekiyor.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Aşağıdaki örnekte tanımlandığı gibi WAF ayarları yapılandırın:

   İçin **FirewallMode**, önleme ve algılama değerleri kullanılabilir.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Uygulama ağ geçidi önceki adımda tanımlanan ayarlarıyla güncelleştirin.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Bu komut, uygulama ağ geçidi web uygulaması güvenlik duvarı ile güncelleştirir. Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) uygulama ağ geçidiniz için günlükleri görüntülemek nasıl anlamak için. WAF güvenlik yapısı nedeniyle, günlükleri, web uygulamalarınızı güvenlik yaklaşımı anlamak için düzenli olarak gözden geçirilmesi gerekir.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturma

Aşağıdaki adımları web uygulaması güvenlik duvarı ile bir uygulama ağ geçidi oluşturmak için bitiş başından tüm süreci izleyin.

Azure PowerShell’in en yeni sürümünü kullandığınızdan emin olun. Daha fazla bilgi için bkz.[Resource Manager ile Windows PowerShell Kullanma](../powershell-azure-resource-manager.md)

1. Azure'a çalıştırarak oturum açma `Login-AzureRmAccount`, kimlik bilgilerinizle kimliğinizi isteyip istemediğiniz sorulur.

1. Hesap için abonelikler denetleyin`Get-AzureRmSubscription`

1. Hangi Azure aboneliğinizin kullanılacağını seçin.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Uygulama ağ geçidi için bir kaynak grubu oluşturun.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu konum, kaynak grubundaki kaynaklar için varsayılan konum olarak kullanılır. Bir uygulama ağ geçidi oluşturmak için verilecek komutların aynı kaynak grubunu kullandığından emin olun.

Önceki örnekte, "appgw-RG adlı" "Batı ABD." konumlu bir kaynak grubu oluşturduk

> [!NOTE]
> Uygulama ağ geçidiniz için özel bir araştırma yapılandırmanız gerekiyorsa, bkz: [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-ps.md). Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.

### <a name="configure-virtual-network"></a>Sanal ağ yapılandırma

Uygulama ağ geçidi alt ağı için kendi gerektirir. Bu adımda, bir sanal ağ adres alanı 10.0.0.0/16 ve iki alt ağ, uygulama ağ geçidi için bir tane ve arka uç havuzu üyeleri için bir tane oluşturun.

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Genel IP adresi yapılandırın

Dış isteklerini işlemek için uygulama ağ geçidi genel bir IP adresi gerektirir. Bu genel IP adresi değil olmalıdır bir `DomainNameLabel` uygulama ağ geçidi tarafından kullanılması için tanımlanmış.

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a>Uygulama ağ geçidi yapılandırma

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Temel web uygulaması güvenlik duvarı yapılandırması ile oluşturulmuş uygulama ağ geçitleri için koruma CRS 3.0 ile yapılandırılır.

## <a name="get-application-gateway-dns-name"></a>Uygulama ağ geçidi DNS adını Al

Ağ geçidi oluşturulduktan sonraki adım, iletişim için ön uç yapılandırması yapmaktır. Genel IP kullanırken, uygulama ağ geçidi kolay olmayan dinamik olarak atanmış bir DNS adı gerektirir. Son kullanıcıların uygulama ağ geçidi isabet emin olmak için bir CNAME kaydı uygulama ağ geçidi ortak uç noktasına işaret etmek için kullanılabilir. [Azure’da özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). Bir diğer ad yapılandırmak için uygulama ağ geçidi ve ilişkili IP/DNS adını kullanarak uygulama ağ geçidine bağlı Publicıpaddress öğesi ayrıntılarını alamadı. Uygulama ağ geçidi DNS adı, iki web uygulamaları bu DNS adına işaret eden bir CNAME kaydı oluşturmak için kullanılmalıdır. Uygulama ağ geçidi başlatmada VIP değişebileceği A kayıtlarını kullanılması önerilmez.

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

Algılanan ya da engelledi ile web uygulaması güvenlik duvarı adresini ziyaret ederek günlük olaylarıyla tanılama günlük yapılandırmayı öğrenin [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
