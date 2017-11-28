
<span data-ttu-id="66721-101">Bu bölümde, bir .NET konsol uygulamasından etiketli olarak şablon bildirimleri son dakika haberleri göndermek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66721-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="66721-102">Mobile Apps kullanıyorsanız, lütfen [Mobile Apps için anında iletme bildirimleri ekleme] öğretici ve üst platformunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="66721-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span></span>

<span data-ttu-id="66721-103">PHP başvurun veya Java kullanmak istiyorsanız [Java/php'den Notification Hubs kullanma].</span><span class="sxs-lookup"><span data-stu-id="66721-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="66721-104">Tüm arka uç kullanımından bildirimleri gönderebilir [bildirim hub'ları REST arabirimini].</span><span class="sxs-lookup"><span data-stu-id="66721-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="66721-105">Atla tamamlandığında, bildirim göndermek için konsol uygulamasını oluşturduysanız, 1-3 adımları [Notification Hubs ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="66721-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="66721-106">Visual Studio'da yeni bir Visual C# konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="66721-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="66721-107">Visual Studio ana menüye tıklayın **Araçları**, **kitaplık Paket Yöneticisi**, ve **Paket Yöneticisi Konsolu**, ardından konsol penceresinde aşağıdaki komutu yazın ve tuşunabasın **Girin**:</span><span class="sxs-lookup"><span data-stu-id="66721-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="66721-108">Bu, [Microsoft.Azure.Notification Hubs NuGet paketini] kullanarak Azure Notification Hubs SDK'sına bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="66721-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="66721-109">Program.cs dosyasını açın ve aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="66721-109">Open the file Program.cs and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="66721-110">İçinde `Program` sınıfı, aşağıdaki yöntemi ekleyin veya zaten varsa değiştirin:</span><span class="sxs-lookup"><span data-stu-id="66721-110">In the `Program` class, add the following method, or replace it if it already exists:</span></span>
   
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
   
    <span data-ttu-id="66721-111">Bu kod, her bir dize dizisi altı etiketleri için bir şablon bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="66721-111">This code sends a template notification for each of the six tags in the string array.</span></span> <span data-ttu-id="66721-112">Etiketler aygıtları bildirimlerin yalnızca kayıtlı kategorileri için emin olur.</span><span class="sxs-lookup"><span data-stu-id="66721-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span></span>
5. <span data-ttu-id="66721-113">Yukarıdaki kodla `<hub name>` ve `<connection string with full access>` , bildirim hub'ı adı ve bağlantı dizesinde yer tutucularını *DefaultFullSharedAccessSignature* bildirim hub'ınızın panosundan.</span><span class="sxs-lookup"><span data-stu-id="66721-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span></span>
6. <span data-ttu-id="66721-114">Aşağıdaki satırları **Main** yöntemine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="66721-114">Add the following lines in the **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="66721-115">Konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66721-115">Build the console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
<span data-ttu-id="66721-116">[Notification Hubs ile çalışmaya başlama]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="66721-116">[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="66721-117">[bildirim hub'ları REST arabirimini]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span><span class="sxs-lookup"><span data-stu-id="66721-117">[Notification Hubs REST interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx</span></span>
<span data-ttu-id="66721-118">[Mobile Apps için anında iletme bildirimleri ekleme]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="66721-118">[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="66721-119">[Java/php'den Notification Hubs kullanma]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span><span class="sxs-lookup"><span data-stu-id="66721-119">[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md</span></span>
<span data-ttu-id="66721-120">[Microsoft.Azure.Notification Hubs NuGet paketini]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span><span class="sxs-lookup"><span data-stu-id="66721-120">[Microsoft.Azure.Notification Hubs NuGet package]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/</span></span>
