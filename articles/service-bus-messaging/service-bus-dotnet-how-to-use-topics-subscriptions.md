---
title: "aaaGet başlatılan Azure Service Bus konuları ve abonelikleri | Microsoft Docs"
description: "Service Bus mesajlaşma konuları ve aboneliklerini kullanan bir C# konsol uygulaması yazın."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Service Bus konuları ile çalışmaya başlama

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>Ne elde edilecek

Bu öğretici hello aşağıdaki adımları kapsar:

1. Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturun.
2. Hello Azure portal kullanarak bir Service Bus konu oluşturun.
3. Hello Azure portal kullanarak bir Service Bus abonelik toothat konu oluşturun.
4. Bir konsol uygulaması toosend bir ileti toohello konu yazın.
5. Bir konsol uygulaması tooreceive hello abonelikten ileti yazın.

## <a name="prerequisites"></a>Ön koşullar

1. [Visual Studio 2015 veya üzeri](http://www.visualstudio.com). Bu öğreticide Hello örnekler Visual Studio 2017 kullanın.
2. Azure aboneliği.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Hello Azure portal kullanarak ad alanı oluşturma

Service Bus Mesajlaşma hizmeti ad alanı zaten oluşturduysanız, toohello atlama [hello Azure portal kullanarak bir konu oluşturun](#2-create-a-topic-using-the-azure-portal) bölümü.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Hello Azure portal kullanarak bir konu oluşturun

1. Toohello üzerinde oturum [Azure portal][azure-portal].
2. Hello sol gezinti bölmesinde hello portalı tıklatın **Service Bus** (görmüyorsanız **Service Bus**, tıklatın **daha fazla hizmet**).
3. Toocreate hello konu istediğiniz hello ad alanına tıklayın. Merhaba ad genel bakış dikey penceresinde görünür:
   
    ![Konu başlığı oluşturma][createtopic1]
4. Merhaba, **Service Bus ad alanı** dikey penceresinde'ı tıklatın **konuları**, ardından **Ekle konu**.
   
    ![Konu Seçme][createtopic2]
5. Merhaba konu için bir ad girin ve hello işaretini **bölümleme etkinleştirmek** seçeneği. Merhaba diğer seçenekleri varsayılan değerleriyle bırakın.
   
    ![Yeni Seçme][createtopic3]
6. Merhaba dikey penceresinde Hello altındaki tıklatın **oluşturma**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Bir abonelik toohello konu oluştur

1. Merhaba portalı kaynakları bölmesinde, 1. adımda oluşturduğunuz hello ad alanına tıklayın ve ardından 2. adımda oluşturduğunuz hello konu adına tıklayın.
2. Merhaba genel bakış bölmesinde, hello üstündeki hello tıklatın artı sonraki çok oturum**abonelik** tooadd bir abonelik toothis konu.

    ![Abonelik oluşturma][createtopic4]

3. Merhaba abonelik için bir ad girin. Merhaba diğer seçenekleri varsayılan değerleriyle bırakın.

## <a name="4-send-messages-toohello-topic"></a>4. İletileri toohello konu gönderin

toosend iletileri toohello konu, Visual Studio kullanarak C# konsol uygulaması yazma.

### <a name="create-a-console-application"></a>Konsol uygulaması oluşturma

Visual Studio'yu başlatın ve yeni bir **Konsol uygulaması (.NET Framework)** projesi oluşturun.

### <a name="add-hello-service-bus-nuget-package"></a>Merhaba Service Bus NuGet paketi ekleme

1. Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.
2. Merhaba tıklatın **Gözat** sekmesinde, arama **Microsoft Azure Service Bus**seçip hello **WindowsAzure.ServiceBus** öğesi. Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.
   
    ![NuGet paketi seçme][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Bir ileti toohello konu bazı kod toosend yazma

1. Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Aşağıdaki kodu toohello hello eklemek `Main` yöntemi. Set hello `connectionString` değişken toohello bağlantı dizesi hello ad alanı oluştururken, edinilen ve ayarlama `topicName` hello konu oluşturulurken kullanılan toohello adı.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Merhaba programını çalıştırın ve hello Azure portal denetleyin: Konunuzu hello ad alanındaki hello adına tıklayın **genel bakış** dikey. Merhaba konu **Essentials** dikey penceresi görüntülenir. Bu hello hello dikey penceresinde Hello altına listelenen hello aboneliklerinden içinde fark **ileti sayısı** değeri her abonelik şimdi 1 olmalıdır. Her zaman hello gönderen uygulama (Merhaba sonraki bölümde açıklandığı gibi) hello ileti alma olmadan çalıştırdığınızda, bu değer 1 ile artırır. Ayrıca bu hello geçerli boyutu hello konu artışlarla hello unutmayın **geçerli** hello değeri **Essentials** dikey penceresinde hello uygulama bir ileti toohello konu başlığının/aboneliğinin ekler her zaman.
   
      ![İleti boyutu][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Merhaba abonelikten ileti alma

1. tooreceive selamlama iletisine veya, yalnızca gönderilen iletiler, yeni bir konsol uygulaması oluşturun ve bir başvuru toohello Service Bus NuGet paketi, benzer toohello önceki gönderen uygulama ekleyin.
2. Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Aşağıdaki kodu toohello hello eklemek `Main` yöntemi. Set hello `connectionString` değişken toohello bağlantı dizesi hello ad alanı oluştururken, edinilen ve ayarlamanıza `topicName` hello konu oluşturulurken kullanılan toohello adı.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. Merhaba programını çalıştırın ve hello portal yeniden denetleyin. Bu hello fark **ileti sayısı** ve **geçerli** değerler şimdi 0.
   
    ![Konu uzunluğu][topic-message-receive]

Tebrikler! Bir konu ve abonelik oluşturdunuz, ileti gönderdiniz ve bu iletiyi aldınız.

## <a name="next-steps"></a>Sonraki adımlar

Kullanıma bizim [örnekleri GitHub deposuyla](https://github.com/Azure/azure-service-bus/tree/master/samples) , göstermek daha gelişmiş özellikler Service Bus Mesajlaşma hello bazıları.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
