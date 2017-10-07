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
# <a name="event-hubs-net-standard-api-overview"></a>Event Hubs .NET standart API genel bakış
Bu makalede hello anahtar olay hub'ları .NET standart istemci API özetlenmektedir. Şu anda iki .NET standart istemci kitaplıkları vardır:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Bu kitaplık tüm temel çalışma zamanı işlemler sağlar.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Bu kitaplık işlenen olayları izlemek için sağlar ve hello en kolay yolu tooread event hub'ındaki ek işlevsellik ekler.

## <a name="event-hubs-client"></a>Olay hub'ları istemci
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) olan hello toosend olayları, kullandığınız birincil nesnesi oluşturmak alıcıları ve tooget çalışma zamanı bilgileri. Bu istemci bağlantılı tooa belirli bir olay hub'ı ve yeni bir bağlantı toohello olay hub'ları uç noktası oluşturur.

### <a name="create-an-event-hubs-client"></a>Event Hubs istemcisi oluşturma
Bir [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) nesnesi, bir bağlantı dizesinden oluşturulur. Merhaba en basit yolu tooinstantiate yeni bir istemci aşağıdaki örneğine hello gösterilir:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically düzenleme hello bağlantı dizesi, hello kullanabilirsiniz [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) sınıfı ve hello bağlantı dizesi çok parametre olarak geçirmek[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Olayları gönderme
toosend olayları tooan olay hub'ı kullan hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) sınıfı. Merhaba gövde olmalıdır bir `byte` diziye veya `byte` dizi kesimi.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Olayları alma
Olay hub'larından yolu tooreceive olayları önerilen hello hello kullanarak [olay işleyicisi konağı](#event-processor-host-apis), işlevselliği tooautomatically sağlayan uzaklığı izlemek ve bölüm bilgileri. Ancak, toouse hello hello çekirdek olay hub'ları kitaplığı tooreceive olaylarını esnekliğini isteyebilirsiniz bazı durumlar vardır.

#### <a name="create-a-receiver"></a>Alıcı oluşturma
Alıcıları bağlı toospecific bölümlerdir, bu nedenle, tooreceive tüm olayları bir event hub'ında sipariş, birden çok örneği toocreate gerekir. Genel olarak bakıldığında, onu bir iyi bir uygulama tooget hello bölüm programlı şekilde, hello bölüm kimlikleri sabit kodlama yerine bilgilerdir. Bunu toodo sipariş, hello kullanabilirsiniz [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) yöntemi.

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

Olayları bir event hub'ından hiçbir zaman kaldırılır (ve yalnızca sona olduğundan), toospecify hello uygun başlangıç noktası gerekir. Merhaba aşağıdaki örnek olası birleşimlerini gösterir.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Bir olay kullanma
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

## <a name="event-processor-host-apis"></a>Olay işlemcisi konağı API'leri
Bu API'leri kullanılabilir çalışanları bölüm dağıtarak, kullanılamayabilir dayanıklılık tooworker işlemler sağlar.

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

Merhaba aşağıda bir örnek hello uygulamasıdır [Ieventprocessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Sonraki adımlar
Event Hubs senaryoları hakkında daha fazla toolearn bu bağlantıları ziyaret edin:

* [Azure Event Hubs nedir?](event-hubs-what-is-event-hubs.md)
* [Kullanılabilir olay hub'ları API'leri](event-hubs-api-overview.md)

Merhaba .NET API başvuru şunlardır:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)