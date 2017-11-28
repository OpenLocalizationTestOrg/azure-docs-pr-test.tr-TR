---
title: "aaaAdd anında iletme bildirimleri tooApache Azure Mobile Apps ile Cordova uygulaması | Microsoft Docs"
description: "Nasıl toouse Azure Mobile Apps toosend anında bildirimler tooyour Apache Cordova uygulaması hakkında bilgi edinin."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a><span data-ttu-id="d41e8-103">Anında iletme bildirimleri tooyour Apache Cordova uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="d41e8-103">Add push notifications tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="d41e8-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d41e8-104">Overview</span></span>
<span data-ttu-id="d41e8-105">Bu öğreticide, böylece bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen anında iletme bildirimleri toohello [Apache Cordova Hızlı Başlangıç] projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-105">In this tutorial, you add push notifications toohello [Apache Cordova quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="d41e8-106">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello.</span><span class="sxs-lookup"><span data-stu-id="d41e8-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="d41e8-107">Daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][1].</span><span class="sxs-lookup"><span data-stu-id="d41e8-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

## <span data-ttu-id="d41e8-108"><a name="prerequisites"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d41e8-108"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="d41e8-109">Bu öğretici hello Google Android öykünücüsü, bir Android cihazında, bir Windows aygıtı ve bir iOS aygıtı üzerinde çalışan Visual Studio 2015 ile geliştirilen bir Apache Cordova uygulaması kapsar.</span><span class="sxs-lookup"><span data-stu-id="d41e8-109">This tutorial covers an Apache Cordova application developed with Visual Studio 2015 that runs on hello Google Android Emulator, an Android device, a Windows device, and an iOS device.</span></span>

<span data-ttu-id="d41e8-110">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="d41e8-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="d41e8-111">Bir bilgisayarla [Visual Studio Community 2015] [ 2] veya sonraki sürümler.</span><span class="sxs-lookup"><span data-stu-id="d41e8-111">A PC with [Visual Studio Community 2015][2] or later versions.</span></span>
* <span data-ttu-id="d41e8-112">[Apache Cordova için Visual Studio Araçları][4].</span><span class="sxs-lookup"><span data-stu-id="d41e8-112">[Visual Studio Tools for Apache Cordova][4].</span></span>
* <span data-ttu-id="d41e8-113">Bir [etkin Azure hesabı][3].</span><span class="sxs-lookup"><span data-stu-id="d41e8-113">An [active Azure account][3].</span></span>
* <span data-ttu-id="d41e8-114">Bir tamamlanmış [Apache Cordova Hızlı Başlangıç] [ 5] projesi.</span><span class="sxs-lookup"><span data-stu-id="d41e8-114">A completed [Apache Cordova quick start][5] project.</span></span>
* <span data-ttu-id="d41e8-115">(Android) A [Google hesabı] [ 6] doğrulanmış e-posta adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="d41e8-115">(Android) A [Google account][6] with a verified email address.</span></span>
* <span data-ttu-id="d41e8-116">(iOS) Bir [Apple Developer Program üyeliği] [ 7] ve bir iOS cihazı (iOS simülatörü itme desteklemez).</span><span class="sxs-lookup"><span data-stu-id="d41e8-116">(iOS) An [Apple Developer Program membership][7] and an iOS device (iOS Simulator does not support push).</span></span>
* <span data-ttu-id="d41e8-117">(Windows) A [Windows mağazası Geliştirici hesabınızla] [ 8] ve Windows 10 cihaz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-117">(Windows) A [Windows Store Developer Account][8] and a Windows 10 device.</span></span>

## <span data-ttu-id="d41e8-118"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-118"><a name="configure-hub"></a>Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

<span data-ttu-id="d41e8-119">[Bu bölümdeki adımları gösteren bir videoyu izleyin][9]</span><span class="sxs-lookup"><span data-stu-id="d41e8-119">[Watch a video showing steps in this section][9]</span></span>

## <a name="update-hello-server-project"></a><span data-ttu-id="d41e8-120">Güncelleştirme hello sunucu projesi</span><span class="sxs-lookup"><span data-stu-id="d41e8-120">Update hello server project</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="d41e8-121"><a name="add-push-to-app"></a>Cordova uygulamanızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="d41e8-121"><a name="add-push-to-app"></a>Modify your Cordova app</span></span>
<span data-ttu-id="d41e8-122">Apache Cordova uygulaması projenize hazır toohandle anında iletme bildirimleri yükleme hello Cordova itme eklentisi artı hiçbir platforma özgü anında hizmet tarafından olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d41e8-122">Ensure your Apache Cordova app project is ready toohandle push notifications by installing hello Cordova push plugin plus any platform-specific push services.</span></span>

#### <a name="update-hello-cordova-version-in-your-project"></a><span data-ttu-id="d41e8-123">Projenizdeki Hello Cordova sürümünü güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-123">Update hello Cordova version in your project.</span></span>
<span data-ttu-id="d41e8-124">Projenizi Apache Cordova v6.1.1'den önceki bir sürümünü kullanıyorsa, hello istemci projesi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-124">If your project uses a version of Apache Cordova earlier than v6.1.1, update hello client project.</span></span> <span data-ttu-id="d41e8-125">tooupdate hello proje:</span><span class="sxs-lookup"><span data-stu-id="d41e8-125">tooupdate hello project:</span></span>

* <span data-ttu-id="d41e8-126">Sağ `config.xml` tooopen hello yapılandırma Tasarımcısı.</span><span class="sxs-lookup"><span data-stu-id="d41e8-126">Right-click `config.xml` tooopen hello configuration designer.</span></span>
* <span data-ttu-id="d41e8-127">Merhaba platformları sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-127">Select hello Platforms tab.</span></span>
* <span data-ttu-id="d41e8-128">Hello 6.1.1 seçin **Cordova CLI** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="d41e8-128">Choose 6.1.1 in hello **Cordova CLI** text box.</span></span>
* <span data-ttu-id="d41e8-129">Seçin **yapı**, ardından **yapı çözümü** tooupdate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="d41e8-129">Choose **Build**, then **Build Solution** tooupdate hello project.</span></span>

#### <a name="install-hello-push-plugin"></a><span data-ttu-id="d41e8-130">Merhaba itme eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="d41e8-130">Install hello push plugin</span></span>
<span data-ttu-id="d41e8-131">Apache Cordova uygulamaları aygıt ya da ağ yetenekleri yerel işleyemez.</span><span class="sxs-lookup"><span data-stu-id="d41e8-131">Apache Cordova applications do not natively handle device or network capabilities.</span></span>  <span data-ttu-id="d41e8-132">Bu özellikler tarafından sağlanan olan eklentileri üzerinde ya da yayımlanan [npm] [ 10] veya github'da.</span><span class="sxs-lookup"><span data-stu-id="d41e8-132">These capabilities are provided by plugins that are published either on [npm][10] or on GitHub.</span></span>  <span data-ttu-id="d41e8-133">Merhaba `phonegap-plugin-push` eklentidir kullanılan toohandle ağ anında iletme bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="d41e8-133">hello `phonegap-plugin-push` plugin is used toohandle network push notifications.</span></span>

<span data-ttu-id="d41e8-134">Merhaba itme eklentisi şu yollardan biriyle yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d41e8-134">You can install hello push plugin in one of these ways:</span></span>

<span data-ttu-id="d41e8-135">**Merhaba-komut dosyasından:**</span><span class="sxs-lookup"><span data-stu-id="d41e8-135">**From hello command-prompt:**</span></span>

<span data-ttu-id="d41e8-136">Merhaba aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="d41e8-136">Execute hello following command:</span></span>

    cordova plugin add phonegap-plugin-push

<span data-ttu-id="d41e8-137">**Gelen Visual Studio içinde:**</span><span class="sxs-lookup"><span data-stu-id="d41e8-137">**From within Visual Studio:**</span></span>

1. <span data-ttu-id="d41e8-138">Çözüm Gezgini'nde hello açın `config.xml` dosyası **eklentileri** > **özel**seçin **Git** yükleme kaynağı olarak enter`https://github.com/phonegap/phonegap-plugin-push`hello kaynağı olarak.</span><span class="sxs-lookup"><span data-stu-id="d41e8-138">In Solution Explorer, open hello `config.xml` file click **Plugins** > **Custom**, select **Git** as the  installation source, then enter `https://github.com/phonegap/phonegap-plugin-push` as hello source.</span></span>

   ![][img1]

2. <span data-ttu-id="d41e8-139">Merhaba ok sonraki toohello yükleme kaynağı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-139">Click hello arrow next toohello installation source.</span></span>
3. <span data-ttu-id="d41e8-140">İçinde **SENDER_ID**, sayısal proje kimliği hello Google Developer konsol projesi için zaten varsa, bunu burada ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-140">In **SENDER_ID**, if you already have a numeric project ID for hello Google Developer Console project, you can add it here.</span></span> <span data-ttu-id="d41e8-141">Aksi takdirde, 777777 gibi bir yer tutucu değerini girin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-141">Otherwise, enter a placeholder value, like 777777.</span></span>  <span data-ttu-id="d41e8-142">Android hedefliyorsanız, bu değeri daha sonra config.xml güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-142">If you are targeting Android, you can update this value in config.xml later.</span></span>
4. <span data-ttu-id="d41e8-143">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-143">Click **Add**.</span></span>

<span data-ttu-id="d41e8-144">Merhaba itme eklentisi artık yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="d41e8-144">hello push plugin is now installed.</span></span>

#### <a name="install-hello-device-plugin"></a><span data-ttu-id="d41e8-145">Merhaba aygıt eklentisini yükleme</span><span class="sxs-lookup"><span data-stu-id="d41e8-145">Install hello device plugin</span></span>
<span data-ttu-id="d41e8-146">İzleme hello aynı yordamı tooinstall hello itme eklentisi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d41e8-146">Follow hello same procedure you used tooinstall hello push plugin.</span></span>  <span data-ttu-id="d41e8-147">Merhaba çekirdek eklentiler listesinden Hello aygıt eklenti ekleme (tıklatın **eklentileri** > **çekirdek** toofind onu).</span><span class="sxs-lookup"><span data-stu-id="d41e8-147">Add hello Device plugin from hello Core plugins list (click **Plugins** > **Core** toofind it).</span></span> <span data-ttu-id="d41e8-148">Bu eklenti tooobtain hello platform adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-148">You need this plugin tooobtain hello platform name.</span></span>

#### <a name="register-your-device-on-application-start-up"></a><span data-ttu-id="d41e8-149">Uygulama başlatma aygıtınızda kaydetme</span><span class="sxs-lookup"><span data-stu-id="d41e8-149">Register your device on application start-up</span></span>
<span data-ttu-id="d41e8-150">Başlangıçta, biz bazı çok az kod Android için içerir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-150">Initially, we include some minimal code for Android.</span></span> <span data-ttu-id="d41e8-151">Daha sonra iOS veya Windows 10 hello uygulama toorun değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-151">Later, modify hello app toorun on iOS or Windows 10.</span></span>

1. <span data-ttu-id="d41e8-152">Çağrı çok ekleyin**registerForPushNotifications** hello oturum açma işlemi için ya da hello hello sonundaki hello geri çağırma sırasında **onDeviceReady** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d41e8-152">Add a call too**registerForPushNotifications** during hello callback for hello login process, or at hello bottom of  hello **onDeviceReady** method:</span></span>

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    <span data-ttu-id="d41e8-153">Bu örnek, arama gösterir **registerForPushNotifications** kimlik doğrulaması başarılı olduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="d41e8-153">This example shows calling **registerForPushNotifications** after authentication succeeds.</span></span>  <span data-ttu-id="d41e8-154">Çağırabilirsiniz `registerForPushNotifications()` gereklidir sıklıkta.</span><span class="sxs-lookup"><span data-stu-id="d41e8-154">You can call `registerForPushNotifications()` as often as is required.</span></span>

2. <span data-ttu-id="d41e8-155">Merhaba yeni Ekle **registerForPushNotifications** yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="d41e8-155">Add hello new **registerForPushNotifications** method as follows:</span></span>

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. <span data-ttu-id="d41e8-156">(Android) Kod önceki hello yerine `Your_Project_ID` uygulamanızdan için kimliği ile Merhaba sayısal proje [Google Developer konsolunda][18].</span><span class="sxs-lookup"><span data-stu-id="d41e8-156">(Android) In hello preceding code, replace `Your_Project_ID` with hello numeric project ID for your app from the  [Google Developer Console][18].</span></span>

## <a name="optional-configure-and-run-hello-app-on-android"></a><span data-ttu-id="d41e8-157">(İsteğe bağlı) Yapılandırma ve hello uygulama Android'de çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-157">(Optional) Configure and run hello app on Android</span></span>
<span data-ttu-id="d41e8-158">Bu bölümde tooenable anında iletme bildirimleri Android tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-158">Complete this section tooenable push notifications for Android.</span></span>

#### <span data-ttu-id="d41e8-159"><a name="enable-gcm"></a>Firebase etkinleştirmek bulut Mesajlaşma</span><span class="sxs-lookup"><span data-stu-id="d41e8-159"><a name="enable-gcm"></a>Enable Firebase Cloud Messaging</span></span>
<span data-ttu-id="d41e8-160">Google Android platformu hello başlangıçta hedefleme bu yana Firebase Cloud Messaging etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-160">Since we are targeting hello Google Android platform initially, you must enable Firebase Cloud Messaging.</span></span>

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <span data-ttu-id="d41e8-161"><a name="configure-backend"></a>Merhaba mobil uygulama arka uç toosend gönderme istekleri FCM kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-161"><a name="configure-backend"></a>Configure hello Mobile App backend toosend push requests using FCM</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a><span data-ttu-id="d41e8-162">Android için Cordova uygulamanızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-162">Configure your Cordova app for Android</span></span>
<span data-ttu-id="d41e8-163">Cordova uygulamanızı config.xml açın ve değiştirmek `Your_Project_ID` hello uygulamanızdan için kimliği ile Merhaba sayısal proje [Google Developer konsolunda][18].</span><span class="sxs-lookup"><span data-stu-id="d41e8-163">In your Cordova app, open config.xml and replace `Your_Project_ID` with hello numeric project ID for your app from hello [Google Developer Console][18].</span></span>

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

<span data-ttu-id="d41e8-164">İndex.js açın ve sayısal proje kimliğinizi hello kod toouse güncelleştir</span><span class="sxs-lookup"><span data-stu-id="d41e8-164">Open index.js and update hello code toouse your numeric project ID.</span></span>

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <span data-ttu-id="d41e8-165"><a name="configure-device"></a>USB hata ayıklama için Android Cihazınızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d41e8-165"><a name="configure-device"></a>Configure your Android device for USB debugging</span></span>
<span data-ttu-id="d41e8-166">Uygulama tooyour Android cihazı dağıtmadan önce tooenable USB hata ayıklama gerekir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-166">Before you can deploy your application tooyour Android Device, you need tooenable USB Debugging.</span></span>  <span data-ttu-id="d41e8-167">Android telefonunuzda aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d41e8-167">Perform the following steps on your Android phone:</span></span>

1. <span data-ttu-id="d41e8-168">Çok Git**ayarları** > **telefon hakkında**, hello dokunun **yapı numarası** geliştirici modunu (yaklaşık yedi defa) etkinleştirilene kadar.</span><span class="sxs-lookup"><span data-stu-id="d41e8-168">Go too**Settings** > **About phone**, then tap hello **Build number** until developer mode is enabled  (about seven times).</span></span>
2. <span data-ttu-id="d41e8-169">Geri **ayarları** > **Geliştirici seçenekleri** etkinleştirmek **USB hata ayıklama**, ardından Android telefonunuzu tooyour geliştirme bilgisayarınıza bir USB kablosu ile bağlanın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-169">Back in **Settings** > **Developer Options** enable **USB debugging**, then connect your Android phone  tooyour development PC with a USB Cable.</span></span>

<span data-ttu-id="d41e8-170">Bu Android 6.0 (Marshmallow) çalıştıran bir Google Nexus 5 X aygıtı kullanarak test.</span><span class="sxs-lookup"><span data-stu-id="d41e8-170">We tested this using a Google Nexus 5X device running Android 6.0 (Marshmallow).</span></span>  <span data-ttu-id="d41e8-171">Ancak, tüm modern Android sürüm arasında hello teknikleri yaygındır.</span><span class="sxs-lookup"><span data-stu-id="d41e8-171">However, hello techniques are common across any modern Android release.</span></span>

#### <a name="install-google-play-services"></a><span data-ttu-id="d41e8-172">Google Play hizmetlerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="d41e8-172">Install Google Play Services</span></span>
<span data-ttu-id="d41e8-173">Merhaba itme eklentisi Android Google Play Hizmetleri'nin anında iletme bildirimleri için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d41e8-173">hello push plugin relies on Android Google Play Services for push notifications.</span></span>

1. <span data-ttu-id="d41e8-174">Visual Studio'da sırasıyla **Araçları** > **Android** > **Android SDK Manager**, hello genişletin **ek özellikler** klasör ve onay hello kutusunu toomake her SDK'ları aşağıdaki hello yüklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d41e8-174">In Visual Studio, click **Tools** > **Android** > **Android SDK Manager**, expand hello **Extras** folder and  check hello box toomake sure that each of hello following SDKs is installed.</span></span>

   * <span data-ttu-id="d41e8-175">Android 2.3 veya daha yüksek</span><span class="sxs-lookup"><span data-stu-id="d41e8-175">Android 2.3 or higher</span></span>
   * <span data-ttu-id="d41e8-176">Google depo düzeltme 27 veya daha yüksek</span><span class="sxs-lookup"><span data-stu-id="d41e8-176">Google Repository revision 27 or higher</span></span>
   * <span data-ttu-id="d41e8-177">Google Play hizmetlerini 9.0.2 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="d41e8-177">Google Play Services 9.0.2 or higher</span></span>

2. <span data-ttu-id="d41e8-178">Tıklatın **yükleme paketleri** ve hello yükleme toocomplete için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-178">Click **Install Packages** and wait for hello installation toocomplete.</span></span>

<span data-ttu-id="d41e8-179">Merhaba geçerli kitaplıkları hello listelenen gerekli [phonegap eklentiyi itme yükleme belgelerini][19].</span><span class="sxs-lookup"><span data-stu-id="d41e8-179">hello current required libraries are listed in hello [phonegap-plugin-push installation documentation][19].</span></span>

#### <a name="test-push-notifications-in-hello-app-on-android"></a><span data-ttu-id="d41e8-180">Merhaba uygulamasında android'de test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d41e8-180">Test push notifications in hello app on Android</span></span>
<span data-ttu-id="d41e8-181">Uygulama ve hello Todoıtem tablosu ekleme öğelerde çalıştırarak test anında iletme bildirimleri hello artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-181">You can now test push notifications by running hello app and inserting items in hello TodoItem table.</span></span> <span data-ttu-id="d41e8-182">Test edebilirsiniz hello aynı cihaz veya kullanmakta olduğunuz sürece ikinci bir aygıttan aynı hello arka uç.</span><span class="sxs-lookup"><span data-stu-id="d41e8-182">You can test from hello same device or from a second device, as long as you are using hello same backend.</span></span> <span data-ttu-id="d41e8-183">Cordova uygulamanızı hello Android platformunda yolları aşağıdaki hello birinde test edin:</span><span class="sxs-lookup"><span data-stu-id="d41e8-183">Test your Cordova app on hello Android platform in one of hello following ways:</span></span>

* <span data-ttu-id="d41e8-184">**Bir fiziksel cihaz üzerindeki:** Android cihaz tooyour geliştirme bilgisayarınıza bir USB kablosu ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-184">**On a physical device:** Attach your Android device tooyour development computer with a USB cable.</span></span>  <span data-ttu-id="d41e8-185">Yerine **Google Android öykünücüsü**seçin **aygıt**.</span><span class="sxs-lookup"><span data-stu-id="d41e8-185">Instead of **Google Android Emulator**, select **Device**.</span></span> <span data-ttu-id="d41e8-186">Visual Studio hello uygulama toohello aygıt dağıtır ve ardından Merhaba uygulaması çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d41e8-186">Visual Studio deploys hello application toohello device and then runs hello application.</span></span>  <span data-ttu-id="d41e8-187">Hello aygıtta hello uygulama ile etkileşim kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-187">You can then interact with hello application on hello device.</span></span>

  <span data-ttu-id="d41e8-188">Geliştirme deneyiminizi iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-188">Improve your development experience.</span></span>  <span data-ttu-id="d41e8-189">Ekran uygulamaları gibi paylaşımı [Mobizen] [ 20] Android uygulama geliştirmede yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-189">Screen sharing applications such as [Mobizen][20] can assist you in developing an Android application.</span></span>  <span data-ttu-id="d41e8-190">Mobizen Android ekran tooa web tarayıcınızı bilgisayarınıza projeleri.</span><span class="sxs-lookup"><span data-stu-id="d41e8-190">Mobizen projects your Android screen tooa web browser on your PC.</span></span>

* <span data-ttu-id="d41e8-191">**Android öykünücüsünde üzerinde:** bir öykünücü üzerinde çalışırken gereken ek yapılandırma adımları vardır.</span><span class="sxs-lookup"><span data-stu-id="d41e8-191">**On an Android emulator:** There are additional configuration steps required when running on an emulator.</span></span>

    <span data-ttu-id="d41e8-192">Google API'leri hello hedef olarak ayarlanmış hello Android sanal cihazı (AVD) Yöneticisi'nde gösterildiği gibi tooa sanal cihaza dağıttığınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="d41e8-192">Make sure you are deploying tooa virtual device that has Google APIs set as hello target, as shown in hello Android Virtual Device (AVD) manager.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    <span data-ttu-id="d41e8-193">Daha hızlı x86 toouse istiyorsanız öykünücüsü, [hello HAXM sürücüyü yüklemek] [ 11] ve hello öykünücüsü toouse yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="d41e8-193">If you want toouse a faster x86 emulator, you [install hello HAXM driver][11] and configure hello emulator toouse it.</span></span>

    <span data-ttu-id="d41e8-194">Bir Google hesabı toohello Android cihazı tıklayarak ekleyin **uygulamaları** > **ayarları** > **hesabı eklemek**, hello istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-194">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    <span data-ttu-id="d41e8-195">Önce Hello Yapılacaklar listesi uygulaması gibi çalıştırabilir ve yeni bir Yapılacaklar öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-195">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="d41e8-196">Bu süre, hello bildirim alanında bir bildirim simgesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-196">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="d41e8-197">Merhaba bildirim çekmecesini tooview hello tam metin hello bildirim açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-197">You can open hello notification drawer tooview hello full text of hello notification.</span></span>

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a><span data-ttu-id="d41e8-198">(İsteğe bağlı) Yapılandırma ve İos'ta çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-198">(Optional) Configure and run on iOS</span></span>
<span data-ttu-id="d41e8-199">Bu bölümde, iOS cihazlarda hello Cordova projesi çalıştırmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-199">This section is for running hello Cordova project on iOS devices.</span></span> <span data-ttu-id="d41e8-200">İOS cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-200">If you are not working with iOS devices, you can skip this section.</span></span>

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a><span data-ttu-id="d41e8-201">Yükleme ve çalıştırma hello iOS uzak aracı bir Mac veya Bulut hizmetinde derleme</span><span class="sxs-lookup"><span data-stu-id="d41e8-201">Install and run hello iOS remote build agent on a Mac or cloud service</span></span>
<span data-ttu-id="d41e8-202">Visual Studio kullanarak iOS Cordova uygulaması çalıştırmadan önce hello hello içinde adımlarını [iOS kurulum kılavuzunu] [ 12] tooinstall ve uzak çalışma hello derleme aracısı.</span><span class="sxs-lookup"><span data-stu-id="d41e8-202">Before you can run a Cordova app on iOS using Visual Studio, go through hello steps in hello [iOS Setup Guide][12] tooinstall and run hello remote build agent.</span></span>

<span data-ttu-id="d41e8-203">İOS için başlangıç uygulaması oluşturduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d41e8-203">Make sure you can build hello app for iOS.</span></span> <span data-ttu-id="d41e8-204">Merhaba hello Kurulum Kılavuzu'nda Visual Studio'dan iOS için gerekli toobuild adımlardır.</span><span class="sxs-lookup"><span data-stu-id="d41e8-204">hello steps in hello setup guide are required toobuild for iOS from Visual Studio.</span></span> <span data-ttu-id="d41e8-205">Mac yoksa hello uzak derleme aracısı MacInCloud gibi bir hizmet kullanarak iOS için oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-205">If you do not have a Mac, you can build for iOS using hello remote build agent on a service like MacInCloud.</span></span> <span data-ttu-id="d41e8-206">Daha fazla bilgi için bkz: [hello bulutta iOS uygulamanızı çalıştırma][21].</span><span class="sxs-lookup"><span data-stu-id="d41e8-206">For more info, see [Run your iOS app in hello cloud][21].</span></span>

> [!NOTE]
> <span data-ttu-id="d41e8-207">XCode 7 veya daha fazla gerekli toouse hello itme iOS eklentidir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-207">XCode 7 or greater is required toouse hello push plugin on iOS.</span></span>

#### <a name="find-hello-id-toouse-as-your-app-id"></a><span data-ttu-id="d41e8-208">Merhaba kimliği toouse uygulama Kimliğiniz Bul</span><span class="sxs-lookup"><span data-stu-id="d41e8-208">Find hello ID toouse as your App ID</span></span>
<span data-ttu-id="d41e8-209">Anında iletme bildirimleri için uygulamanızı kaydetme önce config.xml Cordova uygulamanızı açın, hello Bul `id` öznitelik değeri hello pencere öğesinde ve daha sonra kullanmak üzere kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-209">Before you register your app for push notifications, open config.xml in your Cordova app, find hello `id` attribute value in hello widget element, and copy it for later use.</span></span> <span data-ttu-id="d41e8-210">XML aşağıdaki hello hello kimliğidir `io.cordova.myapp7777777`.</span><span class="sxs-lookup"><span data-stu-id="d41e8-210">In hello following XML, hello ID is `io.cordova.myapp7777777`.</span></span>

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

<span data-ttu-id="d41e8-211">Apple Geliştirici Portalı üzerinde bir uygulama kimliği oluşturduğunuzda, daha sonra bu tanımlayıcı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-211">Later, use this identifier when you create an App ID on Apple's developer portal.</span></span> <span data-ttu-id="d41e8-212">Farklı bir uygulama kimliği hello Geliştirici portalında oluşturursanız, daha sonra Bu öğreticide birkaç ek adımlar atmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-212">If you create a different App ID on hello developer portal, you must take a few extra steps later in this tutorial.</span></span> <span data-ttu-id="d41e8-213">Pencere öğesinde Hello kimliği hello uygulama kimliği hello Geliştirici portalındaki eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-213">hello ID in the widget element must match hello App ID on hello developer portal.</span></span>

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="d41e8-214">Apple Geliştirici portalındaki anında iletme bildirimleri için Hello uygulamasını Kaydet</span><span class="sxs-lookup"><span data-stu-id="d41e8-214">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[<span data-ttu-id="d41e8-215">Benzer adımları gösteren bir video izleyin</span><span class="sxs-lookup"><span data-stu-id="d41e8-215">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="d41e8-216">Azure toosend anında iletme bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-216">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a><span data-ttu-id="d41e8-217">Uygulama Kimliğiniz Cordova uygulamanızı eşleştiğini doğrulayın</span><span class="sxs-lookup"><span data-stu-id="d41e8-217">Verify that your App ID matches your Cordova app</span></span>
<span data-ttu-id="d41e8-218">Merhaba Apple Geliştirici hesabınızda zaten oluşturulmuş uygulama kimliği config.xml hello pencere öğesinde hello Kimliğini eşleşiyorsa, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-218">If hello App ID you created in your Apple Developer Account already matches hello ID of hello widget element in config.xml, you can skip this step.</span></span> <span data-ttu-id="d41e8-219">Ancak, Hello kimlikler eşleşmezse, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="d41e8-219">However, if hello IDs don't match, take hello following steps:</span></span>

1. <span data-ttu-id="d41e8-220">Merhaba platformları klasörü projenizden silin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-220">Delete hello platforms folder from your project.</span></span>
2. <span data-ttu-id="d41e8-221">Merhaba eklentileri klasörü projenizden silin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-221">Delete hello plugins folder from your project.</span></span>
3. <span data-ttu-id="d41e8-222">Merhaba node_modules klasörü projenizden silin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-222">Delete hello node_modules folder from your project.</span></span>
4. <span data-ttu-id="d41e8-223">Güncelleştirme hello ID özniteliği hello pencere öğesinde config.xml toouse hello Apple Geliştirici hesabınızda oluşturduğunuz uygulama kimliği.</span><span class="sxs-lookup"><span data-stu-id="d41e8-223">Update hello id attribute of hello widget element in config.xml toouse hello App ID that you created in your  Apple Developer Account.</span></span>
5. <span data-ttu-id="d41e8-224">Projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-224">Rebuild your project.</span></span>

##### <a name="test-push-notifications-in-your-ios-app"></a><span data-ttu-id="d41e8-225">İOS uygulamanızı test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d41e8-225">Test push notifications in your iOS app</span></span>
1. <span data-ttu-id="d41e8-226">Visual Studio'da olduğundan emin olun **iOS** hello dağıtım hedefi olarak seçilir ve ardından **aygıt** toorun bağlı iOS Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="d41e8-226">In Visual Studio, make sure that **iOS** is selected as hello deployment target, and then choose **Device** toorun on your connected iOS device.</span></span>

    <span data-ttu-id="d41e8-227">Bir iOS aygıtı bağlı tooyour PC çalıştırabilirsiniz iTunes kullanma.</span><span class="sxs-lookup"><span data-stu-id="d41e8-227">You can run on an iOS device connected tooyour PC using iTunes.</span></span> <span data-ttu-id="d41e8-228">Merhaba iOS simülatörü anında iletme bildirimlerini desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="d41e8-228">hello iOS Simulator does not support push notifications.</span></span>

2. <span data-ttu-id="d41e8-229">Tuşuna hello **çalıştırmak** düğmesini veya **F5** Visual Studio toobuild hello proje ve başlangıç hello bir iOS aygıtı uygulamada ve ardından tıklayın **Tamam** tooaccept anında iletme bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="d41e8-229">Press hello **Run** button or **F5** in Visual Studio toobuild hello project and start hello app in an iOS  device, then click **OK** tooaccept push notifications.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d41e8-230">Merhaba uygulaması ilk çalıştırma hello sırasında anında iletme bildirimleri için onay ister.</span><span class="sxs-lookup"><span data-stu-id="d41e8-230">hello app requests confirmation for push notifications during hello first run.</span></span>

3. <span data-ttu-id="d41e8-231">Merhaba uygulamada, bir görev yazın ve hello artı (+) ardından simge.</span><span class="sxs-lookup"><span data-stu-id="d41e8-231">In hello app, type a task, and then click hello plus (+) icon.</span></span>
4. <span data-ttu-id="d41e8-232">Bir bildirim alındı ve ardından Tamam toodismiss hello bildirim doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-232">Verify that a notification is received, then click OK toodismiss hello notification.</span></span>

## <a name="optional-configure-and-run-on-windows"></a><span data-ttu-id="d41e8-233">(İsteğe bağlı) Yapılandırma ve Windows'ta çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-233">(Optional) Configure and run on Windows</span></span>
<span data-ttu-id="d41e8-234">Bu bölümde, Windows 10 cihazlarda (Merhaba PhoneGap itme eklentisi üzerinde Windows 10 desteklenir) hello Apache Cordova uygulaması projesi çalıştırmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="d41e8-234">This section is for running hello Apache Cordova app project on Windows 10 devices (hello PhoneGap push plugin is supported on Windows 10).</span></span> <span data-ttu-id="d41e8-235">Windows cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-235">If you are not working with Windows devices, you can skip this section.</span></span>

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a><span data-ttu-id="d41e8-236">Windows uygulamanızı anında iletme bildirimleri için WNS ile kaydetme</span><span class="sxs-lookup"><span data-stu-id="d41e8-236">Register your Windows app for push notifications with WNS</span></span>
<span data-ttu-id="d41e8-237">Visual Studio'da toouse hello depolama seçenekleri Windows hedef gibi hello çözüm platformları listeden seçin **Windows x64** veya **Windows x86** (kaçının **Windows AnyCPU** için anında iletme bildirimleri).</span><span class="sxs-lookup"><span data-stu-id="d41e8-237">toouse hello Store options in Visual Studio, select a Windows target from hello Solution Platforms list, like **Windows-x64** or **Windows-x86** (avoid **Windows-AnyCPU** for push notifications).</span></span>

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

<span data-ttu-id="d41e8-238">[Benzer adımları gösteren bir videoyu izleyin][13]</span><span class="sxs-lookup"><span data-stu-id="d41e8-238">[Watch a video showing similar steps][13]</span></span>

#### <a name="configure-hello-notification-hub-for-wns"></a><span data-ttu-id="d41e8-239">WNS için Hello bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-239">Configure hello notification hub for WNS</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a><span data-ttu-id="d41e8-240">Cordova uygulaması toosupport Windows anında iletme bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d41e8-240">Configure your Cordova app toosupport Windows push notifications</span></span>
<span data-ttu-id="d41e8-241">Açık hello yapılandırma Tasarımcısı (sağ tıklatın ve config.xml **Görünüm Tasarımcısı**), select hello **Windows** sekmesini tıklatın ve seçin **Windows 10** altında**Windows hedef sürüm**.</span><span class="sxs-lookup"><span data-stu-id="d41e8-241">Open hello configuration designer (right-click on config.xml and select **View Designer**), select hello **Windows** tab, and choose **Windows 10** under **Windows Target Version**.</span></span>

<span data-ttu-id="d41e8-242">Açık build.json dosya toosupport anında iletme bildirimleri için varsayılan (hata ayıklama) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d41e8-242">toosupport push notifications in your default (debug) builds, open build.json file.</span></span> <span data-ttu-id="d41e8-243">"Yayın" yapılandırma tooyour hata ayıklama yapılandırması kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-243">Copy the "release" configuration tooyour debug configuration.</span></span>

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="d41e8-244">Merhaba güncelleştirmeden sonra hello build.json koddan hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="d41e8-244">After hello update, hello build.json should contain hello following code:</span></span>

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

<span data-ttu-id="d41e8-245">Merhaba uygulaması oluşturma ve hiçbir hata sahip olduğunuzu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-245">Build hello app and verify that you have no errors.</span></span> <span data-ttu-id="d41e8-246">İstemci uygulamanızı hello mobil uygulama arka ucu hello bildirimleri için şimdi kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="d41e8-246">Your client app should now register for hello notifications from hello Mobile App backend.</span></span> <span data-ttu-id="d41e8-247">Bu bölümde, çözümünüz içinde her Windows projesi için tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-247">Repeat this section for every Windows project in your solution.</span></span>

#### <a name="test-push-notifications-in-your-windows-app"></a><span data-ttu-id="d41e8-248">Windows uygulamanızı test anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d41e8-248">Test push notifications in your Windows app</span></span>
<span data-ttu-id="d41e8-249">Visual Studio'da Windows platformu aşağıdaki gibi hello dağıtım hedefi olarak seçildiğinden emin olun **Windows x64** veya **Windows x86**.</span><span class="sxs-lookup"><span data-stu-id="d41e8-249">In Visual Studio, make sure that a Windows platform is selected as hello deployment target, such as **Windows-x64** or **Windows-x86**.</span></span> <span data-ttu-id="d41e8-250">Visual Studio, barındırma Windows 10 PC'de toorun hello uygulamayı seçin **yerel makine**.</span><span class="sxs-lookup"><span data-stu-id="d41e8-250">toorun hello app on a Windows 10 PC hosting Visual Studio, choose **Local Machine**.</span></span>

<span data-ttu-id="d41e8-251">Tuşuna hello düğmesi toobuild Merhaba projeyi çalıştırın ve hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-251">Press hello Run button toobuild hello project and start hello app.</span></span>

<span data-ttu-id="d41e8-252">Merhaba uygulamasında yeni bir todoıtem için bir ad yazın ve hello artı (+) ardından simge tooadd onu.</span><span class="sxs-lookup"><span data-stu-id="d41e8-252">In hello app, type a name for a new todoitem, and then click hello plus (+) icon tooadd it.</span></span>

<span data-ttu-id="d41e8-253">Merhaba öğesi eklendiğinde, bir bildirim alındığında doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d41e8-253">Verify that a notification is received when hello item is added.</span></span>

## <span data-ttu-id="d41e8-254"><a name="next-steps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d41e8-254"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="d41e8-255">Hakkında bilgi edinin [bildirim hub'ları] [ 17] toolearn anında iletme bildirimleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="d41e8-255">Read about [Notification Hubs][17] toolearn about push notifications.</span></span>
* <span data-ttu-id="d41e8-256">Zaten yapmadıysanız, hello Öğreticisi tarafından devam [Authentication ekleme] [ 14] tooyour Apache Cordova uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d41e8-256">If you have not already done so, continue hello tutorial by [Adding Authentication][14] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="d41e8-257">Nasıl toouse hello SDK'ları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d41e8-257">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="d41e8-258">[Apache Cordova SDK'sı][15]</span><span class="sxs-lookup"><span data-stu-id="d41e8-258">[Apache Cordova SDK][15]</span></span>
* <span data-ttu-id="d41e8-259">[ASP.NET sunucusu SDK][1]</span><span class="sxs-lookup"><span data-stu-id="d41e8-259">[ASP.NET Server SDK][1]</span></span>
* <span data-ttu-id="d41e8-260">[Node.js sunucusu SDK][16]</span><span class="sxs-lookup"><span data-stu-id="d41e8-260">[Node.js Server SDK][16]</span></span>

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
