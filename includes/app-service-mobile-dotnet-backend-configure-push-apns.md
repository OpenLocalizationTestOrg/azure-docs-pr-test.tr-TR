
* <span data-ttu-id="b46df-101">**.NET arka ucu (C#)**:</span><span class="sxs-lookup"><span data-stu-id="b46df-101">**.NET backend (C#)**:</span></span>      
  
  1. <span data-ttu-id="b46df-102">Visual Studio'da sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**, arama `Microsoft.Azure.NotificationHubs`, ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="b46df-102">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.NotificationHubs`, then click **Install**.</span></span> <span data-ttu-id="b46df-103">Bu arka ucunuzdan bildirim göndermek için Notification Hubs kitaplığı yükler.</span><span class="sxs-lookup"><span data-stu-id="b46df-103">This installs the Notification Hubs library for sending notifications from your backend.</span></span>
  2. <span data-ttu-id="b46df-104">Arka ucun Visual Studio projeyi açın **denetleyicileri** > **TodoItemController.cs**.</span><span class="sxs-lookup"><span data-stu-id="b46df-104">In the backend's Visual Studio project, open **Controllers** > **TodoItemController.cs**.</span></span> <span data-ttu-id="b46df-105">Dosyanın üst kısmında, aşağıdaki ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="b46df-105">At the top of the file, add the following `using` statement:</span></span>
     
          using Microsoft.Azure.Mobile.Server.Config;
          using Microsoft.Azure.NotificationHubs;

    3. <span data-ttu-id="b46df-106">Değiştir `PostTodoItem` aşağıdaki kod ile yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b46df-106">Replace the `PostTodoItem` method with the following code:</span></span>  

            public async Task<IHttpActionResult> PostTodoItem(TodoItem item)
            {
                TodoItem current = await InsertAsync(item);
                // Get the settings for the server project.
                HttpConfiguration config = this.Configuration;

                MobileAppSettingsDictionary settings = 
                    this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

                // Get the Notification Hubs credentials for the Mobile App.
                string notificationHubName = settings.NotificationHubName;
                string notificationHubConnection = settings
                    .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

                // Create a new Notification Hub client.
                NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

                // iOS payload
                var appleNotificationPayload = "{\"aps\":{\"alert\":\"" + item.Text + "\"}}";

                try
                {
                    // Send the push notification and log the results.
                    var result = await hub.SendAppleNativeNotificationAsync(appleNotificationPayload);

                    // Write the success result to the logs.
                    config.Services.GetTraceWriter().Info(result.State.ToString());
                }
                catch (System.Exception ex)
                {
                    // Write the failure result to the logs.
                    config.Services.GetTraceWriter()
                        .Error(ex.Message, null, "Push.SendAsync Error");
                }
                return CreatedAtRoute("Tables", new { id = current.Id }, current);
            }

    4. <span data-ttu-id="b46df-107">Sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="b46df-107">Republish the server project.</span></span>

* <span data-ttu-id="b46df-108">**Node.js arka ucu** :</span><span class="sxs-lookup"><span data-stu-id="b46df-108">**Node.js backend** :</span></span> 
  
  1. <span data-ttu-id="b46df-109">Bunu zaten bunu yapmadıysanız [hızlı başlangıç projesi indirme](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) veya başka kullanım [Azure portalında çevrimiçi düzenleyicisini](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="b46df-109">If you haven't already done so, [download the quickstart project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>    
  2. <span data-ttu-id="b46df-110">Todoitem.js tablo betik aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b46df-110">Replace the todoitem.js table script with the following code:</span></span>

            var azureMobileApps = require('azure-mobile-apps'),
                promises = require('azure-mobile-apps/src/utilities/promises'),
                logger = require('azure-mobile-apps/src/logger');

            var table = azureMobileApps.table();

            // When adding record, send a push notification via APNS
            table.insert(function (context) {
                // For details of the Notification Hubs JavaScript SDK, 
                // see http://aka.ms/nodejshubs
                logger.info('Running TodoItem.insert');

                // Create a payload that contains the new item Text.
                var payload = "{\"aps\":{\"alert\":\"" + context.item.text + "\"}}";

                // Execute the insert; Push as a post-execute action when results are returned as a Promise.
                return context.execute()
                    .then(function (results) {
                        // Only do the push if configured
                        if (context.push) {
                            context.push.apns.send(null, payload, function (error) {
                                if (error) {
                                    logger.error('Error while sending push notification: ', error);
                                } else {
                                    logger.info('Push notification sent successfully!');
                                }
                            });
                        }
                        return results;
                    })
                    .catch(function (error) {
                        logger.error('Error while running context.execute: ', error);
                    });
            });

            module.exports = table;

    2. <span data-ttu-id="b46df-111">Yerel bilgisayarınızda dosyayı düzenlerken, sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="b46df-111">When editing the file on your local computer, republish the server project.</span></span>
