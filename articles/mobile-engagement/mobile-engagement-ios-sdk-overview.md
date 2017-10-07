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
# <a name="ios-sdk-for-azure-mobile-engagement"></a>Azure Mobile Engagement için iOS SDK’sı
Tooget tüm hello ayrıntıları hakkında buradan başlayın toointegrate Azure Mobile Engagement iOS uygulaması içinde. Toogive isterseniz bir try ilk olarak, emin olun, bunu bizim [15 dakika Öğreticisi](mobile-engagement-ios-get-started.md).

Toosee hello tıklatın [SDK içerik](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>Tümleştirme yordamları
1. Buradan başlayın: [nasıl toointegrate Mobile Engagement iOS uygulamanıza](mobile-engagement-ios-integrate-engagement.md)
2. Bildirimlerinin: [nasıl toointegrate ulaşma (bildirimler) iOS uygulamanıza](mobile-engagement-ios-integrate-engagement-reach.md)
3. Etiket planı uygulama: [nasıl toouse hello Mobile Engagement iOS uygulamanızı API etiketleme Gelişmiş](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>Sürüm notları
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Sabit rozetleri arka planda temizlendi.
* Sabit uyarılar ana sırada adlı değil API'leri hakkında XCode 9.
* Bellek sızıntısı ulaşma yoklamalarda sabit.
* İOS için destek bırakılan 6.X. Bu sürüm hello dağıtım hedefi, uygulamanızın başlangıç olmalıdır en az iOS 7.

Önceki sürümü için lütfen bkz hello [tamamlamak sürüm notları](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>Yükseltme yordamları
Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.

Bkz: SDK hello birçok sürümü eksik, çeşitli yordamlar toofollow olabilir hello tam [yükseltme yordamları](mobile-engagement-ios-upgrade-procedure.md).

Hello SDK her yeni sürümü için önce değiştirmeniz gerekir (kaldırın ve yeniden xcode'da içeri aktarın) EngagementSDK ve EngagementReach klasörleri hello.

### <a name="from-300-too400"></a>3.0.0 gelen too4.0.0
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

#### <a name="usernotifications-framework"></a>UserNotifications framework
Tooadd hello gereksinim `UserNotifications` derleme aşamaları framework.

Merhaba proje Gezgini'nde, proje bölmesini açın ve hello doğru hedef seçin. Merhaba açın **"Derleme aşamaları"** sekmesi ve hello **"Bağlantı ikiliyi kitaplıklara"** menüsünde framework eklemek `UserNotifications.framework` -kümesi hello bağlantı olarak`Optional`

#### <a name="application-push-capability"></a>Uygulamayı anında iletme yeteneği
XCode 8 uygulamanızı sıfırlama anında iletme yeteneği, Lütfen çift hello denetleyin `capability` seçilen hedef sekmesi.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Merhaba yeni iOS 10 bildirim kayıt kodu ekleyin
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

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>UNUserNotificationCenter temsilci çakışmalarını çözme

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
