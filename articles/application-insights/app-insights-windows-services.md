---
title: "aaaAzure için Application Insights Windows server ve çalışan rolleri | Microsoft Docs"
description: "Merhaba Application Insights SDK'sı tooyour ASP.NET uygulama tooanalyze kullanımını, kullanılabilirliğini ve performansını el ile ekleyin."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="d882e-103">.NET uygulamaları için Application Insights’ı el ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d882e-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="d882e-104">Yapılandırabileceğiniz [Application Insights](app-insights-overview.md) toomonitor çok çeşitli uygulamaları veya uygulama rollerini, bileşenleri veya mikro.</span><span class="sxs-lookup"><span data-stu-id="d882e-104">You can configure [Application Insights](app-insights-overview.md) toomonitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="d882e-105">Web uygulamaları ve hizmetleri için, Visual Studio [tek adımlı yapılandırma](app-insights-asp-net.md) sunar.</span><span class="sxs-lookup"><span data-stu-id="d882e-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="d882e-106">Arka uç sunucu rolleri veya masaüstü uygulamaları gibi diğer .NET uygulaması türleri için Application Insights’ı el ile yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d882e-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Örnek performans izleme grafikleri](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="d882e-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d882e-108">Before you start</span></span>

<span data-ttu-id="d882e-109">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="d882e-109">You need:</span></span>

* <span data-ttu-id="d882e-110">Bir abonelik çok[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="d882e-110">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="d882e-111">Merhaba sahibi ekibinizin ve kuruluşunuzun bir Azure aboneliğiniz varsa, tooit, ekleyebilir kullanarak, [Microsoft hesabı](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="d882e-111">If your team or organization has an Azure subscription, hello owner can add you tooit, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="d882e-112">Visual Studio 2013 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="d882e-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="d882e-113"><a name="add"></a>1. Application Insights kaynağı seçme</span><span class="sxs-lookup"><span data-stu-id="d882e-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="d882e-114">Burada, veriler toplanır ve hello Azure portalında görüntülenen Hello 'kaynak' değil.</span><span class="sxs-lookup"><span data-stu-id="d882e-114">hello 'resource' is where your data is collected and displayed in hello Azure portal.</span></span> <span data-ttu-id="d882e-115">Toodecide gerekip gerekmediği toocreate yeni bir ya da mevcut bir paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d882e-115">You need toodecide whether toocreate a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="d882e-116">Daha büyük bir uygulamanın parçası: Var olan kaynağı kullanma</span><span class="sxs-lookup"><span data-stu-id="d882e-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="d882e-117">Web uygulamanız - Örneğin, bir ön uç web uygulaması ve bir veya daha fazla arka uç hizmetlerinin - çeşitli bileşenleri sahip sonra tüm hello bileşenleri toohello telemetri göndermelisiniz aynı kaynak.</span><span class="sxs-lookup"><span data-stu-id="d882e-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all hello components toohello same resource.</span></span> <span data-ttu-id="d882e-118">Bu tek bir uygulama haritada görüntülenmelerini toobe etkinleştirmek ve olası tootrace bir bileşen tooanother isteğinden yapar.</span><span class="sxs-lookup"><span data-stu-id="d882e-118">This will enable them toobe displayed on a single Application Map, and make it possible tootrace a request from one component tooanother.</span></span>

<span data-ttu-id="d882e-119">Bu nedenle, bu uygulamanın diğer bileşenleri izliyorsanız sonra yalnızca kullanım hello aynı kaynak.</span><span class="sxs-lookup"><span data-stu-id="d882e-119">So, if you're already monitoring other components of this app, then just use hello same resource.</span></span>

<span data-ttu-id="d882e-120">Merhaba kaynak hello açmak [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d882e-120">Open hello resource in hello [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="d882e-121">Kendi içinde uygulama: Yeni bir kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="d882e-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="d882e-122">Merhaba yeni uygulama ilgisiz tooother uygulamalar varsa, kendi kaynak olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d882e-122">If hello new app is unrelated tooother applications, then it should have its own resource.</span></span>

<span data-ttu-id="d882e-123">İçinde toohello oturum [Azure portal](https://portal.azure.com/)ve yeni bir Application Insights kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d882e-123">Sign in toohello [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="d882e-124">ASP.NET hello uygulama türü olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="d882e-124">Choose ASP.NET as hello application type.</span></span>

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="d882e-126">uygulama türü Hello seçimi hello kaynak dikey pencerelerinin varsayılan içeriğini hello ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d882e-126">hello choice of application type sets hello default content of hello resource blades.</span></span>

## <a name="2-copy-hello-instrumentation-key"></a><span data-ttu-id="d882e-127">2. Merhaba izleme anahtarını kopyalama</span><span class="sxs-lookup"><span data-stu-id="d882e-127">2. Copy hello Instrumentation Key</span></span>
<span data-ttu-id="d882e-128">başlangıç anahtarı hello kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d882e-128">hello key identifies hello resource.</span></span> <span data-ttu-id="d882e-129">En kısa sürede hello SDK'sı, sıra toodirect veri toohello kaynak de yüklemeniz.</span><span class="sxs-lookup"><span data-stu-id="d882e-129">You'll install it soon in hello SDK, in order toodirect data toohello resource.</span></span>

![Özellikler'i tıklatın, başlangıç anahtarı seçin ve ctrl + C tuşlarına basın](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="d882e-131"><a name="sdk"></a>3. Uygulamanızda Hello Application Insights paketini yükle</span><span class="sxs-lookup"><span data-stu-id="d882e-131"><a name="sdk"></a>3. Install hello Application Insights package in your application</span></span>
<span data-ttu-id="d882e-132">Yükleme ve yapılandırma hello Application Insights paketini hello platform üzerinde çalıştığınız bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="d882e-132">Installing and configuring hello Application Insights package varies depending on hello platform you're working on.</span></span> 

1. <span data-ttu-id="d882e-133">Visual Studio’da projenize sağ tıklayıp **NuGet Paketlerini Yönet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d882e-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Merhaba projesine sağ tıklayın ve Nuget paketlerini Yönet seçin](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="d882e-135">Windows server uygulamaları, "Microsoft.ApplicationInsights.WindowsServer." Merhaba Application Insights paketini yükle</span><span class="sxs-lookup"><span data-stu-id="d882e-135">Install hello Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    !["Application Insights" araması yapın](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="d882e-137">*Hangi sürüm?*</span><span class="sxs-lookup"><span data-stu-id="d882e-137">*Which version?*</span></span>

    <span data-ttu-id="d882e-138">Denetleme **dahil et** bizim en son özellikleri tootry istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d882e-138">Check **Include prerelease** if you want tootry our latest features.</span></span> <span data-ttu-id="d882e-139">Merhaba ilgili belgeleri veya blog ön sürümü gerekip gerekmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d882e-139">hello relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="d882e-140">*Diğer paketleri kullanabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="d882e-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="d882e-141">Evet.</span><span class="sxs-lookup"><span data-stu-id="d882e-141">Yes.</span></span> <span data-ttu-id="d882e-142">Kendi telemetrinizi yalnızca toouse hello API toosend isterseniz, "Microsoft.ApplicationInsights" seçin.</span><span class="sxs-lookup"><span data-stu-id="d882e-142">Choose "Microsoft.ApplicationInsights" if you only want toouse hello API toosend your own telemetry.</span></span> <span data-ttu-id="d882e-143">Merhaba Windows Server paketi hello API artı bir dizi performans sayacı toplama ve bağımlılık izleme gibi diğer paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d882e-143">hello Windows Server package includes hello API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="tooupgrade-toofuture-package-versions"></a><span data-ttu-id="d882e-144">tooupgrade toofuture paketi sürümleri</span><span class="sxs-lookup"><span data-stu-id="d882e-144">tooupgrade toofuture package versions</span></span>
<span data-ttu-id="d882e-145">Biz hello SDK zaman tootime gelen yeni bir sürümü kullanıma.</span><span class="sxs-lookup"><span data-stu-id="d882e-145">We release a new version of hello SDK from time tootime.</span></span>

<span data-ttu-id="d882e-146">tooupgrade tooa [hello paketinin yeni sürümü](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), NuGet paket yöneticisini yeniden açın ve yüklü paketleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="d882e-146">tooupgrade tooa [new release of hello package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="d882e-147">**Microsoft.ApplicationInsights.WindowsServer** ve **Yükselt**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="d882e-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="d882e-148">Tüm özelleştirmeler tooApplicationInsights.config yaptıysanız, yükseltme ve daha sonra değişikliklerinizi hello yeni sürümle birleştirin önce bir kopyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d882e-148">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into hello new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="d882e-149">4. Telemetri gönderme</span><span class="sxs-lookup"><span data-stu-id="d882e-149">4. Send telemetry</span></span>
<span data-ttu-id="d882e-150">**Yalnızca hello API paket yüklediyseniz:**</span><span class="sxs-lookup"><span data-stu-id="d882e-150">**If you installed only hello API package:**</span></span>

* <span data-ttu-id="d882e-151">Kümesinde hello izleme anahtarını kodda, örneğin `main()`:</span><span class="sxs-lookup"><span data-stu-id="d882e-151">Set hello instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="d882e-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *anahtarınız* `";`</span><span class="sxs-lookup"><span data-stu-id="d882e-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="d882e-153">[Merhaba API kullanarak kendi telemetrinizi yazmanızı](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="d882e-153">[Write your own telemetry using hello API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="d882e-154">**Diğer Application Insights paketleri yüklediyseniz** tercih ederseniz, hello .config dosyası tooset hello izleme anahtarını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d882e-154">**If you installed other Application Insights packages,** you can, if you prefer, use hello .config file tooset hello instrumentation key:</span></span>

* <span data-ttu-id="d882e-155">(Hangi NuGet yükleme hello tarafından eklendi) Applicationınsights.config düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="d882e-155">Edit ApplicationInsights.config (which was added by hello NuGet install).</span></span> <span data-ttu-id="d882e-156">Bu, yalnızca kapanış etiketi hello önce ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d882e-156">Insert this just before hello closing tag:</span></span>
  
    <span data-ttu-id="d882e-157">`<InstrumentationKey>`*kopyaladığınız hello izleme anahtarını*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="d882e-157">`<InstrumentationKey>` *hello instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="d882e-158">Çözüm Gezgini'nde Applicationınsights.config Hello özelliklerini çok ayarlandığından emin olun**yapı eylemi içerik, kopya tooOutput dizin = kopyalama =**.</span><span class="sxs-lookup"><span data-stu-id="d882e-158">Make sure that hello properties of ApplicationInsights.config in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>

<span data-ttu-id="d882e-159">Çok istiyorsanız yararlı tooset hello izleme anahtarını kodda olduğu[farklı derleme yapılandırmaları için anahtar hello anahtar](app-insights-separate-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d882e-159">It's useful tooset hello instrumentation key in code if you want too[switch hello key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="d882e-160">Kodda hello anahtar ayarlarsanız, tooset yok hello içinde `.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="d882e-160">If you set hello key in code, you don't have tooset it in hello `.config` file.</span></span>

## <span data-ttu-id="d882e-161"><a name="run"></a> Projenizi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d882e-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="d882e-162">Kullanım hello **F5** toorun uygulamanız ve deneyin: birkaç telemetri açık farklı sayfaları toogenerate.</span><span class="sxs-lookup"><span data-stu-id="d882e-162">Use hello **F5** toorun your application and try it out: open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="d882e-163">Visual Studio'da gönderilmiş hello etkinliklerin sayısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d882e-163">In Visual Studio, you'll see a count of hello events that have been sent.</span></span>

![Visual Studio’da olay sayımı](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="d882e-165"><a name="monitor"></a> Telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d882e-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="d882e-166">Toohello iade [Azure portal](https://portal.azure.com/) ve tooyour Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="d882e-166">Return toohello [Azure portal](https://portal.azure.com/) and browse tooyour Application Insights resource.</span></span>

<span data-ttu-id="d882e-167">Merhaba genel bakış grafiklerinde veri arayın.</span><span class="sxs-lookup"><span data-stu-id="d882e-167">Look for data in hello Overview charts.</span></span> <span data-ttu-id="d882e-168">İlk olarak yalnızca bir veya iki nokta görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d882e-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="d882e-169">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d882e-169">For example:</span></span>

![Toomore verilerine tıklatın](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="d882e-171">Tıklatın herhangi grafik toosee ayrıntılı ölçümler.</span><span class="sxs-lookup"><span data-stu-id="d882e-171">Click through any chart toosee more detailed metrics.</span></span> [<span data-ttu-id="d882e-172">Ölçümler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="d882e-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="d882e-173">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="d882e-173">No data?</span></span>
* <span data-ttu-id="d882e-174">Birkaç telemetri oluşturması için farklı sayfaları açarak hello uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="d882e-174">Use hello application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="d882e-175">Açık hello [arama](app-insights-diagnostic-search.md) döşeme, olayları tek tek toosee.</span><span class="sxs-lookup"><span data-stu-id="d882e-175">Open hello [Search](app-insights-diagnostic-search.md) tile, toosee individual events.</span></span> <span data-ttu-id="d882e-176">Bazen biraz uzun tooget hello ölçümleri ardışık düzeninden olayları alır.</span><span class="sxs-lookup"><span data-stu-id="d882e-176">Sometimes it takes events a little while longer tooget through hello metrics pipeline.</span></span>
* <span data-ttu-id="d882e-177">Birkaç saniye bekleyin ve **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d882e-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="d882e-178">Grafikler kendilerini düzenli olarak yeniler, ancak için bazı veri tooshow bekliyorsanız el ile yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d882e-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data tooshow up.</span></span>
* <span data-ttu-id="d882e-179">Bkz. [Sorun giderme](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d882e-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="d882e-180">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="d882e-180">Publish your app</span></span>
<span data-ttu-id="d882e-181">Şimdi veri birleştirdiğinizde uygulama tooyour sunucunuz veya tooAzure ve izleme hello dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d882e-181">Now deploy your application tooyour server or tooAzure and watch hello data accumulate.</span></span>

![Visual Studio toopublish uygulamanızı kullanın](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="d882e-183">Hata ayıklama modunda çalıştırdığınızda telemetri görüntülenen verileri saniyeler içinde görmeniz gerekir böylece hello ardışık düzen üzerinden hızlandırılır.</span><span class="sxs-lookup"><span data-stu-id="d882e-183">When you run in debug mode, telemetry is expedited through hello pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="d882e-184">Uygulamanızı Sürüm yapılandırmasında dağıttığınızda veriler daha yavaş birikir.</span><span class="sxs-lookup"><span data-stu-id="d882e-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-tooyour-server"></a><span data-ttu-id="d882e-185">Tooyour sunucu yayımladıktan sonra veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="d882e-185">No data after you publish tooyour server?</span></span>
<span data-ttu-id="d882e-186">Sunucunuzun güvenlik duvarında giden trafik için bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="d882e-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="d882e-187">Bkz: [bu sayfayı](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) gerekli adreslerini hello listesi</span><span class="sxs-lookup"><span data-stu-id="d882e-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for hello list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="d882e-188">Derleme sunucunuzda sorun mu yaşıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="d882e-188">Trouble on your build server?</span></span>
<span data-ttu-id="d882e-189">Lütfen [bu Sorun Giderme maddesine](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild) bakın.</span><span class="sxs-lookup"><span data-stu-id="d882e-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="d882e-190">Uygulamanız çok sayıda telemetri oluşturuyorsa hello Uyarlamalı örnekleme modülü olayların yalnızca bir temsilci fraksiyonunu göndererek toohello portal gönderilen hello birim otomatik olarak azaltır.</span><span class="sxs-lookup"><span data-stu-id="d882e-190">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="d882e-191">Ancak, böylece ilgili olaylar arasında gezinebilirsiniz olayları, ilgili toohello aynı istekte seçili veya bir grup olarak işaretli değildir.</span><span class="sxs-lookup"><span data-stu-id="d882e-191">However, events that are related toohello same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="d882e-192">[Örnekleme hakkında bilgi edinin](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d882e-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="d882e-193">Video</span><span class="sxs-lookup"><span data-stu-id="d882e-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="d882e-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d882e-194">Next steps</span></span>
* <span data-ttu-id="d882e-195">[Daha fazla telemetri ekleme](app-insights-asp-net-more.md) tooget hello uygulamanızın 360 derecelik tam görünümünü.</span><span class="sxs-lookup"><span data-stu-id="d882e-195">[Add more telemetry](app-insights-asp-net-more.md) tooget hello full 360-degree view of your application.</span></span>

