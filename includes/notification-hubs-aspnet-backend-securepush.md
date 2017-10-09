## <a name="webapi-project"></a>Webapı proje
1. Visual Studio'da hello açın **AppBackend** hello oluşturulan proje **kullanıcılara bildirme** Öğreticisi.
2. Notifications.cs, tüm Değiştir hello içinde **bildirimleri** koddan hello sınıfıyla. Emin tooreplace hello yer tutucularını bağlantı dizenizi (tam erişimli) için bildirim hub'ı ve hello hub adı olabilir. Bu değerleri hello edinebilirsiniz [Klasik Azure portalı](http://manage.windowsazure.com). Bu modül şimdi gönderilecek hello farklı güvenli bildirimleri temsil eder. Tam bir uygulama hello bildirimleri bir veritabanında depolanır; Kolaylık olması için bu durumda bunları bellekte depolarız.
   
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

1. Merhaba kod hello içinde NotificationsController.cs içinde değiştirin **NotificationsController** sınıf tanımının koddan hello ile. Bu bileşen hello aygıt tooretrieve hello bildirimi için bir yol güvenli bir şekilde uygular ve aynı zamanda bir yol (Bu öğreticinin amaçları hello) tootrigger güvenli itme tooyour aygıtları sağlar. Merhaba bildirim toohello bildirim hub'ı gönderirken, biz yalnızca ham bildirim hello kimlikli hello bildirim (ve gerçek ileti yok) göndermek olduğunu unutmayın:
   
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


Bu hello Not `Post` yöntemi şimdi göndermez bildirim. Yalnızca hello bildirim kimliği ve hassas olmayan tüm içeriği içeren bir ham bildirim gönderir. Ayrıca, işlem hatalarına neden şekilde, bildirim hub'ına, yapılandırılmış kimlik bilgilerine sahip olduğunuz değil hello platformlar için Gönder emin toocomment hello olun.

1. Sipariş toomake bu uygulama tooan Azure Web sitesi yeniden dağıtımını yapacaksınız şimdi onu tüm cihazlardan erişilebilir. Merhaba üzerinde sağ **AppBackend** proje ve seçin **Yayımla**.
2. Azure Web sitesi yayımlama hedefi olarak seçin. Azure hesabınızla oturum açın ve mevcut veya yeni bir Web sitesini seçin ve hello Not **hedef URL** hello özelliğinde **bağlantı** sekmesi. Toothis URL'si olarak başvuruda bulunacak, *arka uç nokta* Bu öğreticide daha sonra. **Yayımla**’ta tıklayın.

