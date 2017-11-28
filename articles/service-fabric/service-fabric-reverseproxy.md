---
title: Service Fabric aaaAzure ters proxy | Microsoft Docs
description: "İç ve dış hello küme iletişimi toomicroservices için Service Fabric'ın ters proxy kullanın."
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
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a><span data-ttu-id="a2f88-103">Azure Service Fabric ters proxy</span><span class="sxs-lookup"><span data-stu-id="a2f88-103">Reverse proxy in Azure Service Fabric</span></span>
<span data-ttu-id="a2f88-104">Azure Service Fabric yerleşik hello ters proxy HTTP uç noktaları gösteren hello Service Fabric kümesindeki mikro giderir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-104">hello reverse proxy that's built into Azure Service Fabric addresses microservices in hello Service Fabric cluster that exposes HTTP endpoints.</span></span>

## <a name="microservices-communication-model"></a><span data-ttu-id="a2f88-105">Mikro iletişim modelini</span><span class="sxs-lookup"><span data-stu-id="a2f88-105">Microservices communication model</span></span>
<span data-ttu-id="a2f88-106">Service Fabric mikro genellikle bir alt hello kümedeki sanal makinelerin çalışır ve bir sanal makine tooanother çeşitli nedenlerle taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f88-106">Microservices in Service Fabric typically run on a subset of virtual machines in hello cluster and can move from one virtual machine tooanother for various reasons.</span></span> <span data-ttu-id="a2f88-107">Bu nedenle, hello uç noktaları mikro için dinamik olarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f88-107">So, hello endpoints for microservices can change dynamically.</span></span> <span data-ttu-id="a2f88-108">Merhaba tipik bir düzen toocommunicate toohello mikro hello aşağıdaki döngüsü çözmek şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a2f88-108">hello typical pattern toocommunicate toohello microservice is hello following resolve loop:</span></span>

1. <span data-ttu-id="a2f88-109">Başlangıçta hello adlandırma hizmeti aracılığıyla Hello hizmet konumu çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f88-109">Resolve hello service location initially through hello naming service.</span></span>
2. <span data-ttu-id="a2f88-110">Toohello hizmetine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a2f88-110">Connect toohello service.</span></span>
3. <span data-ttu-id="a2f88-111">Bağlantı hataları Hello nedenini ve gerektiğinde Merhaba hizmet konumu yeniden çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f88-111">Determine hello cause of connection failures, and resolve hello service location again when necessary.</span></span>

<span data-ttu-id="a2f88-112">Bu işlem genellikle hello hizmeti çözümleme ve Yeniden Dene'yi ilkeleri uygulayan bir yeniden deneme döngüsüne istemci-tarafı iletişim kitaplıklarında kaydırma içerir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-112">This process generally involves wrapping client-side communication libraries in a retry loop that implements hello service resolution and retry policies.</span></span>
<span data-ttu-id="a2f88-113">Daha fazla bilgi için bkz: [Bağlan ve Hizmetleri ile iletişim](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="a2f88-113">For more information, see [Connect and communicate with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

### <a name="communicating-by-using-hello-reverse-proxy"></a><span data-ttu-id="a2f88-114">Merhaba ters proxy kullanarak iletişim</span><span class="sxs-lookup"><span data-stu-id="a2f88-114">Communicating by using hello reverse proxy</span></span>
<span data-ttu-id="a2f88-115">Merhaba kümedeki tüm hello düğümlere Hello ters proxy Service Fabric içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-115">hello reverse proxy in Service Fabric runs on all hello nodes in hello cluster.</span></span> <span data-ttu-id="a2f88-116">Bir istemcinin adına hello tüm hizmet çözümleme işlemi gerçekleştirir ve hello istemci isteğini iletir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-116">It performs hello entire service resolution process on a client's behalf and then forwards hello client request.</span></span> <span data-ttu-id="a2f88-117">Bu nedenle, hello kümede çalışan istemciler, yerel olarak çalışır aynı düğümde hello hello ters Ara sunucu kullanarak tüm istemci-tarafı HTTP iletişim kitaplıkları tootalk toohello hedef hizmetini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f88-117">So, clients that run on hello cluster can use any client-side HTTP communication libraries tootalk toohello target service by using hello reverse proxy that runs locally on hello same node.</span></span>

![İç iletişim][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a><span data-ttu-id="a2f88-119">Dış hello kümeden mikro ulaşmasını</span><span class="sxs-lookup"><span data-stu-id="a2f88-119">Reaching microservices from outside hello cluster</span></span>
<span data-ttu-id="a2f88-120">Merhaba varsayılan dış iletişim modelini mikro için burada her hizmetin doğrudan dış istemcilerden erişilemez bir katılımı modelidir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-120">hello default external communication model for microservices is an opt-in model where each service cannot be accessed directly from external clients.</span></span> <span data-ttu-id="a2f88-121">[Azure yük dengeleyici](../load-balancer/load-balancer-overview.md), mikro dış istemcileri arasındaki bir ağ sınırında olduğu ağ adresi çevirisi gerçekleştirir ve ileten dış toointernal IP: BağlantıNoktası uç noktaları ister.</span><span class="sxs-lookup"><span data-stu-id="a2f88-121">[Azure Load Balancer](../load-balancer/load-balancer-overview.md), which is a network boundary between microservices and external clients, performs network address translation and forwards external requests toointernal IP:port endpoints.</span></span> <span data-ttu-id="a2f88-122">toomake mikro 's uç noktası doğrudan erişilebilir tooexternal istemciler, önce hizmet hello tooforward trafiği tooeach bağlantı noktası kullanan yük dengeleyici hello kümede yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-122">toomake a microservice's endpoint directly accessible tooexternal clients, you must first configure Load Balancer tooforward traffic tooeach port that hello service uses in hello cluster.</span></span> <span data-ttu-id="a2f88-123">Ayrıca, çoğu mikro, özellikle durum bilgisi olan mikro hello kümenin tüm düğümlerinde dinamik yok.</span><span class="sxs-lookup"><span data-stu-id="a2f88-123">Furthermore, most microservices, especially stateful microservices, don't live on all nodes of hello cluster.</span></span> <span data-ttu-id="a2f88-124">Merhaba mikro yük devretme düğümlerinde arasında taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f88-124">hello microservices can move between nodes on failover.</span></span> <span data-ttu-id="a2f88-125">Böyle durumlarda, yük dengeleyici etkili bir şekilde hello konumu belirlenemiyor hello çoğaltmaları toowhich, hedef düğümü hello trafiği iletmek.</span><span class="sxs-lookup"><span data-stu-id="a2f88-125">In such cases, Load Balancer cannot effectively determine hello location of hello target node of hello replicas toowhich it should forward traffic.</span></span>

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a><span data-ttu-id="a2f88-126">Dış hello kümeden hello ters proxy aracılığıyla mikro ulaşmasını</span><span class="sxs-lookup"><span data-stu-id="a2f88-126">Reaching microservices via hello reverse proxy from outside hello cluster</span></span>
<span data-ttu-id="a2f88-127">Yük dengeleyicisi bir bireysel hizmet başlangıç bağlantı noktası yapılandırmak yerine, yalnızca hello ters proxy hello bağlantı yük dengeleyici yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f88-127">Instead of configuring hello port of an individual service in Load Balancer, you can configure just hello port of hello reverse proxy in Load Balancer.</span></span> <span data-ttu-id="a2f88-128">Bu yapılandırma hello küme dışındaki istemcilerin hello ters proxy ek yapılandırma olmadan kullanarak hello küme içindeki hizmetlere erişmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2f88-128">This configuration lets clients outside hello cluster reach services inside hello cluster by using hello reverse proxy without additional configuration.</span></span>

![Dış iletişimi][0]

> [!WARNING]
> <span data-ttu-id="a2f88-130">Yük dengeleyicisi hello ters proxy'nın bağlantı noktası yapılandırdığınızda, bir HTTP uç noktası kullanıma hello kümedeki tüm mikro hello küme dışında adreslenebilir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-130">When you configure hello reverse proxy's port in Load Balancer, all microservices in hello cluster that expose an HTTP endpoint are addressable from outside hello cluster.</span></span>
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a><span data-ttu-id="a2f88-131">Merhaba ters proxy kullanarak Hizmetleri adresleme için URI biçimi</span><span class="sxs-lookup"><span data-stu-id="a2f88-131">URI format for addressing services by using hello reverse proxy</span></span>
<span data-ttu-id="a2f88-132">belirli bir Tekdüzen Kaynak Tanımlayıcısı (URI) biçimi tooidentify hello hizmet bölüm toowhich hello gelen isteği iletilmesi gereken hello ters proxy kullanır:</span><span class="sxs-lookup"><span data-stu-id="a2f88-132">hello reverse proxy uses a specific uniform resource identifier (URI) format tooidentify hello service partition toowhich hello incoming request should be forwarded:</span></span>

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* <span data-ttu-id="a2f88-133">**http (s):** hello ters proxy yapılandırılmış tooaccept HTTP veya HTTPS trafiği olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-133">**http(s):** hello reverse proxy can be configured tooaccept HTTP or HTTPS traffic.</span></span> <span data-ttu-id="a2f88-134">HTTPS iletme için çok başvuran[tooa güvenli service hello ters proxy ile bağlanma](service-fabric-reverseproxy-configure-secure-communication.md) HTTPS üzerinde ters proxy Kurulum toolisten sahip olduğunda.</span><span class="sxs-lookup"><span data-stu-id="a2f88-134">For HTTPS forwarding, refer too[Connect tooa secure service with hello reverse proxy](service-fabric-reverseproxy-configure-secure-communication.md) once you have reverse proxy setup toolisten on HTTPS.</span></span>
* <span data-ttu-id="a2f88-135">**Küme tam etki alanı adı (FQDN) | iç IP:** dış istemcileri için böylece mycluster.eastus.cloudapp.azure.com gibi hello küme etki üzerinden erişilebilen hello ters proxy yapılandırabilirsiniz. Varsayılan olarak, hello ters proxy her düğüm üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-135">**Cluster fully qualified domain name (FQDN) | internal IP:** For external clients, you can configure hello reverse proxy so that it is reachable through hello cluster domain, such as mycluster.eastus.cloudapp.azure.com. By default, hello reverse proxy runs on every node.</span></span> <span data-ttu-id="a2f88-136">İç trafiği için hello ters proxy 10.0.0.1 gibi herhangi bir iç düğüm IP'yi veya localhost üzerinde erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-136">For internal traffic, hello reverse proxy can be reached on localhost or on any internal node IP, such as 10.0.0.1.</span></span>
* <span data-ttu-id="a2f88-137">**Bağlantı noktası:** hello ters proxy için belirtilen hello gibi bağlantı noktası 19081, budur.</span><span class="sxs-lookup"><span data-stu-id="a2f88-137">**Port:** This is hello port, such as 19081, that has been specified for hello reverse proxy.</span></span>
* <span data-ttu-id="a2f88-138">**ServiceInstanceName:** bu hello tam hello olmadan tooreach çalıştığınız dağıtılan hello hizmet örneği adıdır "fabric: /" düzeni.</span><span class="sxs-lookup"><span data-stu-id="a2f88-138">**ServiceInstanceName:** This is hello fully-qualified name of hello deployed service instance that you are trying tooreach without hello "fabric:/" scheme.</span></span> <span data-ttu-id="a2f88-139">Örneğin, tooreach hello *fabric: / myapp/myservice/* hizmeti, kullandığınız *myapp/myservice*.</span><span class="sxs-lookup"><span data-stu-id="a2f88-139">For example, tooreach hello *fabric:/myapp/myservice/* service, you would use *myapp/myservice*.</span></span>

    <span data-ttu-id="a2f88-140">Merhaba hizmet örneği adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-140">hello service instance name is case-sensitive.</span></span> <span data-ttu-id="a2f88-141">Merhaba URL'deki hello hizmet örneği adı için farklı büyük/küçük harf kullanarak hello istekleri toofail 404 ile (bulunamadı) neden olur.</span><span class="sxs-lookup"><span data-stu-id="a2f88-141">Using a different casing for hello service instance name in hello URL causes hello requests toofail with 404 (Not Found).</span></span>
* <span data-ttu-id="a2f88-142">**Sonek yol:** hello gerçek URL yolu gibi budur *myapi/değerleri/ekleme/3*, tooconnect için istediğiniz hello hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a2f88-142">**Suffix path:** This is hello actual URL path, such as *myapi/values/add/3*, for hello service that you want tooconnect to.</span></span>
* <span data-ttu-id="a2f88-143">**PartitionKey:** bölümlenmiş bir hizmet için bu hello hesaplanan bölüm tooreach istediğiniz hello bölümünün anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-143">**PartitionKey:** For a partitioned service, this is hello computed partition key of hello partition that you want tooreach.</span></span> <span data-ttu-id="a2f88-144">Bu Not *değil* bölüm kimliği GUID hello.</span><span class="sxs-lookup"><span data-stu-id="a2f88-144">Note that this is *not* hello partition ID GUID.</span></span> <span data-ttu-id="a2f88-145">Bu parametre hello tek bölüm düzeni kullanan Hizmetleri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-145">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="a2f88-146">**PartitionKind:** hello hizmet bölüm düzeni budur.</span><span class="sxs-lookup"><span data-stu-id="a2f88-146">**PartitionKind:** This is hello service partition scheme.</span></span> <span data-ttu-id="a2f88-147">Bu, 'Int64Range' veya 'Adlı' olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-147">This can be 'Int64Range' or 'Named'.</span></span> <span data-ttu-id="a2f88-148">Bu parametre hello tek bölüm düzeni kullanan Hizmetleri için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-148">This parameter is not required for services that use hello singleton partition scheme.</span></span>
* <span data-ttu-id="a2f88-149">**ListenerName** hello hello hizmetinden noktalarıdır hello biçimi {"Bitiş": {"Listener1": "Bitiş noktası 1", "Listener2": "Endpoint2"...}}.</span><span class="sxs-lookup"><span data-stu-id="a2f88-149">**ListenerName** hello endpoints from hello service are of hello form {"Endpoints":{"Listener1":"Endpoint1","Listener2":"Endpoint2" ...}}.</span></span> <span data-ttu-id="a2f88-150">Birden çok uç nokta Hello hizmet sunan olduğunda bu hello endpoint tanımlar için o hello istemci isteği iletilir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-150">When hello service exposes multiple endpoints, this identifies hello endpoint that hello client request should be forwarded to.</span></span> <span data-ttu-id="a2f88-151">Merhaba hizmet yalnızca bir dinleyici varsa bu atlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-151">This can be omitted if hello service has only one listener.</span></span>
* <span data-ttu-id="a2f88-152">**TargetReplicaSelector** bu hello hedef çoğaltma veya örnek nasıl seçilen belirtir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-152">**TargetReplicaSelector** This specifies how hello target replica or instance should be selected.</span></span>
  * <span data-ttu-id="a2f88-153">Merhaba hedef hizmet durum bilgisi olan olduğunda hello TargetReplicaSelector hello aşağıdakilerden biri olabilir: 'PrimaryReplica', 'RandomSecondaryReplica' veya 'RandomReplica'.</span><span class="sxs-lookup"><span data-stu-id="a2f88-153">When hello target service is stateful, hello TargetReplicaSelector can be one of hello following:  'PrimaryReplica', 'RandomSecondaryReplica', or 'RandomReplica'.</span></span> <span data-ttu-id="a2f88-154">Bu parametre belirtilmediğinde hello 'PrimaryReplica' varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-154">When this parameter is not specified, hello default is 'PrimaryReplica'.</span></span>
  * <span data-ttu-id="a2f88-155">Merhaba hedef hizmet durum bilgisiz olduğunda ters proxy hello hizmet bölüm tooforward hello isteği için rastgele bir örneğini seçer.</span><span class="sxs-lookup"><span data-stu-id="a2f88-155">When hello target service is stateless, reverse proxy picks a random instance of hello service partition tooforward hello request to.</span></span>
* <span data-ttu-id="a2f88-156">**Zaman aşımı:** bu hello istemci isteği adına hello ters proxy toohello hizmeti tarafından oluşturulan hello HTTP isteği için hello zaman aşımını belirtir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-156">**Timeout:**  This specifies hello timeout for hello HTTP request created by hello reverse proxy toohello service on behalf of hello client request.</span></span> <span data-ttu-id="a2f88-157">Merhaba varsayılan değer 60 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-157">hello default value is 60 seconds.</span></span> <span data-ttu-id="a2f88-158">Bu isteğe bağlı bir parametredir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-158">This is an optional parameter.</span></span>

### <a name="example-usage"></a><span data-ttu-id="a2f88-159">Örnek Kullanım</span><span class="sxs-lookup"><span data-stu-id="a2f88-159">Example usage</span></span>
<span data-ttu-id="a2f88-160">Örnek olarak, hello atalım *fabric: / MyApp/MyService* URL aşağıdaki hello üzerinde bir HTTP dinleyicisi açar hizmeti:</span><span class="sxs-lookup"><span data-stu-id="a2f88-160">As an example, let's take hello *fabric:/MyApp/MyService* service that opens an HTTP listener on hello following URL:</span></span>

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

<span data-ttu-id="a2f88-161">Merhaba hizmet için hello kaynağı şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a2f88-161">Following are hello resources for hello service:</span></span>

* `/index.html`
* `/api/users/<userId>`

<span data-ttu-id="a2f88-162">Merhaba hizmetini bölümleme hello singleton kullanıyorsa, hello *PartitionKey* ve *PartitionKind* sorgu dizesi parametreleri gerekli değildir ve hello hizmeti hello ağ geçidi olarak kullanarak üst sınırına:</span><span class="sxs-lookup"><span data-stu-id="a2f88-162">If hello service uses hello singleton partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters are not required, and hello service can be reached by using hello gateway as:</span></span>

* <span data-ttu-id="a2f88-163">Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="a2f88-163">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`</span></span>
* <span data-ttu-id="a2f88-164">Dahili olarak:`http://localhost:19081/MyApp/MyService`</span><span class="sxs-lookup"><span data-stu-id="a2f88-164">Internally: `http://localhost:19081/MyApp/MyService`</span></span>

<span data-ttu-id="a2f88-165">Merhaba hizmetini bölümleme hello Tekdüzen Int64 kullanıyorsa, hello *PartitionKey* ve *PartitionKind* sorgu dizesi parametreleri kullanılan tooreach hello hizmetinin bir bölüm olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2f88-165">If hello service uses hello Uniform Int64 partitioning scheme, hello *PartitionKey* and *PartitionKind* query string parameters must be used tooreach a partition of hello service:</span></span>

* <span data-ttu-id="a2f88-166">Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a2f88-166">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="a2f88-167">Dahili olarak:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a2f88-167">Internally: `http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="a2f88-168">Merhaba hizmet sunan, tooreach hello kaynakları yalnızca yerleştirin hello kaynak yolu hello hizmet adı hello URL'de sonra:</span><span class="sxs-lookup"><span data-stu-id="a2f88-168">tooreach hello resources that hello service exposes, simply place hello resource path after hello service name in hello URL:</span></span>

* <span data-ttu-id="a2f88-169">Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a2f88-169">Externally: `http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`</span></span>
* <span data-ttu-id="a2f88-170">Dahili olarak:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span><span class="sxs-lookup"><span data-stu-id="a2f88-170">Internally: `http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`</span></span>

<span data-ttu-id="a2f88-171">Merhaba ağ geçidi, ardından bu istekleri toohello hizmetin URL iletir:</span><span class="sxs-lookup"><span data-stu-id="a2f88-171">hello gateway will then forward these requests toohello service's URL:</span></span>

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a><span data-ttu-id="a2f88-172">Bağlantı noktası paylaşımı için bir özel işleme Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a2f88-172">Special handling for port-sharing services</span></span>
<span data-ttu-id="a2f88-173">Azure uygulama ağ geçidi hizmet yeniden adresi ve bir hizmet erişildiğinde hello isteği yeniden deneyin tooresolve çalışır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-173">Azure Application Gateway attempts tooresolve a service address again and retry hello request when a service cannot be reached.</span></span> <span data-ttu-id="a2f88-174">İstemci kodu değil tooimplement kendi hizmet çözümlemesi gerekir ve döngüsü çözmek uygulama ağ geçidi önemli bir avantajı olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-174">This is a major benefit of Application Gateway because client code does not need tooimplement its own service resolution and resolve loop.</span></span>

<span data-ttu-id="a2f88-175">Genellikle, bir hizmetine ulaşılamıyor zaman hello hizmet örneği veya çoğaltma farklı bir düğüme tooa normal yaşam döngüsünün parçası olarak taşındı.</span><span class="sxs-lookup"><span data-stu-id="a2f88-175">Generally, when a service cannot be reached, hello service instance or replica has moved tooa different node as part of its normal lifecycle.</span></span> <span data-ttu-id="a2f88-176">Bu gerçekleştiğinde, ağ bağlantısı hatası bir uç nokta hello üzerinde daha uzun hiçbir açık adres başlangıçta çözülmüş olduğunu belirten bir uygulama ağ geçidi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f88-176">When this happens, Application Gateway might receive a network connection error indicating that an endpoint is no longer open on hello originally resolved address.</span></span>

<span data-ttu-id="a2f88-177">Ancak, çoğaltmalar veya hizmet örneklerinin bir ana bilgisayar işlemi paylaşabilir ve ayrıca bir http.sys tabanlı bir web sunucusu tarafından barındırılan bir bağlantı noktası paylaşabilen dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="a2f88-177">However, replicas or service instances can share a host process and might also share a port when hosted by an http.sys-based web server, including:</span></span>

* [<span data-ttu-id="a2f88-178">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="a2f88-178">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [<span data-ttu-id="a2f88-179">ASP.NET Core WebListener</span><span class="sxs-lookup"><span data-stu-id="a2f88-179">ASP.NET Core WebListener</span></span>](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [<span data-ttu-id="a2f88-180">Katana</span><span class="sxs-lookup"><span data-stu-id="a2f88-180">Katana</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

<span data-ttu-id="a2f88-181">Bu durumda, hello ana bilgisayar işlemi ve toorequests ancak hello hizmet örneği çözümlenmiş ya da çoğaltma artık hello ana bilgisayarda kullanılabilir yanıt hello web sunucusu kullanılabilir olasıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-181">In this situation, it is likely that hello web server is available in hello host process and responding toorequests, but hello resolved service instance or replica is no longer available on hello host.</span></span> <span data-ttu-id="a2f88-182">Bu durumda, hello ağ geçidi hello web sunucusundan bir HTTP 404 yanıtı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a2f88-182">In this case, hello gateway will receive an HTTP 404 response from hello web server.</span></span> <span data-ttu-id="a2f88-183">Bu nedenle, bir HTTP 404 iki ayrı anlama gelir:</span><span class="sxs-lookup"><span data-stu-id="a2f88-183">Thus, an HTTP 404 has two distinct meanings:</span></span>

- <span data-ttu-id="a2f88-184">Durum #1: hello hizmet adresinin doğru olduğundan, ancak istenen kullanıcı hello hello kaynak yok.</span><span class="sxs-lookup"><span data-stu-id="a2f88-184">Case #1: hello service address is correct, but hello resource that hello user requested does not exist.</span></span>
- <span data-ttu-id="a2f88-185">Durum #2: hello hizmeti adresi yanlış ve istenen kullanıcı hello hello kaynak farklı bir kümede mevcut.</span><span class="sxs-lookup"><span data-stu-id="a2f88-185">Case #2: hello service address is incorrect, and hello resource that hello user requested might exist on a different node.</span></span>

<span data-ttu-id="a2f88-186">Merhaba ilk olarak bir normal HTTP kullanıcı hata olarak kabul edilen 404, olur.</span><span class="sxs-lookup"><span data-stu-id="a2f88-186">hello first case is a normal HTTP 404, which is considered a user error.</span></span> <span data-ttu-id="a2f88-187">Ancak, hello ikinci durumda, mevcut bir kaynak hello kullanıcı istedi.</span><span class="sxs-lookup"><span data-stu-id="a2f88-187">However, in hello second case, hello user has requested a resource that does exist.</span></span> <span data-ttu-id="a2f88-188">Uygulama ağ geçidi hello hizmet çünkü kendisine taşındı oluşturulamıyor toolocate oluştu.</span><span class="sxs-lookup"><span data-stu-id="a2f88-188">Application Gateway was unable toolocate it because hello service itself has moved.</span></span> <span data-ttu-id="a2f88-189">Uygulama ağ geçidi gereksinimlerini tooresolve hello adresi yeniden ve yeniden deneme hello isteği.</span><span class="sxs-lookup"><span data-stu-id="a2f88-189">Application Gateway needs tooresolve hello address again and retry hello request.</span></span>

<span data-ttu-id="a2f88-190">Uygulama ağ geçidi, bu nedenle bu iki çalışmaları arasında bir şekilde toodistinguish gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2f88-190">Application Gateway thus needs a way toodistinguish between these two cases.</span></span> <span data-ttu-id="a2f88-191">toomake ayrım, bir ipucu hello sunucusundan gerekli olur.</span><span class="sxs-lookup"><span data-stu-id="a2f88-191">toomake that distinction, a hint from hello server is required.</span></span>

* <span data-ttu-id="a2f88-192">Varsayılan olarak, uygulama ağ geçidi örneği #2 varsayar ve hello istek tooresolve ve sorunu yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="a2f88-192">By default, Application Gateway assumes case #2 and attempts tooresolve and issue hello request again.</span></span>
* <span data-ttu-id="a2f88-193">tooindicate durum #1 tooApplication ağ geçidi, bir HTTP yanıt üstbilgisi aşağıdaki hello hello hizmet döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2f88-193">tooindicate case #1 tooApplication Gateway, hello service should return hello following HTTP response header:</span></span>

  `X-ServiceFabric : ResourceNotFound`

<span data-ttu-id="a2f88-194">Bu bir HTTP yanıt üstbilgisi hangi hello istenen kaynak yok normal bir HTTP 404 durumu gösterir ve uygulama ağ geçidi tooresolve hello hizmeti adresi yeniden denemez.</span><span class="sxs-lookup"><span data-stu-id="a2f88-194">This HTTP response header indicates a normal HTTP 404 situation in which hello requested resource does not exist, and Application Gateway will not attempt tooresolve hello service address again.</span></span>

## <a name="setup-and-configuration"></a><span data-ttu-id="a2f88-195">Kurulum ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a2f88-195">Setup and configuration</span></span>

### <a name="enable-reverse-proxy-via-azure-portal"></a><span data-ttu-id="a2f88-196">Azure Portalı aracılığıyla ters proxy etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a2f88-196">Enable reverse proxy via Azure portal</span></span>

<span data-ttu-id="a2f88-197">Azure portalı, yeni bir Service Fabric kümesi oluşturulurken bir seçenek tooenable ters proxy sağlar.</span><span class="sxs-lookup"><span data-stu-id="a2f88-197">Azure portal provides an option tooenable Reverse proxy while creating a new Service Fabric cluster.</span></span>
<span data-ttu-id="a2f88-198">Altında **oluşturma Service Fabric kümesi**, adım 2: küme yapılandırması, düğüm türü yapılandırması hello onay kutusu çok seçin "Etkinleştirme ters proxy".</span><span class="sxs-lookup"><span data-stu-id="a2f88-198">Under **Create Service Fabric cluster**, Step 2: Cluster Configuration, Node type configuration, select hello checkbox too"Enable reverse proxy".</span></span>
<span data-ttu-id="a2f88-199">Güvenli ters proxy yapılandırmak için SSL sertifikası adım 3'te belirtilebilir: güvenlik, küme güvenlik ayarlarını yapılandırma, select hello onay kutusu çok "ters proxy için bir SSL sertifikası Ekle" ve hello sertifika ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="a2f88-199">For configuring secure reverse proxy, SSL certificate can be specified in Step 3: Security, Configure cluster security settings, select hello checkbox too"Include a SSL certificate for reverse proxy" and enter hello certificate details.</span></span>

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a><span data-ttu-id="a2f88-200">Ters proxy aracılığıyla Azure Resource Manager şablonları etkinleştir</span><span class="sxs-lookup"><span data-stu-id="a2f88-200">Enable reverse proxy via Azure Resource Manager templates</span></span>

<span data-ttu-id="a2f88-201">Merhaba kullanabilirsiniz [Azure Resource Manager şablonu](service-fabric-cluster-creation-via-arm.md) tooenable hello için ters proxy hizmeti yapıda hello küme.</span><span class="sxs-lookup"><span data-stu-id="a2f88-201">You can use hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) tooenable hello reverse proxy in Service Fabric for hello cluster.</span></span>

<span data-ttu-id="a2f88-202">Çok başvuran[HTTPS Ters Proxy Yapılandırma güvenli bir kümede](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) için Azure Resource Manager şablonu güvenli ters proxy bir sertifika ve işleme sertifika rollover tooconfigure örnekleri.</span><span class="sxs-lookup"><span data-stu-id="a2f88-202">Refer too[Configure HTTPS Reverse Proxy in a secure cluster](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) for Azure Resource Manager template samples tooconfigure secure reverse proxy with a certificate and handling certificate rollover.</span></span>

<span data-ttu-id="a2f88-203">İlk olarak, toodeploy istediğiniz hello küme için hello Şablon Al.</span><span class="sxs-lookup"><span data-stu-id="a2f88-203">First, you get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="a2f88-204">Merhaba örnek şablonları kullanabilir veya özel bir Resource Manager şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2f88-204">You can either use hello sample templates or create a custom Resource Manager template.</span></span> <span data-ttu-id="a2f88-205">Ardından, aşağıdaki adımları hello kullanarak hello ters proxy etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a2f88-205">Then, you can enable hello reverse proxy by using hello following steps:</span></span>

1. <span data-ttu-id="a2f88-206">Merhaba ters proxy için bir bağlantı noktası hello tanımlamak [parametreleri bölümüne](../azure-resource-manager/resource-group-authoring-templates.md) hello şablonunun.</span><span class="sxs-lookup"><span data-stu-id="a2f88-206">Define a port for hello reverse proxy in hello [Parameters section](../azure-resource-manager/resource-group-authoring-templates.md) of hello template.</span></span>

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. <span data-ttu-id="a2f88-207">Her hello nodetype nesnelerin hello Hello bağlantı noktasını belirtin **küme** [kaynak türü bölümü](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a2f88-207">Specify hello port for each of hello nodetype objects in hello **Cluster** [Resource type section](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    <span data-ttu-id="a2f88-208">başlangıç bağlantı noktası hello parametre adı reverseProxyEndpointPort tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="a2f88-208">hello port is identified by hello parameter name, reverseProxyEndpointPort.</span></span>

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
3. <span data-ttu-id="a2f88-209">1. adımda belirttiğiniz başlangıç bağlantı noktası için hello Azure yük dengeleyici kuralları ayarlama dış hello Azure küme gelen tooaddress hello ters proxy.</span><span class="sxs-lookup"><span data-stu-id="a2f88-209">tooaddress hello reverse proxy from outside hello Azure cluster, set up hello Azure Load Balancer rules for hello port that you specified in step 1.</span></span>

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
4. <span data-ttu-id="a2f88-210">Merhaba ters proxy hello bağlantı noktasında tooconfigure SSL sertifikaları Ekle hello sertifika toohello ***reverseProxyCertificate*** hello özelliğinde **küme** [kaynak türü bölümü](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a2f88-210">tooconfigure SSL certificates on hello port for hello reverse proxy, add hello certificate toohello ***reverseProxyCertificate*** property in hello **Cluster** [Resource type section](../resource-group-authoring-templates.md).</span></span>

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

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a><span data-ttu-id="a2f88-211">Merhaba küme sertifikadan farklı bir ters proxy sertifikası destekleme</span><span class="sxs-lookup"><span data-stu-id="a2f88-211">Supporting a reverse proxy certificate that's different from hello cluster certificate</span></span>
 <span data-ttu-id="a2f88-212">Merhaba ters proxy sertifika hello küme korur hello sertifikasından farklıysa, ardından hello daha önce sertifika hello sanal makineye yüklenmesi ve böylece Service Fabric toohello erişim denetim listesi (ACL) eklenen belirtilen erişim.</span><span class="sxs-lookup"><span data-stu-id="a2f88-212">If hello reverse proxy certificate is different from hello certificate that secures hello cluster, then hello previously specified certificate should be installed on hello virtual machine and added toohello access control list (ACL) so that Service Fabric can access it.</span></span> <span data-ttu-id="a2f88-213">Bu hello yapılabilir **virtualMachineScaleSets** [kaynak türü bölümü](../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a2f88-213">This can be done in hello **virtualMachineScaleSets** [Resource type section](../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="a2f88-214">Yükleme için bu sertifika toohello osProfile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f88-214">For installation, add that certificate toohello osProfile.</span></span> <span data-ttu-id="a2f88-215">Merhaba uzantısı hello şablon bölümünü hello ACL hello sertifikada güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2f88-215">hello extension section of hello template can update hello certificate in hello ACL.</span></span>

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
> <span data-ttu-id="a2f88-216">Merhaba küme sertifika tooenable hello ters proxy var olan bir kümede farklı sertifikaları kullandığınızda, hello ters proxy sertifikası yükleyin ve hello ters proxy etkinleştirmeden önce hello ACL hello kümede güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="a2f88-216">When you use certificates that are different from hello cluster certificate tooenable hello reverse proxy on an existing cluster, install hello reverse proxy certificate and update hello ACL on hello cluster before you enable hello reverse proxy.</span></span> <span data-ttu-id="a2f88-217">Tam hello [Azure Resource Manager şablonu](service-fabric-cluster-creation-via-arm.md) bahsedilen hello ayarlarını kullanarak dağıtım daha önce bir dağıtım tooenable hello ters proxy başlamadan önce adımları 1-4.</span><span class="sxs-lookup"><span data-stu-id="a2f88-217">Complete hello [Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md) deployment by using hello settings mentioned previously before you start a deployment tooenable hello reverse proxy in steps 1-4.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2f88-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a2f88-218">Next steps</span></span>
* <span data-ttu-id="a2f88-219">HTTP iletişimi Hizmetleri'nde arasında örneğine bakın bir [örnek proje github'da](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="a2f88-219">See an example of HTTP communication between services in a [sample project on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).</span></span>
* [<span data-ttu-id="a2f88-220">İletme toosecure HTTP hizmeti ile Merhaba ters proxy</span><span class="sxs-lookup"><span data-stu-id="a2f88-220">Forwarding toosecure HTTP service with hello reverse proxy</span></span>](service-fabric-reverseproxy-configure-secure-communication.md)
* [<span data-ttu-id="a2f88-221">Güvenilir hizmetler remoting ile uzak yordam çağrıları</span><span class="sxs-lookup"><span data-stu-id="a2f88-221">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="a2f88-222">Web API OWIN güvenilir Hizmetleri'nde kullanır</span><span class="sxs-lookup"><span data-stu-id="a2f88-222">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="a2f88-223">Güvenilir hizmetler kullanarak WCF iletişimi</span><span class="sxs-lookup"><span data-stu-id="a2f88-223">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* <span data-ttu-id="a2f88-224">Ek ters proxy yapılandırma seçenekleri için ApplicationGateway/Http bölümüne başvurun [özelleştirme Service Fabric kümesi ayarlarını](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="a2f88-224">For additional reverse proxy configuration options, refer ApplicationGateway/Http section in [Customize Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
