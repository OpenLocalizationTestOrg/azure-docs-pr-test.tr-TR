---
title: "aaaReliable Hizmetleri WCF iletişim yığını | Microsoft Docs"
description: "Merhaba yerleşik WCF iletişim yığını Service Fabric güvenilir hizmetler için İstemci-hizmet WCF iletişimi sağlar."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a>Güvenilir hizmetler için WCF tabanlı iletişim yığını
Merhaba güvenilir framework sağlar Services hizmet yazarlar toochoose hello iletişim yığını toouse için kendi hizmet istiyor. Merhaba iletişimi yığınında hello aracılığıyla kendi seçtikleri ekleyebilirsiniz **ICommunicationListener** hello döndürülen [CreateServiceReplicaListeners veya CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) yöntemleri. Merhaba framework hello iletişimi yığınının hello Windows Communication Foundation (WCF) üzerinde toouse WCF tabanlı iletişim isteyen hizmeti yazarlar için temel bir uygulama sağlar.

## <a name="wcf-communication-listener"></a>WCF iletişimi dinleyicisi
Merhaba WCF özgü uyarlamasını **ICommunicationListener** hello tarafından sağlanan **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** sınıfı.

Bir hizmet sözleşmesini türü deyin sahibiz ekleyin`ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

Aşağıdaki şekilde hello hizmet hello WCF iletişimi dinleyici oluşturabiliriz.

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>İstemciler hello WCF iletişim yığını için yazma
WCF, hello framework kullanarak hizmetleriyle toocommunicate sağlar istemcileri yazma **WcfClientCommunicationFactory**, hello WCF özgü uyarlamasını olduğu [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

Merhaba WCF iletişim kanalını hello erişilebilir **WcfCommunicationClient** hello tarafından oluşturulan **WcfCommunicationClientFactory**.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

İstemci kodu hello kullanabileceğiniz **WcfCommunicationClientFactory** hello birlikte **WcfCommunicationClient** hangi uygulayan **ServicePartitionClient** toodetermine Hizmet uç noktası hello ve hello hizmetiyle iletişim.

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> Merhaba varsayılan ServicePartitionResolver hello istemci aynı küme hello hizmet olarak çalışıyor varsayar. Diğer bir deyişle değil hello durumlarda bir ServicePartitionResolver nesnesi oluşturma ve hello küme bağlantı uç geçirin.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* [Güvenilir hizmetler remoting ile uzaktan yordam çağrısı](service-fabric-reliable-services-communication-remoting.md)
* [Web API OWIN güvenilir Hizmetleri'ndeki ile](service-fabric-reliable-services-communication-webapi.md)
* [Güvenilir hizmetler için iletişimin güvenliğini sağlama](service-fabric-reliable-services-secure-communication.md)

