---
title: ".NET arka ucu ile iOS için Notification Hubs kullanıcılara bildirme aaaAzure"
description: "Nasıl toosend anında iletme bildirimleri toousers Azure'da öğrenin. Objective-C ve hello .NET API hello arka uç için yazılan kod örnekleri."
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
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="8c98d-104">Azure Notification Hubs .NET arka ucu ile iOS için Kullanıcılara Bildirme</span><span class="sxs-lookup"><span data-stu-id="8c98d-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="8c98d-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8c98d-105">Overview</span></span>
<span data-ttu-id="8c98d-106">Azure'da anında iletme bildirimi destek tooaccess kullanımı kolay, multiplatform ve Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir ölçeklendirilmiş gönderim altyapısı sağlar Platform.</span><span class="sxs-lookup"><span data-stu-id="8c98d-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="8c98d-107">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında iletme bildirimleri tooa belirli uygulama kullanıcısı belirli bir cihazda gösterir.</span><span class="sxs-lookup"><span data-stu-id="8c98d-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="8c98d-108">Bir ASP.NET Webapı arka kullanılan tooauthenticate istemcileri ve toogenerate bildirimleri hello Kılavuzu konusundaki gösterildiği gibidir [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="8c98d-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="8c98d-109">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8c98d-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="8c98d-110">Bu öğretici aynı zamanda hello önkoşul toohello olan [güvenli itme (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8c98d-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="8c98d-111">Merhaba toouse Mobile Apps arka uç hizmetinizin istiyorsanız bkz [Mobile Apps ile çalışmaya başlama itme](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="8c98d-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="8c98d-112">İOS uygulamanızı değiştirme</span><span class="sxs-lookup"><span data-stu-id="8c98d-112">Modify your iOS app</span></span>
1. <span data-ttu-id="8c98d-113">Açık hello hello oluşturduğunuz uygulamayı görüntüle tek sayfa [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8c98d-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8c98d-114">Bu bölümde, projenizin bir boş kuruluş adı ile yapılandırıldığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="8c98d-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="8c98d-115">Aksi durumda, kuruluş adını tooall sınıf adları tooprepend gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c98d-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="8c98d-116">Main.storyboard hello nesne kitaplığından hello ekran görüntüsü gösterildiği hello bileşenleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c98d-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="8c98d-117">**Kullanıcı adı**: A UITextField yer tutucu metinle *kullanıcı adı girin*, hemen hello sonuçları etiketi ve sol kısıtlanmış toohello göndermek ve sağ kenar boşlukları ve sonuçları etiketi altında hello Gönder.</span><span class="sxs-lookup"><span data-stu-id="8c98d-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="8c98d-118">**Parola**: A UITextField yer tutucu metinle *parolasını girin*, hemen beneath hello kullanıcı adı metin alanı ve kısıtlı toohello sol ve sağ kenar boşlukları ve hello username metin alanı altında.</span><span class="sxs-lookup"><span data-stu-id="8c98d-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="8c98d-119">Merhaba denetleyin **güvenli metin girişi** hello özniteliği denetçisi altında seçeneği *dönüş anahtar*.</span><span class="sxs-lookup"><span data-stu-id="8c98d-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="8c98d-120">**Oturum açma**: A UIButton hemen hello parola metin alanı altında etiketli ve hello işaretini **etkin** hello öznitelikleri denetçisi altında seçeneği *denetimi içeriğini*</span><span class="sxs-lookup"><span data-stu-id="8c98d-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="8c98d-121">**WNS**: Etiket ve anahtar tooenable gönderme hello hub'ındaki Kurulum yüklediyse bildirim Windows bildirim hizmeti hello.</span><span class="sxs-lookup"><span data-stu-id="8c98d-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="8c98d-122">Merhaba bkz [Windows başlarken](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8c98d-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="8c98d-123">**GCM**: Etiket ve anahtar tooenable gönderme hello hub'ındaki Kurulum yüklediyse bildirim tooGoogle Cloud Messaging hello.</span><span class="sxs-lookup"><span data-stu-id="8c98d-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="8c98d-124">Bkz: [Android Başlarken](notification-hubs-android-push-notification-google-gcm-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8c98d-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="8c98d-125">**APNS**: Etiket ve anahtar tooenable gönderme hello bildirim toohello Apple Platform bildirim hizmeti.</span><span class="sxs-lookup"><span data-stu-id="8c98d-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="8c98d-126">**Recipent kullanıcıadı**: A UITextField yer tutucu metinle *alıcı kullanıcı adı etiketi*, hemen GCM hello etiket ve kısıtlı toohello sol ve sağ kenar boşlukları ve GCM hello etiket.</span><span class="sxs-lookup"><span data-stu-id="8c98d-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="8c98d-127">Bazı bileşenler hello eklenen [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8c98d-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="8c98d-128">**CTRL** hello görünüm tooViewController.h hello bileşenlerden sürükleyin ve bu yeni çıkışlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c98d-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="8c98d-129">ViewController.h içinde hello aşağıdakileri ekleyin `#define` içeri aktarma deyimlerini hemen altında.</span><span class="sxs-lookup"><span data-stu-id="8c98d-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="8c98d-130">Yedek hello *< girin bilgisayarınızı arka uç nokta\>*  yer tutucusunu hello hedef kullandığınız toodeploy, uygulamanızın arka ucuna hello önceki bölümde URL ile.</span><span class="sxs-lookup"><span data-stu-id="8c98d-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="8c98d-131">Örneğin, *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="8c98d-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="8c98d-132">Projenizde, yeni bir oluşturma **Cocoa Touch sınıfı** adlı **RegisterClient** toointerface hello oluşturduğunuz ASP.NET uç ile.</span><span class="sxs-lookup"><span data-stu-id="8c98d-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="8c98d-133">İçinden devralma hello sınıfı oluşturmak `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="8c98d-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="8c98d-134">Ardından hello hello RegisterClient.h kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c98d-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="8c98d-135">Merhaba RegisterClient.m hello güncelleştirme `@interface` bölümü:</span><span class="sxs-lookup"><span data-stu-id="8c98d-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
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
5. <span data-ttu-id="8c98d-136">Hello yerine `@implementation` hello RegisterClient.m koddan hello ile bölümünde.</span><span class="sxs-lookup"><span data-stu-id="8c98d-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

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

    <span data-ttu-id="8c98d-137">Yukarıdaki Hello kod hello Kılavuzu makalesinde açıklandığı hello mantığı uygular [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) NSURLSession kullanarak tooperform REST tooyour uygulama arka ucu ve NSUserDefaults toolocally deposu hello çağırır Merhaba bildirim hub'ı tarafından döndürülen RegistrationId.</span><span class="sxs-lookup"><span data-stu-id="8c98d-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="8c98d-138">Bu sınıf, özelliğinin gerektirdiğini Not **authorizationHeader** toobe sipariş toowork düzgün ayarlanmadı.</span><span class="sxs-lookup"><span data-stu-id="8c98d-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="8c98d-139">Bu özellik tarafından hello ayarlanır **ViewController** hello oturum açtıktan sonra sınıfı.</span><span class="sxs-lookup"><span data-stu-id="8c98d-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="8c98d-140">ViewController.h içinde eklemek bir `#import` RegisterClient.h bildirimi.</span><span class="sxs-lookup"><span data-stu-id="8c98d-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="8c98d-141">Ardından hello cihaz belirteci için bir bildirim eklemek ve tooa başvuru `RegisterClient` hello örneğinde `@interface` bölümü:</span><span class="sxs-lookup"><span data-stu-id="8c98d-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="8c98d-142">Merhaba özel yöntem bildiriminde ViewController.m içinde eklemek `@interface` bölümü:</span><span class="sxs-lookup"><span data-stu-id="8c98d-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="8c98d-143">Merhaba aşağıdaki kod parçacığında güvenli kimlik doğrulama düzeni, hello hello uygulaması yerine kullanmalısınız **createAndSetAuthenticationHeaderWithUsername:AndPassword:** , özel kimlik doğrulama mekanizması ile Merhaba kaydı istemci sınıfı tarafından örneğin OAuth, Active Directory kullanılan bir kimlik doğrulama belirteci toobe oluşturan.</span><span class="sxs-lookup"><span data-stu-id="8c98d-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="8c98d-144">Merhaba sonra `@implementation` ViewController.m bölümünü hello uygulama ayarı, hello cihaz belirteci ve kimlik doğrulama üstbilgisi ekleyen koddan hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8c98d-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="8c98d-145">Ayar hello cihaz belirteci hello Oturum Aç düğmesini nasıl sağladığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8c98d-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="8c98d-146">Merhaba uygulama arka ucu ile anında iletme bildirimleri için hello görünüm denetleyicisini hello oturum açma eylemin bir parçası olarak kaydeder olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="8c98d-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="8c98d-147">Merhaba cihaz belirteci düzgün şekilde ayarlanmış kadar bu nedenle, oturum eylem toobe erişilebilir istiyoruz değil.</span><span class="sxs-lookup"><span data-stu-id="8c98d-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="8c98d-148">Merhaba eski hello ikinci önce gerçekleşir sürece hello günlüğünden içinde hello anında iletme kayıt ayırırsınız.</span><span class="sxs-lookup"><span data-stu-id="8c98d-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="8c98d-149">Parçacıkları tooimplement hello eylem yöntemi için aşağıdaki hello ViewController.m içinde kullanmak, **oturum** düğmesi ve yöntemi toosend hello bildirim iletisini kullanarak bir ASP.NET arka hello.</span><span class="sxs-lookup"><span data-stu-id="8c98d-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="8c98d-150">(IBAction) LogInAction: (ID) gönderen {/ / kimlik doğrulama üst bilgisi oluşturun ve kayıt istemci NSString * kullanıcı ayarlayın self =. UsernameField.text;   NSString * parola self =. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="8c98d-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="8c98d-151">[kendini createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="8c98d-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="8c98d-152">__weak ViewController * selfie kendini; =   [self.registerClient registerWithDeviceToken:self.deviceToken etiketler: nil andCompletion:^(NSError* error) {varsa (! hatası) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered başarıyla!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="8c98d-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="8c98d-153">-(void) SendNotificationASPNETBackend: (NSString*) pns UsernameTag: (NSString*) usernameTag ileti: (NSString*) ileti {NSURLSession* oturum = [NSURLSession sessionWithConfiguration: [NSURLSessionConfiguration defaultSessionConfiguration] temsilci: nil delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="8c98d-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="8c98d-154">Merhaba pns ve kullanıcı adı etiketi hello REST URL'sini toohello ASP.NET arka uç NSURL * requestURL ile parametre olarak geçirmek = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="8c98d-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="8c98d-155">NSMutableURLRequest * isteği [NSMutableURLRequest requestWithURL:requestURL] =;    [setHTTPMethod:@"POST istek"];</span><span class="sxs-lookup"><span data-stu-id="8c98d-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="8c98d-156">Merhaba sahte authenticationheader hello kayıt istemciden NSString * authorizationHeaderValue alma = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization istek"];</span><span class="sxs-lookup"><span data-stu-id="8c98d-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="8c98d-157">Merhaba bildirim ileti gövdesi ekleme [setValue:@"application/json;charset=utf-8 istek" forHTTPHeaderField:@"Content-Type"];    [setHTTPBody istek: [ileti dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="8c98d-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="8c98d-158">Merhaba gönderme bildirim REST API hello ASP.NET arka uç NSURLSessionDataTask * dataTask üzerinde yürütme [oturum dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *= hata) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) yanıt;        varsa (hata || httpResponse.statusCode! = 200) {NSString* Durum = [% NSString stringWithFormat:@"Error durum @: % d\nError: %@\n", pns, httpResponse.statusCode, hata];            dispatch_async(dispatch_get_main_queue(), ^ {/ / tüm 3 PNS çağrıları bilgi tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status] sahip olabileceği için metin Ekle];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="8c98d-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="8c98d-159">}];    [dataTask Sürdür]; }</span><span class="sxs-lookup"><span data-stu-id="8c98d-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="8c98d-160">Merhaba eylemin hello için güncelleştirme **bildirim gönder** düğmesini toouse hello ASP.NET arka ve tooany bir anahtar tarafından etkin PNS gönderin.</span><span class="sxs-lookup"><span data-stu-id="8c98d-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="8c98d-161">İşlevde **ViewDidLoad**tooinstantiate hello RegisterClient örneği aşağıdaki hello ekleyin ve metin alanları için hello temsilci ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8c98d-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="8c98d-162">Artık **AppDelegate.m**, tüm hello içeriği hello yönteminin Kaldır **uygulama: didRegisterForPushNotificationWithDeviceToken:** ve görünüm hello toomake emin aşağıdaki hello ile değiştirin Denetleyici hello APNs alınan son cihaz belirteci içerir:</span><span class="sxs-lookup"><span data-stu-id="8c98d-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="8c98d-163">Son olarak, **AppDelegate.m**, yöntem aşağıdaki hello olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="8c98d-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="8c98d-164">Test hello uygulama</span><span class="sxs-lookup"><span data-stu-id="8c98d-164">Test hello Application</span></span>
1. <span data-ttu-id="8c98d-165">Xcode'da, fiziksel bir iOS cihazında (anında iletme bildirimleri hello benzeticisinde çalışmaz) hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8c98d-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="8c98d-166">Merhaba iOS uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="8c98d-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="8c98d-167">Bunlar herhangi bir dize olabilir, ancak her ikisi de hello olması gerekir aynı dize değeri.</span><span class="sxs-lookup"><span data-stu-id="8c98d-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="8c98d-168">Ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="8c98d-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="8c98d-169">Kayıt başarılı size bildiren bir açılır pencere görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8c98d-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="8c98d-170">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8c98d-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="8c98d-171">Merhaba, **alıcı kullanıcı adı etiketi* metin alanında, başka bir aygıt hello kaydından ile kullanılan hello kullanıcı adı etiketi girin.</span><span class="sxs-lookup"><span data-stu-id="8c98d-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="8c98d-172">Bir bildirim iletisi girin ve tıklayın **bildirim gönder**.</span><span class="sxs-lookup"><span data-stu-id="8c98d-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="8c98d-173">Merhaba alıcı kullanıcı adı etiketi ile kayıt olan hello aygıtların hello bildirim iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8c98d-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="8c98d-174">Ayrıca, toothose kullanıcılar yalnızca gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8c98d-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
