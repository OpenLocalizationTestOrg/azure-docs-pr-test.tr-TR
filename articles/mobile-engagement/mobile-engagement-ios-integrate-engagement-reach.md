---
title: "Azure Mobile Engagement iOS SDK tümleştirmesi ulaşmak | Microsoft Docs"
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
ms.openlocfilehash: ba74e0c442ac10f096d465f989e03d2ceae8cd88
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-reach-on-ios"></a><span data-ttu-id="8e892-103">Engagement Reach tümleştirmek için iOS hakkında</span><span class="sxs-lookup"><span data-stu-id="8e892-103">How to Integrate Engagement Reach on iOS</span></span>
<span data-ttu-id="8e892-104">Açıklanan tümleştirme yordamı izlemelisiniz [tümleştirmek katılım iOS belgesinde nasıl](mobile-engagement-ios-integrate-engagement.md) bu kılavuz aşağıdaki önce.</span><span class="sxs-lookup"><span data-stu-id="8e892-104">You must follow the integration procedure described in the [How to Integrate Engagement on iOS document](mobile-engagement-ios-integrate-engagement.md) before following this guide.</span></span>

<span data-ttu-id="8e892-105">Bu belge, XCode 8 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8e892-105">This documentation requires XCode 8.</span></span> <span data-ttu-id="8e892-106">XCode 7'de gerçekten bağımlı sonra kullanabilirsiniz [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="8e892-106">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="8e892-107">Bir bilinen hata varsa bu önceki sürüm 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir.</span><span class="sxs-lookup"><span data-stu-id="8e892-107">There is a known bug on this previous version while running on iOS 10 devices:  system notifications are not actioned.</span></span> <span data-ttu-id="8e892-108">Bu kullanım dışı API uygulamak için olacaktır sorunu gidermek için `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:</span><span class="sxs-lookup"><span data-stu-id="8e892-108">To fix this you will have to implement the deprecated API `application:didReceiveRemoteNotification:` in your app delegate as follows:</span></span>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> <span data-ttu-id="8e892-109">**Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e892-109">**We do not recommend this workaround** as this behavior can change in any upcoming (even minor) iOS version upgrade because this iOS API is deprecated.</span></span> <span data-ttu-id="8e892-110">Mümkün olan en kısa sürede XCode 8'e geçer.</span><span class="sxs-lookup"><span data-stu-id="8e892-110">You should switch to XCode 8 as soon as possible.</span></span>
>
>

### <a name="enable-your-app-to-receive-silent-push-notifications"></a><span data-ttu-id="8e892-111">Sessiz Anında İletme Bildirimlerini almak üzere uygulamanızı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="8e892-111">Enable your app to receive Silent Push Notifications</span></span>
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a><span data-ttu-id="8e892-112">Tümleştirme adımları</span><span class="sxs-lookup"><span data-stu-id="8e892-112">Integration steps</span></span>
### <a name="embed-the-engagement-reach-sdk-into-your-ios-project"></a><span data-ttu-id="8e892-113">Engagement Reach SDK'sı iOS projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="8e892-113">Embed the Engagement Reach SDK into your iOS project</span></span>
* <span data-ttu-id="8e892-114">Reach SDK'sını Xcode projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8e892-114">Add the Reach sdk in your Xcode project.</span></span> <span data-ttu-id="8e892-115">Xcode'da, Git **proje \> projesine Ekle** ve `EngagementReach` klasör.</span><span class="sxs-lookup"><span data-stu-id="8e892-115">In Xcode, go to **Project \> Add to project** and choose the `EngagementReach` folder.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="8e892-116">Uygulama Temsilcinizi değiştirme</span><span class="sxs-lookup"><span data-stu-id="8e892-116">Modify your Application Delegate</span></span>
* <span data-ttu-id="8e892-117">Uygulama dosyanızın en üstünde Engagement Reach modülünü içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="8e892-117">At the top of your implementation file, import the Engagement Reach module:</span></span>

      [...]
      #import "AEReachModule.h"
* <span data-ttu-id="8e892-118">Yöntemi içinde `applicationDidFinishLaunching:` veya `application:didFinishLaunchingWithOptions:`, bir reach modülü oluşturun ve mevcut Engagement başlatma satırınıza geçirin:</span><span class="sxs-lookup"><span data-stu-id="8e892-118">Inside method `applicationDidFinishLaunching:` or `application:didFinishLaunchingWithOptions:`, create a reach module and pass it to your existing Engagement initialization line:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* <span data-ttu-id="8e892-119">Değiştirme **'icon.png'** dize bildirim simgesi olarak istediğiniz görüntü adı ile.</span><span class="sxs-lookup"><span data-stu-id="8e892-119">Modify **'icon.png'** string with the image name you want as your notification icon.</span></span>
* <span data-ttu-id="8e892-120">Seçeneğini kullanmak istiyorsanız, *güncelleştirme rozet değeri* Reach kampanyaları veya yerel gönderim kullanmak isteyip istemediğinizi \<SaaS/Reach API'sini/Kampanya biçimi/yerel anında iletme\> kampanyalar, rozet yönetmek Reach modülünün izin gerekir (bunu otomatik olarak uygulama rozet temizleyin ve ayrıca uygulama Başlarken veya foregrounded her zaman Engagement tarafından depolanan değer Sıfırla) simgesi kendisi.</span><span class="sxs-lookup"><span data-stu-id="8e892-120">If you want to use the option *Update badge value* in Reach campaigns or if you want to use native push \</SaaS/Reach API/Campaign format/Native Push\> campaigns, you must let the Reach module manage the badge icon itself (it will automatically clear the application badge and also reset the value stored by Engagement every time the application is started or foregrounded).</span></span> <span data-ttu-id="8e892-121">Bu, Reach modülü başlatma sonra aşağıdaki satırı ekleyerek yapılır:</span><span class="sxs-lookup"><span data-stu-id="8e892-121">This is done by adding the following line after Reach module initialization:</span></span>

      [reach setAutoBadgeEnabled:YES];
* <span data-ttu-id="8e892-122">Reach veri gönderimi işlemek istiyorsanız, uygun uygulama temsilcinizi izin vermelisiniz `AEReachDataPushDelegate` protokolü.</span><span class="sxs-lookup"><span data-stu-id="8e892-122">If you want to handle Reach data push, you must let your Application delegate conform to the `AEReachDataPushDelegate` protocol.</span></span> <span data-ttu-id="8e892-123">Reach modülü başlatma sonra aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8e892-123">Add the following line after Reach module initialization:</span></span>

      [reach setDataPushDelegate:self];
* <span data-ttu-id="8e892-124">Yöntemleri uygulayabilirsiniz sonra `onDataPushStringReceived:` ve `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` uygulama temsilcinizi içinde:</span><span class="sxs-lookup"><span data-stu-id="8e892-124">Then you can implement the methods `onDataPushStringReceived:` and `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` in your application delegate:</span></span>

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

### <a name="category"></a><span data-ttu-id="8e892-125">Kategori</span><span class="sxs-lookup"><span data-stu-id="8e892-125">Category</span></span>
<span data-ttu-id="8e892-126">Kategori parametresi bir veri gönderme kampanya oluşturduğunuzda isteğe bağlıdır ve filtre veri iter sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e892-126">The category parameter is optional when you create a Data Push campaign and allows you to filter data pushes.</span></span> <span data-ttu-id="8e892-127">Farklı tür itmek istiyorsanız kullanışlıdır, `Base64` veri ve ayrıştırmadan önce kendi türünü tanımlamak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="8e892-127">This is useful if you want to push different kinds of `Base64` data and want to identify their type before parsing them.</span></span>

<span data-ttu-id="8e892-128">**Uygulamanızı şimdi almak ve reach içeriğini görüntülemek hazır!**</span><span class="sxs-lookup"><span data-stu-id="8e892-128">**Your application is now ready to receive and display reach contents!**</span></span>

## <a name="how-to-receive-announcements-and-polls-at-any-time"></a><span data-ttu-id="8e892-129">Duyuruları ve yoklamaları herhangi bir zamanda alma</span><span class="sxs-lookup"><span data-stu-id="8e892-129">How to receive announcements and polls at any time</span></span>
<span data-ttu-id="8e892-130">Engagement Reach bildirimleri son kullanıcılarınız için herhangi bir zamanda Apple anında iletilen bildirim servisi kullanarak gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e892-130">Engagement can send Reach notifications to your end users at any time by using the Apple Push Notification Service.</span></span>

<span data-ttu-id="8e892-131">Bu işlevselliği etkinleştirmek için Apple anında iletme bildirimleri için uygulamanızı hazırlamak ve uygulama temsilcinizi değiştirme gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e892-131">To enable this functionality, you'll have to prepare your application for Apple push notifications and modify your application delegate.</span></span>

### <a name="prepare-your-application-for-apple-push-notifications"></a><span data-ttu-id="8e892-132">Uygulamanızın Apple anında iletme bildirimleri için hazırlama</span><span class="sxs-lookup"><span data-stu-id="8e892-132">Prepare your application for Apple push notifications</span></span>
<span data-ttu-id="8e892-133">Lütfen kılavuzunu izleyin: [uygulamanız Apple anında iletme bildirimleri için hazırlama](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="8e892-133">Please follow the guide : [How to Prepare your Application for Apple Push Notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

### <a name="add-the-necessary-client-code"></a><span data-ttu-id="8e892-134">Gerekli istemci kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="8e892-134">Add the necessary client code</span></span>
<span data-ttu-id="8e892-135">*Bu noktada, uygulamanızın kayıtlı bir Apple anında iletme sertifika katılım ön ucunda olması gerekir.*</span><span class="sxs-lookup"><span data-stu-id="8e892-135">*At this point your application should have a registered Apple push certificate in the Engagement frontend.*</span></span>

<span data-ttu-id="8e892-136">Henüz yapmadıysanız anında iletme bildirimlerini almak üzere uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e892-136">If it's not done already, you need to register your application to receive push notifications.</span></span>

* <span data-ttu-id="8e892-137">İçeri aktarma `User Notification` framework:</span><span class="sxs-lookup"><span data-stu-id="8e892-137">Import the `User Notification` framework:</span></span>

        #import <UserNotifications/UserNotifications.h>
* <span data-ttu-id="8e892-138">Uygulamanız başladığında aşağıdaki satırı ekleyin (genellikle, `application:didFinishLaunchingWithOptions:`):</span><span class="sxs-lookup"><span data-stu-id="8e892-138">Add the following line when your application starts (typically in `application:didFinishLaunchingWithOptions:`):</span></span>

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

<span data-ttu-id="8e892-139">Ardından, cihaz belirteci Apple sunucuları tarafından döndürülen engagement sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e892-139">Then, You need to provide to Engagement the device token returned by Apple servers.</span></span> <span data-ttu-id="8e892-140">Bu yöntemin adlı yapılır `application:didRegisterForRemoteNotificationsWithDeviceToken:` uygulama temsilcinizi içinde:</span><span class="sxs-lookup"><span data-stu-id="8e892-140">This is done in the method named `application:didRegisterForRemoteNotificationsWithDeviceToken:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

<span data-ttu-id="8e892-141">Son olarak, uygulamanızın uzak bir bildirim aldığında Engagement SDK'sı hakkında bilgilendirmek sahip.</span><span class="sxs-lookup"><span data-stu-id="8e892-141">Finally, you have to inform the Engagement SDK when your application receives a remote notification.</span></span> <span data-ttu-id="8e892-142">Bunu yapmak için yöntemi çağırın `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` uygulama temsilcinizi içinde:</span><span class="sxs-lookup"><span data-stu-id="8e892-142">To do that, call the method `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` in your application delegate:</span></span>

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> <span data-ttu-id="8e892-143">Varsayılan olarak, Engagement Reach completionHandler denetler.</span><span class="sxs-lookup"><span data-stu-id="8e892-143">By default, Engagement Reach controls the completionHandler.</span></span> <span data-ttu-id="8e892-144">El ile yanıt vermek istiyorsanız `handler` kodunuzda engellemek, nil geçirmek `handler` bağımsız değişkeni ve denetim tamamlama bloğu kendiniz.</span><span class="sxs-lookup"><span data-stu-id="8e892-144">If you want to manually respond to the `handler` block in your code, you can pass nil for the `handler` argument and control the completion block yourself.</span></span> <span data-ttu-id="8e892-145">Bkz: `UIBackgroundFetchResult` olası değerler listesi türü.</span><span class="sxs-lookup"><span data-stu-id="8e892-145">See the `UIBackgroundFetchResult` type for a list of possible values.</span></span>
>
>

### <a name="full-example"></a><span data-ttu-id="8e892-146">Tam örnek</span><span class="sxs-lookup"><span data-stu-id="8e892-146">Full example</span></span>
<span data-ttu-id="8e892-147">Tümleştirme tam bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8e892-147">Here is a full example of integration:</span></span>

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a><span data-ttu-id="8e892-148">UNUserNotificationCenter temsilci çakışmalarını çözme</span><span class="sxs-lookup"><span data-stu-id="8e892-148">Resolve UNUserNotificationCenter delegate conflicts</span></span>

<span data-ttu-id="8e892-149">*Uygulamanızı ya da üçüncü taraf Kitaplıklarınızı biri uygulayan bir `UNUserNotificationCenterDelegate` sonra da bu bölümü atlayabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="8e892-149">*If neither your application or one of your third party libraries implements a `UNUserNotificationCenterDelegate` then you can skip this part.*</span></span>

<span data-ttu-id="8e892-150">A `UNUserNotificationCenter` temsilci SDK tarafından katılım bildirimleri 10 veya daha büyük iOS çalıştıran cihazlarda yaşam döngüsünü izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8e892-150">A `UNUserNotificationCenter` delegate is used by the SDK to monitor the life cycle of Engagement notifications on devices running on iOS 10 or greater.</span></span> <span data-ttu-id="8e892-151">SDK, kendi uygulamanızda `UNUserNotificationCenterDelegate` protokol ancak yalnızca bir olabilir `UNUserNotificationCenter` temsilci uygulama başına.</span><span class="sxs-lookup"><span data-stu-id="8e892-151">The SDK has its own implementation of the `UNUserNotificationCenterDelegate` protocol but there can be only one `UNUserNotificationCenter` delegate per application.</span></span> <span data-ttu-id="8e892-152">Eklenen herhangi bir temsilci `UNUserNotificationCenter` nesne katılım bir çakışma.</span><span class="sxs-lookup"><span data-stu-id="8e892-152">Any other delegate added to the `UNUserNotificationCenter` object will conflict with the Engagement one.</span></span> <span data-ttu-id="8e892-153">SDK veya herhangi diğer üçüncü bir tarafın temsilci algılarsa sonra kendi uygulama çakışmaları olanağı vermek için kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="8e892-153">If the SDK detects your or any other third party's delegate then it will not use its own implementation to give you a chance to resolve the conflicts.</span></span> <span data-ttu-id="8e892-154">Çakışmaları çözümlemek amacıyla kendi temsilciye katılım mantığı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e892-154">You will have to add the Engagement logic to your own delegate in order to resolve the conflicts.</span></span>

<span data-ttu-id="8e892-155">Bunu başarmak için iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="8e892-155">There are two ways to achieve this.</span></span>

<span data-ttu-id="8e892-156">SDK çağrıları temsilciniz iletme tarafından yalnızca 1, Teklif:</span><span class="sxs-lookup"><span data-stu-id="8e892-156">Proposal 1, simply by forwarding your delegate calls to the SDK:</span></span>

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

<span data-ttu-id="8e892-157">Veya içinden devralma tarafından 2, teklif `AEUserNotificationHandler` sınıfı</span><span class="sxs-lookup"><span data-stu-id="8e892-157">Or proposal 2, by inheriting from the `AEUserNotificationHandler` class</span></span>

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
> <span data-ttu-id="8e892-158">Bir bildirim geçirerek değil veya katılım üzerinden gelen olup olmadığını belirlemek, `userInfo` aracı sözlüğe `isEngagementPushPayload:` sınıf yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8e892-158">You can determine whether a notification comes from Engagement or not by passing its `userInfo` dictionary to the Agent `isEngagementPushPayload:` class method.</span></span>

<span data-ttu-id="8e892-159">Olduğundan emin olun `UNUserNotificationCenter` nesnenin temsilci temsilciniz ya da içinde ayarlanmış `application:willFinishLaunchingWithOptions:` veya `application:didFinishLaunchingWithOptions:` uygulama temsilcinizi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8e892-159">Make sure that the `UNUserNotificationCenter` object's delegate is set to your delegate within either the `application:willFinishLaunchingWithOptions:` or the `application:didFinishLaunchingWithOptions:` method of your application delegate.</span></span>
<span data-ttu-id="8e892-160">Örneğin, yukarıdaki teklifi 1 uygulanırsa:</span><span class="sxs-lookup"><span data-stu-id="8e892-160">For instance, if you implemented the above proposal 1:</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-to-customize-campaigns"></a><span data-ttu-id="8e892-161">Kampanyalar özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8e892-161">How to customize campaigns</span></span>
### <a name="notifications"></a><span data-ttu-id="8e892-162">Bildirimler</span><span class="sxs-lookup"><span data-stu-id="8e892-162">Notifications</span></span>
<span data-ttu-id="8e892-163">Bildirimler iki tür vardır: Sistem ve uygulama içi bildirimler.</span><span class="sxs-lookup"><span data-stu-id="8e892-163">There are two types of notifications: system and in-app notifications.</span></span>

<span data-ttu-id="8e892-164">Sistem bildirimleri iOS tarafından işlenir ve özelleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="8e892-164">System notifications are handled by iOS, and cannot be customized.</span></span>

<span data-ttu-id="8e892-165">Uygulama bildirimleri geçerli uygulama penceresi dinamik olarak eklenen bir görünümün yapılır.</span><span class="sxs-lookup"><span data-stu-id="8e892-165">In-app notifications are made of a view that is dynamically added to the current application window.</span></span> <span data-ttu-id="8e892-166">Bu bildirim bir katmana çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8e892-166">This is called a notification overlay.</span></span> <span data-ttu-id="8e892-167">Bunlar gerekli olmadığı için uygulamanızda herhangi bir görünüm değiştirmenizi bildirim yer paylaşımları hızlı tümleştirme için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="8e892-167">Notification overlays are great for a fast integration because they does not require you to modify any view in your application.</span></span>

#### <a name="layout"></a><span data-ttu-id="8e892-168">Düzen</span><span class="sxs-lookup"><span data-stu-id="8e892-168">Layout</span></span>
<span data-ttu-id="8e892-169">Uygulama içi bildirimler görünümünü değiştirmek için yalnızca dosyasını değiştirebilirsiniz `AENotificationView.xib` gereksinimlerinize, varolan subviews türünü ve etiket değerleri tutmak sürece.</span><span class="sxs-lookup"><span data-stu-id="8e892-169">To modify the look of your in-app notifications, you can simply modify the file `AENotificationView.xib` to your needs, as long as you keep the tag values and types of the existing subviews.</span></span>

<span data-ttu-id="8e892-170">Varsayılan olarak, uygulama içi bildirimler ekranın alt kısmında sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8e892-170">By default, in-app notifications are presented at the bottom of the screen.</span></span> <span data-ttu-id="8e892-171">Ekranın en üstünde görüntülenecek tercih ederseniz, sağlanan düzenleme `AENotificationView.xib` değiştirip `AutoSizing` kendi değerlendirmesi üstünde tutulması için ana görünümün özelliği.</span><span class="sxs-lookup"><span data-stu-id="8e892-171">If you prefer to display them at the top of screen, edit the provided `AENotificationView.xib` and change the `AutoSizing` property of the main view so it can be kept at the top of its superview.</span></span>

#### <a name="categories"></a><span data-ttu-id="8e892-172">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="8e892-172">Categories</span></span>
<span data-ttu-id="8e892-173">Sağlanan Düzen değiştirdiğinizde, tüm bildirimlerinizi görünümünü değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8e892-173">When you modify the provided layout, you modify the look of all your notifications.</span></span> <span data-ttu-id="8e892-174">Kategoriler, bildirimler için çeşitli hedeflenen görünüyor (büyük olasılıkla davranışları) tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e892-174">Categories allow you to define various targeted looks (possibly behaviors) for notifications.</span></span> <span data-ttu-id="8e892-175">Bir kategori Reach kampanya oluşturduğunuzda belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="8e892-175">A category can be specified when you create a Reach campaign.</span></span> <span data-ttu-id="8e892-176">Bu belgenin sonraki bölümlerinde açıklanan kategoriler de duyuruları ve yoklamaları, özelleştirmenize olanak tanır olduğunu aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8e892-176">Keep in mind that categories also let you customize announcements and polls, that is described later in this document.</span></span>

<span data-ttu-id="8e892-177">Bildirimlerinizi için bir kategori işleyici kaydetmek için reach modülünün başlatıldıktan sonra bir çağrı eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e892-177">To register a category handler for your notifications, you need to add a call once the reach module is initialized.</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

<span data-ttu-id="8e892-178">`myNotifier`protokol uyan bir nesne örneği olmalıdır `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="8e892-178">`myNotifier` must be an instance of an object that conforms to the protocol `AENotifier`.</span></span>

<span data-ttu-id="8e892-179">Kendi kendinize Protokolü yöntemleri uygulayabilirsiniz veya varolan bir sınıfı yeniden uygulamalı seçtiğiniz `AEDefaultNotifier` işlerin çoğunu zaten gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="8e892-179">You can implement the protocol methods by yourself or you can choose to reimplement the existing class `AEDefaultNotifier` which already performs most of the work.</span></span>

<span data-ttu-id="8e892-180">Örneğin, belirli bir kategorideki uyarı görünümünü yeniden tanımlamak istiyorsanız, bu örnek izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8e892-180">For example, if you want to redefine the notification view for a specific category, you can follow this example:</span></span>

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

<span data-ttu-id="8e892-181">Bu basit örnek kategorisinin varsayalım adında bir dosyanız varsa `MyNotificationView.xib` ana uygulama paket içindeki.</span><span class="sxs-lookup"><span data-stu-id="8e892-181">This simple example of category assume that you have a file named `MyNotificationView.xib` in your main application bundle.</span></span> <span data-ttu-id="8e892-182">Yöntem karşılık gelen bulamıyor değilse `.xib`, bildirim görüntülenmeyecek ve katılım konsolunda bir ileti çıktı.</span><span class="sxs-lookup"><span data-stu-id="8e892-182">If the method is not able to find a corresponding `.xib`, the notification will not be displayed and Engagement will output a message in the console.</span></span>

<span data-ttu-id="8e892-183">Sağlanan nib dosyası aşağıdaki kuralları dikkate:</span><span class="sxs-lookup"><span data-stu-id="8e892-183">The provided nib file should respect the following rules:</span></span>

* <span data-ttu-id="8e892-184">Yalnızca bir görünüm içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e892-184">It should only contain one view.</span></span>
* <span data-ttu-id="8e892-185">Sağlanan nib dosyası içindeki olanlarla aynı türlerinin subviews adlı`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="8e892-185">Subviews should be of the same types as the ones inside the provided nib file named `AENotificationView.xib`</span></span>
* <span data-ttu-id="8e892-186">Subviews anahtarlarla sağlanan içinde aynı etiketleri olması gerektiğini adlı nib dosyası`AENotificationView.xib`</span><span class="sxs-lookup"><span data-stu-id="8e892-186">Subviews should have the same tags as the ones inside the provided nib file named `AENotificationView.xib`</span></span>

> [!TIP]
> <span data-ttu-id="8e892-187">Yalnızca adlı sağlanan nib dosya kopyalama `AENotificationView.xib`ve buradan çalışmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="8e892-187">Just copy the provided nib file, named `AENotificationView.xib`, and start working from there.</span></span> <span data-ttu-id="8e892-188">Ancak dikkatli olun, görünüm bu nib dosyası içinde sınıfla ilişkilendirilen `AENotificationView`.</span><span class="sxs-lookup"><span data-stu-id="8e892-188">But be careful, the view inside this nib file is associated to the class `AENotificationView`.</span></span> <span data-ttu-id="8e892-189">Bu sınıf yöntemi yeniden tanımlandı `layoutSubViews` taşımak ve kendi subviews bağlamı göre yeniden boyutlandırmak için.</span><span class="sxs-lookup"><span data-stu-id="8e892-189">This class redefined the method `layoutSubViews` to move and resize its subviews according to context.</span></span> <span data-ttu-id="8e892-190">Değiştirmek istediğiniz bir `UIView` ya da size özel görünüm sınıfı.</span><span class="sxs-lookup"><span data-stu-id="8e892-190">You may want to replace it with an `UIView` or you custom view class.</span></span>
>
>

<span data-ttu-id="8e892-191">Daha derin özelleştirme bildirimlerinizi gerekiyorsa (örneğin istiyorsanız doğrudan kodunuzdan görünümünüzü yüklemek için), sağlanan kaynak kodu ve sınıf belgeleri bakmak için önerilir `Protocol ReferencesDefaultNotifier` ve `AENotifier`.</span><span class="sxs-lookup"><span data-stu-id="8e892-191">If you need deeper customization of your notifications(if you want for instance to load your view directly from the code), it is recommended to take a look at the provided source code and class documentation of `Protocol ReferencesDefaultNotifier` and `AENotifier`.</span></span>

<span data-ttu-id="8e892-192">Birden çok kategori için aynı bildirim kullanabileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8e892-192">Note that you can use the same notifier for multiple categories.</span></span>

<span data-ttu-id="8e892-193">De yeniden tanımlandı varsayılan bildirim şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="8e892-193">You can also redefined the default notifier like this:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a><span data-ttu-id="8e892-194">Bildirim işleme</span><span class="sxs-lookup"><span data-stu-id="8e892-194">Notification handling</span></span>
<span data-ttu-id="8e892-195">Varsayılan Kategori kullanırken, bazı yaşam döngüsü yöntemleri üzerinde denir `AEReachContent` nesne istatistikleri rapor ve kampanya durumunu güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="8e892-195">When using the default category, some life cycle methods are called on the `AEReachContent` object to report statistics and update the campaign state:</span></span>

* <span data-ttu-id="8e892-196">Uygulamada, bildirim görüntülendiğinde `displayNotification` yöntemi (hangi istatistikleri raporları) çağrılır tarafından `AEReachModule` varsa `handleNotification:` döndürür `YES`.</span><span class="sxs-lookup"><span data-stu-id="8e892-196">When the notification is displayed in application, the `displayNotification` method is called (which reports statistics) by `AEReachModule` if `handleNotification:` returns `YES`.</span></span>
* <span data-ttu-id="8e892-197">Bildirim kapatıldığında, `exitNotification` yöntemi çağrıldığında, istatistik bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="8e892-197">If the notification is dismissed, the `exitNotification` method is called, statistic is reported and next campaigns can now be processed.</span></span>
* <span data-ttu-id="8e892-198">Bildirim tıkladıysanız `actionNotification` olan çağrılır, istatistik bildirilir ve ilişkili eylem gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8e892-198">If the notification is clicked, `actionNotification` is called, statistic is reported and the associated action is performed.</span></span>

<span data-ttu-id="8e892-199">Uygulamanıza `AENotifier` varsayılan davranışı, atlar başınıza bu yaşam döngüsü yöntemlerini çağırmaya sahip.</span><span class="sxs-lookup"><span data-stu-id="8e892-199">If your implementation of `AENotifier` bypasses the default behavior, you have to call these life cycle methods by yourself.</span></span> <span data-ttu-id="8e892-200">Aşağıdaki örneklerde varsayılan davranış olduğu atlanır bazı durumlarda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="8e892-200">The following examples illustrate some cases where the default behavior is bypassed:</span></span>

* <span data-ttu-id="8e892-201">Genişletme yok `AEDefaultNotifier`, sıfırdan kategori işleme uygulanan örn.</span><span class="sxs-lookup"><span data-stu-id="8e892-201">You don't extend `AEDefaultNotifier`, e.g. you implemented category handling from scratch.</span></span>
* <span data-ttu-id="8e892-202">Geçersiz kılınmış `prepareNotificationView:forContent:`, en az eşlemek mutlaka `onNotificationActioned` veya `onNotificationExited` , U.I birine denetler.</span><span class="sxs-lookup"><span data-stu-id="8e892-202">You overrode `prepareNotificationView:forContent:`, be sure to map at least `onNotificationActioned` or `onNotificationExited` to one of your U.I controls.</span></span>

> [!WARNING]
> <span data-ttu-id="8e892-203">Varsa `handleNotification:` bir özel durum, içeriği silinir atar ve `drop` olduğu çağrılır, bu istatistiklerine bildirilir ve sonraki Kampanyalar şimdi işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="8e892-203">If `handleNotification:` throws an exception, the content is deleted and `drop` is called, this is reported in statistics and next campaigns can now be processed.</span></span>
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a><span data-ttu-id="8e892-204">Bildirim var olan bir görünümü bir parçası olarak dahil</span><span class="sxs-lookup"><span data-stu-id="8e892-204">Include notification as part of an existing view</span></span>
<span data-ttu-id="8e892-205">Yer paylaşımları hızlı tümleştirme için oldukça uygundur ancak bazen uygun olamaz ya da istenmeyen yan etkileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e892-205">Overlays are great for a fast integration but can be sometimes not convenient, or can have unwanted side effects.</span></span>

<span data-ttu-id="8e892-206">Kendi görünümlerinizi bazıları katmana sistemde memnun değilseniz, bu görünümleri için özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e892-206">If you're not satisfied with the overlay system in some of your views, you can customize it for these views.</span></span>

<span data-ttu-id="8e892-207">Bizim bildirim düzeni varolan görünümlerinizi içerecek şekilde karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e892-207">You can decide to include our notification layout in your existing views.</span></span> <span data-ttu-id="8e892-208">Bunu yapmak için iki uygulama stili vardır:</span><span class="sxs-lookup"><span data-stu-id="8e892-208">To do so, there is two implementation styles:</span></span>

1. <span data-ttu-id="8e892-209">Arabirim Oluşturucusu'nu kullanarak bildirim görünümü ekleme</span><span class="sxs-lookup"><span data-stu-id="8e892-209">Add the notification view using interface builder</span></span>

   * <span data-ttu-id="8e892-210">Açık *arabirim Oluşturucusu*</span><span class="sxs-lookup"><span data-stu-id="8e892-210">Open *Interface Builder*</span></span>
   * <span data-ttu-id="8e892-211">320 x 60'ı (ya da iPad cihazında varsa 768 x 60) koyun `UIView` bildirim görünmesini istediğiniz yere</span><span class="sxs-lookup"><span data-stu-id="8e892-211">Place a 320x60 (or 768x60 if you are on iPad) `UIView` where you want the notification to appear</span></span>
   * <span data-ttu-id="8e892-212">Bu görünüm için etiket değeri ayarlanamıyor: **36822491**</span><span class="sxs-lookup"><span data-stu-id="8e892-212">Set the Tag value for this view to : **36822491**</span></span>
2. <span data-ttu-id="8e892-213">Bildirim görünümü programlı olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8e892-213">Add the notification view programmatically.</span></span> <span data-ttu-id="8e892-214">Görünümünüzü hazırlarken yalnızca aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8e892-214">Just add the following code when your view has been initialized:</span></span>

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values to your needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

<span data-ttu-id="8e892-215">`NOTIFICATION_AREA_VIEW_TAG`Makro bulunabilir `AEDefaultNotifier.h`.</span><span class="sxs-lookup"><span data-stu-id="8e892-215">`NOTIFICATION_AREA_VIEW_TAG` macro can be found in `AEDefaultNotifier.h`.</span></span>

> [!NOTE]
> <span data-ttu-id="8e892-216">Varsayılan bildirim bildirim düzeni bu görünüme dahil edilmiştir ve bir katmana için eklemez otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="8e892-216">The default notifier automatically detects that the notification layout is included in this view and will not add an overlay for it.</span></span>
>
>

### <a name="announcements-and-polls"></a><span data-ttu-id="8e892-217">Duyuruları ve yoklamaları</span><span class="sxs-lookup"><span data-stu-id="8e892-217">Announcements and polls</span></span>
#### <a name="layouts"></a><span data-ttu-id="8e892-218">Düzenleri</span><span class="sxs-lookup"><span data-stu-id="8e892-218">Layouts</span></span>
<span data-ttu-id="8e892-219">Dosyalarda değişiklik yapabilir `AEDefaultAnnouncementView.xib` ve `AEDefaultPollView.xib` varolan subviews türünü ve etiket değerleri tutmak sürece.</span><span class="sxs-lookup"><span data-stu-id="8e892-219">You can modify the files `AEDefaultAnnouncementView.xib` and `AEDefaultPollView.xib` as long as you keep the tag values and types of the existing subviews.</span></span>

#### <a name="categories"></a><span data-ttu-id="8e892-220">Kategoriler</span><span class="sxs-lookup"><span data-stu-id="8e892-220">Categories</span></span>
##### <a name="alternate-layouts"></a><span data-ttu-id="8e892-221">Alternatif düzenleri</span><span class="sxs-lookup"><span data-stu-id="8e892-221">Alternate layouts</span></span>
<span data-ttu-id="8e892-222">Bildirimler gibi kampanya kategori duyuruları ve yoklamaları için alternatif düzenleri sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8e892-222">Like notifications, the campaign's category can be used to have alternate layouts for your announcements and polls.</span></span>

<span data-ttu-id="8e892-223">Duyuru için bir kategori oluşturmak için genişletmelidir **AEAnnouncementViewController** ve reach modülünün başlatıldıktan sonra kaydedin:</span><span class="sxs-lookup"><span data-stu-id="8e892-223">To create a category for an announcement, you must extend **AEAnnouncementViewController** and register it once the reach module has been initialized:</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> <span data-ttu-id="8e892-224">Bir kullanıcı kategorisiyle duyuru için bir bildirim her tıkladığınızda "Benim\_kategori", kayıtlı görünüm denetleyicinizi (Bu durumda `MyCustomAnnouncementViewController`) yöntemi çağrılarak başlatılır `initWithAnnouncement:` ve görünüm eklenir Geçerli uygulama penceresi.</span><span class="sxs-lookup"><span data-stu-id="8e892-224">Each time a user will click on a notification for an announcement with the category "my\_category", your registered view controller (in that case `MyCustomAnnouncementViewController`) will be initialized by calling the method `initWithAnnouncement:` and the view will be added to the current application window.</span></span>
>
>

<span data-ttu-id="8e892-225">Uygulamanızda `AEAnnouncementViewController` özelliği okumaya olacaktır sınıfı `announcement` , subviews başlatılamadı.</span><span class="sxs-lookup"><span data-stu-id="8e892-225">In your implementation of the `AEAnnouncementViewController` class you will have to read the property `announcement` to initialize your subviews.</span></span> <span data-ttu-id="8e892-226">Aşağıdaki örnek düşünün, burada iki etiket başlatılır kullanarak `title` ve `body` özelliklerini `AEReachAnnouncement` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="8e892-226">Consider the example below, where two labels are initialized using `title` and `body` properties of the `AEReachAnnouncement` class:</span></span>

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

<span data-ttu-id="8e892-227">Kendi görünümlerinizi kendiniz yüklemek istemediğiniz ancak yalnızca varsayılan duyuru görünüm düzenini yeniden kullanmak istediğiniz, yalnızca özel görünüm denetleyicinizi yapabilirsiniz sağlanan sınıfını genişleten `AEDefaultAnnouncementViewController`.</span><span class="sxs-lookup"><span data-stu-id="8e892-227">If you don't want to load your views by yourself but you just want to reuse the default announcement view layout, you can simply make your custom view controller extends the provided class `AEDefaultAnnouncementViewController`.</span></span> <span data-ttu-id="8e892-228">Bu durumda, nib dosyası yinelenen `AEDefaultAnnouncementView.xib` ve özel görünüm denetleyicisi tarafından yüklenebilmesi için yeniden adlandırın (adlı bir denetleyici için `CustomAnnouncementViewController`, nib dosyanızı çağırmalıdır `CustomAnnouncementView.xib`).</span><span class="sxs-lookup"><span data-stu-id="8e892-228">In that case, duplicate the nib file `AEDefaultAnnouncementView.xib` and rename it so it can be loaded by your custom view controller (for a controller named `CustomAnnouncementViewController`, you should call your nib file `CustomAnnouncementView.xib`).</span></span>

<span data-ttu-id="8e892-229">Duyurular varsayılan kategorisini değiştirmek için yalnızca özel görünüm denetleyicinizi tanımlanan kategori için kayıt `kAEReachDefaultCategory`:</span><span class="sxs-lookup"><span data-stu-id="8e892-229">To replace the default category of announcements, simply register your custom view controller for the category defined in `kAEReachDefaultCategory`:</span></span>

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

<span data-ttu-id="8e892-230">Tıpkı yoklamalar özelleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="8e892-230">Polls can be customized the same way :</span></span>

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

<span data-ttu-id="8e892-231">Bu süre, sağlanan `MyCustomPollViewController` genişletmelidir `AEPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="8e892-231">This time, the provided `MyCustomPollViewController` must extend `AEPollViewController`.</span></span> <span data-ttu-id="8e892-232">Veya varsayılan denetleyicisinden genişletmek seçebilirsiniz: `AEDefaultPollViewController`.</span><span class="sxs-lookup"><span data-stu-id="8e892-232">Or you can choose to extend from the default controller: `AEDefaultPollViewController`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e892-233">Ya da çağırmayı unuttunuz mu `action` (`submitAnswers:` özel yoklama görünüm denetleyicileri için) veya `exit` görünüm denetleyicisini kapatıldığında önce yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8e892-233">Don't forget to call either `action` (`submitAnswers:` for custom poll view controllers) or `exit` method before the view controller is dismissed.</span></span> <span data-ttu-id="8e892-234">Aksi takdirde istatistikleri (yani bir kampanya hiçbir analytics) gönderilmez ve uygulama işlemini yeniden başlatılana kadar daha fazla önemlisi sonraki Kampanyalar bildirilmez.</span><span class="sxs-lookup"><span data-stu-id="8e892-234">Otherwise, statistics won't be sent (i.e. no analytics on the campaign) and more importantly next campaigns will not be notified until the application process is restarted.</span></span>
>
>

##### <a name="implementation-example"></a><span data-ttu-id="8e892-235">Uygulama örneği</span><span class="sxs-lookup"><span data-stu-id="8e892-235">Implementation example</span></span>
<span data-ttu-id="8e892-236">Bu uygulama özel duyuru görünümü bir dış xib dosyasından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="8e892-236">In this implementation the custom announcement view is loaded from an external xib file.</span></span>

<span data-ttu-id="8e892-237">Gibi gelişmiş bildirim özelleştirme için standart uygulama kaynak koduna bakmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="8e892-237">Like for advanced notification customization, it is recommended to look at the source code of the standard implementation.</span></span>

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
