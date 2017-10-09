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
# <a name="azure-functions-storage-table-bindings"></a>Azure işlevleri depolama tablo bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede nasıl tooconfigure kodu Azure Storage Azure işlevlerinde bağlamaları tablo ve açıklanmaktadır. Giriş ve Azure Storage tablolarının bağlantılarında çıktı Azure işlevleri destekler.

Merhaba depolama Tablo Bağlama hello aşağıdaki senaryoları destekler:

* **C# veya Node.js işlevi tek bir satırda okuma** - ayarlanmış `partitionKey` ve `rowKey`. Merhaba `filter` ve `take` özellikleri bu senaryoda kullanılmaz.
* **C# işlevinde birden çok satır okuma** -hello işlevleri çalışma zamanı sağlayan bir `IQueryable<T>` nesnesi bağlı toohello tablo. Tür `T` öğesinden türetilmelidir `TableEntity` veya uygulayan `ITableEntity`. Merhaba `partitionKey`, `rowKey`, `filter`, ve `take` özellikler bu senaryoda kullanılmaz; hello kullanabilirsiniz `IQueryable` tüm gerekli filtreleme toodo nesne. 
* **Bir düğüm işlevinde birden çok satır okuma** - ayarlanmış hello `filter` ve `take` özellikleri. Ayarlamazsanız `partitionKey` veya `rowKey`.
* **C# işlevinde bir veya daha fazla satır yazma** -hello işlevleri çalışma zamanı sağlar bir `ICollector<T>` veya `IAsyncCollector<T>` ilişkili toohello tablo nerede `T` hello şema belirtir hello varlıklarının tooadd istiyor. Genellikle, yazın `T` türetilen `TableEntity` veya uygulayan `ITableEntity`, ancak gerekli değildir. Merhaba `partitionKey`, `rowKey`, `filter`, ve `take` özellikleri bu senaryoda kullanılmaz.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Depolama tablo giriş bağlama
Hello Azure Storage tablo giriş bağlama toouse işlevinizi depolama tabloda sağlar. 

Merhaba depolama tablo giriş tooa işlevini kullanır hello JSON nesneler şu hello `bindings` function.json dizisi:

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

Merhaba aşağıdakileri göz önünde bulundurun: 

* Kullanım `partitionKey` ve `rowKey` birlikte tooread tek bir varlık. Bu özellikleri isteğe bağlıdır. 
* `connection`Depolama bağlantı dizesi içeren bir uygulama ayarı Hello adını içermelidir. Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde, bir depolama alanı oluşturduğunuzda, hesap ya da mevcut bir seçer için bu uygulama ayarı yapılandırır. Ayrıca [bu uygulamayı el ile ayarlama yapılandırma](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Giriş kullanımı
C# işlevlerde, toohello giriş tablosu varlık (veya varlıklar) adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.
Burada `T` hello veri türü toodeserialize hello verilerini, istediğiniz olduğunda ve `paramName` hello belirtilen hello adı [bağlama giriş](#input). Node.js işlevlerde hello giriş tablosu varlık (veya varlıklar) kullanarak erişim `context.bindings.<name>`.

Node.js veya C# işlevlerde Hello giriş verileri seri durumdan. seri durumdan hello nesneler sahip `RowKey` ve `PartitionKey` özellikleri.

C# işlevleri, şu türlerini hello tooany de bağlayabilirsiniz ve çalışma zamanı deneyecek hello işlevleri çok hello tablo veri türü kullanılarak seri durumdan:

* Uygulayan herhangi bir türü`ITableEntity`
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Giriş örneği
Bir kuyruk tetikleyici tooread tek bir tablo satırı kullanan function.json aşağıdaki hello sahip olması. Merhaba JSON belirtir `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`Bu hello satır anahtarını hello kuyruk iletisi dizeden gelen gösterir.

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

Tek tablo varlığı okur hello dile özgü örneğine bakın.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>C# giriş örneği #
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

### <a name="input-sample-in-f"></a>F # giriş örneği #
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

### <a name="input-sample-in-nodejs"></a>Node.js giriş örneği
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Bağlama depolama tablo çıktısı
Hello Azure depolama tablosu bağlama toowrite varlıklar tooa depolama işlevinizi tabloda etkinleştirir çıktı. 

bir işlev hello JSON nesneler şu hello kullanan depolama tablo çıktısı hello `bindings` function.json dizisi:

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

Merhaba aşağıdakileri göz önünde bulundurun: 

* Kullanım `partitionKey` ve `rowKey` birlikte toowrite tek bir varlık. Bu özellikleri isteğe bağlıdır. Ayrıca belirtebilirsiniz `PartitionKey` ve `RowKey` oluşturduğunuzda hello varlık nesnesi işlevi kodunuzda.
* `connection`Depolama bağlantı dizesi içeren bir uygulama ayarı Hello adını içermelidir. Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde, bir depolama alanı oluşturduğunuzda, hesap ya da mevcut bir seçer için bu uygulama ayarı yapılandırır. Ayrıca [bu uygulamayı el ile ayarlama yapılandırma](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Çıktı kullanımı
C# işlevlerde, toohello tablo çıktısı adlı hello kullanarak bağladığınız `out` işlevi imzanız parametresinde ister `out <T> <name>`, burada `T` hello veri türü tooserialize hello verilerini, istediğiniz olduğunda ve `paramName` olduğu hello adı, Hello belirtilen [bağlama çıktı](#output). Node.js işlevlerde kullanarak çıktıyı hello tablo erişim `context.bindings.<name>`.

Node.js veya C# işlevleri nesneleri seri hale getirebilir. C# işlevlerde, şu türlerini toohello bağlayabilirsiniz:

* Uygulayan herhangi bir türü`ITableEntity`
* `ICollector<T>`(toooutput birden çok varlık. Bkz: [örnek](#outcsharp).)
* `IAsyncCollector<T>`(zaman uyumsuz sürümü `ICollector<T>`)
* `CloudTable`(hello Azure depolama SDK'sını kullanma. Bkz: [örnek](#readmulti).)

<a name="outputsample"></a>

## <a name="output-sample"></a>Çıkış örneği
Merhaba aşağıdaki *function.json* ve *run.csx* örnekteki nasıl toowrite birden çok tablo varlık.

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

Birden çok tablo varlıkları oluşturur hello dile özgü örneğine bakın.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>C# çıktı örneği #
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

### <a name="output-sample-in-f"></a>F # çıktı örneği #
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

### <a name="output-sample-in-nodejs"></a>Node.js çıktı örneği
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

## <a name="sample-read-multiple-table-entities-in-c"></a>Örnek: C# birden çok tablo varlıkları okuma  #
Merhaba aşağıdaki *function.json* ve C# kod örneğinde varlıklar hello kuyruk iletisi içinde belirtilen bir bölüm anahtarı için okur.

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

Böylece hello varlık türü öğesinden türetilen Hello C# kodu ekler başvuru toohello Azure depolama SDK'sı `TableEntity`.

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

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

