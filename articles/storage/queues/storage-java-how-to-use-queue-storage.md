---
title: Java'dan kuyruk depolama kullanma | Microsoft Docs
description: "Oluşturmak ve Kuyruklar silmek için Azure Queue hizmetini kullanmayı öğrenin ve Ekle, Al ve iletilerini silin. Java'da yazılmış örneklerini içerir."
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
ms.openlocfilehash: a56b345c5efb4ce9c8ee2da91b798d09d44e42be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-java"></a><span data-ttu-id="dbc8f-104">Java’dan Kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="dbc8f-104">How to use Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="dbc8f-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="dbc8f-105">Overview</span></span>
<span data-ttu-id="dbc8f-106">Bu kılavuz Azure kuyruk depolama hizmeti kullanılarak yaygın senaryolar gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="dbc8f-107">Java ve kullanım örnekleri yazılır [Java için Azure depolama SDK'sı][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="dbc8f-107">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="dbc8f-108">Kapsamdaki senaryolar dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma** ve **silme** sıralar.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="dbc8f-109">Kuyruklar hakkında daha fazla bilgi için bkz: [sonraki adımlar](#Next-Steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-109">For more information on queues, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="dbc8f-110">Not: Bir SDK'sı Android cihazlarda Azure depolama kullanan geliştiriciler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="dbc8f-111">Daha fazla bilgi için bkz: [Android için Azure depolama SDK'sı][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="dbc8f-111">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="dbc8f-112">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="dbc8f-112">Create a Java application</span></span>
<span data-ttu-id="dbc8f-113">Bu kılavuzda, bir Java uygulaması içinde yerel olarak veya bir web rolü veya Azure çalışan rolünde çalışan kodu çalıştırılabilir depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="dbc8f-114">Bunu yapmak için Java Geliştirme Seti (JDK) yükleyin ve Azure aboneliğinizde bir Azure depolama hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-114">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="dbc8f-115">Bunu yaptıktan sonra geliştirme sisteminizde içinde listelenen bağımlılıkları ve en düşük gereksinimleri karşıladığını doğrulamanız gerekir [Java için Azure depolama SDK'sı] [ Azure Storage SDK for Java] github'daki.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-115">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="dbc8f-116">Sisteminiz bu gereksinimleri karşılıyorsa, indirme ve bu depodan sisteminizdeki Java için Azure depolama kitaplıkları yükleme yönergelerini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-116">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="dbc8f-117">Bu görevleri tamamladığınızda, bu makaledeki örnekler kullanan bir Java uygulaması oluşturmak mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-117">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="dbc8f-118">Kuyruk depolama erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dbc8f-118">Configure your application to access queue storage</span></span>
<span data-ttu-id="dbc8f-119">Aşağıdaki içeri aktarma deyimlerini Azure depolama API'leri sıraları erişmek için kullanmasını istediğiniz Java dosyasının üstüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dbc8f-119">Add the following import statements to the top of the Java file where you want to use Azure storage APIs to access queues:</span></span>

```java
// Include the following imports to use queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="dbc8f-120">Bir Azure depolama bağlantı dizesini ayarlayın</span><span class="sxs-lookup"><span data-stu-id="dbc8f-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="dbc8f-121">Bir Azure storage istemci uç noktaları ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgilerini depolamak için bir depolama bağlantı dizesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="dbc8f-122">Bir istemci uygulamasında çalıştırırken, depolama hesabınızın adını kullanarak depolama bağlantı dizesi şu biçimde sağlamanız gerekir ve depolama hesabı için birincil erişim anahtarını listelenen [Azure Portal](https://portal.azure.com) için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="dbc8f-123">Bu örnek, bağlantı dizesi tutmak için statik bir alana nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="dbc8f-123">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="dbc8f-124">Çalışan bir uygulama içinde Microsoft Azure rolünde içinde bu dize hizmet yapılandırma dosyasında depolanabilir *ServiceConfiguration.cscfg*ve çağrısıyla erişilebilir **RoleEnvironment.getConfigurationSettings** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-124">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="dbc8f-125">Bağlantı dizesi alma örneği bir **ayarı** adlı öğe *StorageConnectionString* hizmet yapılandırma dosyasında:</span><span class="sxs-lookup"><span data-stu-id="dbc8f-125">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="dbc8f-126">Aşağıdaki örnekler, bu iki yöntemden birini depolama bağlantı dizesini almak için kullanılan olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-126">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="dbc8f-127">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="dbc8f-127">How to: Create a queue</span></span>
<span data-ttu-id="dbc8f-128">A **CloudQueueClient** nesne başvuru nesneleri için kuyrukları almak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="dbc8f-129">Aşağıdaki kod oluşturur bir **CloudQueueClient** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-129">The following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="dbc8f-130">(Not: oluşturmak için ek yol vardır **CloudStorageAccount** nesneleri; daha fazla bilgi için bkz: **CloudStorageAccount** içinde [Azure Storage istemci SDK'sı başvurusu].)</span><span class="sxs-lookup"><span data-stu-id="dbc8f-130">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="dbc8f-131">Kullanmak **CloudQueueClient** kullanmak istediğiniz kuyruğuna başvuru nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-131">Use the **CloudQueueClient** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="dbc8f-132">Yoksa, kuyruk oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-132">You can create the queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create the queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference to a queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create the queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-to-a-queue"></a><span data-ttu-id="dbc8f-133">Nasıl yapılır: bir sıraya bir ileti ekleyin</span><span class="sxs-lookup"><span data-stu-id="dbc8f-133">How to: Add a message to a queue</span></span>
<span data-ttu-id="dbc8f-134">Varolan bir sıraya bir ileti yerleştirmek için ilk olarak yeni bir **CloudQueueMessage** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-134">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="dbc8f-135">Ardından, çağrı **addMessage** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-135">Next, call the **addMessage** method.</span></span> <span data-ttu-id="dbc8f-136">A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="dbc8f-137">Burada kodudur (yoksa), bir kuyruk oluşturur ve "Hello, World" iletisini ekler.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-137">Here is code which creates a queue (if it doesn't exist) and inserts the message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create the queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="dbc8f-138">Nasıl yapılır: sonraki iletiye</span><span class="sxs-lookup"><span data-stu-id="dbc8f-138">How to: Peek at the next message</span></span>
<span data-ttu-id="dbc8f-139">Kuyruğun önündeki iletiye sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-139">You can peek at the message in the front of a queue without removing it from the queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at the next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output the message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="dbc8f-140">Nasıl yapılır: kuyruğa alınan iletinin içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="dbc8f-140">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="dbc8f-141">Kuyrukta yer alan bir iletinin içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-141">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="dbc8f-142">Eğer ileti bir iş görevini temsil ediyorsa, bu özelliği kullanarak iş görevinin durumunu güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-142">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="dbc8f-143">Aşağıdaki kod kuyruk iletisini yeni içeriklerle güncelleştirir ve görünürlük zaman aşımını 60 saniye daha uzatır.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-143">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="dbc8f-144">Bu, ileti ile ilişkili işin durumunu kaydeder ve istemciye ileti üzerinde çalışmaya devam etmesi için bir dakika daha zaman verir.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-144">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="dbc8f-145">Bir işleme adımı donanım veya yazılım arızasından dolayı başarısız olursa baştan başlamanıza gerek kalmadan kuyruk iletilerindeki çok adımlı iş akışlarını izlemek için bu yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-145">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="dbc8f-146">Genellikle bir yeniden deneme sayacı tutmanı gerekir ve bir ileti *n* seferden daha fazla yeniden denenirse, silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-146">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="dbc8f-147">Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="dbc8f-148">Aşağıdaki kod örnek aramalar ileti sırası içeriği için "Hello, World" eşleşen sonra içerik ileti değiştirir ve çıkar ilk iletiyi bulur.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-148">The following code sample searches through the queue of messages, locates the first message that matches "Hello, World" for the content, then modifies the message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // The maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through the messages in the queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify the content of the first matching message.
            message.setMessageContent("Updated contents.");
            // Set it to be visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update the message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="dbc8f-149">Alternatif olarak, aşağıdaki kod örneği yalnızca ilk görünür ileti sırasına güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-149">Alternatively, the following code sample updates just the first visible message on the queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify the message content.
        message.setMessageContent("Updated contents.");
        // Set it to be visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update the message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="dbc8f-150">Nasıl yapılır: kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="dbc8f-150">How to: Get the queue length</span></span>
<span data-ttu-id="dbc8f-151">Bir kuyruktaki ileti sayısı ile ilgili bir tahmin alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-151">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="dbc8f-152">**DownloadAttributes** kaç iletiler bir kuyrukta olan sayısına dahil yöntemi çeşitli geçerli değerler için sıra hizmeti sorar.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-152">The **downloadAttributes** method asks the Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="dbc8f-153">İletileri eklenen veya sıra hizmeti isteğinize yanıt sonra kaldırıldığı için yalnızca yaklaşık sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-153">The count is only approximate because messages can be added or removed after the Queue service responds to your request.</span></span> <span data-ttu-id="dbc8f-154">**GetApproximateMessageCount** yöntem çağrısı tarafından alınan en son değeri döndürür **downloadAttributes**, kuyruk hizmetini çağırmadan olmadan.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-154">The **getApproximateMessageCount** method returns the last value retrieved by the call to **downloadAttributes**, without calling the Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download the approximate message count from the server.
    queue.downloadAttributes();

    // Retrieve the newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display the queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="dbc8f-155">Nasıl yapılır: sonraki iletiyi sıradan çıkarma</span><span class="sxs-lookup"><span data-stu-id="dbc8f-155">How to: Dequeue the next message</span></span>
<span data-ttu-id="dbc8f-156">Kodunuzun bir iletiyi bir kuyruktan iki adımda dequeues.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="dbc8f-157">Çağırdığınızda **retrieveMessage**, sonraki iletiyi sıraya alın.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-157">When you call **retrieveMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="dbc8f-158">Döndürülen bir ileti **retrieveMessage** iletileri bu sıradan okuyan herhangi bir kod görünmez olur.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-158">A message returned from **retrieveMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="dbc8f-159">Varsayılan olarak bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="dbc8f-160">İletiyi kuyruktan kaldırmayı tamamlamak için de çağırmanız gerekir **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-160">To finish removing the message from the queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="dbc8f-161">Bir iletinin iki adımlı kaldırılma süreci, donanım veya yazılım arızasından dolayı kodunuzun bir iletiyi işleyememesi durumunda kodunuzun başka bir örneğinin aynı iletiyi alıp yeniden denemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-161">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="dbc8f-162">Kod çağrılarınızı **deleteMessage** ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-162">Your code calls **deleteMessage** right after the message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve the first visible message in the queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process the message in less than 30 seconds, and then delete the message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="dbc8f-163">İletilerin kuyruktan alma için ek seçenekleri</span><span class="sxs-lookup"><span data-stu-id="dbc8f-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="dbc8f-164">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="dbc8f-165">İlk olarak toplu iletiler alabilirsiniz (en fazla 32).</span><span class="sxs-lookup"><span data-stu-id="dbc8f-165">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="dbc8f-166">İkinci olarak daha uzun veya daha kısa bir görünmezlik süresi ayarlayarak kodunuzun her iletiyi tamamen işlemesi için daha az veya daha fazla zaman tanıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="dbc8f-167">Aşağıdaki kod örneğinde **retrieveMessages** tek çağrıda 20 ileti almak için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-167">The following code example uses the **retrieveMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="dbc8f-168">Her bir iletiyi kullanarak işler sonra bir **için** döngü.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="dbc8f-169">Ayrıca beş dakika (300 saniye) her ileti için görünmezlik zaman aşımı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-169">It also sets the invisibility timeout to five minutes (300 seconds) for each message.</span></span> <span data-ttu-id="dbc8f-170">Beş dakika başlar çağrısından sonra aynı anda tüm iletileri böylece zaman beş dakika geçtikten için Not **retrieveMessages**, silinmemiş tüm iletiler görünür olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-170">Note that the five minutes starts for all messages at the same time, so when five minutes have passed since the call to **retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-queues"></a><span data-ttu-id="dbc8f-171">Nasıl yapılır: sıraları listesi</span><span class="sxs-lookup"><span data-stu-id="dbc8f-171">How to: List the queues</span></span>
<span data-ttu-id="dbc8f-172">Geçerli kuyrukların listesini almak için arama **CloudQueueClient.listQueues()** koleksiyonunu döndürür yöntemi **CloudQueue** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-172">To obtain a list of the current queues, call the **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through the collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="dbc8f-173">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="dbc8f-173">How to: Delete a queue</span></span>
<span data-ttu-id="dbc8f-174">Bir kuyruk ve içerdiği tüm iletileri silmek için arama **deleteIfExists** yöntemi **CloudQueue** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-174">To delete a queue and all the messages contained in it, call the **deleteIfExists** method on the **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference to a queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete the queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="dbc8f-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dbc8f-175">Next steps</span></span>
<span data-ttu-id="dbc8f-176">Kuyruk depolamanın temellerini öğrendiğinize göre daha karmaşık depolama görevleri hakkında bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="dbc8f-176">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="dbc8f-177">[Azure depolama için Java SDK'sı][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="dbc8f-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="dbc8f-178">[Azure Storage istemci SDK'sı başvurusu][Azure Storage istemci SDK'sı başvurusu]</span><span class="sxs-lookup"><span data-stu-id="dbc8f-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="dbc8f-179">[Azure Storage Hizmetleri REST API'si][Azure Storage Services REST API]</span><span class="sxs-lookup"><span data-stu-id="dbc8f-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="dbc8f-180">[Azure depolama ekibi blogu][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="dbc8f-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage istemci SDK'sı başvurusu]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
