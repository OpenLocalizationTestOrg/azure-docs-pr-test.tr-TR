1. Yeni bir sınıf olarak adlandırılan hello projesinde oluşturmak `ToDoBroadcastReceiver`.
2. Merhaba aşağıdaki using deyimlerini çok**ToDoBroadcastReceiver** sınıfı:
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. Merhaba arasında izin istekleri aşağıdaki hello eklemek **kullanarak** deyimleri ve hello **ad alanı** bildirimi:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. Merhaba varolan **ToDoBroadcastReceiver** sınıf tanımının hello aşağıdaki ile:
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set hello Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    Yukarıdaki kod Hello değiştirmeniz gerekir  *`<PROJECT_NUMBER>`*  hello Google developer Portal'daki uygulamanıza sağladığında Google tarafından atanan hello proje numarası ile. 
5. Merhaba ToDoBroadcastReceiver.cs proje dosyasında hello tanımlayan kodu aşağıdaki hello eklemek **PushHandlerService** sınıfı:
   
        // hello ServiceAttribute must be applied toohello class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    Bu sınıfın türetildiği Not **GcmServiceBase** ve o hello **hizmet** özniteliği olmalıdır uygulanan toothis sınıfı.
   
   > [!NOTE]
   > Merhaba **GcmServiceBase** sınıfı uygulayan hello **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** ve  **OnError()** yöntemleri. Merhaba bu yöntemleri geçersiz kılmanız gerekir **PushHandlerService** sınıfı.
   > 
   > 
6. Aşağıdaki kodu toohello hello eklemek **PushHandlerService** hello geçersiz kılmaları sınıf **OnRegistered** olay işleyicisi. 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("hello device has been registered with GCM.", "Success!");
   
            // Get hello MobileServiceClient from hello current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define hello template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run hello registration on hello same thread as hello activity, 
                // tooavoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register hello template with Notification Hubs.
                    async () => await push.RegisterAsync(registrationId, templates));
   
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Push Installation Id", push.InstallationId.ToString()));
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(
                    string.Format("Error with Azure push registration: {0}", ex.Message));
            }
        }
   
    Bu yöntem, Itanium tabanlı sistemler için GCM kayıt kimliği tooregister Azure ile anında iletme bildirimleri için döndürülen hello kullanır. Oluşturulduktan sonra etiketleri yalnızca toohello kayıt eklenebilir. Daha fazla bilgi için bkz: [nasıl yapılır: eklemek tooa cihaz yükleme tooenable itme--etiketler etiketler](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).
7. Merhaba geçersiz kılma **Onmessageoptions** yönteminde **PushHandlerService** koddan hello ile:
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract hello push notification message from hello intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager toosend hello notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent tooshow hello notification in hello UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create hello notification using hello builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display hello notification in hello Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. Merhaba geçersiz kılma **OnUnRegistered()** ve **OnError()** koddan hello yöntemleriyle.
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in hello notification: {0}.", errorId));
       }

