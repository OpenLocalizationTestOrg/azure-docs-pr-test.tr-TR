---
title: "Mobile Engagement iOS SDK Yükseltme yordamı aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a><span data-ttu-id="8cce6-103">Yükseltme yordamları</span><span class="sxs-lookup"><span data-stu-id="8cce6-103">Upgrade procedures</span></span>
<span data-ttu-id="8cce6-104">Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.</span><span class="sxs-lookup"><span data-stu-id="8cce6-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="8cce6-105">Hello SDK her yeni sürümü için önce değiştirmeniz gerekir (kaldırın ve yeniden xcode'da içeri aktarın) EngagementSDK ve EngagementReach klasörleri hello.</span><span class="sxs-lookup"><span data-stu-id="8cce6-105">For each new version of hello SDK you must first replace (remove and re-import in xcode) hello EngagementSDK and EngagementReach folders.</span></span>

## <a name="from-300-too400"></a><span data-ttu-id="8cce6-106">3.0.0 gelen too4.0.0</span><span class="sxs-lookup"><span data-stu-id="8cce6-106">From 3.0.0 too4.0.0</span></span>
### <a name="xcode-8"></a><span data-ttu-id="8cce6-107">XCode 8</span><span class="sxs-lookup"><span data-stu-id="8cce6-107">XCode 8</span></span>
<span data-ttu-id="8cce6-108">XCode 8 hello SDK 4.0.0 sürümünden başlayarak zorunludur.</span><span class="sxs-lookup"><span data-stu-id="8cce6-108">XCode 8 is mandatory starting from version 4.0.0 of hello SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="8cce6-109">XCode 7'de gerçekten bağımlı sonra hello kullanabilir [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="8cce6-109">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="8cce6-110">Bir bilinen hata varsa bu önceki sürümünü reach modülünü hello 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir.</span><span class="sxs-lookup"><span data-stu-id="8cce6-110">There is a known bug on hello reach module of this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="8cce6-111">toofix bu tooimplement hello olacaktır API kullanım dışı `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:</span><span class="sxs-lookup"><span data-stu-id="8cce6-111">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="8cce6-112">**Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cce6-112">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="8cce6-113">Mümkün olan en kısa sürede tooXCode 8 geçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="8cce6-113">You should switch tooXCode 8 as soon as possible.</span></span>
> 
> 

### <a name="usernotifications-framework"></a><span data-ttu-id="8cce6-114">UserNotifications framework</span><span class="sxs-lookup"><span data-stu-id="8cce6-114">UserNotifications framework</span></span>
<span data-ttu-id="8cce6-115">Tooadd hello gereksinim `UserNotifications` derleme aşamaları framework.</span><span class="sxs-lookup"><span data-stu-id="8cce6-115">You need tooadd hello `UserNotifications` framework in your Build Phases.</span></span>

<span data-ttu-id="8cce6-116">Merhaba proje Gezgini'nde, proje bölmesini açın ve hello doğru hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="8cce6-116">in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="8cce6-117">Merhaba açın **"Derleme aşamaları"** sekmesi ve hello **"Bağlantı ikiliyi kitaplıklara"** menüsünde framework eklemek `UserNotifications.framework` -kümesi hello bağlantı olarak`Optional`</span><span class="sxs-lookup"><span data-stu-id="8cce6-117">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add framework `UserNotifications.framework` - set hello link as `Optional`</span></span>

### <a name="application-push-capability"></a><span data-ttu-id="8cce6-118">Uygulamayı anında iletme yeteneği</span><span class="sxs-lookup"><span data-stu-id="8cce6-118">Application push capability</span></span>
<span data-ttu-id="8cce6-119">XCode 8 uygulamanızı sıfırlama anında iletme yeteneği, Lütfen çift hello denetleyin `capability` seçilen hedef sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8cce6-119">XCode 8 may reset your app push capability, please double check it in hello `capability` tab of your selected target.</span></span>

### <a name="add-hello-new-ios-10-notification-registration-code"></a><span data-ttu-id="8cce6-120">Merhaba yeni iOS 10 bildirim kayıt kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="8cce6-120">Add hello new iOS 10 notification registration code</span></span>
<span data-ttu-id="8cce6-121">toonotifications hala çalışır ancak kullanıyor hello eski kod parçacığını tooregister hello uygulaması, iOS 10 çalıştırılırken API'leri kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="8cce6-121">hello older code snippet tooregister hello app toonotifications still works but is using deprecated APIs while running on iOS 10.</span></span>

<span data-ttu-id="8cce6-122">İçeri aktarma hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="8cce6-122">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h> 

<span data-ttu-id="8cce6-123">Uygulama temsilcinizi içinde `application:didFinishLaunchingWithOptions` yöntemi Değiştir:</span><span class="sxs-lookup"><span data-stu-id="8cce6-123">In your application delegate `application:didFinishLaunchingWithOptions` method replace:</span></span>

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

<span data-ttu-id="8cce6-124">tarafından:</span><span class="sxs-lookup"><span data-stu-id="8cce6-124">by :</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="8cce6-125">UNUserNotificationCenter temsilci çakışmalarını çözme</span><span class="sxs-lookup"><span data-stu-id="8cce6-125">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="8cce6-126">*Uygulamanızı ya da üçüncü taraf Kitaplıklarınızı biri uygulayan bir `UNUserNotificationCenterDelegate` sonra da bu bölümü atlayabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="8cce6-126">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="8cce6-127">A `UNUserNotificationCenter` temsilci hello SDK toomonitor hello yaşam döngüsü katılım bildirimler iOS 10 veya daha büyük çalıştıran cihazlarda tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8cce6-127">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="8cce6-128">Merhaba SDK sahip hello kendi uyarlamasını `UNUserNotificationCenterDelegate` protokol ancak yalnızca bir olabilir `UNUserNotificationCenter` temsilci uygulama başına.</span><span class="sxs-lookup"><span data-stu-id="8cce6-128">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="8cce6-129">Herhangi bir temsilci eklenen toohello `UNUserNotificationCenter` nesne katılım bir hello ile çakışan.</span><span class="sxs-lookup"><span data-stu-id="8cce6-129">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="8cce6-130">Merhaba SDK veya herhangi diğer üçüncü bir tarafın temsilci algılarsa, kendi uygulama toogive kullanmayacak sonra bir fırsat tooresolve çakışmaları hello.</span><span class="sxs-lookup"><span data-stu-id="8cce6-130">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="8cce6-131">Tooadd hello katılım mantığı tooyour tooresolve hello çakışmaları temsilci sırada sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8cce6-131">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="8cce6-132">Var olan iki yolu tooachieve bu.</span><span class="sxs-lookup"><span data-stu-id="8cce6-132">There are two ways tooachieve this.</span></span>

<span data-ttu-id="8cce6-133">Teklif 1, temsilciniz ileterek toohello SDK çağırır:</span><span class="sxs-lookup"><span data-stu-id="8cce6-133">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="8cce6-134">Veya hello devralan tarafından 2, teklif `AEUserNotificationHandler` sınıfı</span><span class="sxs-lookup"><span data-stu-id="8cce6-134">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="8cce6-135">Bir bildirim geçirerek değil veya katılım üzerinden gelen olup olmadığını belirlemek, `userInfo` sözlük toohello Aracısı `isEngagementPushPayload:` sınıf yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8cce6-135">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="8cce6-136">Bu hello emin olun `UNUserNotificationCenter` nesnenin temsilci ya da hello içinde tooyour temsilci Ayarla `application:willFinishLaunchingWithOptions:` veya hello `application:didFinishLaunchingWithOptions:` uygulama temsilcinizi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8cce6-136">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="8cce6-137">Örneğin, Teklif 1 yukarıda hello uygulanırsa:</span><span class="sxs-lookup"><span data-stu-id="8cce6-137">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a><span data-ttu-id="8cce6-138">2.0.0 gelen too3.0.0</span><span class="sxs-lookup"><span data-stu-id="8cce6-138">From 2.0.0 too3.0.0</span></span>
<span data-ttu-id="8cce6-139">İOS için destek bırakılan 4.X.</span><span class="sxs-lookup"><span data-stu-id="8cce6-139">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="8cce6-140">Bu sürüm hello dağıtım hedefi, uygulamanızın başlangıç olmalıdır en az iOS 6.</span><span class="sxs-lookup"><span data-stu-id="8cce6-140">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

<span data-ttu-id="8cce6-141">Reach uygulamanızda kullanıyorsanız, eklemelisiniz `remote-notification` değeri toohello `UIBackgroundModes` Info.plist dosyanızdaki sipariş tooreceive uzak bildirimler dizisinde.</span><span class="sxs-lookup"><span data-stu-id="8cce6-141">If you are using Reach in your application, you must add `remote-notification` value toohello `UIBackgroundModes` array in your Info.plist file in order tooreceive remote notifications.</span></span>

<span data-ttu-id="8cce6-142">Merhaba yöntemi `application:didReceiveRemoteNotification:` değiştirilmiştir toobe gereken `application:didReceiveRemoteNotification:fetchCompletionHandler:` uygulama temsilcinizi içinde.</span><span class="sxs-lookup"><span data-stu-id="8cce6-142">hello method `application:didReceiveRemoteNotification:` needs toobe replaced by `application:didReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate.</span></span>

<span data-ttu-id="8cce6-143">"AEPushDelegate.h" kullanım dışı arabirimi ve tüm başvuruları tooremove gerekir.</span><span class="sxs-lookup"><span data-stu-id="8cce6-143">"AEPushDelegate.h" is deprecated interface and you need tooremove all references.</span></span> <span data-ttu-id="8cce6-144">Bu kaldırma içerir `[[EngagementAgent shared] setPushDelegate:self]` ve uygulama temsilcinizi yöntemleri temsilci hello:</span><span class="sxs-lookup"><span data-stu-id="8cce6-144">This includes removing `[[EngagementAgent shared] setPushDelegate:self]` and hello delegate methods from your application delegate:</span></span>

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a><span data-ttu-id="8cce6-145">1.16.0 gelen too2.0.0</span><span class="sxs-lookup"><span data-stu-id="8cce6-145">From 1.16.0 too2.0.0</span></span>
<span data-ttu-id="8cce6-146">Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8cce6-146">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span>
<span data-ttu-id="8cce6-147">Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too1.16 ilk başvurun sonra hello aşağıdaki yordamı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="8cce6-147">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.16 first then apply hello following procedure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cce6-148">Capptain ve Mobile Engagement olan değil hello aynı Hizmetleri ve yalnızca aşağıda verilen hello yordamı nasıl toomigrate hello istemci uygulamaları vurgular.</span><span class="sxs-lookup"><span data-stu-id="8cce6-148">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="8cce6-149">Geçirme hello SDK hello uygulama hello Capptain sunucuları toohello Mobile Engagement sunuculardan veri geçişi YAPILMAZ</span><span class="sxs-lookup"><span data-stu-id="8cce6-149">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

### <a name="agent"></a><span data-ttu-id="8cce6-150">Aracı</span><span class="sxs-lookup"><span data-stu-id="8cce6-150">Agent</span></span>
<span data-ttu-id="8cce6-151">Merhaba yöntemi `registerApp:` hello yeni yöntemi tarafından değiştirildiğini `init:`.</span><span class="sxs-lookup"><span data-stu-id="8cce6-151">hello method `registerApp:` has been replaced by hello new method `init:`.</span></span> <span data-ttu-id="8cce6-152">Uygulama temsilcinizi uygun şekilde güncelleştirilmesi gerekir ve bağlantı dizesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="8cce6-152">Your application delegate must be updated accordingly and use connection string:</span></span>

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

<span data-ttu-id="8cce6-153">SmartAd izleme yalnızca gerekir tooremove tüm örneklerini SDK'dan kaldırıldı `AETrackModule` sınıfı</span><span class="sxs-lookup"><span data-stu-id="8cce6-153">SmartAd tracking has been removed from SDK you just have tooremove all instances of `AETrackModule` class</span></span>

### <a name="class-name-changes"></a><span data-ttu-id="8cce6-154">Sınıf adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="8cce6-154">Class Name Changes</span></span>
<span data-ttu-id="8cce6-155">Merhaba rebranding bir parçası olarak değiştirilen toobe gereken sınıf/dosya adları birkaç vardır.</span><span class="sxs-lookup"><span data-stu-id="8cce6-155">As part of hello rebranding, there are couple of class/file names that need toobe changed.</span></span>

<span data-ttu-id="8cce6-156">Tüm sınıflar "CP" öneki "AE" önekiyle adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8cce6-156">All classes prefixed with "CP" are renamed with "AE" prefix.</span></span>

<span data-ttu-id="8cce6-157">Örnek:</span><span class="sxs-lookup"><span data-stu-id="8cce6-157">Example:</span></span>

* <span data-ttu-id="8cce6-158">`CPModule.h`çok adlandırılır`AEModule.h`.</span><span class="sxs-lookup"><span data-stu-id="8cce6-158">`CPModule.h` is renamed too`AEModule.h`.</span></span>

<span data-ttu-id="8cce6-159">Tüm sınıflar "İle Capptain" öneki "Katılım" önekiyle adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="8cce6-159">All classes prefixed with "Capptain" are renamed with "Engagement" prefix.</span></span>

<span data-ttu-id="8cce6-160">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="8cce6-160">Examples:</span></span>

* <span data-ttu-id="8cce6-161">Merhaba sınıfı `CapptainAgent` çok adlandırılır`EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="8cce6-161">hello class `CapptainAgent` is renamed too`EngagementAgent`.</span></span>
* <span data-ttu-id="8cce6-162">Merhaba sınıfı `CapptainTableViewController` çok adlandırılır`EngagementTableViewController`.</span><span class="sxs-lookup"><span data-stu-id="8cce6-162">hello class `CapptainTableViewController` is renamed too`EngagementTableViewController`.</span></span>
* <span data-ttu-id="8cce6-163">Merhaba sınıfı `CapptainUtils` çok adlandırılır`EngagementUtils`.</span><span class="sxs-lookup"><span data-stu-id="8cce6-163">hello class `CapptainUtils` is renamed too`EngagementUtils`.</span></span>
* <span data-ttu-id="8cce6-164">Merhaba sınıfı `CapptainViewController` çok adlandırılır`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="8cce6-164">hello class `CapptainViewController` is renamed too`EngagementViewController`.</span></span>

