---
title: "Azure cloud services için İnternet’e yönelik yük dengeleyicisi oluşturma | Microsoft Docs"
description: "Klasik dağıtımda bulut hizmetleri için İnternet’e yönelik yük dengeleyici oluşturmayı öğrenin"
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
ms.openlocfilehash: 1ceaafebcaebecb04314c7da62c69b2e9b5ba39a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="99d1e-103">Bulut hizmetleri için İnternet’e yönelik yük dengeleyici oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="99d1e-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="99d1e-104">Klasik Azure portalı</span><span class="sxs-lookup"><span data-stu-id="99d1e-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="99d1e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99d1e-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="99d1e-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="99d1e-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="99d1e-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="99d1e-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="99d1e-108">Azure kaynaklarıyla çalışmadan önce Azure’da şu anda iki dağıtım modeli olduğunu anlamak önemlidir: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="99d1e-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="99d1e-109">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="99d1e-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="99d1e-110">Bu makalenin en üstündeki sekmelere tıklayarak farklı araçlarla ilgili belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d1e-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="99d1e-111">Bu makale, klasik dağıtım modelini kapsamaktadır.</span><span class="sxs-lookup"><span data-stu-id="99d1e-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="99d1e-112">[Azure Resource Manager kullanarak İnternet’e yönelik yük dengeleyici oluşturma](load-balancer-get-started-internet-arm-ps.md) sayfasını da inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d1e-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="99d1e-113">Bulut hizmetleri yük dengeleyici ile otomatik olarak yapılandırılır ve hizmet modeliyle özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="99d1e-113">Cloud services are automatically configured with a load balancer and can be customized via the service model.</span></span>

## <a name="create-a-load-balancer-using-the-service-definition-file"></a><span data-ttu-id="99d1e-114">Hizmet tanım dosyası kullanarak yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="99d1e-114">Create a load balancer using the service definition file</span></span>

<span data-ttu-id="99d1e-115">Bulut hizmetinizi güncelleştirme amacıyla .NET 2.5 için Azure SDK kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d1e-115">You can leverage the Azure SDK for .NET 2.5 to update your cloud service.</span></span> <span data-ttu-id="99d1e-116">Bulut hizmetleri için uç nokta ayarları [servicedefinition](https://msdn.microsoft.com/library/azure/gg557553.aspx).csdef dosyasında yapılır.</span><span class="sxs-lookup"><span data-stu-id="99d1e-116">Endpoint settings for cloud services are made in the [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="99d1e-117">Aşağıdaki örnekte servicedefinition.csdef dosyasının bir bulut dağıtımı için nasıl yapılandırıldığı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="99d1e-117">The following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="99d1e-118">Bir bulut dağıtımı tarafından oluşturulmuş .csdef dosyası parçacığını denetlediğinizde, dış uç noktanın 10000, 10001 ve 10002 numaralı bağlantı noktaları üzerinde HTTP bağlantı noktalarını kullanacak şekilde yapılandırıldığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d1e-118">Checking the snippet for the .csdef file generated by a cloud deployment, you can see the external endpoint configured to use ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="99d1e-119">Bulut hizmetleri için yük dengeleyici sistem durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="99d1e-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="99d1e-120">Aşağıda bir sistem durumu araştırma örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="99d1e-120">The following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="99d1e-121">Yük dengeleyici uç nokta bilgilerini ve araştırma bilgilerini kullanarak sistem durumunu sorgulamak için kullanılabilecek `http://{DIP of VM}:80/Probe.aspx` biçiminde bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99d1e-121">The load balancer combines the information of the endpoint and the information of the probe to create a URL in the form of `http://{DIP of VM}:80/Probe.aspx` that can be used to query the health of the service.</span></span>

<span data-ttu-id="99d1e-122">Hizmet aynı IP adresinden gelen aralıklı araştırmaları algılar.</span><span class="sxs-lookup"><span data-stu-id="99d1e-122">The service detects periodic probes from the same IP address.</span></span> <span data-ttu-id="99d1e-123">Bu, sanal makinenin çalıştığı düğümün ana bilgisayarından gelen sistem durumu araştırma isteğidir.</span><span class="sxs-lookup"><span data-stu-id="99d1e-123">This is the health probe request coming from the host of the node where the virtual machine is running.</span></span> <span data-ttu-id="99d1e-124">Yük dengeleyicinin, hizmetin iyi durumda olduğunu kabul etmesi için hizmetin HTTP 200 durum koduyla yanıt vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="99d1e-124">The service has to respond with a HTTP 200 status code for the load balancer to assume that the service is healthy.</span></span> <span data-ttu-id="99d1e-125">Diğer tüm HTTP durum kodları (503 gibi) sanal makineyi sistemin dışında bırakır.</span><span class="sxs-lookup"><span data-stu-id="99d1e-125">Any other HTTP status code (for example 503) directly takes the virtual machine out of rotation.</span></span>

<span data-ttu-id="99d1e-126">Araştırma tanımı ayrıca araştırma sıklığını da denetler.</span><span class="sxs-lookup"><span data-stu-id="99d1e-126">The probe definition also controls the frequency of the probe.</span></span> <span data-ttu-id="99d1e-127">Yukarıdaki durumda yük dengeleyici uç noktayı 5 saniyede bir araştırmaktadır.</span><span class="sxs-lookup"><span data-stu-id="99d1e-127">In our case above, the load balancer is probing the endpoint every 5 secs.</span></span> <span data-ttu-id="99d1e-128">10 saniye (iki araştırma aralığı) boyunca olumlu yanıt gelmemesi halinde araştırma sonucu olumsuz kabul edilir ve sanal makine sistemin dışında tutulur.</span><span class="sxs-lookup"><span data-stu-id="99d1e-128">If no positive answer is received for 10 secs (two probe intervals), the probe is assumed down, and the virtual machine is taken out of rotation.</span></span> <span data-ttu-id="99d1e-129">Benzer şekilde, hizmetin sistem dışında tutulması sırasında olumlu yanıt alınması halinde hizmet yeniden devreye alınır.</span><span class="sxs-lookup"><span data-stu-id="99d1e-129">Similarly, if the service is out of rotation and a positive answer is received, the service is put back to rotation right away.</span></span> <span data-ttu-id="99d1e-130">Hizmet durumu sağlam ve sağlam değil şeklinde değişiklik gösteriyorsa yük dengeleyici, hizmetin birkaç araştırma boyunca sağlam olduğunu algılaması halinde hizmetin devreye alınmasını geciktirmeye karar verebilir.</span><span class="sxs-lookup"><span data-stu-id="99d1e-130">If the service is fluctuating between healthy and unhealthy, the load balancer can decide to delay the re-introduction of the service back to rotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="99d1e-131">Daha fazla bilgi için [sistem durumu araştırması](https://msdn.microsoft.com/library/azure/jj151530.aspx) hizmet tanım düzenini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="99d1e-131">Check the service definition schema for the [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99d1e-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99d1e-132">Next steps</span></span>

[<span data-ttu-id="99d1e-133">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="99d1e-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="99d1e-134">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="99d1e-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="99d1e-135">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="99d1e-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

