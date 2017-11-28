---
title: "Azure hizmet veri yolundaki işlem genel bakış | Microsoft Docs"
description: "Azure Service Bus atomik işlemleri ve aracılığıyla gönderme genel bakış"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: a88f2d81ab43e38c9363a67aaefc178b47bfb259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="8dd8c-103">Hizmet veri yolu işlem genel bakış</span><span class="sxs-lookup"><span data-stu-id="8dd8c-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="8dd8c-104">Bu makalede Azure hizmet veri yolu işlem özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="8dd8c-105">Tartışma çoğunu tarafından gösterilen [hizmet veri yolu örnek ile atomik işlemleri](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="8dd8c-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="8dd8c-106">Bu makalede işlem genel bir bakış için sınırlıdır ve *aracılığıyla gönderme* Service Bus atomik işlemleri örnek kapsamında daha geniş ve daha karmaşık olsa da, özelliği.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="8dd8c-107">Hizmet veri yolu işlemleri</span><span class="sxs-lookup"><span data-stu-id="8dd8c-107">Transactions in Service Bus</span></span>
<span data-ttu-id="8dd8c-108">A [işlem](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) iki veya daha fazla işlem içine gruplandıran bir *yürütme kapsam*.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="8dd8c-109">Doğası gereği, böyle bir işlem işlemlerinin belirli bir gruba ait tüm işlemlerin başarılı veya başarısız ortaklaşa emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="8dd8c-110">Bu bakımdan genellikle olarak adlandırılır tek bir birim olarak hareketleri hareket *kararlılık*.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="8dd8c-111">Hizmet veri yolu işlem ileti Aracısı olduğunu ve kendi ileti depoları karşı tüm iç işlemleri için işlem bütünlüğünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="8dd8c-112">Aktarımlar iletileri taşıma gibi iletilerinin Service Bus içinde bir [sahipsiz sırayı](service-bus-dead-letter-queues.md) veya [otomatik iletme](service-bus-auto-forwarding.md) varlıklar arasındaki iletileri işlem şunlardır.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="8dd8c-113">Bu nedenle, hizmet veri yolu ileti kabul ediyorsa, zaten olduğundan depolanan ve bir sıra numarasıyla etiketli.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="8dd8c-114">Daha sonra Service Bus içinde ileti aktarımlar Eşgüdümlü işlemleri arasında varlıklardır ve hiçbiri kaybına neden (başarılı kaynak ve hedef başarısız) veya çoğaltma için (kaynak başarısız olur ve hedef başarılı) iletisi.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="8dd8c-115">Hizmet veri yolu bir işlem tek bir Mesajlaşma varlık (kuyruk, konu, abonelik) kapsamındaki karşı gruplandırma işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="8dd8c-116">Örneğin, bir işlem kapsamı içinde bir kuyruktan çeşitli iletiler gönderebilir ve işlem başarıyla tamamlandığında iletileri yalnızca sıra günlüğe kaydedilmiş olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="8dd8c-117">Bir işlem kapsamı içinde işlemleri</span><span class="sxs-lookup"><span data-stu-id="8dd8c-117">Operations within a transaction scope</span></span>
<span data-ttu-id="8dd8c-118">Bir işlem kapsamı içinde gerçekleştirilen işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8dd8c-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="8dd8c-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: SendBatchAsync SendAsync, SendBatch, Gönder</span><span class="sxs-lookup"><span data-stu-id="8dd8c-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="8dd8c-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: tam, CompleteAsync, durdurma, AbandonAsync, sahipsiz, DeadletterAsync, erteleme, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="8dd8c-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="8dd8c-121">Alma işlemleri olmayan dahil, uygulamayı kullanarak iletileri alması varsayıldığından [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) bazı içinde mod döngü almak veya ile bir [Onmessageoptions](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) geri ve yalnızca ardından iletiyi işlemek için bir işlem kapsamı açar.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="8dd8c-122">(Tam abandon, teslim edilemeyen erteleneceği,) ileti değerlendirme kapsamında ve bağımlı üzerinde genel işlem sonucunu sonra oluşur.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="8dd8c-123">Aktarımları ve "aracılığıyla Gönder"</span><span class="sxs-lookup"><span data-stu-id="8dd8c-123">Transfers and "send via"</span></span>
<span data-ttu-id="8dd8c-124">Bir kuyruk verilerini bir işlemci ve ardından üzere başka bir sıra işlem handover etkinleştirmek için Service Bus destekler *aktarımları*.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="8dd8c-125">Aktarım işlemi bir gönderen bir "aktarımı kuyruğuna" ilk ileti gönderir ve aktarımı sıranın otomatik iletme yeteneği kullanır aynı güçlü aktarım uygulamasını kullanarak hedeflenen hedef sırasındaki ileti hemen taşır.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="8dd8c-126">İleti hiçbir zaman bu aktarımı sıranın Tüketiciler için görünür olacağı şekilde transfer sıranın günlüğüne taahhüt eder.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="8dd8c-127">Aktarma sırası gönderenin giriş iletileri kaynağı olduğunda bu işlem özelliği gücünü belirgin olur.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="8dd8c-128">Diğer bir deyişle, hizmet veri yolu ileti hedef sırasına aktarımı sıranın "ile" tam gerçekleştirilirken aktarabilirsiniz (veya erteleneceği, ya da teslim edilemeyen) giriş ileti, tüm tek bir atomik işlemle işlemi.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="8dd8c-129">Kodda bakın</span><span class="sxs-lookup"><span data-stu-id="8dd8c-129">See it in code</span></span>
<span data-ttu-id="8dd8c-130">Bu tür aktarımları ayarlamak için hedef sıra aktarımı kuyruk üzerinden hedefleyen bir ileti gönderen oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="8dd8c-131">Bu aynı sıraya alınan iletileri çeken bir alıcı da sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="8dd8c-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="8dd8c-132">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="8dd8c-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="8dd8c-133">Aşağıdaki örnekte olduğu gibi bu öğelerden sonra basit bir işlem kullanır:</span><span class="sxs-lookup"><span data-stu-id="8dd8c-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="8dd8c-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8dd8c-134">Next steps</span></span>

<span data-ttu-id="8dd8c-135">Service Bus kuyruklarını hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="8dd8c-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="8dd8c-136">Hizmet veri yolu varlıklarını otomatik iletme ile zincirleme</span><span class="sxs-lookup"><span data-stu-id="8dd8c-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="8dd8c-137">Otomatik iletme örnek</span><span class="sxs-lookup"><span data-stu-id="8dd8c-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="8dd8c-138">Hizmet veri yolu örnek ile atomik işlemleri</span><span class="sxs-lookup"><span data-stu-id="8dd8c-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="8dd8c-139">Azure kuyruklar ve hizmet veri yolu sıraları karşılaştırılan</span><span class="sxs-lookup"><span data-stu-id="8dd8c-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="8dd8c-140">Service Bus kuyruklarını kullanma</span><span class="sxs-lookup"><span data-stu-id="8dd8c-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

