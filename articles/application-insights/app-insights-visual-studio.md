---
title: Visual Studio'da Azure Application Insights aaaDebug uygulamalarla | Microsoft Docs
description: "Hata ayıklama ve üretim sırasında wen uygulaması performans analizi ve tanılama."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a><span data-ttu-id="a8d5d-103">Visual Studio'da Azure Application Insights uygulamalarınızla hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="a8d5d-103">Debug your applications with Azure Application Insights in Visual Studio</span></span>
<span data-ttu-id="a8d5d-104">Visual Studio’da (2015 ve sonraki sürümler) hem hata ayıklama hem de üretim sırasında [Azure Application Insights](app-insights-overview.md)’tan alınan telemetri verilerini kullanarak, ASP.NET web uygulamanızdaki performansı çözümleyebilir ve sorunları tanılayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-104">In Visual Studio (2015 and later), you can analyze performance and diagnose issues in your ASP.NET web app both in debugging and in production, using telemetry from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="a8d5d-105">Visual Studio 2017'nı kullanarak ASP.NET web uygulamanızı oluşturduğunuz veya daha sonra hello Application Insights SDK'sı zaten sahip olur.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-105">If you created your ASP.NET web app using Visual Studio 2017 or later, it already has hello Application Insights SDK.</span></span> <span data-ttu-id="a8d5d-106">Aksi takdirde, bu nedenle, bu işlemi yapmadıysanız [Application Insights tooyour uygulama Ekle](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="a8d5d-106">Otherwise, if you haven't done so already, [add Application Insights tooyour app](app-insights-asp-net.md).</span></span>

<span data-ttu-id="a8d5d-107">toomonitor uygulamanızı Canlı üretimde olduğunda, normalde hello hello Application Insights telemetriyi görüntüleyebilir [Azure portal](https://portal.azure.com), burada uyarıları ayarlama ve güçlü izleme araçlarını uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-107">toomonitor your app when it's in live production, you normally view hello Application Insights telemetry in hello [Azure portal](https://portal.azure.com), where you can set alerts and apply powerful monitoring tools.</span></span> <span data-ttu-id="a8d5d-108">Ancak, hata ayıklama için ayrıca arama ve Visual Studio hello telemetriyi çözümle.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-108">But for debugging, you can also search and analyze hello telemetry in Visual Studio.</span></span> <span data-ttu-id="a8d5d-109">Visual Studio tooanalyze telemetri üretim sitenizden hem çalıştırır, geliştirme makinenizde hata ayıklama kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-109">You can use Visual Studio tooanalyze telemetry both from your production site and from debugging runs on your development machine.</span></span> <span data-ttu-id="a8d5d-110">Merhaba SDK toosend telemetri toohello Azure portal henüz yapılandırılmamış henüz olsa bile, hello ikinci durumda, hata ayıklama çalışmalarınızı çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-110">In hello latter case, you can analyze debugging runs even if you haven't yet configured hello SDK toosend telemetry toohello Azure portal.</span></span> 

## <span data-ttu-id="a8d5d-111"><a name="run"></a> Projenizin hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="a8d5d-111"><a name="run"></a> Debug your project</span></span>
<span data-ttu-id="a8d5d-112">F5 kullanarak web uygulamanızı yerel hata ayıklama modunda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-112">Run your web app in local debug mode by using F5.</span></span> <span data-ttu-id="a8d5d-113">Farklı sayfalara toogenerate bazı telemetriyi açın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-113">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="a8d5d-114">Visual Studio'da, projenizdeki hello Application Insights modülü tarafından günlüğe hello etkinliklerin sayısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-114">In Visual Studio, you see a count of hello events that have been logged by hello Application Insights module in your project.</span></span>

![Visual Studio'da hata ayıklama sırasında hello Application Insights düğmesi gösterilir.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

<span data-ttu-id="a8d5d-116">Bu düğme toosearch telemetrinizi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-116">Click this button toosearch your telemetry.</span></span> 

## <a name="application-insights-search"></a><span data-ttu-id="a8d5d-117">Application Insights araması</span><span class="sxs-lookup"><span data-stu-id="a8d5d-117">Application Insights search</span></span>
<span data-ttu-id="a8d5d-118">Merhaba uygulama Insights arama penceresi günlüğe kaydedilmiş olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-118">hello Application Insights Search window shows events that have been logged.</span></span> <span data-ttu-id="a8d5d-119">(Application Insights'ı ayarladığınızda tooAzure kaydolduysanız arayabilirsiniz hello hello Azure portal'ın olaylar ile aynıdır.)</span><span class="sxs-lookup"><span data-stu-id="a8d5d-119">(If you signed in tooAzure when you set up Application Insights, you can search hello same events in hello Azure portal.)</span></span>

![Merhaba projesine sağ tıklayın ve Application Insights seçme arama](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> <span data-ttu-id="a8d5d-121">Filtre seçimini kaldırın veya seçin sonra hello metin arama alanı hello sonunda hello arama düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-121">After you select or deselect filters, click hello Search button at hello end of hello text search field.</span></span>
>

<span data-ttu-id="a8d5d-122">Merhaba serbest metin arama hello olayları tüm alanlarda çalışır.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-122">hello free text search works on any fields in hello events.</span></span> <span data-ttu-id="a8d5d-123">Örneğin, bir sayfanın hello URL'SİNİN bir parçası için arama; ya da istemcinin şehri gibi bir özelliğin değerini hello; veya bir izleme günlüğündeki belirli kelimeleri.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-123">For example, search for part of hello URL of a page; or hello value of a property such as client city; or specific words in a trace log.</span></span>

<span data-ttu-id="a8d5d-124">Tüm olay toosee ayrıntılı özelliklerini'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-124">Click any event toosee its detailed properties.</span></span>

<span data-ttu-id="a8d5d-125">İstekleri tooyour web uygulaması için toohello koduyla tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-125">For requests tooyour web app, you can click through toohello code.</span></span>

![İstek Ayrıntıları altında toohello koduyla'ı tıklatın.](./media/app-insights-visual-studio/31.png)

<span data-ttu-id="a8d5d-127">İlgili öğeler de açabilirsiniz toohelp tanılamak başarısız isteklerin veya özel durumları.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-127">You can also open related items toohelp diagnose failed requests or exceptions.</span></span>

![İstek Ayrıntıları altında toorelated öğeleri kaydırın](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a><span data-ttu-id="a8d5d-129">Özel durumları görüntüle ve başarısız isteklerin</span><span class="sxs-lookup"><span data-stu-id="a8d5d-129">View exceptions and failed requests</span></span>
<span data-ttu-id="a8d5d-130">Merhaba arama penceresinde özel durum raporları göster.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-130">Exception reports show in hello Search window.</span></span> <span data-ttu-id="a8d5d-131">(ASP.NET uygulaması bazı eski türlerinde çok elinizde[özel durum izleme ayarladıysanız](app-insights-asp-net-exceptions.md) hello çerçevesi tarafından işlenen toosee özel durumlar.)</span><span class="sxs-lookup"><span data-stu-id="a8d5d-131">(In some older types of ASP.NET application, you have too[set up exception monitoring](app-insights-asp-net-exceptions.md) toosee exceptions that are handled by hello framework.)</span></span>

<span data-ttu-id="a8d5d-132">Bir özel durum tooget Yığın İzleme'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-132">Click an exception tooget a stack trace.</span></span> <span data-ttu-id="a8d5d-133">Visual Studio'da hello uygulamanın Hello kodunu açıksa, hello yığın izleme toohello ilgili satırından hello kod aracılığıyla tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-133">If hello code of hello app is open in Visual Studio, you can click through from hello stack trace toohello relevant line of hello code.</span></span>

![Özel durum yığın izlemesi](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a><span data-ttu-id="a8d5d-135">Merhaba kodda istek ve özel durum özetlerini görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="a8d5d-135">View request and exception summaries in hello code</span></span>
<span data-ttu-id="a8d5d-136">Hello her işleyici yöntemi Yukarıdaki kod Mercek satır, hello istekler ve özel durumlar Application Insights tarafından hello son 24 h oturum sayısını bakın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-136">In hello Code Lens line above each handler method, you see a count of hello requests and exceptions logged by Application Insights in hello past 24 h.</span></span>

![Özel durum yığın izlemesi](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> <span data-ttu-id="a8d5d-138">Kod Mercek varsa yalnızca Application Insights verileri gösterir [uygulama toosend telemetri toohello Application Insights portalınızdaki yapılandırılmış](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="a8d5d-138">Code Lens shows Application Insights data only if you have [configured your app toosend telemetry toohello Application Insights portal](app-insights-asp-net.md).</span></span>
>

[<span data-ttu-id="a8d5d-139">Kod Odağı’nda Application Insights hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="a8d5d-139">More about Application Insights in Code Lens</span></span>](app-insights-visual-studio-codelens.md)

## <a name="trends"></a><span data-ttu-id="a8d5d-140">Eğilimler</span><span class="sxs-lookup"><span data-stu-id="a8d5d-140">Trends</span></span>
<span data-ttu-id="a8d5d-141">Eğilimler, uygulamanızın zaman içinde nasıl davrandığını görselleştirmeye yönelik bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-141">Trends is a tool for visualizing how your app behaves over time.</span></span> 

<span data-ttu-id="a8d5d-142">Seçin **Telemetri eğilimlerini keşfet** hello Application Insights araç çubuğu düğmesini veya uygulama Insights arama penceresi.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-142">Choose **Explore Telemetry Trends** from hello Application Insights toolbar button or Application Insights Search window.</span></span> <span data-ttu-id="a8d5d-143">Başlatılan beş ortak sorguları tooget birini seçin.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-143">Choose one of five common queries tooget started.</span></span> <span data-ttu-id="a8d5d-144">Telemetri türleri, zaman aralıkları ve diğer özelliklere göre farklı veri kümelerini çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-144">You can analyze different datasets based on telemetry types, time ranges, and other properties.</span></span> 

<span data-ttu-id="a8d5d-145">verilerinizde, toofind anormallikleri hello "Görünüm türü" açılan altındaki hello anomali seçeneklerden birini seçin.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-145">toofind anomalies in your data, choose one of hello anomaly options under hello "View Type" dropdown.</span></span> <span data-ttu-id="a8d5d-146">Merhaba filtreleme seçenekleri hello pencerenin hello altındaki içinde kolay toohone üzerinde belirli alt olun.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-146">hello filtering options at hello bottom of hello window make it easy toohone in on specific subsets of your telemetry.</span></span>

![Eğilimler](./media/app-insights-visual-studio/51.png)

<span data-ttu-id="a8d5d-148">[Eğilimler hakkında daha fazla bilgi](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="a8d5d-148">[More about Trends](app-insights-visual-studio-trends.md).</span></span>

## <a name="local-monitoring"></a><span data-ttu-id="a8d5d-149">Yerel izleme</span><span class="sxs-lookup"><span data-stu-id="a8d5d-149">Local monitoring</span></span>
<span data-ttu-id="a8d5d-150">(Visual Studio 2015 Update'ten 2) Merhaba SDK toosend telemetri toohello Application Insights portalındaki yapılandırmadıysanız (yani izleme anahtarı Applicationınsights.Config'de) hello tanılama penceresinde en son hata ayıklama oturumunuzda telemetri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-150">(From Visual Studio 2015 Update 2) If you haven't configured hello SDK toosend telemetry toohello Application Insights portal (so that there is no instrumentation key in ApplicationInsights.config) then hello diagnostics window displays telemetry from your latest debugging session.</span></span> 

<span data-ttu-id="a8d5d-151">Daha önce uygulamanızın önceki bir sürümünü yayımladıysanız bu iyi bir şeydir.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-151">This is desirable if you have already published a previous version of your app.</span></span> <span data-ttu-id="a8d5d-152">Hata ayıklama oturumları toobe hello telemetrisinden hello hello telemetriyi ile Merhaba yayımlanan uygulamanın Application Insights portalından karma istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-152">You don't want hello telemetry from your debugging sessions toobe mixed up with hello telemetry on hello Application Insights portal from hello published app.</span></span>

<span data-ttu-id="a8d5d-153">Bazı varsa de kullanışlıdır [özel telemetri](app-insights-api-custom-events-metrics.md) telemetri toohello portal göndermeden önce toodebug istiyor.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-153">It's also useful if you have some [custom telemetry](app-insights-api-custom-events-metrics.md) that you want toodebug before sending telemetry toohello portal.</span></span>

* <span data-ttu-id="a8d5d-154">*İlk başta, t tam olarak Application Insights toosend telemetri toohello portal yapılandırılmamış. Ancak şimdi toosee hello telemetriyi yalnızca Visual Studio'da istersiniz.*</span><span class="sxs-lookup"><span data-stu-id="a8d5d-154">*At first, I fully configured Application Insights toosend telemetry toohello portal. But now I'd like toosee hello telemetry only in Visual Studio.*</span></span>
  
  * <span data-ttu-id="a8d5d-155">Merhaba arama penceresinin Ayarlar bölümünde var. bir seçenek toosearch yerel tanılama uygulamanızı telemetri toohello portal gönderse bile</span><span class="sxs-lookup"><span data-stu-id="a8d5d-155">In hello Search window's Settings, there's an option toosearch local diagnostics even if your app sends telemetry toohello portal.</span></span>
  * <span data-ttu-id="a8d5d-156">toohello portalı, açıklama hello satırı çıkışı gönderilen toostop telemetri `<instrumentationkey>...` applicationınsights.Config'de. Hazır toosend telemetri toohello portal yeniden olduğunuzda açıklamayı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-156">toostop telemetry being sent toohello portal, comment out hello line `<instrumentationkey>...` from ApplicationInsights.config. When you're ready toosend telemetry toohello portal again, uncomment it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a8d5d-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8d5d-157">Next steps</span></span>
|  |  |
| --- | --- |
| <span data-ttu-id="a8d5d-158">**[Daha fazla veri ekleme](app-insights-asp-net-more.md)**</span><span class="sxs-lookup"><span data-stu-id="a8d5d-158">**[Add more data](app-insights-asp-net-more.md)**</span></span><br/><span data-ttu-id="a8d5d-159">Kullanımı, kullanılabilirliği, bağımlılıkları, özel durumları izleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-159">Monitor usage, availability, dependencies, exceptions.</span></span> <span data-ttu-id="a8d5d-160">Günlük altyapılarından izlemeleri tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-160">Integrate traces from logging frameworks.</span></span> <span data-ttu-id="a8d5d-161">Özel telemetri yazın.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-161">Write custom telemetry.</span></span> |![Visual studio](./media/app-insights-visual-studio/64.png) |
| <span data-ttu-id="a8d5d-163">**[Merhaba Application Insights portalıyla çalışma](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="a8d5d-163">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/><span data-ttu-id="a8d5d-164">Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulama ve dışarı aktarılan telemetri verileri Canlı bağımlılık Haritası görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="a8d5d-164">View dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and exported telemetry data.</span></span> |![Visual studio](./media/app-insights-visual-studio/62.png) |

