---
title: "Durumunu denetlemek için günlüğe kaydetmeyi ayarlayın ve Uyarıları - Azure mantıksal uygulamaları alma | Microsoft Docs"
description: "Durum ve logic apps için performans izleme, tanılama verilerini günlüğe ve uyarılarını ayarlama"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 4795f5728d4ce6ff21b97bc3fefd6a53e0c6a11b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="2b230-103">Durum İzleme, tanılama günlük ayarlama ve Azure Logic Apps için uyarılarını Aç</span><span class="sxs-lookup"><span data-stu-id="2b230-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="2b230-104">Çalıştırdıktan sonra [oluşturma ve bir mantıksal uygulama çalıştırma](../logic-apps/logic-apps-create-a-logic-app.md), çalışır geçmişi, tetikleyici geçmişi, durumunu ve performansını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b230-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="2b230-105">Gerçek zamanlı Olay izleme ve daha zengin hata ayıklama için ayarlanmış [tanılama günlükleri](#azure-diagnostics) mantığı uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="2b230-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="2b230-106">Bu şekilde yapabilecekleriniz [bulma ve görüntüleme olayları](#find-events)tetikleyici olayları, çalışma olayları ve eylem olayları gibi.</span><span class="sxs-lookup"><span data-stu-id="2b230-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="2b230-107">Bu da kullanabilirsiniz [tanılama verilerini diğer hizmetlerle](#extend-diagnostic-data)Azure Storage ve Azure Event Hubs gibi.</span><span class="sxs-lookup"><span data-stu-id="2b230-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="2b230-108">Hataları veya diğer olası sorunları hakkında bildirim almak için ayarladığınız [uyarıları](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="2b230-108">To get notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="2b230-109">Örneğin, "beşten fazla çalıştığında bir saat içinde başarısız olduğunda." algıladığında bir uyarı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="2b230-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="2b230-110">Ayrıca izleme, izleme ve program aracılığıyla kullanarak oturum ayarlayabilirsiniz [Azure tanılama olay ayarlarını ve özelliklerini](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="2b230-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="2b230-111">Görünüm çalıştırır ve mantıksal uygulamanız için tetikleyici geçmişi</span><span class="sxs-lookup"><span data-stu-id="2b230-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="2b230-112">Mantıksal uygulamanızı bulmak için [Azure portal](https://portal.azure.com), ana Azure menüsünde, **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="2b230-112">To find your logic app in the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **More services**.</span></span> <span data-ttu-id="2b230-113">Arama kutusuna "logic apps" bulun ve seçin **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="2b230-113">In the search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Mantıksal uygulamanızı Bul](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="2b230-115">Azure portalı, Azure aboneliğinizle ilişkili tüm mantığı uygulamalar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2b230-115">The Azure portal shows all the logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="2b230-116">Mantıksal uygulamanızı seçin, sonra seçin **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="2b230-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="2b230-117">Azure Portalı'nı çalıştırır geçmişi ve mantıksal uygulamanızı için tetikleyici geçmişini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b230-117">The Azure portal shows the runs history and trigger history for your logic app.</span></span> <span data-ttu-id="2b230-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2b230-118">For example:</span></span>

   ![Mantıksal uygulama geçmişi ve tetikleyici geçmişi çalıştırır](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="2b230-120">**Geçmiş çalıştıran** mantığı uygulamanız için tüm metinler gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b230-120">**Runs history** shows all the runs for your logic app.</span></span> 
   * <span data-ttu-id="2b230-121">**Tetiklemek geçmişi** mantığı uygulamanız için tüm tetikleyici etkinliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b230-121">**Trigger History** shows all the trigger activity for your logic app.</span></span>

   <span data-ttu-id="2b230-122">Durum açıklamaları için bkz: [mantıksal uygulamanızı sorun giderme](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="2b230-123">Araç çubuğunda, beklediğiniz veri bulamazsanız seçin **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="2b230-123">If you don't find the data that you expect, on the toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="2b230-124">Belirli bir çalıştırma adımları altında görüntülemek için **çalıştıran geçmişi**, çalıştırılan seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-124">To view the steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="2b230-125">İzleme görünümü her adım, çalışan gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b230-125">The monitor view shows each step in that run.</span></span> <span data-ttu-id="2b230-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2b230-126">For example:</span></span>

   ![Belirli bir çalıştırma için Eylemler](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="2b230-128">Çalıştırma hakkında daha fazla bilgi almak için tercih **çalıştırma ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="2b230-128">To get more details about the run, choose **Run Details**.</span></span> <span data-ttu-id="2b230-129">Adımlar, durumu, girişleri ve çıkışları çalıştırma için bu bilgileri özetler.</span><span class="sxs-lookup"><span data-stu-id="2b230-129">This information summarizes the steps, status, inputs, and outputs for the run.</span></span> 

   ![Seçin "Ayrıntıları Çalıştır"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="2b230-131">Örneğin, çalışmanın elde edebilirsiniz **bağıntı kimliği**, kullandığınızda, gereksinim duyabileceğiniz [Logic Apps için REST API](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="2b230-131">For example, you can get the run's **Correlation ID**, which you might need when you use the [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="2b230-132">Belirli bir adıma hakkında bilgi almak için bu adım seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-132">To get details about a specific step, choose that step.</span></span> <span data-ttu-id="2b230-133">Şimdi girişleri ve çıkışları Bu adım için gerçekleşen hataları gibi ayrıntıları gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b230-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="2b230-134">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2b230-134">For example:</span></span>

   ![Adım ayrıntıları](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="2b230-136">Tüm çalışma zamanı ayrıntılarını ve olayları Logic Apps Hizmeti'nde şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="2b230-136">All runtime details and events are encrypted within the Logic Apps service.</span></span> <span data-ttu-id="2b230-137">Yalnızca bir kullanıcı bu verileri görüntülemek için istediğinde şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="2b230-137">They are decrypted only when a user requests to view that data.</span></span> <span data-ttu-id="2b230-138">Ayrıca bu olaylar ile erişimi denetleyebilirsiniz [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-138">You can also control access to these events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="2b230-139">Belirli tetikleyici olay hakkında bilgi almak için geri dönüp **genel bakış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="2b230-139">To get details about a specific trigger event, go back to the **Overview** pane.</span></span> <span data-ttu-id="2b230-140">Altında **tetiklemek geçmişi**, tetikleyici olayı seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-140">Under **Trigger history**, select the trigger event.</span></span> <span data-ttu-id="2b230-141">Şimdi girişleri ve çıkışları, gibi ayrıntıları örneğin gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2b230-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Tetikleyici olay çıkış ayrıntıları](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="2b230-143">Tanılama mantığı uygulamanız için oturum açma</span><span class="sxs-lookup"><span data-stu-id="2b230-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="2b230-144">Daha zengin çalışma zamanı ayrıntılarını ve olayları ile hata ayıklama, tanılama ile oturum ayarlayabilirsiniz [Azure günlük analizi](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="2b230-145">Günlük analizi olan bir hizmet olarak [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) bulut izler ve şirket içi ortamları, performans ve kullanılabilirlik tutmanıza yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="2b230-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments to help you maintain their availability and performance.</span></span> 

<span data-ttu-id="2b230-146">Başlamadan önce OMS çalışma alanınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2b230-146">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="2b230-147">Bilgi [bir OMS çalışma alanı oluşturmak nasıl](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-147">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="2b230-148">İçinde [Azure portal](https://portal.azure.com), bulma ve mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-148">In the [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="2b230-149">Mantıksal uygulama dikey menüsünde altında **izleme**, seçin **tanılama** > **tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="2b230-149">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![, Tanılama, Tanılama izleme ayarları için Git](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="2b230-151">Altında **tanılama ayarları**, seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="2b230-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Tanılama günlüklerini Aç](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="2b230-153">Şimdi gösterildiği gibi günlüğe kaydetme için OMS çalışma ve olay kategorisi seçin:</span><span class="sxs-lookup"><span data-stu-id="2b230-153">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="2b230-154">Seçin **için günlük analizi Gönder**.</span><span class="sxs-lookup"><span data-stu-id="2b230-154">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="2b230-155">Altında **günlük analizi**, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="2b230-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="2b230-156">Altında **OMS çalışma alanları**, günlük için kullanılacak OMS çalışma alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-156">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="2b230-157">Altında **günlük**seçin **WorkflowRuntime** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="2b230-157">Under **Log**, select the **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="2b230-158">Ölçüm aralığını seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-158">Choose the metric interval.</span></span>
   6. <span data-ttu-id="2b230-159">İşiniz bittiğinde seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2b230-159">When you're done, choose **Save**.</span></span>

   ![OMS çalışma ve günlük verilerini seçin](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="2b230-161">Şimdi, olaylar ve eylem olaylar çalıştırmak tetikleyici olaylar için olayları ve diğer verileri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b230-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="2b230-162">Mantıksal uygulamanız için olaylar ve veri Bul</span><span class="sxs-lookup"><span data-stu-id="2b230-162">Find events and data for your logic app</span></span>

<span data-ttu-id="2b230-163">Bulma ve mantıksal uygulamanızı olaylarını görüntüleme gibi için olaylar, olaylar, çalıştırmak ve eylem olaylar tetikleyin, şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2b230-163">To find and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="2b230-164">İçinde [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="2b230-164">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="2b230-165">"İçin günlük analizi" arayın, ardından seçin **günlük analizi** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="2b230-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   !["Günlük analizi" seçin](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="2b230-167">Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS çalışma alanınızı seçin](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="2b230-169">Altında **Yönetim**, seçin **OMS portalı**.</span><span class="sxs-lookup"><span data-stu-id="2b230-169">Under **Management**, choose **OMS Portal**.</span></span>

   !["OMS portalı" seçin](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="2b230-171">OMS giriş sayfanızda seçin **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="2b230-171">On your OMS home page, choose **Log Search**.</span></span>

   ![OMS giriş sayfanızda "Günlük arama" seçin](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="2b230-173">-veya-</span><span class="sxs-lookup"><span data-stu-id="2b230-173">-or-</span></span>

   ![OMS menüsünde "Günlük arama" yi seçin](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="2b230-175">Arama kutusuna, bulmak ve basın istediğiniz bir alanı belirtmek **Enter**.</span><span class="sxs-lookup"><span data-stu-id="2b230-175">In the search box, specify a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="2b230-176">Yazmaya başladığınızda, OMS olası eşleşmeler ve kullanabileceğiniz işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b230-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="2b230-177">Örneğin, ilk 10 olayları bulmak için girin ve bu arama sorgusuna seçin: **kategori WorkflowRuntime = | üst 10**</span><span class="sxs-lookup"><span data-stu-id="2b230-177">For example, to find the top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Arama dizesini girin](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="2b230-179">Daha fazla bilgi edinmek [günlük analizi verileri bulmak üzere nasıl](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-179">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="2b230-180">Sonuçları sayfasında sol çubuğunda görüntülemek istediğiniz zaman dilimini seçin.</span><span class="sxs-lookup"><span data-stu-id="2b230-180">On the results page, in the left bar, choose the timeframe that you want to view.</span></span>
<span data-ttu-id="2b230-181">Bir filtre ekleyerek sorgunuzu daraltın tercih **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2b230-181">To refine your query by adding a filter, choose **+Add**.</span></span>

   ![Sorgu sonuçları ilişkin zaman çerçevesini seçin](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="2b230-183">Altında **filtreler Ekle**, istediğiniz filtreyi bulabilmek için filtre adı girin.</span><span class="sxs-lookup"><span data-stu-id="2b230-183">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="2b230-184">Filtreyi seçin ve **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2b230-184">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="2b230-185">Bu örnekte "Durum" word altında başarısız olayları bulmak için kullanır. **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="2b230-185">This example uses the word "status" to find failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="2b230-186">Burada filtresi için **status_s** zaten seçilidir.</span><span class="sxs-lookup"><span data-stu-id="2b230-186">Here the filter for **status_s** is already selected.</span></span>

   ![Filtreyi seçin](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="2b230-188">Sol çubuğunda ve seçin istediğiniz filtre değeri seçin **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="2b230-188">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   ![Filtre değeri seçin, "Uygula"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="2b230-190">Şimdi oluşturmakta olduğunuz sorgu döndür.</span><span class="sxs-lookup"><span data-stu-id="2b230-190">Now return to the query that you're building.</span></span> <span data-ttu-id="2b230-191">Sorgunuz seçili filtresi ve değer ile güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2b230-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="2b230-192">Önceki sonuçlarınızı artık çok filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="2b230-192">Your previous results are now filtered too.</span></span>

   ![Sorgunuz filtrelenmiş sonuçlar döndürür](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="2b230-194">Sorgunuz gelecekte kullanım için kaydetmek üzere seçim yapın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2b230-194">To save your query for future use, choose **Save**.</span></span> <span data-ttu-id="2b230-195">Bilgi [sorgunuzu kaydetmek nasıl](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="2b230-195">Learn [how to save your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="2b230-196">Nasıl ve tanılama verilerini diğer hizmetleri ile kullandığınız genişletme</span><span class="sxs-lookup"><span data-stu-id="2b230-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="2b230-197">Azure günlük analizi ile birlikte nasıl mantığı uygulamanızın tanılama verilerini diğer Azure hizmetleriyle örneğin kullandığınız genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2b230-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="2b230-198">Azure depolama alanında Azure tanılama günlüklerini arşiv</span><span class="sxs-lookup"><span data-stu-id="2b230-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="2b230-199">Azure Event hubs'a akış Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="2b230-199">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="2b230-200">Telemetri ve diğer hizmetlerden analizi kullanarak izleme Get gerçek zamanlı ister sonra şunları yapabilirsiniz [Azure akış analizi](../stream-analytics/stream-analytics-introduction.md) ve [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="2b230-201">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="2b230-201">For example:</span></span>

* [<span data-ttu-id="2b230-202">Event Hubs akış verilerini akış analizi</span><span class="sxs-lookup"><span data-stu-id="2b230-202">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="2b230-203">Akış Analizi ile akış verilerini çözümleme ve gerçek zamanlı analiz Pano Power BI'da oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b230-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="2b230-204">Ayarlamak istediğiniz seçenekleri bağlı olarak, olduğundan emin olun, ilk [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md) veya [Azure olay hub'ı oluşturma](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-204">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="2b230-205">Ardından Tanılama verileri gönder istediğiniz seçenekleri seçin:</span><span class="sxs-lookup"><span data-stu-id="2b230-205">Then select the options for where you want to send diagnostic data:</span></span>

![Verileri Azure depolama hesabı veya olay hub'ına Gönder](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="2b230-207">Yalnızca bir depolama hesabı kullanmayı seçtiğinizde bekletme dönemleri uygulamak.</span><span class="sxs-lookup"><span data-stu-id="2b230-207">Retention periods apply only when you choose to use a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="2b230-208">Mantıksal uygulamanız için uyarıları ayarlama</span><span class="sxs-lookup"><span data-stu-id="2b230-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="2b230-209">Belirli ölçümleri veya aşıldı eşikler mantıksal uygulamanızı izlemek için ayarladığınız [Azure içindeki uyarıları](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-209">To monitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="2b230-210">Hakkında bilgi edinin [Azure ölçümlerini](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="2b230-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="2b230-211">Uyarıları ayarlamak için [Azure günlük analizi](../log-analytics/log-analytics-overview.md), şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2b230-211">To set up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="2b230-212">Uyarı ölçütleri ve Eylemler, daha gelişmiş [günlük analizi ayarlamak](#azure-diagnostics) çok.</span><span class="sxs-lookup"><span data-stu-id="2b230-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="2b230-213">Mantıksal uygulama dikey menüsünde altında **izleme**, seçin **tanılama** > **uyarı kuralları** > **UyarıEkle**aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="2b230-213">On the logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Mantıksal uygulamanız için uyarı ekleme](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="2b230-215">Üzerinde **uyarı kuralı eklemek** dikey penceresinde, uyarı gösterildiği gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2b230-215">On the **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="2b230-216">Altında **kaynak**, mantıksal uygulamanızı seçin, seçili değilse.</span><span class="sxs-lookup"><span data-stu-id="2b230-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="2b230-217">Bir ad ve açıklama için uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="2b230-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="2b230-218">Seçin bir **ölçüm** veya izlemek istediğiniz olay.</span><span class="sxs-lookup"><span data-stu-id="2b230-218">Select a **Metric** or event that you want to track.</span></span>
   4. <span data-ttu-id="2b230-219">Seçin bir **koşulu**, belirtin bir **eşik** ölçüm ve select **süresi** Bu ölçüm izleme.</span><span class="sxs-lookup"><span data-stu-id="2b230-219">Select a **Condition**, specify a **Threshold** for the metric, and select the **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="2b230-220">Uyarı için posta göndermek isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="2b230-220">Select whether to send mail for the alert.</span></span> 
   6. <span data-ttu-id="2b230-221">Diğer tüm e-posta adreslerini uyarı göndermek için belirtin.</span><span class="sxs-lookup"><span data-stu-id="2b230-221">Specify any other email addresses for sending the alert.</span></span> 
   <span data-ttu-id="2b230-222">Uyarı göndermek istediğiniz bir Web kancası URL'si de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b230-222">You can also specify a webhook URL where you want to send the alert.</span></span>

   <span data-ttu-id="2b230-223">Örneğin, bu kural beş olduğunda bir uyarı gönderir veya daha fazla çalıştığında bir saat içinde başarısız:</span><span class="sxs-lookup"><span data-stu-id="2b230-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Ölçüm uyarı kuralı oluştur](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="2b230-225">Bir mantıksal uygulama bir uyarıdan çalıştırmak için dahil edebileceğiniz [isteği tetikleyici](../connectors/connectors-native-reqres.md) , iş akışınızı olanak sağlayan bu örnekler gibi görevleri gerçekleştirmenize:</span><span class="sxs-lookup"><span data-stu-id="2b230-225">To run a logic app from an alert, you can include the [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="2b230-226">POST boşluk için</span><span class="sxs-lookup"><span data-stu-id="2b230-226">Post to Slack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="2b230-227">Bir metin Gönder</span><span class="sxs-lookup"><span data-stu-id="2b230-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="2b230-228">Kuyruğa bir ileti Ekle</span><span class="sxs-lookup"><span data-stu-id="2b230-228">Add a message to a queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="2b230-229">Azure Tanılama Olay ayarları ve ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="2b230-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="2b230-230">Mantıksal uygulamanızı ve bu olay, örneğin, durum ayrıntılarını her Tanılama Olay sahipse, başlangıç saati, bitiş saati ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="2b230-230">Each diagnostic event has details about your logic app and that event, for example, the status, start time, end time, and so on.</span></span> <span data-ttu-id="2b230-231">İzleme, izleme ve günlüğe kaydetme programlı olarak ayarlamak için ou bu ayrıntılarla kullanabilirsiniz [Azure Logic Apps için REST API](https://docs.microsoft.com/rest/api/logic) ve [Azure tanılama için REST API](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="2b230-231">To programmatically set up monitoring, tracking, and logging, ou can use these details with the [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and the [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="2b230-232">Örneğin, `ActionCompleted` olayında `clientTrackingId` ve `trackedProperties` izleme ve izleme için kullanabileceğiniz özellikler:</span><span class="sxs-lookup"><span data-stu-id="2b230-232">For example, the `ActionCompleted` event has the `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="2b230-233">`clientTrackingId`: Değilse tüm iç içe geçmiş iş akışları dahil olmak üzere Azure otomatik olarak bu kimliği oluşturur ve olayları çalıştırmak bir mantıksal uygulama arasında karşılık gelen sağlanan mantığı uygulamadan çağrılan.</span><span class="sxs-lookup"><span data-stu-id="2b230-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from the logic app.</span></span> <span data-ttu-id="2b230-234">Bu kodu bir tetikleyiciden geçirerek el ile belirtebilirsiniz bir `x-ms-client-tracking-id` , özel tetikleyici istek kimliği değeri ile üstbilgisi.</span><span class="sxs-lookup"><span data-stu-id="2b230-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in the trigger request.</span></span> <span data-ttu-id="2b230-235">Bir istek tetikleyici, HTTP tetikleyicisini ya da Web kancası tetikleyici kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b230-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="2b230-236">`trackedProperties`: Girişleri veya çıkışları tanılama veri izlemek için mantığı uygulamanızın JSON tanımında Eylemler izlenen özellikleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b230-236">`trackedProperties`: To track inputs or outputs in diagnostics data, you can add tracked properties to actions in your logic app's JSON definition.</span></span> <span data-ttu-id="2b230-237">İzlenen özellikleri yalnızca tek bir eylemin girişleri ve çıkışları izleyebilirsiniz, ancak kullanabileceğiniz `correlation` çalıştırmada eylemler arasında ilişkilendirilmesi olayları özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="2b230-237">Tracked properties can track only a single action's inputs and outputs, but you can use the `correlation` properties of events to correlate across actions in a run.</span></span>

  <span data-ttu-id="2b230-238">Bir veya daha fazla özellikleri izlemek için ekleme `trackedProperties` bölümü ve eylem tanımına istediğiniz özellikleri.</span><span class="sxs-lookup"><span data-stu-id="2b230-238">To track one or more properties, add the `trackedProperties` section and the properties you want to the action definition.</span></span> <span data-ttu-id="2b230-239">Örneğin, bir "sipariş Kimliğinde" telemetrinizi gibi verileri izlemek istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="2b230-239">For example, suppose you want to track data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="2b230-240">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b230-240">Next steps</span></span>

* [<span data-ttu-id="2b230-241">Mantıksal uygulama dağıtımı için şablonlar oluşturma ve yayın Yönetimi</span><span class="sxs-lookup"><span data-stu-id="2b230-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="2b230-242">B2B senaryolarını Kurumsal tümleştirme paketi</span><span class="sxs-lookup"><span data-stu-id="2b230-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="2b230-243">B2B iletilerini izleme</span><span class="sxs-lookup"><span data-stu-id="2b230-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)