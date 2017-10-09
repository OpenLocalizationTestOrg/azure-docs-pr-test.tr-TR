---
title: "Azure Application Insights ölçümlerini aaaExploring | Microsoft Docs"
description: "Ölçüm explorer toointerpret grafikleri nasıl ve nasıl toocustomize ölçüm Gezgini dikey."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: bwren
ms.openlocfilehash: b77ae227ae61e800ad6f3af8a05cd123ea1d69e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="exploring-metrics-in-application-insights"></a><span data-ttu-id="d6730-103">Application ınsights'ta ölçümleri keşfederken</span><span class="sxs-lookup"><span data-stu-id="d6730-103">Exploring Metrics in Application Insights</span></span>
<span data-ttu-id="d6730-104">Ölçümlerini [Application Insights] [ start] ölçülen değerleri ve telemetri uygulamanızdan gönderilen olaylar sayısı.</span><span class="sxs-lookup"><span data-stu-id="d6730-104">Metrics in [Application Insights][start] are measured values and counts of events that are sent in telemetry from your application.</span></span> <span data-ttu-id="d6730-105">Performans sorunlarını algılamak ve eğilimleri, uygulamanızın nasıl kullanıldığını içinde izleme yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d6730-105">They help you detect performance issues and watch trends in how your application is being used.</span></span> <span data-ttu-id="d6730-106">Çok çeşitli standart ölçümleri yoktur ve kendi özel ölçümleri ve olayları de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-106">There's a wide range of standard metrics, and you can also create your own custom metrics and events.</span></span>

<span data-ttu-id="d6730-107">Ölçümleri ve olay sayısını, SUM'ları, ortalama veya sayıları gibi toplanmış değerler grafiklerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d6730-107">Metrics and event counts are displayed in charts of aggregated values such as sums, averages, or counts.</span></span>

<span data-ttu-id="d6730-108">Grafikler dizi örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d6730-108">Here's a sample set of charts:</span></span>

![](./media/app-insights-metrics-explorer/01-overview.png)

<span data-ttu-id="d6730-109">Her yerde ölçümler grafiklerde hello Application Insights portalında bulun.</span><span class="sxs-lookup"><span data-stu-id="d6730-109">You find metrics charts everywhere in hello Application Insights portal.</span></span> <span data-ttu-id="d6730-110">Çoğu durumda bunlar özelleştirilebilir ve daha fazla grafik toohello dikey ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-110">In most cases, they can be customized, and you can add more charts toohello blade.</span></span> <span data-ttu-id="d6730-111">Merhaba genel bakış dikey penceresinden toomore tıklayın ("Sunucuları" gibi başlıkları olan) grafikler, ayrıntılı veya **ölçüm Gezgini** tooopen özel grafikler oluşturduğunuz yeni bir dikey pencere.</span><span class="sxs-lookup"><span data-stu-id="d6730-111">From hello Overview blade, click through toomore detailed charts (which have titles such as "Servers"), or click **Metrics Explorer** tooopen a new blade where you can create custom charts.</span></span>

## <a name="time-range"></a><span data-ttu-id="d6730-112">Zaman aralığı</span><span class="sxs-lookup"><span data-stu-id="d6730-112">Time range</span></span>
<span data-ttu-id="d6730-113">Merhaba hello grafikler veya tüm dikey kılavuzları kapsadığı zaman aralığını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-113">You can change hello Time range covered by hello charts or grids on any blade.</span></span>

![Dikey penceresinde hello Azure portalı uygulamanızda açık hello genel bakış](./media/app-insights-metrics-explorer/03-range.png)

<span data-ttu-id="d6730-115">Henüz görünen kurmadı bazı veriler bekliyorsunuz, Yenile'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d6730-115">If you're expecting some data that hasn't appeared yet, click Refresh.</span></span> <span data-ttu-id="d6730-116">Grafikler kendilerini aralıklarla yenileme ancak hello aralıkları büyük zaman aralıkları için daha uzun.</span><span class="sxs-lookup"><span data-stu-id="d6730-116">Charts refresh themselves at intervals, but hello intervals are longer for larger time ranges.</span></span> <span data-ttu-id="d6730-117">Bir grafik, verileri toocome hello analiz ardışık düzeninden biraz sürebilir.</span><span class="sxs-lookup"><span data-stu-id="d6730-117">It can take a while for data toocome through hello analysis pipeline onto a chart.</span></span>

<span data-ttu-id="d6730-118">bir grafik parçası içine toozoom üzerine sürükleyin:</span><span class="sxs-lookup"><span data-stu-id="d6730-118">toozoom into part of a chart, drag over it:</span></span>

![Bir grafik parçası arasında sürükleyin.](./media/app-insights-metrics-explorer/12-drag.png)

<span data-ttu-id="d6730-120">Merhaba geri Yakınlaştırma düğmesi toorestore'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d6730-120">Click hello Undo Zoom button toorestore it.</span></span>

## <a name="granularity-and-point-values"></a><span data-ttu-id="d6730-121">Ayrıntı düzeyi ve noktası değerleri</span><span class="sxs-lookup"><span data-stu-id="d6730-121">Granularity and point values</span></span>
<span data-ttu-id="d6730-122">Fare bu noktada hello grafik toodisplay hello değerleri hello ölçümleri gelin.</span><span class="sxs-lookup"><span data-stu-id="d6730-122">Hover your mouse over hello chart toodisplay hello values of hello metrics at that point.</span></span>

![Merhaba fare grafiğinin üzerine getirin](./media/app-insights-metrics-explorer/02-focus.png)

<span data-ttu-id="d6730-124">belirli bir noktada hello ölçüm Hello değerini hello önceki örnekleme aralığı içinde toplanır.</span><span class="sxs-lookup"><span data-stu-id="d6730-124">hello value of hello metric at a particular point is aggregated over hello preceding sampling interval.</span></span>

<span data-ttu-id="d6730-125">Merhaba örnekleme aralığı veya "ayrıntı düzeyi" Merhaba dikey penceresinde hello üstünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d6730-125">hello sampling interval or "granularity" is shown at hello top of hello blade.</span></span>

![bir dikey pencere Hello üstbilgisi.](./media/app-insights-metrics-explorer/11-grain.png)

<span data-ttu-id="d6730-127">Merhaba zaman aralığı dikey penceresinde hello ayrıntı düzeyi ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d6730-127">You can adjust hello granularity in hello Time range blade:</span></span>

![bir dikey pencere Hello üstbilgisi.](./media/app-insights-metrics-explorer/grain.png)

<span data-ttu-id="d6730-129">Merhaba ayrıntı kullanılabilir seçtiğiniz hello zaman aralığı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d6730-129">hello granularities available depend on hello time range you select.</span></span> <span data-ttu-id="d6730-130">Merhaba açık ayrıntı alternatifleri hello zaman aralığına ilişkin toohello "Otomatik" ayrıntı düzeyi var.</span><span class="sxs-lookup"><span data-stu-id="d6730-130">hello explicit granularities are alternatives toohello "automatic" granularity for hello time range.</span></span>


## <a name="editing-charts-and-grids"></a><span data-ttu-id="d6730-131">Grafikler ve Izgaralar düzenleme</span><span class="sxs-lookup"><span data-stu-id="d6730-131">Editing charts and grids</span></span>
<span data-ttu-id="d6730-132">Yeni bir grafik toohello dikey pencere tooadd:</span><span class="sxs-lookup"><span data-stu-id="d6730-132">tooadd a new chart toohello blade:</span></span>

![Ölçümleri Explorer'da eklemek grafik seçin](./media/app-insights-metrics-explorer/04-add.png)

<span data-ttu-id="d6730-134">Seçin **Düzenle** bir mevcut veya yeni bir grafik tooedit gösterdiklerini:</span><span class="sxs-lookup"><span data-stu-id="d6730-134">Select **Edit** on an existing or new chart tooedit what it shows:</span></span>

![Bir veya daha çok ölçümü seçin](./media/app-insights-metrics-explorer/08-select.png)

<span data-ttu-id="d6730-136">Kısıtlamaları birlikte görüntülenebilir hello birleşimleri hakkında olsa grafikte, birden fazla ölçüm görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-136">You can display more than one metric on a chart, though there are restrictions about hello combinations that can be displayed together.</span></span> <span data-ttu-id="d6730-137">Başkalarının devre dışı bırakılır hello bazıları bir ölçüm seçtiğiniz üzerine çıkar.</span><span class="sxs-lookup"><span data-stu-id="d6730-137">As soon as you choose one metric, some of hello others are disabled.</span></span>

<span data-ttu-id="d6730-138">Kodlu [özel ölçümleri] [ track] uygulamanıza (çağrıları tooTrackMetric ve TrackEvent) bunlar burada listelenir.</span><span class="sxs-lookup"><span data-stu-id="d6730-138">If you coded [custom metrics][track] into your app (calls tooTrackMetric and TrackEvent) they will be listed here.</span></span>

## <a name="segment-your-data"></a><span data-ttu-id="d6730-139">Verilerinizi segmentlere</span><span class="sxs-lookup"><span data-stu-id="d6730-139">Segment your data</span></span>
<span data-ttu-id="d6730-140">Özelliği - Örneğin, toocompare sayfa görünümleri istemcilerde farklı işletim sistemleri tarafından bir ölçüm bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-140">You can split a metric by property - for example, toocompare page views on clients with different operating systems.</span></span>

<span data-ttu-id="d6730-141">Bir grafik veya kılavuz, gruplandırılması geçin ve özellik toogroup tarafından seçin:</span><span class="sxs-lookup"><span data-stu-id="d6730-141">Select a chart or grid, switch on grouping and pick a property toogroup by:</span></span>

![Gruplandırma'kümesi seçip bir özellik içinde Group By'ı seçin](./media/app-insights-metrics-explorer/15-segment.png)

> [!NOTE]
> <span data-ttu-id="d6730-143">Gruplandırma kullandığınızda, hello alan ve çubuk grafik türleri Yığılmış bir görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="d6730-143">When you use grouping, hello Area and Bar chart types provide a stacked display.</span></span> <span data-ttu-id="d6730-144">Merhaba toplama yöntemi toplam olduğu bu uygundur.</span><span class="sxs-lookup"><span data-stu-id="d6730-144">This is suitable where hello Aggregation method is Sum.</span></span> <span data-ttu-id="d6730-145">Ancak hello toplama türü ortalama olduğu hello çizgi veya kılavuz görüntü türlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="d6730-145">But where hello aggregation type is Average, choose hello Line or Grid display types.</span></span>
>
>

<span data-ttu-id="d6730-146">Kodlu [özel ölçümleri] [ track] uygulamanıza ve özellik değerlerini içerir, mümkün tooselect hello özelliğinin hello listesinde olması.</span><span class="sxs-lookup"><span data-stu-id="d6730-146">If you coded [custom metrics][track] into your app and they include property values, you'll be able tooselect hello property in hello list.</span></span>

<span data-ttu-id="d6730-147">Merhaba grafik bölümlenmiş veri için çok küçük mi?</span><span class="sxs-lookup"><span data-stu-id="d6730-147">Is hello chart too small for segmented data?</span></span> <span data-ttu-id="d6730-148">Kendi yüksekliğini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d6730-148">Adjust its height:</span></span>

![Merhaba kaydırıcısını ayarlayın](./media/app-insights-metrics-explorer/18-height.png)

## <a name="aggregation-types"></a><span data-ttu-id="d6730-150">Toplama türleri</span><span class="sxs-lookup"><span data-stu-id="d6730-150">Aggregation types</span></span>
<span data-ttu-id="d6730-151">Varsayılan olarak hello tarafında Hello gösterge genellikle hello grafik hello dönemi boyunca toplanan hello değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6730-151">hello legend at hello side by default usually shows hello aggregated value over hello period of hello chart.</span></span> <span data-ttu-id="d6730-152">Merhaba grafiğinin üzerine getirirseniz, o noktada hello değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6730-152">If you hover over hello chart, it shows hello value at that point.</span></span>

<span data-ttu-id="d6730-153">Her veri hello grafik hello örnekleme aralığı veya "ayrıntı düzeyi" önceki alınan hello veri değerlerinin bir toplama noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="d6730-153">Each data point on hello chart is an aggregate of hello data values received in hello preceding sampling interval or "granularity".</span></span> <span data-ttu-id="d6730-154">Merhaba ayrıntı düzeyi hello dikey penceresinde hello üst kısmında gösterilen ve hello ile değişir hello grafik genel ölçeğini.</span><span class="sxs-lookup"><span data-stu-id="d6730-154">hello granularity is shown at hello top of hello blade, and varies with hello overall timescale of hello chart.</span></span>

<span data-ttu-id="d6730-155">Ölçümleri farklı şekilde toplanabilir:</span><span class="sxs-lookup"><span data-stu-id="d6730-155">Metrics can be aggregated in different ways:</span></span>

* <span data-ttu-id="d6730-156">**Count** hello örnekleme aralığında alınan hello olayların sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="d6730-156">**Count** is a count of hello events received in hello sampling interval.</span></span> <span data-ttu-id="d6730-157">İstekleri gibi olaylar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6730-157">It is used for events such as requests.</span></span> <span data-ttu-id="d6730-158">Merhaba yükseklik Çeşitlemeler hello grafiğin hello olaylar meydana geldiği hello oranı Çeşitlemeler gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6730-158">Variations in hello height of hello chart indicates variations in hello rate at which hello events occur.</span></span> <span data-ttu-id="d6730-159">Ancak, hello örnekleme aralığı değiştirdiğinizde hello sayısal değer değiştiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d6730-159">But note that hello numeric value changes when you change hello sampling interval.</span></span>
* <span data-ttu-id="d6730-160">**Sum** hello örnekleme aralığı veya hello grafik hello süre üzerinden alınan tüm hello veri noktalarının hello değerleri toplar.</span><span class="sxs-lookup"><span data-stu-id="d6730-160">**Sum** adds up hello values of all hello data points received over hello sampling interval, or hello period of hello chart.</span></span>
* <span data-ttu-id="d6730-161">**Ortalama** böler hello hello aralığı içinde alınan veri noktası sayısı tarafından Sum hello.</span><span class="sxs-lookup"><span data-stu-id="d6730-161">**Average** divides hello Sum by hello number of data points received over hello interval.</span></span>
* <span data-ttu-id="d6730-162">**Benzersiz** sayıları, kullanıcıları ve hesaplarını sayısı için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6730-162">**Unique** counts are used for counts of users and accounts.</span></span> <span data-ttu-id="d6730-163">Merhaba örnekleme aralığı içinde ya da hello grafik hello süre boyunca hello şekil farklı kullanıcılar bu süre içinde görülen hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6730-163">Over hello sampling interval, or over hello period of hello chart, hello figure shows hello count of different users seen in that time.</span></span>
* <span data-ttu-id="d6730-164">**%**-Her bir toplama yüzdesi sürümleri yalnızca bölümlenmiş grafiklerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6730-164">**%** - percentage versions of each aggregation are used only with segmented charts.</span></span> <span data-ttu-id="d6730-165">Merhaba toplam her zaman too100% ekler ve farklı bileşenlerin toplam hello göreli katkı hello grafik gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6730-165">hello total always adds up too100%, and hello chart shows hello relative contribution of different components of a total.</span></span>

    ![Yüzdesi toplama](./media/app-insights-metrics-explorer/percentage-aggregation.png)

### <a name="change-hello-aggregation-type"></a><span data-ttu-id="d6730-167">Merhaba toplama türünü değiştir</span><span class="sxs-lookup"><span data-stu-id="d6730-167">Change hello aggregation type</span></span>

![Merhaba grafik düzenleyin ve ardından toplama seçin](./media/app-insights-metrics-explorer/05-aggregation.png)

<span data-ttu-id="d6730-169">Yeni bir grafik veya olduğunda tüm ölçüm seçili oluşturduğunuzda her ölçümü için hello varsayılan yöntemi gösterilir:</span><span class="sxs-lookup"><span data-stu-id="d6730-169">hello default method for each metric is shown when you create a new chart or when all metrics are deselected:</span></span>

![Tüm ölçümleri toosee hello Varsayılanları seçimini kaldırın](./media/app-insights-metrics-explorer/06-total.png)

## <a name="pin-y-axis"></a><span data-ttu-id="d6730-171">PIN y ekseni</span><span class="sxs-lookup"><span data-stu-id="d6730-171">Pin Y-axis</span></span> 
<span data-ttu-id="d6730-172">Varsayılan olarak bir grafik sıfır hello veri aralığında toogive görsel bir hello değerlerin Zamanlayıcının en yüksek değerleri kasa başlayarak Y ekseni değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6730-172">By default a chart shows Y axis values starting from zero till maximum values in hello data range, toogive a visual representation of quantum of hello values.</span></span> <span data-ttu-id="d6730-173">Ancak bazı durumlarda birden fazla ilginç toovisually olabilir hello Zamanlayıcının değerleri küçük değişiklikler inceleyin.</span><span class="sxs-lookup"><span data-stu-id="d6730-173">But in some cases more than hello quantum it might be interesting toovisually inspect minor changes in values.</span></span> <span data-ttu-id="d6730-174">Özelleştirmeleri ister için bu kullanım y ekseni aralık düzenleme özelliği toopin hello y ekseni minimum veya maksimum değeri istediğiniz yerde hello.</span><span class="sxs-lookup"><span data-stu-id="d6730-174">For customizations like this use hello Y-axis range editing feature toopin hello Y-axis minimum or maximum value at desired place.</span></span>
<span data-ttu-id="d6730-175">"Gelişmiş" onay kutusunu toobring hello yukarı üzerinde y ekseni aralığını ayarlar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d6730-175">Click on "Advanced Settings" check box toobring up hello Y-axis range Settings</span></span>

![Gelişmiş Ayarlar'ı tıklatın, özel aralık seçin ve min en yüksek değerleri belirtin](./media/app-insights-metrics-explorer/y-axis-range.png)

## <a name="filter-your-data"></a><span data-ttu-id="d6730-177">Verilerinizi filtre</span><span class="sxs-lookup"><span data-stu-id="d6730-177">Filter your data</span></span>
<span data-ttu-id="d6730-178">Seçilen özellik değerlerini birtakım toosee yalnızca hello ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="d6730-178">toosee just hello metrics for a selected set of property values:</span></span>

![Filtre'yi tıklatın, bir özelliği'ni genişletin ve bazı değerleri kontrol edin](./media/app-insights-metrics-explorer/19-filter.png)

<span data-ttu-id="d6730-180">Belirli bir özellik için herhangi bir değer seçmezseniz, onu sahip hello aynı tümünü seçmek: söz konusu özellik üzerinde hiçbir filtre yoktur.</span><span class="sxs-lookup"><span data-stu-id="d6730-180">If you don't select any values for a particular property, it's hello same as selecting them all: there is no filter on that property.</span></span>

<span data-ttu-id="d6730-181">Her özellik değerini yanında olayların bildirimi hello sayar.</span><span class="sxs-lookup"><span data-stu-id="d6730-181">Notice hello counts of events alongside each property value.</span></span> <span data-ttu-id="d6730-182">Bir özellik değerlerini seçtiğinizde hello değerleri ayarlanır diğer mülkiyet sayar.</span><span class="sxs-lookup"><span data-stu-id="d6730-182">When you select values of one property, hello counts alongside other property values are adjusted.</span></span>

<span data-ttu-id="d6730-183">Filtreler tooall hello grafikleri bir dikey pencerede uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d6730-183">Filters apply tooall hello charts on a blade.</span></span> <span data-ttu-id="d6730-184">Farklı Filtreler uygulanmış istiyorsanız toodifferent grafikleri oluşturun ve farklı ölçümleri Kanatlar kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d6730-184">If you want different filters applied toodifferent charts, create and save different metrics blades.</span></span> <span data-ttu-id="d6730-185">İsterseniz, böylece bunları diğer gördüğünüz farklı Kanatlar toohello panosundan grafikleri sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-185">If you want, you can pin charts from different blades toohello dashboard, so that you can see them alongside each other.</span></span>

### <a name="remove-bot-and-web-test-traffic"></a><span data-ttu-id="d6730-186">Bot ve web testi trafiği Kaldır</span><span class="sxs-lookup"><span data-stu-id="d6730-186">Remove bot and web test traffic</span></span>
<span data-ttu-id="d6730-187">Kullanım hello filtre **gerçek veya yapay trafiği** ve denetleme **gerçek**.</span><span class="sxs-lookup"><span data-stu-id="d6730-187">Use hello filter **Real or synthetic traffic** and check **Real**.</span></span>

<span data-ttu-id="d6730-188">Göre filtre uygulayabilirsiniz **yapay trafik kaynak**.</span><span class="sxs-lookup"><span data-stu-id="d6730-188">You can also filter by **Source of synthetic traffic**.</span></span>

### <a name="tooadd-properties-toohello-filter-list"></a><span data-ttu-id="d6730-189">tooadd özellikleri toohello filtre listesi</span><span class="sxs-lookup"><span data-stu-id="d6730-189">tooadd properties toohello filter list</span></span>
<span data-ttu-id="d6730-190">Toofilter telemetri kategorisine kendi seçme ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="d6730-190">Would you like toofilter telemetry on a category of your own choosing?</span></span> <span data-ttu-id="d6730-191">Örneğin, kullanıcılarınız farklı kategorilere yukarı bölmek olabilir ve verilerinizi kategorilerine göre segmentlere ayırmak istiyor musunuz.</span><span class="sxs-lookup"><span data-stu-id="d6730-191">For example, maybe you divide up your users into different categories, and you would like segment your data by these categories.</span></span>

<span data-ttu-id="d6730-192">[Kendi özellik oluşturmak](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="d6730-192">[Create your own property](app-insights-api-custom-events-metrics.md#properties).</span></span> <span data-ttu-id="d6730-193">Bunu kümesinde bir [Telemetri Başlatıcı](app-insights-api-custom-events-metrics.md#defaults) toohave hello standart telemetri dahil olmak üzere farklı SDK modülleri tarafından gönderilen tüm telemetri - görünür.</span><span class="sxs-lookup"><span data-stu-id="d6730-193">Set it in a [Telemetry Initializer](app-insights-api-custom-events-metrics.md#defaults) toohave it appear in all telemetry - including hello standard telemetry sent by different SDK modules.</span></span>

## <a name="edit-hello-chart-type"></a><span data-ttu-id="d6730-194">Merhaba grafik türü Düzenle</span><span class="sxs-lookup"><span data-stu-id="d6730-194">Edit hello chart type</span></span>
<span data-ttu-id="d6730-195">Kılavuzları ve grafiklerinizi arasında geçiş yapabilirsiniz dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="d6730-195">Notice that you can switch between grids and graphs:</span></span>

![Kılavuz veya grafiği seçin, sonra bir grafik türü seçin](./media/app-insights-metrics-explorer/16-chart-grid.png)

## <a name="save-your-metrics-blade"></a><span data-ttu-id="d6730-197">Ölçümleri dikey pencerenizin Kaydet</span><span class="sxs-lookup"><span data-stu-id="d6730-197">Save your metrics blade</span></span>
<span data-ttu-id="d6730-198">Bazı grafiklerde oluşturduğunuz zaman, sık kullanılan olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-198">When you've created some charts, save them as a favorite.</span></span> <span data-ttu-id="d6730-199">Kurumsal bir hesap kullanırsanız, tooshare diğer ile ekip üyelerinin olup olmadığını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-199">You can choose whether tooshare it with other team members, if you use an organizational account.</span></span>

![Sık kullanılan seçin](./media/app-insights-metrics-explorer/21-favorite-save.png)

<span data-ttu-id="d6730-201">toosee hello dikey penceresini yeniden **gidin toohello genel bakış dikey** ve Sık Kullanılanlar açın:</span><span class="sxs-lookup"><span data-stu-id="d6730-201">toosee hello blade again, **go toohello overview blade** and open Favorites:</span></span>

![Sık Kullanılanlar Hello genel bakış dikey penceresinde, seçin](./media/app-insights-metrics-explorer/22-favorite-get.png)

<span data-ttu-id="d6730-203">Kaydettiğinizde göreli zaman aralığını seçerseniz, hello dikey penceresinde hello son Ölçümleriyle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d6730-203">If you chose Relative time range when you saved, hello blade will be updated with hello latest metrics.</span></span> <span data-ttu-id="d6730-204">Mutlak zaman aralığını seçerseniz, Göster her zaman aynı veri hello.</span><span class="sxs-lookup"><span data-stu-id="d6730-204">If you chose Absolute time range, it will show hello same data every time.</span></span>

## <a name="reset-hello-blade"></a><span data-ttu-id="d6730-205">Merhaba dikey Sıfırla</span><span class="sxs-lookup"><span data-stu-id="d6730-205">Reset hello blade</span></span>
<span data-ttu-id="d6730-206">Yalnızca bir dikey pencerede düzenleyebilir, ancak tooget geri toohello özgün kaydedilmiş kümesi ister misiniz, Sıfırla'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d6730-206">If you edit a blade but then you'd like tooget back toohello original saved set, just click Reset.</span></span>

![Ölçüm Gezgini hello üstündeki Hello düğmeleri](./media/app-insights-metrics-explorer/17-reset.png)

## <a name="live-metrics-stream"></a><span data-ttu-id="d6730-208">Canlı ölçümleri akış</span><span class="sxs-lookup"><span data-stu-id="d6730-208">Live metrics stream</span></span>

<span data-ttu-id="d6730-209">Telemetrinizi hakkında daha fazla anlık görünümü için açık [canlı akış](app-insights-live-stream.md).</span><span class="sxs-lookup"><span data-stu-id="d6730-209">For a much more immediate view of your telemetry, open [Live Stream](app-insights-live-stream.md).</span></span> <span data-ttu-id="d6730-210">Çoğu ölçümleri toplama hello işlemi nedeniyle birkaç dakika tooappear alın.</span><span class="sxs-lookup"><span data-stu-id="d6730-210">Most metrics take a few minutes tooappear, because of hello process of aggregation.</span></span> <span data-ttu-id="d6730-211">Bunun aksine, Canlı ölçümleri düşük gecikme süresi için en iyi duruma getirilir.</span><span class="sxs-lookup"><span data-stu-id="d6730-211">By contrast, live metrics are optimized for low latency.</span></span> 

## <a name="set-alerts"></a><span data-ttu-id="d6730-212">Uyarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="d6730-212">Set alerts</span></span>
<span data-ttu-id="d6730-213">alışılmadık değerlerin herhangi bir ölçümü, e-postayla bildirim toobe bir uyarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6730-213">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="d6730-214">Toosend hello e-posta toohello hesap yöneticileri ya da toospecific e-posta adreslerini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-214">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![Uyarı kuralları, ekleme uyarı ölçümleri Explorer'da seçin](./media/app-insights-metrics-explorer/appinsights-413setMetricAlert.png)

<span data-ttu-id="d6730-216">[Uyarılar hakkında daha fazla bilgi][alerts].</span><span class="sxs-lookup"><span data-stu-id="d6730-216">[Learn more about alerts][alerts].</span></span>


## <a name="continuous-export"></a><span data-ttu-id="d6730-217">Sürekli Dışarı Aktarma</span><span class="sxs-lookup"><span data-stu-id="d6730-217">Continuous Export</span></span>
<span data-ttu-id="d6730-218">Böylece dışarıdan işleyebilmesi için sürekli olarak verilen verileri istiyorsanız kullanmayı [sürekli verme](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="d6730-218">If you want data continuously exported so that you can process it externally, consider using [Continuous export](app-insights-export-telemetry.md).</span></span>

### <a name="power-bi"></a><span data-ttu-id="d6730-219">Power BI</span><span class="sxs-lookup"><span data-stu-id="d6730-219">Power BI</span></span>
<span data-ttu-id="d6730-220">Verilerinizin daha zengin görünümlerini isterseniz [tooPower BI verme](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6730-220">If you want even richer views of your data, you can [export tooPower BI](http://blogs.msdn.com/b/powerbi/archive/2015/11/04/explore-your-application-insights-data-with-power-bi.aspx).</span></span>

## <a name="analytics"></a><span data-ttu-id="d6730-221">Analiz</span><span class="sxs-lookup"><span data-stu-id="d6730-221">Analytics</span></span>
<span data-ttu-id="d6730-222">[Analytics](app-insights-analytics.md) daha verimli bir şekilde tooanalyze güçlü sorgu dili kullanarak telemetrinizi değil.</span><span class="sxs-lookup"><span data-stu-id="d6730-222">[Analytics](app-insights-analytics.md) is a more versatile way tooanalyze your telemetry using a powerful query language.</span></span> <span data-ttu-id="d6730-223">Toocombine istediğiniz veya ölçümleri sonuçlarından işlem veya ayrıntılı incelenmesi uygulamanızın son performansını gerçekleştirmek, bunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6730-223">Use it if you want toocombine or compute results from metrics, or perform an in-depth exploration of your app's recent performance.</span></span> 

<span data-ttu-id="d6730-224">Bir ölçüm grafikten hello Analytics simgesi tooget tıklatabilirsiniz doğrudan toohello eşdeğer Analytics sorgu.</span><span class="sxs-lookup"><span data-stu-id="d6730-224">From a metric chart, you can click hello Analytics icon tooget directly toohello equivalent Analytics query.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d6730-225">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="d6730-225">Troubleshooting</span></span>
<span data-ttu-id="d6730-226">*Herhangi bir veri my grafikte bakın yok.*</span><span class="sxs-lookup"><span data-stu-id="d6730-226">*I don't see any data on my chart.*</span></span>

* <span data-ttu-id="d6730-227">Filtreler tooall hello grafikleri hello dikey penceresinde uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d6730-227">Filters apply tooall hello charts on hello blade.</span></span> <span data-ttu-id="d6730-228">Bir grafik odaklanan olsa da, tüm hello verilerini başka bir dışlar bir filtre ayarlamak alamadık, emin olun.</span><span class="sxs-lookup"><span data-stu-id="d6730-228">Make sure that, while you're focusing on one chart, you didn't set a filter that excludes all hello data on another.</span></span>

    <span data-ttu-id="d6730-229">Farklı grafiklerde tooset farklı filtreler istiyorsanız, bunları kaydetmek farklı dikey olarak ayrı Sık Kullanılanlar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6730-229">If you want tooset different filters on different charts, create them in different blades, save them as separate favorites.</span></span> <span data-ttu-id="d6730-230">İsterseniz, böylece bunları diğer görebilirsiniz bunları toohello Pano sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6730-230">If you want, you can pin them toohello dashboard so that you can see them alongside each other.</span></span>
* <span data-ttu-id="d6730-231">Merhaba ölçüm üzerinde tanımlı değil bir özelliği bir grafik grupla, ardından olacaktır hiçbir şey hello grafikte.</span><span class="sxs-lookup"><span data-stu-id="d6730-231">If you group a chart by a property that is not defined on hello metric, then there will be nothing on hello chart.</span></span> <span data-ttu-id="d6730-232">'Group by' temizlemeyi deneyin veya farklı gruplandırma özelliği seçin.</span><span class="sxs-lookup"><span data-stu-id="d6730-232">Try clearing 'group by', or choose a different grouping property.</span></span>
* <span data-ttu-id="d6730-233">Performans verilerini (CPU, g/ç hızı vb.) Java web Hizmetleri, Windows Masaüstü uygulamaları, kullanılabilir [IIS, uygulama ve hizmetlere Durum İzleyicisi yüklerseniz web](app-insights-monitor-performance-live-website-now.md), ve [Azure Cloud Services](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="d6730-233">Performance data (CPU, IO rate, and so on) is available for Java web services, Windows desktop apps, [IIS web apps and services if you install status monitor](app-insights-monitor-performance-live-website-now.md), and [Azure Cloud Services](app-insights-azure.md).</span></span> <span data-ttu-id="d6730-234">Azure Web siteleri için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="d6730-234">It isn't available for Azure websites.</span></span>

## <a name="video"></a><span data-ttu-id="d6730-235">Video</span><span class="sxs-lookup"><span data-stu-id="d6730-235">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="d6730-236">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6730-236">Next steps</span></span>
* [<span data-ttu-id="d6730-237">Application Insights ile kullanım izleme</span><span class="sxs-lookup"><span data-stu-id="d6730-237">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="d6730-238">Tanılama aramayı kullanma</span><span class="sxs-lookup"><span data-stu-id="d6730-238">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)

<!--Link references-->

[alerts]: app-insights-alerts.md
[start]: app-insights-overview.md
[track]: app-insights-api-custom-events-metrics.md
