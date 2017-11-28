---
title: "Kuyruk depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (bulut Hizmetleri) | Microsoft Docs"
description: "Visual Studio kullanarak bir depolama hesabı bağlandıktan sonra bir bulut hizmeti projesini Visual Studio kullanarak Azure kuyruk depolamaya başlama Hizmetleri bağlı"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: d0e6e3eab312f169b1d05ba16e2e293e103df1ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="ec060-103">Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama (Projeler bulut Hizmetleri) Hizmetleri bağlı</span><span class="sxs-lookup"><span data-stu-id="ec060-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="ec060-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ec060-104">Overview</span></span>
<span data-ttu-id="ec060-105">Bu makalede nasıl oluşturduğunuz veya Visual Studio kullanarak bir Azure depolama hesabı bulut Hizmetleri projesinde başvurulan sonra Visual Studio'da Azure kuyruk depolama kullanarak başlayacağınızı **bağlı Hizmetleri Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="ec060-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="ec060-106">Kodda bir kuyruk oluşturulacağını göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="ec060-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="ec060-107">Ayrıca, ekleme, değiştirme, okuma ve iletileri kuyruğa kaldırma gibi temel kuyruk işlemlerini gerçekleştirmek nasıl göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="ec060-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="ec060-108">Örnekler C# kodu ve kullanım yazılır [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec060-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="ec060-109">**Bağlı Hizmetleri Ekle** işlemi Azure depolama projenize erişmek için uygun NuGet paketlerini yükler ve proje yapılandırma dosyalarınızı depolama hesabı için bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="ec060-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="ec060-110">Bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](storage-dotnet-how-to-use-queues.md) kod kuyruklarda düzenleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="ec060-110">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="ec060-111">Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="ec060-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="ec060-112">Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ec060-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="ec060-113">Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="ec060-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="ec060-114">Azure Kuyruk depolama, HTTP veya HTTPS kullanan kimlik doğrulaması yapılmış çağrılar aracılığıyla dünyanın her yerinden erişilebilen çok sayıda iletinin depolanması için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="ec060-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="ec060-115">Tek bir kuyruk iletisinin boyutu 64 KB’ye kadar olabilir ve bir kuyrukta, depolama hesabının toplam kapasite sınırına kadar milyonlarca ileti bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="ec060-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="ec060-116">Kod erişim kuyruklar</span><span class="sxs-lookup"><span data-stu-id="ec060-116">Access queues in code</span></span>
<span data-ttu-id="ec060-117">Visual Studio bulut Hizmetleri projeleri kuyruklarda erişmek için Azure kuyruk depolama erişim aşağıdaki öğeler herhangi C# kaynak dosyaya eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec060-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="ec060-118">Ad alanı bildirimlerini dosyanın üst kısmındaki C# bu eklediğinizden emin olun **kullanarak** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="ec060-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="ec060-119">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="ec060-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ec060-120">Almak için aşağıdaki kodu kullanın depolama bağlantı dizesini ve Azure hizmet yapılandırma depolama hesabı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ec060-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="ec060-121">Alma bir **CloudQueueClient** depolama hesabınızda sıra nesneleri başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="ec060-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="ec060-122">Alma bir **CloudQueue** belirli bir kuyruğa başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="ec060-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="ec060-123">**Not:** tüm kod önünde Yukarıdaki kod aşağıdaki örneklerde kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec060-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="ec060-124">Kodda bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="ec060-124">Create a queue in code</span></span>
<span data-ttu-id="ec060-125">Kodda sırayı oluşturmak için yalnızca bir çağrı ekleyin **CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="ec060-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="ec060-126">Kuyruğa bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="ec060-126">Add a message to a queue</span></span>
<span data-ttu-id="ec060-127">Varolan bir sıraya bir ileti eklemek için yeni bir oluşturma **CloudQueueMessage** nesne sonra çağırın **AddMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ec060-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="ec060-128">A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="ec060-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="ec060-129">Burada, 'Hello, World' iletisini ekleyen bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ec060-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="ec060-130">Bir kuyruktaki ileti okuma</span><span class="sxs-lookup"><span data-stu-id="ec060-130">Read a message in a queue</span></span>
<span data-ttu-id="ec060-131">**PeekMessage** yöntemini çağırarak iletiyi kuyruktan kaldırmadan kuyruğun önündeki iletiye göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec060-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="ec060-132">Okuma ve bir sıraya bir ileti Kaldır</span><span class="sxs-lookup"><span data-stu-id="ec060-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="ec060-133">Kodunuzu kaldırabilirsiniz (kuyruktan) bir iletiyi bir kuyruktan iki adımda.</span><span class="sxs-lookup"><span data-stu-id="ec060-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="ec060-134">Çağrı **GetMessage** sonraki iletiyi sıraya alınamadı.</span><span class="sxs-lookup"><span data-stu-id="ec060-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="ec060-135">**GetMessage**’dan dönen bir ileti bu kuyruktaki kod okuyan iletilere karşı görünmez olur.</span><span class="sxs-lookup"><span data-stu-id="ec060-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="ec060-136">Varsayılan olarak bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="ec060-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="ec060-137">İletiyi kuyruktan kaldırmayı tamamlamak için arama **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="ec060-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="ec060-138">Bir iletinin iki adımlı kaldırılma süreci, donanım veya yazılım arızasından dolayı kodunuzun bir iletiyi işleyememesi durumunda kodunuzun başka bir örneğinin aynı iletiyi alıp yeniden denemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec060-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="ec060-139">Aşağıdaki kod çağrıları **DeleteMessage** ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="ec060-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="ec060-140">İşlem ve iletileri kuyruğa kaldırmak için ek seçenekleri kullanın</span><span class="sxs-lookup"><span data-stu-id="ec060-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="ec060-141">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec060-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="ec060-142">Toplu (en fazla 32) iletiler alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec060-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="ec060-143">Uzun veya daha kısa bir görünmezlik zaman aşımı kodunuzun her iletiyi tamamen işlemesi için zaman daha az veya daha fazla izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec060-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="ec060-144">Aşağıdaki kod örneğinde tek çağrıda 20 ileti almak için **GetMessages** yöntemi kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ec060-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="ec060-145">Ardından her ileti bir **foreach** döngüsü ile işlenir.</span><span class="sxs-lookup"><span data-stu-id="ec060-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="ec060-146">Ayrıca her ileti için görünmezlik zaman aşımı beş dakika olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ec060-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="ec060-147">5 dakikalık sürenin tüm iletiler için aynı zamanda başladığını unutmayın, bu nedenle **GetMessages** çağrısından itibaren 5 dakika geçtikten sonra silinmeyen tüm iletiler görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ec060-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="ec060-148">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ec060-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="ec060-149">Kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="ec060-149">Get the queue length</span></span>
<span data-ttu-id="ec060-150">Bir kuyruktaki ileti sayısı ile ilgili bir tahmin alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec060-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="ec060-151">**FetchAttributes** yöntemi, ileti sayısı dahil olmak üzere Kuyruk hizmetinden kuyruk özniteliklerini almasını ister.</span><span class="sxs-lookup"><span data-stu-id="ec060-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="ec060-152">**ApproximateMethodCount** özelliği tarafından alınan en son değeri döndürür **FetchAttributes** kuyruk hizmetini çağırmadan olmadan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ec060-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="ec060-153">Ortak Azure sıra API'leri ile zaman uyumsuz-bekleme yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="ec060-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="ec060-154">Bu örnek nasıl ortak Azure sıra API'leri ile zaman uyumsuz-bekleme yönteminin kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ec060-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="ec060-155">Verilen yöntemlerin her biri zaman uyumsuz sürümü örnek çağırır, bu tarafından görülebilir **zaman uyumsuz** yönteminin her sonrası düzeltme.</span><span class="sxs-lookup"><span data-stu-id="ec060-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="ec060-156">Zaman uyumsuz yöntem kullanıldığında zaman uyumsuz-bekleme düzeni çağrı tamamlanana kadar yerel çalıştırmayı askıya alır.</span><span class="sxs-lookup"><span data-stu-id="ec060-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="ec060-157">Bu davranış geçerli iş parçacığının performans sorunlarını engellemeye yardımcı olmak ve uygulamanızın genel yanıt hızını artırır başka işler yapmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ec060-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="ec060-158">.NET’te Zaman Uyumsuz-Bekleme yönteminin kullanılması ile ilgili daha fazla ayrıntı için bkz. [Zaman Uyumsuz ve Bekleme (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec060-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="ec060-159">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="ec060-159">Delete a queue</span></span>
<span data-ttu-id="ec060-160">Bir kuyruğu ve içinde yer alan tüm iletileri silmek için kuyruk nesnesindeki **Sil** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ec060-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="ec060-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ec060-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

