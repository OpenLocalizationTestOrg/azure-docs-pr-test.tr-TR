---
title: "aaaGet ile Azure Service Bus kuyruklarını kullanmaya | Microsoft Docs"
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
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Service Bus kuyrukları ile çalışmaya başlama
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>Ne elde edilecek
Bu öğretici hello aşağıdaki adımları kapsar:

1. Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturun.
2. Hello Azure portal kullanarak bir Service Bus kuyruğu oluşturun.
3. Bir konsol uygulaması toosend bir ileti yazın.
4. Bir konsol uygulaması tooreceive hello hello önceki adımda gönderilen iletileri yazma.

## <a name="prerequisites"></a>Ön koşullar
1. [Visual Studio 2015 veya üzeri](http://www.visualstudio.com). Bu öğreticide Hello örnekler Visual Studio 2017 kullanın.
2. Azure aboneliği.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Hello Azure portal kullanarak ad alanı oluşturma
Service Bus Mesajlaşma hizmeti ad alanı zaten oluşturduysanız, toohello atlama [hello Azure portal kullanarak bir kuyruk oluşturun](#2-create-a-queue-using-the-azure-portal) bölümü.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Hello Azure portal kullanarak bir sıra oluşturun
Service Bus kuyruğuna zaten oluşturduysanız, toohello atlama [gönderme iletileri toohello sırası](#3-send-messages-to-the-queue) bölümü.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. İletileri toohello sırası Gönder
toosend iletileri toohello sırası, Visual Studio kullanarak C# konsol uygulaması yazma.

### <a name="create-a-console-application"></a>Konsol uygulaması oluşturma

Visual Studio'yu başlatın ve yeni bir **Konsol uygulaması (.NET Framework)** projesi oluşturun.

### <a name="add-hello-service-bus-nuget-package"></a>Merhaba Service Bus NuGet paketi ekleme
1. Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.
2. Merhaba tıklatın **Gözat** sekmesinde, arama **Microsoft Azure Service Bus**seçip hello **WindowsAzure.ServiceBus** öğesi. Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.
   
    ![NuGet paketi seçme][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Bir ileti toohello sırası bazı kod toosend yazma
1. Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Aşağıdaki kodu toohello hello eklemek `Main` yöntemi. Set hello `connectionString` değişken toohello bağlantı dizesi hello ad alanı oluştururken, edinilen ve ayarlama `queueName` hello sıra oluşturulurken kullanılan toohello sıra adı.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Program.cs dosyanızın şu biçimde olması gerekir:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Merhaba programını çalıştırın ve hello Azure portal denetleyin: sıranız hello ad alanındaki hello adına tıklayın **genel bakış** dikey. Merhaba sıra **Essentials** dikey penceresi görüntülenir. Bu hello fark **etkin ileti sayısı** değeri artık 1 olmalıdır. Merhaba, iletilere olmadan hello gönderen uygulama çalıştıran her zaman bu değer 1 ile artar. Ayrıca bir ileti toohello sırası hello geçerli boyutu hello sırasının her zaman hello uygulama artırır Not ekler.
   
      ![İleti boyutu][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Merhaba kuyruktan ileti alma

1. tooreceive karışılama iletileri yalnızca gönderdiğiniz, yeni bir konsol uygulaması oluşturun ve bir başvuru toohello Service Bus NuGet paketi, benzer toohello önceki gönderen uygulama ekleyin.
2. Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Aşağıdaki kodu toohello hello eklemek `Main` yöntemi. Set hello `connectionString` hello ad alanı oluştururken, edinilen ve ayarlama değişken toohello bağlantı dizesi `queueName` hello sıra oluşturulurken kullanılan toohello sıra adı.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Program.cs dosyanız aşağıdaki gibi görünmelidir:
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Merhaba programını çalıştırın ve hello portal yeniden denetleyin. Bu hello fark **etkin ileti sayısı** ve **geçerli** değerler şimdi 0.
   
    ![Kuyruk uzunluğu][queue-message-receive]

Tebrikler! Bir kuyruk oluşturdunuz, ileti gönderdiniz ve ileti aldınız.

## <a name="next-steps"></a>Sonraki adımlar

Kullanıma bizim [örnekleri GitHub deposuyla](https://github.com/Azure/azure-service-bus/tree/master/samples) , göstermek daha gelişmiş özellikler Service Bus Mesajlaşma hello bazıları.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
