---
title: "Azure işlevleri Cosmos DB bağlamaları | Microsoft Docs"
description: "Azure işlevleri Azure Cosmos DB bağlamaları kullanmayı öğrenme."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="04b62-104">Azure işlevleri Cosmos DB bağlamaları</span><span class="sxs-lookup"><span data-stu-id="04b62-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="04b62-105">Bu makalede nasıl yapılandırılacağı ve kod Azure Cosmos DB bağlamaları Azure işlevlerinde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="04b62-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="04b62-106">Giriş ve Cosmos DB bağlantılarında çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="04b62-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="04b62-107">Cosmos DB hakkında daha fazla bilgi için bkz: [Cosmos DB giriş](../documentdb/documentdb-introduction.md) ve [Cosmos DB konsol uygulaması oluşturma](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04b62-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="04b62-108">DocumentDB API giriş bağlama</span><span class="sxs-lookup"><span data-stu-id="04b62-108">DocumentDB API input binding</span></span>
<span data-ttu-id="04b62-109">DocumentDB API giriş bağlaması Cosmos DB belge alır ve işlev adlandırılmış giriş parametresi olarak geçirir.</span><span class="sxs-lookup"><span data-stu-id="04b62-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="04b62-110">Kimliği belirlenebilir belge işlevi çağırır Tetikle temel.</span><span class="sxs-lookup"><span data-stu-id="04b62-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="04b62-111">DocumentDB API giriş bağlaması aşağıdaki özelliklere sahip *function.json*:</span><span class="sxs-lookup"><span data-stu-id="04b62-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="04b62-112">`name`: İşlev kodu ve belge için kullanılan tanımlayıcı adı</span><span class="sxs-lookup"><span data-stu-id="04b62-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="04b62-113">`type`: "documentdb" olarak ayarlanmalıdır</span><span class="sxs-lookup"><span data-stu-id="04b62-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="04b62-114">`databaseName`: Belge içeren veritabanı</span><span class="sxs-lookup"><span data-stu-id="04b62-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="04b62-115">`collectionName`: Belge içeren bir koleksiyon</span><span class="sxs-lookup"><span data-stu-id="04b62-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="04b62-116">`id`: Alınacak kimliği belge.</span><span class="sxs-lookup"><span data-stu-id="04b62-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="04b62-117">Bu özellik bağlamaları parametreleri destekler; bkz: [bir bağlama ifadesinde özel giriş özellikleri bağlamak](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) makalede [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="04b62-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="04b62-118">`sqlQuery`Birden çok belge almak için kullanılan Cosmos DB SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="04b62-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="04b62-119">Sorgu, çalışma zamanı bağlamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="04b62-119">The query supports runtime bindings.</span></span> <span data-ttu-id="04b62-120">Örneğin, `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="04b62-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="04b62-121">`connection`: Cosmos DB bağlantı dizesi içeren uygulama ayarı adı</span><span class="sxs-lookup"><span data-stu-id="04b62-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="04b62-122">`direction`: ayarlanmalıdır `"in"`.</span><span class="sxs-lookup"><span data-stu-id="04b62-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="04b62-123">Özellikler `id` ve `sqlQuery` hem de belirtilemez.</span><span class="sxs-lookup"><span data-stu-id="04b62-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="04b62-124">Ne `id` ya da `sqlQuery` , tüm koleksiyon alınır ayarlanmadı.</span><span class="sxs-lookup"><span data-stu-id="04b62-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="04b62-125">Bir DocumentDB API giriş bağlama işlemini kullanma</span><span class="sxs-lookup"><span data-stu-id="04b62-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="04b62-126">İşlev başarıyla çıktığında, C# ve F # işlevleri adlandırılmış giriş parametreleri aracılığıyla giriş belgeye yapılan değişiklikler otomatik olarak kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="04b62-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="04b62-127">JavaScript işlevleri güncelleştirmeleri otomatik olarak işlevi çıkış duruma getirilmez.</span><span class="sxs-lookup"><span data-stu-id="04b62-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="04b62-128">Bunun yerine, kullanın `context.bindings.<documentName>In` ve `context.bindings.<documentName>Out` güncelleştirme yapmak için.</span><span class="sxs-lookup"><span data-stu-id="04b62-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="04b62-129">Bkz: [JavaScript örnek](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="04b62-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="04b62-130">Tek belge için giriş örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-130">Input sample for single document</span></span>
<span data-ttu-id="04b62-131">Aşağıdaki olduğunu varsayalım DocumentDB API bağlamasında giriş `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="04b62-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

<span data-ttu-id="04b62-132">Belgenin metin değeri güncelleştirmek için bu giriş bağlama kullanır dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="04b62-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="04b62-133">C#</span><span class="sxs-lookup"><span data-stu-id="04b62-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="04b62-134">F#</span><span class="sxs-lookup"><span data-stu-id="04b62-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="04b62-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="04b62-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="04b62-136">C# giriş örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="04b62-137">F # giriş örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="04b62-138">Bu örnek gerektiren bir `project.json` belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:</span><span class="sxs-lookup"><span data-stu-id="04b62-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="04b62-139">Eklemek için bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="04b62-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="04b62-140">JavaScript giriş örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="04b62-141">Giriş örneği ile birden çok belge</span><span class="sxs-lookup"><span data-stu-id="04b62-141">Input sample with multiple documents</span></span>

<span data-ttu-id="04b62-142">Bir SQL sorgusu tarafından belirtilen birden çok belge almak sorgu parametrelerini özelleştirmek için bir sıra tetikleyici kullanarak istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="04b62-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="04b62-143">Bu örnekte, bir parametre sırası tetikleyici sağlar `departmentId`. Bir kuyruk iletisi, `{ "departmentId" : "Finance" }` Finans departmanı için tüm kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="04b62-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="04b62-144">Aşağıda, kullanmak *function.json*:</span><span class="sxs-lookup"><span data-stu-id="04b62-144">Use the following in *function.json*:</span></span>

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="04b62-145">Giriş örneği birden çok belge C# ile</span><span class="sxs-lookup"><span data-stu-id="04b62-145">Input sample with multiple documents in C#</span></span>

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="04b62-146">JavaScript içindeki birden çok belge giriş örnekle</span><span class="sxs-lookup"><span data-stu-id="04b62-146">Input sample with multiple documents in JavaScript</span></span>

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <span data-ttu-id="04b62-147"><a id="docdboutput"></a>DocumentDB API bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="04b62-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="04b62-148">Sağlar bağlama DocumentDB API çıktı yeni bir belge bir Azure Cosmos DB veritabanına yazar.</span><span class="sxs-lookup"><span data-stu-id="04b62-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="04b62-149">Aşağıdaki özelliklere sahip *function.json*:</span><span class="sxs-lookup"><span data-stu-id="04b62-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="04b62-150">`name`: İşlev kodu yeni belge için kullanılan tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="04b62-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="04b62-151">`type`: ayarlanmalıdır`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="04b62-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="04b62-152">`databaseName`: Yeni belge oluşturulacağı koleksiyonu içeren veritabanı.</span><span class="sxs-lookup"><span data-stu-id="04b62-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="04b62-153">`collectionName`: Yeni belge oluşturulacağı koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="04b62-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="04b62-154">`createIfNotExists`: Henüz yoksa koleksiyonu oluşturduğunuzda olup olmadığını belirtmek için bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="04b62-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="04b62-155">Varsayılan değer *false*.</span><span class="sxs-lookup"><span data-stu-id="04b62-155">The default is *false*.</span></span> <span data-ttu-id="04b62-156">Neden bu yeni için koleksiyonları fiyatlandırmaya olan ayrılmış işleme ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="04b62-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="04b62-157">Daha fazla ayrıntı için lütfen ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="04b62-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="04b62-158">`connection`: Cosmos DB bağlantı dizesi içeren uygulama ayarı adı</span><span class="sxs-lookup"><span data-stu-id="04b62-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="04b62-159">`direction`: ayarlanmalıdır`"out"`</span><span class="sxs-lookup"><span data-stu-id="04b62-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="04b62-160">Bir DocumentDB API kullanarak çıktıyı bağlama</span><span class="sxs-lookup"><span data-stu-id="04b62-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="04b62-161">Bu bölümde işlevi kodunuzda bağlama, DocumentDB API çıkış kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="04b62-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="04b62-162">Çıktı parametresi, işlev yazdığınızda, varsayılan olarak yeni bir belge belge kimliği olarak bir otomatik olarak oluşturulan GUID ile veritabanınızda oluşturulur</span><span class="sxs-lookup"><span data-stu-id="04b62-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="04b62-163">Çıktı belgenin belge kimliği belirterek belirtebilirsiniz `id` çıkış parametresi bir JSON özellik.</span><span class="sxs-lookup"><span data-stu-id="04b62-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="04b62-164">Var olan bir belgeyi Kimliğini belirttiğinizde, yeni çıktı belgenin üzerine.</span><span class="sxs-lookup"><span data-stu-id="04b62-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="04b62-165">Birden çok belge çıktısını almak için de bağlayabilirsiniz `ICollector<T>` veya `IAsyncCollector<T>` burada `T` desteklenen türlerden biri.</span><span class="sxs-lookup"><span data-stu-id="04b62-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="04b62-166">DocumentDB API çıkış bağlama örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="04b62-167">Aşağıdaki olduğunu varsayalım DocumentDB API bağlamasında çıktı `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="04b62-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

<span data-ttu-id="04b62-168">Ve şu biçimde JSON alan sıra için bir sıra giriş bağlama sahip:</span><span class="sxs-lookup"><span data-stu-id="04b62-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="04b62-169">Ve her kayıt için şu biçimde Cosmos DB belgeleri oluşturmak isterseniz:</span><span class="sxs-lookup"><span data-stu-id="04b62-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="04b62-170">Belgeler, veritabanına eklemek için bu çıktı bağlama kullanan dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="04b62-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="04b62-171">C#</span><span class="sxs-lookup"><span data-stu-id="04b62-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="04b62-172">F#</span><span class="sxs-lookup"><span data-stu-id="04b62-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="04b62-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="04b62-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="04b62-174">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-174">Output sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="04b62-175">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-175">Output sample in F#</span></span> #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

<span data-ttu-id="04b62-176">Bu örnek gerektiren bir `project.json` belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:</span><span class="sxs-lookup"><span data-stu-id="04b62-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="04b62-177">Eklemek için bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="04b62-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="04b62-178">JavaScript çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="04b62-178">Output sample in JavaScript</span></span>

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
