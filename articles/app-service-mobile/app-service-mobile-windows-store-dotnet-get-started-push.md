---
title: "Evrensel Windows Platformu (UWP) uygulamanıza anında iletme bildirimleri ekleme | Microsoft Docs"
description: "Evrensel Windows Platformu (UWP) uygulamanıza anında iletme bildirimleri göndermek için Azure App Service Mobile Apps ve Azure bildirim hub'ları kullanmayı öğrenin."
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
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="fde48-103">Windows uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fde48-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="fde48-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="fde48-104">Overview</span></span>
<span data-ttu-id="fde48-105">Bu öğreticide, anında iletme bildirimleri ekleme [Windows Hızlı Başlangıç](app-service-mobile-windows-store-dotnet-get-started.md) proje böylece bir kayda eklenen her zaman bir anında iletme bildirimi cihaza gönderilir.</span><span class="sxs-lookup"><span data-stu-id="fde48-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="fde48-106">İndirilen hızlı başlangıç sunucu projesi kullanmazsanız, anında iletme bildirimi uzantısı paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde48-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="fde48-107">Bkz: [.NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fde48-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="fde48-108"><a name="configure-hub"></a>Bildirim hub'ı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fde48-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="fde48-109">Anında iletme bildirimleri için uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="fde48-109">Register your app for push notifications</span></span>
<span data-ttu-id="fde48-110">Uygulamanızı Windows Mağazası'na gönderin ve ardından Windows Bildirim Hizmetleri (anında iletme göndermek için WNS ile) tümleştirmek için sunucu projenizi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde48-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="fde48-111">UWP uygulaması projesini Visual Studio Çözüm Gezgini'nde sağ tıklayın, **deposu** > **uygulamayı mağaza ile ilişkilendir...** .</span><span class="sxs-lookup"><span data-stu-id="fde48-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![Uygulamayı Windows mağazası ile ilişkilendirme](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="fde48-113">Sihirbazı'nda tıklatın **sonraki**, Microsoft hesabınızla oturum açın, uygulamanız için bir ad yazın **yeni bir uygulama adı yedek**, ardından **ayırma**.</span><span class="sxs-lookup"><span data-stu-id="fde48-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="fde48-114">Uygulama kaydı başarıyla oluşturulduktan sonra yeni uygulama adı seçin, **sonraki**ve ardından **ilişkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="fde48-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="fde48-115">Bu, uygulama bildirimine gerekli Windows Mağazası kayıt bilgilerini ekler.</span><span class="sxs-lookup"><span data-stu-id="fde48-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="fde48-116">Gidin [Windows Geliştirme Merkezi](https://dev.windows.com/en-us/overview), oturum açma Microsoft hesabınızla, yeni uygulama kaydında tıklatın **uygulamalarım**, ardından **Hizmetleri**  >   **Anında iletme bildirimleri**.</span><span class="sxs-lookup"><span data-stu-id="fde48-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="fde48-117">İçinde **anında iletme bildirimleri** sayfasında, **Live Services sitesi** altında **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="fde48-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="fde48-118">Kayıt sayfanın altında bulunan değerini not **uygulama parolaları** ve **paket SID'si**, sonraki, mobil uygulamanızın arka ucuna yapılandırmak için kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="fde48-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![Uygulamayı Windows mağazası ile ilişkilendirme](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="fde48-120">Gizli anahtar ve paket SID'si önemli güvenlik kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="fde48-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="fde48-121">Bu değerleri kimseyle paylaşmayın veya uygulamanızla birlikte dağıtmayın.</span><span class="sxs-lookup"><span data-stu-id="fde48-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="fde48-122">**Uygulama kimliği** gizli anahtarı ile Microsoft Account kimlik doğrulamasını yapılandırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fde48-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="fde48-123">Anında iletme bildirimleri göndermek için arka uç yapılandırın</span><span class="sxs-lookup"><span data-stu-id="fde48-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="fde48-124"><a id="update-service"></a>Anında iletme bildirimleri göndermek için sunucusunu güncelleştir</span><span class="sxs-lookup"><span data-stu-id="fde48-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="fde48-125">Arka uç projesi türünüzle eşleşen aşağıdaki yordamı kullanın&mdash;ya da [.NET arka ucu](#dotnet) veya [Node.js arka ucu](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="fde48-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="fde48-126"><a name="dotnet"></a>.NET arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="fde48-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="fde48-127">Visual Studio'da sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**, Microsoft.Azure.NotificationHubs için arama yapın ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="fde48-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="fde48-128">Bu, bildirim hub'ları istemci kitaplığı yükler.</span><span class="sxs-lookup"><span data-stu-id="fde48-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="fde48-129">Genişletin **denetleyicileri**TodoItemController.cs açın ve aşağıdaki using deyimlerini:</span><span class="sxs-lookup"><span data-stu-id="fde48-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="fde48-130">İçinde **PostTodoItem** yöntemini çağırdıktan sonra aşağıdaki kodu ekleyin **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="fde48-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="fde48-131">Bu kod, yeni bir öğe ekleme tamamlandıktan sonra bir anında iletme bildirimi göndermek için bildirim hub'ı söyler.</span><span class="sxs-lookup"><span data-stu-id="fde48-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="fde48-132">Sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="fde48-132">Republish the server project.</span></span>

### <span data-ttu-id="fde48-133"><a name="nodejs"></a>Node.js arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="fde48-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="fde48-134">Bunu zaten bunu yapmadıysanız [hızlı başlangıç projesi indirme](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) veya başka kullanım [Azure portalında çevrimiçi düzenleyicisini](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="fde48-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="fde48-135">Todoitem.js dosyasındaki var olan kodu aşağıdakilerle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="fde48-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="fde48-136">Bu, yeni bir Yapılacaklar öğesi eklendiğinde item.text içeren WNS bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="fde48-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="fde48-137">Yerel bilgisayarınızda dosyayı düzenlerken, sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="fde48-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="fde48-138"><a id="update-app"></a>Uygulamanıza anında iletme bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="fde48-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="fde48-139">Ardından, uygulamanızı anında iletme bildirimleri başlatma üzerinde için kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fde48-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="fde48-140">Kimlik doğrulaması zaten etkinleştirdiyseniz, kullanıcı için anında iletme bildirimleri kaydetmeyi denemeden önce oturum açtığında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fde48-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="fde48-141">Açık **App.xaml.cs** proje dosyası ve aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="fde48-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="fde48-142">Aynı dosyada aşağıdakileri ekleyin **Initnotificationsasync** yöntemi tanımına **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="fde48-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="fde48-143">Bu kod, WNS'den uygulamanın ChannelURI alır ve ardından bu ChannelURI, mobil uygulama hizmeti ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="fde48-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="fde48-144">Üstündeki **OnLaunched** olay işleyicisini **App.xaml.cs**, ekleme **zaman uyumsuz** değiştirici yöntem tanımına ve yeni aşağıdaki çağrıyı ekleyin  **Initnotificationsasync** aşağıdaki örnekteki gibi yöntemi:</span><span class="sxs-lookup"><span data-stu-id="fde48-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="fde48-145">Bu kısa süreli ChannelURI uygulama başlatılan her zaman kayıtlı olduğunu güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="fde48-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="fde48-146">UWP uygulama projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="fde48-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="fde48-147">Uygulamanız şimdi bildirim almaya hazırdır.</span><span class="sxs-lookup"><span data-stu-id="fde48-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="fde48-148"><a id="test"></a>Test, uygulamanızda anında iletme bildirimleri</span><span class="sxs-lookup"><span data-stu-id="fde48-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="fde48-149"><a id="more"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fde48-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="fde48-150">Anında iletme bildirimleri hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="fde48-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="fde48-151">Azure Mobile Apps için yönetilen istemciyi kullanma</span><span class="sxs-lookup"><span data-stu-id="fde48-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="fde48-152">Şablonları platformlar arası gönderim ve yerelleştirilmiş bildirim göndermek için esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="fde48-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="fde48-153">Şablonlarını kaydetmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fde48-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="fde48-154">Anında iletme bildirimi sorunlarını tanılamak</span><span class="sxs-lookup"><span data-stu-id="fde48-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="fde48-155">Neden bildirimleri bırakılan veya cihazlarda bitmeyen çeşitli nedenleri vardır.</span><span class="sxs-lookup"><span data-stu-id="fde48-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="fde48-156">Bu konuda çözümlemek ve anında iletme bildirimi hataları kök nedenini anlamak nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fde48-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="fde48-157">Aşağıdaki öğreticiler birini açın etmeden göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="fde48-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="fde48-158">Uygulamanıza kimlik doğrulaması ekleme</span><span class="sxs-lookup"><span data-stu-id="fde48-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="fde48-159">Uygulamanızdaki kullanıcıların kimliklerini bir kimlik sağlayıcısı ile nasıl doğrulayacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fde48-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="fde48-160">Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fde48-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="fde48-161">Mobil Uygulama arka ucu kullanarak uygulamanıza çevrimdışı destek eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="fde48-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="fde48-162">Çevrimdışı eşitleme son kullanıcıların, ağ bağlantısı yokken dahi, mobil uygulama ile etkileşim kurmalarına &mdash;veri görüntüleme, ekleme ya da değiştirme&mdash; olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fde48-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
