---
title: "Azure bulut Hizmetleri için bir iç yük dengeleyici aaaCreate | Microsoft Docs"
description: "Toocreate bir iç yük dengeleyici hello Klasik dağıtım modelinde PowerShell kullanarak nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="003e8-103">Bulut hizmetleri için iç yük dengeleyici (klasik) oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="003e8-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="003e8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="003e8-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="003e8-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="003e8-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="003e8-106">Bulut hizmetleri</span><span class="sxs-lookup"><span data-stu-id="003e8-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="003e8-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="003e8-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="003e8-108">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="003e8-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="003e8-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="003e8-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="003e8-110">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="003e8-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="003e8-111">Bulut hizmetleri için iç yük dengeleyiciyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="003e8-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="003e8-112">İç yük dengeleyici hem sanal makineler hem de bulut hizmetleri için desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="003e8-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="003e8-113">Bölgesel sanal ağ dışında bir bulut hizmetinde oluşturulan bir iç yük dengeleyici uç nokta yalnızca hello bulut hizmetinde erişilebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="003e8-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="003e8-114">Merhaba iç yük dengeleyici yapılandırması hello bulut hizmeti, ilk dağıtımda hello hello oluşturulması sırasında örnek hello aşağıda gösterildiği gibi ayarlamak toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="003e8-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="003e8-115">Bir önkoşul toorun hello adımları toohave zaten hello bulut dağıtımı için oluşturulan bir sanal ağ olur.</span><span class="sxs-lookup"><span data-stu-id="003e8-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="003e8-116">Sanal ağ adı ve alt ağ adı toocreate hello iç Yük Dengeleme hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="003e8-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="003e8-117">1. Adım</span><span class="sxs-lookup"><span data-stu-id="003e8-117">Step 1</span></span>

<span data-ttu-id="003e8-118">Visual Studio bulut dağıtımınız için hello hizmet yapılandırma dosyasının (.cscfg) açın ve son bölümü toocreate hello iç Yük Dengeleme hello altında aşağıdaki hello Ekle "`</Role>`" Merhaba ağ yapılandırması için öğesi.</span><span class="sxs-lookup"><span data-stu-id="003e8-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="003e8-119">Merhaba ağ yapılandırma dosyası tooshow nasıl görüneceğine hello değerlerini ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="003e8-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="003e8-120">Merhaba örnekte test_subnet ve statik bir IP 10.0.0.4 adlı bir 10.0.0.0/24 alt ağıyla "test_vnet" adlı bir VNet oluşturulan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="003e8-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="003e8-121">Merhaba yük dengeleyici testLB adlandırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="003e8-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="003e8-122">Merhaba yük dengeleyici şeması hakkında daha fazla bilgi için bkz: [Ekle yük dengeleyici](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="003e8-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="003e8-123">2. Adım</span><span class="sxs-lookup"><span data-stu-id="003e8-123">Step 2</span></span>

<span data-ttu-id="003e8-124">Merhaba hizmet açıklaması (.csdef) dosya tooadd uç noktaları toohello iç Yük Dengeleme değiştirin.</span><span class="sxs-lookup"><span data-stu-id="003e8-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="003e8-125">Merhaba şu anda bir rol örneği oluşturulur, hello hizmet tanımı dosyası hello rol örnekleri toohello iç Yük Dengeleme ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="003e8-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="003e8-126">Örnek hello yukarıdaki değerlerini aynı hello hello değerleri toohello hizmet tanımı dosyası ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="003e8-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="003e8-127">Merhaba ağ trafiğini tooworker rol örneklerine de bağlantı noktası 80 üzerinde gönderme gelen istekler için 80 numaralı bağlantı noktasını kullanarak hello testLB yük dengeleyici kullanılarak Yük Dengeleme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="003e8-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="003e8-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="003e8-128">Next steps</span></span>

[<span data-ttu-id="003e8-129">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="003e8-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="003e8-130">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="003e8-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

