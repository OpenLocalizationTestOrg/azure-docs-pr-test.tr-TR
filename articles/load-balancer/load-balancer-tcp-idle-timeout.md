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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="b2e5e-103">Azure yük dengeleyici için TCP boşta kalma zaman aşımı ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b2e5e-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="b2e5e-104">Varsayılan yapılandırmasında, Azure yük dengeleyici, 4 dakikalık bir boşta kalma zaman aşımı ayarının.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="b2e5e-105">Bir süre işlem yapılmadığında hello zaman aşımı değeri uzun olması durumunda, TCP hello garantisi yoktur veya HTTP oturumu hello istemci ile bulut hizmetiniz arasında korunur.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="b2e5e-106">Merhaba bağlantı kapalı olduğunda istemci uygulamanızı hello aşağıdaki hata iletisini alabilirsiniz: "Merhaba temel alınan bağlantı kapatıldı: Canlı tutulur toobe hello sunucu tarafından kapatıldı bekleniyordu bir bağlantı."</span><span class="sxs-lookup"><span data-stu-id="b2e5e-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="b2e5e-107">Toouse TCP tutma yaygın bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="b2e5e-108">Bu uygulama için daha uzun bir süre hello bağlantıyı etkin tutar.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="b2e5e-109">Daha fazla bilgi için bkz: [.NET örnekleri](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2e5e-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="b2e5e-110">Tutma etkin, paketleri hello bağlantıda kaldıktan dönemlerde gönderilir.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="b2e5e-111">Bu tutma paketler hello boşta kalma zaman aşımı değeri hiçbir zaman ulaşıldığında ve hello bağlantısı uzun bir süre boyunca tutulur emin olun.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="b2e5e-112">Bu ayar yalnızca gelen bağlantılar için çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="b2e5e-113">tooavoid kaybeden hello bağlantı hello boşta kalma zaman aşımı ayarını veya artış hello boşta kalma zaman aşımı değeri'den bir aralık ile Merhaba TCP tutma yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="b2e5e-114">toosupport bu senaryolara yapılandırılabilir boşta kalma zaman aşımı için destek ekledik.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="b2e5e-115">Şimdi 4 too30 dakika süresince ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="b2e5e-116">TCP tutma iyi pil ömrünün bir kısıtlaması olduğu senaryolar için çalışır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="b2e5e-117">Mobil uygulamalar için önerilmez.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="b2e5e-118">Bir mobil uygulama tutma bir TCP kullanarak hello aygıt pil daha hızlı tükenir.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![TCP zaman aşımı](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="b2e5e-120">Aşağıdaki bölümlerde hello nasıl toochange boşta kalma zaman aşımı ayarları sanal makineler ve bulut Hizmetleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="b2e5e-121">Merhaba TCP zaman aşımı, örnek düzeyinde ortak IP too15 dakika için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2e5e-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="b2e5e-122">`IdleTimeoutInMinutes` isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="b2e5e-123">Ayarlanmazsa, varsayılan zaman aşımı hello 4 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="b2e5e-124">Merhaba kabul edilebilir zaman aşımı aralığı 4 too30 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="b2e5e-125">Azure bir uç nokta bir sanal makinede oluştururken Hello boşta kalma zaman aşımını ayarlama</span><span class="sxs-lookup"><span data-stu-id="b2e5e-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="b2e5e-126">toochange zaman aşımı için bir uç nokta ayarlama Merhaba, hello aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="b2e5e-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="b2e5e-127">tooretrieve boşta kalma zaman aşımı yapılandırmanıza, komutu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="b2e5e-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="b2e5e-128">Merhaba TCP zaman aşımı üzerinde bir yük dengeli uç nokta kümesi</span><span class="sxs-lookup"><span data-stu-id="b2e5e-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="b2e5e-129">Uç nokta yük dengeli uç nokta kümesi parçasıysa hello TCP zaman aşımı hello yük dengeli uç nokta kümesi ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="b2e5e-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="b2e5e-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="b2e5e-131">Bulut Hizmetleri zaman aşımı ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="b2e5e-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="b2e5e-132">Bulut hizmetinizi hello Azure SDK'sı tooupdate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="b2e5e-133">Bulut Hizmetleri için uç nokta ayarlarını hello .csdef dosyasında yapın.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="b2e5e-134">Bir bulut hizmeti dağıtımının Hello TCP zaman aşımı güncelleştirme dağıtımı yükseltme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="b2e5e-135">Merhaba TCP zaman aşımı yalnızca genel IP için belirtilmezse dışındadır.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="b2e5e-136">Genel IP ayarlarını hello .cscfg dosyasında yer alır ve bunları dağıtım güncelleştirme ve yükseltme güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="b2e5e-137">uç noktası ayarları için Hello .csdef değişiklikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b2e5e-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="b2e5e-138">Merhaba zaman aşımı ayarını genel IP'ler için Hello .cscfg değişiklikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b2e5e-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="b2e5e-139">REST API örneği</span><span class="sxs-lookup"><span data-stu-id="b2e5e-139">REST API example</span></span>

<span data-ttu-id="b2e5e-140">Merhaba TCP boşta kalma zaman aşımı hello Hizmet Yönetimi API kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="b2e5e-141">Bu hello emin olun `x-ms-version` üstbilgisi tooversion ayarlandı `2014-06-01` veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="b2e5e-142">Merhaba belirtilen hello yapılandırmasını yük dengeli bir dağıtımdaki tüm sanal makinelerde giriş uç noktaları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b2e5e-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="b2e5e-143">İstek</span><span class="sxs-lookup"><span data-stu-id="b2e5e-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="b2e5e-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="b2e5e-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b2e5e-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2e5e-145">Next steps</span></span>

[<span data-ttu-id="b2e5e-146">İç yük dengeleyiciye genel bakış</span><span class="sxs-lookup"><span data-stu-id="b2e5e-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="b2e5e-147">Bir Internet'e yönelik Yük Dengeleyici yapılandırma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b2e5e-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="b2e5e-148">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b2e5e-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
