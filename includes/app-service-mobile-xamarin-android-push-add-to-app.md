1. <span data-ttu-id="35ba2-101">Adlı projeye yeni bir sınıf oluşturun `ToDoBroadcastReceiver`.</span><span class="sxs-lookup"><span data-stu-id="35ba2-101">Create a new class in the project called `ToDoBroadcastReceiver`.</span></span>
2. <span data-ttu-id="35ba2-102">Aşağıdaki using deyimlerini ekleyin **ToDoBroadcastReceiver** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="35ba2-102">Add the following using statements to **ToDoBroadcastReceiver** class:</span></span>
   
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="35ba2-103">Arasına aşağıdaki izin isteklerini ekleyin **kullanarak** deyimleri ve **ad alanı** bildirimi:</span><span class="sxs-lookup"><span data-stu-id="35ba2-103">Add the following permission requests between the **using** statements and the **namespace** declaration:</span></span>
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
4. <span data-ttu-id="35ba2-104">Varolan **ToDoBroadcastReceiver** sınıf tanımının aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="35ba2-104">Replace the existing **ToDoBroadcastReceiver** class definition with the following:</span></span>
   
        [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, 
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, 
        Categories = new string[] { "@PACKAGE_NAME@" })]
        public class ToDoBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            // Set the Google app ID.
            public static string[] senderIDs = new string[] { "<PROJECT_NUMBER>" };
        }
   
    <span data-ttu-id="35ba2-105">Yukarıdaki kodu değiştirmeniz gerekir  *`<PROJECT_NUMBER>`*  uygulamanızı Google developer Portal'daki sağladığında Google tarafından atanan proje numarası ile.</span><span class="sxs-lookup"><span data-stu-id="35ba2-105">In the above code, you must replace *`<PROJECT_NUMBER>`* with the project number assigned by Google when you provisioned your app in the Google developer portal.</span></span> 
5. <span data-ttu-id="35ba2-106">ToDoBroadcastReceiver.cs proje dosyasında tanımlar aşağıdaki kodu ekleyin **PushHandlerService** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="35ba2-106">In the ToDoBroadcastReceiver.cs project file, add the following code that defines the **PushHandlerService** class:</span></span>
   
        // The ServiceAttribute must be applied to the class.
        [Service] 
        public class PushHandlerService : GcmServiceBase
        {
            public static string RegistrationID { get; private set; }
   
            public PushHandlerService() : base(ToDoBroadcastReceiver.senderIDs) { }
        }
   
    <span data-ttu-id="35ba2-107">Bu sınıfın türetildiği Not **GcmServiceBase** ve **hizmet** özniteliği bu sınıfa uygulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="35ba2-107">Note that this class derives from **GcmServiceBase** and that the **Service** attribute must be applied to this class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="35ba2-108">**GcmServiceBase** uygulayan sınıf **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** ve  **OnError()** yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="35ba2-108">The **GcmServiceBase** class implements the **OnRegistered()**, **OnUnRegistered()**, **OnMessage()** and **OnError()** methods.</span></span> <span data-ttu-id="35ba2-109">Bu yöntemleri geçersiz kılmanız gerekir **PushHandlerService** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="35ba2-109">You must override these methods in the **PushHandlerService** class.</span></span>
   > 
   > 
6. <span data-ttu-id="35ba2-110">Aşağıdaki kodu ekleyin **PushHandlerService** geçersiz kılmaları sınıf **OnRegistered** olay işleyicisi.</span><span class="sxs-lookup"><span data-stu-id="35ba2-110">Add the following code to the **PushHandlerService** class that overrides the **OnRegistered** event handler.</span></span> 
   
        protected override void OnRegistered(Context context, string registrationId)
        {
            System.Diagnostics.Debug.WriteLine("The device has been registered with GCM.", "Success!");
   
            // Get the MobileServiceClient from the current activity instance.
            MobileServiceClient client = ToDoActivity.CurrentActivity.CurrentClient;
            var push = client.GetPush();
   
            // Define a message body for GCM.
            const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";
   
            // Define the template registration as JSON.
            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
              {"body", templateBodyGCM }
            };
   
            try
            {
                // Make sure we run the registration on the same thread as the activity, 
                // to avoid threading errors.
                ToDoActivity.CurrentActivity.RunOnUiThread(
   
                    // Register the template with Notification Hubs.
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
   
    <span data-ttu-id="35ba2-111">Bu yöntem, anında iletme bildirimleri için Azure ile kaydetmek için döndürülen GCM kayıt Kimliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="35ba2-111">This method uses the returned GCM registration ID to register with Azure for push notifications.</span></span> <span data-ttu-id="35ba2-112">Oluşturulduktan sonra etiketleri yalnızca kayıt için eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="35ba2-112">Tags can only be added to the registration after it is created.</span></span> <span data-ttu-id="35ba2-113">Daha fazla bilgi için bkz: [nasıl yapılır: anında iletme etiketleri etkinleştirmek için bir aygıt yükleme etiketler ekleme](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span><span class="sxs-lookup"><span data-stu-id="35ba2-113">For more information, see [How to: Add tags to a device installation to enable push-to-tags](../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags).</span></span>
7. <span data-ttu-id="35ba2-114">Geçersiz kılma **Onmessageoptions** yönteminde **PushHandlerService** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="35ba2-114">Override the **OnMessage** method in **PushHandlerService** with the following code:</span></span>
   
       protected override void OnMessage(Context context, Intent intent)
       {          
           string message = string.Empty;
   
           // Extract the push notification message from the intent.
           if (intent.Extras.ContainsKey("message"))
           {
               message = intent.Extras.Get("message").ToString();
               var title = "New item added:";
   
               // Create a notification manager to send the notification.
               var notificationManager = 
                   GetSystemService(Context.NotificationService) as NotificationManager;
   
               // Create a new intent to show the notification in the UI. 
               PendingIntent contentIntent = 
                   PendingIntent.GetActivity(context, 0, 
                   new Intent(this, typeof(ToDoActivity)), 0);              
   
               // Create the notification using the builder.
               var builder = new Notification.Builder(context);
               builder.SetAutoCancel(true);
               builder.SetContentTitle(title);
               builder.SetContentText(message);
               builder.SetSmallIcon(Resource.Drawable.ic_launcher);
               builder.SetContentIntent(contentIntent);
               var notification = builder.Build();
   
               // Display the notification in the Notifications Area.
               notificationManager.Notify(1, notification);
   
           }
       }
8. <span data-ttu-id="35ba2-115">Geçersiz kılma **OnUnRegistered()** ve **OnError()** aşağıdaki kodla yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="35ba2-115">Override the **OnUnRegistered()** and **OnError()** methods with the following code.</span></span>
   
       protected override void OnUnRegistered(Context context, string registrationId)
       {
           throw new NotImplementedException();
       }
   
       protected override void OnError(Context context, string errorId)
       {
           System.Diagnostics.Debug.WriteLine(
               string.Format("Error occurred in the notification: {0}.", errorId));
       }

