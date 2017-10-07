---
title: aaaHow toouse kuyruk depolama (C++) | Microsoft Docs
description: "Nasıl toouse hello Azure kuyruk depolama hizmetinde öğrenin. C++'ta örnekleri yazılır."
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
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="eb24a-104">Nasıl toouse C++ içinden kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="eb24a-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="eb24a-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="eb24a-105">Overview</span></span>
<span data-ttu-id="eb24a-106">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="eb24a-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="eb24a-107">Merhaba örnekleri C++ ile yazılmış ve hello kullan [C++ için Azure Storage istemci Kitaplığı](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="eb24a-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="eb24a-108">Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**.</span><span class="sxs-lookup"><span data-stu-id="eb24a-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="eb24a-109">Bu kılavuzu hedefleri c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hello.</span><span class="sxs-lookup"><span data-stu-id="eb24a-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="eb24a-110">Merhaba önerilir sürümü aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="eb24a-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="eb24a-111">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb24a-111">Create a C++ application</span></span>
<span data-ttu-id="eb24a-112">Bu kılavuzda, C++ uygulamasında çalıştırabileceğiniz depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="eb24a-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="eb24a-113">toodo tooinstall ihtiyacınız olacak şekilde, C++ için Azure Storage istemci kitaplığı hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eb24a-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="eb24a-114">tooinstall hello Azure Storage istemci kitaplığı C++ için hello aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb24a-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="eb24a-115">**Linux:** hello verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="eb24a-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="eb24a-116">**Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="eb24a-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="eb24a-117">Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eb24a-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="eb24a-118">Uygulama tooaccess kuyruk depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eb24a-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="eb24a-119">Deyimleri toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess sıraları istediğiniz hello C++ Hello şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="eb24a-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="eb24a-120">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="eb24a-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="eb24a-121">Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="eb24a-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="eb24a-122">Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello listelenen hello depolama hesabı için depolama hesabı ve hello depolama erişim anahtarınızı hello adını kullanarak hello olarak sağlamalısınız [Azure Portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="eb24a-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="eb24a-123">Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure Storage hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb24a-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="eb24a-124">Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="eb24a-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="eb24a-125">tootest uygulamanızı yerel Windows bilgisayarınızda, Microsoft Azure hello kullanabilirsiniz [depolama öykünücüsü](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) ile Merhaba yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="eb24a-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="eb24a-126">Merhaba depolama öykünücüsü hello Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde Azure'da kullanılabilir benzetim yapan bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="eb24a-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="eb24a-127">Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesi tooyour yerel depolama öykünücüsü nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="eb24a-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="eb24a-128">toostart hello Azure storage öykünücüsü, select hello **Başlat** düğmesini veya tuşuna hello **Windows** anahtarı.</span><span class="sxs-lookup"><span data-stu-id="eb24a-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="eb24a-129">Yazmaya başlayın **Azure Storage öykünücüsü**seçip **Microsoft Azure Storage öykünücüsü** uygulamaları hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="eb24a-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="eb24a-130">Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="eb24a-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="eb24a-131">Bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="eb24a-131">Retrieve your connection string</span></span>
<span data-ttu-id="eb24a-132">Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesabı bilgilerinizi sınıfı.</span><span class="sxs-lookup"><span data-stu-id="eb24a-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="eb24a-133">tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello kullanabilirsiniz **ayrıştırma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="eb24a-134">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="eb24a-134">How to: Create a queue</span></span>
<span data-ttu-id="eb24a-135">A **cloud_queue_client** nesne başvuru nesneleri için kuyrukları almak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb24a-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="eb24a-136">Merhaba aşağıdaki kod oluşturur bir **cloud_queue_client** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="eb24a-137">Kullanım hello **cloud_queue_client** tooget toouse istediğiniz bir başvuru toohello sıra nesnesi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="eb24a-138">Yoksa, hello kuyruk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="eb24a-139">Nasıl yapılır: bir sıraya bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="eb24a-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="eb24a-140">var olan bir sırayı iletiye tooinsert ilk oluşturma yeni bir **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="eb24a-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="eb24a-141">Ardından, hello'ı çağırın **add_message** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="eb24a-142">A **cloud_queue_message** herhangi birinden bir dize oluşturulabilir veya **bayt** dizi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="eb24a-143">İşte (yoksa), bir kuyruk oluşturur ve eklemeleri selamlama iletisine 'Hello, World' kod:</span><span class="sxs-lookup"><span data-stu-id="eb24a-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="eb24a-144">Nasıl yapılır: hello sonraki iletiye gözatın</span><span class="sxs-lookup"><span data-stu-id="eb24a-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="eb24a-145">Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **peek_message** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="eb24a-146">Nasıl yapılır: hello kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="eb24a-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="eb24a-147">Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="eb24a-148">Merhaba ileti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello durumu hello iş görevi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="eb24a-149">koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve ayarlar görünürlük zaman aşımı tooextend 60 saniye hello.</span><span class="sxs-lookup"><span data-stu-id="eb24a-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="eb24a-150">Bu hello hello ileti ile ilişkili işin durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb24a-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="eb24a-151">Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="eb24a-152">Genellikle, bir yeniden deneme sayısı da tutacak ve selamlama iletisine n birden fazla kez denenirse, silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="eb24a-153">Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb24a-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="eb24a-154">Nasıl yapılır: hello sonraki iletiyi sıradan çıkarmak</span><span class="sxs-lookup"><span data-stu-id="eb24a-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="eb24a-155">Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır.</span><span class="sxs-lookup"><span data-stu-id="eb24a-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="eb24a-156">Çağırdığınızda **get_message**, hello sonraki iletiyi sıraya alın.</span><span class="sxs-lookup"><span data-stu-id="eb24a-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="eb24a-157">Döndürülen bir ileti **get_message** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="eb24a-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="eb24a-158">toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="eb24a-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="eb24a-159">Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb24a-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="eb24a-160">Kod çağrılarınızı **delete_message** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="eb24a-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="eb24a-161">Nasıl yapılır: yararlanan çıkarılması iletileri için ek seçenekleri</span><span class="sxs-lookup"><span data-stu-id="eb24a-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="eb24a-162">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="eb24a-163">İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="eb24a-164">İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="eb24a-165">Merhaba aşağıdaki kod örneği kullanır hello **get_messages** bir çağrı yöntemi tooget 20 iletileri.</span><span class="sxs-lookup"><span data-stu-id="eb24a-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="eb24a-166">Her bir iletiyi kullanarak işler sonra bir **için** döngü.</span><span class="sxs-lookup"><span data-stu-id="eb24a-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="eb24a-167">Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar.</span><span class="sxs-lookup"><span data-stu-id="eb24a-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="eb24a-168">Bu hello 5 dakika Not hello tüm iletileri için aynı başlatıldığında, bunu hello görüşmede çok 5 dakika geçtikten sonra**get_messages**, silinmemiş tüm iletiler görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="eb24a-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="eb24a-169">Nasıl yapılır: hello kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="eb24a-169">How to: Get hello queue length</span></span>
<span data-ttu-id="eb24a-170">Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb24a-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="eb24a-171">Merhaba **download_attributes** yöntemi hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini hello kuyruk hizmeti tooretrieve sorar.</span><span class="sxs-lookup"><span data-stu-id="eb24a-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="eb24a-172">Merhaba **approximate_message_count** yöntemi hello sırada hello yaklaşık iletilerin sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="eb24a-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="eb24a-173">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="eb24a-173">How to: Delete a queue</span></span>
<span data-ttu-id="eb24a-174">bir kuyruk ve tüm karışılama iletileri bulunan, içinde arama hello toodelete **delete_queue_if_exists** hello nesnesinde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eb24a-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="eb24a-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb24a-175">Next steps</span></span>
<span data-ttu-id="eb24a-176">Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre Azure Storage hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="eb24a-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="eb24a-177">Nasıl toouse Blob depolama alanından C++</span><span class="sxs-lookup"><span data-stu-id="eb24a-177">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="eb24a-178">Nasıl toouse C++ tablo depolamasından</span><span class="sxs-lookup"><span data-stu-id="eb24a-178">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="eb24a-179">C++'ta listesi Azure Storage kaynakları</span><span class="sxs-lookup"><span data-stu-id="eb24a-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="eb24a-180">C++ başvurusu için depolama istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="eb24a-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="eb24a-181">Azure Depolama Belgeleri</span><span class="sxs-lookup"><span data-stu-id="eb24a-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)