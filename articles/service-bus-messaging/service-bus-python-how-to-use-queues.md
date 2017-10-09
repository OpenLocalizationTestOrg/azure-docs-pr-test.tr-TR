---
title: "aaaHow toouse Azure Service Bus kuyrukları Python ile | Microsoft Docs"
description: "Python nasıl toouse Azure Service Bus kuyrukları öğrenin."
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
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="8b0fc-103">Python ile nasıl toouse Service Bus kuyrukları</span><span class="sxs-lookup"><span data-stu-id="8b0fc-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="8b0fc-104">Bu makalede nasıl toouse Service Bus kuyruklarını.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="8b0fc-105">Merhaba örnekleri Python içinde yazılmış ve hello kullan [Python Azure Service Bus paket][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="8b0fc-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="8b0fc-106">Merhaba kapsanan senaryolar dahil **ileti gönderme ve alma sıra oluşturma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="8b0fc-107">Python veya hello tooinstall [Python Azure Service Bus paket][Python Azure Service Bus package], hello bkz [Python Yükleme Kılavuzu'na](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="8b0fc-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="8b0fc-108">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="8b0fc-108">Create a queue</span></span>
<span data-ttu-id="8b0fc-109">Merhaba **ServiceBusService** nesne kuyruklarla toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="8b0fc-110">Tooprogrammatically erişim Service Bus istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8b0fc-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="8b0fc-111">Merhaba aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="8b0fc-112">Değiştir `mynamespace`, `sharedaccesskeyname`, ve `sharedaccesskey` ad alanı, paylaşılan erişim imzası (SAS) anahtar adını ve değeri.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="8b0fc-113">Merhaba hello SAS anahtar adı ve değeri değerlerini hello bulunabilir [Azure portal] [ Azure portal] bağlantı bilgilerini veya hello Visual Studio **özellikleri** seçerken bölmesi Sunucu Gezgininde Service Bus ad alanı (Merhaba önceki bölümde gösterildiği gibi) hello.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="8b0fc-114">Merhaba `create_queue` yöntemi de ileti toolive süresi (TTL) veya en büyük sıra boyutu gibi toooverride varsayılan sıra ayarları etkinleştirmek ek seçenekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="8b0fc-115">Merhaba aşağıdaki örnek hello en büyük sıra boyutu too5 GB ve hello TTL değeri too1 minute ayarlar:</span><span class="sxs-lookup"><span data-stu-id="8b0fc-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="8b0fc-116">İletileri tooa sırası Gönder</span><span class="sxs-lookup"><span data-stu-id="8b0fc-116">Send messages tooa queue</span></span>
<span data-ttu-id="8b0fc-117">ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `send_queue_message` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="8b0fc-118">Merhaba aşağıdaki örnekte nasıl toosend adlı bir sınama iletisi toohello sırası gösteren `taskqueue` kullanarak `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="8b0fc-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="8b0fc-119">Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="8b0fc-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="8b0fc-120">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="8b0fc-121">Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="8b0fc-122">Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="8b0fc-123">Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="8b0fc-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="8b0fc-124">Kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="8b0fc-124">Receive messages from a queue</span></span>
<span data-ttu-id="8b0fc-125">İletileri hello kullanarak bir kuyruktan alınan `receive_queue_message` hello yöntemi **ServiceBusService** nesnesi:</span><span class="sxs-lookup"><span data-stu-id="8b0fc-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="8b0fc-126">İletileri zaman okunduğu gibi hello sıradan silinir parametre hello `peek_lock` çok ayarlanır**False**.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="8b0fc-127">(Özet) okuma ve ayarlama hello parametresiyle hello sıradan silmeden selamlama iletisine kilitlemek `peek_lock` çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="8b0fc-128">Okuma davranışını hello ve hello parçası işlemi aldıklarında hello iletisi siliniyor hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryolarda en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="8b0fc-129">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="8b0fc-130">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="8b0fc-131">Merhaba, `peek_lock` parametresi çok ayarlanırsa**True**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="8b0fc-132">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="8b0fc-133">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar tarafından arama hello alma işleminin **silmek** hello yöntemi **ileti** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="8b0fc-134">Merhaba **silmek** yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="8b0fc-135">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="8b0fc-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="8b0fc-136">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="8b0fc-137">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz **kilidini** hello yöntemi **ileti** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="8b0fc-138">Bu hizmet veri yolu toounlock selamlama iletisine hello sıra içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="8b0fc-139">Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve hello tooprocess önce iletiyi hello hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine otomatik olarak kilitlenmeden kilit zaman aşımı dolmadan ve yeniden alınan kullanılabilir toobe yapın.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="8b0fc-140">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor **silmek** yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="8b0fc-141">Bu genellikle adlandırılır **en az bir kez işleme**, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="8b0fc-142">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="8b0fc-143">Bu genellikle hello kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b0fc-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8b0fc-144">Next steps</span></span>
<span data-ttu-id="8b0fc-145">Service Bus kuyruklarını hello temel bilgileri öğrendiniz, daha fazla Bu makaleler toolearn bakın.</span><span class="sxs-lookup"><span data-stu-id="8b0fc-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="8b0fc-146">[Kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="8b0fc-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

