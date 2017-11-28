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
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="79fbb-104">Java ile nasıl toouse Service Bus kuyrukları</span><span class="sxs-lookup"><span data-stu-id="79fbb-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="79fbb-105">Bu makalede nasıl toouse Service Bus kuyruklarını.</span><span class="sxs-lookup"><span data-stu-id="79fbb-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="79fbb-106">Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure SDK][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="79fbb-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="79fbb-107">Merhaba kapsanan senaryolar dahil **sıra oluşturma**, **ileti gönderme ve alma**, ve **sıraları silme**.</span><span class="sxs-lookup"><span data-stu-id="79fbb-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="79fbb-108">Uygulama toouse Service Bus yapılandırın</span><span class="sxs-lookup"><span data-stu-id="79fbb-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="79fbb-109">Merhaba yüklediğinizden emin olun [Java için Azure SDK] [ Azure SDK for Java] önce bu örnek oluşturma.</span><span class="sxs-lookup"><span data-stu-id="79fbb-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="79fbb-110">Eclipse kullanıyorsanız, hello yükleyebilirsiniz [Eclipse için Azure Araç Seti] [ Azure Toolkit for Eclipse] hello Java için Azure SDK'sı içerir.</span><span class="sxs-lookup"><span data-stu-id="79fbb-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="79fbb-111">Merhaba daha sonra ekleyebilirsiniz **Java için Microsoft Azure kitaplıkları** tooyour proje:</span><span class="sxs-lookup"><span data-stu-id="79fbb-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="79fbb-112">Merhaba aşağıdakileri ekleyin `import` deyimleri toohello dosyasının üst kısmında hello Java:</span><span class="sxs-lookup"><span data-stu-id="79fbb-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="79fbb-113">Bir kuyruk oluşturma</span><span class="sxs-lookup"><span data-stu-id="79fbb-113">Create a queue</span></span>
<span data-ttu-id="79fbb-114">Service Bus kuyruklarına yönelik yönetim işlemlerini aracılığıyla gerçekleştirilebilecek **ServiceBusContract** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="79fbb-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="79fbb-115">A **ServiceBusContract** nesnesini izinlere toomanage ile SAS belirteci ve hello yalıtır uygun bir yapılandırma ile oluşturulan **ServiceBusContract** sınıftır hello tek nokta Azure ile iletişimi.</span><span class="sxs-lookup"><span data-stu-id="79fbb-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="79fbb-116">Merhaba **ServiceBusService** sınıfı yöntemleri toocreate sağlar, sıralama ve sıraları silme.</span><span class="sxs-lookup"><span data-stu-id="79fbb-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="79fbb-117">gösterir aşağıdaki örnekte nasıl hello bir **ServiceBusService** nesne adlı bir sırası kullanılan toocreate olabilir `TestQueue`, adlı bir ad alanı ile `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="79fbb-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

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

<span data-ttu-id="79fbb-118">Yöntemleri vardır `QueueInfo` ayarlanmış hello sıra toobe özelliklerini izin ver (örneğin: tooset hello varsayılan yaşam süresi (TTL) değerini uygulanan toobe toomessages toohello sıraya gönderilen).</span><span class="sxs-lookup"><span data-stu-id="79fbb-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="79fbb-119">Merhaba aşağıdaki örnekte nasıl toocreate adlı bir sırası gösterilmektedir `TestQueue` maksimum 5 GB boyuta sahip:</span><span class="sxs-lookup"><span data-stu-id="79fbb-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="79fbb-120">Merhaba kullanabileceğinizi unutmayın `listQueues` yöntemi **ServiceBusContract** belirtilen ada sahip bir sıra içinde hizmet ad alanı zaten varsa toocheck nesneleri.</span><span class="sxs-lookup"><span data-stu-id="79fbb-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="79fbb-121">İletileri tooa sırası Gönder</span><span class="sxs-lookup"><span data-stu-id="79fbb-121">Send messages tooa queue</span></span>
<span data-ttu-id="79fbb-122">toosend ileti tooa Service Bus kuyruğuna, uygulamanızın alacağı bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="79fbb-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="79fbb-123">kodun gösterdiği nasıl aşağıdaki hello toosend hello için bir ileti `TestQueue` hello daha önce oluşturduğunuz sıra `HowToSample` ad alanı:</span><span class="sxs-lookup"><span data-stu-id="79fbb-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

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

<span data-ttu-id="79fbb-124">Gönderilen iletileri ve Service Bus alınan hello örnekleridir [BrokeredMessage] [ BrokeredMessage] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="79fbb-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="79fbb-125">[BrokeredMessage] [ BrokeredMessage] nesneleri olan bir standart özellikler kümesi (gibi [etiket](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) ve [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), kullanılan toohold özel bir sözlüğü uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi.</span><span class="sxs-lookup"><span data-stu-id="79fbb-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="79fbb-126">Bir uygulama herhangi bir seri hale getirilebilir nesnesi hello hello oluşturucusuna geçirerek hello hello ileti gövdesini ayarlayabilir [BrokeredMessage][BrokeredMessage], ve hello uygun seri hale getirici sonra kullanılacak tooserialize hello nesnesi.</span><span class="sxs-lookup"><span data-stu-id="79fbb-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="79fbb-127">Alternatif olarak, sağlayabilir bir **java. G/Ç. InputStream** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="79fbb-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="79fbb-128">Merhaba aşağıdaki örnekte nasıl toothe toosend beş test iletisi gösteren `TestQueue` **MessageSender** biz hello önceki kod parçacığında elde:</span><span class="sxs-lookup"><span data-stu-id="79fbb-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

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

<span data-ttu-id="79fbb-129">Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="79fbb-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="79fbb-130">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="79fbb-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="79fbb-131">Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="79fbb-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="79fbb-132">Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="79fbb-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="79fbb-133">Kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="79fbb-133">Receive messages from a queue</span></span>
<span data-ttu-id="79fbb-134">Merhaba birincil yolu tooreceive iletilerin bir kuyruktan toouse olan bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="79fbb-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="79fbb-135">Alınan iletiler, iki farklı modda çalışabilir: **ReceiveAndDelete** ve **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="79fbb-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="79fbb-136">Merhaba kullanırken **ReceiveAndDelete** modu, alma bir tek işlemi - diğer bir deyişle, hizmet veri yolu bir kuyrukta İletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toohello uygulama döndürür.</span><span class="sxs-lookup"><span data-stu-id="79fbb-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="79fbb-137">**ReceiveAndDelete** (Merhaba varsayılan mod budur) modunda hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="79fbb-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="79fbb-138">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="79fbb-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="79fbb-139">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="79fbb-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="79fbb-140">İçinde **PeekLock** modu, alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="79fbb-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="79fbb-141">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="79fbb-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="79fbb-142">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin **silmek** hello alınan ileti üzerinde.</span><span class="sxs-lookup"><span data-stu-id="79fbb-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="79fbb-143">Hizmet veri yolu hello gördüğünde **silmek** çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="79fbb-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="79fbb-144">Merhaba aşağıdaki örnekte nasıl iletilerin alındığını ve işlenen kullanarak gösteren **PeekLock** (Merhaba varsayılan modu değil).</span><span class="sxs-lookup"><span data-stu-id="79fbb-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="79fbb-145">Merhaba aşağıdaki örnek sonsuz bir döngüde yapar ve içine geldikçe iletileri işleyen bizim `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="79fbb-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="79fbb-146">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="79fbb-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="79fbb-147">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="79fbb-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="79fbb-148">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz **unlockMessage** hello alınan ileti üzerinde yöntemi (hello yerine **deleteMessage** yöntemi).</span><span class="sxs-lookup"><span data-stu-id="79fbb-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="79fbb-149">Hizmet veri yolu toounlock hello hello sıra içinde ileti gönderme ve yeniden alınan kullanılabilir toobe olun Bu nedenler ya da göre hello aynı uygulama veya başka bir kullanıcı uygulama tarafından kullanma.</span><span class="sxs-lookup"><span data-stu-id="79fbb-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="79fbb-150">Ayrıca, kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve Merhaba uygulaması tooprocess başarısız olursa (örneğin, hello uygulama çökerse) kilit zaman aşımı süresi dolmadan önce iletiyi hello sonra Service Bus selamlama iletisine otomatik olarak kilidini açar ve yeniden alınan kullanılabilir toobe kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="79fbb-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="79fbb-151">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor **deleteMessage** isteği bildirilmeden sonra hello ileti yeniden teslim toohello uygulama başlatıldığında içindir.</span><span class="sxs-lookup"><span data-stu-id="79fbb-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="79fbb-152">Bu genellikle adlandırılır *en az bir kez işleme*; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="79fbb-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="79fbb-153">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="79fbb-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="79fbb-154">Bu genellikle hello kullanılarak elde edilen **getMessageId** teslimat denemelerinde hello iletisinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="79fbb-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79fbb-155">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="79fbb-155">Next Steps</span></span>
<span data-ttu-id="79fbb-156">Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [kuyruklar, konu başlıkları ve abonelikler] [ Queues, topics, and subscriptions] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="79fbb-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="79fbb-157">Daha fazla bilgi için bkz: Merhaba [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="79fbb-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
