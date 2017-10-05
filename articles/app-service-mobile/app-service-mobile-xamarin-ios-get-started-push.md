---
title: "Xamarin.iOS uygulamanızı Azure App Service için anında iletme bildirimleri ekleme"
description: "Azure uygulama hizmeti Xamarin.iOS uygulamanızı anında iletme bildirimleri göndermek için nasıl kullanılacağını öğrenin"
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
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="23471-103">Xamarin.iOS uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="23471-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="23471-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="23471-104">Overview</span></span>
<span data-ttu-id="23471-105">Bu öğreticide, anında iletme bildirimleri ekleme [Xamarin.iOS Hızlı Başlangıç](app-service-mobile-xamarin-ios-get-started.md) proje böylece bir kayda eklenen her zaman bir anında iletme bildirimi cihaza gönderilir.</span><span class="sxs-lookup"><span data-stu-id="23471-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="23471-106">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, anında iletme bildirimi uzantısı paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="23471-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="23471-107">Bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="23471-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23471-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="23471-108">Prerequisites</span></span>
* <span data-ttu-id="23471-109">Tamamlamak [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="23471-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="23471-110">Fiziksel bir iOS cihazına.</span><span class="sxs-lookup"><span data-stu-id="23471-110">A physical iOS device.</span></span> <span data-ttu-id="23471-111">Anında iletme bildirimlerini iOS simülatörü tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="23471-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="23471-112">Apple Geliştirici portalındaki anında iletme bildirimleri için uygulamanızı kaydetmeniz</span><span class="sxs-lookup"><span data-stu-id="23471-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="23471-113">Anında iletme bildirimleri göndermek için mobil uygulama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="23471-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="23471-114">Güncelleştirme anında iletme bildirimleri göndermek için sunucu projesi</span><span class="sxs-lookup"><span data-stu-id="23471-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="23471-115">Xamarin.iOS projesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="23471-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="23471-116">Uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="23471-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="23471-117">İçinde **QSTodoService**, aşağıdaki özellik eklemek için **AppDelegate** mobil istemci elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="23471-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
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
2. <span data-ttu-id="23471-118">Aşağıdakileri ekleyin `using` deyimi üstüne **AppDelegate.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="23471-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="23471-119">İçinde **AppDelegate**, geçersiz kılma **FinishedLaunching** olay:</span><span class="sxs-lookup"><span data-stu-id="23471-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="23471-120">Aynı dosyada geçersiz kılma **RegisteredForRemoteNotifications** olay.</span><span class="sxs-lookup"><span data-stu-id="23471-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="23471-121">Bu kod sunucu tarafından tüm desteklenen platformlarda gönderilecek basit bir şablon bildirim kaydediyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="23471-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="23471-122">Notification Hubs ile şablonları hakkında daha fazla bilgi için bkz: [şablonları](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="23471-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="23471-123">Ardından, geçersiz kılma **DidReceivedRemoteNotification** olay:</span><span class="sxs-lookup"><span data-stu-id="23471-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="23471-124">Uygulamanıza anında iletme bildirimlerini desteklemek üzere güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="23471-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="23471-125"><a name="test"></a>Test, uygulamanızda anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="23471-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="23471-126">Tuşuna **çalıştırmak** projeyi oluşturun ve uygulamayı bir iOS özellikli aygıtı Başlat düğmesine ve ardından **Tamam** anında iletme bildirimleri kabul etmek için.</span><span class="sxs-lookup"><span data-stu-id="23471-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23471-127">Anında iletme bildirimleri, uygulamanızdan açıkça kabul etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="23471-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="23471-128">Bu istek, yalnızca uygulamayı çalıştıran ilk kez oluşur.</span><span class="sxs-lookup"><span data-stu-id="23471-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="23471-129">Uygulamasında bir görevi yazın ve ardından artı (**+**) simgesi.</span><span class="sxs-lookup"><span data-stu-id="23471-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="23471-130">Bir bildirim alındı ve ardından doğrulamak **Tamam** bildirim kapatılamadı.</span><span class="sxs-lookup"><span data-stu-id="23471-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="23471-131">2. adımı yineleyin ve hemen uygulamasını kapatın, sonra bir bildirim göründüğünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="23471-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="23471-132">Bu öğreticiyi başarıyla tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="23471-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



