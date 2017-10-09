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
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="b9894-104">Azure işlevleri Blob Depolama bağlamaları</span><span class="sxs-lookup"><span data-stu-id="b9894-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b9894-105">Bu makalede açıklanır nasıl tooconfigure ve Azure Blob Depolama bağlamaları Azure işlevlerinde ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="b9894-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="b9894-106">Azure işlevleri destekler tetikleyici, giriş ve Azure Blob Depolama bağlantılarında çıkış.</span><span class="sxs-lookup"><span data-stu-id="b9894-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="b9894-107">Tüm bağlama kullanılabilir olan özellikler için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="b9894-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="b9894-108">A [yalnızca depolama hesabı blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b9894-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="b9894-109">BLOB Depolama Tetikleyicileri ve bağlamaları genel amaçlı depolama hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b9894-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="b9894-110">BLOB Depolama Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="b9894-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="b9894-111">Yeni veya güncelleştirilmiş bir blob algılandığında hello Azure Blob Depolama tetikleyici kullanılarak, işlevi kodunuzu çağrılır.</span><span class="sxs-lookup"><span data-stu-id="b9894-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="b9894-112">Merhaba blob içeriklerini giriş toohello işlev olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b9894-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="b9894-113">Hello kullanarak blob depolama tetikleyici tanımlamak **tümleştir** hello işlevleri portalındaki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="b9894-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="b9894-114">Merhaba portal oluşturur hello tanımında aşağıdaki hello **bağlamaları** bölümünü *function.json*:</span><span class="sxs-lookup"><span data-stu-id="b9894-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="b9894-115">BLOB giriş ve çıkış bağlamalar kullanılarak tanımlanır `blob` hello bağlama türü olarak:</span><span class="sxs-lookup"><span data-stu-id="b9894-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="b9894-116">Merhaba `path` ifadeleri ve filtre parametrelerini bağlama özelliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="b9894-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="b9894-117">Bkz: [adı desenleri](#pattern).</span><span class="sxs-lookup"><span data-stu-id="b9894-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="b9894-118">Merhaba `connection` özelliği, depolama bağlantı dizesi içeren bir uygulama ayarı hello adını içermelidir.</span><span class="sxs-lookup"><span data-stu-id="b9894-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="b9894-119">Hello Azure portal, standart Düzenleyicisi'nde hello hello **tümleştir** sekmesinde bir depolama hesabı seçtiğinizde, bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b9894-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="b9894-120">Tüketim plan üzerinde bir blob tetikleyici kullanırken olabilir tooa 10 dakikalık gecikme bir işlev uygulaması boşta geçti sonra yeni BLOB'lar işleme.</span><span class="sxs-lookup"><span data-stu-id="b9894-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="b9894-121">Merhaba işlev uygulaması çalışmaya başladıktan sonra BLOB'ları hemen işlenir.</span><span class="sxs-lookup"><span data-stu-id="b9894-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="b9894-122">Bu ilk tooavoid gecikme, aşağıdaki seçenekleri şu hello birini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="b9894-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="b9894-123">Always On özellikli ile bir uygulama hizmeti planını kullan.</span><span class="sxs-lookup"><span data-stu-id="b9894-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="b9894-124">Başka bir mekanizma tootrigger hello blob hello blob adı içeren bir kuyruk iletisi gibi işlemleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9894-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="b9894-125">Bir örnek için bkz: [sıra tetikleyicisi blob ile girişi bağlamayı](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="b9894-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="b9894-126">Adı desenleri</span><span class="sxs-lookup"><span data-stu-id="b9894-126">Name patterns</span></span>
<span data-ttu-id="b9894-127">Bir blob adı deseni hello belirtebilirsiniz `path` filtre veya bağlama bir ifade olabilir özelliği.</span><span class="sxs-lookup"><span data-stu-id="b9894-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="b9894-128">Bkz: [ifadeleri ve desenler bağlama](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="b9894-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="b9894-129">Örneğin, "özgün," Merhaba dize ile başlayan toofilter tooblobs tanımı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9894-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="b9894-130">Bu yol adlı bir blob bulur *özgün Blob1.txt* hello içinde *giriş* kapsayıcı ve hello hello değerini `name` işlevi kodda değişkenidir `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="b9894-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="b9894-131">Ayrıca, toobind toohello blob dosya adını ve uzantısını iki desenlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9894-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="b9894-132">Bu yolu da adlı bir blob bulur *özgün Blob1.txt*ve hello hello değerini `blobname` ve `blobextension` değişkenleri işlevi kodda *özgün Blob1* ve *txt*.</span><span class="sxs-lookup"><span data-stu-id="b9894-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="b9894-133">Merhaba dosya uzantısı için sabit bir değer kullanarak hello dosya türü BLOB kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9894-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="b9894-134">Örneğin, tootrigger yalnızca dosyalarda .png desen aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="b9894-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="b9894-135">Süslü ayraçlar adı desenleri bulunan özel karakterleri var.</span><span class="sxs-lookup"><span data-stu-id="b9894-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="b9894-136">Süslü ayraçlar hello sahip toospecify blob adları, iki ayraçlar kullanılmasını hello kaşlı kaçış.</span><span class="sxs-lookup"><span data-stu-id="b9894-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="b9894-137">Merhaba aşağıdaki örnek bulur adlı bir blob *{20140101}-soundfile.mp3* hello içinde *görüntüleri* kapsayıcı ve hello `name` hello işlevi kodda değişken değeri  *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="b9894-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="b9894-138">Tetikleyici meta verileri</span><span class="sxs-lookup"><span data-stu-id="b9894-138">Trigger metadata</span></span>

<span data-ttu-id="b9894-139">Merhaba blob tetikleyici çeşitli meta veri özelliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9894-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="b9894-140">Bu özellikler, diğer bağlamaları bağlamaları ifadelerinde bir parçası olarak ya da kodunuzu parametre olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b9894-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="b9894-141">Merhaba bu değerlere sahip aynı topluca [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="b9894-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="b9894-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="b9894-142">**BlobTrigger**.</span></span> <span data-ttu-id="b9894-143">`string` yazın.</span><span class="sxs-lookup"><span data-stu-id="b9894-143">Type `string`.</span></span> <span data-ttu-id="b9894-144">Merhaba tetikleme blob yolu</span><span class="sxs-lookup"><span data-stu-id="b9894-144">hello triggering blob path</span></span>
- <span data-ttu-id="b9894-145">**URI**.</span><span class="sxs-lookup"><span data-stu-id="b9894-145">**Uri**.</span></span> <span data-ttu-id="b9894-146">`System.Uri` yazın.</span><span class="sxs-lookup"><span data-stu-id="b9894-146">Type `System.Uri`.</span></span> <span data-ttu-id="b9894-147">Merhaba birincil konumu için Hello blob'un URI.</span><span class="sxs-lookup"><span data-stu-id="b9894-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="b9894-148">**Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="b9894-148">**Properties**.</span></span> <span data-ttu-id="b9894-149">`Microsoft.WindowsAzure.Storage.Blob.BlobProperties` yazın.</span><span class="sxs-lookup"><span data-stu-id="b9894-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="b9894-150">BLOB'ın sistem özellikleri hello.</span><span class="sxs-lookup"><span data-stu-id="b9894-150">hello blob's system properties.</span></span>
- <span data-ttu-id="b9894-151">**Meta veri**.</span><span class="sxs-lookup"><span data-stu-id="b9894-151">**Metadata**.</span></span> <span data-ttu-id="b9894-152">`IDictionary<string,string>` yazın.</span><span class="sxs-lookup"><span data-stu-id="b9894-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="b9894-153">Merhaba kullanıcı tanımlı meta veriler hello blob.</span><span class="sxs-lookup"><span data-stu-id="b9894-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="b9894-154">BLOB giriş</span><span class="sxs-lookup"><span data-stu-id="b9894-154">Blob receipts</span></span>
<span data-ttu-id="b9894-155">Hello Azure işlevleri çalışma zamanı yok blob Tetik işlevi için birden çok kez çağrılır sağlar aynı yeni veya güncelleştirilmiş blob hello.</span><span class="sxs-lookup"><span data-stu-id="b9894-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="b9894-156">Belirtilen blob sürümü işlediğinde toodetermine sakladığı *blob giriş*.</span><span class="sxs-lookup"><span data-stu-id="b9894-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="b9894-157">Azure işlevleri depoları Alındılar adlı bir kapsayıcıda blob *azure Web işleri konakları* hello işlevi uygulamanız için Azure depolama hesabı içinde (Merhaba uygulama ayarı tarafından tanımlanan `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="b9894-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="b9894-158">Bir blob giriş bilgisinden hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b9894-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="b9894-159">Merhaba tetiklenen işlevi ("*&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*", örneğin:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="b9894-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="b9894-160">Merhaba kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="b9894-160">hello container name</span></span>
* <span data-ttu-id="b9894-161">Merhaba blob türü ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b9894-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b9894-162">Merhaba blob adı</span><span class="sxs-lookup"><span data-stu-id="b9894-162">hello blob name</span></span>
* <span data-ttu-id="b9894-163">Merhaba ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b9894-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="b9894-164">Merhaba silme hello blob giriş bu blob için tooforce bir blob yeniden işlemeyerek *azure Web işleri konakları* kapsayıcı el ile.</span><span class="sxs-lookup"><span data-stu-id="b9894-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="b9894-165">Zararlı BLOB'ları işleme</span><span class="sxs-lookup"><span data-stu-id="b9894-165">Handling poison blobs</span></span>
<span data-ttu-id="b9894-166">Belirli bir blob için bir blob Tetik işlevi başarısız olduğunda, Azure işlevleri, varsayılan olarak 5 kez toplam işlev yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="b9894-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="b9894-167">Tüm 5 deneme başarısız olursa, Azure işlevleri adlı bir ileti tooa depolama kuyruğu ekler *webjobs blobtrigger poison*.</span><span class="sxs-lookup"><span data-stu-id="b9894-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="b9894-168">Merhaba kuyruk iletisi zararlı BLOB'lar için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:</span><span class="sxs-lookup"><span data-stu-id="b9894-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="b9894-169">FunctionId (Merhaba biçiminde  *&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*)</span><span class="sxs-lookup"><span data-stu-id="b9894-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="b9894-170">BlobType ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b9894-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b9894-171">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="b9894-171">ContainerName</span></span>
* <span data-ttu-id="b9894-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="b9894-172">BlobName</span></span>
* <span data-ttu-id="b9894-173">ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b9894-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="b9894-174">Blob büyük kapsayıcıları için yoklama</span><span class="sxs-lookup"><span data-stu-id="b9894-174">Blob polling for large containers</span></span>
<span data-ttu-id="b9894-175">İzlenmekte olan hello blob kapsayıcısı 10. 000'den fazla BLOB'ları içeriyorsa, çalışma zamanı tarar hello işlevleri dosyaları toowatch yeni veya değiştirilmiş BLOB'lar için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b9894-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="b9894-176">Bu işlem, gerçek zamanlı değildir.</span><span class="sxs-lookup"><span data-stu-id="b9894-176">This process is not real time.</span></span> <span data-ttu-id="b9894-177">Merhaba blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil.</span><span class="sxs-lookup"><span data-stu-id="b9894-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="b9894-178">Ayrıca, [depolama günlüklerine "en iyi çaba" üzerinde oluşturulan](/rest/api/storageservices/About-Storage-Analytics-Logging) temel.</span><span class="sxs-lookup"><span data-stu-id="b9894-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="b9894-179">Tüm olayları yakalanır garantisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="b9894-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="b9894-180">Bazı koşullarda günlükleri eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9894-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="b9894-181">Daha hızlı veya daha güvenilir blob işleme gerekiyorsa oluşturma göz önünde bulundurun bir [kuyruk iletisi](../storage/queues/storage-dotnet-how-to-use-queues.md) hello blob oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="b9894-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="b9894-182">Ardından, bir [sıra tetikleyici](functions-bindings-storage-queue.md) blob tetikleyici tooprocess hello blob yerine.</span><span class="sxs-lookup"><span data-stu-id="b9894-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="b9894-183">Blob tetikleyici kullanılarak ve giriş bağlama</span><span class="sxs-lookup"><span data-stu-id="b9894-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="b9894-184">.NET işlevlerde gibi bir yöntem parametresi kullanılarak hello blob veri erişim `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="b9894-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="b9894-185">Burada, `paramName` hello belirtilen hello değeri [tetikleyici yapılandırma](#trigger).</span><span class="sxs-lookup"><span data-stu-id="b9894-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="b9894-186">Node.js işlevlerde erişim hello giriş blob verilerini kullanarak `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b9894-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="b9894-187">.NET ile Merhaba aşağıdaki listede hello türlerinin tooany bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9894-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="b9894-188">Giriş bağlama olarak kullandıysanız, bu türlerinden bazıları gerektiren bir `inout` yönde bağlama *function.json*.</span><span class="sxs-lookup"><span data-stu-id="b9894-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="b9894-189">Düzenleyici Gelişmiş hello kullanmalısınız bu yönünü hello standart Düzenleyicisi tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="b9894-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="b9894-190">`ICloudBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="b9894-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="b9894-191">`CloudBlockBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="b9894-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="b9894-192">`CloudPageBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="b9894-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="b9894-193">`CloudAppendBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="b9894-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="b9894-194">Metin BLOB'ları beklenir, tooa .NET de bağlayabilirsiniz `string` türü.</span><span class="sxs-lookup"><span data-stu-id="b9894-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="b9894-195">Bu, yalnızca Hello tüm blob içeriklerini belleğe yüklenen gibi hello blob boyutu, küçükse önerilir.</span><span class="sxs-lookup"><span data-stu-id="b9894-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="b9894-196">Genellikle, tercih toouse olan bir `Stream` veya `CloudBlockBlob` türü.</span><span class="sxs-lookup"><span data-stu-id="b9894-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="b9894-197">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="b9894-197">Trigger sample</span></span>
<span data-ttu-id="b9894-198">Bir blob depolama tetikleyici tanımlar function.json aşağıdaki hello olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="b9894-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="b9894-199">Merhaba içeriğine toohello izlenen kapsayıcı eklenen her bir blob günlüklerini hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="b9894-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="b9894-200">C#</span><span class="sxs-lookup"><span data-stu-id="b9894-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b9894-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="b9894-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="b9894-202">BLOB tetikleyici örnekler C#</span><span class="sxs-lookup"><span data-stu-id="b9894-202">Blob trigger examples in C#</span></span> #

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

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="b9894-203">Tetikleyici örnekte Node.js</span><span class="sxs-lookup"><span data-stu-id="b9894-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="b9894-204">Bir blob kullanarak çıktıyı bağlama</span><span class="sxs-lookup"><span data-stu-id="b9894-204">Using a blob output binding</span></span>

<span data-ttu-id="b9894-205">.NET işlevlerde ya da kullanım gereken bir `out string` parametresi işlev imzası veya hello türlerinin listesi aşağıdaki hello kullanımı.</span><span class="sxs-lookup"><span data-stu-id="b9894-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="b9894-206">Node.js işlevlerde hello çıkış blob kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="b9894-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="b9894-207">.NET işlevlerde şu türlerini hello tooany çıkarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b9894-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="b9894-208">Sıra tetikleyiciyle blob girdi ve çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="b9894-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="b9894-209">Function.json aşağıdaki hello olduğunu varsayalım tanımlayan bir [kuyruk depolama tetikleyici](functions-bindings-storage-queue.md)bir blob depolama giriş ve bir blob depolama çıkış.</span><span class="sxs-lookup"><span data-stu-id="b9894-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="b9894-210">Bildirim hello hello kullanımını `queueTrigger` meta veri özelliği.</span><span class="sxs-lookup"><span data-stu-id="b9894-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="b9894-211">Giriş ve çıkış hello blob içinde `path` özellikleri:</span><span class="sxs-lookup"><span data-stu-id="b9894-211">in hello blob input and output `path` properties:</span></span>

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

<span data-ttu-id="b9894-212">Merhaba giriş blob toohello çıkış blob kopyalar hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="b9894-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="b9894-213">C#</span><span class="sxs-lookup"><span data-stu-id="b9894-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="b9894-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="b9894-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="b9894-215">BLOB bağlama örnek C#</span><span class="sxs-lookup"><span data-stu-id="b9894-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="b9894-216">BLOB bağlama Node.js örneğinde</span><span class="sxs-lookup"><span data-stu-id="b9894-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="b9894-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9894-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

