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
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>ASP.NET kullanarak anında iletme bildirimleri için Hello geçerli kullanıcı kaydı
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Bu konu nasıl toorequest anında iletme bildirimi kaydı Azure Notification Hubs ile kayıt ASP.NET Web API tarafından gerçekleştirildiğinde gösterir. Bu konuda hello öğretici genişletir [Notification Hubs kullanıcılara bildirme]. Bu öğretici toocreate kimliği doğrulanmış hello mobil hizmet hello gerekli adımları önceden tamamlamış olmalıdır. Kullanıcıların senaryo bildir hello hakkında daha fazla bilgi için bkz: [Notification Hubs kullanıcılara bildirme].

## <a name="update-your-app"></a>Uygulamanızı güncelleştirme
1. MainStoryboard_iPhone.storyboard içinde bileşenleri hello nesne kitaplığından aşağıdaki hello ekleyin:
   
   * **Etiket**: "Push Notification Hubs ile tooUser"
   * **Etiket**: "InstallationId"
   * **Etiket**: "Kullanıcı"
   * **Metin alanı**: "Kullanıcı"
   * **Etiket**: "Parola"
   * **Metin alanı**: "Parola"
   * **Düğme**: "Oturum Aç"
     
     Bu noktada, şeridinizin hello aşağıdaki gibi görünür:
     
      ![][0]
2. Hello Yardımcısı düzenleyicisinde çıkışlar tüm anahtarlı hello denetimler için oluşturma ve bunları çağrısı, hello metin alanları hello View Controller (temsilci) ile bağlanmak ve oluşturma bir **eylem** hello için **oturum açma** düğmesi.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Adlı bir sınıf oluşturun **Deviceınfo**, ve kopyalama hello aşağıdaki kodu DeviceInfo.h hello dosyasının arabirimi bölüme hello:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Merhaba DeviceInfo.m dosyasının hello uygulama bölümünde koddan hello kopyalayın:
   
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
5. PushToUserAppDelegate.h içinde özellik singleton aşağıdaki hello ekleyin:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. Merhaba, **didFinishLaunchingWithOptions** PushToUserAppDelegate.m, yönteminde hello aşağıdaki kodu ekleyin:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    Merhaba ilk satırı başlatır hello **Deviceınfo** singleton. Merhaba, zaten ikinci satır başlatır hello kayıt anında iletme bildirimleri için hello zaten tamamladığınızdan değil [Notification Hubs ile çalışmaya başlama] Öğreticisi.
7. Merhaba yöntemi PushToUserAppDelegate.m içinde uygulaması **didRegisterForRemoteNotificationsWithDeviceToken** AppDelegate içinde ve hello aşağıdaki kodu ekleyin:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    Merhaba cihaz belirteci hello istek için ayarlar.
   
   > [!NOTE]
   > Bu noktada, olmamalıdır başka bir kodu bu yöntem. Çağrı toohello zaten varsa **registerNativeWithDeviceToken** hello tamamlandığında eklediğiniz yöntemi [Notification Hubs ile çalışmaya başlama](/manage/services/notification-hubs/get-started-notification-hubs-ios/) eğitmen, yorum genişletme veya, kaldırmanız gerekir çağırın.
   > 
   > 
8. Merhaba PushToUserAppDelegate.m dosyasında işleyici yöntemi aşağıdaki hello ekleyin:
   
   * (void) uygulama:(UIApplication *) uygulama didReceiveRemoteNotification:(NSDictionary *) kullanıcı bilgisi {NSLog (@"% @", kullanıcı bilgisi);   UIAlertView * uyarı = [[UIAlertView ayırma] initWithTitle:@"Notification" iletisi: [kullanıcı bilgisi objectForKey:@"inAppMessage"] temsilci: nil cancelButtonTitle: @"Tamam" otherButtonTitles:nil, nil];   [uyarı göster]; }
   
   Uygulamanızı çalışırken bildirimi aldığında bu yöntem hello UI bir uyarı görüntüler.
9. Merhaba PushToUserViewController.m dosya ve dönüş hello klavye uygulama aşağıdaki hello açın:
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. Merhaba, **viewDidLoad** Initialize hello InstallationID etiket gibi hello PushToUserViewController.m dosyasında yöntemi:
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Aşağıdaki özelliklere PushToUserViewController.m arabiriminde hello ekleyin:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. Ardından, uygulama aşağıdaki hello ekleyin:
    
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
13. Kopya hello aşağıdaki kod hello **oturum açma** XCode tarafından oluşturulan işleyici yöntemi:
    
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
    
    Bu yöntem anında iletme bildirimleri için bir yükleme kimliği ve kanal alır ve bunu hello cihaz türü ile birlikte gönderir, Notification Hubs ' bir kayıt oluşturur Web API yöntemi toohello kimlik doğrulaması. Bu Web API tanımlanan [Notification Hubs kullanıcılara bildirme].

Merhaba istemci uygulaması güncelleştirildi, toohello dönmek [Notification Hubs kullanıcılara bildirme] ve bildirim hub'ları kullanarak hello mobil hizmet toosend bildirimleri güncelleştirin.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[Notification Hubs kullanıcılara bildirme]: /manage/services/notification-hubs/notify-users-aspnet

[Notification Hubs ile çalışmaya başlama]: /manage/services/notification-hubs/get-started-notification-hubs-ios
