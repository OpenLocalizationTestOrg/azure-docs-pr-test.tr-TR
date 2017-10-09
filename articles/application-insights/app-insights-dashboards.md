---
title: Azure Application Insights hello gezintisi ve aaaDashboards | Microsoft Docs
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
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a><span data-ttu-id="f2dbe-103">Gezinti ve panolar hello Application Insights portalında</span><span class="sxs-lookup"><span data-stu-id="f2dbe-103">Navigation and Dashboards in hello Application Insights portal</span></span>
<span data-ttu-id="f2dbe-104">Sonra [projenizde Application Insights'ı ayarlamak](app-insights-overview.md), uygulamanızın performansı ve kullanımı hakkında telemetri verileri hello projenizin Application Insights kaynağını görünür [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-104">After you have [set up Application Insights on your project](app-insights-overview.md), telemetry data about your app's performance and usage will appear in your project's Application Insights resource in hello [Azure portal](https://portal.azure.com).</span></span>

## <a name="find-your-telemetry"></a><span data-ttu-id="f2dbe-105">Telemetrinizi Bul</span><span class="sxs-lookup"><span data-stu-id="f2dbe-105">Find your telemetry</span></span>
<span data-ttu-id="f2dbe-106">İçinde toohello oturum [Azure portal](https://portal.azure.com) ve uygulamanız için oluşturduğunuz toohello Application Insights kaynağı gidin.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-106">Sign in toohello [Azure portal](https://portal.azure.com) and navigate toohello Application Insights resource that you created for your app.</span></span>

![Gözat'ı tıklatın, Application Insights ve ardından uygulamanızı seçin.](./media/app-insights-dashboards/00-start.png)

<span data-ttu-id="f2dbe-108">Uygulamanız için Hello genel bakış dikey penceresinde (sayfa) hello anahtar tanılama ölçümleri, uygulamanızın özetini gösterir ve bir ağ geçidi toohello hello Portalı'nın diğer özellikleri.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-108">hello overview blade (page) for your app shows a summary of hello key diagnostic metrics of your app, and is a gateway toohello other features of hello portal.</span></span>

![Yollar tooview telemetrinizi büyük](./media/app-insights-dashboards/010-oview.png)

<span data-ttu-id="f2dbe-110">Tüm hello grafikleri ve kılavuzları özelleştirebilir ve tooa Pano sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-110">You can customize any of hello charts and grids and pin them tooa dashboard.</span></span> <span data-ttu-id="f2dbe-111">Bu şekilde, merkezi bir Panoda farklı uygulamalardan birlikte hello anahtar telemetri getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-111">That way, you can bring together hello key telemetry from different apps on a central dashboard.</span></span>

## <a name="dashboards"></a><span data-ttu-id="f2dbe-112">Panolar</span><span class="sxs-lookup"><span data-stu-id="f2dbe-112">Dashboards</span></span>
<span data-ttu-id="f2dbe-113">içinde toohello oturumu sonra hello ilk şey gördüğünüz [Microsoft Azure portal](https://portal.azure.com) bir Pano.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-113">hello first thing you see after you sign in toohello [Microsoft Azure portal](https://portal.azure.com) is a dashboard.</span></span> <span data-ttu-id="f2dbe-114">Burada birlikte telemetrisinden dahil olmak üzere tüm Azure kaynaklarınızı, üzerinden en önemli tooyou olan hello grafikleri getirebileceğinizden [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-114">Here you can bring together hello charts that are most important tooyou across all your Azure resources, including telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

![Özelleştirilmiş bir Pano.](./media/app-insights-dashboards/31.png)

1. <span data-ttu-id="f2dbe-116">**Toospecific kaynaklara gitme** uygulamanıza Application Insights gibi: kullanım hello sol çubuğu.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-116">**Navigate toospecific resources** such as your app in Application Insights: Use hello left bar.</span></span>
2. <span data-ttu-id="f2dbe-117">**Dönüş toohello geçerli Pano**, veya geçiş tooother son görünümleri: sol üst kullanım hello açılır menü.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-117">**Return toohello current dashboard**, or switch tooother recent views: Use hello drop-down menu at top left.</span></span>
3. <span data-ttu-id="f2dbe-118">**Geçiş panolar**: hello Pano başlık kullanım hello aşağı açılan menüsünde</span><span class="sxs-lookup"><span data-stu-id="f2dbe-118">**Switch dashboards**: Use hello drop-down menu on hello dashboard title</span></span>
4. <span data-ttu-id="f2dbe-119">**Oluşturma, düzenleme ve panoları paylaşmak** hello Pano araç.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-119">**Create, edit, and share dashboards** in hello dashboard toolbar.</span></span>
5. <span data-ttu-id="f2dbe-120">**Merhaba Pano düzenleme**: kutucuğunun üzerine gelerek ve kendi üst kullan toomove, çubuk özelleştirebilir ya da kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-120">**Edit hello dashboard**: Hover over a tile and then use its top bar toomove, customize, or remove it.</span></span>

## <a name="add-tooa-dashboard"></a><span data-ttu-id="f2dbe-121">Tooa Pano Ekle</span><span class="sxs-lookup"><span data-stu-id="f2dbe-121">Add tooa dashboard</span></span>
<span data-ttu-id="f2dbe-122">Bir dikey veya özellikle ilginç grafikler kümesi bakarken toohello panonun bir kopyasını sabitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-122">When you're looking at a blade or set of charts that's particularly interesting, you can pin a copy of it toohello dashboard.</span></span> <span data-ttu-id="f2dbe-123">Sonraki sefer var. dönmek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-123">You'll see it next time you return there.</span></span>

![bir grafik toopin üzerine gelin ve ardından hello üstbilgisindeki "...".](./media/app-insights-dashboards/33.png)

1. <span data-ttu-id="f2dbe-125">Grafik toodashboard sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-125">Pin chart toodashboard.</span></span> <span data-ttu-id="f2dbe-126">Merhaba grafik bir kopyasını hello panosunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-126">A copy of hello chart appears on hello dashboard.</span></span>
2. <span data-ttu-id="f2dbe-127">PIN hello tüm dikey toohello Pano - aracılığıyla tıklayabilirsiniz bir kutucuk olarak hello panosunda görünür.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-127">Pin hello whole blade toohello dashboard - it appears on hello dashboard as a tile that you can click through.</span></span>
3. <span data-ttu-id="f2dbe-128">Merhaba sol üst köşesinde tooreturn toohello geçerli panodan'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-128">Click hello top left corner tooreturn toohello current dashboard.</span></span> <span data-ttu-id="f2dbe-129">Daha sonra hello açılır menü tooreturn toohello geçerli görünümü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-129">Then you can use hello drop-down menu tooreturn toohello current view.</span></span>

<span data-ttu-id="f2dbe-130">Grafikleri döşeme gruplandırılır dikkat edin: bir kutucuk birden fazla grafik içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-130">Notice that charts are grouped into tiles: a tile can contain more than one chart.</span></span> <span data-ttu-id="f2dbe-131">Merhaba tüm döşeme toohello Pano sabitleyin.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-131">You pin hello whole tile toohello dashboard.</span></span>

<span data-ttu-id="f2dbe-132">Merhaba grafik hello grafiğin zaman aralığı bağımlı sıklık otomatik olarak yenilenir:</span><span class="sxs-lookup"><span data-stu-id="f2dbe-132">hello chart is automatically refreshed with a frequency that depends on hello chart's time range:</span></span>

* <span data-ttu-id="f2dbe-133">Zaman aralığı too1 saat oluşturmak: her 5 dakikada bir Yenile</span><span class="sxs-lookup"><span data-stu-id="f2dbe-133">Time range up too1 hour: Refresh every 5 minutes</span></span>
* <span data-ttu-id="f2dbe-134">Aralık 1-24 saat saat: 15 dakikada bir Yenile</span><span class="sxs-lookup"><span data-stu-id="f2dbe-134">Time range 1 - 24 hours: Refresh every 15 minutes</span></span>
* <span data-ttu-id="f2dbe-135">Zaman aralığı 24 saat yukarıda: (zaman aralığı) / 60.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-135">Time range above 24 hours: (Time range)/60.</span></span>

### <a name="pin-any-query-in-analytics"></a><span data-ttu-id="f2dbe-136">Herhangi bir sorgu analizleri sabitleyin</span><span class="sxs-lookup"><span data-stu-id="f2dbe-136">Pin any query in Analytics</span></span>
<span data-ttu-id="f2dbe-137">Ayrıca [Analytics PIN](app-insights-analytics-using.md#pin-to-dashboard) grafikleri tooa [paylaşılan](#share-dashboards-with-your-team) Pano.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-137">You can also [pin Analytics](app-insights-analytics-using.md#pin-to-dashboard) charts tooa [shared](#share-dashboards-with-your-team) dashboard.</span></span> <span data-ttu-id="f2dbe-138">Bu, herhangi bir rastgele sorgu hello standart ölçümleri yanında tooadd grafiklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-138">This allows you tooadd charts of any arbitrary query alongside hello standard metrics.</span></span> 

<span data-ttu-id="f2dbe-139">Sonuçları her saat otomatik olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-139">Results are automatically recalculated every hour.</span></span> <span data-ttu-id="f2dbe-140">Hemen hello grafik toorecalculate Hello Yenile simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-140">Click hello Refresh icon on hello chart toorecalculate immediately.</span></span> <span data-ttu-id="f2dbe-141">(Tarayıcı Yenile hesaplamaz.)</span><span class="sxs-lookup"><span data-stu-id="f2dbe-141">(Browser refresh doesn't recalculate.)</span></span>

## <a name="adjust-a-tile-on-hello-dashboard"></a><span data-ttu-id="f2dbe-142">Başlangıç Panosu kutucuk Ayarla</span><span class="sxs-lookup"><span data-stu-id="f2dbe-142">Adjust a tile on hello dashboard</span></span>
<span data-ttu-id="f2dbe-143">Merhaba Panoda bir kutucuğu olduktan sonra ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-143">Once a tile is on hello dashboard, you can adjust it.</span></span>

![Üzerine gelerek sipariş tooedit grafik üzerinden bu.](./media/app-insights-dashboards/36.png)

1. <span data-ttu-id="f2dbe-145">Bir grafik toohello kutucuğu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-145">Add a chart toohello tile.</span></span>
2. <span data-ttu-id="f2dbe-146">Merhaba ölçüm, grup tarafından boyut ve grafiğinin stilini (tablo, grafik) ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-146">Set hello metric, group-by dimension and style (table, graph) of a chart.</span></span>
3. <span data-ttu-id="f2dbe-147">Merhaba diyagramı toozoom sürükleyin; Merhaba geri düğmesini tooreset hello timespan tıklayın; Merhaba döşeme hello grafiklerde filtre özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-147">Drag across hello diagram toozoom in; click hello undo button tooreset hello timespan; set filter properties for hello charts on hello tile.</span></span>
4. <span data-ttu-id="f2dbe-148">Kutucuk başlığı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-148">Set tile title.</span></span>

<span data-ttu-id="f2dbe-149">Ölçüm Gezgini dikey penceresinden Sabitlenen kutucuklar bir genel bakış dikey penceresinden Sabitlenen kutucuklar'den daha fazla düzenleme seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-149">Tiles pinned from metric explorer blades have more editing options than tiles pinned from an Overview blade.</span></span>

<span data-ttu-id="f2dbe-150">Sabitlenmiş hello özgün döşeme düzenlemeleriniz tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-150">hello original tile that you pinned isn't affected by your edits.</span></span>

## <a name="switch-between-dashboards"></a><span data-ttu-id="f2dbe-151">Panolar arasında geçiş</span><span class="sxs-lookup"><span data-stu-id="f2dbe-151">Switch between dashboards</span></span>
<span data-ttu-id="f2dbe-152">Birden fazla panoyu kaydedin ve bunlar arasında geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-152">You can save more than one dashboard and switch between them.</span></span> <span data-ttu-id="f2dbe-153">Bir grafik veya dikey pencere sabitlemek bunlar toohello geçerli Pano eklenmesi.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-153">When you pin a chart or blade, they're added toohello current dashboard.</span></span>

![Panolar arasında tooswitch Pano tıklatın ve kaydedilmiş bir Pano seçin.](./media/app-insights-dashboards/32.png)

<span data-ttu-id="f2dbe-157">Örneğin, hello takım odası ve genel geliştirme için başka bir tam ekran görüntüleme için tek bir Panoda olabilir.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-157">For example, you might have one dashboard for displaying full screen in hello team room, and another for general development.</span></span>

<span data-ttu-id="f2dbe-158">Merhaba Panoda bir kutucuk bir dikey pencere görünür: toogo toohello dikey tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-158">On hello dashboard, a blade appears as a tile: click it toogo toohello blade.</span></span> <span data-ttu-id="f2dbe-159">Bir grafik özgün konumuna hello grafikte çoğaltır.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-159">A chart replicates hello chart in its original location.</span></span>

![Temsil ettiği bir kutucuğu tooopen hello dikey tıklayın](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a><span data-ttu-id="f2dbe-161">Panoları paylaşmak</span><span class="sxs-lookup"><span data-stu-id="f2dbe-161">Share dashboards</span></span>
<span data-ttu-id="f2dbe-162">Bir Pano oluşturduğunuz zaman, diğer kullanıcılarla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-162">When you've created a dashboard, you can share it with other users.</span></span>

![Merhaba Pano üstbilgisinde Paylaş'ı tıklatın.](./media/app-insights-dashboards/41.png)

<span data-ttu-id="f2dbe-164">Hakkında bilgi edinin [rolleri ve erişim denetimi](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-164">Learn about [Roles and access control](app-insights-resources-roles-access-control.md).</span></span>

## <a name="app-navigation"></a><span data-ttu-id="f2dbe-165">Uygulama gezinme</span><span class="sxs-lookup"><span data-stu-id="f2dbe-165">App navigation</span></span>
<span data-ttu-id="f2dbe-166">Hello genel bakış dikey penceresinde hello ağ geçidi toomore uygulamanız hakkındaki bilgilerdir.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-166">hello overview blade is hello gateway toomore information about your app.</span></span>

* <span data-ttu-id="f2dbe-167">**Herhangi bir grafik veya döşeme** - herhangi bir kutucuğu tıklayın veya toosee ne görüntüler hakkında daha fazla ayrıntı grafik.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-167">**Any chart or tile** - Click any tile or chart toosee more detail about what it displays.</span></span>

### <a name="overview-blade-buttons"></a><span data-ttu-id="f2dbe-168">Genel Bakış dikey düğmeleri</span><span class="sxs-lookup"><span data-stu-id="f2dbe-168">Overview blade buttons</span></span>
![Genel Bakış dikey üst gezinti çubuğu](./media/app-insights-dashboards/app-overview-top-nav.png)

* <span data-ttu-id="f2dbe-170">[**Ölçüm Gezgini** ](app-insights-metrics-explorer.md) -performans ve kullanım kendi grafikleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-170">[**Metrics Explorer**](app-insights-metrics-explorer.md) - Create your own charts of performance and usage.</span></span>
* <span data-ttu-id="f2dbe-171">[**Arama** ](app-insights-diagnostic-search.md) - olayları istekleri, özel durumlar gibi belirli örneklerini araştırmak veya oturum izlemeleri.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-171">[**Search**](app-insights-diagnostic-search.md) - Investigate specific instances of events such as requests, exceptions, or log traces.</span></span>
* <span data-ttu-id="f2dbe-172">[**Analytics** ](app-insights-analytics.md) -telemetrinizi üzerinden güçlü sorgular.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-172">[**Analytics**](app-insights-analytics.md) - Powerful queries over your telemetry.</span></span>
* <span data-ttu-id="f2dbe-173">**Zaman aralığı** -hello dikey penceresinde tüm hello grafikler tarafından görüntülenen hello aralığını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-173">**Time range** - Adjust hello range displayed by all hello charts on hello blade.</span></span>
* <span data-ttu-id="f2dbe-174">**Silme** -bu uygulama için hello Application Insights kaynağı silme.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-174">**Delete** - Delete hello Application Insights resource for this app.</span></span> <span data-ttu-id="f2dbe-175">Ayrıca uygulama kodunuzdan hello Application Insights paketlerini kaldırın, veya hello Düzenle [izleme anahtarını](app-insights-create-new-resource.md#copy-the-instrumentation-key) uygulama toodirect telemetri tooa farklı Application Insights kaynağınıza içinde.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-175">You should also either remove hello Application Insights packages from your app code, or edit hello [instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) in your app toodirect telemetry tooa different Application Insights resource.</span></span>

### <a name="essentials-tab"></a><span data-ttu-id="f2dbe-176">Essentials sekmesi</span><span class="sxs-lookup"><span data-stu-id="f2dbe-176">Essentials tab</span></span>
* <span data-ttu-id="f2dbe-177">[İzleme anahtarını](app-insights-create-new-resource.md#copy-the-instrumentation-key) -bu uygulama kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-177">[Instrumentation key](app-insights-create-new-resource.md#copy-the-instrumentation-key) - Identifies this app resource.</span></span>
* <span data-ttu-id="f2dbe-178">Fiyatlandırma - özellikler kullanılabilir ve ayarlanmış birim caps olun.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-178">Pricing - Make features available and set volume caps.</span></span>

### <a name="app-navigation-bar"></a><span data-ttu-id="f2dbe-179">Uygulama gezinti çubuğu</span><span class="sxs-lookup"><span data-stu-id="f2dbe-179">App navigation bar</span></span>
![Sol gezinti çubuğu](./media/app-insights-dashboards/app-left-nav-bar.png)

* <span data-ttu-id="f2dbe-181">**Genel Bakış** -dönüş toohello uygulamaya genel bakış dikey.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-181">**Overview** - Return toohello app overview blade.</span></span>
* <span data-ttu-id="f2dbe-182">**Etkinlik günlüğü** -uyarı ve Azure yönetim olayları.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-182">**Activity log** - Alerts and Azure administrative events.</span></span>
* <span data-ttu-id="f2dbe-183">[**Erişim denetimi** ](app-insights-resources-roles-access-control.md) -erişim tooteam üyeleri ve diğerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-183">[**Access control**](app-insights-resources-roles-access-control.md) - Provide access tooteam members and others.</span></span>
* <span data-ttu-id="f2dbe-184">[**Etiketler** ](../azure-resource-manager/resource-group-using-tags.md) -kullanım uygulamanızı başkalarıyla toogroup etiketler.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-184">[**Tags**](../azure-resource-manager/resource-group-using-tags.md) - Use tags toogroup your app with others.</span></span>

<span data-ttu-id="f2dbe-185">ARAŞTIR</span><span class="sxs-lookup"><span data-stu-id="f2dbe-185">INVESTIGATE</span></span>

* <span data-ttu-id="f2dbe-186">[**Uygulama eşlemesi** ](app-insights-app-map.md) -hello bileşenleri, uygulamanızın gösteren etkin eşleme türetilmiş hello bağımlılık bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-186">[**Application map**](app-insights-app-map.md) - Active map showing hello components of your application, derived from hello dependency information.</span></span>
* <span data-ttu-id="f2dbe-187">[**Akıllı algılama** ](app-insights-proactive-diagnostics.md) -son performans uyarıları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-187">[**Smart Detection**](app-insights-proactive-diagnostics.md) - Review recent performance alerts.</span></span>
* <span data-ttu-id="f2dbe-188">[**Canlı akış** ](app-insights-live-stream.md) - sabit neredeyse anında ölçümler, yeni bir yapı dağıtırken yararlı kümesi veya hata ayıklama A.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-188">[**Live Stream**](app-insights-live-stream.md) - A fixed set of near-instant metrics, useful when deploying a new build or debugging.</span></span>
* <span data-ttu-id="f2dbe-189">[**Kullanılabilirlik / Web testleri** ](app-insights-monitor-web-app-availability.md) -gönderme normal istekleri tooyour web uygulamasından hello world.* geçici</span><span class="sxs-lookup"><span data-stu-id="f2dbe-189">[**Availability / Web tests**](app-insights-monitor-web-app-availability.md) - Send regular requests tooyour web app from around hello world.*</span></span>
* <span data-ttu-id="f2dbe-190">[**Hataları, performans** ](app-insights-web-monitor-performance.md) -özel durumları, hata oranları ve yanıt süreleri uygulamanız gelen istekleri ve istekleri tooyour uygulama için çok[bağımlılıkları](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-190">[**Failures, Performance**](app-insights-web-monitor-performance.md) - Exceptions, failure rates and response times for requests tooyour app and for requests from your app too[dependencies](app-insights-asp-net-dependencies.md).</span></span>
* <span data-ttu-id="f2dbe-191">[**Performans** ](app-insights-web-monitor-performance.md) -yanıt süresi, bağımlılık yanıt sürelerini.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-191">[**Performance**](app-insights-web-monitor-performance.md) - Response time, dependency response times.</span></span>
* <span data-ttu-id="f2dbe-192">[Sunucuları](app-insights-web-monitor-performance.md) -performans sayaçları.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-192">[Servers](app-insights-web-monitor-performance.md) - Performance counters.</span></span> <span data-ttu-id="f2dbe-193">Kullanılabilir ise, [Durum İzleyicisi yükleme](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-193">Available if you [install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="f2dbe-194">**Tarayıcı** -sayfa görünümü ve AJAX performans.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-194">**Browser** - Page view and AJAX performance.</span></span> <span data-ttu-id="f2dbe-195">Kullanılabilir ise, [web sayfalarınıza izleme](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-195">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>
* <span data-ttu-id="f2dbe-196">**Kullanım** -sayfa görünümü, kullanıcı ve oturum sayısını.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-196">**Usage** - Page view, user, and session counts.</span></span> <span data-ttu-id="f2dbe-197">Kullanılabilir ise, [web sayfalarınıza izleme](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-197">Available if you [instrument your web pages](app-insights-javascript.md).</span></span>

<span data-ttu-id="f2dbe-198">YAPILANDIRMA</span><span class="sxs-lookup"><span data-stu-id="f2dbe-198">CONFIGURE</span></span>

* <span data-ttu-id="f2dbe-199">**Başlarken** -satır içi öğretici.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-199">**Getting started** - inline tutorial.</span></span>
* <span data-ttu-id="f2dbe-200">**Özellikler** -izleme anahtarı, abonelik ve kaynak kimliği.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-200">**Properties** - instrumentation key, subscription and resource id.</span></span>
* <span data-ttu-id="f2dbe-201">[Uyarıları](app-insights-alerts.md) -ölçüm uyarı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-201">[Alerts](app-insights-alerts.md) - metric alert configuration.</span></span>
* <span data-ttu-id="f2dbe-202">[Sürekli verme](app-insights-export-telemetry.md) -telemetri tooAzure depolama verilmesini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-202">[Continuous export](app-insights-export-telemetry.md) - configure export of telemetry tooAzure storage.</span></span>
* <span data-ttu-id="f2dbe-203">[Performans testi](app-insights-monitor-web-app-availability.md#performance-tests) -Web sitenizde yapay yük ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-203">[Performance testing](app-insights-monitor-web-app-availability.md#performance-tests) - set up a synthetic load on your website.</span></span>
* <span data-ttu-id="f2dbe-204">[Kota ve fiyatlarını](app-insights-pricing.md) ve [alım örnekleme](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="f2dbe-204">[Quota and pricing](app-insights-pricing.md) and [ingestion sampling](app-insights-sampling.md).</span></span>
* <span data-ttu-id="f2dbe-205">**API erişimini** -oluşturmak [yayın ek açıklamaları](app-insights-annotations.md) ve hello veri erişim API için.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-205">**API Access** - Create [release annotations](app-insights-annotations.md) and for hello Data Access API.</span></span>
* <span data-ttu-id="f2dbe-206">[**İş öğeleri** ](app-insights-diagnostic-search.md#create-work-item) -tooa iş telemetri incelenirken hatalar oluşturabilmesi için sistem izleme bağlanın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-206">[**Work Items**](app-insights-diagnostic-search.md#create-work-item) - Connect tooa work tracking system so that you can create bugs while inspecting telemetry.</span></span>

<span data-ttu-id="f2dbe-207">AYARLAR</span><span class="sxs-lookup"><span data-stu-id="f2dbe-207">SETTINGS</span></span>

* <span data-ttu-id="f2dbe-208">[**Kilitler** ](../azure-resource-manager/resource-group-lock-resources.md) -Azure kaynaklarını Kilitle</span><span class="sxs-lookup"><span data-stu-id="f2dbe-208">[**Locks**](../azure-resource-manager/resource-group-lock-resources.md) - lock Azure resources</span></span>
* <span data-ttu-id="f2dbe-209">[**Otomasyon betiğini** ](app-insights-powershell.md) -hello Azure kaynak tanımını dışa şablonu bir toocreate yeni kaynağı olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2dbe-209">[**Automation script**](app-insights-powershell.md) - export a definition of hello Azure resource so that you can use it as a template toocreate new resources.</span></span>


## <a name="video"></a><span data-ttu-id="f2dbe-210">Video</span><span class="sxs-lookup"><span data-stu-id="f2dbe-210">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="f2dbe-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f2dbe-211">Next steps</span></span>

|  |  |
| --- | --- |
| [<span data-ttu-id="f2dbe-212">Ölçüm Gezgini</span><span class="sxs-lookup"><span data-stu-id="f2dbe-212">Metrics explorer</span></span>](app-insights-metrics-explorer.md)<br/><span data-ttu-id="f2dbe-213">Filtre ve segment ölçümleri</span><span class="sxs-lookup"><span data-stu-id="f2dbe-213">Filter and segment metrics</span></span> |![Arama örneği](./media/app-insights-dashboards/64.png) |
| [<span data-ttu-id="f2dbe-215">Tanılama arama</span><span class="sxs-lookup"><span data-stu-id="f2dbe-215">Diagnostic search</span></span>](app-insights-diagnostic-search.md)<br/><span data-ttu-id="f2dbe-216">Bul ve olayları, ilgili olayları inceleyin ve hatalar oluşturma</span><span class="sxs-lookup"><span data-stu-id="f2dbe-216">Find and inspect events, related events, and create bugs</span></span> |![Arama örneği](./media/app-insights-dashboards/61.png) |
| [<span data-ttu-id="f2dbe-218">Analizler</span><span class="sxs-lookup"><span data-stu-id="f2dbe-218">Analytics</span></span>](app-insights-analytics.md)<br/><span data-ttu-id="f2dbe-219">Güçlü sorgu dili</span><span class="sxs-lookup"><span data-stu-id="f2dbe-219">Powerful query language</span></span> |![Arama örneği](./media/app-insights-dashboards/63.png) |
