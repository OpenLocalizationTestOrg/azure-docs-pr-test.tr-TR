---
title: "Azure Notification Hubs ile aaaSend anında iletme bildirimleri tooChrome uygulamaları | Microsoft Docs"
description: "Nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Chrome uygulaması hakkında bilgi edinin."
services: notification-hubs
keywords: "mobil anında iletme bildirimleri,anında iletme bildirimleri,anında iletme bildirimi,chrome anında iletme bildirimleri"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a><span data-ttu-id="b3541-104">Anında iletme bildirimleri tooChrome uygulamaları Azure Notification Hubs ile gönderme</span><span class="sxs-lookup"><span data-stu-id="b3541-104">Send push notifications tooChrome apps with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

<span data-ttu-id="b3541-105">Bu konuda nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa hello hello Google Chrome tarayıcısı bağlamında görüntülenen Chrome uygulaması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b3541-105">This topic shows you how toouse Azure Notification Hubs toosend push notifications tooa Chrome App, which will be displayed within hello context of hello Google Chrome browser.</span></span> <span data-ttu-id="b3541-106">Bu öğreticide, [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/) kullanarak anında iletme bildirimleri alan bir Chrome uygulaması oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="b3541-106">In this tutorial, we will create a Chrome app that receives push notifications by using [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/).</span></span> 

> [!NOTE]
> <span data-ttu-id="b3541-107">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3541-107">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b3541-108">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3541-108">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b3541-109">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="b3541-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="b3541-110">Merhaba öğreticide şu temel adımlarda tooenable anında iletme bildirimleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="b3541-110">hello tutorial walks you through these basic steps tooenable push notifications:</span></span>

* [<span data-ttu-id="b3541-111">Google Cloud Messaging'i etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b3541-111">Enable Google Cloud Messaging</span></span>](#register)
* [<span data-ttu-id="b3541-112">Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b3541-112">Configure your notification hub</span></span>](#configure-hub)
* [<span data-ttu-id="b3541-113">Chrome uygulaması toohello bildirim hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="b3541-113">Connect your Chrome App toohello notification hub</span></span>](#connect-app)
* [<span data-ttu-id="b3541-114">Anında iletme bildirimi tooyour Chrome uygulaması Gönder</span><span class="sxs-lookup"><span data-stu-id="b3541-114">Send a push notification tooyour Chrome App</span></span>](#send)
* [<span data-ttu-id="b3541-115">Ek işlevler ve özellikler</span><span class="sxs-lookup"><span data-stu-id="b3541-115">Additional functionality & capabilities</span></span>](#next-steps)

> [!NOTE]
> <span data-ttu-id="b3541-116">Chrome uygulaması anında iletme bildirimleri genel tarayıcı içi bildirimler olmayan - belirli toohello tarayıcı genişletilebilirlik modeli vardır (bkz [Chrome uygulamalarına genel bakış] Ayrıntılar için).</span><span class="sxs-lookup"><span data-stu-id="b3541-116">Chrome app push notifications are not generic in-browser notifications - they are specific toohello browser extensibility model (see [Chrome Apps Overview] for details).</span></span> <span data-ttu-id="b3541-117">Ayrıca Chrome uygulamaları toohello Masaüstü tarayıcısı, Apache Cordova aracılığıyla mobil (Android ve iOS) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b3541-117">In addition toohello desktop browser, Chrome apps run on mobile (Android and iOS) through Apache Cordova.</span></span> <span data-ttu-id="b3541-118">Bkz: [mobil cihazlarda Chrome uygulamaları] toolearn daha fazla.</span><span class="sxs-lookup"><span data-stu-id="b3541-118">See [Chrome Apps on Mobile] toolearn more.</span></span>
> 
> 

<span data-ttu-id="b3541-119">GCM ve Azure Notification Hubs yapılandırma olan Android için aynı tooconfiguring beri [Google Cloud Messaging for Chrome] kullanım dışı bırakıldı ve aynı GCM hello artık Android cihazları hem Chrome örneklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="b3541-119">Configuring GCM and Azure Notification Hubs is identical tooconfiguring for Android, since [Google Cloud Messaging for Chrome] has been deprecated and hello same GCM now supports both Android devices and Chrome instances.</span></span>

## <span data-ttu-id="b3541-120"><a id="register"></a>Google Cloud Messaging'i etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="b3541-120"><a id="register"></a>Enable Google Cloud Messaging</span></span>
1. <span data-ttu-id="b3541-121">Toohello gidin [Google Cloud Console] Web sitesi, Google hesabı kimlik bilgilerinizle oturum açın ve hello ardından **proje oluştur** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b3541-121">Navigate toohello [Google Cloud Console] website, sign in with your Google account credentials, and then click hello **Create Project** button.</span></span> <span data-ttu-id="b3541-122">Uygun bir sağlamak **proje adı**ve ardından hello **oluşturma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b3541-122">Provide an appropriate **Project Name**, and then click hello **Create** button.</span></span>
   
       ![Google Cloud Console - Create Project][1]
2. <span data-ttu-id="b3541-123">Merhaba Not **proje numarası** hello üzerinde **projeleri** oluşturduğunuz hello projesi için sayfa.</span><span class="sxs-lookup"><span data-stu-id="b3541-123">Make a note of hello **Project Number** on hello **Projects** page for hello project that you just created.</span></span> <span data-ttu-id="b3541-124">Bu hello kullanacağınız **GCM Gönderen Kimliği** hello Chrome uygulaması tooregister GCM ile içinde.</span><span class="sxs-lookup"><span data-stu-id="b3541-124">You will use this as hello **GCM Sender ID** in hello Chrome App tooregister with GCM.</span></span>
   
       ![Google Cloud Console - Project Number][2]
3. <span data-ttu-id="b3541-125">Merhaba sol bölmede **API'leri & auth**ve ardından aşağı kaydırın ve hello geçiş tooenable tıklatın **Google Cloud Messaging for Android**.</span><span class="sxs-lookup"><span data-stu-id="b3541-125">In hello left pane, click **APIs & auth**, and then scroll down and click hello toggle tooenable **Google Cloud Messaging for Android**.</span></span> <span data-ttu-id="b3541-126">Tooenable yok **Google Cloud Messaging for Chrome**.</span><span class="sxs-lookup"><span data-stu-id="b3541-126">You don't have tooenable **Google Cloud Messaging for Chrome**.</span></span>
   
       ![Google Cloud Console - Server Key][3]
4. <span data-ttu-id="b3541-127">Merhaba sol bölmede **kimlik bilgileri** > **yeni anahtarı oluştur** > **sunucu anahtarı** > **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b3541-127">In hello left pane, click **Credentials** > **Create New Key** > **Server Key** > **Create**.</span></span>
   
       ![Google Cloud Console - Credentials][4]
5. <span data-ttu-id="b3541-128">Merhaba sunucu Not **API anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="b3541-128">Make a note of hello server **API Key**.</span></span> <span data-ttu-id="b3541-129">Bu, bildirim hub'ı İleri tooenable yapılandırır, toosend anında iletme bildirimleri tooGCM.</span><span class="sxs-lookup"><span data-stu-id="b3541-129">You will configure this in your notification hub next, tooenable it toosend push notifications tooGCM.</span></span>
   
       ![Google Cloud Console - API Key][5]

## <span data-ttu-id="b3541-130"><a id="configure-hub"></a>Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b3541-130"><a id="configure-hub"></a>Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<span data-ttu-id="b3541-131">&emsp;&emsp;6.</span><span class="sxs-lookup"><span data-stu-id="b3541-131">&emsp;&emsp;6.</span></span>   <span data-ttu-id="b3541-132">Merhaba, **ayarları** dikey penceresinde, select **Bildirim Hizmetleri** ve ardından **Google (GCM)**.</span><span class="sxs-lookup"><span data-stu-id="b3541-132">In hello **Settings** blade, select **Notification Services** and then **Google (GCM)**.</span></span> <span data-ttu-id="b3541-133">Merhaba API anahtarını girin ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b3541-133">Enter hello API key and save.</span></span>

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <span data-ttu-id="b3541-135"><a id="connect-app"></a>Chrome uygulaması toohello bildirim hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="b3541-135"><a id="connect-app"></a>Connect your Chrome App toohello notification hub</span></span>
<span data-ttu-id="b3541-136">Bildirim hub'ınız şimdi GCM ile yapılandırılmış toowork olduğu ve uygulama tooboth anında iletme bildirimleri göndermenizi ve hello bağlantı dizeleri tooregister sahip.</span><span class="sxs-lookup"><span data-stu-id="b3541-136">Your notification hub is now configured toowork with GCM, and you have hello connection strings tooregister your app tooboth receive and send push notifications.</span></span> <span data-ttu-id="b3541-137">LK</span><span class="sxs-lookup"><span data-stu-id="b3541-137">LK</span></span>

### <a name="create-a-new-chrome-app"></a><span data-ttu-id="b3541-138">Yeni bir Chrome Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="b3541-138">Create a new Chrome App</span></span>
<span data-ttu-id="b3541-139">Aşağıdaki Hello örneği üzerinde hello temel [Chrome uygulaması GCM örneği] ve kullandığı hello bir Chrome uygulaması şekilde toocreate önerilir.</span><span class="sxs-lookup"><span data-stu-id="b3541-139">hello sample below is based on hello [Chrome App GCM Sample] and uses hello recommended way toocreate a Chrome App.</span></span> <span data-ttu-id="b3541-140">Biz hello adımları özellikle ilgili tooAzure bildirim hub'ları vurgular.</span><span class="sxs-lookup"><span data-stu-id="b3541-140">We will highlight hello steps specifically related tooAzure Notification Hubs.</span></span> 

> [!NOTE]
> <span data-ttu-id="b3541-141">Bu Chrome uygulamasının hello kaynak karşıdan öneririz [Chrome uygulaması bildirim hub'ı örneği].</span><span class="sxs-lookup"><span data-stu-id="b3541-141">We recommend that you download hello source for this Chrome App from [Chrome App Notification Hub Sample].</span></span>
> 
> 

<span data-ttu-id="b3541-142">Merhaba Chrome uygulaması JavaScript aracılığıyla oluşturulur ve oluşturmak için tercih edilen sözcük düzenleyicisini birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3541-142">hello Chrome App is created via JavaScript, and you can use any of your preferred word editors for creating it.</span></span> <span data-ttu-id="b3541-143">Aşağıda, bu Chrome Uygulamasının nasıl görüneceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b3541-143">Below is what this Chrome App will look like.</span></span>

![Google Chrome Uygulaması][15]

1. <span data-ttu-id="b3541-145">Bir klasör oluşturun ve `ChromePushApp` olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="b3541-145">Create a folder and name it `ChromePushApp`.</span></span> <span data-ttu-id="b3541-146">Elbette, hello rastgele bir addır - farklı bir ad kullanırsanız hello hello gerekli kod kesimlerinde yolu değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b3541-146">Of course, hello name is arbitrary - if you name it something different, make sure you substitute hello path in hello required code segments.</span></span>
2. <span data-ttu-id="b3541-147">Merhaba karşıdan [crypto-js Kitaplığı] hello ikinci adımda oluşturduğunuz hello klasöründeki.</span><span class="sxs-lookup"><span data-stu-id="b3541-147">Download hello [crypto-js library] in hello folder you created in hello second step.</span></span> <span data-ttu-id="b3541-148">Bu kitaplık klasörü iki alt klasör içerir: `components` ve `rollups`.</span><span class="sxs-lookup"><span data-stu-id="b3541-148">This library folder will contain two subfolders: `components` and `rollups`.</span></span>
3. <span data-ttu-id="b3541-149">Bir `manifest.json` dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3541-149">Create a `manifest.json` file.</span></span> <span data-ttu-id="b3541-150">Tüm Chrome uygulamaları hello uygulama meta verilerini ve en içeren bir bildirim dosyası tarafından yedeklenen hello kullanıcı yüklediğinde toohello uygulama verilen önemlisi, tüm izinleri.</span><span class="sxs-lookup"><span data-stu-id="b3541-150">All Chrome Apps are backed by a manifest file that contains hello app metadata and, most importantly, all permissions that are granted toohello app when hello user installs it.</span></span>
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    <span data-ttu-id="b3541-151">Bildirim hello `permissions` bu Chrome uygulaması GCM mümkün tooreceive anında iletme bildirimleri olacağını belirten öğesi.</span><span class="sxs-lookup"><span data-stu-id="b3541-151">Notice hello `permissions` element, which specifies that this Chrome App will be able tooreceive push notifications from GCM.</span></span> <span data-ttu-id="b3541-152">Ayrıca hello Azure bildirim hub'ları hello Chrome uygulaması REST çağrısı tooregister burada yapacak URI belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3541-152">It must also specify hello Azure Notification Hubs URI where hello Chrome App will make a REST call tooregister.</span></span>
    <span data-ttu-id="b3541-153">Bizim örnek uygulamamız da bir simge dosyası kullanan `gcm_128.png`, hello özgün GCM örneğinden yeniden kullanılan hello kaynaktaki bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b3541-153">Our sample app also uses an icon file, `gcm_128.png`, that you will find at hello source that's reused from hello original GCM sample.</span></span> <span data-ttu-id="b3541-154">Merhaba uygun herhangi bir görüntü için alternatif [simge ölçütleri](https://developer.chrome.com/apps/manifest/icons).</span><span class="sxs-lookup"><span data-stu-id="b3541-154">You can substitute it for any image that fits hello [icon criteria](https://developer.chrome.com/apps/manifest/icons).</span></span>
4. <span data-ttu-id="b3541-155">Adlı bir dosya oluşturun `background.js` koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="b3541-155">Create a file called `background.js` with hello following code:</span></span>
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    <span data-ttu-id="b3541-156">Bu, hello Chrome uygulama penceresi HTML'sini hello dosyasıdır (**register.html**) ve ayrıca hello işleyicisini tanımlar **messageReceived** toohandle hello gelen anında iletme bildirimi.</span><span class="sxs-lookup"><span data-stu-id="b3541-156">This is hello file that pops up hello Chrome App window HTML (**register.html**) and also defines hello handler **messageReceived** toohandle hello incoming push notification.</span></span>
5. <span data-ttu-id="b3541-157">Adlı bir dosya oluşturun `register.html` -bu hello hello Chrome uygulamasının kullanıcı arabirimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b3541-157">Create a file called `register.html` - this defines hello UI of hello Chrome App.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b3541-158">Bu örnekte **CryptoJS v3.1.2** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b3541-158">This sample uses **CryptoJS v3.1.2**.</span></span> <span data-ttu-id="b3541-159">Merhaba kitaplığının başka bir sürümünü yüklediyseniz, hello hello sürümünde düzgün şekilde değiştirdiğinizden emin olun `src` yolu.</span><span class="sxs-lookup"><span data-stu-id="b3541-159">If you downloaded another version of hello library, make sure you properly substitute hello version in hello `src` path.</span></span>
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. <span data-ttu-id="b3541-160">Adlı bir dosya oluşturun `register.js` hello kodu aşağıdaki ile.</span><span class="sxs-lookup"><span data-stu-id="b3541-160">Create a file called `register.js` with hello code below.</span></span> <span data-ttu-id="b3541-161">Bu dosyanın arkasındaki hello betiği belirtir `register.html`.</span><span class="sxs-lookup"><span data-stu-id="b3541-161">This file specifies hello script behind `register.html`.</span></span> <span data-ttu-id="b3541-162">Toocreate Arabiriminiz için ayrı bir destek betiği alacak şekilde chrome uygulamaları satır içi yürütmeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="b3541-162">Chrome Apps do not allow inline execution, so you have toocreate a separate backing script for your UI.</span></span>
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    <span data-ttu-id="b3541-163">betik yukarıdaki Hello anahtar parametreleri aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="b3541-163">hello above script has hello following key parameters:</span></span>
   
   * <span data-ttu-id="b3541-164">**Window.onLoad** UI hello üzerinde hello iki düğmelerinin hello düğme tıklama olaylarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b3541-164">**window.onload** defines hello button-click events of hello two buttons on hello UI.</span></span> <span data-ttu-id="b3541-165">Biri GCM'ye kaydedilir ve diğer hello Azure Notification Hubs ile GCM tooregister kaydı sonra döndürülen hello kayıt Kimliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b3541-165">One registers with GCM, and hello other uses hello registration ID that's returned after registration with GCM tooregister with Azure Notification Hubs.</span></span>
   * <span data-ttu-id="b3541-166">**updateLog** toohandle basit günlüğe kaydetme özelliklerini tanır hello işlevdir.</span><span class="sxs-lookup"><span data-stu-id="b3541-166">**updateLog** is hello function that allows us toohandle simple logging capabilities.</span></span>
   * <span data-ttu-id="b3541-167">**registerWithGCM** hello kılan hello ilk düğme tıklama işleyicisidir `chrome.gcm.register` çağrısı tooGCM tooregister hello geçerli Chrome uygulaması örneğini.</span><span class="sxs-lookup"><span data-stu-id="b3541-167">**registerWithGCM** is hello first button-click handler, which makes hello `chrome.gcm.register` call tooGCM tooregister hello current Chrome App instance.</span></span>
   * <span data-ttu-id="b3541-168">**registerCallback** hello GCM kayıt çağrısı döndürüldüğünde çağrılan hello geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="b3541-168">**registerCallback** is hello callback function that gets called when hello GCM registration call returns.</span></span>
   * <span data-ttu-id="b3541-169">**registerWithNH** , Notification hubs'a hello ikinci düğme tıklama işleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="b3541-169">**registerWithNH** is hello second button-click handler, which registers with Notification Hubs.</span></span> <span data-ttu-id="b3541-170">Alır `hubName` ve `connectionString` (Merhaba kullanıcının belirttiği) ve el becerisi gerektiren işler hello Notification Hubs kayıt REST API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="b3541-170">It gets `hubName` and `connectionString` (which hello user has specified) and crafts hello Notification Hubs Registration REST API call.</span></span>
   * <span data-ttu-id="b3541-171">**splitConnectionString** ve **generateSaSToken** hello tüm REST API çağrılarında kullanılan bir SaS belirteci oluşturma işleminin JavaScript uygulamasını temsil eden yardımcılardır.</span><span class="sxs-lookup"><span data-stu-id="b3541-171">**splitConnectionString** and **generateSaSToken** are helpers that represent hello JavaScript implementation of a SaS token creation process, that must be used in all REST API calls.</span></span> <span data-ttu-id="b3541-172">Daha fazla bilgi için bkz. [Ortak Kavramlar](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="b3541-172">For more information, see [Common Concepts](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
   * <span data-ttu-id="b3541-173">**sendNHRegistrationRequest** HTTP REST yapar hello işlevi çağırmak tooAzure bildirim hub'ları.</span><span class="sxs-lookup"><span data-stu-id="b3541-173">**sendNHRegistrationRequest** is hello function that makes a HTTP REST call tooAzure Notification Hubs.</span></span>
   * <span data-ttu-id="b3541-174">**registrationPayload** hello kayıt XML yükünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b3541-174">**registrationPayload** defines hello registration XML payload.</span></span> <span data-ttu-id="b3541-175">Daha fazla bilgi için bkz. [Kayıt NH REST API’si oluşturma].</span><span class="sxs-lookup"><span data-stu-id="b3541-175">For more information, see [Create Registration NH REST API].</span></span> <span data-ttu-id="b3541-176">Ne GCM'den aldık ile Merhaba kayıt Kimliğini güncelleştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="b3541-176">We update hello registration ID in it with what we received from GCM.</span></span>
   * <span data-ttu-id="b3541-177">**İstemci** örneği **XMLHttpRequest** toomake hello HTTP POST isteği kullanırız.</span><span class="sxs-lookup"><span data-stu-id="b3541-177">**client** is an instance of **XMLHttpRequest** that we use toomake hello HTTP POST request.</span></span> <span data-ttu-id="b3541-178">Merhaba güncelleştiriyoruz Not `Authorization` üstbilgiyle `sasToken`.</span><span class="sxs-lookup"><span data-stu-id="b3541-178">Note that we update hello `Authorization` header with `sasToken`.</span></span> <span data-ttu-id="b3541-179">Bu çağrının başarıyla tamamlanması, bu Chrome Uygulaması örneğinin Azure Notification Hubs'a kaydedilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3541-179">Successful completion of this call will register this Chrome App instance with Azure Notification Hubs.</span></span>

<span data-ttu-id="b3541-180">Merhaba bu proje için genel klasör yapısı şuna benzemelidir: ![Google Chrome uygulaması - klasör yapısı][21]</span><span class="sxs-lookup"><span data-stu-id="b3541-180">hello overall folder structure for this project should resemble this: ![Google Chrome App - Folder Structure][21]</span></span>

### <a name="set-up-and-test-your-chrome-app"></a><span data-ttu-id="b3541-181">Chrome Uygulamanızı ayarlama ve test etme</span><span class="sxs-lookup"><span data-stu-id="b3541-181">Set up and test your Chrome App</span></span>
1. <span data-ttu-id="b3541-182">Chrome tarayıcınızı açın.</span><span class="sxs-lookup"><span data-stu-id="b3541-182">Open your Chrome browser.</span></span> <span data-ttu-id="b3541-183">**Chrome uzantıları**'nı açın ve **Geliştirici modunu** etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="b3541-183">Open **Chrome extensions** and enable **Developer mode**.</span></span>
   
       ![Google Chrome - Enable Developer Mode][16]
2. <span data-ttu-id="b3541-184">Tıklatın **paketi açılmış uzantı Yükle** ve hello dosyaları oluşturulduğu toohello klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="b3541-184">Click **Load unpacked extension** and navigate toohello folder where you created hello files.</span></span> <span data-ttu-id="b3541-185">Merhaba Ayrıca isteğe bağlı olarak kullanabileceğiniz **Chrome Apps & Extensions Developer aracı**.</span><span class="sxs-lookup"><span data-stu-id="b3541-185">You can also optionally use hello **Chrome Apps & Extensions Developer Tool**.</span></span> <span data-ttu-id="b3541-186">Bu araç kendi (Merhaba Chrome Web Mağazası ' yüklenir) içinde bir Chrome uygulaması ve Chrome uygulaması geliştirmeniz için Gelişmiş hata ayıklama özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3541-186">This tool is a Chrome App in itself (installed from hello Chrome Web Store) and provides advanced debugging capabilities for your Chrome App development.</span></span>
   
       ![Google Chrome - Load Unpacked Extension][17]
3. <span data-ttu-id="b3541-187">Ardından Hello Chrome uygulaması hatasız oluşturduysanız görünmesini Chrome uygulamanızı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b3541-187">If hello Chrome App is created without any errors, then you will see your Chrome App show up.</span></span>
   
       ![Google Chrome - Chrome App Display][18]
4. <span data-ttu-id="b3541-188">Hello girin **proje numarası** daha önce hello aldığınız **Google Cloud Console** tıklatın ve hello Gönderen Kimliği olarak **GCM ile kayıt**.</span><span class="sxs-lookup"><span data-stu-id="b3541-188">Enter hello **Project Number** that you got earlier from hello **Google Cloud Console** as hello sender ID, and click **Register with GCM**.</span></span> <span data-ttu-id="b3541-189">Selamlama iletisine görmesi gereken **başarılı GCM ile kayıt.**</span><span class="sxs-lookup"><span data-stu-id="b3541-189">You must see hello message **Registration with GCM succeeded.**</span></span>
   
       ![Google Chrome - Chrome App Customization][19]
5. <span data-ttu-id="b3541-190">Girin, **bildirim hub'ı adı** ve hello **DefaultListenSharedAccessSignature** önceki hello portal ve tıklatın Elde **Azure Notification Hubkaydetme**.</span><span class="sxs-lookup"><span data-stu-id="b3541-190">Enter your **Notification Hub Name** and hello **DefaultListenSharedAccessSignature** that you obtained from hello portal earlier, and click **Register with Azure Notification Hub**.</span></span> <span data-ttu-id="b3541-191">Selamlama iletisine görmesi gereken **bildirim hub'ı kaydı başarılı!**</span><span class="sxs-lookup"><span data-stu-id="b3541-191">You must see hello message **Notification Hub Registration successful!**</span></span> <span data-ttu-id="b3541-192">ve hello hello Azure Notification Hubs kayıt içeren hello kayıt yanıtının ayrıntılarını kimliği</span><span class="sxs-lookup"><span data-stu-id="b3541-192">and hello details of hello registration response, which contains hello Azure Notification Hubs registration ID.</span></span>
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <span data-ttu-id="b3541-193"><a name="send"></a>Bildirim tooyour Chrome uygulaması Gönder</span><span class="sxs-lookup"><span data-stu-id="b3541-193"><a name="send"></a>Send a notification tooyour Chrome App</span></span>
<span data-ttu-id="b3541-194">Test amacıyla, bir .NET konsol uygulaması kullanarak size Chrome anında iletme bildirimleri göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="b3541-194">For testing purposes, we will send Chrome push notifications by using a .NET console application.</span></span> 

> [!NOTE]
> <span data-ttu-id="b3541-195">Notification Hubs ile Ortak <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST arabirimimizi</a> kullanarak herhangi bir arka uçtan anında iletme bildirimleri gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3541-195">You can send push notifications with Notification Hubs from any backend via our public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="b3541-196">Daha fazla platformlar arası örnek için [belge portalımıza](https://azure.microsoft.com/documentation/services/notification-hubs/) göz atın.</span><span class="sxs-lookup"><span data-stu-id="b3541-196">Check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/) for more cross-platform examples.</span></span>
> 
> 

1. <span data-ttu-id="b3541-197">Merhaba gelen Visual Studio **dosya** menüsünde, select **yeni** ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="b3541-197">In Visual Studio, from hello **File** menu, select **New** and then **Project**.</span></span> <span data-ttu-id="b3541-198">**Visual C#** altında, **Windows** ve **Konsol Uygulaması**'na, ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b3541-198">Under **Visual C#**, click **Windows** and **Console Application**, and then click **OK**.</span></span>  <span data-ttu-id="b3541-199">Bu, yeni bir konsol uygulama projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b3541-199">This creates a new console application project.</span></span>
2. <span data-ttu-id="b3541-200">Merhaba gelen **Araçları** menüsünde tıklatın **kitaplık Paket Yöneticisi** ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="b3541-200">From hello **Tools** menu, click **Library Package Manager** and then **Package Manager Console**.</span></span> <span data-ttu-id="b3541-201">Merhaba Paket Yöneticisi Konsolu'nu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b3541-201">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="b3541-202">Merhaba konsol penceresinde hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="b3541-202">In hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. <span data-ttu-id="b3541-203">Açık `Program.cs` ve hello aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="b3541-203">Open `Program.cs` and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="b3541-204">Merhaba, `Program` sınıfı, yöntem aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b3541-204">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > <span data-ttu-id="b3541-205">Merhaba bağlantı dizesiyle kullandığınızdan emin olun **tam** erişimi ile değil, **dinleme** erişim.</span><span class="sxs-lookup"><span data-stu-id="b3541-205">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="b3541-206">Merhaba **dinleme** erişim bağlantı dizesi toosend anında iletme bildirimleri izinleri vermez.</span><span class="sxs-lookup"><span data-stu-id="b3541-206">hello **Listen** access connection string does not grant permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="b3541-207">Merhaba aşağıdaki çağırır hello eklemek `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b3541-207">Add hello following calls in hello `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="b3541-208">Chrome'un çalıştığından emin olun ve hello konsol uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b3541-208">Make sure that Chrome is running, and run hello console application.</span></span>
8. <span data-ttu-id="b3541-209">Merhaba aşağıdaki görmelisiniz bildirim masaüstünüzde açılır.</span><span class="sxs-lookup"><span data-stu-id="b3541-209">You should see hello following notification pop up on your desktop.</span></span>
   
       ![Google Chrome - Notification][13]
9. <span data-ttu-id="b3541-210">Hello Chrome Bildirimler penceresinde hello görev çubuğunda (Windows'ta) kullanarak da tüm bildirimlerinizi görebilirsiniz Chrome çalışırken.</span><span class="sxs-lookup"><span data-stu-id="b3541-210">You can also see all your notifications by using hello Chrome Notifications window in hello taskbar (in Windows) when Chrome is running.</span></span>
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> <span data-ttu-id="b3541-211">(Merhaba Chrome tarayıcısının çalışıyor olması gerekir rağmen) çalışan veya hello tarayıcıda aç toohave hello Chrome uygulaması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b3541-211">You don't need toohave hello Chrome App running or open in hello browser (though hello Chrome browser itself must be running).</span></span> <span data-ttu-id="b3541-212">Ayrıca tüm bildirimlerinizi birleştirilmiş bir görünüm hello Chrome Bildirimler penceresinde elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="b3541-212">You also get a consolidated view of all your notifications in hello Chrome Notifications window.</span></span>
> 
> 

## <span data-ttu-id="b3541-213"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3541-213"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="b3541-214">[Notification Hubs'a Genel Bakış]'ta Notification Hubs hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="b3541-214">Learn more about Notification Hubs in [Notification Hubs Overview].</span></span>

<span data-ttu-id="b3541-215">tootarget belirli kullanıcılar, başvuran toohello [Azure Notification Hubs kullanıcılara bildirme] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b3541-215">tootarget specific users, refer toohello [Azure Notification Hubs Notify Users] tutorial.</span></span> 

<span data-ttu-id="b3541-216">Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız hello izleyebilirsiniz [Azure Notification Hubs son dakika haberleri] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="b3541-216">If you want toosegment your users by interest groups, you can follow hello [Azure Notification Hubs breaking news] tutorial.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[Chrome uygulaması bildirim hub'ı örneği]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs'a Genel Bakış]: notification-hubs-push-notification-overview.md
[Chrome uygulamalarına genel bakış]: https://developer.chrome.com/apps/about_apps
[Chrome uygulaması GCM örneği]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[mobil cihazlarda Chrome uygulamaları]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Kayıt NH REST API’si oluşturma]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto-js Kitaplığı]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs kullanıcılara bildirme]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Azure Notification Hubs son dakika haberleri]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
