---
title: "aaaConfigure SSL boşaltma - Azure uygulama ağ geçidi - PowerShell Klasik | Microsoft Docs"
description: "Bu makalede, bir uygulama ağ geçidi ile SSL boşaltma kullanarak toocreate hello Azure Klasik dağıtım modeli yönergeler sağlar."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Merhaba Klasik dağıtım modeli kullanarak SSL yük boşaltımı için bir uygulama ağ geçidi yapılandırma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Klasik PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure uygulama ağ geçidi yapılandırılmış tooterminate hello Güvenli Yuva Katmanı (SSL) hello ağ geçidi tooavoid maliyetli SSL şifre çözme görevleri toohappen hello web grubu adresindeki oturumunda olabilir. SSL boşaltma ayrıca hello ön uç sunucusunun kurulumunu ve hello web uygulamasının yönetimini basitleştirir.

## <a name="before-you-begin"></a>Başlamadan önce

1. Merhaba Web Platformu Yükleyicisi'ni kullanarak Hello hello Azure PowerShell cmdlet'lerinin en yeni sürümünü yükleyin. Karşıdan yükle ve hello hello en son sürümünü yüklemek **Windows PowerShell** hello bölümünü [indirmeler sayfası](https://azure.microsoft.com/downloads/).
2. Geçerli bir alt ağla çalışan bir sanal ağa sahip olduğunuzu doğrulayın. Hiçbir sanal makine veya Bulut dağıtımları hello alt kullandığınızdan emin olun. Merhaba uygulama ağ geçidi tek başına bir sanal ağ alt ağında olmalıdır.
3. toouse hello uygulama ağ geçidi yapılandırma hello sunucular mevcut olmalıdır veya hello sanal ağ veya genel IP/VIP'ye ile oluşturulan uç noktaları atadınız.

tooconfigure SSL bir uygulama ağ geçidinde boşaltma, aşağıdaki adımları listelenen hello sırayla hello:

1. [Bir uygulama ağ geçidi oluşturma](#create-an-application-gateway)
2. [SSL sertifikalarını karşıya yükleme](#upload-ssl-certificates)
3. [Merhaba ağ geçidini yapılandırma](#configure-the-gateway)
4. [Kümesi hello ağ geçidi yapılandırması](#set-the-gateway-configuration)
5. [Merhaba ağ geçidi Başlat](#start-the-gateway)
6. [Merhaba ağ geçidi durumunu doğrulama](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

toocreate hello ağ geçidi, kullanım hello `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i. Merhaba ağ geçidi için fatura bu noktada başlatılmaz. Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

ağ geçidi hello toovalidate oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.

Merhaba örneğinde, *açıklama*, *Instancecount*, ve *GatewaySize* isteğe bağlı parametrelerdir. Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir. Merhaba için varsayılan değer *GatewaySize* Orta'dır. Küçük ve büyük diğer değerleri kullanılabilir. *VirtualIPs* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir. Merhaba ağ geçidi hello çalışır durumda olduğunda bu değerleri oluşturulur.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>SSL sertifikalarını karşıya yükleme

Kullanım `Add-AzureApplicationGatewaySslCertificate` tooupload hello sunucu sertifikasında *pfx* biçimi toohello uygulama ağ geçidi. Merhaba sertifika adı, bir kullanıcı tarafından seçilen adıdır ve hello uygulama ağ geçidi içinde benzersiz olmalıdır. Bu sertifika başvurulan tooby tüm sertifika yönetimi işlemlerinin hello uygulama ağ geçidi üzerinde bu adıdır.

Bu aşağıdaki örnek gösterir cmdlet Merhaba, hello örnek hello değerleri kendinizinkilerle değiştirin.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Ardından, hello sertifika yükleme doğrulayın. Kullanım hello `Get-AzureApplicationGatewayCertificate` cmdlet'i.

Bu örnek hello cmdlet'i hello ilk satırında, gösterilmektedir hello çıktı tarafından izlenen.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> Merhaba sertifika parolası 4 too12 karakterler, harf veya sayı arasında toobe sahiptir. Özel karakterleri kabul edilmedi.

## <a name="configure-hello-gateway"></a>Merhaba ağ geçidini yapılandırma

Bir uygulama ağ geçidi yapılandırması birden çok değerden oluşur. Merhaba değerleri bağlı birlikte tooconstruct hello yapılandırma.

Merhaba değerler şunlardır:

* **Arka uç sunucusu havuzu:** hello hello arka uç sunucularının IP adresleri listesi. listede hello IP adresleri ya da toohello sanal ağ alt veya ait genel IP/VIP'ye olmalıdır.
* **Arka uç sunucu havuzu ayarları**: Her havuzun bağlantı noktası, protokol ve tanımlama bilgisi temelli benzeşim gibi ayarları vardır. Bu ayarlar bağlı tooa olan havuzu ve hello havuz içindeki uygulanan tooall sunucularıdır.
* **Ön uç bağlantı noktası:** Bu bağlantı noktası hello hello uygulama ağ geçidinde açılan genel bağlantı noktasıdır. Bu bağlantı noktasında trafik trafik ve tooone hello arka uç sunucularının alır yeniden yönlendirildi.
* **Dinleyici:** hello dinleyicisi sahip bir ön uç bağlantı noktası, bir protokol (Http veya Https, bu değerleri büyük küçük harfe duyarlı) ve hello SSL sertifika adı (SSL yük boşaltımı yapılandırılıyorsa).
* **Kural:** hello kural hello dinleyicisi ve hello arka uç sunucusu havuzunu bağlar ve belli bir Dinleyicide trafik yönlendirilmiş toowhen hangi arka uç sunucu havuzu hello trafiğinin olmalıdır belirler. Şu anda yalnızca hello *temel* kural desteklenmektedir. Merhaba *temel* hepsini bir kez deneme yük dağıtımı kuralıdır.

**Ek yapılandırma notları**

SSL sertifikaları yapılandırma, protokolünde hello **HttpListener** çok değiştirmelisiniz*Https* (büyük küçük harf duyarlı). Merhaba **SslCert** öğesi çok eklenen**HttpListener** hello ile aynı ad olarak kullanılan SSL sertifikaları bölüm önceki, hello karşıya toohello değerini ayarlayın. Merhaba ön uç bağlantı noktası güncelleştirilmiş too443 olmalıdır.

**tooenable tanımlama bilgisi temelli benzeşimi**: bir uygulama ağ geçidi isteği bir istemci oturumundan her zaman yönlendirilmiş toohello olduğunu yapılandırılmış tooensure olabilir hello web grubundaki aynı VM. Bu senaryo, uygun şekilde hello ağ geçidi toodirect trafiğe izin veren bir oturum tanımlama bilgisi ekleme işlemi tarafından yapılır. tanımlama bilgisi temelli benzeşimi tooenable ayarlamak **CookieBasedAffinity** çok*etkin* hello içinde **BackendHttpSettings** öğesi.

Bir yapılandırma nesnesi oluşturma veya bir XML yapılandırma dosyası kullanarak yapılandırmanızı oluşturabilirsiniz.
bir yapılandırma XML dosyasını kullanarak yapılandırmanızı tooconstruct kullanmak hello örnek:

**Yapılandırma XML örneği**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

Ardından, hello uygulama ağ geçidi ayarlayın. Merhaba kullanabilirsiniz `Set-AzureApplicationGatewayConfig` cmdlet'i bir yapılandırma nesnesi veya bir XML yapılandırma dosyası.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Merhaba ağ geçidi Başlat

Hello ağ geçidi yapılandırıldıktan sonra hello kullanarak `Start-AzureApplicationGateway` cmdlet toostart hello ağ geçidi. Bir uygulama ağ geçidi için fatura Hello ağ geçidi başarıyla başlatıldıktan sonra başlar.

> [!NOTE]
> Merhaba `Start-AzureApplicationGateway` cmdlet too15-20 dakika toofinish alabilir.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Merhaba ağ geçidi durumunu doğrulama

Kullanım hello `Get-AzureApplicationGateway` cmdlet toocheck hello hello ağ geçidi durumunu. Varsa `Start-AzureApplicationGateway` hello önceki adımda başarılı *durumu* çalıştırması gerekir, ve *VirtualIPs* ve *DnsName* geçerli girdilere sahip olmalıdır.

Bu örnek, çalışır ve hazır tootake trafiği olan bir uygulama ağ geçidi gösterir.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Sonraki adımlar

Yük dengeleme seçenekleri hakkında daha fazla genel bilgi edinmek istiyorsanız, bkz.

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

