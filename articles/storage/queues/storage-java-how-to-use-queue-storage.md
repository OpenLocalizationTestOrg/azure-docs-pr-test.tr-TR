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
# <a name="how-toouse-queue-storage-from-java"></a>Nasıl toouse Java'dan kuyruk depolama
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir. Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure depolama SDK'sı][Azure Storage SDK for Java]. Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma** ve **silme** sıralar. Merhaba kuyruklar hakkında daha fazla bilgi için bkz: [sonraki adımlar](#Next-Steps) bölümü.

Not: Bir SDK'sı Android cihazlarda Azure depolama kullanan geliştiriciler için kullanılabilir. Daha fazla bilgi için bkz: Merhaba [Android için Azure depolama SDK'sı][Azure Storage SDK for Android].

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Java uygulaması oluşturma
Bu kılavuzda, bir Java uygulaması içinde yerel olarak veya bir web rolü veya Azure çalışan rolünde çalışan kodu çalıştırılabilir depolama özelliklerini kullanır.

toodo tooinstall ihtiyacınız olacak şekilde, Java Geliştirme Seti (JDK) hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun. Bunu yaptıktan sonra geliştirme sisteminizde hello en düşük gereksinimleri ve hello listelenen bağımlılıkları karşılayan tooverify gerekir [Java için Azure depolama SDK'sı] [ Azure Storage SDK for Java] github'daki. Sisteminiz bu gereksinimleri karşılıyorsa, karşıdan yükleme ve bu depodan sisteminizdeki Java için hello Azure depolama kitaplıkları için hello yönergeleri izleyebilir. Bu görevleri tamamladıktan sonra mümkün toocreate hello örnekleri bu makalede kullanan bir Java uygulaması olacaktır.

## <a name="configure-your-application-tooaccess-queue-storage"></a>Uygulama tooaccess kuyruk depolama yapılandırma
İçeri aktarma deyimlerini toohello dosyasının üst kısmında toouse Azure depolama API'leri tooaccess sıraları istediğiniz hello Java aşağıdaki hello ekleyin:

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesini ayarlayın
Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri. Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello depolama hesabınızın adını kullanarak hello olarak sağlamak ve hello listelenen hello depolama hesabı için birincil erişim anahtarını hello gerekir [Azure Portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri. Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Çalışan bir uygulama içinde Microsoft Azure rolünde içinde bu dize hello hizmet yapılandırma dosyasında depolanabilir *ServiceConfiguration.cscfg*ve bir çağrı toohello ile erişilebilir  **RoleEnvironment.getConfigurationSettings** yöntemi. Merhaba bağlantı dizesinden alma örneği bir **ayarı** adlı öğe *StorageConnectionString* hello hizmet yapılandırma dosyasında:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.

## <a name="how-to-create-a-queue"></a>Nasıl yapılır: bir sıra oluşturun
A **CloudQueueClient** nesne başvuru nesneleri için kuyrukları almak olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **CloudQueueClient** nesnesi. (Not: ek yolları toocreate vardır **CloudStorageAccount** nesneleri; daha fazla bilgi için bkz: **CloudStorageAccount** hello içinde [Azure Storage istemci SDK'sı başvurusu].)

Kullanım hello **CloudQueueClient** tooget toouse istediğiniz bir başvuru toohello sıra nesnesi. Yoksa, hello kuyruk oluşturabilirsiniz.

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

## <a name="how-to-add-a-message-tooa-queue"></a>Nasıl yapılır: bir ileti tooa sırası Ekle
var olan bir sırayı iletiye tooinsert ilk oluşturma yeni bir **CloudQueueMessage**. Ardından, hello'ı çağırın **addMessage** yöntemi. A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi oluşturulabilir. İşte (yoksa), bir kuyruk oluşturur ve eklemeleri selamlama iletisine "Hello, World" kod.

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

## <a name="how-to-peek-at-hello-next-message"></a>Nasıl yapılır: hello sonraki iletiye gözatın
Bir sıra Merhaba öne hello iletiye hello sıradan çağırarak kaldırmadan iletiye göz atabilirsiniz **peekMessage**.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Nasıl yapılır: hello kuyruğa alınan iletinin içeriğini değiştirme
Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz. Merhaba ileti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello durumu hello iş görevi kullanabilirsiniz. koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve ayarlar görünürlük zaman aşımı tooextend 60 saniye hello. Bu hello hello ileti ile ilişkili işin durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar. Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz. Genellikle, bir yeniden deneme sayısı da tutacak ve hello olursa ileti denenir birden fazla  *n*  kez silmeniz. Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.

Merhaba aşağıdaki örnek aramalar hello iletileri kuyruğunu aracılığıyla kod, "Hello, World" Merhaba içerik için eşleşen sonra selamlama iletisine içerik değiştirir ve çıkar hello ilk iletiyi bulur.

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

Alternatif olarak, hello aşağıdaki kod örneği yalnızca hello ilk görünür ileti hello sırasına güncelleştirir.

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

## <a name="how-to-get-hello-queue-length"></a>Nasıl yapılır: hello kuyruk uzunluğu alma
Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz. Merhaba **downloadAttributes** kaç iletiler bir kuyrukta olan sayısına dahil yöntemi çeşitli geçerli değerler için hello sıra hizmeti sorar. iletileri eklenen veya hello sıra hizmeti tooyour isteği yanıtlar sonra kaldırıldığı için hello yalnızca yaklaşık sayısıdır. Merhaba **getApproximateMessageCount** yöntemi çok hello çağrısı tarafından alınan hello son değeri döndürür**downloadAttributes**, hello kuyruk hizmetini çağırmadan olmadan.

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

## <a name="how-to-dequeue-hello-next-message"></a>Nasıl yapılır: hello sonraki iletiyi sıradan çıkarma
Kodunuzun bir iletiyi bir kuyruktan iki adımda dequeues. Çağırdığınızda **retrieveMessage**, hello sonraki iletiyi sıraya alın. Döndürülen bir ileti **retrieveMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. Varsayılan olarak bu ileti 30 saniye görünmez kalır. toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **deleteMessage**. Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar. Kod çağrılarınızı **deleteMessage** hello ileti işlendikten sonra sağ.

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

## <a name="additional-options-for-dequeuing-messages"></a>İletilerin kuyruktan alma için ek seçenekleri
İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz. İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz. İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.

Merhaba aşağıdaki kod örneği kullanır hello **retrieveMessages** bir çağrı yöntemi tooget 20 iletileri. Her bir iletiyi kullanarak işler sonra bir **için** döngü. Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika (300 saniye cinsinden) ayarlar. Bu hello beş dakika başlatıldığında tüm not iletileri hello aynı zaman, bunu beş dakika hello görüşmede çok geçtiğinde**retrieveMessages**, silinmemiş tüm iletiler görünür olacaktır.

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

## <a name="how-to-list-hello-queues"></a>Nasıl yapılır: liste hello sıraları
tooobtain hello geçerli kuyrukların, çağrı hello listesini **CloudQueueClient.listQueues()** koleksiyonunu döndürür yöntemi **CloudQueue** nesneleri.

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

## <a name="how-to-delete-a-queue"></a>Nasıl yapılır: bir kuyruk silme
toodelete bir sıra ve tüm karışılama iletileri bulunan, içinde arama hello **deleteIfExists** hello yöntemi **CloudQueue** nesnesi.

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

## <a name="next-steps"></a>Sonraki adımlar
Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.

* [Azure depolama için Java SDK'sı][Azure Storage SDK for Java]
* [Azure Storage istemci SDK'sı başvurusu][Azure Storage istemci SDK'sı başvurusu]
* [Azure Storage Hizmetleri REST API'si][Azure Storage Services REST API]
* [Azure depolama ekibi blogu][Azure Storage Team Blog]

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage istemci SDK'sı başvurusu]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
