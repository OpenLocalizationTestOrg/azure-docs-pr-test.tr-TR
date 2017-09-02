
Bu bölümde, bir .NET konsol uygulamasından etiketli olarak şablon bildirimleri son dakika haberleri göndermek gösterilmiştir.

Mobile Apps kullanıyorsanız, lütfen [Mobile Apps için anında iletme bildirimleri ekleme] öğretici ve üst platformunuzu seçin.

PHP başvurun veya Java kullanmak istiyorsanız [Java/php'den Notification Hubs kullanma]. Tüm arka uç kullanımından bildirimleri gönderebilir [bildirim hub'ları REST arabirimini].

Atla tamamlandığında, bildirim göndermek için konsol uygulamasını oluşturduysanız, 1-3 adımları [Notification Hubs ile çalışmaya başlama].

1. Visual Studio'da yeni bir Visual C# konsol uygulaması oluşturun:
   
       ![][13]
2. Visual Studio ana menüye tıklayın **Araçları**, **kitaplık Paket Yöneticisi**, ve **Paket Yöneticisi Konsolu**, ardından konsol penceresinde aşağıdaki komutu yazın ve tuşunabasın **Girin**:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Bu, [Microsoft.Azure.Notification Hubs NuGet paketini] kullanarak Azure Notification Hubs SDK'sına bir başvuru ekler.
3. Program.cs dosyasını açın ve aşağıdakileri ekleyin `using` deyimi:
   
        using Microsoft.Azure.NotificationHubs;
4. İçinde `Program` sınıfı, aşağıdaki yöntemi ekleyin veya zaten varsa değiştirin:
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending the notification as a template notification. All template registrations that contain
            // "messageParam" and the proper tags will receive the notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    Bu kod, her bir dize dizisi altı etiketleri için bir şablon bildirim gönderir. Etiketler aygıtları bildirimlerin yalnızca kayıtlı kategorileri için emin olur.
5. Yukarıdaki kodla `<hub name>` ve `<connection string with full access>` , bildirim hub'ı adı ve bağlantı dizesinde yer tutucularını *DefaultFullSharedAccessSignature* bildirim hub'ınızın panosundan.
6. Aşağıdaki satırları **Main** yöntemine ekleyin:
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. Konsol uygulaması oluşturun.

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Notification Hubs ile çalışmaya başlama]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[bildirim hub'ları REST arabirimini]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Mobile Apps için anında iletme bildirimleri ekleme]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[Java/php'den Notification Hubs kullanma]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet paketini]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
