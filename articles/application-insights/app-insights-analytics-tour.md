---
title: "Azure Application Insights Analytics üzerinden aaaA tur | Microsoft Docs"
description: "Tüm hello ana sorgularda Analytics, Application Insights hello güçlü arama aracının kısa örnekleri."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="839bb-103">Application ınsights'ta Analytics turu</span><span class="sxs-lookup"><span data-stu-id="839bb-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="839bb-104">[Analytics](app-insights-analytics.md) hello güçlü arama özelliği [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="839bb-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="839bb-105">Bu sayfaları günlük analizi sorgu dili açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="839bb-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="839bb-106">**[Merhaba tanıtım videosunu izleyin](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="839bb-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="839bb-107">**[Benzetimli verilerimizi Analytics sürücüde test](https://analytics.applicationinsights.io/demo)**  uygulamanızı veri tooApplication Öngörüler henüz değil gönderiliyorsa.</span><span class="sxs-lookup"><span data-stu-id="839bb-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="839bb-108">**[SQL-kullanıcıların kopya sayfası](https://aka.ms/sql-analytics)**  hello en yaygın deyimleri çevirir.</span><span class="sxs-lookup"><span data-stu-id="839bb-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="839bb-109">Başlattığınız bazı temel sorguları tooget aracılığıyla ilerlemesi atalım.</span><span class="sxs-lookup"><span data-stu-id="839bb-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="839bb-110">Tooyour uygulama istatistikleri verilerine bağlanma</span><span class="sxs-lookup"><span data-stu-id="839bb-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="839bb-111">Uygulamanızın analizi açmak [genel bakış dikey penceresinde](app-insights-dashboards.md) Application ınsights'ta:</span><span class="sxs-lookup"><span data-stu-id="839bb-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Portal.Azure.com açın, Application Insights kaynağınıza açın ve analizi'ı tıklatın.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="839bb-113">[Ele](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): n satırları göster</span><span class="sxs-lookup"><span data-stu-id="839bb-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="839bb-114">Kullanıcı işlemleri (web uygulamanız tarafından alınan genellikle HTTP isteklerini) oturum veri noktaları denilen bir tabloda depolanır `requests`.</span><span class="sxs-lookup"><span data-stu-id="839bb-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="839bb-115">Her satır, uygulamanıza Application Insights SDK'sı hello alınan telemetri bir veri noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="839bb-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="839bb-116">Merhaba tablonun birkaç örnek satırlarını inceleyerek başlayalım:</span><span class="sxs-lookup"><span data-stu-id="839bb-116">Let's start by examining a few sample rows of hello table:</span></span>

![sonuçlar](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="839bb-118">Git tıklamadan önce hello imleç hello deyiminde yere yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="839bb-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="839bb-119">Bir deyim birden fazla hattından bölebilirsiniz ancak boş satırlar bir deyimde koymayın.</span><span class="sxs-lookup"><span data-stu-id="839bb-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="839bb-120">Boş satırlar olan uygun şekilde tookeep birkaç ayrı hello penceresinde sorgular.</span><span class="sxs-lookup"><span data-stu-id="839bb-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="839bb-121">Sütunları seçin, bunları sütunlara göre Gruplandır sürükleyin ve filtre:</span><span class="sxs-lookup"><span data-stu-id="839bb-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Sütun Seçimi sonuçlarının üst sağ tıklatın](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="839bb-123">Hiçbir öğe toosee hello ayrıntı genişletin:</span><span class="sxs-lookup"><span data-stu-id="839bb-123">Expand any item toosee hello detail:</span></span>

![Tablo seçin ve yapılandırma sütunları kullanın](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="839bb-125">Bir sütun toore düzeni hello sonuçları hello web tarayıcısında kullanılabilir Hello başı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="839bb-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="839bb-126">Ancak büyük sonuç kümesi için satır indirilen toohello tarayıcı hello sayısı sınırlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="839bb-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="839bb-127">Bu şekilde sıralama, her zaman en yüksek gerçek hello veya en düşük öğeleri göstermez.</span><span class="sxs-lookup"><span data-stu-id="839bb-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="839bb-128">toosort öğelerini güvenilir bir şekilde, hello kullanma `top` veya `sort` işleci.</span><span class="sxs-lookup"><span data-stu-id="839bb-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="839bb-129">[Üst](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) ve [sıralama](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="839bb-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="839bb-130">`take`yararlı tooget bir sonuç hızlı örneğidir ancak hello tablodaki belirli bir sırada gösterir.</span><span class="sxs-lookup"><span data-stu-id="839bb-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="839bb-131">tooget sıralı bir görünümü kullanmak `top` (için bir örnek) veya `sort` (üzerinden hello tüm tablo).</span><span class="sxs-lookup"><span data-stu-id="839bb-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="839bb-132">Belirli bir sütuna göre sıralanmış hello ilk n satırları göster:</span><span class="sxs-lookup"><span data-stu-id="839bb-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="839bb-133">*Sözdizimi:* çoğu işleçleri gibi anahtar sözcüğü parametrelere sahip `by`.</span><span class="sxs-lookup"><span data-stu-id="839bb-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="839bb-134">`desc`azalan düzende = `asc` artan =.</span><span class="sxs-lookup"><span data-stu-id="839bb-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="839bb-135">`top...`Daha fazla kullanıcı bildiren yoludur `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="839bb-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="839bb-136">Biz yazılı:</span><span class="sxs-lookup"><span data-stu-id="839bb-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="839bb-137">Merhaba sonuç aynı Merhaba, ancak biraz daha yavaş çalışır olacaktır.</span><span class="sxs-lookup"><span data-stu-id="839bb-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="839bb-138">(Ayrıca yazabilirsiniz `order`, bir diğer ad olduğu `sort`.)</span><span class="sxs-lookup"><span data-stu-id="839bb-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="839bb-139">Merhaba Tablo görünümünde Hello sütun üst bilgileri de Merhaba ekranında kullanılan toosort hello sonuçları olabilir.</span><span class="sxs-lookup"><span data-stu-id="839bb-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="839bb-140">Ancak, kullandıysanız Kuşkusuz `take` veya `top` tooretrieve yalnızca bir tablonun parçası, alınan yalnızca yeniden sıralamak hello kayıtları gerekir.</span><span class="sxs-lookup"><span data-stu-id="839bb-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="839bb-141">[Burada](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): bir koşula göre filtreleme</span><span class="sxs-lookup"><span data-stu-id="839bb-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="839bb-142">Belirli Sonuç kodu döndürdü yalnızca istekleri görelim:</span><span class="sxs-lookup"><span data-stu-id="839bb-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="839bb-143">Merhaba `where` işleci bir Boole ifadesi alır.</span><span class="sxs-lookup"><span data-stu-id="839bb-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="839bb-144">Bunlarla ilgili bazı önemli noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="839bb-144">Here are some key points about them:</span></span>

* <span data-ttu-id="839bb-145">`and`, `or`: Boole işleçleri</span><span class="sxs-lookup"><span data-stu-id="839bb-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="839bb-146">`==`, `<>`, `!=` : eşit ve eşit değil</span><span class="sxs-lookup"><span data-stu-id="839bb-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="839bb-147">`=~`, `!~` : büyük küçük harf duyarlı dize eşit ve eşit değil.</span><span class="sxs-lookup"><span data-stu-id="839bb-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="839bb-148">Daha fazla dize karşılaştırma işleçleri çok vardır.</span><span class="sxs-lookup"><span data-stu-id="839bb-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="839bb-149">Merhaba sağ türü alınıyor</span><span class="sxs-lookup"><span data-stu-id="839bb-149">Getting hello right type</span></span>
<span data-ttu-id="839bb-150">Başarısız istekleri Bul:</span><span class="sxs-lookup"><span data-stu-id="839bb-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="839bb-151">Zaman</span><span class="sxs-lookup"><span data-stu-id="839bb-151">Time</span></span>

<span data-ttu-id="839bb-152">Varsayılan olarak, sorgularınızı kısıtlı toohello son 24 saat etkilenir.</span><span class="sxs-lookup"><span data-stu-id="839bb-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="839bb-153">Ancak bu aralığı değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="839bb-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="839bb-154">İlgili herhangi bir sorgu yazarak Hello zaman aralığını geçersiz kılma `timestamp` where yan tümcesinde.</span><span class="sxs-lookup"><span data-stu-id="839bb-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="839bb-155">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="839bb-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="839bb-156">Merhaba zaman aralığı eşdeğer tooa 'where' yan tümcesi hello kaynak tabloları birinin her Bahsetme sonra eklenen bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="839bb-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="839bb-157">`ago(3d)`'üç gün önce' anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="839bb-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="839bb-158">Diğer birimleri süreyi saat dahil et (`2h`, `2.5h`), dakika (`25m`) ve saniye (`10s`).</span><span class="sxs-lookup"><span data-stu-id="839bb-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="839bb-159">Diğer örnekler:</span><span class="sxs-lookup"><span data-stu-id="839bb-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="839bb-160">[Tarihler ve saatlere başvuru](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="839bb-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="839bb-161">[Proje](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): sütunları işlem seçin ve yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="839bb-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="839bb-162">Kullanım [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick istediğiniz hello sütun çıkışı:</span><span class="sxs-lookup"><span data-stu-id="839bb-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="839bb-163">Sütunları yeniden adlandırın ve yenilerini tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="839bb-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![Sonuç](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="839bb-165">Sütun adları, boşluk içerebilir veya bunlar köşeli parantez içindeki, simgeler şöyle: `['...']` veya`["..."]`</span><span class="sxs-lookup"><span data-stu-id="839bb-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="839bb-166">`%`Merhaba modulo işleci normal ' dir.</span><span class="sxs-lookup"><span data-stu-id="839bb-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="839bb-167">`1d`(bir basamak biri olan sonra bir 'D ') bir timespan değişmez değer bir gün anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="839bb-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="839bb-168">Daha fazla bazı timespan değişmez değerler şunlardır: `12h`, `30m`, `10s`, `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="839bb-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="839bb-169">`floor`(diğer ad `bin`) bir değer birden çok sağladığınız hello taban değeri en yakın toohello aşağı yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="839bb-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="839bb-170">Bu nedenle `floor(aTime, 1s)` birer ikinci en yakın toohello aşağı yuvarlar.</span><span class="sxs-lookup"><span data-stu-id="839bb-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="839bb-171">İfadeler, tüm hello normal işleçleri içerebilir (`+`, `-`,...), ve bir dizi kullanışlı işlevi yoktur.</span><span class="sxs-lookup"><span data-stu-id="839bb-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="839bb-172">Genişletme</span><span class="sxs-lookup"><span data-stu-id="839bb-172">Extend</span></span>
<span data-ttu-id="839bb-173">Yalnızca var olanları tooadd sütunları toohello istiyorsanız, kullanmak [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="839bb-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="839bb-174">Kullanarak [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) daha az ayrıntılıdır [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) tookeep istiyorsanız tüm var olan sütunlar hello.</span><span class="sxs-lookup"><span data-stu-id="839bb-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="839bb-175">Toolocal zaman Dönüştür</span><span class="sxs-lookup"><span data-stu-id="839bb-175">Convert toolocal time</span></span>

<span data-ttu-id="839bb-176">Zaman damgaları her zaman UTC biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="839bb-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="839bb-177">Bu nedenle hello BİZE Pasifik Yakası üzerinde olduğunuz ve Kış ise, bu istediğiniz:</span><span class="sxs-lookup"><span data-stu-id="839bb-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="839bb-178">[Özetlemek](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): toplam satır grupları</span><span class="sxs-lookup"><span data-stu-id="839bb-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="839bb-179">`Summarize`Belirtilen bir geçerlidir *toplama işlevi* satır grupları üzerinden.</span><span class="sxs-lookup"><span data-stu-id="839bb-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="839bb-180">Örneğin, web uygulamanızı toorespond tooa isteği hello süresini hello alanında bildirilir `duration`.</span><span class="sxs-lookup"><span data-stu-id="839bb-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="839bb-181">Görelim hello ortalama yanıt süresi tooall istekleri:</span><span class="sxs-lookup"><span data-stu-id="839bb-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="839bb-182">Veya biz hello sonuç farklı adlar istekleri ayrı:</span><span class="sxs-lookup"><span data-stu-id="839bb-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="839bb-183">`Summarize`toplar hangi hello için gruplar halinde veri noktaları hello akışında hello `by` yan tümcesi eşit olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="839bb-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="839bb-184">Merhaba yer alan her değerin `by` ifade - her işlem adı örnek yukarıda hello - hello sonuç tablosunda bir satırı sonuçlanıyor.</span><span class="sxs-lookup"><span data-stu-id="839bb-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="839bb-185">Veya sonuçları günün saatini göre gruplandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="839bb-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="839bb-186">Biz hello nasıl kullanmakta olduğunuz fark `bin` işlevi (diğer adıyla `floor`).</span><span class="sxs-lookup"><span data-stu-id="839bb-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="839bb-187">Yalnızca kullansaydık `by timestamp`, kendi az grubunda her giriş satır yapmış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="839bb-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="839bb-188">Sürekli bir skaler için LIKE kez veya numaraları toobreak hello sürekli aralığına ayrık değerler yönetilebilir bir dizi sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="839bb-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="839bb-189">`bin`-yalnızca hello tanıdık yuvarlama aşağı olduğu `floor` işlev - hello en kolay yolu toodo olduğundan.</span><span class="sxs-lookup"><span data-stu-id="839bb-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="839bb-190">Biz kullanabilirsiniz hello dizeleri aynı teknik tooreduce aralığı:</span><span class="sxs-lookup"><span data-stu-id="839bb-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="839bb-191">Kullanabileceğiniz bildirimi `name=` hello toplama ifadeleri veya hello tarafından yan tümcesi bir sonuç sütunu tooset hello adı.</span><span class="sxs-lookup"><span data-stu-id="839bb-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="839bb-192">Sayım örneklenen verileri</span><span class="sxs-lookup"><span data-stu-id="839bb-192">Counting sampled data</span></span>
<span data-ttu-id="839bb-193">`sum(itemCount)`Merhaba toocount olaylarını toplama önerilen olur.</span><span class="sxs-lookup"><span data-stu-id="839bb-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="839bb-194">Çoğu durumda, ItemCount hello işlevi yalnızca hello hello Grup satır sayısı yukarı sayar şekilde == 1.</span><span class="sxs-lookup"><span data-stu-id="839bb-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="839bb-195">Ancak zaman [örnekleme](app-insights-sampling.md) olan işleminde, yalnızca bir kesir hello özgün olayların korunur Application ınsights'ta veri noktaları olarak gördüğünüz her veri noktası için vardır; böylece `itemCount` olaylar.</span><span class="sxs-lookup"><span data-stu-id="839bb-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="839bb-196">Örnekleme %75 hello özgün olayları, daha sonra ItemCount atar, örneğin, == 4 korunur hello kayıtlarında - diğer bir deyişle, tutulan her kayıt için vardı dört özgün kaydeder.</span><span class="sxs-lookup"><span data-stu-id="839bb-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="839bb-197">Uyarlamalı örnekleme ItemCount toobe uygulamanızı ağırlıklı olarak ne zaman kullanıldığını dönemlerde yüksek neden olur.</span><span class="sxs-lookup"><span data-stu-id="839bb-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="839bb-198">ItemCount birleşimi, bu nedenle hello özgün olay sayısı için iyi bir gösterge sağlar.</span><span class="sxs-lookup"><span data-stu-id="839bb-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="839bb-199">Ayrıca bir `count()` toplama (ve sayısı işlemi) durumlarda gerçekten istediğiniz toocount hello bir grup satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="839bb-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="839bb-200">Bir dizi var. [toplama işlevleri](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="839bb-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="839bb-201">Grafik hello sonuçları</span><span class="sxs-lookup"><span data-stu-id="839bb-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="839bb-202">Varsayılan olarak bir tablo olarak sonuçları görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="839bb-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="839bb-203">Merhaba Tablo görünümü daha iyi yapabileceğimiz.</span><span class="sxs-lookup"><span data-stu-id="839bb-203">We can do better than hello table view.</span></span> <span data-ttu-id="839bb-204">Merhaba Grafik görünümünde hello sonuçlarını hello dikey çubuk seçeneğiyle bakalım:</span><span class="sxs-lookup"><span data-stu-id="839bb-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Grafiği tıklatın ardından dikey çubuk grafiği seçin ve ata x ve y eksenleri](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="839bb-206">Ancak dikkat edin (Merhaba Tablo görünümünde görebileceğiniz gibi) zamanına göre hello sonuçları biz sıralamak alamadık, hello grafik görüntüleme her zaman doğru sırayla tarih/saat gösterilir.</span><span class="sxs-lookup"><span data-stu-id="839bb-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="839bb-207">Timecharts</span><span class="sxs-lookup"><span data-stu-id="839bb-207">Timecharts</span></span>
<span data-ttu-id="839bb-208">Kaç tane var. her saat olaylardır göster:</span><span class="sxs-lookup"><span data-stu-id="839bb-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="839bb-209">Merhaba grafik görüntüleme seçeneği belirleyin:</span><span class="sxs-lookup"><span data-stu-id="839bb-209">Select hello Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="839bb-211">Birden fazla seri</span><span class="sxs-lookup"><span data-stu-id="839bb-211">Multiple series</span></span>
<span data-ttu-id="839bb-212">Birden çok ifadelerinde hello `summarize` yan tümcesi birden çok sütun oluşturur.</span><span class="sxs-lookup"><span data-stu-id="839bb-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="839bb-213">Birden çok ifadelerinde hello `by` yan tümcesi her değer birleşimlerinde birden çok satır oluşturur.</span><span class="sxs-lookup"><span data-stu-id="839bb-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Saat ve konuma göre istekleri tablosu](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="839bb-215">Bir grafik boyutlara göre bölme</span><span class="sxs-lookup"><span data-stu-id="839bb-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="839bb-216">Bir dize sütunu ve hello dize sayısal bir sütun içeren bir tablo grafik kullanılan toosplit hello sayısal veri noktalarını ayrı bir dizi olabiliyorsa.</span><span class="sxs-lookup"><span data-stu-id="839bb-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="839bb-217">Birden çok dize sütunu ise, hangi sütunun toouse hello ayrıştırıcı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="839bb-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Bir analiz grafik segment](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="839bb-219">Oranı sıçrama</span><span class="sxs-lookup"><span data-stu-id="839bb-219">Bounce rate</span></span>

<span data-ttu-id="839bb-220">Boolean tooa dize toouse Dönüştür bir Ayrıştırıcıyı olarak:</span><span class="sxs-lookup"><span data-stu-id="839bb-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="839bb-221">Birden çok ölçümleri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="839bb-221">Display multiple metrics</span></span>
<span data-ttu-id="839bb-222">Birden fazla sayısal sütun eklenmesi toohello zaman damgasına sahip bir tablo grafik herhangi bir bileşimini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="839bb-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Bir analiz grafik segment](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="839bb-224">Seçmelisiniz **yok bölünmüş** birden çok sayısal sütunlar seçebilmeniz için önce.</span><span class="sxs-lookup"><span data-stu-id="839bb-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="839bb-225">Bir dize sütunu hello tarafından aynı bölünemez birden fazla sayısal sütun görüntüleme olarak zaman.</span><span class="sxs-lookup"><span data-stu-id="839bb-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="839bb-226">Günlük ortalama döngüsü</span><span class="sxs-lookup"><span data-stu-id="839bb-226">Daily average cycle</span></span>
<span data-ttu-id="839bb-227">Kullanım ortalama bir günün hello nasıl değişiyor?</span><span class="sxs-lookup"><span data-stu-id="839bb-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="839bb-228">Saate binned sayısı istekler, bir gün modulo hello zamana göre:</span><span class="sxs-lookup"><span data-stu-id="839bb-228">Count requests by hello time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Saat cinsinden ortalama bir günün çizgi grafiği](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="839bb-230">Biz şu anda tooconvert zaman süreleri toodatetimes sipariş toodisplay üzerinde bir çizgi grafiği özen gösterin.</span><span class="sxs-lookup"><span data-stu-id="839bb-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="839bb-231">Birden fazla günlük seri Karşılaştır</span><span class="sxs-lookup"><span data-stu-id="839bb-231">Compare multiple daily series</span></span>
<span data-ttu-id="839bb-232">Nasıl kullanım günü hello zaman içinde farklı ülkelerde değişiyor mu?</span><span class="sxs-lookup"><span data-stu-id="839bb-232">How does usage vary over hello time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Bölünmüş tarafından client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="839bb-234">Bir dağıtım Çiz</span><span class="sxs-lookup"><span data-stu-id="839bb-234">Plot a distribution</span></span>
<span data-ttu-id="839bb-235">Kaç tane oturumları vardır, farklı uzunlukta?</span><span class="sxs-lookup"><span data-stu-id="839bb-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="839bb-236">Merhaba son gerekli tooconvert toodatetime satırdır.</span><span class="sxs-lookup"><span data-stu-id="839bb-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="839bb-237">Şu anda yalnızca bir datetime ise bir grafiğin hello x ekseninin skaler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="839bb-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="839bb-238">Merhaba `where` yan tümcesi dışlar tek adımda oturumları (sessionDuration == 0) ve ayarlar hello hello x ekseni uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="839bb-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="839bb-239">Yüzdebirlik değeri</span><span class="sxs-lookup"><span data-stu-id="839bb-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="839bb-240">Hangi süreleri aralıklarına oturumları farklı yüzdelerini kapak?</span><span class="sxs-lookup"><span data-stu-id="839bb-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="839bb-241">Sorgu yukarıda Hello kullanır, ancak hello son satırı değiştirin:</span><span class="sxs-lookup"><span data-stu-id="839bb-241">Use hello above query, but replace hello last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="839bb-242">Biz de hello üst sınırı burada tümcesinde sipariş tooget düzeltmek birden fazla isteği ile tüm oturumları dahil olmak üzere rakamları hello kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="839bb-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![Sonuç](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="839bb-244">İçinden biz görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="839bb-244">From which we can see that:</span></span>

* <span data-ttu-id="839bb-245">%5 oturumlarının 3 dakikadan 34s daha kısa bir süre; yine de sahip istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="839bb-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="839bb-246">Son 36 dakikadan az %50 oturumlarının;</span><span class="sxs-lookup"><span data-stu-id="839bb-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="839bb-247">7 günden fazla %5 oturumlarının son</span><span class="sxs-lookup"><span data-stu-id="839bb-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="839bb-248">tooget her ülke için ayrı bir çözümleme, biz yalnızca toobring hello client_CountryOrRegion sütunu işleçleri özetlemek ayrı ayrı her ikisi de aracılığıyla vardır:</span><span class="sxs-lookup"><span data-stu-id="839bb-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="839bb-249">Birleştir</span><span class="sxs-lookup"><span data-stu-id="839bb-249">Join</span></span>
<span data-ttu-id="839bb-250">Erişim tooseveral tabloları, istekler ve özel durumlar dahil olmak üzere sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="839bb-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="839bb-251">hata yanıtını döndürülen toofind hello özel durumlar ilgili tooa isteği, biz katılmayı hello tabloları `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="839bb-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="839bb-252">İyi bir uygulama toouse olan `project` ihtiyacımız gerçekleştirmeden önce tooselect yalnızca hello sütunları hello birleştirme.</span><span class="sxs-lookup"><span data-stu-id="839bb-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="839bb-253">Merhaba, aynı yan tümceleri, biz hello zaman damgası sütunu yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="839bb-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="839bb-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): sonuç tooa değişkeni atayın</span><span class="sxs-lookup"><span data-stu-id="839bb-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="839bb-255">Kullanım `let` tooseparate hello önceki ifade hello bölümlerini çıkışı.</span><span class="sxs-lookup"><span data-stu-id="839bb-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="839bb-256">Merhaba sonuçları aynıdır:</span><span class="sxs-lookup"><span data-stu-id="839bb-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="839bb-257">Merhaba Analytics istemcisinde hello hello sorgunun bölümlerini arasında boş satırlar koymayın.</span><span class="sxs-lookup"><span data-stu-id="839bb-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="839bb-258">Emin tooexecute tamamını yapın.</span><span class="sxs-lookup"><span data-stu-id="839bb-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="839bb-259">Kullanım `toscalar` tooconvert tek tablo hücre tooa değeri:</span><span class="sxs-lookup"><span data-stu-id="839bb-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="839bb-260">İşlevler</span><span class="sxs-lookup"><span data-stu-id="839bb-260">Functions</span></span>

<span data-ttu-id="839bb-261">Kullanım *izin* toodefine bir işlev:</span><span class="sxs-lookup"><span data-stu-id="839bb-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="839bb-262">İç içe geçmiş nesnelere erişme</span><span class="sxs-lookup"><span data-stu-id="839bb-262">Accessing nested objects</span></span>
<span data-ttu-id="839bb-263">İç içe geçmiş nesnelerde kolayca erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="839bb-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="839bb-264">Örneğin, hello özel durumlar akışında yapılandırılmış nesneleri bu gibi görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="839bb-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![Sonuç](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="839bb-266">İlgilendiğiniz hello özellikleri seçerek düzleştirmek:</span><span class="sxs-lookup"><span data-stu-id="839bb-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="839bb-267">Toocast hello sonuç toohello uygun türü gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="839bb-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="839bb-268">Özel özellikler ve ölçümler</span><span class="sxs-lookup"><span data-stu-id="839bb-268">Custom properties and measurements</span></span>
<span data-ttu-id="839bb-269">Uygulamanızı bağlanıyorsa [özel boyutları (Özellikler) ve özel ölçümleri](app-insights-api-custom-events-metrics.md#properties) tooevents, ardından görürsünüz: bunları hello `customDimensions` ve `customMeasurements` nesneleri.</span><span class="sxs-lookup"><span data-stu-id="839bb-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="839bb-270">Örneğin, uygulamanızın içeriyorsa:</span><span class="sxs-lookup"><span data-stu-id="839bb-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="839bb-271">tooextract Analytics bu değerleri:</span><span class="sxs-lookup"><span data-stu-id="839bb-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="839bb-272">tooverify Özel boyut belirli bir tür olup:</span><span class="sxs-lookup"><span data-stu-id="839bb-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="839bb-273">Panolar</span><span class="sxs-lookup"><span data-stu-id="839bb-273">Dashboards</span></span>
<span data-ttu-id="839bb-274">Sonuçları tooa Panonuzda sipariş toobring birlikte, en önemli grafikler ve tablolar sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="839bb-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="839bb-275">[Azure paylaşılan Pano](app-insights-dashboards.md#share-dashboards): hello PIN simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="839bb-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="839bb-276">Bunu, bir paylaşılan Pano sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="839bb-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="839bb-277">Hello Azure portal, açın veya bir pano oluşturun ve Paylaşım'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="839bb-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="839bb-278">[Power BI panosuna](app-insights-export-power-bi.md): tıklatın verme, Power BI sorgu.</span><span class="sxs-lookup"><span data-stu-id="839bb-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="839bb-279">Bu alternatif bir avantajı, çok çeşitli diğer sonuçlarından kaynakları yanında sorgunuzu görüntüleyebilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="839bb-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="839bb-280">İçeri aktarılan verilerle birleştirin</span><span class="sxs-lookup"><span data-stu-id="839bb-280">Combine with imported data</span></span>

<span data-ttu-id="839bb-281">Analytics Raporları hello Panoda harika bakın, ancak bazen daha fazla digestible form tootranslate hello veri tooa istiyor.</span><span class="sxs-lookup"><span data-stu-id="839bb-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="839bb-282">Örneğin, bir diğer ad tarafından tanımlanan, kimliği doğrulanmış kullanıcılar hello telemetri varsayalım.</span><span class="sxs-lookup"><span data-stu-id="839bb-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="839bb-283">Sonuç olarak, gerçek adlarını tooshow ister.</span><span class="sxs-lookup"><span data-stu-id="839bb-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="839bb-284">toodo bunu hello diğer adlar toohello gerçek adlarını eşleyen bir CSV dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="839bb-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="839bb-285">Bir veri dosyasını içeri aktarın ve gibi hello standart tablolardan (istekleri, özel durumlar ve benzeri) herhangi birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="839bb-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="839bb-286">Bu, kendi sorgulamak ya da diğer tablolarla katılın.</span><span class="sxs-lookup"><span data-stu-id="839bb-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="839bb-287">Örneğin, usermap adlı bir tablo varsa ve sütunları içeren `realName` ve `userId`, tootranslate hello kullanmayı `user_AuthenticatedId` hello isteği telemetri alanındaki:</span><span class="sxs-lookup"><span data-stu-id="839bb-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="839bb-288">tooimport hello şema dikey penceresinde, bir tablo altında **diğer veri kaynakları**, örnek verileriniz yükleyerek hello yönergeleri tooadd yeni bir veri kaynağı izleyin.</span><span class="sxs-lookup"><span data-stu-id="839bb-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="839bb-289">Ardından bu tanımı tooupload tabloları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="839bb-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="839bb-290">"Diğer veri kaynakları." altında "bize başvurun" Bağlantı başlangıçta göreceğiniz şekilde hello içe aktar özelliği şu anda önizlemede, değil</span><span class="sxs-lookup"><span data-stu-id="839bb-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="839bb-291">Merhaba bağlantı sonra bir "yeni veri kaynağı Ekle" düğmesi tarafından değiştirilir ve bu toosign toohello Önizleme programı kullanın.</span><span class="sxs-lookup"><span data-stu-id="839bb-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="839bb-292">Tablolar</span><span class="sxs-lookup"><span data-stu-id="839bb-292">Tables</span></span>
<span data-ttu-id="839bb-293">Merhaba, uygulamanızdan alınan telemetri çeşitli tablolara erişilebilir akışıdır.</span><span class="sxs-lookup"><span data-stu-id="839bb-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="839bb-294">Her tablo için kullanılabilen özellikleri Hello şeması hello penceresinde hello sol tarafında görünür olur.</span><span class="sxs-lookup"><span data-stu-id="839bb-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="839bb-295">İstekler tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-295">Requests table</span></span>
<span data-ttu-id="839bb-296">Count HTTP istekleri tooyour web app ve kesim tarafından sayfa adı:</span><span class="sxs-lookup"><span data-stu-id="839bb-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Ada göre kesimli sayısı istekleri](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="839bb-298">Çoğu başarısız hello istekleri Bul:</span><span class="sxs-lookup"><span data-stu-id="839bb-298">Find hello requests that fail most:</span></span>

![Ada göre kesimli sayısı istekleri](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="839bb-300">Özel olaylar tablo</span><span class="sxs-lookup"><span data-stu-id="839bb-300">Custom events table</span></span>
<span data-ttu-id="839bb-301">Kullanırsanız [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend kendi olayları bu tablodan okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="839bb-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="839bb-302">Bu satırlar, uygulama kodunuzun içerdiği bir örnek atalım:</span><span class="sxs-lookup"><span data-stu-id="839bb-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="839bb-303">Bu olaylar Hello sıklığını görüntüle:</span><span class="sxs-lookup"><span data-stu-id="839bb-303">Display hello frequency of these events:</span></span>

![Özel olaylar görüntü oranı](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="839bb-305">Ölçüleri ve boyutları hello olaylarından ayıklayın:</span><span class="sxs-lookup"><span data-stu-id="839bb-305">Extract measurements and dimensions from hello events:</span></span>

![Özel olaylar görüntü oranı](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="839bb-307">Özel ölçümleri tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-307">Custom metrics table</span></span>
<span data-ttu-id="839bb-308">Kullanıyorsanız [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend ölçüm kendi değerlerinizi hello sonuçlarını bulacaksınız **customMetrics** akış.</span><span class="sxs-lookup"><span data-stu-id="839bb-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="839bb-309">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="839bb-309">For example:</span></span>  

![Application Insights analytics'te özel ölçümleri](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="839bb-311">İçinde [ölçüm Gezgini](app-insights-metrics-explorer.md), ekli tooany türüne telemetri görünür birlikte hello ölçümleri dikey kullanılarak gönderilen ölçümleri yanı sıra tüm özel ölçümleri `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="839bb-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="839bb-312">Ancak, analizleri özel ölçümleri hala bunlar taşınan - olayları veya istekleri vb. - TrackMetric tarafından gönderilen ölçümleri kendi akışında görünürken telemetri toowhichever türü bağlı.</span><span class="sxs-lookup"><span data-stu-id="839bb-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="839bb-313">Performans sayaçları tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-313">Performance counters table</span></span>
<span data-ttu-id="839bb-314">[Performans sayaçları](app-insights-performance-counters.md) ve ağ kullanımı gibi CPU, bellek, uygulamanız için temel sistem ölçümleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="839bb-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="839bb-315">Kendi özel sayaçlar dahil hello SDK toosend ek sayaçları, yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="839bb-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="839bb-316">Merhaba **performanceCounters** şeması sunan hello `category`, `counter` adı ve `instance` her performans sayacı adı.</span><span class="sxs-lookup"><span data-stu-id="839bb-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="839bb-317">Sayaç örneği adları yalnızca geçerli toosome performans sayaçları ve genellikle hello işlem toowhich hello sayısı hello adını ilişkili gösterir.</span><span class="sxs-lookup"><span data-stu-id="839bb-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="839bb-318">Telemetri Hello her uygulama için yalnızca bu uygulama için hello sayaçları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="839bb-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="839bb-319">Örneğin, toosee hangi sayaçları kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="839bb-319">For example, toosee what counters are available:</span></span>

![Application Insights analytics performans sayaçları](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="839bb-321">Seçilen dönemi tooget hello üzerinden kullanılabilir belleğin bir grafik:</span><span class="sxs-lookup"><span data-stu-id="839bb-321">tooget a chart of available memory over hello selected period:</span></span>

![Application Insights analytics'te bellek timechart](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="839bb-323">Gibi diğer telemetri **performanceCounters** de bir sütuna sahip `cloud_RoleInstance` hello uygulamanızı çalıştıran hello ana bilgisayar makine kimliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="839bb-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="839bb-324">Örneğin, toocompare hello uygulamanızın performansı ile Merhaba farklı makinelerde:</span><span class="sxs-lookup"><span data-stu-id="839bb-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Performans rol örneğinde Application Insights tarafından analiz bölümlenmiş.](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="839bb-326">Özel durumlar tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-326">Exceptions table</span></span>
<span data-ttu-id="839bb-327">[Özel durumlar, uygulamanız tarafından bildirilen](app-insights-asp-net-exceptions.md) bu tabloda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="839bb-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="839bb-328">toofind hello özel durumu oluştu, uygulamanızın işleme HTTP isteği Merhaba, üzerinde operation_Id Katıl:</span><span class="sxs-lookup"><span data-stu-id="839bb-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Özel durumlar isteklerle operation_Id üzerinde katılma](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="839bb-330">Tarayıcı zamanlamaları tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-330">Browser timings table</span></span>
<span data-ttu-id="839bb-331">`browserTimings`Kullanıcılarınızın tarayıcılarda toplanan sayfa yükleme verileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="839bb-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="839bb-332">[İstemci tarafı telemetri için uygulamanızı ayarlayın](app-insights-javascript.md) içinde bu ölçümleri toosee sipariş.</span><span class="sxs-lookup"><span data-stu-id="839bb-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="839bb-333">Merhaba şeması içerir [hello uzunlukları hello sayfa yükleme işlemi farklı aşaması gösteren ölçümleri](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="839bb-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="839bb-334">(Bunlar hello süreyi kullanıcılarınızın bir sayfa okuma göstermediği.)</span><span class="sxs-lookup"><span data-stu-id="839bb-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="839bb-335">Merhaba popularities farklı sayfaların göstermek ve her bir sayfa için zamanları yük:</span><span class="sxs-lookup"><span data-stu-id="839bb-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Sayfa yükleme sürelerinin analytics'te](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="839bb-337">Kullanılabilirlik sonuçları tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-337">Availability results table</span></span>
<span data-ttu-id="839bb-338">`availabilityResults`Merhaba sonuçlarını gösterir, [web testleri](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="839bb-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="839bb-339">Her çalışma testlerinizin her test konumdan ayrı olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="839bb-339">Each run of your tests from each test location is reported separately.</span></span>

![Sayfa yükleme sürelerinin analytics'te](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="839bb-341">Bağımlılıklar tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-341">Dependencies table</span></span>
<span data-ttu-id="839bb-342">Arama sonuçlarını içeren uygulamanızı toodatabases ve REST API'leri ve diğer yapar tooTrackDependency() çağırır.</span><span class="sxs-lookup"><span data-stu-id="839bb-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="839bb-343">Ayrıca hello tarayıcıdan oluşturulan AJAX çağrıları içerir.</span><span class="sxs-lookup"><span data-stu-id="839bb-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="839bb-344">AJAX çağrıları hello tarayıcısından:</span><span class="sxs-lookup"><span data-stu-id="839bb-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="839bb-345">Bağımlılık çağrıları hello sunucusundan:</span><span class="sxs-lookup"><span data-stu-id="839bb-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="839bb-346">Sunucu tarafı bağımlılık sonuçları her zaman göster `success==False` Merhaba, Application Insights aracısı yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="839bb-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="839bb-347">Ancak, hello diğer verileri doğru değildir.</span><span class="sxs-lookup"><span data-stu-id="839bb-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="839bb-348">İzlemeler tablosu</span><span class="sxs-lookup"><span data-stu-id="839bb-348">Traces table</span></span>
<span data-ttu-id="839bb-349">Merhaba telemetri TrackTrace(), kullanma, uygulamanız tarafından gönderilen içerir veya [başka günlük altyapılarına](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="839bb-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="839bb-350">Video</span><span class="sxs-lookup"><span data-stu-id="839bb-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="839bb-351">Gelişmiş sorgular:</span><span class="sxs-lookup"><span data-stu-id="839bb-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="839bb-352">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="839bb-352">Next steps</span></span>
* [<span data-ttu-id="839bb-353">Analytics dil başvurusu</span><span class="sxs-lookup"><span data-stu-id="839bb-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="839bb-354">[SQL-kullanıcıların kopya sayfası](https://aka.ms/sql-analytics) hello en yaygın deyimleri çevirir.</span><span class="sxs-lookup"><span data-stu-id="839bb-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
