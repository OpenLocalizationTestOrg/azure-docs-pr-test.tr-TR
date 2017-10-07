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
# <a name="azure-notification-hubs-rich-push"></a>Azure bildirim hub'ları zengin gönderme
## <a name="overview"></a>Genel Bakış
Anlık zengin içeriğiyle sipariş tooengage kullanıcıların bir uygulama toopush düz metin ötesinde isteyebilirsiniz. Bu bildirimler kullanıcı etkileşimleri ve URL'ler, ses, görüntüler/kuponlar ve daha fazlasını gibi mevcut içeriği yükseltin. Bu öğretici üzerinde hello derlemeler [kullanıcılara bildirme](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) konusuna ve toosend yüklerini (örneğin, görüntü) dahil bildirimleri nasıl anında iletme gösterir.

Bu öğretici, iOS 7 ve 8 ile uyumludur.

  ![][IOS1]

Yüksek düzeyde:

1. Merhaba uygulama arka ucu:
   * Depoları hello zengin Yükü (Bu durumda, görüntü) hello arka uç veritabanı/yerel depolama
   * Bu zengin bildirim toohello aygıtın Kimliğini gönderir
2. Merhaba cihaza uygulamanın:
   * Arka uç hello zengin yükü aldığı hello kimlikli isteyen kişiler hello
   * Veri alma işlemi tamamlandığında ve hemen kullanıcılar toolearn daha fazla dokunduğunuzda hello yükü gösterir hello aygıtta kullanıcılara bildirim gönderme

## <a name="webapi-project"></a>Webapı proje
1. Visual Studio'da hello açın **AppBackend** hello oluşturulan proje [kullanıcılara bildirme](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) Öğreticisi.
2. Bir görüntü gibi toonotify kullanıcılarla ve bunu koymak elde bir **img** proje dizininizde klasör.
3. Tıklatın **tüm dosyaları göster** içinde Çözüm Gezgini hello ve çok hello klasörü sağ tıklatın**projeye dahil et**.
4. Seçili hello görüntüsüyle Özellikleri penceresinde yapı eylemi çok değiştirme**katıştırılmış kaynak**.
   
    ![][IOS2]
5. İçinde **Notifications.cs**, hello aşağıdaki ekleme deyimini kullanarak:
   
        using System.Reflection;
6. Güncelleştirme hello tüm **bildirimleri** koddan hello sınıfıyla. Bildirim hub'ı kimlik bilgilerinizi ve görüntü dosya adı hello yer tutucularını emin tooreplace olabilir.
   
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
   > (isteğe bağlı) Çok başvurmak[nasıl Visual C# kullanarak tooembed ve erişim kaynakları](http://support.microsoft.com/kb/319292) hakkında daha fazla bilgi için tooadd ve proje kaynakları alın.
   > 
   > 
7. İçinde **NotificationsController.cs**, yeniden tanımlamanız **NotificationsController** parçacıkları aşağıdaki hello ile. Bu ilk sessiz zengin bildirim kimliği toodevice gönderir ve resmin istemci-tarafı alınmasına izin:
   
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
8. Sipariş toomake bu uygulama tooan Azure Web sitesi yeniden dağıtımını yapacaksınız şimdi onu tüm cihazlardan erişilebilir. Merhaba üzerinde sağ **AppBackend** proje ve seçin **Yayımla**.
9. Azure Web sitesi yayımlama hedefi olarak seçin. Azure hesabınızla oturum açın ve mevcut veya yeni bir Web sitesini seçin ve hello Not **hedef URL** hello özelliğinde **bağlantı** sekmesi. Toothis URL'si olarak başvuruda bulunacak, *arka uç nokta* Bu öğreticide daha sonra. **Yayımla**’ta tıklayın.

## <a name="modify-hello-ios-project"></a>Merhaba iOS projesi değiştirme
Uygulama arka uç toosend yalnızca hello değiştirdiniz. göre *kimliği* ilişkin bir bildirim, siz iOS app toohandle bu kimliği değiştirebilir ve arka ucunuzdan hello zengin ileti almak.

1. İOS projenizi açın ve tooyour ana uygulama hedef hello giderek tarafından uzaktan bildirimlerini etkinleştirin **hedefleri** bölümü.
2. Tıklayın **yetenekleri**, Aç **arka plan modları**ve hello denetleyin **uzak bildirimler** onay kutusu.
   
    ![][IOS3]
3. Çok Git**Main.storyboard**ve gelen View Controller (giriş View Controller bu öğreticideki refered tooas) sahip olduğunuzdan emin olun [bildir kullanıcı](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) Öğreticisi.
4. Ekleme bir **Gezinti denetleyicisi** tooyour film şeridi ve onu hello tooHome View Controller toomake control-sürükleyin **kök görünümü** gezinti. Merhaba emin olun **ilk görünüm denetleyicisinin** öznitelikleri yalnızca hello Gezinti denetleyicisi için denetleyici seçilir.
5. Ekleme bir **View Controller** toostoryboard ve ekleme bir **görüntü Görünüm**. Bu hello notifiication üzerinde tıklayarak daha fazla toolearn seçtikten sonra kullanıcıların göreceği hello sayfasıdır. Şeridinizin aşağıdaki gibi görünmelidir:
   
    ![][IOS4]
6. Tıklatın hello üzerinde **giriş View Controller** film şeridi ve emin olun sahip **homeViewController** olarak kendi **özel sınıf** ve **film şeridi kimliği**hello kimlik denetçisi altında.
7. Aynı görüntü görünüm denetleyicisi hello **imageViewController**.
8. Ardından, başlıklı yeni bir görünüm denetleyici sınıfını oluşturmak **imageViewController** toohandle hello oluşturduğunuz kullanıcı Arabirimi.
9. İçinde **imageViewController.h**, toohello denetleyicinin arabirimi bildirimleri aşağıdaki hello ekleyin. Merhaba film şeridi görüntü görünüm toothese özellikleri toolink hello iki gelen emin toocontrol sürükleme olun:
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. İçinde **imageViewController.m**, hello aşağıdaki hello sonuna Ekle **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. İçinde **AppDelegate.m**, oluşturduğunuz alma hello görüntü denetleyicisi:
    
        #import "imageViewController.h"
12. Bir arabirim bölümüne bildiriminin hello ile ekleyin:
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. İçinde **AppDelegate**, emin olun, uygulamanızın sessiz bildirimleri için kayıtları **uygulama: didFinishLaunchingWithOptions**:
    
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

1. Uygulama için aşağıdaki hello DEVICEHIGH **uygulama: didRegisterForRemoteNotificationsWithDeviceToken** tootake hello film şeridi UI dikkate değiştirir:
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. Ardından, yöntem çok aşağıdaki hello ekleyin**AppDelegate.m** tooretrieve hello uç noktanızı görüntüden ve alma işlemi tamamlandığında, yerel bir bildirim gönderecek. Emin toosubstitute hello yer tutucu olun `{backend endpoint}` arka uç noktası ile:
   
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
3. Merhaba görüntü görünüm denetleyicisini açarak yukarıda Hello yerel bildirimi tutamacı **AppDelegate.m** yöntemler aşağıdaki hello ile:
   
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

## <a name="run-hello-application"></a>Merhaba uygulama çalıştırın
1. Xcode'da, fiziksel bir iOS cihazında (anında iletme bildirimleri hello benzeticisinde çalışmaz) hello uygulamayı çalıştırın.
2. Merhaba iOS uygulama kullanıcı Arabirimi, bir kullanıcı adını ve parolasını aynı değeri için kimlik doğrulaması ve tıklayın hello girin **oturum**.
3. Tıklatın **Gönder itme** ve bir uygulama uyarı görmeniz gerekir. Üzerinde tıklatırsanız **daha fazla**, uygulama arka ucunda, seçtiğiniz tooinclude duruma toohello görüntü olacaktır.
4. Tıklatarak **Gönder itme** ve hemen aygıtınızın hello giriş düğmesine basın. Birkaç dakika sonra bir anında iletme bildirimi alırsınız. Üzerinde dokunun veya daha fazla tıklatın, tooyour uygulama ve hello zengin görüntü içeriğini gidersiniz.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
