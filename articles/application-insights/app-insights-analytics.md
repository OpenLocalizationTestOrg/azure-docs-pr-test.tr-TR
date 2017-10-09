---
title: "aaaAnalytics - hello güçlü arama aracının Azure Application Insights | Microsoft Docs"
description: "Analytics, Application Insights hello güçlü tanılama arama aracının genel bakış. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="65a20-103">Application Insights analizleri</span><span class="sxs-lookup"><span data-stu-id="65a20-103">Analytics in Application Insights</span></span>
<span data-ttu-id="65a20-104">[Analytics](app-insights-analytics.md) hello güçlü arama özelliği [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65a20-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="65a20-105">Bu sayfaları günlük analizi sorgu dili açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="65a20-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="65a20-106">**[Merhaba tanıtım videosunu izleyin](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="65a20-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="65a20-107">**[Benzetimli verilerimizi Analytics sürücüde test](https://analytics.applicationinsights.io/demo)**  uygulamanızı veri tooApplication Öngörüler henüz değil gönderiliyorsa.</span><span class="sxs-lookup"><span data-stu-id="65a20-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="65a20-108">**[SQL-kullanıcıların kopya sayfası](https://aka.ms/sql-analytics)**  hello en yaygın deyimleri çevirir.</span><span class="sxs-lookup"><span data-stu-id="65a20-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="65a20-109">**[Dil Başvurusu](app-insights-analytics-reference.md)**  nasıl toouse tüm hello hello günlük analizi sorgu dili güçlü özelliklerini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="65a20-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="65a20-110">Sorgularda Analytics</span><span class="sxs-lookup"><span data-stu-id="65a20-110">Queries in Analytics</span></span>
<span data-ttu-id="65a20-111">Tipik bir sorgu bir *kaynak* tablo izleyen bir dizi tarafından *işleçleri* ayırarak `|`.</span><span class="sxs-lookup"><span data-stu-id="65a20-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="65a20-112">Örneğin, günlük hello kullanıcılarının Hyderabad, ne zaman web uygulamamız denemenin şimdi bulun.</span><span class="sxs-lookup"><span data-stu-id="65a20-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="65a20-113">Ve var ki olsa da, hangi sonuç kodları tootheir HTTP isteklerini döndürülür görelim.</span><span class="sxs-lookup"><span data-stu-id="65a20-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="65a20-114">Biz, farklı istemci IP adresleri, hello saat hello tarafından hello son 7 gün gruplandırarak sayısı.</span><span class="sxs-lookup"><span data-stu-id="65a20-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="65a20-115">Merhaba önceki 24h dışında tooget sonuçları 'timestamp' açıkça sorgunuzda yer ya da hello zaman aralığı açılan menüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="65a20-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="65a20-116">Şimdi toostack hello sonuçları farklı yanıt kodları seçme grafik sunu çubuğu hello hello sonuçlarıyla görüntüle:</span><span class="sxs-lookup"><span data-stu-id="65a20-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![Çubuk grafiği, x ve y eksenleri ardından kesimleme seçin](./media/app-insights-analytics/020.png)

<span data-ttu-id="65a20-118">Lunchtime ve Hyderabad yatak zamanında uygulamamıza en popüler olduğu gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="65a20-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="65a20-119">(Ve bu 500 kodlar araştırmanız gerekir.)</span><span class="sxs-lookup"><span data-stu-id="65a20-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="65a20-120">Güçlü istatistiksel işlemler vardır:</span><span class="sxs-lookup"><span data-stu-id="65a20-120">There are also powerful statistical operations:</span></span>

![İstatistiksel sorgu sonuçları](./media/app-insights-analytics/025.png)

<span data-ttu-id="65a20-122">Merhaba dil çok çekici özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="65a20-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="65a20-123">[Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) ölçümleri ve özel özellikler de dahil olmak üzere herhangi bir sorgu tarafından ham uygulama telemetrinizi.</span><span class="sxs-lookup"><span data-stu-id="65a20-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="65a20-124">[Katılma](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) birden çok tabloları – sayfa görünümleri, bağımlılık çağrıları, özel durumlar ve günlük izlemelerini ile ilişkilendirmek ister.</span><span class="sxs-lookup"><span data-stu-id="65a20-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="65a20-125">Güçlü istatistiksel [toplamalar](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="65a20-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="65a20-126">Yalnızca, SQL kadar güçlü ve karmaşık sorgular için çok daha kolay: iç içe geçmiş deyimler yerine, bir başlangıç işlemi toohello hello verilerden sonraki kanal.</span><span class="sxs-lookup"><span data-stu-id="65a20-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="65a20-127">Anında ve güçlü görselleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="65a20-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="65a20-128">[PIN grafikleri tooAzure panolar](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="65a20-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="65a20-129">[Sorguları tooPower BI verme](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="65a20-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="65a20-130">Var olan bir [REST API](https://dev.applicationinsights.io/) toorun sorguları program aracılığıyla, örneğin Powershell'den kullanabileceğinizi.</span><span class="sxs-lookup"><span data-stu-id="65a20-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="65a20-131">Tooyour uygulama istatistikleri verilerine bağlanma</span><span class="sxs-lookup"><span data-stu-id="65a20-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="65a20-132">Uygulamanızın analizi açmak [genel bakış dikey penceresinde](app-insights-dashboards.md) Application ınsights'ta:</span><span class="sxs-lookup"><span data-stu-id="65a20-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Portal.Azure.com açın, Application Insights kaynağınıza açın ve analizi'ı tıklatın.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="65a20-134">Video</span><span class="sxs-lookup"><span data-stu-id="65a20-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="65a20-135">Sorgu örnekleri</span><span class="sxs-lookup"><span data-stu-id="65a20-135">Query examples</span></span>

<span data-ttu-id="65a20-136">Bu izlenecek yollar tooillustrate hello güç Analytics kullanmanın deneyin:</span><span class="sxs-lookup"><span data-stu-id="65a20-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="65a20-137">Otomatik tanılamayı ani ve adım istekleri süreleri atlar.</span><span class="sxs-lookup"><span data-stu-id="65a20-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="65a20-138">Zaman serisi analiz ile performans degradations analiz etme</span><span class="sxs-lookup"><span data-stu-id="65a20-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="65a20-139">Uygulama hataları autocluster ve diffpatterns analiz etme</span><span class="sxs-lookup"><span data-stu-id="65a20-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="65a20-140">Zaman serisi analiz ile Gelişmiş şekli algılama</span><span class="sxs-lookup"><span data-stu-id="65a20-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="65a20-141">(MAU/DAU vb. çalışırken) kayan pencere işlemleri tooanalyze uygulama kullanımı kullanma</span><span class="sxs-lookup"><span data-stu-id="65a20-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="65a20-142">[Hizmet kesilmelerini algılanması tabanlı hata ayıklama günlüklerini analiz üzerinde](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span><span class="sxs-lookup"><span data-stu-id="65a20-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="65a20-143">[Basit hata ayıklama günlüklerini kullanarak uygulamalarınızın performans profili oluşturma](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="65a20-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="65a20-144">[Basit hata ayıklama günlüklerini kullanarak, kodu akışınızı her adımı için Hello süresini ölçme](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="65a20-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="65a20-145">[Çözümleme eşzamanlılık basit hata ayıklama günlüklerini kullanarak](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="65a20-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="65a20-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65a20-146">Next steps</span></span>
* <span data-ttu-id="65a20-147">Merhaba ile başlattığınız öneririz [dil Turu](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="65a20-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="65a20-148">Hakkında daha fazla bilgi [analizi kullanarak](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="65a20-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="65a20-149">[Dil Başvurusu](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="65a20-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
