1. <span data-ttu-id="e3495-101">İçinde **uygulama** projesi, dosyayı açma `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="e3495-101">In your **app** project, open the file `AndroidManifest.xml`.</span></span> <span data-ttu-id="e3495-102">Sonraki iki adımda kodla  *`**my_app_package**`*  projeniz için uygulama paketi adıyla.</span><span class="sxs-lookup"><span data-stu-id="e3495-102">In the code in the next two steps, replace *`**my_app_package**`* with the name of the app package for your project.</span></span> <span data-ttu-id="e3495-103">Bu değeri `package` özniteliği `manifest` etiketi.</span><span class="sxs-lookup"><span data-stu-id="e3495-103">This is the value of the `package` attribute of the `manifest` tag.</span></span>
2. <span data-ttu-id="e3495-104">Varolan sonra aşağıdaki yeni izinleri ekleyin `uses-permission` öğe:</span><span class="sxs-lookup"><span data-stu-id="e3495-104">Add the following new permissions after the existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="e3495-105">Sonra aşağıdaki kodu ekleyin `application` etiketi açma:</span><span class="sxs-lookup"><span data-stu-id="e3495-105">Add the following code after the `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="e3495-106">Dosyayı açmak *ToDoActivity.java*ve aşağıdaki içeri aktarma deyimini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e3495-106">Open the file *ToDoActivity.java*, and add the following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="e3495-107">Aşağıdaki özel değişken sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e3495-107">Add the following private variable to the class.</span></span> <span data-ttu-id="e3495-108">Değiştir  *`<PROJECT_NUMBER>`*  önceki yordamda ve uygulamanızın Google tarafından atanan proje numarası ile.</span><span class="sxs-lookup"><span data-stu-id="e3495-108">Replace *`<PROJECT_NUMBER>`* with the project number assigned by Google to your app in the preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="e3495-109">Tanımını değiştirin *MobileServiceClient* gelen **özel** için **ortak statik**, şimdi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e3495-109">Change the definition of *MobileServiceClient* from **private** to **public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="e3495-110">Bildirimleri işlemek için yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e3495-110">Add a new class to handle notifications.</span></span> <span data-ttu-id="e3495-111">Proje Gezgini'nde Aç **src** > **ana** > **java** düğümler ve paket adı düğümünü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e3495-111">In Project Explorer, open the **src** > **main** > **java** nodes, and right-click the package name node.</span></span> <span data-ttu-id="e3495-112">Tıklatın **yeni**ve ardından **Java sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="e3495-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="e3495-113">İçinde **adı**, türü `MyHandler`ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e3495-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="e3495-114">MyHandler dosyasında, sınıf bildirimi ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e3495-114">In the MyHandler file, replace the class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="e3495-115">İçin aşağıdaki içeri aktarma deyimlerini ekleyin `MyHandler` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="e3495-115">Add the following import statements for the `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="e3495-116">Bu üye sonraki eklemek `MyHandler` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="e3495-116">Next add this member to the `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="e3495-117">İçinde `MyHandler` sınıfı, geçersiz kılmak için aşağıdaki kodu ekleyin **onRegistered** Cihazınızı mobil hizmet bildirim hub'ı ile kaydeder yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e3495-117">In the `MyHandler` class, add the following code to override the **onRegistered** method, which registers your device with the mobile service notification hub.</span></span>

        @Override
        public void onRegistered(Context context,  final String gcmRegistrationId) {
           super.onRegistered(context, gcmRegistrationId);

           new AsyncTask<Void, Void, Void>() {

               protected Void doInBackground(Void... params) {
                   try {
                       ToDoActivity.mClient.getPush().register(gcmRegistrationId);
                       return null;
                   }
                   catch(Exception e) {
                       // handle error                
                   }
                   return null;              
               }
           }.execute();
       <span data-ttu-id="e3495-118">}</span><span class="sxs-lookup"><span data-stu-id="e3495-118">}</span></span>
13. <span data-ttu-id="e3495-119">İçinde `MyHandler` sınıfı, geçersiz kılmak için aşağıdaki kodu ekleyin **onReceive** , alındığında görüntülemek için bildirime neden olan yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e3495-119">In the `MyHandler` class, add the following code to override the **onReceive** method, which causes the notification to display when it is received.</span></span>

        @Override
        public void onReceive(Context context, Bundle bundle) {
               String msg = bundle.getString("message");

               PendingIntent contentIntent = PendingIntent.getActivity(context,
                       0, // requestCode
                       new Intent(context, ToDoActivity.class),
                       0); // flags

               Notification notification = new NotificationCompat.Builder(context)
                       .setSmallIcon(R.drawable.ic_launcher)
                       .setContentTitle("Notification Hub Demo")
                       .setStyle(new NotificationCompat.BigTextStyle().bigText(msg))
                       .setContentText(msg)
                       .setContentIntent(contentIntent)
                       .build();

               NotificationManager notificationManager = (NotificationManager)
                       context.getSystemService(Context.NOTIFICATION_SERVICE);
               notificationManager.notify(NOTIFICATION_ID, notification);
       <span data-ttu-id="e3495-120">}</span><span class="sxs-lookup"><span data-stu-id="e3495-120">}</span></span>
14. <span data-ttu-id="e3495-121">Geri TodoActivity.java dosyasında güncelleştirme **onCreate** yöntemi *ToDoActivity* bildirim işleyici sınıfını sınıfı.</span><span class="sxs-lookup"><span data-stu-id="e3495-121">Back in the TodoActivity.java file, update the **onCreate** method of the *ToDoActivity* class to register the notification handler class.</span></span> <span data-ttu-id="e3495-122">Sonra bu kodu eklediğinizden emin olun *MobileServiceClient* örneği.</span><span class="sxs-lookup"><span data-stu-id="e3495-122">Make sure to add this code after the *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="e3495-123">Uygulamanıza anında iletme bildirimlerini desteklemek üzere güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e3495-123">Your app is now updated to support push notifications.</span></span>
