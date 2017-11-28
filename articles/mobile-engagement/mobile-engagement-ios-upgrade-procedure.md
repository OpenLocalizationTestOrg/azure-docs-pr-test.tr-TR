---
title: "Azure Mobile Engagement iOS SDK Yükseltme yordamı | Microsoft Docs"
description: "En son güncelleştirmeler ve iOS için Azure Mobile Engagement SDK'sı için yordamlar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 37c7f133d079186f828d58cabce0d2a259efd085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="2a87e-103">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="2a87e-103">Upgrade procedures</span></span>
<span data-ttu-id="2a87e-104">Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz, SDK'yı yükseltirken aşağıdaki noktaları dikkate almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a87e-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="2a87e-105">SDK'sı için her yeni sürümü, ilk değiştirmeniz gerekir (kaldırın ve yeniden xcode'da içeri aktarın) EngagementSDK ve EngagementReach klasörler.</span><span class="sxs-lookup"><span data-stu-id="2a87e-105">For each new version of the SDK you must first replace (remove and re-import in xcode) the EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-to-400"></a><span data-ttu-id="2a87e-106">3.0.0 4.0.0 için</span><span class="sxs-lookup"><span data-stu-id="2a87e-106">From 3.0.0 to 4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="2a87e-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="2a87e-107">XCode 8</span></span>
<span data-ttu-id="2a87e-108">XCode 8 SDK 4.0.0 sürümünden başlayarak zorunludur.</span><span class="sxs-lookup"><span data-stu-id="2a87e-108">XCode 8 is mandatory starting from version 4.0.0 of the SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="2a87e-109">XCode 7'de gerçekten bağımlı sonra kullanabilirsiniz [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="2a87e-109">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="2a87e-110">Bir bilinen hata varsa bu önceki sürüm reach modülünü 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir.</span><span class="sxs-lookup"><span data-stu-id="2a87e-110">There is a known bug on the reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="2a87e-111">Bu kullanım dışı API uygulamak için olacaktır sorunu gidermek için `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:</span><span class="sxs-lookup"><span data-stu-id="2a87e-111">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="2a87e-112">**Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a87e-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="2a87e-113">Mümkün olan en kısa sürede XCode 8'e geçer.</span><span class="sxs-lookup"><span data-stu-id="2a87e-113">You should switch to XCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="2a87e-114">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="2a87e-114">UserNotifications framework</span></span>
<span data-ttu-id="2a87e-115">Eklemenize gerek `UserNotifications` derleme aşamaları framework.</span><span class="sxs-lookup"><span data-stu-id="2a87e-115">You need to add the `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="2a87e-116">Proje Gezgini'nde, proje bölmesini açın ve doğru hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="2a87e-116">in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="2a87e-117">Ardından, açın **"Derleme aşamaları"** sekmesi ve **"Bağlantı ikiliyi kitaplıklara"** menüsünde framework eklemek `UserNotifications.framework` -bağlantı olarak ayarlayın`Optional`</span><span class="sxs-lookup"><span data-stu-id="2a87e-117">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set the link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="2a87e-118">Uygulamayı anında iletme yeteneği</span><span class="sxs-lookup"><span data-stu-id="2a87e-118">Application push capability</span></span>
<span data-ttu-id="2a87e-119">XCode 8 uygulamanızı sıfırlama anında iletme yeteneği, lütfen tekrar gözden geçirin `capability` seçilen hedef sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2a87e-119">XCode 8 may reset your app push capability, please double check it in the `capability` tab of your selected target.</span></span>

### <a name="add-the-new-ios-10-notification-registration-code"></a><span data-ttu-id="2a87e-120">Yeni iOS 10 bildirim kayıt kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="2a87e-120">Add the new iOS 10 notification registration code</span></span>
<span data-ttu-id="2a87e-121">Uygulama bildirimleri kaydetmek için eski kod parçacığını hala çalışır ancak iOS 10 çalıştırılırken kullanım dışı API'lerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="2a87e-121">The older code snippet to register the app to notifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="2a87e-122">İçeri aktarma `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="2a87e-122">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="2a87e-123">Uygulama temsilcinizi içinde `application:didFinishLaunchingWithOptions` yöntemi Değiştir:</span><span class="sxs-lookup"><span data-stu-id="2a87e-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="2a87e-124">tarafından:</span><span class="sxs-lookup"><span data-stu-id="2a87e-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="2a87e-125">UNUserNotificationCenter temsilci çakışmalarını çözme</span><span class="sxs-lookup"><span data-stu-id="2a87e-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="2a87e-126">*Uygulamanızı ya da üçüncü taraf Kitaplıklarınızı biri uygulayan bir `UNUserNotificationCenterDelegate` sonra da bu bölümü atlayabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="2a87e-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="2a87e-127">A `UNUserNotificationCenter` temsilci SDK tarafından katılım bildirimleri 10 veya daha büyük iOS çalıştıran cihazlarda yaşam döngüsünü izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2a87e-127">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="2a87e-128">SDK, kendi uygulamanızda `UNUserNotificationCenterDelegate` protokol ancak yalnızca bir olabilir `UNUserNotificationCenter` temsilci uygulama başına.</span><span class="sxs-lookup"><span data-stu-id="2a87e-128">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="2a87e-129">Eklenen herhangi bir temsilci `UNUserNotificationCenter` nesne katılım bir çakışma.</span><span class="sxs-lookup"><span data-stu-id="2a87e-129">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="2a87e-130">SDK veya herhangi diğer üçüncü bir tarafın temsilci algılarsa sonra kendi uygulama çakışmaları olanağı vermek için kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="2a87e-130">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="2a87e-131">Çakışmaları çözümlemek amacıyla kendi temsilciye katılım mantığı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a87e-131">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="2a87e-132">Bunu başarmak için iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="2a87e-132">There are two ways to achieve this.</span></span>

<span data-ttu-id="2a87e-133">SDK çağrıları temsilciniz iletme tarafından yalnızca 1, Teklif:</span><span class="sxs-lookup"><span data-stu-id="2a87e-133">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="2a87e-134">Veya içinden devralma tarafından 2, teklif `AEUserNotificationHandler` sınıfı</span><span class="sxs-lookup"><span data-stu-id="2a87e-134">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="2a87e-135">Bir bildirim geçirerek değil veya katılım üzerinden gelen olup olmadığını belirlemek, `userInfo` aracı sözlüğe `isEngagementPushPayload:` sınıf yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2a87e-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="2a87e-136">Olduğundan emin olun `UNUserNotificationCenter` nesnenin temsilci temsilciniz ya da içinde ayarlanmış `application:willFinishLaunchingWithOptions:` veya `application:didFinishLaunchingWithOptions:` uygulama temsilcinizi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2a87e-136">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="2a87e-137">Örneğin, yukarıdaki teklifi 1 uygulanırsa:</span><span class="sxs-lookup"><span data-stu-id="2a87e-137">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-to-300"></a><span data-ttu-id="2a87e-138">2.0.0 3.0.0 için</span><span class="sxs-lookup"><span data-stu-id="2a87e-138">From 2.0.0 to 3.0.0</span></span>
<span data-ttu-id="2a87e-139">İOS için destek bırakılan 4.X.</span><span class="sxs-lookup"><span data-stu-id="2a87e-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="2a87e-140">Uygulamanızın dağıtım hedef bu sürümünden başlayarak olmalıdır en az iOS 6.</span><span class="sxs-lookup"><span data-stu-id="2a87e-140">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="2a87e-141">Reach uygulamanızda kullanıyorsanız, eklemelisiniz `remote-notification` değeri `UIBackgroundModes` dizi Info.plist dosyanızdaki uzak bildirimleri almak için.</span><span class="sxs-lookup"><span data-stu-id="2a87e-141">If you are using Reach in your application, you must add `remote-notification` value to the `UIBackgroundModes` array in your Info.plist file in order to receive remote notifications.</span></span>

<span data-ttu-id="2a87e-142">Yöntem `application:didReceiveRemoteNotification:` tarafından değiştirilmesi gereken `application:didReceiveRemoteNotification:fetchCompletionHandler:` uygulama temsilcinizi içinde.</span><span class="sxs-lookup"><span data-stu-id="2a87e-142">The method `application:didReceiveRemoteNotification:` needs to be replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="2a87e-143">"AEPushDelegate.h" kullanım dışı arabirimi ve tüm başvurularını kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a87e-143">"AEPushDelegate.h" is deprecated interface and you need to remove all references.</span></span> <span data-ttu-id="2a87e-144">Bu kaldırma içerir `[[EngagementAgent shared] setPushDelegate:self]` ve uygulama temsilcinizi temsilci yöntemleri:</span><span class="sxs-lookup"><span data-stu-id="2a87e-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and the delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-to-200"></a><span data-ttu-id="2a87e-145">1.16.0 2.0.0 için</span><span class="sxs-lookup"><span data-stu-id="2a87e-145">From 1.16.0 to 2.0.0</span></span>
<span data-ttu-id="2a87e-146">Aşağıdaki nasıl Azure Mobile Engagement tarafından desteklenen bir uygulamaya Capptain SAS tarafından sunulan Capptain hizmetinden bir SDK tümleştirmesi geçirileceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2a87e-146">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="2a87e-147">Önceki bir sürümünden geçiş yapıyorsanız, Lütfen 1.16 için önce geçirmenizi sonra aşağıdaki yordamı uygulamak için Capptain web sitesine bakın.</span><span class="sxs-lookup"><span data-stu-id="2a87e-147">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.16 first then apply the following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a87e-148">Capptain ve Mobile Engagement aynı Hizmetleri değildir ve aşağıda verilen yordamı yalnızca istemci uygulaması geçirmek nasıl vurgular.</span><span class="sxs-lookup"><span data-stu-id="2a87e-148">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="2a87e-149">Uygulama SDK'yı geçirme verilerinizi Capptain sunucularından Mobile Engagement sunucuya geçişi YAPILMAZ</span><span class="sxs-lookup"><span data-stu-id="2a87e-149">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="2a87e-150">Aracı</span><span class="sxs-lookup"><span data-stu-id="2a87e-150">Agent</span></span>
<span data-ttu-id="2a87e-151">Yöntem `registerApp:` yeni yöntemi tarafından değiştirildiğini `init:`.</span><span class="sxs-lookup"><span data-stu-id="2a87e-151">The method `registerApp:` has been replaced by the new method `init:`.</span></span> <span data-ttu-id="2a87e-152">Uygulama temsilcinizi uygun şekilde güncelleştirilmesi gerekir ve bağlantı dizesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="2a87e-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="2a87e-153">SmartAd izleme yalnızca sahip tüm örneklerini kaldırmak için SDK'dan kaldırıldı `AETrackModule` sınıfı</span><span class="sxs-lookup"><span data-stu-id="2a87e-153">SmartAd tracking has been removed from SDK you just have to remove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="2a87e-154">Sınıf adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="2a87e-154">Class Name Changes</span></span>
<span data-ttu-id="2a87e-155">Rebranding bir parçası olarak değiştirilmesi gereken sınıf/dosya adları birkaç vardır.</span><span class="sxs-lookup"><span data-stu-id="2a87e-155">As part of the rebranding, there are couple of class/file names that need to be changed.</span></span>

<span data-ttu-id="2a87e-156">Tüm sınıflar "CP" öneki "AE" önekiyle adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="2a87e-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="2a87e-157">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2a87e-157">Example:</span></span>

* <span data-ttu-id="2a87e-158">`CPModule.h`yeniden adlandırılır `AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="2a87e-158">`CPModule.h` is renamed to `AEModule.h`.</span></span>

<span data-ttu-id="2a87e-159">Tüm sınıflar "İle Capptain" öneki "Katılım" önekiyle adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="2a87e-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="2a87e-160">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="2a87e-160">Examples:</span></span>

* <span data-ttu-id="2a87e-161">Sınıf `CapptainAgent` adlandırılır `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="2a87e-161">The class `CapptainAgent` is renamed to `EngagementAgent`.</span></span>
* <span data-ttu-id="2a87e-162">Sınıf `CapptainTableViewController` adlandırılır `EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="2a87e-162">The class `CapptainTableViewController` is renamed to `EngagementTableViewController`.</span></span>
* <span data-ttu-id="2a87e-163">Sınıf `CapptainUtils` adlandırılır `EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="2a87e-163">The class `CapptainUtils` is renamed to `EngagementUtils`.</span></span>
* <span data-ttu-id="2a87e-164">Sınıf `CapptainViewController` adlandırılır `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="2a87e-164">The class `CapptainViewController` is renamed to `EngagementViewController`.</span></span>

