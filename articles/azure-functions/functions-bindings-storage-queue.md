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
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="34004-104">Azure işlevleri kuyruk depolama bağlamaları</span><span class="sxs-lookup"><span data-stu-id="34004-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="34004-105">Bu makalede nasıl tooconfigure ve kod Azure kuyruk depolama bağlamaları Azure işlevlerinde.</span><span class="sxs-lookup"><span data-stu-id="34004-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="34004-106">Tetikler ve Azure sıralar bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="34004-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="34004-107">Tüm bağlama kullanılabilir olan özellikler için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="34004-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="34004-108">Kuyruk depolama tetikleyici</span><span class="sxs-lookup"><span data-stu-id="34004-108">Queue storage trigger</span></span>
<span data-ttu-id="34004-109">Hello Azure kuyruk depolama tetikleyici toothem tepki vermek ve yeni iletiler için bir kuyruk depolama toomonitor sağlar.</span><span class="sxs-lookup"><span data-stu-id="34004-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="34004-110">Hello kullanarak bir sıra tetikleyici tanımlamak **tümleştir** hello işlevleri portalındaki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="34004-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="34004-111">Merhaba portal oluşturur hello tanımında aşağıdaki hello **bağlamaları** bölümünü *function.json*:</span><span class="sxs-lookup"><span data-stu-id="34004-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="34004-112">Merhaba `connection` özelliği, depolama bağlantı dizesi içeren bir uygulama ayarı hello adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="34004-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="34004-113">Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde bir depolama hesabı seçtiğinizde, bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="34004-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="34004-114">Ek ayarları sağlanabilir bir [host.json dosya](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ince ayar kuyruk depolama tetikler.</span><span class="sxs-lookup"><span data-stu-id="34004-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="34004-115">Örneğin, host.json hello sıra yoklama aralığını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34004-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="34004-116">Bir kuyruk Tetikleyici kullanma</span><span class="sxs-lookup"><span data-stu-id="34004-116">Using a queue trigger</span></span>
<span data-ttu-id="34004-117">Node.js işlevlerde hello sıra verileri kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="34004-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="34004-118">.NET işlevlerde hello sıra yükü gibi bir yöntem parametresi kullanılarak erişim `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="34004-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="34004-119">Burada, `paramName` hello belirtilen hello değeri [tetikleyici yapılandırma](#trigger).</span><span class="sxs-lookup"><span data-stu-id="34004-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="34004-120">Hello kuyruk iletisi seri durumdan çıkarılmış tooany şu türlerini hello biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="34004-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="34004-121">POCO nesnesi.</span><span class="sxs-lookup"><span data-stu-id="34004-121">POCO object.</span></span> <span data-ttu-id="34004-122">Merhaba kuyruk yükü bir JSON nesnesi ise kullanın.</span><span class="sxs-lookup"><span data-stu-id="34004-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="34004-123">Merhaba işlevleri çalışma zamanı hello yükü hello POCO nesnesine seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="34004-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="34004-124">Sıra tetikleyici meta verileri</span><span class="sxs-lookup"><span data-stu-id="34004-124">Queue trigger metadata</span></span>
<span data-ttu-id="34004-125">Merhaba sıra tetikleyici çeşitli meta veri özelliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="34004-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="34004-126">Bu özellikler, diğer bağlamaları bağlama ifadelerinde bir parçası olarak ya da kodunuzu parametre olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="34004-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="34004-127">Merhaba değerlere sahip hello aynı topluca [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="34004-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="34004-128">**QueueTrigger** -sıra Yükü (geçerli bir dize ise)</span><span class="sxs-lookup"><span data-stu-id="34004-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="34004-129">**DequeueCount** -türü `int`.</span><span class="sxs-lookup"><span data-stu-id="34004-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="34004-130">Bu iletiyi kuyruktan çıkarıldı sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="34004-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="34004-131">**ExpirationTime** -türü `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="34004-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="34004-132">Başlangıç saati, selamlama iletisine süresi dolar.</span><span class="sxs-lookup"><span data-stu-id="34004-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="34004-133">**Kimliği** -türü `string`.</span><span class="sxs-lookup"><span data-stu-id="34004-133">**Id** - Type `string`.</span></span> <span data-ttu-id="34004-134">Sıra ileti kimliği.</span><span class="sxs-lookup"><span data-stu-id="34004-134">Queue message ID.</span></span>
* <span data-ttu-id="34004-135">**InsertionTime** -türü `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="34004-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="34004-136">Başlangıç saati, selamlama iletisine toohello sıraya eklendi.</span><span class="sxs-lookup"><span data-stu-id="34004-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="34004-137">**NextVisibleTime** -türü `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="34004-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="34004-138">Başlangıç saati, selamlama iletisine sonraki görünür olur.</span><span class="sxs-lookup"><span data-stu-id="34004-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="34004-139">**PopReceipt** -türü `string`.</span><span class="sxs-lookup"><span data-stu-id="34004-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="34004-140">Merhaba ileti pop giriş.</span><span class="sxs-lookup"><span data-stu-id="34004-140">hello message's pop receipt.</span></span>

<span data-ttu-id="34004-141">Nasıl toouse hello sıra meta verilerde bkz [tetikleyici örnek](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="34004-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="34004-142">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="34004-142">Trigger sample</span></span>
<span data-ttu-id="34004-143">Bir kuyruk tetikleyici tanımlar function.json aşağıdaki hello olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="34004-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="34004-144">Alan ve sıra meta veri günlüklerini hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="34004-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="34004-145">C#</span><span class="sxs-lookup"><span data-stu-id="34004-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="34004-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="34004-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="34004-147">Tetikleyici örnek C#</span><span class="sxs-lookup"><span data-stu-id="34004-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="34004-148">Node.js tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="34004-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="34004-149">Zarar iletileri işleme</span><span class="sxs-lookup"><span data-stu-id="34004-149">Handling poison queue messages</span></span>
<span data-ttu-id="34004-150">Bir kuyruk Tetik işlevi başarısız olduğunda, Azure işlevleri hello ilk içeren verilen kuyruk iletisi saatlere deneyin toofive bu işlevini yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="34004-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="34004-151">Tüm beş deneme başarısız olursa hello işlevleri çalışma zamanı adlı bir ileti tooa kuyruk depolama ekler  *&lt;originalqueuename >-zararlı*.</span><span class="sxs-lookup"><span data-stu-id="34004-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="34004-152">Bir işlev tooprocess iletileri hello zararlı sıradan günlüğe yazma veya el ile ilgilenilmesi gereken bir bildirim göndererek yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34004-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="34004-153">toohandle zarar iletileri el ile denetleyin hello `dequeueCount` hello kuyruk iletisinin (bkz [sıra tetikleyici meta verileri](#meta)).</span><span class="sxs-lookup"><span data-stu-id="34004-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="34004-154">Kuyruk depolama bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="34004-154">Queue storage output binding</span></span>
<span data-ttu-id="34004-155">Hello Azure kuyruk depolama bağlama toowrite iletileri tooa sırası etkinleştirir çıktı.</span><span class="sxs-lookup"><span data-stu-id="34004-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="34004-156">Bir sırayı tanımlayan hello kullanarak çıktı bağlama **tümleştir** hello işlevleri portalındaki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="34004-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="34004-157">Merhaba portal oluşturur hello tanımında aşağıdaki hello **bağlamaları** bölümünü *function.json*:</span><span class="sxs-lookup"><span data-stu-id="34004-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="34004-158">Merhaba `connection` özelliği, depolama bağlantı dizesi içeren bir uygulama ayarı hello adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="34004-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="34004-159">Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde bir depolama hesabı seçtiğinizde, bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="34004-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="34004-160">Bir kuyruk kullanarak çıktıyı bağlama</span><span class="sxs-lookup"><span data-stu-id="34004-160">Using a queue output binding</span></span>
<span data-ttu-id="34004-161">Node.js işlevlerde hello çıkış sırası kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="34004-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="34004-162">.NET işlevlerde şu türlerini hello tooany çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34004-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="34004-163">Tür parametresi olduğunda `T`, `T` desteklenen hello çıkış türlerinden birini gibi olmalıdır `string` veya bir POCO.</span><span class="sxs-lookup"><span data-stu-id="34004-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="34004-164">`out T`(JSON olarak serileştirilmiş)</span><span class="sxs-lookup"><span data-stu-id="34004-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="34004-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="34004-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="34004-166">Merhaba yönteminin dönüş türü hello kullanabilirsiniz bağlama çıktı.</span><span class="sxs-lookup"><span data-stu-id="34004-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="34004-167">Sıra çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="34004-167">Queue output sample</span></span>
<span data-ttu-id="34004-168">Merhaba aşağıdaki *function.json* bir HTTP tetikleyicisi bir sıra ile tanımlar bağlama çıktı:</span><span class="sxs-lookup"><span data-stu-id="34004-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="34004-169">Bir kuyruk iletisi hello gelen HTTP yükü ile çıkarır hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="34004-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="34004-170">C#</span><span class="sxs-lookup"><span data-stu-id="34004-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="34004-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="34004-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="34004-172">C# sıra çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="34004-172">Queue output sample in C#</span></span> #

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

<span data-ttu-id="34004-173">birden çok iletileri toosend kullanan bir `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="34004-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="34004-174">Node.js sıra çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="34004-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="34004-175">Veya, toosend birden fazla ileti</span><span class="sxs-lookup"><span data-stu-id="34004-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="34004-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34004-176">Next steps</span></span>

<span data-ttu-id="34004-177">Kuyruk depolama Tetikleyicileri ve bağlamaları kullanan bir işlev örneği için bkz: [Azure bağlı işlevi tooan Azure hizmeti oluşturma](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="34004-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

['CloudQueueMessage']: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
