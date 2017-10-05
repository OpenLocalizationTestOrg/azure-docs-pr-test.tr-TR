---
title: "Azure Mobile Engagement kullanıcı arabirimi - Reach nasıl yapılır"
description: "Azure Mobile Engagement için kullanıcı arabirimi genel bakış"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 33a0a9d0c399cb7f0a791c4c16dde2e2d62364ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-using-and-managing-pushes-to-reach-out-to-your-end-users"></a><span data-ttu-id="22b4a-103">Son kullanıcılarınıza ulaşmak için kullanarak ve yönetmeye başlamak nasıl iter</span><span class="sxs-lookup"><span data-stu-id="22b4a-103">How to get started using and managing pushes to reach out to your end users</span></span>
<span data-ttu-id="22b4a-104">SDK'sını uygulamanıza tam olarak tümleşiktir sonra kullanmaya başlamak, uygulamanızın kullanıcılara anında iletme bildirimleri UI ulaşma bölüm.</span><span class="sxs-lookup"><span data-stu-id="22b4a-104">Once the SDK is fully integrated into your app, you can get started using the the Reach section of the UI to Push notifications to the users of your app.</span></span>  

## <a name="do-your-first-push-notification-campaign"></a><span data-ttu-id="22b4a-105">İlk anında iletme bildirimi kampanyanızı yapın</span><span class="sxs-lookup"><span data-stu-id="22b4a-105">Do Your First Push Notification Campaign</span></span>
* <span data-ttu-id="22b4a-106">SDK'sı ile uygulamanızı elinizin tümleştirilmiş onaylayın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-106">Confirm that your Reach is integrated into your app with the SDK.</span></span> 
* <span data-ttu-id="22b4a-107">Uygulamanızı seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-107">Select your application</span></span>

![First1][1]

* <span data-ttu-id="22b4a-109">"Reach" bölümü ve tıklatın "Yeni duyuru için" gidin</span><span class="sxs-lookup"><span data-stu-id="22b4a-109">Go to the "Reach" Section and Click "New announcement"</span></span>

![First2][2]

* <span data-ttu-id="22b4a-111">Yeni bir kampanya oluşturun ve adlandırın</span><span class="sxs-lookup"><span data-stu-id="22b4a-111">Create a new campaign and name it</span></span>
  
![First3][3]

* <span data-ttu-id="22b4a-113">Nasıl bildirim, uygulama yalnızca gönderilmesi gereken seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-113">Select how the notification should be delivered, as In-app only</span></span>

![First4][4]

* <span data-ttu-id="22b4a-115">Anında iletme istediğiniz iletiyi oluşturun</span><span class="sxs-lookup"><span data-stu-id="22b4a-115">Create the message you want to push</span></span>

![First5][5]

* <span data-ttu-id="22b4a-117">Bir başlık (isteğe bağlı) bildirim yazabilir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-117">You may write a title on the notification (Optional).</span></span>
* <span data-ttu-id="22b4a-118">Anında iletme iletisi içeriği yazma.</span><span class="sxs-lookup"><span data-stu-id="22b4a-118">Write push message content.</span></span>
* <span data-ttu-id="22b4a-119">Görüntüyü karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-119">You can upload an image.</span></span> <span data-ttu-id="22b4a-120">Dosyanın boyutu 32.768 baytı aşamaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-120">Be aware that the size of the file cannot exceed 32,768 bytes.</span></span>
* <span data-ttu-id="22b4a-121">Ayrıca daha fazla seçenek seçmek olanağına sahip, ancak bu öğretici için odak, daha sonra göreceğiz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-121">You also have the ability to select further options, but for the focus of this tutorial, we will see that later.</span></span>
* <span data-ttu-id="22b4a-122">Yalnızca bildirim olarak içerik türünü seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-122">Select the content type as Notification only</span></span>

![First6][6]

* <span data-ttu-id="22b4a-124">Anında iletme kampanyanızı oluşturmak ve kampanya listenizde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-124">Create your push campaign and it will appear in your campaign list.</span></span>

![First7][7]

## <a name="test-your-push-notification-campaign"></a><span data-ttu-id="22b4a-126">Anında iletme bildirimi kampanyanızı test</span><span class="sxs-lookup"><span data-stu-id="22b4a-126">Test Your Push Notification Campaign</span></span>
![Test1][8]

* <span data-ttu-id="22b4a-128">Cihazınızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="22b4a-128">Register your device.</span></span>
* <span data-ttu-id="22b4a-129">Anında iletme cihazın onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-129">Click on the checkbox of the device you want to push.</span></span>
* <span data-ttu-id="22b4a-130">Anında iletme cihaza göndermek için "Test" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-130">Click on the "Test" button to send the push to the device.</span></span>

![Test2][9]

* <span data-ttu-id="22b4a-132">Kampanya etkinleştir</span><span class="sxs-lookup"><span data-stu-id="22b4a-132">Activate the campaign</span></span>

![test3][10]

* <span data-ttu-id="22b4a-134">Kampanyanızı oluşturduğunuza göre yalnızca kullanıcılarınıza edilmesini bildirim için etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-134">Now that you have created your campaign you just need to activate it for the notification to be pushed to your users.</span></span>

## <a name="send-personalized-pushes"></a><span data-ttu-id="22b4a-135">Kişiselleştirilmiş bildirim gönder</span><span class="sxs-lookup"><span data-stu-id="22b4a-135">Send Personalized Pushes</span></span>
* <span data-ttu-id="22b4a-136">Bu örnek, bir özel indirim kod anında iletme bildirimi girildiği push oluşturur.</span><span class="sxs-lookup"><span data-stu-id="22b4a-136">This example creates a push where a custom rebate code is entered into the push notification.</span></span>

![Personalize1][11]

<span data-ttu-id="22b4a-138">Kişiselleştirme çalışır, böylece tarafından bir işaretçi bir uygulama bilgisi etiketinde değiştirerek kullanıcının ilk olarak tanımlanan uygun app-info olduğundan emin olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-138">Personalization works by replacing a marker by from an app info tag so, you'll have to make sure the user has the proper app-info defined first.</span></span> <span data-ttu-id="22b4a-139">Bu örnekte ve hedef kullanıcı tanımlı rebate_code adlı bir uygulama bilgisi etiketi sahip olur.</span><span class="sxs-lookup"><span data-stu-id="22b4a-139">In this example the targeted users will have an app info tag named rebate_code defined.</span></span>
<span data-ttu-id="22b4a-140">Yukarıda gördüğünüz gibi anında bildirim içeriği uygulama bilgisi etiketi gerçek içerik tarafından değiştirilmesini olduğunu bildirecektir işaret ${rebate_code} içerir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-140">As you see above the push notification content includes the marker ${rebate_code} which will indicate that it is to be replaced by the actual content of the app info tag.</span></span>

> [!WARNING]
> <span data-ttu-id="22b4a-141">Uygulama bilgileri etiketi için kullanıcı tanımlı değil, kullanıcı anında alır değil.</span><span class="sxs-lookup"><span data-stu-id="22b4a-141">If the app info tag is not defined for the user, the user will not receive the push.</span></span>

* <span data-ttu-id="22b4a-142">Sonuç</span><span class="sxs-lookup"><span data-stu-id="22b4a-142">Result</span></span>

![Personalize2][12]

### <a name="you-can-further-personalize-the-text-your-notification"></a><span data-ttu-id="22b4a-144">Daha fazla metin bildiriminizin kişiselleştirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="22b4a-144">You can further personalize the text your notification</span></span>
![Personalize3][13]

* <span data-ttu-id="22b4a-146">Bildirim başlığı dahil olmak üzere,</span><span class="sxs-lookup"><span data-stu-id="22b4a-146">Including the title of the notification,</span></span>
* <span data-ttu-id="22b4a-147">Ve ileti içeriği.</span><span class="sxs-lookup"><span data-stu-id="22b4a-147">And the content of the message.</span></span>
* <span data-ttu-id="22b4a-148">Duyuru (metin görünümü veya Web görünümü) türünü seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-148">Choose the type of announcement (Text view or Web view)</span></span>

![Personalize4][14]

### <a name="the-body-of-an-announcement-may-also-be-personalized-with"></a><span data-ttu-id="22b4a-150">Duyuru gövdesi ile de kişiselleştirilmiş:</span><span class="sxs-lookup"><span data-stu-id="22b4a-150">The body of an announcement may also be personalized with:</span></span>
* <span data-ttu-id="22b4a-151">Eylem URL'si giriş sayfası özelleştirmek istediğiniz</span><span class="sxs-lookup"><span data-stu-id="22b4a-151">The action URL, should you want to customize the landing page</span></span>
* <span data-ttu-id="22b4a-152">Başlık</span><span class="sxs-lookup"><span data-stu-id="22b4a-152">The title,</span></span>
* <span data-ttu-id="22b4a-153">İleti gövdesi.</span><span class="sxs-lookup"><span data-stu-id="22b4a-153">The body of the message.</span></span>

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a><span data-ttu-id="22b4a-154">Bilgisayarınızı anında iletilen bildirim (içeri veya uygulama dışında) ayırt</span><span class="sxs-lookup"><span data-stu-id="22b4a-154">Differentiate Your Push Notification (in or out of app)</span></span>
* <span data-ttu-id="22b4a-155">Anında iletme, uygulamanızı seçin, "Reach" bölümüne gidin, seçin veya bir anında iletme kampanya oluşturacak ve "Bildirim" bölümüne gidin bildirim türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="22b4a-155">Choose the type of notification you will push, select your application, go to the "Reach" section, select or create a push campaign and go to the "Notification" section.</span></span>
* <span data-ttu-id="22b4a-156">' I tıklatın, "teslimat modunu" istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-156">Click on the "delivery mode" you want.</span></span>
* <span data-ttu-id="22b4a-157">Bildirim istediğinizde "Kısıtlamak etkinlikler" onay kutusunu tıklayarak belirli etkinlikleri (ekranları) oluşur.</span><span class="sxs-lookup"><span data-stu-id="22b4a-157">Click on the "Restrict Activities" checkbox when you want the notification occurs on specific activities (screens).</span></span>

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a><span data-ttu-id="22b4a-159">"Yalnızca uygulama dışında" teslimat</span><span class="sxs-lookup"><span data-stu-id="22b4a-159">"Out of App Only" delivery mode</span></span>
![Differentiate2][16]

<span data-ttu-id="22b4a-161">"Yalnızca uygulama dışında" teslimat uygulama kapatıldığında anında iletme bildirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="22b4a-161">"Out of App Only" delivery mode provides push notification when the application is closed.</span></span> <span data-ttu-id="22b4a-162">Standart anında iletme bildirimi budur.</span><span class="sxs-lookup"><span data-stu-id="22b4a-162">This is the standard push notification.</span></span>
<span data-ttu-id="22b4a-163">"Yalnızca uygulama dışı" seçtiğinizde, zaten uygulamanız (APNS veya GCM) oluşturuyor platform sertifikalardan sağlamış olmanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="22b4a-163">When you select "out of app only" ,you must have already provided the certificates from the platform that your application is building on (APNS or GCM).</span></span>

### <a name="see-also"></a><span data-ttu-id="22b4a-164">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-164">See also</span></span>
* <span data-ttu-id="22b4a-165">[Apple anında bildirim hizmeti – sertifikaları](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google bulut Mesajlaşma – sertifika](http://developer.android.com/google/gcm/index.html)</span><span class="sxs-lookup"><span data-stu-id="22b4a-165">[Apple Push Notification Service – Certificates](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging – Certificate](http://developer.android.com/google/gcm/index.html)</span></span> 

### <a name="in-app-only-delivery-mode"></a><span data-ttu-id="22b4a-166">"uygulama yalnızca" teslimat</span><span class="sxs-lookup"><span data-stu-id="22b4a-166">"in-App Only" delivery mode</span></span>
![Differentiate3][17]

<span data-ttu-id="22b4a-168">Uygulama çalışırken "Uygulama yalnızca" teslimat anında iletme bildirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="22b4a-168">"In-App Only" delivery mode provides push notification when the application is running.</span></span>
<span data-ttu-id="22b4a-169">Bu bildirim için APNS ve GCM sistem üzerinden gitmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="22b4a-169">For this notification, you do not need to go through the APNS and GCM system.</span></span>
<span data-ttu-id="22b4a-170">Uygulama teslim sistemi kullanıcılarınıza ulaşmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-170">You can use the in-app delivery system to reach your end-users.</span></span>
<span data-ttu-id="22b4a-171">Tam bildirim özelleştirmek ve etkinlik (ekran) bildirim görüntüleneceği karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-171">You can fully customize the notification and decide in which activity (screen) the notification will appear.</span></span>

### <a name="anytime-delivery-mode"></a><span data-ttu-id="22b4a-172">"Dilediğiniz zaman" teslimat</span><span class="sxs-lookup"><span data-stu-id="22b4a-172">"Anytime" delivery mode</span></span>
<span data-ttu-id="22b4a-173">Bir "Her zaman" teslimat seçebilirsiniz, uygulama veya çalışıp çalışmadığını kullanıcınızın ulaşması sağlar.</span><span class="sxs-lookup"><span data-stu-id="22b4a-173">You can choose an "Anytime" delivery mode, ensures you to reach your end-user whether the application is running or not.</span></span>
<span data-ttu-id="22b4a-174">"Dilediğiniz zaman" seçtiğinizde, zaten uygulamanız (APNS veya GCM) oluşturuyor platform sertifikalardan sağlamış olmanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="22b4a-174">When you select "Anytime" , you must have already provided the certificates from the platform that your application is building upon (APNS or GCM).</span></span> 

## <a name="schedule-a-push-campaign"></a><span data-ttu-id="22b4a-175">Anında iletme kampanya zamanlama</span><span class="sxs-lookup"><span data-stu-id="22b4a-175">Schedule a Push Campaign</span></span>
### <a name="plan-to-start-a-campaign"></a><span data-ttu-id="22b4a-176">Bir kampanya başlatmak planlama</span><span class="sxs-lookup"><span data-stu-id="22b4a-176">Plan to Start a campaign</span></span>
![Shedule1][18]

<span data-ttu-id="22b4a-178">21 Mart olduğu ve yapmak için bir bildirime sahip, 22 Mart için gece yarısı planlanmış.</span><span class="sxs-lookup"><span data-stu-id="22b4a-178">It is the 21st of March and you have an announcement to make and planed for the 22nd of March at midnight.</span></span> <span data-ttu-id="22b4a-179">Push yapmak için arabirimi önünde kalmak gerekmez!</span><span class="sxs-lookup"><span data-stu-id="22b4a-179">You don’t have to stay in front of the interface to do a push!</span></span> <span data-ttu-id="22b4a-180">Önceden bildirimleri gönderilecek tam dakika planlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-180">You can plan in advance the exact minute notifications will be sent.</span></span>

* <span data-ttu-id="22b4a-181">Kaldırma onay "Hiçbiri" onay kutusunu ve bir başlangıç saati seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-181">Un-check the "None" checkbox and select a start time</span></span> 
* <span data-ttu-id="22b4a-182">Tarih ve itme kampanya başlamasını istediğiniz saati seçin.</span><span class="sxs-lookup"><span data-stu-id="22b4a-182">Choose the date and the time you want to start the push campaign.</span></span>

### <a name="plan-to-end-a-campaign"></a><span data-ttu-id="22b4a-183">Bir kampanya sona erdirmek planlama</span><span class="sxs-lookup"><span data-stu-id="22b4a-183">Plan to end a campaign</span></span>
![Shedule2][19]

<span data-ttu-id="22b4a-185">Kampanyanızı 25 Mart üzerinde 3:00 pm durdurmak istiyor ancak orada yapmak için olmayacaktır biliyor.</span><span class="sxs-lookup"><span data-stu-id="22b4a-185">You want your campaign to stop on the 25th of March at 3.00 pm but you know you won't be there to do it.</span></span>
<span data-ttu-id="22b4a-186">İtme arabirimi önünde kalmak gerekmez!</span><span class="sxs-lookup"><span data-stu-id="22b4a-186">You don’t have to stay in front of the interface to push!</span></span> <span data-ttu-id="22b4a-187">Önceden, kampanya durur tam dakika planlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22b4a-187">You can plan in advance the exact minute your campaign will stop.</span></span>

* <span data-ttu-id="22b4a-188">Tıklayın "yok" onay kutusunu veya bir bitiş saati seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-188">Click on the "None" checkbox or select a end time</span></span>
* <span data-ttu-id="22b4a-189">Tarih ve saat itme kampanya tamamlamak istiyorsanız seçin.</span><span class="sxs-lookup"><span data-stu-id="22b4a-189">Choose the date and the time you want to finish the push campaign.</span></span>

### <a name="end-a-campaign-manually"></a><span data-ttu-id="22b4a-190">Bir kampanya el ile bitmelidir</span><span class="sxs-lookup"><span data-stu-id="22b4a-190">End a campaign manually</span></span>
![Shedule3][20]

<span data-ttu-id="22b4a-192">Varsayılan olarak, "None" onay kutuları seçilir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-192">By default, the "None" check-boxes are selected.</span></span>
<span data-ttu-id="22b4a-193">Başka bir deyişle, ulaşma bölümünde etkinleştirmek ve reach bölümüne durdurulacak zaman sona ereceği hemen sonra kampanya başlar.</span><span class="sxs-lookup"><span data-stu-id="22b4a-193">This means that the campaign will start as soon as you activate it in the reach section and will end when you will stop it on the reach section.</span></span>

> [!NOTE]
> <span data-ttu-id="22b4a-194">Bitiş tarihi oluşturulan Kampanyalar itme cihazda yerel olarak depolamak ve kampanya el ile sona erdi olsa bile uygulama sonraki açılışında gösterir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-194">Campaigns created without an end date store the push locally on the device and show it the next time the app is opened even if the campaign is manually ended.</span></span>

## <a name="enhance-a-push-notification-with-a-text-view"></a><span data-ttu-id="22b4a-195">Metin görünümü ile anında iletme bildirimi geliştirin</span><span class="sxs-lookup"><span data-stu-id="22b4a-195">Enhance a Push Notification with a Text View</span></span>
### <a name="what-is-a-text-view"></a><span data-ttu-id="22b4a-196">Metin Görünümü nedir?</span><span class="sxs-lookup"><span data-stu-id="22b4a-196">What is a Text View?</span></span>
![TextView1][21]

<span data-ttu-id="22b4a-198">Metni metin içeriği içeren bir açılır pencere görülmektedir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-198">A text view is a pop-up with text content.</span></span> <span data-ttu-id="22b4a-199">Son kullanıcı anında iletme bildirimine tıklamıştır sonra bu açılır pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="22b4a-199">This pop-up appears after the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="22b4a-200">Metin görünümü, son kullanıcı için daha fazla içerik sunmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="22b4a-200">A text view allows you to present more content to your end-user.</span></span> <span data-ttu-id="22b4a-201">Bu da bir coğrafi olarak yerelleştirilmiş arama başlayarak bir e-posta gönderilirken bir web sayfası açılıyor bir mağazaya, yeniden yönlendirme, uygulamanızın bir sayfa atlama gibi bir işlem için bir çağrı sunmak için fırsattır vb....</span><span class="sxs-lookup"><span data-stu-id="22b4a-201">This is also the opportunity to present a call to action such as jumping to a page of your app, redirecting to a Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-text-view"></a><span data-ttu-id="22b4a-202">Örnek: Metin görünümü</span><span class="sxs-lookup"><span data-stu-id="22b4a-202">Example: Text View</span></span>
* <span data-ttu-id="22b4a-203">"Reach" bölümünde anında iletme bildirimi kampanyanızı oluşturmak ve kampanyanızı adlandırın</span><span class="sxs-lookup"><span data-stu-id="22b4a-203">Create your Push notification campaign in the "Reach" section and give your campaign a name</span></span>

![TextView2][22]

* <span data-ttu-id="22b4a-205">Görüntülenecek ileti bildirimi yazma.</span><span class="sxs-lookup"><span data-stu-id="22b4a-205">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="22b4a-206">"Metin" Duyuru içerik türünü seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-206">Select the Announcement Content Type of “text”</span></span>

![TextView3][23]

> [!NOTE]
> <span data-ttu-id="22b4a-208">Metin görünümü bastığınızda, her zaman içeren bir bildirim önce gelir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-208">When you push a text view, it always comes with a notification first.</span></span> 

* <span data-ttu-id="22b4a-209">Metin (metin duyuru içeriği alt bölümünün görünür, görüntülenmesini istediğiniz metin tanımlamanıza olanak sağlayan seçtikten sonra.) tanımlayın</span><span class="sxs-lookup"><span data-stu-id="22b4a-209">Define the text (After having selected the text announcement content, the sub-section will appear, allowing you to define the text you want to be displayed.)</span></span>

![TextView4][24]

* <span data-ttu-id="22b4a-211">İleti üstünde görünür başlık yazın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-211">Write the title that will appear at the top of the message.</span></span>
* <span data-ttu-id="22b4a-212">Metin görünümü ana içeriğini yazma.</span><span class="sxs-lookup"><span data-stu-id="22b4a-212">Write the main content of the text view.</span></span>
* <span data-ttu-id="22b4a-213">(Bir uygulama mağazasının veya herhangi bir tür, sağlayabilirsiniz kaynakları yönlendirme uygulama sayfasını açarak gibi belirli bir eylemi yapmak uygulama eylem düğmesi sağlar) eylem düğmesine görünür içerik yazma.</span><span class="sxs-lookup"><span data-stu-id="22b4a-213">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to an App store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="22b4a-214">Çıkış düğmesi görünür içerik yazma (çıkış düğmeyi tıklatarak, metin görünümü kaybolur.)</span><span class="sxs-lookup"><span data-stu-id="22b4a-214">Write the content that will appear on the exit button (by clicking on the exit button, the text view will disappear.)</span></span>
* <span data-ttu-id="22b4a-215">Anında iletme bildirimi kampanyanızı oluşturmak ve kampanya listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-215">Create your push notification campaign and it will appear on the campaign list.</span></span>

![TextView5][25]

* <span data-ttu-id="22b4a-217">Metin görünümü, kullanıcılara göndermek için anında iletme bildirimi kampanyanızı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="22b4a-217">Activate your push notification campaign to send the text view to your users.</span></span>

![TextView6][26]

* <span data-ttu-id="22b4a-219">Sonuç</span><span class="sxs-lookup"><span data-stu-id="22b4a-219">Result</span></span>

![TextView7][27]

* <span data-ttu-id="22b4a-221">Kullanıcı onu tıklayın ve bildirim alır.</span><span class="sxs-lookup"><span data-stu-id="22b4a-221">The user receives the notification and click on it.</span></span>
* <span data-ttu-id="22b4a-222">Metin görünümü ile etkileşim arkasından bir açılır pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="22b4a-222">The text view appears as a pop-up allowing the user to interact with it.</span></span>

## <a name="enhance-a-push-notification-with-a-web-view"></a><span data-ttu-id="22b4a-223">Bir Web görünümü ile anında iletme bildirimi geliştirin</span><span class="sxs-lookup"><span data-stu-id="22b4a-223">Enhance a Push Notification with a Web View</span></span>
### <a name="what-is-a-web-view"></a><span data-ttu-id="22b4a-224">Bir Web Görünümü nedir?</span><span class="sxs-lookup"><span data-stu-id="22b4a-224">What is a Web View?</span></span>
![WebView1][28]

<span data-ttu-id="22b4a-226">Bir web görünümü web içeriği içeren bir açılır pencere ' dir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-226">A web view is a pop-up with web content.</span></span> <span data-ttu-id="22b4a-227">Bu açılır pencere, son kullanıcı anında iletme bildirimine tıkladığında açılır.</span><span class="sxs-lookup"><span data-stu-id="22b4a-227">This pop-up appears when the end-user has clicked on the push notification.</span></span>
<span data-ttu-id="22b4a-228">Web görünümü son kullanıcı ile daha fazla etkileşime girmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="22b4a-228">A web view allows you to have more interaction with the end-user.</span></span>
<span data-ttu-id="22b4a-229">Bu aynı zamanda App Store için yeniden yönlendirme gibi eylem çağrısı sunmak için fırsattır bir web sayfasını açarak, bir e-posta gönderme, coğrafi olarak yerelleştirilmiş bir arama başlayarak, vb....</span><span class="sxs-lookup"><span data-stu-id="22b4a-229">This is also the opportunity to present a call to action such as redirection to App Store, opening a web page, sending an e-mail, starting a geo-localized search, etc...</span></span>

### <a name="example-web-view"></a><span data-ttu-id="22b4a-230">Örnek: Web görünümü</span><span class="sxs-lookup"><span data-stu-id="22b4a-230">Example: Web View</span></span>
* <span data-ttu-id="22b4a-231">"Reach" bölümünde anında iletme kampanyanızı oluşturmak ve kampanyanızı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-231">Create your Push campaign in the "Reach" section and give your campaign a name.</span></span>

![WebView2][29]

* <span data-ttu-id="22b4a-233">Görüntülenecek ileti bildirimi yazma.</span><span class="sxs-lookup"><span data-stu-id="22b4a-233">Write the message that will appear on the notification.</span></span>
* <span data-ttu-id="22b4a-234">"Web" Duyuru içerik türünü seçin</span><span class="sxs-lookup"><span data-stu-id="22b4a-234">Select the Announcement Content Type as “web”</span></span>

![WebView3][30]

### <a name="about-announcement-types"></a><span data-ttu-id="22b4a-236">Duyuru türleri hakkında:</span><span class="sxs-lookup"><span data-stu-id="22b4a-236">About Announcement types:</span></span>
* <span data-ttu-id="22b4a-237">Yalnızca bildirim: Basit standart bir bildirim değil.</span><span class="sxs-lookup"><span data-stu-id="22b4a-237">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="22b4a-238">Bu kullanıcı üzerinde tıklatır, ek görünüm yok görünür, ancak yalnızca kendisine ilişkili eylemin oluşacağını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-238">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="22b4a-239">Metin duyuru: metin görünümü bakın kullanıcıya prosese bir bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-239">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="22b4a-240">Web duyuru: kullanıcının bir web görünümü göz prosese bir bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-240">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>
  <span data-ttu-id="22b4a-241">"Web duyuru" içeriğini seçin.</span><span class="sxs-lookup"><span data-stu-id="22b4a-241">Select the "Web announcement" content.</span></span>

> [!NOTE]
> <span data-ttu-id="22b4a-242">Bir web görünümü bastığınızda, her zaman içeren bir bildirim önce gelir.</span><span class="sxs-lookup"><span data-stu-id="22b4a-242">When you push a web view, it always comes with a notification first.</span></span>

* <span data-ttu-id="22b4a-243">(Web duyuru içeriği alt bölümde görünür, görüntülenmesini istediğiniz web görünümü içeriğini tanımlamanıza olanak sağlayan seçtikten sonra.) web içeriğini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="22b4a-243">Define the web content (After having selected the web announcement content, the subsection will appear, allowing you to define the web view content you want to be displayed.)</span></span>

![WebView4][31]

* <span data-ttu-id="22b4a-245">(İsteğe bağlı) iletinin üstünde görünür başlık yazın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-245">Write the title that will appear at the top of the message (optional).</span></span>
* <span data-ttu-id="22b4a-246">HTML kodunuzu buraya yazın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-246">Write your HTML code here.</span></span>
* <span data-ttu-id="22b4a-247">Kaynak düzenleme modu düğmesini edition geçmek ve nasıl nasıl göründüğünü görmek için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-247">Click on the source editing mode button to switch edition and see how it looks like.</span></span>
* <span data-ttu-id="22b4a-248">(Bir mağazaya veya herhangi bir tür, sağlayabilirsiniz kaynakları yönlendirme uygulama sayfasını açarak gibi belirli bir eylemi yapmak uygulama eylem düğmesi sağlar) eylem düğmesine görünür içerik yazma.</span><span class="sxs-lookup"><span data-stu-id="22b4a-248">Write the content that will appear on the action button (an action button enables the application to make a specific action such as opening a page of the application, redirecting to a Store or any kind of sources you can provide).</span></span>
* <span data-ttu-id="22b4a-249">Çıkış düğmesi görünür içerik yazma (çıkış düğmeyi tıklatarak, web görünümü kaybolur).</span><span class="sxs-lookup"><span data-stu-id="22b4a-249">Write the content that will appear on the exit button (by clicking on the exit button, the web view will disappear).</span></span>
* <span data-ttu-id="22b4a-250">Sonuç</span><span class="sxs-lookup"><span data-stu-id="22b4a-250">Result</span></span>

![WebView5][32]

* <span data-ttu-id="22b4a-252">Kullanıcı bildirimi ve tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22b4a-252">The user receive the notification and click on it.</span></span>
* <span data-ttu-id="22b4a-253">Metin görünümü ile etkileşim arkasından bir açılır pencere görünür.</span><span class="sxs-lookup"><span data-stu-id="22b4a-253">The text view appears as a pop-up allowing the user to interact with it.</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

