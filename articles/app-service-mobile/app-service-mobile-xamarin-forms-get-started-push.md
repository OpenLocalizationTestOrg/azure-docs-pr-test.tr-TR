---
title: "aaaAdd anında iletme bildirimleri tooyour Xamarin.Forms uygulaması | Microsoft Docs"
description: "Toosend birden çok platform anında iletme bildirimleri tooyour Xamarin.Forms uygulamaları nasıl toouse Azure hizmetleri hakkında bilgi edinin."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: d9b1ba9a-b3f2-4d12-affc-2ee34311538b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 9133a0b6dd99c01def525607c20ce5a9c19b9502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a>Anında iletme bildirimleri tooyour Xamarin.Forms uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, hello sonuçlandı anında iletme bildirimleri tooall hello projelerine ekleme [Xamarin.Forms Hızlı Başlangıç](app-service-mobile-xamarin-forms-get-started.md). Bu, bir kayda eklenen her zaman bir anında iletme bildirimi tooall platformlar arası istemcileri gönderilen anlamına gelir.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello. Daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Ön koşullar
İOS için size gereken bir [Apple Developer Program üyeliği](https://developer.apple.com/programs/ios/) ve fiziksel bir iOS cihazına. Merhaba [iOS simülatörü anında iletme bildirimlerini desteklemiyor](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).

## <a name="configure-hub"></a>Bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Güncelleştirme Hello sunucu projesi toosend anında iletme bildirimleri
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a>Yapılandırma ve hello (isteğe bağlı) Android projesi çalıştırma
Bu bölümde tooenable anında iletme bildirimlerinin hello Xamarin.Forms Android projesi Android için tamamlayın.

### <a name="enable-firebase-cloud-messaging-fcm"></a>Firebase Cloud Messaging'i (FCM) etkinleştirme
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a>Merhaba Mobile Apps arka uç toosend gönderme istekleri FCM kullanarak yapılandırma
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a>Anında iletme bildirimleri toohello Android projesi ekleme
FCM ile yapılandırılmış hello arka ucu ile bileşenleri ve kodları toohello istemci tooregister FCM ile ekleyebilirsiniz. Mobile Apps sonlandırmak ve bildirimlerin hello aracılığıyla Azure Notification Hubs ile anında iletme bildirimleri için kaydedebilirsiniz.

1. Merhaba, **Droid** proje, hello sağ tıklatın **bileşenleri** klasörü ve tıklatın **daha almak bileşenleri...** . Merhaba arama **Google Cloud Messaging istemcisi** bileşeni ve toohello proje ekleyin. Bu bileşen, bir Xamarin Android projesi için anında iletme bildirimleri destekler.
2. Merhaba MainActivity.cs proje dosyasını açın ve aşağıdaki ifadeyi hello dosyanın üst kısmındaki hello hello ekleyin:

        using Gcm.Client;
3. Aşağıdaki kodu toohello hello eklemek **OnCreate** hello sonra yöntemini çağırın çok**LoadApplication**:

        try
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);

            // Register for push notifications
            System.Diagnostics.Debug.WriteLine("Registering...");
            GcmClient.Register(this, PushHandlerBroadcastReceiver.SENDER_IDS);
        }
        catch (Java.Net.MalformedURLException)
        {
            CreateAndShowDialog("There was an error creating hello client. Verify hello URL.", "Error");
        }
        catch (Exception e)
        {
            CreateAndShowDialog(e.Message, "Error");
        }
4. Yeni bir ekleme **CreateAndShowDialog** yardımcı yöntemi, aşağıdaki gibi:

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. Aşağıdaki kodu toohello hello eklemek **MainActivity** sınıfı:

        // Create a new instance field for this activity.
        static MainActivity instance = null;

        // Return hello current activity instance.
        public static MainActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }

    Bu hello geçerli sunan **MainActivity** örnek biz hello ana kullanıcı Arabirimi iş parçacığı üzerinde çalıştırabilirsiniz.
6. Merhaba başlatma `instance` hello hello başında değişken **OnCreate** şekilde yöntemi.

        // Set hello current instance of MainActivity.
        instance = this;
7. Yeni bir sınıf dosya toohello ekleme **Droid** adlı projesi `GcmService.cs`ve hello aşağıdakilerden emin olun **kullanarak** deyimleri mevcut hello dosya hello üstünde:

        using Android.App;
        using Android.Content;
        using Android.Media;
        using Android.Support.V4.App;
        using Android.Util;
        using Gcm.Client;
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Text;
8. Merhaba dosyasının hello üstünde izin istekleri hello sonra aşağıdaki hello eklemek **kullanarak** deyimleri ve hello önce **ad alanı** bildirimi.

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. Sınıf tanımı toohello namespace aşağıdaki hello ekleyin.

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > Değiştir **< PROJECT_NUMBER >** not ettiğiniz daha önce proje numarası ile.    
   >
   >
10. Merhaba boş Değiştir **GcmService** hello yeni yayın alıcı kullanan kodu aşağıdaki hello sınıfıyla:

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. Aşağıdaki kodu toohello hello eklemek **GcmService** sınıfı. Bu hello geçersiz kılar **OnRegistered** olay işleyicisi ve uygulayan bir **kaydetmek** yöntemi.

        protected override void OnRegistered(Context context, string registrationId)
        {
            Log.Verbose("PushHandlerBroadcastReceiver", "GCM Registered: " + registrationId);
            RegistrationID = registrationId;

            var push = TodoItemManager.DefaultManager.CurrentClient.GetPush();

            MainActivity.CurrentActivity.RunOnUiThread(() => Register(push, null));
        }

        public async void Register(Microsoft.WindowsAzure.MobileServices.Push push, IEnumerable<string> tags)
        {
            try
            {
                const string templateBodyGCM = "{\"data\":{\"message\":\"$(messageParam)\"}}";

                JObject templates = new JObject();
                templates["genericMessage"] = new JObject
                {
                    {"body", templateBodyGCM}
                };

                await push.RegisterAsync(RegistrationID, templates);
                Log.Info("Push Installation Id", push.InstallationId.ToString());
            }
            catch (Exception ex)
            {
                System.Diagnostics.Debug.WriteLine(ex.Message);
                Debugger.Break();
            }
        }

    Bu kod hello kullandığına dikkat edin `messageParam` hello şablonu kayıt parametresi.
12. Uygulayan kod aşağıdaki hello eklemek **Onmessageoptions**:

        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info("PushHandlerBroadcastReceiver", "GCM Message Received!");

            var msg = new StringBuilder();

            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }

            //Store hello message
            var prefs = GetSharedPreferences(context.PackageName, FileCreationMode.Private);
            var edit = prefs.Edit();
            edit.PutString("last_msg", msg.ToString());
            edit.Commit();

            string message = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty(message))
            {
                createNotification("New todo item!", "Todo item: " + message);
                return;
            }

            string msg2 = intent.Extras.GetString("msg");
            if (!string.IsNullOrEmpty(msg2))
            {
                createNotification("New hub message!", msg2);
                return;
            }

            createNotification("Unknown message details", msg.ToString());
        }

        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;

            //Create an intent tooshow ui
            var uiIntent = new Intent(this, typeof(MainActivity));

            //Use Notification Builder
            NotificationCompat.Builder builder = new NotificationCompat.Builder(this);

            //Create hello notification
            //we use hello pending intent, passing our ui intent over which will get called
            //when hello notification is tapped.
            var notification = builder.SetContentIntent(PendingIntent.GetActivity(this, 0, uiIntent, 0))
                    .SetSmallIcon(Android.Resource.Drawable.SymActionEmail)
                    .SetTicker(title)
                    .SetContentTitle(title)
                    .SetContentText(desc)

                    //Set hello notification sound
                    .SetSound(RingtoneManager.GetDefaultUri(RingtoneType.Notification))

                    //Auto cancel will remove hello notification once hello user touches it
                    .SetAutoCancel(true).Build();

            //Show hello notification
            notificationManager.Notify(1, notification);
        }

    Bu gelen bildirimlerini işleme ve görüntülenen toohello bildirim Yöneticisi toobe gönderir.
13. **GcmServiceBase** de tooimplement hello gerektirir **OnUnRegistered** ve **OnError** şu şekilde yapabilirsiniz işleyici yöntemleri:

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

Şimdi, bir Android cihazında çalıştırılan hello uygulamasında anında iletme bildirimleri hazır test olan veya öykünücü hello.

### <a name="test-push-notifications-in-your-android-app"></a>Android uygulamanızda test anında iletme bildirimleri
bir öykünücü üzerinde yalnızca test ettiğiniz zaman hello ilk iki adım gerekli değildir.

1. Aşağıda hello Android Sanal Aygıt Yöneticisi'nde gösterildiği gibi Google API'leri hello hedef olarak ayarlanmış olan bir sanal cihazdaki tooor hata ayıklama dağıtıyorsanız emin olun.
2. Bir Google hesabı toohello Android cihazı tıklayarak ekleyin **uygulamaları** > **ayarları** > **hesabı eklemek**. Daha sonra yeni bir hello istemleri tooadd varolan bir Google hesabı toohello aygıt ya da toocreate izleyin.
3. Visual Studio veya Xamarin Studio'da hello sağ **Droid** proje ve tıklatın **başlangıç projesi olarak ayarla**.
4. Tıklatın **çalıştırmak** toobuild hello proje ve Android cihaz veya öykünücü üzerinde hello uygulamayı başlatın.
5. Merhaba uygulamasında, bir görev yazın ve ardından hello artı (**+**) simgesi.
6. Bir öğe eklendiğinde, bir bildiriminin alındığını doğrulayın.

## <a name="configure-and-run-hello-ios-project-optional"></a>Yapılandırma ve (isteğe bağlı) hello iOS projesi çalıştırma
Bu bölüm iOS cihazları için hello Xamarin iOS projesi çalıştırmaya yöneliktir. iOS cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a>APNS için Hello bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

Ardından, Xamarin Studio veya Visual Studio'da hello iOS proje ayarı yapılandırır.

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a>Anında iletme bildirimleri tooyour iOS uygulaması ekleyin
1. Merhaba, **iOS** proje, AppDelegate.cs açın ve deyimi toohello üst hello kod dosyasının aşağıdaki hello ekleyin.

        using Newtonsoft.Json.Linq;
2. Merhaba, **AppDelegate** sınıfı, hello için bir geçersiz kılma ekleyip **RegisteredForRemoteNotifications** olay tooregister bildirimler için:

        public override void RegisteredForRemoteNotifications(UIApplication application,
            NSData deviceToken)
        {
            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
                {
                  {"body", templateBodyAPNS}
                };

            // Register for push with your mobile app
            Push push = TodoItemManager.DefaultManager.CurrentClient.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }
3. İçinde **AppDelegate**, ayrıca hello için geçersiz kılma aşağıdaki hello ekleyin **DidReceiveRemoteNotification** olay işleyicisi:

        public override void DidReceiveRemoteNotification(UIApplication application,
            NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;

            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps[new NSString("alert")] as NSString).ToString();

            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

    Merhaba uygulama çalışırken bu yöntem gelen bildirimlerini işler.
4. Merhaba, **AppDelegate** sınıfı, kod toohello aşağıdaki hello eklemek **FinishedLaunching** yöntemi:

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    Bu uzak bildirimler için destek sağlar ve kayıt istekleri gönderme.

Uygulamanızı güncelleştirilmiş toosupport anında iletme bildirimleri sunulmuştur.

#### <a name="test-push-notifications-in-your-ios-app"></a>İOS uygulamanızı test anında iletme bildirimleri
1. Merhaba iOS projesine sağ tıklayın ve **başlangıç projesi olarak ayarla**.
2. Tuşuna hello **çalıştırmak** düğmesini veya **F5** Visual Studio toobuild hello proje ve bir iOS aygıtı hello uygulamayı başlatın. Ardından **Tamam** tooaccept anında iletme bildirimleri.

   > [!NOTE]
   > Anında iletme bildirimleri, uygulamanızdan açıkça kabul etmeniz gerekir. Bu istek, yalnızca uygulama çalıştırır hello ilk kez hello oluşur.
   >
   >
3. Merhaba uygulamasında, bir görev yazın ve ardından hello artı (**+**) simgesi.
4. Bir bildirim alındı ve ardından doğrulamak **Tamam** toodismiss hello bildirim.

## <a name="configure-and-run-windows-projects-optional"></a>Yapılandırma ve çalıştırma (isteğe bağlı) Windows projeleri
Bu bölüm Windows cihazları için Xamarin.Forms WinApp ve WinPhone81 projeleri hello çalıştırmaya yöneliktir. Bu adımları, Evrensel Windows Platformu (UWP) projeleri de destekler. Windows cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a>Windows bildirim Hizmeti'ni (WNS) Windows uygulamanızı anında iletme bildirimleri için kaydetme
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a>WNS için Hello bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a>Anında iletme bildirimleri tooyour Windows uygulaması Ekle
1. Visual Studio'da açın **App.xaml.cs** Windows proje ve hello aşağıdaki deyimleri ekleyin.

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    Değiştir `<your_TodoItemManager_portable_class_namespace>` taşınabilir projenizin hello içeren hello ad alanıyla `TodoItemManager` sınıfı.
2. App.xaml.cs dosyasında hello aşağıdakileri ekleyin **Initnotificationsasync** yöntemi:

        private async Task InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            const string templateBodyWNS =
                "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";

            JObject headers = new JObject();
            headers["X-WNS-Type"] = "wns/toast";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyWNS},
                {"headers", headers} // Needed for WNS.
            };

            await TodoItemManager.DefaultManager.CurrentClient.GetPush()
                .RegisterAsync(channel.Uri, templates);
        }

    Bu yöntem hello anında bildirim kanalı alır ve bir şablon tooreceive şablon bildirim bildirim hub'ınıza kaydeder. Destekleyen bir şablon bildirim *messageParam* toothis istemci teslim edilecek.
3. App.xaml.cs dosyasında hello güncelleştirme **OnLaunched** hello ekleyerek olay işleyici yöntemi tanımının `async` değiştiricisi. Daha sonra aşağıdaki kod hello yöntemi hello sonunda hello ekleyin:

        await InitNotificationsAsync();

    Bu, hello anında iletme bildirimi kaydı oluşturulur veya hello uygulama her başlatıldığında yenilenir sağlar. Önemli toodo WNS anında iletme kanal hello bu tooguarantee her zaman etkin olduğunu.  
4. Visual Studio için Çözüm Gezgini'nde hello açın **Package.appxmanifest** dosya ve ayarlayın **bildirim özellikli** çok**Evet** altında **bildirimleri**.
5. Merhaba uygulama derleyin ve hata olmadığını doğrulayın. İstemci uygulamanızın artık Mobile Apps bitiş hello şablon bildirimleri için hello kaydetmelisiniz. Bu bölümde, çözümünüz içinde her Windows projesi için tekrarlayın.

#### <a name="test-push-notifications-in-your-windows-app"></a>Windows uygulamanızı test anında iletme bildirimleri
1. Visual Studio'da Windows projesine sağ tıklayın ve **başlangıç projesi olarak ayarla**.
2. Tuşuna hello **çalıştırmak** düğmesini toobuild hello proje ve hello uygulamayı başlatın.
3. Merhaba uygulamasında yeni bir todoıtem için bir ad yazın ve ardından hello artı (**+**) simgesi tooadd.
4. Merhaba öğesi eklendiğinde, bir bildirim alındığında doğrulayın.

## <a name="next-steps"></a>Sonraki adımlar
Anında iletme bildirimleri hakkında daha fazla bilgi edinebilirsiniz:

* [Anında iletme bildirimi sorunlarını tanılamak](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Neden bildirimleri bırakılan veya cihazlarda bitmeyen çeşitli nedenleri vardır. Bu konu nasıl anında iletme bildirimi hatalarının tooanalyze ve Şekil hello kök çıkışı neden gösterir.

Eğitim aşağıdaki hello tooone üzerinde de devam edebilirsiniz:

* [Kimlik doğrulama tooyour uygulama Ekle](app-service-mobile-xamarin-forms-get-started-users.md)  
  Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.
* [Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Bilgi nasıl tooadd çevrimdışı destek Mobile Apps kullanarak uygulamanız için yedekleme son. Çevrimdışı Eşitleme ile kullanıcılar mobil uygulama ile etkileşim kurabilen&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
