---
title: "Azure Event Hubs'a .NET standart kullanarak olayları göndermek | Microsoft Docs"
description: "Event Hubs .NET standart, olayları göndermek kullanmaya başlama"
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
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="3cfed-103">Azure Event Hubs .NET standart içinde ileti göndermek kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3cfed-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="3cfed-104">Bu örnek edinilebilir [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="3cfed-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="3cfed-105">Bu öğretici, bir dizi ileti olay hub'ına gönderir .NET Core konsol uygulamasının nasıl yazılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3cfed-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="3cfed-106">Çalıştırabilirsiniz [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) çözümü olarak-yerini alacak olan `EhConnectionString` ve `EhEntityPath` dizeleri, olay hub'ı değerlerle.</span><span class="sxs-lookup"><span data-stu-id="3cfed-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="3cfed-107">Veya, kendi oluşturmak için Bu öğreticide adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3cfed-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cfed-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3cfed-108">Prerequisites</span></span>

* <span data-ttu-id="3cfed-109">[Microsoft Visual Studio 2015 veya 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="3cfed-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="3cfed-110">Bu öğretici kullanım Visual Studio 2017 ancak Visual Studio 2015 örneklerde de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3cfed-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="3cfed-111">[.NET core Visual Studio 2015 veya 2017 Araçları](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="3cfed-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="3cfed-112">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="3cfed-112">An Azure subscription.</span></span>
* <span data-ttu-id="3cfed-113">Bir olay hub'ad alanı.</span><span class="sxs-lookup"><span data-stu-id="3cfed-113">An event hub namespace.</span></span>

<span data-ttu-id="3cfed-114">Olay hub'ına iletileri göndermek için Visual Studio bir C# konsol uygulaması yazmak için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="3cfed-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="3cfed-115">Event Hubs ad alanı ve bir olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cfed-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="3cfed-116">İlk adım kullanmaktır [Azure portal](https://portal.azure.com) olay hub'türü için bir ad alanı oluşturmak ve event hub ile iletişim kurması için uygulamanız gereken yönetim kimlik bilgilerini elde etmek için.</span><span class="sxs-lookup"><span data-stu-id="3cfed-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="3cfed-117">Bir ad ve bir olay hub'ı oluşturmak için yordamı izleyin [bu makalede](event-hubs-create.md)ve ardından aşağıdaki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="3cfed-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="3cfed-118">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cfed-118">Create a console application</span></span>

<span data-ttu-id="3cfed-119">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3cfed-119">Start Visual Studio.</span></span> <span data-ttu-id="3cfed-120">**Dosya** menüsünde **Yeni**'ye ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3cfed-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="3cfed-121">.NET Core konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3cfed-121">Create a .NET Core console application.</span></span>

![Yeni Proje][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="3cfed-123">Olay hub'ları NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="3cfed-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="3cfed-124">Ekleme [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) aşağıdaki adımları izleyerek projeniz .NET standart kitaplığı NuGet paketi:</span><span class="sxs-lookup"><span data-stu-id="3cfed-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="3cfed-125">Yeni oluşturulan projeye sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="3cfed-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="3cfed-126">Tıklatın **Gözat** sekmesini ve ardından "Microsoft.Azure.EventHubs" ve select arama **Microsoft.Azure.EventHubs** paket.</span><span class="sxs-lookup"><span data-stu-id="3cfed-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="3cfed-127">Yüklemeyi tamamlamak için **Yükle**'ye tıklayın, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="3cfed-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="3cfed-128">Olay hub'ına iletileri göndermek için bazı kod yazma</span><span class="sxs-lookup"><span data-stu-id="3cfed-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="3cfed-129">Aşağıdaki `using` deyimlerini Program.cs dosyasının üst kısmına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3cfed-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="3cfed-130">Sabitlere eklemek `Program` sınıfı Event Hubs bağlantı dizesini ve varlık yolu için (tek olay hub'ı adı).</span><span class="sxs-lookup"><span data-stu-id="3cfed-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="3cfed-131">Köşeli ayraçlar içindeki yer tutucuları olay hub'ı oluştururken edinilen uygun değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3cfed-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="3cfed-132">Adlı yeni bir yöntem ekleyin `MainAsync` için `Program` sınıfı, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="3cfed-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="3cfed-133">Adlı yeni bir yöntem ekleyin `SendMessagesToEventHub` için `Program` sınıfı, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="3cfed-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. <span data-ttu-id="3cfed-134">Aşağıdaki kodu ekleyin `Main` yönteminde `Program` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3cfed-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="3cfed-135">Program.cs dosyanız aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="3cfed-135">Here is what your Program.cs should look like.</span></span>

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. <span data-ttu-id="3cfed-136">Programı çalıştırın ve herhangi bir hata olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="3cfed-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="3cfed-137">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="3cfed-137">Congratulations!</span></span> <span data-ttu-id="3cfed-138">Bir olay hub'ına ileti gönderdiniz.</span><span class="sxs-lookup"><span data-stu-id="3cfed-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cfed-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3cfed-139">Next steps</span></span>
<span data-ttu-id="3cfed-140">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3cfed-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="3cfed-141">Olay hub'larından olayları alma</span><span class="sxs-lookup"><span data-stu-id="3cfed-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="3cfed-142">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="3cfed-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3cfed-143">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3cfed-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="3cfed-144">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="3cfed-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
