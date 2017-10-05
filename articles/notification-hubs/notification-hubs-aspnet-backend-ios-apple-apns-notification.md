---
title: "Azure Notification Hubs .NET arka ucu ile iOS için Kullanıcılara Bildirme"
description: "Azure kullanıcılara anında iletme bildirimleri göndermek öğrenin. Objective-C ve .NET API arka uç için yazılan kod örnekleri."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="97cee-104">Azure Notification Hubs .NET arka ucu ile iOS için Kullanıcılara Bildirme</span><span class="sxs-lookup"><span data-stu-id="97cee-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="97cee-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="97cee-105">Overview</span></span>
<span data-ttu-id="97cee-106">Azure'da anında iletme bildirimi desteği, kullanımı kolay, multiplatform ve mobil platformlar için tüketici ve kurumsal uygulama için anında iletme bildirimleri uyarlamasını büyük ölçüde basitleştirir ölçeklendirilmiş gönderim altyapısı erişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="97cee-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="97cee-107">Bu öğreticide, belirli bir cihazdaki belirli bir uygulama kullanıcısına anında iletme bildirimleri göndermek için Azure Bildirim Hub'larını nasıl kullanacağınız gösterilir.</span><span class="sxs-lookup"><span data-stu-id="97cee-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="97cee-108">Bir ASP.NET Webapı arka istemcilerin kimliğini doğrulamak ve bildirimleri oluşturmak için Kılavuzu konusundaki gösterildiği gibi kullanılır [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="97cee-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="97cee-109">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="97cee-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="97cee-110">Bu öğreticinin ayrıca için ön koşuldur [güvenli itme (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="97cee-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="97cee-111">Mobile Apps arka uç hizmetinizin kullanmak istiyorsanız, bkz: [Mobile Apps ile çalışmaya başlama itme](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="97cee-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="97cee-112">İOS uygulamanızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="97cee-112">Modify your iOS app</span></span>
1. <span data-ttu-id="97cee-113">Oluşturduğunuz tek sayfa görünümü uygulamasını açın [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="97cee-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="97cee-114">Bu bölümde, projenizin bir boş kuruluş adı ile yapılandırıldığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="97cee-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="97cee-115">Aksi durumda, tüm sınıf adları için kuruluşunuzun adı başına gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="97cee-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="97cee-116">Main.storyboard nesne kitaplığından ekran görüntüsünde gösterilen bileşenleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97cee-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="97cee-117">**Kullanıcı adı**: A UITextField yer tutucu metinle *kullanıcı adı girin*hemen sonuçları etiket ve sol ve sağ kenar boşlukları kısıtlı Gönder altındaki ve gönderme sonuçları etiketinin altına.</span><span class="sxs-lookup"><span data-stu-id="97cee-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="97cee-118">**Parola**: A UITextField yer tutucu metinle *parolasını girin*, kullanıcı adı hemen altındaki metin alan ve sağ ve sol kenar boşluklarına ve kullanıcı adı metin alanı altında kısıtlanmış.</span><span class="sxs-lookup"><span data-stu-id="97cee-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="97cee-119">Denetleme **güvenli metin girişi** özniteliği Denetçisi'nde altında seçeneği *dönüş anahtar*.</span><span class="sxs-lookup"><span data-stu-id="97cee-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="97cee-120">**Oturum açma**: A UIButton hemen parola metin alanı etiketli ve işaretini **etkin** öznitelikleri Denetçisi'nde altında seçeneği *denetimi içeriğini*</span><span class="sxs-lookup"><span data-stu-id="97cee-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="97cee-121">**WNS**: Etiket ve anahtarı Windows bildirim hizmeti bildirim hub'ında Kurulum yüklediyse gönderilmesine izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="97cee-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="97cee-122">Bkz: [Windows başlarken](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="97cee-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="97cee-123">**GCM**: Etiket ve anahtarı Google bulut Mesajlaşma için bildirim hub'ında Kurulum yüklediyse gönderilmesine izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="97cee-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="97cee-124">Bkz: [Android Başlarken](notification-hubs-android-push-notification-google-gcm-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="97cee-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="97cee-125">**APNS**: Etiket ve anahtar için Apple Platform bildirim hizmet bildirimi gönderilmesine izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="97cee-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="97cee-126">**Recipent kullanıcıadı**: A UITextField yer tutucu metinle *alıcı kullanıcı adı etiketi*, hemen GCM etiket ve sağ ve sol kenar boşluklarına ve GCM etiketinin altına kısıtlı.</span><span class="sxs-lookup"><span data-stu-id="97cee-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="97cee-127">Bazı bileşenler eklenmiştir [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="97cee-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="97cee-128">**CTRL** görünümünde bileşenlerinden ViewController.h için sürükleyin ve bu yeni çıkışlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97cee-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="97cee-129">ViewController.h içinde aşağıdaki ekleme `#define` içeri aktarma deyimlerini hemen altında.</span><span class="sxs-lookup"><span data-stu-id="97cee-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="97cee-130">Yedek *< girin bilgisayarınızı arka uç nokta\>*  yer tutucusunu, uygulamanızın arka ucuna önceki bölümdeki dağıtmak için kullanılan hedef URL ile.</span><span class="sxs-lookup"><span data-stu-id="97cee-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="97cee-131">Örneğin, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="97cee-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="97cee-132">Projenizde, yeni bir oluşturma **Cocoa Touch sınıfı** adlı **RegisterClient** oluşturduğunuz ASP.NET arka uç ile arabirim oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="97cee-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="97cee-133">İçinden devralma sınıfı oluşturmak `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="97cee-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="97cee-134">Ardından aşağıdaki kodu RegisterClient.h ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97cee-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="97cee-135">RegisterClient.m Güncelleştirmesi'nde `@interface` bölümü:</span><span class="sxs-lookup"><span data-stu-id="97cee-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. <span data-ttu-id="97cee-136">Değiştir `@implementation` aşağıdaki kodla RegisterClient.m bölümünde.</span><span class="sxs-lookup"><span data-stu-id="97cee-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    <span data-ttu-id="97cee-137">Yukarıdaki kod Kılavuzu makalesinde açıklanan mantığını uygular [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) NSURLSession kullanarak REST gerçekleştirmek için uygulamanızın arka ucuna çağırır ve RegistrationId yerel olarak depolamak için NSUserDefaults bildirim hub'ı döndürdü.</span><span class="sxs-lookup"><span data-stu-id="97cee-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="97cee-138">Bu sınıf, özelliğinin gerektirdiğini Not **authorizationHeader** düzgün çalışması için ayarlanacak.</span><span class="sxs-lookup"><span data-stu-id="97cee-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="97cee-139">Bu özelliği ayarlamak **ViewController** günlüğünde sonra sınıfı.</span><span class="sxs-lookup"><span data-stu-id="97cee-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="97cee-140">ViewController.h içinde eklemek bir `#import` RegisterClient.h bildirimi.</span><span class="sxs-lookup"><span data-stu-id="97cee-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="97cee-141">Daha sonra cihaz belirteci için bir bildirim ekler ve başvuru bir `RegisterClient` örneğini `@interface` bölümü:</span><span class="sxs-lookup"><span data-stu-id="97cee-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="97cee-142">Bir özel yöntem bildiriminde ViewController.m içinde eklemek `@interface` bölümü:</span><span class="sxs-lookup"><span data-stu-id="97cee-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="97cee-143">Aşağıdaki kod parçacığında güvenli kimlik doğrulama düzeni değil, uygulaması yerine kullanmalısınız **createAndSetAuthenticationHeaderWithUsername:AndPassword:** kaydı istemci sınıfı tarafından örneğin OAuth, Active Directory kullanılması için bir kimlik doğrulama belirteci oluşturur, özel kimlik doğrulama mekanizması ile.</span><span class="sxs-lookup"><span data-stu-id="97cee-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="97cee-144">Ardından `@implementation` ViewController.m bölümünü cihaz belirteci ve kimlik doğrulama üstbilgisi ayarlamak için uygulama ekleyen aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97cee-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    <span data-ttu-id="97cee-145">Cihaz belirteci ayarı Oturum Aç düğmesini nasıl sağladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="97cee-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="97cee-146">Uygulama arka ucu ile anında iletme bildirimleri için Görünüm denetleyicisini oturum açma eylemin bir parçası olarak kaydettirir olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="97cee-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="97cee-147">Bu nedenle, biz cihaz belirteci düzgün şekilde ayarlanmış kadar erişilebilir olmasını oturum eylem istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="97cee-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="97cee-148">Eski ikinci önce gerçekleşir sürece iletme kaydı içinde günlüğünden ayırırsınız.</span><span class="sxs-lookup"><span data-stu-id="97cee-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="97cee-149">Eylem yöntemi için uygulamak için aşağıdaki kod parçacıkları ViewController.m içinde kullanmak, **oturum** düğmesi ve ASP.NET arka ucu kullanarak bildirim iletisini göndermek için bir yöntem.</span><span class="sxs-lookup"><span data-stu-id="97cee-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="97cee-150">(IBAction) LogInAction: (ID) gönderen {/ / kimlik doğrulama üst bilgisi oluşturun ve kayıt istemci NSString * kullanıcı ayarlayın self =. UsernameField.text;   NSString * parola self =. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="97cee-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="97cee-151">[kendini createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="97cee-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="97cee-152">__weak ViewController * selfie kendini; =   [self.registerClient registerWithDeviceToken:self.deviceToken etiketler: nil andCompletion:^(NSError* error) {varsa (! hatası) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered başarıyla!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="97cee-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="97cee-153">-(void) SendNotificationASPNETBackend: (NSString*) pns UsernameTag: (NSString*) usernameTag ileti: (NSString*) ileti {NSURLSession* oturum = [NSURLSession sessionWithConfiguration: [NSURLSessionConfiguration defaultSessionConfiguration] temsilci: nil delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="97cee-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="97cee-154">Pns ve kullanıcı adı etiketi için ASP.NET arka uç NSURL * requestURL REST URL ile parametre olarak geçirmek = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="97cee-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="97cee-155">NSMutableURLRequest * isteği [NSMutableURLRequest requestWithURL:requestURL] =;    [setHTTPMethod:@"POST istek"];</span><span class="sxs-lookup"><span data-stu-id="97cee-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="97cee-156">Sahte authenticationheader kayıt istemciden NSString * authorizationHeaderValue alma = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization istek"];</span><span class="sxs-lookup"><span data-stu-id="97cee-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="97cee-157">Bildirim ileti gövdesi ekleme [setValue:@"application/json;charset=utf-8 istek" forHTTPHeaderField:@"Content-Type"];    [setHTTPBody istek: [ileti dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="97cee-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="97cee-158">REST API gönderme bildirim ASP.NET arka uç NSURLSessionDataTask * dataTask üzerinde yürütme = [oturum dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) yanıt;        varsa (hata || httpResponse.statusCode! = 200) {NSString* Durum = [% NSString stringWithFormat:@"Error durum @: % d\nError: %@\n", pns, httpResponse.statusCode, hata];            dispatch_async(dispatch_get_main_queue(), ^ {/ / tüm 3 PNS çağrıları bilgileri [self.sendResults setText:[self.sendResults.text stringByAppendingString:status] görünümüne sahip olabileceği için metin Ekle];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="97cee-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="97cee-159">}];    [dataTask Sürdür]; }</span><span class="sxs-lookup"><span data-stu-id="97cee-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="97cee-160">Eylem için güncelleştirme **bildirim gönder** düğmesine ASP.NET arka kullanın ve bir anahtar tarafından etkin PNS gönderin.</span><span class="sxs-lookup"><span data-stu-id="97cee-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. <span data-ttu-id="97cee-161">İşlevde **ViewDidLoad**, RegisterClient örneği oluşturmak için aşağıdaki örneği ve metin alanları için temsilci Ayarla ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97cee-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="97cee-162">Artık **AppDelegate.m**, yönteminin tüm içeriğini kaldırın **uygulama: didRegisterForPushNotificationWithDeviceToken:** ve görünüm denetleyicisini APNs alınan son cihaz belirteci içerdiğinden emin olmak için aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="97cee-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="97cee-163">Son olarak, **AppDelegate.m**, aşağıdaki yöntemi olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="97cee-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="97cee-164">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="97cee-164">Test the Application</span></span>
1. <span data-ttu-id="97cee-165">Xcode'da, uygulamayı fiziksel bir iOS cihazında (anında iletme bildirimleri benzeticisinde çalışmaz) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="97cee-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="97cee-166">İOS uygulaması UI'da, bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="97cee-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="97cee-167">Bunlar herhangi bir dize olabilir, ancak her ikisi de aynı dize değeri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="97cee-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="97cee-168">Ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="97cee-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="97cee-169">Kayıt başarılı size bildiren bir açılır pencere görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="97cee-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="97cee-170">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97cee-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="97cee-171">İçinde **alıcı kullanıcı adı etiketi* metin alanında, başka bir cihaz kaydından ile kullanılan kullanıcı adı etiketi girin.</span><span class="sxs-lookup"><span data-stu-id="97cee-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="97cee-172">Bir bildirim iletisi girin ve tıklayın **bildirim gönder**.</span><span class="sxs-lookup"><span data-stu-id="97cee-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="97cee-173">Alıcı kullanıcı adı etiketi ile kayıt olan cihazları bildirim iletisini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="97cee-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="97cee-174">Ayrıca, bu kullanıcılara yalnızca gönderilir.</span><span class="sxs-lookup"><span data-stu-id="97cee-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
