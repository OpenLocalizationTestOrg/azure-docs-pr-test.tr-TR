---
title: ".NET Framework API'ları Azure Event Hubs'a genel bakış | Microsoft Docs"
description: "Bazı temel olay hub'ları .NET Framework istemci API özeti."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bc525e7ca8b21e9e5f1e36b3152d71420b041700
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="2237c-103">Event Hubs .NET Framework API genel bakış</span><span class="sxs-lookup"><span data-stu-id="2237c-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="2237c-104">Bu makalede olay hub'ları .NET Framework istemci API anahtarı özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="2237c-104">This article summarizes some of the key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="2237c-105">İki kategorisi vardır: Yönetim ve çalıştırma API'leri.</span><span class="sxs-lookup"><span data-stu-id="2237c-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="2237c-106">Çalışma zamanı API'leri bir ileti alıp göndermek için gereken tüm işlemler oluşur.</span><span class="sxs-lookup"><span data-stu-id="2237c-106">Run-time APIs consist of all operations needed to send and receive a message.</span></span> <span data-ttu-id="2237c-107">Yönetim işlemlerini bir olay hub'ları varlık durumu oluşturma, güncelleştirme ve silme varlıklar olarak yönetmek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2237c-107">Management operations enable you to manage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="2237c-108">İzleme senaryoları, yönetim ve çalışma zamanı span.</span><span class="sxs-lookup"><span data-stu-id="2237c-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="2237c-109">.NET API'ları üzerinde ayrıntılı başvuru belgeleri için bkz: [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) ve [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) başvuruları.</span><span class="sxs-lookup"><span data-stu-id="2237c-109">For detailed reference documentation on the .NET APIs, see the [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="2237c-110">Yönetim API'leri</span><span class="sxs-lookup"><span data-stu-id="2237c-110">Management APIs</span></span>
<span data-ttu-id="2237c-111">Aşağıdaki yönetim işlemlerini gerçekleştirmek için olmalıdır **Yönet** olay hub'ları ad alanı izinleri:</span><span class="sxs-lookup"><span data-stu-id="2237c-111">To perform the following management operations, you must have **Manage** permissions on the Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="2237c-112">Oluştur</span><span class="sxs-lookup"><span data-stu-id="2237c-112">Create</span></span>
```csharp
// Create the event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="2237c-113">Güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2237c-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="2237c-114">Sil</span><span class="sxs-lookup"><span data-stu-id="2237c-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="2237c-115">Çalışma zamanı API'leri</span><span class="sxs-lookup"><span data-stu-id="2237c-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="2237c-116">Yayımcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2237c-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="2237c-117">İleti yayımlama</span><span class="sxs-lookup"><span data-stu-id="2237c-117">Publish message</span></span>
```csharp
// Create the device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="2237c-118">Tüketici oluşturma</span><span class="sxs-lookup"><span data-stu-id="2237c-118">Create consumer</span></span>
```csharp
// Create the Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get the default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="2237c-119">İleti kullanma</span><span class="sxs-lookup"><span data-stu-id="2237c-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="2237c-120">Olay işlemcisi konağı API'leri</span><span class="sxs-lookup"><span data-stu-id="2237c-120">Event Processor Host APIs</span></span>
<span data-ttu-id="2237c-121">Bu API'leri kullanılabilir çalışanları bölüm dağıtarak, kullanılamayabilir çalışan işlemleri için esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="2237c-121">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use the EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// To close
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="2237c-122">[Ieventprocessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) arabirimi şu şekilde tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="2237c-122">The [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2237c-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2237c-123">Next steps</span></span>
<span data-ttu-id="2237c-124">Event Hubs senaryoları hakkında daha fazla bilgi almak için aşağıdaki bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="2237c-124">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="2237c-125">Azure Event Hubs nedir?</span><span class="sxs-lookup"><span data-stu-id="2237c-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2237c-126">Event Hubs programlama kılavuzu</span><span class="sxs-lookup"><span data-stu-id="2237c-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="2237c-127">.NET API başvuru şunlardır:</span><span class="sxs-lookup"><span data-stu-id="2237c-127">The .NET API references are here:</span></span>

* [<span data-ttu-id="2237c-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="2237c-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="2237c-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="2237c-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
