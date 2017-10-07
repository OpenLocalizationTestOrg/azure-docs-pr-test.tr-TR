---
title: "Azure Application Insights ile web uygulamaları için aaaUser bekletme analizi | Microsoft docs"
description: "Kaç kullanıcının tooyour uygulamaya dönün?"
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="66c75-103">Application Insights ile web uygulamaları için kullanıcı bekletme çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="66c75-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="66c75-104">Merhaba bekletme özelliği [Azure Application Insights](app-insights-overview.md) kaç kullanıcı analiz yardımcı dönmek tooyour uygulama ve ne sıklıkta belirli görevleri veya hedeflerinize ulaşmak.</span><span class="sxs-lookup"><span data-stu-id="66c75-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="66c75-105">Örneğin, bir oyun sitesi çalıştırırsanız, kimin kazanan sonra iade toohello site hello numarasıyla oyun kaybettikten sonra iade kullanıcıların hello sayıları karşılaştırma.</span><span class="sxs-lookup"><span data-stu-id="66c75-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="66c75-106">Bu bilgi, kullanıcı deneyiminizi ve iş stratejinizi geliştirmenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="66c75-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="66c75-107">başlarken</span><span class="sxs-lookup"><span data-stu-id="66c75-107">Get started</span></span>

<span data-ttu-id="66c75-108">Merhaba Application Insights portalında hello bekletme aracında veri henüz görmüyorsanız, [tooget hello kullanım araçları ile çalışmaya nasıl bilgi](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66c75-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="66c75-109">Merhaba bekletme aracı</span><span class="sxs-lookup"><span data-stu-id="66c75-109">hello Retention tool</span></span>

![Elde tutma aracı](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="66c75-111">Hello araç toocreate yeni bekletme Raporlar kullanıcılara, varolan bekletme raporları açın, geçerli bekletme raporu kaydedin veya farklı kaydet, yapılan değişiklikleri toosaved raporları geri, hello raporu, e-posta veya doğrudan bağlantı ve erişim hello aracılığıyla paylaşımı rapor verileri Yenile belgeler sayfası.</span><span class="sxs-lookup"><span data-stu-id="66c75-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="66c75-112">Varsayılan olarak, bekletme herhangi bir şey mi tüm kullanıcılar daha sonra geri geldiği ve belirli bir süre boyunca başka bir şey mi gösterir.</span><span class="sxs-lookup"><span data-stu-id="66c75-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="66c75-113">Olayları toonarrow hello belirli kullanıcı etkinlikleri odaklanmak farklı bileşimini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c75-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="66c75-114">Bir veya daha fazla filtre özellikleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="66c75-114">Add one or more filters on properties.</span></span> <span data-ttu-id="66c75-115">Örneğin, belirli bir ülke veya bölgedeki kullanıcılar üzerinde odaklanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c75-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="66c75-116">Tıklatın **güncelleştirme** hello filtreleri ayarladıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="66c75-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="66c75-117">Merhaba genel saklama grafik kullanıcı bekletme özetini süre seçili hello arasında gösterir.</span><span class="sxs-lookup"><span data-stu-id="66c75-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="66c75-118">Merhaba kılavuz according toohello Sorgu Oluşturucu #2'hello sayısı, kullanıcı korunur gösterir.</span><span class="sxs-lookup"><span data-stu-id="66c75-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="66c75-119">Her satır, dönem gösterilen hello zaman içinde herhangi bir olay gerçekleştiren bir kohort kullanıcıların temsil eder.</span><span class="sxs-lookup"><span data-stu-id="66c75-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="66c75-120">Merhaba satırdaki her hücre en az bir kez daha sonraki bir süre içinde bu kohort kaç döndürülen gösterir.</span><span class="sxs-lookup"><span data-stu-id="66c75-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="66c75-121">Bazı kullanıcılar, birden fazla dönemde döndürebilir.</span><span class="sxs-lookup"><span data-stu-id="66c75-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="66c75-122">Merhaba Öngörüler kartları üst beş başlatma olaylarını göstermek ve daha iyi anlamak kendi saklama raporun üst beş olayları toogive kullanıcı döndürdü.</span><span class="sxs-lookup"><span data-stu-id="66c75-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Bekletme fare vurgulu](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="66c75-124">Kullanıcıların hücreleri hello bekletme aracı tooaccess hello analytics düğmesine üzerine getirin ve hangi hello hücre açıklayan araç ipuçları anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="66c75-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="66c75-125">Merhaba Analytics düğmesi kullanıcılar toohello analiz aracı önceden doldurulmuş haldedir sorgu toogenerate kullanıcılarla hello hücreden alır.</span><span class="sxs-lookup"><span data-stu-id="66c75-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="66c75-126">İş olayları tootrack bekletme kullanın</span><span class="sxs-lookup"><span data-stu-id="66c75-126">Use business events tootrack retention</span></span>

<span data-ttu-id="66c75-127">tooget hello en yararlı bekletme analiz, önemli iş faaliyetlerine temsil eden ölçü olaylar.</span><span class="sxs-lookup"><span data-stu-id="66c75-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="66c75-128">Örneğin, çok sayıda kullanıcı görüntülediği hello oyuna olmadan bir sayfa uygulamanızda açılabilir.</span><span class="sxs-lookup"><span data-stu-id="66c75-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="66c75-129">Yalnızca hello sayfa görünümleri izleme yanlış tahminidir kaç kişinin, daha önce keyfini sonra hello oyun tooplay dönün, bu nedenle sağlar.</span><span class="sxs-lookup"><span data-stu-id="66c75-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="66c75-130">tooget oynatıcıları döndürme NET bir resim, uygulamanızı bir kullanıcı gerçekte yürütürken özel bir olay göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="66c75-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="66c75-131">Bu anahtar iş eylemleri temsil eder ve bu bekletme çözümleme için kullanmak iyi bir uygulama toocode özel olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="66c75-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="66c75-132">toocapture hello oyun sonucu, toowrite kod toosend özel olay tooApplication Öngörüler kolu gerekir.</span><span class="sxs-lookup"><span data-stu-id="66c75-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="66c75-133">Merhaba web sayfası koduna veya Node.JS yazma, şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="66c75-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="66c75-134">ASP.NET sunucusu kod:</span><span class="sxs-lookup"><span data-stu-id="66c75-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="66c75-135">[Özel olaylar yazma hakkında daha fazla bilgi](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="66c75-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="66c75-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66c75-136">Next steps</span></span>
- <span data-ttu-id="66c75-137">tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="66c75-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="66c75-138">Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.</span><span class="sxs-lookup"><span data-stu-id="66c75-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="66c75-139">Kullanıcılar, Oturumlar, Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="66c75-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="66c75-140">Huniler</span><span class="sxs-lookup"><span data-stu-id="66c75-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="66c75-141">Kullanıcı Akışları</span><span class="sxs-lookup"><span data-stu-id="66c75-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="66c75-142">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="66c75-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="66c75-143">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="66c75-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


