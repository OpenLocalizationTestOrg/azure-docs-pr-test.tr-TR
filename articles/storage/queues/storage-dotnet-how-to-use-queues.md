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
# <a name="get-started-with-azure-queue-storage-using-net"></a>.NET kullanarak Azure Kuyruk Depolamaya başlayın
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Genel Bakış
Azure Queue depolama birimi, uygulama bileşenleri arasında bulut mesajlaşma özelliği sağlar. Ölçeklendirmek üzere uygulama tasarlarken, uygulama bileşenleri birbirinden bağımsız şekilde ölçeklenebilmek için genellikle birbirinden ayrılır. Merhaba bulutta, hello Masaüstü, bir şirket içi sunucu veya bir mobil cihaz çalıştırıp çalıştırmadığınızı uygulama bileşenleri arasında iletişim için zaman uyumsuz Mesajlaşma kuyruk depolama sunar. Kuyruk depolama ayrıca zaman uyumsuz görevlerin yönetilmesini ve süreç iş akışlarının oluşturulmasını destekler.

### <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici, nasıl Azure kuyruk depolama kullanarak bazı genel senaryolar için .NET toowrite kodu gösterir. Kapsanan senaryolara kuyruk oluşturma ve silme ile kuyruk iletileri ekleme, okuma ve silme dahildir.

**Zaman toocomplete tahmini:** 45 dakika

**Önkoşullar:**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [.NET için Azure Depolama İstemcisi](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [.NET için Azure Yapılandırma Yöneticisi](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Bir [Azure Storage hesabı](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Using yönergeleri ekleme
Merhaba aşağıdakileri ekleyin `using` hello yönergeleri toohello üst `Program.cs` dosyası:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Merhaba bağlantı dizesini ayrıştırma
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Merhaba kuyruk hizmeti istemcisi oluşturma
Merhaba **CloudQueueClient** sınıfı, kuyruk depolamada depolanan, tooretrieve sıraları sağlar. Tek yönlü toocreate hello hizmeti istemcisi şöyledir:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Artık veri okuyan ve yazan veri tooQueue depolama hazır toowrite kodu bulunur.

## <a name="create-a-queue"></a>Bir kuyruk oluşturma
Bu örnekte gösterilir nasıl toocreate zaten yoksa, bir kuyruk:

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

## <a name="insert-a-message-into-a-queue"></a>Kuyruğa bir ileti yerleştirme
var olan bir sırayı iletiye tooinsert ilk oluşturma yeni bir **CloudQueueMessage**. Ardından, hello'ı çağırın **AddMessage** yöntemi. **CloudQueueMessage** bir dizeden (UTF-8 biçiminde) veya bir **bayt** dizisinden oluşturulabilir. İşte (yoksa), bir kuyruk oluşturur ve eklemeleri selamlama iletisine 'Hello, World' kod:

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

## <a name="peek-at-hello-next-message"></a>Merhaba sonraki iletiye gözatın
Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **PeekMessage** yöntemi.

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

## <a name="change-hello-contents-of-a-queued-message"></a>Merhaba kuyruğa alınan iletinin içeriğini değiştirme
Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz. İleti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello iş görevinin durumunu kullanabilirsiniz. koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve ayarlar görünürlük zaman aşımı tooextend 60 saniye hello. Bu hello hello ileti ile ilişkili işin durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar. Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz. Genellikle, bir yeniden deneme sayısı da tutacak ve hello olursa ileti denenir birden fazla  *n*  kez silmeniz. Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.

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

## <a name="de-queue-hello-next-message"></a>Merhaba sonraki iletiyi sıradan çıkarmak
Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır. Çağırdığınızda **GetMessage**, hello sonraki iletiyi sıraya alın. Döndürülen bir ileti **GetMessage** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. Varsayılan olarak bu ileti 30 saniye görünmez kalır. toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **DeleteMessage**. Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar. Kod çağrılarınızı **DeleteMessage** hello ileti işlendikten sonra sağ.

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

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Genel Kuyruk depolama API’leri ile Zaman Uyumsuz-Bekleme yöntemini kullanma
Bu örnek nasıl toouse hello zaman uyumsuz-bekleme desen genel kuyruk depolama API'leri gösterir. Hello örnek hello tarafından belirtildiği şekilde her bir yöntem, verilen hello hello zaman uyumsuz sürümlerini çağırır *zaman uyumsuz* yönteminin her soneki. Async yöntemi kullanıldığında, zaman uyumsuz hello-bekleme düzeni hello çağrı tamamlanana kadar yerel çalıştırmayı askıya alır. Bu davranış, performans sorunlarını engellemeye yardımcı olur ve artırır diğer iş hello geçerli iş parçacığı toodo verir Merhaba, uygulamanızın genel yanıt. Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [zaman uyumsuz ve bekleme (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>İletilerin kuyruktan çıkarılması için ek seçenekleri kullanma
İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.
İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz. İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi. Merhaba aşağıdaki kod örneğinde **GetMessages** bir çağrı yöntemi tooget 20 iletileri. Ardından her ileti bir **foreach** döngüsü ile işlenir. Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar. Bu hello 5 dakika Not hello tüm iletileri için aynı başlatıldığında, bunu hello görüşmede çok 5 dakika geçtikten sonra**GetMessages**, silinmemiş tüm iletiler görünür olacaktır.

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

## <a name="get-hello-queue-length"></a>Merhaba kuyruk uzunluğu alma
Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz. **FetchAttributes** yöntemi hello sıra hizmetinin hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini almasını ister. Merhaba **ApproximateMessageCount** özelliği tarafından alınan hello son değeri döndürür **FetchAttributes** hello kuyruk hizmetini çağırmadan olmadan yöntemi.

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

## <a name="delete-a-queue"></a>Bir kuyruk silme
toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **silmek** hello nesnesinde yöntemi.

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
    

## <a name="next-steps"></a>Sonraki adımlar
Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin.

* Kullanılabilir API'ler ile ilgili tam Ayrıntılar için Hello kuyruk hizmeti başvuru belgelerini görüntüleyin:
  * [.NET başvurusu için Depolama İstemci Kitaplığı](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [REST API başvurusu](http://msdn.microsoft.com/library/azure/dd179355)
* Nasıl toosimplify hello kodu yazdığınız öğrenin hello kullanarak Azure Storage ile toowork [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).
* Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.
  * [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore yapılandırılmış veri.
  * [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../blobs/storage-dotnet-how-to-use-blobs.md) toostore yapılandırılmamış veriler.
  * [.NET (C#) kullanarak tooSQL veritabanına bağlanma](../../sql-database/sql-database-connect-query-dotnet-core.md) toostore ilişkisel veri.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
