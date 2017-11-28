---
title: "B2B hareketlerini izlemek ve günlük - Azure Logic Apps ayarlama | Microsoft Docs"
description: "İzleyici AS2, X 12 ve EDIFACT iletileri tümleştirme hesabınız için tanılama günlüğünü Başlat"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="fc53e-103">İzleme ve tanılama günlüklerini tümleştirme hesaplarındaki B2B iletişimi için ayarlayın</span><span class="sxs-lookup"><span data-stu-id="fc53e-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="fc53e-104">İkisi arasındaki B2B iletişim kurduktan sonra iş süreçlerini veya tümleştirme hesabınızı aracılığıyla uygulamaları çalıştıran bu varlıkların birbirleriyle iletileri değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="fc53e-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="fc53e-105">Bu iletişim beklendiği gibi çalıştığından, AS2, X12, izleme işlevini ayarlama ve tümleştirme hesabınız üzerinden için tanılama günlüğünü birlikte EDIFACT iletileri onaylamak için [Azure günlük analizi](../log-analytics/log-analytics-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="fc53e-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="fc53e-106">Bu hizmet [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) bulut izler ve şirket içi ortamları, bunların kullanılabilirlik ve performans, tutmanıza yardımcı olur ve ayrıca çalışma zamanı Ayrıntılar ve daha zengin hata ayıklama olaylarını toplar.</span><span class="sxs-lookup"><span data-stu-id="fc53e-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="fc53e-107">Ayrıca [diğer hizmetlerle tanılama verilerinizi kullanma](#extend-diagnostic-data)Azure Storage ve Azure Event Hubs gibi.</span><span class="sxs-lookup"><span data-stu-id="fc53e-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="fc53e-108">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="fc53e-108">Requirements</span></span>

* <span data-ttu-id="fc53e-109">Tanılama Günlüğü ile ayarlanmış bir mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="fc53e-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="fc53e-110">Bilgi [bu mantıksal uygulama için günlük kaydını ayarlamak nasıl](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="fc53e-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="fc53e-111">Bu gereksinim karşılamanızın sonra bir çalışma alanı olmalıdır [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="fc53e-112">Tümleştirme hesabınız için günlüğü ayarlarken aynı OMS çalışma kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc53e-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="fc53e-113">Bir OMS çalışma alanı yoksa, bilgi [bir OMS çalışma alanı oluşturmak nasıl](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="fc53e-114">Mantıksal uygulamanızı bağlantılı bir tümleştirme hesabı.</span><span class="sxs-lookup"><span data-stu-id="fc53e-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="fc53e-115">Bilgi [mantıksal uygulamanızı bağlantı tümleştirme hesap oluşturmak nasıl](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="fc53e-116">Tanılama tümleştirme hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="fc53e-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="fc53e-117">Doğrudan tümleştirme hesabınızdan ya da günlük özelliğini açın veya [Azure İzleyicisi hizmeti aracılığıyla](#azure-monitor-service).</span><span class="sxs-lookup"><span data-stu-id="fc53e-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="fc53e-118">Azure İzleyicisi temel altyapı düzeyinde verilerle izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc53e-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="fc53e-119">Daha fazla bilgi edinmek [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="fc53e-120">Tanılama tümleştirme hesabınızdan doğrudan oturum aç</span><span class="sxs-lookup"><span data-stu-id="fc53e-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="fc53e-121">İçinde [Azure portal](https://portal.azure.com), bulma ve tümleştirme hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="fc53e-122">Altında **izleme**, seçin **tanılama günlükleri** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="fc53e-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![Bulma ve tümleştirme hesabınızı seçin, "Tanılama günlükleri"](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="fc53e-124">Tümleştirme hesabınızı seçtikten sonra aşağıdaki değerleri otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="fc53e-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="fc53e-125">Bu değerler doğru olup olmadığını seçin **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="fc53e-126">Aksi takdirde, istediğiniz değerleri seçin:</span><span class="sxs-lookup"><span data-stu-id="fc53e-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="fc53e-127">Altında **abonelik**, tümleştirme hesabınızla kullandığınız Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="fc53e-128">Altında **kaynak grubu**, tümleştirme hesabınızla kullandığınız kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="fc53e-129">Altında **kaynak türü**seçin **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="fc53e-130">Altında **kaynak**, tümleştirme hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="fc53e-131">Seçin **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-131">Choose **Turn on diagnostics**.</span></span>

   ![Tanılama tümleştirme hesabınız için ayarlama](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="fc53e-133">Altında **tanılama ayarları**ve ardından **durum**, seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Azure tanılamayı açın](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="fc53e-135">Şimdi gösterildiği gibi günlük için kullanılacak veri ve OMS çalışma alanını seçin:</span><span class="sxs-lookup"><span data-stu-id="fc53e-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="fc53e-136">Seçin **için günlük analizi Gönder**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="fc53e-137">Altında **günlük analizi**, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="fc53e-138">Altında **OMS çalışma alanları**, günlük için kullanılacak OMS çalışma alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="fc53e-139">Altında **günlük**seçin **IntegrationAccountTrackingEvents** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="fc53e-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="fc53e-140">**Kaydet**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-140">Choose **Save**.</span></span>

   ![Tanılama verilerini günlüğe gönderebilmek için günlük analizi ayarlayın](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="fc53e-142">Şimdi [OMS B2B iletilerinizi izleme ayarlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="fc53e-143">Tanılama günlükleri Azure İzleyicisi üzerinden Aç</span><span class="sxs-lookup"><span data-stu-id="fc53e-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="fc53e-144">İçinde [Azure portal](https://portal.azure.com), ana Azure menüsünde, **İzleyici**, **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="fc53e-145">Ardından aşağıda gösterildiği gibi tümleştirme hesabınızı seçin:</span><span class="sxs-lookup"><span data-stu-id="fc53e-145">Then select your integration account as shown here:</span></span>

   !["İzleme", "Tanılama günlükleri" seçin tümleştirme hesabınızı seçin](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="fc53e-147">Tümleştirme hesabınızı seçtikten sonra aşağıdaki değerleri otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="fc53e-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="fc53e-148">Bu değerler doğru olup olmadığını seçin **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="fc53e-149">Aksi takdirde, istediğiniz değerleri seçin:</span><span class="sxs-lookup"><span data-stu-id="fc53e-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="fc53e-150">Altında **abonelik**, tümleştirme hesabınızla kullandığınız Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="fc53e-151">Altında **kaynak grubu**, tümleştirme hesabınızla kullandığınız kaynak grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="fc53e-152">Altında **kaynak türü**seçin **tümleştirme hesapları**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="fc53e-153">Altında **kaynak**, tümleştirme hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="fc53e-154">Seçin **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-154">Choose **Turn on diagnostics**.</span></span>

   ![Tanılama tümleştirme hesabınız için ayarlama](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="fc53e-156">Altında **tanılama ayarları**, seçin **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Azure tanılamayı açın](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="fc53e-158">Şimdi gösterildiği gibi günlüğe kaydetme için OMS çalışma ve olay kategorisi seçin:</span><span class="sxs-lookup"><span data-stu-id="fc53e-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="fc53e-159">Seçin **için günlük analizi Gönder**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="fc53e-160">Altında **günlük analizi**, seçin **yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="fc53e-161">Altında **OMS çalışma alanları**, günlük için kullanılacak OMS çalışma alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="fc53e-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="fc53e-162">Altında **günlük**seçin **IntegrationAccountTrackingEvents** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="fc53e-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="fc53e-163">İşiniz bittiğinde seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fc53e-163">When you're done, choose **Save**.</span></span>

   ![Tanılama verilerini günlüğe gönderebilmek için günlük analizi ayarlayın](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="fc53e-165">Şimdi [OMS B2B iletilerinizi izleme ayarlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="fc53e-166">Nasıl ve tanılama verilerini diğer hizmetleri ile kullandığınız genişletme</span><span class="sxs-lookup"><span data-stu-id="fc53e-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="fc53e-167">Azure günlük analizi ile birlikte nasıl mantığı uygulamanızın tanılama verilerini diğer Azure hizmetleriyle örneğin kullandığınız genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fc53e-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="fc53e-168">Azure depolama alanında Azure tanılama günlüklerini arşiv</span><span class="sxs-lookup"><span data-stu-id="fc53e-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="fc53e-169">Azure Event hubs'a akış Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="fc53e-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="fc53e-170">Telemetri ve diğer hizmetlerden analizi kullanarak izleme Get gerçek zamanlı ister sonra şunları yapabilirsiniz [Azure akış analizi](../stream-analytics/stream-analytics-introduction.md) ve [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="fc53e-171">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fc53e-171">For example:</span></span>

* [<span data-ttu-id="fc53e-172">Event Hubs akış verilerini akış analizi</span><span class="sxs-lookup"><span data-stu-id="fc53e-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="fc53e-173">Akış Analizi ile akış verilerini çözümleme ve gerçek zamanlı analiz Pano Power BI'da oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc53e-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="fc53e-174">Ayarlamak istediğiniz seçenekleri bağlı olarak, olduğundan emin olun, ilk [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md) veya [Azure olay hub'ı oluşturma](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="fc53e-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="fc53e-175">Ardından Tanılama verileri gönder istediğiniz seçenekleri seçin:</span><span class="sxs-lookup"><span data-stu-id="fc53e-175">Then select the options for where you want to send diagnostic data:</span></span>

![Verileri Azure depolama hesabı veya olay hub'ına Gönder](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="fc53e-177">Yalnızca bir depolama hesabı kullanmayı seçtiğinizde bekletme dönemleri uygulamak.</span><span class="sxs-lookup"><span data-stu-id="fc53e-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="fc53e-178">Desteklenen izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="fc53e-178">Supported tracking schemas</span></span>

<span data-ttu-id="fc53e-179">Azure bunlar tüm özel türü dışında şemaları sabit şema türleri, izleme destekler.</span><span class="sxs-lookup"><span data-stu-id="fc53e-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="fc53e-180">AS2 izleme şeması</span><span class="sxs-lookup"><span data-stu-id="fc53e-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="fc53e-181">X12 izleme şeması</span><span class="sxs-lookup"><span data-stu-id="fc53e-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="fc53e-182">Özel izleme şeması</span><span class="sxs-lookup"><span data-stu-id="fc53e-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="fc53e-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc53e-183">Next steps</span></span>

* [<span data-ttu-id="fc53e-184">OMS B2B iletilerini izlemek</span><span class="sxs-lookup"><span data-stu-id="fc53e-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "OMS izleme B2B iletileri")
* [<span data-ttu-id="fc53e-185">Enterprise Integration Pack hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="fc53e-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Enterprise Integration Pack hakkında bilgi edinin")

