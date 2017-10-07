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
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Azure kuyruk depolama ve Visual Studio ile çalışmaya başlama (Projeler bulut Hizmetleri) Hizmetleri bağlı
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Oluşturulan veya hello Visual Studio kullanarak bir Azure depolama hesabı bulut Hizmetleri projesinde başvurulan sonra Visual Studio'da Azure kuyruk depolama kullanarak tooget nasıl başlatılacağını bu makalede **bağlı Hizmetleri Ekle** iletişim .

Nasıl göstereceğiz toocreate bir kuyruktaki kod. Ayrıca, nasıl tooperform basic sıraya ekleme, değiştirme, okuma ve kaldırma iletileri gibi işlemleri göstereceğiz. Merhaba örnekler C# kodda yazılır ve hello kullanır [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.

* Bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](../storage/queues/storage-dotnet-how-to-use-queues.md) kod kuyruklarda düzenleme hakkında daha fazla bilgi.
* Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.
* Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.
* Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.

Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir. Tek bir kuyruk iletisinin boyutu too64 KB yukarı olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.

## <a name="access-queues-in-code"></a>Kod erişim kuyruklar
Visual Studio bulut Hizmetleri projelerinde tooaccess sıraları, gereksinim duyduğunuz tooinclude hello aşağıdaki Azure kuyruk depolama erişim öğeleri tooany C# kaynak dosyası.

1. Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Alma bir **CloudQueueClient** tooreference hello sıra nesneleri depolama hesabınızdaki nesne.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Alma bir **CloudQueue** tooreference belirli bir kuyruğa nesne.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Not:** hello hello kod önünde kodu yukarıdaki tüm örnekleri aşağıdaki hello kullanın.

## <a name="create-a-queue-in-code"></a>Kodda bir sıra oluşturun
kodda, toocreate hello sıra eklemeniz yeterlidir bir çağrı çok**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Bir ileti tooa sırası Ekle
var olan bir sırayı iletiye tooinsert oluşturma yeni bir **CloudQueueMessage** nesne sonra çağrı hello **AddMessage** yöntemi.

A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.

Burada, selamlama iletisine 'Hello, World' ekleyen bir örnek verilmiştir.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Bir kuyruktaki ileti okuma
Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **PeekMessage** yöntemi.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Okuma ve bir sıraya bir ileti Kaldır
Kodunuzu kaldırabilirsiniz (kuyruktan) bir iletiyi bir kuyruktan iki adımda.

1. Çağrı **GetMessage** tooget hello sıradaki ilk iletiye bir sıra. Döndürülen bir ileti **GetMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. Varsayılan olarak bu ileti 30 saniye görünmez kalır.
2. Merhaba sıradan çağrısı selamlama iletisine kaldırarak toofinish **DeleteMessage**.

Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar. Merhaba aşağıdaki kod çağrıları **DeleteMessage** hello ileti işlendikten sonra sağ.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Ek seçenekler tooprocess kullanın ve iletileri kuyruğa kaldırın
İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.

* Toplu (yukarı too32) iletiler alabilirsiniz.
* Kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi. Merhaba aşağıdaki kod örneğinde **GetMessages** bir çağrı yöntemi tooget 20 iletileri. Ardından her ileti bir **foreach** döngüsü ile işlenir. Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar. Bu hello 5 dakika Not hello tüm iletileri için aynı başlatıldığında, bunu hello görüşmede çok 5 dakika geçtikten sonra**GetMessages**, silinmemiş tüm iletiler görünür olacaktır.

Örnek aşağıda verilmiştir:

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Merhaba kuyruk uzunluğu alma
Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz. **FetchAttributes** yöntemi hello sıra hizmetinin hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini almasını ister. Merhaba **ApproximateMethodCount** özelliği tarafından alınan hello son değeri döndürür **FetchAttributes** hello kuyruk hizmetini çağırmadan olmadan yöntemi.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Kullanım hello ortak Azure sıra API'leri ile zaman uyumsuz-bekleme yöntemi
Bu örnek nasıl toouse hello zaman uyumsuz-bekleme desen ile ortak Azure sıra API'leri gösterir. Merhaba örnek çağırır hello zaman uyumsuz sürümü her yöntemleri verilen Merhaba, bu hello tarafından görülebilir **zaman uyumsuz** yönteminin her sonrası düzeltme. Zaman uyumsuz yöntem kullanılan hello zaman uyumsuz olduğunda-bekleme düzeni hello çağrı tamamlanana kadar yerel çalıştırmayı askıya alır. Bu davranış, performans sorunlarını engellemeye yardımcı olur ve artırır diğer iş hello geçerli iş parçacığı toodo verir Merhaba, uygulamanızın genel yanıt. Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [zaman uyumsuz ve bekleme (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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

## <a name="delete-a-queue"></a>Bir kuyruk silme
bir kuyruk ve tüm karışılama iletileri bulunan, içinde arama hello toodelete **silmek** hello nesnesinde yöntemi.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

