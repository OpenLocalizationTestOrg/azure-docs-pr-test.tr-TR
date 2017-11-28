---
title: "Azure Application Insights algılama aaaSmart | Microsoft Docs"
description: "Application Insights uygulama telemetrinin otomatik derin çözümleme yapar ve olası sorunları sizi uyarır."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="1dc09-103">Application ınsights'ta akıllı algılama</span><span class="sxs-lookup"><span data-stu-id="1dc09-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="1dc09-104">Akıllı algılama, web uygulamanızın olası performans sorunları otomatik olarak sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="1dc09-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="1dc09-105">Uygulamanız çok gönderir hello telemetri öngörülü çözümlemesi gerçekleştirir[Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1dc09-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1dc09-106">Başarısızlık oranları ani bir artışa veya istemci veya sunucu performans anormal desenlerini ise bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1dc09-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="1dc09-107">Bu özellik, herhangi bir yapılandırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="1dc09-107">This feature needs no configuration.</span></span> <span data-ttu-id="1dc09-108">Uygulamanız yeterli telemetri gönderirse çalışır.</span><span class="sxs-lookup"><span data-stu-id="1dc09-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="1dc09-109">Akıllı algılama uyarıları hem aldığınız hello e-postalar ve hello akıllı algılama dikey penceresinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1dc09-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="1dc09-110">Akıllı algılamaların gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="1dc09-110">Review your Smart Detections</span></span>
<span data-ttu-id="1dc09-111">İki yolla algılamaların bulabilir:</span><span class="sxs-lookup"><span data-stu-id="1dc09-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="1dc09-112">**Bir e-posta aldığınız** Application Insights gelen.</span><span class="sxs-lookup"><span data-stu-id="1dc09-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="1dc09-113">Aşağıda, genel bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1dc09-113">Here's a typical example:</span></span>
  
    ![E-posta uyarısı](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="1dc09-115">Merhaba büyük düğme tooopen daha ayrıntılı olarak hello portal'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1dc09-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="1dc09-116">**Merhaba akıllı algılama döşeme** uygulamanızın bir genel bakış dikey son uyarıların sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1dc09-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="1dc09-117">Merhaba döşeme toosee son uyarıların bir listesi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1dc09-117">Click hello tile toosee a list of recent alerts.</span></span>

![Görünümü en son algılama](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="1dc09-119">Bir uyarı toosee ayrıntılarını seçin.</span><span class="sxs-lookup"><span data-stu-id="1dc09-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="1dc09-120">Hangi sorunlar algılandığında?</span><span class="sxs-lookup"><span data-stu-id="1dc09-120">What problems are detected?</span></span>
<span data-ttu-id="1dc09-121">Algılama üç tür vardır:</span><span class="sxs-lookup"><span data-stu-id="1dc09-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="1dc09-122">[Algılama - hatası anormallikleri akıllı](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1dc09-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="1dc09-123">Machine learning kullanırız yük ve diğer etkenlere bağlı ile ilişkilendirerek, uygulamanız için başarısız isteklerin tooset beklenen hello oranı.</span><span class="sxs-lookup"><span data-stu-id="1dc09-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="1dc09-124">Merhaba hata oranı hello beklenen zarfının dışında kalırsa, size bir uyarı göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="1dc09-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="1dc09-125">[Algılama - performans Anormalliklerini akıllı](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="1dc09-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="1dc09-126">Yanıt süresi bir işlem veya bağımlılık sürenin karşılaştırılan toohistorical temel yavaşlamasını veya yanıt süresi veya sayfa yükleme süresi anormal bir desen tanımlamak bildirimler alın.</span><span class="sxs-lookup"><span data-stu-id="1dc09-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="1dc09-127">[Akıllı algılama - Azure bulut hizmeti sorunları](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="1dc09-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="1dc09-128">Uygulamanızı Azure bulut Hizmetleri'nde barındırılan ve rol örneği başlatma hataları, sık sık geri dönüştürülüyor veya çalışma zamanı çökme (Crash) varsa, uyarılar alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1dc09-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="1dc09-129">(her bir bildirim hello Yardım bağlantıları toohello ilgili makaleler atmanız.)</span><span class="sxs-lookup"><span data-stu-id="1dc09-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="1dc09-130">Video</span><span class="sxs-lookup"><span data-stu-id="1dc09-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="1dc09-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1dc09-131">Next steps</span></span>
<span data-ttu-id="1dc09-132">Bu tanılama araçları hello telemetriyi uygulamanızdan incelemek yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="1dc09-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="1dc09-133">Ölçüm Gezgini</span><span class="sxs-lookup"><span data-stu-id="1dc09-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="1dc09-134">Arama Gezgini</span><span class="sxs-lookup"><span data-stu-id="1dc09-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="1dc09-135">Analizi - güçlü sorgu dili</span><span class="sxs-lookup"><span data-stu-id="1dc09-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="1dc09-136">Akıllı algılama tamamen otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="1dc09-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="1dc09-137">Ancak, belki de daha fazla bazı uyarılar tooset ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="1dc09-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="1dc09-138">El ile yapılandırılmış ölçüm uyarıları</span><span class="sxs-lookup"><span data-stu-id="1dc09-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="1dc09-139">Kullanılabilirlik web testleri</span><span class="sxs-lookup"><span data-stu-id="1dc09-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

