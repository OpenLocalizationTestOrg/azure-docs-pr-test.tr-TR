## <a name="webapi-project"></a><span data-ttu-id="bb2b3-101">Webapı proje</span><span class="sxs-lookup"><span data-stu-id="bb2b3-101">WebAPI Project</span></span>
1. <span data-ttu-id="bb2b3-102">Visual Studio'da hello açın **AppBackend** hello oluşturulan proje **kullanıcılara bildirme** Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-102">In Visual Studio, open hello **AppBackend** project that you created in hello **Notify Users** tutorial.</span></span>
2. <span data-ttu-id="bb2b3-103">Notifications.cs, tüm Değiştir hello içinde **bildirimleri** koddan hello sınıfıyla.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-103">In Notifications.cs, replace hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="bb2b3-104">Emin tooreplace hello yer tutucularını bağlantı dizenizi (tam erişimli) için bildirim hub'ı ve hello hub adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-104">Be sure tooreplace hello placeholders with your connection string (with full access) for your notification hub, and hello hub name.</span></span> <span data-ttu-id="bb2b3-105">Bu değerleri hello edinebilirsiniz [Klasik Azure portalı](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bb2b3-105">You can obtain these values from hello [Azure Classic Portal](http://manage.windowsazure.com).</span></span> <span data-ttu-id="bb2b3-106">Bu modül şimdi gönderilecek hello farklı güvenli bildirimleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-106">This module now represents hello different secure notifications that will be sent.</span></span> <span data-ttu-id="bb2b3-107">Tam bir uygulama hello bildirimleri bir veritabanında depolanır; Kolaylık olması için bu durumda bunları bellekte depolarız.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-107">In a complete implementation, hello notifications will be stored in a database; for simplicity, in this case we store them in memory.</span></span>
   
        public class Notification
        {
            public int Id { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }

        public class Notifications
        {
            public static Notifications Instance = new Notifications();

            private List<Notification> notifications = new List<Notification>();

            public NotificationHubClient Hub { get; set; }

            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",     "{hub name}");
            }

            public Notification CreateNotification(string payload)
            {
                var notification = new Notification() {
                Id = notifications.Count,
                Payload = payload,
                Read = false
                };

                notifications.Add(notification);

                return notification;
            }

            public Notification ReadNotification(int id)
            {
                return notifications.ElementAt(id);
            }
        }

1. <span data-ttu-id="bb2b3-108">Merhaba kod hello içinde NotificationsController.cs içinde değiştirin **NotificationsController** sınıf tanımının koddan hello ile.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-108">In NotificationsController.cs, replace hello code inside hello **NotificationsController** class definition with hello following code.</span></span> <span data-ttu-id="bb2b3-109">Bu bileşen hello aygıt tooretrieve hello bildirimi için bir yol güvenli bir şekilde uygular ve aynı zamanda bir yol (Bu öğreticinin amaçları hello) tootrigger güvenli itme tooyour aygıtları sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-109">This component implements a way for hello device tooretrieve hello notification securely, and also provides a way (for hello purposes of this tutorial) tootrigger a secure push tooyour devices.</span></span> <span data-ttu-id="bb2b3-110">Merhaba bildirim toohello bildirim hub'ı gönderirken, biz yalnızca ham bildirim hello kimlikli hello bildirim (ve gerçek ileti yok) göndermek olduğunu unutmayın:</span><span class="sxs-lookup"><span data-stu-id="bb2b3-110">Note that when sending hello notification toohello notification hub, we only send a raw notification with hello ID of hello notification (and no actual message):</span></span>
   
       public NotificationsController()
       {
           Notifications.Instance.CreateNotification("This is a secure notification!");
       }
   
       // GET api/notifications/id
       public Notification Get(int id)
       {
           return Notifications.Instance.ReadNotification(id);
       }
   
       public async Task<HttpResponseMessage> Post()
       {
           var secureNotificationInTheBackend = Notifications.Instance.CreateNotification("Secure confirmation.");
           var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
           // windows
           var rawNotificationToBeSent = new Microsoft.Azure.NotificationHubs.WindowsNotification(secureNotificationInTheBackend.Id.ToString(),
                           new Dictionary<string, string> {
                               {"X-WNS-Type", "wns/raw"}
                           });
           await Notifications.Instance.Hub.SendNotificationAsync(rawNotificationToBeSent, usernameTag);
   
           // apns
           await Notifications.Instance.Hub.SendAppleNativeNotificationAsync("{\"aps\": {\"content-available\": 1}, \"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}", usernameTag);
   
           // gcm
           await Notifications.Instance.Hub.SendGcmNativeNotificationAsync("{\"data\": {\"secureId\": \"" + secureNotificationInTheBackend.Id.ToString() + "\"}}", usernameTag);

            return Request.CreateResponse(HttpStatusCode.OK);
        }


<span data-ttu-id="bb2b3-111">Bu hello Not `Post` yöntemi şimdi göndermez bildirim.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-111">Note that hello `Post` method now does not send a toast notification.</span></span> <span data-ttu-id="bb2b3-112">Yalnızca hello bildirim kimliği ve hassas olmayan tüm içeriği içeren bir ham bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-112">It sends a raw notification that contains only hello notification ID, and not any sensitive content.</span></span> <span data-ttu-id="bb2b3-113">Ayrıca, işlem hatalarına neden şekilde, bildirim hub'ına, yapılandırılmış kimlik bilgilerine sahip olduğunuz değil hello platformlar için Gönder emin toocomment hello olun.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-113">Also, make sure toocomment hello send operation for hello platforms for which you do not have credentials configured on your notification hub, as they will result in errors.</span></span>

1. <span data-ttu-id="bb2b3-114">Sipariş toomake bu uygulama tooan Azure Web sitesi yeniden dağıtımını yapacaksınız şimdi onu tüm cihazlardan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-114">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="bb2b3-115">Merhaba üzerinde sağ **AppBackend** proje ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-115">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="bb2b3-116">Azure Web sitesi yayımlama hedefi olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-116">Select Azure Website as your publish target.</span></span> <span data-ttu-id="bb2b3-117">Azure hesabınızla oturum açın ve mevcut veya yeni bir Web sitesini seçin ve hello Not **hedef URL** hello özelliğinde **bağlantı** sekmesi. Toothis URL'si olarak başvuruda bulunacak, *arka uç nokta* Bu öğreticide daha sonra.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-117">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="bb2b3-118">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bb2b3-118">Click **Publish**.</span></span>

