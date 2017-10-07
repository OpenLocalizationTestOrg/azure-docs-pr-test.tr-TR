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
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="d099d-103">Service Bus konuları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d099d-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="d099d-104">Ne elde edilecek</span><span class="sxs-lookup"><span data-stu-id="d099d-104">What will be accomplished</span></span>

<span data-ttu-id="d099d-105">Bu öğretici hello aşağıdaki adımları kapsar:</span><span class="sxs-lookup"><span data-stu-id="d099d-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="d099d-106">Hello Azure portal kullanarak bir hizmet veri yolu ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d099d-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="d099d-107">Hello Azure portal kullanarak bir Service Bus konu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d099d-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="d099d-108">Hello Azure portal kullanarak bir Service Bus abonelik toothat konu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d099d-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="d099d-109">Bir konsol uygulaması toosend bir ileti toohello konu yazın.</span><span class="sxs-lookup"><span data-stu-id="d099d-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="d099d-110">Bir konsol uygulaması tooreceive hello abonelikten ileti yazın.</span><span class="sxs-lookup"><span data-stu-id="d099d-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d099d-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d099d-111">Prerequisites</span></span>

1. <span data-ttu-id="d099d-112">[Visual Studio 2015 veya üzeri](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d099d-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="d099d-113">Bu öğreticide Hello örnekler Visual Studio 2017 kullanın.</span><span class="sxs-lookup"><span data-stu-id="d099d-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="d099d-114">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="d099d-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="d099d-115">1. Hello Azure portal kullanarak ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d099d-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="d099d-116">Service Bus Mesajlaşma hizmeti ad alanı zaten oluşturduysanız, toohello atlama [hello Azure portal kullanarak bir konu oluşturun](#2-create-a-topic-using-the-azure-portal) bölümü.</span><span class="sxs-lookup"><span data-stu-id="d099d-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="d099d-117">2. Hello Azure portal kullanarak bir konu oluşturun</span><span class="sxs-lookup"><span data-stu-id="d099d-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="d099d-118">Toohello üzerinde oturum [Azure portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d099d-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="d099d-119">Hello sol gezinti bölmesinde hello portalı tıklatın **Service Bus** (görmüyorsanız **Service Bus**, tıklatın **daha fazla hizmet**).</span><span class="sxs-lookup"><span data-stu-id="d099d-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="d099d-120">Toocreate hello konu istediğiniz hello ad alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d099d-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="d099d-121">Merhaba ad genel bakış dikey penceresinde görünür:</span><span class="sxs-lookup"><span data-stu-id="d099d-121">hello namespace overview blade appears:</span></span>
   
    ![Konu başlığı oluşturma][createtopic1]
4. <span data-ttu-id="d099d-123">Merhaba, **Service Bus ad alanı** dikey penceresinde'ı tıklatın **konuları**, ardından **Ekle konu**.</span><span class="sxs-lookup"><span data-stu-id="d099d-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Konu Seçme][createtopic2]
5. <span data-ttu-id="d099d-125">Merhaba konu için bir ad girin ve hello işaretini **bölümleme etkinleştirmek** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d099d-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="d099d-126">Merhaba diğer seçenekleri varsayılan değerleriyle bırakın.</span><span class="sxs-lookup"><span data-stu-id="d099d-126">Leave hello other options with their default values.</span></span>
   
    ![Yeni Seçme][createtopic3]
6. <span data-ttu-id="d099d-128">Merhaba dikey penceresinde Hello altındaki tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d099d-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="d099d-129">3. Bir abonelik toohello konu oluştur</span><span class="sxs-lookup"><span data-stu-id="d099d-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="d099d-130">Merhaba portalı kaynakları bölmesinde, 1. adımda oluşturduğunuz hello ad alanına tıklayın ve ardından 2. adımda oluşturduğunuz hello konu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d099d-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="d099d-131">Merhaba genel bakış bölmesinde, hello üstündeki hello tıklatın artı sonraki çok oturum**abonelik** tooadd bir abonelik toothis konu.</span><span class="sxs-lookup"><span data-stu-id="d099d-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Abonelik oluşturma][createtopic4]

3. <span data-ttu-id="d099d-133">Merhaba abonelik için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="d099d-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="d099d-134">Merhaba diğer seçenekleri varsayılan değerleriyle bırakın.</span><span class="sxs-lookup"><span data-stu-id="d099d-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="d099d-135">4. İletileri toohello konu gönderin</span><span class="sxs-lookup"><span data-stu-id="d099d-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="d099d-136">toosend iletileri toohello konu, Visual Studio kullanarak C# konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="d099d-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="d099d-137">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d099d-137">Create a console application</span></span>

<span data-ttu-id="d099d-138">Visual Studio'yu başlatın ve yeni bir **Konsol uygulaması (.NET Framework)** projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d099d-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="d099d-139">Merhaba Service Bus NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="d099d-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="d099d-140">Yeni oluşturulan hello projesine sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="d099d-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="d099d-141">Merhaba tıklatın **Gözat** sekmesinde, arama **Microsoft Azure Service Bus**seçip hello **WindowsAzure.ServiceBus** öğesi.</span><span class="sxs-lookup"><span data-stu-id="d099d-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="d099d-142">Tıklatın **yükleme** toocomplete hello yükleme, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="d099d-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![NuGet paketi seçme][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="d099d-144">Bir ileti toohello konu bazı kod toosend yazma</span><span class="sxs-lookup"><span data-stu-id="d099d-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="d099d-145">Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.</span><span class="sxs-lookup"><span data-stu-id="d099d-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="d099d-146">Aşağıdaki kodu toohello hello eklemek `Main` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d099d-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="d099d-147">Set hello `connectionString` değişken toohello bağlantı dizesi hello ad alanı oluştururken, edinilen ve ayarlama `topicName` hello konu oluşturulurken kullanılan toohello adı.</span><span class="sxs-lookup"><span data-stu-id="d099d-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="d099d-148">Program.cs dosyanızın şu biçimde olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d099d-148">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="d099d-149">Merhaba programını çalıştırın ve hello Azure portal denetleyin: Konunuzu hello ad alanındaki hello adına tıklayın **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="d099d-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="d099d-150">Merhaba konu **Essentials** dikey penceresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d099d-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="d099d-151">Bu hello hello dikey penceresinde Hello altına listelenen hello aboneliklerinden içinde fark **ileti sayısı** değeri her abonelik şimdi 1 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d099d-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="d099d-152">Her zaman hello gönderen uygulama (Merhaba sonraki bölümde açıklandığı gibi) hello ileti alma olmadan çalıştırdığınızda, bu değer 1 ile artırır.</span><span class="sxs-lookup"><span data-stu-id="d099d-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="d099d-153">Ayrıca bu hello geçerli boyutu hello konu artışlarla hello unutmayın **geçerli** hello değeri **Essentials** dikey penceresinde hello uygulama bir ileti toohello konu başlığının/aboneliğinin ekler her zaman.</span><span class="sxs-lookup"><span data-stu-id="d099d-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![İleti boyutu][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="d099d-155">5. Merhaba abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="d099d-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="d099d-156">tooreceive selamlama iletisine veya, yalnızca gönderilen iletiler, yeni bir konsol uygulaması oluşturun ve bir başvuru toohello Service Bus NuGet paketi, benzer toohello önceki gönderen uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d099d-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="d099d-157">Merhaba aşağıdakileri ekleyin `using` hello Program.cs dosyasının deyimi toohello üst.</span><span class="sxs-lookup"><span data-stu-id="d099d-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="d099d-158">Aşağıdaki kodu toohello hello eklemek `Main` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d099d-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="d099d-159">Set hello `connectionString` değişken toohello bağlantı dizesi hello ad alanı oluştururken, edinilen ve ayarlamanıza `topicName` hello konu oluşturulurken kullanılan toohello adı.</span><span class="sxs-lookup"><span data-stu-id="d099d-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="d099d-160">Program.cs dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d099d-160">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="d099d-161">Merhaba programını çalıştırın ve hello portal yeniden denetleyin.</span><span class="sxs-lookup"><span data-stu-id="d099d-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="d099d-162">Bu hello fark **ileti sayısı** ve **geçerli** değerler şimdi 0.</span><span class="sxs-lookup"><span data-stu-id="d099d-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Konu uzunluğu][topic-message-receive]

<span data-ttu-id="d099d-164">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="d099d-164">Congratulations!</span></span> <span data-ttu-id="d099d-165">Bir konu ve abonelik oluşturdunuz, ileti gönderdiniz ve bu iletiyi aldınız.</span><span class="sxs-lookup"><span data-stu-id="d099d-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d099d-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d099d-166">Next steps</span></span>

<span data-ttu-id="d099d-167">Kullanıma bizim [örnekleri GitHub deposuyla](https://github.com/Azure/azure-service-bus/tree/master/samples) , göstermek daha gelişmiş özellikler Service Bus Mesajlaşma hello bazıları.</span><span class="sxs-lookup"><span data-stu-id="d099d-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

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
