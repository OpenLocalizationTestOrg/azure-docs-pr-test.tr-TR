---
title: Java'dan kuyruk depolama aaaHow toouse | Microsoft Docs
description: "Nasıl toouse hello Azure kuyruk hizmeti toocreate ve delete kuyruklar ve Ekle, Al ve iletileri silmek öğrenin. Java'da yazılmış örneklerini içerir."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 297f89c9d21a38d2b4a5f4346f66f59f9d487010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="30936-104">Nasıl toouse Java'dan kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="30936-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="30936-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="30936-105">Overview</span></span>
<span data-ttu-id="30936-106">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="30936-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="30936-107">Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure depolama SDK'sı][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="30936-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="30936-108">Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma** ve **silme** sıralar.</span><span class="sxs-lookup"><span data-stu-id="30936-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="30936-109">Merhaba kuyruklar hakkında daha fazla bilgi için bkz: [sonraki adımlar](#Next-Steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="30936-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="30936-110">Not: Bir SDK'sı Android cihazlarda Azure depolama kullanan geliştiriciler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="30936-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="30936-111">Daha fazla bilgi için bkz: Merhaba [Android için Azure depolama SDK'sı][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="30936-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="30936-112">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="30936-112">Create a Java application</span></span>
<span data-ttu-id="30936-113">Bu kılavuzda, bir Java uygulaması içinde yerel olarak veya bir web rolü veya Azure çalışan rolünde çalışan kodu çalıştırılabilir depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="30936-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="30936-114">toodo tooinstall ihtiyacınız olacak şekilde, Java Geliştirme Seti (JDK) hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30936-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="30936-115">Bunu yaptıktan sonra geliştirme sisteminizde hello en düşük gereksinimleri ve hello listelenen bağımlılıkları karşılayan tooverify gerekir [Java için Azure depolama SDK'sı] [ Azure Storage SDK for Java] github'daki.</span><span class="sxs-lookup"><span data-stu-id="30936-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="30936-116">Sisteminiz bu gereksinimleri karşılıyorsa, karşıdan yükleme ve bu depodan sisteminizdeki Java için hello Azure depolama kitaplıkları için hello yönergeleri izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="30936-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="30936-117">Bu görevleri tamamladıktan sonra mümkün toocreate hello örnekleri bu makalede kullanan bir Java uygulaması olacaktır.</span><span class="sxs-lookup"><span data-stu-id="30936-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="30936-118">Uygulama tooaccess kuyruk depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="30936-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="30936-119">İçeri aktarma deyimlerini toohello dosyasının üst kısmında toouse Azure depolama API'leri tooaccess sıraları istediğiniz hello Java aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="30936-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="30936-120">Bir Azure depolama bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="30936-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="30936-121">Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="30936-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="30936-122">Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello depolama hesabınızın adını kullanarak hello olarak sağlamak ve hello listelenen hello depolama hesabı için birincil erişim anahtarını hello gerekir [Azure Portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="30936-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="30936-123">Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="30936-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="30936-124">Çalışan bir uygulama içinde Microsoft Azure rolünde içinde bu dize hello hizmet yapılandırma dosyasında depolanabilir *ServiceConfiguration.cscfg*ve bir çağrı toohello ile erişilebilir  **RoleEnvironment.getConfigurationSettings** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="30936-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="30936-125">Merhaba bağlantı dizesinden alma örneği bir **ayarı** adlı öğe *StorageConnectionString* hello hizmet yapılandırma dosyasında:</span><span class="sxs-lookup"><span data-stu-id="30936-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="30936-126">Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="30936-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="30936-127">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="30936-127">How to: Create a queue</span></span>
<span data-ttu-id="30936-128">A **CloudQueueClient** nesne başvuru nesneleri için kuyrukları almak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="30936-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="30936-129">Merhaba aşağıdaki kod oluşturur bir **CloudQueueClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="30936-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="30936-130">(Not: ek yolları toocreate vardır **CloudStorageAccount** nesneleri; daha fazla bilgi için bkz: **CloudStorageAccount** hello içinde [Azure Storage istemci SDK'sı başvurusu].)</span><span class="sxs-lookup"><span data-stu-id="30936-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="30936-131">Kullanım hello **CloudQueueClient** tooget toouse istediğiniz bir başvuru toohello sıra nesnesi.</span><span class="sxs-lookup"><span data-stu-id="30936-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="30936-132">Yoksa, hello kuyruk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30936-132">You can create hello queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="30936-133">Nasıl yapılır: bir ileti tooa sırası Ekle</span><span class="sxs-lookup"><span data-stu-id="30936-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="30936-134">var olan bir sırayı iletiye tooinsert ilk oluşturma yeni bir **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="30936-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="30936-135">Ardından, hello'ı çağırın **addMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="30936-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="30936-136">A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="30936-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="30936-137">İşte (yoksa), bir kuyruk oluşturur ve eklemeleri selamlama iletisine "Hello, World" kod.</span><span class="sxs-lookup"><span data-stu-id="30936-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="30936-138">Nasıl yapılır: hello sonraki iletiye gözatın</span><span class="sxs-lookup"><span data-stu-id="30936-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="30936-139">Bir sıra Merhaba öne hello iletiye hello sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="30936-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="30936-140">Nasıl yapılır: hello kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="30936-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="30936-141">Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30936-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="30936-142">Merhaba ileti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello durumu hello iş görevi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30936-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="30936-143">koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve ayarlar görünürlük zaman aşımı tooextend 60 saniye hello.</span><span class="sxs-lookup"><span data-stu-id="30936-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="30936-144">Bu hello hello ileti ile ilişkili işin durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar.</span><span class="sxs-lookup"><span data-stu-id="30936-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="30936-145">Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30936-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="30936-146">Genellikle, bir yeniden deneme sayısı da tutacak ve hello olursa ileti denenir birden fazla  *n*  kez silmeniz.</span><span class="sxs-lookup"><span data-stu-id="30936-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="30936-147">Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="30936-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="30936-148">Merhaba aşağıdaki örnek aramalar hello iletileri kuyruğunu aracılığıyla kod, "Hello, World" Merhaba içerik için eşleşen sonra selamlama iletisine içerik değiştirir ve çıkar hello ilk iletiyi bulur.</span><span class="sxs-lookup"><span data-stu-id="30936-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="30936-149">Alternatif olarak, hello aşağıdaki kod örneği yalnızca hello ilk görünür ileti hello sırasına güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="30936-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="30936-150">Nasıl yapılır: hello kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="30936-150">How to: Get hello queue length</span></span>
<span data-ttu-id="30936-151">Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30936-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="30936-152">Merhaba **downloadAttributes** kaç iletiler bir kuyrukta olan sayısına dahil yöntemi çeşitli geçerli değerler için hello sıra hizmeti sorar.</span><span class="sxs-lookup"><span data-stu-id="30936-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="30936-153">iletileri eklenen veya hello sıra hizmeti tooyour isteği yanıtlar sonra kaldırıldığı için hello yalnızca yaklaşık sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="30936-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="30936-154">Merhaba **getApproximateMessageCount** yöntemi çok hello çağrısı tarafından alınan hello son değeri döndürür**downloadAttributes**, hello kuyruk hizmetini çağırmadan olmadan.</span><span class="sxs-lookup"><span data-stu-id="30936-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="30936-155">Nasıl yapılır: hello sonraki iletiyi sıradan çıkarma</span><span class="sxs-lookup"><span data-stu-id="30936-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="30936-156">Kodunuzun bir iletiyi bir kuyruktan iki adımda dequeues.</span><span class="sxs-lookup"><span data-stu-id="30936-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="30936-157">Çağırdığınızda **retrieveMessage**, hello sonraki iletiyi sıraya alın.</span><span class="sxs-lookup"><span data-stu-id="30936-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="30936-158">Döndürülen bir ileti **retrieveMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="30936-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="30936-159">Varsayılan olarak bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="30936-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="30936-160">toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="30936-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="30936-161">Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="30936-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="30936-162">Kod çağrılarınızı **deleteMessage** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="30936-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="30936-163">İletilerin kuyruktan alma için ek seçenekleri</span><span class="sxs-lookup"><span data-stu-id="30936-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="30936-164">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30936-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="30936-165">İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30936-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="30936-166">İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="30936-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="30936-167">Merhaba aşağıdaki kod örneği kullanır hello **retrieveMessages** bir çağrı yöntemi tooget 20 iletileri.</span><span class="sxs-lookup"><span data-stu-id="30936-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="30936-168">Her bir iletiyi kullanarak işler sonra bir **için** döngü.</span><span class="sxs-lookup"><span data-stu-id="30936-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="30936-169">Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika (300 saniye cinsinden) ayarlar.</span><span class="sxs-lookup"><span data-stu-id="30936-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="30936-170">Bu hello beş dakika başlatıldığında tüm not iletileri hello aynı zaman, bunu beş dakika hello görüşmede çok geçtiğinde**retrieveMessages**, silinmemiş tüm iletiler görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="30936-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="30936-171">Nasıl yapılır: liste hello sıraları</span><span class="sxs-lookup"><span data-stu-id="30936-171">How to: List hello queues</span></span>
<span data-ttu-id="30936-172">tooobtain hello geçerli kuyrukların, çağrı hello listesini **CloudQueueClient.listQueues()** koleksiyonunu döndürür yöntemi **CloudQueue** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="30936-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="30936-173">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="30936-173">How to: Delete a queue</span></span>
<span data-ttu-id="30936-174">toodelete bir sıra ve tüm karışılama iletileri bulunan, içinde arama hello **deleteIfExists** hello yöntemi **CloudQueue** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="30936-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="30936-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30936-175">Next steps</span></span>
<span data-ttu-id="30936-176">Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.</span><span class="sxs-lookup"><span data-stu-id="30936-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="30936-177">[Azure depolama için Java SDK'sı][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="30936-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="30936-178">[Azure Storage istemci SDK'sı başvurusu][Azure Storage istemci SDK'sı başvurusu]</span><span class="sxs-lookup"><span data-stu-id="30936-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="30936-179">[Azure Storage Hizmetleri REST API'si][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="30936-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="30936-180">[Azure depolama ekibi blogu][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="30936-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage istemci SDK'sı başvurusu]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
