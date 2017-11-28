---
title: "Azure işlevleri Service Bus Tetikleyicileri ve bağlamaları | Microsoft Docs"
description: "Azure Service Bus Tetikleyicileri ve bağlamaları Azure işlevlerinde nasıl kullanılacağını anlayın."
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
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="d4035-104">Azure işlevleri Service Bus bağlamaları</span><span class="sxs-lookup"><span data-stu-id="d4035-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d4035-105">Bu makalede, yapılandırma ve Azure Service Bus bağlamaları Azure işlevlerinde çalışmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d4035-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="d4035-106">Tetikler ve Service Bus kuyrukları ve konuları için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="d4035-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="d4035-107">Hizmet veri yolu tetikleyici</span><span class="sxs-lookup"><span data-stu-id="d4035-107">Service Bus trigger</span></span>
<span data-ttu-id="d4035-108">Hizmet veri yolu kuyruğu ya da konu iletilerine yanıt için Service Bus tetikleyici kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4035-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="d4035-109">Hizmet veri yolu kuyruk ve konu Tetikleyicileri aşağıdaki JSON nesneler tarafından tanımlanan `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d4035-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="d4035-110">*sıra* tetikleyici:</span><span class="sxs-lookup"><span data-stu-id="d4035-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="d4035-111">*konu* tetikleyici:</span><span class="sxs-lookup"><span data-stu-id="d4035-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="d4035-112">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d4035-112">Note the following:</span></span>

* <span data-ttu-id="d4035-113">İçin `connection`, [işlevi uygulamanıza bir uygulama ayarı oluşturmak](functions-how-to-use-azure-function-app-settings.md) hizmet veri yolu ad alanınıza bağlantı dizesi içeren, uygulama ayarı adı belirtin `connection` , tetikleyici bir özellik.</span><span class="sxs-lookup"><span data-stu-id="d4035-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="d4035-114">Konumundaki gösterilen adımları izleyerek bağlantı dizesini elde [yönetim kimlik bilgileri elde](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="d4035-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="d4035-115">Bağlantı dizesi, belirli bir kuyruğa ya da konu bunlarla sınırlı olmamak bir hizmet veri yolu ad alanı için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d4035-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="d4035-116">Bırakır `connection` boş, tetikleyici bir varsayılan hizmet veri yolu bağlantı dizesi ayarı adlandırılmış bir uygulamada belirttiğinizi varsayar `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="d4035-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="d4035-117">İçin `accessRights`, kullanılabilir değerler `manage` ve `listen`.</span><span class="sxs-lookup"><span data-stu-id="d4035-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="d4035-118">Varsayılan değer `manage`, hangi gösterir `connection` sahip **Yönet** izni.</span><span class="sxs-lookup"><span data-stu-id="d4035-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="d4035-119">Sahip olmayan bir bağlantı dizesi kullanıyorsanız **Yönet** izni, `accessRights` için `listen`.</span><span class="sxs-lookup"><span data-stu-id="d4035-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="d4035-120">Aksi halde, çalışma zamanı gerektiren işlemleri yapmaya başarısız olabilir işlevleri hakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="d4035-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="d4035-121">Tetikleyici davranışı</span><span class="sxs-lookup"><span data-stu-id="d4035-121">Trigger behavior</span></span>
* <span data-ttu-id="d4035-122">**Tek iş parçacığı oluşturma** - varsayılan olarak, çoklu iletileri aynı anda işlevleri çalışma zamanı işlemler.</span><span class="sxs-lookup"><span data-stu-id="d4035-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="d4035-123">Bir kerede yalnızca bir tek kuyruk veya konu ileti işleme için çalışma zamanı yönlendirmek için ayarlanmış `serviceBus.maxConcurrentCalls` 1 olarak *host.json*.</span><span class="sxs-lookup"><span data-stu-id="d4035-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="d4035-124">Hakkında bilgi için *host.json*, bkz: [klasör yapısını](functions-reference.md#folder-structure) ve [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="d4035-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="d4035-125">**Zehirli ileti işleme** -Service Bus, denetlenmesi veya Azure işlevleri yapılandırma veya kod yapılandırılmış kendi zehirli ileti işleme yapar.</span><span class="sxs-lookup"><span data-stu-id="d4035-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="d4035-126">**PeekLock davranışı** -işlevler çalışma zamanı alan bir ileti [ `PeekLock` modu](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) ve çağrıları `Complete` işlevi başarıyla tamamlanırsa ileti veya çağrıları `Abandon` varsa işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d4035-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="d4035-127">İşlev süreden uzun çalışırsa `PeekLock` zaman aşımı, kilidi otomatik olarak yenilenir.</span><span class="sxs-lookup"><span data-stu-id="d4035-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="d4035-128">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="d4035-128">Trigger usage</span></span>
<span data-ttu-id="d4035-129">Bu bölümde işlevi kodunuzda, Service Bus tetikleyici kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4035-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="d4035-130">C# ve F #'de Service Bus tetikleyici ileti herhangi aşağıdaki giriş türleri seri durumdan çıkarılabiliyorsa:</span><span class="sxs-lookup"><span data-stu-id="d4035-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="d4035-131">`string`-dize iletileri için faydalı</span><span class="sxs-lookup"><span data-stu-id="d4035-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="d4035-132">`byte[]`-ikili veriler için kullanışlıdır</span><span class="sxs-lookup"><span data-stu-id="d4035-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="d4035-133">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş veriler için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="d4035-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="d4035-134">Özel bir giriş türü gibi bildirme varsa `CustomType`, Azure işlevleri, belirtilen türe JSON verilerini seri durumdan dener.</span><span class="sxs-lookup"><span data-stu-id="d4035-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="d4035-135">`BrokeredMessage`-ile seri durumdan çıkarılmış mesajıyla [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d4035-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="d4035-136">Node.js içinde Service Bus tetikleyici ileti işlevine bir dize veya JSON nesnesi olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d4035-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="d4035-137">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="d4035-137">Trigger sample</span></span>
<span data-ttu-id="d4035-138">Aşağıdaki function.json olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d4035-138">Suppose you have the following function.json:</span></span>

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

<span data-ttu-id="d4035-139">Hizmet veri yolu kuyruğu iletisini işler dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="d4035-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="d4035-140">C#</span><span class="sxs-lookup"><span data-stu-id="d4035-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="d4035-141">F#</span><span class="sxs-lookup"><span data-stu-id="d4035-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="d4035-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="d4035-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="d4035-143">Tetikleyici örnek C#</span><span class="sxs-lookup"><span data-stu-id="d4035-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="d4035-144">F # tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="d4035-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="d4035-145">Node.js tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="d4035-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="d4035-146">Hizmet veri yolu bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="d4035-146">Service Bus output binding</span></span>
<span data-ttu-id="d4035-147">Hizmet veri yolu kuyruk ve konu çıkış bir işlev için aşağıdaki JSON nesneleri kullan `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d4035-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="d4035-148">*sıra* çıktı:</span><span class="sxs-lookup"><span data-stu-id="d4035-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="d4035-149">*konu* çıktı:</span><span class="sxs-lookup"><span data-stu-id="d4035-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="d4035-150">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d4035-150">Note the following:</span></span>

* <span data-ttu-id="d4035-151">İçin `connection`, [işlevi uygulamanıza bir uygulama ayarı oluşturmak](functions-how-to-use-azure-function-app-settings.md) hizmet veri yolu ad alanınıza bağlantı dizesi içeren, uygulama ayarı adı belirtin `connection` çıkış bağlama özelliği.</span><span class="sxs-lookup"><span data-stu-id="d4035-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="d4035-152">Konumundaki gösterilen adımları izleyerek bağlantı dizesini elde [yönetim kimlik bilgileri elde](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="d4035-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="d4035-153">Bağlantı dizesi, belirli bir kuyruğa ya da konu bunlarla sınırlı olmamak bir hizmet veri yolu ad alanı için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d4035-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="d4035-154">Bırakır `connection` boş çıkış bağlama varsayılan hizmet veri yolu bağlantı dizesi ayarı adlandırılmış bir uygulamada belirttiğinizi varsayar `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="d4035-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="d4035-155">İçin `accessRights`, kullanılabilir değerler `manage` ve `listen`.</span><span class="sxs-lookup"><span data-stu-id="d4035-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="d4035-156">Varsayılan değer `manage`, hangi gösterir `connection` sahip **Yönet** izni.</span><span class="sxs-lookup"><span data-stu-id="d4035-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="d4035-157">Sahip olmayan bir bağlantı dizesi kullanıyorsanız **Yönet** izni, `accessRights` için `listen`.</span><span class="sxs-lookup"><span data-stu-id="d4035-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="d4035-158">Aksi halde, çalışma zamanı gerektiren işlemleri yapmaya başarısız olabilir işlevleri hakları yönetin.</span><span class="sxs-lookup"><span data-stu-id="d4035-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="d4035-159">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="d4035-159">Output usage</span></span>
<span data-ttu-id="d4035-160">C# ve F #'de Azure işlevleri şu türlerden birini bir Service Bus kuyruk iletisi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d4035-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="d4035-161">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) -parametre tanımına arar gibi `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="d4035-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="d4035-162">İşlevler JSON iletiye nesne seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d4035-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="d4035-163">Çıkış değeri null ise, işlev çıktığında işlevleri null bir nesne ile iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4035-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="d4035-164">`string`-Parametre tanımına arar gibi `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="d4035-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="d4035-165">Parametre değeri null olmayan ise işlevi çıktığında işlevleri bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4035-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="d4035-166">`byte[]`-Parametre tanımına arar gibi `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="d4035-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="d4035-167">Parametre değeri null olmayan ise işlevi çıktığında işlevleri bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4035-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="d4035-168">`BrokeredMessage`Parametre tanımına arar gibi `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="d4035-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="d4035-169">Parametre değeri null olmayan ise işlevi çıktığında işlevleri bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4035-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="d4035-170">C# işlevinde birden çok ileti oluşturmak için kullanabilirsiniz `ICollector<T>` veya `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="d4035-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="d4035-171">Çağırdığınızda bir ileti oluşturulur `Add` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d4035-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="d4035-172">Node.js içinde bir dize, bir bayt dizisi veya (JSON'a seri durumdan) bir Javascript nesnesi atayabileceğiniz `context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="d4035-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="d4035-173">Çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="d4035-173">Output sample</span></span>
<span data-ttu-id="d4035-174">Hizmet veri yolu kuyruğu çıkış tanımlayan aşağıdaki function.json olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d4035-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="d4035-175">Service bus kuyruğuna ileti gönderir dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="d4035-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="d4035-176">C#</span><span class="sxs-lookup"><span data-stu-id="d4035-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="d4035-177">F#</span><span class="sxs-lookup"><span data-stu-id="d4035-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="d4035-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="d4035-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="d4035-179">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="d4035-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="d4035-180">Veya birden çok iletileri oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="d4035-180">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="d4035-181">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="d4035-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="d4035-182">Node.js çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="d4035-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="d4035-183">Veya birden çok iletileri oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="d4035-183">Or, to create multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d4035-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4035-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

