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
# <a name="enterprise-push-architectural-guidance"></a>Kurumsal gönderim mimari kılavuzu
Kuruluşlar bugün kademeli olarak mobil uygulamaları ya da kendi son kullanıcıları (harici) oluşturmak için doğru veya hello çalışanların (iç) geçiyor. Ana bilgisayarlar olması varolan arka uç sistemleri yerinde olması veya tümleştirilmiş gereken bazı iş kolu uygulamaları mobil uygulama mimarisi hello. Bu kılavuz hakkında en iyi nasıl toodo toocommon senaryoları olası çözüm öneren Bu tümleştirme konuşur.

Hello arka uç sistemleri ilgi bir olay meydana geldiğinde, anında iletme bildirimi toohello kullanıcılar kendi mobil uygulama üzerinden göndermek için sık gerekli değildir. Örneğin belirli bir miktar hesabını veya kendi Windows Phone bir bütçe onay uygulaması olan bir çalışanın Finans departmanından toobe burada istediği intranet senaryosu yukarıda borç yapıldığında bildirim toobe hello bankanın bankacılık uygulama kendi iPhone üzerinde sahip bir banka Müşterinin istediği kendisine bir onay isteği aldığında bildirim.

Merhaba banka hesabı veya onay işleme itme toohello kullanıcı başlatmalıdır bazı arka uç sisteminde yapılan büyük olasılıkla toobe değil. Bu tür birden fazla arka uç olabilir tüm oluşturmalısınız sistemlerini hello mantığı tooimplement itme aynı türde olduğunda bir bildirim bir olay tetikler. Son kullanıcılar toodifferent bildirimleri abone ve hatta olabilir hello intranet mobil uygulamaların hello durumda örneğin birden çok mobil uygulama olması yerde tek itme sistemiyle birlikte birkaç arka uç sistemleri tümleştirme burada Hello karmaşıklık arasındadır Burada bir mobil uygulama gibi birden fazla arka uç sistemleri tooreceive bildirimleri isteyebilirsiniz. Merhaba arka uç sistemleri bilmiyorsanız veya burada ortak bir çözüm geleneksel toointroduce hello arka uç sistemleri tüm olayları ilgi yokladığı ve Merhaba anında iletme iletileri göndermek için sorumlu olan bir bileşen olan için anında iletme semantiği/teknolojinin tooknow olması gerekir. toohello istemci.
Burada size Azure Service Bus - hello çözüm ölçeklenebilir yaparken hello karmaşıklığını azaltır konu başlığının/aboneliğinin modeli kullanarak daha iyi bir çözüm hakkında konuşur.

İşte hello genel hello çözüm mimarisini (birden çok mobil uygulamaları ile genelleştirilmiş ancak yalnızca bir mobil uygulama olduğunda eşit oranda geçerlidir)

## <a name="architecture"></a>Mimari
![][1]

Merhaba anahtar mimarisi Bu diyagramda parçasıdır programlama modeli konuları/abonelikleri sağlayan Azure Service Bus (adresinden hakkında daha fazla [Service Bus Pub/alt programlama]). Bu durumda, hello mobil arka uç olduğu hello alıcı (genellikle [Azure mobil hizmeti], hangi itme toohello mobil uygulamaları başlatmak) doğrudan hello arka uç sistemlerden iletilerini değil, ancak bunun yerine sahibiz bir tarafından sağlanan Ara Soyutlama Katmanı [Azure Service Bus] mobil arka uç tooreceive iletileri bir veya daha fazla arka uç sistemlerden sağlar. Hizmet veri yolu konusu her hello arka uç sistemleri Örneğin hesap, SA, temel olarak "" anında iletme bildirimi tarafından gönderilen iletileri toobe başlatacaktır ilgi konulardır Finans için oluşturulan toobe gerekir. Merhaba arka uç sistemleri toothese konuları gönderecek. Bir mobil arka uç tooone ya da daha fazla gibi konular, bir hizmet veri yolu abonelik oluşturarak abone olabilirsiniz. Bu hello mobil arka uç tooreceive hello karşılık gelen arka uç sisteminden bildirim entitle. Mobil arka uç toolisten iletileri için kendi aboneliklere ilişkin devam eder ve bir ileti ulaşır ulaşmaz geri kapatır ve bildirim tooits bildirim hub'ı olarak gönderir. Bildirim hub'ları sonra sonunda sunar hello ileti toohello mobil uygulama. Bu nedenle toosummarize hello anahtar bileşenleri, biz vardır:

1. Arka uç sistemleri (LoB/eski sistemler için)
   * Hizmet veri yolu konusu oluşturur
   * İleti gönderir
2. Mobil arka uç
   * Hizmet aboneliği oluşturur
   * İleti (arka uç sistemden) alır
   * Bildirim tooclients (aracılığıyla Azure bildirim hub'ı) gönderir
3. Mobil uygulama
   * Alır ve bildirim göster

### <a name="benefits"></a>Yararları:
1. Merhaba hello alıcı (mobil uygulama/hizmet bildirim hub'ı aracılığıyla) ve gönderen (arka uç sistemleri) arasında kesilmesi en az değişiklikle tümleştirilmekte ek arka uç sistemleri sağlar.
2. Bu da bir veya daha fazla arka uç sistemleri yapabilir tooreceive olaylarından olan birden çok mobil uygulama hello senaryo hale getirir.  

## <a name="sample"></a>Örnek:
### <a name="prerequisites"></a>Ön koşullar
Öğreticiler toofamiliarize hello kavramları ve bunun yanı sıra ortak oluşturma ve yapılandırma adımları izleyerek hello tamamlaması gerekir:

1. [Service Bus Pub/alt programlama] -bu çalışma ile hizmet veri yolu konuları/abonelikleri hello ayrıntılarını nasıl açıklanmaktadır toocreate bir ad alanı toocontain konuları/abonelikler, nasıl toosend & iletileri gönderdikleri.
2. [Notification Hubs - Windows Evrensel Öğreticisine] -bu nasıl tooset bir Windows mağazası uygulaması ve bildirim hub'ları tooregister kullanın ve ardından bildirimlerin açıklanmaktadır.

### <a name="sample-code"></a>Örnek kod
Merhaba tam örnek kod, şu adreste [bildirim Hub örnekleri]. Üç bileşenlerine ayrılır:

1. **EnterprisePushBackendSystem**
   
    a. Bu proje hello kullanıyor *WindowsAzure.ServiceBus* Nuget paketi ve dayanır [Service Bus Pub/alt programlama].
   
    b. Bir basit C# konsol uygulaması toosimulate toohello mobil uygulama teslim hello ileti toobe başlatan bir LoB sistem budur.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`kullanılan toocreate hello Service Bus konu iletileri burada göndereceğiz ' dir.
   
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
   
    d. `SendMessage`kullanılan toosend hello iletileri toothis hizmet veri yolu konusu değil. Burada size rastgele iletileri toohello konu hello örnek hello amacı için düzenli olarak bir dizi yalnızca gönderiyor. Normalde bir olay gerçekleştiğinde gönderecek bir arka uç sistemi olacaktır.
   
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
2. **ReceiveAndSendNotification**
   
    a. Bu proje hello kullanıyor *WindowsAzure.ServiceBus* ve *Microsoft.Web.WebJobs.Publish* Nuget paketleri ve dayanır [Service Bus Pub/alt programlama].
   
    b. Bu olarak çalışacak başka bir C# konsol uygulaması olan bir [Azure WebJob] toorun sürekli olduğundan hello LoB/arka uç sistemleri için toolisten iletileri. Bu, mobil arka uç parçası olacak.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`Merhaba arka uç sistem burada gönderecek bir Service Bus abonelik hello konu için kullanılan toocreate var. Merhaba iş senaryosu bağlı olarak bu bileşen toocorresponding konuları (örneğin bazı iletileri sisteminden HR bazı Finans sistem ve benzeri alıyor olabilir) bir veya daha fazla abonelik oluşturur
   
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
   
    d. ReceiveMessageAndSendNotification kullanılan tooread hello aboneliğini kullanarak hello konu iletisidir ve okuma hello başarılı olursa bildiriminde (Merhaba Örnek senaryo Windows yerel bildirim) gönderilen toobe toohello mobil oluşturabilir Azure bildirim hub'ları kullanarak uygulama.
   
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
   
    e. Bu olarak yayımlamak için bir **WebJob**, Visual Studio hello çözümüne sağ tıklayın ve seçin **Web işi olarak Yayımla**
   
    ![][2]
   
    f. Yayımlama profilinizi seçin ve bu Web işi barındıracak olan zaten yoksa ve ardından hello Web sitesini bulduktan sonra yeni bir Azure Web sitesi oluşturma **Yayımla**.
   
    ![][3]
   
    g. "Sürekli Çalıştır" Merhaba iş toobe toohello içinde oturum açtıklarında şekilde yapılandırmanız [Klasik Azure portalı] hello aşağıdaki gibi bir şey görmeniz gerekir:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. Mobil arka bir parçası olarak hello WebJob çalışmasını bildirimleri alır ve görüntüler bir Windows mağazası uygulaması budur. Bu temel alır [Notification Hubs - Windows Evrensel Öğreticisine].  
   
    b. Uygulamanızı etkin tooreceive bildirimleri olduğundan emin olun.
   
    c. Bildirim hub'ları kayıt koddan bu hello hello uygulama başlatma sırasında çağrılma emin olun (Merhaba değiştirildikten sonra *HubName* ve *DefaultListenSharedAccessSignature*:
   
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

### <a name="running-sample"></a>Örnek çalıştırma:
1. Web işi başarıyla çalıştığını ve zamanlanmış çok "sürekli olarak çalıştır" emin olun.
2. Merhaba çalıştırmak **EnterprisePushMobileApp** hello Windows mağazası uygulaması başlayacak.
3. Merhaba çalıştırmak **EnterprisePushBackendSystem** hello LoB arka benzetimini yapacak ve göndermeye başla konsol uygulaması iletileri ve hello aşağıdaki gibi görünen bildirimleri görmeniz gerekir:
   
    ![][5]
4. Merhaba iletileri ilk olarak Web işinizin Service Bus Aboneliklerde tarafından izlenen tooService veri yolu konuları gönderildi. Bir ileti alındığında bir bildirim oluşturuldu ve toohello mobil uygulama gönderilir. Web işi günlüklerini günlükleri bağlantı toohello olduğunuzda tooconfirm hello işleme hello aracılığıyla bakabilirsiniz [Klasik Azure portalı] Web işi için:
   
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
