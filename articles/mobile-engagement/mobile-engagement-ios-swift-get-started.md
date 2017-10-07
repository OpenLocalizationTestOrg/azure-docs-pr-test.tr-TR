---
title: "swift'te iOS için Azure Mobile Engagement başlangıç aaaGet | Microsoft Docs"
description: "Bilgi nasıl iOS uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 196c282d-6f2f-4cbc-aeee-6517c5ad866d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: swift
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: piyushjo
ms.openlocfilehash: 9a3841d305745f8b80c6b0c86aabe18e0c7c0e59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-swift"></a>Swift’te iOS Uygulamaları için Azure Mobile Engagement Kullanmaya Başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar tooan iOS uygulaması.
Bu öğreticide, temel verileri toplayan ve Apple Anında İletme Bildirimi Sistemi’ni (APNS) kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturursunuz.

Bu öğretici hello aşağıdakileri gerektirir:

* MAC App Store'dan yükleyebileceğiniz XCode 8
* Merhaba [Mobile Engagement iOS SDK'sı]
* Apple Dev Center'ınızda edinebileceğiniz anında iletme bildirimi sertifikası (.p12)

> [!NOTE]
> Bu öğreticide Swift sürüm 3.0 kullanılmaktadır. 
> 
> 

Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin tüm Mobile Engagement öğreticileri için önkoşuldur.

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-swift-get-started).
> 
> 

## <a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir. Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement iOS SDK tümleştirmesi](mobile-engagement-ios-sdk-overview.md)

XCode toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız:

### <a name="create-a-new-ios-project"></a>Yeni bir iOS projesi oluşturma
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toomobile-engagement-backend"></a>Uygulamanızın tooMobile Engagement arka ucuna bağlanmak
1. Merhaba karşıdan [Mobile Engagement iOS SDK'sı]
2. Merhaba ayıklayın. tar.gz dosyasını bilgisayarınızdaki tooa klasöre
3. Merhaba projeyi sağ tıklatın ve seçin "çok dosyaları Ekle..."
   
    ![][1]
4. Ayıkladığınız hello SDK ve select hello toohello klasöre gidin `EngagementSDK` klasörünü seçip Tamam'a basın.
   
    ![][2]
5. Açık hello `Build Phases` sekmesi ve hello `Link Binary With Libraries` menü hello çerçeveleri aşağıda gösterildiği gibi ekleyin:
   
    ![][3]
6. Dosya seçerek bir köprü oluşturma üst bilgisi toobe mümkün toouse hello SDK'ın Objective C API'lerini oluşturma > Yeni > Dosya > iOS > kaynak > üst bilgi dosyası.
   
    ![][4]
7. Üstbilgi dosyası tooexpose Mobile Engagement Objective-C kodunu tooyour SWIFT kodu köprüleme hello düzenleme, içeri aktarmalar aşağıdaki hello ekleyin:
   
        /* Mobile Engagement Agent */
        #import "AEModule.h"
        #import "AEPushMessage.h"
        #import "AEStorage.h"
        #import "EngagementAgent.h"
        #import "EngagementTableViewController.h"
        #import "EngagementViewController.h"
        #import "AEUserNotificationHandler.h"
        #import "AEIdfaProvider.h"
8. Derleme Ayarları'nda bir yol toothis üstbilgisi hello Objective-C köprü oluşturma üst bilgisi derleme ayarının Swift derleyicisi - kod oluşturma altında olduğundan emin olun. Yol için bir örnek şudur: **$(SRCROOT)/MySuperApp/MySuperApp-Bridging-Header.h (bağlı olarak hello yolu)**
   
   ![][6]
9. Toohello uygulamanızın Azure portalında dön *bağlantı bilgisi* sayfası ve kopyalama hello bağlantı dizesi
   
   ![][5]
10. Şimdi hello hello bağlantı dizesini yapıştırın `didFinishLaunchingWithOptions` temsilci seçme
    
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool
        {
              [...]
                EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}")
              [...]
        }

## <a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme
Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.

1. Açık hello **ViewController.swift** dosya ve hello temel sınıfını değiştirme **ViewController** toobe **EngagementViewController**:
   
    `class ViewController : EngagementViewController {`

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında İletme Bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement hello Kampanyalar bağlamında toointeract ve anında iletme bildirimleri ve uygulama içi Mesajlaşma ile kullanıcılarınız erişim sağlar. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Merhaba aşağıdaki bölümlerde, app tooreceive Kurulum bunları.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Uygulama tooreceive sessiz anında iletme bildirimlerini etkinleştirme
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Merhaba ulaşma kitaplığı tooyour projesini ekleyin
1. Projenize sağ tıklayın
2. `Add file too...` seçeneğini belirleyin
3. Merhaba SDK'sını ayıkladığınız toohello klasöre gidin
4. Select hello `EngagementReach` klasörü
5. Ekle'ye tıklayın.
6. Mobile Engagement Objective-C Reach üst bilgi dosyası tooexpose üstbilgileri köprüleme hello düzenleyin ve hello aşağıdaki içeri aktarmaları ekleyin:
   
        /* Mobile Engagement Reach */
        #import "AEAnnouncementViewController.h"
        #import "AEAutorotateView.h"
        #import "AEContentViewController.h"
        #import "AEDefaultAnnouncementViewController.h"
        #import "AEDefaultNotifier.h"
        #import "AEDefaultPollViewController.h"
        #import "AEInteractiveContent.h"
        #import "AENotificationView.h"
        #import "AENotifier.h"
        #import "AEPollViewController.h"
        #import "AEReachAbstractAnnouncement.h"
        #import "AEReachAnnouncement.h"
        #import "AEReachContent.h"
        #import "AEReachDataPush.h"
        #import "AEReachDataPushDelegate.h"
        #import "AEReachModule.h"
        #import "AEReachNotifAnnouncement.h"
        #import "AEReachPoll.h"
        #import "AEReachPollQuestion.h"
        #import "AEViewControllerUtil.h"
        #import "AEWebAnnouncementJsBridge.h"

### <a name="modify-your-application-delegate"></a>Uygulama Temsilcinizi değiştirme
1. İç hello `didFinishLaunchingWithOptions` - reach modülü oluşturun ve tooyour mevcut Engagement başlatma satır geçirme:
   
        func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool 
        {
            let reach = AEReachModule.module(withNotificationIcon: UIImage(named:"icon.png")) as! AEReachModule
            EngagementAgent.init("Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}", modulesArray:[reach])
            [...]
            return true
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Uygulama tooreceive APNS anında iletme bildirimlerini etkinleştirme
1. Satır toohello aşağıdaki hello eklemek `didFinishLaunchingWithOptions` yöntemi:
   
        if #available(iOS 8.0, *)
        {
            if #available(iOS 10.0, *)
            {
                UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (granted, error) in }
            }else
            {
                let settings = UIUserNotificationSettings(types: [.alert, .badge, .sound], categories: nil)
                application.registerUserNotificationSettings(settings)
            }
            application.registerForRemoteNotifications()
        }
        else
        {
            application.registerForRemoteNotifications(matching: [.alert, .badge, .sound])
        }
2. Merhaba eklemek `didRegisterForRemoteNotificationsWithDeviceToken` yöntemini aşağıdaki şekilde:
   
        func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
            EngagementAgent.shared().registerDeviceToken(deviceToken)
        }
3. Merhaba eklemek `didReceiveRemoteNotification:fetchCompletionHandler:` yöntemini aşağıdaki şekilde:
   
        func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
            EngagementAgent.shared().applicationDidReceiveRemoteNotification(userInfo, fetchCompletionHandler:completionHandler)
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK'sı]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-swift-get-started/add-header-file.png
[5]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
[6]: ./media/mobile-engagement-ios-swift-get-started/add-bridging-header.png
