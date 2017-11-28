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
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a><span data-ttu-id="58724-103">Xamarin.iOS Uygulamaları için Azure Mobile Engagement kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="58724-103">Get Started with Azure Mobile Engagement for Xamarin.iOS Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="58724-104">Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar bir Xamarin.iOS uygulaması.</span><span class="sxs-lookup"><span data-stu-id="58724-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users in a Xamarin.iOS application.</span></span>
<span data-ttu-id="58724-105">Bu öğreticide, temel verileri toplayan ve Apple Anında İletme Bildirimi Sistemi’ni (APNS) kullanarak anında iletme bildirimleri alan boş bir Xamarin.iOS uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="58724-105">In this tutorial, you create a blank Xamarin.iOS app that collects basic data and receives push notifications using Apple Push Notification System (APNS).</span></span>

> [!NOTE]
> <span data-ttu-id="58724-106">Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir.</span><span class="sxs-lookup"><span data-stu-id="58724-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="58724-107">Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="58724-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="58724-108">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="58724-108">This tutorial requires hello following:</span></span>

* <span data-ttu-id="58724-109">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="58724-109">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="58724-110">Xamarin ile Visual Studio’yu da kullanabilirsiniz, ancak bu öğretici Xamarin Studio'yu kullanır.</span><span class="sxs-lookup"><span data-stu-id="58724-110">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="58724-111">Yükleme yönergeleri için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="58724-111">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span> 
* [<span data-ttu-id="58724-112">Mobile Engagement Xamarin SDK</span><span class="sxs-lookup"><span data-stu-id="58724-112">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="58724-113">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="58724-113">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="58724-114">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58724-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="58724-115">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="58724-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="58724-116"><a id="setup-azme"></a>iOS uygulamanız için Mobile Engagement kurma</span><span class="sxs-lookup"><span data-stu-id="58724-116"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="58724-117"><a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="58724-117"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="58724-118">Bu öğreticide hello en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir "temel tümleştirme" gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="58724-118">This tutorial presents a "basic integration" which is hello minimal set required toocollect data and send a push notification.</span></span>

<span data-ttu-id="58724-119">Xamarin toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="58724-119">We will create a basic app with Xamarin toodemonstrate hello integration:</span></span>

### <a name="create-a-new-xamarinios-project"></a><span data-ttu-id="58724-120">Yeni bir Xamarin.iOS projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="58724-120">Create a new Xamarin.iOS project</span></span>
1. <span data-ttu-id="58724-121">Xamarin Studio’yu başlatın.</span><span class="sxs-lookup"><span data-stu-id="58724-121">Launch Xamarin Studio.</span></span> <span data-ttu-id="58724-122">Çok Git**dosya** -> **yeni** -> **çözümü**</span><span class="sxs-lookup"><span data-stu-id="58724-122">Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="58724-123">Seçin **Single View uygulaması**, seçili hello dil olduğundan emin olun **C#** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="58724-123">Select **Single View App**, make sure hello selected language is **C#** and then click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="58724-124">Hello dolgu **App Name** ve hello **kuruluş tanımlayıcı** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="58724-124">Fill in hello **App Name** and hello **Organization Identifier** and then click **Next**.</span></span> 
   
    ![][3]
   
   > [!IMPORTANT]
   > <span data-ttu-id="58724-125">Yayımlama profilini, iOS uygulamanızın tam olarak hello burada sahip olduğunuz paket tanımlayıcısı'ile eşleşen bir uygulama kimliği kullanarak toodeploy kullanıp sonunda bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="58724-125">Make sure that hello publishing profile you eventually use toodeploy your iOS app is using an App ID which matches exactly with hello Bundle Identifier you have here.</span></span> 
   > 
   > 
4. <span data-ttu-id="58724-126">Güncelleştirme hello **proje adı**, **çözüm adı** ve **konumu** gerekli ve tıklatırsanız **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="58724-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="58724-127">Xamarin Studio biz Mobile Engagement tümleştirecek hello tanıtım uygulamasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="58724-127">Xamarin Studio will create hello demo app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="58724-128">Uygulamanızın tooMobile Engagement arka ucuna bağlanmak</span><span class="sxs-lookup"><span data-stu-id="58724-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="58724-129">Merhaba sağ tıklayın **paketleri** seçip hello çözüm windows klasörü **paketleri Ekle...**</span><span class="sxs-lookup"><span data-stu-id="58724-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="58724-130">Merhaba Ara **Microsoft Azure Mobile Engagement Xamarin SDK** ve tooyour çözüme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="58724-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="58724-131">Açık **AppDelegate.cs** ve hello aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="58724-131">Open **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
4. <span data-ttu-id="58724-132">Merhaba, **FinishedLaunching** yöntemi, Mobile Engagement arka ucuyla tooinitialize hello bağlantıyı izleyerek hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="58724-132">In hello **FinishedLaunching** method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="58724-133">Tooadd emin olun, **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="58724-133">Make sure tooadd your **ConnectionString**.</span></span> <span data-ttu-id="58724-134">Bu kodu aynı zamanda bir kukla kullanır **Notificationıcon** hello istediğiniz Mobile Engagement SDK tarafından eklenen tooreplace.</span><span class="sxs-lookup"><span data-stu-id="58724-134">This code also uses a dummy **NotificationIcon** which is added by hello Mobile Engagement SDK which you may want tooreplace.</span></span> 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <span data-ttu-id="58724-135"><a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="58724-135"><a id="monitor"></a>Enabling real-time monitoring</span></span>
<span data-ttu-id="58724-136">Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran toohello Mobile Engagement arka göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="58724-136">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="58724-137">Açık **ViewController.cs** ve hello aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="58724-137">Open **ViewController.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Xamarin;
2. <span data-ttu-id="58724-138">Merhaba sınıfı Değiştir `ViewController` devraldığı `UIViewController` çok`EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="58724-138">Replace hello class from which `ViewController` inherits from `UIViewController` too`EngagementViewController`.</span></span> 

## <span data-ttu-id="58724-139"><a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama</span><span class="sxs-lookup"><span data-stu-id="58724-139"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="58724-140"><a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="58724-140"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="58724-141">Mobile Engagement anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında toointeract kullanıcılarınız ve REACH sağlar.</span><span class="sxs-lookup"><span data-stu-id="58724-141">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="58724-142">Bu modül hello Mobile Engagement portalında REACH adı verilir.</span><span class="sxs-lookup"><span data-stu-id="58724-142">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="58724-143">Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="58724-143">hello following sections set up your app tooreceive them.</span></span>

### <a name="modify-your-application-delegate"></a><span data-ttu-id="58724-144">Uygulama Temsilcinizi değiştirme</span><span class="sxs-lookup"><span data-stu-id="58724-144">Modify your Application Delegate</span></span>
1. <span data-ttu-id="58724-145">Açık hello **AppDelegate.cs** ve hello aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="58724-145">Open hello **AppDelegate.cs** and add hello following using statement:</span></span>
   
        using System; 
2. <span data-ttu-id="58724-146">Şimdi hello içinde `FinishedLaunching` yöntemi, anında iletileri sonra tooregister aşağıdaki hello ekleme`EngagementAgent.init(...)`</span><span class="sxs-lookup"><span data-stu-id="58724-146">Now inside hello `FinishedLaunching` method, add hello following tooregister for push messages after `EngagementAgent.init(...)`</span></span>
   
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
3. <span data-ttu-id="58724-147">Son olarak - güncelleştirin veya aşağıdaki yöntemleri hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="58724-147">Finally - update or add hello following methods:</span></span>
   
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
4. <span data-ttu-id="58724-148">İçinde **Info.plist** dosya hello çözümde, bu hello onaylayın **paket tanımlayıcı** hello ile eşleşen **uygulama kimliği** hello Apple Dev sağlama profilinizde sahip Merkezi.</span><span class="sxs-lookup"><span data-stu-id="58724-148">In your **Info.plist** file in hello solution, confirm that hello **Bundle Identifier** matches with hello **App ID** you have in your provisioning profile in hello Apple Dev Center.</span></span> 
   
    ![][7]
5. <span data-ttu-id="58724-149">İçinde aynı hello **Info.plist** dosya, hello işaretli olduğundan emin olun **arka plan modlarını etkinleştir** ve **uzak bildirimler**.</span><span class="sxs-lookup"><span data-stu-id="58724-149">In hello same **Info.plist** file, make sure that you have checked hello **Enable Background Modes** and **Remote Notifications**.</span></span> 
   
     ![][8]
6. <span data-ttu-id="58724-150">Bu yayımlama profiliyle ilişkilendirdiğiniz hello cihazda Hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="58724-150">Run hello app on hello device you have associated with this publishing profile.</span></span> 

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
