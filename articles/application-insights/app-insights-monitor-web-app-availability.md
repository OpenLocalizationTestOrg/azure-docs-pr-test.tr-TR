---
title: "Web sitelerinin kullanılabilirlik ve yanıt hızını izleme | Microsoft Docs"
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
ms.openlocfilehash: 6c7f52fc3998b0b29301206ffbc6a5a0c4134f6a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a><span data-ttu-id="423d4-104">Web sitelerinin kullanılabilirlik ve yanıt hızını izleme</span><span class="sxs-lookup"><span data-stu-id="423d4-104">Monitor availability and responsiveness of any web site</span></span>
<span data-ttu-id="423d4-105">Web uygulamanızı veya web sitenizi herhangi bir sunucuya dağıttıktan sonra kullanılabilirlik ve yanıt hızını izlemeye yönelik testler ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-105">After you've deployed your web app or web site to any server, you can set up tests to monitor its availability and responsiveness.</span></span> <span data-ttu-id="423d4-106">[Azure Application Insights](app-insights-overview.md), dünyanın her yerindeki noktalarından uygulamanıza düzenli aralıklarla web istekleri gönderir.</span><span class="sxs-lookup"><span data-stu-id="423d4-106">[Azure Application Insights](app-insights-overview.md) sends web requests to your application at regular intervals from points around the world.</span></span> <span data-ttu-id="423d4-107">Uygulamanız yanıt vermezse veya yavaş yanıt verirse sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="423d4-107">It alerts you if your application doesn't respond, or responds slowly.</span></span>

<span data-ttu-id="423d4-108">Genel İnternet'ten erişilebilen herhangi bir HTTP veya HTTPS uç noktası için kullanılabilirlik testleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-108">You can set up availability tests for any HTTP or HTTPS endpoint that is accessible from the public internet.</span></span> <span data-ttu-id="423d4-109">Test ettiğiniz web sitesine eklemeniz gereken bir şey yoktur.</span><span class="sxs-lookup"><span data-stu-id="423d4-109">You don't have to add anything to the web site you're testing.</span></span> <span data-ttu-id="423d4-110">Kendi siteniz olması bile gerekmez. Kullandığınız bir REST API hizmetini test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-110">It doesn't even have to be your site: you could test a REST API service on which you depend.</span></span>

<span data-ttu-id="423d4-111">İki tür kullanılabilirlik testi vardır:</span><span class="sxs-lookup"><span data-stu-id="423d4-111">There are two types of availability tests:</span></span>

* <span data-ttu-id="423d4-112">[URL ping testi](#create): Azure portalında oluşturabileceğiniz basit bir test.</span><span class="sxs-lookup"><span data-stu-id="423d4-112">[URL ping test](#create): a simple test that you can create in the Azure portal.</span></span>
* <span data-ttu-id="423d4-113">[Çok adımlı web testi](#multi-step-web-tests): Visual Studio Enterprise’da oluşturup portala yüklediğiniz test.</span><span class="sxs-lookup"><span data-stu-id="423d4-113">[Multi-step web test](#multi-step-web-tests): which you create in Visual Studio Enterprise and upload to the portal.</span></span>

<span data-ttu-id="423d4-114">Her uygulama kaynağı için 25’e kadar kullanılabilirlik testi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-114">You can create up to 25 availability tests per application resource.</span></span>

## <span data-ttu-id="423d4-115"><a name="create"></a>1. Kullanılabilirlik testi raporlarınız için kaynak açma</span><span class="sxs-lookup"><span data-stu-id="423d4-115"><a name="create"></a>1. Open a resource for your availability test reports</span></span>

<span data-ttu-id="423d4-116">Web uygulamanız için **Application Insights’ı zaten yapılandırdıysanız**, Application Insights kaynağını [Azure portalında](https://portal.azure.com) açın.</span><span class="sxs-lookup"><span data-stu-id="423d4-116">**If you have already configured Application Insights** for your web app, open its Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="423d4-117">**Veya raporlarınızı yeni bir kaynakta görmek istiyorsanız,** [Microsoft Azure](http://azure.com)’a kaydolun, [Azure portalı](https://portal.azure.com)’na gidin ve bir Application Insights kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="423d4-117">**Or, if you want to see your reports in a new resource,** sign up to [Microsoft Azure](http://azure.com), go to the [Azure portal](https://portal.azure.com), and create an Application Insights resource.</span></span>

![Yeni > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

<span data-ttu-id="423d4-119">Yeni kaynağa ait Genel Bakış dikey penceresini açmak için **Tüm kaynaklar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-119">Click **All resources** to open the Overview blade for the new resource.</span></span>

## <span data-ttu-id="423d4-120"><a name="setup"></a>2. URL ping testi oluşturma</span><span class="sxs-lookup"><span data-stu-id="423d4-120"><a name="setup"></a>2. Create a URL ping test</span></span>
<span data-ttu-id="423d4-121">Kullanılabilirlik dikey penceresini açın ve bir kullanılabilirlik testi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-121">Open the Availability blade and add a test.</span></span>

![En azından web sitenizin URL'sini doldurma](./media/app-insights-monitor-web-app-availability/13-availability.png)

* <span data-ttu-id="423d4-123">**URL**, test etmek istediğiniz herhangi bir web sayfası olabilir, ancak ortak İnternet’te görünür olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-123">**The URL** can be any web page you want to test, but it must be visible from the public internet.</span></span> <span data-ttu-id="423d4-124">URL bir sorgu dizesi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-124">The URL can include a query string.</span></span> <span data-ttu-id="423d4-125">Bu nedenle, örneğin, veritabanınızla biraz alıştırma yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-125">So, for example, you can exercise your database a little.</span></span> <span data-ttu-id="423d4-126">URL yeniden yönlendirme adresine çözümlenirse, en fazla 10 yeniden yönlendirmeyi izleriz.</span><span class="sxs-lookup"><span data-stu-id="423d4-126">If the URL resolves to a redirect, we follow it up to 10 redirects.</span></span>
* <span data-ttu-id="423d4-127">**Bağımlı istekleri ayrıştır**: Bu seçenek işaretlenirse test, test kapsamındaki web sitesine ait görüntü, betik, stil dosyaları ve diğer dosyaları ister.</span><span class="sxs-lookup"><span data-stu-id="423d4-127">**Parse dependent requests**: If this option is checked, the test requests images, scripts, style files, and other files that are part of the web page under test.</span></span> <span data-ttu-id="423d4-128">Kayıtlı yanıt süresi, bu dosyaları almak için geçen süreyi içerir.</span><span class="sxs-lookup"><span data-stu-id="423d4-128">The recorded response time includes the time taken to get these files.</span></span> <span data-ttu-id="423d4-129">Testin tamamının zaman aşımı süresi içinde tüm bu kaynaklar sorunsuz yüklenemezse, test başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="423d4-129">The test fails if all these resources cannot be successfully downloaded within the timeout for the whole test.</span></span> 

    <span data-ttu-id="423d4-130">Seçenek işaretlenmezse, test yalnızca belirttiğiniz URL’deki dosyayı ister.</span><span class="sxs-lookup"><span data-stu-id="423d4-130">If the option is not checked, the test only requests the file at the URL you specified.</span></span>
* <span data-ttu-id="423d4-131">**Yeniden denemeyi etkinleştir**: Bu seçenek işaretlenirse, test başarısız olduğunda kısa bir süre sonra yeniden denenir.</span><span class="sxs-lookup"><span data-stu-id="423d4-131">**Enable retries**:  If this option is checked, when the test fails, it is retried after a short interval.</span></span> <span data-ttu-id="423d4-132">Art arda üç deneme başarısız olursa bir hata bildirilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-132">A failure is reported only if three successive attempts fail.</span></span> <span data-ttu-id="423d4-133">Sonraki testler bundan sonra her zamanki test sıklığında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-133">Subsequent tests are then performed at the usual test frequency.</span></span> <span data-ttu-id="423d4-134">Bir sonraki başarılı olana kadar yeniden deneme geçici olarak askıya alınır.</span><span class="sxs-lookup"><span data-stu-id="423d4-134">Retry is temporarily suspended until the next success.</span></span> <span data-ttu-id="423d4-135">Bu kural her test konuma bağımsız olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="423d4-135">This rule is applied independently at each test location.</span></span> <span data-ttu-id="423d4-136">Bu ayar önerilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-136">We recommend this option.</span></span> <span data-ttu-id="423d4-137">Ortalama olarak hataların yaklaşık %80’i yeniden deneme sırasında kaybolur.</span><span class="sxs-lookup"><span data-stu-id="423d4-137">On average, about 80% of failures disappear on retry.</span></span>
* <span data-ttu-id="423d4-138">**Test sıklığı**: Her test konumdan testin ne sıklıkta çalıştırılacağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="423d4-138">**Test frequency**: Sets how often the test is run from each test location.</span></span> <span data-ttu-id="423d4-139">Beş dakikalık sıklığında ve beş test konumuyla, siteniz ortalama olarak dakikada bir test edilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-139">With a frequency of five minutes and five test locations, your site is tested on average every minute.</span></span>
* <span data-ttu-id="423d4-140">**Test konumları**, sunucularımızın URL’nize web istekleri gönderdiği yerlerdir.</span><span class="sxs-lookup"><span data-stu-id="423d4-140">**Test locations** are the places from where our servers send web requests to your URL.</span></span> <span data-ttu-id="423d4-141">Bir konumdan fazla seçin; böylece, web sitenizdeki ağ sorunlarını ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-141">Choose more than one so that you can distinguish problems in your website from network issues.</span></span> <span data-ttu-id="423d4-142">En fazla 16 konum seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-142">You can select up to 16 locations.</span></span>
* <span data-ttu-id="423d4-143">**Başarı ölçütleri**:</span><span class="sxs-lookup"><span data-stu-id="423d4-143">**Success criteria**:</span></span>

    <span data-ttu-id="423d4-144">**Test zaman aşımı**: Yavaş yanıtlar hakkında uyarı almak için bu değeri azaltın.</span><span class="sxs-lookup"><span data-stu-id="423d4-144">**Test timeout**: Decrease this value to be alerted about slow responses.</span></span> <span data-ttu-id="423d4-145">Yanıtlar sitenizden bu süre içinde alınmadıysa test başarısız sayılır.</span><span class="sxs-lookup"><span data-stu-id="423d4-145">The test is counted as a failure if the responses from your site have not been received within this period.</span></span> <span data-ttu-id="423d4-146">**Bağımlı istekleri ayrıştır**’ı seçtiyseniz; tüm görüntüler, stil dosyaları, betikler ve diğer bağımlı kaynaklar bu süre içinde alınmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-146">If you selected **Parse dependent requests**, then all the images, style files, scripts, and other dependent resources must have been received within this period.</span></span>

    <span data-ttu-id="423d4-147">**HTTP yanıtı**: Başarılı sayılan döndürüldü durum kodu.</span><span class="sxs-lookup"><span data-stu-id="423d4-147">**HTTP response**: The returned status code that is counted as a success.</span></span> <span data-ttu-id="423d4-148">200, normal web sayfası döndürüldüğünü belirten koddur.</span><span class="sxs-lookup"><span data-stu-id="423d4-148">200 is the code that indicates that a normal web page has been returned.</span></span>

    <span data-ttu-id="423d4-149">**İçerik eşleşmesi**: "Hoş geldiniz!" gibi bir dize.</span><span class="sxs-lookup"><span data-stu-id="423d4-149">**Content match**: a string, like "Welcome!"</span></span> <span data-ttu-id="423d4-150">Her yanıtta büyük küçük harfe duyarlı bir tam eşleşme oluştuğunu test edebiliriz.</span><span class="sxs-lookup"><span data-stu-id="423d4-150">We test that an exact case-sensitive match occurs in every response.</span></span> <span data-ttu-id="423d4-151">Joker karakter bulunmayan düz bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-151">It must be a plain string, without wildcards.</span></span> <span data-ttu-id="423d4-152">Sayfanızın içeriği değişirse bunu güncelleştirmeniz gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-152">Don't forget that if your page content changes you might have to update it.</span></span>
* <span data-ttu-id="423d4-153">**Uyarılar**, varsayılan olarak, beş dakikayı geçen bir sürede üç konumda hata varsa size gönderilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-153">**Alerts** are, by default, sent to you if there are failures in three locations over five minutes.</span></span> <span data-ttu-id="423d4-154">Tek konumdaki hata daha çok bir ağ sorunudur, sitenizle ilgili değildir.</span><span class="sxs-lookup"><span data-stu-id="423d4-154">A failure in one location is likely to be a network problem, and not a problem with your site.</span></span> <span data-ttu-id="423d4-155">Ancak, eşiği daha fazla veya daha az hassas olarak değiştirebilirsiniz; size kimlerin e-posta göndermesi gerektiğini de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-155">But you can change the threshold to be more or less sensitive, and you can also change who the emails should be sent to.</span></span>

    <span data-ttu-id="423d4-156">Bir uyarı ortaya çıktığında çağrılan bir [web kancası](../monitoring-and-diagnostics/insights-webhooks-alerts.md) ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-156">You can set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span> <span data-ttu-id="423d4-157">(Ancak şu anda sorgu parametreleri Özellikler aracılığıyla geçirilmez.)</span><span class="sxs-lookup"><span data-stu-id="423d4-157">(But note that, at present, query parameters are not passed through as Properties.)</span></span>

### <a name="test-more-urls"></a><span data-ttu-id="423d4-158">Daha fazla URL test etme</span><span class="sxs-lookup"><span data-stu-id="423d4-158">Test more URLs</span></span>
<span data-ttu-id="423d4-159">Daha fazla test ekleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-159">Add more tests.</span></span> <span data-ttu-id="423d4-160">Örneğin, giriş sayfanızın test edilmesine ek olarak arama URL’sini de test ederek veritabanınızın çalıştığından emin olursunuz.</span><span class="sxs-lookup"><span data-stu-id="423d4-160">For example, In addition to testing your home page, you can make sure your database is running by testing the URL for a search.</span></span>


## <span data-ttu-id="423d4-161"><a name="monitor"></a>3. Kullanılabilirlik testi sonuçlarınızı görme</span><span class="sxs-lookup"><span data-stu-id="423d4-161"><a name="monitor"></a>3. See your availability test results</span></span>

<span data-ttu-id="423d4-162">Birkaç dakika sonra, test sonuçlarını görmek için **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-162">After a few minutes, click **Refresh** to see test results.</span></span> 

![Giriş dikey penceresinde özet sonuçları](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

<span data-ttu-id="423d4-164">Dağılım grafiği, tanılama testi adım ayrıntılarını içeren örnek test sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="423d4-164">The scatterplot shows samples of the test results that have diagnostic test-step detail in them.</span></span> <span data-ttu-id="423d4-165">Test altyapısı, hata içeren testler için tanılama ayrıntılarını depolar.</span><span class="sxs-lookup"><span data-stu-id="423d4-165">The test engine stores diagnostic detail for tests that have failures.</span></span> <span data-ttu-id="423d4-166">Başarılı testlerde, yürütmelerin bir alt kümesi için tanılama ayrıntıları depolanır.</span><span class="sxs-lookup"><span data-stu-id="423d4-166">For successful tests, diagnostic details are stored for a subset of the executions.</span></span> <span data-ttu-id="423d4-167">Test zaman damgası, test süresi, konum ve test adını görmek için yeşil/kırmızı noktalardan herhangi birinin üzerine gelin.</span><span class="sxs-lookup"><span data-stu-id="423d4-167">Hover over any of the green/red dots to see the test timestamp, test duration, location, and test name.</span></span> <span data-ttu-id="423d4-168">Test sonucunun ayrıntılarını görmek için dağılım grafiğinde noktalara tıklayarak gezinin.</span><span class="sxs-lookup"><span data-stu-id="423d4-168">Click through any dot in the scatter plot to see the details of the test result.</span></span>  

<span data-ttu-id="423d4-169">Belirli bir testi veya konumu seçin ya da ilgilendiğiniz dönemle ilgili daha fazla sonuç görmek için zaman dilimini küçültün.</span><span class="sxs-lookup"><span data-stu-id="423d4-169">Select a particular test, location, or reduce the time period to see more results around the time period of interest.</span></span> <span data-ttu-id="423d4-170">Arama Gezgini’ni kullanarak tüm yürütmelerden alınan sonuçları görün veya Analytics sorgularını kullanarak bu veriler üzerinde özel raporlar çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="423d4-170">Use Search Explorer to see results from all executions, or use Analytics queries to run custom reports on this data.</span></span>

<span data-ttu-id="423d4-171">Ölçüm Gezgini’nde ham sonuçlara ek olarak iki Kullanılabilirlik ölçümü vardır:</span><span class="sxs-lookup"><span data-stu-id="423d4-171">In addition to the raw results, there are two Availability metrics in Metrics Explorer:</span></span> 

1. <span data-ttu-id="423d4-172">Kullanılabilirlik: Tüm test yürütmelerinde başarılı olan testlerin yüzdelik oranı.</span><span class="sxs-lookup"><span data-stu-id="423d4-172">Availability: Percentage of the tests that were successful, across all test executions.</span></span> 
2. <span data-ttu-id="423d4-173">Test Süresi: Tüm test yürütmelerinde ortalama test süresi.</span><span class="sxs-lookup"><span data-stu-id="423d4-173">Test Duration: Average test duration across all test executions.</span></span>

<span data-ttu-id="423d4-174">Belirli bir testin ve/veya konumun eğilimlerini analiz etmek için test adına ve konumuna göre filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-174">You can apply filters on the test name, location to analyze trends of a particular test and/or location.</span></span>

## <span data-ttu-id="423d4-175"><a name="edit"></a> Testleri inceleme ve düzenleme</span><span class="sxs-lookup"><span data-stu-id="423d4-175"><a name="edit"></a> Inspect and edit tests</span></span>

<span data-ttu-id="423d4-176">Özet sayfasından belirli bir test seçin.</span><span class="sxs-lookup"><span data-stu-id="423d4-176">From the summary page, select a specific test.</span></span> <span data-ttu-id="423d4-177">Burada özel sonuçları görebilir ve düzenleyebilir ya da geçici olarak devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-177">There, you can see its specific results, and edit or temporarily disable it.</span></span>

![Web testini düzenleme veya devre dışı bırakma](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

<span data-ttu-id="423d4-179">Hizmetinizde bakım gerçekleştirdiğiniz sırada kullanılabilirlik testlerini veya bunlarla ilişkili uyarıları devre dışı bırakmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-179">You might want to disable availability tests or the alert rules associated with them while you are performing maintenance on your service.</span></span> 

## <span data-ttu-id="423d4-180"><a name="failures"></a>Hata görürseniz</span><span class="sxs-lookup"><span data-stu-id="423d4-180"><a name="failures"></a>If you see failures</span></span>
<span data-ttu-id="423d4-181">Kırmızı noktaya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-181">Click a red dot.</span></span>

![Kırmızı noktaya tıklama](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


<span data-ttu-id="423d4-183">Bir kullanılabilirlik testi sonucundan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="423d4-183">From an availability test result, you can:</span></span>

* <span data-ttu-id="423d4-184">Sunucunuzdan alınan yanıtı denetleme.</span><span class="sxs-lookup"><span data-stu-id="423d4-184">Inspect the response received from your server.</span></span>
* <span data-ttu-id="423d4-185">Başarısız istek örneği işlenirken sunucu uygulamanız tarafından gönderilen telemetriyi açma.</span><span class="sxs-lookup"><span data-stu-id="423d4-185">Open the telemetry sent by your server app while processing the failed request instance.</span></span>
* <span data-ttu-id="423d4-186">Sorunu izlemek için bir sorunu veya iş öğesini Git’te ya da VSTS’de günlüğe kaydetme.</span><span class="sxs-lookup"><span data-stu-id="423d4-186">Log an issue or work item in Git or VSTS to track the problem.</span></span> <span data-ttu-id="423d4-187">Hata, bu olayın bir bağlantısını içerir.</span><span class="sxs-lookup"><span data-stu-id="423d4-187">The bug will contain a link to this event.</span></span>
* <span data-ttu-id="423d4-188">Web testi sonucunu Visual Studio’da açın.</span><span class="sxs-lookup"><span data-stu-id="423d4-188">Open the web test result in Visual Studio.</span></span>


<span data-ttu-id="423d4-189">*Sorunsuz görünüyor ancak hata olarak mı bildiriliyor?*</span><span class="sxs-lookup"><span data-stu-id="423d4-189">*Looks OK but reported as a failure?*</span></span> <span data-ttu-id="423d4-190">Tüm görüntüleri, betikleri, stil sayfalarını ve sayfa tarafından yüklenen diğer dosyaları denetleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-190">Check all the images, scripts, style sheets, and any other files loaded by the page.</span></span> <span data-ttu-id="423d4-191">Herhangi biri başarısızsa, ana html sayfası Tamam olarak yüklense bile test başarısız olarak raporlanır.</span><span class="sxs-lookup"><span data-stu-id="423d4-191">If any of them fails, the test is reported as failed, even if the main html page loads OK.</span></span>

<span data-ttu-id="423d4-192">*İlgili öğe yok mu?*</span><span class="sxs-lookup"><span data-stu-id="423d4-192">*No related items?*</span></span> <span data-ttu-id="423d4-193">Sunucu tarafı uygulamanız için Application Insights ayarlanmışsa, bunun nedeni [örnekleme](app-insights-sampling.md) işleminin devam ediyor olması olabilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-193">If you have Application Insights set up for your server-side application, that may be because [sampling](app-insights-sampling.md) is in operation.</span></span> 

## <a name="multi-step-web-tests"></a><span data-ttu-id="423d4-194">Çok adımlı web testleri</span><span class="sxs-lookup"><span data-stu-id="423d4-194">Multi-step web tests</span></span>
<span data-ttu-id="423d4-195">Bir dizi URL'nin bulunduğu bir senaryoyu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-195">You can monitor a scenario that involves a sequence of URLs.</span></span> <span data-ttu-id="423d4-196">Örneğin, bir satış web sitesi izliyorsanız, öğelerin alışveriş sepetine doğru eklendiğini test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-196">For example, if you are monitoring a sales website, you can test that adding items to the shopping cart works correctly.</span></span>

> [!NOTE] 
> <span data-ttu-id="423d4-197">Çok adımlı web testleri ücrete tabidir.</span><span class="sxs-lookup"><span data-stu-id="423d4-197">There is a charge for multi-step web tests.</span></span> <span data-ttu-id="423d4-198">[Fiyatlandırma düzeni](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="423d4-198">[Pricing scheme](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>
> 

<span data-ttu-id="423d4-199">Çok adımlı bir test oluşturmak için Visual Studio Enterprise kullanarak senaryoyu kaydedin ve kaydı Application Insights'a yükleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-199">To create a multi-step test, you record the scenario by using Visual Studio Enterprise, and then upload the recording to Application Insights.</span></span> <span data-ttu-id="423d4-200">Application Insights, senaryoyu aralıklarla yeniden yürütür ve yanıtları doğrular.</span><span class="sxs-lookup"><span data-stu-id="423d4-200">Application Insights replays the scenario at intervals and verifies the responses.</span></span>

> [!NOTE]
> <span data-ttu-id="423d4-201">Testlerinizde kodlanmış işlevler veya döngüler kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="423d4-201">You can't use coded functions or loops in your tests.</span></span> <span data-ttu-id="423d4-202">Test tamamen .webtest betiğinde yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-202">The test must be contained completely in the .webtest script.</span></span> <span data-ttu-id="423d4-203">Ancak, standart eklentiler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-203">However, you can use standard plugins.</span></span>
>

#### <a name="1-record-a-scenario"></a><span data-ttu-id="423d4-204">1. Senaryo kaydetme</span><span class="sxs-lookup"><span data-stu-id="423d4-204">1. Record a scenario</span></span>
<span data-ttu-id="423d4-205">Web oturumu kaydetmek için Visual Studio Enterprise kullanın.</span><span class="sxs-lookup"><span data-stu-id="423d4-205">Use Visual Studio Enterprise to record a web session.</span></span>

1. <span data-ttu-id="423d4-206">Web performans testi projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="423d4-206">Create a Web performance test project.</span></span>

    ![Visual Studio Enterprise sürümünde, Web Performansı ve Yük Testi şablonundan bir proje oluşturun.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * <span data-ttu-id="423d4-208">*Web Performansı ve Yük Testi şablonunu görmüyor musunuz?*</span><span class="sxs-lookup"><span data-stu-id="423d4-208">*Don't see the Web Performance and Load Test template?*</span></span> <span data-ttu-id="423d4-209">- Visual Studio Enterprise’ı kapatın.</span><span class="sxs-lookup"><span data-stu-id="423d4-209">- Close Visual Studio Enterprise.</span></span> <span data-ttu-id="423d4-210">**Visual Studio Yükleyicisi**’ni açarak Visual Studio Enterprise yüklemesini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="423d4-210">Open **Visual Studio Installer** to modify your Visual Studio Enterprise installation.</span></span> <span data-ttu-id="423d4-211">**Tek Bileşenler** altında **Web Performansı ve yük testi araçları**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="423d4-211">Under **Individual Components**, select **Web Performance and load testing tools**.</span></span>

2. <span data-ttu-id="423d4-212">.webtest dosyasını açın ve kaydı başlatın.</span><span class="sxs-lookup"><span data-stu-id="423d4-212">Open the .webtest file and start recording.</span></span>

    ![.webtest dosyasını açın ve Kaydet’e tıklayın.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. <span data-ttu-id="423d4-214">Testinizde benzetimini yapmak istediğiniz kullanıcı işlemlerini yapın: web sitenizi açın, sepete ürün ekleyin ve bunlara devam edin.</span><span class="sxs-lookup"><span data-stu-id="423d4-214">Do the user actions you want to simulate in your test: open your website, add a product to the cart, and so on.</span></span> <span data-ttu-id="423d4-215">Sonra testinizi durdurun.</span><span class="sxs-lookup"><span data-stu-id="423d4-215">Then stop your test.</span></span>

    ![Internet Explorer'da web testi kaydedicisi çalışır.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    <span data-ttu-id="423d4-217">Uzun bir senaryo oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-217">Don't make a long scenario.</span></span> <span data-ttu-id="423d4-218">100 adımlık ve 2 dakikalık bir sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="423d4-218">There's a limit of 100 steps and 2 minutes.</span></span>
4. <span data-ttu-id="423d4-219">Testi düzenleme nedenleri:</span><span class="sxs-lookup"><span data-stu-id="423d4-219">Edit the test to:</span></span>

   * <span data-ttu-id="423d4-220">Alınan metin ve yanıt kodlarını denetlemek için doğrulama ekleme.</span><span class="sxs-lookup"><span data-stu-id="423d4-220">Add validations to check the received text and response codes.</span></span>
   * <span data-ttu-id="423d4-221">Gereksiz tüm etkileşimleri kaldırma.</span><span class="sxs-lookup"><span data-stu-id="423d4-221">Remove any superfluous interactions.</span></span> <span data-ttu-id="423d4-222">Ayrıca, resim veya reklam için ya da sitelerin izlenmesi için bağımlı istekleri kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-222">You could also remove dependent requests for pictures or to ad or tracking sites.</span></span>

     <span data-ttu-id="423d4-223">Yalnızca test betiğini düzenleyebildiğinizi, özel kod veya başka web testlerinden çağrı ekleyemediğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-223">Remember that you can only edit the test script - you can't add custom code or call other web tests.</span></span> <span data-ttu-id="423d4-224">Testlere döngü eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-224">Don't insert loops in the test.</span></span> <span data-ttu-id="423d4-225">Standart web testi eklentileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-225">You can use standard web test plug-ins.</span></span>
5. <span data-ttu-id="423d4-226">Çalıştığından emin olmak için testi Visual Studio’da çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="423d4-226">Run the test in Visual Studio to make sure it works.</span></span>

    <span data-ttu-id="423d4-227">Web test çalıştırıcısı bir web tarayıcısı açar ve kaydettiğiniz eylemleri yineler.</span><span class="sxs-lookup"><span data-stu-id="423d4-227">The web test runner opens a web browser and repeats the actions you recorded.</span></span> <span data-ttu-id="423d4-228">Beklediğiniz gibi çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="423d4-228">Make sure it works as you expect.</span></span>

    ![Visual Studio’da .webtest dosyasını açın ve Çalıştır’a tıklayın.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-the-web-test-to-application-insights"></a><span data-ttu-id="423d4-230">2. Web testi Application Insights'a yükleme</span><span class="sxs-lookup"><span data-stu-id="423d4-230">2. Upload the web test to Application Insights</span></span>
1. <span data-ttu-id="423d4-231">Application Insights portalında bir web testi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="423d4-231">In the Application Insights portal, create a web test.</span></span>

    ![Web testleri dikey penceresinde Ekle'yi seçin.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. <span data-ttu-id="423d4-233">Çok adımlı testi seçip .webtest dosyasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-233">Select multi-step test, and upload the .webtest file.</span></span>

    ![Çok adımlı web testini seçin.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    <span data-ttu-id="423d4-235">Test konumları, sıklığı ve uyarı parametrelerini aynı ping testlerinde olduğu gibi aynı şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-235">Set the test locations, frequency, and alert parameters in the same way as for ping tests.</span></span>

#### <a name="3-see-the-results"></a><span data-ttu-id="423d4-236">3. Sonuçları görme</span><span class="sxs-lookup"><span data-stu-id="423d4-236">3. See the results</span></span>

<span data-ttu-id="423d4-237">Tek url testlerinde olduğu gibi test sonuçlarını ve hatalarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-237">View your test results and any failures in the same way as single-url tests.</span></span>

<span data-ttu-id="423d4-238">Ayrıca, test sonuçlarını indirerek Visual Studio’da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-238">In addition, you can download the test results to view them in Visual Studio.</span></span>

#### <a name="too-many-failures"></a><span data-ttu-id="423d4-239">Çok fazla hata mı var?</span><span class="sxs-lookup"><span data-stu-id="423d4-239">Too many failures?</span></span>

* <span data-ttu-id="423d4-240">Yaygın bir başarısızlık nedeni testin çok uzun çalışmasıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-240">A common reason for failure is that the test runs too long.</span></span> <span data-ttu-id="423d4-241">İki dakikadan uzun çalıştırılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-241">It mustn't run longer than two minutes.</span></span>

* <span data-ttu-id="423d4-242">Betikler, stil sayfaları, görüntüler ve diğerleri de dahil olmak üzere, testin başarılı olması için sayfanın tüm kaynaklarının doğru yüklenmiş olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-242">Don't forget that all the resources of a page must load correctly for the test to succeed, including scripts, style sheets, images, and so forth.</span></span>

* <span data-ttu-id="423d4-243">Web testi tamamen .webtest dosyasında olmalıdır: Testte kodlanmış işlevleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="423d4-243">The web test must be entirely contained in the .webtest script: you can't use coded functions in the test.</span></span>

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a><span data-ttu-id="423d4-244">Çok adımlı testinizde bağlı kalma süresi ve rasgele rakamlar</span><span class="sxs-lookup"><span data-stu-id="423d4-244">Plugging time and random numbers into your multi-step test</span></span>
<span data-ttu-id="423d4-245">Dış bir kaynağa ait stoklar gibi zamana bağımlı veriler alan bir aracı test ettiğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="423d4-245">Suppose you're testing a tool that gets time-dependent data such as stocks from an external feed.</span></span> <span data-ttu-id="423d4-246">Web testinizi kaydettiğinizde, belirli zamanları kullanmanız gerekse de, bunları testin parametreleri (StartTime ve EndTime) olarak ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="423d4-246">When you record your web test, you have to use specific times, but you set them as parameters of the test, StartTime and EndTime.</span></span>

![Parametrelere sahip web testi.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

<span data-ttu-id="423d4-248">Testi çalıştırdığınızda, EndTime her zaman geçerli zaman, StartTime da 15 dakika öncesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-248">When you run the test, you'd like EndTime always to be the present time, and StartTime should be 15 minutes ago.</span></span>

<span data-ttu-id="423d4-249">Web Testi Eklentileri, zamanları parametreleme yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="423d4-249">Web Test Plug-ins provide the way to do parameterize times.</span></span>

1. <span data-ttu-id="423d4-250">İstediğiniz her değişken parametre değeri için bir web testi eklentisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-250">Add a web test plug-in for each variable parameter value you want.</span></span> <span data-ttu-id="423d4-251">Web testi araç çubuğunda, **Web Testi Eklentisi Ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="423d4-251">In the web test toolbar, choose **Add Web Test Plugin**.</span></span>

    ![Web Testi Eklentisi Ekle’yi, sonra da bir türü seçin.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    <span data-ttu-id="423d4-253">Bu örnekte, Tarih Saat Eklentisinin iki örneğini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="423d4-253">In this example, we use two instances of the Date Time Plug-in.</span></span> <span data-ttu-id="423d4-254">Bir örnek "15 dakika önce" için, bir örnek de "şimdi" için.</span><span class="sxs-lookup"><span data-stu-id="423d4-254">One instance is for "15 minutes ago" and another for "now."</span></span>
2. <span data-ttu-id="423d4-255">Her eklentinin özelliklerini açın.</span><span class="sxs-lookup"><span data-stu-id="423d4-255">Open the properties of each plug-in.</span></span> <span data-ttu-id="423d4-256">Buna bir ad verip geçerli saat olarak kullanılmak üzere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-256">Give it a name and set it to use the current time.</span></span> <span data-ttu-id="423d4-257">Bunlardan birini Dakika Ekle = 15 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-257">For one of them, set Add Minutes = -15.</span></span>

    ![Adı, Geçerli Saati Kullan’ı ve Dakika Ekle’yi ayarlayın.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. <span data-ttu-id="423d4-259">Web testi parametrelerinde, eklenti adına başvurmak için {{plug-in name}} kullanın.</span><span class="sxs-lookup"><span data-stu-id="423d4-259">In the web test parameters, use {{plug-in name}} to reference a plug-in name.</span></span>

    ![Test parametresinde {{plug-in name}} kullanın.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

<span data-ttu-id="423d4-261">Artık testi portala yükleyin.</span><span class="sxs-lookup"><span data-stu-id="423d4-261">Now, upload your test to the portal.</span></span> <span data-ttu-id="423d4-262">Testin her çalıştırılışında dinamik değerler kullanılır.</span><span class="sxs-lookup"><span data-stu-id="423d4-262">It uses the dynamic values on every run of the test.</span></span>

## <a name="dealing-with-sign-in"></a><span data-ttu-id="423d4-263">Oturum açmayla ilgilenme</span><span class="sxs-lookup"><span data-stu-id="423d4-263">Dealing with sign-in</span></span>
<span data-ttu-id="423d4-264">Kullanıcılarınız uygulamanızda oturum açarsa, oturum açma benzetimi için bir dizi seçeneğiniz vardır; böylece, oturum açmanın ötesinde sayfaları test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-264">If your users sign in to your app, you have various options for simulating sign-in so that you can test pages behind the sign-in.</span></span> <span data-ttu-id="423d4-265">Kullandığınız yaklaşım, uygulamanın sağladığı güvenlik türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-265">The approach you use depends on the type of security provided by the app.</span></span>

<span data-ttu-id="423d4-266">Her durumda, uygulamanızda yalnızca test amacıyla bir hesap oluşturmalısınız.</span><span class="sxs-lookup"><span data-stu-id="423d4-266">In all cases, you should create an account in your application just for the purpose of testing.</span></span> <span data-ttu-id="423d4-267">Mümkünse, web testlerinin gerçek kullanıcıları etkileme olasılığını önlemek için test hesabının izinlerini kısıtlayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-267">If possible, restrict the permissions of this test account so that there's no possibility of the web tests affecting real users.</span></span>

### <a name="simple-username-and-password"></a><span data-ttu-id="423d4-268">Basit kullanıcı adı ve parola</span><span class="sxs-lookup"><span data-stu-id="423d4-268">Simple username and password</span></span>
<span data-ttu-id="423d4-269">Web testini normal şekilde kaydedin.</span><span class="sxs-lookup"><span data-stu-id="423d4-269">Record a web test in the usual way.</span></span> <span data-ttu-id="423d4-270">Önce tanımlama bilgilerini silin.</span><span class="sxs-lookup"><span data-stu-id="423d4-270">Delete cookies first.</span></span>

### <a name="saml-authentication"></a><span data-ttu-id="423d4-271">SAML kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="423d4-271">SAML authentication</span></span>
<span data-ttu-id="423d4-272">Web testlerinde kullanıma uygun SAML eklentisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="423d4-272">Use the SAML plugin that is available for web tests.</span></span>

### <a name="client-secret"></a><span data-ttu-id="423d4-273">Gizli anahtar</span><span class="sxs-lookup"><span data-stu-id="423d4-273">Client secret</span></span>
<span data-ttu-id="423d4-274">Uygulamanızda gizli anahtar içeren bir oturum açma yolu varsa bu yolu kullanın.</span><span class="sxs-lookup"><span data-stu-id="423d4-274">If your app has a sign-in route that involves a client secret, use that route.</span></span> <span data-ttu-id="423d4-275">Azure Active Directory (AAD), gizli anahtarla oturum açmayı sağlayan bir hizmet örneğidir.</span><span class="sxs-lookup"><span data-stu-id="423d4-275">Azure Active Directory (AAD) is an example of a service that provides a client secret sign-in.</span></span> <span data-ttu-id="423d4-276">AAD’de gizli anahtar, Uygulama Anahtarı’dır.</span><span class="sxs-lookup"><span data-stu-id="423d4-276">In AAD, the client secret is the App Key.</span></span>

<span data-ttu-id="423d4-277">Aşağıda uygulama anahtarı kullanan bir Azure web uygulaması için web testi örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="423d4-277">Here's a sample web test of an Azure web app using an app key:</span></span>

![Gizli anahtar örneği](./media/app-insights-monitor-web-app-availability/110.png)

1. <span data-ttu-id="423d4-279">Gizli anahtar (AppKey) kullanarak AAD’den belirteç alın.</span><span class="sxs-lookup"><span data-stu-id="423d4-279">Get token from AAD using client secret (AppKey).</span></span>
2. <span data-ttu-id="423d4-280">Yanıttan taşıyıcı belirteci ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-280">Extract bearer token from response.</span></span>
3. <span data-ttu-id="423d4-281">Yetkilendirme üst bilgisinde taşıyıcı belirteç kullanarak API çağırın.</span><span class="sxs-lookup"><span data-stu-id="423d4-281">Call API using bearer token in the authorization header.</span></span>

<span data-ttu-id="423d4-282">Web testinin gerçek bir istemci olduğundan, yani AAD’de kendi uygulamasına sahip olduğundan emin olun ve bu istemcinin clientId’si ile appkey’ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="423d4-282">Make sure that the web test is an actual client - that is, it has its own app in AAD - and use its clientId + appkey.</span></span> <span data-ttu-id="423d4-283">Test edilen hizmetiniz, AAD içinde kendi uygulamasına sahiptir: bu uygulamanın appID URI’si, web testinin “kaynak” alanında yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="423d4-283">Your service under test also has its own app in AAD: the appID URI of this app is reflected in the web test in the “resource” field.</span></span>

### <a name="open-authentication"></a><span data-ttu-id="423d4-284">Açık Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="423d4-284">Open Authentication</span></span>
<span data-ttu-id="423d4-285">Microsoft veya Google hesabınızla oturum açma, bir açık kimlik doğrulaması örneğidir.</span><span class="sxs-lookup"><span data-stu-id="423d4-285">An example of open authentication is signing in with your Microsoft or Google account.</span></span> <span data-ttu-id="423d4-286">OAuth kullanan çok sayıda uygulama, alternatif gizli anahtar da sağlar; bu nedenle ilk taktiğiniz bu olasılığın incelenmesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-286">Many apps that use OAuth provide the client secret alternative, so your first tactic should be to investigate that possibility.</span></span>

<span data-ttu-id="423d4-287">Testinizde OAuth kullanılarak oturum açılması gerekiyorsa, genel yaklaşım şöyledir:</span><span class="sxs-lookup"><span data-stu-id="423d4-287">If your test must sign in using OAuth, the general approach is:</span></span>

* <span data-ttu-id="423d4-288">Web tarayıcınız, kimlik doğrulama sitesi ve uygulamanız arasındaki trafiği incelemek için Fiddler gibi bir araç kullanın.</span><span class="sxs-lookup"><span data-stu-id="423d4-288">Use a tool such as Fiddler to examine the traffic between your web browser, the authentication site, and your app.</span></span>
* <span data-ttu-id="423d4-289">Farklı makineler veya tarayıcılar kullanarak veya uzun aralıklarla (süresi dolacak şekilde belirteçleri izin vermek için) iki veya daha fazla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="423d4-289">Perform two or more sign-ins using different machines or browsers, or at long intervals (to allow tokens to expire).</span></span>
* <span data-ttu-id="423d4-290">Farklı oturumları karşılaştırarak, kimlik doğrulama sitesinden geri geçirilen belirteci tanımlayın; başka bir deyişle oturum açıldıktan sonra uygulama sunucunuza geçirilen belirteç.</span><span class="sxs-lookup"><span data-stu-id="423d4-290">By comparing different sessions, identify the token passed back from the authenticating site, that is then passed to your app server after sign-in.</span></span>
* <span data-ttu-id="423d4-291">Visual Studio’yu kullanarak web testini kaydetme</span><span class="sxs-lookup"><span data-stu-id="423d4-291">Record a web test using Visual Studio.</span></span>
* <span data-ttu-id="423d4-292">Belirteçleri parametreleyin; belirteç kimlik doğrulayıcıdan döndürüldüğünde ve sitede sorgu sırasında kullanıldığında parametre ayarı.</span><span class="sxs-lookup"><span data-stu-id="423d4-292">Parameterize the tokens, setting the parameter when the token is returned from the authenticator, and using it in the query to the site.</span></span>
  <span data-ttu-id="423d4-293">(Visual Studio testi parametrelemeyi dener, ancak belirteçleri doğru parametrelemez.)</span><span class="sxs-lookup"><span data-stu-id="423d4-293">(Visual Studio attempts to parameterize the test, but does not correctly parameterize the tokens.)</span></span>


## <a name="performance-tests"></a><span data-ttu-id="423d4-294">Performans testleri</span><span class="sxs-lookup"><span data-stu-id="423d4-294">Performance tests</span></span>
<span data-ttu-id="423d4-295">Web sitenizde bir yük testi çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-295">You can run a load test on your website.</span></span> <span data-ttu-id="423d4-296">Kullanılabilirlik testinde olduğu gibi dünyanın dört bir yanındaki noktalarımızdan basit istekler ya da çok adımlı istekler gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-296">Like the availability test, you can send either simple requests or multi-step requests from our points around the world.</span></span> <span data-ttu-id="423d4-297">Kullanılabilirlik testinden farklı olarak eşzamanlı birden fazla kullanıcıyı benzeten çok sayıda istek gönderilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-297">Unlike an availability test, many requests are sent, simulating multiple simultaneous users.</span></span>

<span data-ttu-id="423d4-298">Genel Bakış dikey penceresinde **Ayarlar**, **Performans Testleri**’ni açın.</span><span class="sxs-lookup"><span data-stu-id="423d4-298">From the Overview blade, open **Settings**, **Performance Tests**.</span></span> <span data-ttu-id="423d4-299">Bir test oluşturduğunuzda Visual Studio Team Services hesabı oluşturmaya davet edilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="423d4-299">When you create a test, you are invited to connect to or create a Visual Studio Team Services account.</span></span>

<span data-ttu-id="423d4-300">Test tamamlandığında yanıt süreleri ve başarı oranları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-300">When the test is complete, you are shown response times and success rates.</span></span>


![Performans testi](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> <span data-ttu-id="423d4-302">Performans testi etkilerini gözlemlemek için [Canlı Akış](app-insights-live-stream.md)'ı ve [Profil Oluşturucu](app-insights-profiler.md)'yu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="423d4-302">To observe the effects of a performance test, use [Live Stream](app-insights-live-stream.md) and [Profiler](app-insights-profiler.md).</span></span>
>

## <a name="automation"></a><span data-ttu-id="423d4-303">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="423d4-303">Automation</span></span>
* <span data-ttu-id="423d4-304">Otomatik olarak [kullanılabilirlik testi ayarlamak için PowerShell betiklerini kullanın](app-insights-powershell.md#add-an-availability-test).</span><span class="sxs-lookup"><span data-stu-id="423d4-304">[Use PowerShell scripts to set up an availability test](app-insights-powershell.md#add-an-availability-test) automatically.</span></span>
* <span data-ttu-id="423d4-305">Bir uyarı ortaya çıktığında çağrılan bir [web kancası](../monitoring-and-diagnostics/insights-webhooks-alerts.md) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="423d4-305">Set up a [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) that is called when an alert is raised.</span></span>

## <span data-ttu-id="423d4-306"><a name="qna"></a>Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="423d4-306"><a name="qna"></a>Questions?</span></span> <span data-ttu-id="423d4-307">Sorunlarınız mı var?</span><span class="sxs-lookup"><span data-stu-id="423d4-307">Problems?</span></span>
* <span data-ttu-id="423d4-308">*Web testimden kod çağırabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="423d4-308">*Can I call code from my web test?*</span></span>

    <span data-ttu-id="423d4-309">Hayır.</span><span class="sxs-lookup"><span data-stu-id="423d4-309">No.</span></span> <span data-ttu-id="423d4-310">Test adımları .webtest dosyasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="423d4-310">The steps of the test must be in the .webtest file.</span></span> <span data-ttu-id="423d4-311">Bu nedenle, başka web testlerini çağıramaz, döngüleri kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="423d4-311">And you can't call other web tests or use loops.</span></span> <span data-ttu-id="423d4-312">Ancak yararlı bulabileceğiniz bir dizi eklenti vardır.</span><span class="sxs-lookup"><span data-stu-id="423d4-312">But there are several plug-ins that you might find helpful.</span></span>
* <span data-ttu-id="423d4-313">*HTTPS destekleniyor mu?*</span><span class="sxs-lookup"><span data-stu-id="423d4-313">*Is HTTPS supported?*</span></span>

    <span data-ttu-id="423d4-314">TLS 1.1 ve TLS 1.2 desteklenir.</span><span class="sxs-lookup"><span data-stu-id="423d4-314">We support TLS 1.1 and TLS 1.2.</span></span>
* <span data-ttu-id="423d4-315">*"Web testleri" ve "kullanılabilirlik testleri" arasında bir fark var mı?*</span><span class="sxs-lookup"><span data-stu-id="423d4-315">*Is there a difference between "web tests" and "availability tests"?*</span></span>

    <span data-ttu-id="423d4-316">Bu iki terim birbirlerinin yerine kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-316">The two terms may be referenced interchangeably.</span></span> <span data-ttu-id="423d4-317">Kullanılabilirlik testleri, çok adımlı web testlerine ek olarak tek URL ping testlerini de içeren daha genel bir terimdir.</span><span class="sxs-lookup"><span data-stu-id="423d4-317">Availability tests is a more generic term that includes the single URL ping tests in addition to the multi-step web tests.</span></span>
* <span data-ttu-id="423d4-318">*Kullanılabilirlik testlerini, güvenlik duvarının arkasında çalışan kendi iç sunucumuzda kullanmak istiyorum.*</span><span class="sxs-lookup"><span data-stu-id="423d4-318">*I'd like to use availability tests on our internal server that runs behind a firewall.*</span></span>

    <span data-ttu-id="423d4-319">İki olası çözümü vardır:</span><span class="sxs-lookup"><span data-stu-id="423d4-319">There are two possible solutions:</span></span>
    
    * <span data-ttu-id="423d4-320">Güvenlik duvarınızı, [Web testi aracılarımızın IP adreslerinden](app-insights-ip-addresses.md) gelen isteklere izin verecek şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="423d4-320">Configure your firewall to permit incoming requests from the [IP addresses of our web test agents](app-insights-ip-addresses.md).</span></span>
    * <span data-ttu-id="423d4-321">İç sunucunuzu düzenli olarak test etmek için kendi kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="423d4-321">Write your own code to periodically test your internal server.</span></span> <span data-ttu-id="423d4-322">Kodu, güvenlik duvarınızın arkasındaki bir test sunucusunda arka plan işlemi olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="423d4-322">Run the code as a background process on a test server behind your firewall.</span></span> <span data-ttu-id="423d4-323">Test işleminiz, temel SDK paketindeki [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API’sini kullanarak sonuçları Application Insights’a gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="423d4-323">Your test process can send its results to Application Insights by using [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API in the core SDK package.</span></span> <span data-ttu-id="423d4-324">Bunun için test sunucunuzun Application Insights alım uç noktası ile giden bağlantısının olması gerekir, ancak bu, gelen isteklere izin vermeye göre çok daha küçük bir güvenlik riski oluşturur.</span><span class="sxs-lookup"><span data-stu-id="423d4-324">This requires your test server to have outgoing access to the Application Insights ingestion endpoint, but that is a much smaller security risk than the alternative of permitting incoming requests.</span></span> <span data-ttu-id="423d4-325">Sonuçlar kullanılabilirlik web testi dikey pencerelerinde görünür, ancak Analytics, Search ve Ölçüm Gezgini’nde kullanılabilirlik sonuçları olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="423d4-325">The results will not appear in the availability web tests blades, but appears as availability results in Analytics, Search, and Metric Explorer.</span></span>
* <span data-ttu-id="423d4-326">*Çok adımlı web testi karşıya yüklenemiyor*</span><span class="sxs-lookup"><span data-stu-id="423d4-326">*Uploading a multi-step web test fails*</span></span>

    <span data-ttu-id="423d4-327">300 K boyut sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="423d4-327">There's a size limit of 300 K.</span></span>

    <span data-ttu-id="423d4-328">Döngüler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="423d4-328">Loops aren't supported.</span></span>

    <span data-ttu-id="423d4-329">Başka web testlerine başvurular desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="423d4-329">References to other web tests aren't supported.</span></span>

    <span data-ttu-id="423d4-330">Veri kaynakları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="423d4-330">Data sources aren't supported.</span></span>
* <span data-ttu-id="423d4-331">*Çok adımlı testim tamamlanmıyor*</span><span class="sxs-lookup"><span data-stu-id="423d4-331">*My multi-step test doesn't complete*</span></span>

    <span data-ttu-id="423d4-332">Test başına 100 istek sınırı var.</span><span class="sxs-lookup"><span data-stu-id="423d4-332">There's a limit of 100 requests per test.</span></span>

    <span data-ttu-id="423d4-333">Test, iki dakikadan uzun çalışırsa durdurulur.</span><span class="sxs-lookup"><span data-stu-id="423d4-333">The test is stopped if it runs longer than two minutes.</span></span>
* <span data-ttu-id="423d4-334">*İstemci sertifikalarıyla testi nasıl çalıştırırım?*</span><span class="sxs-lookup"><span data-stu-id="423d4-334">*How can I run a test with client certificates?*</span></span>

    <span data-ttu-id="423d4-335">Üzgünüz, bunu desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="423d4-335">We don't support that, sorry.</span></span>


## <span data-ttu-id="423d4-336"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="423d4-336"><a name="next"></a>Next steps</span></span>
<span data-ttu-id="423d4-337">[Tanılama günlüklerinde arama yapma][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="423d4-337">[Search diagnostic logs][diagnostic]</span></span>

<span data-ttu-id="423d4-338">[Sorun giderme][qna]</span><span class="sxs-lookup"><span data-stu-id="423d4-338">[Troubleshooting][qna]</span></span>

[<span data-ttu-id="423d4-339">Web testi aracılarının IP adresleri</span><span class="sxs-lookup"><span data-stu-id="423d4-339">IP addresses of web test agents</span></span>](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
