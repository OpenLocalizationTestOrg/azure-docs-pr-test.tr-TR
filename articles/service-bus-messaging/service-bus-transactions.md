---
title: "Azure hizmet veri yolundaki işlem aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="21fe8-103">Hizmet veri yolu işlem genel bakış</span><span class="sxs-lookup"><span data-stu-id="21fe8-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="21fe8-104">Bu makalede Azure hizmet veri yolu hello işlem özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="21fe8-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="21fe8-105">Merhaba tartışma çoğunu hello tarafından gösterilen [hizmet veri yolu örnek ile atomik işlemleri](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="21fe8-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="21fe8-106">Bu makalede işlem ve hello sınırlı tooan genel bakıştır *aracılığıyla gönderme* Service Bus hello atomik işlemleri örnek kapsamında daha geniş ve daha karmaşık olsa da, özelliği.</span><span class="sxs-lookup"><span data-stu-id="21fe8-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="21fe8-107">Hizmet veri yolu işlemleri</span><span class="sxs-lookup"><span data-stu-id="21fe8-107">Transactions in Service Bus</span></span>
<span data-ttu-id="21fe8-108">A [işlem](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) iki veya daha fazla işlem içine gruplandıran bir *yürütme kapsam*.</span><span class="sxs-lookup"><span data-stu-id="21fe8-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="21fe8-109">Doğası gereği, böyle bir işlem tooa işlemlerinin gruba ait tüm işlemlerin başarılı veya başarısız ortaklaşa emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="21fe8-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="21fe8-110">Bu bakımdan işlemleri genellikle başvurulan tooas olan bir birim olarak hareket *kararlılık*.</span><span class="sxs-lookup"><span data-stu-id="21fe8-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="21fe8-111">Hizmet veri yolu işlem ileti Aracısı olduğunu ve kendi ileti depoları karşı tüm iç işlemleri için işlem bütünlüğünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="21fe8-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="21fe8-112">Service Bus içinde iletilerinin taşıma iletileri tooa gibi tüm aktarımları [sahipsiz sırayı](service-bus-dead-letter-queues.md) veya [otomatik iletme](service-bus-auto-forwarding.md) varlıklar arasındaki iletileri işlem şunlardır.</span><span class="sxs-lookup"><span data-stu-id="21fe8-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="21fe8-113">Bu nedenle, hizmet veri yolu ileti kabul ediyorsa, zaten olduğundan depolanan ve bir sıra numarasıyla etiketli.</span><span class="sxs-lookup"><span data-stu-id="21fe8-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="21fe8-114">Daha sonra Service Bus içinde ileti aktarımlar Eşgüdümlü işlemleri arasında varlıklardır ve hiçbiri (kaynak başarılı ve başarısız hedef) tooloss götürür veya tooduplication (kaynak başarısız olur ve hedef başarılı) Başlangıç iletisi.</span><span class="sxs-lookup"><span data-stu-id="21fe8-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="21fe8-115">Hizmet veri yolu bir işlem tek bir Mesajlaşma varlık (kuyruk, konu, abonelik) hello kapsam içinde karşı gruplandırma işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="21fe8-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="21fe8-116">Örneğin, bir işlem kapsamı içinde birkaç iletileri tooone sıradan gönderebilir ve hello işlem başarıyla tamamlandığında Merhaba iletileri yalnızca kaydedilmiş toohello sıranın günlük olur.</span><span class="sxs-lookup"><span data-stu-id="21fe8-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="21fe8-117">Bir işlem kapsamı içinde işlemleri</span><span class="sxs-lookup"><span data-stu-id="21fe8-117">Operations within a transaction scope</span></span>
<span data-ttu-id="21fe8-118">bir işlem kapsamı içinde gerçekleştirilebilir hello işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="21fe8-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="21fe8-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: SendBatchAsync SendAsync, SendBatch, Gönder</span><span class="sxs-lookup"><span data-stu-id="21fe8-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="21fe8-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: tam, CompleteAsync, durdurma, AbandonAsync, sahipsiz, DeadletterAsync, erteleme, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="21fe8-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="21fe8-121">Alma işlemleri olmayan dahil Merhaba uygulaması hello kullanarak iletileri alması varsayıldığından [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) bazı içinde mod döngü almak veya ile bir [Onmessageoptions](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) geri arama, ve işlem yalnızca sonra açılır işleme selamlama iletisine için kapsam.</span><span class="sxs-lookup"><span data-stu-id="21fe8-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="21fe8-122">Merhaba değerlendirme selamlama iletisine (tam abandon, teslim edilemeyen erteleneceği,), ardından hello kapsamını ve bağımlı, içinde hello oluşur hello işlem genel sonucu.</span><span class="sxs-lookup"><span data-stu-id="21fe8-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="21fe8-123">Aktarımları ve "aracılığıyla Gönder"</span><span class="sxs-lookup"><span data-stu-id="21fe8-123">Transfers and "send via"</span></span>
<span data-ttu-id="21fe8-124">Hizmet veri yolu tooenable işlem handover bir sıra tooa işlemcisini ve ardından tooanother kuyruk verilerini destekleyen *aktarımları*.</span><span class="sxs-lookup"><span data-stu-id="21fe8-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="21fe8-125">Aktarım işlemi bir gönderen bir ileti tooa "aktarımı sırası" ilk gönderir. ve sağlam aynı hello otomatik iletme yeteneği bağımlı uygulama aktarım hello kullanarak hedef sıra hello ileti toohello hedeflenen hello aktarımı sıra hemen taşır .</span><span class="sxs-lookup"><span data-stu-id="21fe8-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="21fe8-126">Merhaba hiçbir zaman onu hello aktarımı sıranın Tüketiciler için görünür olacağı şekilde taahhüt toohello aktarımı sıranın günlük iletisidir.</span><span class="sxs-lookup"><span data-stu-id="21fe8-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="21fe8-127">Merhaba aktarımı sıranın kendisine hello gönderenin giriş iletileri hello kaynağı hello güç bu işlem yeteneğinin görünür olur.</span><span class="sxs-lookup"><span data-stu-id="21fe8-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="21fe8-128">Diğer bir deyişle, Service Bus hello ileti toohello hedef sırası hello aktarımı sırası "ile" tam gerçekleştirilirken aktarabilirsiniz (veya erteleneceği, ya da teslim edilemeyen) hello giriş ileti, tüm tek bir atomik işlemle işlemi.</span><span class="sxs-lookup"><span data-stu-id="21fe8-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="21fe8-129">Kodda bakın</span><span class="sxs-lookup"><span data-stu-id="21fe8-129">See it in code</span></span>
<span data-ttu-id="21fe8-130">tooset böyle aktarımları yukarı hello hedef sıra hello aktarımı sıra aracılığıyla hedefleyen bir ileti gönderen oluşturun.</span><span class="sxs-lookup"><span data-stu-id="21fe8-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="21fe8-131">Bu aynı sıraya alınan iletileri çeken bir alıcı da sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="21fe8-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="21fe8-132">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="21fe8-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="21fe8-133">Aşağıdaki örneğine hello olduğu gibi bu öğelerden sonra basit bir işlem kullanır:</span><span class="sxs-lookup"><span data-stu-id="21fe8-133">A simple transaction then uses these elements, as in hello following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="21fe8-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21fe8-134">Next steps</span></span>

<span data-ttu-id="21fe8-135">Makaleler hizmet veri yolu kuyrukları hakkında daha fazla bilgi için aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="21fe8-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="21fe8-136">Hizmet veri yolu varlıklarını otomatik iletme ile zincirleme</span><span class="sxs-lookup"><span data-stu-id="21fe8-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="21fe8-137">Otomatik iletme örnek</span><span class="sxs-lookup"><span data-stu-id="21fe8-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="21fe8-138">Hizmet veri yolu örnek ile atomik işlemleri</span><span class="sxs-lookup"><span data-stu-id="21fe8-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="21fe8-139">Azure kuyruklar ve hizmet veri yolu sıraları karşılaştırılan</span><span class="sxs-lookup"><span data-stu-id="21fe8-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="21fe8-140">Nasıl toouse Service Bus kuyrukları</span><span class="sxs-lookup"><span data-stu-id="21fe8-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

