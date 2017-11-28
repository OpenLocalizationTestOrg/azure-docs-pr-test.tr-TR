---
title: "aaaAdd anında iletme bildirimleri tooyour Evrensel Windows Platformu (UWP) uygulamasını | Microsoft Docs"
description: "Azure App Service Mobile Apps toouse ve Azure Notification Hubs toosend bildirimleri tooyour Evrensel Windows Platformu (UWP) uygulamasını nasıl anında bilgi alın."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="4760d-103">Anında iletme bildirimleri tooyour Windows uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="4760d-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="4760d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4760d-104">Overview</span></span>
<span data-ttu-id="4760d-105">Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Windows Hızlı Başlangıç](app-service-mobile-windows-store-dotnet-get-started.md) bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.</span><span class="sxs-lookup"><span data-stu-id="4760d-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="4760d-106">Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello.</span><span class="sxs-lookup"><span data-stu-id="4760d-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="4760d-107">Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4760d-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="4760d-108"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4760d-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="4760d-109">Anında iletme bildirimleri için uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="4760d-109">Register your app for push notifications</span></span>
<span data-ttu-id="4760d-110">Windows mağazası, app toohello toosubmit gerekir, sonra Windows Bildirim Hizmetleri (WNS) toosend itme sunucu projesi toointegrate yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4760d-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="4760d-111">Visual Studio Çözüm Gezgini'nde sağ hello UWP uygulaması projesi tıklatın **deposu** > **uygulamayı hello mağaza ile ilişkilendir...** .</span><span class="sxs-lookup"><span data-stu-id="4760d-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Uygulamayı Windows mağazası ile ilişkilendirme](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="4760d-113">Başlangıç Sihirbazı'nda tıklatın **sonraki**, Microsoft hesabınızla oturum açın, uygulamanız için bir ad yazın **yeni bir uygulama adı yedek**, ardından **ayırma**.</span><span class="sxs-lookup"><span data-stu-id="4760d-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="4760d-114">Merhaba uygulama kaydı başarıyla oluşturuldu, select hello yeni uygulama adı sonra tıklatın **sonraki**ve ardından **ilişkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="4760d-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="4760d-115">Bu gerekli hello Windows mağazası kayıt bilgilerini toohello uygulama bildirimi ekler.</span><span class="sxs-lookup"><span data-stu-id="4760d-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="4760d-116">Toohello gidin [Windows Geliştirme Merkezi](https://dev.windows.com/en-us/overview), oturum açma Microsoft hesabınızla, hello yeni uygulama kaydında tıklatın **uygulamalarım**, ardından **Hizmetleri**  >  **Anında iletme bildirimleri**.</span><span class="sxs-lookup"><span data-stu-id="4760d-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="4760d-117">Merhaba, **anında iletme bildirimleri** sayfasında, **Live Services sitesi** altında **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="4760d-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="4760d-118">Merhaba kayıt sayfası altındaki hello değeri Not **uygulama parolaları** ve hello **paket SID'si**, hangi, mobil uygulamanızın arka ucuna tooconfigure sonraki kullanır.</span><span class="sxs-lookup"><span data-stu-id="4760d-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Uygulamayı Windows mağazası ile ilişkilendirme](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="4760d-120">Merhaba istemci parolası ve paket SID'si önemli güvenlik kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="4760d-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="4760d-121">Bu değerleri kimseyle paylaşmayın veya uygulamanızla birlikte dağıtmayın.</span><span class="sxs-lookup"><span data-stu-id="4760d-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="4760d-122">Merhaba **uygulama kimliği** hello gizli tooconfigure Microsoft Account ile kimlik doğrulaması kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4760d-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="4760d-123">Merhaba arka uç toosend anında iletme bildirimleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4760d-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="4760d-124"><a id="update-service"></a>Güncelleştirme Hello sunucu toosend anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="4760d-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="4760d-125">Arka uç projesi türünüzle eşleşen hello aşağıdaki yordamı kullanın&mdash;ya da [.NET arka ucu](#dotnet) veya [Node.js arka ucu](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="4760d-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="4760d-126"><a name="dotnet"></a>.NET arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="4760d-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="4760d-127">Visual Studio'da hello sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**, Microsoft.Azure.NotificationHubs için arama yapın ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="4760d-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="4760d-128">Merhaba bildirim hub'ları istemci kitaplığı yükler.</span><span class="sxs-lookup"><span data-stu-id="4760d-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="4760d-129">Genişletin **denetleyicileri**TodoItemController.cs açın ve hello aşağıdaki using deyimleri:</span><span class="sxs-lookup"><span data-stu-id="4760d-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="4760d-130">Merhaba, **PostTodoItem** yöntemi, hello çağrısından sonra çok koddan hello eklemek**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="4760d-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="4760d-131">Yeni bir öğe ekleme sonra bu kodu bir anında iletme bildirimi hello bildirim hub'ı toosend söyler.</span><span class="sxs-lookup"><span data-stu-id="4760d-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="4760d-132">Merhaba sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="4760d-132">Republish hello server project.</span></span>

### <span data-ttu-id="4760d-133"><a name="nodejs"></a>Node.js arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="4760d-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="4760d-134">Bunu zaten bunu yapmadıysanız [hello hızlı başlangıç projesi indirme](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) veya başka hello kullan [çevrimiçi Düzenleyicisi'nde hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="4760d-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="4760d-135">Merhaba todoitem.js dosyasındaki var olan kodu Hello hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4760d-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="4760d-136">Bu, yeni bir Yapılacaklar öğesi eklendiğinde hello item.text içeren WNS bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="4760d-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="4760d-137">Yerel bilgisayarınızda Hello dosyasının düzenlenmesi sırasında hello sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="4760d-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="4760d-138"><a id="update-app"></a>Anında iletme bildirimleri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="4760d-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="4760d-139">Ardından, uygulamanızı anında iletme bildirimleri başlatma üzerinde için kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4760d-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="4760d-140">Kimlik doğrulaması zaten etkinleştirdiyseniz, bu hello kullanıcı anında iletme bildirimleri için tooregister denemeden önce oturum açtığında emin olun.</span><span class="sxs-lookup"><span data-stu-id="4760d-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="4760d-141">Açık hello **App.xaml.cs** proje dosyası ve hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="4760d-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="4760d-142">Buna Merhaba aynı dosya, hello aşağıdakileri ekleyin **Initnotificationsasync** yöntemi tanımı toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="4760d-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="4760d-143">Bu kod WNS'den hello ChannelURI hello uygulamasının alır ve ardından bu ChannelURI, mobil uygulama hizmeti ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4760d-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="4760d-144">Merhaba hello üstündeki **OnLaunched** olay işleyicisini **App.xaml.cs**, hello eklemek **zaman uyumsuz** değiştiricisi toohello yöntem tanımını ve hello aşağıdaki çağrı toohello yeni ekleyin **Initnotificationsasync** yönteminizdeki aşağıdaki örneğine hello:</span><span class="sxs-lookup"><span data-stu-id="4760d-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="4760d-145">Bu kısa süreli ChannelURI Merhaba uygulaması başlatılan her zaman kayıtlı bu hello güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="4760d-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="4760d-146">UWP uygulama projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="4760d-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="4760d-147">Uygulamanızı hazır tooreceive bildirimleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="4760d-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="4760d-148"><a id="test"></a>Test, uygulamanızda anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="4760d-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="4760d-149"><a id="more"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4760d-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="4760d-150">Anında iletme bildirimleri hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="4760d-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="4760d-151">Nasıl toouse hello Azure Mobile Apps için yönetilen</span><span class="sxs-lookup"><span data-stu-id="4760d-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="4760d-152">Şablonları esneklik toosend platformlar arası gönderim ve yerelleştirilmiş iter verin.</span><span class="sxs-lookup"><span data-stu-id="4760d-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="4760d-153">Bilgi nasıl tooregister şablonları.</span><span class="sxs-lookup"><span data-stu-id="4760d-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="4760d-154">Anında iletme bildirimi sorunlarını tanılamak</span><span class="sxs-lookup"><span data-stu-id="4760d-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="4760d-155">Neden bildirimleri bırakılan veya cihazlarda bitmeyen çeşitli nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="4760d-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="4760d-156">Bu konu nasıl anında iletme bildirimi hatalarının tooanalyze ve Şekil hello kök çıkışı neden gösterir.</span><span class="sxs-lookup"><span data-stu-id="4760d-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="4760d-157">Öğreticiler aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4760d-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="4760d-158">Kimlik doğrulama tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="4760d-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="4760d-159">Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="4760d-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="4760d-160">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="4760d-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="4760d-161">Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="4760d-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="4760d-162">Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.</span><span class="sxs-lookup"><span data-stu-id="4760d-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
