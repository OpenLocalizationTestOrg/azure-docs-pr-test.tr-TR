---
title: "Azure Application Insights algılama akıllı | Microsoft Docs"
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
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="d8495-103">Application ınsights'ta akıllı algılama</span><span class="sxs-lookup"><span data-stu-id="d8495-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="d8495-104">Akıllı algılama, web uygulamanızın olası performans sorunları otomatik olarak sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="d8495-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="d8495-105">Uygulamanızı gönderdiği telemetriyi öngörülü analizini gerçekleştirir [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8495-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="d8495-106">Başarısızlık oranları ani bir artışa veya istemci veya sunucu performans anormal desenlerini ise bir uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d8495-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="d8495-107">Bu özellik, herhangi bir yapılandırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8495-107">This feature needs no configuration.</span></span> <span data-ttu-id="d8495-108">Uygulamanız yeterli telemetri gönderirse çalışır.</span><span class="sxs-lookup"><span data-stu-id="d8495-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="d8495-109">Akıllı algılama uyarıları hem aldığınız e-postalar ve akıllı algılama dikey penceresinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8495-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="d8495-110">Akıllı algılamaların gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="d8495-110">Review your Smart Detections</span></span>
<span data-ttu-id="d8495-111">İki yolla algılamaların bulabilir:</span><span class="sxs-lookup"><span data-stu-id="d8495-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="d8495-112">**Bir e-posta aldığınız** Application Insights gelen.</span><span class="sxs-lookup"><span data-stu-id="d8495-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="d8495-113">Aşağıda, genel bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d8495-113">Here's a typical example:</span></span>
  
    ![E-posta uyarısı](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="d8495-115">Daha fazla ayrıntı Portalı'nda açmak için büyük düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d8495-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="d8495-116">**Akıllı algılama döşeme** uygulamanızın bir genel bakış dikey son uyarıların sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8495-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="d8495-117">Son uyarıları listesini görmek için kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8495-117">Click the tile to see a list of recent alerts.</span></span>

![Görünümü en son algılama](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="d8495-119">Ayrıntılarını görmek için bir uyarı seçin.</span><span class="sxs-lookup"><span data-stu-id="d8495-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="d8495-120">Hangi sorunlar algılandığında?</span><span class="sxs-lookup"><span data-stu-id="d8495-120">What problems are detected?</span></span>
<span data-ttu-id="d8495-121">Algılama üç tür vardır:</span><span class="sxs-lookup"><span data-stu-id="d8495-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="d8495-122">[Algılama - hatası anormallikleri akıllı](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d8495-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="d8495-123">Yük ve diğer etkenlere bağlı ile ilişkilendirerek machine learning, uygulamanız için başarısız istekleri beklenen oranını ayarlamak kullanırız.</span><span class="sxs-lookup"><span data-stu-id="d8495-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="d8495-124">Hata oranı beklenen zarfının dışında kalırsa, size bir uyarı göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="d8495-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="d8495-125">[Algılama - performans Anormalliklerini akıllı](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d8495-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="d8495-126">Yanıt süresi bir işlem veya bağımlılık süresi geçmiş taban çizgisine göre yavaşlamadan veya yanıt süresi veya sayfa yükleme süresi anormal bir desen tanımlamak bildirimler alın.</span><span class="sxs-lookup"><span data-stu-id="d8495-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="d8495-127">[Akıllı algılama - Azure bulut hizmeti sorunları](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="d8495-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="d8495-128">Uygulamanızı Azure bulut Hizmetleri'nde barındırılan ve rol örneği başlatma hataları, sık sık geri dönüştürülüyor veya çalışma zamanı çökme (Crash) varsa, uyarılar alırsınız.</span><span class="sxs-lookup"><span data-stu-id="d8495-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="d8495-129">(Her bir bildirim Yardım bağlantıları ilgili makaleler için atmanız.)</span><span class="sxs-lookup"><span data-stu-id="d8495-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="d8495-130">Video</span><span class="sxs-lookup"><span data-stu-id="d8495-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="d8495-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8495-131">Next steps</span></span>
<span data-ttu-id="d8495-132">Bu tanılama araçları, uygulamanızdan alınan telemetri incelemek yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="d8495-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="d8495-133">Ölçüm Gezgini</span><span class="sxs-lookup"><span data-stu-id="d8495-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="d8495-134">Arama Gezgini</span><span class="sxs-lookup"><span data-stu-id="d8495-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="d8495-135">Analizi - güçlü sorgu dili</span><span class="sxs-lookup"><span data-stu-id="d8495-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="d8495-136">Akıllı algılama tamamen otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="d8495-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="d8495-137">Ancak, belki de daha fazla bazı uyarıları ayarlamak ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="d8495-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="d8495-138">El ile yapılandırılmış ölçüm uyarıları</span><span class="sxs-lookup"><span data-stu-id="d8495-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="d8495-139">Kullanılabilirlik web testleri</span><span class="sxs-lookup"><span data-stu-id="d8495-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

