---
title: ".NET standart kullanarak Azure Event Hubs'tan gelen olayları alma | Microsoft Docs"
description: "EventProcessorHost bulunan iletiler alma standart .NET içinde kullanmaya başlama"
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="44d4d-103">Olay işleyicisi konağı iletilerle .NET standart alma kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="44d4d-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="44d4d-104">Bu örnek edinilebilir [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="44d4d-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="44d4d-105">Bu öğretici kullanarak bir event hub'ından iletileri alan bir .NET Core konsol uygulamasının nasıl yazılacağını gösterir **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="44d4d-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="44d4d-106">Çalıştırabilirsiniz [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) çözümü olarak-olduğundan, olay hub'ı ve depolama hesabı değerleriniz ile dizeleri değiştirme.</span><span class="sxs-lookup"><span data-stu-id="44d4d-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="44d4d-107">Veya, kendi oluşturmak için Bu öğreticide adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44d4d-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44d4d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="44d4d-108">Prerequisites</span></span>

* <span data-ttu-id="44d4d-109">[Microsoft Visual Studio 2015 veya 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="44d4d-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="44d4d-110">Bu öğretici kullanım Visual Studio 2017 ancak Visual Studio 2015 örneklerde de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="44d4d-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="44d4d-111">[.NET core Visual Studio 2015 veya 2017 Araçları](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="44d4d-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="44d4d-112">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="44d4d-112">An Azure subscription.</span></span>
* <span data-ttu-id="44d4d-113">Bir Azure Event Hubs ad alanı.</span><span class="sxs-lookup"><span data-stu-id="44d4d-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="44d4d-114">Bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="44d4d-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="44d4d-115">Event Hubs ad alanı ve bir olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="44d4d-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="44d4d-116">İlk adım kullanmaktır [Azure portal](https://portal.azure.com) olay hub'ları türü için bir ad alanı oluşturmak ve event hub ile iletişim kurması için uygulamanız gereken yönetim kimlik bilgilerini elde etmek için.</span><span class="sxs-lookup"><span data-stu-id="44d4d-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="44d4d-117">Bir ad alanı ve olay hub'ı oluşturmak için yordamı izleyin [bu makalede](event-hubs-create.md)ve ardından aşağıdaki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="44d4d-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="44d4d-118">Azure Storage hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="44d4d-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="44d4d-119">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="44d4d-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="44d4d-120">Portalın sol gezinti bölmesinde tıklatın **yeni**, tıklatın **depolama**ve ardından **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="44d4d-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="44d4d-121">Depolama hesabı dikey penceresindeki alanları doldurun ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="44d4d-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Depolama hesabı oluşturma][1]

4. <span data-ttu-id="44d4d-123">Gördükten sonra **dağıtımları başarılı** ileti, yeni depolama hesabı adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="44d4d-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="44d4d-124">İçinde **Essentials** dikey penceresinde tıklatın **BLOB'lar**.</span><span class="sxs-lookup"><span data-stu-id="44d4d-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="44d4d-125">Zaman **Blob hizmeti** dikey penceresi açıldığında, tıklatın **+ kapsayıcı** üstünde.</span><span class="sxs-lookup"><span data-stu-id="44d4d-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="44d4d-126">Kapsayıcı bir ad verin ve ardından kapatın **Blob hizmeti** dikey.</span><span class="sxs-lookup"><span data-stu-id="44d4d-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="44d4d-127">Tıklatın **erişim anahtarları** Sol dikey kopyalayıp adını depolama kapsayıcısı, depolama hesabı ve değerini **key1**.</span><span class="sxs-lookup"><span data-stu-id="44d4d-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="44d4d-128">Bu değerleri Not Defteri'nde veya başka bir geçici konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="44d4d-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="44d4d-129">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="44d4d-129">Create a console application</span></span>

<span data-ttu-id="44d4d-130">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="44d4d-130">Start Visual Studio.</span></span> <span data-ttu-id="44d4d-131">**Dosya** menüsünde **Yeni**'ye ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44d4d-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="44d4d-132">.NET Core konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44d4d-132">Create a .NET Core console application.</span></span>

![Yeni Proje][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="44d4d-134">Olay hub'ları NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="44d4d-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="44d4d-135">Ekleme [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) ve [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET standart kitaplığı NuGet paketlerini projenize aşağıdaki adımları izleyerek:</span><span class="sxs-lookup"><span data-stu-id="44d4d-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="44d4d-136">Yeni oluşturulan projeye sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="44d4d-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="44d4d-137">Tıklatın **Gözat** sekmesini ve ardından "Microsoft.Azure.EventHubs" ve select arama **Microsoft.Azure.EventHubs** paket.</span><span class="sxs-lookup"><span data-stu-id="44d4d-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="44d4d-138">Yüklemeyi tamamlamak için **Yükle**'ye tıklayın, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="44d4d-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="44d4d-139">1 ve 2. adımları yineleyin ve yükleme **Microsoft.Azure.EventHubs.Processor** paket.</span><span class="sxs-lookup"><span data-stu-id="44d4d-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="44d4d-140">Ieventprocessor arabirimini uygulama</span><span class="sxs-lookup"><span data-stu-id="44d4d-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="44d4d-141">Çözüm Gezgini'nde projeye sağ tıklayın, **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="44d4d-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="44d4d-142">Yeni sınıf **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="44d4d-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="44d4d-143">SimpleEventProcessor.cs dosyasını açın ve aşağıdakileri ekleyin `using` deyimlerini dosyanın en üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44d4d-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="44d4d-144">Uygulama `IEventProcessor` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="44d4d-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="44d4d-145">Tüm içeriğini değiştirin `SimpleEventProcessor` aşağıdaki kodla sınıfı:</span><span class="sxs-lookup"><span data-stu-id="44d4d-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="44d4d-146">SimpleEventProcessor sınıfı iletileri almak için kullandığı bir ana Konsolu yöntemi yazma</span><span class="sxs-lookup"><span data-stu-id="44d4d-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="44d4d-147">Aşağıdaki `using` deyimlerini Program.cs dosyasının üst kısmına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44d4d-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="44d4d-148">Sabitlere eklemek `Program` olay hub bağlantı dizesine, olay hub'ı adı, depolama hesabı kapsayıcı adı, depolama hesabı adı ve depolama hesabı anahtarı için sınıf.</span><span class="sxs-lookup"><span data-stu-id="44d4d-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="44d4d-149">Yer tutucuları bunlara karşılık gelen değerler ile değiştirerek aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="44d4d-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="44d4d-150">Adlı yeni bir yöntem ekleyin `MainAsync` için `Program` sınıfı, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="44d4d-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="44d4d-151">Aşağıdaki kod satırını ekleyin `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="44d4d-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="44d4d-152">Program.cs dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="44d4d-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="44d4d-153">Programı çalıştırın ve herhangi bir hata olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="44d4d-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="44d4d-154">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="44d4d-154">Congratulations!</span></span> <span data-ttu-id="44d4d-155">İletilerin bir event hub'ından olay işleyicisi konağı kullanarak şimdi aldınız.</span><span class="sxs-lookup"><span data-stu-id="44d4d-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44d4d-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44d4d-156">Next steps</span></span>
<span data-ttu-id="44d4d-157">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="44d4d-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="44d4d-158">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="44d4d-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="44d4d-159">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="44d4d-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="44d4d-160">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="44d4d-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
