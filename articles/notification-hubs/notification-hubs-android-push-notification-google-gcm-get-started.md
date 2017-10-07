---
title: "Azure Notification Hubs ile anında iletme bildirimleri tooAndroid aaaSending | Microsoft Docs"
description: "Bu öğreticide, bilgi nasıl toouse Azure Notification Hubs toopush bildirimleri tooAndroid aygıtlar."
services: notification-hubs
documentationcenter: android
keywords: "anında iletme bildirimleri,anında iletme bildirimi,android anında iletme bildirimi"
author: ysxu
manager: erikre
editor: 
ms.assetid: 8268c6ef-af63-433c-b14e-a20b04a0342a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: hero-article
ms.date: 07/05/2016
ms.author: yuaxu
ms.openlocfilehash: 6b15a477d86cf1e6efffb21c5bcef0de7761af79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooandroid-with-azure-notification-hubs"></a>Azure Notification Hubs ile anında iletme bildirimleri tooAndroid gönderme
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
> [!IMPORTANT]
> Bu konuda Google Cloud Messaging (GCM) ile anında iletme bildirimleri gösterilmektedir. Google Firebase bulut Mesajlaşma (FCM) kullanıyorsanız, bkz: [gönderme anında iletme bildirimleri tooAndroid Azure Notification Hubs ve FCM ile](notification-hubs-android-push-notification-google-fcm-get-started.md).
> 
> 

Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan Android uygulaması gösterir.
Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan bir Android uygulaması oluşturacaksınız.

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Bu öğreticinin tamamlanan hello kodu Github'dan indirilebilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted).

## <a name="prerequisites"></a>Ön koşullar
> [!IMPORTANT]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

Ayrıca tooan etkin Azure hesabı belirtilen yukarıdaki Bu öğretici yalnızca hello en son sürümünü gerektirir [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797).

Bu öğreticiyi tamamlamak Android uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a>Google Cloud Messaging'i destekleyen bir proje oluşturma
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Yeni bir bildirim hub'ı yapılandırma
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   Merhaba, **ayarları** dikey penceresinde, select **Bildirim Hizmetleri** ve ardından **Google (GCM)**. Merhaba API anahtarını girin ve tıklatın **kaydetmek**.

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

Bildirim hub'ınız şimdi GCM ile yapılandırılmış toowork olduğu ve uygulama tooreceive kaydolun ve anında iletme bildirimleri göndermek hello bağlantı dizeleri tooboth sahip.

## <a id="connecting-app"></a>Uygulama toohello bildirim hub'ınıza bağlanın
### <a name="create-a-new-android-project"></a>Yeni bir Android projesi oluşturma
1. Android Studio'da yeni bir Android Studio projesi başlatın.
   
   ![Android Studio - yeni proje][13]
2. Merhaba seçin **telefon ve Tablet** form faktörünü ve hello **Minimum SDK** toosupport istiyor. Ardından **İleri**'ye tıklayın.
   
   ![Android Studio - proje oluşturma iş akışı][14]
3. Seçin **boş etkinlik** hello ana etkinlik için tıklatın **sonraki**ve ardından **son**.

### <a name="add-google-play-services-toohello-project"></a>Google Play Hizmetleri toohello proje ekleyin
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Azure Notification Hubs kitaplıkları ekleme
1. Merhaba, `Build.Gradle` hello dosyası **uygulama**, hello satırlarında aşağıdaki hello eklemek **bağımlılıkları** bölümü.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. Depo hello sonra aşağıdaki hello eklemek **bağımlılıkları** bölümü.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-hello-androidmanifestxml"></a>Merhaba AndroidManifest.xml güncelleştiriliyor.
1. toosupport GCM, biz uygulanmalı bir örnek kimliği dinleme hizmeti çok kullanılan bizim kodda[kayıt belirteçleri elde](https://developers.google.com/cloud-messaging/android/client#sample-register) kullanarak [Google'nın örnek kimliği API'sini](https://developers.google.com/instance-id/). Bu öğreticide biz hello sınıfı adlandıracaktır `MyInstanceIDService`. 
   
    Hizmet tanımı toohello AndroidManifest.xml dosyasına hello aşağıdaki hello eklemek `<application>` etiketi. Hello yerine `<your package>` tutucuyla hello hello hello üst kısmında gösterilen asıl Paket adınızla `AndroidManifest.xml` dosya.
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. Biz örnek kimliği API'sini hello GCM kayıt belirtecimizi aldıktan sonra onu çok kullanacağız[hello Azure bildirim hub'ı ile kayıt](notification-hubs-push-notification-registration-management.md). Arka plan hello kullanarak Biz bu kayıt destekleyecek bir `IntentService` adlı `RegistrationIntentService`. Bu hizmet, [GCM kayıt belirtecimizi yenilemekten](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) de sorumludur.
   
    Hizmet tanımı toohello AndroidManifest.xml dosyasına hello aşağıdaki hello eklemek `<application>` etiketi. Hello yerine `<your package>` tutucuyla hello hello hello üst kısmında gösterilen asıl Paket adınızla `AndroidManifest.xml` dosya. 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. Biz de alıcı tooreceive bildirimleri tanımlayacaksınız. Aşağıdaki alıcı tanımını toohello AndroidManifest.xml dosyasına hello hello eklemek `<application>` etiketi. Hello yerine `<your package>` tutucuyla hello hello hello üst kısmında gösterilen asıl Paket adınızla `AndroidManifest.xml` dosya.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Gerekli GCM aşağıdaki hello ilgili hello aşağıdaki izinleri ekleyin `</application>` etiketi. Emin tooreplace olun `<your package>` hello hello üst kısmında gösterilen hello paket adı ile `AndroidManifest.xml` dosya.
   
    Bu izinler hakkında daha fazla bilgi için bkz. [Android için bir GCM İstemcisi uygulaması kurma](https://developers.google.com/cloud-messaging/android/client#manifest).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a>Kod ekleme
1. Hello Proje Görünümü'da, genişletin **uygulama** > **src** > **ana** > **java**. **Java**'nın altındaki paket klasörünüze sağ tıklayın, **Yeni**'ye tıklayın ve ardından **Java Sınıfı**'na tıklayın. `NotificationSettings` adlı yeni bir sınıf ekleyin. 
   
    ![Android Studio - yeni Java sınıfı][6]
   
    Tooupdate hello hello kodunu aşağıdaki hello bu üç yer tutucuları emin olun `NotificationSettings` sınıfı:
   
   * **Senderıd**: Merhaba önceki hello elde ettiğiniz proje numarası [Google Cloud Console](http://cloud.google.com/console).
   * **HubListenConnectionString**: Merhaba **DefaultListenAccessSignature** hub'ınız için bağlantı dizesi. Tıklayarak bağlantı dizesini kopyalayabilirsiniz **erişim ilkeleri** hello üzerinde **ayarları** dikey penceresinde hello üzerinde hub'ınızın [Azure Portal].
   * **HubName**: hello hub dikey penceresinde hello görünen bildirim hub'ınızın hello adını kullan [Azure Portal].
     
     `NotificationSettings` kodu:
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       }
2. Yukarıdaki Hello adımları kullanarak adlı başka bir yeni sınıf ekleyin `MyInstanceIDService`. Bu bizim Örnek Kimliği dinleme hizmeti uygulamamız olacak.
   
    Bu sınıfın Hello kodu çağıracaktır bizim `IntentService` çok[yenileme hello GCM belirtecini](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) hello arka planda.
   
        import android.content.Intent;
        import android.util.Log;
        import com.google.android.gms.iid.InstanceIDListenerService;

        public class MyInstanceIDService extends InstanceIDListenerService {

            private static final String TAG = "MyInstanceIDService";

            @Override
            public void onTokenRefresh() {

                Log.i(TAG, "Refreshing GCM Registration Token");

                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        };


1. Adlı başka bir yeni sınıf tooyour projesi eklemek `RegistrationIntentService`. Bu hello uygulaması olacak bizim `IntentService` işleyecek [yenileme hello GCM belirtecini](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) ve [hello bildirim hub'kaydetme](notification-hubs-push-notification-registration-management.md).
   
    Bu sınıfın kodu aşağıdaki hello kullanın.
   
        import android.app.IntentService;
        import android.content.Intent;
        import android.content.SharedPreferences;
        import android.preference.PreferenceManager;
        import android.util.Log;
   
        import com.google.android.gms.gcm.GoogleCloudMessaging;
        import com.google.android.gms.iid.InstanceID;
        import com.microsoft.windowsazure.messaging.NotificationHub;
   
        public class RegistrationIntentService extends IntentService {
   
            private static final String TAG = "RegIntentService";
   
            private NotificationHub hub;
   
            public RegistrationIntentService() {
                super(TAG);
            }
   
            @Override
            protected void onHandleIntent(Intent intent) {        
                SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(this);
                String resultString = null;
                String regID = null;
   
                try {
                    InstanceID instanceID = InstanceID.getInstance(this);
                    String token = instanceID.getToken(NotificationSettings.SenderId,
                            GoogleCloudMessaging.INSTANCE_ID_SCOPE);        
                    Log.i(TAG, "Got GCM Registration Token: " + token);
   
                    // Storing hello registration id that indicates whether hello generated token has been
                    // sent tooyour server. If it is not stored, send hello token tooyour server,
                    // otherwise your server should have already received hello token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting tooregister with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want toouse tags...
                        // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed toocomplete token refresh", e);
                    // If an exception happens while fetching hello new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt hello update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. İçinde `MainActivity` sınıfı, hello aşağıdakileri ekleyin `import` deyimleri hello yukarıda sınıf bildiriminin.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Özel üyelerin hello sınıfı hello üstündeki aşağıdaki hello ekleyin. Bunları kullanırız [hello Google Play Hizmetleri'nin kullanılabilirliğini Google tarafından önerildiği şekilde denetlemek](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk).
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. İçinde `MainActivity` sınıfı, yöntemi toohello Google Play Hizmetleri'nin kullanılabilirliğini izleyen hello ekleyin. 
   
        /**
         * Check hello device toomake sure it has hello Google Play Services APK. If
         * it doesn't, display a dialog that allows users toodownload hello APK from
         * hello Google Play Store or enable it in hello device's system settings.
         */
        private boolean checkPlayServices() {
            GoogleApiAvailability apiAvailability = GoogleApiAvailability.getInstance();
            int resultCode = apiAvailability.isGooglePlayServicesAvailable(this);
            if (resultCode != ConnectionResult.SUCCESS) {
                if (apiAvailability.isUserResolvableError(resultCode)) {
                    apiAvailability.getErrorDialog(this, resultCode, PLAY_SERVICES_RESOLUTION_REQUEST)
                            .show();
                } else {
                    Log.i(TAG, "This device is not supported by Google Play Services.");
                    ToastNotify("This device is not supported by Google Play Services.");
                    finish();
                }
                return false;
            }
            return true;
        }
5. İçinde `MainActivity` sınıfı, çağırmadan önce Google Play Hizmetleri'ni denetleyecek koddan hello eklemek, `IntentService` tooget GCM kayıt belirtecinizi ve bildirim hub'ınızı ile kaydedin.
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService tooregister this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. Merhaba, `OnCreate` hello yöntemi `MainActivity` sınıfı, etkinlik oluşturulduğunda kod toostart hello kayıt işlemi aşağıdaki hello ekleyin.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Bu ek yöntemleri toohello ekleme `MainActivity` uygulamanızda tooverify uygulama durumu ve rapor durumu.
   
        @Override
        protected void onStart() {
            super.onStart();
            isVisible = true;
        }
   
        @Override
        protected void onPause() {
            super.onPause();
            isVisible = false;
        }
   
        @Override
        protected void onResume() {
            super.onResume();
            isVisible = true;
        }
   
        @Override
        protected void onStop() {
            super.onStop();
            isVisible = false;
        }
   
        public void ToastNotify(final String notificationMessage) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(MainActivity.this, notificationMessage, Toast.LENGTH_LONG).show();
                    TextView helloText = (TextView) findViewById(R.id.text_hello);
                    helloText.setText(notificationMessage);
                }
            });
        }
8. Merhaba `ToastNotify` yöntemi kullanan hello *"Hello World"* `TextView` kontrol tooreport durumunu ve bildirimleri hello uygulamasında kalıcı olarak. Activity_main.xml düzeninizde, bu denetim için kimliği hello ekleyin.
   
       android:id="@+id/text_hello"
9. Merhaba AndroidManifest.xml tanımladığımız bizim alıcısı için bir alt sınıfı sonraki ekleyeceğiz. Adlı başka bir yeni sınıf tooyour projesi eklemek `MyHandler`.
10. İçeri aktarma deyimlerini hello üst kısmındaki aşağıdaki hello eklemek `MyHandler.java`:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. Merhaba kodunu aşağıdaki hello eklemek `MyHandler` öğesinin bir alt kolaylaştırarak sınıfı `com.microsoft.windowsazure.notifications.NotificationsHandler`.
    
    Bu kod hello geçersiz kılmaları `OnReceive` hello işleyici alınan bildirimleri bildirmesi yöntemi. Merhaba işleyici ayrıca hello kullanarak hello anında iletme bildirimi toohello Android bildirim Yöneticisi gönderir `sendNotification()` yöntemi. Merhaba `sendNotification()` yöntemi hello uygulama çalışmıyorken ve bir bildirim alındığında yürütülmelidir.
    
        public class MyHandler extends NotificationsHandler {
            public static final int NOTIFICATION_ID = 1;
            private NotificationManager mNotificationManager;
            NotificationCompat.Builder builder;
            Context ctx;
    
            @Override
            public void onReceive(Context context, Bundle bundle) {
                ctx = context;
                String nhMessage = bundle.getString("message");
                sendNotification(nhMessage);
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(nhMessage);
                }
            }
    
            private void sendNotification(String msg) {
    
                Intent intent = new Intent(ctx, MainActivity.class);
                intent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);
    
                mNotificationManager = (NotificationManager)
                        ctx.getSystemService(Context.NOTIFICATION_SERVICE);
    
                PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                        intent, PendingIntent.FLAG_ONE_SHOT);
    
                Uri defaultSoundUri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
                NotificationCompat.Builder mBuilder =
                        new NotificationCompat.Builder(ctx)
                                .setSmallIcon(R.mipmap.ic_launcher)
                                .setContentTitle("Notification Hub Demo")
                                .setStyle(new NotificationCompat.BigTextStyle()
                                        .bigText(msg))
                                .setSound(defaultSoundUri)
                                .setContentText(msg);
    
                mBuilder.setContentIntent(contentIntent);
                mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
            }
        }
12. Merhaba menü çubuğunda Android Studio'da sırasıyla **yapı** > **projeyi** toomake kodunuzda hiçbir hata bulunmadığından emin.

## <a name="sending-push-notifications"></a>Anında iletme bildirimleri gönderme
Merhaba göndererek uygulamanızda anında iletme bildirimleri almayı test edebilirsiniz [Azure Portal] -Merhaba Ara **sorun giderme** bölümünde hello hub dikey penceresinde, aşağıda gösterildiği gibi.

![Azure Notification Hubs - Test Gönderimi](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-hello-app"></a>(İsteğe bağlı) Doğrudan hello uygulamadan anında iletme bildirimleri gönderme
Normalde bildirimleri bir arka uç sunucusu kullanarak gönderirsiniz. Bazı durumlarda, toobe mümkün toosend anında iletme bildirimleri hello istemci uygulamasından doğrudan isteyebilirsiniz. Bu bölümde, nasıl toosend bildirimleri kullanan hello istemciden hello açıklanmaktadır [Azure bildirim hub'ı REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx).

1. Android Studio Proje Görünümü'nde, **App** > **src** > **main** > **res** > **layout**'u genişletin. Açık hello `activity_main.xml` düzeni dosya ve hello tıklatın **metin** sekmesinde hello dosyasının tooupdate hello metin içeriği. Aşağıdaki hello kodu ile yeni ekleyen güncelleştirmek `Button` ve `EditText` göndermek için denetimleri anında bildirim iletileri toohello bildirim hub'ı. Bu kod hello altındaki hemen önüne ekleyin `</RelativeLayout>`.
   
        <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:layout_centerVertical="true"
        android:layout_centerHorizontal="true"
        android:onClick="sendNotificationButtonOnClick" />
   
        <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_above="@+id/sendbutton"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="42dp"
        android:hint="@string/notification_message_hint" />
2. Android Studio Proje Görünümü'nde **App** > **src** > **main** > **res** > **values**'u genişletin. Açık hello `strings.xml` dosya ve hello yeni tarafından başvurulan hello dize değerlerini ekleyin `Button` ve `EditText` kontrol eder. Bunlar hello dosyasının hello altındaki hemen önüne ekleyin `</resources>`.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. İçinde `NotificationSetting.java` dosya, ayar toohello aşağıdaki hello eklemek `NotificationSettings` sınıfı.
   
    Güncelleştirme `HubFullAccess` hello ile **DefaultFullSharedAccessSignature** hub'ınız için bağlantı dizesi. Bu bağlantı dizesi hello kopyalanabilir [Azure Portal] tıklayarak **erişim ilkeleri** hello üzerinde **ayarları** dikey bildirim hub'ınız için.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. İçinde `MainActivity.java` dosya, hello aşağıdakileri ekleyin `import` deyimleri hello yukarıda `MainActivity` sınıfı.
   
        import java.io.BufferedOutputStream;
        import java.io.BufferedReader;
        import java.io.InputStreamReader;
        import java.io.OutputStream;
        import java.net.HttpURLConnection;
        import java.net.URL;
        import java.net.URLEncoder;
        import javax.crypto.Mac;
        import javax.crypto.spec.SecretKeySpec;
        import android.util.Base64;
        import android.view.View;
        import android.widget.EditText;
5. İçinde `MainActivity.java` dosya, üyeleri hello hello üstündeki aşağıdaki hello eklemek `MainActivity` sınıfı.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Bir POST isteği toosend iletileri tooyour bildirim hub'ı bir yazılım erişim imzası (SaS) belirteci tooauthenticate oluşturmanız gerekir. Bu hello anahtar veri hello bağlantı dizesinden ayrıştırarak yapılır ve ardından oluşturarak hello SaS belirteci hello belirtildiği gibi [ortak kavramlar](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API Başvurusu. koddan hello örnek bir uygulamadır.
   
    İçinde `MainActivity.java`, yöntem toohello aşağıdaki hello eklemek `MainActivity` tooparse bağlantı dizenizi sınıfı.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * tooparse hello connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be hello DefaultFullSharedAccess connection
         *                         string for this example.
         */
        private void ParseConnectionString(String connectionString)
        {
            String[] parts = connectionString.split(";");
            if (parts.length != 3)
                throw new RuntimeException("Error parsing connection string: "
                        + connectionString);
   
            for (int i = 0; i < parts.length; i++) {
                if (parts[i].startsWith("Endpoint")) {
                    this.HubEndpoint = "https" + parts[i].substring(11);
                } else if (parts[i].startsWith("SharedAccessKeyName")) {
                    this.HubSasKeyName = parts[i].substring(20);
                } else if (parts[i].startsWith("SharedAccessKey")) {
                    this.HubSasKeyValue = parts[i].substring(16);
                }
            }
        }
7. İçinde `MainActivity.java`, yöntem toohello aşağıdaki hello eklemek `MainActivity` sınıfı toocreate bir SaS kimlik doğrulama belirteci.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from hello access key tooauthenticate a request.
         *
         * @param uri hello unencoded resource URI string for this operation. hello resource
         *            URI is hello full URI of hello Service Bus resource toowhich access is
         *            claimed. For example,
         *            "http://<namespace>.servicebus.windows.net/<hubName>"
         */
        private String generateSasToken(String uri) {
   
            String targetUri;
            String token = null;
            try {
                targetUri = URLEncoder
                        .encode(uri.toString().toLowerCase(), "UTF-8")
                        .toLowerCase();
   
                long expiresOnDate = System.currentTimeMillis();
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60 * 1000;
                long expires = expiresOnDate / 1000;
                String toSign = targetUri + "\n" + expires;
   
                // Get an hmac_sha1 key from hello raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute hello hmac on input data bytes
                byte[] rawHmac = mac.doFinal(toSign.getBytes("UTF-8"));
   
                // Using android.util.Base64 for Android Studio instead of
                // Apache commons codec
                String signature = URLEncoder.encode(
                        Base64.encodeToString(rawHmac, Base64.NO_WRAP).toString(), "UTF-8");
   
                // Construct authorization string
                token = "SharedAccessSignature sr=" + targetUri + "&sig="
                        + signature + "&se=" + expires + "&skn=" + HubSasKeyName;
            } catch (Exception e) {
                if (isVisible) {
                    ToastNotify("Exception Generating SaS : " + e.getMessage().toString());
                }
            }
   
            return token;
        }
8. İçinde `MainActivity.java`, yöntemi toohello aşağıdaki hello eklemek `MainActivity` sınıfı toohandle hello **bildirim gönder** düğmesini tıklatın ve yerleşik REST API'sini kullanarak ileti toohello hub hello hello anında iletme bildirimi gönderin.
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added toohello Authorization header on hello POST request toothe
         * notification hub. hello text in hello editTextNotificationMessage control
         * is added as hello JSON body for hello request tooadd a GCM message toohello hub.
         *
         * @param v
         */
        public void sendNotificationButtonOnClick(View v) {
            EditText notificationText = (EditText) findViewById(R.id.editTextNotificationMessage);
            final String json = "{\"data\":{\"message\":\"" + notificationText.getText().toString() + "\"}}";
   
            new Thread()
            {
                public void run()
                {
                    try
                    {
                        // Based on reference documentation...
                        // http://msdn.microsoft.com/library/azure/dn223273.aspx
                        ParseConnectionString(NotificationSettings.HubFullAccess);
                        URL url = new URL(HubEndpoint + NotificationSettings.HubName +
                                "/messages/?api-version=2015-01");
   
                        HttpURLConnection urlConnection = (HttpURLConnection)url.openConnection();
   
                        try {
                            // POST request
                            urlConnection.setDoOutput(true);
   
                            // Authenticate hello POST request with hello SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer too: https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                            // urlConnection.setRequestProperty("ServiceBusNotification-Tags", 
                            //        "tag1 || tag2 || tag3");
   
                            // Send notification message
                            urlConnection.setFixedLengthStreamingMode(json.length());
                            OutputStream bodyStream = new BufferedOutputStream(urlConnection.getOutputStream());
                            bodyStream.write(json.getBytes());
                            bodyStream.close();
   
                            // Get reponse
                            urlConnection.connect();
                            int responseCode = urlConnection.getResponseCode();
                            if ((responseCode != 200) && (responseCode != 201)) {
                                BufferedReader br = new BufferedReader(new InputStreamReader((urlConnection.getErrorStream())));
                                String line;
                                StringBuilder builder = new StringBuilder("Send Notification returned " +
                                        responseCode + " : ")  ;
                                while ((line = br.readLine()) != null) {
                                    builder.append(line);
                                }
   
                                ToastNotify(builder.toString());
                            }
                        } finally {
                            urlConnection.disconnect();
                        }
                    }
                    catch(Exception e)
                    {
                        if (isVisible) {
                            ToastNotify("Exception Sending Notification : " + e.getMessage().toString());
                        }
                    }
                }
            }.start();
        }

## <a name="testing-your-app"></a>Uygulamanızı test etme
#### <a name="push-notifications-in-hello-emulator"></a>Merhaba öykünücüde anında iletme bildirimleri
Tootest anında iletme bildirimlerini bir öykünücüde isterseniz öykünücü görüntünüzün, uygulamanız için seçtiğiniz hello Google API düzeyini desteklediğinden emin olun. Görüntünüzü yerel Google API'lerini desteklemiyorsa, hello ile karşılaşırsınız **hizmet\_değil\_kullanılabilir** özel durum.

Buna ek olarak toohello yukarıdaki emin öykünücüsü altında çalışan, Google hesabı tooyour eklediğiniz **ayarları** > **hesapları**. Aksi takdirde, deneme tooregister GCM ile hello sonuçlanabilir **kimlik doğrulaması\_başarısız** özel durum.

#### <a name="running-hello-application"></a>Çalışan hello uygulama
1. Merhaba uygulamayı çalıştırın ve hello kayıt kimliği başarılı bir kaydı bildirdiğine dikkat edin.
   
      ![Android'de test etme - Kanal kaydı][18]
2. Merhaba hub'da kayıtlı Android cihazlar tooall gönderilen bir bildirim iletisi toobe girin.
   
      ![Andorid'de test etme - bir ileti gönderme][19]

3. **Bildirim Gönder**'e basın. Merhaba uygulamasının çalışıyor cihazlarını göstermeyecektir bir `AlertDialog` hello anında iletme bildirimi iletisi örneğiyle. Merhaba uygulamasının çalışıyor yoksa, ancak daha önce kaydolan cihazlar anında iletme bildirimleri için hello Android bildirim Yöneticisi bir bildirim alırsınız. Bu, hello sol üst köşeden aşağı çekilerek görüntülenebilir.
   
      ![Android'de test etme - bildirimler][21]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers] hello sonraki adım olarak Öğreticisi. Bunu nasıl kullanarak bir ASP.NET arka uç toosend bildirimleri etiketler tootarget belirli kullanıcılara gösterilir.

Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız, hello denetleyin [son dakika haberleri Notification Hubs kullanma toosend] Öğreticisi.

toolearn Notification Hubs hakkında daha fazla genel bilgi bizim [Notification Hubs Kılavuzu].

<!-- Images. -->
[6]: ./media/notification-hubs-android-get-started/notification-hub-android-new-class.png

[12]: ./media/notification-hubs-android-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-new-project.png
[14]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-choose-form-factor.png
[15]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app4.png
[16]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app5.png
[17]: ./media/notification-hubs-android-get-started/notification-hub-create-android-app6.png

[18]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-registered.png
[19]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-set-message.png

[20]: ./media/notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-received-message.png
[22]: ./media/notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/notification-hubs-android-get-started/notification-hub-scheduler2.png
[29]: ./media/mobile-services-android-get-started-push/mobile-eclipse-import-Play-library.png

[30]: ./media/notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png

[31]: ./media/notification-hubs-android-get-started/notification-hubs-android-studio-add-ui.png


<!-- URLs. -->
[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-android-get-started-push.md  
[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Referencing a library project]: http://go.microsoft.com/fwlink/?LinkId=389800
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs kullanma toopush bildirimleri toousers]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com
