---
title: aaaHow toouse hello WebJobs SDK ile Azure kuyruk depolama
description: "Nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile bilgi edinin. Oluşturma ve kuyrukları silin; Ekle, Gözat, Al ve iletileri kuyruğa ve daha fazlasını silin."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="138a0-104">Nasıl toouse Azure kuyruk depolama hello WebJobs SDK ile</span><span class="sxs-lookup"><span data-stu-id="138a0-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="138a0-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="138a0-105">Overview</span></span>
<span data-ttu-id="138a0-106">Bu kılavuz, nasıl toouse hello Azure WebJobs SDK sürüm gösteren C# kod örnekleri sağlar 1.x hello Azure kuyruk depolama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="138a0-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="138a0-107">Merhaba Kılavuzu varsayar bildiğiniz [nasıl toocreate bağlantısı ile Visual Studio'da bir Web işi projesi bu noktası tooyour depolama hesabı dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya çok[birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="138a0-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="138a0-108">Merhaba kod parçacıkları çoğunu İşlevler, yalnızca Göster hello oluşturan kodunu hello değil `JobHost` nesne bu örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="138a0-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="138a0-109">Aşağıdaki konularda hello Hello kılavuz içerir:</span><span class="sxs-lookup"><span data-stu-id="138a0-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="138a0-110">Nasıl tootrigger bir kuyruk iletisi alındığında işlevi</span><span class="sxs-lookup"><span data-stu-id="138a0-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="138a0-111">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-111">String queue messages</span></span>
  * <span data-ttu-id="138a0-112">POCO iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-112">POCO queue messages</span></span>
  * <span data-ttu-id="138a0-113">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="138a0-113">Async functions</span></span>
  * <span data-ttu-id="138a0-114">Türleri hello QueueTrigger özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="138a0-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="138a0-115">Yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="138a0-115">Polling algorithm</span></span>
  * <span data-ttu-id="138a0-116">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="138a0-116">Multiple instances</span></span>
  * <span data-ttu-id="138a0-117">Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="138a0-117">Parallel execution</span></span>
  * <span data-ttu-id="138a0-118">Sıra veya sıra ileti meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="138a0-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="138a0-119">Kapama</span><span class="sxs-lookup"><span data-stu-id="138a0-119">Graceful shutdown</span></span>
* [<span data-ttu-id="138a0-120">Toocreate bir kuyruk iletisi nasıl bir kuyruk iletisi işlenirken</span><span class="sxs-lookup"><span data-stu-id="138a0-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="138a0-121">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-121">String queue messages</span></span>
  * <span data-ttu-id="138a0-122">POCO iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-122">POCO queue messages</span></span>
  * <span data-ttu-id="138a0-123">Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="138a0-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="138a0-124">Türleri hello sıra özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="138a0-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="138a0-125">Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın</span><span class="sxs-lookup"><span data-stu-id="138a0-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="138a0-126">Tooread ve yazma BLOB nasıl bir kuyruk iletisi işlenirken</span><span class="sxs-lookup"><span data-stu-id="138a0-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="138a0-127">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-127">String queue messages</span></span>
  * <span data-ttu-id="138a0-128">POCO iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-128">POCO queue messages</span></span>
  * <span data-ttu-id="138a0-129">Türleri hello Blob özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="138a0-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="138a0-130">Nasıl toohandle zehirli ileti</span><span class="sxs-lookup"><span data-stu-id="138a0-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="138a0-131">Otomatik zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="138a0-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="138a0-132">El ile zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="138a0-132">Manual poison message handling</span></span>
* [<span data-ttu-id="138a0-133">Nasıl tooset yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="138a0-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="138a0-134">Kod içinde SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="138a0-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="138a0-135">QueueTrigger ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="138a0-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="138a0-136">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="138a0-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="138a0-137">Nasıl tootrigger bir işlev el ile</span><span class="sxs-lookup"><span data-stu-id="138a0-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="138a0-138">Toowrite nasıl kaydeder</span><span class="sxs-lookup"><span data-stu-id="138a0-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="138a0-139">Nasıl toohandle hataları ve zaman aşımları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="138a0-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="138a0-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="138a0-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="138a0-141"><a id="trigger"></a>Nasıl tootrigger bir kuyruk iletisi alındığında işlevi</span><span class="sxs-lookup"><span data-stu-id="138a0-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="138a0-142">toowrite Web işleri SDK'si hello işlevi çağıran bir kuyruk iletisi alındığında, hello kullan `QueueTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="138a0-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="138a0-143">Hello özniteliği Oluşturucusu hello sıra toopoll hello adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="138a0-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="138a0-144">Ayrıca [hello sıra adı dinamik olarak ayarlamak](#config).</span><span class="sxs-lookup"><span data-stu-id="138a0-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="138a0-145">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-145">String queue messages</span></span>
<span data-ttu-id="138a0-146">Bir dize ileti hello sıra aşağıdaki örneğine hello, bu nedenle içeren `QueueTrigger` adlı uygulanan tooa dize parametresi `logMessage` hello kuyruk iletisi Merhaba içeriğine içerir.</span><span class="sxs-lookup"><span data-stu-id="138a0-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="138a0-147">Merhaba işlevi [bir günlük iletisi toohello Pano Yazar](#logs).</span><span class="sxs-lookup"><span data-stu-id="138a0-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="138a0-148">Yanında `string`, hello parametresi bir bayt dizisi olabilir bir `CloudQueueMessage` nesne ya da tanımladığınız bir POCO.</span><span class="sxs-lookup"><span data-stu-id="138a0-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="138a0-149">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="138a0-150">Aşağıdaki örneğine hello, JSON hello kuyruk iletisi içeren bir `BlobInformation` içeren nesne bir `BlobName` özelliği.</span><span class="sxs-lookup"><span data-stu-id="138a0-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="138a0-151">Merhaba SDK otomatik olarak hello nesne seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="138a0-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="138a0-152">Merhaba SDK kullanan hello [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize ve iletileri seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="138a0-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="138a0-153">Merhaba WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bu hello hello örnek toocreate bir POCO kuyruk iletisi aşağıdaki gibi kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="138a0-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="138a0-154">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="138a0-154">Async functions</span></span>
<span data-ttu-id="138a0-155">Async işlevi aşağıdaki hello [günlük toohello Pano Yazar](#logs).</span><span class="sxs-lookup"><span data-stu-id="138a0-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="138a0-156">Zaman uyumsuz işlevleri sürebilir bir [iptal belirteci](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)hello blob kopyaladığı örnek aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="138a0-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="138a0-157">(Merhaba açıklaması için `queueTrigger` yer tutucu hello bkz [BLOB'lar](#blobs) bölüm.)</span><span class="sxs-lookup"><span data-stu-id="138a0-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="138a0-158"><a id="qtattributetypes"></a>Türleri hello QueueTrigger özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="138a0-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="138a0-159">Kullanabileceğiniz `QueueTrigger` şu türlerini hello ile:</span><span class="sxs-lookup"><span data-stu-id="138a0-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="138a0-160">JSON olarak serileştirilen bir POCO türü</span><span class="sxs-lookup"><span data-stu-id="138a0-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="138a0-161"><a id="polling"></a>Yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="138a0-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="138a0-162">Merhaba SDK boşta kuyruk depolama işlem maliyetleri yoklama rasgele üstel geri alma algoritması tooreduce hello etkisini uygular.</span><span class="sxs-lookup"><span data-stu-id="138a0-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="138a0-163">Bir ileti bulunduğunda, hello SDK iki saniye bekler ve ardından başka bir ileti için denetler; bir ileti bulunduğunda yeniden denemeden önce yaklaşık dört saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="138a0-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="138a0-164">Merhaba maksimum bekleme süresi, ulaşana kadar sonraki başarısız denemeler tooget bir kuyruk iletisi sonra hello bekleme süresi tooincrease devam eder. hangi Varsayılanları tooone minute.</span><span class="sxs-lookup"><span data-stu-id="138a0-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="138a0-165">[Merhaba maksimum bekleme süresi yapılandırılabilir](#config).</span><span class="sxs-lookup"><span data-stu-id="138a0-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="138a0-166"><a id="instances"></a>Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="138a0-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="138a0-167">Web uygulamanız birden çok örneği üzerinde çalışıyorsa, bir sürekli Webjob'un her makinede çalışır ve her makine için Tetikleyicileri bekleyin ve toorun işlevlerini deneyin.</span><span class="sxs-lookup"><span data-stu-id="138a0-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="138a0-168">Merhaba WebJobs SDK sıra tetikleyici otomatik olarak bir işlev bir kuyruk iletisi birden çok kez önlediği; İşlevler toobe ıdempotent yazılmış toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="138a0-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="138a0-169">Ancak, tooensure istiyorsanız bile hello ana web uygulamanızın birden fazla örneği bulunduğunda bir işlevi yalnızca bir örneğini çalıştıran, hello kullanabilirsiniz `Singleton` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="138a0-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="138a0-170"><a id="parallel"></a>Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="138a0-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="138a0-171">Birden çok işlevler farklı sıralarda dinleme varsa, iletileri aynı anda alındığında hello SDK bunları paralel olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="138a0-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="138a0-172">tek bir kuyruk için birden fazla ileti alındığında hello aynı durum geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="138a0-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="138a0-173">Varsayılan olarak, hello SDK 16 iletileri kuyruğa toplu bir zaman alır ve paralel olarak işler hello işlevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="138a0-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="138a0-174">[Merhaba toplu iş boyutu Dur yapılandırılabilir](#config).</span><span class="sxs-lookup"><span data-stu-id="138a0-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="138a0-175">İşlenmekte olan hello numarası hello toplu iş boyutu toohalf aldığında hello SDK başka bir toplu iş alır ve bu iletileri işleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="138a0-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="138a0-176">Bu nedenle hello en fazla eş zamanlı ileti işlevi işlenen sayısı bir ve yarı kez bir hello toplu iş boyutu dur.</span><span class="sxs-lookup"><span data-stu-id="138a0-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="138a0-177">Bu sınır olan tooeach işlev ayrı ayrı uygular bir `QueueTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="138a0-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="138a0-178">Paralel yürütme üzerinde bir Sıraya alınan iletileri istemiyorsanız hello toplu iş boyutu too1 ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="138a0-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="138a0-179">Ayrıca bkz. **sırası işleme üzerinde daha fazla denetim** içinde [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="138a0-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="138a0-180"><a id="queuemetadata"></a>Sıra veya sıra ileti meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="138a0-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="138a0-181">Aşağıdaki ileti özelliklere parametreleri toohello yöntemi imza ekleyerek hello alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="138a0-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="138a0-182">`DateTimeOffset`expirationTime</span><span class="sxs-lookup"><span data-stu-id="138a0-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="138a0-183">`DateTimeOffset`insertionTime</span><span class="sxs-lookup"><span data-stu-id="138a0-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="138a0-184">`DateTimeOffset`nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="138a0-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="138a0-185">`string`queueTrigger (ileti metni içerir)</span><span class="sxs-lookup"><span data-stu-id="138a0-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="138a0-186">`string`Kimliği</span><span class="sxs-lookup"><span data-stu-id="138a0-186">`string` id</span></span>
* <span data-ttu-id="138a0-187">`string`popReceipt</span><span class="sxs-lookup"><span data-stu-id="138a0-187">`string` popReceipt</span></span>
* <span data-ttu-id="138a0-188">`int`dequeueCount</span><span class="sxs-lookup"><span data-stu-id="138a0-188">`int` dequeueCount</span></span>

<span data-ttu-id="138a0-189">Hello Azure storage API'si ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir `CloudStorageAccount` parametresi.</span><span class="sxs-lookup"><span data-stu-id="138a0-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="138a0-190">Merhaba aşağıdaki örnekte tüm bu meta verileri tooan bilgisi uygulama günlüğüne yazar.</span><span class="sxs-lookup"><span data-stu-id="138a0-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="138a0-191">Merhaba örnekte hello kuyruk iletisi Merhaba içeriğine logMessage ve queueTrigger içerir.</span><span class="sxs-lookup"><span data-stu-id="138a0-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="138a0-192">Merhaba örnek kodu ile yazılmış bir örnek günlük şöyledir:</span><span class="sxs-lookup"><span data-stu-id="138a0-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="138a0-193"><a id="graceful"></a>Kapama</span><span class="sxs-lookup"><span data-stu-id="138a0-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="138a0-194">Sürekli bir WebJob içinde çalışan bir işlevinin kabul edebileceği bir `CancellationToken` hello işletim sistemi toonotify hello işlevi hello zaman sağlayan Web işi parametredir hakkında toobe sonlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="138a0-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="138a0-195">Bu bildirim toomake hello beklenmedik bir şekilde veri tutarsız bir durumda bırakır şekilde sonlandırma işlevi değil emin kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="138a0-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="138a0-196">örnekte gösterildiği nasıl aşağıdaki hello toocheck bir işlevdeki yaklaşan WebJob sonlandırma için.</span><span class="sxs-lookup"><span data-stu-id="138a0-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="138a0-197">**Not:** hello Pano hello durumunu ve çıkışını kapatılmışsa işlevlerin doğru şekilde göstermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="138a0-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="138a0-198">Daha fazla bilgi için bkz: [Web işleri normal şekilde kapatılmasını](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="138a0-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="138a0-199"><a id="createqueue"></a>Toocreate bir kuyruk iletisi nasıl bir kuyruk iletisi işlenirken</span><span class="sxs-lookup"><span data-stu-id="138a0-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="138a0-200">Yeni bir kuyruk iletisi kullanım hello oluşturan bir işlev toowrite `Queue` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="138a0-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="138a0-201">Gibi `QueueTrigger`, hello kuyruk adı bir dize olarak geçirin veya yapabilecekleriniz [hello sıra adı dinamik olarak ayarlamak](#config).</span><span class="sxs-lookup"><span data-stu-id="138a0-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="138a0-202">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-202">String queue messages</span></span>
<span data-ttu-id="138a0-203">zaman uyumsuz olmayan kodu örneği aşağıdaki hello hello kuyruk iletisi olarak içerik aynı "inputqueue" adlı hello sıraya alınan hello hello sırasındaki "outputqueue" adlı yeni bir kuyruk iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="138a0-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="138a0-204">(İşlevler için async kullanma `IAsyncCollector<T>` daha sonra bu bölümde gösterilen.)</span><span class="sxs-lookup"><span data-stu-id="138a0-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="138a0-205">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="138a0-206">toocreate geçişi hello POCO bir dize yerine bir POCO içeren bir kuyruk iletisi türü bir çıkış parametresi toohello `Queue` özniteliği Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="138a0-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="138a0-207">Merhaba SDK hello nesne tooJSON otomatik olarak serileştirir.</span><span class="sxs-lookup"><span data-stu-id="138a0-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="138a0-208">Merhaba nesnesi boş olsa bile bir kuyruk iletisi her zaman oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="138a0-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="138a0-209">Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="138a0-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="138a0-210">toocreate birden fazla ileti olun hello çıkış sırası için hello parametre türü `ICollector<T>` veya `IAsyncCollector<T>`hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="138a0-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="138a0-211">Her kuyruk iletisi hemen hello oluşturulduğunda `Add` yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="138a0-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="138a0-212">Türleri bu hello sıra özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="138a0-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="138a0-213">Merhaba kullanabilirsiniz `Queue` parametre türleri şu hello özniteliği:</span><span class="sxs-lookup"><span data-stu-id="138a0-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="138a0-214">`out string`(Merhaba işlevi sona erdiğinde parametre değeri null olmayan ise kuyruk iletisi oluşturur)</span><span class="sxs-lookup"><span data-stu-id="138a0-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="138a0-215">`out byte[]`(gibi çalışır `string`)</span><span class="sxs-lookup"><span data-stu-id="138a0-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="138a0-216">`out CloudQueueMessage`(gibi çalışır `string`)</span><span class="sxs-lookup"><span data-stu-id="138a0-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="138a0-217">`out POCO`(serializable bir tür oluşturduğu bir ileti null bir nesne ile Merhaba işlevi sona erdiğinde hello parametre null ise)</span><span class="sxs-lookup"><span data-stu-id="138a0-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="138a0-218">`CloudQueue`(el ile hello Azure Storage API'sini kullanarak doğrudan iletileri oluşturmak için)</span><span class="sxs-lookup"><span data-stu-id="138a0-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="138a0-219"><a id="ibinder"></a>Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın</span><span class="sxs-lookup"><span data-stu-id="138a0-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="138a0-220">Toodo ihtiyacınız varsa bazı, işlevinde bir Web işleri SDK'si öznitelik gibi kullanmadan önce iş `Queue`, `Blob`, veya `Table`, hello kullanabilirsiniz `IBinder` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="138a0-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="138a0-221">Aşağıdaki örneğine hello bir giriş sırası iletisi sürer ve aynı bir çıkış sırasının içerik hello ile yeni bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="138a0-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="138a0-222">Merhaba çıkış sırası adı hello işlevi hello gövdesinde kodu tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="138a0-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="138a0-223">Merhaba `IBinder` arabirimi hello ile de kullanılabilir `Table` ve `Blob` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="138a0-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="138a0-224"><a id="blobs"></a>Nasıl tooread ve yazma BLOB ve bir sıraya ileti işlenirken tabloları</span><span class="sxs-lookup"><span data-stu-id="138a0-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="138a0-225">Merhaba `Blob` ve `Table` öznitelikleri tooread etkinleştirmek ve blobları ve tabloları yazma.</span><span class="sxs-lookup"><span data-stu-id="138a0-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="138a0-226">Bu bölümdeki Hello örnekler tooblobs uygulayın.</span><span class="sxs-lookup"><span data-stu-id="138a0-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="138a0-227">BLOB'ları oluşturulduğunda veya güncelleştirilmiş tootrigger nasıl işlediği gösteren kod örnekleri için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)ve okuma ve yazma tabloları kod örnekleri için bkz: [nasıl toouse Azure tablo Depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="138a0-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="138a0-228">Dize iletileri kuyruğa blobu işlemleri tetikleme</span><span class="sxs-lookup"><span data-stu-id="138a0-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="138a0-229">Bir dizeyi içeren bir kuyruk iletisi için `queueTrigger` hello kullanabileceğiniz bir yer tutucudur `Blob` özniteliğin `blobPath` selamlama iletisine Merhaba içeriğine içeren parametre.</span><span class="sxs-lookup"><span data-stu-id="138a0-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="138a0-230">Merhaba aşağıdaki örnek kullanır `Stream` tooread ve yazma BLOB'lar nesneleri.</span><span class="sxs-lookup"><span data-stu-id="138a0-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="138a0-231">Merhaba kuyruk iletisi hello textblobs kapsayıcıda bulunan bir blob hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="138a0-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="138a0-232">Merhaba blob ile bir kopyasını "-Yeni" eklenmiş toohello adı oluşturulduğu hello aynı kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="138a0-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="138a0-233">Merhaba `Blob` özniteliği Oluşturucusu alır bir `blobPath` hello kapsayıcı ve blob adı belirten parametre.</span><span class="sxs-lookup"><span data-stu-id="138a0-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="138a0-234">Bu yer tutucu hakkında daha fazla bilgi için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="138a0-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="138a0-235">Ne zaman hello öznitelik süsler bir `Stream` nesnesi, başka bir oluşturucu parametresini belirtir hello `FileAccess` modu okuma, yazma veya okuma/yazma olarak.</span><span class="sxs-lookup"><span data-stu-id="138a0-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="138a0-236">Merhaba aşağıdaki örnek kullanan bir `CloudBlockBlob` toodelete blob nesnesi.</span><span class="sxs-lookup"><span data-stu-id="138a0-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="138a0-237">Merhaba kuyruk iletisi hello blob hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="138a0-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="138a0-238"><a id="pocoblobs"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="138a0-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="138a0-239">JSON olarak hello kuyruk iletisi içinde depolanan bir POCO için hello hello nesnesinde özelliklerini adı yer tutucuları kullanabilirsiniz `Queue` özniteliğin `blobPath` parametresi.</span><span class="sxs-lookup"><span data-stu-id="138a0-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="138a0-240">Aynı zamanda [sıra meta veri özellik adları](#queuemetadata) yer tutucu olarak.</span><span class="sxs-lookup"><span data-stu-id="138a0-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="138a0-241">Merhaba aşağıdaki örnek bir blob tooa yeni blob farklı bir uzantı kopyalar.</span><span class="sxs-lookup"><span data-stu-id="138a0-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="138a0-242">Merhaba kuyruk iletisi bir `BlobInformation` içeren nesnesinin `BlobName` ve `BlobNameWithoutExtension` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="138a0-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="138a0-243">Merhaba özellik adları olarak kullanılan hello blob yolu yer tutucuları Merhaba `Blob` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="138a0-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="138a0-244">Merhaba SDK kullanan hello [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize ve iletileri seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="138a0-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="138a0-245">Merhaba WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bu hello hello örnek toocreate bir POCO kuyruk iletisi aşağıdaki gibi kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="138a0-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="138a0-246">Bazı iş toodo, bir blob tooan nesnesi bağlama önce işlevinde gerekiyorsa hello işlevi hello gövdesinde hello özniteliğini kullanabilirsiniz [hello sıra özniteliği için daha önce gösterildiği gibi](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="138a0-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="138a0-247"><a id="blobattributetypes"></a>Merhaba kullanabileceğiniz türü özniteliğiyle Blob</span><span class="sxs-lookup"><span data-stu-id="138a0-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="138a0-248">Merhaba `Blob` özniteliği şu türlerini hello ile kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="138a0-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="138a0-249">`Stream`(okuma veya yazma, hello FileAccess Oluşturucu parametresi kullanılarak belirtilen)</span><span class="sxs-lookup"><span data-stu-id="138a0-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="138a0-250">`string`(okuma)</span><span class="sxs-lookup"><span data-stu-id="138a0-250">`string` (read)</span></span>
* <span data-ttu-id="138a0-251">`out string`(yazma; hello işlevi döndüğünde yalnızca hello dizesi parametresi null olmayan ise bir blob oluşturur)</span><span class="sxs-lookup"><span data-stu-id="138a0-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="138a0-252">POCO (okuma)</span><span class="sxs-lookup"><span data-stu-id="138a0-252">POCO (read)</span></span>
* <span data-ttu-id="138a0-253">POCO out (yazma; her zaman bir blob oluşturur, hello işlevi döndüğünde POCO parametre null ise null nesnesi olarak oluşturur)</span><span class="sxs-lookup"><span data-stu-id="138a0-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="138a0-254">`CloudBlobStream`(yazma)</span><span class="sxs-lookup"><span data-stu-id="138a0-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="138a0-255">`ICloudBlob`(okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="138a0-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="138a0-256">`CloudBlockBlob`(okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="138a0-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="138a0-257">`CloudPageBlob`(okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="138a0-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="138a0-258"><a id="poison"></a>Nasıl toohandle zehirli ileti</span><span class="sxs-lookup"><span data-stu-id="138a0-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="138a0-259">İçerikleri işlevi toofail neden olan iletileri çağrılır *zehirli ileti*.</span><span class="sxs-lookup"><span data-stu-id="138a0-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="138a0-260">Merhaba işlevi başarısız olduğunda, hello kuyruk iletisi silinmez ve sonunda yeniden neden hello döngüsü toobe yinelenen kayıt.</span><span class="sxs-lookup"><span data-stu-id="138a0-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="138a0-261">otomatik olarak hello döngüsü Hello SDK sınırlı sayıda yineleme sonra kesintiye uğratabilir veya el ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="138a0-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="138a0-262">Otomatik zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="138a0-262">Automatic poison message handling</span></span>
<span data-ttu-id="138a0-263">Merhaba SDK too5 kez tooprocess bir kuyruk iletisi yukarı işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="138a0-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="138a0-264">Merhaba beşinci deneme başarısız olursa, selamlama iletisine taşınan tooa zararlı sıradır.</span><span class="sxs-lookup"><span data-stu-id="138a0-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="138a0-265">[Merhaba en fazla yeniden deneme sayısı yapılandırılabilir](#config).</span><span class="sxs-lookup"><span data-stu-id="138a0-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="138a0-266">Merhaba zararlı sıra adlandırılan *{originalqueuename}*-zararlı.</span><span class="sxs-lookup"><span data-stu-id="138a0-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="138a0-267">Bir işlev tooprocess iletileri hello zararlı sıradan günlüğe yazma veya el ile ilgilenilmesi gereken bir bildirim göndererek yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="138a0-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="138a0-268">Aşağıdaki örnek hello hello içinde `CopyBlob` bir kuyruk iletisi mevcut olmayan bir blob hello adını içerdiğinde işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="138a0-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="138a0-269">Bu durum oluştuğunda selamlama iletisine hello copyblobqueue sıra toohello copyblobqueue poison sıradan taşınır.</span><span class="sxs-lookup"><span data-stu-id="138a0-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="138a0-270">Merhaba `ProcessPoisonMessage` zehir iletisi günlükleri hello sonra.</span><span class="sxs-lookup"><span data-stu-id="138a0-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="138a0-271">zararlı bir ileti işlendiğinde hello aşağıda bu işlevler konsol çıktısı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="138a0-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Zehirli ileti işleme için konsol çıkışı](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="138a0-273">El ile zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="138a0-273">Manual poison message handling</span></span>
<span data-ttu-id="138a0-274">Hello sayısı bir ileti toplanma işleme ekleyerek alabileceğiniz bir `int` adlı parametre `dequeueCount` tooyour işlevi.</span><span class="sxs-lookup"><span data-stu-id="138a0-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="138a0-275">Bundan sonra onay hello işlev kodu sayıma dequeue ve hello sayısı hello aşağıdaki örnekte gösterildiği gibi bir eşiği aştığında kendi zehirli ileti işleme gerçekleştirmek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="138a0-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <span data-ttu-id="138a0-276"><a id="config"></a>Nasıl tooset yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="138a0-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="138a0-277">Merhaba kullanabilirsiniz `JobHostConfiguration` yapılandırma seçenekleri aşağıdaki türü tooset hello:</span><span class="sxs-lookup"><span data-stu-id="138a0-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="138a0-278">Kodda Hello SDK bağlantı dizelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="138a0-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="138a0-279">Yapılandırma `QueueTrigger` maksimum gibi ayarları dequeue sayısı.</span><span class="sxs-lookup"><span data-stu-id="138a0-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="138a0-280">Sıra adları yapılandırmasından alın.</span><span class="sxs-lookup"><span data-stu-id="138a0-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="138a0-281"><a id="setconnstr"></a>Kod içinde SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="138a0-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="138a0-282">Kodda Hello SDK bağlantı dizelerini ayarlama, toouse kendi bağlantı dizesi adlarında yapılandırma dosyalarının veya ortam değişkenleri hello aşağıdaki örnekte gösterildiği gibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="138a0-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="138a0-283"><a id="configqueue"></a>QueueTrigger ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="138a0-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="138a0-284">Toohello sıraya ileti işleme uygulanan ayarları aşağıdaki hello yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="138a0-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="138a0-285">Merhaba en fazla eşzamanlı olarak paralel olarak yürütülen toobe yukarı çekilen sıraya ileti sayısı (varsayılan olarak 16).</span><span class="sxs-lookup"><span data-stu-id="138a0-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="138a0-286">bir kuyruk iletisi tooa zararlı sıra gönderilmeden önce yeniden deneme sayısı Hello (varsayılan olarak 5).</span><span class="sxs-lookup"><span data-stu-id="138a0-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="138a0-287">bir sıranın boş olduğunda yeniden yoklama önce hello maksimum bekleme süresi (varsayılan değer 1 dakika).</span><span class="sxs-lookup"><span data-stu-id="138a0-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="138a0-288">örnekte gösterildiği nasıl aşağıdaki hello tooconfigure bu ayarları:</span><span class="sxs-lookup"><span data-stu-id="138a0-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="138a0-289"><a id="setnamesincode"></a>Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="138a0-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="138a0-290">Kuyruk adı, bir blob adı veya kapsayıcı toospecify bazen istediğiniz veya bir tablo adı kod sabit kodlu yerine onu.</span><span class="sxs-lookup"><span data-stu-id="138a0-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="138a0-291">Örneğin, toospecify hello sıra adı için isteyebilirsiniz `QueueTrigger` bir yapılandırma dosyası veya ortam değişkeninde.</span><span class="sxs-lookup"><span data-stu-id="138a0-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="138a0-292">Bunu geçirerek yapabilirsiniz bir `NameResolver` toohello nesne `JobHostConfiguration` türü.</span><span class="sxs-lookup"><span data-stu-id="138a0-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="138a0-293">Web işleri SDK'si özniteliği Oluşturucusu parametrelerinde yüzde (%) işareti tarafından çevrelenen özel yer tutucular içerir ve `NameResolver` kod bu yer tutucular yerine kullanılan hello gerçek değerler toobe belirtir.</span><span class="sxs-lookup"><span data-stu-id="138a0-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="138a0-294">Örneğin, toouse istediğinizi düşünelim bir sıra hello test ortamında logqueuetest ve üretimde bir adlandırılmış logqueueprod adlı.</span><span class="sxs-lookup"><span data-stu-id="138a0-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="138a0-295">Sabit kodlanmış kuyruk adı yerine bir girişe hello toospecify hello adı istediğiniz `appSettings` hello gerçek sıra adı olurdu koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="138a0-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="138a0-296">Merhaba, `appSettings` anahtarı logqueue, işlevinizi aşağıdaki örneğine hello gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="138a0-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="138a0-297">`NameResolver` Sınıfını hello sıra adından sonra almak `appSettings` hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="138a0-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="138a0-298">Merhaba geçirdiğiniz `NameResolver` toohello sınıfında `JobHost` nesne hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="138a0-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="138a0-299">**Not:** kuyruk, tablo ve blob adları çözümlenmiş her zaman bir işlev çağrılır, ancak blob kapsayıcı adları yalnızca Merhaba uygulaması başladığında çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="138a0-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="138a0-300">Merhaba iş çalışırken blob kapsayıcı adı değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="138a0-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="138a0-301"><a id="manual"></a>Nasıl tootrigger bir işlev el ile</span><span class="sxs-lookup"><span data-stu-id="138a0-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="138a0-302">tootrigger işlevi el ile Merhaba kullanmak `Call` veya `CallAsync` hello yöntemi `JobHost` nesne ve hello `NoAutomaticTrigger` hello aşağıdaki örnekte gösterildiği gibi hello işlevi üzerinde özniteliği.</span><span class="sxs-lookup"><span data-stu-id="138a0-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <span data-ttu-id="138a0-303"><a id="logs"></a>Toowrite nasıl kaydeder</span><span class="sxs-lookup"><span data-stu-id="138a0-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="138a0-304">Başlangıç Panosu iki yerde günlükleri gösterir: hello sayfası hello Web işi için ve belirli bir Web işi çağırma için hello sayfası.</span><span class="sxs-lookup"><span data-stu-id="138a0-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Web işi sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![İşlev çağırma sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="138a0-307">Bir işlev veya hello çağıran konsol yöntemlerini çıkışı `Main()` yöntemi görünür hello Web işi için hello Pano sayfası, belirli yöntem çağırma için hello sayfasındaki değil.</span><span class="sxs-lookup"><span data-stu-id="138a0-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="138a0-308">Çıktı yöntemi imzanız bir parametresinden alma hello TextWriter nesneden bir yöntem çağırma için hello Pano sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="138a0-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="138a0-309">Konsol çıktısı, bağlantılı tooa belirli yöntemi çağırma olamaz, hello konsol birçok iş işlevlerinin hello çalışmıyor olabilir tek iş parçacıklı, olduğu için aynı anda.</span><span class="sxs-lookup"><span data-stu-id="138a0-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="138a0-310">İşte bu nedenle hello SDK her işlev çağrısını kendi benzersiz günlük yazıcı nesnesi ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="138a0-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="138a0-311">toowrite [uygulama izleme günlükleri](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), kullanın `Console.Out` (bilgisi olarak işaretlenmiş günlükleri oluşturur) ve `Console.Error` (hata olarak işaretlenmiş günlükleri oluşturur).</span><span class="sxs-lookup"><span data-stu-id="138a0-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="138a0-312">Toouse alternatiftir [izleme veya TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), uyarı, ayrıntı sağlar ve kritik düzeyleri toplama tooInfo ve hata.</span><span class="sxs-lookup"><span data-stu-id="138a0-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="138a0-313">Azure web uygulamanızı nasıl yapılandırdığınıza bağlı olarak Azure BLOB veya uygulama izleme günlükleri hello web uygulama günlük dosyalarında Azure tabloları görünür.</span><span class="sxs-lookup"><span data-stu-id="138a0-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="138a0-314">Tüm konsol çıktısı doğru olduğu gibi hello en son 100 uygulama günlüklerini da hello Web işi, olmayan bir işlev çağrısını hello sayfasını için hello Pano sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="138a0-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="138a0-315">Merhaba hello programı yerel olarak çalışmıyorsa hello program bir Azure WebJob içinde yalnızca çalışıyorsa, Pano veya başka bir ortamında konsol çıktısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="138a0-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="138a0-316">Yüksek verimlilik senaryolar için panoyu günlüğü devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="138a0-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="138a0-317">Varsayılan olarak, günlükler toostorage hello SDK yazar ve birçok iletilerini işlerken bu etkinliği performansının düşmesine neden.</span><span class="sxs-lookup"><span data-stu-id="138a0-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="138a0-318">Günlük, toodisable hello aşağıdaki örnekte gösterildiği gibi hello Pano bağlantı dizesi toonull ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="138a0-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="138a0-319">Merhaba aşağıdaki örnekte çeşitli yollar gösterir toowrite günlükleri:</span><span class="sxs-lookup"><span data-stu-id="138a0-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="138a0-320">Hello WebJobs SDK Pano, hello hello çıktısını `TextWriter` toohello sayfa belirli bir zaman gittiğiniz yukarı gösterir işlev çağırma ve tıklatın nesnesi **geçiş çıktı**:</span><span class="sxs-lookup"><span data-stu-id="138a0-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![İşlev çağırma bağlantısına tıklayın](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![İşlev çağırma sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="138a0-323">Merhaba WebJob (değil hello işlev çağrısını) için toohello sayfasına gidin ve'ı tıklattığınızda hello WebJobs SDK Pano, konsolunun hello en son 100 satırları göster yukarı çıktı **geçiş çıktı**.</span><span class="sxs-lookup"><span data-stu-id="138a0-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Çıkışı Aç/Kapat'ı tıklatın](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="138a0-325">Bir sürekli Webjob'un uygulama günlüklerini/data/işleri/sürekli/içinde gösterilmesi*{webjobname}*hello web uygulama dosya sisteminde /job_log.txt.</span><span class="sxs-lookup"><span data-stu-id="138a0-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="138a0-326">Azure blob hello uygulamada günlükleri şuna benzeyebilir: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Merhaba Dünya!, 2014-09-26T21:01:13, hata, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Merhaba Dünya!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Merhaba Dünya!,</span><span class="sxs-lookup"><span data-stu-id="138a0-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="138a0-327">Ve Azure tablo hello `Console.Out` ve `Console.Error` günlükleri şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="138a0-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Tablo bilgi günlüğüne](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Hata günlüğü tablosundaki](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="138a0-330">Kendi Günlükçü tooplug istiyorsanız, bkz: [Bu örnek](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="138a0-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="138a0-331"><a id="errors"></a>Nasıl toohandle hataları ve zaman aşımları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="138a0-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="138a0-332">Merhaba WebJobs SDK de içeren bir [zaman aşımı](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) işlevi toobe iptal varsa toocause kullanabileceğiniz öznitelik belirtilen sürede tamamlamak değil.</span><span class="sxs-lookup"><span data-stu-id="138a0-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="138a0-333">Belirtilen bir süre içinde çok fazla hata oluştuğunda tooraise bir uyarı istiyorsanız, hello kullanabileceğiniz `ErrorTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="138a0-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="138a0-334">Burada bir [ErrorTrigger örnek](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="138a0-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="138a0-335">Ayrıca dinamik olarak devre dışı bırakın ve bunlar, bir uygulama ayarı veya ortam değişkeni adı olabilir bir yapılandırma anahtarı kullanarak tetiklenebilir olup olmadığını işlevleri toocontrol etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="138a0-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="138a0-336">Merhaba örnek kod için bkz: `Disable` özniteliğini [hello Web işleri SDK'si örnekleri depo](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="138a0-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="138a0-337"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="138a0-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="138a0-338">Bu kılavuz kodu sağlamıştır gösteren nasıl örnekleri Azure kuyruklarla çalışmaya yönelik yaygın senaryolar toohandle.</span><span class="sxs-lookup"><span data-stu-id="138a0-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="138a0-339">Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="138a0-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
