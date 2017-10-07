---
title: "Hizmet veri yolu aaaAzure eşleştirilmiş ad alanları | Microsoft Docs"
description: "Eşleştirilmiş ad uygulama ayrıntılarını ve maliyet"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Ad alanı uygulama ayrıntılarını eşleştirilmiş ve etkileri maliyet
Merhaba [PairNamespaceAsync] [ PairNamespaceAsync] yöntemini kullanarak bir [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] örneği, görünür görevleri gerçekleştirir sizin adınıza. Var maliyet konuları hello özelliğini kullanırken, böylece bu durum oluştuğunda hello davranışı beklediğiniz bu görevleri yararlı toounderstand demektir. Merhaba API sizin adınıza otomatik davranışı aşağıdaki hello prosese:

* Biriktirme listesi sıraları oluşturma.
* Oluşturulmasını bir [MessageSender] [ MessageSender] tooqueues veya konular ettiği nesnesi.
* Bir Mesajlaşma varlığı kullanılamaz duruma geldiğinde ping iletilerine varlık yeniden kullanılabilir duruma geldiğinde bir girişim toodetect toohello varlık gönderir.
* İsteğe bağlı olarak taşıma iletileri biriktirme listesi sıraları toohello birincil sıraları hello "iletisi Pompalar" kümesi oluşturur.
* Koordinatları kapanış/hatalı hello birincil ve ikincil, [Eventhubclient] [ MessagingFactory] örnekleri.

Yüksek bir düzeyde hello özelliği şu şekilde çalışır: hello birincil varlık iyi durumda hiçbir davranış değişiklikleri oluşur. Ne zaman hello [FailoverInterval] [ FailoverInterval] süresi dolduktan ve hello birincil varlık, bir geçici olmayan sonra hiçbir başarılı gönderir görür [MessagingException] [ MessagingException] veya [TimeoutException][TimeoutException], aşağıdaki davranış hello oluşur:

1. İşlemleri toohello varlık devre dışı bırakılır ve ping başarıyla teslim edilebilir kadar birincil varlık hello sistem ping hello birincil gönderin.
2. Rastgele biriktirme listesi sırası seçilir.
3. [BrokeredMessage] [ BrokeredMessage] biriktirme listesi sırası seçilen yönlendirilmiş toohello nesneleridir.
4. Biriktirme listesi sırası seçilen gönderme işlemi toohello başarısız olursa, o sıra hello döndürme çekilir ve yeni bir sıra seçilir. Merhaba üzerindeki tüm gönderenlerin [Eventhubclient] [ MessagingFactory] örneği hello başarısızlığını öğrenin.

şekiller aşağıdaki hello hello dizisini tarif. İlk olarak, hello gönderen iletileri gönderir.

![Eşleştirilmiş ad alanları][0]

Hata toosend toohello birincil kuyruk sonra rasgele biriktirme listesi sırası seçilen iletileri tooa gönderme hello gönderen başlar. Aynı anda bir ping görev başlatır.

![Eşleştirilmiş ad alanları][1]

Bu noktada hello iletiler hala hello ikincil sıraya ve toohello birincil kuyruk teslim edilmedi. Merhaba birincil kuyruk yeniden sağlıklı olduğunda en az bir işlem hello Sifon çalıştırıyor olması gerekir. Merhaba Sifon Merhaba iletileri sıraları toohello uygun hedef varlıkları (kuyruklar ve konu başlıkları) tüm hello çeşitli biriktirme listesi sunar.

![Eşleştirilmiş ad alanları][2]

Bu konunun geri kalanı Hello parçaların nasıl işe hello belirli Ayrıntılar açıklanmaktadır.

## <a name="creation-of-backlog-queues"></a>Biriktirme listesi sıraların oluşturma
Merhaba [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] toohello geçirilen nesnesi [PairNamespaceAsync] [ PairNamespaceAsync] yöntemi hello gösterir biriktirme listesi sayısı kuyruklar toouse istiyor. Her bir biriktirme listesi sırası sonra hello ile oluşturulan aşağıdaki özelliklere açıkça ayarlayın (diğer tüm değerler toohello ayarlanır [QueueDescription] [ QueueDescription] Varsayılanları):

| Yol | [birincil ad alanı] / x servicebus aktarımı / [[dizin] [0, BacklogQueueCount) değerinde olduğu dizin] |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| maxDeliveryCount |int MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1 dakika |
| EnableDeadLetteringOnMessageExpiration |TRUE |
| EnableBatchedOperations |TRUE |

Örneğin, hello ilk biriktirme listesi sırası oluşturulan ad alanı için **contoso** adlı `contoso/x-servicebus-transfer/0`.

Böyle bir sıraya varsa hello sıraları oluştururken hello kodunu ilk toosee denetler. Merhaba sırası yoksa hello sırası oluşturulur. Merhaba kod desteklemez "ek" biriktirme listesi sıraları temizlenemedi. Özellikle, Merhaba, uygulama ile Merhaba birincil ad alanı **contoso** beş biriktirme listesi sırası ancak bir biriktirme listesi sırası hello yolu ile istekleri `contoso/x-servicebus-transfer/7` var, bu ek biriktirme listesi kuyruğa hala var, ancak kullanılmaz. Merhaba sistem değil kullanılacak ek biriktirme listesi sıraları tooexist açıkça izin verir. Merhaba ad alanı sahibi olarak, tüm kullanılmayan/istenmeyen biriktirme listesi sıralarını temizleme işlemi için sorumluluğu size aittir. Merhaba Bu karar hizmet veri yolu ad alanınız içinde hello sıraların tümü için hangi amacıyla mevcut bilemezsiniz nedeni. Ayrıca, bir sıra hello verilen ada sahip var, ancak kabul hello karşılamıyor [QueueDescription][QueueDescription], için kendi değişen hello varsayılan davranışı, nedenleri sonra. Garanti değişiklikler toohello biriktirme listesi kuyruklarında kodunuz tarafından yapılır. Emin tootest baştan sona istediğiniz değişiklikleri yapın.

## <a name="custom-messagesender"></a>Özel MessageSender
Tüm iletileri gönderirken, bir iç Git [MessageSender] [ MessageSender] zaman her şeyi çalışır ve şey "böldüğünüzde." toohello biriktirme listesi sıraları yönlendiren normal şekilde davranır nesnesi Bir geçici olmayan hata alındıktan sonra bir süreölçer başlatır. Sonra bir [TimeSpan] [ TimeSpan] hello oluşan süresi [FailoverInterval] [ FailoverInterval] sırasında başarılı bir ileti gönderilir özellik değeri , hello yük devretme gerçekleştiriliyor. Bu noktada, hello aşağıdaki her bir varlık için olacaklar:

* Bir ping görevi yürütür her [PingPrimaryInterval] [ PingPrimaryInterval] hello varlık varsa toocheck. Bu görev başarılı olduktan sonra yeni iletiler toohello birincil ad alanı göndermeye hello varlığı hemen kullanan tüm istemci kodu başlar.
* Başka Gönderenler aynı varlıktan hello sonuçlanacak gelecekteki isteklerin toosend toothat [BrokeredMessage] [ BrokeredMessage] toobe gönderilen hello biriktirme listesi sırasındaki toosit değiştirdi. Merhaba değişikliği hello bazı özellikler kaldırır [BrokeredMessage] [ BrokeredMessage] nesne ve başka bir yerde depolar. Merhaba aşağıdaki özellikleri temizlenir ve Service Bus ve hello SDK tooprocess iletileri hep sağlayan yeni bir ad altında eklendi:

| Eski özellik adı | Yeni özellik adı |
| --- | --- |
| SessionID |x-ms-SessionID |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-yol |

Merhaba özgün hedef yolu x-ms-path adlı bir özellik olarak da selamlama iletisine içinde depolanır. Bu tasarım, birçok varlıklar toocoexist iletilerde tek biriktirme listesi sıraya sağlar. Merhaba özellikleri geri hello Sifon tarafından çevrilir.

Merhaba özel [MessageSender] [ MessageSender] nesne sorunlarla iletileri hello 256 KB sınıra yaklaşmak ve yük devretme gerçekleştiriliyor. Merhaba özel [MessageSender] [ MessageSender] nesnesi tüm kuyrukları ve konularından hello biriktirme listesi kuyruklarda birlikte iletileri saklar. Bu nesne pek çok ana hello biriktirme listesi sıraları içinde birlikte gelen iletileri karıştırır. toohandle Yük Dengeleme her diğer hello SDK rastgele bilmiyorsanız birçok istemciler arasında her biri için bir biriktirme listesi sırası Çekmeleri [QueueClient] [ QueueClient] veya [TopicClient] [ TopicClient] kodda oluşturabilir.

## <a name="pings"></a>Ping isteği
Boş bir ping iletisidir [BrokeredMessage] [ BrokeredMessage] ile kendi [ContentType] [ ContentType] özelliği tooapplication/vnd.ms-servicebus-ping ayarlayın ve [TimeToLive] [ TimeToLive] 1 saniye değeri. Bu ping Service Bus içinde bir özellik vardır: hello sunucusunun herhangi bir çağırıcı istediğinde, bir ping hiçbir zaman sunduğundan bir [BrokeredMessage][BrokeredMessage]. Bu nedenle, hiçbir zaman toolearn nasıl elinizde tooreceive ve bu iletileri yok sayın. Her varlığın (benzersiz kuyruk veya konu) başına [Eventhubclient] [ MessagingFactory] istemci başına örnek ping işlemi olduğunda bunlar toobe kullanılamaz olarak kabul edilir. Varsayılan olarak, bu kez dakika başına gerçekleşir. Ping iletilerine toobe normal Service Bus iletileri kabul edilir ve bant genişliği ve iletileri ilişkin ücretlere neden olabilir. Merhaba istemciler hello sistemin kullanılabilir olduğunu tespit hemen Merhaba iletileri durdurun.

## <a name="hello-syphon"></a>Merhaba Sifon
En az bir yürütülebilir program hello uygulamada etkin şekilde hello Sifon çalıştırıyor olması gerekir. Merhaba Sifon gerçekleştiren bir uzun yoklama alırsınız, 15 dakika sürer. Tüm varlıklar kullanılabilir olduğunda ve 10 biriktirme listesi sıraların sahip olduğunda hello alma işlemi 40 kez saatte, günde 960 kez ve 28800 kez 30 gün içinde hello Sifon çağrıları barındıran uygulama hello. Merhaba Sifon etkin bir şekilde hello biriktirme listesi toohello birincil kuyruktan iletileri taşımaktır, her ileti giderleri (tüm aşamalarda ileti boyutu ve bant genişliği için standart ücretler geçerlidir) aşağıdaki hello görür:

1. Toohello biriktirme listesi gönderir.
2. Hello biriktirme listesi alır.
3. Toohello birincil gönderin.
4. Merhaba birincil alırsınız.

## <a name="closefault-behavior"></a>Davranış Kapat/hata
Merhaba Sifon, bir kez hello birincil veya ikincil barındıran uygulama içinde [Eventhubclient] [ MessagingFactory] hataları veya kapalı hello ve ayrıca hatalı/kapatılan iş ortağı Sifon bu durum algılar. , hello Sifon davranır. Varsa diğer hello [Eventhubclient] [ MessagingFactory] kapalı 5 saniye içinde hello hala açık hello Sifon hata [Eventhubclient] [ MessagingFactory] .

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [zaman uyumsuz desenleri ve yüksek kullanılabilirlik Mesajlaşma] [ Asynchronous messaging patterns and high availability] Service Bus zaman uyumsuz Mesajlaşma hakkında ayrıntılı bilgi için. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
