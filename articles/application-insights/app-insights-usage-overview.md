---
title: "Azure Application Insights ile web uygulamaları için aaaUsage çözümleme | Microsoft docs"
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="59157-103">Application Insights ile web uygulamaları için kullanım analizi</span><span class="sxs-lookup"><span data-stu-id="59157-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="59157-104">Web uygulamanızın hangi özellikleri en popüler var mı?</span><span class="sxs-lookup"><span data-stu-id="59157-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="59157-105">Kullanıcılarınızın uygulamanızla hedeflerine ulaşması?</span><span class="sxs-lookup"><span data-stu-id="59157-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="59157-106">Bunlar belirli zamanlarda bırakma ve döndürmeleri daha sonra?</span><span class="sxs-lookup"><span data-stu-id="59157-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="59157-107">[Azure Application Insights](app-insights-overview.md) , kişiler, web uygulamanızın kullanımını içine güçlü Öngörüler kazanmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="59157-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="59157-108">Uygulamanızı güncelleştirme her zaman, kullanıcılar için ne kadar iyi çalıştığı değerlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59157-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="59157-109">Bu bilgiyle, veri sonraki geliştirme döngüsü hakkında kararlar tabanlı yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59157-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="59157-110">Telemetriyi uygulamanızdan Gönder</span><span class="sxs-lookup"><span data-stu-id="59157-110">Send telemetry from your app</span></span>

<span data-ttu-id="59157-111">Uygulama sunucusu kodunuzu hem de web sayfalarınıza Application Insights yükleyerek Hello en iyi deneyimi elde edilir.</span><span class="sxs-lookup"><span data-stu-id="59157-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="59157-112">Merhaba istemci ve sunucu bileşenleri, uygulamanızın telemetri geri toohello analiz için Azure portalı gönderin.</span><span class="sxs-lookup"><span data-stu-id="59157-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="59157-113">**Sunucu kodu:** için yükleme hello uygun modülü, [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), veya [diğer](app-insights-platforms.md) uygulama.</span><span class="sxs-lookup"><span data-stu-id="59157-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="59157-114">*Tooinstall sunucu kodu istiyor mu? Yalnızca [Azure Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="59157-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="59157-115">**Web sayfası koduna:** açık hello [Azure portal](https://portal.azure.com), uygulamanız için hello Application Insights kaynağı açın ve ardından açın **Başlarken > İzleme ve tanılama istemci tarafı**.</span><span class="sxs-lookup"><span data-stu-id="59157-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Merhaba komut dosyası ana web sayfanızın hello head kopyalayın.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="59157-117">**Telemetri alın:** projeniz için bir kaç dakika hata ayıklama modunda çalıştırılması ve hello genel bakış dikey penceresinde Application Insights sonuçlarında arayın.</span><span class="sxs-lookup"><span data-stu-id="59157-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="59157-118">Uygulamanızın performansını uygulama toomonitor yayımlama ve uygulamanızla kullanıcıların ne yaptıklarını bulun.</span><span class="sxs-lookup"><span data-stu-id="59157-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="59157-119">Kullanıcı ve oturum kimliği, telemetri dahil</span><span class="sxs-lookup"><span data-stu-id="59157-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="59157-120">zaman içinde tootrack kullanıcılar, Application Insights gerektirir yolu tooidentify bunları.</span><span class="sxs-lookup"><span data-stu-id="59157-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="59157-121">bir kullanıcı kimliği veya bir oturum kimliği gerektirmez yalnızca kullanım aracı araçtır hello olayları hello</span><span class="sxs-lookup"><span data-stu-id="59157-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="59157-122">Bu kimlikleri göndermeye Başla [burada](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="59157-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="59157-123">Kullanım demografisine ve istatistikleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="59157-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="59157-124">Kişiler uygulamanızı kullandığınızda, bunlar en, kullanıcılarınızın bulunduğu ilgileniyor hangi sayfaların, hangi tarayıcılar ve işletim sistemleri bunlar kullandığını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="59157-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="59157-125">Merhaba kullanıcı ve oturum raporlar verilerinize sayfaları veya özel olaylar göre filtre uygulamak ve bunları konumu, ortam ve sayfa gibi özelliklere göre segmentlere ayırmak.</span><span class="sxs-lookup"><span data-stu-id="59157-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="59157-126">Kendi filtreler de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59157-126">You can also add your own filters.</span></span>

![Kullanıcılar](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="59157-128">Veri kümesi hello ilginç kalıpları çıkışı Öngörüler hello sağ üzerinde gelin.</span><span class="sxs-lookup"><span data-stu-id="59157-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="59157-129">Merhaba **kullanıcılar** rapor hello sayıda sayfalarınızı içinde seçilen zaman dönemleriniz erişim benzersiz kullanıcı sayısı.</span><span class="sxs-lookup"><span data-stu-id="59157-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="59157-130">(Kullanıcılar tanımlama bilgilerini kullanarak sayılır.</span><span class="sxs-lookup"><span data-stu-id="59157-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="59157-131">Birisi farklı tarayıcılar veya istemci makinelerle sitenize erişen veya kendi tanımlama bilgilerini temizler, ardından bunlar birden çok kez sayılacaktır.)</span><span class="sxs-lookup"><span data-stu-id="59157-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="59157-132">Merhaba **oturumları** rapor sitenize erişen kullanıcı oturumlarını hello sayısını sayar.</span><span class="sxs-lookup"><span data-stu-id="59157-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="59157-133">Bir süre etkinlik bir süre işlem yapılmadığında birden fazla yarım saat biri tarafından sonlandırıldı, bir kullanıcı tarafından oturumdur.</span><span class="sxs-lookup"><span data-stu-id="59157-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="59157-134">Merhaba kullanıcıları, oturumlar ve olayları araçları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="59157-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="59157-135">Sayfa görünümleri</span><span class="sxs-lookup"><span data-stu-id="59157-135">Page views</span></span>

<span data-ttu-id="59157-136">Merhaba kullanım dikey penceresinden hello sayfa görünümleri döşeme tooget en popüler sayfalarınızı dökümünü tıklayın:</span><span class="sxs-lookup"><span data-stu-id="59157-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![Merhaba genel bakış dikey penceresinden hello sayfa görünümleri grafik tıklayın](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="59157-138">Yukarıdaki Hello örnek bir oyun web sitesinden ' dir.</span><span class="sxs-lookup"><span data-stu-id="59157-138">hello example above is from a games web site.</span></span> <span data-ttu-id="59157-139">Merhaba grafikten biz hemen görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="59157-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="59157-140">Kullanım, geçen hafta hello geliştirilmiş kurmadı.</span><span class="sxs-lookup"><span data-stu-id="59157-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="59157-141">Belki de arama motoru iyileştirme hakkında düşünüyoruz?</span><span class="sxs-lookup"><span data-stu-id="59157-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="59157-142">Tenis hello en popüler oyun sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="59157-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="59157-143">Şimdi daha fazla geliştirmeleri toothis sayfasında odaklanın.</span><span class="sxs-lookup"><span data-stu-id="59157-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="59157-144">Ortalama, kullanıcıların hello tenis sayfasını yaklaşık üç kez haftalık ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="59157-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="59157-145">(Yaklaşık üç kat daha fazla oturumları kullanıcıları daha vardır.)</span><span class="sxs-lookup"><span data-stu-id="59157-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="59157-146">Kullanıcıların çoğunun hello ABD çalışma hafta sırasında ve çalışma saatleri içinde hello sitesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="59157-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="59157-147">Belki de biz "hızlı gizle" düğmesini hello web sayfasında sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="59157-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="59157-148">Merhaba [ek açıklamaları](app-insights-annotations.md) hello Web sitesi yeni sürümlerini ne zaman dağıtılan hello grafikte göster.</span><span class="sxs-lookup"><span data-stu-id="59157-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="59157-149">Merhaba son dağıtımlarda hiçbirinin kullanım belirgin bir etkisi vardı.</span><span class="sxs-lookup"><span data-stu-id="59157-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="59157-150">Ne tooinvestigate hello trafiği tooyour site, site, sayfa görünümü telemetrisi gönderir özel bir özellik tarafından bölme gibi daha ayrıntılı istediğiniz?</span><span class="sxs-lookup"><span data-stu-id="59157-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="59157-151">Açık hello **olayları** hello Application Insights kaynağı menüsünde aracı.</span><span class="sxs-lookup"><span data-stu-id="59157-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="59157-152">Bu araç kaç sayfa görünümleri ve özel olaylar çeşitli süzme, cohorting ve kesimleme seçenekleri dayalı uygulamanızdan gönderilen analiz etmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="59157-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="59157-153">"Any sayfa görünümü" Hello "Kimin kullanılan" açılır listesinde, seçin.</span><span class="sxs-lookup"><span data-stu-id="59157-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="59157-154">Merhaba "Tarafından bölme" açılır listede tarafından hangi toosplit sayfanızı görüntülemek telemetri özelliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="59157-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="59157-155">Bekletme - kaç kullanıcı döndürülmesini?</span><span class="sxs-lookup"><span data-stu-id="59157-155">Retention - how many users come back?</span></span>

<span data-ttu-id="59157-156">Bekletme ne sıklıkta kullanıcılarınızın toouse belirli bir zaman aralığı sırasında bazı iş eylemi gerçekleştiren kullanıcı cohorts göre kendi uygulama dönüş anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="59157-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="59157-157">Hangi belirli özellikleri diğerlerinden daha fazla toocome geri kullanıcıların neden anlama</span><span class="sxs-lookup"><span data-stu-id="59157-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="59157-158">Form varsayımlar gerçek kullanıcı verilerine dayalı</span><span class="sxs-lookup"><span data-stu-id="59157-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="59157-159">Bekletme ürününüz için bir sorun olup olmadığını</span><span class="sxs-lookup"><span data-stu-id="59157-159">Determine whether retention is a problem in your product</span></span> 

![Bekletme](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="59157-161">Merhaba bekletme denetimleri üstte, toodefine belirli olayları ve zaman aralığı toocalculate bekletme izin verir.</span><span class="sxs-lookup"><span data-stu-id="59157-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="59157-162">Merhaba hello Orta grafiğinde verir görsel bir hello belirtilen hello zaman aralığına göre genel saklama yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="59157-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="59157-163">Merhaba alt Hello grafikte saklama belirli bir dönemde temsil eder.</span><span class="sxs-lookup"><span data-stu-id="59157-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="59157-164">Bu düzeyde ayrıntı kullanıcıların ne yaptıklarını toounderstand ve ne daha ayrıntılı ayrıntı düzeyi döndürmeyi kullanıcıları etkileyebilecek sağlar.</span><span class="sxs-lookup"><span data-stu-id="59157-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="59157-165">Merhaba bekletme aracı hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="59157-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="59157-166">Özel iş olayları</span><span class="sxs-lookup"><span data-stu-id="59157-166">Custom business events</span></span>

<span data-ttu-id="59157-167">tooget hangi kullanıcıların NET bir anlayış yapmak, web uygulamanızı, yararlı tooinsert satırlık bir kod toolog özel olaylar.</span><span class="sxs-lookup"><span data-stu-id="59157-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="59157-168">Bu olayların her şeyi belirli düğmelerini, satın alma veya oyun kazanma gibi toomore önemli iş olayları gibi ayrıntılı kullanıcı eylemlerine izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59157-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="59157-169">Bazı durumlarda, sayfa görünümleri yararlı olaylar gösterebilir rağmen genel doğru değil.</span><span class="sxs-lookup"><span data-stu-id="59157-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="59157-170">Bir kullanıcı hello ürün satın alma olmadan bir ürün sayfasını açabilir.</span><span class="sxs-lookup"><span data-stu-id="59157-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="59157-171">Belirli iş olaylarla kullanıcılarınızın siteniz aracılığıyla kullanıcılarınızın ilerleme grafik.</span><span class="sxs-lookup"><span data-stu-id="59157-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="59157-172">Farklı seçenekler için tercihlerini çıkışı bulabilir ve bunlar bırakma out veya sorunlar vardır.</span><span class="sxs-lookup"><span data-stu-id="59157-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="59157-173">Bu bilgiyle, geliştirme kapsamınızı hello öncelikleri hakkında bilinçli kararlar yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59157-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="59157-174">Olayları hello web sayfasında kaydedilebilir:</span><span class="sxs-lookup"><span data-stu-id="59157-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="59157-175">Veya sunucu tarafı hello web uygulaması hello:</span><span class="sxs-lookup"><span data-stu-id="59157-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="59157-176">Filtre ya da hello Portalı'nda incelediğinizde hello olayları bölme özellik değerleri toothese olayları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59157-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="59157-177">Ayrıca, bir standart özellikler tootrace hello tek bir kullanıcı etkinliklerini bir dizi sağlar anonim kullanıcı kimliği gibi ekli tooeach olay kümesidir.</span><span class="sxs-lookup"><span data-stu-id="59157-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="59157-178">Daha fazla bilgi edinmek [özel olaylar](app-insights-api-custom-events-metrics.md#trackevent) ve [özellikleri](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="59157-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="59157-179">Dilimlediği olayları</span><span class="sxs-lookup"><span data-stu-id="59157-179">Slice and dice events</span></span>

<span data-ttu-id="59157-180">Merhaba kullanıcıları, oturumlar ve olayları araçları dilim ve kullanıcı, olay adı ve özellikleri tarafından özel olaylar inin.</span><span class="sxs-lookup"><span data-stu-id="59157-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="59157-181">![Kullanıcılar](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="59157-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="59157-182">Merhaba telemetri hello uygulama ile tasarlama</span><span class="sxs-lookup"><span data-stu-id="59157-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="59157-183">Her bir özellik, uygulamanızın tasarlarken nasıl toomeasure başarısını Kullanıcılarınızla adımıdır göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="59157-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="59157-184">Ne başlatma toorecord gerekir ve olaylar için çağrı uygulamanıza hello izleme hello kod iş olayları karar verin.</span><span class="sxs-lookup"><span data-stu-id="59157-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="59157-185">A | B testi</span><span class="sxs-lookup"><span data-stu-id="59157-185">A | B Testing</span></span>
<span data-ttu-id="59157-186">Bir özelliğin hangi değişken daha başarılı olacaktır bilmiyorsanız, bunların her erişilebilir toodifferent kullanıcıların her ikisi de serbest bırakın.</span><span class="sxs-lookup"><span data-stu-id="59157-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="59157-187">Her Hello başarısını ölçmenize ve tooa birleşik sürüm taşıyın.</span><span class="sxs-lookup"><span data-stu-id="59157-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="59157-188">Bu yöntem, her sürümü, uygulamanız tarafından gönderilen farklı özellik değerleri tooall hello telemetri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59157-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="59157-189">Bunu hello özelliklerini tanımlayarak yapabilirsiniz etkin TelemetryContext.</span><span class="sxs-lookup"><span data-stu-id="59157-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="59157-190">Bu varsayılan özellikleri uygulama hello tooevery telemetri iletisi gönderir - yalnızca, özel iletiler, ancak de standart telemetri hello eklenir.</span><span class="sxs-lookup"><span data-stu-id="59157-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="59157-191">Merhaba Application Insights portalında filtre ve hello özellik değerleri, verilerinizde toocompare hello farklı sürümlerini farklı şekilde bölebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59157-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="59157-192">toodo bunu [telemetri Başlatıcı ayarlama](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="59157-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="59157-193">Merhaba web uygulama Başlatıcı Global.asax.cs gibi:</span><span class="sxs-lookup"><span data-stu-id="59157-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="59157-194">Tüm yeni TelemetryClients belirttiğiniz başlangıç özellik değeri otomatik olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="59157-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="59157-195">Telemetri olaylarını tek tek hello varsayılan değerleri geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="59157-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59157-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59157-196">Next steps</span></span>
   - [<span data-ttu-id="59157-197">Kullanıcılar, Oturumlar, Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="59157-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="59157-198">Huniler</span><span class="sxs-lookup"><span data-stu-id="59157-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="59157-199">Bekletme</span><span class="sxs-lookup"><span data-stu-id="59157-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="59157-200">Kullanıcı Akışları</span><span class="sxs-lookup"><span data-stu-id="59157-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="59157-201">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="59157-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="59157-202">Kullanıcı bağlamı Ekle</span><span class="sxs-lookup"><span data-stu-id="59157-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
