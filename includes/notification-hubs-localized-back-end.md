



Şablon bildirimleri tooprovide bir özellikler kümesi yeterlidir gönderdiğinizde, örneğimizde hello hello güncel haberleri yerelleştirilmiş sürümünü hello örneği için içeren özellikler kümesini göndereceğiz:

    {
        "News_English": "World News in English!",
        "News_French": "World News in French!",
        "News_Mandarin": "World News in Mandarin!"
    }


Bu bölümde gösterilmiştir nasıl bir konsol uygulaması kullanarak toosend bildirimleri

Hello arka uç tooany hello desteklenen aygıtların yayınlayabilirsiniz beri hello kod yayınları tooboth Windows mağazası ve iOS aygıtları dahil.

### <a name="toosend-notifications-using-a-c-console-app"></a>bir C# konsol uygulaması kullanarak toosend bildirimleri
Merhaba değiştirme `SendTemplateNotificationAsync` koddan hello ile daha önce oluşturduğunuz hello konsol uygulaması yöntemi. Nasıl bu durumda hiçbir gerek toosend farklı yerel ayarlara ve platformlar için birden fazla bildirim fark.

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


Bu basit aramayı hello yerelleştirilmiş haber parçası çok teslim eder Not**tüm** bildirim Hub'ınızı oluşturur ve teslim gibi hello platform yedeklemiş aygıtlarınızı doğru yerel yükü tooall hello aygıtları abone hello tooa belirli etiketi.

### <a name="sending-hello-notification-with-mobile-services"></a>Mobile Services Hello bildirim gönderme
Mobil Hizmeti Zamanlayıcı komut dosyası izleyen hello kullanabilirsiniz:

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


