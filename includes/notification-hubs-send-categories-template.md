
<span data-ttu-id="1cc6c-101">Bu bölümde, son dakika haberleri olarak toosend şablon bildirimleri .NET konsol uygulamasından nasıl etiketli gösterir.</span><span class="sxs-lookup"><span data-stu-id="1cc6c-101">This section shows how toosend breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="1cc6c-102">Mobile Apps kullanıyorsanız, lütfen toohello bakın [Mobile Apps için anında iletme bildirimleri ekleme] öğretici ve platformunuz hello üstünde seçin.</span><span class="sxs-lookup"><span data-stu-id="1cc6c-102">If you are using Mobile Apps please refer toohello [Add push notifications for Mobile Apps] tutorial and select your platform at hello top.</span></span>

<span data-ttu-id="1cc6c-103">PHP başvurmak çok ya da toouse Java istiyorsanız[nasıl toouse Java/php'den Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="1cc6c-103">If you want toouse Java or PHP refer too[How toouse Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="1cc6c-104">Tüm arka uç kullanımından bildirimleri gönderebilir [bildirim hub'ları REST arabirimini].</span><span class="sxs-lookup"><span data-stu-id="1cc6c-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="1cc6c-105">Atla tamamlandığında, bildirim göndermek için hello konsol uygulamasını oluşturduysanız, 1-3 adımları [Notification Hubs ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="1cc6c-105">Skip steps 1-3 if you created hello console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="1cc6c-106">Visual Studio'da yeni bir Visual C# konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1cc6c-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="1cc6c-107">Merhaba Visual Studio ana menüsünde tıklatın **Araçları**, **kitaplık Paket Yöneticisi**, ve **Paket Yöneticisi Konsolu**, ardından hello konsol penceresinde aşağıdaki komutu yazın ve tuşuna basın **Girin**:</span><span class="sxs-lookup"><span data-stu-id="1cc6c-107">In hello Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in hello console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="1cc6c-108">Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak [Microsoft.Azure.Notification Hubs NuGet paketini].</span><span class="sxs-lookup"><span data-stu-id="1cc6c-108">This adds a reference toohello Azure Notification Hubs SDK using hello [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="1cc6c-109">Program.cs Hello dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="1cc6c-109">Open hello file Program.cs and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="1cc6c-110">Merhaba, `Program` sınıfı, yöntemi aşağıdaki hello eklemek veya zaten varsa değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1cc6c-110">In hello `Program` class, add hello following method, or replace it if it already exists:</span></span>
   
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
   
    <span data-ttu-id="1cc6c-111">Bu kodu her hello altı etiketler hello dize dizisi için bir şablon bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="1cc6c-111">This code sends a template notification for each of hello six tags in hello string array.</span></span> <span data-ttu-id="1cc6c-112">etiketlerin Hello kullan cihazları bildirimlerin yalnızca kayıtlı hello kategorileri için emin olur.</span><span class="sxs-lookup"><span data-stu-id="1cc6c-112">hello use of tags makes sure that devices receive notifications only for hello registered categories.</span></span>
5. <span data-ttu-id="1cc6c-113">Kod yukarıda Hello hello yerine `<hub name>` ve `<connection string with full access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultFullSharedAccessSignature* bildirim hub'ınızın hello panosundan .</span><span class="sxs-lookup"><span data-stu-id="1cc6c-113">In hello above code, replace hello `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and hello connection  string for *DefaultFullSharedAccessSignature* from hello dashboard of your notification hub.</span></span>
6. <span data-ttu-id="1cc6c-114">Merhaba satırlarında aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="1cc6c-114">Add hello following lines in hello **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="1cc6c-115">Merhaba konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1cc6c-115">Build hello console app.</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Notification Hubs ile çalışmaya başlama]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[bildirim hub'ları REST arabirimini]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Mobile Apps için anında iletme bildirimleri ekleme]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[nasıl toouse Java/php'den Notification Hubs]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet paketini]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/
