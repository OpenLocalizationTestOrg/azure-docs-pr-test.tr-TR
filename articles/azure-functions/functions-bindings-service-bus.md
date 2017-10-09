---
title: "aaaAzure işlevleri Service Bus Tetikleyicileri ve bağlamaları | Microsoft Docs"
description: "Nasıl toouse Azure Service Bus tetikler ve Azure işlevlerinde bağlamaları anlayın."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Azure işlevleri Service Bus bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede açıklanır nasıl tooconfigure ve Azure işlevlerinde Azure Service Bus bağlamaları ile çalışır. 

Tetikler ve Service Bus kuyrukları ve konuları için bağlamaları çıktı Azure işlevleri destekler.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Hizmet veri yolu tetikleyici
Hizmet veri yolu kuyruğu ya da konu Hello Service Bus tetikleyici toorespond toomessages kullanın. 

Merhaba Service Bus kuyruk ve konu Tetikleyicileri hello JSON nesneler şu hello tanımlanır `bindings` function.json dizisi:

* *sıra* tetikleyici:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* *konu* tetikleyici:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

Merhaba aşağıdakileri göz önünde bulundurun:

* İçin `connection`, [işlevi uygulamanıza bir uygulama ayarı oluşturmak](functions-how-to-use-azure-function-app-settings.md) hello bağlantı dizesi tooyour Service Bus ad alanı içeren, ardından hello hello uygulama ayarı hello adını belirtin `connection` , tetikleyici bir özellik. Konumundaki gösterilen hello adımları izleyerek hello bağlantı dizesi elde [hello yönetim kimlik bilgileri elde](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Merhaba bağlantı dizesi, bir hizmet veri yolu ad alanı, bunlarla sınırlı tooa belirli kuyruk veya konu başlığı için olmalıdır.
  Bırakır `connection` boş hello tetikleyici bir varsayılan hizmet veri yolu bağlantı dizesi ayarı adlandırılmış bir uygulamada belirttiğinizi varsayar `AzureWebJobsServiceBus`.
* İçin `accessRights`, kullanılabilir değerler `manage` ve `listen`. Merhaba varsayılandır `manage`, o hello gösterir `connection` hello sahip **Yönet** izni. Merhaba sahip olmayan bir bağlantı dizesi kullanıyorsanız **Yönet** izni, `accessRights` çok`listen`. Aksi halde, çalışma zamanı gerektiren çalışırken toodo işlemler başarısız olabilir hello işlevleri hakları yönetin.

## <a name="trigger-behavior"></a>Tetikleyici davranışı
* **Tek iş parçacığı oluşturma** - varsayılan olarak, çoklu iletileri aynı anda hello işlevleri çalışma zamanı işlemler. toodirect hello çalışma zamanı tooprocess yalnızca tek bir kuyruk veya konu ileti aynı anda ayarlamak `serviceBus.maxConcurrentCalls` içinde too1 *host.json*. 
  Hakkında bilgi için *host.json*, bkz: [klasör yapısını](functions-reference.md#folder-structure) ve [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Zehirli ileti işleme** -Service Bus, denetlenmesi veya Azure işlevleri yapılandırma veya kod yapılandırılmış kendi zehirli ileti işleme yapar. 
* **PeekLock davranışı** -hello işlevleri çalışma zamanı alan bir ileti [ `PeekLock` modu](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) ve çağrıları `Complete` hello işlevi başarıyla tamamlanırsa selamlama iletisine veya çağrıları `Abandon` hello varsa işlev başarısız olur. 
  Merhaba işlevi hello uzun çalışırsa `PeekLock` zaman aşımı, hello kilidi otomatik olarak yenilenir.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Tetikleyici kullanımı
Bu bölümde, nasıl toouse, Service Bus tetiklemek işlevi kodunuzda gösterir. 

C# ve F #'de hello Service Bus tetikleyici ileti şu giriş türlerini Merhaba, seri durumdan çıkarılmış tooany olabilir:

* `string`-dize iletileri için faydalı
* `byte[]`-ikili veriler için kullanışlıdır
* Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş veriler için kullanışlıdır.
  Özel bir giriş türü gibi bildirme varsa `CustomType`, Azure işlevleri, belirtilen türe toodeserialize hello JSON verilerini çalışır.
* `BrokeredMessage`-sağlar, hello seri hello iletisiyle [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) yöntemi.

Node.js içinde hello Service Bus tetikleyici ileti hello işlevine bir dize veya JSON nesnesi olarak geçirilir.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Tetikleyici örnek
Function.json aşağıdaki hello olduğunu varsayalım:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Hizmet veri yolu kuyruğu iletisini işler hello dile özgü örneğine bakın.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Tetikleyici örnek C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>F # tetikleyici örnek #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Node.js tetikleyici örnek

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Hizmet veri yolu bağlama çıktı
Merhaba işlevi için Service Bus kuyruk ve konu çıkış kullanmak hello JSON nesneler şu hello `bindings` function.json dizisi:

* *sıra* çıktı:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* *konu* çıktı:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

Merhaba aşağıdakileri göz önünde bulundurun:

* İçin `connection`, [işlevi uygulamanıza bir uygulama ayarı oluşturmak](functions-how-to-use-azure-function-app-settings.md) hello bağlantı dizesi tooyour Service Bus ad alanı içeren, ardından hello hello uygulama ayarı hello adını belirtin `connection` özelliği, çıkışı bağlama. Konumundaki gösterilen hello adımları izleyerek hello bağlantı dizesi elde [hello yönetim kimlik bilgileri elde](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Merhaba bağlantı dizesi, bir hizmet veri yolu ad alanı, bunlarla sınırlı tooa belirli kuyruk veya konu başlığı için olmalıdır.
  Bırakır `connection` boş hello çıkış bağlama varsayılan hizmet veri yolu bağlantı dizesi adlandırılmış ayarını bir uygulamada belirttiğiniz varsayar `AzureWebJobsServiceBus`.
* İçin `accessRights`, kullanılabilir değerler `manage` ve `listen`. Merhaba varsayılandır `manage`, o hello gösterir `connection` hello sahip **Yönet** izni. Merhaba sahip olmayan bir bağlantı dizesi kullanıyorsanız **Yönet** izni, `accessRights` çok`listen`. Aksi halde, çalışma zamanı gerektiren çalışırken toodo işlemler başarısız olabilir hello işlevleri hakları yönetin.

<a name="outputusage"></a>

## <a name="output-usage"></a>Çıktı kullanımı
C# ve F #'de Azure işlevleri şu türlerini hello hiçbirini bir Service Bus kuyruk iletisi oluşturun:

* Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) -parametre tanımına arar gibi `out T paramName` (C#).
  İşlevler JSON iletiye hello nesne seri durumdan çıkarır. Merhaba işlevi çıktığında hello çıkış değer null ise işlevleri null bir nesne ile Merhaba iletisi oluşturur.
* `string`-Parametre tanımına arar gibi `out string paraName` (C#). Merhaba işlevi çıktığında hello parametre değeri null olmayan ise, işlevleri bir ileti oluşturur.
* `byte[]`-Parametre tanımına arar gibi `out byte[] paraName` (C#). Merhaba işlevi çıktığında hello parametre değeri null olmayan ise, işlevleri bir ileti oluşturur.
* `BrokeredMessage`Parametre tanımına arar gibi `out BrokeredMessage paraName` (C#). Merhaba işlevi çıktığında hello parametre değeri null olmayan ise, işlevleri bir ileti oluşturur.

C# işlevinde birden çok ileti oluşturmak için kullanabilirsiniz `ICollector<T>` veya `IAsyncCollector<T>`. Merhaba çağırdığınızda bir ileti oluşturulur `Add` yöntemi.

Node.js içinde bir dize, bir bayt dizisi veya (JSON'a seri durumdan) bir Javascript nesne çok atayabilirsiniz`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Çıkış örneği
Hizmet veri yolu kuyruğu çıkış tanımlayan function.json aşağıdaki hello olduğunu varsayalım:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Bir ileti toohello hizmet veri yolu kuyruğu gönderir hello dile özgü örneğine bakın.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# çıktı örneği #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

Veya, toocreate birden fazla ileti:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>F # çıktı örneği #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Node.js çıktı örneği

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

Veya, toocreate birden fazla ileti:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

