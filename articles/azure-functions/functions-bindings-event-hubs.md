---
title: "Azure işlevleri olay hub'ları bağlamaları | Microsoft Docs"
description: "Azure Event Hubs bağlamaları Azure işlevlerini kullanmak nasıl anlayın."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: 19021bef8b7156b3049f43b0275c0ed0c6b22514
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="b0465-104">Azure işlevleri olay hub'ları bağlamaları</span><span class="sxs-lookup"><span data-stu-id="b0465-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b0465-105">Bu makalede, yapılandırmak ve kullanmak açıklanmaktadır [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) Azure işlevleri için bağlamaları.</span><span class="sxs-lookup"><span data-stu-id="b0465-105">This article explains how to configure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="b0465-106">Tetikler ve olay hub'ları için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="b0465-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="b0465-107">Azure Event Hubs'a yeni istiyorsanız bkz [Event Hubs'a genel bakış](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="b0465-107">If you are new to Azure Event Hubs, see the [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="b0465-108">Olay hub'ı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="b0465-108">Event hub trigger</span></span>
<span data-ttu-id="b0465-109">Bir olay hub'ı olay akışı gönderilen bir olayın yanıtlamak için olay hub'ları tetikleyici kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0465-109">Use the Event Hubs trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="b0465-110">Olay hub'ına tetikleyecek için okuma erişimi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0465-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="b0465-111">Olay hub'ları işlevi tetikleyici aşağıdaki JSON nesnesinde kullanan `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b0465-111">The Event Hubs function trigger uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="b0465-112">`consumerGroup`ayarlamak için kullanılan isteğe bağlı bir özellik [tüketici grubu](../event-hubs/event-hubs-features.md#event-consumers) hub olaylara abone olmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0465-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="b0465-113">Atlanırsa, `$Default` tüketici grubu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b0465-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="b0465-114">`connection`Olay hub'ın ad bağlantı dizesi içeren bir uygulama ayarı adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0465-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="b0465-115">Tıklayarak bu bağlantı dizesini kopyalayın **bağlantı bilgilerini** için düğmesini *ad alanı*, olay hub kendisini değil.</span><span class="sxs-lookup"><span data-stu-id="b0465-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="b0465-116">Bu bağlantı dizesi en az tetikleyici etkinleştirmek için Okuma izinleriniz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0465-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="b0465-117">[Ek ayarları](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) daha fazla olay hub'ları Tetikleyicileri ince için host.json dosyasında sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b0465-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="b0465-118">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="b0465-118">Trigger usage</span></span>
<span data-ttu-id="b0465-119">Bir olay hub'ları Tetik işlevi tetiklendiğinde tetikler ileti işlevdeki bir dize olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="b0465-119">When an Event Hubs trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="b0465-120">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="b0465-120">Trigger sample</span></span>
<span data-ttu-id="b0465-121">Aşağıdaki olduğunu varsayalım, olay hub'ları tetiklemek `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b0465-121">Suppose you have the following Event Hubs trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="b0465-122">Olay hub'ı tetikleyicisi ileti gövdesini günlüklerini dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="b0465-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="b0465-123">C#</span><span class="sxs-lookup"><span data-stu-id="b0465-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b0465-124">F#</span><span class="sxs-lookup"><span data-stu-id="b0465-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="b0465-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="b0465-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="b0465-126">Tetikleyici örnek C#</span><span class="sxs-lookup"><span data-stu-id="b0465-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="b0465-127">Olayı olarak da alabileceğiniz bir [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) olay meta verilere erişmenizi nesnesi.</span><span class="sxs-lookup"><span data-stu-id="b0465-127">You can also receive the event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access to the event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="b0465-128">Bir toplu işlemde olaylarını almak için yöntem imzası değiştirme `string[]` veya `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="b0465-128">To receive events in a batch, change the method signature to `string[]` or `EventData[]`.</span></span>

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="b0465-129">F # tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="b0465-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="b0465-130">Node.js tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="b0465-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="b0465-131">Olay hub'ları bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="b0465-131">Event Hubs output binding</span></span>
<span data-ttu-id="b0465-132">Bir olay hub'ı olay akışına yazma olayları bağlama olay hub'ları çıkış kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0465-132">Use the Event Hubs output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="b0465-133">Yazma olayları için bir olay hub'ına gönderme izni olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0465-133">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="b0465-134">Aşağıdaki JSON nesnesinde çıkış bağlama kullanır `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b0465-134">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="b0465-135">`connection`Olay hub'ın ad bağlantı dizesi içeren bir uygulama ayarı adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0465-135">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="b0465-136">Tıklayarak bu bağlantı dizesini kopyalayın **bağlantı bilgilerini** için düğmesini *ad alanı*, olay hub kendisini değil.</span><span class="sxs-lookup"><span data-stu-id="b0465-136">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="b0465-137">Bu bağlantı dizesi olay akışının ileti göndermek için Gönder izinleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b0465-137">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="b0465-138">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="b0465-138">Output usage</span></span>
<span data-ttu-id="b0465-139">Bu bölümde işlevi kodunuzda bağlama, olay hub'ları çıkış kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b0465-139">This section shows you how to use your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="b0465-140">Aşağıdaki parametre türleri ile yapılandırılmış olay hub'ına iletileri çıkarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b0465-140">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="b0465-141">`ICollector<string>`(birden çok ileti çıkışı için)</span><span class="sxs-lookup"><span data-stu-id="b0465-141">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="b0465-142">`IAsyncCollector<string>`(zaman uyumsuz sürümü `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="b0465-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="b0465-143">Çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="b0465-143">Output sample</span></span>
<span data-ttu-id="b0465-144">Aşağıdaki olduğunu varsayalım olay hub'ları bağlamasında çıktı `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="b0465-144">Suppose you have the following Event Hubs output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="b0465-145">Bir olay bile akışa Yazar dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="b0465-145">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="b0465-146">C#</span><span class="sxs-lookup"><span data-stu-id="b0465-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b0465-147">F#</span><span class="sxs-lookup"><span data-stu-id="b0465-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="b0465-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="b0465-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="b0465-149">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="b0465-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="b0465-150">Veya birden çok iletileri oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="b0465-150">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="b0465-151">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="b0465-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="b0465-152">Node.js için çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="b0465-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="b0465-153">Veya birden çok ileti göndermek için</span><span class="sxs-lookup"><span data-stu-id="b0465-153">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b0465-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b0465-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
