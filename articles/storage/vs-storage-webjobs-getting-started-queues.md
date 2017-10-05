---
title: "Kuyruk depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (Web işi projeleri) | Microsoft Docs"
description: "Visual Studio kullanarak bir depolama hesabı bağlandıktan sonra bir Web işi projesinin Azure kuyruk depolama ile çalışmaya başlamak nasıl Hizmetleri bağlı."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: abd4814c099620345e04833e14dafd38432064e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="cea69-103">Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (Web işi projeler)</span><span class="sxs-lookup"><span data-stu-id="cea69-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="cea69-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cea69-104">Overview</span></span>
<span data-ttu-id="cea69-105">Bu makalede nasıl oluşturduğunuz veya Visual Studio kullanarak Azure storage hesabı başvurulan sonra Visual Studio Azure WebJob projede Azure kuyruk depolama kullanma başlamak **bağlı Hizmetleri Ekle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="cea69-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="cea69-106">Eklediğinizde bir depolama hesabı bir Web işi projesi için Visual Studio kullanarak **bağlı Hizmetleri Ekle** iletişim kutusunda, uygun Azure depolama NuGet paketleri yüklü, uygun .NET başvuruları projeye eklenir ve depolama hesabı için bağlantı dizelerini App.config dosyasında güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cea69-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="cea69-107">Bu makalede Azure WebJobs SDK sürümü kullanmak nasıl gösteren C# kod örnekleri sağlar 1.x Azure kuyruk depolama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="cea69-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="cea69-108">Azure Kuyruk depolama, HTTP veya HTTPS kullanan kimlik doğrulaması yapılmış çağrılar aracılığıyla dünyanın her yerinden erişilebilen çok sayıda iletinin depolanması için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="cea69-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="cea69-109">Tek bir kuyruk iletisinin boyutu 64 KB’ye kadar olabilir ve bir kuyrukta, depolama hesabının toplam kapasite sınırına kadar milyonlarca ileti bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="cea69-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="cea69-110">Bkz: [.NET kullanarak Azure kuyruk depolama ile çalışmaya başlama](storage-dotnet-how-to-use-queues.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="cea69-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="cea69-111">ASP.NET hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="cea69-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="cea69-112">Bir kuyruk iletisi alındığında bir işlev tetikleme</span><span class="sxs-lookup"><span data-stu-id="cea69-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="cea69-113">Bir kuyruk iletisi alındığında WebJobs SDK çağıran bir işlev yazmak için **QueueTrigger** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="cea69-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="cea69-114">Öznitelik oluşturucunun yoklamak için sıra adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="cea69-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="cea69-115">Kuyruk adı dinamik olarak belirlemek nasıl görmek için kullanıma [yapılandırma seçeneklerinin nasıl ayarlanacağını](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="cea69-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="cea69-116">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="cea69-116">String queue messages</span></span>
<span data-ttu-id="cea69-117">Bir dize ileti sırası aşağıdaki örnekte, bu nedenle içerir **QueueTrigger** adlı bir dize parametresi uygulanan **logMessage** kuyruk iletisini içeriğini içerir.</span><span class="sxs-lookup"><span data-stu-id="cea69-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="cea69-118">İşlev [Pano için bir günlük iletisi Yazar](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="cea69-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="cea69-119">Yanında **dize**, parametresi bir bayt dizisi olabilir bir **CloudQueueMessage** nesne ya da tanımladığınız bir POCO.</span><span class="sxs-lookup"><span data-stu-id="cea69-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="cea69-120">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="cea69-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="cea69-121">Aşağıdaki örnekte, JSON için kuyruk iletisini içeren bir **BlobInformation** içeren nesne bir **BlobName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="cea69-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="cea69-122">SDK'yı otomatik olarak nesne seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="cea69-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="cea69-123">SDK'sı [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) seri hale getirmek ve seri durumdan iletileri.</span><span class="sxs-lookup"><span data-stu-id="cea69-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="cea69-124">WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bir POCO kuyruk iletisi oluşturmak için aşağıdaki örneğe benzer kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea69-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="cea69-125">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="cea69-125">Async functions</span></span>
<span data-ttu-id="cea69-126">Aşağıdaki zaman uyumsuz işlev [bir günlüğü panoya Yazar](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="cea69-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="cea69-127">Zaman uyumsuz işlevleri sürebilir bir [iptal belirteci](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)blob kopyalar aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="cea69-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="cea69-128">(Bir açıklaması için **queueTrigger** yer tutucu, bkz: [BLOB'lar](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) bölümüne.)</span><span class="sxs-lookup"><span data-stu-id="cea69-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="cea69-129">Türleri QueueTrigger öznitelik birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="cea69-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="cea69-130">Kullanabileceğiniz **QueueTrigger** şu türden:</span><span class="sxs-lookup"><span data-stu-id="cea69-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="cea69-131">**dize**</span><span class="sxs-lookup"><span data-stu-id="cea69-131">**string**</span></span>
* <span data-ttu-id="cea69-132">JSON olarak serileştirilen bir POCO türü</span><span class="sxs-lookup"><span data-stu-id="cea69-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="cea69-133">**byte]**</span><span class="sxs-lookup"><span data-stu-id="cea69-133">**byte[]**</span></span>
* <span data-ttu-id="cea69-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="cea69-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="cea69-135">Yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="cea69-135">Polling algorithm</span></span>
<span data-ttu-id="cea69-136">SDK boşta kuyruk depolama işlem maliyetleri yoklama etkisini azaltmak için bir rastgele üstel geri alma algoritması uygular.</span><span class="sxs-lookup"><span data-stu-id="cea69-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="cea69-137">Bir ileti bulunduğunda, SDK iki saniye bekler ve ardından başka bir ileti için denetler; bir ileti bulunduğunda yeniden denemeden önce yaklaşık dört saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="cea69-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="cea69-138">Bir kuyruk iletisi almak için sonraki başarısız girişimden sonra bekleme süresini bir dakika olarak varsayılan olarak en fazla bekleme süresi ulaşana kadar artmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="cea69-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="cea69-139">[En fazla bekleme süresi yapılandırılabilir](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="cea69-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="cea69-140">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="cea69-140">Multiple instances</span></span>
<span data-ttu-id="cea69-141">Web uygulamanız birden çok örneği üzerinde çalışıyorsa, sürekli Webjob'lar her makinede çalışır ve her makine için Tetikleyicileri bekleyin ve işlevleri çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="cea69-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="cea69-142">Bu aynı verileri iki kez işlemeyi bazı işlevler neden bazı senaryolarda, böylece işlevleri (böylece bunları sürekli olarak aynı girdi verileriyle çağırma yinelenen sonuçları oluşturmuyor yazılmış) ıdempotent gerekir.</span><span class="sxs-lookup"><span data-stu-id="cea69-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="cea69-143">Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="cea69-143">Parallel execution</span></span>
<span data-ttu-id="cea69-144">Birden çok işlevler farklı sıralarda dinleme varsa, iletileri aynı anda alındığında SDK bunları paralel olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="cea69-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="cea69-145">Tek bir kuyruk için birden fazla ileti alındığında aynı durum geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cea69-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="cea69-146">Varsayılan olarak, SDK 16 iletileri kuyruğa toplu bir zaman alır ve paralel olarak işler işlevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="cea69-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="cea69-147">[Toplu iş boyutu yapılandırılabilir](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="cea69-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="cea69-148">İşlenmekte olan numarası yarısı toplu iş boyutu aldığında, SDK başka bir toplu iş alır ve bu iletileri işleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="cea69-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="cea69-149">Bu nedenle en fazla eş zamanlı ileti işlevi işlenen sayısı bir ve yarı kez bir toplu iş boyutu dur.</span><span class="sxs-lookup"><span data-stu-id="cea69-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="cea69-150">Bu sınırı olan her işlev ayrı olarak geçerli bir **QueueTrigger** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="cea69-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="cea69-151">Paralel yürütme üzerinde bir Sıraya alınan iletileri istemiyorsanız, yığın boyutu 1 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cea69-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="cea69-152">Sıra veya sıra ileti meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="cea69-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="cea69-153">Aşağıdaki ileti özellikleri yöntemi imza parametreleri ekleyerek alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cea69-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="cea69-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="cea69-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="cea69-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="cea69-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="cea69-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="cea69-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="cea69-157">**dize** queueTrigger (ileti metni içerir)</span><span class="sxs-lookup"><span data-stu-id="cea69-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="cea69-158">**dize** kimliği</span><span class="sxs-lookup"><span data-stu-id="cea69-158">**string** id</span></span>
* <span data-ttu-id="cea69-159">**dize** popReceipt</span><span class="sxs-lookup"><span data-stu-id="cea69-159">**string** popReceipt</span></span>
* <span data-ttu-id="cea69-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="cea69-160">**int** dequeueCount</span></span>

<span data-ttu-id="cea69-161">Azure depolama alanıyla doğrudan API çalışmak isterseniz, ayrıca ekleyebileceğiniz bir **CloudStorageAccount** parametresi.</span><span class="sxs-lookup"><span data-stu-id="cea69-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="cea69-162">Aşağıdaki örnekte tüm bu meta veri bilgileri uygulama günlüğüne yazar.</span><span class="sxs-lookup"><span data-stu-id="cea69-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="cea69-163">Örnekte, kuyruk iletisini içeriğini logMessage ve queueTrigger içerir.</span><span class="sxs-lookup"><span data-stu-id="cea69-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="cea69-164">Örnek kodu ile yazılmış bir örnek günlük şöyledir:</span><span class="sxs-lookup"><span data-stu-id="cea69-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="cea69-165">Kapama</span><span class="sxs-lookup"><span data-stu-id="cea69-165">Graceful shutdown</span></span>
<span data-ttu-id="cea69-166">Sürekli bir WebJob içinde çalışan bir işlevinin kabul edebileceği bir **CancellationToken** işlevi hakkında sonlandırılacak WebJob olduğunu bildirmek işletim sistemi sağlayan parametre.</span><span class="sxs-lookup"><span data-stu-id="cea69-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="cea69-167">Bu bildirim, beklenmedik bir şekilde veri tutarsız bir durumda bırakır şekilde sonlandırma işlevi değil emin olmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea69-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="cea69-168">Aşağıdaki örnek, bir işlev yaklaşan WebJob sonlandırma denetlemek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="cea69-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="cea69-169">**Not:** durumunu ve çıkışını kapatılmışsa işlevlerin Pano doğru gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="cea69-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="cea69-170">Daha fazla bilgi için bkz: [Web işleri normal şekilde kapatılmasını](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="cea69-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="cea69-171">Bir kuyruk iletisi işlenirken bir kuyruk iletisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cea69-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="cea69-172">Yeni bir kuyruk iletisi oluşturan bir işlev yazmak için **sıra** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="cea69-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="cea69-173">Gibi **QueueTrigger**, kuyruk adı bir dize olarak geçirin veya yapabilecekleriniz [sıra adı dinamik olarak ayarlamak](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="cea69-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="cea69-174">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="cea69-174">String queue messages</span></span>
<span data-ttu-id="cea69-175">Aşağıdaki zaman uyumsuz olmayan kod örneği sıranın "inputqueue" adlı sıraya alınan kuyruk iletisini aynı içerikle "outputqueue" adlı yeni bir kuyruk iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cea69-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="cea69-176">(İşlevler için async kullanma **IAsyncCollector<T>**  daha sonra bu bölümde gösterilen.)</span><span class="sxs-lookup"><span data-stu-id="cea69-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="cea69-177">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="cea69-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="cea69-178">Bir dize yerine bir POCO içeren bir kuyruk iletisi oluşturmak için bir çıktı parametresi olarak POCO türü geçirmek **sıra** özniteliği Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="cea69-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="cea69-179">SDK'yı otomatik olarak JSON nesneyi serileştirir.</span><span class="sxs-lookup"><span data-stu-id="cea69-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="cea69-180">Nesne boş olsa bile bir kuyruk iletisi her zaman oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cea69-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="cea69-181">Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="cea69-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="cea69-182">Birden çok iletileri oluşturmak için çıkış sırası için parametre türü olun **ICollector<T>**  veya **IAsyncCollector<T>**, aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="cea69-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="cea69-183">Her kuyruk iletisi hemen oluşturulan zaman **Ekle** yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="cea69-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="cea69-184">Sıra özniteliği çalışır türleri</span><span class="sxs-lookup"><span data-stu-id="cea69-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="cea69-185">Kullanabileceğiniz **sıra** özniteliği aşağıdaki parametre türleri:</span><span class="sxs-lookup"><span data-stu-id="cea69-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="cea69-186">**dize çıkışı** (parametre değeri null olmayan ise işlevi sona erdiğinde kuyruk iletisi oluşturur)</span><span class="sxs-lookup"><span data-stu-id="cea69-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="cea69-187">**byte [] çıkışı** (gibi çalışır **dize**)</span><span class="sxs-lookup"><span data-stu-id="cea69-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="cea69-188">**CloudQueueMessage çıkışı** (gibi çalışır **dize**)</span><span class="sxs-lookup"><span data-stu-id="cea69-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="cea69-189">**POCO çıkışı** (serializable bir tür oluşturduğu bir ileti null bir nesne ile işlevi sona erdiğinde parametre null ise)</span><span class="sxs-lookup"><span data-stu-id="cea69-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="cea69-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="cea69-190">**ICollector**</span></span>
* <span data-ttu-id="cea69-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="cea69-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="cea69-192">**CloudQueue** (için el ile Azure Storage API'sini kullanarak doğrudan iletileri oluşturma)</span><span class="sxs-lookup"><span data-stu-id="cea69-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="cea69-193">Web işleri SDK'si öznitelikleri bir işlev gövdesine kullanın</span><span class="sxs-lookup"><span data-stu-id="cea69-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="cea69-194">Web işleri SDK'si öznitelik gibi kullanmadan önce işlevinizi bazı iş yapmanız gerekirse **sıra**, **Blob**, veya **tablo**, kullanabilirsiniz **IBinder** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="cea69-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="cea69-195">Aşağıdaki örnek, bir giriş sırası iletisi alır ve bir çıkış sırası aynı içeriği ile yeni bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cea69-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="cea69-196">Çıkış sırası adı işlevinin gövdesini kodda tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="cea69-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="cea69-197">**IBinder** arabirimi de kullanılabilir olan **tablo** ve **Blob** öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="cea69-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="cea69-198">Nasıl okunacağını ve yazma BLOB'ları ve bir sıraya ileti işlenirken tabloları</span><span class="sxs-lookup"><span data-stu-id="cea69-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="cea69-199">**Blob** ve **tablo** öznitelikleri BLOB'ları ve tabloları okuma ve yazma olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="cea69-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="cea69-200">Bu bölümdeki örnekler BLOB'lar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="cea69-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="cea69-201">BLOB'ları oluşturulduğunda veya güncelleştirilmiş işlemleri tetiklemek nasıl gösteren kod örnekleri için bkz: [WebJobs SDK ile Azure blob storage kullanma](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)ve okuma ve yazma tabloları kod örnekleri için bkz: [WebJobs SDK ile Azure table storage kullanma](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="cea69-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="cea69-202">Dize iletileri kuyruğa blobu işlemleri tetikleme</span><span class="sxs-lookup"><span data-stu-id="cea69-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="cea69-203">Bir dizeyi içeren bir kuyruk iletisi için **queueTrigger** olarak kullanabileceğiniz bir yer tutucudur **Blob** özniteliğin **blobPath** iletinin içeriğini içeren bir parametre.</span><span class="sxs-lookup"><span data-stu-id="cea69-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="cea69-204">Aşağıdaki örnek kullanır **akış** nesneleri okumak ve BLOB'ları yazmak için.</span><span class="sxs-lookup"><span data-stu-id="cea69-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="cea69-205">Kuyruk iletisini textblobs kapsayıcıda bulunan bir blob adıdır.</span><span class="sxs-lookup"><span data-stu-id="cea69-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="cea69-206">Blob ile birlikte bir kopyasını "-Yeni" eklenecek ad aynı kapsayıcıda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cea69-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="cea69-207">**Blob** özniteliği Oluşturucusu alır bir **blobPath** kapsayıcı ve blob adını belirten parametre.</span><span class="sxs-lookup"><span data-stu-id="cea69-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="cea69-208">Bu yer tutucu hakkında daha fazla bilgi için bkz: [WebJobs SDK ile Azure blob storage kullanma](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="cea69-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="cea69-209">Ne zaman öznitelik süsler bir **akış** nesnesi, başka bir oluşturucu parametresini belirtir **FileAccess** modu okuma, yazma veya okuma/yazma olarak.</span><span class="sxs-lookup"><span data-stu-id="cea69-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="cea69-210">Aşağıdaki örnek kullanan bir **CloudBlockBlob** bir blobu silmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="cea69-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="cea69-211">Kuyruk iletisini blob adıdır.</span><span class="sxs-lookup"><span data-stu-id="cea69-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="cea69-212">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="cea69-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="cea69-213">Kuyruk iletisini JSON olarak depolanan bir POCO için nesnenin özelliklerini adı yer tutucuları kullanabilirsiniz **sıra** özniteliğin **blobPath** parametresi.</span><span class="sxs-lookup"><span data-stu-id="cea69-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="cea69-214">Bu gibi durumlarda, sıra meta veri özellik adları da yer tutucu olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea69-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="cea69-215">Bkz: [sıra veya sıra ileti meta verileri alma](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="cea69-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="cea69-216">Aşağıdaki örnek yeni bir blob farklı bir uzantıya sahip bir blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="cea69-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="cea69-217">Kuyruk iletisi bir **BlobInformation** içeren nesnesinin **BlobName** ve **BlobNameWithoutExtension** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="cea69-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="cea69-218">Blob yolu için yer tutucu olarak kullanılan özellik adları **Blob** öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="cea69-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="cea69-219">SDK'sı [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) seri hale getirmek ve seri durumdan iletileri.</span><span class="sxs-lookup"><span data-stu-id="cea69-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="cea69-220">WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bir POCO kuyruk iletisi oluşturmak için aşağıdaki örneğe benzer kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea69-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="cea69-221">Bir blob için bir nesne bağlama önce işlevinizi bazı iş gerçekleştirmeniz gerekiyorsa, gösterildiği gibi işlevinin gövdesini özniteliğinde kullanabilirsiniz [kullanmak Web işleri SDK'si öznitelikleri bir işlev gövdesine](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="cea69-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="cea69-222">Blob özniteliğiyle kullanabileceğiniz türü</span><span class="sxs-lookup"><span data-stu-id="cea69-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="cea69-223">**Blob** özniteliği şu türleriyle kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="cea69-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="cea69-224">**Akış** (okuma veya yazma, FileAccess Oluşturucu parametresi kullanılarak belirtilen)</span><span class="sxs-lookup"><span data-stu-id="cea69-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="cea69-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="cea69-225">**TextReader**</span></span>
* <span data-ttu-id="cea69-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="cea69-226">**TextWriter**</span></span>
* <span data-ttu-id="cea69-227">**dize** (okuma)</span><span class="sxs-lookup"><span data-stu-id="cea69-227">**string** (read)</span></span>
* <span data-ttu-id="cea69-228">**dize çıkışı** (yazma; işlevi döndüğünde yalnızca dize parametresi null olmayan ise bir blob oluşturur)</span><span class="sxs-lookup"><span data-stu-id="cea69-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="cea69-229">POCO (okuma)</span><span class="sxs-lookup"><span data-stu-id="cea69-229">POCO (read)</span></span>
* <span data-ttu-id="cea69-230">POCO out (yazma; her zaman bir blob oluşturur, işlevi döndüğünde POCO parametre null ise null nesnesi olarak oluşturur)</span><span class="sxs-lookup"><span data-stu-id="cea69-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="cea69-231">**CloudBlobStream** (yazma)</span><span class="sxs-lookup"><span data-stu-id="cea69-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="cea69-232">**ICloudBlob** (okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="cea69-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="cea69-233">**CloudBlockBlob** (okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="cea69-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="cea69-234">**CloudPageBlob** (okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="cea69-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="cea69-235">Zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="cea69-235">How to handle poison messages</span></span>
<span data-ttu-id="cea69-236">İçerikleri bir işlev başarısız olmasına neden olan iletileri çağrılır *zehirli ileti*.</span><span class="sxs-lookup"><span data-stu-id="cea69-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="cea69-237">İşlev başarısız olduğunda, kuyruk iletisini silinmez ve sonunda tekrar tekrar için döngü neden kayıt.</span><span class="sxs-lookup"><span data-stu-id="cea69-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="cea69-238">SDK'yı otomatik olarak sınırlı sayıda yineleme sonra döngüsü engelleyebilecek veya el ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea69-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="cea69-239">Otomatik zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="cea69-239">Automatic poison message handling</span></span>
<span data-ttu-id="cea69-240">SDK bir kuyruk iletisi işleyemedi 5 kata işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="cea69-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="cea69-241">Beşinci deneme başarısız olursa, ileti zararlı kuyruğuna taşınır.</span><span class="sxs-lookup"><span data-stu-id="cea69-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="cea69-242">İçinde yeniden deneme sayısı üst sınırını yapılandırmak nasıl görebilirsiniz [yapılandırma seçeneklerinin nasıl ayarlanacağını](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="cea69-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="cea69-243">Adlı zararlı sırası *{originalqueuename}*-zararlı.</span><span class="sxs-lookup"><span data-stu-id="cea69-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="cea69-244">Günlüğe yazma veya el ile ilgili dikkat bir bildirim göndererek zararlı sırasından iletilerini işlemek için bir işlev gerekli yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea69-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="cea69-245">Aşağıdaki örnekte **CopyBlob** bir kuyruk iletisi mevcut olmayan bir blob adını içerdiğinde işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cea69-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="cea69-246">Bu durum oluştuğunda ileti copyblobqueue poison kuyruğuna copyblobqueue sıradan taşınır.</span><span class="sxs-lookup"><span data-stu-id="cea69-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="cea69-247">**ProcessPoisonMessage** zehir iletisi günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="cea69-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

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

<span data-ttu-id="cea69-248">Zararlı bir ileti işlenirken bu işlevler konsol çıktısı aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cea69-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Zehirli ileti işleme için konsol çıkışı](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="cea69-250">El ile zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="cea69-250">Manual poison message handling</span></span>
<span data-ttu-id="cea69-251">Ekleyerek sayısı bir ileti toplanma işleme alabilirsiniz bir **int** adlı parametre **dequeueCount** , işlevi.</span><span class="sxs-lookup"><span data-stu-id="cea69-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="cea69-252">Ardından, işlev kodu dequeue sayıma denetleyin ve sayısı bir eşiği aştığında kendi zehir iletisi aşağıdaki örnekte gösterildiği gibi işleme gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cea69-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

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

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="cea69-253">Yapılandırma seçeneklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="cea69-253">How to set configuration options</span></span>
<span data-ttu-id="cea69-254">Kullanabileceğiniz **JobHostConfiguration** türü aşağıdaki yapılandırma seçeneklerini ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="cea69-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="cea69-255">Kod içinde SDK bağlantı dizelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cea69-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="cea69-256">Yapılandırma **QueueTrigger** maksimum gibi ayarları dequeue sayısı.</span><span class="sxs-lookup"><span data-stu-id="cea69-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="cea69-257">Sıra adları yapılandırmasından alın.</span><span class="sxs-lookup"><span data-stu-id="cea69-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="cea69-258">Kod içinde SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="cea69-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="cea69-259">Kodda SDK bağlantı dizelerini ayarlama, kendi bağlantı dizesi adlarında yapılandırma dosyalarının veya ortam değişkenlerini kullanmak aşağıdaki örnekte gösterildiği gibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cea69-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="cea69-260">QueueTrigger ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cea69-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="cea69-261">Sıra ileti işleme için uygulama aşağıdaki ayarları yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cea69-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="cea69-262">En fazla eşzamanlı olarak paralel olarak yürütülecek toplanmış sıra ileti sayısı (varsayılan olarak 16).</span><span class="sxs-lookup"><span data-stu-id="cea69-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="cea69-263">Bir kuyruk iletisi zararlı bir sıraya gönderilmeden önce yeniden deneme sayısı (varsayılan olarak 5).</span><span class="sxs-lookup"><span data-stu-id="cea69-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="cea69-264">En fazla bekleme süresi bir sıra boş olduğunda yeniden yoklama önce (varsayılan değer 1 dakika).</span><span class="sxs-lookup"><span data-stu-id="cea69-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="cea69-265">Aşağıdaki örnek, bu ayarların nasıl yapılandırılacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="cea69-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="cea69-266">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="cea69-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="cea69-267">Kuyruk adı, bir blob adı veya kapsayıcı belirtmek istediğiniz bazen veya bir tablo adı kod sabit kodlu yerine onu.</span><span class="sxs-lookup"><span data-stu-id="cea69-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="cea69-268">Örneğin, kuyruk adı belirtmek isteyebilirsiniz **QueueTrigger** bir yapılandırma dosyası veya ortam değişkeninde.</span><span class="sxs-lookup"><span data-stu-id="cea69-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="cea69-269">Bunu geçirerek yapabilirsiniz bir **NameResolver** nesnesini **JobHostConfiguration** türü.</span><span class="sxs-lookup"><span data-stu-id="cea69-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="cea69-270">Web işleri SDK'si özniteliği Oluşturucusu parametrelerinde yüzde (%) işareti tarafından çevrelenen özel yer tutucular içerir ve **NameResolver** kod bu yer tutucular yerine kullanılacak gerçek değerler belirtir.</span><span class="sxs-lookup"><span data-stu-id="cea69-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="cea69-271">Örneğin, test ortamında logqueuetest ve üretimde bir adlandırılmış logqueueprod adlı bir sıra kullanmak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="cea69-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="cea69-272">Bir giriş adını belirtmek istediğiniz sabit kodlanmış kuyruk adı yerine **appSettings** gerçek sıra adı olurdu koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="cea69-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="cea69-273">Varsa **appSettings** anahtar logqueue, işlevinizi aşağıdaki gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="cea69-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="cea69-274">**NameResolver** sınıfını sıra adından sonra almak **appSettings** aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="cea69-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="cea69-275">Geçirdiğiniz **NameResolver** için sınıfını **JobHost** nesne aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="cea69-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="cea69-276">**Not:** kuyruk, tablo ve blob adları çözümlenmiş her zaman bir işlev çağrılır, ancak blob kapsayıcı adları yalnızca uygulama başladığında çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="cea69-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="cea69-277">İş çalışırken blob kapsayıcı adı değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="cea69-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="cea69-278">Bir işlev el ile tetikleme</span><span class="sxs-lookup"><span data-stu-id="cea69-278">How to trigger a function manually</span></span>
<span data-ttu-id="cea69-279">Bir işlev el ile tetiklemek için kullanabileceğiniz **çağrısı** veya **CallAsync** yöntemi **JobHost** nesne ve **NoAutomaticTrigger** aşağıdaki örnekte gösterildiği gibi işlev, öznitelik.</span><span class="sxs-lookup"><span data-stu-id="cea69-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

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

## <a name="how-to-write-logs"></a><span data-ttu-id="cea69-280">Günlükleri yazma</span><span class="sxs-lookup"><span data-stu-id="cea69-280">How to write logs</span></span>
<span data-ttu-id="cea69-281">Pano günlükleri iki yerde gösterir: Web işi için sayfası ve sayfanın belli bir Web işi başlatma.</span><span class="sxs-lookup"><span data-stu-id="cea69-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Web işi sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![İşlev çağırma sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="cea69-284">Konsol yöntemler, bir işlev çağrısı veya buna çıktısını **Main()** yöntemi görünür Web işi için Pano sayfası, sayfa belirli yöntem çağırma için içinde değil.</span><span class="sxs-lookup"><span data-stu-id="cea69-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="cea69-285">Çıktı yöntemi imzanız bir parametresinden alma TextWriter nesneden bir yöntem çağırma için Pano sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cea69-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="cea69-286">Konsol birçok iş işlevlerinin aynı anda çalışabilir tek iş parçacıklı, olduğu için konsol çıktısı bir belirli yöntem çağrısının bağlanamaz.</span><span class="sxs-lookup"><span data-stu-id="cea69-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="cea69-287">İşte bu nedenle SDK, her işlev çağrısını kendi benzersiz günlük yazıcı nesnesi ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="cea69-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="cea69-288">Yazılacak [uygulama izleme günlükleri](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), kullanın **Console.Out** (bilgisi olarak işaretlenmiş günlükleri oluşturur) ve **Console.Error** (hata olarak işaretlenmiş günlükleri oluşturur).</span><span class="sxs-lookup"><span data-stu-id="cea69-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="cea69-289">Alternatif kullanmaktır [izleme veya TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), uyarı, ayrıntı sağlar ve kritik bilgileri ve hata yanı sıra düzeyleri.</span><span class="sxs-lookup"><span data-stu-id="cea69-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="cea69-290">Azure web uygulamanızı nasıl yapılandırdığınıza bağlı olarak Azure BLOB'veya uygulama izleme günlükleri web app günlük dosyalarında, Azure tabloları, görünür.</span><span class="sxs-lookup"><span data-stu-id="cea69-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="cea69-291">Tüm konsol çıktısı doğru olduğundan, en son 100 uygulama günlüklerini sayfada değil bir işlev çağrısını için Web işi için Pano sayfası da görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cea69-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="cea69-292">Programı yerel olarak çalışmıyorsa program bir Azure WebJob içinde yalnızca çalışıyorsa, Pano veya başka bir ortamında konsol çıktısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cea69-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="cea69-293">Günlüğe kaydetme, Pano bağlantı dizesi null değerine ayarlayarak devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cea69-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="cea69-294">Daha fazla bilgi için bkz: [yapılandırma seçeneklerinin nasıl ayarlanacağını](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="cea69-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="cea69-295">Aşağıdaki örnek günlüklerini yazma için çeşitli yollar gösterir:</span><span class="sxs-lookup"><span data-stu-id="cea69-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="cea69-296">WebJobs SDK panosunda, çıkışı **TextWriter** zaman, belirli bir sayfaya gitmek yukarı gösterir işlev çağırma ve seçin nesnesi **geçiş çıktı**:</span><span class="sxs-lookup"><span data-stu-id="cea69-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Çağırma bağlantı](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![İşlev çağırma sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="cea69-299">Web işi (için işlev çağrısını) için sayfaya gidin ve seçin WebJobs SDK panosunda en son 100 satır konsolunun Göster yukarı çıktı **geçiş çıktı**.</span><span class="sxs-lookup"><span data-stu-id="cea69-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Çıkışı Aç/Kapat](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="cea69-301">Bir sürekli Webjob'un uygulama günlüklerini/data/işleri/sürekli/içinde gösterilmesi*{webjobname}*web uygulama dosya sisteminde /job_log.txt.</span><span class="sxs-lookup"><span data-stu-id="cea69-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="cea69-302">Bir Azure uygulama günlükleri görünümlü bu blob: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Merhaba Dünya!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Merhaba Dünya!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Merhaba Dünya!,</span><span class="sxs-lookup"><span data-stu-id="cea69-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="cea69-303">Ve bir Azure tablosu **Console.Out** ve **Console.Error** günlükleri şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="cea69-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Tablo bilgi günlüğüne](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Hata günlüğü tablosundaki](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="cea69-306">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cea69-306">Next steps</span></span>
<span data-ttu-id="cea69-307">Bu makalede Azure kuyruklarla çalışmaya yönelik yaygın senaryolar nasıl ele alınacağını gösteren kod örnekleri sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="cea69-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="cea69-308">Azure Web işleri ve WebJobs SDK nasıl kullanılacağı hakkında daha fazla bilgi için bkz: [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="cea69-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

