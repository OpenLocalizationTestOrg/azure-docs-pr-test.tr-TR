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
# <a name="add-push-notifications-tooyour-xamarinforms-app"></a><span data-ttu-id="9750f-103">Anında iletme bildirimleri tooyour Xamarin.Forms uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="9750f-103">Add push notifications tooyour Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="9750f-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9750f-104">Overview</span></span>
<span data-ttu-id="9750f-105">Bu öğreticide, hello sonuçlandı anında iletme bildirimleri tooall hello projelerine ekleme [Xamarin.Forms Hızlı Başlangıç](app-service-mobile-xamarin-forms-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9750f-105">In this tutorial, you add push notifications tooall hello projects that resulted from hello [Xamarin.Forms quick start](app-service-mobile-xamarin-forms-get-started.md).</span></span> <span data-ttu-id="9750f-106">Bu, bir kayda eklenen her zaman bir anında iletme bildirimi tooall platformlar arası istemcileri gönderilen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9750f-106">This means that a push notification is sent tooall cross-platform clients every time a record is inserted.</span></span>

<span data-ttu-id="9750f-107">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello.</span><span class="sxs-lookup"><span data-stu-id="9750f-107">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="9750f-108">Daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9750f-108">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9750f-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9750f-109">Prerequisites</span></span>
<span data-ttu-id="9750f-110">İOS için size gereken bir [Apple Developer Program üyeliği](https://developer.apple.com/programs/ios/) ve fiziksel bir iOS cihazına.</span><span class="sxs-lookup"><span data-stu-id="9750f-110">For iOS, you will need an [Apple Developer Program membership](https://developer.apple.com/programs/ios/) and a physical iOS device.</span></span> <span data-ttu-id="9750f-111">Merhaba [iOS simülatörü anında iletme bildirimlerini desteklemiyor](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="9750f-111">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span>

## <span data-ttu-id="9750f-112"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9750f-112"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="9750f-113">Güncelleştirme Hello sunucu projesi toosend anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="9750f-113">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-and-run-hello-android-project-optional"></a><span data-ttu-id="9750f-114">Yapılandırma ve hello (isteğe bağlı) Android projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9750f-114">Configure and run hello Android project (optional)</span></span>
<span data-ttu-id="9750f-115">Bu bölümde tooenable anında iletme bildirimlerinin hello Xamarin.Forms Android projesi Android için tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="9750f-115">Complete this section tooenable push notifications for hello Xamarin.Forms Droid project for Android.</span></span>

### <a name="enable-firebase-cloud-messaging-fcm"></a><span data-ttu-id="9750f-116">Firebase Cloud Messaging'i (FCM) etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9750f-116">Enable Firebase Cloud Messaging (FCM)</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

### <a name="configure-hello-mobile-apps-back-end-toosend-push-requests-by-using-fcm"></a><span data-ttu-id="9750f-117">Merhaba Mobile Apps arka uç toosend gönderme istekleri FCM kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9750f-117">Configure hello Mobile Apps back end toosend push requests by using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

### <a name="add-push-notifications-toohello-android-project"></a><span data-ttu-id="9750f-118">Anında iletme bildirimleri toohello Android projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="9750f-118">Add push notifications toohello Android project</span></span>
<span data-ttu-id="9750f-119">FCM ile yapılandırılmış hello arka ucu ile bileşenleri ve kodları toohello istemci tooregister FCM ile ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9750f-119">With hello back end configured with FCM, you can add components and codes toohello client tooregister with FCM.</span></span> <span data-ttu-id="9750f-120">Mobile Apps sonlandırmak ve bildirimlerin hello aracılığıyla Azure Notification Hubs ile anında iletme bildirimleri için kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9750f-120">You can also register for push notifications with Azure Notification Hubs through hello Mobile Apps back end, and receive notifications.</span></span>

1. <span data-ttu-id="9750f-121">Merhaba, **Droid** proje, hello sağ tıklatın **bileşenleri** klasörü ve tıklatın **daha almak bileşenleri...** . Merhaba arama **Google Cloud Messaging istemcisi** bileşeni ve toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9750f-121">In hello **Droid** project, right-click hello **Components** folder, and click **Get More Components...**. Then search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span> <span data-ttu-id="9750f-122">Bu bileşen, bir Xamarin Android projesi için anında iletme bildirimleri destekler.</span><span class="sxs-lookup"><span data-stu-id="9750f-122">This component supports push notifications for a Xamarin Android project.</span></span>
2. <span data-ttu-id="9750f-123">Merhaba MainActivity.cs proje dosyasını açın ve aşağıdaki ifadeyi hello dosyanın üst kısmındaki hello hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9750f-123">Open hello MainActivity.cs project file, and add hello following statement at hello top of hello file:</span></span>

        using Gcm.Client;
3. <span data-ttu-id="9750f-124">Aşağıdaki kodu toohello hello eklemek **OnCreate** hello sonra yöntemini çağırın çok**LoadApplication**:</span><span class="sxs-lookup"><span data-stu-id="9750f-124">Add hello following code toohello **OnCreate** method after hello call too**LoadApplication**:</span></span>

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
4. <span data-ttu-id="9750f-125">Yeni bir ekleme **CreateAndShowDialog** yardımcı yöntemi, aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="9750f-125">Add a new **CreateAndShowDialog** helper method, as follows:</span></span>

        private void CreateAndShowDialog(String message, String title)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);

            builder.SetMessage (message);
            builder.SetTitle (title);
            builder.Create().Show ();
        }
5. <span data-ttu-id="9750f-126">Aşağıdaki kodu toohello hello eklemek **MainActivity** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="9750f-126">Add hello following code toohello **MainActivity** class:</span></span>

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

    <span data-ttu-id="9750f-127">Bu hello geçerli sunan **MainActivity** örnek biz hello ana kullanıcı Arabirimi iş parçacığı üzerinde çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9750f-127">This exposes hello current **MainActivity** instance, so we can execute on hello main UI thread.</span></span>
6. <span data-ttu-id="9750f-128">Merhaba başlatma `instance` hello hello başında değişken **OnCreate** şekilde yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9750f-128">Initialize hello `instance` variable at hello beginning of hello **OnCreate** method, as follows.</span></span>

        // Set hello current instance of MainActivity.
        instance = this;
7. <span data-ttu-id="9750f-129">Yeni bir sınıf dosya toohello ekleme **Droid** adlı projesi `GcmService.cs`ve hello aşağıdakilerden emin olun **kullanarak** deyimleri mevcut hello dosya hello üstünde:</span><span class="sxs-lookup"><span data-stu-id="9750f-129">Add a new class file toohello **Droid** project named `GcmService.cs`, and make sure hello following **using** statements are present at hello top of hello file:</span></span>

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
8. <span data-ttu-id="9750f-130">Merhaba dosyasının hello üstünde izin istekleri hello sonra aşağıdaki hello eklemek **kullanarak** deyimleri ve hello önce **ad alanı** bildirimi.</span><span class="sxs-lookup"><span data-stu-id="9750f-130">Add hello following permission requests at hello top of hello file, after hello **using** statements and before hello **namespace** declaration.</span></span>

        [assembly: Permission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "@PACKAGE_NAME@.permission.C2D_MESSAGE")]
        [assembly: UsesPermission(Name = "com.google.android.c2dm.permission.RECEIVE")]
        [assembly: UsesPermission(Name = "android.permission.INTERNET")]
        [assembly: UsesPermission(Name = "android.permission.WAKE_LOCK")]
        //GET_ACCOUNTS is only needed for android versions 4.0.3 and below
        [assembly: UsesPermission(Name = "android.permission.GET_ACCOUNTS")]
9. <span data-ttu-id="9750f-131">Sınıf tanımı toohello namespace aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9750f-131">Add hello following class definition toohello namespace.</span></span>

       [BroadcastReceiver(Permission = Gcm.Client.Constants.PERMISSION_GCM_INTENTS)]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_MESSAGE }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_REGISTRATION_CALLBACK }, Categories = new string[] { "@PACKAGE_NAME@" })]
       [IntentFilter(new string[] { Gcm.Client.Constants.INTENT_FROM_GCM_LIBRARY_RETRY }, Categories = new string[] { "@PACKAGE_NAME@" })]
       public class PushHandlerBroadcastReceiver : GcmBroadcastReceiverBase<GcmService>
       {
           public static string[] SENDER_IDS = new string[] { "<PROJECT_NUMBER>" };
       }

   > [!NOTE]
   > <span data-ttu-id="9750f-132">Değiştir **< PROJECT_NUMBER >** not ettiğiniz daha önce proje numarası ile.</span><span class="sxs-lookup"><span data-stu-id="9750f-132">Replace **<PROJECT_NUMBER>** with your project number you noted earlier.</span></span>    
   >
   >
10. <span data-ttu-id="9750f-133">Merhaba boş Değiştir **GcmService** hello yeni yayın alıcı kullanan kodu aşağıdaki hello sınıfıyla:</span><span class="sxs-lookup"><span data-stu-id="9750f-133">Replace hello empty **GcmService** class with hello following code, which uses hello new broadcast receiver:</span></span>

         [Service]
         public class GcmService : GcmServiceBase
         {
             public static string RegistrationID { get; private set; }

             public GcmService()
                 : base(PushHandlerBroadcastReceiver.SENDER_IDS){}
         }
11. <span data-ttu-id="9750f-134">Aşağıdaki kodu toohello hello eklemek **GcmService** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9750f-134">Add hello following code toohello **GcmService** class.</span></span> <span data-ttu-id="9750f-135">Bu hello geçersiz kılar **OnRegistered** olay işleyicisi ve uygulayan bir **kaydetmek** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9750f-135">This overrides hello **OnRegistered** event handler and implements a **Register** method.</span></span>

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

    <span data-ttu-id="9750f-136">Bu kod hello kullandığına dikkat edin `messageParam` hello şablonu kayıt parametresi.</span><span class="sxs-lookup"><span data-stu-id="9750f-136">Note that this code uses hello `messageParam` parameter in hello template registration.</span></span>
12. <span data-ttu-id="9750f-137">Uygulayan kod aşağıdaki hello eklemek **Onmessageoptions**:</span><span class="sxs-lookup"><span data-stu-id="9750f-137">Add hello following code that implements **OnMessage**:</span></span>

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

    <span data-ttu-id="9750f-138">Bu gelen bildirimlerini işleme ve görüntülenen toohello bildirim Yöneticisi toobe gönderir.</span><span class="sxs-lookup"><span data-stu-id="9750f-138">This handles incoming notifications and sends them toohello notification manager toobe displayed.</span></span>
13. <span data-ttu-id="9750f-139">**GcmServiceBase** de tooimplement hello gerektirir **OnUnRegistered** ve **OnError** şu şekilde yapabilirsiniz işleyici yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="9750f-139">**GcmServiceBase** also requires you tooimplement hello **OnUnRegistered** and **OnError** handler methods, which you can do as follows:</span></span>

        protected override void OnUnRegistered(Context context, string registrationId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "Unregistered RegisterationId : " + registrationId);
        }

        protected override void OnError(Context context, string errorId)
        {
            Log.Error("PushHandlerBroadcastReceiver", "GCM Error: " + errorId);
        }

<span data-ttu-id="9750f-140">Şimdi, bir Android cihazında çalıştırılan hello uygulamasında anında iletme bildirimleri hazır test olan veya öykünücü hello.</span><span class="sxs-lookup"><span data-stu-id="9750f-140">Now, you are ready test push notifications in hello app running on an Android device or hello emulator.</span></span>

### <a name="test-push-notifications-in-your-android-app"></a><span data-ttu-id="9750f-141">Android uygulamanızda test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="9750f-141">Test push notifications in your Android app</span></span>
<span data-ttu-id="9750f-142">bir öykünücü üzerinde yalnızca test ettiğiniz zaman hello ilk iki adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9750f-142">hello first two steps are required only when you're testing on an emulator.</span></span>

1. <span data-ttu-id="9750f-143">Aşağıda hello Android Sanal Aygıt Yöneticisi'nde gösterildiği gibi Google API'leri hello hedef olarak ayarlanmış olan bir sanal cihazdaki tooor hata ayıklama dağıtıyorsanız emin olun.</span><span class="sxs-lookup"><span data-stu-id="9750f-143">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device manager.</span></span>
2. <span data-ttu-id="9750f-144">Bir Google hesabı toohello Android cihazı tıklayarak ekleyin **uygulamaları** > **ayarları** > **hesabı eklemek**.</span><span class="sxs-lookup"><span data-stu-id="9750f-144">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**.</span></span> <span data-ttu-id="9750f-145">Daha sonra yeni bir hello istemleri tooadd varolan bir Google hesabı toohello aygıt ya da toocreate izleyin.</span><span class="sxs-lookup"><span data-stu-id="9750f-145">Then follow hello prompts tooadd an existing Google account toohello device, or toocreate a new one.</span></span>
3. <span data-ttu-id="9750f-146">Visual Studio veya Xamarin Studio'da hello sağ **Droid** proje ve tıklatın **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="9750f-146">In Visual Studio or Xamarin Studio, right-click hello **Droid** project and click **Set as startup project**.</span></span>
4. <span data-ttu-id="9750f-147">Tıklatın **çalıştırmak** toobuild hello proje ve Android cihaz veya öykünücü üzerinde hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="9750f-147">Click **Run** toobuild hello project and start hello app on your Android device or emulator.</span></span>
5. <span data-ttu-id="9750f-148">Merhaba uygulamasında, bir görev yazın ve ardından hello artı (**+**) simgesi.</span><span class="sxs-lookup"><span data-stu-id="9750f-148">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
6. <span data-ttu-id="9750f-149">Bir öğe eklendiğinde, bir bildiriminin alındığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9750f-149">Verify that a notification is received when an item is added.</span></span>

## <a name="configure-and-run-hello-ios-project-optional"></a><span data-ttu-id="9750f-150">Yapılandırma ve (isteğe bağlı) hello iOS projesi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9750f-150">Configure and run hello iOS project (optional)</span></span>
<span data-ttu-id="9750f-151">Bu bölüm iOS cihazları için hello Xamarin iOS projesi çalıştırmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="9750f-151">This section is for running hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="9750f-152">iOS cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9750f-152">You can skip this section if you are not working with iOS devices.</span></span>

[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

#### <a name="configure-hello-notification-hub-for-apns"></a><span data-ttu-id="9750f-153">APNS için Hello bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9750f-153">Configure hello notification hub for APNS</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

<span data-ttu-id="9750f-154">Ardından, Xamarin Studio veya Visual Studio'da hello iOS proje ayarı yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9750f-154">Next, you will configure hello iOS project setting in Xamarin Studio or Visual Studio.</span></span>

[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

#### <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="9750f-155">Anında iletme bildirimleri tooyour iOS uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="9750f-155">Add push notifications tooyour iOS app</span></span>
1. <span data-ttu-id="9750f-156">Merhaba, **iOS** proje, AppDelegate.cs açın ve deyimi toohello üst hello kod dosyasının aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9750f-156">In hello **iOS** project, open AppDelegate.cs and add hello following statement toohello top of hello code file.</span></span>

        using Newtonsoft.Json.Linq;
2. <span data-ttu-id="9750f-157">Merhaba, **AppDelegate** sınıfı, hello için bir geçersiz kılma ekleyip **RegisteredForRemoteNotifications** olay tooregister bildirimler için:</span><span class="sxs-lookup"><span data-stu-id="9750f-157">In hello **AppDelegate** class, add an override for hello **RegisteredForRemoteNotifications** event tooregister for notifications:</span></span>

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
3. <span data-ttu-id="9750f-158">İçinde **AppDelegate**, ayrıca hello için geçersiz kılma aşağıdaki hello ekleyin **DidReceiveRemoteNotification** olay işleyicisi:</span><span class="sxs-lookup"><span data-stu-id="9750f-158">In **AppDelegate**, also add hello following override for hello **DidReceiveRemoteNotification** event handler:</span></span>

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

    <span data-ttu-id="9750f-159">Merhaba uygulama çalışırken bu yöntem gelen bildirimlerini işler.</span><span class="sxs-lookup"><span data-stu-id="9750f-159">This method handles incoming notifications while hello app is running.</span></span>
4. <span data-ttu-id="9750f-160">Merhaba, **AppDelegate** sınıfı, kod toohello aşağıdaki hello eklemek **FinishedLaunching** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="9750f-160">In hello **AppDelegate** class, add hello following code toohello **FinishedLaunching** method:</span></span>

        // Register for push notifications.
        var settings = UIUserNotificationSettings.GetSettingsForTypes(
            UIUserNotificationType.Alert
            | UIUserNotificationType.Badge
            | UIUserNotificationType.Sound,
            new NSSet());

        UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
        UIApplication.SharedApplication.RegisterForRemoteNotifications();

    <span data-ttu-id="9750f-161">Bu uzak bildirimler için destek sağlar ve kayıt istekleri gönderme.</span><span class="sxs-lookup"><span data-stu-id="9750f-161">This enables support for remote notifications and requests push registration.</span></span>

<span data-ttu-id="9750f-162">Uygulamanızı güncelleştirilmiş toosupport anında iletme bildirimleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="9750f-162">Your app is now updated toosupport push notifications.</span></span>

#### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="9750f-163">İOS uygulamanızı test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="9750f-163">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="9750f-164">Merhaba iOS projesine sağ tıklayın ve **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="9750f-164">Right-click hello iOS project, and click **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="9750f-165">Tuşuna hello **çalıştırmak** düğmesini veya **F5** Visual Studio toobuild hello proje ve bir iOS aygıtı hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="9750f-165">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS device.</span></span> <span data-ttu-id="9750f-166">Ardından **Tamam** tooaccept anında iletme bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="9750f-166">Then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9750f-167">Anında iletme bildirimleri, uygulamanızdan açıkça kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9750f-167">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="9750f-168">Bu istek, yalnızca uygulama çalıştırır hello ilk kez hello oluşur.</span><span class="sxs-lookup"><span data-stu-id="9750f-168">This request only occurs hello first time that hello app runs.</span></span>
   >
   >
3. <span data-ttu-id="9750f-169">Merhaba uygulamasında, bir görev yazın ve ardından hello artı (**+**) simgesi.</span><span class="sxs-lookup"><span data-stu-id="9750f-169">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
4. <span data-ttu-id="9750f-170">Bir bildirim alındı ve ardından doğrulamak **Tamam** toodismiss hello bildirim.</span><span class="sxs-lookup"><span data-stu-id="9750f-170">Verify that a notification is received, and then click **OK** toodismiss hello notification.</span></span>

## <a name="configure-and-run-windows-projects-optional"></a><span data-ttu-id="9750f-171">Yapılandırma ve çalıştırma (isteğe bağlı) Windows projeleri</span><span class="sxs-lookup"><span data-stu-id="9750f-171">Configure and run Windows projects (optional)</span></span>
<span data-ttu-id="9750f-172">Bu bölüm Windows cihazları için Xamarin.Forms WinApp ve WinPhone81 projeleri hello çalıştırmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="9750f-172">This section is for running hello Xamarin.Forms WinApp and WinPhone81 projects for Windows devices.</span></span> <span data-ttu-id="9750f-173">Bu adımları, Evrensel Windows Platformu (UWP) projeleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="9750f-173">These steps also support Universal Windows Platform (UWP) projects.</span></span> <span data-ttu-id="9750f-174">Windows cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9750f-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-windows-notification-service-wns"></a><span data-ttu-id="9750f-175">Windows bildirim Hizmeti'ni (WNS) Windows uygulamanızı anında iletme bildirimleri için kaydetme</span><span class="sxs-lookup"><span data-stu-id="9750f-175">Register your Windows app for push notifications with Windows Notification Service (WNS)</span></span>
[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="9750f-176">WNS için Hello bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9750f-176">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="9750f-177">Anında iletme bildirimleri tooyour Windows uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="9750f-177">Add push notifications tooyour Windows app</span></span>
1. <span data-ttu-id="9750f-178">Visual Studio'da açın **App.xaml.cs** Windows proje ve hello aşağıdaki deyimleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9750f-178">In Visual Studio, open **App.xaml.cs** in a Windows project, and add hello following statements.</span></span>

        using Newtonsoft.Json.Linq;
        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
        using <your_TodoItemManager_portable_class_namespace>;

    <span data-ttu-id="9750f-179">Değiştir `<your_TodoItemManager_portable_class_namespace>` taşınabilir projenizin hello içeren hello ad alanıyla `TodoItemManager` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9750f-179">Replace `<your_TodoItemManager_portable_class_namespace>` with hello namespace of your portable project that contains hello `TodoItemManager` class.</span></span>
2. <span data-ttu-id="9750f-180">App.xaml.cs dosyasında hello aşağıdakileri ekleyin **Initnotificationsasync** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="9750f-180">In App.xaml.cs, add hello following **InitNotificationsAsync** method:</span></span>

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

    <span data-ttu-id="9750f-181">Bu yöntem hello anında bildirim kanalı alır ve bir şablon tooreceive şablon bildirim bildirim hub'ınıza kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9750f-181">This method gets hello push notification channel, and registers a template tooreceive template notifications from your notification hub.</span></span> <span data-ttu-id="9750f-182">Destekleyen bir şablon bildirim *messageParam* toothis istemci teslim edilecek.</span><span class="sxs-lookup"><span data-stu-id="9750f-182">A template notification that supports *messageParam* will be delivered toothis client.</span></span>
3. <span data-ttu-id="9750f-183">App.xaml.cs dosyasında hello güncelleştirme **OnLaunched** hello ekleyerek olay işleyici yöntemi tanımının `async` değiştiricisi.</span><span class="sxs-lookup"><span data-stu-id="9750f-183">In App.xaml.cs, update hello **OnLaunched** event handler method definition by adding hello `async` modifier.</span></span> <span data-ttu-id="9750f-184">Daha sonra aşağıdaki kod hello yöntemi hello sonunda hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9750f-184">Then add hello following line of code at hello end of hello method:</span></span>

        await InitNotificationsAsync();

    <span data-ttu-id="9750f-185">Bu, hello anında iletme bildirimi kaydı oluşturulur veya hello uygulama her başlatıldığında yenilenir sağlar.</span><span class="sxs-lookup"><span data-stu-id="9750f-185">This ensures that hello push notification registration is created or refreshed every time hello app is launched.</span></span> <span data-ttu-id="9750f-186">Önemli toodo WNS anında iletme kanal hello bu tooguarantee her zaman etkin olduğunu.</span><span class="sxs-lookup"><span data-stu-id="9750f-186">It's important toodo this tooguarantee that hello WNS push channel is always active.</span></span>  
4. <span data-ttu-id="9750f-187">Visual Studio için Çözüm Gezgini'nde hello açın **Package.appxmanifest** dosya ve ayarlayın **bildirim özellikli** çok**Evet** altında **bildirimleri**.</span><span class="sxs-lookup"><span data-stu-id="9750f-187">In Solution Explorer for Visual Studio, open hello **Package.appxmanifest** file, and set **Toast Capable** too**Yes** under **Notifications**.</span></span>
5. <span data-ttu-id="9750f-188">Merhaba uygulama derleyin ve hata olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9750f-188">Build hello app and verify you have no errors.</span></span> <span data-ttu-id="9750f-189">İstemci uygulamanızın artık Mobile Apps bitiş hello şablon bildirimleri için hello kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9750f-189">Your client app should now register for hello template notifications from hello Mobile Apps back end.</span></span> <span data-ttu-id="9750f-190">Bu bölümde, çözümünüz içinde her Windows projesi için tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="9750f-190">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="9750f-191">Windows uygulamanızı test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="9750f-191">Test push notifications in your Windows app</span></span>
1. <span data-ttu-id="9750f-192">Visual Studio'da Windows projesine sağ tıklayın ve **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="9750f-192">In Visual Studio, right-click a Windows project, and click **Set as startup project**.</span></span>
2. <span data-ttu-id="9750f-193">Tuşuna hello **çalıştırmak** düğmesini toobuild hello proje ve hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="9750f-193">Press hello **Run** button toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="9750f-194">Merhaba uygulamasında yeni bir todoıtem için bir ad yazın ve ardından hello artı (**+**) simgesi tooadd.</span><span class="sxs-lookup"><span data-stu-id="9750f-194">In hello app, type a name for a new todoitem, and then click hello plus (**+**) icon tooadd it.</span></span>
4. <span data-ttu-id="9750f-195">Merhaba öğesi eklendiğinde, bir bildirim alındığında doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9750f-195">Verify that a notification is received when hello item is added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9750f-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9750f-196">Next steps</span></span>
<span data-ttu-id="9750f-197">Anında iletme bildirimleri hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9750f-197">You can learn more about push notifications:</span></span>

* [<span data-ttu-id="9750f-198">Anında iletme bildirimi sorunlarını tanılamak</span><span class="sxs-lookup"><span data-stu-id="9750f-198">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="9750f-199">Neden bildirimleri bırakılan veya cihazlarda bitmeyen çeşitli nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="9750f-199">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="9750f-200">Bu konu nasıl anında iletme bildirimi hatalarının tooanalyze ve Şekil hello kök çıkışı neden gösterir.</span><span class="sxs-lookup"><span data-stu-id="9750f-200">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="9750f-201">Eğitim aşağıdaki hello tooone üzerinde de devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9750f-201">You can also continue on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="9750f-202">Kimlik doğrulama tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="9750f-202">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="9750f-203">Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="9750f-203">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="9750f-204">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="9750f-204">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="9750f-205">Bilgi nasıl tooadd çevrimdışı destek Mobile Apps kullanarak uygulamanız için yedekleme son.</span><span class="sxs-lookup"><span data-stu-id="9750f-205">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="9750f-206">Çevrimdışı Eşitleme ile kullanıcılar mobil uygulama ile etkileşim kurabilen&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="9750f-206">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[Xcode]: https://go.microsoft.com/fwLink/?LinkID=266532
[apns object]: http://go.microsoft.com/fwlink/p/?LinkId=272333
