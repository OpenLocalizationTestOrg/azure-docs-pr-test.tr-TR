Arka uç projesi türünüzle eşleşen hello yordamı kullanın&mdash;ya da [.NET geri son](#dotnet) veya [Node.js arka ucu](#nodejs).

### <a name="dotnet"></a>.NET arka uç projesi
1. Visual Studio'da hello sunucu projesi sağ tıklayın ve **NuGet paketlerini Yönet**. Arama `Microsoft.Azure.NotificationHubs`ve ardından **yükleme**. Merhaba bildirim hub'ları istemci kitaplığı yükler.
2. Merhaba denetleyicileri klasöründe TodoItemController.cs açın ve hello aşağıdakileri ekleyin `using` deyimleri:

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. Hello yerine `PostTodoItem` koddan hello yöntemiyle:  

        public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
        {
            TodoItem current = await InsertAsync(item);
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

            // Android payload
            var androidNotificationPayload = "{ \"data\" : {\"message\":\"" + item.Text + "\"}}";

            try
            {
                // Send hello push notification and log hello results.
                var result = await hub.SendGcmNativeNotificationAsync(androidNotificationPayload);

                // Write hello success result toohello logs.
                config.Services.GetTraceWriter().Info(result.State.ToString());
            }
            catch (System.Exception ex)
            {
                // Write hello failure result toohello logs.
                config.Services.GetTraceWriter()
                    .Error(ex.Message, null, "Push.SendAsync Error");
            }
            return CreatedAtRoute("Tables", new { id = current.Id }, current);
        }

4. Merhaba sunucu projesi yeniden yayımlayın.

### <a name="nodejs"></a>Node.js arka uç projesi
1. Bunu zaten bunu yapmadıysanız [hello hızlı başlangıç projesi indirme](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), veya başka hello kullan [çevrimiçi Düzenleyicisi'nde hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).
2. Merhaba todoitem.js dosyasındaki var olan kodu Hello hello şununla değiştirin:

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello GCM payload.
        var payload = {
            "data": {
                "message": context.item.text
            }
        };   

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a GCM native notification.
                    context.push.gcm.send(null, payload, function (error) {
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

    Bu, yeni bir Yapılacaklar öğesi eklendiğinde hello item.text içeren bir GCM bildirim gönderir.
3. Yerel bilgisayarınızda Hello dosyasının düzenlenmesi sırasında hello sunucu projesi yeniden yayımlayın.
