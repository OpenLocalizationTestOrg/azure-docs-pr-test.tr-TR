---
title: "Azure Service Fabric aaaService uzaktan çalışma | Microsoft Docs"
description: "Service Fabric uzak istemcilerin ve toocommunicate ile bir uzak yordam çağrısı kullanarak hizmetleri."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="e4c50-103">Güvenilir hizmetler ile hizmet uzaktan iletişim</span><span class="sxs-lookup"><span data-stu-id="e4c50-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4c50-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="e4c50-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="e4c50-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="e4c50-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="e4c50-106">Merhaba Reliable Services framework uzaktan iletişim mekanizması tooquickly sağlar ve uzak yordam çağrısı Hizmetleri için kolayca ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e4c50-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="e4c50-107">Bir hizmeti uzaktan iletişim ayarlama</span><span class="sxs-lookup"><span data-stu-id="e4c50-107">Set up remoting on a service</span></span>
<span data-ttu-id="e4c50-108">Bir hizmet için uzaktan iletişim kurma iki basit adımda gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="e4c50-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="e4c50-109">Hizmet tooimplement için bir arabirimi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e4c50-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="e4c50-110">Bu arabirim, hizmeti uzaktan yordam çağrısı için kullanılabilen hello yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e4c50-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="e4c50-111">Merhaba yöntemleri görev döndürme olmalıdır zaman uyumsuz yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="e4c50-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="e4c50-112">Merhaba arabirimi uygulanmalı `microsoft.serviceFabric.services.remoting.Service` hizmet hello toosignal remoting arabirimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="e4c50-113">Remoting dinleyici hizmetinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4c50-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="e4c50-114">Bu bir `CommunicationListener` remoting özellikleri sağlayan uygulama.</span><span class="sxs-lookup"><span data-stu-id="e4c50-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="e4c50-115">`FabricTransportServiceRemotingListener`kullanılan toocreate hello varsayılan remoting aktarım protokolünü kullanarak bir uzak dinleyicisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="e4c50-116">Örneğin, hello aşağıdaki durum bilgisiz hizmeti uzaktan yordam çağrısı üzerinden tek bir yöntem tooget "Hello World" kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="e4c50-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="e4c50-117">Merhaba bağımsız değişkenler ve hello hello hizmet arabirimi türlerinde basit, karmaşık veya özel türleri olabilir, ancak bunlar Serileştirilebilir olmalıdır döndürür.</span><span class="sxs-lookup"><span data-stu-id="e4c50-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="e4c50-118">Uzak Hizmet yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="e4c50-118">Call remote service methods</span></span>
<span data-ttu-id="e4c50-119">Merhaba remoting yığını kullanarak bir hizmet yöntemleri çağırma yapılır hello üzerinden bir yerel ara toohello hizmeti kullanarak `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e4c50-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="e4c50-120">Merhaba `ServiceProxyBase` yöntemi, hizmet hello aynı arabirimini uygulayan hello kullanarak yerel bir proxy oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4c50-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="e4c50-121">Proxy ile yalnızca yöntemleri hello arabirimde uzaktan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4c50-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="e4c50-122">Merhaba remoting framework hello hizmet toohello istemcide oluşturulan özel durumları yayar.</span><span class="sxs-lookup"><span data-stu-id="e4c50-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="e4c50-123">Bu nedenle özel durum işleme mantığı kullanarak hello istemcide `ServiceProxyBase` doğrudan hizmet atar hello özel durumlar işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="e4c50-124">Hizmet Proxy ömrü</span><span class="sxs-lookup"><span data-stu-id="e4c50-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="e4c50-125">ServiceProxy oluşturma hafif bir işlem olduğundan, kullanıcı ihtiyaç duydukları kadar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4c50-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="e4c50-126">Kullanıcı gerek sürece hizmeti proxy'si yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="e4c50-127">Kullanıcı yeniden kullanabilir hello aynı proxy özel durum durumunda.</span><span class="sxs-lookup"><span data-stu-id="e4c50-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="e4c50-128">Her ServiceProxy hello kablo üzerinden iletişimi kullanılan istemci toosend iletilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="e4c50-129">Kullanılan iletişim istemcinin geçerli olup olmadığını API istenirken iç onay toosee sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="e4c50-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="e4c50-130">Bu sonuca göre hello iletişimi istemci yeniden oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="e4c50-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="e4c50-131">Bu nedenle kullanıcı gerek kalmaz toorecreate serviceproxy özel durum durumunda.</span><span class="sxs-lookup"><span data-stu-id="e4c50-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="e4c50-132">ServiceProxyFactory yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="e4c50-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="e4c50-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) farklı remoting arabirimleri için proxy oluşturan bir üreteci değil.</span><span class="sxs-lookup"><span data-stu-id="e4c50-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="e4c50-134">API kullanırsanız `ServiceProxyBase.create` proxy oluşturmak, ardından framework oluşturan bir `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="e4c50-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="e4c50-135">Toooverride gerektiğinde yararlı toocreate biri el ile olmasından [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) özellikleri.</span><span class="sxs-lookup"><span data-stu-id="e4c50-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="e4c50-136">Fabrika pahalı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-136">Factory is an expensive operation.</span></span> <span data-ttu-id="e4c50-137">`FabricServiceProxyFactory`iletişim istemci önbelleğini korur.</span><span class="sxs-lookup"><span data-stu-id="e4c50-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="e4c50-138">En iyi uygulamadır toocache `FabricServiceProxyFactory` mümkün olduğunca uzun bir süredir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="e4c50-139">Remoting özel durum işleme</span><span class="sxs-lookup"><span data-stu-id="e4c50-139">Remoting Exception Handling</span></span>
<span data-ttu-id="e4c50-140">Hizmeti API'si tarafından tüm hello uzak durum gönderilen geri toohello istemci RuntimeException veya FabricException olarak.</span><span class="sxs-lookup"><span data-stu-id="e4c50-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="e4c50-141">ServiceProxy hello hizmet bölüm için oluşturulan tüm yük devretme özel durumu işler.</span><span class="sxs-lookup"><span data-stu-id="e4c50-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="e4c50-142">Merhaba doğru uç noktası ile yük devretme Exceptions(Non-Transient Exceptions) ve yeniden deneme hello çağrı ise hello uç noktaları yeniden çözümler.</span><span class="sxs-lookup"><span data-stu-id="e4c50-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="e4c50-143">Yük devretme özel durumu için yeniden deneme sayısı belirsiz.</span><span class="sxs-lookup"><span data-stu-id="e4c50-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="e4c50-144">TransientExceptions durumunda hello çağrı yalnızca deneme.</span><span class="sxs-lookup"><span data-stu-id="e4c50-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="e4c50-145">[OperationRetrySettings] tarafından sağlanan varsayılan yeniden deneme parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="e4c50-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="e4c50-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Kullanıcı OperationRetrySettings nesne tooServiceProxyFactory Oluşturucusu geçirerek bu değerleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4c50-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4c50-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e4c50-147">Next steps</span></span>
* [<span data-ttu-id="e4c50-148">Güvenilir hizmetler için iletişimin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="e4c50-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
