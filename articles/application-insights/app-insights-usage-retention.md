---
title: "Azure Application Insights ile web uygulamaları için kullanıcı bekletme analizi | Microsoft docs"
description: "Kaç kullanıcının uygulamanıza dönüş?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="be368-103">Application Insights ile web uygulamaları için kullanıcı bekletme çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="be368-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="be368-104">Bekletme özelliği [Azure Application Insights](app-insights-overview.md) , analiz, uygulamanızın nasıl sayıda kullanıcının döneceğini ve ne sıklıkta belirli görevleri veya hedeflerinize ulaşmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="be368-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="be368-105">Örneğin, bir oyun sitesi çalıştırırsanız, kimin kazanan sonra iade numarayla oyun kaybettikten sonra siteye geri dönün kullanıcılar sayıda karşılaştırın.</span><span class="sxs-lookup"><span data-stu-id="be368-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="be368-106">Bu bilgi, kullanıcı deneyiminizi ve iş stratejinizi geliştirmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="be368-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="be368-107">başlarken</span><span class="sxs-lookup"><span data-stu-id="be368-107">Get started</span></span>

<span data-ttu-id="be368-108">Veri saklama aracında Application Insights portalında henüz görmüyorsanız, [kullanım araçları ile çalışmaya başlama öğrenin](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be368-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="be368-109">Bekletme aracı</span><span class="sxs-lookup"><span data-stu-id="be368-109">The Retention tool</span></span>

![Elde tutma aracı](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="be368-111">Araç, yeni bekletme raporları oluşturmak, varolan bekletme raporları açmak, geçerli bekletme raporu kaydedin veya kaydedilmiş raporları yapılan değişiklikleri geri, rapor veri yenileme, e-posta veya doğrudan bağlantı raporu paylaşmak ve belgelerine erişmek olarak kaydetmek kullanıcılara Sayfa.</span><span class="sxs-lookup"><span data-stu-id="be368-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="be368-112">Varsayılan olarak, bekletme herhangi bir şey mi tüm kullanıcılar daha sonra geri geldiği ve belirli bir süre boyunca başka bir şey mi gösterir.</span><span class="sxs-lookup"><span data-stu-id="be368-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="be368-113">Belirli kullanıcı etkinlikleri odaklanmak daraltmak için olayları farklı bileşimini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be368-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="be368-114">Bir veya daha fazla filtre özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="be368-114">Add one or more filters on properties.</span></span> <span data-ttu-id="be368-115">Örneğin, belirli bir ülke veya bölgedeki kullanıcılar üzerinde odaklanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be368-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="be368-116">Tıklatın **güncelleştirme** filtreleri ayarladıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="be368-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="be368-117">Genel saklama grafik seçili süre kullanıcı bekletme özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="be368-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="be368-118">Izgara Sorgu Oluşturucu #2'göre tutulur kullanıcı sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="be368-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="be368-119">Her satır, dönem gösterilen zaman içinde herhangi bir olay gerçekleştiren bir kohort kullanıcıların temsil eder.</span><span class="sxs-lookup"><span data-stu-id="be368-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="be368-120">Sıradaki her hücre en az bir kez daha sonraki bir süre içinde bu kohort kaç döndürülen gösterir.</span><span class="sxs-lookup"><span data-stu-id="be368-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="be368-121">Bazı kullanıcılar, birden fazla dönemde döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="be368-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="be368-122">Öngörüler kartları üst beş başlatma olaylarını ve daha iyi anlamak kendi saklama rapor kullanıcılara vermek için üst beş döndürülen olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="be368-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Bekletme fare vurgulu](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="be368-124">Kullanıcı hücrenin ne anlama geldiğini açıklayan analytics düğmesi ve araç ipuçları erişmek için bekletme aracı hücreleri üzerine getirin.</span><span class="sxs-lookup"><span data-stu-id="be368-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="be368-125">Analytics düğmesi hücreden kullanıcı oluşturmak için önceden girilmiş bir sorgu Analytics aracıyla kullanıcılara alır.</span><span class="sxs-lookup"><span data-stu-id="be368-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="be368-126">Bekletme izlemek için iş olaylarını kullanın</span><span class="sxs-lookup"><span data-stu-id="be368-126">Use business events to track retention</span></span>

<span data-ttu-id="be368-127">En kullanışlı bekletme analiz almak için önemli iş faaliyetlerine temsil olayları ölçün.</span><span class="sxs-lookup"><span data-stu-id="be368-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="be368-128">Örneğin, çok sayıda kullanıcı görüntülediği oyuna olmadan bir sayfa uygulamanızda açılabilir.</span><span class="sxs-lookup"><span data-stu-id="be368-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="be368-129">Yalnızca sayfa görünümleri izleme yanlış tahminidir kaç kişinin önceden keyfini sonra oyun dönün, bu nedenle sağlar.</span><span class="sxs-lookup"><span data-stu-id="be368-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="be368-130">Oynatıcıları döndürme NET bir resim almak için uygulamanızı bir kullanıcı gerçekte yürütürken özel bir olay göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="be368-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="be368-131">Anahtar iş eylemlerini temsil eden özel olaylar kod ve bunlar bekletme çözümleme için kullanmak için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="be368-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="be368-132">Oyun sonucu yakalamak için özel bir olay Application Insights'a gönderme kod satırı yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="be368-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="be368-133">Web sayfası koduna veya Node.JS yazma, şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="be368-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="be368-134">ASP.NET sunucusu kod:</span><span class="sxs-lookup"><span data-stu-id="be368-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="be368-135">[Özel olaylar yazma hakkında daha fazla bilgi](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="be368-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="be368-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be368-136">Next steps</span></span>
- <span data-ttu-id="be368-137">Kullanımı deneyimleri etkinleştirmek için göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="be368-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="be368-138">Özel olaylar veya sayfa görünümleri zaten gönderirseniz, kullanıcıların hizmetinizin kullanımını öğrenmek için kullanım araçları keşfedin.</span><span class="sxs-lookup"><span data-stu-id="be368-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="be368-139">Kullanıcılar, Oturumlar, Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="be368-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="be368-140">Huniler</span><span class="sxs-lookup"><span data-stu-id="be368-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="be368-141">Kullanıcı Akışları</span><span class="sxs-lookup"><span data-stu-id="be368-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="be368-142">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="be368-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="be368-143">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="be368-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


