---
title: "Azure Notification Hubs ile Android'e anında iletme bildirimleri gönderme | Microsoft Belgeleri"
description: "Bu öğreticide, Android cihazlarına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını öğrenirsiniz."
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
ms.openlocfilehash: 808fc10ef1ebb3288facbdf2e9e817b27d4fc6bc
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="sending-push-notifications-to-android-with-azure-notification-hubs"></a>Azure Notification Hubs ile Android'e anında iletme bildirimleri gönderme
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
> [!IMPORTANT]
> Bu konuda Google Cloud Messaging (GCM) ile anında iletme bildirimleri gösterilmektedir. Google Firebase Cloud Messaging (FCM) kullanıyorsanız bkz. [Azure Notification Hubs ve FCM ile Android’e anında iletme bildirimleri gönderme](notification-hubs-android-push-notification-google-fcm-get-started.md).
> 
> 

Bu öğreticide, bir Android uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağı gösterilir.
Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan bir Android uygulaması oluşturacaksınız.

[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Bu öğreticinin tamamlanan kodu GitHub'da [buradan](https://github.com/Azure/azure-notificationhubs-samples/tree/master/Android/GetStarted) indirilebilir.

## <a name="prerequisites"></a>Ön koşullar
> [!IMPORTANT]
> Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-android-get-started).
> 
> 

Yukarıda belirtilen etkin bir Azure hesabının yanı sıra, bu öğretici yalnızca [Android Studio](http://go.microsoft.com/fwlink/?LinkId=389797)'nun en son sürümünü gerektirir.

Bu öğreticiyi tamamlamak Android uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.

## <a name="creating-a-project-that-supports-google-cloud-messaging"></a>Google Cloud Messaging'i destekleyen bir proje oluşturma
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-a-new-notification-hub"></a>Yeni bir bildirim hub'ı yapılandırma
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   **Ayarlar** dikey penceresinde, **Bildirim Hizmetleri**'ni ve ardından **Google (GCM)** seçeneğini belirleyin. API anahtarını girin ve **Kaydet**'e tıklayın.

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

Bildirim hub'ınız şimdi GCM ile birlikte çalışmak üzere yapılandırıldı. Ayrıca, uygulamanızı anında iletme bildirimleri alması ve göndermesi amacıyla kaydetmek için bağlantı dizelerine sahipsiniz.

## <a id="connecting-app"></a>Uygulamanızı bildirim hub'ına bağlama
### <a name="create-a-new-android-project"></a>Yeni bir Android projesi oluşturma
1. Android Studio'da yeni bir Android Studio projesi başlatın.
   
   ![Android Studio - yeni proje][13]
2. **Telefon ve Tablet** form faktörünü ve desteklemek istediğiniz **Minimum SDK**'yı seçin. Ardından **İleri**'ye tıklayın.
   
   ![Android Studio - proje oluşturma iş akışı][14]
3. Ana etkinlik için **Boş Etkinlik**'i seçin, **İleri**'ye tıklayın ve ardından **Son**'a tıklayın.

### <a name="add-google-play-services-to-the-project"></a>Projeye Google Play hizmetlerini ekleme
[!INCLUDE [Add Play Services](../../includes/notification-hubs-android-studio-add-google-play-services.md)]

### <a name="adding-azure-notification-hubs-libraries"></a>Azure Notification Hubs kitaplıkları ekleme
1. **Uygulamanın** `Build.Gradle` dosyasında **bağımlılıklar** bölümüne aşağıdaki satırları ekleyin.
   
        compile 'com.microsoft.azure:notification-hubs-android-sdk:0.4@aar'
        compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@aar'
2. **Bağımlılıklar** bölümünden sonra aşağıdaki depoyu ekleyin.
   
        repositories {
            maven {
                url "http://dl.bintray.com/microsoftazuremobile/SDK"
            }
        }

### <a name="updating-the-androidmanifestxml"></a>AndroidManifest.xml'i güncelleştirme
1. GCM'yi desteklemek için kodumuza, [Google'ın Örnek Kimliği API'sini](https://developers.google.com/instance-id/) kullanarak [kayıt belirteçleri elde etmek](https://developers.google.com/cloud-messaging/android/client#sample-register) için kullanılan bir Örnek Kimliği dinleme hizmeti eklememiz gereklidir. Bu öğreticide sınıfa `MyInstanceIDService` adını vereceğiz. 
   
    Aşağıdaki hizmet tanımını AndroidManifest.xml dosyasında `<application>` etiketinin içine ekleyin. `<your package>` yer tutucusunu, `AndroidManifest.xml` dosyasının üst kısmında gösterilen asıl paket adınızla değiştirin.
   
        <service android:name="<your package>.MyInstanceIDService" android:exported="false">
            <intent-filter>
                <action android:name="com.google.android.gms.iid.InstanceID"/>
            </intent-filter>
        </service>
2. Örnek Kimliği API'sinden GCM kayıt belirtecimizi aldıktan sonra, [Azure Notification Hubs'a kaydolmak](notification-hubs-push-notification-registration-management.md) için bu belirteci kullanacağız. `RegistrationIntentService` adlı bir `IntentService` kullanarak bu kaydı arka planda destekleyeceğiz. Bu hizmet, [GCM kayıt belirtecimizi yenilemekten](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) de sorumludur.
   
    Aşağıdaki hizmet tanımını AndroidManifest.xml dosyasında `<application>` etiketinin içine ekleyin. `<your package>` yer tutucusunu, `AndroidManifest.xml` dosyasının üst kısmında gösterilen asıl paket adınızla değiştirin. 
   
        <service
            android:name="<your package>.RegistrationIntentService"
            android:exported="false">
        </service>
3. Bildirimleri almak için bir alıcı da tanımlayacağız. Aşağıdaki alıcı tanımını AndroidManifest.xml dosyasına `<application>` etiketinin içine ekleyin. `<your package>` yer tutucusunu, `AndroidManifest.xml` dosyasının üst kısmında gösterilen asıl paket adınızla değiştirin.
   
        <receiver android:name="com.microsoft.windowsazure.notifications.NotificationsBroadcastReceiver"
            android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your package name>" />
            </intent-filter>
        </receiver>
4. Aşağıdak GCM ile ilgili gerekli izinleri `</application>` etiketinin altına ekleyin. `<your package>` öğesini, `AndroidManifest.xml` dosyasının üst kısmında gösterilen paket adıyla değiştirdiğinizden emin olun.
   
    Bu izinler hakkında daha fazla bilgi için bkz. [Android için bir GCM İstemcisi uygulaması kurma](https://developers.google.com/cloud-messaging/android/client#manifest).
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
   
        <permission android:name="<your package>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your package>.permission.C2D_MESSAGE"/>

### <a name="adding-code"></a>Kod ekleme
1. Proje Görünümü'nde **app** > **src** > **main** > **java**'yı genişletin. **Java**'nın altındaki paket klasörünüze sağ tıklayın, **Yeni**'ye tıklayın ve ardından **Java Sınıfı**'na tıklayın. `NotificationSettings` adlı yeni bir sınıf ekleyin. 
   
    ![Android Studio - yeni Java sınıfı][6]
   
    Aşağıdaki kodda `NotificationSettings` sınıfı için bu üç yer tutucuyu güncelleştirdiğinizden emin olun:
   
   * **SenderId**: Daha önce [Google Cloud Console](http://cloud.google.com/console)'da elde ettiğiniz proje numarası.
   * **HubListenConnectionString**: Hub'ınız için **DefaultListenAccessSignature** bağlantı dizesi. [Azure Portal]'da hub'ınızın **Ayarlar** dikey penceresinde bulunan **Erişim İlkeleri**'ne tıklayarak bağlantı dizesini kopyalayabilirsiniz.
   * **HubName**: [Azure Portal]'daki hub dikey penceresinde görünen bildirim hub'ınızın adını kullanın.
     
     `NotificationSettings` kodu:
     
       public class NotificationSettings {
     
           public static String SenderId = "<Your project number>";
           public static String HubName = "<Your HubName>";
           public static String HubListenConnectionString = "<Your default listen connection string>";
       }
2. Yukarıdaki adımları kullanarak `MyInstanceIDService` adlı yeni bir sınıf daha ekleyin. Bu bizim Örnek Kimliği dinleme hizmeti uygulamamız olacak.
   
    Bu sınıfın kodu, arka planda `IntentService`GCM belirtecini yenileme[ amacıyla ](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) öğemizi çağırır.
   
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


1. `RegistrationIntentService` adlı projenize, başka bir yeni sınıf ekleyin. Bu, [GCM belirtecini yenileme](https://developers.google.com/instance-id/guides/android-implementation#refresh_tokens) ve [bildirim hub'ıyla kayıt yapma](notification-hubs-push-notification-registration-management.md) işlemlerini ele alacak `IntentService` hizmetimizin uygulanması olacak.
   
    Bu sınıf için aşağıdaki kod kullanın.
   
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
   
                    // Storing the registration id that indicates whether the generated token has been
                    // sent to your server. If it is not stored, send the token to your server,
                    // otherwise your server should have already received the token.
                    if ((regID=sharedPreferences.getString("registrationID", null)) == null) {        
                        NotificationHub hub = new NotificationHub(NotificationSettings.HubName,
                                NotificationSettings.HubListenConnectionString, this);
                        Log.i(TAG, "Attempting to register with NH using token : " + token);
   
                        regID = hub.register(token).getRegistrationId();
   
                        // If you want to use tags...
                        // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
                        // regID = hub.register(token, "tag1", "tag2").getRegistrationId();
   
                        resultString = "Registered Successfully - RegId : " + regID;
                        Log.i(TAG, resultString);        
                        sharedPreferences.edit().putString("registrationID", regID ).apply();
                    } else {
                        resultString = "Previously Registered Successfully - RegId : " + regID;
                    }
                } catch (Exception e) {
                    Log.e(TAG, resultString="Failed to complete token refresh", e);
                    // If an exception happens while fetching the new token or updating our registration data
                    // on a third-party server, this ensures that we'll attempt the update at a later time.
                }
   
                // Notify UI that registration has completed.
                if (MainActivity.isVisible) {
                    MainActivity.mainActivity.ToastNotify(resultString);
                }
            }
        }
2. `MainActivity` sınıfınızda aşağıdaki `import` deyimlerini sınıf bildiriminin üstüne ekleyin.
   
        import com.google.android.gms.common.ConnectionResult;
        import com.google.android.gms.common.GoogleApiAvailability;
        import com.google.android.gms.gcm.*;
        import com.microsoft.windowsazure.notifications.NotificationsManager;
        import android.util.Log;
        import android.widget.TextView;
        import android.widget.Toast;
3. Aşağıdaki özel üyeleri sınıfın en üst kısmına ekleyin. [Google Play Hizmetleri'nin kullanılabilirliğini Google tarafından önerildiği şekilde denetlemek](https://developers.google.com/android/guides/setup#ensure_devices_have_the_google_play_services_apk) için bunları kullanırız.
   
        public static MainActivity mainActivity;
        public static Boolean isVisible = false;    
        private GoogleCloudMessaging gcm;
        private static final int PLAY_SERVICES_RESOLUTION_REQUEST = 9000;
4. `MainActivity` sınıfınızda Google Play Hizmetleri'nin kullanılabilirliğine aşağıdaki yöntemi ekleyin. 
   
        /**
         * Check the device to make sure it has the Google Play Services APK. If
         * it doesn't, display a dialog that allows users to download the APK from
         * the Google Play Store or enable it in the device's system settings.
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
5. `MainActivity` sınıfınızda, GCM kayıt belirtecinizi almak ve bildirim hub'ınızla kaydolmak için `IntentService` öğenizi çağırmadan önce Google Play Hizmetleri'ni denetleyecek aşağıdaki kodu ekleyin.
   
        public void registerWithNotificationHubs()
        {
            Log.i(TAG, " Registering with Notification Hubs");
   
            if (checkPlayServices()) {
                // Start IntentService to register this application with GCM.
                Intent intent = new Intent(this, RegistrationIntentService.class);
                startService(intent);
            }
        }
6. `MainActivity` sınıfının `OnCreate` yönteminde, etkinlik oluşturulduğunda kayıt işlemini başlatmak için aşağıdaki kodu ekleyin.
   
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);
   
            mainActivity = this;
            NotificationsManager.handleNotifications(this, NotificationSettings.SenderId, MyHandler.class);
            registerWithNotificationHubs();
        }
7. Uygulama durumunu doğrulamak ve uygulamanızda durumu raporlamak için bu ek yöntemleri `MainActivity` öğesine ekleyin.
   
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
8. `ToastNotify` yöntemi, uygulamada kalıcı olarak durumu ve bildirimleri raporlamak için *"Hello World"* `TextView` denetimini kullanır. activity_main.xml düzeninizde bu denetim için aşağıdaki kimliği ekleyin.
   
       android:id="@+id/text_hello"
9. Ardından, AndroidManifest.xml'de tanımladığımız alıcımız için bir alt sınıf ekleyeceğiz. `MyHandler` adlı projenize başka bir yeni sınıf ekleyin.
10. `MyHandler.java`'in üst kısmına şu içeri aktarma deyimlerini ekleyin:
    
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.os.Bundle;
        import android.support.v4.app.NotificationCompat;
        import com.microsoft.windowsazure.notifications.NotificationsHandler;
11. `MyHandler` sınıfı için aşağıdaki kodu ekleyip bunu `com.microsoft.windowsazure.notifications.NotificationsHandler` öğesinin bir alt sınıfı haline getirin.
    
    Bu kod, `OnReceive` yöntemini geçersiz kılar; böylece işleyici alınan bildirimleri raporlar. İşleyici, `sendNotification()` yöntemini kullanarak Android bildirim yöneticisine anında iletme bildirimi gönderir. `sendNotification()` yöntemi, uygulama çalışmıyorken ve bir bildirim alındığında yürütülmelidir.
    
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
12. Android Studio'nun menü çubuğunda, kodunuzda hiçbir hata bulunmadığından emin olmak için **Oluştur** > **Projeyi Yeniden Oluştur**'a tıklayın.

## <a name="sending-push-notifications"></a>Anında iletme bildirimleri gönderme
Uygulamanızda anında iletme bildirimlerini aldığınızı, bunları [Azure Portal] aracılığıyla göndererek test edebilirsiniz; aşağıda gösterildiği gibi hub dikey penceresinin **Sorun Giderme** Bölümü'nü bulun.

![Azure Notification Hubs - Test Gönderimi](./media/notification-hubs-android-get-started/notification-hubs-test-send.png)

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-directly-from-the-app"></a>(İsteğe bağlı) Doğrudan uygulamadan anında iletme bildirimleri gönderme
Normalde bildirimleri bir arka uç sunucusu kullanarak gönderirsiniz. Bazı durumlarda, anında iletme bildirimlerini doğrudan istemci uygulamasından gönderebilmek isteyebilirsiniz. Bu bölüm, [Azure Notification Hubs REST API'si](https://msdn.microsoft.com/library/azure/dn223264.aspx) kullanarak istemciden nasıl bildirim gönderildiğini açıklamaktadır.

1. Android Studio Proje Görünümü'nde, **App** > **src** > **main** > **res** > **layout**'u genişletin. `activity_main.xml` düzen dosyasını açın ve dosyanın metin içeriğini güncelleştirmek için **Metin** sekmesine tıklayın. Bildirim hub'ına anında iletme bildirimi iletileri göndermek için yeni `Button` ve `EditText` denetimlerini ekleyen aşağıdaki kod ile güncelleştirin. Bu kodu en alta, `</RelativeLayout>` öğesinin hemen önüne ekleyin.
   
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
2. Android Studio Proje Görünümü'nde **App** > **src** > **main** > **res** > **values**'u genişletin. `strings.xml` dosyasını açın ve yeni `Button` ve `EditText` denetimleri tarafından başvurulan dize değerlerini ekleyin. Bunları dosyanın en altına, `</resources>` öğesinin hemen önüne ekleyin.
   
        <string name="send_button">Send Notification</string>
        <string name="notification_message_hint">Enter notification message text</string>
3. `NotificationSetting.java` dosyanızda `NotificationSettings` sınıfına aşağıdaki ayarı ekleyin.
   
    `HubFullAccess` öğesini, **DefaultFullSharedAccessSignature** bağlantı dizesiyle hub'ınız için güncelleştirin. Bu bağlantı dizesi, bildirim hub'ınızın **Ayarlar** dikey penceresinde **Erişim İlkeleri**'ne tıklanarak [Azure Portal]'dan kopyalanabilir.
   
        public static String HubFullAccess = "<Enter Your DefaultFullSharedAccess Connection string>";
4. `MainActivity.java` dosyanızda aşağıdaki `import` deyimlerini `MainActivity` sınıfının üstüne ekleyin.
   
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
5. `MainActivity.java` dosyanızda aşağıdaki üyeleri `MainActivity` sınıfının üstüne ekleyin.    
   
        private String HubEndpoint = null;
        private String HubSasKeyName = null;
        private String HubSasKeyValue = null;
6. Bildirim hub'ınıza ileti göndermek amacıyla bir POST isteğinin kimlik doğrulamasını yapmak için bir Yazılım Erişim İmzası (SaS) belirteci oluşturmanız gerekir. Bu, anahtar verilerini bağlantı dizesinden ayrıştırarak ve ardından [Ortak Kavramlar](http://msdn.microsoft.com/library/azure/dn495627.aspx) REST API'si başvurusunda belirtildiği gibi SaS belirtecini oluşturarak yapılır. Aşağıdaki kod örnek bir uygulamadır.
   
    Bağlantı dizenizi ayrıştırmak için `MainActivity.java` öğesinde aşağıdaki yöntemi `MainActivity` sınıfına ekleyin.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx
         * to parse the connection string so a SaS authentication token can be
         * constructed.
         *
         * @param connectionString This must be the DefaultFullSharedAccess connection
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
7. Bir SaS kimlik doğrulaması belirteci oluşturmak için `MainActivity.java` öğesinde aşağıdaki yöntemi `MainActivity` sınıfına ekleyin.
   
        /**
         * Example code from http://msdn.microsoft.com/library/azure/dn495627.aspx to
         * construct a SaS token from the access key to authenticate a request.
         *
         * @param uri The unencoded resource URI string for this operation. The resource
         *            URI is the full URI of the Service Bus resource to which access is
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
   
                // Get an hmac_sha1 key from the raw key bytes
                byte[] keyBytes = HubSasKeyValue.getBytes("UTF-8");
                SecretKeySpec signingKey = new SecretKeySpec(keyBytes, "HmacSHA256");
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                Mac mac = Mac.getInstance("HmacSHA256");
                mac.init(signingKey);
   
                // Compute the hmac on input data bytes
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
8. **Bildirim Gönder** düğmesine tıklanmasını ele almak ve yerleşik REST API'sini kullanarak hub'a anında iletme bildirimi iletisi göndermek için `MainActivity.java` öğesinde `MainActivity` sınıfına aşağıdaki yöntemi ekleyin.
   
        /**
         * Send Notification button click handler. This method parses the
         * DefaultFullSharedAccess connection string and generates a SaS token. The
         * token is added to the Authorization header on the POST request to the
         * notification hub. The text in the editTextNotificationMessage control
         * is added as the JSON body for the request to add a GCM message to the hub.
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
   
                            // Authenticate the POST request with the SaS token
                            urlConnection.setRequestProperty("Authorization", 
                                generateSasToken(url.toString()));
   
                            // Notification format should be GCM
                            urlConnection.setRequestProperty("ServiceBusNotification-Format", "gcm");
   
                            // Include any tags
                            // Example below targets 3 specific tags
                            // Refer to : https://azure.microsoft.com/en-us/documentation/articles/notification-hubs-routing-tag-expressions/
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
#### <a name="push-notifications-in-the-emulator"></a>Öykünücüde anında iletme bildirimleri
Anında iletme bildirimlerini bir öykünücüde test etmek isterseniz öykünücü görüntünüzün, uygulamanız için seçtiğiniz Google API düzeyini desteklediğinden emin olun. Görüntünüz yerel Google API'lerini desteklemiyorsa **HİZMET\_\_KULLANILAMIYOR** özel durumuyla karşılaşırsınız.

Yukarıdakine ek olarak, **Ayarlar** > **Hesaplar**'ın altında çalışan öykünücünüze Google hesabınızı eklediğinizden emin olun. Aksi halde, GCM ile kayıt girişimleriniz **KİMLİK DOĞRULAMASI\_BAŞARISIZ** özel durumuyla sonuçlanabilir.

#### <a name="running-the-application"></a>Uygulamayı çalıştırma
1. Uygulamayı çalıştırın ve kayıt kimliğinin başarılı bir kaydı bildirdiğine dikkat edin.
   
      ![Android'de test etme - Kanal kaydı][18]
2. Hub'da kayıtlı tüm Android cihazlara gönderilecek bir bildirim iletisi girin.
   
      ![Andorid'de test etme - bir ileti gönderme][19]

3. **Bildirim Gönder**'e basın. Uygulamayı çalıştıran tüm cihazlarda, anında iletme bildirimi iletisiyle birlikte bir `AlertDialog` örneği görünür. Uygulamayı çalıştırmayan ancak anında iletme bildirimleri için daha önce kaydolan cihazlar, Android Bildirim Yöneticisi'nde bir bildirim alır. Bunlar, sol üst köşeden aşağı çekilerek görüntülenebilir.
   
      ![Android'de test etme - bildirimler][21]

## <a name="next-steps"></a>Sonraki adımlar
Sonraki adım olarak [Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma] öğreticisini öneririz. Bu, belirli kullanıcıları hedeflemek için etiketler kullanarak ASP.NET arka ucundan nasıl bildirim göndereceğinizi gösterir.

Kullanıcılarınızı ilgi alanı gruplarına göre segmentlere ayırmak istiyorsanız [Son dakika haberleri göndermek için Notification Hubs kullanma] öğreticisine göz atın.

Notification Hubs hakkında daha fazla genel bilgi edinmek için bkz. [Notification Hubs Kılavuzu].

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
[Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma]: notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md
[Son dakika haberleri göndermek için Notification Hubs kullanma]: notification-hubs-aspnet-backend-android-xplat-segmented-gcm-push-notification.md
[Azure Portal]: https://portal.azure.com
