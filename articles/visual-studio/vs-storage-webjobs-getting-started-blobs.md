---
title: "aaaGet, bağlı hizmetler (Web işi projeleri) blob depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak Azure depolama tooan bağlandıktan sonra bir Web işi projesinin Blob storage kullanarak tooget nasıl başlatılacağını Hizmetleri bağlı."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="4be69-103">Azure Blob ile çalışmaya başlama depolama ve Visual Studio bağlı Hizmetleri (Web işi projeler)</span><span class="sxs-lookup"><span data-stu-id="4be69-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="4be69-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4be69-104">Overview</span></span>
<span data-ttu-id="4be69-105">Bu makalede, C# sağlanmaktadır kod örnekleri gösteren nasıl tootrigger bir Azure blob oluşturulduğunda veya bir işlem.</span><span class="sxs-lookup"><span data-stu-id="4be69-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="4be69-106">Merhaba kod örnekleri kullanır hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) sürüm 1.x.</span><span class="sxs-lookup"><span data-stu-id="4be69-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="4be69-107">Merhaba Visual Studio kullanarak bir depolama hesabı tooa Web işi projesinin eklediğinizde **bağlı Hizmetleri Ekle** iletişim kutusunda, hello uygun Azure depolama NuGet paketi yüklenir, hello uygun .NET başvuruları eklenen toohello Proje ve hello depolama hesabı için bağlantı dizelerini hello App.config dosyasında güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4be69-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="4be69-108">Nasıl tootrigger blob oluşturulduğunda veya bir işlevi</span><span class="sxs-lookup"><span data-stu-id="4be69-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="4be69-109">Bu bölümde gösterilmiştir nasıl toouse hello **BlobTrigger** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="4be69-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="4be69-110">**Not:** WebJobs SDK taramaları günlük dosyaları toowatch yeni veya değiştirilmiş BLOB'lar için hello.</span><span class="sxs-lookup"><span data-stu-id="4be69-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="4be69-111">Bu işlem, doğası gereği yavaş; Merhaba blob oluşturulduktan sonra bir işlev birkaç dakika kadar veya daha uzun tetiklenen değil.</span><span class="sxs-lookup"><span data-stu-id="4be69-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="4be69-112">Uygulamanızı tooprocess BLOB'ları hemen gerekirse, hello yöntemi toocreate bir kuyruk iletisi hello blob oluşturun ve hello kullandığınızda önerilir [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) özniteliği hello yerine **BlobTrigger** hello blob işler hello işlevi özniteliği.</span><span class="sxs-lookup"><span data-stu-id="4be69-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="4be69-113">Blob adı uzantısı için tek bir yer tutucu</span><span class="sxs-lookup"><span data-stu-id="4be69-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="4be69-114">Merhaba aşağıdaki kod örneği görüntülenen metin BLOB'ları hello kopyalar *giriş* kapsayıcı toohello *çıkış* kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="4be69-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="4be69-115">Merhaba öznitelik oluşturucunun hello kapsayıcı adı ve hello blob adı için bir yer tutucu belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="4be69-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="4be69-116">Bu örnekte, bir blob adlandırırsanız *Blob1.txt* hello oluşturulur *giriş* kapsayıcısının hello işlev oluşturur adlı bir blob *Blob1.txt* hello içinde *çıkış*  kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4be69-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="4be69-117">Aşağıdaki kod örneği hello gösterildiği gibi hello blob adı tutucuyla adı düzeni belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4be69-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="4be69-118">Bu kodu "özgün-" ile başlayan adlara sahip yalnızca BLOB'ları kopyalar.</span><span class="sxs-lookup"><span data-stu-id="4be69-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="4be69-119">Örneğin, *özgün Blob1.txt* hello içinde *giriş* kapsayıcı çok kopyalanan*kopya Blob1.txt* hello içinde *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4be69-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="4be69-120">Süslü ayraçlar hello sahip blob adları için toospecify adı deseni gerekiyorsa hello süslü ayraçlar çift.</span><span class="sxs-lookup"><span data-stu-id="4be69-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="4be69-121">Merhaba toofind blobları isterseniz, örneğin, *görüntüleri* böyle adlara sahip kapsayıcı:</span><span class="sxs-lookup"><span data-stu-id="4be69-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="4be69-122">Bu, düzeni için kullanın:</span><span class="sxs-lookup"><span data-stu-id="4be69-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="4be69-123">Merhaba örnekte hello *adı* yer tutucu değerini olacaktır *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="4be69-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="4be69-124">Ayrı bir blob adı ve uzantısı yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="4be69-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="4be69-125">hello görünür BLOB'ları kopyalar hello aşağıdaki kod örnek değişikliklerini dosya uzantısı hello *giriş* kapsayıcı toohello *çıkış* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4be69-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="4be69-126">Merhaba kodunu günlüğe yazar hello hello uzantısı *giriş* blob ve hello hello uzantısı ayarlar *çıkış* çok blob*.txt*.</span><span class="sxs-lookup"><span data-stu-id="4be69-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="4be69-127">Tooblobs bağlayabilirsiniz türleri</span><span class="sxs-lookup"><span data-stu-id="4be69-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="4be69-128">Merhaba kullanabilirsiniz **BlobTrigger** şu türlerini hello özniteliği:</span><span class="sxs-lookup"><span data-stu-id="4be69-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="4be69-129">**dize**</span><span class="sxs-lookup"><span data-stu-id="4be69-129">**string**</span></span>
* <span data-ttu-id="4be69-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="4be69-130">**TextReader**</span></span>
* <span data-ttu-id="4be69-131">**Akış**</span><span class="sxs-lookup"><span data-stu-id="4be69-131">**Stream**</span></span>
* <span data-ttu-id="4be69-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="4be69-132">**ICloudBlob**</span></span>
* <span data-ttu-id="4be69-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="4be69-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="4be69-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="4be69-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="4be69-135">Tarafından seri diğer türleri [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="4be69-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="4be69-136">Hello Azure depolama hesabı ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir **CloudStorageAccount** parametre toohello yöntemi imzası.</span><span class="sxs-lookup"><span data-stu-id="4be69-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="4be69-137">Bağlama toostring tarafından metin blob içeriği alma</span><span class="sxs-lookup"><span data-stu-id="4be69-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="4be69-138">Metin BLOB'ları beklenir, **BlobTrigger** uygulanan tooa olabilir **dize** parametresi.</span><span class="sxs-lookup"><span data-stu-id="4be69-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="4be69-139">Merhaba aşağıdaki kod örneği bağlar metin blob tooa **dize** adlı parametre **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="4be69-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="4be69-140">Merhaba işlevi hello blob toohello WebJobs SDK Pano Bu parametre toowrite hello içeriğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="4be69-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="4be69-141">Blob içeriğinin ICloudBlobStreamBinder kullanarak serileştirilen alma</span><span class="sxs-lookup"><span data-stu-id="4be69-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="4be69-142">Merhaba aşağıdaki kod örneği kullanan uygulayan bir sınıf **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind blob toohello özniteliği **WebImage** türü.</span><span class="sxs-lookup"><span data-stu-id="4be69-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="4be69-143">Merhaba **WebImage** kod bağlama sağlanır bir **WebImageBinder** öğesinden türetilen sınıf **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="4be69-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="4be69-144">Nasıl toohandle poison BLOB</span><span class="sxs-lookup"><span data-stu-id="4be69-144">How toohandle poison blobs</span></span>
<span data-ttu-id="4be69-145">Zaman bir **BlobTrigger** işlevi başarısız oldu, hello SDK çağırır onu yeniden durumda hello hatası tarafından geçici bir hata neden oldu.</span><span class="sxs-lookup"><span data-stu-id="4be69-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="4be69-146">Merhaba blob hello içeriğe göre Hello hatasına neden oldu tooprocess hello blob çalışır her zaman hello işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4be69-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="4be69-147">Varsayılan olarak, hello SDK too5 kez bir işlev için belirli bir blob çağırır.</span><span class="sxs-lookup"><span data-stu-id="4be69-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="4be69-148">Merhaba beşinci deneme başarısız olursa, hello SDK adlı bir ileti tooa sırası ekler *webjobs blobtrigger poison*.</span><span class="sxs-lookup"><span data-stu-id="4be69-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="4be69-149">Merhaba en fazla yeniden deneme sayısı yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4be69-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="4be69-150">aynı hello [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ayarı zararlı blob işleme ve zararlı sıraya ileti işleme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4be69-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="4be69-151">Merhaba kuyruk iletisi zararlı BLOB'lar için aşağıdaki özelliklere hello içeren bir JSON nesnesi şudur:</span><span class="sxs-lookup"><span data-stu-id="4be69-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="4be69-152">FunctionId (Merhaba biçiminde *{Web işi adı}*. İşlevler. *{İşlev adı}*, örneğin: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="4be69-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="4be69-153">BlobType ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4be69-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4be69-154">Kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="4be69-154">ContainerName</span></span>
* <span data-ttu-id="4be69-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="4be69-155">BlobName</span></span>
* <span data-ttu-id="4be69-156">ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4be69-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="4be69-157">Merhaba aşağıdaki örnek, hello kod **CopyBlob** işlev her çağrıldığında, toofail neden olan kod bulunur.</span><span class="sxs-lookup"><span data-stu-id="4be69-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="4be69-158">Sonra Hello SDK çağrıları, hello en fazla yeniden deneme sayısı için hello zararlı blob sırada bir ileti oluşturulur ve bu ileti hello tarafından işlenir **LogPoisonBlob** işlevi.</span><span class="sxs-lookup"><span data-stu-id="4be69-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="4be69-159">Merhaba SDK hello JSON ileti otomatik olarak seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="4be69-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="4be69-160">Merhaba işte **PoisonBlobMessage** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4be69-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="4be69-161">BLOB yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="4be69-161">Blob polling algorithm</span></span>
<span data-ttu-id="4be69-162">Merhaba WebJobs SDK tarafından belirtilen tüm kapsayıcıları tarar **BlobTrigger** uygulama başlangıcında öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="4be69-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="4be69-163">Yeni BLOB'lar bulunan önce biraz olabilir şekilde büyük depolama hesabı bu tarama biraz zaman alabilir ve **BlobTrigger** işlevleri çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="4be69-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="4be69-164">toodetect yeni veya değiştirilmiş BLOB'lar uygulama başlatma sonra SDK düzenli aralıklarla hello blob depolama alanından okur hello günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4be69-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="4be69-165">Merhaba blob günlükleri arabelleğe alınmış ve yalnızca fiziksel olarak her 10 dakikada yazılan veya bu nedenle, bu nedenle önemli gecikme olabileceğini blob oluşturulmuş veya hello karşılık gelen önce güncelleştirilmiş sonra **BlobTrigger** işlevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="4be69-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="4be69-166">Hello kullanarak oluşturduğunuz BLOB'ları için bir özel durum var. **Blob** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="4be69-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="4be69-167">Merhaba WebJobs SDK yeni blob oluşturduğunda, hello yeni blob hemen geçtikten tooany eşleşen **BlobTrigger** işlevleri.</span><span class="sxs-lookup"><span data-stu-id="4be69-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="4be69-168">Blob girişleri ve çıkışları zinciri varsa, bu nedenle hello SDK bunları verimli bir şekilde işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="4be69-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="4be69-169">Ancak, düşük gecikme süresi, blob işleme işlevleri için oluşturulmuş veya başka yollarla güncelleştirilmiş BLOB'ları çalıştıran istiyorsanız, kullanmanızı öneririz **QueueTrigger** yerine **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="4be69-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="4be69-170">BLOB giriş</span><span class="sxs-lookup"><span data-stu-id="4be69-170">Blob receipts</span></span>
<span data-ttu-id="4be69-171">Merhaba WebJobs SDK emin olur hiçbir **BlobTrigger** işlevi birden çok kez Merhaba aynı yeni adlı veya blob güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="4be69-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="4be69-172">Bunu tutarak yapar *blob giriş* verilen blob sürümü işlediğinde sipariş toodetermine içinde.</span><span class="sxs-lookup"><span data-stu-id="4be69-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="4be69-173">BLOB giriş adlı bir kapsayıcıda depolanır *azure Web işleri konakları* hello AzureWebJobsStorage bağlantı dizesi tarafından belirtilen hello Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="4be69-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="4be69-174">Bir blob giriş bilgisinden hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4be69-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="4be69-175">Merhaba hello blobu çağrıldı işlevi ("*{Web işi adı}*. İşlevler. *{İşlev adı}*", örneğin:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="4be69-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="4be69-176">Merhaba kapsayıcı adı</span><span class="sxs-lookup"><span data-stu-id="4be69-176">hello container name</span></span>
* <span data-ttu-id="4be69-177">Merhaba blob türü ("BlockBlob" veya "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4be69-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4be69-178">Merhaba blob adı</span><span class="sxs-lookup"><span data-stu-id="4be69-178">hello blob name</span></span>
* <span data-ttu-id="4be69-179">Merhaba ETag (örneğin bir blob sürüm tanıtıcısını: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4be69-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="4be69-180">Tooforce bir blob yeniden işleme istiyorsanız, o blob için hello blob giriş hello el ile silebilirsiniz *azure Web işleri konakları* kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4be69-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="4be69-181">Merhaba sıraları makalesiyle kapsanan ilgili konular</span><span class="sxs-lookup"><span data-stu-id="4be69-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="4be69-182">Nasıl toohandle blob işleme bir kuyruk iletisi tarafından veya WebJobs SDK senaryoları tetiklenen değil hakkında bilgi için işleme, belirli tooblob bakın [nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="4be69-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="4be69-183">Bu makalede ele alınan ilgili konular hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="4be69-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="4be69-184">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="4be69-184">Async functions</span></span>
* <span data-ttu-id="4be69-185">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="4be69-185">Multiple instances</span></span>
* <span data-ttu-id="4be69-186">Kapama</span><span class="sxs-lookup"><span data-stu-id="4be69-186">Graceful shutdown</span></span>
* <span data-ttu-id="4be69-187">Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın</span><span class="sxs-lookup"><span data-stu-id="4be69-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="4be69-188">Kodda Hello SDK bağlantı dizelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4be69-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="4be69-189">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="4be69-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="4be69-190">Yapılandırma **MaxDequeueCount** zararlı blob işleme.</span><span class="sxs-lookup"><span data-stu-id="4be69-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="4be69-191">Tetik el ile bir işlevi</span><span class="sxs-lookup"><span data-stu-id="4be69-191">Trigger a function manually</span></span>
* <span data-ttu-id="4be69-192">Günlüklerini yazma</span><span class="sxs-lookup"><span data-stu-id="4be69-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="4be69-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4be69-193">Next steps</span></span>
<span data-ttu-id="4be69-194">Bu makalede, nasıl Azure çalışmak için genel senaryolar toohandle BLOB gösteren kod örnekleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="4be69-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="4be69-195">Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="4be69-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

