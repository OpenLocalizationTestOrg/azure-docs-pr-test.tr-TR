---
title: "hello Azure olay hub'ları .NET standart API'leri aaaOverview | Microsoft Docs"
description: ".NET standart API genel bakış"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="d3d25-103">Event Hubs .NET standart API genel bakış</span><span class="sxs-lookup"><span data-stu-id="d3d25-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="d3d25-104">Bu makalede hello anahtar olay hub'ları .NET standart istemci API özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d3d25-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="d3d25-105">Şu anda iki .NET standart istemci kitaplıkları vardır:</span><span class="sxs-lookup"><span data-stu-id="d3d25-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="d3d25-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="d3d25-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="d3d25-107">Bu kitaplık tüm temel çalışma zamanı işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3d25-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="d3d25-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="d3d25-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="d3d25-109">Bu kitaplık işlenen olayları izlemek için sağlar ve hello en kolay yolu tooread event hub'ındaki ek işlevsellik ekler.</span><span class="sxs-lookup"><span data-stu-id="d3d25-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="d3d25-110">Olay hub'ları istemci</span><span class="sxs-lookup"><span data-stu-id="d3d25-110">Event Hubs client</span></span>
<span data-ttu-id="d3d25-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) olan hello toosend olayları, kullandığınız birincil nesnesi oluşturmak alıcıları ve tooget çalışma zamanı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d3d25-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="d3d25-112">Bu istemci bağlantılı tooa belirli bir olay hub'ı ve yeni bir bağlantı toohello olay hub'ları uç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d3d25-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="d3d25-113">Event Hubs istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3d25-113">Create an Event Hubs client</span></span>
<span data-ttu-id="d3d25-114">Bir [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) nesnesi, bir bağlantı dizesinden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d3d25-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="d3d25-115">Merhaba en basit yolu tooinstantiate yeni bir istemci aşağıdaki örneğine hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="d3d25-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="d3d25-116">tooprogrammatically düzenleme hello bağlantı dizesi, hello kullanabilirsiniz [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) sınıfı ve hello bağlantı dizesi çok parametre olarak geçirmek[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="d3d25-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="d3d25-117">Olayları gönderme</span><span class="sxs-lookup"><span data-stu-id="d3d25-117">Send events</span></span>
<span data-ttu-id="d3d25-118">toosend olayları tooan olay hub'ı kullan hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d3d25-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="d3d25-119">Merhaba gövde olmalıdır bir `byte` diziye veya `byte` dizi kesimi.</span><span class="sxs-lookup"><span data-stu-id="d3d25-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="d3d25-120">Olayları alma</span><span class="sxs-lookup"><span data-stu-id="d3d25-120">Receive events</span></span>
<span data-ttu-id="d3d25-121">Olay hub'larından yolu tooreceive olayları önerilen hello hello kullanarak [olay işleyicisi konağı](#event-processor-host-apis), işlevselliği tooautomatically sağlayan uzaklığı izlemek ve bölüm bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d3d25-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="d3d25-122">Ancak, toouse hello hello çekirdek olay hub'ları kitaplığı tooreceive olaylarını esnekliğini isteyebilirsiniz bazı durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="d3d25-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="d3d25-123">Alıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d3d25-123">Create a receiver</span></span>
<span data-ttu-id="d3d25-124">Alıcıları bağlı toospecific bölümlerdir, bu nedenle, tooreceive tüm olayları bir event hub'ında sipariş, birden çok örneği toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3d25-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="d3d25-125">Genel olarak bakıldığında, onu bir iyi bir uygulama tooget hello bölüm programlı şekilde, hello bölüm kimlikleri sabit kodlama yerine bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="d3d25-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="d3d25-126">Bunu toodo sipariş, hello kullanabilirsiniz [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d3d25-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="d3d25-127">Olayları bir event hub'ından hiçbir zaman kaldırılır (ve yalnızca sona olduğundan), toospecify hello uygun başlangıç noktası gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3d25-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="d3d25-128">Merhaba aşağıdaki örnek olası birleşimlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d3d25-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="d3d25-129">Bir olay kullanma</span><span class="sxs-lookup"><span data-stu-id="d3d25-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="d3d25-130">Olay işlemcisi konağı API'leri</span><span class="sxs-lookup"><span data-stu-id="d3d25-130">Event Processor Host APIs</span></span>
<span data-ttu-id="d3d25-131">Bu API'leri kullanılabilir çalışanları bölüm dağıtarak, kullanılamayabilir dayanıklılık tooworker işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d3d25-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="d3d25-132">Merhaba aşağıda bir örnek hello uygulamasıdır [Ieventprocessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="d3d25-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d3d25-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d3d25-133">Next steps</span></span>
<span data-ttu-id="d3d25-134">Event Hubs senaryoları hakkında daha fazla toolearn bu bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="d3d25-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="d3d25-135">Azure Event Hubs nedir?</span><span class="sxs-lookup"><span data-stu-id="d3d25-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="d3d25-136">Kullanılabilir olay hub'ları API'leri</span><span class="sxs-lookup"><span data-stu-id="d3d25-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="d3d25-137">Merhaba .NET API başvuru şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d3d25-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="d3d25-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="d3d25-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="d3d25-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="d3d25-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)