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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="e8710-103">Merhaba dağıtım modunu yük dengeleyici için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e8710-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="e8710-104">Karma tabanlı dağıtım modu</span><span class="sxs-lookup"><span data-stu-id="e8710-104">Hash-based distribution mode</span></span>

<span data-ttu-id="e8710-105">Merhaba varsayılan dağıtım algoritmasıdır, 5-tanımlama grubu (kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası, protokol türü) toomap trafiği tooavailable sunucuları karma.</span><span class="sxs-lookup"><span data-stu-id="e8710-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="e8710-106">Bu, yalnızca bir aktarım oturumu içinde sürekliliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8710-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="e8710-107">Aynı oturum olacak hello paketlerinde aynı veri merkezi IP (DIP) örneği hello yük dengeli uç nokta toohello yönlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="e8710-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="e8710-108">Merhaba istemci başlatıldığında yeni bir oturum ile aynı kaynak IP Merhaba, hello kaynak bağlantı noktası değiştirir ve hello trafiği toogo tooa farklı DIP endpoint neden olur.</span><span class="sxs-lookup"><span data-stu-id="e8710-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![Karma tabanlı yük dengeleyici](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="e8710-110">Şekil 1-5-tanımlama grubu dağıtımı</span><span class="sxs-lookup"><span data-stu-id="e8710-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="e8710-111">Kaynak IP benzeşim modu</span><span class="sxs-lookup"><span data-stu-id="e8710-111">Source IP affinity mode</span></span>

<span data-ttu-id="e8710-112">Biz kaynak IP benzeşimi (oturum benzeşimi veya istemci IP benzeşim olarak da bilinir) adlı başka bir dağıtım moduna sahip.</span><span class="sxs-lookup"><span data-stu-id="e8710-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="e8710-113">3-tanımlama grubu (kaynak IP, hedef IP Protokolü) toomap trafiği toohello kullanılabilir sunuculara veya Azure yük dengeleyici yapılandırılmış toouse 2-tanımlama grubu (kaynak IP, hedef IP) olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8710-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="e8710-114">Kaynak IP benzeşimini kullanarak hello aynı başlatılan bağlantıları istemci bilgisayar gider toohello aynı DIP uç noktası.</span><span class="sxs-lookup"><span data-stu-id="e8710-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="e8710-115">Aşağıdaki diyagramda hello 2 bölütlü yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e8710-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="e8710-116">Ardından VM2 ve VM3 tarafından yedeklenen hello yük dengeleyici toovirtual makine 1 (VM1) aracılığıyla hello 2 bölütlü nasıl çalışacağını dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e8710-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![oturum benzeşimi](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="e8710-118">Şekil 2-2 bölütlü dağıtım</span><span class="sxs-lookup"><span data-stu-id="e8710-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="e8710-119">Kaynak IP benzeşim hello Azure yük dengeleyici ve Uzak Masaüstü (RD) ağ geçidi arasında bir uyumsuzluk çözer.</span><span class="sxs-lookup"><span data-stu-id="e8710-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="e8710-120">Şimdi tek bulut hizmetindeki bir RD Ağ Geçidi grubu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8710-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="e8710-121">Başka bir kullanım senaryosu burada hello veri yükleme UDP gerçekleşir ancak hello denetim düzlemi TCP ile elde edilen medya karşıya yükleme şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e8710-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="e8710-122">Bir istemci ilk ortak adres toohello yük dengeli bir TCP oturumu başlatır, sol etkin toomonitor hello bağlantı durumu belirli DIP, bu kanal olan yönlendirilmiş tooa alır</span><span class="sxs-lookup"><span data-stu-id="e8710-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="e8710-123">Aynı istemci bilgisayar hello yeni bir UDP oturumdan toohello başlatılan aynı yük dengeli ortak uç nokta, hello burada beklenir Bu bağlantı ayrıca yönlendirilmiş toohello olduğunu aynı DIP uç noktası hello önceki TCP bağlantısı olarak medyayı karşıya yükleme böylece olabilir yüksek verimlilik denetim kanalı TCP üzerinden de korurken yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="e8710-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="e8710-124">(Ekleyerek veya çıkararak bir sanal makine) bir yük dengeli kümesi değiştiğinde, istemci isteklerini hello dağıtımını yeniden.</span><span class="sxs-lookup"><span data-stu-id="e8710-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="e8710-125">Aynı hello sonlanır varolan istemcilerden gelen yeni bağlantıları bağlı olamazlar sunucu.</span><span class="sxs-lookup"><span data-stu-id="e8710-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="e8710-126">Ayrıca, kaynak IP kullanarak benzeşim dağıtım modu trafiğinin eşit olmayan bir dağıtım neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e8710-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="e8710-127">Proxy çalıştıran istemciler bir benzersiz istemci uygulaması olarak görülebilir.</span><span class="sxs-lookup"><span data-stu-id="e8710-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="e8710-128">İçin kaynak IP benzeşim ayarlarını yapılandırmaya yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="e8710-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="e8710-129">Sanal makineler için PowerShell toochange zaman aşımı ayarları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e8710-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="e8710-130">Azure uç noktası tooa sanal makine ekleyin ve yük dengeleyici dağıtım modunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="e8710-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="e8710-131">LoadBalancerDistribution toosourceIP, 3-tanımlama grubu (kaynak IP, hedef IP Protokolü) Yük Dengeleme veya hiçbiri sourceIPProtocol 5-tanımlama grubu Yük Dengelemesi hello varsayılan davranışı istiyorsanız 2 bölütlü (kaynak IP, hedef IP) Yük Dengeleme için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e8710-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="e8710-132">Tooretrieve bir uç nokta yük dengeleyici dağıtım modu yapılandırma aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e8710-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="e8710-133">Merhaba LoadBalancerDistribution öğesi mevcut değilse hello Azure yük dengeleyici hello varsayılan 5-tanımlama grubu algoritması kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8710-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="e8710-134">Yük dengeli uç nokta kümesi üzerindeki hello dağıtım modunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="e8710-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="e8710-135">Uç nokta yük dengeli uç nokta kümesi parçasıysa hello dağıtım modu hello yük dengeli uç nokta kümesi ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e8710-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="e8710-136">Bulut hizmeti yapılandırma toochange dağıtım modu</span><span class="sxs-lookup"><span data-stu-id="e8710-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="e8710-137">.NET 2.5 (Kasım'da yayımlanan toobe) için Azure SDK'sı hello yararlanabilirsiniz tooupdate bulut hizmetiniz.</span><span class="sxs-lookup"><span data-stu-id="e8710-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="e8710-138">Bulut Hizmetleri için uç nokta ayarlarını hello .csdef yapılır.</span><span class="sxs-lookup"><span data-stu-id="e8710-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="e8710-139">Sipariş tooupdate hello yük dengeleyici dağıtım modunda bulut Hizmetleri dağıtımı için dağıtım yükseltme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e8710-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="e8710-140">.Csdef değişiklikleri uç noktası ayarları için bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e8710-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="e8710-141">API örneği</span><span class="sxs-lookup"><span data-stu-id="e8710-141">API example</span></span>

<span data-ttu-id="e8710-142">Merhaba Hizmet Yönetimi API'si kullanılarak hello yük dengeleyici dağıtım yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8710-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="e8710-143">Tooadd hello emin olun `x-ms-version` üstbilgisi tooversion ayarlandı `2014-09-01` ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="e8710-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="e8710-144">Hello güncelleştirme hello yapılandırmasını Yük Dengelemesi yapılmış bir dağıtımda belirtildi.</span><span class="sxs-lookup"><span data-stu-id="e8710-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="e8710-145">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="e8710-145">Request example</span></span>

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

<span data-ttu-id="e8710-146">LoadBalancerDistribution başlangıç değeri 2 bölütlü benzeşimi, 3-tanımlama grubu benzeşimi sourceIPProtocol veya hiçbiri (için benzeşimi yok. Sourceıp olabilir</span><span class="sxs-lookup"><span data-stu-id="e8710-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="e8710-147">yani 5-tanımlama grubu)</span><span class="sxs-lookup"><span data-stu-id="e8710-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="e8710-148">Yanıt</span><span class="sxs-lookup"><span data-stu-id="e8710-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="e8710-149">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e8710-149">Next Steps</span></span>

[<span data-ttu-id="e8710-150">İç yük dengeleyiciye genel bakış</span><span class="sxs-lookup"><span data-stu-id="e8710-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="e8710-151">Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e8710-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="e8710-152">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e8710-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
