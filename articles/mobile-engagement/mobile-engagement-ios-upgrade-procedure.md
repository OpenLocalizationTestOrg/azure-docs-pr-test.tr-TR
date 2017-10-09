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
# <a name="upgrade-procedures"></a>Yükseltme yordamları
Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.

Hello SDK her yeni sürümü için önce değiştirmeniz gerekir (kaldırın ve yeniden xcode'da içeri aktarın) EngagementSDK ve EngagementReach klasörleri hello.

## <a name="from-300-too400"></a>3.0.0 gelen too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 hello SDK 4.0.0 sürümünden başlayarak zorunludur.

> [!NOTE]
> XCode 7'de gerçekten bağımlı sonra hello kullanabilir [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh). Bir bilinen hata varsa bu önceki sürümünü reach modülünü hello 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir. toofix bu tooimplement hello olacaktır API kullanım dışı `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:
> 
> 

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz. Mümkün olan en kısa sürede tooXCode 8 geçmelisiniz.
> 
> 

### <a name="usernotifications-framework"></a>UserNotifications framework
Tooadd hello gereksinim `UserNotifications` derleme aşamaları framework.

Merhaba proje Gezgini'nde, proje bölmesini açın ve hello doğru hedef seçin. Merhaba açın **"Derleme aşamaları"** sekmesi ve hello **"Bağlantı ikiliyi kitaplıklara"** menüsünde framework eklemek `UserNotifications.framework` -kümesi hello bağlantı olarak`Optional`

### <a name="application-push-capability"></a>Uygulamayı anında iletme yeteneği
XCode 8 uygulamanızı sıfırlama anında iletme yeteneği, Lütfen çift hello denetleyin `capability` seçilen hedef sekmesi.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Merhaba yeni iOS 10 bildirim kayıt kodu ekleyin
toonotifications hala çalışır ancak kullanıyor hello eski kod parçacığını tooregister hello uygulaması, iOS 10 çalıştırılırken API'leri kullanım dışı.

İçeri aktarma hello `User Notification` framework:

        #import <UserNotifications/UserNotifications.h> 

Uygulama temsilcinizi içinde `application:didFinishLaunchingWithOptions` yöntemi Değiştir:

    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
        [application registerForRemoteNotifications];
    }
    else {

        [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }

tarafından:

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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>UNUserNotificationCenter temsilci çakışmalarını çözme

*Uygulamanızı ya da üçüncü taraf Kitaplıklarınızı biri uygulayan bir `UNUserNotificationCenterDelegate` sonra da bu bölümü atlayabilirsiniz.*

A `UNUserNotificationCenter` temsilci hello SDK toomonitor hello yaşam döngüsü katılım bildirimler iOS 10 veya daha büyük çalıştıran cihazlarda tarafından kullanılır. Merhaba SDK sahip hello kendi uyarlamasını `UNUserNotificationCenterDelegate` protokol ancak yalnızca bir olabilir `UNUserNotificationCenter` temsilci uygulama başına. Herhangi bir temsilci eklenen toohello `UNUserNotificationCenter` nesne katılım bir hello ile çakışan. Merhaba SDK veya herhangi diğer üçüncü bir tarafın temsilci algılarsa, kendi uygulama toogive kullanmayacak sonra bir fırsat tooresolve çakışmaları hello. Tooadd hello katılım mantığı tooyour tooresolve hello çakışmaları temsilci sırada sahip olacaktır.

Var olan iki yolu tooachieve bu.

Teklif 1, temsilciniz ileterek toohello SDK çağırır:

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

Veya hello devralan tarafından 2, teklif `AEUserNotificationHandler` sınıfı

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
> Bir bildirim geçirerek değil veya katılım üzerinden gelen olup olmadığını belirlemek, `userInfo` sözlük toohello Aracısı `isEngagementPushPayload:` sınıf yöntemi.

Bu hello emin olun `UNUserNotificationCenter` nesnenin temsilci ya da hello içinde tooyour temsilci Ayarla `application:willFinishLaunchingWithOptions:` veya hello `application:didFinishLaunchingWithOptions:` uygulama temsilcinizi yöntemi.
Örneğin, Teklif 1 yukarıda hello uygulanırsa:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code
  
        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="from-200-too300"></a>2.0.0 gelen too3.0.0
İOS için destek bırakılan 4.X. Bu sürüm hello dağıtım hedefi, uygulamanızın başlangıç olmalıdır en az iOS 6.

Reach uygulamanızda kullanıyorsanız, eklemelisiniz `remote-notification` değeri toohello `UIBackgroundModes` Info.plist dosyanızdaki sipariş tooreceive uzak bildirimler dizisinde.

Merhaba yöntemi `application:didReceiveRemoteNotification:` değiştirilmiştir toobe gereken `application:didReceiveRemoteNotification:fetchCompletionHandler:` uygulama temsilcinizi içinde.

"AEPushDelegate.h" kullanım dışı arabirimi ve tüm başvuruları tooremove gerekir. Bu kaldırma içerir `[[EngagementAgent shared] setPushDelegate:self]` ve uygulama temsilcinizi yöntemleri temsilci hello:

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>1.16.0 gelen too2.0.0
Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır.
Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too1.16 ilk başvurun sonra hello aşağıdaki yordamı uygulayın.

> [!IMPORTANT]
> Capptain ve Mobile Engagement olan değil hello aynı Hizmetleri ve yalnızca aşağıda verilen hello yordamı nasıl toomigrate hello istemci uygulamaları vurgular. Geçirme hello SDK hello uygulama hello Capptain sunucuları toohello Mobile Engagement sunuculardan veri geçişi YAPILMAZ
> 
> 

### <a name="agent"></a>Aracı
Merhaba yöntemi `registerApp:` hello yeni yöntemi tarafından değiştirildiğini `init:`. Uygulama temsilcinizi uygun şekilde güncelleştirilmesi gerekir ve bağlantı dizesi kullanın:

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

SmartAd izleme yalnızca gerekir tooremove tüm örneklerini SDK'dan kaldırıldı `AETrackModule` sınıfı

### <a name="class-name-changes"></a>Sınıf adı değişikliği
Merhaba rebranding bir parçası olarak değiştirilen toobe gereken sınıf/dosya adları birkaç vardır.

Tüm sınıflar "CP" öneki "AE" önekiyle adlandırılır.

Örnek:

* `CPModule.h`çok adlandırılır`AEModule.h`.

Tüm sınıflar "İle Capptain" öneki "Katılım" önekiyle adlandırılır.

Örnekler:

* Merhaba sınıfı `CapptainAgent` çok adlandırılır`EngagementAgent`.
* Merhaba sınıfı `CapptainTableViewController` çok adlandırılır`EngagementTableViewController`.
* Merhaba sınıfı `CapptainUtils` çok adlandırılır`EngagementUtils`.
* Merhaba sınıfı `CapptainViewController` çok adlandırılır`EngagementViewController`.

