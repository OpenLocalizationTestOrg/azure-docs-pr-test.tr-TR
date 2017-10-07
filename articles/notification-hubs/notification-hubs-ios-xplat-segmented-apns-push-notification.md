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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Bildirim hub'ları toosend son dakika haberleri kullanın
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast son dakika haberleri bildirimleri tooan iOS uygulaması. Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak. Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin, RSS Okuyucu, müzik fanlar, vb. için uygulamaları ilgi bildirilen kullanıcıların sahip olduğu bir senaryodur.

Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken. Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız. Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez. Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Ön koşullar
Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started]. Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].

## <a name="add-category-selection-toohello-app"></a>Kategori seçimi toohello uygulama Ekle
Merhaba ilk hello kullanıcı tooselect kategorileri tooregister sağlayan tooadd hello kullanıcı Arabirimi öğeleri tooyour varolan film şeridi adımdır. bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır. Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.

1. MainStoryboard_iPhone.storyboard bileşenleri hello nesne kitaplığından aşağıdaki hello ekleyin:
   
   * Bir etiket "Haber sonu" metni ile
   * Kategori metinleri ile etiketler "World", "Siyaset", "İş", "Teknolojisinin", "Bilim", "Spor",
   * Her kategori, altı anahtarları ayarlamak her anahtar **durumu** toobe **kapalı** varsayılan olarak.
   * Bir düğme "Abonelik" olarak etiketlenmiş
     
     Şeridinizin aşağıdaki gibi görünmelidir:
     
     ![][3]
2. Merhaba Yardımcısı düzenleyicisinde çıkışlar tüm hello anahtarları oluşturmak ve "WorldSwitch", çağrı "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"
3. "Abone" olarak adlandırılan, düğme için bir eylem oluşturun. ViewController.h hello şunları içermelidir:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Yeni bir **Cocoa Touch sınıfı** adlı `Notifications`. Kod Notifications.h hello dosyasının hello arabirimi bölümünde aşağıdaki hello kopyalayın:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. İçe aktarma yönergesi tooNotifications.m aşağıdaki hello ekleyin:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Kod Notifications.m hello dosyasının hello uygulama bölümünde aşağıdaki hello kopyalayın.
   
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



    Bu sınıf, yerel depolama toostore kullanır ve bu aygıt alacak Haberler hello kategorileri alma. Ayrıca, bir yöntem tooregister kullanarak bu kategorilerin içeren bir [şablonu](notification-hubs-templates-cross-platform-push-messages.md) kayıt.

1. Merhaba AppDelegate.h dosyasında Notifications.h için bir içeri aktarma deyimini ekleyin ve hello bildirimleri sınıfı örneği için bir özellik ekleyin:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. Merhaba, **didFinishLaunchingWithOptions** AppDelegate.m, yönteminde hello hello yöntemi başında hello kod tooinitialize hello bildirimleri örneği ekleyin.  
   
    `HUBNAME`ve `HUBLISTENACCESS` (hubınfo.h içinde tanımlanmıştır) hello zaten yüklü olmalıdır `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucular yerine *DefaultListenSharedAccessSignature*daha önce edindiğiniz
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak. Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor. Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.
   > 
   > 
3. Merhaba, **didRegisterForRemoteNotificationsWithDeviceToken** AppDelegate.m, yönteminde hello yöntemi hello kodda kod toopass hello cihaz belirteci toohello bildirimleri sınıfı aşağıdaki hello ile değiştirin. Merhaba bildirimleri sınıfı hello hello kategorilerle bildirimlere kaydolma işlemini gerçekleştirecek. Merhaba kullanıcı kategori seçimlerinin değişirse Merhaba diyoruz `subscribeWithCategories` yanıt toohello yönteminde **abone** düğmesini tooupdate bunları.
   
   > [!NOTE]
   > Apple anında iletilen bildirim servisi (APNS) Hello tarafından atanan hello cihaz belirteci herhangi bir anda fırsat çünkü bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz. Bu hello uygulama her başlatıldığında bu örnek bir bildirime kaydolur. Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.
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

    Bu noktada olması gereken başka bir kod hello Not **didRegisterForRemoteNotificationsWithDeviceToken** yöntemi.

1. Merhaba aşağıdaki yöntemlerden zaten hello tamamlamanızı AppDelegate.m içinde bulunması gereken [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.  Yoksa, bunları ekleyin.
   
    -(void) MessageBox:(NSString *) başlık iletisi:(NSString *) ileti metni {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * (void) uygulama:(UIApplication *) uygulama didReceiveRemoteNotification: (NSDictionary *) kullanıcı bilgisi {NSLog (@"% @", kullanıcı bilgisi);   [kendini MessageBox:@"Notification" iletisi: [[kullanıcı bilgisi objectForKey:@"aps"] valueForKey:@"alert"]]; }
   
   Bu yöntem hello uygulama basit bir görüntüleyerek çalışırken alınan bildirimlerini işleme **Uıalert**.
2. ViewController.m içinde alma kodu hello aşağıdaki AppDelegate.h ve kopyalama hello için deyimine XCode oluşturulan **abone** yöntemi. Bu kod hello kullanıcı arabiriminde hello kullanıcının seçtiği hello bildirim kayıt toouse hello yeni kategori etiketleri güncelleştirir.
   
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
   
   Bu yöntem oluşturur bir **NSMutableArray** kategorileri ve kullandığı Merhaba, **bildirimleri** sınıfı toostore hello hello yerel depolama ve kayıtları hello karşılık gelen etiketleriyle bildirim hub'ınızı listesinde. Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.
3. Merhaba kodda aşağıdaki hello ViewController.m içinde eklemek **viewDidLoad** yöntemi tooset hello kullanıcı arabirimi tabanlı önceden kaydedilmiş hello kategorilerindeki.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



Merhaba uygulamasını başlattığında hello uygulama artık kategorileri kümesi hello aygıt kullanılan yerel depolama tooregister hello bildirim hub'ı ile depolayabilirsiniz.  Merhaba kullanıcı kategorileri çalışma zamanında hello Seçimi değiştirip hello'ı **abone** yöntemi tooupdate hello kayıt hello cihaz için. Ardından, haberi bildirimleri doğrudan hello uygulama içinde kesme hello uygulama toosend hello güncelleştirir.

## <a name="optional-sending-tagged-notifications"></a>(isteğe bağlı) Etiketli bildirimleri gönderme
Erişim tooVisual Studio yoksa, toohello sonraki bölüm atlayın ve hello uygulamadan kendisini bildirimleri gönderin. Merhaba uygun şablon bildirim hello gönderebilirsiniz [Klasik Azure portalı] için bildirim hub'ınız hello hata ayıklama sekmesini kullanarak. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(isteğe bağlı) Merhaba aygıttan bildirimleri gönderme
Normalde bildirimleri bir arka uç hizmeti tarafından gönderilir ancak doğrudan hello uygulamadan son dakika haberi bildirimleri gönderebilir. toodo bu güncelleştiriyoruz hello `SendNotificationRESTAPI` hello tanımladığımız yöntemi [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.

1. ViewController.m güncelleştirme hello içinde `SendNotificationRESTAPI` yöntemi olarak, böylece hello kategori etiketi için bir parametre kabul eder ve uygun hello gönderir izleyen [şablonu](notification-hubs-templates-cross-platform-push-messages.md) bildirim.
   
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
2. ViewController.m güncelleştirme hello içinde **bildirim gönder** izleyen hello kodda gösterildiği gibi eylem. Göndereceğiz böylece her kullanarak hello bildirimleri tek tek etiket ve toomultiple platformları gönderin.

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



1. Projenizi yeniden derleyin ve hiçbir derleme hataları olduğundan emin olun.

## <a name="run-hello-app-and-generate-notifications"></a>Merhaba uygulamayı çalıştırın ve bildirimler oluşturma
1. Tuşuna hello düğmesi toobuild Merhaba projeyi çalıştırın ve hello uygulamayı başlatın. Bazı son dakika haberleri seçenekleri toosubscribe tooand seçin sonra basın hello **abone ol** düğmesi. Bildirimler için abone olunmuş hello belirten bir iletişim kutusu görmeniz gerekir.
   
    ![][1]
   
    Seçtiğinizde **abone ol**, uygulama dönüştürür seçili hello kategorileri etiketlerine hello ve seçili hello etiketleri için yeni bir cihaz kaydı hello bildirim hub'ından ister.
2. Son dakika haberleri tuşuna gibi hello gönderilen bir ileti toobe girin **bildirim gönder** düğmesi. Alternatif olarak, hello .NET konsol uygulaması toogenerate bildirimleri çalıştırın.
   
    ![][2]
3. Her abone aygıt toobreaking haber yalnızca gönderilen hello son dakika haberi bildirimleri alır.

## <a name="next-steps"></a>Sonraki adımlar
Biz bu öğreticide öğrenilen nasıl kategoriye göre son dakika haberleri toobroadcast. Diğer gelişmiş Notification Hubs senaryoları vurgulayın öğreticileri aşağıdaki hello birini Tamamlanıyor göz önünde bulundurun:

* **[Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]**
  
    Haber uygulama tooenable göndermek çiğnemekten tooexpand hello bildirimleri nasıl yerelleştirilmiş öğrenin.

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
