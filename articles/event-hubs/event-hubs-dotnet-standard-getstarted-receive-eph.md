---
title: "Azure Event Hubs .NET standart kullanarak aaaReceive olaylarından | Microsoft Docs"
description: "İleti hello EventProcessorHost ile .NET standart alma kullanmaya başlama"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Merhaba olay işleyicisi konağı iletilerle .NET standart alma kullanmaya başlama

> [!NOTE]
> Bu örnek edinilebilir [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

Bu öğretici nasıl toowrite .NET Core konsol kullanarak bir event hub'ından iletileri alan uygulaması gösterir **EventProcessorHost**. Merhaba çalıştırabilirsiniz [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) çözümü olarak-hello dizeler, olay hub'ı ve depolama hesabı değerleri ile yerini alacak olan. Ya da izleyebilirsiniz hello adımları Bu öğretici toocreate kendi.

## <a name="prerequisites"></a>Ön koşullar

* [Microsoft Visual Studio 2015 veya 2017](http://www.visualstudio.com). Bu öğretici kullanımı Visual Studio 2017 Hello örneklerde, ancak Visual Studio 2015'de desteklenir.
* [.NET core Visual Studio 2015 veya 2017 Araçları](http://www.microsoft.com/net/core).
* Azure aboneliği.
* Bir Azure Event Hubs ad alanı.
* Bir Azure depolama hesabı.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs ad alanı ve bir olay hub’ı oluşturma  

Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate hello olay hub'ları için bir ad yazın ve hello uygulamanızı hello olay hub'ı ile toocommunicate gerektiğini yönetim kimlik bilgilerini alın. toocreate bir ad alanı ve olay hub'ı izleyin hello yordamda [bu makalede](event-hubs-create.md)ve ardından aşağıdaki adımları hello ile devam edin.  

## <a name="create-an-azure-storage-account"></a>Azure Storage hesabı oluşturma  

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).  
2. Merhaba sol gezinti bölmesinde hello portalı tıklatın **yeni**, tıklatın **depolama**ve ardından **depolama hesabı**.  
3. Hello depolama hesabı dikey penceresinde hello alanları tamamlayın ve ardından **oluşturma**.

    ![Depolama hesabı oluşturma][1]

4. Merhaba gördükten sonra **dağıtımları başarılı** iletisi, hello yeni depolama hesabı hello adına tıklayın. Merhaba, **Essentials** dikey penceresinde tıklatın **BLOB'lar**. Ne zaman hello **Blob hizmeti** dikey penceresi açıldığında, tıklatın **+ kapsayıcı** hello üstünde. Merhaba kapsayıcı bir ad verin ve ardından hello kapatın **Blob hizmeti** dikey.  
5. Tıklatın **erişim anahtarları** hello Sol dikey ve kopyalama hello adı hello depolama kapsayıcısı, hello depolama hesabı ve hello değerini **key1**. Bu değerleri tooNotepad veya başka bir geçici konuma kaydedin.  

## <a name="create-a-console-application"></a>Konsol uygulaması oluşturma

Visual Studio’yu çalıştırın. Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**. .NET Core konsol uygulaması oluşturun.

![Yeni Proje][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Merhaba olay hub'ları NuGet paketi ekleme

Merhaba eklemek [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) ve [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) aşağıdaki adımları izleyerek .NET standart kitaplığı NuGet paketleri tooyour proje: 

1. Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.
2. Merhaba tıklatın **Gözat** sekmesini ve ardından "Microsoft.Azure.EventHubs" ve select hello arama **Microsoft.Azure.EventHubs** paket. Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.
3. 1 ve 2. adımları yineleyin ve hello yükleme **Microsoft.Azure.EventHubs.Processor** paket.

## <a name="implement-hello-ieventprocessor-interface"></a>Merhaba Ieventprocessor arabirimini uygulama

1. Çözüm Gezgini'nde, sağ hello proje tıklatın **Ekle**ve ardından **sınıfı**. Ad hello yeni sınıf **SimpleEventProcessor**.

2. Merhaba SimpleEventProcessor.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimleri toohello dosyasının üst kısmında hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Uygulama hello `IEventProcessor` arabirimi. Merhaba Hello tüm içeriğini değiştirin `SimpleEventProcessor` koddan hello sınıfıyla:

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Merhaba SimpleEventProcessor sınıfı tooreceive iletileri kullanan bir ana Konsolu yöntemi yazma

1. Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimleri toohello üst.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Ekleme sabitlerin toohello `Program` hello olay hub bağlantı dizesine, olay hub'ı adı, depolama hesabı kapsayıcı adı, depolama hesabı adı ve depolama hesabı anahtarı için sınıf. Aşağıdaki kod, bunlara karşılık gelen değerler ile Merhaba yer tutucuları değiştirme hello ekleyin.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Adlı yeni bir yöntem ekleyin `MainAsync` toohello `Program` sınıfı, şu şekilde:

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. Kod toohello satırının aşağıdaki hello eklemek `Main` yöntemi:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    Program.cs dosyanız aşağıdaki gibi görünmelidir:

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.

Tebrikler! Şimdi, iletileri hello olay işleyicisi konağı kullanarak bir event hub'ından aldınız.

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
