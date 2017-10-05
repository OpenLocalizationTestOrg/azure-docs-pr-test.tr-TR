---
title: Kuyruk depolama (C++) kullanma | Microsoft Docs
description: "Azure kuyruk depolama hizmetini kullanmayı öğrenin. C++'ta örnekleri yazılır."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: 5e81d5e0af9871099b7f921f355cf94249e4d30c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="dd7e0-104">C++ içinden kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="dd7e0-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="dd7e0-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="dd7e0-105">Overview</span></span>
<span data-ttu-id="dd7e0-106">Bu kılavuz Azure kuyruk depolama hizmeti kullanılarak yaygın senaryolar gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="dd7e0-107">C++ ve kullanım örnekleri yazılır [C++ için Azure Storage istemci Kitaplığı](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="dd7e0-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="dd7e0-108">Kapsamdaki senaryolar dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı **oluşturma ve silme**.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="dd7e0-109">Bu kılavuz, c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hedefler.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="dd7e0-110">Aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, önerilen sürümüdür [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="dd7e0-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="dd7e0-111">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd7e0-111">Create a C++ application</span></span>
<span data-ttu-id="dd7e0-112">Bu kılavuzda, C++ uygulamasında çalıştırabileceğiniz depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="dd7e0-113">Bunu yapmak için Azure Storage istemci kitaplığı C++ için yükleme ve Azure aboneliğinizde bir Azure depolama hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="dd7e0-114">C++ için Azure Storage istemci kitaplığı yüklemek için aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd7e0-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="dd7e0-115">**Linux:** verilen yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="dd7e0-116">**Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="dd7e0-117">Aşağıdaki komutu yazın [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="dd7e0-118">Kuyruk depolama erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dd7e0-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="dd7e0-119">Azure depolama API'leri sıraları erişmek için kullanmasını istediğiniz C++ dosyanın en üstüne deyimlerini şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dd7e0-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="dd7e0-120">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="dd7e0-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="dd7e0-121">Bir Azure storage istemci uç noktaları ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgilerini depolamak için bir depolama bağlantı dizesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="dd7e0-122">Bir istemci uygulamasında çalıştırırken, depolama hesabı altında listelenen için adını depolama hesabınız ve depolama erişim tuşunu kullanarak depolama bağlantı dizesi şu biçimde sağlamalısınız [Azure Portal](https://portal.azure.com) için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="dd7e0-123">Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure Storage hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd7e0-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="dd7e0-124">Bu örnek, bağlantı dizesi tutmak için statik bir alana nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="dd7e0-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="dd7e0-125">Yerel Windows bilgisayarınızda uygulamanızı test etmek için Microsoft Azure kullanabilirsiniz [depolama öykünücüsü](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) ile yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dd7e0-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="dd7e0-126">Depolama öykünücüsü Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde Azure'da kullanılabilir benzetim yapan bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="dd7e0-127">Aşağıdaki örnek, yerel depolama öykünücüsü için bağlantı dizesi tutmak için statik bir alana nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="dd7e0-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="dd7e0-128">Azure storage öykünücüsü başlatmak için **Başlat** düğmesini veya tuşuna **Windows** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="dd7e0-129">Yazmaya başlayın **Azure Storage öykünücüsü**seçip **Microsoft Azure Storage öykünücüsü** uygulamalar listesinden.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="dd7e0-130">Aşağıdaki örnekler, bu iki yöntemden birini depolama bağlantı dizesini almak için kullanılan olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="dd7e0-131">Bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="dd7e0-131">Retrieve your connection string</span></span>
<span data-ttu-id="dd7e0-132">Kullanabileceğiniz **cloud_storage_account** depolama hesabı bilgileri temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="dd7e0-133">Depolama bağlantı dizesi, depolama hesabı bilgilerini almak için kullanabileceğiniz **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="dd7e0-134">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="dd7e0-134">How to: Create a queue</span></span>
<span data-ttu-id="dd7e0-135">A **cloud_queue_client** nesne başvuru nesneleri için kuyrukları almak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="dd7e0-136">Aşağıdaki kod oluşturur bir **cloud_queue_client** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="dd7e0-137">Kullanmak **cloud_queue_client** kullanmak istediğiniz kuyruğuna başvuru nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="dd7e0-138">Yoksa, kuyruk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="dd7e0-139">Nasıl yapılır: bir sıraya bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="dd7e0-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="dd7e0-140">Varolan bir sıraya bir ileti eklemek için ilk olarak yeni bir oluşturma **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="dd7e0-141">Ardından, çağrı **add_message** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="dd7e0-142">A **cloud_queue_message** herhangi birinden bir dize oluşturulabilir veya **bayt** dizi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="dd7e0-143">Burada, bir kuyruk oluşturan (eğer yoksa) ve 'Hello, World' iletisini yerleştiren bir kod yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="dd7e0-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="dd7e0-144">Nasıl yapılır: sonraki iletiye</span><span class="sxs-lookup"><span data-stu-id="dd7e0-144">How to: Peek at the next message</span></span>
<span data-ttu-id="dd7e0-145">Kuyruğun önündeki iletiye sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **peek_message** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="dd7e0-146">Nasıl yapılır: kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="dd7e0-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="dd7e0-147">Kuyrukta yer alan bir iletinin içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="dd7e0-148">Eğer ileti bir iş görevini temsil ediyorsa, bu özelliği kullanarak iş görevinin durumunu güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="dd7e0-149">Aşağıdaki kod kuyruk iletisini yeni içeriklerle güncelleştirir ve görünürlük zaman aşımını 60 saniye daha uzatır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="dd7e0-150">Bu, ileti ile ilişkili işin durumunu kaydeder ve istemciye ileti üzerinde çalışmaya devam etmesi için bir dakika daha zaman verir.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="dd7e0-151">Bir işleme adımı donanım veya yazılım arızasından dolayı başarısız olursa baştan başlamanıza gerek kalmadan kuyruk iletilerindeki çok adımlı iş akışlarını izlemek için bu yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="dd7e0-152">Genellikle, bir yeniden deneme sayısı da tutacak ve ileti birden fazla n kez denenirse, silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="dd7e0-153">Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="dd7e0-154">Nasıl yapılır: sonraki iletiyi sıradan çıkarmak</span><span class="sxs-lookup"><span data-stu-id="dd7e0-154">How to: De-queue the next message</span></span>
<span data-ttu-id="dd7e0-155">Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="dd7e0-156">Çağırdığınızda **get_message**, sonraki iletiyi sıraya alın.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="dd7e0-157">Döndürülen bir ileti **get_message** iletileri bu sıradan okuyan herhangi bir kod görünmez olur.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="dd7e0-158">İletiyi kuyruktan kaldırmayı tamamlamak için de çağırmanız gerekir **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="dd7e0-159">Bir iletinin iki adımlı kaldırılma süreci, donanım veya yazılım arızasından dolayı kodunuzun bir iletiyi işleyememesi durumunda kodunuzun başka bir örneğinin aynı iletiyi alıp yeniden denemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="dd7e0-160">Kod çağrılarınızı **delete_message** ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="dd7e0-161">Nasıl yapılır: yararlanan çıkarılması iletileri için ek seçenekleri</span><span class="sxs-lookup"><span data-stu-id="dd7e0-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="dd7e0-162">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="dd7e0-163">İlk olarak toplu iletiler alabilirsiniz (en fazla 32).</span><span class="sxs-lookup"><span data-stu-id="dd7e0-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="dd7e0-164">İkinci olarak daha uzun veya daha kısa bir görünmezlik süresi ayarlayarak kodunuzun her iletiyi tamamen işlemesi için daha az veya daha fazla zaman tanıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="dd7e0-165">Aşağıdaki kod örneğinde **get_messages** tek çağrıda 20 ileti almak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="dd7e0-166">Her bir iletiyi kullanarak işler sonra bir **için** döngü.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="dd7e0-167">Ayrıca her ileti için görünmezlik zaman aşımı beş dakika olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="dd7e0-168">5 dakikalık sürenin tüm iletiler için aynı anda Not böylece sonra 5 dakika geçirilen çağrısından sonra **get_messages**, silinmemiş tüm iletiler görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="dd7e0-169">Nasıl yapılır: kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="dd7e0-169">How to: Get the queue length</span></span>
<span data-ttu-id="dd7e0-170">Bir kuyruktaki ileti sayısı ile ilgili bir tahmin alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="dd7e0-171">**Download_attributes** yöntemi kuyruk hizmeti ileti sayısı dahil olmak üzere kuyruk özniteliklerini almasını ister.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="dd7e0-172">**Approximate_message_count** yöntemi kuyrukta yaklaşık iletilerin sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="dd7e0-173">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="dd7e0-173">How to: Delete a queue</span></span>
<span data-ttu-id="dd7e0-174">Bir kuyruk ve içerdiği tüm iletileri silmek için arama **delete_queue_if_exists** nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="dd7e0-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd7e0-175">Next steps</span></span>
<span data-ttu-id="dd7e0-176">Kuyruk depolamanın temellerini öğrendiğinize göre Azure Storage hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="dd7e0-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="dd7e0-177">C++ içinden BLOB Storage kullanma</span><span class="sxs-lookup"><span data-stu-id="dd7e0-177">How to use Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="dd7e0-178">Tablo depolama C++ içinden kullanma</span><span class="sxs-lookup"><span data-stu-id="dd7e0-178">How to use Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="dd7e0-179">C++'ta listesi Azure Storage kaynakları</span><span class="sxs-lookup"><span data-stu-id="dd7e0-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="dd7e0-180">C++ başvurusu için depolama istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="dd7e0-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="dd7e0-181">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="dd7e0-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)