---
title: "Windows sunucu ve çalışan rolleri için Azure Application Insights | Microsoft Docs"
description: "Kullanım, kullanılabilirlik ve performansı analiz etmek için Application Insights SDK’sını ASP.NET uygulamanıza el ile ekleyin."
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
ms.openlocfilehash: 4b9f8c618a69c4c157dafeb7f726aae24efad428
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a><span data-ttu-id="9cdfe-103">.NET uygulamaları için Application Insights’ı el ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9cdfe-103">Manually configure Application Insights for .NET applications</span></span>

<span data-ttu-id="9cdfe-104">[Application Insights](app-insights-overview.md)’ı, çok çeşitli uygulamaları veya uygulama rolleri, bileşenler veya mikro hizmetleri izlemek üzere yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-104">You can configure [Application Insights](app-insights-overview.md) to monitor a wide variety of applications or application roles, components, or microservices.</span></span> <span data-ttu-id="9cdfe-105">Web uygulamaları ve hizmetleri için, Visual Studio [tek adımlı yapılandırma](app-insights-asp-net.md) sunar.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-105">For web apps and services, Visual Studio offers [one-step configuration](app-insights-asp-net.md).</span></span> <span data-ttu-id="9cdfe-106">Arka uç sunucu rolleri veya masaüstü uygulamaları gibi diğer .NET uygulaması türleri için Application Insights’ı el ile yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-106">For other types of .NET application, such as backend server roles or desktop applications, you can configure Application Insights manually.</span></span>

![Örnek performans izleme grafikleri](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a><span data-ttu-id="9cdfe-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="9cdfe-108">Before you start</span></span>

<span data-ttu-id="9cdfe-109">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="9cdfe-109">You need:</span></span>

* <span data-ttu-id="9cdfe-110">Bir [Microsoft Azure](http://azure.com) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-110">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="9cdfe-111">Ekibinizin ve kuruluşunuzun Azure aboneliği varsa, sahibi [Microsoft hesabınızı](http://live.com) kullanarak sizi buna ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-111">If your team or organization has an Azure subscription, the owner can add you to it, using your [Microsoft account](http://live.com).</span></span>
* <span data-ttu-id="9cdfe-112">Visual Studio 2013 veya üstü.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-112">Visual Studio 2013 or later.</span></span>

## <span data-ttu-id="9cdfe-113"><a name="add"></a>1. Application Insights kaynağı seçme</span><span class="sxs-lookup"><span data-stu-id="9cdfe-113"><a name="add"></a>1. Choose an Application Insights resource</span></span>

<span data-ttu-id="9cdfe-114">'Kaynak', verilerinizin toplandığı ve Azure portalında gösterildiği yerdir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-114">The 'resource' is where your data is collected and displayed in the Azure portal.</span></span> <span data-ttu-id="9cdfe-115">Yeni bir tane oluşturmaya veya mevcut olanı paylaşmaya karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-115">You need to decide whether to create a new one, or share an existing one.</span></span>

### <a name="part-of-a-larger-app-use-existing-resource"></a><span data-ttu-id="9cdfe-116">Daha büyük bir uygulamanın parçası: Var olan kaynağı kullanma</span><span class="sxs-lookup"><span data-stu-id="9cdfe-116">Part of a larger app: Use existing resource</span></span>

<span data-ttu-id="9cdfe-117">Web uygulamanızın ön uç web uygulaması ve bir ya da daha fazla arka uç hizmeti gibi birkaç bileşeni varsa, tüm bileşenlerden aynı kaynağa telemetri verileri göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-117">If your web application has several components - for example, a front-end web app and one or more back-end services - then you should send telemetry from all the components to the same resource.</span></span> <span data-ttu-id="9cdfe-118">Bunun yapılması, verilerin tek bir Uygulama Eşlemesinde gösterilmesini sağlar ve bir bileşenden diğerine gönderilen isteğin izlenmesini mümkün hale getirir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-118">This will enable them to be displayed on a single Application Map, and make it possible to trace a request from one component to another.</span></span>

<span data-ttu-id="9cdfe-119">Bu nedenle, bu uygulamanın diğer bileşenlerini izliyorsanız aynı kaynağı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-119">So, if you're already monitoring other components of this app, then just use the same resource.</span></span>

<span data-ttu-id="9cdfe-120">Kaynağı [Azure portalında](https://portal.azure.com/) açın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-120">Open the resource in the [Azure portal](https://portal.azure.com/).</span></span> 

### <a name="self-contained-app-create-a-new-resource"></a><span data-ttu-id="9cdfe-121">Kendi içinde uygulama: Yeni bir kaynak oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cdfe-121">Self-contained app: Create a new resource</span></span>

<span data-ttu-id="9cdfe-122">Yeni uygulama başka uygulamalarla ilgisiz ise, kendi kaynağına sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-122">If the new app is unrelated to other applications, then it should have its own resource.</span></span>

<span data-ttu-id="9cdfe-123">[Azure portalında](https://portal.azure.com/) oturum açın ve yeni bir Application Insights kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-123">Sign in to the [Azure portal](https://portal.azure.com/), and create a new Application Insights resource.</span></span> <span data-ttu-id="9cdfe-124">Uygulama türü olarak ASP.NET’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-124">Choose ASP.NET as the application type.</span></span>

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-windows-services/01-new-asp.png)

<span data-ttu-id="9cdfe-126">Uygulama türü seçimi, kaynak dikey pencerelerinin varsayılan içeriğini belirler.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-126">The choice of application type sets the default content of the resource blades.</span></span>

## <a name="2-copy-the-instrumentation-key"></a><span data-ttu-id="9cdfe-127">2. İzleme Anahtarını Kopyalama</span><span class="sxs-lookup"><span data-stu-id="9cdfe-127">2. Copy the Instrumentation Key</span></span>
<span data-ttu-id="9cdfe-128">Anahtar, kaynağı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-128">The key identifies the resource.</span></span> <span data-ttu-id="9cdfe-129">Bu anahtarı kısa bir süre sonra verileri kaynağa yönlendirmek için SDK’ya yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-129">You'll install it soon in the SDK, in order to direct data to the resource.</span></span>

![Özellikler'e tıklayın, anahtarı seçin ve ctrl + C tuşlarına basın](./media/app-insights-windows-services/02-props-asp.png)

## <span data-ttu-id="9cdfe-131"><a name="sdk"></a>3. Uygulamanıza Application Insights paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="9cdfe-131"><a name="sdk"></a>3. Install the Application Insights package in your application</span></span>
<span data-ttu-id="9cdfe-132">Application Insights paketinin yüklenmesi ve yapılandırılması, üzerinde çalıştığınız platforma bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-132">Installing and configuring the Application Insights package varies depending on the platform you're working on.</span></span> 

1. <span data-ttu-id="9cdfe-133">Visual Studio’da projenize sağ tıklayıp **NuGet Paketlerini Yönet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-133">In Visual Studio, right-click your project and choose **Manage Nuget Packages**.</span></span>
   
    ![Projeye sağ tıklayın ve Nuget Paketlerini Yönet’i seçin](./media/app-insights-windows-services/03-nuget.png)
2. <span data-ttu-id="9cdfe-135">Windows sunucu uygulamaları için "Microsoft.ApplicationInsights.WindowsServer" adlı Application Insights paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-135">Install the Application Insights package for Windows server apps, "Microsoft.ApplicationInsights.WindowsServer."</span></span>
   
    !["Application Insights" araması yapın](./media/app-insights-windows-services/04-ai-nuget.png)
   
    <span data-ttu-id="9cdfe-137">*Hangi sürüm?*</span><span class="sxs-lookup"><span data-stu-id="9cdfe-137">*Which version?*</span></span>

    <span data-ttu-id="9cdfe-138">En son özelliklerimizi denemek istiyorsanız **Ön sürümleri dahil et**’i işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-138">Check **Include prerelease** if you want to try our latest features.</span></span> <span data-ttu-id="9cdfe-139">Ön sürümün gerekip gerekmediği ilgili belge veya bloglarda belirtilir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-139">The relevant documents or blogs note whether you need a prerelease version.</span></span>
    
    <span data-ttu-id="9cdfe-140">*Diğer paketleri kullanabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="9cdfe-140">*Can I use other packages?*</span></span>
   
    <span data-ttu-id="9cdfe-141">Evet.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-141">Yes.</span></span> <span data-ttu-id="9cdfe-142">API’yi yalnızca kendi telemetrinizi göndermek için kullanmak istiyorsanız “Microsoft.ApplicationInsights” öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-142">Choose "Microsoft.ApplicationInsights" if you only want to use the API to send your own telemetry.</span></span> <span data-ttu-id="9cdfe-143">Windows Server paketi API’nin yanı sıra performans sayacı koleksiyonu ve bağımlılık izlemesi gibi birkaç paketi daha içerir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-143">The Windows Server package includes the API plus a number of other packages such as performance counter collection and dependency monitoring.</span></span> 

### <a name="to-upgrade-to-future-package-versions"></a><span data-ttu-id="9cdfe-144">Gelecekteki paket sürümlerine yükseltmek için</span><span class="sxs-lookup"><span data-stu-id="9cdfe-144">To upgrade to future package versions</span></span>
<span data-ttu-id="9cdfe-145">SDK’nın yeni sürümü zaman zaman yayınlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-145">We release a new version of the SDK from time to time.</span></span>

<span data-ttu-id="9cdfe-146">[Paketin yeni sürümüne](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/) yükseltme yapmak için NuGet paket yöneticisini yeniden açın ve yüklü paketleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-146">To upgrade to a [new release of the package](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), open NuGet package manager again and filter on installed packages.</span></span> <span data-ttu-id="9cdfe-147">**Microsoft.ApplicationInsights.WindowsServer** ve **Yükselt**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-147">Select **Microsoft.ApplicationInsights.WindowsServer** and choose **Upgrade**.</span></span>

<span data-ttu-id="9cdfe-148">ApplicationInsights.config dosyasında herhangi bir özelleştirme yaptıysanız yükseltmeden önce bir kopyasını kaydedin ve daha sonra değişikliklerinizi yeni sürümle birleştirin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-148">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade, and afterwards merge your changes into the new version.</span></span>

## <a name="4-send-telemetry"></a><span data-ttu-id="9cdfe-149">4. Telemetri gönderme</span><span class="sxs-lookup"><span data-stu-id="9cdfe-149">4. Send telemetry</span></span>
<span data-ttu-id="9cdfe-150">**Yalnızca API paketini yüklediyseniz:**</span><span class="sxs-lookup"><span data-stu-id="9cdfe-150">**If you installed only the API package:**</span></span>

* <span data-ttu-id="9cdfe-151">Koddaki izleme anahtarını ayarlayın, örneğin `main()` içinde:</span><span class="sxs-lookup"><span data-stu-id="9cdfe-151">Set the instrumentation key in code, for example in `main()`:</span></span> 
  
    <span data-ttu-id="9cdfe-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *anahtarınız* `";`</span><span class="sxs-lookup"><span data-stu-id="9cdfe-152">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
* <span data-ttu-id="9cdfe-153">[API'yi kullanarak kendi telemetrinizi yazın](app-insights-api-custom-events-metrics.md#ikey).</span><span class="sxs-lookup"><span data-stu-id="9cdfe-153">[Write your own telemetry using the API](app-insights-api-custom-events-metrics.md#ikey).</span></span>

<span data-ttu-id="9cdfe-154">**Diğer Application Insights paketlerini yüklediyseniz** izleme anahtarını ayarlamak için isterseniz .config dosyasını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9cdfe-154">**If you installed other Application Insights packages,** you can, if you prefer, use the .config file to set the instrumentation key:</span></span>

* <span data-ttu-id="9cdfe-155">ApplicationInsights.config dosyasını (NuGet yüklemesinde eklenen dosya) düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-155">Edit ApplicationInsights.config (which was added by the NuGet install).</span></span> <span data-ttu-id="9cdfe-156">Kapanış etiketinin hemen önüne şunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9cdfe-156">Insert this just before the closing tag:</span></span>
  
    <span data-ttu-id="9cdfe-157">`<InstrumentationKey>` *kopyaladığınız izleme anahtarı* `</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="9cdfe-157">`<InstrumentationKey>` *the instrumentation key you copied* `</InstrumentationKey>`</span></span>
* <span data-ttu-id="9cdfe-158">Çözüm Gezgini’nde ApplicationInsights.config dosyası özelliklerinin **Build Action = Content, Copy to Output Directory = Copy** olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-158">Make sure that the properties of ApplicationInsights.config in Solution Explorer are set to **Build Action = Content, Copy to Output Directory = Copy**.</span></span>

<span data-ttu-id="9cdfe-159">[Farklı derleme yapılandırmalarında anahtarı değiştirmek istiyorsanız](app-insights-separate-resources.md) kodda izleme anahtarı belirlemeniz faydalı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-159">It's useful to set the instrumentation key in code if you want to [switch the key for different build configurations](app-insights-separate-resources.md).</span></span> <span data-ttu-id="9cdfe-160">Kodda anahtarı ayarladıysanız `.config` dosyasında ayarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-160">If you set the key in code, you don't have to set it in the `.config` file.</span></span>

## <span data-ttu-id="9cdfe-161"><a name="run"></a> Projenizi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9cdfe-161"><a name="run"></a> Run your project</span></span>
<span data-ttu-id="9cdfe-162">**F5** ile uygulamanızı çalıştırın ve şunu deneyin: birkaç telemetri oluşturmak için farklı sayfalar açın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-162">Use the **F5** to run your application and try it out: open different pages to generate some telemetry.</span></span>

<span data-ttu-id="9cdfe-163">Visual Studio'da gönderilmiş etkinliklerin sayısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-163">In Visual Studio, you'll see a count of the events that have been sent.</span></span>

![Visual Studio’da olay sayımı](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <span data-ttu-id="9cdfe-165"><a name="monitor"></a> Telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9cdfe-165"><a name="monitor"></a> View your telemetry</span></span>
<span data-ttu-id="9cdfe-166">[Azure portal](https://portal.azure.com/)’a geri dönün ve Application Insights kaynağınıza göz atın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-166">Return to the [Azure portal](https://portal.azure.com/) and browse to your Application Insights resource.</span></span>

<span data-ttu-id="9cdfe-167">Genel Bakış grafiklerinde veri arayın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-167">Look for data in the Overview charts.</span></span> <span data-ttu-id="9cdfe-168">İlk olarak yalnızca bir veya iki nokta görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-168">At first, you'll just see one or two points.</span></span> <span data-ttu-id="9cdfe-169">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9cdfe-169">For example:</span></span>

![Daha fazla veri için tıklayın](./media/app-insights-windows-services/12-first-perf.png)

<span data-ttu-id="9cdfe-171">Daha ayrıntılı ölçümler görmek için herhangi bir grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-171">Click through any chart to see more detailed metrics.</span></span> [<span data-ttu-id="9cdfe-172">Ölçümler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-172">Learn more about metrics.</span></span>](app-insights-web-monitor-performance.md)

### <a name="no-data"></a><span data-ttu-id="9cdfe-173">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="9cdfe-173">No data?</span></span>
* <span data-ttu-id="9cdfe-174">Birkaç telemetri oluşturması için farklı sayfaları açarak uygulamayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-174">Use the application, opening different pages so that it generates some telemetry.</span></span>
* <span data-ttu-id="9cdfe-175">Olayları tek tek görmek için [Ara](app-insights-diagnostic-search.md) kutucuğunu açın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-175">Open the [Search](app-insights-diagnostic-search.md) tile, to see individual events.</span></span> <span data-ttu-id="9cdfe-176">Bazı durumlarda olayların ölçüm ardışık düzenine ulaşması biraz daha uzun sürer.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-176">Sometimes it takes events a little while longer to get through the metrics pipeline.</span></span>
* <span data-ttu-id="9cdfe-177">Birkaç saniye bekleyin ve **Yenile**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-177">Wait a few seconds and click **Refresh**.</span></span> <span data-ttu-id="9cdfe-178">Grafikler kendilerini düzenli olarak yeniler, ancak bazı verilerin görüntülenmesini bekliyorsanız el ile yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-178">Charts refresh themselves periodically, but you can refresh manually if you're waiting for some data to show up.</span></span>
* <span data-ttu-id="9cdfe-179">Bkz. [Sorun giderme](app-insights-troubleshoot-faq.md).</span><span class="sxs-lookup"><span data-stu-id="9cdfe-179">See [Troubleshooting](app-insights-troubleshoot-faq.md).</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="9cdfe-180">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="9cdfe-180">Publish your app</span></span>
<span data-ttu-id="9cdfe-181">Şimdi uygulamanızı sunucunuza veya Azure’a dağıtın ve verilerin birikmesini izleyin.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-181">Now deploy your application to your server or to Azure and watch the data accumulate.</span></span>

![Visual Studio kullanarak uygulamanızı yayımlama](./media/app-insights-windows-services/15-publish.png)

<span data-ttu-id="9cdfe-183">Hata ayıklama modunda çalıştırdığınızda telemetri ardışık düzen üzerinden gönderilir, böylece görüntülenen verileri saniyeler içinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-183">When you run in debug mode, telemetry is expedited through the pipeline, so that you should see data appearing within seconds.</span></span> <span data-ttu-id="9cdfe-184">Uygulamanızı Sürüm yapılandırmasında dağıttığınızda veriler daha yavaş birikir.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-184">When you deploy your app in Release configuration, data accumulates more slowly.</span></span>

### <a name="no-data-after-you-publish-to-your-server"></a><span data-ttu-id="9cdfe-185">Sunucunuza yayımladıktan sonra veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="9cdfe-185">No data after you publish to your server?</span></span>
<span data-ttu-id="9cdfe-186">Sunucunuzun güvenlik duvarında giden trafik için bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-186">Open ports for outgoing traffic in your server's firewall.</span></span> <span data-ttu-id="9cdfe-187">Gerekli adreslerin listesi için [bu sayfaya](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) bakın</span><span class="sxs-lookup"><span data-stu-id="9cdfe-187">See [this page](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) for the list of required addresses</span></span> 

### <a name="trouble-on-your-build-server"></a><span data-ttu-id="9cdfe-188">Derleme sunucunuzda sorun mu yaşıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="9cdfe-188">Trouble on your build server?</span></span>
<span data-ttu-id="9cdfe-189">Lütfen [bu Sorun Giderme maddesine](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild) bakın.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-189">Please see [this Troubleshooting item](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild).</span></span>

> [!NOTE]
> <span data-ttu-id="9cdfe-190">Uygulamanız çok sayıda telemetri oluşturuyorsa, uyarlamalı örnekleme modülü olayların yalnızca bir temsilci fraksiyonunu göndererek portala gönderilen hacmi otomatik olarak azaltır.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-190">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="9cdfe-191">Ancak, aynı istekle ilişkili olaylar grup olarak seçilir ya da seçimi kaldırılır, böylece ilgili olaylar arasında gezinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cdfe-191">However, events that are related to the same request will be selected or deselected as a group, so that you can navigate between related events.</span></span> 
> <span data-ttu-id="9cdfe-192">[Örnekleme hakkında bilgi edinin](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9cdfe-192">[Learn about sampling](app-insights-sampling.md).</span></span>
> 
> 

## <a name="video"></a><span data-ttu-id="9cdfe-193">Video</span><span class="sxs-lookup"><span data-stu-id="9cdfe-193">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="9cdfe-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9cdfe-194">Next steps</span></span>
* <span data-ttu-id="9cdfe-195">Uygulamanızın 360 derecelik tam görünümünü elde etmek üzere [daha fazla telemetri ekleyin](app-insights-asp-net-more.md).</span><span class="sxs-lookup"><span data-stu-id="9cdfe-195">[Add more telemetry](app-insights-asp-net-more.md) to get the full 360-degree view of your application.</span></span>

