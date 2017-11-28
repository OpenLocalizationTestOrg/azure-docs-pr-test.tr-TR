---
title: "Azure bulut Hizmetleri için aaaCreate bir Internet'e yönelik Yük Dengeleyici | Microsoft Docs"
description: "Nasıl toocreate Internet'e yönelik Yük Dengeleyici bulut Hizmetleri için Klasik dağıtım modelinde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="a5099-103">Bulut hizmetleri için İnternet’e yönelik yük dengeleyici oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a5099-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a5099-104">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="a5099-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="a5099-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5099-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="a5099-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a5099-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="a5099-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a5099-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="a5099-108">Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="a5099-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a5099-109">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a5099-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="a5099-110">Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5099-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="a5099-111">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="a5099-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="a5099-112">Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Azure Resource Manager kullanarak bilgi](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="a5099-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="a5099-113">Bulut Hizmetleri, bir yük dengeleyici ile otomatik olarak yapılandırılır ve hello hizmet modeli özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a5099-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="a5099-114">Merhaba hizmet tanımı dosyası kullanarak bir yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5099-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="a5099-115">.NET 2.5 tooupdate için Azure SDK'sı Merhaba, bulut hizmetinden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5099-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="a5099-116">Bulut Hizmetleri için uç nokta ayarlarını hello yapılan [hizmet tanımı](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef dosyası.</span><span class="sxs-lookup"><span data-stu-id="a5099-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="a5099-117">Merhaba aşağıdaki örnek bir bulut dağıtımı için bir servicedefinition.csdef dosyası nasıl yapılandırıldığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="a5099-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="a5099-118">Bulut dağıtım tarafından oluşturulan hello .csdef dosyası için Hello parçacığı denetimi, 10000, 10001 ve 10002 bağlantı noktası hello yapılandırılan dış uç noktası toouse bağlantı noktaları HTTP görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5099-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="a5099-119">Bulut hizmetleri için yük dengeleyici sistem durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="a5099-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="a5099-120">Merhaba, bir sistem durumu araştırması örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="a5099-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="a5099-121">Merhaba yük dengeleyici hello araştırma toocreate hello uç noktasının hello bilgileri ve hello hello biçiminde bir URL birleştirir `http://{DIP of VM}:80/Probe.aspx` kullanılan tooquery hello hello hizmet durumunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="a5099-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="a5099-122">Merhaba hizmeti algılar hello gelen düzenli araştırmalar aynı IP adresi.</span><span class="sxs-lookup"><span data-stu-id="a5099-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="a5099-123">Merhaba sanal makinenin çalıştığı hello düğümü hello ana bilgisayardan gelen hello sistem durumu araştırma isteğinin budur.</span><span class="sxs-lookup"><span data-stu-id="a5099-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="a5099-124">Merhaba hizmeti hello hizmet sağlıklı olduğunu hello yük dengeleyici tooassume için bir HTTP 200 durum koduyla toorespond sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a5099-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="a5099-125">Sanal makineyi döndürme dışına alır hello doğrudan diğer HTTP durum kodu (örneğin 503).</span><span class="sxs-lookup"><span data-stu-id="a5099-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="a5099-126">Merhaba araştırma tanımı da hello araştırma hello sıklığını denetler.</span><span class="sxs-lookup"><span data-stu-id="a5099-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="a5099-127">Örneğimizde yukarıdaki hello yük dengeleyici hello uç nokta her 5 saniye yoklama.</span><span class="sxs-lookup"><span data-stu-id="a5099-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="a5099-128">10 saniye (iki yoklama aralıkları) olumlu bir yanıt alınmazsa, hello araştırma aşağı kabul edilir ve hello sanal makine dışına döndürme alınır.</span><span class="sxs-lookup"><span data-stu-id="a5099-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="a5099-129">Benzer şekilde, döndürme dışında hello hizmetidir ve olumlu bir yanıt alındı, hello hizmeti geri toorotation hemen yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a5099-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="a5099-130">Merhaba hizmeti arasında sağlıklı ve sağlıksız dalgalı, araştırmalar sayısı için sağlıklı bırakıldı kadar hello yük dengeleyici toodelay hello yeniden giriş hello hizmeti geri toorotation karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5099-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="a5099-131">Hello için Hello hizmet tanımı şemayı denetle [durumu araştırması](https://msdn.microsoft.com/library/azure/jj151530.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a5099-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5099-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a5099-132">Next steps</span></span>

[<span data-ttu-id="a5099-133">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="a5099-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="a5099-134">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a5099-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a5099-135">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a5099-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

