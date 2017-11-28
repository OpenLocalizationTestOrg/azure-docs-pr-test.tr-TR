---
title: "aaaGetting, bağlı hizmetler (Web işi projeleri) kuyruk depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra bir Web işi projesinin Azure kuyruk depolama kullanarak nasıl tooget başlatıldı."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 47a446aa5c6bbf25526339823db4952ac1a8802f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="46c75-103">Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (Web işi projeler)</span><span class="sxs-lookup"><span data-stu-id="46c75-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="46c75-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="46c75-104">Overview</span></span>
<span data-ttu-id="46c75-105">Bu makalede nereden Azure kuyruk kullanmaya oluşturduğunuz veya Azure storage hesabı kullanarak başvurulan sonra Visual Studio Azure WebJob projesinde depolama hello Visual Studio **bağlı Hizmetleri Ekle** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="46c75-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="46c75-106">Merhaba Visual Studio kullanarak bir depolama hesabı tooa Web işi projesinin eklediğinizde **bağlı Hizmetleri Ekle** iletişim kutusunda, hello uygun Azure depolama NuGet paketleri yüklenir, hello uygun .NET başvuruları eklenen toohello Proje ve hello depolama hesabı için bağlantı dizelerini hello App.config dosyasında güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="46c75-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="46c75-107">Bu makalede nasıl toouse hello Azure WebJobs SDK sürüm gösteren C# kod örnekleri sağlar 1.x hello Azure kuyruk depolama hizmeti ile.</span><span class="sxs-lookup"><span data-stu-id="46c75-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="46c75-108">Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="46c75-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="46c75-109">Tek bir kuyruk iletisinin boyutu too64 KB yukarı olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.</span><span class="sxs-lookup"><span data-stu-id="46c75-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="46c75-110">Bkz: [.NET kullanarak Azure kuyruk depolama ile çalışmaya başlama](../storage/queues/storage-dotnet-how-to-use-queues.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="46c75-110">See [Get started with Azure Queue Storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="46c75-111">ASP.NET hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="46c75-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="46c75-112">Nasıl tootrigger bir kuyruk iletisi alındığında işlevi</span><span class="sxs-lookup"><span data-stu-id="46c75-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="46c75-113">toowrite Web işleri SDK'si hello işlevi çağıran bir kuyruk iletisi alındığında, hello kullan **QueueTrigger** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="46c75-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="46c75-114">Hello özniteliği Oluşturucusu hello sıra toopoll hello adını belirten bir dize parametresi alan.</span><span class="sxs-lookup"><span data-stu-id="46c75-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="46c75-115">toosee tooset hello nasıl sıra adı dinamik olarak kullanıma [nasıl tooset yapılandırma seçenekleri](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="46c75-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="46c75-116">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="46c75-116">String queue messages</span></span>
<span data-ttu-id="46c75-117">Bir dize ileti hello sıra aşağıdaki örneğine hello, bu nedenle içeren **QueueTrigger** adlı uygulanan tooa dize parametresi **logMessage** hello kuyruk iletisi Merhaba içeriğine içerir.</span><span class="sxs-lookup"><span data-stu-id="46c75-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="46c75-118">Merhaba işlevi [bir günlük iletisi toohello Pano Yazar](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="46c75-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="46c75-119">Yanında **dize**, hello parametresi bir bayt dizisi olabilir bir **CloudQueueMessage** nesne ya da tanımladığınız bir POCO.</span><span class="sxs-lookup"><span data-stu-id="46c75-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="46c75-120">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="46c75-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="46c75-121">Aşağıdaki örneğine hello, JSON hello kuyruk iletisi içeren bir **BlobInformation** içeren nesne bir **BlobName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="46c75-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="46c75-122">Merhaba SDK otomatik olarak hello nesne seri durumdan çıkarır.</span><span class="sxs-lookup"><span data-stu-id="46c75-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="46c75-123">Merhaba SDK kullanan hello [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize ve iletileri seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="46c75-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="46c75-124">Merhaba WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bu hello hello örnek toocreate bir POCO kuyruk iletisi aşağıdaki gibi kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="46c75-125">Zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="46c75-125">Async functions</span></span>
<span data-ttu-id="46c75-126">Async işlevi aşağıdaki hello [günlük toohello Pano Yazar](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="46c75-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="46c75-127">Zaman uyumsuz işlevleri sürebilir bir [iptal belirteci](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken)hello blob kopyaladığı örnek aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="46c75-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="46c75-128">(Merhaba açıklaması için **queueTrigger** yer tutucu hello bkz [BLOB'lar](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) bölüm.)</span><span class="sxs-lookup"><span data-stu-id="46c75-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="46c75-129">Türleri hello QueueTrigger özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="46c75-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="46c75-130">Kullanabileceğiniz **QueueTrigger** şu türlerini hello ile:</span><span class="sxs-lookup"><span data-stu-id="46c75-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="46c75-131">**dize**</span><span class="sxs-lookup"><span data-stu-id="46c75-131">**string**</span></span>
* <span data-ttu-id="46c75-132">JSON olarak serileştirilen bir POCO türü</span><span class="sxs-lookup"><span data-stu-id="46c75-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="46c75-133">**byte]**</span><span class="sxs-lookup"><span data-stu-id="46c75-133">**byte[]**</span></span>
* <span data-ttu-id="46c75-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="46c75-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="46c75-135">Yoklama algoritması</span><span class="sxs-lookup"><span data-stu-id="46c75-135">Polling algorithm</span></span>
<span data-ttu-id="46c75-136">Merhaba SDK boşta kuyruk depolama işlem maliyetleri yoklama rasgele üstel geri alma algoritması tooreduce hello etkisini uygular.</span><span class="sxs-lookup"><span data-stu-id="46c75-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="46c75-137">Bir ileti bulunduğunda, hello SDK iki saniye bekler ve ardından başka bir ileti için denetler; bir ileti bulunduğunda yeniden denemeden önce yaklaşık dört saniye bekler.</span><span class="sxs-lookup"><span data-stu-id="46c75-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="46c75-138">Merhaba maksimum bekleme süresi, ulaşana kadar sonraki başarısız denemeler tooget bir kuyruk iletisi sonra hello bekleme süresi tooincrease devam eder. hangi Varsayılanları tooone minute.</span><span class="sxs-lookup"><span data-stu-id="46c75-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="46c75-139">[Merhaba maksimum bekleme süresi yapılandırılabilir](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="46c75-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="46c75-140">Birden çok örneği</span><span class="sxs-lookup"><span data-stu-id="46c75-140">Multiple instances</span></span>
<span data-ttu-id="46c75-141">Web uygulamanız birden çok örneklerinde çalıştırıyorsa, her makineye sürekli Webjob'lar çalışır ve her makine için Tetikleyicileri bekleyin ve toorun işlevlerini deneyin.</span><span class="sxs-lookup"><span data-stu-id="46c75-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="46c75-142">Bu yol açabilir bazı senaryolarda işleme toosome işlevleri aynı veri nedenle işlevleri (bunları sürekli olarak aynı giriş verisi oluşturmuyor hello ile arama sonuçları çoğaltmak için yazılmış) ıdempotent olmalıdır, iki kez hello.</span><span class="sxs-lookup"><span data-stu-id="46c75-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="46c75-143">Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="46c75-143">Parallel execution</span></span>
<span data-ttu-id="46c75-144">Birden çok işlevler farklı sıralarda dinleme varsa, iletileri aynı anda alındığında hello SDK bunları paralel olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="46c75-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="46c75-145">tek bir kuyruk için birden fazla ileti alındığında hello aynı durum geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="46c75-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="46c75-146">Varsayılan olarak, hello SDK 16 iletileri kuyruğa toplu bir zaman alır ve paralel olarak işler hello işlevi yürütür.</span><span class="sxs-lookup"><span data-stu-id="46c75-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="46c75-147">[Merhaba toplu iş boyutu Dur yapılandırılabilir](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="46c75-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="46c75-148">İşlenmekte olan hello numarası hello toplu iş boyutu toohalf aldığında hello SDK başka bir toplu iş alır ve bu iletileri işleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="46c75-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="46c75-149">Bu nedenle hello en fazla eş zamanlı ileti işlevi işlenen sayısı bir ve yarı kez bir hello toplu iş boyutu dur.</span><span class="sxs-lookup"><span data-stu-id="46c75-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="46c75-150">Bu sınır olan tooeach işlev ayrı ayrı uygular bir **QueueTrigger** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="46c75-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="46c75-151">Paralel yürütme üzerinde bir Sıraya alınan iletileri istemiyorsanız hello toplu iş boyutu too1 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="46c75-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="46c75-152">Sıra veya sıra ileti meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="46c75-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="46c75-153">Aşağıdaki ileti özelliklere parametreleri toohello yöntemi imza ekleyerek hello alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46c75-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="46c75-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="46c75-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="46c75-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="46c75-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="46c75-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="46c75-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="46c75-157">**dize** queueTrigger (ileti metni içerir)</span><span class="sxs-lookup"><span data-stu-id="46c75-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="46c75-158">**dize** kimliği</span><span class="sxs-lookup"><span data-stu-id="46c75-158">**string** id</span></span>
* <span data-ttu-id="46c75-159">**dize** popReceipt</span><span class="sxs-lookup"><span data-stu-id="46c75-159">**string** popReceipt</span></span>
* <span data-ttu-id="46c75-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="46c75-160">**int** dequeueCount</span></span>

<span data-ttu-id="46c75-161">Hello Azure storage API'si ile doğrudan toowork isterseniz, ayrıca ekleyebileceğiniz bir **CloudStorageAccount** parametresi.</span><span class="sxs-lookup"><span data-stu-id="46c75-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="46c75-162">Merhaba aşağıdaki örnekte tüm bu meta verileri tooan bilgisi uygulama günlüğüne yazar.</span><span class="sxs-lookup"><span data-stu-id="46c75-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="46c75-163">Merhaba örnekte hello kuyruk iletisi Merhaba içeriğine logMessage ve queueTrigger içerir.</span><span class="sxs-lookup"><span data-stu-id="46c75-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="46c75-164">Merhaba örnek kodu ile yazılmış bir örnek günlük şöyledir:</span><span class="sxs-lookup"><span data-stu-id="46c75-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="46c75-165">Kapama</span><span class="sxs-lookup"><span data-stu-id="46c75-165">Graceful shutdown</span></span>
<span data-ttu-id="46c75-166">Sürekli bir WebJob içinde çalışan bir işlevinin kabul edebileceği bir **CancellationToken** hello işletim sistemi toonotify hello işlevi hello zaman sağlayan Web işi parametredir hakkında toobe sonlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="46c75-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="46c75-167">Bu bildirim toomake hello beklenmedik bir şekilde veri tutarsız bir durumda bırakır şekilde sonlandırma işlevi değil emin kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="46c75-168">örnekte gösterildiği nasıl aşağıdaki hello toocheck bir işlevdeki yaklaşan WebJob sonlandırma için.</span><span class="sxs-lookup"><span data-stu-id="46c75-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="46c75-169">**Not:** hello Pano hello durumunu ve çıkışını kapatılmışsa işlevlerin doğru şekilde göstermeyebilir.</span><span class="sxs-lookup"><span data-stu-id="46c75-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="46c75-170">Daha fazla bilgi için bkz: [Web işleri normal şekilde kapatılmasını](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="46c75-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="46c75-171">Toocreate bir kuyruk iletisi nasıl bir kuyruk iletisi işlenirken</span><span class="sxs-lookup"><span data-stu-id="46c75-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="46c75-172">Yeni bir kuyruk iletisi kullanım hello oluşturan bir işlev toowrite **sıra** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="46c75-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="46c75-173">Gibi **QueueTrigger**, hello kuyruk adı bir dize olarak geçirin veya yapabilecekleriniz [hello sıra adı dinamik olarak ayarlamak](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="46c75-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="46c75-174">Dize iletileri</span><span class="sxs-lookup"><span data-stu-id="46c75-174">String queue messages</span></span>
<span data-ttu-id="46c75-175">zaman uyumsuz olmayan kodu örneği aşağıdaki hello hello kuyruk iletisi olarak içerik aynı "inputqueue" adlı hello sıraya alınan hello hello sırasındaki "outputqueue" adlı yeni bir kuyruk iletisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46c75-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="46c75-176">(İşlevler için async kullanma **IAsyncCollector<T>**  daha sonra bu bölümde gösterilen.)</span><span class="sxs-lookup"><span data-stu-id="46c75-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="46c75-177">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="46c75-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="46c75-178">toocreate geçişi hello POCO bir dize yerine bir POCO içeren bir kuyruk iletisi türü bir çıkış parametresi toohello **sıra** özniteliği Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="46c75-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="46c75-179">Merhaba SDK hello nesne tooJSON otomatik olarak serileştirir.</span><span class="sxs-lookup"><span data-stu-id="46c75-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="46c75-180">Merhaba nesnesi boş olsa bile bir kuyruk iletisi her zaman oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="46c75-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="46c75-181">Birden çok iletileri oluşturmak veya zaman uyumsuz işlevleri</span><span class="sxs-lookup"><span data-stu-id="46c75-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="46c75-182">toocreate birden fazla ileti olun hello çıkış sırası için hello parametre türü **ICollector<T>**  veya **IAsyncCollector<T>**hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="46c75-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="46c75-183">Her kuyruk iletisi hemen hello oluşturulduğunda **Ekle** yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="46c75-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="46c75-184">Türleri bu hello sıra özniteliği birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="46c75-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="46c75-185">Merhaba kullanabilirsiniz **sıra** parametre türleri şu hello özniteliği:</span><span class="sxs-lookup"><span data-stu-id="46c75-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="46c75-186">**dize çıkışı** (Merhaba işlevi sona erdiğinde parametre değeri null olmayan ise kuyruk iletisi oluşturur)</span><span class="sxs-lookup"><span data-stu-id="46c75-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="46c75-187">**byte [] çıkışı** (gibi çalışır **dize**)</span><span class="sxs-lookup"><span data-stu-id="46c75-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="46c75-188">**CloudQueueMessage çıkışı** (gibi çalışır **dize**)</span><span class="sxs-lookup"><span data-stu-id="46c75-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="46c75-189">**POCO çıkışı** (serializable bir tür oluşturduğu bir ileti null bir nesne ile Merhaba işlevi sona erdiğinde hello parametre null ise)</span><span class="sxs-lookup"><span data-stu-id="46c75-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="46c75-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="46c75-190">**ICollector**</span></span>
* <span data-ttu-id="46c75-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="46c75-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="46c75-192">**CloudQueue** (iletileri el ile oluşturmak için kullanarak hello Azure Storage API'sini doğrudan)</span><span class="sxs-lookup"><span data-stu-id="46c75-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="46c75-193">Web işleri SDK'si özniteliklerini işlevinin hello gövdesindeki kullanın</span><span class="sxs-lookup"><span data-stu-id="46c75-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="46c75-194">Toodo ihtiyacınız varsa bazı, işlevinde bir Web işleri SDK'si öznitelik gibi kullanmadan önce iş **sıra**, **Blob**, veya **tablo**, hello kullanabilirsiniz **IBinder** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="46c75-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="46c75-195">Aşağıdaki örneğine hello bir giriş sırası iletisi sürer ve aynı bir çıkış sırasının içerik hello ile yeni bir ileti oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46c75-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="46c75-196">Merhaba çıkış sırası adı hello işlevi hello gövdesinde kodu tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="46c75-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="46c75-197">Merhaba **IBinder** arabirimi hello ile de kullanılabilir **tablo** ve **Blob** öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="46c75-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="46c75-198">Nasıl tooread ve yazma BLOB ve bir sıraya ileti işlenirken tabloları</span><span class="sxs-lookup"><span data-stu-id="46c75-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="46c75-199">Merhaba **Blob** ve **tablo** öznitelikleri tooread etkinleştirmek ve blobları ve tabloları yazma.</span><span class="sxs-lookup"><span data-stu-id="46c75-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="46c75-200">Bu bölümdeki Hello örnekler tooblobs uygulayın.</span><span class="sxs-lookup"><span data-stu-id="46c75-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="46c75-201">BLOB'ları oluşturulduğunda veya güncelleştirilmiş tootrigger nasıl işlediği gösteren kod örnekleri için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)ve okuma ve yazma tabloları kod örnekleri için bkz: [nasıl toouse Azure tablo Depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="46c75-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="46c75-202">Dize iletileri kuyruğa blobu işlemleri tetikleme</span><span class="sxs-lookup"><span data-stu-id="46c75-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="46c75-203">Bir dizeyi içeren bir kuyruk iletisi için **queueTrigger** hello kullanabileceğiniz bir yer tutucudur **Blob** özniteliğin **blobPath** Merhaba içeriğine içeren parametresi Başlangıç iletisi.</span><span class="sxs-lookup"><span data-stu-id="46c75-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="46c75-204">Merhaba aşağıdaki örnek kullanır **akış** tooread ve yazma BLOB'lar nesneleri.</span><span class="sxs-lookup"><span data-stu-id="46c75-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="46c75-205">Merhaba kuyruk iletisi hello textblobs kapsayıcıda bulunan bir blob hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="46c75-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="46c75-206">Merhaba blob ile bir kopyasını "-Yeni" eklenmiş toohello adı oluşturulduğu hello aynı kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="46c75-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="46c75-207">Merhaba **Blob** özniteliği Oluşturucusu alır bir **blobPath** hello kapsayıcı ve blob adı belirten parametre.</span><span class="sxs-lookup"><span data-stu-id="46c75-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="46c75-208">Bu yer tutucu hakkında daha fazla bilgi için bkz: [nasıl toouse Azure blob depolama hello WebJobs SDK ile](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="46c75-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="46c75-209">Ne zaman hello öznitelik süsler bir **akış** nesnesi, başka bir oluşturucu parametresini belirtir hello **FileAccess** modu okuma, yazma veya okuma/yazma olarak.</span><span class="sxs-lookup"><span data-stu-id="46c75-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="46c75-210">Merhaba aşağıdaki örnek kullanan bir **CloudBlockBlob** toodelete blob nesnesi.</span><span class="sxs-lookup"><span data-stu-id="46c75-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="46c75-211">Merhaba kuyruk iletisi hello blob hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="46c75-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="46c75-212">POCO [(düz eski CLR nesnesi](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) kuyruk iletileri</span><span class="sxs-lookup"><span data-stu-id="46c75-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="46c75-213">JSON olarak hello kuyruk iletisi içinde depolanan bir POCO için hello hello nesnesinde özelliklerini adı yer tutucuları kullanabilirsiniz **sıra** özniteliğin **blobPath** parametresi.</span><span class="sxs-lookup"><span data-stu-id="46c75-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="46c75-214">Bu gibi durumlarda, sıra meta veri özellik adları da yer tutucu olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="46c75-215">Bkz: [sıra veya sıra ileti meta verileri alma](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="46c75-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="46c75-216">Merhaba aşağıdaki örnek bir blob tooa yeni blob farklı bir uzantı kopyalar.</span><span class="sxs-lookup"><span data-stu-id="46c75-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="46c75-217">Merhaba kuyruk iletisi bir **BlobInformation** içeren nesnesinin **BlobName** ve **BlobNameWithoutExtension** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="46c75-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="46c75-218">Merhaba özellik adları olarak kullanılan hello blob yolu yer tutucuları Merhaba **Blob** öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="46c75-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="46c75-219">Merhaba SDK kullanan hello [Newtonsoft.Json NuGet paketi](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize ve iletileri seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="46c75-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="46c75-220">Merhaba WebJobs SDK kullanmayan bir programda iletileri kuyruğa oluşturursanız, SDK ayrıştıramıyor bu hello hello örnek toocreate bir POCO kuyruk iletisi aşağıdaki gibi kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="46c75-221">Bir blob tooan nesnesi bağlama önce işlevinde bazı iş toodo gerekiyorsa, gösterildiği gibi hello işlevinin hello gövdesi hello özniteliğinde kullanabilirsiniz [hello gövdesi bir işlev kullanmak Web işleri SDK'si öznitelikleri](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="46c75-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="46c75-222">Merhaba kullanabileceğiniz türü özniteliğiyle Blob</span><span class="sxs-lookup"><span data-stu-id="46c75-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="46c75-223">Merhaba **Blob** özniteliği şu türlerini hello ile kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="46c75-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="46c75-224">**Akış** (okuma veya yazma, hello FileAccess Oluşturucu parametresi kullanılarak belirtilen)</span><span class="sxs-lookup"><span data-stu-id="46c75-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="46c75-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="46c75-225">**TextReader**</span></span>
* <span data-ttu-id="46c75-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="46c75-226">**TextWriter**</span></span>
* <span data-ttu-id="46c75-227">**dize** (okuma)</span><span class="sxs-lookup"><span data-stu-id="46c75-227">**string** (read)</span></span>
* <span data-ttu-id="46c75-228">**dize çıkışı** (yazma; hello işlevi döndüğünde yalnızca hello dizesi parametresi null olmayan ise bir blob oluşturur)</span><span class="sxs-lookup"><span data-stu-id="46c75-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="46c75-229">POCO (okuma)</span><span class="sxs-lookup"><span data-stu-id="46c75-229">POCO (read)</span></span>
* <span data-ttu-id="46c75-230">POCO out (yazma; her zaman bir blob oluşturur, hello işlevi döndüğünde POCO parametre null ise null nesnesi olarak oluşturur)</span><span class="sxs-lookup"><span data-stu-id="46c75-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="46c75-231">**CloudBlobStream** (yazma)</span><span class="sxs-lookup"><span data-stu-id="46c75-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="46c75-232">**ICloudBlob** (okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="46c75-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="46c75-233">**CloudBlockBlob** (okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="46c75-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="46c75-234">**CloudPageBlob** (okuma veya yazma)</span><span class="sxs-lookup"><span data-stu-id="46c75-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="46c75-235">Nasıl toohandle zehirli ileti</span><span class="sxs-lookup"><span data-stu-id="46c75-235">How toohandle poison messages</span></span>
<span data-ttu-id="46c75-236">İçerikleri işlevi toofail neden olan iletileri çağrılır *zehirli ileti*.</span><span class="sxs-lookup"><span data-stu-id="46c75-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="46c75-237">Merhaba işlevi başarısız olduğunda, hello kuyruk iletisi silinmez ve sonunda yeniden neden hello döngüsü toobe yinelenen kayıt.</span><span class="sxs-lookup"><span data-stu-id="46c75-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="46c75-238">otomatik olarak hello döngüsü Hello SDK sınırlı sayıda yineleme sonra kesintiye uğratabilir veya el ile yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="46c75-239">Otomatik zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="46c75-239">Automatic poison message handling</span></span>
<span data-ttu-id="46c75-240">Merhaba SDK too5 kez tooprocess bir kuyruk iletisi yukarı işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="46c75-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="46c75-241">Merhaba beşinci deneme başarısız olursa, selamlama iletisine taşınan tooa zararlı sıradır.</span><span class="sxs-lookup"><span data-stu-id="46c75-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="46c75-242">Nasıl tooconfigure Merhaba yeniden deneme sayısı görebilirsiniz [nasıl tooset yapılandırma seçenekleri](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="46c75-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="46c75-243">Merhaba zararlı sıra adlandırılan *{originalqueuename}*-zararlı.</span><span class="sxs-lookup"><span data-stu-id="46c75-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="46c75-244">Bir işlev tooprocess iletileri hello zararlı sıradan günlüğe yazma veya el ile ilgilenilmesi gereken bir bildirim göndererek yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="46c75-245">Aşağıdaki örnek hello hello içinde **CopyBlob** bir kuyruk iletisi mevcut olmayan bir blob hello adını içerdiğinde işlevi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="46c75-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="46c75-246">Bu durum oluştuğunda selamlama iletisine hello copyblobqueue sıra toohello copyblobqueue poison sıradan taşınır.</span><span class="sxs-lookup"><span data-stu-id="46c75-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="46c75-247">Merhaba **ProcessPoisonMessage** zehir iletisi günlükleri hello sonra.</span><span class="sxs-lookup"><span data-stu-id="46c75-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

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

<span data-ttu-id="46c75-248">zararlı bir ileti işlendiğinde hello aşağıda bu işlevler konsol çıktısı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="46c75-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Zehirli ileti işleme için konsol çıkışı](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="46c75-250">El ile zehirli ileti işleme</span><span class="sxs-lookup"><span data-stu-id="46c75-250">Manual poison message handling</span></span>
<span data-ttu-id="46c75-251">Hello sayısı bir ileti toplanma işleme ekleyerek alabileceğiniz bir **int** adlı parametre **dequeueCount** tooyour işlevi.</span><span class="sxs-lookup"><span data-stu-id="46c75-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="46c75-252">Bundan sonra onay hello işlev kodu sayıma dequeue ve hello sayısı hello aşağıdaki örnekte gösterildiği gibi bir eşiği aştığında kendi zehirli ileti işleme gerçekleştirmek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="46c75-253">Nasıl tooset yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="46c75-253">How tooset configuration options</span></span>
<span data-ttu-id="46c75-254">Merhaba kullanabilirsiniz **JobHostConfiguration** yapılandırma seçenekleri aşağıdaki türü tooset hello:</span><span class="sxs-lookup"><span data-stu-id="46c75-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="46c75-255">Kodda Hello SDK bağlantı dizelerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="46c75-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="46c75-256">Yapılandırma **QueueTrigger** maksimum gibi ayarları dequeue sayısı.</span><span class="sxs-lookup"><span data-stu-id="46c75-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="46c75-257">Sıra adları yapılandırmasından alın.</span><span class="sxs-lookup"><span data-stu-id="46c75-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="46c75-258">Kod içinde SDK bağlantı dizelerini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="46c75-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="46c75-259">Kodda Hello SDK bağlantı dizelerini ayarlama, toouse kendi bağlantı dizesi adlarında yapılandırma dosyalarının veya ortam değişkenleri hello aşağıdaki örnekte gösterildiği gibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="46c75-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="46c75-260">QueueTrigger ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46c75-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="46c75-261">Toohello sıraya ileti işleme uygulanan ayarları aşağıdaki hello yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="46c75-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="46c75-262">Merhaba en fazla eşzamanlı olarak paralel olarak yürütülen toobe yukarı çekilen sıraya ileti sayısı (varsayılan olarak 16).</span><span class="sxs-lookup"><span data-stu-id="46c75-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="46c75-263">bir kuyruk iletisi tooa zararlı sıra gönderilmeden önce yeniden deneme sayısı Hello (varsayılan olarak 5).</span><span class="sxs-lookup"><span data-stu-id="46c75-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="46c75-264">bir sıranın boş olduğunda yeniden yoklama önce hello maksimum bekleme süresi (varsayılan değer 1 dakika).</span><span class="sxs-lookup"><span data-stu-id="46c75-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="46c75-265">örnekte gösterildiği nasıl aşağıdaki hello tooconfigure bu ayarları:</span><span class="sxs-lookup"><span data-stu-id="46c75-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="46c75-266">Değerleri için Web işleri SDK'si Oluşturucu parametreleri kodda ayarlama</span><span class="sxs-lookup"><span data-stu-id="46c75-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="46c75-267">Kuyruk adı, bir blob adı veya kapsayıcı toospecify bazen istediğiniz veya bir tablo adı kod sabit kodlu yerine onu.</span><span class="sxs-lookup"><span data-stu-id="46c75-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="46c75-268">Örneğin, toospecify hello sıra adı için isteyebilirsiniz **QueueTrigger** bir yapılandırma dosyası veya ortam değişkeninde.</span><span class="sxs-lookup"><span data-stu-id="46c75-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="46c75-269">Bunu geçirerek yapabilirsiniz bir **NameResolver** toohello nesne **JobHostConfiguration** türü.</span><span class="sxs-lookup"><span data-stu-id="46c75-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="46c75-270">Web işleri SDK'si özniteliği Oluşturucusu parametrelerinde yüzde (%) işareti tarafından çevrelenen özel yer tutucular içerir ve **NameResolver** kod bu yer tutucular yerine kullanılan hello gerçek değerler toobe belirtir.</span><span class="sxs-lookup"><span data-stu-id="46c75-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="46c75-271">Örneğin, toouse istediğinizi düşünelim bir sıra hello test ortamında logqueuetest ve üretimde bir adlandırılmış logqueueprod adlı.</span><span class="sxs-lookup"><span data-stu-id="46c75-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="46c75-272">Sabit kodlanmış kuyruk adı yerine bir girişe hello toospecify hello adı istediğiniz **appSettings** hello gerçek sıra adı olurdu koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="46c75-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="46c75-273">Merhaba, **appSettings** anahtar logqueue, işlevinizi aşağıdaki örneğine hello gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="46c75-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="46c75-274">**NameResolver** sınıfını hello sıra adından sonra almak **appSettings** hello aşağıdaki örnekte gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="46c75-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="46c75-275">Merhaba geçirdiğiniz **NameResolver** toohello sınıfında **JobHost** nesne hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="46c75-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="46c75-276">**Not:** kuyruk, tablo ve blob adları çözümlenmiş her zaman bir işlev çağrılır, ancak blob kapsayıcı adları yalnızca Merhaba uygulaması başladığında çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="46c75-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="46c75-277">Merhaba iş çalışırken blob kapsayıcı adı değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="46c75-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="46c75-278">Nasıl tootrigger bir işlev el ile</span><span class="sxs-lookup"><span data-stu-id="46c75-278">How tootrigger a function manually</span></span>
<span data-ttu-id="46c75-279">tootrigger işlevi el ile Merhaba kullanmak **çağrısı** veya **CallAsync** hello yöntemi **JobHost** nesne ve hello **NoAutomaticTrigger** hello aşağıdaki örnekte gösterildiği gibi hello işlevi özniteliği.</span><span class="sxs-lookup"><span data-stu-id="46c75-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

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

## <a name="how-toowrite-logs"></a><span data-ttu-id="46c75-280">Toowrite nasıl kaydeder</span><span class="sxs-lookup"><span data-stu-id="46c75-280">How toowrite logs</span></span>
<span data-ttu-id="46c75-281">Başlangıç Panosu iki yerde günlükleri gösterir: hello sayfası hello Web işi için ve belirli bir Web işi çağırma için hello sayfası.</span><span class="sxs-lookup"><span data-stu-id="46c75-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Web işi sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![İşlev çağırma sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="46c75-284">Bir işlev veya hello çağıran konsol yöntemlerini çıkışı **Main()** yöntemi görünür hello Web işi için hello Pano sayfası, belirli yöntem çağırma için hello sayfasındaki değil.</span><span class="sxs-lookup"><span data-stu-id="46c75-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="46c75-285">Çıktı yöntemi imzanız bir parametresinden alma hello TextWriter nesneden bir yöntem çağırma için hello Pano sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="46c75-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="46c75-286">Konsol çıktısı, bağlantılı tooa belirli yöntemi çağırma olamaz, hello konsol birçok iş işlevlerinin hello çalışmıyor olabilir tek iş parçacıklı, olduğu için aynı anda.</span><span class="sxs-lookup"><span data-stu-id="46c75-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="46c75-287">İşte bu nedenle hello SDK her işlev çağrısını kendi benzersiz günlük yazıcı nesnesi ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="46c75-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="46c75-288">toowrite [uygulama izleme günlükleri](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), kullanın **Console.Out** (bilgisi olarak işaretlenmiş günlükleri oluşturur) ve **Console.Error** (hata olarak işaretlenmiş günlükleri oluşturur).</span><span class="sxs-lookup"><span data-stu-id="46c75-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="46c75-289">Toouse alternatiftir [izleme veya TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), uyarı, ayrıntı sağlar ve kritik düzeyleri toplama tooInfo ve hata.</span><span class="sxs-lookup"><span data-stu-id="46c75-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="46c75-290">Azure web uygulamanızı nasıl yapılandırdığınıza bağlı olarak Azure BLOB veya uygulama izleme günlükleri hello web uygulama günlük dosyalarında Azure tabloları görünür.</span><span class="sxs-lookup"><span data-stu-id="46c75-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="46c75-291">Tüm konsol çıktısı doğru olduğu gibi hello en son 100 uygulama günlüklerini da hello Web işi, olmayan bir işlev çağrısını hello sayfasını için hello Pano sayfası görünür.</span><span class="sxs-lookup"><span data-stu-id="46c75-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="46c75-292">Merhaba hello programı yerel olarak çalışmıyorsa hello program bir Azure WebJob içinde yalnızca çalışıyorsa, Pano veya başka bir ortamında konsol çıktısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="46c75-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="46c75-293">Merhaba Pano bağlantı dizesi toonull ayarlayarak günlüğü devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46c75-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="46c75-294">Daha fazla bilgi için bkz: [nasıl tooset yapılandırma seçenekleri](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="46c75-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="46c75-295">Merhaba aşağıdaki örnekte çeşitli yollar gösterir toowrite günlükleri:</span><span class="sxs-lookup"><span data-stu-id="46c75-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="46c75-296">Hello WebJobs SDK Pano, hello hello çıktısını **TextWriter** toohello sayfa belirli bir zaman gittiğiniz yukarı gösterir işlev çağırma ve seçin nesnesi **geçiş çıktı**:</span><span class="sxs-lookup"><span data-stu-id="46c75-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Çağırma bağlantı](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![İşlev çağırma sayfasındaki günlükleri](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="46c75-299">Merhaba WebJob (değil hello işlev çağrısını) için toohello sayfasına gidin ve seçin hello WebJobs SDK Pano, konsol hello en son 100 satırları göster yukarı çıktı **geçiş çıktı**.</span><span class="sxs-lookup"><span data-stu-id="46c75-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Çıkışı Aç/Kapat](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="46c75-301">Bir sürekli Webjob'un uygulama günlüklerini/data/işleri/sürekli/içinde gösterilmesi*{webjobname}*hello web uygulama dosya sisteminde /job_log.txt.</span><span class="sxs-lookup"><span data-stu-id="46c75-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="46c75-302">Azure blob hello uygulamada günlükleri şuna benzeyebilir: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Merhaba Dünya!, 2014-09-26T21:01:13, hata, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Merhaba Dünya!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Merhaba Dünya!,</span><span class="sxs-lookup"><span data-stu-id="46c75-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="46c75-303">Ve Azure tablo hello **Console.Out** ve **Console.Error** günlükleri şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="46c75-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Tablo bilgi günlüğüne](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Hata günlüğü tablosundaki](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="46c75-306">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46c75-306">Next steps</span></span>
<span data-ttu-id="46c75-307">Bu makalede kod sağlamıştır gösteren nasıl örnekleri Azure kuyruklarla çalışmaya yönelik yaygın senaryolar toohandle.</span><span class="sxs-lookup"><span data-stu-id="46c75-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="46c75-308">Toouse Azure Web işleri ve hello Web işleri SDK'si nasıl görürüm hakkında daha fazla bilgi için [Azure Web işleri belge kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="46c75-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

