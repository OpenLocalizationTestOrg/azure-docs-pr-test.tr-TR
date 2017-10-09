
Bu bölümde, son dakika haberleri olarak toosend şablon bildirimleri .NET konsol uygulamasından nasıl etiketli gösterir.

Mobile Apps kullanıyorsanız, lütfen toohello bakın [Mobile Apps için anında iletme bildirimleri ekleme] öğretici ve platformunuz hello üstünde seçin.

PHP başvurmak çok ya da toouse Java istiyorsanız[nasıl toouse Java/php'den Notification Hubs]. Tüm arka uç kullanımından bildirimleri gönderebilir [bildirim hub'ları REST arabirimini].

Atla tamamlandığında, bildirim göndermek için hello konsol uygulamasını oluşturduysanız, 1-3 adımları [Notification Hubs ile çalışmaya başlama].

1. Visual Studio'da yeni bir Visual C# konsol uygulaması oluşturun:
   
       ![][13]
2. Merhaba Visual Studio ana menüsünde tıklatın **Araçları**, **kitaplık Paket Yöneticisi**, ve **Paket Yöneticisi Konsolu**, ardından hello konsol penceresinde aşağıdaki komutu yazın ve tuşuna basın **Girin**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak [Microsoft.Azure.Notification Hubs NuGet paketini].
3. Program.cs Hello dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimi:
   
        using Microsoft.Azure.NotificationHubs;
4. Merhaba, `Program` sınıfı, yöntemi aşağıdaki hello eklemek veya zaten varsa değiştirin:
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define hello notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending hello notification as a template notification. All template registrations that contain
            // "messageParam" and hello proper tags will receive hello notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    Bu kodu her hello altı etiketler hello dize dizisi için bir şablon bildirim gönderir. etiketlerin Hello kullan cihazları bildirimlerin yalnızca kayıtlı hello kategorileri için emin olur.
5. Kod yukarıda Hello hello yerine `<hub name>` ve `<connection string with full access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultFullSharedAccessSignature* bildirim hub'ınızın hello panosundan .
6. Merhaba satırlarında aşağıdaki hello eklemek **ana** yöntemi:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Merhaba konsol uygulaması oluşturun.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Notification Hubs ile çalışmaya başlama]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[bildirim hub'ları REST arabirimini]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Mobile Apps için anında iletme bildirimleri ekleme]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[nasıl toouse Java/php'den Notification Hubs]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet paketini]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
