1. İçinde **uygulama** proje, açık hello dosya `AndroidManifest.xml`. Kodla Hello hello sonraki iki adımda  *`**my_app_package**`*  adıyla hello hello uygulama paketi projeniz için. Bu hello hello değeri `package` hello özniteliği `manifest` etiketi.
2. Merhaba varolan sonra aşağıdaki yeni izinleri hello eklemek `uses-permission` öğe:

        <permission android:name="**my_app_package**.permission.C2D_MESSAGE"
            android:protectionLevel="signature" />
        <uses-permission android:name="**my_app_package**.permission.C2D_MESSAGE" />
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="android.permission.GET_ACCOUNTS" />
        <uses-permission android:name="android.permission.WAKE_LOCK" />
3. Koddan sonra hello hello eklemek `application` etiketi açma:

        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
                                         android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="**my_app_package**" />
            </intent-filter>
        </receiver>
4. Açık hello dosya *ToDoActivity.java*ve içeri aktarma deyimini aşağıdaki hello ekleyin:

        import com.microsoft.windowsazure.notifications.NotificationsManager;
5. Özel değişken toohello sınıfı aşağıdaki hello ekleyin. Değiştir  *`<PROJECT_NUMBER>`*  yordamdan önceki hello tooyour uygulamada Google tarafından atanan hello proje numarası ile.

        public static final String SENDER_ID = "<PROJECT_NUMBER>";
6. Değiştirme hello tanımını *MobileServiceClient* gelen **özel** çok**ortak statik**, şimdi şöyle görünür:

        public static MobileServiceClient mClient;
7. Yeni bir sınıf toohandle bildirimleri ekleyin. Proje Gezgini'nde hello açmak **src** > **ana** > **java** düğümleri ve sağ hello paket adı düğüm. Tıklatın **yeni**ve ardından **Java sınıfı**.
8. İçinde **adı**, türü `MyHandler`ve ardından **Tamam**.

    ![](./media/app-service-mobile-android-configure-push/android-studio-create-class.png)

9. Merhaba MyHandler dosyasında hello sınıf bildirimi ile değiştirin:

        public class MyHandler extends NotificationsHandler {
10. İçeri aktarma deyimlerini hello için aşağıdaki hello eklemek `MyHandler` sınıfı:

        import com.microsoft.windowsazure.notifications.NotificationsHandler;
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.AsyncTask;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
11. Bu üye toohello ekleyeceğimize `MyHandler` sınıfı:

        public static final int NOTIFICATION_ID = 1;
12. Merhaba, `MyHandler` sınıfı, kod toooverride hello aşağıdaki hello eklemek **onRegistered** Cihazınızı hello mobil hizmet bildirim hub'ı ile kaydeder yöntemi.

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
       }
13. Merhaba, `MyHandler` sınıfı, kod toooverride hello aşağıdaki hello eklemek **onReceive** , alındığında hello bildirim toodisplay neden yöntemi.

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
       }
14. Merhaba geri hello TodoActivity.java dosyasında güncelleştirme **onCreate** hello yöntemi *ToDoActivity* sınıf tooregister hello bildirim işleyici sınıfı. Merhaba sonra bu kodu emin tooadd olun *MobileServiceClient* örneği.

        NotificationsManager.handleNotifications(this, SENDER_ID, MyHandler.class);

    Uygulamanızı güncelleştirilmiş toosupport anında iletme bildirimleri sunulmuştur.
