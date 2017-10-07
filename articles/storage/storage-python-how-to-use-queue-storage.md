---
title: python'dan kuyruk depolama aaaHow toouse | Microsoft Docs
description: "Nasıl toouse Python toocreate Azure kuyruk hizmetinden hello sıraları, silme ve Ekle, Al ve iletileri silmek öğrenin."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a>Nasıl toouse python'dan kuyruk depolama
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir. Merhaba örnekleri Python içinde yazılmış ve hello kullan [Python için Microsoft Azure depolama SDK]. Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**. Kuyruklar hakkında daha fazla bilgi için toohello [sonraki adımlar] bölümüne bakın.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Nasıl yapılır: bir sıra oluşturun
Merhaba **QueueService** nesne kuyruklarla çalışmanıza olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **QueueService** nesnesi. Tooprogrammatically erişim Azure Storage istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın Hello aşağıdakileri ekleyin:

```python
from azure.storage.queue import QueueService
```

Merhaba aşağıdaki kod oluşturur bir **QueueService** Merhaba, depolama hesabı adı ve hesap anahtarını kullanarak nesnesi. 'Myaccount' ve 'mykey' hesap adı ve anahtarı ile değiştirin.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Nasıl yapılır: bir sıraya bir ileti Ekle
tooinsert bir sıra kullanım hello iletiye **put\_ileti** yeni bir ileti oluşturun ve toohello sırası eklemek için yöntem.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Nasıl yapılır: sonraki iletiyi hello Gözat
Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **gözlem\_iletileri** yöntemi. Varsayılan olarak, **gözlem\_iletileri** tek bir iletiye peeks.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Nasıl yapılır: İletiler Dequeue
Kodunuzun bir iletiyi bir kuyruktan iki adımda kaldırır. Çağırdığınızda **almak\_iletileri**, varsayılan olarak bir kuyruktaki hello sonraki iletiyi alın. Döndürülen bir ileti **almak\_iletileri** iletileri bu sıradan okuma başka bir kod görünmez tooany olur. Varsayılan olarak bu ileti 30 saniye görünmez kalır. toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **silmek\_ileti**. Bir ileti kaldırmanın bu iki adımlı işlem kodunuzu tooprocess donanım veya yazılım hatası nedeniyle bir ileti başarısız olduğunda, kodunuzu başka bir örneği aynı ileti alma ve yeniden deneyin sağlar. Kod çağrılarınızı **silmek\_ileti** hello ileti işlendikten sonra sağ.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.
İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz. İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi. Merhaba aşağıdaki kod örneğinde **almak\_iletileri** bir çağrı yöntemi tooget 16 iletileri. Her bir iletiyi kullanarak işler sonra bir döngü için. Ayrıca her ileti için beş dakika hello görünmezlik zaman aşımı ayarlar.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Nasıl yapılır: bir sıraya ileti hello içeriğini değiştirme
Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz. İleti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello iş görevinin durumunu kullanabilirsiniz. Aşağıdaki Hello kodu kullanan hello **güncelleştirme\_ileti** yöntemi tooupdate bir ileti. Merhaba görünürlük zaman aşımı iletisi hemen görüntülenir ve hello içeriği güncellenir anlamına too0 ayarlanır.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Nasıl yapılır: hello kuyruk uzunluğu alma
Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz. **Almak\_sıra\_meta veri** yöntemi ister kuyruk hizmeti tooreturn hello kuyruk hakkındaki meta verileri hello ve hello **approximate_message_count**. iletileri eklenen veya sıra hizmeti tooyour isteği yanıtlar sonra kaldırıldığı için hello yalnızca yaklaşık sonucudur.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Nasıl yapılır: bir kuyruk silme
toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **silmek\_sıra** yöntemi.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Sonraki Adımlar
Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* [Python Geliştirici Merkezi](/develop/python/)
* [Azure Depolama Hizmetleri REST API'si](http://msdn.microsoft.com/library/azure/dd179355)
* [Azure Depolama Ekibi Blog’u]
* [Python için Microsoft Azure depolama SDK]

[Azure Depolama Ekibi Blog’u]: http://blogs.msdn.com/b/windowsazurestorage/
[Python için Microsoft Azure depolama SDK]: https://github.com/Azure/azure-storage-python