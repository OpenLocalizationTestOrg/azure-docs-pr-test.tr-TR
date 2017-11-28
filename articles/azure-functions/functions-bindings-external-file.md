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
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="95716-103">Azure işlevleri dış dosya bağlamalarını (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="95716-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="95716-104">Bu makalede nasıl toomanipulate yerleşik bağlamalar kullanılarak işlevinizi içindeki sağlayıcıları (örneğin, OneDrive, Dropbox) farklı SaaS dosyaları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="95716-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="95716-105">Tetiklemek, giriş ve dış dosya için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="95716-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="95716-106">Bu bağlama tooSaaS sağlayıcıları API bağlantısı oluşturur veya mevcut API bağlantıları işlevi uygulamanızın kaynak grubundan kullanır.</span><span class="sxs-lookup"><span data-stu-id="95716-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="95716-107">Desteklenen dosya bağlantıları</span><span class="sxs-lookup"><span data-stu-id="95716-107">Supported File connections</span></span>

|<span data-ttu-id="95716-108">Bağlayıcı</span><span class="sxs-lookup"><span data-stu-id="95716-108">Connector</span></span>|<span data-ttu-id="95716-109">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="95716-109">Trigger</span></span>|<span data-ttu-id="95716-110">Girdi</span><span class="sxs-lookup"><span data-stu-id="95716-110">Input</span></span>|<span data-ttu-id="95716-111">Çıktı</span><span class="sxs-lookup"><span data-stu-id="95716-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="95716-112">Kutusu</span><span class="sxs-lookup"><span data-stu-id="95716-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="95716-113">x</span><span class="sxs-lookup"><span data-stu-id="95716-113">x</span></span>|<span data-ttu-id="95716-114">x</span><span class="sxs-lookup"><span data-stu-id="95716-114">x</span></span>|<span data-ttu-id="95716-115">x</span><span class="sxs-lookup"><span data-stu-id="95716-115">x</span></span>
|[<span data-ttu-id="95716-116">Açılan kutu</span><span class="sxs-lookup"><span data-stu-id="95716-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="95716-117">x</span><span class="sxs-lookup"><span data-stu-id="95716-117">x</span></span>|<span data-ttu-id="95716-118">x</span><span class="sxs-lookup"><span data-stu-id="95716-118">x</span></span>|<span data-ttu-id="95716-119">x</span><span class="sxs-lookup"><span data-stu-id="95716-119">x</span></span>
|[<span data-ttu-id="95716-120">FTP</span><span class="sxs-lookup"><span data-stu-id="95716-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="95716-121">x</span><span class="sxs-lookup"><span data-stu-id="95716-121">x</span></span>|<span data-ttu-id="95716-122">x</span><span class="sxs-lookup"><span data-stu-id="95716-122">x</span></span>|<span data-ttu-id="95716-123">x</span><span class="sxs-lookup"><span data-stu-id="95716-123">x</span></span>
|[<span data-ttu-id="95716-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="95716-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="95716-125">x</span><span class="sxs-lookup"><span data-stu-id="95716-125">x</span></span>|<span data-ttu-id="95716-126">x</span><span class="sxs-lookup"><span data-stu-id="95716-126">x</span></span>|<span data-ttu-id="95716-127">x</span><span class="sxs-lookup"><span data-stu-id="95716-127">x</span></span>
|[<span data-ttu-id="95716-128">OneDrive İş</span><span class="sxs-lookup"><span data-stu-id="95716-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="95716-129">x</span><span class="sxs-lookup"><span data-stu-id="95716-129">x</span></span>|<span data-ttu-id="95716-130">x</span><span class="sxs-lookup"><span data-stu-id="95716-130">x</span></span>|<span data-ttu-id="95716-131">x</span><span class="sxs-lookup"><span data-stu-id="95716-131">x</span></span>
|[<span data-ttu-id="95716-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="95716-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="95716-133">x</span><span class="sxs-lookup"><span data-stu-id="95716-133">x</span></span>|<span data-ttu-id="95716-134">x</span><span class="sxs-lookup"><span data-stu-id="95716-134">x</span></span>|<span data-ttu-id="95716-135">x</span><span class="sxs-lookup"><span data-stu-id="95716-135">x</span></span>
|[<span data-ttu-id="95716-136">Google sürücü</span><span class="sxs-lookup"><span data-stu-id="95716-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="95716-137">x</span><span class="sxs-lookup"><span data-stu-id="95716-137">x</span></span>|<span data-ttu-id="95716-138">x</span><span class="sxs-lookup"><span data-stu-id="95716-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="95716-139">Dış dosya bağlantıları da kullanılabilir [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="95716-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="95716-140">Dış dosya tetiklemek bağlama</span><span class="sxs-lookup"><span data-stu-id="95716-140">External File trigger binding</span></span>

<span data-ttu-id="95716-141">Hello Azure dış dosya tetikleyici uzak bir klasör izlemenizi ve değişiklik algılandığında işlevi kodunuzu çalıştırmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="95716-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="95716-142">Merhaba dış dosya tetikleyici kullanan hello JSON nesneler şu hello `bindings` function.json dizisi</span><span class="sxs-lookup"><span data-stu-id="95716-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

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

### <a name="name-patterns"></a><span data-ttu-id="95716-143">Adı desenleri</span><span class="sxs-lookup"><span data-stu-id="95716-143">Name patterns</span></span>
<span data-ttu-id="95716-144">Bir dosya adı deseni hello belirtebilirsiniz `path` özelliği.</span><span class="sxs-lookup"><span data-stu-id="95716-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="95716-145">Başvurulan hello klasörü hello SaaS sağlayıcısında mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="95716-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="95716-146">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="95716-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="95716-147">Bu yol adlı bir dosyayı bulur *özgün Dosya1.ref* hello içinde *giriş* klasörü ve hello hello değerini `name` işlev kodu değişkende olacaktır `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="95716-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="95716-148">Bir örnek daha:</span><span class="sxs-lookup"><span data-stu-id="95716-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="95716-149">Bu yolu da adlı bir dosyayı bulur *özgün Dosya1.ref*ve hello hello değerini `filename` ve `fileextension` işlev kodu değişkenleri olacaktır *özgün dosya1* ve  *txt*.</span><span class="sxs-lookup"><span data-stu-id="95716-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="95716-150">Merhaba dosya uzantısı için sabit bir değer kullanarak dosyaları hello dosya türü kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95716-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="95716-151">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="95716-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="95716-152">Bu durumda, yalnızca *.png* hello dosyalarında *örnekleri* klasörü tetikleyici hello işlevi.</span><span class="sxs-lookup"><span data-stu-id="95716-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="95716-153">Süslü ayraçlar adı desenleri bulunan özel karakterleri var.</span><span class="sxs-lookup"><span data-stu-id="95716-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="95716-154">Süslü ayraçlar hello adına, çift hello süslü ayraçlar sahip toospecify dosya adları.</span><span class="sxs-lookup"><span data-stu-id="95716-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="95716-155">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="95716-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="95716-156">Bu yol adlı bir dosyayı bulur *{20140101}-soundfile.mp3* hello içinde *görüntüleri* klasörü ve hello `name` hello işlevi kodda değişken değeri olacaktır *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="95716-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

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

### <a name="handling-poison-files"></a><span data-ttu-id="95716-157">Zararlı dosyaları işleme</span><span class="sxs-lookup"><span data-stu-id="95716-157">Handling poison files</span></span>
<span data-ttu-id="95716-158">Bir dış dosya Tetik işlevi başarısız olduğunda, belirli bir dosya için (Merhaba ilk denemede dahil) varsayılan olarak bu işlevini too5 kez Azure işlevleri yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="95716-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="95716-159">Tüm 5 deneme başarısız olursa işlevleri ekler adlı bir ileti tooa depolama kuyruğu *webjobs apihubtrigger poison*.</span><span class="sxs-lookup"><span data-stu-id="95716-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="95716-160">Merhaba kuyruk iletisi zararlı dosyaları için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:</span><span class="sxs-lookup"><span data-stu-id="95716-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="95716-161">FunctionId (Merhaba biçiminde  *&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*)</span><span class="sxs-lookup"><span data-stu-id="95716-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="95716-162">Dosya türü</span><span class="sxs-lookup"><span data-stu-id="95716-162">FileType</span></span>
* <span data-ttu-id="95716-163">KlasörAdı</span><span class="sxs-lookup"><span data-stu-id="95716-163">FolderName</span></span>
* <span data-ttu-id="95716-164">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="95716-164">FileName</span></span>
* <span data-ttu-id="95716-165">ETag (örneğin, bir dosya sürümü tanımlayıcısı: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="95716-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="95716-166">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="95716-166">Trigger usage</span></span>
<span data-ttu-id="95716-167">C# işlevlerde, toohello giriş dosyası veri adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="95716-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="95716-168">Burada `T` hello veri türü toodeserialize hello verilerini, istediğiniz olduğunda ve `paramName` içinde belirtilen hello adı [JSON tetiklemek](#trigger).</span><span class="sxs-lookup"><span data-stu-id="95716-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="95716-169">Node.js işlevlerde hello giriş dosyası verileri kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="95716-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="95716-170">Merhaba dosya şu türlerini hello hiçbirine seri durumdan çıkarılabiliyorsa:</span><span class="sxs-lookup"><span data-stu-id="95716-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="95716-171">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş dosya verileri için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="95716-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="95716-172">Özel bir giriş türü bildirirseniz (örneğin `FooType`), Azure işlevleri, belirtilen türe toodeserialize hello JSON verilerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="95716-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="95716-173">String - metin dosya verileri için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="95716-173">String - useful for text file data.</span></span>

<span data-ttu-id="95716-174">C# işlevleri, şu türlerini hello tooany de bağlayabilirsiniz ve hello işlevleri çalışma zamanı türü kullanarak hello dosya verileri seri durumdan dener:</span><span class="sxs-lookup"><span data-stu-id="95716-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="95716-175">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="95716-175">Trigger sample</span></span>
<span data-ttu-id="95716-176">Function.json aşağıdaki hello olduğunu varsayalım, bir dış dosya tetikleyicisi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="95716-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="95716-177">Merhaba içeriğine toohello izlenen klasöre eklenen her dosya günlüklerini hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="95716-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="95716-178">C#</span><span class="sxs-lookup"><span data-stu-id="95716-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="95716-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="95716-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="95716-180">C# tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="95716-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="95716-181">Node.js tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="95716-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="95716-182">Dış dosya bağlama giriş</span><span class="sxs-lookup"><span data-stu-id="95716-182">External File input binding</span></span>
<span data-ttu-id="95716-183">Hello Azure dış dosya giriş bağlaması toouse işlevinizi dış bir klasörde dosyasından sağlar.</span><span class="sxs-lookup"><span data-stu-id="95716-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="95716-184">Merhaba dış dosya giriş tooa işlevini kullanan hello JSON nesneler şu hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="95716-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="95716-185">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="95716-185">Note hello following:</span></span>

* <span data-ttu-id="95716-186">`path`Merhaba klasör adı ve hello dosya adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="95716-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="95716-187">Örneğin, bir [sıra tetikleyici](functions-bindings-storage-queue.md) işlevinizi, kullandığınız `"path": "samples-workitems/{queueTrigger}"` toopoint tooa hello dosyasında `samples-workitems` hello tetikleyici iletisinde belirtilen hello dosya adıyla eşleşen bir ada sahip klasör.</span><span class="sxs-lookup"><span data-stu-id="95716-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="95716-188">Giriş kullanımı</span><span class="sxs-lookup"><span data-stu-id="95716-188">Input usage</span></span>
<span data-ttu-id="95716-189">C# işlevlerde, toohello giriş dosyası veri adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="95716-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="95716-190">Burada `T` hello veri türü toodeserialize hello verilerini, istediğiniz olduğunda ve `paramName` içinde belirtilen hello adı [bağlama giriş](#input).</span><span class="sxs-lookup"><span data-stu-id="95716-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="95716-191">Node.js işlevlerde hello giriş dosyası verileri kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="95716-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="95716-192">Merhaba dosya şu türlerini hello hiçbirine seri durumdan çıkarılabiliyorsa:</span><span class="sxs-lookup"><span data-stu-id="95716-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="95716-193">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş dosya verileri için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="95716-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="95716-194">Özel bir giriş türü bildirirseniz (örneğin `InputType`), Azure işlevleri, belirtilen türe toodeserialize hello JSON verilerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="95716-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="95716-195">String - metin dosya verileri için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="95716-195">String - useful for text file data.</span></span>

<span data-ttu-id="95716-196">C# işlevleri, şu türlerini hello tooany de bağlayabilirsiniz ve hello işlevleri çalışma zamanı türü kullanarak hello dosya verileri seri durumdan dener:</span><span class="sxs-lookup"><span data-stu-id="95716-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="95716-197">Çıkış dış dosyası bağlama</span><span class="sxs-lookup"><span data-stu-id="95716-197">External File output binding</span></span>
<span data-ttu-id="95716-198">Hello Azure dış dosya bağlama toowrite dosyaları tooan dış klasöründe işlevinizi etkinleştirir çıktı.</span><span class="sxs-lookup"><span data-stu-id="95716-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="95716-199">bir işlev hello JSON nesneler şu hello kullanan çıktı hello dış dosya `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="95716-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="95716-200">Merhaba aşağıdakileri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="95716-200">Note hello following:</span></span>

* <span data-ttu-id="95716-201">`path`Merhaba klasör adı ve hello dosya adı toowrite içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="95716-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="95716-202">Örneğin, bir [sıra tetikleyici](functions-bindings-storage-queue.md) işlevinizi, kullandığınız `"path": "samples-workitems/{queueTrigger}"` toopoint tooa hello dosyasında `samples-workitems` hello tetikleyici iletisinde belirtilen hello dosya adıyla eşleşen bir ada sahip klasör.</span><span class="sxs-lookup"><span data-stu-id="95716-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="95716-203">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="95716-203">Output usage</span></span>
<span data-ttu-id="95716-204">C# işlevlerde, toohello çıktı dosyası adlı hello kullanarak bağladığınız `out` işlevi imzanız parametresinde ister `out <T> <name>`, burada `T` hello veri türü tooserialize hello verilerini, istediğiniz olduğunda ve `paramName` olduğu hello adı, Belirtilen [bağlama çıktı](#output).</span><span class="sxs-lookup"><span data-stu-id="95716-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="95716-205">Node.js işlevlerde hello çıktı dosyası kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="95716-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="95716-206">Şu türlerini hello birini kullanarak toohello çıktı dosyası yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95716-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="95716-207">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirmesi için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="95716-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="95716-208">Özel çıkış türü bildirirseniz (örneğin `out OutputType paramName`), Azure işlevleri tooserialize nesne JSON içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="95716-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="95716-209">Merhaba işlevi çıktığında hello çıkış parametre null ise hello işlevleri çalışma zamanı null bir nesne bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="95716-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="95716-210">String - (`out string paramName`) metin dosya verileri için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="95716-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="95716-211">Merhaba işlevi çıktığında yalnızca dize parametresi null olmayan ise hello işlevleri çalışma zamanı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="95716-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="95716-212">C# işlevlerde şu türlerini hello tooany çıkarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95716-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="95716-213">Giriş + çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="95716-213">Input + Output sample</span></span>
<span data-ttu-id="95716-214">Function.json aşağıdaki hello olduğunu varsayalım tanımlayan bir [depolama kuyruğu tetikleyici](functions-bindings-storage-queue.md)dış dosyası giriş ve çıkış bir dış dosyası:</span><span class="sxs-lookup"><span data-stu-id="95716-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="95716-215">Merhaba giriş dosyası toohello çıktı dosyası kopyalar hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="95716-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="95716-216">C#</span><span class="sxs-lookup"><span data-stu-id="95716-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="95716-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="95716-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="95716-218">C# kullanımı</span><span class="sxs-lookup"><span data-stu-id="95716-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="95716-219">Node.js kullanımı</span><span class="sxs-lookup"><span data-stu-id="95716-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="95716-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95716-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
