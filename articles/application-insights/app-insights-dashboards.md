---
title: "Panolar ve Gezinti bölmesinde Azure Application Insights | Microsoft Docs"
description: "Anahtar APM grafikler ve sorguları görünümleri oluşturun."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9987f04e7e71df5fe10c8bc209a390cb940ec4f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="navigation-and-dashboards-in-the-application-insights-portal"></a><span data-ttu-id="327a4-103">Gezinti ve Application Insights portalında panoları</span><span class="sxs-lookup"><span data-stu-id="327a4-103">Navigation and Dashboards in the Application Insights portal</span></span>
<span data-ttu-id="327a4-104">Sonra [projenizde Application Insights'ı ayarlamak](app-insights-overview.md), uygulamanızın performansı ve kullanımı hakkında telemetri verileri projenizin Application Insights kaynağını görünür [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="327a4-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in the [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="327a4-105">Telemetrinizi Bul</span><span class="sxs-lookup"><span data-stu-id="327a4-105">Find your telemetry</span></span>
<span data-ttu-id="327a4-106">Oturum [Azure portal](https://portal.azure.com) ve uygulamanız için oluşturduğunuz Application Insights kaynağı gidin.</span><span class="sxs-lookup"><span data-stu-id="327a4-106">Sign in to the [Azure portal](https://portal.azure.com) and navigate to the Application Insights resource that you created for your app.</span></span>

![Gözat'ı tıklatın, Application Insights ve ardından uygulamanızı seçin.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="327a4-108">Uygulamanız için genel bakış dikey (sayfa) anahtar tanılama ölçümleri, uygulamanızın bir özetini gösterir ve Portalı'nın diğer özellikleri için bir ağ geçididir.</span><span class="sxs-lookup"><span data-stu-id="327a4-108">The overview blade (page) for your app shows a summary of the key diagnostic metrics of your app, and is a gateway to the other features of the portal.</span></span>

![Önde gelen yollar telemetrinizi görüntüleme](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="327a4-110">Tüm grafikler ve kılavuzları özelleştirebilir ve bunları bir panoya Sabitle.</span><span class="sxs-lookup"><span data-stu-id="327a4-110">You can customize any of the charts and grids and pin them to a dashboard.</span></span> <span data-ttu-id="327a4-111">Bu şekilde, merkezi bir Panoda farklı uygulamalardan birlikte anahtar telemetri getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="327a4-111">That way, you can bring together the key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="327a4-112">Panolar</span><span class="sxs-lookup"><span data-stu-id="327a4-112">Dashboards</span></span>
<span data-ttu-id="327a4-113">İçin oturum açtıktan sonra gördüğünüz ilk şey [Microsoft Azure portal](https://portal.azure.com) bir Pano.</span><span class="sxs-lookup"><span data-stu-id="327a4-113">The first thing you see after you sign in to the [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="327a4-114">Burada birlikte telemetrisinden dahil olmak üzere tüm Azure kaynaklarınızı, üzerinden sizin için en önemli olan grafikleri getirebileceğinizden [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="327a4-114">Here you can bring together the charts that are most important to you across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Özelleştirilmiş bir Pano.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="327a4-116">**Belirli kaynaklara gidin** uygulamanıza Application Insights gibi: sol Çubuğu'nu kullanın.</span><span class="sxs-lookup"><span data-stu-id="327a4-116">**Navigate to specific resources** such as your app in Application Insights: Use the left bar.</span></span>
2. <span data-ttu-id="327a4-117">**Geçerli panoya dönmek**, veya geçiş son diğer görünümlere: sol üst kısmında açılan menüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="327a4-117">**Return to the current dashboard**, or switch to other recent views: Use the drop-down menu at top left.</span></span>
3. <span data-ttu-id="327a4-118">**Geçiş panolar**: Pano başlığında açılan menüsünü kullanın</span><span class="sxs-lookup"><span data-stu-id="327a4-118">**Switch dashboards**: Use the drop-down menu on the dashboard title</span></span>
4. <span data-ttu-id="327a4-119">**Oluşturma, düzenleme ve panoları paylaşmak** Pano araç.</span><span class="sxs-lookup"><span data-stu-id="327a4-119">**Create, edit, and share dashboards** in the dashboard toolbar.</span></span>
5. <span data-ttu-id="327a4-120">**Pano düzenleme**: kutucuğunun üzerine gelerek ve taşımak, özelleştirme veya kaldırmak için üst çubuğunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="327a4-120">**Edit the dashboard**: Hover over a tile and then use its top bar to move, customize, or remove it.</span></span>

## <a name="add-to-a-dashboard"></a><span data-ttu-id="327a4-121">Bir Pano ekleyin</span><span class="sxs-lookup"><span data-stu-id="327a4-121">Add to a dashboard</span></span>
<span data-ttu-id="327a4-122">Bir dikey veya özellikle ilginç grafikler kümesi bakarken bir kopyasını panoya sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="327a4-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it to the dashboard.</span></span> <span data-ttu-id="327a4-123">Sonraki sefer var. dönmek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="327a4-123">You'll see it next time you return there.</span></span>

![Bir grafik sabitlemek için üzerine gelin ve ardından üstbilgisindeki "...".](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="327a4-125">Pano grafiği PIN.</span><span class="sxs-lookup"><span data-stu-id="327a4-125">Pin chart to dashboard.</span></span> <span data-ttu-id="327a4-126">Grafik bir kopyasını panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="327a4-126">A copy of the chart appears on the dashboard.</span></span>
2. <span data-ttu-id="327a4-127">Pano tüm dikey pencere sabitlemek - aracılığıyla tıklayabilirsiniz bir kutucuk olarak panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="327a4-127">Pin the whole blade to the dashboard - it appears on the dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="327a4-128">Geçerli panoya dönmek için sol üst köşede'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="327a4-128">Click the top left corner to return to the current dashboard.</span></span> <span data-ttu-id="327a4-129">Ardından geçerli görünümüne dönmek için açılan menüyü kullanın.</span><span class="sxs-lookup"><span data-stu-id="327a4-129">Then you can use the drop-down menu to return to the current view.</span></span>

<span data-ttu-id="327a4-130">Grafikleri döşeme gruplandırılır dikkat edin: bir kutucuk birden fazla grafik içerebilir.</span><span class="sxs-lookup"><span data-stu-id="327a4-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="327a4-131">Panoya tüm kutucuğu sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="327a4-131">You pin the whole tile to the dashboard.</span></span>

<span data-ttu-id="327a4-132">Grafik, grafiğin zaman aralığı bağımlı sıklık otomatik olarak yenilenir:</span><span class="sxs-lookup"><span data-stu-id="327a4-132">The chart is automatically refreshed with a frequency that depends on the chart's time range:</span></span>

* <span data-ttu-id="327a4-133">Zaman aralığı 1 saat: her 5 dakikada bir Yenile</span><span class="sxs-lookup"><span data-stu-id="327a4-133">Time range up to 1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="327a4-134">Aralık 1-24 saat saat: 15 dakikada bir Yenile</span><span class="sxs-lookup"><span data-stu-id="327a4-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="327a4-135">Zaman aralığı 24 saat yukarıda: (zaman aralığı) / 60.</span><span class="sxs-lookup"><span data-stu-id="327a4-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="327a4-136">Herhangi bir sorgu analizleri sabitleyin</span><span class="sxs-lookup"><span data-stu-id="327a4-136">Pin any query in Analytics</span></span>
<span data-ttu-id="327a4-137">Ayrıca [Analytics PIN](app-insights-analytics-using.md#pin-to-dashboard) için grafikleri bir [paylaşılan](#share-dashboards-with-your-team) Pano.</span><span class="sxs-lookup"><span data-stu-id="327a4-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts to a [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="327a4-138">Bu, standart ölçümleri yanında herhangi bir rastgele sorgu grafiklerini eklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="327a4-138">This allows you to add charts of any arbitrary query alongside the standard metrics.</span></span> 

<span data-ttu-id="327a4-139">Sonuçları her saat otomatik olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="327a4-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="327a4-140">Hemen yeniden hesaplamak için grafiği Yenile simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="327a4-140">Click the Refresh icon on the chart to recalculate immediately.</span></span> <span data-ttu-id="327a4-141">(Tarayıcı Yenile hesaplamaz.)</span><span class="sxs-lookup"><span data-stu-id="327a4-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-the-dashboard"></a><span data-ttu-id="327a4-142">Panoda bir kutucuğu Ayarla</span><span class="sxs-lookup"><span data-stu-id="327a4-142">Adjust a tile on the dashboard</span></span>
<span data-ttu-id="327a4-143">Panoda bir kutucuğu olduktan sonra ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="327a4-143">Once a tile is on the dashboard, you can adjust it.</span></span>

![Düzenlemek için bir grafik üzerine gelin.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="327a4-145">Bir grafik döşeme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="327a4-145">Add a chart to the tile.</span></span>
2. <span data-ttu-id="327a4-146">Ölçüm, grup tarafından boyut ve grafiğinin stilini (tablo, grafik) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="327a4-146">Set the metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="327a4-147">Diyagramı yakınlaştırır sürükleyin; timespan sıfırlamak için geri düğmesini tıklatın; Döşeme grafiklerde filtre özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="327a4-147">Drag across the diagram to zoom in; click the undo button to reset the timespan; set filter properties for the charts on the tile.</span></span>
4. <span data-ttu-id="327a4-148">Kutucuk başlığı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="327a4-148">Set tile title.</span></span>

<span data-ttu-id="327a4-149">Ölçüm Gezgini dikey penceresinden Sabitlenen kutucuklar bir genel bakış dikey penceresinden Sabitlenen kutucuklar'den daha fazla düzenleme seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="327a4-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="327a4-150">Sabitlenmiş özgün döşeme düzenlemeleriniz tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="327a4-150">The original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="327a4-151">Panolar arasında geçiş</span><span class="sxs-lookup"><span data-stu-id="327a4-151">Switch between dashboards</span></span>
<span data-ttu-id="327a4-152">Birden fazla panoyu kaydedin ve bunlar arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="327a4-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="327a4-153">Bir grafik veya dikey pencere sabitlemek bunlar geçerli panoya eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="327a4-153">When you pin a chart or blade, they're added to the current dashboard.</span></span>

![Panolar arasında geçiş yapmak için Pano tıklatın ve kaydedilmiş bir Pano seçin.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="327a4-157">Örneğin, takım odası ve genel geliştirme için başka bir tam ekran görüntüleme için tek bir Panoda olabilir.</span><span class="sxs-lookup"><span data-stu-id="327a4-157">For example, you might have one dashboard for displaying full screen in the team room, and another for general development.</span></span>

<span data-ttu-id="327a4-158">Panoda bir kutucuk bir dikey pencere görünür: dikey penceresine gitmek için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="327a4-158">On the dashboard, a blade appears as a tile: click it to go to the blade.</span></span> <span data-ttu-id="327a4-159">Bir grafik özgün konumuna grafikte çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="327a4-159">A chart replicates the chart in its original location.</span></span>

![Temsil ettiği dikey penceresini açmak için kutucuğa tıklayın](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="327a4-161">Panoları paylaşmak</span><span class="sxs-lookup"><span data-stu-id="327a4-161">Share dashboards</span></span>
<span data-ttu-id="327a4-162">Bir Pano oluşturduğunuz zaman, diğer kullanıcılarla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="327a4-162">When you've created a dashboard, you can share it with other users.</span></span>

![Pano üstbilgisinde Paylaş'ı tıklatın.](./media/app-insights-dashboards/41.png)

<span data-ttu-id="327a4-164">Hakkında bilgi edinin [rolleri ve erişim denetimi](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="327a4-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="327a4-165">Uygulama gezinme</span><span class="sxs-lookup"><span data-stu-id="327a4-165">App navigation</span></span>
<span data-ttu-id="327a4-166">Genel Bakış dikey penceresinde uygulamanızı hakkında daha fazla bilgi için ağ geçididir.</span><span class="sxs-lookup"><span data-stu-id="327a4-166">The overview blade is the gateway to more information about your app.</span></span>

* <span data-ttu-id="327a4-167">**Herhangi bir grafik veya döşeme** - herhangi bir kutucuğu tıklayın veya görüntülenenlerin hakkında daha fazla ayrıntı için grafik.</span><span class="sxs-lookup"><span data-stu-id="327a4-167">**Any chart or tile** - Click any tile or chart to see more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="327a4-168">Genel Bakış dikey düğmeleri</span><span class="sxs-lookup"><span data-stu-id="327a4-168">Overview blade buttons</span></span>
![Genel Bakış dikey üst gezinti çubuğu](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="327a4-170">[**Ölçüm Gezgini** ](app-insights-metrics-explorer.md) -performans ve kullanım kendi grafikleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="327a4-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="327a4-171">[**Arama** ](app-insights-diagnostic-search.md) - olayları istekleri, özel durumlar gibi belirli örneklerini araştırmak veya oturum izlemeleri.</span><span class="sxs-lookup"><span data-stu-id="327a4-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="327a4-172">[**Analytics** ](app-insights-analytics.md) -telemetrinizi üzerinden güçlü sorgular.</span><span class="sxs-lookup"><span data-stu-id="327a4-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="327a4-173">**Zaman aralığı** -dikey penceresinde tüm grafikler tarafından görüntülenen aralığını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="327a4-173">**Time range** - Adjust the range displayed by all the charts on the blade.</span></span>
* <span data-ttu-id="327a4-174">**Silme** -bu uygulama için Application Insights kaynağını silin.</span><span class="sxs-lookup"><span data-stu-id="327a4-174">**Delete** - Delete the Application Insights resource for this app.</span></span> <span data-ttu-id="327a4-175">Ayrıca uygulama kodunuzdan Application Insights paketlerini kaldırın, veya Düzenle [izleme anahtarını](app-insights-create-new-resource.md#copy-the-instrumentation-key) farklı bir Application Insights kaynağı telemetri yönlendirmek için uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="327a4-175">You should also either remove the Application Insights packages from your app code, or edit the [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app to direct telemetry to a different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="327a4-176">Essentials sekmesi</span><span class="sxs-lookup"><span data-stu-id="327a4-176">Essentials tab</span></span>
* <span data-ttu-id="327a4-177">[İzleme anahtarını](app-insights-create-new-resource.md#copy-the-instrumentation-key) -bu uygulama kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="327a4-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="327a4-178">Fiyatlandırma - özellikler kullanılabilir ve ayarlanmış birim caps olun.</span><span class="sxs-lookup"><span data-stu-id="327a4-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="327a4-179">Uygulama gezinti çubuğu</span><span class="sxs-lookup"><span data-stu-id="327a4-179">App navigation bar</span></span>
![Sol gezinti çubuğu](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="327a4-181">**Genel Bakış** -uygulama genel bakış dikey penceresine dönün.</span><span class="sxs-lookup"><span data-stu-id="327a4-181">**Overview** - Return to the app overview blade.</span></span>
* <span data-ttu-id="327a4-182">**Etkinlik günlüğü** -uyarı ve Azure yönetim olayları.</span><span class="sxs-lookup"><span data-stu-id="327a4-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="327a4-183">[**Erişim denetimi** ](app-insights-resources-roles-access-control.md) -takım üyeleri ve diğerleri erişim sağlama.</span><span class="sxs-lookup"><span data-stu-id="327a4-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access to team members and others.</span></span>
* <span data-ttu-id="327a4-184">[**Etiketler** ](../azure-resource-manager/resource-group-using-tags.md) -uygulamanızı başkalarıyla gruplandırmak için etiketler kullanın.</span><span class="sxs-lookup"><span data-stu-id="327a4-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags to group your app with others.</span></span>

<span data-ttu-id="327a4-185">ARAŞTIR</span><span class="sxs-lookup"><span data-stu-id="327a4-185">INVESTIGATE</span></span>

* <span data-ttu-id="327a4-186">[**Uygulama eşlemesi** ](app-insights-app-map.md) -, uygulamanızın bileşenleri gösteren etkin eşleme türetilmiş bağımlılık bilgileri.</span><span class="sxs-lookup"><span data-stu-id="327a4-186">[**Application map**](app-insights-app-map.md) - Active map showing the components of your application, derived from the dependency information.</span></span>
* <span data-ttu-id="327a4-187">[**Akıllı algılama** ](app-insights-proactive-diagnostics.md) -son performans uyarıları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="327a4-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="327a4-188">[**Canlı akış** ](app-insights-live-stream.md) - sabit neredeyse anında ölçümler, yeni bir yapı dağıtırken yararlı kümesi veya hata ayıklama A.</span><span class="sxs-lookup"><span data-stu-id="327a4-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="327a4-189">[**Kullanılabilirlik / Web testleri** ](app-insights-monitor-web-app-availability.md) -world.* geçici web uygulamanıza normal İsteği Gönder</span><span class="sxs-lookup"><span data-stu-id="327a4-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests to your web app from around the world.*</span></span>
* <span data-ttu-id="327a4-190">[**Hataları, performans** ](app-insights-web-monitor-performance.md) -özel durumları, hata oranları ve istekleri uygulamanız için ve uygulamanıza gelen isteklere yanıt süreleri [bağımlılıkları](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="327a4-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests to your app and for requests from your app to [dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="327a4-191">[**Performans** ](app-insights-web-monitor-performance.md) -yanıt süresi, bağımlılık yanıt sürelerini.</span><span class="sxs-lookup"><span data-stu-id="327a4-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="327a4-192">[Sunucuları](app-insights-web-monitor-performance.md) -performans sayaçları.</span><span class="sxs-lookup"><span data-stu-id="327a4-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="327a4-193">Kullanılabilir ise, [Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="327a4-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="327a4-194">**Tarayıcı** -sayfa görünümü ve AJAX performans.</span><span class="sxs-lookup"><span data-stu-id="327a4-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="327a4-195">Kullanılabilir ise, [web sayfalarınıza izleme](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="327a4-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="327a4-196">**Kullanım** -sayfa görünümü, kullanıcı ve oturum sayısını.</span><span class="sxs-lookup"><span data-stu-id="327a4-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="327a4-197">Kullanılabilir ise, [web sayfalarınıza izleme](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="327a4-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="327a4-198">YAPILANDIRMA</span><span class="sxs-lookup"><span data-stu-id="327a4-198">CONFIGURE</span></span>

* <span data-ttu-id="327a4-199">**Başlarken** -satır içi öğretici.</span><span class="sxs-lookup"><span data-stu-id="327a4-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="327a4-200">**Özellikler** -izleme anahtarı, abonelik ve kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="327a4-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="327a4-201">[Uyarıları](app-insights-alerts.md) -ölçüm uyarı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="327a4-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="327a4-202">[Sürekli verme](app-insights-export-telemetry.md) -Azure depolama alanına telemetri verilmesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="327a4-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry to Azure storage.</span></span>
* <span data-ttu-id="327a4-203">[Performans testi](app-insights-monitor-web-app-availability.md#performance-tests) -Web sitenizde yapay yük ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="327a4-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="327a4-204">[Kota ve fiyatlarını](app-insights-pricing.md) ve [alım örnekleme](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="327a4-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="327a4-205">**API erişimini** -oluşturmak [yayın ek açıklamaları](app-insights-annotations.md) ve veri erişim API'si.</span><span class="sxs-lookup"><span data-stu-id="327a4-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for the Data Access API.</span></span>
* <span data-ttu-id="327a4-206">[**İş öğeleri** ](app-insights-diagnostic-search.md#create-work-item) -telemetri incelenirken hatalar oluşturabilmesi için izleme sistemi iş bağlanın.</span><span class="sxs-lookup"><span data-stu-id="327a4-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect to a work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="327a4-207">AYARLAR</span><span class="sxs-lookup"><span data-stu-id="327a4-207">SETTINGS</span></span>

* <span data-ttu-id="327a4-208">[**Kilitler** ](../azure-resource-manager/resource-group-lock-resources.md) -Azure kaynaklarını Kilitle</span><span class="sxs-lookup"><span data-stu-id="327a4-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="327a4-209">[**Otomasyon betiğini** ](app-insights-powershell.md) -Azure kaynak tanımını dışa yeni kaynak oluşturmak için bir şablon olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="327a4-209">[**Automation script**](app-insights-powershell.md) - export a definition of the Azure resource so that you can use it as a template to create new resources.</span></span>


## <a name="video"></a><span data-ttu-id="327a4-210">Video</span><span class="sxs-lookup"><span data-stu-id="327a4-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="327a4-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="327a4-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="327a4-212">Ölçüm Gezgini</span><span class="sxs-lookup"><span data-stu-id="327a4-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="327a4-213">Filtre ve segment ölçümleri</span><span class="sxs-lookup"><span data-stu-id="327a4-213">Filter and segment metrics</span></span> |![Arama örneği](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="327a4-215">Tanılama arama</span><span class="sxs-lookup"><span data-stu-id="327a4-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="327a4-216">Bul ve olayları, ilgili olayları inceleyin ve hatalar oluşturma</span><span class="sxs-lookup"><span data-stu-id="327a4-216">Find and inspect events, related events, and create bugs</span></span> |![Arama örneği](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="327a4-218">Analizler</span><span class="sxs-lookup"><span data-stu-id="327a4-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="327a4-219">Güçlü sorgu dili</span><span class="sxs-lookup"><span data-stu-id="327a4-219">Powerful query language</span></span> |![Arama örneği](./media/app-insights-dashboards/63.png) |
