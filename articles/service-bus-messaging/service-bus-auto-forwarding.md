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
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Hizmet veri yolu varlıklarını otomatik iletme ile zincirleme

Merhaba Service Bus *otomatik iletme* özelliği sağlar, size, toochain bir sıraya veya abonelik tooanother sıra ya da hello parçası olan konu aynı ad. Otomatik iletme etkinleştirildiğinde, Service Bus otomatik olarak hello ilk sırayı veya abonelik (kaynak) yerleştirilen iletileri kaldırır ve hello ikinci kuyruk veya konu (hedef) koyar. Bunu hala olası toosend bir ileti toohello hedef varlık doğrudan olduğuna dikkat edin. Ayrıca, olası toochain sahipsiz sıraya, tooanother kuyruk veya konu gibi bir alt sırasına değil.

## <a name="using-auto-forwarding"></a>Otomatik iletme kullanma
Otomatik iletme ayarı hello tarafından etkinleştirebilirsiniz [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] veya [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] Merhaba özellikleri [QueueDescription] [ QueueDescription] veya [SubscriptionDescription] [ SubscriptionDescription] hello olduğu gibi hello kaynağı için nesneler Aşağıdaki örnek.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

Merhaba hedef varlık hello kaynak varlık oluşturulan hello aynı anda mevcut olması gerekir. Merhaba hedef varlık mevcut değilse sorulan toocreate hello kaynak varlık Service Bus bir özel durum döndürür.

Tek bir konu çıkışı otomatik iletme tooscale kullanabilirsiniz. Hizmet veri yolu sınırları hello [belirli bir konu Aboneliklerde sayısı](service-bus-quotas.md) too2, 000. İkinci düzey konuları oluşturarak ek abonelikleri barındırabilir. Merhaba tarafından bağlı olmayan olsa bile Service Bus abonelik, ikinci düzey konuları ekleme hello sayısını sınırlama artırabilir, konunun genel üretilen işi hello unutmayın.

![Otomatik iletme senaryosu][0]

Otomatik iletme toodecouple ileti alıcıları göndericilerden de kullanabilirsiniz. Örneğin, üç modülden oluşur bir ERP sistemi göz önünde bulundurun: sipariş işleme, Envanter yönetimine ve müşteri ilişkileri yönetimi. Bu modüllerin her biri, karşılık gelen bir konu içine sıraya alınan iletileri oluşturur. Alice ve Bob tootheir müşteriler ile ilgili tüm iletileri ilginizi çekiyor mu satış temsilcisi markalarıdır. Bu iletileri tooreceive Alice ve Bob kişisel bir sıra ve bir abonelik her tüm iletileri tootheir sırası otomatik olarak ilet hello ERP konuları oluşturun.

![Otomatik iletme senaryosu][1]

Alice tatil, kendi kişisel kuyruk, yerine hello ERP konu kalırsa, dolar. Bir satış temsilcisi herhangi bir iletisi aldı değil çünkü bu senaryoda, hello ERP konuları hiçbiri hiç kota ulaşabilirsiniz.

## <a name="auto-forwarding-considerations"></a>Otomatik iletme konuları

Merhaba hedef varlık çok fazla ileti toplanır ve hello kotasını aşıyor veya hello hedef varlık devre dışıysa, hello kaynak varlık hello iletileri tooits ekler [sahipsiz sırayı](service-bus-dead-letter-queues.md) hello hedef alan kadar (veya hello varlık yeniden etkinleştirildi). Açıkça almak ve bunları hello sahipsiz sıradan işlemek için bu iletileri hello sahipsiz sırasındaki toolive devam eder.

Ayrı ayrı konularını tooobtain birçok abonelikleri bileşik konuyla birlikte zincirleme kullanırken Orta sayıda hello birinci düzey konu Aboneliklerde ve hello ikinci düzey konuları birçok Aboneliklerde sahip önerilir. Örneğin, birinci düzey konu 20 abonelikler ile bunların zincirleme her birini tooa ikinci düzey konu 200 abonelikler ile 200 Abonelikleri, birinci düzey konuyla daha yüksek verimlilik sağlar her zincirleme tooa ikinci düzey konu 20 abonelikler ile .

Hizmet veri yolu iletilen her ileti için bir işlem ödemenizi işler. Örneğin, bir ileti tooa konu 20 abonelikler ile gönderme, bunların her birini tooanother kuyruk veya konu faturalandırılır 21 işlemleri olarak birinci düzey abonelikler hello iletinin bir kopyasını alırsanız tooauto iletme iletileri yapılandırılmış.

toocreate zincirleme tooanother kuyruk veya konu aboneliği, hello abonelik hello oluşturan olmalıdır **Yönet** hello kaynak ve hedef varlık hello izinleri. İletileri toohello kaynak konu yalnızca gerektirir gönderme **Gönder** hello kaynak konu izinleri.

## <a name="next-steps"></a>Sonraki adımlar

Otomatik iletme hakkında ayrıntılı bilgi için aşağıdaki başvuru konularda hello bakın:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

Hizmet veri yolu performans iyileştirmeleri hakkında daha fazla toolearn bakın 

* [Service Bus Mesajlaşma hizmeti kullanarak performans iyileştirmeleri için en iyi yöntemler](service-bus-performance-improvements.md)
* [Bölümlenmiş Mesajlaşma varlıkları][Partitioned messaging entities].

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
