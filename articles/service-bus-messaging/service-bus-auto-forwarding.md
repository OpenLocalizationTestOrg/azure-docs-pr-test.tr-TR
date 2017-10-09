---
title: "aaaAuto iletme Azure Service Bus Mesajlaşma varlıkları | Microsoft Docs"
description: "Nasıl toochain bir hizmet veri yolu kuyruğu ya da abonelik tooanother kuyruk veya konu başlığı."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="4090f-103">Hizmet veri yolu varlıklarını otomatik iletme ile zincirleme</span><span class="sxs-lookup"><span data-stu-id="4090f-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="4090f-104">Merhaba Service Bus *otomatik iletme* özelliği sağlar, size, toochain bir sıraya veya abonelik tooanother sıra ya da hello parçası olan konu aynı ad.</span><span class="sxs-lookup"><span data-stu-id="4090f-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="4090f-105">Otomatik iletme etkinleştirildiğinde, Service Bus otomatik olarak hello ilk sırayı veya abonelik (kaynak) yerleştirilen iletileri kaldırır ve hello ikinci kuyruk veya konu (hedef) koyar.</span><span class="sxs-lookup"><span data-stu-id="4090f-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="4090f-106">Bunu hala olası toosend bir ileti toohello hedef varlık doğrudan olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4090f-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="4090f-107">Ayrıca, olası toochain sahipsiz sıraya, tooanother kuyruk veya konu gibi bir alt sırasına değil.</span><span class="sxs-lookup"><span data-stu-id="4090f-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="4090f-108">Otomatik iletme kullanma</span><span class="sxs-lookup"><span data-stu-id="4090f-108">Using auto-forwarding</span></span>
<span data-ttu-id="4090f-109">Otomatik iletme ayarı hello tarafından etkinleştirebilirsiniz [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] veya [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] Merhaba özellikleri [QueueDescription] [ QueueDescription] veya [SubscriptionDescription] [ SubscriptionDescription] hello olduğu gibi hello kaynağı için nesneler Aşağıdaki örnek.</span><span class="sxs-lookup"><span data-stu-id="4090f-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="4090f-110">Merhaba hedef varlık hello kaynak varlık oluşturulan hello aynı anda mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4090f-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="4090f-111">Merhaba hedef varlık mevcut değilse sorulan toocreate hello kaynak varlık Service Bus bir özel durum döndürür.</span><span class="sxs-lookup"><span data-stu-id="4090f-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="4090f-112">Tek bir konu çıkışı otomatik iletme tooscale kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4090f-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="4090f-113">Hizmet veri yolu sınırları hello [belirli bir konu Aboneliklerde sayısı](service-bus-quotas.md) too2, 000.</span><span class="sxs-lookup"><span data-stu-id="4090f-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="4090f-114">İkinci düzey konuları oluşturarak ek abonelikleri barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="4090f-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="4090f-115">Merhaba tarafından bağlı olmayan olsa bile Service Bus abonelik, ikinci düzey konuları ekleme hello sayısını sınırlama artırabilir, konunun genel üretilen işi hello unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4090f-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![Otomatik iletme senaryosu][0]

<span data-ttu-id="4090f-117">Otomatik iletme toodecouple ileti alıcıları göndericilerden de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4090f-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="4090f-118">Örneğin, üç modülden oluşur bir ERP sistemi göz önünde bulundurun: sipariş işleme, Envanter yönetimine ve müşteri ilişkileri yönetimi.</span><span class="sxs-lookup"><span data-stu-id="4090f-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="4090f-119">Bu modüllerin her biri, karşılık gelen bir konu içine sıraya alınan iletileri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4090f-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="4090f-120">Alice ve Bob tootheir müşteriler ile ilgili tüm iletileri ilginizi çekiyor mu satış temsilcisi markalarıdır.</span><span class="sxs-lookup"><span data-stu-id="4090f-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="4090f-121">Bu iletileri tooreceive Alice ve Bob kişisel bir sıra ve bir abonelik her tüm iletileri tootheir sırası otomatik olarak ilet hello ERP konuları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4090f-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![Otomatik iletme senaryosu][1]

<span data-ttu-id="4090f-123">Alice tatil, kendi kişisel kuyruk, yerine hello ERP konu kalırsa, dolar.</span><span class="sxs-lookup"><span data-stu-id="4090f-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="4090f-124">Bir satış temsilcisi herhangi bir iletisi aldı değil çünkü bu senaryoda, hello ERP konuları hiçbiri hiç kota ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4090f-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="4090f-125">Otomatik iletme konuları</span><span class="sxs-lookup"><span data-stu-id="4090f-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="4090f-126">Merhaba hedef varlık çok fazla ileti toplanır ve hello kotasını aşıyor veya hello hedef varlık devre dışıysa, hello kaynak varlık hello iletileri tooits ekler [sahipsiz sırayı](service-bus-dead-letter-queues.md) hello hedef alan kadar (veya hello varlık yeniden etkinleştirildi).</span><span class="sxs-lookup"><span data-stu-id="4090f-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="4090f-127">Açıkça almak ve bunları hello sahipsiz sıradan işlemek için bu iletileri hello sahipsiz sırasındaki toolive devam eder.</span><span class="sxs-lookup"><span data-stu-id="4090f-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="4090f-128">Ayrı ayrı konularını tooobtain birçok abonelikleri bileşik konuyla birlikte zincirleme kullanırken Orta sayıda hello birinci düzey konu Aboneliklerde ve hello ikinci düzey konuları birçok Aboneliklerde sahip önerilir.</span><span class="sxs-lookup"><span data-stu-id="4090f-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="4090f-129">Örneğin, birinci düzey konu 20 abonelikler ile bunların zincirleme her birini tooa ikinci düzey konu 200 abonelikler ile 200 Abonelikleri, birinci düzey konuyla daha yüksek verimlilik sağlar her zincirleme tooa ikinci düzey konu 20 abonelikler ile .</span><span class="sxs-lookup"><span data-stu-id="4090f-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="4090f-130">Hizmet veri yolu iletilen her ileti için bir işlem ödemenizi işler.</span><span class="sxs-lookup"><span data-stu-id="4090f-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="4090f-131">Örneğin, bir ileti tooa konu 20 abonelikler ile gönderme, bunların her birini tooanother kuyruk veya konu faturalandırılır 21 işlemleri olarak birinci düzey abonelikler hello iletinin bir kopyasını alırsanız tooauto iletme iletileri yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="4090f-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="4090f-132">toocreate zincirleme tooanother kuyruk veya konu aboneliği, hello abonelik hello oluşturan olmalıdır **Yönet** hello kaynak ve hedef varlık hello izinleri.</span><span class="sxs-lookup"><span data-stu-id="4090f-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="4090f-133">İletileri toohello kaynak konu yalnızca gerektirir gönderme **Gönder** hello kaynak konu izinleri.</span><span class="sxs-lookup"><span data-stu-id="4090f-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4090f-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4090f-134">Next steps</span></span>

<span data-ttu-id="4090f-135">Otomatik iletme hakkında ayrıntılı bilgi için aşağıdaki başvuru konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="4090f-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="4090f-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="4090f-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="4090f-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="4090f-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="4090f-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="4090f-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="4090f-139">Hizmet veri yolu performans iyileştirmeleri hakkında daha fazla toolearn bakın</span><span class="sxs-lookup"><span data-stu-id="4090f-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="4090f-140">Service Bus Mesajlaşma hizmeti kullanarak performans iyileştirmeleri için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="4090f-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="4090f-141">[Bölümlenmiş Mesajlaşma varlıkları][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="4090f-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
