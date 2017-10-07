---
title: "aaaSend olayları tooAzure olay hub'ın .NET standart kullanarak | Microsoft Docs"
description: "Olayları tooEvent hub .NET standart gönderme kullanmaya başlama"
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
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="c3fa3-103">İleti tooAzure Event Hubs .NET standart gönderme kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c3fa3-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="c3fa3-104">Bu örnek edinilebilir [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="c3fa3-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="c3fa3-105">Bu öğretici, bir dizi gönderir bir .NET Core konsol uygulaması toowrite tooan olay hub'ı nasıl iletileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="c3fa3-106">Merhaba çalıştırabilirsiniz [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) çözümü olarak-hello yerini alacak olan `EhConnectionString` ve `EhEntityPath` dizeleri, olay hub'ı değerlerle.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="c3fa3-107">Ya da izleyebilirsiniz hello adımları Bu öğretici toocreate kendi.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3fa3-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c3fa3-108">Prerequisites</span></span>

* <span data-ttu-id="c3fa3-109">[Microsoft Visual Studio 2015 veya 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="c3fa3-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="c3fa3-110">Bu öğretici kullanımı Visual Studio 2017 Hello örneklerde, ancak Visual Studio 2015'de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="c3fa3-111">[.NET core Visual Studio 2015 veya 2017 Araçları](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="c3fa3-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="c3fa3-112">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-112">An Azure subscription.</span></span>
* <span data-ttu-id="c3fa3-113">Bir olay hub'ad alanı.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-113">An event hub namespace.</span></span>

<span data-ttu-id="c3fa3-114">Visual Studio toowrite C# konsol uygulaması toosend iletileri tooan olay hub'ı kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="c3fa3-115">Event Hubs ad alanı ve bir olay hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3fa3-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="c3fa3-116">Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate hello olay hub'türü için bir ad alanı ve hello uygulamanızı hello olay hub'ı ile toocommunicate gerektiğini yönetim kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="c3fa3-117">toocreate bir ad ve bir event hub hello yordamı izleyin [bu makalede](event-hubs-create.md)ve ardından aşağıdaki adımları hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="c3fa3-118">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3fa3-118">Create a console application</span></span>

<span data-ttu-id="c3fa3-119">Visual Studio’yu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-119">Start Visual Studio.</span></span> <span data-ttu-id="c3fa3-120">Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="c3fa3-121">.NET Core konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-121">Create a .NET Core console application.</span></span>

![Yeni Proje][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="c3fa3-123">Merhaba olay hub'ları NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="c3fa3-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="c3fa3-124">Merhaba eklemek [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) aşağıdaki adımları izleyerek .NET standart kitaplığı NuGet paketi tooyour proje:</span><span class="sxs-lookup"><span data-stu-id="c3fa3-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="c3fa3-125">Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c3fa3-126">Merhaba tıklatın **Gözat** sekmesini ve ardından "Microsoft.Azure.EventHubs" ve select hello arama **Microsoft.Azure.EventHubs** paket.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="c3fa3-127">Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="c3fa3-128">Bazı kod toosend iletileri toohello olay hub'ı yazma</span><span class="sxs-lookup"><span data-stu-id="c3fa3-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="c3fa3-129">Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimleri toohello üst.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="c3fa3-130">Ekleme sabitlerin toohello `Program` hello olay hub'ları bağlantı dizesi ve varlık yolu (tek olay hub'ı adı) için sınıf.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="c3fa3-131">Köşeli ayraçlar Hello yer tutucuları hello olay hub'ı oluştururken edinilen hello uygun değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="c3fa3-132">Adlı yeni bir yöntem ekleyin `MainAsync` toohello `Program` sınıfı, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="c3fa3-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="c3fa3-133">Adlı yeni bir yöntem ekleyin `SendMessagesToEventHub` toohello `Program` sınıfı, şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="c3fa3-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
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

5. <span data-ttu-id="c3fa3-134">Aşağıdaki kodu toohello hello eklemek `Main` hello yönteminde `Program` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="c3fa3-135">Program.cs dosyanız aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
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

6. <span data-ttu-id="c3fa3-136">Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="c3fa3-137">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="c3fa3-137">Congratulations!</span></span> <span data-ttu-id="c3fa3-138">İletileri tooan olay hub'ı şimdi gönderdiniz.</span><span class="sxs-lookup"><span data-stu-id="c3fa3-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3fa3-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3fa3-139">Next steps</span></span>
<span data-ttu-id="c3fa3-140">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3fa3-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="c3fa3-141">Olay hub'larından olayları alma</span><span class="sxs-lookup"><span data-stu-id="c3fa3-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="c3fa3-142">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="c3fa3-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="c3fa3-143">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3fa3-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="c3fa3-144">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="c3fa3-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
