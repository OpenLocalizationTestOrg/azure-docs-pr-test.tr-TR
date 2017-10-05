---
title: "Java kullanarak Azure Event Hubs'tan gelen olayları alma | Microsoft Docs"
description: "Java kullanarak Event Hubs'dan alma kullanmaya başlama"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 3c1b455e6298367dc50f0943b58f6cf1e7f1c5fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="06dc5-103">Java kullanarak Azure Event Hubs'tan gelen olayları alma</span><span class="sxs-lookup"><span data-stu-id="06dc5-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="06dc5-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="06dc5-104">Introduction</span></span>
<span data-ttu-id="06dc5-105">Olay hub'ları saniye başına milyonlarca olayı alma, bir uygulamaya etkinleştirme işlemek ve veri bağlı cihazlarınız ve uygulamalarınız tarafından üretilen oldukça büyük miktardaki analiz bir yüksek düzeyde ölçeklenebilir bir alım sistemine olur.</span><span class="sxs-lookup"><span data-stu-id="06dc5-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="06dc5-106">Veriler Event Hubs hizmetinde toplandığında, herhangi bir gerçek zamanlı analitik sağlayıcısı veya depolama kümesi kullanarak bu verileri dönüştürebilir veya depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06dc5-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="06dc5-107">Daha fazla bilgi için bkz: [Event Hubs'a genel bakış][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="06dc5-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="06dc5-108">Bu öğretici Java'da yazılmış bir konsol uygulaması kullanarak bir event hub içine olaylarını almak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="06dc5-108">This tutorial shows how to receive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06dc5-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="06dc5-109">Prerequisites</span></span>

<span data-ttu-id="06dc5-110">Bu öğreticiyi tamamlamak için aşağıdaki önkoşullar gerekir:</span><span class="sxs-lookup"><span data-stu-id="06dc5-110">In order to complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="06dc5-111">Java geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="06dc5-111">A Java development environment.</span></span> <span data-ttu-id="06dc5-112">Bu öğretici için varsayıyoruz [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="06dc5-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="06dc5-113">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="06dc5-113">An active Azure account.</span></span> <br/><span data-ttu-id="06dc5-114">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06dc5-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="06dc5-115">Ayrıntılı bilgi için bkz. <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.</span><span class="sxs-lookup"><span data-stu-id="06dc5-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="06dc5-116">Java’da EventProcessorHost bulunan iletiler alma</span><span class="sxs-lookup"><span data-stu-id="06dc5-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="06dc5-117">**EventProcessorHost** kalıcı denetim noktalarını yöneterek Event Hubs'a ait alma olaylarını basitleştiren bir Java sınıfı ve paralel alımları bu Event Hubs'a ait.</span><span class="sxs-lookup"><span data-stu-id="06dc5-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="06dc5-118">EventProcessorHost kullanarak, olayları birden çok alıcı arasında farklı düğümlerde barındırıldığında bile bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06dc5-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="06dc5-119">Bu örnek, tek alıcı için EventProcessorHost’un nasıl kullanıldığını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="06dc5-119">This example shows how to use EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="06dc5-120">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06dc5-120">Create a storage account</span></span>
<span data-ttu-id="06dc5-121">EventProcessorHost kullanmak için olmalıdır bir [Azure depolama hesabı][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="06dc5-121">To use EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="06dc5-122">Oturum [Azure portal][Azure portal], tıklatıp **+ yeni** ekranın sol taraftaki.</span><span class="sxs-lookup"><span data-stu-id="06dc5-122">Log on to the [Azure portal][Azure portal], and click **+ New** on the left-hand side of the screen.</span></span>
2. <span data-ttu-id="06dc5-123">**Depolama** ve ardından **Depolama hesabı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06dc5-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="06dc5-124">**Depolama hesabı oluştur** dikey penceresinde depolama hesabı için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="06dc5-124">In the **Create storage account** blade, type a name for the storage account.</span></span> <span data-ttu-id="06dc5-125">Alanları geri kalanını tamamlamak için istediğiniz bölgeyi seçin ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="06dc5-125">Complete the rest of the fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="06dc5-126">Yeni oluşturulan depolama hesabına ve **Erişim Tuşlarını Yönet**’e tıklayın:</span><span class="sxs-lookup"><span data-stu-id="06dc5-126">Click the newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="06dc5-127">Birincil erişim tuşunu daha sonra Bu öğreticide kullanmak için geçici bir konuma kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="06dc5-127">Copy the primary access key to a temporary location, to use later in this tutorial.</span></span>

### <a name="create-a-java-project-using-the-eventprocessor-host"></a><span data-ttu-id="06dc5-128">EventProcessor Ana Bilgisayarını kullanarak Java projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06dc5-128">Create a Java project using the EventProcessor Host</span></span>
<span data-ttu-id="06dc5-129">Olay hub'ları için Java istemci kitaplığı Maven projelerden kullanmak için kullanılabilir [Maven merkezi bir depoya][Maven Package]ve aşağıdaki bağımlılığı bildirimi, Maven içinde kullanarak başvurulabilir Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="06dc5-129">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository][Maven Package], and can be referenced using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="06dc5-130">Derleme ortamları farklı türleri için en son yayımlanan JAR dosyalarını açıkça edinebilirsiniz [Maven merkezi bir depoya] [ Maven Package] veya [GitHub yayın dağıtım noktasında ](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="06dc5-130">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository][Maven Package] or from [the release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="06dc5-131">Aşağıdaki örnek için önce en sevdiğiniz Java geliştirme ortamında bir konsol/kabuk uygulaması için yeni bir Maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06dc5-131">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="06dc5-132">Sınıf adı verilen `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="06dc5-132">The class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="06dc5-133">`EventProcessor` adlı yeni bir sınıf oluşturmak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="06dc5-133">Use the following code to create a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="06dc5-134">Adlı bir sınıf oluşturma `EventProcessorSample`, aşağıdaki kodu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="06dc5-134">Create one more class called `EventProcessorSample`, using the following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter to stop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="06dc5-135">Aşağıdaki alanları olay hub'ı ve depolama hesabı oluştururken kullanılan değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06dc5-135">Replace the following fields with the values used when you created the event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="06dc5-136">Bu öğretici, EventProcessorHost’un tek bir örneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="06dc5-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="06dc5-137">Verimliliğini artırmak için birden çok örneğini EventProcessorHost, tercihen ayrı makinelerde çalıştırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="06dc5-137">To increase throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="06dc5-138">Bu da artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="06dc5-138">This provides redundancy as well.</span></span> <span data-ttu-id="06dc5-139">Böyle durumlarda, alınan olayların yük dengesi için çeşitli örnekler otomatik olarak birbirleriyle koordine olurlar.</span><span class="sxs-lookup"><span data-stu-id="06dc5-139">In those cases, the various instances automatically coordinate with each other in order to load balance the received events.</span></span> <span data-ttu-id="06dc5-140">Birden çok alıcının her birinin *tüm* olayları işlemesini istiyorsanız **ConsumerGroup** kavramını kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="06dc5-140">If you want multiple receivers to each process *all* the events, you must use the **ConsumerGroup** concept.</span></span> <span data-ttu-id="06dc5-141">Olaylar farklı makinelerden alındığında, dağıtıldıkları makineleri (veya rolleri) temel alan EventProcessorHost örnekleri için ad belirtmek yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="06dc5-141">When receiving events from different machines, it might be useful to specify names for EventProcessorHost instances based on the machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="06dc5-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="06dc5-142">Next steps</span></span>
<span data-ttu-id="06dc5-143">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="06dc5-143">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="06dc5-144">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="06dc5-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="06dc5-145">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06dc5-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="06dc5-146">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="06dc5-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
