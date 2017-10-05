---
title: "Azure Notification Hubs ile iOS'a anında iletme bildirimleri gönderme | Microsoft Belgeleri"
description: "Bu öğreticide, bir iOS uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını öğrenirsiniz."
services: notification-hubs
documentationcenter: ios
keywords: "anında iletme bildirimi,anında iletme bildirimleri,ios anında iletme bildirimleri"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ab0777f859e80afcd61e371056b44d018c7b7ab9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-to-ios-with-azure-notification-hubs"></a><span data-ttu-id="1e7d2-104">Azure Notification Hubs ile iOS'a anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="1e7d2-104">Sending push notifications to iOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1e7d2-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1e7d2-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="1e7d2-106">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="1e7d2-107">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1e7d2-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="1e7d2-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="1e7d2-109">Bu öğretici, bir iOS uygulamasına anında iletme bildirimleri göndermek için Azure Notification Hubs'ın nasıl kullanılacağını size gösterir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span> <span data-ttu-id="1e7d2-110">[Apple Anında İletilen Bildirim servisini (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-110">You'll create a blank iOS app that receives push notifications by using the [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="1e7d2-111">İşiniz bittiğinde, uygulamanızı çalıştıran tüm cihazlara anında iletme bildirimleri yayımlamak için bildirim hub'ınızı kullanabileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1e7d2-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1e7d2-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="1e7d2-113">Bu öğreticinin tamamlanan kodu [GitHub'da](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted) bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-113">The completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1e7d2-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1e7d2-114">Prerequisites</span></span>
<span data-ttu-id="1e7d2-115">Bu öğretici için aşağıdakiler gereklidir:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="1e7d2-116">[Mobile Services iOS SDK'sı sürüm 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="1e7d2-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="1e7d2-117">[Xcode]'un en son sürümü</span><span class="sxs-lookup"><span data-stu-id="1e7d2-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="1e7d2-118">iOS 8 (veya sonraki bir sürümü) uyumlu bir cihaz</span><span class="sxs-lookup"><span data-stu-id="1e7d2-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="1e7d2-119">[Apple Developer Program](https://developer.apple.com/programs/) üyeliği.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="1e7d2-120">Anında iletme bildirimlerinin yapılandırma gereksinimleri nedeniyle, anında iletme bildirimlerini iOS Simülatörü'nün yerine fiziksel bir iOS cihazında (iPhone veya iPad) dağıtmanız ve test etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of the iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="1e7d2-121">Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="1e7d2-122">iOS anında iletme bildirimleri için Notification Hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1e7d2-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="1e7d2-123">Bu bölüm, yeni bir bildirim hub'ı oluşturma ve oluşturduğunuz **.p12** anında iletme sertifikasını kullanarak APNS ile kimlik doğrulaması yapılandırma konusunda size yol gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="1e7d2-124">Önceden oluşturduğunuz bir bildirim hub'ını kullanmak istiyorsanız 5. adıma geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="1e7d2-125"><b>Ayarlar</b> dikey penceresinde, <b>Bildirim Hizmetleri</b> düğmesine tıklayın, ardından <b>Apple'ı (APNS)</b> seçin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-125">Click the <b>Notification Services</b> button in the <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="1e7d2-126"><b>Sertifikayı Karşıya Yükle</b>'ye tıklayıp daha önce dışarı aktardığınız <b>.p12</b> dosyasını seçin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-126">Click on <b>Upload Certificate</b> and select the <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="1e7d2-127">Ayrıca, doğru parolayı belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-127">Make sure you also specify the correct password.</span></span></p>

<p><span data-ttu-id="1e7d2-128"><b>Korumalı Alan</b> modu geliştirme içindir, bu nedenle bu seçeneği belirlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-128">Make sure to select <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="1e7d2-129"><b>Üretim</b> seçeneğini yalnızca uygulamanızı mağazadan satın alan kullanıcılara anında iletme bildirimleri göndermek istiyorsanız kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-129">Only use the <b>Production</b> if you want to send push notifications to users who purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="1e7d2-130">&emsp;&emsp;&emsp;&emsp;![Azure portalında APNS yapılandırın](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="1e7d2-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Azure Portal'da APNS sertifikası yapılandırma](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="1e7d2-132">Bildirim hub'ınız şimdi APNS ile birlikte çalışmak üzere yapılandırıldı. Ayrıca uygulamanızı kaydetmenizi ve anlık iletme bildirimleri göndermenizi sağlayan bağlantı dizelerine sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-132">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-to-notification-hubs"></a><span data-ttu-id="1e7d2-133">iOS uygulamanızı Notification Hubs'a bağlama</span><span class="sxs-lookup"><span data-stu-id="1e7d2-133">Connect your iOS app to Notification Hubs</span></span>
1. <span data-ttu-id="1e7d2-134">Xcode'da yeni bir iOS projesi oluşturun ve **Single View Application** (Tek Görünüm Uygulaması) şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-134">In Xcode, create a new iOS project and select the **Single View Application** template.</span></span>
   
    ![Xcode - Single View Application (Tek Görünüm Uygulaması)][8]
    
2. <span data-ttu-id="1e7d2-136">Yeni projeniz için seçenekleri ayarlarken, daha önce Apple Developer portalında paket kimliğini açarken kullandığınız **Product Name** (Ürün Adı) ve **Organization Identifier**'nı (Kuruluş Tanımlayıcısı) kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-136">When setting the options for your new project, make sure to use the same **Product Name** and **Organization Identifier** that you used when you previously set the bundle ID on the Apple Developer portal.</span></span>
   
    ![Xcode - proje seçenekleri][11]
    
3. <span data-ttu-id="1e7d2-138">**Targets** (Hedefler) altında projenizin adına tıklayın, **Build Settings** (Derleme Ayarları) sekmesine tıklayın ve **Code Signing Identity**'yi (Kod İmzalama Kimliği) genişletin. Ardından **Debug** (Hata Ayıklama) altında kod imzalama kimliğinizi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-138">Under **Targets**, click your project name, click the **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="1e7d2-139">**Levels**'i (Düzeyler) **Basic**'ten (Temel) **All**'a (Tüm) geçirin ve **Provisioning Profile**'ı (Hazırlama Profili) daha önce oluşturduğunuz hazırlama profiline ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-139">Toggle **Levels** from **Basic** to **All**, and set **Provisioning Profile** to the provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="1e7d2-140">Xcode'da oluşturduğunuz yeni hazırlama profilini göremiyorsanız imzalama kimliğiniz için profilleri yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-140">If you don't see the new provisioning profile that you created in Xcode, try refreshing the profiles for your signing identity.</span></span> <span data-ttu-id="1e7d2-141">Menü çubuğunda **Xcode**'a tıklayın, **Preferences**'a (Tercihler) tıklayın, **Account** (Hesap) sekmesine tıklayın, **View Details** (Ayrıntıları Görüntüle) düğmesine tıklayın, imzalama kimliğinize tıklayın ve ardından sağ alt köşedeki yenile düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-141">Click **Xcode** on the menu bar, click **Preferences**, click the **Account** tab, click the **View Details** button, click your signing identity, and then click the refresh button in the bottom-right corner.</span></span>
   
    ![Xcode - hazırlama profili][9]
4. <span data-ttu-id="1e7d2-143">[Mobile Services iOS SDK'sı sürüm 1.2.4]'ü indirin ve dosyanın sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-143">Download the [Mobile Services iOS SDK version 1.2.4] and unzip the file.</span></span> <span data-ttu-id="1e7d2-144">Xcode'da projenize sağ tıklayın ve **WindowsAzureMessaging.framework** klasörünü Xcode projenize eklemek için **Add Files to** (Dosyaları Şuraya Ekle) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-144">In Xcode, right-click your project and click the **Add Files to** option to add the **WindowsAzureMessaging.framework** folder to your Xcode project.</span></span> <span data-ttu-id="1e7d2-145">**Copy items if needed** (Gerekirse öğeleri kopyala) seçeneğini belirleyin ve ardından **Add** (Ekle) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1e7d2-146">Bildirim hub'ları SDK'sı şu anda Xcode 7'de bitcode'u desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-146">The notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="1e7d2-147">**Build Options** (Derleme Seçenekleri) içinde, projeniz için **Enable Bitcode** (Bitcode'u Etkinleştir) seçeneğini **No** (Hayır) olarak ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-147">You must set **Enable Bitcode** to **No** in the **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Azure SDK'nın sıkıştırmasını açma][10]
5. <span data-ttu-id="1e7d2-149">Projenize `HubInfo.h` adlı yeni bir üst bilgi dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-149">Add a new header file to your project named `HubInfo.h`.</span></span> <span data-ttu-id="1e7d2-150">Bu dosya, bildirim hub'ınız için sabitleri tutar.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-150">This file will hold the constants for your notification hub.</span></span>  <span data-ttu-id="1e7d2-151">Aşağıdaki tanımları ekleyin ve dize sabiti yer tutucularını, daha önce not ettiğiniz *hub adınız* ve *DefaultListenSharedAccessSignature* ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-151">Add the following definitions and replace the string literal placeholders with your *hub name* and the *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter the name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="1e7d2-152">`AppDelegate.h` dosyanızı açıp aşağıdaki içeri aktarma yönergelerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-152">Open your `AppDelegate.h` file add the following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="1e7d2-153">`AppDelegate.m file` dosyanızda, iOS sürümünüze bağlı olarak `didFinishLaunchingWithOptions` yöntemine aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-153">In your `AppDelegate.m file`, add the following code in the `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="1e7d2-154">Bu kod, cihaz tanıtıcınızı APNs'ye kaydeder:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="1e7d2-155">iOS 8 için:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="1e7d2-156">8'den önceki iOS sürümleri için:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-156">For iOS versions prior to 8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="1e7d2-157">Aynı dosyada, aşağıdaki yöntemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-157">In the same file, add the following methods.</span></span> <span data-ttu-id="1e7d2-158">Bu kod, HubInfo.h içinde belirttiğiniz bağlantı bilgilerini kullanarak bildirim hub'ına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-158">This code connects to the notification hub using the connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="1e7d2-159">Ardından, cihaz belirtecini bildirim hub'ına verir. Böylece bildirim hub'ı bildirim gönderebilir:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-159">It then gives the device token to the notification hub so that the notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="1e7d2-160">Aynı dosyaya, uygulama etkinken bildirim alınırsa **UIAlert** görüntülenmesi için aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-160">In the same file, add the following method to display a **UIAlert** if the notification is received while the app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="1e7d2-161">Herhangi bir hata olmadığını doğrulamak için cihazınızda uygulamayı derleyin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-161">Build and run the app on your device to verify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="1e7d2-162">Test amaçlı anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="1e7d2-162">Send test push notifications</span></span>
<span data-ttu-id="1e7d2-163">Hub dikey penceresindeki **Sorun Giderme** bölümü aracılığıyla [Azure Portal]'da anında iletme bildirimleri göndererek uygulamanızda bildirim almayı test edebilirsiniz (*Test Gönderimi* seçeneğini kullanın).</span><span class="sxs-lookup"><span data-stu-id="1e7d2-163">You can test receiving notifications in your app by sending push notifications in the [Azure Portal] via the **Troubleshooting** section in the hub blade (use the *Test Send* option).</span></span>

![Azure Portal - Test Gönderimi][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-the-app"></a><span data-ttu-id="1e7d2-165">(İsteğe bağlı) Uygulamadan anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="1e7d2-165">(Optional) Send push notifications from the app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1e7d2-166">İstemci uygulamasından bildirim göndermeye yönelik bu örnek yalnızca öğrenme amacıyla verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-166">This example of sending notifications from the client app is provided for learning purposes only.</span></span> <span data-ttu-id="1e7d2-167">Bu işlem istemci uygulamada `DefaultFullSharedAccessSignature` gerektireceğinden, bildirim hub’ınızı bir kullanıcının istemcilerinize yetkisiz bildirimler göndermek üzere erişim kazanabilmesi riskine maruz bırakır.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-167">Since this will require the `DefaultFullSharedAccessSignature` to be present on the client app, it exposes your notification hub to the risk that a user may gain access to send unauthorized notifications to your clients.</span></span>
> 
> 

<span data-ttu-id="1e7d2-168">Bir uygulama içinden anında iletme bildirimleri göndermek isterseniz bu bölümde REST arabirimini kullanarak bunu nasıl yapacağınız konusunda bir örnek sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-168">If you want to send push notifications from within an app, this section provides an example of how to do this using the REST interface.</span></span>

1. <span data-ttu-id="1e7d2-169">Xcode'da `Main.storyboard` öğesini açın ve kullanıcının uygulama içinde anında iletme bildirimleri göndermesine izin vermek için nesne kitaplığından aşağıdaki kullanıcı arabirimi bileşenlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-169">In Xcode, open `Main.storyboard` and add the following UI components from the object library to allow the user to send push notifications in the app:</span></span>
   
   * <span data-ttu-id="1e7d2-170">Etiket metni olmayan bir etiket.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-170">A label with no label text.</span></span> <span data-ttu-id="1e7d2-171">Bildirim gönderme hatalarını raporlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-171">It will be used to report errors in sending notifications.</span></span> <span data-ttu-id="1e7d2-172">**Lines** özelliği **0** olarak ayarlanmalıdır. Böylece, otomatik olarak sağ ve sol kenar boşluklarına ve üst görünüme göre kısıtlandırılarak otomatik olarak boyutlandırılır.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-172">The **Lines** property should be set to **0** so that it will automatically size constrained to the right and left margins and the top of the view.</span></span>
   * <span data-ttu-id="1e7d2-173">**Placeholder** (Yer Tutucu) metninin **Enter Notification Message** (Bildirim İletisi Girin) olarak ayarlandığı bir metin alanı.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-173">A text field with **Placeholder** text set to **Enter Notification Message**.</span></span> <span data-ttu-id="1e7d2-174">Aşağıda gösterildiği gibi, bu alanı tam etiketin altında kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-174">Constrain the field just below the label as shown below.</span></span> <span data-ttu-id="1e7d2-175">Görünüm Denetleyicisi'ni çıkış temsilcisi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-175">Set the View Controller as the outlet delegate.</span></span>
   * <span data-ttu-id="1e7d2-176">Tam metin alanı altında ve yatay ortada kısıtlanmış **Send Notification** (Bildirim Gönder) adlı bir düğme.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-176">A button titled **Send Notification** constrained just below the text field and in the horizontal center.</span></span>
     
     <span data-ttu-id="1e7d2-177">Görünüm aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-177">The view should look as follows:</span></span>
     
     ![Xcode tasarımcısı][32]
2. <span data-ttu-id="1e7d2-179">Görünümünüze bağlı etiket ve metin alanı için [çıkışlar ekleyin](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html); `interface` tanımınızı, `UITextFieldDelegate` ve `NSXMLParserDelegate` yöntemlerini desteklemesi için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for the label and text field connected your view, and update your `interface` definition to support `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="1e7d2-180">REST API çağırmayı ve yanıt ayrıştırmayı desteklemeye yardımcı olmak için aşağıda gösterilen üç özellik bildirimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-180">Add the three property declarations shown below to help support calling the REST API and parsing the response.</span></span>
   
    <span data-ttu-id="1e7d2-181">ViewController.h dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="1e7d2-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected to your UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="1e7d2-182">`HubInfo.h` öğesini açın ve hub'ınıza bildirimler göndermek için kullanılacak olan aşağıdaki sabitleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-182">Open `HubInfo.h` and add the following constants which will be used for sending notifications to your hub.</span></span> <span data-ttu-id="1e7d2-183">Yer tutucu dize sabitini, gerçek *DefaultFullSharedAccessSignature* bağlantı dizeniz ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-183">Replace the placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="1e7d2-184">Aşağıdaki `#import` deyimlerini `ViewController.h` dosyanıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-184">Add the following `#import` statements to your `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="1e7d2-185">`ViewController.m` içinde, arabirim uygulamasına aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-185">In `ViewController.m` add the following code to the interface implementation.</span></span> <span data-ttu-id="1e7d2-186">Bu kod, *DefaultFullSharedAccessSignature* bağlantı dizenizi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="1e7d2-187">[REST API başvurusu](http://msdn.microsoft.com/library/azure/dn495627.aspx)'nda belirtildiği gibi, bu ayrıştırılmış bilgiler **Authorization** (Yetkilendirme) istek üst bilgisi için bir SaS belirteci oluşturmak üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-187">As mentioned in the [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used to generate a SaS token for the **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="1e7d2-188">`ViewController.m` içinde, görünüm yüklenirken bağlantı dizesini ayrıştırmak için `viewDidLoad` yöntemini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-188">In `ViewController.m`, update the `viewDidLoad` method to parse the connection string when the view loads.</span></span> <span data-ttu-id="1e7d2-189">Ayrıca, aşağıda gösterilen yardımcı program yöntemlerini arabirim uygulamasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-189">Also add the utility methods, shown below, to the interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="1e7d2-190">`ViewController.m` içinde, [REST API Başvurusu](http://msdn.microsoft.com/library/azure/dn495627.aspx)'nda belirtildiği gibi **Authorization** (Yetkilendirme) üst bilgisinde sağlanacak olan SaS yetkilendirme belirtecini oluşturmak için, aşağıdaki kodu arabirim uygulamasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-190">In `ViewController.m`, add the following code to the interface implementation to generate the SaS authorization token that will be provided in the **Authorization** header, as mentioned in the [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with the signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="1e7d2-191">**Touch Down** olayı için **SendNotificationMessage** adlı bir eylem eklemek amacıyla, **Send Notification** (Bildirim Gönder) düğmesinden `ViewController.m` öğesine Ctrl tuşunu basılı tutup sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-191">Ctrl+drag from the **Send Notification** button to `ViewController.m` to add an action named **SendNotificationMessage** for the **Touch Down** event.</span></span> <span data-ttu-id="1e7d2-192">REST API kullanarak bildirim göndermek için aşağıdaki kod ile yöntemi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-192">Update method with the following code to send the notification using the REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of the notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct the message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate the token to be used in the authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the APNs notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="1e7d2-193">`ViewController.m` içinde, metin alanı için klavye kapatmayı desteklemek üzere aşağıdaki temsilci yöntemini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-193">In `ViewController.m`, add the following delegate method to support closing the keyboard for the text field.</span></span> <span data-ttu-id="1e7d2-194">Görünüm denetleyicisini çıkış temsilcisi olarak ayarlamak için, metin alanından arabirim tasarımcısındaki Görünüm Denetleyicisi'ne Ctrl tuşunu basılı tutup sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-194">Ctrl+drag from the text field to the View Controller icon in the interface designer to set the view controller as the outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="1e7d2-195">`ViewController.m` içinde, `NSXMLParser` kullanarak yanıt ayrıştırmayı desteklemek için aşağıdaki temsilci yöntemlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-195">In `ViewController.m`, add the following delegate methods to support parsing the response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set the status label text on the UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="1e7d2-196">Projeyi derleyin ve hata olmadığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-196">Build the project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="1e7d2-197">Xcode7'de bitcode desteğine ilişkin bir derleme hatası ile karşılaşırsanız Xcode'da **Build Settings** (Derleme Ayarları) > **Enable Bitcode (ENABLE_BITCODE)** (Bitcode'u Etkinleştir) seçeneğini **NO** (HAYIR) olarak değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-197">If you encounter a build error in Xcode7 about bitcode support, you should change the **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** to **NO** in Xcode.</span></span> <span data-ttu-id="1e7d2-198">Notification Hubs SDK'sı şu anda bitcode'u desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-198">The Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="1e7d2-199">Apple [Local and Push Notification Programming Guide] (Yerel ve Anında İletilen Bildirim Programlama Kılavuzu) içinde tüm olası bildirim yüklerini bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-199">You can find all the possible notification payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="1e7d2-200">Uygulamanızın anında iletme bildirimleri alıp almadığını denetleme</span><span class="sxs-lookup"><span data-stu-id="1e7d2-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="1e7d2-201">iOS'ta anında iletme bildirimlerini test etmek için, uygulamayı fiziksel bir iOS cihazına dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-201">To test push notifications on iOS, you must deploy the app to a physical iOS device.</span></span> <span data-ttu-id="1e7d2-202">iOS Simülatörü'nü kullanarak Apple anında iletme bildirimleri gönderemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-202">You cannot send Apple push notifications by using the iOS Simulator.</span></span>

1. <span data-ttu-id="1e7d2-203">Uygulamayı çalıştırın ve kaydın başarılı olduğunu doğrulayın. Ardından, **Tamam**'a basın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-203">Run the app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![iOS Uygulaması Anında İletme Bildirimi Kayıt Testi][33]
2. <span data-ttu-id="1e7d2-205">Yukarıda açıklandığı gibi, [Azure Portal]'dan test amaçlı anında iletme bildirimi gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-205">You can send a test push notification from the [Azure Portal], as described above.</span></span> <span data-ttu-id="1e7d2-206">Uygulamada anında iletme bildirimleri göndermek için kod eklediyseniz bildirim iletisi girmek için metin alanı içine dokunun.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-206">If you added code for sending push notifications in the app, touch inside the text field to enter a notification message.</span></span> <span data-ttu-id="1e7d2-207">Ardından, bildirim iletisini göndermek için klavyede **Send** (Gönder) düğmesine veya görünümdeki **Send Notification** (Bildirim Gönder) düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-207">Then press the **Send** button on the keyboard or the **Send Notification** button in the view to send the notification message.</span></span>
   
    ![iOS Uygulaması Anında İletilen Bildirim Gönderme Testi][34]
3. <span data-ttu-id="1e7d2-209">Belirli Bildirim Hub'ından bildirimleri almak için kaydedilen tüm cihazlara anında iletme bildirimi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-209">The push notification is sent to all devices that are registered to receive the notifications from the particular Notification Hub.</span></span>
   
    ![iOS Uygulaması Anında İletilen Bildirim Alma Testi][35]

## <a name="next-steps"></a><span data-ttu-id="1e7d2-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e7d2-211">Next steps</span></span>
<span data-ttu-id="1e7d2-212">Bu basit örnekte, tüm kayıtlı iOS cihazlarınıza anında iletme bildirimleri yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-212">In this simple example, you broadcasted push notifications to all your registered iOS devices.</span></span> <span data-ttu-id="1e7d2-213">Öğrenmenizde bir sonraki adım olarak, etiketleri kullanarak anında iletme bildirimleri göndermek için arka uç oluşturmada size yol gösterecek [Azure Notification Hubs .NET arka ucu ile iOS için Kullanıcılara Bildirme] öğreticisine devam etmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-213">We suggest as a next step in your learning that you proceed to the [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend to send push notifications using tags.</span></span> 

<span data-ttu-id="1e7d2-214">Kullanıcılarınızı ilgi alanı gruplarına göre segmentlere ayırmak istiyorsanız buna ek olarak, [Son dakika haberleri göndermek için Notification Hubs kullanma] öğreticisine gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e7d2-214">If you want to segment your users by interest groups, you can additionally move on to the [Use Notification Hubs to send breaking news] tutorial.</span></span> 

<span data-ttu-id="1e7d2-215">Notification Hubs hakkında genel bilgi için bkz. [Notification Hubs Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="1e7d2-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
<span data-ttu-id="1e7d2-216">[Mobile Services iOS SDK'sı sürüm 1.2.4]: http://aka.ms/kymw2g</span><span class="sxs-lookup"><span data-stu-id="1e7d2-216">[Mobile Services iOS SDK version 1.2.4]: http://aka.ms/kymw2g</span></span>
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
<span data-ttu-id="1e7d2-217">[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="1e7d2-217">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="1e7d2-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span><span class="sxs-lookup"><span data-stu-id="1e7d2-218">[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532</span></span>
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
<span data-ttu-id="1e7d2-219">[Azure Notification Hubs .NET arka ucu ile iOS için Kullanıcılara Bildirme]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span><span class="sxs-lookup"><span data-stu-id="1e7d2-219">[Azure Notification Hubs Notify Users for iOS with .NET backend]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md</span></span>
<span data-ttu-id="1e7d2-220">[Son dakika haberleri göndermek için Notification Hubs kullanma]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="1e7d2-220">[Use Notification Hubs to send breaking news]: notification-hubs-ios-xplat-segmented-apns-push-notification.md</span></span>

<span data-ttu-id="1e7d2-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span><span class="sxs-lookup"><span data-stu-id="1e7d2-221">[Local and Push Notification Programming Guide]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1</span></span>
<span data-ttu-id="1e7d2-222">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="1e7d2-222">[Azure Portal]: https://portal.azure.com</span></span>
