



<span data-ttu-id="874b9-101">Şablon bildirimleri tooprovide bir özellikler kümesi yeterlidir gönderdiğinizde, örneğimizde hello hello güncel haberleri yerelleştirilmiş sürümünü hello örneği için içeren özellikler kümesini göndereceğiz:</span><span class="sxs-lookup"><span data-stu-id="874b9-101">When you send template notifications you only need tooprovide a set of properties, in our case we will send hello set of properties containing hello localized version of hello current news, for instance:</span></span>

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


<span data-ttu-id="874b9-102">Bu bölümde gösterilmiştir nasıl bir konsol uygulaması kullanarak toosend bildirimleri</span><span class="sxs-lookup"><span data-stu-id="874b9-102">This section shows how toosend notifications using a console app</span></span>

<span data-ttu-id="874b9-103">Hello arka uç tooany hello desteklenen aygıtların yayınlayabilirsiniz beri hello kod yayınları tooboth Windows mağazası ve iOS aygıtları dahil.</span><span class="sxs-lookup"><span data-stu-id="874b9-103">hello included code broadcasts tooboth Windows Store and iOS devices, since hello backend can broadcast tooany of hello supported devices.</span></span>

### <a name="toosend-notifications-using-a-c-console-app"></a><span data-ttu-id="874b9-104">bir C# konsol uygulaması kullanarak toosend bildirimleri</span><span class="sxs-lookup"><span data-stu-id="874b9-104">toosend notifications using a C# console app</span></span>
<span data-ttu-id="874b9-105">Merhaba değiştirme `SendTemplateNotificationAsync` koddan hello ile daha önce oluşturduğunuz hello konsol uygulaması yöntemi.</span><span class="sxs-lookup"><span data-stu-id="874b9-105">Modify hello `SendTemplateNotificationAsync` method in hello console app you previously created with hello following code.</span></span> <span data-ttu-id="874b9-106">Nasıl bu durumda hiçbir gerek toosend farklı yerel ayarlara ve platformlar için birden fazla bildirim fark.</span><span class="sxs-lookup"><span data-stu-id="874b9-106">Notice how in this case there is no need toosend multiple notifications for different locales and platforms.</span></span>

        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub = 
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");

            // Sending hello notification as a template notification. All template registrations that contain 
            // "messageParam" or "News_<local selected>" and hello proper tags will receive hello notifications. 
            // This includes APNS, GCM, WNS, and MPNS template registrations.
            Dictionary<string, string> templateParams = new Dictionary<string, string>();

            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business", "Technology", "Science", "Sports"};
            var locales = new string[] { "English", "French", "Mandarin" };

            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";

                // Sending localized News for each tag too...
                foreach( var locale in locales)
                {
                    string key = "News_" + locale;

                    // Your real localized news content would go here.
                    templateParams[key] = "Breaking " + category + " News in " + locale + "!";
                }

                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
        }


<span data-ttu-id="874b9-107">Bu basit aramayı hello yerelleştirilmiş haber parçası çok teslim eder Not**tüm** bildirim Hub'ınızı oluşturur ve teslim gibi hello platform yedeklemiş aygıtlarınızı doğru yerel yükü tooall hello aygıtları abone hello tooa belirli etiketi.</span><span class="sxs-lookup"><span data-stu-id="874b9-107">Note that this simple call will deliver hello localized piece of news too**all** your devices, irrespective of hello platform, as your Notification Hub builds and delivers hello correct native payload tooall hello devices subscribed tooa specific tag.</span></span>

### <a name="sending-hello-notification-with-mobile-services"></a><span data-ttu-id="874b9-108">Mobile Services Hello bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="874b9-108">Sending hello notification with Mobile Services</span></span>
<span data-ttu-id="874b9-109">Mobil Hizmeti Zamanlayıcı komut dosyası izleyen hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="874b9-109">In your Mobile Service scheduler, you can use hello following script:</span></span>

    var azure = require('azure');
    var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string with full access>');
    var notification = {
            "News_English": "World News in English!",
            "News_French": "World News in French!",
            "News_Mandarin", "World News in Mandarin!"
    }
    notificationHubService.send('World', notification, function(error) {
        if (!error) {
            console.warn("Notification successful");
        }
    });


