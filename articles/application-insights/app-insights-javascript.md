---
title: "JavaScript web uygulamaları için Azure Application Insights | Microsoft Docs"
description: "Sayfa görünümü ve oturum sayısını, web istemci verilerini alın ve kullanım desenlerini izleyin. JavaScript web sayfalarında özel durumları ve performans sorunlarını yakalayın."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="7da1a-104">Web sayfaları için Application Insights</span><span class="sxs-lookup"><span data-stu-id="7da1a-104">Application Insights for web pages</span></span>
<span data-ttu-id="7da1a-105">Web sayfanızın veya uygulamanızın performansı ve kullanımı hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="7da1a-106">Sayfa betiğinize [Application Insights](app-insights-overview.md)’ı ekleyerek, sayfa yüklemelerinin ve AJAX çağrılarının zamanlamalarının yanı sıra, tarayıcı özel durumları ile AJAX hatalarının sayılarını ve ayrıntılarını, ayrıca kullanıcı ve oturum sayılarını elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="7da1a-107">Bunların tümü sayfaya, istemci işletim sistemi ve tarayıcı sürümüne, coğrafi konuma ve başka boyutlara göre kesimlere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="7da1a-108">Hata sayısı veya yavaş sayfa yüklemesi hakkında uyarı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="7da1a-109">Ayrıca JavaScript kodunuza izleme çağrıları ekleyerek web sayfası uygulamanızın farklı özelliklerinin nasıl kullanıldığını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="7da1a-110">Application Insights tüm web sayfalarıyla kullanılabilir; kısa bir JavaScript eklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="7da1a-111">Web hizmetinizin [Java](app-insights-java-get-started.md) veya [ASP.NET](app-insights-asp-net.md) olması halinde, sunucunuzdan ve istemcilerinizden telemetri tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![portal.azure.com adresinde uygulamanızın kaynağını açıp Tarayıcı’ya tıklayın](./media/app-insights-javascript/03.png)

<span data-ttu-id="7da1a-113">Bir [Microsoft Azure](https://azure.com) aboneliğine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="7da1a-114">Takımınızın kurumsal bir aboneliği varsa sahibinden Microsoft Hesabınızı eklemesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="7da1a-115">Geliştirme ve küçük ölçekli kullanımın herhangi bir maliyeti olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="7da1a-116">Web sayfalarınız için Application Insights’ı ayarlama</span><span class="sxs-lookup"><span data-stu-id="7da1a-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="7da1a-117">Yükleyici kod parçacığını web sayfalarınıza aşağıdaki şekilde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="7da1a-118">Application Insights kaynağı açma veya oluşturma</span><span class="sxs-lookup"><span data-stu-id="7da1a-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="7da1a-119">Sayfanızın performansı ve kullanımı hakkında verilerin görüntülendiği yer Application Insights kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="7da1a-120">[Azure portalda](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7da1a-121">Uygulamanız sunucu tarafı için izlemeyi zaten ayarladıysanız zaten bir kaynağınız vardır:</span><span class="sxs-lookup"><span data-stu-id="7da1a-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Gözat, Geliştirici Hizmetleri, Application Insights’ı seçin.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="7da1a-123">Yoksa, bir tane oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7da1a-123">If you don't have one, create it:</span></span>

![Yeni, Geliştirici Hizmetleri, Application Insights’ı seçin.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="7da1a-125">*Hala sorularınız mı var?*</span><span class="sxs-lookup"><span data-stu-id="7da1a-125">*Questions already?*</span></span> <span data-ttu-id="7da1a-126">[Kaynak oluşturma hakkında daha fazla bilgi](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7da1a-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="7da1a-127">Uygulamanıza veya web sayfalarınıza SDK betiği ekleme</span><span class="sxs-lookup"><span data-stu-id="7da1a-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="7da1a-128">Hızlı Başlangıç’ta web sayfaları için betik alın:</span><span class="sxs-lookup"><span data-stu-id="7da1a-128">In Quick Start, get the script for web pages:</span></span>

![Uygulamaya genel bakış dikey pencerenizde, Hızlı Başlat, Web sayfalarımı izlemeyi sağlayan kodu al'ı seçin.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="7da1a-131">Betiği, izlemek istediğiniz her sayfanın `</head>` etiketinin hemen önüne ekleyin. Web sayfanızda bir ana sayfa varsa betiği buraya koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="7da1a-132">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7da1a-132">For example:</span></span>

* <span data-ttu-id="7da1a-133">ASP.NET MVC projesinde `View\Shared\_Layout.cshtml` içine koyabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7da1a-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="7da1a-134">SharePoint sitesinde, denetim masasında [Site Ayarları / Ana Sayfa](app-insights-sharepoint.md)’yı açın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="7da1a-135">Betikte, verileri Application Insights kaynağınıza yönlendiren izleme anahtarı bulunur.</span><span class="sxs-lookup"><span data-stu-id="7da1a-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="7da1a-136">([Betiğin daha ayrıntılı açıklaması](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="7da1a-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="7da1a-137">*(İyi bilinen web sayfası altyapısı kullanıyorsanız, Application Insights bağdaştırıcılarını araştırın. Örneğin, [AngularJS modülü](http://ngmodules.org/modules/angular-appinsights) var.)*</span><span class="sxs-lookup"><span data-stu-id="7da1a-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="7da1a-138">Ayrıntılı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7da1a-138">Detailed configuration</span></span>
<span data-ttu-id="7da1a-139">Çoğunlukla gerekmese de, ayarlayabileceğiniz birkaç [parametre](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) vardır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="7da1a-140">Örneğin, sayfa başına görünümde bildirilen Ajax çağrılarını devre dışı bırakabilir veya çağrıların sayısını sınırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="7da1a-141">Alternatif olarak, hata ayıklama modunu; telemetriyi toplu hale getirilmeden, ardışık düzende taşıyacak şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="7da1a-142">Bu parametreleri ayarlamak için kod parçacığında bu satırı bulun ve şunun arkasına virgülle ayrılmış daha fazla öğe ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7da1a-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="7da1a-143">[Kullanılabilir parametreler](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7da1a-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="7da1a-144"><a name="run"></a>Uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7da1a-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="7da1a-145">Web uygulamanızı çalıştırın, telemetri oluşturmak için bir süre bunu kullanın ve birkaç saniye bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="7da1a-146">Geliştirme makinenizdeki **F5** tuşunu kullanarak bunu çalıştırabilir ya da yayımlayabilir ve kullanıcıların bunu yürütmesine izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="7da1a-147">Web uygulamasının Application Insights’a gönderdiği telemetriyi denetlemek istiyorsanız, tarayıcınızın hata ayıklama araçlarını kullanın (birçok tarayıcıda **F12**).</span><span class="sxs-lookup"><span data-stu-id="7da1a-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="7da1a-148">Veriler dc.services.visualstudio.com adresine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="7da1a-149">Tarayıcı performans verilerinizi araştırma</span><span class="sxs-lookup"><span data-stu-id="7da1a-149">Explore your browser performance data</span></span>
<span data-ttu-id="7da1a-150">Kullanıcılarınızın tarayıcılarından toplanan performans verilerini göstermek için Tarayıcı dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![portal.azure.com adresinde uygulamanızın kaynağını açıp Ayarlar, Tarayıcı’ya tıklama](./media/app-insights-javascript/03.png)

<span data-ttu-id="7da1a-152">*Henüz veri yok mu? Sayfanın üstündeki **Yenile**'ye tıklayın. Hala hiçbir şey yok mu? Bkz. [Sorun giderme](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="7da1a-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="7da1a-153">Tarayıcı dikey penceresi, hazır filtrelerin ve grafik seçimlerinin bulunduğu [Ölçüm Gezgini dikey penceresidir](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="7da1a-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="7da1a-154">İsterseniz zaman aralığını, filtreleri ve grafik yapılandırmasını düzenleyebilir ve sonucu sık kullanılan olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="7da1a-155">Asıl dikey pencere yapılandırmasına dönmek için **Varsayılanları geri yükle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="7da1a-156">Sayfa yükleme performansı</span><span class="sxs-lookup"><span data-stu-id="7da1a-156">Page load performance</span></span>
<span data-ttu-id="7da1a-157">Üst kısım sayfa yükleme sürelerinin bölümlenmiş bir grafiğidir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="7da1a-158">Grafiğin toplam yüksekliği yüklenecek ortalama süreyi ve kullanıcılarınızın tarayıcılarda uygulamanızdan görüntülenecek sayfaları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7da1a-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="7da1a-159">Süre, düzen ve çalışma betikleri de dahil tüm zaman uyumlu yük etkinlikleri işlenene kadar tarayıcının ilk HTTP isteğini gönderdiği zamandan ölçülür.</span><span class="sxs-lookup"><span data-stu-id="7da1a-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="7da1a-160">AJAX çağrılarından web bölümleri yükleme gibi zaman uyumsuz görevleri içermez.</span><span class="sxs-lookup"><span data-stu-id="7da1a-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="7da1a-161">Grafik, toplam sayfa yükleme süresini [W3C tarafından tanımlanan standart zamanlamalara](http://www.w3.org/TR/navigation-timing/#processing-model) böler.</span><span class="sxs-lookup"><span data-stu-id="7da1a-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="7da1a-162">*Ağa bağlanma* süresinin çoğunlukla beklediğinizden kısa olduğunu unutmayın; bunun nedeni, tarayıcıdan sunucuya yapılan tüm isteklerin ortalaması olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="7da1a-163">Tek tek isteklerin çoğunun bağlantı süresi 0 değerindedir; çünkü sunucuya zaten etkin bir bağlantı vardır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="7da1a-164">Yavaş mı yükleniyor?</span><span class="sxs-lookup"><span data-stu-id="7da1a-164">Slow loading?</span></span>
<span data-ttu-id="7da1a-165">Yavaş sayfa yüklenmesi kullanım memnuniyetsizliğinin başlıca kaynaklarından biridir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="7da1a-166">Grafik yavaş sayfa yüklemeleri gösteriyorsa, bazı tanılama araştırmalarını yapmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="7da1a-167">Grafik, uygulamanızdaki tüm sayfa yüklerinin ortalamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="7da1a-168">Sorunun belirli sayfalara sınırlı olup olmadığını görmek için, sayfa URL'siyle bölümlenmiş kılavuzun bulunduğu dikey pencereyi daha fazla inceleyin:</span><span class="sxs-lookup"><span data-stu-id="7da1a-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="7da1a-169">Sayfa görünümü sayısına ve standart sapmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="7da1a-170">Sayfa sayısı çok azsa, sorun kullanıcıları çok etkilemez.</span><span class="sxs-lookup"><span data-stu-id="7da1a-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="7da1a-171">Yüksek bir standart sapma (ortalamayla karşılaştırılabilir) tek tek ölçüler arasında çok sayıda farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="7da1a-172">**Tek URL’yi ve tek sayfa görünümünü yakınlaştırma.**</span><span class="sxs-lookup"><span data-stu-id="7da1a-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="7da1a-173">Tam da bu URL için filtre uygulanmış tarayıcı grafiklerinin dikey penceresini görüntülemek için sayfa adlarından istediğinize tıklayın; bundan sonra da bir sayfa görünümü örneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="7da1a-174">Bu etkinlikle ilgili özelliklerin tam listesi için `...` seçeneğine tıklayın veya Ajax çağrılarını ve bağlantılı etkinlikleri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="7da1a-175">Zaman uyumluysalar, Yavaş Ajax çağrıları genel sayfa yükleme süresini etkiler.</span><span class="sxs-lookup"><span data-stu-id="7da1a-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="7da1a-176">İlgili etkinlikler aynı URL için sunucu isteklerini ekler (web sunucunuza Application Insights kurduysanız).</span><span class="sxs-lookup"><span data-stu-id="7da1a-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="7da1a-177">**Zaman içerisinde performans sayfası.**</span><span class="sxs-lookup"><span data-stu-id="7da1a-177">**Page performance over time.**</span></span> <span data-ttu-id="7da1a-178">Tarayıcılar dikey penceresine dönün, Sayfa Görünümü Yükleme Süresi kılavuzunu çizgi grafiği olarak değiştirerek belirli zamanlarda yükselme olup olmadığına bakın:</span><span class="sxs-lookup"><span data-stu-id="7da1a-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Kılavuzun başlığına tıklayın ve yeni bir grafik türü seçin](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="7da1a-180">**Diğer boyutlara göre bölme.**</span><span class="sxs-lookup"><span data-stu-id="7da1a-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="7da1a-181">Sayfalarınızın yavaş yüklenme nedeni belirli bir tarayıcı, istemci işletim sistemi veya kullanıcı konumu olabilir mi?</span><span class="sxs-lookup"><span data-stu-id="7da1a-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="7da1a-182">Yeni bir grafik ekleyin ve denemenizi **Gruplandır** boyutuyla yapın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="7da1a-183">AJAX Performansı</span><span class="sxs-lookup"><span data-stu-id="7da1a-183">AJAX Performance</span></span>
<span data-ttu-id="7da1a-184">Web sayfalarınızda AJAX çağrılarının iyi iş çıkardığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="7da1a-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="7da1a-185">Bunlar çoğunlukla zaman uyumsuz olarak sayfanızı bölümlerini doldurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="7da1a-186">Genel sayfa hemen yüklenebilse de, kullanıcılarınızın boş web bölümlerine bakıp burada veri görünmesini bekleyerek hayal kırıklığına uğrayabilirler.</span><span class="sxs-lookup"><span data-stu-id="7da1a-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="7da1a-187">Web sayfasından oluşturulan AJAX çağrıları Tarayıcılar dikey penceresinde bağımlılıklar olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="7da1a-188">Dikey pencerenin üst kısmında özet grafikleri vardır:</span><span class="sxs-lookup"><span data-stu-id="7da1a-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="7da1a-189">daha aşağıda da ayrıntılı kılavuzlar:</span><span class="sxs-lookup"><span data-stu-id="7da1a-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="7da1a-190">Belirli ayrıntılar için herhangi bir satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="7da1a-191">Dikey pencerede Tarayıcılar filtresini silerseniz, bu grafiklere hem sunucu hem de AJAX bağımlılıkları eklenir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="7da1a-192">Filtreyi yeniden yapılandırmak için Varsayılanları Geri Yükle'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="7da1a-193">**Başarısız Ajax çağrılarını incelemek için** Bağımlılık hataları kılavuzuna gidin ve belirli örnekleri görmek için bir satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="7da1a-194">Ajax çağrısıyla ilgili tam telemetri için `...` seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="7da1a-195">Hiç Ajax çağrısı bildirilmedi mi?</span><span class="sxs-lookup"><span data-stu-id="7da1a-195">No Ajax calls reported?</span></span>
<span data-ttu-id="7da1a-196">Ajax çağrılarında web sayfanızın betiğinden oluşturulan HTTP/HTTPS çağrıları vardır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="7da1a-197">Bunların bildirildiğini görmüyorsanız, kod parçacığının `disableAjaxTracking` öğesini veya `maxAjaxCallsPerView` [parametrelerini](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) ayarlayıp ayarlamadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="7da1a-198">Tarayıcı özel durumları</span><span class="sxs-lookup"><span data-stu-id="7da1a-198">Browser exceptions</span></span>
<span data-ttu-id="7da1a-199">Tarayıcılar dikey penceresinde bir özel durum özet grafiği, dikey pencerenin daha aşağısındaysa özel durum türleri kılavuzu bulunur.</span><span class="sxs-lookup"><span data-stu-id="7da1a-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="7da1a-200">Tarayıcı özel durumlarının bildirildiğini görmüyorsanız, kod parçacığının `disableExceptionTracking`[parametresini](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) ayarlayıp ayarlamadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="7da1a-201">Tek tek sayfa görünümü etkinliklerini inceleme</span><span class="sxs-lookup"><span data-stu-id="7da1a-201">Inspect individual page view events</span></span>

<span data-ttu-id="7da1a-202">Sayfa görünümü telemetrisi çoğunlukla Application Insights tarafından analiz edilir; yalnızca birikmeli raporları, tüm kullanıcıların ortalamasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="7da1a-203">Ancak, hata ayıklama amacıyla tek tek sayfa görünümü etkinliklerine de bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="7da1a-204">Tanılama Ara dikey penceresinde Filtreler’i Sayfa Görünümü olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="7da1a-205">Daha fazla ayrıntı için herhangi bir olayı seçin.</span><span class="sxs-lookup"><span data-stu-id="7da1a-205">Select any event to see more detail.</span></span> <span data-ttu-id="7da1a-206">Daha da fazla ayrıntı görmek için, ayrıntılar sayfasında "..." öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7da1a-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="7da1a-207">[Ara](app-insights-diagnostic-search.md) seçeneğini kullanırsanız, tam sözcükleri eşleştirmeye özen gösterin: "Hak" ve "Hakkın" girişleri "About" sözcüğüyle eşleşmez.</span><span class="sxs-lookup"><span data-stu-id="7da1a-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="7da1a-208">Ayrıca sayfa görünümlerini aramak için güçlü [Log Analytics dilinden](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) de yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="7da1a-209">Sayfa görünümü özellikleri</span><span class="sxs-lookup"><span data-stu-id="7da1a-209">Page view properties</span></span>
* <span data-ttu-id="7da1a-210">**Sayfa görünümü süresi**</span><span class="sxs-lookup"><span data-stu-id="7da1a-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="7da1a-211">Varsayılan olarak, istemcinin tam yükleme isteğine ait sayfa yükleme süresi (yardımcı dosyalar da dahildir, ancak Ajax çağırıları gibi zaman uyumsuz görevler hariç tutulur).</span><span class="sxs-lookup"><span data-stu-id="7da1a-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="7da1a-212">`overridePageViewDuration` seçeneğini [sayfa yapılandırması](#detailed-configuration) içinde ayarlarsanız, ilk `trackPageView` yürütmesi için istemci isteğinin zaman aralığıdır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="7da1a-213">betiğin başlatılmasından sonra trackPageView öğesini normal konumundan taşırsanız farklı bir değer yansıtır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="7da1a-214">`overridePageViewDuration` ayarlanmış ve süre bağımsız değişkeni `trackPageView()` çağrısında verilmişse, bunun yerine bağımsız değişken değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7da1a-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="7da1a-215">Özel sayfa sayıları</span><span class="sxs-lookup"><span data-stu-id="7da1a-215">Custom page counts</span></span>
<span data-ttu-id="7da1a-216">Varsayılan olarak, istemci tarayıcısına yeni bir sayfanın her yüklenişinde bir sayfa sayısı oluşur.</span><span class="sxs-lookup"><span data-stu-id="7da1a-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="7da1a-217">Ancak, ek sayfa görünümlerini de saymak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-217">But you might want to count additional page views.</span></span> <span data-ttu-id="7da1a-218">Örneğin, sayfa içeriğini sekmelerde görüntüleyebilir; sizse kullanıcı sekmeler arasında geçiş yaptığında sayfayı saymak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="7da1a-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="7da1a-219">Sayfadaki JavaScript kodu tarayıcının URL’sini değiştirmeden yeni içerik yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="7da1a-220">İstemci kodunun uygun bir noktasına buradaki gibi JavaScript çağrısı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7da1a-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="7da1a-221">Sayfa adında,URL’deki karakterlerin aynısı bulunabilir, ancak "#" veya "?" karakterinden sonraki her şey göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="7da1a-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="7da1a-222">Kullanımı izleme</span><span class="sxs-lookup"><span data-stu-id="7da1a-222">Usage tracking</span></span>
<span data-ttu-id="7da1a-223">Uygulamanızla kullanıcılarınızın neler yaptığını bilmek ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="7da1a-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="7da1a-224">Kullanımı izleme hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="7da1a-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="7da1a-225">[Özel etkinlikler ve ölçüm API’si hakkında bilgi edinin](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="7da1a-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="7da1a-226"><a name="video"></a> Video</span><span class="sxs-lookup"><span data-stu-id="7da1a-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="7da1a-227"><a name="next"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7da1a-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="7da1a-228">Kullanımı izleme</span><span class="sxs-lookup"><span data-stu-id="7da1a-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="7da1a-229">Özel etkinlikler ve ölçümler</span><span class="sxs-lookup"><span data-stu-id="7da1a-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="7da1a-230">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="7da1a-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

