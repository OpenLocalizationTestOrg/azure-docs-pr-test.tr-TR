---
title: "aaaGet başlatılan .NET kullanarak Azure kuyruk depolamaya | Microsoft Docs"
description: "Azure Queues, uygulama bileşenleri arasında güvenilir ve zaman uyumsuz mesajlaşma sağlar. İleti etkinleştirir, uygulama bileşenleri tooscale bağımsız olarak bulut."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="d5d0e-104">.NET kullanarak Azure Kuyruk Depolamaya başlayın</span><span class="sxs-lookup"><span data-stu-id="d5d0e-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="d5d0e-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d5d0e-105">Overview</span></span>
<span data-ttu-id="d5d0e-106">Azure Queue depolama birimi, uygulama bileşenleri arasında bulut mesajlaşma özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="d5d0e-107">Ölçeklendirmek üzere uygulama tasarlarken, uygulama bileşenleri birbirinden bağımsız şekilde ölçeklenebilmek için genellikle birbirinden ayrılır.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="d5d0e-108">Merhaba bulutta, hello Masaüstü, bir şirket içi sunucu veya bir mobil cihaz çalıştırıp çalıştırmadığınızı uygulama bileşenleri arasında iletişim için zaman uyumsuz Mesajlaşma kuyruk depolama sunar.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="d5d0e-109">Kuyruk depolama ayrıca zaman uyumsuz görevlerin yönetilmesini ve süreç iş akışlarının oluşturulmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="d5d0e-110">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="d5d0e-110">About this tutorial</span></span>
<span data-ttu-id="d5d0e-111">Bu öğretici, nasıl Azure kuyruk depolama kullanarak bazı genel senaryolar için .NET toowrite kodu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="d5d0e-112">Kapsanan senaryolara kuyruk oluşturma ve silme ile kuyruk iletileri ekleme, okuma ve silme dahildir.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="d5d0e-113">**Zaman toocomplete tahmini:** 45 dakika</span><span class="sxs-lookup"><span data-stu-id="d5d0e-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="d5d0e-114">**Önkoşullar:**</span><span class="sxs-lookup"><span data-stu-id="d5d0e-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="d5d0e-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5d0e-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="d5d0e-116">.NET için Azure Depolama İstemcisi</span><span class="sxs-lookup"><span data-stu-id="d5d0e-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="d5d0e-117">.NET için Azure Yapılandırma Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="d5d0e-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="d5d0e-118">Bir [Azure Storage hesabı](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="d5d0e-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="d5d0e-119">Using yönergeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d5d0e-119">Add using directives</span></span>
<span data-ttu-id="d5d0e-120">Merhaba aşağıdakileri ekleyin `using` hello yönergeleri toohello üst `Program.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="d5d0e-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="d5d0e-121">Merhaba bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="d5d0e-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="d5d0e-122">Merhaba kuyruk hizmeti istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5d0e-122">Create hello Queue service client</span></span>
<span data-ttu-id="d5d0e-123">Merhaba **CloudQueueClient** sınıfı, kuyruk depolamada depolanan, tooretrieve sıraları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="d5d0e-124">Tek yönlü toocreate hello hizmeti istemcisi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d5d0e-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="d5d0e-125">Artık veri okuyan ve yazan veri tooQueue depolama hazır toowrite kodu bulunur.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="d5d0e-126">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="d5d0e-126">Create a queue</span></span>
<span data-ttu-id="d5d0e-127">Bu örnekte gösterilir nasıl toocreate zaten yoksa, bir kuyruk:</span><span class="sxs-lookup"><span data-stu-id="d5d0e-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="d5d0e-128">Kuyruğa bir ileti yerleştirme</span><span class="sxs-lookup"><span data-stu-id="d5d0e-128">Insert a message into a queue</span></span>
<span data-ttu-id="d5d0e-129">var olan bir sırayı iletiye tooinsert ilk oluşturma yeni bir **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="d5d0e-130">Ardından, hello'ı çağırın **AddMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="d5d0e-131">**CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir **bayt** dizisinden oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="d5d0e-132">İşte (yoksa), bir kuyruk oluşturur ve eklemeleri selamlama iletisine 'Hello, World' kod:</span><span class="sxs-lookup"><span data-stu-id="d5d0e-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="d5d0e-133">Merhaba sonraki iletiye gözatın</span><span class="sxs-lookup"><span data-stu-id="d5d0e-133">Peek at hello next message</span></span>
<span data-ttu-id="d5d0e-134">Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **PeekMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="d5d0e-135">Merhaba kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="d5d0e-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="d5d0e-136">Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="d5d0e-137">İleti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello iş görevinin durumunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="d5d0e-138">koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve ayarlar görünürlük zaman aşımı tooextend 60 saniye hello.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="d5d0e-139">Bu hello hello ileti ile ilişkili işin durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="d5d0e-140">Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="d5d0e-141">Genellikle, bir yeniden deneme sayısı da tutacak ve hello olursa ileti denenir birden fazla  *n*  kez silmeniz.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="d5d0e-142">Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="d5d0e-143">Merhaba sonraki iletiyi sıradan çıkarmak</span><span class="sxs-lookup"><span data-stu-id="d5d0e-143">De-queue hello next message</span></span>
<span data-ttu-id="d5d0e-144">Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="d5d0e-145">Çağırdığınızda **GetMessage**, hello sonraki iletiyi sıraya alın.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="d5d0e-146">Döndürülen bir ileti **GetMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="d5d0e-147">Varsayılan olarak bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="d5d0e-148">toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="d5d0e-149">Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="d5d0e-150">Kod çağrılarınızı **DeleteMessage** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="d5d0e-151">Genel Kuyruk depolama API’leri ile Zaman Uyumsuz-Bekleme yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="d5d0e-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="d5d0e-152">Bu örnek nasıl toouse hello zaman uyumsuz-bekleme desen genel kuyruk depolama API'leri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="d5d0e-153">Hello örnek hello tarafından belirtildiği şekilde her bir yöntem, verilen hello hello zaman uyumsuz sürümlerini çağırır *zaman uyumsuz* yönteminin her soneki.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="d5d0e-154">Async yöntemi kullanıldığında, zaman uyumsuz hello-bekleme düzeni hello çağrı tamamlanana kadar yerel çalıştırmayı askıya alır.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="d5d0e-155">Bu davranış, performans sorunlarını engellemeye yardımcı olur ve artırır diğer iş hello geçerli iş parçacığı toodo verir Merhaba, uygulamanızın genel yanıt.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="d5d0e-156">Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [zaman uyumsuz ve bekleme (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="d5d0e-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="d5d0e-157">İletilerin kuyruktan çıkarılması için ek seçenekleri kullanma</span><span class="sxs-lookup"><span data-stu-id="d5d0e-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="d5d0e-158">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="d5d0e-159">İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="d5d0e-160">İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="d5d0e-161">Merhaba aşağıdaki kod örneğinde **GetMessages** bir çağrı yöntemi tooget 20 iletileri.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="d5d0e-162">Ardından her ileti bir **foreach** döngüsü ile işlenir.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="d5d0e-163">Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="d5d0e-164">Bu hello 5 dakika Not hello tüm iletileri için aynı başlatıldığında, bunu hello görüşmede çok 5 dakika geçtikten sonra**GetMessages**, silinmemiş tüm iletiler görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="d5d0e-165">Merhaba kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="d5d0e-165">Get hello queue length</span></span>
<span data-ttu-id="d5d0e-166">Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="d5d0e-167">**FetchAttributes** yöntemi hello sıra hizmetinin hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini almasını ister.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="d5d0e-168">Merhaba **ApproximateMessageCount** özelliği tarafından alınan hello son değeri döndürür **FetchAttributes** hello kuyruk hizmetini çağırmadan olmadan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="d5d0e-169">Bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="d5d0e-169">Delete a queue</span></span>
<span data-ttu-id="d5d0e-170">toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **silmek** hello nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="d5d0e-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d5d0e-171">Next steps</span></span>
<span data-ttu-id="d5d0e-172">Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="d5d0e-173">Kullanılabilir API'ler ile ilgili tam Ayrıntılar için Hello kuyruk hizmeti başvuru belgelerini görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="d5d0e-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="d5d0e-174">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="d5d0e-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="d5d0e-175">REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="d5d0e-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="d5d0e-176">Nasıl toosimplify hello kodu yazdığınız öğrenin hello kullanarak Azure Storage ile toowork [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d5d0e-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="d5d0e-177">Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="d5d0e-178">[.NET kullanarak Azure Table storage'ı kullanmaya başlama](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore yapılandırılmış veri.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore structured data.</span></span>
  * <span data-ttu-id="d5d0e-179">[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md) toostore yapılandırılmamış veriler.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="d5d0e-180">[.NET (C#) kullanarak tooSQL veritabanına bağlanma](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore ilişkisel veri.</span><span class="sxs-lookup"><span data-stu-id="d5d0e-180">[Connect tooSQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
