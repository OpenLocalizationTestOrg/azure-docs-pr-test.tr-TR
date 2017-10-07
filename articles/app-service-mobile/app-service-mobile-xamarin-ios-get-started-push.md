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
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="a702d-103">Anında iletme bildirimleri tooyour Xamarin.iOS uygulaması ekleyin</span><span class="sxs-lookup"><span data-stu-id="a702d-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="a702d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a702d-104">Overview</span></span>
<span data-ttu-id="a702d-105">Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Xamarin.iOS Hızlı Başlangıç](app-service-mobile-xamarin-ios-get-started.md) bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.</span><span class="sxs-lookup"><span data-stu-id="a702d-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="a702d-106">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello.</span><span class="sxs-lookup"><span data-stu-id="a702d-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="a702d-107">Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a702d-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a702d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a702d-108">Prerequisites</span></span>
* <span data-ttu-id="a702d-109">Tam hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="a702d-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="a702d-110">Fiziksel bir iOS cihazına.</span><span class="sxs-lookup"><span data-stu-id="a702d-110">A physical iOS device.</span></span> <span data-ttu-id="a702d-111">Anında iletme bildirimleri hello iOS simülatörü tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="a702d-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="a702d-112">Apple Geliştirici portalındaki anında iletme bildirimleri için Hello uygulamasını Kaydet</span><span class="sxs-lookup"><span data-stu-id="a702d-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="a702d-113">Mobil uygulama toosend anında iletme bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a702d-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="a702d-114">Güncelleştirme Hello sunucu projesi toosend anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="a702d-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="a702d-115">Xamarin.iOS projesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a702d-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="a702d-116">Anında iletme bildirimleri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="a702d-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="a702d-117">İçinde **QSTodoService**, özellik aşağıdaki hello eklemek için **AppDelegate** hello mobil istemci elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a702d-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
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
2. <span data-ttu-id="a702d-118">Merhaba aşağıdakileri ekleyin `using` hello deyimi toohello üst **AppDelegate.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="a702d-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="a702d-119">İçinde **AppDelegate**, hello geçersiz kılma **FinishedLaunching** olay:</span><span class="sxs-lookup"><span data-stu-id="a702d-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="a702d-120">Buna Merhaba aynı dosya, hello geçersiz kılma **RegisteredForRemoteNotifications** olay.</span><span class="sxs-lookup"><span data-stu-id="a702d-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="a702d-121">Bu kodda hello sunucu tarafından tüm desteklenen platformlarda gönderilecek basit bir şablon bildirim kaydediyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="a702d-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="a702d-122">Notification Hubs ile şablonları hakkında daha fazla bilgi için bkz: [şablonları](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="a702d-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="a702d-123">Ardından, hello geçersiz kılma **DidReceivedRemoteNotification** olay:</span><span class="sxs-lookup"><span data-stu-id="a702d-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="a702d-124">Uygulamanızı güncelleştirilmiş toosupport anında iletme bildirimleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a702d-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="a702d-125"><a name="test"></a>Test, uygulamanızda anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="a702d-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="a702d-126">Tuşuna hello **çalıştırmak** düğmesini toobuild hello proje ve hello uygulamayı bir iOS özellikli aygıt başlatın, ardından **Tamam** tooaccept anında iletme bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="a702d-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a702d-127">Anında iletme bildirimleri, uygulamanızdan açıkça kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a702d-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="a702d-128">Bu istek, yalnızca uygulama çalıştırır hello ilk kez hello oluşur.</span><span class="sxs-lookup"><span data-stu-id="a702d-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="a702d-129">Merhaba uygulamasında, bir görev yazın ve ardından hello artı (**+**) simgesi.</span><span class="sxs-lookup"><span data-stu-id="a702d-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="a702d-130">Bir bildirim alındı ve ardından doğrulamak **Tamam** toodismiss hello bildirim.</span><span class="sxs-lookup"><span data-stu-id="a702d-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="a702d-131">Adım 2 ve hemen kapat hello uygulama yineleyin ve sonra bir bildirim göründüğünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a702d-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="a702d-132">Bu öğreticiyi başarıyla tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="a702d-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



