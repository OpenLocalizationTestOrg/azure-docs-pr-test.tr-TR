---
title: "Azure Application ınsights'ta aaaTelemetry örnekleme | Microsoft Docs"
description: "Nasıl tookeep telemetri denetimindeki hacmi hello."
services: application-insights
documentationcenter: windows
author: vgorbenko
manager: carmonm
ms.assetid: 015ab744-d514-42c0-8553-8410eef00368
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bwren
ms.openlocfilehash: e19c350d0a5f16736c100322a9922fcfbf5d7b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sampling-in-application-insights"></a><span data-ttu-id="4bd0b-103">Application Insights’ta örnekleme</span><span class="sxs-lookup"><span data-stu-id="4bd0b-103">Sampling in Application Insights</span></span>


<span data-ttu-id="4bd0b-104">Örnekleme bir özelliktir [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4bd0b-104">Sampling is a feature in [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="4bd0b-105">Bu uygulama verilerinin istatistiksel olarak doğru bir analiz korurken hello yolu tooreduce telemetri trafiği ve depolama, önerilen olur.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-105">It is hello recommended way tooreduce telemetry traffic and storage, while preserving  a statistically correct analysis of application data.</span></span> <span data-ttu-id="4bd0b-106">Böylece, tanılama araştırmalar yaparken öğeleri arasında gezinebilirsiniz hello filtre ilgili öğeleri seçer.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-106">hello filter selects items that are related, so that you can navigate between items when you are doing diagnostic investigations.</span></span>
<span data-ttu-id="4bd0b-107">Ölçüm sayıları hello Portalı'nda tooyou sunulduğunda renormalized örnekleme, herhangi bir efekt hello istatistiklerle toominimize hello tootake hesabı.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-107">When metric counts are presented tooyou in hello portal, they are renormalized tootake account of hello sampling, toominimize any effect on hello statistics.</span></span>

<span data-ttu-id="4bd0b-108">Örnekleme trafiği ve veri maliyetleri azaltır ve azaltma önlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-108">Sampling reduces traffic and data costs, and helps you avoid throttling.</span></span>

## <a name="in-brief"></a><span data-ttu-id="4bd0b-109">Kısaca:</span><span class="sxs-lookup"><span data-stu-id="4bd0b-109">In brief:</span></span>
* <span data-ttu-id="4bd0b-110">Örnekleme korur 1'de  *n*  kaydeder ve hello rest atar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-110">Sampling retains 1 in *n* records and discards hello rest.</span></span> <span data-ttu-id="4bd0b-111">Örneğin, 1, 5 olayları, % 20 örnekleme oranını korumak.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-111">For example, it might retain 1 in 5 events, a sampling rate of 20%.</span></span> 
* <span data-ttu-id="4bd0b-112">Uygulamanız çok sayıda telemetri, ASP.NET web sunucusu uygulamalarında gönderirse örnekleme otomatik olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-112">Sampling happens automatically if your application sends a lot of telemetry, in ASP.NET web server apps.</span></span>
* <span data-ttu-id="4bd0b-113">El ile ya da hello örnekleme de ayarlayabilirsiniz fiyatlandırma sayfası; hello portalını ve hello hello .config dosyasına ASP.NET SDK, tooalso hello ağ trafiğini azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-113">You can also set sampling manually, either in hello portal on hello pricing page; or in hello ASP.NET SDK in hello .config file, tooalso reduce hello network traffic.</span></span>
* <span data-ttu-id="4bd0b-114">Özel olayları günlüğe kaydedin ve toomake olayların kümesini korunur veya birlikte atılan emin emin istiyorsanız, bunlar sahip Merhaba, aynı Operationıd değeri emin olun.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-114">If you log custom events and you want toomake sure that a set of events is either retained or discarded together, make sure that they have hello same OperationId value.</span></span>
* <span data-ttu-id="4bd0b-115">Merhaba örnekleme bölen  *n*  hello özelliğinde her bir kayıttaki bildirilen `itemCount`, arama göründüğü hello kolay adı "istek sayısı" veya "olay sayısı" altında.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-115">hello sampling divisor *n* is reported in each record in hello property `itemCount`, which in Search appears under hello friendly name "request count" or "event count".</span></span> <span data-ttu-id="4bd0b-116">Örnekleme işlemi içinde olmadığında `itemCount==1`.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-116">When sampling is not in operation, `itemCount==1`.</span></span>
* <span data-ttu-id="4bd0b-117">Analitik sorguları yazma durumunda [örnekleme hesaba](app-insights-analytics-tour.md#counting-sampled-data).</span><span class="sxs-lookup"><span data-stu-id="4bd0b-117">If you write Analytics queries, you should [take account of sampling](app-insights-analytics-tour.md#counting-sampled-data).</span></span> <span data-ttu-id="4bd0b-118">Özellikle, yalnızca kayıtları sayım yerine, kullanmanız gereken `summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-118">In particular, instead of simply counting records, you should use `summarize sum(itemCount)`.</span></span>

## <a name="types-of-sampling"></a><span data-ttu-id="4bd0b-119">Örnekleme türleri</span><span class="sxs-lookup"><span data-stu-id="4bd0b-119">Types of sampling</span></span>
<span data-ttu-id="4bd0b-120">Üç alternatif örnekleme yöntemi vardır:</span><span class="sxs-lookup"><span data-stu-id="4bd0b-120">There are three alternative sampling methods:</span></span>

* <span data-ttu-id="4bd0b-121">**Uyarlamalı örnekleme** hello telemetri ASP.NET uygulamanızı hello SDK gönderilen hacmi otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-121">**Adaptive sampling** automatically adjusts hello volume of telemetry sent from hello SDK in your ASP.NET app.</span></span> <span data-ttu-id="4bd0b-122">SDK v 2.0.0-beta3 varsayılan.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-122">Default from SDK v 2.0.0-beta3.</span></span> <span data-ttu-id="4bd0b-123">Şu anda, yalnızca ASP.NET sunucu tarafı telemetri için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-123">Currently available for ASP.NET server-side telemetry only.</span></span> 
* <span data-ttu-id="4bd0b-124">**Sabit oran örnekleme** ASP.NET sunucunuzdan hem ve kullanıcılarınızın tarayıcılarından gönderilen telemetri hello hacmini azaltır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-124">**Fixed-rate sampling** reduces hello volume of telemetry sent from both your ASP.NET server and from your users' browsers.</span></span> <span data-ttu-id="4bd0b-125">Merhaba oranı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-125">You set hello rate.</span></span> <span data-ttu-id="4bd0b-126">Merhaba istemci ve sunucu kendi örnekleme eşitleyecek böylece söz konusu, arama ilgili sayfa görünümleri ve istekler arasında gezinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-126">hello client and server will synchronize their sampling so that, in Search, you can navigate between related page views and requests.</span></span>
* <span data-ttu-id="4bd0b-127">**Alım örnekleme** hello Azure portal çalışır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-127">**Ingestion sampling** works in hello Azure portal.</span></span> <span data-ttu-id="4bd0b-128">Belirlediğiniz bir hızda uygulamanızdan ulaşan hello telemetri bazıları atar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-128">It discards some of hello telemetry that arrives from your app, at a rate that you set.</span></span> <span data-ttu-id="4bd0b-129">Telemetri trafiği azaltmaz ancak içinde aylık kota tutmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-129">It doesn't reduce telemetry traffic, but helps you keep within your monthly quota.</span></span> <span data-ttu-id="4bd0b-130">Alım örnekleme büyük avantajlarından Hello uygulamanızı yeniden dağıtmadan ayarlayabilirsiniz ve tüm sunucular ve istemciler için aynı şekilde çalışır ' dir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-130">hello big advantage of ingestion sampling is that you can set it without redeploying your app, and it works uniformly for all servers and clients.</span></span> 

<span data-ttu-id="4bd0b-131">Bağdaşık veya sabit oranı örnekleme işlemi yoksa alım örnekleme devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-131">If Adaptive or Fixed rate sampling are in operation, Ingestion sampling is disabled.</span></span>

## <a name="ingestion-sampling"></a><span data-ttu-id="4bd0b-132">Alım örnekleme</span><span class="sxs-lookup"><span data-stu-id="4bd0b-132">Ingestion sampling</span></span>
<span data-ttu-id="4bd0b-133">Bu biçimi örnekleme, burada web sunucusu, tarayıcılar ve cihazlar hello telemetrisini hello Application Insights Hizmeti uç noktası ulaştığında hello noktada çalışır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-133">This form of sampling operates at hello point where hello telemetry from your web server, browsers, and devices reaches hello Application Insights service endpoint.</span></span> <span data-ttu-id="4bd0b-134">Uygulamanızdan gönderilen hello telemetri trafiği azaltmaz ancak hello miktarını azaltmak işlenen ve korunur (ve için sizden ücret) Application Insights tarafından.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-134">Although it doesn't reduce hello telemetry traffic sent from your app, it does reduce hello amount processed and retained (and charged for) by Application Insights.</span></span>

<span data-ttu-id="4bd0b-135">Bu tür örnekleme uygulamanızı genellikle aylık kotasına gider ve hello SDK tabanlı türleri örnekleme birini kullanarak hello seçeneği yoksa kullanın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-135">Use this type of sampling if your app often goes over its monthly quota and you don't have hello option of using either of hello SDK-based types of sampling.</span></span> 

<span data-ttu-id="4bd0b-136">Merhaba örnekleme hızını hello kotalar ve fiyatlandırma dikey ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4bd0b-136">Set hello sampling rate in hello Quotas and Pricing blade:</span></span>

![Merhaba uygulama genel bakış dikey penceresinden ayarları, kota, örnekleri, tıklatın ardından örnekleme hızını seçin ve Güncelleştir'i tıklatın.](./media/app-insights-sampling/04.png)

<span data-ttu-id="4bd0b-138">Örnekleme diğer türleri gibi ilgili telemetri öğeleri hello algoritması korur.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-138">Like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="4bd0b-139">Aramadaki hello telemetri incelerken, örneğin, size kullanabileceksiniz toofind hello isteği ilgili tooa belirli özel durum.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-139">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> <span data-ttu-id="4bd0b-140">Ölçüm isteği hızı gibi sayar ve özel durum oranı doğru korunur.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-140">Metric counts such as request rate and exception rate are correctly retained.</span></span>

<span data-ttu-id="4bd0b-141">Örnekleme tarafından atılan veri noktaları kullanılamıyor herhangi bir Application Insights özellik gibi [sürekli verme](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="4bd0b-141">Data points that are discarded by sampling are not available in any Application Insights feature such as [Continuous Export](app-insights-export-telemetry.md).</span></span>

<span data-ttu-id="4bd0b-142">SDK tabanlı uyarlamalı veya sabit oranı örnekleme çalışıyorken alım örnekleme çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-142">Ingestion sampling doesn't operate while SDK-based adaptive or fixed-rate sampling is in operation.</span></span> <span data-ttu-id="4bd0b-143">Merhaba SDK Hello örnekleme Oranı % 100'den az ise, ardından hello ayarladığınız alım örnekleme oranını göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-143">If hello sampling rate at hello SDK is less than 100%, then hello ingestion sampling rate that you set is ignored.</span></span>

> [!WARNING]
> <span data-ttu-id="4bd0b-144">Merhaba kutucuğu gösterilen hello değere alım örnekleme için ayarladığınız hello değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-144">hello value shown on hello tile indicates hello value that you set for ingestion sampling.</span></span> <span data-ttu-id="4bd0b-145">SDK örnekleme işlemiyse hello gerçek örnekleme oranını temsil etmez.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-145">It doesn't represent hello actual sampling rate if SDK sampling is in operation.</span></span>
> 
> 

## <a name="adaptive-sampling-at-your-web-server"></a><span data-ttu-id="4bd0b-146">Web sunucunuzdaki Uyarlamalı örnekleme</span><span class="sxs-lookup"><span data-stu-id="4bd0b-146">Adaptive sampling at your web server</span></span>
<span data-ttu-id="4bd0b-147">Uyarlamalı örnekleme hello Application Insights SDK'sı ASP.NET v 2.0.0-beta3 ve sonraki sürümleri için kullanılabilir ve varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-147">Adaptive sampling is available for hello Application Insights SDK for ASP.NET v 2.0.0-beta3 and later, and is enabled by default.</span></span> 

<span data-ttu-id="4bd0b-148">Uyarlamalı örnekleme, web sunucusu uygulama toohello Application Insights hizmeti gönderilen telemetri hello hacmi etkiler.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-148">Adaptive sampling affects hello volume of telemetry sent from your web server app toohello Application Insights service.</span></span> <span data-ttu-id="4bd0b-149">Merhaba birimi otomatik olarak düzeltilir tookeep trafiğinin belirtilen maksimum oranını içinde.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-149">hello volume is adjusted automatically tookeep within a specified maximum rate of traffic.</span></span>

<span data-ttu-id="4bd0b-150">Bu telemetrinin, düşük birimlerinin hata ayıklama, bir uygulama şekilde çalışmaz veya bir Web sitesi düşük kullanımı ile etkilenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-150">It doesn't operate at low volumes of telemetry, so an app in debugging or a website with low usage won't be affected.</span></span>

<span data-ttu-id="4bd0b-151">tooachieve hello hedef birim, oluşturulan hello telemetri bazıları göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-151">tooachieve hello target volume, some of hello telemetry generated is discarded.</span></span> <span data-ttu-id="4bd0b-152">Ancak, diğer örnekleme türleri gibi hello algoritması ilgili telemetri öğeleri korur.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-152">But like other types of sampling, hello algorithm retains related telemetry items.</span></span> <span data-ttu-id="4bd0b-153">Aramadaki hello telemetri incelerken, örneğin, size kullanabileceksiniz toofind hello isteği ilgili tooa belirli özel durum.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-153">For example, when you're inspecting hello telemetry in Search, you'll be able toofind hello request related tooa particular exception.</span></span> 

<span data-ttu-id="4bd0b-154">Böylece bunlar yaklaşık doğru değerlerin ölçüm Gezgininde Göster istek hızı ve özel durum oranı oranı, örnekleme hello için ayarlanan toocompensate gibi ölçüm sayar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-154">Metric counts such as request rate and exception rate are adjusted toocompensate for hello sampling rate, so that they show approximately correct values in Metric Explorer.</span></span>

<span data-ttu-id="4bd0b-155">**Projenizin NuGet güncelleştirme** toohello son paketleri *yayın öncesi* Application Insights sürümü: hello Çözüm Gezgini'nde projeye sağ tıklayın, NuGet paketlerini Yönet seçin denetleyin **Ekle yayın öncesi** ve Microsoft.applicationınsights.Web arayın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-155">**Update your project's NuGet** packages toohello latest *pre-release* version of Application Insights: Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 

<span data-ttu-id="4bd0b-156">İçinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), hello çeşitli parametreleri ayarlayabileceğiniz `AdaptiveSamplingTelemetryProcessor` düğümü.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-156">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), you can adjust several parameters in hello `AdaptiveSamplingTelemetryProcessor` node.</span></span> <span data-ttu-id="4bd0b-157">gösterilen hello rakamları hello varsayılan değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4bd0b-157">hello figures shown are hello default values:</span></span>

* `<MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>`
  
    <span data-ttu-id="4bd0b-158">Merhaba Uyarlamalı algoritması hello hedef hızı için amaçlar **her sunucu ana bilgisayarda**.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-158">hello target rate that hello adaptive algorithm aims for **on each server host**.</span></span> <span data-ttu-id="4bd0b-159">Web uygulamanızı pek çok ana bilgisayarda çalışıyorsa, bu değer, hedef hello Application Insights portalındaki trafiğinin oranını içinde tooremain olarak şekilde azaltın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-159">If your web app runs on many hosts, reduce this value so as tooremain within your target rate of traffic at hello Application Insights portal.</span></span>
* `<EvaluationInterval>00:00:15</EvaluationInterval>` 
  
    <span data-ttu-id="4bd0b-160">Merhaba aralığı sırasında hangi hello telemetri geçerli hızı yeniden değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-160">hello interval at which hello current rate of telemetry is re-evaluated.</span></span> <span data-ttu-id="4bd0b-161">Değerlendirme hareketli ortalama gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-161">Evaluation is performed as a moving average.</span></span> <span data-ttu-id="4bd0b-162">Telemetrinizi zararlardan toosudden WINS'e ise bu aralığı tooshorten isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-162">You might want tooshorten this interval if your telemetry is liable toosudden bursts.</span></span>
* `<SamplingPercentageDecreaseTimeout>00:02:00</SamplingPercentageDecreaseTimeout>`
  
    <span data-ttu-id="4bd0b-163">Örnekleme yüzdesi değeri, ne zaman sonra değişir, biz toocapture veri daha az yüzdesi yeniden örnekleme toolower izin.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-163">When sampling percentage value changes, how soon after are we allowed toolower sampling percentage again toocapture less data.</span></span>
* `<SamplingPercentageIncreaseTimeout>00:15:00</SamplingPercentageIncreaseTimeout>`
  
    <span data-ttu-id="4bd0b-164">Örnekleme yüzdesi değeri, ne zaman sonra değişir, biz yüzdesi yeniden örnekleme tooincrease toocapture izin daha fazla veri.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-164">When sampling percentage value changes, how soon after are we allowed tooincrease sampling percentage again toocapture more data.</span></span>
* `<MinSamplingPercentage>0.1</MinSamplingPercentage>`
  
    <span data-ttu-id="4bd0b-165">Yüzde örnekleme değiştikçe hello en düşük değer nedir biz tooset izin verilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-165">As sampling percentage varies, what is hello minimum value we're allowed tooset.</span></span>
* `<MaxSamplingPercentage>100.0</MaxSamplingPercentage>`
  
    <span data-ttu-id="4bd0b-166">Yüzde örnekleme değiştikçe hello en büyük değer nedir biz tooset izin verilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-166">As sampling percentage varies, what is hello maximum value we're allowed tooset.</span></span>
* `<MovingAverageRatio>0.25</MovingAverageRatio>` 
  
    <span data-ttu-id="4bd0b-167">Hareketli Ortalama hello Hello hesaplamadaki hello ağırlık toohello en son değer atanmış.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-167">In hello calculation of hello moving average, hello weight assigned toohello most recent value.</span></span> <span data-ttu-id="4bd0b-168">1'den küçük bir değere eşit tooor kullanın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-168">Use a value equal tooor less than 1.</span></span> <span data-ttu-id="4bd0b-169">Küçük değerler hello algoritması daha az reaktif toosudden değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-169">Smaller values make hello algorithm less reactive toosudden changes.</span></span>
* `<InitialSamplingPercentage>100</InitialSamplingPercentage>`
  
    <span data-ttu-id="4bd0b-170">Merhaba uygulama yalnızca başladığında atanan hello değer.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-170">hello value assigned when hello app has just started.</span></span> <span data-ttu-id="4bd0b-171">Hatalarını ayıkladığınız sırada bu azaltma yok.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-171">Don't reduce this while you're debugging.</span></span> 

* `<ExcludedTypes>Trace;Exception</ExcludedTypes>`
  
    <span data-ttu-id="4bd0b-172">Noktalı virgülle ayrılmış örneklenen toobe istemediğiniz türleri listesi.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-172">A semi-colon delimited list of types that you do not want toobe sampled.</span></span> <span data-ttu-id="4bd0b-173">Türler tanınan: bağımlılık, olay, özel durum, sayfa görünümü, istek, izleme.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-173">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="4bd0b-174">Merhaba tüm örneklerini türleri aktarılan belirtilen; belirtilmediği hello türleri örneklenen.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-174">All instances of hello specified types are transmitted; hello types that are not specified are sampled.</span></span>

* `<IncludedTypes>Request;Dependency</IncludedTypes>`
  
    <span data-ttu-id="4bd0b-175">Örneklenen toobe istediğiniz türlerini noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-175">A semi-colon delimited list of types that you want toobe sampled.</span></span> <span data-ttu-id="4bd0b-176">Türler tanınan: bağımlılık, olay, özel durum, sayfa görünümü, istek, izleme.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-176">Recognized types are: Dependency, Event, Exception, PageView, Request, Trace.</span></span> <span data-ttu-id="4bd0b-177">Merhaba türleri örneklenen belirtilen; tüm örnekleri Merhaba diğer türleri her zaman aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-177">hello specified types are sampled; all instances of hello other types will always be transmitted.</span></span>


<span data-ttu-id="4bd0b-178">**Kapalı tooswitch** Uyarlamalı örnekleme, Kaldır hello AdaptiveSamplingTelemetryProcessor applicationınsights-config düğümden.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-178">**tooswitch off** adaptive sampling, remove hello AdaptiveSamplingTelemetryProcessor node from applicationinsights-config.</span></span>

### <a name="alternative-configure-adaptive-sampling-in-code"></a><span data-ttu-id="4bd0b-179">Alternatif: Uyarlamalı örnekleme yapılandırma</span><span class="sxs-lookup"><span data-stu-id="4bd0b-179">Alternative: configure adaptive sampling in code</span></span>
<span data-ttu-id="4bd0b-180">Örnekleme hello .config dosyasına ayarlama yerine kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-180">Instead of adjusting sampling in hello .config file, you can use code.</span></span> <span data-ttu-id="4bd0b-181">Bu, toospecify hello örnekleme hızını tekrar değerlendirilir olduğunda çağrılan bir geri çağırma işlevi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-181">This allows you toospecify a callback function that is invoked whenever hello sampling rate is re-evaluated.</span></span> <span data-ttu-id="4bd0b-182">Bu kullanabilirsiniz, örneğin, hangi örnekleme hızını çıkışı toofind kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-182">You could use this, for example, toofind out what sampling rate is being used.</span></span>

<span data-ttu-id="4bd0b-183">Merhaba kaldırmak `AdaptiveSamplingTelemetryProcessor` hello .config dosyası düğümden.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-183">Remove hello `AdaptiveSamplingTelemetryProcessor` node from hello .config file.</span></span>

<span data-ttu-id="4bd0b-184">*C#*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-184">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights;
    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.Channel.Implementation;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var adaptiveSamplingSettings = new SamplingPercentageEstimatorSettings();

    // Optional: here you can adjust hello settings from their defaults.

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;

    builder.UseAdaptiveSampling(
         adaptiveSamplingSettings,

        // Callback on rate re-evaluation:
        (double afterSamplingTelemetryItemRatePerSecond,
         double currentSamplingPercentage,
         double newSamplingPercentage,
         bool isSamplingPercentageChanged,
         SamplingPercentageEstimatorSettings s
        ) =>
        {
          if (isSamplingPercentageChanged)
          {
             // Report hello sampling rate.
             telemetryClient.TrackMetric("samplingPercentage", newSamplingPercentage);
          }
      });

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="4bd0b-185">([Telemetri işlemciler hakkında daha fazla bilgi](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="4bd0b-185">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

<a name="other-web-pages"></a>

## <a name="sampling-for-web-pages-with-javascript"></a><span data-ttu-id="4bd0b-186">JavaScript web sayfaları için örnekleme</span><span class="sxs-lookup"><span data-stu-id="4bd0b-186">Sampling for web pages with JavaScript</span></span>
<span data-ttu-id="4bd0b-187">Web sayfaları için herhangi bir sunucudan sabit oranı örnekleme yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-187">You can configure web pages for fixed-rate sampling from any server.</span></span> 

<span data-ttu-id="4bd0b-188">Olduğunda, [hello web sayfaları için Application Insights yapılandırma](app-insights-javascript.md), hello Application Insights portalından aldığınız hello parçacığını değiştirmek.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-188">When you [configure hello web pages for Application Insights](app-insights-javascript.md), modify hello snippet that you get from hello Application Insights portal.</span></span> <span data-ttu-id="4bd0b-189">(ASP.NET uygulamalarında hello parçacığı genellikle _Layout.cshtml içinde gider.)  Benzer bir satır ekleyin `samplingPercentage: 10,` hello izleme anahtarını önce:</span><span class="sxs-lookup"><span data-stu-id="4bd0b-189">(In ASP.NET apps, hello snippet typically goes in _Layout.cshtml.)  Insert a line like `samplingPercentage: 10,` before hello instrumentation key:</span></span>

    <script>
    var appInsights= ... 
    }({ 


    // Value must be 100/N where N is an integer.
    // Valid examples: 50, 25, 20, 10, 5, 1, 0.1, ...
    samplingPercentage: 10, 

    instrumentationKey:...
    }); 

    window.appInsights=appInsights; 
    appInsights.trackPageView(); 
    </script> 

<span data-ttu-id="4bd0b-190">Merhaba örnekleme yüzdesi Kapat too100/N N bir tamsayı olduğu bir yüzde seçin.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-190">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="4bd0b-191">Şu anda örnekleme diğer değerleri desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-191">Currently sampling doesn't support other values.</span></span>

<span data-ttu-id="4bd0b-192">Sabit oran örnekleme hello sunucuda da etkinleştirirseniz, bu, içinde arama ilgili sayfa görünümleri ve istekler arasında gezinebilirsiniz şekilde hello istemciler ve sunucu eşitler.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-192">If you also enable fixed-rate sampling at hello server, hello clients and server will synchronize so that, in Search, you can  navigate between related page views and requests.</span></span>

## <a name="fixed-rate-sampling-for-aspnet-web-sites"></a><span data-ttu-id="4bd0b-193">ASP.NET web siteleri için sabit oranı örnekleme</span><span class="sxs-lookup"><span data-stu-id="4bd0b-193">Fixed-rate sampling for ASP.NET web sites</span></span>
<span data-ttu-id="4bd0b-194">Sabit oranı örnekleme, web sunucunuz ve web tarayıcıları gönderilen hello trafiğini azaltır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-194">Fixed rate sampling reduces hello traffic sent from your web server and web browsers.</span></span> <span data-ttu-id="4bd0b-195">Uyarlamalı örnekleme aksine, telemetri sizin tarafınızdan karar sabit bir oranda azaltır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-195">Unlike adaptive sampling, it reduces telemetry at a fixed rate decided by you.</span></span> <span data-ttu-id="4bd0b-196">İlgili öğeler - Örneğin, korunur, böylece arama sayfası görünümünde bakarsanız, ilgili isteğini bulabilmesi için aynı zamanda hello istemci ve sunucu örnekleme eşitler.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-196">It also synchronizes hello client and server sampling so that related items are retained - for example, so that if you look at a page view in Search, you can find its related request.</span></span>

<span data-ttu-id="4bd0b-197">Merhaba örnekleme algoritması ilgili öğeler korur.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-197">hello sampling algorithm retains related items.</span></span> <span data-ttu-id="4bd0b-198">Her HTTP isteği için olay, bu ve ilgili olaylar atılan aktarılan ya.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-198">For each HTTP request event, it and its related events are either discarded or transmitted.</span></span> 

<span data-ttu-id="4bd0b-199">Yaklaşık doğru; böylece ölçümleri Explorer'da faktörü toocompensate hello örnekleme hızı için istek ve özel durum sayısı gibi oranları çarpılır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-199">In Metrics Explorer, rates such as request and exception counts are multiplied by a factor toocompensate for hello sampling rate, so that they are approximately correct.</span></span>

1. <span data-ttu-id="4bd0b-200">**Projenizin NuGet paketlerini güncelleştirmeyi** son toohello *yayın öncesi* Application Insights sürümü.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-200">**Update your project's NuGet packages** toohello latest *pre-release* version of Application Insights.</span></span> <span data-ttu-id="4bd0b-201">Çözüm Gezgini'nde Hello projeye sağ tıklayın, NuGet paketlerini Yönet seçin denetleyin **dahil et** ve Microsoft.applicationınsights.Web arayın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-201">Right-click hello project in Solution Explorer, choose Manage NuGet Packages, check **Include prerelease** and search for Microsoft.ApplicationInsights.Web.</span></span> 
2. <span data-ttu-id="4bd0b-202">**Uyarlamalı örnekleme devre dışı**: içinde [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md), kaldırmak veya yorum hello `AdaptiveSamplingTelemetryProcessor` düğümü.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-202">**Disable adaptive sampling**: In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), remove or comment out hello `AdaptiveSamplingTelemetryProcessor` node.</span></span>
   
    ```xml
   
    <TelemetryProcessors>
   
    <!-- Disabled adaptive sampling:
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    -->

    ```

1. <span data-ttu-id="4bd0b-203">**Merhaba sabit oranı örnekleme modülü etkinleştirin.**</span><span class="sxs-lookup"><span data-stu-id="4bd0b-203">**Enable hello fixed-rate sampling module.**</span></span> <span data-ttu-id="4bd0b-204">Bu kod parçacığında çok eklemek[Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="4bd0b-204">Add this snippet too[ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>
   
    ```XML
   
    <TelemetryProcessors>
     <Add  Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
   
      <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
      <SamplingPercentage>10</SamplingPercentage>
      </Add>
    </TelemetryProcessors>
   
    ```

> [!NOTE]
> <span data-ttu-id="4bd0b-205">Merhaba örnekleme yüzdesi Kapat too100/N N bir tamsayı olduğu bir yüzde seçin.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-205">For hello sampling percentage, choose a percentage that is close too100/N where N is an integer.</span></span>  <span data-ttu-id="4bd0b-206">Şu anda örnekleme diğer değerleri desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-206">Currently sampling doesn't support other values.</span></span>
> 
> 

### <a name="alternative-enable-fixed-rate-sampling-in-your-server-code"></a><span data-ttu-id="4bd0b-207">Alternatif: sunucu kodunuzdaki sabit oranı örnekleme etkinleştir</span><span class="sxs-lookup"><span data-stu-id="4bd0b-207">Alternative: enable fixed-rate sampling in your server code</span></span>
<span data-ttu-id="4bd0b-208">Merhaba .config dosyasına Hello örnekleme parametre ayarı yerine kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-208">Instead of setting hello sampling parameter in hello .config file, you can use code.</span></span> 

<span data-ttu-id="4bd0b-209">*C#*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-209">*C#*</span></span>

```C#

    using Microsoft.ApplicationInsights.Extensibility;
    using Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel;
    ...

    var builder = TelemetryConfiguration.Active.GetTelemetryProcessorChainBuilder();
    builder.UseSampling(10.0); // percentage

    // If you have other telemetry processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="4bd0b-210">([Telemetri işlemciler hakkında daha fazla bilgi](app-insights-api-filtering-sampling.md#filtering).)</span><span class="sxs-lookup"><span data-stu-id="4bd0b-210">([Learn about telemetry processors](app-insights-api-filtering-sampling.md#filtering).)</span></span>

## <a name="when-toouse-sampling"></a><span data-ttu-id="4bd0b-211">Zaman toouse örnekleme?</span><span class="sxs-lookup"><span data-stu-id="4bd0b-211">When toouse sampling?</span></span>
<span data-ttu-id="4bd0b-212">Uyarlamalı örnekleme hello ASP.NET SDK sürüm 2.0.0-beta3 kullanırsanız, otomatik olarak etkinleştirilmiş veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-212">Adaptive sampling is automatically enabled if you use hello ASP.NET SDK version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="4bd0b-213">Kullandığınız hangi SDK sürümü olsun alım örnekleme (bizim sunucuda) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-213">No matter what SDK version you use, you can use ingestion sampling (at our server).</span></span>

<span data-ttu-id="4bd0b-214">En küçük ve orta ölçekli uygulamalar için örnekleme gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-214">You don’t need sampling for most small and medium size applications.</span></span> <span data-ttu-id="4bd0b-215">Merhaba en yararlı tanı bilgilerini ve en doğru istatistikleri, tüm kullanıcı etkinliklerini veri toplayarak elde edilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-215">hello most useful diagnostic information and most accurate statistics are obtained by collecting data on all your user activities.</span></span> 

<span data-ttu-id="4bd0b-216">örnekleme Hello ana avantajları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4bd0b-216">hello main advantages of sampling are:</span></span>

* <span data-ttu-id="4bd0b-217">Uygulamanızı telemetri çok yüksek oranda kısa gönderdiğinde uygulama Öngörüler hizmeti düşme ("kısıtlamaları") veri noktaları aralığı zaman.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-217">Application Insights service drops ("throttles") data points when your app sends a very high rate of telemetry in short time interval.</span></span> 
* <span data-ttu-id="4bd0b-218">Merhaba içinde tookeep [kota](app-insights-pricing.md) fiyatlandırma katmanınızı veri noktaları.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-218">tookeep within hello [quota](app-insights-pricing.md) of data points for your pricing tier.</span></span> 
* <span data-ttu-id="4bd0b-219">telemetri hello koleksiyonundan tooreduce ağ trafiği.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-219">tooreduce network traffic from hello collection of telemetry.</span></span> 

### <a name="which-type-of-sampling-should-i-use"></a><span data-ttu-id="4bd0b-220">Hangi tür örnekleme kullanmalıyım?</span><span class="sxs-lookup"><span data-stu-id="4bd0b-220">Which type of sampling should I use?</span></span>
<span data-ttu-id="4bd0b-221">**Alım varsa örnekleme kullanın:**</span><span class="sxs-lookup"><span data-stu-id="4bd0b-221">**Use ingestion sampling if:**</span></span>

* <span data-ttu-id="4bd0b-222">Genellikle, telemetri aylık kota de gidin.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-222">You often go through your monthly quota of telemetry.</span></span>
* <span data-ttu-id="4bd0b-223">Merhaba örnekleme - örneğin desteklemiyor SDK'sı, hello Java SDK'sı veya ASP.NET sürümleri sürümünü 2'den önceki kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-223">You're using a version of hello SDK that doesn't support sampling - for example, hello Java SDK or ASP.NET versions earlier than 2.</span></span>
* <span data-ttu-id="4bd0b-224">Çok sayıda telemetri kullanıcılarınızın web tarayıcılarından alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-224">You're getting a lot of telemetry from your users' web browsers.</span></span>

<span data-ttu-id="4bd0b-225">**Sabit oranı, örnekleme kullanın:**</span><span class="sxs-lookup"><span data-stu-id="4bd0b-225">**Use fixed-rate sampling if:**</span></span>

* <span data-ttu-id="4bd0b-226">ASP.NET web Hizmetleri sürüm 2.0.0 hello Application Insights SDK kullanıyorsanız veya sonraki bir sürümü ve</span><span class="sxs-lookup"><span data-stu-id="4bd0b-226">You're using hello Application Insights SDK for ASP.NET web services version 2.0.0 or later, and</span></span>
* <span data-ttu-id="4bd0b-227">Olayların ne zaman çalışıyoruz böylece istemci ve sunucu arasında eşitlenen örnekleme istediğiniz [arama](app-insights-diagnostic-search.md), hello istemcide ilgili olaylar ve sayfa görünümleri ve http isteklerini gibi sunucu arasında gezinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-227">You want synchronized sampling between client and server, so that, when you're investigating events in [Search](app-insights-diagnostic-search.md), you can navigate between related events on hello client and server, such as page views and http requests.</span></span>
* <span data-ttu-id="4bd0b-228">Uygulamanız için hello uygun örnekleme yüzdesi emin olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-228">You are confident of hello appropriate sampling percentage for your app.</span></span> <span data-ttu-id="4bd0b-229">Bunu yeterince tooget doğru ölçümler, ancak aşağıda fiyatlandırma kotayı aştığı oranı hello ve gerekir azaltma sınırları hello.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-229">It should be high enough tooget accurate metrics, but below hello rate that exceeds your pricing quota and hello throttling limits.</span></span> 

<span data-ttu-id="4bd0b-230">**Uyarlamalı örnekleme kullanın:**</span><span class="sxs-lookup"><span data-stu-id="4bd0b-230">**Use adaptive sampling:**</span></span>

<span data-ttu-id="4bd0b-231">Aksi takdirde, Uyarlamalı örnekleme öneririz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-231">Otherwise, we recommend adaptive sampling.</span></span> <span data-ttu-id="4bd0b-232">Bu hello ASP.NET sunucusu SDK sürüm 2.0.0-beta3 varsayılan olarak etkin veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-232">This is enabled by default in hello ASP.NET server SDK, version 2.0.0-beta3 or later.</span></span> <span data-ttu-id="4bd0b-233">Düşük kullanım site etkilememesi için trafiği bir belirli en düşük hızı kadar azaltmaz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-233">It doesn't reduce traffic until a certain minimum rate, so it won't affect a low-use site.</span></span>

## <a name="how-do-i-know-whether-sampling-is-in-operation"></a><span data-ttu-id="4bd0b-234">Örnekleme işlemi olup olmadığını nasıl anlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="4bd0b-234">How do I know whether sampling is in operation?</span></span>
<span data-ttu-id="4bd0b-235">Burada uygulandığından, olsun oranı örnekleme toodiscover hello gerçek kullanmak bir [Analytics sorgu](app-insights-analytics.md) bu gibi:</span><span class="sxs-lookup"><span data-stu-id="4bd0b-235">toodiscover hello actual sampling rate no matter where it has been applied, use an [Analytics query](app-insights-analytics.md) such as this:</span></span>

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

<span data-ttu-id="4bd0b-236">Her kaydı tutulur `itemCount` temsil eder, özgün kayıt eşit too1 + hello kayıt sayısı, önceki atılan hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-236">In each retained record, `itemCount` indicates hello number of original records that it represents, equal too1 + hello number of previous discarded records.</span></span> 

## <a name="how-does-sampling-work"></a><span data-ttu-id="4bd0b-237">Örnekleme nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="4bd0b-237">How does sampling work?</span></span>
<span data-ttu-id="4bd0b-238">Sabit oranı ve Uyarlamalı örnekleme hello SDK başlayarak 2.0.0 ASP.NET sürümlerden bir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-238">Fixed-rate and adaptive sampling are a feature of hello SDK in ASP.NET versions from 2.0.0 onwards.</span></span> <span data-ttu-id="4bd0b-239">Alım örnekleme hello Application Insights hizmeti, bir özelliğidir ve hello SDK örnekleme gerçekleştirmiyorsa işleminde olabilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-239">Ingestion sampling is a feature of hello Application Insights service, and can be in operation if hello SDK is not performing sampling.</span></span> 

<span data-ttu-id="4bd0b-240">hangi telemetri öğeleri toodrop ve (Merhaba SDK veya hello Application Insights hizmeti olup) hangi olanları tookeep Hello örnekleme algoritmasını belirler.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-240">hello sampling algorithm decides which telemetry items toodrop, and which ones tookeep (whether it's in hello SDK or in hello Application Insights service).</span></span> <span data-ttu-id="4bd0b-241">Merhaba örnekleme karar toopreserve tüm birbiriyle veri noktaları olduğu gibi bir işlem yapılabilir ve hatta sınırlı bir veri kümesi ile güvenilir Application Insights tanılama deneyimi koruma hedeflenir çeşitli kurallar temel alır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-241">hello sampling decision is based on several rules that aim toopreserve all interrelated data points intact, maintaining a diagnostic experience in Application Insights that is actionable and reliable even with a reduced data set.</span></span> <span data-ttu-id="4bd0b-242">Başarısız bir istek için ek telemetri öğeleri (örneğin, özel durumu ve bu istekten oturum izlemeleri) uygulamanızı gönderirse, örneğin, örnekleme bu istek ve başka telemetriyle bölecek değil.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-242">For example, if for a failed request your app sends additional telemetry items (such as exception and traces logged from this request), sampling will not split this request and other telemetry.</span></span> <span data-ttu-id="4bd0b-243">Tutar ya da hepsini bir araya bırakır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-243">It either keeps or drops them all together.</span></span> <span data-ttu-id="4bd0b-244">Sonuç olarak, Application ınsights'ta hello İstek Ayrıntıları baktığınızda, her zaman hello istekle ilişkili telemetri öğelerinden birlikte görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-244">As a result, when you look at hello request details in Application Insights, you can always see hello request along with its associated telemetry items.</span></span> 

<span data-ttu-id="4bd0b-245">"Kullanıcı" tanımlamak uygulamalar için (diğer bir deyişle, en tipik web uygulamaları), hello örnekleme karar herhangi belirli bir kullanıcı için tüm telemetri korunur veya bırakılan anlamına gelir hello kullanıcı kimliği hello karmasını dayanır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-245">For applications that define "user" (that is, most typical web applications), hello sampling decision is based on hello hash of hello user id, which means that all telemetry for any particular user is either preserved or dropped.</span></span> <span data-ttu-id="4bd0b-246">Merhaba türleri (örneğin, web Hizmetleri) kullanıcıları tanımlamak olmayan uygulamalar için hello örnekleme karar üzerinde hello isteğin hello işlemi kimliği temel alır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-246">For hello types of applications that don't define users (such as web services) hello sampling decision is based on hello operation id of hello request.</span></span> <span data-ttu-id="4bd0b-247">Son olarak, tipleri (için örnek telemetri öğeleri http bağlam ile zaman uyumsuz iş parçacıklarından bildirilen) Ayarla kullanıcı veya işlem kimliğine sahip hello telemetri öğeleri için örnekleme yalnızca her tür telemetri öğeleri yüzdesini yakalar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-247">Finally, for hello telemetry items that neither have user nor operation id set (for example telemetry items reported from asynchronous threads with no http context) sampling simply captures a percentage of telemetry items of each type.</span></span> 

<span data-ttu-id="4bd0b-248">Telemetri geri tooyou sunan, hello Application Insights hizmeti tarafından hello ölçümleri ayarlar hello zaman koleksiyonunun toocompensate veri noktaları eksik hello için kullanılan aynı örnekleme yüzdesini hello.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-248">When presenting telemetry back tooyou, hello Application Insights service adjusts hello metrics by hello same sampling percentage that was used at hello time of collection, toocompensate for hello missing data points.</span></span> <span data-ttu-id="4bd0b-249">Bu nedenle, Application ınsights'ta hello telemetri bakıldığında hello kullanıcılar için çok yakın toohello gerçek sayılar istatistiksel olarak doğru yakın görüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-249">Hence, when looking at hello telemetry in Application Insights, hello users are seeing statistically correct approximations that are very close toohello real numbers.</span></span>

<span data-ttu-id="4bd0b-250">Merhaba yaklaşık Hello doğruluğu büyük ölçüde yapılandırılmış hello örnekleme yüzdesi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-250">hello accuracy of hello approximation largely depends on hello configured sampling percentage.</span></span> <span data-ttu-id="4bd0b-251">Ayrıca, kullanıcıların çok sayıda genellikle benzer isteklerinden büyük miktarda işleyen uygulamalar için hello doğruluğu artırır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-251">Also, hello accuracy increases for applications that handle a large volume of generally similar requests from lots of users.</span></span> <span data-ttu-id="4bd0b-252">Üzerinde önemli bir yük ile çalışmıyor uygulamalar için diğer yandan Merhaba, bu uygulamalar genellikle kendi telemetri azaltma gelen veri kaybına neden olmadan hello kotanın kalsanız gönderebilirsiniz gibi örnekleme gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-252">On hello other hand, for applications that don't work with a significant load, sampling is not needed as these applications can usually send all their telemetry while staying within hello quota, without causing data loss from throttling.</span></span> 

<span data-ttu-id="4bd0b-253">Application Insights telemetri türlerini, ölçümleri ve oturumlar itibaren bu türleri için örnek değil, hello duyarlık azalma yüksek oranda istenmeyen dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-253">Note that Application Insights does not sample Metrics and Sessions telemetry types, since for these types, reduction in hello precision can be highly undesirable.</span></span> 

### <a name="adaptive-sampling"></a><span data-ttu-id="4bd0b-254">Uyarlamalı örnekleme</span><span class="sxs-lookup"><span data-stu-id="4bd0b-254">Adaptive sampling</span></span>
<span data-ttu-id="4bd0b-255">Uyarlamalı örnekleme hello SDK ' iletim izleyiciler hello geçerli hızı bir bileşen ekler ve hello örnekleme yüzde tootry toostay hello hedef en yüksek hızı içinde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-255">Adaptive sampling adds a component that monitors hello current rate of transmission from hello SDK, and adjusts hello sampling percentage tootry toostay within hello target maximum rate.</span></span> <span data-ttu-id="4bd0b-256">Merhaba ayarlama düzenli aralıklarla yeniden hesaplanır ve bir aktarım hızını giden hello hareketli ortalama üzerinde temel alır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-256">hello adjustment is recalculated at regular intervals, and is based on a moving average of hello outgoing transmission rate.</span></span>

## <a name="sampling-and-hello-javascript-sdk"></a><span data-ttu-id="4bd0b-257">Örnekleme ve hello JavaScript SDK'sı</span><span class="sxs-lookup"><span data-stu-id="4bd0b-257">Sampling and hello JavaScript SDK</span></span>
<span data-ttu-id="4bd0b-258">Sabit oran örnekleme hello sunucu tarafı birlikte Hello istemci-tarafı (JavaScript) SDK katılan SDK.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-258">hello client-side (JavaScript) SDK participates in fixed-rate sampling in conjunction with hello server-side SDK.</span></span> <span data-ttu-id="4bd0b-259">izlenmiş hello sayfaları yalnızca aynı kullanıcıların hangi hello için sunucu tarafı kendi kararı çok "içinde sample." Merhaba gelen istemci-tarafı telemetri gönderir</span><span class="sxs-lookup"><span data-stu-id="4bd0b-259">hello instrumented pages will only send client-side telemetry from hello same users for which hello server-side made its decision too"sample in."</span></span> <span data-ttu-id="4bd0b-260">Bu mantık, istemci - ve sunucu-tarafı boyunca kullanıcı oturumunun tasarlanmış toomaintain bütünlüğü içindir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-260">This logic is designed toomaintain integrity of user session across client- and server-sides.</span></span> <span data-ttu-id="4bd0b-261">Sonuç olarak, Application Insights herhangi belirli telemetri öğeden bu kullanıcıyı ya da oturumu için diğer tüm telemetri öğeleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-261">As a result, from any particular telemetry item in Application Insights you can find all other telemetry items for this user or session.</span></span> 

<span data-ttu-id="4bd0b-262">*Yukarıda açıklanan şekilde my istemci ve sunucu tarafı telemetri Eşgüdümlü örnekleri gösterme.*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-262">*My client and server-side telemetry don't show coordinated samples as you describe above.*</span></span>

* <span data-ttu-id="4bd0b-263">Sabit oran örnekleme hem de sunucu ve istemci etkin olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-263">Verify that you enabled fixed-rate sampling both on server and client.</span></span>
* <span data-ttu-id="4bd0b-264">Bu hello SDK sürüm 2.0 olduğundan emin olun veya üstü.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-264">Make sure that hello SDK version is 2.0 or above.</span></span>
* <span data-ttu-id="4bd0b-265">Ayarladığınız onay hello aynı hello istemci ve sunucu yüzde örnekleme.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-265">Check that you set hello same sampling percentage in both hello client and server.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="4bd0b-266">Sık Sorulan Sorular</span><span class="sxs-lookup"><span data-stu-id="4bd0b-266">Frequently Asked Questions</span></span>
<span data-ttu-id="4bd0b-267">*Bir basit "toplama her telemetri türü yüzdesi X" örnekleme değil neden?*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-267">*Why isn't sampling a simple "collect X percent of each telemetry type"?*</span></span>

* <span data-ttu-id="4bd0b-268">Bu örnekleme yaklaşım ölçüm yaklaşık değerler, çok yüksek duyarlılık ile sağlayacak olsa da, kullanıcı, oturum ve tanılama için önemli olan istek başına özelliği toocorrelate Tanılama verileri bölün.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-268">While this sampling approach would provide with a very high precision in metric approximations, it would break ability toocorrelate diagnostic data per user, session, and request, which is critical for diagnostics.</span></span> <span data-ttu-id="4bd0b-269">Bu nedenle, works daha iyi "tüm telemetri öğeleri için yüzde X uygulama kullanıcılarının toplamak" veya "uygulama isteklerin yüzdesi X için tüm telemetri Topla" örnekleme mantığı.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-269">Therefore, sampling works better with "collect all telemetry items for X percent of app users", or "collect all telemetry for X percent of app requests" logic.</span></span> <span data-ttu-id="4bd0b-270">(Örneğin, arka plan zaman uyumsuz işleme) hello isteklerle ilişkili olmayan hello telemetri öğeleri için hello sonbaharda geri çok "toplama her telemetri türü için tüm öğeleri yüzdesi X."</span><span class="sxs-lookup"><span data-stu-id="4bd0b-270">For hello telemetry items not associated with hello requests (such as background asynchronous processing), hello fall back is too"collect X percent of all items for each telemetry type."</span></span> 

<span data-ttu-id="4bd0b-271">*Merhaba örnekleme yüzdesi zamanla değiştirebilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-271">*Can hello sampling percentage change over time?*</span></span>

* <span data-ttu-id="4bd0b-272">Evet, Uyarlamalı örnekleme kademeli olarak hello örnekleme yüzde, şu anda hello telemetri hacmi gözlenen hello üzerinde tabanlı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-272">Yes, adaptive sampling gradually changes hello sampling percentage, based on hello currently observed volume of hello telemetry.</span></span>

<span data-ttu-id="4bd0b-273">*Sabit oran örnekleme kullanırsanız, nasıl anlarım hangi örnekleme yüzdesi çalışır hello Uygulamam için en iyi?*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-273">*If I use fixed-rate sampling, how do I know which sampling percentage will work hello best for my app?*</span></span>

* <span data-ttu-id="4bd0b-274">Uyarlamalı örnekleme ile toostart bir yoludur, üzerinde ne oranı çıkışı Bul kapatır (Merhaba soru yukarıda bakın), ve ardından anahtar toofixed hızında örnekleme hızı kullanma.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-274">One way is toostart with adaptive sampling, find out what rate it settles on (see hello above question), and then switch toofixed-rate sampling using that rate.</span></span> 
  
    <span data-ttu-id="4bd0b-275">Aksi takdirde tooguess sahip.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-275">Otherwise, you have tooguess.</span></span> <span data-ttu-id="4bd0b-276">Geçerli telemetri kullanımınızı AI çözümlemek, herhangi diğer bir deyişle gerçekleşen ve hello toplanan telemetri hello hacmini tahmin azaltma inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-276">Analyze your current telemetry usage in AI, observe any throttling that is occurring, and estimate hello volume of hello collected telemetry.</span></span> <span data-ttu-id="4bd0b-277">Seçilen fiyatlandırma katmanınızı birlikte bu üç girişleri tooreduce hello hello toplanan telemetri hacmi ne kadar isteyebilirsiniz öneririz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-277">These three inputs, together with your selected pricing tier, suggest how much you might want tooreduce hello volume of hello collected telemetry.</span></span> <span data-ttu-id="4bd0b-278">Ancak, kullanıcılarınızın hello sayısı artan ya da diğer bazı shift telemetri hello birimindeki, tahmin geçersiz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-278">However, an increase in hello number of your users or some other shift in hello volume of telemetry might invalidate your estimate.</span></span>

<span data-ttu-id="4bd0b-279">*Örnekleme yüzdesi çok düşük yapılandırırsanız ne olur?*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-279">*What happens if I configure sampling percentage too low?*</span></span>

* <span data-ttu-id="4bd0b-280">Application Insights toocompensate hello görselleştirme hello veri birimi azaltılması için hello verilerin çalıştığında aşırı düşük örnekleme yüzdesi (over-aggressive örnekleme) hello yakın hello doğruluğunu azaltır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-280">Excessively low sampling percentage (over-aggressive sampling) reduces hello accuracy of hello approximations, when Application Insights attempts toocompensate hello visualization of hello data for hello data volume reduction.</span></span> <span data-ttu-id="4bd0b-281">Ayrıca, tanılama deneyimi olumsuz, bazı sık başarısız hello etkilenebilir veya yavaş istekler çıkışı örneklenebilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-281">Also, diagnostic experience might be negatively impacted, as some of hello infrequently failing or slow requests may be sampled out.</span></span>

<span data-ttu-id="4bd0b-282">*Örnekleme yüzdesi çok yüksek yapılandırırsanız ne olur?*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-282">*What happens if I configure sampling percentage too high?*</span></span>

* <span data-ttu-id="4bd0b-283">Merhaba hello hacmi yetersiz bir düşüş yapılandırma çok yüksek örnekleme yüzdesi (değil agresif yeterince) sonuçlarında telemetri toplanır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-283">Configuring too high sampling percentage (not aggressive enough) results in an insufficient reduction in hello volume of hello collected telemetry.</span></span> <span data-ttu-id="4bd0b-284">Veri kaybı toothrottling ve Application Insights kullanma maliyetini Merhaba, toooverage ücretleri planlanan daha yüksek olabilir ilgili telemetri hala karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-284">You may still experience telemetry data loss related toothrottling, and hello cost of using Application Insights might be higher than you planned due toooverage charges.</span></span>

<span data-ttu-id="4bd0b-285">*Hangi platformlarda örnekleme kullanabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-285">*On what platforms can I use sampling?*</span></span>

* <span data-ttu-id="4bd0b-286">Merhaba SDK örnekleme gerçekleştirmiyor alım örnekleme otomatik olarak belirli bir birim üzerinde herhangi bir telemetri için ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-286">Ingestion sampling can occur automatically for any telemetry above a certain volume, if hello SDK is not performing sampling.</span></span> <span data-ttu-id="4bd0b-287">Bu, örneğin, uygulamanız Java sunucusu kullanıyorsa ya da hello ASP.NET SDK daha eski bir sürümü kullanıyorsanız çalışır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-287">This would work, for example, if your app uses a Java server, or if you are using an older version of hello ASP.NET SDK.</span></span>
* <span data-ttu-id="4bd0b-288">ASP.NET SDK sürüm 2.0.0 kullanıyorsanız ve üstünde (Azure veya kendi sunucusunda barındırılan), Uyarlamalı örnekleme varsayılan olarak alır ancak yukarıda açıklandığı gibi toofixed oranı geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-288">If you're using ASP.NET SDK versions 2.0.0 and above (hosted either in Azure or on your own server), you get adaptive sampling by default, but you can switch toofixed-rate as described above.</span></span> <span data-ttu-id="4bd0b-289">Sabit oran örnekleme ile Merhaba tarayıcı SDK toosample otomatik olarak eşitleyen ilgili olaylar.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-289">With fixed-rate sampling, hello browser SDK automatically synchronizes toosample related events.</span></span> 

<span data-ttu-id="4bd0b-290">*Her zaman toosee istiyorum nadir belirli olaylar vardır. Nasıl bunları hello örnekleme modülü alabilirim?*</span><span class="sxs-lookup"><span data-stu-id="4bd0b-290">*There are certain rare events I always want toosee. How can I get them past hello sampling module?*</span></span>

* <span data-ttu-id="4bd0b-291">Yeni TelemetryConfiguration (Merhaba varsayılan etkin) ile TelemetryClient ayrı bir örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-291">Initialize a separate instance of TelemetryClient with a new TelemetryConfiguration (not hello default Active one).</span></span> <span data-ttu-id="4bd0b-292">Bu toosend nadir olaylarınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-292">Use that toosend your rare events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bd0b-293">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4bd0b-293">Next steps</span></span>
* <span data-ttu-id="4bd0b-294">[Filtreleme](app-insights-api-filtering-sampling.md) ne, SDK gönderir, daha katı denetim sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="4bd0b-294">[Filtering](app-insights-api-filtering-sampling.md) can provide more strict control of what your SDK sends.</span></span>

