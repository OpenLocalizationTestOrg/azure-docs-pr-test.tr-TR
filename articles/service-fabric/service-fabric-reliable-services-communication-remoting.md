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
# <a name="service-remoting-with-reliable-services"></a>Güvenilir hizmetler ile hizmet uzaktan iletişim
Tooa belirli iletişim protokolü veya Webapı, Windows Communication Foundation (WCF) veya diğerleri gibi yığını bulunmayan hizmet bağlı hello Reliable Services framework uzaktan iletişim mekanizması tooquickly sağlar ve uzak yordam çağrısı kolayca ayarlayın Hizmetler için.

## <a name="set-up-remoting-on-a-service"></a>Bir hizmeti uzaktan iletişim ayarlama
Bir hizmet için uzaktan iletişim kurma iki basit adımda gerçekleştirilir:

1. Hizmet tooimplement için bir arabirimi oluşturun. Bu arabirim, hizmeti uzaktan yordam çağrısı için kullanılabilecek hello yöntemleri tanımlar. Merhaba yöntemleri görev döndürme olmalıdır zaman uyumsuz yöntemleri. Merhaba arabirimi uygulanmalı `Microsoft.ServiceFabric.Services.Remoting.IService` hizmet hello toosignal remoting arabirimine sahiptir.
2. Remoting dinleyici hizmetinizi kullanın. Bu bir `ICommunicationListener` remoting özellikleri sağlayan uygulama. Merhaba `Microsoft.ServiceFabric.Services.Remoting.Runtime` ad alanı içeren bir genişletme yöntemi`CreateServiceRemotingListener` durum bilgisiz ve durum bilgisi olan hizmetler için olması kullanılan toocreate remoting dinleyici kullanarak hello varsayılan remoting Aktarım Protokolü.

Not: Merhaba `Remoting` ad alanı adı verilen bir ayrı nuget paketi olarak kullanılabilir`Microsoft.ServiceFabric.Services.Remoting` 

Örneğin, hello aşağıdaki durum bilgisiz hizmeti uzaktan yordam çağrısı üzerinden tek bir yöntem tooget "Hello World" kullanıma sunar.

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
> Merhaba bağımsız değişkenleri ve hello hello hizmet arabirimi türlerinde basit, karmaşık veya özel türleri olabilir, ancak bunlar .NET hello tarafından Serileştirilebilir olmalıdır dönmek [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Uzak Hizmet yöntemleri çağırma
Merhaba remoting yığını kullanarak bir hizmet yöntemleri çağırma yapılır hello üzerinden bir yerel ara toohello hizmeti kullanarak `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` sınıfı. Merhaba `ServiceProxy` yöntemi, hizmet hello aynı arabirimini uygulayan hello kullanarak yerel bir proxy oluşturur. Proxy ile yalnızca yöntemleri hello arabirimde uzaktan çağırabilirsiniz.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

Merhaba remoting framework hello hizmet toohello istemcide oluşturulan özel durumları yayar. Bu nedenle özel durum işleme mantığı kullanarak hello istemcide `ServiceProxy` doğrudan hizmet atar hello özel durumlar işleyebilir.

## <a name="service-proxy-lifetime"></a>Hizmet Proxy ömrü
ServiceProxy oluşturma hafif bir işlem olduğundan, kullanıcı ihtiyaç duydukları kadar oluşturabilirsiniz. Kullanıcı gerek sürece hizmeti proxy'si yeniden kullanılabilir. Kullanıcı yeniden kullanabilir hello aynı proxy özel durum durumunda. Her ServiceProxy hello kablo üzerinden çoğaltmayla kullanılan istemci toosend iletilerini içerir. Kullanılan iletişim istemcinin geçerli olup olmadığını API istenirken iç onay toosee sunuyoruz. Bu sonuca göre hello iletişimi istemci yeniden oluşturuyoruz. Bu nedenle kullanıcı gerek kalmaz toorecreate serviceproxy özel durum durumunda.

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory yaşam süresi
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) farklı remoting arabirimleri için proxy oluşturan bir üreteci değil. Proxy oluşturmak için API ServiceProxy.Create kullanırsanız, framework hello singelton ServiceProxyFactory oluşturur.
Toooverride gerektiğinde yararlı toocreate biri el ile olmasından [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) özellikleri.
Fabrika pahalı bir işlemdir. ServiceProxyFactory iletişimi istemci önbelleğini korur.
Mümkün olduğunca uzun bir süredir toocache ServiceProxyFactory en iyi uygulamadır.

## <a name="remoting-exception-handling"></a>Remoting özel durum işleme
Hizmeti API'si tarafından oluşturulan tüm hello Uzak özel durum, geri toohello istemci AggregateException gönderilir. RemoteExceptions olmalıdır DataContract seri hale getirilebilir aksi [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) toohello proxy API hello seri hale getirme hatası ile içinde oluşturulur.

ServiceProxy hello hizmet bölüm için oluşturulan tüm yük devretme özel durumu işler. Merhaba doğru uç noktası ile yük devretme Exceptions(Non-Transient Exceptions) ve yeniden deneme hello çağrı ise hello uç noktaları yeniden çözümler. Yük devretme özel durumu için yeniden deneme sayısı belirsiz.
TransientExceptions durumunda hello çağrı yalnızca deneme.

[OperationRetrySettings] tarafından sağlanan varsayılan yeniden deneme parametreleridir. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Kullanıcı OperationRetrySettings nesne tooServiceProxyFactory Oluşturucusu geçirerek bu değerleri yapılandırabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* [Web API OWIN güvenilir Hizmetleri'ndeki ile](service-fabric-reliable-services-communication-webapi.md)
* [Güvenilir hizmetler ile WCF iletişim](service-fabric-reliable-services-communication-wcf.md)
* [Güvenilir hizmetler için iletişimin güvenliğini sağlama](service-fabric-reliable-services-secure-communication.md)
