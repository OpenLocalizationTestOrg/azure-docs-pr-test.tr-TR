1. <span data-ttu-id="30146-101">İçinde **uygulama** proje, açık hello dosya `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="30146-101">In your **app** project, open hello file `AndroidManifest.xml`.</span></span> <span data-ttu-id="30146-102">Kodla Hello hello sonraki iki adımda  *`**my_app_package**`*  adıyla hello hello uygulama paketi projeniz için.</span><span class="sxs-lookup"><span data-stu-id="30146-102">In hello code in hello next two steps, replace *`**my_app_package**`* with hello name of hello app package for your project.</span></span> <span data-ttu-id="30146-103">Bu hello hello değeri `package` hello özniteliği `manifest` etiketi.</span><span class="sxs-lookup"><span data-stu-id="30146-103">This is hello value of hello `package` attribute of hello `manifest` tag.</span></span>
2. <span data-ttu-id="30146-104">Merhaba varolan sonra aşağıdaki yeni izinleri hello eklemek `uses-permission` öğe:</span><span class="sxs-lookup"><span data-stu-id="30146-104">Add hello following new permissions after hello existing `uses-permission` element:</span></span>

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. <span data-ttu-id="30146-105">Koddan sonra hello hello eklemek `application` etiketi açma:</span><span class="sxs-lookup"><span data-stu-id="30146-105">Add hello following code after hello `application` opening tag:</span></span>

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. <span data-ttu-id="30146-106">Açık hello dosya *ToDoActivity.java*ve içeri aktarma deyimini aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="30146-106">Open hello file *ToDoActivity.java*, and add hello following import statement:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. <span data-ttu-id="30146-107">Özel değişken toohello sınıfı aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="30146-107">Add hello following private variable toohello class.</span></span> <span data-ttu-id="30146-108">Değiştir  *`<PROJECT_NUMBER>`*  yordamdan önceki hello tooyour uygulamada Google tarafından atanan hello proje numarası ile.</span><span class="sxs-lookup"><span data-stu-id="30146-108">Replace *`<PROJECT_NUMBER>`* with hello project number assigned by Google tooyour app in hello preceding procedure.</span></span>

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. <span data-ttu-id="30146-109">Değiştirme hello tanımını *MobileServiceClient* gelen **özel** çok**ortak statik**, şimdi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="30146-109">Change hello definition of *MobileServiceClient* from **private** too**public static**, so it now looks like this:</span></span>

        public static MobileServiceClient mClient;
7. <span data-ttu-id="30146-110">Yeni bir sınıf toohandle bildirimleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="30146-110">Add a new class toohandle notifications.</span></span> <span data-ttu-id="30146-111">Proje Gezgini'nde hello açmak **src** > **ana** > **java** düğümleri ve sağ hello paket adı düğüm.</span><span class="sxs-lookup"><span data-stu-id="30146-111">In Project Explorer, open hello **src** > **main** > **java** nodes, and right-click hello package name node.</span></span> <span data-ttu-id="30146-112">Tıklatın **yeni**ve ardından **Java sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="30146-112">Click **New**, and then click **Java Class**.</span></span>
8. <span data-ttu-id="30146-113">İçinde **adı**, türü `MyHandler`ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="30146-113">In **Name**, type `MyHandler`, and then click **OK**.</span></span>

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. <span data-ttu-id="30146-114">Merhaba MyHandler dosyasında hello sınıf bildirimi ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="30146-114">In hello MyHandler file, replace hello class declaration with:</span></span>

        public class MyHandler extends NotificationsHandler {
10. <span data-ttu-id="30146-115">İçeri aktarma deyimlerini hello için aşağıdaki hello eklemek `MyHandler` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="30146-115">Add hello following import statements for hello `MyHandler` class:</span></span>

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. <span data-ttu-id="30146-116">Bu üye toohello ekleyeceğimize `MyHandler` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="30146-116">Next add this member toohello `MyHandler` class:</span></span>

        public static final int NOTIFICATION_ID = 1;
12. <span data-ttu-id="30146-117">Merhaba, `MyHandler` sınıfı, kod toooverride hello aşağıdaki hello eklemek **onRegistered** Cihazınızı hello mobil hizmet bildirim hub'ı ile kaydeder yöntemi.</span><span class="sxs-lookup"><span data-stu-id="30146-117">In hello `MyHandler` class, add hello following code toooverride hello **onRegistered** method, which registers your device with hello mobile service notification hub.</span></span>

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
       <span data-ttu-id="30146-118">}</span><span class="sxs-lookup"><span data-stu-id="30146-118">}</span></span>
13. <span data-ttu-id="30146-119">Merhaba, `MyHandler` sınıfı, kod toooverride hello aşağıdaki hello eklemek **onReceive** , alındığında hello bildirim toodisplay neden yöntemi.</span><span class="sxs-lookup"><span data-stu-id="30146-119">In hello `MyHandler` class, add hello following code toooverride hello **onReceive** method, which causes hello notification toodisplay when it is received.</span></span>

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
       <span data-ttu-id="30146-120">}</span><span class="sxs-lookup"><span data-stu-id="30146-120">}</span></span>
14. <span data-ttu-id="30146-121">Merhaba geri hello TodoActivity.java dosyasında güncelleştirme **onCreate** hello yöntemi *ToDoActivity* sınıf tooregister hello bildirim işleyici sınıfı.</span><span class="sxs-lookup"><span data-stu-id="30146-121">Back in hello TodoActivity.java file, update hello **onCreate** method of hello *ToDoActivity* class tooregister hello notification handler class.</span></span> <span data-ttu-id="30146-122">Merhaba sonra bu kodu emin tooadd olun *MobileServiceClient* örneği.</span><span class="sxs-lookup"><span data-stu-id="30146-122">Make sure tooadd this code after hello *MobileServiceClient* is instantiated.</span></span>

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    <span data-ttu-id="30146-123">Uygulamanızı güncelleştirilmiş toosupport anında iletme bildirimleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="30146-123">Your app is now updated toosupport push notifications.</span></span>
