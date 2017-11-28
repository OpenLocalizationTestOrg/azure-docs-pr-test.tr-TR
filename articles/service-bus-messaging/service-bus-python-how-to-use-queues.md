---
title: "Python ile Azure Service Bus kuyruklarını kullanma | Microsoft Docs"
description: "Python'dan Azure Service Bus kuyruklarını kullanmayı öğrenin."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="d6043-103">Python ile Service Bus kuyruklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="d6043-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="d6043-104">Bu makalede, Service Bus kuyruklarının nasıl kullanılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="d6043-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="d6043-105">Python ve kullanım örnekleri yazılır [Python Azure Service Bus paket][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="d6043-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="d6043-106">Kapsamdaki senaryolar dahil **ileti gönderme ve alma sıra oluşturma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="d6043-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="d6043-107">Python yüklemek için veya [Python Azure Service Bus paket][Python Azure Service Bus package], bkz: [Python Yükleme Kılavuzu'na](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="d6043-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="d6043-108">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6043-108">Create a queue</span></span>
<span data-ttu-id="d6043-109">**ServiceBusService** nesne kuyruklarla çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6043-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="d6043-110">Service Bus programlı olarak erişmek istediğiniz tüm Python dosyanın en üstüne yakın aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d6043-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="d6043-111">Aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d6043-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="d6043-112">Değiştir `mynamespace`, `sharedaccesskeyname`, ve `sharedaccesskey` ad alanı, paylaşılan erişim imzası (SAS) anahtar adını ve değeri.</span><span class="sxs-lookup"><span data-stu-id="d6043-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="d6043-113">SAS anahtar adını ve değerini değerlerini bulunabilir [Azure portal] [ Azure portal] bağlantı bilgilerini veya Visual Studio'da **özellikleri** hizmet seçerken bölmesi Veri yolu ad alanı Sunucu Gezgininde (önceki bölümde gösterildiği gibi).</span><span class="sxs-lookup"><span data-stu-id="d6043-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="d6043-114">`create_queue` Yöntemi de ileti zamanı dinamik (TTL) veya en büyük sıra boyutu gibi varsayılan sırası ayarlarını geçersiz kılmanıza olanak sağlayan ek seçenekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="d6043-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="d6043-115">Aşağıdaki örnek en büyük sıra boyutu 5 GB ve TTL değeri 1 dakika olarak ayarlar:</span><span class="sxs-lookup"><span data-stu-id="d6043-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="d6043-116">Kuyruğa ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="d6043-116">Send messages to a queue</span></span>
<span data-ttu-id="d6043-117">Uygulama çağrılarınızı bir Service Bus kuyruğuna bir ileti göndermek için `send_queue_message` yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d6043-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="d6043-118">Aşağıdaki örnek adlı sırasına sınama iletisi göndermek nasıl gösterir `taskqueue` kullanarak `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="d6043-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="d6043-119">Service Bus kuyrukları, [Standart katmanda](service-bus-premium-messaging.md) maksimum 256 KB ve [Premium katmanda](service-bus-premium-messaging.md) maksimum 1 MB ileti boyutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="d6043-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="d6043-120">Standart ve özel uygulama özelliklerini içeren üst bilginin maksimum dosya boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6043-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="d6043-121">Kuyrukta tutulan ileti sayısına ilişkin bir sınır yoktur ancak kuyruk tarafından tutulan iletilerin toplam boyutu için uç sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="d6043-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="d6043-122">Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="d6043-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="d6043-123">Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="d6043-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="d6043-124">Kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="d6043-124">Receive messages from a queue</span></span>
<span data-ttu-id="d6043-125">İletileri kullanarak bir Sıraya alınan `receive_queue_message` yöntemi **ServiceBusService** nesnesi:</span><span class="sxs-lookup"><span data-stu-id="d6043-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="d6043-126">İletileri zaman okunduğu gibi sıradan silinir parametresi `peek_lock` ayarlanır **False**.</span><span class="sxs-lookup"><span data-stu-id="d6043-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="d6043-127">(Özet) okuma ve iletiyi sıradan parametresi ayarlanarak silmeden kilitlemek `peek_lock` için **doğru**.</span><span class="sxs-lookup"><span data-stu-id="d6043-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="d6043-128">Okuma ve ileti alma işleminin bir parçası olarak silme davranışı en basit modeldir ve uygulamanın hata oluştuğunda bir iletiyi işlemeyi değil dayanabileceği senaryoları için en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d6043-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="d6043-129">Bu durumu daha iyi anlamak için müşterinin bir alma isteği bildirdiğini ve bu isteğin işlenmeden çöktüğünü varsayın.</span><span class="sxs-lookup"><span data-stu-id="d6043-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="d6043-130">Service Bus iletiyi kullanılıyor olarak işaretlenmiş nedeniyle uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında, sonra da çökmenin öncesinde kullanılan iletiyi atlamış olur.</span><span class="sxs-lookup"><span data-stu-id="d6043-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="d6043-131">Varsa `peek_lock` parametrenin ayarlanmış **doğru**, alma, iletilere veremeyen uygulamaları desteklemenin mümkün kılar bir iki aşamalı işlemi haline gelir.</span><span class="sxs-lookup"><span data-stu-id="d6043-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="d6043-132">Service Bus bir istek aldığında bir sonraki kullanılacak iletiyi bulur, diğer tüketicilerin bu iletiyi almasını engellemek için kilitler ve ardından uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6043-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="d6043-133">Uygulama iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), çağırarak alma işleminin ikinci aşamasını tamamlar **silmek** yöntemi **ileti** nesne.</span><span class="sxs-lookup"><span data-stu-id="d6043-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="d6043-134">**Silmek** yöntemi iletiyi kullanılıyor olarak işaretler ve kuyruktan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d6043-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="d6043-135">Uygulama çökmelerini ve okunmayan iletileri giderme</span><span class="sxs-lookup"><span data-stu-id="d6043-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="d6043-136">Service Bus, uygulamanızda gerçekleşen hataları veya ileti işlenirken oluşan zorlukları rahat bir şekilde ortadan kaldırmanıza yardımcı olmak için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6043-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="d6043-137">Alıcı uygulamanın iletiyi herhangi bir nedenden dolayı işleyemedi sonra işleyememesi **kilidini** yöntemi **ileti** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d6043-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="d6043-138">Bu, Service Bus hizmetinin Kuyruktaki iletinin kilidini açmasına ve iletiyi aynı veya başka bir kullanıcı uygulama tarafından tekrar alınabilir hale getirmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="d6043-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="d6043-139">Ayrıca kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve uygulama önce iletiyi işleyemezse (örneğin, uygulama çökerse) Service Bus otomatik olarak iletinin kilidini açmak ve onu kilit zaman aşımı dolmadan yeniden alınabilmesi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6043-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="d6043-140">Uygulama iletiyi ancak önce çökmesi durumunda, **silmek** yöntemi çağrıldıktan sonra yeniden başlatıldığında ileti uygulamaya tekrar teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="d6043-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="d6043-141">Bu genellikle adlandırılır **en az bir kez işleme**, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="d6043-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="d6043-142">Senaryo yinelenen işlemeyi kabul etmiyorsa yinelenen ileti teslimine izin vermek için uygulama geliştiricilerin uygulamaya ilave bir mantık eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d6043-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="d6043-143">Bu genellikle kullanılarak elde edilen **MessageID** özelliğini iletinin teslimat denemelerinde.</span><span class="sxs-lookup"><span data-stu-id="d6043-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6043-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6043-144">Next steps</span></span>
<span data-ttu-id="d6043-145">Service Bus kuyruklarını temel bilgileri öğrendiniz, daha fazla bilgi için aşağıdaki makalelere bakın.</span><span class="sxs-lookup"><span data-stu-id="d6043-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="d6043-146">[Kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="d6043-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

