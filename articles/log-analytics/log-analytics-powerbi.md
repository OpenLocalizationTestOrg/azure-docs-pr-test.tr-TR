---
title: "aaaExport günlük analizi veri tooPower BI | Microsoft Docs"
description: "Power BI bir zengin Görselleştirmelerini ve raporları farklı veri kümelerinin analize sağlayan bir Microsoft bulut tabanlı iş analiz hizmetidir.  Görselleştirmeleri ve çözümleme araçları yararlanabilirsiniz şekilde günlük analizi sürekli olarak veri hello OMS depodan Power BI'a aktarabilirsiniz.  Bu makalede nasıl tooconfigure tooPower BI düzenli aralıklarla otomatik olarak dışarı aktarma günlük analizi sorgular açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a><span data-ttu-id="cbe3f-105">Günlük analizi veri tooPower BI dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="cbe3f-105">Export Log Analytics data tooPower BI</span></span>

>[!NOTE]
> <span data-ttu-id="cbe3f-106">Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra da günlük analizi veri tooPower BI dışa aktarmak için bu işlem artık çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then this process for exporting Log Analytics data tooPower BI will no longer work.</span></span>  <span data-ttu-id="cbe3f-107">Yükseltmeden önce oluşturulan tüm var olan zamanlamalar devre dışı bırakılacaktır.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-107">Any existing schedules that you created before upgrading will become disabled.</span></span> 
>
> <span data-ttu-id="cbe3f-108">Yükseltmeden sonra aynı platform Application Insights olarak Azure günlük analizi kullanır hello ve aynı işlemi olarak tooexport günlük analizi sorguları tooPower BI hello kullandığınız [hello işlem tooexport Application Insights sorgular tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span><span class="sxs-lookup"><span data-stu-id="cbe3f-108">After upgrade, Azure Log Analytics uses hello same platform as Application Insights, and you use hello same process tooexport Log Analytics queries tooPower BI as [hello process tooexport Application Insights queries tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>  <span data-ttu-id="cbe3f-109">Merhaba sorgu makalesinde açıklandığı gibi hello Analytics konsolunu kullanarak ya da dışa aktarabilirsiniz veya hello seçebilirsiniz **Power BI** hello günlük arama portal Merhaba ekranında hello üstündeki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-109">You can either export hello query using hello Analytics console as described in that article, or you can select hello **Power BI** button at hello top of hello screen in hello Log Search portal.</span></span>



<span data-ttu-id="cbe3f-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) bir bulut tabanlı İş analizi hizmeti Microsoft'tan farklı veri kümelerinin analize zengin Görselleştirmelerini ve raporlar sunar.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-110">[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) is a cloud based business analytics service from Microsoft that provides rich visualizations and reports for analysis of different sets of data.</span></span>  <span data-ttu-id="cbe3f-111">Görselleştirmeleri ve çözümleme araçları yararlanabilirsiniz şekilde günlük analizi otomatik olarak veri hello OMS depodan Power BI'a aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-111">Log Analytics can automatically export data from hello OMS repository into Power BI so you can leverage its visualizations and analysis tools.</span></span>

<span data-ttu-id="cbe3f-112">Günlük analizi ile Power BI yapılandırırken kendi Power BI sonuçları toocorresponding kümelerinde verme günlük sorgular oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-112">When you configure Power BI with Log Analytics, you create log queries that export their results toocorresponding datasets in Power BI.</span></span>  <span data-ttu-id="cbe3f-113">Merhaba sorgu ve dışarı aktarma hello en son verilerle günlük analizi tarafından toplanan tookeep hello dataset toodate yukarı tanımlayan bir zamanlamaya göre çalıştır tooautomatically devam eder.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-113">hello query and export continues tooautomatically run on a schedule that you define tookeep hello dataset up toodate with hello latest data collected by Log Analytics.</span></span>

![Günlük analizi tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a><span data-ttu-id="cbe3f-115">Power BI zamanlamaları</span><span class="sxs-lookup"><span data-stu-id="cbe3f-115">Power BI Schedules</span></span>
<span data-ttu-id="cbe3f-116">A *Power BI zamanlama* kümesinden hello OMS depo tooa karşılık gelen Power BI ve bu arama tookeep hello veri kümesi geçerli ne sıklıkta çalıştırmak tanımlayan bir zamanlama bir veri kümesi aktarır günlük arama içerir.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-116">A *Power BI Schedule* includes a log search that exports a set of data from hello OMS repository tooa corresponding dataset in Power BI and a schedule that defines how often this search is run tookeep hello dataset current.</span></span>

<span data-ttu-id="cbe3f-117">Merhaba dataset Hello alanlarında hello günlük araması tarafından döndürülen hello kayıtları hello özelliklerini eşleşir.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-117">hello fields in hello dataset will match hello properties of hello records returned by hello log search.</span></span>  <span data-ttu-id="cbe3f-118">Merhaba dataset tüm içerecektir sonra hello arama farklı türlerde kayıtları döndürüyorsa her hello hello özelliklerinden kayıt türleri dahil.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-118">If hello search returns records of different types then hello dataset will include all of hello properties from each of hello included record types.</span></span>  

> [!NOTE]
> <span data-ttu-id="cbe3f-119">En iyi yöntem toouse ham verileri karşılıklı tooperforming komutları gibi kullanarak birleştirme döndürür. bir günlük arama sorgusu olduğundan [ölçü](log-analytics-search-reference.md#measure).</span><span class="sxs-lookup"><span data-stu-id="cbe3f-119">It is a best practice toouse a log search query that returns raw data as opposed tooperforming any consolidation using commands such as [Measure](log-analytics-search-reference.md#measure).</span></span>  <span data-ttu-id="cbe3f-120">Power BI'da hello ham verilerden herhangi bir toplama ve hesaplamalar gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-120">You can perform any aggregation and calculations in Power BI from hello raw data.</span></span>
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a><span data-ttu-id="cbe3f-121">OMS çalışma tooPower BI bağlanma</span><span class="sxs-lookup"><span data-stu-id="cbe3f-121">Connecting OMS workspace tooPower BI</span></span>
<span data-ttu-id="cbe3f-122">Günlük analizi tooPower BI verebilmeniz hello aşağıdaki yordamı kullanarak OMS çalışma tooyour Power BI hesabınızı bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-122">Before you can export from Log Analytics tooPower BI, you must connect your OMS workspace tooyour Power BI account using hello following procedure.</span></span>  

1. <span data-ttu-id="cbe3f-123">Merhaba Hello OMS konsolunda tıklatın **ayarları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-123">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="cbe3f-124">Seçin **hesapları**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-124">Select **Accounts**.</span></span>
3. <span data-ttu-id="cbe3f-125">Merhaba, **çalışma alanı bilgisi** bölümünde **tooPower BI hesabına bağlanmak**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-125">In hello **Workspace Information** section click **Connect tooPower BI Account**.</span></span>
4. <span data-ttu-id="cbe3f-126">Merhaba, Power BI hesabının kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-126">Enter hello credentials for your Power BI account.</span></span>

## <a name="create-a-power-bi-schedule"></a><span data-ttu-id="cbe3f-127">Power BI zamanlama oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbe3f-127">Create a Power BI Schedule</span></span>
<span data-ttu-id="cbe3f-128">Merhaba aşağıdaki yordamı kullanarak her veri kümesi için Power BI zamanlama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-128">Create a Power BI Schedule for each dataset using hello following procedure.</span></span>

1. <span data-ttu-id="cbe3f-129">Merhaba Hello OMS konsolunda tıklatın **günlük arama** döşeme.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-129">In hello OMS console click hello **Log Search** tile.</span></span>
2. <span data-ttu-id="cbe3f-130">Döndürür tooexport çok istediğiniz verileri hello kaydedilmiş bir aramayı seçin veya yazın yeni bir sorgu**Power BI**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-130">Type in a new query or select a saved search that returns hello data that you want tooexport too**Power BI**.</span></span>  
3. <span data-ttu-id="cbe3f-131">Merhaba tıklatın **Power BI** düğmesi hello sayfa tooopen hello hello üstündeki **Power BI** iletişim.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-131">Click hello **Power BI** button at hello top of hello page tooopen hello **Power BI** dialog.</span></span>
4. <span data-ttu-id="cbe3f-132">Aşağıdaki tablo ve tıklayın hello Hello bilgi sağlamak **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-132">Provide hello information in hello following table and click **Save**.</span></span>

| <span data-ttu-id="cbe3f-133">Özellik</span><span class="sxs-lookup"><span data-stu-id="cbe3f-133">Property</span></span> | <span data-ttu-id="cbe3f-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbe3f-134">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cbe3f-135">Ad</span><span class="sxs-lookup"><span data-stu-id="cbe3f-135">Name</span></span> |<span data-ttu-id="cbe3f-136">Power BI zamanlamaları hello listesini görüntülediğinizde adı tooidentify hello zamanlama.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-136">Name tooidentify hello schedule when you view hello list of Power BI schedules.</span></span> |
| <span data-ttu-id="cbe3f-137">Kayıtlı arama</span><span class="sxs-lookup"><span data-stu-id="cbe3f-137">Saved Search</span></span> |<span data-ttu-id="cbe3f-138">Merhaba günlük arama toorun.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-138">hello log search toorun.</span></span>  <span data-ttu-id="cbe3f-139">Merhaba geçerli sorguyu seçin veya varolan kaydedilmiş bir aramayı hello açılır kutusundan seçin.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-139">You can either select hello current query or select an existing saved search from hello dropdown box.</span></span> |
| <span data-ttu-id="cbe3f-140">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="cbe3f-140">Schedule</span></span> |<span data-ttu-id="cbe3f-141">Ne sıklıkta toorun hello kaydedilen arama ve toohello Power BI veri kümesi dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-141">How often toorun hello saved search and export toohello Power BI dataset.</span></span>  <span data-ttu-id="cbe3f-142">Merhaba değeri 15 dakika ile 24 saat arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-142">hello value must be between 15 minutes and 24 hours.</span></span> |
| <span data-ttu-id="cbe3f-143">Veri kümesi adı</span><span class="sxs-lookup"><span data-stu-id="cbe3f-143">Dataset Name</span></span> |<span data-ttu-id="cbe3f-144">Power bı'da hello DataSet'in Hello adı.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-144">hello name of hello dataset in Power BI.</span></span>  <span data-ttu-id="cbe3f-145">Yoksa oluşturulur ve mevcut değilse güncelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-145">It will be created if it doesn’t exist and updated if it does exist.</span></span> |

## <a name="viewing-and-removing-power-bi-schedules"></a><span data-ttu-id="cbe3f-146">Görüntüleme ve Power BI zamanlamaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="cbe3f-146">Viewing and Removing Power BI Schedules</span></span>
<span data-ttu-id="cbe3f-147">Aşağıdaki yordamı hello ile mevcut Power BI zamanlama hello listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-147">View hello list of existing Power BI Schedules with hello following procedure.</span></span>

1. <span data-ttu-id="cbe3f-148">Merhaba Hello OMS konsolunda tıklatın **ayarları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-148">In hello OMS console click hello **Settings** tile.</span></span>
2. <span data-ttu-id="cbe3f-149">Seçin **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-149">Select **Power BI**.</span></span>

<span data-ttu-id="cbe3f-150">Ayrıca hello toohello ayrıntılarını zamanlama, hello sayısı zamanlama hello hello geçen hafta çalıştırıldı ve hello son eşitleme hello durumu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-150">In addition toohello details of hello schedule, hello number of times that hello schedule has run in hello past week and hello status of hello last sync are displayed.</span></span>  <span data-ttu-id="cbe3f-151">Merhaba Eşitleme hatalarla karşılaştı, hello bağlantı toorun günlük arama hello hata ayrıntılarını ile kayıt tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-151">If hello sync encountered errors, you can click hello link toorun a log search for records with details of hello error.</span></span>

<span data-ttu-id="cbe3f-152">Bir zamanlama üzerinde hello tıklatarak kaldırabilirsiniz **X** hello içinde **Kaldır sütun**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-152">You can remove a schedule by clicking on hello **X** in hello **Remove column**.</span></span>  <span data-ttu-id="cbe3f-153">Seçerek bir zamanlama devre dışı bırakabilirsiniz **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-153">You can disable a schedule by selecting **Off**.</span></span>  <span data-ttu-id="cbe3f-154">toomodify bir zamanlama kaldırmak ve hello yeni ayarlarla yeniden oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-154">toomodify a schedule you must remove it and recreate it with hello new settings.</span></span>

![Power BI zamanlamaları](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a><span data-ttu-id="cbe3f-156">Örnek gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="cbe3f-156">Sample walkthrough</span></span>
<span data-ttu-id="cbe3f-157">Merhaba aşağıdaki bölümde, Power BI zamanlama oluşturma ve veri kümesi toocreate kullanma örneği basit bir rapor anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-157">hello following section walks through an example of creating a Power BI Schedule and using its dataset toocreate a simple report.</span></span>  <span data-ttu-id="cbe3f-158">Bu örnekte, bir bilgisayar kümesi için tüm performans verilerini dışa aktarılan tooPower BI olduğundan ve bir çizgi grafiği toodisplay işlemci kullanımı sonra oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-158">In this example, all performance data for a set of computers is exported tooPower BI and then a line graph is created toodisplay processor utilization.</span></span>

### <a name="create-log-search"></a><span data-ttu-id="cbe3f-159">Günlük arama oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbe3f-159">Create log search</span></span>
<span data-ttu-id="cbe3f-160">Bir günlük veri aramak için toosend toohello dataset istiyoruz hello oluşturmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-160">We start by creating a log search for hello data that we want toosend toohello dataset.</span></span>  <span data-ttu-id="cbe3f-161">Bu örnekte, ile başlayan bir ada sahip bilgisayarlar için tüm performans verileri döndüren bir sorgu kullanacağız *srv*.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-161">In this example, we’ll use a query that returns all performance data for computers with a name that starts with *srv*.</span></span>  

![Power BI zamanlamaları](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a><span data-ttu-id="cbe3f-163">Power BI arama oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbe3f-163">Create Power BI Search</span></span>
<span data-ttu-id="cbe3f-164">Merhaba öğesini **Power BI** düğmesini tooopen hello Power BI iletişim ve hello gerekli bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-164">We click hello **Power BI** button tooopen hello Power BI dialog and provide hello required information.</span></span>  <span data-ttu-id="cbe3f-165">Bu arama toorun saatte istediğiniz ve adlı bir veri kümesi oluşturma *Contoso Perf*.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-165">We want this search toorun once per hour and create a dataset called *Contoso Perf*.</span></span>  <span data-ttu-id="cbe3f-166">Zaten sahip olduğumuz istiyoruz hello veri oluşturuyor hello arama açık olduğundan, biz hello varsayılan seçimini koruyun *kullanım geçerli arama sorgusunu* için **kayıtlı arama**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-166">Since we already have hello search open that creates hello data we want, we keep hello default of *Use current search query* for **Saved Search**.</span></span>

![Power BI arama](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a><span data-ttu-id="cbe3f-168">Power BI arama doğrulayın</span><span class="sxs-lookup"><span data-stu-id="cbe3f-168">Verify Power BI Search</span></span>
<span data-ttu-id="cbe3f-169">Biz hello zamanlama doğru şekilde oluşturulmuş tooverify, biz hello listesini görüntülemek Power BI aramaları hello altında **ayarları** döşeme hello OMS panosunda.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-169">tooverify that we created hello schedule correctly, we view hello list of Power BI Searches under hello **Settings** tile in hello OMS dashboard.</span></span>  <span data-ttu-id="cbe3f-170">Biz, birkaç dakika bekleyin ve hello eşitleme yapılmadı raporları kadar bu görünümü yenileyin.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-170">We wait several minutes and refresh this view until it reports that hello sync has been run.</span></span>

![Power BI arama](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a><span data-ttu-id="cbe3f-172">Power BI Hello kümesinde doğrulayın</span><span class="sxs-lookup"><span data-stu-id="cbe3f-172">Verify hello dataset in Power BI</span></span>
<span data-ttu-id="cbe3f-173">Bizim hesabı içine oturumunuzu [powerbi.microsoft.com](http://powerbi.microsoft.com/) ve çok kaydırma**veri kümeleri** hello sol bölmenin hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-173">We log into our account at [powerbi.microsoft.com](http://powerbi.microsoft.com/) and scroll too**Datasets** at hello bottom of hello left pane.</span></span>  <span data-ttu-id="cbe3f-174">Bu hello görebiliriz *Contoso Perf* dataset bizim verme başarıyla çalıştırıldığını belirten listelenir.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-174">We can see that hello *Contoso Perf* dataset is listed indicating that our export has run successfully.</span></span>

![Power BI veri kümesi](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a><span data-ttu-id="cbe3f-176">Veri kümesi üzerinde tabanlı rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="cbe3f-176">Create report based on dataset</span></span>
<span data-ttu-id="cbe3f-177">Biz hello seçin **Contoso Perf** dataset tıklayın **sonuçları** hello içinde **alanları** bölmesinde bu veri kümesinin parçası olan hello sağ tooview hello alanlar.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-177">We select hello **Contoso Perf** dataset and then click on **Results** in hello **Fields** pane on hello right tooview hello fields that are part of this dataset.</span></span>  <span data-ttu-id="cbe3f-178">toocreate bir çizgi grafiği gösteren işlemci kullanımını her bilgisayar için aşağıdaki eylemler hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-178">toocreate a line graph showing processor utilization for each computer, we perform hello following actions.</span></span>

1. <span data-ttu-id="cbe3f-179">Merhaba çizgi grafiği görselleştirme seçin.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-179">Select hello Line chart visualization.</span></span>
2. <span data-ttu-id="cbe3f-180">Sürükleme **ObjectName** çok**rapor düzeyi filtresi** ve denetleme **İşlemci**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-180">Drag **ObjectName** too**Report level filter** and check **Processor**.</span></span>
3. <span data-ttu-id="cbe3f-181">Sürükleme **CounterName** çok**rapor düzeyi filtresi** ve denetleme **% işlemci zamanı**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-181">Drag **CounterName** too**Report level filter** and check **% Processor Time**.</span></span>
4. <span data-ttu-id="cbe3f-182">Sürükleme **CounterValue** çok**değerleri**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-182">Drag **CounterValue** too**Values**.</span></span>
5. <span data-ttu-id="cbe3f-183">Sürükleme **bilgisayar** çok**gösterge**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-183">Drag **Computer** too**Legend**.</span></span>
6. <span data-ttu-id="cbe3f-184">Sürükleme **TimeGenerated** çok**eksen**.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-184">Drag **TimeGenerated** too**Axis**.</span></span>

<span data-ttu-id="cbe3f-185">Bu hello elde edilen çizgi grafiği kümemize hello verilerle görüntülenen görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-185">We can see that hello resulting line graph is displayed with hello data from our dataset.</span></span>

![Power BI çizgi grafiği](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a><span data-ttu-id="cbe3f-187">Merhaba raporu kaydedin</span><span class="sxs-lookup"><span data-stu-id="cbe3f-187">Save hello report</span></span>
<span data-ttu-id="cbe3f-188">Biz hello üzerinde tıklatarak hello rapor kaydet Kaydet düğmesi Merhaba ekranında hello üstündeki ve bunu şimdi hello Raporlar bölümünde hello sol bölmesinde listelendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-188">We save hello report by clicking on hello Save button at hello top of hello screen and validate that it is now listed in hello Reports section in hello left pane.</span></span>

![Power BI raporları](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a><span data-ttu-id="cbe3f-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbe3f-190">Next steps</span></span>
* <span data-ttu-id="cbe3f-191">Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) olabilir toobuild sorguları dışarı tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-191">Learn about [log searches](log-analytics-log-searches.md) toobuild queries that can be exported tooPower BI.</span></span>
* <span data-ttu-id="cbe3f-192">Daha fazla bilgi edinmek [Power BI](http://powerbi.microsoft.com) toobuild görselleştirmeleri dayalı üzerinde günlük analizi dışarı aktarır.</span><span class="sxs-lookup"><span data-stu-id="cbe3f-192">Learn more about [Power BI](http://powerbi.microsoft.com) toobuild visualizations based on Log Analytics exports.</span></span>
