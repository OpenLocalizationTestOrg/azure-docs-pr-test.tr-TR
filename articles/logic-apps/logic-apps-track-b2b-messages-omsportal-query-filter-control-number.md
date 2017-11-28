---
title: "Operations Management Suite - Azure Logic Apps B2B iletiler için aaaQuery | Microsoft Docs"
description: "Merhaba Operations Management Suite sorguları tootrack AS2, X 12 ve EDIFACT iletileri oluşturma"
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
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="26a96-103">Sorgu için AS2, X 12 ve EDIFACT iletilerinde hello Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="26a96-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="26a96-104">toofind hello AS2, X 12 veya ile takip ettiğiniz EDIFACT iletileri [Azure günlük analizi](../log-analytics/log-analytics-overview.md) hello içinde [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), belirli bağlı eylemleri filtre sorgular oluşturabilirsiniz ölçütleri.</span><span class="sxs-lookup"><span data-stu-id="26a96-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="26a96-105">Örneğin, belirli Değişim Denetimi sayısına bağlı olarak iletileri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26a96-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="26a96-106">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="26a96-106">Requirements</span></span>

* <span data-ttu-id="26a96-107">Tanılama Günlüğü ile ayarlanmış bir mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="26a96-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="26a96-108">Bilgi [nasıl toocreate bir mantıksal uygulama](../logic-apps/logic-apps-create-a-logic-app.md) ve [nasıl tooset bu mantıksal uygulama günlüklerini](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="26a96-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="26a96-109">İzleme ve günlük ile ayarlanan bir tümleştirme hesabı.</span><span class="sxs-lookup"><span data-stu-id="26a96-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="26a96-110">Bilgi [nasıl toocreate bir tümleştirme hesap](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) ve [nasıl izleme ve o hesap için oturum tooset](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="26a96-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="26a96-111">Henüz yapmadıysanız [tanılama veri tooLog Analytics yayımlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) ve [ileti OMS içinde izleme ayarlama](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="26a96-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="26a96-112">Merhaba önceki gereksinimlerini karşılamanızın sonra hello çalışma olmalıdır [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="26a96-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="26a96-113">Kullanmanız gereken Merhaba, OMS B2B iletişiminde izleme için aynı OMS çalışma.</span><span class="sxs-lookup"><span data-stu-id="26a96-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="26a96-114">Bir OMS çalışma alanı yoksa, bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="26a96-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="26a96-115">Merhaba Operations Management Suite portalına filtreleri ile iletisi sorguları oluşturma</span><span class="sxs-lookup"><span data-stu-id="26a96-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="26a96-116">Bu örnek, değişim denetimi numarasına göre iletileri nasıl bulabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="26a96-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="26a96-117">OMS çalışma alanı adınız biliyorsanız, tooyour çalışma giriş sayfasına gidin (`https://{your-workspace-name}.portal.mms.microsoft.com`) ve adım 4 olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="26a96-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="26a96-118">Aksi takdirde, adım 1'den başlar.</span><span class="sxs-lookup"><span data-stu-id="26a96-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="26a96-119">Merhaba, [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="26a96-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="26a96-120">"İçin günlük analizi" araması yapın ve ardından **günlük analizi** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="26a96-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Günlük analizi Bul](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="26a96-122">Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="26a96-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![OMS çalışma alanınızı seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="26a96-124">Altında **Yönetim**, seçin **OMS portalı**.</span><span class="sxs-lookup"><span data-stu-id="26a96-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![OMS portalı seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="26a96-126">OMS giriş sayfanızda seçin **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="26a96-126">On your OMS home page, choose **Log Search**.</span></span>

   ![OMS giriş sayfanızda "Günlük arama" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="26a96-128">-veya-</span><span class="sxs-lookup"><span data-stu-id="26a96-128">-or-</span></span>

   ![Merhaba OMS menüsünde "Günlük arama" öğesini seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="26a96-130">Toofind, istediğiniz bir alanı Hello arama kutusuna girin ve basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="26a96-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="26a96-131">Yazmaya başladığınızda, OMS olası eşleşmeler ve kullanabileceğiniz işlemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="26a96-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="26a96-132">Daha fazla bilgi edinmek [nasıl günlük analizi toofind verileri](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="26a96-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="26a96-133">Bu örnekte arama olan olaylar için **türü AzureDiagnostics =**.</span><span class="sxs-lookup"><span data-stu-id="26a96-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Sorgu dizesi yazmaya başlayın](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="26a96-135">Merhaba sol çubuğunda hello zaman dilimi seçin tooview istiyor.</span><span class="sxs-lookup"><span data-stu-id="26a96-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="26a96-136">tooadd bir filtre tooyour sorgu seçin **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="26a96-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Filtre tooquery Ekle](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="26a96-138">Altında **filtreler Ekle**, istediğiniz hello filtre bulabilmesi hello filtre adı girin.</span><span class="sxs-lookup"><span data-stu-id="26a96-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="26a96-139">Merhaba filtresini seçin ve **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="26a96-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="26a96-140">toofind hello değiş tokuş denetim numarası, bu örnek için "değişim" Merhaba word arar ve seçer **event_record_messageProperties_interchangeControlNumber_s** hello filtre olarak.</span><span class="sxs-lookup"><span data-stu-id="26a96-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Filtreyi seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="26a96-142">Hello sol çubuğunda toouse istediğiniz ve seçin hello filtre değeri seçin **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="26a96-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="26a96-143">Bu örnek hello değiş tokuş denetim numarası istiyoruz Merhaba iletileri için seçer.</span><span class="sxs-lookup"><span data-stu-id="26a96-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Filtre değeri seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="26a96-145">Şimdi oluşturmakta olduğunuz toohello sorgu döndür.</span><span class="sxs-lookup"><span data-stu-id="26a96-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="26a96-146">Sorgunuz seçilen filtre olay ve değeri ile güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="26a96-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="26a96-147">Önceki sonuçlarınızı artık çok filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="26a96-147">Your previous results are now filtered too.</span></span>

    ![Filtrelenmiş sonuçlar tooyour sorgu döndürme](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="26a96-149">Sorgunuz gelecekte kullanım için Kaydet</span><span class="sxs-lookup"><span data-stu-id="26a96-149">Save your query for future use</span></span>

1. <span data-ttu-id="26a96-150">Sorgunuzu hello üzerinde gelen **günlük arama** sayfasında, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="26a96-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="26a96-151">Sorgunuz bir ad verin, bir kategori seçin ve **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="26a96-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Bir ad ve kategori sorgunuz verin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="26a96-153">tooview Sorgunuzdaki seçin **Sık Kullanılanlar**.</span><span class="sxs-lookup"><span data-stu-id="26a96-153">tooview your query, choose **Favorites**.</span></span>

   !["Sık Kullanılanlar" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="26a96-155">Altında **kayıtlı aramaları**, sorgunuzu hello sonuçları görüntüleyebilmesi için seçin.</span><span class="sxs-lookup"><span data-stu-id="26a96-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="26a96-156">farklı sonuçlar bulabilmesi tooupdate hello sorgu hello sorgu düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="26a96-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Sorgunuz seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="26a96-158">Bulma ve hello Operations Management Suite Portalı'nda kayıtlı sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="26a96-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="26a96-159">OMS çalışma giriş sayfanız açın (`https://{your-workspace-name}.portal.mms.microsoft.com`) ve seçin **günlük arama**.</span><span class="sxs-lookup"><span data-stu-id="26a96-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![OMS giriş sayfanızda "Günlük arama" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="26a96-161">-veya-</span><span class="sxs-lookup"><span data-stu-id="26a96-161">-or-</span></span>

   ![Merhaba OMS menüsünde "Günlük arama" öğesini seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="26a96-163">Merhaba üzerinde **günlük arama** giriş sayfasını, seçin **Sık Kullanılanlar**.</span><span class="sxs-lookup"><span data-stu-id="26a96-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   !["Sık Kullanılanlar" seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="26a96-165">Altında **kayıtlı aramaları**, sorgunuzu hello sonuçları görüntüleyebilmesi için seçin.</span><span class="sxs-lookup"><span data-stu-id="26a96-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="26a96-166">farklı sonuçlar bulabilmesi tooupdate hello sorgu hello sorgu düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="26a96-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Sorgunuz seçin](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="26a96-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26a96-168">Next steps</span></span>

* [<span data-ttu-id="26a96-169">AS2 izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="26a96-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="26a96-170">X12 izleme şemaları</span><span class="sxs-lookup"><span data-stu-id="26a96-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="26a96-171">Özel İzleme şemaları</span><span class="sxs-lookup"><span data-stu-id="26a96-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)