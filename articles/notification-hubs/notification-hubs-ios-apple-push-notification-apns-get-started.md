---
title: "Azure Notification Hubs ile anında iletme bildirimleri tooiOS aaaSending | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan iOS uygulaması öğrenin."
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
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="076e6-104">Azure Notification Hubs ile anında iletme bildirimleri tooiOS gönderme</span><span class="sxs-lookup"><span data-stu-id="076e6-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="076e6-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="076e6-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="076e6-106">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="076e6-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="076e6-107">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="076e6-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="076e6-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="076e6-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="076e6-109">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan iOS uygulaması gösterir.</span><span class="sxs-lookup"><span data-stu-id="076e6-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="076e6-110">Hello kullanarak anında iletme bildirimleri alan boş bir iOS uygulaması oluşturacaksınız [Apple anında iletilen bildirim servisi (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span><span class="sxs-lookup"><span data-stu-id="076e6-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="076e6-111">Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.</span><span class="sxs-lookup"><span data-stu-id="076e6-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="076e6-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="076e6-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="076e6-113">Bu öğreticinin tamamlanan hello kodu bulunabilir [github'da](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span><span class="sxs-lookup"><span data-stu-id="076e6-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="076e6-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="076e6-114">Prerequisites</span></span>
<span data-ttu-id="076e6-115">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="076e6-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="076e6-116">[Mobile Services iOS SDK'sı sürüm 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="076e6-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="076e6-117">[Xcode]'un en son sürümü</span><span class="sxs-lookup"><span data-stu-id="076e6-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="076e6-118">iOS 8 (veya sonraki bir sürümü) uyumlu bir cihaz</span><span class="sxs-lookup"><span data-stu-id="076e6-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="076e6-119">[Apple Developer Program](https://developer.apple.com/programs/) üyeliği.</span><span class="sxs-lookup"><span data-stu-id="076e6-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="076e6-120">Anında iletme bildirimlerinin yapılandırma gereksinimleri nedeniyle, dağıtmak ve hello iOS simülatörü yerine bir fiziksel iOS cihazında (iPhone veya iPad) anında iletme bildirimleri test.</span><span class="sxs-lookup"><span data-stu-id="076e6-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="076e6-121">Bu öğreticiyi tamamlamak iOS uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="076e6-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="076e6-122">iOS anında iletme bildirimleri için Notification Hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="076e6-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="076e6-123">Bu bölümde, yeni bir bildirim hub'ı oluşturma ve hello kullanarak APNS ile kimlik doğrulaması yapılandırma açıklanmaktadır **.p12** oluşturduğunuz bildirim sertifikası.</span><span class="sxs-lookup"><span data-stu-id="076e6-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="076e6-124">Önceden oluşturduğunuz bir bildirim hub'ı toouse istiyorsanız, toostep 5 atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="076e6-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="076e6-125">Merhaba tıklatın <b>Bildirim Hizmetleri</b> hello düğmesini <b>ayarları</b> dikey penceresinde, ardından <b>Apple (APNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="076e6-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="076e6-126">Tıklayın <b>sertifikasını karşıya yükle</b> ve select hello <b>.p12</b> daha önce dışarı aktarılan dosya.</span><span class="sxs-lookup"><span data-stu-id="076e6-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="076e6-127">Ayrıca hello doğru parolayı belirttiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="076e6-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="076e6-128">Emin tooselect olun <b>korumalı alan</b> bu geliştirme için olduğundan modu.</span><span class="sxs-lookup"><span data-stu-id="076e6-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="076e6-129">Yalnızca hello kullan <b>üretim</b> uygulamanızı hello mağazadan satın alan toosend anında iletme bildirimleri toousers istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="076e6-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="076e6-130">&emsp;&emsp;&emsp;&emsp;![Azure portalında APNS yapılandırın](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="076e6-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Azure Portal'da APNS sertifikası yapılandırma](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="076e6-132">Bildirim hub'ınız şimdi APNS ile yapılandırılmış toowork olan ve hello bağlantı dizeleri tooregister uygulamanızı çalıştırdıktan ve anında iletme bildirimleri göndermek.</span><span class="sxs-lookup"><span data-stu-id="076e6-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="076e6-133">İOS uygulama tooNotification hub Bağlan</span><span class="sxs-lookup"><span data-stu-id="076e6-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="076e6-134">Xcode'da yeni bir iOS projesi oluşturun ve seçin hello **tek görünüm uygulaması** şablonu.</span><span class="sxs-lookup"><span data-stu-id="076e6-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode - Single View Application (Tek Görünüm Uygulaması)][8]
    
2. <span data-ttu-id="076e6-136">Yeni projeniz için başlangıç seçeneklerini ayarlarken toouse aynı hello emin olun **ürün adı** ve **kuruluş tanımlayıcı** hello paket kimliği daha önce Apple Developer hello üzerinde ayarlarken kullandığınız Portal.</span><span class="sxs-lookup"><span data-stu-id="076e6-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode - proje seçenekleri][11]
    
3. <span data-ttu-id="076e6-138">Altında **hedefleri**, projenizin adına tıklayın, hello tıklatın **Build Settings** sekmesinde ve genişletin **kod imzalama kimliği**ve ardından **hataayıklama**, kod imzalama kimliğinizi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="076e6-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="076e6-139">İki durumlu **düzeyleri** gelen **temel** çok**tüm**ve **sağlama profili** toohello daha önce oluşturduğunuz profili sağlama .</span><span class="sxs-lookup"><span data-stu-id="076e6-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="076e6-140">Yeni sağlama Xcode'da oluşturduğunuz profili hello göremiyorsanız imzalama kimliğiniz için hello profilleri yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="076e6-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="076e6-141">' I tıklatın **Xcode** hello menü çubuğunda **Tercihler**, hello tıklatın **hesap** sekmesini ve ardından hello **ayrıntıları görüntüle** düğmesini tıklatın, kimlik imzalama ve hello hello sağ alt köşedeki Yenile düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="076e6-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode - hazırlama profili][9]
4. <span data-ttu-id="076e6-143">Merhaba karşıdan [Mobile Services iOS SDK'sı sürüm 1.2.4] ve hello dosyanın sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="076e6-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="076e6-144">Xcode'da projenize sağ tıklayın ve hello **için dosyaları Ekle** seçeneği tooadd hello **WindowsAzureMessaging.framework** klasörü tooyour Xcode projesi.</span><span class="sxs-lookup"><span data-stu-id="076e6-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="076e6-145">**Copy items if needed** (Gerekirse öğeleri kopyala) seçeneğini belirleyin ve ardından **Add** (Ekle) seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="076e6-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="076e6-146">Merhaba bildirim hub'ları SDK Xcode 7'de bitcode'u şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="076e6-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="076e6-147">Ayarlamalısınız **Bitcode'u etkinleştir** çok**Hayır** hello içinde **derleme seçenekleri** projeniz için.</span><span class="sxs-lookup"><span data-stu-id="076e6-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Azure SDK'nın sıkıştırmasını açma][10]
5. <span data-ttu-id="076e6-149">Adlı yeni bir üstbilgi dosyası tooyour proje eklemek `HubInfo.h`.</span><span class="sxs-lookup"><span data-stu-id="076e6-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="076e6-150">Bu dosya, bildirim hub'ınız için hello sabitleri tutar.</span><span class="sxs-lookup"><span data-stu-id="076e6-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="076e6-151">Tanımları aşağıdaki hello ekleyin ve hello ile dize sabiti yer tutucularını değiştirin, *hub adı* ve hello *DefaultListenSharedAccessSignature* daha önce not ettiğiniz.</span><span class="sxs-lookup"><span data-stu-id="076e6-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="076e6-152">Açık, `AppDelegate.h` dosyasını içeri aktarma yönergeleri izleyerek hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="076e6-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="076e6-153">İçinde `AppDelegate.m file`, hello kodda aşağıdaki hello eklemek `didFinishLaunchingWithOptions` yöntemi iOS sürümünüze bağlı.</span><span class="sxs-lookup"><span data-stu-id="076e6-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="076e6-154">Bu kod, cihaz tanıtıcınızı APNs'ye kaydeder:</span><span class="sxs-lookup"><span data-stu-id="076e6-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="076e6-155">iOS 8 için:</span><span class="sxs-lookup"><span data-stu-id="076e6-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="076e6-156">İOS sürümleri önceki too8 için:</span><span class="sxs-lookup"><span data-stu-id="076e6-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="076e6-157">Aynı dosya Merhaba, yöntemler aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="076e6-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="076e6-158">Bu kod, Hubınfo.h içinde belirttiğiniz hello bağlantı bilgilerini kullanarak toohello bildirim hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="076e6-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="076e6-159">Merhaba bildirim hub'ı bildirimleri gönderebilmesi hello cihaz belirteci toohello bildirim hub'ı sonra sağlar:</span><span class="sxs-lookup"><span data-stu-id="076e6-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
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
9. <span data-ttu-id="076e6-160">Buna Merhaba aynı dosya, yöntem toodisplay aşağıdaki hello eklemek bir **Uıalert** hello uygulama etkin durumdayken hello bildirim alınırsa:</span><span class="sxs-lookup"><span data-stu-id="076e6-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="076e6-161">Derleme ve hello uygulama hiçbir hatalar varsa, cihaz tooverify üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="076e6-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="076e6-162">Test amaçlı anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="076e6-162">Send test push notifications</span></span>
<span data-ttu-id="076e6-163">Hello anında iletme bildirimleri göndererek uygulamanızda bildirim almayı test edebilirsiniz [Azure Portal] hello aracılığıyla **sorun giderme** hello hub dikey bölümde (Merhaba kullanmak *Test gönderimi* seçeneği).</span><span class="sxs-lookup"><span data-stu-id="076e6-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Azure Portal - Test Gönderimi][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="076e6-165">(İsteğe bağlı) Merhaba uygulamadan anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="076e6-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="076e6-166">Bu örneği hello istemci uygulamasından bildirim gönderme sadece öğrenme amaçları için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="076e6-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="076e6-167">Bu hello gerektirir beri `DefaultFullSharedAccessSignature` toobe hello istemci uygulaması varsa, bir kullanıcının erişim yetkisiz toosend bildirimlerine tooyour istemcileri kazanabilir bildirim hub'ı toohello riskini gösterir.</span><span class="sxs-lookup"><span data-stu-id="076e6-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="076e6-168">Bir uygulama içinde toosend anında iletme bildirimleri istiyorsanız, bu bölümde nasıl bir örnek sağlar toodo hello REST arabirimini kullanarak bu.</span><span class="sxs-lookup"><span data-stu-id="076e6-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="076e6-169">Xcode'da, açık `Main.storyboard` ve hello Nesne Kitaplığı tooallow hello kullanıcı toosend anında iletme bildirimleri hello uygulama kullanıcı Arabirimi bileşenlerini yükseltmesinin hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="076e6-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="076e6-170">Etiket metni olmayan bir etiket.</span><span class="sxs-lookup"><span data-stu-id="076e6-170">A label with no label text.</span></span> <span data-ttu-id="076e6-171">Bildirimleri gönderirken kullanılan tooreport hataları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="076e6-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="076e6-172">Merhaba **satırları** özelliği çok ayarlanmalıdır**0** böylece kısıtlanmış toohello sağ ve sol kenar boşluklarına ve hello üst hello görünümün otomatik olarak boyutlandırılır.</span><span class="sxs-lookup"><span data-stu-id="076e6-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="076e6-173">Bir metin alanı **yer tutucu** metin ayarlamak çok**bildirim iletisi girin**.</span><span class="sxs-lookup"><span data-stu-id="076e6-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="076e6-174">Aşağıda gösterildiği gibi yalnızca hello etiket altındaki Hello alanı kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="076e6-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="076e6-175">Merhaba View Controller hello çıkış temsilcisi olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="076e6-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="076e6-176">Adlı bir düğme **bildirim gönder** hemen hello metin alanı altında ve hello yatay ortada kısıtlanmış.</span><span class="sxs-lookup"><span data-stu-id="076e6-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="076e6-177">Merhaba görünüm aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="076e6-177">hello view should look as follows:</span></span>
     
     ![Xcode tasarımcısı][32]
2. <span data-ttu-id="076e6-179">[Çıkışlar ekleyin](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) hello etiket ve metin alanı görünümünüze bağlı için ve güncelleştirme, `interface` tanımı toosupport `UITextFieldDelegate` ve `NSXMLParserDelegate`.</span><span class="sxs-lookup"><span data-stu-id="076e6-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="076e6-180">Merhaba Hello REST API çağırma ve hello yanıt ayrıştırmayı toohelp desteği gösterilen üç özellik bildirimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="076e6-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="076e6-181">ViewController.h dosyanız aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="076e6-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="076e6-182">Açık `HubInfo.h` ve bildirimleri tooyour hub göndermek için kullanılacak olan sabitleri aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="076e6-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="076e6-183">Merhaba yer tutucu dize sabitini, gerçek Değiştir *DefaultFullSharedAccessSignature* bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="076e6-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="076e6-184">Merhaba aşağıdakileri ekleyin `#import` deyimleri tooyour `ViewController.h` dosya.</span><span class="sxs-lookup"><span data-stu-id="076e6-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="076e6-185">İçinde `ViewController.m` kod toohello arabirim uygulamasına aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="076e6-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="076e6-186">Bu kod, *DefaultFullSharedAccessSignature* bağlantı dizenizi ayrıştırır.</span><span class="sxs-lookup"><span data-stu-id="076e6-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="076e6-187">Hello belirtildiği gibi [REST API Başvurusu](http://msdn.microsoft.com/library/azure/dn495627.aspx), bu ayrıştırılmış bilgiler kullanılan toogenerate hello için bir SaS belirteci olacaktır **yetkilendirme** istek üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="076e6-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
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
6. <span data-ttu-id="076e6-188">İçinde `ViewController.m`, güncelleştirme hello `viewDidLoad` hello görünüm yüklenirken yöntemi tooparse hello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="076e6-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="076e6-189">Ayrıca, aşağıda gösterilen hello yardımcı program yöntemlerini ekleyin toohello arabirim uygulaması.</span><span class="sxs-lookup"><span data-stu-id="076e6-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

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





1. <span data-ttu-id="076e6-190">İçinde `ViewController.m`, hello sağlanan kod toohello arabirimi uygulama toogenerate hello SaS yetkilendirme belirtecini aşağıdaki hello eklemek **yetkilendirme** hello belirtildiği gibi üst [REST API'si Başvuru](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="076e6-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
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
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
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
2. <span data-ttu-id="076e6-191">CTRL + Sürükle gelen hello **bildirim gönder** çok düğmesini`ViewController.m` tooadd adlı bir eylem **SendNotificationMessage** hello için **Touch Down** olay.</span><span class="sxs-lookup"><span data-stu-id="076e6-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="076e6-192">Kod toosend hello bildirim hello REST API kullanarak aşağıdaki hello ile yöntemi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="076e6-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
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
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
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
3. <span data-ttu-id="076e6-193">İçinde `ViewController.m`, aşağıdaki temsilci yöntemini toosupport hello metin alanı için hello klavye kapatmayı hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="076e6-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="076e6-194">CTRL + Sürükle simgesinden hello metin alanı toohello View Controller hello arabirimi Tasarımcı tooset hello denetleyicisi hello çıkış temsilcisi olarak görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="076e6-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="076e6-195">İçinde `ViewController.m`, hello aşağıdaki temsilci yöntemlerini toosupport ayrıştırma hello yanıt kullanarak eklemek `NSXMLParser`.</span><span class="sxs-lookup"><span data-stu-id="076e6-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
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
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="076e6-196">Merhaba projeyi oluşturun ve hiçbir hata doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="076e6-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="076e6-197">Xcode7 bitcode'u desteği hakkında bir derleme hatası karşılaşırsanız hello değiştirmelisiniz **Build Settings** > **etkinleştirmek Bitcode (enable_bıtcode)** çok**Hayır** Xcode'da.</span><span class="sxs-lookup"><span data-stu-id="076e6-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="076e6-198">Merhaba Notification Hubs SDK'sı şu anda bitcode'u desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="076e6-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="076e6-199">Merhaba Apple tüm hello olası bildirim yüklerini bulabilirsiniz [yerel ve anında iletilen bildirim Programlama Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="076e6-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="076e6-200">Uygulamanızın anında iletme bildirimleri alıp almadığını denetleme</span><span class="sxs-lookup"><span data-stu-id="076e6-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="076e6-201">tootest anında iletme bildirimlerini iOS hello uygulama tooa fiziksel iOS cihazına dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="076e6-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="076e6-202">Merhaba iOS simülatörü'nü kullanarak Apple anında iletme bildirimleri gönderemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="076e6-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="076e6-203">Merhaba uygulamayı çalıştırın ve kayıt başarılı tuşuna basarak olduğunu doğrulayın ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="076e6-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![iOS Uygulaması Anında İletme Bildirimi Kayıt Testi][33]
2. <span data-ttu-id="076e6-205">Merhaba bir sınama anında iletme bildirimi gönderebilirsiniz [Azure Portal], yukarıda açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="076e6-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="076e6-206">Hello uygulamasında anında iletme bildirimleri göndermek için kod eklediyseniz, bir bildirim iletisi hello metin alanı tooenter dokunun.</span><span class="sxs-lookup"><span data-stu-id="076e6-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="076e6-207">Hello tuşuna **Gönder** hello klavye veya hello düğmesine **bildirim gönder** hello görünüm toosend hello bildirim iletisi düğmesini.</span><span class="sxs-lookup"><span data-stu-id="076e6-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![iOS Uygulaması Anında İletilen Bildirim Gönderme Testi][34]
3. <span data-ttu-id="076e6-209">Merhaba anında iletme bildirimi kayıtlı tooreceive hello bildirimleri tooall cihazlara gönderilen belirli bildirim Hub'hello.</span><span class="sxs-lookup"><span data-stu-id="076e6-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![iOS Uygulaması Anında İletilen Bildirim Alma Testi][35]

## <a name="next-steps"></a><span data-ttu-id="076e6-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="076e6-211">Next steps</span></span>
<span data-ttu-id="076e6-212">Bu basit örnekte, kayıtlı iOS cihazlarınıza anında iletme bildirimleri tooall yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="076e6-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="076e6-213">Toohello devam öğrendiklerinizi bir sonraki adım olarak önerdiğimiz [Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile iOS için] öğretici, bir arka uç toosend anında iletme bildirimleri etiketleri kullanarak oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="076e6-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="076e6-214">Kullanıcılarınızı ilgi alanı gruplarına göre toosegment isterseniz, ayrıca toohello üzerinde taşıyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="076e6-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="076e6-215">Notification Hubs hakkında genel bilgi için bkz. [Notification Hubs Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="076e6-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
[Mobile Services iOS SDK'sı sürüm 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile iOS için]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[yerel ve anında iletilen bildirim Programlama Kılavuzu]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure Portal]: https://portal.azure.com
