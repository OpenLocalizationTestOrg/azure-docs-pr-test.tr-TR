---
title: "aaaConfigure yük dengeleyici dağıtım modu | Microsoft Docs"
description: "Nasıl tooconfigure Azure yük dengeleyici dağıtım modu toosupport kaynak IP benzeşimi"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Merhaba dağıtım modunu yük dengeleyici için yapılandırma

## <a name="hash-based-distribution-mode"></a>Karma tabanlı dağıtım modu

Merhaba varsayılan dağıtım algoritmasıdır, 5-tanımlama grubu (kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası, protokol türü) toomap trafiği tooavailable sunucuları karma. Bu, yalnızca bir aktarım oturumu içinde sürekliliği sağlar. Aynı oturum olacak hello paketlerinde aynı veri merkezi IP (DIP) örneği hello yük dengeli uç nokta toohello yönlendirilmiş. Merhaba istemci başlatıldığında yeni bir oturum ile aynı kaynak IP Merhaba, hello kaynak bağlantı noktası değiştirir ve hello trafiği toogo tooa farklı DIP endpoint neden olur.

![Karma tabanlı yük dengeleyici](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Şekil 1-5-tanımlama grubu dağıtımı

## <a name="source-ip-affinity-mode"></a>Kaynak IP benzeşim modu

Biz kaynak IP benzeşimi (oturum benzeşimi veya istemci IP benzeşim olarak da bilinir) adlı başka bir dağıtım moduna sahip. 3-tanımlama grubu (kaynak IP, hedef IP Protokolü) toomap trafiği toohello kullanılabilir sunuculara veya Azure yük dengeleyici yapılandırılmış toouse 2-tanımlama grubu (kaynak IP, hedef IP) olabilir. Kaynak IP benzeşimini kullanarak hello aynı başlatılan bağlantıları istemci bilgisayar gider toohello aynı DIP uç noktası.

Aşağıdaki diyagramda hello 2 bölütlü yapılandırma gösterilmektedir. Ardından VM2 ve VM3 tarafından yedeklenen hello yük dengeleyici toovirtual makine 1 (VM1) aracılığıyla hello 2 bölütlü nasıl çalışacağını dikkat edin.

![oturum benzeşimi](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Şekil 2-2 bölütlü dağıtım

Kaynak IP benzeşim hello Azure yük dengeleyici ve Uzak Masaüstü (RD) ağ geçidi arasında bir uyumsuzluk çözer. Şimdi tek bulut hizmetindeki bir RD Ağ Geçidi grubu oluşturabilirsiniz.

Başka bir kullanım senaryosu burada hello veri yükleme UDP gerçekleşir ancak hello denetim düzlemi TCP ile elde edilen medya karşıya yükleme şöyledir:

* Bir istemci ilk ortak adres toohello yük dengeli bir TCP oturumu başlatır, sol etkin toomonitor hello bağlantı durumu belirli DIP, bu kanal olan yönlendirilmiş tooa alır
* Aynı istemci bilgisayar hello yeni bir UDP oturumdan toohello başlatılan aynı yük dengeli ortak uç nokta, hello burada beklenir Bu bağlantı ayrıca yönlendirilmiş toohello olduğunu aynı DIP uç noktası hello önceki TCP bağlantısı olarak medyayı karşıya yükleme böylece olabilir yüksek verimlilik denetim kanalı TCP üzerinden de korurken yürütüldü.

> [!NOTE]
> (Ekleyerek veya çıkararak bir sanal makine) bir yük dengeli kümesi değiştiğinde, istemci isteklerini hello dağıtımını yeniden. Aynı hello sonlanır varolan istemcilerden gelen yeni bağlantıları bağlı olamazlar sunucu. Ayrıca, kaynak IP kullanarak benzeşim dağıtım modu trafiğinin eşit olmayan bir dağıtım neden olabilir. Proxy çalıştıran istemciler bir benzersiz istemci uygulaması olarak görülebilir.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>İçin kaynak IP benzeşim ayarlarını yapılandırmaya yük dengeleyici

Sanal makineler için PowerShell toochange zaman aşımı ayarları kullanabilirsiniz:

Azure uç noktası tooa sanal makine ekleyin ve yük dengeleyici dağıtım modunu ayarlama

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution toosourceIP, 3-tanımlama grubu (kaynak IP, hedef IP Protokolü) Yük Dengeleme veya hiçbiri sourceIPProtocol 5-tanımlama grubu Yük Dengelemesi hello varsayılan davranışı istiyorsanız 2 bölütlü (kaynak IP, hedef IP) Yük Dengeleme için ayarlanabilir.

Tooretrieve bir uç nokta yük dengeleyici dağıtım modu yapılandırma aşağıdaki hello kullan:

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

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
    LoadBalancerDistribution : sourceIP

Merhaba LoadBalancerDistribution öğesi mevcut değilse hello Azure yük dengeleyici hello varsayılan 5-tanımlama grubu algoritması kullanır.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Yük dengeli uç nokta kümesi üzerindeki hello dağıtım modunu ayarlama

Uç nokta yük dengeli uç nokta kümesi parçasıysa hello dağıtım modu hello yük dengeli uç nokta kümesi ayarlamanız gerekir:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Bulut hizmeti yapılandırma toochange dağıtım modu

.NET 2.5 (Kasım'da yayımlanan toobe) için Azure SDK'sı hello yararlanabilirsiniz tooupdate bulut hizmetiniz. Bulut Hizmetleri için uç nokta ayarlarını hello .csdef yapılır. Sipariş tooupdate hello yük dengeleyici dağıtım modunda bulut Hizmetleri dağıtımı için dağıtım yükseltme gereklidir.
.Csdef değişiklikleri uç noktası ayarları için bir örneği burada verilmiştir:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
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

## <a name="api-example"></a>API örneği

Merhaba Hizmet Yönetimi API'si kullanılarak hello yük dengeleyici dağıtım yapılandırabilirsiniz. Tooadd hello emin olun `x-ms-version` üstbilgisi tooversion ayarlandı `2014-09-01` ya da daha yüksek.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Hello güncelleştirme hello yapılandırmasını Yük Dengelemesi yapılmış bir dağıtımda belirtildi.

#### <a name="request-example"></a>Örnek istek

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

LoadBalancerDistribution başlangıç değeri 2 bölütlü benzeşimi, 3-tanımlama grubu benzeşimi sourceIPProtocol veya hiçbiri (için benzeşimi yok. Sourceıp olabilir yani 5-tanımlama grubu)

#### <a name="response"></a>Yanıt

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Sonraki Adımlar

[İç yük dengeleyiciye genel bakış](load-balancer-internal-overview.md)

[Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama](load-balancer-get-started-internet-arm-ps.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
