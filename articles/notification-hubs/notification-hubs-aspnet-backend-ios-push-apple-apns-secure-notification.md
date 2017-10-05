---
title: "Azure Notification Hubs güvenli bildirme"
description: "Azure'dan bir iOS uygulamasının güvenli anında iletme bildirimleri göndermek öğrenin. Objective-C ve C# içinde yazılan kod örnekleri."
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
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="b32df-104">Azure Notification Hubs güvenli bildirme</span><span class="sxs-lookup"><span data-stu-id="b32df-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b32df-105">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="b32df-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="b32df-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b32df-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="b32df-107">Android</span><span class="sxs-lookup"><span data-stu-id="b32df-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="b32df-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b32df-108">Overview</span></span>
<span data-ttu-id="b32df-109">Microsoft Azure anında iletme bildirimi desteği, mobil platformlar için tüketici ve kurumsal uygulama için anında iletme bildirimleri uyarlamasını büyük ölçüde basitleştirir bir kullanımı kolay, çok platformlu, ölçeği gönderim altyapısı erişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b32df-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="b32df-110">Yasal nedeniyle veya güvenlik kısıtlamaları, bazen bir uygulama bir şey standart anında iletme bildirimi altyapısı iletilen bildirimi dahil olmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b32df-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="b32df-111">Bu öğretici, hassas bilgileri istemci cihaz ve uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı aracılığıyla göndererek aynı deneyimi elde etmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="b32df-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="b32df-112">Yüksek bir düzeyde akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="b32df-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="b32df-113">Uygulama arka ucu:</span><span class="sxs-lookup"><span data-stu-id="b32df-113">The app back-end:</span></span>
   * <span data-ttu-id="b32df-114">Arka uç veritabanı güvenli yükünde depolar.</span><span class="sxs-lookup"><span data-stu-id="b32df-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="b32df-115">Bu bildirim Kimliğini (güvenli hiçbir bilgi gönderilmez) cihaza gönderir.</span><span class="sxs-lookup"><span data-stu-id="b32df-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="b32df-116">Bildirim alırken cihaza uygulamanın:</span><span class="sxs-lookup"><span data-stu-id="b32df-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="b32df-117">Cihaz güvenli yükü isteyen arka uç bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="b32df-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="b32df-118">Uygulama yükü cihaz bildirim olarak gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="b32df-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="b32df-119">Önceki akış (ve Bu öğreticide), kullanıcı oturum açtığında sonra cihaz kimlik doğrulama belirtecini yerel depoda sakladığı varsayıyoruz olduğunu dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b32df-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="b32df-120">Cihaz Bu belirteci kullanarak bildirim 's güvenli yükü alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="b32df-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="b32df-121">Uygulamanızın kimlik doğrulama belirteçleri cihazda depolamaz veya bu belirteçleri süresi, bildirim alma sırasında cihaz uygulaması uygulamayı başlatmak için kullanıcıdan genel bir bildirim görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="b32df-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="b32df-122">Uygulama kullanıcının kimliğini doğrular ve bildirim yükü gösterir.</span><span class="sxs-lookup"><span data-stu-id="b32df-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="b32df-123">Bu güvenli itme öğretici güvenli bir şekilde bir anında iletme bildirimi göndermek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="b32df-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="b32df-124">Öğretici derlemeler [kullanıcılara bildirme](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) önce bu öğreticide adımları tamamlanmalıdır şekilde öğretici.</span><span class="sxs-lookup"><span data-stu-id="b32df-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="b32df-125">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (iOS) ile çalışmaya başlama](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b32df-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="b32df-126">İOS projesine değiştirme</span><span class="sxs-lookup"><span data-stu-id="b32df-126">Modify the iOS project</span></span>
<span data-ttu-id="b32df-127">Uygulama göndermek için uç değiştiren göre yalnızca *kimliği* ilişkin bir bildirim, iOS uygulamanızı bu bildirim işlemek ve görüntülenecek güvenli ileti almak için arka uç geri arama için değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b32df-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="b32df-128">Bu hedefe ulaşmak için şu uygulama arka ucunu güvenli içeriği almak için mantığı yazmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="b32df-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="b32df-129">İçinde **AppDelegate.m**, emin olun uygulama kaydeder sessiz bildirimleri için gönderilen arka ucundan bildirim kimliği işler şekilde.</span><span class="sxs-lookup"><span data-stu-id="b32df-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="b32df-130">Ekleme **UIRemoteNotificationTypeNewsstandContentAvailability** didFinishLaunchingWithOptions seçeneği:</span><span class="sxs-lookup"><span data-stu-id="b32df-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="b32df-131">İçinde **AppDelegate.m** en üstünde şu bildirimi ile bir uygulama bölümüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b32df-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="b32df-132">Sonra uygulama bölümünde yer tutucu değiştirerek aşağıdaki kodu ekleyin `{back-end endpoint}` daha önce edindiğiniz, arka uç için uç noktaya sahip:</span><span class="sxs-lookup"><span data-stu-id="b32df-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

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

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="b32df-133">Şimdi biz gelen bildirim işlemek ve görüntülemek için içeriği almak için yukarıdaki yöntemini kullanın gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b32df-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="b32df-134">İlk olarak, biz, iOS uygulamanızın arka planda bir anında iletme bildirimi alınırken yürütmek etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b32df-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="b32df-135">İçinde **XCode**, uygulama projenizi Sol paneldeki seçin ve ardından ana uygulama hedefiniz tıklayın **hedefleri** merkezi bölmesinden bölümü.</span><span class="sxs-lookup"><span data-stu-id="b32df-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="b32df-136">Ardından, **yetenekleri** sekmesinde, merkezi bölmenin en üstünde ve denetleyin **uzak bildirimler** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="b32df-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="b32df-137">İçinde **AppDelegate.m** anında iletme bildirimleri işlemek için aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b32df-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
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
   
    <span data-ttu-id="b32df-138">Arka uç tarafından durumlarında eksik kimlik doğrulama üstbilgisi özelliği ya da reddetme tercih olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="b32df-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="b32df-139">Bu durumlarda belirli işleme çoğunlukla, hedef kullanıcı deneyimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b32df-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="b32df-140">Gerçek bildirim almak için kullanıcının kimliğini doğrulamak bildirim genel istemiyle görüntüle bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="b32df-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="b32df-141">Uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b32df-141">Run the Application</span></span>
<span data-ttu-id="b32df-142">Uygulamayı çalıştırmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="b32df-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="b32df-143">Xcode'da, uygulamayı fiziksel bir iOS cihazında (anında iletme bildirimleri benzeticisinde çalışmaz) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b32df-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="b32df-144">İOS uygulaması UI'da, bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="b32df-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="b32df-145">Bunlar herhangi bir dize olabilir, ancak aynı değeri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b32df-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="b32df-146">İOS uygulaması UI'da, tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="b32df-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="b32df-147">Ardından **Gönder itme**.</span><span class="sxs-lookup"><span data-stu-id="b32df-147">Then click **Send push**.</span></span> <span data-ttu-id="b32df-148">Bildirim Merkezinize görüntülenmesini güvenli bildirim görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b32df-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
