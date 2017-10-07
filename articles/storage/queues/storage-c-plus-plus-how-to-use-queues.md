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
# <a name="how-toouse-queue-storage-from-c"></a>Nasıl toouse C++ içinden kuyruk depolama
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir. Merhaba örnekleri C++ ile yazılmış ve hello kullan [C++ için Azure Storage istemci Kitaplığı](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**.

> [!NOTE]
> Bu kılavuzu hedefleri c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hello. Merhaba önerilir sürümü aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>C++ uygulaması oluşturma
Bu kılavuzda, C++ uygulamasında çalıştırabileceğiniz depolama özelliklerini kullanır.

toodo tooinstall ihtiyacınız olacak şekilde, C++ için Azure Storage istemci kitaplığı hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.

tooinstall hello Azure Storage istemci kitaplığı C++ için hello aşağıdaki yöntemleri kullanabilirsiniz:

* **Linux:** hello verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.
* **Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**. Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve basın **ENTER**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Uygulama tooaccess kuyruk depolama yapılandırma
Deyimleri toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess sıraları istediğiniz hello C++ Hello şunlar ekleyin:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesi ayarlama
Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri. Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello listelenen hello depolama hesabı için depolama hesabı ve hello depolama erişim anahtarınızı hello adını kullanarak hello olarak sağlamalısınız [Azure Portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri. Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure Storage hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json). Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest uygulamanızı yerel Windows bilgisayarınızda, Microsoft Azure hello kullanabilirsiniz [depolama öykünücüsü](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) ile Merhaba yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/). Merhaba depolama öykünücüsü hello Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde Azure'da kullanılabilir benzetim yapan bir yardımcı programdır. Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesi tooyour yerel depolama öykünücüsü nasıl bildirebilir gösterir:  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

toostart hello Azure storage öykünücüsü, select hello **Başlat** düğmesini veya tuşuna hello **Windows** anahtarı. Yazmaya başlayın **Azure Storage öykünücüsü**seçip **Microsoft Azure Storage öykünücüsü** uygulamaları hello listesinden.

Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.

## <a name="retrieve-your-connection-string"></a>Bağlantı dizesi alma
Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesabı bilgilerinizi sınıfı. tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello kullanabilirsiniz **ayrıştırma** yöntemi.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Nasıl yapılır: bir sıra oluşturun
A **cloud_queue_client** nesne başvuru nesneleri için kuyrukları almak olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **cloud_queue_client** nesnesi.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Kullanım hello **cloud_queue_client** tooget toouse istediğiniz bir başvuru toohello sıra nesnesi. Yoksa, hello kuyruk oluşturabilirsiniz.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Nasıl yapılır: bir sıraya bir ileti Ekle
var olan bir sırayı iletiye tooinsert ilk oluşturma yeni bir **cloud_queue_message**. Ardından, hello'ı çağırın **add_message** yöntemi. A **cloud_queue_message** herhangi birinden bir dize oluşturulabilir veya **bayt** dizi. İşte (yoksa), bir kuyruk oluşturur ve eklemeleri selamlama iletisine 'Hello, World' kod:

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

## <a name="how-to-peek-at-hello-next-message"></a>Nasıl yapılır: hello sonraki iletiye gözatın
Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **peek_message** yöntemi.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Nasıl yapılır: hello kuyruğa alınan iletinin içeriğini değiştirme
Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz. Merhaba ileti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello durumu hello iş görevi kullanabilirsiniz. koddan hello hello kuyruk iletisini yeni içeriklerle güncelleştirir ve ayarlar görünürlük zaman aşımı tooextend 60 saniye hello. Bu hello hello ileti ile ilişkili işin durumunu kaydeder ve hello istemci selamlama iletisine üzerinde çalışan başka bir dakika toocontinue sağlar. Bir işleme adımı toohardware veya yazılım hatası başarısız olursa hello başından üzerinden toostart gerek kalmadan kuyruk iletilerindeki bu teknik tootrack çok adımlı iş akışlarını kullanabilirsiniz. Genellikle, bir yeniden deneme sayısı da tutacak ve selamlama iletisine n birden fazla kez denenirse, silebilirsiniz. Bu, her işlendiğinde bir uygulama hatası tetikleyen bir iletiye karşı koruma sağlar.

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

## <a name="how-to-de-queue-hello-next-message"></a>Nasıl yapılır: hello sonraki iletiyi sıradan çıkarmak
Kodunuz, bir iletiyi bir kuyruktan iki adımda çıkarır. Çağırdığınızda **get_message**, hello sonraki iletiyi sıraya alın. Döndürülen bir ileti **get_message** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **delete_message**. Bir ileti kaldırmanın bu iki adımlı işlem, kodunuzu toohardware veya yazılım hatası, başka bir örneği kodunuzu nedeniyle bir ileti alabilirsiniz tooprocess başarısız olursa aynı iletiyi hello ve yeniden deneyin olmasını sağlar. Kod çağrılarınızı **delete_message** hello ileti işlendikten sonra sağ.

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Nasıl yapılır: yararlanan çıkarılması iletileri için ek seçenekleri
İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz. İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz. İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi. Merhaba aşağıdaki kod örneği kullanır hello **get_messages** bir çağrı yöntemi tooget 20 iletileri. Her bir iletiyi kullanarak işler sonra bir **için** döngü. Ayrıca, her ileti için hello görünmezlik zaman aşımı toofive dakika ayarlar. Bu hello 5 dakika Not hello tüm iletileri için aynı başlatıldığında, bunu hello görüşmede çok 5 dakika geçtikten sonra**get_messages**, silinmemiş tüm iletiler görünür olacaktır.

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

## <a name="how-to-get-hello-queue-length"></a>Nasıl yapılır: hello kuyruk uzunluğu alma
Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz. Merhaba **download_attributes** yöntemi hello ileti sayısı dahil olmak üzere hello kuyruk özniteliklerini hello kuyruk hizmeti tooretrieve sorar. Merhaba **approximate_message_count** yöntemi hello sırada hello yaklaşık iletilerin sayısını alır.

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

## <a name="how-to-delete-a-queue"></a>Nasıl yapılır: bir kuyruk silme
bir kuyruk ve tüm karışılama iletileri bulunan, içinde arama hello toodelete **delete_queue_if_exists** hello nesnesinde yöntemi.

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

## <a name="next-steps"></a>Sonraki adımlar
Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre Azure Storage hakkında daha fazla bu bağlantılar toolearn izleyin.

* [Nasıl toouse Blob depolama alanından C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Nasıl toouse C++ tablo depolamasından](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [C++'ta listesi Azure Storage kaynakları](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [C++ başvurusu için depolama istemci kitaplığı](http://azure.github.io/azure-storage-cpp)
* [Azure Depolama Belgeleri](https://azure.microsoft.com/documentation/services/storage/)