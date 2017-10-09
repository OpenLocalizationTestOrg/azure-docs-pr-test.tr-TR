---
title: "Xamarin uygulamaları için Notification Hubs ile anında iletme bildirimleri aaaiOS | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooa Xamarin iOS uygulaması öğrenin."
services: notification-hubs
keywords: "ios anında iletme bildirimleri,anında iletme iletileri,anında iletme bildirimleri,anında iletme iletisi"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="2ba3e-104">Xamarin uygulamaları için Notification Hubs ile iOS Anında İletme Bildirimleri</span><span class="sxs-lookup"><span data-stu-id="2ba3e-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="2ba3e-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2ba3e-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2ba3e-106">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="2ba3e-107">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2ba3e-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="2ba3e-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="2ba3e-109">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan iOS uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="2ba3e-110">Hello kullanarak anında iletme bildirimleri alan boş bir Xamarin.iOS uygulaması oluşturacaksınız [Apple anında iletilen bildirim servisi (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="2ba3e-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="2ba3e-111">Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="2ba3e-112">Merhaba tamamlanmış kod hello kullanılabilir [NotificationHubs uygulaması] [ GitHub] örnek.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="2ba3e-113">Bu öğretici Notification Hubs ile Merhaba basit anında iletme iletisi yayımlama senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ba3e-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ba3e-114">Prerequisites</span></span>
<span data-ttu-id="2ba3e-115">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="2ba3e-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="2ba3e-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="2ba3e-117">iOS 7.0 (veya sonraki bir sürümü) uyumlu bir cihaz</span><span class="sxs-lookup"><span data-stu-id="2ba3e-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="2ba3e-118">iOS Developer Program üyeliği</span><span class="sxs-lookup"><span data-stu-id="2ba3e-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="2ba3e-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="2ba3e-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="2ba3e-120">İOS anında iletme bildirimlerinin yapılandırma gereksinimleri nedeniyle dağıtın ve hello benzetici yerine bir fiziksel iOS cihazında (iPhone veya iPad) hello örnek uygulamayı test.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="2ba3e-121">Bu öğreticiyi tamamlamak Xamarin iOS uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="2ba3e-122">Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2ba3e-122">Configure your notification hub</span></span>
<span data-ttu-id="2ba3e-123">Bu bölümde, yeni bir bildirim hub'ı oluşturma ve hello kullanarak APNS ile kimlik doğrulaması yapılandırma açıklanmaktadır **.p12** oluşturduğunuz bildirim sertifikası.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="2ba3e-124">Önceden oluşturduğunuz bir bildirim hub'ı toouse istiyorsanız, toostep 5 atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="2ba3e-125">Notification Hub ayarlarınızı, istediğimizden tıklatın hello Azure Portal'ın tooconfigure hello APNS bağlantısını istiyoruz gibi açmak <b>Bildirim Hizmetleri</b>ve ardından hello <b>Apple (APNS)</b> hello listedeki öğesi.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="2ba3e-126">Bunu yaptıktan sonra tıklayın <b>sertifikasını karşıya yükle</b> ve select hello <b>.p12</b> hello hello sertifikanın parolasını yanı sıra daha önce verilen sertifika.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="2ba3e-127">Emin tooselect olun <b>korumalı alan</b> itme göndereceğinizden modu geliştirme ortamında iletileri.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="2ba3e-128">Yalnızca hello kullan <b>üretim</b> zaten uygulamanızı hello mağazadan satın alan toosend anında iletme bildirimleri toousers isterseniz ayarı.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="2ba3e-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="2ba3e-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="2ba3e-130">Bildirim hub'ınız şimdi APNS ile yapılandırılmış toowork olan ve hello bağlantı dizeleri tooregister uygulamanızı çalıştırdıktan ve anında iletme bildirimleri göndermek.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="2ba3e-131">Uygulama toohello bildirim hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="2ba3e-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="2ba3e-132">Yeni bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="2ba3e-132">Create a new project</span></span>
1. <span data-ttu-id="2ba3e-133">Xamarin Studio'da yeni bir iOS projesi oluşturun ve seçin hello **Unified API** > **tek görünüm uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - Uygulama Türünü Seçme][31]
2. <span data-ttu-id="2ba3e-135">Bir başvuru toohello Azure Mesajlaşma bileşeni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="2ba3e-136">Merhaba Hello çözüm görünümü, sağ **bileşenleri** projeniz için klasör ve seçin **daha almak bileşenleri**.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="2ba3e-137">Merhaba Ara **Azure Mesajlaşma** bileşeni ve hello bileşen tooyour projeye ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="2ba3e-138">İçinde **AppDelegate.cs**, hello aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="2ba3e-139">Bir **SBNotificationHub** örneği bildirin:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="2ba3e-140">Oluşturma bir **Constants.cs** değişkenleri aşağıdaki hello sınıfıyla:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="2ba3e-141">İçinde **AppDelegate.cs**, güncelleştirme **FinishedLaunching()** toomatch hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="2ba3e-142">Merhaba geçersiz kılma **Appledelegate.cs** yönteminde **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="2ba3e-143">Merhaba geçersiz kılma **Appledelegate.cs** yönteminde **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="2ba3e-144">Merhaba aşağıdaki oluşturma **Appledelegate.cs** yönteminde **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="2ba3e-145">Toooverride seçebilirsiniz **FailedToRegisterForRemoteNotifications()** toohandle durumlar gibi ağ bağlantısı yok.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="2ba3e-146">Bu burada hello kullanıcı uygulamanızı çevrimdışı modda (örneğin, uçak) başlayabilir ve toohandle itme senaryolarında belirli tooyour uygulama içi mesajlaşmayı istediğiniz özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="2ba3e-147">Merhaba uygulama Cihazınızda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="2ba3e-148">Anında İletme Bildirimleri Gönderme</span><span class="sxs-lookup"><span data-stu-id="2ba3e-148">Sending Push Notifications</span></span>
<span data-ttu-id="2ba3e-149">Hello bildirimleri göndererek uygulamanızda anında iletme bildirimleri almayı test edebilirsiniz [Azure Portal] hello aracılığıyla **Test gönderimi** hello özelliği **sorun giderme** araç takımı, sağda ekranda hello aşağıda gösterildiği gibi hello bildirim hub'ı sayfasında.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="2ba3e-150">Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmeti aracılığıyla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="2ba3e-151">Bir kitaplık senaryonuzda kullanılabilir değilse, toosend anında iletme iletileri doğrudan hello REST API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="2ba3e-152">Bu öğreticide, biz basit tutmak ve yalnızca arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için hello .NET SDK kullanarak bildirim göndererek istemci uygulamanızı test etme gösterin.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="2ba3e-153">Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) hello bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="2ba3e-154">Ancak, aşağıdaki yaklaşımlardan hello bildirim göndermek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="2ba3e-155">**REST arabirimi**: hello kullanarak herhangi bir arka uç platformunda anında iletme bildirimi destekleyebilir [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="2ba3e-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="2ba3e-156">**Microsoft Azure Notification Hubs .NET SDK'sı**: hello Visual Studio için Nuget Paket Yöneticisi, çalışması [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="2ba3e-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="2ba3e-157">**Node.js** : [nasıl toouse node.js'den Notification Hubs](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2ba3e-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="2ba3e-158">**Mobile Apps**: bir örneği için Notification Hubs ile tümleştirilmiş Azure App Service Mobile Apps arka uç toosend bildirimleri bkz [Ekle anında iletme bildirimleri tooyour mobil uygulama](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="2ba3e-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="2ba3e-159">**Java / PHP**: REST API'lerini kullanarak toosend anında iletme bildirimleri nasıl hello ilişkin bir örnek için bkz: "nasıl toouse Java/php'den Notification Hubs" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="2ba3e-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="2ba3e-160">(İsteğe bağlı) .NET Konsol Uygulamasından Anında İletme Bildirimleri Gönderme</span><span class="sxs-lookup"><span data-stu-id="2ba3e-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="2ba3e-161">Bu bölümde, basit bir .NET konsol uygulaması kullanarak anında iletme bildirimleri göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="2ba3e-162">Bu örnek Hello amaçları doğrultusunda, biz Visual Studio'nun zaten yüklü olduğu tooa Windows geliştirme ortamına geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="2ba3e-163">Visual Studio'da yeni bir Visual C# konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="2ba3e-164">Visual Studio'da **Araçlar**'a, **NuGet Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="2ba3e-165">Merhaba Paket Yöneticisi konsolu, Visual Studio çalışma alanınızın yerleşik toohello alt görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="2ba3e-166">Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="2ba3e-167">Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="2ba3e-168">Açık hello `Program.cs` dosya ve hello aşağıdakileri ekleyin `using` deyimi, size Azure sınıflarını ve işlevlerini ana sınıfınız içindeki kullanabilirsiniz sağlama:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="2ba3e-169">İçinde `Program` sınıfı, yöntem aşağıdaki hello ekleyin (tooreplace hello unutmayın **bağlantı dizesi** ve **hub adı**):</span><span class="sxs-lookup"><span data-stu-id="2ba3e-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="2ba3e-170">Hello aşağıdaki satırları ekleyin, `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="2ba3e-171">Merhaba F5 anahtar toorun hello uygulama tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="2ba3e-172">Saniyeler içinde, cihazınızda bir anında iletme bildirimi görüntülendiğini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="2ba3e-173">Wi-Fi veya hücresel veri ağı kullanmanızdan bağımsız hello cihazda etkin bir Internet bağlantısı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="2ba3e-174">Merhaba Apple hello tüm olası yükleri bulabilirsiniz [yerel ve anında iletilen bildirim Programlama Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="2ba3e-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="2ba3e-175">(İsteğe bağlı) Mobil Hizmetten Bildirim Gönderme</span><span class="sxs-lookup"><span data-stu-id="2ba3e-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="2ba3e-176">Bu bölümde, bir node betiği aracılığıyla mobil hizmet kullanarak anında iletme bildirimleri göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="2ba3e-177">bir mobil hizmet kullanarak bildirim toosend izleyin [Mobile Services'i kullanmaya başlama]ve ardından:</span><span class="sxs-lookup"><span data-stu-id="2ba3e-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="2ba3e-178">İçinde toohello oturum [Klasik Azure portalı]ve mobil hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="2ba3e-179">Select hello **Zamanlayıcı** hello üst sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="2ba3e-180">Yeni bir zamanlanan iş oluşturun, ad ekleyin ve **İsteğe bağlı**'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="2ba3e-181">Merhaba iş oluşturulduğunda hello iş adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="2ba3e-182">Merhaba ardından **betik** hello üst çubuğu sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="2ba3e-183">Komut dosyası Zamanlayıcı işlevinizin içine aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="2ba3e-184">Bildirim hub'ı adı ve hello için bağlantı dizenizi emin tooreplace hello yer tutucularını olun *DefaultFullSharedAccessSignature* daha önce edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="2ba3e-185">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="2ba3e-186">Tıklatın **bir kez çalıştır** hello alt çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="2ba3e-187">Cihazınızda bir uyarı almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ba3e-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ba3e-188">Next steps</span></span>
<span data-ttu-id="2ba3e-189">Bu basit örnekte, iOS cihazlarınıza anında iletme bildirimleri tooall yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="2ba3e-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="2ba3e-190">Buna belirli kullanıcılara tootarget sipariş, toohello öğretici başvurun [Notification Hubs kullanma toopush bildirimleri toousers].</span><span class="sxs-lookup"><span data-stu-id="2ba3e-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="2ba3e-191">Toosegment kullanıcılarınızı ilgi alanı gruplarına göre isterseniz, okuyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend].</span><span class="sxs-lookup"><span data-stu-id="2ba3e-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="2ba3e-192">Hakkında daha fazla bilgi toouse bildirim hub'ları [Notification Hubs Kılavuzu] ve hello [bildirim hub'ları nasıl-toofor iOS].</span><span class="sxs-lookup"><span data-stu-id="2ba3e-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Mobile Services'i kullanmaya başlama]: /develop/mobile/tutorials/get-started-xamarin-ios
[Klasik Azure portalı]: https://manage.windowsazure.com/
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[bildirim hub'ları nasıl-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Notification Hubs kullanma toopush bildirimleri toousers]: /manage/services/notification-hubs/notify-users-aspnet
[son dakika haberleri Notification Hubs kullanma toosend]: /manage/services/notification-hubs/breaking-news-dotnet

[yerel ve anında iletilen bildirim Programlama Kılavuzu]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
