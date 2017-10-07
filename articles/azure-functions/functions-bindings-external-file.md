---
title: "aaaAzure işlevleri dış dosya bağlamalarını (Önizleme) | Microsoft Docs"
description: "Dış dosya bağlamaları Azure işlevlerini kullanma"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a>Azure işlevleri dış dosya bağlamalarını (Önizleme)
Bu makalede nasıl toomanipulate yerleşik bağlamalar kullanılarak işlevinizi içindeki sağlayıcıları (örneğin, OneDrive, Dropbox) farklı SaaS dosyaları gösterilmektedir. Tetiklemek, giriş ve dış dosya için bağlamaları çıktı Azure işlevleri destekler.

Bu bağlama tooSaaS sağlayıcıları API bağlantısı oluşturur veya mevcut API bağlantıları işlevi uygulamanızın kaynak grubundan kullanır.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Desteklenen dosya bağlantıları

|Bağlayıcı|Tetikleyici|Girdi|Çıktı|
|:-----|:---:|:---:|:---:|
|[Kutusu](https://www.box.com)|x|x|x
|[Açılan kutu](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive İş](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google sürücü](https://www.google.com/drive/)||x|x|

> [!NOTE]
> Dış dosya bağlantıları da kullanılabilir [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)

## <a name="external-file-trigger-binding"></a>Dış dosya tetiklemek bağlama

Hello Azure dış dosya tetikleyici uzak bir klasör izlemenizi ve değişiklik algılandığında işlevi kodunuzu çalıştırmak sağlar.

Merhaba dış dosya tetikleyici kullanan hello JSON nesneler şu hello `bindings` function.json dizisi

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a>Adı desenleri
Bir dosya adı deseni hello belirtebilirsiniz `path` özelliği. Başvurulan hello klasörü hello SaaS sağlayıcısında mevcut olması gerekir.
Örnekler:

```json
"path": "input/original-{name}",
```

Bu yol adlı bir dosyayı bulur *özgün Dosya1.ref* hello içinde *giriş* klasörü ve hello hello değerini `name` işlev kodu değişkende olacaktır `File1.txt`.

Bir örnek daha:

```json
"path": "input/{filename}.{fileextension}",
```

Bu yolu da adlı bir dosyayı bulur *özgün Dosya1.ref*ve hello hello değerini `filename` ve `fileextension` işlev kodu değişkenleri olacaktır *özgün dosya1* ve  *txt*.

Merhaba dosya uzantısı için sabit bir değer kullanarak dosyaları hello dosya türü kısıtlayabilirsiniz. Örneğin:

```json
"path": "samples/{name}.png",
```

Bu durumda, yalnızca *.png* hello dosyalarında *örnekleri* klasörü tetikleyici hello işlevi.

Süslü ayraçlar adı desenleri bulunan özel karakterleri var. Süslü ayraçlar hello adına, çift hello süslü ayraçlar sahip toospecify dosya adları.
Örneğin:

```json
"path": "images/{{20140101}}-{name}",
```

Bu yol adlı bir dosyayı bulur *{20140101}-soundfile.mp3* hello içinde *görüntüleri* klasörü ve hello `name` hello işlevi kodda değişken değeri olacaktır *soundfile.mp3*.

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a>Zararlı dosyaları işleme
Bir dış dosya Tetik işlevi başarısız olduğunda, belirli bir dosya için (Merhaba ilk denemede dahil) varsayılan olarak bu işlevini too5 kez Azure işlevleri yeniden dener.
Tüm 5 deneme başarısız olursa işlevleri ekler adlı bir ileti tooa depolama kuyruğu *webjobs apihubtrigger poison*. Merhaba kuyruk iletisi zararlı dosyaları için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:

* FunctionId (Merhaba biçiminde  *&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*)
* Dosya türü
* KlasörAdı
* Dosya adı
* ETag (örneğin, bir dosya sürümü tanımlayıcısı: "0x8D1DC6E70A277EF")


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Tetikleyici kullanımı
C# işlevlerde, toohello giriş dosyası veri adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.
Burada `T` hello veri türü toodeserialize hello verilerini, istediğiniz olduğunda ve `paramName` içinde belirtilen hello adı [JSON tetiklemek](#trigger). Node.js işlevlerde hello giriş dosyası verileri kullanarak erişim `context.bindings.<name>`.

Merhaba dosya şu türlerini hello hiçbirine seri durumdan çıkarılabiliyorsa:

* Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş dosya verileri için kullanışlıdır.
  Özel bir giriş türü bildirirseniz (örneğin `FooType`), Azure işlevleri, belirtilen türe toodeserialize hello JSON verilerini çalışır.
* String - metin dosya verileri için yararlıdır.

C# işlevleri, şu türlerini hello tooany de bağlayabilirsiniz ve hello işlevleri çalışma zamanı türü kullanarak hello dosya verileri seri durumdan dener:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Tetikleyici örnek
Function.json aşağıdaki hello olduğunu varsayalım, bir dış dosya tetikleyicisi tanımlar:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

Merhaba içeriğine toohello izlenen klasöre eklenen her dosya günlüklerini hello dile özgü örneğine bakın.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>C# tetikleyici kullanımı #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a>Node.js tetikleyici kullanımı

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Dış dosya bağlama giriş
Hello Azure dış dosya giriş bağlaması toouse işlevinizi dış bir klasörde dosyasından sağlar.

Merhaba dış dosya giriş tooa işlevini kullanan hello JSON nesneler şu hello `bindings` function.json dizisi:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Merhaba aşağıdakileri göz önünde bulundurun:

* `path`Merhaba klasör adı ve hello dosya adını içermelidir. Örneğin, bir [sıra tetikleyici](functions-bindings-storage-queue.md) işlevinizi, kullandığınız `"path": "samples-workitems/{queueTrigger}"` toopoint tooa hello dosyasında `samples-workitems` hello tetikleyici iletisinde belirtilen hello dosya adıyla eşleşen bir ada sahip klasör.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Giriş kullanımı
C# işlevlerde, toohello giriş dosyası veri adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.
Burada `T` hello veri türü toodeserialize hello verilerini, istediğiniz olduğunda ve `paramName` içinde belirtilen hello adı [bağlama giriş](#input). Node.js işlevlerde hello giriş dosyası verileri kullanarak erişim `context.bindings.<name>`.

Merhaba dosya şu türlerini hello hiçbirine seri durumdan çıkarılabiliyorsa:

* Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş dosya verileri için kullanışlıdır.
  Özel bir giriş türü bildirirseniz (örneğin `InputType`), Azure işlevleri, belirtilen türe toodeserialize hello JSON verilerini çalışır.
* String - metin dosya verileri için yararlıdır.

C# işlevleri, şu türlerini hello tooany de bağlayabilirsiniz ve hello işlevleri çalışma zamanı türü kullanarak hello dosya verileri seri durumdan dener:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Çıkış dış dosyası bağlama
Hello Azure dış dosya bağlama toowrite dosyaları tooan dış klasöründe işlevinizi etkinleştirir çıktı.

bir işlev hello JSON nesneler şu hello kullanan çıktı hello dış dosya `bindings` function.json dizisi:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Merhaba aşağıdakileri göz önünde bulundurun:

* `path`Merhaba klasör adı ve hello dosya adı toowrite içermesi gerekir. Örneğin, bir [sıra tetikleyici](functions-bindings-storage-queue.md) işlevinizi, kullandığınız `"path": "samples-workitems/{queueTrigger}"` toopoint tooa hello dosyasında `samples-workitems` hello tetikleyici iletisinde belirtilen hello dosya adıyla eşleşen bir ada sahip klasör.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Çıktı kullanımı
C# işlevlerde, toohello çıktı dosyası adlı hello kullanarak bağladığınız `out` işlevi imzanız parametresinde ister `out <T> <name>`, burada `T` hello veri türü tooserialize hello verilerini, istediğiniz olduğunda ve `paramName` olduğu hello adı, Belirtilen [bağlama çıktı](#output). Node.js işlevlerde hello çıktı dosyası kullanarak erişim `context.bindings.<name>`.

Şu türlerini hello birini kullanarak toohello çıktı dosyası yazabilirsiniz:

* Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirmesi için kullanışlıdır.
  Özel çıkış türü bildirirseniz (örneğin `out OutputType paramName`), Azure işlevleri tooserialize nesne JSON içinde çalışır. Merhaba işlevi çıktığında hello çıkış parametre null ise hello işlevleri çalışma zamanı null bir nesne bir dosya oluşturur.
* String - (`out string paramName`) metin dosya verileri için kullanışlıdır. Merhaba işlevi çıktığında yalnızca dize parametresi null olmayan ise hello işlevleri çalışma zamanı bir dosya oluşturur.

C# işlevlerde şu türlerini hello tooany çıkarabilirsiniz:

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Giriş + çıktı örneği
Function.json aşağıdaki hello olduğunu varsayalım tanımlayan bir [depolama kuyruğu tetikleyici](functions-bindings-storage-queue.md)dış dosyası giriş ve çıkış bir dış dosyası:

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Merhaba giriş dosyası toohello çıktı dosyası kopyalar hello dile özgü örneğine bakın.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>C# kullanımı #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a>Node.js kullanımı

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
