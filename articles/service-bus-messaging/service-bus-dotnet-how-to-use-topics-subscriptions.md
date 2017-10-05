---
title: "Azure Service Bus konuları ve abonelikleri ile çalışmaya başlama | Microsoft Docs"
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
ms.openlocfilehash: 9401ada519f600b0d2817f06a396e16607a24129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="a4fbd-103">Service Bus konuları ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a4fbd-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="a4fbd-104">Ne elde edilecek</span><span class="sxs-lookup"><span data-stu-id="a4fbd-104">What will be accomplished</span></span>

<span data-ttu-id="a4fbd-105">Bu öğreticide aşağıdaki adımlar yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="a4fbd-105">This tutorial covers the following steps:</span></span>

1. <span data-ttu-id="a4fbd-106">Azure portalı ile Service Bus ad alanı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-106">Create a Service Bus namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="a4fbd-107">Azure portalı ile Service Bus konusu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-107">Create a Service Bus topic, using the Azure portal.</span></span>
3. <span data-ttu-id="a4fbd-108">Azure portalı ile bu konu için bir Service Bus aboneliği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-108">Create a Service Bus subscription to that topic, using the Azure portal.</span></span>
4. <span data-ttu-id="a4fbd-109">Konuya ileti göndermek için bir konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-109">Write a console application to send a message to the topic.</span></span>
5. <span data-ttu-id="a4fbd-110">Abonelikten bu iletiyi almak için bir konsol uygulaması yazma.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-110">Write a console application to receive that message from the subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4fbd-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a4fbd-111">Prerequisites</span></span>

1. <span data-ttu-id="a4fbd-112">[Visual Studio 2015 veya üzeri](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="a4fbd-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="a4fbd-113">Bu öğreticideki örneklerde Visual Studio 2017 kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-113">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="a4fbd-114">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="a4fbd-115">1. Azure portalı kullanılarak ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4fbd-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="a4fbd-116">Daha önce bir Service Bus Mesajlaşma ad alanı oluşturduysanız [Azure portalını kullanarak konu oluşturma](#2-create-a-topic-using-the-azure-portal) bölümüne atlayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-116">If you have already created a Service Bus Messaging namespace, jump to the [Create a topic using the Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-the-azure-portal"></a><span data-ttu-id="a4fbd-117">2. Azure portalını kullanarak konu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4fbd-117">2. Create a topic using the Azure portal</span></span>

1. <span data-ttu-id="a4fbd-118">[Azure portalında][azure-portal] oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-118">Log on to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="a4fbd-119">Portalın sol tarafındaki gezinme bölmesinde **Service Bus**'a tıklayın (**Service Bus** yoksa **Diğer hizmetler**'e tıklayın).</span><span class="sxs-lookup"><span data-stu-id="a4fbd-119">In the left navigation pane of the portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="a4fbd-120">Konuyu oluşturmak istediğiniz ad alanına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-120">Click the namespace in which you would like to create the topic.</span></span> <span data-ttu-id="a4fbd-121">Ad alanına genel bakış dikey penceresi görünür:</span><span class="sxs-lookup"><span data-stu-id="a4fbd-121">The namespace overview blade appears:</span></span>
   
    ![Konu başlığı oluşturma][createtopic1]
4. <span data-ttu-id="a4fbd-123">**Service Bus ad alanı** dikey penceresinde **Konular** ve ardından **Konu ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-123">In the **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Konu Seçme][createtopic2]
5. <span data-ttu-id="a4fbd-125">Konu için bir ad girin ve **Bölümlemeyi etkinleştir** seçeneğini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-125">Enter a name for the topic, and uncheck the **Enable partitioning** option.</span></span> <span data-ttu-id="a4fbd-126">Diğer seçenekleri varsayılan değerlerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-126">Leave the other options with their default values.</span></span>
   
    ![Yeni Seçme][createtopic3]
6. <span data-ttu-id="a4fbd-128">Dikey pencerenin altında yer alan **Oluştur** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-128">At the bottom of the blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-to-the-topic"></a><span data-ttu-id="a4fbd-129">3. Konuya abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4fbd-129">3. Create a subscription to the topic</span></span>

1. <span data-ttu-id="a4fbd-130">Portal kaynakları bölmesinde, 1. adımda oluşturduğunuz ad alanına tıklayın ve ardından 2. adımda oluşturduğunuz konu adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-130">In the portal resources pane, click the namespace you created in step 1, then click name of the topic you created in step 2.</span></span>
2. <span data-ttu-id="a4fbd-131">Genel bakış bölmesinin üst kısmında **Abonelik** seçeneğinin yanındaki artı işaretine tıklayarak bu konuya bir abonelik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-131">A the top of the overview pane, click the plus sign next to **Subscription** to add a subscription to this topic.</span></span>

    ![Abonelik oluşturma][createtopic4]

3. <span data-ttu-id="a4fbd-133">Abonelik için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-133">Enter a name for the subscription.</span></span> <span data-ttu-id="a4fbd-134">Diğer seçenekleri varsayılan değerlerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-134">Leave the other options with their default values.</span></span>

## <a name="4-send-messages-to-the-topic"></a><span data-ttu-id="a4fbd-135">4. Konuya ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="a4fbd-135">4. Send messages to the topic</span></span>

<span data-ttu-id="a4fbd-136">Konuya ileti göndermek için Visual Studio kullanılarak bir C# konsol uygulaması yazılır.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-136">To send messages to the topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="a4fbd-137">Konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4fbd-137">Create a console application</span></span>

<span data-ttu-id="a4fbd-138">Visual Studio'yu başlatın ve yeni bir **Konsol uygulaması (.NET Framework)** projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-the-service-bus-nuget-package"></a><span data-ttu-id="a4fbd-139">Service Bus NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="a4fbd-139">Add the Service Bus NuGet package</span></span>

1. <span data-ttu-id="a4fbd-140">Yeni oluşturulan projeye sağ tıklayın ve **NuGet Paketlerini Yönet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-140">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="a4fbd-141">**Gözat** sekmesine tıklayın, **Microsoft Azure Service Bus** araması yapın ve **WindowsAzure.ServiceBus** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-141">Click the **Browse** tab, search for **Microsoft Azure Service Bus**, and then select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="a4fbd-142">Yüklemeyi tamamlamak için **Yükle**'ye tıklayın, ardından bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-142">Click **Install** to complete the installation, then close this dialog box.</span></span>
   
    ![NuGet paketi seçme][nuget-pkg]

### <a name="write-some-code-to-send-a-message-to-the-topic"></a><span data-ttu-id="a4fbd-144">Konuya ileti göndermek için kod yazma</span><span class="sxs-lookup"><span data-stu-id="a4fbd-144">Write some code to send a message to the topic</span></span>

1. <span data-ttu-id="a4fbd-145">Aşağıdaki `using` deyimini Program.cs dosyasının üst kısmına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-145">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="a4fbd-146">`Main` yöntemine aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-146">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a4fbd-147">`connectionString` değişkenini, ad alanını oluştururken elde ettiğiniz bağlantı dizesine, `topicName` değerini ise konuyu oluştururken kullandığınız ada ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-147">Set the `connectionString` variable to the connection string that you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a4fbd-148">Program.cs dosyanız aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-148">Here is what your Program.cs file should look like.</span></span>
   
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

                Console.WriteLine("Message successfully sent! Press ENTER to exit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="a4fbd-149">Programı çalıştırın ve Azure portalını denetleyin: Ad alanının **Genel Bakış** dikey penceresinde konunuzun adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-149">Run the program, and check the Azure portal: click the name of your topic in the namespace **Overview** blade.</span></span> <span data-ttu-id="a4fbd-150">Konunun **Temel Bileşenler** dikey penceresi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-150">The topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="a4fbd-151">Dikey pencerenin alt kısmının yanında listelenen aboneliklerde, her bir aboneliğin **İleti Sayısı** değerinin artık 1 olmasına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-151">In the subscription(s) listed near the bottom of the blade, notice that the **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="a4fbd-152">İletileri almadan gönderen uygulamasını her çalıştırdığınızda (sonraki bölümde açıklandığı gibi), bu değer 1 artar.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-152">Each time you run the sender application without retrieving the messages (as described in the next section), this value increases by 1.</span></span> <span data-ttu-id="a4fbd-153">Ayrıca, uygulamanın konuya/aboneliğe ileti eklediği her durumda konunun geçerli boyutu, **Temel Bileşenler** dikey penceresindeki **Geçerli** değerini artırır.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-153">Also note that the current size of the topic increments the **Current** value on the **Essentials** blade each time the app adds a message to the topic/subscription.</span></span>
   
      ![İleti boyutu][topic-message]

## <a name="5-receive-messages-from-the-subscription"></a><span data-ttu-id="a4fbd-155">5. Abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="a4fbd-155">5. Receive messages from the subscription</span></span>

1. <span data-ttu-id="a4fbd-156">Yeni gönderdiğiniz iletiyi veya iletileri almak için yeni bir konsol uygulaması oluşturun ve Service Bus NuGet paketine daha önceki gönderen uygulamasına benzer bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-156">To receive the message or messages you just sent, create a new console application and add a reference to the Service Bus NuGet package, similar to the previous sender application.</span></span>
2. <span data-ttu-id="a4fbd-157">Aşağıdaki `using` deyimini Program.cs dosyasının üst kısmına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-157">Add the following `using` statement to the top of the Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="a4fbd-158">`Main` yöntemine aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-158">Add the following code to the `Main` method.</span></span> <span data-ttu-id="a4fbd-159">`connectionString` değişkenini, ad alanını oluştururken elde ettiğiniz bağlantı dizesine, `topicName` değerini ise konuyu oluştururken kullandığınız ada ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-159">Set the `connectionString` variable to the connection string you obtained when creating the namespace, and set `topicName` to the name that you used when creating the topic.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER to exit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="a4fbd-160">Program.cs dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="a4fbd-160">Here is what your Program.cs file should look like:</span></span>
   
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

          Console.WriteLine("Press ENTER to exit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. <span data-ttu-id="a4fbd-161">Programı çalıştırın ve portalı tekrar denetleyin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-161">Run the program, and check the portal again.</span></span> <span data-ttu-id="a4fbd-162">**İleti Sayısı** ve **Geçerli** değerlerinin artık 0 olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-162">Notice that the **Message Count** and **Current** values are now 0.</span></span>
   
    ![Konu uzunluğu][topic-message-receive]

<span data-ttu-id="a4fbd-164">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="a4fbd-164">Congratulations!</span></span> <span data-ttu-id="a4fbd-165">Bir konu ve abonelik oluşturdunuz, ileti gönderdiniz ve bu iletiyi aldınız.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4fbd-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4fbd-166">Next steps</span></span>

<span data-ttu-id="a4fbd-167">Service Bus mesajlaşmasının daha gelişmiş özelliklerini gösteren [örneklerin bulunduğu GitHub depomuza](https://github.com/Azure/azure-service-bus/tree/master/samples) göz atın.</span><span class="sxs-lookup"><span data-stu-id="a4fbd-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of the more advanced features of Service Bus messaging.</span></span>

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
