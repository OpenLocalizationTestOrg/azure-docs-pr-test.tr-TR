---
title: "İzleyici ve get Öngörüler mantıksal uygulamanızı hakkında çalıştıran OMS - Azure mantıksal uygulamaları kullanma | Microsoft Docs"
description: "Mantıksal uygulama çalışmalarınız sorun giderme ve tanılama için Öngörüler ve daha zengin hata ayıklama ayrıntılarını almak için günlük analizi ve Operations Management Suite (OMS) ile izleme"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: 0e9f0ef3c87b5c0da1cc4ad16d37178c8f5c9625
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="20dc2-103">İzleyici ve get Öngörüler mantıksal uygulama hakkında Operations Management Suite (OMS) ve günlük analizi ile çalışır</span><span class="sxs-lookup"><span data-stu-id="20dc2-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="20dc2-104">İzleme ve daha zengin hata ayıklama bilgileri almak için bir mantıksal uygulama oluşturduğunuzda, aynı anda günlük analizi kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20dc2-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="20dc2-105">Günlük analizi günlüğe kaydetme ve izleme mantığı uygulamanız için tanılama Operations Management Suite (OMS) portalı üzerinden çalışan sağlar.</span><span class="sxs-lookup"><span data-stu-id="20dc2-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="20dc2-106">Logic Apps yönetim çözümü için OMS eklediğinizde, logic app çalıştırır ve durumu, yürütme süresi, yeniden gönderme durumu ve bağıntı kimlikleri gibi belirli Ayrıntılar için toplanan durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="20dc2-106">When you add the Logic Apps Management solution to OMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="20dc2-107">Bu konu, günlük analizi kapatabilir veya çalıştırmak mantığı uygulamanız için çalışma zamanı olayları ve veri görüntüleyebilmeniz için Logic Apps yönetimi çözümü içinde OMS yükleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="20dc2-107">This topic shows how to turn on Log Analytics or install the Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="20dc2-108">Mevcut mantıksal uygulamalarınızı izlemek için aşağıdaki adımları izleyin [tanılama günlük özelliğini açar ve mantığı uygulama çalışma zamanı veri göndermek için OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="20dc2-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="20dc2-109">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="20dc2-109">Requirements</span></span>

<span data-ttu-id="20dc2-110">Başlamadan önce OMS çalışma alanınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="20dc2-110">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="20dc2-111">Bilgi [bir OMS çalışma alanı oluşturmak nasıl](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="20dc2-111">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="20dc2-112">Logic apps oluştururken tanılama günlüğünü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="20dc2-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="20dc2-113">İçinde [Azure portal](https://portal.azure.com), bir mantıksal uygulama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="20dc2-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="20dc2-114">Seçin **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama** > **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Mantıksal uygulama oluşturma](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="20dc2-116">İçinde **oluşturma mantıksal uygulama** sayfasında, gösterildiği gibi bu görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="20dc2-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="20dc2-117">Mantıksal uygulamanız için bir ad ve Azure aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="20dc2-118">Bir Azure kaynak grubu seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20dc2-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="20dc2-119">Ayarlama **oturum Analytics** için **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="20dc2-120">Mantıksal uygulamanız için veri çalıştıran göndermek istediğiniz OMS çalışma alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-120">Select the OMS workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="20dc2-121">Hazır olduğunuzda, seçin **panoya Sabitle** > **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![Mantıksal uygulama oluşturma](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="20dc2-123">Bu adımı tamamladıktan sonra artık mantıksal uygulamanızı Azure oluşturur, OMS çalışma alanıyla ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="20dc2-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="20dc2-124">Ayrıca, bu adım OMS çalışma alanınızda Logic Apps yönetimi çözümü de otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="20dc2-124">Also, this step also automatically installs the Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="20dc2-125">Mantığınızı görüntülemek için uygulamanın OMS içinde çalıştığı [bu adımlarla devam](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="20dc2-125">To view your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution-in-oms"></a><span data-ttu-id="20dc2-126">Logic Apps yönetimi çözümü içinde OMS yükleyin</span><span class="sxs-lookup"><span data-stu-id="20dc2-126">Install the Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="20dc2-127">Mantıksal uygulamanızı oluşturduğunuzda günlük analizi zaten etkinleştirdiyseniz, bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="20dc2-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="20dc2-128">Logic Apps yönetimi çözümü içinde OMS yüklenmiş zaten var.</span><span class="sxs-lookup"><span data-stu-id="20dc2-128">You already have the Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="20dc2-129">İçinde [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="20dc2-130">Filtre olarak "günlük analizi" arayın ve seçin **günlük analizi** gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="20dc2-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   !["Günlük analizi" seçin](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="20dc2-132">Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS çalışma alanınızı seçin](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="20dc2-134">Altında **Yönetim**, seçin **OMS portalı**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-134">Under **Management**, choose **OMS Portal**.</span></span>

   !["OMS portalı" seçin](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="20dc2-136">Yükseltme başlık görünürse, OMS sayfanız, OMS çalışma yükseltmeniz başlığı seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-136">On your OMS homepage, if the upgrade banner appears, choose the banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="20dc2-137">Ardından **Çözümleri Galerisi**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-137">Then choose **Solutions Gallery**.</span></span>

   !["Çözümleri Galerisi" seçin](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="20dc2-139">Altında **tüm çözümleri**, bulmak ve seçmek için döşeme **Logic Apps Yönetim** çözümü.</span><span class="sxs-lookup"><span data-stu-id="20dc2-139">Under **All solutions**, find and choose the tile for the **Logic Apps Management** solution.</span></span>

   !["Logic Apps Yönetimi" seçin](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="20dc2-141">OMS çalışma alanınızda çözümü yüklemek için tercih **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-141">To install the solution in your OMS workspace, choose **Add**.</span></span>

   !["" Logic Apps yönetimi için"Ekle" yi seçin](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="20dc2-143">OMS çalışma alanınızda mantıksal uygulamanızı çalıştıran görünümü</span><span class="sxs-lookup"><span data-stu-id="20dc2-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="20dc2-144">Sayısı ve logic app çalışmalarınız durumunu görüntülemek için OMS çalışma alanınız için genel bakış sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-144">To view the count and status for your logic app runs, go to the overview page for your OMS workspace.</span></span> <span data-ttu-id="20dc2-145">Ayrıntıları gözden **Logic Apps Yönetim** döşeme.</span><span class="sxs-lookup"><span data-stu-id="20dc2-145">Review the details on the **Logic Apps Management** tile.</span></span>

   ![Mantığı çalıştırmak uygulama sayısı ve durumunu gösteren genel bakış kutucuğu](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="20dc2-147">Bu yükseltme başlık yerine Logic Apps yönetim döşeme görünürse, böylece OMS çalışma alanınızı yükseltmeniz başlığını seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-147">If this upgrade banner appears instead of the Logic Apps Management tile, choose the banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Yükseltme "OMS çalışma"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="20dc2-149">Bir Özet mantığı uygulama çalışmalarınız hakkında daha fazla ayrıntı görüntülemek için seçin **Logic Apps Yönetim** döşeme.</span><span class="sxs-lookup"><span data-stu-id="20dc2-149">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="20dc2-150">Burada, logic app çalışmalarınız adına veya yürütme durumu göre gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="20dc2-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Mantıksal uygulamanız için Özet durum çalıştırır](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="20dc2-152">Belirli mantıksal uygulama ya da durum için tüm çalıştırmalarını görüntülemek için bir mantıksal uygulama veya bir durum için satır seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-152">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="20dc2-153">Belirli mantıksal uygulama için tüm çalıştırmalarını gösteren bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="20dc2-153">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![Bir mantıksal uygulama veya bir durum görünümü çalıştırır](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="20dc2-155">**Yeniden gönderme** sütun yeniden gönderilen bir çalıştırma sonucu çalışmaları için "Evet" gösterir.</span><span class="sxs-lookup"><span data-stu-id="20dc2-155">The **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="20dc2-156">Bu sonuçları filtrelemek için istemci tarafı ve sunucu tarafı filtreleme gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20dc2-156">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="20dc2-157">İstemci tarafı filtresi: her sütun için istediğiniz filtreleri seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-157">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="20dc2-158">İşte bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="20dc2-158">Here are some examples:</span></span>

     ![Örnek sütun filtreleri](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="20dc2-160">Sunucu tarafı filtresi: belirli bir zaman penceresinin seçin ya da görünür çalıştırmalarının sayısını sınırlamak için sayfanın en üstünde kapsam denetimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="20dc2-160">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="20dc2-161">Varsayılan olarak, aynı anda yalnızca 1.000 kayıtları görünür.</span><span class="sxs-lookup"><span data-stu-id="20dc2-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Değişiklik zaman penceresi](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="20dc2-163">Tüm Eylemler ve bunların belirli bir çalışma ayrıntılarını görüntülemek için günlük arama sayfası açılır bir satır seçin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-163">To view all the actions and their details for a specific run, select a row, which opens the Log Search page.</span></span> 

   * <span data-ttu-id="20dc2-164">Bir tablodaki bu bilgileri görüntülemek için seçin **tablo**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-164">To view this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="20dc2-165">Sorguyu değiştirmek için arama çubuğunda sorgu dizesi düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20dc2-165">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="20dc2-166">Daha iyi bir deneyim için seçin **Advanced Analytics**.</span><span class="sxs-lookup"><span data-stu-id="20dc2-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Eylemler ve Çalıştır bir mantıksal uygulama ayrıntılarını görüntüleyin](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="20dc2-168">Burada Azure günlük analizi sayfasında sorguları güncelleştirebilirsiniz ve tablodan sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="20dc2-168">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="20dc2-169">Bu sorgu kullanır [Kusto sorgu dili](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), farklı sonuçlar görüntülemek istiyorsanız, düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20dc2-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want to view different results.</span></span> 

     ![Azure günlük analizi - sorgu görünümü](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="20dc2-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20dc2-171">Next steps</span></span>

* [<span data-ttu-id="20dc2-172">B2B iletilerini izleme</span><span class="sxs-lookup"><span data-stu-id="20dc2-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
