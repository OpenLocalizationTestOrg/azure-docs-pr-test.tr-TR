---
title: "Azure Cloud Services için İç yük dengeleyicisi oluşturma | Microsoft Docs"
description: "Klasik dağıtım modelinde PowerShell kullanarak iç yük dengeleyici oluşturmayı öğrenin"
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
ms.openlocfilehash: 8dbc951416d577fa7f534c2eab1605c6bee61fce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="22bf9-103">Bulut hizmetleri için iç yük dengeleyici (klasik) oluşturmaya başlama</span><span class="sxs-lookup"><span data-stu-id="22bf9-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="22bf9-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22bf9-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="22bf9-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="22bf9-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="22bf9-106">Bulut hizmetleri</span><span class="sxs-lookup"><span data-stu-id="22bf9-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="22bf9-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="22bf9-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="22bf9-108">Bu makale klasik dağıtım modelini incelemektedir.</span><span class="sxs-lookup"><span data-stu-id="22bf9-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="22bf9-109">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="22bf9-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="22bf9-110">[Bu adımları Resource Manager modeli kullanarak gerçekleştirmeyi](load-balancer-get-started-ilb-arm-ps.md) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="22bf9-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="22bf9-111">Bulut hizmetleri için iç yük dengeleyiciyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="22bf9-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="22bf9-112">İç yük dengeleyici hem sanal makineler hem de bulut hizmetleri için desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="22bf9-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="22bf9-113">Bölgesel bir sanal ağın dışındaki bulut hizmetinde oluşturulmuş olan iç yük dengeleyici uç noktasına yalnızca bulut hizmetinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="22bf9-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span></span>

<span data-ttu-id="22bf9-114">İç yük dengeleyici yapılandırmasının aşağıdaki örnekte gösterilen şekilde bulut hizmetindeki ilk dağıtımın oluşturulması sırasında yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="22bf9-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22bf9-115">Aşağıdaki adımları çalıştırmanın ön koşulu, bulut dağıtımı için sanal ağ oluşturmuş olmaktır.</span><span class="sxs-lookup"><span data-stu-id="22bf9-115">A prerequisite to run the steps below is to have a virtual network already created for the cloud deployment.</span></span> <span data-ttu-id="22bf9-116">İç Yük Dengeleme oluşturmak için sanal ağ adına ve alt ağ adına ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="22bf9-116">You will need the virtual network name and subnet name to create the Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="22bf9-117">1. Adım</span><span class="sxs-lookup"><span data-stu-id="22bf9-117">Step 1</span></span>

<span data-ttu-id="22bf9-118">Bulut dağıtımınıza ait hizmet yapılandırma dosyasını (.cscfg) Visual Studio’da açın ve İç Yük Dengeleme oluşturmak için ağ yapılandırmasının son "`</Role>`" öğesinin altına aşağıdaki bölümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="22bf9-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="22bf9-119">Şimdi nasıl görüneceğini görmek için ağ yapılandırma dosyasına değerleri ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="22bf9-119">Let's add the values for the network configuration file to show how it will look.</span></span> <span data-ttu-id="22bf9-120">Bu örnekte test_subnet adına ve 10.0.0.0/24 alt ağına sahip, 10.0.0.4 statik IP numaralı ve "test_vnet" adlı bir VNet oluşturduğunuzu varsayın.</span><span class="sxs-lookup"><span data-stu-id="22bf9-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="22bf9-121">Yük dengeleyici testLB olarak adlandırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="22bf9-121">The load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="22bf9-122">Yük dengeleyici şeması hakkında daha fazla bilgi için bkz. [Yük dengeleyici ekleme](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="22bf9-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="22bf9-123">2. Adım</span><span class="sxs-lookup"><span data-stu-id="22bf9-123">Step 2</span></span>

<span data-ttu-id="22bf9-124">İç Yük Dengeleme uç noktalarını eklemek için hizmet tanımı (.csdef) dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="22bf9-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span></span> <span data-ttu-id="22bf9-125">Rol örneği oluşturulduğunda hizmet tanım dosyası rol örneklerini İç Yük Dengeleyiciye ekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="22bf9-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="22bf9-126">Yukarıdaki örnekteki değerleri kullanarak bu değerleri hizmet tanımı dosyasına ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="22bf9-126">Following the same values from the example above, let's add the values to the service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="22bf9-127">Ağ trafiği gelen isteklere için 80 numaralı bağlantı noktasını kullana e çalışan rolü örneklerini de 80 numaralı bağlantı noktasına gönderen testLB adlı yük dengeleyiciyi kullanarak yük dengeleme yapılacaktır.</span><span class="sxs-lookup"><span data-stu-id="22bf9-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22bf9-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="22bf9-128">Next steps</span></span>

[<span data-ttu-id="22bf9-129">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="22bf9-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="22bf9-130">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="22bf9-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

