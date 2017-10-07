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
# <a name="azure-functions-event-hubs-bindings"></a>Azure işlevleri olay hub'ları bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede açıklanır nasıl tooconfigure ve [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) Azure işlevleri için bağlamaları.
Tetikler ve olay hub'ları için bağlamaları çıktı Azure işlevleri destekler.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Yeni tooAzure olay hub'ları olup olmadığını hello görmek [Event Hubs'a genel bakış](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Olay hub'ı tetikleyicisi
Merhaba olay hub'ı kullan tooan olay hub'ı olay akışının gönderilen toorespond tooan olay tetikler. Okuma erişimi toohello olay hub'ı tooset hello tetikleyici yukarı olması gerekir.

Merhaba olay hub'ları işlevi tetikleyici kullanan hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:

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

`consumerGroup`kullanılan isteğe bağlı özellik tooset hello olan [tüketici grubu](../event-hubs/event-hubs-features.md#event-consumers) toosubscribe tooevents hello hub kullanılır. Atlanırsa, hello `$Default` tüketici grubu kullanılır.  
`connection`Merhaba bağlantı dizesi toohello olay hub'ın ad alanı içeren bir uygulama ayarı Hello adı olması gerekir.
Merhaba tıklayarak bu bağlantı dizesini kopyalayın **bağlantı bilgilerini** hello düğmesi *ad alanı*, değil hello olay hub'ı kendisi. Bu bağlantı dizesi, en az izinleri tooactivate hello tetikleyici okuma sahiptir.

[Ek ayarları](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) bir host.json dosya toofurther ince ince ayar sağlanan olay hub'ları Tetikleyicileri olabilir.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Tetikleyici kullanımı
Bir olay hub'ları Tetik işlevi tetiklendiğinde tetikler selamlama iletisine tabloya hello işlev bir dize olarak geçirilir.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Tetikleyici örnek
Aşağıdaki olay hub'ları tetiklemek hello hello olduğunu varsayalım `bindings` function.json dizisi:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Merhaba olay hub'ı tetikleyicisi hello ileti gövdesi günlüklerini hello dile özgü örneğine bakın.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Tetikleyici örnek C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Merhaba olayı olarak da alabileceğiniz bir [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) size verir nesneye erişim toohello olay meta verileri.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

bir toplu tooreceive olayları değiştir hello yöntem imzası çok`string[]` veya `EventData[]`.

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

### <a name="trigger-sample-in-f"></a>F # tetikleyici örnek #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Node.js tetikleyici örnek

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Olay hub'ları bağlama çıktı
Kullanım hello olay hub'ları bağlama toowrite olayları tooan olay hub'ı olay akışının çıktı. Gönderme izni tooan olay hub'ı toowrite olayları tooit olması gerekir.

Merhaba çıkış bağlama kullanır hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`Merhaba bağlantı dizesi toohello olay hub'ın ad alanı içeren bir uygulama ayarı Hello adı olması gerekir.
Merhaba tıklayarak bu bağlantı dizesini kopyalayın **bağlantı bilgilerini** hello düğmesi *ad alanı*, değil hello olay hub'ı kendisi. Bu bağlantı dizesi gönderme izinleri toosend hello ileti toohello olay akışı olması gerekir.

## <a name="output-usage"></a>Çıktı kullanımı
Bu bölümde, nasıl işlevi kodunuzda bağlama toouse, olay hub'larınızı çıktısını gösterir.

Parametre türleri şu hello ile yapılandırılmış toohello event hub'ı iletileri çıkarabilirsiniz:

* `out string`
* `ICollector<string>`(toooutput birden fazla ileti)
* `IAsyncCollector<string>`(zaman uyumsuz sürümü `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Çıkış örneği
Merhaba aşağıdaki olduğunu varsayalım olay hub'ları hello bağlamasında çıktı `bindings` function.json dizisi:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Bir olay toohello bile akışa Yazar hello dile özgü örneğine bakın.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# çıktı örneği #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

Veya, toocreate birden fazla ileti:

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

### <a name="output-sample-in-f"></a>F # çıktı örneği #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Node.js için çıktı örneği

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

Veya, toosend birden fazla ileti

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

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
