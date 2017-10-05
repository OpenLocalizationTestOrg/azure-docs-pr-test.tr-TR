---
title: "Objective C'de iOS için Azure Mobile Engagement ile Çalışmaya Başlama | Microsoft Belgeleri"
description: "iOS uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement kullanmayı öğrenin."
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
ms.openlocfilehash: 1b87a2ebb35b31ee3d3139ecead6267e62eb1033
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a><span data-ttu-id="ea4ad-103">Objective C’de iOS uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ea4ad-103">Get Started with Azure Mobile Engagement for iOS apps in Objective C</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="ea4ad-104">Bu konuda, uygulama kullanımınızı anlamak ve bir iOS uygulamasının segmentli kullanıcılarına anında iletme bildirimleri göndermek için nasıl Azure Mobile Engagement kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users to an iOS application.</span></span>
<span data-ttu-id="ea4ad-105">Bu öğreticide, temel verileri toplayan ve Apple Anında İletme Bildirimi Sistemi’ni (APNS) kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-105">In this tutorial, you create a blank iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

<span data-ttu-id="ea4ad-106">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-106">This tutorial requires the following:</span></span>

* <span data-ttu-id="ea4ad-107">MAC App Store'dan yükleyebileceğiniz XCode 8</span><span class="sxs-lookup"><span data-stu-id="ea4ad-107">XCode 8, which you can install from your MAC App Store</span></span>
* <span data-ttu-id="ea4ad-108">[Mobile Engagement iOS SDK]</span><span class="sxs-lookup"><span data-stu-id="ea4ad-108">the [Mobile Engagement iOS SDK]</span></span>

<span data-ttu-id="ea4ad-109">Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin tüm Mobile Engagement öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-109">Completing this tutorial is a prerequisite for all other Mobile Engagement tutorials for iOS apps.</span></span>

> [!NOTE]
> <span data-ttu-id="ea4ad-110">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-110">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ea4ad-111">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ea4ad-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="ea4ad-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).</span></span>
>
>

## <span data-ttu-id="ea4ad-113"><a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="ea4ad-113"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="ea4ad-114"><a id="connecting-app"></a>Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="ea4ad-114"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="ea4ad-115">Bu öğreticide, veri toplamak ve anında iletme bildirimi göndermek için gerekli en küçük grup olan bir "temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-115">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="ea4ad-116">Tümleştirme belgelerinin tamamı [Mobile Engagement iOS SDK tümleştirmesi](mobile-engagement-ios-sdk-overview.md)’nde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-116">The complete integration documentation can be found in the [Mobile Engagement iOS SDK integration](mobile-engagement-ios-sdk-overview.md)</span></span>

<span data-ttu-id="ea4ad-117">Tümleştirmeyi göstermek için XCode ile temel bir uygulama oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-117">We will create a basic app with XCode to demonstrate the integration.</span></span>

### <a name="create-a-new-ios-project"></a><span data-ttu-id="ea4ad-118">Yeni bir iOS projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea4ad-118">Create a new iOS project</span></span>
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-to-the-mobile-engagement-backend"></a><span data-ttu-id="ea4ad-119">Uygulamanızı Mobile Engagement arka ucuna bağlama</span><span class="sxs-lookup"><span data-stu-id="ea4ad-119">Connect your app to the Mobile Engagement backend</span></span>
1. <span data-ttu-id="ea4ad-120">[Mobile Engagement iOS SDK]’yı indirin.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-120">Download the [Mobile Engagement iOS SDK].</span></span>
2. <span data-ttu-id="ea4ad-121">.tar.gz dosyasını bilgisayarınızdaki bir klasöre ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-121">Extract the .tar.gz file to a folder in your computer.</span></span>
3. <span data-ttu-id="ea4ad-122">Projeye sağ tıklayıp **Add files to** (Dosyaları şuraya ekle) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-122">Right-click the project, and then select **Add files to**.</span></span>

    ![][1]
4. <span data-ttu-id="ea4ad-123">SDK’yı ayıkladığınız klasöre gidip `EngagementSDK` klasörünü seçin, sol alt köşedeki **Seçenekler**’e tıklayın ve **Gerekirse öğeleri kopyala** onay kutusuyla hedefinizin onay kutusunun onay işaretli olduğundan emin olduktan sonra **Tamam**’a basın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-123">Navigate to the folder where you extracted the SDK, select the `EngagementSDK` folder, click **Options** on the bottom left corner and make sure that the checkbox **Copy items if needed** and the checkbox for your target are checked then press **OK**.</span></span>

    ![][2]
5. <span data-ttu-id="ea4ad-124">**Build Phases** (Derleme Aşamaları) sekmesini açın, **Link Binary With Libraries** (İkiliyi Kitaplıklara Bağla) menüsünde çerçeveleri aşağıda gösterildiği gibi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-124">Open the **Build Phases** tab, and in the **Link Binary With Libraries** menu, add the frameworks as shown below:</span></span>

    ![][3]
6. <span data-ttu-id="ea4ad-125">Uygulamanızın**Bağlantı Bilgileri** sayfasında Azure Portalı’na geri gidin ve bağlantı dizesini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-125">Go back to the Azure portal in your app's **Connection Info** page and copy the connection string.</span></span>

    ![][4]
7. <span data-ttu-id="ea4ad-126">**AppDelegate.m** dosyanıza aşağıdaki kod satırını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-126">Add the following line of code in your **AppDelegate.m** file.</span></span>

        #import "EngagementAgent.h"
8. <span data-ttu-id="ea4ad-127">Şimdi, bağlantı dizesini `didFinishLaunchingWithOptions` temsilcisine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-127">Now paste the connection string in the `didFinishLaunchingWithOptions` delegate.</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. <span data-ttu-id="ea4ad-128">`setTestLogEnabled`, sorunları belirleyebilmeniz için SDK günlüklerini etkinleştiren isteğe bağlı bir ifadedir.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-128">`setTestLogEnabled` is an optional statement which enables SDK logs for you to identify issues.</span></span>

## <span data-ttu-id="ea4ad-129"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ea4ad-129"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="ea4ad-130">Veri göndermeye başlamak ve kullanıcıların etkin olduğundan emin olmak için, Mobile Engagement arka ucuna en az bir ekran (Etkinlik) göndermelisiniz.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-130">In order to start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="ea4ad-131">**ViewController.h** dosyasını açıp **EngagementViewController.h** dosyasını içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-131">Open the **ViewController.h** file and import **EngagementViewController.h**:</span></span>

    `#import "EngagementViewController.h"`
2. <span data-ttu-id="ea4ad-132">**ViewController** arabiriminin süper sınıfını `EngagementViewController` ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-132">Now replace the super class of the **ViewController** interface by `EngagementViewController`:</span></span>

    `@interface ViewController : EngagementViewController`

## <span data-ttu-id="ea4ad-133"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="ea4ad-133"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="ea4ad-134"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ea4ad-134"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="ea4ad-135">Mobile Engagement, kullanıcılarınız ile etkileşim kurmanızı ve onlara kampanyalar bağlamında anında iletme bildirimleri ve uygulama içi mesajlaşma aracılığıyla erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-135">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="ea4ad-136">Mobile Engagement portalında bu modüle REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-136">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="ea4ad-137">Aşağıdaki bölümler bunları almak için uygulamanızı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-137">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="ea4ad-138">Sessiz Anında İletme Bildirimlerini almak üzere uygulamanızı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ea4ad-138">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-the-reach-library-to-your-project"></a><span data-ttu-id="ea4ad-139">Reach kitaplığını projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-139">Add the Reach library to your project</span></span>
1. <span data-ttu-id="ea4ad-140">Projenize sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-140">Right-click your project.</span></span>
2. <span data-ttu-id="ea4ad-141">**Add files to** (Dosyaları şuraya ekle) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-141">Select **Add file to**.</span></span>
3. <span data-ttu-id="ea4ad-142">SDK’yı ayıkladığınız klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-142">Navigate to the folder where you extracted the SDK.</span></span>
4. <span data-ttu-id="ea4ad-143">`EngagementReach` klasörünü seçin.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-143">Select the `EngagementReach` folder.</span></span>
5. <span data-ttu-id="ea4ad-144">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-144">Click **Add**.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="ea4ad-145">Uygulama Temsilcinizi değiştirme</span><span class="sxs-lookup"><span data-stu-id="ea4ad-145">Modify your Application Delegate</span></span>
1. <span data-ttu-id="ea4ad-146">**AppDeletegate.m** dosyana geri dönüp Engagement Reach modülünü içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="ea4ad-146">Back in **AppDeletegate.m** file, import the Engagement Reach module.</span></span>

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. <span data-ttu-id="ea4ad-147">`application:didFinishLaunchingWithOptions` yöntemi içerisinde bir Reach modülü oluşturun ve bu modülü mevcut Engagement başlatma satırınıza geçirin:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-147">Inside the `application:didFinishLaunchingWithOptions` method, create a Reach module and pass it to your existing Engagement initialization line:</span></span>

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-to-receive-apns-push-notifications"></a><span data-ttu-id="ea4ad-148">APNS Anında İletme Bildirimlerini almak üzere uygulamanızı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ea4ad-148">Enable your app to receive APNS Push Notifications</span></span>
1. <span data-ttu-id="ea4ad-149">`application:didFinishLaunchingWithOptions` yöntemine aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-149">Add the following line to the `application:didFinishLaunchingWithOptions` method:</span></span>

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
2. <span data-ttu-id="ea4ad-150">`application:didRegisterForRemoteNotificationsWithDeviceToken` yöntemini aşağıdaki şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-150">Add the `application:didRegisterForRemoteNotificationsWithDeviceToken` method as follows:</span></span>

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. <span data-ttu-id="ea4ad-151">`didFailToRegisterForRemoteNotificationsWithError` yöntemini aşağıdaki şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-151">Add the `didFailToRegisterForRemoteNotificationsWithError` method as follows:</span></span>

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed to get token, error: %@", error);
        }
4. <span data-ttu-id="ea4ad-152">`didReceiveRemoteNotification:fetchCompletionHandler` yöntemini aşağıdaki şekilde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ea4ad-152">Add the `didReceiveRemoteNotification:fetchCompletionHandler` method as follows:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
<span data-ttu-id="ea4ad-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span><span class="sxs-lookup"><span data-stu-id="ea4ad-153">[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
