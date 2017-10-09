---
title: "aaaGet, bağlı hizmetler (ASP.NET Core) kuyruk depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio'da ASP.NET Core projesinde Azure kuyruk depolama kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 75adb7163827ab17ad89707051ff0e48dbae9c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="171d2-103">Kuyruk depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (ASP.NET çekirdek)</span><span class="sxs-lookup"><span data-stu-id="171d2-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="171d2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="171d2-104">Overview</span></span>
<span data-ttu-id="171d2-105">Oluşturulan veya hello Visual Studio kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra Visual Studio'da Azure kuyruk depolama kullanarak tooget nasıl başlatılacağını bu makalede **bağlı Hizmetleri Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="171d2-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="171d2-106">Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="171d2-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="171d2-107">Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="171d2-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="171d2-108">Tek bir kuyruk iletisinin boyutu too64 kilobayt (KB) ayarlama olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.</span><span class="sxs-lookup"><span data-stu-id="171d2-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="171d2-109">başlatılan tooget önce toocreate Azure kuyruk depolama hesabınızdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="171d2-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="171d2-110">Nasıl göstereceğiz toocreate bir kuyruktaki kod.</span><span class="sxs-lookup"><span data-stu-id="171d2-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="171d2-111">Ayrıca, nasıl tooperform basic sıraya ekleme, değiştirme, okuma ve iletileri kuyruğa kaldırma gibi işlemleri göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="171d2-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="171d2-112">Merhaba örnekleri C'de yazılmış\# kod ve .NET için Azure Storage istemci kitaplığı hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="171d2-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="171d2-113">ASP.NET hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="171d2-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="171d2-114">**Not:** hello çağrıları tooAzure depolama ASP.NET Core gerçekleştirmek API'leri bazıları zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="171d2-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="171d2-115">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="171d2-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="171d2-116">Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="171d2-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="171d2-117">Bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](storage-dotnet-how-to-use-queues.md) program aracılığıyla Kuyrukları düzenleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="171d2-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="171d2-118">Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="171d2-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="171d2-119">Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.</span><span class="sxs-lookup"><span data-stu-id="171d2-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="171d2-120">Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="171d2-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="171d2-121">Kod erişim kuyruklar</span><span class="sxs-lookup"><span data-stu-id="171d2-121">Access queues in code</span></span>
<span data-ttu-id="171d2-122">ASP.NET Core projelerinde tooaccess sıraları, gereksinim duyduğunuz tooinclude hello aşağıdaki Azure kuyruk depolama erişen öğeleri tooany C# kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="171d2-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="171d2-123">Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="171d2-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="171d2-124">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="171d2-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="171d2-125">Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.</span><span class="sxs-lookup"><span data-stu-id="171d2-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="171d2-126">Alma bir **CloudQueueClient** tooreference hello sıra nesneleri depolama hesabınızdaki nesne.</span><span class="sxs-lookup"><span data-stu-id="171d2-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="171d2-127">Alma bir **CloudQueue** tooreference belirli bir kuyruğa nesne.</span><span class="sxs-lookup"><span data-stu-id="171d2-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="171d2-128">**Not:** hello hello kod önünde kodu yukarıdaki tüm örnekleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="171d2-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="171d2-129">Kodda bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="171d2-129">Create a queue in code</span></span>
<span data-ttu-id="171d2-130">toocreate hello kodda, Azure kuyruk eklemeniz yeterlidir bir çağrı çok**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="171d2-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="171d2-131">Bir ileti tooa sırası Ekle</span><span class="sxs-lookup"><span data-stu-id="171d2-131">Add a message tooa queue</span></span>
<span data-ttu-id="171d2-132">var olan bir sırayı iletiye tooinsert oluşturma yeni bir **CloudQueueMessage** nesne sonra çağrı hello **AddMessageAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="171d2-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="171d2-133">A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="171d2-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="171d2-134">Burada, selamlama iletisine 'Hello, World' ekleyen bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="171d2-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="171d2-135">Bir kuyruktaki ileti okuma</span><span class="sxs-lookup"><span data-stu-id="171d2-135">Read a message in a queue</span></span>
<span data-ttu-id="171d2-136">Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **PeekMessageAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="171d2-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="171d2-137">Okuma ve bir sıraya bir ileti Kaldır</span><span class="sxs-lookup"><span data-stu-id="171d2-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="171d2-138">Kodunuzu kaldırabilirsiniz (dequeue) bir iletiyi bir kuyruktan iki adımda.</span><span class="sxs-lookup"><span data-stu-id="171d2-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="171d2-139">Çağrı **GetMessageAsync** tooget hello sıradaki ilk iletiye bir sıra.</span><span class="sxs-lookup"><span data-stu-id="171d2-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="171d2-140">Döndürülen bir ileti **GetMessageAsync** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="171d2-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="171d2-141">Varsayılan olarak bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="171d2-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="171d2-142">Merhaba sıradan çağrısı selamlama iletisine kaldırarak toofinish **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="171d2-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="171d2-143">Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="171d2-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="171d2-144">Merhaba aşağıdaki kod çağrıları **DeleteMessageAsync** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="171d2-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="171d2-145">İletilerin kuyruktan alma için ek seçenekler yararlanın</span><span class="sxs-lookup"><span data-stu-id="171d2-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="171d2-146">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="171d2-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="171d2-147">İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="171d2-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="171d2-148">İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="171d2-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="171d2-149">Merhaba aşağıdaki kod örneğinde **GetMessages** bir çağrı yöntemi tooget 20 iletileri.</span><span class="sxs-lookup"><span data-stu-id="171d2-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="171d2-150">Ardından her ileti bir **foreach** döngüsü ile işlenir.</span><span class="sxs-lookup"><span data-stu-id="171d2-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="171d2-151">Ayrıca, her ileti için hello görünmezlik zaman aşımı too5 dakika ayarlar.</span><span class="sxs-lookup"><span data-stu-id="171d2-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="171d2-152">Tüm Hello 5 dakika başlangıç hello aynı iletilerini olduğunu not alın zaman, bunu hello çağrısından sonra çok 5 dakika geçtikten sonra**GetMessages**, silinmemiş herhangi ileti yeniden görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="171d2-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="171d2-153">Merhaba kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="171d2-153">Get hello queue length</span></span>
<span data-ttu-id="171d2-154">Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="171d2-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="171d2-155">**FetchAttributes** yöntemi hello sıra hizmetinin hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini almasını ister.</span><span class="sxs-lookup"><span data-stu-id="171d2-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="171d2-156">Merhaba **ApproximateMethodCount** özelliği tarafından alınan hello son değeri döndürür **FetchAttributes** hello kuyruk hizmetini çağırmadan olmadan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="171d2-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="171d2-157">Ortak sıra API'leri Hello zaman uyumsuz-bekleme düzenini kullanın</span><span class="sxs-lookup"><span data-stu-id="171d2-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="171d2-158">Bu örnek nasıl toouse hello genel sıra API'leri ile zaman uyumsuz-bekleme düzeni gösterir.</span><span class="sxs-lookup"><span data-stu-id="171d2-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="171d2-159">Her bir yöntem verilen hello Hello örnek çağrıları hello zaman uyumsuz sürümü.</span><span class="sxs-lookup"><span data-stu-id="171d2-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="171d2-160">Bu hello zaman uyumsuz sonrası düzeltme her yöntemin tarafından görülebilir.</span><span class="sxs-lookup"><span data-stu-id="171d2-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="171d2-161">Async yöntemi kullanıldığında, hello çağrı tamamlanana kadar hello zaman uyumsuz-bekleme yerel yürütme askıya alır.</span><span class="sxs-lookup"><span data-stu-id="171d2-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="171d2-162">Bu davranış, performans sorunlarını engellemeye yardımcı olur ve artırır diğer iş hello geçerli iş parçacığı toodo verir Merhaba, uygulamanızın genel yanıt.</span><span class="sxs-lookup"><span data-stu-id="171d2-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="171d2-163">Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [zaman uyumsuz ve bekleme (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="171d2-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="171d2-164">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="171d2-164">Delete a queue</span></span>
<span data-ttu-id="171d2-165">toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **silmek** hello nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="171d2-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="171d2-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="171d2-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

