---
title: "aaaCreate özel araştırma - Azure uygulama ağ geçidi - PowerShell Klasik | Microsoft Docs"
description: "Nasıl toocreate özel bir araştırma uygulama ağ geçidi için hello Klasik dağıtım modelinde PowerShell kullanarak bilgi edinin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Özel bir araştırma için Azure uygulama ağ geçidi (Klasik) PowerShell kullanarak oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Klasik PowerShell](application-gateway-create-probe-classic-ps.md)

Bu makalede, bir özel araştırma tooan varolan uygulama ağ geçidi PowerShell ile ekleyin. Özel araştırmalara başarılı bir yanıt hello varsayılan web uygulaması üzerinde sağlamaz, uygulamaları veya belirli bir sağlık denetimi sayfası uygulamaları için kullanışlıdır.

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Uygulama ağ geçidi oluşturma

bir uygulama ağ geçidi toocreate:

1. Uygulama ağ geçidi kaynağı oluşturun.
2. Bir XML yapılandırma dosyası veya yapılandırma nesnesi oluşturun.
3. Hello yapılandırma toohello yeni oluşturulmuş uygulama ağ geçidi kaynağına uygulayın.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Özel bir araştırma ile uygulama ağ geçidi kaynağı oluşturma

toocreate hello ağ geçidi, kullanım hello `New-AzureApplicationGateway` hello değerleri kendi değerlerinizle değiştirerek cmdlet'i. Merhaba ağ geçidi için fatura bu noktada başlatılmaz. Merhaba ağ geçidi başarıyla başlatıldığında faturalama bir sonraki adımda başlar.

Merhaba aşağıdaki örnek bir uygulama ağ geçidi "testvnet1" ve "subnet-1" adlı bir alt ağ olarak adlandırılan bir sanal ağ kullanarak oluşturur.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

ağ geçidi hello toovalidate oluşturuldu, hello kullanabilirsiniz `Get-AzureApplicationGateway` cmdlet'i.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Merhaba için varsayılan değer *Instancecount* 10 maksimum değerini 2'dir. Merhaba için varsayılan değer *GatewaySize* Orta'dır. Küçük, Orta ve büyük arasında seçim yapabilirsiniz.
> 
> 

*VirtualIPs* ve *DnsName* hello ağ geçidi henüz başlatılmamış olduğundan boş olarak gösterilir. Merhaba ağ geçidi hello çalışır durumda olduğunda bu değerleri oluşturulur.

### <a name="configure-an-application-gateway-by-using-xml"></a>XML kullanarak uygulama ağ geçidi yapılandırma

Aşağıdaki örneğine hello, tüm uygulama ağ geçidi ayarları bir XML dosyası tooconfigure kullanın ve toohello uygulama ağ geçidi kaynağına uygulayın.  

Metin tooNotepad aşağıdaki hello kopyalayın.

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Merhaba yapılandırma öğeleri için hello parantez Hello değerlerini düzenleyin. Merhaba dosyası .xml. uzantısıyla kaydedin.

Merhaba aşağıdaki örnekte nasıl toouse bir yapılandırma dosyası tooset hello uygulama ağ geçidi tooload yukarı ortak bağlantı noktası 80 üzerinde HTTP trafiği dengelemek ve ağ trafiğini iki IP adreslerini özel bir araştırma kullanarak arasında tooback uç bağlantı noktası 80 Gönder gösterir.

> [!IMPORTANT]
> Http veya Https Hello protokol öğesi büyük/küçük harf duyarlıdır.

Yeni bir yapılandırma öğesi \<araştırma\> tooconfigure özel araştırmalara eklenir.

Merhaba yapılandırma Parametreler şunlardır:

|Parametre|Açıklama|
|---|---|
|**Ad** |Özel araştırma için başvuru adı. |
* **Protokolü** | Kullanılan protokol (olası değerler HTTP veya HTTPS).|
| **Ana bilgisayar** ve **yolu** | Merhaba uygulama ağ geçidi toodetermine hello sistem hello örneğinin tarafından çağrılan tam URL yolu. Örneğin, sonra da Hello özel araştırma için yapılandırılabilir bir Web sitesi http://contoso.com/ varsa araştırma için "http://contoso.com/path/custompath.htm" toohave başarılı bir HTTP yanıt denetler.|
| **Aralığı** | Merhaba yoklama aralığı denetimleri saniye olarak yapılandırır.|
| **Zaman aşımı** | Bir HTTP yanıt denetimi için Hello yoklama zaman aşımını tanımlar.|
| **UnhealthyThreshold** | Merhaba başarısız HTTP yanıt sayısı tooflag hello arka uç örnek olarak *sağlıksız*.|

Merhaba araştırma adı hello başvurulan \<BackendHttpSettings\> yapılandırma tooassign hangi arka uç havuzuna özel araştırma ayarlarını kullanır.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Bir özel araştırma tooan varolan uygulama ağ geçidi Ekle

Bir uygulama ağ geçidi değişen hello geçerli yapılandırmasını üç adımı gerektirir: Get hello geçerli XML yapılandırma dosyası, toohave özel bir araştırma değiştirmek ve hello uygulama ağ geçidi hello yeni XML ayarlarla yapılandırın.

1. Merhaba XML dosyasını kullanarak alma `Get-AzureApplicationGatewayConfig`. Bu cmdlet dışarı hello yapılandırma XML toobe tooadd bir yoklama ayarı değiştirildi.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Merhaba XML dosyasını bir metin düzenleyicisinde açın. Ekleme bir `<probe>` sonra bölümünde `<frontendport>`.

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  Merhaba backendHttpSettings bölümünde hello XML hello araştırma adı hello aşağıdaki örnekte gösterildiği gibi ekleyin:

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  Merhaba XML dosyasını kaydedin.

1. Güncelleştirme hello uygulama ağ geçidi yapılandırmasını kullanarak hello yeni bir XML dosyası ile `Set-AzureApplicationGatewayConfig`. Bu cmdlet, uygulama ağ geçidi hello yeni yapılandırmayla güncelleştirir.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Sonraki adımlar

Güvenli Yuva Katmanı (SSL) yük boşaltma tooconfigure istiyorsanız, bkz: [SSL yük boşaltımı için bir uygulama ağ geçidi](application-gateway-ssl.md).

Bir iç yük dengeleyici ile bir uygulama ağ geçidi toouse tooconfigure istiyorsanız, bkz: [bir iç yük dengeleyici (ILB) ile bir uygulama ağ geçidi oluşturma](application-gateway-ilb.md).

