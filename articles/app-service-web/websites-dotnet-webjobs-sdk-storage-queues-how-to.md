---
title: "WebJobs SDK ile Azure kuyruk depolama kullanımı"
description: "Azure kuyruk depolama WebJobs SDK ile kullanmayı öğrenin. Oluşturma ve kuyrukları silin; Ekle, Gözat, Al ve iletileri kuyruğa ve daha fazlasını silin."
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
ms.openlocfilehash: 63b987a2c9471f2929b8d2dd605323910d2ad43b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-queue-storage-with-the-webjobs-sdk"></a><span data-ttu-id="9e0fa-104">WebJobs SDK ile Azure kuyruk depolama kullanımı</span><span class="sxs-lookup"><span data-stu-id="9e0fa-104">How to use Azure queue storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="9e0fa-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9e0fa-105">Overview</span></span>
<span data-ttu-id="9e0fa-106">Bu kılavuz, Azure WebJobs SDK sürümü kullanmak nasıl gösteren C# kod örnekleri sağlar 1.x Azure kuyruk depolama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-106">This guide provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure queue storage service.</span></span>

<span data-ttu-id="9e0fa-107">Bildiğiniz Kılavuzu varsayar [bağlantıyla Visual Studio'da bir Web işi projesi oluşturma, depolama hesabınıza o noktadan dizeleri](websites-dotnet-webjobs-sdk-get-started.md) veya [birden çok depolama hesabı](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-107">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="9e0fa-108">Kod parçacıkları çoğunu İşlevler, oluşturur kod değil yalnızca Göster `JobHost` nesne bu örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-108">Most of the code snippets only show functions, not the code that creates the `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="9e0fa-109">Kılavuzu, aşağıdaki konuları içerir:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-109">The guide includes the following topics:</span></span>

* [<span data-ttu-id="9e0fa-110">Bir kuyruk iletisi alındığında bir işlev tetikleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-110">How to trigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="9e0fa-111">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-111">String queue messages</span></span>
  * <span data-ttu-id="9e0fa-112">POCO iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-112">POCO queue messages</span></span>
  * <span data-ttu-id="9e0fa-113">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-113">Async functions</span></span>
  * <span data-ttu-id="9e0fa-114">Türleri QueueTrigger öznitelik birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-114">Types the QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="9e0fa-115">Yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="9e0fa-115">Polling algorithm</span></span>
  * <span data-ttu-id="9e0fa-116">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="9e0fa-116">Multiple instances</span></span>
  * <span data-ttu-id="9e0fa-117">Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-117">Parallel execution</span></span>
  * <span data-ttu-id="9e0fa-118">Sıra veya sıra ileti meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="9e0fa-119">Kapama</span><span class="sxs-lookup"><span data-stu-id="9e0fa-119">Graceful shutdown</span></span>
* [<span data-ttu-id="9e0fa-120">Bir kuyruk iletisi işlenirken bir kuyruk iletisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-120">How to create a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="9e0fa-121">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-121">String queue messages</span></span>
  * <span data-ttu-id="9e0fa-122">POCO iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-122">POCO queue messages</span></span>
  * <span data-ttu-id="9e0fa-123">Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="9e0fa-124">Türleri sıra özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-124">Types the Queue attribute works with</span></span>
  * <span data-ttu-id="9e0fa-125">Web işleri SDK'si öznitelikleri bir işlev gövdesine kullanın</span><span class="sxs-lookup"><span data-stu-id="9e0fa-125">Use WebJobs SDK attributes in the body of a function</span></span>
* [<span data-ttu-id="9e0fa-126">Nasıl okunacağını ve bir sıraya ileti işlenirken yazma BLOB'ları</span><span class="sxs-lookup"><span data-stu-id="9e0fa-126">How to read and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="9e0fa-127">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-127">String queue messages</span></span>
  * <span data-ttu-id="9e0fa-128">POCO iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-128">POCO queue messages</span></span>
  * <span data-ttu-id="9e0fa-129">Türleri Blob özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-129">Types the Blob attribute works with</span></span>
* [<span data-ttu-id="9e0fa-130">Zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-130">How to handle poison messages</span></span>](#poison)
  * <span data-ttu-id="9e0fa-131">Otomatik zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="9e0fa-132">El ile zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-132">Manual poison message handling</span></span>
* [<span data-ttu-id="9e0fa-133">Yapılandırma seçeneklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="9e0fa-133">How to set configuration options</span></span>](#config)
  * <span data-ttu-id="9e0fa-134">Kod içinde SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="9e0fa-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="9e0fa-135">QueueTrigger ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="9e0fa-136">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="9e0fa-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="9e0fa-137">Bir işlev el ile tetikleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-137">How to trigger a function manually</span></span>](#manual)
* [<span data-ttu-id="9e0fa-138">Günlükleri yazma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-138">How to write logs</span></span>](#logs)
* [<span data-ttu-id="9e0fa-139">Hataları işlemek ve zaman aşımları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-139">How to handle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="9e0fa-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e0fa-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="9e0fa-141"><a id="trigger"></a>Bir kuyruk iletisi alındığında bir işlev tetikleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-141"><a id="trigger"></a> How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="9e0fa-142">Bir kuyruk iletisi alındığında WebJobs SDK çağıran bir işlev yazmak için `QueueTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-142">To write a function that the WebJobs SDK calls when a queue message is received, use the `QueueTrigger` attribute.</span></span> <span data-ttu-id="9e0fa-143">Öznitelik oluşturucunun yoklamak için sıra adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-143">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="9e0fa-144">Ayrıca [sıra adı dinamik olarak ayarlamak](#config).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-144">You can also [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="9e0fa-145">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-145">String queue messages</span></span>
<span data-ttu-id="9e0fa-146">Bir dize ileti sırası aşağıdaki örnekte, bu nedenle içerir `QueueTrigger` adlı bir dize parametresi uygulanan `logMessage` kuyruk iletisini içeriğini içerir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-146">In the following example, the queue contains a string message, so `QueueTrigger` is applied to a string parameter named `logMessage` which contains the content of the queue message.</span></span> <span data-ttu-id="9e0fa-147">İşlev [Pano için bir günlük iletisi Yazar](#logs).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-147">The function [writes a log message to the Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="9e0fa-148">Yanında `string`, parametresi bir bayt dizisi olabilir bir `CloudQueueMessage` nesne ya da tanımladığınız bir POCO.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-148">Besides `string`, the parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="9e0fa-149">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="9e0fa-150">Aşağıdaki örnekte, JSON için kuyruk iletisini içeren bir `BlobInformation` içeren nesne bir `BlobName` özelliği.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-150">In the following example, the queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="9e0fa-151">SDK'yı otomatik olarak nesne seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-151">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="9e0fa-152">SDK'sı [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) seri hale getirmek ve seri durumdan iletileri.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-152">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="9e0fa-153">WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bir POCO kuyruk iletisi oluşturmak için aşağıdaki örneğe benzer kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-153">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="9e0fa-154">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-154">Async functions</span></span>
<span data-ttu-id="9e0fa-155">Aşağıdaki zaman uyumsuz işlev [bir günlüğü panoya Yazar](#logs).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-155">The following async function [writes a log to the Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="9e0fa-156">Zaman uyumsuz işlevleri sürebilir bir [iptal belirteci](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)blob kopyalar aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="9e0fa-157">(Bir açıklaması için `queueTrigger` yer tutucu, bkz: [BLOB'lar](#blobs) bölümüne.)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-157">(For an explanation of the `queueTrigger` placeholder, see the [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="9e0fa-158"><a id="qtattributetypes"></a>Türleri QueueTrigger öznitelik birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-158"><a id="qtattributetypes"></a> Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="9e0fa-159">Kullanabileceğiniz `QueueTrigger` şu türden:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-159">You can use `QueueTrigger` with the following types:</span></span>

* `string`
* <span data-ttu-id="9e0fa-160">JSON olarak serileştirilen bir POCO türü</span><span class="sxs-lookup"><span data-stu-id="9e0fa-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="9e0fa-161"><a id="polling"></a>Yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="9e0fa-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="9e0fa-162">SDK boşta kuyruk depolama işlem maliyetleri yoklama etkisini azaltmak için bir rastgele üstel geri alma algoritması uygular.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-162">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="9e0fa-163">Bir ileti bulunduğunda, SDK iki saniye bekler ve ardından başka bir ileti için denetler; bir ileti bulunduğunda yeniden denemeden önce yaklaşık dört saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-163">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="9e0fa-164">Bir kuyruk iletisi almak için sonraki başarısız girişimden sonra bekleme süresini bir dakika olarak varsayılan olarak en fazla bekleme süresi ulaşana kadar artmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-164">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="9e0fa-165">[En fazla bekleme süresi yapılandırılabilir](#config).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-165">[The maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="9e0fa-166"><a id="instances"></a>Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="9e0fa-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="9e0fa-167">Web uygulamanız birden çok örneği üzerinde çalışıyorsa, bir sürekli Webjob'un her makinede çalışır ve her makine için Tetikleyicileri bekleyin ve işlevleri çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="9e0fa-168">Web işleri SDK'si sıra tetikleyici otomatik olarak bir işlev bir kuyruk iletisi birden çok kez önlediği; İşlevler ıdempotent olmasını yazılması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-168">The WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have to be written to be idempotent.</span></span> <span data-ttu-id="9e0fa-169">Ancak, yalnızca bir örneğini emin olmak istiyorsanız bile ana web uygulamanızın birden fazla örneği bulunduğunda bir işlevi çalıştırır, kullanabileceğiniz `Singleton` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-169">However, if you want to ensure that only one instance of a function runs even when there are multiple instances of the host web app, you can use the `Singleton` attribute.</span></span>

### <span data-ttu-id="9e0fa-170"><a id="parallel"></a>Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="9e0fa-171">Birden çok işlevler farklı sıralarda dinleme varsa, iletileri aynı anda alındığında SDK bunları paralel olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-171">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="9e0fa-172">Tek bir kuyruk için birden fazla ileti alındığında aynı durum geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-172">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="9e0fa-173">Varsayılan olarak, SDK 16 iletileri kuyruğa toplu bir zaman alır ve paralel olarak işler işlevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-173">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="9e0fa-174">[Toplu iş boyutu yapılandırılabilir](#config).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-174">[The batch size is configurable](#config).</span></span> <span data-ttu-id="9e0fa-175">İşlenmekte olan numarası yarısı toplu iş boyutu aldığında, SDK başka bir toplu iş alır ve bu iletileri işleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-175">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="9e0fa-176">Bu nedenle en fazla eş zamanlı ileti işlevi işlenen sayısı bir ve yarı kez bir toplu iş boyutu dur.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-176">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="9e0fa-177">Bu sınırı olan her işlev ayrı olarak geçerli bir `QueueTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-177">This limit applies separately to each function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="9e0fa-178">Paralel yürütme üzerinde bir Sıraya alınan iletileri istemiyorsanız, yığın boyutu 1 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-178">If you don't want parallel execution for messages received on one queue, you can set the batch size to 1.</span></span> <span data-ttu-id="9e0fa-179">Ayrıca bkz. **sırası işleme üzerinde daha fazla denetim** içinde [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="9e0fa-180"><a id="queuemetadata"></a>Sıra veya sıra ileti meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="9e0fa-181">Aşağıdaki ileti özellikleri yöntemi imza parametreleri ekleyerek alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-181">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="9e0fa-182">`DateTimeOffset`expirationTime</span><span class="sxs-lookup"><span data-stu-id="9e0fa-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="9e0fa-183">`DateTimeOffset`insertionTime</span><span class="sxs-lookup"><span data-stu-id="9e0fa-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="9e0fa-184">`DateTimeOffset`nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="9e0fa-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="9e0fa-185">`string`queueTrigger (ileti metni içerir)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="9e0fa-186">`string`Kimliği</span><span class="sxs-lookup"><span data-stu-id="9e0fa-186">`string` id</span></span>
* <span data-ttu-id="9e0fa-187">`string`popReceipt</span><span class="sxs-lookup"><span data-stu-id="9e0fa-187">`string` popReceipt</span></span>
* <span data-ttu-id="9e0fa-188">`int`dequeueCount</span><span class="sxs-lookup"><span data-stu-id="9e0fa-188">`int` dequeueCount</span></span>

<span data-ttu-id="9e0fa-189">Azure depolama alanıyla doğrudan API çalışmak isterseniz, ayrıca ekleyebileceğiniz bir `CloudStorageAccount` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-189">If you want to work directly with the Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="9e0fa-190">Aşağıdaki örnekte tüm bu meta veri bilgileri uygulama günlüğüne yazar.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-190">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="9e0fa-191">Örnekte, kuyruk iletisini içeriğini logMessage ve queueTrigger içerir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-191">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="9e0fa-192">Örnek kodu ile yazılmış bir örnek günlük şöyledir:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-192">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="9e0fa-193"><a id="graceful"></a>Kapama</span><span class="sxs-lookup"><span data-stu-id="9e0fa-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="9e0fa-194">Sürekli bir WebJob içinde çalışan bir işlevinin kabul edebileceği bir `CancellationToken` işlevi hakkında sonlandırılacak WebJob olduğunu bildirmek işletim sistemi sağlayan parametre.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="9e0fa-195">Bu bildirim, beklenmedik bir şekilde veri tutarsız bir durumda bırakır şekilde sonlandırma işlevi değil emin olmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-195">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="9e0fa-196">Aşağıdaki örnek, bir işlev yaklaşan WebJob sonlandırma denetlemek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-196">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="9e0fa-197">**Not:** durumunu ve çıkışını kapatılmışsa işlevlerin Pano doğru gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-197">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="9e0fa-198">Daha fazla bilgi için bkz: [Web işleri normal şekilde kapatılmasını](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="9e0fa-199"><a id="createqueue"></a>Bir kuyruk iletisi işlenirken bir kuyruk iletisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-199"><a id="createqueue"></a> How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="9e0fa-200">Yeni bir kuyruk iletisi oluşturan bir işlev yazmak için `Queue` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-200">To write a function that creates a new queue message, use the `Queue` attribute.</span></span> <span data-ttu-id="9e0fa-201">Gibi `QueueTrigger`, kuyruk adı bir dize olarak geçirin veya yapabilecekleriniz [sıra adı dinamik olarak ayarlamak](#config).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-201">Like `QueueTrigger`, you pass in the queue name as a string or you can [set the queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="9e0fa-202">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-202">String queue messages</span></span>
<span data-ttu-id="9e0fa-203">Aşağıdaki zaman uyumsuz olmayan kod örneği sıranın "inputqueue" adlı sıraya alınan kuyruk iletisini aynı içerikle "outputqueue" adlı yeni bir kuyruk iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-203">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="9e0fa-204">(İşlevler için async kullanma `IAsyncCollector<T>` daha sonra bu bölümde gösterilen.)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="9e0fa-205">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="9e0fa-206">Bir dize yerine bir POCO içeren bir kuyruk iletisi oluşturmak için bir çıktı parametresi olarak POCO türü geçirmek `Queue` özniteliği Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-206">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="9e0fa-207">SDK'yı otomatik olarak JSON nesneyi serileştirir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-207">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="9e0fa-208">Nesne boş olsa bile bir kuyruk iletisi her zaman oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-208">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="9e0fa-209">Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="9e0fa-210">Birden çok iletileri oluşturmak için çıkış sırası için parametre türü olun `ICollector<T>` veya `IAsyncCollector<T>`, aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-210">To create multiple messages, make the parameter type for the output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="9e0fa-211">Her kuyruk iletisi hemen oluşturulan zaman `Add` yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-211">Each queue message is created immediately when the `Add` method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="9e0fa-212">Sıra özniteliği çalışır türleri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-212">Types that the Queue attribute works with</span></span>
<span data-ttu-id="9e0fa-213">Kullanabileceğiniz `Queue` özniteliği aşağıdaki parametre türleri:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-213">You can use the `Queue` attribute on the following parameter types:</span></span>

* <span data-ttu-id="9e0fa-214">`out string`(işlev sona erdiğinde parametre değeri null olmayan ise kuyruk iletisi oluşturur)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-214">`out string` (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="9e0fa-215">`out byte[]`(gibi çalışır `string`)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="9e0fa-216">`out CloudQueueMessage`(gibi çalışır `string`)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="9e0fa-217">`out POCO`(serializable bir tür oluşturduğu bir ileti null bir nesne ile işlevi sona erdiğinde parametre null ise)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-217">`out POCO` (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="9e0fa-218">`CloudQueue`(iletileri el ile oluşturmak için Azure Storage API'sini kullanarak doğrudan)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-218">`CloudQueue` (for creating messages manually using the Azure Storage API directly)</span></span>

### <span data-ttu-id="9e0fa-219"><a id="ibinder"></a>Web işleri SDK'si öznitelikleri bir işlev gövdesine kullanın</span><span class="sxs-lookup"><span data-stu-id="9e0fa-219"><a id="ibinder"></a>Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="9e0fa-220">Web işleri SDK'si öznitelik gibi kullanmadan önce işlevinizi bazı iş yapmanız gerekirse `Queue`, `Blob`, veya `Table`, kullanabileceğiniz `IBinder` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-220">If you need to do some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use the `IBinder` interface.</span></span>

<span data-ttu-id="9e0fa-221">Aşağıdaki örnek, bir giriş sırası iletisi alır ve bir çıkış sırası aynı içeriği ile yeni bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-221">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="9e0fa-222">Çıkış sırası adı işlevinin gövdesini kodda tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-222">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="9e0fa-223">`IBinder` Arabirimi de kullanılabilir olan `Table` ve `Blob` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-223">The `IBinder` interface can also be used with the `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="9e0fa-224"><a id="blobs"></a>Nasıl okunacağını ve yazma BLOB'ları ve bir sıraya ileti işlenirken tabloları</span><span class="sxs-lookup"><span data-stu-id="9e0fa-224"><a id="blobs"></a> How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="9e0fa-225">`Blob` Ve `Table` öznitelikleri BLOB'ları ve tabloları okuma ve yazma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-225">The `Blob` and `Table` attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="9e0fa-226">Bu bölümdeki örnekler BLOB'lar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-226">The samples in this section apply to blobs.</span></span> <span data-ttu-id="9e0fa-227">BLOB'ları oluşturulduğunda veya güncelleştirilmiş işlemleri tetiklemek nasıl gösteren kod örnekleri için bkz: [WebJobs SDK ile Azure blob storage kullanma](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)ve okuma ve yazma tabloları kod örnekleri için bkz: [WebJobs SDK ile Azure table storage kullanma](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-227">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="9e0fa-228">Dize iletileri kuyruğa blobu işlemleri tetikleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="9e0fa-229">Bir dizeyi içeren bir kuyruk iletisi için `queueTrigger` olarak kullanabileceğiniz bir yer tutucudur `Blob` özniteliğin `blobPath` iletinin içeriğini içeren bir parametre.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in the `Blob` attribute's `blobPath` parameter that contains the contents of the message.</span></span>

<span data-ttu-id="9e0fa-230">Aşağıdaki örnek kullanır `Stream` nesneleri okumak ve BLOB'ları yazmak için.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-230">The following example uses `Stream` objects to read and write blobs.</span></span> <span data-ttu-id="9e0fa-231">Kuyruk iletisini textblobs kapsayıcıda bulunan bir blob adıdır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-231">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="9e0fa-232">Blob ile birlikte bir kopyasını "-Yeni" eklenecek ad aynı kapsayıcıda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-232">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="9e0fa-233">`Blob` Özniteliği Oluşturucusu alır bir `blobPath` kapsayıcısı ve blob adını belirten parametre.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-233">The `Blob` attribute constructor takes a `blobPath` parameter that specifies the container and blob name.</span></span> <span data-ttu-id="9e0fa-234">Bu yer tutucu hakkında daha fazla bilgi için bkz: [WebJobs SDK ile Azure blob storage kullanma](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="9e0fa-234">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="9e0fa-235">Ne zaman öznitelik süsler bir `Stream` nesnesi, başka bir oluşturucu parametresini belirtir `FileAccess` modu okuma, yazma veya okuma/yazma olarak.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-235">When the attribute decorates a `Stream` object, another constructor parameter specifies the `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="9e0fa-236">Aşağıdaki örnek kullanan bir `CloudBlockBlob` bir blobu silmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-236">The following example uses a `CloudBlockBlob` object to delete a blob.</span></span> <span data-ttu-id="9e0fa-237">Kuyruk iletisini blob adıdır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-237">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="9e0fa-238"><a id="pocoblobs"></a>POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="9e0fa-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="9e0fa-239">Kuyruk iletisini JSON olarak depolanan bir POCO için nesnenin özelliklerini adı yer tutucuları kullanabilirsiniz `Queue` özniteliğin `blobPath` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-239">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="9e0fa-240">Aynı zamanda [sıra meta veri özellik adları](#queuemetadata) yer tutucu olarak.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="9e0fa-241">Aşağıdaki örnek yeni bir blob farklı bir uzantıya sahip bir blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-241">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="9e0fa-242">Kuyruk iletisi bir `BlobInformation` içeren nesnesinin `BlobName` ve `BlobNameWithoutExtension` özellikleri.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-242">The queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="9e0fa-243">Blob yolu için yer tutucu olarak kullanılan özellik adları `Blob` öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-243">The property names are used as placeholders in the blob path for the `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="9e0fa-244">SDK'sı [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) seri hale getirmek ve seri durumdan iletileri.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-244">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="9e0fa-245">WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bir POCO kuyruk iletisi oluşturmak için aşağıdaki örneğe benzer kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-245">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="9e0fa-246">Bir blob için bir nesne bağlama önce işlevinizi bazı iş gerçekleştirmeniz gerekiyorsa, işlevinin gövdesini özniteliğinde kullanabilirsiniz [sıra özniteliği için daha önce gösterildiği gibi](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-246">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, [as shown earlier for the Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="9e0fa-247"><a id="blobattributetypes"></a>Blob özniteliğiyle kullanabileceğiniz türü</span><span class="sxs-lookup"><span data-stu-id="9e0fa-247"><a id="blobattributetypes"></a> Types you can use the Blob attribute with</span></span>
<span data-ttu-id="9e0fa-248">`Blob` Özniteliği şu türleriyle kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-248">The `Blob` attribute can be used with the following types:</span></span>

* <span data-ttu-id="9e0fa-249">`Stream`(okuma veya yazma, FileAccess Oluşturucu parametresi kullanılarak belirtilen)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-249">`Stream` (read or write, specified by using the FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="9e0fa-250">`string`(okuma)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-250">`string` (read)</span></span>
* <span data-ttu-id="9e0fa-251">`out string`(yazma; işlevi döndüğünde yalnızca dize parametresi null olmayan ise bir blob oluşturur)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-251">`out string` (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="9e0fa-252">POCO (okuma)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-252">POCO (read)</span></span>
* <span data-ttu-id="9e0fa-253">POCO out (yazma; her zaman bir blob oluşturur, işlevi döndüğünde POCO parametre null ise null nesnesi olarak oluşturur)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="9e0fa-254">`CloudBlobStream`(yazma)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="9e0fa-255">`ICloudBlob`(okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="9e0fa-256">`CloudBlockBlob`(okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="9e0fa-257">`CloudPageBlob`(okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="9e0fa-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="9e0fa-258"><a id="poison"></a>Zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-258"><a id="poison"></a> How to handle poison messages</span></span>
<span data-ttu-id="9e0fa-259">İçerikleri bir işlev başarısız olmasına neden olan iletileri çağrılır *zehirli ileti*.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-259">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="9e0fa-260">İşlev başarısız olduğunda, kuyruk iletisini silinmez ve sonunda tekrar tekrar için döngü neden kayıt.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-260">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="9e0fa-261">SDK'yı otomatik olarak sınırlı sayıda yineleme sonra döngüsü engelleyebilecek veya el ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-261">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="9e0fa-262">Otomatik zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-262">Automatic poison message handling</span></span>
<span data-ttu-id="9e0fa-263">SDK bir kuyruk iletisi işleyemedi 5 kata işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-263">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="9e0fa-264">Beşinci deneme başarısız olursa, ileti zararlı kuyruğuna taşınır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-264">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="9e0fa-265">[En fazla yeniden deneme sayısı yapılandırılabilir](#config).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-265">[The maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="9e0fa-266">Adlı zararlı sırası *{originalqueuename}*-zararlı.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-266">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="9e0fa-267">Günlüğe yazma veya el ile ilgili dikkat bir bildirim göndererek zararlı sırasından iletilerini işlemek için bir işlev gerekli yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-267">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="9e0fa-268">Aşağıdaki örnekte `CopyBlob` bir kuyruk iletisi mevcut olmayan bir blob adını içerdiğinde işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-268">In the following example the `CopyBlob` function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="9e0fa-269">Bu durum oluştuğunda ileti copyblobqueue poison kuyruğuna copyblobqueue sıradan taşınır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-269">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="9e0fa-270">`ProcessPoisonMessage` Zehir iletisi günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-270">The `ProcessPoisonMessage` then logs the poison message.</span></span>

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
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="9e0fa-271">Zararlı bir ileti işlenirken bu işlevler konsol çıktısı aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-271">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Zehirli ileti işleme için konsol çıkışı](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="9e0fa-273">El ile zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-273">Manual poison message handling</span></span>
<span data-ttu-id="9e0fa-274">Ekleyerek sayısı bir ileti toplanma işleme alabilirsiniz bir `int` adlı parametre `dequeueCount` , işlevi.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-274">You can get the number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` to your function.</span></span> <span data-ttu-id="9e0fa-275">Ardından, işlev kodu dequeue sayıma denetleyin ve sayısı bir eşiği aştığında kendi zehir iletisi aşağıdaki örnekte gösterildiği gibi işleme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-275">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <span data-ttu-id="9e0fa-276"><a id="config"></a>Yapılandırma seçeneklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="9e0fa-276"><a id="config"></a> How to set configuration options</span></span>
<span data-ttu-id="9e0fa-277">Kullanabileceğiniz `JobHostConfiguration` türü aşağıdaki yapılandırma seçeneklerini ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-277">You can use the `JobHostConfiguration` type to set the following configuration options:</span></span>

* <span data-ttu-id="9e0fa-278">Kod içinde SDK bağlantı dizelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-278">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="9e0fa-279">Yapılandırma `QueueTrigger` maksimum gibi ayarları dequeue sayısı.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="9e0fa-280">Sıra adları yapılandırmasından alın.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="9e0fa-281"><a id="setconnstr"></a>Kod içinde SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="9e0fa-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="9e0fa-282">Kodda SDK bağlantı dizelerini ayarlama, kendi bağlantı dizesi adlarında yapılandırma dosyalarının veya ortam değişkenlerini kullanmak aşağıdaki örnekte gösterildiği gibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-282">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <span data-ttu-id="9e0fa-283"><a id="configqueue"></a>QueueTrigger ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="9e0fa-284">Sıra ileti işleme için uygulama aşağıdaki ayarları yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-284">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="9e0fa-285">En fazla eşzamanlı olarak paralel olarak yürütülecek toplanmış sıra ileti sayısı (varsayılan olarak 16).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-285">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="9e0fa-286">Bir kuyruk iletisi zararlı bir sıraya gönderilmeden önce yeniden deneme sayısı (varsayılan olarak 5).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-286">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="9e0fa-287">En fazla bekleme süresi bir sıra boş olduğunda yeniden yoklama önce (varsayılan değer 1 dakika).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-287">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="9e0fa-288">Aşağıdaki örnek, bu ayarların nasıl yapılandırılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-288">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="9e0fa-289"><a id="setnamesincode"></a>Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="9e0fa-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="9e0fa-290">Kuyruk adı, bir blob adı veya kapsayıcı belirtmek istediğiniz bazen veya bir tablo adı kod sabit kodlu yerine onu.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-290">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="9e0fa-291">Örneğin, kuyruk adı belirtmek isteyebilirsiniz `QueueTrigger` bir yapılandırma dosyası veya ortam değişkeninde.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-291">For example, you might want to specify the queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="9e0fa-292">Bunu geçirerek yapabilirsiniz bir `NameResolver` nesnesine `JobHostConfiguration` türü.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-292">You can do that by passing in a `NameResolver` object to the `JobHostConfiguration` type.</span></span> <span data-ttu-id="9e0fa-293">Web işleri SDK'si özniteliği Oluşturucusu parametrelerinde yüzde (%) işareti tarafından çevrelenen özel yer tutucular içerir ve `NameResolver` kod bu yer tutucular yerine kullanılacak gerçek değerler belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="9e0fa-294">Örneğin, test ortamında logqueuetest ve üretimde bir adlandırılmış logqueueprod adlı bir sıra kullanmak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-294">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="9e0fa-295">Bir giriş adını belirtmek istediğiniz sabit kodlanmış kuyruk adı yerine `appSettings` gerçek sıra adı olurdu koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-295">Instead of a hard-coded queue name, you want to specify the name of an entry in the `appSettings` collection that would have the actual queue name.</span></span> <span data-ttu-id="9e0fa-296">Varsa `appSettings` anahtar logqueue, işlevinizi aşağıdaki gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-296">If the `appSettings` key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="9e0fa-297">`NameResolver` Sınıfını sıra adından sonra almak `appSettings` aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-297">Your `NameResolver` class could then get the queue name from `appSettings` as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="9e0fa-298">Geçirdiğiniz `NameResolver` için sınıfını `JobHost` nesne aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-298">You pass the `NameResolver` class in to the `JobHost` object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="9e0fa-299">**Not:** kuyruk, tablo ve blob adları çözümlenmiş her zaman bir işlev çağrılır, ancak blob kapsayıcı adları yalnızca uygulama başladığında çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="9e0fa-300">İş çalışırken blob kapsayıcı adı değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-300">You can't change blob container name while the job is running.</span></span>

## <span data-ttu-id="9e0fa-301"><a id="manual"></a>Bir işlev el ile tetikleme</span><span class="sxs-lookup"><span data-stu-id="9e0fa-301"><a id="manual"></a>How to trigger a function manually</span></span>
<span data-ttu-id="9e0fa-302">Bir işlev el ile tetiklemek için kullanabileceğiniz `Call` veya `CallAsync` yöntemi `JobHost` nesne ve `NoAutomaticTrigger` aşağıdaki örnekte gösterildiği gibi işlev, öznitelik.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-302">To trigger a function manually, use the `Call` or `CallAsync` method on the `JobHost` object and the `NoAutomaticTrigger` attribute on the function, as shown in the following example.</span></span>

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

## <span data-ttu-id="9e0fa-303"><a id="logs"></a>Günlükleri yazma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-303"><a id="logs"></a>How to write logs</span></span>
<span data-ttu-id="9e0fa-304">Pano günlükleri iki yerde gösterir: Web işi için sayfası ve sayfanın belli bir Web işi başlatma.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-304">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Web işi sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![İşlev çağırma sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="9e0fa-307">Konsol yöntemler, bir işlev çağrısı veya buna çıktısını `Main()` yöntemi görünür Web işi için Pano sayfası, sayfa belirli yöntem çağırma için içinde değil.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-307">Output from Console methods that you call in a function or in the `Main()` method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="9e0fa-308">Çıktı yöntemi imzanız bir parametresinden alma TextWriter nesneden bir yöntem çağırma için Pano sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-308">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="9e0fa-309">Konsol birçok iş işlevlerinin aynı anda çalışabilir tek iş parçacıklı, olduğu için konsol çıktısı bir belirli yöntem çağrısının bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-309">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="9e0fa-310">İşte bu nedenle SDK, her işlev çağrısını kendi benzersiz günlük yazıcı nesnesi ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-310">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="9e0fa-311">Yazılacak [uygulama izleme günlükleri](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), kullanın `Console.Out` (bilgisi olarak işaretlenmiş günlükleri oluşturur) ve `Console.Error` (hata olarak işaretlenmiş günlükleri oluşturur).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-311">To write [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="9e0fa-312">Alternatif kullanmaktır [izleme veya TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), uyarı, ayrıntı sağlar ve kritik bilgileri ve hata yanı sıra düzeyleri.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-312">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="9e0fa-313">Azure web uygulamanızı nasıl yapılandırdığınıza bağlı olarak Azure BLOB'veya uygulama izleme günlükleri web app günlük dosyalarında, Azure tabloları, görünür.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-313">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="9e0fa-314">Tüm konsol çıktısı doğru olduğundan, en son 100 uygulama günlüklerini sayfada değil bir işlev çağrısını için Web işi için Pano sayfası da görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-314">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="9e0fa-315">Programı yerel olarak çalışmıyorsa program bir Azure WebJob içinde yalnızca çalışıyorsa, Pano veya başka bir ortamında konsol çıktısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-315">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="9e0fa-316">Yüksek verimlilik senaryolar için panoyu günlüğü devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="9e0fa-317">Varsayılan olarak, SDK depolama birimine günlükler yazar ve birçok iletilerini işlerken bu etkinliği performansının düşmesine neden.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-317">By default, the SDK writes logs to storage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="9e0fa-318">Günlüğünü devre dışı bırakmak için aşağıdaki örnekte gösterildiği gibi null olarak Pano bağlantı dizesini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-318">To disable logging, set the dashboard connection string to null as shown in the following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="9e0fa-319">Aşağıdaki örnek günlüklerini yazma için çeşitli yollar gösterir:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-319">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="9e0fa-320">WebJobs SDK panosunda, çıkışı `TextWriter` nesne zaman, belirli bir sayfaya gitmek yukarı gösterir işlev çağırma ve tıklatın **geçiş çıktı**:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-320">In the WebJobs SDK Dashboard, the output from the `TextWriter` object shows up when you go to the page for a particular function invocation and click **Toggle Output**:</span></span>

![İşlev çağırma bağlantısına tıklayın](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![İşlev çağırma sayfasındaki günlükleri](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="9e0fa-323">Web işi (için işlev çağrısını) için sayfaya gidin ve'ı tıklattığınızda WebJobs SDK panosunda en son 100 satır konsolunun Göster yukarı çıktı **geçiş çıktı**.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-323">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and click **Toggle Output**.</span></span>

![Çıkışı Aç/Kapat'ı tıklatın](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="9e0fa-325">Bir sürekli Webjob'un uygulama günlüklerini/data/işleri/sürekli/içinde gösterilmesi*{webjobname}*web uygulama dosya sisteminde /job_log.txt.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="9e0fa-326">Bir Azure uygulama günlükleri görünümlü bu blob: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Merhaba Dünya!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Merhaba Dünya!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Merhaba Dünya!,</span><span class="sxs-lookup"><span data-stu-id="9e0fa-326">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="9e0fa-327">Ve bir Azure tablosu `Console.Out` ve `Console.Error` günlükleri şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="9e0fa-327">And in an Azure table the `Console.Out` and `Console.Error` logs look like this:</span></span>

![Tablo bilgi günlüğüne](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Hata günlüğü tablosundaki](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="9e0fa-330">Kendi Günlükçü takın istiyorsanız, bkz: [Bu örnek](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-330">If you want to plug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="9e0fa-331"><a id="errors"></a>Hataları işlemek ve zaman aşımları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9e0fa-331"><a id="errors"></a>How to handle errors and configure timeouts</span></span>
<span data-ttu-id="9e0fa-332">WebJobs SDK de içeren bir [zaman aşımı](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) iptal edilebilir için bir işlev neden kullandığınız öznitelik belirtilen sürede tamamlamak değil.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-332">The WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use to cause a function to be canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="9e0fa-333">Belirtilen bir süre içinde çok fazla hata gerçekleştiğinde bir uyarı yükseltmek istiyorsanız, kullanabileceğiniz `ErrorTrigger` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-333">And if you want to raise an alert when too many errors happen within a specified period of time, you can use the `ErrorTrigger` attribute.</span></span> <span data-ttu-id="9e0fa-334">Burada bir [ErrorTrigger örnek](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    To = "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors to the Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

<span data-ttu-id="9e0fa-335">Ayrıca dinamik olarak devre dışı bırakabilir ve bunlar, bir uygulama ayarı veya ortam değişkeni adı olabilir bir yapılandırma anahtarı kullanarak tetiklenebilir olup olmadığını denetlemek için işlevler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-335">You can also dynamically disable and enable functions to control whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="9e0fa-336">Örnek kod için bkz: `Disable` özniteliğini [WebJobs SDK deposu örnekleri](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-336">For sample code, see the `Disable` attribute in [the WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="9e0fa-337"><a id="nextsteps"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e0fa-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="9e0fa-338">Bu kılavuz, Azure kuyruklarla çalışmaya yönelik yaygın senaryolar nasıl ele alınacağını gösteren kod örnekleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="9e0fa-338">This guide has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="9e0fa-339">Azure Web işleri ve WebJobs SDK nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="9e0fa-339">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
