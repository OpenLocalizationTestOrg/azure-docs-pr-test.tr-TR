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
# <a name="azure-functions-cosmos-db-bindings"></a>Azure işlevleri Cosmos DB bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede nasıl yapılandırılacağı ve kod Azure Cosmos DB bağlamaları Azure işlevlerinde açıklanmaktadır. Giriş ve Cosmos DB bağlantılarında çıktı Azure işlevleri destekler.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Cosmos DB hakkında daha fazla bilgi için bkz: [Cosmos DB giriş](../documentdb/documentdb-introduction.md) ve [Cosmos DB konsol uygulaması oluşturma](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>DocumentDB API giriş bağlama
DocumentDB API giriş bağlaması Cosmos DB belge alır ve işlev adlandırılmış giriş parametresi olarak geçirir. Kimliği belirlenebilir belge işlevi çağırır Tetikle temel. 

DocumentDB API giriş bağlaması aşağıdaki özelliklere sahip *function.json*:

- `name`: İşlev kodu ve belge için kullanılan tanımlayıcı adı
- `type`: "documentdb" olarak ayarlanmalıdır
- `databaseName`: Belge içeren veritabanı
- `collectionName`: Belge içeren bir koleksiyon
- `id`: Alınacak kimliği belge. Bu özellik bağlamaları parametreleri destekler; bkz: [bir bağlama ifadesinde özel giriş özellikleri bağlamak](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) makalede [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).
- `sqlQuery`Birden çok belge almak için kullanılan Cosmos DB SQL sorgusu. Sorgu, çalışma zamanı bağlamaları destekler. Örneğin, `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: Cosmos DB bağlantı dizesi içeren uygulama ayarı adı
- `direction`: ayarlanmalıdır `"in"`.

Özellikler `id` ve `sqlQuery` hem de belirtilemez. Ne `id` ya da `sqlQuery` , tüm koleksiyon alınır ayarlanmadı.

## <a name="using-a-documentdb-api-input-binding"></a>Bir DocumentDB API giriş bağlama işlemini kullanma

* İşlev başarıyla çıktığında, C# ve F # işlevleri adlandırılmış giriş parametreleri aracılığıyla giriş belgeye yapılan değişiklikler otomatik olarak kalıcıdır. 
* JavaScript işlevleri güncelleştirmeleri otomatik olarak işlevi çıkış duruma getirilmez. Bunun yerine, kullanın `context.bindings.<documentName>In` ve `context.bindings.<documentName>Out` güncelleştirme yapmak için. Bkz: [JavaScript örnek](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Tek belge için giriş örneği
Aşağıdaki olduğunu varsayalım DocumentDB API bağlamasında giriş `bindings` function.json dizisi:

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

Belgenin metin değeri güncelleştirmek için bu giriş bağlama kullanır dile özgü örneğe bakın.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>C# giriş örneği #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>F # giriş örneği #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

Bu örnek gerektiren bir `project.json` belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:

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

Eklemek için bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>JavaScript giriş örneği

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Giriş örneği ile birden çok belge

Bir SQL sorgusu tarafından belirtilen birden çok belge almak sorgu parametrelerini özelleştirmek için bir sıra tetikleyici kullanarak istediğiniz varsayalım. 

Bu örnekte, bir parametre sırası tetikleyici sağlar `departmentId`. Bir kuyruk iletisi, `{ "departmentId" : "Finance" }` Finans departmanı için tüm kayıtları döndürür. Aşağıda, kullanmak *function.json*:

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

### <a name="input-sample-with-multiple-documents-in-c"></a>Giriş örneği birden çok belge C# ile

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a>JavaScript içindeki birden çok belge giriş örnekle

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

## <a id="docdboutput"></a>DocumentDB API bağlama çıktı
Sağlar bağlama DocumentDB API çıktı yeni bir belge bir Azure Cosmos DB veritabanına yazar. Aşağıdaki özelliklere sahip *function.json*:

- `name`: İşlev kodu yeni belge için kullanılan tanımlayıcı
- `type`: ayarlanmalıdır`"documentdb"`
- `databaseName`: Yeni belge oluşturulacağı koleksiyonu içeren veritabanı.
- `collectionName`: Yeni belge oluşturulacağı koleksiyonu.
- `createIfNotExists`: Henüz yoksa koleksiyonu oluşturduğunuzda olup olmadığını belirtmek için bir Boole değeri. Varsayılan değer *false*. Neden bu yeni için koleksiyonları fiyatlandırmaya olan ayrılmış işleme ile oluşturulur. Daha fazla ayrıntı için lütfen ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: Cosmos DB bağlantı dizesi içeren uygulama ayarı adı
- `direction`: ayarlanmalıdır`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Bir DocumentDB API kullanarak çıktıyı bağlama
Bu bölümde işlevi kodunuzda bağlama, DocumentDB API çıkış kullanmayı gösterir.

Çıktı parametresi, işlev yazdığınızda, varsayılan olarak yeni bir belge belge kimliği olarak bir otomatik olarak oluşturulan GUID ile veritabanınızda oluşturulur Çıktı belgenin belge kimliği belirterek belirtebilirsiniz `id` çıkış parametresi bir JSON özellik. 

>[!Note]  
>Var olan bir belgeyi Kimliğini belirttiğinizde, yeni çıktı belgenin üzerine. 

Birden çok belge çıktısını almak için de bağlayabilirsiniz `ICollector<T>` veya `IAsyncCollector<T>` burada `T` desteklenen türlerden biri.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>DocumentDB API çıkış bağlama örneği
Aşağıdaki olduğunu varsayalım DocumentDB API bağlamasında çıktı `bindings` function.json dizisi:

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

Ve şu biçimde JSON alan sıra için bir sıra giriş bağlama sahip:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Ve her kayıt için şu biçimde Cosmos DB belgeleri oluşturmak isterseniz:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Belgeler, veritabanına eklemek için bu çıktı bağlama kullanan dile özgü örneğine bakın.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# çıktı örneği #

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

### <a name="output-sample-in-f"></a>F # çıktı örneği #

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

Bu örnek gerektiren bir `project.json` belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:

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

Eklemek için bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>JavaScript çıktı örneği

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
