---
title: "Objective C'de iOS için Azure Mobile Engagement başlangıç aaaGet | Microsoft Docs"
description: "Bilgi nasıl iOS uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="0bf2d-103">Objective C’de iOS uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0bf2d-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="0bf2d-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar tooan iOS uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users tooan iOS application.</span></span>
<span data-ttu-id="0bf2d-105">Bu öğreticide, temel verileri toplayan ve Apple Anında İletme Bildirimi Sistemi’ni (APNS) kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="0bf2d-106">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-106">This tutorial requires hello following:</span></span>

* <span data-ttu-id="0bf2d-107">MAC App Store'dan yükleyebileceğiniz XCode 8</span><span class="sxs-lookup"><span data-stu-id="0bf2d-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="0bf2d-108">Merhaba [Mobile Engagement iOS SDK'sı]</span><span class="sxs-lookup"><span data-stu-id="0bf2d-108">hello [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="0bf2d-109">Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin tüm Mobile Engagement öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf2d-110">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="0bf2d-111">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0bf2d-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="0bf2d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="0bf2d-113"><a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="0bf2d-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="0bf2d-114"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="0bf2d-114"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="0bf2d-115">Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-115">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="0bf2d-116">Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement iOS SDK tümleştirmesi](mobile-engagement-ios-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0bf2d-116">hello complete integration documentation can be found in hello [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="0bf2d-117">XCode toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-117">We will create a basic app with XCode toodemonstrate hello integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="0bf2d-118">Yeni bir iOS projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0bf2d-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="0bf2d-119">Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="0bf2d-119">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="0bf2d-120">Merhaba karşıdan [Mobile Engagement iOS SDK'sı].</span><span class="sxs-lookup"><span data-stu-id="0bf2d-120">Download hello [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="0bf2d-121">Merhaba ayıklayın. tar.gz dosyasını bilgisayarınızdaki tooa klasöre.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-121">Extract hello .tar.gz file tooa folder in your computer.</span></span>
3. <span data-ttu-id="0bf2d-122">Merhaba projesine sağ tıklayın ve ardından **eklemek için dosyaları**.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-122">Right-click hello project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="0bf2d-123">Toohello hello SDK'sını ayıkladığınız klasöre gidin, seçin hello `EngagementSDK` klasörünü tıklatın **seçenekleri** hello sol alt köşedeki ve o hello onay kutusunu emin olun **gerekirse öğeleri Kopyala** ve hello Hedef onay kutusunu denetlenir sonra basın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-123">Navigate toohello folder where you extracted hello SDK, select hello `EngagementSDK` folder, click **Options** on hello bottom left corner and make sure that hello checkbox **Copy items if needed** and hello checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="0bf2d-124">Açık hello **derleme aşamaları** sekmesinde ve hello **bağlantı ikiliyi kitaplıklara** menüsünde hello çerçeveleri aşağıda gösterildiği gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-124">Open hello **Build Phases** tab, and in hello **Link Binary With Libraries** menu, add hello frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="0bf2d-125">Toohello uygulamanızın Azure portalında dön **bağlantı bilgisi** sayfası ve kopyalama hello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-125">Go back toohello Azure portal in your app's **Connection Info** page and copy hello connection string.</span></span>

    ![][4]
7. <span data-ttu-id="0bf2d-126">Aşağıdaki kod satırı hello eklemek, **AppDelegate.m** dosya.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-126">Add hello following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="0bf2d-127">Şimdi hello hello bağlantı dizesini yapıştırın `didFinishLaunchingWithOptions` temsilci.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-127">Now paste hello connection string in hello `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="0bf2d-128">`setTestLogEnabled`SDK günlükleri için tooidentify sorunları sağlayan isteğe bağlı bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you tooidentify issues.</span></span>

## <span data-ttu-id="0bf2d-129"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0bf2d-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="0bf2d-130">Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-130">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="0bf2d-131">Açık hello **ViewController.h** dosya ve içeri aktarma **EngagementViewController.h**:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-131">Open hello **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="0bf2d-132">Şimdi hello hello Süper sınıfını değiştirmek **ViewController** tarafından arabirim `EngagementViewController`:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-132">Now replace hello super class of hello **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="0bf2d-133"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="0bf2d-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="0bf2d-134"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0bf2d-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="0bf2d-135">Mobile Engagement anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında toointeract kullanıcılarınız ve REACH sağlar.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-135">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="0bf2d-136">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-136">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="0bf2d-137">Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-137">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="0bf2d-138">Uygulama tooreceive sessiz anında iletme bildirimlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0bf2d-138">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a><span data-ttu-id="0bf2d-139">Merhaba ulaşma kitaplığı tooyour projesini ekleyin</span><span class="sxs-lookup"><span data-stu-id="0bf2d-139">Add hello Reach library tooyour project</span></span>
1. <span data-ttu-id="0bf2d-140">Projenize sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-140">Right-click your project.</span></span>
2. <span data-ttu-id="0bf2d-141">**Add files to** (Dosyaları şuraya ekle) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="0bf2d-142">Merhaba SDK'sını ayıkladığınız toohello klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-142">Navigate toohello folder where you extracted hello SDK.</span></span>
4. <span data-ttu-id="0bf2d-143">Select hello `EngagementReach` klasör.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-143">Select hello `EngagementReach` folder.</span></span>
5. <span data-ttu-id="0bf2d-144">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="0bf2d-145">Uygulama Temsilcinizi değiştirme</span><span class="sxs-lookup"><span data-stu-id="0bf2d-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="0bf2d-146">Geri **AppDeletegate.m** dosya, hello Engagement Reach modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="0bf2d-146">Back in **AppDeletegate.m** file, import hello Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="0bf2d-147">İç hello `application:didFinishLaunchingWithOptions` yöntemi, bir Reach modülü oluşturun ve tooyour mevcut Engagement başlatma satır geçirin:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-147">Inside hello `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it tooyour existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a><span data-ttu-id="0bf2d-148">Uygulama tooreceive APNS anında iletme bildirimlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0bf2d-148">Enable your app tooreceive APNS Push Notifications</span></span>
1. <span data-ttu-id="0bf2d-149">Satır toohello aşağıdaki hello eklemek `application:didFinishLaunchingWithOptions` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-149">Add hello following line toohello `application:didFinishLaunchingWithOptions` method:</span></span>

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }
2. <span data-ttu-id="0bf2d-150">Merhaba eklemek `application:didRegisterForRemoteNotificationsWithDeviceToken` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-150">Add hello `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="0bf2d-151">Merhaba eklemek `didFailToRegisterForRemoteNotificationsWithError` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-151">Add hello `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. <span data-ttu-id="0bf2d-152">Merhaba eklemek `didReceiveRemoteNotification:fetchCompletionHandler` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="0bf2d-152">Add hello `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK'sı]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
