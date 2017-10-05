---
title: "Azure işlevleri dış dosya bağlamalarını (Önizleme) | Microsoft Docs"
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
ms.openlocfilehash: 2082e4e9b23271be93f3e3ab43997c3243238da8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="d72ef-103">Azure işlevleri dış dosya bağlamalarını (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="d72ef-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="d72ef-104">Bu makalede sağlayıcılardan farklı SaaS (örneğin, OneDrive, Dropbox) dosyaları yönetmek yerleşik bağlamalar kullanılarak işlevinizi içinde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d72ef-104">This article shows how to manipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="d72ef-105">Tetiklemek, giriş ve dış dosya için bağlamaları çıktı Azure işlevleri destekler.</span><span class="sxs-lookup"><span data-stu-id="d72ef-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="d72ef-106">Bu bağlama SaaS sağlayıcısı API bağlantılar oluşturur veya mevcut API bağlantıları işlevi uygulamanızın kaynak grubundan kullanır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-106">This binding creates API connections to SaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="d72ef-107">Desteklenen dosya bağlantıları</span><span class="sxs-lookup"><span data-stu-id="d72ef-107">Supported File connections</span></span>

|<span data-ttu-id="d72ef-108">Bağlayıcı</span><span class="sxs-lookup"><span data-stu-id="d72ef-108">Connector</span></span>|<span data-ttu-id="d72ef-109">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="d72ef-109">Trigger</span></span>|<span data-ttu-id="d72ef-110">Girdi</span><span class="sxs-lookup"><span data-stu-id="d72ef-110">Input</span></span>|<span data-ttu-id="d72ef-111">Çıktı</span><span class="sxs-lookup"><span data-stu-id="d72ef-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="d72ef-112">Kutusu</span><span class="sxs-lookup"><span data-stu-id="d72ef-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="d72ef-113">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-113">x</span></span>|<span data-ttu-id="d72ef-114">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-114">x</span></span>|<span data-ttu-id="d72ef-115">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-115">x</span></span>
|[<span data-ttu-id="d72ef-116">Açılan kutu</span><span class="sxs-lookup"><span data-stu-id="d72ef-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="d72ef-117">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-117">x</span></span>|<span data-ttu-id="d72ef-118">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-118">x</span></span>|<span data-ttu-id="d72ef-119">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-119">x</span></span>
|[<span data-ttu-id="d72ef-120">FTP</span><span class="sxs-lookup"><span data-stu-id="d72ef-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="d72ef-121">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-121">x</span></span>|<span data-ttu-id="d72ef-122">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-122">x</span></span>|<span data-ttu-id="d72ef-123">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-123">x</span></span>
|[<span data-ttu-id="d72ef-124">OneDrive</span><span class="sxs-lookup"><span data-stu-id="d72ef-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="d72ef-125">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-125">x</span></span>|<span data-ttu-id="d72ef-126">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-126">x</span></span>|<span data-ttu-id="d72ef-127">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-127">x</span></span>
|[<span data-ttu-id="d72ef-128">OneDrive İş</span><span class="sxs-lookup"><span data-stu-id="d72ef-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="d72ef-129">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-129">x</span></span>|<span data-ttu-id="d72ef-130">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-130">x</span></span>|<span data-ttu-id="d72ef-131">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-131">x</span></span>
|[<span data-ttu-id="d72ef-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="d72ef-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="d72ef-133">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-133">x</span></span>|<span data-ttu-id="d72ef-134">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-134">x</span></span>|<span data-ttu-id="d72ef-135">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-135">x</span></span>
|[<span data-ttu-id="d72ef-136">Google sürücü</span><span class="sxs-lookup"><span data-stu-id="d72ef-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="d72ef-137">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-137">x</span></span>|<span data-ttu-id="d72ef-138">x</span><span class="sxs-lookup"><span data-stu-id="d72ef-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="d72ef-139">Dış dosya bağlantıları da kullanılabilir [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="d72ef-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="d72ef-140">Dış dosya tetiklemek bağlama</span><span class="sxs-lookup"><span data-stu-id="d72ef-140">External File trigger binding</span></span>

<span data-ttu-id="d72ef-141">Azure dış dosya tetikleyici uzak bir klasör izlemenizi ve değişiklik algılandığında işlevi kodunuzu çalıştırmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d72ef-141">The Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="d72ef-142">Dış dosya tetikleyici aşağıdaki JSON nesneleri kullanan `bindings` function.json dizisi</span><span class="sxs-lookup"><span data-stu-id="d72ef-142">The external file trigger uses the following JSON objects in the `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder to monitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of the following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="d72ef-143">Adı desenleri</span><span class="sxs-lookup"><span data-stu-id="d72ef-143">Name patterns</span></span>
<span data-ttu-id="d72ef-144">Bir dosya adı deseni içinde belirttiğiniz `path` özelliği.</span><span class="sxs-lookup"><span data-stu-id="d72ef-144">You can specify a file name pattern in the `path` property.</span></span> <span data-ttu-id="d72ef-145">Başvurulan klasörü SaaS sağlayıcı mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-145">The folder referenced must exist in the SaaS provider.</span></span>
<span data-ttu-id="d72ef-146">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="d72ef-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="d72ef-147">Bu yol adlı bir dosyayı bulur *özgün Dosya1.ref* içinde *giriş* klasörü ve değerini `name` işlev kodu değişkende olacaktır `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="d72ef-147">This path would find a file named *original-File1.txt* in the *input* folder, and the value of the `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="d72ef-148">Bir örnek daha:</span><span class="sxs-lookup"><span data-stu-id="d72ef-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="d72ef-149">Bu yolu da adlı bir dosyayı bulur *özgün Dosya1.ref*, değerini `filename` ve `fileextension` işlev kodu değişkenleri olacaktır *özgün dosya1* ve *txt* .</span><span class="sxs-lookup"><span data-stu-id="d72ef-149">This path would also find a file named *original-File1.txt*, and the value of the `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="d72ef-150">Dosya uzantısı için sabit bir değer kullanarak dosyaları dosya türünü kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d72ef-150">You can restrict the file type of files by using a fixed value for the file extension.</span></span> <span data-ttu-id="d72ef-151">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d72ef-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="d72ef-152">Bu durumda, yalnızca *.png* dosyalar *örnekleri* klasörü tetiklemek işlevi.</span><span class="sxs-lookup"><span data-stu-id="d72ef-152">In this case, only *.png* files in the *samples* folder trigger the function.</span></span>

<span data-ttu-id="d72ef-153">Süslü ayraçlar adı desenleri bulunan özel karakterleri var.</span><span class="sxs-lookup"><span data-stu-id="d72ef-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="d72ef-154">Süslü ayraçlar içinde ada sahip dosya adlarını belirtmek için süslü ayraçlar çift.</span><span class="sxs-lookup"><span data-stu-id="d72ef-154">To specify file names that have curly braces in the name, double the curly braces.</span></span>
<span data-ttu-id="d72ef-155">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d72ef-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="d72ef-156">Bu yol adlı bir dosyayı bulur *{20140101}-soundfile.mp3* içinde *görüntüleri* klasörünü ve `name` işlev kodu değişken değerinin olacaktır *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="d72ef-156">This path would find a file named *{20140101}-soundfile.mp3* in the *images* folder, and the `name` variable value in the function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
The Azure Functions runtime makes sure that no external file trigger function gets called more than once for the same new or updated file.
It does so by maintaining *file receipts* to determine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in the Azure storage account for your function app
(specified by the `AzureWebJobsStorage` app setting). A file receipt has the following information:

* The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* The folder name
* The file type ("BlockFile" or "PageFile")
* The file name
* The ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

To force reprocessing of a file, delete the file receipt for that file from the *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="d72ef-157">Zararlı dosyaları işleme</span><span class="sxs-lookup"><span data-stu-id="d72ef-157">Handling poison files</span></span>
<span data-ttu-id="d72ef-158">Bir dış dosya Tetik işlevi başarısız olduğunda, Azure işlevleri, işlevi en fazla 5 kez (ilk denemede dahil) varsayılan olarak belirli bir dosya için yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="d72ef-158">When an external file trigger function fails, Azure Functions retries that function up to 5 times by default (including the first try) for a given file.</span></span>
<span data-ttu-id="d72ef-159">İşlevler tüm 5 deneme başarısız olursa adlı bir depolama kuyruğuna bir ileti ekler *webjobs apihubtrigger poison*.</span><span class="sxs-lookup"><span data-stu-id="d72ef-159">If all 5 tries fail, Functions adds a message to a Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="d72ef-160">Kuyruk iletisini zararlı dosyaları için aşağıdaki özellikleri içeren bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="d72ef-160">The queue message for poison files is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="d72ef-161">FunctionId (biçimde  *&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*)</span><span class="sxs-lookup"><span data-stu-id="d72ef-161">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="d72ef-162">Dosya türü</span><span class="sxs-lookup"><span data-stu-id="d72ef-162">FileType</span></span>
* <span data-ttu-id="d72ef-163">KlasörAdı</span><span class="sxs-lookup"><span data-stu-id="d72ef-163">FolderName</span></span>
* <span data-ttu-id="d72ef-164">Dosya adı</span><span class="sxs-lookup"><span data-stu-id="d72ef-164">FileName</span></span>
* <span data-ttu-id="d72ef-165">ETag (örneğin, bir dosya sürümü tanımlayıcısı: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="d72ef-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="d72ef-166">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="d72ef-166">Trigger usage</span></span>
<span data-ttu-id="d72ef-167">C# işlevlerde, girdi dosyası veri adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="d72ef-167">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="d72ef-168">Burada `T` veri türü, verileri seri durumdan istediğiniz olduğunda ve `paramName` , belirtilen adı [JSON tetiklemek](#trigger).</span><span class="sxs-lookup"><span data-stu-id="d72ef-168">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="d72ef-169">Giriş dosyası kullanarak veri erişim node.js işlevlerde `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d72ef-169">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d72ef-170">Dosya türlerinden herhangi birinde aşağıdaki seri durumdan çıkarılabiliyorsa:</span><span class="sxs-lookup"><span data-stu-id="d72ef-170">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="d72ef-171">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş dosya verileri için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="d72ef-172">Özel bir giriş türü bildirirseniz (örneğin `FooType`), Azure işlevleri, belirtilen türe JSON verilerini seri durumdan dener.</span><span class="sxs-lookup"><span data-stu-id="d72ef-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="d72ef-173">String - metin dosya verileri için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-173">String - useful for text file data.</span></span>

<span data-ttu-id="d72ef-174">C# işlevleri, şu türlerden birine de bağlayabilirsiniz ve işlevleri çalışma zamanı bu türünü kullanarak dosya verileri seri durumdan dener:</span><span class="sxs-lookup"><span data-stu-id="d72ef-174">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="d72ef-175">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="d72ef-175">Trigger sample</span></span>
<span data-ttu-id="d72ef-176">Bir dış dosya tetikleyicisi tanımlayan aşağıdaki function.json olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d72ef-176">Suppose you have the following function.json, that defines an external file trigger:</span></span>

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

<span data-ttu-id="d72ef-177">İzlenen klasöre eklenen her dosyanın içeriğini günlüklerini dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="d72ef-177">See the language-specific sample that logs the contents of each file that is added to the monitored folder.</span></span>

* [<span data-ttu-id="d72ef-178">C#</span><span class="sxs-lookup"><span data-stu-id="d72ef-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="d72ef-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="d72ef-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="d72ef-180">C# tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="d72ef-180">Trigger usage in C#</span></span> #

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

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="d72ef-181">Node.js tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="d72ef-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="d72ef-182">Dış dosya bağlama giriş</span><span class="sxs-lookup"><span data-stu-id="d72ef-182">External File input binding</span></span>
<span data-ttu-id="d72ef-183">Azure dış dosya giriş bağlaması, dış işlevinizi klasöründeki bir dosya kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d72ef-183">The Azure external file input binding enables you to use a file from an external folder in your function.</span></span>

<span data-ttu-id="d72ef-184">Bir işlev dış dosya girdisi aşağıdaki JSON nesneleri kullanır `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d72ef-184">The external file input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="d72ef-185">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d72ef-185">Note the following:</span></span>

* <span data-ttu-id="d72ef-186">`path`Klasör adı ve dosya adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d72ef-186">`path` must contain the folder name and the file name.</span></span> <span data-ttu-id="d72ef-187">Örneğin, bir [sıra tetikleyici](functions-bindings-storage-queue.md) işlevinizi, kullandığınız `"path": "samples-workitems/{queueTrigger}"` bir dosyaya işaret edecek şekilde `samples-workitems` tetikleyici iletisinde belirtilen dosya adıyla eşleşen bir ada sahip klasör.</span><span class="sxs-lookup"><span data-stu-id="d72ef-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="d72ef-188">Giriş kullanımı</span><span class="sxs-lookup"><span data-stu-id="d72ef-188">Input usage</span></span>
<span data-ttu-id="d72ef-189">C# işlevlerde, girdi dosyası veri adlandırılmış bir parametre gibi işlevi imzanız kullanarak bağladığınız `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="d72ef-189">In C# functions, you bind to the input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="d72ef-190">Burada `T` veri türü, verileri seri durumdan istediğiniz olduğunda ve `paramName` , belirtilen adı [bağlama giriş](#input).</span><span class="sxs-lookup"><span data-stu-id="d72ef-190">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="d72ef-191">Giriş dosyası kullanarak veri erişim node.js işlevlerde `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d72ef-191">In Node.js functions, you access the input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d72ef-192">Dosya türlerinden herhangi birinde aşağıdaki seri durumdan çıkarılabiliyorsa:</span><span class="sxs-lookup"><span data-stu-id="d72ef-192">The file can be deserialized into any of the following types:</span></span>

* <span data-ttu-id="d72ef-193">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirilmiş dosya verileri için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="d72ef-194">Özel bir giriş türü bildirirseniz (örneğin `InputType`), Azure işlevleri, belirtilen türe JSON verilerini seri durumdan dener.</span><span class="sxs-lookup"><span data-stu-id="d72ef-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="d72ef-195">String - metin dosya verileri için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-195">String - useful for text file data.</span></span>

<span data-ttu-id="d72ef-196">C# işlevleri, şu türlerden birine de bağlayabilirsiniz ve işlevleri çalışma zamanı bu türünü kullanarak dosya verileri seri durumdan dener:</span><span class="sxs-lookup"><span data-stu-id="d72ef-196">In C# functions, you can also bind to any of the following types, and the Functions runtime attempts to deserialize the file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="d72ef-197">Çıkış dış dosyası bağlama</span><span class="sxs-lookup"><span data-stu-id="d72ef-197">External File output binding</span></span>
<span data-ttu-id="d72ef-198">Azure dış dosya çıktı bağlama dosyaları işlevinizi dış bir klasörde yazma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d72ef-198">The Azure external file output binding enables you to write files to an external folder in your function.</span></span>

<span data-ttu-id="d72ef-199">Bir işlev aşağıdaki JSON nesneleri kullanan çıktısı dış dosya `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d72ef-199">The external file output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="d72ef-200">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d72ef-200">Note the following:</span></span>

* <span data-ttu-id="d72ef-201">`path`Klasör adı ve yazmak için dosya adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d72ef-201">`path` must contain the folder name and the file name to write to.</span></span> <span data-ttu-id="d72ef-202">Örneğin, bir [sıra tetikleyici](functions-bindings-storage-queue.md) işlevinizi, kullandığınız `"path": "samples-workitems/{queueTrigger}"` bir dosyaya işaret edecek şekilde `samples-workitems` tetikleyici iletisinde belirtilen dosya adıyla eşleşen bir ada sahip klasör.</span><span class="sxs-lookup"><span data-stu-id="d72ef-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` to point to a file in the `samples-workitems` folder with a name that matches the file name specified in the trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="d72ef-203">Çıktı kullanımı</span><span class="sxs-lookup"><span data-stu-id="d72ef-203">Output usage</span></span>
<span data-ttu-id="d72ef-204">C# işlevlerde, çıktı dosyasına adlandırılmış kullanarak bağladığınız `out` işlevi imzanız parametresinde ister `out <T> <name>`, burada `T` veri türü, verileri seri hale getirmek istediğiniz olduğunda ve `paramName` , belirtilen adı [bağlama çıktı](#output).</span><span class="sxs-lookup"><span data-stu-id="d72ef-204">In C# functions, you bind to the output file by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="d72ef-205">Çıkış dosyası kullanarak erişim node.js işlevlerde `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d72ef-205">In Node.js functions, you access the output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d72ef-206">Şu türlerden birini kullanarak çıktı dosyasına yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d72ef-206">You can write to the output file using any of the following types:</span></span>

* <span data-ttu-id="d72ef-207">Tüm [nesne](https://msdn.microsoft.com/library/system.object.aspx) - JSON serileştirmesi için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="d72ef-208">Özel çıkış türü bildirirseniz (örneğin `out OutputType paramName`), JSON içinde nesneyi serileştirmek Azure işlevleri çalışır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts to serialize object into JSON.</span></span> <span data-ttu-id="d72ef-209">Çıkış parametresi null ise, işlev çıktığında işlevleri çalışma zamanı null bir nesne bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d72ef-209">If the output parameter is null when the function exits, the Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="d72ef-210">String - (`out string paramName`) metin dosya verileri için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="d72ef-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="d72ef-211">işlev çıktığında yalnızca dize parametresi null olmayan ise işlevleri çalışma zamanı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d72ef-211">the Functions runtime creates a file only if the string parameter is non-null when the function exits.</span></span>

<span data-ttu-id="d72ef-212">C# işlevlerde şu türlerden birine de çıkarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d72ef-212">In C# functions you can also output to any of the following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="d72ef-213">Giriş + çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="d72ef-213">Input + Output sample</span></span>
<span data-ttu-id="d72ef-214">Aşağıdaki function.json olduğunu varsayalım tanımlayan bir [depolama kuyruğu tetikleyici](functions-bindings-storage-queue.md)dış dosyası giriş ve çıkış bir dış dosyası:</span><span class="sxs-lookup"><span data-stu-id="d72ef-214">Suppose you have the following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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

<span data-ttu-id="d72ef-215">Giriş dosyası çıktı dosyasına kopyalar dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="d72ef-215">See the language-specific sample that copies the input file to the output file.</span></span>

* [<span data-ttu-id="d72ef-216">C#</span><span class="sxs-lookup"><span data-stu-id="d72ef-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="d72ef-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="d72ef-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="d72ef-218">C# kullanımı</span><span class="sxs-lookup"><span data-stu-id="d72ef-218">Usage in C#</span></span> #

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

### <a name="usage-in-nodejs"></a><span data-ttu-id="d72ef-219">Node.js kullanımı</span><span class="sxs-lookup"><span data-stu-id="d72ef-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="d72ef-220">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d72ef-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
