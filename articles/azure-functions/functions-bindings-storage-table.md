---
title: "Azure işlevleri depolama tablosu bağlamaları | Microsoft Docs"
description: "Azure Storage bağlamaları Azure işlevlerini kullanmak nasıl anlayın."
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
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="401a4-104">Azure işlevleri depolama tablo bağlamaları</span><span class="sxs-lookup"><span data-stu-id="401a4-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="401a4-105">Bu makalede nasıl yapılandırılacağı ve kod Azure Storage tablo bağlamaları Azure işlevlerinde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="401a4-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="401a4-106">Giriş ve Azure Storage tablolarının bağlantılarında çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="401a4-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="401a4-107">Depolama Tablo Bağlama aşağıdaki senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="401a4-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="401a4-108">**C# veya Node.js işlevi tek bir satırda okuma** - ayarlanmış `partitionKey` ve `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="401a4-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="401a4-109">`filter` Ve `take` özellikleri bu senaryoda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="401a4-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="401a4-110">**C# işlevinde birden çok satır okuma** -işlevler çalışma zamanı sağlayan bir `IQueryable<T>` nesnesi tabloya bağlı.</span><span class="sxs-lookup"><span data-stu-id="401a4-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="401a4-111">Tür `T` öğesinden türetilmelidir `TableEntity` veya uygulayan `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="401a4-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="401a4-112">`partitionKey`, `rowKey`, `filter`, Ve `take` özellikler bu senaryoda kullanılmaz; kullanabilirsiniz `IQueryable` tüm gerekli filtreleme yapmak için nesne.</span><span class="sxs-lookup"><span data-stu-id="401a4-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="401a4-113">**Bir düğüm işlevinde birden çok satır okuma** - ayarlanmış `filter` ve `take` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="401a4-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="401a4-114">Ayarlamazsanız `partitionKey` veya `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="401a4-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="401a4-115">**C# işlevinde bir veya daha fazla satır yazma** -işlevler çalışma zamanı sağlar bir `ICollector<T>` veya `IAsyncCollector<T>` tabloya bağlı olduğu `T` eklemek istediğiniz varlıklar şeması belirtir.</span><span class="sxs-lookup"><span data-stu-id="401a4-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="401a4-116">Genellikle, yazın `T` türetilen `TableEntity` veya uygulayan `ITableEntity`, ancak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="401a4-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="401a4-117">`partitionKey`, `rowKey`, `filter`, Ve `take` özellikleri bu senaryoda kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="401a4-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="401a4-118">Depolama tablo giriş bağlama</span><span class="sxs-lookup"><span data-stu-id="401a4-118">Storage table input binding</span></span>
<span data-ttu-id="401a4-119">Azure Storage tablo giriş bağlama depolama tablosu, işlevinde kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="401a4-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="401a4-120">Bir işlev depolama tablo girişi aşağıdaki JSON nesneleri kullanan `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="401a4-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="401a4-121">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="401a4-121">Note the following:</span></span> 

* <span data-ttu-id="401a4-122">Kullanım `partitionKey` ve `rowKey` birlikte tek bir varlık okunamıyor.</span><span class="sxs-lookup"><span data-stu-id="401a4-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="401a4-123">Bu özellikleri isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="401a4-123">These properties are optional.</span></span> 
* <span data-ttu-id="401a4-124">`connection`Depolama bağlantı dizesi içeren bir uygulama ayarı adı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="401a4-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="401a4-125">Standart Düzenleyici'de Azure portalında **tümleştir** sekmesinde, bir depolama alanı oluşturduğunuzda, hesap ya da mevcut bir seçer için bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="401a4-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="401a4-126">Ayrıca [bu uygulamayı el ile ayarlama yapılandırma](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="401a4-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="401a4-127">Giriş kullanımı</span><span class="sxs-lookup"><span data-stu-id="401a4-127">Input usage</span></span>
<span data-ttu-id="401a4-128">C# işlevlerde, giriş tablosu varlık (veya varlıklar) adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="401a4-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="401a4-129">Burada `T` veri türü, verileri seri durumdan istediğiniz olduğunda ve `paramName` , belirtilen adı [bağlama giriş](#input).</span><span class="sxs-lookup"><span data-stu-id="401a4-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="401a4-130">Node.js işlevlerde kullanarak giriş tablosu varlık (veya varlıklar) erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="401a4-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="401a4-131">Giriş verisi Node.js veya C# işlevlerde serisi.</span><span class="sxs-lookup"><span data-stu-id="401a4-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="401a4-132">Seri durumdan çıkarılmış nesneler sahip `RowKey` ve `PartitionKey` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="401a4-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="401a4-133">C# işlevleri, şu türlerden birine de bağlayabilirsiniz ve işlevleri çalışma zamanı türü kullanarak tablo verileri seri durumdan dener:</span><span class="sxs-lookup"><span data-stu-id="401a4-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="401a4-134">Uygulayan herhangi bir türü`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="401a4-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="401a4-135">Giriş örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-135">Input sample</span></span>
<span data-ttu-id="401a4-136">Tek bir tablo satırı okumak için bir sıra tetikleyici kullanır aşağıdaki function.json sahip olması.</span><span class="sxs-lookup"><span data-stu-id="401a4-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="401a4-137">JSON belirtir `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="401a4-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="401a4-138">`"rowKey": "{queueTrigger}"`Satır anahtarını kuyruk iletisi dizeden geldiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="401a4-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

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

<span data-ttu-id="401a4-139">Tek tablo varlığı okur dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="401a4-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="401a4-140">C#</span><span class="sxs-lookup"><span data-stu-id="401a4-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="401a4-141">F#</span><span class="sxs-lookup"><span data-stu-id="401a4-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="401a4-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="401a4-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="401a4-143">C# giriş örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="401a4-144">F # giriş örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="401a4-145">Node.js giriş örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="401a4-146">Bağlama depolama tablo çıktısı</span><span class="sxs-lookup"><span data-stu-id="401a4-146">Storage table output binding</span></span>
<span data-ttu-id="401a4-147">Etkinleştirir bağlama Azure Storage tablo çıktısı, varlıklar bir depolama alanına yazmak için işlevinde tablo.</span><span class="sxs-lookup"><span data-stu-id="401a4-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="401a4-148">Bir işlev aşağıdaki JSON nesneleri kullanan çıktısı depolama tablosu `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="401a4-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="401a4-149">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="401a4-149">Note the following:</span></span> 

* <span data-ttu-id="401a4-150">Kullanım `partitionKey` ve `rowKey` birlikte tek bir varlık yazmak için.</span><span class="sxs-lookup"><span data-stu-id="401a4-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="401a4-151">Bu özellikleri isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="401a4-151">These properties are optional.</span></span> <span data-ttu-id="401a4-152">Ayrıca belirtebilirsiniz `PartitionKey` ve `RowKey` işlevi kodunuzda varlık nesnesi oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="401a4-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="401a4-153">`connection`Depolama bağlantı dizesi içeren bir uygulama ayarı adı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="401a4-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="401a4-154">Standart Düzenleyici'de Azure portalında **tümleştir** sekmesinde, bir depolama alanı oluşturduğunuzda, hesap ya da mevcut bir seçer için bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="401a4-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="401a4-155">Ayrıca [bu uygulamayı el ile ayarlama yapılandırma](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="401a4-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="401a4-156">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="401a4-156">Output usage</span></span>
<span data-ttu-id="401a4-157">C# İşlevler, tablo çıktısı adlandırılmış kullanarak bağladığınız `out` işlevi imzanız parametresinde ister `out <T> <name>`, burada `T` veri türü, verileri seri hale getirmek istediğiniz olduğunda ve `paramName` , belirtilen adı [bağlama çıktı](#output).</span><span class="sxs-lookup"><span data-stu-id="401a4-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="401a4-158">Node.js işlevlerde kullanarak çıktıyı tabloya erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="401a4-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="401a4-159">Node.js veya C# işlevleri nesneleri seri hale getirebilir.</span><span class="sxs-lookup"><span data-stu-id="401a4-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="401a4-160">C# işlevlerde, aşağıdaki türlerine bağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="401a4-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="401a4-161">Uygulayan herhangi bir türü`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="401a4-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="401a4-162">`ICollector<T>`(birden çok varlık çıkarmak için.</span><span class="sxs-lookup"><span data-stu-id="401a4-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="401a4-163">Bkz: [örnek](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="401a4-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="401a4-164">`IAsyncCollector<T>`(zaman uyumsuz sürümü `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="401a4-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="401a4-165">`CloudTable`(Azure depolama SDK'sını kullanma.</span><span class="sxs-lookup"><span data-stu-id="401a4-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="401a4-166">Bkz: [örnek](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="401a4-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="401a4-167">Çıkış örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-167">Output sample</span></span>
<span data-ttu-id="401a4-168">Aşağıdaki *function.json* ve *run.csx* örnek nasıl birden çok tablo varlıkları yazılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="401a4-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

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

<span data-ttu-id="401a4-169">Birden çok tablo varlıkları oluşturur dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="401a4-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="401a4-170">C#</span><span class="sxs-lookup"><span data-stu-id="401a4-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="401a4-171">F#</span><span class="sxs-lookup"><span data-stu-id="401a4-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="401a4-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="401a4-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="401a4-173">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="401a4-174">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="401a4-175">Node.js çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="401a4-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="401a4-176">Örnek: C# birden çok tablo varlıkları okuma</span><span class="sxs-lookup"><span data-stu-id="401a4-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="401a4-177">Aşağıdaki *function.json* ve C# kod örneği sıra iletide belirtilen bir bölüm anahtarı için varlıklar okur.</span><span class="sxs-lookup"><span data-stu-id="401a4-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

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

<span data-ttu-id="401a4-178">C# kodu, Azure depolama SDK'sına bir başvuru ekler, böylece varlık türü öğesinden türetilen `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="401a4-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="401a4-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="401a4-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

