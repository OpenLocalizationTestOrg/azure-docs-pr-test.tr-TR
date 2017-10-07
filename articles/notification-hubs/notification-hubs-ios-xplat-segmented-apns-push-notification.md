---
title: "aaaNotification hub çiğnemekten haber Öğreticisi - iOS"
description: "Bilgi nasıl toouse Azure hizmet veri yolu bildirim hub'ları toosend haber bildirimleri tooiOS aygıtları kesiliyor."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="72b65-103">Bildirim hub'ları toosend son dakika haberleri kullanın</span><span class="sxs-lookup"><span data-stu-id="72b65-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="72b65-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="72b65-104">Overview</span></span>
<span data-ttu-id="72b65-105">Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast son dakika haberleri bildirimleri tooan iOS uygulaması.</span><span class="sxs-lookup"><span data-stu-id="72b65-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="72b65-106">Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak.</span><span class="sxs-lookup"><span data-stu-id="72b65-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="72b65-107">Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin, RSS Okuyucu, müzik fanlar, vb. için uygulamaları ilgi bildirilen kullanıcıların sahip olduğu bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="72b65-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="72b65-108">Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken.</span><span class="sxs-lookup"><span data-stu-id="72b65-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="72b65-109">Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="72b65-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="72b65-110">Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="72b65-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="72b65-111">Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="72b65-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72b65-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="72b65-112">Prerequisites</span></span>
<span data-ttu-id="72b65-113">Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="72b65-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="72b65-114">Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="72b65-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="72b65-115">Kategori seçimi toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="72b65-115">Add category selection toohello app</span></span>
<span data-ttu-id="72b65-116">Merhaba ilk hello kullanıcı tooselect kategorileri tooregister sağlayan tooadd hello kullanıcı Arabirimi öğeleri tooyour varolan film şeridi adımdır.</span><span class="sxs-lookup"><span data-stu-id="72b65-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="72b65-117">bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır.</span><span class="sxs-lookup"><span data-stu-id="72b65-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="72b65-118">Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="72b65-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="72b65-119">MainStoryboard_iPhone.storyboard bileşenleri hello nesne kitaplığından aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="72b65-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="72b65-120">Bir etiket "Haber sonu" metni ile</span><span class="sxs-lookup"><span data-stu-id="72b65-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="72b65-121">Kategori metinleri ile etiketler "World", "Siyaset", "İş", "Teknolojisinin", "Bilim", "Spor",</span><span class="sxs-lookup"><span data-stu-id="72b65-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="72b65-122">Her kategori, altı anahtarları ayarlamak her anahtar **durumu** toobe **kapalı** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="72b65-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="72b65-123">Bir düğme "Abonelik" olarak etiketlenmiş</span><span class="sxs-lookup"><span data-stu-id="72b65-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="72b65-124">Şeridinizin aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="72b65-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="72b65-125">Merhaba Yardımcısı düzenleyicisinde çıkışlar tüm hello anahtarları oluşturmak ve "WorldSwitch", çağrı "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="72b65-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="72b65-126">"Abone" olarak adlandırılan, düğme için bir eylem oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72b65-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="72b65-127">ViewController.h hello şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="72b65-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="72b65-128">Yeni bir **Cocoa Touch sınıfı** adlı `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="72b65-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="72b65-129">Kod Notifications.h hello dosyasının hello arabirimi bölümünde aşağıdaki hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="72b65-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="72b65-130">İçe aktarma yönergesi tooNotifications.m aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="72b65-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="72b65-131">Kod Notifications.m hello dosyasının hello uygulama bölümünde aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="72b65-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    <span data-ttu-id="72b65-132">Bu sınıf, yerel depolama toostore kullanır ve bu aygıt alacak Haberler hello kategorileri alma.</span><span class="sxs-lookup"><span data-stu-id="72b65-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="72b65-133">Ayrıca, bir yöntem tooregister kullanarak bu kategorilerin içeren bir [şablonu](notification-hubs-templates-cross-platform-push-messages.md) kayıt.</span><span class="sxs-lookup"><span data-stu-id="72b65-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="72b65-134">Merhaba AppDelegate.h dosyasında Notifications.h için bir içeri aktarma deyimini ekleyin ve hello bildirimleri sınıfı örneği için bir özellik ekleyin:</span><span class="sxs-lookup"><span data-stu-id="72b65-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="72b65-135">Merhaba, **didFinishLaunchingWithOptions** AppDelegate.m, yönteminde hello hello yöntemi başında hello kod tooinitialize hello bildirimleri örneği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72b65-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="72b65-136">`HUBNAME`ve `HUBLISTENACCESS` (hubınfo.h içinde tanımlanmıştır) hello zaten yüklü olmalıdır `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucular yerine *DefaultListenSharedAccessSignature*daha önce edindiğiniz</span><span class="sxs-lookup"><span data-stu-id="72b65-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="72b65-137">Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak.</span><span class="sxs-lookup"><span data-stu-id="72b65-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="72b65-138">Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="72b65-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="72b65-139">Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="72b65-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="72b65-140">Merhaba, **didRegisterForRemoteNotificationsWithDeviceToken** AppDelegate.m, yönteminde hello yöntemi hello kodda kod toopass hello cihaz belirteci toohello bildirimleri sınıfı aşağıdaki hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="72b65-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="72b65-141">Merhaba bildirimleri sınıfı hello hello kategorilerle bildirimlere kaydolma işlemini gerçekleştirecek.</span><span class="sxs-lookup"><span data-stu-id="72b65-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="72b65-142">Merhaba kullanıcı kategori seçimlerinin değişirse Merhaba diyoruz `subscribeWithCategories` yanıt toohello yönteminde **abone** düğmesini tooupdate bunları.</span><span class="sxs-lookup"><span data-stu-id="72b65-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="72b65-143">Apple anında iletilen bildirim servisi (APNS) Hello tarafından atanan hello cihaz belirteci herhangi bir anda fırsat çünkü bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="72b65-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="72b65-144">Bu hello uygulama her başlatıldığında bu örnek bir bildirime kaydolur.</span><span class="sxs-lookup"><span data-stu-id="72b65-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="72b65-145">Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72b65-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="72b65-146">Bu noktada olması gereken başka bir kod hello Not **didRegisterForRemoteNotificationsWithDeviceToken** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="72b65-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="72b65-147">Merhaba aşağıdaki yöntemlerden zaten hello tamamlamanızı AppDelegate.m içinde bulunması gereken [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="72b65-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="72b65-148">Yoksa, bunları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72b65-148">If not, add them.</span></span>
   
    <span data-ttu-id="72b65-149">-(void) MessageBox:(NSString *) başlık iletisi:(NSString *) ileti metni {</span><span class="sxs-lookup"><span data-stu-id="72b65-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="72b65-150">}</span><span class="sxs-lookup"><span data-stu-id="72b65-150">}</span></span>
   
   * <span data-ttu-id="72b65-151">(void) uygulama:(UIApplication *) uygulama didReceiveRemoteNotification: (NSDictionary *) kullanıcı bilgisi {NSLog (@"% @", kullanıcı bilgisi);   [kendini MessageBox:@"Notification" iletisi: [[kullanıcı bilgisi objectForKey:@"aps"] valueForKey:@"alert"]]; }</span><span class="sxs-lookup"><span data-stu-id="72b65-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="72b65-152">Bu yöntem hello uygulama basit bir görüntüleyerek çalışırken alınan bildirimlerini işleme **Uıalert**.</span><span class="sxs-lookup"><span data-stu-id="72b65-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="72b65-153">ViewController.m içinde alma kodu hello aşağıdaki AppDelegate.h ve kopyalama hello için deyimine XCode oluşturulan **abone** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="72b65-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="72b65-154">Bu kod hello kullanıcı arabiriminde hello kullanıcının seçtiği hello bildirim kayıt toouse hello yeni kategori etiketleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="72b65-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   <span data-ttu-id="72b65-155">Bu yöntem oluşturur bir **NSMutableArray** kategorileri ve kullandığı Merhaba, **bildirimleri** sınıfı toostore hello hello yerel depolama ve kayıtları hello karşılık gelen etiketleriyle bildirim hub'ınızı listesinde.</span><span class="sxs-lookup"><span data-stu-id="72b65-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="72b65-156">Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="72b65-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="72b65-157">Merhaba kodda aşağıdaki hello ViewController.m içinde eklemek **viewDidLoad** yöntemi tooset hello kullanıcı arabirimi tabanlı önceden kaydedilmiş hello kategorilerindeki.</span><span class="sxs-lookup"><span data-stu-id="72b65-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="72b65-158">Merhaba uygulamasını başlattığında hello uygulama artık kategorileri kümesi hello aygıt kullanılan yerel depolama tooregister hello bildirim hub'ı ile depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72b65-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="72b65-159">Merhaba kullanıcı kategorileri çalışma zamanında hello Seçimi değiştirip hello'ı **abone** yöntemi tooupdate hello kayıt hello cihaz için.</span><span class="sxs-lookup"><span data-stu-id="72b65-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="72b65-160">Ardından, haberi bildirimleri doğrudan hello uygulama içinde kesme hello uygulama toosend hello güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="72b65-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="72b65-161">(isteğe bağlı) Etiketli bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="72b65-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="72b65-162">Erişim tooVisual Studio yoksa, toohello sonraki bölüm atlayın ve hello uygulamadan kendisini bildirimleri gönderin.</span><span class="sxs-lookup"><span data-stu-id="72b65-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="72b65-163">Merhaba uygun şablon bildirim hello gönderebilirsiniz [Klasik Azure portalı] için bildirim hub'ınız hello hata ayıklama sekmesini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="72b65-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="72b65-164">(isteğe bağlı) Merhaba aygıttan bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="72b65-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="72b65-165">Normalde bildirimleri bir arka uç hizmeti tarafından gönderilir ancak doğrudan hello uygulamadan son dakika haberi bildirimleri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="72b65-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="72b65-166">toodo bu güncelleştiriyoruz hello `SendNotificationRESTAPI` hello tanımladığımız yöntemi [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="72b65-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="72b65-167">ViewController.m güncelleştirme hello içinde `SendNotificationRESTAPI` yöntemi olarak, böylece hello kategori etiketi için bir parametre kabul eder ve uygun hello gönderir izleyen [şablonu](notification-hubs-templates-cross-platform-push-messages.md) bildirim.</span><span class="sxs-lookup"><span data-stu-id="72b65-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. <span data-ttu-id="72b65-168">ViewController.m güncelleştirme hello içinde **bildirim gönder** izleyen hello kodda gösterildiği gibi eylem.</span><span class="sxs-lookup"><span data-stu-id="72b65-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="72b65-169">Göndereceğiz böylece her kullanarak hello bildirimleri tek tek etiket ve toomultiple platformları gönderin.</span><span class="sxs-lookup"><span data-stu-id="72b65-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="72b65-170">Projenizi yeniden derleyin ve hiçbir derleme hataları olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="72b65-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="72b65-171">Merhaba uygulamayı çalıştırın ve bildirimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="72b65-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="72b65-172">Tuşuna hello düğmesi toobuild Merhaba projeyi çalıştırın ve hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="72b65-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="72b65-173">Bazı son dakika haberleri seçenekleri toosubscribe tooand seçin sonra basın hello **abone ol** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72b65-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="72b65-174">Bildirimler için abone olunmuş hello belirten bir iletişim kutusu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="72b65-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="72b65-175">Seçtiğinizde **abone ol**, uygulama dönüştürür seçili hello kategorileri etiketlerine hello ve seçili hello etiketleri için yeni bir cihaz kaydı hello bildirim hub'ından ister.</span><span class="sxs-lookup"><span data-stu-id="72b65-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="72b65-176">Son dakika haberleri tuşuna gibi hello gönderilen bir ileti toobe girin **bildirim gönder** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="72b65-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="72b65-177">Alternatif olarak, hello .NET konsol uygulaması toogenerate bildirimleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72b65-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="72b65-178">Her abone aygıt toobreaking haber yalnızca gönderilen hello son dakika haberi bildirimleri alır.</span><span class="sxs-lookup"><span data-stu-id="72b65-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b65-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72b65-179">Next steps</span></span>
<span data-ttu-id="72b65-180">Biz bu öğreticide öğrenilen nasıl kategoriye göre son dakika haberleri toobroadcast.</span><span class="sxs-lookup"><span data-stu-id="72b65-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="72b65-181">Diğer gelişmiş Notification Hubs senaryoları vurgulayın öğreticileri aşağıdaki hello birini Tamamlanıyor göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="72b65-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="72b65-182">**[Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]**</span><span class="sxs-lookup"><span data-stu-id="72b65-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="72b65-183">Haber uygulama tooenable göndermek çiğnemekten tooexpand hello bildirimleri nasıl yerelleştirilmiş öğrenin.</span><span class="sxs-lookup"><span data-stu-id="72b65-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[Klasik Azure portalı]: https://manage.windowsazure.com
