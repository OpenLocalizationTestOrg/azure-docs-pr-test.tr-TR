---
title: "aaaNotification Hubs - kuruluş itme mimarisi"
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
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="e7846-103">Kurumsal gönderim mimari kılavuzu</span><span class="sxs-lookup"><span data-stu-id="e7846-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="e7846-104">Kuruluşlar bugün kademeli olarak mobil uygulamaları ya da kendi son kullanıcıları (harici) oluşturmak için doğru veya hello çalışanların (iç) geçiyor.</span><span class="sxs-lookup"><span data-stu-id="e7846-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="e7846-105">Ana bilgisayarlar olması varolan arka uç sistemleri yerinde olması veya tümleştirilmiş gereken bazı iş kolu uygulamaları mobil uygulama mimarisi hello.</span><span class="sxs-lookup"><span data-stu-id="e7846-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="e7846-106">Bu kılavuz hakkında en iyi nasıl toodo toocommon senaryoları olası çözüm öneren Bu tümleştirme konuşur.</span><span class="sxs-lookup"><span data-stu-id="e7846-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="e7846-107">Hello arka uç sistemleri ilgi bir olay meydana geldiğinde, anında iletme bildirimi toohello kullanıcılar kendi mobil uygulama üzerinden göndermek için sık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e7846-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="e7846-108">Örneğin</span><span class="sxs-lookup"><span data-stu-id="e7846-108">E.g.</span></span> <span data-ttu-id="e7846-109">belirli bir miktar hesabını veya kendi Windows Phone bir bütçe onay uygulaması olan bir çalışanın Finans departmanından toobe burada istediği intranet senaryosu yukarıda borç yapıldığında bildirim toobe hello bankanın bankacılık uygulama kendi iPhone üzerinde sahip bir banka Müşterinin istediği kendisine bir onay isteği aldığında bildirim.</span><span class="sxs-lookup"><span data-stu-id="e7846-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="e7846-110">Merhaba banka hesabı veya onay işleme itme toohello kullanıcı başlatmalıdır bazı arka uç sisteminde yapılan büyük olasılıkla toobe değil.</span><span class="sxs-lookup"><span data-stu-id="e7846-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="e7846-111">Bu tür birden fazla arka uç olabilir tüm oluşturmalısınız sistemlerini hello mantığı tooimplement itme aynı türde olduğunda bir bildirim bir olay tetikler.</span><span class="sxs-lookup"><span data-stu-id="e7846-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="e7846-112">Son kullanıcılar toodifferent bildirimleri abone ve hatta olabilir hello intranet mobil uygulamaların hello durumda örneğin birden çok mobil uygulama olması yerde tek itme sistemiyle birlikte birkaç arka uç sistemleri tümleştirme burada Hello karmaşıklık arasındadır Burada bir mobil uygulama gibi birden fazla arka uç sistemleri tooreceive bildirimleri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7846-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="e7846-113">Merhaba arka uç sistemleri bilmiyorsanız veya burada ortak bir çözüm geleneksel toointroduce hello arka uç sistemleri tüm olayları ilgi yokladığı ve Merhaba anında iletme iletileri göndermek için sorumlu olan bir bileşen olan için anında iletme semantiği/teknolojinin tooknow olması gerekir. toohello istemci.</span><span class="sxs-lookup"><span data-stu-id="e7846-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="e7846-114">Burada size Azure Service Bus - hello çözüm ölçeklenebilir yaparken hello karmaşıklığını azaltır konu başlığının/aboneliğinin modeli kullanarak daha iyi bir çözüm hakkında konuşur.</span><span class="sxs-lookup"><span data-stu-id="e7846-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="e7846-115">İşte hello genel hello çözüm mimarisini (birden çok mobil uygulamaları ile genelleştirilmiş ancak yalnızca bir mobil uygulama olduğunda eşit oranda geçerlidir)</span><span class="sxs-lookup"><span data-stu-id="e7846-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="e7846-116">Mimari</span><span class="sxs-lookup"><span data-stu-id="e7846-116">Architecture</span></span>
![][1]

<span data-ttu-id="e7846-117">Merhaba anahtar mimarisi Bu diyagramda parçasıdır programlama modeli konuları/abonelikleri sağlayan Azure Service Bus (adresinden hakkında daha fazla [Service Bus Pub/alt programlama]).</span><span class="sxs-lookup"><span data-stu-id="e7846-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="e7846-118">Bu durumda, hello mobil arka uç olduğu hello alıcı (genellikle [Azure mobil hizmeti], hangi itme toohello mobil uygulamaları başlatmak) doğrudan hello arka uç sistemlerden iletilerini değil, ancak bunun yerine sahibiz bir tarafından sağlanan Ara Soyutlama Katmanı [Azure Service Bus] mobil arka uç tooreceive iletileri bir veya daha fazla arka uç sistemlerden sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7846-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="e7846-119">Hizmet veri yolu konusu her hello arka uç sistemleri Örneğin hesap, SA, temel olarak "" anında iletme bildirimi tarafından gönderilen iletileri toobe başlatacaktır ilgi konulardır Finans için oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7846-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="e7846-120">Merhaba arka uç sistemleri toothese konuları gönderecek.</span><span class="sxs-lookup"><span data-stu-id="e7846-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="e7846-121">Bir mobil arka uç tooone ya da daha fazla gibi konular, bir hizmet veri yolu abonelik oluşturarak abone olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7846-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="e7846-122">Bu hello mobil arka uç tooreceive hello karşılık gelen arka uç sisteminden bildirim entitle.</span><span class="sxs-lookup"><span data-stu-id="e7846-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="e7846-123">Mobil arka uç toolisten iletileri için kendi aboneliklere ilişkin devam eder ve bir ileti ulaşır ulaşmaz geri kapatır ve bildirim tooits bildirim hub'ı olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="e7846-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="e7846-124">Bildirim hub'ları sonra sonunda sunar hello ileti toohello mobil uygulama.</span><span class="sxs-lookup"><span data-stu-id="e7846-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="e7846-125">Bu nedenle toosummarize hello anahtar bileşenleri, biz vardır:</span><span class="sxs-lookup"><span data-stu-id="e7846-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="e7846-126">Arka uç sistemleri (LoB/eski sistemler için)</span><span class="sxs-lookup"><span data-stu-id="e7846-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="e7846-127">Hizmet veri yolu konusu oluşturur</span><span class="sxs-lookup"><span data-stu-id="e7846-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="e7846-128">İleti gönderir</span><span class="sxs-lookup"><span data-stu-id="e7846-128">Sends Message</span></span>
2. <span data-ttu-id="e7846-129">Mobil arka uç</span><span class="sxs-lookup"><span data-stu-id="e7846-129">Mobile backend</span></span>
   * <span data-ttu-id="e7846-130">Hizmet aboneliği oluşturur</span><span class="sxs-lookup"><span data-stu-id="e7846-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="e7846-131">İleti (arka uç sistemden) alır</span><span class="sxs-lookup"><span data-stu-id="e7846-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="e7846-132">Bildirim tooclients (aracılığıyla Azure bildirim hub'ı) gönderir</span><span class="sxs-lookup"><span data-stu-id="e7846-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="e7846-133">Mobil uygulama</span><span class="sxs-lookup"><span data-stu-id="e7846-133">Mobile Application</span></span>
   * <span data-ttu-id="e7846-134">Alır ve bildirim göster</span><span class="sxs-lookup"><span data-stu-id="e7846-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="e7846-135">Yararları:</span><span class="sxs-lookup"><span data-stu-id="e7846-135">Benefits:</span></span>
1. <span data-ttu-id="e7846-136">Merhaba hello alıcı (mobil uygulama/hizmet bildirim hub'ı aracılığıyla) ve gönderen (arka uç sistemleri) arasında kesilmesi en az değişiklikle tümleştirilmekte ek arka uç sistemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7846-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="e7846-137">Bu da bir veya daha fazla arka uç sistemleri yapabilir tooreceive olaylarından olan birden çok mobil uygulama hello senaryo hale getirir.</span><span class="sxs-lookup"><span data-stu-id="e7846-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="e7846-138">Örnek:</span><span class="sxs-lookup"><span data-stu-id="e7846-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="e7846-139">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e7846-139">Prerequisites</span></span>
<span data-ttu-id="e7846-140">Öğreticiler toofamiliarize hello kavramları ve bunun yanı sıra ortak oluşturma ve yapılandırma adımları izleyerek hello tamamlaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7846-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="e7846-141">[Service Bus Pub/alt programlama] -bu çalışma ile hizmet veri yolu konuları/abonelikleri hello ayrıntılarını nasıl açıklanmaktadır toocreate bir ad alanı toocontain konuları/abonelikler, nasıl toosend & iletileri gönderdikleri.</span><span class="sxs-lookup"><span data-stu-id="e7846-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="e7846-142">[Notification Hubs - Windows Evrensel Öğreticisine] -bu nasıl tooset bir Windows mağazası uygulaması ve bildirim hub'ları tooregister kullanın ve ardından bildirimlerin açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e7846-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="e7846-143">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="e7846-143">Sample code</span></span>
<span data-ttu-id="e7846-144">Merhaba tam örnek kod, şu adreste [bildirim Hub örnekleri].</span><span class="sxs-lookup"><span data-stu-id="e7846-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="e7846-145">Üç bileşenlerine ayrılır:</span><span class="sxs-lookup"><span data-stu-id="e7846-145">It is split into three components:</span></span>

1. <span data-ttu-id="e7846-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="e7846-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="e7846-147">a.</span><span class="sxs-lookup"><span data-stu-id="e7846-147">a.</span></span> <span data-ttu-id="e7846-148">Bu proje hello kullanıyor *WindowsAzure.ServiceBus* Nuget paketi ve dayanır [Service Bus Pub/alt programlama].</span><span class="sxs-lookup"><span data-stu-id="e7846-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="e7846-149">b.</span><span class="sxs-lookup"><span data-stu-id="e7846-149">b.</span></span> <span data-ttu-id="e7846-150">Bir basit C# konsol uygulaması toosimulate toohello mobil uygulama teslim hello ileti toobe başlatan bir LoB sistem budur.</span><span class="sxs-lookup"><span data-stu-id="e7846-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="e7846-151">c.</span><span class="sxs-lookup"><span data-stu-id="e7846-151">c.</span></span> <span data-ttu-id="e7846-152">`CreateTopic`kullanılan toocreate hello Service Bus konu iletileri burada göndereceğiz ' dir.</span><span class="sxs-lookup"><span data-stu-id="e7846-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="e7846-153">d.</span><span class="sxs-lookup"><span data-stu-id="e7846-153">d.</span></span> <span data-ttu-id="e7846-154">`SendMessage`kullanılan toosend hello iletileri toothis hizmet veri yolu konusu değil.</span><span class="sxs-lookup"><span data-stu-id="e7846-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="e7846-155">Burada size rastgele iletileri toohello konu hello örnek hello amacı için düzenli olarak bir dizi yalnızca gönderiyor.</span><span class="sxs-lookup"><span data-stu-id="e7846-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="e7846-156">Normalde bir olay gerçekleştiğinde gönderecek bir arka uç sistemi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e7846-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
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
2. <span data-ttu-id="e7846-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="e7846-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="e7846-158">a.</span><span class="sxs-lookup"><span data-stu-id="e7846-158">a.</span></span> <span data-ttu-id="e7846-159">Bu proje hello kullanıyor *WindowsAzure.ServiceBus* ve *Microsoft.Web.WebJobs.Publish* Nuget paketleri ve dayanır [Service Bus Pub/alt programlama].</span><span class="sxs-lookup"><span data-stu-id="e7846-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="e7846-160">b.</span><span class="sxs-lookup"><span data-stu-id="e7846-160">b.</span></span> <span data-ttu-id="e7846-161">Bu olarak çalışacak başka bir C# konsol uygulaması olan bir [Azure WebJob] toorun sürekli olduğundan hello LoB/arka uç sistemleri için toolisten iletileri.</span><span class="sxs-lookup"><span data-stu-id="e7846-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="e7846-162">Bu, mobil arka uç parçası olacak.</span><span class="sxs-lookup"><span data-stu-id="e7846-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="e7846-163">c.</span><span class="sxs-lookup"><span data-stu-id="e7846-163">c.</span></span> <span data-ttu-id="e7846-164">`CreateSubscription`Merhaba arka uç sistem burada gönderecek bir Service Bus abonelik hello konu için kullanılan toocreate var.</span><span class="sxs-lookup"><span data-stu-id="e7846-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="e7846-165">Merhaba iş senaryosu bağlı olarak bu bileşen toocorresponding konuları (örneğin bazı iletileri sisteminden HR bazı Finans sistem ve benzeri alıyor olabilir) bir veya daha fazla abonelik oluşturur</span><span class="sxs-lookup"><span data-stu-id="e7846-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="e7846-166">d.</span><span class="sxs-lookup"><span data-stu-id="e7846-166">d.</span></span> <span data-ttu-id="e7846-167">ReceiveMessageAndSendNotification kullanılan tooread hello aboneliğini kullanarak hello konu iletisidir ve okuma hello başarılı olursa bildiriminde (Merhaba Örnek senaryo Windows yerel bildirim) gönderilen toobe toohello mobil oluşturabilir Azure bildirim hub'ları kullanarak uygulama.</span><span class="sxs-lookup"><span data-stu-id="e7846-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
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
   
    <span data-ttu-id="e7846-168">e.</span><span class="sxs-lookup"><span data-stu-id="e7846-168">e.</span></span> <span data-ttu-id="e7846-169">Bu olarak yayımlamak için bir **WebJob**, Visual Studio hello çözümüne sağ tıklayın ve seçin **Web işi olarak Yayımla**</span><span class="sxs-lookup"><span data-stu-id="e7846-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="e7846-170">f.</span><span class="sxs-lookup"><span data-stu-id="e7846-170">f.</span></span> <span data-ttu-id="e7846-171">Yayımlama profilinizi seçin ve bu Web işi barındıracak olan zaten yoksa ve ardından hello Web sitesini bulduktan sonra yeni bir Azure Web sitesi oluşturma **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e7846-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="e7846-172">g.</span><span class="sxs-lookup"><span data-stu-id="e7846-172">g.</span></span> <span data-ttu-id="e7846-173">"Sürekli Çalıştır" Merhaba iş toobe toohello içinde oturum açtıklarında şekilde yapılandırmanız [Klasik Azure portalı] hello aşağıdaki gibi bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7846-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="e7846-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="e7846-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="e7846-175">a.</span><span class="sxs-lookup"><span data-stu-id="e7846-175">a.</span></span> <span data-ttu-id="e7846-176">Mobil arka bir parçası olarak hello WebJob çalışmasını bildirimleri alır ve görüntüler bir Windows mağazası uygulaması budur.</span><span class="sxs-lookup"><span data-stu-id="e7846-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="e7846-177">Bu temel alır [Notification Hubs - Windows Evrensel Öğreticisine].</span><span class="sxs-lookup"><span data-stu-id="e7846-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="e7846-178">b.</span><span class="sxs-lookup"><span data-stu-id="e7846-178">b.</span></span> <span data-ttu-id="e7846-179">Uygulamanızı etkin tooreceive bildirimleri olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e7846-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="e7846-180">c.</span><span class="sxs-lookup"><span data-stu-id="e7846-180">c.</span></span> <span data-ttu-id="e7846-181">Bildirim hub'ları kayıt koddan bu hello hello uygulama başlatma sırasında çağrılma emin olun (Merhaba değiştirildikten sonra *HubName* ve *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="e7846-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="e7846-182">Örnek çalıştırma:</span><span class="sxs-lookup"><span data-stu-id="e7846-182">Running sample:</span></span>
1. <span data-ttu-id="e7846-183">Web işi başarıyla çalıştığını ve zamanlanmış çok "sürekli olarak çalıştır" emin olun.</span><span class="sxs-lookup"><span data-stu-id="e7846-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="e7846-184">Merhaba çalıştırmak **EnterprisePushMobileApp** hello Windows mağazası uygulaması başlayacak.</span><span class="sxs-lookup"><span data-stu-id="e7846-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="e7846-185">Merhaba çalıştırmak **EnterprisePushBackendSystem** hello LoB arka benzetimini yapacak ve göndermeye başla konsol uygulaması iletileri ve hello aşağıdaki gibi görünen bildirimleri görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e7846-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="e7846-186">Merhaba iletileri ilk olarak Web işinizin Service Bus Aboneliklerde tarafından izlenen tooService veri yolu konuları gönderildi.</span><span class="sxs-lookup"><span data-stu-id="e7846-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="e7846-187">Bir ileti alındığında bir bildirim oluşturuldu ve toohello mobil uygulama gönderilir.</span><span class="sxs-lookup"><span data-stu-id="e7846-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="e7846-188">Web işi günlüklerini günlükleri bağlantı toohello olduğunuzda tooconfirm hello işleme hello aracılığıyla bakabilirsiniz [Klasik Azure portalı] Web işi için:</span><span class="sxs-lookup"><span data-stu-id="e7846-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[bildirim Hub örnekleri]: https://github.com/Azure/azure-notificationhubs-samples
[Azure mobil hizmeti]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[Service Bus Pub/alt programlama]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Notification Hubs - Windows Evrensel Öğreticisine]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[Klasik Azure portalı]: https://manage.windowsazure.com/
