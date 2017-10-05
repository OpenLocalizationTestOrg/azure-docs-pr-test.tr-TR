---
title: "Azure Application Insights ile ASP.NET Web uygulaması analizi ayarlama | Microsoft Docs"
description: "Şirket içi veya Azure’de barındırılan ASP.NET web siteniz için performans, kullanılabilirlik ve kullanım analizi yapılandırın."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: cb247ee68da88265f7c51258644064463d44f8b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="9ab50-103">ASP.NET web siteniz için Application Insights'ı ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ab50-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="9ab50-104">Bu yordam ASP.NET web uygulamanızı [Azure Application Insights](app-insights-overview.md) hizmetine telemetri gönderecek şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="9ab50-105">Kendi IIS sunucunuzda veya Bulut’ta barındırılan ASP.NET uygulamaları için çalışır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span></span> <span data-ttu-id="9ab50-106">Uygulamanızın performansını ve nasıl kullanıldığını anlamanıza yardımcı olan grafikler ve güçlü bir sorgu dilinin yanı sıra hata ya da performans sorunları hakkında otomatik uyarılar alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9ab50-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="9ab50-107">Çoğu geliştirici, özellikleri bu haliyle mükemmel bulsa da, gerekirse telemetriyi genişletip özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="9ab50-108">Visual Studio'da kurulum yalnızca birkaç tıklama ile yapılır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="9ab50-109">Telemetri hacmini sınırlayarak ücret doğmamasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="9ab50-110">Bunun yapılması, çok fazla kullanıcı olmadan bir siteyi deneyip hatalarını ayıklamanıza veya izlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="9ab50-111">Devam edip üretim merkezinizi izlemeye karar verdiğinizde, sınırı daha sonra kolayca artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9ab50-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="9ab50-112">Before you start</span></span>
<span data-ttu-id="9ab50-113">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="9ab50-113">You need:</span></span>

* <span data-ttu-id="9ab50-114">Visual Studio 2013 güncelleştirme 3 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="9ab50-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="9ab50-115">Ne kadar yeniyse o kadar iyidir.</span><span class="sxs-lookup"><span data-stu-id="9ab50-115">Later is better.</span></span>
* <span data-ttu-id="9ab50-116">Bir [Microsoft Azure](http://azure.com) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="9ab50-116">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="9ab50-117">Takımınızın veya kuruluşunuzun Azure aboneliği varsa, abonelik sahibi [Microsoft hesabınızı](http://live.com) kullanarak sizi aboneliğe ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="9ab50-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="9ab50-118">İlginizi çekiyorsa inceleyebileceğiniz alternatif konu başlıkları da mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="9ab50-118">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="9ab50-119">Çalışma zamanında bir web uygulamasını izleme</span><span class="sxs-lookup"><span data-stu-id="9ab50-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="9ab50-120">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="9ab50-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="9ab50-121"><a name="ide"></a> 1. Adım: Application Insights SDK’yı ekleme</span><span class="sxs-lookup"><span data-stu-id="9ab50-121"><a name="ide"></a> Step 1: Add the Application Insights SDK</span></span>

<span data-ttu-id="9ab50-122">Çözüm Gezgini'nde web uygulaması projenize sağ tıklayın ve **Ekle** > **, Application Insights Telemetrisi...**'ni veya **Application Insights'ı Yapılandır**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Application Insights Telemetrisi Ekle seçeneğinin vurgulandığı Çözüm Gezgini’nin ekran görüntüsü](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="9ab50-124">(Visual Studio 2015'te Yeni Proje iletişim kutusunda da Application Insights ekleme seçeneği mevcuttur.)</span><span class="sxs-lookup"><span data-stu-id="9ab50-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span></span>

<span data-ttu-id="9ab50-125">Application Insights yapılandırma sayfasına gidin:</span><span class="sxs-lookup"><span data-stu-id="9ab50-125">Continue to the Application Insights configuration page:</span></span>

![Uygulamanızı Application Insights'a kaydedin sayfasının ekran görüntüsü](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="9ab50-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="9ab50-127">**a.**</span></span> <span data-ttu-id="9ab50-128">Azure'a erişmek için kullandığınız hesabı ve aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-128">Select the account and subscription that you use to access Azure.</span></span>

<span data-ttu-id="9ab50-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="9ab50-129">**b.**</span></span> <span data-ttu-id="9ab50-130">Uygulamanızdan gelen verileri görmek istediğiniz Azure kaynağını seçin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-130">Select the resource in Azure where you want to see the data from your app.</span></span> <span data-ttu-id="9ab50-131">Genellikle:</span><span class="sxs-lookup"><span data-stu-id="9ab50-131">Usually:</span></span>

* <span data-ttu-id="9ab50-132">Tek bir uygulamanın [farklı bileşenleri için tek kaynak](app-insights-monitor-multi-role-apps.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="9ab50-133">İlişkisiz uygulamalar için ayrı kaynaklar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ab50-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="9ab50-134">Verilerin depolandığı kaynak grubunu veya konumu ayarlamak isterseniz **Ayarları yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-134">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="9ab50-135">Kaynak grupları, verilere erişimi denetlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-135">Resource groups are used to control access to data.</span></span> <span data-ttu-id="9ab50-136">Örneğin aynı sistemin parçalarını oluşturan birden uygulamanız varsa bunların Application Insights verilerini aynı kaynak grubuna ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-136">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

<span data-ttu-id="9ab50-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="9ab50-137">**c.**</span></span> <span data-ttu-id="9ab50-138">Ücret yansımaması için ücretsiz veri hacmi sınırında bir sınır ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-138">Set a cap at the free data volume limit, to avoid charges.</span></span> <span data-ttu-id="9ab50-139">Application Insights, belirli bir telemetri hacmine kadar ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="9ab50-139">Application Insights is free up to a certain volume of telemetry.</span></span> <span data-ttu-id="9ab50-140">Kaynak oluşturulduktan sonra portalda **Özellikler + fiyatlandırma** > **Veri hacmi yönetimi** > **Günlük hacim sınırı** sayfasından seçiminizi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-140">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="9ab50-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="9ab50-141">**d.**</span></span> <span data-ttu-id="9ab50-142">Devam etmek ve web uygulamanızda Application Insights'ı yapılandırmak için **Kaydol**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-142">Click **Register** to go ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="9ab50-143">Telemetri hem hata ayıklama sırasında hem de uygulamanızı yayımladıktan sonra [Azure portalına](https://portal.azure.com) gönderilir.</span><span class="sxs-lookup"><span data-stu-id="9ab50-143">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="9ab50-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="9ab50-144">**e.**</span></span> <span data-ttu-id="9ab50-145">Hata ayıklama sırasında portala telemetri göndermek istemiyorsanız, uygulamanıza Application Insights SDK’sını ekleyin, ancak portalda bir kaynak yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-145">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="9ab50-146">Hata ayıklama sırasında telemetri verilerini Visual Studio'da görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-146">You will be able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="9ab50-147">Daha sonra bu yapılandırma sayfasına dönebilir veya uygulamanızı dağıtana kadar bekleyip [telemetriyi çalışma zamanında açabilirsiniz](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="9ab50-147">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="9ab50-148"><a name="run"></a> 2. Adım: Uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9ab50-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="9ab50-149">F5 tuşuna basarak uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-149">Run your app with F5.</span></span> <span data-ttu-id="9ab50-150">Farklı sayfalar açarak telemetri verileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ab50-150">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="9ab50-151">Visual Studio'da, günlüğe kaydedilmiş etkinliklerin sayısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-151">In Visual Studio, you see a count of the events that have been logged.</span></span>

![Visual Studio’nun ekran görüntüsü.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="9ab50-154">Adım 3: Telemetrinize bakma</span><span class="sxs-lookup"><span data-stu-id="9ab50-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="9ab50-155">Visual Studio’da veya Application Insights web portalında telemetrinizi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-155">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="9ab50-156">Uygulamanızın hatalarını ayıklamanıza yardımcı olması için Visual Studio'da telemetri arayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-156">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="9ab50-157">Sisteminiz canlıyken web portalında performans ve kullanımı izleyin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-157">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="9ab50-158">Visual Studio'da telemetrinize bakma</span><span class="sxs-lookup"><span data-stu-id="9ab50-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="9ab50-159">Visual Studio’da Application Insights penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-159">In Visual Studio, open the Application Insights window.</span></span> <span data-ttu-id="9ab50-160">**Application Insights** düğmesine tıklayın veya Çözüm Gezgini’nden projenize sağ tıklayıp **Application Insights**’ı seçin ve ardından **Canlı Telemetride Ara**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-160">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="9ab50-161">Visual Studio Application Insights Arama penceresinde, uygulamanızın sunucu tarafında oluşturulan telemetri için **Hata Ayıklama oturumundan alınan veriler** görünümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-161">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="9ab50-162">Filtrelerle denemeler yapın ve daha fazla ayrıntı için herhangi bir etkinliğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-162">Experiment with the filters, and click any event to see more detail.</span></span>

![Application Insights penceresindeki Hata ayıklama oturumundan alınan veriler görünümünün ekran görüntüsü.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="9ab50-164">Herhangi bir veri gösterilmiyorsa zaman aralığının doğru olduğundan emin olup Ara simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-164">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="9ab50-165">[Visual Studio’daki Application Insights araçları hakkında daha fazla bilgi edinin](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9ab50-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="9ab50-166">Web portalında telemetriye bakma</span><span class="sxs-lookup"><span data-stu-id="9ab50-166">See telemetry in web portal</span></span>

<span data-ttu-id="9ab50-167">Yalnızca SDK’yı yüklemeyi seçmediyseniz telemetriyi Application Insights web portalında da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-167">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="9ab50-168">Portalda, Visual Studio’ya kıyasla daha çok grafik, analiz aracı ve bileşenler arası görünüm bulunur.</span><span class="sxs-lookup"><span data-stu-id="9ab50-168">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="9ab50-169">Portal ayrıca uyarılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ab50-169">The portal also provides alerts.</span></span>

<span data-ttu-id="9ab50-170">Application Insights kaynağınızı açın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-170">Open your Application Insights resource.</span></span> <span data-ttu-id="9ab50-171">[Azure portalında](https://portal.azure.com/) oturum açıp portalda bulun ya da Visual Studio’da projeye sağ tıklayıp sizi yönlendirmesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-171">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span></span>

![Visual Studio’da Application Insights portalının nasıl açılacağını gösteren ekran görüntüsü](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="9ab50-173">Bir erişim hatası alırsanız: Birden çok Microsoft kimlik bilgisi kümeniz mi var ve yanlış küme ile mi oturum açtınız?</span><span class="sxs-lookup"><span data-stu-id="9ab50-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span></span> <span data-ttu-id="9ab50-174">Portalda oturumunuzu kapatıp yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-174">In the portal, sign out and sign in again.</span></span>

<span data-ttu-id="9ab50-175">Portal, uygulamanızdan alınan telemetri görünümünde açılır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-175">The portal opens on a view of the telemetry from your app.</span></span>

![Application Insights’a genel bakış sayfasının ekran görüntüsü](./media/app-insights-asp-net/66.png)

<span data-ttu-id="9ab50-177">Daha fazla ayrıntı görmek için portalda istediğiniz kutucuğa veya grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-177">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="9ab50-178">[Azure portalında Application Insights kullanma hakkında daha fazla bilgi edinin](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="9ab50-178">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="9ab50-179">4. Adım: Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="9ab50-179">Step 4: Publish your app</span></span>
<span data-ttu-id="9ab50-180">Uygulamanızı IIS sunucunuza veya Azure’a yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-180">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="9ab50-181">Her şeyin sorunsuz çalıştığından emin olmak için [Canlı Ölçümler Akışı](app-insights-metrics-explorer.md#live-metrics-stream)’nı izleyin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="9ab50-182">Telemetriniz Application Insights portalında biriktirilir ve burada ölçümlerinizi izleyebilir, telemetrinizde arama yapabilir ve [panolar](app-insights-dashboards.md) ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-182">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="9ab50-183">Ayrıca, güçlü [Log Analytics sorgu dili](https://docs.loganalytics.io/)’ni kullanarak kullanımı ve performansı analiz edebilir ya da belirli olayları bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-183">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="9ab50-184">Telemetrinizi tanılama araması ve [eğilimler](app-insights-visual-studio-trends.md) gibi araçlarla [Visual Studio](app-insights-visual-studio.md)’da analiz etmeye de devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-184">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9ab50-185">Uygulamanız [azaltma sınırlarına](app-insights-pricing.md#limits-summary) yaklaşmak için yeterli telemetri gönderiyorsa, otomatik [örnekleme](app-insights-sampling.md) etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9ab50-185">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="9ab50-186">Örnekleme, tanılama amaçlı bağlantı verilerini korurken uygulamanızdan gönderilen telemetri miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-186">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="9ab50-187"><a name="land"></a> İşiniz tamamlandı</span><span class="sxs-lookup"><span data-stu-id="9ab50-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="9ab50-188">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="9ab50-188">Congratulations!</span></span> <span data-ttu-id="9ab50-189">Application Insights paketini uygulamanıza yüklediniz ve Azure üzerinde Application Insights hizmetine telemetri gönderecek şekilde yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="9ab50-189">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Telemetri hareketlerinin diyagramı](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="9ab50-191">Uygulamanızın telemetrisini alan Azure kaynağı bir *izleme anahtarı* ile tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9ab50-191">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="9ab50-192">Bu anahtarı ApplicationInsights.config dosyasında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-192">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="9ab50-193">Gelecek SDK sürümlerine yükseltme</span><span class="sxs-lookup"><span data-stu-id="9ab50-193">Upgrade to future SDK versions</span></span>
<span data-ttu-id="9ab50-194">[SDK’nın yeni bir sürümüne](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases) yükseltmek için **NuGet paket yöneticisini** yeniden açıp yüklü paketleri filtreleyin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-194">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="9ab50-195">**Microsoft.ApplicationInsights.Web**’i seçip **Yükselt**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="9ab50-196">ApplicationInsights.config’de herhangi bir özelleştirme gerçekleştirdiyseniz yükseltmeden önce dosyanın bir kopyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-196">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="9ab50-197">Daha sonra, yaptığınız değişiklikleri yeni sürümle birleştirin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-197">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="9ab50-198">Video</span><span class="sxs-lookup"><span data-stu-id="9ab50-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="9ab50-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ab50-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="9ab50-200">Daha fazla telemetri</span><span class="sxs-lookup"><span data-stu-id="9ab50-200">More telemetry</span></span>

* <span data-ttu-id="9ab50-201">**[Tarayıcı ve sayfa yükleme verileri](app-insights-javascript.md)** - Web sayfalarınıza bir kod parçacığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="9ab50-202">**[Daha ayrıntılı bağımlılık ve özel durum izlemesi alın](app-insights-monitor-performance-live-website-now.md)** - Sunucunuza Durum İzleyicisi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="9ab50-203">Kullanıcı eylemlerini saymak, zamanlamak veya ölçmek için **[özel olaylar kodlayın](app-insights-api-custom-events-metrics.md)**.</span><span class="sxs-lookup"><span data-stu-id="9ab50-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="9ab50-204">**[Günlük verilerini alma](app-insights-asp-net-trace-logs.md)** - Günlük verilerini telemetrinizle ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="9ab50-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="9ab50-205">Analiz</span><span class="sxs-lookup"><span data-stu-id="9ab50-205">Analysis</span></span>

* <span data-ttu-id="9ab50-206">**[Visual Studio’da Application Insights ile çalışma](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="9ab50-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="9ab50-207">Telemetri, tanılama araması ve kodun detayına gitme ile hata ayıklama hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="9ab50-207">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="9ab50-208">**[Application Insights portalıyla çalışma](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="9ab50-208">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="9ab50-209">Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulamanızın canlı bağımlılık haritası ve telemetriyi dışarı aktarma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="9ab50-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="9ab50-210">**[Analytics](app-insights-analytics-tour.md)** - Güçlü sorgu dili.</span><span class="sxs-lookup"><span data-stu-id="9ab50-210">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="9ab50-211">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="9ab50-211">Alerts</span></span>

* <span data-ttu-id="9ab50-212">[Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md): Sitenizin web’de görünür olduğundan emin olmaya yönelik testler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9ab50-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="9ab50-213">[Akıllı tanılama](app-insights-proactive-diagnostics.md): Bu testler otomatik olarak çalıştığından, bunları ayarlamak için herhangi bir şey yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ab50-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="9ab50-214">Uygulamanızda olağan dışı oranda başarısız istek olup olmadığını bildirirler.</span><span class="sxs-lookup"><span data-stu-id="9ab50-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="9ab50-215">[Ölçüm uyarıları](app-insights-alerts.md): Bir metrik tarafından herhangi bir eşiğin aşılması durumunda uyarı almak için bunları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ab50-215">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="9ab50-216">Bunları, uygulamanıza kodladığınız özel ölçümlerde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ab50-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="9ab50-217">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="9ab50-217">Automation</span></span>

* [<span data-ttu-id="9ab50-218">Application Insights kaynağı oluşturmayı otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="9ab50-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
