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
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="bc417-104">Azure işlevleri Service Bus bağlamaları</span><span class="sxs-lookup"><span data-stu-id="bc417-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="bc417-105">Bu makalede açıklanır nasıl tooconfigure ve Azure işlevlerinde Azure Service Bus bağlamaları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="bc417-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="bc417-106">Tetikler ve Service Bus kuyrukları ve konuları için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="bc417-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="bc417-107">Hizmet veri yolu tetikleyici</span><span class="sxs-lookup"><span data-stu-id="bc417-107">Service Bus trigger</span></span>
<span data-ttu-id="bc417-108">Hizmet veri yolu kuyruğu ya da konu Hello Service Bus tetikleyici toorespond toomessages kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc417-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="bc417-109">Merhaba Service Bus kuyruk ve konu Tetikleyicileri hello JSON nesneler şu hello tanımlanır `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="bc417-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="bc417-110">*sıra* tetikleyici:</span><span class="sxs-lookup"><span data-stu-id="bc417-110">*queue* trigger:</span></span>

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

* <span data-ttu-id="bc417-111">*konu* tetikleyici:</span><span class="sxs-lookup"><span data-stu-id="bc417-111">*topic* trigger:</span></span>

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

<span data-ttu-id="bc417-112">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="bc417-112">Note hello following:</span></span>

* <span data-ttu-id="bc417-113">İçin `connection`, [işlevi uygulamanıza bir uygulama ayarı oluşturmak](functions-how-to-use-azure-function-app-settings.md) hello bağlantı dizesi tooyour Service Bus ad alanı içeren, ardından hello hello uygulama ayarı hello adını belirtin `connection` , tetikleyici bir özellik.</span><span class="sxs-lookup"><span data-stu-id="bc417-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="bc417-114">Konumundaki gösterilen hello adımları izleyerek hello bağlantı dizesi elde [hello yönetim kimlik bilgileri elde](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="bc417-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="bc417-115">Merhaba bağlantı dizesi, bir hizmet veri yolu ad alanı, bunlarla sınırlı tooa belirli kuyruk veya konu başlığı için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc417-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="bc417-116">Bırakır `connection` boş hello tetikleyici bir varsayılan hizmet veri yolu bağlantı dizesi ayarı adlandırılmış bir uygulamada belirttiğinizi varsayar `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="bc417-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="bc417-117">İçin `accessRights`, kullanılabilir değerler `manage` ve `listen`.</span><span class="sxs-lookup"><span data-stu-id="bc417-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="bc417-118">Merhaba varsayılandır `manage`, o hello gösterir `connection` hello sahip **Yönet** izni.</span><span class="sxs-lookup"><span data-stu-id="bc417-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="bc417-119">Merhaba sahip olmayan bir bağlantı dizesi kullanıyorsanız **Yönet** izni, `accessRights` çok`listen`.</span><span class="sxs-lookup"><span data-stu-id="bc417-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="bc417-120">Aksi halde, çalışma zamanı gerektiren çalışırken toodo işlemler başarısız olabilir hello işlevleri hakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc417-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="bc417-121">Tetikleyici davranışı</span><span class="sxs-lookup"><span data-stu-id="bc417-121">Trigger behavior</span></span>
* <span data-ttu-id="bc417-122">**Tek iş parçacığı oluşturma** - varsayılan olarak, çoklu iletileri aynı anda hello işlevleri çalışma zamanı işlemler.</span><span class="sxs-lookup"><span data-stu-id="bc417-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="bc417-123">toodirect hello çalışma zamanı tooprocess yalnızca tek bir kuyruk veya konu ileti aynı anda ayarlamak `serviceBus.maxConcurrentCalls` içinde too1 *host.json*.</span><span class="sxs-lookup"><span data-stu-id="bc417-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="bc417-124">Hakkında bilgi için *host.json*, bkz: [klasör yapısını](functions-reference.md#folder-structure) ve [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="bc417-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="bc417-125">**Zehirli ileti işleme** -Service Bus, denetlenmesi veya Azure işlevleri yapılandırma veya kod yapılandırılmış kendi zehirli ileti işleme yapar.</span><span class="sxs-lookup"><span data-stu-id="bc417-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="bc417-126">**PeekLock davranışı** -hello işlevleri çalışma zamanı alan bir ileti [ `PeekLock` modu](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) ve çağrıları `Complete` hello işlevi başarıyla tamamlanırsa selamlama iletisine veya çağrıları `Abandon` hello varsa işlev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="bc417-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="bc417-127">Merhaba işlevi hello uzun çalışırsa `PeekLock` zaman aşımı, hello kilidi otomatik olarak yenilenir.</span><span class="sxs-lookup"><span data-stu-id="bc417-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="bc417-128">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="bc417-128">Trigger usage</span></span>
<span data-ttu-id="bc417-129">Bu bölümde, nasıl toouse, Service Bus tetiklemek işlevi kodunuzda gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc417-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="bc417-130">C# ve F #'de hello Service Bus tetikleyici ileti şu giriş türlerini Merhaba, seri durumdan çıkarılmış tooany olabilir:</span><span class="sxs-lookup"><span data-stu-id="bc417-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="bc417-131">`string`-dize iletileri için faydalı</span><span class="sxs-lookup"><span data-stu-id="bc417-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="bc417-132">`byte[]`-ikili veriler için kullanışlıdır</span><span class="sxs-lookup"><span data-stu-id="bc417-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="bc417-133">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş veriler için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="bc417-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="bc417-134">Özel bir giriş türü gibi bildirme varsa `CustomType`, Azure işlevleri, belirtilen türe toodeserialize hello JSON verilerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="bc417-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="bc417-135">`BrokeredMessage`-sağlar, hello seri hello iletisiyle [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bc417-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="bc417-136">Node.js içinde hello Service Bus tetikleyici ileti hello işlevine bir dize veya JSON nesnesi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="bc417-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="bc417-137">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="bc417-137">Trigger sample</span></span>
<span data-ttu-id="bc417-138">Function.json aşağıdaki hello olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="bc417-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="bc417-139">Hizmet veri yolu kuyruğu iletisini işler hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="bc417-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="bc417-140">C#</span><span class="sxs-lookup"><span data-stu-id="bc417-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="bc417-141">F#</span><span class="sxs-lookup"><span data-stu-id="bc417-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="bc417-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="bc417-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="bc417-143">Tetikleyici örnek C#</span><span class="sxs-lookup"><span data-stu-id="bc417-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="bc417-144">F # tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="bc417-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="bc417-145">Node.js tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="bc417-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="bc417-146">Hizmet veri yolu bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="bc417-146">Service Bus output binding</span></span>
<span data-ttu-id="bc417-147">Merhaba işlevi için Service Bus kuyruk ve konu çıkış kullanmak hello JSON nesneler şu hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="bc417-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="bc417-148">*sıra* çıktı:</span><span class="sxs-lookup"><span data-stu-id="bc417-148">*queue* output:</span></span>

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
* <span data-ttu-id="bc417-149">*konu* çıktı:</span><span class="sxs-lookup"><span data-stu-id="bc417-149">*topic* output:</span></span>

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

<span data-ttu-id="bc417-150">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="bc417-150">Note hello following:</span></span>

* <span data-ttu-id="bc417-151">İçin `connection`, [işlevi uygulamanıza bir uygulama ayarı oluşturmak](functions-how-to-use-azure-function-app-settings.md) hello bağlantı dizesi tooyour Service Bus ad alanı içeren, ardından hello hello uygulama ayarı hello adını belirtin `connection` özelliği, çıkışı bağlama.</span><span class="sxs-lookup"><span data-stu-id="bc417-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="bc417-152">Konumundaki gösterilen hello adımları izleyerek hello bağlantı dizesi elde [hello yönetim kimlik bilgileri elde](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="bc417-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="bc417-153">Merhaba bağlantı dizesi, bir hizmet veri yolu ad alanı, bunlarla sınırlı tooa belirli kuyruk veya konu başlığı için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bc417-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="bc417-154">Bırakır `connection` boş hello çıkış bağlama varsayılan hizmet veri yolu bağlantı dizesi adlandırılmış ayarını bir uygulamada belirttiğiniz varsayar `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="bc417-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="bc417-155">İçin `accessRights`, kullanılabilir değerler `manage` ve `listen`.</span><span class="sxs-lookup"><span data-stu-id="bc417-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="bc417-156">Merhaba varsayılandır `manage`, o hello gösterir `connection` hello sahip **Yönet** izni.</span><span class="sxs-lookup"><span data-stu-id="bc417-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="bc417-157">Merhaba sahip olmayan bir bağlantı dizesi kullanıyorsanız **Yönet** izni, `accessRights` çok`listen`.</span><span class="sxs-lookup"><span data-stu-id="bc417-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="bc417-158">Aksi halde, çalışma zamanı gerektiren çalışırken toodo işlemler başarısız olabilir hello işlevleri hakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc417-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="bc417-159">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="bc417-159">Output usage</span></span>
<span data-ttu-id="bc417-160">C# ve F #'de Azure işlevleri şu türlerini hello hiçbirini bir Service Bus kuyruk iletisi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="bc417-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="bc417-161">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) -parametre tanımına arar gibi `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bc417-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="bc417-162">İşlevler JSON iletiye hello nesne seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="bc417-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="bc417-163">Merhaba işlevi çıktığında hello çıkış değer null ise işlevleri null bir nesne ile Merhaba iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc417-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="bc417-164">`string`-Parametre tanımına arar gibi `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bc417-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="bc417-165">Merhaba işlevi çıktığında hello parametre değeri null olmayan ise, işlevleri bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc417-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="bc417-166">`byte[]`-Parametre tanımına arar gibi `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bc417-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="bc417-167">Merhaba işlevi çıktığında hello parametre değeri null olmayan ise, işlevleri bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc417-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="bc417-168">`BrokeredMessage`Parametre tanımına arar gibi `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="bc417-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="bc417-169">Merhaba işlevi çıktığında hello parametre değeri null olmayan ise, işlevleri bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc417-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="bc417-170">C# işlevinde birden çok ileti oluşturmak için kullanabilirsiniz `ICollector<T>` veya `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="bc417-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="bc417-171">Merhaba çağırdığınızda bir ileti oluşturulur `Add` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bc417-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="bc417-172">Node.js içinde bir dize, bir bayt dizisi veya (JSON'a seri durumdan) bir Javascript nesne çok atayabilirsiniz`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="bc417-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="bc417-173">Çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="bc417-173">Output sample</span></span>
<span data-ttu-id="bc417-174">Hizmet veri yolu kuyruğu çıkış tanımlayan function.json aşağıdaki hello olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="bc417-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="bc417-175">Bir ileti toohello hizmet veri yolu kuyruğu gönderir hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="bc417-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="bc417-176">C#</span><span class="sxs-lookup"><span data-stu-id="bc417-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="bc417-177">F#</span><span class="sxs-lookup"><span data-stu-id="bc417-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="bc417-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="bc417-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="bc417-179">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="bc417-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="bc417-180">Veya, toocreate birden fazla ileti:</span><span class="sxs-lookup"><span data-stu-id="bc417-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="bc417-181">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="bc417-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="bc417-182">Node.js çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="bc417-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="bc417-183">Veya, toocreate birden fazla ileti:</span><span class="sxs-lookup"><span data-stu-id="bc417-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bc417-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc417-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

