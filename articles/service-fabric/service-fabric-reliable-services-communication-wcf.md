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
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="5766d-103">Güvenilir hizmetler için WCF tabanlı iletişim yığını</span><span class="sxs-lookup"><span data-stu-id="5766d-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="5766d-104">Merhaba güvenilir framework sağlar Services hizmet yazarlar toochoose hello iletişim yığını toouse için kendi hizmet istiyor.</span><span class="sxs-lookup"><span data-stu-id="5766d-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="5766d-105">Merhaba iletişimi yığınında hello aracılığıyla kendi seçtikleri ekleyebilirsiniz **ICommunicationListener** hello döndürülen [CreateServiceReplicaListeners veya CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="5766d-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="5766d-106">Merhaba framework hello iletişimi yığınının hello Windows Communication Foundation (WCF) üzerinde toouse WCF tabanlı iletişim isteyen hizmeti yazarlar için temel bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="5766d-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="5766d-107">WCF iletişimi dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="5766d-107">WCF Communication Listener</span></span>
<span data-ttu-id="5766d-108">Merhaba WCF özgü uyarlamasını **ICommunicationListener** hello tarafından sağlanan **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5766d-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="5766d-109">Bir hizmet sözleşmesini türü deyin sahibiz ekleyin`ICalculator`</span><span class="sxs-lookup"><span data-stu-id="5766d-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="5766d-110">Aşağıdaki şekilde hello hizmet hello WCF iletişimi dinleyici oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="5766d-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="5766d-111">İstemciler hello WCF iletişim yığını için yazma</span><span class="sxs-lookup"><span data-stu-id="5766d-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="5766d-112">WCF, hello framework kullanarak hizmetleriyle toocommunicate sağlar istemcileri yazma **WcfClientCommunicationFactory**, hello WCF özgü uyarlamasını olduğu [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="5766d-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="5766d-113">Merhaba WCF iletişim kanalını hello erişilebilir **WcfCommunicationClient** hello tarafından oluşturulan **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="5766d-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="5766d-114">İstemci kodu hello kullanabileceğiniz **WcfCommunicationClientFactory** hello birlikte **WcfCommunicationClient** hangi uygulayan **ServicePartitionClient** toodetermine Hizmet uç noktası hello ve hello hizmetiyle iletişim.</span><span class="sxs-lookup"><span data-stu-id="5766d-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

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
> <span data-ttu-id="5766d-115">Merhaba varsayılan ServicePartitionResolver hello istemci aynı küme hello hizmet olarak çalışıyor varsayar.</span><span class="sxs-lookup"><span data-stu-id="5766d-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="5766d-116">Diğer bir deyişle değil hello durumlarda bir ServicePartitionResolver nesnesi oluşturma ve hello küme bağlantı uç geçirin.</span><span class="sxs-lookup"><span data-stu-id="5766d-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="5766d-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5766d-117">Next steps</span></span>
* [<span data-ttu-id="5766d-118">Güvenilir hizmetler remoting ile uzaktan yordam çağrısı</span><span class="sxs-lookup"><span data-stu-id="5766d-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="5766d-119">Web API OWIN güvenilir Hizmetleri'ndeki ile</span><span class="sxs-lookup"><span data-stu-id="5766d-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="5766d-120">Güvenilir hizmetler için iletişimin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="5766d-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

