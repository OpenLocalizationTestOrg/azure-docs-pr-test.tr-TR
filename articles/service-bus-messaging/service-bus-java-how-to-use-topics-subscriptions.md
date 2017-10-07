---
title: "Java ile aaaHow toouse Azure Service Bus konularını | Microsoft Docs"
description: "Azure'da Service Bus konuları ve abonelikleri kullanın."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>Nasıl toouse Service Bus konuları ve abonelikleri Java ile

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Bu kılavuzda açıklanmaktadır nasıl toouse Service Bus konuları ve abonelikleri. Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure SDK][Azure SDK for Java]. Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **iletileri tooa konu gönderme**, **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Service Bus konuları ve abonelikleri nelerdir?
Service Bus konuları ve abonelikleri *publish/subscribe* mesajlaşma iletişim modelini destekler. Konular ve abonelikler kullanıldığında, dağıtılmış uygulamanın bileşenleri birbirleriyle doğrudan iletişim kurmazlar; bunun yerine bir aracı gibi davranan bir konu aracılığıyla iletileri değiş tokuş eder.

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

Service Bus kuyruklarının tersine, burada her ileti bir tüketici tarafından işlenir; konular ve abonelikler, publish/subscribe modelini kullanarak iletişimin "bir-çok" biçimini sağlar. Birden çok abonelik tooa konu kaydetmek mümkündür. Tooa konu bir ileti gönderildiğinde, ardından kullanılabilir tooeach abonelik toohandle/işlem bağımsız olarak yapılır.

Bir abonelik tooa konu toohello konu gönderilen Merhaba iletileri kopyalarını alan sanal kuyruğa benzer. Filtre kuralları toofilter kısıtlamak/hangi iletileri tooa konu hangi konu abonelikleriyle alınan sağlayan bir abonelik başına temelinde bir konu için isteğe bağlı olarak kaydedebilirsiniz.

Service Bus konuları ve abonelikleri çok sayıda kullanıcılar ve uygulamalar arasında tooscale tooprocess iletileri çok fazla sayıda etkinleştirin.

## <a name="create-a-service-namespace"></a>Hizmet ad alanı oluşturma
Azure'da Service Bus konuları ve abonelikleri kullanarak toobegin ilk uygulamanızı Service Bus kaynaklarını adreslemek için kapsam bir kapsayıcı sağlar bir ad alanı oluşturmanız gerekir.

toocreate bir ad alanı:

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Uygulama toouse Service Bus yapılandırın
Merhaba yüklediğinizden emin olun [Java için Azure SDK] [ Azure SDK for Java] önce bu örnek oluşturma. Eclipse kullanıyorsanız, hello yükleyebilirsiniz [Eclipse için Azure Araç Seti] [ Azure Toolkit for Eclipse] hello Java için Azure SDK'sı içerir. Merhaba daha sonra ekleyebilirsiniz **Java için Microsoft Azure kitaplıkları** tooyour proje:

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Merhaba aşağıdakileri ekleyin `import` deyimleri toohello dosyasının üst kısmında hello Java:

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Java tooyour için Hello Azure kitaplıkları yolu oluştur ve proje dağıtım derlemenizi dahil ekleyin.

## <a name="create-a-topic"></a>Konu başlığı oluşturma
Service Bus konu başlıklarına yönelik yönetim işlemlerini aracılığıyla gerçekleştirilebilecek **ServiceBusContract** sınıfı. A **ServiceBusContract** nesnesini izinlere toomanage ile SAS belirteci ve hello yalıtır uygun bir yapılandırma ile oluşturulan **ServiceBusContract** sınıftır hello tek nokta Azure ile iletişimi.

Merhaba **ServiceBusService** sınıfı yöntemleri toocreate sağlar, sıralama ve konuları silin. örnekte gösterildiği nasıl aşağıdaki hello bir **ServiceBusService** nesnesi, bir konu adında kullanılan toocreate olabilir `TestTopic`, adlı bir ad alanı ile `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Yöntemleri vardır **TopicInfo** ayarlanacak hello konu özelliklerini etkinleştirme (örneğin: tooset hello varsayılan yaşam süresi (TTL) değerini uygulanan toobe toomessages gönderilen toohello konu). Merhaba aşağıdaki örnekte nasıl toocreate bir konu adlı gösterir `TestTopic` maksimum 5 GB boyuta sahip:

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Merhaba kullanabileceğinizi unutmayın **listTopics** yöntemi **ServiceBusContract** bir hizmet ad alanında belirtilen ada sahip bir konu zaten varsa toocheck nesneleri.

## <a name="create-subscriptions"></a>Abonelikleri oluşturma
Abonelikler tootopics de hello ile oluşturulan **ServiceBusService** sınıfı. Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna gönderilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma
Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir. Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu aboneliğin sanal kuyruğuna yerleştirilir. Merhaba aşağıdaki örnekte "AllMessages" adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Filtre içeren abonelik oluşturma
Hangi iletilerin tooa konu içinde belirli konu aboneliği göstermelidir gönderilen tooscope sağlayan filtreler de oluşturabilirsiniz.

Merhaba en esnek filtre abonelikler tarafından desteklenen türünde [SqlFilter][SqlFilter], SQL92 alt kümesi uygular. SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır. Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla ayrıntı için gözden [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sözdizimi.

Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir [SqlFilter] [ SqlFilter] yalnızca özel iletileri seçen nesne **MessageNumber** özellik 3'ten büyük:

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir [SqlFilter] [ SqlFilter] yalnızca sahip iletileri seçen nesnesi bir **MessageNumber** özelliği daha az veya bu değere eşit too3:

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

Ne zaman bir ileti artık gönderilir çok`TestTopic`, her zaman abone tooreceivers toohello teslim `AllMessages` abonelik ve abone olunan seçmeli olarak teslim tooreceivers toohello `HighMessages` ve `LowMessages` abonelikleri () ileti içeriği bağlı olarak).

## <a name="send-messages-tooa-topic"></a>İletileri tooa konu gönderin
toosend ileti tooa Service Bus konu, uygulamanızı alacağı bir **ServiceBusContract** nesnesi. Merhaba aşağıdaki kodu gösterir nasıl toosend hello için bir ileti `TestTopic` hello içinde daha önce oluşturduğunuz konu `HowToSample` ad alanı:

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

TooService Bus konu başlıklarına gönderilen iletiler örnekleridir [BrokeredMessage] [ BrokeredMessage] sınıfı. [BrokeredMessage][BrokeredMessage]* nesneler sahip bir dizi standart yöntem (gibi **setLabel** ve **TimeToLive**), kullanılan toohold özel bir sözlüğü uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi. Bir uygulama herhangi bir seri hale getirilebilir nesnesi hello oluşturucusuna geçirerek ileti gövdesini hello ayarlayabilirsiniz [BrokeredMessage][BrokeredMessage]ve hello uygun **DataContractSerializer**  kullanılan tooserialize hello nesne sonra olacaktır. Alternatif olarak, bir **java.io.InputStream** sağlanabilir.

Merhaba aşağıdaki örnekte nasıl toothe toosend beş test iletisi gösteren `TestTopic` **MessageSender** biz hello kod parçacığında yukarıdaki elde.
Not nasıl hello **MessageNumber** her ileti özelliği değeri değişir hello döngü hello yinelemesi (Bu alacak abonelikleri belirler):

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.

## <a name="how-tooreceive-messages-from-a-subscription"></a>Nasıl tooreceive abonelikten iletileri
bir aboneliğe ilişkin tooreceive iletileri kullanan bir **ServiceBusContract** nesnesi. Alınan iletiler, iki farklı modda çalışabilir: **ReceiveAndDelete** ve **PeekLock**.

Merhaba kullanırken **ReceiveAndDelete** modu, alma bir tek işlemi - diğer bir deyişle, Service Bus iletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toothe uygulama döndürür. **ReceiveAndDelete** modu hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu ileti hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş olduğundan, onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

İçinde **PeekLock** modu, alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin **silmek** hello alınan ileti üzerinde. Hizmet veri yolu hello gördüğünde **silmek** çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello konusundan kaldırın.

Merhaba aşağıdaki örnek nasıl ileti aldı ve işlenen kullanarak gösterir **PeekLock** (Merhaba varsayılan modu değil). Merhaba aşağıdaki örnek bir döngü gerçekleştirir ve hello "HighMessages" abonelik iletilerinde işler ve daha fazla ileti olduğunda çıkar (Alternatif olarak, yeni iletiler için toowait ayarlanması).

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz **unlockMessage** hello alınan ileti üzerinde yöntemi (hello yerine **deleteMessage** yöntemi). Bu hizmet veri yolu toounlock selamlama iletisine hello konusu içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.

Ayrıca konusu içinde kilitli bir ileti ile ilişkili bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine otomatik olarak kilitlenmeden kilit zaman aşımı dolmadan ve yeniden alınan kullanılabilir toobe yapın.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor **deleteMessage** isteği bildirilmeden sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır **en az bir kez işleme**, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle hello kullanılarak elde edilen **getMessageId** teslimat denemelerinde hello iletisinin yöntemi.

## <a name="delete-topics-and-subscriptions"></a>Konu başlıklarını ve abonelikleri silme
birincil yolu toodelete konuları hello ve abonelikleri içindir toouse bir **ServiceBusContract** nesnesi. Konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikler de silinir. Ayrıca, abonelikler bağımsız olarak da silinebilir.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Sonraki Adımlar
Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [Service Bus kuyrukları, konu başlıkları ve abonelikler] [ Service Bus queues, topics, and subscriptions] daha fazla bilgi için.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
