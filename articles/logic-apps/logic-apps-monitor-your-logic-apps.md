---
title: "aaaCheck durum günlüğe kaydetmeyi ayarlayın ve Uyarıları - Azure mantıksal uygulamaları alma | Microsoft Docs"
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
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="f4f7f-103">Durum İzleme, tanılama günlük ayarlama ve Azure Logic Apps için uyarılarını Aç</span><span class="sxs-lookup"><span data-stu-id="f4f7f-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="f4f7f-104">Çalıştırdıktan sonra [oluşturma ve bir mantıksal uygulama çalıştırma](../logic-apps/logic-apps-create-a-logic-app.md), çalışır geçmişi, tetikleyici geçmişi, durumunu ve performansını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="f4f7f-105">Gerçek zamanlı Olay izleme ve daha zengin hata ayıklama için ayarlanmış [tanılama günlükleri](#azure-diagnostics) mantığı uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="f4f7f-106">Bu şekilde yapabilecekleriniz [bulma ve görüntüleme olayları](#find-events)tetikleyici olayları, çalışma olayları ve eylem olayları gibi.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="f4f7f-107">Bu da kullanabilirsiniz [tanılama verilerini diğer hizmetlerle](#extend-diagnostic-data)Azure Storage ve Azure Event Hubs gibi.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="f4f7f-108">hataları veya diğer olası sorunları hakkında tooget bildirimler ayarlanan [uyarıları](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="f4f7f-109">Örneğin, "beşten fazla çalıştığında bir saat içinde başarısız olduğunda." algıladığında bir uyarı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="f4f7f-110">Ayrıca izleme, izleme ve program aracılığıyla kullanarak oturum ayarlayabilirsiniz [Azure tanılama olay ayarlarını ve özelliklerini](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="f4f7f-111">Görünüm çalıştırır ve mantıksal uygulamanız için tetikleyici geçmişi</span><span class="sxs-lookup"><span data-stu-id="f4f7f-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="f4f7f-112">toofind mantıksal uygulamanızı hello [Azure portal](https://portal.azure.com), üzerinde hello Azure ana menü, seçin **daha fazla hizmet**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="f4f7f-113">Merhaba arama kutusuna "logic apps" bulun ve seçin **Logic apps**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Mantıksal uygulamanızı Bul](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="f4f7f-115">Hello Azure portal, Azure aboneliğinizle ilişkili tüm hello mantıksal uygulamaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="f4f7f-116">Mantıksal uygulamanızı seçin, sonra seçin **genel bakış**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="f4f7f-117">Hello Azure portal hello çalıştırır geçmişi ve mantıksal uygulamanızı için tetikleyici geçmişini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="f4f7f-118">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-118">For example:</span></span>

   ![Mantıksal uygulama geçmişi ve tetikleyici geçmişi çalıştırır](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="f4f7f-120">**Geçmiş çalıştıran** mantıksal uygulamanızı tüm hello çalıştırmalarında gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="f4f7f-121">**Tetiklemek geçmişi** mantığı uygulamanız için tüm hello tetikleyici etkinliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="f4f7f-122">Durum açıklamaları için bkz: [mantıksal uygulamanızı sorun giderme](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="f4f7f-123">Merhaba araç çubuğunda, beklediğiniz hello veri bulamazsanız seçin **yenileme**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="f4f7f-124">tooview hello adımları belirli bir çalışma altında **çalıştıran geçmişi**, çalıştırılan seçin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="f4f7f-125">Merhaba İzleyicisi görünümü her adım, çalışan gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="f4f7f-126">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-126">For example:</span></span>

   ![Belirli bir çalıştırma için Eylemler](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="f4f7f-128">tooget Çalıştır hello hakkında daha fazla ayrıntı seçin **çalıştırma ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="f4f7f-129">Bu bilgileri özetler hello adımları, durumu girişleri ve çıkışları hello için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Seçin "Ayrıntıları Çalıştır"](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="f4f7f-131">Örneğin, hello elde edebilirsiniz çalışmanın **bağıntı kimliği**, hello kullandığınızda, gereksinim duyabileceğiniz [Logic Apps için REST API](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="f4f7f-132">belirli bir adıma tooget ayrıntılarını bu adımı seçin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="f4f7f-133">Şimdi girişleri ve çıkışları Bu adım için gerçekleşen hataları gibi ayrıntıları gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="f4f7f-134">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-134">For example:</span></span>

   ![Adım ayrıntıları](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="f4f7f-136">Tüm çalışma zamanı ayrıntılarını ve olayları Logic Apps hizmet hello içinde şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="f4f7f-137">Yalnızca bir kullanıcı bu verileri tooview istediğinde şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="f4f7f-138">Erişimi toothese olaylarını kontrol edebilirsiniz [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="f4f7f-139">belirli tetikleyici olay tooget ayrıntılarını Geri Git toohello **genel bakış** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="f4f7f-140">Altında **tetiklemek geçmişi**seçin hello tetikleyici olay.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="f4f7f-141">Şimdi girişleri ve çıkışları, gibi ayrıntıları örneğin gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Tetikleyici olay çıkış ayrıntıları](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="f4f7f-143">Tanılama mantığı uygulamanız için oturum açma</span><span class="sxs-lookup"><span data-stu-id="f4f7f-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="f4f7f-144">Daha zengin çalışma zamanı ayrıntılarını ve olayları ile hata ayıklama, tanılama ile oturum ayarlayabilirsiniz [Azure günlük analizi](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="f4f7f-145">Günlük analizi olan bir hizmet olarak [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) bulut izler ve şirket içi ortamları toohelp kendi kullanılabilirliğini ve performansını korumak.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="f4f7f-146">Başlamadan önce toohave bir OMS çalışma alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="f4f7f-147">Bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="f4f7f-148">Merhaba, [Azure portal](https://portal.azure.com), bulma ve mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="f4f7f-149">Merhaba mantığı uygulama dikey menüsünde altında **izleme**, seçin **tanılama** > **tanılama ayarlarını**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![TooMonitoring, tanılama, tanılama ayarlarına Git](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="f4f7f-151">Altında **tanılama ayarları**, seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Tanılama günlüklerini Aç](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="f4f7f-153">Şimdi gösterildiği gibi günlüğe kaydetme için hello OMS çalışma ve olay kategorisi seçin:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="f4f7f-154">Seçin **tooLog Analytics Gönder**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="f4f7f-155">Altında **günlük analizi**, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="f4f7f-156">Altında **OMS çalışma alanları**, hello OMS çalışma toouse günlüğü için seçin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="f4f7f-157">Altında **günlük**seçin hello **WorkflowRuntime** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="f4f7f-158">Merhaba ölçüm aralığını seçin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="f4f7f-159">İşiniz bittiğinde seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-159">When you're done, choose **Save**.</span></span>

   ![OMS çalışma ve günlük verilerini seçin](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="f4f7f-161">Şimdi, olaylar ve eylem olaylar çalıştırmak tetikleyici olaylar için olayları ve diğer verileri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="f4f7f-162">Mantıksal uygulamanız için olaylar ve veri Bul</span><span class="sxs-lookup"><span data-stu-id="f4f7f-162">Find events and data for your logic app</span></span>

<span data-ttu-id="f4f7f-163">Tetikleyici olaylar, olaylar, çalıştırmak ve eylem olaylar gibi mantıksal uygulamanızı toofind ve görünüm olayları aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="f4f7f-164">Merhaba, [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="f4f7f-165">"İçin günlük analizi" arayın, ardından seçin **günlük analizi** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   !["Günlük analizi" seçin](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="f4f7f-167">Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS çalışma alanınızı seçin](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="f4f7f-169">Altında **Yönetim**, seçin **OMS portalı**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-169">Under **Management**, choose **OMS Portal**.</span></span>

   !["OMS portalı" seçin](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="f4f7f-171">OMS giriş sayfanızda seçin **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-171">On your OMS home page, choose **Log Search**.</span></span>

   ![OMS giriş sayfanızda "Günlük arama" seçin](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="f4f7f-173">-veya-</span><span class="sxs-lookup"><span data-stu-id="f4f7f-173">-or-</span></span>

   ![Merhaba OMS menüsünde "Günlük arama" öğesini seçin](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="f4f7f-175">Merhaba arama kutusuna, toofind, istediğiniz bir alanı belirtin ve basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="f4f7f-176">Yazmaya başladığınızda, OMS olası eşleşmeler ve kullanabileceğiniz işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="f4f7f-177">Örneğin, toofind hello ilk 10 olayları girin ve bu arama sorgusuna seçin: **kategori WorkflowRuntime = | üst 10**</span><span class="sxs-lookup"><span data-stu-id="f4f7f-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Arama dizesini girin](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="f4f7f-179">Daha fazla bilgi edinmek [nasıl günlük analizi toofind verileri](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="f4f7f-180">Merhaba sonuçları sayfasında hello sol çubuğunda hello zaman dilimi seçin tooview istiyor.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="f4f7f-181">bir filtre ekleyerek sorgunuzu toorefine seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Sorgu sonuçları ilişkin zaman çerçevesini seçin](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="f4f7f-183">Altında **filtreler Ekle**, istediğiniz hello filtre bulabilmesi hello filtre adı girin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="f4f7f-184">Merhaba filtresini seçin ve **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="f4f7f-185">Kullandığı hello word "Durum" toofind Bu örnek altındaki olaylarını başarısız **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="f4f7f-186">Burada, filtre için hello **status_s** zaten seçilidir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Filtreyi seçin](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="f4f7f-188">Hello sol çubuğunda toouse istediğiniz ve seçin hello filtre değeri seçin **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Filtre değeri seçin, "Uygula"](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="f4f7f-190">Şimdi oluşturmakta olduğunuz toohello sorgu döndür.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="f4f7f-191">Sorgunuz seçili filtresi ve değer ile güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="f4f7f-192">Önceki sonuçlarınızı artık çok filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-192">Your previous results are now filtered too.</span></span>

   ![Filtrelenmiş sonuçlar tooyour sorgu döndürme](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="f4f7f-194">Sorgunuz gelecekte kullanım için toosave seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="f4f7f-195">Bilgi [nasıl toosave sorgunuzu](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="f4f7f-196">Nasıl ve tanılama verilerini diğer hizmetleri ile kullandığınız genişletme</span><span class="sxs-lookup"><span data-stu-id="f4f7f-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="f4f7f-197">Azure günlük analizi ile birlikte nasıl mantığı uygulamanızın tanılama verilerini diğer Azure hizmetleriyle örneğin kullandığınız genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="f4f7f-198">Azure depolama alanında Azure tanılama günlüklerini arşiv</span><span class="sxs-lookup"><span data-stu-id="f4f7f-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="f4f7f-199">Akış Azure tanılama günlükleri tooAzure olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="f4f7f-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="f4f7f-200">Telemetri ve diğer hizmetlerden analizi kullanarak izleme Get gerçek zamanlı ister sonra şunları yapabilirsiniz [Azure akış analizi](../stream-analytics/stream-analytics-introduction.md) ve [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="f4f7f-201">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-201">For example:</span></span>

* [<span data-ttu-id="f4f7f-202">Olay hub'ları tooStream Analytics akış verileri</span><span class="sxs-lookup"><span data-stu-id="f4f7f-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="f4f7f-203">Akış Analizi ile akış verilerini çözümleme ve gerçek zamanlı analiz Pano Power BI'da oluşturma</span><span class="sxs-lookup"><span data-stu-id="f4f7f-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="f4f7f-204">Ayarlamak istediğiniz hello seçenekleri bağlı olarak, olduğundan emin olun, ilk [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md) veya [Azure olay hub'ı oluşturma](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="f4f7f-205">Ardından toosend tanılama verilerini istediğiniz hello seçeneklerini seçin:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Veri tooAzure depolama hesabı veya olay hub'ı Gönder](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="f4f7f-207">Yalnızca, bir depolama hesabı toouse'ı seçtiğinizde bekletme dönemleri uygulamak.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="f4f7f-208">Mantıksal uygulamanız için uyarıları ayarlama</span><span class="sxs-lookup"><span data-stu-id="f4f7f-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="f4f7f-209">toomonitor belirli ölçümleri veya mantıksal uygulamanızı aşıldı eşikler ayarlanmış [Azure içindeki uyarıları](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="f4f7f-210">Hakkında bilgi edinin [Azure ölçümlerini](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="f4f7f-211">Uyarılar tooset [Azure günlük analizi](../log-analytics/log-analytics-overview.md), şu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="f4f7f-212">Uyarı ölçütleri ve Eylemler, daha gelişmiş [günlük analizi ayarlamak](#azure-diagnostics) çok.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="f4f7f-213">Merhaba mantığı uygulama dikey menüsünde altında **izleme**, seçin **tanılama** > **uyarı kuralları** > **UyarıEkle**aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Mantıksal uygulamanız için uyarı ekleme](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="f4f7f-215">Hello üzerinde **uyarı kuralı eklemek** dikey penceresinde, uyarı gösterildiği gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="f4f7f-216">Altında **kaynak**, mantıksal uygulamanızı seçin, seçili değilse.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="f4f7f-217">Bir ad ve açıklama için uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="f4f7f-218">Seçin bir **ölçüm** veya tootrack istediğiniz olay.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="f4f7f-219">Seçin bir **koşulu**, belirtin bir **eşik** hello ölçüm ve select hello **süresi** Bu ölçüm izleme.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="f4f7f-220">Toosend posta olup olmadığını hello uyarı için seçin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="f4f7f-221">Diğer tüm e-posta adreslerini hello uyarı göndermek için belirtin.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="f4f7f-222">Toosend hello uyarı istediğiniz bir Web kancası URL'si de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="f4f7f-223">Örneğin, bu kural beş olduğunda bir uyarı gönderir veya daha fazla çalıştığında bir saat içinde başarısız:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Ölçüm uyarı kuralı oluştur](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="f4f7f-225">bir mantıksal uygulama toorun bir uyarıdan hello içerebilir [isteği tetikleyici](../connectors/connectors-native-reqres.md) , iş akışınızı olanak sağlayan bu örnekler gibi görevleri gerçekleştirmenize:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="f4f7f-226">POST tooSlack</span><span class="sxs-lookup"><span data-stu-id="f4f7f-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="f4f7f-227">Bir metin Gönder</span><span class="sxs-lookup"><span data-stu-id="f4f7f-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="f4f7f-228">Bir ileti tooa sırası Ekle</span><span class="sxs-lookup"><span data-stu-id="f4f7f-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="f4f7f-229">Azure Tanılama Olay ayarları ve ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f4f7f-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="f4f7f-230">Mantıksal uygulamanızı ve bu olay, örneğin, hello durumu hakkındaki ayrıntıları her Tanılama Olay sahipse, başlangıç saati, bitiş saati ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="f4f7f-231">İzleme, izleme ve günlüğe kaydetme ayarlama tooprogrammatically ou kullanabilir bu ayrıntıları ile Merhaba [Azure Logic Apps için REST API](https://docs.microsoft.com/rest/api/logic) ve hello [Azure tanılama için REST API](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="f4f7f-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="f4f7f-232">Örneğin, hello `ActionCompleted` olayında hello `clientTrackingId` ve `trackedProperties` izleme ve izleme için kullanabileceğiniz özellikler:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

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

* <span data-ttu-id="f4f7f-233">`clientTrackingId`: Değilse tüm iç içe geçmiş iş akışları dahil olmak üzere Azure otomatik olarak bu kimliği oluşturur ve olayları çalıştırmak bir mantıksal uygulama arasında karşılık gelen sağlanan hello mantığı uygulamadan çağrılan.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="f4f7f-234">Bu kimliği bir tetikleyiciden geçirerek el ile belirtebilirsiniz bir `x-ms-client-tracking-id` üstbilgisi, özel hello tetikleyici isteği kimliği değere sahip.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="f4f7f-235">Bir istek tetikleyici, HTTP tetikleyicisini ya da Web kancası tetikleyici kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="f4f7f-236">`trackedProperties`: tootrack girişleri veya çıkışları tanılama verilerdeki, ekleyebilirsiniz izlenen özellikleri tooactions mantığı uygulamanızın JSON tanımında.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="f4f7f-237">İzlenen özellikleri yalnızca tek bir eylemin girişleri ve çıkışları izleyebilirsiniz, ancak hello kullanabilirsiniz `correlation` çalıştırmada eylemler arasında olayları toocorrelate özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="f4f7f-238">tootrack bir veya daha fazla özellik eklemek hello `trackedProperties` toohello eylem tanımı istediğiniz bölüm ve hello özellikleri.</span><span class="sxs-lookup"><span data-stu-id="f4f7f-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="f4f7f-239">Örneğin, "Düzeni kimliği" gibi tootrack veri, telemetri istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="f4f7f-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f4f7f-240">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f4f7f-240">Next steps</span></span>

* [<span data-ttu-id="f4f7f-241">Mantıksal uygulama dağıtımı için şablonlar oluşturma ve yayın Yönetimi</span><span class="sxs-lookup"><span data-stu-id="f4f7f-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="f4f7f-242">B2B senaryolarını Kurumsal tümleştirme paketi</span><span class="sxs-lookup"><span data-stu-id="f4f7f-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="f4f7f-243">B2B iletilerini izleme</span><span class="sxs-lookup"><span data-stu-id="f4f7f-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)