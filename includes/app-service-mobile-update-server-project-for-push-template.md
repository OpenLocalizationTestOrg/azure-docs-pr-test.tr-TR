Yeni bir öğe eklenen her zaman bu bölümde, kod, mevcut Mobile Apps arka uç projesi toosend içinde bir anında iletme bildirimi güncelleştirin. Bu hello tarafından destekleniyor [şablonu](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) Azure Notification Hubs, platformlar arası iter etkinleştirme özelliğidir. Merhaba çeşitli istemcilere şablonları kullanarak anında iletme bildirimleri için kaydedilir ve tek bir evrensel itme tooall istemci platformları elde edebilirsiniz.

Arka uç projesi türünüzle eşleşen yordamları izleyerek hello birini&mdash;ya da [.NET geri son](#dotnet) veya [Node.js arka ucu](#nodejs).

### <a name="dotnet"></a>.NET arka uç projesi
1. Visual Studio'da hello sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**. Arama `Microsoft.Azure.NotificationHubs`ve ardından **yükleme**. Bu arka ucunuzdan bildirim göndermek için Notification Hubs kitaplığı hello yükler.
2. Merhaba sunucu projeyi açın **denetleyicileri** > **TodoItemController.cs**ve hello aşağıdakileri ekleyin using deyimleri:

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

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
        .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Sending hello message so that all template registrations that contain "messageParam"
        // will receive hello notifications. This includes APNS, GCM, WNS, and MPNS template registrations.
        Dictionary<string,string> templateParams = new Dictionary<string,string>();
        templateParams["messageParam"] = item.Text + " was added toohello list.";

        try
        {
            // Send hello push notification and log hello results.
            var result = await hub.SendTemplateNotificationAsync(templateParams);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    Merhaba öğeyi içeren bir şablon bildirim gönderir. Yeni bir öğe eklendiğinde, metin.
4. Merhaba sunucu projesi yeniden yayımlayın.

### <a name="nodejs"></a>Node.js arka uç projesi
1. Bunu zaten bunu yapmadıysanız [hello hızlı başlangıç arka uç projesi indirme](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), veya başka hello kullan [çevrimiçi Düzenleyicisi'nde hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Merhaba todoitem.js var olan kodda hello şununla değiştirin:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello template payload.
        var payload = '{"messageParam": "' + context.item.text + '" }';  

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a template notification.
                    context.push.send(null, payload, function (error) {
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

    Bu, yeni bir öğe eklendiğinde hello item.text içeren bir şablon bildirim gönderir.
3. Yerel bilgisayarınızda Hello dosyasının düzenlenmesi sırasında hello sunucu projesi yeniden yayımlayın.
