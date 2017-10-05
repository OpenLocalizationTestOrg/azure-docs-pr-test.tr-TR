---
title: "Yük Dengeleyici dağıtım modunu yapılandırmak | Microsoft Docs"
description: "Kaynak IP benzeşimini desteklemek için Azure yük dengeleyici dağıtım modunu yapılandırma"
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
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a>Yük Dengeleyici için dağıtım modunu yapılandırma

## <a name="hash-based-distribution-mode"></a>Karma tabanlı dağıtım modu

Varsayılan dağıtım algoritmasıdır 5-tanımlama grubu (kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası, protokol türü) trafiği kullanılabilir sunuculara eşlemek için karma. Bu, yalnızca bir aktarım oturumu içinde sürekliliği sağlar. Yük dengeli uç nokta arkasındaki aynı veri merkezinde IP'yi (DIP) örneğini paketleri aynı oturumda yönlendirilir. İstemci aynı kaynak IP yeni bir oturum başlatıldığında, kaynak bağlantı noktası değiştirir ve farklı bir DIP bitiş noktasına gitmek trafiği neden olur.

![Karma tabanlı yük dengeleyici](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Şekil 1-5-tanımlama grubu dağıtımı

## <a name="source-ip-affinity-mode"></a>Kaynak IP benzeşim modu

Biz kaynak IP benzeşimi (oturum benzeşimi veya istemci IP benzeşim olarak da bilinir) adlı başka bir dağıtım moduna sahip. Azure yük dengeleyici 2 bölütlü (kaynak IP, hedef IP) veya 3-tanımlama grubu (kaynak IP, hedef IP Protokolü) trafiği kullanılabilir sunuculara eşlemek için kullanmak üzere yapılandırılabilir. Kaynak IP benzeşim kullanarak, aynı istemci bilgisayardan başlatılan bağlantıları aynı DIP uç noktasına gider.

Aşağıdaki diyagramda 2 bölütlü yapılandırma gösterilmektedir. Ardından VM2 ve VM3 tarafından yedeklenen yük dengeleyici sanal makineye 1 (VM1) aracılığıyla 2 bölütlü nasıl çalışacağını dikkat edin.

![oturum benzeşimi](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Şekil 2-2 bölütlü dağıtım

Kaynak IP benzeşim Azure yük dengeleyici ve Uzak Masaüstü (RD) ağ geçidi arasında bir uyumsuzluk çözer. Şimdi tek bulut hizmetindeki bir RD Ağ Geçidi grubu oluşturabilirsiniz.

Başka bir kullanım senaryosu burada veriler karşıya UDP gerçekleşir ancak denetim düzlemi TCP ile elde edilen medya karşıya yükleme şöyledir:

* Bir istemci ilk yükü dengelenmiş genel adresine TCP oturumu başlatır, yönlendirilmiş belirli bir DIP için bu kanal bağlantı durumunu izlemek için etkin kalır
* Aynı istemci bilgisayardan yeni bir UDP oturum aynı yük dengeli ortak uç nokta başlatılır, burada medyayı karşıya yükleme böylece yüksek önceki TCP bağlantı yürütülebilecek gibi bu bağlantı aynı DIP uç noktasına ayrıca yönlendirilmiş beklenir denetim kanalı TCP üzerinden de korurken üretilen işi.

> [!NOTE]
> Bir yük dengeli kümesi değiştiğinde (bir sanal makine ekleyerek veya çıkararak), istemci isteklerini dağıtımını yeniden. Aynı sunucuda sonlanır varolan istemcilerden gelen yeni bağlantıları üzerinde bağımlı olamaz. Ayrıca, kaynak IP kullanarak benzeşim dağıtım modu trafiğinin eşit olmayan bir dağıtım neden olabilir. Proxy çalıştıran istemciler bir benzersiz istemci uygulaması olarak görülebilir.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>İçin kaynak IP benzeşim ayarlarını yapılandırmaya yük dengeleyici

Sanal makineler için zaman aşımı ayarlarını değiştirmek için PowerShell kullanabilirsiniz:

Bir sanal makine için Azure bir uç nokta ekleyin ve yük dengeleyici dağıtım modunu ayarlama

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution Sourceıp, 3-tanımlama grubu (kaynak IP, hedef IP Protokolü) Yük Dengeleme veya hiçbiri sourceIPProtocol 5-tanımlama grubu Yük Dengelemesi varsayılan davranışı istiyorsanız 2 bölütlü (kaynak IP, hedef IP) Yük Dengeleme için ayarlayabilirsiniz.

Bir uç nokta yük dengeleyici dağıtım modu yapılandırmayı almak için aşağıdakileri kullanın:

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

LoadBalancerDistribution öğesi mevcut değilse Azure yük dengeleyici varsayılan 5-tanımlama grubu algoritması kullanır.

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a>Bir yük dengeli uç nokta kümesi dağıtım modunu ayarlama

Uç nokta yük dengeli uç nokta kümesi parçası ise, dağıtım modu yük dengeli uç nokta kümesi ayarlamanız gerekir:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a>Dağıtım modunu değiştirmek için bulut hizmeti yapılandırması

Bulut hizmeti güncelleştirmek için 2.5 (Kasım'da yayımlanacak) .NET için Azure SDK'sı yararlanabilirsiniz. Bulut Hizmetleri için uç nokta ayarlar .csdef yapılır. Bulut Hizmetleri dağıtımı için yük dengeleyici dağıtım modu güncelleştirmek için bir dağıtım yükseltme gereklidir.
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

Hizmet Yönetimi API'si kullanılarak yük dengeleyici dağıtım yapılandırabilirsiniz. Eklediğinizden emin olun `x-ms-version` üstbilgisi sürüme ayarlandı `2014-09-01` ya da daha yüksek.

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a>Belirtilen yük dengeli kümesi bir dağıtımda yapılandırmasını güncelleştirme

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

LoadBalancerDistribution değeri 2 bölütlü benzeşimi, 3-tanımlama grubu benzeşimi sourceIPProtocol veya hiçbiri (için benzeşimi yok. Sourceıp olabilir yani 5-tanımlama grubu)

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
