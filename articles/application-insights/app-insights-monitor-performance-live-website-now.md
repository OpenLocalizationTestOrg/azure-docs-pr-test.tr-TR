---
title: "aaaMonitor canlı bir ASP.NET web uygulaması Azure Application Insights ile | Microsoft Docs"
description: "Yeniden dağıtmadan web sitesinin performansını izleme. Şirket içinde, sanal makinelerde veya Azure üzerinde ASP.NET web uygulamaları ile çalışır."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a><span data-ttu-id="e7602-104">Application Insights ile çalışma zamanında web uygulamalarını izleme</span><span class="sxs-lookup"><span data-stu-id="e7602-104">Instrument web apps at runtime with Application Insights</span></span>


<span data-ttu-id="e7602-105">Azure Application Insights, canlı web uygulamasıyla toomodify gerek kalmadan izleme ya da kodunuzu yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e7602-105">You can instrument a live web app with Azure Application Insights, without having toomodify or redeploy your code.</span></span> <span data-ttu-id="e7602-106">Uygulamalarınız şirket içi IIS sunucusu tarafından barındırılıyorsa, Durum İzleyicisi’ni yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e7602-106">If your apps are hosted by an on-premises IIS server, install Status Monitor.</span></span> <span data-ttu-id="e7602-107">Azure web uygulamaları olduğunuz veya bir Azure VM çalıştırmak, Application Insights hello Azure Denetim Masası'ndan izleme geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7602-107">If they're Azure web apps or run in an Azure VM, you can switch on Application Insights monitoring from hello Azure control panel.</span></span> <span data-ttu-id="e7602-108">([Canlı J2EE web uygulamaları](app-insights-java-live.md) ve [Azure Cloud Services](app-insights-cloudservices.md) izleme hakkında ayrı makaleler de vardır.) [Microsoft Azure](http://azure.com) aboneliğiniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7602-108">(There are also separate articles about instrumenting [live J2EE web apps](app-insights-java-live.md) and [Azure Cloud Services](app-insights-cloudservices.md).) You need a [Microsoft Azure](http://azure.com) subscription.</span></span>

![örnek grafikler](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

<span data-ttu-id="e7602-110">Üç yollar tooapply Application Insights tooyour .NET web uygulamalarının seçenekleriniz vardır:</span><span class="sxs-lookup"><span data-stu-id="e7602-110">You have a choice of three routes tooapply Application Insights tooyour .NET web applications:</span></span>

* <span data-ttu-id="e7602-111">**Derleme süresi:** [Ekle hello Application Insights SDK'sı] [ greenbrown] tooyour web uygulama kodu.</span><span class="sxs-lookup"><span data-stu-id="e7602-111">**Build time:** [Add hello Application Insights SDK][greenbrown] tooyour web app code.</span></span>
* <span data-ttu-id="e7602-112">**Çalışma zamanı:** yeniden oluşturma ve hello kod dağıtarak, aşağıda açıklandığı gibi hello sunucuda web uygulamanızı izleme.</span><span class="sxs-lookup"><span data-stu-id="e7602-112">**Run time:** Instrument your web app on hello server, as described below, without rebuilding and redeploying hello code.</span></span>
* <span data-ttu-id="e7602-113">**Her ikisi:** web uygulaması kodunuza hello SDK derleme ve hello çalışma zamanı uzantıları de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e7602-113">**Both:** Build hello SDK into your web app code, and also apply hello run-time extensions.</span></span> <span data-ttu-id="e7602-114">Merhaba her iki seçenek en iyi alın.</span><span class="sxs-lookup"><span data-stu-id="e7602-114">Get hello best of both options.</span></span>

<span data-ttu-id="e7602-115">Burada, her yöntemle kazanacaklarınızın bir özeti verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e7602-115">Here's a summary of what you get by each route:</span></span>

|  | <span data-ttu-id="e7602-116">Derleme zamanı</span><span class="sxs-lookup"><span data-stu-id="e7602-116">Build time</span></span> | <span data-ttu-id="e7602-117">Çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="e7602-117">Run time</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7602-118">İstekler ve özel durumlar</span><span class="sxs-lookup"><span data-stu-id="e7602-118">Requests & exceptions</span></span> |<span data-ttu-id="e7602-119">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-119">Yes</span></span> |<span data-ttu-id="e7602-120">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-120">Yes</span></span> |
| [<span data-ttu-id="e7602-121">Daha ayrıntılı özel durumlar</span><span class="sxs-lookup"><span data-stu-id="e7602-121">More detailed exceptions</span></span>](app-insights-asp-net-exceptions.md) | |<span data-ttu-id="e7602-122">Yes</span><span class="sxs-lookup"><span data-stu-id="e7602-122">Yes</span></span> |
| [<span data-ttu-id="e7602-123">Bağımlılık tanılaması</span><span class="sxs-lookup"><span data-stu-id="e7602-123">Dependency diagnostics</span></span>](app-insights-asp-net-dependencies.md) |<span data-ttu-id="e7602-124">.NET 4.6+ üzerinde ancak daha az ayrıntılı</span><span class="sxs-lookup"><span data-stu-id="e7602-124">On .NET 4.6+, but less detail</span></span> |<span data-ttu-id="e7602-125">Evet, tam ayrıntılı: sonuç kodları, SQL komut metni, HTTP fiili</span><span class="sxs-lookup"><span data-stu-id="e7602-125">Yes, full detail: result codes, SQL command text, HTTP verb</span></span>|
| [<span data-ttu-id="e7602-126">Sistem performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="e7602-126">System performance counters</span></span>](app-insights-performance-counters.md) |<span data-ttu-id="e7602-127">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-127">Yes</span></span> |<span data-ttu-id="e7602-128">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-128">Yes</span></span> |
| <span data-ttu-id="e7602-129">[Özel telemetri için API][api]</span><span class="sxs-lookup"><span data-stu-id="e7602-129">[API for custom telemetry][api]</span></span> |<span data-ttu-id="e7602-130">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-130">Yes</span></span> |<span data-ttu-id="e7602-131">Hayır</span><span class="sxs-lookup"><span data-stu-id="e7602-131">No</span></span> |
| [<span data-ttu-id="e7602-132">İzleme günlüğü tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="e7602-132">Trace log integration</span></span>](app-insights-asp-net-trace-logs.md) |<span data-ttu-id="e7602-133">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-133">Yes</span></span> |<span data-ttu-id="e7602-134">Hayır</span><span class="sxs-lookup"><span data-stu-id="e7602-134">No</span></span> |
| [<span data-ttu-id="e7602-135">Sayfa görünümü ve kullanıcı verileri</span><span class="sxs-lookup"><span data-stu-id="e7602-135">Page view & user data</span></span>](app-insights-javascript.md) |<span data-ttu-id="e7602-136">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-136">Yes</span></span> |<span data-ttu-id="e7602-137">Hayır</span><span class="sxs-lookup"><span data-stu-id="e7602-137">No</span></span> |
| <span data-ttu-id="e7602-138">Toorebuild kodu gerekli</span><span class="sxs-lookup"><span data-stu-id="e7602-138">Need toorebuild code</span></span> |<span data-ttu-id="e7602-139">Evet</span><span class="sxs-lookup"><span data-stu-id="e7602-139">Yes</span></span> | <span data-ttu-id="e7602-140">Hayır</span><span class="sxs-lookup"><span data-stu-id="e7602-140">No</span></span> |


## <a name="monitor-a-live-azure-web-app"></a><span data-ttu-id="e7602-141">Canlı bir Azure web uygulamasını izleme</span><span class="sxs-lookup"><span data-stu-id="e7602-141">Monitor a live Azure web app</span></span>

<span data-ttu-id="e7602-142">Uygulamanız bir Azure web Service'in, burada çalışıp çalışmadığını nasıl izleme tooswitch:</span><span class="sxs-lookup"><span data-stu-id="e7602-142">If your application is running as an Azure web service, here's how tooswitch on monitoring:</span></span>

* <span data-ttu-id="e7602-143">Azure'da hello uygulamanın Denetim Masası'Application Insights'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7602-143">Select Application Insights on hello app's control panel in Azure.</span></span>

    ![Bir Azure web uygulaması için Application Insights’ı ayarlama](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* <span data-ttu-id="e7602-145">Merhaba Application Insights Özet sayfası açıldığında, hello alt tooopen hello tam Application Insights kaynağı hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e7602-145">When hello Application Insights summary page opens, click hello link at hello bottom tooopen hello full Application Insights resource.</span></span>

    ![TooApplication Insights'ı tıklatın](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

<span data-ttu-id="e7602-147">[Bulut ve VM uygulamalarını izleme](app-insights-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e7602-147">[Monitoring Cloud and VM apps](app-insights-azure.md).</span></span>

### <a name="enable-client-side-monitoring-in-azure"></a><span data-ttu-id="e7602-148">Azure'da istemci tarafı izlemeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e7602-148">Enable client-side monitoring in Azure</span></span>

<span data-ttu-id="e7602-149">Azure'da Application Insights'ı etkinleştirdiyseniz sayfa görüntülemesi ve kullanıcı telemetrisi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7602-149">If you have enabled Application Insights in Azure, you can add page view and user telemetry.</span></span>

1. <span data-ttu-id="e7602-150">Ayarlar > Uygulama Ayarları'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7602-150">Select Settings > Application Settings</span></span>
2.  <span data-ttu-id="e7602-151">Uygulama Ayarları'nın altında yeni bir anahtar değer çifti ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e7602-151">Under App Settings, add a new key value pair:</span></span> 
   
    <span data-ttu-id="e7602-152">Anahtar: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span><span class="sxs-lookup"><span data-stu-id="e7602-152">Key: `APPINSIGHTS_JAVASCRIPT_ENABLED`</span></span> 
    
    <span data-ttu-id="e7602-153">Değer:`true`</span><span class="sxs-lookup"><span data-stu-id="e7602-153">Value: `true`</span></span>
3. <span data-ttu-id="e7602-154">**Kaydet** hello ayarları ve **yeniden** uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="e7602-154">**Save** hello settings and **Restart** your app.</span></span>

<span data-ttu-id="e7602-155">Merhaba Application Insights JavaScript SDK'sı şimdi her web sayfasına eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="e7602-155">hello Application Insights JavaScript SDK is now injected into each web page.</span></span>

## <a name="monitor-a-live-iis-web-app"></a><span data-ttu-id="e7602-156">Canlı bir IIS web uygulamasını izleme</span><span class="sxs-lookup"><span data-stu-id="e7602-156">Monitor a live IIS web app</span></span>

<span data-ttu-id="e7602-157">Uygulamanız bir IIS sunucusunda barındırılıyorsa, Durum İzleyici’yi kullanarak Application Insights’ı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7602-157">If your app is hosted on an IIS server, enable Application Insights by using Status Monitor.</span></span>

1. <span data-ttu-id="e7602-158">IIS web sunucunuzda yönetici kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e7602-158">On your IIS web server, sign in with administrator credentials.</span></span>
2. <span data-ttu-id="e7602-159">Application Insights Durum İzleyicisi zaten yüklü değilse, indirme ve hello çalıştırma [Durum İzleyicisi yükleyici](http://go.microsoft.com/fwlink/?LinkId=506648) (veya çalıştırmak [Web Platformu yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx) ve uygulama Öngörüler durumu da arayın İzleyici).</span><span class="sxs-lookup"><span data-stu-id="e7602-159">If Application Insights Status Monitor is not already installed, download and run hello [Status Monitor installer](http://go.microsoft.com/fwlink/?LinkId=506648) (or run [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) and search in it for Application Insights Status Monitor).</span></span>
3. <span data-ttu-id="e7602-160">Durum İzleyicisi'nde hello yüklü web uygulaması veya toomonitor istediğiniz Web sitesi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7602-160">In Status Monitor, select hello installed web application or website that you want toomonitor.</span></span> <span data-ttu-id="e7602-161">Azure kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e7602-161">Sign in with your Azure credentials.</span></span>

    <span data-ttu-id="e7602-162">Merhaba kaynak toosee hello sonuçları hello Application Insights portalında istediğiniz yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="e7602-162">Configure hello resource where you want toosee hello results in hello Application Insights portal.</span></span> <span data-ttu-id="e7602-163">(Normalde, en iyi toocreate yeni bir kaynak olur.</span><span class="sxs-lookup"><span data-stu-id="e7602-163">(Normally, it's best toocreate a new resource.</span></span> <span data-ttu-id="e7602-164">Bu uygulama için zaten [web testleriniz][availability] veya [istemci izleme][client] özelliği varsa mevcut bir kaynağı seçin.)</span><span class="sxs-lookup"><span data-stu-id="e7602-164">Select an existing resource if you already have [web tests][availability] or [client monitoring][client] for this app.)</span></span> 

    ![Uygulama ve kaynak seçin.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. <span data-ttu-id="e7602-166">IIS’yi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e7602-166">Restart IIS.</span></span>

    ![Merhaba iletişim hello üstündeki yeniden Başlat'ı seçin.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    <span data-ttu-id="e7602-168">Web hizmetiniz kısa bir süre kesintiye uğrar.</span><span class="sxs-lookup"><span data-stu-id="e7602-168">Your web service is interrupted for a short while.</span></span>

## <a name="customize-monitoring-options"></a><span data-ttu-id="e7602-169">İzlemeyi özelleştirme seçenekleri</span><span class="sxs-lookup"><span data-stu-id="e7602-169">Customize monitoring options</span></span>

<span data-ttu-id="e7602-170">Application Insights etkinleştirilmesi ekler DLL'ler ve Applicationınsights.config tooyour web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e7602-170">Enabling Application Insights adds DLLs and ApplicationInsights.config tooyour web app.</span></span> <span data-ttu-id="e7602-171">Yapabilecekleriniz [hello .config dosyasını düzenleyin](app-insights-configuration-with-applicationinsights-config.md) toochange bazı hello seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="e7602-171">You can [edit hello .config file](app-insights-configuration-with-applicationinsights-config.md) toochange some of hello options.</span></span>

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a><span data-ttu-id="e7602-172">Uygulamanızı yeniden yayımladığınızda, Application Insights’ı yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="e7602-172">When you re-publish your app, re-enable Application Insights</span></span>

<span data-ttu-id="e7602-173">Uygulamanızı yeniden yayımlamadan önce göz önünde bulundurun [Visual Studio'da Application Insights toohello kod ekleme][greenbrown].</span><span class="sxs-lookup"><span data-stu-id="e7602-173">Before you re-publish your app, consider [adding Application Insights toohello code in Visual Studio][greenbrown].</span></span> <span data-ttu-id="e7602-174">Daha ayrıntılı telemetri ve hello özelliği toowrite özel telemetri elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="e7602-174">You'll get more detailed telemetry and hello ability toowrite custom telemetry.</span></span>

<span data-ttu-id="e7602-175">Toore istiyorsanız-Application Insights toohello kodu eklemeden yayımlama, hello dağıtım işlemini hello DLL'leri Sil ve Applicationınsights.config hello gelen yayımlanan web sitesi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e7602-175">If you want toore-publish without adding Application Insights toohello code, be aware that hello deployment process may delete hello DLLs and ApplicationInsights.config from hello published web site.</span></span> <span data-ttu-id="e7602-176">Bu nedenle:</span><span class="sxs-lookup"><span data-stu-id="e7602-176">Therefore:</span></span>

1. <span data-ttu-id="e7602-177">ApplicationInsights.config dosyasını düzenlediyseniz, uygulamanızı yeniden yayımlamadan önce bir kopyasını alın.</span><span class="sxs-lookup"><span data-stu-id="e7602-177">If you edited ApplicationInsights.config, take a copy of it before you re-publish your app.</span></span>
2. <span data-ttu-id="e7602-178">Uygulamanızı yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e7602-178">Republish your app.</span></span>
3. <span data-ttu-id="e7602-179">Application Insights izlemeyi yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e7602-179">Re-enable Application Insights monitoring.</span></span> <span data-ttu-id="e7602-180">(Merhaba uygun yöntemi kullanın: hello Azure web uygulaması Denetim Masası veya bir IIS konaktaki Durum İzleyicisi Merhaba.)</span><span class="sxs-lookup"><span data-stu-id="e7602-180">(Use hello appropriate method: either hello Azure web app control panel, or hello Status Monitor on an IIS host.)</span></span>
4. <span data-ttu-id="e7602-181">Merhaba .config dosyası üzerinde gerçekleştirilen herhangi bir düzenleme yeniden devreye sokmanız.</span><span class="sxs-lookup"><span data-stu-id="e7602-181">Reinstate any edits you performed on hello .config file.</span></span>


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a><span data-ttu-id="e7602-182">Application Insights çalışma zamanı yapılandırma sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="e7602-182">Troubleshooting runtime configuration of Application Insights</span></span>

### <a name="cant-connect-no-telemetry"></a><span data-ttu-id="e7602-183">Bağlanamıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="e7602-183">Can't connect?</span></span> <span data-ttu-id="e7602-184">Telemetri yok mu?</span><span class="sxs-lookup"><span data-stu-id="e7602-184">No telemetry?</span></span>

* <span data-ttu-id="e7602-185">Açık [hello gerekli giden bağlantı noktaları](app-insights-ip-addresses.md#outgoing-ports) sunucunuzun güvenlik duvarı tooallow Durum İzleyicisi toowork içinde.</span><span class="sxs-lookup"><span data-stu-id="e7602-185">Open [hello necessary outgoing ports](app-insights-ip-addresses.md#outgoing-ports) in your server's firewall tooallow Status Monitor toowork.</span></span>

* <span data-ttu-id="e7602-186">Durum İzleyicisi’ni açın ve sol bölmede uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7602-186">Open Status Monitor and select your application on left pane.</span></span> <span data-ttu-id="e7602-187">Bu uygulamada hello "Yapılandırma bildirimleri" bölümü için herhangi bir tanılama iletisi olup olmadığını denetleyin:</span><span class="sxs-lookup"><span data-stu-id="e7602-187">Check if there are any diagnostics messages for this application in hello "Configuration notifications" section:</span></span>

  ![Merhaba performans dikey toosee istek, yanıt süresi, bağımlılık ve diğer verileri açın](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* <span data-ttu-id="e7602-189">"Yetersiz izinler" hakkında bir ileti görürseniz, hello sunucuda hello aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="e7602-189">On hello server, if you see a message about "insufficient permissions", try hello following:</span></span>
  * <span data-ttu-id="e7602-190">IIS Yöneticisi'nde, uygulama havuzunu seçin açmak **Gelişmiş ayarları**ve altında **işlem modeli** hello kimliğini not edin.</span><span class="sxs-lookup"><span data-stu-id="e7602-190">In IIS Manager, select your application pool, open **Advanced Settings**, and under **Process Model** note hello identity.</span></span>
  * <span data-ttu-id="e7602-191">Bilgisayar Yönetimi Denetim Masası'nda bu kimlik toohello Performans İzleyicisi kullanıcıları grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e7602-191">In Computer management control panel, add this identity toohello Performance Monitor Users group.</span></span>
* <span data-ttu-id="e7602-192">Sunucunuza yüklenmiş MMA/SCOM (System Center Operations Manager) varsa bazı sürümler çakışabilir.</span><span class="sxs-lookup"><span data-stu-id="e7602-192">If you have MMA/SCOM (Systems Center Operations Manager) installed on your server, some versions can conflict.</span></span> <span data-ttu-id="e7602-193">Hem SCOM'u hem de Durum İzleyicisi'ni kaldırın ve hello en son sürümleri yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e7602-193">Uninstall both SCOM and Status Monitor, and re-install hello latest versions.</span></span>
* <span data-ttu-id="e7602-194">Bkz. [Sorun giderme][qna].</span><span class="sxs-lookup"><span data-stu-id="e7602-194">See [Troubleshooting][qna].</span></span>

## <a name="system-requirements"></a><span data-ttu-id="e7602-195">Sistem Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="e7602-195">System Requirements</span></span>
<span data-ttu-id="e7602-196">Sunucuda Application Insights Durum İzleyicisi için işletim sistemi desteği:</span><span class="sxs-lookup"><span data-stu-id="e7602-196">OS support for Application Insights Status Monitor on Server:</span></span>

* <span data-ttu-id="e7602-197">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="e7602-197">Windows Server 2008</span></span>
* <span data-ttu-id="e7602-198">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="e7602-198">Windows Server 2008 R2</span></span>
* <span data-ttu-id="e7602-199">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e7602-199">Windows Server 2012</span></span>
* <span data-ttu-id="e7602-200">Windows server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e7602-200">Windows server 2012 R2</span></span>
* <span data-ttu-id="e7602-201">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e7602-201">Windows Server 2016</span></span>

<span data-ttu-id="e7602-202">en son SP ve .NET Framework 4.5 ile</span><span class="sxs-lookup"><span data-stu-id="e7602-202">with latest SP and .NET Framework 4.5</span></span>

<span data-ttu-id="e7602-203">Merhaba istemci tarafında: Windows 7, 8, 8.1 ve 10, .NET Framework 4.5 ile yeniden</span><span class="sxs-lookup"><span data-stu-id="e7602-203">On hello client side: Windows 7, 8, 8.1 and 10, again with .NET Framework 4.5</span></span>

<span data-ttu-id="e7602-204">IIS desteği: IIS 7, 7.5, 8, 8.5 (IIS gereklidir)</span><span class="sxs-lookup"><span data-stu-id="e7602-204">IIS support is: IIS 7, 7.5, 8, 8.5 (IIS is required)</span></span>

## <a name="automation-with-powershell"></a><span data-ttu-id="e7602-205">PowerShell ile Automation</span><span class="sxs-lookup"><span data-stu-id="e7602-205">Automation with PowerShell</span></span>
<span data-ttu-id="e7602-206">IIS sunucunuzda PowerShell'i kullanarak izlemeyi başlatabilir ve durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7602-206">You can start and stop monitoring by using PowerShell on your IIS server.</span></span>

<span data-ttu-id="e7602-207">İlk hello Application Insights modülünü içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="e7602-207">First import hello Application Insights module:</span></span>

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

<span data-ttu-id="e7602-208">Hangi uygulamaların izlenmekte olduğunu öğrenin:</span><span class="sxs-lookup"><span data-stu-id="e7602-208">Find out which apps are being monitored:</span></span>

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* <span data-ttu-id="e7602-209">`-Name`Bir web uygulaması adı (isteğe bağlı) hello.</span><span class="sxs-lookup"><span data-stu-id="e7602-209">`-Name` (Optional) hello name of a web app.</span></span>
* <span data-ttu-id="e7602-210">Görüntüler, bu IIS sunucusundaki her web uygulaması (veya uygulama adlı hello) Application Insights izleme durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="e7602-210">Displays hello Application Insights monitoring status for each web app (or hello named app) in this IIS server.</span></span>
* <span data-ttu-id="e7602-211">Her uygulama için `ApplicationInsightsApplication` döndürür:</span><span class="sxs-lookup"><span data-stu-id="e7602-211">Returns `ApplicationInsightsApplication` for each app:</span></span>

  * <span data-ttu-id="e7602-212">`SdkState==EnabledAfterDeployment`: Uygulama izlenmektedir ve çalışma zamanında hello Durum İzleyicisi aracıyla veya tarafından izlendi `Start-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="e7602-212">`SdkState==EnabledAfterDeployment`: App is being monitored, and was instrumented at run time, either by hello Status Monitor tool, or by `Start-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="e7602-213">`SdkState==Disabled`: hello uygulama için Application Insights değil işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="e7602-213">`SdkState==Disabled`: hello app is not instrumented for Application Insights.</span></span> <span data-ttu-id="e7602-214">Hiçbir zaman izlendi ya da çalışma zamanı izlemesi devre dışı hello Durum İzleyicisi aracıyla veya ile `Stop-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="e7602-214">Either it was never instrumented, or run-time monitoring was disabled with hello Status Monitor tool or with `Stop-ApplicationInsightsMonitoring`.</span></span>
  * <span data-ttu-id="e7602-215">`SdkState==EnabledByCodeInstrumentation`: hello uygulama izlenmiş hello SDK toohello kaynak kodu ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="e7602-215">`SdkState==EnabledByCodeInstrumentation`: hello app was instrumented by adding hello SDK toohello source code.</span></span> <span data-ttu-id="e7602-216">SDK’si güncelleştirilemez veya durdurulamaz.</span><span class="sxs-lookup"><span data-stu-id="e7602-216">Its SDK cannot be updated or stopped.</span></span>
  * <span data-ttu-id="e7602-217">`SdkVersion`Bu uygulamanın izlenmesi için kullanımda Hello sürümünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="e7602-217">`SdkVersion` shows hello version in use for monitoring this app.</span></span>
  * <span data-ttu-id="e7602-218">`LatestAvailableSdkVersion`şu anda kullanılabilir Hello sürüm hello NuGet galerisinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="e7602-218">`LatestAvailableSdkVersion`shows hello version currently available on hello NuGet gallery.</span></span> <span data-ttu-id="e7602-219">tooupgrade hello uygulamanın toothis sürüm, kullanım `Update-ApplicationInsightsMonitoring`.</span><span class="sxs-lookup"><span data-stu-id="e7602-219">tooupgrade hello app toothis version, use `Update-ApplicationInsightsMonitoring`.</span></span>

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* <span data-ttu-id="e7602-220">`-Name`IIS'de hello uygulamasının Hello adı</span><span class="sxs-lookup"><span data-stu-id="e7602-220">`-Name` hello name of hello app in IIS</span></span>
* <span data-ttu-id="e7602-221">`-InstrumentationKey`Merhaba hello sonuçları toobe görüntülenmesini istediğiniz Application Insights kaynağı ikey hello.</span><span class="sxs-lookup"><span data-stu-id="e7602-221">`-InstrumentationKey` hello ikey of hello Application Insights resource where you want hello results toobe displayed.</span></span>
* <span data-ttu-id="e7602-222">Bu cmdlet yalnızca henüz izlenmemiş uygulamaları etkiler; başka bir deyişle zaten işaretlendiğine değil - diğer bir deyişle, SdkState==NotInstrumented.</span><span class="sxs-lookup"><span data-stu-id="e7602-222">This cmdlet only affects apps that are not already instrumented - that is, SdkState==NotInstrumented.</span></span>

    <span data-ttu-id="e7602-223">Merhaba cmdlet, zaten izlenmiş olan uygulamayı etkilemez.</span><span class="sxs-lookup"><span data-stu-id="e7602-223">hello cmdlet does not affect an app that is already instrumented.</span></span> <span data-ttu-id="e7602-224">Bırakmaz hello uygulama hello SDK toohello kodu ekleyerek derleme zamanında izlenmektedir olup olmadığını önemli, veya bu cmdlet'in önceki bir kullanımıyla çalışma zamanı sırasında.</span><span class="sxs-lookup"><span data-stu-id="e7602-224">It does not matter whether hello app was instrumented at build time by adding hello SDK toohello code, or at run time by a previous use of this cmdlet.</span></span>

    <span data-ttu-id="e7602-225">Merhaba SDK kullanılan sürümü tooinstrument hello son çoğu hello sürüm toothis Sunucusu'nu indirdiğiniz uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="e7602-225">hello SDK version used tooinstrument hello app is hello version that was most recently downloaded toothis server.</span></span>

    <span data-ttu-id="e7602-226">toodownload hello en son sürümü, Update-Applicationınsightsversion kullanın.</span><span class="sxs-lookup"><span data-stu-id="e7602-226">toodownload hello latest version, use Update-ApplicationInsightsVersion.</span></span>
* <span data-ttu-id="e7602-227">Başarılı bir şekilde `ApplicationInsightsApplication` döndürür.</span><span class="sxs-lookup"><span data-stu-id="e7602-227">Returns `ApplicationInsightsApplication` on success.</span></span> <span data-ttu-id="e7602-228">Başarısız olursa izleme toostderr günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e7602-228">If it fails, it logs a trace toostderr.</span></span>

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* <span data-ttu-id="e7602-229">`-Name`IIS'de bir uygulamanın Hello adı</span><span class="sxs-lookup"><span data-stu-id="e7602-229">`-Name` hello name of an app in IIS</span></span>
* <span data-ttu-id="e7602-230">`-All` Bu IIS sunucusunda, şu koşulu sağlayan tüm uygulamaları izlemeyi durdurur: `SdkState==EnabledAfterDeployment`</span><span class="sxs-lookup"><span data-stu-id="e7602-230">`-All` Stops monitoring all apps in this IIS server for which `SdkState==EnabledAfterDeployment`</span></span>
* <span data-ttu-id="e7602-231">Merhaba izlemesini durdurur, belirtilen uygulamaların ve izlemeyi kaldırır.</span><span class="sxs-lookup"><span data-stu-id="e7602-231">Stops monitoring hello specified apps and removes instrumentation.</span></span> <span data-ttu-id="e7602-232">Durum izleme aracını veya Start-Applicationınsightsapplication kullanarak çalışma zamanında izleme eklenmiş uygulamalar hello için yalnızca çalışır.</span><span class="sxs-lookup"><span data-stu-id="e7602-232">It only works for apps that have been instrumented at run-time using hello Status Monitoring tool or Start-ApplicationInsightsApplication.</span></span> <span data-ttu-id="e7602-233">(`SdkState==EnabledAfterDeployment`)</span><span class="sxs-lookup"><span data-stu-id="e7602-233">(`SdkState==EnabledAfterDeployment`)</span></span>
* <span data-ttu-id="e7602-234">ApplicationInsightsApplication döndürür.</span><span class="sxs-lookup"><span data-stu-id="e7602-234">Returns ApplicationInsightsApplication.</span></span>

<span data-ttu-id="e7602-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span><span class="sxs-lookup"><span data-stu-id="e7602-235">`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]</span></span>

* <span data-ttu-id="e7602-236">`-Name`: IIS'de web uygulamasının hello adı.</span><span class="sxs-lookup"><span data-stu-id="e7602-236">`-Name`: hello name of a web app in IIS.</span></span>
* <span data-ttu-id="e7602-237">`-InstrumentationKey` (İsteğe bağlı.) Bu toochange hello kaynak toowhich hello uygulamanın telemetri gönderildiği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e7602-237">`-InstrumentationKey` (Optional.) Use this toochange hello resource toowhich hello app's telemetry is sent.</span></span>
* <span data-ttu-id="e7602-238">Bu cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e7602-238">This cmdlet:</span></span>
  * <span data-ttu-id="e7602-239">Uygulama toohello hello SDK sürümü adlı yükseltmeler hello toothis makine en son indirilen.</span><span class="sxs-lookup"><span data-stu-id="e7602-239">Upgrades hello named app toohello version of hello SDK most recently downloaded toothis machine.</span></span> <span data-ttu-id="e7602-240">(Yalnızca `SdkState==EnabledAfterDeployment` ise çalışır)</span><span class="sxs-lookup"><span data-stu-id="e7602-240">(Only works if `SdkState==EnabledAfterDeployment`)</span></span>
  * <span data-ttu-id="e7602-241">İzleme anahtarını sağlarsanız, uygulama adlı hello yeniden yapılandırılan toosend telemetri toohello aynı anahtarla kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="e7602-241">If you provide an instrumentation key, hello named app is reconfigured toosend telemetry toohello resource with that key.</span></span> <span data-ttu-id="e7602-242">(`SdkState != Disabled` ise çalışır)</span><span class="sxs-lookup"><span data-stu-id="e7602-242">(Works if `SdkState != Disabled`)</span></span>

`Update-ApplicationInsightsVersion`

* <span data-ttu-id="e7602-243">Merhaba en son Application Insights SDK'sı toohello sunucusu yükler.</span><span class="sxs-lookup"><span data-stu-id="e7602-243">Downloads hello latest Application Insights SDK toohello server.</span></span>

## <span data-ttu-id="e7602-244"><a name="questions"></a>Durum İzleyicisi hakkında sorular</span><span class="sxs-lookup"><span data-stu-id="e7602-244"><a name="questions"></a>Questions about Status Monitor</span></span>

### <a name="what-is-status-monitor"></a><span data-ttu-id="e7602-245">Durum İzleyicisi nedir?</span><span class="sxs-lookup"><span data-stu-id="e7602-245">What is Status Monitor?</span></span>

<span data-ttu-id="e7602-246">IIS web sunucunuza yüklediğiniz bir masaüstü uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="e7602-246">A desktop application that you install in your IIS web server.</span></span> <span data-ttu-id="e7602-247">Web uygulamalarını izleyip yapılandırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e7602-247">It helps you instrument and configure web apps.</span></span> 

### <a name="when-do-i-use-status-monitor"></a><span data-ttu-id="e7602-248">Durum İzleyicisi’ni ne zaman kullanırım?</span><span class="sxs-lookup"><span data-stu-id="e7602-248">When do I use Status Monitor?</span></span>

* <span data-ttu-id="e7602-249">zaten çalışıyor olsa bile herhangi bir web uygulamanız IIS sunucunuzda - çalıştıran uygulaması tooinstrument.</span><span class="sxs-lookup"><span data-stu-id="e7602-249">tooinstrument any web app that is running on your IIS server - even if it is already running.</span></span>
* <span data-ttu-id="e7602-250">Silinmiş web uygulamaları için ek telemetri tooenable [hello Application Insights SDK'sı ile oluşturulan](app-insights-asp-net.md) derleme zamanında.</span><span class="sxs-lookup"><span data-stu-id="e7602-250">tooenable additional telemetry for web apps that have been [built with hello Application Insights SDK](app-insights-asp-net.md) at compile time.</span></span> 

### <a name="can-i-close-it-after-it-runs"></a><span data-ttu-id="e7602-251">Çalıştıktan sonra kapatabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="e7602-251">Can I close it after it runs?</span></span>

<span data-ttu-id="e7602-252">Evet.</span><span class="sxs-lookup"><span data-stu-id="e7602-252">Yes.</span></span> <span data-ttu-id="e7602-253">Seçtiğiniz hello Web siteleri izlenmiş sonra kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7602-253">After it has instrumented hello websites you select, you can close it.</span></span>

<span data-ttu-id="e7602-254">Telemetriyi tek başına toplamaz.</span><span class="sxs-lookup"><span data-stu-id="e7602-254">It doesn't collect telemetry by itself.</span></span> <span data-ttu-id="e7602-255">Yalnızca hello web uygulamaları yapılandırır ve bazı izinleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e7602-255">It just configures hello web apps and sets some permissions.</span></span>

### <a name="what-does-status-monitor-do"></a><span data-ttu-id="e7602-256">Durum İzleyicisi ne yapar?</span><span class="sxs-lookup"><span data-stu-id="e7602-256">What does Status Monitor do?</span></span>

<span data-ttu-id="e7602-257">Bir web uygulaması için Durum İzleyicisi tooinstrument seçtiğinizde:</span><span class="sxs-lookup"><span data-stu-id="e7602-257">When you select a web app for Status Monitor tooinstrument:</span></span>

* <span data-ttu-id="e7602-258">İndirir ve hello web uygulamanızın ikili dosyaları klasörüne hello Application Insights derlemeler ve .config dosyasına yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="e7602-258">Downloads and places hello Application Insights assemblies and .config file in hello web app's binaries folder.</span></span>
* <span data-ttu-id="e7602-259">Değiştirir `web.config` tooadd hello uygulama Öngörüler HTTP izleme modülü.</span><span class="sxs-lookup"><span data-stu-id="e7602-259">Modifies `web.config` tooadd hello Application Insights HTTP tracking module.</span></span>
* <span data-ttu-id="e7602-260">CLR toocollect bağımlılık çağrıları profil sağlar.</span><span class="sxs-lookup"><span data-stu-id="e7602-260">Enables CLR profiling toocollect dependency calls.</span></span>

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a><span data-ttu-id="e7602-261">Merhaba uygulama güncelleştirdiğinizde toorun Durum İzleyicisi ihtiyacım var mı?</span><span class="sxs-lookup"><span data-stu-id="e7602-261">Do I need toorun Status Monitor whenever I update hello app?</span></span>

<span data-ttu-id="e7602-262">Artımlı olarak dağıtmanız durumunda gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e7602-262">Not if you redeploy incrementally.</span></span> 

<span data-ttu-id="e7602-263">Hello hello 'var olan dosyaları silin' seçeneği belirlerseniz işlem yayımlama, toore çalıştırma Durum İzleyicisi tooconfigure Application Insights gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7602-263">If you select hello 'delete existing files' option in hello publish process, you would need toore-run Status Monitor tooconfigure Application Insights.</span></span>

### <a name="what-telemetry-is-collected"></a><span data-ttu-id="e7602-264">Hangi telemetri toplanır?</span><span class="sxs-lookup"><span data-stu-id="e7602-264">What telemetry is collected?</span></span>

<span data-ttu-id="e7602-265">Durum İzleyicisi'ni kullanarak yalnızca çalışma zamanında izlediğiniz uygulamalar için:</span><span class="sxs-lookup"><span data-stu-id="e7602-265">For applications that you instrument only at run-time by using Status Monitor:</span></span>

* <span data-ttu-id="e7602-266">HTTP istekleri</span><span class="sxs-lookup"><span data-stu-id="e7602-266">HTTP requests</span></span>
* <span data-ttu-id="e7602-267">Toodependencies çağırır</span><span class="sxs-lookup"><span data-stu-id="e7602-267">Calls toodependencies</span></span>
* <span data-ttu-id="e7602-268">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="e7602-268">Exceptions</span></span>
* <span data-ttu-id="e7602-269">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="e7602-269">Performance counters</span></span>

<span data-ttu-id="e7602-270">Derleme zamanında zaten izlenmekte olan uygulamalar için:</span><span class="sxs-lookup"><span data-stu-id="e7602-270">For applications already instrumented at compile time:</span></span>

 * <span data-ttu-id="e7602-271">İşlem sayaçları.</span><span class="sxs-lookup"><span data-stu-id="e7602-271">Process counters.</span></span>
 * <span data-ttu-id="e7602-272">Bağımlılık çağrıları (.NET 4.5); bağımlılık çağrılarındaki dönüş değerleri (.NET 4.6).</span><span class="sxs-lookup"><span data-stu-id="e7602-272">Dependency calls (.NET 4.5); return values in dependency calls (.NET 4.6).</span></span>
 * <span data-ttu-id="e7602-273">Özel durum yığın izleme değerleri.</span><span class="sxs-lookup"><span data-stu-id="e7602-273">Exception stack trace values.</span></span>

[<span data-ttu-id="e7602-274">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="e7602-274">Learn more</span></span>](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a><span data-ttu-id="e7602-275">Video</span><span class="sxs-lookup"><span data-stu-id="e7602-275">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <span data-ttu-id="e7602-276"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e7602-276"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="e7602-277">Telemetrinizi görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="e7602-277">View your telemetry:</span></span>

* <span data-ttu-id="e7602-278">[Ölçümleri keşfedin](app-insights-metrics-explorer.md) toomonitor performansı ve kullanımı</span><span class="sxs-lookup"><span data-stu-id="e7602-278">[Explore metrics](app-insights-metrics-explorer.md) toomonitor performance and usage</span></span>
* <span data-ttu-id="e7602-279">[Olayları ve günlükleri arayın] [ diagnostic] toodiagnose sorunları</span><span class="sxs-lookup"><span data-stu-id="e7602-279">[Search events and logs][diagnostic] toodiagnose problems</span></span>
* <span data-ttu-id="e7602-280">Daha gelişmiş sorgular için [analiz](app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="e7602-280">[Analytics](app-insights-analytics.md) for more advanced queries</span></span>
* [<span data-ttu-id="e7602-281">Panolar oluşturun</span><span class="sxs-lookup"><span data-stu-id="e7602-281">Create dashboards</span></span>](app-insights-dashboards.md)

<span data-ttu-id="e7602-282">Daha fazla telemetri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e7602-282">Add more telemetry:</span></span>

* <span data-ttu-id="e7602-283">[Web testleri oluşturma] [ availability] toomake sitenizin Canlı kaldığından emin.</span><span class="sxs-lookup"><span data-stu-id="e7602-283">[Create web tests][availability] toomake sure your site stays live.</span></span>
* <span data-ttu-id="e7602-284">[Web istemcisi telemetrisini ekleyin] [ usage] web sayfası koduna ve eklediğiniz toolet toosee özel durumlar çağrıları izleme.</span><span class="sxs-lookup"><span data-stu-id="e7602-284">[Add web client telemetry][usage] toosee exceptions from web page code and toolet you insert trace calls.</span></span>
* <span data-ttu-id="e7602-285">[Application Insights SDK'sı tooyour kodu ekleyin] [ greenbrown] izleme ekleyin ve oturum çağrıları</span><span class="sxs-lookup"><span data-stu-id="e7602-285">[Add Application Insights SDK tooyour code][greenbrown] so that you can insert trace and log calls</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
