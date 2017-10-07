---
title: "aaaService Bus teslim edilemeyen sıraları | Microsoft Docs"
description: "Azure Service Bus sıralarındaki genel bakış"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Hizmet veri yolu sıralarındaki genel bakış

Service Bus kuyrukları ve konu abonelikleri adlı ikincil alt bir sıra sağlayan bir *sahipsiz sırayı* (DLQ). Merhaba sahipsiz sırayı açıkça oluşturulan toobe gerekmez ve silinmiş veya başka yönetilen bağımsız hello ana varlığın olamaz.

Bu makalede Azure hizmet veri yolu sahipsiz kuyruklarda anlatılmaktadır. Merhaba tartışma çoğunu hello tarafından gösterilen [sıralarındaki örnek](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) github'da.
 
## <a name="hello-dead-letter-queue"></a>Merhaba eski ileti sırası

Merhaba sahipsiz sırayı Hello amacı tooany alıcı teslim toohold iletileri veya işlenemedi iletileri budur. İletileri hello DLQ ' kaldırıldı ve sahip denetlenir. Bir uygulama bir işleç yardımıyla, sorunları düzeltmek ve selamlama iletisine yeniden gönderin, bir hata oluştu hello olgu oturum ve düzeltme eylemlerini gerçekleştirin. 

Bir API ve protokolü açısından DLQ Merhaba iletileri yalnızca hello üst varlığın hello sahipsiz hareketi gönderilebilir çoğunlukla benzer tooany başka bir kuyrukta olmasıdır. Ayrıca, yaşam süresi gözlenir değil, ve teslim edilemeyen bir DLQ iletiden olamaz. Merhaba sahipsiz sırayı tam olarak gözlem kilidinin teslim ve işlem işlemleri destekler.

Merhaba DLQ otomatik olarak temizleneceği olduğuna dikkat edin. İletileri kalır hello DLQ, açıkça bunları hello DLQ ve çağrı almak kadar [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) hello teslim edilemeyen ileti üzerinde.

## <a name="moving-messages-toohello-dlq"></a>Taşıma toohello DLQ iletileri

Service Bus'ın toohello DLQ gelen Mesajlaşma altyapısı kendisini hello içinde gönderilen iletileri tooget neden birkaç aktivitelerde vardır. Bir uygulama aynı zamanda açıkça iletileri toohello DLQ taşıyabilirsiniz. 

Selamlama iletisine hello aracısı tarafından taşınan gibi kendi iç hello sürümü hello Aracısı çağırır gibi iki özellikler toohello iletisi eklenir [sahipsiz](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) selamlama iletisine yöntemi: `DeadLetterReason` ve `DeadLetterErrorDescription`.

Uygulamaları, kendi kodlarını hello tanımlayabilirsiniz `DeadLetterReason` özelliği, ancak değerler aşağıdaki hello sistem kümeleri hello.

| Koşul | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Her zaman |HeaderSizeExceeded |Bu akış için Hello boyutu kotası aşıldı. |
| ! TopicDescription.<br />EnableFilteringMessagesBeforePublishing ve SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |özel durum. GetType(). Adı |özel durum. İleti |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |Selamlama iletisine süresi ve kullanılmayan lettered. |
| SubscriptionDescription.RequiresSession |Oturum kimliği null şeklindedir. |Etkin oturum varlık, bir oturum tanımlayıcısı null bir ileti izin vermez. |
| ! Sahipsiz Sıra |MaxTransferHopCountExceeded |Null |
| Uygulama kullanılmayan lettering açık |Uygulama tarafından belirtilen |Uygulama tarafından belirtilen |

## <a name="exceeding-maxdeliverycount"></a>MaxDeliveryCount aşan
Kuyruklar ve abonelikler sahip bir [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) ve [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) özelliği sırasıyla; hello varsayılan değer 10'dur. Her bir ileti teslim kilidi altında ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)), ya da açıkça olmuştur ancak terk veya hello kilit süresi doldu, hello iletinin [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) olduğu artırılır. Zaman [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) aşıyor [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), hello iletisidir taşınan toohello hello belirtme DLQ `MaxDeliveryCountExceeded` neden kodu.

Bu davranışı devre dışı bırakılamaz, ancak ayarlayabileceğiniz [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa çok büyük bir sayı.

## <a name="exceeding-timetolive"></a>TimeToLive aşan
Ne zaman hello [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) veya [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) özelliği çok ayarlanmış**true** (Merhaba varsayılandır **false**), tüm süresi dolan iletileri taşınan toohello hello belirtme DLQ olan `TTLExpiredException` neden kodu.

Süresi dolan iletileri yalnızca temizlenir ve hello ana sıranın veya abonelik çekme en az bir etkin alıcı olduğunda bu nedenle toohello DLQ taşınmış unutmayın; Bu davranış tasarım gereğidir.

## <a name="errors-while-processing-subscription-rules"></a>Abonelik kuralları işlenirken hatalar
Ne zaman hello [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) özelliği için bir abonelik etkin olduğunda, bir aboneliğin Web SQL filtre kuralı çalışırken oluşabilecek hatalar hello DLQ yakalanır ileti sorunlu hello yanı sıra.

## <a name="application-level-dead-lettering"></a>Uygulama düzeyi ulaşmayan posta
Toplama toohello sistem tarafından sağlanan ulaşmayan posta özellikleri, uygulamaları hello DLQ tooexplicitly Red kabul edilemez iletileri kullanabilir. Bu, sistem sorunu, hatalı biçimlendirilmiş yüklerini tutun iletileri veya bazı ileti düzeyi güvenlik düzeni kullanıldığında, kimlik doğrulaması başarısız iletileri tooany sıralama düzgün işlenemiyor iletileri içerebilir.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>ForwardTo veya SendVia senaryolarda ulaşmayan posta

İletileri gönderilen toohello aktarımı sahipsiz sıra koşullar aşağıdaki hello altında olacaktır:

- Bir ileti 3'ten fazla sıralar veya olan konuları geçirir [birbirine zincirlenmiş](service-bus-auto-forwarding.md).
- Merhaba hedef sıra ya da konu devre dışı veya silinmiş.
- Merhaba hedef sıra ya da konu hello maksimum varlık boyutu aşıyor.

tooretrieve bu eski lettered iletileri hello kullanarak bir alıcı oluşturabilirsiniz [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) yardımcı yöntemi.

## <a name="example"></a>Örnek
Aşağıdaki kod parçacığını hello ileti alıcı oluşturur. Döngü hello ana sıranın Hello Al, hello kodunu alır hello iletisiyle [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), hangi hello Aracısı tooinstantly dönüş kullanıma hazır herhangi bir iletisi ister ya da hiçbir sonuç ile tooreturn. Merhaba kod bir ileti alırsa, bu hemen, hangi hello artırır kenara bırakır `DeliveryCount`. Merhaba ileti toohello DLQ Hello sistem taşır sonra hello ana sıranın boş ve olarak döngü çıkar hello [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) döndürür **null**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
Makaleler hizmet veri yolu kuyrukları hakkında daha fazla bilgi için aşağıdaki hello bakın:

* [Service Bus kuyrukları ile çalışmaya başlama](service-bus-dotnet-get-started-with-queues.md)
* [Azure kuyruklar ve hizmet veri yolu sıraları karşılaştırılan](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

