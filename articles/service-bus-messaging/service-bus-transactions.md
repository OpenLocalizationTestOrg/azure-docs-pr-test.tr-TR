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
# <a name="overview-of-service-bus-transaction-processing"></a>Hizmet veri yolu işlem genel bakış
Bu makalede Azure hizmet veri yolu hello işlem özellikleri açıklanmaktadır. Merhaba tartışma çoğunu hello tarafından gösterilen [hizmet veri yolu örnek ile atomik işlemleri](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). Bu makalede işlem ve hello sınırlı tooan genel bakıştır *aracılığıyla gönderme* Service Bus hello atomik işlemleri örnek kapsamında daha geniş ve daha karmaşık olsa da, özelliği.

## <a name="transactions-in-service-bus"></a>Hizmet veri yolu işlemleri
A [işlem](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) iki veya daha fazla işlem içine gruplandıran bir *yürütme kapsam*. Doğası gereği, böyle bir işlem tooa işlemlerinin gruba ait tüm işlemlerin başarılı veya başarısız ortaklaşa emin olmalısınız. Bu bakımdan işlemleri genellikle başvurulan tooas olan bir birim olarak hareket *kararlılık*. 

Hizmet veri yolu işlem ileti Aracısı olduğunu ve kendi ileti depoları karşı tüm iç işlemleri için işlem bütünlüğünü sağlar. Service Bus içinde iletilerinin taşıma iletileri tooa gibi tüm aktarımları [sahipsiz sırayı](service-bus-dead-letter-queues.md) veya [otomatik iletme](service-bus-auto-forwarding.md) varlıklar arasındaki iletileri işlem şunlardır. Bu nedenle, hizmet veri yolu ileti kabul ediyorsa, zaten olduğundan depolanan ve bir sıra numarasıyla etiketli. Daha sonra Service Bus içinde ileti aktarımlar Eşgüdümlü işlemleri arasında varlıklardır ve hiçbiri (kaynak başarılı ve başarısız hedef) tooloss götürür veya tooduplication (kaynak başarısız olur ve hedef başarılı) Başlangıç iletisi.

Hizmet veri yolu bir işlem tek bir Mesajlaşma varlık (kuyruk, konu, abonelik) hello kapsam içinde karşı gruplandırma işlemleri destekler. Örneğin, bir işlem kapsamı içinde birkaç iletileri tooone sıradan gönderebilir ve hello işlem başarıyla tamamlandığında Merhaba iletileri yalnızca kaydedilmiş toohello sıranın günlük olur.

## <a name="operations-within-a-transaction-scope"></a>Bir işlem kapsamı içinde işlemleri
bir işlem kapsamı içinde gerçekleştirilebilir hello işlem aşağıdaki gibidir:

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: SendBatchAsync SendAsync, SendBatch, Gönder 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: tam, CompleteAsync, durdurma, AbandonAsync, sahipsiz, DeadletterAsync, erteleme, DeferAsync, RenewLock, RenewLockAsync 

Alma işlemleri olmayan dahil Merhaba uygulaması hello kullanarak iletileri alması varsayıldığından [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) bazı içinde mod döngü almak veya ile bir [Onmessageoptions](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) geri arama, ve işlem yalnızca sonra açılır işleme selamlama iletisine için kapsam.

Merhaba değerlendirme selamlama iletisine (tam abandon, teslim edilemeyen erteleneceği,), ardından hello kapsamını ve bağımlı, içinde hello oluşur hello işlem genel sonucu.

## <a name="transfers-and-send-via"></a>Aktarımları ve "aracılığıyla Gönder"
Hizmet veri yolu tooenable işlem handover bir sıra tooa işlemcisini ve ardından tooanother kuyruk verilerini destekleyen *aktarımları*. Aktarım işlemi bir gönderen bir ileti tooa "aktarımı sırası" ilk gönderir. ve sağlam aynı hello otomatik iletme yeteneği bağımlı uygulama aktarım hello kullanarak hedef sıra hello ileti toohello hedeflenen hello aktarımı sıra hemen taşır . Merhaba hiçbir zaman onu hello aktarımı sıranın Tüketiciler için görünür olacağı şekilde taahhüt toohello aktarımı sıranın günlük iletisidir.

Merhaba aktarımı sıranın kendisine hello gönderenin giriş iletileri hello kaynağı hello güç bu işlem yeteneğinin görünür olur. Diğer bir deyişle, Service Bus hello ileti toohello hedef sırası hello aktarımı sırası "ile" tam gerçekleştirilirken aktarabilirsiniz (veya erteleneceği, ya da teslim edilemeyen) hello giriş ileti, tüm tek bir atomik işlemle işlemi. 

### <a name="see-it-in-code"></a>Kodda bakın
tooset böyle aktarımları yukarı hello hedef sıra hello aktarımı sıra aracılığıyla hedefleyen bir ileti gönderen oluşturun. Bu aynı sıraya alınan iletileri çeken bir alıcı da sahip olursunuz. Örneğin:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Aşağıdaki örneğine hello olduğu gibi bu öğelerden sonra basit bir işlem kullanır:

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

## <a name="next-steps"></a>Sonraki adımlar

Makaleler hizmet veri yolu kuyrukları hakkında daha fazla bilgi için aşağıdaki hello bakın:

* [Hizmet veri yolu varlıklarını otomatik iletme ile zincirleme](service-bus-auto-forwarding.md)
* [Otomatik iletme örnek](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Hizmet veri yolu örnek ile atomik işlemleri](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Azure kuyruklar ve hizmet veri yolu sıraları karşılaştırılan](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [Nasıl toouse Service Bus kuyrukları](service-bus-dotnet-get-started-with-queues.md)

