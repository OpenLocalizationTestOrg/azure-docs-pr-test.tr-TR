---
title: "Java ile aaaHow toouse Azure Service Bus kuyrukları | Microsoft Docs"
description: "Azure'da nasıl toouse Service Bus kuyrukları öğrenin. Java dilinde yazılan kod örnekleri."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a>Java ile nasıl toouse Service Bus kuyrukları
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Bu makalede nasıl toouse Service Bus kuyruklarını. Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure SDK][Azure SDK for Java]. Merhaba kapsanan senaryolar dahil **sıra oluşturma**, **ileti gönderme ve alma**, ve **sıraları silme**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Uygulama toouse Service Bus yapılandırın
Merhaba yüklediğinizden emin olun [Java için Azure SDK] [ Azure SDK for Java] önce bu örnek oluşturma. Eclipse kullanıyorsanız, hello yükleyebilirsiniz [Eclipse için Azure Araç Seti] [ Azure Toolkit for Eclipse] hello Java için Azure SDK'sı içerir. Merhaba daha sonra ekleyebilirsiniz **Java için Microsoft Azure kitaplıkları** tooyour proje:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Merhaba aşağıdakileri ekleyin `import` deyimleri toohello dosyasının üst kısmında hello Java:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Bir kuyruk oluşturma
Service Bus kuyruklarına yönelik yönetim işlemlerini aracılığıyla gerçekleştirilebilecek **ServiceBusContract** sınıfı. A **ServiceBusContract** nesnesini izinlere toomanage ile SAS belirteci ve hello yalıtır uygun bir yapılandırma ile oluşturulan **ServiceBusContract** sınıftır hello tek nokta Azure ile iletişimi.

Merhaba **ServiceBusService** sınıfı yöntemleri toocreate sağlar, sıralama ve sıraları silme. gösterir aşağıdaki örnekte nasıl hello bir **ServiceBusService** nesne adlı bir sırası kullanılan toocreate olabilir `TestQueue`, adlı bir ad alanı ile `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Yöntemleri vardır `QueueInfo` ayarlanmış hello sıra toobe özelliklerini izin ver (örneğin: tooset hello varsayılan yaşam süresi (TTL) değerini uygulanan toobe toomessages toohello sıraya gönderilen). Merhaba aşağıdaki örnekte nasıl toocreate adlı bir sırası gösterilmektedir `TestQueue` maksimum 5 GB boyuta sahip:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Merhaba kullanabileceğinizi unutmayın `listQueues` yöntemi **ServiceBusContract** belirtilen ada sahip bir sıra içinde hizmet ad alanı zaten varsa toocheck nesneleri.

## <a name="send-messages-tooa-queue"></a>İletileri tooa sırası Gönder
toosend ileti tooa Service Bus kuyruğuna, uygulamanızın alacağı bir **ServiceBusContract** nesnesi. kodun gösterdiği nasıl aşağıdaki hello toosend hello için bir ileti `TestQueue` hello daha önce oluşturduğunuz sıra `HowToSample` ad alanı:

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Gönderilen iletileri ve Service Bus alınan hello örnekleridir [BrokeredMessage] [ BrokeredMessage] sınıfı. [BrokeredMessage] [ BrokeredMessage] nesneleri olan bir standart özellikler kümesi (gibi [etiket](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) ve [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), kullanılan toohold özel bir sözlüğü uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi. Bir uygulama herhangi bir seri hale getirilebilir nesnesi hello hello oluşturucusuna geçirerek hello hello ileti gövdesini ayarlayabilir [BrokeredMessage][BrokeredMessage], ve hello uygun seri hale getirici sonra kullanılacak tooserialize hello nesnesi. Alternatif olarak, sağlayabilir bir **java. G/Ç. InputStream** nesnesi.

Merhaba aşağıdaki örnekte nasıl toothe toosend beş test iletisi gösteren `TestQueue` **MessageSender** biz hello önceki kod parçacığında elde:

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.

## <a name="receive-messages-from-a-queue"></a>Kuyruktan ileti alma
Merhaba birincil yolu tooreceive iletilerin bir kuyruktan toouse olan bir **ServiceBusContract** nesnesi. Alınan iletiler, iki farklı modda çalışabilir: **ReceiveAndDelete** ve **PeekLock**.

Merhaba kullanırken **ReceiveAndDelete** modu, alma bir tek işlemi - diğer bir deyişle, hizmet veri yolu bir kuyrukta İletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toohello uygulama döndürür. **ReceiveAndDelete** (Merhaba varsayılan mod budur) modunda hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.
Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

İçinde **PeekLock** modu, alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin **silmek** hello alınan ileti üzerinde. Hizmet veri yolu hello gördüğünde **silmek** çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.

Merhaba aşağıdaki örnekte nasıl iletilerin alındığını ve işlenen kullanarak gösteren **PeekLock** (Merhaba varsayılan modu değil). Merhaba aşağıdaki örnek sonsuz bir döngüde yapar ve içine geldikçe iletileri işleyen bizim `TestQueue`:

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
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
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
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
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz **unlockMessage** hello alınan ileti üzerinde yöntemi (hello yerine **deleteMessage** yöntemi). Hizmet veri yolu toounlock hello hello sıra içinde ileti gönderme ve yeniden alınan kullanılabilir toobe olun Bu nedenler ya da göre hello aynı uygulama veya başka bir kullanıcı uygulama tarafından kullanma.

Ayrıca, kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve Merhaba uygulaması tooprocess başarısız olursa (örneğin, hello uygulama çökerse) kilit zaman aşımı süresi dolmadan önce iletiyi hello sonra Service Bus selamlama iletisine otomatik olarak kilidini açar ve yeniden alınan kullanılabilir toobe kolaylaştırır.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor **deleteMessage** isteği bildirilmeden sonra hello ileti yeniden teslim toohello uygulama başlatıldığında içindir. Bu genellikle adlandırılır *en az bir kez işleme*; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle hello kullanılarak elde edilen **getMessageId** teslimat denemelerinde hello iletisinin yöntemi.

## <a name="next-steps"></a>Sonraki Adımlar
Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [kuyruklar, konu başlıkları ve abonelikler] [ Queues, topics, and subscriptions] daha fazla bilgi için.

Daha fazla bilgi için bkz: Merhaba [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
