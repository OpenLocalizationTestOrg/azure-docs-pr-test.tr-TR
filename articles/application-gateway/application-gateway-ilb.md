---
title: "Azure uygulama ağ geçidi iç yük dengeleyici ile aaaUsing | Microsoft Docs"
description: "Bu sayfa, Azure uygulama ağ geçidi ile bir iç yük dengeli uç nokta yönergeleri tooconfigure sağlar"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>İç Load Balancer (ILB) aracılığıyla Application Gateway oluşturun

> [!div class="op_single_selector"]
> * [Azure Klasik PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

Bir iç uç nokta sunulmaz toohello veya internet'e yönelik sanal IP ile uygulama ağ geçidi yapılandırılabilir Internet, olarak da bilinen iç yük dengeleyici (ILB) uç noktası. Bir ILB ile yapılandırma hello ağ geçidi sunulmaz iç iş kolu satır uygulamaları toointernet için yararlıdır. Güvenlik sunulmaz sınır toointernet içinde bulunur, ancak hala hepsini bir kez deneme yük dağıtımı, oturum sürekliliği veya SSL sonlandırması gerektiren çok katmanlı uygulama içinde Hizmetleri/katmanları için de yararlıdır. Bu makalede, hello adımları tooconfigure bir uygulama ağ geçidini bir ILB ile adım adım anlatılmaktadır.

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu yükleyicisi kullanılarak hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirme sayfası](https://azure.microsoft.com/downloads/).
2. Geçerli bir alt ağ ile çalışan bir sanal ağa sahip olduğunuzu doğrulayın.
3. Merhaba sanal ağda veya atanan genel IP/VIP'ye ile arka uç sunucularına sahip olduğunuzu doğrulayın.

bir uygulama ağ geçidi toocreate hello sırayı adımlarını izleyerek hello gerçekleştirin. 

1. [Bir uygulama ağ geçidi oluşturma](#create-a-new-application-gateway)
2. [Merhaba ağ geçidini yapılandırma](#configure-the-gateway)
3. [Kümesi hello ağ geçidi yapılandırması](#set-the-gateway-configuration)
4. [Merhaba ağ geçidi Başlat](#start-the-gateway)
5. [Merhaba ağ geçidini doğrulama](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Bir uygulama ağ geçidi oluşturun:

**toocreate hello ağ geçidi**, hello kullan `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i. Merhaba ağ geçidi için fatura bu noktada başlamıyor unutmayın. Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** hello ağ geçidi oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i. 

Merhaba örneğinde, *açıklama*, *Instancecount*, ve *GatewaySize* isteğe bağlı parametrelerdir. Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir. Merhaba için varsayılan değer *GatewaySize* Orta'dır. Küçük ve büyük diğer değerleri kullanılabilir. *VIP* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir. Merhaba ağ geçidi çalışır durumda hello olduğunda bunlar oluşturulur. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Merhaba ağ geçidini yapılandırma
Bir uygulama ağ geçidi yapılandırması birden çok değerden oluşur. Merhaba değerleri bağlı birlikte tooconstruct hello yapılandırma.

Merhaba değerler şunlardır:

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adreslerinin listesi. listede hello IP adresleri ya da toohello sanal alt ait olması gerekir veya genel IP/VIP'ye olmalıdır. 
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello uygulama ağ geçidinde açılan hello genel bağlantı noktasıdır. Trafiği, bu bağlantı noktasında trafik ve yeniden yönlendirilen tooone hello arka uç sunucularının alır.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bunlar büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa). 
* **Kural:** hello kural hello dinleyici ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğini olmalıdır belirler. Şu anda yalnızca hello *temel* kural desteklenmektedir. Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.

Bir yapılandırma nesnesi oluşturarak veya bir XML yapılandırma dosyası kullanarak yapılandırmanızı oluşturabilirsiniz. tooconstruct yapılandırma XML dosyası, kullanım hello kullanarak yapılandırmanızı Aşağıda örnek.

Merhaba aşağıdakileri göz önünde bulundurun:

* Merhaba *Frontendıpconfigurations'a* öğesi hello ILB ayrıntıları uygulama ağ geçidini bir ILB ile yapılandırılmasıyla ilgili açıklar. 
* Merhaba ön uç IP *türü* too'Private ayarlanmalıdır '
* Merhaba *StaticIPAddress* istenen toohello iç IP hangi hello üzerinde ağ geçidi alır trafiği ayarlamanız gerekir. Bu hello Not *StaticIPAddress* öğesidir isteğe bağlıdır. Aksi durumda kümesi, kullanılabilir bir iç IP dağıtılan hello alt ağdan seçilir. 
* Merhaba hello değerini *adı* belirtilen öğesi *Frontendıpconfiguration* hello HTTPListener's kullanılmalıdır *FrontendIP* öğesi toorefer toohello Frontendıpconfiguration.
  
  **Yapılandırma XML örneği**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a>Kümesi hello ağ geçidi yapılandırması
Ardından, hello uygulama ağ geçidi ayarlarsınız. Merhaba kullanabilirsiniz `Set-AzureApplicationGatewayConfig` cmdlet'i bir yapılandırma nesnesi veya bir XML yapılandırma dosyası. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Merhaba ağ geçidi Başlat

Hello ağ geçidi yapılandırıldıktan sonra hello kullanarak `Start-AzureApplicationGateway` cmdlet toostart hello ağ geçidi. Bir uygulama ağ geçidi için fatura Hello ağ geçidi başarıyla başlatıldıktan sonra başlar. 

> [!NOTE]
> Merhaba `Start-AzureApplicationGateway` cmdlet too15-20 dakika toocomplete alabilir. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Merhaba ağ geçidi durumunu doğrulama

Kullanım hello `Get-AzureApplicationGateway` cmdlet toocheck hello ağ geçidi durumunu. Varsa `Start-AzureApplicationGateway` hello önceki adımda başarılı oldu, hello durumu olmalıdır *çalıştıran*, VIP hello ve DnsName geçerli girişi olmalıdır. Bu örnek hello cmdlet'i hello ilk satırında, gösterilmektedir hello çıktı tarafından izlenen. Bu örnek hello ağ geçidi çalışıyor ve hazır tootake trafiğidir. 

> [!NOTE]
> Merhaba uygulama ağ geçidi yapılandırılmış hello tooaccept trafiğinin Bu örnekte 10.0.0.10 ILB uç noktasını yapılandırılmış.

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Sonraki adımlar
Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

