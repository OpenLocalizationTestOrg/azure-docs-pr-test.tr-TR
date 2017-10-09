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
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="83bf0-103">Service Bus kuyrukları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="83bf0-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="83bf0-104">Ne elde edilecek</span><span class="sxs-lookup"><span data-stu-id="83bf0-104">What will be accomplished</span></span>
<span data-ttu-id="83bf0-105">Bu öğretici hello aşağıdaki adımları kapsar:</span><span class="sxs-lookup"><span data-stu-id="83bf0-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="83bf0-106">Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="83bf0-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="83bf0-107">Hello Azure portal kullanarak bir Service Bus kuyruğu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="83bf0-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="83bf0-108">Bir konsol uygulaması toosend bir ileti yazın.</span><span class="sxs-lookup"><span data-stu-id="83bf0-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="83bf0-109">Bir konsol uygulaması tooreceive hello hello önceki adımda gönderilen iletileri yazma.</span><span class="sxs-lookup"><span data-stu-id="83bf0-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83bf0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="83bf0-110">Prerequisites</span></span>
1. <span data-ttu-id="83bf0-111">[Visual Studio 2015 veya üzeri](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="83bf0-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="83bf0-112">Bu öğreticide Hello örnekler Visual Studio 2017 kullanın.</span><span class="sxs-lookup"><span data-stu-id="83bf0-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="83bf0-113">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="83bf0-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="83bf0-114">1. Hello Azure portal kullanarak ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="83bf0-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="83bf0-115">Service Bus Mesajlaşma hizmeti ad alanı zaten oluşturduysanız, toohello atlama [hello Azure portal kullanarak bir kuyruk oluşturun](#2-create-a-queue-using-the-azure-portal) bölümü.</span><span class="sxs-lookup"><span data-stu-id="83bf0-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="83bf0-116">2. Hello Azure portal kullanarak bir sıra oluşturun</span><span class="sxs-lookup"><span data-stu-id="83bf0-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="83bf0-117">Service Bus kuyruğuna zaten oluşturduysanız, toohello atlama [gönderme iletileri toohello sırası](#3-send-messages-to-the-queue) bölümü.</span><span class="sxs-lookup"><span data-stu-id="83bf0-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="83bf0-118">3. İletileri toohello sırası Gönder</span><span class="sxs-lookup"><span data-stu-id="83bf0-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="83bf0-119">toosend iletileri toohello sırası, Visual Studio kullanarak C# konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="83bf0-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="83bf0-120">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="83bf0-120">Create a console application</span></span>

<span data-ttu-id="83bf0-121">Visual Studio'yu başlatın ve yeni bir **Konsol uygulaması (.NET Framework)** projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="83bf0-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="83bf0-122">Merhaba Service Bus NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="83bf0-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="83bf0-123">Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="83bf0-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="83bf0-124">Merhaba tıklatın **Gözat** sekmesinde, arama **Microsoft Azure Service Bus**seçip hello **WindowsAzure.ServiceBus** öğesi.</span><span class="sxs-lookup"><span data-stu-id="83bf0-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="83bf0-125">Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="83bf0-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![NuGet paketi seçme][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="83bf0-127">Bir ileti toohello sırası bazı kod toosend yazma</span><span class="sxs-lookup"><span data-stu-id="83bf0-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="83bf0-128">Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.</span><span class="sxs-lookup"><span data-stu-id="83bf0-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="83bf0-129">Aşağıdaki kodu toohello hello eklemek `Main` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="83bf0-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="83bf0-130">Set hello `connectionString` değişken toohello bağlantı dizesi hello ad alanı oluştururken, edinilen ve ayarlama `queueName` hello sıra oluşturulurken kullanılan toohello sıra adı.</span><span class="sxs-lookup"><span data-stu-id="83bf0-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="83bf0-131">Program.cs dosyanızın şu biçimde olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="83bf0-131">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="83bf0-132">Merhaba programını çalıştırın ve hello Azure portal denetleyin: sıranız hello ad alanındaki hello adına tıklayın **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="83bf0-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="83bf0-133">Merhaba sıra **Essentials** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="83bf0-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="83bf0-134">Bu hello fark **etkin ileti sayısı** değeri artık 1 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="83bf0-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="83bf0-135">Merhaba, iletilere olmadan hello gönderen uygulama çalıştıran her zaman bu değer 1 ile artar.</span><span class="sxs-lookup"><span data-stu-id="83bf0-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="83bf0-136">Ayrıca bir ileti toohello sırası hello geçerli boyutu hello sırasının her zaman hello uygulama artırır Not ekler.</span><span class="sxs-lookup"><span data-stu-id="83bf0-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![İleti boyutu][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="83bf0-138">4. Merhaba kuyruktan ileti alma</span><span class="sxs-lookup"><span data-stu-id="83bf0-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="83bf0-139">tooreceive karışılama iletileri yalnızca gönderdiğiniz, yeni bir konsol uygulaması oluşturun ve bir başvuru toohello Service Bus NuGet paketi, benzer toohello önceki gönderen uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="83bf0-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="83bf0-140">Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.</span><span class="sxs-lookup"><span data-stu-id="83bf0-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="83bf0-141">Aşağıdaki kodu toohello hello eklemek `Main` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="83bf0-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="83bf0-142">Set hello `connectionString` hello ad alanı oluştururken, edinilen ve ayarlama değişken toohello bağlantı dizesi `queueName` hello sıra oluşturulurken kullanılan toohello sıra adı.</span><span class="sxs-lookup"><span data-stu-id="83bf0-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="83bf0-143">Program.cs dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="83bf0-143">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="83bf0-144">Merhaba programını çalıştırın ve hello portal yeniden denetleyin.</span><span class="sxs-lookup"><span data-stu-id="83bf0-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="83bf0-145">Bu hello fark **etkin ileti sayısı** ve **geçerli** değerler şimdi 0.</span><span class="sxs-lookup"><span data-stu-id="83bf0-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Kuyruk uzunluğu][queue-message-receive]

<span data-ttu-id="83bf0-147">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="83bf0-147">Congratulations!</span></span> <span data-ttu-id="83bf0-148">Bir kuyruk oluşturdunuz, ileti gönderdiniz ve ileti aldınız.</span><span class="sxs-lookup"><span data-stu-id="83bf0-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83bf0-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="83bf0-149">Next steps</span></span>

<span data-ttu-id="83bf0-150">Kullanıma bizim [örnekleri GitHub deposuyla](https://github.com/Azure/azure-service-bus/tree/master/samples) , göstermek daha gelişmiş özellikler Service Bus Mesajlaşma hello bazıları.</span><span class="sxs-lookup"><span data-stu-id="83bf0-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
