---
title: "Güvenli anında iletme bildirimleri Azure Notification Hubs ile aaaSending"
description: "Nasıl toosend güvenli anında iletme bildirimleri tooan Android uygulaması Azure'dan öğrenin. Java ve C# içinde yazılan kod örnekleri."
documentationcenter: android
keywords: "anında iletme bildirimi, anında iletme bildirimleri, anında iletileri, android anında iletme bildirimleri"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="44569-105">Azure Notification Hubs ile güvenli anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="44569-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44569-106">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="44569-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="44569-107">iOS</span><span class="sxs-lookup"><span data-stu-id="44569-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="44569-108">Android</span><span class="sxs-lookup"><span data-stu-id="44569-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="44569-109">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="44569-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="44569-110">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44569-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="44569-111">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44569-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="44569-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="44569-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="44569-113">Microsoft Azure anında iletme bildirimi desteği tooaccess tüketici ve kurumsal uygulamalar için anında iletme bildirimlerinin hello uyarlamasını büyük ölçüde basitleştirir kullanımı kolay, çok platformlu, ölçeği anında iletme iletisi altyapısı sağlar Mobil platformlar.</span><span class="sxs-lookup"><span data-stu-id="44569-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="44569-114">Tooregulatory veya güvenlik kısıtlamaları, bazen bir uygulama bir şey hello standart anında iletme bildirimi altyapısı iletilen hello bildirim tooinclude isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44569-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="44569-115">Bu öğretici nasıl tooachieve hello aynı deneyimi hello istemci Android cihazı ve hello uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı üzerinden hassas bilgileri göndererek açıklar.</span><span class="sxs-lookup"><span data-stu-id="44569-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="44569-116">Yüksek bir düzeyde hello akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="44569-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="44569-117">Merhaba uygulama arka ucu:</span><span class="sxs-lookup"><span data-stu-id="44569-117">hello app back-end:</span></span>
   * <span data-ttu-id="44569-118">Arka uç veritabanı güvenli yükünde depolar.</span><span class="sxs-lookup"><span data-stu-id="44569-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="44569-119">Merhaba (güvenli hiçbir bilgi gönderilmez) Bu bildirim toohello Android bir aygıtın Kimliğini gönderir.</span><span class="sxs-lookup"><span data-stu-id="44569-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="44569-120">Merhaba cihaza hello bildirim alırken Hello uygulamanın:</span><span class="sxs-lookup"><span data-stu-id="44569-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="44569-121">Merhaba Android cihaz hello arka uç isteyen hello güvenli yükü bağlanır.</span><span class="sxs-lookup"><span data-stu-id="44569-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="44569-122">Merhaba uygulama hello yükü hello aygıt bildirim olarak gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="44569-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="44569-123">Merhaba kullanıcı oturum açtığında sonra akışı önceki hello (ve Bu öğreticide), biz hello aygıt varsayın toonote kimlik doğrulama belirtecini yerel depolama biriminde, depolar. önemlidir.</span><span class="sxs-lookup"><span data-stu-id="44569-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="44569-124">Merhaba aygıt hello bildirim'ın güvenli yükü bu belirteci kullanarak alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="44569-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="44569-125">Uygulamanızın kimlik doğrulama belirteçleri hello aygıtta depolamaz veya bu belirteçleri süresi, hello anında iletme bildirimi aldığında gerçekleştireceği hello cihaz uygulaması hello kullanıcı toolaunch hello uygulama isteyen genel bir bildirim görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="44569-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="44569-126">Merhaba uygulama hello kullanıcının kimliğini doğrular ve hello bildirim yükü gösterir.</span><span class="sxs-lookup"><span data-stu-id="44569-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="44569-127">Bu öğretici nasıl toosend güvenli anında iletme bildirimleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="44569-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="44569-128">Merhaba üzerinde derlemeler [kullanıcılara bildirme](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) henüz yapmadıysanız, hello adımları Bu öğreticinin ilk tamamlamanız gerekir böylece öğretici.</span><span class="sxs-lookup"><span data-stu-id="44569-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="44569-129">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (Android) ile çalışmaya başlama](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44569-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="44569-130">Merhaba Android projesi değiştirme</span><span class="sxs-lookup"><span data-stu-id="44569-130">Modify hello Android project</span></span>
<span data-ttu-id="44569-131">Uygulama arka uç toosend yalnızca hello değiştiren göre *kimliği* bir anında iletme bildirimi bildirim ve geri arama, arka uç tooretrieve hello görüntülenen ileti toobe güvenli, Android uygulaması toohandle toochange sahip.</span><span class="sxs-lookup"><span data-stu-id="44569-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="44569-132">tooachieve bu hedefe toomake Android uygulamanızı bilir emin sahip nasıl tooauthenticate kendisi, hello anında iletme bildirimleri aldığında uç ile.</span><span class="sxs-lookup"><span data-stu-id="44569-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="44569-133">Biz şimdi hello değiştirecek *oturum açma* sipariş toosave hello kimlik doğrulaması üstbilgi değeri hello akışında paylaşılan tercihleri, uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="44569-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="44569-134">Benzer mekanizmaları kullanılan toostore olabilir kullanıcı kimlik bilgilerini gerek kalmadan toouse uygulama hello tüm kimlik doğrulama belirteci (örneğin OAuth belirteçlerini) sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="44569-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="44569-135">Merhaba hello üstündeki sabitleri aşağıdaki hello Android uygulaması projenize eklemek **MainActivity** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="44569-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="44569-136">Merhaba yine de **MainActivity** sınıfı, güncelleştirme hello `getAuthorizationHeader()` koddan yöntemi toocontain hello:</span><span class="sxs-lookup"><span data-stu-id="44569-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="44569-137">Merhaba aşağıdakileri ekleyin `import` deyimleri hello hello üstündeki **MainActivity** dosyası:</span><span class="sxs-lookup"><span data-stu-id="44569-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="44569-138">Şimdi biz hello bildirim alındığında çağrılan hello işleyici değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="44569-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="44569-139">Merhaba, **MyHandler** sınıfı değiştirmek hello `OnReceive()` yöntemi toocontain:</span><span class="sxs-lookup"><span data-stu-id="44569-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="44569-140">Merhaba eklemek `retrieveNotification()` hello yer tutucu değiştirme yöntemi `{back-end endpoint}` , arka uç dağıtırken elde hello arka uç uç noktası ile:</span><span class="sxs-lookup"><span data-stu-id="44569-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="44569-141">Bu yöntem, uygulama arka uç tooretrieve hello bildirim hello depolanan hello kimlik bilgilerini kullanarak ve paylaşılan tercihleri normal bir bildirim görüntüler içerik çağırır.</span><span class="sxs-lookup"><span data-stu-id="44569-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="44569-142">Merhaba bildirim toohello uygulama kullanıcı herhangi bir anında iletme bildirimi gibi tam olarak arar.</span><span class="sxs-lookup"><span data-stu-id="44569-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="44569-143">Tercih toohandle hello örneklerini eksik kimlik doğrulama üstbilgisi özelliği ya da reddetme hello arka uç tarafından olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="44569-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="44569-144">Bu durumlarda belirli işleme Hello çoğunlukla, hedef kullanıcı deneyimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="44569-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="44569-145">Toodisplay hello kullanıcı tooauthenticate tooretrieve hello gerçek bildirimi için genel bir istem içeren bir bildirim bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="44569-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="44569-146">Merhaba uygulama çalıştırın</span><span class="sxs-lookup"><span data-stu-id="44569-146">Run hello Application</span></span>
<span data-ttu-id="44569-147">toorun Merhaba uygulama, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="44569-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="44569-148">Emin olun **AppBackend** Azure'da dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="44569-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="44569-149">Visual Studio kullanıyorsanız hello çalıştırın **AppBackend** Web API uygulaması.</span><span class="sxs-lookup"><span data-stu-id="44569-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="44569-150">Bir ASP.NET web sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="44569-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="44569-151">Eclipse'te, Android fiziksel bir aygıt veya hello öykünücüsü hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="44569-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="44569-152">Hello Android uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="44569-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="44569-153">Bunlar herhangi bir dize olabilir, ancak bunlar olmalıdır hello aynı değeri.</span><span class="sxs-lookup"><span data-stu-id="44569-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="44569-154">Merhaba Android uygulamanın kullanıcı Arabirimi, tıklayın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="44569-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="44569-155">Ardından **Gönder itme**.</span><span class="sxs-lookup"><span data-stu-id="44569-155">Then click **Send push**.</span></span>

