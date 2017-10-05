---
title: "Notification Hubs - kuruluş anında iletme mimarisi"
description: "Bir kuruluş ortamında Azure Notification Hubs kullanma yönergeleri"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="bc617-103">Kurumsal gönderim mimari kılavuzu</span><span class="sxs-lookup"><span data-stu-id="bc617-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="bc617-104">Kuruluşlar bugün kademeli olarak mobil uygulamaları ya da kendi son kullanıcıları (harici) oluşturmak için doğru veya (iç) çalışanlar için geçiyor.</span><span class="sxs-lookup"><span data-stu-id="bc617-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="bc617-105">Ana bilgisayarlar veya mobil uygulama mimariye tümleşik bazı iş kolu uygulamaları olması varolan arka uç sistemleri yerinde sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="bc617-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="bc617-106">Bu kılavuz, bu tümleştirme senaryoları için olası çözüm öneren yapmak en iyi nasıl hakkında konuşur.</span><span class="sxs-lookup"><span data-stu-id="bc617-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="bc617-107">Arka uç sistemleri ilgi bir olay meydana geldiğinde anında iletme bildirimi kendi mobil uygulama aracılığıyla kullanıcılara göndermek için sık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="bc617-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="bc617-108">Örneğin</span><span class="sxs-lookup"><span data-stu-id="bc617-108">E.g.</span></span> <span data-ttu-id="bc617-109">kendi iPhone üzerinde bankanın bankacılık uygulama olan banka müşteriye borç belirli bir miktar hesabını veya burada kendi Windows Phone bir bütçe onay uygulaması olan bir çalışanın Finans departmanından kendisine bir onay isteği aldığında bildirim almak isteyen bir intranet senaryosu yukarıda yapıldığında bildirilmesini istiyor.</span><span class="sxs-lookup"><span data-stu-id="bc617-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="bc617-110">Banka hesabı veya onay işleme kullanıcı için bir itme başlatmalıdır bazı arka uç sistemi yapılması olasıdır.</span><span class="sxs-lookup"><span data-stu-id="bc617-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="bc617-111">Tüm olay bildirim harekete geçirdiğinde itme uygulamak için mantığı aynı türde oluşturmalısınız gibi birden fazla arka uç sistemler olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc617-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="bc617-112">Burada son kullanıcıların farklı bildirimlerine abone ve hatta olabilir örneğin intranet mobil uygulamalar olması durumunda birden çok mobil uygulama burada bir mobil uygulama bildirimleri gibi birden fazla arka uç sistemlerden almak isteyebilirsiniz tek itme sistemiyle birlikte birkaç arka uç sistemleri tümleştirme karmaşıklık burada arasındadır.</span><span class="sxs-lookup"><span data-stu-id="bc617-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="bc617-113">Arka uç sistemleri bilmiyorsanız veya burada ortak bir çözüm geleneksel herhangi olaylarının için arka uç sistemleri yoklar ve istemciye anında iletme iletileri göndermek için sorumlu olan bir bileşen tanıtmak için bırakıldı şekilde itme semantiği/teknolojisini bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc617-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="bc617-114">Burada size Azure Service Bus - çözüm ölçeklenebilir yaparken karmaşıklığını azaltır konu başlığının/aboneliğinin modeli kullanarak daha iyi bir çözüm hakkında konuşur.</span><span class="sxs-lookup"><span data-stu-id="bc617-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="bc617-115">İşte çözümünün genel mimari (birden çok mobil uygulamaları ile genelleştirilmiş ancak yalnızca bir mobil uygulama olduğunda eşit oranda geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="bc617-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="bc617-116">Mimari</span><span class="sxs-lookup"><span data-stu-id="bc617-116">Architecture</span></span>
![][1]

<span data-ttu-id="bc617-117">Anahtar mimarisi Bu diyagramda programlama modeli konuları/abonelikleri sağlayan Azure Service Bus parçasıdır (adresinden hakkında daha fazla [Service Bus Pub/alt programlama]).</span><span class="sxs-lookup"><span data-stu-id="bc617-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="bc617-118">Bu durumda, mobil arka uç olduğundan alıcı (genellikle [Azure mobil hizmeti], hangi mobil uygulamalara push başlatmak) doğrudan arka uç sistemlerden iletilerini değil, ancak bunun yerine biz tarafından sağlanan bir ara Soyutlama Katmanı sahip [Azure Service Bus] bir veya daha fazla arka uç sistemlerinden iletileri almak mobil arka uç sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc617-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="bc617-119">Hizmet veri yolu konusu her arka uç sistemleri Örneğin hesap, SA, temel olarak "" anında iletme bildirimi gönderilecek iletilerin başlatacaktır ilgi konulardır Finans oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc617-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="bc617-120">Arka uç sistemleri bu konulara gönderecek.</span><span class="sxs-lookup"><span data-stu-id="bc617-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="bc617-121">Bir mobil arka uç, bir hizmet veri yolu abonelik oluşturarak bir veya daha fazla gibi konular için abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc617-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="bc617-122">Bu, karşılık gelen arka uç sistemden bir bildirim almak için mobil arka uç entitle.</span><span class="sxs-lookup"><span data-stu-id="bc617-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="bc617-123">Aboneliği iletilerde dinlemek mobil arka uç devam eder ve bir ileti ulaşır ulaşmaz geri kapatır ve kendi bildirim hub'ına bildirimi olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="bc617-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="bc617-124">Bildirim hub'ları sonra sonunda sunar ileti mobil uygulamaya.</span><span class="sxs-lookup"><span data-stu-id="bc617-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="bc617-125">Bu nedenle anahtar bileşenleri özetlemek için biz vardır:</span><span class="sxs-lookup"><span data-stu-id="bc617-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="bc617-126">Arka uç sistemleri (LoB/eski sistemler için)</span><span class="sxs-lookup"><span data-stu-id="bc617-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="bc617-127">Hizmet veri yolu konusu oluşturur</span><span class="sxs-lookup"><span data-stu-id="bc617-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="bc617-128">İleti gönderir</span><span class="sxs-lookup"><span data-stu-id="bc617-128">Sends Message</span></span>
2. <span data-ttu-id="bc617-129">Mobil arka uç</span><span class="sxs-lookup"><span data-stu-id="bc617-129">Mobile backend</span></span>
   * <span data-ttu-id="bc617-130">Hizmet aboneliği oluşturur</span><span class="sxs-lookup"><span data-stu-id="bc617-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="bc617-131">İleti (arka uç sistemden) alır</span><span class="sxs-lookup"><span data-stu-id="bc617-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="bc617-132">İstemciler (aracılığıyla Azure bildirim hub'ı) bildirim gönderir</span><span class="sxs-lookup"><span data-stu-id="bc617-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="bc617-133">Mobil uygulama</span><span class="sxs-lookup"><span data-stu-id="bc617-133">Mobile Application</span></span>
   * <span data-ttu-id="bc617-134">Alır ve bildirim göster</span><span class="sxs-lookup"><span data-stu-id="bc617-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="bc617-135">Yararları:</span><span class="sxs-lookup"><span data-stu-id="bc617-135">Benefits:</span></span>
1. <span data-ttu-id="bc617-136">Alıcı (mobil uygulama/hizmet bildirim hub'ı aracılığıyla) ve gönderen (arka uç sistemleri) arasında kesilmesi en az değişiklikle tümleştirilmekte ek arka uç sistemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc617-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="bc617-137">Bu da bir veya daha fazla arka uç sistemlerden olaylarını almak için birden çok mobil uygulama senaryo hale getirir.</span><span class="sxs-lookup"><span data-stu-id="bc617-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="bc617-138">Örnek:</span><span class="sxs-lookup"><span data-stu-id="bc617-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="bc617-139">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bc617-139">Prerequisites</span></span>
<span data-ttu-id="bc617-140">Kavramları yanı sıra ortak oluşturma ve yapılandırma adımları hakkında bilgi edinmek için aşağıdaki öğreticileri tamamlaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc617-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="bc617-141">[Service Bus Pub/alt programlama] -bu hizmet veri yolu konuları/abonelikleri ile çalışma ayrıntılarını açıklanmaktadır konuları/abonelikleri içerecek şekilde bir ad alanı oluşturmak nasıl nasıl iletileri gönderdikleri & Gönder.</span><span class="sxs-lookup"><span data-stu-id="bc617-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="bc617-142">[Notification Hubs - Windows Evrensel Öğreticisine] -bu bir Windows mağazası uygulama ayarlama ve kaydetme ve bildirimleri almak için bildirim hub'ları nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="bc617-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="bc617-143">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="bc617-143">Sample code</span></span>
<span data-ttu-id="bc617-144">Tam örnek kod şu adresten edinilebilir [bildirim Hub örnekleri].</span><span class="sxs-lookup"><span data-stu-id="bc617-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="bc617-145">Üç bileşenlerine ayrılır:</span><span class="sxs-lookup"><span data-stu-id="bc617-145">It is split into three components:</span></span>

1. <span data-ttu-id="bc617-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="bc617-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="bc617-147">a.</span><span class="sxs-lookup"><span data-stu-id="bc617-147">a.</span></span> <span data-ttu-id="bc617-148">Bu proje kullanıyor *WindowsAzure.ServiceBus* Nuget paketi ve dayanır [Service Bus Pub/alt programlama].</span><span class="sxs-lookup"><span data-stu-id="bc617-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="bc617-149">b.</span><span class="sxs-lookup"><span data-stu-id="bc617-149">b.</span></span> <span data-ttu-id="bc617-150">Mobil uygulama teslim edilecek ileti başlatan bir LoB sistem benzetimini yapmak için bir basit C# konsol uygulaması budur.</span><span class="sxs-lookup"><span data-stu-id="bc617-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="bc617-151">c.</span><span class="sxs-lookup"><span data-stu-id="bc617-151">c.</span></span> <span data-ttu-id="bc617-152">`CreateTopic`Service Bus konu oluşturmak için iletileri burada göndereceğiz kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc617-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="bc617-153">d.</span><span class="sxs-lookup"><span data-stu-id="bc617-153">d.</span></span> <span data-ttu-id="bc617-154">`SendMessage`Bu hizmet veri yolu konusu iletileri göndermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc617-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="bc617-155">Burada biz bir dizi rastgele ileti konusuna örnek amacıyla düzenli aralıklarla yalnızca gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="bc617-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="bc617-156">Normalde bir olay gerçekleştiğinde gönderecek bir arka uç sistemi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="bc617-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="bc617-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="bc617-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="bc617-158">a.</span><span class="sxs-lookup"><span data-stu-id="bc617-158">a.</span></span> <span data-ttu-id="bc617-159">Bu proje kullanıyor *WindowsAzure.ServiceBus* ve *Microsoft.Web.WebJobs.Publish* Nuget paketleri ve dayanır [Service Bus Pub/alt programlama].</span><span class="sxs-lookup"><span data-stu-id="bc617-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="bc617-160">b.</span><span class="sxs-lookup"><span data-stu-id="bc617-160">b.</span></span> <span data-ttu-id="bc617-161">Bu olarak çalışacak başka bir C# konsol uygulaması olan bir [Azure WebJob] LoB/arka uç sistemleri iletilerden dinlemek için sürekli çalışacak şekilde olduğundan.</span><span class="sxs-lookup"><span data-stu-id="bc617-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="bc617-162">Bu, mobil arka uç parçası olacak.</span><span class="sxs-lookup"><span data-stu-id="bc617-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="bc617-163">c.</span><span class="sxs-lookup"><span data-stu-id="bc617-163">c.</span></span> <span data-ttu-id="bc617-164">`CreateSubscription`konu için bir hizmet veri yolu aboneliği oluşturmak için arka uç sistem burada gönderecek kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc617-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="bc617-165">İş senaryosu bağlı olarak bu bileşen (örneğin bazı iletileri sisteminden HR bazı Finans sistem ve benzeri alıyor olabilir) ilgili konular için bir veya daha fazla abonelik oluşturur</span><span class="sxs-lookup"><span data-stu-id="bc617-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="bc617-166">d.</span><span class="sxs-lookup"><span data-stu-id="bc617-166">d.</span></span> <span data-ttu-id="bc617-167">ReceiveMessageAndSendNotification aboneliğini kullanarak konusundan iletisini okuyun ve okuma başarılı olursa sonra bir bildirim (senaryoda örnek Windows yerel bildirim) Azure bildirim hub'ları kullanarak mobil uygulamaya gönderilmek üzere oluşturabilir için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bc617-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="bc617-168">e.</span><span class="sxs-lookup"><span data-stu-id="bc617-168">e.</span></span> <span data-ttu-id="bc617-169">Bu olarak yayımlamak için bir **WebJob**, Visual Studio çözümüne sağ tıklayın ve seçin **Web işi olarak Yayımla**</span><span class="sxs-lookup"><span data-stu-id="bc617-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="bc617-170">f.</span><span class="sxs-lookup"><span data-stu-id="bc617-170">f.</span></span> <span data-ttu-id="bc617-171">Yayımlama profilinizi seçin ve bu Web işi barındıracak olan zaten yoksa ve ardından Web sitesini bulduktan sonra yeni bir Azure Web sitesi oluşturma **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="bc617-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="bc617-172">g.</span><span class="sxs-lookup"><span data-stu-id="bc617-172">g.</span></span> <span data-ttu-id="bc617-173">Böylece zaman oturum "Sürekli Çalıştır" olarak iş yapılandırma [Klasik Azure portalı] aşağıdaki gibi bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc617-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="bc617-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="bc617-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="bc617-175">a.</span><span class="sxs-lookup"><span data-stu-id="bc617-175">a.</span></span> <span data-ttu-id="bc617-176">Mobil arka bir parçası olarak çalışan Web işi bildirimleri almak ve görüntüleme bir Windows mağazası uygulaması budur.</span><span class="sxs-lookup"><span data-stu-id="bc617-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="bc617-177">Bu temel alır [Notification Hubs - Windows Evrensel Öğreticisine].</span><span class="sxs-lookup"><span data-stu-id="bc617-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="bc617-178">b.</span><span class="sxs-lookup"><span data-stu-id="bc617-178">b.</span></span> <span data-ttu-id="bc617-179">Uygulamanızı bildirim almaya etkinleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc617-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="bc617-180">c.</span><span class="sxs-lookup"><span data-stu-id="bc617-180">c.</span></span> <span data-ttu-id="bc617-181">Kayıt kodu uygulamaya çağrılma aşağıdaki Notification Hubs zaman başlatıldığından emin olun (değiştirildikten sonra *HubName* ve *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="bc617-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="bc617-182">Örnek çalıştırma:</span><span class="sxs-lookup"><span data-stu-id="bc617-182">Running sample:</span></span>
1. <span data-ttu-id="bc617-183">Web işi başarıyla çalıştığından ve "Çalıştır kesintisiz olarak" zamanlanmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc617-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="bc617-184">Çalıştırma **EnterprisePushMobileApp** Windows mağazası uygulaması başlayacak.</span><span class="sxs-lookup"><span data-stu-id="bc617-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="bc617-185">Çalıştırma **EnterprisePushBackendSystem** LoB arka benzetimini yapacak ve göndermeye başla konsol uygulaması iletileri ve aşağıdaki gibi görünen bildirimleri görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc617-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="bc617-186">İletileri, ilk olarak Web işinizin Service Bus Aboneliklerde tarafından izlenen Service Bus konu başlıklarını gönderildi.</span><span class="sxs-lookup"><span data-stu-id="bc617-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="bc617-187">Bir ileti alındığında bir bildirim oluşturuldu ve mobil uygulamaya gönderilir.</span><span class="sxs-lookup"><span data-stu-id="bc617-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="bc617-188">İşlem günlükleri bağlantıyı gittiğinizde onaylamak için Web işi günlükleri aracılığıyla bakabilirsiniz [Klasik Azure portalı] Web işi için:</span><span class="sxs-lookup"><span data-stu-id="bc617-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="bc617-189">[bildirim Hub örnekleri]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="bc617-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="bc617-190">[Azure mobil hizmeti]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="bc617-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="bc617-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="bc617-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="bc617-192">[Service Bus Pub/alt programlama]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="bc617-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="bc617-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="bc617-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="bc617-194">[Notification Hubs - Windows Evrensel Öğreticisine]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="bc617-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="bc617-195">[Klasik Azure portalı]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="bc617-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
