---
title: "aaaAzure Mobile Engagement iOS SDK genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a><span data-ttu-id="f4186-103">Azure Mobile Engagement için iOS SDK’sı</span><span class="sxs-lookup"><span data-stu-id="f4186-103">iOS SDK for Azure Mobile Engagement</span></span>
<span data-ttu-id="f4186-104">Tooget tüm hello ayrıntıları hakkında buradan başlayın toointegrate Azure Mobile Engagement iOS uygulaması içinde.</span><span class="sxs-lookup"><span data-stu-id="f4186-104">Start here tooget all hello details on how toointegrate Azure Mobile Engagement in an iOS App.</span></span> <span data-ttu-id="f4186-105">Toogive isterseniz bir try ilk olarak, emin olun, bunu bizim [15 dakika Öğreticisi](mobile-engagement-ios-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f4186-105">If you'd like toogive it a try first, make sure you do our [15 minutes tutorial](mobile-engagement-ios-get-started.md).</span></span>

<span data-ttu-id="f4186-106">Toosee hello tıklatın [SDK içerik](mobile-engagement-ios-sdk-content.md)</span><span class="sxs-lookup"><span data-stu-id="f4186-106">Click toosee hello [SDK Content](mobile-engagement-ios-sdk-content.md)</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="f4186-107">Tümleştirme yordamları</span><span class="sxs-lookup"><span data-stu-id="f4186-107">Integration procedures</span></span>
1. <span data-ttu-id="f4186-108">Buradan başlayın: [nasıl toointegrate Mobile Engagement iOS uygulamanıza](mobile-engagement-ios-integrate-engagement.md)</span><span class="sxs-lookup"><span data-stu-id="f4186-108">Start here: [How toointegrate Mobile Engagement in your iOS app](mobile-engagement-ios-integrate-engagement.md)</span></span>
2. <span data-ttu-id="f4186-109">Bildirimlerinin: [nasıl toointegrate ulaşma (bildirimler) iOS uygulamanıza](mobile-engagement-ios-integrate-engagement-reach.md)</span><span class="sxs-lookup"><span data-stu-id="f4186-109">For Notifications: [How toointegrate Reach (Notifications) in your iOS app](mobile-engagement-ios-integrate-engagement-reach.md)</span></span>
3. <span data-ttu-id="f4186-110">Etiket planı uygulama: [nasıl toouse hello Mobile Engagement iOS uygulamanızı API etiketleme Gelişmiş](mobile-engagement-ios-use-engagement-api.md)</span><span class="sxs-lookup"><span data-stu-id="f4186-110">Tag plan implementation: [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md)</span></span>

## <a name="release-notes"></a><span data-ttu-id="f4186-111">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="f4186-111">Release notes</span></span>
### <a name="410-07172017"></a><span data-ttu-id="f4186-112">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="f4186-112">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="f4186-113">Sabit rozetleri arka planda temizlendi.</span><span class="sxs-lookup"><span data-stu-id="f4186-113">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="f4186-114">Sabit uyarılar ana sırada adlı değil API'leri hakkında XCode 9.</span><span class="sxs-lookup"><span data-stu-id="f4186-114">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="f4186-115">Bellek sızıntısı ulaşma yoklamalarda sabit.</span><span class="sxs-lookup"><span data-stu-id="f4186-115">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="f4186-116">İOS için destek bırakılan 6.X.</span><span class="sxs-lookup"><span data-stu-id="f4186-116">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="f4186-117">Bu sürüm hello dağıtım hedefi, uygulamanızın başlangıç olmalıdır en az iOS 7.</span><span class="sxs-lookup"><span data-stu-id="f4186-117">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

<span data-ttu-id="f4186-118">Önceki sürümü için lütfen bkz hello [tamamlamak sürüm notları](mobile-engagement-ios-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="f4186-118">For earlier version please see hello [complete release notes](mobile-engagement-ios-release-notes.md)</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="f4186-119">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="f4186-119">Upgrade procedures</span></span>
<span data-ttu-id="f4186-120">Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.</span><span class="sxs-lookup"><span data-stu-id="f4186-120">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="f4186-121">Bkz: SDK hello birçok sürümü eksik, çeşitli yordamlar toofollow olabilir hello tam [yükseltme yordamları](mobile-engagement-ios-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="f4186-121">You may have toofollow several procedures if you missed several versions of hello SDK see hello complete [Upgrade Procedures](mobile-engagement-ios-upgrade-procedure.md).</span></span>

<span data-ttu-id="f4186-122">Hello SDK her yeni sürümü için önce değiştirmeniz gerekir (kaldırın ve yeniden xcode'da içeri aktarın) EngagementSDK ve EngagementReach klasörleri hello.</span><span class="sxs-lookup"><span data-stu-id="f4186-122">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

### <a name="from-300-too400"></a><span data-ttu-id="f4186-123">3.0.0 gelen too4.0.0</span><span class="sxs-lookup"><span data-stu-id="f4186-123">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="f4186-124">XCode 8</span><span class="sxs-lookup"><span data-stu-id="f4186-124">XCode 8</span></span>
<span data-ttu-id="f4186-125">XCode 8 hello SDK 4.0.0 sürümünden başlayarak zorunludur.</span><span class="sxs-lookup"><span data-stu-id="f4186-125">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="f4186-126">XCode 7'de gerçekten bağımlı sonra hello kullanabilir [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="f4186-126">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="f4186-127">Bir bilinen hata varsa bu önceki sürümünü reach modülünü hello 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir.</span><span class="sxs-lookup"><span data-stu-id="f4186-127">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="f4186-128">toofix bu tooimplement hello olacaktır API kullanım dışı `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:</span><span class="sxs-lookup"><span data-stu-id="f4186-128">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="f4186-129">**Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4186-129">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="f4186-130">Mümkün olan en kısa sürede tooXCode 8 geçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="f4186-130">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

#### <a name="usernotifications-framework"></a><span data-ttu-id="f4186-131">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="f4186-131">UserNotifications framework</span></span>
<span data-ttu-id="f4186-132">Tooadd hello gereksinim `UserNotifications` derleme aşamaları framework.</span><span class="sxs-lookup"><span data-stu-id="f4186-132">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="f4186-133">Merhaba proje Gezgini'nde, proje bölmesini açın ve hello doğru hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="f4186-133">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="f4186-134">Merhaba açın **"Derleme aşamaları"** sekmesi ve hello **"Bağlantı ikiliyi kitaplıklara"** menüsünde framework eklemek `UserNotifications.framework` -kümesi hello bağlantı olarak`Optional`</span><span class="sxs-lookup"><span data-stu-id="f4186-134">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

#### <a name="application-push-capability"></a><span data-ttu-id="f4186-135">Uygulamayı anında iletme yeteneği</span><span class="sxs-lookup"><span data-stu-id="f4186-135">Application push capability</span></span>
<span data-ttu-id="f4186-136">XCode 8 uygulamanızı sıfırlama anında iletme yeteneği, Lütfen çift hello denetleyin `capability` seçilen hedef sekmesi.</span><span class="sxs-lookup"><span data-stu-id="f4186-136">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

#### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="f4186-137">Merhaba yeni iOS 10 bildirim kayıt kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="f4186-137">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="f4186-138">toonotifications hala çalışır ancak kullanıyor hello eski kod parçacığını tooregister hello uygulaması, iOS 10 çalıştırılırken API'leri kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="f4186-138">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="f4186-139">İçeri aktarma hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="f4186-139">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>

<span data-ttu-id="f4186-140">Uygulama temsilcinizi içinde `application:didFinishLaunchingWithOptions` yöntemi Değiştir:</span><span class="sxs-lookup"><span data-stu-id="f4186-140">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

<span data-ttu-id="f4186-141">tarafından:</span><span class="sxs-lookup"><span data-stu-id="f4186-141">by :</span></span>

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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="f4186-142">UNUserNotificationCenter temsilci çakışmalarını çözme</span><span class="sxs-lookup"><span data-stu-id="f4186-142">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="f4186-143">*Uygulamanızı ya da üçüncü taraf Kitaplıklarınızı biri uygulayan bir `UNUserNotificationCenterDelegate` sonra da bu bölümü atlayabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="f4186-143">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="f4186-144">A `UNUserNotificationCenter` temsilci hello SDK toomonitor hello yaşam döngüsü katılım bildirimler iOS 10 veya daha büyük çalıştıran cihazlarda tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f4186-144">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="f4186-145">Merhaba SDK sahip hello kendi uyarlamasını `UNUserNotificationCenterDelegate` protokol ancak yalnızca bir olabilir `UNUserNotificationCenter` temsilci uygulama başına.</span><span class="sxs-lookup"><span data-stu-id="f4186-145">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="f4186-146">Herhangi bir temsilci eklenen toohello `UNUserNotificationCenter` nesne katılım bir hello ile çakışan.</span><span class="sxs-lookup"><span data-stu-id="f4186-146">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="f4186-147">Merhaba SDK veya herhangi diğer üçüncü bir tarafın temsilci algılarsa, kendi uygulama toogive kullanmayacak sonra bir fırsat tooresolve çakışmaları hello.</span><span class="sxs-lookup"><span data-stu-id="f4186-147">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="f4186-148">Tooadd hello katılım mantığı tooyour tooresolve hello çakışmaları temsilci sırada sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f4186-148">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="f4186-149">Var olan iki yolu tooachieve bu.</span><span class="sxs-lookup"><span data-stu-id="f4186-149">There are two ways tooachieve this.</span></span>

<span data-ttu-id="f4186-150">Teklif 1, temsilciniz ileterek toohello SDK çağırır:</span><span class="sxs-lookup"><span data-stu-id="f4186-150">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="f4186-151">Veya hello devralan tarafından 2, teklif `AEUserNotificationHandler` sınıfı</span><span class="sxs-lookup"><span data-stu-id="f4186-151">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="f4186-152">Bir bildirim geçirerek değil veya katılım üzerinden gelen olup olmadığını belirlemek, `userInfo` sözlük toohello Aracısı `isEngagementPushPayload:` sınıf yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f4186-152">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="f4186-153">Bu hello emin olun `UNUserNotificationCenter` nesnenin temsilci ya da hello içinde tooyour temsilci Ayarla `application:willFinishLaunchingWithOptions:` veya hello `application:didFinishLaunchingWithOptions:` uygulama temsilcinizi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f4186-153">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="f4186-154">Örneğin, Teklif 1 yukarıda hello uygulanırsa:</span><span class="sxs-lookup"><span data-stu-id="f4186-154">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
