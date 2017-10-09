---
title: "aaaConnect ve Azure Service Fabric hizmetleriyle iletişim | Microsoft Docs"
description: "Nasıl tooresolve, bağlanmak ve Service Fabric hizmetleriyle iletişim öğrenin."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a><span data-ttu-id="3336f-103">Bağlanma ve Service Fabric Hizmetleri ile iletişim</span><span class="sxs-lookup"><span data-stu-id="3336f-103">Connect and communicate with services in Service Fabric</span></span>
<span data-ttu-id="3336f-104">Service Fabric içinde bir hizmet birden çok VM genellikle dağıtılmış bir Service Fabric kümesindeki herhangi bir yerde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3336f-104">In Service Fabric, a service runs somewhere in a Service Fabric cluster, typically distributed across multiple VMs.</span></span> <span data-ttu-id="3336f-105">Bu tek bir yerde tooanother hello hizmet sahibi tarafından ya da otomatik olarak Service Fabric tarafından taşınabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-105">It can be moved from one place tooanother, either by hello service owner, or automatically by Service Fabric.</span></span> <span data-ttu-id="3336f-106">Hizmetleri statik olarak bağlı tooa belirli makine veya adresi olmayan.</span><span class="sxs-lookup"><span data-stu-id="3336f-106">Services are not statically tied tooa particular machine or address.</span></span>

<span data-ttu-id="3336f-107">Service Fabric uygulaması genellikle burada her hizmet özelleştirilmiş bir görev gerçekleştiren birçok farklı hizmetlerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="3336f-107">A Service Fabric application is generally composed of many different services, where each service performs a specialized task.</span></span> <span data-ttu-id="3336f-108">Bu hizmetler birbirine tooform ile bir web uygulaması farklı kısımlarını işleme gibi bir tam işlevi iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-108">These services may communicate with each other tooform a complete function, such as rendering different parts of a web application.</span></span> <span data-ttu-id="3336f-109">İstemci tooand bağlanan uygulamaları Hizmetleri ile iletişim vardır.</span><span class="sxs-lookup"><span data-stu-id="3336f-109">There are also client applications that connect tooand communicate with services.</span></span> <span data-ttu-id="3336f-110">Bu belgede ele nasıl tooset ile ve hizmetlerinizi Service Fabric içinde arasında iletişim kurma.</span><span class="sxs-lookup"><span data-stu-id="3336f-110">This document discusses how tooset up communication with and between your services in Service Fabric.</span></span>

<span data-ttu-id="3336f-111">Bu Microsoft Virtual Academy video Ayrıca hizmet iletişimi ele alınmıştır:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span><span class="sxs-lookup"><span data-stu-id="3336f-111">This Microsoft Virtual Academy video also discusses service communication: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965"></span></span>  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a><span data-ttu-id="3336f-112">Kendi Protokolü Getir</span><span class="sxs-lookup"><span data-stu-id="3336f-112">Bring your own protocol</span></span>
<span data-ttu-id="3336f-113">Service Fabric, hizmetlerin hello yaşam döngüsünü yönetmenize yardımcı olur, ancak hizmetlerinizi neler hakkında kararlar yapmaz.</span><span class="sxs-lookup"><span data-stu-id="3336f-113">Service Fabric helps manage hello lifecycle of your services but it does not make decisions about what your services do.</span></span> <span data-ttu-id="3336f-114">Bu iletişim içerir.</span><span class="sxs-lookup"><span data-stu-id="3336f-114">This includes communication.</span></span> <span data-ttu-id="3336f-115">Gelen istekleri için bir uç nokta yukarı hizmetinizin fırsat tooset olduğundan, Service Fabric tarafından hizmetiniz açıldığında ne olursa olsun protokolü veya iletişim yığını kullanarak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="3336f-115">When your service is opened by Service Fabric, that's your service's opportunity tooset up an endpoint for incoming requests, using whatever protocol or communication stack you want.</span></span> <span data-ttu-id="3336f-116">Hizmetinizi normal üzerinde dinler **IP: BağlantıNoktası** bir URI gibi herhangi bir adres düzeni kullanarak adres.</span><span class="sxs-lookup"><span data-stu-id="3336f-116">Your service will listen on a normal **IP:port** address using any addressing scheme, such as a URI.</span></span> <span data-ttu-id="3336f-117">Birden fazla hizmet örneği veya çoğaltmaları bir ana bilgisayar işlemi, bu durumda bunlar toouse farklı bağlantı noktaları gerekir veya Windows hello http.sys çekirdek sürücüsü gibi bir bağlantı noktası paylaşma mekanizması kullanmak paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-117">Multiple service instances or replicas may share a host process, in which case they will either need toouse different ports or use a port-sharing mechanism, such as hello http.sys kernel driver in Windows.</span></span> <span data-ttu-id="3336f-118">Her iki durumda da, her bir hizmet örneği veya bir ana bilgisayar işlemi yinelemede benzersiz olarak adreslenebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3336f-118">In either case, each service instance or replica in a host process must be uniquely addressable.</span></span>

![Hizmet uç noktaları][1]

## <a name="service-discovery-and-resolution"></a><span data-ttu-id="3336f-120">Hizmet bulma ve çözümleme</span><span class="sxs-lookup"><span data-stu-id="3336f-120">Service discovery and resolution</span></span>
<span data-ttu-id="3336f-121">Dağıtılmış bir sistemde Hizmetleri zaman içinde bir makine tooanother taşıyabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-121">In a distributed system, services may move from one machine tooanother over time.</span></span> <span data-ttu-id="3336f-122">Bu kaynak Dengeleme, yükseltmeler, yük devretme veya genişleme dahil olmak üzere çeşitli nedenlerden kaynaklanabilir. Bu, hello hizmet toonodes farklı IP adresleriyle taşır ve hello hizmet dinamik olarak seçilen bağlantı noktası kullanıyorsa farklı bağlantı noktalarını açmanız hizmeti bitiş noktası adreslerini değiştirmek anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3336f-122">This can happen for various reasons, including resource balancing, upgrades, failovers, or scale-out. This means service endpoint addresses change as hello service moves toonodes with different IP addresses, and may open on different ports if hello service uses a dynamically selected port.</span></span>

![Hizmetlerinin dağıtımı][7]

<span data-ttu-id="3336f-124">Service Fabric adlandırma hizmeti bulma ve hizmeti adlı çözüm hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="3336f-124">Service Fabric provides a discovery and resolution service called hello Naming Service.</span></span> <span data-ttu-id="3336f-125">Merhaba adlandırma hizmeti eşleyen bir tablo hizmet örneği üzerinde dinleme toohello uç nokta adresleri adlı tutar.</span><span class="sxs-lookup"><span data-stu-id="3336f-125">hello Naming Service maintains a table that maps named service instances toohello endpoint addresses they listen on.</span></span> <span data-ttu-id="3336f-126">Service Fabric tüm adlandırılmış hizmet örnekleri olarak URI'ler, örneğin temsil benzersiz adlara sahip `"fabric:/MyApplication/MyService"`.</span><span class="sxs-lookup"><span data-stu-id="3336f-126">All named service instances in Service Fabric have unique names represented as URIs, for example, `"fabric:/MyApplication/MyService"`.</span></span> <span data-ttu-id="3336f-127">Merhaba hello hizmetin adını hello hizmet hello ömrü boyunca değiştirmez, hizmetleri taşıdığınızda, değiştirebileceğiniz hello uç nokta adresleri.</span><span class="sxs-lookup"><span data-stu-id="3336f-127">hello name of hello service does not change over hello lifetime of hello service, it's only hello endpoint addresses that can change when services move.</span></span> <span data-ttu-id="3336f-128">Sabit URL'leri sahip ancak başlangıç IP adresi burada değişebilir benzer toowebsites budur.</span><span class="sxs-lookup"><span data-stu-id="3336f-128">This is analogous toowebsites that have constant URLs but where hello IP address may change.</span></span> <span data-ttu-id="3336f-129">Ve Web sitesi URL'leri tooIP adresleri çözümler, hello Web'de benzer tooDNS Service Fabric hizmeti adları tootheir uç noktası adresi eşleşen bir kayıt sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3336f-129">And similar tooDNS on hello web, which resolves website URLs tooIP addresses, Service Fabric has a registrar that maps service names tootheir endpoint address.</span></span>

![Hizmet uç noktaları][2]

<span data-ttu-id="3336f-131">Çözümleme ve tooservices bağlanan bir döngüde çalıştırılacak adımları izleyerek hello içerir:</span><span class="sxs-lookup"><span data-stu-id="3336f-131">Resolving and connecting tooservices involves hello following steps run in a loop:</span></span>

* <span data-ttu-id="3336f-132">**Gidermek**: bir hizmet yayımlandığı Get hello uç nokta hello adlandırma hizmeti.</span><span class="sxs-lookup"><span data-stu-id="3336f-132">**Resolve**: Get hello endpoint that a service has published from hello Naming Service.</span></span>
* <span data-ttu-id="3336f-133">**Connect**: ne olursa olsun, bu uç noktada kullandığı protokol üzerinden toohello hizmetine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3336f-133">**Connect**: Connect toohello service over whatever protocol it uses on that endpoint.</span></span>
* <span data-ttu-id="3336f-134">**Yeniden deneme**: herhangi bir sayıda nedenlerle hello son zaman hello uç noktası adresi çözümlenmiş başlatıldığından beri hello hizmet taşınmışsa örnek için bir bağlantı girişimi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-134">**Retry**: A connection attempt may fail for any number of reasons, for example if hello service has moved since hello last time hello endpoint address was resolved.</span></span> <span data-ttu-id="3336f-135">Bu durumda çözümleme önceki hello ve bağlanma adımları ihtiyacınız denenen toobe ve hello bağlantı başarılı olana kadar bu döngü yinelenir.</span><span class="sxs-lookup"><span data-stu-id="3336f-135">In that case, hello preceding resolve and connect steps need toobe retried, and this cycle is repeated until hello connection succeeds.</span></span>

## <a name="connecting-tooother-services"></a><span data-ttu-id="3336f-136">Tooother Hizmetleri bağlanma</span><span class="sxs-lookup"><span data-stu-id="3336f-136">Connecting tooother services</span></span>
<span data-ttu-id="3336f-137">Bir kümedeki Hello düğümler üzerinde hello olduğundan tooeach bağlanma Hizmetleri başka bir küme içindeki genellikle doğrudan diğer hizmetlerin hello uç noktaları erişebilirsiniz aynı yerel ağ.</span><span class="sxs-lookup"><span data-stu-id="3336f-137">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="3336f-138">toomake hizmetleri arasında daha kolay tooconnect, Service Fabric adlandırma hizmeti kullanan ek hizmetleri hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="3336f-138">toomake is easier tooconnect between services, Service Fabric provides additional services that use hello Naming Service.</span></span> <span data-ttu-id="3336f-139">DNS hizmeti ve bir ters proxy hizmeti.</span><span class="sxs-lookup"><span data-stu-id="3336f-139">A DNS service and a reverse proxy service.</span></span>


### <a name="dns-service"></a><span data-ttu-id="3336f-140">DNS hizmeti</span><span class="sxs-lookup"><span data-stu-id="3336f-140">DNS service</span></span>
<span data-ttu-id="3336f-141">Birçok hizmetler, özellikle kapsayıcılı hizmetler var olan bir URL adı olduğundan mümkün tooresolve olan bu hello standart DNS Protokolü (Merhaba adlandırma hizmeti Protokolü) yerine çok kullanışlı bir yoldur, özellikle uygulamada "kaldırın ve shift" senaryoları.</span><span class="sxs-lookup"><span data-stu-id="3336f-141">Since many services, especially containerized services, can have an existing URL name, being able tooresolve these using hello standard DNS protocol (rather than hello Naming Service protocol) is very convenient, especially in application "lift and shift" scenarios.</span></span> <span data-ttu-id="3336f-142">Bu, tam olarak hangi hello DNS hizmeti yapar olur.</span><span class="sxs-lookup"><span data-stu-id="3336f-142">This is exactly what hello DNS service does.</span></span> <span data-ttu-id="3336f-143">Toomap DNS adları tooa hizmet adı sağlar ve bu nedenle uç noktası IP adresi çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="3336f-143">It enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="3336f-144">Gösterildiği hello Aşağıdaki diyagramda, hello hello Service Fabric kümede çalışan DNS hizmeti, ardından hello adlandırma hizmeti tooreturn hello bitiş noktası adreslerini tooconnect için tarafından çözümlenen DNS adlarını tooservice adlarını eşler.</span><span class="sxs-lookup"><span data-stu-id="3336f-144">As shown in hello following diagram, hello DNS service, running in hello Service Fabric cluster, maps DNS names tooservice names which are then resolved by hello Naming Service tooreturn hello endpoint addresses tooconnect to.</span></span> <span data-ttu-id="3336f-145">Merhaba hizmeti için Hello DNS ad hello oluşturma sırasında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="3336f-145">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Hizmet uç noktaları][9]

<span data-ttu-id="3336f-147">Toouse hello DNS hizmeti nasıl görürüm hakkında daha fazla ayrıntı için [Azure Service Fabric DNS hizmetinde](service-fabric-dnsservice.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3336f-147">For more details on how toouse hello DNS service see [DNS service in Azure Service Fabric](service-fabric-dnsservice.md) article.</span></span>

### <a name="reverse-proxy-service"></a><span data-ttu-id="3336f-148">Ters proxy hizmeti</span><span class="sxs-lookup"><span data-stu-id="3336f-148">Reverse proxy service</span></span>
<span data-ttu-id="3336f-149">Hello ters proxy services HTTP uç noktaları HTTPS dahil olmak üzere sunan hello kümedeki giderir.</span><span class="sxs-lookup"><span data-stu-id="3336f-149">hello reverse proxy addresses services in hello cluster that exposes HTTP endpoints including HTTPS.</span></span> <span data-ttu-id="3336f-150">diğer hizmetler çağırma Hello ters proxy büyük ölçüde basitleştirir ve belirli bir sahip yöntemleriyle URI biçimlendirmek ve hello gidermek, tanıtıcıları bağlanma, başka bir kullanarak bir hizmet toocommunicate için gerekli yeniden deneme adımları adlandırma hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="3336f-150">hello reverse proxy greatly simplifies calling other services and their methods by having a specific URI format and handles hello resolve, connect, retry steps required for one service toocommunicate with another using hello Naming Serivce.</span></span> <span data-ttu-id="3336f-151">Diğer bir deyişle, diğer hizmetler bu URL çağrılması kadar basit hale getirerek çağrılırken Merhaba, adlandırma hizmetinden gizler.</span><span class="sxs-lookup"><span data-stu-id="3336f-151">In other words, it hides hello Naming Service from you when calling other services by making this as simple as calling a URL.</span></span>

![Hizmet uç noktaları][10]

<span data-ttu-id="3336f-153">Nasıl toouse hello ters proxy hizmeti hakkında daha fazla bilgi için bkz [ters proxy Azure Service Fabric](service-fabric-reverseproxy.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3336f-153">For more details on how toouse hello reverse proxy service see [Reverse proxy in Azure Service Fabric](service-fabric-reverseproxy.md) article.</span></span>

## <a name="connections-from-external-clients"></a><span data-ttu-id="3336f-154">Dış istemcilerden gelen bağlantıları</span><span class="sxs-lookup"><span data-stu-id="3336f-154">Connections from external clients</span></span>
<span data-ttu-id="3336f-155">Bir kümedeki Hello düğümler üzerinde hello olduğundan tooeach bağlanma Hizmetleri başka bir küme içindeki genellikle doğrudan diğer hizmetlerin hello uç noktaları erişebilirsiniz aynı yerel ağ.</span><span class="sxs-lookup"><span data-stu-id="3336f-155">Services connecting tooeach other inside a cluster generally can directly access hello endpoints of other services because hello nodes in a cluster are on hello same local network.</span></span> <span data-ttu-id="3336f-156">Bazı ortamlarda, sınırlı bir dizi bağlantı noktası üzerinden harici giriş trafiğini yönlendiren bir yük dengeleyicinin arkasındaki bir küme ancak olabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-156">In some environments, however, a cluster may be behind a load balancer that routes external ingress traffic through a limited set of ports.</span></span> <span data-ttu-id="3336f-157">Bu durumlarda, hizmetleri yine birbirleri ile iletişim kurmak ve adlandırma hizmeti kullanarak bir adres hello ancak ek adımlar çekildiği tooallow dış istemcilere tooconnect tooservices olmalıdır çözmek.</span><span class="sxs-lookup"><span data-stu-id="3336f-157">In these cases, services can still communicate with each other and resolve addresses using hello Naming Service, but extra steps must be taken tooallow external clients tooconnect tooservices.</span></span>

## <a name="service-fabric-in-azure"></a><span data-ttu-id="3336f-158">Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3336f-158">Service Fabric in Azure</span></span>
<span data-ttu-id="3336f-159">Azure Service Fabric kümesi bir Azure yük dengeleyici yer alır.</span><span class="sxs-lookup"><span data-stu-id="3336f-159">A Service Fabric cluster in Azure is placed behind an Azure Load Balancer.</span></span> <span data-ttu-id="3336f-160">Tüm dış trafiğin toohello küme hello yük dengeleyici üzerinden geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3336f-160">All external traffic toohello cluster must pass through hello load balancer.</span></span> <span data-ttu-id="3336f-161">Merhaba yük dengeleyici otomatik olarak trafik iletir rastgele bir verilen bağlantı noktası tooa gelen trafik *düğümü* aynı bağlantı noktasını açın hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3336f-161">hello load balancer will automatically forward traffic inbound on a given port tooa random *node* that has hello same port open.</span></span> <span data-ttu-id="3336f-162">Hello Azure yük dengeleyici yalnızca hello üzerinde açık bağlantı noktalarını bildiği *düğümleri*, bağlantı noktalarının açık kişi tarafından hakkında bilmez *Hizmetleri*.</span><span class="sxs-lookup"><span data-stu-id="3336f-162">hello Azure Load Balancer only knows about ports open on hello *nodes*, it does not know about ports open by individual *services*.</span></span>

![Azure yük dengeleyici ve Service Fabric topolojisi][3]

<span data-ttu-id="3336f-164">Örneğin, sipariş tooaccept bağlantı noktasındaki dış trafiğini içinde **80**, şeyler aşağıdaki hello yapılandırılmış olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="3336f-164">For example, in order tooaccept external traffic on port **80**, hello following things must be configured:</span></span>

1. <span data-ttu-id="3336f-165">Bağlantı noktası 80 üzerinde dinleyen bir hizmet yazma.</span><span class="sxs-lookup"><span data-stu-id="3336f-165">Write a service that listens on port 80.</span></span> <span data-ttu-id="3336f-166">Bağlantı noktası 80'hello hizmetin ServiceManifest.xml yapılandırmak ve bir dinleyici hello hizmetinde, örneğin, bir kendi kendini barındıran web sunucusu açın.</span><span class="sxs-lookup"><span data-stu-id="3336f-166">Configure port 80 in hello service's ServiceManifest.xml and open a listener in hello service, for example, a self-hosted web server.</span></span>

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. <span data-ttu-id="3336f-167">Service Fabric kümesi oluşturma ve bağlantı noktasını belirtin **80** hello hizmetini barındıran hello düğüm türü için bir özel uç nokta bağlantı noktası olarak.</span><span class="sxs-lookup"><span data-stu-id="3336f-167">Create a Service Fabric Cluster in Azure and specify port **80** as a custom endpoint port for hello node type that will host hello service.</span></span> <span data-ttu-id="3336f-168">Birden fazla düğüm türü varsa, ayarlayabileceğiniz bir *yerleştirme kısıtlaması* hello özel uç noktası portunu sahip hello düğüm türünde yalnızca çalıştırdığı hello hizmet tooensure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="3336f-168">If you have more than one node type, you can set up a *placement constraint* on hello service tooensure it only runs on hello node type that has hello custom endpoint port opened.</span></span>

    ![Düğüm türü bir bağlantı noktası açın][4]
3. <span data-ttu-id="3336f-170">Merhaba Küme oluşturulduktan sonra hello Azure yük dengeleyici hello küme kaynak grubu tooforward trafiği 80 numaralı bağlantı noktasında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3336f-170">Once hello cluster has been created, configure hello Azure Load Balancer in hello cluster's Resource Group tooforward traffic on port 80.</span></span> <span data-ttu-id="3336f-171">Hello Azure portal aracılığıyla bir küme oluştururken, bu otomatik olarak yapılandırılan her özel uç nokta bağlantı noktası için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3336f-171">When creating a cluster through hello Azure portal, this is set up automatically for each custom endpoint port that was configured.</span></span>

    ![Hello Azure yük dengeleyici trafiği ilet][5]
4. <span data-ttu-id="3336f-173">Azure yük dengeleyici kullanan bir araştırma toodetermine olup hello veya değil toosend trafiği tooa belirli düğüm.</span><span class="sxs-lookup"><span data-stu-id="3336f-173">hello Azure Load Balancer uses a probe toodetermine whether or not toosend traffic tooa particular node.</span></span> <span data-ttu-id="3336f-174">Merhaba araştırma düzenli aralıklarla denetimleri hello düğümü yanıt vermeyen her düğüm toodetermine üzerinde bir uç nokta.</span><span class="sxs-lookup"><span data-stu-id="3336f-174">hello probe periodically checks an endpoint on each node toodetermine whether or not hello node is responding.</span></span> <span data-ttu-id="3336f-175">Hello araştırma tooreceive yanıt yapılandırılmış birkaç kez sonra başarısız olursa, trafiğin toothat düğümü gönderme hello yük dengeleyici durdurur.</span><span class="sxs-lookup"><span data-stu-id="3336f-175">If hello probe fails tooreceive a response after a configured number of times, hello load balancer stops sending traffic toothat node.</span></span> <span data-ttu-id="3336f-176">Hello Azure portal aracılığıyla bir küme oluştururken, bir yoklama yapılandırılmış her özel uç nokta bağlantı noktası için otomatik olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3336f-176">When creating a cluster through hello Azure portal, a probe is automatically set up for each custom endpoint port that was configured.</span></span>

    ![Hello Azure yük dengeleyici trafiği ilet][8]

<span data-ttu-id="3336f-178">Hello Azure yük dengeleyici ve hello araştırma hakkında hello yalnızca bildiğiniz önemli tooremember olan *düğümleri*, değil hello *Hizmetleri* hello düğümlerinde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="3336f-178">It's important tooremember that hello Azure Load Balancer and hello probe only know about hello *nodes*, not hello *services* running on hello nodes.</span></span> <span data-ttu-id="3336f-179">Hello Azure yük dengeleyici her zaman toohello araştırma yanıt trafiği toonodes gönderir, dikkatli olunması gerekir böylece tooensure Hizmetleri mümkün toorespond toohello araştırma olan hello düğümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-179">hello Azure Load Balancer will always send traffic toonodes that respond toohello probe, so care must be taken tooensure services are available on hello nodes that are able toorespond toohello probe.</span></span>

## <a name="reliable-services-built-in-communication-api-options"></a><span data-ttu-id="3336f-180">Güvenilir hizmetler: Yerleşik iletişim API seçenekleri</span><span class="sxs-lookup"><span data-stu-id="3336f-180">Reliable Services: Built-in communication API options</span></span>
<span data-ttu-id="3336f-181">Merhaba Reliable Services framework birkaç önceden derlenmiş iletişim seçenekleri ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="3336f-181">hello Reliable Services framework ships with several pre-built communication options.</span></span> <span data-ttu-id="3336f-182">programlama modeli, hello iletişimi framework ve hizmetlerinizi yazılan dil programlama hello hello hello seçimine hakkında bir en iyi işinize hello karar bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3336f-182">hello decision about which one will work best for you depends on hello choice of hello programming model, hello communication framework, and hello programming language that your services are written in.</span></span>

* <span data-ttu-id="3336f-183">**Belirli bir protokol:** iletişim framework'ün belirli bir seçim yok ancak tooget bir şey yukarı ve çalışan hızla istediğiniz durumunda hello ideal seçenek sizin için [hizmet remoting](service-fabric-reliable-services-communication-remoting.md), veren Reliable Services ve Reliable Actors için kesin tür belirtilmiş uzak yordam çağrıları.</span><span class="sxs-lookup"><span data-stu-id="3336f-183">**No specific protocol:**  If you don't have a particular choice of communication framework, but you want tooget something up and running quickly, then hello ideal option for you is [service remoting](service-fabric-reliable-services-communication-remoting.md), which allows strongly-typed remote procedure calls for Reliable Services and Reliable Actors.</span></span> <span data-ttu-id="3336f-184">Bu hello kolay ve hızlı şekilde tooget hizmet iletişimi ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="3336f-184">This is hello easiest and fastest way tooget started with service communication.</span></span> <span data-ttu-id="3336f-185">Hizmet remoting service adresleri, bağlantı, yeniden deneyin ve hata işleme çözünürlüğü işler.</span><span class="sxs-lookup"><span data-stu-id="3336f-185">Service remoting handles resolution of service addresses, connection, retry, and error handling.</span></span> <span data-ttu-id="3336f-186">Bu, hem C# ve Java uygulamaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-186">This is available for both C# and Java applications.</span></span>
* <span data-ttu-id="3336f-187">**HTTP**: dilden bağımsız iletişim için HTTP bir endüstri standardı seçim araçları ve HTTP sunucularıyla birçok farklı dillerde, Service Fabric tarafından desteklenen tüm kullanılabilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="3336f-187">**HTTP**: For language-agnostic communication, HTTP provides an industry-standard choice with tools and HTTP servers available in many different languages, all supported by Service Fabric.</span></span> <span data-ttu-id="3336f-188">Hizmetleri dahil olmak üzere, kullanılabilir tüm HTTP yığınını kullanma [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) C# uygulamaları için.</span><span class="sxs-lookup"><span data-stu-id="3336f-188">Services can use any HTTP stack available, including [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) for C# applications.</span></span> <span data-ttu-id="3336f-189">C# ile yazılmış istemcileri hello yararlanabilir `ICommunicationClient` ve `ServicePartitionClient` , ancak sınıfları Java için hello kullan `CommunicationClient` ve `FabricServicePartitionClient` sınıfları [hizmet çözümleme, HTTP bağlantılarını ve yeniden deneme döngüsü](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="3336f-189">Clients written in C# can leverage hello `ICommunicationClient` and `ServicePartitionClient` classes, whereas for Java, use hello `CommunicationClient` and `FabricServicePartitionClient` classes, [for service resolution, HTTP connections, and retry loops](service-fabric-reliable-services-communication.md).</span></span>
* <span data-ttu-id="3336f-190">**WCF**: WCF iletişimi çerçeve olarak kullanan var olan kodu olması durumunda hello kullanabilirsiniz `WcfCommunicationListener` hello sunucu tarafı için ve `WcfCommunicationClient` ve `ServicePartitionClient` hello istemci sınıfları.</span><span class="sxs-lookup"><span data-stu-id="3336f-190">**WCF**: If you have existing code that uses WCF as your communication framework, then you can use hello `WcfCommunicationListener` for hello server side and `WcfCommunicationClient` and `ServicePartitionClient` classes for hello client.</span></span> <span data-ttu-id="3336f-191">Bu ancak yalnızca Windows tabanlı kümelerde C# uygulamaları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3336f-191">This however is only available for C# applications on Windows based clusters.</span></span> <span data-ttu-id="3336f-192">Bu makalede daha fazla ayrıntı için bkz: [WCF tabanlı bir uygulama hello iletişimi yığınının](service-fabric-reliable-services-communication-wcf.md).</span><span class="sxs-lookup"><span data-stu-id="3336f-192">For more details, see this article about [WCF-based implementation of hello communication stack](service-fabric-reliable-services-communication-wcf.md).</span></span>

## <a name="using-custom-protocols-and-other-communication-frameworks"></a><span data-ttu-id="3336f-193">Özel protokoller ve diğer iletişim çerçeveleri kullanma</span><span class="sxs-lookup"><span data-stu-id="3336f-193">Using custom protocols and other communication frameworks</span></span>
<span data-ttu-id="3336f-194">Hizmetleri kullanma herhangi bir protokolü veya framework iletişimi için özel bir ikili protokol TCP yuvaları ya da aracılığıyla akış olaylarını üzerinden olup olmadığını [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) veya [Azure IOT Hub](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="3336f-194">Services can use any protocol or framework for communication, whether its a custom binary protocol over TCP sockets, or streaming events through [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="3336f-195">Service Fabric iletişimi tüm hello toodiscover çalışma ve bağlanmak, iletişim yığını, Tak API'leri sizden soyutlanır sağlar.</span><span class="sxs-lookup"><span data-stu-id="3336f-195">Service Fabric provides communication APIs that you can plug your communication stack into, while all hello work toodiscover and connect is abstracted from you.</span></span> <span data-ttu-id="3336f-196">Bu makalede hello hakkında bkz [güvenilir hizmet iletişim modelini](service-fabric-reliable-services-communication.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="3336f-196">See this article about hello [Reliable Service communication model](service-fabric-reliable-services-communication.md) for more details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3336f-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3336f-197">Next steps</span></span>
<span data-ttu-id="3336f-198">Merhaba kavramları ve hello kullanılabilir API'ler hakkında daha fazla bilgi edinmek [Reliable Services iletişim modelini](service-fabric-reliable-services-communication.md), sonra hızlı şekilde kullanmaya başlamanızı [hizmet remoting](service-fabric-reliable-services-communication-remoting.md) veya ayrıntılı toolearn nasıl gidin toowrite bir kullanarak iletişim dinleyici [OWIN kendini barındırma ile Web API](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="3336f-198">Learn more about hello concepts and APIs available in hello [Reliable Services communication model](service-fabric-reliable-services-communication.md), then get started quickly with [service remoting](service-fabric-reliable-services-communication-remoting.md) or go in-depth toolearn how toowrite a communication listener using [Web API with OWIN self-host](service-fabric-reliable-services-communication-webapi.md).</span></span>

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
