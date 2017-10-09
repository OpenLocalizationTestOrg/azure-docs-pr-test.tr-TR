---
title: "Azure Service Bus kuyrukları, konu başlıkları ve abonelikleri Mesajlaşma aaaOverview | Microsoft Docs"
description: "Service Bus Mesajlaşma genel bakış."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Service Bus kuyrukları, konu başlıkları ve abonelikleri

Microsoft Azure Service Bus güvenilir message queuing bulut tabanlı, ileti odaklı Ara teknolojilerini ve dayanıklı yayımlama/Mesajlaşma abonelik, bir kümesini destekler. Bu "aracılı" Mesajlaşma işlevleri, ardından ayrılmış destek yayımlama-abonelik özellikleri Mesajlaşma, zamana bağlı ayırma ve Yük Dengeleme hello Service Bus Mesajlaşma doku kullanarak düşünülebilir. Ayrılmış iletişim birçok avantaj sunar. Örneğin, sunucular ve istemciler gerektiğinde bağlantı kurabilir ve kendi işlemlerini zaman uyumsuz olarak gerçekleştirebilir.

Service Bus içinde Mesajlaşma hello hello özünü oluşturan hello ileti kuyrukları, konuları ve abonelikleri ve kuralları/Eylemler varlıklardır.

## <a name="queues"></a>Kuyruklar

Kuyruklar teklif *ilk gelen, giden ilk* (FIFO yöntemine göre) ileti teslimi tooone veya birden çok rakip tüketiciye. Diğer bir deyişle, iletileri alınan ve hangi toohello sıraya eklendi ve her ileti alındı ve tek bir ileti tüketicisi tarafından alınıp hello düzende hello alıcılar tarafından işlenen genellikle beklenen toobe edilir. Kuyrukları kullanmanın önemli bir avantajı, uygulama bileşenlerinin tooachieve "zamana bağlı ayırma" olur. Diğer bir deyişle, üreticiler (göndericiler) hello ve tüketicilerin (Alıcılar) sahip değil toobe gönderme ve alma aynı hello iletileri iletileri işlemi hello kuyrukta depolandığından, saat. Ayrıca, hello üretici değil toowait hello tüketici yanıt sırası toocontinue tooprocess sahip ve ileti gönderme.

Bir avantaj "üreticileri ve tüketicileri toosend sağlar ve iletileri farklı hızlarda almasına, Dengeleme, yükleme" dir. Birçok uygulamada hello sistem yükü zamana değişir; Bununla birlikte, her iş birimi için gerekli hello işleme süresi genellikle sabittir. Aracılığıyla ileti üreticileri ve tüketicileri bir kuyruk, toobe sağlanan toobe mümkün toohandle ortalama yük yoğun yük yerine yalnızca uygulama bu hello sahip anlamına gelir. Merhaba hello sıra derinliği büyüdükçe ve hello gelen Yük hacmi değiştikçe sözleşme. Bu, doğrudan para şekilde toohello altyapı gerekli tooservice hello uygulama yük miktarı ile kaydeder. Hello yük arttıkça, daha fazla çalışan işlemi hello sırasından eklenen tooread olabilir. Her ileti tek hello çalışan işlemleri tarafından işlenir. Ayrıca, hesaba tooprocessing güç ile Merhaba çalışan bilgisayarlar farklılık gösterse bile iletileri kendi maksimum hızında çeker gibi hello çalışan bilgisayarlar için en iyi kullanımı bu çekme tabanlı yük dengeleme sağlar. Bu desen genellikle hello "tüketici rekabet" düzeni olarak adlandırılır.

İleti üreticileri ve tüketicileri arasında sıraları toointermediate kullanarak hello bileşenler arasındaki yapısında bir gevşek bağlantı sağlar. Üreticileri ve tüketicileri birbirinden farkında değildir çünkü bir tüketici hello üretici üzerinde hiçbir etkisi olmadan yükseltilebilir.

Bir kuyruk oluşturma çok adımlı bir işlemdir. Service Bus Mesajlaşma varlıkları (kuyruklar ve konu başlıkları) hello aracılığıyla yönelik yönetim işlemlerini gerçekleştirmek [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) hello Service Bus temel adresini hello sağlayarak oluşturulan sınıfı ad alanı ve hello kullanıcı kimlik bilgileri. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) yöntemleri toocreate sağlar numaralandırır ve mesajlaşma varlıklarını silme. Oluşturduktan sonra bir [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) nesnesinden hello SAS adını ve anahtar ve bir hizmet ad alanı Yönetim nesnesi, hello kullanabileceğiniz [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) yöntemi toocreate hello sırası. Örneğin:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

Ardından, bağımsız değişken olarak Service Bus URI'si hello ile bir sıra nesnesi ve bir Mesajlaşma fabrikası oluşturabilirsiniz. Örneğin:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

Ardından, iletileri toohello sırası gönderebilirsiniz. Örneğin, adında aracılı iletilerin listesini varsa `MessageList`, hello kodu benzer toohello aşağıdaki görünür:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

Ardından iletileri hello sıradan aşağıdaki gibi alabilirsiniz:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

Merhaba, [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) hello modu, alma tek bir işlemdir; diğer bir deyişle, Service Bus hello isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toohello uygulama döndürür. **ReceiveAndDelete** modu hello en basit modeldir ve hangi hello uygulama tolerans bir hatanın hello Olay iletisinde işlenmiyor senaryolarda en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Service Bus selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, kullanılıyor olarak işaretler çünkü bunu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

İçinde [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) hello modu, alma işlemi, hangi iletilere olası toosupport uygulamaları yapar iki aşamalı haline gelir. Service Bus hello isteği aldığında, tüketilen hello sonraki ileti toobe bulur, tooprevent kilitler, almasını diğer tüketicilerin ve toohello uygulama döndürür. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello alınan ileti üzerinde. Hizmet veri yolu hello gördüğünde **tam** çağrısı hello iletiyi kullanılıyor olarak işaretler.

Merhaba uygulaması kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı hello çağırabilirsiniz [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) hello alınan ileti üzerinde yöntemi (yerine [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Bu hizmet veri yolu toounlock selamlama iletisine sağlar ve yeniden alınan kullanılabilir toobe olun, ya da aynı tüketici hello veya başka bir rakip tüketici tarafından. (Örneğin, hello uygulama çökerse) Service Bus hello iletinin kilidini açar ve kullanılabilir toobe sağlar hello kilit zaman aşımı dolmadan önce İkincisi, var. bir zaman aşımı hello kilidi ile ilişkili olan ve hello uygulama tooprocess başarısız olursa ileti hello yeniden alınan (temelde gerçekleştiren bir [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) işlemi varsayılan olarak).

Hello hello ileti işlenirken sonra ancak hello önce uygulama hello olay çöküyor Not **tam** isteği bildirilmeden, hello ileti yeniden teslim toohello uygulama başlatıldığında. Bu genellikle adlandırılır *en az bir kez* işleme; diğer bir deyişle, her ileti en az bir kez işlenir. Ancak, bazı durumlarda hello aynı ileti yeniden teslim edilebilir. Merhaba senaryo yinelenen işlemeyi tolerans olamaz sonra ek mantık, hello dayalı sağlanabilir hello uygulama toodetect çoğaltmaları gereklidir **MessageID** kalır hello iletinin özelliği sabiti teslim boyunca çalışır. Bu olarak bilinir *tam olarak bir kez* işleme.

## <a name="topics-and-subscriptions"></a>Konular ve abonelikler
Her ileti tek bir tüketici tarafından işlenir Karşıtlık tooqueues içinde *konuları* ve *abonelikleri* iletişim, bir çok form sağladığınız bir *Yayımlama/abonelik* düzeni. Çok sayıda alıcı toovery ölçekleme için yararlı yayımlanan her ileti hello konuya kaydedilen kullanılabilir tooeach abonelik yapılır. İletileri tooa konu ve teslim tooone ya da bir abonelik başına temelinde ayarlanabilir filtre kuralları bağlı olarak daha ilişkili abonelik gönderilir. Merhaba abonelikleri tooreceive istedikleri ek filtreler toorestrict Merhaba iletileri kullanabilirsiniz. İletileri tooa konu gönderilen hello aynı şekilde tooa sıra gönderilmeden ancak iletileri alınmayan hello konusundan doğrudan. Bunun yerine, bunlar aboneliklerden alınır. Bir konu aboneliği toohello konu gönderilen Merhaba iletileri kopyalarını alan sanal kuyruğa benzer. İletileri alınan abonelikten aynı kuyruktan alınan bunlar toohello yolu.

Karşılaştırma, yapmamanız hello bir kuyruk iletisi göndererek işlevselliğini doğrudan tooa konu eşler ve ileti alma işlevselliğini tooa abonelik eşler. Bunun yanı sıra, bu abonelikleri aynı desenler açıklandığı önceki şekilde tooqueues ile bu bölümdeki hello destek anlamına gelir: Rakip tüketici, zamana bağlı ayırma, Yük Dengeleme ve Yük Dengeleme.

Bir konu oluşturma, hello önceki bölümdeki hello örnekte gösterildiği gibi benzer toocreating bir sıraya bağlıdır. Merhaba hizmet URI'si oluşturmak ve ardından hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) sınıfı toocreate hello ad alanı istemci. Ardından hello kullanarak bir konu oluşturun [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) yöntemi. Örneğin:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Ardından, abonelikleri istendiği gibi ekleyin:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

Daha sonra bir konu istemci oluşturabilirsiniz. Örneğin:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Merhaba ileti gönderen kullanarak gönderebilir ve iletileri tooand hello konusundan hello önceki bölümde gösterildiği gibi alabilirsiniz. Örneğin:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Benzer tooqueues, iletileri kullanarak bir abonelik alınan bir [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) yerine Nesne bir [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) nesnesi. Merhaba adı hello konusunun hello abonelik hello adı geçirme hello abonelik istemci oluşturun ve (isteğe bağlı) hello alma modu parametre olarak. Örneğin, hello ile **stok** abonelik:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Kurallar ve eylemler
Birçok senaryoda belirli özelliklere sahip iletileri farklı şekillerde işlenmelidir. tooenable bu özellikler istenilen ve bazı değişiklikler toothose özellikleri gerçekleştirmek abonelikleri toofind iletiler yapılandırabilirsiniz. Hizmet veri yolu abonelikleri toohello konu gönderilen tüm iletiler görürsünüz, ancak yalnızca bir alt kümesini bu iletileri toohello sanal abonelik sırası kopyalayabilirsiniz. Bu, abonelik filtreleri kullanılarak gerçekleştirilir. Tür değişiklikler adlı *filtre eylemlerini*. Bir abonelik oluşturduğunuzda, selamlama iletisine hello özelliklerini çalışır bir filtre ifadesi sağlayabilir, hem de Sistem özellikleri hello (örneğin, **etiket**) ve özel uygulama özelliklerini (örneğin, **StoreName**.) hello SQL filtre ifadesi isteğe bağlı bu durumda; bir SQL filtre ifadesi bir abonelikte tanımlanan herhangi bir filtre eylemi Bu abonelik için tüm hello ileti üzerinde gerçekleştirilir.

Merhaba önceki örnekte, yalnızca'ten gelen toofilter mesajları **Store1**, hello Pano abonelik gibi oluşturursunuz:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Bu abonelik filtresi yerinde hello olan iletiler birlikte `StoreName` çok ayarlanan özelliği`Store1` kopyalanan toohello sanal sıra hello için olan `Dashboard` abonelik.

Hello hello belgelerine olası filtre değerleri hakkında daha fazla bilgi için bkz: [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) ve [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) sınıfları. Ayrıca bkz.: Merhaba [aracılı Mesajlaşma: Gelişmiş filtreler](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) ve [konu filtreleri](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) örnekleri.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba aşağıdaki konularda daha fazla bilgi ve Service Bus Mesajlaşma kullanma örnekleri Gelişmiş bakın.

* [Service Bus mesajlaşma hizmetine genel bakış](service-bus-messaging-overview.md)
* [Service Bus aracılı mesajlaşma .NET eğitmeni](service-bus-brokered-tutorial-dotnet.md)
* [Service Bus aracılı Mesajlaşma REST Öğreticisi](service-bus-brokered-tutorial-rest.md)
* [Konu başlığı filtreleri örneği](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [Aracılı Mesajlaşma: Gelişmiş filtreleri örneği](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

