---
title: "aaaAzure güvenli hub bildirim gönderme"
description: "Nasıl toosend güvenli anında iletme bildirimleri ile Azure öğrenin. Merhaba .NET API kullanarak C# içinde yazılan kod örnekleri."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="46862-104">Azure Notification Hubs güvenli bildirme</span><span class="sxs-lookup"><span data-stu-id="46862-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46862-105">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="46862-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="46862-106">iOS</span><span class="sxs-lookup"><span data-stu-id="46862-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="46862-107">Android</span><span class="sxs-lookup"><span data-stu-id="46862-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="46862-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="46862-108">Overview</span></span>
<span data-ttu-id="46862-109">Microsoft Azure anında iletme bildirimi desteği tooaccess Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir bir kullanımı kolay, çok platformlu, ölçeği gönderim altyapısı sağlar Platform.</span><span class="sxs-lookup"><span data-stu-id="46862-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="46862-110">Tooregulatory veya güvenlik kısıtlamaları, bazen bir uygulama bir şey hello standart anında iletme bildirimi altyapısı iletilen hello bildirim tooinclude isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46862-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="46862-111">Bu öğretici nasıl tooachieve hello aynı deneyimi hello istemci aygıt hello uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı üzerinden hassas bilgileri göndererek açıklar.</span><span class="sxs-lookup"><span data-stu-id="46862-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="46862-112">Yüksek bir düzeyde hello akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="46862-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="46862-113">Merhaba uygulama arka ucu:</span><span class="sxs-lookup"><span data-stu-id="46862-113">hello app back-end:</span></span>
   * <span data-ttu-id="46862-114">Arka uç veritabanı güvenli yükünde depolar.</span><span class="sxs-lookup"><span data-stu-id="46862-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="46862-115">Merhaba (güvenli hiçbir bilgi gönderilmez) Bu bildirim toohello aygıtın Kimliğini gönderir.</span><span class="sxs-lookup"><span data-stu-id="46862-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="46862-116">Merhaba cihaza hello bildirim alırken Hello uygulamanın:</span><span class="sxs-lookup"><span data-stu-id="46862-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="46862-117">Merhaba cihaz hello arka uç isteyen hello güvenli yükü bağlanır.</span><span class="sxs-lookup"><span data-stu-id="46862-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="46862-118">Merhaba uygulama hello yükü hello aygıt bildirim olarak gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="46862-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="46862-119">Merhaba kullanıcı oturum açtığında sonra akışı önceki hello (ve Bu öğreticide), biz hello aygıt varsayın toonote kimlik doğrulama belirtecini yerel depolama biriminde, depolar. önemlidir.</span><span class="sxs-lookup"><span data-stu-id="46862-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="46862-120">Merhaba aygıt hello bildirim'ın güvenli yükü bu belirteci kullanarak alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="46862-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="46862-121">Uygulamanızın kimlik doğrulama belirteçleri hello aygıtta depolamaz veya bu belirteçleri süresi, hello hello bildirim alma sırasında cihaz uygulaması hello kullanıcı toolaunch hello uygulama isteyen genel bir bildirim görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="46862-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="46862-122">Merhaba uygulama hello kullanıcının kimliğini doğrular ve hello bildirim yükü gösterir.</span><span class="sxs-lookup"><span data-stu-id="46862-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="46862-123">Bu güvenli itme öğreticide gösterilmiştir nasıl toosend bir anında iletme bildirimi güvenli bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="46862-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="46862-124">Merhaba öğretici derlemeler üzerinde hello [kullanıcılara bildirme](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) önce bu öğreticide hello adımlar tamamlanmalıdır şekilde öğretici.</span><span class="sxs-lookup"><span data-stu-id="46862-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="46862-125">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (Windows mağazası) ile çalışmaya başlama](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="46862-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="46862-126">Ayrıca, Windows Phone 8.1 (Windows Phone değil) Windows kimlik bilgileri gerektirir ve arka plan görevleri Windows Phone 8.0 veya Silverlight 8.1 çalışmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="46862-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="46862-127">Windows mağazası uygulamaları için yalnızca hello uygulama ekran kilitleme etkin ise bir arka plan görevi aracılığıyla bildirimleri alabilirsiniz (Merhaba Appmanifest hello onay kutusu tıklayın).</span><span class="sxs-lookup"><span data-stu-id="46862-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="46862-128">Windows Phone proje Hello değiştirme</span><span class="sxs-lookup"><span data-stu-id="46862-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="46862-129">Merhaba, **NotifyUserWindowsPhone** projesi, kod tooApp.xaml.cs tooregister hello itme arka plan görevi aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="46862-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="46862-130">Aşağıdaki kod hello hello sonunda hello eklemek `OnLaunched()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="46862-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="46862-131">Hala App.xaml.cs dosyasında koddan hemen sonra hello hello eklemek `OnLaunched()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="46862-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="46862-132">Merhaba aşağıdakileri ekleyin `using` deyimleri hello App.xaml.cs dosyasını hello üstündeki:</span><span class="sxs-lookup"><span data-stu-id="46862-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="46862-133">Merhaba gelen **dosya** Visual Studio'da menüsünü **Tümünü Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="46862-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="46862-134">Merhaba itme arka plan bileşeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="46862-134">Create hello Push Background Component</span></span>
<span data-ttu-id="46862-135">Merhaba sonraki adıma toocreate hello itme arka plan bileşendir.</span><span class="sxs-lookup"><span data-stu-id="46862-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="46862-136">Çözüm Gezgini'nde hello çözümün hello en üst düzey düğüme sağ tıklayın (**çözüm SecurePush** bu durumda), ardından **Ekle**, ardından **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="46862-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="46862-137">Genişletme **mağazası uygulamaları**, ardından **Windows Phone uygulamaları**, ardından **Windows çalışma zamanı bileşeni (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="46862-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="46862-138">Ad hello proje **PushBackgroundComponent**ve ardından **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="46862-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="46862-139">Çözüm Gezgini'nde hello sağ **PushBackgroundComponent (Windows Phone 8.1)** proje ve ardından **Ekle**, ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="46862-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="46862-140">Ad hello yeni sınıf **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="46862-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="46862-141">Tıklatın **Ekle** toogenerate hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="46862-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="46862-142">Merhaba Hello tüm içeriğini değiştirin **PushBackgroundComponent** ad alanı tanımını aşağıdaki kod, hello yer tutucu değiştirerek hello ile `{back-end endpoint}` dağıtırken elde hello arka uç uç noktası ile arka uç:</span><span class="sxs-lookup"><span data-stu-id="46862-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="46862-143">Çözüm Gezgini'nde hello sağ **PushBackgroundComponent (Windows Phone 8.1)** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="46862-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="46862-144">Merhaba sol taraftaki tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="46862-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="46862-145">Merhaba, **arama** kutusuna **Http istemcisi**.</span><span class="sxs-lookup"><span data-stu-id="46862-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="46862-146">Merhaba sonuçlar listesinde tıklayın **Microsoft HTTP istemci kitaplıkları**ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="46862-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="46862-147">Merhaba yüklemeyi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="46862-147">Complete hello installation.</span></span>
9. <span data-ttu-id="46862-148">Merhaba NuGet edilene **arama** kutusuna **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="46862-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="46862-149">Merhaba yüklemek **Json.NET** paket sonra Kapat hello NuGet Paket Yöneticisi penceresi.</span><span class="sxs-lookup"><span data-stu-id="46862-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="46862-150">Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **PushBackgroundTask.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="46862-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="46862-151">Çözüm Gezgini'nde, hello **NotifyUserWindowsPhone (Windows Phone 8.1)** projesinde **başvuruları**, ardından **Başvuru Ekle...** . Merhaba başvuru Yöneticisi iletişim kutusunda, hello sonraki çok onay kutusunu**PushBackgroundComponent**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="46862-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="46862-152">Çözüm Gezgini'nde çift tıklayarak **Package.appxmanifest** hello içinde **NotifyUserWindowsPhone (Windows Phone 8.1)** projesi.</span><span class="sxs-lookup"><span data-stu-id="46862-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="46862-153">Altında **bildirimleri**ayarlayın **bildirim özellikli** çok**Evet**.</span><span class="sxs-lookup"><span data-stu-id="46862-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="46862-154">Hala **Package.appxmanifest**, hello tıklatın **bildirimleri** menü hello üstüne yakın.</span><span class="sxs-lookup"><span data-stu-id="46862-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="46862-155">Merhaba, **kullanılabilir bildirimleri** açılan listesinde, tıklatın **arka plan görevleri**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="46862-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="46862-156">İçinde **Package.appxmanifest**altında **özellikleri**, denetleme **anında bildirim**.</span><span class="sxs-lookup"><span data-stu-id="46862-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="46862-157">İçinde **Package.appxmanifest**altında **uygulama ayarları**, türü **PushBackgroundComponent.PushBackgroundTask** hello içinde **giriş noktası** alan.</span><span class="sxs-lookup"><span data-stu-id="46862-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="46862-158">Merhaba gelen **dosya** menüsünde tıklatın **Tümünü Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="46862-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="46862-159">Merhaba uygulama çalıştırın</span><span class="sxs-lookup"><span data-stu-id="46862-159">Run hello Application</span></span>
<span data-ttu-id="46862-160">toorun Merhaba uygulama, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="46862-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="46862-161">Visual Studio'da hello çalıştırmak **AppBackend** Web API uygulaması.</span><span class="sxs-lookup"><span data-stu-id="46862-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="46862-162">Bir ASP.NET web sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="46862-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="46862-163">Visual Studio'da hello çalıştırmak **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone Uygulama.</span><span class="sxs-lookup"><span data-stu-id="46862-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="46862-164">Merhaba Windows Phone öykünücüsü çalışır ve hello uygulamayı otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="46862-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="46862-165">Merhaba, **NotifyUserWindowsPhone** uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="46862-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="46862-166">Bunlar herhangi bir dize olabilir, ancak bunlar olmalıdır hello aynı değeri.</span><span class="sxs-lookup"><span data-stu-id="46862-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="46862-167">Merhaba, **NotifyUserWindowsPhone** uygulama kullanıcı Arabirimi, tıklatın **oturum açma ve kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="46862-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="46862-168">Ardından **Gönder itme**.</span><span class="sxs-lookup"><span data-stu-id="46862-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
