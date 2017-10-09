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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Azure Notification Hubs .NET arka ucu ile iOS için Kullanıcılara Bildirme
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Genel Bakış
Azure'da anında iletme bildirimi destek tooaccess kullanımı kolay, multiplatform ve Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir ölçeklendirilmiş gönderim altyapısı sağlar Platform. Bu öğretici nasıl toouse Azure Notification Hubs toosend anında iletme bildirimleri tooa belirli uygulama kullanıcısı belirli bir cihazda gösterir. Bir ASP.NET Webapı arka kullanılan tooauthenticate istemcileri ve toogenerate bildirimleri hello Kılavuzu konusundaki gösterildiği gibidir [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md). Bu öğretici aynı zamanda hello önkoşul toohello olan [güvenli itme (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) Öğreticisi.
> Merhaba toouse Mobile Apps arka uç hizmetinizin istiyorsanız bkz [Mobile Apps ile çalışmaya başlama itme](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>İOS uygulamanızı değiştirme
1. Açık hello hello oluşturduğunuz uygulamayı görüntüle tek sayfa [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md) Öğreticisi.
   
   > [!NOTE]
   > Bu bölümde, projenizin bir boş kuruluş adı ile yapılandırıldığını varsayar. Aksi durumda, kuruluş adını tooall sınıf adları tooprepend gerekir.
   > 
   > 
2. Main.storyboard hello nesne kitaplığından hello ekran görüntüsü gösterildiği hello bileşenleri ekleyin.
   
    ![][1]
   
   * **Kullanıcı adı**: A UITextField yer tutucu metinle *kullanıcı adı girin*, hemen hello sonuçları etiketi ve sol kısıtlanmış toohello göndermek ve sağ kenar boşlukları ve sonuçları etiketi altında hello Gönder.
   * **Parola**: A UITextField yer tutucu metinle *parolasını girin*, hemen beneath hello kullanıcı adı metin alanı ve kısıtlı toohello sol ve sağ kenar boşlukları ve hello username metin alanı altında. Merhaba denetleyin **güvenli metin girişi** hello özniteliği denetçisi altında seçeneği *dönüş anahtar*.
   * **Oturum açma**: A UIButton hemen hello parola metin alanı altında etiketli ve hello işaretini **etkin** hello öznitelikleri denetçisi altında seçeneği *denetimi içeriğini*
   * **WNS**: Etiket ve anahtar tooenable gönderme hello hub'ındaki Kurulum yüklediyse bildirim Windows bildirim hizmeti hello. Merhaba bkz [Windows başlarken](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Öğreticisi.
   * **GCM**: Etiket ve anahtar tooenable gönderme hello hub'ındaki Kurulum yüklediyse bildirim tooGoogle Cloud Messaging hello. Bkz: [Android Başlarken](notification-hubs-android-push-notification-google-gcm-get-started.md) Öğreticisi.
   * **APNS**: Etiket ve anahtar tooenable gönderme hello bildirim toohello Apple Platform bildirim hizmeti.
   * **Recipent kullanıcıadı**: A UITextField yer tutucu metinle *alıcı kullanıcı adı etiketi*, hemen GCM hello etiket ve kısıtlı toohello sol ve sağ kenar boşlukları ve GCM hello etiket.

    Bazı bileşenler hello eklenen [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md) Öğreticisi.

1. **CTRL** hello görünüm tooViewController.h hello bileşenlerden sürükleyin ve bu yeni çıkışlar ekleyin.
   
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
2. ViewController.h içinde hello aşağıdakileri ekleyin `#define` içeri aktarma deyimlerini hemen altında. Yedek hello *< girin bilgisayarınızı arka uç nokta\>*  yer tutucusunu hello hedef kullandığınız toodeploy, uygulamanızın arka ucuna hello önceki bölümde URL ile. Örneğin, *http://you_backend.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. Projenizde, yeni bir oluşturma **Cocoa Touch sınıfı** adlı **RegisterClient** toointerface hello oluşturduğunuz ASP.NET uç ile. İçinden devralma hello sınıfı oluşturmak `NSObject`. Ardından hello hello RegisterClient.h kodu ekleyin.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. Merhaba RegisterClient.m hello güncelleştirme `@interface` bölümü:
   
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
5. Hello yerine `@implementation` hello RegisterClient.m koddan hello ile bölümünde.

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

    Yukarıdaki Hello kod hello Kılavuzu makalesinde açıklandığı hello mantığı uygular [uygulama arka ucunuzdan kaydetme](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) NSURLSession kullanarak tooperform REST tooyour uygulama arka ucu ve NSUserDefaults toolocally deposu hello çağırır Merhaba bildirim hub'ı tarafından döndürülen RegistrationId.

    Bu sınıf, özelliğinin gerektirdiğini Not **authorizationHeader** toobe sipariş toowork düzgün ayarlanmadı. Bu özellik tarafından hello ayarlanır **ViewController** hello oturum açtıktan sonra sınıfı.

1. ViewController.h içinde eklemek bir `#import` RegisterClient.h bildirimi. Ardından hello cihaz belirteci için bir bildirim eklemek ve tooa başvuru `RegisterClient` hello örneğinde `@interface` bölümü:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. Merhaba özel yöntem bildiriminde ViewController.m içinde eklemek `@interface` bölümü:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Merhaba aşağıdaki kod parçacığında güvenli kimlik doğrulama düzeni, hello hello uygulaması yerine kullanmalısınız **createAndSetAuthenticationHeaderWithUsername:AndPassword:** , özel kimlik doğrulama mekanizması ile Merhaba kaydı istemci sınıfı tarafından örneğin OAuth, Active Directory kullanılan bir kimlik doğrulama belirteci toobe oluşturan.
> 
> 

1. Merhaba sonra `@implementation` ViewController.m bölümünü hello uygulama ayarı, hello cihaz belirteci ve kimlik doğrulama üstbilgisi ekleyen koddan hello ekleyin.
   
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
   
    Ayar hello cihaz belirteci hello Oturum Aç düğmesini nasıl sağladığını unutmayın. Merhaba uygulama arka ucu ile anında iletme bildirimleri için hello görünüm denetleyicisini hello oturum açma eylemin bir parçası olarak kaydeder olmasıdır. Merhaba cihaz belirteci düzgün şekilde ayarlanmış kadar bu nedenle, oturum eylem toobe erişilebilir istiyoruz değil. Merhaba eski hello ikinci önce gerçekleşir sürece hello günlüğünden içinde hello anında iletme kayıt ayırırsınız.
2. Parçacıkları tooimplement hello eylem yöntemi için aşağıdaki hello ViewController.m içinde kullanmak, **oturum** düğmesi ve yöntemi toosend hello bildirim iletisini kullanarak bir ASP.NET arka hello.
   
       - (IBAction) LogInAction: (ID) gönderen {/ / kimlik doğrulama üst bilgisi oluşturun ve kayıt istemci NSString * kullanıcı ayarlayın self =. UsernameField.text;   NSString * parola self =. PasswordField.text;
   
           [kendini createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie kendini; =   [self.registerClient registerWithDeviceToken:self.deviceToken etiketler: nil andCompletion:^(NSError* error) {varsa (! hatası) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered başarıyla!"];});}}];}

        -(void) SendNotificationASPNETBackend: (NSString*) pns UsernameTag: (NSString*) usernameTag ileti: (NSString*) ileti {NSURLSession* oturum = [NSURLSession sessionWithConfiguration: [NSURLSessionConfiguration defaultSessionConfiguration] temsilci: nil delegateQueue:nil];

            Merhaba pns ve kullanıcı adı etiketi hello REST URL'sini toohello ASP.NET arka uç NSURL * requestURL ile parametre olarak geçirmek = [NSURL URLWithString: [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];

            NSMutableURLRequest * isteği [NSMutableURLRequest requestWithURL:requestURL] =;    [setHTTPMethod:@"POST istek"];

            Merhaba sahte authenticationheader hello kayıt istemciden NSString * authorizationHeaderValue alma = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization istek"];

            Merhaba bildirim ileti gövdesi ekleme [setValue:@"application/json;charset=utf-8 istek" forHTTPHeaderField:@"Content-Type"];    [setHTTPBody istek: [ileti dataUsingEncoding:NSUTF8StringEncoding]];

            Merhaba gönderme bildirim REST API hello ASP.NET arka uç NSURLSessionDataTask * dataTask üzerinde yürütme [oturum dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *= hata) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) yanıt;        varsa (hata || httpResponse.statusCode! = 200) {NSString* Durum = [% NSString stringWithFormat:@"Error durum @: % d\nError: %@\n", pns, httpResponse.statusCode, hata];            dispatch_async(dispatch_get_main_queue(), ^ {/ / tüm 3 PNS çağrıları bilgi tooview [self.sendResults setText:[self.sendResults.text stringByAppendingString:status] sahip olabileceği için metin Ekle];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask Sürdür]; }


1. Merhaba eylemin hello için güncelleştirme **bildirim gönder** düğmesini toouse hello ASP.NET arka ve tooany bir anahtar tarafından etkin PNS gönderin.

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



1. İşlevde **ViewDidLoad**tooinstantiate hello RegisterClient örneği aşağıdaki hello ekleyin ve metin alanları için hello temsilci ayarlayın.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. Artık **AppDelegate.m**, tüm hello içeriği hello yönteminin Kaldır **uygulama: didRegisterForPushNotificationWithDeviceToken:** ve görünüm hello toomake emin aşağıdaki hello ile değiştirin Denetleyici hello APNs alınan son cihaz belirteci içerir:
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Son olarak, **AppDelegate.m**, yöntem aşağıdaki hello olduğundan emin olun:
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Test hello uygulama
1. Xcode'da, fiziksel bir iOS cihazında (anında iletme bildirimleri hello benzeticisinde çalışmaz) hello uygulamayı çalıştırın.
2. Merhaba iOS uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin. Bunlar herhangi bir dize olabilir, ancak her ikisi de hello olması gerekir aynı dize değeri. Ardından **oturum**.
   
    ![][2]
3. Kayıt başarılı size bildiren bir açılır pencere görmeniz gerekir. **Tamam** düğmesine tıklayın.
   
    ![][3]
4. Merhaba, **alıcı kullanıcı adı etiketi* metin alanında, başka bir aygıt hello kaydından ile kullanılan hello kullanıcı adı etiketi girin.
5. Bir bildirim iletisi girin ve tıklayın **bildirim gönder**.  Merhaba alıcı kullanıcı adı etiketi ile kayıt olan hello aygıtların hello bildirim iletisi alırsınız.  Ayrıca, toothose kullanıcılar yalnızca gönderilir.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
