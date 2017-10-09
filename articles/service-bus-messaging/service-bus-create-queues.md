---
title: "Azure Service Bus kuyruklarını kullanan aaaWrite uygulamaları | Microsoft Docs"
description: "Nasıl toowrite Azure Service Bus kullanan basit sıra tabanlı bir uygulama."
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
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Hizmet Veri Yolu kuyrukları kullanan uygulamalar oluşturma
Bu konu Service Bus kuyruklarını açıklar ve gösterir nasıl toowrite Service Bus kullanan basit sıra tabanlı bir uygulama.

Perakende satış verilerini gelen tek tek Point-of-Sale (Terminal olmalıdır POS) hello veri toodetermine hisse senedi yenilenir toobe olduğunda kullanan tooan Stok yönetim sisteminin yönlendirilecek hello world senaryodan göz önünde bulundurun. Bu çözüm hello Terminal hello Stok yönetim sisteminin arasında hello iletişimi için Service Bus Mesajlaşma hello aşağıdaki şekilde gösterildiği gibi kullanır:

![Service Bus kuyrukları görüntü 1](./media/service-bus-create-queues/IC657161.gif)

İletileri toohello göndererek satış verilerini her POS terminal raporları **DataCollectionQueue**. Merhaba Stok yönetim sistemi tarafından alınana kadar bu iletiler bu sırada kalır. Bu desen genellikle adlandırılır *zaman uyumsuz Mesajlaşma*, çünkü hello POS terminal toowait hello envanter yönetimi sistemi toocontinue işleme yanıt yok.

## <a name="why-queuing"></a>Queuing neden?
Bu uygulamasının gerekli tooset hello kod ele önce (zaman uyumlu olarak) toohello stok doğrudan yönetim sistemi hello POS Terminal sahip olmak yerine bu senaryoda bir sıra kullanmanın yararları hello konuşun göz önünde bulundurun.

### <a name="temporal-decoupling"></a>Zamana bağlı ayırma
Merhaba zaman uyumsuz Mesajlaşma düzeni sayesinde üreticileri ve tüketicileri çevrimiçi toobe hello yok aynı anda. Merhaba Mesajlaşma altyapısı depoladıktan iletileri hello kullanıcı taraf hazır tooreceive kadar bunları. Bu, dağıtılmış hello uygulamanın hello bileşenleri, ya da gönüllü kesilebilir anlamına gelir; Örneğin Bakım veya hello sisteminin tamamını etkilemeden tooa bileşen kilitlenme nedeniyle. Ayrıca, uygulama hello hello günün belirli zamanlarında yalnızca çevrimiçi toobe olabilir. Örneğin, bu perakende senaryoda hello Stok yönetim sisteminin yalnızca çevrimiçi toocome hello hello iş günü sonunda olabilir.

### <a name="load-leveling"></a>Yük Dengeleme
Her iş birimi için gerekli hello işleme süresi genellikle sabit iken birçok uygulamada sistem yükü zaman içinde değişir. Aracılığıyla ileti üreticileri ve sıra anlamına gelir, kullanıcı uygulama (Merhaba çalışan) hello tüketicileri toobe sahip yalnızca ortalama yük yoğun yük yerine tooservice sağlandı. Merhaba hello sıra derinliği büyüyecektir ve sözleşme gelen yük hello olarak değişir. Bu, doğrudan para şekilde toohello altyapı gerekli tooservice hello uygulama yük miktarı ile kaydeder.

![Service Bus kuyrukları görüntü 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Yük dengeleme
Hello yük arttıkça, daha fazla çalışan işlemi hello çalışan sırasından eklenen tooread olabilir. Her ileti tek hello çalışan işlemleri tarafından işlenir. Ayrıca, hesaba tooprocessing güç ile Merhaba çalışan bilgisayarlar farklılık gösterse bile iletileri kendi maksimum hızında çeker gibi hello çalışan bilgisayarlar optimum kullanım için bu çekme tabanlı yük dengeleme sağlar. Bu desen genellikle hello rakip tüketici düzeni olarak adlandırılır.

![Service Bus kuyruklarını 3 görüntü](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Gevşek bağlantı
Message queuing toointermediate ileti üreticileri ve tüketicileri arasında kullanarak hello bileşenleri arasında bir iç gevşek bağlantı sağlar. Üreticileri ve tüketicileri birbirinden farkında değildir çünkü bir tüketici hello üretici üzerinde hiçbir etkisi olmadan yükseltilebilir. Ayrıca, topoloji Mesajlaşma hello hello mevcut uç noktalar etkilemeden gelişmesi. Biz Yayınla/Abone ol hakkında konuşurken Biz bu daha ele alacağız.

## <a name="show-me-hello-code"></a>Merhaba Kodu Göster
bölümü gösterir nasıl aşağıdaki hello toouse Service Bus toobuild bu uygulama.

### <a name="sign-up-for-an-azure-account"></a>Azure hesabı için kaydolun
Service Bus ile çalışma sırasını toostart içinde bir Azure hesabınızın olması gerekir. Zaten bir yoksa, ücretsiz bir hesap için kaydolabilirsiniz [burada](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Ad alanı oluşturma
Abonelik aldıktan sonra şunları yapabilirsiniz [hizmet ad alanı oluşturma](service-bus-create-namespace-portal.md). Her ad alanı, Service Bus varlık kümesi için bir kapsam kapsayıcı görevi görür. Yeni ad alanınızı tüm Service Bus hesaplarında benzersiz bir ad verin. 

### <a name="install-hello-nuget-package"></a>Merhaba NuGet paketini yükleyin
toouse hello Service Bus ad alanı, bir uygulama hello Service Bus derlemesine, özellikle Microsoft.ServiceBus.dll başvurmalıdır. Bu derleme hello Microsoft Azure SDK'sı bir parçası olarak bulabilir ve hello indirme sırasında hello kullanılabilir [Azure SDK'sını indirme sayfası](https://azure.microsoft.com/downloads/). Ancak, hello [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus) hello en kolay yolu tooget hello hizmet veri yolu API'sini ve tooconfigure tüm hello Service Bus bağımlılıklarıyla uygulamanızla olduğu.

### <a name="create-hello-queue"></a>Merhaba kuyruk oluşturma
Service Bus Mesajlaşma varlıkları (kuyruklar ve yayımlama/abonelik konuları) hello gerçekleştirilen yönetim işlemlerinin [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) sınıfı. Service Bus kullanan bir [paylaşılan erişim imzası (SAS)](service-bus-sas.md) tabanlı güvenlik modeli. Merhaba [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) sınıfı, bazı iyi bilinen belirteç sağlayıcılarını döndüren fabrikada yerleştirilen yöntemleri bir güvenlik belirteci sağlayıcısı gösterir. Kullanacağız bir [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) yöntemi toohold hello SAS kimlik bilgileri. Merhaba [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) örneği ile Merhaba taban adresini hello Service Bus ad alanı hello belirteç sağlayıcısı ve ardından yapılandırılmıştır.

Merhaba [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) sınıfı yöntemleri toocreate sağlar, numaralandırır ve mesajlaşma varlıklarını silme. Merhaba gösterir nasıl hello burada gösterilen kodu [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) örneğidir oluşturulup kullanılan toocreate hello **DataCollectionQueue** sırası.

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

Merhaba aşırı olduğuna dikkat edin [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) ayarlanmış hello sıra toobe özelliklerini etkinleştirme yöntemi. Örneğin, hello varsayılan yaşam süresi (TTL) değerini toohello sıraya gönderilen iletiler için ayarlayabilirsiniz.

### <a name="send-messages-toohello-queue"></a>İletileri toohello sırası Gönder
Hizmet veri yolu varlıklar üzerinde çalıştırma işlemleri için; Örneğin, ileti gönderme ve alma, bir uygulama önce oluşturmanız gerekir bir [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) nesnesi. Benzer toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) hello sınıfı [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) örneği hello temel adresinden hello hizmet ad alanı ve hello belirteç sağlayıcısı oluşturulur.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

Gönderilen iletileri ve Service Bus alınan hello örnekleridir [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) sınıfı. Bu sınıf bir standart özellikler kümesi içerir (gibi [etiket](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) ve [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), bir kullanılan toohold uygulama özellikleri sözlük ve rastgele uygulama verileri gövdesi içerir. Uygulama herhangi bir seri hale getirilebilir nesnesi geçirerek hello gövde ayarlayabilirsiniz (hello aşağıdaki örnek, başarılı bir **SalesData** hello POS terminal durumundan hello satış verileri temsil eden nesne), hello kullanacak [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize hello nesnesi. Alternatif olarak, bir [akış](https://msdn.microsoft.com/library/system.io.stream.aspx) nesne sağlanabilir.

en kolay yolu toosend iletileri tooa sıra, servis talebi bizim hello verilen hello **DataCollectionQueue**, toouse olan [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate bir [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) nesnesi Merhaba doğrudan [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) örneği.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Merhaba sıradan ileti alma
kullanabileceğiniz hello sırasından tooreceive ileti, bir [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) doğrudan hello oluşturan nesne [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) kullanarak [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). İleti alıcılar, iki farklı modda çalışabilir: **ReceiveAndDelete** ve **PeekLock**. Merhaba [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) hello ileti alıcı oluşturulduğunda, bir parametre toohello ayarlanmış [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) çağırın.

Merhaba kullanırken **ReceiveAndDelete** hello modu, alma bir tek işlemi; diğer bir deyişle, Service Bus hello isteği aldığında, onu hello iletiyi kullanılıyor olarak işaretler ve toohello uygulama döndürür. **ReceiveAndDelete** modu hello en basit modeldir ve hangi hello uygulama tolerans hata toooccur olsaydı bir ileti işlenmiyor senaryolarda en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu hello iletiyi kullanılıyor olarak işaretlenmiş olduğundan, ne zaman hello uygulama yeniden başlatıldıktan ve iletileri tekrar, kullanmaya başlar, hello kilitlenme önce kullanılan hello iletiyi atlamış olur.

İçinde **PeekLock** hello modu, alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur. Service Bus hello isteği aldığında, hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) hello alınan ileti üzerinde. Hizmet veri yolu hello gördüğünde [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) çağrısı hello iletiyi kullanılıyor olarak işaretler.

Diğer iki sonuçlar mümkündür. İlk olarak, Merhaba uygulaması kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı işleyememesi [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) hello alınan ileti üzerinde (yerine [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Bu hizmet veri yolu toounlock selamlama iletisine neden olur ve yeniden alınan kullanılabilir toobe olun, ya da aynı tüketici hello veya başka bir Tamamlanıyor tüketici tarafından. İkinci olarak, hello kilidi ile ilişkili bir zaman aşımı yoktur ve selamlama iletisine Merhaba uygulaması işleyemezse (örneğin, hello uygulama çökerse) Service Bus kilidini hello kilit zaman aşımı dolmadan önce iletiyi hello ve kullanılabilir toobe yapın yeniden alınan (temelde gerçekleştiren bir [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) işlemi varsayılan olarak).

Merhaba, uygulama hello iletisini işledikten sonra ancak hello önce çöküyor Not [tam](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) isteği yayınlandı, başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır * en az bir kez * işleniyor. Başka bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa ek mantık hello uygulama toodetect çoğaltmaları gereklidir. Bu hello üzerinde temel sağlanabilir [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) hello iletinin özelliği. Bu özellik başlangıç değeri teslimat denemelerinde. Bu adlandırılır *tam olarak bir kez* işleme.

Merhaba burada gösterilen kodu alır ve hello kullanarak ileti işler **PeekLock** yoksa hello varsayılandır modu [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) değeri açıkça sağlanır.

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

### <a name="use-hello-queue-client"></a>Merhaba sıra İstemcisi'ni kullanın
Merhaba daha önce oluşturulan bu bölümdeki örnekleri [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) ve [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) hello doğrudan nesnelerden [Eventhubclient](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend ileti alıp Merhaba sırasından sırasıyla. Alternatif bir yaklaşım toouse olan bir [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) destekleyen hem gönderme ve alma işlemlerinin eklenmesi toomore nesne Gelişmiş oturumları gibi özellikleri.

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
Sıraların hello temel bilgileri öğrendiğinize göre bkz: [Service Bus konuları ve abonelikleri kullanan uygulamalar oluşturmak](service-bus-create-topics-subscriptions.md) toocontinue hello yayımlama/abonelik yetenekleri Service Bus konuları kullanarak bu tartışma ve Abonelikler.

