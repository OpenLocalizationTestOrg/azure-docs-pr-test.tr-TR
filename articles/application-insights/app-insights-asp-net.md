---
title: "Azure Application Insights ile ASP.NET web uygulaması analizi yukarı aaaSet | Microsoft Docs"
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
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="55589-103">ASP.NET web siteniz için Application Insights'ı ayarlama</span><span class="sxs-lookup"><span data-stu-id="55589-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="55589-104">Bu yordam, ASP.NET web uygulaması toosend telemetri toohello yapılandırır [Azure Application Insights](app-insights-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="55589-104">This procedure configures your ASP.NET web app toosend telemetry toohello [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="55589-105">Kendi IIS sunucunuzu veya hello bulut barındırılan ASP.NET uygulamaları için çalışır.</span><span class="sxs-lookup"><span data-stu-id="55589-105">It works for ASP.NET apps that are hosted either in your own IIS server or in hello Cloud.</span></span> <span data-ttu-id="55589-106">Grafikler alın ve yardımcı bir güçlü sorgu dili, uygulamanızın hello performansı ve nasıl kişiler, artı otomatik uyarıları hatalar veya performans sorunları kullandığını anlamak.</span><span class="sxs-lookup"><span data-stu-id="55589-106">You get charts and a powerful query language that help you understand hello performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="55589-107">Geliştiricilerin çoğu bu özellikleri harika olduklarından, ancak aynı zamanda genişletmek ve gerekirse hello telemetri özelleştirme gibi bulun.</span><span class="sxs-lookup"><span data-stu-id="55589-107">Many developers find these features great as they are, but you can also extend and customize hello telemetry if you need to.</span></span>

<span data-ttu-id="55589-108">Visual Studio'da kurulum yalnızca birkaç tıklama ile yapılır.</span><span class="sxs-lookup"><span data-stu-id="55589-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="55589-109">Telemetri hello hacmi sınırlayarak hello seçeneği tooavoid ücretleri sahip.</span><span class="sxs-lookup"><span data-stu-id="55589-109">You have hello option tooavoid charges by limiting hello volume of telemetry.</span></span> <span data-ttu-id="55589-110">Bu, tooexperiment ve hata ayıklama veya toomonitor değil çok sayıda kullanıcı içeren bir site sağlar.</span><span class="sxs-lookup"><span data-stu-id="55589-110">This allows you tooexperiment and debug, or toomonitor a site with not many users.</span></span> <span data-ttu-id="55589-111">Şimdi toogo istediğiniz ve üretim sitesini izleme karar verdiğinizde, daha sonra kolay tooraise hello sınırı olan.</span><span class="sxs-lookup"><span data-stu-id="55589-111">When you decide you want toogo ahead and monitor your production site, it's easy tooraise hello limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="55589-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="55589-112">Before you start</span></span>
<span data-ttu-id="55589-113">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="55589-113">You need:</span></span>

* <span data-ttu-id="55589-114">Visual Studio 2013 güncelleştirme 3 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="55589-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="55589-115">Ne kadar yeniyse o kadar iyidir.</span><span class="sxs-lookup"><span data-stu-id="55589-115">Later is better.</span></span>
* <span data-ttu-id="55589-116">Bir abonelik çok[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="55589-116">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="55589-117">Ekibinizin ve kuruluşunuzun bir Azure aboneliğiniz varsa, hello sahibi, tooit, kullanarak ekleyebilir, [Microsoft hesabı](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="55589-117">If your team or organization has an Azure subscription, hello owner can add you tooit, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="55589-118">İçinde ilgileniyorsanız alternatif konuları toolook adresindeki vardır:</span><span class="sxs-lookup"><span data-stu-id="55589-118">There are alternative topics toolook at if you are interested in:</span></span>

* [<span data-ttu-id="55589-119">Çalışma zamanında bir web uygulamasını izleme</span><span class="sxs-lookup"><span data-stu-id="55589-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="55589-120">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="55589-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="55589-121"><a name="ide"></a>1. adım: hello Application Insights SDK ekleme</span><span class="sxs-lookup"><span data-stu-id="55589-121"><a name="ide"></a> Step 1: Add hello Application Insights SDK</span></span>

<span data-ttu-id="55589-122">Çözüm Gezgini'nde web uygulaması projenize sağ tıklayın ve **Ekle** > **, Application Insights Telemetrisi...**'ni veya **Application Insights'ı Yapılandır**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="55589-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Application Insights Telemetrisi Ekle seçeneğinin vurgulandığı Çözüm Gezgini’nin ekran görüntüsü](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="55589-124">(Visual Studio 2015'te de bulunmaktadır hello yeni proje iletişim kutusunda seçeneği tooadd Application Insights.)</span><span class="sxs-lookup"><span data-stu-id="55589-124">(In Visual Studio 2015, there's also an option tooadd Application Insights in hello New Project dialog.)</span></span>

<span data-ttu-id="55589-125">Toohello Application Insights yapılandırma sayfası devam edin:</span><span class="sxs-lookup"><span data-stu-id="55589-125">Continue toohello Application Insights configuration page:</span></span>

![Uygulamanızı Application Insights'a kaydedin sayfasının ekran görüntüsü](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="55589-127">**a.**</span><span class="sxs-lookup"><span data-stu-id="55589-127">**a.**</span></span> <span data-ttu-id="55589-128">Merhaba hesabınızı ve aboneliğinizi tooaccess Azure kullandığınız seçin.</span><span class="sxs-lookup"><span data-stu-id="55589-128">Select hello account and subscription that you use tooaccess Azure.</span></span>

<span data-ttu-id="55589-129">**b.**</span><span class="sxs-lookup"><span data-stu-id="55589-129">**b.**</span></span> <span data-ttu-id="55589-130">Toosee hello verilerin uygulamanızdan istediğiniz azure'da Hello kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="55589-130">Select hello resource in Azure where you want toosee hello data from your app.</span></span> <span data-ttu-id="55589-131">Genellikle:</span><span class="sxs-lookup"><span data-stu-id="55589-131">Usually:</span></span>

* <span data-ttu-id="55589-132">Tek bir uygulamanın [farklı bileşenleri için tek kaynak](app-insights-monitor-multi-role-apps.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="55589-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="55589-133">İlişkisiz uygulamalar için ayrı kaynaklar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="55589-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="55589-134">Verilerinizin depolandığı tooset hello kaynak grubu veya hello konumu istiyorsanız, **ayarlarını yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="55589-134">If you want tooset hello resource group or hello location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="55589-135">Kaynak, kullanılan toocontrol erişim toodata gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="55589-135">Resource groups are used toocontrol access toodata.</span></span> <span data-ttu-id="55589-136">Örneğin, form kısmı çeşitli uygulamalar varsa aynı hello sistemi içine Application Insights verilerini hello aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="55589-136">For example, if you have several apps that form part of hello same system, you might put their Application Insights data in hello same resource group.</span></span>

<span data-ttu-id="55589-137">**c.**</span><span class="sxs-lookup"><span data-stu-id="55589-137">**c.**</span></span> <span data-ttu-id="55589-138">Bir uç tooavoid ücretleri hello boş veri birimi sınırı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="55589-138">Set a cap at hello free data volume limit, tooavoid charges.</span></span> <span data-ttu-id="55589-139">Application Insights tooa ücretsiz belirli birim telemetri.</span><span class="sxs-lookup"><span data-stu-id="55589-139">Application Insights is free up tooa certain volume of telemetry.</span></span> <span data-ttu-id="55589-140">Merhaba kaynak oluşturulduktan sonra açarak seçiminizi hello portalında değiştirebilirsiniz **özellikleri + fiyatlandırma** > **veri birimi Yönetimi** > **günlük Birim cap**.</span><span class="sxs-lookup"><span data-stu-id="55589-140">After hello resource is created, you can change your selection in hello portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="55589-141">**d.**</span><span class="sxs-lookup"><span data-stu-id="55589-141">**d.**</span></span> <span data-ttu-id="55589-142">Tıklatın **kaydetmek** devam toogo ve Application Insights web uygulamanız için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="55589-142">Click **Register** toogo ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="55589-143">Telemetri toohello gönderilecek [Azure portal](https://portal.azure.com), hem hata ayıklama sırasında hem de uygulamanızı yayımladıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="55589-143">Telemetry will be sent toohello [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="55589-144">**e.**</span><span class="sxs-lookup"><span data-stu-id="55589-144">**e.**</span></span> <span data-ttu-id="55589-145">Hatalarını ayıkladığınız sırada toosend telemetri toohello portal istemiyorsanız, yalnızca hello Application Insights SDK'sı tooyour uygulama Ekle ancak kaynak hello Portalı'nda yapılandırmayın.</span><span class="sxs-lookup"><span data-stu-id="55589-145">If you don't want toosend telemetry toohello portal while you're debugging, just add hello Application Insights SDK tooyour app but don't configure a resource in hello portal.</span></span> <span data-ttu-id="55589-146">Hata ayıklarken Visual Studio'da mümkün toosee telemetri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="55589-146">You will be able toosee telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="55589-147">Daha sonra toothis yapılandırma sayfasına dönmek veya uygulamanızı dağıttıktan sonra kadar beklemeniz ve [telemetriyi çalışma zamanında geçiş](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="55589-147">Later, you can return toothis configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="55589-148"><a name="run"></a> 2. Adım: Uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="55589-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="55589-149">F5 tuşuna basarak uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="55589-149">Run your app with F5.</span></span> <span data-ttu-id="55589-150">Farklı sayfalara toogenerate bazı telemetriyi açın.</span><span class="sxs-lookup"><span data-stu-id="55589-150">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="55589-151">Visual Studio'da günlüğe kaydedilmiş hello etkinliklerin sayısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="55589-151">In Visual Studio, you see a count of hello events that have been logged.</span></span>

![Visual Studio’nun ekran görüntüsü.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="55589-154">Adım 3: Telemetrinize bakma</span><span class="sxs-lookup"><span data-stu-id="55589-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="55589-155">Visual Studio'da veya hello Application Insights web Portalı'nda telemetrinizi görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55589-155">You can see your telemetry either in Visual Studio or in hello Application Insights web portal.</span></span> <span data-ttu-id="55589-156">Arama telemetri Visual Studio toohelp uygulamanızın hatalarını ayıklama.</span><span class="sxs-lookup"><span data-stu-id="55589-156">Search telemetry in Visual Studio toohelp you debug your app.</span></span> <span data-ttu-id="55589-157">Sisteminizin Canlı olduğunda performans ve kullanım hello web Portalı'nda izleyin.</span><span class="sxs-lookup"><span data-stu-id="55589-157">Monitor performance and usage in hello web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="55589-158">Visual Studio'da telemetrinize bakma</span><span class="sxs-lookup"><span data-stu-id="55589-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="55589-159">Visual Studio'da hello Application Insights penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="55589-159">In Visual Studio, open hello Application Insights window.</span></span> <span data-ttu-id="55589-160">Hello tıklayın **Application Insights** düğmesini ya da Çözüm Gezgini'nde, select projenize sağ tıklayıp **Application Insights**ve ardından **arama Canlı Telemetri**.</span><span class="sxs-lookup"><span data-stu-id="55589-160">Either click hello **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="55589-161">Merhaba Visual Studio uygulama Insights arama penceresinde hello bkz **hata ayıklama oturumu verilerden** hello sunucu tarafı, uygulamanızın içinde oluşturulan telemetri için görünümü.</span><span class="sxs-lookup"><span data-stu-id="55589-161">In hello Visual Studio Application Insights Search window, see hello **Data from Debug session** view for telemetry generated in hello server side of your app.</span></span> <span data-ttu-id="55589-162">Hello filtrelerle denemeler yapın ve daha ayrıntılı olay toosee tıklayın.</span><span class="sxs-lookup"><span data-stu-id="55589-162">Experiment with hello filters, and click any event toosee more detail.</span></span>

![Ekran görüntüsü hello hata ayıklama oturumu verilerden hello Application Insights penceresinde görüntüleyebilirsiniz.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="55589-164">Herhangi bir veri görmüyorsanız, hello zaman aralığı doğru olduğundan ve hello arama simgesine tıklayın emin olun.</span><span class="sxs-lookup"><span data-stu-id="55589-164">If you don't see any data, make sure hello time range is correct, and click hello Search icon.</span></span>

<span data-ttu-id="55589-165">[Visual Studio’daki Application Insights araçları hakkında daha fazla bilgi edinin](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="55589-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="55589-166">Web portalında telemetriye bakma</span><span class="sxs-lookup"><span data-stu-id="55589-166">See telemetry in web portal</span></span>

<span data-ttu-id="55589-167">(Tooinstall yalnızca hello SDK seçmedikçe) hello Application Insights web portalındaki telemetriyi de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55589-167">You can also see telemetry in hello Application Insights web portal (unless you chose tooinstall only hello SDK).</span></span> <span data-ttu-id="55589-168">Merhaba portal daha fazla grafikler, analiz aracı ve çapraz bileşen görünümleri Visual Studio'ya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="55589-168">hello portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="55589-169">Merhaba portal ayrıca uyarılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="55589-169">hello portal also provides alerts.</span></span>

<span data-ttu-id="55589-170">Application Insights kaynağınızı açın.</span><span class="sxs-lookup"><span data-stu-id="55589-170">Open your Application Insights resource.</span></span> <span data-ttu-id="55589-171">Ya da oturum içinde toohello [Azure portal](https://portal.azure.com/) ve onu yok veya sağ hello proje Visual Studio'da bulmak ve var olması çalışmasına izin.</span><span class="sxs-lookup"><span data-stu-id="55589-171">Either sign in toohello [Azure portal](https://portal.azure.com/) and find it there, or right-click hello project in Visual Studio, and let it take you there.</span></span>

![Ekran görüntüsü, Visual nasıl tooopen hello Application Insights portalındaki gösteren Studio](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="55589-173">Erişim hata alırsanız: birden fazla dizi Microsoft kimlik bilgisi var ve bu hello yanlış kümesi ile imzalanmış?</span><span class="sxs-lookup"><span data-stu-id="55589-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with hello wrong set?</span></span> <span data-ttu-id="55589-174">Merhaba portalında, oturumu kapatın ve yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="55589-174">In hello portal, sign out and sign in again.</span></span>

<span data-ttu-id="55589-175">Merhaba portal uygulamanızdan hello telemetrinin bir görünümünü açar.</span><span class="sxs-lookup"><span data-stu-id="55589-175">hello portal opens on a view of hello telemetry from your app.</span></span>

![Application Insights’a genel bakış sayfasının ekran görüntüsü](./media/app-insights-asp-net/66.png)

<span data-ttu-id="55589-177">Merhaba Portalı'nda daha fazla ayrıntı döşeme veya grafiği toosee'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="55589-177">In hello portal, click any tile or chart toosee more detail.</span></span>

<span data-ttu-id="55589-178">[Hello Azure portalında Application Insights kullanma hakkında daha fazla bilgi](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="55589-178">[Learn more about using Application Insights in hello Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="55589-179">4. Adım: Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="55589-179">Step 4: Publish your app</span></span>
<span data-ttu-id="55589-180">Uygulama tooyour IIS sunucusu veya tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="55589-180">Publish your app tooyour IIS server or tooAzure.</span></span> <span data-ttu-id="55589-181">Gözcü [ölçümleri bir canlı akışı](app-insights-metrics-explorer.md#live-metrics-stream) toomake emin her şeyi sorunsuz çalışır.</span><span class="sxs-lookup"><span data-stu-id="55589-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) toomake sure everything is running smoothly.</span></span>

<span data-ttu-id="55589-182">Burada izleyebilir ölçümleri, telemetrinizi arama ve ayarlanan hello Application Insights portalında, telemetrinizi derlemeler [panolar](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="55589-182">Your telemetry builds up in hello Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="55589-183">Ayrıca hello güçlü kullanabilirsiniz [günlük analizi sorgu dili](https://docs.loganalytics.io/) tooanalyze kullanım ve performans veya toofind belirli olaylar.</span><span class="sxs-lookup"><span data-stu-id="55589-183">You can also use hello powerful [Log Analytics query language](https://docs.loganalytics.io/) tooanalyze usage and performance, or toofind specific events.</span></span>

<span data-ttu-id="55589-184">Ayrıca, telemetri tooanalyze devam edebilirsiniz [Visual Studio](app-insights-visual-studio.md), tanılama arama gibi araçlar ve [eğilimleri](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="55589-184">You can also continue tooanalyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="55589-185">Uygulamanızı yeterli telemetri tooapproach hello gönderirse [azaltma sınırları](app-insights-pricing.md#limits-summary), otomatik [örnekleme](app-insights-sampling.md) anahtarlarını.</span><span class="sxs-lookup"><span data-stu-id="55589-185">If your app sends enough telemetry tooapproach hello [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="55589-186">Örnekleme tanılama amacıyla ilişkili verileri korurken, uygulamanızdan gönderilen telemetri hello miktarını azaltır.</span><span class="sxs-lookup"><span data-stu-id="55589-186">Sampling reduces hello quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="55589-187"><a name="land"></a> İşiniz tamamlandı</span><span class="sxs-lookup"><span data-stu-id="55589-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="55589-188">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="55589-188">Congratulations!</span></span> <span data-ttu-id="55589-189">Uygulamanızda hello Application Insights paketini yüklü ve Azure üzerinde toosend telemetri toohello Application Insights hizmeti yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="55589-189">You installed hello Application Insights package in your app, and configured it toosend telemetry toohello Application Insights service on Azure.</span></span>

![Telemetri hareketlerinin diyagramı](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="55589-191">Merhaba, uygulamanızın telemetri alır Azure kaynak tarafından tanımlanan bir *izleme anahtarını*.</span><span class="sxs-lookup"><span data-stu-id="55589-191">hello Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="55589-192">Bu anahtar hello Applicationınsights.config dosyasında bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55589-192">You'll find this key in hello ApplicationInsights.config file.</span></span>


## <a name="upgrade-toofuture-sdk-versions"></a><span data-ttu-id="55589-193">Toofuture SDK sürümlerine yükseltme</span><span class="sxs-lookup"><span data-stu-id="55589-193">Upgrade toofuture SDK versions</span></span>
<span data-ttu-id="55589-194">tooupgrade tooa [hello SDK'ın yeni sürümüne](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)açın hello **NuGet Paket Yöneticisi** yeniden ve yüklü paketleri filtre.</span><span class="sxs-lookup"><span data-stu-id="55589-194">tooupgrade tooa [new release of hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open hello **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="55589-195">**Microsoft.ApplicationInsights.Web**’i seçip **Yükselt**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="55589-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="55589-196">Tüm özelleştirmeler tooApplicationInsights.config yaptıysanız yükseltmeden önce bir kopyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="55589-196">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="55589-197">Daha sonra değişikliklerinizi hello yeni sürümle birleştirin.</span><span class="sxs-lookup"><span data-stu-id="55589-197">Then, merge your changes into hello new version.</span></span>

## <a name="video"></a><span data-ttu-id="55589-198">Video</span><span class="sxs-lookup"><span data-stu-id="55589-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="55589-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="55589-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="55589-200">Daha fazla telemetri</span><span class="sxs-lookup"><span data-stu-id="55589-200">More telemetry</span></span>

* <span data-ttu-id="55589-201">**[Tarayıcı ve sayfa yükleme verileri](app-insights-javascript.md)** - Web sayfalarınıza bir kod parçacığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="55589-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="55589-202">**[Daha ayrıntılı bağımlılık ve özel durum izlemesi alın](app-insights-monitor-performance-live-website-now.md)** - Sunucunuza Durum İzleyicisi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="55589-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="55589-203">**[Özel olaylar kod](app-insights-api-custom-events-metrics.md)**  toocount, saat ya da kullanıcı eylemlerini ölçün.</span><span class="sxs-lookup"><span data-stu-id="55589-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** toocount, time, or measure user actions.</span></span>
* <span data-ttu-id="55589-204">**[Günlük verilerini alma](app-insights-asp-net-trace-logs.md)** - Günlük verilerini telemetrinizle ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="55589-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="55589-205">Analiz</span><span class="sxs-lookup"><span data-stu-id="55589-205">Analysis</span></span>

* <span data-ttu-id="55589-206">**[Visual Studio’da Application Insights ile çalışma](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="55589-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="55589-207">Telemetri ile hata ayıklama hakkında bilgi içeren tanılama arama ve toocode ayrıntılarına gidin.</span><span class="sxs-lookup"><span data-stu-id="55589-207">Includes information about debugging with telemetry, diagnostic search, and drill through toocode.</span></span>
* <span data-ttu-id="55589-208">**[Merhaba Application Insights portalıyla çalışma](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="55589-208">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="55589-209">Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulamanızın canlı bağımlılık haritası ve telemetriyi dışarı aktarma hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="55589-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="55589-210">**[Analytics](app-insights-analytics-tour.md)**  -hello güçlü sorgu dili.</span><span class="sxs-lookup"><span data-stu-id="55589-210">**[Analytics](app-insights-analytics-tour.md)** - hello powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="55589-211">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="55589-211">Alerts</span></span>

* <span data-ttu-id="55589-212">[Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md): testleri oluşturma toomake sitenizi hello Web'de göründüğünden emin.</span><span class="sxs-lookup"><span data-stu-id="55589-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests toomake sure your site is visible on hello web.</span></span>
* <span data-ttu-id="55589-213">[Akıllı tanılama](app-insights-proactive-diagnostics.md): toodo tooset herhangi bir şey yok Bu testler otomatik olarak çalıştırmaz, bu nedenle bunları ayarlama.</span><span class="sxs-lookup"><span data-stu-id="55589-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have toodo anything tooset them up.</span></span> <span data-ttu-id="55589-214">Uygulamanızda olağan dışı oranda başarısız istek olup olmadığını bildirirler.</span><span class="sxs-lookup"><span data-stu-id="55589-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="55589-215">[Ölçüm uyarıları](app-insights-alerts.md): Bu toowarn ayarlayın, bir ölçüm bir eşik kestiği durumunda.</span><span class="sxs-lookup"><span data-stu-id="55589-215">[Metric alerts](app-insights-alerts.md): Set these toowarn you if a metric crosses a threshold.</span></span> <span data-ttu-id="55589-216">Bunları, uygulamanıza kodladığınız özel ölçümlerde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55589-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="55589-217">Otomasyon</span><span class="sxs-lookup"><span data-stu-id="55589-217">Automation</span></span>

* [<span data-ttu-id="55589-218">Application Insights kaynağı oluşturmayı otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="55589-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
