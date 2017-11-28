---
title: "aaaReliable Hizmetleri iletişimi genel bakış | Microsoft Docs"
description: "Açılış dinleyicileri Hizmetleri dahil olmak üzere, uç noktaları çözme ve hizmetleri arasında iletişim kurarken hello Reliable Services iletişim modeline genel bakış."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="f0d07-103">Nasıl toouse hello Reliable Services iletişim API'leri</span><span class="sxs-lookup"><span data-stu-id="f0d07-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="f0d07-104">Bir platform olarak Azure Service Fabric Hizmetleri arasındaki iletişim hakkında tamamen bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="f0d07-105">Tüm protokoller ve yığınları UDP tooHTTP kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="f0d07-106">Bu hizmetleri nasıl iletişim kurmanız gerekir toohello Hizmet Geliştirici toochoose olur.</span><span class="sxs-lookup"><span data-stu-id="f0d07-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="f0d07-107">yerleşik iletişim toobuild kullanabileceğiniz API'leri yanı sıra, özel iletişim bileşenlerinizin yığınlar Hello Reliable Services uygulama çerçevesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="f0d07-108">Hizmet iletişim kurma ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f0d07-108">Set up service communication</span></span>
<span data-ttu-id="f0d07-109">Merhaba güvenilir Hizmetleri API hizmeti iletişimi için basit bir arabirim kullanır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="f0d07-110">tooopen hizmetiniz için bir uç nokta yalnızca bu arabirimi uygular:</span><span class="sxs-lookup"><span data-stu-id="f0d07-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="f0d07-111">Hizmet tabanlı sınıfı yöntemi geçersiz kılma seçeneğinde döndürerek iletişimi dinleyicisi uygulamanızı daha sonra ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0d07-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="f0d07-112">Durum bilgisi olmayan hizmetler için:</span><span class="sxs-lookup"><span data-stu-id="f0d07-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="f0d07-113">Durum bilgisi olan hizmetler için:</span><span class="sxs-lookup"><span data-stu-id="f0d07-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="f0d07-114">Durum bilgisi olan güvenilir hizmetler Java'da henüz desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f0d07-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="f0d07-115">Her iki durumda da dinleyicileri koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f0d07-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="f0d07-116">Bu, büyük olasılıkla birden çok dinleyici kullanarak farklı protokoller kullanarak birden çok uç noktalarda hizmet toolisten sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="f0d07-117">Örneğin, bir HTTP dinleyicisi ve ayrı bir Web yuvası dinleyicisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="f0d07-118">Her dinleyicisi adı ve hello elde edilen koleksiyonunu alır *ad: adresi* bir istemci bir hizmet örneği veya bir bölüm için dinleme adresleri hello istediğinde, çiftleri bir JSON nesnesi olarak temsil.</span><span class="sxs-lookup"><span data-stu-id="f0d07-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="f0d07-119">Bir durum bilgisiz hizmetinde hello geçersiz kılma ServiceInstanceListeners koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f0d07-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="f0d07-120">A `ServiceInstanceListener` işlevi toocreate içeren bir `ICommunicationListener(C#) / CommunicationListener(Java)` ve bir ad sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="f0d07-121">Durum bilgisi olan hizmetler için hello geçersiz kılma ServiceReplicaListeners koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f0d07-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="f0d07-122">Bu durum bilgisiz kendisine karşılık gelen biraz farklı değildir çünkü bir `ServiceReplicaListener` seçeneği tooopen sahip bir `ICommunicationListener` ikincil çoğaltmalar üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f0d07-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="f0d07-123">Yalnızca bir hizmet birden çok iletişim dinleyicileri kullanabilirsiniz, ancak aynı zamanda hangi dinleyicileri ikincil çoğaltmalar üzerinde isteklerini kabul etmek ve hangilerinin yalnızca birincil çoğaltmalar üzerinde dinleme belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0d07-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="f0d07-124">Örneğin, yalnızca birincil çoğaltmalar RPC çağrılarını alan bir ServiceRemotingListener sahip olabilir ve okuma geçen ikinci, özel bir dinleyici ikincil çoğaltmaların üzerine HTTP üzerinden ister:</span><span class="sxs-lookup"><span data-stu-id="f0d07-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="f0d07-125">Hizmet için her dinleyicisi birden çok dinleyici oluştururken **gerekir** benzersiz bir ad verilmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="f0d07-126">Son olarak, hello hello hizmeti için gerekli olan hello uç noktaları açıklayan [hizmet bildirimi](service-fabric-application-model.md) uç noktalarda hello bölümünde.</span><span class="sxs-lookup"><span data-stu-id="f0d07-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="f0d07-127">Merhaba iletişimi dinleyici tooit hello ayrılan hello uç nokta kaynaklara erişebilir `CodePackageActivationContext` hello içinde `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="f0d07-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="f0d07-128">Merhaba dinleyicisi açıldığında isteklerini dinlemeye başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0d07-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="f0d07-129">Uç nokta kaynaklardır ortak toohello tüm hizmet paketi ve hello hizmet paketi etkinleştirildiğinde Service Fabric tarafından ayrılır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="f0d07-130">Aynı aynı ServiceHost paylaşmak hello barındırılan birden çok hizmet çoğaltmalar Merhaba bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="f0d07-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="f0d07-131">Başka bir deyişle, bu hello iletişimi dinleyicisi bağlantı noktası paylaşımı desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="f0d07-132">Merhaba hello dinleme adresi oluşturduğunda bunu yapmanın yolu hello iletişimi dinleyici toouse hello için bölüm kimliği ve çoğaltma/örnek kimliği önerilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="f0d07-133">Hizmeti adresi kaydı</span><span class="sxs-lookup"><span data-stu-id="f0d07-133">Service address registration</span></span>
<span data-ttu-id="f0d07-134">Bir sistem hizmeti adlı hello *adlandırma hizmeti* Service Fabric kümelerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="f0d07-135">Merhaba adlandırma Hizmetleri ve her bir örneği veya çoğaltma hello hizmetinin dinlediği adresleri için bir kayıt hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="f0d07-136">Ne zaman hello `OpenAsync(C#) / openAsync(Java)` yöntemi bir `ICommunicationListener(C#) / CommunicationListener(Java)` tamamlar, dönüş değeri hello Adlandırma Hizmeti kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="f0d07-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="f0d07-137">Bu adlandırma hizmeti olarak yayımlanan hello değeri herhangi bir şey hiç olabilir bir dize alır değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="f0d07-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="f0d07-138">Merhaba hizmetinden hello adlandırma hizmeti için bir adres için söylediğinizde istemcileri gördükleri Bu dize değeridir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="f0d07-139">Service Fabric hizmet adına göre bu adres için istemcileri ve diğer hizmetleri toothen izin API'leri isteyin sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="f0d07-140">Merhaba hizmeti adresi statik olmadığı için bu önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="f0d07-141">Hizmetleri kaynak Dengeleme ve kullanılabilirlik amacıyla hello kümedeki taşındı.</span><span class="sxs-lookup"><span data-stu-id="f0d07-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="f0d07-142">Bu adresi bir hizmet için dinleme tooresolve hello ver hello mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="f0d07-143">Nasıl bir iletişim dinleyici toowrite bakın, tam bir gözden geçirme [OWIN kendi kendine barındırma ile Service Fabric Web API Hizmetleri](service-fabric-reliable-services-communication-webapi.md) Java için kendi HTTP sunucusu uygulamasını yazabilirsiniz gelirken, C# ' ta EchoServer bakın https://github.com/Azure-Samples/service-fabric-java-getting-started örneğe.</span><span class="sxs-lookup"><span data-stu-id="f0d07-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="f0d07-144">Bir hizmet ile iletişim</span><span class="sxs-lookup"><span data-stu-id="f0d07-144">Communicating with a service</span></span>
<span data-ttu-id="f0d07-145">Merhaba güvenilir Hizmetleri API Hizmetleri ile iletişim kitaplıkları toowrite istemcileri aşağıdaki hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="f0d07-146">Hizmet uç noktası çözümleme</span><span class="sxs-lookup"><span data-stu-id="f0d07-146">Service endpoint resolution</span></span>
<span data-ttu-id="f0d07-147">bir hizmeti ile Merhaba ilk adım toocommunication tooresolve bir uç nokta adresi hello bölüm veya tootalk için istediğiniz hello hizmet örneği, ' dir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="f0d07-148">Merhaba `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` yardımcı programının sınıfıdır hizmetin çalışma zamanında hello uç noktası belirlemek istemcileri yardımcı olan basit bir temel tür.</span><span class="sxs-lookup"><span data-stu-id="f0d07-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="f0d07-149">Service Fabric terminolojisinde hizmetin hello uç noktası belirleme hello başvurulan tooas hello işlemidir *hizmet uç noktası çözümleme*.</span><span class="sxs-lookup"><span data-stu-id="f0d07-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="f0d07-150">Varsayılan ayarları kullanarak ServicePartitionResolver tooconnect tooservices bir küme içinde oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="f0d07-151">Merhaba kullanım çoğu durum için önerilen şudur:</span><span class="sxs-lookup"><span data-stu-id="f0d07-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="f0d07-152">tooconnect tooservices farklı bir kümede bir küme ağ geçidi uç noktaları kümesiyle bir ServicePartitionResolver oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="f0d07-153">Ağ geçidi uç noktaları toohello bağlanmak için yalnızca farklı uç noktalar olduğuna dikkat edin aynı küme.</span><span class="sxs-lookup"><span data-stu-id="f0d07-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="f0d07-154">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f0d07-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="f0d07-155">Alternatif olarak, `ServicePartitionResolver` oluşturmak için bir işlev verilebilir bir `FabricClient` toouse dahili olarak:</span><span class="sxs-lookup"><span data-stu-id="f0d07-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="f0d07-156">`FabricClient`kullanılan toocommunicate hello kümede çeşitli yönetim işlemlerini için hello Service Fabric kümesi ile olan hello nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="f0d07-157">Hizmet bölüm çözümleyici kümenizle nasıl etkileşim kurduğu üzerinde daha fazla denetim istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="f0d07-158">`FabricClient`önemli tooreuse nedenle dahili olarak önbelleğe alma gerçekleştirir ve genellikle pahalı toocreate `FabricClient` mümkün olduğunca örnekleri.</span><span class="sxs-lookup"><span data-stu-id="f0d07-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="f0d07-159">Kullanılan tooretrieve hello sonra bir hizmet veya hizmet bölüm bölümlenmiş Hizmetleri için Adres Çözümleme yöntemidir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="f0d07-160">Bir hizmet adresi kolayca bir ServicePartitionResolver kullanılarak çözülebilir, ancak daha fazla iş gereklidir tooensure hello çözülmüş adresi doğru şekilde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="f0d07-161">Merhaba bağlantı denemesi geçici bir hata nedeniyle başarısız oldu ve yeniden denenebilir olup olmadığını istemciniz toodetect gerekir (örn., hizmet taşınmış veya geçici olarak kullanım dışı), ya da kalıcı bir hata (örneğin, hizmet silindi veya hello istenen kaynak artık yok).</span><span class="sxs-lookup"><span data-stu-id="f0d07-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="f0d07-162">Hizmet örneği veya çoğaltmaları düğümü toonode birden çok nedeniyle herhangi bir zamanda taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0d07-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="f0d07-163">hello hizmeti adresi ServicePartitionResolver çözümlendi, istemci kodunuzun tooconnect çalışır hello zamanına göre eski olabilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="f0d07-164">Bu durumda yeniden hello istemci toore Çöz hello adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="f0d07-165">Merhaba önceki sağlama `ResolvedServicePartition` , çözümleyici gereksinimlerini tootry yeniden hello yerine yalnızca bir önbelleğe alınan adresi almak gösterir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="f0d07-166">Genellikle, hello istemci kodu ServicePartitionResolver hello ile doğrudan işe.</span><span class="sxs-lookup"><span data-stu-id="f0d07-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="f0d07-167">Oluşturulan ve toocommunication istemci hello güvenilir Hizmetleri API factory'leri geçirildi.</span><span class="sxs-lookup"><span data-stu-id="f0d07-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="f0d07-168">Merhaba oluşturucuları kullanma hello çözümleyici dahili olarak toogenerate Hizmetleri ile kullanılan toocommunicate olabilecek istemci nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f0d07-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="f0d07-169">İletişim istemcileri ve oluşturucuları</span><span class="sxs-lookup"><span data-stu-id="f0d07-169">Communication clients and factories</span></span>
<span data-ttu-id="f0d07-170">Merhaba iletişimi Fabrika kitaplığı yeniden deneniyor bağlantıları tooresolved hizmet uç noktaları kolaylaştırır tipik bir hata işleme yeniden deneme deseni uygular.</span><span class="sxs-lookup"><span data-stu-id="f0d07-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="f0d07-171">Merhaba hata işleyicileri sunarken hello Fabrika kitaplığı hello yeniden deneme mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="f0d07-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`tooa Service Fabric hizmeti iletişim kurabilirsiniz istemcileri üreten bir iletişim istemci sınıf üreticisi tarafından uygulanan hello temel arabirimi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="f0d07-173">Burada hello istemci toocommunicate istediği hello Service Fabric hizmeti tarafından kullanılan hello iletişimi yığında CommunicationClientFactory bağlıdır hello uyarlamasını hello.</span><span class="sxs-lookup"><span data-stu-id="f0d07-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="f0d07-174">Merhaba güvenilir Hizmetleri API sağlayan bir `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="f0d07-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="f0d07-175">Bu temel bir hello CommunicationClientFactory arabirimi uygulamasını sağlar ve ortak tooall hello iletişimi yığınları olan görevleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="f0d07-176">(ServicePartitionResolver toodetermine hello hizmet uç noktası kullanarak bu görevleri dahil).</span><span class="sxs-lookup"><span data-stu-id="f0d07-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="f0d07-177">İstemcileri genellikle belirli toohello iletişim yığını olan hello soyut CommunicationClientFactoryBase sınıfı toohandle mantığı uygular.</span><span class="sxs-lookup"><span data-stu-id="f0d07-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="f0d07-178">Merhaba iletişimi istemci yalnızca bir adresi alır ve tooconnect tooa hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="f0d07-179">Merhaba istemci istediği ne olursa olsun protokolünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0d07-179">hello client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="f0d07-180">Merhaba istemci Fabrika iletişimi istemcileri oluşturmak için öncelikle sorumludur.</span><span class="sxs-lookup"><span data-stu-id="f0d07-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="f0d07-181">Bir HTTP istemcisi gibi kalıcı bir bağlantı korumak olmayan istemciler için hello Fabrika toocreate ve dönüş hello istemci yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="f0d07-182">Merhaba bağlantı toobe yeniden oluşturulması gerekip gerekmediğini bazı ikili protokolleri gibi kalıcı bir bağlantı korumak diğer protokolleri de hello Fabrika toodetermine tarafından doğrulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f0d07-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="f0d07-183">Son olarak, bir özel durum oluştuğunda hangi eylemini tootake belirlemek için bir özel durum işleyici sorumludur.</span><span class="sxs-lookup"><span data-stu-id="f0d07-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="f0d07-184">Özel durumlar kategorilere içine **yeniden denenebilir** ve **denenemeyen**.</span><span class="sxs-lookup"><span data-stu-id="f0d07-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="f0d07-185">**Denenemeyen** özel durumlar yalnızca geri toohello çağıran işlenemezse.</span><span class="sxs-lookup"><span data-stu-id="f0d07-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="f0d07-186">**yeniden denenebilir** özel durumlar daha fazla kategorilere ayrılabilir içine **geçici** ve **geçici olmayan**.</span><span class="sxs-lookup"><span data-stu-id="f0d07-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="f0d07-187">**Geçici** istisnaları, yalnızca hello hizmet uç noktası adresi yeniden çözümlemeden yeniden denenebilir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="f0d07-188">Bu geçici ağ sorunları içerir veya hizmet hata yanıtları hello hizmet uç noktası adresi gösteren olanlar dışındaki mevcut değil.</span><span class="sxs-lookup"><span data-stu-id="f0d07-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="f0d07-189">**Geçici olmayan** istisnaları hello hizmet uç noktası adresi toobe yeniden çözülmüş gerektirenler.</span><span class="sxs-lookup"><span data-stu-id="f0d07-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="f0d07-190">Bunlar hello Hizmeti uç noktası, hello hizmet tooa farklı bir düğüme taşındıktan belirten erişilemedi belirtmek özel durumları içerir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="f0d07-191">Merhaba `TryHandleException` belirli bir özel durum hakkında karar verir.</span><span class="sxs-lookup"><span data-stu-id="f0d07-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="f0d07-192">Varsa, **bilmediği** hangi bir özel durum hakkında kararlar toomake döndürme zorunluluğu **false**.</span><span class="sxs-lookup"><span data-stu-id="f0d07-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="f0d07-193">Varsa, **bilen** hangi karar toomake, hello sonuç uygun şekilde ayarlama ve döndürme **doğru**.</span><span class="sxs-lookup"><span data-stu-id="f0d07-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="f0d07-194">Tüm bir araya getirme</span><span class="sxs-lookup"><span data-stu-id="f0d07-194">Putting it all together</span></span>
<span data-ttu-id="f0d07-195">İle bir `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, ve `IExceptionHandler(C#) / ExceptionHandler(Java)` bir iletişim protokolü, yerleşik bir `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` hepsini bir araya sarmalar ve hello hata işleme ve hizmet bölümü adres çözünürlüğü döngü bu bileşenlerin çevresinde sağlar.</span><span class="sxs-lookup"><span data-stu-id="f0d07-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="f0d07-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f0d07-196">Next steps</span></span>
* <span data-ttu-id="f0d07-197">HTTP iletişimi Hizmetleri'nde arasında örneğine bakın bir [C# örnek proje github'da](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) veya [Java örnek proje github'da](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="f0d07-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="f0d07-198">Güvenilir hizmetler remoting ile uzak yordam çağrıları</span><span class="sxs-lookup"><span data-stu-id="f0d07-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="f0d07-199">Web API OWIN güvenilir Hizmetleri'nde kullanır</span><span class="sxs-lookup"><span data-stu-id="f0d07-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="f0d07-200">Güvenilir hizmetler kullanarak WCF iletişimi</span><span class="sxs-lookup"><span data-stu-id="f0d07-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
