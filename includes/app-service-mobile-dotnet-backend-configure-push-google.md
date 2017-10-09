<span data-ttu-id="963f2-101">Arka uç projesi türünüzle eşleşen hello yordamı kullanın&mdash;ya da [.NET geri son](#dotnet) veya [Node.js arka ucu](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="963f2-101">Use hello procedure that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="963f2-102"><a name="dotnet"></a>.NET arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="963f2-102"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="963f2-103">Visual Studio'da hello sunucu projesi sağ tıklayın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="963f2-103">In Visual Studio, right-click hello server project, and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="963f2-104">Arama `Microsoft.Azure.NotificationHubs`ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="963f2-104">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="963f2-105">Merhaba bildirim hub'ları istemci kitaplığı yükler.</span><span class="sxs-lookup"><span data-stu-id="963f2-105">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="963f2-106">Merhaba denetleyicileri klasöründe TodoItemController.cs açın ve hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="963f2-106">In hello Controllers folder, open TodoItemController.cs and add hello following `using` statements:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
        using Microsoft.Azure.NotificationHubs;
3. <span data-ttu-id="963f2-107">Hello yerine `PostTodoItem` koddan hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="963f2-107">Replace hello `PostTodoItem` method with hello following code:</span></span>  

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

4. <span data-ttu-id="963f2-108">Merhaba sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="963f2-108">Republish hello server project.</span></span>

### <span data-ttu-id="963f2-109"><a name="nodejs"></a>Node.js arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="963f2-109"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="963f2-110">Bunu zaten bunu yapmadıysanız [hello hızlı başlangıç projesi indirme](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), veya başka hello kullan [çevrimiçi Düzenleyicisi'nde hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="963f2-110">If you haven't already done so, [download hello quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="963f2-111">Merhaba todoitem.js dosyasındaki var olan kodu Hello hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="963f2-111">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

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

    <span data-ttu-id="963f2-112">Bu, yeni bir Yapılacaklar öğesi eklendiğinde hello item.text içeren bir GCM bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="963f2-112">This sends a GCM notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="963f2-113">Yerel bilgisayarınızda Hello dosyasının düzenlenmesi sırasında hello sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="963f2-113">When editing hello file in your local computer, republish hello server project.</span></span>
