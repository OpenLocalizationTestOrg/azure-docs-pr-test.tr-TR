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
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="a9ac5-103">Merhaba olay işleyicisi konağı iletilerle .NET standart alma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a9ac5-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="a9ac5-104">Bu örnek edinilebilir [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="a9ac5-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="a9ac5-105">Bu öğretici nasıl toowrite .NET Core konsol kullanarak bir event hub'ından iletileri alan uygulaması gösterir **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="a9ac5-106">Merhaba çalıştırabilirsiniz [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) çözümü olarak-hello dizeler, olay hub'ı ve depolama hesabı değerleri ile yerini alacak olan.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="a9ac5-107">Ya da izleyebilirsiniz hello adımları Bu öğretici toocreate kendi.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9ac5-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a9ac5-108">Prerequisites</span></span>

* <span data-ttu-id="a9ac5-109">[Microsoft Visual Studio 2015 veya 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a9ac5-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="a9ac5-110">Bu öğretici kullanımı Visual Studio 2017 Hello örneklerde, ancak Visual Studio 2015'de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="a9ac5-111">[.NET core Visual Studio 2015 veya 2017 Araçları](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="a9ac5-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="a9ac5-112">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-112">An Azure subscription.</span></span>
* <span data-ttu-id="a9ac5-113">Bir Azure Event Hubs ad alanı.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="a9ac5-114">Bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="a9ac5-115">Event Hubs ad alanı ve bir olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9ac5-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="a9ac5-116">Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate hello olay hub'ları için bir ad yazın ve hello uygulamanızı hello olay hub'ı ile toocommunicate gerektiğini yönetim kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="a9ac5-117">toocreate bir ad alanı ve olay hub'ı izleyin hello yordamda [bu makalede](event-hubs-create.md)ve ardından aşağıdaki adımları hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="a9ac5-118">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9ac5-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="a9ac5-119">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a9ac5-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="a9ac5-120">Merhaba sol gezinti bölmesinde hello portalı tıklatın **yeni**, tıklatın **depolama**ve ardından **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="a9ac5-121">Hello depolama hesabı dikey penceresinde hello alanları tamamlayın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Depolama hesabı oluşturma][1]

4. <span data-ttu-id="a9ac5-123">Merhaba gördükten sonra **dağıtımları başarılı** iletisi, hello yeni depolama hesabı hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="a9ac5-124">Merhaba, **Essentials** dikey penceresinde tıklatın **BLOB'lar**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="a9ac5-125">Ne zaman hello **Blob hizmeti** dikey penceresi açıldığında, tıklatın **+ kapsayıcı** hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="a9ac5-126">Merhaba kapsayıcı bir ad verin ve ardından hello kapatın **Blob hizmeti** dikey.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="a9ac5-127">Tıklatın **erişim anahtarları** hello Sol dikey ve kopyalama hello adı hello depolama kapsayıcısı, hello depolama hesabı ve hello değerini **key1**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="a9ac5-128">Bu değerleri tooNotepad veya başka bir geçici konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="a9ac5-129">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9ac5-129">Create a console application</span></span>

<span data-ttu-id="a9ac5-130">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-130">Start Visual Studio.</span></span> <span data-ttu-id="a9ac5-131">Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="a9ac5-132">.NET Core konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-132">Create a .NET Core console application.</span></span>

![Yeni Proje][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="a9ac5-134">Merhaba olay hub'ları NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="a9ac5-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="a9ac5-135">Merhaba eklemek [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) ve [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) aşağıdaki adımları izleyerek .NET standart kitaplığı NuGet paketleri tooyour proje:</span><span class="sxs-lookup"><span data-stu-id="a9ac5-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="a9ac5-136">Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a9ac5-137">Merhaba tıklatın **Gözat** sekmesini ve ardından "Microsoft.Azure.EventHubs" ve select hello arama **Microsoft.Azure.EventHubs** paket.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="a9ac5-138">Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="a9ac5-139">1 ve 2. adımları yineleyin ve hello yükleme **Microsoft.Azure.EventHubs.Processor** paket.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="a9ac5-140">Merhaba Ieventprocessor arabirimini uygulama</span><span class="sxs-lookup"><span data-stu-id="a9ac5-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="a9ac5-141">Çözüm Gezgini'nde, sağ hello proje tıklatın **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="a9ac5-142">Ad hello yeni sınıf **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="a9ac5-143">Merhaba SimpleEventProcessor.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimleri toohello dosyasının üst kısmında hello.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="a9ac5-144">Uygulama hello `IEventProcessor` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="a9ac5-145">Merhaba Hello tüm içeriğini değiştirin `SimpleEventProcessor` koddan hello sınıfıyla:</span><span class="sxs-lookup"><span data-stu-id="a9ac5-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="a9ac5-146">Merhaba SimpleEventProcessor sınıfı tooreceive iletileri kullanan bir ana Konsolu yöntemi yazma</span><span class="sxs-lookup"><span data-stu-id="a9ac5-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="a9ac5-147">Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimleri toohello üst.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="a9ac5-148">Ekleme sabitlerin toohello `Program` hello olay hub bağlantı dizesine, olay hub'ı adı, depolama hesabı kapsayıcı adı, depolama hesabı adı ve depolama hesabı anahtarı için sınıf.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="a9ac5-149">Aşağıdaki kod, bunlara karşılık gelen değerler ile Merhaba yer tutucuları değiştirme hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="a9ac5-150">Adlı yeni bir yöntem ekleyin `MainAsync` toohello `Program` sınıfı, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="a9ac5-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

3. <span data-ttu-id="a9ac5-151">Kod toohello satırının aşağıdaki hello eklemek `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a9ac5-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="a9ac5-152">Program.cs dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="a9ac5-152">Here is what your Program.cs file should look like:</span></span>

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

4. <span data-ttu-id="a9ac5-153">Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="a9ac5-154">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a9ac5-154">Congratulations!</span></span> <span data-ttu-id="a9ac5-155">Şimdi, iletileri hello olay işleyicisi konağı kullanarak bir event hub'ından aldınız.</span><span class="sxs-lookup"><span data-stu-id="a9ac5-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9ac5-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9ac5-156">Next steps</span></span>
<span data-ttu-id="a9ac5-157">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a9ac5-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="a9ac5-158">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="a9ac5-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="a9ac5-159">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9ac5-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a9ac5-160">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="a9ac5-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
