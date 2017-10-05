---
title: "Service Fabric hizmeti uzaktan çalışma | Microsoft Docs"
description: "Service Fabric uzak istemciler ve hizmetler uzaktan yordam çağrısı kullanarak Hizmetleri ile iletişim kurmasına olanak sağlar."
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
# <a name="service-remoting-with-reliable-services"></a>Güvenilir hizmetler ile hizmet uzaktan iletişim
Belirli bir iletişim protokolü veya Webapı, Windows Communication Foundation (WCF) veya diğerleri gibi yığın bağlanmayan Hizmetleri için uzak yordam çağrısı için hızlı ve kolay bir şekilde ayarlamak için uzaktan iletişim mekanizması Reliable Services çerçevesi sağlar Hizmetler.

## <a name="set-up-remoting-on-a-service"></a>Bir hizmeti uzaktan iletişim ayarlama
Bir hizmet için uzaktan iletişim kurma iki basit adımda gerçekleştirilir:

1. Hizmetinizin uygulamak bir arabirim oluşturun. Bu arabirim, hizmeti uzaktan yordam çağrısı için kullanılabilecek yöntemleri tanımlar. Görev döndüren yöntemler olmalıdır zaman uyumsuz yöntemleri. Arabirimi uygulamalıdır `Microsoft.ServiceFabric.Services.Remoting.IService` hizmet remoting arabirimi olduğunu göstermek için.
2. Remoting dinleyici hizmetinizi kullanın. Bu bir `ICommunicationListener` remoting özellikleri sağlayan uygulama. `Microsoft.ServiceFabric.Services.Remoting.Runtime` Ad alanı içeren bir genişletme yöntemi`CreateServiceRemotingListener` varsayılan remoting aktarım protokolünü kullanarak bir uzak dinleyicisi oluşturmak için kullanılan durum bilgisiz ve durum bilgisi olan hizmetler için.

Not: `Remoting` ad alanı adı verilen bir ayrı nuget paketi olarak kullanılabilir`Microsoft.ServiceFabric.Services.Remoting` 

Örneğin, aşağıdaki durum bilgisiz hizmeti üzerinden bir uzak yordam çağrısı "Hello World" almak için tek bir yöntemi gösterir.

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
> Bağımsız değişkenler ve hizmet arabirimi dönüş türler basit, karmaşık veya özel türleri olabilir, ancak .NET tarafından Serileştirilebilir olmalıdır [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Uzak Hizmet yöntemleri çağırma
Uzaktan iletişim yığını kullanarak bir hizmet yöntemleri çağırma yapılır yerel bir proxy üzerinden hizmete kullanarak `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` sınıfı. `ServiceProxy` Yöntemi hizmeti uygulayan aynı arabirimini kullanarak yerel bir proxy oluşturur. Proxy ile yalnızca yöntemleri arabirimde uzaktan çağırabilirsiniz.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

Remoting framework istemciye hizmet sırasında oluşturulan özel durumları yayar. Bu nedenle özel durum işleme mantığı kullanarak istemcide `ServiceProxy` doğrudan hizmet oluşturur özel durumlar işleyebilir.

## <a name="service-proxy-lifetime"></a>Hizmet Proxy ömrü
ServiceProxy oluşturma hafif bir işlem olduğundan, kullanıcı ihtiyaç duydukları kadar oluşturabilirsiniz. Kullanıcı gerek sürece hizmeti proxy'si yeniden kullanılabilir. Kullanıcı aynı proxy özel durum durumunda yeniden kullanabilirsiniz. Her ServiceProxy kablo üzerinden ileti göndermek için kullanılan çoğaltmayla istemci içerir. API istenirken kullanılan iletişim istemci geçerli olup olmadığını görmek için iç onay sunuyoruz. Bu sonuca bağlı olarak, iletişim istemci yeniden oluşturuyoruz. Bu nedenle kullanıcı gerekmez serviceproxy özel durum durumunda yeniden oluşturun.

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory yaşam süresi
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) farklı remoting arabirimleri için proxy oluşturan bir üreteci değil. Proxy oluşturmak için API ServiceProxy.Create kullanırsanız, framework ServiceProxyFactory singelton oluşturur.
Geçersiz kılmak gerektiğinde el ile oluşturmak kullanışlıdır [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) özellikleri.
Fabrika pahalı bir işlemdir. ServiceProxyFactory iletişimi istemci önbelleğini korur.
Mümkün olduğunca uzun bir süredir ServiceProxyFactory önbelleğe en iyi uygulamadır.

## <a name="remoting-exception-handling"></a>Remoting özel durum işleme
Hizmeti API'si tarafından oluşturulan tüm uzak özel durum, istemciye AggregateException gönderilir. RemoteExceptions olmalıdır DataContract seri hale getirilebilir aksi [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) proxy API, seri hale getirme hatası ile oluşturulur.

ServiceProxy için oluşturulan hizmet bölümü için tüm yük devretme özel durumu işler. Yük devretme Exceptions(Non-Transient Exceptions) ise uç noktaları yeniden çözümlediği ve doğru uç nokta çağrısıyla yeniden dener. Yük devretme özel durumu için yeniden deneme sayısı belirsiz.
TransientExceptions durumunda çağrı yalnızca deneme.

[OperationRetrySettings] tarafından sağlanan varsayılan yeniden deneme parametreleridir. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Kullanıcı OperationRetrySettings ServiceProxyFactory oluşturucusuna geçirerek bu değerleri yapılandırabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* [Web API OWIN güvenilir Hizmetleri'ndeki ile](service-fabric-reliable-services-communication-webapi.md)
* [Güvenilir hizmetler ile WCF iletişim](service-fabric-reliable-services-communication-wcf.md)
* [Güvenilir hizmetler için iletişimin güvenliğini sağlama](service-fabric-reliable-services-secure-communication.md)
