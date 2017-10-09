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
# <a name="service-remoting-with-reliable-services"></a>Güvenilir hizmetler ile hizmet uzaktan iletişim
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-services-communication-remoting.md)
> * [Linux üzerinde Java](service-fabric-reliable-services-communication-remoting-java.md)
>
>

Merhaba Reliable Services framework uzaktan iletişim mekanizması tooquickly sağlar ve uzak yordam çağrısı Hizmetleri için kolayca ayarlayın.

## <a name="set-up-remoting-on-a-service"></a>Bir hizmeti uzaktan iletişim ayarlama
Bir hizmet için uzaktan iletişim kurma iki basit adımda gerçekleştirilir:

1. Hizmet tooimplement için bir arabirimi oluşturun. Bu arabirim, hizmeti uzaktan yordam çağrısı için kullanılabilen hello yöntemleri tanımlar. Merhaba yöntemleri görev döndürme olmalıdır zaman uyumsuz yöntemleri. Merhaba arabirimi uygulanmalı `microsoft.serviceFabric.services.remoting.Service` hizmet hello toosignal remoting arabirimine sahiptir.
2. Remoting dinleyici hizmetinizi kullanın. Bu bir `CommunicationListener` remoting özellikleri sağlayan uygulama. `FabricTransportServiceRemotingListener`kullanılan toocreate hello varsayılan remoting aktarım protokolünü kullanarak bir uzak dinleyicisi olabilir.

Örneğin, hello aşağıdaki durum bilgisiz hizmeti uzaktan yordam çağrısı üzerinden tek bir yöntem tooget "Hello World" kullanıma sunar.

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
> Merhaba bağımsız değişkenler ve hello hello hizmet arabirimi türlerinde basit, karmaşık veya özel türleri olabilir, ancak bunlar Serileştirilebilir olmalıdır döndürür.
>
>

## <a name="call-remote-service-methods"></a>Uzak Hizmet yöntemleri çağırma
Merhaba remoting yığını kullanarak bir hizmet yöntemleri çağırma yapılır hello üzerinden bir yerel ara toohello hizmeti kullanarak `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` sınıfı. Merhaba `ServiceProxyBase` yöntemi, hizmet hello aynı arabirimini uygulayan hello kullanarak yerel bir proxy oluşturur. Proxy ile yalnızca yöntemleri hello arabirimde uzaktan çağırabilirsiniz.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

Merhaba remoting framework hello hizmet toohello istemcide oluşturulan özel durumları yayar. Bu nedenle özel durum işleme mantığı kullanarak hello istemcide `ServiceProxyBase` doğrudan hizmet atar hello özel durumlar işleyebilir.

## <a name="service-proxy-lifetime"></a>Hizmet Proxy ömrü
ServiceProxy oluşturma hafif bir işlem olduğundan, kullanıcı ihtiyaç duydukları kadar oluşturabilirsiniz. Kullanıcı gerek sürece hizmeti proxy'si yeniden kullanılabilir. Kullanıcı yeniden kullanabilir hello aynı proxy özel durum durumunda. Her ServiceProxy hello kablo üzerinden iletişimi kullanılan istemci toosend iletilerini içerir. Kullanılan iletişim istemcinin geçerli olup olmadığını API istenirken iç onay toosee sunuyoruz. Bu sonuca göre hello iletişimi istemci yeniden oluşturuyoruz. Bu nedenle kullanıcı gerek kalmaz toorecreate serviceproxy özel durum durumunda.

### <a name="serviceproxyfactory-lifetime"></a>ServiceProxyFactory yaşam süresi
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) farklı remoting arabirimleri için proxy oluşturan bir üreteci değil. API kullanırsanız `ServiceProxyBase.create` proxy oluşturmak, ardından framework oluşturan bir `FabricServiceProxyFactory`.
Toooverride gerektiğinde yararlı toocreate biri el ile olmasından [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) özellikleri.
Fabrika pahalı bir işlemdir. `FabricServiceProxyFactory`iletişim istemci önbelleğini korur.
En iyi uygulamadır toocache `FabricServiceProxyFactory` mümkün olduğunca uzun bir süredir.

## <a name="remoting-exception-handling"></a>Remoting özel durum işleme
Hizmeti API'si tarafından tüm hello uzak durum gönderilen geri toohello istemci RuntimeException veya FabricException olarak.

ServiceProxy hello hizmet bölüm için oluşturulan tüm yük devretme özel durumu işler. Merhaba doğru uç noktası ile yük devretme Exceptions(Non-Transient Exceptions) ve yeniden deneme hello çağrı ise hello uç noktaları yeniden çözümler. Yük devretme özel durumu için yeniden deneme sayısı belirsiz.
TransientExceptions durumunda hello çağrı yalnızca deneme.

[OperationRetrySettings] tarafından sağlanan varsayılan yeniden deneme parametreleridir. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Kullanıcı OperationRetrySettings nesne tooServiceProxyFactory Oluşturucusu geçirerek bu değerleri yapılandırabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
* [Güvenilir hizmetler için iletişimin güvenliğini sağlama](service-fabric-reliable-services-secure-communication.md)
