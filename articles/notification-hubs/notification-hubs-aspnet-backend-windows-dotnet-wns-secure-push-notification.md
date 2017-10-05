---
title: "Azure Notification Hubs güvenli bildirme"
description: "Azure'da güvenli anında iletme bildirimleri göndermek öğrenin. .NET API kullanarak C# dilinde yazılan kod örnekleri."
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
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="00749-104">Azure Notification Hubs güvenli bildirme</span><span class="sxs-lookup"><span data-stu-id="00749-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00749-105">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="00749-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="00749-106">iOS</span><span class="sxs-lookup"><span data-stu-id="00749-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="00749-107">Android</span><span class="sxs-lookup"><span data-stu-id="00749-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="00749-108">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="00749-108">Overview</span></span>
<span data-ttu-id="00749-109">Microsoft Azure anında iletme bildirimi desteği, mobil platformlar için tüketici ve kurumsal uygulama için anında iletme bildirimleri uyarlamasını büyük ölçüde basitleştirir bir kullanımı kolay, çok platformlu, ölçeği gönderim altyapısı erişmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="00749-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="00749-110">Yasal nedeniyle veya güvenlik kısıtlamaları, bazen bir uygulama bir şey standart anında iletme bildirimi altyapısı iletilen bildirimi dahil olmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00749-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="00749-111">Bu öğretici, hassas bilgileri istemci cihaz ve uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı aracılığıyla göndererek aynı deneyimi elde etmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="00749-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="00749-112">Yüksek bir düzeyde akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="00749-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="00749-113">Uygulama arka ucu:</span><span class="sxs-lookup"><span data-stu-id="00749-113">The app back-end:</span></span>
   * <span data-ttu-id="00749-114">Arka uç veritabanı güvenli yükünde depolar.</span><span class="sxs-lookup"><span data-stu-id="00749-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="00749-115">Bu bildirim Kimliğini (güvenli hiçbir bilgi gönderilmez) cihaza gönderir.</span><span class="sxs-lookup"><span data-stu-id="00749-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="00749-116">Bildirim alırken cihaza uygulamanın:</span><span class="sxs-lookup"><span data-stu-id="00749-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="00749-117">Cihaz güvenli yükü isteyen arka uç bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="00749-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="00749-118">Uygulama yükü cihaz bildirim olarak gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="00749-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="00749-119">Önceki akış (ve Bu öğreticide), kullanıcı oturum açtığında sonra cihaz kimlik doğrulama belirtecini yerel depoda sakladığı varsayıyoruz olduğunu dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="00749-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="00749-120">Cihaz Bu belirteci kullanarak bildirim 's güvenli yükü alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="00749-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="00749-121">Uygulamanızın kimlik doğrulama belirteçleri cihazda depolamaz veya bu belirteçleri süresi, bildirim alma sırasında cihaz uygulaması uygulamayı başlatmak için kullanıcıdan genel bir bildirim görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="00749-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="00749-122">Uygulama kullanıcının kimliğini doğrular ve bildirim yükü gösterir.</span><span class="sxs-lookup"><span data-stu-id="00749-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="00749-123">Bu güvenli itme öğretici güvenli bir şekilde bir anında iletme bildirimi göndermek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="00749-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="00749-124">Öğretici derlemeler [kullanıcılara bildirme](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) önce bu öğreticide adımları tamamlanmalıdır şekilde öğretici.</span><span class="sxs-lookup"><span data-stu-id="00749-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="00749-125">Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (Windows mağazası) ile çalışmaya başlama](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="00749-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="00749-126">Ayrıca, Windows Phone 8.1 (Windows Phone değil) Windows kimlik bilgileri gerektirir ve arka plan görevleri Windows Phone 8.0 veya Silverlight 8.1 çalışmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="00749-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="00749-127">Windows mağazası uygulamaları için yalnızca uygulama ekran kilitleme etkin ise bir arka plan görevi aracılığıyla bildirimleri alabilirsiniz (Appmanifest, onay kutusuna tıklayın).</span><span class="sxs-lookup"><span data-stu-id="00749-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="00749-128">Windows Phone proje değiştirme</span><span class="sxs-lookup"><span data-stu-id="00749-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="00749-129">İçinde **NotifyUserWindowsPhone** projesi, App.xaml.cs için anında iletme arka plan görevi kaydetmek için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="00749-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="00749-130">Sonuna aşağıdaki kod satırını ekleyin `OnLaunched()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="00749-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="00749-131">Hala App.xaml.cs dosyasında, aşağıdaki ekleyin hemen sonra kod `OnLaunched()` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="00749-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="00749-132">Aşağıdakileri ekleyin `using` deyimleri App.xaml.cs dosyasını üstündeki:</span><span class="sxs-lookup"><span data-stu-id="00749-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="00749-133">Visual Studio'daki **Dosya** menüsünde **Tümünü Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="00749-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="00749-134">Anında iletme arka plan bileşeni oluşturma</span><span class="sxs-lookup"><span data-stu-id="00749-134">Create the Push Background Component</span></span>
<span data-ttu-id="00749-135">Sonraki adım, anında iletme arka plan bileşeni oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="00749-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="00749-136">Çözüm Gezgini'nde çözüme üst düzey düğümünü sağ tıklayın (**çözüm SecurePush** bu durumda), ardından **Ekle**, ardından **yeni proje**.</span><span class="sxs-lookup"><span data-stu-id="00749-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="00749-137">Genişletme **mağazası uygulamaları**, ardından **Windows Phone uygulamaları**, ardından **Windows çalışma zamanı bileşeni (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="00749-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="00749-138">Proje adı **PushBackgroundComponent**ve ardından **Tamam** projesi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="00749-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="00749-139">Çözüm Gezgini'nde sağ **PushBackgroundComponent (Windows Phone 8.1)** proje ve ardından **Ekle**, ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="00749-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="00749-140">Yeni sınıf **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="00749-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="00749-141">Tıklatın **Ekle** sınıfı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="00749-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="00749-142">Tüm içeriğini değiştirin **PushBackgroundComponent** ad alanı tanımını aşağıdaki kodla yer tutucu değiştirerek `{back-end endpoint}` , arka uç dağıtırken elde arka uç uç noktası ile:</span><span class="sxs-lookup"><span data-stu-id="00749-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store the content received from the notification so it can be retrieved from the UI.
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
5. <span data-ttu-id="00749-143">Çözüm Gezgini'nde sağ **PushBackgroundComponent (Windows Phone 8.1)** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="00749-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="00749-144">Sol taraftaki tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="00749-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="00749-145">İçinde **arama** kutusuna **Http istemcisi**.</span><span class="sxs-lookup"><span data-stu-id="00749-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="00749-146">Sonuçlar listesinde tıklatın **Microsoft HTTP istemci kitaplıkları**ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="00749-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="00749-147">Yüklemeyi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="00749-147">Complete the installation.</span></span>
9. <span data-ttu-id="00749-148">NuGet edilene **arama** kutusuna **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="00749-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="00749-149">Yükleme **Json.NET** paketini sonra NuGet Paket Yöneticisi penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="00749-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="00749-150">Aşağıdakileri ekleyin `using` deyimleri en üstündeki **PushBackgroundTask.cs** dosyası:</span><span class="sxs-lookup"><span data-stu-id="00749-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="00749-151">Çözüm Gezgini'nde, içinde **NotifyUserWindowsPhone (Windows Phone 8.1)** projesinde **başvuruları**, ardından **Başvuru Ekle...** .</span><span class="sxs-lookup"><span data-stu-id="00749-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="00749-152">Başvuru Yöneticisi iletişim kutusunda yanındaki kutuyu işaretleyin **PushBackgroundComponent**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="00749-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="00749-153">Çözüm Gezgini'nde çift tıklayarak **Package.appxmanifest** içinde **NotifyUserWindowsPhone (Windows Phone 8.1)** projesi.</span><span class="sxs-lookup"><span data-stu-id="00749-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="00749-154">Altında **bildirimleri**ayarlayın **bildirim özellikli** için **Evet**.</span><span class="sxs-lookup"><span data-stu-id="00749-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="00749-155">Hala **Package.appxmanifest**, tıklatın **bildirimleri** menü üstüne yakın.</span><span class="sxs-lookup"><span data-stu-id="00749-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="00749-156">İçinde **kullanılabilir bildirimleri** açılan listesinde, tıklatın **arka plan görevleri**ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="00749-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="00749-157">İçinde **Package.appxmanifest**altında **özellikleri**, denetleme **anında bildirim**.</span><span class="sxs-lookup"><span data-stu-id="00749-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="00749-158">İçinde **Package.appxmanifest**altında **uygulama ayarları**, türü **PushBackgroundComponent.PushBackgroundTask** içinde **giriş noktası** alan.</span><span class="sxs-lookup"><span data-stu-id="00749-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="00749-159">**Dosya** menüsünden **Tümünü Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="00749-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="00749-160">Uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="00749-160">Run the Application</span></span>
<span data-ttu-id="00749-161">Uygulamayı çalıştırmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="00749-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="00749-162">Visual Studio'da çalıştırın **AppBackend** Web API uygulaması.</span><span class="sxs-lookup"><span data-stu-id="00749-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="00749-163">Bir ASP.NET web sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="00749-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="00749-164">Visual Studio'da çalıştırın **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone Uygulama.</span><span class="sxs-lookup"><span data-stu-id="00749-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="00749-165">Windows Phone öykünücüsü çalışır ve uygulamayı otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="00749-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="00749-166">İçinde **NotifyUserWindowsPhone** uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="00749-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="00749-167">Bunlar herhangi bir dize olabilir, ancak aynı değeri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="00749-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="00749-168">İçinde **NotifyUserWindowsPhone** uygulama kullanıcı Arabirimi, tıklatın **oturum açma ve kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="00749-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="00749-169">Ardından **Gönder itme**.</span><span class="sxs-lookup"><span data-stu-id="00749-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
