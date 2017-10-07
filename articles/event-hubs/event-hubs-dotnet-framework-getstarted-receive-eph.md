---
title: "Azure Event Hubs kullanarak aaaReceive olayları hello .NET Framework | Microsoft Docs"
description: "Bu öğretici tooreceive olayları hello .NET Framework kullanılarak Azure Event Hubs'tan gelen izleyin."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="950b7-103">Merhaba .NET Framework kullanılarak Azure Event Hubs'tan gelen olayları alma</span><span class="sxs-lookup"><span data-stu-id="950b7-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="950b7-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="950b7-104">Introduction</span></span>

<span data-ttu-id="950b7-105">Event Hubs bağlı cihaz ve uygulamalardan büyük miktarlarda olay verileri (telemetri) işleyen bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="950b7-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="950b7-106">Verileri Event Hubs'a topladıktan sonra bir depolama kümesi kullanarak hello veri depolamak veya gerçek zamanlı analiz sağlayıcısı kullanarak dönüştürme.</span><span class="sxs-lookup"><span data-stu-id="950b7-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="950b7-107">Bu büyük ölçekli olay toplama ve işleme özelliği hello nesnelerin interneti (IOT) dahil modern uygulama mimarilerinin temel bir bileşenidir.</span><span class="sxs-lookup"><span data-stu-id="950b7-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="950b7-108">Bu öğretici nasıl toowrite bir .NET Framework konsol hello kullanarak bir event hub iletileri alan uygulaması gösterir  **[olay işleyicisi konağı][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="950b7-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="950b7-109">Merhaba, .NET Framework kullanarak toosend olaylara bakın hello [tooAzure olay hub'ın hello .NET Framework kullanarak olayları göndermek](event-hubs-dotnet-framework-getstarted-send.md) makale ya da uygun gönderen dili hello sol İçindekiler hello tıklatın.</span><span class="sxs-lookup"><span data-stu-id="950b7-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="950b7-110">Merhaba [olay işleyicisi konağı] [ EventProcessorHost] kalıcı denetim noktalarını yöneterek event hubs'a ait alma olaylarını basitleştiren bir .NET sınıfıdır ve paralel bu event hubs'a ait alır.</span><span class="sxs-lookup"><span data-stu-id="950b7-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="950b7-111">Hello kullanarak [olay işleyicisi konağı][Event Processor Host], farklı düğümlerde barındırıldığında bile birden çok alıcı arasında olayları bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950b7-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="950b7-112">Bu örnekte gösterilir nasıl toouse hello [olay işleyicisi konağı] [ EventProcessorHost] tek alıcı için.</span><span class="sxs-lookup"><span data-stu-id="950b7-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="950b7-113">Merhaba [olay işleme genişletme] [ Scale out Event Processing with Event Hubs] örnek gösterir nasıl toouse hello [olay işleyicisi konağı] [ EventProcessorHost] birden çok alıcısı bulunan.</span><span class="sxs-lookup"><span data-stu-id="950b7-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="950b7-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="950b7-114">Prerequisites</span></span>

<span data-ttu-id="950b7-115">toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="950b7-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="950b7-116">[Microsoft Visual Studio 2015 veya üzeri](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="950b7-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="950b7-117">Bu öğreticide Hello ekran görüntüleri, Visual Studio 2017 kullanın.</span><span class="sxs-lookup"><span data-stu-id="950b7-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="950b7-118">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="950b7-118">An active Azure account.</span></span> <span data-ttu-id="950b7-119">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir hesap oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="950b7-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="950b7-120">Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="950b7-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="950b7-121">Event Hubs ad alanı ve bir olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="950b7-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="950b7-122">Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate ad alanı bir olay hub'ları yazın ve hello uygulamanız gereken toocommunicate hello olay hub'ı ile yönetim kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="950b7-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="950b7-123">toocreate bir ad alanı ve olay hub'ı izleyin hello yordamda [bu makalede](event-hubs-create.md), sonra Bu öğreticide adımları izleyerek hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="950b7-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="950b7-124">Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="950b7-124">Create an Azure Storage account</span></span>

<span data-ttu-id="950b7-125">toouse hello [olay işleyicisi konağı][EventProcessorHost], bilmeniz gereken bir [Azure depolama hesabı][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="950b7-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="950b7-126">Toohello üzerinde oturum [Azure portal][Azure portal], tıklatıp **yeni** hello adresindeki hello ekranın sol üst.</span><span class="sxs-lookup"><span data-stu-id="950b7-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="950b7-127">**Depolama** ve ardından **Depolama hesabı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="950b7-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="950b7-128">Merhaba, **depolama hesabı oluşturma** dikey penceresinde hello depolama hesabı için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="950b7-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="950b7-129">Bir Azure aboneliği, kaynak grubunu ve konumu hangi toocreate hello kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="950b7-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="950b7-130">Sonra **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="950b7-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="950b7-131">Depolama hesapları Hello listesinde yeni oluşturulan depolama hesabı hello tıklayın.</span><span class="sxs-lookup"><span data-stu-id="950b7-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="950b7-132">Merhaba depolama hesabı dikey penceresinde tıklayın **erişim anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="950b7-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="950b7-133">Merhaba değerini kopyalayın **key1** toouse Bu öğreticide daha sonra.</span><span class="sxs-lookup"><span data-stu-id="950b7-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="950b7-134">Alıcı konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="950b7-134">Create a receiver console application</span></span>

1. <span data-ttu-id="950b7-135">Visual Studio'da hello kullanarak yeni bir Visual C# masaüstü uygulaması projesi oluşturma **konsol uygulaması** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="950b7-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="950b7-136">Ad hello proje **alıcı**.</span><span class="sxs-lookup"><span data-stu-id="950b7-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="950b7-137">Çözüm Gezgini'nde hello sağ **alıcı** proje ve ardından **çözüm için NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="950b7-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="950b7-138">Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="950b7-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="950b7-139">Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="950b7-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="950b7-140">Visual Studio indirir, yükler ve başvuru toohello ekler [Azure Service Bus Event Hub - EventProcessorHost NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), tüm bağımlılıklarıyla birlikte.</span><span class="sxs-lookup"><span data-stu-id="950b7-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="950b7-141">Sağ hello **alıcı** proje, tıklatın **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="950b7-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="950b7-142">Ad hello yeni sınıf **SimpleEventProcessor**ve ardından **Ekle** toocreate hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="950b7-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="950b7-143">Merhaba SimpleEventProcessor.cs dosyasının hello üst deyimlerini aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="950b7-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="950b7-144">Ardından, kod hello sınıfı hello gövdesi için aşağıdaki hello değiştirin:</span><span class="sxs-lookup"><span data-stu-id="950b7-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  <span data-ttu-id="950b7-145">Bu sınıf tarafından hello adlı **EventProcessorHost** hello olay hub'ından alınan tooprocess olaylar.</span><span class="sxs-lookup"><span data-stu-id="950b7-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="950b7-146">Merhaba `SimpleEventProcessor` sınıfını kullanan bir kronometre tooperiodically çağrısı hello denetim noktası yöntemini hello üzerinde **EventProcessorHost** bağlamı.</span><span class="sxs-lookup"><span data-stu-id="950b7-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="950b7-147">Bu işleme hello alıcı yeniden başlatılırsa, iş işleme en fazla beş dakika kaybederse, sağlar.</span><span class="sxs-lookup"><span data-stu-id="950b7-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="950b7-148">Merhaba, **Program** sınıfı, hello aşağıdakileri ekleyin `using` deyimi hello dosyanın üst kısmındaki hello:</span><span class="sxs-lookup"><span data-stu-id="950b7-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="950b7-149">Hello yerine `Main` hello yönteminde `Program` sınıf koddan hello ile hello olay hub'ı adı ve hello ad alanı düzeyinde bağlantı değiştirerek, daha önce kaydettiğiniz dize ve hello depolama hesabı ve hello kopyaladığınız anahtar Önceki bölümlerde.</span><span class="sxs-lookup"><span data-stu-id="950b7-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. <span data-ttu-id="950b7-150">Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="950b7-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="950b7-151">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="950b7-151">Congratulations!</span></span> <span data-ttu-id="950b7-152">Bir event hub'hello olay işleyicisi konağı kullanarak iletileri şimdi aldınız.</span><span class="sxs-lookup"><span data-stu-id="950b7-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="950b7-153">Bu öğretici, [EventProcessorHost][EventProcessorHost]'un tek bir örneğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="950b7-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="950b7-154">tooincrease verimlilik, birden çok örneğini çalıştırmanız önerilir [EventProcessorHost][EventProcessorHost]hello [ölçeklendirilmiş olay işleme out] gösterildiği gibi [ölçeklendirilmiş olay işleme out] örnek.</span><span class="sxs-lookup"><span data-stu-id="950b7-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="950b7-155">Bu gibi durumlarda hello çeşitli örnekler otomatik olarak birbirleriyle tooload Bakiye alınan hello olayları koordine.</span><span class="sxs-lookup"><span data-stu-id="950b7-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="950b7-156">Birden çok alıcıya tooeach işlem istiyorsanız *tüm* hello olayları hello kullanmalısınız **ConsumerGroup** kavram.</span><span class="sxs-lookup"><span data-stu-id="950b7-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="950b7-157">Olaylar farklı makinelerden alındığında için yararlı toospecify adları olabilir [EventProcessorHost] [ EventProcessorHost] çıkarak hello makineleri (veya rolleri) hangi dağıtıldıkları.</span><span class="sxs-lookup"><span data-stu-id="950b7-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="950b7-158">Bu konular hakkında daha fazla bilgi için bkz: Merhaba [Event Hubs'a genel bakış] [ Event Hubs overview] ve hello [Event Hubs Programlama Kılavuzu] [ Event Hubs Programming Guide] Konular.</span><span class="sxs-lookup"><span data-stu-id="950b7-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="950b7-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="950b7-159">Next steps</span></span>

<span data-ttu-id="950b7-160">Bir olay hub'ı oluşturan ve verileri alan çalışan bir uygulama oluşturduğunuza göre bağlantılar aşağıdaki hello ziyaret tarafından daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="950b7-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="950b7-161">[Olay İşlemcisi Konağı][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="950b7-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="950b7-162">[Event Hubs'a genel bakış][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="950b7-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="950b7-163">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="950b7-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
