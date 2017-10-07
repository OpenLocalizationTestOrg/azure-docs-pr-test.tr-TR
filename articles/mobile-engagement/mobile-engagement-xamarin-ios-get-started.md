---
title: "aaaGet Xamarin.iOS için Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl toouse analizi ve Xamarin.iOS uygulamaları için anında iletme bildirimleri ile Azure Mobile Engagement."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Xamarin.iOS Uygulamaları için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar bir Xamarin.iOS uygulaması.
Bu öğreticide, temel verileri toplayan ve Apple Anında İletme Bildirimi Sistemi’ni (APNS) kullanarak anında iletme bildirimleri alan boş bir Xamarin.iOS uygulaması oluşturursunuz.

> [!NOTE]
> Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir. Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Bu öğretici hello aşağıdakileri gerektirir:

* [Xamarin Studio](http://xamarin.com/studio). Xamarin ile Visual Studio’yu da kullanabilirsiniz, ancak bu öğretici Xamarin Studio'yu kullanır. Yükleme yönergeleri için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx). 
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).
> 
> 

## <a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğreticide hello en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir "temel tümleştirme" gösterilmektedir.

Xamarin toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız:

### <a name="create-a-new-xamarinios-project"></a>Yeni bir Xamarin.iOS projesi oluşturma
1. Xamarin Studio’yu başlatın. Çok Git**dosya** -> **yeni** -> **çözümü** 
   
    ![][1]
2. Seçin **Single View uygulaması**, seçili hello dil olduğundan emin olun **C#** ve ardından **sonraki**.
   
    ![][2]
3. Hello dolgu **App Name** ve hello **kuruluş tanımlayıcı** ve ardından **sonraki**. 
   
    ![][3]
   
   > [!IMPORTANT]
   > Yayımlama profilini, iOS uygulamanızın tam olarak hello burada sahip olduğunuz paket tanımlayıcısı'ile eşleşen bir uygulama kimliği kullanarak toodeploy kullanıp sonunda bu hello emin olun. 
   > 
   > 
4. Güncelleştirme hello **proje adı**, **çözüm adı** ve **konumu** gerekli ve tıklatırsanız **oluşturma**.
   
    ![][4]

Xamarin Studio biz Mobile Engagement tümleştirecek hello tanıtım uygulamasını oluşturur. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Uygulamanızın tooMobile Engagement arka ucuna bağlanmak
1. Merhaba sağ tıklayın **paketleri** seçip hello çözüm windows klasörü **paketleri Ekle...**
   
    ![][5]
2. Merhaba Ara **Microsoft Azure Mobile Engagement Xamarin SDK** ve tooyour çözüme ekleyin.  
   
    ![][6]
3. Açık **AppDelegate.cs** ve hello aşağıdaki ekleme deyimini kullanarak:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. Merhaba, **FinishedLaunching** yöntemi, Mobile Engagement arka ucuyla tooinitialize hello bağlantıyı izleyerek hello ekleyin. Tooadd emin olun, **ConnectionString**. Bu kodu aynı zamanda bir kukla kullanır **Notificationıcon** hello istediğiniz Mobile Engagement SDK tarafından eklenen tooreplace. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme
Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran toohello Mobile Engagement arka göndermeniz gerekir.

1. Açık **ViewController.cs** ve hello aşağıdaki ekleme deyimini kullanarak:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Merhaba sınıfı Değiştir `ViewController` devraldığı `UIViewController` çok`EngagementViewController`. 

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında toointeract kullanıcılarınız ve REACH sağlar. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.

### <a name="modify-your-application-delegate"></a>Uygulama Temsilcinizi değiştirme
1. Açık hello **AppDelegate.cs** ve hello aşağıdaki ekleme deyimini kullanarak:
   
        using System; 
2. Şimdi hello içinde `FinishedLaunching` yöntemi, anında iletileri sonra tooregister aşağıdaki hello ekleme`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. Son olarak - güncelleştirin veya aşağıdaki yöntemleri hello ekleyin:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. İçinde **Info.plist** dosya hello çözümde, bu hello onaylayın **paket tanımlayıcı** hello ile eşleşen **uygulama kimliği** hello Apple Dev sağlama profilinizde sahip Merkezi. 
   
    ![][7]
5. İçinde aynı hello **Info.plist** dosya, hello işaretli olduğundan emin olun **arka plan modlarını etkinleştir** ve **uzak bildirimler**. 
   
     ![][8]
6. Bu yayımlama profiliyle ilişkilendirdiğiniz hello cihazda Hello uygulamayı çalıştırın. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
