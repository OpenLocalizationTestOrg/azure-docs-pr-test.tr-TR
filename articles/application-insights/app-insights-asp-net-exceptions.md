---
title: "aaaDiagnose hataları ve özel durumları web uygulamaları Azure Application Insights ile | Microsoft Docs"
description: "ASP.NET uygulamaları isteği telemetri ile birlikte özel durumları yakalar."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="6d686-103">Web uygulamalarınızı Application Insights ile özel durumları tanılama</span><span class="sxs-lookup"><span data-stu-id="6d686-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="6d686-104">Özel durumlar, canlı web uygulamanızda tarafından bildirilen [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d686-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="6d686-105">Böylece hızla hello nedenler tanılamak özel durumlar ve diğer olayları hello istemci ve sunucu, başarısız olan istekler ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d686-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="6d686-106">Set up reporting özel durumu</span><span class="sxs-lookup"><span data-stu-id="6d686-106">Set up exception reporting</span></span>
* <span data-ttu-id="6d686-107">Sunucu uygulamanızdan bildirilen toohave özel durumlar:</span><span class="sxs-lookup"><span data-stu-id="6d686-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="6d686-108">Yükleme [Application Insights SDK'sı](app-insights-asp-net.md) , uygulama kodunuzda veya</span><span class="sxs-lookup"><span data-stu-id="6d686-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="6d686-109">IIS web sunucuları: çalıştırmak [Application Insights Aracısı](app-insights-monitor-performance-live-website-now.md); veya</span><span class="sxs-lookup"><span data-stu-id="6d686-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="6d686-110">Azure web uygulamaları: hello eklemek [uygulama Öngörüler uzantısı](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="6d686-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="6d686-111">Java web uygulamaları: yükleme hello [Java aracı](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="6d686-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="6d686-112">Merhaba yüklemek [JavaScript kod parçacığı](app-insights-javascript.md) , web sayfaları toocatch tarayıcı özel durumlarda.</span><span class="sxs-lookup"><span data-stu-id="6d686-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="6d686-113">Bazı uygulama çerçeveleri veya bazı ayarlar ile bazı ek adımlar toocatch tootake gereken daha fazla özel durum:</span><span class="sxs-lookup"><span data-stu-id="6d686-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="6d686-114">Web formları</span><span class="sxs-lookup"><span data-stu-id="6d686-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="6d686-115">MVC</span><span class="sxs-lookup"><span data-stu-id="6d686-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="6d686-116">Web API 1.*</span><span class="sxs-lookup"><span data-stu-id="6d686-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="6d686-117">Web API 2.*</span><span class="sxs-lookup"><span data-stu-id="6d686-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="6d686-118">WCF</span><span class="sxs-lookup"><span data-stu-id="6d686-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="6d686-119">Visual Studio kullanarak tanılama özel durumlar</span><span class="sxs-lookup"><span data-stu-id="6d686-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="6d686-120">Hata ayıklama ile Visual Studio toohelp Hello uygulama çözümü açın.</span><span class="sxs-lookup"><span data-stu-id="6d686-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="6d686-121">Merhaba uygulama sunucunuzda veya geliştirme makinenizde F5 kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6d686-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="6d686-122">Visual Studio'da Hello uygulama Insights arama penceresi açın ve uygulamanızdan toodisplay olayları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6d686-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="6d686-123">Hatalarını ayıkladığınız sırada yalnızca hello Application Insights düğmesine tıklayarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d686-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Merhaba projesine sağ tıklayın ve Application Insights seçme açın.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="6d686-125">Merhaba rapor tooshow yalnızca özel durumlar filtreleyebilirsiniz dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6d686-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="6d686-126">*Özel durumlar gösteren? Bkz: [özel durumları yakalama](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="6d686-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="6d686-127">Bir özel durum raporu tooshow Yığın İzleme'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6d686-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="6d686-128">Merhaba yığın izlemesi, tooopen hello ilgili kod dosyası satırı başvurusunda'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6d686-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="6d686-129">Merhaba kodda CodeLens hello özel durumlar hakkında veri gösterdiğine dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="6d686-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![Özel durumlar CodeLens bildirimi.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="6d686-131">Hello Azure portal kullanarak hataları tanılama</span><span class="sxs-lookup"><span data-stu-id="6d686-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="6d686-132">Merhaba Application Insights genel bakış, uygulamanızın hello hatalar kutucuğuna özel durumlar grafiklerini gösterir ve HTTP isteklerini hello listesini birlikte hello en sık rastlanan hatalarına neden URL'leri isteği başarısız.</span><span class="sxs-lookup"><span data-stu-id="6d686-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Ayarları, hataları seçin](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="6d686-134">Merhaba birini geçişli tıklatma burada hello ayrıntıları görmek ve izleme yığın hello özel durum, özel durum türleri hello listesi tooget tooindividual oluşum içinde başarısız oldu:</span><span class="sxs-lookup"><span data-stu-id="6d686-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Başarısız bir istek ve özel durum ayrıntıları altında bir örnek seçin, hello özel durum tooinstances Al.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="6d686-136">**Alternatif olarak,** istekleri hello listesinden başlama ve özel durumları ilgili tooit bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d686-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="6d686-137">*Özel durumlar gösteren? Bkz: [özel durumları yakalama](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="6d686-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="6d686-138">Özel İzleme ve günlük verileri</span><span class="sxs-lookup"><span data-stu-id="6d686-138">Custom tracing and log data</span></span>
<span data-ttu-id="6d686-139">tooget tanılama veri belirli tooyour uygulama, kod toosend ekleyebilirsiniz kendi telemetri verileri.</span><span class="sxs-lookup"><span data-stu-id="6d686-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="6d686-140">Bu tanılama arama hello isteğinin, sayfa görünümü ve diğer otomatik olarak toplanan verileri yanında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6d686-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="6d686-141">Birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="6d686-141">You have several options:</span></span>

* <span data-ttu-id="6d686-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) genellikle hello gönderdiği ayrıca veri tanılama Arama'da özel olayları altında görünür ancak kullanım desenlerini izlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6d686-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="6d686-143">Olayları adlandırılır ve dize özellikleri ve üzerinde yapabilecekleriniz sayısal ölçümleri taşıyabilir [tanılama aramalarınız filtre](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="6d686-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="6d686-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) POST bilgileri gibi daha uzun veri göndermesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d686-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="6d686-145">[TrackException()](#exceptions) yığın izlemeler gönderir.</span><span class="sxs-lookup"><span data-stu-id="6d686-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="6d686-146">[Özel durumlar hakkında daha fazla](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="6d686-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="6d686-147">Log4Net veya NLog gibi günlük framework kullanırsanız, yapabilecekleriniz [Bu günlükleri yakalama](app-insights-asp-net-trace-logs.md) ve bunları istek ve özel durum verilerin yanında tanılama arama bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="6d686-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="6d686-148">Bu olaylar toosee açmak [arama](app-insights-diagnostic-search.md)filtre açın ve ardından özel olay, izleme veya özel durumu seçin.</span><span class="sxs-lookup"><span data-stu-id="6d686-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Detaylandırma](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="6d686-150">Uygulamanız çok sayıda telemetri oluşturuyorsa hello Uyarlamalı örnekleme modülü olayların yalnızca bir temsilci fraksiyonunu göndererek toohello portal gönderilen hello birim otomatik olarak azaltır.</span><span class="sxs-lookup"><span data-stu-id="6d686-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="6d686-151">Aynı işlemi seçili veya bir grup olarak işaretli hello parçası olan ve böylece ilgili olaylar arasında gezinebilirsiniz olaylar.</span><span class="sxs-lookup"><span data-stu-id="6d686-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="6d686-152">Örnekleme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6d686-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="6d686-153">Nasıl toosee isteği gönderme verisi</span><span class="sxs-lookup"><span data-stu-id="6d686-153">How toosee request POST data</span></span>
<span data-ttu-id="6d686-154">İstek Ayrıntıları tooyour uygulama bir POST çağrısında gönderilen hello veri eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="6d686-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="6d686-155">Bu veriler bildirdiği toohave:</span><span class="sxs-lookup"><span data-stu-id="6d686-155">toohave this data reported:</span></span>

* <span data-ttu-id="6d686-156">[Merhaba SDK yükleme](app-insights-asp-net.md) uygulama projenizdeki.</span><span class="sxs-lookup"><span data-stu-id="6d686-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="6d686-157">Kod, uygulama toocall ekleme [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="6d686-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="6d686-158">Merhaba gönderme verisi hello ileti parametresinde gönderin.</span><span class="sxs-lookup"><span data-stu-id="6d686-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="6d686-159">Olmadığından sınırı izin verilen toohello boyutu toosend yalnızca hello gerekli verileri denemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="6d686-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="6d686-160">Başarısız bir istek incelediğinizde, ilişkili hello izlemeleri bulun.</span><span class="sxs-lookup"><span data-stu-id="6d686-160">When you investigate a failed request, find hello associated traces.</span></span>  

![Detaylandırma](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="6d686-162"><a name="exceptions"></a>Özel durumlar ve ilgili Tanılama verileri yakalama</span><span class="sxs-lookup"><span data-stu-id="6d686-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="6d686-163">İlk başta, uygulamanızda hatalarına neden tüm hello özel durumları hello portalında görmez.</span><span class="sxs-lookup"><span data-stu-id="6d686-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="6d686-164">Tarayıcı özel durumlar görürsünüz (Merhaba kullanıyorsanız [JavaScript SDK'sı](app-insights-javascript.md) web sayfalarınızda).</span><span class="sxs-lookup"><span data-stu-id="6d686-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="6d686-165">Çoğu sunucu özel durumları IIS tarafından yakalanan ve toowrite biraz kod toosee sahip olan ancak bunları.</span><span class="sxs-lookup"><span data-stu-id="6d686-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="6d686-166">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6d686-166">You can:</span></span>

* <span data-ttu-id="6d686-167">**Özel durumlar açıkça oturum** kodu özel durum işleyicileri tooreport hello durumlar ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="6d686-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="6d686-168">**Özel durumlar otomatik olarak yakalama** , ASP.NET framework yapılandırarak.</span><span class="sxs-lookup"><span data-stu-id="6d686-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="6d686-169">Merhaba gerekli eklemeleri framework'ün farklı türleri için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="6d686-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="6d686-170">Özel durumlar açıkça raporlama</span><span class="sxs-lookup"><span data-stu-id="6d686-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="6d686-171">Merhaba basit tooinsert çağrısı tooTrackException() bir özel durum işleyici içinde yoldur.</span><span class="sxs-lookup"><span data-stu-id="6d686-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="6d686-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6d686-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="6d686-173">C#</span><span class="sxs-lookup"><span data-stu-id="6d686-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="6d686-174">VB</span><span class="sxs-lookup"><span data-stu-id="6d686-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="6d686-175">Merhaba özellikleri ve ölçülerini parametreler isteğe bağlıdır, ancak için yararlı olan [filtreleme ve ekleyerek](app-insights-diagnostic-search.md) ek bilgiler.</span><span class="sxs-lookup"><span data-stu-id="6d686-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="6d686-176">Örneğin, birkaç oyunlar çalıştırabilirsiniz bir uygulamanız varsa, tüm hello özel durum raporları ilgili tooa belirli oyun bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6d686-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="6d686-177">Tooeach sözlük gibi sayıda öğe ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d686-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="6d686-178">Tarayıcı özel durumları</span><span class="sxs-lookup"><span data-stu-id="6d686-178">Browser exceptions</span></span>
<span data-ttu-id="6d686-179">Çoğu tarayıcı özel durumları raporlanır.</span><span class="sxs-lookup"><span data-stu-id="6d686-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="6d686-180">Web sayfanızın içerik teslim ağlara veya diğer etki alanından komut dosyaları içeriyorsa, komut dosyası etiketinin hello özniteliği olduğundan emin olun ```crossorigin="anonymous"```, ve hello sunucu gönderir [CORS üstbilgilerini](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="6d686-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="6d686-181">Bu tooget yığın izlemesi ve bu kaynaklardan işlenmemiş JavaScript özel durumlarının ayrıntı sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="6d686-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="6d686-182">Web formları</span><span class="sxs-lookup"><span data-stu-id="6d686-182">Web forms</span></span>
<span data-ttu-id="6d686-183">Web formları için CustomErrors ile yapılandırılmış hiçbir yeniden yönlendirmeleri olduğunda hello HTTP modülü mümkün toocollect hello özel durumlar olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6d686-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="6d686-184">Ancak etkin yeniden yönlendirmeleri varsa, aşağıdaki satırları toohello uygulama_hatası Global.asax.cs işlevinde hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6d686-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="6d686-185">(Zaten yoksa, Global.asax dosyası ekleyin.)</span><span class="sxs-lookup"><span data-stu-id="6d686-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="6d686-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="6d686-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="6d686-187">MVC</span><span class="sxs-lookup"><span data-stu-id="6d686-187">MVC</span></span>
<span data-ttu-id="6d686-188">Merhaba, [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) Yapılandırması `Off`, özel durumlar hello için kullanılabilecek sonra [HTTP modülü](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="6d686-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="6d686-189">Ancak, bu ise `RemoteOnly` (varsayılan) veya `On`, ardından hello özel durum temizlendi ve Application Insights için kullanılamaz tooautomatically topla.</span><span class="sxs-lookup"><span data-stu-id="6d686-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="6d686-190">Hello geçersiz kılarak düzeltme [System.Web.Mvc.HandleErrorAttribute sınıfı](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)ve hello farklı MVC sürümleri için aşağıda gösterildiği gibi hello geçersiz sınıf uygulama ([github kaynağına](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="6d686-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="6d686-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="6d686-191">MVC 2</span></span>
<span data-ttu-id="6d686-192">Merhaba HandleError özniteliği yeni özniteliğinizi denetleyicilerinizi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6d686-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="6d686-193">Örnek</span><span class="sxs-lookup"><span data-stu-id="6d686-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="6d686-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="6d686-194">MVC 3</span></span>
<span data-ttu-id="6d686-195">Kayıt `AiHandleErrorAttribute` Global.asax.cs genel filtre olarak:</span><span class="sxs-lookup"><span data-stu-id="6d686-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="6d686-196">Örnek</span><span class="sxs-lookup"><span data-stu-id="6d686-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="6d686-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="6d686-197">MVC 4, MVC5</span></span>
<span data-ttu-id="6d686-198">FilterConfig.cs genel filtre olarak AiHandleErrorAttribute kaydedin:</span><span class="sxs-lookup"><span data-stu-id="6d686-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="6d686-199">Örnek</span><span class="sxs-lookup"><span data-stu-id="6d686-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="6d686-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="6d686-200">Web API 1.x</span></span>
<span data-ttu-id="6d686-201">System.Web.Http.Filters.ExceptionFilterAttribute geçersiz kıl:</span><span class="sxs-lookup"><span data-stu-id="6d686-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="6d686-202">Bu geçersiz kılınan özniteliği toospecific denetleyicileri ekleme ya da hello WebApiConfig sınıfının toohello genel filtre yapılandırması eklemek:</span><span class="sxs-lookup"><span data-stu-id="6d686-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="6d686-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="6d686-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="6d686-204">Merhaba özel durum filtreleri işleyemiyor durumlarda mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="6d686-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="6d686-205">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6d686-205">For example:</span></span>

* <span data-ttu-id="6d686-206">Denetleyici oluşturucular oluşturulan özel durumları.</span><span class="sxs-lookup"><span data-stu-id="6d686-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="6d686-207">İleti işleyicileri oluşturulan özel durumları.</span><span class="sxs-lookup"><span data-stu-id="6d686-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="6d686-208">Yönlendirme sırasında oluşturulan özel durumları.</span><span class="sxs-lookup"><span data-stu-id="6d686-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="6d686-209">Yanıtın içerik serileştirilmesi sırasında oluşturulan özel durumları.</span><span class="sxs-lookup"><span data-stu-id="6d686-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="6d686-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="6d686-210">Web API 2.x</span></span>
<span data-ttu-id="6d686-211">IExceptionLogger uygulaması ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6d686-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="6d686-212">Bu toohello Hizmetleri içinde WebApiConfig ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6d686-212">Add this toohello services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="6d686-213">}</span><span class="sxs-lookup"><span data-stu-id="6d686-213">}</span></span>

[<span data-ttu-id="6d686-214">Örnek</span><span class="sxs-lookup"><span data-stu-id="6d686-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="6d686-215">Alternatif, şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="6d686-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="6d686-216">Yerine yalnızca ExceptionHandler IExceptionHandler, özel bir uygulama hello.</span><span class="sxs-lookup"><span data-stu-id="6d686-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="6d686-217">Merhaba framework koruyabilmeyi toochoose hangi yanıt iletisi toosend (Merhaba bağlantısı örneği için iptal edildiğinde değil) olduğunda bu yalnızca çağrılır</span><span class="sxs-lookup"><span data-stu-id="6d686-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="6d686-218">Her durumda değil olarak adlandırılan özel durum filtreleri (açıklandığı gibi hello bölümünde Web API'sini 1.x denetleyicilerinde yukarıdaki) -.</span><span class="sxs-lookup"><span data-stu-id="6d686-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="6d686-219">WCF</span><span class="sxs-lookup"><span data-stu-id="6d686-219">WCF</span></span>
<span data-ttu-id="6d686-220">Öznitelik genişleten ve IErrorHandler ve IServiceBehavior uygulayan bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6d686-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="6d686-221">Merhaba özniteliği toohello hizmet uygulamaları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6d686-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="6d686-222">Örnek</span><span class="sxs-lookup"><span data-stu-id="6d686-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="6d686-223">Özel durum performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="6d686-223">Exception performance counters</span></span>
<span data-ttu-id="6d686-224">Varsa [hello Application Insights aracısı yüklü](app-insights-monitor-performance-live-website-now.md) sunucunuz üzerinde bir grafik .NET tarafından ölçülür hello özel durumlara oranı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d686-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="6d686-225">Bu, işlenen ve işlenmeyen özel durumları .NET içerir.</span><span class="sxs-lookup"><span data-stu-id="6d686-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="6d686-226">Ölçüm Gezgini dikey penceresini açın, yeni bir grafik ekleyin ve seçin **özel durum oranı**, performans sayaçları altında listelenen.</span><span class="sxs-lookup"><span data-stu-id="6d686-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="6d686-227">Hello .NET framework ile özel durum sayısı hello bir zaman aralığı sayım ve hello hello aralığı uzunluğuna bölünmesi hello oranı hesaplar.</span><span class="sxs-lookup"><span data-stu-id="6d686-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="6d686-228">Merhaba Application Insights portalı tarafından TrackException raporları sayım tarafından hesaplanan hello 'özel durumları' sayısı farklı olacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6d686-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="6d686-229">Merhaba örnekleme aralıkları farklıdır ve hello SDK TrackException raporları tüm işlenen ve işlenmeyen özel durumlar için göndermez.</span><span class="sxs-lookup"><span data-stu-id="6d686-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="6d686-230">Video</span><span class="sxs-lookup"><span data-stu-id="6d686-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="6d686-231">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d686-231">Next steps</span></span>
* [<span data-ttu-id="6d686-232">REST, SQL ve diğer çağrıları toodependencies izleme</span><span class="sxs-lookup"><span data-stu-id="6d686-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="6d686-233">Sayfa yükleme sürelerinin, tarayıcı özel durumlar ve AJAX çağrıları izleme</span><span class="sxs-lookup"><span data-stu-id="6d686-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="6d686-234">İzleyici performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="6d686-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
