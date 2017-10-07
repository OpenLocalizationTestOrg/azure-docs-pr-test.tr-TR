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
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Objective C’de iOS uygulamaları için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar tooan iOS uygulaması.
Bu öğreticide, temel verileri toplayan ve Apple Anında İletme Bildirimi Sistemi’ni (APNS) kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturursunuz.

Bu öğretici hello aşağıdakileri gerektirir:

* MAC App Store'dan yükleyebileceğiniz XCode 8
* Merhaba [Mobile Engagement iOS SDK'sı]

Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin tüm Mobile Engagement öğreticileri için önkoşuldur.

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
>
>

## <a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir. Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement iOS SDK tümleştirmesi](mobile-engagement-ios-sdk-overview.md)

XCode toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız.

### <a name="create-a-new-ios-project"></a>Yeni bir iOS projesi oluşturma
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
1. Merhaba karşıdan [Mobile Engagement iOS SDK'sı].
2. Merhaba ayıklayın. tar.gz dosyasını bilgisayarınızdaki tooa klasöre.
3. Merhaba projesine sağ tıklayın ve ardından **eklemek için dosyaları**.

    ![][1]
4. Toohello hello SDK'sını ayıkladığınız klasöre gidin, seçin hello `EngagementSDK` klasörünü tıklatın **seçenekleri** hello sol alt köşedeki ve o hello onay kutusunu emin olun **gerekirse öğeleri Kopyala** ve hello Hedef onay kutusunu denetlenir sonra basın **Tamam**.

    ![][2]
5. Açık hello **derleme aşamaları** sekmesinde ve hello **bağlantı ikiliyi kitaplıklara** menüsünde hello çerçeveleri aşağıda gösterildiği gibi ekleyin:

    ![][3]
6. Toohello uygulamanızın Azure portalında dön **bağlantı bilgisi** sayfası ve kopyalama hello bağlantı dizesi.

    ![][4]
7. Aşağıdaki kod satırı hello eklemek, **AppDelegate.m** dosya.

        #import "EngagementAgent.h"
8. Şimdi hello hello bağlantı dizesini yapıştırın `didFinishLaunchingWithOptions` temsilci.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`SDK günlükleri için tooidentify sorunları sağlayan isteğe bağlı bir ifadedir.

## <a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme
Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.

1. Açık hello **ViewController.h** dosya ve içeri aktarma **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Şimdi hello hello Süper sınıfını değiştirmek **ViewController** tarafından arabirim `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında toointeract kullanıcılarınız ve REACH sağlar. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Uygulama tooreceive sessiz anında iletme bildirimlerini etkinleştirme
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Merhaba ulaşma kitaplığı tooyour projesini ekleyin
1. Projenize sağ tıklayın.
2. **Add files to** (Dosyaları şuraya ekle) seçeneğine tıklayın.
3. Merhaba SDK'sını ayıkladığınız toohello klasöre gidin.
4. Select hello `EngagementReach` klasör.
5. **Ekle**'ye tıklayın.

### <a name="modify-your-application-delegate"></a>Uygulama Temsilcinizi değiştirme
1. Geri **AppDeletegate.m** dosya, hello Engagement Reach modülünü içeri aktarın.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. İç hello `application:didFinishLaunchingWithOptions` yöntemi, bir Reach modülü oluşturun ve tooyour mevcut Engagement başlatma satır geçirin:

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Uygulama tooreceive APNS anında iletme bildirimlerini etkinleştirme
1. Satır toohello aşağıdaki hello eklemek `application:didFinishLaunchingWithOptions` yöntemi:

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
2. Merhaba eklemek `application:didRegisterForRemoteNotificationsWithDeviceToken` yöntemini aşağıdaki şekilde:

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Merhaba eklemek `didFailToRegisterForRemoteNotificationsWithError` yöntemini aşağıdaki şekilde:

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Merhaba eklemek `didReceiveRemoteNotification:fetchCompletionHandler` yöntemini aşağıdaki şekilde:

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
