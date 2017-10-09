---
title: "aaaHow toouse Azure Service Bus kuyrukları ile Söyleniş | Microsoft Docs"
description: "Azure'da nasıl toouse Service Bus kuyrukları öğrenin. Ruby içinde yazılan kod örnekleri."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a><span data-ttu-id="1af43-104">Ruby ile nasıl toouse Service Bus kuyrukları</span><span class="sxs-lookup"><span data-stu-id="1af43-104">How toouse Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="1af43-105">Bu kılavuzda açıklanmaktadır nasıl toouse Service Bus kuyruklarını.</span><span class="sxs-lookup"><span data-stu-id="1af43-105">This guide describes how toouse Service Bus queues.</span></span> <span data-ttu-id="1af43-106">Merhaba örnekler içinde Ruby yazılır ve hello Azure gem kullanır.</span><span class="sxs-lookup"><span data-stu-id="1af43-106">hello samples are written in Ruby and use hello Azure gem.</span></span> <span data-ttu-id="1af43-107">Merhaba kapsanan senaryolar dahil **ileti gönderme ve alma sıra oluşturma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="1af43-107">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="1af43-108">Service Bus kuyruklarını hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="1af43-108">For more information about Service Bus queues, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a><span data-ttu-id="1af43-109">Nasıl bir kuyruk toocreate</span><span class="sxs-lookup"><span data-stu-id="1af43-109">How toocreate a queue</span></span>
<span data-ttu-id="1af43-110">Merhaba **Azure::ServiceBusService** nesne kuyruklarla toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="1af43-110">hello **Azure::ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="1af43-111">toocreate bir sıra kullanmak hello `create_queue()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1af43-111">toocreate a queue, use hello `create_queue()` method.</span></span> <span data-ttu-id="1af43-112">Merhaba aşağıdaki örnekte bir kuyruk oluşturur veya tüm hataları yazdırır.</span><span class="sxs-lookup"><span data-stu-id="1af43-112">hello following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="1af43-113">Ayrıca iletebilirsiniz bir **Azure::ServiceBus::Queue** nesne ek seçeneklerle toooverride hello varsayılan sıra ayarları, ileti zaman toolive veya en büyük sıra boyutu gibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1af43-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you toooverride hello default queue settings, such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="1af43-114">Aşağıdaki örnek hello nasıl tooset en büyük sıra boyutu too5 GB hello ve toolive too1 minute zaman gösterir:</span><span class="sxs-lookup"><span data-stu-id="1af43-114">hello following example shows how tooset hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a><span data-ttu-id="1af43-115">Nasıl toosend iletileri tooa sırası</span><span class="sxs-lookup"><span data-stu-id="1af43-115">How toosend messages tooa queue</span></span>
<span data-ttu-id="1af43-116">ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `send_queue_message()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1af43-116">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1af43-117">İletileri çok gönderilen (ve öğesinden alınan) hizmet kuyruklar veri yolu **Azure::ServiceBus::BrokeredMessage** nesneleri ve bir standart özellikler kümesi sahip (gibi `label` ve `time_to_live`), kullanılan toohold bir sözlüğü Özel uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi.</span><span class="sxs-lookup"><span data-stu-id="1af43-117">Messages sent too(and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="1af43-118">Bir uygulama selamlama iletisine bir dize değeri geçirerek hello hello ileti gövdesini ayarlayabilir ve gerekli tüm standart özellikleri varsayılan değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="1af43-118">An application can set hello body of hello message by passing a string value as hello message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="1af43-119">Merhaba aşağıdaki örnekte nasıl toosend adlı bir sınama iletisi toohello sırası gösteren `test-queue` kullanarak `send_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="1af43-119">hello following example demonstrates how toosend a test message toohello queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="1af43-120">Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1af43-120">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1af43-121">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="1af43-121">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1af43-122">Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="1af43-122">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="1af43-123">Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="1af43-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-queue"></a><span data-ttu-id="1af43-124">Nasıl tooreceive kuyruktan iletileri</span><span class="sxs-lookup"><span data-stu-id="1af43-124">How tooreceive messages from a queue</span></span>
<span data-ttu-id="1af43-125">İletileri hello kullanarak bir kuyruktan alınan `receive_queue_message()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1af43-125">Messages are received from a queue using hello `receive_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1af43-126">Varsayılan olarak, iletileri okumak ve hello sıradan silinir olmadan kilitli.</span><span class="sxs-lookup"><span data-stu-id="1af43-126">By default, messages are read and locked without being deleted from hello queue.</span></span> <span data-ttu-id="1af43-127">Ayarı hello tarafından okurken ancak iletileri hello sıradan silebilirsiniz `:peek_lock` çok seçenek**false**.</span><span class="sxs-lookup"><span data-stu-id="1af43-127">However, you can delete messages from hello queue as they are read by setting hello `:peek_lock` option too**false**.</span></span>

<span data-ttu-id="1af43-128">Merhaba varsayılan davranışı okumak ve ayrıca, iletilere olası toosupport uygulamaları kılar bir iki aşamalı işlemi silme hello yapar.</span><span class="sxs-lookup"><span data-stu-id="1af43-128">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1af43-129">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="1af43-129">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="1af43-130">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `delete_queue_message()` yöntemi ve parametre olarak silinmiş hello ileti toobe sağlama.</span><span class="sxs-lookup"><span data-stu-id="1af43-130">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_queue_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="1af43-131">Merhaba `delete_queue_message()` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1af43-131">hello `delete_queue_message()` method will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="1af43-132">Merhaba, `:peek_lock` parametresi çok ayarlanırsa**yanlış**, okuma ve hello iletisi siliniyor hello basit model olur ve senaryoları bir uygulama içinde tolerans hello olayı içinde ileti işlenirken değil en iyi şekilde çalışır bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="1af43-132">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="1af43-133">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="1af43-133">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="1af43-134">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında, kullanılan olarak işaretlenmiş olduğundan, onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="1af43-134">Because Service Bus has marked hello message as being consumed, when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="1af43-135">Merhaba aşağıdaki örnekte nasıl tooreceive ve işlem iletileri kullanarak gösteren `receive_queue_message()`.</span><span class="sxs-lookup"><span data-stu-id="1af43-135">hello following example demonstrates how tooreceive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="1af43-136">Merhaba örneği ilk alır ve bir iletiyi kullanarak siler `:peek_lock` çok ayarlamak**false**, ardından başka bir ileti alır ve ardından iletiyi kullanarak siler hello `delete_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="1af43-136">hello example first receives and deletes a message by using `:peek_lock` set too**false**, then it receives another message and then deletes hello message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1af43-137">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="1af43-137">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="1af43-138">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="1af43-138">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1af43-139">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlock_queue_message()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="1af43-139">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_queue_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="1af43-140">Bu çağrı nedenler Service Bus toounlock hello hello sıra içinde ileti gönderme ve yeniden alınan kullanılabilir toobe olun ya da göre hello aynı uygulama veya başka bir kullanıcı uygulama tarafından kullanma.</span><span class="sxs-lookup"><span data-stu-id="1af43-140">This call causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1af43-141">Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus hello iletinin kilidini açar hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe yapar.</span><span class="sxs-lookup"><span data-stu-id="1af43-141">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="1af43-142">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `delete_queue_message()` yöntemi çağrıldıktan sonra hello ileti yeniden teslim toohello uygulama başlatıldığında içindir.</span><span class="sxs-lookup"><span data-stu-id="1af43-142">In hello event that hello application crashes after processing hello message but before hello `delete_queue_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="1af43-143">Bu işlem genellikle adlı *en az bir kez işleme*; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="1af43-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="1af43-144">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1af43-144">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="1af43-145">Bu genellikle hello kullanılarak elde edilen `message_id` teslimat denemelerinde hello iletinin özelliği.</span><span class="sxs-lookup"><span data-stu-id="1af43-145">This is often achieved using hello `message_id` property of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1af43-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1af43-146">Next steps</span></span>
<span data-ttu-id="1af43-147">Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="1af43-147">Now that you've learned hello basics of Service Bus queues, follow these links toolearn more.</span></span>

* <span data-ttu-id="1af43-148">Genel Bakış [kuyruklar, konu başlıkları ve abonelikler](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="1af43-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="1af43-149">Merhaba ziyaret [Ruby için Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) github'daki.</span><span class="sxs-lookup"><span data-stu-id="1af43-149">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="1af43-150">Bu makalede açıklanan hello Azure Service Bus kuyrukları ve Azure hello ele alınan sıraları arasında bir karşılaştırma için [nasıl toouse ruby'den kuyruk depolama](../storage/queues/storage-ruby-how-to-use-queue-storage.md) makale için bkz: [Azure kuyrukları ve Azure hizmet veri yolu kuyrukları - karşılaştırma ve Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="1af43-150">For a comparison between hello Azure Service Bus queues discussed in this article and Azure Queues discussed in hello [How toouse Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>

