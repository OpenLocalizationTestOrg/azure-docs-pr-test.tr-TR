---
title: "aaaConfigure yük dengeleyici TCP boşta kalma zaman aşımı | Microsoft Docs"
description: "Yük Dengeleyici TCP boşta kalma zaman aşımı yapılandırın"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Azure yük dengeleyici için TCP boşta kalma zaman aşımı ayarlarını yapılandırın

Varsayılan yapılandırmasında, Azure yük dengeleyici, 4 dakikalık bir boşta kalma zaman aşımı ayarının. Bir süre işlem yapılmadığında hello zaman aşımı değeri uzun olması durumunda, TCP hello garantisi yoktur veya HTTP oturumu hello istemci ile bulut hizmetiniz arasında korunur.

Merhaba bağlantı kapalı olduğunda istemci uygulamanızı hello aşağıdaki hata iletisini alabilirsiniz: "Merhaba temel alınan bağlantı kapatıldı: Canlı tutulur toobe hello sunucu tarafından kapatıldı bekleniyordu bir bağlantı."

Toouse TCP tutma yaygın bir uygulamadır. Bu uygulama için daha uzun bir süre hello bağlantıyı etkin tutar. Daha fazla bilgi için bkz: [.NET örnekleri](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Tutma etkin, paketleri hello bağlantıda kaldıktan dönemlerde gönderilir. Bu tutma paketler hello boşta kalma zaman aşımı değeri hiçbir zaman ulaşıldığında ve hello bağlantısı uzun bir süre boyunca tutulur emin olun.

Bu ayar yalnızca gelen bağlantılar için çalışır. tooavoid kaybeden hello bağlantı hello boşta kalma zaman aşımı ayarını veya artış hello boşta kalma zaman aşımı değeri'den bir aralık ile Merhaba TCP tutma yapılandırmanız gerekir. toosupport bu senaryolara yapılandırılabilir boşta kalma zaman aşımı için destek ekledik. Şimdi 4 too30 dakika süresince ayarlayabilirsiniz.

TCP tutma iyi pil ömrünün bir kısıtlaması olduğu senaryolar için çalışır. Mobil uygulamalar için önerilmez. Bir mobil uygulama tutma bir TCP kullanarak hello aygıt pil daha hızlı tükenir.

![TCP zaman aşımı](./media/load-balancer-tcp-idle-timeout/image1.png)

Aşağıdaki bölümlerde hello nasıl toochange boşta kalma zaman aşımı ayarları sanal makineler ve bulut Hizmetleri açıklanmaktadır.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Merhaba TCP zaman aşımı, örnek düzeyinde ortak IP too15 dakika için yapılandırma

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` isteğe bağlıdır. Ayarlanmazsa, varsayılan zaman aşımı hello 4 dakikadır. Merhaba kabul edilebilir zaman aşımı aralığı 4 too30 dakikadır.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Azure bir uç nokta bir sanal makinede oluştururken Hello boşta kalma zaman aşımını ayarlama

toochange zaman aşımı için bir uç nokta ayarlama Merhaba, hello aşağıdakileri kullanın:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve boşta kalma zaman aşımı yapılandırmanıza, komutu aşağıdaki kullanım hello:

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Merhaba TCP zaman aşımı üzerinde bir yük dengeli uç nokta kümesi

Uç nokta yük dengeli uç nokta kümesi parçasıysa hello TCP zaman aşımı hello yük dengeli uç nokta kümesi ayarlamanız gerekir. Örneğin:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Bulut Hizmetleri zaman aşımı ayarlarını değiştirme

Bulut hizmetinizi hello Azure SDK'sı tooupdate kullanabilirsiniz. Bulut Hizmetleri için uç nokta ayarlarını hello .csdef dosyasında yapın. Bir bulut hizmeti dağıtımının Hello TCP zaman aşımı güncelleştirme dağıtımı yükseltme gerektirir. Merhaba TCP zaman aşımı yalnızca genel IP için belirtilmezse dışındadır. Genel IP ayarlarını hello .cscfg dosyasında yer alır ve bunları dağıtım güncelleştirme ve yükseltme güncelleştirebilirsiniz.

uç noktası ayarları için Hello .csdef değişiklikleri şunlardır:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

Merhaba zaman aşımı ayarını genel IP'ler için Hello .cscfg değişiklikleri şunlardır:

```xml
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
    <InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
        <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
    </InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="rest-api-example"></a>REST API örneği

Merhaba TCP boşta kalma zaman aşımı hello Hizmet Yönetimi API kullanarak yapılandırabilirsiniz. Bu hello emin olun `x-ms-version` üstbilgisi tooversion ayarlandı `2014-06-01` veya sonraki bir sürümü. Merhaba belirtilen hello yapılandırmasını yük dengeli bir dağıtımdaki tüm sanal makinelerde giriş uç noktaları güncelleştirin.

### <a name="request"></a>İstek

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Yanıt

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a>Sonraki adımlar

[İç yük dengeleyiciye genel bakış](load-balancer-internal-overview.md)

[Bir Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-internet-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)
