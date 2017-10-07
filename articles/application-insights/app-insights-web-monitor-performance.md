---
title: "aaaMonitor uygulamanızın sistem durumu ve Application Insights ile kullanım"
description: "Application Insights ile çalışmaya başlayın. Kullanım, kullanılabilirlik ve şirket içi veya Microsoft Azure uygulamalarının performansını analiz edin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 40650472-e860-4c1b-a589-9956245df307
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/25/2015
ms.author: bwren
ms.openlocfilehash: 9230a6e65e5afb00c36122ff1d1de01ba19cd7f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-in-web-applications"></a><span data-ttu-id="65474-104">Web uygulamalarının performansını izleme</span><span class="sxs-lookup"><span data-stu-id="65474-104">Monitor performance in web applications</span></span>


<span data-ttu-id="65474-105">Uygulamanızın düzgün çalışıp emin olun ve hatalar hakkında hızlı bir şekilde öğrenin.</span><span class="sxs-lookup"><span data-stu-id="65474-105">Make sure your application is performing well, and find out quickly about any failures.</span></span> <span data-ttu-id="65474-106">[Application Insights] [ start] herhangi bir performans sorunlarını ve özel durumlar hakkında söyleyin ve bulmak ve hello tanılamanıza yardımcı kök neden olur.</span><span class="sxs-lookup"><span data-stu-id="65474-106">[Application Insights][start] will tell you about any performance issues and exceptions, and help you find and diagnose hello root causes.</span></span>

<span data-ttu-id="65474-107">Application Insights, Java ve ASP.NET web uygulamaları ve Hizmetleri, WCF hizmetleri izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-107">Application Insights can monitor both Java and ASP.NET web applications and services, WCF services.</span></span> <span data-ttu-id="65474-108">Bunlar barındırılan şirket içi, sanal makinelerde ya da Microsoft Azure Web siteleri farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="65474-108">They can be hosted on-premises, on virtual machines, or as Microsoft Azure websites.</span></span> 

<span data-ttu-id="65474-109">Merhaba istemci tarafında, Application Insights telemetri web sayfalarını ve çok çeşitli cihazlar iOS, Android ve Windows mağazası uygulamaları dahil olmak üzere alabilir.</span><span class="sxs-lookup"><span data-stu-id="65474-109">On hello client side, Application Insights can take telemetry from web pages and a wide variety of devices including iOS, Android and Windows Store apps.</span></span>

>[!Note]
> <span data-ttu-id="65474-110">Size yeni bir deneyim bulma yavaş sayfaları web uygulamanızda gerçekleştirmek için kullanılabilir yaptınız.</span><span class="sxs-lookup"><span data-stu-id="65474-110">We have made a new experience available for finding slow performing pages in your web application.</span></span> <span data-ttu-id="65474-111">Erişim tooit yoksa, Önizleme seçeneklerinizi hello ile yapılandırarak etkinleştirmek [Önizleme dikey](app-insights-previews.md).</span><span class="sxs-lookup"><span data-stu-id="65474-111">If you don't have access tooit, enable it by configuring your preview options with hello [Preview blade](app-insights-previews.md).</span></span> <span data-ttu-id="65474-112">Bu yeni deneyim okuyun [bulup hello etkileşimli performans araştırma ile performans sorunları giderin](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span><span class="sxs-lookup"><span data-stu-id="65474-112">Read about this new experience in [Find and fix performance bottlenecks with hello interactive Performance investigation](#Find-and-fix-performance-bottlenecks-with-an-interactive-Performance-investigation).</span></span>

## <span data-ttu-id="65474-113"><a name="setup"></a>Performans izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="65474-113"><a name="setup"></a>Set up performance monitoring</span></span>
<span data-ttu-id="65474-114">Application Insights tooyour henüz eklemediyseniz (diğer bir deyişle, Applicationınsights.config yoksa) projesi, şu yöntemlerden birini kullanarak seçin tooget başlatıldı:</span><span class="sxs-lookup"><span data-stu-id="65474-114">If you haven't yet added Application Insights tooyour project (that is, if it doesn't have ApplicationInsights.config), choose one of these ways tooget started:</span></span>

* [<span data-ttu-id="65474-115">ASP.NET web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="65474-115">ASP.NET web apps</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="65474-116">Özel durum izleme Ekle</span><span class="sxs-lookup"><span data-stu-id="65474-116">Add exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
  * [<span data-ttu-id="65474-117">Bağımlılık izleme Ekle</span><span class="sxs-lookup"><span data-stu-id="65474-117">Add dependency monitoring</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="65474-118">J2EE web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="65474-118">J2EE web apps</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="65474-119">Bağımlılık izleme Ekle</span><span class="sxs-lookup"><span data-stu-id="65474-119">Add dependency monitoring</span></span>](app-insights-java-agent.md)

## <span data-ttu-id="65474-120"><a name="view"></a>Performans ölçümleri keşfederken</span><span class="sxs-lookup"><span data-stu-id="65474-120"><a name="view"></a>Exploring performance metrics</span></span>
<span data-ttu-id="65474-121">İçinde [Azure portal hello](https://portal.azure.com), uygulamanız için ayarladığınız toohello Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="65474-121">In [hello Azure portal](https://portal.azure.com), browse toohello Application Insights resource that you set up for your application.</span></span> <span data-ttu-id="65474-122">Merhaba genel bakış dikey temel performans verilerini gösterir:</span><span class="sxs-lookup"><span data-stu-id="65474-122">hello overview blade shows basic performance data:</span></span>

<span data-ttu-id="65474-123">Tüm grafik toosee toosee sonuçları ve daha fazla ayrıntı için daha uzun bir süre tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65474-123">Click any chart toosee more detail, and toosee results for a longer period.</span></span> <span data-ttu-id="65474-124">Örneğin, hello istekleri kutucuğa tıklayın ve bir zaman aralığı seçin:</span><span class="sxs-lookup"><span data-stu-id="65474-124">For example, click hello Requests tile and then select a time range:</span></span>

![Toomore verilerine tıklayın ve bir zaman aralığı seçin](./media/app-insights-web-monitor-performance/appinsights-48metrics.png)

<span data-ttu-id="65474-126">Bir grafik toochoose, görüntüler, veya yeni bir grafik ekleyin ve onun ölçümleri seçin hangi ölçümleri tıklatın:</span><span class="sxs-lookup"><span data-stu-id="65474-126">Click a chart toochoose which metrics it displays, or add a new chart and select its metrics:</span></span>

![Bir grafik toochoose ölçümleri'ı tıklatın](./media/app-insights-web-monitor-performance/appinsights-61perfchoices.png)

> [!NOTE]
> <span data-ttu-id="65474-128">**Tüm hello ölçümleri işaretini** kullanılabilir toosee hello tam seçimi.</span><span class="sxs-lookup"><span data-stu-id="65474-128">**Uncheck all hello metrics** toosee hello full selection that is available.</span></span> <span data-ttu-id="65474-129">Merhaba ölçümleri gruba ayrılır; herhangi bir grubun üyesi seçildiğinde, bu yalnızca hello diğer grubun üyesi görünür.</span><span class="sxs-lookup"><span data-stu-id="65474-129">hello metrics fall into groups; when any member of a group is selected, only hello other members of that group appear.</span></span>

## <span data-ttu-id="65474-130"><a name="metrics"></a>Tüm ortalama yaptığı?</span><span class="sxs-lookup"><span data-stu-id="65474-130"><a name="metrics"></a>What does it all mean?</span></span> <span data-ttu-id="65474-131">Performans kutucukları ve raporlar</span><span class="sxs-lookup"><span data-stu-id="65474-131">Performance tiles and reports</span></span>
<span data-ttu-id="65474-132">Çeşitli performans ölçümleri alma vardır.</span><span class="sxs-lookup"><span data-stu-id="65474-132">There are various performance metrics you can get.</span></span> <span data-ttu-id="65474-133">Varsayılan hello uygulaması dikey penceresinde görünen olanla başlayalım tıklatın.</span><span class="sxs-lookup"><span data-stu-id="65474-133">Let's start with those that appear by default on hello application blade.</span></span>

### <a name="requests"></a><span data-ttu-id="65474-134">İstekler</span><span class="sxs-lookup"><span data-stu-id="65474-134">Requests</span></span>
<span data-ttu-id="65474-135">Merhaba belirli bir süre içinde alınan HTTP isteklerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="65474-135">hello number of HTTP requests received in a specified period.</span></span> <span data-ttu-id="65474-136">Bu hello yük değiştikçe uygulamanızı nasıl davranacağını diğer raporları toosee hello sonuçlarına karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="65474-136">Compare this with hello results on other reports toosee how your app behaves as hello load varies.</span></span>

<span data-ttu-id="65474-137">HTTP istekleri sayfaları, veri ve görüntüleri için tüm GET veya POST istekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="65474-137">HTTP requests include all GET or POST requests for pages, data, and images.</span></span>

<span data-ttu-id="65474-138">Merhaba döşeme tooget sayar belirli URL'ler için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="65474-138">Click on hello tile tooget counts for specific URLs.</span></span>

### <a name="average-response-time"></a><span data-ttu-id="65474-139">Ortalama yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="65474-139">Average response time</span></span>
<span data-ttu-id="65474-140">Döndürülen uygulama ve hello yanıtınız girerek web isteği arasındaki ölçüleri hello süre.</span><span class="sxs-lookup"><span data-stu-id="65474-140">Measures hello time between a web request entering your application and hello response being returned.</span></span>

<span data-ttu-id="65474-141">Başlangıç noktaları bir hareketli ortalama gösterir.</span><span class="sxs-lookup"><span data-stu-id="65474-141">hello points show a moving average.</span></span> <span data-ttu-id="65474-142">Çok sayıda isteği varsa, olabilir hello ortalama belirgin yoğun olmayan gelen sapma veya hello grafiğinde DIP bazı.</span><span class="sxs-lookup"><span data-stu-id="65474-142">If there are a lot of requests, there might be some that deviate from hello average without an obvious peak or dip in hello graph.</span></span>

<span data-ttu-id="65474-143">Olağan dışı yükselmeleri arayın.</span><span class="sxs-lookup"><span data-stu-id="65474-143">Look for unusual peaks.</span></span> <span data-ttu-id="65474-144">Genel olarak, bir artışa istekleri ile yanıt süresi toorise bekler.</span><span class="sxs-lookup"><span data-stu-id="65474-144">In general, expect response time toorise with a rise in requests.</span></span> <span data-ttu-id="65474-145">Hello neden orantısız ise, uygulamanızın kullandığı bir hizmet CPU veya hello kapasitesi gibi bir kaynak sınırına ulaşması.</span><span class="sxs-lookup"><span data-stu-id="65474-145">If hello rise is disproportionate, your app might be hitting a resource limit such as CPU or hello capacity of a service it uses.</span></span>

<span data-ttu-id="65474-146">Merhaba döşeme tooget kez belirli URL'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="65474-146">Click hello tile tooget times for specific URLs.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-42reqs.png)

### <a name="slowest-requests"></a><span data-ttu-id="65474-147">En yavaş istekler</span><span class="sxs-lookup"><span data-stu-id="65474-147">Slowest requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-44slowest.png)

<span data-ttu-id="65474-148">Hangi isteklerinin performans ayarlaması gerekebilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="65474-148">Shows which requests might need performance tuning.</span></span>

### <a name="failed-requests"></a><span data-ttu-id="65474-149">Başarısız istekler</span><span class="sxs-lookup"><span data-stu-id="65474-149">Failed requests</span></span>
![](./media/app-insights-web-monitor-performance/appinsights-46failed.png)

<span data-ttu-id="65474-150">Yakalanmayan bir özel durum oluşturdu isteği sayısı.</span><span class="sxs-lookup"><span data-stu-id="65474-150">A count of requests that threw uncaught exceptions.</span></span>

<span data-ttu-id="65474-151">Merhaba döşeme toosee hello belirli hataları ayrıntılarını tıklayın ve kendi ayrıntı ayrı istek toosee seçin.</span><span class="sxs-lookup"><span data-stu-id="65474-151">Click hello tile toosee hello details of specific failures, and select an individual request toosee its detail.</span></span> 

<span data-ttu-id="65474-152">Hatalar için temsili bir örnek için tek tek denetleme korunur.</span><span class="sxs-lookup"><span data-stu-id="65474-152">Only a representative sample of failures is retained for individual inspection.</span></span>

### <a name="other-metrics"></a><span data-ttu-id="65474-153">Diğer ölçümleri</span><span class="sxs-lookup"><span data-stu-id="65474-153">Other metrics</span></span>
<span data-ttu-id="65474-154">toosee görüntülemek, bir grafiğe tıklayın ve ardından tüm hello ölçümleri toosee hello tam kullanılabilir seçimini kaldırın hangi diğer ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="65474-154">toosee what other metrics you can display, click a graph, and then deselect all hello metrics toosee hello full available set.</span></span> <span data-ttu-id="65474-155">()'ı toosee her ölçümü 's tanımı.</span><span class="sxs-lookup"><span data-stu-id="65474-155">Click (i) toosee each metric's definition.</span></span>

![Tüm ölçümleri toosee hello tüm seçimini kaldırın](./media/app-insights-web-monitor-performance/appinsights-62allchoices.png)

<span data-ttu-id="65474-157">Tüm ölçüm devre dışı bırakır hello seçerek üzerinde bulunamaz başkalarının aynı grafik hello.</span><span class="sxs-lookup"><span data-stu-id="65474-157">Selecting any metric disables hello others that can't appear on hello same chart.</span></span>

## <a name="set-alerts"></a><span data-ttu-id="65474-158">Uyarı ayarlama</span><span class="sxs-lookup"><span data-stu-id="65474-158">Set alerts</span></span>
<span data-ttu-id="65474-159">alışılmadık değerlerin herhangi bir ölçümü, e-postayla bildirim toobe bir uyarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="65474-159">toobe notified by email of unusual values of any metric, add an alert.</span></span> <span data-ttu-id="65474-160">Toosend hello e-posta toohello hesap yöneticileri ya da toospecific e-posta adreslerini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-160">You can choose either toosend hello email toohello account administrators, or toospecific email addresses.</span></span>

![](./media/app-insights-web-monitor-performance/appinsights-413setMetricAlert.png)

<span data-ttu-id="65474-161">Merhaba kaynak hello önce diğer özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="65474-161">Set hello resource before hello other properties.</span></span> <span data-ttu-id="65474-162">Performans ya da kullanım ölçümleri tooset uyarılar istiyorsanız hello Web testine kaynakları seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="65474-162">Don't choose hello webtest resources if you want tooset alerts on performance or usage metrics.</span></span>

<span data-ttu-id="65474-163">Dikkatli toonote hello birimleri tooenter hello eşik değeri sorulur olabilir.</span><span class="sxs-lookup"><span data-stu-id="65474-163">Be careful toonote hello units in which you're asked tooenter hello threshold value.</span></span>

<span data-ttu-id="65474-164">*Merhaba Ekle uyarı düğmesini görmek yok.*</span><span class="sxs-lookup"><span data-stu-id="65474-164">*I don't see hello Add Alert button.*</span></span> <span data-ttu-id="65474-165">-Bu salt okunur erişime sahip bir grup hesabı toowhich mi?</span><span class="sxs-lookup"><span data-stu-id="65474-165">- Is this a group account toowhich you have read-only access?</span></span> <span data-ttu-id="65474-166">Merhaba hesap yöneticinize danışın.</span><span class="sxs-lookup"><span data-stu-id="65474-166">Check with hello account administrator.</span></span>

## <span data-ttu-id="65474-167"><a name="diagnosis"></a>Sorunlarını tanılama</span><span class="sxs-lookup"><span data-stu-id="65474-167"><a name="diagnosis"></a>Diagnosing issues</span></span>
<span data-ttu-id="65474-168">Aşağıda, bulma ve performans sorunlarını tanılamak için birkaç ipucu verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="65474-168">Here are a few tips for finding and diagnosing performance issues:</span></span>

* <span data-ttu-id="65474-169">Ayarlanan [web testleri] [ availability] web sitenizi arıza ya da yanlış veya yavaş yanıt uyarı toobe.</span><span class="sxs-lookup"><span data-stu-id="65474-169">Set up [web tests][availability] toobe alerted if your web site goes down or responds incorrectly or slowly.</span></span> 
* <span data-ttu-id="65474-170">Hataları veya yavaş yanıt ilgili tooload varsa hello isteği diğer ölçümleri toosee sayısıyla karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="65474-170">Compare hello Request count with other metrics toosee if failures or slow response are related tooload.</span></span>
* <span data-ttu-id="65474-171">[Ekle ve arama izleme deyimleri] [ diagnostic] sorunları, kod toohelp sabitleme.</span><span class="sxs-lookup"><span data-stu-id="65474-171">[Insert and search trace statements][diagnostic] in your code toohelp pinpoint problems.</span></span>
* <span data-ttu-id="65474-172">Web uygulamanızda işlemiyle izlemek [ölçümleri bir canlı akışı][livestream].</span><span class="sxs-lookup"><span data-stu-id="65474-172">Monitor your Web app in operation with [Live Metrics Stream][livestream].</span></span>
* <span data-ttu-id="65474-173">.Net uygulamanızla Hello durumunu yakalama [anlık görüntü hata ayıklayıcı][snapshot].</span><span class="sxs-lookup"><span data-stu-id="65474-173">Capture hello state of your .Net application with [Snapshot Debugger][snapshot].</span></span>

## <a name="find-and-fix-performance-bottlenecks-with-an-interactive-performance-investigation"></a><span data-ttu-id="65474-174">Bulun ve etkileşimli performans araştırma ile performans sorunları giderin</span><span class="sxs-lookup"><span data-stu-id="65474-174">Find and fix performance bottlenecks with an interactive performance investigation</span></span>

<span data-ttu-id="65474-175">Genel performansını yavaşlamasının hello yeni Application Insights etkileşimli performans araştırma toolocate alanlarını Web uygulamanızı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-175">You can use hello new Application Insights interactive performance investigation toolocate areas of your Web app that are slowing down overall performance.</span></span> <span data-ttu-id="65474-176">Yavaşlamadan olan ve hello kullanan Bul belirli sayfaları hızla yapabilirsiniz [profil oluşturma aracı](app-insights-profiler.md) bu sayfaları arasında bir bağıntı ise toosee.</span><span class="sxs-lookup"><span data-stu-id="65474-176">You can quickly find specific pages that are slowing down, and use hello [Profiling tool](app-insights-profiler.md) toosee if there is a correlation between these pages.</span></span>

### <a name="create-a-list-of-slow-performing-pages"></a><span data-ttu-id="65474-177">Yavaş gerçekleştiren sayfalar listesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="65474-177">Create a list of slow performing pages</span></span> 

<span data-ttu-id="65474-178">performans sorunları bulmak için ilk adımı hello tooget hello sayfaları yanıt yavaş listesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="65474-178">hello first step for finding performance issues is tooget a list of hello slow responding pages.</span></span> <span data-ttu-id="65474-179">Aşağıda gösterilen hello ekran hello performans dikey tooget olası sayfaları tooinvestigate daha ayrıntılı bir listesini kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="65474-179">hello screen shot below demonstrates using hello Performance blade tooget a list of potential pages tooinvestigate further.</span></span> <span data-ttu-id="65474-180">Bu sayfadan yaklaşık 6:00 PM ve yeniden yaklaşık 10 PM, olduğunu bir konumlanır hello uygulama yanıt süresini hello hızlı şekilde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-180">You can quickly see from this page that there was a slow-down in hello response time of hello app at approximately 6:00 PM and again at approximately 10 PM.</span></span> <span data-ttu-id="65474-181">Merhaba GET müşteri/Ayrıntılar işlemi işlemleri bir 507.05 milisaniye ortalama yanıt süresi ile uzun çalışan olduğunu da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-181">You can also see that hello GET customer/details operation had some long running operations with a median response time of 507.05 milliseconds.</span></span> 

![Uygulama Öngörüler etkileşimli performansı](./media/app-insights-web-monitor-performance/performance1.png)

### <a name="drill-down-on-specific-pages"></a><span data-ttu-id="65474-183">Belirli sayfalara detaya gitme</span><span class="sxs-lookup"><span data-stu-id="65474-183">Drill down on specific pages</span></span>

<span data-ttu-id="65474-184">Uygulamanızın performansını görüntüsünü oluşturduktan sonra belirli yavaş performanslı işlemleri daha fazla bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-184">Once you have a snapshot of your app's performance, you can get more details on specific slow-performing operations.</span></span> <span data-ttu-id="65474-185">Aşağıda gösterildiği gibi hello listesi toosee hello ayrıntıları herhangi bir işlem tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65474-185">Click on any operation in hello list toosee hello details as shown below.</span></span> <span data-ttu-id="65474-186">Merhaba grafikten hello performans bir bağımlılığı dayanarak if görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-186">From hello chart you can see if hello performance was based on a dependency.</span></span> <span data-ttu-id="65474-187">Kaç tane kullanıcılar deneyimli hello çeşitli yanıt sürelerini de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-187">You can also see how many users experienced hello various response times.</span></span> 

![Uygulama Öngörüler işlemleri dikey penceresi](./media/app-insights-web-monitor-performance/performance5.png)

### <a name="drill-down-on-a-specific-time-period"></a><span data-ttu-id="65474-189">Belirli bir döneme detaya gitme</span><span class="sxs-lookup"><span data-stu-id="65474-189">Drill down on a specific time period</span></span>

<span data-ttu-id="65474-190">Zaman tooinvestigate noktasında tanımladıktan sonra hatta başka toolook hello performans konumlanır neden olabilecek hello belirli işlemler sırasında detaya.</span><span class="sxs-lookup"><span data-stu-id="65474-190">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="65474-191">Belirli bir noktasında zamanında tıkladığınızda hello Ayrıntılar aşağıda gösterildiği gibi hello sayfasının alın.</span><span class="sxs-lookup"><span data-stu-id="65474-191">When you click on a specific point in time you get hello details of hello page as shown below.</span></span> <span data-ttu-id="65474-192">Hello hello sunucu yanıt kodları ve hello işlemi süresi yanı sıra belirli bir süre için listelenen hello işlemleri, aşağıdaki örnekte görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-192">In hello example below you can see hello operations listed for a given time period along with hello server response codes and hello operation duration.</span></span> <span data-ttu-id="65474-193">Ayrıca bu bilgileri tooyour geliştirme ekibi toosend ihtiyacınız varsa, TFS iş öğesi açmak için hello url vardır.</span><span class="sxs-lookup"><span data-stu-id="65474-193">You also have hello url for opening a TFS work item if you need toosend this information tooyour development team.</span></span>

![Uygulama Öngörüler saat dilimi](./media/app-insights-web-monitor-performance/performance2.png)

### <a name="drill-down-on-a-specific-operation"></a><span data-ttu-id="65474-195">Belirli bir işlemi detaya gitme</span><span class="sxs-lookup"><span data-stu-id="65474-195">Drill down on a specific operation</span></span>

<span data-ttu-id="65474-196">Zaman tooinvestigate noktasında tanımladıktan sonra hatta başka toolook hello performans konumlanır neden olabilecek hello belirli işlemler sırasında detaya.</span><span class="sxs-lookup"><span data-stu-id="65474-196">After you have identified a point in time tooinvestigate, drill down even further toolook at hello specific operations that might have caused hello performance slow-down.</span></span> <span data-ttu-id="65474-197">Bir işlem hello listesi toosee hello ayrıntıları aşağıda gösterildiği gibi hello işleminin tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65474-197">Click on an operation from hello list toosee hello details of hello operation as shown below.</span></span> <span data-ttu-id="65474-198">Merhaba işlemi başarısız oldu ve Application Insights hello hello ayrıntılarını sağlamıştır görebilirsiniz Bu örnekte hello uygulama özel durum oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="65474-198">In this example you can see that hello operation failed, and Application Insights has provided hello details of hello exception hello application threw.</span></span> <span data-ttu-id="65474-199">Yeniden, bu dikey pencereden bir TFS iş öğesi kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65474-199">Again, you can easily create a TFS work item from this blade.</span></span>

![Uygulama Öngörüler işlemi dikey penceresi](./media/app-insights-web-monitor-performance/performance3.png)


## <span data-ttu-id="65474-201"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65474-201"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="65474-202">[Web testleri] [ availability] -web istekleri tooyour uygulama düzenli aralıklarla Merhaba Dünya göndermiş.</span><span class="sxs-lookup"><span data-stu-id="65474-202">[Web tests][availability] - Have web requests sent tooyour application at regular intervals from around hello world.</span></span>

<span data-ttu-id="65474-203">[Yakalama ve arama tanılama izlemeleri] [ diagnostic] - Ekle izleme çağrıları ve hello sonuçları toopinpoint sorunları SIFT.</span><span class="sxs-lookup"><span data-stu-id="65474-203">[Capture and search diagnostic traces][diagnostic] - Insert trace calls and sift through hello results toopinpoint issues.</span></span>

<span data-ttu-id="65474-204">[Kullanımı izleme] [ usage] -kişiler, uygulamanızın kullanımını bulun.</span><span class="sxs-lookup"><span data-stu-id="65474-204">[Usage tracking][usage] - Find out how people use your application.</span></span>

<span data-ttu-id="65474-205">[Sorun giderme] [ qna] - ve soru- cevap</span><span class="sxs-lookup"><span data-stu-id="65474-205">[Troubleshooting][qna] - and Q & A</span></span>



<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
[usage]: app-insights-web-track-usage.md
[livestream]: app-insights-live-stream.md
[snapshot]: app-insights-snapshot-debugger.md



