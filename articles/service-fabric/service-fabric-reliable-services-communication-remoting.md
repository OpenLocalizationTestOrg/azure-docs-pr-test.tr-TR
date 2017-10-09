---
title: "Service Fabric aaaService uzaktan çalışma | Microsoft Docs"
description: "Service Fabric uzak istemcilerin ve toocommunicate ile bir uzak yordam çağrısı kullanarak hizmetleri."
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
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="2c3ca-103">Güvenilir hizmetler ile hizmet uzaktan iletişim</span><span class="sxs-lookup"><span data-stu-id="2c3ca-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="2c3ca-104">Tooa belirli iletişim protokolü veya Webapı, Windows Communication Foundation (WCF) veya diğerleri gibi yığını bulunmayan hizmet bağlı hello Reliable Services framework uzaktan iletişim mekanizması tooquickly sağlar ve uzak yordam çağrısı kolayca ayarlayın Hizmetler için.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="2c3ca-105">Bir hizmeti uzaktan iletişim ayarlama</span><span class="sxs-lookup"><span data-stu-id="2c3ca-105">Set up remoting on a service</span></span>
<span data-ttu-id="2c3ca-106">Bir hizmet için uzaktan iletişim kurma iki basit adımda gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="2c3ca-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="2c3ca-107">Hizmet tooimplement için bir arabirimi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="2c3ca-108">Bu arabirim, hizmeti uzaktan yordam çağrısı için kullanılabilecek hello yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="2c3ca-109">Merhaba yöntemleri görev döndürme olmalıdır zaman uyumsuz yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="2c3ca-110">Merhaba arabirimi uygulanmalı `Microsoft.ServiceFabric.Services.Remoting.IService` hizmet hello toosignal remoting arabirimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="2c3ca-111">Remoting dinleyici hizmetinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="2c3ca-112">Bu bir `ICommunicationListener` remoting özellikleri sağlayan uygulama.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="2c3ca-113">Merhaba `Microsoft.ServiceFabric.Services.Remoting.Runtime` ad alanı içeren bir genişletme yöntemi`CreateServiceRemotingListener` durum bilgisiz ve durum bilgisi olan hizmetler için olması kullanılan toocreate remoting dinleyici kullanarak hello varsayılan remoting Aktarım Protokolü.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="2c3ca-114">Not: Merhaba `Remoting` ad alanı adı verilen bir ayrı nuget paketi olarak kullanılabilir`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="2c3ca-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="2c3ca-115">Örneğin, hello aşağıdaki durum bilgisiz hizmeti uzaktan yordam çağrısı üzerinden tek bir yöntem tooget "Hello World" kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="2c3ca-116">Merhaba bağımsız değişkenleri ve hello hello hizmet arabirimi türlerinde basit, karmaşık veya özel türleri olabilir, ancak bunlar .NET hello tarafından Serileştirilebilir olmalıdır dönmek [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c3ca-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="2c3ca-117">Uzak Hizmet yöntemleri çağırma</span><span class="sxs-lookup"><span data-stu-id="2c3ca-117">Call remote service methods</span></span>
<span data-ttu-id="2c3ca-118">Merhaba remoting yığını kullanarak bir hizmet yöntemleri çağırma yapılır hello üzerinden bir yerel ara toohello hizmeti kullanarak `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="2c3ca-119">Merhaba `ServiceProxy` yöntemi, hizmet hello aynı arabirimini uygulayan hello kullanarak yerel bir proxy oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="2c3ca-120">Proxy ile yalnızca yöntemleri hello arabirimde uzaktan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="2c3ca-121">Merhaba remoting framework hello hizmet toohello istemcide oluşturulan özel durumları yayar.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="2c3ca-122">Bu nedenle özel durum işleme mantığı kullanarak hello istemcide `ServiceProxy` doğrudan hizmet atar hello özel durumlar işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="2c3ca-123">Hizmet Proxy ömrü</span><span class="sxs-lookup"><span data-stu-id="2c3ca-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="2c3ca-124">ServiceProxy oluşturma hafif bir işlem olduğundan, kullanıcı ihtiyaç duydukları kadar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="2c3ca-125">Kullanıcı gerek sürece hizmeti proxy'si yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="2c3ca-126">Kullanıcı yeniden kullanabilir hello aynı proxy özel durum durumunda.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="2c3ca-127">Her ServiceProxy hello kablo üzerinden çoğaltmayla kullanılan istemci toosend iletilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="2c3ca-128">Kullanılan iletişim istemcinin geçerli olup olmadığını API istenirken iç onay toosee sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="2c3ca-129">Bu sonuca göre hello iletişimi istemci yeniden oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="2c3ca-130">Bu nedenle kullanıcı gerek kalmaz toorecreate serviceproxy özel durum durumunda.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="2c3ca-131">ServiceProxyFactory yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="2c3ca-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="2c3ca-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) farklı remoting arabirimleri için proxy oluşturan bir üreteci değil.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="2c3ca-133">Proxy oluşturmak için API ServiceProxy.Create kullanırsanız, framework hello singelton ServiceProxyFactory oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="2c3ca-134">Toooverride gerektiğinde yararlı toocreate biri el ile olmasından [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="2c3ca-135">Fabrika pahalı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-135">Factory is an expensive operation.</span></span> <span data-ttu-id="2c3ca-136">ServiceProxyFactory iletişimi istemci önbelleğini korur.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="2c3ca-137">Mümkün olduğunca uzun bir süredir toocache ServiceProxyFactory en iyi uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="2c3ca-138">Remoting özel durum işleme</span><span class="sxs-lookup"><span data-stu-id="2c3ca-138">Remoting Exception Handling</span></span>
<span data-ttu-id="2c3ca-139">Hizmeti API'si tarafından oluşturulan tüm hello Uzak özel durum, geri toohello istemci AggregateException gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="2c3ca-140">RemoteExceptions olmalıdır DataContract seri hale getirilebilir aksi [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) toohello proxy API hello seri hale getirme hatası ile içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="2c3ca-141">ServiceProxy hello hizmet bölüm için oluşturulan tüm yük devretme özel durumu işler.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="2c3ca-142">Merhaba doğru uç noktası ile yük devretme Exceptions(Non-Transient Exceptions) ve yeniden deneme hello çağrı ise hello uç noktaları yeniden çözümler.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="2c3ca-143">Yük devretme özel durumu için yeniden deneme sayısı belirsiz.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="2c3ca-144">TransientExceptions durumunda hello çağrı yalnızca deneme.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="2c3ca-145">[OperationRetrySettings] tarafından sağlanan varsayılan yeniden deneme parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="2c3ca-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Kullanıcı OperationRetrySettings nesne tooServiceProxyFactory Oluşturucusu geçirerek bu değerleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c3ca-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c3ca-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c3ca-147">Next steps</span></span>
* [<span data-ttu-id="2c3ca-148">Web API OWIN güvenilir Hizmetleri'ndeki ile</span><span class="sxs-lookup"><span data-stu-id="2c3ca-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="2c3ca-149">Güvenilir hizmetler ile WCF iletişim</span><span class="sxs-lookup"><span data-stu-id="2c3ca-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="2c3ca-150">Güvenilir hizmetler için iletişimin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="2c3ca-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
