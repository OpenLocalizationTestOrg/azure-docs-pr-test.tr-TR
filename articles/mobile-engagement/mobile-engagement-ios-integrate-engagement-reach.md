---
title: "Mobile Engagement iOS SDK tümleştirmesi ulaşmak aaaAzure | Microsoft Docs"
description: "En son güncelleştirmeler ve iOS için Azure Mobile Engagement SDK'sı için yordamlar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a><span data-ttu-id="3019e-103">TooIntegrate Engagement Reach nasıl iOS</span><span class="sxs-lookup"><span data-stu-id="3019e-103">How tooIntegrate Engagement Reach on iOS</span></span>
<span data-ttu-id="3019e-104">Merhaba tümleştirme hello yordamını izleyin [nasıl tooIntegrate Engagement iOS belgesinde](mobile-engagement-ios-integrate-engagement.md) bu kılavuz aşağıdaki önce.</span><span class="sxs-lookup"><span data-stu-id="3019e-104">You must follow hello integration procedure described in hello [How tooIntegrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="3019e-105">Bu belge, XCode 8 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3019e-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="3019e-106">XCode 7'de gerçekten bağımlı sonra hello kullanabilir [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="3019e-106">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="3019e-107">Bir bilinen hata varsa bu önceki sürüm 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir.</span><span class="sxs-lookup"><span data-stu-id="3019e-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="3019e-108">toofix bu tooimplement hello olacaktır API kullanım dışı `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:</span><span class="sxs-lookup"><span data-stu-id="3019e-108">toofix this you will have tooimplement hello deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="3019e-109">**Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3019e-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="3019e-110">Mümkün olan en kısa sürede tooXCode 8 geçmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="3019e-110">You should switch tooXCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a><span data-ttu-id="3019e-111">Uygulama tooreceive sessiz anında iletme bildirimlerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3019e-111">Enable your app tooreceive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="3019e-112">Tümleştirme adımları</span><span class="sxs-lookup"><span data-stu-id="3019e-112">Integration steps</span></span>
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="3019e-113">Merhaba Engagement Reach SDK'sı iOS projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="3019e-113">Embed hello Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="3019e-114">Merhaba Reach SDK'sını Xcode projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3019e-114">Add hello Reach sdk in your Xcode project.</span></span> <span data-ttu-id="3019e-115">Xcode'da, çok Git**proje \> tooproject ekleme** ve hello seçin `EngagementReach` klasör.</span><span class="sxs-lookup"><span data-stu-id="3019e-115">In Xcode, go too**Project \> Add tooproject** and choose hello `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="3019e-116">Uygulama Temsilcinizi değiştirme</span><span class="sxs-lookup"><span data-stu-id="3019e-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="3019e-117">Uygulama dosyanızı Hello üstünde hello Engagement Reach modülünü içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="3019e-117">At hello top of your implementation file, import hello Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="3019e-118">Yöntemi içinde `applicationDidFinishLaunching:` veya `application:didFinishLaunchingWithOptions:`, bir reach modülü oluşturun ve tooyour mevcut Engagement başlatma satır geçirme:</span><span class="sxs-lookup"><span data-stu-id="3019e-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it tooyour existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="3019e-119">Değiştirme **'icon.png'** dize bildirim simgesi olarak istediğiniz hello görüntü adı ile.</span><span class="sxs-lookup"><span data-stu-id="3019e-119">Modify **'icon.png'** string with hello image name you want as your notification icon.</span></span>
* <span data-ttu-id="3019e-120">Toouse hello seçenek istiyorsanız *güncelleştirme rozet değeri* Reach kampanyaları veya toouse yerel gönderim isteyip istemediğinizi \<SaaS/Reach API'sini/Kampanya biçimi/yerel anında iletme\> kampanyalar, hello Reach modülünün yönetmenize izin gerekir (bunu hello uygulama gösterge otomatik olarak temizlemek ve ayrıca başlatılmadı veya foregrounded hello uygulama her zaman Engagement tarafından depolanan hello değerini sıfırlamak) hello rozet simgesi kendisi.</span><span class="sxs-lookup"><span data-stu-id="3019e-120">If you want toouse hello option *Update badge value* in Reach campaigns or if you want toouse native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let hello Reach module manage hello badge icon itself (it will automatically clear hello application badge and also reset hello value stored by Engagement every time hello application is started or foregrounded).</span></span> <span data-ttu-id="3019e-121">Bu satırı Reach modülü başlatma sonra aşağıdaki hello ekleyerek yapılır:</span><span class="sxs-lookup"><span data-stu-id="3019e-121">This is done by adding hello following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="3019e-122">Toohandle Reach veri gönderimi istiyorsanız, uygulama temsilcinizi toohello uygun izin vermelisiniz `AEReachDataPushDelegate` protokolü.</span><span class="sxs-lookup"><span data-stu-id="3019e-122">If you want toohandle Reach data push, you must let your Application delegate conform toohello `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="3019e-123">Satır Reach modülü başlatma sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3019e-123">Add hello following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="3019e-124">Merhaba yöntemleri uygulayabilirsiniz sonra `onDataPushStringReceived:` ve `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` uygulama temsilcinizi içinde:</span><span class="sxs-lookup"><span data-stu-id="3019e-124">Then you can implement hello methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a><span data-ttu-id="3019e-125">Kategori</span><span class="sxs-lookup"><span data-stu-id="3019e-125">Category</span></span>
<span data-ttu-id="3019e-126">Merhaba kategori parametresi bir veri gönderme kampanya oluşturduğunuzda isteğe bağlıdır ve toofilter verileri iter sağlar.</span><span class="sxs-lookup"><span data-stu-id="3019e-126">hello category parameter is optional when you create a Data Push campaign and allows you toofilter data pushes.</span></span> <span data-ttu-id="3019e-127">Toopush farklı tür istiyorsanız kullanışlıdır, `Base64` veri ve istediğiniz tooidentify bunları ayrıştırma önce kendi türü.</span><span class="sxs-lookup"><span data-stu-id="3019e-127">This is useful if you want toopush different kinds of `Base64` data and want tooidentify their type before parsing them.</span></span>

<span data-ttu-id="3019e-128">**Hazır tooreceive ve görüntü içeriğini ulaşmak şimdi uygulamanızı değil!**</span><span class="sxs-lookup"><span data-stu-id="3019e-128">**Your application is now ready tooreceive and display reach contents!**</span></span>

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a><span data-ttu-id="3019e-129">Nasıl tooreceive duyuruları ve yoklamaları herhangi bir zamanda</span><span class="sxs-lookup"><span data-stu-id="3019e-129">How tooreceive announcements and polls at any time</span></span>
<span data-ttu-id="3019e-130">Engagement Reach bildirim tooyour son kullanıcıların herhangi bir zamanda hello Apple anında iletilen bildirim Servisi'ni kullanarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3019e-130">Engagement can send Reach notifications tooyour end users at any time by using hello Apple Push Notification Service.</span></span>

<span data-ttu-id="3019e-131">tooenable bu işlevselliği Apple anında iletme bildirimleri için uygulamanızı tooprepare varsa ve uygulama temsilcinizi değiştirme.</span><span class="sxs-lookup"><span data-stu-id="3019e-131">tooenable this functionality, you'll have tooprepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="3019e-132">Uygulamanızın Apple anında iletme bildirimleri için hazırlama</span><span class="sxs-lookup"><span data-stu-id="3019e-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="3019e-133">Lütfen başlangıç kılavuzunu izleyin: [nasıl tooPrepare uygulamanız için Apple anında iletme bildirimleri](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="3019e-133">Please follow hello guide : [How tooPrepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-hello-necessary-client-code"></a><span data-ttu-id="3019e-134">Merhaba gerekli istemci kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="3019e-134">Add hello necessary client code</span></span>
<span data-ttu-id="3019e-135">*Bu noktada, uygulamanızın kayıtlı bir Apple anında iletme sertifika hello katılım ön ucunda olması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="3019e-135">*At this point your application should have a registered Apple push certificate in hello Engagement frontend.*</span></span>

<span data-ttu-id="3019e-136">Henüz yapmadıysanız, uygulama tooreceive anında iletme bildirimleri tooregister gerekir.</span><span class="sxs-lookup"><span data-stu-id="3019e-136">If it's not done already, you need tooregister your application tooreceive push notifications.</span></span>

* <span data-ttu-id="3019e-137">İçeri aktarma hello `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="3019e-137">Import hello `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="3019e-138">Uygulamanız başladığında satır aşağıdaki hello ekleyin (genellikle, `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="3019e-138">Add hello following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="3019e-139">Ardından, tooprovide tooEngagement hello cihaz belirteci Apple sunucuları tarafından döndürülen gerekir.</span><span class="sxs-lookup"><span data-stu-id="3019e-139">Then, You need tooprovide tooEngagement hello device token returned by Apple servers.</span></span> <span data-ttu-id="3019e-140">Bu adlı hello yönteminde yapılır `application:didRegisterForRemoteNotificationsWithDeviceToken:` uygulama temsilcinizi içinde:</span><span class="sxs-lookup"><span data-stu-id="3019e-140">This is done in hello method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="3019e-141">Son olarak, uygulamanızın uzak bir bildirim aldığında tooinform hello Engagement SDK'sı olması.</span><span class="sxs-lookup"><span data-stu-id="3019e-141">Finally, you have tooinform hello Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="3019e-142">çağrı, toodo hello yöntemi `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` uygulama temsilcinizi içinde:</span><span class="sxs-lookup"><span data-stu-id="3019e-142">toodo that, call hello method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="3019e-143">Varsayılan olarak, Engagement Reach hello completionHandler denetler.</span><span class="sxs-lookup"><span data-stu-id="3019e-143">By default, Engagement Reach controls hello completionHandler.</span></span> <span data-ttu-id="3019e-144">Toomanually yanıt toohello istiyorsanız `handler` kodunuzda engellemek, hello nil geçirebilirsiniz `handler` bağımsız değişkeni ve denetim hello tamamlama kendiniz engelleyin.</span><span class="sxs-lookup"><span data-stu-id="3019e-144">If you want toomanually respond toohello `handler` block in your code, you can pass nil for hello `handler` argument and control hello completion block yourself.</span></span> <span data-ttu-id="3019e-145">Merhaba bkz `UIBackgroundFetchResult` olası değerler listesi türü.</span><span class="sxs-lookup"><span data-stu-id="3019e-145">See hello `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="3019e-146">Tam örnek</span><span class="sxs-lookup"><span data-stu-id="3019e-146">Full example</span></span>
<span data-ttu-id="3019e-147">Tümleştirme tam bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3019e-147">Here is a full example of integration:</span></span>

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="3019e-148">UNUserNotificationCenter temsilci çakışmalarını çözme</span><span class="sxs-lookup"><span data-stu-id="3019e-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="3019e-149">*Uygulamanızı ya da üçüncü taraf Kitaplıklarınızı biri uygulayan bir `UNUserNotificationCenterDelegate` sonra da bu bölümü atlayabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="3019e-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="3019e-150">A `UNUserNotificationCenter` temsilci hello SDK toomonitor hello yaşam döngüsü katılım bildirimler iOS 10 veya daha büyük çalıştıran cihazlarda tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3019e-150">A `UNUserNotificationCenter` delegate is used by hello SDK toomonitor hello life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="3019e-151">Merhaba SDK sahip hello kendi uyarlamasını `UNUserNotificationCenterDelegate` protokol ancak yalnızca bir olabilir `UNUserNotificationCenter` temsilci uygulama başına.</span><span class="sxs-lookup"><span data-stu-id="3019e-151">hello SDK has its own implementation of hello `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="3019e-152">Herhangi bir temsilci eklenen toohello `UNUserNotificationCenter` nesne katılım bir hello ile çakışan.</span><span class="sxs-lookup"><span data-stu-id="3019e-152">Any other delegate added toohello `UNUserNotificationCenter` object will conflict with hello Engagement one.</span></span> <span data-ttu-id="3019e-153">Merhaba SDK veya herhangi diğer üçüncü bir tarafın temsilci algılarsa, kendi uygulama toogive kullanmayacak sonra bir fırsat tooresolve çakışmaları hello.</span><span class="sxs-lookup"><span data-stu-id="3019e-153">If hello SDK detects your or any other third party's delegate then it will not use its own implementation toogive you a chance tooresolve hello conflicts.</span></span> <span data-ttu-id="3019e-154">Tooadd hello katılım mantığı tooyour tooresolve hello çakışmaları temsilci sırada sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3019e-154">You will have tooadd hello Engagement logic tooyour own delegate in order tooresolve hello conflicts.</span></span>

<span data-ttu-id="3019e-155">Var olan iki yolu tooachieve bu.</span><span class="sxs-lookup"><span data-stu-id="3019e-155">There are two ways tooachieve this.</span></span>

<span data-ttu-id="3019e-156">Teklif 1, temsilciniz ileterek toohello SDK çağırır:</span><span class="sxs-lookup"><span data-stu-id="3019e-156">Proposal 1, simply by forwarding your delegate calls toohello SDK:</span></span>

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

<span data-ttu-id="3019e-157">Veya hello devralan tarafından 2, teklif `AEUserNotificationHandler` sınıfı</span><span class="sxs-lookup"><span data-stu-id="3019e-157">Or proposal 2, by inheriting from hello `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="3019e-158">Bir bildirim geçirerek değil veya katılım üzerinden gelen olup olmadığını belirlemek, `userInfo` sözlük toohello Aracısı `isEngagementPushPayload:` sınıf yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3019e-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary toohello Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="3019e-159">Bu hello emin olun `UNUserNotificationCenter` nesnenin temsilci ya da hello içinde tooyour temsilci Ayarla `application:willFinishLaunchingWithOptions:` veya hello `application:didFinishLaunchingWithOptions:` uygulama temsilcinizi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3019e-159">Make sure that hello `UNUserNotificationCenter` object's delegate is set tooyour delegate within either hello `application:willFinishLaunchingWithOptions:` or hello `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="3019e-160">Örneğin, Teklif 1 yukarıda hello uygulanırsa:</span><span class="sxs-lookup"><span data-stu-id="3019e-160">For instance, if you implemented hello above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a><span data-ttu-id="3019e-161">Nasıl toocustomize Kampanyalar</span><span class="sxs-lookup"><span data-stu-id="3019e-161">How toocustomize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="3019e-162">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="3019e-162">Notifications</span></span>
<span data-ttu-id="3019e-163">Bildirimler iki tür vardır: Sistem ve uygulama içi bildirimler.</span><span class="sxs-lookup"><span data-stu-id="3019e-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="3019e-164">Sistem bildirimleri iOS tarafından işlenir ve özelleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="3019e-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="3019e-165">Uygulama bildirimleri toohello geçerli uygulama penceresi dinamik olarak eklenen bir görünümünü yapılır.</span><span class="sxs-lookup"><span data-stu-id="3019e-165">In-app notifications are made of a view that is dynamically added toohello current application window.</span></span> <span data-ttu-id="3019e-166">Bu bildirim bir katmana çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3019e-166">This is called a notification overlay.</span></span> <span data-ttu-id="3019e-167">Uygulamanız herhangi bir görünümde, toomodify bunlar gerekli olmadığı için bildirim yer paylaşımları hızlı tümleştirme için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="3019e-167">Notification overlays are great for a fast integration because they does not require you toomodify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="3019e-168">Düzen</span><span class="sxs-lookup"><span data-stu-id="3019e-168">Layout</span></span>
<span data-ttu-id="3019e-169">Uygulama bildirimlerinizi toomodify hello görünümünü, yalnızca değiştirebileceğiniz hello dosya `AENotificationView.xib` hello etiket değerlerini ve hello varolan subviews türleri tutmak sürece tooyour gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3019e-169">toomodify hello look of your in-app notifications, you can simply modify hello file `AENotificationView.xib` tooyour needs, as long as you keep hello tag values and types of hello existing subviews.</span></span>

<span data-ttu-id="3019e-170">Varsayılan olarak, uygulama içi bildirimler hello ekranın hello altında sunulur.</span><span class="sxs-lookup"><span data-stu-id="3019e-170">By default, in-app notifications are presented at hello bottom of hello screen.</span></span> <span data-ttu-id="3019e-171">Toodisplay tercih ederseniz, bunları ekran, düzenleme hello hello üstündeki sağlanan `AENotificationView.xib` hello değiştirip `AutoSizing` kendi değerlendirmesi hello üstünde tutulabilir şekilde hello ana görünüm özelliği.</span><span class="sxs-lookup"><span data-stu-id="3019e-171">If you prefer toodisplay them at hello top of screen, edit hello provided `AENotificationView.xib` and change hello `AutoSizing` property of hello main view so it can be kept at hello top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="3019e-172">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="3019e-172">Categories</span></span>
<span data-ttu-id="3019e-173">Düzen sağlanan hello değiştirdiğinizde, tüm bildirimlerinizi hello görünümünü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3019e-173">When you modify hello provided layout, you modify hello look of all your notifications.</span></span> <span data-ttu-id="3019e-174">Çeşitli hedeflenen toodefine (büyük olasılıkla davranışları) bildirimleri için görünür kategoriler.</span><span class="sxs-lookup"><span data-stu-id="3019e-174">Categories allow you toodefine various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="3019e-175">Bir kategori Reach kampanya oluşturduğunuzda belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="3019e-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="3019e-176">Bu belgenin sonraki bölümlerinde açıklanan kategoriler de duyuruları ve yoklamaları, özelleştirmenize olanak tanır olduğunu aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="3019e-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="3019e-177">tooregister bildirimlerinizi için bir kategori işleyici, hello modülü ulaştığınızda bir çağrı başlatılmış tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="3019e-177">tooregister a category handler for your notifications, you need tooadd a call once hello reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="3019e-178">`myNotifier`toohello Protokolü uyan bir nesne örneği olmalıdır `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="3019e-178">`myNotifier` must be an instance of an object that conforms toohello protocol `AENotifier`.</span></span>

<span data-ttu-id="3019e-179">Kendi kendinize hello Protokolü yöntemleri uygulayabilirsiniz veya tooreimplement hello varolan sınıf seçebilir `AEDefaultNotifier` hello çalışmanın çoğu zaten gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="3019e-179">You can implement hello protocol methods by yourself or you can choose tooreimplement hello existing class `AEDefaultNotifier` which already performs most of hello work.</span></span>

<span data-ttu-id="3019e-180">Örneğin, belirli bir kategorideki için tooredefine hello bildirim görünümü istiyorsanız, bu örnek izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3019e-180">For example, if you want tooredefine hello notification view for a specific category, you can follow this example:</span></span>

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

<span data-ttu-id="3019e-181">Bu basit örnek kategorisinin varsayalım adında bir dosyanız varsa `MyNotificationView.xib` ana uygulama paket içindeki.</span><span class="sxs-lookup"><span data-stu-id="3019e-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="3019e-182">Merhaba yöntemi karşılık gelen mümkün toofind değilse `.xib`hello bildirim görüntülenmez ve katılım hello konsolunda bir ileti çıktı.</span><span class="sxs-lookup"><span data-stu-id="3019e-182">If hello method is not able toofind a corresponding `.xib`, hello notification will not be displayed and Engagement will output a message in hello console.</span></span>

<span data-ttu-id="3019e-183">sağlanan hello nib dosyası kuralları aşağıdaki hello saygı:</span><span class="sxs-lookup"><span data-stu-id="3019e-183">hello provided nib file should respect hello following rules:</span></span>

* <span data-ttu-id="3019e-184">Yalnızca bir görünüm içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3019e-184">It should only contain one view.</span></span>
* <span data-ttu-id="3019e-185">Subviews aynı olanları adlı sağlanan hello nib dosyası içinde hello gibi türleri hello olması`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="3019e-185">Subviews should be of hello same types as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="3019e-186">Aynı adlı sağlanan hello nib dosyası içinde olanları hello gibi etiketler hello subviews olmalıdır`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="3019e-186">Subviews should have hello same tags as hello ones inside hello provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="3019e-187">Yalnızca, adlı sağlanan hello nib dosya kopyalama `AENotificationView.xib`ve buradan çalışmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="3019e-187">Just copy hello provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="3019e-188">Ancak dikkatli olun, bu nib dosya iç ilişkili toohello sınıf görünümü hello `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="3019e-188">But be careful, hello view inside this nib file is associated toohello class `AENotificationView`.</span></span> <span data-ttu-id="3019e-189">Bu sınıf hello yöntemi yeniden tanımlandı `layoutSubViews` toomove ve toocontext göre kendi subviews yeniden boyutlandırın.</span><span class="sxs-lookup"><span data-stu-id="3019e-189">This class redefined hello method `layoutSubViews` toomove and resize its subviews according toocontext.</span></span> <span data-ttu-id="3019e-190">Tooreplace isteyebilirsiniz ile bir `UIView` ya da size özel görünüm sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3019e-190">You may want tooreplace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="3019e-191">Daha derin özelleştirme bildirimlerinizi (örneğin tooload görünümünüzden doğrudan hello kod istiyorsanız) gerekiyorsa, hello göz sağlanan kaynak kodu ve sınıf belgelerine tootake önerilir `Protocol ReferencesDefaultNotifier` ve `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="3019e-191">If you need deeper customization of your notifications(if you want for instance tooload your view directly from hello code), it is recommended tootake a look at hello provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="3019e-192">Kullanabileceğiniz Not hello birden çok kategori için aynı bildirim.</span><span class="sxs-lookup"><span data-stu-id="3019e-192">Note that you can use hello same notifier for multiple categories.</span></span>

<span data-ttu-id="3019e-193">Aynı zamanda yeniden tanımlanan hello varsayılan bildirim şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="3019e-193">You can also redefined hello default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="3019e-194">Bildirim işleme</span><span class="sxs-lookup"><span data-stu-id="3019e-194">Notification handling</span></span>
<span data-ttu-id="3019e-195">Merhaba varsayılan kategori kullanırken, bazı yaşam döngüsü yöntemleri üzerinde hello denir `AEReachContent` nesne tooreport istatistikleri ve güncelleştirme hello kampanya durumu:</span><span class="sxs-lookup"><span data-stu-id="3019e-195">When using hello default category, some life cycle methods are called on hello `AEReachContent` object tooreport statistics and update hello campaign state:</span></span>

* <span data-ttu-id="3019e-196">Merhaba bildirim uygulamada görüntülendiğinde hello `displayNotification` yöntemi (hangi istatistikleri raporları) çağrılır tarafından `AEReachModule` varsa `handleNotification:` döndürür `YES`.</span><span class="sxs-lookup"><span data-stu-id="3019e-196">When hello notification is displayed in application, hello `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="3019e-197">Merhaba bildirim kapatıldığında, hello `exitNotification` yöntemi çağrıldığında, istatistik bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="3019e-197">If hello notification is dismissed, hello `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="3019e-198">Merhaba bildirim tıkladıysanız `actionNotification` olduğu adlı istatistik bildirilir ve ilişkili hello eylem gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3019e-198">If hello notification is clicked, `actionNotification` is called, statistic is reported and hello associated action is performed.</span></span>

<span data-ttu-id="3019e-199">Uygulamanıza `AENotifier` atlamaların hello varsayılan davranışı, toocall bu yaşam döngüsü yöntemleri başınıza gerekir.</span><span class="sxs-lookup"><span data-stu-id="3019e-199">If your implementation of `AENotifier` bypasses hello default behavior, you have toocall these life cycle methods by yourself.</span></span> <span data-ttu-id="3019e-200">Örnek hello hello varsayılan davranışı burada atlanır bazı durumlarda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3019e-200">hello following examples illustrate some cases where hello default behavior is bypassed:</span></span>

* <span data-ttu-id="3019e-201">Genişletme yok `AEDefaultNotifier`, sıfırdan kategori işleme uygulanan örn.</span><span class="sxs-lookup"><span data-stu-id="3019e-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="3019e-202">Geçersiz kılınmış `prepareNotificationView:forContent:`emin toomap olması en az `onNotificationActioned` veya `onNotificationExited` U.I denetimlerin tooone.</span><span class="sxs-lookup"><span data-stu-id="3019e-202">You overrode `prepareNotificationView:forContent:`, be sure toomap at least `onNotificationActioned` or `onNotificationExited` tooone of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="3019e-203">Varsa `handleNotification:` bir özel durum, içerik hello silinir ve `drop` olduğu çağrılır, bu istatistiklerine bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="3019e-203">If `handleNotification:` throws an exception, hello content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="3019e-204">Bildirim var olan bir görünümü bir parçası olarak dahil</span><span class="sxs-lookup"><span data-stu-id="3019e-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="3019e-205">Yer paylaşımları hızlı tümleştirme için oldukça uygundur ancak bazen uygun olamaz ya da istenmeyen yan etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3019e-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="3019e-206">Merhaba katmana sistem bazı görünümlerinizi memnun değilseniz, bu görünümleri için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3019e-206">If you're not satisfied with hello overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="3019e-207">Varolan görünümlerinizi tooinclude bizim bildirim düzeni karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3019e-207">You can decide tooinclude our notification layout in your existing views.</span></span> <span data-ttu-id="3019e-208">toodo bu nedenle, iki uygulama stili vardır:</span><span class="sxs-lookup"><span data-stu-id="3019e-208">toodo so, there is two implementation styles:</span></span>

1. <span data-ttu-id="3019e-209">Arabirim Oluşturucusu'nu kullanarak hello bildirim görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="3019e-209">Add hello notification view using interface builder</span></span>

   * <span data-ttu-id="3019e-210">Açık *arabirim Oluşturucusu*</span><span class="sxs-lookup"><span data-stu-id="3019e-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="3019e-211">320 x 60'ı (ya da iPad cihazında varsa 768 x 60) koyun `UIView` hello bildirim tooappear istediğiniz</span><span class="sxs-lookup"><span data-stu-id="3019e-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want hello notification tooappear</span></span>
   * <span data-ttu-id="3019e-212">Bu görünüm için Hello etiket değeri çok ayarlayın: **36822491**</span><span class="sxs-lookup"><span data-stu-id="3019e-212">Set hello Tag value for this view too: **36822491**</span></span>
2. <span data-ttu-id="3019e-213">Merhaba bildirim görünümü programlı olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3019e-213">Add hello notification view programmatically.</span></span> <span data-ttu-id="3019e-214">Görünümünüzü hazırlarken koddan hello eklemeniz yeterlidir:</span><span class="sxs-lookup"><span data-stu-id="3019e-214">Just add hello following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="3019e-215">`NOTIFICATION_AREA_VIEW_TAG`Makro bulunabilir `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="3019e-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="3019e-216">Merhaba varsayılan bildirim hello bildirim düzenini bu görünüme dahil edilmiştir ve bir katmana için eklemez otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="3019e-216">hello default notifier automatically detects that hello notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="3019e-217">Duyuruları ve yoklamaları</span><span class="sxs-lookup"><span data-stu-id="3019e-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="3019e-218">Düzenleri</span><span class="sxs-lookup"><span data-stu-id="3019e-218">Layouts</span></span>
<span data-ttu-id="3019e-219">Merhaba dosyalarda değişiklik yapabilir `AEDefaultAnnouncementView.xib` ve `AEDefaultPollView.xib` hello etiket değerlerini ve hello varolan subviews türleri tutmak sürece.</span><span class="sxs-lookup"><span data-stu-id="3019e-219">You can modify hello files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep hello tag values and types of hello existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="3019e-220">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="3019e-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="3019e-221">Alternatif düzenleri</span><span class="sxs-lookup"><span data-stu-id="3019e-221">Alternate layouts</span></span>
<span data-ttu-id="3019e-222">Bildirimler gibi hello kampanya kategori duyuruları ve yoklamaları için kullanılan toohave alternatif düzenleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3019e-222">Like notifications, hello campaign's category can be used toohave alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="3019e-223">toocreate duyuru için bir kategori, genişlemelidir **AEAnnouncementViewController** ve hello reach modülünün başlatıldıktan sonra kaydedin:</span><span class="sxs-lookup"><span data-stu-id="3019e-223">toocreate a category for an announcement, you must extend **AEAnnouncementViewController** and register it once hello reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="3019e-224">Bir kullanıcı hello kategorisiyle duyuru için bir bildirim her tıkladığınızda "Benim\_kategori", kayıtlı görünüm denetleyicinizi (Bu durumda `MyCustomAnnouncementViewController`) hello yöntemi çağrılarak başlatılır `initWithAnnouncement:` ve hello görünümü olacaktır eklenen toohello geçerli uygulama penceresi.</span><span class="sxs-lookup"><span data-stu-id="3019e-224">Each time a user will click on a notification for an announcement with hello category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling hello method `initWithAnnouncement:` and hello view will be added toohello current application window.</span></span>
>
>

<span data-ttu-id="3019e-225">Uygulamanızda hello `AEAnnouncementViewController` tooread hello özelliği olacaktır sınıfı `announcement` tooinitialize, subviews.</span><span class="sxs-lookup"><span data-stu-id="3019e-225">In your implementation of hello `AEAnnouncementViewController` class you will have tooread hello property `announcement` tooinitialize your subviews.</span></span> <span data-ttu-id="3019e-226">Merhaba aşağıdaki örnekte, iki yapmayı düşünebilirsiniz etiketleri kullanarak başlatılır `title` ve `body` hello özelliklerini `AEReachAnnouncement` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="3019e-226">Consider hello example below, where two labels are initialized using `title` and `body` properties of hello `AEReachAnnouncement` class:</span></span>

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

<span data-ttu-id="3019e-227">Tooload görünümlerinizi başınıza istemediğiniz ancak yalnızca tooreuse hello varsayılan duyuru görünüm düzeni istediğiniz, özel görünüm denetleyicinizi yalnızca yapabileceğiniz sağlanan hello sınıfını genişleten `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="3019e-227">If you don't want tooload your views by yourself but you just want tooreuse hello default announcement view layout, you can simply make your custom view controller extends hello provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="3019e-228">Bu durumda, hello nib dosya yinelenen `AEDefaultAnnouncementView.xib` ve özel görünüm denetleyicisi tarafından yüklenebilmesi için yeniden adlandırın (adlı bir denetleyici için `CustomAnnouncementViewController`, nib dosyanızı çağırmalıdır `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="3019e-228">In that case, duplicate hello nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="3019e-229">tooreplace hello varsayılan kategorisini Duyurular, yalnızca özel görünüm denetleyicinizi tanımlanan hello kategorisi için kayıt `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="3019e-229">tooreplace hello default category of announcements, simply register your custom view controller for hello category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="3019e-230">Anketler, özelleştirilmiş hello olabilir aynı şekilde:</span><span class="sxs-lookup"><span data-stu-id="3019e-230">Polls can be customized hello same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="3019e-231">Bu süre, sağlanan hello `MyCustomPollViewController` genişletmelidir `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="3019e-231">This time, hello provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="3019e-232">Veya hello varsayılan denetleyicisinden tooextend seçebilirsiniz: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="3019e-232">Or you can choose tooextend from hello default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3019e-233">Toocall ya da unutmayın `action` (`submitAnswers:` özel yoklama görünüm denetleyicileri için) veya `exit` hello görünüm denetleyicisini kapatıldığında önce yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3019e-233">Don't forget toocall either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before hello view controller is dismissed.</span></span> <span data-ttu-id="3019e-234">Aksi takdirde istatistikleri (yani hello kampanyası hiçbir analytics) gönderilmez ve hello uygulama işlemini yeniden başlatılana kadar daha fazla önemlisi sonraki Kampanyalar bildirilmez.</span><span class="sxs-lookup"><span data-stu-id="3019e-234">Otherwise, statistics won't be sent (i.e. no analytics on hello campaign) and more importantly next campaigns will not be notified until hello application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="3019e-235">Uygulama örneği</span><span class="sxs-lookup"><span data-stu-id="3019e-235">Implementation example</span></span>
<span data-ttu-id="3019e-236">Bu uygulama hello özel duyuru görünümü bir dış xib dosyasından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3019e-236">In this implementation hello custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="3019e-237">Gibi gelişmiş bildirim özelleştirmesi hello kaynak koduna hello standart uygulama toolook önerilir.</span><span class="sxs-lookup"><span data-stu-id="3019e-237">Like for advanced notification customization, it is recommended toolook at hello source code of hello standard implementation.</span></span>

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
