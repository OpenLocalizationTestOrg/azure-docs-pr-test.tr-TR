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
# <a name="add-push-notifications-tooyour-windows-app"></a>Anında iletme bildirimleri tooyour Windows uygulaması Ekle
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, eklediğiniz anında iletme bildirimleri toohello [Windows Hızlı Başlangıç](app-service-mobile-windows-store-dotnet-get-started.md) bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen böylece proje.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello. Bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) daha fazla bilgi için.

## <a name="configure-hub"></a>Bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a>Anında iletme bildirimleri için uygulamanızı kaydetme
Windows mağazası, app toohello toosubmit gerekir, sonra Windows Bildirim Hizmetleri (WNS) toosend itme sunucu projesi toointegrate yapılandırın.

1. Visual Studio Çözüm Gezgini'nde sağ hello UWP uygulaması projesi tıklatın **deposu** > **uygulamayı hello mağaza ile ilişkilendir...** .

    ![Uygulamayı Windows mağazası ile ilişkilendirme](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. Başlangıç Sihirbazı'nda tıklatın **sonraki**, Microsoft hesabınızla oturum açın, uygulamanız için bir ad yazın **yeni bir uygulama adı yedek**, ardından **ayırma**.
3. Merhaba uygulama kaydı başarıyla oluşturuldu, select hello yeni uygulama adı sonra tıklatın **sonraki**ve ardından **ilişkilendirmek**. Bu gerekli hello Windows mağazası kayıt bilgilerini toohello uygulama bildirimi ekler.  
4. Toohello gidin [Windows Geliştirme Merkezi](https://dev.windows.com/en-us/overview), oturum açma Microsoft hesabınızla, hello yeni uygulama kaydında tıklatın **uygulamalarım**, ardından **Hizmetleri**  >  **Anında iletme bildirimleri**.
5. Merhaba, **anında iletme bildirimleri** sayfasında, **Live Services sitesi** altında **Microsoft Azure Mobile Services**.
6. Merhaba kayıt sayfası altındaki hello değeri Not **uygulama parolaları** ve hello **paket SID'si**, hangi, mobil uygulamanızın arka ucuna tooconfigure sonraki kullanır.

    ![Uygulamayı Windows mağazası ile ilişkilendirme](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > Merhaba istemci parolası ve paket SID'si önemli güvenlik kimlik bilgileridir. Bu değerleri kimseyle paylaşmayın veya uygulamanızla birlikte dağıtmayın. Merhaba **uygulama kimliği** hello gizli tooconfigure Microsoft Account ile kimlik doğrulaması kullanılır.
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a>Merhaba arka uç toosend anında iletme bildirimleri yapılandırma
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <a id="update-service"></a>Güncelleştirme Hello sunucu toosend anında iletme bildirimleri
Arka uç projesi türünüzle eşleşen hello aşağıdaki yordamı kullanın&mdash;ya da [.NET arka ucu](#dotnet) veya [Node.js arka ucu](#nodejs).

### <a name="dotnet"></a>.NET arka uç projesi
1. Visual Studio'da hello sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**, Microsoft.Azure.NotificationHubs için arama yapın ve ardından **yükleme**. Merhaba bildirim hub'ları istemci kitaplığı yükler.
2. Genişletin **denetleyicileri**TodoItemController.cs açın ve hello aşağıdaki using deyimleri:

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. Merhaba, **PostTodoItem** yöntemi, hello çağrısından sonra çok koddan hello eklemek**InsertAsync**:

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

    Yeni bir öğe ekleme sonra bu kodu bir anında iletme bildirimi hello bildirim hub'ı toosend söyler.
4. Merhaba sunucu projesi yeniden yayımlayın.

### <a name="nodejs"></a>Node.js arka uç projesi
1. Bunu zaten bunu yapmadıysanız [hello hızlı başlangıç projesi indirme](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) veya başka hello kullan [çevrimiçi Düzenleyicisi'nde hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Merhaba todoitem.js dosyasındaki var olan kodu Hello hello şununla değiştirin:

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

    Bu, yeni bir Yapılacaklar öğesi eklendiğinde hello item.text içeren WNS bildirim gönderir.
3. Yerel bilgisayarınızda Hello dosyasının düzenlenmesi sırasında hello sunucu projesi yeniden yayımlayın.

## <a id="update-app"></a>Anında iletme bildirimleri tooyour uygulama Ekle
Ardından, uygulamanızı anında iletme bildirimleri başlatma üzerinde için kaydetmeniz gerekir. Kimlik doğrulaması zaten etkinleştirdiyseniz, bu hello kullanıcı anında iletme bildirimleri için tooregister denemeden önce oturum açtığında emin olun.

1. Açık hello **App.xaml.cs** proje dosyası ve hello aşağıdakileri ekleyin `using` deyimleri:

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. Buna Merhaba aynı dosya, hello aşağıdakileri ekleyin **Initnotificationsasync** yöntemi tanımı toohello **uygulama** sınıfı:

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    Bu kod WNS'den hello ChannelURI hello uygulamasının alır ve ardından bu ChannelURI, mobil uygulama hizmeti ile kaydeder.
3. Merhaba hello üstündeki **OnLaunched** olay işleyicisini **App.xaml.cs**, hello eklemek **zaman uyumsuz** değiştiricisi toohello yöntem tanımını ve hello aşağıdaki çağrı toohello yeni ekleyin **Initnotificationsasync** yönteminizdeki aşağıdaki örneğine hello:

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    Bu kısa süreli ChannelURI Merhaba uygulaması başlatılan her zaman kayıtlı bu hello güvence altına alır.
4. UWP uygulama projenizi yeniden derleyin. Uygulamanızı hazır tooreceive bildirimleri sunulmuştur.

## <a id="test"></a>Test, uygulamanızda anında iletme bildirimleri
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <a id="more"></a>Sonraki adımlar
Anında iletme bildirimleri hakkında daha fazla bilgi edinin:

* [Nasıl toouse hello Azure Mobile Apps için yönetilen](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  Şablonları esneklik toosend platformlar arası gönderim ve yerelleştirilmiş iter verin. Bilgi nasıl tooregister şablonları.
* [Anında iletme bildirimi sorunlarını tanılamak](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  Neden bildirimleri bırakılan veya cihazlarda bitmeyen çeşitli nedenleri vardır. Bu konu nasıl anında iletme bildirimi hatalarının tooanalyze ve Şekil hello kök çıkışı neden gösterir.

Öğreticiler aşağıdaki hello tooone üzerinde etmeden göz önünde bulundurun:

* [Kimlik doğrulama tooyour uygulama Ekle](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Bilgi nasıl bir kimlik sağlayıcısı ile uygulamanızın tooauthenticate kullanıcılar.
* [Uygulamanız için çevrimdışı eşitlemeyi etkinleştirme](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Bir mobil uygulama arka ucu kullanarak uygulamanıza çevrimdışı tooadd destek nasıl bilgi edinin. Çevrimdışı eşitleme sağlayan bir mobil uygulama ile son kullanıcılar toointeract&mdash;görüntüleme, ekleme veya değiştirme veri&mdash;hiçbir ağ bağlantısı olduğunda bile.

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
