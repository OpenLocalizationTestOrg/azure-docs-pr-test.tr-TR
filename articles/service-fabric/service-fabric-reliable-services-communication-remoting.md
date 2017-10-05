---
title: "<span data-ttu-id=\"62446-101\">Service Fabric hizmeti uzaktan çalışma | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"62446-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"62446-102\">Service Fabric uzak istemciler ve hizmetler uzaktan yordam çağrısı kullanarak Hizmetleri ile iletişim kurmasına olanak sağlar.</span><span class=\"sxs-lookup\"><span data-stu-id=\"62446-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="62446-103">Güvenilir hizmetler ile hizmet uzaktan iletişim</span><span class="sxs-lookup"><span data-stu-id="62446-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="62446-104">Belirli bir iletişim protokolü veya Webapı, Windows Communication Foundation (WCF) veya diğerleri gibi yığın bağlanmayan Hizmetleri için uzak yordam çağrısı için hızlı ve kolay bir şekilde ayarlamak için uzaktan iletişim mekanizması Reliable Services çerçevesi sağlar Hizmetler.</span><span class="sxs-lookup"><span data-stu-id="62446-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="62446-105">Bir hizmeti uzaktan iletişim ayarlama</span><span class="sxs-lookup"><span data-stu-id="62446-105">Set up remoting on a service</span></span>
<span data-ttu-id="62446-106">Bir hizmet için uzaktan iletişim kurma iki basit adımda gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="62446-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="62446-107">Hizmetinizin uygulamak bir arabirim oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62446-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="62446-108">Bu arabirim, hizmeti uzaktan yordam çağrısı için kullanılabilecek yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="62446-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="62446-109">Görev döndüren yöntemler olmalıdır zaman uyumsuz yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="62446-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="62446-110">Arabirimi uygulamalıdır `Microsoft.ServiceFabric.Services.Remoting.IService` hizmet remoting arabirimi olduğunu göstermek için.</span><span class="sxs-lookup"><span data-stu-id="62446-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="62446-111">Remoting dinleyici hizmetinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="62446-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="62446-112">Bu bir `ICommunicationListener` remoting özellikleri sağlayan uygulama.</span><span class="sxs-lookup"><span data-stu-id="62446-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="62446-113">`Microsoft.ServiceFabric.Services.Remoting.Runtime` Ad alanı içeren bir genişletme yöntemi`CreateServiceRemotingListener` varsayılan remoting aktarım protokolünü kullanarak bir uzak dinleyicisi oluşturmak için kullanılan durum bilgisiz ve durum bilgisi olan hizmetler için.</span><span class="sxs-lookup"><span data-stu-id="62446-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="62446-114">Not: `Remoting` ad alanı adı verilen bir ayrı nuget paketi olarak kullanılabilir`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="62446-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="62446-115">Örneğin, aşağıdaki durum bilgisiz hizmeti üzerinden bir uzak yordam çağrısı "Hello World" almak için tek bir yöntemi gösterir.</span><span class="sxs-lookup"><span data-stu-id="62446-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="62446-116">Bağımsız değişkenler ve hizmet arabirimi dönüş türler basit, karmaşık veya özel türleri olabilir, ancak .NET tarafından Serileştirilebilir olmalıdır [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="62446-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="62446-117">Uzak Hizmet yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="62446-117">Call remote service methods</span></span>
<span data-ttu-id="62446-118">Uzaktan iletişim yığını kullanarak bir hizmet yöntemleri çağırma yapılır yerel bir proxy üzerinden hizmete kullanarak `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="62446-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="62446-119">`ServiceProxy` Yöntemi hizmeti uygulayan aynı arabirimini kullanarak yerel bir proxy oluşturur.</span><span class="sxs-lookup"><span data-stu-id="62446-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="62446-120">Proxy ile yalnızca yöntemleri arabirimde uzaktan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62446-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="62446-121">Remoting framework istemciye hizmet sırasında oluşturulan özel durumları yayar.</span><span class="sxs-lookup"><span data-stu-id="62446-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="62446-122">Bu nedenle özel durum işleme mantığı kullanarak istemcide `ServiceProxy` doğrudan hizmet oluşturur özel durumlar işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="62446-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="62446-123">Hizmet Proxy ömrü</span><span class="sxs-lookup"><span data-stu-id="62446-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="62446-124">ServiceProxy oluşturma hafif bir işlem olduğundan, kullanıcı ihtiyaç duydukları kadar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62446-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="62446-125">Kullanıcı gerek sürece hizmeti proxy'si yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="62446-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="62446-126">Kullanıcı aynı proxy özel durum durumunda yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62446-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="62446-127">Her ServiceProxy kablo üzerinden ileti göndermek için kullanılan çoğaltmayla istemci içerir.</span><span class="sxs-lookup"><span data-stu-id="62446-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="62446-128">API istenirken kullanılan iletişim istemci geçerli olup olmadığını görmek için iç onay sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="62446-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="62446-129">Bu sonuca bağlı olarak, iletişim istemci yeniden oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="62446-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="62446-130">Bu nedenle kullanıcı gerekmez serviceproxy özel durum durumunda yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="62446-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="62446-131">ServiceProxyFactory yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="62446-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="62446-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) farklı remoting arabirimleri için proxy oluşturan bir üreteci değil.</span><span class="sxs-lookup"><span data-stu-id="62446-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="62446-133">Proxy oluşturmak için API ServiceProxy.Create kullanırsanız, framework ServiceProxyFactory singelton oluşturur.</span><span class="sxs-lookup"><span data-stu-id="62446-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="62446-134">Geçersiz kılmak gerektiğinde el ile oluşturmak kullanışlıdır [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) özellikleri.</span><span class="sxs-lookup"><span data-stu-id="62446-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="62446-135">Fabrika pahalı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="62446-135">Factory is an expensive operation.</span></span> <span data-ttu-id="62446-136">ServiceProxyFactory iletişimi istemci önbelleğini korur.</span><span class="sxs-lookup"><span data-stu-id="62446-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="62446-137">Mümkün olduğunca uzun bir süredir ServiceProxyFactory önbelleğe en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="62446-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="62446-138">Remoting özel durum işleme</span><span class="sxs-lookup"><span data-stu-id="62446-138">Remoting Exception Handling</span></span>
<span data-ttu-id="62446-139">Hizmeti API'si tarafından oluşturulan tüm uzak özel durum, istemciye AggregateException gönderilir.</span><span class="sxs-lookup"><span data-stu-id="62446-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="62446-140">RemoteExceptions olmalıdır DataContract seri hale getirilebilir aksi [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) proxy API, seri hale getirme hatası ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="62446-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="62446-141">ServiceProxy için oluşturulan hizmet bölümü için tüm yük devretme özel durumu işler.</span><span class="sxs-lookup"><span data-stu-id="62446-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="62446-142">Yük devretme Exceptions(Non-Transient Exceptions) ise uç noktaları yeniden çözümlediği ve doğru uç nokta çağrısıyla yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="62446-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="62446-143">Yük devretme özel durumu için yeniden deneme sayısı belirsiz.</span><span class="sxs-lookup"><span data-stu-id="62446-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="62446-144">TransientExceptions durumunda çağrı yalnızca deneme.</span><span class="sxs-lookup"><span data-stu-id="62446-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="62446-145">[OperationRetrySettings] tarafından sağlanan varsayılan yeniden deneme parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="62446-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="62446-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Kullanıcı OperationRetrySettings ServiceProxyFactory oluşturucusuna geçirerek bu değerleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62446-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62446-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62446-147">Next steps</span></span>
* [<span data-ttu-id="62446-148">Web API OWIN güvenilir Hizmetleri'ndeki ile</span><span class="sxs-lookup"><span data-stu-id="62446-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="62446-149">Güvenilir hizmetler ile WCF iletişim</span><span class="sxs-lookup"><span data-stu-id="62446-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="62446-150">Güvenilir hizmetler için iletişimin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="62446-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
