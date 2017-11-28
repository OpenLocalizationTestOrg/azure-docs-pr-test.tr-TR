---
title: "aaaAzure ASP.NET Core için Application Insights | Microsoft Docs"
description: "Kullanılabilirlik, performans ve kullanım için Web uygulamalarını izleyin."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="89b13-103">ASP.NET Core için Application Insights</span><span class="sxs-lookup"><span data-stu-id="89b13-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="89b13-104">[Application Insights](app-insights-overview.md) , web uygulamanızın kullanılabilirlik, performans ve kullanım izlemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="89b13-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="89b13-105">Merhaba performans ve hello uygulamanızda verimliliğini hakkında joker elde hello geri bildirim ile her geliştirme yaşam döngüsündeki hello tasarım hello yönünü hakkında bilinçli seçimler yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89b13-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Örnek](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="89b13-107">Bir aboneliğe gerekir [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="89b13-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="89b13-108">Windows, XBox Live veya diğer Microsoft bulut hizmetlerinde kullanıyor olabileceğiniz bir Microsoft hesabıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="89b13-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="89b13-109">Takımınızın Kurumsal abonelik tooAzure sahip olabilir: hello sahibi tooadd isteyin Microsoft hesabınızı kullanarak tooit.</span><span class="sxs-lookup"><span data-stu-id="89b13-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="89b13-110">Başlarken</span><span class="sxs-lookup"><span data-stu-id="89b13-110">Getting started</span></span>

* <span data-ttu-id="89b13-111">Visual Studio Çözüm Gezgini'nde, projenize sağ tıklayın ve seçin **yapılandırma Application Insights**, veya **Ekle > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="89b13-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="89b13-112">[Daha fazla bilgi edinin](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="89b13-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="89b13-113">Bu menü komutlarını görmüyorsanız hello izleyin [alma Başlarken Kılavuzu](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="89b13-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="89b13-114">Projeniz Visual Studio sürümü ile 2017 önce oluşturulduysa, bu toodo gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="89b13-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="89b13-115">Application Insights’ı Kullanma</span><span class="sxs-lookup"><span data-stu-id="89b13-115">Using Application Insights</span></span>
<span data-ttu-id="89b13-116">Merhaba içine oturum [Microsoft Azure portal](https://portal.azure.com)seçin **tüm kaynakları** veya **Application Insights**ve ardından uygulamanızı toomonitor oluşturulan hello kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="89b13-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="89b13-117">Ayrı bir tarayıcı penceresinde uygulamanızı biraz kullanın.</span><span class="sxs-lookup"><span data-stu-id="89b13-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="89b13-118">Merhaba Application Insights grafikte görüntülenen verileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="89b13-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="89b13-119">(Tooclick yenileme sahip olabilir.) Geliştirme yapıyorsanız sırasında yalnızca küçük miktarda veri olacaktır, ancak uygulamanızı yayınlama ve çok sayıda kullanıcı varsa bu grafikler gerçekten Canlı gelir.</span><span class="sxs-lookup"><span data-stu-id="89b13-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="89b13-120">Merhaba genel bakış sayfasında anahtar performans grafiklerini gösterir: sunucu yanıt süresi, sayfa yükleme süresi ve başarısız isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="89b13-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="89b13-121">Daha fazla grafikler ve veri herhangi grafik toosee tıklayın.</span><span class="sxs-lookup"><span data-stu-id="89b13-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="89b13-122">Merhaba portal görünümlerde üç ana kategoriye ayrılır:</span><span class="sxs-lookup"><span data-stu-id="89b13-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="89b13-123">[Ölçüm Gezgini](app-insights-metrics-explorer.md) oluşturduğunuz kendiniz ile Merhaba grafikleri ve ölçümleri ve yanıt sürelerini, başarısızlık oranları veya ölçümleri gibi sayıları tabloları gösterir [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="89b13-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="89b13-124">Daha iyi uygulamanızı ve kullanıcılarına anlamak özellik değerleri tooget tarafından filtre ve segment hello verileri.</span><span class="sxs-lookup"><span data-stu-id="89b13-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="89b13-125">[Arama Gezgini](app-insights-diagnostic-search.md) belirli istekleri, özel durumlar, günlük izlemelerini ya da oluşturduğunuz kendiniz hello ile olayları gibi olayları tek tek listeler [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="89b13-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="89b13-126">Filtre hello olayları aramak ve ilgili olaylar tooinvestigate sorunları arasında gidin.</span><span class="sxs-lookup"><span data-stu-id="89b13-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="89b13-127">[Analytics](app-insights-analytics.md) siz telemetrinize SQL benzeri sorguları çalıştırmak sağlar ve güçlü bir Analitik ve tanı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="89b13-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="89b13-128">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="89b13-128">Alerts</span></span>
* <span data-ttu-id="89b13-129">Otomatik olarak Al [öngörülü tanılama uyarıları](app-insights-proactive-diagnostics.md) , belirtilir başarısızlık oranları ve diğer ölçümleri anormal değişiklikler hakkında.</span><span class="sxs-lookup"><span data-stu-id="89b13-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="89b13-130">Ayarlanan [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) Web sitenizi sürekli olarak dünya çapında konumları ve get herhangi başarısız test hemen sonra e-postalar tootest.</span><span class="sxs-lookup"><span data-stu-id="89b13-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="89b13-131">Ayarlanan [ölçüm uyarıları](app-insights-monitor-web-app-availability.md) ölçümleri yanıt sürelerini veya özel durum oranları gibi dış kabul edilebilir sınırlar giderseniz tooknow.</span><span class="sxs-lookup"><span data-stu-id="89b13-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="89b13-132">Video</span><span class="sxs-lookup"><span data-stu-id="89b13-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="89b13-133">Açık kaynak</span><span class="sxs-lookup"><span data-stu-id="89b13-133">Open source</span></span>
[<span data-ttu-id="89b13-134">Okuma ve toohello kodu katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="89b13-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="89b13-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89b13-135">Next steps</span></span>
* <span data-ttu-id="89b13-136">[Telemetri tooyour web sayfaları eklemek](app-insights-javascript.md) toomonitor sayfa kullanım ve performans.</span><span class="sxs-lookup"><span data-stu-id="89b13-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="89b13-137">[İzleme bağımlılıkları](app-insights-asp-net-dependencies.md) REST, SQL veya diğer dış kaynaklara, yavaşlamadan varsa toosee.</span><span class="sxs-lookup"><span data-stu-id="89b13-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="89b13-138">[Merhaba API kullanan](app-insights-api-custom-events-metrics.md) toosend kendi olayları ve ölçümleri, uygulamanızın performansı ve kullanımı daha ayrıntılı bir görünüm için.</span><span class="sxs-lookup"><span data-stu-id="89b13-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="89b13-139">[Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) uygulamanızdan sürekli Merhaba Dünya denetleyin.</span><span class="sxs-lookup"><span data-stu-id="89b13-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

