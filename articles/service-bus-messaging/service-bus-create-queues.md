---
title: "Azure Service Bus kuyruklarını kullanan uygulamalar yazma | Microsoft Docs"
description: "Azure Service Bus kullanan bir basit sıra tabanlı uygulamasının nasıl yazılacağını."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 419caff7e8ceeb419c89a2ef9a6614c1accf3e52
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Hizmet Veri Yolu kuyrukları kullanan uygulamalar oluşturma
Bu konu, Service Bus kuyruklarını açıklar ve Service Bus kullanan bir basit sıra tabanlı uygulamasının nasıl yazılacağını gösterir.

Perakende satış verilerinden ayrı Point-of-Sale (POS) Terminal yenilenecek hisse sahip olduğunda belirlemek için veri kullanan bir stok yönetim sisteminin yönlendirilmesi gereken dünyadan bir senaryo düşünün. Bu çözüm aşağıdaki resimde gösterildiği gibi Terminal ve stok yönetim sistemi arasındaki iletişim için Service Bus Mesajlaşma kullanır:

![Service Bus kuyrukları görüntü 1](./media/service-bus-create-queues/IC657161.gif)

İletiler göndererek satış verilerini her POS terminal raporları **DataCollectionQueue**. Stok yönetim sistemi tarafından alınana kadar bu iletiler bu sırada kalır. Bu desen genellikle adlandırılır *zaman uyumsuz Mesajlaşma*, POS terminal işleme devam etmek için Stok yönetim sisteminin yanıt beklemesi gerekmez.

## <a name="why-queuing"></a>Queuing neden?
Bu uygulamayı kurmak için gerekli kod ele önce POS Terminal sahip olmak yerine bu senaryoda bir sıra kullanmanın yararları konuşun doğrudan göz önünde bulundurun (zaman uyumlu olarak) Stok yönetim sistemine.

### <a name="temporal-decoupling"></a>Zamana bağlı ayırma
Zaman uyumsuz Mesajlaşma düzeni sayesinde üreticilerin ve tüketicilerin aynı anda çevrimiçi olması gerekmez. Kullanıcı tarafı almaya hazır olana kadar ileti altyapısı iletileri güvenilir bir şekilde depolar. Bu dağıtılmış uygulamanın bileşenleri, ya da gönüllü kesilebilir anlamına gelir; Örneğin, bakım için veya bir bileşen çökmesinden dolayı olmadan tüm sisteme etkileyen. Ayrıca, kullanıcı uygulamanın yalnızca günün belirli zamanlarında çevrimiçi olması gerekebilir. Örneğin, bu perakende senaryoda Stok yönetim sisteminin sadece iş günü sonunda çevrimiçi olması gerekebilir.

### <a name="load-leveling"></a>Yük Dengeleme
Her iş birimi için gereken işleme süresi genellikle sabit iken birçok uygulamada sistem yükü zaman içinde değişir. Aracılığıyla ileti üreticileri ve tüketicileri bir kuyruk, kullanıcı uygulama (çalışan) yalnızca yoğun yük yerine ortalama yük hizmet vermek için sağlanacak olduğunu anlamına gelir. Sıra Derinliği büyür ve gelen Yük hacmi değiştikçe sözleşme. Bu, doğrudan para uygulama yükünü sunmak için gereken altyapı miktarı ile kaydeder.

![Service Bus kuyrukları görüntü 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Yük dengeleme
Yük arttıkça çalışan kuyruktan okunmak üzere daha fazla çalışan işlemi eklenebilir. Her ileti yalnızca bir çalışan işlemi tarafından işlenir. Ayrıca, çalışan bilgisayarlar işleme gücünü göre farklılık gösterse bile iletileri kendi maksimum hızında çeker gibi çalışan bilgisayarlar optimum kullanım için bu çekme tabanlı yük dengeleme sağlar. Bu model, genellikle rakip tüketici düzeni olarak adlandırılır.

![Service Bus kuyruklarını 3 görüntü](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Gevşek bağlantı
Message queuing ileti üreticileri ve tüketicileri arasında Orta kullanarak bileşenleri arasında bir iç gevşek bağlantı sağlar. Üreticileri ve tüketicileri birbirinden farkında değildir çünkü bir tüketici üretici üzerinde hiçbir etkisi olmadan yükseltilebilir. Ayrıca, Mesajlaşma topolojisi mevcut uç noktalar etkilemeden gelişmesi. Biz Yayınla/Abone ol hakkında konuşurken Biz bu daha ele alacağız.

## <a name="show-me-the-code"></a>Kod Göster
Aşağıdaki bölümde, Service Bus bu uygulama oluşturmak için nasıl kullanılacağını gösterir.

### <a name="sign-up-for-an-azure-account"></a>Azure hesabı için kaydolun
Service Bus ile çalışmaya başlamak için bir Azure hesabınızın olması gerekir. Zaten bir yoksa, ücretsiz bir hesap için kaydolabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Ad alanı oluşturma
Abonelik aldıktan sonra şunları yapabilirsiniz [hizmet ad alanı oluşturma](service-bus-create-namespace-portal.md). Her ad alanı, Service Bus varlık kümesi için bir kapsam kapsayıcı görevi görür. Yeni ad alanınızı tüm Service Bus hesaplarında benzersiz bir ad verin. 

### <a name="install-the-nuget-package"></a>NuGet paket yüklemesi
Hizmet veri yolu ad alanını kullanmak için bir uygulama Service Bus derlemesine, özellikle Microsoft.ServiceBus.dll başvurmalıdır. Microsoft Azure SDK'sı bir parçası olarak bu derleme bulabilir ve yükleme şu adresten edinilebilir [Azure SDK'sını indirme sayfası](https://azure.microsoft.com/downloads/). Ancak, [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus) Service Bus API'sini almanın ve uygulamanızı tüm Service Bus bağımlılıklarıyla yapılandırmanın en kolay yolu.

### <a name="create-the-queue"></a>Kuyruk oluşturma
Service Bus Mesajlaşma varlıkları (kuyruklar ve yayımlama/abonelik konuları) aracılığıyla gerçekleştirilir yönelik yönetim işlemlerini [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) sınıfı. Service Bus kullanan bir [paylaşılan erişim imzası (SAS)](service-bus-sas.md) tabanlı güvenlik modeli. [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) sınıfı, bazı iyi bilinen belirteç sağlayıcılarını döndüren fabrikada yerleştirilen yöntemleri bir güvenlik belirteci sağlayıcısı gösterir. Kullanacağız bir [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) SAS kimlik bilgilerini saklamak için yöntem. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) örneği sonra Service Bus ad alanı ve belirteç sağlayıcı taban adresi ile yapılandırılmıştır.

[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) sınıfı oluşturmak, numaralandırır ve mesajlaşma varlıkları silmek için yöntemler sağlar. Gösterir burada gösterilen kodu nasıl [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) örneği oluşturulur ve oluşturmak için kullanılan **DataCollectionQueue** sırası.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Vardır Not overloads [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) ayarlanmasına kuyruğun özelliklerini etkinleştirme yöntemi. Örneğin, kuyruğa gönderilen iletiler için varsayılan yaşam süresi (TTL) değerini ayarlayabilirsiniz.

### <a name="send-messages-to-the-queue"></a>Kuyruğa ileti gönderme
Hizmet veri yolu varlıklar üzerinde çalıştırma işlemleri için; Örneğin, ileti gönderme ve alma, bir uygulama önce oluşturmanız gerekir bir [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) nesnesi. Benzer şekilde [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) sınıfı, [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) örneği, hizmet ad alanı ve belirteç sağlayıcı temel adresinden oluşturulur.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

Gönderilen iletileri ve Service Bus alınan örnekleridir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sınıfı. Bu sınıf bir standart özellikler kümesi içerir (gibi [etiket](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) ve [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), bir uygulama özellikleri tutmak için kullanılan bir sözlük ve rastgele uygulama verileri gövdesi içerir. Bir uygulama herhangi bir seri hale getirilebilir nesnesi geçirerek gövdesi ayarlayabilirsiniz (aşağıdaki örnekte, geçirir bir **SalesData** POS terminal durumundan satış verilerini temsil eden nesne), hangi kullanacak [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) nesneyi serileştirmek için. Alternatif olarak, bir [akış](https://msdn.microsoft.com/library/system.io.stream.aspx) nesne sağlanabilir.

Bu örnekte belirli bir sıradaki iletiler göndermek için en kolay yolu **DataCollectionQueue**, kullanmaktır [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) oluşturmak için bir [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) doğrudan nesnesi gelen [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) örneği.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-the-queue"></a>Kuyruktan ileti alma
Kuyruktan iletileri almak için kullanabileceğiniz bir [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) doğrudan oluşturduğunuz nesne [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) kullanarak [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). İleti alıcılar, iki farklı modda çalışabilir: **ReceiveAndDelete** ve **PeekLock**. [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) ileti alıcı oluşturulduğunda bir parametre olarak ayarlanmış [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) çağırın.

Kullanırken **ReceiveAndDelete** modu, alma tek bir işlemdir; diğer bir deyişle, Service Bus isteği aldığında, iletiyi kullanılıyor olarak işaretler ve uygulamaya döndürür. **ReceiveAndDelete** modu en basit modeldir ve, uygulama tolerans gerçekleşmesi için bir hata varsa bir ileti işlenmiyor senaryolarda en iyi şekilde çalışır. Bu durumu daha iyi anlamak için müşterinin bir alma isteği bildirdiğini ve bu isteğin işlenmeden çöktüğünü varsayın. Service Bus iletiyi kullanılıyor olarak işaretlenmiş olduğundan, ne zaman iletileri tekrar, kullanmaya başlar ve uygulama yeniden başlatılmadan, kilitlenme önce kullanılan iletiyi atlamış olur.

İçinde **PeekLock** modu, alma, iletilere veremeyen uygulamaları desteklemenin mümkün kılar bir iki aşamalı işlemi haline gelir. Service Bus isteği aldığında, kullanılacak sonraki iletiyi bulur, diğer tüketicilerin iletiyi almasını engellemek için kilitler ve uygulamaya döndürür. Uygulama iletiyi işlemeyi tamamladıktan sonra (veya iletiyi daha sonra işlemek üzere güvenli şekilde depoladıktan sonra) alınan iletide [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) yöntemini çağırarak alma işleminin ikinci aşamasını tamamlar. Hizmet veri yolu gördüğünde [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) çağrısı, iletiyi kullanılıyor olarak işaretler.

Diğer iki sonuçlar mümkündür. İlk olarak, uygulama herhangi bir nedenden dolayı iletisi işleyemedi ise işleyememesi [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) alınan iletide (yerine [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Bu iletinin kilidini açmak ve aynı tüketici veya başka bir Tamamlanıyor tüketici tarafından tekrar alınabilir kullanılabilir hale getirmek Service Bus neden olur. İkinci olarak, kilidi ile ilişkili bir zaman aşımı yoktur ve uygulama (örneğin, uygulama çökerse) hizmet veri yolu ileti kilidini açmak ve onu kilit zaman aşımı dolmadan önce iletiyi işleyemezse kullanılabilir olması yeniden alınan) temelde gerçekleştiren bir [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) işlemi varsayılan olarak).

Sonra uygulama çökerse, ileti önce işleme Not [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) isteği yayınlandı, başlatıldığında ileti uygulamaya tekrar teslim edilir. Bu genellikle adlandırılır * en az bir kez * işleniyor. Başka bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda aynı ileti yeniden teslim. Senaryo yinelenen işlemeyi kabul etmiyorsa ek mantık yinelemeleri algılamak için uygulamada gereklidir. Bu temel sağlanabilir [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) iletinin özelliği. Bu özelliğin değeri teslimat denemelerinde. Bu adlandırılır *tam olarak bir kez* işleme.

Burada gösterilen kodu alan ve işleyen bir iletiyi kullanarak **PeekLock** yoksa varsayılan değer modu [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) değeri açıkça sağlanır.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
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

### <a name="use-the-queue-client"></a>Sıra istemcisini kullanın
Daha önce oluşturulan bu bölümdeki örnekleri [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) ve [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) doğrudan nesneleri [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) göndermek ve gelen iletileri almak için , sırasıyla sırası. Alternatif bir yaklaşım kullanmaktır bir [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) destekleyen hem gönderme ve alma işlemlerinin oturumları gibi daha gelişmiş özellikleri yanı sıra nesnesi.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Sonraki adımlar
Sıraların öğrendiğinize göre bkz: [Service Bus konuları ve abonelikleri kullanan uygulamalar oluşturmak](service-bus-create-topics-subscriptions.md) Service Bus konuları ve abonelikleri Yayımla ve abone yeteneklerini kullanarak bu tartışma devam etmek için.

