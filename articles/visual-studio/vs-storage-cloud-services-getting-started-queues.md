---
title: "aaaGet, bağlı hizmetler (bulut Hizmetleri) kuyruk depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra bir bulut hizmeti projesini Visual Studio'da Azure kuyruk depolama kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="633c8-103">Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama (Projeler bulut Hizmetleri) Hizmetleri bağlı</span><span class="sxs-lookup"><span data-stu-id="633c8-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="633c8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="633c8-104">Overview</span></span>
<span data-ttu-id="633c8-105">Oluşturulan veya hello Visual Studio kullanarak bir Azure depolama hesabı bulut Hizmetleri projesinde başvurulan sonra Visual Studio'da Azure kuyruk depolama kullanarak tooget nasıl başlatılacağını bu makalede **bağlı Hizmetleri Ekle** iletişim .</span><span class="sxs-lookup"><span data-stu-id="633c8-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="633c8-106">Nasıl göstereceğiz toocreate bir kuyruktaki kod.</span><span class="sxs-lookup"><span data-stu-id="633c8-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="633c8-107">Ayrıca, nasıl tooperform basic sıraya ekleme, değiştirme, okuma ve kaldırma iletileri gibi işlemleri göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="633c8-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="633c8-108">Merhaba örnekler C# kodda yazılır ve hello kullanır [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="633c8-109">Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="633c8-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="633c8-110">Bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](../storage/queues/storage-dotnet-how-to-use-queues.md) kod kuyruklarda düzenleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="633c8-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="633c8-111">Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="633c8-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="633c8-112">Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.</span><span class="sxs-lookup"><span data-stu-id="633c8-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="633c8-113">Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="633c8-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="633c8-114">Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="633c8-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="633c8-115">Tek bir kuyruk iletisinin boyutu too64 KB yukarı olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.</span><span class="sxs-lookup"><span data-stu-id="633c8-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="633c8-116">Kod erişim kuyruklar</span><span class="sxs-lookup"><span data-stu-id="633c8-116">Access queues in code</span></span>
<span data-ttu-id="633c8-117">Visual Studio bulut Hizmetleri projelerinde tooaccess sıraları, gereksinim duyduğunuz tooinclude hello aşağıdaki Azure kuyruk depolama erişim öğeleri tooany C# kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="633c8-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="633c8-118">Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="633c8-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="633c8-119">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="633c8-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="633c8-120">Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="633c8-121">Alma bir **CloudQueueClient** tooreference hello sıra nesneleri depolama hesabınızdaki nesne.</span><span class="sxs-lookup"><span data-stu-id="633c8-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="633c8-122">Alma bir **CloudQueue** tooreference belirli bir kuyruğa nesne.</span><span class="sxs-lookup"><span data-stu-id="633c8-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="633c8-123">**Not:** hello hello kod önünde kodu yukarıdaki tüm örnekleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="633c8-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="633c8-124">Kodda bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="633c8-124">Create a queue in code</span></span>
<span data-ttu-id="633c8-125">kodda, toocreate hello sıra eklemeniz yeterlidir bir çağrı çok**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="633c8-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="633c8-126">Bir ileti tooa sırası Ekle</span><span class="sxs-lookup"><span data-stu-id="633c8-126">Add a message tooa queue</span></span>
<span data-ttu-id="633c8-127">var olan bir sırayı iletiye tooinsert oluşturma yeni bir **CloudQueueMessage** nesne sonra çağrı hello **AddMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="633c8-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="633c8-128">A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="633c8-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="633c8-129">Burada, selamlama iletisine 'Hello, World' ekleyen bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="633c8-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="633c8-130">Bir kuyruktaki ileti okuma</span><span class="sxs-lookup"><span data-stu-id="633c8-130">Read a message in a queue</span></span>
<span data-ttu-id="633c8-131">Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **PeekMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="633c8-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="633c8-132">Okuma ve bir sıraya bir ileti Kaldır</span><span class="sxs-lookup"><span data-stu-id="633c8-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="633c8-133">Kodunuzu kaldırabilirsiniz (kuyruktan) bir iletiyi bir kuyruktan iki adımda.</span><span class="sxs-lookup"><span data-stu-id="633c8-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="633c8-134">Çağrı **GetMessage** tooget hello sıradaki ilk iletiye bir sıra.</span><span class="sxs-lookup"><span data-stu-id="633c8-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="633c8-135">Döndürülen bir ileti **GetMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="633c8-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="633c8-136">Varsayılan olarak bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="633c8-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="633c8-137">Merhaba sıradan çağrısı selamlama iletisine kaldırarak toofinish **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="633c8-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="633c8-138">Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="633c8-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="633c8-139">Merhaba aşağıdaki kod çağrıları **DeleteMessage** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="633c8-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="633c8-140">Ek seçenekler tooprocess kullanın ve iletileri kuyruğa kaldırın</span><span class="sxs-lookup"><span data-stu-id="633c8-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="633c8-141">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="633c8-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="633c8-142">Toplu (yukarı too32) iletiler alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="633c8-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="633c8-143">Kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="633c8-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="633c8-144">Merhaba aşağıdaki kod örneğinde **GetMessages** bir çağrı yöntemi tooget 20 iletileri.</span><span class="sxs-lookup"><span data-stu-id="633c8-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="633c8-145">Ardından her ileti bir **foreach** döngüsü ile işlenir.</span><span class="sxs-lookup"><span data-stu-id="633c8-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="633c8-146">Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar.</span><span class="sxs-lookup"><span data-stu-id="633c8-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="633c8-147">Bu hello 5 dakika Not hello tüm iletileri için aynı başlatıldığında, bunu hello görüşmede çok 5 dakika geçtikten sonra**GetMessages**, silinmemiş tüm iletiler görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="633c8-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="633c8-148">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="633c8-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="633c8-149">Merhaba kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="633c8-149">Get hello queue length</span></span>
<span data-ttu-id="633c8-150">Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="633c8-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="633c8-151">**FetchAttributes** yöntemi hello sıra hizmetinin hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini almasını ister.</span><span class="sxs-lookup"><span data-stu-id="633c8-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="633c8-152">Merhaba **ApproximateMethodCount** özelliği tarafından alınan hello son değeri döndürür **FetchAttributes** hello kuyruk hizmetini çağırmadan olmadan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="633c8-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="633c8-153">Kullanım hello ortak Azure sıra API'leri ile zaman uyumsuz-bekleme yöntemi</span><span class="sxs-lookup"><span data-stu-id="633c8-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="633c8-154">Bu örnek nasıl toouse hello zaman uyumsuz-bekleme desen ile ortak Azure sıra API'leri gösterir.</span><span class="sxs-lookup"><span data-stu-id="633c8-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="633c8-155">Merhaba örnek çağırır hello zaman uyumsuz sürümü her yöntemleri verilen Merhaba, bu hello tarafından görülebilir **zaman uyumsuz** yönteminin her sonrası düzeltme.</span><span class="sxs-lookup"><span data-stu-id="633c8-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="633c8-156">Zaman uyumsuz yöntem kullanılan hello zaman uyumsuz olduğunda-bekleme düzeni hello çağrı tamamlanana kadar yerel çalıştırmayı askıya alır.</span><span class="sxs-lookup"><span data-stu-id="633c8-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="633c8-157">Bu davranış, performans sorunlarını engellemeye yardımcı olur ve artırır diğer iş hello geçerli iş parçacığı toodo verir Merhaba, uygulamanızın genel yanıt.</span><span class="sxs-lookup"><span data-stu-id="633c8-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="633c8-158">Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [zaman uyumsuz ve bekleme (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="633c8-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="633c8-159">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="633c8-159">Delete a queue</span></span>
<span data-ttu-id="633c8-160">bir kuyruk ve tüm karışılama iletileri bulunan, içinde arama hello toodelete **silmek** hello nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="633c8-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="633c8-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="633c8-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

