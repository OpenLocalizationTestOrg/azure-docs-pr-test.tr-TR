---
title: "Azure Service Bus kuyrukları ve konularından aaaCreate bölümlenmiş | Microsoft Docs"
description: "Nasıl toopartition Service Bus kuyrukları ve konularından birden çok iletisini kullanarak aracıların açıklar."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Bölümlenmiş kuyruklar ve konular
Birden çok ileti aracıların tooprocess iletiler Azure hizmet veri yolu kullanır ve birden çok Mesajlaşma toostore iletileri depolar. Geleneksel kuyruk veya konu tek ileti aracısı tarafından işlenen ve bir Mesajlaşma deposunda depolanır. Hizmet veri yolu *bölümleri* kuyruklar ve konu başlıkları, etkinleştirmek veya *Mesajlaşma*, birden çok ileti aracıları ve mesajlaşma depoları arasında bölümlenmiş toobe. Bölümlenmiş bir varlığın genel üretilen işi hello Bunun anlamı artık tek ileti Aracısı ya da ileti deposu hello performans ile sınırlıdır. Ayrıca, bir Mesajlaşma deposu geçici bir kesinti bölümlenmiş kuyruk veya konu kullanılamaz işlemez. Bölümlenmiş kuyrukları ve konularından işlemleri ve oturumlar için destek gibi tüm Gelişmiş Service Bus özellikler içerebilir.

Hizmet veri yolu dahili bileşenleri hakkında daha fazla bilgi için bkz: hello [Service Bus mimarisi] [ Service Bus architecture] makalesi.

Bölümleme varlık oluşturulurken tüm kuyruklar ve konular standart ve Premium, varsayılan olarak etkinleştirilmiştir Mesajlaşma. Standart katmanı bölümleme olmadan Mesajlaşma oluşturabilirsiniz, ancak kuyruklar ve konular Premium ad alanı, her zaman bölümlenmiş; Bu seçenek devre dışı bırakılamaz. 

Olası toochange hello olmadığı hello varlık oluşturduğunuzda seçeneği olan bir sırayı veya standart veya Premium katmanları konudaki bölümlendirme, yalnızca hello seçeneği ayarlayabilirsiniz.

## <a name="how-it-works"></a>Nasıl çalışır?

Her bölümlenmiş kuyruk veya konu birden çok parçalarını oluşur. Her parça farklı bir Mesajlaşma deposunda depolanır ve farklı ileti aracısı tarafından işlenir. Bir ileti tooa bölümlenmiş kuyruk veya konu gönderildiğinde, Service Bus hello ileti tooone hello parçaların atar. Merhaba seçimi rastgele Service Bus tarafından yapılır veya gönderen hello bir bölüm anahtarı kullanarak belirtebilirsiniz.

Bir istemci tooreceive bölümlenmiş bir kuyruktan bir ileti istediği ya da bir abonelik tooa bölümlenmiş konusundan, hizmet veri yolu ileti tüm parçaları sorgular depoları toohello alıcı Mesajlaşma hello hiçbirini elde hello ilk ileti döndürür. Hizmet veri yolu önbellekleri diğer iletiler ve bunları ek aldığında isteklerini alacak döndürür hello. Bir alıcı istemci hello bölümlendirme farkında değildir; Merhaba istemciye yönelik davranışını bölümlenmiş kuyruk veya konu (örneğin, okuma, tamamlamak, sahipsiz, erteleneceği prefetching) normal bir varlık aynı toohello davranıştır.

İleti gönderirken ya da bölümlenmiş kuyruk veya konu, bir mesaj alarak ek bir maliyeti yoktur.

## <a name="enable-partitioning"></a>Bölümleme etkinleştir

bölümlenmiş toouse kuyrukları ve konularından Azure Service Bus ile hello Azure SDK'sını 2.2 veya sonraki bir sürümü kullanın veya belirtin `api-version=2013-10` , HTTP istekleri.

### <a name="standard"></a>Standart

Merhaba standart Mesajlaşma katmanında, Service Bus kuyrukları ve konuları (Merhaba varsayılan 1 GB'dır) 1, 2, 3, 4 veya 5 GB boyutlarda oluşturabilirsiniz. Etkin bölümlendirme ile hizmet veri yolu için belirttiğiniz her GB hello varlık 16 kopyalarını (16 bölümler) oluşturur. Bu nedenle, 5 GB boyutunda bir sırasına oluşturursanız, hello en büyük sıra boyutu olan 16 bölümleri olur (5 \* 16) = 80 GB. Merhaba üzerinde kendi girdisi bakarak bölümlenmiş kuyruk veya konu en büyük boyutunu hello görebilirsiniz [Azure portal][Azure portal], hello içinde **genel bakış** dikey penceresinde bu varlık için.

### <a name="premium"></a>Premium

Premium katmanı ad alanında Service Bus kuyrukları ve konuları (Merhaba varsayılan 1 GB'dır) 1, 2, 3, 4, 5, 10, 20, 40 veya 80 GB boyutlarda oluşturabilirsiniz. Varsayılan olarak etkin bölümlendirme ile Service Bus varlık başına iki bölüm oluşturur. Merhaba üzerinde kendi girdisi bakarak bölümlenmiş kuyruk veya konu en büyük boyutunu hello görebilirsiniz [Azure portal][Azure portal], hello içinde **genel bakış** dikey penceresinde bu varlık için.

Merhaba Premium Mesajlaşma katmanında bölümleme hakkında daha fazla bilgi için bkz: [Service Bus Premium ve standart Mesajlaşma katmanları](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Bölümlenmiş bir varlık oluştur

Çeşitli yolları toocreate bölümlenmiş bir kuyruk veya konu vardır. Uygulamanızdan hello kuyruk veya konu oluşturduğunuzda, hello kuyruk veya konu başlığı için sırasıyla ayarı hello tarafından bölümleme etkinleştirebilirsiniz [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] veya [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] özelliği çok**doğru**. Bu özellikleri hello zaman hello sıraya ayarlanmalı veya konu oluşturulur. Daha önce belirtildiği gibi bu özellikleri mümkün değil toochange olduğu bir varolan kuyruk veya konu başlığı. Örneğin:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Alternatif olarak, bölümlenmiş kuyruk veya konu hello oluşturabilirsiniz [Azure portal] [ Azure portal] veya Visual Studio'da. Merhaba Portalı'nda bir kuyruk veya konu oluşturduğunuzda, hello **bölümleme etkinleştirmek** hello kuyruk veya konu seçeneğinde **oluşturma** dikey varsayılan olarak işaretli. Yalnızca standart katmanı varlıktaki bu seçenek devre dışı bırakabilirsiniz; Hello Premium katmanı bölümleme her zaman etkindir. Visual Studio'da hello tıklatın **etkinleştirmek bölümleme** hello onay kutusu **yeni kuyruk** veya **yeni konu** iletişim kutusu.

## <a name="use-of-partition-keys"></a>Bölüm anahtarlarını kullanımı
İleti sıraya alınan bölümlenmiş kuyruk veya konu içine olduğunda, hizmet veri yolu bir bölüm anahtarı hello varlığını denetler. Bulursa, bu anahtarı temel hello parça seçer. Bölüm anahtarı bulamazsa, bir iç algoritmadan yola çıkılarak hello parça seçer.

### <a name="using-a-partition-key"></a>Bir bölüm anahtarının kullanılması
Oturumları veya işlemleri gibi bazı senaryolar belirli parçadaki depolanan iletileri toobe gerektirir. Bu senaryolar bölüm anahtarı hello kullanılmasını gerektirir. Tüm iletileri aynı bölüm anahtarı atanır, kullanım hello toohello aynı parçalara. Merhaba parça geçici olarak devre dışı ise, hizmet veri yolu bir hata döndürür.

Merhaba senaryo bağlı olarak farklı ileti özellikleri bir bölüm anahtarı olarak kullanılır:

**SessionID**: bir ileti hello sahipse [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] özelliğini ayarlayın, sonra Service Bus, bu özellik hello bölüm anahtarı olarak kullanır. Bu şekilde, toohello ait tüm iletileri aynı oturum hello tarafından işlenmiş aynı ileti Aracısı. Bu hizmet veri yolu tooguarantee ileti oturum durumları hello tutarlılık yanı sıra sıralama sağlar.

**PartitionKey**: bir ileti hello sahipse [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] özelliği, ancak değil hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] özelliğini ayarlayın, sonra Service Bus kullanan hello [PartitionKey] [ PartitionKey] özelliği hello bölüm anahtarı olarak. Merhaba ileti iki hello sahipse [SessionID] [ SessionId] ve hello [PartitionKey] [ PartitionKey] özellikler kümesi, her iki özellik aynı olmalıdır. Merhaba, [PartitionKey] [ PartitionKey] özelliği tooa farklı hello değerinden ayarlanmış [SessionID] [ SessionId] özelliği, hizmet veri yolu geçersiz bir döndürür işlem özel durum. Merhaba [PartitionKey] [ PartitionKey] özelliği, oturum olmayan farkında işlem iletileri gönderen gönderirse, kullanılmalıdır. Merhaba bölüm anahtarı bir işlem içinde gönderilen tüm iletiler hello tarafından aynı işlenmesini sağlar Mesajlaşma Aracısı.

**MessageID**: hello hello kuyruk veya konu varsa [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] çok ayarlanan özelliği**doğru** ve hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] veya [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] özellikleri ayarlanmaz, ardından hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] özelliği hello bölüm anahtarı olarak hizmet verir. (Merhaba gönderen uygulama yoksa hello Microsoft .NET ve AMQP kitaplıkları otomatik olarak bir ileti kimliği atamak unutmayın.) Bu durumda, aynı iletiyi tarafından işlenmesini hello tüm kopyalarını aynı ileti Aracısı hello. Bu hizmet veri yolu toodetect sağlar ve yinelenen iletileri ortadan kaldırmak. Merhaba, [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] özelliği çok ayarlanmamışsa**true**, Service Bus hello dikkate almaz [MessageID] [ MessageId] bölüm anahtarı olarak özelliği.

### <a name="not-using-a-partition-key"></a>Bir bölüm anahtarının kullanılması değil
Bölüm anahtarı Hello olmaması durumunda, hizmet veri yolu ileti hepsini şekilde tooall hello parçada hello bölümlenmiş kuyruk veya konu dağıtır. Seçilen hello parça kullanılabilir durumda değilse, hizmet veri yolu hello ileti tooa farklı parça atar. Bu şekilde hello geçici olarak kullanım dışı kalması bir Mesajlaşma deposu rağmen hello gönderme işlemi başarılı olur. Ancak, bir bölüm anahtarı sağladığını sıralama garanti hello elde.

Merhaba kolaylığını kullanılabilirlik (bölüm anahtarı) ve tutarlılık (bölüm anahtarı kullanarak) arasında daha ayrıntılı bir tartışma için bkz: [bu makalede](../event-hubs/event-hubs-availability-and-consistency.md). Bu bilgiler, toopartitioned hizmet veri yolu varlıklarını ve Event Hubs bölümleri eşit oranda geçerlidir.

toogive Service Bus yeterli zamanı tooenqueue hello iletisi farklı bir parça hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] hello iletisi gönderir hello istemci tarafından belirtilen değeri 15 saniyeden büyük olmalıdır. Merhaba ayarlamanız önerilir [OperationTimeout] [ OperationTimeout] özelliği toohello varsayılan değer 60 saniye.

Bölüm anahtarı "iletisi tooa belirli parça sabitler," unutmayın. Bu parça tutan hello Mesajlaşma deposu kullanılamıyorsa, hizmet veri yolu bir hata döndürür. Bölüm anahtarı hello olmadığında, Service Bus farklı bir parça seçebilir ve hello işlemi başarılı olur. Bu nedenle, gerekli olmadığı sürece bir bölüm anahtarı sağlamazsanız önerilir.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Gelişmiş konular: bölümlenmiş varlıklarıyla işlemleri kullanın
Bir işlemin bir parçası gönderilen iletileri bir bölüm anahtarı belirtmeniz gerekir. Bu özellikler aşağıdaki hello biri olabilir: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], veya [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Aynı işlem belirtmelisiniz hello bir parçası olarak gönderilen tüm iletiler hello aynı bölüm anahtarı. Bir işlem içinde bölüm anahtarı olmayan bir ileti toosend çalışırsanız, hizmet veri yolu geçersiz işlemi özel durum döndürür. Farklı aynı işlem içinde birden fazla ileti hello toosend çalışırsanız bölüm anahtarlarını, hizmet veri yolu geçersiz işlemi özel durum döndürür. Örneğin:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Herhangi bir bölüm anahtarı olarak hizmet hello özelliklerinin ayarlanırsa, Service Bus PIN'ler ileti tooa belirli parça hello. Bu davranış, bir işlem kullanılan olup olmadığına bakılmaksızın oluşur. Gerekli değilse bölüm anahtarı belirtmeyin önerilir.

## <a name="using-sessions-with-partitioned-entities"></a>Bölümlenmiş varlıklarıyla oturumları kullanma
toosend bir işlem iletisi tooa oturum algılayan konu veya sıra, selamlama iletisine sahip olması gerekir hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] özellik kümesi. Merhaba, [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] özelliği de belirtilen, aynı toohello olmalıdır [SessionID] [ SessionId] özelliği. Bunlar farklıysa, hizmet veri yolu geçersiz işlemi özel durum döndürür.

Normal (bölümlenmemiş) sıraları veya konuları aksine, olası toouse tek işlem toosend birden çok iletileri toodifferent oturumu değil. Bulamazsa, hizmet veri yolu geçersiz işlemi özel durum döndürür. Örneğin:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Bölümlenmiş varlıklarla otomatik ileti iletme
Service Bus otomatik ileti gelen ya da bölümlenen varlıklar arasında iletme destekler. tooenable otomatik ileti iletme'yi ayarlayın hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] hello kaynak sırası veya Abonelik özelliği. Selamlama iletisine bölüm anahtarı belirtiyorsa ([SessionID][SessionId], [PartitionKey][PartitionKey], veya [MessageID] [ MessageId]), bu bölüm anahtarı hello hedef varlık için kullanılır.

## <a name="considerations-and-guidelines"></a>Dikkat edilecek noktalar ve yönergeleri
* **Yüksek tutarlılık özellikleri**: bir varlığı oturumları, yinelenen algılama veya bölümlendirme anahtarı açık denetim gibi özellikler kullanan sonra hello Mesajlaşma işlemleri her zaman yönlendirilmiş toospecific parça. Merhaba parçaları hiçbirini yüksek trafik deneyimi veya hello alttaki deponun sağlam değil, bu işlemler başarısız ve kullanılabilirlik azalır. Genel olarak, hello tutarlılık bölümlenmemiş varlıklar hala çok daha yüksektir; yalnızca bir alt trafik karşılıklı tooall hello trafiği olarak sorunları yaşıyor. Daha fazla bilgi için bkz [kullanılabilirlik ve tutarlılık tartışma](../event-hubs/event-hubs-availability-and-consistency.md).
* **Yönetim**: oluşturma, güncelleştirme ve silme gibi işlemleri tüm hello parçaları hello varlık gerçekleştirilmesi gerekir. Herhangi bir parça sağlıksız ise, bu işlemler için hataları neden olabilir. İleti sayısı gibi hello alma işlemi için bilgi tüm parçaları toplanması gerekir. Herhangi bir parça sağlıksız ise, hello varlık kullanılabilirlik durumunu sınırlı raporlanır.
* **Düşük birim ileti senaryosu**: Bu senaryolara, özellikle hello HTTP protokolü kullanılırken tooperform olabilir birden çok alma işlemlerinin sipariş tooobtain tüm Merhaba iletileri. Alma istekleri hello ön uç üzerinde tüm hello parçaları alma gerçekleştirir ve alınan tüm hello yanıtlarını önbelleğe kaydeder. Bir sonraki alma isteği aynı bağlantı ve bu önbelleğe alma işleminden faydalanır gecikmeleri alma hello daha düşük olacaktır. Ancak, birden çok bağlantınız veya HTTP kullanıyorsanız, her istek için yeni bir bağlantı kurar. Bu nedenle, üzerinde hello güden garanti yoktur aynı düğüm. Tüm mevcut iletileri kilitlenir ve içinde başka bir ön uç, önbelleğe alınmış hello işlemi döndürür alıyorsunuz **null**. İletileri sonunda süresi dolacak ve yeniden alırsınız. HTTP Etkin tutmayı önerilir.
* **Gözat/gözlem iletileri**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) her zaman hello belirtilen iletilerinin hello sayısı döndürmüyor [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) özelliği. Bu iki ortak nedenleri vardır. Bir nedeni bu hello iletileri hello koleksiyonunu toplanmış boyutunu aşıyor hello en büyük boyutu 256KB. Merhaba Hello kuyruk veya konu varsa olan başka bir nedenle [EnablePartitioning özelliğinin](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) çok ayarlamak**doğru**, bir bölüm yeterli iletileri olmayabilir toocomplete hello istenen iletilerinin sayısı. Bir uygulama tooreceive iletileri belirli sayıda isterse, genel olarak, çağırmalıdır [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) kadar art arda bu iletilerin sayısını alır veya daha fazla hiçbir iletileri toopeek vardır. Kod örnekleri dahil olmak üzere daha fazla bilgi için bkz: [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) veya [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>En son eklenen özellikler
* Ekleme veya kaldırma kural bölümlenmiş varlıklarıyla artık desteklenmektedir. Bölümlenmiş olmayan varlıklar farklıdır, bu işlemler altında işlemleri desteklenmez. 
* AMQP iletileri tooand bölümlenmiş bir varlıktan gönderip için artık desteklenmektedir.
* AMQP işlemleri aşağıdaki hello için artık desteklenmektedir: [toplu iş gönderme](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [toplu alma](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [alma sıra numarası tarafından](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [Peek](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Kilit yenileme](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [zamanlama ileti](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [zamanlanmış iletiyi iptal](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [Kuralı Ekle](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [kaldırmak kural](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Oturumunuzu yenilemek kilit](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [kümesi oturum durumu](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [Get oturum durumu](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), ve [oturumları listeleme](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Bölümlenen varlıklar sınırlamaları
Şu anda hizmet veri yolu bölümlenmiş kuyrukları ve konularından sınırlamalar aşağıdaki hello getirir:

* Bölümlenmiş kuyruklar ve konu başlıkları toodifferent ait iletileri gönderme desteklemez tek bir işlemde oturumları.
* Hizmet veri yolu şu anda bölümlenmiş too100 sıraları veya ad alanı başına konuları sağlar. Her bölümlenmiş kuyruk veya konu hello kota (tooPremium katmanı geçerli değildir) ad alanı başına 10.000 varlıkların doğru sayar.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba tartışması bkz [hizmet veri yolu AMQP 1.0 desteği bölümlenmiş kuyruklar ve konu başlıkları] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn Mesajlaşma varlıkları bölümleme hakkında daha fazla bilgi. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
