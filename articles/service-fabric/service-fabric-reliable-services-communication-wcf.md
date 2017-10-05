---
title: "Güvenilir hizmetler WCF iletişim yığını | Microsoft Docs"
description: "Service Fabric yerleşik WCF iletişimi yığınında güvenilir hizmetler için İstemci-hizmet WCF iletişimi sağlar."
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
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="e6f32-103">Güvenilir hizmetler için WCF tabanlı iletişim yığını</span><span class="sxs-lookup"><span data-stu-id="e6f32-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="e6f32-104">Güvenilir hizmetler altyapısına hizmet yazarların kendi hizmet için kullanmak istedikleri iletişim yığını seçin izin verir.</span><span class="sxs-lookup"><span data-stu-id="e6f32-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="e6f32-105">Kendi seçtikleri iletişim yığınındaki ekleyebilirsiniz **ICommunicationListener** döndürülen [CreateServiceReplicaListeners veya CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="e6f32-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="e6f32-106">Çerçeve WCF tabanlı iletişim kullanmak istediğiniz hizmet yazarlar için Windows Communication Foundation (WCF) tabanlı iletişim yığını uygulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6f32-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="e6f32-107">WCF iletişimi dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="e6f32-107">WCF Communication Listener</span></span>
<span data-ttu-id="e6f32-108">WCF özel uyarlamasını **ICommunicationListener** tarafından sağlanan **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e6f32-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="e6f32-109">Bir hizmet sözleşmesini türü deyin sahibiz ekleyin`ICalculator`</span><span class="sxs-lookup"><span data-stu-id="e6f32-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="e6f32-110">Aşağıdaki şekilde hizmetinde bir WCF iletişimi dinleyici oluşturabiliriz.</span><span class="sxs-lookup"><span data-stu-id="e6f32-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="e6f32-111">İstemciler için WCF iletişim yığını yazma</span><span class="sxs-lookup"><span data-stu-id="e6f32-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="e6f32-112">WCF kullanarak Hizmetleri ile iletişim kurmak için istemcileri yazmak için bir çerçeve sağlar **WcfClientCommunicationFactory**, WCF özgü uyarlamasını olduğu [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="e6f32-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="e6f32-113">WCF iletişim kanalını erişilebilen **WcfCommunicationClient** tarafından oluşturulan **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="e6f32-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="e6f32-114">İstemci kodu kullanabileceğiniz **WcfCommunicationClientFactory** ile birlikte **WcfCommunicationClient** hangi uygulayan **ServicePartitionClient** hizmet uç noktası belirlemek ve hizmeti ile iletişim için.</span><span class="sxs-lookup"><span data-stu-id="e6f32-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="e6f32-115">ServicePartitionResolver varsayılan istemci hizmeti olarak aynı kümedeki çalıştığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="e6f32-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="e6f32-116">Diğer bir deyişle Aksi halde, bir ServicePartitionResolver nesnesi oluşturur ve küme bağlantı uç noktalardan geçirin.</span><span class="sxs-lookup"><span data-stu-id="e6f32-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e6f32-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6f32-117">Next steps</span></span>
* [<span data-ttu-id="e6f32-118">Güvenilir hizmetler remoting ile uzaktan yordam çağrısı</span><span class="sxs-lookup"><span data-stu-id="e6f32-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="e6f32-119">Web API OWIN güvenilir Hizmetleri'ndeki ile</span><span class="sxs-lookup"><span data-stu-id="e6f32-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="e6f32-120">Güvenilir hizmetler için iletişimin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="e6f32-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

