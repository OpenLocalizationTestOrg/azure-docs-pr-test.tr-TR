---
title: "aaaAzure işlevleri Cosmos DB bağlamaları | Microsoft Docs"
description: "Anlamak nasıl toouse Azure Cosmos DB bağlamaları Azure işlevlerinde."
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
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="465c5-104">Azure işlevleri Cosmos DB bağlamaları</span><span class="sxs-lookup"><span data-stu-id="465c5-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="465c5-105">Bu makalede açıklanır nasıl tooconfigure ve kod Azure Cosmos DB bağlamaları Azure işlevlerinde.</span><span class="sxs-lookup"><span data-stu-id="465c5-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="465c5-106">Giriş ve Cosmos DB bağlantılarında çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="465c5-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="465c5-107">Cosmos DB hakkında daha fazla bilgi için bkz: [giriş tooCosmos DB](../documentdb/documentdb-introduction.md) ve [Cosmos DB konsol uygulaması oluşturma](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="465c5-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="465c5-108">DocumentDB API giriş bağlama</span><span class="sxs-lookup"><span data-stu-id="465c5-108">DocumentDB API input binding</span></span>
<span data-ttu-id="465c5-109">Merhaba DocumentDB API giriş bağlaması Cosmos DB belge alır ve hello işlevinin giriş parametresi adlı toohello geçirir.</span><span class="sxs-lookup"><span data-stu-id="465c5-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="465c5-110">Merhaba belge kimliği belirlenebilir hello işlevi çağırır hello Tetikle temel.</span><span class="sxs-lookup"><span data-stu-id="465c5-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="465c5-111">Merhaba DocumentDB API giriş bağlaması sahip özelliklerinde aşağıdaki hello *function.json*:</span><span class="sxs-lookup"><span data-stu-id="465c5-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="465c5-112">`name`: İşlev kodu hello belge için kullanılan tanımlayıcı adı</span><span class="sxs-lookup"><span data-stu-id="465c5-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="465c5-113">`type`: çok ayarlanması gerekir "documentdb"</span><span class="sxs-lookup"><span data-stu-id="465c5-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="465c5-114">`databaseName`: hello belge içeren hello veritabanı</span><span class="sxs-lookup"><span data-stu-id="465c5-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="465c5-115">`collectionName`: hello belge içeren hello koleksiyon</span><span class="sxs-lookup"><span data-stu-id="465c5-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="465c5-116">`id`: hello belge tooretrieve kimliğini hello.</span><span class="sxs-lookup"><span data-stu-id="465c5-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="465c5-117">Bu özellik bağlamaları parametreleri destekler; bkz: [toocustom giriş özellikleri bağlama ifadesinde bağlamak](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) hello makalede [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="465c5-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="465c5-118">`sqlQuery`Birden çok belge almak için kullanılan Cosmos DB SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="465c5-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="465c5-119">Merhaba query çalışma zamanı bağlamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="465c5-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="465c5-120">Örneğin, `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="465c5-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="465c5-121">`connection`: Cosmos DB bağlantı dizesi içeren hello uygulama ayarı hello adı</span><span class="sxs-lookup"><span data-stu-id="465c5-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="465c5-122">`direction`: çok ayarlanmalıdır`"in"`.</span><span class="sxs-lookup"><span data-stu-id="465c5-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="465c5-123">Merhaba özellikleri `id` ve `sqlQuery` hem de belirtilemez.</span><span class="sxs-lookup"><span data-stu-id="465c5-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="465c5-124">Ne `id` ya da `sqlQuery` , hello tüm ayarlanmış koleksiyonu alınır.</span><span class="sxs-lookup"><span data-stu-id="465c5-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="465c5-125">Bir DocumentDB API giriş bağlama işlemini kullanma</span><span class="sxs-lookup"><span data-stu-id="465c5-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="465c5-126">Merhaba işlevi başarıyla çıktığında, C# ve F # işlevleri toohello giriş belgesi adlandırılmış giriş parametreleri aracılığıyla yapılan tüm değişiklikler otomatik olarak kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="465c5-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="465c5-127">JavaScript işlevleri güncelleştirmeleri otomatik olarak işlevi çıkış duruma getirilmez.</span><span class="sxs-lookup"><span data-stu-id="465c5-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="465c5-128">Bunun yerine, kullanın `context.bindings.<documentName>In` ve `context.bindings.<documentName>Out` toomake güncelleştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="465c5-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="465c5-129">Merhaba bkz [JavaScript örnek](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="465c5-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="465c5-130">Tek belge için giriş örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-130">Input sample for single document</span></span>
<span data-ttu-id="465c5-131">Merhaba aşağıdaki olduğunu varsayalım DocumentDB API hello bağlamasında giriş `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="465c5-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="465c5-132">Bu giriş bağlaması tooupdate hello belgenin metin değeri kullanan hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="465c5-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="465c5-133">C#</span><span class="sxs-lookup"><span data-stu-id="465c5-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="465c5-134">F#</span><span class="sxs-lookup"><span data-stu-id="465c5-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="465c5-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="465c5-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="465c5-136">C# giriş örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="465c5-137">F # giriş örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="465c5-138">Bu örnek gerektiren bir `project.json` hello belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:</span><span class="sxs-lookup"><span data-stu-id="465c5-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="465c5-139">tooadd bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="465c5-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="465c5-140">JavaScript giriş örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="465c5-141">Giriş örneği ile birden çok belge</span><span class="sxs-lookup"><span data-stu-id="465c5-141">Input sample with multiple documents</span></span>

<span data-ttu-id="465c5-142">Bir kuyruk tetikleyici toocustomize hello sorgu parametrelerini kullanarak, bir SQL sorgusu tarafından belirtilen birden çok belge tooretrieve istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="465c5-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="465c5-143">Bu örnekte, bir parametre hello sıra tetikleyici sağlar `departmentId`. Bir kuyruk iletisi, `{ "departmentId" : "Finance" }` hello Finans departmanı için tüm kayıtları döndürür.</span><span class="sxs-lookup"><span data-stu-id="465c5-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="465c5-144">Merhaba aşağıdakileri kullanmak *function.json*:</span><span class="sxs-lookup"><span data-stu-id="465c5-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="465c5-145">Giriş örneği birden çok belge C# ile</span><span class="sxs-lookup"><span data-stu-id="465c5-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="465c5-146">JavaScript içindeki birden çok belge giriş örnekle</span><span class="sxs-lookup"><span data-stu-id="465c5-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="465c5-147"><a id="docdboutput"></a>DocumentDB API bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="465c5-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="465c5-148">Merhaba DocumentDB API bağlama, yeni bir belge tooan Azure Cosmos DB veritabanı yazmanıza olanak veren çıktı.</span><span class="sxs-lookup"><span data-stu-id="465c5-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="465c5-149">Aşağıdaki özelliklere de hello sahip *function.json*:</span><span class="sxs-lookup"><span data-stu-id="465c5-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="465c5-150">`name`: İşlev kodu hello yeni belge için kullanılan tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="465c5-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="465c5-151">`type`: çok ayarlanmalıdır`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="465c5-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="465c5-152">`databaseName`: Burada hello yeni belge oluşturulacak hello koleksiyonu içeren hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="465c5-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="465c5-153">`collectionName`: Merhaba burada hello yeni belge oluşturulacak koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="465c5-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="465c5-154">`createIfNotExists`: Henüz yoksa hello koleksiyon oluşturulur olup olmadığını tooindicate bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="465c5-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="465c5-155">Merhaba varsayılandır *false*.</span><span class="sxs-lookup"><span data-stu-id="465c5-155">hello default is *false*.</span></span> <span data-ttu-id="465c5-156">Merhaba neden bu yeni için koleksiyonları fiyatlandırmaya olan ayrılmış işleme ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="465c5-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="465c5-157">Daha fazla ayrıntı için lütfen başlangıç adresini ziyaret edin [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="465c5-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="465c5-158">`connection`: Cosmos DB bağlantı dizesi içeren hello uygulama ayarı hello adı</span><span class="sxs-lookup"><span data-stu-id="465c5-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="465c5-159">`direction`: çok ayarlanmalıdır`"out"`</span><span class="sxs-lookup"><span data-stu-id="465c5-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="465c5-160">Bir DocumentDB API kullanarak çıktıyı bağlama</span><span class="sxs-lookup"><span data-stu-id="465c5-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="465c5-161">Bu bölümde işlevi kodunuzda bağlama toouse DocumentDB API'nizi nasıl çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="465c5-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="465c5-162">Başlangıç olarak bir otomatik olarak oluşturulan GUID ile yeni bir belge veritabanınızda oluşturulan varsayılan olarak, işlevinde toohello çıktı parametresi yazdığınızda, kimliği belge</span><span class="sxs-lookup"><span data-stu-id="465c5-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="465c5-163">Merhaba belirterek hello belge kimliği çıktı belgenin belirtebilirsiniz `id` hello JSON özelliğinde çıktı parametresi.</span><span class="sxs-lookup"><span data-stu-id="465c5-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="465c5-164">Var olan bir belgeyi hello Kimliğini belirttiğinizde, hello yeni çıkış belge tarafından üzerine.</span><span class="sxs-lookup"><span data-stu-id="465c5-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="465c5-165">toooutput birden çok belge, ayrıca çok bağlayabilirsiniz`ICollector<T>` veya `IAsyncCollector<T>` burada `T` desteklenen hello türlerinden biridir.</span><span class="sxs-lookup"><span data-stu-id="465c5-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="465c5-166">DocumentDB API çıkış bağlama örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="465c5-167">Merhaba aşağıdaki olduğunu varsayalım DocumentDB API hello bağlamasında çıktı `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="465c5-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="465c5-168">Ve JSON biçimini izleyen hello alan sıra için bir sıra giriş bağlama vardır:</span><span class="sxs-lookup"><span data-stu-id="465c5-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="465c5-169">Ve toocreate Cosmos DB hello biçimi her kayıt için aşağıdaki belgelerde istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="465c5-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="465c5-170">Bu çıktı bağlama tooadd belgeleri tooyour veritabanı kullanan hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="465c5-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="465c5-171">C#</span><span class="sxs-lookup"><span data-stu-id="465c5-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="465c5-172">F#</span><span class="sxs-lookup"><span data-stu-id="465c5-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="465c5-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="465c5-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="465c5-174">C# çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="465c5-175">F # çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-175">Output sample in F#</span></span> #

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

<span data-ttu-id="465c5-176">Bu örnek gerektiren bir `project.json` hello belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:</span><span class="sxs-lookup"><span data-stu-id="465c5-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="465c5-177">tooadd bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="465c5-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="465c5-178">JavaScript çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="465c5-178">Output sample in JavaScript</span></span>

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
