---
title: "Azure Service Bus konuları ve abonelikleri kullanan aaaCreate uygulamaları | Microsoft Docs"
description: "Giriş toohello yayımlama-abone olma Service Bus konuları ve abonelikleri tarafından sunulan yetenekleri."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Service Bus konuları ve abonelikleri kullanan uygulamalar oluşturma
Azure Service Bus güvenilir message queuing bulut tabanlı, ileti odaklı Ara teknolojilerini ve dayanıklı yayımlama/Mesajlaşma abonelik, bir kümesini destekler. Bu makalede sağlanan hello bilgileri inşa edilmiştir [Service Bus kuyruklarını kullanan uygulamalar oluşturmak](service-bus-create-queues.md) ve giriş Service Bus konu başlıklarını tarafından sunulan toohello yayımlama/abonelik yetenekleri sunar.

## <a name="evolving-retail-scenario"></a>Gelişen perakende senaryosu
Bu makalede kullanılan hello perakende senaryo devam [Service Bus kuyruklarını kullanan uygulamalar oluşturmak](service-bus-create-queues.md). Tek tek satış noktası (POS) Terminal satış verileri yenilenir toobe hisse sahip olduğunda, bu veri toodetermine kullanan yönlendirilmiş tooan Stok yönetim sisteminin olmalıdır geri çağırma. İletileri toohello göndererek satış verilerini her POS terminal raporları **DataCollectionQueue** sırası, burada kalırlar hello Stok yönetim sistemi tarafından alınana kadar aşağıda gösterildiği gibi:

![Hizmet veri yolu 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

Bu senaryo, yeni gereksinimi süredir tooevolve eklenen toohello sistem: hello mağaza sahibi hello deposu gerçek zamanlı olarak gerçekleştirip nasıl toobe mümkün toomonitor istemektedir.

tooaddress bu gereksinim hello sistem "Merhaba satış veri akışı dokunun gerekir". Itanium tabanlı sistemler için toohello Stok yönetim sisteminin olarak önce gönderilen hello POS Terminal toobe tarafından gönderilen her ileti hala istiyoruz, ancak her iletinin toopresent hello Pano görünümü toohello mağaza sahibi kullanabileceğiniz başka bir kopyasını istiyoruz.

Bu, birden çok taraflar tarafından tüketilen her ileti toobe gerektiren gibi herhangi bir durumda, hizmet veri yolu kullanabilirsiniz *konuları*. Konular, yayımlanmış her ileti kullanılabilir tooone yapılan veya daha fazla abonelik hello konu başlığına kayıtlı olan bir publish/subscribe modelini sağlar. Buna karşılık, Kuyruklarla her ileti tek bir tüketici tarafından alınır.

İletileri tooa konu hello gönderilen aynı şekilde tooa sıra gönderilir. Ancak, iletileri hello konusundan doğrudan alınmaz; Bunlar aboneliklerden alınır. Abonelik tooa konu toothat konu gönderilen Merhaba iletileri kopyalarını alan sanal kuyruğa düşünebilirsiniz. İletileri abonelikten alınan bir kuyruktan şekilde alınmış olarak aynı hello.

Toohello perakende senaryo geri dönerseniz, hello sıraya göre bir konu değiştirilir ve hangi hello Stok yönetim sisteminin bileşeni kullanabileceğiniz bir abonelik eklenir. Merhaba sistem şimdi aşağıdaki gibi görünür:

![Hizmet veri yolu 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

Burada Hello yapılandırması aynı toohello önceki sıra tabanlı tasarım gerçekleştirir. Diğer bir deyişle, yönlendirilmiş toohello toohello konu gönderilen iletiler olan **stok** abonelikten hangi hello **Stok yönetim sisteminin** bunları kullanır.

Sipariş toosupport hello Yönetimi panosunda, biz ikinci abonelik hello konuyla ilgili aşağıda gösterildiği gibi oluşturun:

![Hizmet veri yolu 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

Bu yapılandırma ile kullanılabilir tooboth hello hello POS Terminal her iletiden yapılan **Pano** ve **stok** abonelikleri.

## <a name="show-me-hello-code"></a>Merhaba Kodu Göster
Merhaba makale [Service Bus kuyruklarını kullanan uygulamalar oluşturmak](service-bus-create-queues.md) açıklar nasıl toosign bir Azure hesabı için ve bir hizmet ad alanı oluşturun. Merhaba en kolay yolu tooreference Service Bus bağımlılıklarıyla olan tooinstall hello Service Bus [Nuget paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). Ayrıca, Service Bus kitaplıkları hello Azure SDK'sı bir parçası olarak hello bulabilirsiniz. Merhaba indirme sırasında hello kullanılabilir [Azure SDK'sını indirme sayfası](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Merhaba konu ve abonelik oluşturma
Service Bus Mesajlaşma varlıkları (kuyruklar ve yayımlama/abonelik konuları) hello gerçekleştirilen yönetim işlemlerinin [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) sınıfı. Uygun kimlik bilgilerini sipariş toocreate gerekli bir **NamespaceManager** örneği için belirli bir ad alanı. Service Bus kullanan bir [paylaşılan erişim imzası (SAS)](service-bus-sas.md) tabanlı güvenlik modeli. Merhaba [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) sınıfı, bazı iyi bilinen belirteç sağlayıcılarını döndüren fabrikada yerleştirilen yöntemleri bir güvenlik belirteci sağlayıcısı gösterir. Kullanacağız bir [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) yöntemi toohold hello SAS kimlik bilgileri. Merhaba [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) örneği ile Merhaba taban adresini hello Service Bus ad alanı hello belirteç sağlayıcısı ve ardından yapılandırılmıştır.

Merhaba [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) sınıfı yöntemleri toocreate sağlar, numaralandırır ve mesajlaşma varlıklarını silme. Merhaba gösterir nasıl hello burada gösterilen kodu **NamespaceManager** örneğidir oluşturulup kullanılan toocreate hello **DataCollectionTopic** konu.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Merhaba aşırı olduğuna dikkat edin [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) hello konu tooset özelliklerini etkinleştirme yöntemi. Örneğin, hello varsayılan yaşam süresi (TTL) değerini toohello konu gönderilen iletiler için ayarlayabilirsiniz. Ardından, hello eklemek **stok** ve **Pano** abonelikleri.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>İletileri toohello konu gönderin
Hizmet veri yolu varlıklar üzerinde çalıştırma işlemleri için; Örneğin, ileti gönderme ve alma, bir uygulama önce oluşturmanız gerekir bir [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) nesnesi. Benzer toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) hello sınıfı **Eventhubclient** örneği hello temel adresinden hello hizmet ad alanı ve hello belirteç sağlayıcısı oluşturulur.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Service Bus konularından, alınan gönderilen iletileri tooand hello bir örnekleridir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sınıfı. Bu sınıf bir standart özellikler kümesi içerir (gibi [etiket](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) ve [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), bir kullanılan toohold uygulama özellikleri sözlük ve rastgele uygulama verileri gövdesi içerir. Uygulama herhangi bir seri hale getirilebilir nesnesi geçirerek hello gövde ayarlayabilirsiniz (hello aşağıdaki örnek, başarılı bir **SalesData** hello POS terminal durumundan hello satış verileri temsil eden nesne), hello kullanacak [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello nesnesi. Alternatif olarak, bir [akış](https://msdn.microsoft.com/library/system.io.stream.aspx) nesne sağlanabilir.

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

Merhaba en kolay yolu toosend iletileri toohello konudur toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate bir [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) hello doğrudan nesnesinden [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) Örnek:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Abonelikten ileti alma
Benzer toousing kuyruklar, tooreceive iletileri kullanabileceğiniz bir abonelikten bir [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) doğrudan hello oluşturan nesne [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) kullanarak [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Kullanabilirsiniz Merhaba iki farklı modlarını alma (**ReceiveAndDelete** ve **PeekLock**) makalesinde ele alındığı gibi [Service Bus kuyruklarını kullanan uygulamalar oluşturmak](service-bus-create-queues.md).

Oluşturduğunuzda unutmayın bir **MessageReceiver** abonelikler için hello *entityPath* parametredir hello biçiminde `topicPath/subscriptions/subscriptionName`. Bu nedenle, toocreate bir **MessageReceiver** hello için **stok** hello aboneliği **DataCollectionTopic** konusuna *entityPath*çok ayarlanmalıdır`DataCollectionTopic/subscriptions/Inventory`. Merhaba kod aşağıdaki gibidir:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

## <a name="subscription-filters"></a>Abonelik filtreleri
Şu ana kadar bu senaryoda toohello konu gönderilen tüm iletiler kayıtlı kullanılabilir tooall abonelikleri hale getirilir. Burada anahtar tümcecik Hello "kullanılabilir hale getirilir." Hizmet veri yolu abonelikleri toohello konu gönderilen tüm iletiler görürsünüz, ancak yalnızca bir alt kümesini bu iletileri toohello sanal abonelik sırası kopyalayabilirsiniz. Bu aboneliği kullanarak gerçekleştirilir *filtreleri*. Bir abonelik oluşturduğunuzda, bir filtre ifadesi, selamlama iletisine hello özellikler üzerinde çalıştığı bir SQL92 stili koşulun hello formunda sağlayabilir, hem de Sistem özellikleri hello (örneğin, [etiket](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) ve hello uygulama özellikler gibi **StoreName** hello önceki örnekte.

Merhaba senaryo tooillustrate Bu gelişen, ikinci bir mağaza toobe eklenen tooour perakende senaryodur. Tüm hello POS Terminal hem depoları gelen satış verileri hala yönlendirilen toobe merkezi toohello Stok yönetim sisteminin sahip, ancak hello Pano aracını kullanarak bir mağaza yöneticisi yalnızca bu depoyu hello performansta ilgileniyor. Bu tooachieve filtreleme aboneliği kullanabilirsiniz. Merhaba POS Terminal iletileri yayımladığınızda, bunların hello ayarlamanız **StoreName** selamlama iletisine uygulama özelliği. İki depolar, örneğin verilen **Redmond** ve **Seattle**, hello POS Terminal hello Redmond, depolama damgası satış verilerini iletileri ile bir **StoreName** çok eşit **Redmond**, hello Seattle depolamak ancak POS Terminal kullanımı bir **StoreName** çok eşit**Seattle**. Hello mağaza yöneticisi hello Redmond depolamak yalnızca, kendi POS Terminal toosee verilerden istemektedir. Merhaba sistem aşağıdaki gibi görünür:

![Hizmet Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

Bu yönlendirme yukarı tooset, oluşturduğunuz hello **Pano** abonelik şekilde:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Bu [abonelik filtresi](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), hello olan iletiler **StoreName** çok ayarlanan özelliği**Redmond** kopyalanan toohello sanal sıra hello içinolacaktır**Pano** abonelik. Filtreleme, ancak daha fazla toosubscription yoktur. Tooa aboneliğin sanal kuyruğuna geçerken uygulamalar ayrıca toohello özelliği toomodify hello özelliklerinde bir ileti abonelik başına birden çok filtre kuralları sahip olabilir.

## <a name="summary"></a>Özet
Tüm hello nedeniyle toouse Queuing'in açıklanan [Service Bus kuyruklarını kullanan uygulamalar oluşturmak](service-bus-create-queues.md) tootopics, özellikle de geçerlidir:

* Zamana bağlı ayırma – ileti üreticileri ve tüketicileri sahip çevrimiçi toobe Merhaba aynı anda.
* Yük Dengeleme – yük genişliğindeki yükselmeleri yoğun yük yerine ortalama yük için sağlanan kullanıcı uygulamaları toobe etkinleştirme hello konu tarafından düzeltilmesini.
* Yük Dengeleme – benzer tooa sıra tooonly hello Tüketiciler, böylece Yük Dengeleme, bir karmalayan her ileti tek bir abonelik üzerinde dinleme birden çok rakip tüketiciye sahip olabilir.
* Gevşek bağlantı – mevcut uç noktaları; etkilemeden ağ Mesajlaşma hello geliştirin Örneğin, abonelik ekleme veya değiştirme tooa konu tooallow yeni Tüketiciler için filtreler.

## <a name="next-steps"></a>Sonraki adımlar

Bkz: [Service Bus kuyruklarını kullanan uygulamalar oluşturmak](service-bus-create-queues.md) toouse hello POS perakende senaryoda nasıl kuyruklar hakkında bilgi.

