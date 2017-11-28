---
title: "Azure işlevleri Blob Storage bağlamaları | Microsoft Docs"
description: "Azure Storage Tetikleyicileri ve bağlamaları Azure işlevlerinde kullanmayı öğrenme."
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
ms.openlocfilehash: 8d8f510ec906c0e0420ec48d45d88b93c144658a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="a1c05-104">Azure işlevleri Blob Depolama bağlamaları</span><span class="sxs-lookup"><span data-stu-id="a1c05-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="a1c05-105">Bu makalede, yapılandırma ve Azure Blob Depolama bağlamaları Azure işlevlerinde çalışmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1c05-105">This article explains how to configure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="a1c05-106">Azure işlevleri destekler tetikleyici, giriş ve Azure Blob Depolama bağlantılarında çıkış.</span><span class="sxs-lookup"><span data-stu-id="a1c05-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="a1c05-107">Tüm bağlama kullanılabilir olan özellikler için bkz: [Azure işlevleri Tetikleyicileri ve bağlamaları kavramları](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="a1c05-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="a1c05-108">A [yalnızca depolama hesabı blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a1c05-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="a1c05-109">BLOB Depolama Tetikleyicileri ve bağlamaları genel amaçlı depolama hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="a1c05-110">BLOB Depolama Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="a1c05-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="a1c05-111">Azure Blob Depolama tetikleyici kullanarak, yeni veya güncelleştirilmiş bir blob algılandığında işlevi kodunuzu adı verilir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-111">Using the Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="a1c05-112">Blob içeriklerini işleve giriş olarak sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a1c05-112">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="a1c05-113">Bir blob depolama tetikleyici kullanarak tanımlarsınız **tümleştir** işlevleri portalındaki sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a1c05-113">Define a blob storage trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="a1c05-114">Portal aşağıdaki tanımında oluşturur **bağlamaları** bölümünü *function.json*:</span><span class="sxs-lookup"><span data-stu-id="a1c05-114">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<The name used to identify the trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="a1c05-115">BLOB giriş ve çıkış bağlamalar kullanılarak tanımlanır `blob` bağlama türü olarak:</span><span class="sxs-lookup"><span data-stu-id="a1c05-115">Blob input and output bindings are defined using `blob` as the binding type:</span></span>

```json
{
  "name": "<The name used to identify the blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="a1c05-116">`path` İfadeleri ve filtre parametrelerini bağlama özelliğini destekler.</span><span class="sxs-lookup"><span data-stu-id="a1c05-116">The `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="a1c05-117">Bkz: [adı desenleri](#pattern).</span><span class="sxs-lookup"><span data-stu-id="a1c05-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="a1c05-118">`connection` Özelliği, depolama bağlantı dizesi içeren bir uygulama ayarı adı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-118">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="a1c05-119">Standart Düzenleyici'de Azure portalında **tümleştir** sekmesinde bir depolama hesabı seçtiğinizde, bu uygulama ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a1c05-119">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="a1c05-120">Tüketim plan üzerinde bir blob tetikleyici kullanırken olabilir en fazla 10 dakikalık bir gecikmeyle bir işlev uygulaması boşta geçti sonra yeni BLOB'lar işleme.</span><span class="sxs-lookup"><span data-stu-id="a1c05-120">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="a1c05-121">İşlev uygulaması çalışmaya başladıktan sonra BLOB'ları hemen işlenir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-121">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="a1c05-122">Bu ilk gecikmeyi önlemek için aşağıdaki seçeneklerden birini göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="a1c05-122">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="a1c05-123">Always On özellikli ile bir uygulama hizmeti planını kullan.</span><span class="sxs-lookup"><span data-stu-id="a1c05-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="a1c05-124">Başka bir mekanizma, blob adı içeren bir kuyruk iletisi gibi işleme blob tetiklemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-124">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="a1c05-125">Bir örnek için bkz: [sıra tetikleyicisi blob ile girişi bağlamayı](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="a1c05-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="a1c05-126">Adı desenleri</span><span class="sxs-lookup"><span data-stu-id="a1c05-126">Name patterns</span></span>
<span data-ttu-id="a1c05-127">Bir blob adı desende belirtebilirsiniz `path` filtre veya bağlama bir ifade olabilir özelliği.</span><span class="sxs-lookup"><span data-stu-id="a1c05-127">You can specify a blob name pattern in the `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="a1c05-128">Bkz: [ifadeleri ve desenler bağlama](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="a1c05-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="a1c05-129">Örneğin, "özgün" dizesiyle başlayan BLOB'ları için filtre uygulamak için aşağıdaki tanımını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-129">For example, to filter to blobs that start with the string "original," use the following definition.</span></span> <span data-ttu-id="a1c05-130">Bu yol adlı bir blob bulur *özgün Blob1.txt* içinde *giriş* kapsayıcı ve değerini `name` işlevi kodda değişkenidir `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="a1c05-130">This path finds a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="a1c05-131">Blob dosya adını ve uzantısını ayrı olarak bağlamak için iki desenlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-131">To bind to the blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="a1c05-132">Bu yolu da adlı bir blob bulur *özgün Blob1.txt*, değerini `blobname` ve `blobextension` değişkenleri işlevi kodda *özgün Blob1* ve *txt*.</span><span class="sxs-lookup"><span data-stu-id="a1c05-132">This path also finds a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="a1c05-133">Dosya uzantısı için sabit bir değer kullanarak BLOB dosya türünü kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c05-133">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="a1c05-134">Örneğin, yalnızca .png dosyalarda tetiklemek için şu biçimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="a1c05-134">For instance, to trigger only on .png files, use the following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="a1c05-135">Süslü ayraçlar adı desenleri bulunan özel karakterleri var.</span><span class="sxs-lookup"><span data-stu-id="a1c05-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="a1c05-136">Süslü ayraçlar sahip blob adlarını belirtmek için iki ayraçlar kullanılmasını küme ayraçları kaçış.</span><span class="sxs-lookup"><span data-stu-id="a1c05-136">To specify blob names that have curly braces in the name, you can escape the braces using two braces.</span></span> <span data-ttu-id="a1c05-137">Aşağıdaki örnek adlı bir blob bulur *{20140101}-soundfile.mp3* içinde *görüntüleri* kapsayıcı ve `name` işlevi kodda değişken değeri *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="a1c05-137">The following example finds a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="a1c05-138">Tetikleyici meta verileri</span><span class="sxs-lookup"><span data-stu-id="a1c05-138">Trigger metadata</span></span>

<span data-ttu-id="a1c05-139">Blob tetikleyici çeşitli meta veri özelliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1c05-139">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="a1c05-140">Bu özellikler, diğer bağlamaları bağlamaları ifadelerinde bir parçası olarak ya da kodunuzu parametre olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="a1c05-141">Bu değerler olarak aynı semantiklerine sahip [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="a1c05-141">These values have the same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="a1c05-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="a1c05-142">**BlobTrigger**.</span></span> <span data-ttu-id="a1c05-143">`string` yazın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-143">Type `string`.</span></span> <span data-ttu-id="a1c05-144">Tetikleyici blob yolu</span><span class="sxs-lookup"><span data-stu-id="a1c05-144">The triggering blob path</span></span>
- <span data-ttu-id="a1c05-145">**URI**.</span><span class="sxs-lookup"><span data-stu-id="a1c05-145">**Uri**.</span></span> <span data-ttu-id="a1c05-146">`System.Uri` yazın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-146">Type `System.Uri`.</span></span> <span data-ttu-id="a1c05-147">Birincil konumu için blob'un URI.</span><span class="sxs-lookup"><span data-stu-id="a1c05-147">The blob's URI for the primary location.</span></span>
- <span data-ttu-id="a1c05-148">**Özellikler**.</span><span class="sxs-lookup"><span data-stu-id="a1c05-148">**Properties**.</span></span> <span data-ttu-id="a1c05-149">`Microsoft.WindowsAzure.Storage.Blob.BlobProperties` yazın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="a1c05-150">Blob'un Sistem Özellikleri.</span><span class="sxs-lookup"><span data-stu-id="a1c05-150">The blob's system properties.</span></span>
- <span data-ttu-id="a1c05-151">**Meta veri**.</span><span class="sxs-lookup"><span data-stu-id="a1c05-151">**Metadata**.</span></span> <span data-ttu-id="a1c05-152">`IDictionary<string,string>` yazın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="a1c05-153">Kullanıcı tanımlı meta veriler blob'a.</span><span class="sxs-lookup"><span data-stu-id="a1c05-153">The user-defined metadata for the blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="a1c05-154">BLOB giriş</span><span class="sxs-lookup"><span data-stu-id="a1c05-154">Blob receipts</span></span>
<span data-ttu-id="a1c05-155">Azure işlevleri çalışma zamanı yok blob Tetik işlevi için aynı yeni veya güncelleştirilmiş blob birden çok kez çağrılır sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1c05-155">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="a1c05-156">Belirtilen blob sürümü işlediğinde tutar belirlemek için *blob giriş*.</span><span class="sxs-lookup"><span data-stu-id="a1c05-156">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="a1c05-157">Azure işlevleri depoları Alındılar adlı bir kapsayıcıda blob *azure Web işleri konakları* işlev uygulamanız için Azure depolama hesabında (uygulama ayarı tarafından tanımlanan `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="a1c05-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="a1c05-158">Bir blob giriş aşağıdaki bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="a1c05-158">A blob receipt has the following information:</span></span>

* <span data-ttu-id="a1c05-159">Tetiklenen işlevi ("*&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*", örneğin:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="a1c05-159">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="a1c05-160">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="a1c05-160">The container name</span></span>
* <span data-ttu-id="a1c05-161">Blob türü ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="a1c05-161">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a1c05-162">Blob adı</span><span class="sxs-lookup"><span data-stu-id="a1c05-162">The blob name</span></span>
* <span data-ttu-id="a1c05-163">ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="a1c05-163">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a1c05-164">Bir blob yeniden işlemeyerek zorlamak için bu blobundan blob giriş silme *azure Web işleri konakları* kapsayıcı el ile.</span><span class="sxs-lookup"><span data-stu-id="a1c05-164">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="a1c05-165">Zararlı BLOB'ları işleme</span><span class="sxs-lookup"><span data-stu-id="a1c05-165">Handling poison blobs</span></span>
<span data-ttu-id="a1c05-166">Belirli bir blob için bir blob Tetik işlevi başarısız olduğunda, Azure işlevleri, varsayılan olarak 5 kez toplam işlev yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="a1c05-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="a1c05-167">Tüm 5 deneme başarısız olursa, Azure işlevleri adlı bir depolama kuyruğuna bir ileti ekler *webjobs blobtrigger poison*.</span><span class="sxs-lookup"><span data-stu-id="a1c05-167">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="a1c05-168">Kuyruk iletisini zararlı BLOB'lar için aşağıdaki özellikleri içeren bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="a1c05-168">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="a1c05-169">FunctionId (biçimde  *&lt;işlevi uygulama adı >*. İşlevler.  *&lt;işlev adı >*)</span><span class="sxs-lookup"><span data-stu-id="a1c05-169">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="a1c05-170">BlobType ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="a1c05-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a1c05-171">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="a1c05-171">ContainerName</span></span>
* <span data-ttu-id="a1c05-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="a1c05-172">BlobName</span></span>
* <span data-ttu-id="a1c05-173">ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="a1c05-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="a1c05-174">Blob büyük kapsayıcıları için yoklama</span><span class="sxs-lookup"><span data-stu-id="a1c05-174">Blob polling for large containers</span></span>
<span data-ttu-id="a1c05-175">İzlenmekte olan blob kapsayıcısı 10. 000'den fazla BLOB'ları içeriyorsa, işlevleri çalışma zamanı taramaları için yeni veya değiştirilmiş BLOB'lar izlemek için günlük dosyalarını.</span><span class="sxs-lookup"><span data-stu-id="a1c05-175">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="a1c05-176">Bu işlem, gerçek zamanlı değildir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-176">This process is not real time.</span></span> <span data-ttu-id="a1c05-177">Blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil.</span><span class="sxs-lookup"><span data-stu-id="a1c05-177">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="a1c05-178">Ayrıca, [depolama günlüklerine "en iyi çaba" üzerinde oluşturulan](/rest/api/storageservices/About-Storage-Analytics-Logging) temel.</span><span class="sxs-lookup"><span data-stu-id="a1c05-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="a1c05-179">Tüm olayları yakalanır garantisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="a1c05-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="a1c05-180">Bazı koşullarda günlükleri eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="a1c05-181">Daha hızlı veya daha güvenilir blob işleme gerekiyorsa oluşturma göz önünde bulundurun bir [kuyruk iletisi](../storage/queues/storage-dotnet-how-to-use-queues.md) blob oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="a1c05-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="a1c05-182">Ardından, bir [sıra tetikleyici](functions-bindings-storage-queue.md) blob işlemek için bir blob tetikleyici yerine.</span><span class="sxs-lookup"><span data-stu-id="a1c05-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="a1c05-183">Blob tetikleyici kullanılarak ve giriş bağlama</span><span class="sxs-lookup"><span data-stu-id="a1c05-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="a1c05-184">.NET işlevlerde gibi bir yöntem parametresi kullanılarak blob veri erişim `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="a1c05-184">In .NET functions, access the blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="a1c05-185">Burada, `paramName` , belirtilen değer [tetikleyici yapılandırma](#trigger).</span><span class="sxs-lookup"><span data-stu-id="a1c05-185">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="a1c05-186">Node.js işlevlerde kullanarak giriş blob veri erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="a1c05-186">In Node.js functions, access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="a1c05-187">.NET içinde aşağıdaki listede türlerinden herhangi birini bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1c05-187">In .NET, you can bind to any of the types in the list below.</span></span> <span data-ttu-id="a1c05-188">Giriş bağlama olarak kullandıysanız, bu türlerinden bazıları gerektiren bir `inout` yönde bağlama *function.json*.</span><span class="sxs-lookup"><span data-stu-id="a1c05-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="a1c05-189">Gelişmiş Düzenleyicisi'ni kullanmanız gerekir böylece bu yönünü standart Düzenleyicisi tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a1c05-189">This direction is not supported by the standard editor, so you must use the advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="a1c05-190">`ICloudBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="a1c05-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="a1c05-191">`CloudBlockBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="a1c05-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="a1c05-192">`CloudPageBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="a1c05-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="a1c05-193">`CloudAppendBlob`("ınout" bağlama yönü gerektirir)</span><span class="sxs-lookup"><span data-stu-id="a1c05-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="a1c05-194">Metin BLOB'ları beklenen, bir .NET de bağlayabilirsiniz `string` türü.</span><span class="sxs-lookup"><span data-stu-id="a1c05-194">If text blobs are expected, you can also bind to a .NET `string` type.</span></span> <span data-ttu-id="a1c05-195">Bu, yalnızca tüm blob içeriklerini belleğe yüklenen olarak blob boyutu, küçükse önerilir.</span><span class="sxs-lookup"><span data-stu-id="a1c05-195">This is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="a1c05-196">Genellikle, kullanılması tercih edilir bir `Stream` veya `CloudBlockBlob` türü.</span><span class="sxs-lookup"><span data-stu-id="a1c05-196">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="a1c05-197">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="a1c05-197">Trigger sample</span></span>
<span data-ttu-id="a1c05-198">Bir blob depolama tetikleyici tanımlar aşağıdaki function.json olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="a1c05-198">Suppose you have the following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="a1c05-199">İzlenen kapsayıcıya eklenen her bir blob içeriğini günlüklerini dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-199">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="a1c05-200">C#</span><span class="sxs-lookup"><span data-stu-id="a1c05-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="a1c05-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="a1c05-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="a1c05-202">BLOB tetikleyici örnekler C#</span><span class="sxs-lookup"><span data-stu-id="a1c05-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding to a CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="a1c05-203">Tetikleyici örnekte Node.js</span><span class="sxs-lookup"><span data-stu-id="a1c05-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="a1c05-204">Bir blob kullanarak çıktıyı bağlama</span><span class="sxs-lookup"><span data-stu-id="a1c05-204">Using a blob output binding</span></span>

<span data-ttu-id="a1c05-205">.NET işlevlerde ya da kullanım gereken bir `out string` işlev imzası veya kullanım türlerinden birini aşağıdaki listede parametresi.</span><span class="sxs-lookup"><span data-stu-id="a1c05-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of the types in the following list.</span></span> <span data-ttu-id="a1c05-206">Node.js işlevlerde çıkış blob kullanarak erişim `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="a1c05-206">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="a1c05-207">.NET işlevlerde şu türlerden birine çıkarabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a1c05-207">In .NET functions you can output to any of the following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="a1c05-208">Sıra tetikleyiciyle blob girdi ve çıktı örneği</span><span class="sxs-lookup"><span data-stu-id="a1c05-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="a1c05-209">Aşağıdaki function.json olduğunu varsayalım tanımlayan bir [kuyruk depolama tetikleyici](functions-bindings-storage-queue.md)bir blob depolama giriş ve bir blob depolama çıkış.</span><span class="sxs-lookup"><span data-stu-id="a1c05-209">Suppose you have the following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="a1c05-210">Kullanımına dikkat edin `queueTrigger` meta veri özelliği.</span><span class="sxs-lookup"><span data-stu-id="a1c05-210">Notice the use of the `queueTrigger` metadata property.</span></span> <span data-ttu-id="a1c05-211">blob giriş ve çıkış `path` özellikleri:</span><span class="sxs-lookup"><span data-stu-id="a1c05-211">in the blob input and output `path` properties:</span></span>

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

<span data-ttu-id="a1c05-212">Giriş blob çıkış blob kopyalar dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="a1c05-212">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="a1c05-213">C#</span><span class="sxs-lookup"><span data-stu-id="a1c05-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="a1c05-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="a1c05-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="a1c05-215">BLOB bağlama örnek C#</span><span class="sxs-lookup"><span data-stu-id="a1c05-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input to output, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="a1c05-216">BLOB bağlama Node.js örneğinde</span><span class="sxs-lookup"><span data-stu-id="a1c05-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input to output, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="a1c05-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1c05-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

