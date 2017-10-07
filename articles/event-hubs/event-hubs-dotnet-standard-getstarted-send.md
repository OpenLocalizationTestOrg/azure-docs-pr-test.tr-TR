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
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>İleti tooAzure Event Hubs .NET standart gönderme kullanmaya başlama

> [!NOTE]
> Bu örnek edinilebilir [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

Bu öğretici, bir dizi gönderir bir .NET Core konsol uygulaması toowrite tooan olay hub'ı nasıl iletileri gösterir. Merhaba çalıştırabilirsiniz [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) çözümü olarak-hello yerini alacak olan `EhConnectionString` ve `EhEntityPath` dizeleri, olay hub'ı değerlerle. Ya da izleyebilirsiniz hello adımları Bu öğretici toocreate kendi.

## <a name="prerequisites"></a>Ön koşullar

* [Microsoft Visual Studio 2015 veya 2017](http://www.visualstudio.com). Bu öğretici kullanımı Visual Studio 2017 Hello örneklerde, ancak Visual Studio 2015'de desteklenir.
* [.NET core Visual Studio 2015 veya 2017 Araçları](http://www.microsoft.com/net/core).
* Azure aboneliği.
* Bir olay hub'ad alanı.

Visual Studio toowrite C# konsol uygulaması toosend iletileri tooan olay hub'ı kullanacağız.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Event Hubs ad alanı ve bir olay hub’ı oluşturma

Merhaba ilk adımdır toouse hello [Azure portal](https://portal.azure.com) toocreate hello olay hub'türü için bir ad alanı ve hello uygulamanızı hello olay hub'ı ile toocommunicate gerektiğini yönetim kimlik bilgilerini alın. toocreate bir ad ve bir event hub hello yordamı izleyin [bu makalede](event-hubs-create.md)ve ardından aşağıdaki adımları hello ile devam edin.

## <a name="create-a-console-application"></a>Konsol uygulaması oluşturma

Visual Studio’yu çalıştırın. Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**. .NET Core konsol uygulaması oluşturun.

![Yeni Proje][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Merhaba olay hub'ları NuGet paketi ekleme

Merhaba eklemek [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) aşağıdaki adımları izleyerek .NET standart kitaplığı NuGet paketi tooyour proje: 

1. Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.
2. Merhaba tıklatın **Gözat** sekmesini ve ardından "Microsoft.Azure.EventHubs" ve select hello arama **Microsoft.Azure.EventHubs** paket. Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Bazı kod toosend iletileri toohello olay hub'ı yazma

1. Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimleri toohello üst.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Ekleme sabitlerin toohello `Program` hello olay hub'ları bağlantı dizesi ve varlık yolu (tek olay hub'ı adı) için sınıf. Köşeli ayraçlar Hello yer tutucuları hello olay hub'ı oluştururken edinilen hello uygun değerlerle değiştirin.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Adlı yeni bir yöntem ekleyin `MainAsync` toohello `Program` sınıfı, şu şekilde:

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

4. Adlı yeni bir yöntem ekleyin `SendMessagesToEventHub` toohello `Program` sınıfı, şu şekilde:

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

5. Aşağıdaki kodu toohello hello eklemek `Main` hello yönteminde `Program` sınıfı.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Program.cs dosyanız aşağıdaki gibi görünmelidir.

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

6. Merhaba programını çalıştırın ve herhangi bir hata olduğundan emin olun.

Tebrikler! İletileri tooan olay hub'ı şimdi gönderdiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Olay hub'larından olayları alma](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](event-hubs-create.md)
* [Event Hubs ile ilgili SSS](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
