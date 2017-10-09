---
title: "aaaGet Xamarin.Android uygulamaları için Notification Hubs ile çalışmaya | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Xamarin Android uygulaması öğrenin."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: xamarin
ms.assetid: 0be600fe-d5f3-43a5-9e5e-3135c9743e54
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c5c7ead9a9381ab9fb6bbe86e930a8a9254813d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-with-xamarin-for-android"></a>Android için Xamarin ile Notification Hubs'ı kullanmaya başlama
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooa Xamarin.Android uygulaması gösterir.
Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan boş bir Xamarin.Android uygulaması oluşturacaksınız. Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin. Merhaba tamamlanmış kod hello kullanılabilir [NotificationHubs uygulaması] [ GitHub] örnek.

Bu öğretici Notification Hubs kullanımında hello basit yayın senaryosunu gösterir.

## <a name="before-you-begin"></a>Başlamadan önce
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Bu öğreticinin hello tamamlanan kodu Github'da bulunabilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/Xamarin/GetStartedXamarinAndroid).

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici hello aşağıdakileri gerektirir:

* Windows'ta Xamarin ile Visual Studio veya Mac OS X'te Xamarin Studio. Tam yükleme yönergeleri [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx) sayfasında bulunabilir.
* Etkin Google hesabı
* [Azure Mesajlaşma Bileşeni]
* [Google Cloud Messaging İstemci Bileşeni]

Bu öğreticiyi tamamlamak Xamarin.Android uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.

> [!IMPORTANT]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A9C9624B5&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-android-get-started%2F).
> 
> 

## <a name="enable-google-cloud-messaging"></a>Google Cloud Messaging'i etkinleştirme
[!INCLUDE [mobile-services-enable-Google-cloud-messaging](../../includes/mobile-services-enable-google-cloud-messaging.md)]

## <a name="configure-your-notification-hub"></a>Bildirim hub'ınızı yapılandırma
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li><p>Merhaba tıklatın <b>yapılandırma</b> sekmesinde hello üstünde, hello girin <b>API anahtarı</b> değerini hello önceki bölümde edindiğiniz ve ardından <b>kaydetmek</b>.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-android-get-started/notification-hub-configure-android.png)

Bildirim hub'ınız şimdi GCM ile yapılandırılmış toowork olduğu ve toosend anında iletme bildirimleri ve uygulama tooreceive bildirimleri kaydetmek hello bağlantı dizeleri tooboth sahip.

## <a name="connect-your-app-toohello-notification-hub"></a>Uygulama toohello bildirim hub'ınıza bağlanın
### <a name="create-a-new-project"></a>Yeni bir proje oluşturma
1. Xamarin Studio'da **New Solution**'a (Yeni Çözüm), **Android App** 'e (Android Uygulaması) ve **Next**'e (İleri) tıklayın.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project1.png)

2. **App Name**'i (Uygulama Adı) ve **Identifier**'ı (Tanımlayıcı) girin. Merhaba tıklatın **Target Plaforms** toosupport istediğiniz ve ardından **sonraki** ve **oluşturma**.
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-project2.png)

    Bu, yeni bir Android projesi oluşturur.

1. Merhaba çözüm görünümü yeni projenize sağ tıklayıp seçerek hello proje özelliklerini açın **seçenekleri**. Select hello **Android uygulaması** hello öğesinde **yapı** bölümü.
   
    Bu hello ilk harfini emin olun, **paket adı** küçük harf.
   
   > [!IMPORTANT]
   > Merhaba hello paket adının ilk harfi küçük olmalıdır. Aksi durumda, aşağıdaki anında iletme bildirimleri için **BroadcastReceiver** ve **IntentFilter** öğelerinizi kaydettiğinizde uygulama bildirim hataları alırsınız.
   > 
   > 
   
      ![](./media/partner-xamarin-notification-hubs-android-get-started/notification-hub--xamarin-android-app-options.png)
2. İsteğe bağlı olarak, kümesi hello **Minimum Android sürümü** tooanother API düzeyi.
3. İsteğe bağlı olarak, kümesi hello **hedef Android sürümü** toohello (olmalıdır API düzeyi 8 veya sonraki sürümler) tootarget istediğiniz başka bir API sürümü.

Tıklatın **Tamam** ve Kapat hello proje Seçenekleri iletişim kutusu.

### <a name="add-hello-required-components-tooyour-project"></a>Merhaba gerekli bileşenleri tooyour proje ekleyin
Hello Google Cloud Messaging istemcisi Xamarin bileşen Deposu'nda hello üzerinde kullanılabilir hello Xamarin.Android içinde anında iletme bildirimlerini destekleme işlemini basitleştirir.

1. Xamarin.Android uygulaması Hello bileşenleri klasörü sağ tıklatın ve seçin **daha almak bileşenleri**.
2. Merhaba Ara **Azure Mesajlaşma** bileşeni ve toohello proje ekleyin.
3. Merhaba Ara **Google Cloud Messaging istemcisi** bileşeni ve toohello proje ekleyin.

### <a name="set-up-notification-hubs-in-your-project"></a>Projenizdeki bildirim hub'larını ayarlama
1. Android uygulamanız ve bildirim hub'ınız için bilgisinden hello toplayın:
   
   * **GoogleProjectNumber**: hello hello Google Developer Portal'daki uygulamanıza genel bakış'nden bu proje numarası değerini alın. Merhaba portalında hello uygulama oluştururken bu değeri daha önce Not yaptığınız.
   * **Dinleme bağlantı dizesi**: hello hello Panoda [Klasik Azure portalı], tıklatın **bağlantı dizelerini görüntüle**. Kopya hello *DefaultListenSharedAccessSignature* bu değer için bağlantı dizesi.
   * **Hub adı**: Bu hello Merhaba, hub'dan adıdır [Klasik Azure portalı]. Örneğin, *mynotificationhub2*.
     
     Oluşturma bir **Constants.cs** Xamarin projeniz için sınıf ve sabit değerleri hello sınıfında aşağıdaki hello tanımlayın. Merhaba yer tutucuları değerleriniz ile değiştirin.
     
       public static class Constants   {
     
           public const string SenderID = "<GoogleProjectNumber>"; // Google API Project Number
           public const string ListenConnectionString = "<Listen connection string>";
           public const string NotificationHubName = "<hub name>";
       }
2. Merhaba aşağıdaki using deyimlerini çok**MainActivity.cs**:
   
        using Android.Util;
        using Gcm.Client;
3. Bir örnek değişkeni toohello ekleme `MainActivity` hello uygulama çalışırken, kullanılan tooshow uyarı iletişim kutusu sınıfı:
   
        public static MainActivity instance;
4. Merhaba yönteminde aşağıdaki hello oluşturma **MainActivity** sınıfı:
   
        private void RegisterWithGCM()
        {
            // Check tooensure everything's set up right
            GcmClient.CheckDevice(this);
            GcmClient.CheckManifest(this);
   
            // Register for push notifications
            Log.Info("MainActivity", "Registering...");
            GcmClient.Register(this, Constants.SenderID);
        }
5. Merhaba, `OnCreate` yöntemi **MainActivity.cs**, hello başlatma `instance` değişkeni ve çok bir çağrı ekleyin`RegisterWithGCM`:
   
        protected override void OnCreate (Bundle bundle)
        {
            instance = this;
   
            base.OnCreate (bundle);
   
            // Set your view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);
   
            // Get your button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);
   
            RegisterWithGCM();
        }
6. **MyBroadcastReceiver** adlı yeni bir sınıf oluşturun.
   
   > [!NOTE]
   > Aşağıda, sıfırdan bir **BroadcastReceiver** sınıfı oluşturma konusunda size yol göstereceğiz. Ancak, hızlı alternatif toomanually oluşturma **MyBroadcastReceiver.cs** toorefer toohello olan **GcmService.cs** helloiledahilhelloörnekXamarin.Androidprojesindebulunandosya[NotificationHubs örnekleri][GitHub]. Çoğaltma **GcmService.cs** ve sınıf adlarını değiştirmek de harika yer toostart olabilir.
   > 
   > 
7. Merhaba aşağıdaki using deyimlerini çok**MyBroadcastReceiver.cs** (toohello bileşeni ve daha önce eklediğimiz derleme başvuran):
   
        using System.Collections.Generic;
        using System.Text;
        using Android.App;
        using Android.Content;
        using Android.Util;
        using Gcm.Client;
        using WindowsAzure.Messaging;
8. İçinde **MyBroadcastReceiver.cs**, izin istekleri arasında hello aşağıdaki hello eklemek **kullanarak** deyimleri ve hello **ad alanı** bildirimi:
   
        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
   
        //GET_ACCOUNTS is needed only for Android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
9. İçinde **MyBroadcastReceiver.cs**, hello değiştirme **MyBroadcastReceiver** sınıf toomatch hello aşağıdaki:
   
        [BroadcastReceiver(Permission=Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY },
            Categories = new string[] { "@PACKAGE_NAME@" })]
        public class MyBroadcastReceiver : GcmBroadcastReceiverBase<PushHandlerService>
        {
            public static string[] SENDER_IDS = new string[] { Constants.SenderID };
   
            public const string TAG = "MyBroadcastReceiver-GCM";
        }
10. **MyBroadcastReceiver.cs**'ye **GcmServiceBase**'den türetilen **PushHandlerService** adlı başka bir sınıf ekleyin. Tooapply hello emin olun **hizmet** özniteliği toohello sınıfı:
    
         [Service] // Must use hello service tag
         public class PushHandlerService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }
             private NotificationHub Hub { get; set; }
    
             public PushHandlerService() : base(Constants.SenderID)
                {
                 Log.Info(MyBroadcastReceiver.TAG, "PushHandlerService() constructor");
             }
         }
11. **GcmServiceBase**; **OnRegistered()**, **OnUnRegistered()**, **OnMessage()**, **OnRecoverableError()** ve **OnError()** yöntemlerini uygular. Bizim **PushHandlerService** uygulama sınıfımızın bu yöntemleri geçersiz kılması gerekir ve bu yöntemleri hello bildirim hub'ı ile yanıt toointeracting ateşlenir.
12. Merhaba geçersiz kılma **OnRegistered()** yönteminde **PushHandlerService** koddan hello kullanarak:
    
         protected override void OnRegistered(Context context, string registrationId)
         {
             Log.Verbose(MyBroadcastReceiver.TAG, "GCM Registered: " + registrationId);
             RegistrationID = registrationId;
    
             createNotification("PushHandlerService-GCM Registered...",
                                 "hello device has been Registered!");
    
             Hub = new NotificationHub(Constants.NotificationHubName, Constants.ListenConnectionString,
                                         context);
             try
             {
                 Hub.UnregisterAll(registrationId);
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
    
             //var tags = new List<string>() { "falcons" }; // create tags if you want
             var tags = new List<string>() {};
    
             try
             {
                 var hubRegistration = Hub.Register(registrationId, tags.ToArray());
             }
             catch (Exception ex)
             {
                 Log.Error(MyBroadcastReceiver.TAG, ex.Message);
             }
         }
    
    > [!NOTE]
    > Merhaba, **OnRegistered()** Yukarıdaki kod, belirli Mesajlaşma kanallarına için hello özelliği toospecify etiketleri tooregister unutmamalısınız.
    > 
    > 
13. Merhaba geçersiz kılma **Onmessageoptions** yönteminde **PushHandlerService** koddan hello kullanarak:
    
        protected override void OnMessage(Context context, Intent intent)
        {
            Log.Info(MyBroadcastReceiver.TAG, "GCM Message Received!");
    
            var msg = new StringBuilder();
    
            if (intent != null && intent.Extras != null)
            {
                foreach (var key in intent.Extras.KeySet())
                    msg.AppendLine(key + "=" + intent.Extras.Get(key).ToString());
            }
    
            string messageText = intent.Extras.GetString("message");
            if (!string.IsNullOrEmpty (messageText))
            {
                createNotification ("New hub message!", messageText);
            }
            else
            {
                createNotification ("Unknown message details", msg.ToString ());
            }
        }
14. Merhaba aşağıdakileri ekleyin **Pushhandlerservice** ve **Createnotification** yöntemleri çok**PushHandlerService** bir bildirim alındığında kullanıcıları bilgilendirmek için.
    
    > [!NOTE]
    > Android sürüm 5.0 ve sonrasındaki bildirim tasarımı önceki sürümlerden önemli ölçüde farklıdır. Bunu Android 5.0 veya sonraki sürümlerinde test ederseniz hello uygulama tooreceive hello bildirim çalıştıran toobe gerekir. Daha fazla bilgi için bkz. [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Android Bildirimleri).
    > 
    > 
    
        void createNotification(string title, string desc)
        {
            //Create notification
            var notificationManager = GetSystemService(Context.NotificationService) as NotificationManager;
    
            //Create an intent tooshow UI
            var uiIntent = new Intent(this, typeof(MainActivity));
    
            //Create hello notification
            var notification = new Notification(Android.Resource.Drawable.SymActionEmail, title);
    
            //Auto-cancel will remove hello notification once hello user touches it
            notification.Flags = NotificationFlags.AutoCancel;
    
            //Set hello notification info
            //we use hello pending intent, passing our ui intent over, which will get called
            //when hello notification is tapped.
            notification.SetLatestEventInfo(this, title, desc, PendingIntent.GetActivity(this, 0, uiIntent, 0));
    
            //Show hello notification
            notificationManager.Notify(1, notification);
            dialogNotify (title, desc);
        }
    
        protected void dialogNotify(String title, String message)
        {
    
            MainActivity.instance.RunOnUiThread(() => {
                AlertDialog.Builder dlg = new AlertDialog.Builder(MainActivity.instance);
                AlertDialog alert = dlg.Create();
                alert.SetTitle(title);
                alert.SetButton("Ok", delegate {
                    alert.Dismiss();
                });
                alert.SetMessage(message);
                alert.Show();
            });
        }
15. **OnUnRegistered()**, **OnRecoverableError()** ve **OnError()** soyut üyelerini geçersiz kılarak kodunuzu derleyin:
    
        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Verbose(MyBroadcastReceiver.TAG, "GCM Unregistered: " + registrationId);
    
            createNotification("GCM Unregistered...", "hello device has been unregistered!");
        }
    
        protected override bool OnRecoverableError(Context context, string errorId)
        {
            Log.Warn(MyBroadcastReceiver.TAG, "Recoverable Error: " + errorId);
    
            return base.OnRecoverableError (context, errorId);
        }
    
        protected override void OnError(Context context, string errorId)
        {
            Log.Error(MyBroadcastReceiver.TAG, "GCM Error: " + errorId);
        }

## <a name="run-your-app-in-hello-emulator"></a>Merhaba öykünücüsünde uygulamanızı çalıştırma
Bu uygulamayı hello öykünücüde çalıştırırsanız, bir Android sanal cihazı (Google API'lerini destekleyen AVD) kullandığınızdan emin olun.

> [!IMPORTANT]
> Sipariş tooreceive anında iletme bildirimlerini Android sanal Cihazınızda bir Google hesabı ayarlamanız gerekir. (Merhaba öykünücüsünde çok gidin**ayarları** tıklatıp **hesabı Ekle**.) Ayrıca, bu hello öykünücüsü bağlı toohello Internet olduğundan emin olun.
> 
> [!NOTE]
> Android sürüm 5.0 ve sonrasındaki bildirim tasarımı önceki sürümlerden önemli ölçüde farklıdır. Daha fazla bilgi için bkz. [Android Notifications](http://go.microsoft.com/fwlink/?LinkId=615880) (Android Bildirimleri).
> 
> 

1. **Tools**'da (Araçlar), **Open Android Emulator Manager** (Android Öykünücüsü Yöneticisini Aç) seçeneğine tıklayın, cihazınızı açın ve ardından **Edit** (Düzenle) seçeneğine tıklayın.
   
      ![][18]
2. **Target** (Hedef) içinde **Google APIs** (Google API'leri) seçeneğini belirleyin ve ardından **Tamam**'a tıklayın.
   
      ![][19]
3. Merhaba üst araç çubuğunda tıklatın **çalıştırmak**ve ardından uygulamanızı seçin. Bu hello öykünücüyü başlatır ve hello uygulama çalıştırır.
   
   Merhaba uygulama alır hello *RegistrationId* GCM ve hello bildirim hub'ına kaydeder.

## <a name="send-notifications-from-your-backend"></a>Arka ucunuzdan bildirim gönderme
Hello bildirimleri göndererek uygulamanızda bildirim almayı test edebilirsiniz [Klasik Azure portalı] ekranda hello aşağıda gösterildiği gibi hello bildirim hub'ındaki sekmesi hello hata ayıklama.

![][30]

Anında iletme bildirimleri normalde, uyumlu bir kitaplık aracılığıyla Mobile Services veya ASP.NET gibi bir arka uç hizmetinde gönderilir. Bir kitaplık arka ucunuz için kullanılabilir değilse, toosend bildirim iletilerini doğrudan hello REST API de kullanabilirsiniz.

Bildirimleri göndermek için tooreview isteyebileceğiniz diğer bazı öğreticilerin bir listesi aşağıda verilmiştir:

* ASP.NET: Bkz [Notification Hubs kullanma toopush bildirimleri toousers].
* Azure Notification Hubs Java SDK: bkz [nasıl toouse Java'dan Notification Hubs](notification-hubs-java-push-notification-tutorial.md) Java'dan bildirim göndermek için. Android geliştirmesi için Eclipse'te sınanmıştır.
* PHP: Bkz [nasıl toouse php'den Notification Hubs](notification-hubs-php-push-notification-tutorial.md).

Merhaba sonraki alt hello öğreticinin içinde bir .NET konsol uygulaması kullanarak ve bir node betiği aracılığıyla mobil hizmet kullanarak bildirim gönderin.

#### <a name="optional-send-notifications-by-using-a-net-app"></a>(İsteğe bağlı) .NET uygulaması kullanarak bildirim gönderme
Bu bölümde, .NET konsol uygulaması kullanarak bildirim göndereceğiz

1. Yeni bir Visual C# konsol uygulaması oluşturun:
   
      ![][20]
2. Visual Studio'da **Araçlar**'a, **NuGet Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.
   
    Bu, Visual Studio'da Paket Yöneticisi konsolu hello görüntüler.
3. Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Merhaba Program.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimi:
   
        using Microsoft.Azure.NotificationHubs;
5. İçinde `Program` sınıfı, yöntem aşağıdaki hello ekleyin. Merhaba yer tutucu metnini güncelleştirin, *DefaultFullSharedAccessSignature* hello bağlantı dizenizi ve hub adı [Klasik Azure portalı].
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            await hub.SendGcmNativeNotificationAsync("{ \"data\" : {\"message\":\"Hello from Azure!\"}}");
        }
6. Hello aşağıdaki satırları ekleyin, **ana** yöntemi:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Merhaba F5 anahtar toorun hello uygulama tuşuna basın. Merhaba uygulamada bir bildirim almanız gerekir.
   
      ![][21]

#### <a name="optional-send-notifications-by-using-a-mobile-service"></a>(İsteğe bağlı) Mobil hizmet kullanarak bildirim gönderme
1. [Mobile Services'i kullanmaya başlama]'yı izleyin.
2. İçinde toohello oturum [Klasik Azure portalı]ve mobil hizmetinizi seçin.
3. Select hello **Zamanlayıcı** hello üst sekmesinde.
   
      ![][22]
4. Yeni bir zamanlanan iş oluşturun, ad ekleyin ve **İsteğe bağlı**'yı seçin.
   
      ![][23]
5. Merhaba iş oluşturulduğunda hello iş adına tıklayın. Merhaba ardından **betik** hello üst çubuğu sekmesinde.
6. Komut dosyası Zamanlayıcı işlevinizin içine aşağıdaki hello ekleyin. Bildirim hub'ı adı ve hello için bağlantı dizenizi emin tooreplace hello yer tutucularını olun *DefaultFullSharedAccessSignature* daha önce edindiğiniz. **Kaydet** düğmesine tıklayın.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<hub name>', '<connection string>');
        notificationHubService.gcm.send(null,'{"data":{"message" : "Hello from Mobile Services!"}}',
          function (error)
          {
            if (!error) {
               console.warn("Notification successful");
            }
            else
            {
              console.warn("Notification failed" + error);
            }
          }
        );
7. Tıklatın **bir kez çalıştır** hello alt çubuğunda. Bir bildirim almanız gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Bu basit örnekte, Android cihazları bildirimleri tooall yayımladınız. Buna belirli kullanıcılara tootarget sipariş, toohello öğretici başvurun [Notification Hubs kullanma toopush bildirimleri toousers]. Toosegment kullanıcılarınızı ilgi alanı gruplarına göre isterseniz, okuyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend]. Hakkında daha fazla bilgi toouse bildirim hub'ları [Notification Hubs Kılavuzu] ve hello [bildirim hub'ları nasıl toofor Android].

<!-- Anchors. -->
[Enable Google Cloud Messaging]: #register
[Configure your Notification Hub]: #configure-hub
[Connecting your app toohello Notification Hub]: #connecting-app
[Run your app with hello emulator]: #run-app
[Send notifications from your back-end]: #send
[Next steps]:#next-steps

<!-- Images. -->

[11]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-configure-android.png

[13]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app1.png
[15]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-xamarin-android-app3.png

[18]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app7.png
[19]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-android-app8.png

[20]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-create-console-app.png
[21]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-android-toast.png
[22]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler1.png
[23]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hub-scheduler2.png

[30]: ./media/partner-xamarin-notification-hubs-android-get-started/notification-hubs-debug-hub-gcm.png


<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Mobile Services'i kullanmaya başlama]: /develop/mobile/tutorials/get-started-xamarin-android/#create-new-service
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[Klasik Azure portalı]: https://manage.windowsazure.com/
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[bildirim hub'ları nasıl toofor Android]: http://msdn.microsoft.com/library/dn282661.aspx

[Notification Hubs kullanma toopush bildirimleri toousers]: /manage/services/notification-hubs/notify-users-aspnet
[son dakika haberleri Notification Hubs kullanma toosend]: /manage/services/notification-hubs/breaking-news-dotnet
[GCMClient Component page]: http://components.xamarin.com/view/GCMClient
[Xamarin.NotificationHub GitHub page]: https://github.com/SaschaDittmann/Xamarin.NotificationHub
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Google Cloud Messaging İstemci Bileşeni]: http://components.xamarin.com/view/GCMClient/
[Azure Mesajlaşma Bileşeni]: http://components.xamarin.com/view/azure-messaging
