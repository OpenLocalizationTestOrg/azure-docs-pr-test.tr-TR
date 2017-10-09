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
# <a name="how-toointegrate-engagement-reach-on-ios"></a>TooIntegrate Engagement Reach nasıl iOS
Merhaba tümleştirme hello yordamını izleyin [nasıl tooIntegrate Engagement iOS belgesinde](mobile-engagement-ios-integrate-engagement.md) bu kılavuz aşağıdaki önce.

Bu belge, XCode 8 gerektirir. XCode 7'de gerçekten bağımlı sonra hello kullanabilir [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh). Bir bilinen hata varsa bu önceki sürüm 10 ios'de çalıştırılırken: Sistem bildirimleri işleme alınan değildir. toofix bu tooimplement hello olacaktır API kullanım dışı `application:didReceiveRemoteNotification:` uygulamanızda temsilci gibi:

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Bu geçici çözüm önermiyoruz** gibi bu iOS API kullanım dışı olduğundan tüm yaklaşan (hatta küçük) iOS sürüm yükseltme Bu davranışı değiştirebilirsiniz. Mümkün olan en kısa sürede tooXCode 8 geçmelisiniz.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Uygulama tooreceive sessiz anında iletme bildirimlerini etkinleştirme
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Tümleştirme adımları
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Merhaba Engagement Reach SDK'sı iOS projenize ekleme
* Merhaba Reach SDK'sını Xcode projenize ekleyin. Xcode'da, çok Git**proje \> tooproject ekleme** ve hello seçin `EngagementReach` klasör.

### <a name="modify-your-application-delegate"></a>Uygulama Temsilcinizi değiştirme
* Uygulama dosyanızı Hello üstünde hello Engagement Reach modülünü içeri aktarın:

      [...]
      #import "AEReachModule.h"
* Yöntemi içinde `applicationDidFinishLaunching:` veya `application:didFinishLaunchingWithOptions:`, bir reach modülü oluşturun ve tooyour mevcut Engagement başlatma satır geçirme:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Değiştirme **'icon.png'** dize bildirim simgesi olarak istediğiniz hello görüntü adı ile.
* Toouse hello seçenek istiyorsanız *güncelleştirme rozet değeri* Reach kampanyaları veya toouse yerel gönderim isteyip istemediğinizi \<SaaS/Reach API'sini/Kampanya biçimi/yerel anında iletme\> kampanyalar, hello Reach modülünün yönetmenize izin gerekir (bunu hello uygulama gösterge otomatik olarak temizlemek ve ayrıca başlatılmadı veya foregrounded hello uygulama her zaman Engagement tarafından depolanan hello değerini sıfırlamak) hello rozet simgesi kendisi. Bu satırı Reach modülü başlatma sonra aşağıdaki hello ekleyerek yapılır:

      [reach setAutoBadgeEnabled:YES];
* Toohandle Reach veri gönderimi istiyorsanız, uygulama temsilcinizi toohello uygun izin vermelisiniz `AEReachDataPushDelegate` protokolü. Satır Reach modülü başlatma sonra aşağıdaki hello ekleyin:

      [reach setDataPushDelegate:self];
* Merhaba yöntemleri uygulayabilirsiniz sonra `onDataPushStringReceived:` ve `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` uygulama temsilcinizi içinde:

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

### <a name="category"></a>Kategori
Merhaba kategori parametresi bir veri gönderme kampanya oluşturduğunuzda isteğe bağlıdır ve toofilter verileri iter sağlar. Toopush farklı tür istiyorsanız kullanışlıdır, `Base64` veri ve istediğiniz tooidentify bunları ayrıştırma önce kendi türü.

**Hazır tooreceive ve görüntü içeriğini ulaşmak şimdi uygulamanızı değil!**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>Nasıl tooreceive duyuruları ve yoklamaları herhangi bir zamanda
Engagement Reach bildirim tooyour son kullanıcıların herhangi bir zamanda hello Apple anında iletilen bildirim Servisi'ni kullanarak gönderebilirsiniz.

tooenable bu işlevselliği Apple anında iletme bildirimleri için uygulamanızı tooprepare varsa ve uygulama temsilcinizi değiştirme.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Uygulamanızın Apple anında iletme bildirimleri için hazırlama
Lütfen başlangıç kılavuzunu izleyin: [nasıl tooPrepare uygulamanız için Apple anında iletme bildirimleri](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Merhaba gerekli istemci kodu ekleyin
*Bu noktada, uygulamanızın kayıtlı bir Apple anında iletme sertifika hello katılım ön ucunda olması gerekir.*

Henüz yapmadıysanız, uygulama tooreceive anında iletme bildirimleri tooregister gerekir.

* İçeri aktarma hello `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>
* Uygulamanız başladığında satır aşağıdaki hello ekleyin (genellikle, `application:didFinishLaunchingWithOptions:`):

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

Ardından, tooprovide tooEngagement hello cihaz belirteci Apple sunucuları tarafından döndürülen gerekir. Bu adlı hello yönteminde yapılır `application:didRegisterForRemoteNotificationsWithDeviceToken:` uygulama temsilcinizi içinde:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

Son olarak, uygulamanızın uzak bir bildirim aldığında tooinform hello Engagement SDK'sı olması. çağrı, toodo hello yöntemi `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` uygulama temsilcinizi içinde:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> Varsayılan olarak, Engagement Reach hello completionHandler denetler. Toomanually yanıt toohello istiyorsanız `handler` kodunuzda engellemek, hello nil geçirebilirsiniz `handler` bağımsız değişkeni ve denetim hello tamamlama kendiniz engelleyin. Merhaba bkz `UIBackgroundFetchResult` olası değerler listesi türü.
>
>

### <a name="full-example"></a>Tam örnek
Tümleştirme tam bir örneği burada verilmiştir:

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

## <a name="how-toocustomize-campaigns"></a>Nasıl toocustomize Kampanyalar
### <a name="notifications"></a>Bildirimler
Bildirimler iki tür vardır: Sistem ve uygulama içi bildirimler.

Sistem bildirimleri iOS tarafından işlenir ve özelleştirilemez.

Uygulama bildirimleri toohello geçerli uygulama penceresi dinamik olarak eklenen bir görünümünü yapılır. Bu bildirim bir katmana çağrılır. Uygulamanız herhangi bir görünümde, toomodify bunlar gerekli olmadığı için bildirim yer paylaşımları hızlı tümleştirme için mükemmeldir.

#### <a name="layout"></a>Düzen
Uygulama bildirimlerinizi toomodify hello görünümünü, yalnızca değiştirebileceğiniz hello dosya `AENotificationView.xib` hello etiket değerlerini ve hello varolan subviews türleri tutmak sürece tooyour gerekiyor.

Varsayılan olarak, uygulama içi bildirimler hello ekranın hello altında sunulur. Toodisplay tercih ederseniz, bunları ekran, düzenleme hello hello üstündeki sağlanan `AENotificationView.xib` hello değiştirip `AutoSizing` kendi değerlendirmesi hello üstünde tutulabilir şekilde hello ana görünüm özelliği.

#### <a name="categories"></a>Kategoriler
Düzen sağlanan hello değiştirdiğinizde, tüm bildirimlerinizi hello görünümünü değiştirin. Çeşitli hedeflenen toodefine (büyük olasılıkla davranışları) bildirimleri için görünür kategoriler. Bir kategori Reach kampanya oluşturduğunuzda belirtilebilir. Bu belgenin sonraki bölümlerinde açıklanan kategoriler de duyuruları ve yoklamaları, özelleştirmenize olanak tanır olduğunu aklınızda bulundurun.

tooregister bildirimlerinizi için bir kategori işleyici, hello modülü ulaştığınızda bir çağrı başlatılmış tooadd gerekir.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`toohello Protokolü uyan bir nesne örneği olmalıdır `AENotifier`.

Kendi kendinize hello Protokolü yöntemleri uygulayabilirsiniz veya tooreimplement hello varolan sınıf seçebilir `AEDefaultNotifier` hello çalışmanın çoğu zaten gerçekleştirir.

Örneğin, belirli bir kategorideki için tooredefine hello bildirim görünümü istiyorsanız, bu örnek izleyebilirsiniz:

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

Bu basit örnek kategorisinin varsayalım adında bir dosyanız varsa `MyNotificationView.xib` ana uygulama paket içindeki. Merhaba yöntemi karşılık gelen mümkün toofind değilse `.xib`hello bildirim görüntülenmez ve katılım hello konsolunda bir ileti çıktı.

sağlanan hello nib dosyası kuralları aşağıdaki hello saygı:

* Yalnızca bir görünüm içermesi gerekir.
* Subviews aynı olanları adlı sağlanan hello nib dosyası içinde hello gibi türleri hello olması`AENotificationView.xib`
* Aynı adlı sağlanan hello nib dosyası içinde olanları hello gibi etiketler hello subviews olmalıdır`AENotificationView.xib`

> [!TIP]
> Yalnızca, adlı sağlanan hello nib dosya kopyalama `AENotificationView.xib`ve buradan çalışmaya başlayın. Ancak dikkatli olun, bu nib dosya iç ilişkili toohello sınıf görünümü hello `AENotificationView`. Bu sınıf hello yöntemi yeniden tanımlandı `layoutSubViews` toomove ve toocontext göre kendi subviews yeniden boyutlandırın. Tooreplace isteyebilirsiniz ile bir `UIView` ya da size özel görünüm sınıfı.
>
>

Daha derin özelleştirme bildirimlerinizi (örneğin tooload görünümünüzden doğrudan hello kod istiyorsanız) gerekiyorsa, hello göz sağlanan kaynak kodu ve sınıf belgelerine tootake önerilir `Protocol ReferencesDefaultNotifier` ve `AENotifier`.

Kullanabileceğiniz Not hello birden çok kategori için aynı bildirim.

Aynı zamanda yeniden tanımlanan hello varsayılan bildirim şöyle olabilir:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Bildirim işleme
Merhaba varsayılan kategori kullanırken, bazı yaşam döngüsü yöntemleri üzerinde hello denir `AEReachContent` nesne tooreport istatistikleri ve güncelleştirme hello kampanya durumu:

* Merhaba bildirim uygulamada görüntülendiğinde hello `displayNotification` yöntemi (hangi istatistikleri raporları) çağrılır tarafından `AEReachModule` varsa `handleNotification:` döndürür `YES`.
* Merhaba bildirim kapatıldığında, hello `exitNotification` yöntemi çağrıldığında, istatistik bildirilir ve sonraki Kampanyalar şimdi işlenebilir.
* Merhaba bildirim tıkladıysanız `actionNotification` olduğu adlı istatistik bildirilir ve ilişkili hello eylem gerçekleştirilir.

Uygulamanıza `AENotifier` atlamaların hello varsayılan davranışı, toocall bu yaşam döngüsü yöntemleri başınıza gerekir. Örnek hello hello varsayılan davranışı burada atlanır bazı durumlarda gösterilmiştir:

* Genişletme yok `AEDefaultNotifier`, sıfırdan kategori işleme uygulanan örn.
* Geçersiz kılınmış `prepareNotificationView:forContent:`emin toomap olması en az `onNotificationActioned` veya `onNotificationExited` U.I denetimlerin tooone.

> [!WARNING]
> Varsa `handleNotification:` bir özel durum, içerik hello silinir ve `drop` olduğu çağrılır, bu istatistiklerine bildirilir ve sonraki Kampanyalar şimdi işlenebilir.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Bildirim var olan bir görünümü bir parçası olarak dahil
Yer paylaşımları hızlı tümleştirme için oldukça uygundur ancak bazen uygun olamaz ya da istenmeyen yan etkileri olabilir.

Merhaba katmana sistem bazı görünümlerinizi memnun değilseniz, bu görünümleri için özelleştirebilirsiniz.

Varolan görünümlerinizi tooinclude bizim bildirim düzeni karar verebilirsiniz. toodo bu nedenle, iki uygulama stili vardır:

1. Arabirim Oluşturucusu'nu kullanarak hello bildirim görünümü ekleme

   * Açık *arabirim Oluşturucusu*
   * 320 x 60'ı (ya da iPad cihazında varsa 768 x 60) koyun `UIView` hello bildirim tooappear istediğiniz
   * Bu görünüm için Hello etiket değeri çok ayarlayın: **36822491**
2. Merhaba bildirim görünümü programlı olarak ekleyin. Görünümünüzü hazırlarken koddan hello eklemeniz yeterlidir:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

`NOTIFICATION_AREA_VIEW_TAG`Makro bulunabilir `AEDefaultNotifier.h`.

> [!NOTE]
> Merhaba varsayılan bildirim hello bildirim düzenini bu görünüme dahil edilmiştir ve bir katmana için eklemez otomatik olarak algılar.
>
>

### <a name="announcements-and-polls"></a>Duyuruları ve yoklamaları
#### <a name="layouts"></a>Düzenleri
Merhaba dosyalarda değişiklik yapabilir `AEDefaultAnnouncementView.xib` ve `AEDefaultPollView.xib` hello etiket değerlerini ve hello varolan subviews türleri tutmak sürece.

#### <a name="categories"></a>Kategoriler
##### <a name="alternate-layouts"></a>Alternatif düzenleri
Bildirimler gibi hello kampanya kategori duyuruları ve yoklamaları için kullanılan toohave alternatif düzenleri olabilir.

toocreate duyuru için bir kategori, genişlemelidir **AEAnnouncementViewController** ve hello reach modülünün başlatıldıktan sonra kaydedin:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Bir kullanıcı hello kategorisiyle duyuru için bir bildirim her tıkladığınızda "Benim\_kategori", kayıtlı görünüm denetleyicinizi (Bu durumda `MyCustomAnnouncementViewController`) hello yöntemi çağrılarak başlatılır `initWithAnnouncement:` ve hello görünümü olacaktır eklenen toohello geçerli uygulama penceresi.
>
>

Uygulamanızda hello `AEAnnouncementViewController` tooread hello özelliği olacaktır sınıfı `announcement` tooinitialize, subviews. Merhaba aşağıdaki örnekte, iki yapmayı düşünebilirsiniz etiketleri kullanarak başlatılır `title` ve `body` hello özelliklerini `AEReachAnnouncement` sınıfı:

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

Tooload görünümlerinizi başınıza istemediğiniz ancak yalnızca tooreuse hello varsayılan duyuru görünüm düzeni istediğiniz, özel görünüm denetleyicinizi yalnızca yapabileceğiniz sağlanan hello sınıfını genişleten `AEDefaultAnnouncementViewController`. Bu durumda, hello nib dosya yinelenen `AEDefaultAnnouncementView.xib` ve özel görünüm denetleyicisi tarafından yüklenebilmesi için yeniden adlandırın (adlı bir denetleyici için `CustomAnnouncementViewController`, nib dosyanızı çağırmalıdır `CustomAnnouncementView.xib`).

tooreplace hello varsayılan kategorisini Duyurular, yalnızca özel görünüm denetleyicinizi tanımlanan hello kategorisi için kayıt `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Anketler, özelleştirilmiş hello olabilir aynı şekilde:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Bu süre, sağlanan hello `MyCustomPollViewController` genişletmelidir `AEPollViewController`. Veya hello varsayılan denetleyicisinden tooextend seçebilirsiniz: `AEDefaultPollViewController`.

> [!IMPORTANT]
> Toocall ya da unutmayın `action` (`submitAnswers:` özel yoklama görünüm denetleyicileri için) veya `exit` hello görünüm denetleyicisini kapatıldığında önce yöntemi. Aksi takdirde istatistikleri (yani hello kampanyası hiçbir analytics) gönderilmez ve hello uygulama işlemini yeniden başlatılana kadar daha fazla önemlisi sonraki Kampanyalar bildirilmez.
>
>

##### <a name="implementation-example"></a>Uygulama örneği
Bu uygulama hello özel duyuru görünümü bir dış xib dosyasından yüklenir.

Gibi gelişmiş bildirim özelleştirmesi hello kaynak koduna hello standart uygulama toolook önerilir.

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
