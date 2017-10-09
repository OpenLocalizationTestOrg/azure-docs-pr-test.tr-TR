---
title: "aaaAzure işlevleri depolama tablosu bağlamaları | Microsoft Docs"
description: "Anlamak nasıl toouse Azure Storage bağlamaları Azure işlevlerinde."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="07696-104">Azure işlevleri depolama tablo bağlamaları</span><span class="sxs-lookup"><span data-stu-id="07696-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="07696-105">Bu makalede nasıl tooconfigure kodu Azure Storage Azure işlevlerinde bağlamaları tablo ve açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="07696-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="07696-106">Giriş ve Azure Storage tablolarının bağlantılarında çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="07696-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="07696-107">Merhaba depolama Tablo Bağlama hello aşağıdaki senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="07696-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="07696-108">**C# veya Node.js işlevi tek bir satırda okuma** - ayarlanmış `partitionKey` ve `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="07696-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="07696-109">Merhaba `filter` ve `take` özellikleri bu senaryoda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="07696-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="07696-110">**C# işlevinde birden çok satır okuma** -hello işlevleri çalışma zamanı sağlayan bir `IQueryable<T>` nesnesi bağlı toohello tablo.</span><span class="sxs-lookup"><span data-stu-id="07696-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="07696-111">Tür `T` öğesinden türetilmelidir `TableEntity` veya uygulayan `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="07696-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="07696-112">Merhaba `partitionKey`, `rowKey`, `filter`, ve `take` özellikler bu senaryoda kullanılmaz; hello kullanabilirsiniz `IQueryable` tüm gerekli filtreleme toodo nesne.</span><span class="sxs-lookup"><span data-stu-id="07696-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="07696-113">**Bir düğüm işlevinde birden çok satır okuma** - ayarlanmış hello `filter` ve `take` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="07696-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="07696-114">Ayarlamazsanız `partitionKey` veya `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="07696-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="07696-115">**C# işlevinde bir veya daha fazla satır yazma** -hello işlevleri çalışma zamanı sağlar bir `ICollector<T>` veya `IAsyncCollector<T>` ilişkili toohello tablo nerede `T` hello şema belirtir hello varlıklarının tooadd istiyor.</span><span class="sxs-lookup"><span data-stu-id="07696-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="07696-116">Genellikle, yazın `T` türetilen `TableEntity` veya uygulayan `ITableEntity`, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="07696-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="07696-117">Merhaba `partitionKey`, `rowKey`, `filter`, ve `take` özellikleri bu senaryoda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="07696-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="07696-118">Depolama tablo giriş bağlama</span><span class="sxs-lookup"><span data-stu-id="07696-118">Storage table input binding</span></span>
<span data-ttu-id="07696-119">Hello Azure Storage tablo giriş bağlama toouse işlevinizi depolama tabloda sağlar.</span><span class="sxs-lookup"><span data-stu-id="07696-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="07696-120">Merhaba depolama tablo giriş tooa işlevini kullanır hello JSON nesneler şu hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="07696-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="07696-121">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="07696-121">Note hello following:</span></span> 

* <span data-ttu-id="07696-122">Kullanım `partitionKey` ve `rowKey` birlikte tooread tek bir varlık.</span><span class="sxs-lookup"><span data-stu-id="07696-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="07696-123">Bu özellikleri isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="07696-123">These properties are optional.</span></span> 
* <span data-ttu-id="07696-124">`connection`Depolama bağlantı dizesi içeren bir uygulama ayarı Hello adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="07696-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="07696-125">Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde, bir depolama alanı oluşturduğunuzda, hesap ya da mevcut bir seçer için bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="07696-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="07696-126">Ayrıca [bu uygulamayı el ile ayarlama yapılandırma](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="07696-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="07696-127">Giriş kullanımı</span><span class="sxs-lookup"><span data-stu-id="07696-127">Input usage</span></span>
<span data-ttu-id="07696-128">C# işlevlerde, toohello giriş tablosu varlık (veya varlıklar) adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="07696-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="07696-129">Burada `T` hello veri türü toodeserialize hello verilerini, istediğiniz olduğunda ve `paramName` hello belirtilen hello adı [bağlama giriş](#input).</span><span class="sxs-lookup"><span data-stu-id="07696-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="07696-130">Node.js işlevlerde hello giriş tablosu varlık (veya varlıklar) kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="07696-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="07696-131">Node.js veya C# işlevlerde Hello giriş verileri seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="07696-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="07696-132">seri durumdan hello nesneler sahip `RowKey` ve `PartitionKey` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="07696-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="07696-133">C# işlevleri, şu türlerini hello tooany de bağlayabilirsiniz ve çalışma zamanı deneyecek hello işlevleri çok hello tablo veri türü kullanılarak seri durumdan:</span><span class="sxs-lookup"><span data-stu-id="07696-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="07696-134">Uygulayan herhangi bir türü`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="07696-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="07696-135">Giriş örneği</span><span class="sxs-lookup"><span data-stu-id="07696-135">Input sample</span></span>
<span data-ttu-id="07696-136">Bir kuyruk tetikleyici tooread tek bir tablo satırı kullanan function.json aşağıdaki hello sahip olması.</span><span class="sxs-lookup"><span data-stu-id="07696-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="07696-137">Merhaba JSON belirtir `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="07696-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="07696-138">`"rowKey": "{queueTrigger}"`Bu hello satır anahtarını hello kuyruk iletisi dizeden gelen gösterir.</span><span class="sxs-lookup"><span data-stu-id="07696-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="07696-139">Tek tablo varlığı okur hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="07696-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="07696-140">C#</span><span class="sxs-lookup"><span data-stu-id="07696-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="07696-141">F#</span><span class="sxs-lookup"><span data-stu-id="07696-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="07696-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="07696-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="07696-143">C# giriş örneği</span><span class="sxs-lookup"><span data-stu-id="07696-143">Input sample in C#</span></span> #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="07696-144">F # giriş örneği</span><span class="sxs-lookup"><span data-stu-id="07696-144">Input sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="07696-145">Node.js giriş örneği</span><span class="sxs-lookup"><span data-stu-id="07696-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="07696-146">Bağlama depolama tablo çıktısı</span><span class="sxs-lookup"><span data-stu-id="07696-146">Storage table output binding</span></span>
<span data-ttu-id="07696-147">Hello Azure depolama tablosu bağlama toowrite varlıklar tooa depolama işlevinizi tabloda etkinleştirir çıktı.</span><span class="sxs-lookup"><span data-stu-id="07696-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="07696-148">bir işlev hello JSON nesneler şu hello kullanan depolama tablo çıktısı hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="07696-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="07696-149">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="07696-149">Note hello following:</span></span> 

* <span data-ttu-id="07696-150">Kullanım `partitionKey` ve `rowKey` birlikte toowrite tek bir varlık.</span><span class="sxs-lookup"><span data-stu-id="07696-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="07696-151">Bu özellikleri isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="07696-151">These properties are optional.</span></span> <span data-ttu-id="07696-152">Ayrıca belirtebilirsiniz `PartitionKey` ve `RowKey` oluşturduğunuzda hello varlık nesnesi işlevi kodunuzda.</span><span class="sxs-lookup"><span data-stu-id="07696-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="07696-153">`connection`Depolama bağlantı dizesi içeren bir uygulama ayarı Hello adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="07696-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="07696-154">Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde, bir depolama alanı oluşturduğunuzda, hesap ya da mevcut bir seçer için bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="07696-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="07696-155">Ayrıca [bu uygulamayı el ile ayarlama yapılandırma](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="07696-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="07696-156">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="07696-156">Output usage</span></span>
<span data-ttu-id="07696-157">C# işlevlerde, toohello tablo çıktısı adlı hello kullanarak bağladığınız `out` işlevi imzanız parametresinde ister `out <T> <name>`, burada `T` hello veri türü tooserialize hello verilerini, istediğiniz olduğunda ve `paramName` olduğu hello adı, Hello belirtilen [bağlama çıktı](#output).</span><span class="sxs-lookup"><span data-stu-id="07696-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="07696-158">Node.js işlevlerde kullanarak çıktıyı hello tablo erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="07696-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="07696-159">Node.js veya C# işlevleri nesneleri seri hale getirebilir.</span><span class="sxs-lookup"><span data-stu-id="07696-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="07696-160">C# işlevlerde, şu türlerini toohello bağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="07696-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="07696-161">Uygulayan herhangi bir türü`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="07696-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="07696-162">`ICollector<T>`(toooutput birden çok varlık.</span><span class="sxs-lookup"><span data-stu-id="07696-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="07696-163">Bkz: [örnek](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="07696-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="07696-164">`IAsyncCollector<T>`(zaman uyumsuz sürümü `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="07696-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="07696-165">`CloudTable`(hello Azure depolama SDK'sını kullanma.</span><span class="sxs-lookup"><span data-stu-id="07696-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="07696-166">Bkz: [örnek](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="07696-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="07696-167">Çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="07696-167">Output sample</span></span>
<span data-ttu-id="07696-168">Merhaba aşağıdaki *function.json* ve *run.csx* örnekteki nasıl toowrite birden çok tablo varlık.</span><span class="sxs-lookup"><span data-stu-id="07696-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="07696-169">Birden çok tablo varlıkları oluşturur hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="07696-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="07696-170">C#</span><span class="sxs-lookup"><span data-stu-id="07696-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="07696-171">F#</span><span class="sxs-lookup"><span data-stu-id="07696-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="07696-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="07696-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="07696-173">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="07696-173">Output sample in C#</span></span> #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="07696-174">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="07696-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="07696-175">Node.js çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="07696-175">Output sample in Node.js</span></span>
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="07696-176">Örnek: C# birden çok tablo varlıkları okuma</span><span class="sxs-lookup"><span data-stu-id="07696-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="07696-177">Merhaba aşağıdaki *function.json* ve C# kod örneğinde varlıklar hello kuyruk iletisi içinde belirtilen bir bölüm anahtarı için okur.</span><span class="sxs-lookup"><span data-stu-id="07696-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="07696-178">Böylece hello varlık türü öğesinden türetilen Hello C# kodu ekler başvuru toohello Azure depolama SDK'sı `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="07696-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="07696-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07696-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

