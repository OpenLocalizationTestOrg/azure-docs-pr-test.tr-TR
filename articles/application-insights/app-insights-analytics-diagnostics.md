---
title: "Azure Application Insights web uygulaması performans değişikliklerin aaaSmart tanılama | Microsoft Docs"
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
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="a4238-103">Uygulama telemetrinizi ani değişiklikler tanılama</span><span class="sxs-lookup"><span data-stu-id="a4238-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="a4238-104">*Bu özelliğin önizlemede değil.*</span><span class="sxs-lookup"><span data-stu-id="a4238-104">*This feature is in preview.*</span></span>

<span data-ttu-id="a4238-105">Web uygulamanızın performansı veya tek bir tıklatmayla kullanımı ani değişiklikler tanılamak!</span><span class="sxs-lookup"><span data-stu-id="a4238-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="a4238-106">Merhaba akıllı Tanılama özelliğini, her zaman grafik oluşturduğunuzda kullanılabilir [Analytics](app-insights-analytics.md) içinde [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4238-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a4238-107">Bir depo veya bir DIP gibi sonuçlarınızı hello eğilimini olağan dışı bir değişiklik olduğunda akıllı tanılama bir desen boyutları ve hello değişiklik açıklayabilir ilgili değerleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a4238-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="a4238-108">Bu, hızlı bir şekilde hello sorunu tanılamak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a4238-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="a4238-109">Bu örnekte, akıllı tanılama hello değişiklikle ilişkili özellik değerlerinin bir desen belirledi ve sonuçları ile ve bu deseni olmadan hello birbirinden vurgular:</span><span class="sxs-lookup"><span data-stu-id="a4238-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![Örnek analytics Tanılama sonucu](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="a4238-111">Veri değişikliklerini tanılama</span><span class="sxs-lookup"><span data-stu-id="a4238-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="a4238-112">Analizleri bir sorgu çalıştırın ve zaman grafik olarak işleme.</span><span class="sxs-lookup"><span data-stu-id="a4238-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="a4238-113">Varsa herhangi bir vurgulanan yoğun noktasını'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a4238-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![yoğun noktası](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="a4238-115">Tanılama birkaç saniye sürer toodiscover bir desen.</span><span class="sxs-lookup"><span data-stu-id="a4238-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="a4238-116">Merhaba Tanılama sonuçları sekmesi, veri süreksizlik açıklayabilir bir desen gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4238-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![Sonuç](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="a4238-118">Merhaba metni hello shift ile toocorrelate görünür hello boyut değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4238-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="a4238-119">Bu örnekte, belirli bir istek ve belirli tarayıcı sürümü ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="a4238-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="a4238-120">Ayrıca hello grafikle hello filtre true ve false hello iki bileşenlerinin dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a4238-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="a4238-121">Merhaba false bileşen değişmeden eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4238-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="a4238-122">Diğer bir deyişle, biz hello sorunlu birleşimlerini tanılama tanımladığı bıraksanız hello telemetri sonuçlarında değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="a4238-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="a4238-123">Bunun aksine, bu bileşimi içinde hello sonuçları çarpıcı değişiklik gösterir ve bu da araştırma vurgulanmış hello alanı içinde.</span><span class="sxs-lookup"><span data-stu-id="a4238-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="a4238-124">Bu tanılama hello değişiklik açıklayan özellikleri bileşimini buldu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4238-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="a4238-125">Merhaba düzeni karmaşıksa toohover üzerinden ihtiyacınız **Tümünü Göster** toosee hello boyutları.</span><span class="sxs-lookup"><span data-stu-id="a4238-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![tümünü göster](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="a4238-127">Hiçbir önemli düzeni toonotify 'sonuç' sayfa sunulur hello hakkında tanılama bulur durumda.</span><span class="sxs-lookup"><span data-stu-id="a4238-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="a4238-128">Bu noktada, sorgunuzu değişebilir.</span><span class="sxs-lookup"><span data-stu-id="a4238-128">At this point, you may change your query.</span></span> <span data-ttu-id="a4238-129">Örneğin, hello zaman aralığı ve daha fazla çözümleme ve potansiyel olarak daha iyi sonuçlar için Analytics sorgu binning daraltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4238-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="a4238-130">Web sitenizin belirli bir sayfa üzerinde belirli bir tarayıcı bir sorun olduğunu hello bilen sayesinde artık düz toohello sorun sayfasına gidin ve en son değişiklikler araştırın.</span><span class="sxs-lookup"><span data-stu-id="a4238-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="a4238-131">Merhaba Tanıtımı deneyin</span><span class="sxs-lookup"><span data-stu-id="a4238-131">Try hello demo</span></span>

<span data-ttu-id="a4238-132">[Toosee Tanıtımı burayı](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) örnek verileri.</span><span class="sxs-lookup"><span data-stu-id="a4238-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="a4238-133">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="a4238-133">How it works</span></span>

<span data-ttu-id="a4238-134">Akıllı tanılama üzerinde hello dayalı bir Gelişmiş Denetimsiz machine learning algoritmasını kullanan [DiffPatterns](app-insights-analytics-reference.md) işlemi.</span><span class="sxs-lookup"><span data-stu-id="a4238-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="a4238-135">Merhaba veri değişikliği açıklayabilir için aday desenleri görünüyor.</span><span class="sxs-lookup"><span data-stu-id="a4238-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="a4238-136">Her adayı hello ölçüm üzerindeki etkisini hello analizleri yaparken ve en iyi hello değişiklikle karşılık gelen hello deseni gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4238-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="a4238-137">Tanılama noktası yok?</span><span class="sxs-lookup"><span data-stu-id="a4238-137">No diagnostic points?</span></span>

<span data-ttu-id="a4238-138">Ölçüt aşağıdaki hello sağlandığında akıllı tanılama yalnızca çalışır:</span><span class="sxs-lookup"><span data-stu-id="a4238-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="a4238-139">Akıllı tanılama ayarını açık.</span><span class="sxs-lookup"><span data-stu-id="a4238-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="a4238-140">Merhaba ayarlar simgesine analytics'te kısmına bakın.</span><span class="sxs-lookup"><span data-stu-id="a4238-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="a4238-141">Merhaba analizi ayarları akıllı tanılama seçeneğinde seçilir.</span><span class="sxs-lookup"><span data-stu-id="a4238-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="a4238-142">Zaman ekseni: hello hello grafiğin x ekseni türde olmalıdır `datetime`.</span><span class="sxs-lookup"><span data-stu-id="a4238-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="a4238-143">Çizgi veya alan grafiği: Tanılama yalnızca bu tür grafik çalışır.</span><span class="sxs-lookup"><span data-stu-id="a4238-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="a4238-144">Kullanım `| render timechart` veya `| render areachart` ; sorgunuzu hello sonunda veya satır ya da alan grafiği hello açılan seçicisini seçin.</span><span class="sxs-lookup"><span data-stu-id="a4238-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="a4238-145">Süreksizlik: Hello verilerde önemli süreksizlik koyulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a4238-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="a4238-146">Yeterli noktaları tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="a4238-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="a4238-147">Birden fazla hello sorgu yan tümcesinde özetler.</span><span class="sxs-lookup"><span data-stu-id="a4238-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="a4238-148">Merhaba önce adı tanımını içeren hiçbir proje yan tümcesi özetler.</span><span class="sxs-lookup"><span data-stu-id="a4238-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="a4238-149">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="a4238-149">Related articles</span></span>

 * [<span data-ttu-id="a4238-150">Analytics Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="a4238-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="a4238-151">[Akıllı algılama](app-insights-proactive-diagnostics.md) tooperformance sorunları otomatik olarak sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="a4238-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
