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
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="e15f1-103">Bildirim hub'ları yerelleştirilmiş toosend son dakika haberleri tooiOS aygıtları'nı kullanın</span><span class="sxs-lookup"><span data-stu-id="e15f1-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e15f1-104">Windows mağazası C#</span><span class="sxs-lookup"><span data-stu-id="e15f1-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="e15f1-105">iOS</span><span class="sxs-lookup"><span data-stu-id="e15f1-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e15f1-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e15f1-106">Overview</span></span>
<span data-ttu-id="e15f1-107">Bu konu, nasıl gösterir toouse hello [şablonları](notification-hubs-templates-cross-platform-push-messages.md) dil ve cihaz tarafından yerelleştirilmiş haberi bildirimleri çiğnemekten Azure Notification Hubs toobroadcast özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="e15f1-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="e15f1-108">Bu öğreticide oluşturduğunuz hello iOS uygulaması ile başlamanız [son dakika haberleri Notification Hubs kullanma toosend].</span><span class="sxs-lookup"><span data-stu-id="e15f1-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="e15f1-109">Tamamlandığında, ilgilendiğiniz kategorileri için mümkün tooregister olacaktır, hangi tooreceive hello bildirimleri bir dil belirtin ve yalnızca anında iletme bildirimlerini seçili hello kategorileri için o dilde alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e15f1-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="e15f1-110">İki bölümden toothis senaryo vardır:</span><span class="sxs-lookup"><span data-stu-id="e15f1-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="e15f1-111">iOS uygulamanızın istemci cihazları toospecify bir dil ve haber kategorileri çiğnemekten toosubscribe toodifferent olanak tanır;</span><span class="sxs-lookup"><span data-stu-id="e15f1-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="e15f1-112">Merhaba arka uç yayınlar hello kullanarak hello bildirimleri **etiketi** ve **şablonu** Azure bildirim hub'larını feautres.</span><span class="sxs-lookup"><span data-stu-id="e15f1-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e15f1-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e15f1-113">Prerequisites</span></span>
<span data-ttu-id="e15f1-114">Önceden hello tamamlamış olmalıdır [son dakika haberleri Notification Hubs kullanma toosend] öğretici ve bu öğreticinin bu kodu doğrudan derlemeler için kullanılabilir, hello koduna sahip.</span><span class="sxs-lookup"><span data-stu-id="e15f1-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="e15f1-115">Visual Studio 2012 veya sonraki sürümünü isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e15f1-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="e15f1-116">Şablon kavramları</span><span class="sxs-lookup"><span data-stu-id="e15f1-116">Template concepts</span></span>
<span data-ttu-id="e15f1-117">İçinde [son dakika haberleri Notification Hubs kullanma toosend] kullanılan bir uygulama yerleşik **etiketleri** toosubscribe toonotifications farklı haber kategorileri için.</span><span class="sxs-lookup"><span data-stu-id="e15f1-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="e15f1-118">Birçok uygulama, ancak, birden çok pazarda hedef ve yerelleştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e15f1-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="e15f1-119">Bunun anlamı hello bildirimleri kendilerini Merhaba içeriğine sahip yerelleştirilmiş toobe ve teslim toohello cihaz kümesini düzeltin.</span><span class="sxs-lookup"><span data-stu-id="e15f1-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="e15f1-120">Bu konudaki göstereceğiz nasıl toouse hello **şablonu** özellik bildirim hub'larını tooeasily teslim yerelleştirilmiş son dakika haberi bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="e15f1-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="e15f1-121">Not: tek yönlü toosend yerelleştirilmiş bildirimleri toocreate her etiket birden çok sürümünün olduğu.</span><span class="sxs-lookup"><span data-stu-id="e15f1-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="e15f1-122">Örneğin, toosupport İngilizce, Fransızca ve Mandarin, üç farklı etiketler world haberler için ihtiyacımız: "world_en", "world_fr" ve "world_ch".</span><span class="sxs-lookup"><span data-stu-id="e15f1-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="e15f1-123">Toosend sonra hello world haber tooeach bu etiketlerin yerelleştirilmiş bir sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="e15f1-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="e15f1-124">Bu konudaki şablonları tooavoid hello artışı etiketleri ve birden fazla ileti gönderme hello gereksinimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e15f1-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="e15f1-125">Yüksek bir düzeyde bir şekilde toospecify şablonlarıdır nasıl belirli bir aygıt bir bildirim almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e15f1-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="e15f1-126">Merhaba şablon, uygulama arka ucu tarafından gönderilen Merhaba ileti parçası olan tooproperties bakarak hello tam yük biçimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="e15f1-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="e15f1-127">Örneğimizde, biz tüm desteklenen diller içeren bir yerel ayar belirsiz ileti gönderir:</span><span class="sxs-lookup"><span data-stu-id="e15f1-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="e15f1-128">Ardından cihazlarını toohello doğru özellik başvuran bir şablonla kaydetmek sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="e15f1-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="e15f1-129">Örneğin, Fransızca haberler için tooregister istediği bir iOS uygulaması hello aşağıdaki kaydeder:</span><span class="sxs-lookup"><span data-stu-id="e15f1-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="e15f1-130">Şablonlar, daha fazla bilgi bulabilir hakkında içinde çok güçlü bir özellik olan bizim [şablonları](notification-hubs-templates-cross-platform-push-messages.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e15f1-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="e15f1-131">Merhaba uygulama kullanıcı arabirimi</span><span class="sxs-lookup"><span data-stu-id="e15f1-131">hello app user interface</span></span>
<span data-ttu-id="e15f1-132">Biz şimdi hello konuda oluşturulan hello çiğnemekten haber uygulama değiştirecek [son dakika haberleri Notification Hubs kullanma toosend] toosend yerelleştirilmiş şablonları kullanarak son dakika haberleri.</span><span class="sxs-lookup"><span data-stu-id="e15f1-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="e15f1-133">MainStoryboard_iPhone.storyboard, biz destekleyecek hello üç dilleri ile bölümlenmiş bir denetim ekleyin: İngilizce, Fransızca ve Mandarin.</span><span class="sxs-lookup"><span data-stu-id="e15f1-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="e15f1-134">Ardından emin tooadd bir IBOutlet, ViewController.h aşağıda gösterildiği gibi yapın:</span><span class="sxs-lookup"><span data-stu-id="e15f1-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="e15f1-135">Yapı hello iOS uygulaması</span><span class="sxs-lookup"><span data-stu-id="e15f1-135">Building hello iOS app</span></span>
1. <span data-ttu-id="e15f1-136">Merhaba, Notification.h eklemek *retrieveLocale* yöntemi, hello deposu değiştirmek ve yöntemleri aşağıda gösterildiği gibi abone olun:</span><span class="sxs-lookup"><span data-stu-id="e15f1-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="e15f1-137">Merhaba, Notification.m içinde değişiklik *storeCategoriesAndSubscribe* hello yerel ayar parametresi ekleme ve hello kullanıcı varsayılan ayarlarında depolayarak yöntemi:</span><span class="sxs-lookup"><span data-stu-id="e15f1-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="e15f1-138">Merhaba değiştirme *abone* yöntemi tooinclude hello yerel ayar:</span><span class="sxs-lookup"><span data-stu-id="e15f1-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
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
   
    <span data-ttu-id="e15f1-139">Nasıl hello yöntemi şimdi kullanıyoruz Not *registerTemplateWithDeviceToken*, yerine *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="e15f1-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="e15f1-140">Biz için bir şablon kaydederken (uygulamamıza tooregister farklı şablonlar isteyebilirsiniz gibi) size tooprovide hello json şablonunu ve ayrıca hello şablon için bir ad sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e15f1-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="e15f1-141">Bu haberler için toomake emin tooreceive hello notifciations istiyoruz, kategori etiketleri olarak emin tooregister kılın.</span><span class="sxs-lookup"><span data-stu-id="e15f1-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="e15f1-142">Bir yöntem tooretrieve hello yerel hello kullanıcı varsayılan ayarlardan ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e15f1-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="e15f1-143">Biz bizim bildirimleri sınıfı değiştirilmiş, toomake bizim ViewController kullandığına emin sahibiz hello Kullan yeni UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="e15f1-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="e15f1-144">Merhaba satırında aşağıdaki hello eklemek *viewDidLoad* şu anda seçili olan yöntemi toomake emin tooshow hello yerel ayar:</span><span class="sxs-lookup"><span data-stu-id="e15f1-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="e15f1-145">Ardından, *abone* yöntemi çağrısı toohello değiştirme *storeCategoriesAndSubscribe* toohello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e15f1-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
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
3. <span data-ttu-id="e15f1-146">Son olarak, tooupdate hello olması *didRegisterForRemoteNotificationsWithDeviceToken* , AppDelegate.m yönteminde böylece uygulamanız başladığında kaydınızı doğru yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e15f1-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="e15f1-147">Çağrı toohello değiştirme *abone* hello aşağıdaki bildirimlerle yöntemi:</span><span class="sxs-lookup"><span data-stu-id="e15f1-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="e15f1-148">(isteğe bağlı) .NET konsol uygulamasından yerelleştirilmiş şablon bildirimleri gönderin.</span><span class="sxs-lookup"><span data-stu-id="e15f1-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="e15f1-149">(isteğe bağlı) Merhaba aygıttan yerelleştirilmiş şablon bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="e15f1-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="e15f1-150">Erişim tooVisual Studio sahip veya toojust sınama hello aygıtta hello uygulamasından doğrudan yerelleştirilmiş hello şablon bildirim göndermek istediğiniz yok olur.</span><span class="sxs-lookup"><span data-stu-id="e15f1-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="e15f1-151">Basit yapabilecekleriniz yerelleştirilmiş hello şablon parametreleri toohello ekleme `SendNotificationRESTAPI` hello önceki öğreticide tanımladığınız yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e15f1-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="e15f1-152">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e15f1-152">Next Steps</span></span>
<span data-ttu-id="e15f1-153">Şablonları kullanma hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="e15f1-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="e15f1-154">[Notification Hubs ile kullanıcılara bildirin: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="e15f1-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="e15f1-155">[Notification Hubs ile kullanıcılara bildirin: Mobil hizmetler]</span><span class="sxs-lookup"><span data-stu-id="e15f1-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

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
