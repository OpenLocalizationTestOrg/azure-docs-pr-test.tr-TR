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
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="8d7bb-103">Nasıl toouse python'dan kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="8d7bb-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="8d7bb-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8d7bb-104">Overview</span></span>
<span data-ttu-id="8d7bb-105">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure kuyruk depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="8d7bb-106">Merhaba örnekleri Python içinde yazılmış ve hello kullan [Python için Microsoft Azure depolama SDK].</span><span class="sxs-lookup"><span data-stu-id="8d7bb-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="8d7bb-107">Merhaba kapsamdaki senaryolar da dahil **ekleme**, **gözatma**, **alma**, ve **silme** kuyruk iletileri yanı  **oluşturma ve silme**.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="8d7bb-108">Kuyruklar hakkında daha fazla bilgi için toohello [sonraki adımlar] bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="8d7bb-109">Nasıl yapılır: bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="8d7bb-109">How To: Create a Queue</span></span>
<span data-ttu-id="8d7bb-110">Merhaba **QueueService** nesne kuyruklarla çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="8d7bb-111">Merhaba aşağıdaki kod oluşturur bir **QueueService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="8d7bb-112">Tooprogrammatically erişim Azure Storage istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın Hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8d7bb-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="8d7bb-113">Merhaba aşağıdaki kod oluşturur bir **QueueService** Merhaba, depolama hesabı adı ve hesap anahtarını kullanarak nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="8d7bb-114">'Myaccount' ve 'mykey' hesap adı ve anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="8d7bb-115">Nasıl yapılır: bir sıraya bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="8d7bb-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="8d7bb-116">tooinsert bir sıra kullanım hello iletiye **put\_ileti** yeni bir ileti oluşturun ve toohello sırası eklemek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="8d7bb-117">Nasıl yapılır: sonraki iletiyi hello Gözat</span><span class="sxs-lookup"><span data-stu-id="8d7bb-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="8d7bb-118">Bir sıra Merhaba öne hello iletiye tarafından arama hello hello kuyruktan kaldırmadan iletiye göz atabilirsiniz **gözlem\_iletileri** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="8d7bb-119">Varsayılan olarak, **gözlem\_iletileri** tek bir iletiye peeks.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="8d7bb-120">Nasıl yapılır: İletiler Dequeue</span><span class="sxs-lookup"><span data-stu-id="8d7bb-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="8d7bb-121">Kodunuzun bir iletiyi bir kuyruktan iki adımda kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="8d7bb-122">Çağırdığınızda **almak\_iletileri**, varsayılan olarak bir kuyruktaki hello sonraki iletiyi alın.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="8d7bb-123">Döndürülen bir ileti **almak\_iletileri** iletileri bu sıradan okuma başka bir kod görünmez tooany olur.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="8d7bb-124">Varsayılan olarak bu ileti 30 saniye görünmez kalır.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="8d7bb-125">toofinish kaldırma selamlama iletisine hello sırasından ayrıca çağırmalısınız **silmek\_ileti**.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="8d7bb-126">Bir ileti kaldırmanın bu iki adımlı işlem kodunuzu tooprocess donanım veya yazılım hatası nedeniyle bir ileti başarısız olduğunda, kodunuzu başka bir örneği aynı ileti alma ve yeniden deneyin sağlar.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="8d7bb-127">Kod çağrılarınızı **silmek\_ileti** hello ileti işlendikten sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="8d7bb-128">İletilerin bir kuyruktan alınma şeklini iki yöntemle özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="8d7bb-129">İlk olarak toplu iletiler (yukarı too32) elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="8d7bb-130">İkinci olarak, kodunuzu daha fazla izin vererek uzun veya daha kısa bir görünmezlik zaman aşımı ayarlayabilirsiniz veya daha az zaman toofully her ileti işlenemedi.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="8d7bb-131">Merhaba aşağıdaki kod örneğinde **almak\_iletileri** bir çağrı yöntemi tooget 16 iletileri.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="8d7bb-132">Her bir iletiyi kullanarak işler sonra bir döngü için.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="8d7bb-133">Ayrıca her ileti için beş dakika hello görünmezlik zaman aşımı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="8d7bb-134">Nasıl yapılır: bir sıraya ileti hello içeriğini değiştirme</span><span class="sxs-lookup"><span data-stu-id="8d7bb-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="8d7bb-135">Bir ileti yerinde hello sırasındaki hello içeriğini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="8d7bb-136">İleti bir iş görevini temsil ediyorsa, bu özellik tooupdate hello iş görevinin durumunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="8d7bb-137">Aşağıdaki Hello kodu kullanan hello **güncelleştirme\_ileti** yöntemi tooupdate bir ileti.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="8d7bb-138">Merhaba görünürlük zaman aşımı iletisi hemen görüntülenir ve hello içeriği güncellenir anlamına too0 ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="8d7bb-139">Nasıl yapılır: hello kuyruk uzunluğu alma</span><span class="sxs-lookup"><span data-stu-id="8d7bb-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="8d7bb-140">Bir kuyruktaki ileti sayısı hello tahmini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="8d7bb-141">**Almak\_sıra\_meta veri** yöntemi ister kuyruk hizmeti tooreturn hello kuyruk hakkındaki meta verileri hello ve hello **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="8d7bb-142">iletileri eklenen veya sıra hizmeti tooyour isteği yanıtlar sonra kaldırıldığı için hello yalnızca yaklaşık sonucudur.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="8d7bb-143">Nasıl yapılır: bir kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="8d7bb-143">How To: Delete a Queue</span></span>
<span data-ttu-id="8d7bb-144">toodelete bir sıra ve tüm karışılama iletileri bulunan içinde arama **silmek\_sıra** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="8d7bb-145">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8d7bb-145">Next Steps</span></span>
<span data-ttu-id="8d7bb-146">Kuyruk depolamanın hello temel bilgileri öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="8d7bb-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="8d7bb-147">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="8d7bb-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="8d7bb-148">Azure Depolama Hizmetleri REST API'si</span><span class="sxs-lookup"><span data-stu-id="8d7bb-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="8d7bb-149">[Azure Depolama Ekibi Blog’u]</span><span class="sxs-lookup"><span data-stu-id="8d7bb-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="8d7bb-150">[Python için Microsoft Azure depolama SDK]</span><span class="sxs-lookup"><span data-stu-id="8d7bb-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Azure Depolama Ekibi Blog’u]: http://blogs.msdn.com/b/windowsazurestorage/
[Python için Microsoft Azure depolama SDK]: https://github.com/Azure/azure-storage-python