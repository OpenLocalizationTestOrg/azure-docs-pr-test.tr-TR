---
title: "aaaAzure işlevleri kuyruk depolama bağlamaları | Microsoft Docs"
description: "Nasıl toouse Azure Storage tetikler ve Azure işlevlerinde bağlamaları anlayın."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a>Azure işlevleri kuyruk depolama bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede nasıl tooconfigure ve kod Azure kuyruk depolama bağlamaları Azure işlevlerinde. Tetikler ve Azure sıralar bağlamaları çıktı Azure işlevleri destekler. Tüm bağlama kullanılabilir olan özellikler için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Kuyruk depolama tetikleyici
Hello Azure kuyruk depolama tetikleyici toothem tepki vermek ve yeni iletiler için bir kuyruk depolama toomonitor sağlar. 

Hello kullanarak bir sıra tetikleyici tanımlamak **tümleştir** hello işlevleri portalındaki sekmesi. Merhaba portal oluşturur hello tanımında aşağıdaki hello **bağlamaları** bölümünü *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Merhaba `connection` özelliği, depolama bağlantı dizesi içeren bir uygulama ayarı hello adını içermelidir. Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde bir depolama hesabı seçtiğinizde, bu uygulama ayarı yapılandırır.

Ek ayarları sağlanabilir bir [host.json dosya](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ince ayar kuyruk depolama tetikler. Örneğin, host.json hello sıra yoklama aralığını değiştirebilirsiniz.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Bir kuyruk Tetikleyici kullanma
Node.js işlevlerde hello sıra verileri kullanarak erişim `context.bindings.<name>`.


.NET işlevlerde hello sıra yükü gibi bir yöntem parametresi kullanılarak erişim `CloudQueueMessage paramName`. Burada, `paramName` hello belirtilen hello değeri [tetikleyici yapılandırma](#trigger). Hello kuyruk iletisi seri durumdan çıkarılmış tooany şu türlerini hello biri olabilir:

* POCO nesnesi. Merhaba kuyruk yükü bir JSON nesnesi ise kullanın. Merhaba işlevleri çalışma zamanı hello yükü hello POCO nesnesine seri durumdan çıkarır. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Sıra tetikleyici meta verileri
Merhaba sıra tetikleyici çeşitli meta veri özelliklerini sağlar. Bu özellikler, diğer bağlamaları bağlama ifadelerinde bir parçası olarak ya da kodunuzu parametre olarak kullanılabilir. Merhaba değerlere sahip hello aynı topluca [ `CloudQueueMessage` ].

* **QueueTrigger** -sıra Yükü (geçerli bir dize ise)
* **DequeueCount** -türü `int`. Bu iletiyi kuyruktan çıkarıldı sayısı hello.
* **ExpirationTime** -türü `DateTimeOffset?`. Başlangıç saati, selamlama iletisine süresi dolar.
* **Kimliği** -türü `string`. Sıra ileti kimliği.
* **InsertionTime** -türü `DateTimeOffset?`. Başlangıç saati, selamlama iletisine toohello sıraya eklendi.
* **NextVisibleTime** -türü `DateTimeOffset?`. Başlangıç saati, selamlama iletisine sonraki görünür olur.
* **PopReceipt** -türü `string`. Merhaba ileti pop giriş.

Nasıl toouse hello sıra meta verilerde bkz [tetikleyici örnek](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Tetikleyici örnek
Bir kuyruk tetikleyici tanımlar function.json aşağıdaki hello olduğunu varsayalım:

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

Alan ve sıra meta veri günlüklerini hello dile özgü örneğine bakın.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Tetikleyici örnek C# #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Node.js tetikleyici örnek

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a>Zarar iletileri işleme
Bir kuyruk Tetik işlevi başarısız olduğunda, Azure işlevleri hello ilk içeren verilen kuyruk iletisi saatlere deneyin toofive bu işlevini yeniden dener. Tüm beş deneme başarısız olursa hello işlevleri çalışma zamanı adlı bir ileti tooa kuyruk depolama ekler  *&lt;originalqueuename >-zararlı*. Bir işlev tooprocess iletileri hello zararlı sıradan günlüğe yazma veya el ile ilgilenilmesi gereken bir bildirim göndererek yazabilirsiniz. 

toohandle zarar iletileri el ile denetleyin hello `dequeueCount` hello kuyruk iletisinin (bkz [sıra tetikleyici meta verileri](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Kuyruk depolama bağlama çıktı
Hello Azure kuyruk depolama bağlama toowrite iletileri tooa sırası etkinleştirir çıktı. 

Bir sırayı tanımlayan hello kullanarak çıktı bağlama **tümleştir** hello işlevleri portalındaki sekmesi. Merhaba portal oluşturur hello tanımında aşağıdaki hello **bağlamaları** bölümünü *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Merhaba `connection` özelliği, depolama bağlantı dizesi içeren bir uygulama ayarı hello adını içermelidir. Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde bir depolama hesabı seçtiğinizde, bu uygulama ayarı yapılandırır.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Bir kuyruk kullanarak çıktıyı bağlama
Node.js işlevlerde hello çıkış sırası kullanarak erişim `context.bindings.<name>`.

.NET işlevlerde şu türlerini hello tooany çıkarabilirsiniz. Tür parametresi olduğunda `T`, `T` desteklenen hello çıkış türlerinden birini gibi olmalıdır `string` veya bir POCO.

* `out T`(JSON olarak serileştirilmiş)
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

Merhaba yönteminin dönüş türü hello kullanabilirsiniz bağlama çıktı.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Sıra çıktı örneği
Merhaba aşağıdaki *function.json* bir HTTP tetikleyicisi bir sıra ile tanımlar bağlama çıktı:

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

Bir kuyruk iletisi hello gelen HTTP yükü ile çıkarır hello dile özgü örneğine bakın.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>C# sıra çıktı örneği #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

birden çok iletileri toosend kullanan bir `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Node.js sıra çıktı örneği

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

Veya, toosend birden fazla ileti

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Sonraki adımlar

Kuyruk depolama Tetikleyicileri ve bağlamaları kullanan bir işlev örneği için bkz: [Azure bağlı işlevi tooan Azure hizmeti oluşturma](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

['CloudQueueMessage']: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
