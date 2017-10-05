---
title: "WebJobs SDK ile Azure Blob Storage kullanımı"
description: "WebJobs SDK ile Azure blob depolama kullanmayı öğrenin. Yeni bir blob bir kapsayıcıda görüntülendiğinde bir işlem tetikleyebilir ve 'zararlı BLOB' tanıtıcı."
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
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="32d18-104">WebJobs SDK ile Azure Blob Storage kullanımı</span><span class="sxs-lookup"><span data-stu-id="32d18-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="32d18-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="32d18-105">Overview</span></span>
<span data-ttu-id="32d18-106">Bu kılavuz, Azure blob oluşturulduğunda veya bir işlem tetiklemek nasıl gösteren C# kod örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="32d18-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="32d18-107">Kod örnekleri kullan [WebJobs SDK](websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="32d18-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="32d18-108">BLOB'ları oluşturmak nasıl gösteren kod örnekleri için bkz: [WebJobs SDK ile Azure kuyruk depolama kullanma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="32d18-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="32d18-109">Bildiğiniz Kılavuzu varsayar [bağlantıyla Visual Studio'da bir Web işi projesi oluşturma, depolama hesabınıza o noktadan dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya [birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="32d18-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="32d18-110"><a id="trigger"></a>Bir blob oluşturulduğunda veya bir işlev tetikleme</span><span class="sxs-lookup"><span data-stu-id="32d18-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="32d18-111">Bu bölümde nasıl kullanılacağını gösterir `BlobTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="32d18-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="32d18-112">Web işleri SDK'si için yeni veya değiştirilmiş BLOB'lar izlemek için günlük dosyalarını tarar.</span><span class="sxs-lookup"><span data-stu-id="32d18-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="32d18-113">Bu işlem, gerçek zamanlı değildir; blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil.</span><span class="sxs-lookup"><span data-stu-id="32d18-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="32d18-114">Ayrıca, [depolama günlüklerine "en iyi çaba" üzerinde oluşturulan](https://msdn.microsoft.com/library/azure/hh343262.aspx) temel; tüm olayları Yakalanacak garantisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="32d18-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="32d18-115">Bazı koşullarda günlükleri eksik.</span><span class="sxs-lookup"><span data-stu-id="32d18-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="32d18-116">Blob Tetikleyicileri hızı ve güvenilirliği sınırlamaları, uygulamanız için kabul edilebilir değilse, blob oluşturma ve kullanma, bir kuyruk iletisi oluşturmak için önerilen yöntem olduğu [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) yerineözniteliği`BlobTrigger` blob işler işlevi özniteliği.</span><span class="sxs-lookup"><span data-stu-id="32d18-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="32d18-117">Blob adı uzantısı için tek bir yer tutucu</span><span class="sxs-lookup"><span data-stu-id="32d18-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="32d18-118">Aşağıdaki kod örneği görünen metin BLOB'ları kopyalar *giriş* kapsayıcıya *çıkış* kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="32d18-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="32d18-119">Öznitelik oluşturucunun kapsayıcı adı hem de blob adı için bir yer tutucu belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="32d18-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="32d18-120">Bu örnekte, bir blob adlandırırsanız *Blob1.txt* oluşturulur *giriş* kapsayıcı, işlev oluşturur adlı bir blob *Blob1.txt* içinde *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="32d18-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="32d18-121">Aşağıdaki kod örneğinde gösterildiği gibi blob adı yer tutucu ile adı deseni belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="32d18-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="32d18-122">Bu kodu "özgün-" ile başlayan adlara sahip yalnızca BLOB'ları kopyalar.</span><span class="sxs-lookup"><span data-stu-id="32d18-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="32d18-123">Örneğin, *özgün Blob1.txt* içinde *giriş* kapsayıcı kopyalanır *kopya Blob1.txt* içinde *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="32d18-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="32d18-124">Süslü ayraçlar sahip blob adları için bir ad deseni belirtmeniz gerekiyorsa, süslü ayraçlar çift.</span><span class="sxs-lookup"><span data-stu-id="32d18-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="32d18-125">Örneğin, BLOB'ları bulmak istiyorsanız *görüntüleri* böyle adlara sahip kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="32d18-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="32d18-126">Bu, düzeni için kullanın:</span><span class="sxs-lookup"><span data-stu-id="32d18-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="32d18-127">Örnekte, *adı* yer tutucu değerini olacaktır *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="32d18-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="32d18-128">Ayrı bir blob adı ve uzantısı yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="32d18-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="32d18-129">Görünen BLOB'ları kopyalar olarak aşağıdaki kod örneği dosya uzantısını değiştiren *giriş* kapsayıcıya *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="32d18-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="32d18-130">Kod uzantısını günlüklerini *giriş* blob ve genişletilmesi ayarlar *çıkış* için blob *.txt*.</span><span class="sxs-lookup"><span data-stu-id="32d18-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <span data-ttu-id="32d18-131"><a id="types"></a>BLOB'larını bağlayabilirsiniz türleri</span><span class="sxs-lookup"><span data-stu-id="32d18-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="32d18-132">Kullanabileceğiniz `BlobTrigger` özniteliği aşağıdaki türler:</span><span class="sxs-lookup"><span data-stu-id="32d18-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

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
* <span data-ttu-id="32d18-133">Tarafından seri diğer türleri [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="32d18-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="32d18-134">Azure depolama hesabı ile doğrudan çalışmak isterseniz, ayrıca ekleyebileceğiniz bir `CloudStorageAccount` yöntem imzası parametresi.</span><span class="sxs-lookup"><span data-stu-id="32d18-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="32d18-135">Örnekler için bkz: [blob Github.com'u azure webjobs sdk havuzda bağlama kodda](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="32d18-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="32d18-136"><a id="string"></a>Dize bağlayarak metin blob içeriği alma</span><span class="sxs-lookup"><span data-stu-id="32d18-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="32d18-137">Metin BLOB'ları beklenir, `BlobTrigger` uygulanabilir bir `string` parametresi.</span><span class="sxs-lookup"><span data-stu-id="32d18-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="32d18-138">Aşağıdaki kod örneği için metin blob bağlar bir `string` adlı parametre `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="32d18-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="32d18-139">İşlevi için Web işleri SDK'si Pano blob içeriğini yazmak için bu parametresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="32d18-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="32d18-140"><a id="icbsb"></a>Blob içeriğinin ICloudBlobStreamBinder kullanarak serileştirilen alma</span><span class="sxs-lookup"><span data-stu-id="32d18-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="32d18-141">Aşağıdaki kod örneği uygulayan bir sınıf kullanır `ICloudBlobStreamBinder` etkinleştirmek için `BlobTrigger` bir blobu bağlamak için öznitelik `WebImage` türü.</span><span class="sxs-lookup"><span data-stu-id="32d18-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="32d18-142">`WebImage` Kod bağlama sağlanır bir `WebImageBinder` öğesinden türetilen sınıf `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="32d18-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="32d18-143">Blob yolu için tetikleyici blob alma</span><span class="sxs-lookup"><span data-stu-id="32d18-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="32d18-144">İşlevi tetikleyen blob blob adını ve kapsayıcı adını almak için içeren bir `blobTrigger` işlev imzası parametresinde dize.</span><span class="sxs-lookup"><span data-stu-id="32d18-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="32d18-145"><a id="poison"></a>Zararlı BLOB'ları nasıl ele alınacağını</span><span class="sxs-lookup"><span data-stu-id="32d18-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="32d18-146">Zaman bir `BlobTrigger` işlevi başarısız oldu, SDK çağırır onu yeniden durumunda hata geçici bir hata neden oldu.</span><span class="sxs-lookup"><span data-stu-id="32d18-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="32d18-147">Blob içerik tarafından hatasına neden oldu blob işlemeye çalıştığında her zaman işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="32d18-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="32d18-148">Varsayılan olarak, SDK'sı bir işlev en fazla 5 kez için belirli bir blob çağırır.</span><span class="sxs-lookup"><span data-stu-id="32d18-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="32d18-149">Beşinci başarısız çalışırsanız, SDK bir ileti adlandırılan bir kuyruğun ekler. *webjobs blobtrigger poison*.</span><span class="sxs-lookup"><span data-stu-id="32d18-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="32d18-150">En fazla yeniden deneme sayısı yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="32d18-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="32d18-151">Aynı [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ayarı zararlı blob işleme ve zararlı sıraya ileti işleme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="32d18-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="32d18-152">Kuyruk iletisini zararlı BLOB'lar için aşağıdaki özellikleri içeren bir JSON nesnesidir:</span><span class="sxs-lookup"><span data-stu-id="32d18-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="32d18-153">FunctionId (biçimde *{Web işi adı}*. İşlevler. *{İşlev adı}*, örneğin: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="32d18-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="32d18-154">BlobType ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="32d18-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="32d18-155">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="32d18-155">ContainerName</span></span>
* <span data-ttu-id="32d18-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="32d18-156">BlobName</span></span>
* <span data-ttu-id="32d18-157">ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="32d18-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="32d18-158">Aşağıdaki kod örneğinde, `CopyBlob` işlev her çağrıldığında başarısız olmasına neden kodu bulunur.</span><span class="sxs-lookup"><span data-stu-id="32d18-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="32d18-159">Sonra en fazla yeniden deneme sayısı için çağırır SDK, zararlı blob sıraya bir ileti oluşturulur ve bu iletiyi tarafından işlenen `LogPoisonBlob` işlevi.</span><span class="sxs-lookup"><span data-stu-id="32d18-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="32d18-160">SDK JSON ileti otomatik olarak seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="32d18-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="32d18-161">Burada `PoisonBlobMessage` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="32d18-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="32d18-162"><a id="polling"></a>BLOB yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="32d18-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="32d18-163">WebJobs SDK tarafından belirtilen tüm kapsayıcıları tarar `BlobTrigger` uygulama başlangıcında öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="32d18-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="32d18-164">Yeni BLOB'lar bulunan önce biraz olabilir şekilde büyük depolama hesabı bu tarama biraz zaman alabilir ve `BlobTrigger` işlevleri çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="32d18-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="32d18-165">SDK'sı, uygulama başladıktan sonra yeni veya değiştirilmiş BLOB'lar algılamak için blob depolama günlüklerinden düzenli aralıklarla okur.</span><span class="sxs-lookup"><span data-stu-id="32d18-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="32d18-166">Blob günlükleri arabelleğe alınmış ve yalnızca fiziksel olarak her 10 dakikada yazılan veya bu nedenle, bu nedenle önemli gecikme olabileceğini blob oluşturulmuş veya karşılık gelen önce güncelleştirilmiş sonra `BlobTrigger` işlevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="32d18-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="32d18-167">Kullanarak oluşturduğunuz BLOB'ları için bir özel durum var. `Blob` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="32d18-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="32d18-168">WebJobs SDK yeni blob oluşturduğunda, bunu yeni blob hemen eşleşen tüm geçirir `BlobTrigger` işlevleri.</span><span class="sxs-lookup"><span data-stu-id="32d18-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="32d18-169">Blob girişleri ve çıkışları zinciri varsa, bu nedenle SDK bunları verimli bir şekilde işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="32d18-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="32d18-170">Ancak, düşük gecikme süresi, blob işleme işlevleri için oluşturulmuş veya başka yollarla güncelleştirilmiş BLOB'ları çalıştıran istiyorsanız, kullanmanızı öneririz `QueueTrigger` yerine `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="32d18-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="32d18-171"><a id="receipts"></a>BLOB giriş</span><span class="sxs-lookup"><span data-stu-id="32d18-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="32d18-172">WebJobs SDK emin yapıyorsa hiçbir `BlobTrigger` işlevi için aynı yeni veya güncelleştirilmiş blob birden çok kez çağrıldığından.</span><span class="sxs-lookup"><span data-stu-id="32d18-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="32d18-173">Bunu tutarak yapar *blob giriş* verilen blob sürümü işlenen belirlemek için.</span><span class="sxs-lookup"><span data-stu-id="32d18-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="32d18-174">BLOB giriş adlı bir kapsayıcıda depolanır *azure Web işleri konakları* AzureWebJobsStorage bağlantı dizesi tarafından belirtilen Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="32d18-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="32d18-175">Bir blob giriş aşağıdaki bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="32d18-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="32d18-176">İçin blob çağrıldı işlevi ("*{Web işi adı}*. İşlevler. *{İşlev adı}*", örneğin:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="32d18-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="32d18-177">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="32d18-177">The container name</span></span>
* <span data-ttu-id="32d18-178">Blob türü ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="32d18-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="32d18-179">Blob adı</span><span class="sxs-lookup"><span data-stu-id="32d18-179">The blob name</span></span>
* <span data-ttu-id="32d18-180">ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="32d18-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="32d18-181">Bir blob yeniden işlemeyerek zorlamak istiyorsanız, o blobundan blob giriş el ile silebilirsiniz *azure Web işleri konakları* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="32d18-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="32d18-182"><a id="queues"></a>Kuyruklar makalesiyle kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="32d18-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="32d18-183">İşleme, senaryoları blob özgü olmayan Web işleri SDK'si veya nasıl bir kuyruk iletisi tarafından tetiklenen blob işleme yönetileceği hakkında bilgi için bkz [WebJobs SDK ile Azure kuyruk depolama kullanma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="32d18-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="32d18-184">Bu makalede ele alınan ilgili konular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="32d18-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="32d18-185">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="32d18-185">Async functions</span></span>
* <span data-ttu-id="32d18-186">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="32d18-186">Multiple instances</span></span>
* <span data-ttu-id="32d18-187">Kapama</span><span class="sxs-lookup"><span data-stu-id="32d18-187">Graceful shutdown</span></span>
* <span data-ttu-id="32d18-188">Web işleri SDK'si öznitelikleri bir işlev gövdesine kullanın</span><span class="sxs-lookup"><span data-stu-id="32d18-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="32d18-189">Kod içinde SDK bağlantı dizelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="32d18-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="32d18-190">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="32d18-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="32d18-191">Yapılandırma `MaxDequeueCount` zararlı blob işleme.</span><span class="sxs-lookup"><span data-stu-id="32d18-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="32d18-192">Tetik el ile bir işlevi</span><span class="sxs-lookup"><span data-stu-id="32d18-192">Trigger a function manually</span></span>
* <span data-ttu-id="32d18-193">Günlüklerini yazma</span><span class="sxs-lookup"><span data-stu-id="32d18-193">Write logs</span></span>

## <span data-ttu-id="32d18-194"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32d18-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="32d18-195">Bu kılavuz, Azure BLOB'ları ile çalışmak için genel senaryolar nasıl ele alınacağını gösteren kod örnekleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="32d18-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="32d18-196">Azure Web işleri ve WebJobs SDK nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="32d18-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

