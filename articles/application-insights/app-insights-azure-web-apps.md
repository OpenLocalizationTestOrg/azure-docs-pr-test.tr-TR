---
title: "Azure web uygulaması performans aaaMonitor | Microsoft Docs"
description: "Azure web uygulamaları için uygulama performansını izleme. Yük, yanıt süresi ve bağımlılık bilgilerinin grafiğini çıkarın ve performansa bağlı uyarılar ayarlayın."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a><span data-ttu-id="905bf-104">Azure web uygulaması performansını izleme</span><span class="sxs-lookup"><span data-stu-id="905bf-104">Monitor Azure web app performance</span></span>
<span data-ttu-id="905bf-105">Merhaba, [Azure Portal](https://portal.azure.com) için uygulama performansı izleme yukarı ayarlayabilir, [Azure web uygulamaları](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="905bf-105">In hello [Azure Portal](https://portal.azure.com) you can set up application performance monitoring for your [Azure web apps](../app-service-web/app-service-web-overview.md).</span></span> <span data-ttu-id="905bf-106">[Azure Application Insights](app-insights-overview.md) hakkında kendi etkinlikleri toohello nerede depolandığı ve analiz Application Insights hizmeti, uygulama toosend telemetrinizi Instruments.</span><span class="sxs-lookup"><span data-stu-id="905bf-106">[Azure Application Insights](app-insights-overview.md) instruments your app toosend telemetry about its activities toohello Application Insights service, where it is stored and analyzed.</span></span> <span data-ttu-id="905bf-107">Burada, ölçüm grafikler ve arama araçları kullanılabilir toohelp sorunlarını tanılamak, performansı ve kullanımı değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="905bf-107">There, metric charts and search tools can be used toohelp diagnose issues, improve performance, and assess usage.</span></span>

## <a name="run-time-or-build-time"></a><span data-ttu-id="905bf-108">Çalışma zamanı veya derleme zamanı</span><span class="sxs-lookup"><span data-stu-id="905bf-108">Run time or build time</span></span>
<span data-ttu-id="905bf-109">İki yoldan biriyle hello uygulamada işaretlenerek izleme yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="905bf-109">You can configure monitoring by instrumenting hello app in either of two ways:</span></span>

* <span data-ttu-id="905bf-110">**Çalışma zamanı**: Web uygulamanız zaten yayındayken bir performans izleme uzantısını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="905bf-110">**Run-time** - You can select a performance monitoring extension when your web app is already live.</span></span> <span data-ttu-id="905bf-111">Gerekli toorebuild değil veya uygulamanızı yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="905bf-111">It isn't necessary toorebuild or re-install your app.</span></span> <span data-ttu-id="905bf-112">Yanıt süreleri, başarı oranları, özel durumlar ve bağımlılıklar gibi değişkenleri izleyen standart bir paket kümesine sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="905bf-112">You get a standard set of packages that monitor response times, success rates, exceptions, dependencies, and so on.</span></span> 
* <span data-ttu-id="905bf-113">**Derleme zamanı**: Geliştirme sırasında uygulamanıza bir paket yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="905bf-113">**Build time** - You can install a package in your app in development.</span></span> <span data-ttu-id="905bf-114">Bu seçenek daha kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="905bf-114">This option is more versatile.</span></span> <span data-ttu-id="905bf-115">Toplama toohello içinde aynı standart paketleri yazabilirsiniz kod toocustomize hello telemetri veya toosend kendi telemetrinizi.</span><span class="sxs-lookup"><span data-stu-id="905bf-115">In addition toohello same standard packages, you can write code toocustomize hello telemetry or toosend your own telemetry.</span></span> <span data-ttu-id="905bf-116">Belirli etkinlikleri veya uygulama etki alanınızın toohello semantiği göre kayıt olayları oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="905bf-116">You can log specific activities or record events according toohello semantics of your app domain.</span></span> 

## <a name="run-time-instrumentation-with-application-insights"></a><span data-ttu-id="905bf-117">Application Insights ile çalışma zamanında izleme</span><span class="sxs-lookup"><span data-stu-id="905bf-117">Run time instrumentation with Application Insights</span></span>
<span data-ttu-id="905bf-118">Azure’da çalışmakta olan bir web uygulamanız varsa zaten bazı izleme verileri alırsınız: İstek ve hata oranları.</span><span class="sxs-lookup"><span data-stu-id="905bf-118">If you're already running a web app in Azure, you already get some monitoring: request and error rates.</span></span> <span data-ttu-id="905bf-119">Application Insights tooget daha fazla yanıt sürelerini ve izleme çağrıları toodependencies, akıllı algılama ve hello güçlü günlük analizi sorgu dili gibi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="905bf-119">Add Application Insights tooget more, such as response times, monitoring calls toodependencies, smart detection, and hello powerful Log Analytics query language.</span></span> 

1. <span data-ttu-id="905bf-120">**Application Insights seçin** web uygulamanız için hello Azure Denetim Masası'nda.</span><span class="sxs-lookup"><span data-stu-id="905bf-120">**Select Application Insights** in hello Azure control panel for your web app.</span></span>
   
    ![İzleme bölümünden Application Insights’ı seçin](./media/app-insights-azure-web-apps/05-extend.png)
   
   * <span data-ttu-id="905bf-122">Zaten bu uygulama için Application Insights kaynağı başka bir yol ayarlamadıysanız toocreate yeni bir kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="905bf-122">Choose toocreate a new resource, unless you already set up an Application Insights resource for this app by another route.</span></span>
2. <span data-ttu-id="905bf-123">Application Insights yüklendikten sonra **web uygulamanızı izleyin** .</span><span class="sxs-lookup"><span data-stu-id="905bf-123">**Instrument your web app** after Application Insights has been installed.</span></span> 
   
    ![Web uygulamanızı izleme](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   <span data-ttu-id="905bf-125">Sayfa görüntülemesi ve kullanıcı telemetrisi için **istemci tarafı izlemeyi etkinleştirin**.</span><span class="sxs-lookup"><span data-stu-id="905bf-125">**Enable client side monitoring** for page view and user telemetry.</span></span>

   * <span data-ttu-id="905bf-126">Ayarlar > Uygulama Ayarları'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="905bf-126">Select Settings > Application Settings</span></span>
   * <span data-ttu-id="905bf-127">Uygulama Ayarları'nın altında yeni bir anahtar değer çifti ekleyin:</span><span class="sxs-lookup"><span data-stu-id="905bf-127">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="905bf-128">Anahtar: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="905bf-128">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="905bf-129">Değer:`true`</span><span class="sxs-lookup"><span data-stu-id="905bf-129">Value: `true`</span></span>
   * <span data-ttu-id="905bf-130">**Kaydet** hello ayarları ve **yeniden** uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="905bf-130">**Save** hello settings and **Restart** your app.</span></span>
3. <span data-ttu-id="905bf-131">**Uygulamanızı izleyin**.</span><span class="sxs-lookup"><span data-stu-id="905bf-131">**Monitor your app**.</span></span>  <span data-ttu-id="905bf-132">[Expore hello veri](#explore-the-data).</span><span class="sxs-lookup"><span data-stu-id="905bf-132">[Expore hello data](#explore-the-data).</span></span>

<span data-ttu-id="905bf-133">Daha sonra isterseniz hello uygulama Application Insights ile oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="905bf-133">Later, you can build hello app with Application Insights if you want.</span></span>

<span data-ttu-id="905bf-134">*Nasıl kaldırabilirim Application Insights, veya toosending tooanother kaynak geçiş?*</span><span class="sxs-lookup"><span data-stu-id="905bf-134">*How do I remove Application Insights, or switch toosending tooanother resource?*</span></span>

* <span data-ttu-id="905bf-135">Azure, açık hello web uygulaması denetim dikey ve geliştirme araçları altında açmak **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="905bf-135">In Azure, open hello web app control blade, and under Development Tools, open **Extensions**.</span></span> <span data-ttu-id="905bf-136">Merhaba Application Insights uzantısını silin.</span><span class="sxs-lookup"><span data-stu-id="905bf-136">Delete hello Application Insights extension.</span></span> <span data-ttu-id="905bf-137">Ardından altında izleme, Application Insights'ı seçin ve oluşturmak veya istediğiniz hello kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="905bf-137">Then under Monitoring, choose Application Insights and create or select hello resource you want.</span></span>

## <a name="build-hello-app-with-application-insights"></a><span data-ttu-id="905bf-138">Application Insights ile Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="905bf-138">Build hello app with Application Insights</span></span>
<span data-ttu-id="905bf-139">Application Insights, uygulamanıza bir SDK yükleyerek daha ayrıntılı telemetri sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="905bf-139">Application Insights can provide more detailed telemetry by installing an SDK into your app.</span></span> <span data-ttu-id="905bf-140">Bunların başında izleme günlüklerini toplama, [özel telemetri yazma](app-insights-api-custom-events-metrics.md) ve daha ayrıntılı özel durum raporları alma gelir.</span><span class="sxs-lookup"><span data-stu-id="905bf-140">In particular, you can collect trace logs, [write custom telemetry](app-insights-api-custom-events-metrics.md), and get more detailed exception reports.</span></span>

1. <span data-ttu-id="905bf-141">**Visual Studio**’da (2013 güncelleştirme 2 veya sonraki sürümler), projeniz için Application Insights’ı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="905bf-141">**In Visual Studio** (2013 update 2 or later), configure Application Insights for your project.</span></span>

    <span data-ttu-id="905bf-142">Merhaba web projesine sağ tıklayın ve seçin **Ekle > Application Insights** veya **yapılandırma Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="905bf-142">Right-click hello web project, and select **Add > Application Insights** or **Configure Application Insights**.</span></span>
   
    ![Merhaba web projesine sağ tıklayın ve Ekle veya yapılandırma Application Insights'ı seçin](./media/app-insights-azure-web-apps/03-add.png)
   
    <span data-ttu-id="905bf-144">İçinde toosign sorulursa hello kimlik Azure hesabınız için kullanın.</span><span class="sxs-lookup"><span data-stu-id="905bf-144">If you're asked toosign in, use hello credentials for your Azure account.</span></span>
   
    <span data-ttu-id="905bf-145">Merhaba işlemi iki etkilere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="905bf-145">hello operation has two effects:</span></span>
   
   1. <span data-ttu-id="905bf-146">Azure’da telemetrinin depolanacağı, analiz edileceği ve görüntüleneceği bir Application Insights kaynağı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="905bf-146">Creates an Application Insights resource in Azure, where telemetry is stored, analyzed and displayed.</span></span>
   2. <span data-ttu-id="905bf-147">Merhaba (Bu zaten yoksa) uygulama Öngörüler NuGet paket tooyour kodu ekler ve toosend telemetri toohello Azure kaynak yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="905bf-147">Adds hello Application Insights NuGet package tooyour code (if it isn't there already), and configures it toosend telemetry toohello Azure resource.</span></span>
2. <span data-ttu-id="905bf-148">**Test hello telemetri** çalışan hello uygulama geliştirme makinenizdeki (F5) tarafından.</span><span class="sxs-lookup"><span data-stu-id="905bf-148">**Test hello telemetry** by running hello app in your development machine (F5).</span></span>
3. <span data-ttu-id="905bf-149">**Merhaba uygulama yayımlama** hello tooAzure her zamanki gibi.</span><span class="sxs-lookup"><span data-stu-id="905bf-149">**Publish hello app** tooAzure in hello usual way.</span></span> 

<span data-ttu-id="905bf-150">*Toosending tooa farklı Application Insights kaynağı nasıl geçiş yapabilirim?*</span><span class="sxs-lookup"><span data-stu-id="905bf-150">*How do I switch toosending tooa different Application Insights resource?*</span></span>

* <span data-ttu-id="905bf-151">Visual Studio'da, sağ hello proje **yapılandırma Application Insights** ve istediğiniz hello kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="905bf-151">In Visual Studio, right-click hello project, choose **Configure Application Insights** and choose hello resource you want.</span></span> <span data-ttu-id="905bf-152">Yeni bir kaynak hello seçeneği toocreate alın.</span><span class="sxs-lookup"><span data-stu-id="905bf-152">You get hello option toocreate a new resource.</span></span> <span data-ttu-id="905bf-153">Yeniden derleyin ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="905bf-153">Rebuild and redeploy.</span></span>

## <a name="explore-hello-data"></a><span data-ttu-id="905bf-154">Merhaba veri keşfedin</span><span class="sxs-lookup"><span data-stu-id="905bf-154">Explore hello data</span></span>
1. <span data-ttu-id="905bf-155">Merhaba Application Insights dikey penceresinde, web uygulama Denetim Masası'nın ikinci bir veya iki bunların içinde istekleri ve hataları gösterir Canlı ölçümlerini görmek gerçekleşen.</span><span class="sxs-lookup"><span data-stu-id="905bf-155">On hello Application Insights blade of your web app control panel, you see Live Metrics, which shows requests and failures within a second or two of them occurring.</span></span> <span data-ttu-id="905bf-156">Uygulamanızı yeniden yayımlıyorsanız herhangi bir sorunu anında görmenizi sağlayan bu ekran çok kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="905bf-156">It's very useful display when you're republishing your app - you can see any problems immediately.</span></span>
2. <span data-ttu-id="905bf-157">Toohello tam Application Insights kaynağı ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="905bf-157">Click through toohello full Application Insights resource.</span></span>

    ![Tıklayarak gitme](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    <span data-ttu-id="905bf-159">Kaynağa doğrudan Azure kaynak gezintisinden de gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="905bf-159">You can also go there either directly from Azure resource navigation.</span></span>

1. <span data-ttu-id="905bf-160">Tüm grafik tooget daha fazla ayrıntı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="905bf-160">Click through any chart tooget more detail:</span></span>
   
    ![Bir grafik Hello Application Insights genel bakış dikey penceresinde](./media/app-insights-azure-web-apps/07-dependency.png)
   
    <span data-ttu-id="905bf-162">[Ölçüm dikey pencerelerini özelleştirme](app-insights-metrics-explorer.md) olanağınız vardır.</span><span class="sxs-lookup"><span data-stu-id="905bf-162">You can [customize metrics blades](app-insights-metrics-explorer.md).</span></span>
2. <span data-ttu-id="905bf-163">Daha fazla toosee olayları tek tek ve bunların özelliklerini tıklatın:</span><span class="sxs-lookup"><span data-stu-id="905bf-163">Click through further toosee individual events and their properties:</span></span>
   
    ![Bir arama, o türde filtre uygulanmış bir olay türü tooopen tıklatın](./media/app-insights-azure-web-apps/08-requests.png)
   
    <span data-ttu-id="905bf-165">Bağlantı tooopen tüm özellikleri "..." Merhaba dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="905bf-165">Notice hello "..." link tooopen all properties.</span></span>
   
    <span data-ttu-id="905bf-166">[Aramaları özelleştirme](app-insights-diagnostic-search.md) olanağınız vardır.</span><span class="sxs-lookup"><span data-stu-id="905bf-166">You can [customize searches](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="905bf-167">Merhaba telemetrinizi üzerinden daha güçlü arar kullanmak [günlük analizi sorgu dili](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="905bf-167">For more powerful searches over your telemetry, use hello [Log Analytics query language](app-insights-analytics-tour.md).</span></span>

## <a name="more-telemetry"></a><span data-ttu-id="905bf-168">Daha fazla telemetri</span><span class="sxs-lookup"><span data-stu-id="905bf-168">More telemetry</span></span>

* [<span data-ttu-id="905bf-169">Web sayfası yükleme verileri</span><span class="sxs-lookup"><span data-stu-id="905bf-169">Web page load data</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="905bf-170">Özel telemetri</span><span class="sxs-lookup"><span data-stu-id="905bf-170">Custom telemetry</span></span>](app-insights-api-custom-events-metrics.md)

## <a name="video"></a><span data-ttu-id="905bf-171">Video</span><span class="sxs-lookup"><span data-stu-id="905bf-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="905bf-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="905bf-172">Next steps</span></span>
* <span data-ttu-id="905bf-173">[Canlı uygulamanızı üzerinde Hello profil oluşturucu çalıştırma](app-insights-profiler.md).</span><span class="sxs-lookup"><span data-stu-id="905bf-173">[Run hello profiler on your live app](app-insights-profiler.md).</span></span>
* <span data-ttu-id="905bf-174">[Azure İşlevleri](https://github.com/christopheranderson/azure-functions-app-insights-sample) - Application Insights ile Azure İşlevlerini izleyin</span><span class="sxs-lookup"><span data-stu-id="905bf-174">[Azure Functions](https://github.com/christopheranderson/azure-functions-app-insights-sample) - monitor Azure Functions with Application Insights</span></span>
* <span data-ttu-id="905bf-175">[Azure Tanılama'yı etkinleştirmek](app-insights-azure-diagnostics.md) gönderilen toobe tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="905bf-175">[Enable Azure diagnostics](app-insights-azure-diagnostics.md) toobe sent tooApplication Insights.</span></span>
* <span data-ttu-id="905bf-176">[İzleme hizmeti sistem durumu ölçümleri](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.</span><span class="sxs-lookup"><span data-stu-id="905bf-176">[Monitor service health metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
* <span data-ttu-id="905bf-177">İşletimsel olaylar gerçekleştiğinde ya da ölçümler bir eşiği aştığında [uyarı bildirimleri alın](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="905bf-177">[Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) whenever operational events happen or metrics cross a threshold.</span></span>
* <span data-ttu-id="905bf-178">Kullanım [JavaScript uygulamaları ve web sayfaları için Application Insights](app-insights-javascript.md) tooget istemci telemetri hello tarayıcılardan bir web sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="905bf-178">Use [Application Insights for JavaScript apps and web pages](app-insights-javascript.md) tooget client telemetry from hello browsers that visit a web page.</span></span>
* <span data-ttu-id="905bf-179">[Kullanılabilirlik web testleri oluşturma](app-insights-monitor-web-app-availability.md) sitenizi kapalı olduğunda uyarı toobe.</span><span class="sxs-lookup"><span data-stu-id="905bf-179">[Set up Availability web tests](app-insights-monitor-web-app-availability.md) toobe alerted if your site is down.</span></span>

