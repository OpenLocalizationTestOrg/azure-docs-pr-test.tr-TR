---
title: "Azure Service Bus kuyrukları ile çalışmaya başlama | Microsoft Docs"
description: "Service Bus mesajlaşması kuyruklarını kullanan bir C# konsol uygulaması yazın."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 12/7/2017
ms.author: sethm
ms.openlocfilehash: 6af7e4d238c10c0fed3443db58644e3557525993
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="get-started-with-service-bus-queues"></a>Service Bus kuyrukları ile çalışmaya başlama

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Bu öğreticide aşağıdaki adımlar yer almaktadır:

1. Azure portalı ile Service Bus ad alanı oluşturma.
2. Azure portalını kullanarak Service Bus kuyruğu oluşturma.
3. Sıraya bir dizi ileti göndermek için bir .NET Core konsol uygulaması yazın.
4. Bu iletileri kuyruktan almak için bir .NET Core konsol uygulaması yazın.

## <a name="prerequisites"></a>Ön koşullar

1. [Visual Studio 2017 Güncelleştirme 3 (sürüm 15.3, 26730.01)](http://www.visualstudio.com/vs) veya sonraki sürümler.
2. [NET Core SDK](https://www.microsoft.com/net/download/windows), sürüm 2.0 veya sonraki sürümler.
2. Azure aboneliği.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a>1. Azure portalı kullanılarak ad alanı oluşturma

> [!NOTE] 
> Dilerseniz [PowerShell](/powershell/azure/get-started-azureps) kullanarak Service Bus ad alanı ve mesajlaşma varlıkları da oluşturabilirsiniz. Daha fazla bilgi için bkz. [Service Bus kaynaklarını yönetmek için PowerShell’i kullanma](service-bus-manage-with-ps.md).

Daha önce bir Service Bus Mesajlaşması ad alanı oluşturduysanız [Azure portalını kullanarak kuyruk oluşturma](#2-create-a-queue-using-the-azure-portal) bölümüne atlayın.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-the-azure-portal"></a>2. Azure portalını kullanarak kuyruk oluşturma

Daha önce bir Service Bus kuyruğu oluşturduysanız [Kuyruğa ileti gönderme](#3-send-messages-to-the-queue) bölümüne atlayın.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-to-the-queue"></a>3. Kuyruğa ileti gönderme

Kuyruğa ileti göndermek için, Visual Studio'yu kullanarak bir C# konsol uygulaması yazın.

### <a name="create-a-console-application"></a>Konsol uygulaması oluşturma

Visual Studio'yu başlatın ve yeni bir **Konsol Uygulaması (.NET Core)** projesi oluşturun.

### <a name="add-the-service-bus-nuget-package"></a>Service Bus NuGet paketi ekleme

1. Yeni oluşturulan projeye sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.
2. **Gözat** sekmesine tıklayın, **[Microsoft.Azure.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus/)** araması yapın ve ardından **Microsoft.Azure.ServiceBus** öğesini seçin. Yüklemeyi tamamlamak için **Yükle**'ye tıklayın, ardından bu iletişim kutusunu kapatın.
   
    ![NuGet paketi seçme][nuget-pkg]

### <a name="write-code-to-send-messages-to-the-queue"></a>Kuyruğa ileti göndermek için kod yazma

1. Program.cs’de, ad alanı tanımının üst kısmına, sınıf bildiriminden önce aşağıdaki `using` deyimlerini ekleyin:
   
    ```csharp
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.ServiceBus;
    ```

2. `Program` sınıfında, aşağıdaki değişkenleri bildirin. `ServiceBusConnectionString` değişkenini, ad alanını oluştururken elde ettiğiniz bağlantı dizesine, `QueueName` değerini ise kuyruğu oluştururken kullandığınız ada ayarlayın:
   
    ```csharp
    const string ServiceBusConnectionString = "<your_connection_string>";
    const string QueueName = "<your_queue_name>";
    static IQueueClient queueClient;
    ``` 

3. `Main()` öğesinin varsayılan içeriklerini aşağıdaki kod satırıyla değiştirin:

    ```csharp
    MainAsync().GetAwaiter().GetResult();
    ```

4. `Main()` öğesinden hemen sonra, gönderme iletilerini metoda çağıran aşağıdaki zaman uyumsuz `MainAsync()` metodunu ekleyin:

    ```csharp
    static async Task MainAsync()
    {
        const int numberOfMessages = 10;
        queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

        Console.WriteLine("======================================================");
        Console.WriteLine("Press ENTER key to exit after sending all the messages.");
        Console.WriteLine("======================================================");

        // Send messages.
        await SendMessagesAsync(numberOfMessages);

        Console.ReadKey();

        await queueClient.CloseAsync();
    }
    ```

5. `MainAsync()` metodundan hemen sonra, `numberOfMessagesToSend` tarafından belirlenen sayıda mesajı (geçerli değer: 10) gönderen aşağıdaki `SendMessagesAsync()` metodunu ekleyin:

    ```csharp
    static async Task SendMessagesAsync(int numberOfMessagesToSend)
    {
        try
        {
            for (var i = 0; i < numberOfMessagesToSend; i++)
            {
                // Create a new message to send to the queue.
                string messageBody = $"Message {i}";
                var message = new Message(Encoding.UTF8.GetBytes(messageBody));

                // Write the body of the message to the console.
                Console.WriteLine($"Sending message: {messageBody}");

                // Send the message to the queue.
                await queueClient.SendAsync(message);
            }
        }
        catch (Exception exception)
        {
            Console.WriteLine($"{DateTime.Now} :: Exception: {exception.Message}");
        }
    }
    ```
   
6. Program.cs dosyanızın şu biçimde olması gerekir:
   
    ```csharp
    namespace CoreSenderApp
    {
        using System;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.ServiceBus;

        class Program
        {
            // Connection String for the namespace can be obtained from the Azure portal under the 
            // 'Shared Access policies' section.
            const string ServiceBusConnectionString = "<your_connection_string>";
            const string QueueName = "<your_queue_name>";
            static IQueueClient queueClient;

            static void Main(string[] args)
            {
                MainAsync().GetAwaiter().GetResult();
            }

            static async Task MainAsync()
            {
                const int numberOfMessages = 10;
                queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

                Console.WriteLine("======================================================");
                Console.WriteLine("Press ENTER key to exit after receiving all the messages.");
                Console.WriteLine("======================================================");

                // Send Messages
                await SendMessagesAsync(numberOfMessages);
                        
                Console.ReadKey();

                await queueClient.CloseAsync();
            }

            static async Task SendMessagesAsync(int numberOfMessagesToSend)
            {
                try
                {
                    for (var i = 0; i < numberOfMessagesToSend; i++)
                    {
                        // Create a new message to send to the queue
                        string messageBody = $"Message {i}";
                        var message = new Message(Encoding.UTF8.GetBytes(messageBody));

                        // Write the body of the message to the console
                        Console.WriteLine($"Sending message: {messageBody}");

                        // Send the message to the queue
                        await queueClient.SendAsync(message);
                    }
                }
                catch (Exception exception)
                {
                    Console.WriteLine($"{DateTime.Now} :: Exception: {exception.Message}");
                }
            }
        }
    }
    ```

7. Programı çalıştırın ve Azure portalını denetleyin: Ad alanına ilişkin **Genel Bakış** penceresinde kuyruğunuzun adına tıklayın. Kuyruğun **Temel Bileşenler** penceresi gösterilir. Kuyruğun **Etkin İleti Sayısı** değerinin **10** olduğuna dikkat edin. İletileri almadan gönderen uygulamasını her çalıştırdığınızda (sonraki bölümde açıklandığı gibi), bu değer 10 artar. Ayrıca, uygulamanın kuyruğa ileti eklediği her durumda kuyruğun geçerli boyutu, **Temel Bileşenler** penceresindeki **Geçerli** değerini artırır.
   
      ![İleti boyutu][queue-message]

## <a name="4-receive-messages-from-the-queue"></a>4. Kuyruktan ileti alma

Gönderdiğiniz iletileri almak için farklı bir .NET Core konsol uygulaması oluşturun ve önceki gönderen uygulamaya benzer şekilde, **Microsoft.Azure.ServiceBus** NuGet paketine başvuru ekleyin.

### <a name="write-code-to-receive-messages-from-the-queue"></a>Kuyruktan ileti almak için kod yazma

1. Program.cs’de, ad alanı tanımının üst kısmına, sınıf bildiriminden önce aşağıdaki `using` deyimlerini ekleyin:
   
    ```csharp
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.ServiceBus;
    ```

2. `Program` sınıfında, aşağıdaki değişkenleri bildirin. `ServiceBusConnectionString` değişkenini, ad alanını oluştururken elde ettiğiniz bağlantı dizesine, `QueueName` değerini ise kuyruğu oluştururken kullandığınız ada ayarlayın:
   
    ```csharp
    const string ServiceBusConnectionString = "<your_connection_string>";
    const string QueueName = "<your_queue_name>";
    static IQueueClient queueClient;
    ```

3. `Main()` öğesinin varsayılan içeriklerini aşağıdaki kod satırıyla değiştirin:

    ```csharp
    MainAsync().GetAwaiter().GetResult();
    ```

4. `Main()` öğesinden hemen sonra, `RegisterOnMessageHandlerAndReceiveMessages()` metoduna çağrı yapan aşağıdaki zaman uyumsuz `MainAsync()` metodunu ekleyin:

    ```csharp
    static async Task MainAsync()
    {
        queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

        Console.WriteLine("======================================================");
        Console.WriteLine("Press ENTER key to exit after receiving all the messages.");
        Console.WriteLine("======================================================");

        // Register the queue message handler and receive messages in a loop
        RegisterOnMessageHandlerAndReceiveMessages();

        Console.ReadKey();

        await queueClient.CloseAsync();
    }
    ```

5. `MainAsync()` metodundan hemen sonra, ileti işleyiciyi kaydeden ve gönderen uygulama tarafından gönderilen iletileri alan aşağıdaki metodu ekleyin:

    ```csharp
    static void RegisterOnMessageHandlerAndReceiveMessages()
    {
        // Configure the message handler options in terms of exception handling, number of concurrent messages to deliver, etc.
        var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
        {
            // Maximum number of concurrent calls to the callback ProcessMessagesAsync(), set to 1 for simplicity.
            // Set it according to how many messages the application wants to process in parallel.
            MaxConcurrentCalls = 1,

            // Indicates whether the message pump should automatically complete the messages after returning from user callback.
            // False below indicates the complete operation is handled by the user callback as in ProcessMessagesAsync().
            AutoComplete = false
        };

        // Register the function that processes messages.
        queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    }
    ```

6. Önceki metottan hemen sonra, alınan mesajları işlemek için aşağıdaki `ProcessMessagesAsync()` metodunu ekleyin:
 
    ```csharp
    static async Task ProcessMessagesAsync(Message message, CancellationToken token)
    {
        // Process the message.
        Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");

        // Complete the message so that it is not received again.
        // This can be done only if the queue Client is created in ReceiveMode.PeekLock mode (which is the default).
        await queueClient.CompleteAsync(message.SystemProperties.LockToken);

        // Note: Use the cancellationToken passed as necessary to determine if the queueClient has already been closed.
        // If queueClient has already been closed, you can choose to not call CompleteAsync() or AbandonAsync() etc.
        // to avoid unnecessary exceptions.
    }
    ```

7. Son olarak, olası özel durumları işlemek için aşağıdaki metodu ekleyin:
 
    ```csharp
    // Use this handler to examine the exceptions received on the message pump.
    static Task ExceptionReceivedHandler(ExceptionReceivedEventArgs exceptionReceivedEventArgs)
    {
        Console.WriteLine($"Message handler encountered an exception {exceptionReceivedEventArgs.Exception}.");
        var context = exceptionReceivedEventArgs.ExceptionReceivedContext;
        Console.WriteLine("Exception context for troubleshooting:");
        Console.WriteLine($"- Endpoint: {context.Endpoint}");
        Console.WriteLine($"- Entity Path: {context.EntityPath}");
        Console.WriteLine($"- Executing Action: {context.Action}");
        return Task.CompletedTask;
    }    
    ```    
   
8. Program.cs dosyanız aşağıdaki gibi görünmelidir:
   
    ```csharp
    namespace CoreReceiverApp
    {
        using System;
        using System.Text;
        using System.Threading;
        using System.Threading.Tasks;
        using Microsoft.Azure.ServiceBus;

        class Program
        {
            // Connection String for the namespace can be obtained from the Azure portal under the 
            // 'Shared Access policies' section.
            const string ServiceBusConnectionString = "<your_connection_string>";
            const string QueueName = "<your_queue_name>";
            static IQueueClient queueClient;

            static void Main(string[] args)
            {
                MainAsync().GetAwaiter().GetResult();
            }

            static async Task MainAsync()
            {
                queueClient = new QueueClient(ServiceBusConnectionString, QueueName);

                Console.WriteLine("======================================================");
                Console.WriteLine("Press ENTER key to exit after receiving all the messages.");
                Console.WriteLine("======================================================");

                // Register QueueClient's MessageHandler and receive messages in a loop
                RegisterOnMessageHandlerAndReceiveMessages();
                    
                Console.ReadKey();

                await queueClient.CloseAsync();
            }

            static void RegisterOnMessageHandlerAndReceiveMessages()
            {
                // Configure the MessageHandler Options in terms of exception handling, number of concurrent messages to deliver etc.
                var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
                {
                    // Maximum number of Concurrent calls to the callback `ProcessMessagesAsync`, set to 1 for simplicity.
                    // Set it according to how many messages the application wants to process in parallel.
                    MaxConcurrentCalls = 1,

                    // Indicates whether MessagePump should automatically complete the messages after returning from User Callback.
                    // False below indicates the Complete will be handled by the User Callback as in `ProcessMessagesAsync` below.
                    AutoComplete = false
                };

                // Register the function that will process messages
                queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
            }

            static async Task ProcessMessagesAsync(Message message, CancellationToken token)
            {
                // Process the message
                Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");

                // Complete the message so that it is not received again.
                // This can be done only if the queueClient is created in ReceiveMode.PeekLock mode (which is default).
                await queueClient.CompleteAsync(message.SystemProperties.LockToken);

                // Note: Use the cancellationToken passed as necessary to determine if the queueClient has already been closed.
                // If queueClient has already been Closed, you may chose to not call CompleteAsync() or AbandonAsync() etc. calls 
               // to avoid unnecessary exceptions.
            }

            static Task ExceptionReceivedHandler(ExceptionReceivedEventArgs exceptionReceivedEventArgs)
            {
                Console.WriteLine($"Message handler encountered an exception {exceptionReceivedEventArgs.Exception}.");
                var context = exceptionReceivedEventArgs.ExceptionReceivedContext;
                Console.WriteLine("Exception context for troubleshooting:");
                Console.WriteLine($"- Endpoint: {context.Endpoint}");
                Console.WriteLine($"- Entity Path: {context.EntityPath}");
                Console.WriteLine($"- Executing Action: {context.Action}");
                return Task.CompletedTask;
            }
        }
    }
    ```
4. Programı çalıştırın ve portalı tekrar denetleyin. Bu işlemden sonra **Etkin Mesaj Sayısı** ve **Geçerli** değerlerinin **0** olduğuna dikkat edin.
   
    ![Kuyruk uzunluğu][queue-message-receive]

Tebrikler! Bir kuyruk oluşturdunuz, bu kuyruğa bir dizi ileti gönderdiniz ve aynı kuyruktan ileti aldınız.

## <a name="next-steps"></a>Sonraki adımlar

Service Bus mesajlaşmasının daha gelişmiş özelliklerini gösteren [örneklerin bulunduğu GitHub depomuza](https://github.com/Azure/azure-service-bus/tree/master/samples) göz atın.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png

