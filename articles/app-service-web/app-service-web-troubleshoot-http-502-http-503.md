---
title: "aaaFix 502 hatalı ağ geçidi, 503 Hizmet kullanılamıyor hatalarıyla | Microsoft Docs"
description: "502 hatalı ağ geçidi ve Azure App Service içinde barındırılan web uygulamanızda 503 Hizmet kullanılamıyor hatalarıyla ilgili sorunları giderme."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 hatalı ağ geçidi 503 Hizmet kullanılamıyor hatası 503, hata 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a><span data-ttu-id="1986a-104">"502 hatalı ağ geçidi" ve "503 Hizmet kullanılamıyor", Azure web uygulamalarında HTTP hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="1986a-104">Troubleshoot HTTP errors of "502 bad gateway" and "503 service unavailable" in your Azure web apps</span></span>
<span data-ttu-id="1986a-105">"502 hatalı ağ geçidi" ve "503 Hizmet kullanılamıyor" olan yaygın hatalar içinde barındırılan web uygulamanızda [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1986a-105">"502 bad gateway" and "503 service unavailable" are common errors in your web app hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="1986a-106">Bu makalede bu hataları gidermenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1986a-106">This article helps you troubleshoot these errors.</span></span>

<span data-ttu-id="1986a-107">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="1986a-107">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1986a-108">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="1986a-108">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="1986a-109">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) ve tıklayın **destek alın**.</span><span class="sxs-lookup"><span data-stu-id="1986a-109">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click on **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="1986a-110">Belirti</span><span class="sxs-lookup"><span data-stu-id="1986a-110">Symptom</span></span>
<span data-ttu-id="1986a-111">Toohello web uygulaması göz attığınızda, bir HTTP döndürür "502 hatalı ağ geçidi" hatası ya da bir HTTP "503 Hizmet kullanılamıyor" hatasını.</span><span class="sxs-lookup"><span data-stu-id="1986a-111">When you browse toohello web app, it returns a HTTP "502 Bad Gateway" error or a HTTP "503 Service Unavailable" error.</span></span>

## <a name="cause"></a><span data-ttu-id="1986a-112">Nedeni</span><span class="sxs-lookup"><span data-stu-id="1986a-112">Cause</span></span>
<span data-ttu-id="1986a-113">Bu sorun sık sık uygulama düzeyi sorunları tarafından gibi neden olur:</span><span class="sxs-lookup"><span data-stu-id="1986a-113">This problem is often caused by application level issues, such as:</span></span>

* <span data-ttu-id="1986a-114">uzun süren istekleri</span><span class="sxs-lookup"><span data-stu-id="1986a-114">requests taking a long time</span></span>
* <span data-ttu-id="1986a-115">yüksek bellek/CPU kullanarak uygulama</span><span class="sxs-lookup"><span data-stu-id="1986a-115">application using high memory/CPU</span></span>
* <span data-ttu-id="1986a-116">tooan özel durum kilitlenen uygulama.</span><span class="sxs-lookup"><span data-stu-id="1986a-116">application crashing due tooan exception.</span></span>

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a><span data-ttu-id="1986a-117">Adımları toosolve "502 hatalı ağ geçidi" ve "503 Hizmet kullanılamıyor" hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="1986a-117">Troubleshooting steps toosolve "502 bad gateway" and "503 service unavailable" errors</span></span>
<span data-ttu-id="1986a-118">Sorun giderme sıralı bir düzende üç farklı görevler ayrılabilir:</span><span class="sxs-lookup"><span data-stu-id="1986a-118">Troubleshooting can be divided into three distinct tasks, in sequential order:</span></span>

1. [<span data-ttu-id="1986a-119">İnceleyin ve uygulama davranışı izleme</span><span class="sxs-lookup"><span data-stu-id="1986a-119">Observe and monitor application behavior</span></span>](#observe)
2. [<span data-ttu-id="1986a-120">Veri toplama</span><span class="sxs-lookup"><span data-stu-id="1986a-120">Collect data</span></span>](#collect)
3. [<span data-ttu-id="1986a-121">Merhaba sorunu azaltmak</span><span class="sxs-lookup"><span data-stu-id="1986a-121">Mitigate hello issue</span></span>](#mitigate)

<span data-ttu-id="1986a-122">[App Service Web Apps](/services/app-service/web/) her adımda çeşitli seçenekler sunar.</span><span class="sxs-lookup"><span data-stu-id="1986a-122">[App Service Web Apps](/services/app-service/web/) gives you various options at each step.</span></span>

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a><span data-ttu-id="1986a-123">1. İnceleyin ve uygulama davranışı izleme</span><span class="sxs-lookup"><span data-stu-id="1986a-123">1. Observe and monitor application behavior</span></span>
#### <a name="track-service-health"></a><span data-ttu-id="1986a-124">Hizmet durumu izleme</span><span class="sxs-lookup"><span data-stu-id="1986a-124">Track Service health</span></span>
<span data-ttu-id="1986a-125">Microsoft Azure hizmet kesintisi veya performans düşüşü olduğundan her zaman publicizes.</span><span class="sxs-lookup"><span data-stu-id="1986a-125">Microsoft Azure publicizes each time there is a service interruption or performance degradation.</span></span> <span data-ttu-id="1986a-126">Merhaba üzerinde hello hello hizmet durumunu izleyebilirsiniz [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1986a-126">You can track hello health of hello service on hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1986a-127">Daha fazla bilgi için bkz: [hizmet durumu izleme](../monitoring-and-diagnostics/insights-service-health.md).</span><span class="sxs-lookup"><span data-stu-id="1986a-127">For more information, see [Track service health](../monitoring-and-diagnostics/insights-service-health.md).</span></span>

#### <a name="monitor-your-web-app"></a><span data-ttu-id="1986a-128">Web uygulamanızı izlemek</span><span class="sxs-lookup"><span data-stu-id="1986a-128">Monitor your web app</span></span>
<span data-ttu-id="1986a-129">Uygulamanızı sorunları yaşıyorsa bu seçenek, toofind çıkışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="1986a-129">This option enables you toofind out if your application is having any issues.</span></span> <span data-ttu-id="1986a-130">Web uygulamanızın dikey penceresinde hello tıklayın **istekleri ve hataları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="1986a-130">In your web app’s blade, click hello **Requests and errors** tile.</span></span> <span data-ttu-id="1986a-131">Merhaba **ölçüm** dikey gösterir, tüm hello ölçümleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1986a-131">hello **Metric** blade will show you all hello metrics you can add.</span></span>

<span data-ttu-id="1986a-132">Web uygulamanız için toomonitor isteyebilirsiniz hello ölçümleri bazıları</span><span class="sxs-lookup"><span data-stu-id="1986a-132">Some of hello metrics that you might want toomonitor for your web app are</span></span>

* <span data-ttu-id="1986a-133">Ortalama bellek çalışma kümesi</span><span class="sxs-lookup"><span data-stu-id="1986a-133">Average memory working set</span></span>
* <span data-ttu-id="1986a-134">Ortalama yanıt süresi</span><span class="sxs-lookup"><span data-stu-id="1986a-134">Average response time</span></span>
* <span data-ttu-id="1986a-135">CPU süresi</span><span class="sxs-lookup"><span data-stu-id="1986a-135">CPU time</span></span>
* <span data-ttu-id="1986a-136">Bellek çalışma kümesi</span><span class="sxs-lookup"><span data-stu-id="1986a-136">Memory working set</span></span>
* <span data-ttu-id="1986a-137">İstekler</span><span class="sxs-lookup"><span data-stu-id="1986a-137">Requests</span></span>

![HTTP hataları hatalı ağ geçidi 502 ve 503 Hizmet kullanılamıyor çözme doğrultusunda web uygulaması izleme](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

<span data-ttu-id="1986a-139">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="1986a-139">For more information, see:</span></span>

* [<span data-ttu-id="1986a-140">Azure App Service'te Web uygulamalarını izleme</span><span class="sxs-lookup"><span data-stu-id="1986a-140">Monitor Web Apps in Azure App Service</span></span>](web-sites-monitor.md)
* [<span data-ttu-id="1986a-141">Uyarı bildirimleri alma</span><span class="sxs-lookup"><span data-stu-id="1986a-141">Receive alert notifications</span></span>](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a><span data-ttu-id="1986a-142">2. Veri toplama</span><span class="sxs-lookup"><span data-stu-id="1986a-142">2. Collect data</span></span>
#### <a name="use-hello-azure-app-service-support-portal"></a><span data-ttu-id="1986a-143">Hello Azure App Service destek portalında kullanın</span><span class="sxs-lookup"><span data-stu-id="1986a-143">Use hello Azure App Service Support Portal</span></span>
<span data-ttu-id="1986a-144">Web uygulamaları HTTP günlükleri, olay günlükleri, işlem dökümleri ve daha fazla bakarak hello özelliği tootroubleshoot sorunları ilgili tooyour web uygulaması ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="1986a-144">Web Apps provides you with hello ability tootroubleshoot issues related tooyour web app by looking at HTTP logs, event logs, process dumps, and more.</span></span> <span data-ttu-id="1986a-145">Bizim destek portalında kullanarak tüm bu bilgilere erişebilen **http://&lt;, uygulama adı >.scm.azurewebsites.net/Support**</span><span class="sxs-lookup"><span data-stu-id="1986a-145">You can access all this information using our Support portal at **http://&lt;your app name>.scm.azurewebsites.net/Support**</span></span>

<span data-ttu-id="1986a-146">Hello Azure App Service desteği portal üç ayrı sekmeler toosupport hello üç adımdan yaygın bir sorun giderme senaryo ile sağlar:</span><span class="sxs-lookup"><span data-stu-id="1986a-146">hello Azure App Service Support portal provides you with three separate tabs toosupport hello three steps of a common troubleshooting scenario:</span></span>

1. <span data-ttu-id="1986a-147">Şu anki davranışı inceleyin</span><span class="sxs-lookup"><span data-stu-id="1986a-147">Observe current behavior</span></span>
2. <span data-ttu-id="1986a-148">Tanılama bilgilerini toplama ve yerleşik çözümleyiciler hello çalıştıran analiz eder.</span><span class="sxs-lookup"><span data-stu-id="1986a-148">Analyze by collecting diagnostics information and running hello built-in analyzers</span></span>
3. <span data-ttu-id="1986a-149">Azaltmak</span><span class="sxs-lookup"><span data-stu-id="1986a-149">Mitigate</span></span>

<span data-ttu-id="1986a-150">Merhaba sorunu şimdi oluşuyorsa tıklatın **Çözümle** > **tanılama** > **şimdi tanılamak** toocreate sizin için tanılama oturumu hangi HTTP toplar, Olay Görüntüleyicisi günlükleri, bellek dökümleri, PHP Hata günlüklerini ve PHP rapor işlem günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1986a-150">If hello issue is happening right now, click **Analyze** > **Diagnostics** > **Diagnose Now** toocreate a diagnostic session for you, which will collect HTTP logs, event viewer logs, memory dumps, PHP error logs and PHP process report.</span></span>

<span data-ttu-id="1986a-151">Merhaba veri toplandığında, ayrıca hello verilerini analiz çalıştırmak ve bir HTML raporu ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1986a-151">Once hello data is collected, it will also run an analysis on hello data and provide you with an HTML report.</span></span>

<span data-ttu-id="1986a-152">Varsayılan olarak toodownload hello veri istemeniz durumunda, hello D:\home\data\DaaS klasöründe depolanması.</span><span class="sxs-lookup"><span data-stu-id="1986a-152">In case you want toodownload hello data, by default, it would be stored in hello D:\home\data\DaaS folder.</span></span>

<span data-ttu-id="1986a-153">Hello Azure App Service desteği portal hakkında daha fazla bilgi için bkz: [yeni güncelleştirmeler tooSupport Azure Web siteleri için Site uzantısı](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span><span class="sxs-lookup"><span data-stu-id="1986a-153">For more information on hello Azure App Service Support portal, see [New Updates tooSupport Site Extension for Azure Websites](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).</span></span>

#### <a name="use-hello-kudu-debug-console"></a><span data-ttu-id="1986a-154">Merhaba Kudu hata ayıklama konsolunu kullanma</span><span class="sxs-lookup"><span data-stu-id="1986a-154">Use hello Kudu Debug Console</span></span>
<span data-ttu-id="1986a-155">Web uygulamaları, hata ayıklama, keşfetme, ortamınız hakkında bilgi almak için JSON bitiş noktaları yanı sıra, dosyaları karşıya yükleme için kullanabileceğiniz bir hata ayıklama konsolu ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="1986a-155">Web Apps comes with a debug console that you can use for debugging, exploring, uploading files, as well as JSON endpoints for getting information about your environment.</span></span> <span data-ttu-id="1986a-156">Bu hello adlandırılır *Kudu konsol* veya hello *SCM Pano* web uygulamanız için.</span><span class="sxs-lookup"><span data-stu-id="1986a-156">This is called hello *Kudu Console* or hello *SCM Dashboard* for your web app.</span></span>

<span data-ttu-id="1986a-157">Giden toohello bağlantısıyla bu panoya erişebilir **https://&lt;, uygulama adı >.scm.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="1986a-157">You can access this dashboard by going toohello link **https://&lt;Your app name>.scm.azurewebsites.net/**.</span></span>

<span data-ttu-id="1986a-158">Kudu sağlar hello şeylerden bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1986a-158">Some of hello things that Kudu provides are:</span></span>

* <span data-ttu-id="1986a-159">Uygulamanız için ortam ayarları</span><span class="sxs-lookup"><span data-stu-id="1986a-159">environment settings for your application</span></span>
* <span data-ttu-id="1986a-160">günlük akışı</span><span class="sxs-lookup"><span data-stu-id="1986a-160">log stream</span></span>
* <span data-ttu-id="1986a-161">Tanılama dökümü</span><span class="sxs-lookup"><span data-stu-id="1986a-161">diagnostic dump</span></span>
* <span data-ttu-id="1986a-162">hata ayıklama konsolunu Powershell cmdlet'leri ve temel DOS komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1986a-162">debug console in which you can run Powershell cmdlets and basic DOS commands.</span></span>

<span data-ttu-id="1986a-163">Başka bir yararlı Kudu uygulamanızı ilk fırsat özel durum atma durumunda, Kudu kullanabilirsiniz ve hello SysInternals aracı Procdump toocreate bellek dökümleri, özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="1986a-163">Another useful feature of Kudu is that, in case your application is throwing first-chance exceptions, you can use Kudu and hello SysInternals tool Procdump toocreate memory dumps.</span></span> <span data-ttu-id="1986a-164">Bu bellek dökümlerini hello işleminin anlık görüntüleri ve genellikle web uygulamanızı daha karmaşık sorunları gidermenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1986a-164">These memory dumps are snapshots of hello process and can often help you troubleshoot more complicated issues with your web app.</span></span>

<span data-ttu-id="1986a-165">Kudu içinde kullanılabilir özellikler hakkında daha fazla bilgi için bkz: [Azure Web siteleri çevrimiçi araçlar hakkında bilmeniz](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span><span class="sxs-lookup"><span data-stu-id="1986a-165">For more information on features available in Kudu, see [Azure Websites online tools you should know about](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).</span></span>

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a><span data-ttu-id="1986a-166">3. Merhaba sorunu azaltmak</span><span class="sxs-lookup"><span data-stu-id="1986a-166">3. Mitigate hello issue</span></span>
#### <a name="scale-hello-web-app"></a><span data-ttu-id="1986a-167">Ölçek hello web uygulaması</span><span class="sxs-lookup"><span data-stu-id="1986a-167">Scale hello web app</span></span>
<span data-ttu-id="1986a-168">Azure App Service'te performansı artırmak ve üretilen işi için uygulamanızı çalıştıran hello ölçek ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1986a-168">In Azure App Service, for increased performance and throughput,  you can adjust hello scale at which you are running your application.</span></span> <span data-ttu-id="1986a-169">Bir web uygulamasını kurup ölçeklendirmeyi kapsar iki eylemlerin: fiyatlandırma katmanı ve daha yüksek fiyatlandırma katmanı toohello geçirildikten sonra belirli ayarları yapılandırma yüksek, uygulama hizmeti planı tooa değiştirme.</span><span class="sxs-lookup"><span data-stu-id="1986a-169">Scaling up a web app involves two related actions: changing your App Service plan tooa higher pricing tier, and configuring certain settings after you have switched toohello higher pricing tier.</span></span>

<span data-ttu-id="1986a-170">Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [bir web uygulamasını Azure App Service'te ölçeklendirme](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="1986a-170">For more information on scaling, see [Scale a web app in Azure App Service](web-sites-scale.md).</span></span>

<span data-ttu-id="1986a-171">Ayrıca, uygulamanızı birden fazla örneği üzerinde toorun seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1986a-171">Additionally, you can choose toorun your application on more than one instance .</span></span> <span data-ttu-id="1986a-172">Bu yalnızca ile daha fazla işleme yeteneği sağlar, ancak ayrıca miktar hataya dayanıklılık sağlar.</span><span class="sxs-lookup"><span data-stu-id="1986a-172">This not only provides you with more processing capability, but also gives you some amount of fault tolerance.</span></span> <span data-ttu-id="1986a-173">Merhaba işlem bir örneğinde devre dışı kalırsa, hello diğer örneğe hala isteklere hizmet vermeyi devam eder.</span><span class="sxs-lookup"><span data-stu-id="1986a-173">If hello process goes down on one instance, hello other instance will still continue serving requests.</span></span>

<span data-ttu-id="1986a-174">Toobe el ile veya otomatik ölçeklendirme hello ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1986a-174">You can set hello scaling toobe Manual or Automatic.</span></span>

#### <a name="use-autoheal"></a><span data-ttu-id="1986a-175">AutoHeal kullanın</span><span class="sxs-lookup"><span data-stu-id="1986a-175">Use AutoHeal</span></span>
<span data-ttu-id="1986a-176">AutoHeal (yapılandırma değişiklikleri, istekleri, bellek tabanlı sınırları veya hello zaman tooexecute bir istek gerekli gibi) seçtiğiniz ayarlarına dayanarak, uygulamanız için hello çalışan işlemi geri dönüştürüldüğünde.</span><span class="sxs-lookup"><span data-stu-id="1986a-176">AutoHeal recycles hello worker process for your app based on settings you choose (like configuration changes, requests, memory-based limits, or hello time needed tooexecute a request).</span></span> <span data-ttu-id="1986a-177">Başlangıç saati, çoğu hello en hızlı yolu toorecover bir sorun geri dönüşüm hello işlemidir.</span><span class="sxs-lookup"><span data-stu-id="1986a-177">Most of hello time, recycle hello process is hello fastest way toorecover from a problem.</span></span> <span data-ttu-id="1986a-178">Her zaman hello web uygulamasından doğrudan hello Azure portalı içinde yeniden olsa AutoHeal onu otomatik olarak sizin için yapar.</span><span class="sxs-lookup"><span data-stu-id="1986a-178">Though you can always restart hello web app from directly within hello Azure Portal, AutoHeal will do it automatically for you.</span></span> <span data-ttu-id="1986a-179">Toodo gereken tek şey, web uygulamanız için hello kök web.config dosyasında bazı tetikleyicileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1986a-179">All you need toodo is add some triggers in hello root web.config for your web app.</span></span> <span data-ttu-id="1986a-180">Bu ayarları hello aynı çalışır, Not şekilde uygulamanızı bir .net olsa bile.</span><span class="sxs-lookup"><span data-stu-id="1986a-180">Note that these settings would work in hello same way even if your application is not a .Net one.</span></span>

<span data-ttu-id="1986a-181">Daha fazla bilgi için bkz: [Azure Web siteleri otomatik düzeltme](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span><span class="sxs-lookup"><span data-stu-id="1986a-181">For more information, see [Auto-Healing Azure Web Sites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).</span></span>

#### <a name="restart-hello-web-app"></a><span data-ttu-id="1986a-182">Merhaba web uygulaması yeniden</span><span class="sxs-lookup"><span data-stu-id="1986a-182">Restart hello web app</span></span>
<span data-ttu-id="1986a-183">Bu genellikle hello en basit yolu toorecover tek seferlik sorunlardan olur.</span><span class="sxs-lookup"><span data-stu-id="1986a-183">This is often hello simplest way toorecover from one-time issues.</span></span> <span data-ttu-id="1986a-184">Merhaba üzerinde [Azure Portal](https://portal.azure.com/), web uygulamanızın dikey penceresinde hello seçenekleri toostop sahip veya uygulamanızı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1986a-184">On hello [Azure Portal](https://portal.azure.com/), on your web app’s blade, you have hello options toostop or restart your app.</span></span>

 ![Uygulama toosolve HTTP hataları 502 hatalı ağ geçidi 503 Hizmet kullanılamıyor ve yeniden başlatın](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

<span data-ttu-id="1986a-186">Web uygulamanızı Azure Powershell kullanarak da yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1986a-186">You can also manage your web app using Azure Powershell.</span></span> <span data-ttu-id="1986a-187">Daha fazla bilgi için bkz. [Azure PowerShell'i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1986a-187">For more information, see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

