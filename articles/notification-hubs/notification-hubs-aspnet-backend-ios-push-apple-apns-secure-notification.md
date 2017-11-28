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
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="2552e-104">Azure Notification Hubs güvenli bildirme</span><span class="sxs-lookup"><span data-stu-id="2552e-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2552e-105">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="2552e-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="2552e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="2552e-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="2552e-107">Android</span><span class="sxs-lookup"><span data-stu-id="2552e-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="2552e-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2552e-108">Overview</span></span>
<span data-ttu-id="2552e-109">Microsoft Azure anında iletme bildirimi desteği tooaccess Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir bir kullanımı kolay, çok platformlu, ölçeği gönderim altyapısı sağlar Platform.</span><span class="sxs-lookup"><span data-stu-id="2552e-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="2552e-110">Tooregulatory veya güvenlik kısıtlamaları, bazen bir uygulama bir şey hello standart anında iletme bildirimi altyapısı iletilen hello bildirim tooinclude isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2552e-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="2552e-111">Bu öğretici nasıl tooachieve hello aynı deneyimi hello istemci aygıt hello uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı üzerinden hassas bilgileri göndererek açıklar.</span><span class="sxs-lookup"><span data-stu-id="2552e-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="2552e-112">Yüksek bir düzeyde hello akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="2552e-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="2552e-113">Merhaba uygulama arka ucu:</span><span class="sxs-lookup"><span data-stu-id="2552e-113">hello app back-end:</span></span>
   * <span data-ttu-id="2552e-114">Arka uç veritabanı güvenli yükünde depolar.</span><span class="sxs-lookup"><span data-stu-id="2552e-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="2552e-115">Merhaba (güvenli hiçbir bilgi gönderilmez) Bu bildirim toohello aygıtın Kimliğini gönderir.</span><span class="sxs-lookup"><span data-stu-id="2552e-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="2552e-116">Merhaba cihaza hello bildirim alırken Hello uygulamanın:</span><span class="sxs-lookup"><span data-stu-id="2552e-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="2552e-117">Merhaba cihaz hello arka uç isteyen hello güvenli yükü bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2552e-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="2552e-118">Merhaba uygulama hello yükü hello aygıt bildirim olarak gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="2552e-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="2552e-119">Merhaba kullanıcı oturum açtığında sonra akışı önceki hello (ve Bu öğreticide), biz hello aygıt varsayın toonote kimlik doğrulama belirtecini yerel depolama biriminde, depolar. önemlidir.</span><span class="sxs-lookup"><span data-stu-id="2552e-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="2552e-120">Merhaba aygıt hello bildirim'ın güvenli yükü bu belirteci kullanarak alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="2552e-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="2552e-121">Uygulamanızın kimlik doğrulama belirteçleri hello aygıtta depolamaz veya bu belirteçleri süresi, hello hello bildirim alma sırasında cihaz uygulaması hello kullanıcı toolaunch hello uygulama isteyen genel bir bildirim görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="2552e-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="2552e-122">Merhaba uygulama hello kullanıcının kimliğini doğrular ve hello bildirim yükü gösterir.</span><span class="sxs-lookup"><span data-stu-id="2552e-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="2552e-123">Bu güvenli itme öğreticide gösterilmiştir nasıl toosend bir anında iletme bildirimi güvenli bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="2552e-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="2552e-124">Merhaba öğretici derlemeler üzerinde hello [kullanıcılara bildirme](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) önce bu öğreticide hello adımlar tamamlanmalıdır şekilde öğretici.</span><span class="sxs-lookup"><span data-stu-id="2552e-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="2552e-125">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2552e-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="2552e-126">Merhaba iOS projesi değiştirme</span><span class="sxs-lookup"><span data-stu-id="2552e-126">Modify hello iOS project</span></span>
<span data-ttu-id="2552e-127">Uygulama arka uç toosend yalnızca hello değiştiren göre *kimliği* ilişkin bir bildirim, bildirim ve geri arama, arka uç tooretrieve hello görüntülenen ileti toobe güvenli, iOS uygulama toohandle toochange sahip.</span><span class="sxs-lookup"><span data-stu-id="2552e-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="2552e-128">tooachieve bu hedef uygulama arka ucu hello toowrite hello mantığı tooretrieve hello güvenli içerikten sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="2552e-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="2552e-129">İçinde **AppDelegate.m**, hello bildirim kimliği hello arka ucundan gönderilen işler sessiz bildirimleri için emin hello uygulama kaydeder olmak.</span><span class="sxs-lookup"><span data-stu-id="2552e-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="2552e-130">Merhaba eklemek **UIRemoteNotificationTypeNewsstandContentAvailability** didFinishLaunchingWithOptions seçeneği:</span><span class="sxs-lookup"><span data-stu-id="2552e-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="2552e-131">İçinde **AppDelegate.m** bir uygulama bölümü hello üstünde bildiriminin hello ile ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2552e-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="2552e-132">Merhaba uygulama bölümü hello koddan, hello yer tutucu değiştirerek eklemek `{back-end endpoint}` hello uç noktası için daha önce edindiğiniz, arka uç ile:</span><span class="sxs-lookup"><span data-stu-id="2552e-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

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

1. <span data-ttu-id="2552e-133">Şimdi biz toohandle hello gelen bildirim sahip ve tooretrieve hello içerik toodisplay yukarıda hello yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2552e-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="2552e-134">İlk olarak, tooenable iOS app toorun hello arka planda bir anında iletme bildirimi alırken sahibiz.</span><span class="sxs-lookup"><span data-stu-id="2552e-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="2552e-135">İçinde **XCode**, uygulama projenizi hello Sol paneldeki seçin ve ardından Merhaba, ana uygulamanın hedef tıklayın **hedefleri** hello merkezi bölmesinden bölümü.</span><span class="sxs-lookup"><span data-stu-id="2552e-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="2552e-136">Ardından, **yetenekleri** sekmesinde merkezi bölmesinde hello üstünde ve hello denetleyin **uzak bildirimler** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="2552e-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="2552e-137">İçinde **AppDelegate.m** yöntemi toohandle anında iletme bildirimleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2552e-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
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
   
    <span data-ttu-id="2552e-138">Tercih toohandle hello örneklerini eksik kimlik doğrulama üstbilgisi özelliği ya da reddetme hello arka uç tarafından olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="2552e-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="2552e-139">Bu durumlarda belirli işleme Hello çoğunlukla, hedef kullanıcı deneyimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2552e-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="2552e-140">Toodisplay hello kullanıcı tooauthenticate tooretrieve hello gerçek bildirimi için genel bir istem içeren bir bildirim bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="2552e-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="2552e-141">Merhaba uygulama çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2552e-141">Run hello Application</span></span>
<span data-ttu-id="2552e-142">toorun Merhaba uygulama, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="2552e-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="2552e-143">Xcode'da, fiziksel bir iOS cihazında (anında iletme bildirimleri hello benzeticisinde çalışmaz) hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2552e-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="2552e-144">Merhaba iOS uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="2552e-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="2552e-145">Bunlar herhangi bir dize olabilir, ancak bunlar olmalıdır hello aynı değeri.</span><span class="sxs-lookup"><span data-stu-id="2552e-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="2552e-146">Merhaba iOS uygulama kullanıcı Arabirimi, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="2552e-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="2552e-147">Ardından **Gönder itme**.</span><span class="sxs-lookup"><span data-stu-id="2552e-147">Then click **Send push**.</span></span> <span data-ttu-id="2552e-148">Bildirim Merkezinize görüntülenmesini hello güvenli bildirim görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2552e-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
