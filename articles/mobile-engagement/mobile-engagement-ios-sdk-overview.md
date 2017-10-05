---
title: "Azure Mobile Engagement iOS SDK genel bakış | Microsoft Docs"
description: "En son güncelleştirmeler ve iOS için Azure Mobile Engagement SDK'sı için yordamlar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 6acd343782a3ee07750e27ec3022ff81cedfadee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="85573-103">Azure Mobile Engagement için iOS SDK’sı</span><span class="sxs-lookup"><span data-stu-id="85573-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="85573-104">Azure Mobile Engagement bir iOS uygulaması tümleştirme hakkında tüm ayrıntıları almak buradan başlayın.</span><span class="sxs-lookup"><span data-stu-id="85573-104">Start here to get all the details on how to integrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="85573-105">Try ilk vermek istiyorsanız, bunu emin olun bizim [15 dakika Öğreticisi](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="85573-105">If you'd like to give it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="85573-106">Görmek için tıklatın [SDK içerik](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="85573-106">Click to see the [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="85573-107">Tümleştirme yordamları</span><span class="sxs-lookup"><span data-stu-id="85573-107">Integration procedures</span></span>
1. <span data-ttu-id="85573-108">Buradan başlayın: [iOS uygulamanızı Mobile Engagement tümleştirme](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="85573-108">Start here: [How to integrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="85573-109">Bildirimlerinin: [ulaşma (bildirimleri), iOS uygulamanızın tümleştirme](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="85573-109">For Notifications: [How to integrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="85573-110">Etiket planı uygulama: [iOS uygulamanızı API etiketleme Gelişmiş Mobile Engagement kullanma](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="85573-110">Tag plan implementation: [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="85573-111">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="85573-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="85573-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="85573-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="85573-113">Sabit rozetleri arka planda temizlendi.</span><span class="sxs-lookup"><span data-stu-id="85573-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="85573-114">Sabit uyarılar ana sırada adlı değil API'leri hakkında XCode 9.</span><span class="sxs-lookup"><span data-stu-id="85573-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="85573-115">Bellek sızıntısı ulaşma yoklamalarda sabit.</span><span class="sxs-lookup"><span data-stu-id="85573-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="85573-116">İOS için destek bırakılan 6.X.</span><span class="sxs-lookup"><span data-stu-id="85573-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="85573-117">Uygulamanızın dağıtım hedef bu sürümünden başlayarak olmalıdır en az iOS 7.</span><span class="sxs-lookup"><span data-stu-id="85573-117">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="85573-118">Önceki sürümü için lütfen bkz. [tamamlamak sürüm notları](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="85573-118">For earlier version please see the [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="85573-119">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="85573-119">Upgrade procedures</span></span>
<span data-ttu-id="85573-120">Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz, SDK'yı yükseltirken aşağıdaki noktaları dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="85573-120">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="85573-121">SDK bkz: tam birçok sürümü eksik birkaç yordamları izleyin gerekebilir [yükseltme yordamları](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="85573-121">You may have to follow several procedures if you missed several versions of the SDK see the complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="85573-122">SDK'sı için her yeni sürümü, ilk değiştirmeniz gerekir (kaldırın ve yeniden xcode'da içeri aktarın) EngagementSDK ve EngagementReach klasörler.</span><span class="sxs-lookup"><span data-stu-id="85573-122">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-to-400"></a><span data-ttu-id="85573-123">3.0.0 4.0.0 için</span><span class="sxs-lookup"><span data-stu-id="85573-123">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="85573-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="85573-124">XCode 8</span></span>
<span data-ttu-id="85573-125">XCode 8 SDK 4.0.0 sürümünden başlayarak zorunludur.</span><span class="sxs-lookup"><span data-stu-id="85573-125">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="85573-126">XCode 7'de gerçekten bağımlı sonra kullanabilirsiniz [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="85573-126">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="85573-127">Bir bilinen hata varsa bu önceki sürüm reach modülünü 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir.</span><span class="sxs-lookup"><span data-stu-id="85573-127">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="85573-128">Bu kullanım dışı API uygulamak için olacaktır sorunu gidermek için `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:</span><span class="sxs-lookup"><span data-stu-id="85573-128">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="85573-129">**Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85573-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="85573-130">Mümkün olan en kısa sürede XCode 8'e geçer.</span><span class="sxs-lookup"><span data-stu-id="85573-130">You should switch to XCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="85573-131">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="85573-131">UserNotifications framework</span></span>
<span data-ttu-id="85573-132">Eklemenize gerek `UserNotifications` derleme aşamaları framework.</span><span class="sxs-lookup"><span data-stu-id="85573-132">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="85573-133">Proje Gezgini'nde, proje bölmesini açın ve doğru hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="85573-133">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="85573-134">Ardından, açın **"Derleme aşamaları"** sekmesi ve **"Bağlantı ikiliyi kitaplıklara"** menüsünde framework eklemek `UserNotifications.framework` -bağlantı olarak ayarlayın`Optional`</span><span class="sxs-lookup"><span data-stu-id="85573-134">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="85573-135">Uygulamayı anında iletme yeteneği</span><span class="sxs-lookup"><span data-stu-id="85573-135">Application push capability</span></span>
<span data-ttu-id="85573-136">XCode 8 uygulamanızı sıfırlama anında iletme yeteneği, lütfen tekrar gözden geçirin `capability` seçilen hedef sekmesi.</span><span class="sxs-lookup"><span data-stu-id="85573-136">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

#### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="85573-137">Yeni iOS 10 bildirim kayıt kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="85573-137">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="85573-138">Uygulama bildirimleri kaydetmek için eski kod parçacığını hala çalışır ancak iOS 10 çalıştırılırken kullanım dışı API'lerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="85573-138">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="85573-139">İçeri aktarma `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="85573-139">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="85573-140">Uygulama temsilcinizi içinde `application:didFinishLaunchingWithOptions` yöntemi Değiştir:</span><span class="sxs-lookup"><span data-stu-id="85573-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="85573-141">tarafından:</span><span class="sxs-lookup"><span data-stu-id="85573-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="85573-142">UNUserNotificationCenter temsilci çakışmalarını çözme</span><span class="sxs-lookup"><span data-stu-id="85573-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="85573-143">*Uygulamanızı ya da üçüncü taraf Kitaplıklarınızı biri uygulayan bir `UNUserNotificationCenterDelegate` sonra da bu bölümü atlayabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="85573-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="85573-144">A `UNUserNotificationCenter` temsilci SDK tarafından katılım bildirimleri 10 veya daha büyük iOS çalıştıran cihazlarda yaşam döngüsünü izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85573-144">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="85573-145">SDK, kendi uygulamanızda `UNUserNotificationCenterDelegate` protokol ancak yalnızca bir olabilir `UNUserNotificationCenter` temsilci uygulama başına.</span><span class="sxs-lookup"><span data-stu-id="85573-145">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="85573-146">Eklenen herhangi bir temsilci `UNUserNotificationCenter` nesne katılım bir çakışma.</span><span class="sxs-lookup"><span data-stu-id="85573-146">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="85573-147">SDK veya herhangi diğer üçüncü bir tarafın temsilci algılarsa sonra kendi uygulama çakışmaları olanağı vermek için kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="85573-147">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="85573-148">Çakışmaları çözümlemek amacıyla kendi temsilciye katılım mantığı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="85573-148">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="85573-149">Bunu başarmak için iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="85573-149">There are two ways to achieve this.</span></span>

<span data-ttu-id="85573-150">SDK çağrıları temsilciniz iletme tarafından yalnızca 1, Teklif:</span><span class="sxs-lookup"><span data-stu-id="85573-150">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

<span data-ttu-id="85573-151">Veya içinden devralma tarafından 2, teklif `AEUserNotificationHandler` sınıfı</span><span class="sxs-lookup"><span data-stu-id="85573-151">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> <span data-ttu-id="85573-152">Bir bildirim geçirerek değil veya katılım üzerinden gelen olup olmadığını belirlemek, `userInfo` aracı sözlüğe `isEngagementPushPayload:` sınıf yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85573-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="85573-153">Olduğundan emin olun `UNUserNotificationCenter` nesnenin temsilci temsilciniz ya da içinde ayarlanmış `application:willFinishLaunchingWithOptions:` veya `application:didFinishLaunchingWithOptions:` uygulama temsilcinizi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="85573-153">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="85573-154">Örneğin, yukarıdaki teklifi 1 uygulanırsa:</span><span class="sxs-lookup"><span data-stu-id="85573-154">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
