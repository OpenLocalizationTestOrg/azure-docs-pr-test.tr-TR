---
title: aaaHow toouse hello WebJobs SDK ile Azure blob storage
description: "Nasıl toouse Azure blob depolama hello WebJobs SDK ile bilgi edinin. Yeni bir blob bir kapsayıcıda görüntülendiğinde bir işlem tetikleyebilir ve 'zararlı BLOB' tanıtıcı."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="ca0ef-104">Nasıl toouse Azure blob depolama hello WebJobs SDK ile</span><span class="sxs-lookup"><span data-stu-id="ca0ef-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="ca0ef-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ca0ef-105">Overview</span></span>
<span data-ttu-id="ca0ef-106">Bu kılavuz C# sağlar kod örnekleri gösteren nasıl tootrigger bir Azure blob oluşturulduğunda veya bir işlem.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="ca0ef-107">Merhaba kod örnekleri kullan [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="ca0ef-108">BLOB'nasıl toocreate gösteren kod örnekleri için bkz: [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="ca0ef-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="ca0ef-109">Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya çok[birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="ca0ef-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="ca0ef-110"><a id="trigger"></a>Nasıl tootrigger blob oluşturulduğunda veya bir işlevi</span><span class="sxs-lookup"><span data-stu-id="ca0ef-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="ca0ef-111">Bu bölümde gösterilmiştir nasıl toouse hello `BlobTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="ca0ef-112">Yeni veya değiştirilmiş BLOB'lar için Web işleri SDK'si taramaları günlük dosyaları toowatch hello.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="ca0ef-113">Bu işlem, gerçek zamanlı değildir; Merhaba blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="ca0ef-114">Ayrıca, [depolama günlüklerine "en iyi çaba" üzerinde oluşturulan](https://msdn.microsoft.com/library/azure/hh343262.aspx) temel; tüm olayları Yakalanacak garantisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="ca0ef-115">Bazı koşullarda günlükleri eksik.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="ca0ef-116">Merhaba hızı ve güvenilirliği sınırlamaları blob tetikleyicileri, uygulamanız için kabul edilebilir değilse, hello yöntemi toocreate bir kuyruk iletisi hello blob oluşturun ve hello kullandığınızda önerilir [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) yerine özniteliği Merhaba `BlobTrigger` hello blob işler hello işlevi özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="ca0ef-117">Blob adı uzantısı için tek bir yer tutucu</span><span class="sxs-lookup"><span data-stu-id="ca0ef-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="ca0ef-118">Merhaba aşağıdaki kod örneği görüntülenen metin BLOB'ları hello kopyalar *giriş* kapsayıcı toohello *çıkış* kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="ca0ef-119">Merhaba öznitelik oluşturucunun hello kapsayıcı adı ve hello blob adı için bir yer tutucu belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="ca0ef-120">Bu örnekte, bir blob adlandırırsanız *Blob1.txt* hello oluşturulur *giriş* kapsayıcısının hello işlev oluşturur adlı bir blob *Blob1.txt* hello içinde *çıkış*  kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="ca0ef-121">Aşağıdaki kod örneği hello gösterildiği gibi hello blob adı tutucuyla adı düzeni belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="ca0ef-122">Bu kodu "özgün-" ile başlayan adlara sahip yalnızca BLOB'ları kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="ca0ef-123">Örneğin, *özgün Blob1.txt* hello içinde *giriş* kapsayıcı çok kopyalanan*kopya Blob1.txt* hello içinde *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="ca0ef-124">Süslü ayraçlar hello sahip blob adları için toospecify adı deseni gerekiyorsa hello süslü ayraçlar çift.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="ca0ef-125">Merhaba toofind blobları isterseniz, örneğin, *görüntüleri* böyle adlara sahip kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="ca0ef-126">Bu, düzeni için kullanın:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="ca0ef-127">Merhaba örnekte hello *adı* yer tutucu değerini olacaktır *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="ca0ef-128">Ayrı bir blob adı ve uzantısı yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="ca0ef-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="ca0ef-129">hello görünür BLOB'ları kopyalar hello aşağıdaki kod örnek değişikliklerini dosya uzantısı hello *giriş* kapsayıcı toohello *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="ca0ef-130">Merhaba kodunu günlüğe yazar hello hello uzantısı *giriş* blob ve hello hello uzantısı ayarlar *çıkış* çok blob*.txt*.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <span data-ttu-id="ca0ef-131"><a id="types"></a>Tooblobs bağlayabilirsiniz türleri</span><span class="sxs-lookup"><span data-stu-id="ca0ef-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="ca0ef-132">Merhaba kullanabilirsiniz `BlobTrigger` şu türlerini hello özniteliği:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="ca0ef-133">Tarafından seri diğer türleri [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="ca0ef-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="ca0ef-134">Hello Azure depolama hesabı ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir `CloudStorageAccount` parametre toohello yöntemi imzası.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="ca0ef-135">Merhaba örnekler için bkz [blob Github.com'u hello azure webjobs sdk havuzda bağlama kodda](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="ca0ef-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="ca0ef-136"><a id="string"></a>Bağlama toostring tarafından metin blob içeriği alma</span><span class="sxs-lookup"><span data-stu-id="ca0ef-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="ca0ef-137">Metin BLOB'ları beklenir, `BlobTrigger` uygulanan tooa olabilir `string` parametresi.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="ca0ef-138">Merhaba aşağıdaki kod örneği bağlar metin blob tooa `string` adlı parametre `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="ca0ef-139">Merhaba işlevi hello blob toohello WebJobs SDK Pano Bu parametre toowrite hello içeriğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="ca0ef-140"><a id="icbsb"></a>Blob içeriğinin ICloudBlobStreamBinder kullanarak serileştirilen alma</span><span class="sxs-lookup"><span data-stu-id="ca0ef-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="ca0ef-141">Merhaba aşağıdaki kod örneği kullanan uygulayan bir sınıf `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind blob toohello özniteliği `WebImage` türü.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="ca0ef-142">Merhaba `WebImage` kod bağlama sağlanır bir `WebImageBinder` öğesinden türetilen sınıf `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="ca0ef-143">Blob tetikleme Merhaba Hello blob yolu alınıyor</span><span class="sxs-lookup"><span data-stu-id="ca0ef-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="ca0ef-144">tooget hello kapsayıcı adı ve hello işlevi tetikleyen hello blobu blob adını içeren bir `blobTrigger` hello işlev imzası parametresinde dize.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="ca0ef-145"><a id="poison"></a>Nasıl toohandle poison BLOB</span><span class="sxs-lookup"><span data-stu-id="ca0ef-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="ca0ef-146">Zaman bir `BlobTrigger` işlevi başarısız oldu, hello SDK çağırır onu yeniden durumda hello hatası tarafından geçici bir hata neden oldu.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="ca0ef-147">Merhaba blob hello içeriğe göre Hello hatasına neden oldu tooprocess hello blob çalışır her zaman hello işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="ca0ef-148">Varsayılan olarak, hello SDK too5 kez bir işlev için belirli bir blob çağırır.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="ca0ef-149">Merhaba beşinci deneme başarısız olursa, hello SDK adlı bir ileti tooa sırası ekler *webjobs blobtrigger poison*.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="ca0ef-150">Merhaba en fazla yeniden deneme sayısı yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="ca0ef-151">aynı hello [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ayarı zararlı blob işleme ve zararlı sıraya ileti işleme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="ca0ef-152">Merhaba kuyruk iletisi zararlı BLOB'lar için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="ca0ef-153">FunctionId (Merhaba biçiminde *{Web işi adı}*. İşlevler. *{İşlev adı}*, örneğin: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="ca0ef-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="ca0ef-154">BlobType ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="ca0ef-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ca0ef-155">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="ca0ef-155">ContainerName</span></span>
* <span data-ttu-id="ca0ef-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="ca0ef-156">BlobName</span></span>
* <span data-ttu-id="ca0ef-157">ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="ca0ef-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="ca0ef-158">Merhaba aşağıdaki örnek, hello kod `CopyBlob` işlev her çağrıldığında, toofail neden olan kod bulunur.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="ca0ef-159">Sonra Hello SDK çağrıları, hello en fazla yeniden deneme sayısı için hello zararlı blob sırada bir ileti oluşturulur ve bu ileti hello tarafından işlenir `LogPoisonBlob` işlevi.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="ca0ef-160">Merhaba SDK hello JSON ileti otomatik olarak seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="ca0ef-161">Merhaba işte `PoisonBlobMessage` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="ca0ef-162"><a id="polling"></a>BLOB yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="ca0ef-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="ca0ef-163">Merhaba WebJobs SDK tarafından belirtilen tüm kapsayıcıları tarar `BlobTrigger` uygulama başlangıcında öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="ca0ef-164">Yeni BLOB'lar bulunan önce biraz olabilir şekilde büyük depolama hesabı bu tarama biraz zaman alabilir ve `BlobTrigger` işlevleri çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="ca0ef-165">toodetect yeni veya değiştirilmiş BLOB'lar uygulama başlatma sonra SDK düzenli aralıklarla hello blob depolama alanından okur hello günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="ca0ef-166">Merhaba blob günlükleri arabelleğe alınmış ve yalnızca fiziksel olarak her 10 dakikada yazılan veya bu nedenle, bu nedenle önemli gecikme olabileceğini blob oluşturulmuş veya hello karşılık gelen önce güncelleştirilmiş sonra `BlobTrigger` işlevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="ca0ef-167">Hello kullanarak oluşturduğunuz BLOB'ları için bir özel durum var. `Blob` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="ca0ef-168">Merhaba WebJobs SDK yeni blob oluşturduğunda, hello yeni blob hemen geçtikten tooany eşleşen `BlobTrigger` işlevleri.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="ca0ef-169">Blob girişleri ve çıkışları zinciri varsa, bu nedenle hello SDK bunları verimli bir şekilde işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="ca0ef-170">Ancak, düşük gecikme süresi, blob işleme işlevleri için oluşturulmuş veya başka yollarla güncelleştirilmiş BLOB'ları çalıştıran istiyorsanız, kullanmanızı öneririz `QueueTrigger` yerine `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="ca0ef-171"><a id="receipts"></a>BLOB giriş</span><span class="sxs-lookup"><span data-stu-id="ca0ef-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="ca0ef-172">Merhaba WebJobs SDK emin olur hiçbir `BlobTrigger` işlevi birden çok kez Merhaba aynı yeni adlı veya blob güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="ca0ef-173">Bunu tutarak yapar *blob giriş* verilen blob sürümü işlediğinde sipariş toodetermine içinde.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="ca0ef-174">BLOB giriş adlı bir kapsayıcıda depolanır *azure Web işleri konakları* hello AzureWebJobsStorage bağlantı dizesi tarafından belirtilen hello Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="ca0ef-175">Bir blob giriş bilgisinden hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="ca0ef-176">Merhaba hello blobu çağrıldı işlevi ("*{Web işi adı}*. İşlevler. *{İşlev adı}*", örneğin:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="ca0ef-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="ca0ef-177">Merhaba kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="ca0ef-177">hello container name</span></span>
* <span data-ttu-id="ca0ef-178">Merhaba blob türü ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="ca0ef-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="ca0ef-179">Merhaba blob adı</span><span class="sxs-lookup"><span data-stu-id="ca0ef-179">hello blob name</span></span>
* <span data-ttu-id="ca0ef-180">Merhaba ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="ca0ef-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="ca0ef-181">Tooforce bir blob yeniden işleme istiyorsanız, o blob için hello blob giriş hello el ile silebilirsiniz *azure Web işleri konakları* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="ca0ef-182"><a id="queues"></a>Merhaba sıraları makalesiyle kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="ca0ef-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="ca0ef-183">Nasıl toohandle blob işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, belirli tooblob bakın [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="ca0ef-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="ca0ef-184">Bu makalede ele alınan ilgili konular hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="ca0ef-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="ca0ef-185">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="ca0ef-185">Async functions</span></span>
* <span data-ttu-id="ca0ef-186">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="ca0ef-186">Multiple instances</span></span>
* <span data-ttu-id="ca0ef-187">Kapama</span><span class="sxs-lookup"><span data-stu-id="ca0ef-187">Graceful shutdown</span></span>
* <span data-ttu-id="ca0ef-188">Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın</span><span class="sxs-lookup"><span data-stu-id="ca0ef-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="ca0ef-189">Kodda Hello SDK bağlantı dizelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="ca0ef-190">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="ca0ef-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="ca0ef-191">Yapılandırma `MaxDequeueCount` zararlı blob işleme.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="ca0ef-192">Tetik el ile bir işlevi</span><span class="sxs-lookup"><span data-stu-id="ca0ef-192">Trigger a function manually</span></span>
* <span data-ttu-id="ca0ef-193">Günlüklerini yazma</span><span class="sxs-lookup"><span data-stu-id="ca0ef-193">Write logs</span></span>

## <span data-ttu-id="ca0ef-194"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca0ef-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="ca0ef-195">Bu kılavuz, nasıl Azure çalışmak için genel senaryolar toohandle BLOB gösteren kod örnekleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="ca0ef-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="ca0ef-196">Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="ca0ef-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

