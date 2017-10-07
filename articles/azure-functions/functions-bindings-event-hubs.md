---
title: "aaaAzure işlevleri olay hub'ları bağlamaları | Microsoft Docs"
description: "Anlamak nasıl toouse Azure Event Hubs bağlamaları Azure işlevlerinde."
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
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="44137-104">Azure işlevleri olay hub'ları bağlamaları</span><span class="sxs-lookup"><span data-stu-id="44137-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="44137-105">Bu makalede açıklanır nasıl tooconfigure ve [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) Azure işlevleri için bağlamaları.</span><span class="sxs-lookup"><span data-stu-id="44137-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="44137-106">Tetikler ve olay hub'ları için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="44137-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="44137-107">Yeni tooAzure olay hub'ları olup olmadığını hello görmek [Event Hubs'a genel bakış](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="44137-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="44137-108">Olay hub'ı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="44137-108">Event hub trigger</span></span>
<span data-ttu-id="44137-109">Merhaba olay hub'ı kullan tooan olay hub'ı olay akışının gönderilen toorespond tooan olay tetikler.</span><span class="sxs-lookup"><span data-stu-id="44137-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="44137-110">Okuma erişimi toohello olay hub'ı tooset hello tetikleyici yukarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44137-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="44137-111">Merhaba olay hub'ları işlevi tetikleyici kullanan hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="44137-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="44137-112">`consumerGroup`kullanılan isteğe bağlı özellik tooset hello olan [tüketici grubu](../event-hubs/event-hubs-features.md#event-consumers) toosubscribe tooevents hello hub kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44137-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="44137-113">Atlanırsa, hello `$Default` tüketici grubu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44137-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="44137-114">`connection`Merhaba bağlantı dizesi toohello olay hub'ın ad alanı içeren bir uygulama ayarı Hello adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44137-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="44137-115">Merhaba tıklayarak bu bağlantı dizesini kopyalayın **bağlantı bilgilerini** hello düğmesi *ad alanı*, değil hello olay hub'ı kendisi.</span><span class="sxs-lookup"><span data-stu-id="44137-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="44137-116">Bu bağlantı dizesi, en az izinleri tooactivate hello tetikleyici okuma sahiptir.</span><span class="sxs-lookup"><span data-stu-id="44137-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="44137-117">[Ek ayarları](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) bir host.json dosya toofurther ince ince ayar sağlanan olay hub'ları Tetikleyicileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="44137-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="44137-118">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="44137-118">Trigger usage</span></span>
<span data-ttu-id="44137-119">Bir olay hub'ları Tetik işlevi tetiklendiğinde tetikler selamlama iletisine tabloya hello işlev bir dize olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="44137-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="44137-120">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="44137-120">Trigger sample</span></span>
<span data-ttu-id="44137-121">Aşağıdaki olay hub'ları tetiklemek hello hello olduğunu varsayalım `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="44137-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="44137-122">Merhaba olay hub'ı tetikleyicisi hello ileti gövdesi günlüklerini hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="44137-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="44137-123">C#</span><span class="sxs-lookup"><span data-stu-id="44137-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="44137-124">F#</span><span class="sxs-lookup"><span data-stu-id="44137-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="44137-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="44137-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="44137-126">Tetikleyici örnek C#</span><span class="sxs-lookup"><span data-stu-id="44137-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="44137-127">Merhaba olayı olarak da alabileceğiniz bir [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) size verir nesneye erişim toohello olay meta verileri.</span><span class="sxs-lookup"><span data-stu-id="44137-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="44137-128">bir toplu tooreceive olayları değiştir hello yöntem imzası çok`string[]` veya `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="44137-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="44137-129">F # tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="44137-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="44137-130">Node.js tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="44137-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="44137-131">Olay hub'ları bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="44137-131">Event Hubs output binding</span></span>
<span data-ttu-id="44137-132">Kullanım hello olay hub'ları bağlama toowrite olayları tooan olay hub'ı olay akışının çıktı.</span><span class="sxs-lookup"><span data-stu-id="44137-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="44137-133">Gönderme izni tooan olay hub'ı toowrite olayları tooit olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44137-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="44137-134">Merhaba çıkış bağlama kullanır hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="44137-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="44137-135">`connection`Merhaba bağlantı dizesi toohello olay hub'ın ad alanı içeren bir uygulama ayarı Hello adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44137-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="44137-136">Merhaba tıklayarak bu bağlantı dizesini kopyalayın **bağlantı bilgilerini** hello düğmesi *ad alanı*, değil hello olay hub'ı kendisi.</span><span class="sxs-lookup"><span data-stu-id="44137-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="44137-137">Bu bağlantı dizesi gönderme izinleri toosend hello ileti toohello olay akışı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44137-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="44137-138">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="44137-138">Output usage</span></span>
<span data-ttu-id="44137-139">Bu bölümde, nasıl işlevi kodunuzda bağlama toouse, olay hub'larınızı çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="44137-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="44137-140">Parametre türleri şu hello ile yapılandırılmış toohello event hub'ı iletileri çıkarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="44137-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="44137-141">`ICollector<string>`(toooutput birden fazla ileti)</span><span class="sxs-lookup"><span data-stu-id="44137-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="44137-142">`IAsyncCollector<string>`(zaman uyumsuz sürümü `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="44137-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="44137-143">Çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="44137-143">Output sample</span></span>
<span data-ttu-id="44137-144">Merhaba aşağıdaki olduğunu varsayalım olay hub'ları hello bağlamasında çıktı `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="44137-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="44137-145">Bir olay toohello bile akışa Yazar hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="44137-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="44137-146">C#</span><span class="sxs-lookup"><span data-stu-id="44137-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="44137-147">F#</span><span class="sxs-lookup"><span data-stu-id="44137-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="44137-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="44137-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="44137-149">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="44137-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="44137-150">Veya, toocreate birden fazla ileti:</span><span class="sxs-lookup"><span data-stu-id="44137-150">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="44137-151">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="44137-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="44137-152">Node.js için çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="44137-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="44137-153">Veya, toosend birden fazla ileti</span><span class="sxs-lookup"><span data-stu-id="44137-153">Or, toosend multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="44137-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44137-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
