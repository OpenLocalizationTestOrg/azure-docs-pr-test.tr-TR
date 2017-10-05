---
title: "Azure Application Insights ile web uygulamaları için kullanım analizi | Microsoft docs"
description: "Kullanıcılarınızın ve web uygulamanızı ile neler yaptığını anlayın."
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
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="081b4-103">Application Insights ile web uygulamaları için kullanım analizi</span><span class="sxs-lookup"><span data-stu-id="081b4-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="081b4-104">Web uygulamanızın hangi özellikleri en popüler var mı?</span><span class="sxs-lookup"><span data-stu-id="081b4-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="081b4-105">Kullanıcılarınızın uygulamanızla hedeflerine ulaşması?</span><span class="sxs-lookup"><span data-stu-id="081b4-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="081b4-106">Bunlar belirli zamanlarda bırakma ve döndürmeleri daha sonra?</span><span class="sxs-lookup"><span data-stu-id="081b4-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="081b4-107">[Azure Application Insights](app-insights-overview.md) , kişiler, web uygulamanızın kullanımını içine güçlü Öngörüler kazanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="081b4-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="081b4-108">Uygulamanızı güncelleştirme her zaman, kullanıcılar için ne kadar iyi çalıştığı değerlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="081b4-109">Bu bilgiyle, veri sonraki geliştirme döngüsü hakkında kararlar tabanlı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="081b4-110">Telemetriyi uygulamanızdan Gönder</span><span class="sxs-lookup"><span data-stu-id="081b4-110">Send telemetry from your app</span></span>

<span data-ttu-id="081b4-111">Uygulama sunucusu kodunuzu hem de web sayfalarınıza Application Insights yükleyerek en iyi deneyimi elde edilir.</span><span class="sxs-lookup"><span data-stu-id="081b4-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="081b4-112">İstemci ve sunucu bileşenleri, uygulamanızın telemetri geri analiz için Azure portalı gönderin.</span><span class="sxs-lookup"><span data-stu-id="081b4-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="081b4-113">**Sunucu kodu:** için uygun modülünü yükleyin, [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), veya [diğer](app-insights-platforms.md) uygulama.</span><span class="sxs-lookup"><span data-stu-id="081b4-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="081b4-114">*Sunucu kodu yüklemek istemiyor musunuz? Yalnızca [Azure Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="081b4-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="081b4-115">**Web sayfası koduna:** açmak [Azure portal](https://portal.azure.com), uygulamanız için Application Insights kaynağı açın ve ardından açın **Başlarken > İzleme ve tanılama istemci tarafı**.</span><span class="sxs-lookup"><span data-stu-id="081b4-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Komut dosyası ana web sayfanızın head kopyalayın.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="081b4-117">**Telemetri alın:** projeniz için bir kaç dakika hata ayıklama modunda çalıştırılması ve genel bakış dikey penceresinde Application Insights sonuçlarında arayın.</span><span class="sxs-lookup"><span data-stu-id="081b4-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="081b4-118">Uygulamanızın performansını izlemek ve uygulamanızla kullanıcıların ne yaptıklarını bulmak için uygulamanızı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="081b4-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="081b4-119">Kullanıcı ve oturum kimliği, telemetri dahil</span><span class="sxs-lookup"><span data-stu-id="081b4-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="081b4-120">Zaman içinde kullanıcıları izlemek için Application Insights bunları belirlemenin bir yolu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="081b4-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="081b4-121">Bir kullanıcı kimliği veya bir oturum kimliği gerektirmez yalnızca kullanım aracı olayları araçtır</span><span class="sxs-lookup"><span data-stu-id="081b4-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="081b4-122">Bu kimlikleri göndermeye Başla [burada](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="081b4-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="081b4-123">Kullanım demografisine ve istatistikleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="081b4-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="081b4-124">Kişiler uygulamanızı kullandığınızda, bunlar en, kullanıcılarınızın bulunduğu ilgileniyor hangi sayfaların, hangi tarayıcılar ve işletim sistemleri bunlar kullandığını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="081b4-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="081b4-125">Kullanıcı ve oturum raporları, veri sayfaları veya özel olaylar tarafından filtre ve bunları konumu, ortam ve sayfa gibi özelliklere göre segmentlere ayırmak.</span><span class="sxs-lookup"><span data-stu-id="081b4-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="081b4-126">Kendi filtreler de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-126">You can also add your own filters.</span></span>

![Kullanıcılar](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="081b4-128">Veri kümesi ilginç kalıpları çıkışı sağdaki Öngörüler gelin.</span><span class="sxs-lookup"><span data-stu-id="081b4-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="081b4-129">**Kullanıcılar** rapor içinde seçilen zaman dönemleriniz sayfalarınızı erişim benzersiz kullanıcı sayısı sayar.</span><span class="sxs-lookup"><span data-stu-id="081b4-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="081b4-130">(Kullanıcılar tanımlama bilgilerini kullanarak sayılır.</span><span class="sxs-lookup"><span data-stu-id="081b4-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="081b4-131">Birisi farklı tarayıcılar veya istemci makinelerle sitenize erişen veya kendi tanımlama bilgilerini temizler, ardından bunlar birden çok kez sayılacaktır.)</span><span class="sxs-lookup"><span data-stu-id="081b4-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="081b4-132">**Oturumları** raporu, sitenize erişen kullanıcı oturumlarını sayar.</span><span class="sxs-lookup"><span data-stu-id="081b4-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="081b4-133">Bir süre etkinlik bir süre işlem yapılmadığında birden fazla yarım saat biri tarafından sonlandırıldı, bir kullanıcı tarafından oturumdur.</span><span class="sxs-lookup"><span data-stu-id="081b4-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="081b4-134">Kullanıcıları, oturumlar ve olayları araçları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="081b4-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="081b4-135">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="081b4-135">Page views</span></span>

<span data-ttu-id="081b4-136">Kullanım dikey penceresinden en popüler sayfalarınızı dökümünü almak için sayfa görünümleri döşeme tıklayın:</span><span class="sxs-lookup"><span data-stu-id="081b4-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![Genel Bakış dikey penceresinden sayfa görünümleri grafiği tıklatın](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="081b4-138">Yukarıdaki örnek bir oyun web sitesinden ' dir.</span><span class="sxs-lookup"><span data-stu-id="081b4-138">The example above is from a games web site.</span></span> <span data-ttu-id="081b4-139">Grafikte, biz hemen görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="081b4-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="081b4-140">Kullanım, geçen hafta içinde geliştirilmiş kurmadı.</span><span class="sxs-lookup"><span data-stu-id="081b4-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="081b4-141">Belki de arama motoru iyileştirme hakkında düşünüyoruz?</span><span class="sxs-lookup"><span data-stu-id="081b4-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="081b4-142">Tenis en popüler oyun sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="081b4-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="081b4-143">Daha fazla geliştirmeleri bu sayfaya şimdi odaklanır.</span><span class="sxs-lookup"><span data-stu-id="081b4-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="081b4-144">Ortalama, kullanıcıların tenis sayfasını yaklaşık üç kez haftalık ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="081b4-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="081b4-145">(Yaklaşık üç kat daha fazla oturumları kullanıcıları daha vardır.)</span><span class="sxs-lookup"><span data-stu-id="081b4-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="081b4-146">Kullanıcıların çoğunun ABD çalışma hafta sırasında ve çalışma saatleri içinde sitesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="081b4-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="081b4-147">Web sayfasında belki de bir "hızlı gizle" düğmesini sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="081b4-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="081b4-148">[Ek açıklamaları](app-insights-annotations.md) Web sitesi yeni sürümlerini ne zaman dağıtılan grafikte göster.</span><span class="sxs-lookup"><span data-stu-id="081b4-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="081b4-149">Son dağıtımlarda hiçbirinin kullanım belirgin bir etkisi vardı.</span><span class="sxs-lookup"><span data-stu-id="081b4-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="081b4-150">Ne sitenizi siteniz, sayfa görünümü telemetrisi gönderir özel bir özellik tarafından bölme gibi daha ayrıntılı trafiği incelemek istediğiniz?</span><span class="sxs-lookup"><span data-stu-id="081b4-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="081b4-151">Açık **olayları** Application Insights kaynağı menüde aracı.</span><span class="sxs-lookup"><span data-stu-id="081b4-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="081b4-152">Bu araç kaç sayfa görünümleri ve özel olaylar çeşitli süzme, cohorting ve kesimleme seçenekleri dayalı uygulamanızdan gönderilen analiz etmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="081b4-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="081b4-153">"Kimin kullanılan" açılır listede "Any sayfa görünümü" seçin.</span><span class="sxs-lookup"><span data-stu-id="081b4-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="081b4-154">"Tarafından bölme" açılır listede, sayfa görünümü telemetrisi bölmek bir özellik seçin.</span><span class="sxs-lookup"><span data-stu-id="081b4-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="081b4-155">Bekletme - kaç kullanıcı döndürülmesini?</span><span class="sxs-lookup"><span data-stu-id="081b4-155">Retention - how many users come back?</span></span>

<span data-ttu-id="081b4-156">Bekletme ne sıklıkta bir, belirli bir zaman aralığındaki yüzdeler sırasında bazı iş eylemi gerçekleştiren kullanıcı cohorts göre kendi uygulama kullanmak için kullanıcılarınızın dönüş anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="081b4-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="081b4-157">Hangi belirli özellikleri diğerlerinden geri daha fazla gelen kullanıcıların neden anlama</span><span class="sxs-lookup"><span data-stu-id="081b4-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="081b4-158">Form varsayımlar gerçek kullanıcı verilerine dayalı</span><span class="sxs-lookup"><span data-stu-id="081b4-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="081b4-159">Bekletme ürününüz için bir sorun olup olmadığını</span><span class="sxs-lookup"><span data-stu-id="081b4-159">Determine whether retention is a problem in your product</span></span> 

![Bekletme](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="081b4-161">Üstteki bekletme denetimleri, belirli olayları ve saklama hesaplamak için zaman aralığını tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="081b4-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="081b4-162">Orta grafiğinde görsel bir genel saklama yüzdesi belirtilen zaman aralığına göre sağlar.</span><span class="sxs-lookup"><span data-stu-id="081b4-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="081b4-163">Grafiğin altındaki belirli bir dönemde saklama temsil eder.</span><span class="sxs-lookup"><span data-stu-id="081b4-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="081b4-164">Bu düzeyde ayrıntı, kullanıcıların ne yaptıklarını ve ne daha ayrıntılı ayrıntı düzeyi döndürmeyi kullanıcıları etkileyebilecek anlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="081b4-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="081b4-165">Bekletme aracı hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="081b4-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="081b4-166">Özel iş olayları</span><span class="sxs-lookup"><span data-stu-id="081b4-166">Custom business events</span></span>

<span data-ttu-id="081b4-167">Kullanıcılar web uygulamanızı ile neler NET bir anlayış almak için özel günlük olaylarıyla kod satırlarını eklemek yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="081b4-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="081b4-168">Bu olaylar herhangi bir şey satın alma veya oyun kazanma gibi daha önemli iş olaylarına belirli düğmelerini gibi ayrıntılı kullanıcı eylemlerine izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="081b4-169">Bazı durumlarda, sayfa görünümleri yararlı olaylar gösterebilir rağmen genel doğru değil.</span><span class="sxs-lookup"><span data-stu-id="081b4-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="081b4-170">Bir kullanıcı, ürün satın alma olmadan bir ürün sayfasını açabilir.</span><span class="sxs-lookup"><span data-stu-id="081b4-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="081b4-171">Belirli iş olaylarla kullanıcılarınızın siteniz aracılığıyla kullanıcılarınızın ilerleme grafik.</span><span class="sxs-lookup"><span data-stu-id="081b4-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="081b4-172">Farklı seçenekler için tercihlerini çıkışı bulabilir ve bunlar bırakma out veya sorunlar vardır.</span><span class="sxs-lookup"><span data-stu-id="081b4-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="081b4-173">Bu bilgiyle, geliştirme kapsamınızı önceliklerini hakkında bilinçli kararlar yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="081b4-174">Web sayfasında olayları kaydedilebilir:</span><span class="sxs-lookup"><span data-stu-id="081b4-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="081b4-175">Veya web uygulamasının sunucu tarafı:</span><span class="sxs-lookup"><span data-stu-id="081b4-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="081b4-176">Filtre ya da Portalı'nda incelediğinizde olayları bölme özellik değerlerini bu olaylara iliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="081b4-177">Ayrıca, tek bir kullanıcıya etkinlik dizisini izlemenizi sağlayan bir anonim kullanıcı kimliği gibi her olay için bir standart özellikler kümesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="081b4-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="081b4-178">Daha fazla bilgi edinmek [özel olaylar](app-insights-api-custom-events-metrics.md#trackevent) ve [özellikleri](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="081b4-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="081b4-179">Dilimlediği olayları</span><span class="sxs-lookup"><span data-stu-id="081b4-179">Slice and dice events</span></span>

<span data-ttu-id="081b4-180">Kullanıcıları, oturumlar ve olayları araçlarında dilim ve kullanıcı, olay adı ve özellikleri tarafından özel olaylar inin.</span><span class="sxs-lookup"><span data-stu-id="081b4-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="081b4-181">![Kullanıcılar](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="081b4-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="081b4-182">Tasarım telemetri uygulama</span><span class="sxs-lookup"><span data-stu-id="081b4-182">Design the telemetry with the app</span></span>

<span data-ttu-id="081b4-183">Her bir özellik, uygulamanızın tasarlarken, kullanıcılarınız ile başarısını ölçmek için nasıl adımıdır göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="081b4-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="081b4-184">Hangi iş olaylarını kaydetmek için gereken ve izleme olayları için uygulamanıza başından çağıran kodu karar verin.</span><span class="sxs-lookup"><span data-stu-id="081b4-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="081b4-185">A | B testi</span><span class="sxs-lookup"><span data-stu-id="081b4-185">A | B Testing</span></span>
<span data-ttu-id="081b4-186">Bir özelliğin hangi değişken daha başarılı olacaktır bilmiyorsanız, bunların her farklı erişilebilir kullanıcıların her ikisi de serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="081b4-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="081b4-187">Her başarısını ölçmenize ve birleştirilmiş bir sürüme taşıyın.</span><span class="sxs-lookup"><span data-stu-id="081b4-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="081b4-188">Bu bir teknik uygulamanızı her sürümü tarafından gönderilen tüm telemetri için ayrı özellik değerlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="081b4-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="081b4-189">Bunu etkin TelemetryContext özelliklerini tanımlayarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="081b4-190">Bu varsayılan özellikleri, uygulamanın gönderdiği - her telemetri iletiye özel iletilerinizi değil, ancak standart telemetriyi de eklenir.</span><span class="sxs-lookup"><span data-stu-id="081b4-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="081b4-191">Application Insights portalında filtre ve farklı sürümlerini karşılaştırmak için özellik değerleri, verilerinizde bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="081b4-192">Bunu yapmak için [telemetri Başlatıcı ayarlama](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="081b4-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="081b4-193">Web uygulama Başlatıcı Global.asax.cs gibi:</span><span class="sxs-lookup"><span data-stu-id="081b4-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="081b4-194">Tüm yeni TelemetryClients belirttiğiniz özellik değeri otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="081b4-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="081b4-195">Telemetri olaylarını tek tek varsayılan değerleri geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="081b4-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="081b4-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="081b4-196">Next steps</span></span>
   - [<span data-ttu-id="081b4-197">Kullanıcılar, Oturumlar, Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="081b4-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="081b4-198">Huniler</span><span class="sxs-lookup"><span data-stu-id="081b4-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="081b4-199">Bekletme</span><span class="sxs-lookup"><span data-stu-id="081b4-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="081b4-200">Kullanıcı Akışları</span><span class="sxs-lookup"><span data-stu-id="081b4-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="081b4-201">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="081b4-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="081b4-202">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="081b4-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
