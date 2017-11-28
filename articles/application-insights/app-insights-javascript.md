---
title: "JavaScript için aaaAzure Application Insights web uygulamaları | Microsoft Docs"
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
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="f48fc-104">Web sayfaları için Application Insights</span><span class="sxs-lookup"><span data-stu-id="f48fc-104">Application Insights for web pages</span></span>
<span data-ttu-id="f48fc-105">Merhaba performans ve web sayfası veya uygulama kullanımı hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="f48fc-106">Eklerseniz [Application Insights](app-insights-overview.md) tooyour sayfa komut dosyası, sayfa yükler ve AJAX çağrıları, sayıları ve tarayıcı özel durumlar ve AJAX hataları yanı sıra kullanıcıları ve oturum sayıları ayrıntılarını zamanlamaları alın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="f48fc-107">Bunların tümü sayfaya, istemci işletim sistemi ve tarayıcı sürümüne, coğrafi konuma ve başka boyutlara göre kesimlere ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="f48fc-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="f48fc-108">Hata sayısı veya yavaş sayfa yüklemesi hakkında uyarı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="f48fc-109">Ve JavaScript kodunuzda izleme çağrıları ekleyerek hello farklı özellikler, web sayfası uygulamanızın nasıl kullanıldığını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="f48fc-110">Application Insights tüm web sayfalarıyla kullanılabilir; kısa bir JavaScript eklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="f48fc-111">Web hizmetinizin [Java](app-insights-java-get-started.md) veya [ASP.NET](app-insights-asp-net.md) olması halinde, sunucunuzdan ve istemcilerinizden telemetri tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![portal.azure.com adresinde uygulamanızın kaynağını açıp Tarayıcı’ya tıklayın](./media/app-insights-javascript/03.png)

<span data-ttu-id="f48fc-113">Bir abonelik gerekiyor[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="f48fc-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="f48fc-114">Takımınızın kurumsal bir aboneliği varsa, Microsoft Account tooit hello sahibi tooadd isteyin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="f48fc-115">Geliştirme ve küçük ölçekli kullanımın herhangi bir maliyeti olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="f48fc-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="f48fc-116">Web sayfalarınız için Application Insights’ı ayarlama</span><span class="sxs-lookup"><span data-stu-id="f48fc-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="f48fc-117">Hello yükleyicisi kod parçacığını tooyour web sayfaları, aşağıdaki şekilde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="f48fc-118">Application Insights kaynağı açma veya oluşturma</span><span class="sxs-lookup"><span data-stu-id="f48fc-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="f48fc-119">sayfanızın performansı ve kullanımı hakkında verilerin görüntülendiği Hello Application Insights kaynağı değil.</span><span class="sxs-lookup"><span data-stu-id="f48fc-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="f48fc-120">[Azure portalda](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f48fc-121">Uygulamanızın hello sunucu tarafı için izlemeyi zaten ayarladıysanız zaten bir kaynağa sahip:</span><span class="sxs-lookup"><span data-stu-id="f48fc-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Gözat, Geliştirici Hizmetleri, Application Insights’ı seçin.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="f48fc-123">Yoksa, bir tane oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f48fc-123">If you don't have one, create it:</span></span>

![Yeni, Geliştirici Hizmetleri, Application Insights’ı seçin.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="f48fc-125">*Hala sorularınız mı var?*</span><span class="sxs-lookup"><span data-stu-id="f48fc-125">*Questions already?*</span></span> <span data-ttu-id="f48fc-126">[Kaynak oluşturma hakkında daha fazla bilgi](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f48fc-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="f48fc-127">Merhaba SDK komut dosyası tooyour uygulama ya da web sayfalarına ekleme</span><span class="sxs-lookup"><span data-stu-id="f48fc-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="f48fc-128">Hızlı Başlangıç'ta web sayfaları için hello betik alın:</span><span class="sxs-lookup"><span data-stu-id="f48fc-128">In Quick Start, get hello script for web pages:</span></span>

![Uygulama genel bakış dikey pencerenizde, Hızlı Başlat'ı seçin, web sayfalarımı kod toomonitor alın.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="f48fc-131">Merhaba hemen önce Hello komut dosyası Ekle `</head>` etiketi her sayfada tootrack istiyor.</span><span class="sxs-lookup"><span data-stu-id="f48fc-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="f48fc-132">Web sitenizi bir ana sayfa varsa, hello betiği buraya koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="f48fc-133">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f48fc-133">For example:</span></span>

* <span data-ttu-id="f48fc-134">ASP.NET MVC projesinde `View\Shared\_Layout.cshtml` içine koyabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="f48fc-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="f48fc-135">Bir SharePoint sitesinde hello Denetim Masası'nda açmak [Site Ayarları / ana sayfa](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="f48fc-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="f48fc-136">Hello betik hello veri tooyour Application Insights kaynağı yönlendirir hello izleme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="f48fc-137">([Hello betik daha ayrıntılı açıklaması. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="f48fc-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="f48fc-138">*(İyi bilinen web sayfası altyapısı kullanıyorsanız, Application Insights bağdaştırıcılarını araştırın. Örneğin, [AngularJS modülü](http://ngmodules.org/modules/angular-appinsights) var.)*</span><span class="sxs-lookup"><span data-stu-id="f48fc-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="f48fc-139">Ayrıntılı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f48fc-139">Detailed configuration</span></span>
<span data-ttu-id="f48fc-140">Çoğunlukla gerekmese de, ayarlayabileceğiniz birkaç [parametre](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) vardır.</span><span class="sxs-lookup"><span data-stu-id="f48fc-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="f48fc-141">Örneğin, devre dışı bırakın ya da (tooreduce trafiği) sayfa görünümü rapor edilen Ajax çağrılarını hello sayısını sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="f48fc-142">Veya toplu hale olmadan hata ayıklama modu toohave telemetri taşıma hello ardışık düzeninden hızlı bir şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="f48fc-143">tooset Bu parametreler hello kod parçacığında bu satırı arayın ve sonra virgülle ayrılmış daha fazla öğe ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f48fc-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="f48fc-144">Merhaba [kullanılabilir parametrelerin](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) içerir:</span><span class="sxs-lookup"><span data-stu-id="f48fc-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="f48fc-145"><a name="run"></a>Uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f48fc-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="f48fc-146">Web uygulamanızı çalıştırmak ve kullanacağını bir toogenerate telemetri ve bir birkaç saniye bekleyin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="f48fc-147">Her iki çalışma hello kullanarak şunları yapabilirsiniz **F5** anahtar geliştirme makinenizde yayımlayabilir ve kullanıcıların bunu yürütmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f48fc-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="f48fc-148">Bir web uygulaması tooApplication Öngörüler gönderiyor toocheck hello telemetri istiyorsanız, tarayıcınızın hata ayıklama araçlarını kullanın (**F12** birçok tarayıcılarda).</span><span class="sxs-lookup"><span data-stu-id="f48fc-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="f48fc-149">Veri toodc.services.visualstudio.com gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="f48fc-150">Tarayıcı performans verilerinizi araştırma</span><span class="sxs-lookup"><span data-stu-id="f48fc-150">Explore your browser performance data</span></span>
<span data-ttu-id="f48fc-151">Açık hello tarayıcı dikey tooshow kullanıcılarınızın tarayıcılarından performans verilerini bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![portal.azure.com adresinde uygulamanızın kaynağını açıp Ayarlar, Tarayıcı’ya tıklama](./media/app-insights-javascript/03.png)

<span data-ttu-id="f48fc-153">*Henüz veri yok mu? Tıklatın **yenileme** hello sayfanın üst kısmındaki hello. Hala hiçbir şey yok mu? Bkz. [Sorun giderme](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="f48fc-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="f48fc-154">Merhaba tarayıcı dikey penceresi bir [ölçüm Gezgini dikey](app-insights-metrics-explorer.md) hazır filtrelerin ve grafik seçimlerinin ile.</span><span class="sxs-lookup"><span data-stu-id="f48fc-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="f48fc-155">Ve hello sonucu sık kullanılan olarak kaydetmek istiyorsanız hello zaman aralığını, filtreleri ve grafik yapılandırmasını düzenleyebilir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="f48fc-156">Tıklatın **Varsayılanları Geri Yükle** tooget geri toohello asıl dikey pencere yapılandırmasına.</span><span class="sxs-lookup"><span data-stu-id="f48fc-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="f48fc-157">Sayfa yükleme performansı</span><span class="sxs-lookup"><span data-stu-id="f48fc-157">Page load performance</span></span>
<span data-ttu-id="f48fc-158">Merhaba üst kısım sayfa yükleme sürelerinin bölümlenmiş bir grafik bulunur.</span><span class="sxs-lookup"><span data-stu-id="f48fc-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="f48fc-159">Merhaba grafiğin toplam yüksekliği Hello kullanıcılarınızın tarayıcılarda uygulamanızdan hello ortalama süre tooload ve görüntü sayfaları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="f48fc-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="f48fc-160">Merhaba tarayıcı olayları, Düzen ve çalışan komut dosyaları da dahil olmak üzere işlenen tüm zaman uyumlu yük kadar hello ilk HTTP isteği gönderdiğinde hello zamandan ölçülür.</span><span class="sxs-lookup"><span data-stu-id="f48fc-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="f48fc-161">AJAX çağrılarından web bölümleri yükleme gibi zaman uyumsuz görevleri içermez.</span><span class="sxs-lookup"><span data-stu-id="f48fc-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="f48fc-162">Merhaba grafik kesim hello toplam sayfa yükleme süresi hello [W3C tarafından tanımlanan standart zamanlamalara](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="f48fc-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="f48fc-163">Bu hello Not *ağa bağlanma* zaman nedeni genellikle beklenenden daha düşük hello tarayıcı toohello sunucusundan gelen tüm istekleri üzerinden ortalama bir değer.</span><span class="sxs-lookup"><span data-stu-id="f48fc-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="f48fc-164">Zaten bir etkin bağlantı toohello sunucusu olduğundan tek tek isteklerin bağlantı süresi 0 ' var.</span><span class="sxs-lookup"><span data-stu-id="f48fc-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="f48fc-165">Yavaş mı yükleniyor?</span><span class="sxs-lookup"><span data-stu-id="f48fc-165">Slow loading?</span></span>
<span data-ttu-id="f48fc-166">Yavaş sayfa yüklenmesi kullanım memnuniyetsizliğinin başlıca kaynaklarından biridir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="f48fc-167">Merhaba grafik yavaş sayfa yüklemeleri gösteriyorsa, kolay toodo olan bazı tanılama araştırmalarını.</span><span class="sxs-lookup"><span data-stu-id="f48fc-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="f48fc-168">Merhaba grafik uygulamanızda hello tüm sayfa yüklerinin ortalamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="f48fc-169">Merhaba sorun toosee tooparticular sayfaları, daha fazla hello dikey penceresini aşağı görünüm sınırlı, tarafından bölümlenmiş kılavuzun bulunduğu sayfası URL'si:</span><span class="sxs-lookup"><span data-stu-id="f48fc-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="f48fc-170">Merhaba sayfa görünümü sayısına ve standart sapmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="f48fc-171">Ardından Hello sayfa sayısı çok azsa hello sorun kullanıcıları çok etkilemez.</span><span class="sxs-lookup"><span data-stu-id="f48fc-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="f48fc-172">Yüksek bir standart sapma (karşılaştırılabilir toohello ortalama kendisini) çok sayıda tek tek ölçüler arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="f48fc-173">**Tek URL’yi ve tek sayfa görünümünü yakınlaştırma.**</span><span class="sxs-lookup"><span data-stu-id="f48fc-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="f48fc-174">Tüm sayfa adı toosee tarayıcı grafikleri filtrelenmez yalnızca toothat URL dikey tıklayın; ve daha sonra bir sayfa görünümü örneği üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f48fc-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="f48fc-175">Tıklatın `...` bu olay için özelliklerin tam listesi için veya hello Ajax çağrılarını ve bağlantılı etkinlikleri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="f48fc-176">Yavaş Ajax çağrıları etkileyen hello genel sayfa yükleme süresi zaman uyumlu olmaları durumunda.</span><span class="sxs-lookup"><span data-stu-id="f48fc-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="f48fc-177">İlgili olaylar hello için sunucu isteklerini içerir (web sunucunuza Application Insights'ı ayarladıysanız) aynı URL.</span><span class="sxs-lookup"><span data-stu-id="f48fc-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="f48fc-178">**Zaman içerisinde performans sayfası.**</span><span class="sxs-lookup"><span data-stu-id="f48fc-178">**Page performance over time.**</span></span> <span data-ttu-id="f48fc-179">Belirli zamanlarda yükselme olup geri hello tarayıcılar dikey penceresine, hello sayfa görünümü yükleme süresi kılavuzunu çizgi grafiği toosee değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f48fc-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Merhaba head hello kılavuzunun tıklayın ve yeni bir grafik türü seçin](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="f48fc-181">**Diğer boyutlara göre bölme.**</span><span class="sxs-lookup"><span data-stu-id="f48fc-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="f48fc-182">Belki de sayfalarınızın yavaş tooload üzerinde belirli bir tarayıcı, istemci işletim sistemi veya kullanıcı yer misiniz?</span><span class="sxs-lookup"><span data-stu-id="f48fc-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="f48fc-183">Yeni bir grafik ekleyin ve hello ile denemeler **Group by** boyut.</span><span class="sxs-lookup"><span data-stu-id="f48fc-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="f48fc-184">AJAX Performansı</span><span class="sxs-lookup"><span data-stu-id="f48fc-184">AJAX Performance</span></span>
<span data-ttu-id="f48fc-185">Web sayfalarınızda AJAX çağrılarının iyi iş çıkardığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f48fc-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="f48fc-186">Bunlar genellikle kullanılan toofill sayfanızı zaman uyumsuz olarak bölümlerdir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="f48fc-187">Merhaba genel sayfa hemen yüklenebilse de, kullanıcılarınızın boş web bölümlerine bakıp burada veri tooappear bunlara bekleniyor kırıklığına uğrayabilirler.</span><span class="sxs-lookup"><span data-stu-id="f48fc-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="f48fc-188">Web sayfasından oluşturulan AJAX çağrıları hello tarayıcılar dikey penceresinde bağımlılıklar olarak gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="f48fc-189">Merhaba dikey pencerenin üst kısmındaki hello Özet grafikleri vardır:</span><span class="sxs-lookup"><span data-stu-id="f48fc-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="f48fc-190">daha aşağıda da ayrıntılı kılavuzlar:</span><span class="sxs-lookup"><span data-stu-id="f48fc-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="f48fc-191">Belirli ayrıntılar için herhangi bir satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="f48fc-192">Merhaba dikey penceresinde hello tarayıcılar filtresini silerseniz, bu grafiklere hem sunucu hem de AJAX bağımlılıkları eklenir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="f48fc-193">Tooreconfigure hello filtre Varsayılanları Geri Yükle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="f48fc-194">**başarısız Ajax çağrılarını içine toodrill** toohello bağımlılık hataları kılavuzuna kaydırın ve satır toosee belirli örnekleri'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="f48fc-195">Tıklatın `...` hello tam telemetri için bir Ajax çağrısı için.</span><span class="sxs-lookup"><span data-stu-id="f48fc-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="f48fc-196">Hiç Ajax çağrısı bildirilmedi mi?</span><span class="sxs-lookup"><span data-stu-id="f48fc-196">No Ajax calls reported?</span></span>
<span data-ttu-id="f48fc-197">Web sayfanızın hello betikten yapılan tüm HTTP/HTTPS çağrıları AJAX çağrılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="f48fc-198">Bunların bildirildiğini görmüyorsanız, bu hello kod parçacığını hello ayarlanmış değil denetlemek `disableAjaxTracking` veya `maxAjaxCallsPerView` [parametreleri](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="f48fc-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="f48fc-199">Tarayıcı özel durumları</span><span class="sxs-lookup"><span data-stu-id="f48fc-199">Browser exceptions</span></span>
<span data-ttu-id="f48fc-200">Merhaba tarayıcılar dikey penceresinde, bir özel durum Özet grafiği ve özel durum türleri daha fazla hello dikey penceresini aşağı oluşan bir kılavuz yoktur.</span><span class="sxs-lookup"><span data-stu-id="f48fc-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="f48fc-201">Tarayıcı özel durumlarının bildirildiğini görmüyorsanız, bu hello kod parçacığını hello ayarlanmış değil denetlemek `disableExceptionTracking` [parametresi](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="f48fc-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="f48fc-202">Tek tek sayfa görünümü etkinliklerini inceleme</span><span class="sxs-lookup"><span data-stu-id="f48fc-202">Inspect individual page view events</span></span>

<span data-ttu-id="f48fc-203">Sayfa görünümü telemetrisi çoğunlukla Application Insights tarafından analiz edilir; yalnızca birikmeli raporları, tüm kullanıcıların ortalamasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="f48fc-204">Ancak, hata ayıklama amacıyla tek tek sayfa görünümü etkinliklerine de bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="f48fc-205">Merhaba tanılama Ara dikey penceresinde filtreleri tooPage görünümü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="f48fc-206">Tüm olay toosee daha fazla ayrıntı seçin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-206">Select any event toosee more detail.</span></span> <span data-ttu-id="f48fc-207">Merhaba Ayrıntılar sayfasında "..." toosee daha fazla ayrıntı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f48fc-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="f48fc-208">Kullanırsanız [arama](app-insights-diagnostic-search.md), toomatch tam sözcükleri özen gösterin: "Abou" ve "bout girişleri" eşleşmiyor "About".</span><span class="sxs-lookup"><span data-stu-id="f48fc-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="f48fc-209">Ayrıca hello güçlü kullanabilirsiniz [günlük analizi sorgu dili](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch sayfa görünümleri.</span><span class="sxs-lookup"><span data-stu-id="f48fc-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="f48fc-210">Sayfa görünümü özellikleri</span><span class="sxs-lookup"><span data-stu-id="f48fc-210">Page view properties</span></span>
* <span data-ttu-id="f48fc-211">**Sayfa görünümü süresi**</span><span class="sxs-lookup"><span data-stu-id="f48fc-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="f48fc-212">Varsayılan olarak, hello alır tooload hello sayfa zaman, (yardımcı dosyalar ancak Ajax çağrıları gibi hariç zaman uyumsuz görevleri dahil) istemci isteği toofull yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f48fc-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="f48fc-213">Ayarlarsanız `overridePageViewDuration` hello içinde [sayfa Yapılandırması](#detailed-configuration), istemci isteği tooexecution Merhaba, aralığını ilk hello `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="f48fc-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="f48fc-214">Merhaba betik hello başlatma sonra normal konumundan trackPageView taşındıysa, farklı bir değer yansıtır.</span><span class="sxs-lookup"><span data-stu-id="f48fc-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="f48fc-215">Varsa `overridePageViewDuration` ayarlanır ve bağımsız değişkeni hello sağlanan süre `trackPageView()` çağrısı hello bağımsız değişken değeri yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f48fc-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="f48fc-216">Özel sayfa sayıları</span><span class="sxs-lookup"><span data-stu-id="f48fc-216">Custom page counts</span></span>
<span data-ttu-id="f48fc-217">Varsayılan olarak, yeni bir sayfa hello istemci tarayıcısına her yüklenişinde bir sayfa sayısı oluşur.</span><span class="sxs-lookup"><span data-stu-id="f48fc-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="f48fc-218">Ancak toocount ek sayfa görünümlerini isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f48fc-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="f48fc-219">Örneğin, bir sayfa içeriğini sekmelerde görüntüleyebilir ve hello kullanıcı sekmeler arasında geçiş yaptığında toocount bir sayfa istiyor.</span><span class="sxs-lookup"><span data-stu-id="f48fc-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="f48fc-220">Veya JavaScript kodu hello sayfasındaki hello tarayıcının URL'sini değiştirmeden yeni içerik yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="f48fc-221">İstemci kodunuzda hello uygun noktada gibi JavaScript çağrısı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f48fc-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="f48fc-222">Merhaba sayfa adı, URL olarak ancak "#" sonra hepsi aynı karakterleri hello içerebilir veya "?" göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="f48fc-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="f48fc-223">Kullanımı izleme</span><span class="sxs-lookup"><span data-stu-id="f48fc-223">Usage tracking</span></span>
<span data-ttu-id="f48fc-224">Uygulamanızla kullanıcılarınızın neler çıkışı toofind istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="f48fc-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="f48fc-225">Kullanımı izleme hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="f48fc-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="f48fc-226">[Özel etkinlikler ve ölçüm API’si hakkında bilgi edinin](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f48fc-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="f48fc-227"><a name="video"></a> Video</span><span class="sxs-lookup"><span data-stu-id="f48fc-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="f48fc-228"><a name="next"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f48fc-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="f48fc-229">Kullanımı izleme</span><span class="sxs-lookup"><span data-stu-id="f48fc-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="f48fc-230">Özel etkinlikler ve ölçümler</span><span class="sxs-lookup"><span data-stu-id="f48fc-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="f48fc-231">Build-measure-learn</span><span class="sxs-lookup"><span data-stu-id="f48fc-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

