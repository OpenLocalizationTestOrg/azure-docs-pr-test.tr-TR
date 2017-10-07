---
title: "Azure uygulama hizmeti ile aaaAdd anında iletme bildirimleri tooyour Xamarin.iOS uygulaması"
description: "Nasıl toouse Azure App Service toosend anında bildirimler tooyour Xamarin.iOS uygulaması öğrenin"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>Anında iletme bildirimleri tooyour Xamarin.iOS uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Xamarin.iOS Hızlı Başlangıç](app-service-mobile-xamarin-ios-get-started.md) bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello. Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.

## <a name="prerequisites"></a>Ön koşullar
* Tam hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) Öğreticisi.
* Fiziksel bir iOS cihazına. Anında iletme bildirimleri hello iOS simülatörü tarafından desteklenmez.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Apple Geliştirici portalındaki anında iletme bildirimleri için Hello uygulamasını Kaydet
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>Mobil uygulama toosend anında iletme bildirimleri yapılandırma
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>Güncelleştirme Hello sunucu projesi toosend anında iletme bildirimleri
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Xamarin.iOS projesi yapılandırma
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>Anında iletme bildirimleri tooyour uygulama Ekle
1. İçinde **QSTodoService**, özellik aşağıdaki hello eklemek için **AppDelegate** hello mobil istemci elde edebilirsiniz:
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. Merhaba aşağıdakileri ekleyin `using` hello deyimi toohello üst **AppDelegate.cs** dosya.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. İçinde **AppDelegate**, hello geçersiz kılma **FinishedLaunching** olay:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. Buna Merhaba aynı dosya, hello geçersiz kılma **RegisteredForRemoteNotifications** olay. Bu kodda hello sunucu tarafından tüm desteklenen platformlarda gönderilecek basit bir şablon bildirim kaydediyorsunuz.
   
    Notification Hubs ile şablonları hakkında daha fazla bilgi için bkz: [şablonları](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. Ardından, hello geçersiz kılma **DidReceivedRemoteNotification** olay:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

Uygulamanızı güncelleştirilmiş toosupport anında iletme bildirimleri sunulmuştur.

## <a name="test"></a>Test, uygulamanızda anında iletme bildirimleri
1. Tuşuna hello **çalıştırmak** düğmesini toobuild hello proje ve hello uygulamayı bir iOS özellikli aygıt başlatın, ardından **Tamam** tooaccept anında iletme bildirimleri.
   
   > [!NOTE]
   > Anında iletme bildirimleri, uygulamanızdan açıkça kabul etmeniz gerekir. Bu istek, yalnızca uygulama çalıştırır hello ilk kez hello oluşur.
   > 
   > 
2. Merhaba uygulamasında, bir görev yazın ve ardından hello artı (**+**) simgesi.
3. Bir bildirim alındı ve ardından doğrulamak **Tamam** toodismiss hello bildirim.
4. Adım 2 ve hemen kapat hello uygulama yineleyin ve sonra bir bildirim göründüğünü doğrulayın.

Bu öğreticiyi başarıyla tamamladınız.

<!-- Images. -->

<!-- URLs. -->



