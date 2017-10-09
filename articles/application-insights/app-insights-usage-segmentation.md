---
title: Azure Application Insights aaaUser, oturum ve olay analizi | Microsoft docs
description: "Kullanıcılar, web uygulamanızın demografik analizini."
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="5cd0d-103">Application Insights kullanıcıları, oturumlar ve olayları çözümleme</span><span class="sxs-lookup"><span data-stu-id="5cd0d-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="5cd0d-104">Kişilerin web uygulamanızı kullandığınızda, bunlar en, kullanıcılarınızın bulunduğu ilgileniyor hangi sayfaların, hangi tarayıcılar ve işletim sistemleri bunlar kullandığını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="5cd0d-105">İş ve kullanım telemetrisi kullanarak çözümlemek [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cd0d-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="5cd0d-106">başlarken</span><span class="sxs-lookup"><span data-stu-id="5cd0d-106">Get started</span></span>

<span data-ttu-id="5cd0d-107">Merhaba kullanıcıları, oturumları veya olayları Kanatlar hello Application Insights portalında verileri henüz görmüyorsanız, [tooget hello kullanım araçları ile çalışmaya nasıl bilgi](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cd0d-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="5cd0d-108">Merhaba kullanıcıları, oturumlar ve Olayları kesimleme aracı</span><span class="sxs-lookup"><span data-stu-id="5cd0d-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="5cd0d-109">Üç perspektiflerden web uygulamanızdan aynı aracı tooslice ve bölmek telemetrinin hello üç hello kullanım Kanatlar kullanın.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="5cd0d-110">Filtreleme ve hello veri bölme hello göreli ve kullanımı için farklı sayfalar özellikleri hakkında Öngörüler açığa.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="5cd0d-111">**Kullanıcılar aracını**: kaç kişinin uygulamanızı ve özelliklerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="5cd0d-112">Kullanıcıların, tarayıcı tanımlama bilgilerinde depolanan anonim kimlikleri kullanılarak sayılır.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="5cd0d-113">Farklı tarayıcılar ya da makineleri kullanan tek bir kişi olarak birden fazla kullanıcı sayılacaktır.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="5cd0d-114">**Oturumlar aracını**: kullanıcı etkinliği kaç oturumları belirli sayfalarını ve özelliklerini, uygulamanızın eklediniz.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="5cd0d-115">Bir oturum kullanım sürekli 24 h veya kullanıcı yapılmadıktan yarım saat sonra sayılır.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="5cd0d-116">**Olayları aracı**: belirli sayfalarını ve özelliklerini, uygulamanızın ne sıklıkta kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="5cd0d-117">Sahip olduğunuz sağlanan sayfa görünümü bir tarayıcı, uygulamanızdan bir sayfa yüklediğinde sayılır [onu izlenmiş](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="5cd0d-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="5cd0d-118">Özel bir olay şeyin uygulamanızda bir düğmeyi tıklatın veya bazı görev tamamlanmasından hello gibi genellikle bir kullanıcı etkileşimi bir oluşumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="5cd0d-119">Kodu, uygulamanızda çok eklediğiniz[özel olayları](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="5cd0d-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Kullanım aracı](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="5cd0d-121">Belirli kullanıcıların sorgulama</span><span class="sxs-lookup"><span data-stu-id="5cd0d-121">Querying for Certain Users</span></span> 

<span data-ttu-id="5cd0d-122">Farklı kullanıcı grupları hello kullanıcılar aracını hello üstündeki hello sorgu seçeneklerini ayarlayarak keşfedin:</span><span class="sxs-lookup"><span data-stu-id="5cd0d-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="5cd0d-123">Kim: özel olaylar seçin ve sayfa görünümleri.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="5cd0d-124">İşlem sırasında: bir zaman aralığı seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="5cd0d-125">: Tarafından nasıl toobucket hello verileri, bir süre veya tarayıcı veya şehir gibi başka bir özellik seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="5cd0d-126">Bölme: bir özellik tarafından toosplit veya segment hello veri seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="5cd0d-127">Filtreler ekleyin: hello sorgusu toocertain kullanıcıları, oturumları veya olayları, tarayıcı veya şehir gibi özelliklerine göre sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="5cd0d-128">Kaydetme ve raporları paylaşma</span><span class="sxs-lookup"><span data-stu-id="5cd0d-128">Saving and sharing reports</span></span> 
<span data-ttu-id="5cd0d-129">Kullanıcıların raporları, hello raporlarım bölümünde, özel ya da yalnızca tooyou kaydedebilir veya erişim toothis Application Insights kaynağı başka herkesle hello paylaşılan raporları bölümüne paylaşılan.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="5cd0d-130">Raporu kaydetme veya özelliklerini düzenlerken, bazı sabit süreyi geri dönerseniz verilerin, bir rapor sürekli olacak "Geçerli göreli zaman aralığı" toosave yenilenmesi seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="5cd0d-131">"Geçerli mutlak zaman aralığı" toosave sabit bir veri kümesiyle bir rapor seçin.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="5cd0d-132">Application Insights verileri yalnızca 90 90 günden itibaren mutlak zaman aralığı olan bir raporu geçmişse kaydedildiği şekilde gün süreyle depolanır unutmayın, hello rapor boş görünür.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="5cd0d-133">Örnek örnekleri</span><span class="sxs-lookup"><span data-stu-id="5cd0d-133">Example instances</span></span>

<span data-ttu-id="5cd0d-134">Merhaba örnek örnekleri bölümüne sayıda bireysel kullanıcıları, oturumları veya hello geçerli sorgu tarafından eşleşen olaylar hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="5cd0d-135">Dikkate ve toplama tooaggregates içinde kişiler hello davranışlarını keşfetme kişiler gerçekten uygulamanızı kullanma hakkında bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="5cd0d-136">Insights</span><span class="sxs-lookup"><span data-stu-id="5cd0d-136">Insights</span></span> 

<span data-ttu-id="5cd0d-137">Merhaba Öngörüler kenar ortak özellikleri paylaşır kullanıcılar büyük kümelerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="5cd0d-138">Bu kümeleri kişiler uygulamanızı kullanma şaşırtıcı eğilimleri ortaya çıkarmaya.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="5cd0d-139">Örneğin, tüm, uygulamanızın hello kullanımı % 40 tek bir özelliğini kullanarak kişilerden geliyorsa.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="5cd0d-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cd0d-140">Next steps</span></span>
- <span data-ttu-id="5cd0d-141">tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="5cd0d-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="5cd0d-142">Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.</span><span class="sxs-lookup"><span data-stu-id="5cd0d-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="5cd0d-143">Huniler</span><span class="sxs-lookup"><span data-stu-id="5cd0d-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="5cd0d-144">Bekletme</span><span class="sxs-lookup"><span data-stu-id="5cd0d-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="5cd0d-145">Kullanıcı Akışları</span><span class="sxs-lookup"><span data-stu-id="5cd0d-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="5cd0d-146">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="5cd0d-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="5cd0d-147">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="5cd0d-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

