---
title: "aaaCreate, başlatma veya bir uygulama ağ geçidini silme | Microsoft Docs"
description: "Bu sayfa toocreate, yapılandırmak, başlatın ve bir Azure uygulama ağ geçidini silme yönergelerini sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>PowerShell ile bir uygulama ağ geçidi oluşturma, başlatma veya silme 

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Klasik PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager şablonu](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

Azure Application Gateway, bir katman 7 yük dengeleyicidir. Merhaba Bulut veya şirket içinde olmalarından bağımsız yük devretme, HTTP isteklerini, farklı sunucular arasında performans amaçlı yönlendirme sağlar. Application Gateway; HTTP yük dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi, Güvenli Yuva Katmanı (SSL) boşaltma, özel sistem durumu araştırmaları, çoklu site desteği gibi birçok Application Delivery Controller (ADC) özelliği sunar. toofind desteklenen özelliklerin tam bir listesi ziyaret [uygulama ağ geçidi'ne genel bakış](application-gateway-introduction.md)

Bu makalede hello adımları toocreate anlatılmaktadır, yapılandırmak, başlatmak ve bir uygulama ağ geçidini silin.

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Varolan bir sanal ağınız varsa, mevcut bir boş alt seçin veya hello uygulama ağ geçidi tarafından kullanılmak üzere yalnızca varolan sanal ağınızda yeni bir alt ağ oluşturun. Merhaba uygulama ağ geçidi tooa farklı sanal ağı dağıtamazsınız daha hello kaynak vnet eşlemesi kullanılmadığı sürece hello uygulama ağ geçidi arkasında toodeploy düşündüğünüz. toolearn daha ziyaret [Vnet eşlemesi](../virtual-network/virtual-network-peering-overview.md)
3. Geçerli bir alt ağla çalışan bir sanal ağa sahip olduğunuzu doğrulayın. Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun. Merhaba uygulama ağ geçidi tek başına bir sanal ağ alt ağında olmalıdır.
4. toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Gerekli toocreate bir uygulama ağ geçidi nedir?

Merhaba kullandığınızda `New-AzureApplicationGateway` komutu toocreate hello uygulama ağ geçidi, herhangi bir yapılandırma bu noktada ayarlanır ve yeni oluşturulan hello kaynak yapılandırılmış XML veya bir yapılandırma nesnesi kullanarak.

Merhaba değerler şunlardır:

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi. listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).
* **Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler.

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

bir uygulama ağ geçidi toocreate:

1. Uygulama ağ geçidi kaynağı oluşturun.
2. Bir XML yapılandırma dosyası veya yapılandırma nesnesi oluşturun.
3. Hello yapılandırma toohello yeni oluşturulmuş uygulama ağ geçidi kaynağına uygulayın.

> [!NOTE]
> Uygulama ağ geçidiniz için özel bir araştırma tooconfigure gerekirse bkz [PowerShell kullanarak özel araştırmalara sahip bir uygulama ağ geçidi oluşturma](application-gateway-create-probe-classic-ps.md). Daha fazla bilgi için [özel araştırmalar ve sistem durumu izleme](application-gateway-probe-overview.md) konusunu inceleyin.

![Senaryo örneği][scenario]

### <a name="create-an-application-gateway-resource"></a>Bir uygulama ağ geçidi kaynağı oluşturma

toocreate hello ağ geçidi, kullanım hello `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i. Merhaba ağ geçidi için fatura bu noktada başlatılmaz. Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.

Merhaba aşağıdaki örnek bir uygulama ağ geçidi "testvnet1" ve "subnet-1" adlı bir alt ağ olarak adlandırılan bir sanal ağ kullanarak oluşturur:

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* ve *GatewaySize* tercihe bağlı parametrelerdir.

ağ geçidi hello toovalidate oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir. Merhaba için varsayılan değer *GatewaySize* Orta'dır. Small, Medium ve Large seçenekleri bulunur.

*VirtualIPs* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir. Merhaba ağ geçidi çalışır durumda hello olduğunda bunlar oluşturulur.

## <a name="configure-hello-application-gateway"></a>Merhaba uygulama ağ geçidi yapılandırma

XML veya bir yapılandırma nesnesi kullanarak hello uygulama ağ geçidini yapılandırabilirsiniz.

### <a name="configure-hello-application-gateway-by-using-xml"></a>XML kullanarak Hello uygulama ağ geçidi yapılandırma

Aşağıdaki örneğine hello, tüm uygulama ağ geçidi ayarları bir XML dosyası tooconfigure kullanın ve toohello uygulama ağ geçidi kaynağına uygulayın.  

#### <a name="step-1"></a>1. Adım

Metin tooNotepad aşağıdaki hello kopyalayın.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Merhaba yapılandırma öğeleri için hello parantez Hello değerlerini düzenleyin. Merhaba dosyası .xml. uzantısıyla kaydedin.

> [!IMPORTANT]
> Http veya Https Hello protokol öğesi büyük/küçük harf duyarlıdır.

Aşağıdaki örneğine hello nasıl toouse bir yapılandırma dosyası hello uygulama ağ geçidi yukarı tooset gösterir. Merhaba örnek yük ortak bağlantı noktası 80 üzerinde HTTP trafiği dengeler ve ağ trafiğini iki IP adresi arasında tooback uç bağlantı noktası 80 gönderir.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a>2. Adım

Ardından, hello uygulama ağ geçidi ayarlayın. Kullanım hello `Set-AzureApplicationGatewayConfig` cmdlet'ini bir XML yapılandırma dosyası.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Bir yapılandırma nesnesi kullanarak Hello uygulama ağ geçidi yapılandırma

Aşağıdaki örnek hello nasıl tooconfigure hello uygulama ağ geçidi yapılandırma nesnesi kullanarak gösterir. Tüm yapılandırma öğeleri ayrı ayrı yapılandırılır ve daha sonra eklenen tooan uygulama ağ geçidi yapılandırma nesnesi. Merhaba Yapılandırma nesnesini oluşturduktan sonra hello kullan `Set-AzureApplicationGateway` komutu toocommit hello yapılandırma toohello daha önce oluşturduğunuz uygulama ağ geçidi kaynağı.

> [!NOTE]
> Bir değer tooeach yapılandırma nesnesi atamadan önce depolama için PowerShell ne tür bir nesneyi kullanan toodeclare gerekir. Merhaba ilk satırı toocreate hello ayrı ayrı öğeler tanımlar ne `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` kullanılır.

#### <a name="step-1"></a>1. Adım

Tüm bireysel yapılandırma öğelerini oluşturun.

Merhaba ön uç IP hello aşağıdaki örnekte gösterildiği gibi oluşturun.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Merhaba ön uç bağlantı noktası hello aşağıdaki örnekte gösterildiği gibi oluşturun.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Merhaba arka uç sunucu havuzu oluşturun.

Merhaba sonraki örnekte gösterildiği gibi toohello arka uç sunucu havuzuna eklenmiş hello IP adreslerini tanımlayın.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Merhaba $server tooadd hello değerleri toohello arka uç havuzu nesne ($pool) kullanın.

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Merhaba arka uç sunucu havuzu ayarlarını oluşturun.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Merhaba dinleyici oluşturun.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Merhaba kuralı oluşturun.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>2. Adım

Tüm Bireysel yapılandırma öğelerini tooan uygulama ağ geçidi yapılandırma nesnesi ($appgwconfig) atayın.

Merhaba ön uç IP toohello yapılandırmasını ekleyin.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Merhaba ön uç bağlantı noktası toohello yapılandırma ekleyin.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Merhaba arka uç sunucu havuzu toohello yapılandırması ekleyin.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Merhaba arka uç havuzu ayarı toohello yapılandırması ekleyin.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Merhaba dinleyici toohello yapılandırması ekleyin.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Merhaba kural toohello yapılandırma ekleyin.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>3. Adım
Merhaba yapılandırma nesnesi toohello uygulama ağ geçidi kaynağı kullanarak yürütme `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Merhaba ağ geçidi Başlat

Hello ağ geçidi yapılandırıldıktan sonra hello kullanarak `Start-AzureApplicationGateway` cmdlet toostart hello ağ geçidi. Bir uygulama ağ geçidi için fatura Hello ağ geçidi başarıyla başlatıldıktan sonra başlar.

> [!NOTE]
> Merhaba `Start-AzureApplicationGateway` cmdlet too15-20 dakika toofinish alabilir.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Merhaba ağ geçidi durumunu doğrulama

Kullanım hello `Get-AzureApplicationGateway` cmdlet toocheck hello hello ağ geçidi durumunu. Varsa `Start-AzureApplicationGateway` hello önceki adımda başarılı *durumu* çalıştırması gerekir, ve *VIP* ve *DnsName* geçerli girdilere sahip olmalıdır.

Hello aşağıdaki örnekte gösterilir çalışır durumda, bir uygulama ağ geçidi ve hazır tootake trafiği hedefleyen için `http://<generated-dns-name>.cloudapp.net`.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Merhaba uygulama ağ geçidini Sil

toodelete hello uygulama ağ geçidi:

1. Kullanım hello `Stop-AzureApplicationGateway` cmdlet toostop hello ağ geçidi.
2. Kullanım hello `Remove-AzureApplicationGateway` cmdlet tooremove hello ağ geçidi.
3. Bu hello ağ geçidi hello kullanarak kaldırıldı doğrulayın `Get-AzureApplicationGateway` cmdlet'i.

Merhaba aşağıdaki örnekte gösterilir hello `Stop-AzureApplicationGateway` cmdlet hello ilk satırdaki ardından tarafından hello çıktı.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Merhaba uygulama ağ geçidi durdurulmuş durumda olduğunda, hello kullan `Remove-AzureApplicationGateway` cmdlet tooremove hello hizmet.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

Hizmet hello tooverify kaldırıldı, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i. Bu adım gerekli değildir.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Sonraki adımlar

SSL boşaltma tooconfigure istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).

Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
