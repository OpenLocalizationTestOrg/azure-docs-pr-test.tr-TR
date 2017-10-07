---
title: aaaHow yedeklerim... Azure Application Insights'ta | Microsoft Docs
description: "Application ınsights'ta SSS."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="02131-103">Application Insights’ta nasıl ... yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="02131-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="02131-104">Bir e-posta almak zaman...</span><span class="sxs-lookup"><span data-stu-id="02131-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="02131-105">Sitem devre dışı kalırsa e-posta</span><span class="sxs-lookup"><span data-stu-id="02131-105">Email if my site goes down</span></span>
<span data-ttu-id="02131-106">Ayarlanmış bir [kullanılabilirlik web testi](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="02131-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="02131-107">Sitem aşırı yüklüyse e-posta</span><span class="sxs-lookup"><span data-stu-id="02131-107">Email if my site is overloaded</span></span>
<span data-ttu-id="02131-108">Ayarlanmış bir [uyarı](app-insights-alerts.md) üzerinde **sunucu yanıt süresi**.</span><span class="sxs-lookup"><span data-stu-id="02131-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="02131-109">1 ve 2 saniye arasında bir eşik çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="02131-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="02131-110">Uygulamanızı hata kodları döndürme yükü belirtileri da gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="02131-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="02131-111">Bir uyarı ayarlamak **başarısız istekler**.</span><span class="sxs-lookup"><span data-stu-id="02131-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="02131-112">Tooset bir uyarı istiyorsanız **sunucu özel durumları**, toodo olabilir [bazı ek kurulum](app-insights-asp-net-exceptions.md) sipariş toosee veri.</span><span class="sxs-lookup"><span data-stu-id="02131-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="02131-113">Özel durumları e-posta</span><span class="sxs-lookup"><span data-stu-id="02131-113">Email on exceptions</span></span>
1. [<span data-ttu-id="02131-114">Özel durum izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="02131-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="02131-115">[Bir uyarı ayarlamak](app-insights-alerts.md) ölçüm hello üzerinde özel durum sayısı</span><span class="sxs-lookup"><span data-stu-id="02131-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="02131-116">Uygulamam olayda e-posta</span><span class="sxs-lookup"><span data-stu-id="02131-116">Email on an event in my app</span></span>
<span data-ttu-id="02131-117">Şimdi belirli bir olay gerçekleştiğinde tooget bir e-posta istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="02131-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="02131-118">Application Insights sunmaz bu tesis doğrudan, ancak bunu [bir eşik ölçüm kestiği olduğunda bir uyarı gönder](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="02131-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="02131-119">Uyarılar, üzerinde ayarlanabilir [özel ölçümleri](app-insights-api-custom-events-metrics.md#trackmetric)olmayan özel olaylar ancak.</span><span class="sxs-lookup"><span data-stu-id="02131-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="02131-120">Merhaba olay gerçekleştiğinde bazı kod tooincrease ölçüm yazma:</span><span class="sxs-lookup"><span data-stu-id="02131-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="02131-121">Ya da:</span><span class="sxs-lookup"><span data-stu-id="02131-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="02131-122">İki durumlu uyarıları sahip olduğundan, toohave sona erdi hello uyarı göz önüne aldığınızda düşük bir değere toosend vardır:</span><span class="sxs-lookup"><span data-stu-id="02131-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="02131-123">Grafik oluşturma [ölçüm Gezgini](app-insights-metrics-explorer.md) toosee, uyarısı:</span><span class="sxs-lookup"><span data-stu-id="02131-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="02131-124">Şimdi Hello ölçüm kısa bir süre için orta değer geçtiğinde bir uyarı toofire ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="02131-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="02131-125">Dönem toohello minimum ortalaması hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="02131-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="02131-126">E-postaları hello ölçüm yukarıda gittiğinde hem hello eşiğin altına elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="02131-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="02131-127">Bazı noktaları tooconsider:</span><span class="sxs-lookup"><span data-stu-id="02131-127">Some points tooconsider:</span></span>

* <span data-ttu-id="02131-128">Bir uyarı iki durumlu ("uyarı" ve "sağlıklı") sahiptir.</span><span class="sxs-lookup"><span data-stu-id="02131-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="02131-129">yalnızca bir ölçü alındığında hello durumu değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="02131-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="02131-130">Yalnızca hello durumu değiştiğinde bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="02131-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="02131-131">Toosend sahip olmanızın nedeni budur yüksek ve düşük değer ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="02131-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="02131-132">tooevaluate hello uyarı, hello ortalama süre önceki hello alınan hello değerlerini alınır.</span><span class="sxs-lookup"><span data-stu-id="02131-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="02131-133">Ölçüm alınan her zaman, e-postaları ayarladığınız hello süresinden daha sık gönderilmesini şekilde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="02131-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="02131-134">Hem "uyarı" ve "sağlıklı" e-postaları gönderilen olduğundan, tek adımda olayınızın iki durumlu koşul olarak yeniden düşünüyorum tooconsider isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02131-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="02131-135">Örneğin, "işi tamamlandı" olay yerine hello başlangıç ve bitiş bir işin e-postaları nereden bir "devam eden işi" koşula sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="02131-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="02131-136">Uyarıları otomatik olarak ayarla</span><span class="sxs-lookup"><span data-stu-id="02131-136">Set up alerts automatically</span></span>
[<span data-ttu-id="02131-137">PowerShell toocreate yeni uyarıları kullanın</span><span class="sxs-lookup"><span data-stu-id="02131-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="02131-138">PowerShell tooManage Application Insights kullanın</span><span class="sxs-lookup"><span data-stu-id="02131-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="02131-139">Yeni kaynaklar oluşturma</span><span class="sxs-lookup"><span data-stu-id="02131-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="02131-140">Yeni uyarılar oluştur</span><span class="sxs-lookup"><span data-stu-id="02131-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="02131-141">Farklı sürümlerdeki ayrı telemetri</span><span class="sxs-lookup"><span data-stu-id="02131-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="02131-142">Bir uygulama içinde birden çok rol: tek bir Application Insights kaynağı kullanın ve filtre cloud_Rolename üzerinde.</span><span class="sxs-lookup"><span data-stu-id="02131-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="02131-143">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="02131-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="02131-144">Geliştirme, test ve yayın sürümleri ayırma: farklı Application Insights kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="02131-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="02131-145">Web.config hello araçları anahtarları seçin. [Daha fazla bilgi](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="02131-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="02131-146">Sürümleri derleme raporlama: telemetri Başlatıcı kullanarak özellik ekleme.</span><span class="sxs-lookup"><span data-stu-id="02131-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="02131-147">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="02131-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="02131-148">Arka uç sunucularının ve Masaüstü uygulamaları izleme</span><span class="sxs-lookup"><span data-stu-id="02131-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="02131-149">[Kullanım hello Windows Server SDK Modülü](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="02131-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="02131-150">Verileri görselleştirin</span><span class="sxs-lookup"><span data-stu-id="02131-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="02131-151">Birden çok uygulamalardan ölçümlerle Panosu</span><span class="sxs-lookup"><span data-stu-id="02131-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="02131-152">İçinde [ölçüm Gezgini](app-insights-metrics-explorer.md), grafiğinizi özelleştirmek ve sık kullanılan olarak Kaydet.</span><span class="sxs-lookup"><span data-stu-id="02131-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="02131-153">Toohello Azure Pano sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="02131-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="02131-154">Diğer kaynaklardan ve Application Insights verilerle Panosu</span><span class="sxs-lookup"><span data-stu-id="02131-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="02131-155">[Telemetri tooPower BI verme](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="02131-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="02131-156">Veya</span><span class="sxs-lookup"><span data-stu-id="02131-156">Or</span></span>

* <span data-ttu-id="02131-157">SharePoint web bölümleri verileri görüntüleme panonuz olarak SharePoint kullanın.</span><span class="sxs-lookup"><span data-stu-id="02131-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="02131-158">[Sürekli dışarı aktarma ve akış analizi tooexport tooSQL kullanmak](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="02131-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="02131-159">PowerView tooexamine hello veritabanını kullanın ve bir SharePoint web bölümü için PowerView oluşturun.</span><span class="sxs-lookup"><span data-stu-id="02131-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="02131-160">Anonim veya kimliği doğrulanmış kullanıcıları Filtrele</span><span class="sxs-lookup"><span data-stu-id="02131-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="02131-161">Kullanıcılarınız oturum açarsa, hello ayarlayabilirsiniz [kullanıcı kimliği kimlik doğrulaması](app-insights-api-custom-events-metrics.md#authenticated-users). (Bunu otomatik olarak gerçekleşmez.)</span><span class="sxs-lookup"><span data-stu-id="02131-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="02131-162">Sonra şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="02131-162">You can then:</span></span>

* <span data-ttu-id="02131-163">Belirli bir kullanıcı kimliklerine göre ara</span><span class="sxs-lookup"><span data-stu-id="02131-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="02131-164">Ölçümleri tooeither anonim veya kimliği doğrulanmış kullanıcıları Filtrele</span><span class="sxs-lookup"><span data-stu-id="02131-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="02131-165">Özellik adlarını ve değerleri değiştirme</span><span class="sxs-lookup"><span data-stu-id="02131-165">Modify property names or values</span></span>
<span data-ttu-id="02131-166">Oluşturma bir [filtre](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="02131-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="02131-167">Bu, değiştirmek veya uygulama tooApplication Öngörüler gönderilmeden önce telemetri filtre sağlar.</span><span class="sxs-lookup"><span data-stu-id="02131-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="02131-168">Liste belirli kullanıcılar ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="02131-168">List specific users and their usage</span></span>
<span data-ttu-id="02131-169">Yalnızca çok istiyorsanız[belirli kullanıcılar için arama](#search-specific-users), hello ayarlayabilirsiniz [kullanıcı kimliği kimlik doğrulaması](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="02131-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="02131-170">Hangi sayfaların gibi verileri sahip kullanıcıların listesini istiyorsanız, bunlar bakmak veya ne sıklıkta oturum, iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="02131-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="02131-171">[Kümesi kimliği doğrulanmış kullanıcı kimliği](app-insights-api-custom-events-metrics.md#authenticated-users), [tooa veritabanı dışarı](app-insights-code-sample-export-sql-stream-analytics.md) ve araçları tooanalyze kullanın uygun kullanıcı verilerinizi vardır.</span><span class="sxs-lookup"><span data-stu-id="02131-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="02131-172">Az sayıda kullanıcılar varsa, özel olaylar veya ölçümleri, ölçüm değeri veya olay adı ve ayarı hello kullanıcı kimliği özelliği olarak hello gibi hello verileri kullanarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="02131-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="02131-173">tooanalyze sayfa görünümleri hello standart JavaScript trackPageView çağrısı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="02131-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="02131-174">tooanalyze sunucu tarafı telemetri, bir telemetri Başlatıcı tooadd hello kullanıcı kimliği tooall sunucu telemetri kullanın.</span><span class="sxs-lookup"><span data-stu-id="02131-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="02131-175">Bundan sonra filtre ve segment ölçümleri ve hello kullanıcı kimliği arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02131-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="02131-176">My uygulama tooApplication Öngörüler trafiğini azaltır</span><span class="sxs-lookup"><span data-stu-id="02131-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="02131-177">İçinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), gerek yoktur, herhangi bir modül gibi hello performans sayacı Toplayıcı devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="02131-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="02131-178">Kullanım [örnekleme ve filtre](app-insights-api-filtering-sampling.md) hello SDK adresindeki.</span><span class="sxs-lookup"><span data-stu-id="02131-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="02131-179">Web sayfalarınızda Ajax çağrıları her sayfa görünümü için bildirilen hello sayısını sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="02131-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="02131-180">Sonra hello kod parçacığında bulunan `instrumentationKey:...` , Ekle: `,maxAjaxCallsPerView:3` (veya uygun rakam).</span><span class="sxs-lookup"><span data-stu-id="02131-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="02131-181">Kullanıyorsanız, [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), ölçüm değerleri toplu hello toplamını hello sonuç göndermeden önce işlem.</span><span class="sxs-lookup"><span data-stu-id="02131-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="02131-182">Bir aşırı yüklemesini için sağlayan TrackMetric() yoktur.</span><span class="sxs-lookup"><span data-stu-id="02131-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="02131-183">Daha fazla bilgi edinmek [fiyatlandırma ve kotaları](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="02131-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="02131-184">Telemetri devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="02131-184">Disable telemetry</span></span>
<span data-ttu-id="02131-185">çok**dinamik olarak durdurmak ve başlatmak** hello toplama ve hello sunucusundan telemetri iletimini:</span><span class="sxs-lookup"><span data-stu-id="02131-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="02131-186">çok**seçili standart toplayıcıları devre dışı** - örnek, performans sayaçları, HTTP isteklerini veya bağımlılıkları - silin veya açıklama hello ilgili satırlarında çıkışı [Applicationınsights.config](app-insights-api-custom-events-metrics.md). Örneğin, kendi TrackRequest veri toosend istiyorsanız bunu.</span><span class="sxs-lookup"><span data-stu-id="02131-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="02131-187">Görünüm sistem performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="02131-187">View system performance counters</span></span>
<span data-ttu-id="02131-188">Merhaba arasında ölçümleri Gezgini'nde Göster ölçümleri sistem performans sayaçları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="02131-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="02131-189">Başlıklı önceden tanımlanmış bir dikey pencere yok **sunucuları** birkaç görüntüler.</span><span class="sxs-lookup"><span data-stu-id="02131-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Application Insights kaynağınıza açın ve sunucuları'nı tıklatın](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="02131-191">Hiçbir performans sayacı verilerini görürseniz</span><span class="sxs-lookup"><span data-stu-id="02131-191">If you see no performance counter data</span></span>
* <span data-ttu-id="02131-192">**IIS server** kendi makine veya bir VM üzerinde.</span><span class="sxs-lookup"><span data-stu-id="02131-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="02131-193">[Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="02131-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="02131-194">**Azure web sitesi** -performans sayaçları henüz desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="02131-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="02131-195">Hello Azure web sitesi Denetim Masası standart bir parçası olarak alabilirsiniz çeşitli ölçümleri vardır.</span><span class="sxs-lookup"><span data-stu-id="02131-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="02131-196">**UNIX sunucusu** - [collectd yükleyin](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="02131-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="02131-197">toodisplay daha fazla performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="02131-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="02131-198">İlk olarak, [yeni bir grafik ekleyin](app-insights-metrics-explorer.md) ve hello sayaç hello temel, sunduğumuz ayarlanmış olup olmadığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02131-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="02131-199">Aksi durumda, [eklemek hello performans sayacı modülü tarafından toplanan hello sayaç toohello kümesi](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="02131-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
