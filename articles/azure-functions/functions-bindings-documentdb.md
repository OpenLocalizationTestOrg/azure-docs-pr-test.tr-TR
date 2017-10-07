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
# <a name="azure-functions-cosmos-db-bindings"></a>Azure işlevleri Cosmos DB bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede açıklanır nasıl tooconfigure ve kod Azure Cosmos DB bağlamaları Azure işlevlerinde. Giriş ve Cosmos DB bağlantılarında çıktı Azure işlevleri destekler.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Cosmos DB hakkında daha fazla bilgi için bkz: [giriş tooCosmos DB](../documentdb/documentdb-introduction.md) ve [Cosmos DB konsol uygulaması oluşturma](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>DocumentDB API giriş bağlama
Merhaba DocumentDB API giriş bağlaması Cosmos DB belge alır ve hello işlevinin giriş parametresi adlı toohello geçirir. Merhaba belge kimliği belirlenebilir hello işlevi çağırır hello Tetikle temel. 

Merhaba DocumentDB API giriş bağlaması sahip özelliklerinde aşağıdaki hello *function.json*:

- `name`: İşlev kodu hello belge için kullanılan tanımlayıcı adı
- `type`: çok ayarlanması gerekir "documentdb"
- `databaseName`: hello belge içeren hello veritabanı
- `collectionName`: hello belge içeren hello koleksiyon
- `id`: hello belge tooretrieve kimliğini hello. Bu özellik bağlamaları parametreleri destekler; bkz: [toocustom giriş özellikleri bağlama ifadesinde bağlamak](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) hello makalede [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).
- `sqlQuery`Birden çok belge almak için kullanılan Cosmos DB SQL sorgusu. Merhaba query çalışma zamanı bağlamaları destekler. Örneğin, `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: Cosmos DB bağlantı dizesi içeren hello uygulama ayarı hello adı
- `direction`: çok ayarlanmalıdır`"in"`.

Merhaba özellikleri `id` ve `sqlQuery` hem de belirtilemez. Ne `id` ya da `sqlQuery` , hello tüm ayarlanmış koleksiyonu alınır.

## <a name="using-a-documentdb-api-input-binding"></a>Bir DocumentDB API giriş bağlama işlemini kullanma

* Merhaba işlevi başarıyla çıktığında, C# ve F # işlevleri toohello giriş belgesi adlandırılmış giriş parametreleri aracılığıyla yapılan tüm değişiklikler otomatik olarak kalıcıdır. 
* JavaScript işlevleri güncelleştirmeleri otomatik olarak işlevi çıkış duruma getirilmez. Bunun yerine, kullanın `context.bindings.<documentName>In` ve `context.bindings.<documentName>Out` toomake güncelleştirmeleri. Merhaba bkz [JavaScript örnek](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Tek belge için giriş örneği
Merhaba aşağıdaki olduğunu varsayalım DocumentDB API hello bağlamasında giriş `bindings` function.json dizisi:

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

Bu giriş bağlaması tooupdate hello belgenin metin değeri kullanan hello dile özgü örneğine bakın.

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

Bu örnek gerektiren bir `project.json` hello belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:

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

tooadd bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).

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

Bir kuyruk tetikleyici toocustomize hello sorgu parametrelerini kullanarak, bir SQL sorgusu tarafından belirtilen birden çok belge tooretrieve istediğiniz varsayalım. 

Bu örnekte, bir parametre hello sıra tetikleyici sağlar `departmentId`. Bir kuyruk iletisi, `{ "departmentId" : "Finance" }` hello Finans departmanı için tüm kayıtları döndürür. Merhaba aşağıdakileri kullanmak *function.json*:

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
Merhaba DocumentDB API bağlama, yeni bir belge tooan Azure Cosmos DB veritabanı yazmanıza olanak veren çıktı. Aşağıdaki özelliklere de hello sahip *function.json*:

- `name`: İşlev kodu hello yeni belge için kullanılan tanımlayıcı
- `type`: çok ayarlanmalıdır`"documentdb"`
- `databaseName`: Burada hello yeni belge oluşturulacak hello koleksiyonu içeren hello veritabanı.
- `collectionName`: Merhaba burada hello yeni belge oluşturulacak koleksiyonu.
- `createIfNotExists`: Henüz yoksa hello koleksiyon oluşturulur olup olmadığını tooindicate bir Boole değeri. Merhaba varsayılandır *false*. Merhaba neden bu yeni için koleksiyonları fiyatlandırmaya olan ayrılmış işleme ile oluşturulur. Daha fazla ayrıntı için lütfen başlangıç adresini ziyaret edin [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: Cosmos DB bağlantı dizesi içeren hello uygulama ayarı hello adı
- `direction`: çok ayarlanmalıdır`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Bir DocumentDB API kullanarak çıktıyı bağlama
Bu bölümde işlevi kodunuzda bağlama toouse DocumentDB API'nizi nasıl çıktısını gösterir.

Başlangıç olarak bir otomatik olarak oluşturulan GUID ile yeni bir belge veritabanınızda oluşturulan varsayılan olarak, işlevinde toohello çıktı parametresi yazdığınızda, kimliği belge Merhaba belirterek hello belge kimliği çıktı belgenin belirtebilirsiniz `id` hello JSON özelliğinde çıktı parametresi. 

>[!Note]  
>Var olan bir belgeyi hello Kimliğini belirttiğinizde, hello yeni çıkış belge tarafından üzerine. 

toooutput birden çok belge, ayrıca çok bağlayabilirsiniz`ICollector<T>` veya `IAsyncCollector<T>` burada `T` desteklenen hello türlerinden biridir.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>DocumentDB API çıkış bağlama örneği
Merhaba aşağıdaki olduğunu varsayalım DocumentDB API hello bağlamasında çıktı `bindings` function.json dizisi:

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

Ve JSON biçimini izleyen hello alan sıra için bir sıra giriş bağlama vardır:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Ve toocreate Cosmos DB hello biçimi her kayıt için aşağıdaki belgelerde istiyorsanız:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Bu çıktı bağlama tooadd belgeleri tooyour veritabanı kullanan hello dile özgü örneğine bakın.

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

Bu örnek gerektiren bir `project.json` hello belirten dosyası `FSharp.Interop.Dynamic` ve `Dynamitey` NuGet bağımlılıklar:

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

tooadd bir `project.json` dosya için bkz: [F # paket Yönetimi](functions-reference-fsharp.md#package).

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
