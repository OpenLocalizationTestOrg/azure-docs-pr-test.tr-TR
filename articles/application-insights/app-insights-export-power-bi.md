---
title: Application Insights gelen aaaExport tooPower BI | Microsoft Docs
description: "Power BI'da analiz sorguları görüntülenebilir."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="7a810-103">Power BI Application Insights akış</span><span class="sxs-lookup"><span data-stu-id="7a810-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="7a810-104">[Power BI](http://www.powerbi.com/) yardımcı iş analiz araçları dizisi verileri çözümlemek ve paylaşmak Öngörüler.</span><span class="sxs-lookup"><span data-stu-id="7a810-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="7a810-105">Zengin panolar her cihazda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a810-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="7a810-106">Analytics sorgularından dahil olmak üzere pek çok kaynaktan veri birleştirebilirsiniz [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a810-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="7a810-107">Application Insights veri tooPower BI verme üç önerilen yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="7a810-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="7a810-108">Bunları ayrı olarak veya birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a810-108">You can use them separately or together.</span></span>

* <span data-ttu-id="7a810-109">[**Power BI bağdaştırıcısı** ](#power-pi-adapter) -uygulamanızdan telemetrinin bir tam Pano ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7a810-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="7a810-110">grafikler Hello dizi önceden tanımlanmış ancak kendi sorgularınızı diğer kaynaklardan gelen ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a810-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="7a810-111">[**Analitik sorguları dışarı** ](#export-analytics-queries) -herhangi bir yazma analizi kullanarak istediğiniz ve tooPower BI verme sorgu.</span><span class="sxs-lookup"><span data-stu-id="7a810-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="7a810-112">Bu sorgu, diğer verilerin bir Panoda yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a810-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="7a810-113">[**Sürekli dışarı aktarma ve akış analizi** ](app-insights-export-stream-analytics.md) -bu yukarı daha fazla iş tooset içerir.</span><span class="sxs-lookup"><span data-stu-id="7a810-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="7a810-114">Uzun süre boyunca, verilerinizi tookeep istiyorsanız kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="7a810-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="7a810-115">Aksi takdirde hello diğer yöntemleri önerilir.</span><span class="sxs-lookup"><span data-stu-id="7a810-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="7a810-116">Power BI bağdaştırıcısı</span><span class="sxs-lookup"><span data-stu-id="7a810-116">Power BI adapter</span></span>
<span data-ttu-id="7a810-117">Bu yöntem telemetri tam bir Pano oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a810-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="7a810-118">Merhaba ilk veri kümesi önceden, ancak daha fazla veri tooit ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a810-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="7a810-119">Merhaba bağdaştırıcısı Al</span><span class="sxs-lookup"><span data-stu-id="7a810-119">Get hello adapter</span></span>
1. <span data-ttu-id="7a810-120">Çok oturum[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="7a810-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="7a810-121">Açık **veri alma**, **Hizmetleri**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="7a810-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Application Insights veri kaynağından veri alın](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="7a810-123">Application Insights kaynağınıza Hello ayrıntılarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="7a810-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Application Insights veri kaynağından veri alın](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="7a810-125">Bir veya iki içeri hello veri toobe için dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7a810-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Power BI bağdaştırıcısı](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="7a810-127">Merhaba Application Insights grafikleri olanla diğer kaynakları ve analiz sorguları birleştirme hello panoyu düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a810-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="7a810-128">Burada, daha fazla grafik alabilirsiniz ve her bir grafik ayarlayabileceğiniz bir parametre yok görselleştirme galeri yoktur.</span><span class="sxs-lookup"><span data-stu-id="7a810-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="7a810-129">Merhaba sonra ilk alma, hello Pano ve hello raporları tooupdate günlük devam eder.</span><span class="sxs-lookup"><span data-stu-id="7a810-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="7a810-130">Merhaba Yenileme zamanlaması hello veri kümesi üzerinde kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a810-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="7a810-131">Analitik sorguları dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="7a810-131">Export Analytics queries</span></span>
<span data-ttu-id="7a810-132">Bu yol toowrite sağlayan herhangi Analytics sorgu ister ve bu tooa Power BI panosuna dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="7a810-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="7a810-133">(Merhaba bağdaştırıcısı tarafından oluşturulan toohello Panoda ekleyebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="7a810-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="7a810-134">Bir kez: Power BI Desktop yükleyin</span><span class="sxs-lookup"><span data-stu-id="7a810-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="7a810-135">tooimport Application Insights sorgunuzu hello Power BI Masaüstü sürümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a810-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="7a810-136">Ancak daha sonra onu toohello web veya tooyour Power BI bulut çalışma yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a810-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="7a810-137">Yükleme [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="7a810-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="7a810-138">Analytics sorgusu dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="7a810-138">Export an Analytics query</span></span>
1. <span data-ttu-id="7a810-139">[Analytics açın ve sorgunuzu yazma](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="7a810-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="7a810-140">Test ve hello Sonuçlardan memnun kaldıysanız kadar hello sorgu daraltın.</span><span class="sxs-lookup"><span data-stu-id="7a810-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="7a810-141">**Merhaba sorgulayan çalıştırır doğru önce analytics'te dışa emin olun.**</span><span class="sxs-lookup"><span data-stu-id="7a810-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="7a810-142">Merhaba üzerinde **verme** menüsünde seçin **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="7a810-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="7a810-143">Merhaba metin dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7a810-143">Save hello text file.</span></span>
   
    ![Power BI sorgu verme](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="7a810-145">Power BI Desktop seçin **Veri Al, boş sorgu** ve hello Düzenleyicisi altında sorgu **Görünüm** seçin **Gelişmiş sorgu düzenleyici**.</span><span class="sxs-lookup"><span data-stu-id="7a810-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="7a810-146">İçine yapıştırma dışarı hello M Dil komut dosyası hello Gelişmiş Sorgu Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="7a810-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Gelişmiş Sorgu Düzenleyici](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="7a810-148">Tooprovide kimlik bilgileri tooallow Power BI tooaccess Azure olabilir.</span><span class="sxs-lookup"><span data-stu-id="7a810-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="7a810-149">Microsoft hesabınızla 'kuruluş hesabı' toosign kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a810-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Application Insights sorgunuzu Azure kimlik tooenable Power BI toorun sağlayın](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="7a810-151">(Tooverify hello kimlik bilgileri gerekiyorsa, hello veri kaynağı ayarları menü komutu hello sorgu Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a810-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="7a810-152">Power BI için kimlik bilgilerinizi farklı olabilir Azure için kullandığınız toospecify hello kimlik özen.)</span><span class="sxs-lookup"><span data-stu-id="7a810-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="7a810-153">Sorgunuz için bir görsel öğe seçin ve x ekseni, y ekseni ve boyut kesimlere hello alanları seçin.</span><span class="sxs-lookup"><span data-stu-id="7a810-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Görselleştirme seçin](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="7a810-155">Rapor tooyour Power BI bulut alanınıza yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="7a810-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="7a810-156">Buradan, eşitlenen sürüm diğer web sayfalarına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7a810-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Görselleştirme seçin](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="7a810-158">Merhaba rapor aralıklarla el ile yenileme veya zamanlanan yenileme hello seçenekleri sayfasında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7a810-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7a810-159">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="7a810-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="7a810-160">401 veya 403 yetkisiz</span><span class="sxs-lookup"><span data-stu-id="7a810-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="7a810-161">Refesh belirtecinizi güncelleştirilmez bu durum meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="7a810-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="7a810-162">Bu adımları tooensure hala erişiminiz deneyin.</span><span class="sxs-lookup"><span data-stu-id="7a810-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="7a810-163">Erişiminiz ve refershing hello kimlik bilgileri çalışmıyor, Lütfen bir destek bileti açın.</span><span class="sxs-lookup"><span data-stu-id="7a810-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="7a810-164">Azure Portal Hello oturum ve hello kaynak erişebildiğinden emin olun</span><span class="sxs-lookup"><span data-stu-id="7a810-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="7a810-165">Merhaba Pano toorefresh hello kimlik bilgilerini deneyin</span><span class="sxs-lookup"><span data-stu-id="7a810-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="7a810-166">502 hatalı ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="7a810-166">502 Bad Gateway</span></span>
<span data-ttu-id="7a810-167">Bunun nedeni genellikle çok fazla veri döndüren bir Analytics sorgusu.</span><span class="sxs-lookup"><span data-stu-id="7a810-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="7a810-168">Küçük bir zaman aralığı kullanarak denemelisiniz veya hello kullanarak [önce](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) veya [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) yalnızca işlevleri [proje](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello gereksinim alanları.</span><span class="sxs-lookup"><span data-stu-id="7a810-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="7a810-169">Merhaba Analytics sorgusundan gelen hello dataset azaltma gereksinimlerinizi karşılamıyorsa hello kullanmayı düşünmelisiniz [API](https://dev.applicationinsights.io/documentation/overview) toopull daha büyük bir veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="7a810-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="7a810-170">Burada, tooconvert hello M sorgu toouse hello API nasıl dışarı aktarma yönergeleri verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7a810-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="7a810-171">Oluşturma bir [API anahtarı](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="7a810-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="7a810-172">Güncelleştirme hello değiştirerek Analytics'ten dışarı Power BI M betik ARM URL AI API ile Merhaba (aşağıdaki örneğe bakın)</span><span class="sxs-lookup"><span data-stu-id="7a810-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="7a810-173">Değiştir **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="7a810-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="7a810-174">ile **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="7a810-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="7a810-175">Son olarak, kimlik bilgileri toobasic güncelleştirin ve API anahtarınızı kullanın</span><span class="sxs-lookup"><span data-stu-id="7a810-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="7a810-176">**Varolan komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="7a810-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="7a810-177">**Güncelleştirilmiş bir komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="7a810-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="7a810-178">Örnekleme hakkında</span><span class="sxs-lookup"><span data-stu-id="7a810-178">About sampling</span></span>
<span data-ttu-id="7a810-179">Uygulamanız çok miktarda veri gönderiyorsa hello Uyarlamalı örnekleme özelliği çalışır ve yalnızca telemetrinizi yüzdesi gönderin.</span><span class="sxs-lookup"><span data-stu-id="7a810-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="7a810-180">Merhaba, el ile örnekleme hello SDK veya alım ayarladıysanız doğru aynıdır.</span><span class="sxs-lookup"><span data-stu-id="7a810-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="7a810-181">Örnekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7a810-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="7a810-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a810-182">Next steps</span></span>
* [<span data-ttu-id="7a810-183">Power BI - öğrenin</span><span class="sxs-lookup"><span data-stu-id="7a810-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="7a810-184">Analytics Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="7a810-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

