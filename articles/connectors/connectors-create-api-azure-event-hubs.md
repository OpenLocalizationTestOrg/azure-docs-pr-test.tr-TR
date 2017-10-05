---
title: "Azure mantıksal uygulamaları için Azure Event Hubs ile Olay İzleyicisi ayarlama | Microsoft Docs"
description: "Veri akışları olaylarını almak ve Azure Logic Apps ile Azure Event Hubs için olayları göndermek için izleme"
services: logic-apps
keywords: "veri akışı, olay izleme, olay hub'ları"
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="6d701-104">İzleme, almak ve Event Hubs Bağlayıcısı ile olayları göndermek</span><span class="sxs-lookup"><span data-stu-id="6d701-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="6d701-105">Mantıksal uygulamanızı olayları algılamak, olayları alabilir ve olayları göndermek için bir Olay İzleyicisi ayarlamak üzere bağlanmak bir [Azure olay hub'ı](https://azure.microsoft.com/services/event-hubs) mantığı uygulamanızdan.</span><span class="sxs-lookup"><span data-stu-id="6d701-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="6d701-106">Daha fazla bilgi edinmek [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="6d701-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="6d701-107">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="6d701-107">Requirements</span></span>

* <span data-ttu-id="6d701-108">Sahip olmanız bir [olay hub'ları ad alanı ve olay hub'ı](../event-hubs/event-hubs-create.md) azure'da.</span><span class="sxs-lookup"><span data-stu-id="6d701-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="6d701-109">Bilgi [bir olay hub'ları ad alanı ve olay hub'ı nasıl oluşturulacağını](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="6d701-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="6d701-110">Kullanılacak [tüm bağlayıcıların](https://docs.microsoft.com/azure/connectors/apis-list) mantıksal uygulamanızı bir mantıksal uygulama ilk oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6d701-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="6d701-111">Bilgi [bir mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6d701-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="6d701-112">Olay hub'ları ad alanı izinleri denetleyin ve bağlantı dizesini bulun</span><span class="sxs-lookup"><span data-stu-id="6d701-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="6d701-113">Oluşturmak zorunda mantıksal uygulamanızı herhangi bir hizmete erişmek bir [ *bağlantı* ](./connectors-overview.md) mantıksal uygulamanızı ve henüz yapmadıysanız hizmetin arasında.</span><span class="sxs-lookup"><span data-stu-id="6d701-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="6d701-114">Bu bağlantı verilere erişmek için mantıksal uygulamanızı yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="6d701-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="6d701-115">Mantıksal uygulamanızı olay Hub'ınızı erişmek sahip olmanız **Yönet** izinleri ve Event Hubs ad alanınıza bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="6d701-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="6d701-116">İzinlerinizi denetleyin ve bağlantı dizesini almak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d701-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="6d701-117">[Azure portalı](https://portal.azure.com "Azure portalı") oturumunu açın.</span><span class="sxs-lookup"><span data-stu-id="6d701-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="6d701-118">Olay hub'larınız gidin *ad alanı*, değil belirli olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="6d701-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="6d701-119">Ad alanı dikey altında **ayarları**, seçin **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="6d701-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="6d701-120">Altında **talep**, sahip olduğunuz onay **Yönet** bu ad alanı için izinleri.</span><span class="sxs-lookup"><span data-stu-id="6d701-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Olay hub'ı ad alanınız için izinleri yönetme](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="6d701-122">Olay hub'ları ad alanı için bağlantı dizesini kopyalayın tercih **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="6d701-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="6d701-123">Birincil anahtar bağlantı dizenizi yanındaki Kopyala düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="6d701-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Olay hub'ları ad alanı bağlantı dizesini kopyalayın](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="6d701-125">Bağlantı dizenizi olay hub'ları ad alanınız ile veya belirli bir Event Hub ile ilişkili olup olmadığını doğrulamak için bağlantı dizesini kontrol `EntityPath` parametresi.</span><span class="sxs-lookup"><span data-stu-id="6d701-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="6d701-126">Bu parametre bulursanız, bağlantı dizesi belirli olay hub için "varlığı" ve mantıksal uygulamanızı ile kullanılacak doğru dizesi değil.</span><span class="sxs-lookup"><span data-stu-id="6d701-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="6d701-127">Şimdi bir olay hub'ları tetikleyici veya eylem mantıksal uygulamanızı ekledikten sonra kimlik bilgileri istendiğinde, olay hub'ları ad alanına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6d701-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="6d701-128">Bağlantınızı bir ad verin, kopyalanır ve seçin bağlantı dizesi **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6d701-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Olay hub'ları ad alanı için bağlantı dizesi girin](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="6d701-130">Bağlantınızı oluşturduktan sonra bağlantı adı olay hub'ları tetikleyici veya eylem görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="6d701-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="6d701-131">Ardından, mantıksal uygulamanızı diğer adımlarla devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d701-131">You can then continue with the other steps in your logic app.</span></span>

    ![Oluşturulan olay hub'ları ad alanı bağlantı](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="6d701-133">Yeni olaylar olay Hub'ınızı aldığında, iş akışı Başlat</span><span class="sxs-lookup"><span data-stu-id="6d701-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="6d701-134">A [ *tetikleyici* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) mantıksal uygulamanızı bir iş akışı başlatır bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="6d701-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="6d701-135">Yeni olaylar için olay Hub'ınızı gönderildiğinde bir iş akışını başlatmak için bu olay algılar tetikleyici eklemek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d701-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="6d701-136">İçinde [Azure portal](https://portal.azure.com "Azure portal"), var olan mantıksal uygulamanızı Git veya boş mantıksal uygulama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="6d701-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="6d701-137">Mantıksal Uygulama Tasarımcısı'nı arama kutusuna girin `event hubs` filtreniz için.</span><span class="sxs-lookup"><span data-stu-id="6d701-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="6d701-138">Bu tetikleyici seçin: **zaman olayların Event Hub'ında kullanılabilir**</span><span class="sxs-lookup"><span data-stu-id="6d701-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Olay Hub'ınızı yeni olayların ne zaman alan için tetikleyici seçin](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="6d701-140">Olay hub'ları ad alanınıza bağlantı sahip değilseniz, bu bağlantı artık oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="6d701-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="6d701-141">Bağlantınızı bir ad verin ve için olay hub'ları ad alanınıza bağlantı dizesi girin.</span><span class="sxs-lookup"><span data-stu-id="6d701-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="6d701-142">Gerekirse, bilgi [bağlantı dizenizi bulmak nasıl](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="6d701-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Olay hub'ları ad alanı için bağlantı dizesi girin](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="6d701-144">Bağlantı ayarlarını oluşturduktan sonra **bir olay gerçekleştiğinde bir olay Hub'ındaki kullanılabilir** tetikleyici görünür.</span><span class="sxs-lookup"><span data-stu-id="6d701-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Olay Hub'ınızı yeni olayların ne zaman alan için tetikleyici ayarları](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="6d701-146">Adını girin veya izlemek istediğiniz olay hub'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d701-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="6d701-147">Olay hub'ı denetlemek istediğiniz sıklıkta aralığı ve sıklığı seçin.</span><span class="sxs-lookup"><span data-stu-id="6d701-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="6d701-148">İsteğe bağlı olarak olayları okumak için bir tüketici grubu seçmek için Seç **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="6d701-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Olay hub'ı veya tüketici grubu belirtin](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="6d701-150">Şimdi bir tetikleyici mantığı uygulamanız için bir iş akışını başlatmak için ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="6d701-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="6d701-151">Mantıksal uygulamanızı belirtilen Event Hub'in belirlediğiniz bir zamanlamaya göre denetler.</span><span class="sxs-lookup"><span data-stu-id="6d701-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="6d701-152">Uygulamanızı yeni olaylar bulursa olay Hub'ı tetikleyici diğer eylemleri çalıştırır veya mantıksal uygulamanızı tetikler.</span><span class="sxs-lookup"><span data-stu-id="6d701-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="6d701-153">Olayları için olay Hub'ınızı mantığı uygulamanızdan Gönder</span><span class="sxs-lookup"><span data-stu-id="6d701-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="6d701-154">[*Eylem*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts), mantıksal uygulama iş akışınız tarafından gerçekleştirilen bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="6d701-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="6d701-155">Mantıksal uygulamanıza bir tetikleyici ekledikten sonra, bu tetikleyici tarafından oluşturulan işlemleri gerçekleştirmek için bir eylem ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d701-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="6d701-156">Bir olay için olay Hub'ınızı mantığı uygulamanızdan göndermek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d701-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="6d701-157">Mantıksal Uygulama Tasarımcısı'nda mantığı uygulama tetikleyici altında seçin **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6d701-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    !["Yeni adım" sonra "Eylem Ekle" seçin](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="6d701-159">Şimdi Bul ve gerçekleştirmek istediğiniz eylemi seçin.</span><span class="sxs-lookup"><span data-stu-id="6d701-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="6d701-160">Bu örnek için herhangi bir eylem seçebilmenize rağmen olayları göndermek için olay hub'ları eylem istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6d701-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="6d701-161">Arama kutusuna `event hubs` filtreniz için.</span><span class="sxs-lookup"><span data-stu-id="6d701-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="6d701-162">Bu eylem seçin: **gönderme olayı**</span><span class="sxs-lookup"><span data-stu-id="6d701-162">Select this action: **Send event**</span></span>

    !["Event Hubs - gönderme olayı" seçin eylemi](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="6d701-164">Olay göndermek istediğiniz olay hub'ı adı gibi olayı için gerekli ayrıntıları girin.</span><span class="sxs-lookup"><span data-stu-id="6d701-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="6d701-165">Bu olay için içeriği gibi olaya ilişkin isteğe bağlı diğer ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="6d701-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="6d701-166">İsteğe bağlı olarak olay hub'ı bölüm olay gönderileceği yeri belirtmek için **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="6d701-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Olay hub'ı adı ve isteğe bağlı olay ayrıntılarını girin](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="6d701-168">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6d701-168">Save your changes.</span></span>

    ![Mantıksal uygulamanızı kaydetme](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="6d701-170">Şimdi, mantıksal uygulamanızı olayları göndermek için eylem ayarlama.</span><span class="sxs-lookup"><span data-stu-id="6d701-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="6d701-171">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="6d701-171">Connector-specific details</span></span>

<span data-ttu-id="6d701-172">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="6d701-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="6d701-173">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="6d701-173">Get help</span></span>

<span data-ttu-id="6d701-174">Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını görmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="6d701-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="6d701-175">Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın.</span><span class="sxs-lookup"><span data-stu-id="6d701-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d701-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d701-176">Next steps</span></span>

*  [<span data-ttu-id="6d701-177">Azure mantıksal uygulamaları için diğer bağlayıcıları Bul</span><span class="sxs-lookup"><span data-stu-id="6d701-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)