---
title: "ASP.NET Core için Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: d86495eea467977f6c079de72e2b49a2a1da2b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="6be67-103">ASP.NET Core için Application Insights</span><span class="sxs-lookup"><span data-stu-id="6be67-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="6be67-104">[Application Insights](app-insights-overview.md) , web uygulamanızın kullanılabilirlik, performans ve kullanım izlemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="6be67-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="6be67-105">Uygulamanızın gerçek hayattaki performansı ve etkinliğine ilişkin aldığınız geri bildirimlerden yararlanarak her geliştirme yaşam döngüsünde tasarımın yönü konusunda bilinçli kararlar alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6be67-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![Örnek](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="6be67-107">Bir aboneliğe gerekir [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="6be67-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="6be67-108">Windows, XBox Live veya diğer Microsoft bulut hizmetlerinde kullanıyor olabileceğiniz bir Microsoft hesabıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6be67-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="6be67-109">Takımınızın kurumsal bir Azure aboneliğine sahip olabilir: sahibinden Microsoft hesabınızı kullanarak eklemeli isteyin.</span><span class="sxs-lookup"><span data-stu-id="6be67-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6be67-110">Başlarken</span><span class="sxs-lookup"><span data-stu-id="6be67-110">Getting started</span></span>

* <span data-ttu-id="6be67-111">Visual Studio Çözüm Gezgini'nde, projenize sağ tıklayın ve seçin **yapılandırma Application Insights**, veya **Ekle > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="6be67-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="6be67-112">[Daha fazla bilgi edinin](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="6be67-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="6be67-113">Bu menü komutlarını görmüyorsanız izleyin [alma Başlarken Kılavuzu](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="6be67-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="6be67-114">Projeniz Visual Studio sürümü ile 2017 önce oluşturulduysa, bunu yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6be67-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="6be67-115">Application Insights’ı Kullanma</span><span class="sxs-lookup"><span data-stu-id="6be67-115">Using Application Insights</span></span>
<span data-ttu-id="6be67-116">Oturum [Microsoft Azure portal](https://portal.azure.com)seçin **tüm kaynakları** veya **Application Insights**ve ardından oluşturduğunuz uygulamanızı izlemek için kaynak seçin.</span><span class="sxs-lookup"><span data-stu-id="6be67-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="6be67-117">Ayrı bir tarayıcı penceresinde uygulamanızı biraz kullanın.</span><span class="sxs-lookup"><span data-stu-id="6be67-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="6be67-118">Application Insights grafikte görüntülenen verileri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6be67-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="6be67-119">(Yenile'yi tıklatın gerekebilir.) Geliştirme yapıyorsanız sırasında yalnızca küçük miktarda veri olacaktır, ancak uygulamanızı yayınlama ve çok sayıda kullanıcı varsa bu grafikler gerçekten Canlı gelir.</span><span class="sxs-lookup"><span data-stu-id="6be67-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="6be67-120">Genel bakış sayfasında anahtar performans grafiklerini gösterir: sunucu yanıt süresi, sayfa yükleme süresi ve başarısız isteklerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="6be67-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="6be67-121">Daha fazla grafikler ve veri görmek için herhangi bir grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6be67-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="6be67-122">Portal görünümlerde üç ana kategoriye ayrılır:</span><span class="sxs-lookup"><span data-stu-id="6be67-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="6be67-123">[Ölçüm Gezgini](app-insights-metrics-explorer.md) grafikleri ve ölçümleri ve yanıt sürelerini, başarısızlık oranları veya kendiniz ile oluşturduğunuz ölçümleri gibi sayıları tabloları gösterir [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="6be67-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="6be67-124">Verileri daha iyi uygulamanızı ve kullanıcılarına anlamak almak için özellik değerlerine göre segmentlere ayırmak ve filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6be67-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="6be67-125">[Arama Gezgini](app-insights-diagnostic-search.md) belirli istekleri, özel durumlar, günlük izlemelerini veya kendiniz ile oluşturulan olaylar gibi olayları tek tek listeler [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="6be67-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="6be67-126">Filtre ve olayları arayın ve sorunları araştırmak için ilgili olaylar arasında gidin.</span><span class="sxs-lookup"><span data-stu-id="6be67-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="6be67-127">[Analytics](app-insights-analytics.md) siz telemetrinize SQL benzeri sorguları çalıştırmak sağlar ve güçlü bir Analitik ve tanı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="6be67-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="6be67-128">Uyarılar</span><span class="sxs-lookup"><span data-stu-id="6be67-128">Alerts</span></span>
* <span data-ttu-id="6be67-129">Otomatik olarak Al [öngörülü tanılama uyarıları](app-insights-proactive-diagnostics.md) , belirtilir başarısızlık oranları ve diğer ölçümleri anormal değişiklikler hakkında.</span><span class="sxs-lookup"><span data-stu-id="6be67-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="6be67-130">Ayarlanan [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) sürekli konumlardan dünya çapında Web sitenizi test ve herhangi bir test başarısız olarak e-postaları almak için.</span><span class="sxs-lookup"><span data-stu-id="6be67-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="6be67-131">Ayarlanan [ölçüm uyarıları](app-insights-monitor-web-app-availability.md) ölçümleri yanıt sürelerini veya özel durum oranları gibi dış kabul edilebilir sınırlar Git olmadığını bilmek.</span><span class="sxs-lookup"><span data-stu-id="6be67-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="6be67-132">Video</span><span class="sxs-lookup"><span data-stu-id="6be67-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="6be67-133">Açık kaynak</span><span class="sxs-lookup"><span data-stu-id="6be67-133">Open source</span></span>
[<span data-ttu-id="6be67-134">Okuma ve koda katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="6be67-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="6be67-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6be67-135">Next steps</span></span>
* <span data-ttu-id="6be67-136">[Web sayfalarınıza telemetri ekleyin](app-insights-javascript.md) sayfa kullanımını izleme ve performans.</span><span class="sxs-lookup"><span data-stu-id="6be67-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="6be67-137">[İzleme bağımlılıkları](app-insights-asp-net-dependencies.md) REST, SQL veya diğer dış kaynaklara, yavaşlamadan olmadığını görmek için.</span><span class="sxs-lookup"><span data-stu-id="6be67-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="6be67-138">[API kullanan](app-insights-api-custom-events-metrics.md) kendi olayları ve ölçümleri, uygulamanızın performansı ve kullanımı daha ayrıntılı bir görünüm için gönderilecek.</span><span class="sxs-lookup"><span data-stu-id="6be67-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="6be67-139">[Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) uygulamanızdan sürekli dünyanın denetleyin.</span><span class="sxs-lookup"><span data-stu-id="6be67-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 

