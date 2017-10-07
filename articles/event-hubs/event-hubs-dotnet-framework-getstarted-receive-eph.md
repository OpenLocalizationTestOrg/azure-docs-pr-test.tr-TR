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
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Merhaba .NET Framework kullanılarak Azure Event Hubs'tan gelen olayları alma

## <a name="introduction"></a>Giriş

Event Hubs bağlı cihaz ve uygulamalardan büyük miktarlarda olay verileri (telemetri) işleyen bir hizmettir. Verileri Event Hubs'a topladıktan sonra bir depolama kümesi kullanarak hello veri depolamak veya gerçek zamanlı analiz sağlayıcısı kullanarak dönüştürme. Bu büyük ölçekli olay toplama ve işleme özelliği hello nesnelerin interneti (IOT) dahil modern uygulama mimarilerinin temel bir bileşenidir.

Bu öğretici nasıl toowrite bir .NET Framework konsol hello kullanarak bir event hub iletileri alan uygulaması gösterir  **[olay işleyicisi konağı][EventProcessorHost]**. Merhaba, .NET Framework kullanarak toosend olaylara bakın hello [tooAzure olay hub'ın hello .NET Framework kullanarak olayları göndermek](event-hubs-dotnet-framework-getstarted-send.md) makale ya da uygun gönderen dili hello sol İçindekiler hello tıklatın.

Merhaba [olay işleyicisi konağı] [ EventProcessorHost] kalıcı denetim noktalarını yöneterek event hubs'a ait alma olaylarını basitleştiren bir .NET sınıfıdır ve paralel bu event hubs'a ait alır. Hello kullanarak [olay işleyicisi konağı][Event Processor Host], farklı düğümlerde barındırıldığında bile birden çok alıcı arasında olayları bölebilirsiniz. Bu örnekte gösterilir nasıl toouse hello [olay işleyicisi konağı] [ EventProcessorHost] tek alıcı için. Merhaba [olay işleme genişletme] [ Scale out Event Processing with Event Hubs] örnek gösterir nasıl toouse hello [olay işleyicisi konağı] [ EventProcessorHost] birden çok alıcısı bulunan.

## <a name="prerequisites"></a>Ön koşullar

toocomplete Bu öğretici önkoşulları aşağıdaki hello gerekir:

* [Microsoft Visual Studio 2015 veya üzeri](http://visualstudio.com). Bu öğreticide Hello ekran görüntüleri, Visual Studio 2017 kullanın.
* Etkin bir Azure hesabı. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir hesap oluşturabilirsiniz. Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs ad alanı ve bir olay hub’ı oluşturma

Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate ad alanı bir olay hub'ları yazın ve hello uygulamanız gereken toocommunicate hello olay hub'ı ile yönetim kimlik bilgilerini alın. toocreate bir ad alanı ve olay hub'ı izleyin hello yordamda [bu makalede](event-hubs-create.md), sonra Bu öğreticide adımları izleyerek hello ile devam edin.

## <a name="create-an-azure-storage-account"></a>Azure Depolama hesabı oluşturma

toouse hello [olay işleyicisi konağı][EventProcessorHost], bilmeniz gereken bir [Azure depolama hesabı][Azure Storage account]:

1. Toohello üzerinde oturum [Azure portal][Azure portal], tıklatıp **yeni** hello adresindeki hello ekranın sol üst.
2. **Depolama** ve ardından **Depolama hesabı**’na tıklayın.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. Merhaba, **depolama hesabı oluşturma** dikey penceresinde hello depolama hesabı için bir ad yazın. Bir Azure aboneliği, kaynak grubunu ve konumu hangi toocreate hello kaynak seçin. Sonra **Oluştur**’a tıklayın.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. Depolama hesapları Hello listesinde yeni oluşturulan depolama hesabı hello tıklayın.
5. Merhaba depolama hesabı dikey penceresinde tıklayın **erişim anahtarları**. Merhaba değerini kopyalayın **key1** toouse Bu öğreticide daha sonra.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Alıcı konsol uygulaması oluşturma

1. Visual Studio'da hello kullanarak yeni bir Visual C# masaüstü uygulaması projesi oluşturma **konsol uygulaması** proje şablonu. Ad hello proje **alıcı**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. Çözüm Gezgini'nde hello sağ **alıcı** proje ve ardından **çözüm için NuGet paketlerini Yönet**.
3. Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Visual Studio indirir, yükler ve başvuru toohello ekler [Azure Service Bus Event Hub - EventProcessorHost NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), tüm bağımlılıklarıyla birlikte.
4. Sağ hello **alıcı** proje, tıklatın **Ekle**ve ardından **sınıfı**. Ad hello yeni sınıf **SimpleEventProcessor**ve ardından **Ekle** toocreate hello sınıfı.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Merhaba SimpleEventProcessor.cs dosyasının hello üst deyimlerini aşağıdaki hello ekleyin:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  Ardından, kod hello sınıfı hello gövdesi için aşağıdaki hello değiştirin:
    
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
    
  Bu sınıf tarafından hello adlı **EventProcessorHost** hello olay hub'ından alınan tooprocess olaylar. Merhaba `SimpleEventProcessor` sınıfını kullanan bir kronometre tooperiodically çağrısı hello denetim noktası yöntemini hello üzerinde **EventProcessorHost** bağlamı. Bu işleme hello alıcı yeniden başlatılırsa, iş işleme en fazla beş dakika kaybederse, sağlar.
6. Merhaba, **Program** sınıfı, hello aşağıdakileri ekleyin `using` deyimi hello dosyanın üst kısmındaki hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Hello yerine `Main` hello yönteminde `Program` sınıf koddan hello ile hello olay hub'ı adı ve hello ad alanı düzeyinde bağlantı değiştirerek, daha önce kaydettiğiniz dize ve hello depolama hesabı ve hello kopyaladığınız anahtar Önceki bölümlerde. 
    
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

7. Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.
  
Tebrikler! Bir event hub'hello olay işleyicisi konağı kullanarak iletileri şimdi aldınız.


> [!NOTE]
> Bu öğretici, [EventProcessorHost][EventProcessorHost]'un tek bir örneğini kullanır. tooincrease verimlilik, birden çok örneğini çalıştırmanız önerilir [EventProcessorHost][EventProcessorHost]hello [ölçeklendirilmiş olay işleme out] gösterildiği gibi [ölçeklendirilmiş olay işleme out] örnek. Bu gibi durumlarda hello çeşitli örnekler otomatik olarak birbirleriyle tooload Bakiye alınan hello olayları koordine. Birden çok alıcıya tooeach işlem istiyorsanız *tüm* hello olayları hello kullanmalısınız **ConsumerGroup** kavram. Olaylar farklı makinelerden alındığında için yararlı toospecify adları olabilir [EventProcessorHost] [ EventProcessorHost] çıkarak hello makineleri (veya rolleri) hangi dağıtıldıkları. Bu konular hakkında daha fazla bilgi için bkz: Merhaba [Event Hubs'a genel bakış] [ Event Hubs overview] ve hello [Event Hubs Programlama Kılavuzu] [ Event Hubs Programming Guide] Konular.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar

Bir olay hub'ı oluşturan ve verileri alan çalışan bir uygulama oluşturduğunuza göre bağlantılar aşağıdaki hello ziyaret tarafından daha fazla bilgi edinebilirsiniz:

* [Olay İşlemcisi Konağı][Event Processor Host]
* [Event Hubs'a genel bakış][Event Hubs overview]
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

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
