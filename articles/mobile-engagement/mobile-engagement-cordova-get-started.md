---
title: "aaaGet Cordova/Phonegap için Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl toouse analizler ve anında iletme bildirimleri ile Azure Mobile Engagement Cordova/Phonegap uygulamaları için."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a><span data-ttu-id="ca44c-103">Cordova/Phonegap için Azure Mobile Engagement Kullanmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="ca44c-103">Get Started with Azure Mobile Engagement for Cordova/Phonegap</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="ca44c-104">Bu konu, nasıl gösterir, uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılarınızın bir mobil uygulama için Cordova ile geliştirilen toouse Azure Mobile Engagement toounderstand.</span><span class="sxs-lookup"><span data-stu-id="ca44c-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users for a mobile application developed with Cordova.</span></span>

<span data-ttu-id="ca44c-105">Bu öğreticide, Mac kullanarak boş bir Cordova uygulaması oluşturup Mobile Engagement SDK ile tümleştireceğiz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-105">In this tutorial, we will create a blank Cordova app using Mac and then integrate Mobile Engagement SDK.</span></span> <span data-ttu-id="ca44c-106">Uygulama, temel analiz verileri toplar, iOS için Apple Anında İletilen Bildirim Sistemi (APNS) ve Android için Google Cloud Messaging (GCM) kullanarak anında iletme bildirimlerini alır.</span><span class="sxs-lookup"><span data-stu-id="ca44c-106">It collects basic analytics data and receives push notifications using Apple Push Notification System (APNS) for iOS and Google Cloud Messaging (GCM) for Android.</span></span> <span data-ttu-id="ca44c-107">Bu tooan iOS veya Android cihazında Test dağıtımını yapacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ca44c-107">We will deploy this tooan iOS or Android device for testing.</span></span> 

> [!NOTE]
> <span data-ttu-id="ca44c-108">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca44c-108">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ca44c-109">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-109">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ca44c-110">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span><span class="sxs-lookup"><span data-stu-id="ca44c-110">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).</span></span>
> 
> 

<span data-ttu-id="ca44c-111">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="ca44c-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="ca44c-112">Mac uygulama Mağazası'ndan (tooiOS dağıtmak için) yükleyebileceğiniz XCode</span><span class="sxs-lookup"><span data-stu-id="ca44c-112">XCode, which you can install from Mac App Store (for deploying tooiOS)</span></span>
* <span data-ttu-id="ca44c-113">[Android SDK ve öykünücüsü](http://developer.android.com/sdk/installing/index.html) (dağıtmayla tooAndroid)</span><span class="sxs-lookup"><span data-stu-id="ca44c-113">[Android SDK & Emulator](http://developer.android.com/sdk/installing/index.html) (for deploying tooAndroid)</span></span>
* <span data-ttu-id="ca44c-114">APNS için Apple Dev Center'dan edinebileceğiniz anında iletme bildirimi sertifikası (.p12)</span><span class="sxs-lookup"><span data-stu-id="ca44c-114">Push notification certificate (.p12) that you can obtain from Apple Dev Center for APNS</span></span>
* <span data-ttu-id="ca44c-115">GCM için Google Developer Console’unuzdan edinebileceğiniz GCM Proje numarası</span><span class="sxs-lookup"><span data-stu-id="ca44c-115">GCM Project number that you can obtain from your Google Developer Console for GCM</span></span>
* [<span data-ttu-id="ca44c-116">Mobile Engagement Cordova eklentisi</span><span class="sxs-lookup"><span data-stu-id="ca44c-116">Mobile Engagement Cordova Plugin</span></span>](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> <span data-ttu-id="ca44c-117">Merhaba kaynak kodu bulun ve üzerinde hello Cordova eklentisi için Benioku hello [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span><span class="sxs-lookup"><span data-stu-id="ca44c-117">You can find hello source code and hello ReadMe for hello Cordova plugin on [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)</span></span>
> 
> 

## <span data-ttu-id="ca44c-118"><a id="setup-azme"></a>Cordova uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="ca44c-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Cordova app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="ca44c-119"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="ca44c-119"><a id="connecting-app"></a>Connecting your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="ca44c-120">Bu öğreticide hello en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir "temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ca44c-120">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="ca44c-121">Cordova toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="ca44c-121">We will create a basic app with Cordova toodemonstrate hello integration:</span></span>

### <a name="create-a-new-cordova-project"></a><span data-ttu-id="ca44c-122">Yeni bir Cordova projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca44c-122">Create a new Cordova project</span></span>
1. <span data-ttu-id="ca44c-123">Başlatma *Terminal* hangi hello varsayılan şablondan yeni bir Cordova projesi oluşturacak aşağıdaki, Mac makine ve türü hello penceresinde.</span><span class="sxs-lookup"><span data-stu-id="ca44c-123">Launch *Terminal* window on your Mac machine and type hello following which will create a new Cordova project from hello default template.</span></span> <span data-ttu-id="ca44c-124">Hello yayımlama, sonunda kullanım toodeploy profil olduğundan emin olun, iOS uygulamanızın uygulama kimliği hello olarak 'com.mycompany.myapp' kullanıyor</span><span class="sxs-lookup"><span data-stu-id="ca44c-124">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using 'com.mycompany.myapp' as hello App ID.</span></span> 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. <span data-ttu-id="ca44c-125">Projeniz için tooconfigure aşağıdaki hello yürütme **iOS** ve hello iOS simülatörü çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ca44c-125">Execute hello following tooconfigure your project for **iOS** and run it in hello iOS Simulator:</span></span>
   
        $ cordova platform add ios 
        $ cordova run ios
3. <span data-ttu-id="ca44c-126">Projeniz için tooconfigure aşağıdaki hello yürütme **Android** ve hello Android öykünücüsünde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca44c-126">Execute hello following tooconfigure your project for **Android** and run it in hello Android emulator.</span></span> <span data-ttu-id="ca44c-127">Android SDK öykünücüsü ayarlarınızı hedef olarak Google API'leri (Google Inc.) ile Merhaba CPU olduğundan emin olun / ABI olarak Google API'ler ARM'si.</span><span class="sxs-lookup"><span data-stu-id="ca44c-127">Make sure that your Android SDK Emulator settings have its Target as Google APIs (Google Inc.) with hello CPU / ABI as Google APIs ARM.</span></span>  
   
        $ cordova platform add android
        $ cordova run android
4. <span data-ttu-id="ca44c-128">Merhaba Cordova Konsolu eklentisini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca44c-128">Add hello Cordova Console plugin.</span></span> 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="ca44c-129">Uygulamanızın tooMobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="ca44c-129">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="ca44c-130">Merhaba değişken değerleri tooconfigure hello eklentisi sağlarken Hello Azure Mobile Engagement Cordova eklentisini yükleyin:</span><span class="sxs-lookup"><span data-stu-id="ca44c-130">Install hello Azure Mobile Engagement Cordova plugin while providing hello variable values tooconfigure hello plugin:</span></span>
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

<span data-ttu-id="ca44c-131">*Android Reach simgesi* : hello kaynağı herhangi bir uzantı veya drawable ön eki olmadan hello adı olması gerekir (örn: mynotificationicon), ve android projenize (platformları/android/res/drawable) hello simge dosyası kopyalanır</span><span class="sxs-lookup"><span data-stu-id="ca44c-131">*Android Reach Icon* : must be hello name of hello resource without any extension, nor drawable prefix (ex: mynotificationicon), and hello icon file must be copied into your android project (platforms/android/res/drawable)</span></span>

<span data-ttu-id="ca44c-132">*iOS Reach simgesi* : hello kaynak uzantısı hello adı olması gerekir (örn: mynotificationicon.png), ve hello simge dosyası eklenir (Merhaba Ekle dosyaları menüsünü kullanarak) XCode ile iOS projenize gerekir</span><span class="sxs-lookup"><span data-stu-id="ca44c-132">*iOS Reach Icon*  : must be hello name of hello resource with its extension (ex:  mynotificationicon.png), and hello icon file must be added into your iOS project with XCode (using hello Add Files Menu)</span></span>

## <span data-ttu-id="ca44c-133"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ca44c-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
1. <span data-ttu-id="ca44c-134">Merhaba Cordova projesinde **www/js/index.js** tooMobile katılım toodeclare yeni bir etkinlik bir kez hello tooadd hello çağrısı *deviceReady* olayı alındığında.</span><span class="sxs-lookup"><span data-stu-id="ca44c-134">In hello Cordova project - edit **www/js/index.js** tooadd hello call tooMobile Engagement toodeclare a new activity once hello *deviceReady* event is received.</span></span>
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. <span data-ttu-id="ca44c-135">Merhaba uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ca44c-135">Run hello application:</span></span>
   
   * <span data-ttu-id="ca44c-136">**iOS için**</span><span class="sxs-lookup"><span data-stu-id="ca44c-136">**For iOS**</span></span>
     
       <span data-ttu-id="ca44c-137">İçinde `Terminal` penceresinde hello aşağıdakini yürüterek uygulamanızı yeni bir Simulator örneğinde başlatın:</span><span class="sxs-lookup"><span data-stu-id="ca44c-137">In `Terminal` window launch your app in a new Simulator instance by executing hello following:</span></span>
     
           cordova run ios
   * <span data-ttu-id="ca44c-138">**Android için**</span><span class="sxs-lookup"><span data-stu-id="ca44c-138">**For Android**</span></span>
     
       <span data-ttu-id="ca44c-139">İçinde `Terminal` penceresinde hello aşağıdakini yürüterek uygulamanızı yeni bir öykünücü örneğinde başlatın:</span><span class="sxs-lookup"><span data-stu-id="ca44c-139">In `Terminal` window launch your app in a new emulator instance by executing hello following:</span></span>
     
           cordova run android
3. <span data-ttu-id="ca44c-140">Merhaba konsol günlüklerine hello aşağıdakileri görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca44c-140">You can see hello following in hello console logs:</span></span>
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <span data-ttu-id="ca44c-141"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="ca44c-141"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="ca44c-142"><a id="integrate-push"></a>Anında İletme Bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ca44c-142"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="ca44c-143">Mobile Engagement anında iletme bildirimleri ve uygulama içi hello Kampanyalar bağlamında Mesajlaşma aracılığıyla kullanıcılarınız ile toointeract sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca44c-143">Mobile Engagement allows you toointeract with your users using Push Notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="ca44c-144">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="ca44c-144">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="ca44c-145">Merhaba aşağıdaki bölümlerde, app tooreceive Kurulum bunları.</span><span class="sxs-lookup"><span data-stu-id="ca44c-145">hello following sections will setup your app tooreceive them.</span></span>

### <a name="configure-push-credentials-for-mobile-engagement"></a><span data-ttu-id="ca44c-146">Mobile Engagement için Gönderim kimlik bilgilerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ca44c-146">Configure Push credentials for Mobile Engagement</span></span>
<span data-ttu-id="ca44c-147">sizin adınıza tooallow Mobile Engagement toosend anında iletme bildirimleri, erişim tooyour Apple iOS sertifikanıza veya GCM Server API anahtarını toogrant gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca44c-147">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour Apple iOS certificate or GCM Server API Key.</span></span> 

1. <span data-ttu-id="ca44c-148">Tooyour Mobile Engagement portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="ca44c-148">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="ca44c-149">Bu proje için kullanmakta olduğunuz ve üzerinde hello ardından hello uygulamasında olduğunuz sağlamak **Katıl** hello altındaki düğmesi:</span><span class="sxs-lookup"><span data-stu-id="ca44c-149">Ensure you're in hello app we're using for this project and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![][1]
2. <span data-ttu-id="ca44c-150">Engagement Portal'ınızdaki hello ayarları sayfasına gideceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-150">You will land in hello settings page in your Engagement Portal.</span></span> <span data-ttu-id="ca44c-151">Merhaba orada tıklayın **yerel gönderim** bölümü:</span><span class="sxs-lookup"><span data-stu-id="ca44c-151">From there click on hello **Native Push** section:</span></span>
   
    ![][2]
3. <span data-ttu-id="ca44c-152">iOS Sertifikasını/GCM Server API Anahtarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ca44c-152">Configure iOS Certificate/GCM Server API Key</span></span>
   
    <span data-ttu-id="ca44c-153">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="ca44c-153">**[iOS]**</span></span>
   
    <span data-ttu-id="ca44c-154">a.</span><span class="sxs-lookup"><span data-stu-id="ca44c-154">a.</span></span> <span data-ttu-id="ca44c-155">.p12 sertifikanızı seçin, bunu yükleyip parolanızı yazın:</span><span class="sxs-lookup"><span data-stu-id="ca44c-155">Select your .p12, upload it and type your password:</span></span>
   
    ![][3]
   
    <span data-ttu-id="ca44c-156">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="ca44c-156">**[Android]**</span></span>
   
    <span data-ttu-id="ca44c-157">a.</span><span class="sxs-lookup"><span data-stu-id="ca44c-157">a.</span></span> <span data-ttu-id="ca44c-158">Merhaba Düzenle simgesine önüne **API anahtarı** hello GCM ayarları bölümünde ve gösteren yukarı hello açılan'de, hello GCM Server anahtarını yapıştırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ca44c-158">Click hello edit icon in front of **API Key** in hello GCM Settings section and in hello popup which shows up, paste hello GCM Server Key and click **OK**.</span></span> 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a><span data-ttu-id="ca44c-159">Merhaba Cordova uygulamasında anında iletme bildirimlerini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ca44c-159">Enable push notifications in hello Cordova app</span></span>
<span data-ttu-id="ca44c-160">Düzen **www/js/index.js** tooadd hello çağrısı tooMobile katılım toorequest anında iletme bildirimleri ve bir işleyici bildirin:</span><span class="sxs-lookup"><span data-stu-id="ca44c-160">Edit **www/js/index.js** tooadd hello call tooMobile Engagement toorequest push notifications and declare a handler:</span></span>

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a><span data-ttu-id="ca44c-161">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ca44c-161">Run hello app</span></span>
<span data-ttu-id="ca44c-162">**[iOS]**</span><span class="sxs-lookup"><span data-stu-id="ca44c-162">**[iOS]**</span></span>

1. <span data-ttu-id="ca44c-163">Biz XCode toobuild kullanabilir ve iOS anında iletme bildirimleri tooan gerçek cihaz yalnızca olanak tanıdığından hello aygıt tootest anında iletme bildirimleri hello uygulamasını dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-163">We will use XCode toobuild and deploy hello app on hello device tootest push notifications since iOS only allows push notifications tooan actual device.</span></span> <span data-ttu-id="ca44c-164">Cordova projenizin oluşturulduğu toohello konumuna gidin ve çok gidin**...\platforms\ios** konumu.</span><span class="sxs-lookup"><span data-stu-id="ca44c-164">Go toohello location where your Cordova project is created and navigate too**...\platforms\ios** location.</span></span> <span data-ttu-id="ca44c-165">Xcode'da hello yerel .xcodeproj dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ca44c-165">Open up hello native .xcodeproj file in XCode.</span></span> 
2. <span data-ttu-id="ca44c-166">Derleme ve sağlama profili toohello Mobile Engagement portalına ve hello hello oluşturulurken sağlanan eşleşen bir uygulama kimliği yalnızca karşıya hello sertifikayı içeren hello olan hello hesabı kullanarak hello Cordova uygulaması toohello iOS cihazı dağıtma Merhaba Cordova uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ca44c-166">Build and deploy hello Cordova app toohello iOS device using hello account which has hello provisioning profile containing hello certificate you just uploaded toohello Mobile Engagement portal and hello App Id which matches hello one you provided while creating hello Cordova app.</span></span> <span data-ttu-id="ca44c-167">Merhaba denetleyebilirsiniz *paket tanımlayıcısı* içinde **kaynakları\*-info.plist** yukarı dosya XCode toomatch.</span><span class="sxs-lookup"><span data-stu-id="ca44c-167">You can check out hello *Bundle identifier* in your **Resources\*-info.plist** file in XCode toomatch it up.</span></span> 
3. <span data-ttu-id="ca44c-168">Bu hello uygulama belirten aygıtınızda hello standart iOS açılır penceresini izni toosend bildirimleri istekleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-168">You will see hello standard iOS popup on your device saying that hello app requests permission toosend notifications.</span></span> <span data-ttu-id="ca44c-169">Merhaba izni verin.</span><span class="sxs-lookup"><span data-stu-id="ca44c-169">Grant hello permission.</span></span> 

<span data-ttu-id="ca44c-170">**[Android]**</span><span class="sxs-lookup"><span data-stu-id="ca44c-170">**[Android]**</span></span>

<span data-ttu-id="ca44c-171">GCM bildirimleri hello Android öykünücüsünde desteklenen gibi hello öykünücüsü toorun hello Android uygulaması yalnızca kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-171">You can simply use hello emulator toorun hello Android app as GCM notifications are supported on hello Android emulator.</span></span> 

    cordova run android

## <span data-ttu-id="ca44c-172"><a id="send"></a>Bir bildirim tooyour uygulaması Gönder</span><span class="sxs-lookup"><span data-stu-id="ca44c-172"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="ca44c-173">Şimdi hello cihazda çalışan bir itme tooyour uygulama gönderecek basit bir anında iletme bildirimi kampanyası oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="ca44c-173">We will now create a simple Push Notification campaign that will send a push tooyour app running on hello device:</span></span>

1. <span data-ttu-id="ca44c-174">Toohello gidin **ulaşmak** Mobile Engagement portalınızın sekmesi</span><span class="sxs-lookup"><span data-stu-id="ca44c-174">Navigate toohello **Reach** tab in your Mobile Engagement portal</span></span>
2. <span data-ttu-id="ca44c-175">Tıklatın **Yeni duyuru** toocreate anında iletme kampanyanızı</span><span class="sxs-lookup"><span data-stu-id="ca44c-175">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![][6]
3. <span data-ttu-id="ca44c-176">Kampanyanızı girişleri toocreate sağlamak **[Android]**</span><span class="sxs-lookup"><span data-stu-id="ca44c-176">Provide inputs toocreate your campaign **[Android]**</span></span>
   
   * <span data-ttu-id="ca44c-177">Kampanyanıza bir **Ad** verin.</span><span class="sxs-lookup"><span data-stu-id="ca44c-177">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="ca44c-178">Select hello **teslimat türü** olarak *sistem bildirimi* *basit*</span><span class="sxs-lookup"><span data-stu-id="ca44c-178">Select hello **Delivery Type** as *System notification* *Simple*</span></span>
   * <span data-ttu-id="ca44c-179">Select hello **teslim saati** olarak *"Her zaman"*</span><span class="sxs-lookup"><span data-stu-id="ca44c-179">Select hello **Delivery time** as *"Any Time"*</span></span>
   * <span data-ttu-id="ca44c-180">Sağlayan bir **başlık** hello itme hello ilk satırı olacak bildiriminizin için.</span><span class="sxs-lookup"><span data-stu-id="ca44c-180">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="ca44c-181">Sağlayan bir **ileti** hello ileti gövdesi görevini görecek olan, bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ca44c-181">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][11]
4. <span data-ttu-id="ca44c-182">Kampanyanızı girişleri toocreate sağlamak **[iOS]**</span><span class="sxs-lookup"><span data-stu-id="ca44c-182">Provide inputs toocreate your campaign **[iOS]**</span></span>
   
   * <span data-ttu-id="ca44c-183">Kampanyanıza bir **Ad** verin.</span><span class="sxs-lookup"><span data-stu-id="ca44c-183">Provide a **Name** for your campaign.</span></span> 
   * <span data-ttu-id="ca44c-184">Select hello **teslim saati** olarak *"dışında yalnızca uygulama"*</span><span class="sxs-lookup"><span data-stu-id="ca44c-184">Select hello **Delivery time** as *"Out of app only"*</span></span>
   * <span data-ttu-id="ca44c-185">Sağlayan bir **başlık** hello itme hello ilk satırı olacak bildiriminizin için.</span><span class="sxs-lookup"><span data-stu-id="ca44c-185">Provide a **Title** for your notification which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="ca44c-186">Sağlayan bir **ileti** hello ileti gövdesi görevini görecek olan, bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ca44c-186">Provide a **Message** for your notification which will serve as hello message body.</span></span> 
     
     ![][12]
5. <span data-ttu-id="ca44c-187">Aşağı kaydırın ve içerik bölümü hello seçin **yalnızca bildirim**</span><span class="sxs-lookup"><span data-stu-id="ca44c-187">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![][8]
6. <span data-ttu-id="ca44c-188">[İsteğe bağlı] Bir Eylem URL'si de sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-188">[Optional] You can also provide an Action URL.</span></span> <span data-ttu-id="ca44c-189">Merhaba yapılandırılırken sağlanan bir URL şemasını kullandığından emin olun **AZME\_yeniden yönlendirme\_URL** değişkeni örneğin *myapp://test*.</span><span class="sxs-lookup"><span data-stu-id="ca44c-189">Make sure that it uses a URL scheme provided while configuring hello plugin's **AZME\_REDIRECT\_URL** variable e.g. *myapp://test*.</span></span>  
7. <span data-ttu-id="ca44c-190">Ayar hello en temel kampanya olası bitirdiniz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-190">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="ca44c-191">Şimdi kaydırarak yeniden aşağı gidin ve hello tıklatın **oluşturma** toosave kampanyanızı düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca44c-191">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
8. <span data-ttu-id="ca44c-192">Son olarak **Etkinleştir** düğmesine tıklayarak kampanyanızı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="ca44c-192">Finally **Activate** your campaign</span></span>
   
    ![][10]
9. <span data-ttu-id="ca44c-193">Şimdi cihazınızda veya öykünücünüzde bu kampanyanın bir parçası olan bir anında iletme bildirimi görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ca44c-193">You should now see a push notification on your device or emulator as part of this campaign.</span></span> 

## <span data-ttu-id="ca44c-194"><a id="next-steps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ca44c-194"><a id="next-steps"></a>Next Steps</span></span>
[<span data-ttu-id="ca44c-195">Cordova Mobile Engagement SDK ile kullanılabilen tüm metotlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="ca44c-195">Overview of all methods available with Cordova Mobile Engagement SDK</span></span>](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

