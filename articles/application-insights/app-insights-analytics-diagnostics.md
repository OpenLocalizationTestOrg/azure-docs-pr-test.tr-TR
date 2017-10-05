---
title: "Azure Application Insights web uygulaması performans değişikliklerin tanılama akıllı | Microsoft Docs"
description: "Otomatik tanılama ani veya performans telemetrisini adımlarda web uygulamanızdan."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="35f4c-103">Uygulama telemetrinizi ani değişiklikler tanılama</span><span class="sxs-lookup"><span data-stu-id="35f4c-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="35f4c-104">*Bu özelliğin önizlemede değil.*</span><span class="sxs-lookup"><span data-stu-id="35f4c-104">*This feature is in preview.*</span></span>

<span data-ttu-id="35f4c-105">Web uygulamanızın performansı veya tek bir tıklatmayla kullanımı ani değişiklikler tanılamak!</span><span class="sxs-lookup"><span data-stu-id="35f4c-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="35f4c-106">Her zaman grafik oluşturduğunuzda akıllı tanılama özelliği kullanılabilir [Analytics](app-insights-analytics.md) içinde [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="35f4c-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="35f4c-107">Bir depo veya bir DIP gibi sonuçlarınızı eğilimi olağan dışı bir değişiklik olduğunda akıllı tanılama bir desen boyutları ve değişiklik açıklayabilir ilgili değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35f4c-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="35f4c-108">Bu sorunu hızlı tanılamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="35f4c-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="35f4c-109">Bu örnekte, akıllı tanılama değişiklikle ilişkili özellik değerlerinin bir desen belirledi ve sonuçları ile ve bu deseni olmadan arasındaki farkı vurgular:</span><span class="sxs-lookup"><span data-stu-id="35f4c-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![Örnek analytics Tanılama sonucu](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="35f4c-111">Veri değişikliklerini tanılama</span><span class="sxs-lookup"><span data-stu-id="35f4c-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="35f4c-112">Analizleri bir sorgu çalıştırın ve zaman grafik olarak işleme.</span><span class="sxs-lookup"><span data-stu-id="35f4c-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="35f4c-113">Varsa herhangi bir vurgulanan yoğun noktasını'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="35f4c-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![yoğun noktası](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="35f4c-115">Tanılama bir desen keşfetmek için birkaç saniye sürer.</span><span class="sxs-lookup"><span data-stu-id="35f4c-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="35f4c-116">Tanılama sonuçları sekmesi, veri süreksizlik açıklayabilir bir desen gösterir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![Sonuç](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="35f4c-118">Metin kaydırma ile ilişkilendirmek için görüntülenen boyut değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="35f4c-119">Bu örnekte, belirli bir istek ve belirli tarayıcı sürümü ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="35f4c-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="35f4c-120">Filtre true ve false grafik de iki bileşenden dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="35f4c-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="35f4c-121">False bileşen değişmeden eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="35f4c-122">Diğer bir deyişle, biz tanılama belirledi sorunlu birleşimlerini bıraksanız telemetri sonuçlarında değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="35f4c-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="35f4c-123">Bunun aksine, sonuçları bu bileşimi içinde çarpıcı bir değişiklik araştırma vurgulanmış alanı içinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="35f4c-124">Bu tanılama değişikliği açıklayan özellikleri bileşimini buldu gösterir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="35f4c-125">Desen karmaşıksa üzerine gelerek gerek **Tümünü Göster** boyutları görmek için.</span><span class="sxs-lookup"><span data-stu-id="35f4c-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![tümünü göster](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="35f4c-127">Tanılama hakkında bilgilendirmek için önemli hiçbir desen bulur durumda ' yok ' sunulduğunu sunulur.</span><span class="sxs-lookup"><span data-stu-id="35f4c-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="35f4c-128">Bu noktada, sorgunuzu değişebilir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-128">At this point, you may change your query.</span></span> <span data-ttu-id="35f4c-129">Örneğin, zaman aralığı ve daha fazla çözümleme için Analytics sorgu binning daraltmak ve olası sonuçları daha iyi.</span><span class="sxs-lookup"><span data-stu-id="35f4c-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="35f4c-130">Web sitenizin belirli bir sayfa üzerinde belirli bir tarayıcı bir sorun olduğunu bilen sayesinde artık doğrudan sorun sayfasına gidin ve en son değişiklikler araştırın.</span><span class="sxs-lookup"><span data-stu-id="35f4c-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="35f4c-131">Demoyu deneyin</span><span class="sxs-lookup"><span data-stu-id="35f4c-131">Try the demo</span></span>

<span data-ttu-id="35f4c-132">[Bir örnek görmek için burayı tıklatın](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) örnek verileri.</span><span class="sxs-lookup"><span data-stu-id="35f4c-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="35f4c-133">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="35f4c-133">How it works</span></span>

<span data-ttu-id="35f4c-134">Akıllı tanılama dayalı bir Gelişmiş Denetimsiz makine öğrenme algoritmasını kullanan [DiffPatterns](app-insights-analytics-reference.md) işlemi.</span><span class="sxs-lookup"><span data-stu-id="35f4c-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="35f4c-135">Veri değişikliği açıklayabilir için aday desenleri görünüyor.</span><span class="sxs-lookup"><span data-stu-id="35f4c-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="35f4c-136">Her adayı ölçüm üzerindeki etkisini analizleri yaparken ve en iyi değişikliğe karşılık gelen deseni gösterir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="35f4c-137">Tanılama noktası yok?</span><span class="sxs-lookup"><span data-stu-id="35f4c-137">No diagnostic points?</span></span>

<span data-ttu-id="35f4c-138">Aşağıdaki ölçütler sağlandığında akıllı tanılama yalnızca çalışır:</span><span class="sxs-lookup"><span data-stu-id="35f4c-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="35f4c-139">Akıllı tanılama ayarını açık.</span><span class="sxs-lookup"><span data-stu-id="35f4c-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="35f4c-140">Analytics'te ayarlar simgesinin altında arayın.</span><span class="sxs-lookup"><span data-stu-id="35f4c-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="35f4c-141">Analytics ayarlarında akıllı tanılama seçenek seçilidir.</span><span class="sxs-lookup"><span data-stu-id="35f4c-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="35f4c-142">Zaman ekseni: grafiğin x ekseni türde olmalıdır `datetime`.</span><span class="sxs-lookup"><span data-stu-id="35f4c-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="35f4c-143">Çizgi veya alan grafiği: Tanılama yalnızca bu tür grafik çalışır.</span><span class="sxs-lookup"><span data-stu-id="35f4c-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="35f4c-144">Kullanım `| render timechart` veya `| render areachart` sorgunuzu; sonunda veya satır ya da alan grafiği açılan seçicisini seçin.</span><span class="sxs-lookup"><span data-stu-id="35f4c-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="35f4c-145">Süreksizlik: Verileri önemli süreksizlik koyulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35f4c-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="35f4c-146">Analiz etmek için yeterli noktaları.</span><span class="sxs-lookup"><span data-stu-id="35f4c-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="35f4c-147">Birden fazla sorgu yan tümcesinde özetler.</span><span class="sxs-lookup"><span data-stu-id="35f4c-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="35f4c-148">Özetleme yan tümcesi önce adı tanımını içeren hiçbir proje yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="35f4c-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="35f4c-149">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="35f4c-149">Related articles</span></span>

 * [<span data-ttu-id="35f4c-150">Analytics Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="35f4c-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="35f4c-151">[Akıllı algılama](app-insights-proactive-diagnostics.md) performans sorunları otomatik olarak sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="35f4c-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>