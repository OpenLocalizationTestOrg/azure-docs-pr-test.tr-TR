---
title: "swift'te iOS için Azure Mobile Engagement başlangıç aaaGet | Microsoft Docs"
description: "Bilgi nasıl iOS uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a><span data-ttu-id="d2251-103">Swift’te iOS Uygulamaları için Azure Mobile Engagement Kullanmaya Başlama</span><span class="sxs-lookup"><span data-stu-id="d2251-103">Get Started with Azure Mobile Engagement for iOS Apps in Swift</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d2251-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar tooan iOS uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d2251-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="d2251-105">Bu öğreticide, temel verileri toplayan ve Apple Anında İletme Bildirimi Sistemi’ni (APNS) kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="d2251-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="d2251-106">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="d2251-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="d2251-107">MAC App Store'dan yükleyebileceğiniz XCode 8</span><span class="sxs-lookup"><span data-stu-id="d2251-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="d2251-108">Merhaba [Mobile Engagement iOS SDK'sı]</span><span class="sxs-lookup"><span data-stu-id="d2251-108">hello [Mobile Engagement iOS SDK]</span></span>
* <span data-ttu-id="d2251-109">Apple Dev Center'ınızda edinebileceğiniz anında iletme bildirimi sertifikası (.p12)</span><span class="sxs-lookup"><span data-stu-id="d2251-109">Push notification certificate (.p12) that you can obtain on your Apple Dev Center</span></span>

> [!NOTE]
> <span data-ttu-id="d2251-110">Bu öğreticide Swift sürüm 3.0 kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d2251-110">This tutorial uses Swift version 3.0.</span></span> 
> 
> 

<span data-ttu-id="d2251-111">Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin tüm Mobile Engagement öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="d2251-111">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="d2251-112">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2251-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d2251-113">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2251-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d2251-114">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span><span class="sxs-lookup"><span data-stu-id="d2251-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).</span></span>
> 
> 

## <span data-ttu-id="d2251-115"><a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="d2251-115"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d2251-116"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="d2251-116"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="d2251-117">Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d2251-117">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="d2251-118">Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement iOS SDK tümleştirmesi](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d2251-118">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="d2251-119">XCode toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="d2251-119">We will create a basic app with XCode toodemonstrate hello integration:</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="d2251-120">Yeni bir iOS projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2251-120">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="d2251-121">Uygulamanızın tooMobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="d2251-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="d2251-122">Merhaba karşıdan [Mobile Engagement iOS SDK'sı]</span><span class="sxs-lookup"><span data-stu-id="d2251-122">Download hello [Mobile Engagement iOS SDK]</span></span>
2. <span data-ttu-id="d2251-123">Merhaba ayıklayın. tar.gz dosyasını bilgisayarınızdaki tooa klasöre</span><span class="sxs-lookup"><span data-stu-id="d2251-123">Extract hello .tar.gz file tooa folder in your computer</span></span>
3. <span data-ttu-id="d2251-124">Merhaba projeyi sağ tıklatın ve seçin "çok dosyaları Ekle..."</span><span class="sxs-lookup"><span data-stu-id="d2251-124">Right click hello project and select "Add files too..."</span></span>
   
    ![][1]
4. <span data-ttu-id="d2251-125">Ayıkladığınız hello SDK ve select hello toohello klasöre gidin `EngagementSDK` klasörünü seçip Tamam'a basın.</span><span class="sxs-lookup"><span data-stu-id="d2251-125">Navigate toohello folder where you extracted hello SDK and select hello `EngagementSDK` folder then press OK.</span></span>
   
    ![][2]
5. <span data-ttu-id="d2251-126">Açık hello `Build Phases` sekmesi ve hello `Link Binary With Libraries` menü hello çerçeveleri aşağıda gösterildiği gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d2251-126">Open hello `Build Phases` tab and in hello `Link Binary With Libraries` menu add hello frameworks as shown below:</span></span>
   
    ![][3]
6. <span data-ttu-id="d2251-127">Dosya seçerek bir köprü oluşturma üst bilgisi toobe mümkün toouse hello SDK'ın Objective C API'lerini oluşturma > Yeni > Dosya > iOS > kaynak > üst bilgi dosyası.</span><span class="sxs-lookup"><span data-stu-id="d2251-127">Create a Bridging header toobe able toouse hello SDK's Objective C APIs by choosing File > New > File > iOS > Source > Header File.</span></span>
   
    ![][4]
7. <span data-ttu-id="d2251-128">Üstbilgi dosyası tooexpose Mobile Engagement Objective-C kodunu tooyour SWIFT kodu köprüleme hello düzenleme, içeri aktarmalar aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d2251-128">Edit hello bridging header file tooexpose Mobile Engagement Objective-C code tooyour Swift code, add hello following imports :</span></span>
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. <span data-ttu-id="d2251-129">Derleme Ayarları'nda bir yol toothis üstbilgisi hello Objective-C köprü oluşturma üst bilgisi derleme ayarının Swift derleyicisi - kod oluşturma altında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d2251-129">Under Build Settings, make sure hello Objective-C Bridging Header build setting under Swift Compiler - Code Generation has a path toothis header.</span></span> <span data-ttu-id="d2251-130">Yol için bir örnek şudur: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (bağlı olarak hello yolu)**</span><span class="sxs-lookup"><span data-stu-id="d2251-130">Here is a path example: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (depending on hello path)**</span></span>
   
   ![][6]
9. <span data-ttu-id="d2251-131">Toohello uygulamanızın Azure portalında dön *bağlantı bilgisi* sayfası ve kopyalama hello bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="d2251-131">Go back toohello Azure portal in your app's *Connection Info* page and copy hello Connection String</span></span>
   
   ![][5]
10. <span data-ttu-id="d2251-132">Şimdi hello hello bağlantı dizesini yapıştırın `didFinishLaunchingWithOptions` temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="d2251-132">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate</span></span>
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <span data-ttu-id="d2251-133"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d2251-133"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="d2251-134">Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2251-134">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="d2251-135">Açık hello **ViewController.swift** dosya ve hello temel sınıfını değiştirme **ViewController** toobe **EngagementViewController**:</span><span class="sxs-lookup"><span data-stu-id="d2251-135">Open hello **ViewController.swift** file and replace hello base class of **ViewController** toobe **EngagementViewController**:</span></span>
   
    `class ViewController : EngagementViewController {`

## <span data-ttu-id="d2251-136"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="d2251-136"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d2251-137"><a id="integrate-push"></a>Anında İletme Bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d2251-137"><a id="integrate-push"></a>Enabling Push Notifications and in-app messaging</span></span>
<span data-ttu-id="d2251-138">Mobile Engagement hello Kampanyalar bağlamında toointeract ve anında iletme bildirimleri ve uygulama içi Mesajlaşma ile kullanıcılarınız erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2251-138">Mobile Engagement allows you toointeract and REACH with your users with Push Notifications and In-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="d2251-139">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="d2251-139">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="d2251-140">Merhaba aşağıdaki bölümlerde, app tooreceive Kurulum bunları.</span><span class="sxs-lookup"><span data-stu-id="d2251-140">hello following sections will setup your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="d2251-141">Uygulama tooreceive sessiz anında iletme bildirimlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d2251-141">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="d2251-142">Merhaba ulaşma kitaplığı tooyour projesini ekleyin</span><span class="sxs-lookup"><span data-stu-id="d2251-142">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="d2251-143">Projenize sağ tıklayın</span><span class="sxs-lookup"><span data-stu-id="d2251-143">Right click your project</span></span>
2. <span data-ttu-id="d2251-144">`Add file too...` seçeneğini belirleyin</span><span class="sxs-lookup"><span data-stu-id="d2251-144">Select `Add file too...`</span></span>
3. <span data-ttu-id="d2251-145">Merhaba SDK'sını ayıkladığınız toohello klasöre gidin</span><span class="sxs-lookup"><span data-stu-id="d2251-145">Navigate toohello folder where you extracted hello SDK</span></span>
4. <span data-ttu-id="d2251-146">Select hello `EngagementReach` klasörü</span><span class="sxs-lookup"><span data-stu-id="d2251-146">Select hello `EngagementReach` folder</span></span>
5. <span data-ttu-id="d2251-147">Ekle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d2251-147">Click Add</span></span>
6. <span data-ttu-id="d2251-148">Mobile Engagement Objective-C Reach üst bilgi dosyası tooexpose üstbilgileri köprüleme hello düzenleyin ve hello aşağıdaki içeri aktarmaları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d2251-148">Edit hello bridging header file tooexpose Mobile Engagement Objective-C Reach headers and add hello following imports :</span></span>
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a><span data-ttu-id="d2251-149">Uygulama Temsilcinizi değiştirme</span><span class="sxs-lookup"><span data-stu-id="d2251-149">Modify your Application Delegate</span></span>
1. <span data-ttu-id="d2251-150">İç hello `didFinishLaunchingWithOptions` - reach modülü oluşturun ve tooyour mevcut Engagement başlatma satır geçirme:</span><span class="sxs-lookup"><span data-stu-id="d2251-150">Inside  hello `didFinishLaunchingWithOptions` -  create a reach module and pass it tooyour existing Engagement initialization line:</span></span>
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="d2251-151">Uygulama tooreceive APNS anında iletme bildirimlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d2251-151">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="d2251-152">Satır toohello aşağıdaki hello eklemek `didFinishLaunchingWithOptions` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d2251-152">Add hello following line toohello `didFinishLaunchingWithOptions` method:</span></span>
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. <span data-ttu-id="d2251-153">Merhaba eklemek `didRegisterForRemoteNotificationsWithDeviceToken` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="d2251-153">Add hello `didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. <span data-ttu-id="d2251-154">Merhaba eklemek `didReceiveRemoteNotification:fetchCompletionHandler:` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="d2251-154">Add hello `didReceiveRemoteNotification:fetchCompletionHandler:` method as follows:</span></span>
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK'sı]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
