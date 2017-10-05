---
title: Azure Service Fabric ters proxy | Microsoft Docs
description: "Service Fabric'ın ters proxy mikro içinden ve dışından küme iletişimi için kullanın."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 7897458e9e4a0bbe185bd3f7b4c133c1b26769f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="a4db8-103">Azure Service Fabric ters proxy</span><span class="sxs-lookup"><span data-stu-id="a4db8-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="a4db8-104">Azure Service Fabric yerleşik ters proxy HTTP uç noktaları sunan Service Fabric kümesindeki mikro giderir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-104">The reverse proxy that's built into Azure Service Fabric addresses microservices in the Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="a4db8-105">Mikro iletişim modelini</span><span class="sxs-lookup"><span data-stu-id="a4db8-105">Microservices communication model</span></span>
<span data-ttu-id="a4db8-106">Service Fabric mikro genellikle bir alt küme içindeki sanal makinelerin çalışır ve bir sanal makineden diğerine çeşitli nedenlerle taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4db8-106">Microservices in Service Fabric typically run on a subset of virtual machines in the cluster and can move from one virtual machine to another for various reasons.</span></span> <span data-ttu-id="a4db8-107">Bu nedenle, mikro için bitiş noktalarını dinamik olarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4db8-107">So, the endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="a4db8-108">Mikro hizmet için iletişim kurmak için genel bir desen aşağıdaki çözümleme döngü şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a4db8-108">The typical pattern to communicate to the microservice is the following resolve loop:</span></span>

1. <span data-ttu-id="a4db8-109">Başlangıçta adlandırma hizmeti aracılığıyla hizmet konumu çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="a4db8-109">Resolve the service location initially through the naming service.</span></span>
2. <span data-ttu-id="a4db8-110">Hizmetine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a4db8-110">Connect to the service.</span></span>
3. <span data-ttu-id="a4db8-111">Bağlantı hataları nedenini ve hizmet konumu gerektiğinde yeniden çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="a4db8-111">Determine the cause of connection failures, and resolve the service location again when necessary.</span></span>

<span data-ttu-id="a4db8-112">Bu işlem genellikle istemci-tarafı iletişim hizmeti çözümleme ve Yeniden Dene'yi ilkeleri uygulayan bir yeniden deneme döngüsüne kitaplıklarında kaydırma içerir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements the service resolution and retry policies.</span></span>
<span data-ttu-id="a4db8-113">Daha fazla bilgi için bkz: [Bağlan ve Hizmetleri ile iletişim](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="a4db8-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-the-reverse-proxy"></a><span data-ttu-id="a4db8-114">Ters proxy kullanarak iletişim</span><span class="sxs-lookup"><span data-stu-id="a4db8-114">Communicating by using the reverse proxy</span></span>
<span data-ttu-id="a4db8-115">Kümedeki tüm düğümlerde ters proxy Service Fabric içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a4db8-115">The reverse proxy in Service Fabric runs on all the nodes in the cluster.</span></span> <span data-ttu-id="a4db8-116">Bir istemcinin adına tüm hizmet çözümleme işlemi gerçekleştirir ve ardından istemci isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-116">It performs the entire service resolution process on a client's behalf and then forwards the client request.</span></span> <span data-ttu-id="a4db8-117">Bu nedenle, küme üzerinde çalışan istemciler aynı düğümde yerel olarak çalıştırılan ters proxy kullanarak hedef hizmete anlaşmak için tüm istemci-tarafı HTTP iletişim kitaplıkları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4db8-117">So, clients that run on the cluster can use any client-side HTTP communication libraries to talk to the target service by using the reverse proxy that runs locally on the same node.</span></span>

![İç iletişim][1]

## <a name="reaching-microservices-from-outside-the-cluster"></a><span data-ttu-id="a4db8-119">Mikro hizmetler küme dışındaki ulaşmasını</span><span class="sxs-lookup"><span data-stu-id="a4db8-119">Reaching microservices from outside the cluster</span></span>
<span data-ttu-id="a4db8-120">Varsayılan dış iletişim modelini mikro için burada her hizmetin doğrudan dış istemcilerden erişilemez bir katılımı modelidir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-120">The default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="a4db8-121">[Azure yük dengeleyici](../load-balancer/load-balancer-overview.md), mikro dış istemcileri arasındaki bir ağ sınırında olduğu ağ adresi çevirisi gerçekleştirir ve iç IP: BağlantıNoktası uç noktaları dış isteklerini iletir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests to internal IP:port endpoints.</span></span> <span data-ttu-id="a4db8-122">Mikro hizmet ait uç nokta dış istemcilere doğrudan erişilebilir olması için ilk küme hizmetinin kullandığı her bağlantı noktası trafik iletmek için yük dengeleyici yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-122">To make a microservice's endpoint directly accessible to external clients, you must first configure Load Balancer to forward traffic to each port that the service uses in the cluster.</span></span> <span data-ttu-id="a4db8-123">Ayrıca, çoğu mikro, özellikle durum bilgisi olan mikro kümenin tüm düğümlerinde dinamik yok.</span><span class="sxs-lookup"><span data-stu-id="a4db8-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of the cluster.</span></span> <span data-ttu-id="a4db8-124">Mikro yük devretme düğümlerinde arasında taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4db8-124">The microservices can move between nodes on failover.</span></span> <span data-ttu-id="a4db8-125">Böyle durumlarda, yük dengeleyici etkin olduğu trafiği ileterek çoğaltmalarının hedef düğüm konumu belirlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="a4db8-125">In such cases, Load Balancer cannot effectively determine the location of the target node of the replicas to which it should forward traffic.</span></span>

### <a name="reaching-microservices-via-the-reverse-proxy-from-outside-the-cluster"></a><span data-ttu-id="a4db8-126">Küme dışında ters proxy sunucudan aracılığıyla mikro ulaşmasını</span><span class="sxs-lookup"><span data-stu-id="a4db8-126">Reaching microservices via the reverse proxy from outside the cluster</span></span>
<span data-ttu-id="a4db8-127">Yük dengeleyicisi bir bireysel hizmet bağlantı noktasını yapılandırmak yerine, yük dengeleyici yalnızca ters Ara sunucu bağlantı noktasını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4db8-127">Instead of configuring the port of an individual service in Load Balancer, you can configure just the port of the reverse proxy in Load Balancer.</span></span> <span data-ttu-id="a4db8-128">Bu yapılandırma, kümenin dışındaki istemcilerin ek yapılandırma olmadan ters proxy kullanarak küme içindeki hizmetlere erişmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4db8-128">This configuration lets clients outside the cluster reach services inside the cluster by using the reverse proxy without additional configuration.</span></span>

![Dış iletişimi][0]

> [!WARNING]
> <span data-ttu-id="a4db8-130">Yük dengeleyicisi öğesi ters proxy bağlantı noktası yapılandırdığınızda, bir HTTP uç noktası kullanıma tüm mikro kümedeki küme dışında adreslenebilir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-130">When you configure the reverse proxy's port in Load Balancer, all microservices in the cluster that expose an HTTP endpoint are addressable from outside the cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-the-reverse-proxy"></a><span data-ttu-id="a4db8-131">Ters proxy kullanarak Hizmetleri adresleme için URI biçimi</span><span class="sxs-lookup"><span data-stu-id="a4db8-131">URI format for addressing services by using the reverse proxy</span></span>
<span data-ttu-id="a4db8-132">Ters proxy gelen istek iletilmesi gereken hizmet bölümü tanımlamak için belirli bir Tekdüzen Kaynak Tanımlayıcısı (URI) biçimi kullanır:</span><span class="sxs-lookup"><span data-stu-id="a4db8-132">The reverse proxy uses a specific uniform resource identifier (URI) format to identify the service partition to which the incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="a4db8-133">**http (s):** ters proxy HTTP veya HTTPS trafiğini kabul edecek şekilde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-133">**http(s):** The reverse proxy can be configured to accept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="a4db8-134">HTTPS iletme için başvurmak [güvenli hizmetine ters proxy ile bağlanma](service-fabric-reverseproxy-configure-secure-communication.md) HTTPS üzerinde dinlemek için ters proxy ayarladıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="a4db8-134">For HTTPS forwarding, refer to [Connect to a secure service with the reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup to listen on HTTPS.</span></span>
* <span data-ttu-id="a4db8-135">**Küme tam etki alanı adı (FQDN) | iç IP:** dış istemcileri için böylece mycluster.eastus.cloudapp.azure.com gibi küme etki alanıyla üzerinden erişilebilen ters proxy yapılandırabilirsiniz. Varsayılan olarak, ters proxy her düğüm üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a4db8-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure the reverse proxy so that it is reachable through the cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, the reverse proxy runs on every node.</span></span> <span data-ttu-id="a4db8-136">İç trafiği için ters proxy 10.0.0.1 gibi herhangi bir iç düğüm IP'yi veya localhost üzerinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-136">For internal traffic, the reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="a4db8-137">**Bağlantı noktası:** için ters proxy belirtilen gibi bağlantı noktası 19081, budur.</span><span class="sxs-lookup"><span data-stu-id="a4db8-137">**Port:** This is the port, such as 19081, that has been specified for the reverse proxy.</span></span>
* <span data-ttu-id="a4db8-138">**ServiceInstanceName:** olmadan Ulaşmaya çalıştığınız dağıtılan hizmet örneği tam adını budur "fabric: /" düzeni.</span><span class="sxs-lookup"><span data-stu-id="a4db8-138">**ServiceInstanceName:** This is the fully-qualified name of the deployed service instance that you are trying to reach without the "fabric:/" scheme.</span></span> <span data-ttu-id="a4db8-139">Örneğin, ulaşmak için *fabric: / myapp/myservice/* hizmeti, kullandığınız *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="a4db8-139">For example, to reach the *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="a4db8-140">Hizmet örneği adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a4db8-140">The service instance name is case-sensitive.</span></span> <span data-ttu-id="a4db8-141">URL'de hizmet örnek adı için farklı büyük/küçük harf kullanarak 404 ile (bulunamadı) yapılan isteklerin başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="a4db8-141">Using a different casing for the service instance name in the URL causes the requests to fail with 404 (Not Found).</span></span>
* <span data-ttu-id="a4db8-142">**Sonek yol:** gerçek URL yolu gibi budur *myapi/değerleri/ekleme/3*, bağlanmak istediğiniz hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a4db8-142">**Suffix path:** This is the actual URL path, such as *myapi/values/add/3*, for the service that you want to connect to.</span></span>
* <span data-ttu-id="a4db8-143">**PartitionKey:** bölümlenmiş bir hizmet için bu hesaplanan bölüm erişmek istediğiniz bölümün anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="a4db8-143">**PartitionKey:** For a partitioned service, this is the computed partition key of the partition that you want to reach.</span></span> <span data-ttu-id="a4db8-144">Bu Not *değil* bölüm kimliği GUID.</span><span class="sxs-lookup"><span data-stu-id="a4db8-144">Note that this is *not* the partition ID GUID.</span></span> <span data-ttu-id="a4db8-145">Bu parametre tek bölüm düzeni kullanan Hizmetleri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-145">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="a4db8-146">**PartitionKind:** hizmet bölüm düzeni budur.</span><span class="sxs-lookup"><span data-stu-id="a4db8-146">**PartitionKind:** This is the service partition scheme.</span></span> <span data-ttu-id="a4db8-147">Bu, 'Int64Range' veya 'Adlı' olabilir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="a4db8-148">Bu parametre tek bölüm düzeni kullanan Hizmetleri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-148">This parameter is not required for services that use the singleton partition scheme.</span></span>
* <span data-ttu-id="a4db8-149">**ListenerName** hizmet uç noktaları biçimidir {"Bitiş": {"Listener1": "Bitiş noktası 1", "Listener2": "Endpoint2"...}}.</span><span class="sxs-lookup"><span data-stu-id="a4db8-149">**ListenerName** The endpoints from the service are of the form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="a4db8-150">Hizmet birden çok uç nokta gösterir, bu istemci isteği iletilmesi gereken uç nokta tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a4db8-150">When the service exposes multiple endpoints, this identifies the endpoint that the client request should be forwarded to.</span></span> <span data-ttu-id="a4db8-151">Bu hizmet yalnızca bir dinleyici varsa atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-151">This can be omitted if the service has only one listener.</span></span>
* <span data-ttu-id="a4db8-152">**TargetReplicaSelector** bu hedef çoğaltma veya örnek nasıl seçili belirtir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-152">**TargetReplicaSelector** This specifies how the target replica or instance should be selected.</span></span>
  * <span data-ttu-id="a4db8-153">Hedef hizmet durum bilgisi olan olduğunda TargetReplicaSelector şunlardan biri olabilir: 'PrimaryReplica', 'RandomSecondaryReplica' veya 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="a4db8-153">When the target service is stateful, the TargetReplicaSelector can be one of the following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="a4db8-154">Bu parametre belirtilmediğinde, varsayılan değer 'PrimaryReplica' dir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-154">When this parameter is not specified, the default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="a4db8-155">Hedef hizmet durum bilgisiz olduğunda ters proxy isteği iletmek için hizmet bölüm rastgele bir örneğini seçer.</span><span class="sxs-lookup"><span data-stu-id="a4db8-155">When the target service is stateless, reverse proxy picks a random instance of the service partition to forward the request to.</span></span>
* <span data-ttu-id="a4db8-156">**Zaman aşımı:** bu istemci istek adına hizmeti için ters proxy tarafından oluşturulan HTTP isteği için zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-156">**Timeout:**  This specifies the timeout for the HTTP request created by the reverse proxy to the service on behalf of the client request.</span></span> <span data-ttu-id="a4db8-157">Varsayılan değer 60 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-157">The default value is 60 seconds.</span></span> <span data-ttu-id="a4db8-158">Bu isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="a4db8-159">Örnek Kullanım</span><span class="sxs-lookup"><span data-stu-id="a4db8-159">Example usage</span></span>
<span data-ttu-id="a4db8-160">Örnek olarak, atalım *fabric: / MyApp/MyService* aşağıdaki URL'yi bir HTTP dinleyicisini açar hizmeti:</span><span class="sxs-lookup"><span data-stu-id="a4db8-160">As an example, let's take the *fabric:/MyApp/MyService* service that opens an HTTP listener on the following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="a4db8-161">Hizmet için kaynakları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a4db8-161">Following are the resources for the service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="a4db8-162">Hizmet, bölümleme singleton kullanıyorsa *PartitionKey* ve *PartitionKind* sorgu dizesi parametreleri gerekli değildir ve ağ geçidi olarak kullanarak hizmet erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="a4db8-162">If the service uses the singleton partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters are not required, and the service can be reached by using the gateway as:</span></span>

* <span data-ttu-id="a4db8-163">Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="a4db8-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="a4db8-164">Dahili olarak:`http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="a4db8-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="a4db8-165">Hizmet Tekdüzen Int64 bölümleme düzeni kullanıyorsa *PartitionKey* ve *PartitionKind* sorgu dizesi parametreleri kullanılan, hizmetin bir bölüm ulaşmak için:</span><span class="sxs-lookup"><span data-stu-id="a4db8-165">If the service uses the Uniform Int64 partitioning scheme, the *PartitionKey* and *PartitionKind* query string parameters must be used to reach a partition of the service:</span></span>

* <span data-ttu-id="a4db8-166">Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a4db8-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="a4db8-167">Dahili olarak:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a4db8-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="a4db8-168">Hizmet sunan kaynaklara ulaşmak için basitçe URL'de hizmet adından sonra kaynak yolu yerleştir:</span><span class="sxs-lookup"><span data-stu-id="a4db8-168">To reach the resources that the service exposes, simply place the resource path after the service name in the URL:</span></span>

* <span data-ttu-id="a4db8-169">Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a4db8-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="a4db8-170">Dahili olarak:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a4db8-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="a4db8-171">Ağ geçidi, ardından bu istekleri hizmetin URL'sine iletir:</span><span class="sxs-lookup"><span data-stu-id="a4db8-171">The gateway will then forward these requests to the service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="a4db8-172">Bağlantı noktası paylaşımı için bir özel işleme Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a4db8-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="a4db8-173">Azure uygulama ağ geçidi hizmeti adresi yeniden çözün ve bir hizmet erişildiğinde isteği yeniden deneyin dener.</span><span class="sxs-lookup"><span data-stu-id="a4db8-173">Azure Application Gateway attempts to resolve a service address again and retry the request when a service cannot be reached.</span></span> <span data-ttu-id="a4db8-174">Kendi hizmet çözümlemesi uygulamak ve döngüsü çözmek istemci kodu gereksinimi olmadığından önemli bir avantajı uygulama ağ geçidi budur.</span><span class="sxs-lookup"><span data-stu-id="a4db8-174">This is a major benefit of Application Gateway because client code does not need to implement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="a4db8-175">Genellikle, ne zaman bir hizmet, farklı bir düğüme, normal yaşam döngüsü kapsamında taşınmış hizmet örneği veya çoğaltma erişilemiyor.</span><span class="sxs-lookup"><span data-stu-id="a4db8-175">Generally, when a service cannot be reached, the service instance or replica has moved to a different node as part of its normal lifecycle.</span></span> <span data-ttu-id="a4db8-176">Bu durumda, uygulama ağ geçidi bir uç nokta artık ilk olarak çözümlenmiş adresinde açık olduğunu belirten bir ağ bağlantısı hatası alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4db8-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on the originally resolved address.</span></span>

<span data-ttu-id="a4db8-177">Ancak, çoğaltmalar veya hizmet örneklerinin bir ana bilgisayar işlemi paylaşabilir ve ayrıca bir http.sys tabanlı bir web sunucusu tarafından barındırılan bir bağlantı noktası paylaşabilen dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="a4db8-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="a4db8-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="a4db8-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="a4db8-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="a4db8-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="a4db8-180">Katana</span><span class="sxs-lookup"><span data-stu-id="a4db8-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="a4db8-181">Bu durumda, web sunucusunun ana bilgisayar işlemi ve isteklere yanıt kullanılabilir, ancak çözümlenen hizmet örneği ya da çoğaltma artık ana bilgisayarda kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-181">In this situation, it is likely that the web server is available in the host process and responding to requests, but the resolved service instance or replica is no longer available on the host.</span></span> <span data-ttu-id="a4db8-182">Bu durumda, ağ geçidi web sunucusundan bir HTTP 404 yanıtı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a4db8-182">In this case, the gateway will receive an HTTP 404 response from the web server.</span></span> <span data-ttu-id="a4db8-183">Bu nedenle, bir HTTP 404 iki ayrı anlama gelir:</span><span class="sxs-lookup"><span data-stu-id="a4db8-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="a4db8-184">#1: Hizmet adresi doğru durumdur, ancak kullanıcının istenen kaynak yok.</span><span class="sxs-lookup"><span data-stu-id="a4db8-184">Case #1: The service address is correct, but the resource that the user requested does not exist.</span></span>
- <span data-ttu-id="a4db8-185">Durum #2: Hizmet adresi yanlış ve kullanıcının istenen kaynak üzerinde farklı bir düğüme mevcut.</span><span class="sxs-lookup"><span data-stu-id="a4db8-185">Case #2: The service address is incorrect, and the resource that the user requested might exist on a different node.</span></span>

<span data-ttu-id="a4db8-186">İlk olarak bir normal HTTP kullanıcı hata olarak kabul edilen 404, olur.</span><span class="sxs-lookup"><span data-stu-id="a4db8-186">The first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="a4db8-187">Ancak, İkinci durumda, mevcut bir kaynak kullanıcı istedi.</span><span class="sxs-lookup"><span data-stu-id="a4db8-187">However, in the second case, the user has requested a resource that does exist.</span></span> <span data-ttu-id="a4db8-188">Uygulama ağ geçidi hizmeti taşınmış olduğundan dosyasını bulamadı.</span><span class="sxs-lookup"><span data-stu-id="a4db8-188">Application Gateway was unable to locate it because the service itself has moved.</span></span> <span data-ttu-id="a4db8-189">Uygulama ağ geçidi adresini yeniden çözümlemek ve isteği yeniden deneyin gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-189">Application Gateway needs to resolve the address again and retry the request.</span></span>

<span data-ttu-id="a4db8-190">Uygulama ağ geçidi, bu nedenle bu iki örnekleri arasında ayrım yapmak için bir yol gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-190">Application Gateway thus needs a way to distinguish between these two cases.</span></span> <span data-ttu-id="a4db8-191">Bu ayrım yapmak için sunucudan bir ipucu gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-191">To make that distinction, a hint from the server is required.</span></span>

* <span data-ttu-id="a4db8-192">Varsayılan olarak, uygulama ağ geçidi örneği #2 varsayar ve çözümleyin ve isteği yeniden gönderin dener.</span><span class="sxs-lookup"><span data-stu-id="a4db8-192">By default, Application Gateway assumes case #2 and attempts to resolve and issue the request again.</span></span>
* <span data-ttu-id="a4db8-193">Uygulama ağ geçidi #1 talebine belirtmek için hizmet aşağıdaki HTTP yanıtı üstbilgisini döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4db8-193">To indicate case #1 to Application Gateway, the service should return the following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="a4db8-194">Bu bir HTTP yanıt üstbilgisi istenen kaynak yok ve uygulama ağ geçidi hizmeti adresi yeniden çözümlemeyi dener olmayan normal bir HTTP 404 durumu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-194">This HTTP response header indicates a normal HTTP 404 situation in which the requested resource does not exist, and Application Gateway will not attempt to resolve the service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="a4db8-195">Kurulum ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a4db8-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="a4db8-196">Azure Portalı aracılığıyla ters proxy etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a4db8-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="a4db8-197">Azure portal, yeni bir Service Fabric kümesi oluşturulurken ters proxy etkinleştirmek için bir seçenek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4db8-197">Azure portal provides an option to enable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="a4db8-198">Altında **oluşturma Service Fabric kümesi**, adım 2: küme yapılandırması, düğüm türü yapılandırması için "Ters proxy etkinleştir" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="a4db8-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select the checkbox to "Enable reverse proxy".</span></span>
<span data-ttu-id="a4db8-199">Güvenli ters proxy yapılandırmak için SSL sertifikası adım 3'te belirtilebilir: güvenlik, küme güvenlik ayarlarını yapılandırma, sertifika ayrıntılarını girin ve "ters proxy için bir SSL sertifikası içerir" onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="a4db8-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select the checkbox to "Include a SSL certificate for reverse proxy" and enter the certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="a4db8-200">Ters proxy aracılığıyla Azure Resource Manager şablonları etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a4db8-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="a4db8-201">Kullanabileceğiniz [Azure Resource Manager şablonu](service-fabric-cluster-creation-via-arm.md) Service Fabric kümesi için ters proxy etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a4db8-201">You can use the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) to enable the reverse proxy in Service Fabric for the cluster.</span></span>

<span data-ttu-id="a4db8-202">Başvurmak [HTTPS Ters Proxy Yapılandırma güvenli bir kümede](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) için Azure Resource Manager şablon örnekleri güvenli yapılandırmak için ters proxy ile bir sertifika ve işleme sertifika aktarma.</span><span class="sxs-lookup"><span data-stu-id="a4db8-202">Refer to [Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples to configure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="a4db8-203">İlk olarak, dağıtmak istediğiniz küme için Şablon Al.</span><span class="sxs-lookup"><span data-stu-id="a4db8-203">First, you get the template for the cluster that you want to deploy.</span></span> <span data-ttu-id="a4db8-204">Örnek şablonları kullanabilir veya özel bir Resource Manager şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4db8-204">You can either use the sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="a4db8-205">Ardından, aşağıdaki adımları kullanarak ters proxy etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4db8-205">Then, you can enable the reverse proxy by using the following steps:</span></span>

1. <span data-ttu-id="a4db8-206">Ters proxy için bir bağlantı noktasını tanımlayın [parametreleri bölümüne](../azure-resource-manager/resource-group-authoring-templates.md) şablonun.</span><span class="sxs-lookup"><span data-stu-id="a4db8-206">Define a port for the reverse proxy in the [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of the template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="a4db8-207">Nodetype nesnelerin her biri için bağlantı noktasını belirtin **küme** [kaynak türü bölümü](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a4db8-207">Specify the port for each of the nodetype objects in the **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="a4db8-208">Bağlantı noktası parametre adı, reverseProxyEndpointPort tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a4db8-208">The port is identified by the parameter name, reverseProxyEndpointPort.</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. <span data-ttu-id="a4db8-209">Azure küme dışındaki ters proxy sunucudan adres için 1. adımda belirttiğiniz bağlantı noktası için Azure yük dengeleyici kuralları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a4db8-209">To address the reverse proxy from outside the Azure cluster, set up the Azure Load Balancer rules for the port that you specified in step 1.</span></span>

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. <span data-ttu-id="a4db8-210">SSL sertifikaları için ters Ara sunucu bağlantı noktasını yapılandırmak için sertifikaya eklemek ***reverseProxyCertificate*** özelliğinde **küme** [kaynak türü bölümü](../resource-group-authoring-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="a4db8-210">To configure SSL certificates on the port for the reverse proxy, add the certificate to the ***reverseProxyCertificate*** property in the **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-the-cluster-certificate"></a><span data-ttu-id="a4db8-211">Küme sertifikadan farklı bir ters proxy sertifikası destekleme</span><span class="sxs-lookup"><span data-stu-id="a4db8-211">Supporting a reverse proxy certificate that's different from the cluster certificate</span></span>
 <span data-ttu-id="a4db8-212">Ters proxy sertifika küme güvenliğini sağlar sertifikasından farklıysa, ardından daha önce belirtilen sertifika sanal makinede yüklü ve Service Fabric erişebilmesi erişim denetim listesi (ACL) eklenir.</span><span class="sxs-lookup"><span data-stu-id="a4db8-212">If the reverse proxy certificate is different from the certificate that secures the cluster, then the previously specified certificate should be installed on the virtual machine and added to the access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="a4db8-213">Bu yapılabilir **virtualMachineScaleSets** [kaynak türü bölümü](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a4db8-213">This can be done in the **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a4db8-214">Yükleme için bu sertifika için osProfile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4db8-214">For installation, add that certificate to the osProfile.</span></span> <span data-ttu-id="a4db8-215">Şablon uzantısı bölümünü ACL sertifikada güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4db8-215">The extension section of the template can update the certificate in the ACL.</span></span>

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> <span data-ttu-id="a4db8-216">Var olan bir kümede ters proxy etkinleştirmek için küme sertifikasından farklı sertifikaları kullanırken, ters proxy sertifikasını yükleyin ve ters proxy etkinleştirmeden önce küme üzerinde ACL güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="a4db8-216">When you use certificates that are different from the cluster certificate to enable the reverse proxy on an existing cluster, install the reverse proxy certificate and update the ACL on the cluster before you enable the reverse proxy.</span></span> <span data-ttu-id="a4db8-217">Tamamlamak [Azure Resource Manager şablonu](service-fabric-cluster-creation-via-arm.md) bahsedilen ayarlarını kullanarak dağıtım önceden ters proxy etkinleştirmek için bir dağıtım başlamadan önce adımları 1-4.</span><span class="sxs-lookup"><span data-stu-id="a4db8-217">Complete the [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using the settings mentioned previously before you start a deployment to enable the reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4db8-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4db8-218">Next steps</span></span>
* <span data-ttu-id="a4db8-219">HTTP iletişimi Hizmetleri'nde arasında örneğine bakın bir [örnek proje github'da](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a4db8-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="a4db8-220">Ters proxy ile iletme için Güvenli HTTP hizmeti</span><span class="sxs-lookup"><span data-stu-id="a4db8-220">Forwarding to secure HTTP service with the reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="a4db8-221">Güvenilir hizmetler remoting ile uzak yordam çağrıları</span><span class="sxs-lookup"><span data-stu-id="a4db8-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="a4db8-222">Web API OWIN güvenilir Hizmetleri'nde kullanır</span><span class="sxs-lookup"><span data-stu-id="a4db8-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="a4db8-223">Güvenilir hizmetler kullanarak WCF iletişimi</span><span class="sxs-lookup"><span data-stu-id="a4db8-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="a4db8-224">Ek ters proxy yapılandırma seçenekleri için ApplicationGateway/Http bölümüne başvurun [özelleştirme Service Fabric kümesi ayarlarını](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a4db8-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
