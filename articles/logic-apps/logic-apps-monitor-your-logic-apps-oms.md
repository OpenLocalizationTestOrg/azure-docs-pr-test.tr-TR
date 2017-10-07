---
title: "mantıksal uygulamanızı hakkında aaaMonitor ve get Öngörüler çalıştıran OMS - Azure mantıksal uygulamaları kullanma | Microsoft Docs"
description: "Logic app çalışmalarınız günlük analizi ve Operations Management Suite (OMS) tooget Öngörüler ve sorun giderme ve tanılama daha zengin hata ayıklama ayrıntılarını ile izleme"
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
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="1d91d-103">İzleyici ve get Öngörüler mantıksal uygulama hakkında Operations Management Suite (OMS) ve günlük analizi ile çalışır</span><span class="sxs-lookup"><span data-stu-id="1d91d-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="1d91d-104">İzleme ve daha zengin hata ayıklama bilgileri almak için günlük analizi hello kapatabilirsiniz bir mantıksal uygulama'ı oluşturduğunuzda aynı zamanda.</span><span class="sxs-lookup"><span data-stu-id="1d91d-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="1d91d-105">Günlük analizi günlüğe kaydetme ve izleme mantığı uygulamanız için tanılama hello Operations Management Suite (OMS) portalı üzerinden çalışan sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d91d-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="1d91d-106">Merhaba Logic Apps yönetim çözümü tooOMS eklediğinizde, logic app çalıştırır ve durumu, yürütme süresi, yeniden gönderme durumu ve bağıntı kimlikleri gibi belirli Ayrıntılar için toplanan durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="1d91d-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="1d91d-107">Bu konu, nasıl tooturn günlük analizi veya yükleme hello Logic Apps yönetim çözümüne OMS çalışma olaylarını görüntüleyebilir ve veri mantığı uygulamanız için çalıştırmaları için gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d91d-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="1d91d-108">toomonitor mevcut mantıksal uygulamalarınızı adımları çok [tanılama günlük özelliğini açar ve mantığı uygulama çalışma zamanı verileri tooOMS Gönder](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="1d91d-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="1d91d-109">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="1d91d-109">Requirements</span></span>

<span data-ttu-id="1d91d-110">Başlamadan önce toohave bir OMS çalışma alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d91d-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="1d91d-111">Bilgi [nasıl toocreate bir OMS çalışma](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1d91d-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="1d91d-112">Logic apps oluştururken tanılama günlüğünü etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1d91d-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="1d91d-113">İçinde [Azure portal](https://portal.azure.com), bir mantıksal uygulama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1d91d-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="1d91d-114">Seçin **yeni** > **Kurumsal tümleştirme** > **mantıksal uygulama** > **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Mantıksal uygulama oluşturma](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="1d91d-116">Merhaba, **oluşturma mantıksal uygulama** sayfasında, gösterildiği gibi bu görevleri gerçekleştirmek:</span><span class="sxs-lookup"><span data-stu-id="1d91d-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="1d91d-117">Mantıksal uygulamanız için bir ad ve Azure aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="1d91d-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="1d91d-118">Bir Azure kaynak grubu seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1d91d-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="1d91d-119">Ayarlama **günlük analizi** çok**üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="1d91d-120">Çok mantığı uygulamanız için veri göndermek istediğiniz yeri seçin hello OMS çalışma çalışır.</span><span class="sxs-lookup"><span data-stu-id="1d91d-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="1d91d-121">Hazır olduğunuzda, seçin **PIN toodashboard** > **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Mantıksal uygulama oluşturma](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="1d91d-123">Bu adımı tamamladıktan sonra artık mantıksal uygulamanızı Azure oluşturur, OMS çalışma alanıyla ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="1d91d-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="1d91d-124">Ayrıca, bu adım OMS çalışma alanınızda hello Logic Apps yönetimi çözümü de otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="1d91d-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="1d91d-125">mantıksal uygulamanızı çalıştıran OMS içinde tooview [bu adımlarla devam](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="1d91d-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="1d91d-126">Merhaba Logic Apps yönetimi çözümü içinde OMS yükleyin</span><span class="sxs-lookup"><span data-stu-id="1d91d-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="1d91d-127">Mantıksal uygulamanızı oluşturduğunuzda günlük analizi zaten etkinleştirdiyseniz, bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="1d91d-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="1d91d-128">Merhaba Logic Apps yönetimi çözümü içinde OMS yüklenmiş zaten var.</span><span class="sxs-lookup"><span data-stu-id="1d91d-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="1d91d-129">Merhaba, [Azure portal](https://portal.azure.com), seçin **daha Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="1d91d-130">Filtre olarak "günlük analizi" arayın ve seçin **günlük analizi** gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="1d91d-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   !["Günlük analizi" seçin](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="1d91d-132">Altında **günlük analizi**, bulma ve OMS çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="1d91d-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![OMS çalışma alanınızı seçin](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="1d91d-134">Altında **Yönetim**, seçin **OMS portalı**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-134">Under **Management**, choose **OMS Portal**.</span></span>

   !["OMS portalı" seçin](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="1d91d-136">Merhaba yükseltme başlık görünürse, OMS sayfanız OMS çalışma alanınızı yükseltmeniz hello başlığı seçin.</span><span class="sxs-lookup"><span data-stu-id="1d91d-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="1d91d-137">Ardından **Çözümleri Galerisi**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-137">Then choose **Solutions Gallery**.</span></span>

   !["Çözümleri Galerisi" seçin](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="1d91d-139">Altında **tüm çözümleri**, bulun ve hello bölme hello için seçin **Logic Apps Yönetim** çözümü.</span><span class="sxs-lookup"><span data-stu-id="1d91d-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   !["Logic Apps Yönetimi" seçin](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="1d91d-141">OMS çalışma alanınızdaki tooinstall hello çözümü seçme **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   !["" Logic Apps yönetimi için"Ekle" yi seçin](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="1d91d-143">OMS çalışma alanınızda mantıksal uygulamanızı çalıştıran görünümü</span><span class="sxs-lookup"><span data-stu-id="1d91d-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="1d91d-144">tooview hello sayısı ve mantıksal uygulamanızı durumunun gidin toohello genel bakış sayfasında OMS çalışma alanınız için çalışır.</span><span class="sxs-lookup"><span data-stu-id="1d91d-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="1d91d-145">Merhaba hello ayrıntıları gözden **Logic Apps Yönetim** döşeme.</span><span class="sxs-lookup"><span data-stu-id="1d91d-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Mantığı çalıştırmak uygulama sayısı ve durumunu gösteren genel bakış kutucuğu](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="1d91d-147">Bu yükseltme başlık hello Logic Apps yönetim döşeme yerine görünürse, böylece OMS çalışma alanınızı yükseltmeniz hello başlığını seçin.</span><span class="sxs-lookup"><span data-stu-id="1d91d-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Yükseltme "OMS çalışma"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="1d91d-149">tooview mantığı uygulama çalışmalarınız hakkında daha fazla ayrıntı özeti seçin hello **Logic Apps Yönetim** döşeme.</span><span class="sxs-lookup"><span data-stu-id="1d91d-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="1d91d-150">Burada, logic app çalışmalarınız adına veya yürütme durumu göre gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="1d91d-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Mantıksal uygulamanız için Özet durum çalıştırır](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="1d91d-152">belirli mantıksal uygulama veya durum, bir mantıksal uygulama veya bir durum için select hello satır için tüm hello tooview çalışır.</span><span class="sxs-lookup"><span data-stu-id="1d91d-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="1d91d-153">Belirli mantıksal uygulama için tüm hello çalıştırmalarını gösteren bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1d91d-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Bir mantıksal uygulama veya bir durum görünümü çalıştırır](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="1d91d-155">Merhaba **yeniden gönderme** sütun yeniden gönderilen bir çalıştırma sonucu çalışmaları için "Evet" gösterir.</span><span class="sxs-lookup"><span data-stu-id="1d91d-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="1d91d-156">Bu sonuçları toofilter, istemci tarafı ve sunucu tarafı filtreleme gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d91d-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="1d91d-157">İstemci tarafı filtresi: her sütun için istediğiniz hello filtrelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="1d91d-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="1d91d-158">İşte bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="1d91d-158">Here are some examples:</span></span>

     ![Örnek sütun filtreleri](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="1d91d-160">Sunucu tarafı filtresi: toochoose belirli bir zaman penceresi veya toolimit hello çeşitli görüntülenir, hello sayfanın üst kısmındaki hello kullan hello kapsam denetim çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1d91d-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="1d91d-161">Varsayılan olarak, aynı anda yalnızca 1.000 kayıtları görünür.</span><span class="sxs-lookup"><span data-stu-id="1d91d-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Değişiklik hello zaman penceresi](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="1d91d-163">Tüm tooview hello günlük arama sayfası açılır bir satır Eylemler ve bunların ayrıntılarını belirli bir çalışma, select hello.</span><span class="sxs-lookup"><span data-stu-id="1d91d-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="1d91d-164">Bu bilgileri bir tabloda tooview seçme **tablo**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="1d91d-165">toochange hello sorgu hello sorgu dizesi hello arama çubuğunda düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d91d-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="1d91d-166">Daha iyi bir deneyim için seçin **Advanced Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1d91d-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Eylemler ve Çalıştır bir mantıksal uygulama ayrıntılarını görüntüleyin](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="1d91d-168">Burada hello Azure günlük analizi sayfasında, sorgular ve görünüm güncelleştirebilirsiniz hello hello tablosundan sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="1d91d-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="1d91d-169">Bu sorgu kullanan [Kusto sorgu dili](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), tooview farklı sonuçlar istiyorsanız düzenleyebileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="1d91d-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure günlük analizi - sorgu görünümü](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="1d91d-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d91d-171">Next steps</span></span>

* [<span data-ttu-id="1d91d-172">B2B iletilerini izleme</span><span class="sxs-lookup"><span data-stu-id="1d91d-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
