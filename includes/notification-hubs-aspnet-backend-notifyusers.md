## <a name="create-hello-webapi-project"></a>Merhaba Webapı projesi oluşturma
Yeni bir ASP.NET Webapı arka izleyin hello bölümlerde oluşturulur ve üç ana amacı vardır:

1. **Kimlik doğrulaması yapan istemcilerin**: ileti işleyicisi sonraki tooauthenticate istemci istekleri ve hello isteği ile ilişkilendirme hello kullanıcı eklenir.
2. **İstemci bildirim kayıtları**: denetleyicisi toohandle yeni kayıtlar için bir istemci cihaz tooreceive bildirimleri daha sonra ekleyeceksiniz. Merhaba kimliği doğrulanmış kullanıcı adı otomatik olarak toohello kayıt olarak eklenecek bir [etiketi](https://msdn.microsoft.com/library/azure/dn530749.aspx).
3. **Bildirimleri tooClients gönderme**: daha sonra siz de denetleyicisi tooprovide kullanıcı tootrigger güvenli itme toodevices yolu ve istemciler hello etiketiyle ilişkili ekleyeceksiniz. 

Aşağıdaki adımları hello nasıl toocreate hello yeni ASP.NET Webapı arka uç göster: 

> [!IMPORTANT]
> Visual Studio 2015 kullanıyorsanız veya önceki sürümleri, bu öğreticiye başlamadan önce lütfen hello hello NuGet Paket Yöneticisi en son sürümünü yüklediğinizden emin olun. toocheck, Visual Studio Başlangıç. Merhaba gelen **Araçları** menüsünde tıklatın **Uzantılar ve güncelleştirmeler**. Arama **NuGet Paket Yöneticisi** hello en son sürümü yüklü sürümü için Visual Studio ve emin olun. Aksi takdirde, kaldırın, ardından hello NuGet Paket Yöneticisi'ni yeniden yükleyin.
> 
> ![][B4]
> 
> [!NOTE]
> Visual Studio hello yüklediğinizden emin olun [Azure SDK'sı](https://azure.microsoft.com/downloads/) Web dağıtımı için.
> 
> 

1. Visual Studio veya Visual Studio Express’i başlatın. Tıklatın **Sunucu Gezgini** ve tooyour Azure hesabı oturum açın. Visual Studio toocreate hello web sitesi kaynakları hesabınızda imzalı ihtiyacınız olacaktır.
2. Visual Studio'da sırasıyla **dosya**, ardından **yeni**, ardından **proje**, genişletin **şablonları**, **Visual C#**, ardından **Web** ve **ASP.NET Web uygulaması**, tür hello adı **AppBackend**ve ardından **Tamam**. 
   
    ![][B1]
3. Merhaba, **yeni ASP.NET projesi** iletişim kutusunda, tıklatın **Web API**, ardından **Tamam**.
   
    ![][B2]
4. Merhaba, **yapılandırma Microsoft Azure Web uygulaması** iletişim kutusunda, bir abonelik seçin ve bir **uygulama hizmeti planı** zaten oluşturmuş. Ayrıca seçebilirsiniz **yeni bir uygulama hizmeti planı oluştur** hello iletişim kutusundan oluşturun. Bu öğretici için bir veritabanı gerekmez. Uygulama hizmet planınız seçtikten sonra tıklatın **Tamam** toocreate hello projesi.
   
    ![][B5]

## <a name="authenticating-clients-toohello-webapi-backend"></a>İstemcileri toohello Webapı arka uç kimlik doğrulaması
Bu bölümde, adlı yeni bir ileti işleyicisi sınıfı oluşturacak **AuthenticationTestHandler** hello yeni arka uç için. Bu sınıfın türetildiği [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) ve hello arka uç gelen tüm istekleri işleyebilmek için ileti işleyicisi eklenir. 

1. Çözüm Gezgini'nde hello sağ **AppBackend** proje, tıklatın **Ekle**, ardından **sınıfı**. Ad hello yeni sınıf **AuthenticationTestHandler.cs**, tıklatıp **Ekle** toogenerate hello sınıfı. Bu sınıfı kullanarak kullanılan tooauthenticate kullanıcıların olacaktır *temel kimlik doğrulaması* basitleştirmek için. Uygulamanız herhangi bir kimlik doğrulama şemasını kullanabilir.
2. AuthenticationTestHandler.cs içinde hello aşağıdakileri ekleyin `using` deyimleri:
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Text;
        using System.Threading.Tasks;

3. Merhaba değiştirme AuthenticationTestHandler.cs içinde `AuthenticationTestHandler` sınıf tanımının koddan hello ile. 
   
    Aşağıdaki üç koşul hello tümü doğru olduğunda bu işleyici hello isteği yetkilendirin.
   
   * Merhaba isteği dahil bir *yetkilendirme* üstbilgi. 
   * Merhaba isteği kullanır *temel* kimlik doğrulaması. 
   * Merhaba kullanıcı adı dizesi ve hello parola dizesi olan hello aynı dize.
     
     Aksi takdirde hello isteği reddedilir. Bu geçerli bir kimlik doğrulama ve yetkilendirme yaklaşımı değildir. Yalnızca bu öğreticiye yönelik çok basit bir örnektir.
     
     Merhaba istek iletisi kimliği doğrulanmış ve hello tarafından yetkili varsa `AuthenticationTestHandler`, sonra hello temel kimlik doğrulaması kullanıcı hello geçerli istekte ekli toohello [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx). Kullanıcı bilgilerini hello HttpContext başka bir denetleyici (RegisterController) tarafından kullanılacak sonraki tooadd bir [etiketi](https://msdn.microsoft.com/library/azure/dn530749.aspx) toohello bildirimi kayıt isteği.
     
       public class AuthenticationTestHandler : DelegatingHandler   {       protected override Task<HttpResponseMessage> SendAsync(       HttpRequestMessage request, CancellationToken cancellationToken)       {           var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach hello new principal object toohello current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       }
     
     > [!NOTE]
     > **Güvenlik Notu**: Merhaba `AuthenticationTestHandler` sınıfı doğru kimlik doğrulaması sağlamaz. Kullanılan yalnızca toomimic temel kimlik doğrulaması ve güvenli değildir. Üretim uygulamalarınızda ve hizmetlerinizde güvenli bir kimlik doğrulama mekanizması uygulamanız gerekir.                
     > 
     > 
4. Merhaba hello sonunda koddan hello eklemek `Register` hello yönteminde **App_Start/WebApiConfig.cs** tooregister hello ileti işleyicisi sınıfı:
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. Yaptığınız değişiklikleri kaydedin.

## <a name="registering-for-notifications-using-hello-webapi-backend"></a>Merhaba Webapı arka uç kullanarak bildirimleri için kaydediliyor
Bu bölümde, yeni bir denetleyici toohello Webapı arka uç toohandle tooregister bir kullanıcı ve cihaz bildirimlerinin bildirim hub'ları için hello istemci kitaplığı kullanılarak istekleri ekleyeceğiz. Merhaba denetleyicisi doğrulandı ve toohello HttpContext hello tarafından eklenen hello kullanıcı için bir kullanıcı etiketi eklemek `AuthenticationTestHandler`. Merhaba etiketi hello dize biçiminde olacaktır `"username:<actual username>"`.

1. Çözüm Gezgini'nde hello sağ **AppBackend** proje ve ardından **NuGet paketlerini Yönet**.
2. Merhaba sol taraftaki tıklatın **çevrimiçi**, arayın ve **Microsoft.Azure.NotificationHubs** hello içinde **arama** kutusu.
3. Merhaba sonuçlar listesinde tıklayın **Microsoft Azure bildirim hub'ları**ve ardından **yükleme**. Merhaba yüklemeyi tamamlamak ve sonra hello NuGet Paket Yöneticisi penceresini kapatın.
   
    Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.
4. Bildirim hub'ı kullanılan toosend bildirimleri ile Merhaba bağlantısını temsil eden yeni bir sınıf dosyası artık oluşturacağız. Hello Hello Çözüm Gezgini, sağ tıklatın **modelleri** klasörü, tıklatın **Ekle**, ardından **sınıfı**. Ad hello yeni sınıf **Notifications.cs**, ardından **Ekle** toogenerate hello sınıfı. 
   
    ![][B6]
5. Notifications.cs içinde hello aşağıdakileri ekleyin `using` deyimi hello dosyanın üst kısmındaki hello:
   
        using Microsoft.Azure.NotificationHubs;
6. Hello yerine `Notifications` sınıf hello aşağıdaki tanımıyla ve hello bağlantı dizesi (tam erişim) bildirim hub'ınız için emin tooreplace hello iki yer tutucularını yapıp hello hub adını (adresinde [Klasik Azure portalı ](http://manage.windowsazure.com)):
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. Bundan sonra **RegisterController** adlı yeni bir denetleyici oluşturacağız. Hello Çözüm Gezgini'nde sağ **denetleyicileri** klasörü, ardından **Ekle**, ardından **denetleyicisi**. Merhaba tıklatın **Web API 2 denetleyicisi--boş** öğesini ve ardından **Ekle**. Ad hello yeni sınıf **RegisterController**ve ardından **Ekle** yeniden toogenerate hello denetleyicisi.
   
    ![][B7]
   
    ![][B8]
8. RegisterController.cs içinde hello aşağıdakileri ekleyin `using` deyimleri:
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. Merhaba içindeki kodu aşağıdaki hello eklemek `RegisterController` sınıf tanımının. Bu kodda unutmayın, biz bu hello kullanıcı için bir kullanıcı etiket toohello HttpContext bağlı ekleyin. Merhaba kullanıcı doğrulandı ve toohello HttpContext eklediğimiz, hello İleti Filtresi tarafından bağlı `AuthenticationTestHandler`. Kullanıcı hello isteğe bağlı denetimleri tooverify haklarına sahip de ekleyebilirsiniz tooregister hello için istenen etiketler.
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at hello specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed tooadd these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. Yaptığınız değişiklikleri kaydedin.

## <a name="sending-notifications-from-hello-webapi-backend"></a>Merhaba Webapı arka uç gönderen bildirimleri
Bu bölümde istemci cihazları toosend hello ASP.NET Webapı arka uç Azure bildirim hub'ları Hizmet Yönetimi Kitaplığı kullanarak hello kullanıcı adı etiketi dayalı bir bildirim için bir yol sunan yeni bir denetleyici ekleyin.

1. **NotificationsController** adlı başka bir yeni denetleyici oluşturun. Merhaba oluşturmak hello oluşturduğunuz aynı şekilde **RegisterController** hello önceki bölümdeki.
2. NotificationsController.cs içinde hello aşağıdakileri ekleyin `using` deyimleri:
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. Yöntem toohello aşağıdaki hello eklemek **NotificationsController** sınıfı.
   
    Bu kod Gönder hello Platform bildirim hizmeti (PNS) üzerinde göre bir bildirim türü `pns` parametresi. Merhaba değerini `to_tag` kullanılan tooset hello olan *kullanıcıadı* hello ileti etiketi. Bu etiket, etkin bir bildirim hub'ı kaydının kullanıcı etiketi ile eşleşmelidir. Merhaba bildirim iletisi hello hello POST isteği gövdesinden çekilen ve hello hedef PNS biçimlendirilmiş. 
   
    Merhaba, desteklenen aygıtların tooreceive bildirimleri kullanmayı Platform bildirim hizmeti (PNS) bağlı olarak farklı bildirimleri farklı biçimlerini kullanarak desteklenir. Örneğin, Windows cihazlarında başka bir PNS tarafından doğrudan desteklenmeyen bir [WNS ile bildirim](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) kullanabilirsiniz. Arka PNS cihazların Merhaba için desteklenen bir bildirim içine tooformat hello bildirim gerekir böylece toosupport planlayın. Ardından üzerinde hello hello uygun gönderme API kullanan [NotificationHubClient sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. Tuşuna **F5** toorun hello uygulama ve tooensure hello çalışmanızın doğruluğunu kadarki. Hello uygulama, bir web tarayıcısı başlatmak ve hello ASP.NET giriş sayfasını görüntüleyin. 

## <a name="publish-hello-new-webapi-backend"></a>Yayımlama hello yeni Webapı arka uç
1. Biz sipariş toomake bu uygulama tooan Azure Web sitesi dağıtacağınız şimdi onu tüm cihazlardan erişilebilir. Merhaba üzerinde sağ **AppBackend** proje ve seçin **Yayımla**.
2. Yayımlama hedefi olarak **Microsoft Azure Uygulama Hizmeti**’ni seçip **Yayımla**’ya tıklayın. Bu, Azure'da tüm hello gerekli Azure kaynaklarını toorun hello ASP.NET web uygulaması oluşturmanıza yardımcı olacak hello App Service Oluştur iletişim kutusunu açar.

    ![][B15]
3. Merhaba, **App Service Oluştur** iletişim kutusunda, Azure hesabınızı seçin. **Tür Değiştir**’e tıklayıp **Web Uygulaması**’nı seçin. Merhaba tutmak **Web uygulaması adı** seçin ve verilen hello **abonelik**, **kaynak grubu**, ve **App Service planı**.  **Oluştur**'a tıklayın.

4. Merhaba Not **Site URL'si** hello özelliğinde **Özet** bölümü. Toothis URL'si olarak başvuruda bulunacak, *arka uç nokta* Bu öğreticide daha sonra. **Yayımla**’ta tıklayın.

5. Merhaba Sihirbaz tamamlandıktan sonra hello ASP.NET web uygulaması tooAzure yayımlar ve ardından başlatır hello varsayılan tarayıcıda uygulama hello.  Uygulamanız Azure Uygulama Hizmetileri’nde görüntülenebilir.

Merhaba URL hello biçimi http://<app_name>.azurewebsites.net ile daha önce belirtilen başlangıç web uygulaması adı kullanır.

[B1]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: ./media/notification-hubs-aspnet-backend-notifyusers/publish-to-app-service.png
[B16]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: ./media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG
