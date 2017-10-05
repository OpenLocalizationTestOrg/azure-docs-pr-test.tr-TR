---
title: "Kindle uygulamaları için Azure Notification Hubs'ı kullanmaya başlama | Microsoft Belgeleri"
description: "Bu öğreticide, bir Kindle uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını öğrenirsiniz."
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
ms.openlocfilehash: 7206f152ed7270abc62536a9ee164f7227833bcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="06a7a-103">Kindle uygulamaları için Notification Hubs'ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="06a7a-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="06a7a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="06a7a-104">Overview</span></span>
<span data-ttu-id="06a7a-105">Bu öğretici, bir Kindle uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını size gösterir.</span><span class="sxs-lookup"><span data-stu-id="06a7a-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Kindle application.</span></span>
<span data-ttu-id="06a7a-106">Amazon Device Messaging'i (ADM) kullanarak anında iletme bildirimleri alan boş bir Kindle uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="06a7a-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06a7a-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="06a7a-107">Prerequisites</span></span>
<span data-ttu-id="06a7a-108">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="06a7a-108">This tutorial requires the following:</span></span>

* <span data-ttu-id="06a7a-109"><a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android sitesi</a>'nden Android SDK'sını alın (Eclipse kullanacağınızı varsayıyoruz).</span><span class="sxs-lookup"><span data-stu-id="06a7a-109">Get the Android SDK (we assume that you will use Eclipse) from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="06a7a-110">Kindle için geliştirme ortamınızı ayarlamak üzere <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Geliştirme Ortamınızı Ayarlama</a>'daki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-110">Follow the steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> to set up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-to-the-developer-portal"></a><span data-ttu-id="06a7a-111">Geliştirici portalına yeni bir uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="06a7a-111">Add a new app to the developer portal</span></span>
1. <span data-ttu-id="06a7a-112">Öncelikle, [Amazon geliştirici portalı]'nda bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06a7a-112">First, create an app in the [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="06a7a-113">**Application Key**'i (Uygulama Anahtarı) kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-113">Copy the **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="06a7a-114">Portalda, uygulamanızın adına ve ardından **Device Messaging** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-114">In the portal, click the name of your app, and then click the **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="06a7a-115">**Create a New Security Profile** (Yeni Bir Güvenlik Profili Oluştur) seçeneğine tıklayın ve ardından yeni bir güvenlik profili oluşturun (örneğin, **TestAdm güvenlik profili**).</span><span class="sxs-lookup"><span data-stu-id="06a7a-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="06a7a-116">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="06a7a-117">Az önce oluşturduğunuz güvenlik profilini görüntülemek için **Security Profiles** (Güvenlik Profilleri) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-117">Click **Security Profiles** to view the security profile that you just created.</span></span> <span data-ttu-id="06a7a-118">Daha sonra kullanmak için **Client ID** (İstemci Kimliği) ve **Client Secret** (Gizli Anahtar) değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-118">Copy the **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="06a7a-119">API Anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="06a7a-119">Create an API key</span></span>
1. <span data-ttu-id="06a7a-120">Yönetici ayrıcalıklarına sahip bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="06a7a-121">Android SDK klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-121">Navigate to the Android SDK folder.</span></span>
3. <span data-ttu-id="06a7a-122">Aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-122">Enter the following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="06a7a-123">**keystore** parolası için **android** yazın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-123">For the **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="06a7a-124">**MD5** parmak izini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-124">Copy the **MD5** fingerprint.</span></span>
6. <span data-ttu-id="06a7a-125">Geliştirici portalına geri dönün. **Messaging** sekmesinde **Android/Kindle**'a tıklayın, uygulamanız için olan paket adını (örneğin, **com.sample.notificationhubtest**) ve **MD5** değerini girin, ardından **Generate API Key** (API Anahtarı Oluştur) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-125">Back in the developer portal, on the **Messaging** tab, click **Android/Kindle** and enter the name of the package for your app (for example, **com.sample.notificationhubtest**) and the **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-to-the-hub"></a><span data-ttu-id="06a7a-126">Hub'a kimlik bilgileri ekleme</span><span class="sxs-lookup"><span data-stu-id="06a7a-126">Add credentials to the hub</span></span>
<span data-ttu-id="06a7a-127">Portalda, bildirim hub'ınızın **Configure** (Yapılandır) sekmesine gizli anahtarı ve istemci kimliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-127">In the portal, add the client secret and client ID to the **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="06a7a-128">Uygulamanızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="06a7a-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="06a7a-129">Bir uygulama oluştururken, en az API Düzeyi 17 kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="06a7a-130">ADM kitaplıklarını Eclipse projenize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-130">Add the ADM libraries to your Eclipse project:</span></span>

1. <span data-ttu-id="06a7a-131">ADM kitaplığını almak için [SDK’yı indirin].</span><span class="sxs-lookup"><span data-stu-id="06a7a-131">To obtain the ADM library, [download the SDK].</span></span> <span data-ttu-id="06a7a-132">SDK zip dosyasını ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-132">Extract the SDK zip file.</span></span>
2. <span data-ttu-id="06a7a-133">Eclipse'te, projenize sağ tıklayın ve ardından **Properties** (Özellikler) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="06a7a-134">Seçin **Java oluşturma yolu** solda ve ardından ** kitaplıkları ** üst sekmesini.</span><span class="sxs-lookup"><span data-stu-id="06a7a-134">Select **Java Build Path** on the left, and then select the **Libraries **tab at the top.</span></span> <span data-ttu-id="06a7a-135">**Add External Jar** (Dış Jar Ekle) seçeneğine tıklayın ve Amazon SDK'sını ayıkladığınız dizinden `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-135">Click **Add External Jar**, and select the file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from the directory in which you extracted the Amazon SDK.</span></span>
3. <span data-ttu-id="06a7a-136">NotificationHubs Android SDK'sını indirin (bağlantı).</span><span class="sxs-lookup"><span data-stu-id="06a7a-136">Download the NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="06a7a-137">Paketin sıkıştırmasını açın ve ardından `notification-hubs-sdk.jar` dosyasını Eclipse'te `libs` klasörünün içine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-137">Unzip the package, and then drag the file `notification-hubs-sdk.jar` into the `libs` folder in Eclipse.</span></span>

<span data-ttu-id="06a7a-138">ADM'yi desteklemesi için uygulama bildiriminizi düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-138">Edit your app manifest to support ADM:</span></span>

1. <span data-ttu-id="06a7a-139">Amazon ad alanını kök bildirim öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-139">Add the Amazon namespace in the root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="06a7a-140">Bildirim öğesinin altına ilk öğe olarak izinleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-140">Add permissions as the first element under the manifest element.</span></span> <span data-ttu-id="06a7a-141">**[YOUR PACKAGE NAME]** öğesini uygulamanızı oluşturmak için kullandığınız paket adı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-141">Substitute **[YOUR PACKAGE NAME]** with the package that you used to create your app.</span></span>
   
        <permission
         android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE"
         android:protectionLevel="signature" />
   
        <uses-permission android:name="android.permission.INTERNET"/>
   
        <uses-permission android:name="[YOUR PACKAGE NAME].permission.RECEIVE_ADM_MESSAGE" />
   
        <!-- This permission allows your app access to receive push notifications
        from ADM. -->
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE" />
   
        <!-- ADM uses WAKE_LOCK to keep the processor from sleeping when a message is received. -->
        <uses-permission android:name="android.permission.WAKE_LOCK" />
2. <span data-ttu-id="06a7a-142">Uygulama öğesinin ilk alt öğesi olarak aşağıdaki öğeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-142">Insert the following element as the first child of the application element.</span></span> <span data-ttu-id="06a7a-143">**[YOUR SERVICE NAME]**'i sonraki bölümde oluşturduğunuz ADM ileti işleyicisi adı ile değiştirmeyi unutmayın (paket dahil) ve **[YOUR PACKAGE NAME]**'i uygulamanızı oluşturduğunuz paket adı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-143">Remember to substitute **[YOUR SERVICE NAME]** with the name of your ADM message handler that you create in the next section (including the package), and replace **[YOUR PACKAGE NAME]** with the package name with which you created your app.</span></span>
   
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
   
            <!-- To interact with ADM, your app must listen for the following intents. -->
            <intent-filter>
          <action android:name="com.amazon.device.messaging.intent.REGISTRATION" />
          <action android:name="com.amazon.device.messaging.intent.RECEIVE" />
   
          <!-- Replace the name in the category tag with your app's package name. -->
          <category android:name="[YOUR PACKAGE NAME]" />
            </intent-filter>
        </receiver>

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="06a7a-144">ADM ileti işleyicinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="06a7a-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="06a7a-145">Aşağıdaki şekilde gösterildiği gibi, `com.amazon.device.messaging.ADMMessageHandlerBase` öğesinden devralınan yeni bir sınıf oluşturun ve bunu `MyADMMessageHandler` olarak adlandırın:</span><span class="sxs-lookup"><span data-stu-id="06a7a-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in the following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="06a7a-146">Aşağıdaki `import` deyimlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-146">Add the following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="06a7a-147">Oluşturduğunuz sınıfa aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-147">Add the following code in the class that you created.</span></span> <span data-ttu-id="06a7a-148">Hub adını ve bağlantı dizesini (dinleme) değiştirmeyi unutmayın:</span><span class="sxs-lookup"><span data-stu-id="06a7a-148">Remember to substitute the hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="06a7a-149">`OnMessage()` yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-149">Add the following code to the `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="06a7a-150">`OnRegistered` yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-150">Add the following code to the `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="06a7a-151">`OnUnregistered` yöntemine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-151">Add the following code to the `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="06a7a-152">`MainActivity` yönteminde aşağıdaki içeri aktarma deyimini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-152">In the `MainActivity` method, add the following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="06a7a-153">`OnCreate` yönteminin sonuna aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="06a7a-153">Add the following code at the end of the `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-to-your-app"></a><span data-ttu-id="06a7a-154">Uygulamanıza API anahtarınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="06a7a-154">Add your API key to your app</span></span>
1. <span data-ttu-id="06a7a-155">Eclipse'te, projenizin dizin varlıkları içinde **api_key.txt** adlı yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="06a7a-155">In Eclipse, create a new file named **api_key.txt** in the directory assets of your project.</span></span>
2. <span data-ttu-id="06a7a-156">Dosyayı açın ve Amazon geliştirici portalında oluşturduğunuz API anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-156">Open the file and copy the API key that you generated in the Amazon developer portal.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="06a7a-157">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="06a7a-157">Run the app</span></span>
1. <span data-ttu-id="06a7a-158">Öykünücüyü başlatın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-158">Start the emulator.</span></span>
2. <span data-ttu-id="06a7a-159">Öykünücüde, üstten çekin ve **Settings** (Ayarlar) seçeneğine tıklayın. Ardından **My account** (Hesabım) seçeneğine tıklayın ve geçerli bir Amazon hesabıyla kaydolun.</span><span class="sxs-lookup"><span data-stu-id="06a7a-159">In the emulator, swipe from the top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="06a7a-160">Eclipse'te uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="06a7a-160">In Eclipse, run the app.</span></span>

> [!NOTE]
> <span data-ttu-id="06a7a-161">Bir sorun oluşursa öykünücü (veya cihaz) zamanını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="06a7a-161">If a problem occurs, check the time of the emulator (or device).</span></span> <span data-ttu-id="06a7a-162">Zaman değerinin doğru olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="06a7a-162">The time value must be accurate.</span></span> <span data-ttu-id="06a7a-163">Kindle öykünücüsü zamanını değiştirmek için, Android SDK platformunuzun araçlar dizininden aşağıdaki komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="06a7a-163">To change the time of the Kindle emulator, you can run the following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="06a7a-164">İleti gönderme</span><span class="sxs-lookup"><span data-stu-id="06a7a-164">Send a message</span></span>
<span data-ttu-id="06a7a-165">.NET kullanarak ileti göndermek için:</span><span class="sxs-lookup"><span data-stu-id="06a7a-165">To send a message by using .NET:</span></span>

        static void Main(string[] args)
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("[conn string]", "[hub name]");

            hub.SendAdmNativeNotificationAsync("{\"data\":{\"msg\" : \"Hello from .NET!\"}}").Wait();
        }

![][7]

<!-- URLs. -->
<span data-ttu-id="06a7a-166">[Amazon geliştirici portalı]: https://developer.amazon.com/home.html</span><span class="sxs-lookup"><span data-stu-id="06a7a-166">[Amazon developer portal]: https://developer.amazon.com/home.html</span></span>
<span data-ttu-id="06a7a-167">[SDK’yı indirin]: https://developer.amazon.com/public/resources/development-tools/sdk</span><span class="sxs-lookup"><span data-stu-id="06a7a-167">[download the SDK]: https://developer.amazon.com/public/resources/development-tools/sdk</span></span>

[0]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal1.png
[1]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal2.png
[2]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal3.png
[3]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal4.png
[4]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-portal5.png
[5]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-cmd-window.png
[6]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-new-java-class.png
[7]: ./media/notification-hubs-kindle-get-started/notification-hub-kindle-notification.png
