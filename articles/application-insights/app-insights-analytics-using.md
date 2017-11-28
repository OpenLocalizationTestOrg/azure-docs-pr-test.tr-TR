---
title: "aaaUsing analizi - hello güçlü arama aracının Azure Application Insights | Microsoft Docs"
description: "Merhaba Analytics, Application Insights hello güçlü tanılama arama aracını kullanma. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="e69b6-103">Application Insights'ta Analytics kullanma</span><span class="sxs-lookup"><span data-stu-id="e69b6-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="e69b6-104">[Analytics](app-insights-analytics.md) hello güçlü arama özelliği [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e69b6-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="e69b6-105">Bu sayfaları günlük analizi sorgu dili açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e69b6-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="e69b6-106">**[Merhaba tanıtım videosunu izleyin](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="e69b6-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="e69b6-107">**[Benzetimli verilerimizi Analytics sürücüde test](https://analytics.applicationinsights.io/demo)**  uygulamanızı veri tooApplication Öngörüler henüz değil gönderiliyorsa.</span><span class="sxs-lookup"><span data-stu-id="e69b6-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="e69b6-108">Açık analizi</span><span class="sxs-lookup"><span data-stu-id="e69b6-108">Open Analytics</span></span>
<span data-ttu-id="e69b6-109">Giriş kaynağının, uygulamanızın Application ınsights'ta, Analytics'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Portal.Azure.com açın, Application Insights kaynağınıza açın ve analizi'ı tıklatın.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="e69b6-111">Merhaba satır içi öğretici neler yapabileceğiniz hakkında fikir edinmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="e69b6-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="e69b6-112">Var olan bir [burada daha kapsamlı Turu](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="e69b6-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="e69b6-113">Telemetrinizi sorgu</span><span class="sxs-lookup"><span data-stu-id="e69b6-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="e69b6-114">Bir sorgu yazın</span><span class="sxs-lookup"><span data-stu-id="e69b6-114">Write a query</span></span>
![Şema görüntüleme](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="e69b6-116">Merhaba adını hello sol tarafta listelenen hello tablolar ile başlar (veya hello [aralığı](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) veya [UNION](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) işleçleri).</span><span class="sxs-lookup"><span data-stu-id="e69b6-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="e69b6-117">Kullanım `|` kanalı a toocreate [işleçleri](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="e69b6-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="e69b6-118">IntelliSense hello işleçleri ile kullanabileceğiniz hello ifade öğeleri ister.</span><span class="sxs-lookup"><span data-stu-id="e69b6-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="e69b6-119">Merhaba bilgi simgesini tıklatın (veya CTRL + ARA ÇUBUĞU tuşlarına basın) tooget daha uzun bir açıklama ve örnekleri toouse her öğe.</span><span class="sxs-lookup"><span data-stu-id="e69b6-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="e69b6-120">Merhaba bkz [Analytics dil Turu](app-insights-analytics-tour.md) ve [dil başvurusu](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e69b6-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="e69b6-121">Sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e69b6-121">Run a query</span></span>
![Bir sorgu çalıştırılarak](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="e69b6-123">Sorguda tek satır sonları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="e69b6-124">Merhaba imleç içinde veya toorun istediğiniz hello sorgu hello sonunda yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="e69b6-125">Sorgunuzu Hello zaman aralığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-125">Check hello time range of your query.</span></span> <span data-ttu-id="e69b6-126">(Bunu değiştirmek veya kendi dahil ederek geçersiz kılma [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) yan tümcesinde, sorgunuzu.)</span><span class="sxs-lookup"><span data-stu-id="e69b6-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="e69b6-127">Git toorun hello sorgu tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="e69b6-128">Boş satırlar sorgunuzda koymayın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="e69b6-129">Boş satırlar ile ayırarak bir sorgu sekmede birkaç ayrılmış sorguları kullanmaya devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="e69b6-130">Merhaba imleç sahip hello sorguyu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e69b6-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="e69b6-131">Bir sorguyu kaydetme</span><span class="sxs-lookup"><span data-stu-id="e69b6-131">Save a query</span></span>
![Bir sorguyu kaydetme](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="e69b6-133">Merhaba geçerli sorgu dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-133">Save hello current query file.</span></span>
2. <span data-ttu-id="e69b6-134">Kaydedilmiş sorgu dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-134">Open a saved query file.</span></span>
3. <span data-ttu-id="e69b6-135">Yeni bir sorgu dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e69b6-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="e69b6-136">Merhaba Ayrıntılar bakın</span><span class="sxs-lookup"><span data-stu-id="e69b6-136">See hello details</span></span>
<span data-ttu-id="e69b6-137">Merhaba sonuçları toosee herhangi bir satırın özelliklerini tam listesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="e69b6-138">Daha fazla herhangi bir yapılandırılmış değer - Örneğin, özellik, özel boyutları veya bir özel durum listeleme hello yığını genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Bir satır genişletin](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="e69b6-140">Merhaba sonuçları düzenleyin</span><span class="sxs-lookup"><span data-stu-id="e69b6-140">Arrange hello results</span></span>
<span data-ttu-id="e69b6-141">Sıralama, filtre, sayfalara bölme ve grup, sorgunun döndürdüğü hello sonuçları.</span><span class="sxs-lookup"><span data-stu-id="e69b6-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="e69b6-142">Sıralama, gruplandırma ve filtreleme hello tarayıcıda sorgunuzu yeniden çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="e69b6-143">Bunlar yalnızca son sorgu tarafından döndürülen hello sonuçları yeniden düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="e69b6-144">tooperform hello sonuç döndürmeden önce hello Server'daki bu görevler yazma sorgunuzu hello ile [sıralama](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [özetlemek](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) ve [burada](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) işleçler.</span><span class="sxs-lookup"><span data-stu-id="e69b6-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="e69b6-145">Yaptığınız hello sütunları çekme toosee gibi sütun üst bilgileri toorearrange bunları ve yeniden boyutlandırma sütunları kendi kenarlıklarını sürükleyerek sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Sütunları düzenleme](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="e69b6-147">Sıralama ve filtreleme öğeleri</span><span class="sxs-lookup"><span data-stu-id="e69b6-147">Sort and filter items</span></span>
<span data-ttu-id="e69b6-148">Sonuçlarınızı hello head bir sütunun tıklayarak sıralayın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="e69b6-149">Toosort hello başka bir şekilde yeniden tıklayın ve tıklatın üçüncü kez toorevert toohello özgün sorgu tarafından döndürülen sıralama.</span><span class="sxs-lookup"><span data-stu-id="e69b6-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="e69b6-150">Merhaba filtre simgesini toonarrow aramanızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-150">Use hello filter icon toonarrow your search.</span></span>

![Sütunları sıralama ve filtreleme](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="e69b6-152">Öğeleri gruplandırma</span><span class="sxs-lookup"><span data-stu-id="e69b6-152">Group items</span></span>
<span data-ttu-id="e69b6-153">toosort birden fazla sütuna göre gruplandırma kullanın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="e69b6-154">İlk etkinleştirmek ve sütun üst bilgileri Merhaba tablonun yukarısındaki hello alanına sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Grup](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="e69b6-156">Bazı sonuçları eksik mi?</span><span class="sxs-lookup"><span data-stu-id="e69b6-156">Missing some results?</span></span>

<span data-ttu-id="e69b6-157">Beklediğiniz tüm hello sonuçları görmüyorsanız düşünüyorsanız, birkaç olası nedeni vardır.</span><span class="sxs-lookup"><span data-stu-id="e69b6-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="e69b6-158">**Zaman aralığı filtresi**.</span><span class="sxs-lookup"><span data-stu-id="e69b6-158">**Time range filter**.</span></span> <span data-ttu-id="e69b6-159">Varsayılan olarak, yalnızca son 24 saat hello sonuçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="e69b6-160">Merhaba kaynak tablolardan alınan sonuçları hello aralığını sınırlar otomatik bir filtre yok.</span><span class="sxs-lookup"><span data-stu-id="e69b6-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="e69b6-161">Bununla birlikte, hello zaman aralığını değiştirebilirsiniz hello açılan menüsünü kullanarak filtre.</span><span class="sxs-lookup"><span data-stu-id="e69b6-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="e69b6-162">Ya da kendi dahil ederek hello otomatik aralık geçersiz kılabilirsiniz [ `where  ... timestamp ...` yan tümcesi](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) sorgunuzu içine.</span><span class="sxs-lookup"><span data-stu-id="e69b6-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="e69b6-163">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="e69b6-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="e69b6-164">**Sonuç sınırı**.</span><span class="sxs-lookup"><span data-stu-id="e69b6-164">**Results limit**.</span></span> <span data-ttu-id="e69b6-165">Merhaba portalından döndürülen hello sonuçları yaklaşık 10 k satırlarda sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e69b6-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="e69b6-166">Merhaba sınırın gidin, bir uyarı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="e69b6-167">Bu durumda, sonuçlarınızı hello tablosundaki sıralama her zaman, tüm hello gerçek ilk veya son sonuçları göstermeyecektir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="e69b6-168">İyi bir uygulama tooavoid basarsa hello sınırı'dir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="e69b6-169">Merhaba zaman aralığı filtresi veya işleçleri gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="e69b6-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="e69b6-170">zaman damgası tarafından ilk 100</span><span class="sxs-lookup"><span data-stu-id="e69b6-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="e69b6-171">100 alın</span><span class="sxs-lookup"><span data-stu-id="e69b6-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="e69b6-172">Özetle</span><span class="sxs-lookup"><span data-stu-id="e69b6-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="e69b6-173">Burada zaman damgası > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="e69b6-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="e69b6-174">(10'dan fazla k satırları istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="e69b6-174">(Want more than 10k rows?</span></span> <span data-ttu-id="e69b6-175">Kullanmayı [sürekli verme](app-insights-export-telemetry.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="e69b6-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="e69b6-176">Analytics alınırken ham verileri yerine analiz için tasarlanmıştır.)</span><span class="sxs-lookup"><span data-stu-id="e69b6-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="e69b6-177">Diyagramları</span><span class="sxs-lookup"><span data-stu-id="e69b6-177">Diagrams</span></span>
<span data-ttu-id="e69b6-178">İstediğiniz diyagram Hello türünü seçin:</span><span class="sxs-lookup"><span data-stu-id="e69b6-178">Select hello type of diagram you'd like:</span></span>

![Bir diyagram türü seçin](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="e69b6-180">Merhaba sağ türlerinin birkaç sütun varsa, hello x ve y eksenleri ve boyutları toosplit hello sonuçlarına göre bir sütun seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="e69b6-181">Varsayılan olarak, sonuçlar başlangıçta tablo olarak görüntülenir ve hello diyagramı el ile seçin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="e69b6-182">Ancak hello kullanabilirsiniz [yönergesi işlemek](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) hello sonunda sorgu tooselect bir diyagramı.</span><span class="sxs-lookup"><span data-stu-id="e69b6-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="e69b6-183">Analytics tanılama</span><span class="sxs-lookup"><span data-stu-id="e69b6-183">Analytics diagnostics</span></span>


<span data-ttu-id="e69b6-184">Bir timechart üzerinde ani ani veya verilerinizi adımda ise hello satırında vurgulanan noktasının görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="e69b6-185">Bu Analytics tanılama hello ani değişiklik filtre özellikleri bileşimini belirledi gösterir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="e69b6-186">Başlangıç noktası tooget hello filtre ve toosee hello filtrelenmiş sürüm üzerinde daha fazla ayrıntı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="e69b6-187">Bu, hangi nedeniyle hello değişiklik belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="e69b6-188">Analytics Tanılama hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e69b6-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Analytics tanılama](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="e69b6-190">PIN toodashboard</span><span class="sxs-lookup"><span data-stu-id="e69b6-190">Pin toodashboard</span></span>
<span data-ttu-id="e69b6-191">Bir diyagram veya tablo tooone, sabitleyebilirsiniz, [panolar paylaşılan](app-insights-dashboards.md) -yalnızca hello PIN'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="e69b6-192">(Çok gerekebilecek[yükseltme uygulamanızı paket fiyatlandırma kullanıcının](app-insights-pricing.md) bu özellik üzerinde tooturn.)</span><span class="sxs-lookup"><span data-stu-id="e69b6-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Merhaba PIN'ı tıklatın](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="e69b6-194">Bu, hello performans veya web hizmetlerinizi kullanımını izleme Panosu toohelp birlikte geçirdiğinizde, oldukça karmaşık bir analiz hello yanında diğer ölçümleri ekleyebilirsiniz, anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="e69b6-195">Dört veya daha az sütun varsa bir tablo toohello Pano sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="e69b6-196">Yalnızca hello üst yedi satır görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="e69b6-197">Pano yenileme</span><span class="sxs-lookup"><span data-stu-id="e69b6-197">Dashboard refresh</span></span>
<span data-ttu-id="e69b6-198">Merhaba sabitlenmiş grafik toohello Pano hello sorgu yaklaşık olarak saatte yeniden çalıştırarak otomatik olarak yenilenir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="e69b6-199">Merhaba Yenile düğmesini tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="e69b6-200">Otomatik basitleştirme</span><span class="sxs-lookup"><span data-stu-id="e69b6-200">Automatic simplifications</span></span>

<span data-ttu-id="e69b6-201">Belirli basitleştirme tooa panoya Sabitle uygulanan tooa grafik olur.</span><span class="sxs-lookup"><span data-stu-id="e69b6-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="e69b6-202">**Kısıtlama süresi:** sorgular son 14 gün otomatik olarak sınırlı toohello gerçekleşiyor.</span><span class="sxs-lookup"><span data-stu-id="e69b6-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="e69b6-203">Merhaba etkisi olan hello aynı sorgunuz içeriyorsa gibi `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="e69b6-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="e69b6-204">**Bin sayısı kısıtlaması:** ayrık depo (genellikle bir çubuk grafiği), daha az doldurulan depo otomatik olarak gruplandırılır bir tek "başkalarının" Merhaba çok sahip bir grafik görüntülerseniz depo.</span><span class="sxs-lookup"><span data-stu-id="e69b6-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="e69b6-205">Örneğin, bu sorgu:</span><span class="sxs-lookup"><span data-stu-id="e69b6-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="e69b6-206">analytics'te şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e69b6-206">looks like this in Analytics:</span></span>

![İle uzun tail grafik](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="e69b6-208">ancak tooa panoya Sabitle, şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e69b6-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![İle sınırlı depo grafik](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="e69b6-210">TooExcel dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="e69b6-210">Export tooExcel</span></span>
<span data-ttu-id="e69b6-211">Bir sorgu çalıştırdıktan sonra bir .csv dosyası indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="e69b6-212">Tıklatın **Excel'e,**.</span><span class="sxs-lookup"><span data-stu-id="e69b6-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="e69b6-213">TooPower BI dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="e69b6-213">Export tooPower BI</span></span>
<span data-ttu-id="e69b6-214">Sorguda Hello imleç koyun ve seçin **verme, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="e69b6-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Analytics tooPower BI ' dışarı aktarma](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="e69b6-216">Power BI'da hello sorgu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-216">You run hello query in Power BI.</span></span> <span data-ttu-id="e69b6-217">Toorefresh bir zamanlamaya göre ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="e69b6-218">Power BI sayesinde, çok çeşitli kaynaklardan verileri bir araya getirme panolar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="e69b6-219">Dışarı aktarma tooPower BI hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="e69b6-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="e69b6-220">Ayrıntılı bağlantı</span><span class="sxs-lookup"><span data-stu-id="e69b6-220">Deep link</span></span>

<span data-ttu-id="e69b6-221">Bir bağlantı altında **verme, paylaşım bağlantı** tooanother kullanıcı gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="e69b6-222">Merhaba kullanıcının sağlanan [erişim tooyour kaynak grubu](app-insights-resources-roles-access-control.md), hello sorgu hello Analytics UI açılır.</span><span class="sxs-lookup"><span data-stu-id="e69b6-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="e69b6-223">(Sonra hello sorgu metni hello bağlantıdaki görünür "? q =" gzip sıkıştırılmış ve base-64 kodlamalı.</span><span class="sxs-lookup"><span data-stu-id="e69b6-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="e69b6-224">Kod toogenerate ayrıntılı bağlantılar toousers sağladığınız yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="e69b6-225">Ancak, hello kodundan yolu toorun Analytics hello kullanarak önerilir [REST API](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="e69b6-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="e69b6-226">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="e69b6-226">Automation</span></span>

<span data-ttu-id="e69b6-227">Kullanım hello [veri erişim REST API](https://dev.applicationinsights.io/) toorun Analytics sorgular.</span><span class="sxs-lookup"><span data-stu-id="e69b6-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="e69b6-228">[Örneğin](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (PowerShell kullanarak):</span><span class="sxs-lookup"><span data-stu-id="e69b6-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="e69b6-229">Analytics UI Hello farklı olarak, herhangi bir zaman damgası sınırlaması tooyour sorgu hello REST API otomatik olarak eklemez.</span><span class="sxs-lookup"><span data-stu-id="e69b6-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="e69b6-230">Tooadd kendi where yan tümcesi, büyük yanıtları alma tooavoid unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="e69b6-231">Veri içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="e69b6-231">Import data</span></span>

<span data-ttu-id="e69b6-232">Bir CSV dosyasından veri içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-232">You can import data from a CSV file.</span></span> <span data-ttu-id="e69b6-233">Tipik bir kullanım, telemetrisinden tablolarla katılabilirsiniz tooimport statik verilerdir.</span><span class="sxs-lookup"><span data-stu-id="e69b6-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="e69b6-234">Örneğin, kimliği doğrulanmış kullanıcılar, telemetri bir diğer ad veya karıştırılmış kimliğe göre belirlenirse, diğer adlar tooreal adlarını eşleyen bir tablo içe aktarılamadı.</span><span class="sxs-lookup"><span data-stu-id="e69b6-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="e69b6-235">Merhaba isteği telemetriyi bir birleştirme gerçekleştirerek hello Analytics raporlarında gerçek adlarına göre kullanıcılar tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="e69b6-236">Veri şemanızı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="e69b6-236">Define your data schema</span></span>

1. <span data-ttu-id="e69b6-237">Tıklatın **ayarları** (sol üst) ve ardından **veri kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="e69b6-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="e69b6-238">Merhaba yönergeleri izleyerek bir veri kaynağı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="e69b6-239">Olduğunuz en az on satır içermelidir hello veri örneği toosupply istedi.</span><span class="sxs-lookup"><span data-stu-id="e69b6-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="e69b6-240">Ardından, hello şema de düzeltin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-240">You then correct hello schema.</span></span>

<span data-ttu-id="e69b6-241">Bu, daha sonra bir veri kaynağı tanımlar tooimport tek tek tablolar kullanın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="e69b6-242">Tablo alma</span><span class="sxs-lookup"><span data-stu-id="e69b6-242">Import a table</span></span>

1. <span data-ttu-id="e69b6-243">Veri kaynağı tanımınız hello listeden açın.</span><span class="sxs-lookup"><span data-stu-id="e69b6-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="e69b6-244">"Karşıya Yükle" seçeneğini tıklatın ve hello yönergeleri tooupload hello tablo izleyin.</span><span class="sxs-lookup"><span data-stu-id="e69b6-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="e69b6-245">Bu çağrı tooa REST API içerir ve dolayısıyla kolay tooautomate taşır.</span><span class="sxs-lookup"><span data-stu-id="e69b6-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="e69b6-246">Tablonuz analitik sorguları kullanmak için kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="e69b6-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="e69b6-247">Analizleri görünür</span><span class="sxs-lookup"><span data-stu-id="e69b6-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="e69b6-248">Merhaba tabloyu kullanın</span><span class="sxs-lookup"><span data-stu-id="e69b6-248">Use hello table</span></span>

<span data-ttu-id="e69b6-249">Şimdi veri kaynağı tanımınız varsayın `usermap`, ve iki alan olduğunu `realName` ve `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="e69b6-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="e69b6-250">Merhaba `requests` da tablolu adında bir alan `user_AuthenticatedId`kolay toojoin gelir bunları:</span><span class="sxs-lookup"><span data-stu-id="e69b6-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="e69b6-251">Merhaba isteklerinin ortaya çıkan tabloda sahip başka bir sütuna `realName`.</span><span class="sxs-lookup"><span data-stu-id="e69b6-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="e69b6-252">LogStash alma</span><span class="sxs-lookup"><span data-stu-id="e69b6-252">Import from LogStash</span></span>

<span data-ttu-id="e69b6-253">Kullanırsanız [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), günlüklerinizi Analytics tooquery kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e69b6-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="e69b6-254">Kullanım hello [veri analizi kanallar eklentisi](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="e69b6-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="e69b6-255">Video</span><span class="sxs-lookup"><span data-stu-id="e69b6-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

