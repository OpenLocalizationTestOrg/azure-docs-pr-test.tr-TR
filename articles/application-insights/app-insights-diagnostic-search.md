---
title: "Azure Application Insights aramasında aaaUsing | Microsoft Docs"
description: "Web uygulamanız tarafından gönderilen arama ve filtreleme ham telemetri."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="f05e1-103">Application Insights'ta aramayı kullanma</span><span class="sxs-lookup"><span data-stu-id="f05e1-103">Using Search in Application Insights</span></span>
<span data-ttu-id="f05e1-104">Arama özelliğidir [Application Insights](app-insights-overview.md) toofind kullanıyorsanız ve sayfa görünümleri, özel durumlar gibi tek tek telemetri öğeleri keşfedin veya web istekleri olduğunu.</span><span class="sxs-lookup"><span data-stu-id="f05e1-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="f05e1-105">Ve günlük izlemelerini ve kodlanmış olayları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f05e1-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="f05e1-106">(Verilerinizi üzerinden daha karmaşık sorgular için kullanın [Analytics](app-insights-analytics-tour.md).)</span><span class="sxs-lookup"><span data-stu-id="f05e1-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="f05e1-107">Burada arama görüyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="f05e1-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="f05e1-108">Hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="f05e1-108">In hello Azure portal</span></span>
<span data-ttu-id="f05e1-109">Tanılama arama, uygulamanızın hello uygulama Öngörüler genel bakış dikey penceresinden açıkça açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f05e1-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Tanılama arama Aç](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="f05e1-111">Bazı grafikler ve kılavuz öğeleri tıklattığınızda da açılır.</span><span class="sxs-lookup"><span data-stu-id="f05e1-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="f05e1-112">Bu durumda, kendi filtrelerini toofocus seçtiğiniz öğesi hello türünü önceden ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="f05e1-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="f05e1-113">Örneğin, hello genel bakış dikey penceresinde bir çubuk grafiği, yanıt süresine göre sınıflandırılmış isteklerinin yoktur.</span><span class="sxs-lookup"><span data-stu-id="f05e1-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="f05e1-114">Yanıt süresi aralığı, bir performans aralığı toosee tek tek isteklerin listesini tıklatın:</span><span class="sxs-lookup"><span data-stu-id="f05e1-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![İsteği Performans'ı tıklatın](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="f05e1-116">Tanılama arama ana gövdesini Hello listesidir telemetri öğelerinin - sunucu istekleri, sayfa görünümleri, kodlanmış özel olaylar ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="f05e1-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="f05e1-117">Merhaba hello listenin olayları sayıları zamanla gösteren bir Özet Grafiği ' dir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="f05e1-118">Yenileme tooget yeni olaylar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f05e1-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="f05e1-119">Visual Studio’da</span><span class="sxs-lookup"><span data-stu-id="f05e1-119">In Visual Studio</span></span>

<span data-ttu-id="f05e1-120">Visual Studio'da, ayrıca bir uygulama Insights arama penceresi yok.</span><span class="sxs-lookup"><span data-stu-id="f05e1-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="f05e1-121">Hatalarını ayıkladığınız hello uygulama tarafından oluşturulan telemetri olayları görüntülemek için en kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="f05e1-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="f05e1-122">Ancak hello Azure portal, yayımlanan uygulamanızdan toplanan hello olayları gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="f05e1-123">Visual Studio'da Hello arama penceresini açın:</span><span class="sxs-lookup"><span data-stu-id="f05e1-123">Open hello Search window in Visual Studio:</span></span>

![Visual Studio Application Insights arama açın](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="f05e1-125">Merhaba arama penceresinin özellikleri benzer toohello web portalı vardır:</span><span class="sxs-lookup"><span data-stu-id="f05e1-125">hello Search window has features similar toohello web portal:</span></span>

![Visual Studio Application Insights arama penceresi](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="f05e1-127">bir isteğin ya da bir sayfa görünümü açtığınızda hello izleme işlemi sekmesi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="f05e1-128">Bir'işlemi ' tooa tek istek veya sayfa görünümü ile ilişkili olayları dizisidir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="f05e1-129">Örneğin, bağımlılık çağrıları, özel durumlar, izleme günlükleri ve özel olaylar tek bir işlemin parçası olabilir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="f05e1-130">Merhaba izleme işlemi sekmesini gösterir zamanlaması ve süresi ilişkisi toohello istek veya sayfası görünümünde bu olayların grafiksel hello.</span><span class="sxs-lookup"><span data-stu-id="f05e1-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="f05e1-131">Bireysel öğeleri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="f05e1-131">Inspect individual items</span></span>
<span data-ttu-id="f05e1-132">Tüm telemetri öğesi toosee anahtar alanları ve ilişkili öğeleri seçin.</span><span class="sxs-lookup"><span data-stu-id="f05e1-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="f05e1-133">Toosee hello kümesini alanları isterseniz tıklayın "...".</span><span class="sxs-lookup"><span data-stu-id="f05e1-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Yeni iş öğesini, hello alanları düzenleyin ve Tamam'ı tıklatın.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="f05e1-135">Filtre olay türleri</span><span class="sxs-lookup"><span data-stu-id="f05e1-135">Filter event types</span></span>
<span data-ttu-id="f05e1-136">Merhaba filtre dikey penceresini açın ve hello olay türleri seçin toosee istiyor.</span><span class="sxs-lookup"><span data-stu-id="f05e1-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="f05e1-137">(Daha sonra hello dikey penceresi açılır toorestore hello filtreleri istiyorsanız, Sıfırla'yı tıklatın.)</span><span class="sxs-lookup"><span data-stu-id="f05e1-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Filtre seçin ve telemetri türlerini seçin](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="f05e1-139">Merhaba olay türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f05e1-139">hello event types are:</span></span>

* <span data-ttu-id="f05e1-140">**İzleme** - [tanılama günlükleri](app-insights-asp-net-trace-logs.md) TrackTrace, log4Net, NLog ve System.Diagnostic.Trace çağrıları dahil.</span><span class="sxs-lookup"><span data-stu-id="f05e1-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="f05e1-141">**İstek** -sayfaları, komut dosyaları, görüntüler, Stil dosyaları ve verileri de dahil olmak üzere sunucu uygulamanız tarafından alınan HTTP isteği.</span><span class="sxs-lookup"><span data-stu-id="f05e1-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="f05e1-142">Bu olaylar kullanılan toocreate hello istek ve yanıt genel bakış grafiklerinde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="f05e1-143">**Sayfa görünümü** - [Telemetri hello web istemcisi tarafından gönderilen](app-insights-javascript.md), toocreate sayfa görünümü raporları kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f05e1-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="f05e1-144">**Özel olay** - çağrıları tooTrackEvent() sırada çok eklediğiniz[izlemek kullanım](app-insights-api-custom-events-metrics.md), burada bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f05e1-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="f05e1-145">**Özel durum** - yakalanmayan [hello sunucu özel durumları](app-insights-asp-net-exceptions.md)ve TrackException() kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f05e1-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="f05e1-146">**Bağımlılık** - [sunucu uygulamanızı gelen çağrıları](app-insights-asp-net-dependencies.md) tooother Hizmetleri REST API'leri veya veritabanları gibi ve AJAX çağrıları, [istemci kodu](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="f05e1-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="f05e1-147">**Kullanılabilirlik** -sonuçlarını [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="f05e1-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="f05e1-148">Özellik değerleri üzerinde filtreleme</span><span class="sxs-lookup"><span data-stu-id="f05e1-148">Filter on property values</span></span>
<span data-ttu-id="f05e1-149">Olayları özelliklerini hello değerleri filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f05e1-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="f05e1-150">Merhaba kullanılabilir özellikler seçtiğiniz hello olay türlerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f05e1-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="f05e1-151">Örneğin, belirli yanıt kodu istekleriyle çıkışı seçin.</span><span class="sxs-lookup"><span data-stu-id="f05e1-151">For example, pick out requests with a specific response code.</span></span> 

![Bir özelliği'ni genişletin ve bir değer seçin](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="f05e1-153">Belirli bir özellik yok değerleri seçme aynı tüm değerleri seçme olarak efekt hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="f05e1-154">Bu, söz konusu özellik üzerinde filtreleme kapalı geçer.</span><span class="sxs-lookup"><span data-stu-id="f05e1-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="f05e1-155">Aramanızı daraltın</span><span class="sxs-lookup"><span data-stu-id="f05e1-155">Narrow your search</span></span>
<span data-ttu-id="f05e1-156">Bu hello toohello sağında hello filtre değerleri sayar bildirim göster var. kaç yineleme hello geçerli filtrelenmiş kümesinde yer alan.</span><span class="sxs-lookup"><span data-stu-id="f05e1-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="f05e1-157">Bu örnekte '500' hello hataların çoğu bu hello ' Rpt/çalışanlar' istek sonuçları açıktır:</span><span class="sxs-lookup"><span data-stu-id="f05e1-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Bir özelliği'ni genişletin ve bir değer seçin](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="f05e1-159">Merhaba olaylarla Bul aynı özelliği</span><span class="sxs-lookup"><span data-stu-id="f05e1-159">Find events with hello same property</span></span>
<span data-ttu-id="f05e1-160">Tüm hello Bul öğelerini hello ile aynı özellik değeri:</span><span class="sxs-lookup"><span data-stu-id="f05e1-160">Find all hello items with hello same property value:</span></span>

![Bir özellik sağ tıklayın](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="f05e1-162">Arama hello veri</span><span class="sxs-lookup"><span data-stu-id="f05e1-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="f05e1-163">toowrite daha karmaşık sorgular, açık [ **Analytics** ](app-insights-analytics-tour.md) hello arama dikey hello üstten.</span><span class="sxs-lookup"><span data-stu-id="f05e1-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="f05e1-164">Koşullar herhangi bir hello özellik değerleri için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f05e1-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="f05e1-165">Bu, yazdıysanız özellikle yararlıdır [özel olaylar](app-insights-api-custom-events-metrics.md) özellik değerlerine sahip.</span><span class="sxs-lookup"><span data-stu-id="f05e1-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="f05e1-166">Bir zaman aralığı olarak aramaları daha kısa bir aralık içinde olan daha hızlı tooset isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f05e1-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Tanılama arama Aç](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="f05e1-168">Tam sözcük, değil alt dizeler arayın.</span><span class="sxs-lookup"><span data-stu-id="f05e1-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="f05e1-169">Tırnak işaretleri tooenclose özel karakterler kullanın.</span><span class="sxs-lookup"><span data-stu-id="f05e1-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="f05e1-170">Dize</span><span class="sxs-lookup"><span data-stu-id="f05e1-170">string</span></span> | <span data-ttu-id="f05e1-171">olan *değil* tarafından bulunamadı</span><span class="sxs-lookup"><span data-stu-id="f05e1-171">is *not* found by</span></span> | <span data-ttu-id="f05e1-172">Ancak bu Bul</span><span class="sxs-lookup"><span data-stu-id="f05e1-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f05e1-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="f05e1-173">HomeController.About</span></span> |<span data-ttu-id="f05e1-174">Giriş</span><span class="sxs-lookup"><span data-stu-id="f05e1-174">home</span></span><br/><span data-ttu-id="f05e1-175">Denetleyici</span><span class="sxs-lookup"><span data-stu-id="f05e1-175">controller</span></span><br/><span data-ttu-id="f05e1-176">Çıkışı</span><span class="sxs-lookup"><span data-stu-id="f05e1-176">out</span></span> | <span data-ttu-id="f05e1-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="f05e1-177">homecontroller</span></span><br/><span data-ttu-id="f05e1-178">hakkında</span><span class="sxs-lookup"><span data-stu-id="f05e1-178">about</span></span><br/><span data-ttu-id="f05e1-179">"homecontroller.about"</span><span class="sxs-lookup"><span data-stu-id="f05e1-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="f05e1-180">Amerika Birleşik Devletleri</span><span class="sxs-lookup"><span data-stu-id="f05e1-180">United States</span></span>|<span data-ttu-id="f05e1-181">UNI</span><span class="sxs-lookup"><span data-stu-id="f05e1-181">Uni</span></span><br/><span data-ttu-id="f05e1-182">düzenlenmiş</span><span class="sxs-lookup"><span data-stu-id="f05e1-182">ted</span></span>|<span data-ttu-id="f05e1-183">Birleşik</span><span class="sxs-lookup"><span data-stu-id="f05e1-183">united</span></span><br/><span data-ttu-id="f05e1-184">durumları</span><span class="sxs-lookup"><span data-stu-id="f05e1-184">states</span></span><br/><span data-ttu-id="f05e1-185">VE Birleşik Devletleri</span><span class="sxs-lookup"><span data-stu-id="f05e1-185">united AND states</span></span><br/><span data-ttu-id="f05e1-186">"ABD"</span><span class="sxs-lookup"><span data-stu-id="f05e1-186">"united states"</span></span>

<span data-ttu-id="f05e1-187">Kullanabileceğiniz hello arama ifadeleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f05e1-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="f05e1-188">Örnek sorgu</span><span class="sxs-lookup"><span data-stu-id="f05e1-188">Sample query</span></span> | <span data-ttu-id="f05e1-189">Etki</span><span class="sxs-lookup"><span data-stu-id="f05e1-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="f05e1-190">Tüm olayları, alanlar hello word "apple" Merhaba zaman aralığında Bul</span><span class="sxs-lookup"><span data-stu-id="f05e1-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="f05e1-191">Her iki sözcüklerini olayları bulun.</span><span class="sxs-lookup"><span data-stu-id="f05e1-191">Find events that contain both words.</span></span> <span data-ttu-id="f05e1-192">Capital "ve", değil kullan "ve".</span><span class="sxs-lookup"><span data-stu-id="f05e1-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="f05e1-193">Her iki word içeren olayları bulun.</span><span class="sxs-lookup"><span data-stu-id="f05e1-193">Find events that contain either word.</span></span> <span data-ttu-id="f05e1-194">"", Kullanıp "veya".</span><span class="sxs-lookup"><span data-stu-id="f05e1-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="f05e1-195">Kısa formu.</span><span class="sxs-lookup"><span data-stu-id="f05e1-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="f05e1-196">Bir sözcük ancak değil hello diğer içeren olayları bulun.</span><span class="sxs-lookup"><span data-stu-id="f05e1-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="f05e1-197">Örnekleme</span><span class="sxs-lookup"><span data-stu-id="f05e1-197">Sampling</span></span>
<span data-ttu-id="f05e1-198">Uygulamanız çok sayıda telemetri oluşturuyorsa (ve ASP.NET SDK sürüm 2.0.0-beta3 hello kullanıyorsanız veya sonrası), hello Uyarlamalı örnekleme modülü olayların yalnızca bir temsilci fraksiyonunu göndererek toohello portal gönderilen hello birimi otomatik olarak azaltır.</span><span class="sxs-lookup"><span data-stu-id="f05e1-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="f05e1-199">Ancak, böylece ilgili olaylar arasında gezinebilirsiniz olayları, ilgili toohello aynı istekte seçilen veya bir grup olarak işaretli değildir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="f05e1-200">[Örnekleme hakkında bilgi edinin](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f05e1-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="f05e1-201">İş öğesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f05e1-201">Create work item</span></span>
<span data-ttu-id="f05e1-202">Tüm telemetri öğesinden hello ayrıntılarla GitHub veya Visual Studio Team Services içinde bir hata oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f05e1-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Yeni iş öğesini, hello alanları düzenleyin ve Tamam'ı tıklatın.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="f05e1-204">Merhaba tooconfigure sorulur bunu ilk kez bir bağlantı tooyour Team Services hesabı ve proje.</span><span class="sxs-lookup"><span data-stu-id="f05e1-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Merhaba URL'sini Team Services sunucunuzun ve hello proje adı doldurun ve Yetkilendir'i tıklatın](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="f05e1-206">(De hello bağlantı hello iş öğeleri dikey penceresinde yapılandırabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="f05e1-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="f05e1-207">Aramayı kaydetme</span><span class="sxs-lookup"><span data-stu-id="f05e1-207">Save your search</span></span>
<span data-ttu-id="f05e1-208">İstediğiniz tüm hello filtreleri belirledikten sonra hello aramayı sık kullanılan olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f05e1-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="f05e1-209">Bir kurumsal hesap çalışıyorsanız, seçebileceğiniz olup olmadığını tooshare diğer takım üyeleri ile.</span><span class="sxs-lookup"><span data-stu-id="f05e1-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Sık Kullanılanlar'a tıklayın, hello adını ayarlayın ve Kaydet](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="f05e1-211">yeniden toosee hello arama **gidin toohello genel bakış dikey** ve Sık Kullanılanlar açın:</span><span class="sxs-lookup"><span data-stu-id="f05e1-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Sık Kullanılanlar döşeme](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="f05e1-213">Göreli zaman aralığı ile kaydettiyseniz hello yeniden açılan dikey penceresinde hello en son verileri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="f05e1-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="f05e1-214">Mutlak zaman aralığıyla kaydettiyseniz hello bkz aynı verileri her zaman.</span><span class="sxs-lookup"><span data-stu-id="f05e1-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="f05e1-215">(Toosave sık kullanılan istediğinizde 'Göreli' yoksa, hello başlığında zaman aralığı'nı tıklatın ve özel bir aralık olmadığından bir zaman aralığı ayarlayın.)</span><span class="sxs-lookup"><span data-stu-id="f05e1-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="f05e1-216">Daha fazla telemetri tooApplication Öngörüler Gönder</span><span class="sxs-lookup"><span data-stu-id="f05e1-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="f05e1-217">Toohello Giden kutusu telemetri Application Insights SDK'sı tarafından gönderilen ek şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f05e1-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="f05e1-218">İçinde sık kullandığınız günlük çerçeveden günlük izlemelerini yakalama [.NET](app-insights-asp-net-trace-logs.md) veya [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f05e1-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="f05e1-219">, Günlük izlemelerini arayın ve sayfa görünümleri, özel durumlar ve diğer olaylarla ilişkilendirmek anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f05e1-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="f05e1-220">[Kod yazma](app-insights-api-custom-events-metrics.md) toosend özel olaylar, sayfa görünümleri ve özel durumları.</span><span class="sxs-lookup"><span data-stu-id="f05e1-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="f05e1-221">[Nasıl toosend ve özel telemetri tooApplication Öngörüler öğrenin](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f05e1-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="f05e1-222"><a name="questions"></a>SORU- CEVAP</span><span class="sxs-lookup"><span data-stu-id="f05e1-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="f05e1-223"><a name="limits"></a>Ne kadar veri tutulur?</span><span class="sxs-lookup"><span data-stu-id="f05e1-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="f05e1-224">Merhaba bkz [sınırları Özet](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="f05e1-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="f05e1-225">My server istekleri gönderme verisi nasıl görebilirim?</span><span class="sxs-lookup"><span data-stu-id="f05e1-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="f05e1-226">Merhaba POST verilerini otomatik olarak oturum yoktur, ancak kullanabileceğiniz [TrackTrace ya da günlük çağrıları](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="f05e1-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="f05e1-227">Merhaba gönderme verisi hello ileti parametresinde yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f05e1-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="f05e1-228">Merhaba hello iletisinde aynı filtre olamaz özellikleri şekilde filtre uygulayabilirsiniz, ancak hello boyut sınırı daha uzun.</span><span class="sxs-lookup"><span data-stu-id="f05e1-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="f05e1-229">Video</span><span class="sxs-lookup"><span data-stu-id="f05e1-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="f05e1-230"><a name="add"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f05e1-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="f05e1-231">Karmaşık sorgular analizleri yazma</span><span class="sxs-lookup"><span data-stu-id="f05e1-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="f05e1-232">Günlükleri ve özel telemetri tooApplication Öngörüler Gönder</span><span class="sxs-lookup"><span data-stu-id="f05e1-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="f05e1-233">Kullanılabilirlik ve yanıt hızını testleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="f05e1-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="f05e1-234">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f05e1-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
