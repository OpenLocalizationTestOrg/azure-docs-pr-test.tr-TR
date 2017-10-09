---
title: "Azure mantıksal uygulamaları için Azure Event Hubs ile Olay İzleyicisi yukarı aaaSet | Microsoft Docs"
description: "Veri akışları tooreceive olaylarını izlemek ve Azure Logic Apps ile Azure Event Hubs için olayları Gönder"
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
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="59775-104">İzleme, gönderip hello olay hub'ları bağlayıcı olayları</span><span class="sxs-lookup"><span data-stu-id="59775-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="59775-105">Olay İzleyici yukarı tooset mantıksal uygulamanızı olayları algılamak, olayları alabilir ve olayları, böylece tooan bağlanmak [Azure olay hub'ı](https://azure.microsoft.com/services/event-hubs) mantığı uygulamanızdan.</span><span class="sxs-lookup"><span data-stu-id="59775-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="59775-106">Daha fazla bilgi edinmek [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="59775-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="59775-107">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="59775-107">Requirements</span></span>

* <span data-ttu-id="59775-108">Toohave sahip bir [olay hub'ları ad alanı ve olay hub'ı](../event-hubs/event-hubs-create.md) azure'da.</span><span class="sxs-lookup"><span data-stu-id="59775-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="59775-109">Bilgi [nasıl toocreate bir olay hub'ları ad alanı ve olay hub'ı](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="59775-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="59775-110">toouse [tüm bağlayıcıların](https://docs.microsoft.com/azure/connectors/apis-list) mantıksal uygulamanızı toocreate bir mantıksal uygulama öncelikle olması.</span><span class="sxs-lookup"><span data-stu-id="59775-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="59775-111">Bilgi [nasıl toocreate bir mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="59775-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="59775-112">Olay hub'ları ad alanı izinleri denetleyin ve hello bağlantı dizesini bulun</span><span class="sxs-lookup"><span data-stu-id="59775-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="59775-113">Logic app tooaccess için herhangi bir hizmet, toocreate sahip bir [ *bağlantı* ](./connectors-overview.md) yapmadıysanız mantığı uygulama ve hello hizmetiniz arasında.</span><span class="sxs-lookup"><span data-stu-id="59775-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="59775-114">Bu bağlantı mantığı uygulama tooaccess verilerinizi yetkilendirir.</span><span class="sxs-lookup"><span data-stu-id="59775-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="59775-115">İçin logic app tooaccess toohave sahip olay Hub'ınızı **Yönet** izinleri ve Event Hubs ad alanınız için hello bağlantı dizesi.</span><span class="sxs-lookup"><span data-stu-id="59775-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="59775-116">toocheck izinleri ve get hello bağlantı dizesi, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="59775-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="59775-117">İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="59775-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="59775-118">Tooyour olay hub'ları Git *ad alanı*, belirli olay hub'ı hello değil.</span><span class="sxs-lookup"><span data-stu-id="59775-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="59775-119">Merhaba ad alanı dikey penceresinde, altında **ayarları**, seçin **paylaşılan erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="59775-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="59775-120">Altında **talep**, sahip olduğunuz onay **Yönet** bu ad alanı için izinleri.</span><span class="sxs-lookup"><span data-stu-id="59775-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Olay hub'ı ad alanınız için izinleri yönetme](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="59775-122">Merhaba olay hub'ları ad alanı, toocopy hello bağlantı dizesini seçin **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="59775-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="59775-123">Sonraki tooyour birincil anahtar bağlantı dizesi, hello Kopyala düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="59775-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Olay hub'ları ad alanı bağlantı dizesini kopyalayın](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="59775-125">tooconfirm bağlantı dizenizi olay hub'ları ad alanınız ile veya belirli bir Event Hub ile ilişkili olup olmadığını denetleyin hello hello bağlantı dizesi `EntityPath` parametresi.</span><span class="sxs-lookup"><span data-stu-id="59775-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="59775-126">Bu parametre bulursanız, hello bağlantı dizesi belirli olay hub için "varlığı" ve hello doğru dize toouse mantıksal uygulamanızı sahip değil.</span><span class="sxs-lookup"><span data-stu-id="59775-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="59775-127">Şimdi bir olay hub'ları tetikleyici veya eylem tooyour mantıksal uygulama ekledikten sonra kimlik bilgileri istendiğinde, tooyour olay hub'ları ad bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="59775-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="59775-128">Bağlantınızı bir ad verin, kopyalanır ve seçin hello bağlantı dizesi girin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="59775-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Olay hub'ları ad alanı için bağlantı dizesi girin](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="59775-130">Bağlantınızı oluşturduktan sonra hello bağlantı adı hello olay hub'ları tetikleyici veya eylem görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="59775-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="59775-131">Daha sonra devam edebilirsiniz ile Merhaba mantıksal uygulamanızı diğer adımları.</span><span class="sxs-lookup"><span data-stu-id="59775-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Oluşturulan olay hub'ları ad alanı bağlantı](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="59775-133">Yeni olaylar olay Hub'ınızı aldığında, iş akışı Başlat</span><span class="sxs-lookup"><span data-stu-id="59775-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="59775-134">A [ *tetikleyici* ](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) mantıksal uygulamanızı bir iş akışı başlatır bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="59775-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="59775-135">Yeni olaylar tooyour olay hub'ı gönderildiğinde bir iş akışını başlatmak için bu olay algılar hello tetikleyici eklemek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="59775-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="59775-136">Merhaba, [Azure portal](https://portal.azure.com "Azure portal"), Git tooyour var olan mantıksal uygulama'ı ya da boş mantıksal uygulama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="59775-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="59775-137">Merhaba arama kutusuna hello mantığı Uygulama Tasarımcısı için `event hubs` filtreniz için.</span><span class="sxs-lookup"><span data-stu-id="59775-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="59775-138">Bu tetikleyici seçin: **zaman olayların Event Hub'ında kullanılabilir**</span><span class="sxs-lookup"><span data-stu-id="59775-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Olay Hub'ınızı yeni olayların ne zaman alan için tetikleyici seçin](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="59775-140">Bir bağlantı tooyour olay hub'ları ad alanı zaten sahip değilseniz, istenir toocreate şimdi bu bağlantı.</span><span class="sxs-lookup"><span data-stu-id="59775-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="59775-141">Bağlantınızı bir ad verin ve Event Hubs ad alanınız için hello bağlantı dizesi girin.</span><span class="sxs-lookup"><span data-stu-id="59775-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="59775-142">Gerekirse, bilgi [nasıl toofind bağlantı dizenizi](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="59775-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Olay hub'ları ad alanı için bağlantı dizesi girin](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="59775-144">Merhaba bağlantı oluşturduktan sonra hello ayarlarını hello **bir olay gerçekleştiğinde bir olay Hub'ındaki kullanılabilir** tetikleyici görünür.</span><span class="sxs-lookup"><span data-stu-id="59775-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Olay Hub'ınızı yeni olayların ne zaman alan için tetikleyici ayarları](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="59775-146">Adını girin veya hello için hello toomonitor istediğiniz olay hub'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="59775-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="59775-147">Merhaba sıklığı ve toocheck hello olay hub'ı hangi sıklıkta güncelleştirileceğini aralığını seçin.</span><span class="sxs-lookup"><span data-stu-id="59775-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="59775-148">toooptionally olayları okumak için bir tüketici grubu seçin, **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="59775-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Olay hub'ı veya tüketici grubu belirtin](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="59775-150">Şimdi bir tetikleyici toostart bir iş akışı mantığı uygulamanız için ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="59775-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="59775-151">Olay hub'ı ayarladığınız hello zamanlamaya göre hello belirtilen mantıksal uygulamanızı denetler.</span><span class="sxs-lookup"><span data-stu-id="59775-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="59775-152">Uygulamanızı hello olay hub'ı yeni olaylar bulursa, hello tetikleyici diğer eylemler veya tetikleyicileri mantıksal uygulamanızı çalışır.</span><span class="sxs-lookup"><span data-stu-id="59775-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="59775-153">Olayları tooyour olay hub'ı mantıksal uygulamanızı Gönder</span><span class="sxs-lookup"><span data-stu-id="59775-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="59775-154">[*Eylem*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts), mantıksal uygulama iş akışınız tarafından gerçekleştirilen bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="59775-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="59775-155">Bir tetikleyici tooyour mantıksal uygulama ekledikten sonra Bu tetikleyici tarafından oluşturulan verilerle bir eylem tooperform işlemleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59775-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="59775-156">toosend mantığı uygulamanızdan olay tooyour olay hub'ı şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="59775-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="59775-157">Mantıksal Uygulama Tasarımcısı'nda mantığı uygulama tetikleyici altında seçin **yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="59775-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    !["Yeni adım" sonra "Eylem Ekle" seçin](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="59775-159">Şimdi Bul ve bir eylem tooperform seçin.</span><span class="sxs-lookup"><span data-stu-id="59775-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="59775-160">Bu örnek için herhangi bir eylem seçebilmenize rağmen hello olay hub'ları eylem toosend olayları istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="59775-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="59775-161">Merhaba arama kutusuna `event hubs` filtreniz için.</span><span class="sxs-lookup"><span data-stu-id="59775-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="59775-162">Bu eylem seçin: **gönderme olayı**</span><span class="sxs-lookup"><span data-stu-id="59775-162">Select this action: **Send event**</span></span>

    !["Event Hubs - gönderme olayı" seçin eylemi](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="59775-164">Merhaba Event Hub'ın toosend hello olay istediğiniz hello adı gibi hello olayı için gerekli hello ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="59775-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="59775-165">Bu olay için içeriği gibi hello olay hakkında isteğe bağlı diğer ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="59775-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="59775-166">toooptionally belirtin hello olay hub'ı bölüm nerede toosend hello olayı seçin **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="59775-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Olay hub'ı adı ve isteğe bağlı olay ayrıntılarını girin](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="59775-168">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59775-168">Save your changes.</span></span>

    ![Mantıksal uygulamanızı kaydetme](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="59775-170">Bir eylem toosend olaylarını mantıksal uygulamanızı şimdi ayarladınız.</span><span class="sxs-lookup"><span data-stu-id="59775-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="59775-171">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="59775-171">Connector-specific details</span></span>

<span data-ttu-id="59775-172">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="59775-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="59775-173">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="59775-173">Get help</span></span>

<span data-ttu-id="59775-174">tooask sorular, soruları ve diğer Azure mantıksal uygulamaları kullanıcıların gittiğini, bkz: ziyaret hello [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="59775-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="59775-175">toohelp Logic Apps ve bağlayıcılar geliştirmek, oy veya hello fikir gönderme [Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="59775-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59775-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59775-176">Next steps</span></span>

*  [<span data-ttu-id="59775-177">Azure mantıksal uygulamaları için diğer bağlayıcıları Bul</span><span class="sxs-lookup"><span data-stu-id="59775-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)