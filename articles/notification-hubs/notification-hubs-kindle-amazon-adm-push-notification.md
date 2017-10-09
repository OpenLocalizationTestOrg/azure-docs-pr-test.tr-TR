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
# <a name="get-started-with-notification-hubs-for-kindle-apps"></a><span data-ttu-id="88ea1-103">Kindle uygulamaları için Notification Hubs'ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="88ea1-103">Get started with Notification Hubs for Kindle apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="88ea1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="88ea1-104">Overview</span></span>
<span data-ttu-id="88ea1-105">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooa Kindle uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="88ea1-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Kindle application.</span></span>
<span data-ttu-id="88ea1-106">Amazon Device Messaging'i (ADM) kullanarak anında iletme bildirimleri alan boş bir Kindle uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="88ea1-106">You'll create a blank Kindle app that receives push notifications by using Amazon Device Messaging (ADM).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88ea1-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="88ea1-107">Prerequisites</span></span>
<span data-ttu-id="88ea1-108">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="88ea1-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="88ea1-109">Hello Hello Android (varsayıyoruz Eclipse kullanacağınızı) SDK'sı Al <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span><span class="sxs-lookup"><span data-stu-id="88ea1-109">Get hello Android SDK (we assume that you will use Eclipse) from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a>.</span></span>
* <span data-ttu-id="88ea1-110">Merhaba adımları <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">ayarı yukarı geliştirme ortamınıza</a> tooset Kindle için geliştirme ortamınızı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="88ea1-110">Follow hello steps in <a href="https://developer.amazon.com/appsandservices/resources/development-tools/ide-tools/tech-docs/01-setting-up-your-development-environment">Setting Up Your Development Environment</a> tooset up your development environment for Kindle.</span></span>

## <a name="add-a-new-app-toohello-developer-portal"></a><span data-ttu-id="88ea1-111">Yeni bir uygulama toohello Geliştirici Portalı ekleme</span><span class="sxs-lookup"><span data-stu-id="88ea1-111">Add a new app toohello developer portal</span></span>
1. <span data-ttu-id="88ea1-112">İlk olarak, bir uygulama hello oluşturmak [Amazon Geliştirici Portalı].</span><span class="sxs-lookup"><span data-stu-id="88ea1-112">First, create an app in hello [Amazon developer portal].</span></span>
   
    ![][0]
2. <span data-ttu-id="88ea1-113">Kopya hello **uygulama anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="88ea1-113">Copy hello **Application Key**.</span></span>
   
    ![][1]
3. <span data-ttu-id="88ea1-114">Merhaba portalında uygulamanızı hello adına tıklayın ve hello ardından **Device Messaging** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="88ea1-114">In hello portal, click hello name of your app, and then click hello **Device Messaging** tab.</span></span>
   
    ![][2]
4. <span data-ttu-id="88ea1-115">**Create a New Security Profile** (Yeni Bir Güvenlik Profili Oluştur) seçeneğine tıklayın ve ardından yeni bir güvenlik profili oluşturun (örneğin, **TestAdm güvenlik profili**).</span><span class="sxs-lookup"><span data-stu-id="88ea1-115">Click **Create a New Security Profile**, and then create a new security profile (for example, **TestAdm security profile**).</span></span> <span data-ttu-id="88ea1-116">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-116">Then click **Save**.</span></span>
   
    ![][3]
5. <span data-ttu-id="88ea1-117">Tıklatın **güvenlik profilleri** oluşturduğunuz tooview hello güvenlik profili.</span><span class="sxs-lookup"><span data-stu-id="88ea1-117">Click **Security Profiles** tooview hello security profile that you just created.</span></span> <span data-ttu-id="88ea1-118">Kopya hello **istemci kimliği** ve **gizli** daha sonra kullanmak için değerler.</span><span class="sxs-lookup"><span data-stu-id="88ea1-118">Copy hello **Client ID** and **Client Secret** values for later use.</span></span>
   
    ![][4]

## <a name="create-an-api-key"></a><span data-ttu-id="88ea1-119">API Anahtarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="88ea1-119">Create an API key</span></span>
1. <span data-ttu-id="88ea1-120">Yönetici ayrıcalıklarına sahip bir komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-120">Open a command prompt with administrator privileges.</span></span>
2. <span data-ttu-id="88ea1-121">Toohello Android SDK klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="88ea1-121">Navigate toohello Android SDK folder.</span></span>
3. <span data-ttu-id="88ea1-122">Merhaba aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="88ea1-122">Enter hello following command:</span></span>
   
        keytool -list -v -alias androiddebugkey -keystore ./debug.keystore
   
    ![][5]
4. <span data-ttu-id="88ea1-123">Hello için **keystore** parola, türü **android**.</span><span class="sxs-lookup"><span data-stu-id="88ea1-123">For hello **keystore** password, type **android**.</span></span>
5. <span data-ttu-id="88ea1-124">Kopya hello **MD5** parmak izi.</span><span class="sxs-lookup"><span data-stu-id="88ea1-124">Copy hello **MD5** fingerprint.</span></span>
6. <span data-ttu-id="88ea1-125">Merhaba üzerinde hello Geliştirici Portalı'nda geri **ileti** sekmesini tıklatın, **Android/Kindle** ve uygulamanız için hello hello paket adını girin (örneğin, **com.sample.notificationhubtest**) ve hello **MD5** değer ve ardından **API anahtarı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="88ea1-125">Back in hello developer portal, on hello **Messaging** tab, click **Android/Kindle** and enter hello name of hello package for your app (for example, **com.sample.notificationhubtest**) and hello **MD5** value, and then click **Generate API Key**.</span></span>

## <a name="add-credentials-toohello-hub"></a><span data-ttu-id="88ea1-126">Kimlik bilgileri toohello hub ekleme</span><span class="sxs-lookup"><span data-stu-id="88ea1-126">Add credentials toohello hub</span></span>
<span data-ttu-id="88ea1-127">Merhaba portalında hello istemci gizli anahtarı ve istemci kimliği toohello ekleme **yapılandırma** bildirim hub'ınızın sekmesi.</span><span class="sxs-lookup"><span data-stu-id="88ea1-127">In hello portal, add hello client secret and client ID toohello **Configure** tab of your notification hub.</span></span>

## <a name="set-up-your-application"></a><span data-ttu-id="88ea1-128">Uygulamanızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="88ea1-128">Set up your application</span></span>
> [!NOTE]
> <span data-ttu-id="88ea1-129">Bir uygulama oluştururken, en az API Düzeyi 17 kullanın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-129">When you're creating an application, use at least API Level 17.</span></span>
> 
> 

<span data-ttu-id="88ea1-130">Merhaba ADM kitaplıkları tooyour Eclipse projenizin ekleyin:</span><span class="sxs-lookup"><span data-stu-id="88ea1-130">Add hello ADM libraries tooyour Eclipse project:</span></span>

1. <span data-ttu-id="88ea1-131">tooobtain hello ADM kitaplığını [hello SDK Yükle].</span><span class="sxs-lookup"><span data-stu-id="88ea1-131">tooobtain hello ADM library, [download hello SDK].</span></span> <span data-ttu-id="88ea1-132">Merhaba SDK zip dosyasını ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-132">Extract hello SDK zip file.</span></span>
2. <span data-ttu-id="88ea1-133">Eclipse'te, projenize sağ tıklayın ve ardından **Properties** (Özellikler) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-133">In Eclipse, right-click your project, and then click **Properties**.</span></span> <span data-ttu-id="88ea1-134">Seçin **Java oluşturma yolu** sol hello ve ardından hello ** kitaplıkları ** sekmesini hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="88ea1-134">Select **Java Build Path** on hello left, and then select hello **Libraries **tab at hello top.</span></span> <span data-ttu-id="88ea1-135">Tıklatın **dış Jar Ekle**ve select hello dosya `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` hello Amazon SDK'sını ayıkladığınız hello dizininden.</span><span class="sxs-lookup"><span data-stu-id="88ea1-135">Click **Add External Jar**, and select hello file `\SDK\Android\DeviceMessaging\lib\amazon-device-messaging-*.jar` from hello directory in which you extracted hello Amazon SDK.</span></span>
3. <span data-ttu-id="88ea1-136">Merhaba NotificationHubs Android SDK (bağlantı) indirin.</span><span class="sxs-lookup"><span data-stu-id="88ea1-136">Download hello NotificationHubs Android SDK (link).</span></span>
4. <span data-ttu-id="88ea1-137">Merhaba paketin sıkıştırmasını açın ve sonra hello dosyayı sürükleyin `notification-hubs-sdk.jar` hello içine `libs` Eclipse klasöründe.</span><span class="sxs-lookup"><span data-stu-id="88ea1-137">Unzip hello package, and then drag hello file `notification-hubs-sdk.jar` into hello `libs` folder in Eclipse.</span></span>

<span data-ttu-id="88ea1-138">Uygulama bildirimi toosupport ADM düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="88ea1-138">Edit your app manifest toosupport ADM:</span></span>

1. <span data-ttu-id="88ea1-139">Merhaba Amazon ad hello kök bildirim öğesine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="88ea1-139">Add hello Amazon namespace in hello root manifest element:</span></span>

        xmlns:amazon="http://schemas.amazon.com/apk/res/android"

1. <span data-ttu-id="88ea1-140">Merhaba hello bildirim öğesinin altına ilk öğe olarak izinleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="88ea1-140">Add permissions as hello first element under hello manifest element.</span></span> <span data-ttu-id="88ea1-141">Yedek **[YOUR PACKAGE NAME]** uygulamanızı toocreate kullanılan hello Paketle.</span><span class="sxs-lookup"><span data-stu-id="88ea1-141">Substitute **[YOUR PACKAGE NAME]** with hello package that you used toocreate your app.</span></span>
   
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
2. <span data-ttu-id="88ea1-142">Hello hello uygulama öğesinin ilk alt öğesi aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="88ea1-142">Insert hello following element as hello first child of hello application element.</span></span> <span data-ttu-id="88ea1-143">Toosubstitute unutmayın **[YOUR SERVICE NAME]** hello sonraki bölümde (dahil olmak üzere hello paketi) oluşturmak ve değiştirmek ADM ileti işleyicinizi hello adıyla **[YOUR PACKAGE NAME]** hello ile Uygulamanızı oluşturduğunuz paket adı.</span><span class="sxs-lookup"><span data-stu-id="88ea1-143">Remember toosubstitute **[YOUR SERVICE NAME]** with hello name of your ADM message handler that you create in hello next section (including hello package), and replace **[YOUR PACKAGE NAME]** with hello package name with which you created your app.</span></span>
   
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

## <a name="create-your-adm-message-handler"></a><span data-ttu-id="88ea1-144">ADM ileti işleyicinizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="88ea1-144">Create your ADM message handler</span></span>
1. <span data-ttu-id="88ea1-145">Öğesinden devralınan yeni bir sınıf oluşturun `com.amazon.device.messaging.ADMMessageHandlerBase` ve adlandırın `MyADMMessageHandler`hello aşağıdaki şekilde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="88ea1-145">Create a new class that inherits from `com.amazon.device.messaging.ADMMessageHandlerBase` and name it `MyADMMessageHandler`, as shown in hello following figure:</span></span>
   
    ![][6]
2. <span data-ttu-id="88ea1-146">Merhaba aşağıdakileri ekleyin `import` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="88ea1-146">Add hello following `import` statements:</span></span>
   
        import android.app.NotificationManager;
        import android.app.PendingIntent;
        import android.content.Context;
        import android.content.Intent;
        import android.support.v4.app.NotificationCompat;
        import com.amazon.device.messaging.ADMMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub
3. <span data-ttu-id="88ea1-147">Oluşturduğunuz hello sınıfında koddan hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="88ea1-147">Add hello following code in hello class that you created.</span></span> <span data-ttu-id="88ea1-148">Toosubstitute hello hub adını ve bağlantı dizesini (Dinleme) unutmayın:</span><span class="sxs-lookup"><span data-stu-id="88ea1-148">Remember toosubstitute hello hub name and connection string (listen):</span></span>
   
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
4. <span data-ttu-id="88ea1-149">Aşağıdaki kodu toohello hello eklemek `OnMessage()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="88ea1-149">Add hello following code toohello `OnMessage()` method:</span></span>
   
        String nhMessage = intent.getExtras().getString("msg");
        sendNotification(nhMessage);
5. <span data-ttu-id="88ea1-150">Aşağıdaki kodu toohello hello eklemek `OnRegistered` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="88ea1-150">Add hello following code toohello `OnRegistered` method:</span></span>
   
            try {
        getNotificationHub(getApplicationContext()).register(registrationId);
            } catch (Exception e) {
        Log.e("[your package name]", "Fail onRegister: " + e.getMessage(), e);
            }
6. <span data-ttu-id="88ea1-151">Aşağıdaki kodu toohello hello eklemek `OnUnregistered` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="88ea1-151">Add hello following code toohello `OnUnregistered` method:</span></span>
   
         try {
             getNotificationHub(getApplicationContext()).unregister();
         } catch (Exception e) {
             Log.e("[your package name]", "Fail onUnregister: " + e.getMessage(), e);
         }
7. <span data-ttu-id="88ea1-152">Merhaba, `MainActivity` yöntemi, içeri aktarma deyimini aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="88ea1-152">In hello `MainActivity` method, add hello following import statement:</span></span>
   
        import com.amazon.device.messaging.ADM;
8. <span data-ttu-id="88ea1-153">Merhaba hello sonunda koddan hello eklemek `OnCreate` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="88ea1-153">Add hello following code at hello end of hello `OnCreate` method:</span></span>
   
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

## <a name="add-your-api-key-tooyour-app"></a><span data-ttu-id="88ea1-154">API anahtar tooyour uygulamanızı ekleme</span><span class="sxs-lookup"><span data-stu-id="88ea1-154">Add your API key tooyour app</span></span>
1. <span data-ttu-id="88ea1-155">Eclipse'te, adlı yeni bir dosya oluşturun **api_key.txt** hello projenizin dizin varlıkları içinde.</span><span class="sxs-lookup"><span data-stu-id="88ea1-155">In Eclipse, create a new file named **api_key.txt** in hello directory assets of your project.</span></span>
2. <span data-ttu-id="88ea1-156">Merhaba Amazon Geliştirici Portalı'nda oluşturulan hello dosya ve kopyalama hello API anahtarı açın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-156">Open hello file and copy hello API key that you generated in hello Amazon developer portal.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="88ea1-157">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="88ea1-157">Run hello app</span></span>
1. <span data-ttu-id="88ea1-158">Merhaba öykünücüsünde başlatın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-158">Start hello emulator.</span></span>
2. <span data-ttu-id="88ea1-159">Merhaba üstten Hello öykünücüsünde içeri doğru çekin ve tıklayın **ayarları**ve ardından **Hesabımı** ve geçerli bir Amazon hesabıyla kaydolun.</span><span class="sxs-lookup"><span data-stu-id="88ea1-159">In hello emulator, swipe from hello top and click **Settings**, and then click **My account** and register with a valid Amazon account.</span></span>
3. <span data-ttu-id="88ea1-160">Eclipse'te, hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="88ea1-160">In Eclipse, run hello app.</span></span>

> [!NOTE]
> <span data-ttu-id="88ea1-161">Bir sorun oluşursa, başlangıç saati hello öykünücü (veya aygıt) denetleyin.</span><span class="sxs-lookup"><span data-stu-id="88ea1-161">If a problem occurs, check hello time of hello emulator (or device).</span></span> <span data-ttu-id="88ea1-162">Merhaba zaman değerinin doğru olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="88ea1-162">hello time value must be accurate.</span></span> <span data-ttu-id="88ea1-163">Merhaba Kindle öykünücüsü toochange başlangıç saati, çalıştırabilirsiniz hello komutu, Android SDK platformunuzun Araçlar dizininden aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="88ea1-163">toochange hello time of hello Kindle emulator, you can run hello following command from your Android SDK platform-tools directory:</span></span>
> 
> 

        adb shell  date -s "yyyymmdd.hhmmss"

## <a name="send-a-message"></a><span data-ttu-id="88ea1-164">İleti gönderme</span><span class="sxs-lookup"><span data-stu-id="88ea1-164">Send a message</span></span>
<span data-ttu-id="88ea1-165">.NET kullanarak ileti toosend:</span><span class="sxs-lookup"><span data-stu-id="88ea1-165">toosend a message by using .NET:</span></span>

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
