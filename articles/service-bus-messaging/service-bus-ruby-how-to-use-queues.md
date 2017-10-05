---
title: "Ruby ile Azure Service Bus kuyruklarını kullanma | Microsoft Docs"
description: "Azure'da Service Bus kuyruklarını kullanmayı öğrenin. Ruby içinde yazılan kod örnekleri."
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
ms.openlocfilehash: 357a7277dd42b6973cf35a9f642b8eec36a745e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-ruby"></a><span data-ttu-id="3fe84-104">Ruby ile Service Bus kuyruklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="3fe84-104">How to use Service Bus queues with Ruby</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="3fe84-105">Bu kılavuz, Service Bus kuyruklarını kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="3fe84-105">This guide describes how to use Service Bus queues.</span></span> <span data-ttu-id="3fe84-106">Örnekler Ruby yazılır ve Azure gem kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fe84-106">The samples are written in Ruby and use the Azure gem.</span></span> <span data-ttu-id="3fe84-107">Kapsamdaki senaryolar dahil **ileti gönderme ve alma sıra oluşturma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="3fe84-107">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="3fe84-108">Service Bus kuyruklarını hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fe84-108">For more information about Service Bus queues, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="3fe84-109">Bir sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fe84-109">How to create a queue</span></span>
<span data-ttu-id="3fe84-110">**Azure::ServiceBusService** nesne kuyruklarla çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fe84-110">The **Azure::ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="3fe84-111">Bir kuyruk oluşturmak için kullanmak `create_queue()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3fe84-111">To create a queue, use the `create_queue()` method.</span></span> <span data-ttu-id="3fe84-112">Aşağıdaki örnekte bir kuyruk oluşturur veya hataları yazdırır.</span><span class="sxs-lookup"><span data-stu-id="3fe84-112">The following example creates a queue or prints out any errors.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

<span data-ttu-id="3fe84-113">Ayrıca iletebilirsiniz bir **Azure::ServiceBus::Queue** nesne ek seçenekleri, Canlı veya en büyük sıra boyutu ileti süresi gibi varsayılan sırası ayarlarını geçersiz kılmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fe84-113">You can also pass a **Azure::ServiceBus::Queue** object with additional options, which enables you to override the default queue settings, such as message time to live or maximum queue size.</span></span> <span data-ttu-id="3fe84-114">Aşağıdaki örnekte, en büyük sıra boyutu 5 GB ve saat 1 dakika Canlı ayarlamak gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="3fe84-114">The following example shows how to set the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-to-send-messages-to-a-queue"></a><span data-ttu-id="3fe84-115">Kuyruğa ileti göndermek nasıl</span><span class="sxs-lookup"><span data-stu-id="3fe84-115">How to send messages to a queue</span></span>
<span data-ttu-id="3fe84-116">Uygulama çağrılarınızı bir Service Bus kuyruğuna bir ileti göndermek için `send_queue_message()` yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3fe84-116">To send a message to a Service Bus queue, your application calls the `send_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3fe84-117">İletileri gönderilen (ve öğesinden alınan) hizmet kuyruklar veri yolu **Azure::ServiceBus::BrokeredMessage** nesneleri ve bir standart özellikler kümesi sahip (gibi `label` ve `time_to_live`), bir uygulamaya özgü özel özellikleri tutmak için kullanılan bir sözlük ve rastgele uygulama verileri gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="3fe84-117">Messages sent to (and received from) Service Bus queues are **Azure::ServiceBus::BrokeredMessage** objects, and have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="3fe84-118">Uygulamanın iletiyi olarak bir dize değeri geçirerek ileti gövdesini ayarlayabilir ve gerekli tüm standart özellikleri varsayılan değerlerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="3fe84-118">An application can set the body of the message by passing a string value as the message and any required standard properties are populated with default values.</span></span>

<span data-ttu-id="3fe84-119">Aşağıdaki örnek adlı sırasına sınama iletisi göndermek nasıl gösterir `test-queue` kullanarak `send_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="3fe84-119">The following example demonstrates how to send a test message to the queue named `test-queue` using `send_queue_message()`:</span></span>

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

<span data-ttu-id="3fe84-120">Service Bus kuyrukları, [Standart katmanda](service-bus-premium-messaging.md) maksimum 256 KB ve [Premium katmanda](service-bus-premium-messaging.md) maksimum 1 MB ileti boyutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="3fe84-120">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3fe84-121">Standart ve özel uygulama özelliklerini içeren üst bilginin maksimum dosya boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="3fe84-121">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3fe84-122">Kuyrukta tutulan ileti sayısına ilişkin bir sınır yoktur ancak kuyruk tarafından tutulan iletilerin toplam boyutu için uç sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="3fe84-122">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="3fe84-123">Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="3fe84-123">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-queue"></a><span data-ttu-id="3fe84-124">Kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="3fe84-124">How to receive messages from a queue</span></span>
<span data-ttu-id="3fe84-125">İletileri kullanarak bir Sıraya alınan `receive_queue_message()` yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3fe84-125">Messages are received from a queue using the `receive_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3fe84-126">Varsayılan olarak, iletileri okumak ve sıradan silinir olmadan kilitli.</span><span class="sxs-lookup"><span data-stu-id="3fe84-126">By default, messages are read and locked without being deleted from the queue.</span></span> <span data-ttu-id="3fe84-127">Ayarlayarak okunduğu gibi ancak, ileti kuyruktan silebilirsiniz `:peek_lock` için seçenek **false**.</span><span class="sxs-lookup"><span data-stu-id="3fe84-127">However, you can delete messages from the queue as they are read by setting the `:peek_lock` option to **false**.</span></span>

<span data-ttu-id="3fe84-128">Varsayılan davranış, okuma ve ayrıca, iletilere uygulamaları desteklemek mümkün kılar bir iki aşamalı işlemi silme yapar.</span><span class="sxs-lookup"><span data-stu-id="3fe84-128">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3fe84-129">Service Bus bir istek aldığında bir sonraki kullanılacak iletiyi bulur, diğer tüketicilerin bu iletiyi almasını engellemek için kilitler ve ardından uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="3fe84-129">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="3fe84-130">Uygulama iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), çağırarak alma işleminin ikinci aşamasını tamamlar `delete_queue_message()` yöntemi ve parametre olarak silinecek ileti sağlama.</span><span class="sxs-lookup"><span data-stu-id="3fe84-130">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_queue_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="3fe84-131">`delete_queue_message()` Yöntemi iletiyi kullanılıyor olarak işaretler ve kuyruktan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3fe84-131">The `delete_queue_message()` method will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="3fe84-132">Varsa `:peek_lock` parametrenin ayarlanmış **yanlış**, okuma ve iletisi siliniyor basit model olur ve senaryoları bir uygulama içinde tolerans bir arıza olması durumunda bir ileti işlenirken değil en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3fe84-132">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="3fe84-133">Bu durumu daha iyi anlamak için müşterinin bir alma isteği bildirdiğini ve bu isteğin işlenmeden çöktüğünü varsayın.</span><span class="sxs-lookup"><span data-stu-id="3fe84-133">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="3fe84-134">Hizmet veri yolu ileti uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında, kullanılan olarak işaretlenmiş olduğundan, çökmenin öncesinde kullanılan iletiyi atlamış olur.</span><span class="sxs-lookup"><span data-stu-id="3fe84-134">Because Service Bus has marked the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="3fe84-135">Aşağıdaki örnek, kullanarak iletileri almak ve işlemek gösterilmiştir `receive_queue_message()`.</span><span class="sxs-lookup"><span data-stu-id="3fe84-135">The following example demonstrates how to receive and process messages using `receive_queue_message()`.</span></span> <span data-ttu-id="3fe84-136">Örnek ilk alır ve bir iletiyi kullanarak siler `:peek_lock` kümesine **false**, başka bir ileti alır ve kullanarak iletiyi siler `delete_queue_message()`:</span><span class="sxs-lookup"><span data-stu-id="3fe84-136">The example first receives and deletes a message by using `:peek_lock` set to **false**, then it receives another message and then deletes the message using `delete_queue_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3fe84-137">Uygulama çökmelerini ve okunmayan iletileri giderme</span><span class="sxs-lookup"><span data-stu-id="3fe84-137">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="3fe84-138">Service Bus, uygulamanızda gerçekleşen hataları veya ileti işlenirken oluşan zorlukları rahat bir şekilde ortadan kaldırmanıza yardımcı olmak için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fe84-138">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3fe84-139">Alıcı uygulamanın iletiyi herhangi bir nedenden dolayı işleyemedi sonra işleyememesi `unlock_queue_message()` yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3fe84-139">If a receiver application is unable to process the message for some reason, then it can call the `unlock_queue_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="3fe84-140">Bu çağrı, Service Bus hizmetinin Kuyruktaki iletinin kilidini açmasına ve iletiyi aynı veya başka bir kullanıcı uygulama tarafından tekrar alınabilir hale getirmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="3fe84-140">This call causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3fe84-141">Ayrıca kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve uygulama önce iletiyi işleyemezse (örneğin, uygulama çökerse) Service Bus otomatik olarak iletinin kilidini açar ve tekrar alınabilmesini sağlar kilit zaman aşımı dolmadan.</span><span class="sxs-lookup"><span data-stu-id="3fe84-141">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="3fe84-142">Uygulama iletiyi ancak önce çökmesi durumunda, `delete_queue_message()` yöntemi çağrıldıktan sonra yeniden başlatıldığında ileti uygulamaya tekrar teslim.</span><span class="sxs-lookup"><span data-stu-id="3fe84-142">In the event that the application crashes after processing the message but before the `delete_queue_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="3fe84-143">Bu işlem genellikle adlı *en az bir kez işleme*; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="3fe84-143">This process is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="3fe84-144">Senaryo yinelenen işlemeyi kabul etmiyorsa yinelenen ileti teslimine izin vermek için uygulama geliştiricilerin uygulamaya ilave bir mantık eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fe84-144">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="3fe84-145">Bu genellikle kullanılarak elde edilen `message_id` iletinin teslimat denemelerinde özelliği.</span><span class="sxs-lookup"><span data-stu-id="3fe84-145">This is often achieved using the `message_id` property of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fe84-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3fe84-146">Next steps</span></span>
<span data-ttu-id="3fe84-147">Artık Service Bus kuyruklarına ilişkin temel bilgileri öğrendiğinize göre, daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3fe84-147">Now that you've learned the basics of Service Bus queues, follow these links to learn more.</span></span>

* <span data-ttu-id="3fe84-148">Genel Bakış [kuyruklar, konu başlıkları ve abonelikler](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="3fe84-148">Overview of [queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="3fe84-149">Ziyaret [Ruby için Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) github'daki.</span><span class="sxs-lookup"><span data-stu-id="3fe84-149">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

<span data-ttu-id="3fe84-150">Bu makalede ele alınan Azure Service Bus kuyrukları ve Azure ele sıraları arasında bir karşılaştırma için [ruby'den kuyruk depolama kullanma](../storage/queues/storage-ruby-how-to-use-queue-storage.md) makale için bkz: [Azure kuyrukları ve Karşılaştırılan ve Contrasted Azure hizmet veri yolu kuyrukları -](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="3fe84-150">For a comparison between the Azure Service Bus queues discussed in this article and Azure Queues discussed in the [How to use Queue storage from Ruby](../storage/queues/storage-ruby-how-to-use-queue-storage.md) article, see [Azure Queues and Azure Service Bus Queues - Compared and Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>

