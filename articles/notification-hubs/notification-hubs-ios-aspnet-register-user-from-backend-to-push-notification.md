---
title: "aaaRegister hello geçerli kullanıcı için Web API kullanarak anında iletme bildirimleri | Microsoft Docs"
description: "Nasıl toorequest anında iletme bildirimi kaydı Azure Notification Hubs ile iOS uygulamasında kayda ASP.NET Web API tarafından gerçekleştirildiğinde öğrenin."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="51a4f-103">ASP.NET kullanarak anında iletme bildirimleri için Hello geçerli kullanıcı kaydı</span><span class="sxs-lookup"><span data-stu-id="51a4f-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="51a4f-104">iOS</span><span class="sxs-lookup"><span data-stu-id="51a4f-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="51a4f-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="51a4f-105">Overview</span></span>
<span data-ttu-id="51a4f-106">Bu konu nasıl toorequest anında iletme bildirimi kaydı Azure Notification Hubs ile kayıt ASP.NET Web API tarafından gerçekleştirildiğinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="51a4f-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="51a4f-107">Bu konuda hello öğretici genişletir [Notification Hubs kullanıcılara bildirme].</span><span class="sxs-lookup"><span data-stu-id="51a4f-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="51a4f-108">Bu öğretici toocreate kimliği doğrulanmış hello mobil hizmet hello gerekli adımları önceden tamamlamış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51a4f-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="51a4f-109">Kullanıcıların senaryo bildir hello hakkında daha fazla bilgi için bkz: [Notification Hubs kullanıcılara bildirme].</span><span class="sxs-lookup"><span data-stu-id="51a4f-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="51a4f-110">Uygulamanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="51a4f-110">Update your app</span></span>
1. <span data-ttu-id="51a4f-111">MainStoryboard_iPhone.storyboard içinde bileşenleri hello nesne kitaplığından aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="51a4f-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="51a4f-112">**Etiket**: "Push Notification Hubs ile tooUser"</span><span class="sxs-lookup"><span data-stu-id="51a4f-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="51a4f-113">**Etiket**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="51a4f-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="51a4f-114">**Etiket**: "Kullanıcı"</span><span class="sxs-lookup"><span data-stu-id="51a4f-114">**Label**: "User"</span></span>
   * <span data-ttu-id="51a4f-115">**Metin alanı**: "Kullanıcı"</span><span class="sxs-lookup"><span data-stu-id="51a4f-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="51a4f-116">**Etiket**: "Parola"</span><span class="sxs-lookup"><span data-stu-id="51a4f-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="51a4f-117">**Metin alanı**: "Parola"</span><span class="sxs-lookup"><span data-stu-id="51a4f-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="51a4f-118">**Düğme**: "Oturum Aç"</span><span class="sxs-lookup"><span data-stu-id="51a4f-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="51a4f-119">Bu noktada, şeridinizin hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="51a4f-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="51a4f-120">Hello Yardımcısı düzenleyicisinde çıkışlar tüm anahtarlı hello denetimler için oluşturma ve bunları çağrısı, hello metin alanları hello View Controller (temsilci) ile bağlanmak ve oluşturma bir **eylem** hello için **oturum açma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="51a4f-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="51a4f-121">Adlı bir sınıf oluşturun **Deviceınfo**, ve kopyalama hello aşağıdaki kodu DeviceInfo.h hello dosyasının arabirimi bölüme hello:</span><span class="sxs-lookup"><span data-stu-id="51a4f-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="51a4f-122">Merhaba DeviceInfo.m dosyasının hello uygulama bölümünde koddan hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="51a4f-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="51a4f-123">PushToUserAppDelegate.h içinde özellik singleton aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="51a4f-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="51a4f-124">Merhaba, **didFinishLaunchingWithOptions** PushToUserAppDelegate.m, yönteminde hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="51a4f-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="51a4f-125">Merhaba ilk satırı başlatır hello **Deviceınfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="51a4f-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="51a4f-126">Merhaba, zaten ikinci satır başlatır hello kayıt anında iletme bildirimleri için hello zaten tamamladığınızdan değil [Notification Hubs ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="51a4f-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="51a4f-127">Merhaba yöntemi PushToUserAppDelegate.m içinde uygulaması **didRegisterForRemoteNotificationsWithDeviceToken** AppDelegate içinde ve hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="51a4f-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="51a4f-128">Merhaba cihaz belirteci hello istek için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="51a4f-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="51a4f-129">Bu noktada, olmamalıdır başka bir kodu bu yöntem.</span><span class="sxs-lookup"><span data-stu-id="51a4f-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="51a4f-130">Çağrı toohello zaten varsa **registerNativeWithDeviceToken** hello tamamlandığında eklediğiniz yöntemi [Notification Hubs ile çalışmaya başlama](/manage/services/notification-hubs/get-started-notification-hubs-ios/) eğitmen, yorum genişletme veya, kaldırmanız gerekir çağırın.</span><span class="sxs-lookup"><span data-stu-id="51a4f-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="51a4f-131">Merhaba PushToUserAppDelegate.m dosyasında işleyici yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="51a4f-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="51a4f-132">(void) uygulama:(UIApplication *) uygulama didReceiveRemoteNotification:(NSDictionary *) kullanıcı bilgisi {NSLog (@"% @", kullanıcı bilgisi);   UIAlertView * uyarı = [[UIAlertView ayırma] initWithTitle:@"Notification" iletisi: [kullanıcı bilgisi objectForKey:@"inAppMessage"] temsilci: nil cancelButtonTitle: @"Tamam" otherButtonTitles:nil, nil];   [uyarı göster]; }</span><span class="sxs-lookup"><span data-stu-id="51a4f-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="51a4f-133">Uygulamanızı çalışırken bildirimi aldığında bu yöntem hello UI bir uyarı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="51a4f-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="51a4f-134">Merhaba PushToUserViewController.m dosya ve dönüş hello klavye uygulama aşağıdaki hello açın:</span><span class="sxs-lookup"><span data-stu-id="51a4f-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="51a4f-135">Merhaba, **viewDidLoad** Initialize hello InstallationID etiket gibi hello PushToUserViewController.m dosyasında yöntemi:</span><span class="sxs-lookup"><span data-stu-id="51a4f-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="51a4f-136">Aşağıdaki özelliklere PushToUserViewController.m arabiriminde hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="51a4f-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="51a4f-137">Ardından, uygulama aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="51a4f-137">Then, add hello following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="51a4f-138">Kopya hello aşağıdaki kod hello **oturum açma** XCode tarafından oluşturulan işleyici yöntemi:</span><span class="sxs-lookup"><span data-stu-id="51a4f-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="51a4f-139">Bu yöntem anında iletme bildirimleri için bir yükleme kimliği ve kanal alır ve bunu hello cihaz türü ile birlikte gönderir, Notification Hubs ' bir kayıt oluşturur Web API yöntemi toohello kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="51a4f-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="51a4f-140">Bu Web API tanımlanan [Notification Hubs kullanıcılara bildirme].</span><span class="sxs-lookup"><span data-stu-id="51a4f-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="51a4f-141">Merhaba istemci uygulaması güncelleştirildi, toohello dönmek [Notification Hubs kullanıcılara bildirme] ve bildirim hub'ları kullanarak hello mobil hizmet toosend bildirimleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="51a4f-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[Notification Hubs kullanıcılara bildirme]: /manage/services/notification-hubs/notify-users-aspnet

[Notification Hubs ile çalışmaya başlama]: /manage/services/notification-hubs/get-started-notification-hubs-ios
