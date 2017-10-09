---
title: "aaaGet Kindle uygulamaları için Azure Notification Hubs ile çalışmaya | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooa Kindle uygulaması öğrenin."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 346fc8e5-294b-4e4f-9f27-7a82d9626e93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-kindle
ms.devlang: Java
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c28d64372cd2d90bab9cd9bf818d333f3478f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a>Kindle uygulamaları için Notification Hubs'ı kullanmaya başlama
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooa Kindle uygulaması gösterir.
Amazon Device Messaging'i (ADM) kullanarak anında iletme bildirimleri alan boş bir Kindle uygulaması oluşturacaksınız.

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici hello aşağıdakileri gerektirir:

* Hello Hello Android (varsayıyoruz Eclipse kullanacağınızı) SDK'sı Al <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.
* Merhaba adımları <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">ayarı yukarı geliştirme ortamınıza</a> tooset Kindle için geliştirme ortamınızı ayarlama.

## <a name="add-a-new-app-toohello-developer-portal"></a>Yeni bir uygulama toohello Geliştirici Portalı ekleme
1. İlk olarak, bir uygulama hello oluşturmak [Amazon Geliştirici Portalı].
   
    ![][0]
2. Kopya hello **uygulama anahtarı**.
   
    ![][1]
3. Merhaba portalında uygulamanızı hello adına tıklayın ve hello ardından **Device Messaging** sekmesi.
   
    ![][2]
4. **Create a New Security Profile** (Yeni Bir Güvenlik Profili Oluştur) seçeneğine tıklayın ve ardından yeni bir güvenlik profili oluşturun (örneğin, **TestAdm güvenlik profili**). Daha sonra **Kaydet**'e tıklayın.
   
    ![][3]
5. Tıklatın **güvenlik profilleri** oluşturduğunuz tooview hello güvenlik profili. Kopya hello **istemci kimliği** ve **gizli** daha sonra kullanmak için değerler.
   
    ![][4]

## <a name="create-an-api-key"></a>API Anahtarı oluşturma
1. Yönetici ayrıcalıklarına sahip bir komut istemi açın.
2. Toohello Android SDK klasörüne gidin.
3. Merhaba aşağıdaki komutu girin:
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. Hello için **keystore** parola, türü **android**.
5. Kopya hello **MD5** parmak izi.
6. Merhaba üzerinde hello Geliştirici Portalı'nda geri **ileti** sekmesini tıklatın, **Android/Kindle** ve uygulamanız için hello hello paket adını girin (örneğin, **com.sample.notificationhubtest**) ve hello **MD5** değer ve ardından **API anahtarı oluştur**.

## <a name="add-credentials-toohello-hub"></a>Kimlik bilgileri toohello hub ekleme
Merhaba portalında hello istemci gizli anahtarı ve istemci kimliği toohello ekleme **yapılandırma** bildirim hub'ınızın sekmesi.

## <a name="set-up-your-application"></a>Uygulamanızı ayarlama
> [!NOTE]
> Bir uygulama oluştururken, en az API Düzeyi 17 kullanın.
> 
> 

Merhaba ADM kitaplıkları tooyour Eclipse projenizin ekleyin:

1. tooobtain hello ADM kitaplığını [hello SDK Yükle]. Merhaba SDK zip dosyasını ayıklayın.
2. Eclipse'te, projenize sağ tıklayın ve ardından **Properties** (Özellikler) seçeneğine tıklayın. Seçin **Java oluşturma yolu** sol hello ve ardından hello ** kitaplıkları ** sekmesini hello üstünde. Tıklatın **dış Jar Ekle**ve select hello dosya `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` hello Amazon SDK'sını ayıkladığınız hello dizininden.
3. Merhaba NotificationHubs Android SDK (bağlantı) indirin.
4. Merhaba paketin sıkıştırmasını açın ve sonra hello dosyayı sürükleyin `notification-hubs-sdk.jar` hello içine `libs` Eclipse klasöründe.

Uygulama bildirimi toosupport ADM düzenleyin:

1. Merhaba Amazon ad hello kök bildirim öğesine ekleyin:

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. Merhaba hello bildirim öğesinin altına ilk öğe olarak izinleri ekleyin. Yedek **[YOUR PACKAGE NAME]** uygulamanızı toocreate kullanılan hello Paketle.
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access tooreceive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK tookeep hello processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. Hello hello uygulama öğesinin ilk alt öğesi aşağıdaki hello ekleyin. Toosubstitute unutmayın **[YOUR SERVICE NAME]** hello sonraki bölümde (dahil olmak üzere hello paketi) oluşturmak ve değiştirmek ADM ileti işleyicinizi hello adıyla **[YOUR PACKAGE NAME]** hello ile Uygulamanızı oluşturduğunuz paket adı.
   
        <amazon:enable-feature
              android:name="com.amazon.device.messaging"
                     android:required="true"/>
        <service
            android:name="[YOUR SERVICE NAME]"
            android:exported="false" />
   
        <receiver
            android:name="[YOUR SERVICE NAME]$Receiver" />
   
            <!-- This permission ensures that only ADM can send your app registration broadcasts. -->
            android:permission="com.amazon.device.messaging.permission.SEND" >
   
            <!-- toointeract with ADM, your app must listen for hello following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace hello name in hello category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a>ADM ileti işleyicinizi oluşturma
1. Öğesinden devralınan yeni bir sınıf oluşturun `com.amazon.device.messaging.ADMMessageHandlerBase` ve adlandırın `MyADMMessageHandler`hello aşağıdaki şekilde gösterildiği gibi:
   
    ![][6]
2. Merhaba aşağıdakileri ekleyin `import` deyimleri:
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. Oluşturduğunuz hello sınıfında koddan hello ekleyin. Toosubstitute hello hub adını ve bağlantı dizesini (Dinleme) unutmayın:
   
        public static final int NOTIFICATION_ID = 1;
        private NotificationManager mNotificationManager;
        NotificationCompat.Builder builder;
          private static NotificationHub hub;
        public static NotificationHub getNotificationHub(Context context) {
            Log.v("com.wa.hellokindlefire", "getNotificationHub");
            if (hub == null) {
                hub = new NotificationHub("[hub name]", "[listen connection string]", context);
            }
            return hub;
        }
   
        public MyADMMessageHandler() {
                super("MyADMMessageHandler");
            }
   
            public static class Receiver extends ADMMessageReceiver
            {
                public Receiver()
                {
                    super(MyADMMessageHandler.class);
                }
            }
   
            private void sendNotification(String msg) {
                Context ctx = getApplicationContext();
   
                mNotificationManager = (NotificationManager)
                    ctx.getSystemService(Context.NOTIFICATION_SERVICE);
   
            PendingIntent contentIntent = PendingIntent.getActivity(ctx, 0,
                  new Intent(ctx, MainActivity.class), 0);
   
            NotificationCompat.Builder mBuilder =
                  new NotificationCompat.Builder(ctx)
                  .setSmallIcon(R.mipmap.ic_launcher)
                  .setContentTitle("Notification Hub Demo")
                  .setStyle(new NotificationCompat.BigTextStyle()
                         .bigText(msg))
                  .setContentText(msg);
   
             mBuilder.setContentIntent(contentIntent);
             mNotificationManager.notify(NOTIFICATION_ID, mBuilder.build());
        }
4. Aşağıdaki kodu toohello hello eklemek `OnMessage()` yöntemi:
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. Aşağıdaki kodu toohello hello eklemek `OnRegistered` yöntemi:
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. Aşağıdaki kodu toohello hello eklemek `OnUnregistered` yöntemi:
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. Merhaba, `MainActivity` yöntemi, içeri aktarma deyimini aşağıdaki hello ekleyin:
   
        import com.amazon.device.messaging.ADM;
8. Merhaba hello sonunda koddan hello eklemek `OnCreate` yöntemi:
   
        final ADM adm = new ADM(this);
        if (adm.getRegistrationId() == null)
        {
           adm.startRegister();
        } else {
            new AsyncTask() {
                  @Override
                  protected Object doInBackground(Object... params) {
                     try {                         MyADMMessageHandler.getNotificationHub(getApplicationContext()).register(adm.getRegistrationId());
                     } catch (Exception e) {
                         Log.e("com.wa.hellokindlefire", "Failed registration with hub", e);
                         return e;
                     }
                     return null;
                 }
               }.execute(null, null, null);
        }

## <a name="add-your-api-key-tooyour-app"></a>API anahtar tooyour uygulamanızı ekleme
1. Eclipse'te, adlı yeni bir dosya oluşturun **api_key.txt** hello projenizin dizin varlıkları içinde.
2. Merhaba Amazon Geliştirici Portalı'nda oluşturulan hello dosya ve kopyalama hello API anahtarı açın.

## <a name="run-hello-app"></a>Merhaba uygulamayı çalıştırma
1. Merhaba öykünücüsünde başlatın.
2. Merhaba üstten Hello öykünücüsünde içeri doğru çekin ve tıklayın **ayarları**ve ardından **Hesabımı** ve geçerli bir Amazon hesabıyla kaydolun.
3. Eclipse'te, hello uygulamayı çalıştırın.

> [!NOTE]
> Bir sorun oluşursa, başlangıç saati hello öykünücü (veya aygıt) denetleyin. Merhaba zaman değerinin doğru olması gerekir. Merhaba Kindle öykünücüsü toochange başlangıç saati, çalıştırabilirsiniz hello komutu, Android SDK platformunuzun Araçlar dizininden aşağıdaki:
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a>İleti gönderme
.NET kullanarak ileti toosend:

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
[Amazon Geliştirici Portalı]: https://developer.amazon.com/home.html
[hello SDK Yükle]: https://developer.amazon.com/public/resources/development-tools/sdk

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
