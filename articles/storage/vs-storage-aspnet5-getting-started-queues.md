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
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Kuyruk depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (ASP.NET çekirdek)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Oluşturulan veya hello Visual Studio kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra Visual Studio'da Azure kuyruk depolama kullanarak tooget nasıl başlatılacağını bu makalede **bağlı Hizmetleri Ekle** iletişim. Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.

Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir. Tek bir kuyruk iletisinin boyutu too64 kilobayt (KB) ayarlama olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.

başlatılan tooget önce toocreate Azure kuyruk depolama hesabınızdaki gerekir. Nasıl göstereceğiz toocreate bir kuyruktaki kod. Ayrıca, nasıl tooperform basic sıraya ekleme, değiştirme, okuma ve iletileri kuyruğa kaldırma gibi işlemleri göstereceğiz. Merhaba örnekleri C'de yazılmış\# kod ve .NET için Azure Storage istemci kitaplığı hello kullanın. ASP.NET hakkında daha fazla bilgi için bkz: [ASP.NET](http://www.asp.net).

**Not:** hello çağrıları tooAzure depolama ASP.NET Core gerçekleştirmek API'leri bazıları zaman uyumsuzdur. Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için. Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.

* Bkz: [.NET kullanarak Azure kuyruk depolamaya başlayın](storage-dotnet-how-to-use-queues.md) program aracılığıyla Kuyrukları düzenleme hakkında daha fazla bilgi.
* Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.
* Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.
* Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.

## <a name="access-queues-in-code"></a>Kod erişim kuyruklar
ASP.NET Core projelerinde tooaccess sıraları, gereksinim duyduğunuz tooinclude hello aşağıdaki Azure kuyruk depolama erişen öğeleri tooany C# kaynak dosyası.

1. Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Alma bir **CloudQueueClient** tooreference hello sıra nesneleri depolama hesabınızdaki nesne.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Alma bir **CloudQueue** tooreference belirli bir kuyruğa nesne.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Not:** hello hello kod önünde kodu yukarıdaki tüm örnekleri aşağıdaki hello kullanın.

### <a name="create-a-queue-in-code"></a>Kodda bir sıra oluşturun
toocreate hello kodda, Azure kuyruk eklemeniz yeterlidir bir çağrı çok**CreateIfNotExistsAsync**.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>Bir ileti tooa sırası Ekle
var olan bir sırayı iletiye tooinsert oluşturma yeni bir **CloudQueueMessage** nesne sonra çağrı hello **AddMessageAsync** yöntemi.

A **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir bayt dizisi nesne oluşturulabilir.

Burada, selamlama iletisine 'Hello, World' ekleyen bir örnek verilmiştir.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>Bir kuyruktaki ileti okuma
Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **PeekMessageAsync** yöntemi.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>Okuma ve bir sıraya bir ileti Kaldır
Kodunuzu kaldırabilirsiniz (dequeue) bir iletiyi bir kuyruktan iki adımda.

1. Çağrı **GetMessageAsync** tooget hello sıradaki ilk iletiye bir sıra. Döndürülen bir ileti **GetMessageAsync** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. Varsayılan olarak bu ileti 30 saniye görünmez kalır.
2. Merhaba sıradan çağrısı selamlama iletisine kaldırarak toofinish **DeleteMessageAsync**.

Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar. Merhaba aşağıdaki kod çağrıları **DeleteMessageAsync** hello ileti işlendikten sonra sağ.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>İletilerin kuyruktan alma için ek seçenekler yararlanın
İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.
İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz. İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi. Merhaba aşağıdaki kod örneğinde **GetMessages** bir çağrı yöntemi tooget 20 iletileri. Ardından her ileti bir **foreach** döngüsü ile işlenir. Ayrıca, her ileti için hello görünmezlik zaman aşımı too5 dakika ayarlar. Tüm Hello 5 dakika başlangıç hello aynı iletilerini olduğunu not alın zaman, bunu hello çağrısından sonra çok 5 dakika geçtikten sonra**GetMessages**, silinmemiş herhangi ileti yeniden görünür hale gelmiştir.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Merhaba kuyruk uzunluğu alma
Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz. **FetchAttributes** yöntemi hello sıra hizmetinin hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini almasını ister. Merhaba **ApproximateMethodCount** özelliği tarafından alınan hello son değeri döndürür **FetchAttributes** hello kuyruk hizmetini çağırmadan olmadan yöntemi.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>Ortak sıra API'leri Hello zaman uyumsuz-bekleme düzenini kullanın
Bu örnek nasıl toouse hello genel sıra API'leri ile zaman uyumsuz-bekleme düzeni gösterir. Her bir yöntem verilen hello Hello örnek çağrıları hello zaman uyumsuz sürümü. Bu hello zaman uyumsuz sonrası düzeltme her yöntemin tarafından görülebilir. Async yöntemi kullanıldığında, hello çağrı tamamlanana kadar hello zaman uyumsuz-bekleme yerel yürütme askıya alır. Bu davranış, performans sorunlarını engellemeye yardımcı olur ve artırır diğer iş hello geçerli iş parçacığı toodo verir Merhaba, uygulamanızın genel yanıt. Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [zaman uyumsuz ve bekleme (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
## <a name="delete-a-queue"></a>Bir kuyruk silme
toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **silmek** hello nesnesinde yöntemi.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

