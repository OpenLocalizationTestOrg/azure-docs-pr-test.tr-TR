---
title: "aaaMonitor kullanılabilirlik ve yanıt hızını herhangi bir web sitesini | Microsoft Docs"
description: "Application Insights’ta web testleri ayarlayın. Web sitesi kullanılamaz duruma gelirse veya yavaş yanıt verirse uyarı alın."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a><span data-ttu-id="2a5df-104">Web sitelerinin kullanılabilirlik ve yanıt hızını izleme</span><span class="sxs-lookup"><span data-stu-id="2a5df-104">Monitor availability and responsiveness of any web site</span></span>
<span data-ttu-id="2a5df-105">Web uygulaması veya web sitesi tooany sunucu dağıtıldıktan sonra kullanılabilirlik ve yanıt hızını testleri toomonitor ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-105">After you've deployed your web app or web site tooany server, you can set up tests toomonitor its availability and responsiveness.</span></span> <span data-ttu-id="2a5df-106">[Azure Application Insights](app-insights-overview.md) Merhaba Dünya noktalarından düzenli aralıklarla web istekleri tooyour uygulama gönderir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-106">[Azure Application Insights](app-insights-overview.md) sends web requests tooyour application at regular intervals from points around hello world.</span></span> <span data-ttu-id="2a5df-107">Uygulamanız yanıt vermezse veya yavaş yanıt verirse sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-107">It alerts you if your application doesn't respond, or responds slowly.</span></span>

<span data-ttu-id="2a5df-108">Erişilebilir HTTPS uç noktası hello genel internet veya tüm HTTP için kullanılabilirlik testleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-108">You can set up availability tests for any HTTP or HTTPS endpoint that is accessible from hello public internet.</span></span> <span data-ttu-id="2a5df-109">Tooadd toohello web test etmekte site herhangi bir şey yok.</span><span class="sxs-lookup"><span data-stu-id="2a5df-109">You don't have tooadd anything toohello web site you're testing.</span></span> <span data-ttu-id="2a5df-110">Hatta, sitenizi toobe yok: üzerinde bağımlı bir REST API hizmeti test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-110">It doesn't even have toobe your site: you could test a REST API service on which you depend.</span></span>

<span data-ttu-id="2a5df-111">İki tür kullanılabilirlik testi vardır:</span><span class="sxs-lookup"><span data-stu-id="2a5df-111">There are two types of availability tests:</span></span>

* <span data-ttu-id="2a5df-112">[URL ping testi](#create): hello Azure portalında oluşturabileceğiniz basit bir sınama.</span><span class="sxs-lookup"><span data-stu-id="2a5df-112">[URL ping test](#create): a simple test that you can create in hello Azure portal.</span></span>
* <span data-ttu-id="2a5df-113">[Çok adımlı web testi](#multi-step-web-tests): Visual Studio Enterprise ve karşıya yükleme toohello portal oluşturan.</span><span class="sxs-lookup"><span data-stu-id="2a5df-113">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload toohello portal.</span></span>

<span data-ttu-id="2a5df-114">Her uygulama kaynağı too25 kullanılabilirlik testleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-114">You can create up too25 availability tests per application resource.</span></span>

## <span data-ttu-id="2a5df-115"><a name="create"></a>1. Kullanılabilirlik testi raporlarınız için kaynak açma</span><span class="sxs-lookup"><span data-stu-id="2a5df-115"><a name="create"></a>1. Open a resource for your availability test reports</span></span>

<span data-ttu-id="2a5df-116">**Application Insights zaten yapılandırdıysanız** web uygulamanız için Application Insights kaynağı hello açmak [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2a5df-116">**If you have already configured Application Insights** for your web app, open its Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="2a5df-117">**Veya yeni bir kaynak raporlarınızda toosee istiyorsanız** çok kaydolun[Microsoft Azure](http://azure.com), Git toohello [Azure portal](https://portal.azure.com)ve Application Insights kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a5df-117">**Or, if you want toosee your reports in a new resource,** sign up too[Microsoft Azure](http://azure.com), go toohello [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span></span>

![Yeni > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

<span data-ttu-id="2a5df-119">Tıklatın **tüm kaynakları** tooopen hello genel bakış dikey penceresinde hello yeni kaynak için.</span><span class="sxs-lookup"><span data-stu-id="2a5df-119">Click **All resources** tooopen hello Overview blade for hello new resource.</span></span>

## <span data-ttu-id="2a5df-120"><a name="setup"></a>2. URL ping testi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2a5df-120"><a name="setup"></a>2. Create a URL ping test</span></span>
<span data-ttu-id="2a5df-121">Merhaba kullanılabilirlik dikey penceresini açın ve bir test ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-121">Open hello Availability blade and add a test.</span></span>

![En az hello Web sitenizin URL'sini doldurma](./media/app-insights-monitor-web-app-availability/13-availability.png)

* <span data-ttu-id="2a5df-123">**Merhaba URL** herhangi bir web sayfası olabilir tootest istiyor, ancak gelen görünür olmalıdır genel internet hello.</span><span class="sxs-lookup"><span data-stu-id="2a5df-123">**hello URL** can be any web page you want tootest, but it must be visible from hello public internet.</span></span> <span data-ttu-id="2a5df-124">Merhaba URL sorgu dizesi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-124">hello URL can include a query string.</span></span> <span data-ttu-id="2a5df-125">Bu nedenle, örneğin, veritabanınızla biraz alıştırma yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-125">So, for example, you can exercise your database a little.</span></span> <span data-ttu-id="2a5df-126">Merhaba URL tooa yeniden yönlendirme çözümlenirse, biz bunu too10 yeniden yönlendirmeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-126">If hello URL resolves tooa redirect, we follow it up too10 redirects.</span></span>
* <span data-ttu-id="2a5df-127">**Bağımlı istekleri Ayrıştır**: Bu seçenek işaretlenirse, görüntüler, betikler, Stil dosyaları ve test altındaki hello web sayfasının parçası olan diğer dosyaları hello test ister.</span><span class="sxs-lookup"><span data-stu-id="2a5df-127">**Parse dependent requests**: If this option is checked, hello test requests images, scripts, style files, and other files that are part of hello web page under test.</span></span> <span data-ttu-id="2a5df-128">Merhaba kaydedilen yanıt süresi hello geçen süre tooget bu dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-128">hello recorded response time includes hello time taken tooget these files.</span></span> <span data-ttu-id="2a5df-129">Tüm bu kaynaklar hello tüm test için hello zaman aşımı süresi içinde başarıyla indirilemiyor hello sınama başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="2a5df-129">hello test fails if all these resources cannot be successfully downloaded within hello timeout for hello whole test.</span></span> 

    <span data-ttu-id="2a5df-130">Merhaba seçeneği işaretli değilse hello test yalnızca belirttiğiniz hello URL'sindeki hello dosya ister.</span><span class="sxs-lookup"><span data-stu-id="2a5df-130">If hello option is not checked, hello test only requests hello file at hello URL you specified.</span></span>
* <span data-ttu-id="2a5df-131">**Yeniden denemeyi etkinleştir**: Bu seçenek işaretlenirse hello test başarısız olduğunda, kısa bir süre sonra denenir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-131">**Enable retries**:  If this option is checked, when hello test fails, it is retried after a short interval.</span></span> <span data-ttu-id="2a5df-132">Art arda üç deneme başarısız olursa bir hata bildirilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-132">A failure is reported only if three successive attempts fail.</span></span> <span data-ttu-id="2a5df-133">Sonraki testler ardından hello her zamanki test sıklığında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-133">Subsequent tests are then performed at hello usual test frequency.</span></span> <span data-ttu-id="2a5df-134">Merhaba sonraki başarılı olana kadar yeniden deneme geçici olarak askıya alındı.</span><span class="sxs-lookup"><span data-stu-id="2a5df-134">Retry is temporarily suspended until hello next success.</span></span> <span data-ttu-id="2a5df-135">Bu kural her test konuma bağımsız olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-135">This rule is applied independently at each test location.</span></span> <span data-ttu-id="2a5df-136">Bu ayar önerilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-136">We recommend this option.</span></span> <span data-ttu-id="2a5df-137">Ortalama olarak hataların yaklaşık %80’i yeniden deneme sırasında kaybolur.</span><span class="sxs-lookup"><span data-stu-id="2a5df-137">On average, about 80% of failures disappear on retry.</span></span>
* <span data-ttu-id="2a5df-138">**Test sıklığı**: ne sıklıkta hello test her test konumdan çalıştırılacağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="2a5df-138">**Test frequency**: Sets how often hello test is run from each test location.</span></span> <span data-ttu-id="2a5df-139">Beş dakikalık sıklığında ve beş test konumuyla, siteniz ortalama olarak dakikada bir test edilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span></span>
* <span data-ttu-id="2a5df-140">**Test konumları** hello yerleştirir nerede sunucularımızda web istekleri tooyour URL'si den gönderdiğiniz şunlardır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-140">**Test locations** are hello places from where our servers send web requests tooyour URL.</span></span> <span data-ttu-id="2a5df-141">Bir konumdan fazla seçin; böylece, web sitenizdeki ağ sorunlarını ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-141">Choose more than one so that you can distinguish problems in your website from network issues.</span></span> <span data-ttu-id="2a5df-142">Too16 konumları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-142">You can select up too16 locations.</span></span>
* <span data-ttu-id="2a5df-143">**Başarı ölçütleri**:</span><span class="sxs-lookup"><span data-stu-id="2a5df-143">**Success criteria**:</span></span>

    <span data-ttu-id="2a5df-144">**Test zaman aşımı**: yavaş yanıtlar hakkında uyarı bu değeri toobe azaltın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-144">**Test timeout**: Decrease this value toobe alerted about slow responses.</span></span> <span data-ttu-id="2a5df-145">Merhaba yanıtlar sitenizden bu süre içinde henüz alınmamıştır varsa hello test hata olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-145">hello test is counted as a failure if hello responses from your site have not been received within this period.</span></span> <span data-ttu-id="2a5df-146">Seçtiyseniz **bağımlı istekleri Ayrıştır**, ardından tüm hello görüntüler, Stil dosyaları, betikler ve diğer bağımlı kaynaklar bu süre içinde alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-146">If you selected **Parse dependent requests**, then all hello images, style files, scripts, and other dependent resources must have been received within this period.</span></span>

    <span data-ttu-id="2a5df-147">**HTTP yanıtı**: hello başarılı sayılan durum kodunu döndürdü.</span><span class="sxs-lookup"><span data-stu-id="2a5df-147">**HTTP response**: hello returned status code that is counted as a success.</span></span> <span data-ttu-id="2a5df-148">200, normal web sayfası döndürüldüğünü belirten hello koddur.</span><span class="sxs-lookup"><span data-stu-id="2a5df-148">200 is hello code that indicates that a normal web page has been returned.</span></span>

    <span data-ttu-id="2a5df-149">**İçerik eşleşmesi**: "Hoş geldiniz!" gibi bir dize.</span><span class="sxs-lookup"><span data-stu-id="2a5df-149">**Content match**: a string, like "Welcome!"</span></span> <span data-ttu-id="2a5df-150">Her yanıtta büyük küçük harfe duyarlı bir tam eşleşme oluştuğunu test edebiliriz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-150">We test that an exact case-sensitive match occurs in every response.</span></span> <span data-ttu-id="2a5df-151">Joker karakter bulunmayan düz bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-151">It must be a plain string, without wildcards.</span></span> <span data-ttu-id="2a5df-152">Olması durumunda tooupdate olabilir sayfanızın içeriği değişirse unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-152">Don't forget that if your page content changes you might have tooupdate it.</span></span>
* <span data-ttu-id="2a5df-153">**Uyarıları** beş dakikayı üç konumda hata varsa varsayılan olarak, tooyou gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-153">**Alerts** are, by default, sent tooyou if there are failures in three locations over five minutes.</span></span> <span data-ttu-id="2a5df-154">Tek bir konumda büyük olasılıkla toobe bir ağ sorunu ve sitenizi olmayan bir sorun hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-154">A failure in one location is likely toobe a network problem, and not a problem with your site.</span></span> <span data-ttu-id="2a5df-155">Ancak hello eşik toobe daha fazla değiştirebilir veya duyarlı ve daha az de e-postaları hello değişiklik gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-155">But you can change hello threshold toobe more or less sensitive, and you can also change who hello emails should be sent to.</span></span>

    <span data-ttu-id="2a5df-156">Bir uyarı ortaya çıktığında çağrılan bir [web kancası](../monitoring-and-diagnostics/insights-webhooks-alerts.md) ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span> <span data-ttu-id="2a5df-157">(Ancak şu anda sorgu parametreleri Özellikler aracılığıyla geçirilmez.)</span><span class="sxs-lookup"><span data-stu-id="2a5df-157">(But note that, at present, query parameters are not passed through as Properties.)</span></span>

### <a name="test-more-urls"></a><span data-ttu-id="2a5df-158">Daha fazla URL test etme</span><span class="sxs-lookup"><span data-stu-id="2a5df-158">Test more URLs</span></span>
<span data-ttu-id="2a5df-159">Daha fazla test ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-159">Add more tests.</span></span> <span data-ttu-id="2a5df-160">Örneğin, ek tootesting giriş sayfanız, arama hello URL'sini test ederek veritabanınızın çalıştığından emin olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-160">For example, In addition tootesting your home page, you can make sure your database is running by testing hello URL for a search.</span></span>


## <span data-ttu-id="2a5df-161"><a name="monitor"></a>3. Kullanılabilirlik testi sonuçlarınızı görme</span><span class="sxs-lookup"><span data-stu-id="2a5df-161"><a name="monitor"></a>3. See your availability test results</span></span>

<span data-ttu-id="2a5df-162">Birkaç dakika sonra'ı **yenileme** toosee test sonuçları.</span><span class="sxs-lookup"><span data-stu-id="2a5df-162">After a few minutes, click **Refresh** toosee test results.</span></span> 

![Merhaba giriş dikey penceresinde Özet Sonuçları](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

<span data-ttu-id="2a5df-164">Merhaba scatterplot hello örnekleri tanılama testi adım ayrıntı olması test sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-164">hello scatterplot shows samples of hello test results that have diagnostic test-step detail in them.</span></span> <span data-ttu-id="2a5df-165">Merhaba test altyapısı hataları olan testleri için tanılama ayrıntı depolar.</span><span class="sxs-lookup"><span data-stu-id="2a5df-165">hello test engine stores diagnostic detail for tests that have failures.</span></span> <span data-ttu-id="2a5df-166">Başarılı testleri için tanılama ayrıntıları hello yürütmeleri bir kısmı için depolanır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-166">For successful tests, diagnostic details are stored for a subset of hello executions.</span></span> <span data-ttu-id="2a5df-167">Tüm hello yeşil/kırmızı nokta toosee hello test zaman damgası, test süresi, konum ve test adı gelin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-167">Hover over any of hello green/red dots toosee hello test timestamp, test duration, location, and test name.</span></span> <span data-ttu-id="2a5df-168">Merhaba dağılım çizim toosee hello ayrıntılarını hello test sonucu herhangi bir nokta üzerinden'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-168">Click through any dot in hello scatter plot toosee hello details of hello test result.</span></span>  

<span data-ttu-id="2a5df-169">Konum, belirli bir testi seçin veya dönem toosee hello süre ilgi daha fazla sonuç hello süresini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-169">Select a particular test, location, or reduce hello time period toosee more results around hello time period of interest.</span></span> <span data-ttu-id="2a5df-170">Arama Gezgini toosee tüm yürütmeleri sonuçlarından veya bu veriler üzerinde analiz sorguları toorun özel raporlar kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-170">Use Search Explorer toosee results from all executions, or use Analytics queries toorun custom reports on this data.</span></span>

<span data-ttu-id="2a5df-171">Toplama toohello ham sonuçlarında ölçümleri Explorer'da iki kullanılabilirlik ölçümleri vardır:</span><span class="sxs-lookup"><span data-stu-id="2a5df-171">In addition toohello raw results, there are two Availability metrics in Metrics Explorer:</span></span> 

1. <span data-ttu-id="2a5df-172">Kullanılabilirlik: Tüm test yürütmeleri arasında başarılı hello testleri yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="2a5df-172">Availability: Percentage of hello tests that were successful, across all test executions.</span></span> 
2. <span data-ttu-id="2a5df-173">Test Süresi: Tüm test yürütmelerinde ortalama test süresi.</span><span class="sxs-lookup"><span data-stu-id="2a5df-173">Test Duration: Average test duration across all test executions.</span></span>

<span data-ttu-id="2a5df-174">Filtreler hello test adı, konumu tooanalyze eğilimleri belirli test ve/veya konum uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-174">You can apply filters on hello test name, location tooanalyze trends of a particular test and/or location.</span></span>

## <span data-ttu-id="2a5df-175"><a name="edit"></a> Testleri inceleme ve düzenleme</span><span class="sxs-lookup"><span data-stu-id="2a5df-175"><a name="edit"></a> Inspect and edit tests</span></span>

<span data-ttu-id="2a5df-176">Merhaba Özet sayfası, belirli bir test seçin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-176">From hello summary page, select a specific test.</span></span> <span data-ttu-id="2a5df-177">Burada özel sonuçları görebilir ve düzenleyebilir ya da geçici olarak devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-177">There, you can see its specific results, and edit or temporarily disable it.</span></span>

![Web testini düzenleme veya devre dışı bırakma](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

<span data-ttu-id="2a5df-179">Toodisable kullanılabilirlik testleri veya hizmetinizde Bakımı gerçekleştirirken kuralları ilişkili hello uyarı isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-179">You might want toodisable availability tests or hello alert rules associated with them while you are performing maintenance on your service.</span></span> 

## <span data-ttu-id="2a5df-180"><a name="failures"></a>Hata görürseniz</span><span class="sxs-lookup"><span data-stu-id="2a5df-180"><a name="failures"></a>If you see failures</span></span>
<span data-ttu-id="2a5df-181">Kırmızı noktaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-181">Click a red dot.</span></span>

![Kırmızı noktaya tıklama](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


<span data-ttu-id="2a5df-183">Bir kullanılabilirlik testi sonucundan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2a5df-183">From an availability test result, you can:</span></span>

* <span data-ttu-id="2a5df-184">Sunucudan alınan hello yanıtı inceleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-184">Inspect hello response received from your server.</span></span>
* <span data-ttu-id="2a5df-185">Merhaba başarısız istek örneği işlenirken sunucu uygulamanız tarafından gönderilen hello telemetriyi açın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-185">Open hello telemetry sent by your server app while processing hello failed request instance.</span></span>
* <span data-ttu-id="2a5df-186">Bir sorun oturum veya Git veya VSTS tootrack hello sorun iş öğesi.</span><span class="sxs-lookup"><span data-stu-id="2a5df-186">Log an issue or work item in Git or VSTS tootrack hello problem.</span></span> <span data-ttu-id="2a5df-187">Merhaba hata bağlantı toothis olayı içerir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-187">hello bug will contain a link toothis event.</span></span>
* <span data-ttu-id="2a5df-188">Merhaba web test sonucu Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-188">Open hello web test result in Visual Studio.</span></span>


<span data-ttu-id="2a5df-189">*Sorunsuz görünüyor ancak hata olarak mı bildiriliyor?*</span><span class="sxs-lookup"><span data-stu-id="2a5df-189">*Looks OK but reported as a failure?*</span></span> <span data-ttu-id="2a5df-190">Tüm hello görüntüleri, betikler, stil sayfaları ve hello sayfa tarafından yüklenen diğer dosyaları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-190">Check all hello images, scripts, style sheets, and any other files loaded by hello page.</span></span> <span data-ttu-id="2a5df-191">Herhangi biri başarısız olursa, hello ana html sayfası Tamam olarak yüklense bile hello test başarısız olarak raporlanır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-191">If any of them fails, hello test is reported as failed, even if hello main html page loads OK.</span></span>

<span data-ttu-id="2a5df-192">*İlgili öğe yok mu?*</span><span class="sxs-lookup"><span data-stu-id="2a5df-192">*No related items?*</span></span> <span data-ttu-id="2a5df-193">Sunucu tarafı uygulamanız için Application Insights ayarlanmışsa, bunun nedeni [örnekleme](app-insights-sampling.md) işleminin devam ediyor olması olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-193">If you have Application Insights set up for your server-side application, that may be because [sampling](app-insights-sampling.md) is in operation.</span></span> 

## <a name="multi-step-web-tests"></a><span data-ttu-id="2a5df-194">Çok adımlı web testleri</span><span class="sxs-lookup"><span data-stu-id="2a5df-194">Multi-step web tests</span></span>
<span data-ttu-id="2a5df-195">Bir dizi URL'nin bulunduğu bir senaryoyu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-195">You can monitor a scenario that involves a sequence of URLs.</span></span> <span data-ttu-id="2a5df-196">Örneğin, bir satış Web sitesi izliyorsanız, öğeleri toohello ekleme alışveriş sepeti düzgün çalıştığını test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-196">For example, if you are monitoring a sales website, you can test that adding items toohello shopping cart works correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="2a5df-197">Çok adımlı web testleri ücrete tabidir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-197">There is a charge for multi-step web tests.</span></span> <span data-ttu-id="2a5df-198">[Fiyatlandırma düzeni](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="2a5df-198">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>
> 

<span data-ttu-id="2a5df-199">çok adımlı bir test toocreate, Visual Studio Enterprise kullanarak hello senaryo kaydetmek ve tooApplication Öngörüler kaydı hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-199">toocreate a multi-step test, you record hello scenario by using Visual Studio Enterprise, and then upload hello recording tooApplication Insights.</span></span> <span data-ttu-id="2a5df-200">Application Insights hello senaryoyu aralıklarla başlayarak yeniden oynatılır ve hello yanıtları doğrular.</span><span class="sxs-lookup"><span data-stu-id="2a5df-200">Application Insights replays hello scenario at intervals and verifies hello responses.</span></span>

> [!NOTE]
> <span data-ttu-id="2a5df-201">Testlerinizde kodlanmış işlevler veya döngüler kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="2a5df-201">You can't use coded functions or loops in your tests.</span></span> <span data-ttu-id="2a5df-202">Merhaba test tamamen hello .webtest komut dosyasında yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-202">hello test must be contained completely in hello .webtest script.</span></span> <span data-ttu-id="2a5df-203">Ancak, standart eklentiler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-203">However, you can use standard plugins.</span></span>
>

#### <a name="1-record-a-scenario"></a><span data-ttu-id="2a5df-204">1. Senaryo kaydetme</span><span class="sxs-lookup"><span data-stu-id="2a5df-204">1. Record a scenario</span></span>
<span data-ttu-id="2a5df-205">Visual Studio Enterprise kullanan bir web oturumu toorecord.</span><span class="sxs-lookup"><span data-stu-id="2a5df-205">Use Visual Studio Enterprise toorecord a web session.</span></span>

1. <span data-ttu-id="2a5df-206">Web performans testi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a5df-206">Create a Web performance test project.</span></span>

    ![Visual Studio Enterprise Edition'da hello Web performansı ve yük testi şablonundan bir proje oluşturun.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * <span data-ttu-id="2a5df-208">*Merhaba Web performansı ve yük testi şablon görmüyorum?*</span><span class="sxs-lookup"><span data-stu-id="2a5df-208">*Don't see hello Web Performance and Load Test template?*</span></span> <span data-ttu-id="2a5df-209">- Visual Studio Enterprise’ı kapatın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-209">- Close Visual Studio Enterprise.</span></span> <span data-ttu-id="2a5df-210">Açık **Visual Studio yükleyicisi** toomodify, Visual Studio Enterprise yükleme.</span><span class="sxs-lookup"><span data-stu-id="2a5df-210">Open **Visual Studio Installer** toomodify your Visual Studio Enterprise installation.</span></span> <span data-ttu-id="2a5df-211">**Tek Bileşenler** altında **Web Performansı ve yük testi araçları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-211">Under **Individual Components**, select **Web Performance and load testing tools**.</span></span>

2. <span data-ttu-id="2a5df-212">Merhaba .webtest dosyasını açın ve kaydı başlatın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-212">Open hello .webtest file and start recording.</span></span>

    ![Merhaba .webtest dosyasını açın ve Kaydet'e tıklayın.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. <span data-ttu-id="2a5df-214">Testinizde toosimulate istediğiniz kullanıcı eylemleri hello: Web sitenizi açın, bir ürün toohello Sepeti ekleyin ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="2a5df-214">Do hello user actions you want toosimulate in your test: open your website, add a product toohello cart, and so on.</span></span> <span data-ttu-id="2a5df-215">Sonra testinizi durdurun.</span><span class="sxs-lookup"><span data-stu-id="2a5df-215">Then stop your test.</span></span>

    ![Internet Explorer'da Hello web Testi Kaydedicisi çalışır.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    <span data-ttu-id="2a5df-217">Uzun bir senaryo oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-217">Don't make a long scenario.</span></span> <span data-ttu-id="2a5df-218">100 adımlık ve 2 dakikalık bir sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-218">There's a limit of 100 steps and 2 minutes.</span></span>
4. <span data-ttu-id="2a5df-219">Merhaba testine düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="2a5df-219">Edit hello test to:</span></span>

   * <span data-ttu-id="2a5df-220">Doğrulama, toocheck hello alınan metin ve yanıt kodlarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-220">Add validations toocheck hello received text and response codes.</span></span>
   * <span data-ttu-id="2a5df-221">Gereksiz tüm etkileşimleri kaldırma.</span><span class="sxs-lookup"><span data-stu-id="2a5df-221">Remove any superfluous interactions.</span></span> <span data-ttu-id="2a5df-222">Ayrıca, resim veya tooad ya da sitelerin izlenmesi için bağımlı istekleri kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-222">You could also remove dependent requests for pictures or tooad or tracking sites.</span></span>

     <span data-ttu-id="2a5df-223">Yalnızca hello test betiğini düzenleyebildiğinizi - özel kod ekleme veya başka web testlerinden çağrı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-223">Remember that you can only edit hello test script - you can't add custom code or call other web tests.</span></span> <span data-ttu-id="2a5df-224">Döngüler hello eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-224">Don't insert loops in hello test.</span></span> <span data-ttu-id="2a5df-225">Standart web testi eklentileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-225">You can use standard web test plug-ins.</span></span>
5. <span data-ttu-id="2a5df-226">Merhaba test çalıştığından emin Visual Studio toomake çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-226">Run hello test in Visual Studio toomake sure it works.</span></span>

    <span data-ttu-id="2a5df-227">Merhaba web test Çalıştırıcısı bir web tarayıcısı açar ve kaydettiğiniz eylemleri yineler hello.</span><span class="sxs-lookup"><span data-stu-id="2a5df-227">hello web test runner opens a web browser and repeats hello actions you recorded.</span></span> <span data-ttu-id="2a5df-228">Beklediğiniz gibi çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="2a5df-228">Make sure it works as you expect.</span></span>

    ![Visual Studio'da hello .webtest dosyasını açın ve Çalıştır'ı tıklatın.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a><span data-ttu-id="2a5df-230">2. Merhaba web testi tooApplication Öngörüler karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="2a5df-230">2. Upload hello web test tooApplication Insights</span></span>
1. <span data-ttu-id="2a5df-231">Merhaba Application Insights portalında bir web testi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a5df-231">In hello Application Insights portal, create a web test.</span></span>

    ![Merhaba web testleri dikey penceresinde Ekle'yi seçin.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. <span data-ttu-id="2a5df-233">Çok adımlı testi seçin ve hello .webtest dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-233">Select multi-step test, and upload hello .webtest file.</span></span>

    ![Çok adımlı web testini seçin.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    <span data-ttu-id="2a5df-235">Kümesi hello test konumları, sıklığı ve uyarı parametrelerinde hello aynı şekilde ping gibi sınar.</span><span class="sxs-lookup"><span data-stu-id="2a5df-235">Set hello test locations, frequency, and alert parameters in hello same way as for ping tests.</span></span>

#### <a name="3-see-hello-results"></a><span data-ttu-id="2a5df-236">3. Merhaba sonuçları bakın</span><span class="sxs-lookup"><span data-stu-id="2a5df-236">3. See hello results</span></span>

<span data-ttu-id="2a5df-237">Test görüntülemek sonuçlarını ve hatalarını içinde hello aynı şekilde olarak tek url sınamaları.</span><span class="sxs-lookup"><span data-stu-id="2a5df-237">View your test results and any failures in hello same way as single-url tests.</span></span>

<span data-ttu-id="2a5df-238">Ayrıca, hello test sonuçları tooview indirebilirsiniz Visual Studio bunları.</span><span class="sxs-lookup"><span data-stu-id="2a5df-238">In addition, you can download hello test results tooview them in Visual Studio.</span></span>

#### <a name="too-many-failures"></a><span data-ttu-id="2a5df-239">Çok fazla hata mı var?</span><span class="sxs-lookup"><span data-stu-id="2a5df-239">Too many failures?</span></span>

* <span data-ttu-id="2a5df-240">Yaygın bir başarısızlık nedeni hello testin çok uzun çalıştığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-240">A common reason for failure is that hello test runs too long.</span></span> <span data-ttu-id="2a5df-241">İki dakikadan uzun çalıştırılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-241">It mustn't run longer than two minutes.</span></span>

* <span data-ttu-id="2a5df-242">Bir sayfanın tüm hello kaynakları betikler, stil sayfaları, görüntüler ve diğerleri de dahil olmak üzere hello test toosucceed için doğru yüklemelisiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-242">Don't forget that all hello resources of a page must load correctly for hello test toosucceed, including scripts, style sheets, images, and so forth.</span></span>

* <span data-ttu-id="2a5df-243">Hello web testinin tamamen hello .webtest komut dosyasında yer almalıdır: hello testte kodlanmış işlevleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="2a5df-243">hello web test must be entirely contained in hello .webtest script: you can't use coded functions in hello test.</span></span>

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a><span data-ttu-id="2a5df-244">Çok adımlı testinizde bağlı kalma süresi ve rasgele rakamlar</span><span class="sxs-lookup"><span data-stu-id="2a5df-244">Plugging time and random numbers into your multi-step test</span></span>
<span data-ttu-id="2a5df-245">Dış bir kaynağa ait stoklar gibi zamana bağımlı veriler alan bir aracı test ettiğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="2a5df-245">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span></span> <span data-ttu-id="2a5df-246">Web testinizi kaydettiğinizde, toouse belirli saatler sahip, ancak gibi hello parametrelerinin test, StartTime ve EndTime ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-246">When you record your web test, you have toouse specific times, but you set them as parameters of hello test, StartTime and EndTime.</span></span>

![Parametrelere sahip web testi.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

<span data-ttu-id="2a5df-248">Merhaba testi çalıştırdığınızda, EndTime her zaman zaman toobe hello sunmak istediğiniz ve başlangıç saati, 15 dakika olmalıdır önce.</span><span class="sxs-lookup"><span data-stu-id="2a5df-248">When you run hello test, you'd like EndTime always toobe hello present time, and StartTime should be 15 minutes ago.</span></span>

<span data-ttu-id="2a5df-249">Web testi eklentileri toodo Parametreleştirme kez hello yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="2a5df-249">Web Test Plug-ins provide hello way toodo parameterize times.</span></span>

1. <span data-ttu-id="2a5df-250">İstediğiniz her değişken parametre değeri için bir web testi eklentisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-250">Add a web test plug-in for each variable parameter value you want.</span></span> <span data-ttu-id="2a5df-251">Merhaba web testi araç çubuğunda seçin **Web Testi Eklentisi Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2a5df-251">In hello web test toolbar, choose **Add Web Test Plugin**.</span></span>

    ![Web Testi Eklentisi Ekle’yi, sonra da bir türü seçin.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    <span data-ttu-id="2a5df-253">Bu örnekte, hello tarih saat eklentisinin iki örneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-253">In this example, we use two instances of hello Date Time Plug-in.</span></span> <span data-ttu-id="2a5df-254">Bir örnek "15 dakika önce" için, bir örnek de "şimdi" için.</span><span class="sxs-lookup"><span data-stu-id="2a5df-254">One instance is for "15 minutes ago" and another for "now."</span></span>
2. <span data-ttu-id="2a5df-255">Her eklentinin Hello özelliklerini açın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-255">Open hello properties of each plug-in.</span></span> <span data-ttu-id="2a5df-256">Bir ad verin ve geçerli saati toouse hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-256">Give it a name and set it toouse hello current time.</span></span> <span data-ttu-id="2a5df-257">Bunlardan birini Dakika Ekle = 15 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-257">For one of them, set Add Minutes = -15.</span></span>

    ![Adı, Geçerli Saati Kullan’ı ve Dakika Ekle’yi ayarlayın.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. <span data-ttu-id="2a5df-259">Merhaba web testi parametrelerinde, eklenti adına {{plug-in name}} tooreference kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-259">In hello web test parameters, use {{plug-in name}} tooreference a plug-in name.</span></span>

    ![Merhaba test parametresinde {{plug-in name}} kullanın.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

<span data-ttu-id="2a5df-261">Şimdi, test toohello portalınızı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-261">Now, upload your test toohello portal.</span></span> <span data-ttu-id="2a5df-262">Her hello testi Çalıştır'hello dinamik değerler kullanır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-262">It uses hello dynamic values on every run of hello test.</span></span>

## <a name="dealing-with-sign-in"></a><span data-ttu-id="2a5df-263">Oturum açmayla ilgilenme</span><span class="sxs-lookup"><span data-stu-id="2a5df-263">Dealing with sign-in</span></span>
<span data-ttu-id="2a5df-264">Kullanıcılarınızın tooyour uygulamada oturum açarsanız hello oturum açma ötesinde sayfaları test edebilirsiniz bir oturum açma benzetimi için çeşitli seçenekleriniz vardır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-264">If your users sign in tooyour app, you have various options for simulating sign-in so that you can test pages behind hello sign-in.</span></span> <span data-ttu-id="2a5df-265">kullandığınız hello yaklaşım hello hello uygulamanın sağladığı güvenlik türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-265">hello approach you use depends on hello type of security provided by hello app.</span></span>

<span data-ttu-id="2a5df-266">Her durumda, uygulamanızı test etme yalnızca hello amacı için bir hesap oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-266">In all cases, you should create an account in your application just for hello purpose of testing.</span></span> <span data-ttu-id="2a5df-267">Gerçek kullanıcıları etkileyen hello web testleri hiçbir olasılığını olmasını sağlamak Mümkünse, bu test hesabın hello izinleri kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-267">If possible, restrict hello permissions of this test account so that there's no possibility of hello web tests affecting real users.</span></span>

### <a name="simple-username-and-password"></a><span data-ttu-id="2a5df-268">Basit kullanıcı adı ve parola</span><span class="sxs-lookup"><span data-stu-id="2a5df-268">Simple username and password</span></span>
<span data-ttu-id="2a5df-269">Hello web testini kaydetme her zamanki gibi.</span><span class="sxs-lookup"><span data-stu-id="2a5df-269">Record a web test in hello usual way.</span></span> <span data-ttu-id="2a5df-270">Önce tanımlama bilgilerini silin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-270">Delete cookies first.</span></span>

### <a name="saml-authentication"></a><span data-ttu-id="2a5df-271">SAML kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2a5df-271">SAML authentication</span></span>
<span data-ttu-id="2a5df-272">Web testleri için kullanılabilir hello SAML eklentisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-272">Use hello SAML plugin that is available for web tests.</span></span>

### <a name="client-secret"></a><span data-ttu-id="2a5df-273">Gizli anahtar</span><span class="sxs-lookup"><span data-stu-id="2a5df-273">Client secret</span></span>
<span data-ttu-id="2a5df-274">Uygulamanızda gizli anahtar içeren bir oturum açma yolu varsa bu yolu kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-274">If your app has a sign-in route that involves a client secret, use that route.</span></span> <span data-ttu-id="2a5df-275">Azure Active Directory (AAD), gizli anahtarla oturum açmayı sağlayan bir hizmet örneğidir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-275">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span></span> <span data-ttu-id="2a5df-276">AAD'de, hello gizli hello uygulama anahtarı ' dir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-276">In AAD, hello client secret is hello App Key.</span></span>

<span data-ttu-id="2a5df-277">Aşağıda uygulama anahtarı kullanan bir Azure web uygulaması için web testi örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="2a5df-277">Here's a sample web test of an Azure web app using an app key:</span></span>

![Gizli anahtar örneği](./media/app-insights-monitor-web-app-availability/110.png)

1. <span data-ttu-id="2a5df-279">Gizli anahtar (AppKey) kullanarak AAD’den belirteç alın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-279">Get token from AAD using client secret (AppKey).</span></span>
2. <span data-ttu-id="2a5df-280">Yanıttan taşıyıcı belirteci ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-280">Extract bearer token from response.</span></span>
3. <span data-ttu-id="2a5df-281">Merhaba yetkilendirme üstbilgisinde taşıyıcı belirteci kullanarak API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="2a5df-281">Call API using bearer token in hello authorization header.</span></span>

<span data-ttu-id="2a5df-282">Merhaba web testi gerçek bir istemcidir - diğer bir deyişle, kendi uygulama - AAD'de var olduğundan emin olun ve kendi ClientID + appkey kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-282">Make sure that hello web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span></span> <span data-ttu-id="2a5df-283">Hizmetinizi test altında kendi uygulama AAD'de de vardır.: hello AppID bu uygulamanın URI hello web testi hello "kaynak" alanında yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-283">Your service under test also has its own app in AAD: hello appID URI of this app is reflected in hello web test in hello “resource” field.</span></span>

### <a name="open-authentication"></a><span data-ttu-id="2a5df-284">Açık Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="2a5df-284">Open Authentication</span></span>
<span data-ttu-id="2a5df-285">Microsoft veya Google hesabınızla oturum açma, bir açık kimlik doğrulaması örneğidir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-285">An example of open authentication is signing in with your Microsoft or Google account.</span></span> <span data-ttu-id="2a5df-286">Birçok uygulama tooinvestigate, ilk Taktik bunun nedenle OAuth sağladıkları kullanım istemci gizli alternatif, o olasılığı hello olduğunu.</span><span class="sxs-lookup"><span data-stu-id="2a5df-286">Many apps that use OAuth provide hello client secret alternative, so your first tactic should be tooinvestigate that possibility.</span></span>

<span data-ttu-id="2a5df-287">Testinizde OAuth kullanılarak oturum gerekir, hello genel yaklaşım şöyledir:</span><span class="sxs-lookup"><span data-stu-id="2a5df-287">If your test must sign in using OAuth, hello general approach is:</span></span>

* <span data-ttu-id="2a5df-288">Web tarayıcınız, hello kimlik doğrulama sitesi ve uygulamanız arasındaki Fiddler tooexamine hello trafiği gibi bir araç kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-288">Use a tool such as Fiddler tooexamine hello traffic between your web browser, hello authentication site, and your app.</span></span>
* <span data-ttu-id="2a5df-289">İki veya daha fazla oturum farklı makineler veya tarayıcılar kullanarak bileşenlere gerçekleştirmek veya uzun aralıklarla (tooallow belirteçleri tooexpire).</span><span class="sxs-lookup"><span data-stu-id="2a5df-289">Perform two or more sign-ins using different machines or browsers, or at long intervals (tooallow tokens tooexpire).</span></span>
* <span data-ttu-id="2a5df-290">Farklı oturumları karşılaştırarak hello tooyour uygulama sunucusuna oturum açma işleminden sonra sonra geçirilen site, kimlik doğrulaması'ndan geçirildi hello belirteci tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-290">By comparing different sessions, identify hello token passed back from hello authenticating site, that is then passed tooyour app server after sign-in.</span></span>
* <span data-ttu-id="2a5df-291">Visual Studio’yu kullanarak web testini kaydetme</span><span class="sxs-lookup"><span data-stu-id="2a5df-291">Record a web test using Visual Studio.</span></span>
* <span data-ttu-id="2a5df-292">Merhaba belirteci hello doğrulayıcıdan döndürüldüğünde hello parametre ayarlama ve hello sorgu toohello sitede kullanılarak hello belirteçleri parametreleyin.</span><span class="sxs-lookup"><span data-stu-id="2a5df-292">Parameterize hello tokens, setting hello parameter when hello token is returned from hello authenticator, and using it in hello query toohello site.</span></span>
  <span data-ttu-id="2a5df-293">(Visual Studio tooparameterize hello test çalışır, ancak doğru hello belirteçleri Parametreleştirme değil.)</span><span class="sxs-lookup"><span data-stu-id="2a5df-293">(Visual Studio attempts tooparameterize hello test, but does not correctly parameterize hello tokens.)</span></span>


## <a name="performance-tests"></a><span data-ttu-id="2a5df-294">Performans testleri</span><span class="sxs-lookup"><span data-stu-id="2a5df-294">Performance tests</span></span>
<span data-ttu-id="2a5df-295">Web sitenizde bir yük testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-295">You can run a load test on your website.</span></span> <span data-ttu-id="2a5df-296">Merhaba kullanılabilirlik test gibi Merhaba Dünya bizim noktalarından basit istekleri veya çok adımlı istekleri gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-296">Like hello availability test, you can send either simple requests or multi-step requests from our points around hello world.</span></span> <span data-ttu-id="2a5df-297">Kullanılabilirlik testinden farklı olarak eşzamanlı birden fazla kullanıcıyı benzeten çok sayıda istek gönderilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-297">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span></span>

<span data-ttu-id="2a5df-298">Merhaba genel bakış dikey penceresinden açmak **ayarları**, **performans testleri**.</span><span class="sxs-lookup"><span data-stu-id="2a5df-298">From hello Overview blade, open **Settings**, **Performance Tests**.</span></span> <span data-ttu-id="2a5df-299">Bir test oluşturduğunuzda, davet tooconnect tooor bir Visual Studio Team Services hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2a5df-299">When you create a test, you are invited tooconnect tooor create a Visual Studio Team Services account.</span></span>

<span data-ttu-id="2a5df-300">Merhaba test tamamlandığında yanıt sürelerini ve başarı oranları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-300">When hello test is complete, you are shown response times and success rates.</span></span>


![Performans testi](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> <span data-ttu-id="2a5df-302">bir performans testi tooobserve hello etkilerini kullanmak [canlı akış](app-insights-live-stream.md) ve [profil oluşturucu](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="2a5df-302">tooobserve hello effects of a performance test, use [Live Stream](app-insights-live-stream.md) and [Profiler](app-insights-profiler.md).</span></span>
>

## <a name="automation"></a><span data-ttu-id="2a5df-303">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="2a5df-303">Automation</span></span>
* <span data-ttu-id="2a5df-304">[PowerShell komut dosyaları tooset bir kullanılabilirlik test yukarı kullanmak](app-insights-powershell.md#add-an-availability-test) otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="2a5df-304">[Use PowerShell scripts tooset up an availability test](app-insights-powershell.md#add-an-availability-test) automatically.</span></span>
* <span data-ttu-id="2a5df-305">Bir uyarı ortaya çıktığında çağrılan bir [web kancası](../monitoring-and-diagnostics/insights-webhooks-alerts.md) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-305">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span>

## <span data-ttu-id="2a5df-306"><a name="qna"></a>Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="2a5df-306"><a name="qna"></a>Questions?</span></span> <span data-ttu-id="2a5df-307">Sorunlarınız mı var?</span><span class="sxs-lookup"><span data-stu-id="2a5df-307">Problems?</span></span>
* <span data-ttu-id="2a5df-308">*Web testimden kod çağırabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="2a5df-308">*Can I call code from my web test?*</span></span>

    <span data-ttu-id="2a5df-309">Hayır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-309">No.</span></span> <span data-ttu-id="2a5df-310">Merhaba adımları hello test hello .webtest dosyasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-310">hello steps of hello test must be in hello .webtest file.</span></span> <span data-ttu-id="2a5df-311">Bu nedenle, başka web testlerini çağıramaz, döngüleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="2a5df-311">And you can't call other web tests or use loops.</span></span> <span data-ttu-id="2a5df-312">Ancak yararlı bulabileceğiniz bir dizi eklenti vardır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-312">But there are several plug-ins that you might find helpful.</span></span>
* <span data-ttu-id="2a5df-313">*HTTPS destekleniyor mu?*</span><span class="sxs-lookup"><span data-stu-id="2a5df-313">*Is HTTPS supported?*</span></span>

    <span data-ttu-id="2a5df-314">TLS 1.1 ve TLS 1.2 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-314">We support TLS 1.1 and TLS 1.2.</span></span>
* <span data-ttu-id="2a5df-315">*"Web testleri" ve "kullanılabilirlik testleri" arasında bir fark var mı?*</span><span class="sxs-lookup"><span data-stu-id="2a5df-315">*Is there a difference between "web tests" and "availability tests"?*</span></span>

    <span data-ttu-id="2a5df-316">Merhaba iki terimi birbirlerinin yerine başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="2a5df-316">hello two terms may be referenced interchangeably.</span></span> <span data-ttu-id="2a5df-317">Kullanılabilirlik testleri olduğu hello tek URL PING daha genel bir terim ayrıca toohello çok adımlı web testleri test eder.</span><span class="sxs-lookup"><span data-stu-id="2a5df-317">Availability tests is a more generic term that includes hello single URL ping tests in addition toohello multi-step web tests.</span></span>
* <span data-ttu-id="2a5df-318">*Toouse kullanılabilirlik testleri üzerinde bir güvenlik duvarının arkasında çalışan kendi dahili sunucumuzda ister.*</span><span class="sxs-lookup"><span data-stu-id="2a5df-318">*I'd like toouse availability tests on our internal server that runs behind a firewall.*</span></span>

    <span data-ttu-id="2a5df-319">İki olası çözümü vardır:</span><span class="sxs-lookup"><span data-stu-id="2a5df-319">There are two possible solutions:</span></span>
    
    * <span data-ttu-id="2a5df-320">Güvenlik Duvarı, toopermit gelen istekleri hello gelen yapılandırma [web hizmetlerimizi IP adreslerini test aracılarını](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="2a5df-320">Configure your firewall toopermit incoming requests from hello [IP addresses of our web test agents](app-insights-ip-addresses.md).</span></span>
    * <span data-ttu-id="2a5df-321">Kendi kod tooperiodically test iç sunucunuz yazma.</span><span class="sxs-lookup"><span data-stu-id="2a5df-321">Write your own code tooperiodically test your internal server.</span></span> <span data-ttu-id="2a5df-322">Merhaba kodu arka plan işlemi olarak, güvenlik duvarının arkasındaki bir test sunucusunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2a5df-322">Run hello code as a background process on a test server behind your firewall.</span></span> <span data-ttu-id="2a5df-323">Test işleminizi sonuçlarını tooApplication Öngörüler kullanarak gönderebilirsiniz [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) hello çekirdek SDK paketi API.</span><span class="sxs-lookup"><span data-stu-id="2a5df-323">Your test process can send its results tooApplication Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in hello core SDK package.</span></span> <span data-ttu-id="2a5df-324">Bu, test sunucu toohave giden erişim toohello Application Insights alım uç nokta gerektiriyor, ancak çok daha küçük güvenlik riski gelen istekleri izin veren, hello alternatif daha.</span><span class="sxs-lookup"><span data-stu-id="2a5df-324">This requires your test server toohave outgoing access toohello Application Insights ingestion endpoint, but that is a much smaller security risk than hello alternative of permitting incoming requests.</span></span> <span data-ttu-id="2a5df-325">Merhaba sonuçları hello kullanılabilirlik web testleri dikey görünmez, ancak Analytics, arama ve ölçüm Gezgini kullanılabilirlik sonuç olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="2a5df-325">hello results will not appear in hello availability web tests blades, but appears as availability results in Analytics, Search, and Metric Explorer.</span></span>
* <span data-ttu-id="2a5df-326">*Çok adımlı web testi karşıya yüklenemiyor*</span><span class="sxs-lookup"><span data-stu-id="2a5df-326">*Uploading a multi-step web test fails*</span></span>

    <span data-ttu-id="2a5df-327">300 K boyut sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="2a5df-327">There's a size limit of 300 K.</span></span>

    <span data-ttu-id="2a5df-328">Döngüler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="2a5df-328">Loops aren't supported.</span></span>

    <span data-ttu-id="2a5df-329">Başvuruları tooother web testleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="2a5df-329">References tooother web tests aren't supported.</span></span>

    <span data-ttu-id="2a5df-330">Veri kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="2a5df-330">Data sources aren't supported.</span></span>
* <span data-ttu-id="2a5df-331">*Çok adımlı testim tamamlanmıyor*</span><span class="sxs-lookup"><span data-stu-id="2a5df-331">*My multi-step test doesn't complete*</span></span>

    <span data-ttu-id="2a5df-332">Test başına 100 istek sınırı var.</span><span class="sxs-lookup"><span data-stu-id="2a5df-332">There's a limit of 100 requests per test.</span></span>

    <span data-ttu-id="2a5df-333">iki dakikadan uzun çalışırsa hello test durdurulur.</span><span class="sxs-lookup"><span data-stu-id="2a5df-333">hello test is stopped if it runs longer than two minutes.</span></span>
* <span data-ttu-id="2a5df-334">*İstemci sertifikalarıyla testi nasıl çalıştırırım?*</span><span class="sxs-lookup"><span data-stu-id="2a5df-334">*How can I run a test with client certificates?*</span></span>

    <span data-ttu-id="2a5df-335">Üzgünüz, bunu desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="2a5df-335">We don't support that, sorry.</span></span>


## <span data-ttu-id="2a5df-336"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2a5df-336"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="2a5df-337">[Tanılama günlüklerinde arama yapma][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="2a5df-337">[Search diagnostic logs][diagnostic]</span></span>

<span data-ttu-id="2a5df-338">[Sorun giderme][qna]</span><span class="sxs-lookup"><span data-stu-id="2a5df-338">[Troubleshooting][qna]</span></span>

[<span data-ttu-id="2a5df-339">Web testi aracılarının IP adresleri</span><span class="sxs-lookup"><span data-stu-id="2a5df-339">IP addresses of web test agents</span></span>](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
