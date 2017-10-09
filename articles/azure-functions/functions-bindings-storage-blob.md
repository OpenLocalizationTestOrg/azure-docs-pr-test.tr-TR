---
title: "aaaAzure işlevleri Blob Storage bağlamaları | Microsoft Docs"
description: "Nasıl toouse Azure Storage tetikler ve Azure işlevlerinde bağlamaları anlayın."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Azure işlevleri Blob Depolama bağlamaları
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede açıklanır nasıl tooconfigure ve Azure Blob Depolama bağlamaları Azure işlevlerinde ile çalışır. Azure işlevleri destekler tetikleyici, giriş ve Azure Blob Depolama bağlantılarında çıkış. Tüm bağlama kullanılabilir olan özellikler için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> A [yalnızca depolama hesabı blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts) desteklenmiyor. BLOB Depolama Tetikleyicileri ve bağlamaları genel amaçlı depolama hesabı gerektirir. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>BLOB Depolama Tetikleyicileri ve bağlamaları

Yeni veya güncelleştirilmiş bir blob algılandığında hello Azure Blob Depolama tetikleyici kullanılarak, işlevi kodunuzu çağrılır. Merhaba blob içeriklerini giriş toohello işlev olarak sağlanır.

Hello kullanarak blob depolama tetikleyici tanımlamak **tümleştir** hello işlevleri portalındaki sekmesi. Merhaba portal oluşturur hello tanımında aşağıdaki hello **bağlamaları** bölümünü *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

BLOB giriş ve çıkış bağlamalar kullanılarak tanımlanır `blob` hello bağlama türü olarak:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Merhaba `path` ifadeleri ve filtre parametrelerini bağlama özelliğini destekler. Bkz: [adı desenleri](#pattern).
* Merhaba `connection` özelliği, depolama bağlantı dizesi içeren bir uygulama ayarı hello adını içermelidir. Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde bir depolama hesabı seçtiğinizde, bu uygulama ayarı yapılandırır.

> [!NOTE]
> Tüketim plan üzerinde bir blob tetikleyici kullanırken olabilir tooa 10 dakikalık gecikme bir işlev uygulaması boşta geçti sonra yeni BLOB'lar işleme. Merhaba işlev uygulaması çalışmaya başladıktan sonra BLOB'ları hemen işlenir. Bu ilk tooavoid gecikme, aşağıdaki seçenekleri şu hello birini göz önünde bulundurun:
> - Always On özellikli ile bir uygulama hizmeti planını kullan.
> - Başka bir mekanizma tootrigger hello blob hello blob adı içeren bir kuyruk iletisi gibi işlemleri kullanın. Bir örnek için bkz: [sıra tetikleyicisi blob ile girişi bağlamayı](#input-sample).

<a name="pattern"></a>

### <a name="name-patterns"></a>Adı desenleri
Bir blob adı deseni hello belirtebilirsiniz `path` filtre veya bağlama bir ifade olabilir özelliği. Bkz: [ifadeleri ve desenler bağlama](functions-triggers-bindings.md#binding-expressions-and-patterns).

Örneğin, "özgün," Merhaba dize ile başlayan toofilter tooblobs tanımı aşağıdaki hello kullanın. Bu yol adlı bir blob bulur *özgün Blob1.txt* hello içinde *giriş* kapsayıcı ve hello hello değerini `name` işlevi kodda değişkenidir `Blob1`.

```json
"path": "input/original-{name}",
```

Ayrıca, toobind toohello blob dosya adını ve uzantısını iki desenlerini kullanın. Bu yolu da adlı bir blob bulur *özgün Blob1.txt*ve hello hello değerini `blobname` ve `blobextension` değişkenleri işlevi kodda *özgün Blob1* ve *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

Merhaba dosya uzantısı için sabit bir değer kullanarak hello dosya türü BLOB kısıtlayabilirsiniz. Örneğin, tootrigger yalnızca dosyalarda .png desen aşağıdaki kullanım hello:

```json
"path": "samples/{name}.png",
```

Süslü ayraçlar adı desenleri bulunan özel karakterleri var. Süslü ayraçlar hello sahip toospecify blob adları, iki ayraçlar kullanılmasını hello kaşlı kaçış. Merhaba aşağıdaki örnek bulur adlı bir blob *{20140101}-soundfile.mp3* hello içinde *görüntüleri* kapsayıcı ve hello `name` hello işlevi kodda değişken değeri  *soundfile.mp3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Tetikleyici meta verileri

Merhaba blob tetikleyici çeşitli meta veri özelliklerini sağlar. Bu özellikler, diğer bağlamaları bağlamaları ifadelerinde bir parçası olarak ya da kodunuzu parametre olarak kullanılabilir. Merhaba bu değerlere sahip aynı topluca [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. `string` yazın. Merhaba tetikleme blob yolu
- **URI**. `System.Uri` yazın. Merhaba birincil konumu için Hello blob'un URI.
- **Özellikler**. `Microsoft.WindowsAzure.Storage.Blob.BlobProperties` yazın. BLOB'ın sistem özellikleri hello.
- **Meta veri**. `IDictionary<string,string>` yazın. Merhaba kullanıcı tanımlı meta veriler hello blob.

<a name="receipts"></a>

### <a name="blob-receipts"></a>BLOB giriş
Hello Azure işlevleri çalışma zamanı yok blob Tetik işlevi için birden çok kez çağrılır sağlar aynı yeni veya güncelleştirilmiş blob hello. Belirtilen blob sürümü işlediğinde toodetermine sakladığı *blob giriş*.

Azure işlevleri depoları Alındılar adlı bir kapsayıcıda blob *azure Web işleri konakları* hello işlevi uygulamanız için Azure depolama hesabı içinde (Merhaba uygulama ayarı tarafından tanımlanan `AzureWebJobsStorage`). Bir blob giriş bilgisinden hello sahiptir:

* Merhaba tetiklenen işlevi ("*&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*", örneğin:"MyFunctionApp.Functions.CopyBlob")
* Merhaba kapsayıcı adı
* Merhaba blob türü ("BlockBlob" veya "PageBlob")
* Merhaba blob adı
* Merhaba ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

Merhaba silme hello blob giriş bu blob için tooforce bir blob yeniden işlemeyerek *azure Web işleri konakları* kapsayıcı el ile.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Zararlı BLOB'ları işleme
Belirli bir blob için bir blob Tetik işlevi başarısız olduğunda, Azure işlevleri, varsayılan olarak 5 kez toplam işlev yeniden dener. 

Tüm 5 deneme başarısız olursa, Azure işlevleri adlı bir ileti tooa depolama kuyruğu ekler *webjobs blobtrigger poison*. Merhaba kuyruk iletisi zararlı BLOB'lar için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:

* FunctionId (Merhaba biçiminde  *&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*)
* BlobType ("BlockBlob" veya "PageBlob")
* Kapsayıcı adı
* BlobName
* ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")

### <a name="blob-polling-for-large-containers"></a>Blob büyük kapsayıcıları için yoklama
İzlenmekte olan hello blob kapsayıcısı 10. 000'den fazla BLOB'ları içeriyorsa, çalışma zamanı tarar hello işlevleri dosyaları toowatch yeni veya değiştirilmiş BLOB'lar için oturum açın. Bu işlem, gerçek zamanlı değildir. Merhaba blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil. Ayrıca, [depolama günlüklerine "en iyi çaba" üzerinde oluşturulan](/rest/api/storageservices/About-Storage-Analytics-Logging) temel. Tüm olayları yakalanır garantisi yoktur. Bazı koşullarda günlükleri eksik olabilir. Daha hızlı veya daha güvenilir blob işleme gerekiyorsa oluşturma göz önünde bulundurun bir [kuyruk iletisi](../storage/queues/storage-dotnet-how-to-use-queues.md) hello blob oluşturduğunuzda. Ardından, bir [sıra tetikleyici](functions-bindings-storage-queue.md) blob tetikleyici tooprocess hello blob yerine.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Blob tetikleyici kullanılarak ve giriş bağlama
.NET işlevlerde gibi bir yöntem parametresi kullanılarak hello blob veri erişim `Stream paramName`. Burada, `paramName` hello belirtilen hello değeri [tetikleyici yapılandırma](#trigger). Node.js işlevlerde erişim hello giriş blob verilerini kullanarak `context.bindings.<name>`.

.NET ile Merhaba aşağıdaki listede hello türlerinin tooany bağlayabilirsiniz. Giriş bağlama olarak kullandıysanız, bu türlerinden bazıları gerektiren bir `inout` yönde bağlama *function.json*. Düzenleyici Gelişmiş hello kullanmalısınız bu yönünü hello standart Düzenleyicisi tarafından desteklenmiyor.

* `TextReader`
* `Stream`
* `ICloudBlob`("ınout" bağlama yönü gerektirir)
* `CloudBlockBlob`("ınout" bağlama yönü gerektirir)
* `CloudPageBlob`("ınout" bağlama yönü gerektirir)
* `CloudAppendBlob`("ınout" bağlama yönü gerektirir)

Metin BLOB'ları beklenir, tooa .NET de bağlayabilirsiniz `string` türü. Bu, yalnızca Hello tüm blob içeriklerini belleğe yüklenen gibi hello blob boyutu, küçükse önerilir. Genellikle, tercih toouse olan bir `Stream` veya `CloudBlockBlob` türü.

## <a name="trigger-sample"></a>Tetikleyici örnek
Bir blob depolama tetikleyici tanımlar function.json aşağıdaki hello olduğunu varsayalım:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

Merhaba içeriğine toohello izlenen kapsayıcı eklenen her bir blob günlüklerini hello dile özgü örneğine bakın.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>BLOB tetikleyici örnekler C# #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Tetikleyici örnekte Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Bir blob kullanarak çıktıyı bağlama

.NET işlevlerde ya da kullanım gereken bir `out string` parametresi işlev imzası veya hello türlerinin listesi aşağıdaki hello kullanımı. Node.js işlevlerde hello çıkış blob kullanarak erişim `context.bindings.<name>`.

.NET işlevlerde şu türlerini hello tooany çıkarabilirsiniz:

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Sıra tetikleyiciyle blob girdi ve çıktı örneği
Function.json aşağıdaki hello olduğunu varsayalım tanımlayan bir [kuyruk depolama tetikleyici](functions-bindings-storage-queue.md)bir blob depolama giriş ve bir blob depolama çıkış. Bildirim hello hello kullanımını `queueTrigger` meta veri özelliği. Giriş ve çıkış hello blob içinde `path` özellikleri:

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

Merhaba giriş blob toohello çıkış blob kopyalar hello dile özgü örneğine bakın.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>BLOB bağlama örnek C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>BLOB bağlama Node.js örneğinde

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

