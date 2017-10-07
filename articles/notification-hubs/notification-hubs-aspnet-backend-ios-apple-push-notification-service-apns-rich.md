---
title: "aaaAzure bildirim hub'ları zengin bildirme"
description: "Nasıl toosend zengin Azure'dan bildirimleri tooan iOS uygulaması anında bilgi alın. Objective-C ve C# içinde yazılan kod örnekleri."
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="6a31e-104">Azure bildirim hub'ları zengin gönderme</span><span class="sxs-lookup"><span data-stu-id="6a31e-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="6a31e-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6a31e-105">Overview</span></span>
<span data-ttu-id="6a31e-106">Anlık zengin içeriğiyle sipariş tooengage kullanıcıların bir uygulama toopush düz metin ötesinde isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a31e-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="6a31e-107">Bu bildirimler kullanıcı etkileşimleri ve URL'ler, ses, görüntüler/kuponlar ve daha fazlasını gibi mevcut içeriği yükseltin.</span><span class="sxs-lookup"><span data-stu-id="6a31e-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="6a31e-108">Bu öğretici üzerinde hello derlemeler [kullanıcılara bildirme](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) konusuna ve toosend yüklerini (örneğin, görüntü) dahil bildirimleri nasıl anında iletme gösterir.</span><span class="sxs-lookup"><span data-stu-id="6a31e-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="6a31e-109">Bu öğretici, iOS 7 ve 8 ile uyumludur.</span><span class="sxs-lookup"><span data-stu-id="6a31e-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="6a31e-110">Yüksek düzeyde:</span><span class="sxs-lookup"><span data-stu-id="6a31e-110">At a high level:</span></span>

1. <span data-ttu-id="6a31e-111">Merhaba uygulama arka ucu:</span><span class="sxs-lookup"><span data-stu-id="6a31e-111">hello app backend:</span></span>
   * <span data-ttu-id="6a31e-112">Depoları hello zengin Yükü (Bu durumda, görüntü) hello arka uç veritabanı/yerel depolama</span><span class="sxs-lookup"><span data-stu-id="6a31e-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="6a31e-113">Bu zengin bildirim toohello aygıtın Kimliğini gönderir</span><span class="sxs-lookup"><span data-stu-id="6a31e-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="6a31e-114">Merhaba cihaza uygulamanın:</span><span class="sxs-lookup"><span data-stu-id="6a31e-114">App on hello device:</span></span>
   * <span data-ttu-id="6a31e-115">Arka uç hello zengin yükü aldığı hello kimlikli isteyen kişiler hello</span><span class="sxs-lookup"><span data-stu-id="6a31e-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="6a31e-116">Veri alma işlemi tamamlandığında ve hemen kullanıcılar toolearn daha fazla dokunduğunuzda hello yükü gösterir hello aygıtta kullanıcılara bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="6a31e-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="6a31e-117">Webapı proje</span><span class="sxs-lookup"><span data-stu-id="6a31e-117">WebAPI Project</span></span>
1. <span data-ttu-id="6a31e-118">Visual Studio'da hello açın **AppBackend** hello oluşturulan proje [kullanıcılara bildirme](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="6a31e-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="6a31e-119">Bir görüntü gibi toonotify kullanıcılarla ve bunu koymak elde bir **img** proje dizininizde klasör.</span><span class="sxs-lookup"><span data-stu-id="6a31e-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="6a31e-120">Tıklatın **tüm dosyaları göster** içinde Çözüm Gezgini hello ve çok hello klasörü sağ tıklatın**projeye dahil et**.</span><span class="sxs-lookup"><span data-stu-id="6a31e-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="6a31e-121">Seçili hello görüntüsüyle Özellikleri penceresinde yapı eylemi çok değiştirme**katıştırılmış kaynak**.</span><span class="sxs-lookup"><span data-stu-id="6a31e-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="6a31e-122">İçinde **Notifications.cs**, hello aşağıdaki ekleme deyimini kullanarak:</span><span class="sxs-lookup"><span data-stu-id="6a31e-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="6a31e-123">Güncelleştirme hello tüm **bildirimleri** koddan hello sınıfıyla.</span><span class="sxs-lookup"><span data-stu-id="6a31e-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="6a31e-124">Bildirim hub'ı kimlik bilgilerinizi ve görüntü dosya adı hello yer tutucularını emin tooreplace olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a31e-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="6a31e-125">(isteğe bağlı) Çok başvurmak[nasıl Visual C# kullanarak tooembed ve erişim kaynakları](http://support.microsoft.com/kb/319292) hakkında daha fazla bilgi için tooadd ve proje kaynakları alın.</span><span class="sxs-lookup"><span data-stu-id="6a31e-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="6a31e-126">İçinde **NotificationsController.cs**, yeniden tanımlamanız **NotificationsController** parçacıkları aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="6a31e-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="6a31e-127">Bu ilk sessiz zengin bildirim kimliği toodevice gönderir ve resmin istemci-tarafı alınmasına izin:</span><span class="sxs-lookup"><span data-stu-id="6a31e-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="6a31e-128">Sipariş toomake bu uygulama tooan Azure Web sitesi yeniden dağıtımını yapacaksınız şimdi onu tüm cihazlardan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="6a31e-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="6a31e-129">Merhaba üzerinde sağ **AppBackend** proje ve seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="6a31e-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="6a31e-130">Azure Web sitesi yayımlama hedefi olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="6a31e-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="6a31e-131">Azure hesabınızla oturum açın ve mevcut veya yeni bir Web sitesini seçin ve hello Not **hedef URL** hello özelliğinde **bağlantı** sekmesi. Toothis URL'si olarak başvuruda bulunacak, *arka uç nokta* Bu öğreticide daha sonra.</span><span class="sxs-lookup"><span data-stu-id="6a31e-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="6a31e-132">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6a31e-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="6a31e-133">Merhaba iOS projesi değiştirme</span><span class="sxs-lookup"><span data-stu-id="6a31e-133">Modify hello iOS project</span></span>
<span data-ttu-id="6a31e-134">Uygulama arka uç toosend yalnızca hello değiştirdiniz. göre *kimliği* ilişkin bir bildirim, siz iOS app toohandle bu kimliği değiştirebilir ve arka ucunuzdan hello zengin ileti almak.</span><span class="sxs-lookup"><span data-stu-id="6a31e-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="6a31e-135">İOS projenizi açın ve tooyour ana uygulama hedef hello giderek tarafından uzaktan bildirimlerini etkinleştirin **hedefleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="6a31e-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="6a31e-136">Tıklayın **yetenekleri**, Aç **arka plan modları**ve hello denetleyin **uzak bildirimler** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="6a31e-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="6a31e-137">Çok Git**Main.storyboard**ve gelen View Controller (giriş View Controller bu öğreticideki refered tooas) sahip olduğunuzdan emin olun [bildir kullanıcı](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="6a31e-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="6a31e-138">Ekleme bir **Gezinti denetleyicisi** tooyour film şeridi ve onu hello tooHome View Controller toomake control-sürükleyin **kök görünümü** gezinti.</span><span class="sxs-lookup"><span data-stu-id="6a31e-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="6a31e-139">Merhaba emin olun **ilk görünüm denetleyicisinin** öznitelikleri yalnızca hello Gezinti denetleyicisi için denetleyici seçilir.</span><span class="sxs-lookup"><span data-stu-id="6a31e-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="6a31e-140">Ekleme bir **View Controller** toostoryboard ve ekleme bir **görüntü Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="6a31e-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="6a31e-141">Bu hello notifiication üzerinde tıklayarak daha fazla toolearn seçtikten sonra kullanıcıların göreceği hello sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="6a31e-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="6a31e-142">Şeridinizin aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="6a31e-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="6a31e-143">Tıklatın hello üzerinde **giriş View Controller** film şeridi ve emin olun sahip **homeViewController** olarak kendi **özel sınıf** ve **film şeridi kimliği**hello kimlik denetçisi altında.</span><span class="sxs-lookup"><span data-stu-id="6a31e-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="6a31e-144">Aynı görüntü görünüm denetleyicisi hello **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="6a31e-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="6a31e-145">Ardından, başlıklı yeni bir görünüm denetleyici sınıfını oluşturmak **imageViewController** toohandle hello oluşturduğunuz kullanıcı Arabirimi.</span><span class="sxs-lookup"><span data-stu-id="6a31e-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="6a31e-146">İçinde **imageViewController.h**, toohello denetleyicinin arabirimi bildirimleri aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6a31e-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="6a31e-147">Merhaba film şeridi görüntü görünüm toothese özellikleri toolink hello iki gelen emin toocontrol sürükleme olun:</span><span class="sxs-lookup"><span data-stu-id="6a31e-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="6a31e-148">İçinde **imageViewController.m**, hello aşağıdaki hello sonuna Ekle **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="6a31e-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="6a31e-149">İçinde **AppDelegate.m**, oluşturduğunuz alma hello görüntü denetleyicisi:</span><span class="sxs-lookup"><span data-stu-id="6a31e-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="6a31e-150">Bir arabirim bölümüne bildiriminin hello ile ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6a31e-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="6a31e-151">İçinde **AppDelegate**, emin olun, uygulamanızın sessiz bildirimleri için kayıtları **uygulama: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="6a31e-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. <span data-ttu-id="6a31e-152">Uygulama için aşağıdaki hello DEVICEHIGH **uygulama: didRegisterForRemoteNotificationsWithDeviceToken** tootake hello film şeridi UI dikkate değiştirir:</span><span class="sxs-lookup"><span data-stu-id="6a31e-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="6a31e-153">Ardından, yöntem çok aşağıdaki hello ekleyin**AppDelegate.m** tooretrieve hello uç noktanızı görüntüden ve alma işlemi tamamlandığında, yerel bir bildirim gönderecek.</span><span class="sxs-lookup"><span data-stu-id="6a31e-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="6a31e-154">Emin toosubstitute hello yer tutucu olun `{backend endpoint}` arka uç noktası ile:</span><span class="sxs-lookup"><span data-stu-id="6a31e-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="6a31e-155">Merhaba görüntü görünüm denetleyicisini açarak yukarıda Hello yerel bildirimi tutamacı **AppDelegate.m** yöntemler aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="6a31e-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a><span data-ttu-id="6a31e-156">Merhaba uygulama çalıştırın</span><span class="sxs-lookup"><span data-stu-id="6a31e-156">Run hello Application</span></span>
1. <span data-ttu-id="6a31e-157">Xcode'da, fiziksel bir iOS cihazında (anında iletme bildirimleri hello benzeticisinde çalışmaz) hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6a31e-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="6a31e-158">Merhaba iOS uygulama kullanıcı Arabirimi, bir kullanıcı adını ve parolasını aynı değeri için kimlik doğrulaması ve tıklayın hello girin **oturum**.</span><span class="sxs-lookup"><span data-stu-id="6a31e-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="6a31e-159">Tıklatın **Gönder itme** ve bir uygulama uyarı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a31e-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="6a31e-160">Üzerinde tıklatırsanız **daha fazla**, uygulama arka ucunda, seçtiğiniz tooinclude duruma toohello görüntü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6a31e-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="6a31e-161">Tıklatarak **Gönder itme** ve hemen aygıtınızın hello giriş düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="6a31e-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="6a31e-162">Birkaç dakika sonra bir anında iletme bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6a31e-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="6a31e-163">Üzerinde dokunun veya daha fazla tıklatın, tooyour uygulama ve hello zengin görüntü içeriğini gidersiniz.</span><span class="sxs-lookup"><span data-stu-id="6a31e-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
