---
title: "aaaAzure güvenli hub bildirim gönderme"
description: "Nasıl toosend güvenli anında iletme bildirimleri tooan iOS uygulaması Azure'dan öğrenin. Objective-C ve C# içinde yazılan kod örnekleri."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure Notification Hubs güvenli bildirme
> [!div class="op_single_selector"]
> * [Windows Evrensel](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Microsoft Azure anında iletme bildirimi desteği tooaccess Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir bir kullanımı kolay, çok platformlu, ölçeği gönderim altyapısı sağlar Platform.

Tooregulatory veya güvenlik kısıtlamaları, bazen bir uygulama bir şey hello standart anında iletme bildirimi altyapısı iletilen hello bildirim tooinclude isteyebilirsiniz. Bu öğretici nasıl tooachieve hello aynı deneyimi hello istemci aygıt hello uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı üzerinden hassas bilgileri göndererek açıklar.

Yüksek bir düzeyde hello akışı aşağıdaki gibidir:

1. Merhaba uygulama arka ucu:
   * Arka uç veritabanı güvenli yükünde depolar.
   * Merhaba (güvenli hiçbir bilgi gönderilmez) Bu bildirim toohello aygıtın Kimliğini gönderir.
2. Merhaba cihaza hello bildirim alırken Hello uygulamanın:
   * Merhaba cihaz hello arka uç isteyen hello güvenli yükü bağlanır.
   * Merhaba uygulama hello yükü hello aygıt bildirim olarak gösterebilir.

Merhaba kullanıcı oturum açtığında sonra akışı önceki hello (ve Bu öğreticide), biz hello aygıt varsayın toonote kimlik doğrulama belirtecini yerel depolama biriminde, depolar. önemlidir. Merhaba aygıt hello bildirim'ın güvenli yükü bu belirteci kullanarak alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır. Uygulamanızın kimlik doğrulama belirteçleri hello aygıtta depolamaz veya bu belirteçleri süresi, hello hello bildirim alma sırasında cihaz uygulaması hello kullanıcı toolaunch hello uygulama isteyen genel bir bildirim görüntülemelidir. Merhaba uygulama hello kullanıcının kimliğini doğrular ve hello bildirim yükü gösterir.

Bu güvenli itme öğreticide gösterilmiştir nasıl toosend bir anında iletme bildirimi güvenli bir şekilde. Merhaba öğretici derlemeler üzerinde hello [kullanıcılara bildirme](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) önce bu öğreticide hello adımlar tamamlanmalıdır şekilde öğretici.

> [!NOTE]
> Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Merhaba iOS projesi değiştirme
Uygulama arka uç toosend yalnızca hello değiştiren göre *kimliği* ilişkin bir bildirim, bildirim ve geri arama, arka uç tooretrieve hello görüntülenen ileti toobe güvenli, iOS uygulama toohandle toochange sahip.

tooachieve bu hedef uygulama arka ucu hello toowrite hello mantığı tooretrieve hello güvenli içerikten sunuyoruz.

1. İçinde **AppDelegate.m**, hello bildirim kimliği hello arka ucundan gönderilen işler sessiz bildirimleri için emin hello uygulama kaydeder olmak. Merhaba eklemek **UIRemoteNotificationTypeNewsstandContentAvailability** didFinishLaunchingWithOptions seçeneği:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. İçinde **AppDelegate.m** bir uygulama bölümü hello üstünde bildiriminin hello ile ekleyin:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. Merhaba uygulama bölümü hello koddan, hello yer tutucu değiştirerek eklemek `{back-end endpoint}` hello uç noktası için daha önce edindiğiniz, arka uç ile:

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. Şimdi biz toohandle hello gelen bildirim sahip ve tooretrieve hello içerik toodisplay yukarıda hello yöntemini kullanın. İlk olarak, tooenable iOS app toorun hello arka planda bir anında iletme bildirimi alırken sahibiz. İçinde **XCode**, uygulama projenizi hello Sol paneldeki seçin ve ardından Merhaba, ana uygulamanın hedef tıklayın **hedefleri** hello merkezi bölmesinden bölümü.
2. Ardından, **yetenekleri** sekmesinde merkezi bölmesinde hello üstünde ve hello denetleyin **uzak bildirimler** onay kutusu.
   
    ![][IOS1]
3. İçinde **AppDelegate.m** yöntemi toohandle anında iletme bildirimleri aşağıdaki hello ekleyin:
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    Tercih toohandle hello örneklerini eksik kimlik doğrulama üstbilgisi özelliği ya da reddetme hello arka uç tarafından olduğuna dikkat edin. Bu durumlarda belirli işleme Hello çoğunlukla, hedef kullanıcı deneyimi bağlıdır. Toodisplay hello kullanıcı tooauthenticate tooretrieve hello gerçek bildirimi için genel bir istem içeren bir bildirim bir seçenektir.

## <a name="run-hello-application"></a>Merhaba uygulama çalıştırın
toorun Merhaba uygulama, aşağıdaki hello:

1. Xcode'da, fiziksel bir iOS cihazında (anında iletme bildirimleri hello benzeticisinde çalışmaz) hello uygulamayı çalıştırın.
2. Merhaba iOS uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin. Bunlar herhangi bir dize olabilir, ancak bunlar olmalıdır hello aynı değeri.
3. Merhaba iOS uygulama kullanıcı Arabirimi, tıklatın **oturum**. Ardından **Gönder itme**. Bildirim Merkezinize görüntülenmesini hello güvenli bildirim görmeniz gerekir.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
