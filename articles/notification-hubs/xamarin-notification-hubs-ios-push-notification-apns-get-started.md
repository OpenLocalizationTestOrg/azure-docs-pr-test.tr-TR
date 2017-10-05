---
title: "Xamarin uygulamaları için Notification Hubs ile iOS Anında İletme Bildirimleri | Microsoft Belgeleri"
description: "Bu öğreticide, bir Xamarin iOS uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını öğrenirsiniz."
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
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="3f597-104">Xamarin uygulamaları için Notification Hubs ile iOS Anında İletme Bildirimleri</span><span class="sxs-lookup"><span data-stu-id="3f597-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="3f597-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3f597-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f597-106">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f597-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3f597-107">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3f597-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="3f597-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="3f597-109">Bu öğretici, bir iOS uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını size gösterir.</span><span class="sxs-lookup"><span data-stu-id="3f597-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="3f597-110">[Apple Anında İletilen Bildirim Servisi'ni (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) kullanarak anında iletme bildirimleri alan boş bir Xamarin.iOS uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3f597-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="3f597-111">İşiniz bittiğinde, uygulamanızı çalıştıran tüm cihazlara anında iletme bildirimleri yayımlamak için bildirim hub'ınızı kullanabileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="3f597-112">Tamamlanan kodu [NotificationHubs uygulaması][GitHub] örneğinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="3f597-113">Bu öğretici Notification Hubs ile basit anında iletme iletisi yayımlama senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3f597-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f597-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3f597-114">Prerequisites</span></span>
<span data-ttu-id="3f597-115">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="3f597-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="3f597-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="3f597-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="3f597-117">iOS 7.0 (veya sonraki bir sürümü) uyumlu bir cihaz</span><span class="sxs-lookup"><span data-stu-id="3f597-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="3f597-118">iOS Developer Program üyeliği</span><span class="sxs-lookup"><span data-stu-id="3f597-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="3f597-119">[Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="3f597-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3f597-120">iOS anında iletme bildirimlerinin yapılandırma gereksinimleri nedeniyle, örnek uygulamayı benzetici yerine fiziksel bir iOS cihazında (iPhone veya iPad) dağıtmanız ve test etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f597-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="3f597-121">Bu öğreticiyi tamamlamak Xamarin iOS uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="3f597-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="3f597-122">Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f597-122">Configure your notification hub</span></span>
<span data-ttu-id="3f597-123">Bu bölüm, yeni bir bildirim hub'ı oluşturma ve oluşturduğunuz **.p12** anında iletme sertifikasını kullanarak APNS ile kimlik doğrulaması yapılandırma konusunda size yol gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="3f597-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="3f597-124">Önceden oluşturduğunuz bir bildirim hub'ını kullanmak istiyorsanız 5. adıma geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="3f597-125">APNS bağlantısını yapılandırmak istediğimizden, Azure Portal'da Notification Hub ayarlarınızı açın ve <b>Bildirim Hizmetleri</b>'ne tıklayın. Ardından listede <b>Apple (APNS)</b> öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f597-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="3f597-126">Bunu yaptıktan sonra, <b>Sertifikayı Karşıya Yükle</b>'ye tıklayın. Ardından, daha önce dışarı aktardığınız <b>.p12</b> sertifikasını ve sertifika parolasını seçin.</span><span class="sxs-lookup"><span data-stu-id="3f597-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="3f597-127">Bir geliştirme ortamında anında iletme iletileri göndereceğinizden, <b>Korumalı Alan</b> modunu seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f597-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="3f597-128"><b>Üretim</b> ayarını yalnızca uygulamanızı zaten mağazadan satın almış kullanıcılara anında iletme bildirimleri göndermek istiyorsanız kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f597-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="3f597-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="3f597-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="3f597-130">Bildirim hub'ınız şimdi APNS ile birlikte çalışmak üzere yapılandırıldı. Ayrıca uygulamanızı kaydetmenizi ve anlık iletme bildirimleri göndermenizi sağlayan bağlantı dizelerine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="3f597-131">Uygulamanızı bildirim hub'ına bağlama</span><span class="sxs-lookup"><span data-stu-id="3f597-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="3f597-132">Yeni bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f597-132">Create a new project</span></span>
1. <span data-ttu-id="3f597-133">Xamarin Studio'da yeni bir iOS projesi oluşturun ve **Unified API** (Birleşik API)  > **Single View Application** (Tek Görünüm Uygulaması) şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="3f597-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio - Uygulama Türünü Seçme][31]
2. <span data-ttu-id="3f597-135">Azure Mesajlaşma bileşenine bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3f597-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="3f597-136">Çözüm görünümünde projenizin **Components** (Bileşenler) klasörüne sağ tıklayın ve **Get More Components** (Daha Fazla Bileşen Al) seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3f597-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="3f597-137">**Azure Mesajlaşma** bileşeni için arama yapın ve bileşeni projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3f597-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="3f597-138">**AppDelegate.cs**'ye aşağıdaki using deyimini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3f597-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="3f597-139">Bir **SBNotificationHub** örneği bildirin:</span><span class="sxs-lookup"><span data-stu-id="3f597-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="3f597-140">Aşağıdaki değişkenlerle bir **Constants.cs** sınıfı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3f597-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="3f597-141">**AppDelegate.cs**'de, **FinishedLaunching()**'i aşağıdaki ile eşleşecek şekilde güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="3f597-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
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
7. <span data-ttu-id="3f597-142">**AppleDelegate.cs**'de **RegisteredForRemoteNotifications()** yöntemini geçersiz kılın:</span><span class="sxs-lookup"><span data-stu-id="3f597-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
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
8. <span data-ttu-id="3f597-143">**AppleDelegate.cs**'de **ReceivedRemoteNotification()** yöntemini geçersiz kılın:</span><span class="sxs-lookup"><span data-stu-id="3f597-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="3f597-144">**AppleDelegate.cs**'de aşağıdaki **ProcessNotification()** yöntemini oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3f597-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
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
   > <span data-ttu-id="3f597-145">Ağ bağlantısının olmaması gibi durumlarla başa çıkmak için **FailedToRegisterForRemoteNotifications()**'ı geçersiz kılmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="3f597-146">Bu seçim, kullanıcı uygulamanızı çevrimdışı modda (örneğin, Uçak) başlattığında ve uygulamanıza özgü anında iletme mesajlaşması senaryoları kullanmak istediğinizde özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3f597-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="3f597-147">Cihazınızda uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f597-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="3f597-148">Anında İletme Bildirimleri Gönderme</span><span class="sxs-lookup"><span data-stu-id="3f597-148">Sending Push Notifications</span></span>
<span data-ttu-id="3f597-149">Aşağıdaki ekranda gösterildiği gibi, bildirim hub'ı sayfasında yer alan **Sorun Giderme** araç takımındaki **Test Gönderimi** özelliği ile [Azure Portal]'da bildirim göndererek, uygulamanızda anında iletme bildirimleri almayı test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="3f597-150">Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmeti aracılığıyla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f597-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="3f597-151">Senaryonuzda kullanılabilir bir kitaplık yoksa anında iletme iletileri göndermek için doğrudan REST API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="3f597-152">Bu öğreticide konuyu basit bir şekilde işleyeceğiz ve yalnızca bir arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için .NET SDK ile bildirim göndererek istemci uygulamanızı test etmeyi göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="3f597-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="3f597-153">Bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak [Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) öğreticisini öneririz.</span><span class="sxs-lookup"><span data-stu-id="3f597-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="3f597-154">Bununla birlikte, bildirim göndermek için aşağıdaki yaklaşımlar kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3f597-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="3f597-155">**REST Arabirimi**: [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx) kullanarak herhangi bir arka uç platformunda anında iletme bildirimini destekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="3f597-156">**Microsoft Azure Notification Hubs .NET SDK'sı**: Visual Studio için Nuget Paket Yöneticisi'nde [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3f597-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="3f597-157">**Node.js**: [Node.js'den Notification Hubs'ı kullanma](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3f597-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="3f597-158">**Mobile Apps**: Notification Hubs ile tümleştirilmiş Azure Uygulama Hizmeti Mobile Apps arka ucundan nasıl bildirim gönderildiğinin bir örneği için bkz. [Mobil uygulamalarınıza anında iletme bildirimleri ekleme](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="3f597-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="3f597-159">**Java/PHP**: REST API'ler kullanarak nasıl anında iletme bildirimleri gönderildiğinin bir örneği için bkz. "Java/PHP'den Notification Hubs'ı kullanma" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="3f597-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="3f597-160">(İsteğe bağlı) .NET Konsol Uygulamasından Anında İletme Bildirimleri Gönderme</span><span class="sxs-lookup"><span data-stu-id="3f597-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="3f597-161">Bu bölümde, basit bir .NET konsol uygulaması kullanarak anında iletme bildirimleri göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="3f597-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="3f597-162">Bu örneğin amaçları doğrultusunda, Visual Studio'nun zaten yüklü olduğu bir Windows geliştirme ortamına geçiş yapacağız.</span><span class="sxs-lookup"><span data-stu-id="3f597-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="3f597-163">Visual Studio'da yeni bir Visual C# konsol uygulaması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3f597-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="3f597-164">Visual Studio'da **Araçlar**'a, **NuGet Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f597-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="3f597-165">Paket yöneticisi konsolu, Visual Studio çalışma alanınızın altına yerleştirilmiş olarak görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="3f597-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="3f597-166">Paket Yöneticisi Konsolu penceresinde, **Varsayılan projeyi** yeni konsol uygulaması projeniz olarak ayarlayın ve ardından konsol penceresinde aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="3f597-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="3f597-167">Bu, <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a> kullanarak Azure Notification Hubs SDK'sına bir başvuru ekler.</span><span class="sxs-lookup"><span data-stu-id="3f597-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="3f597-168">`Program.cs` dosyasını açın ve ana sınıfınız içindeki Azure sınıflarını ve işlevlerini kullanabilmemizi sağlayan aşağıdaki `using` deyimini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3f597-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="3f597-169">`Program` sınıfınıza aşağıdaki yöntemi ekleyin (**bağlantı dizesini** ve **hub adını** değiştirmeyi unutmayın):</span><span class="sxs-lookup"><span data-stu-id="3f597-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="3f597-170">Aşağıdaki satırları `Main` yönteminize ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3f597-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="3f597-171">Uygulamayı çalıştırmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="3f597-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="3f597-172">Saniyeler içinde, cihazınızda bir anında iletme bildirimi görüntülendiğini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f597-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="3f597-173">Wi-Fi veya hücresel veri ağı kullanmanızdan bağımsız olarak, cihazda etkin bir İnternet bağlantınızın olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f597-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="3f597-174">Apple [Local and Push Notification Programming Guide] (Yerel ve Anında İletilen Bildirim Programlama Kılavuzu) içinde tüm olası yükleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="3f597-175">(İsteğe bağlı) Mobil Hizmetten Bildirim Gönderme</span><span class="sxs-lookup"><span data-stu-id="3f597-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="3f597-176">Bu bölümde, bir node betiği aracılığıyla mobil hizmet kullanarak anında iletme bildirimleri göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="3f597-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="3f597-177">Mobil hizmet kullanarak bildirim göndermek için [Mobile Services'i kullanmaya başlama]'yı izleyin ve ardından:</span><span class="sxs-lookup"><span data-stu-id="3f597-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="3f597-178">[Klasik Azure Portalı]'nda oturum açın ve mobil hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="3f597-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="3f597-179">Üst kısımdaki **Scheduler** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="3f597-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="3f597-180">Yeni bir zamanlanan iş oluşturun, ad ekleyin ve **İsteğe bağlı**'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="3f597-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="3f597-181">İş oluşturulduğunda iş adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f597-181">When the job is created, click the job name.</span></span> <span data-ttu-id="3f597-182">Ardından, üst çubukta **Betik** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f597-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="3f597-183">Zamanlayıcı işlevinizin içine aşağıdaki betiği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3f597-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="3f597-184">Yer tutucularını daha önce edindiğiniz bildirim hub'ı adınız ve *DefaultFullSharedAccessSignature* bağlantı dizeniz ile değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3f597-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="3f597-185">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f597-185">Click **Save**.</span></span>
   
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
6. <span data-ttu-id="3f597-186">Alt çubukta **Bir Kez Çalıştır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3f597-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="3f597-187">Cihazınızda bir uyarı almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f597-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f597-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3f597-188">Next steps</span></span>
<span data-ttu-id="3f597-189">Bu basit örnekte, tüm iOS cihazlarınıza anında iletme bildirimleri yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="3f597-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="3f597-190">Belirli kullanıcıları hedeflemek için, [Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma] öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="3f597-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="3f597-191">Kullanıcılarınızı ilgi alanı gruplarına göre segmentlere ayırmak istiyorsanız [Son dakika haberleri göndermek için Notification Hubs kullanma]'yı okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f597-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="3f597-192">[Notification Hubs Kılavuzu] ve [iOS için Notification Hubs'ı Kullanma]'da Notification Hubs'ı kullanma hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3f597-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

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

<span data-ttu-id="3f597-193">[Mobile Services'i kullanmaya başlama]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="3f597-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="3f597-194">[Klasik Azure Portalı]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="3f597-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="3f597-195">[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="3f597-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="3f597-196">[iOS için Notification Hubs'ı Kullanma]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="3f597-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="3f597-197">[Kullanıcılara anında iletme bildirimleri göndermek için Notification Hubs’ı kullanma]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="3f597-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="3f597-198">[Son dakika haberleri göndermek için Notification Hubs kullanma]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="3f597-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="3f597-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="3f597-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="3f597-200">[Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="3f597-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="3f597-201">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="3f597-201">[Azure Portal]: https://portal.azure.com</span></span>
