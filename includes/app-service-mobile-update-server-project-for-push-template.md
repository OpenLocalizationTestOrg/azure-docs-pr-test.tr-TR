<span data-ttu-id="9f04b-101">Yeni bir öğe eklenen her zaman bu bölümde, kod, mevcut Mobile Apps arka uç projesi toosend içinde bir anında iletme bildirimi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9f04b-101">In this section, you update code in your existing Mobile Apps back-end project toosend a push notification every time a new item is added.</span></span> <span data-ttu-id="9f04b-102">Bu hello tarafından destekleniyor [şablonu](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) Azure Notification Hubs, platformlar arası iter etkinleştirme özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="9f04b-102">This is powered by hello [template](../articles/notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs, enabling cross-platform pushes.</span></span> <span data-ttu-id="9f04b-103">Merhaba çeşitli istemcilere şablonları kullanarak anında iletme bildirimleri için kaydedilir ve tek bir evrensel itme tooall istemci platformları elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f04b-103">hello various clients are registered for push notifications using templates, and a single universal push can get tooall client platforms.</span></span>

<span data-ttu-id="9f04b-104">Arka uç projesi türünüzle eşleşen yordamları izleyerek hello birini&mdash;ya da [.NET geri son](#dotnet) veya [Node.js arka ucu](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="9f04b-104">Choose one of hello following procedures that matches your back-end project type&mdash;either [.NET back end](#dotnet) or [Node.js back end](#nodejs).</span></span>

### <span data-ttu-id="9f04b-105"><a name="dotnet"></a>.NET arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="9f04b-105"><a name="dotnet"></a>.NET back-end project</span></span>
1. <span data-ttu-id="9f04b-106">Visual Studio'da hello sunucu projesi sağ tıklatın ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9f04b-106">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**.</span></span> <span data-ttu-id="9f04b-107">Arama `Microsoft.Azure.NotificationHubs`ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="9f04b-107">Search for `Microsoft.Azure.NotificationHubs`, and then click **Install**.</span></span> <span data-ttu-id="9f04b-108">Bu arka ucunuzdan bildirim göndermek için Notification Hubs kitaplığı hello yükler.</span><span class="sxs-lookup"><span data-stu-id="9f04b-108">This installs hello Notification Hubs library for sending notifications from your back end.</span></span>
2. <span data-ttu-id="9f04b-109">Merhaba sunucu projeyi açın **denetleyicileri** > **TodoItemController.cs**ve hello aşağıdakileri ekleyin using deyimleri:</span><span class="sxs-lookup"><span data-stu-id="9f04b-109">In hello server project, open **Controllers** > **TodoItemController.cs**, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="9f04b-110">Merhaba, **PostTodoItem** yöntemi, hello çağrısından sonra çok koddan hello eklemek**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="9f04b-110">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>  

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

    <span data-ttu-id="9f04b-111">Merhaba öğeyi içeren bir şablon bildirim gönderir. Yeni bir öğe eklendiğinde, metin.</span><span class="sxs-lookup"><span data-stu-id="9f04b-111">This sends a template notification that contains hello item.Text when a new item is inserted.</span></span>
4. <span data-ttu-id="9f04b-112">Merhaba sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="9f04b-112">Republish hello server project.</span></span>

### <span data-ttu-id="9f04b-113"><a name="nodejs"></a>Node.js arka uç projesi</span><span class="sxs-lookup"><span data-stu-id="9f04b-113"><a name="nodejs"></a>Node.js back-end project</span></span>
1. <span data-ttu-id="9f04b-114">Bunu zaten bunu yapmadıysanız [hello hızlı başlangıç arka uç projesi indirme](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), veya başka hello kullan [çevrimiçi Düzenleyicisi'nde hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="9f04b-114">If you haven't already done so, [download hello quickstart back-end project](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart), or else use hello [online editor in hello Azure portal](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="9f04b-115">Merhaba todoitem.js var olan kodda hello şununla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9f04b-115">Replace hello existing code in todoitem.js with hello following:</span></span>

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

    <span data-ttu-id="9f04b-116">Bu, yeni bir öğe eklendiğinde hello item.text içeren bir şablon bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="9f04b-116">This sends a template notification that contains hello item.text when a new item is inserted.</span></span>
3. <span data-ttu-id="9f04b-117">Yerel bilgisayarınızda Hello dosyasının düzenlenmesi sırasında hello sunucu projesi yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="9f04b-117">When editing hello file on your local computer, republish hello server project.</span></span>
