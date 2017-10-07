---
title: "aaaNotification Hubs yerelleştirilmiş çiğnemekten haber Öğreticisi iOS için"
description: "Son dakika haberi bildirimleri (iOS) nasıl toouse Azure hizmet veri yolu bildirim hub'ları toosend yerelleştirilmiş öğrenin."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Bildirim hub'ları yerelleştirilmiş toosend son dakika haberleri tooiOS aygıtları'nı kullanın
> [!div class="op_single_selector"]
> * [Windows mağazası C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl gösterir toouse hello [şablonları](notification-hubs-templates-cross-platform-push-messages.md) dil ve cihaz tarafından yerelleştirilmiş haberi bildirimleri çiğnemekten Azure Notification Hubs toobroadcast özelliğidir. Bu öğreticide oluşturduğunuz hello iOS uygulaması ile başlamanız [son dakika haberleri Notification Hubs kullanma toosend]. Tamamlandığında, ilgilendiğiniz kategorileri için mümkün tooregister olacaktır, hangi tooreceive hello bildirimleri bir dil belirtin ve yalnızca anında iletme bildirimlerini seçili hello kategorileri için o dilde alırsınız.

İki bölümden toothis senaryo vardır:

* iOS uygulamanızın istemci cihazları toospecify bir dil ve haber kategorileri çiğnemekten toosubscribe toodifferent olanak tanır;
* Merhaba arka uç yayınlar hello kullanarak hello bildirimleri **etiketi** ve **şablonu** Azure bildirim hub'larını feautres.

## <a name="prerequisites"></a>Ön koşullar
Önceden hello tamamlamış olmalıdır [son dakika haberleri Notification Hubs kullanma toosend] öğretici ve bu öğreticinin bu kodu doğrudan derlemeler için kullanılabilir, hello koduna sahip.

Visual Studio 2012 veya sonraki sürümünü isteğe bağlıdır.

## <a name="template-concepts"></a>Şablon kavramları
İçinde [son dakika haberleri Notification Hubs kullanma toosend] kullanılan bir uygulama yerleşik **etiketleri** toosubscribe toonotifications farklı haber kategorileri için.
Birçok uygulama, ancak, birden çok pazarda hedef ve yerelleştirme gerektirir. Bunun anlamı hello bildirimleri kendilerini Merhaba içeriğine sahip yerelleştirilmiş toobe ve teslim toohello cihaz kümesini düzeltin.
Bu konudaki göstereceğiz nasıl toouse hello **şablonu** özellik bildirim hub'larını tooeasily teslim yerelleştirilmiş son dakika haberi bildirimleri.

Not: tek yönlü toosend yerelleştirilmiş bildirimleri toocreate her etiket birden çok sürümünün olduğu. Örneğin, toosupport İngilizce, Fransızca ve Mandarin, üç farklı etiketler world haberler için ihtiyacımız: "world_en", "world_fr" ve "world_ch". Toosend sonra hello world haber tooeach bu etiketlerin yerelleştirilmiş bir sürümü gerekir. Bu konudaki şablonları tooavoid hello artışı etiketleri ve birden fazla ileti gönderme hello gereksinimi kullanın.

Yüksek bir düzeyde bir şekilde toospecify şablonlarıdır nasıl belirli bir aygıt bir bildirim almanız gerekir. Merhaba şablon, uygulama arka ucu tarafından gönderilen Merhaba ileti parçası olan tooproperties bakarak hello tam yük biçimi belirtir. Örneğimizde, biz tüm desteklenen diller içeren bir yerel ayar belirsiz ileti gönderir:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Ardından cihazlarını toohello doğru özellik başvuran bir şablonla kaydetmek sağlayacaktır. Örneğin, Fransızca haberler için tooregister istediği bir iOS uygulaması hello aşağıdaki kaydeder:

    {
        aps:{
            alert: "$(News_French)"
        }
    }

Şablonlar, daha fazla bilgi bulabilir hakkında içinde çok güçlü bir özellik olan bizim [şablonları](notification-hubs-templates-cross-platform-push-messages.md) makalesi.

## <a name="hello-app-user-interface"></a>Merhaba uygulama kullanıcı arabirimi
Biz şimdi hello konuda oluşturulan hello çiğnemekten haber uygulama değiştirecek [son dakika haberleri Notification Hubs kullanma toosend] toosend yerelleştirilmiş şablonları kullanarak son dakika haberleri.

MainStoryboard_iPhone.storyboard, biz destekleyecek hello üç dilleri ile bölümlenmiş bir denetim ekleyin: İngilizce, Fransızca ve Mandarin.

![][13]

Ardından emin tooadd bir IBOutlet, ViewController.h aşağıda gösterildiği gibi yapın:

![][14]

## <a name="building-hello-ios-app"></a>Yapı hello iOS uygulaması
1. Merhaba, Notification.h eklemek *retrieveLocale* yöntemi, hello deposu değiştirmek ve yöntemleri aşağıda gösterildiği gibi abone olun:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    Merhaba, Notification.m içinde değişiklik *storeCategoriesAndSubscribe* hello yerel ayar parametresi ekleme ve hello kullanıcı varsayılan ayarlarında depolayarak yöntemi:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    Merhaba değiştirme *abone* yöntemi tooinclude hello yerel ayar:
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    Nasıl hello yöntemi şimdi kullanıyoruz Not *registerTemplateWithDeviceToken*, yerine *registerNativeWithDeviceToken*. Biz için bir şablon kaydederken (uygulamamıza tooregister farklı şablonlar isteyebilirsiniz gibi) size tooprovide hello json şablonunu ve ayrıca hello şablon için bir ad sahiptir. Bu haberler için toomake emin tooreceive hello notifciations istiyoruz, kategori etiketleri olarak emin tooregister kılın.
   
    Bir yöntem tooretrieve hello yerel hello kullanıcı varsayılan ayarlardan ekleyin:
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Biz bizim bildirimleri sınıfı değiştirilmiş, toomake bizim ViewController kullandığına emin sahibiz hello Kullan yeni UISegmentControl. Merhaba satırında aşağıdaki hello eklemek *viewDidLoad* şu anda seçili olan yöntemi toomake emin tooshow hello yerel ayar:
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    Ardından, *abone* yöntemi çağrısı toohello değiştirme *storeCategoriesAndSubscribe* toohello aşağıdaki:
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. Son olarak, tooupdate hello olması *didRegisterForRemoteNotificationsWithDeviceToken* , AppDelegate.m yönteminde böylece uygulamanız başladığında kaydınızı doğru yenileyebilirsiniz. Çağrı toohello değiştirme *abone* hello aşağıdaki bildirimlerle yöntemi:
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(isteğe bağlı) .NET konsol uygulamasından yerelleştirilmiş şablon bildirimleri gönderin.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(isteğe bağlı) Merhaba aygıttan yerelleştirilmiş şablon bildirimleri gönderme
Erişim tooVisual Studio sahip veya toojust sınama hello aygıtta hello uygulamasından doğrudan yerelleştirilmiş hello şablon bildirim göndermek istediğiniz yok olur.  Basit yapabilecekleriniz yerelleştirilmiş hello şablon parametreleri toohello ekleme `SendNotificationRESTAPI` hello önceki öğreticide tanımladığınız yöntemi.

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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

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




## <a name="next-steps"></a>Sonraki Adımlar
Şablonları kullanma hakkında daha fazla bilgi için bkz:

* [Notification Hubs ile kullanıcılara bildirin: ASP.NET]
* [Notification Hubs ile kullanıcılara bildirin: Mobil hizmetler]

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[son dakika haberleri Notification Hubs kullanma toosend]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs ile kullanıcılara bildirin: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notification Hubs ile kullanıcılara bildirin: Mobil hizmetler]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
